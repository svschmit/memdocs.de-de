---
title: Wiederherstellung von Standortdaten
titleSuffix: Configuration Manager
description: Anhand dieses Diagramms können Sie die Problembehandlung bei der Wiederherstellung der SQL-Replikation für Standortdaten in einer Configuration Manager-Hierarchie starten
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 19741d45-2d42-438e-a9f3-15bb365d63ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6a336bdf323fbb81a16082e9c308577763a7c104
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078588"
---
# <a name="troubleshoot-site-data-reinit"></a>Problembehandlung bei der Wiederherstellung von Standortdaten

In einer Hierarchie mit mehreren Standorten verwendet Configuration Manager die SQL-Replikation zum Übertragen von Daten zwischen Standorten. Weitere Informationen finden Sie unter [Datenbankreplikation](../../../plan-design/hierarchy/database-replication.md).

Anhand des folgenden Diagramms können Sie die Problembehandlung bei der Wiederherstellung der SQL-Replikation für Standortdaten in einer Configuration Manager-Hierarchie starten:

![Diagramm zur Problembehandlung bei der Wiederherstellung von Standortdaten](media/site-data-reinit.svg)

## <a name="queries"></a>Abfragen

In diesem Diagramm werden die folgenden Abfragen verwendet:

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>Überprüfen, ob die Wiederherstellung der Standortreplikation noch nicht abgeschlossen wurde

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Site'
```

### <a name="get-the-trackingguid--status-from-the-cas"></a>TrackingGuid & Status vom primären CAS abrufen

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'Site'
```

### <a name="get-the-trackingguid--status-from-the-primary-site"></a>TrackingGuid & Status vom primären Standort abrufen

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

### <a name="check-primary-site-isnt-in-maintenance-mode"></a>Vergewissern, dass sich der primäre Standort nicht im Wartungsmodus befindet

```sql
SELECT * FROM ServerData
WHERE SiteStatus = 125
AND SiteCode=dbo.fnGetSiteCode()
AND ServerRole=N'Peer'
```

### <a name="check-request-status-for-the-tracking-id"></a>Anforderungsstatus für die Überwachungs-ID überprüfen

```sql
SELECT Status FROM RCM_InitPackageRequest
WHERE RequestTrackingGUID=@trackGuid
```

## <a name="next-steps"></a>Nächste Schritte

- [Wiederherstellung der fehlenden Meldung](reinit-missing-message.md)
- [Globale Datenwiederherstellung](global-data-reinit.md)
