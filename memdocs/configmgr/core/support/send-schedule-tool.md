---
title: Send Schedule Tool
titleSuffix: Configuration Manager
description: Mit dem Send Schedule Tool können Sie einen Zeitplan auf einem Konfigurations-Manager-Client auslösen.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d5ce547d-3b3b-47d3-bcd7-6ff94692c046
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 78e154c5361063224d9e8c99bc87ba117958edf4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707468"
---
# <a name="send-schedule-tool"></a>Send Schedule Tool

*Gilt für: Configuration Manager (Current Branch)*

Das Send Schedule Tool ist eines der [Configuration Manager-Tools](tools.md). Sie können mit dem Tool einen Zeitplan auf einem Client oder die Auswertung einer bestimmten Konfigurationsbaseline auslösen. Es kann für den lokalen Computer oder einen Remoteclient ausgeführt werden.  

Sie können das Tool beispielsweise verwenden, um einen Inventurzeitplan oder eine Konformitätsprüfung auszulösen. Wenn einige Konfigurations-Manager-Clients aktuell einen Inventur- oder Konformitätsstatus gemeldet haben, können Sie das Tool ausführen, um auf den einzelnen Clients den erforderlichen Zeitplan zu initiieren.



## <a name="usage"></a>Verwendung

Führen Sie **SendSchedule.exe** als Administrator aus. 

`SendSchedule /L [Computer Name]`
`SendSchedule "<Message GUID | DCM UID>" [Computer Name]` 

