---
title: Behandeln von Problemen mit Geräte Aktionen
titleSuffix: Configuration Manager
description: Behandeln von Problemen mit Geräte Aktionen Technische Referenz für Configuration Manager
ms.date: 04/01/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 44c2eb8a-3ccc-471f-838b-55d7971bb79e
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 72da589a3f4213fb64b4123d5580cb1be945de0e
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "82140275"
---
# <a name="troubleshooting-device-actions-for-configuration-manager-devices"></a>Problembehandlung bei Geräte Aktionen für Configuration Manager Geräte

*Gilt für: Configuration Manager (Current Branch)*

Ab Configuration Manager 2002 können Configuration Manager Clients mit dem Microsoft Endpoint Manager Admin Center synchronisiert werden. Einige Client Aktionen können über das Microsoft Endpoint Manager Admin Center auf den synchronisierten Clients ausgeführt werden.

Die verfügbaren Aktionen sind:
- Synchronisierungs Computer Richtlinie
- Benutzer Richtlinie synchronisieren
- App-Evaluierungszeitraum


[![Geräte Übersicht im Microsoft Endpoint Manager Admin Center](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)
  
Wenn ein Administrator eine Aktion über das Microsoft Endpoint Manager Admin Center ausführt, wird die Benachrichtigungs Anforderung an Configuration Manager Standort und von der Website an den Client weitergeleitet.

## <a name="configuration-manager-components"></a>Configuration Manager Komponenten

- **SMS_SERVICE_CONNECTOR**: verwendet den gatewaybenachrichtigungs-Worker für die Verarbeitung der Benachrichtigung vom Microsoft Endpoint Manager Admin Center.
- **SMS_NOTIFICATION_SERVER**: Ruft die Benachrichtigung ab und erstellt eine Client Benachrichtigung.
- **Bgbagent**: der Client ruft die Aufgabe ab und führt die angeforderte Aktion aus.

## <a name="sms_service_connector"></a>SMS_SERVICE_CONNECTOR

Wenn eine Aktion vom Microsoft Endpoint Manager Admin Center initiiert wird, verarbeitet **cmgatewaynotificationworker. log** die Anforderung.  

```text
Received new notification. Validating basic notification details...
Validating device action message content...
Authorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID:     a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2
Forwarded BGB remote task. TemplateID: 1 TaskGuid: a43dd1b3-a006-4604-b012-5529380b3b6f TaskParam: TargetDeviceIDs: 1  
```
 
1. Vom Microsoft Endpoint Manager Admin Center wird eine Benachrichtigung empfangen.

   ```text
   Received new notification. Validating basic notification details..
   ```

1. Benutzer-und Geräte Aktionen werden überprüft.

   ```text
   Validating device action message content... 
   Authorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID:     a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2
   ```

1. Der Remote Task wird an den SMS_NOTIFICATION_SERVER weitergeleitet.

    ```text
   Forwarded BGB remote task. TemplateID: 1 TaskGuid: a43dd1b3-a006-4604-b012-5529380b3b6f TaskParam: TargetDeviceIDs: 1  
    ```


## <a name="sms_notification_server"></a>SMS_NOTIFICATION_SERVER

Nachdem die Nachricht an den SMS_NOTIFICATION_SERVER gesendet wurde, wird eine Aufgabe vom Verwaltungspunkt an den entsprechenden Client gesendet. Sie sehen den folgenden Befehl in der **Datei "bgbserver. log**", die sich auf dem Verwaltungspunkt befindet:

```text
Get one push message from database.
Starting to send push task (PushID: 7 TaskID: 8 TaskGUID: A43DD1B3-A006-4604-B012-5529380B3B6F TaskType: 1 TaskParam: ) to 1 clients  with throttling (strategy: 1 param: 42)
```

## <a name="bgbagent"></a>Bgbagent

Der letzte Schritt tritt auf dem Client auf und kann in der **Datei "ccmnotificationagent. log**" angezeigt werden. Nachdem die Aufgabe empfangen wurde, fordert Sie den Scheduler auf, die Aktion auszuführen. Wenn die Aktion ausgeführt wird, wird eine Bestätigungsmeldung angezeigt:

```text
Receive task from server with pushid=7, taskid=8, taskguid=A43DD1B3-A006-4604-B012-5529380B3B6F, tasktype=1 and taskParam=

Send Task response message <BgbResponseMessage TimeStamp="2020-01-21T15:43:43Z"><PushID>8</PushID><TaskID>9</TaskID><ReturnCode>1</ReturnCode></BgbResponseMessage> successfully.
```

## <a name="common-issues"></a>Häufige Probleme

Wenn der Administrator in Configuration Manager nicht über die erforderlichen Berechtigungen verfügt, wird in der `Unauthorized` **Datei "cmgatewaynotificationworker. log**" eine Antwort angezeigt.

```text
Received new notification. Validating basic notification details..
Validating device action message content...
Unauthorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID: 3a1e89e6-e190-4615-9d38-a208b0eb1c78
```  

Stellen Sie sicher, dass der Benutzer, der die Aktion aus dem Microsoft Endpoint Manager Admin Center ausgeführt hat, über die erforderlichen Berechtigungen auf Configuration Manager Website verfügt Weitere Informationen finden Sie unter [Voraussetzungen für den Microsoft Endpoint Manager-Mandanten anfügen](device-sync-actions.md#prerequisites).

## <a name="next-steps"></a>Nächste Schritte

[Aktivieren Sie die Co-Verwaltung](../comanage/overview.md) , um zusätzliche cloudgestützte Funktionen wie den bedingten Zugriff zu erhalten.
