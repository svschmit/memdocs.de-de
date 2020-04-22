---
title: SQL-Replikation
titleSuffix: Configuration Manager
description: Anhand dieses Diagramms können Sie die Problembehandlung für die SQL-Replikation zwischen Configuration Manager-Standorten starten.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: adb198c4-da3c-49c3-8fbd-6d1361272869
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a25218e53313b7a8c3192959b54b65d2a32fae7d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81699858"
---
# <a name="sql-replication"></a>SQL-Replikation

In einer Hierarchie mit mehreren Standorten verwendet Configuration Manager die SQL-Replikation zum Übertragen von Daten zwischen Standorten. Weitere Informationen finden Sie unter [Datenbankreplikation](../../../plan-design/hierarchy/database-replication.md).

Anhand des folgenden Diagramms können Sie die Problembehandlung bei der SQL-Replikation starten, wenn bei einem Link ein Fehler auftritt:

![Diagramm zur Problembehandlung bei der SQL-Replikation](media/sql-replication.svg)

## <a name="queries"></a>Abfragen

In diesem Diagramm werden die folgenden Abfragen verwendet:

### <a name="check-if-the-replication-group-link-is-in-degraded-or-failed-state"></a>Überprüfen, ob der Link für die Replikationsgruppe heruntergestuft wurde oder einen Fehler aufweist

```sql
SELECT * FROM RCM_ReplicationLinkStatus
WHERE Status IN (8, 9)
```

### <a name="check-if-replication-group-link-is-recently-calculated"></a>Überprüfen, ob der Link für die Replikationsgruppe vor Kurzem berechnet wurde

```sql
DECLARE @cutoffTime DATETIME
SELECT @cutoffTime = DATEADD(minute, -30, GETUTCDATE())
SELECT * FROM RCM_ReplicationLinkStatus
WHERE UpdateTime >@cutoffTime
```

### <a name="check-sql-maintenance-mode"></a>SQL-Wartungsmodus überprüfen

```sql
SELECT * FROM ServerData
WHERE Status = 120
```

## <a name="next-steps"></a>Nächste Schritte

- [Neuinitialisierung der SQL-Replikation (wiederherstellen)](sql-replication-reinit.md)
- [SQL-Leistung](sql-performance.md)
- [SQL-Konfiguration](sql-configuration.md)
