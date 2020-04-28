---
title: Technische Referenz zur Problembehandlung bei der Bereitstellung einer Anwendung
titleSuffix: Configuration Manager
description: Technische Referenz zur Problembehandlung bei Anwendungsbereitstellung in Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: a4eb09c8-e570-4369-9adb-ded9c8ad3400
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5b3513131b73ac2b63cf18f31b1e39e15ee97420
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688868"
---
# <a name="technical-reference-for-application-deployment-in-configuration-manager"></a>Technische Referenz für die Anwendungsbereitstellung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

In diesem Artikel erfahren Sie, wie Anwendungsbereitstellungen funktionieren.

## <a name="before-you-begin"></a>Vorbereitungen

Bei der Problembehandlung von Anwendungsbereitstellungen gibt es mehrere Elemente, die beim Überprüfen von Clientprotokollen hilfreich sein können. Zu diesen Elementen gehören:

- Anwendungs-CI-ID
- Eindeutige Anwendungs-ID
- Eindeutige Bereitstellungstyp-ID
- Eindeutige ID der Anwendungsbereitstellung (wird auch als eindeutige Zuweisungs-ID bezeichnet)
- Zweck der Anwendungsbereitstellung
- Eindeutige Inhalts-ID
- Sammlungs-ID und Name
- Sammlungstyp

Zur Vereinfachung der Problembehandlung können Sie eine SQL-Abfrage wie die nachfolgende mit der Configuration Manager-Datenbank ausführen, um die oben aufgeführten Informationen zu erhalten.

```sql
SELECT APP.CI_ID [App CI ID], APP.CI_UniqueID [App Unique ID], APP.DisplayName [App Name],
DT.CI_UniqueID [DT Unique ID], DT.ContentId [DT Content ID],
CIA.Assignment_UniqueID [Assignment ID], CIA.CollectionID, CIA.CollectionName,
CASE CIA.OfferTypeID WHEN 0 THEN 'Required' WHEN 2 THEN 'Available' WHEN 3 THEN 'Simulate' ELSE 'Unknown' END AS [Deployment Purpose],
CASE C.CollectionType WHEN 1 THEN 'User Collection' WHEN 2 THEN 'Device Collection' ELSE 'Unknown' END AS [Collection Type],
DT.Technology, DT.DisplayName [DT Name]
FROM fn_ListApplicationCIs(1033) APP
JOIN fn_ListDeploymentTypeCIs(1033) DT ON DT.AppModelName = APP.ModelName AND DT.IsLatest = 1
LEFT JOIN v_CIAssignmentToCI CIACI ON CIACI.CI_ID = APP.CI_ID
LEFT JOIN v_CIAssignment CIA ON CIACI.AssignmentID = CIA.AssignmentID
LEFT JOIN v_Collection C ON C.CollectionID = CIA.CollectionID
WHERE APP.IsLatest = 1 AND APP.DisplayName = 'Application Name' -- Replace Application Name
```

> [!IMPORTANT]
> Wenn Sie diese Abfrage ausführen, **müssen** Sie den Anwendungsnamen verwenden, der auf der Registerkarte „Allgemeine Informationen“ der Anwendungseigenschaften aufgeführt ist, anstatt den Namen der lokalisierten Anwendung zu verwenden, der auf der Registerkarte „Softwarecenter“ der Anwendungseigenschaften aufgeführt ist.

## <a name="next-steps"></a>Nächste Schritte

- [Anwendungsbereitstellungsrichtlinie](deployment-policy-technical-reference.md)
