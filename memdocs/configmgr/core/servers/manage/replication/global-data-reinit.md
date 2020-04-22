---
title: Globale Datenwiederherstellung
titleSuffix: Configuration Manager
description: Anhand dieses Diagramms können Sie die Problembehandlung bei der Wiederherstellung der SQL-Replikation für globale Daten in einer Configuration Manager-Hierarchie starten.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d36622c0-776c-493b-971a-4a586fc394d4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9fed8a5b257591aa95fcd53b4e12a82249fce762
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694298"
---
# <a name="troubleshoot-global-data-reinit"></a>Behandeln von Problemen bei der Wiederherstellung globaler Daten

In einer Hierarchie mit mehreren Standorten verwendet Configuration Manager die SQL-Replikation zum Übertragen von Daten zwischen Standorten. Weitere Informationen finden Sie unter [Datenbankreplikation](../../../plan-design/hierarchy/database-replication.md).

Anhand des folgenden Diagramms können Sie die Problembehandlung bei der Wiederherstellung der SQL-Replikation für globale Daten in einer Configuration Manager-Hierarchie starten:

![Diagramm zur Problembehandlung bei der Wiederherstellung globaler Daten](media/global-data-reinit.svg)

## <a name="queries"></a>Abfragen

In diesem Diagramm werden die folgenden Abfragen verwendet:

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>Überprüfen, ob die Wiederherstellung der Standortreplikation noch nicht abgeschlossen wurde

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Global'
```

### <a name="get-the-trackingguid--status-from-the-primary-site"></a>TrackingGuid & Status vom primären Standort abrufen

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Global'
```

### <a name="get-the-trackingguid--status-from-the-cas"></a>TrackingGuid & Status vom primären CAS abrufen

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

### <a name="check-request-status-for-the-tracking-id"></a>Anforderungsstatus für die Überwachungs-ID überprüfen

```sql
SELECT Status FROM RCM_InitPackageRequest
WHERE RequestTrackingGUID=@trackGuid
```

## <a name="next-steps"></a>Nächste Schritte

- [Wiederherstellung der fehlenden Meldung](reinit-missing-message.md)
