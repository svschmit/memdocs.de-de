---
title: SQL-Leistung
titleSuffix: Configuration Manager
description: Anhand dieses Diagramms können Sie die Problembehandlung der SQL-Leistung für Configuration Manager starten.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9930a8a4-4d7f-47a4-bf6b-4c36d0ed5528
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4e492b4495e811b21eb582de7314d2ef41241775
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695718"
---
# <a name="sql-performance"></a>SQL-Leistung

In einer Hierarchie mit mehreren Standorten verwendet Configuration Manager die SQL-Replikation zum Übertragen von Daten zwischen Standorten. Weitere Informationen finden Sie unter [Datenbankreplikation](../../../plan-design/hierarchy/database-replication.md).

Verwenden Sie das folgende Diagramm, um die Problembehandlung für die SQL-Leistung zu starten. Diese kann Auswirkungen auf den Replikationsstatus haben.

![Diagramm zur Problembehandlung für die SQL-Leistung](media/sql-performance.png)

<!-- PNG used instead of SVG because the SQL statements wrap weird in the SVG. The SVG file exists in the same location. -->

## <a name="queries"></a>Abfragen

In diesem Diagramm werden die folgenden Abfragen verwendet:

### <a name="make-sure-sql-change-tracking-table-is-cleaned-up"></a>Sicherstellen, dass die SQL-Änderungsnachverfolgungstabelle bereinigt wurde

```sql
DECLARE @RetentionUnit INT = 0;
DECLARE @RetentionPeriod INT = 0;
DECLARE @CTCutOffTime DATETIME;
DECLARE @CTMinTime DATETIME;

SELECT @RetentionPeriod=retention_period,  
    @RetentionUnit=retention_period_units  
FROM sys.change_tracking_databases  
WHERE database_id = DB_ID();

IF @RetentionUnit = 1
    SET @CTCutOffTime = DATEADD(MINUTE,-@RetentionPeriod,GETUTCDATE())
ELSE IF @RetentionUnit = 2
    SET @CTCutOffTime = DATEADD(HOUR,-@RetentionPeriod,GETUTCDATE())
ELSE IF @RetentionUnit = 3
    SET @CTCutOffTime = DATEADD(DAY,-@RetentionPeriod,GETUTCDATE())

-- give a buffer of two days
SET @CTCutOffTime = DATEADD(DAY, -2, @CTCutOffTime)
select top 1 @CTMinTime=commit_time from sys.dm_tran_commit_table order by commit_ts asc
IF @CTMinTime < @CTCutOffTime
    PRINT 'there is change tracking backlog, please contact Microsoft support'
```

### <a name="change-current-sessions-that-handle-sql-service-broker-messages-are-blocked"></a>Überprüfen, dass aktuelle Sitzungen, die SQL Service Broker-Nachrichten verarbeiten, blockiert sind

```sql
select
       req.session_id
       ,req.blocking_session_id
       ,req.last_wait_type
       ,req.wait_type
       ,req.wait_resource
       ,t.text
from sys.dm_exec_sessions s
inner join sys.dm_exec_requests req on s.Session_id=req.session_id
cross apply sys.dm_exec_sql_text(sql_handle) t
where program_name='SMS_data_replication_service'
```

### <a name="check-sessions-asking-too-much-memory"></a>Sitzungen überprüfen, die zu viel Speicher anfordern

```sql
SELECT * FROM sys.dm_exec_query_memory_grants
ORDER BY requested_memory_kb DESC
```

### <a name="check-sessions-taking-too-many-locks"></a>Sitzungen überprüfen, die zu viele Sperrungen anfordern

```sql
SELECT TOP 10 request_session_id,
program_name = (SELECT program_name FROM sys.dm_exec_sessions WHERE session_id=request_session_id),
COUNT (*) num_locks
FROM sys.dm_tran_locks
GROUP BY request_session_id
ORDER BY count (*) DESC
```

## <a name="see-also"></a>Weitere Informationen:

[SQL-Konfiguration](sql-configuration.md)
