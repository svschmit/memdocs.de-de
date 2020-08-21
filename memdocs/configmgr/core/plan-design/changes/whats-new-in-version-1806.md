---
title: Neuigkeiten in Version 1806
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über Änderungen und neue Funktionen, die in Version 1806 des Current Branch von Configuration Manager eingeführt wurden.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0249dbd3-1e85-4d05-a9e5-420fbe44d850
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 3b153dad513107b118d11fa95e3feaa035a1bc90
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692637"
---
# <a name="whats-new-in-version-1806-of-configuration-manager-current-branch"></a>Neuigkeiten in Version 1806 des Current Branch von Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Das Update 1806 für den Current Branch von Configuration Manager ist als konsoleninternes Update verfügbar. Wenden Sie dieses Update auf Standorte an, an denen Version 1706, 1710 oder 1802 ausgeführt wird. <!-- baseline only statement: When installing a new site, it's also available as a baseline version.-->

Überprüfen Sie stets die neueste Checkliste für die Installation dieses Updates. Informationen finden Sie unter [Checkliste für die Installation von Update 1806](../../servers/manage/checklist-for-installing-update-1806.md). Nachdem Sie einen Standort aktualisiert haben, überprüfen Sie auch die [Checkliste für Aufgaben nach dem Update](../../servers/manage/checklist-for-installing-update-1806.md#post-update-checklist).

<!--
> [!Important]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized.  
-->

Die folgenden Abschnitte enthalten Details zu den Änderungen und neuen Features in Version 1806 des Current Branch von Configuration Manager.  



## <a name="deprecated-features-and-operating-systems"></a>Veraltete Features und Betriebssysteme

Erfahren Sie mehr zu Supportänderungen, bevor Sie in [entfernten und veralteten Elementen](deprecated/removed-and-deprecated.md) implementiert werden.

Ab dem 14. August 2018 gilt das Feature für die hybride Verwaltung mobiler Geräte als veraltet. Weitere Informationen finden Sie unter [Hybride Verwaltung mobiler Geräte](../../../mdm/understand/what-happened-to-hybrid.md).<!--Intune feature 2683117-->  

<!--
Version 1806 drops support for the following products:
-->



## <a name="site-infrastructure"></a>Infrastruktur von Standorten

### <a name="cmpivot"></a>CMPivot
<!--1358456-->
Configuration Manager hat immer einen großen zentralen Speicher für Gerätedaten bereitgestellt, die Kunden für Berichtszwecke verwenden. Der Standort erfasst diese Daten in der Regel einmal pro Woche. CMPivot ist ein neues, in der Konsole integriertes Hilfsprogramm, das nun Zugriff auf den Status von Geräten in Ihrer Umgebung in Echtzeit ermöglicht. Es führt sofort eine Abfrage aller derzeit verbundenen Geräte in der Zielsammlung durch und gibt die Ergebnisse zurück. Sie können diese Daten dann im Tool filtern und gruppieren. Mit dem Bereitstellen von Echtzeitdaten von Onlineclients können Sie schneller Geschäftsfragen beantworten, Problembehandlungen durchführen sowie auf Sicherheitsvorfälle reagieren. 

Weitere Informationen finden Sie unter [CMPivot](../../servers/manage/cmpivot.md).  


### <a name="site-server-high-availability"></a>Hochverfügbarkeit der Standortserver
<!--1128774-->
Die Hochverfügbarkeit einer eigenständigen primären Serverrolle ist eine auf Configuration Manager basierende Lösung zum Installieren eines weiteren primären Standortservers im passiven Modus. Der Standortserver im passiven Modus ist zusätzlich zu Ihrem primären Standortserver vorhanden, der sich im aktiven Modus befindet. Ein Standortserver im passiven Modus ist bei Bedarf sofort einsatzbereit. 

Weitere Informationen finden Sie in den folgenden Artikeln: 
- [Hochverfügbarkeit der Standortserver](../../servers/deploy/configure/site-server-high-availability.md) 
- [Flussdiagramm – Einrichten eines Standortservers im passiven Modus](../../servers/deploy/configure/passive-site-server-flowchart.md)
- [Flussdiagramm – Hochstufen des Standortservers (geplant)](../../servers/deploy/configure/promote-site-server-flowchart.md)
- [Flussdiagramm – Hochstufen des Standortservers (ungeplant)](../../servers/deploy/configure/promote-site-server-unplanned-flowchart.md)


### <a name="improvements-to-management-insights"></a>Verbesserungen der Einblicke für die Verwaltung
Dieses Release umfasst die folgenden Verbesserungen der Einblicke für die Verwaltung:  

- Einige Einblicke in die Verwaltung können jetzt Aktionen auslösen. Bei dieser Aktion wird entweder zum zugeordneten Knoten in der Konsole navigiert oder eine gefilterte, abfragebasierte Ansicht angezeigt.<!--1357930-->  

- Für Proactive Maintenance ist eine neue Gruppe mit sechs neuen Regeln verfügbar, durch die mögliche Konfigurationsprobleme hervorgehoben werden können, die durch regelmäßige Wartung vermieden werden sollen.<!--1352184-->  

Weitere Informationen finden Sie unter [Einblicke für die Verwaltung](../../servers/manage/management-insights.md).


### <a name="configuration-manager-tools"></a>Configuration Manager-Tools
<!--1357145-->
Die Configuration Manager-Server- und -Client-Tools sind jetzt auf dem Server enthalten. Sie finden diese im Ordner `CD.Latest\SMSSETUP\Tools` auf dem Standortserver. Es ist keine weitere Installation erforderlich. 

Weitere Informationen finden Sie unter [Configuration Manager-Tools](../../support/tools.md).


### <a name="exclude-active-directory-containers-from-discovery"></a>Ausschließen von Active Directory-Containern von der Ermittlung
<!--1358143-->
Wenn Sie die Anzahl der ermittelten Objekte reduzieren möchten, müssen Sie bestimmte Container aus der Active Directory-Systemermittlung ausschließen. 

Weitere Informationen finden Sie unter [Konfigurieren der Active Directory-Systemermittlung](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_config-adsd).



## <a name="content-management"></a>Content Management

### <a name="configure-a-remote-content-library-for-the-site-server"></a>Konfigurieren einer remoten Inhaltsbibliothek für den Standortserver
<!--1357525-->
Wenn Sie die Hochverfügbarkeit der Standortserver konfigurieren oder auf Ihrem zentralen Verwaltungsserver oder primären Standortserver Speicherplatz auf einem Laufwerk freigeben möchten, müssen Sie die Inhaltsbibliothek an einen anderen Speicherort verschieben. Verschieben Sie die Inhaltsbibliothek auf ein anderes Laufwerk auf dem Standortserver, einen separaten Server oder ein fehlertolerantes Laufwerk in einem Storage Area Network (SAN). 

Weitere Informationen finden Sie in den folgenden Artikeln: 
- [Die Inhaltsbibliothek](../hierarchy/the-content-library.md)
- [Flussdiagramm – Verwalten der Inhaltsbibliothek](../hierarchy/manage-content-library-flowchart.md)


### <a name="cloud-distribution-point-support-for-azure-resource-manager"></a>Cloudverteilungspunkt-Unterstützung für Azure Resource Manager
<!--1322209-->
Beim Erstellen des Cloudverteilungspunkts bietet der Assistent jetzt die Option, eine **Azure Resource Manager-Bereitstellung** zu erstellen. Azure Resource Manager ist eine moderne Plattform zum Verwalten sämtlicher Lösungsressourcen als einzige Entität, die als Ressourcengruppe bezeichnet wird. Beim Bereitstellen eines Cloudverteilungspunkts mit Azure Resource Manager authentifiziert und erstellt der Standort mithilfe von Azure Active Directory die erforderlichen Cloudressourcen. Für diese modernisierte Bereitstellung ist kein klassisches Azure-Verwaltungszertifikat erforderlich. 

Der Featuredokumentation für den Cloudverteilungspunkt wurde ebenfalls überarbeitet und verbessert. Weitere Informationen finden Sie in den folgenden Artikeln:
- [Verwenden eines cloudbasierten Verteilungspunkts](../hierarchy/use-a-cloud-based-distribution-point.md)   
- [Cloudverteilungspunkt installieren](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)  


### <a name="pull-distribution-points-support-cloud-distribution-points-as-source"></a>Pullverteilungspunkte unterstützen Cloudverteilungspunkte als Quelle  
<!--1321554-->
Viele Kunden verwenden in Remotebüros oder Filialen Pullverteilungspunkte, die Inhalte über das WAN von einem Quellverteilungspunkt herunterladen. Wenn Ihre Remotebüros über eine bessere Internetverbindung verfügen oder die Belastung Ihrer WAN-Verbindungen reduziert werden soll, können Sie in Microsoft Azure einen Cloudverteilungspunkt als Quelle verwenden. Wenn Sie auf der Registerkarte **Pullverteilungspunkt** der Verteilungspunkteigenschaften eine Quelle hinzufügen, werden anschließend alle Cloudverteilungspunkte am Standort als verfügbare Verteilungspunkte aufgeführt. Ansonsten ändert sich das Verhalten der beiden Standortsystemrollen nicht. 

Weitere Informationen finden Sie unter [Verwenden eines Pullverteilungspunkts](../hierarchy/use-a-pull-distribution-point.md).


### <a name="enable-distribution-points-to-use-network-congestion-control"></a>Aktivieren der Verwendung der Netzwerküberlastungssteuerung durch die Verteilungspunkte
<!--1358112-->
Windows Low Extra Delay Background Transport (LEDBAT) ist ein Feature von Windows Server zum Verwalten von Netzwerkübertragungen im Hintergrund. Für Verteilungspunkte, die auf unterstützten Versionen von Windows Server ausgeführt werden, können Sie eine Option zum Anpassen des Netzwerkdatenverkehrs aktivieren. Clients verwenden Netzwerkbandbreite nur, wenn sie verfügbar ist. 

Weitere Informationen finden Sie unter [Windows LEDBAT](../hierarchy/fundamental-concepts-for-content-management.md#windows-ledbat).


### <a name="partial-download-support-in-client-peer-cache-to-reduce-wan-utilization"></a>Unterstützung von Teildownloads im Clientpeercache zum Reduzieren der WAN-Auslastung
<!--1357346-->
Clientpeercache-Quellen können Inhalte jetzt in mehrere Teile untergliedern. Diese Teile minimieren die Netzwerkdatenübertragung, um die WAN-Auslastung zu reduzieren. Der Verwaltungspunkt erlaubt eine genauere Nachverfolgung der Inhaltsteile. Er versucht, mehrere Downloads desselben Inhalts pro Begrenzungsgruppe zu vermeiden. 

Weitere Informationen finden Sie unter [Unterstützung von Teildownloads](../hierarchy/client-peer-cache.md#bkmk_parts). 


### <a name="boundary-group-options-for-peer-downloads"></a>Begrenzungsgruppenoptionen für Peerdownloads
<!--1356193-->
Begrenzungsgruppen beinhalten nun zusätzliche Einstellungen, die Ihnen mehr Kontrolle über die Verteilung von Inhalten in Ihrer Umgebung einräumen. Dieses Release bietet die folgenden Optionen:  

- **Peerdownloads in dieser Begrenzungsgruppe zulassen:** Der Verwaltungspunkt bietet Clients eine Liste der Speicherorte für Inhalt, die Peerquellen enthält. Diese Einstellung wirkt sich auch auf die Anwendung von Gruppen-IDs für die Übermittlungsoptimierung aus.  

- **Bei Peerdownloads nur Peers in demselben Subnetz verwenden:** Der Verwaltungspunkt enthält nur in der Inhaltsspeicherort-Liste Peerquellen, die sich im gleichen Subnetz wie der Client befinden.  

Weitere Informationen finden Sie unter [Begrenzungsgruppenoptionen für Peerdownloads](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).


### <a name="improvement-to-peer-cache-source-location-status"></a>Verbesserungen des Status der Speicherorts von Peercachequellen
<!--SCCMDocs issue 850-->
Configuration Manager bestimmt effizienter, ob eine Peercachequelle per Roaming zu einem anderen Speicherort gewechselt hat. Durch dieses Verhalten wird sichergestellt, dass diese vom Verwaltungspunkt am neuen statt am alten Speicherort als Inhaltsquelle für Clients bereitgestellt wird. Wenn Sie die Peercachefunktion mit Roaming von Peercachequellen verwenden, führen Sie nach dem Update des Standorts auf Version 1806 auch Updates auf die neueste Clientversion für alle Peercachequellen durch. Der Verwaltungspunkt führt diese Peercachequellen erst in der Liste der Speicherorte für Inhalte auf, wenn sie mindestens auf Version 1806 aktualisiert wurden.

Weitere Informationen finden Sie unter [Anforderungen und Überlegungen für den Peercache](../hierarchy/client-peer-cache.md#requirements).



<!-- ## Migration  -->



## <a name="client-management"></a>Clientverwaltung

### <a name="improvement-to-client-push-security"></a>Verbesserung der Clientpushsicherheit
<!--1358204-->
Wenn die Clientpushmethode zur Installation des Configuration Manager-Clients verwendet wird, kann der Standort jetzt eine gegenseitige Kerberos-Authentifizierung anfordern. Diese Verbesserung sichert die Kommunikation zwischen dem Server und dem Client. 

Weitere Informationen finden Sie unter [Installieren von Clients mittels Clientpush](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).


### <a name="enhanced-http-site-system"></a><a name="bkmk_ehttp"></a> Erweitertes HTTP-Standortsystem
<!--1356889,1358228-->
Die HTTPS-Kommunikation wird für alle Configuration Manager-Kommunikationspfade empfohlen, kann jedoch wegen der aufwändigen Verwaltung von PKI-Zertifikaten für einige Kunden schwierig sein.

Dieses Release bietet Verbesserungen der Kommunikation von Clients mit Standortsystemen. Wählen Sie bei den Standorteigenschaften auf der Registerkarte **Client Computer Communication** (Clientcomputerkommunikation) die Option für **HTTPS oder HTTP** aus, und aktivieren Sie anschließend die neue Option zum **Verwenden von vom Configuration Manager generierten Zertifikaten für HTTP-Standortsysteme**. Bei diesem Feature handelt es sich um ein [vorab veröffentlichtes Feature](../../servers/manage/pre-release-features.md).

Weitere Informationen finden Sie unter [Enhanced HTTP (Erweitertes HTTP)](../hierarchy/enhanced-http.md).


### <a name="azure-ad-device-identity"></a>Azure AD-Geräteidentität 
<!--1358460-->
Ein in [Azure AD eingebundenes](/azure/active-directory/devices/concept-azure-ad-join) oder [hybrides Azure AD-Gerät](/azure/active-directory/devices/concept-azure-ad-join-hybrid) kann sicher mit seinem zugewiesenen Standort kommunizieren, ohne dass ein Azure AD-Benutzer angemeldet ist. Die cloudbasierte Geräteidentität reicht jetzt für die Authentifizierung beim CMG und Verwaltungspunkt aus.  

Weitere Informationen finden Sie unter [Enhanced HTTP (Erweitertes HTTP)](../hierarchy/enhanced-http.md).


### <a name="cmtrace-installed-with-client"></a>CMTrace mit Client installiert
<!--1357971-->
Das CMTrace-Protokollanzeigetool wird jetzt automatisch mit dem Configuration Manager-Client installiert. Es wird dem Clientinstallationsverzeichnis (standardmäßig `%WinDir%\ccm\cmtrace.exe`) hinzugefügt. 

Weitere Informationen finden Sie unter [CMTrace](../../support/cmtrace.md).


### <a name="cloud-management-dashboard"></a>Dashboard für die Cloudverwaltung
<!--1358461-->
Das neue Dashboard für die Cloudverwaltung bietet eine zentrale Ansicht für die Nutzung von Cloud Management Gateway (CMG). Wenn im Standort Azure AD integriert ist, werden auch Daten zu Cloudbenutzern und -geräten angezeigt.   

Diese Funktion umfasst auch die **CMG-Verbindungsanalyse** für die Echtzeitüberprüfung zur Unterstützung der Problembehandlung. Das Hilfsprogramm in der Konsole überprüft den aktuellen Status des Diensts und den Kommunikationskanal über den CMG-Verbindungspunkt zu Verwaltungspunkten, die CMG-Datenverkehr zulassen. 

Weitere Informationen finden Sie in den folgenden Abschnitten des Artikels [Monitor CMG (Überwachen von CMG)](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md):  
- [Dashboard für die Cloudverwaltung](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md#cloud-management-dashboard)  
- [Verbindungsanalyse](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md#connection-analyzer)  


### <a name="improvements-to-cloud-management-gateway"></a>Verbesserungen am Cloudverwaltungsgateway

Version 1806 umfasst folgende Verbesserungen am Cloud Management Gateway (CMG):

#### <a name="simplified-client-bootstrap-command-line"></a>Vereinfachte Befehlszeile für das Clientbootstrapping
<!--1358215-->
Bei der Installation des Configuration Manager-Clients im Internet über ein CMG sind jetzt weniger Eigenschaften in der Befehlszeile erforderlich. Durch diese Verbesserung wird die Größe der in Microsoft Intune verwendeten Befehlszeile bei der Vorbereitung der Co-Verwaltung reduziert. 

Weitere Informationen finden Sie unter [Vorbereiten internetbasierter Geräte für die Co-Verwaltung](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client).

#### <a name="download-content-from-a-cmg"></a>Herunterladen von Inhalten von einem Cloudverwaltungsgateway
<!--1358651-->
Zuvor mussten Sie einen Cloudverteilungspunkt und ein Cloudverwaltungsgateway als separate Rollen bereitstellen. Jetzt kann ein CMG auch als Inhalt für Clients dienen. Diese Funktion reduziert die erforderlichen Zertifikate und Kosten für Azure-VMs. 

Weitere Informationen finden Sie unter [Ändern eines CMG](../../clients/manage/cmg/setup-cloud-management-gateway.md#modify-a-cmg).

#### <a name="trusted-root-certificate-isnt-required-with-azure-ad"></a>Das vertrauenswürdige Stammzertifikat ist mit Azure AD nicht erforderlich
<!--503899-->
Wenn Sie ein Cloudverwaltungsgateway erstellen, müssen Sie kein [vertrauenswürdiges Stammzertifikat](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_cmgroot) auf der Seite „Einstellungen“ angeben. Dieses Zertifikat ist nicht erforderlich, wenn Sie Azure Active Directory (Azure AD) für die Clientauthentifizierung verwenden. Früher war es im Assistenten erforderlich. Wenn Sie PKI-Clientauthentifizierungszertifikate verwenden, müssen Sie weiterhin ein vertrauenswürdiges Stammzertifikat für das Cloudverwaltungsgateway hinzufügen.



## <a name="co-management"></a>Co-Verwaltung

### <a name="sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device"></a>Synchronisieren von MDM-Richtlinien von Microsoft Intune für ein gemeinsam verwaltetes Gerät
<!--1357377-->
Wenn Sie eine Workload für die Co-Verwaltung verschieben, synchronisieren die gemeinsam verwalteten Geräte automatisch die MDM-Richtlinie von Microsoft Intune. Diese Synchronisierung findet auch statt, wenn Sie die Aktion **Computerrichtlinie herunterladen** aus den Clientbenachrichtigungen in der Configuration Manager-Konsole auslösen. 

Weitere Informationen finden Sie unter [Verschieben von Configuration Manager-Workloads zu Intune](../../../comanage/how-to-switch-workloads.md).


### <a name="transition-new-workloads-to-intune-using-co-management"></a>Übertragen neuer Workloads auf Intune mithilfe der Co-Verwaltung
Die folgenden Workloads können jetzt nach der Aktivierung der Co-Verwaltung von Configuration Manager auf Intune übertragen werden:  

- **Gerätekonfiguration**<!--1357903-->: Mit dieser Workload können Sie Intune zum Bereitstellen von MDM-Richtlinien verwenden, während Sie weiterhin Configuration Manager zum Bereitstellen von Anwendungen verwenden.  

- **Office 365**<!--1357841-->: Geräte installieren keine Office 365-Bereitstellungen über Configuration Manager.  

- **Mobile Apps**<!--1357892-->: Alle über Intune verfügbaren Apps sind im Unternehmensportal verfügbar. Apps, die Sie im Configuration Manager bereitstellen, sind im Softwarecenter verfügbar. Bei diesem Feature handelt es sich um ein [vorab veröffentlichtes Feature](../../servers/manage/pre-release-features.md).  

Wechseln Sie für den Übergang dieser Workloads zur Eigenschaftenseite für die Co-Verwaltung, und bewegen Sie den Schieberegler der Workload von Configuration Manager zu **Pilot** oder **Alle**. 

Weitere Informationen finden Sie unter [Co-Verwaltung für Windows 10-Geräte](../../../comanage/overview.md).


### <a name="support-for-multiple-hierarchies-to-one-intune-tenant"></a>Unterstützung für mehrere Hierarchien für einen Intune-Mandanten
<!--1357944-->
Einige Kunden verfügen über mehrere Configuration Manager-Hierarchien und möchten zukünftig zu einem einzelnen Mandanten für Azure Active Directory und Microsoft Intune konsolidieren. Die Co-Verwaltung unterstützt jetzt das Herstellen einer Verbindung mit mehreren Configuration Manager-Umgebungen für denselben Intune-Mandanten.

Weitere Informationen finden Sie im Artikel zum [Voraussetzungen für die Co-Verwaltung](../../../comanage/overview.md#prerequisites).
 


## <a name="compliance-settings"></a>Kompatibilitätseinstellungen

### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Konfigurieren von Windows Defender SmartScreen-Einstellungen für Microsoft Edge
<!--1353701-->
Der Konformitätsrichtlinie für Microsoft Edge-Browsereinstellungen werden folgende drei Einstellungen für Windows Defender SmartScreen hinzugefügt: 
- SmartScreen zulassen
- Benutzer können SmartScreen-Aufforderung für Websites außer Kraft setzen
- Benutzer können SmartScreen-Aufforderung für Dateien außer Kraft setzen

Weitere Informationen finden Sie unter [Konfigurieren von Microsoft Edge-Einstellungen](../../../compliance/deploy-use/browser-profiles.md).


### <a name="scap-extensions"></a>SCAP-Erweiterungen
<!--1357552-->
Konvertieren von SCAP-Inhalten (SCAP = Security Content Automation Protocol) in Baselines für Konformitätseinstellungen und Generieren von SCAP-Berichten über eine Konsolenerweiterung. Dieses Feature enthält ein neues Dashboard, mit dem die Clientkonformität und die Konformität der XCCDF-Regel visualisiert werden. 





## <a name="application-management"></a>Anwendungsverwaltung

### <a name="phased-deployment-of-applications"></a>Stufenweise Bereitstellung von Anwendungen
<!--1358147-->
Erstellen einer stufenweisen Bereitstellung für eine Anwendung. Mithilfe von Bereitstellungen in Phasen können Sie einen koordinierten, sequenzierten Softwarerollout basierend auf anpassbaren Kriterien und Gruppen orchestrieren. Sie können die Anwendung beispielsweise für eine Pilotsammlung bereitstellen, und anschließend wird der Rollout basierend auf Erfolgskriterien automatisch fortgesetzt. 

Weitere Informationen finden Sie in den folgenden Artikeln:  

- [Erstellen einer Bereitstellung in Phasen](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/apps/toc.json&bc=/mem/configmgr/apps/breadcrumb/toc.json)  

- [Verwalten und Überwachen von Bereitstellungen in Phasen](../../../osd/deploy-use/manage-monitor-phased-deployments.md?toc=/mem/configmgr/apps/toc.json&bc=/mem/configmgr/apps/breadcrumb/toc.json)  


### <a name="provision-windows-app-packages-for-all-users-on-a-device"></a>Bereitstellen von Windows-App-Paketen für alle Benutzer auf einem Gerät
<!--1358310-->
Stellen Sie eine Anwendung mit einem Windows-App-Paket für alle Benutzer auf dem Gerät bereit. Ein allgemeines Beispiel für dieses Szenario ist das Bereitstellen einer App aus dem Microsoft Store für Unternehmen und Bildungseinrichtungen, z. B. Minecraft: Education Edition, für alle Geräte, die von Kursteilnehmer einer Bildungseinrichtung verwendet werden. Zuvor hat Configuration Manager die Installation solcher Anwendungen nur für einzelne Benutzer unterstützt. Wenn ein Schüler sich an einem neuen Gerät anmeldet, musste er warten, bevor er auf eine App zugreifen konnte. Wenn die App nun für das Gerät für alle Benutzer bereitgestellt wird, können sie schneller produktiv sein. 

Weitere Informationen finden Sie unter [Erstellen von Windows-Anwendungen](../../../apps/get-started/creating-windows-applications.md#bkmk_provision).


### <a name="office-customization-tool-integration-with-the-office-365-installer"></a>Integration des Office-Anpassungstools in den Office 365-Installer
<!--1358149-->
Das Office-Anpassungstool ist jetzt in das Office 365-Installer in der Configuration Manager-Konsole integriert. Beim Erstellen einer Bereitstellung für Office 365 können Sie die neuesten Verwaltungseinstellungen von Office dynamisch konfigurieren. Microsoft aktualisiert das Office-Anpassungstool, wenn neue Builds von Office 365 veröffentlicht werden. Mit dieser Integration können Sie neue Verwaltungseinstellungen in Office 365 verwenden, sobald diese verfügbar sind. 

Weitere Informationen finden Sie unter [Bereitstellen von Office 365-Apps](../../../sum/deploy-use/manage-office-365-proplus-updates.md).


### <a name="support-for-new-windows-app-package-formats"></a>Unterstützung für neue Windows-App-Paketformate
<!--1357427-->
Configuration Manager unterstützt jetzt die Bereitstellung der neuen Formate für Windows 10-App-Pakete (.msix) und App-Bundles (.msixbundle). 

Weitere Informationen finden Sie unter [Erstellen von Windows-Anwendungen](../../../apps/get-started/creating-windows-applications.md#bkmk_msix).


### <a name="uninstall-application-on-approval-revocation"></a>Deinstallieren von Anwendungen bei Widerruf von Genehmigungen
<!--1357891-->
Dieses Verhalten hat sich geändert, wenn Sie die Genehmigung für eine Anwendung widerrufen. Wenn Sie die Anforderung der Anwendung ablehnen, deinstalliert der Client nun die Anwendung vom Gerät des Benutzers. Dieses Verhalten erfordert, dass Sie das [optionale Feature](/sccm/core/servers/manage/install-in-console-updates#bkmk_options) **Anwendungsanforderungen für Benutzer pro Gerät genehmigen** aktivieren. 

Weitere Informationen finden Sie unter [Bereitstellen von Anwendungen](../../../apps/deploy-use/deploy-applications.md#bkmk_approval).


### <a name="package-conversion-manager"></a>Package Conversion Manager 
<!--1357861-->
Package Conversion Manager ist nun ein integriertes Tool, mit dem Sie ältere Pakete in Current Branch-Anwendungen von Configuration Manager konvertieren können. Anschließend können Sie Features von Anwendungen verwenden, z.B. Abhängigkeiten, Anforderungsregeln und Affinität zwischen Benutzer und Gerät.

Weitere Informationen finden Sie unter [Paketkonvertierungs-Manager](../../../apps/pcm/package-conversion-manager.md).



## <a name="os-deployment"></a>Bereitstellung des Betriebssystems

### <a name="improvements-to-phased-deployments"></a>Verbesserungen an stufenweisen Bereitstellungen

Dieses Release umfasst die folgenden Verbesserungen an stufenweisen Bereitstellungen:  

#### <a name="create-a-phased-deployment-with-manually-configured-phases"></a>Erstellen einer stufenweisen Bereitstellung mit manuell konfigurierten Phasen
<!--1358148-->
Für eine Tasksequenz können Sie die Phasen jetzt bei Erstellung einer stufenweisen Bereitstellung manuell konfigurieren. Fügen Sie bis zu 10 weitere Phasen aus der Registerkarte **Phasen** des Assistenten zum Erstellen der stufenweisen Bereitstellung hinzu. Sie können weiterhin automatisch eine 2-Phasen-Standardbereitstellung erstellen. 

Weitere Informationen finden Sie unter [Erstellen einer stufenweisen Bereitstellung mit manuell konfigurierten Phasen](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md#bkmk_manual).

#### <a name="phased-deployment-status"></a>Status der stufenweisen Bereitstellung
<!--1358577-->
Bereitstellungen in Phasen verfügen jetzt über eine native Überwachungsoberfläche. Wählen Sie im Knoten **Bereitstellungen** im Arbeitsbereich **Überwachung** eine Bereitstellung in Phasen aus, und klicken Sie dann im Menüband auf **Status der Bereitstellung in Phasen**. 

Weitere Informationen finden Sie unter [Verwalten und Überwachen stufenweiser Bereitstellungen](../../../osd/deploy-use/manage-monitor-phased-deployments.md).  

#### <a name="gradual-rollout-during-phased-deployments"></a>Schrittweiser Rollout während stufenweiser Bereitstellungen
<!--1358578-->
Während einer Bereitstellung in Phasen kann der Rollout in jeder Phase jetzt schrittweise erfolgen. Dieses Verhalten mindert das Risiko von Bereitstellungsproblemen und verringert die Belastung des Netzwerks durch die Verteilung von Inhalten an Clients. Der Standort kann die Software abhängig von der Konfiguration nach und nach für die einzelnen Phasen verfügbar machen. Für jeden Client in einer Phase gilt eine zu dem Zeitpunkt, zu dem die Software zur Verfügung gestellt wird, relative Frist. Das Zeitfenster zwischen dem Zeitpunkt der Verfügbarkeit und der Frist ist für alle Clients in einer Phase identisch. 

Weitere Informationen finden Sie unter [Einstellungen für Phasen](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md#bkmk_settings).  


### <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Verbesserungen an der Tasksequenz für direktes Windows 10-Upgrade
<!--1358500-->
Die Standardvorlage der Tasksequenz für das direkte Windows 10-Upgrade enthält jetzt eine zusätzliche neue Gruppe mit empfohlenen Aktionen, die zusätzlich durchgeführt werden, falls bei dem Upgradevorgang ein Fehler auftritt. Diese Aktionen erleichtern die Problembehandlung. Ein solches Tool ist Windows [SetupDiag](/windows/deployment/upgrade/setupdiag). Mit diesem eigenständigen Diagnosetool können Sie Details zur Ursache des erfolglosen Versuchs eines Windows 10-Upgrades abrufen. 

Weitere Informationen finden Sie unter [Erstellen einer Tasksequenz zum Durchführen eines Upgrades für ein Betriebssystem](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#recommended-task-sequence-steps-on-failure).


### <a name="improvements-to-pxe-enabled-distribution-points"></a>Verbesserungen an PXE-fähigen Verteilungspunkten
<!--1357580-->
Aktivieren Sie auf der Registerkarte **PXE** der Eigenschaften des Verteilungspunkts die Option **PXE-Antwortdienst ohne Windows-Bereitstellungsdienst aktivieren**. Diese neue Option aktiviert einen PXE-Antwortdienst auf dem Verteilungspunkt, der keine Windows Deployment Services (Windows Deployment Service, WDS) benötigt. Da WDS nicht erforderlich ist, kann auf dem PXE-fähigen Verteilungspunkt ein Client- oder Serverbetriebssystem ausgeführt werden, einschließlich Windows Server Core. Dieser neue PXE-Antwortdienst unterstützt IPv6 und erweitert zudem die Flexibilität von PXE-fähigen Verteilungspunkten in Remotebüros. 

Weitere Informationen finden Sie unter [Aktivieren von PXE auf dem Verteilungspunkt](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).


### <a name="network-access-account-not-required-for-some-scenarios"></a>Für einige Szenarios ist kein Netzwerkzugriffskonto erforderlich
<!--1358278,1358279-->
Das Feature [Erweitertes HTTP-Standortsystem](#bkmk_ehttp) entfernt auch einige Abhängigkeiten vom Netzwerkzugriffskonto. Wenn Sie die neue Standortoption **Für HTTP-Websitesysteme von Configuration Manager generierte Zertifikate verwenden** aktivieren, erfordern die folgenden Szenarios keine Netzwerkzugriffskonten zum Herunterladen von Inhalten von einem Verteilungspunkt:  

- Tasksequenzen, die über ein Bootmedium oder über PXE ausgeführt werden
- Tasksequenzen, die über das Softwarecenter ausgeführt werden  

Diese Tasksequenzen können für die Betriebssystembereitstellung oder benutzerdefinierte Bereitstellung verwendet werden. Sie werden auch von Arbeitsgruppencomputern unterstützt.

Weitere Informationen finden Sie unter [Tasksequenzen und das Netzwerkzugriffskonto](../../../osd/plan-design/planning-considerations-for-automating-tasks.md#BKMK_TSNetworkAccessAccount).


### <a name="other-improvements-to-os-deployment"></a>Weitere Verbesserungen bei der Bereitstellung von Betriebssystemen

#### <a name="mask-sensitive-data-stored-in-task-sequence-variables"></a>Verbergen vertraulicher Daten, die in Tasksequenzvariablen gespeichert sind
 <!--1358330-->
 Wählen Sie im Schritt **Tasksequenzvariable festlegen** die neue Option **Diesen Wert nicht anzeigen** aus. 

 Weitere Informationen finden Sie unter [Tasksequenzvariable festlegen](../../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable). 

#### <a name="mask-program-name-during-run-command-step-of-a-task-sequence"></a>Verbergen des Programmnamens während des Schritts „Befehlszeile ausführen“ einer Tasksequenz
 <!--1358493-->
 Wenn Sie verhindern möchten, dass möglicherweise vertrauliche Daten angezeigt oder protokolliert werden, konfigurieren Sie die Tasksequenzvariable **OSDDoNotLogCommand**.  

 Weitere Informationen finden Sie unter [Tasksequenzvariablen](../../../osd/understand/task-sequence-variables.md#OSDDoNotLogCommand). 

#### <a name="task-sequence-variable-for-dism-parameters-when-installing-drivers"></a>Tasksequenzvariable für DISM-Parameter beim Installieren von Treibern
 <!--516679/2840016-->
 Verwenden Sie für die Angabe zusätzlicher Befehlszeilenparameter für DISM die neue Tasksequenzvariable **OSDInstallDriversAdditionalOptions**. 

 Weitere Informationen finden Sie unter [Tasksequenzvariablen](../../../osd/understand/task-sequence-variables.md#OSDInstallDriversAdditionalOptions). 

#### <a name="option-to-use-full-disk-encryption"></a>Option für die Verwendung der vollständigen Datenträgerverschlüsselung
 <!--SCCMDocs-pr issue 2671-->
 Sowohl der Schritt **BitLocker aktivieren** als auch der Schritt **BitLocker vorab bereitstellen** enthalten jetzt die Option **Vollständige Datenträgerverschlüsselung** verwenden. In diesen Schritten wird standardmäßig belegter Speicherplatz auf dem Laufwerk verschlüsselt. Dieses Standardverhalten wird aufgrund der Schnelligkeit und Effizienz empfohlen. 

 Weitere Informationen finden Sie im Abschnitt [Aktivieren von BitLocker](../../../osd/understand/task-sequence-steps.md#BKMK_EnableBitLocker) und [Vorabbereitstellen von BitLocker](../../../osd/understand/task-sequence-steps.md#BKMK_PreProvisionBitLocker). 

#### <a name="client-provisioning-mode-isnt-enabled-with-windows-10-upgrade-compatibility-scan"></a>Der Clientbereitstellungsmodus wird bei der Überprüfung der Kompatibilität mit dem Windows 10-Upgrade nicht aktiviert
 <!--SCCMDocs-pr issue 2812-->
 Wenn Sie nun die Option **Kompatibilitätsprüfung für Windows Setup ausführen**, ohne ein Upgrade zu starten aktivieren, versetzt der Tasksequenzschritt **Betriebssystem aktualisieren** den Configuration Manager-Client nicht in den Bereitstellungsmodus.

 Weitere Informationen finden Sie unter [Betriebssystem aktualisieren](../../../osd/understand/task-sequence-steps.md#BKMK_UpgradeOS).

#### <a name="revised-documentation-for-task-sequence-variables"></a>Dokumentation für Tasksequenzvariablen überarbeitet
Zwei neue Artikel stehen jetzt als Erläuterungen zu Tasksequenzvariablen bereit:  

- [Verwenden von Tasksequenzvariablen](../../../osd/understand/using-task-sequence-variables.md) ist ein neuer Artikel, in dem die verschiedenen Typen von Variablen, Methoden zum Festlegen von Variablen und der Zugriff darauf beschrieben wird.  

- [Tasksequenzvariablen](../../../osd/understand/task-sequence-variables.md) bietet eine Referenz für alle verfügbaren Tasksequenzvariablen. Dieser Artikel kombiniert die vorherigen Artikel, in denen integrierte Variablen von Aktionsvariablen getrennt waren. 



## <a name="software-center"></a>Software Center

> [!Important]  
> Wenn Sie neue Configuration Manager-Features nutzen möchten, müssen Sie zunächst die Clients auf die neueste Version aktualisieren. Beim Update des Standorts und der Konsole werden neue Features in der Configuration Manager-Konsole angezeigt. Das vollständige Szenario ist allerdings erst einsatzbereit, wenn auch die Clientversion aktualisiert wird.


### <a name="software-center-infrastructure-improvements"></a>Verbesserungen an der Infrastruktur des Softwarecenters
<!--1358309-->
Es werden keine Anwendungskatalogrollen mehr benötigt, um für Benutzer verfügbare Anwendungen im Softwarecenter anzuzeigen. Diese Änderung hilft dabei, die erforderliche Serverinfrastruktur zu reduzieren, um Anwendungen schneller für Benutzer bereitzustellen. Softwarecenter verlässt sich nun auf den Verwaltungspunkt, um diese Informationen abzurufen, weshalb größere Umgebungen besser skaliert werden, da sie [Begrenzungsgruppen](../../servers/deploy/configure/boundary-groups.md#management-points) zugewiesen werden.

Weitere Informationen finden Sie unter [Konfigurieren des Softwarecenters](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex).  

> [!Note]  
> Der Anwendungspunkt-Websitepunkt und die Webdienstpunkt-Rollen sind in Version 1806 *nicht mehr erforderlich*, die Rollen werden jedoch weiterhin *unterstützt*. 
> 
> Die **Silverlight-Benutzeroberfläche** für den Anwendungskatalog-Websitepunkt wird nicht mehr unterstützt. Weitere Informationen finden Sie unter [Entfernte und veraltete Features](deprecated/removed-and-deprecated-cmfeatures.md).  


### <a name="specify-the-visibility-of-the-application-catalog-website-link-in-software-center"></a>Angeben der Sichtbarkeit des Links zur Anwendungskatalog-Website im Softwarecenter
<!--1358214-->
Sie können über die Clienteinstellungen steuern, ob die Verknüpfung mit **Website des Anwendungskatalogs öffnen** auf dem Knoten **Installationsstatus** des Softwarecenters angezeigt wird.  

Weitere Informationen finden Sie unter [Softwarecenter-Clienteinstellungen](../../clients/deploy/about-client-settings.md#software-center).

> [!Note]  
> Die **Silverlight-Benutzeroberfläche** für den Anwendungskatalog-Websitepunkt wird nicht mehr unterstützt. Weitere Informationen finden Sie unter [Entfernte und veraltete Features](deprecated/removed-and-deprecated-cmfeatures.md).  


### <a name="custom-tab-for-webpage-in-software-center"></a>Registerkarte „Benutzerdefiniert“ für Webseite im Softwarecenter
<!--1358132-->
Verwenden von Clienteinstellungen zum Erstellen einer benutzerdefinierten Registerkarte, um eine Webseite im Softwarecenter zu öffnen. Mit diesem Feature können Sie Ihren Endbenutzern Inhalte auf eine konsistente und zuverlässige Weise anzeigen. Die folgende Liste enthält einige Beispiele:  

- IT kontaktieren: Informationen, wie die IT-Abteilung Ihrer Organisation kontaktiert werden kann  

- IT-Supportcenter: IT-Self-Service-Aktionen wie das Durchsuchen einer Wissensdatenbank oder das Öffnen eines Supporttickets.  

- Endbenutzerdokumentation: Artikel für Benutzer in Ihrer Organisation zu verschiedenen IT-Themen wie beispielsweise die Verwendung von Anwendungen oder die Aufrüstung auf Windows 10.  

Weitere Informationen finden Sie unter [Softwarecenter-Clienteinstellungen](../../clients/deploy/about-client-settings.md#software-center) und im [Benutzerleitfaden für Softwarecenter](../../understand/software-center.md).


### <a name="maintenance-windows-in-software-center"></a>Wartungsfenster im Softwarecenter
<!--1358131-->
Das Softwarecenter zeigt jetzt das nächste geplante Wartungsfenster an. Wechseln Sie auf der Registerkarte „Installationsstatus“ von „Alle“ zu „Bevorstehend“. Nun werden der Zeitraum und die Liste der geplanten Bereitstellungen angezeigt. Die Liste ist leer, wenn es keine kommenden Wartungsfenster gibt. 

Weitere Informationen finden Sie unter [Verwenden von Wartungsfenstern](../../clients/manage/collections/use-maintenance-windows.md) und im [Benutzerleitfaden für das Softwarecenter](../../understand/software-center.md).



## <a name="software-updates"></a>Softwareupdates

### <a name="third-party-software-updates"></a>Updates für Drittanbietersoftware
<!--1357605, 1352101, 1358714-->
Updates für Drittanbietersoftware ermöglichen Ihnen das Abonnieren von Partnerkatalogen in der Configuration Manager-Konsole und das Veröffentlichen der Updates in WSUS. Anschließend können Sie diese Updates mithilfe des vorhandenen Verwaltungsprozesses für Softwareupdates bereitstellen. 

Weitere Informationen finden Sie unter [Aktivieren von Updates von Drittanbietern](../../../sum/deploy-use/third-party-software-updates.md).


### <a name="deploy-software-updates-without-content"></a>Bereitstellen von Softwareupdates ohne Inhalt
<!--1357933-->
Bereitstellen von Softwareupdates auf Geräten ohne vorheriges Herunterladen und Verteilen von Inhalten zu Verteilungspunkten. Dieses Feature ist nützlich, wenn Sie mit großen Updateinhalten arbeiten, oder wenn Clients den Inhalt immer vom Microsoft Update-Clouddienst erhalten sollen. Clients können den Inhalt in diesem Szenario auch von Peers herunterladen, die bereits über den erforderlichen Inhalt verfügen. Der Configuration Manager-Client verwaltet weiterhin den Inhaltsdownload und kann deshalb das Feature „Peercache“ von Configuration Manager oder andere Technologien verwenden, z.B. die Übermittlungsoptimierung. Dieses Feature unterstützt alle Updatetypen, die von der Configuration Manager-Softwareupdateverwaltung unterstützt werden, einschließlich Windows- und Office-Updates. 

Weitere Informationen finden Sie unter der Option **Kein Bereitstellungspaket**, wenn Sie den Vorgang [Manuelles Bereitstellen von Softwareupdates](../../../sum/deploy-use/manually-deploy-software-updates.md) oder [Automatisches Bereitstellen von Softwareupdates](../../../sum/deploy-use/automatically-deploy-software-updates.md) durchführen.


### <a name="filter-automatic-deployment-rules-by-software-update-architecture"></a>Filtern der automatischen Bereitstellungsregeln durch Softwareupdates für Architektur
 <!--1322266-->
Sie können jetzt Regeln zur automatischen Bereitstellung (Automatic Deployment Rules, ADR) filtern, um Architekturen auszuschließen, z. B. Itanium und ARM64. Auf der Seite **Softwareupdates** des Assistenten zum Erstellen von Regeln zur automatische Bereitstellung ist jetzt der Eigenschaftenfilter **Architektur** verfügbar. 

Weitere Informationen finden Sie unter [Automatically deploy software updates (Automatisches Bereitstellen von Softwareupdates)](../../../sum/deploy-use/automatically-deploy-software-updates.md).


### <a name="improved-wsus-maintenance"></a>Verbesserte WSUS-Wartung 
<!--1357898-->
Der WSUS-Bereinigungsassistent lehnt jetzt Updates ab, die gemäß den für die Eigenschaften der Softwareupdatepunkt-Komponente definierten Ablösungsregeln abgelaufen sind. 

Weitere Informationen finden Sie unter [Wartung von Softwareupdates](../../../sum/deploy-use/software-updates-maintenance.md).



## <a name="reporting"></a>Berichterstellung

### <a name="new-software-updates-compliance-report"></a>Neuer Bericht zur Konformität von Softwareupdates
<!--1357775-->
Das Anzeigen von Berichten zur Konformität von Softwareupdates umfasst normalerweise Daten von Clients, die seit einiger Zeit keinen Kontakt mehr mit dem Standort hatten. In einem neuen Bericht, **Compliance 9 – Overall health and compliance** (Konformität 9: Gesamtintegrität und Konformität), können Sie Konformitätsergebnisse für eine bestimmte Softwareupdategruppe nach „fehlerfreien“ Clients filtern. Dieser Bericht zeigt den realistischeren Konformitätsstatus der aktiven Clients in Ihrer Umgebung. 

Weitere Informationen finden Sie unter [Berichte zu Softwareupdates](../../../sum/deploy-use/monitor-software-updates.md#BKMK_SUReports).



## <a name="inventory"></a>Inventarisierung

### <a name="improvement-to-hardware-inventory-for-large-integer-values"></a><a name="bkmk_bigint"></a> Verbesserung der Hardwareinventur für große ganzzahlige Werte
<!--1357880-->
Für die Hardwareinventur galt bisher für ganze Zahlen der Höchstwert 4.294.967.296 (2^32). Attribute wie z.B. die Festplattengröße in Bytes könnten diesen Grenzwert erreichen. Da der Verwaltungspunkt keine höheren Ganzzahlwerte verarbeitet, wurden diese Werte nicht in der Datenbank gespeichert. Ab diesem Release beträgt der Höchstwert 18.446.744.073.709.551.616 (2^64). 

Weitere Informationen finden Sie unter [Verwenden hoher ganzzahliger Werte](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md#bkmk_bigint).


### <a name="hardware-inventory-default-unit-revision"></a>Überarbeitung der Standardeinheit der Hardwareinventur
<!--514442-->
In [Configuration Manager Version 1710](whats-new-in-version-1710.md#site-infrastructure) wurde die Standardeinheit in vielen Berichtsansichten von Megabytes (MB) in Gigabytes (GB) geändert. Aufgrund von [Verbesserungen der Hardwareinventur für große ganzzahlige Werte](#bkmk_bigint) und Kundenfeedback ist MB nun wieder die Standardeinheit.



<!-- ## Mobile device management -->



<!-- ## Protect devices-->




## <a name="configuration-manager-console"></a>Configuration Manager-Konsole

### <a name="product-lifecycle-dashboard"></a>Dashboard für den Produktlebenszyklus
<!--1319632-->
Das Dashboard für den Produktlebenszyklus zeigt den Status der Microsoft Lifecycle-Richtlinie für Microsoft-Produkte an, die auf mit Configuration Manager verwalteten Geräten installiert sind. Es stellt Ihnen außerdem Informationen zu Microsoft-Produkten in Ihrer Umgebung, deren Supportfähigkeit und den Daten des Supportendes zur Verfügung. Auf diesem Dashboard erfahren Sie, welche Art von Support für die jeweiligen Produkte verfügbar ist. Diese Informationen helfen Ihnen dabei, zu planen, wann Sie die von Ihnen verwendeten Microsoft-Produkte aktualisieren müssen, bevor das Ende des Supports erreicht ist.   

Weitere Informationen finden Sie unter [Dashboard für den Produktlebenszyklus](../../clients/manage/asset-intelligence/product-lifecycle-dashboard.md).


### <a name="copy-asset-details-from-monitoring-views"></a>Kopieren von Bestandsdetails von Überwachungsansichten
<!--1357856-->
In den folgenden Bereichen des Arbeitsbereichs **Überwachung** wird jetzt das Kopieren von Text unterstützt:  

- Wählen Sie im Knoten **Bereitstellungen** eine Bereitstellung aus, und klicken Sie auf **Status anzeigen**. Wählen Sie in der Ansicht „Bereitstellungsstatus“ im Bereich **Bestandsdetails** mindestens ein Gerät aus.  

- Erweitern Sie den Knoten **Verteilungsstatus**, und wählen Sie **Inhaltsstatus** aus. Wählen Sie eine Softwarekomponente aus, und klicken Sie auf **Status anzeigen**. Wählen Sie in der Ansicht „Inhaltsstatus“ im Bereich **Bestandsdetails** mindestens ein Gerät aus. 

Klicken Sie mit der rechten Maustaste auf den Bestand, und klicken Sie auf **Kopieren**. Durch diese Aktion werden die ausgewählten Bestände als durch Trennzeichen getrennte Liste kopiert, die die vollständigen Details enthält. Die Tastenkombination **STRG** + **C** kann in diesen Ansichten auch verwendet werden. 

Weitere Informationen finden Sie unter [Verbesserungen der Konsole in Version 1806](../../servers/manage/admin-console-tips.md#copy-details-in-monitoring-views).


### <a name="improvements-to-the-surface-dashboard"></a>Verbesserungen am Surface-Dashboard
<!--1358654-->
Dieses Release umfasst die folgenden Verbesserungen am Surface-Dashboard:  

- Das Surface-Dashboard zeigt ab sofort eine Liste der relevanten Geräte an, wenn Sie bestimmte Diagrammabschnitte auswählen:  

   - Wenn Sie auf die Kachel **Prozent der Surface-Geräte** klicken, wird eine Liste der Surface-Geräte geöffnet.  

   - Wenn Sie auf die Kachel **Top 5-Firmwareversionen** klicken, wird eine Liste der Surface-Geräte mit der entsprechenden Firmwareversion geöffnet.  

- Wenn Sie diese Gerätelisten über das Surface-Dashboard anzeigen, können Sie mit der rechten Maustaste auf ein Gerät klicken und allgemeine Aktionen durchführen.  

Weitere Informationen finden Sie unter [Surface-Dashboard](../../clients/manage/surface-device-dashboard.md).


### <a name="view-the-currently-signed-on-user-for-a-device"></a>Anzeigen des derzeit angemeldeten Benutzers für ein Gerät
<!--1358202-->
Auf dem Knoten **Geräte** des Arbeitsbereichs **Bestand und Konformität** wird die Spalte **Derzeit angemeldeter Benutzer** angezeigt. Darüber hinaus wird eine sammlungsspezifische Geräteliste angezeigt. Dieser Wert ist so aktuell wie die [Clientstatus](../../clients/manage/monitor-clients.md#bkmk_indStatus). Wenn sich der Benutzer abmeldet, löscht der Client diesen Wert. Wenn kein Benutzer angemeldet ist, ist der Wert leer. 

Weitere Informationen finden Sie unter [Verbesserungen der Konsole in Version 1806](../../servers/manage/admin-console-tips.md#view-users-for-a-device).


### <a name="submit-feedback-from-the-configuration-manager-console"></a>Übermitteln von Feedback über die Configuration Manager-Konsole  
<!--1357542-->

Senden Sie ein Lächeln! Sie können dem Configuration Manager-Team jetzt direkt Ihre Erfahrungen mitteilen. Das Senden von Feedback über die Configuration Manager-Konsole ist ein Kinderspiel. Wir möchten Ihr gesamtes Feedback hören: Lob, Probleme und Vorschläge. Klicken Sie in der Configuration Manager-Konsole auf die Schaltfläche „Lächeln“ in der oberen rechten Ecke des Menübands. Dieses Feedback erreicht direkt das Microsoft-Produktteam für Configuration Manager. Obwohl der Feedback-Hub von Windows 10 weiterhin unterstützt wird, sollten Sie vom konsoleninternen Feedback-Mechanismus Gebrauch machen.  

Weitere Informationen finden Sie unter [Verbesserungen der Konsole in Version 1806](../../servers/manage/admin-console-tips.md#send-feedback) und unter [Produktfeedback](../../understand/find-help.md#BKMK_1806Feedback).



## <a name="other-updates"></a>Weitere Updates

Neben neuen Features umfasst dieses Release auch weitere Änderungen, beispielsweise Fehlerbehebungen. Weitere Informationen finden Sie unter [Summary of changes in Configuration Manager current branch, version 1806 (Zusammenfassung der Änderungen in der Current Branch-Version 1806 von Configuration Manager)](https://support.microsoft.com/help/4459701).

Weitere Informationen zu Änderungen der Windows PowerShell-Cmdlets für Configuration Manager finden Sie unter [PowerShell 1806 Release Notes (Versionshinweise zu PowerShell 1806)](/powershell/sccm/1806_release_notes?view=sccm-ps).

Folgender Updaterollup (4462978) ist ab dem 24. Oktober 2018 in der Konsole verfügbar: [Update rollup for Configuration Manager current branch, version 1806 (Updaterollup für die Current Branch-Version 1806 von Configuration Manager)](https://support.microsoft.com/help/4462978).


### <a name="hotfixes"></a>Hotfixes

Folgende zusätzliche Hotfixes wurden veröffentlicht, um bestimmte Probleme zu beheben:

| ID | Titel | Datum | In der Konsole |
|---------|---------|---------|---------|
| [4346645](https://support.microsoft.com/help/4346645) | Update für Version 1806 von Configuration Manager (erste Welle) | 31. August 2018 | Ja |
| [4465865](https://support.microsoft.com/help/4465865) | Softwareupdates werden in der Umgebung von Configuration Manager nicht heruntergeladen, wenn WSUS nicht verbunden ist.<br><br>Dieses Update ist ebenfalls im Updaterollup (4462978) enthalten. | 1\. Oktober 2018 | Ja |
| [4471892](https://support.microsoft.com/help/4471892) | Der PXE-Antwortdienst funktioniert in Configuration Manager 1806 nicht in Subnetzen. | 23. November 2018 | Nein |
| [4487960](https://support.microsoft.com/help/4487960) | Das Microsoft Intune-Connectorzertifikat wird nicht in Configuration Manager erneuert | 18. Januar 2019 | Ja |


## <a name="next-steps"></a>Nächste Schritte

Wenn Sie zum Installieren dieser Version bereit sind, finden Sie unter [Installieren von Updates für Configuration Manager](../../servers/manage/updates.md) und [Checkliste für die Installation von Update 1806](../../servers/manage/checklist-for-installing-update-1806.md) weitere Informationen.

> [!TIP]  
> Verwenden Sie eine Baselineversion von Configuration Manager, um einen neuen Standort zu installieren.  
>
> Weitere Informationen:    
> - [Installieren von neuen Standorten](../../servers/deploy/install/installing-sites.md)  
> - [Baseline- und Updateversionen](../../servers/manage/updates.md#bkmk_Baselines)

Informationen zu bekannten, erheblichen Problemen finden Sie in den [Versionshinweisen](../../servers/deploy/install/release-notes.md).

Nachdem Sie einen Standort aktualisiert haben, überprüfen Sie auch die [Checkliste für Aufgaben nach dem Update](../../servers/manage/checklist-for-installing-update-1806.md#post-update-checklist).