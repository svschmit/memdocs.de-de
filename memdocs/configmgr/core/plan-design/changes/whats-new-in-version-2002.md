---
title: Neuerungen in Version 2002
titleSuffix: Configuration Manager
description: Hier erfahren Sie mehr über Änderungen und neue Funktionen, die in Version 2002 des Current Branchs von Configuration Manager eingeführt wurden.
ms.date: 05/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: de718cdc-d0a9-47e2-9c99-8fa2cb25b5f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: afdcc608133d306042c9c6dc817396bb2fc3f387
ms.sourcegitcommit: b0ae4a9972bac3518d0d4f33e033ac492eefe3c1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/28/2020
ms.locfileid: "84126480"
---
# <a name="whats-new-in-version-2002-of-configuration-manager-current-branch"></a>Neuerungen in Version 2002 von Configuration Manager (Current Branch)

*Gilt für: Configuration Manager (Current Branch)*

Das Update 2002 für Configuration Manager (Current Branch) ist als konsoleninternes Update verfügbar. Wenden Sie dieses Update auf Standorte an, an denen Version 1810 oder höher ausgeführt wird. <!-- baseline only statement:-->Beim Installieren eines neuen Standorts steht das Update auch als Baselineversion zur Verfügung. In diesem Artikel werden die Änderungen und neuen Features in Configuration Manager Version 2002 zusammengefasst.

