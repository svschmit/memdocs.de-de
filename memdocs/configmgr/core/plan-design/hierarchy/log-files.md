---
title: Protokolldateireferenz
titleSuffix: Configuration Manager
description: Dies ist eine Referenz zu sämtlichen Protokolldateien für Configuration Manager-Client und -Server sowie abhängigen Komponenten.
ms.date: 06/10/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c1ff371e-b0ad-4048-aeda-02a9ff08889e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 63f8ad6827a1aa72c3aaa51e21fecbf639fbb405
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715576"
---
# <a name="log-file-reference"></a>Protokolldateireferenz

*Gilt für: Configuration Manager (Current Branch)*

Von Client- und Standortserverkomponenten in Configuration Manager werden Prozessinformationen in eigenen Protokolldateien aufgezeichnet. Mithilfe der Informationen in diesen Protokolldateien können Sie eventuell auftretende Probleme beheben. Die Client- und Serverkomponentenprotokollierung ist in Configuration Manager standardmäßig aktiviert.

Allgemeinere Informationen zu Protokolldateien in Configuration Manager finden Sie unter [Grundlegendes zu Protokolldateien](about-log-files.md). Dieser Artikel enthält Informationen zu den zu verwendenden Tools. Außerdem wird beschrieben, wie Sie die Protokolle konfigurieren und wo diese zu finden sind.

In den folgenden Abschnitten finden Sie Details zu den verschiedenen verfügbaren Protokolldateien. Sie können die von Configuration Manager aufgezeichneten Client- und -Serverprotokolle überwachen und sich dadurch Vorgangsdetails anzeigen lassen. Die angezeigten Fehlerinformationen können Sie zur Problembehebung verwenden.  

