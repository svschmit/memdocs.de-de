---
title: Wiederherstellung der fehlenden Meldung
titleSuffix: Configuration Manager
description: Anhand dieses Diagramms können Sie die Problembehandlung bei einer fehlenden Meldung mit der Wiederherstellung der SQL-Replikation in Configuration Manager starten.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 39a3001e-2df5-4b36-bd83-4f1d21dda335
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1e640c3dd756d96a58e8b54d6056d2adbb7bb99c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703978"
---
# <a name="reinit-missing-message"></a>Wiederherstellung der fehlenden Meldung

In einer Hierarchie mit mehreren Standorten verwendet Configuration Manager die SQL-Replikation zum Übertragen von Daten zwischen Standorten. Weitere Informationen finden Sie unter [Datenbankreplikation](../../../plan-design/hierarchy/database-replication.md).

Anhand dieses Diagramms können Sie die Problembehandlung bei einer fehlenden Meldung mit der Wiederherstellung der SQL-Replikation starten:

![Diagramm zur Problembehandlung bei der Wiederherstellung fehlender Meldungen](media/reinit-missing-message.svg)

## <a name="queries"></a>Abfragen

In diesem Diagramm werden die folgenden Abfragen verwendet:

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>Überprüfen, ob die Wiederherstellung der Standortreplikation noch nicht abgeschlossen wurde

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
```

### <a name="get-the-trackingguid--status-from-subscriber-site"></a>TrackingGuid & Status vom Abonnentenstandort abrufen

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
```

### <a name="get-the-trackingguid--status-from-the-publishing-site"></a>TrackingGuid & Status vom veröffentlichenden Standort abrufen

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

## <a name="remediation-actions"></a>Wiederherstellungsmaßnahmen

### <a name="version-1902-and-later"></a>Version 1902 und höher

Führen Sie die [Replikationslinkanalyse](../monitor-replication.md#BKMK_RLA)aus, um das Problem zu ermitteln und die Wiederherstellung durchzuführen.

### <a name="version-1810-and-earlier"></a>Version 1810 und älter

Führen Sie die folgende SQL-Abfrage aus, um die `ReplicationGroupID` abzurufen:

```sql
SELECT rd.ID AS ReplicationGroupID from ReplicationData rd
INNER JOIN RCM_DrsInitializationTracking it ON rd.ReplicationGroup = it.ReplicationGroup
WHERE it.RequestTrackingGUID=@trackingGuid
```

Verwenden Sie dann die `InitializeData`-Methode in der `SMS_ReplicationGroup`-WMI-Klasse mit den folgenden Werten:

- ReplicationGroupID: aus der SQL-Abfrage oben
- SiteCode1: übergeordneter Standort
- SiteCode2: untergeordneter Standort

Weitere Informationen finden Sie unter [InitializeData method in class SMS_ReplicationGroup (InitializeData-Methode in der Klasse „SMS_ReplicationGroup“)](../../../../develop/reference/core/servers/configure/initializedata-method-in-class-sms_replicationgroup.md).

#### <a name="example"></a>Beispiel

```PowerShell
Invoke-WmiMethod –Namespace "root\sms\site_CAS" -Class SMS_ReplicationGroup –Name InitializeData -ArgumentList "20", "CAS", "PR1"
```

## <a name="next-steps"></a>Nächste Schritte

- [Neuinitialisierung der SQL-Replikation (wiederherstellen)](sql-replication-reinit.md)