Überprüfen Sie stets die neueste Checkliste für die Installation dieses Updates. Weitere Informationen finden Sie in der [Checkliste für die Installation von Update 2002](../../servers/manage/checklist-for-installing-update-2002.md). Nachdem Sie einen Standort aktualisiert haben, überprüfen Sie auch die [Checkliste für Aufgaben nach dem Update](../../servers/manage/checklist-for-installing-update-2002.md#post-update-checklist).

Wenn Sie die neuen Configuration Manager-Features nach der Aktualisierung des Standorts vollständig nutzen möchten, müssen Sie auch Clients auf die neueste Version aktualisieren. Beim Update des Standorts und der Konsole werden neue Features in der Configuration Manager-Konsole angezeigt. Das vollständige Szenario ist allerdings erst einsatzbereit, wenn auch die Clientversion aktualisiert wird.

> [!TIP]
> Um bei einer Aktualisierung dieser Seite benachrichtigt zu werden, kopieren Sie die folgende URL, und fügen Sie sie in Ihren RSS-Feedreader ein: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+2002+-+Configuration+Manager%22&locale=en-us`

## <a name="microsoft-endpoint-manager-tenant-attach"></a><a name="bkmk_tenant"></a> Anfügen von Mandanten in Microsoft Endpoint Manager

### <a name="device-sync-and-device-actions"></a><a name="bkmk_attach"></a> Gerätesynchronisierung und Geräteaktionen
<!--3555758-->
Microsoft Endpoint Manager ist eine integrierte Lösung für die Verwaltung all Ihrer Geräte. Microsoft vereint Configuration Manager und Intune in einer einzigen Konsole namens **Microsoft Endpoint Manager Admin Center**. Ab diesem Release können Sie Ihre Configuration Manager-Geräte in den Clouddienst laden und Aktionen im Blatt **Geräte** des Admin Centers ausführen.

Weitere Informationen finden Sie unter [Anfügen von Mandanten in Microsoft Endpoint Manager](../../../tenant-attach/device-sync-actions.md).

## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> Standortinfrastruktur

### <a name="remove-a-central-administration-site"></a>Entfernen eines Standorts der zentralen Verwaltung
<!-- 3607277 -->

Wenn Ihre Hierarchie aus einem Standort der zentralen Verwaltung (CAS) und einem einzelnen untergeordneten primären Standort besteht, können Sie ersteren nun entfernen. Dadurch wird Ihre Configuration Manager-Infrastruktur vereinfacht und auf einen einzelnen, eigenständigen primären Standort reduziert. Die komplexe Replikation zwischen Standorten wird beseitigt, und Ihre Verwaltungsaufgaben werden an einem einzelnen Standort zusammengeführt.

Weitere Informationen finden Sie unter [Entfernen des Standorts der zentralen Verwaltung](../../servers/deploy/install/remove-central-administration-site.md).

### <a name="new-management-insight-rules"></a>Neue Regeln für Verwaltungserkenntnisse

Dieses Release umfasst die folgenden Regeln für Verwaltungserkenntnisse:

- Neun Regeln in der **Configuration Manager Assessment**-Gruppe, die von der Microsoft Premier Field Engineering-Abteilung bereitgestellt werden. Diese Regeln sind eine Stichprobe aus einer ganzen Reihe von Überprüfungen, die von Microsoft Premier im Diensthub bereitgestellt werden.<!-- 3607758 -->

  - Active Directory-Sicherheitsgruppenermittlung für eine zu häufige Ausführung konfiguriert
  - Active Directory-Systemermittlung für eine zu häufige Ausführung konfiguriert
  - Active Directory-Benutzerermittlung für eine zu häufige Ausführung konfiguriert
  - Auf „Alle Systeme“ oder „Alle Benutzer“ beschränkte Sammlungen
  - Frequenzermittlung ist deaktiviert
  - Sammlungsabfragen mit langer Ausführungszeit für inkrementelle Updates aktiviert
  - Anzahl von Anwendungen und Paketen auf Verteilungspunkten verringern
  - Probleme mit Installation am sekundären Standort
  - Alle Standorte auf dieselbe Version aktualisieren

- Zwei zusätzliche Regeln in der **Cloud Services**-Gruppe helfen Ihnen beim Konfigurieren Ihrer Website für das Hinzufügen der sicheren HTTPS-Kommunikation:<!-- 6268489 -->

  - Sites that don't have proper HTTPS configuration (Standorte ohne richtige HTTPS-Konfiguration)
  - Devices not uploaded to Azure AD (Nicht in Azure AD hochgeladene Geräte)

Weitere Informationen finden Sie unter [Einblicke für die Verwaltung](../../servers/manage/management-insights.md).

### <a name="improvements-to-administration-service"></a>Verbesserungen am Verwaltungsdienst

<!-- 5728365 -->

Der Verwaltungsdienst ist eine REST-API für SMS-Anbieter. Bisher mussten Sie eine der folgenden Abhängigkeiten implementieren:

- Aktivieren des erweiterten HTTP-Protokolls für die gesamte Website
- Manuelles Binden eines PKI-basierten Zertifikats an die Internetinformationsdienste auf dem Server, auf dem die SMS-Anbieterrolle gehostet wird

Ab diesem Release verwendet der Verwaltungsdienst automatisch das selbstsignierte Zertifikat der Website. Diese Änderung trägt zur vereinfachten Verwendung des Verwaltungsdiensts bei. Das Zertifikat wird immer von der Website generiert. Die erweiterte HTTP-Websiteeinstellung **Für HTTP-Websitesysteme von Configuration Manager generierte Zertifikate verwenden** steuert nur, ob Websitesysteme das Protokoll verwenden oder nicht. Nun ignoriert der Verwaltungsdienst diese Websiteeinstellung, da er immer das Zertifikat der Website verwendet, selbst wenn kein anderes Websitesystem einen erweiterten HTTP-Standard verwendet. Sie können weiterhin ein PKI-basiertes Serverauthentifizierungszertifikat verwenden.

Weitere Informationen finden Sie in den folgenden Artikeln:

- [Was ist der Verwaltungsdienst?](../../../develop/adminservice/overview.md)
- [Einrichten des Verwaltungsdiensts](../../../develop/adminservice/set-up.md)

### <a name="proxy-support-for-azure-active-directory-discovery-and-group-sync"></a>Proxyunterstützung für Azure Active Directory-Ermittlung und -Gruppensynchronisierung

<!-- 5913817 -->

Die Proxyeinstellungen des Standortsystems (einschließlich Authentifizierung) werden jetzt von folgenden Komponenten verwendet:

- Azure Active Directory-Benutzerermittlung (Azure AD)
- Azure AD-Benutzergruppenermittlung
- Synchronisieren der Sammlungsmitgliedschaftsergebnisse mit Azure Active Directory-Gruppen

Weitere Informationen finden Sie unter [Unterstützung von Proxyservern](../network/proxy-server-support.md#bkmk_other).

## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a> Cloudgestützte Verwaltung

### <a name="critical-status-message-shows-server-connection-errors-to-required-endpoints"></a>Kritische Statusmeldung zeigt Serververbindungsfehler für erforderliche Endpunkte an

<!-- 5566763 -->

Wenn die Verbindung des Configuration Manager-Standortservers mit den erforderlichen Endpunkten für einen Clouddienst nicht hergestellt werden kann, wird eine kritische Statusmeldung mit der ID 11488 ausgegeben. Wenn der Standortserver keine Verbindung mit dem Dienst herstellen kann, wird der Status der Komponente „SMS_SERVICE_CONNECTOR“ in „kritisch“ geändert. Zeigen Sie detaillierte Statusinformationen im Knoten „Komponentenstatus“ in der Configuration Manager-Konsole an.

### <a name="token-based-authentication-for-cloud-management-gateway"></a>Tokenbasierte Authentifizierung für Cloud Management Gateway

<!-- 5686290 -->

Cloud Management Gateway (CMG) unterstützt zwar viele Clienttypen, aber auch mit erweitertem HTTP erfordern diese Clients ein Clientauthentifizierungszertifikat. Diese Zertifikatanforderung kann beim Bereitstellen auf internetbasierten Clients Probleme bereiten, die nicht häufig eine Verbindung mit dem internen Netzwerk herstellen, mit Azure Active Directory (Azure AD) verknüpft werden können und über keine Methode zum Installieren eines von der PKI ausgestellten Zertifikats verfügen.

Configuration Manager erweitert die Geräteunterstützung um die folgenden Methoden:

- Registrieren im internen Netzwerk für ein eindeutiges Token
- Erstellen eines Tokens für die Massenregistrierung von internetbasierten Geräten

Weitere Informationen finden Sie unter [Tokenbasierte Authentifizierung für CMG](../../clients/deploy/deploy-clients-cmg-token.md).

### <a name="microsoft-endpoint-configuration-manager-cloud-features"></a>Microsoft Endpoint Configuration Manager-Cloudfeatures

<!--5834830-->

Wenn neue cloudbasierte Features im Microsoft Endpoint Manager Admin Center oder in anderen angefügten Clouddiensten für Ihre lokale Configuration Manager-Installation verfügbar sind, können Sie diese neuen Features jetzt in der Configuration Manager-Konsole aktvieren. Weitere Informationen zum Aktivieren von Features in der Configuration Manager-Konsole finden Sie unter [Aktivieren optionaler Features von Updates](../../servers/manage/install-in-console-updates.md#bkmk_options).

## <a name="desktop-analytics"></a><a name="bkmk_da"></a> Desktop Analytics

Weitere Informationen zu den monatlichen Änderungen am Desktop Analytics-Clouddienst finden Sie unter [Neues in Desktop Analytics](../../../desktop-analytics/whats-new.md).

### <a name="connection-health-dashboard-shows-client-connection-issues"></a>Dashboard „Verbindungsintegrität“ zeigt Probleme bei der Clientverbindung an

Verwenden Sie in Configuration Manager das Desktop Analytics-Dashboard „Verbindungsintegrität“, um die Verbindungsintegrität des Clients zu überwachen. Nun können Sie Probleme mit der Clientproxykonfiguration in zwei Bereichen leichter erkennen:

- **Endpunktkonnektivitätsüberwachung:** Wenn Clients einen erforderlichen Endpunkt nicht erreichen können, wird auf dem Dashboard eine Konfigurationswarnung angezeigt. Führen Sie einen Drilldown aus, um die Endpunkte anzuzeigen, auf die Clients aufgrund von Problemen mit der Proxykonfiguration nicht zugreifen können.<!-- 4963230 -->

- **Konnektivitätsstatus:** Wenn Ihre Clients einen Proxyserver für den Zugriff auf den Desktop Analytics-Clouddienst verwenden, werden in Configuration Manager jetzt Probleme bei der Proxyauthentifizierung von Clients angezeigt. Führen Sie einen Drilldown aus, um Clients anzuzeigen, die aufgrund der Proxyauthentifizierung nicht registriert werden können.<!-- 4963383 -->

Weitere Informationen finden Sie unter [Überwachen der Verbindungsintegrität](../../../desktop-analytics/monitor-connection-health.md).

## <a name="real-time-management"></a><a name="bkmk_real"></a> Verwaltung in Echtzeit

### <a name="improvements-to-cmpivot"></a>Verbesserungen an CMPivot

<!-- 5870934 -->

Das Navigieren zu CMPivot-Entitäten wurde vereinfacht. Sie können jetzt CMPivot-Entitäten suchen. Außerdem wurden neue Symbole hinzugefügt, um die Entitäten und Entitätsobjekttypen leicht unterscheiden zu können.

Weitere Informationen finden Sie unter [CMPivot](../../servers/manage/cmpivot.md#bkmk_2002).

## <a name="content-management"></a><a name="bkmk_content"></a> Content Management

### <a name="exclude-certain-subnets-for-peer-content-download"></a>Ausschließen bestimmter Subnetze für den Peerinhaltsdownload

<!-- 3555777 -->

Begrenzungsgruppen enthalten für Peerdownloads die folgende Option: **During peer downloads, only use peers within the same subnet** (Bei Peerdownloads nur Peers in demselben Subnetz verwenden): Wenn Sie diese Option aktivieren, enthält die Inhaltsspeicherortliste des Verwaltungspunkts nur Peerquellen, die sich im gleichen Subnetz und der gleichen Begrenzungsgruppe befinden wie der Client. Abhängig von der Konfiguration des Netzwerks können Sie jetzt bestimmte Subnetze für den Abgleich ausschließen. Sie können also beispielsweise eine Grenze einschließen und ein bestimmtes VPN-Subnetz ausschließen.

Weitere Informationen finden Sie unter [Begrenzungsgruppenoptionen für Peerdownloads](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).

### <a name="proxy-support-for-microsoft-connected-cache"></a>Proxyunterstützung für Microsoft Connected Cache

<!-- 5856396 -->

Wenn in Ihrer Umgebung ein nicht authentifizierter Proxyserver für den Internetzugriff verwendet wird, kann dieser nun über den Proxy kommunizieren, wenn Sie einen Configuration Manager-Verteilungspunkt für Microsoft Connected Cache aktivieren. Weitere Informationen finden Sie unter [Microsoft Connected Cache](../hierarchy/microsoft-connected-cache.md).

## <a name="client-management"></a><a name="bkmk_client"></a> Clientverwaltung

### <a name="client-log-collection"></a>Clientprotokollsammlung

<!-- 4226618 -->

Sie können jetzt das Hochladen der Clientprotokolle eines Clientgeräts auf den Standortserver auslösen, indem Sie eine Clientbenachrichtigungsaktion über die Configuration Manager-Konsole senden.

Weitere Informationen finden Sie unter [Clientbenachrichtigung](../../clients/manage/client-notification.md#client-diagnostics).

### <a name="wake-up-a-device-from-the-central-administration-site"></a>Reaktivieren eines Geräts über den Standort der zentralen Verwaltung

<!-- 6030715 -->

Über den Standort der zentralen Verwaltung (CAS) können Sie jetzt im Knoten „Geräte“ oder „Gerätesammlungen“ die Clientbenachrichtigungsaktion verwenden, um Geräte zu „reaktivieren“. Diese Aktion war zuvor nur an einem primären Standort verfügbar.

Weitere Informationen finden Sie unter [Konfigurieren von Wake-On-LAN](../../clients/deploy/configure-wake-on-lan.md#bkmk_wol-1810).

### <a name="improvements-to-support-for-arm64-devices"></a>Verbesserungen bei der Unterstützung von ARM64-Geräten

<!--5954175-->

Die Plattformversion **Alle Windows 10 (ARM64)** ist in der Liste unterstützter Betriebssystemversionen für Objekte mit Anforderungsregeln oder Anwendbarkeitslisten verfügbar.

> [!NOTE]
> Bisher wurde diese Aktion bei Auswahl der obersten **Windows 10**-Plattformebene automatisch sowohl für **Alle Windows 10 (64-Bit)** als auch für **Alle Windows 10 (32-Bit)** ausgewählt. Diese neue Plattform wird nicht automatisch ausgewählt. Wenn Sie **Alle Windows 10 (ARM64)** hinzufügen möchten, wählen Sie die Plattform manuell in der Liste aus.

Weitere Informationen zur Unterstützung von ARM64-Geräten in Configuration Manager finden Sie im Abschnitt [Windows 10 auf ARM64](../configs/support-for-windows-10.md#bkmk_arm64).

### <a name="track-configuration-item-remediations"></a>Nachverfolgen von Konfigurationselementwartungen
<!--4261411-->
Sie können nun den **Wartungsverlauf nachverfolgen**, wenn diese Option für die Complianceregeln für das Konfigurationselement unterstützt wird. Wenn diese Option aktiviert ist, wird bei jeder Wartung, die auf dem Client für das Konfigurationselement vorgenommen wird, eine Zustandsmeldung generiert. Der Verlauf wird in der Configuration Manager-Datenbank gespeichert.

Weitere Informationen zu dieser Einstellung finden Sie unter [Erstellen benutzerdefinierter Konfigurationselemente für Windows-Desktop- und Servercomputer, die mit dem Configuration Manager-Client verwaltet werden](../../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md#bkmk_track).

<!-- ## <a name="bkmk_comgmt"></a> Co-management -->

## <a name="application-management"></a><a name="bkmk_app"></a> Anwendungsverwaltung

### <a name="microsoft-edge-management-dashboard"></a>Microsoft Edge-Verwaltungsdashboard

<!-- 3871913 -->

Das Microsoft Edge-Verwaltungsdashboard bietet Einblicke in die Nutzung von Microsoft Edge und anderen Browsern. Das Dashboard ermöglicht Ihnen Folgendes:

- Sehen, auf wie vielen Ihrer Geräte Microsoft Edge installiert wurde
- Sehen, auf wie vielen Clients verschiedene Versionen von Microsoft Edge installiert sind
- Anzeigen der installierten Browser auf Geräten
- Anzeigen des bevorzugten Browsers nach Gerät

Klicken Sie im Arbeitsbereich „Softwarebibliothek“ auf „Microsoft Edge-Verwaltung“, um das Dashboard aufzurufen. Ändern Sie die Sammlung für die Graphdaten, indem Sie auf „Durchsuchen“ klicken und eine andere Sammlung auswählen. Ihre fünf größten Sammlungen werden automatisch in der Dropdownliste angezeigt. Wenn Sie eine Sammlung auswählen, die nicht in der Liste enthalten ist, wird die neu ausgewählte Sammlung unten in der Dropdownliste angezeigt.

Weitere Informationen finden Sie unter [Microsoft Edge-Verwaltung](../../../apps/deploy-use/deploy-edge.md#bkmk_edge-dash).

### <a name="improvements-to-microsoft-edge-management"></a>Verbesserungen an der Microsoft Edge-Verwaltung

<!-- 4561024 -->

Sie können jetzt eine Microsoft Edge-Anwendung erstellen, die für den Empfang von automatischen Updates eingerichtet ist, anstatt automatische Updates zu deaktivieren. Mit dieser Änderung können Sie Updates für Microsoft Edge mit Configuration Manager verwalten oder automatische Updates durch Microsoft Edge zulassen. Wenn Sie die Anwendung erstellen, klicken Sie auf der Seite „Microsoft Edge-Einstellungen“ auf die Option „Allow Microsoft Edge to automatically update the version of the client on the end user‘s device“ (Microsoft Edge das automatische Aktualisieren der Clientversion auf dem Gerät des Endbenutzers erlauben).

Weitere Informationen finden Sie unter [Microsoft Edge-Verwaltung](../../../apps/deploy-use/deploy-edge.md#bkmk_autoupdate).

### <a name="task-sequence-as-an-app-model-deployment-type"></a>Tasksequenz als App-Modellimplementierungstyp

<!-- 3555953 -->

Sie können nun über das Anwendungsmodell komplexe Anwendungen mithilfe von Tasksequenzen installieren. Fügen Sie einer App einen Bereitstellungstyp hinzu, der eine Tasksequenz ist, um die App entweder zu installieren oder zu deinstallieren. Dieses Feature ermöglicht Folgendes:

- Anzeigen der App-Tasksequenz mit einem Symbol im Softwarecenter. Anhand eines Symbols können Benutzer die App-Tasksequenz leichter finden und bestimmen.

- Definieren zusätzlicher Metadaten für die App-Tasksequenz, einschließlich lokalisierter Informationen.

Weitere Informationen finden Sie unter [Erstellen von Windows-Anwendungen](../../../apps/get-started/creating-windows-applications.md#bkmk_tsdt).

## <a name="os-deployment"></a><a name="bkmk_osd"></a> Bereitstellung des Betriebssystems

### <a name="bootstrap-a-task-sequence-immediately-after-client-registration"></a>Ausführen von Bootstrap für eine Tasksequenz direkt nach der Clientregistrierung

<!-- 5526972 -->

Wenn Sie einen neuen Konfigurations-Manager-Client installieren und registrieren und auch eine Tasksequenz darauf bereitstellen, ist es schwierig, zu bestimmen, wie bald nach der Registrierung die Tasksequenz ausgeführt wird. In dieser Version wird eine neue Clienteigenschafteneinstellung eingeführt, mit der Sie eine Tasksequenz auf einem Client starten können, sobald dieser erfolgreich beim Standort registriert ist.

Weitere Informationen finden Sie unter [Informationen zu Parametern und Eigenschaften für die Clientinstallation in Configuration Manager – PROVISIONTS](../../clients/deploy/about-client-installation-properties.md#provisionts).

### <a name="improvements-to-check-readiness-task-sequence-step"></a>Verbesserungen am Tasksequenzschritt „Bereitschaft überprüfen“

<!-- 6005561 -->

Sie können nun im Tasksequenzschritt **Bereitschaft überprüfen** mehr Geräteeigenschaften überprüfen. Verwenden Sie diesen Schritt in einer Tasksequenz, um zu überprüfen, ob der Zielcomputer die Voraussetzungen erfüllt.

- Architektur des aktuellen Betriebssystems
- Minimale Version des Betriebssystems
- Maximale Version des Betriebssystems
- Mindestversion des Clients
- Sprache des aktuellen Betriebssystems
- Netzteil angeschlossen
- Netzwerkadapter ist verbunden und nicht drahtlos

Weitere Informationen finden Sie unter [Tasksequenzschritte – Bereitschaft überprüfen](../../../osd/understand/task-sequence-steps.md#BKMK_CheckReadiness).

### <a name="improvements-to-task-sequence-progress"></a>Verbesserungen am Tasksequenzstatus

<!-- 5932692 -->

Das Fenster für den Tasksequenzstatus wurde folgendermaßen verbessert:

- Aktivieren des Fensters, um die aktuelle Schrittnummer, die Gesamtzahl der Schritte und den Fortschritt in Prozent anzuzeigen
- Vergrößern der Breite des Fensters, um mehr Platz zu schaffen, damit der Name der Organisation in einer einzelnen Zeile besser angezeigt werden kann

Weitere Informationen finden Sie unter [Benutzerfunktionen für die Betriebssystembereitstellung](../../../osd/understand/user-experience.md#task-sequence-progress).

### <a name="improvements-to-os-deployment"></a>Verbesserungen bei der Bereitstellung von Betriebssystemen

Dieses Release umfasst die folgenden Verbesserungen für die Betriebssystembereitstellung:

- Die Tasksequenzumgebung enthält die neue schreibgeschützte Variable `_TSSecureBoot`.<!--5842295--> Verwenden Sie diese Variable, um den Status des sicheren Starts auf einem UEFI-fähigen Gerät zu bestimmen. Weitere Informationen finden Sie unter [Tasksequenzvariablen – _TSSecureBoot](../../../osd/understand/task-sequence-variables.md#TSSecureBoot).

- Legen Sie Tasksequenzvariablen fest, um den Benutzerkontext für die Schritte **Befehlszeile ausführen** und **PowerShell-Skript ausführen** zu konfigurieren.<!-- 5573175 --> Weitere Informationen finden Sie unter [SMSTSRunCommandLineAsUser](../../../osd/understand/task-sequence-variables.md#SMSTSRunCommandLineAsUser) und [SMSTSRunPowerShellAsUser](../../../osd/understand/task-sequence-variables.md#SMSTSRunPowerShellAsUser).

- Im Schritt **PowerShell-Skript ausführen** können Sie nun die Eigenschaft **Parameter** auf eine Variable festlegen.<!-- 5690481 --> Weitere Informationen finden Sie unter [PowerShell-Skript ausführen](../../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript).

- Der Configuration Manager-PXE-Antwortdienst sendet jetzt Statusmeldungen an den Standortserver. Diese Änderung erleichtert die Problembehandlung für Betriebssystembereitstellungen, die diesen Dienst verwenden.<!-- 5568051 -->

<!-- ## <a name="bkmk_userxp"></a> Software Center -->

## <a name="software-updates"></a><a name="bkmk_sum"></a> Softwareupdates

### <a name="orchestration-groups"></a>Orchestrierungsgruppen

<!-- 3098816 -->

Erstellen Sie eine Orchestrierungsgruppe, um die Bereitstellung von Softwareupdates auf Geräten besser steuern zu können. Viele Serveradministratoren müssen Updates für bestimmte Workloads sehr sorgfältig verwalten und das Verhalten zwischen diesen Updates automatisieren.

Eine Orchestrierungsgruppe bietet Ihnen Flexibilität, sodass Sie Geräte basierend auf einem Prozentsatz, einer bestimmten Anzahl oder einer expliziten Reihenfolge aktualisieren können. Sie können auch ein PowerShell-Skript ausführen, bevor und nachdem die Geräte die Updatebereitstellung ausführen.

Nicht nur Server, sondern auch alle Configuration Manager-Clients können Mitglied einer Orchestrierungsgruppe sein. Die Regeln der Orchestrierungsgruppe gelten für Geräte für alle Bereitstellungen von Softwareupdates in allen Sammlungen, die ein Mitglied dieser Orchestrierungsgruppe enthalten. Andere Verhaltensweisen für Bereitstellungen gelten weiterhin. Beispiel: Wartungsfenster und Bereitstellungszeitpläne.

Weitere Informationen finden Sie unter [Orchestrierungsgruppen](../../../sum/deploy-use/orchestration-groups.md).

### <a name="evaluate-software-updates-after-a-servicing-stack-update"></a>Auswerten von Softwareupdates nach einem Wartungsstapelupdate

<!-- 4639943 -->

Configuration Manager erkennt jetzt, ob ein Wartungsstapelupdate (Servicing Stack Update, SSU) Teil einer Installation für mehrere Updates ist. Wenn ein SSU erkannt wird, wird es zuerst installiert. Nach der Installation des SSU wird ein Auswertungszyklus für Softwareupdates ausgeführt, um die verbleibenden Updates zu installieren. Mit dieser Änderung kann nach dem Wartungsstapelupdate ein abhängiges kumulatives Update installiert werden. Das Gerät muss zwischen den Installationen nicht neu gestartet werden, und Sie müssen kein zusätzliches Wartungsfenster erstellen. SSUs werden nur bei nicht vom Benutzer initiierten Installationen zuerst installiert. Wenn ein Benutzer beispielsweise eine Installation von mehreren Updates aus dem Software Center initiiert, wird das SSU möglicherweise nicht zuerst installiert.

Weitere Informationen finden Sie unter [Planen von Softwareupdates](../../../sum/plan-design/plan-for-software-updates.md#bkmk_ssu).

### <a name="office-365-updates-for-disconnected-software-update-points"></a>Office 365-Updates für nicht verbundene Softwareupdatepunkte

<!-- 4065163 -->

Sie können ein neues Tool verwenden, um Office 365-Updates von einem mit dem Internet verbundenen WSUS-Server in eine nicht verbundene Configuration Manager-Umgebung zu importieren. Bisher konnten Sie beim Exportieren und Importieren von Metadaten für Softwareupdates in nicht verbundenen Umgebungen keine Office 365-Updates bereitstellen. Für Office 365-Updates sind zusätzliche Metadaten erforderlich, die über eine Office-API vom Office-CDN heruntergeladen werden, was in nicht verbundenen Umgebungen nicht möglich ist.

Weitere Informationen finden Sie unter [Synchronisieren von Office 365-Updates bei einem getrennten Softwareupdatepunkt](../../../sum/get-started/synchronize-office-updates-disconnected.md).

<!-- ## <a name="bkmk_o365"></a> Office management -->

## <a name="protection"></a><a name="bkmk_protect"></a> Schutz

### <a name="expand-microsoft-defender-advanced-threat-protection-atp-onboarding"></a>Erweitern des Onboardings von Microsoft Defender Advanced Threat Protection (ATP)

<!-- 5229962 -->
Configuration Manager hat die Unterstützung für das Onboarding von Geräten in Microsoft Defender ATP erweitert. Weitere Informationen finden Sie unter [Microsoft Defender Advanced Threat Protection](../../../protect/deploy-use/windows-defender-advanced-threat-protection.md#onboard-devices).

## <a name="onboard-configuration-manager-clients-to-microsoft-defender-atp-via-the-microsoft-endpoint-manager-admin-center"></a><a name="bkmk_atp"></a> Durchführen des Onboardings für Konfigurations-Manager-Clients in Microsoft Defender ATP über das Microsoft Endpoint Manager Admin Center
<!--5691658-->
Sie können nun die Onboardingrichtlinien von Microsoft Defender ATP-Endpunkterkennung und -reaktion für verwaltete Konfigurations-Manager-Clients bereitstellen. Diese Clients benötigen keine Azure AD- oder MDM-Registrierung, und die Richtlinie ist auf ConfigMgr-Sammlungen anstatt auf Azure AD-Gruppen ausgerichtet.

Diese Funktion ermöglicht Kunden, sowohl Intune MDM als auch das EDR/ATP-Onboarding des Konfigurations-Manager-Clients über eine einzelne Verwaltungsbenutzeroberfläche zu verwalten: das Microsoft Endpoint Manager Admin Center. Weitere Informationen finden Sie unter [Endpunkterkennung und Antwortrichtlinie für Endpunktsicherheit in Intune](../../../../intune/protect/endpoint-security-edr-policy.md).

> [!Important]
> Sie benötigen für dieses Feature das in Ihrer Umgebung installierte Hotfixrollup [KB4563473](https://support.microsoft.com/help/4563473).

### <a name="improvements-to-bitlocker-management"></a>Verbesserungen der BitLocker-Verwaltung

- Die BitLocker-Verwaltungsrichtlinie enthält jetzt zusätzliche Einstellungen wie z. B. Richtlinien für Festplattenlaufwerke und Wechseldatenträger.<!-- 5925683 --> Weitere Informationen finden Sie unter [BitLocker-Einstellungsreferenz](../../../protect/tech-ref/bitlocker/settings.md).

- In der Current Branch-Version 1910 von Configuration Manager war zum Integrieren des BitLocker-Wiederherstellungsdiensts ein HTTPS-fähiger Verwaltungspunkt erforderlich. Die HTTPS-Verbindung ist erforderlich, um die Wiederherstellungsschlüssel im Netzwerk zwischen dem Configuration Manager-Client und dem Verwaltungspunkt zu verschlüsseln. Das Konfigurieren des Verwaltungspunkts und sämtlicher Clients für HTTPS stellt für viele Kunden eine Herausforderung dar.

    Ab dieser Version gilt die HTTPS-Anforderung für die IIS-Website, auf der der Wiederherstellungsdienst gehostet wird, und nicht für die gesamte Rolle „Verwaltungspunkt“. Durch diese Änderungen werden die Wiederherstellungsschlüssel trotz weniger strenger Zertifikatanforderungen bei der Übertragung weiterhin verschlüsselt.<!-- 5925660 --> Weitere Informationen finden Sie unter [Verschlüsseln von Wiederherstellungsdaten](../../../protect/deploy-use/bitlocker/encrypt-recovery-data.md).

## <a name="reporting"></a><a name="bkmk_report"></a> Berichterstellung

### <a name="integrate-with-power-bi-report-server"></a>Integrieren mit dem Power BI-Berichtsserver

<!-- 3721603 -->

Sie können den Power BI-Berichtsserver jetzt in die Configuration Manager-Berichterstellung integrieren. So lässt sich die Visualisierung modernisieren und die Leistung verbessern. Durch die Integration werden Power BI-Berichte in der Konsole unterstützt. Dieses Feature ähnelt dem bereits für SQL Server Reporting Services verfügbaren Angebot.

Weitere Informationen hierzu finden Sie unter [Integration mit dem Power BI-Berichtsserver](../../servers/manage/powerbi-report-server.md).

## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Configuration Manager-Konsole

### <a name="show-boundary-groups-for-devices"></a>Anzeigen von Begrenzungsgruppen für Geräte

<!--6521835-->

Sie können nun die Begrenzungsgruppen für bestimmte Geräte anzeigen, um Ihnen die Problembehandlung für Geräteverhalten mit Begrenzungsgruppen zu erleichtern. Fügen Sie der Listenansicht im Knoten **Geräte** oder wenn Sie die Mitglieder einer **Gerätesammlung** anzeigen die neue Spalte **Begrenzungsgruppen** hinzu.

Weitere Informationen finden Sie unter [Begrenzungsgruppen](../../servers/deploy/configure/boundary-groups.md#bkmk_show-boundary).

### <a name="send-a-smile-improvements"></a>Verbesserungen beim Senden von Lächeln

<!-- 5891852 -->

Beim Übermitteln von Feedback wird für die Optionen „Lächeln senden“ oder „Stirnrunzeln senden“ eine Statusmeldung erstellt. Diese Verbesserung bietet einen Datensatz zu folgenden Punkten:

- Informationen zum Zeitpunkt der Übermittlung
- Absender des Feedbacks
- Feedback-ID
- Informationen zur erfolgreichen oder nicht erfolgreichen Übermittlung des Feedbacks

Bei der Statusmeldung mit der ID 53900 handelt es sich um eine erfolgreiche Übermittlung und bei ID 53901 um eine fehlgeschlagene Übermittlung.

Weitere Informationen finden Sie unter [Produktfeedback](../../understand/find-help.md#BKMK_1806Feedback).

### <a name="search-all-subfolders-for-configuration-items-and-configuration-baselines"></a>Durchsuchen aller Unterordner nach Konfigurationselementen und Konfigurationsbaselines

<!--5891241-->

Ähnlich wie bei Verbesserungen in vorherigen Releases, können Sie jetzt die Suchoption **Alle Unterordner** aus den Knoten **Konfigurationselemente** und **Konfigurationsbaselines** verwenden.

## <a name="tools"></a><a name="bkmk_tools"></a> Tools

### <a name="onetrace-log-groups"></a>OneTrace-Protokollgruppen

<!-- 5559993 -->

OneTrace unterstützt jetzt ähnlich wie das Feature im Supportcenter anpassbare Protokollgruppen. Mit Protokollgruppen können Sie alle Protokolldateien für ein einzelnes Szenario öffnen. OneTrace umfasst derzeit Gruppen für die folgenden Szenarios:

- Anwendungsverwaltung
- Kompatibilitätseinstellungen (auch als „Verwaltung gewünschter Konfigurationen“ bezeichnet)
- Softwareupdates

Weitere Informationen finden Sie unter [Supportcenter – OneTrace](../../support/support-center-onetrace.md).

### <a name="improvements-to-extend-and-migrate-on-premises-site-to-microsoft-azure"></a><a name="bkmk_extend"></a> Verbesserungen in Bezug auf das Erweitern und Migrieren eines lokalen Standorts zu Microsoft Azure
<!--5665775, 6307931-->
Das Tool zum Erweitern und Migrieren eines lokalen Standorts zu Microsoft Azure unterstützt jetzt die Bereitstellung mehrerer Standortsystemrollen auf einer einzigen Azure-VM. Sie können Standortsystemrollen nach Abschluss der ersten Bereitstellung der Azure-VM hinzufügen.

Weitere Informationen finden Sie unter [Erweitern und Migrieren eines lokalen Standorts zu Microsoft Azure](../../support/azure-migration-tool.md#bkmk_add_role).

## <a name="other-updates"></a>Weitere Updates

Ab dieser Version sind die folgenden Features keine [Vorabfeatures](../../servers/manage/pre-release-features.md) mehr:

- [Azure Active Directory-Benutzergruppenermittlung](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco)<!--3611956-->
- [Synchronisieren der Sammlungsmitgliedschaftsergebnisse mit Azure Active Directory](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync)<!--3607475-->
- [Eigenständige Verwendung von CMPivot](../../servers/manage/cmpivot.md#bkmk_standalone)<!--3555890/4692885-->
- [Client-Apps für gemeinsam verwaltete Geräte](../../../comanage/workloads.md#client-apps) (zuvor bekannt als *Mobile Apps für gemeinsam verwaltete Geräte*)<!-- 1357892/3600959 -->

Weitere Informationen zu Änderungen der Windows PowerShell-Cmdlets für Configuration Manager finden Sie in den [Versionshinweisen zu PowerShell Version 2002](https://docs.microsoft.com/powershell/sccm/2002-release-notes?view=sccm-ps).

Weitere Informationen zu Änderungen an der Verwaltungsdienst-Rest-API finden Sie in den[Versionshinweisen zum Verwaltungsdienst](../../../develop/adminservice/release-notes.md#bkmk_2002).

Neben neuen Features umfasst dieses Release auch weitere Änderungen, beispielsweise Fehlerbehebungen. Weitere Informationen finden Sie unter [Zusammenfassung der Änderungen im Current Branch von Configuration Manager, Version 2002](https://support.microsoft.com/help/4556203).

<!--
The following update rollup (4517869) is available in the console starting on October 1, 2019: [Update rollup for Configuration Manager current branch, version 1906](https://support.microsoft.com/help/4517869).

-->

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!NOTE]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->

## <a name="next-steps"></a>Nächste Schritte

<!-- At this time, version 2002 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2002.md#early-update-ring). -->

Ab dem 11. Mai 2020 ist Version 2002 global für alle Kunden zur Installation verfügbar.

Wenn Sie zum Installieren dieser Version bereit sind, finden Sie dazu weitere Informationen unter [Updates und Wartung für Configuration Manager](../../servers/manage/updates.md) und [Checkliste für die Installation von Update 2002](../../servers/manage/checklist-for-installing-update-2002.md).

> [!TIP]
> Verwenden Sie eine Baselineversion von Configuration Manager, um einen neuen Standort zu installieren.
>
> Weitere Informationen:
>
> - [Installieren von neuen Standorten](../../servers/deploy/install/installing-sites.md)
> - [Baseline- und Updateversionen](../../servers/manage/updates.md#bkmk_Baselines)

Informationen zu bekannten, erheblichen Problemen finden Sie in den [Versionshinweisen](../../servers/deploy/install/release-notes.md).

Nachdem Sie einen Standort aktualisiert haben, überprüfen Sie auch die [Checkliste für Aufgaben nach dem Update](../../servers/manage/checklist-for-installing-update-2002.md#post-update-checklist).