- [Clientprotokolldateien](#BKMK_ClientLogs)  

  - [Clientvorgänge](#BKMK_ClientOpLogs)  

  - [Clientinstallation](#BKMK_ClientInstallLog)  

  - [Client für Linux und UNIX](#BKMK_LogFilesforLnU)  

  - [Client für Macintosh-Computer](#BKMK_LogfilesforMac)  

- [Serverprotokolldateien](#BKMK_ServerLogs)  

  - [Standortserver und Standortsysteme](#BKMK_SiteSiteServerLog)  

  - [Standortserverinstallation](#BKMK_SiteInstallLog)

  - [Data Warehouse-Dienstpunkt](#BKMK_DataWarehouse)

  - [Fallbackstatuspunkt](#BKMK_FSPLog)  

  - [Verwaltungspunkt](#BKMK_MPLog)  

  - [Dienstverbindungspunkt](#BKMK_WITLog)  

  - [Softwareupdatepunkt](#BKMK_SUPLog)  

- [Protokolldateien für Configuration Manager-Funktionen](#BKMK_FunctionLogs)  

  - [Anwendungsverwaltung](#BKMK_AppManageLog)  

  - [Asset Intelligence](#BKMK_AILog)  

  - [Sicherung und Wiederherstellung:](#BKMK_BnRLog)  

  - [Zertifikatregistrierung](#BKMK_CertificateEnrollment)

  - [Clientbenachrichtigung](#BKMK_BGB)

  - [Cloudverwaltungsgateway](#cloud-management-gateway)

  - [Konformitätseinstellungen und Zugriff auf Unternehmensressourcen](#BKMK_CompSettingsLog)  

  - [Configuration Manager-Konsole](#BKMK_ConsoleLog)  

  - [Content Management](#BKMK_ContentLog)  

  - [Desktop Analytics](#desktop-analytics)

  - [Ermittlung](#BKMK_DiscoveryLog)  

  - [Endpoint Protection](#BKMK_EPLog)  

  - [Erweiterungen](#BKMK_Extensions)  

  - [Inventur](#BKMK_InventoryLog)  

  - [Migration](#BKMK_MigrationLog)  

  - [Mobile Geräte](#BKMK_MDMLog)  

  - [Bereitstellung des Betriebssystems](#BKMK_OSDLog)  

  - [Energieverwaltung](#BKMK_PowerMgmtLog)  

  - [Remotesteuerung](#BKMK_RCLog)  

  - [Berichterstellung](#BKMK_ReportLog)  

  - [Rollenbasierte Verwaltung](#BKMK_RBALog)  

  - [Softwaremessung](#BKMK_MeteringLog)  

  - [Softwareupdates](#BKMK_SU_NAPLog)  

  - [Wake-On-LAN](#BKMK_WOLLog)  

  - [Windows 10-Wartung](#BKMK_WindowsServicingLog)

  - [Windows Update-Agent](#BKMK_WULog)  

  - [WSUS-Server](#BKMK_WSUSLog)  

## <a name="client-log-files"></a><a name="BKMK_ClientLogs"></a> Clientprotokolldateien

In den folgenden Abschnitten werden die Protokolldateien für Clientvorgänge und die Clientinstallation aufgelistet.  

### <a name="client-operations"></a><a name="BKMK_ClientOpLogs"></a> Clientvorgänge

In der folgenden Tabelle werden die Protokolldateien auf dem Configuration Manager-Client aufgelistet.  

|Protokollname|Beschreibung|  
|--------------|-----------------|  
|ADALOperationProvider.log|Enthält Informationen zu Anforderungen von Clientauthentifizierungstoken mit der Azure Active Directory-Authentifizierungsbibliothek (ADAL)|
|BitLockerManagementHandler.log|Zeichnet Informationen über BitLocker-Verwaltungsrichtlinien auf.|
|CAS.log|Der Content Access Service. Verwaltet den lokalen Paketcache auf dem Client.|  
|Ccm32BitLauncher.log|Zeichnet Aktionen zum Starten von Anwendungen auf dem Client auf, die mit *run as 32 bit* (im 32-Bit-Modus ausführen) gekennzeichnet sind.|  
|CcmEval.log|Zeichnet Auswertungsaktivitäten für den Configuration Manager-Clientstatus auf sowie Details für Komponenten, die für den Configuration Manager-Client erforderlich sind|  
|CcmEvalTask.log|Zeichnet die Auswertungsaktivitäten für den Configuration Manager-Clientstatus auf, die vom geplanten Auswertungstask initiiert werden|  
|CcmExec.log|Zeichnet Aktivitäten des Clients und des SMS-Agent-Hostdiensts auf. Diese Protokolldatei enthält auch Informationen zum Aktivieren und Deaktivieren des Aktivierungsproxys.|  
|CcmMessaging.log|Zeichnet Aktivitäten in Zusammenhang mit Kommunikation zwischen Client und Verwaltungspunkten auf.|  
|CCMNotificationAgent.log|Zeichnet Aktivitäten im Zusammenhang mit Client-Benachrichtigungsoperationen auf.|  
|Ccmperf.log|Zeichnet Aktivitäten im Zusammenhang mit Wartung und Erfassung von Daten zu Clientleistungsindikatoren auf.|  
|CcmRestart.log|Zeichnet Neustartaktivitäten zu Clientdiensten auf.|  
|CCMSDKProvider.log|Zeichnet Aktivitäten im Zusammenhang mit den Client-SDK-Schnittstellen auf.|  
|ccmsqlce.log|Dieses Protokoll zeichnet Aktivitäten für die SQL Compact-Edition auf, die der Client verwendet. Es wird in der Regel nur verwendet, wenn Sie die Debugprotokollierung aktivieren oder ein Problem mit der Komponente vorliegt. Der Clientintegritätstask (ccmeval) korrigiert Probleme mit dieser Komponente in der Regel selbst.|
|CertificateMaintenance.log|Verwaltet Zertifikate für die Active Directory-Domänendienste und die Verwaltungspunkte.|  
|CIDownloader.log|Zeichnet Details zu Downloads von Konfigurationselementdefinitionen auf.|  
|CITaskMgr.log|Dieses Protokoll zeichnet Tasks für jeden Anwendungs- und Bereitstellungstyp auf, z. B. für das Herunterladen von Inhalten oder das Installieren und Deinstallieren.|  
|ClientAuth.log|Zeichnet das Signieren und Authentifizieren des Clients auf.|  
|ClientIDManagerStartup.log|Dieses Protokoll erstellt und verwaltet die Client-GUID und identifiziert Tasks während der Anmeldung und Zuweisung von Clients.|  
|ClientLocation.log|Zeichnet Tasks im Zusammenhang mit der Clientstandortzuweisung auf.|  
|CMHttpsReadiness.log|Zeichnet die Ergebnisse der Ausführung des Configuration Manager-Tools zur Überprüfung der HTTPS-Bereitschaft auf. Mithilfe dieses Tools wird überprüft, ob Computer über ein PKI-Clientauthentifizierungszertifikat verfügen, das für Configuration Manager verwendet werden kann.|  
|CmRcService.log|Zeichnet Informationen für den Remotesteuerungsdienst auf.|  
|CoManagementHandler.log|Für die Problembehandlung der Co-Verwaltung auf dem Client verwenden.|
|ContentTransferManager.log|Plant den intelligenten Hintergrundübertragungsdienst (Background Intelligent Transfer Service, BITS) oder den Server Message Block (SMB), um Pakete herunterzuladen oder darauf zuzugreifen.|  
|DataTransferService.log|Zeichnet die gesamte BITS-Kommunikation für den Richtlinien- oder Paketzugriff auf.|  
|DeltaDownload.log|Zeichnet Informationen zum Download von Express-Updates und von Updates auf, die mithilfe der Übermittlungsoptimierung heruntergeladen wurden.|  
|Diagnostics.log|Zeichnet den Status von Clientdiagnoseaktionen auf.|
|EndpointProtectionAgent|Zeichnet Informationen zur Installation des System Center Endpoint Protection-Clients und zum Anwenden der Antischadsoftwarerichtlinie auf diesen Client auf.|  
|execmgr.log|Zeichnet Details zu Paketen und Tasksequenzen auf, die auf dem Client ausgeführt werden.|  
|ExpressionSolver.log|Zeichnet Details zu erweiterten Erkennungsmethoden auf, die verwendet werden, wenn die ausführliche oder die Debugprotokollierung aktiviert ist.|  
|ExternalEventAgent.log|Zeichnet den Verlauf der Schadsoftware-Erkennung und von Ereignissen von Endpoint Protection auf, die mit dem Clientstatus in Verbindung stehen.|  
|FileBITS.log|Zeichnet alle SMB-Paketzugriffsaufgaben auf.|  
|FileSystemFile.log|Zeichnet die Aktivitäten des WMI-Anbieters (Windows Management Instrumentation) für Softwareinventur und Dateisammlung auf.|  
|FSPStateMessage.log|Zeichnet die Aktivitäten im Zusammenhang mit Zustandsmeldungen auf, die vom Client an den Fallbackstatuspunkt gesendet werden.|  
|InternetProxy.log|Zeichnet die Konfigurations- und Nutzungsaktivitäten des Netzwerkproxys für den Client auf.|  
|InventoryAgent.log|Zeichnet Aktivitäten im Zusammenhang mit Hardwareinventur, Softwareinventur und Frequenzermittlung auf dem Client auf.|  
|LocationCache.log|Zeichnet die Aktivitäten im Zusammenhang mit Standortcachenutzung und -wartung für den Client auf.|  
|LocationServices.log|Zeichnet die Clientaktivitäten im Zusammenhang mit der Suche nach Verwaltungspunkten, Softwareupdatepunkten und Verteilungspunkten auf.|  
|M365AHandler.log|Enthält Informationen über die Desktop Analytics-Einstellungsrichtlinie.|
|MaintenanceCoordinator.log|Zeichnet die Aktivitäten im Zusammenhang mit allgemeinen Wartungstasks für den Client auf.|  
|Mifprovider.log|Zeichnet die Aktivitäten des WMI-Anbieters für MIF-Dateien auf.|  
|mtrmgr.log|Überwacht alle Softwaremessungen.|  
|PolicyAgent.log|Zeichnet mithilfe des Datenübertragungsdiensts übermittelte Richtlinienanforderungen auf.|  
|PolicyAgentProvider.log|Zeichnet Richtlinienänderungen auf.|  
|PolicyEvaluator.log|Zeichnet Details zur Auswertung von Richtlinien auf Clientcomputern, einschließlich Softwareupdates, auf.|  
|PolicyPlatformClient.log|Zeichnet den Prozess für Wiederherstellung und Konformität für alle Anbieter in „%Program Files%\Microsoft Policy Platform“ mit Ausnahme des Dateianbieters auf.|  
|PolicySdk.log|Zeichnet Aktivitäten für Schnittstellen des Richtliniensystem-SDK auf.|  
|Pwrmgmt.log|Zeichnet Informationen zum Aktivieren oder Deaktivieren sowie Konfigurieren der Clienteinstellungen des Aktivierungsproxys auf.|  
|PwrProvider.log|Zeichnet die Aktivitäten des Energieverwaltungsanbieters (PWRInvProvider) auf, der im WMI-Dienst (Windows Management Instrumentation) gehostet ist. Unter allen unterstützten Windows-Versionen zählt der Anbieter während der Hardwareinventur auf Computern die aktuellen Einstellungen auf und wendet Energiesparplaneinstellungen an.|  
|SCClient_&lt;*Domäne*\>@&lt;*Benutzername*\>_1.log|Zeichnet die Aktivitäten im Software Center für den angegebenen Benutzer auf dem Clientcomputer auf.|  
|SCClient_&lt;*Domäne*\>@&lt;*Benutzername*\>_2.log|Zeichnet die historischen Aktivitäten im Software Center für den angegebenen Benutzer auf dem Clientcomputer auf.|  
|Scheduler.log|Zeichnet Aktivitäten geplanter Tasks für alle Clientvorgänge auf.|  
|SCNotify_&lt;*Domäne*\>@&lt;*Benutzername*\>_1.log|Zeichnet die Aktivitäten im Zusammenhang mit Benutzerbenachrichtigungen über Software für den angegebenen Benutzer auf.|  
|SCNotify_&lt;*Domäne*\>@&lt;*Benutzername*\>_1-&lt;*date_time*>.log|Zeichnet die historischen Informationen im Zusammenhang mit Benutzerbenachrichtigungen über Software für den angegebenen Benutzer auf.|  
|setuppolicyevaluator.log|Zeichnet Aktivitäten im Zusammenhang mit Konfiguration und der Erstellung von Inventurrichtlinien in WMI auf.|  
|SleepAgent_&lt;*Domäne*\>@SYSTEM_0.log|Die wichtigste Protokolldatei für Aktivierungsproxy.|  
|smscliui.log|Zeichnet die Nutzung des Configuration Manager-Clients in der Systemsteuerung auf.|  
|SrcUpdateMgr.log|Zeichnet Aktivitäten im Zusammenhang mit installierten Windows Installer-Anwendungen auf, für die mithilfe aktueller Verteilungspunktquellpfade ein Update ausgeführt wird.|  
|StatusAgent.log|Zeichnet Statusmeldungen auf, die von Clientkomponenten erstellt werden.|  
|SWMTRReportGen.log|Erstellt einen Verwendungsdatenbericht, der von dem Messungsagent gesammelt wird. Diese Daten werden in Mtrmgr.log protokolliert.|  
|UserAffinity.log|Zeichnet Details zur Affinität zwischen Benutzer und Gerät auf.|  
|VirtualApp.log|Zeichnet spezifische Informationen zur Auswertung der App-V-Bereitstellungstypen auf.|  
|Wedmtrace.log|Zeichnet Vorgänge im Zusammenhang mit Schreibfiltern auf Windows Embedded-Clients auf.|  
|wakeprxy-install.log|Zeichnet Installationsinformationen auf, wenn Clients die Clienteinstellungsoption zur Aktivierung des Aktivierungsproxy empfangen.|  
|wakeprxy-uninstall.log|Zeichnet Informationen zur Deinstallation von Aktivierungsproxys auf, wenn von Clients die Clienteinstellungsoption „Aktivierungsproxys nicht zulassen“ empfangen wurde, wenn der Aktivierungsproxy bereits vorher zugelassen war.|  

### <a name="client-installation"></a><a name="BKMK_ClientInstallLog"></a> Clientinstallation

In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen zur Installation des Configuration Manager-Clients enthalten.  

|Protokollname|Beschreibung|  
|--------------|-----------------|  
|ccmsetup.log|Zeichnet ccmsetup.exe-Tasks für Clienteinstellung, Clientupgrade und Cliententfernung auf. Ist für die Problembehandlung bei Clientinstallationsproblemen hilfreich.|  
|ccmsetup-ccmeval.log|Zeichnet ccmsetup.exe-Tasks für Clientstatus und -wiederherstellung auf.|  
|CcmRepair.log|Zeichnet Reparaturaktivitäten des Client-Agents auf.|  
|client.msi.log|Dieses Protokoll zeichnet die von „client.msi“ erledigten Setuptasks auf. Ist für die Problembehandlung bei Problemen beim Installieren oder Entfernen von Clients hilfreich.|  

### <a name="client-for-linux-and-unix"></a><a name="BKMK_LogFilesforLnU"></a> Client für Linux und UNIX

> [!Important]  
> Ab Version 1902 unterstützt Configuration Manager keine Linux- oder UNIX-Clients mehr.
>
> Ziehen Sie deshalb Microsoft Azure Management zum Verwalten von Linux-Servern in Betracht. Azure-Lösungen verfügen über umfangreiche Linux-Unterstützung, die i.d.R. über die Funktionen von Configuration Manager hinausgeht (einschließlich der End-to-End-Patchverwaltung für Linux).

Vom Configuration Manager-Client für Linux und UNIX werden Informationen in folgenden Protokolldateien aufgezeichnet:  

> [!TIP]
> Verwenden Sie „CMTrace“, um sich Protokolldateien für den Linux- und UNIX-Client anzeigen zu lassen.

|Protokollname|Details|
|-------------------|-----------------------------------------------------------------|
|Scxcm.log| Das ist die Protokolldatei für den Kerndienst des Configuration Manager-Clients für Linux und UNIX (ccmexec.bin). Diese Protokolldatei enthält Informationen zur Installation und zum laufenden Vorgang von ccmexec.bin. Standardmäßig befindet sich diese Protokolldatei unter **/var/opt/microsoft/scxcm.log**. Für das Ändern des Speicherorts der Protokolldatei bearbeiten Sie **/opt/microsoft/configmgr/etc/scxcm.conf** , und ändern Sie das Feld **PATH** . Sie müssen den Clientcomputer oder den Dienst nicht neu starten, damit die Änderungen wirksam werden. Für den Protokolliergrad können Sie eine von vier unterschiedlichen Einstellungen vornehmen. |
| Scxcmprovider.log |Das ist die Protokolldatei für den CIM-Dienst des Configuration Manager-Clients für Linux und UNIX (omiserver.bin). Diese Protokolldatei enthält Informationen zu den laufenden Vorgängen von nwserver.bin. Dieses Protokoll befindet sich unter `/var/opt/microsoft/configmgr/scxcmprovider.log`. Für eine Änderung des Speicherorts der Protokolldatei bearbeiten Sie **/opt/microsoft/omi/etc/scxcmprovider.conf** , und ändern Sie das Feld **PATH** . Sie müssen den Clientcomputer oder den Dienst nicht neu starten, damit die Änderungen wirksam werden. Für den Protokolliergrad können Sie eine von drei unterschiedlichen Einstellungen vornehmen.|

Beide Protokolldateien unterstützen mehrere Protokolliergrade:  

- **scxcm.log**. Für eine Änderung des Protokolliergrads bearbeiten Sie **/opt/microsoft/configmgr/etc/scxcm.conf** und ändern Sie jede Instanz des Tags **MODUL** auf den gewünschten Protokolliergrad  

  - FEHLER: Weist auf Probleme hin, die Ihr Eingreifen erfordern.  

  - WARNUNG: Weist auf mögliche Probleme für Clientvorgänge hin.  

  - INFO: Ausführlichere Protokollierung, durch die der Status verschiedener Ereignisse auf dem Client angegeben wird.  

  - TRACE: Ausführliche Protokollierung, die normalerweise zur Problemdiagnose verwendet wird.  

- **scxcmprovider.log**. Für eine Änderung des Protokolliergrads bearbeiten Sie **/opt/microsoft/omi/etc/ scxcmprovider.conf** und ändern Sie jede Instanz des Tags **MODUL** in den erwünschten Protokolliergrad.  

  - FEHLER: Weist auf Probleme hin, die Ihr Eingreifen erfordern.  

  - WARNUNG: Weist auf mögliche Probleme für Clientvorgänge hin.

  - INFO: Ausführlichere Protokollierung, durch die der Status verschiedener Ereignisse auf dem Client angegeben wird.  

Unter normalen Betriebsbedingungen sollte der Protokollgrad FEHLER verwendet werden. Diese Protokollebene erstellt die kleinste Protokolldatei. Mit der Steigerung des Protokollgrads von FEHLER zu WARNUNG zu INFO zu ABLAUFVERFOLGUNG wird die Protokolldatei mit jedem Schritt größer, da mehr Daten hineingeschrieben werden.  

#### <a name="manage-log-files-for-the-linux-and-unix-client"></a><a name="BKMK_ManageLinuxLogs"></a> Verwalten von Protokolldateien für den Client für Linux und UNIX

Vom Client für Linux und UNIX wird die maximale Größe der Clientprotokolldateien nicht beschränkt. Zudem wird der Inhalt seiner LOG-Dateien nicht automatisch in eine andere Datei (z. B. eine .LO_-Datei) kopiert. Wenn Sie die maximale Größe von Protokolldateien steuern möchten, müssen Sie unabhängig vom Configuration Manager-Client für Linux und UNIX einen Prozess zum Verwalten der Protokolldateien implementieren.  

Beispielsweise können Sie den Linux- und UNIX-Standardbefehl **logrotate** verwenden, um die Größe und Rotation der Clientprotokolldateien zu verwalten. Auf dem Configuration Manager-Client für Linux und UNIX steht eine Schnittstelle zur Verfügung, mit deren Hilfe dem Client über **logrotate** signalisiert werden kann, wann die Protokollrotation abgeschlossen ist, sodass die Informationserfassung in der Protokolldatei wiederaufgenommen werden kann.  

Weitere Informationen über **logrotate**finden Sie in der Dokumentation zu den Linux und UNIX-Verteilungen, die Sie verwenden.  

### <a name="client-for-mac-computers"></a><a name="BKMK_LogfilesforMac"></a> Client für Macintosh-Computer

Vom Configuration Manager-Client für Mac-Computer werden Informationen in folgenden Protokolldateien auf dem Mac-Computer aufgezeichnet:  

|Protokollname|Details|Standort|
|--------------|-------------|-------------|
|CCMClient-&lt;*Datum_Zeit>* .log|Zeichnet Aktivitäten auf, die mit Vorgängen des Macintosh-Clients verknüpft sind. Dazu gehören Anwendungsverwaltung, Inventur und Fehlerprotokollierung.| `/Library/Application Support/Microsoft/CCM/Logs`|  
|CCMAgent-&lt;*Datum_Zeit>* .log|Zeichnet Informationen zu Clientvorgängen auf, einschließlich von Benutzeranmeldungs- und -abmeldungsvorgängen und Macintosh-Computeraktivität.| `~/Library/Logs`|  
|CCMNotifications-&lt;*Datum_Zeit>* .log|Zeichnet Aktivitäten auf, die mit Configuration Manager-Benachrichtigungen verknüpft sind, die auf dem Macintosh-Computer angezeigt werden.| `~/Library/Logs`|  
|CCMPrefPane-&lt;*Datum_Zeit>* .log|Zeichnet Aktivitäten auf, die mit dem Configuration Manager-Dialogfeld für Einstellungen auf dem Macintosh-Computer verknüpft sind. Dazu gehören der allgemeine Status und die Fehlerprotokollierung.| `~/Library/Logs`|  

Zusätzlich wird in der Protokolldatei **SMS_DM.log** auf dem Standortsystemserver die Kommunikation zwischen Macintosh-Computern und dem Verwaltungspunkt aufgezeichnet, der für mobile Geräte und Mac-Computer aktiviert ist.  

## <a name="server-log-files"></a><a name="BKMK_ServerLogs"></a> Serverprotokolldateien

In den folgenden Abschnitten werden Protokolldateien aufgelistet, die sich auf dem Standortserver befinden oder im Zusammenhang mit bestimmten Standortsystemrollen stehen.  

### <a name="site-server-and-site-systems"></a><a name="BKMK_SiteSiteServerLog"></a> Standortserver und Standortsysteme

In der folgenden Tabelle werden die Protokolldateien auf dem Configuration Manager-Standortserver und den entsprechenden Standortsystemservern aufgelistet.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|adctrl.log|Zeichnet Aktivitäten im Zusammenhang mit der Anmeldungsverarbeitung auf.|Standortserver|  
|ADForestDisc.log|Zeichnet Aktionen im Zusammenhang mit der Active Directory-Gesamtstrukturermittlung auf.|Standortserver|  
|adminservice.log|Zeichnet Aktionen für die REST-API des SMS-Anbieter-Verwaltungsdiensts auf|Computer mit dem SMS-Anbieter|
|ADService.log|Zeichnet Details zur Kontoerstellung und zu Sicherheitsgruppen in Active Directory auf.|Standortserver|  
|adsgdis.log|Zeichnet Aktionen der Active Directory-Gruppenermittlung auf.|Standortserver|  
|adsysdis.log|Zeichnet Aktionen im Zusammenhang mit der Active Directory-Systemermittlung auf.|Standortserver|  
|adusrdis.log|Zeichnet Aktionen im Zusammenhang mit der Active Directory-Benutzerermittlung auf.|Standortserver|  
|BusinessAppProcessWorker.log|Zeichnet die Verarbeitung der Microsoft Store für Unternehmen-Apps auf.|Standortserver|
|ccm.log|Zeichnet Aktivitäten für die Clientpushinstallation auf.|Standortserver|  
|CertMgr.log|Zeichnet die Zertifikataktivitäten für die standortinterne Kommunikation auf.|Standortsystemserver|  
|chmgr.log|Zeichnet die Aktivitäten des Clientintegritäts-Managers auf.|Standortserver|  
|Cidm.log|Zeichnet Änderungen an den Clienteinstellungen durch den SMS-Clientinstallationsdaten-Manager (CIDM) auf.|Standortserver|  
|CollectionAADGroupSyncWorker.log | Ab Version 2002 ist dies die Protokolldatei zum Synchronisieren der Sammlungsmitgliedschaftsergebnisse mit Azure Active Directory. In Version 1910 und früher wurde die Protokollierung für diese Funktion in „SMS_AZUREAD_DISCOVERY_AGENT.log“ kombiniert. | Standortserver|
|colleval.log|Zeichnet Details zum Erstellen, Ändern und Löschen von Sammlungen durch den Sammlungsauswerter auf.|Standortserver|  
|compmon.log|Zeichnet den Status von Threadkomponenten auf, die für den Standortserver überwacht werden.|Standortsystemserver|  
|compsumm.log|Zeichnet die Tasks der Statuszusammenfassung für Komponenten auf.|Standortserver|  
|ComRegSetup.log|Zeichnet die Ergebnisse der Erstinstallation der COM-Registrierung für einen Standortserver auf.|Standortsystemserver|  
|dataldr.log|Zeichnet Informationen zur Verarbeitung von MIF-Dateien und Hardwareinventur in der Configuration Manager-Datenbank auf.|Standortserver|  
|ddm.log|Zeichnet die Aktivitäten des Ermittlungsdaten-Managers auf.|Standortserver|  
|despool.log|Zeichnet die eingehende Datenkommunikation zwischen Standorten auf.|Standortserver|  
|distmgr.log|Zeichnet Details zu Paketerstellung, Komprimierung, Deltareplikation und Informationsupdates auf. Es kann auch andere Aktivitäten aus der Komponente des Verteilungs-Managers umfassen. Dazu zählen beispielsweise das Installieren eines Verteilungspunkts, Verbindungsversuche und das Installieren von Komponenten. Weitere Informationen zu anderen Funktionen, die dieses Protokoll verwenden, finden Sie unter [Dienstverbindungspunkt](#BKMK_WITLog) und [Bereitstellung des Betriebssystems](#BKMK_OSDLog).|Standortserver|  
|EPCtrlMgr.log|Zeichnet Informationen zur Synchronisierung von Schadsoftwarebedrohungsdaten vom Endpoint Protection-Server für Standortsystemrollen in die Configuration Manager-Datenbank auf.|Standortserver|  
|EPMgr.log|Zeichnet den Status der Endpoint Protection-Standortsystemrolle auf.|Standortsystemserver|  
|EPSetup.log|Stellt Informationen zur Installation der Endpoint Protection-Standortsystemrolle bereit.|Standortsystemserver|  
|EnrollSrv.log|Zeichnet Aktivitäten des Anmeldungsdienstprozesses auf.|Standortsystemserver|  
|EnrollWeb.log|Zeichnet Aktivitäten des Anmeldungswebsiteprozesses auf.|Standortsystemserver|  
|fspmgr.log|Zeichnet Aktivitäten der Fallbackstatuspunkt-Systemrolle auf.|Standortsystemserver|  
|hman.log|Zeichnet Informationen zu Standortkonfigurationsänderungen und zur Veröffentlichung von Standortinformationen in den Active Directory Domain Services auf.|Standortserver|  
|Inboxast.log|Zeichnet die Dateien auf, die vom Verwaltungspunkt in den entsprechenden Ordner INBOXES auf dem Standortserver verschoben werden.|Standortserver|  
|inboxmgr.log|Zeichnet Aktivitäten im Zusammenhang mit der Dateiübertragung zwischen Eingangsboxordnern auf.|Standortserver|  
|inboxmon.log|Zeichnet Aktivitäten in Zusammenhang mit der Verarbeitung von Eingangsboxdateien und Updates von Leistungsindikatoren auf.|Standortserver|  
|invproc.log|Zeichnet die Weiterleitung von MIF-Dateien von einem sekundären Standort an dessen übergeordneten Standort auf.|Standortserver|  
|migmctrl.log|Zeichnet Informationen zu Migrationsaktionen auf, einschließlich Migrationsaufträge, freigegebener Verteilungspunkte und Upgrades von Verteilungspunkten.|Standort der obersten Ebene in der Configuration Manager-Hierarchie und jeder untergeordnete primäre Standort Verwenden Sie in einer Hierarchie mit mehreren primären Standorten die Protokolldatei, die auf dem Standort der zentralen Verwaltung erstellt wurde.|  
|mpcontrol.log|Zeichnet die Registrierung des Verwaltungspunks in Windows Internet Name Service (WINS) auf. Zeichnet alle 10 Minuten die Verfügbarkeit des Verwaltungspunkts auf.|Standortsystemserver|  
|mpfdm.log|Zeichnet die Aktionen der Verwaltungspunktkomponente auf, von der Clientdateien in den entsprechenden Ordner INBOXES auf dem Standortserver verschoben werden.|Standortsystemserver|  
|mpMSI.log|Zeichnet die Details zur Installation des Verwaltungspunkts auf.|Standortserver|  
|MPSetup.log|Zeichnet den Wrapperprozess der Verwaltungspunktinstallation auf.|Standortserver|  
|netdisc.log|Zeichnet Aktionen im Zusammenhang mit der Netzwerkermittlung auf.|Standortserver|  
|NotiCtrl.log|Benachrichtigungen für Anwendungsanforderungen|Standortserver|  
|ntsvrdis.log|Zeichnet die Ermittlungsaktivitäten des Standortsystemservers auf.|Standortserver|  
|Objreplmgr|Zeichnet die Verarbeitung von Objektänderungsbenachrichtigungen für die Replikation auf.|Standortserver|  
|offermgr.log|Zeichnet Updates von Ankündigungen auf.|Standortserver|  
|offersum.log|Zeichnet die Zusammenfassung von Bereitstellungstatusmeldungen auf.|Standortserver|  
|OfflineServicingMgr.log|Zeichnet die Aktivitäten im Zusammenhang mit der Anwendung von Updates auf Betriebssystemabbilddateien auf.|Standortserver|  
|outboxmon.log|Zeichnet Aktivitäten in Zusammenhang mit der Verarbeitung von Ausgangsboxdateien und Updates von Leistungsindikatoren auf.|Standortserver|  
|PerfSetup.log|Zeichnet die Ergebnisse der Installation von Leistungsindikatoren auf.|Standortsystemserver|  
|PkgXferMgr.log|Zeichnet die Aktionen der Komponente SMS-Executive auf, über die Inhalte von einem primären Standort an einen Remoteverteilungspunkt gesendet werden.|Standortserver|  
|policypv.log|Zeichnet Aktualisierungen der Clientrichtlinien auf und spiegelt Änderungen der Clienteinstellungen oder -bereitstellungen wider.|Primärer Standortserver|  
|rcmctrl.log|Zeichnet die Aktivitäten im Zusammenhang mit der Datenbankreplikation zwischen Standorten in der Hierarchie auf.|Standortserver|  
|replmgr.log|Zeichnet die Replikation von Dateien zwischen Standortserverkomponenten und den Planerkomponenten auf.|Standortserver|  
|ResourceExplorer.log|Zeichnet Fehler, Warnungen und Informationen zur Ausführung des Ressourcen-Explorers auf.|Computer, auf dem die Configuration Manager-Konsole ausgeführt wird|  
|RESTPROVIDERSetup.log|Installation der REST-API des SMS-Anbieter-Verwaltungsdiensts|Computer mit dem SMS-Anbieter|
|ruleengine.log|Zeichnet Details zu automatischen Bereitstellungsregeln im Zusammenhang mit Identifizierung, Inhaltsdownload sowie Erstellung von Softwareupdategruppen und Bereitstellungen auf.|Standortserver|  
|schedule.log|Zeichnet Details zu Aufträgen zwischen Standorten sowie zur Dateireplikation auf.|Standortserver|  
|sender.log|Zeichnet die Dateien auf, die mithilfe von dateibasierter Replikation zwischen Standorten übertragen werden.|Standortserver|  
|sinvproc.log|Zeichnet Informationen zur Verarbeitung der Softwareinventurdaten in die Standortdatenbank auf.|Standortserver|  
|sitecomp.log|Zeichnet Details zur Wartung der installierten Standortkomponenten auf allen Standortsystemservern des Standorts auf.|Standortserver|  
|sitectrl.log|Zeichnet Änderungen der Standorteinstellungen auf, die an Standortsteuerungsobjekten in der Datenbank vorgenommen werden.|Standortserver|  
|sitestat.log|Zeichnet den Verfügbarkeits- und Speicherplatzüberwachungsprozess aller Standortsysteme auf.|Standortserver|
|SMS_AZUREAD_DISCOVERY_AGENT.log| Hierbei handelt es sich um die Protokolldatei für die Azure Active Directory-Ermittlung (Azure AD) von Benutzern und Benutzergruppen. In Version 1910 und früher umfasste es zudem die Synchronisierung der Sammlungsmitgliedschaftsergebnisse in Azure AD.| Standortserver|
|SMS_BUSINESS_APP_PROCESS_MANAGER.log|Protokolldatei für die Komponente, die Apps aus Microsoft Store für Unternehmen synchronisiert.|Standortserver|
|SMS_ISVUPDATES_SYNCAGENT.log| Protokolldatei für die Synchronisierung von Softwareupdates von Drittanbietern| Softwareupdatepunkt der obersten Ebene der Configuration Manager-Hierarchie|
|SMS_OrchestrationGroup.log| Protokolldatei für Orchestrierungsgruppen|Standortserver|
|SMS_PhasedDeployment.log| Protokolldatei für stufenweise Bereitstellungen|Standort der obersten Ebene in der Configuration Manager-Hierarchie|
|SMS_REST_PROVIDER.log|Dienstintegritätsstatus für die REST-API des SMS-Anbieter-Verwaltungsdiensts einschließlich Zertifikatinformationen|Computer mit dem SMS-Anbieter|
|SmsAdminUI.log|Zeichnet die Aktivität der Configuration Manager-Konsole auf|Computer, auf dem die Configuration Manager-Konsole ausgeführt wird|  
|SMSAWEBSVCSetup.log|Zeichnet die Installationsaktivitäten des Anwendungskatalog-Webdienstes auf.|Standortsystemserver|  
|smsbkup.log|Zeichnet die Ausgabe des Standortsicherungsprozesses auf.|Standortserver|  
|smsdbmon.log|Zeichnet Datenbankänderungen auf.|Standortserver|  
|SMSENROLLSRVSetup.log|Zeichnet die Installationsaktivitäten des Anmeldungswebdienstes auf.|Standortsystemserver|  
|SMSENROLLWEBSetup.log|Zeichnet die Installationsaktivitäten der Anmeldungswebsite auf.|Standortsystemserver|  
|smsexec.log|Zeichnet die Verarbeitung aller Threads der Standortserverkomponenten auf.|Standortserver oder Standortsystemserver|  
|SMSFSPSetup.log|Zeichnet Meldungen auf, die bei der Installation eines Fallbackstatuspunkts generiert werden.|Standortsystemserver|  
|SMSPORTALWEBSetup.log|Zeichnet die Installationsaktivitäten der Anwendungskatalog-Website auf.|Standortsystemserver|  
|SMSProv.log|Zeichnet den Zugriff des WMI-Anbieters auf die Standortdatenbank auf.|Computer mit dem SMS-Anbieter|  
|srsrpMSI.log|Zeichnet detaillierte Ergebnisse der Installation des Berichterstattungspunkts aus der MSI-Ausgabe auf.|Standortsystemserver|  
|srsrpsetup.log|Zeichnet Ergebnisse der Installation des Berichterstattungspunkts auf.|Standortsystemserver|  
|statesys.log|Zeichnet die Verarbeitung von Systemzustandsmeldungen auf.|Standortserver|  
|statmgr.log|Zeichnet Schreibvorgänge aller Statusmeldungen in die Datenbank auf.|Standortserver|  
|swmproc.log|Zeichnet die Verarbeitung von Messungsdateien und -einstellungen auf.|Standortserver|  

### <a name="site-server-installation"></a><a name="BKMK_SiteInstallLog"></a> Standortserverinstallation

In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit der Standortinstallation enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|ConfigMgrPrereq.log|Zeichnet Aktivitäten im Zusammenhang mit der Auswertung und Installation von erforderlichen Komponenten auf.|Standortserver|  
|ConfigMgrSetup.log|Zeichnet Ausgabedetails des Standortserver-Setups auf.|Standortserver|  
|ConfigMgrSetupWizard.log|Zeichnet Informationen im Zusammenhang mit Aktivitäten im Setup-Assistenten auf.|Standortserver|  
|SMS_BOOTSTRAP.log|Zeichnet Informationen zum Fortschritt beim Starten der Installation des sekundären Standorts auf. Informationen zum eigentlichen Installationsvorgang sind in ConfigMgrSetup.log enthalten.|Standortserver|  
|smstsvc.log|Dieses Protokoll zeichnet Informationen zum Installieren, Verwenden und Entfernen eines Windows-Diensts auf. Windows verwendet diesen Dienst, um die Netzwerkkonnektivität und die Berechtigungen zwischen Servern zu testen. Dabei wird das Computerkonto des Servers verwendet, der die Verbindung herstellt.|Standortserver und Standortsystemserver|  

### <a name="data-warehouse-service-point"></a><a name="BKMK_DataWarehouse"></a> Data Warehouse-Dienstpunkt

In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit dem Data Warehouse-Dienstpunkt enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|DWSSMSI.log|Zeichnet Meldungen auf, die durch die Installation eines Data Warehouse-Dienstpunkts generiert werden.|Standortsystemserver|  
|DWSSSetup.log|Zeichnet Meldungen auf, die durch die Installation eines Data Warehouse-Dienstpunkts generiert werden.|Standortsystemserver|  
|Microsoft.ConfigMgrDataWarehouse.log|Zeichnet Informationen zur Datensynchronisierung zwischen der Standortdatenbank und der Data Warehouse-Datenbank auf.|Standortsystemserver|  

### <a name="fallback-status-point"></a><a name="BKMK_FSPLog"></a> Fallbackstatuspunkt

In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit dem Fallbackstatuspunkt enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|FspIsapi|Zeichnet Details zur Kommunikation von mobilen Legacyclient-Geräten und Clientcomputern mit dem Fallbackstatuspunkt auf.|Standortsystemserver|  
|fspMSI.log|Zeichnet Meldungen auf, die bei der Installation eines Fallbackstatuspunkts generiert werden.|Standortsystemserver|  
|fspmgr.log|Zeichnet Aktivitäten der Fallbackstatuspunkt-Systemrolle auf.|Standortsystemserver|  

### <a name="management-point"></a><a name="BKMK_MPLog"></a> Verwaltungspunkt

In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit dem Verwaltungspunkt enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|CcmIsapi.log|Zeichnet Aktivitäten im Zusammenhang mit Client-Messaging auf dem Endpunkt auf.|Standortsystemserver|
|CCM_STS.log|Zeichnet Aktivitäten für Authentifizierungstoken auf, entweder für von Azure Active Directory oder von der Website ausgestellte Clienttoken.|Standortsystemserver|
|ClientAuth.log|Zeichnet Signierungs- und Authentifizierungsaktivität auf.|Standortsystemserver|
|MP_CliReg.log|Zeichnet die vom Verwaltungspunkt verarbeiteten Clientregistrierungsaktivitäten auf.|Standortsystemserver|  
|MP_Ddr.log|Zeichnet die Konvertierung von XML DDR-Datensätzen von Clients auf und kopiert diese auf den Standortserver.|Standortsystemserver|  
|MP_Framework.log|Zeichnet die Aktivitäten von Hauptverwaltungspunkt und Clientframeworkkomponenten auf.|Standortsystemserver|  
|MP_GetAuth.log|Zeichnet Aktivitäten im Zusammenhang mit der Clientautorisierung auf.|Standortsystemserver|  
|MP_GetPolicy.log|Zeichnet Aktivitäten im Zusammenhang mit Richtlinienanforderungen von Clientcomputern auf.|Standortsystemserver|  
|MP_Hinv.log|Zeichnet Details zum Konvertieren von XML-Hardwareinventurdatensätzen von Clients und zum Kopieren der Dateien auf den Standortserver auf.|Standortsystemserver|  
|MP_Location.log|Zeichnet Aktivitäten im Zusammenhang mit Suchanforderungen und Antworten von Clients auf.|Standortsystemserver|  
|MP_OOBMgr.log|Zeichnet die Verwaltungspunktaktivitäten im Zusammenhang mit dem Empfangen eines OTP von einem Client auf.|Standortsystemserver|  
|MP_Policy.log|Zeichnet die Richtlinienkommunikation auf.|Standortsystemserver|  
|MP_RegistrationManager.log|Zeichnet Aktivitäten im Zusammenhang mit der Clientregistrierung auf, wie z. B. Validierung von Zertifikaten, Zertifikatsperrlisten und Token.|Standortsystemserver|
|MP_Relay.log|Zeichnet das Übertragen von Dateien auf, die vom Client gesammelt werden.|Standortsystemserver|  
|MP_Retry.log|Zeichnet die Wiederholungsprozesse der Hardwareinventur auf.|Standortsystemserver|  
|MP_Sinv.log|Zeichnet Details zum Konvertieren von XML-Softwareinventurdatensätzen von Clients und zum Kopieren der Dateien auf den Standortserver auf.|Standortsystemserver|  
|MP_SinvCollFile.log|Zeichnet Details zur Dateisammlung auf.|Standortsystemserver|  
|MP_Status.log|Zeichnet Details zum Konvertieren von XML-Statusmeldungsdateien (SVF-Dateien) von Clients und zum Kopieren der Dateien auf den Standortserver auf.|Standortsystemserver|
|mpcontrol.log|Zeichnet die Registrierung des Verwaltungspunks in WINS auf. Zeichnet alle 10 Minuten die Verfügbarkeit des Verwaltungspunkts auf.|Standortserver|  
|mpfdm.log|Zeichnet die Aktionen der Verwaltungspunktkomponente auf, von der Clientdateien in den entsprechenden Ordner INBOXES auf dem Standortserver verschoben werden.|Standortsystemserver|  
|mpMSI.log|Zeichnet die Details zur Installation des Verwaltungspunkts auf.|Standortserver|  
|MPSetup.log|Zeichnet den Wrapperprozess der Verwaltungspunktinstallation auf.|Standortserver|  
|UserService.log|Zeichnet Benutzeranforderungen vom Softwarecenter zum Abrufen/Installieren von für Benutzer verfügbaren Anwendungen vom Server auf.|Standortsystemserver|

### <a name="service-connection-point"></a><a name="BKMK_WITLog"></a> Dienstverbindungspunkt

In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit dem Dienstverbindungspunkt enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|CertMgr.log|Zeichnet Zertifikat- und Proxykontoinformationen auf.|Standortserver|  
|colleval.log|Zeichnet Details zum Erstellen, Ändern und Löschen von Sammlungen durch den Sammlungsauswerter auf.|Primärer Standort und Standort der zentralen Verwaltung|  
|Cloudusersync.log|Zeichnet die Lizenzaktivierung für Benutzer auf.|Computer mit dem Dienstverbindungspunkt|  
|dataldr.log|Zeichnet Informationen über die Verarbeitung von MIF-Dateien auf.|Standortserver|  
|ddm.log|Zeichnet die Aktivitäten des Ermittlungsdaten-Managers auf.|Standortserver|  
|distmgr.log|Zeichnet Details zu Inhaltsverteilungsanforderungen auf.|Standortserver auf oberster Ebene|  
|Dmpdownloader.log|Zeichnet Details zu Downloads von Microsoft Intune auf.|Computer mit dem Dienstverbindungspunkt|  
|Dmpuploader.log|Zeichnet Details zum Hochladen von Datenbankänderungen in Microsoft Intune auf.|Computer mit dem Dienstverbindungspunkt|  
|hman.log|Zeichnet Informationen zur Meldungsweiterleitung auf.|Standortserver|  
|MSfBSyncWorker.log|Zeichnet Informationen zur Kommunikation mit Microsoft Store für Unternehmen auf.|Computer mit dem Dienstverbindungspunkt|
|objreplmgr.log|Zeichnet die Verarbeitung von Richtlinien und Zuweisung auf.|Primärer Standortserver|  
|policypv.log|Zeichnet die Richtliniengenerierung aller Richtlinien auf.|Standortserver|  
|outgoingcontentmanager.log|Zeichnet Inhalte auf, die auf Microsoft Intune hochgeladen werden|Computer mit dem Dienstverbindungspunkt|  
|sitecomp.log|Zeichnet Details zur Installation des Dienstverbindungspunkts auf.|Standortserver|  
|SmsAdminUI.log|Zeichnet die Aktivität der Configuration Manager-Konsole auf|Computer, auf dem die Configuration Manager-Konsole ausgeführt wird|  
|SMS_CLOUDCONNECTION.log|Zeichnet Informationen zu Clouddiensten auf.|Computer mit dem Dienstverbindungspunkt|
|SMSProv.log|Dieses Protokoll zeichnet die Aktivitäten des SMS-Anbieters auf. Configuration Manager-Konsolenaktivitäten verwenden den SMS-Anbieter.|Computer mit dem SMS-Anbieter|  
|SrvBoot.log|Zeichnet Details zum Dienstverbindungspunkt-Installationsdienst auf.|Computer mit dem Dienstverbindungspunkt|  
|Statesys.log|Zeichnet die Verarbeitung von Verwaltungsmeldungen zu mobilen Geräten auf.|Primärer Standort und Standort der zentralen Verwaltung|  

### <a name="software-update-point"></a><a name="BKMK_SUPLog"></a> Softwareupdatepunkt

In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen zum Softwareupdatepunkt enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|objreplmgr.log|Zeichnet Details zur Replikation von Benachrichtigungsdateien für Softwareupdates von einem übergeordneten an untergeordnete Standorte auf.|Standortserver|  
|PatchDownloader.log|Zeichnet Details zum Download von Softwareupdates von der Updatequelle in das Downloadziel auf dem Standortserver.|Wenn Sie Updates manuell herunterladen, befindet sich diese Datei in Ihrem Verzeichnis `%temp%` auf dem Computer, auf dem Sie die Konsole verwenden. Wenn der Configuration Manager-Client auf dem Standortserver installiert ist, befindet sich diese Datei bei automatischen Bereitstellungsregeln auf dem Standortserver unter `%windir%\CCM\Logs`.|  
|ruleengine.log|Zeichnet Details zu automatischen Bereitstellungsregeln im Zusammenhang mit Identifizierung, Inhaltsdownload sowie Erstellung von Softwareupdategruppen und Bereitstellungen auf.|Standortserver|
|SMS_ISVUPDATES_SYNCAGENT.log| Protokolldatei für die Synchronisierung von Softwareupdates von Drittanbietern| Softwareupdatepunkt der obersten Ebene der Configuration Manager-Hierarchie|
|SUPSetup.log|Zeichnet Details zur Installation des Softwareupdatepunkts auf. Nach Abschluss der Softwareupdatepunkt-Installation wird **Installation was successful** in diese Protokolldatei geschrieben.|Standortsystemserver|  
|WCM.log|Zeichnet Details zur Konfiguration des Softwareupdatepunkts und zum Herstellen einer Verbindung mit dem WSUS-Server für abonnierte Updatekategorien, Klassifizierungen und Sprachen auf.|Standortserver, die eine Verbindung mit dem WSUS-Server herstellen|  
|WSUSCtrl.log|Zeichnet Details zur Konfiguration, Datenbankverbindungen und der Integrität von WSUS-Servern für den Standort auf.|Standortsystemserver|  
|wsyncmgr.log|Zeichnet Details zum Synchronisierungsprozess für Softwareupdates auf.|Standortsystemserver|  
|WUSSyncXML.log|Zeichnet Details zum Synchronisierungsvorgang des Inventurprogramms für Microsoft Updates auf.|Der Clientcomputer, der als Synchronisierungshost für das Inventurprogramm für Microsoft Updates konfiguriert ist|  


## <a name="log-files-by-functionality"></a><a name="BKMK_FunctionLogs"></a> Protokolldateien für Configuration Manager-Funktionen

In den folgenden Abschnitten werden Protokolldateien für die Funktionen in Configuration Manager aufgelistet.  

### <a name="application-management"></a><a name="BKMK_AppManageLog"></a> Anwendungsverwaltung

In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit der Anwendungsverwaltung enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|AppIntentEval.log|Zeichnet Details zum aktuellen und beabsichtigten Zustand von Anwendungen sowie zu ihrer Anwendbarkeit, Bereitstellungstypen, Abhängigkeiten und dazu, ob Anforderungen erfüllt wurden.|Client|  
|AppDiscovery.log|Zeichnet die Details über die Ermittlung oder die Erkennung von Anwendungen auf Clientcomputern auf.|Client|  
|AppEnforce.log|Zeichnet Details zu vorgenommenen Erzwingungsaktionen (Installieren und Deinstallieren) für Anwendungen auf dem Client auf.|Client|  
|AppGroupHandler.log|Ab Version 1906, enthält Erkennungs-und Erzwingungsinformationen für Anwendungsgruppen|Client|
|awebsctl.log|Zeichnet die Überwachungsmaßnahmen für die Standortsystemrolle „Anwendungskatalog-Webdienstpunkt“ auf.|Standortsystemserver|  
|awebsvcMSI.log|Zeichnet detaillierte Installationsinformationen für die Standortsystemrolle „Anwendungskatalog-Webdienstpunkt“ auf.|Standortsystemserver|  
|BusinessAppProcessWorker.log|Zeichnet die Verarbeitung der Microsoft Store für Unternehmen-Apps auf.|Standortserver|
|CCMSDKProvider.log|Zeichnet die Aktivitäten des Anwendungsverwaltungs-SDK auf.|Client|  
|colleval.log|Zeichnet Details zum Erstellen, Ändern und Löschen von Sammlungen durch den Sammlungsauswerter auf.|Standortsystemserver|  
|ConfigMgrSoftwareCatalog.log|Zeichnet die Aktivitäten des Anwendungskatalogs auf, darunter auch dessen Verwendung von Silverlight.|Client|  
|MSfBSyncWorker.log|Zeichnet Informationen zur Kommunikation mit Microsoft Store für Unternehmen auf.|Computer mit dem Dienstverbindungspunkt|
|NotiCtrl.log|Benachrichtigungen für Anwendungsanforderungen|Standortserver|  
|portlctl.log|Zeichnet die Überwachungsmaßnahmen für die Standortsystemrolle „Anwendungskatalog-Websitepunkt“ auf.|Standortsystemserver|  
|portlwebMSI.log|Zeichnet die MSI-Installationsaktivitäten für die Anwendungskatalog-Websiterolle auf.|Standortsystemserver|  
|PrestageContent.log|Zeichnet die Details zur Verwendung des Tools ExtractContent.exe auf einem vorab bereitgestellten Remoteverteilungspunkt auf. Mit diesem Tool werden Inhalte extrahiert, die in eine Datei exportiert wurden.|Standortsystemserver|  
|ServicePortalWebService.log|Zeichnet die Aktivitäten des Anwendungskatalog-Webdienstes auf.|Standortsystemserver|  
|ServicePortalWebSite.log|Zeichnet die Aktivitäten der Anwendungskatalog-Website auf.|Standortsystemserver|  
|SettingsAgent.log|Erzwingung bestimmter Anwendungen, erfasst die Orchestrierung der Auswertung von Anwendungsgruppen sowie Details der Co-Verwaltungsrichtlinien.|Client|
|SMS_BUSINESS_APP_PROCESS_MANAGER.log|Protokolldatei für die Komponente, die Apps aus Microsoft Store für Unternehmen synchronisiert.|Standortserver|
|SMS_CLOUDCONNECTION.log|Zeichnet Informationen zu Clouddiensten auf.|Computer mit dem Dienstverbindungspunkt|
|SMSdpmon.log|Zeichnet Details zum geplanten Task für die Integritätsüberwachung des Verteilungspunkts auf, der auf einem Verteilungspunkt konfiguriert wurde.|Standortserver|  
|SoftwareCatalogUpdateEndpoint.log|Zeichnet die Aktivitäten im Zusammenhang mit der Verwaltung der im Softwarecenter angezeigten URL für den Anwendungskatalog auf.|Client|  
|SoftwareCenterSystemTasks.log|Zeichnet die Aktivitäten im Zusammenhang mit der Überprüfung der erforderlichen Komponenten für das Softwarecenter auf.|Client|  
|TSDTHandler.log|Für den Bereitstellungstyp „Tasksequenz“. Protokolliert den Prozess von der App-Erzwingung (Installation oder Deinstallation) bis zum Start der Tasksequenz. Kann mit „AppEnforce.log“ und „smsts.log“ verwendet werden.|Client|<!-- MEMDocs#336 -->

#### <a name="packages-and-programs"></a>Pakete und Programme

In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit der Bereitstellung von Paketen und Programmen enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|colleval.log|Zeichnet Details zum Erstellen, Ändern und Löschen von Sammlungen durch den Sammlungsauswerter auf.|Standortserver|  
|execmgr.log|Zeichnet Details zu Paketen und ausgeführten Tasksequenzen auf.|Client|  

### <a name="asset-intelligence"></a><a name="BKMK_AILog"></a> Asset Intelligence

In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit Asset Intelligence enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|AssetAdvisor.log|Zeichnet Aktivitäten im Zusammenhang mit Asset Intelligence-Inventuraktionen auf.|Client|  
|aikbmgr.log|Zeichnet Details zur Verarbeitung von XML-Dateien aus der Eingangsbox zum Update des Asset Intelligence-Katalogs auf.|Standortserver|  
|AIUpdateSvc.log|Zeichnet Details zur Interaktion des Asset Intelligence-Synchronisierungspunkts mit dem Clouddienst auf.|Standortsystemserver|  
|AIUSMSI.log|Zeichnet Details zur Installation der Standortsystemrolle „Asset Intelligence-Synchronisierungspunkt“ auf.|Standortsystemserver|  
|AIUSSetup.log|Zeichnet Details zur Installation der Standortsystemrolle „Asset Intelligence-Synchronisierungspunkt“ auf.|Standortsystemserver|  
|ManagedProvider.log|Zeichnet Details zur Ermittlung von Software mit einem zugehörigen Software ID-Tag auf. Zeichnet zusätzlich Aktivitäten im Zusammenhang mit der Hardwareinventur auf.|Standortsystemserver|  
|MVLSImport.log|Zeichnet Details zur Verarbeitung importierter Lizenzierungsdateien auf.|Standortsystemserver|  

### <a name="backup-and-recovery"></a><a name="BKMK_BnRLog"></a> Sicherung und Wiederherstellung

In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit Sicherungs- und Wiederherstellungsaktionen enthalten, darunter das Zurücksetzen von Standorten und Änderungen am SMS-Provider.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|ConfigMgrSetup.log|Zeichnet Informationen zu Setup- und Wiederherstellungstasks auf, wenn in Configuration Manager ein Standort aus einer Sicherung wiederhergestellt wird|Standortserver|  
|smsbkup.log|Erfasst Details zu Standortsicherungsaktivitäten.|Standortserver|  
|smssqlbkup.log|Zeichnet die Ausgabe der Standortdatenbanksicherung auf, wenn SQL Server auf einem anderen Server als dem Standortserver installiert ist.|Standortdatenbankserver|  
|Smswriter.log|Zeichnet Informationen zum Zustand von Configuration Manager VSS Writer auf, der im Sicherungsprozess verwendet wird.|Standortserver|  

### <a name="certificate-enrollment"></a><a name="BKMK_CertificateEnrollment"></a> Zertifikatregistrierung

In der folgenden Tabelle werden die Configuration Manager-Protokolldateien aufgelistet, die Informationen im Zusammenhang mit der Zertifikatregistrierung enthalten. Die Zertifikatregistrierung verwendet den Zertifikatregistrierungspunkt und das Configuration Manager-Richtlinienmodul auf dem Server, auf dem der Registrierungsdienst für Netzwerkgeräte (NDES) ausgeführt wird.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|Crp.log|Zeichnet die Registrierungsaktivitäten auf.|Zertifikatregistrierungspunkt|  
|Crpctrl.log|Zeichnet die Betriebsintegrität des Zertifikatregistrierungspunkts auf.|Zertifikatregistrierungspunkt|  
|Crpsetup.log|Zeichnet Einzelheiten über die Installation und Konfiguration des Zertifikatregistrierungspunkts auf.|Zertifikatregistrierungspunkt|  
|Crpmsi.log|Zeichnet Einzelheiten über die Installation und Konfiguration des Zertifikatregistrierungspunkts auf.|Zertifikatregistrierungspunkt|  
|NDESPlugin.log|Zeichnet die Aktivitäten der Abfrageüberprüfung und Zertifikatregistrierung auf.|Configuration Manager-Richtlinienmodul und der Registrierungsdienst für Netzwerkgeräte|  

Prüfen Sie zusammen mit den Configuration Manager-Protokolldateien auch die Windows-Anwendungsprotokolle in der Ereignisanzeige auf dem Server, auf dem der Registrierungsdienst für Netzwerkgeräte ausgeführt wird, sowie auf dem Hostserver des Zertifikatregistrierungspunkts. Achten Sie beispielsweise auf Nachrichten mit der Quellangabe **NetworkDeviceEnrollmentService** .

Sie können auch die folgenden Protokolldateien verwenden:  

- IIS-Protokolldateien für den Registrierungsdienst für Netzwerkgeräte: **%SYSTEMDRIVE%\inetpub\logs\LogFiles\W3SVC1**  

- IIS-Protokolldateien für den Zertifikatregistrierungspunkt: **%SYSTEMDRIVE%\inetpub\logs\LogFiles\W3SVC1**  

- Protokolldatei für den Registrierungsdienst für Netzwerkgeräte: **mscep.log**  

    > [!NOTE]  
    > Diese Datei befindet sich im Ordner für das NDES-Kontoprofil, z. B. in „C:\Benutzer\SCEPSvc“. Weitere Informationen zum Aktivieren der NDES-Protokollierung finden Abschnitt [Enable Logging](https://social.technet.microsoft.com/wiki/contents/articles/9063.active-directory-certificate-services-ad-cs-network-device-enrollment-service-ndes.aspx#Enable_Logging) (Protokollierung aktivieren) des NDES-Wiki.  

### <a name="client-notification"></a><a name="BKMK_BGB"></a> Clientbenachrichtigung

In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit Clientbenachrichtigungen enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|bgbmgr.log|Zeichnet Details zu den Aktivitäten auf dem Standortserver im Zusammenhang mit Clientbenachrichtigungstasks und der Verarbeitung von Online- und Taskstatusdateien auf.|Standortserver|  
|BGBServer.log|Zeichnet die Aktivitäten des Benachrichtigungsservers auf, z.B. die Kommunikation zwischen Client und Server und das Verteilen von Tasks an Clients. Außerdem werden Informationen zur Erstellung von Online- und Taskstatusdateien aufgezeichnet, die an den Standortserver gesendet werden.|Verwaltungspunkt|  
|BgbSetup.log|Zeichnet die Aktivitäten des Wrapperprozesses der Benachrichtigungsserverinstallation während der Installation und Deinstallation auf.|Verwaltungspunkt|  
|bgbisapiMSI.log|Zeichnet Details zur Installation und Deinstallation des Benachrichtigungsservers auf.|Verwaltungspunkt|  
|BgbHttpProxy.log|Zeichnet die Aktivitäten des Benachrichtigungs-HTTP-Proxys auf, wenn von diesem die Meldungen von Clients mittels HTTP von und an den Benachrichtigungsserver übermittelt werden.|Client|  
|CCMNotificationAgent.log|Zeichnet die Aktivitäten des Benachrichtigungsagenten auf, wie die Client-Server-Kommunikation und Informationen zu empfangenen und an andere Clientagenten versendeten Tasks.|Client|  

### <a name="cloud-management-gateway"></a>Cloudverwaltungsgateway

In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit Cloudverwaltungsgateways enthalten.

|Protokollname|Beschreibung|Computer mit Protokolldatei|
|--------------|-----------------|----------------------------|  
|CloudMgr.log|Zeichnet Details zur Bereitstellung des Cloudverwaltungsgateway-Dienstes, den laufenden Dienststatus und Nutzungsdaten, die mit dem Dienst verknüpft sind, auf. Bearbeiten Sie den Wert **Protokolliergrad** im folgenden Registrierungsschlüssel, um den Protokolliergrad zu konfigurieren: `HKLM\SOFTWARE\ Microsoft\SMS\COMPONENTS\ SMS_CLOUD_ SERVICES_MANAGER`|Der Ordner *installdir* auf dem primären Standortserver oder Clientzugriffsserver.|
|CMGSetup.log <sup>[Hinweis 1](#bkmk_note1)</sup>|Dieses Protokoll zeichnet Details zur zweiten Phase der Bereitstellung des Cloudverwaltungsgateways (lokale Bereitstellung in Azure) auf. Verwenden Sie die Einstellung **Ablaufverfolgungsebene** (**Information** (Standard), **Ausführlich**, **Fehler**) auf der Registerkarte **Azure portal\Cloud services configuration** (Azure-Portal\Clouddienstkonfiguration), um den Protokolliergrad zu konfigurieren.|Die **%approot%\logs** auf Ihrem Azure-Server oder der Ordner „SMS/Logs“ auf dem Standortsystemserver|
|CMGService.log <sup>[Hinweis 1](#bkmk_note1)</sup>|Dieses Protokoll zeichnet Details über die Kernkomponente des Cloudverwaltungsgateway-Diensts in Azure auf. Verwenden Sie die Einstellung **Ablaufverfolgungsebene** (**Information** (Standard), **Ausführlich**, **Fehler**) auf der Registerkarte **Azure portal\Cloud services configuration** (Azure-Portal\Clouddienstkonfiguration), um den Protokolliergrad zu konfigurieren.|Die **%approot%\logs** auf Ihrem Azure-Server oder der Ordner „SMS/Logs“ auf dem Standortsystemserver|
|SMS_Cloud_ProxyConnector.log|Zeichnet Details zum Einrichten von Verbindungen zwischen dem Cloud-Management-Gateway-Dienst und dem Verbindungspunkt für das Cloudverwaltungsgateway auf.|Standortsystemserver|
|CMGContentService.log <sup>[Hinweis 1](#bkmk_note1)</sup>|<!--SCCMDocs-pr issue #2822-->Wenn Sie einem CMG ermöglichen, auch Inhalte von Azure Storage bereitzustellen, zeichnet dieses Protokoll die Details dieses Dienstes auf.|Die **%approot%\logs** auf Ihrem Azure-Server oder der Ordner „SMS/Logs“ auf dem Standortsystemserver|

- Verwenden Sie für die Problembehandlung von Bereitstellungen **CloudMgr.log** und **CMGSetup.log**.
- Verwenden Sie für die Problembehandlung der Dienstintegrität **CMGService.log** und **SMS_Cloud_ProxyConnector.log**.
- Verwenden Sie für die Problembehandlung des Client-Datenverkehrs **CMGHttpHandler.log**, **CMGService.log** und **SMS_Cloud_ProxyConnector.log**.

#### <a name="note-1-logs-synchronized-from-azure"></a><a name="bkmk_note1"></a> Hinweis 1: Von Azure synchronisierte Protokolle

Hierbei handelt es sich um lokale Configuration Manager-Protokolldateien, die der Clouddienst-Manager alle fünf Minuten aus Azure Storage synchronisiert. Cloud Management Gateway (CMG) überträgt alle fünf Minuten Protokolle an Azure Storage. Daher beträgt die maximale Verzögerung zehn Minuten. Ausführliche Switches wirken sich auf lokale und Remoteprotokolle aus. Die tatsächlichen Dateinamen enthalten den Dienstnamen und den Bezeichner der Rolleninstanz. Ein Beispiel ist CMG-*Dienstname*-*Rolleninstanz-ID*-CMGSetup.log

### <a name="compliance-settings-and-company-resource-access"></a><a name="BKMK_CompSettingsLog"></a> Konformitätseinstellungen und Zugriff auf Unternehmensressourcen

In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit Konformitätseinstellungen und dem Zugriff auf Unternehmensressourcen enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|CIAgent.log|Zeichnet Details zum Wiederherstellungsprozess sowie zu Kompatibilität für Kompatibilitätseinstellungen, Softwareupdates und Anwendungsverwaltung auf.|Client|  
|CITaskManager.log|Zeichnet Informationen zur Taskplanung für Konfigurationselemente auf.|Client|  
|DCMAgent.log|Zeichnet detaillierte Informationen zu Auswertung, Konfliktberichterstattung und Wiederherstellung von Konfigurationselementen und Anwendungen auf.|Client|  
|DCMReporting.log|Zeichnet Informationen zur Berichterstattung von Richtlinienplattformergebnissen in Statusmeldungen für Konfigurationselemente auf.|Client|  
|DcmWmiProvider.log|Zeichnet Informationen im Zusammenhang mit dem Einlesen von Konfigurationselement-Synclets aus WMI auf.|Client|  

### <a name="configuration-manager-console"></a><a name="BKMK_ConsoleLog"></a> Configuration Manager-Konsole

In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen zur Configuration Manager-Konsole enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|ConfigMgrAdminUISetup.log|Zeichnet die Installation der Configuration Manager-Konsole auf|Computer, auf dem die Configuration Manager-Konsole ausgeführt wird|  
|SmsAdminUI.log|Zeichnet Informationen zum Betrieb der Configuration Manager-Konsole auf|Computer, auf dem die Configuration Manager-Konsole ausgeführt wird|  
|SMSProv.log|Dieses Protokoll zeichnet die Aktivitäten des SMS-Anbieters auf. Configuration Manager-Konsolenaktivitäten verwenden den SMS-Anbieter.|Standortserver oder Standortsystemserver|  

### <a name="content-management"></a><a name="BKMK_ContentLog"></a> Content Management

In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit der Inhaltsverwaltung enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|CloudDP-&lt;guid\>.log|Zeichnet Einzelheiten eines speziellen cloudbasierten Verteilungspunkts auf, einschließlich Informationen über die Speicherung und den Zugriff auf Inhalten.|Standortsystemserver|  
|CloudMgr.log|Zeichnet Einzelheiten über die Bereitstellung von Inhalten, die Sammlung von Speicherungs- und Bandbreitenstatistiken sowie vom Administrator ergriffene Maßnahmen zum Anhalten oder Starten des Clouddiensts, der an einem cloudbasierten Verteilungspunkt ausgeführt wird, auf.|Standortsystemserver|  
|DataTransferService.log|Zeichnet die gesamte BITS-Kommunikation für den Richtlinien- oder Paketzugriff auf. Dieses Protokoll wird auch für das Content Management von Pullverteilungspunkten verwendet.|Ein Computer, der als Pullverteilungspunkt konfiguriert ist|  
|PullDP.log|Zeichnet Details über Inhalte auf, die der Pullverteilungspunkt aus Quellverteilungspunkten überträgt.|Ein Computer, der als Pullverteilungspunkt konfiguriert ist|  
|PrestageContent.log|Zeichnet die Details zur Verwendung des Tools ExtractContent.exe auf einem vorab bereitgestellten Remoteverteilungspunkt auf. Mit diesem Tool werden Inhalte extrahiert, die in eine Datei exportiert wurden.|Standortsystemrolle|  
|SMSdpmon.log|Zeichnet Details zum geplanten Task für die Integritätsüberwachung des Verteilungspunkts auf, der auf einem Verteilungspunkt konfiguriert wurde.|Standortsystemrolle|  
|smsdpprov.log|Zeichnet Details zur Extrahierung komprimierter Dateien auf, die von einem primären Standort stammen. Dieses Protokoll wird vom WMI-Anbieter des Remoteverteilungspunkts generiert.|Ein Verteilungspunktcomputer an einem anderen Standort als der Standortserver|  
|smsdpusage.log|Zeichnet Details zu „smsdpusage.exe“ auf, die Daten zum Bericht zur Verteilungspunkt-Nutzungszusammenfassung sammelt.|Standortsystemrolle|  

### <a name="desktop-analytics"></a>Desktop Analytics

Verwenden Sie die folgenden Protokolldateien, um Probleme mit dem in Configuration Manager integrierten Desktop Analytics-Dienst zu beheben.

Die Protokolldateien im Dienstverbindungspunkt befinden sich in folgendem Verzeichnis: `%ProgramFiles%\Configuration Manager\Logs\M365A`.
Die Protokolldateien im Configuration Manager-Client befinden sich in folgendem Verzeichnis: `%WinDir%\CCM\logs`.

| Protokoll | Beschreibung |Computer mit Protokolldatei|
|---------|---------|---------|
| M365ADeploymentPlanWorker.log | Enthält Informationen über die Synchronisierung des Bereitstellungsplans vom Desktop Analytics-Clouddienst zum lokalen Configuration Manager. |Dienstverbindungspunkt|
| M365ADeviceHealthWorker.log | Enthält Informationen zum Upload von Daten zur Geräteintegrität von Configuration Manager in die Microsoft-Cloud. |Dienstverbindungspunkt|
| M365AHandler.log | Enthält Informationen über die Desktop Analytics-Einstellungsrichtlinie. |Client|
| M365AUploadWorker.log | Enthält Informationen zum Erfassen und zum Upload von Geräten von Configuration Manager in die Microsoft-Cloud. |Dienstverbindungspunkt|
| SmsAdminUI.log | Enthält Informationen zu Configuration Manager-Konsolenaktivitäten wie etwa zum Konfigurieren der Azure-Clouddienste.  |Dienstverbindungspunkt|

### <a name="discovery"></a><a name="BKMK_DiscoveryLog"></a> Ermittlung

In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen zur Ermittlung enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|adsgdis.log|Zeichnet Aktionen im Zusammenhang mit der Active Directory-Sicherheitsgruppenermittlung auf.|Standortserver|  
|adsysdis.log|Zeichnet Aktionen im Zusammenhang mit der Active Directory-Systemermittlung auf.|Standortserver|  
|adusrdis.log|Zeichnet Aktionen im Zusammenhang mit der Active Directory-Benutzerermittlung auf.|Standortserver|  
|ADForestDisc.log|Zeichnet Aktionen im Zusammenhang mit der Active Directory-Gesamtstrukturermittlung auf.|Standortserver|  
|ddm.log|Zeichnet die Aktivitäten des Ermittlungsdaten-Managers auf.|Standortserver|  
|InventoryAgent.log|Zeichnet Aktivitäten im Zusammenhang mit Hardwareinventur, Softwareinventur und Frequenzermittlung auf dem Client auf.|Client|  
|netdisc.log|Zeichnet Aktionen im Zusammenhang mit der Netzwerkermittlung auf.|Standortserver|  

### <a name="endpoint-protection"></a><a name="BKMK_EPLog"></a> Endpoint Protection

In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit Endpoint Protection enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|EndpointProtectionAgent.log|Zeichnet Details zur Installation des Endpoint Protection-Clients und zum Anwenden der Richtlinie für Antischadsoftware auf diesen Client auf.|Client|  
|EPCtrlMgr.log|Zeichnet Details zur Synchronisierung von Schadsoftwarebedrohungsdaten vom Endpoint Protection-Rollenserver in die Configuration Manager-Datenbank auf.|Standortsystemserver|  
|EPMgr.log|Überwacht den Status der Endpoint Protection-Standortsystemrolle.|Standortsystemserver|  
|EPSetup.log|Stellt Informationen zur Installation der Endpoint Protection-Standortsystemrolle bereit.|Standortsystemserver|  

### <a name="extensions"></a><a name="BKMK_Extensions"></a> Erweiterungen

In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit Erweiterungen enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|AdminUI.ExtensionInstaller.log|Zeichnet Informationen zum Download von Erweiterungen von Microsoft sowie zur Installation und Deinstallation aller Erweiterungen auf.|Computer, auf dem die Configuration Manager-Konsole ausgeführt wird|  
|FeatureExtensionInstaller.log|Zeichnet Informationen zur Installation und Deinstallation von einzelnen Erweiterungen auf, wenn diese in der Configuration Manager-Konsole aktiviert oder deaktiviert werden.|Computer, auf dem die Configuration Manager-Konsole ausgeführt wird|  
|SmsAdminUI.log|Zeichnet die Aktivität der Configuration Manager-Konsole auf|Computer, auf dem die Configuration Manager-Konsole ausgeführt wird|  

### <a name="inventory"></a><a name="BKMK_InventoryLog"></a> Inventur

In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit der Verarbeitung von Inventurdaten enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|dataldr.log|Zeichnet Informationen zur Verarbeitung von MIF-Dateien und Hardwareinventur in der Configuration Manager-Datenbank auf.|Standortserver|  
|invproc.log|Zeichnet die Weiterleitung von MIF-Dateien von einem sekundären Standort an dessen übergeordneten Standort auf.|Sekundärer Standortserver|  
|sinvproc.log|Zeichnet Informationen zur Verarbeitung der Softwareinventurdaten in die Standortdatenbank auf.|Standortserver|  

### <a name="metering"></a><a name="BKMK_MeteringLog"></a> Messung

In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit Messungen enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|mtrmgr.log|Überwacht alle Softwaremessungen.|Client|  
|SWMTRReportGen.log|Erstellt einen Verwendungsdatenbericht, der von dem Messungsagent gesammelt wird. Diese Daten werden in Mtrmgr.log protokolliert.|Client|
|swmproc.log|Zeichnet die Verarbeitung von Messungsdateien und -einstellungen auf.|Standortserver|

### <a name="migration"></a><a name="BKMK_MigrationLog"></a> Migration

In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit der Migration enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|migmctrl.log|Zeichnet Informationen zu Migrationsaktionen auf, einschließlich Migrationsaufträge, freigegebener Verteilungspunkte und Upgrades von Verteilungspunkten.|Standort der obersten Ebene in der Configuration Manager-Hierarchie und jeder untergeordnete primäre Standort Verwenden Sie in einer Hierarchie mit mehreren primären Standorten die Protokolldatei, die auf dem Standort der zentralen Verwaltung erstellt wurde.|  

### <a name="mobile-devices"></a><a name="BKMK_MDMLog"></a> Mobile Geräte

In den folgenden Abschnitten werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit der Verwaltung mobiler Geräte enthalten.  

#### <a name="enrollment"></a><a name="BKMK_EnrollmentLog"></a> Registrierung

In der folgenden Tabelle werden Protokolle aufgelistet, die Informationen im Zusammenhang mit der Anmeldung mobiler Geräte enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|DMPRP.log|Zeichnet die Kommunikation zwischen Verwaltungspunkten, die für mobile Geräte aktiviert sind, und den Endpunkten der Verwaltungspunkte auf.|Standortsystemserver|  
|dmpmsi.log|Zeichnet die Windows Installer-Daten für die Konfiguration eines für mobile Geräte aktivierten Verwaltungspunkts auf.|Standortsystemserver|  
|DMPSetup.log|Zeichnet die Konfiguration des Verwaltungspunkts auf, wenn dieser für mobile Geräte aktiviert wird.|Standortsystemserver|  
|enrollsrvMSI.log|Zeichnet die Windows Installer-Daten für die Konfiguration eines Anmeldungspunkts auf.|Standortsystemserver|  
|enrollmentweb.log|Zeichnet die Kommunikation zwischen mobilen Geräten und dem Anmeldungsproxypunkt auf.|Standortsystemserver|  
|enrollwebMSI.log|Zeichnet die Windows Installer-Daten für die Konfiguration eines Anmeldungsproxypunkts auf.|Standortsystemserver|  
|enrollmentservice.log|Zeichnet die Kommunikation zwischen einem Anmeldungsproxypunkt und einem Anmeldungspunkt auf.|Standortsystemserver|  
|SMS_DM.log|Zeichnet die Kommunikation zwischen mobilen Geräten, Macintosh-Computern und dem für mobile Geräte aktivierten Verwaltungspunkt auf.|Standortsystemserver|  

#### <a name="exchange-server-connector"></a><a name="BKMK_ExchSrvLog"></a> Exchange Server-Connector

Die folgenden Protokolle enthalten Informationen im Zusammenhang mit dem Exchange Server-Connector.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|easdisc.log|Zeichnet die Aktivitäten und den Status des Exchange Server-Connectors auf.|Standortserver|  

#### <a name="mobile-device-legacy"></a><a name="BKMK_MDLegLog"></a> Legacyclient für mobile Geräte

In der folgenden Tabelle werden Protokolle aufgelistet, die Informationen im Zusammenhang mit dem Legacyclient für mobile Geräte enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|DmCertEnroll.log|Zeichnet Details zu Zertifikatanmeldungsdaten auf Legacyclients für mobile Geräte auf.|Client|  
|DMCertResp.htm|Zeichnet die HTML-Antwort des Zertifikatsservers auf die Anforderung eines PKI-Zertifikats durch das Anmeldungsprogramm des Legacyclients für mobile Geräte auf.|Client|  
|DmClientHealth.log|Zeichnet die GUIDs aller Legacyclients für mobile Geräte auf, die mit dem für mobile Geräte aktivierten Verwaltungspunkt kommunizieren.|Standortsystemserver|  
|DmClientRegistration.log|Zeichnet Registrierungsanforderungen und -antworten im Zusammenhang mit Legacyclients für mobile Geräte auf.|Standortsystemserver|  
|DmClientSetup.log|Zeichnet Daten des Client-Setup für Legacyclients für mobile Geräte auf.|Client|  
|DmClientXfer.log|Zeichnet die Clientübertragungsdaten für Legacyclients für mobile Geräte und für ActiveSync-Bereitstellungen auf.|Client|  
|DmCommonInstaller.log|Zeichnet die Installation von Clientübertragungsdateien für die Konfiguration von Übertragungsdateien von Legacyclients für mobile Geräte auf.|Client|  
|DmInstaller.log|Zeichnet auf, ob „DmClientSetup“ ordnungsgemäß von „DMInstaller“ aufgerufen wird und ob „DmClientSetup“ erfolgreich oder mit einem Fehler auf Legacyclients für mobile Geräte abgeschlossen wird.|Client|  
|DmpDatastore.log|Zeichnet alle Verbindungen zur Standortdatenbank und alle Abfragen vom für mobile Geräte aktivierten Verwaltungspunkt auf.|Standortsystemserver|  
|DmpDiscovery.log|Zeichnet alle Ermittlungsdaten von den Legacyclients für mobile Geräte auf dem für mobile Geräte aktivierten Verwaltungspunkt auf.|Standortsystemserver|  
|DmpHardware.log|Zeichnet alle Hardwareinventurdaten von den Legacyclients für mobile Geräte auf dem für mobile Geräte aktivierten Verwaltungspunkt auf.|Standortsystemserver|  
|DmpIsapi.log|Zeichnet die Kommunikation zwischen dem Legacyclient für mobile Geräte und dem für mobile Geräte aktivierten Verwaltungspunkt auf.|Standortsystemserver|  
|dmpmsi.log|Zeichnet die Windows Installer-Daten für die Konfiguration eines für mobile Geräte aktivierten Verwaltungspunkts auf.|Standortsystemserver|  
|DMPSetup.log|Zeichnet die Konfiguration des Verwaltungspunkts auf, wenn dieser für mobile Geräte aktiviert wird.|Standortsystemserver|  
|DmpSoftware.log|Zeichnet Softwareverteilungsdaten von den Legacyclients für mobile Geräte auf einem für mobile Geräte aktivierten Verwaltungspunkt auf.|Standortsystemserver|  
|DmpStatus.log|Zeichnet Statusmeldungsdaten von den Clients für mobile Geräte auf einem für mobile Geräte aktivierten Verwaltungspunkt auf.|Standortsystemserver|  
|DmSvc.log|Zeichnet die Kommunikation zwischen dem Legacyclient für mobile Geräte und dem für mobile Geräte aktivierten Verwaltungspunkt auf.|Client|  
|FspIsapi.log|Zeichnet Details zur Kommunikation von mobilen Legacyclient-Geräten und Clientcomputern mit dem Fallbackstatuspunkt auf.|Standortsystemserver|  

### <a name="os-deployment"></a><a name="BKMK_OSDLog"></a> Bereitstellung des Betriebssystems

In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit der Betriebssystembereitstellung enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|CAS.log|Zeichnet die Details von Verteilungspunkten auf, die für referenzierten Inhalt gefunden werden.|Client|  
|ccmsetup.log|Zeichnet ccmsetup-Tasks für Clienteinstellung, Clientupgrade und Cliententfernung auf. Ist für die Problembehandlung bei Clientinstallationsproblemen hilfreich.|Client|  
|CreateTSMedia.log|Zeichnet Details zur Tasksequenz „Medienerstellung“ auf.|Computer, auf dem die Configuration Manager-Konsole ausgeführt wird|  
|Dism.log|Zeichnet Aktionen im Zusammenhang mit der Treiberinstallation oder der Anwendung von Updates für die Offlinewartung auf.|Standortsystemserver|  
|distmgr.log|Zeichnet Details zur Konfiguration beim Aktivieren eines Verteilungspunkts für Preboot Execution Environment (PXE) auf.|Standortsystemserver|  
|DriverCatalog.log|Zeichnet Details zu Gerätetreibern auf, die in den Treiberkatalog importiert wurden.|Standortsystemserver|  
|mcsisapi.log|Zeichnet Informationen im Zusammenhang mit Multicast-Paketübertragungen und Clientanforderungsantworten auf.|Standortsystemserver|  
|mcsexec.log|Zeichnet Aktionen im Zusammenhang mit Integritätsprüfung, Namespaces, Sitzungserstellung und Zertifikatprüfung auf.|Standortsystemserver|  
|mcsmgr.log|Zeichnet Änderungen an Konfiguration, Sicherheitsmodus und Verfügbarkeit auf.|Standortsystemserver|  
|mcsprv.log|Zeichnet die Interaktion zwischen Multicastanbieter und WDS (Windows Deployment Services) auf.|Standortsystemserver|  
|MCSSetup.log|Zeichnet Details zur Installation der Multicastserverrolle auf.|Standortsystemserver|  
|MCSMSI.log|Zeichnet Details zur Installation der Multicastserverrolle auf.|Standortsystemserver|  
|Mcsperf.log|Zeichnet Details zu Updates von Multicastleistungsindikatoren auf.|Standortsystemserver|  
|MP_ClientIDManager.log|Dieses Protokoll zeichnet Antworten des Verwaltungspunkts auf Client-ID-Anforderungen auf, die durch Tasksequenzen über PXE oder über Startmedien gestartet wurden.|Standortsystemserver|  
|MP_DriverManager.log|Zeichnet Antworten des Verwaltungspunkts auf Aktionsanforderungen über die Tasksequenz „Treiber automatisch anwenden“ auf.|Standortsystemserver|  
|OfflineServicingMgr.log|Zeichnet Details zur Planung von Offlinewartungsmaßnahmen und zum Anwenden von Updates auf WIM-Dateien des Betriebssystems auf.|Standortsystemserver|  
|Setupact.log|Zeichnet Details zu Windows-Sysprep- und -Setup-Protokollen auf. Weitere Informationen finden Sie in den [Protokolldateien](https://docs.microsoft.com/windows/deployment/upgrade/log-files).|Client|  
|Setupapi.log|Zeichnet Details zu Windows-Sysprep- und -Setup-Protokollen auf.|Client|  
|Setuperr.log|Zeichnet Details zu Windows-Sysprep- und -Setup-Protokollen auf.|Client|  
|smpisapi.log|Zeichnet Details zum Erfassen und Wiederherstellen des Clientzustands sowie Schwellenwertinformationen auf.|Client|  
|Smpmgr.log|Zeichnet Details zu den Ergebnissen von Integritätsprüfungen und Konfigurationsänderungen von Zustandsmigrationspunkten auf.|Standortsystemserver|  
|smpmsi.log|Zeichnet Installations- und Konfigurationsdetails zum Zustandsmigrationspunkt auf.|Standortsystemserver|  
|smpperf.log|Zeichnet Details zu Updates von Leistungsindikatoren für Zustandsmigrationspunkte auf.|Standortsystemserver|  
|smspxe.log|Zeichnet Details zu den Antworten an Clients mit PXE-Start sowie Details zur Erweiterung von Startimages und Startdateien auf.|Standortsystemserver|  
|smssmpsetup.log|Zeichnet Installations- und Konfigurationsdetails zum Zustandsmigrationspunkt auf.|Standortsystemserver|
| SMS_PhasedDeployment.log| Protokolldatei für stufenweise Bereitstellungen|Standort der obersten Ebene in der Configuration Manager-Hierarchie|
|Smsts.log|Zeichnet Tasksequenzaktivitäten auf.|Client|  
|TSAgent.log|Zeichnet das Ergebnis von Tasksequenzabhängigkeiten vor dem Starten einer Tasksequenz auf.|Client|  
|TaskSequenceProvider.log|Zeichnet Details zu Tasksequenzen auf, wenn diese importiert, exportiert oder bearbeitet werden.|Standortsystemserver|  
|loadstate.log|Zeichnet Details zum Migrationsprogramm für den Benutzerzustand (USMT) sowie zur Wiederherstellung von Benutzerzustandsdaten auf.|Client|  
|scanstate.log|Zeichnet Details zum Migrationsprogramm für den Benutzerzustand (USMT) sowie zur Erfassung von Benutzerzustandsdaten auf.|Client|  

### <a name="power-management"></a><a name="BKMK_PowerMgmtLog"></a> Energieverwaltung

In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit der Energiewaltung enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|Pwrmgmt.log|Zeichnet Details zu Energieverwaltungsaktivitäten auf dem Clientcomputer auf, einschließlich der Überwachung und Erzwingung von Einstellungen durch den Energieverwaltungsclient-Agent.|Client|  

### <a name="remote-control"></a><a name="BKMK_RCLog"></a> Remotesteuerung

In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit der Remotesteuerung enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|CMRcViewer.log|Zeichnet Details zur Aktivität des Remotesteuerungsviewers auf.|Auf dem Computer, auf dem der Remotesteuerungsviewer ausgeführt wird, im %temp%-Ordner|  

### <a name="reporting"></a><a name="BKMK_ReportLog"></a> Berichterstellung

In der folgenden Tabelle werden die Configuration Manager-Protokolldateien aufgelistet, die Informationen im Zusammenhang mit der Berichterstattung enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|srsrp.log|Zeichnet Informationen im Zusammenhang mit den Aktivitäten und dem Status des Reporting Services-Punkts auf.|Standortsystemserver|  
|srsrpMSI.log|Zeichnet detaillierte Ergebnisse der Installation des Reporting Services-Punkts aus der MSI-Ausgabe auf.|Standortsystemserver|  
|srsrpsetup.log|Zeichnet Ergebnisse der Installation des Reporting Services-Punkts auf.|Standortsystemserver|  

### <a name="role-based-administration"></a><a name="BKMK_RBALog"></a> Rollenbasierte Verwaltung

In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit der rollenbasierten Verwaltung enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|hman.log|Zeichnet Informationen zu Standortkonfigurationsänderungen und zur Veröffentlichung von Standortinformationen in Active Directory Domain Services auf.|Standortserver|  
|SMSProv.log|Zeichnet den Zugriff des WMI-Anbieters auf die Standortdatenbank auf.|Computer mit dem SMS-Anbieter|  

### <a name="software-metering"></a><a name="BKMK_MeteringLog"></a> Softwaremessung

In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit Softwaremessungen enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|mtrmgr.log|Überwacht alle Softwaremessungen.|Standortserver|  

### <a name="software-updates"></a><a name="BKMK_SU_NAPLog"></a> Softwareupdates

In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit Softwareupdates enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|AlternateHandler.log|Zeichnet Details auf, wenn der Client die Klick-und-Los-COM-Schnittstelle von Office aufruft, um Clientupdates für Microsoft 365 Apps für Unternehmen herunterzuladen und zu installieren. Ähnelt der Verwendung von WuaHandler, wenn die Windows Update Agent-API aufgerufen wird, um Windows-Updates herunterzuladen und zu installieren.<!-- SCCMDocs#888 -->|Client|
|Ccmperf.log|Zeichnet Aktivitäten im Zusammenhang mit Wartung und Erfassung von Daten zu Clientleistungsindikatoren auf.|Client|
|DeltaDownload.log|Zeichnet Informationen zum Download von Express-Updates und von Updates auf, die mithilfe der Übermittlungsoptimierung heruntergeladen wurden.|Client|  
|PatchDownloader.log|Zeichnet Details zum Download von Softwareupdates von der Updatequelle in das Downloadziel auf dem Standortserver.|Wenn Sie Updates manuell herunterladen, befindet sich diese Protokolldatei im Verzeichnis %temp% des Benutzers, der die Konsole auf dem Computer ausführt, auf dem Sie die Konsole ausführen. Bei automatischen Bereitstellungsregeln befindet sich diese Protokolldatei auf dem Standortserver in %windir%\CCM\Logs, wenn der ConfigMgr-Client auf dem Standortserver installiert ist.|  
|PolicyEvaluator.log|Zeichnet Details zur Auswertung von Richtlinien auf Clientcomputern, einschließlich Softwareupdates, auf.|Client|  
|RebootCoordinator.log|Zeichnet Details zur Koordinierung von Systemneustarts auf Clientcomputern nach der Installation von Softwareupdates auf.|Client|  
|ScanAgent.log|Zeichnet Details zu Überprüfungsanforderungen für Softwareupdates, zum WSUS-Speicherort sowie zu entsprechenden Aktionen auf.|Client|  
|SdmAgent.log|Zeichnet Details zur Nachverfolgung von Wiederherstellung und Konformität auf. Die Protokolldatei für Softwareupdates „Updateshandler.log“ bietet jedoch umfangreichere Informationen zur Installation der für die Konformität benötigten Softwareupdates. Diese Protokolldatei wird mit Kompatibilitätseinstellungen gemeinsam genutzt.|Client|  
|ServiceWindowManager.log|Zeichnet Details zur Auswertung von Wartungsfenstern auf.|Client|
|SMS_ISVUPDATES_SYNCAGENT.log| Protokolldatei für die Synchronisierung von Softwareupdates von Drittanbietern| Softwareupdatepunkt der obersten Ebene der Configuration Manager-Hierarchie|
|SMS_OrchestrationGroup.log| Protokolldatei für Orchestrierungsgruppen|Standortserver|
|SmsWusHandler.log|Zeichnet Details zum Überprüfungsvorgang für das Inventurprogramm für Microsoft Updates auf.|Client|  
|StateMessage.log|Zeichnet Details zu Zustandsmeldungen für Softwareupdates auf, die erstellt und an den Verwaltungspunkt gesendet werden.|Client|  
|SUPSetup.log|Zeichnet Details zur Installation des Softwareupdatepunkts auf. Nach Abschluss der Softwareupdatepunkt-Installation wird **Installation was successful** in diese Protokolldatei geschrieben.|Standortsystemserver|  
|UpdatesDeployment.log|Zeichnet Details zu Bereitstellungen auf dem Client auf, einschließlich Softwareupdateaktivierung, Auswertung und Erzwingung. Die ausführliche Protokollierung zeigt zusätzliche Informationen zur Interaktion mit der Clientbenutzeroberfläche an.|Client|  
|UpdatesHandler.log|Zeichnet Details zur Softwareupdate-Kompatibilitätsüberprüfung, zum Download und zur Installation von Softwareupdates auf dem Client auf.|Client|  
|UpdatesStore.log|Zeichnet Details zum Kompatibilitätsstatus für Softwareupdates auf, die im Rahmen des Kompatibilitätsüberprüfungszyklus bewertet wurden.|Client|  
|WCM.log|Zeichnet Details zur Konfiguration von Softwareupdatepunkten und zum Herstellen einer Verbindung mit WSUS-Server für abonnierte Updatekategorien, Klassifizierungen und Sprachen auf.|Standortserver|  
|WSUSCtrl.log|Zeichnet Details zur Konfiguration, Datenbankverbindungen und der Integrität von WSUS-Servern für den Standort auf.|Standortsystemserver|  
|wsyncmgr.log|Zeichnet Details zum Synchronisierungsprozess von Softwareupdates auf.|Standortserver|  
|WUAHandler.log|Zeichnet Details zum Windows Update-Agent auf dem Client bei der Suche nach Softwareupdates auf.|Client|  

### <a name="wake-on-lan"></a><a name="BKMK_WOLLog"></a> Wake-On-LAN

In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit der Verwendung von Wake-On-LAN enthalten.  

> [!NOTE]  
> Wenn Sie Wake-On-LAN durch die Verwendung des Aktivierungsproxys ergänzen, wird diese Aktivität auf dem Client protokolliert. Weitere Informationen finden Sie z.B. unter „CcmExec.log“ und „SleepAgent_<*Domäne*\>@SYSTEM_0.log“ im Abschnitt [Clientvorgänge](#BKMK_ClientOpLogs) in diesem Artikel.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|wolcmgr.log|Zeichnet Details dazu auf, welche Clients Aktivierungspakete erhalten müssen, die Anzahl der gesendeten Aktivierungspakete und die Anzahl an wiederholten Aktivierungspaketen.|Standortserver|  
|wolmgr.log|Zeichnet Details zu Aktivierungsverfahren auf, beispielsweise zum Zeitpunkt der Aktivierung von Bereitstellungen, die für Wake-On-LAN konfiguriert wurden.|Standortserver|  

### <a name="windows-10-servicing"></a><a name="BKMK_WindowsServicingLog"></a> Windows 10-Wartung

In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit der Windows 10-Wartung enthalten.  
Für die Wartung werden die gleiche Infrastruktur und der gleiche Prozess wie für Softwareupdates verwendet. Informationen zu anderen Protokollen, die für das Wartungsszenario gelten, finden Sie unter [Softwareupdates](#BKMK_SU_NAPLog).

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|„CBS.log“|Zeichnet Wartungsfehler auf, die im Zusammenhang mit Änderungen für Windows Updates oder Rollen und Funktionen stehen|Client|
|„DISM.log“|Zeichnet alle Aktionen mithilfe von DISM auf. Bei Bedarf verweist „DISM.log“ auf „CBS.log“ für weitere Informationen.|Client|
|setupact.log|Primäre Protokolldatei für die meisten Fehler, die während der Installation von Windows auftreten. Die Protokolldatei befindet sich im Ordner % windir%\$Windows.~BT\sources\panther.|Client|

Weitere Informationen finden Sie unter [Online Servicing-Related Log Files (Protokolldateien zur Onlinewartung)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/deployment-troubleshooting-and-log-files#online-servicing-related-log-files).

### <a name="windows-update-agent"></a><a name="BKMK_WULog"></a> Windows Update-Agent

In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit dem Windows Update-Agent enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|WindowsUpdate.log|Zeichnet Details dazu auf, wann der Windows Update-Agent eine Verbindung mit dem WSUS-Server herstellt und die Softwareupdates für die Konformitätsbewertung abruft und ob Updates für die Agent-Komponenten vorhanden sind.|Client|  

Weitere Informationen erhalten Sie in den [Windows Update-Protokolldateien](https://docs.microsoft.com/windows/deployment/update/windows-update-logs).

### <a name="wsus-server"></a><a name="BKMK_WSUSLog"></a> WSUS-Server

In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit dem WSUS-Server enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|Change.log|Zeichnet Details zu geänderten WSUS-Server-Datenbankinformationen auf.|WSUS-Server|  
|SoftwareDistribution.log|Zeichnet Details zu Softwareupdates auf, die von der konfigurierten Updatequelle zur WSUS-Serverdatenbank synchronisiert werden.|WSUS-Server|  

Diese Protokolldateien befinden sich im Ordner `%ProgramFiles%\Update Services\LogFiles`.

## <a name="see-also"></a>Weitere Informationen:

- [Grundlegendes zu Protokolldateien](about-log-files.md)

- [Supportcenter – OneTrace](../../support/support-center-onetrace.md)

- [Protokolldateianzeige des Supportcenters](../../support/support-center.md#support-center-log-file-viewer)

- [CMTrace](../../support/cmtrace.md)
