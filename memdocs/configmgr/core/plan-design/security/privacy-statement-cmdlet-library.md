---
title: Datenschutzbestimmungen für Cmdlets
titleSuffix: Configuration Manager
description: Erfahren Sie mehr darüber, wie Microsoft Daten zur Configuration Manager-Cmdlets sammelt und verwendet.
ms.date: 01/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 551a8086894f877d07c57fbe2848c2befacfc5b5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695748"
---
# <a name="configuration-manager-cmdlet-library-privacy-statement"></a>Datenschutzbestimmungen: Cmdlet-Bibliothek für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Diese Datenschutzbestimmungen gelten für die Features der Configuration Manager-Cmdlet-Bibliothek.  

## <a name="usage-data"></a>Nutzungsdaten  

#### <a name="what-this-feature-does"></a>Leistungsumfang der Funktion

Mit der Configuration Manager-Cmdlet-Bibliothek können Sie eine Configuration Manager-Hierarchie mithilfe von Windows PowerShell-Cmdlets und -Skripts verwalten. Von der Cmdlet-Bibliothek werden Informationen darüber gesammelt, wie Sie die Cmdlets in der Bibliothek verwenden, um Trends und Verwendungsmuster zu ermitteln. Von der Cmdlet-Bibliothek werden auch Art und Anzahl der Fehler gesammelt, die beim Verwenden der Cmdlets auftreten.  

#### <a name="information-collected-processed-or-transmitted"></a>Erfasste, verarbeitete oder übertragene Informationen
   
Zu den gesammelten Nutzungsdaten gehören das Starten, Anhalten und Beenden von Cmdlets und das Ausführen von veralteten Cmdlets und Aktivitätsmetriken für Vorgänge im Zusammenhang mit Cmdlets, die mit SMS-Anbietern verknüpft sind. Diese Informationen sind nicht personenbezogen. Zu den gesammelten Informationen gehören u.a. die von Cmdlets zurückgegebenen Fehler sowie Details zu Ausnahmefehlern. Einige Detailberichte zu Fehlern enthalten möglicherweise unbeabsichtigt personenbezogene Daten, z.B. Seriennummern von Geräten, die mit dem Computer verbunden sind. Diese Informationen in den Fehlerberichten werden von der Cmdlet-Bibliothek gefiltert und anonymisiert, um etwaige persönliche Informationen vor der Übertragung an Microsoft zu entfernen.  

#### <a name="use-of-information"></a>Verwendung von Informationen
   
Microsoft verwendet diese Informationen zur Verbesserung der Qualität, der Sicherheit und der Integrität der angebotenen Produkte und Dienste.  

#### <a name="choicecontrol"></a>Auswahl- und Kontrollmöglichkeiten   

Das Feature zur Erfassung von Nutzungsdaten ist standardmäßig aktiviert. Die Configuration Manager-Cmdlet-Bibliothek umfasst zwei Registrierungsschlüssel zur Steuerung dieser Funktionalität.  

 Legen Sie die Werte dieser beiden Registrierungsschlüssel zur vollständigen Deaktivierung fest. Sie gelten für jeden der Event Tracing for Windows-Anbieter (ETW):  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0 (beendet die Erfassung von Nutzungsdaten für den Laufwerksanbieter)  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets:CeipLevel=0 (beendet die Erfassung von Nutzungsdaten für die Cmdlets)  

  Die Einstellungen für Nutzungsdaten gelten nur für den betreffenden Computer, auf dem sie festgelegt wurden.  


## <a name="next-steps"></a>Nächste Schritte

[Dokumentation zur Configuration Manager-Cmdlets-Bibliothek](https://docs.microsoft.com/powershell/sccm/configurationmanager/).   