Nachdem Sie eine Nachricht (GUID) ausgelöst haben, finden Sie unter **SMSClientMethodProvider.log** weitere Informationen. Weitere Informationen zu verfügbaren Nachrichten-GUIDs finden Sie unter [Nachrichten-IDs](#bkmk_sendschedule-guids).

Nachdem Sie die Auswertung einer Konfigurationsbaseline (DCM-UID) ausgelöst haben, finden Sie unter **DCMAgent.log** weitere Informationen.



## <a name="command-line-options"></a>Befehlszeilenoptionen


### <a name="option-l"></a>Option: `/L` 
Listet sämtliche Nachrichten-GUIDs oder DCM-UIDs auf, die zum Senden verfügbar sind. Zeigt den aussagekräftigen Namen von Nachrichten in der Datentabelle an. Wenn der Computername nicht vorhanden ist, wird der lokale Computer verwendet. Wenn Sie eine Nachricht ohne einen Computernamen angeben, wird die Nachricht an den lokalen Computer gesendet. 



## <a name="examples"></a>Beispiele

#### <a name="list-the-available-messages-on-the-local-machine"></a>Liste der verfügbaren Nachrichten auf dem lokalen Computer 
`SendSchedule /L` 

#### <a name="list-the-available-messages-on-the-client-mypc"></a>Liste der verfügbaren Nachrichten auf dem Client „MyPC:“ 
`SendSchedule /L MyPC`

#### <a name="trigger-hardware-inventory-on-the-local-machine"></a>Auslösen der Hardwareinventur auf dem lokalen Computer
`SendSchedule {00000000-0000-0000-0000-000000000001}`

#### <a name="trigger-hardware-inventory-on-mypc"></a>Auslösen der Hardwareinventur auf „MyPC:“ 
`SendSchedule {00000000-0000-0000-0000-000000000001} MyPC` 

#### <a name="trigger-the-evaluation-of-a-specific-configuration-baseline-on-mypc"></a>Auslösen der Auswertung einer bestimmten Konfigurationsbaseline auf „MyPC:“ 
`SendSchedule ScopeId_611E8382-C064-4B62-B0DE-EFFB52AE8994/Baseline_36722778-69dd-4423-9632-b61148b2b67e MyPC` 



## <a name="message-ids"></a><a name="bkmk_sendschedule-guids"></a> Nachrichten-IDs

|Meldungs-ID  |Anzeigename  |
|---------|---------|
|{00000000-0000-0000-0000-000000000001}|Hardwareinventur|
|{00000000-0000-0000-0000-000000000002}|Softwareinventur|
|{00000000-0000-0000-0000-000000000003}|Discovery-Inventur|
|{00000000-0000-0000-0000-000000000010}|Dateisammlung|
|{00000000-0000-0000-0000-000000000011}|IDMIF-Sammlung|
|{00000000-0000-0000-0000-000000000021}|Anfordern von Computerzuweisungen|
|{00000000-0000-0000-0000-000000000022}|Auswerten von Computerrichtlinien|
|{00000000-0000-0000-0000-000000000023}|Aktualisieren von MP-Standardtasks|
|{00000000-0000-0000-0000-000000000024}|LS (Location Service, Ortsdienst) – Task zur Standortaktualisierung|
|{00000000-0000-0000-0000-000000000025}|LS (Location Service, Ortsdienst) – Task zur Zeitlimitaktualisierung|
|{00000000-0000-0000-0000-000000000026}|Richtlinien-Agent: Zuweisung von Anforderungen (Benutzer)|
|{00000000-0000-0000-0000-000000000027}|Richtlinien-Agent: Zuweisung von Auswertungen (Benutzer)|
|{00000000-0000-0000-0000-000000000031}|Verwendungsbericht zur Generierung von Softwaremessungen|
|{00000000-0000-0000-0000-000000000032}|Nachricht zur Aktualisierung der Quelle|
|{00000000-0000-0000-0000-000000000037}|Löschen des Zwischenspeichers für Proxyeinstellungen|
|{00000000-0000-0000-0000-000000000040}|Bereinigung des Computerrichtlinien-Agents|
|{00000000-0000-0000-0000-000000000041}|Bereinigung des Benutzerrichtlinien-Agents|
|{00000000-0000-0000-0000-000000000042}|Richtlinien-Agent: Richtlinie/Zuweisung zur Überprüfung von Computern|
|{00000000-0000-0000-0000-000000000043}|Richtlinien-Agent: Richtlinie/Zuweisung zur Überprüfung von Benutzern|
|{00000000-0000-0000-0000-000000000051}|Wiederholung/Aktualisierung von Zertifikaten in AD in MP|
|{00000000-0000-0000-0000-000000000061}|Statusberichte zu Peer-DP|
|{00000000-0000-0000-0000-000000000062}|Zeitplan zur Überprüfung ausstehender Pakete des Peer-DP|
|{00000000-0000-0000-0000-000000000063}|Zeitplan zur Installation von SUM-Updates|
|{00000000-0000-0000-0000-000000000101}|Hardwareinventur-Sammlungszyklus|
|{00000000-0000-0000-0000-000000000102}|Softwareinventur-Sammlungszyklus|
|{00000000-0000-0000-0000-000000000103}|Ermittlungsdaten-Sammlungszyklus|
|{00000000-0000-0000-0000-000000000104}|Dateisammlungszyklus|
|{00000000-0000-0000-0000-000000000105}|IDMIF-Sammlungszyklus|
|{00000000-0000-0000-0000-000000000106}|Berichtzyklus für Softwaremessungsnutzung|
|{00000000-0000-0000-0000-000000000107}|Updatezyklus für Windows Installer-Quellliste|
|{00000000-0000-0000-0000-000000000108}|Auswertungszyklus bei Zuweisungen von Aktionen für Softwareupdaterichtlinien|
|{00000000-0000-0000-0000-000000000109}|Zweigverteilungspunkt-Wartungstask für Richtlinien für die PDP-Wartung|
|{00000000-0000-0000-0000-000000000110}|DCM-Richtlinie|
|{00000000-0000-0000-0000-000000000111}|Nicht gesendete Zustandsmeldungen senden|
|{00000000-0000-0000-0000-000000000112}|Bereinigung des Richtliniencache des Zustandssystems|
|{00000000-0000-0000-0000-000000000113}|Quellenrichtlinie aktualisieren|
|{00000000-0000-0000-0000-000000000114}|Store-Richtlinie aktualisieren|
|{00000000-0000-0000-0000-000000000115}|Massensenden der Zustandssystemrichtlinie (hoch)|
|{00000000-0000-0000-0000-000000000116}|Massensenden der Zustandssystemrichtlinie (niedrig)|
|{00000000-0000-0000-0000-000000000121}|Richtlinienaktion des Anwendungs-Managers|
|{00000000-0000-0000-0000-000000000122}|Benutzerrichtlinienaktion des Anwendungs-Managers|
|{00000000-0000-0000-0000-000000000123}|Globale Aktion zur Auswertung des Anwendungs-Managers|
|{00000000-0000-0000-0000-000000000131}|Zusammenfassung des Energieverwaltungsstarts|
|{00000000-0000-0000-0000-000000000221}|Neuauswertung der Endpunktbereitstellung|
|{00000000-0000-0000-0000-000000000222}|Neuauswertung der Endpunkt-AM-Richtlinie|
|{00000000-0000-0000-0000-000000000223}|Erkennung externer Ereignisse|



