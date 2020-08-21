---
title: Configuration Manager-Tools
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über Tools, die Sie bei der Verwaltung und Problembehandlung Ihrer Configuration Manager-Infrastruktur unterstützen.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 395403dc-6997-4415-93fd-6b1eeb6ba31a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cb2529dbbe923a5035f0b7586dab696cd6fc917e
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699414"
---
# <a name="configuration-manager-tools"></a>Configuration Manager-Tools

*Gilt für: Configuration Manager (Current Branch)*

Die Configuration Manager-Tools umfassen [clientbasierte](#client-tools) und [serverbasierte](#server-tools) Tools. Verwenden Sie diese Tools, um Ihre Configuration Manager-Infrastruktur zu unterstützen und Probleme zu behandeln.

Ab Configuration Manager Version 1806 sind diese Tools auf dem Standortserver im Ordner `CD.Latest\SMSSETUP\Tools` enthalten. Es ist keine weitere Installation erforderlich.<!--1357145--> Verwenden Sie für Configuration Manager Version 1806 und höher diese Version der Tools.

Für alle Windows-Betriebssysteme, die unter [Unterstützte Betriebssysteme für Clients und Geräte](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices) als unterstützte Clients aufgeführt sind, wird die Verwendung dieser Tools unterstützt.

> [!Note]  
> Das [System Center 2012 R2 Configuration Manager Toolkit](https://www.microsoft.com/download/details.aspx?id=50012) steht noch über Microsoft Download Center zur Verfügung. Verwenden Sie für Configuration Manager Version 1806 und höher die Versionen der Tools im Ordner „CD.Latest“ auf dem Standortserver. Einige Tools, die vorher im Toolkit enthalten waren, sind in Version 1806 nicht verfügbar. Diese älteren Tools werden nicht mehr unterstützt.


## <a name="client-tools"></a>Clienttools

Diese Tools befinden sich im Unterordner `ClientTools`:

- [CMTrace](cmtrace.md): Anzeigen, Überwachen und Analysieren von Configuration Manager-Protokolldateien  

- [Client Spy](clispy.md): Behandeln von Problemen im Zusammenhang mit Softwareverteilung, -inventur und -messung

- [Deployment Monitoring Tool](deployment-monitoring-tool.md) (Tool zur Überwachung der Bereitstellung): Problembehandlung bei Anwendungen, Updates und Basislinienbereitstellungen  

- [Policy Spy](policy-spy.md) (Richtlinien-Spion): Anzeigen von Richtlinienzuweisungen  

- [Power Viewer Tool](power-viewer-tool.md) (Tool für die Energieanzeige): Anzeigen des Status der Energieverwaltungsfunktion  

- [Send Schedule Tool (Tool zum Senden von Zeitplänen)](send-schedule-tool.md): Auslösen von Zeitplänen und Auswertungen von Konfigurationsbaselines  

> [!Note]  
> Der Ordner `ClientTools` enthält auch die Datei Microsoft.Diagnostics.Tracing.EventSource.dll“. Mehrere Clienttools erfordern diese Bibliothek. Sie können sie nicht direkt verwenden.  


## <a name="server-tools"></a>Servertools

Diese Tools befinden sich im Unterordner `ServerTools`:

- [DP Job Queue Manager (Warteschlangen-Manager für Verteilungspunktaufträge)](dp-job-manager.md): Beheben von Problemen bei Inhaltsverteilungsaufträgen zu Verteilungspunkten  

- [Collection Evaluation Viewer](ceviewer.md) (Sammlungsauswertungs-Viewer): Anzeigen von Details der Sammlungsauswertung  

- [Content Library Explorer](content-library-explorer.md) (Inhaltsbibliothek-Explorer): Anzeigen des Single Instance Store der Inhaltsbibliothek  

- [Content Library Transfer](content-library-transfer.md) (Inhaltsbibliotheksübertragung): Übertragen von Inhaltsbibliotheken zwischen Laufwerken  

- [Content Ownership Tool](content-ownership-tool.md) (Tool für den Inhaltsbesitz): Ändern des Besitzes von verwaisten Paketen. Diese Pakete sind am Standort ohne besitzenden Standortserver vorhanden.

- [Role-based Administration and Auditing Tool](rbaviewer.md) (Tool für die rollenbasierte Verwaltung und Überwachung): Unterstützung für Administratoren bei der Überwachung der Rollenkonfiguration  

- [Run Meter Summarization Tool (Tool für die Zusammenfassung von Verbrauchseinheiten für Ausführungen)](run-meter-summ.md): Ausführen des Zusammenfassungstasks der Messung und Analysieren von Messungsdaten

> [!Note]  
> Der Ordner „ServerTools“ enthält zusätzlich die folgenden Dateien:
>
> - AdminUI.WqlQueryEngine.dll
> - Microsoft.ConfigurationManagement.ManagementProvider.dll
> - Microsoft.Diagnostics.Tracing.EventSource.dll
>
> Mehrere Servertools erfordern diese Bibliotheken. Sie können sie nicht direkt verwenden.  

## <a name="other-tools-and-toolkits"></a>Weitere Tools und Toolkits

- [Supportcenter](support-center.md): Erfassen Sie Informationen von Clients, um die Analyse bei der Problembehandlung zu erleichtern.

    Ab Version 1906 ist **OneTrace** als neue Protokollanzeige im Supportcenter verfügbar. Die Funktionsweise ähnelt der von CMTrace, bietet jedoch einige Verbesserungen. Weitere Informationen finden Sie unter [Supportcenter – OneTrace](support-center-onetrace.md).

- [Erweitern und Migrieren eines lokalen Standorts zu Microsoft Azure:](azure-migration-tool.md) Dieses Tool unterstützt Sie dabei, Azure-VMs für Configuration Manager programmgesteuert zu erstellen. <!--3556022--> 

- [Inhaltsbibliothek-Bereinigungstool](../plan-design/hierarchy/content-library-cleanup-tool.md): Verwenden Sie **ContentLibraryCleanup.exe** in `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup`, um verwaisten Inhalt von einem Verteilungspunkt zu entfernen.  

- [Hierarchiewartungstool](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md): Verwenden Sie **Preinst.exe** im freigegebenen Ordner `\<SiteServerName>\SMS_<SiteCode>\bin\X64\00000409` auf dem Standortserver, um Befehle an die Hierarchie-Manager-Komponente weiterzugeben.  

- [Tool zum Zurücksetzen von Updates](../servers/manage/update-reset-tool.md): Verwenden Sie **CMUpdateReset.exe** in `CD.Latest\SMSSETUP\TOOLS\CMUpdateReset`, um Probleme zu beheben, wenn konsoleninterne Updates Probleme beim Herunterladen oder Replizieren haben.  

- [Dienstverbindungstool](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md): Verwenden Sie **ServiceConnectionTool.exe** in `CD.Latest\SMSSETUP\TOOLS\ServiceConnectionTool`, um Ihren Standort auf dem neuesten Stand zu halten, wenn Ihr Dienstverbindungspunkt offline ist.   

- [Microsoft Deployment Toolkit (MDT)](../../mdt/use-the-mdt.md): Eine einheitliche Sammlung von Tools, Prozessen und Leitfäden für die automatisierte Bereitstellung von Desktop- und Serverbetriebssystemen.

- [System Center Updates Publisher (SCUP)](../../sum/tools/updates-publisher.md): Ein eigenständiges Tool zum Verwalten und Importieren von Updates für benutzerdefinierte Software.

- [Paketkonvertierungs-Manager](../../apps/pcm/package-conversion-manager.md): Konvertieren Sie Legacypakete in Anwendungen.