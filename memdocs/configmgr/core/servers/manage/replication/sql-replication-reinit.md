---
title: Wiederherstellung der SQL-Replikation
titleSuffix: Configuration Manager
description: Anhand dieses Diagramms können Sie die Problembehandlung für die Wiederherstellung der SQL-Replikation zwischen Configuration Manager-Standorten starten.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ce4a1ca8-6433-4447-819f-19dd5faa6f46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f6207ed4eeeef892de38c85096d2cc80189214d1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078554"
---
# <a name="sql-replication-reinit"></a>Wiederherstellung der SQL-Replikation

In einer Hierarchie mit mehreren Standorten verwendet Configuration Manager die SQL-Replikation zum Übertragen von Daten zwischen Standorten. Weitere Informationen finden Sie unter [Datenbankreplikation](../../../plan-design/hierarchy/database-replication.md).

Anhand dieses Diagramms können Sie die Problembehandlung für die Wiederherstellung der SQL-Replikation starten:

![Diagramm zur Problembehandlung bei der Wiederherstellung der SQL-Replikation](media/sql-replication-reinit.svg)

## <a name="queries"></a>Abfragen

In diesem Diagramm werden die folgenden Abfragen verwendet:

### <a name="check-if-site-is-in-maintenance-mode"></a>Überprüfen, ob der Standort sich im Wartungsmodus befindet

```sql
SELECT * FROM ServerData
WHERE Status = 120
```

### <a name="check-which-replication-group-hasnt-completed-reinit"></a>Überprüfen, bei welcher Replikationsgruppe die Wiederherstellung nicht abgeschlossen wurde

```sql
SELECT * FROM RCM_DrsInitializationTracking
WHERE InitializationStatus NOT IN (6,7)
```

### <a name="check-global-data"></a>Globale Daten überprüfen

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'GLOBAL'
```

### <a name="check-site-data"></a>Standortdaten überprüfen

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'Site'
```

## <a name="next-steps"></a>Nächste Schritte

- [Globale Datenwiederherstellung](global-data-reinit.md)
- [Wiederherstellung von Standortdaten](site-data-reinit.md)
- [SQL-Konfiguration](sql-configuration.md)
