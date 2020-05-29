---
title: Neuerungen in Version 1906
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über Änderungen und neue Funktionen, die in Version 1906 des Current Branchs von Configuration Manager eingeführt wurden.
ms.date: 10/01/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 97e23075-549c-4e45-ab1e-0671027edacf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2db1a719aaf1cb79973f1af8e2de3c1bbb91d605
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83879088"
---
# <a name="whats-new-in-version-1906-of-configuration-manager-current-branch"></a>Neuerungen in Version 1906 von Configuration Manager (Current Branch)

*Gilt für: Configuration Manager (Current Branch)*

Das Update 1906 für den Current Branch von Configuration Manager ist als konsoleninternes Update verfügbar. Wenden Sie dieses Update auf Standorte an, an denen Version 1802 oder höher ausgeführt wird. <!-- baseline only statement:When installing a new site, it's also available as a baseline version.--> In diesem Artikel werden die Änderungen und neuen Features in Configuration Manager, Version 1906 zusammengefasst.  

Überprüfen Sie stets die neueste Checkliste für die Installation dieses Updates. Weitere Informationen finden Sie in der [Checkliste für die Installation von Update 1906](../../servers/manage/checklist-for-installing-update-1906.md). Nachdem Sie einen Standort aktualisiert haben, überprüfen Sie auch die [Checkliste für Aufgaben nach dem Update](../../servers/manage/checklist-for-installing-update-1906.md#post-update-checklist).

Wenn Sie die neuen Configuration Manager-Features nach der Aktualisierung des Standorts vollständig nutzen möchten, müssen Sie auch Clients auf die neueste Version aktualisieren. Beim Update des Standorts und der Konsole werden neue Features in der Configuration Manager-Konsole angezeigt. Das vollständige Szenario ist allerdings erst einsatzbereit, wenn auch die Clientversion aktualisiert wird.

> [!Tip]  
> Um bei einer Aktualisierung dieser Seite benachrichtigt zu werden, kopieren Sie die folgende URL, und fügen Sie sie in Ihren RSS-Feedreader ein: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1906+-+Configuration+Manager%22&locale=en-us`


## <a name="requirement-changes"></a>Geänderte Anforderungen

### <a name="version-1906-client-requires-sha-2-code-signing-support"></a>Für Client Version 1906 ist die Unterstützung von SHA-2-Codesignieren erforderlich.

<!--SCCMDocs-pr#3404-->
Aufgrund von Schwächen des SHA-1-Algorithmus und um Branchenstandards zu erfüllen, signiert Microsoft nun Configuration Manager-Binärdateien mit dem SHA-2-Algorithmus, der größere Sicherheit bietet. Die folgenden Windows-Betriebssystemversionen erfordern ein Update, damit SHA-2-Codesignieren unterstützt wird:

- Windows 7 SP1
- Windows Server 2008 R2 SP1
- Windows Server 2008 SP2

Weitere Informationen finden Sie unter [Voraussetzungen für Windows-Clients](../../clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md#bkmk_sha2).


## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> Standortinfrastruktur

### <a name="site-server-maintenance-task-improvements"></a>Verbesserungen von Wartungstasks für Standortserver

<!--3555894-->
Wartungsaufgaben für Standortserver können jetzt auf ihrer eigenen Registerkarte in der Detailansicht eines Standortservers angezeigt und bearbeitet werden. Die neue Registerkarte **Wartungstasks** bietet Ihnen Informationen wie z.B.:

- Ob der Task aktiviert ist
- Der Taskzeitplan
- Letzte Startzeit
- Letzte Abschlusszeit
- Ob der Task erfolgreich abgeschlossen wurde

![Neue Registerkarte für Wartungstasks in der Detailansicht eines Standortservers](./media/3555894-maintenance-tasks.png)

Weitere Informationen finden Sie unter [Wartungstasks](../../servers/manage/maintenance-tasks.md#bkmk_MTs1906).

### <a name="configuration-manager-update-database-upgrade-monitoring"></a>Configuration Manager-Updatedatenbank: Überwachen der Aktualisierung

<!--4200581-->
Bei Anwendung eines Configuration Manager-Updates können Sie jetzt den Status des Tasks **Upgrade für ConfigMgr-Datenbank ausführen** im Installationsstatusfenster sehen.

- Wenn das Datenbankupgrade blockiert ist, erhalten Sie die Warnmeldung **Wird ausgeführt, Eingreifen erforderlich**.
   - In „cmupdate.log“ werden der Name des Programms und die sessionID aus SQL, die das Upgrade der Datenbank blockiert, protokolliert.
- Wenn das Upgrade der Datenbank nicht mehr blockiert wird, wird der Status auf **Wird ausgeführt** oder **Abgeschlossen** zurückgesetzt.
   - Wenn das Upgrade der Datenbank blockiert wird, erfolgt alle 5 Minuten eine Prüfung, um festzustellen, ob es weiterhin blockiert wird.

   ![Überwachen des Upgrades der Datenbank während der Installation](./media/4200581-database-upgrade-monitoring.png)

Weitere Informationen finden Sie unter [Installieren konsoleninterner Updates](../../servers/manage/install-in-console-updates.md#3-monitor-the-progress-of-updates-as-they-install).

### <a name="management-insights-rule-for-ntlm-fallback"></a>Regel für Verwaltungseinblicke für NTLM-Fallback

<!--4572953-->
Verwaltungseinblicke enthält eine neue Regel, die erkennt, ob Sie die weniger sichere NTLM-Authentifizierungs-Fallbackmethode für den Standort aktiviert haben: **NTLM-Fallback ist aktiviert**.

Weitere Informationen finden Sie unter [Einblicke für die Verwaltung](../../servers/manage/management-insights.md#security).

### <a name="improvements-to-support-for-sql-always-on"></a>Verbesserungen für die Unterstützung von SQL Always On

- Hinzufügen eines neuen synchronen Replikats aus dem Setup<!--3127336-->: Sie können nun einer vorhandenen SQL AlwaysOn-Verfügbarkeitsgruppe einen neuen sekundären Replikatknoten hinzufügen. Verwenden Sie anstelle eines manuellen Prozesses das Configuration Manager-Setup, um diese Änderung vorzunehmen. Weitere Informationen finden Sie unter [Konfigurieren von SQL Server AlwaysOn-Verfügbarkeitsgruppen](../../servers/deploy/configure/configure-aoag.md#bkmk_sync).

- Multisubnetz-Failover<!-- SCCMDocs-pr#3734 -->: Sie können nun das [Schlüsselwort der MultiSubnetFailover-Verbindungszeichenfolge](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover) in SQL Server aktivieren. Außerdem müssen Sie den Standortserver manuell konfigurieren. Weitere Informationen finden Sie unter der [MultiSubnetFailover](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#multi-subnet-failover)-Voraussetzung.

- Unterstützung für verteilte Ansichten<!-- SCCMDocs-pr#3792 -->: Die Standortdatenbank kann in einer SQL Server AlwaysOn-Verfügbarkeitsgruppe gehostet werden, und Sie können Datenbankreplikationslinks für die Verwendung von [verteilten Ansichten](../hierarchy/data-transfers-between-sites.md#bkmk_dbrep) aktivieren.

    > [!Note]  
    > Diese Änderung gilt nicht für SQL Server-Cluster.

- Site Recovery kann die Datenbank in einer SQL AlwaysOn-Gruppe neu erstellen. Dieser Prozess funktioniert sowohl mit manuellem als auch mit automatischem Seeding.<!-- SCCMDocs-pr#3846 -->

- Neue Setup-Voraussetzungsprüfungen:<!-- SCCMDocs-pr#3899 -->  

    - SQL-Verfügbarkeitsgruppenreplikate müssen alle denselben Seedingmodus aufweisen.
    - SQL-Verfügbarkeitsgruppenreplikate müssen fehlerfrei sein.

## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a> Cloudgestützte Verwaltung

### <a name="azure-active-directory-user-group-discovery"></a>Azure Active Directory-Benutzergruppenermittlung

<!--3611956-->

Sie können jetzt Benutzergruppen und Mitglieder dieser Gruppen aus Azure Active Directory (Azure AD) ermitteln. Vom Standort zuvor nicht ermittelte, in Azure AD-Gruppen gefundene Benutzer werden als Benutzerressourcen in Configuration Manager hinzugefügt. Ein Benutzergruppen-Datensatz wird erstellt, wenn die Gruppe eine Sicherheitsgruppe ist. Bei diesem Feature handelt es sich um [Vorabfeature](../../servers/manage/pre-release-features.md), das aktiviert werden muss.

Weitere Informationen finden Sie unter [Configure discovery methods](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco) (Konfigurieren von Ermittlungsmethoden).

### <a name="synchronize-collection-membership-results-to-azure-active-directory-groups"></a>Synchronisieren der Sammlungsmitgliedschaftsergebnisse mit Azure Active Directory-Gruppen

<!--3607475-->

Sie können nun die Synchronisierung von Sammlungsmitgliedschaften mit einer Azure Active Directory-Gruppe (Azure AD) aktivieren. Diese Synchronisierung ist eine Featurevorabversion. Wie Sie es aktivieren, erfahren Sie unter [Pre-release features (Features von Vorabreleases)](../../servers/manage/pre-release-features.md).

Durch die Synchronisierung können Sie Ihre vorhandenen lokalen Gruppierungsregeln in der Cloud verwenden, indem Sie Azure AD-Gruppenmitgliedschaften auf Grundlage der Erfassungsergebnisse für Mitgliedschaften erstellen. Es werden nur Geräte mit einem Azure Active Directory-Eintrag in der Azure AD-Gruppe widergespiegelt. Sowohl Geräte mit Azure AD Hybrid-Einbindung als auch per Azure Active Directory eingebundene Geräte werden unterstützt.

Weitere Informationen finden Sie unter [Erstellen von Sammlungen](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync).


## <a name="desktop-analytics"></a><a name="bkmk_da"></a> Desktop Analytics

### <a name="readiness-insights-for-desktop-apps"></a>Bereitschaftserkenntnisse für Desktop-Apps

<!-- 4021225 -->

Sie können nun detailliertere Einblicke in Ihre Desktopanwendungen erhalten, u. a. in branchenspezifische Apps. Das frühere App Health Analyzer-Toolkit ist nun in den Configuration Manager-Client integriert. Diese Integration vereinfacht Bereitstellung und Verwaltbarkeit der Bereitschaftserkenntnisse für Apps im Desktop Analytics-Portal.

Weitere Informationen finden Sie unter [Compatibility assessment in Desktop Analytics](../../../desktop-analytics/compat-assessment.md#advanced-insights) (Kompatibilitätsbewertung in Desktop Analytics).


### <a name="dalogscollector-tool"></a>DALogsCollector-Tool

<!--4622989-->
Verwenden Sie das Tool „DesktopAnalyticsLogsCollector.ps1“ aus dem Installationsverzeichnis von Configuration Manager zum Behandeln von Desktop Analytics-Problemen. Es führt einige grundlegende Schritte zur Problembehandlung aus und sammelt die relevanten Protokolle in einem einzelnen Arbeitsverzeichnis.

Weitere Informationen finden Sie unter [Protokollsammler](../../../desktop-analytics/log-collector.md).


## <a name="real-time-management"></a><a name="bkmk_real"></a> Verwaltung in Echtzeit

### <a name="add-joins-additional-operators-and-aggregators-in-cmpivot"></a>Hinzufügen von Verknüpfungen, zusätzlichen Operatoren und Aggregatoren in CMPivot

<!--4054074-->

Für CMPivot verfügen Sie nun über zusätzliche arithmetische Operatoren, Aggregatoren und die Möglichkeit, Abfrageverknüpfungen hinzuzufügen, wie etwa Registrierung und Datei gemeinsam zu verwenden.

Weitere Informationen finden Sie unter [CMPivot](../../servers/manage/cmpivot.md#bkmk_cmpivot1906).

### <a name="cmpivot-standalone"></a>Eigenständige Verwendung von CMPivot

<!--3555890, 4619340, 4692885 -->

Sie können CMPivot jetzt als eigenständige App verwenden. Die eigenständige CMPivot-Version ist ein **Vorabfeature**, das nur in englischer Sprache verfügbar ist. Führen Sie CMPivot außerhalb der Configuration Manager-Konsole aus, um den Echtzeitstatus von Geräten in Ihrer Umgebung anzuzeigen. Diese Änderung ermöglicht Ihnen die Verwendung von CMPivot auf einem Gerät, ohne die Konsole vorher zu installieren.

Sie können die Leistungsfähigkeit von CMPivot mit anderen Personas wie Helpdesk oder Sicherheitsadministratoren teilen, die die Konsole nicht auf ihrem Computer installiert haben. Diese anderen Personas können CMPivot verwenden, um Configuration Manager neben den anderen Tools, die sie traditionell verwenden, abzufragen. Durch die gemeinsame Nutzung dieser umfangreichen Verwaltungsdaten können Sie proaktiv an der Lösung von rollenübergreifenden Geschäftsproblemen arbeiten.

Weitere Informationen finden Sie unter [CMPivot](../../servers/manage/cmpivot.md#bkmk_standalone) und [Features der Vorabversion](../../servers/manage/pre-release-features.md#bkmk_table).

### <a name="added-permissions-to-the-security-administrator-role"></a>Zur Rolle „Sicherheitsadministrator“ hinzugefügte Berechtigungen

<!--4683130-->

Die folgenden Berechtigungen wurden der in Configuration Manager integrierten Rolle [**Sicherheitsadministrator**](../../understand/fundamentals-of-role-based-administration.md#bkmk_Planroles) hinzugefügt:

- Lesen des SMS-Skripts
- Ausführen von CMPivot für eine Sammlung
- Lesen des Inventarberichts

Weitere Informationen finden Sie unter [CMPivot](../../servers/manage/cmpivot.md#bkmk_cmpivot_secadmin1906).


## <a name="content-management"></a><a name="bkmk_content"></a> Content Management

### <a name="delivery-optimization-download-data-in-client-data-sources-dashboard"></a>Übermittlungsoptimierung-Downloaddaten im Dashboard „Clientdatenquellen“

<!--3555759-->
Das Dashboard „Clientdatenquellen“ enthält nun Daten zur [Übermittlungsoptimierung](../hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization). Mithilfe dieses Dashboards können Sie nachvollziehen, von wo Clients Inhalte in Ihrer Umgebung beziehen.

Weitere Informationen finden Sie unter [Dashboard „Clientdatenquellen“](../../servers/deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard).

### <a name="use-your-distribution-point-as-an-in-network-cache-server-for-delivery-optimization"></a>Verteilungspunkt als netzwerkinternen Cacheserver für die Übermittlungsoptimierung verwenden

<!--3555764-->
Sie können jetzt die Übermittlungsoptimierung für den netzwerkinternen Cacheserver auf Ihren Verteilungspunkten installieren. Wenn Sie diese Art von Inhalt lokal zwischenspeichern, können Ihre Clients von dem Feature zur Übermittlungsoptimierung profitieren, und Sie können dabei helfen, WAN-Links zu schützen.

Dieser Cacheserver dient als bedarfsgesteuerter transparenter Cache für Inhalt, der von der Übermittlungsoptimierung heruntergeladen wird. Verwenden Sie Clienteinstellungen, um sicherzustellen, dass dieser Server nur Mitgliedern der lokalen Begrenzungsgruppe für Configuration Manager angeboten wird.

Weitere Informationen finden Sie unter [Übermittlungsoptimierung durch netzwerkinternen Cache in Configuration Manager](../hierarchy/microsoft-connected-cache.md).


## <a name="client-management"></a><a name="bkmk_client"></a> Clientverwaltung

### <a name="support-for-windows-virtual-desktop"></a>Unterstützung für Windows Virtual Desktop

<!--3556025-->
[Windows Virtual Desktop](https://docs.microsoft.com/azure/virtual-desktop/) ist eine Previewfunktion von Microsoft Azure und Microsoft 365. Sie können diese unter Windows ausgeführten virtuellen Geräte jetzt mit Configuration Manager in Azure verwalten.

Ähnlich wie bei einem Terminalserver ermöglichen diese virtuellen Geräte mehrere gleichzeitige aktive Benutzersitzungen. Um bei der Clientleistung zu helfen, deaktiviert Configuration Manager jetzt Benutzerrichtlinien auf jedem Gerät, dass mehrere Benutzersitzungen zulässt. Auch wenn Sie Benutzerrichtlinien aktivieren, deaktiviert der Client sie standardmäßig auf diesen Geräten, zu denen Windows Virtual Desktop- und Terminalserver zählen.

Weitere Informationen finden Sie unter [Unterstützte Betriebssystemversionen für Clients und Geräte](../configs/supported-operating-systems-for-clients-and-devices.md#windows-computers).

### <a name="support-center-onetrace-preview"></a>Supportcenter: OneTrace (Vorschau)

<!--3555962-->
OneTrace ist eine neue Protokollanzeige im Supportcenter. Die Funktionsweise ist CMTrace ähnlich und bietet die folgenden Verbesserungen:

- Ansicht im Registerkartenformat
- Andockbare Fenster
- Verbesserte Suchfunktionen
- Fähigkeit, Filter zu aktivieren, ohne die Protokollansicht zu verlassen
- Hinweise auf der Scrollleiste, um Gruppen von Fehlern schnell zu bestimmen
- Schnelles Öffnen von Protokollen bei großen Dateien

![Screenshot der OneTrace-Protokollanzeige](./media/3555962-onetrace.png)

Weitere Informationen finden Sie unter [Supportcenter – OneTrace](../../support/support-center-onetrace.md).

### <a name="configure-client-cache-minimum-retention-period"></a>Konfigurieren des Mindestaufbewahrungszeitraums im Clientcache

<!--4485509-->
Sie können nun für den Configuration Manager-Client festlegen, wie lange Inhalte mindestens im Cache aufbewahrt werden sollen. Diese Clienteinstellung definiert die minimale Zeitspanne, die der Configuration Manager-Agent warten sollte, bevor er Inhalt aus dem Cache entfernt, wenn mehr Speicherplatz benötigt wird. Konfigurieren Sie in der Gruppe **Einstellungen für Clientcache** in den Clienteinstellungen die folgende Einstellung: **Mindestdauer vor dem Entfernen von Inhalten aus dem Cache (Minuten)** .

> [!Note]  
> In der gleichen Clienteinstellungsgruppe wurde die vorhandene Einstellung **Configuration Manager-Client in vollständigem Betriebssystem zur Freigabe von Inhalten aktivieren**  in **Als Peercachequelle aktivieren** umbenannt. Das Verhalten der Einstellung ändert sich nicht.  

Weitere Informationen finden Sie unter [Einstellungen des Clientcaches](../../clients/deploy/about-client-settings.md#client-cache-settings).


## <a name="co-management"></a><a name="bkmk_comgmt"></a> Die Co-Verwaltung

### <a name="improvements-to-co-management-auto-enrollment"></a>Verbesserungen bei der automatischen Registrierung der Co-Verwaltung

- Ein neues co-verwaltetes Gerät wird jetzt automatisch basierend auf seinem Azure AD-*Gerätetoken* (Azure Active Directory) beim Microsoft Intune-Dienst registriert. Es muss nicht warten, bis ein Benutzer sich bei dem Gerät anmeldet, um die automatische Registrierung zu starten. Mit dieser Änderung kann die Anzahl von Geräten mit dem [Registrierungsstatus](../../../comanage/how-to-monitor.md#co-management-enrollment-status) *Benutzeranmeldung steht aus* reduziert werden.<!-- 4454491 -->

- Für Kunden, die bereits Geräte für die Co-Verwaltung registriert haben, werden neue Geräte nun sofort registriert, sobald sie die Voraussetzungen erfüllen. Dies erfolgt beispielsweise, wenn das Gerät mit Azure AD verknüpft wird und der Configuration Manager-Client installiert ist.<!--4321130-->

Weitere Informationen finden Sie unter [Aktivieren der Co-Verwaltung](../../../comanage/how-to-enable.md).

### <a name="multiple-pilot-groups-for-co-management-workloads"></a>Mehrere Pilotgruppen für Workloads für die Co-Verwaltung

<!--3555750-->
Sie können jetzt verschiedene Pilotsammlungen für die einzelnen Workloads für die Co-Verwaltung konfigurieren. Durch die Verwendung verschiedener Pilotsammlungen können Sie nun Workloads mit einem präziseren Ansatz verschieben.

- Auf der Registerkarte **Aktivierung** können Sie jetzt eine **Automatische Intune-Registrierung**-Sammlung angeben.
    - Die **Automatische Intune-Registrierung**-Sammlung sollte alle Clients enthalten, die Sie in die Co-Verwaltung integrieren möchten. Es ist im Wesentlichen eine Obermenge von allen anderen Stagingsammlungen.

- Auf der **Staging**-Registerkarte können Sie nun eine einzelne Sammlung für jede Workload auswählen, anstatt eine Pilotsammlung für alle Workloads zu verwenden.

    ![Registerkarte „Co-Verwaltungsstaging“ ermöglicht Ihnen die Auswahl einer Sammlung für jede Workload](./media/3555750-co-management-staging-tab.png)

Diese Optionen sind auch verfügbar, wenn Sie das erste Mal die Co-Verwaltung aktivieren.

Weitere Informationen finden Sie unter [Aktivieren der Co-Verwaltung](../../../comanage/how-to-enable.md).

### <a name="co-management-support-for-government-cloud"></a>Unterstützung der Co-Verwaltung für die Government-Cloud

<!--4075452-->
Kunden in US-Regierungsbehörden können nun die Co-Verwaltung mit dem Azure U.S. Government Cloud (portal.azure.us) verwenden. Weitere Informationen finden Sie unter [Aktivieren der Co-Verwaltung](../../../comanage/how-to-enable.md).


## <a name="application-management"></a><a name="bkmk_app"></a> Anwendungsverwaltung

### <a name="filter-applications-deployed-to-devices"></a>Filtern von Anwendungen, die für Geräte bereitgestellt werden

<!--4451056-->
Benutzerkategorien für geräteorientierte Anwendungsbereitstellungen werden jetzt als Filter im Softwarecenter angezeigt. Geben Sie eine **Benutzerkategorie** für eine Anwendung auf der **Softwarecenter**-Seite ihrer Eigenschaften an. Öffnen Sie die App dann im Softwarecenter, und sehen Sie sich die verfügbaren Filter an.

Weitere Informationen finden Sie unter [Manuelles Angeben von Anwendungsinformationen](../../../apps/deploy-use/create-applications.md#bkmk_manual-app).

### <a name="application-groups"></a>Anwendungsgruppen

<!--3555907-->
Erstellen Sie eine Gruppe von Anwendungen, die Sie als einzelne Bereitstellung an eine Benutzer- oder Gerätesammlung senden können. Die Metadaten, die Sie für die App-Gruppe angeben, werden im Softwarecenter als Einheit dargestellt. Sie können die Apps in der Gruppe so anordnen, dass der Client sie in einer bestimmten Reihenfolge installiert.

Bei diesem Feature handelt es sich um ein vorab veröffentlichtes Feature. Wie Sie es aktivieren, erfahren Sie unter [Pre-release features (Features von Vorabreleases)](../../servers/manage/pre-release-features.md).

Weitere Informationen finden Sie unter [Create application groups](../../../apps/deploy-use/create-app-groups.md) (Erstellen von Anwendungsgruppen).

### <a name="retry-the-install-of-pre-approved-applications"></a>Wiederholen der Installation vorab genehmigter Anwendungen

<!--4336307-->
Sie können nun die Installation einer App wiederholen, die Sie zuvor für einen Benutzer oder ein Gerät genehmigt haben. Die Genehmigungsoption gilt nur für verfügbare Bereitstellungen. Wenn der Benutzer die App deinstalliert oder der erste Installationsvorgang fehlschlägt, wird ihr Zustand von Configuration Manager nicht neu bewertet, sondern es erfolgt eine Neuinstallation. Dieses Feature ermöglicht es einem Supporttechniker, die App-Installation für einen Benutzer, der um Hilfe bittet, schnell zu wiederholen.

Weitere Informationen finden Sie im Artikel zum [Genehmigen von Anwendungen](../../../apps/deploy-use/app-approval.md).

### <a name="install-an-application-for-a-device"></a>Installieren von Anwendungen auf einem Gerät

<!--4402180-->
Über die Configuration Manager-Konsole können Sie jetzt Anwendungen auf einem Gerät in Echtzeit installieren. Dieses Feature kann dazu beitragen, den Bedarf an getrennten Sammlungen für jede Anwendung zu reduzieren.

Weitere Informationen finden Sie unter [Installieren von Anwendungen auf einem Gerät](../../../apps/deploy-use/install-app-for-device.md).

### <a name="improvements-to-app-approvals"></a>Verbesserungen bei App-Genehmigungen

<!--4224910-->
Dieses Release bietet für App-Genehmigungen die folgenden Verbesserungen:

- Wenn Sie eine App-Anforderung in der Konsole genehmigen und dann ablehnen, können Sie sie nun erneut genehmigen. Die App wird auf dem Client erneut installiert, nachdem Sie sie genehmigt haben.  

- In der Configuration Manager-Konsole wurde im Arbeitsbereich **Softwarebibliothek** unter **Anwendungsverwaltung** der Knoten **Genehmigungsanforderungen** in **Anwendungsanforderungen** umbenannt.<!-- SCCMDocs-pr#4028 -->

- Es gibt die neue WMI-Methode **DeleteInstance**, um eine Genehmigungsanforderung für eine App zu entfernen. Bei dieser Aktion wird die App nicht vom Gerät deinstalliert. Falls noch nicht installiert, kann der Benutzer die App nicht aus dem Softwarecenter installieren.

- Rufen Sie die API **CreateApprovedRequest** auf, um eine vorab genehmigte Anforderung für eine App auf einem Gerät zu erstellen. Um die automatische Installation der App auf dem Client zu verhindern, legen Sie den Parameter **AutoInstall** auf `FALSE` fest. Dem Benutzer wird die App im Softwarecenter angezeigt, aber sie wird nicht automatisch installiert.

Weitere Informationen finden Sie im Artikel zum [Genehmigen von Anwendungen](../../../apps/deploy-use/app-approval.md).


## <a name="os-deployment"></a><a name="bkmk_osd"></a> Bereitstellung des Betriebssystems

### <a name="task-sequence-debugger"></a>Debugger für Tasksequenzen

<!--3612274-->
Der Debugger für Tasksequenzen ist ein neues Tool für die Problembehandlung. Sie stellen eine Tasksequenz im Debugmodus für eine Sammlung mit einem Gerät bereit. In diesem Modus können Sie die Tasksequenz kontrolliert durchlaufen, um die Problembehandlung und -untersuchung zu erleichtern.

![Screenshot des Tasksequenz-Debuggers](./media/3612274-tsdebug.png)

Bei diesem Feature handelt es sich um ein vorab veröffentlichtes Feature. Wie Sie es aktivieren, erfahren Sie unter [Pre-release features (Features von Vorabreleases)](../../servers/manage/pre-release-features.md).

Weitere Informationen finden Sie unter [Debuggen einer Tasksequenz](../../../osd/deploy-use/debug-task-sequence.md).

### <a name="clear-app-content-from-client-cache-during-task-sequence"></a>Löschen des App-Inhalts aus dem Clientcache während der Tasksequenz

<!--4485675-->
Im Tasksequenzschritt **Anwendung installieren** können Sie jetzt nach der Ausführung des Schritts den App-Inhalt aus dem Clientcache löschen.

Weitere Informationen finden Sie unter [About task sequence steps](../../../osd/understand/task-sequence-steps.md#BKMK_InstallApplication) (Informationen zu Schritten von Tasksequenzen).

> [!Important]  
> Aktualisieren Sie den Zielclient auf die neueste Version, um dieses neue Feature zu unterstützen.

### <a name="reclaim-sedo-lock-for-task-sequences"></a>SEDO-Sperre für Tasksequenzen freigeben

<!--3699337-->
Wenn die Configuration Manager-Konsole nicht mehr reagiert, können Sie möglicherweise keine weiteren Änderungen an einer Tasksequenz vornehmen. Wenn Sie versuchen, auf eine gesperrte Tasksequenz zuzugreifen, können Sie jetzt die Option **Änderungen verwerfen** auswählen und das Objekt weiter bearbeiten.

Weitere Informationen finden Sie unter [Verwenden des Tasksequenz-Editors](../../../osd/understand/task-sequence-editor.md#bkmk_sedo).

### <a name="pre-cache-driver-packages-and-os-images"></a>Zwischenspeichern von Treiberpaketen und Betriebssystemimages

<!--4224642-->
Der Tasksequenz-Zwischenspeicher enthält nun zusätzliche Inhaltstypen. Zwischengespeicherte Inhalte betrafen bislang nur Betriebssystem-Upgradepakete. Nun können Sie mithilfe der Zwischenspeicherung den Bandbreitenbedarf für Folgendes verringern:

- Betriebssystemimages
- Treiberpakete
- Pakete

Weitere Informationen finden Sie unter [Konfigurieren des zwischengespeicherten Inhalts](../../../osd/deploy-use/configure-precache-content.md).

### <a name="improvements-to-os-deployment"></a>Verbesserungen bei der Bereitstellung von Betriebssystemen

Dieses Release umfasst die folgenden Verbesserungen für die Betriebssystembereitstellung:

- Erstellen und bearbeiten Sie mit den folgenden zwei PowerShell-Cmdlets den Schritt [Tasksequenz ausführen](../../../osd/understand/task-sequence-steps.md#child-task-sequence):<!--2839943-->

    - **New-CMTSStepRunTaskSequence**

    - **Set-CMTSStepRunTaskSequence**

- Das Bearbeiten von Variablen beim Ausführen einer Tasksequenz wurde vereinfacht. Nachdem Sie eine Tasksequenz im Tasksequenzerstellungs-Assistenten-Fenster auswählen, enthält die Seite zum Bearbeiten von Tasksequenzvariablen eine **Bearbeiten**-Schaltfläche.<!-- 4668846 --> Weitere Informationen finden Sie unter [Gewusst wie: Verwenden von Tasksequenzvariablen](../../../osd/understand/using-task-sequence-variables.md#bkmk_set-tswiz).

- Der Tasksequenzschritt **BitLocker deaktivieren** hat einen neuen Neustartzähler. Verwenden Sie diese Option, um die Anzahl der Neustarts festzulegen, um BitLocker deaktiviert zu halten. Diese Änderung trägt zur Vereinfachung der Tasksequenz bei. Anstatt mehrere Instanzen eines Schritts hinzuzufügen, können Sie einen einzigen Schritt verwenden. <!--4512937--> Weitere Informationen finden Sie unter [BitLocker deaktivieren](../../../osd/understand/task-sequence-steps.md#BKMK_DisableBitLocker).

- Verwenden Sie die neue Tasksequenzvariable **SMSTSRebootDelayNext** mit der vorhandenen Variablen [SMSTSRebootDelay](../../../osd/understand/task-sequence-variables.md#SMSTSRebootDelay). Wenn bei späteren Neustarts ein anderes Timeout als beim ersten Neustart verwendet werden soll, legen Sie diese neue Variable auf einen anderen Sekundenwert fest. <!--4447680--> Weitere Informationen finden Sie unter [SMSTSRebootDelayNext](../../../osd/understand/task-sequence-variables.md#SMSTSRebootDelayNext).

- Die Tasksequenz legt die neue schreibgeschützte Variable **_SMSTSLastContentDownloadLocation** fest. Diese Variable enthält den letzten Speicherort, von dem die Tasksequenz Inhalte heruntergeladen bzw. versucht hat, Inhalte herunterzuladen. Überprüfen Sie diese Variable, statt die Clientprotokolle zu analysieren.<!-- 2840337 -->

- Beim Erstellen von Tasksequenzmedien fügt Configuration Manager keine autorun.inf-Datei hinzu. Diese Datei wird in der Regel von Antischadsoftwareprodukten blockiert. Wenn Sie die Datei für Ihr Szenario benötigen, können Sie sie aber weiterhin hinzufügen.<!-- 4090666 -->

### <a name="improvements-to-pxe"></a>Verbesserungen bei PXE

Während des PXE DHCP-Handshakes wird jetzt die Option 82 für den PXE-Antwortdienst ohne WDS unterstützt. Die Option 82 wird mit WDS nicht unterstützt.


## <a name="software-center"></a><a name="bkmk_userxp"></a> Softwarecenter

### <a name="improvements-to-software-center-tab-customizations"></a>Verbesserungen von Anpassungen der Registerkarte „Softwarecenter“

<!--4063773-->
Sie können im Softwarecenter nun bis zu fünf benutzerdefinierte Registerkarten hinzufügen. Sie können auch die Reihenfolge ändern, in der diese Registerkarten im Softwarecenter angezeigt werden.

Weitere Informationen finden Sie unter [Softwarecenter-Clienteinstellungen](../../clients/deploy/about-client-settings.md#software-center).

### <a name="software-center-infrastructure-improvements"></a>Verbesserungen an der Infrastruktur des Softwarecenters

<!--3555950-->

Dieses Release enthält die folgenden Verbesserungen für die Infrastruktur des Softwarecenters:

- Das Softwarecenter kommuniziert nun mit einem verfügbaren Verwaltungspunkt für Benutzer-Apps. Der Anwendungskatalog wird nicht mehr verwendet. Dadurch können Sie den Anwendungskatalog leichter aus dem Standort entfernen.

- Zuvor wurde der erste Verwaltungspunkt aus der Liste mit den verfügbaren Servern verwendet. Ab diesem Release wird der gleiche Verwaltungspunkt genutzt, den auch der Client verwendet. Dadurch kann das Softwarecenter den gleichen Verwaltungspunkt des zugewiesenen primären Standorts verwenden wie der Client.

> [!Important]  
> Diese schrittweise erfolgenden Verbesserungen am Softwarecenter und am Verwaltungspunkt zielen darauf ab, die Anwendungskatalogrollen auslaufen zu lassen.
>
> - Die Silverlight-Benutzeroberfläche wird ab Current Branch-Version 1806 nicht unterstützt.
> - Ab Version 1906 verwenden aktualisierte Clients automatisch den Verwaltungspunkt für Anwendungsbereitstellungen, die Benutzern zur Verfügung stehen. Zudem können Sie keine neuen Anwendungskatalogrollen installieren.
> - Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910.  

Weitere Informationen finden Sie unter [Entfernen des Anwendungskatalogs](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat) und [Plan for Software Center](../../../apps/plan-design/plan-for-software-center.md) (Planen für das Softwarecenter).

### <a name="redesigned-notification-for-newly-available-software"></a>Neu gestaltete Benachrichtigung für neu verfügbare Software

<!--3555904-->
Die Benachrichtigung **Neue Software ist verfügbar** wird für eine bestimmte Anwendung und Revision für einen Benutzer nur einmal angezeigt. Für den Benutzer wird die Benachrichtigung nicht mehr bei jeder Anmeldung angezeigt. Es wird nur dann eine weitere Benachrichtigung für eine Anwendung angezeigt, wenn sie geändert oder neu bereitgestellt wurde.

Weitere Informationen finden Sie unter [Create and deploy an application with System Center Configuration Manager (Erstellen und Bereitstellen einer Anwendung mit System Center Configuration Manager)](../../../apps/get-started/create-and-deploy-an-application.md#end-user-experience).

### <a name="more-frequent-countdown-notifications-for-restarts"></a>Häufigere Countdownbenachrichtigungen für Neustarts

<!--3976435-->

Endbenutzer werden nun häufiger mit gelegentlichen Countdownbenachrichtigungen an einen anstehenden Neustart erinnert. Sie können das Intervall für die zeitweiligen Benachrichtigungen auf der Seite **Computerneustart** in **Clienteinstellungen** festlegen. Ändern Sie den Wert für **Dauer bis zur erneuten Anzeige von Countdownbenachrichtigungen zum Computerneustart angeben (Minuten)** , um zu konfigurieren, wie oft ein Benutzer über einen anstehenden Neustart benachrichtigt wird, bis die endgültige Benachrichtigung mit dem Countdown angezeigt wird.

Der maximale Wert für **Temporäre Benachrichtigung für Benutzer anzeigen, in der auf das Intervall (in Minuten) bis zum Abmelden des Benutzers oder Neustart des Computers hingewiesen wird** wird zudem von 1.440 Minuten (24 Stunden) auf 20.160 Minuten (zwei Wochen) heraufgesetzt.

Weitere Informationen finden Sie unter [Benachrichtigungen zum Geräteneustart](../../clients/deploy/device-restart-notifications.md) und [About client settings](../../clients/deploy/about-client-settings.md#computer-restart) (Informationen zu Clienteinstellungen).

### <a name="direct-link-to-custom-tabs-in-software-center"></a>Direkter Link zu benutzerdefinierten Registerkarten im Softwarecenter

<!--4655176-->

Sie können Endbenutzern jetzt einen direkten Link zu einer [benutzerdefinierten Registerkarte](../../clients/deploy/about-client-settings.md#software-center-tab-visibility) im Softwarecenter bereitstellen.

Verwenden Sie das folgende URL-Format, um das Softwarecenter für eine bestimmte Registerkarte zu öffnen:

`softwarecenter:page=CustomTab1`

Die Zeichenfolge `CustomTab1` ist die erste benutzerdefinierte Registerkarte in der Reihenfolge.

Geben Sie z.B. diese URL in das Windows-Fenster **Ausführen** ein.

Sie können mit dieser Syntax auch Standardregisterkarten im Softwarecenter öffnen:

|Befehlszeile  |Registerkarte  |
|---------|---------|
|`AvailableSoftware`|Applications|
|`Updates`|Updates|
|`OSD`|Betriebssysteme|
|`InstallationStatus`|Installationsstatus|
|`Compliance`|Gerätekonformität|
|`Options`|Optionen|

Weitere Informationen finden Sie unter [Sichtbarkeit der Registerkarten im Softwarecenter](../../clients/deploy/about-client-settings.md#software-center-tab-visibility).

## <a name="software-updates"></a><a name="bkmk_sum"></a> Softwareupdates

### <a name="additional-options-for-wsus-maintenance"></a>Zusätzliche Optionen für die WSUS-Wartung

<!--4110109-->
Sie verfügen nun über zusätzliche WSUS-Wartungstasks, die Configuration Manager ausführen kann, um die Fehlerfreiheit von Softwareupdatepunkten zu gewährleisten. Die WSUS-Wartung erfolgt nach jeder Synchronisierung. Configuration Manager kann nun nicht nur abgelaufene Updates in WSUS ablehnen, sondern auch Folgendes ausführen:

- Entfernen veralteter Updates aus der WSUS-Datenbank.
- Hinzufügen nicht gruppierter Indizes zur WSUS-Datenbank, um die WSUS-Bereinigungsleistung zu verbessern.

Weitere Informationen finden Sie unter [Wartung von Softwareupdates](../../../sum/deploy-use/software-updates-maintenance.md#wsus-cleanup-starting-in-version-1906).

### <a name="configure-the-default-maximum-run-time-for-software-updates"></a>Konfigurieren der standardmäßigen maximalen Laufzeit für Softwareupdates

<!--3734426-->

Sie können nun angeben, wie lange die Installation eines Softwareupdates maximal dauern darf. Sie können auf der Registerkarte **Maximale Laufzeit** auf dem Softwareupdatepunkt folgende Elemente angeben:

- **Maximale Laufzeit für Windows-Featureupdates (Minuten)**
- **Maximale Laufzeit für Office 365-Updates und Nicht-Featureupdates für Windows (Minuten)**

Weitere Informationen finden Sie unter [Planen von Softwareupdates](../../../sum/plan-design/plan-for-software-updates.md#bkmk_maxruntime).

### <a name="configure-dynamic-update-during-feature-updates"></a>Konfigurieren des dynamischen Updates während Featureupdates

<!--4062619-->

Verwenden Sie eine neue Clienteinstellung zum Konfigurieren von [Dynamisches Update](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847) während Installationen von Windows 10-Featureupdates. „Dynamisches Update“ installiert Language Packs, Features bei Bedarf, Treiber und kumulative Updates während des Windows-Setups, indem der Client zum Download der betreffenden Updates aus dem Internet weitergeleitet wird.

Weitere Informationen finden Sie unter [Software update client settings](../../clients/deploy/about-client-settings.md#software-updates) (Clienteinstellungen für Softwareupdates) und [Manage Windows as a service](../../../osd/deploy-use/manage-windows-as-a-service.md) (Verwalten von Manage Windows-as-a-Service).

### <a name="new-windows-10-version-1903-and-later-product-category"></a>Produktkategorie neues Windows 10, Version 1903 und höher

<!--4682946-->

**Windows 10, Version 1903 und höher** wurde Microsoft Update als eigenes Produkt hinzugefügt, anstatt wie frühere Versionen Teil des Produkts **Windows 10** zu sein. Aufgrund dieser Änderung mussten Sie eine Reihe von manuellen Schritten ausführen, um sicherzustellen, dass Ihre Clients diese Updates sehen. Wir haben die Anzahl der manuellen Schritte reduziert, die Sie für das neue Produkt ausführen müssen.

Wenn Sie ein Update auf Configuration Manager, Version 1906 ausführen und das Produkt **Windows 10** für die Synchronisierung ausgewählt haben, werden die folgenden Aktionen automatisch ausgeführt:

- Das Produkt **Windows 10, Version 1903 und höher** wird für die Synchronisierung hinzugefügt.
- Automatische Bereitstellungsregeln, die das Produkt **Windows 10** enthalten, werden aktualisiert, sodass sie **Windows 10, Version 1903 und höher** enthalten.
- Wartungspläne werden aktualisiert, sodass sie das Produkt **Windows 10, Version 1903 und höher** enthalten.

Weitere Informationen finden Sie unter [Konfigurieren der zu synchronisierenden Klassifizierungen und Produkte](../../../sum/get-started/configure-classifications-and-products.md), [Wartungspläne](../../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow) und [Automatische Bereitstellungsregeln](../../../sum/deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process).

### <a name="drill-through-required-updates"></a>Ausführen eines Drillthrough durch erforderliche Updates

<!--4224414-->
Sie können jetzt einen Drillthrough durch die Konformitätsstatistiken durchführen, um herauszufinden, auf welchen Geräten das jeweilige Softwareupdate erforderlich ist. Sie benötigen zum Abrufen der Geräteliste die Berechtigung, Updates und die jeweiligen Sammlungen abzurufen, zu denen die Geräte gehören. Um einen Drilldown in die Geräteliste durchzuführen, wählen Sie den Link **Erforderliche anzeigen** neben dem Kreisdiagramm auf der Registerkarte **Zusammenfassung** für ein Update aus. Wenn Sie auf den Link klicken, gelangen Sie zu einem temporären Knoten unter **Geräte**, in dem die Geräte angezeigt werden, für die das Update erforderlich ist.

Der Link **Erforderliche anzeigen** ist an folgenden Stellen verfügbar:

   - **Softwarebibliothek** > **Softwareupdates** > **Alle Softwareupdates**
   - **Softwarebibliothek** > **Windows 10-Wartung** > **Alle Windows 10-Updates**
   - **Softwarebibliothek** > **Office 365-Clientverwaltung** > **Office 365-Updates**

Weitere Informationen finden Sie unter [Monitor software updates](../../../sum/deploy-use/monitor-software-updates.md#drill-through-required-updates) (Verwalten von Softwareupdates), [Manage Windows as a service](../../../osd/deploy-use/manage-windows-as-a-service.md#drill-through-required-updates) (Verwalten von Windows-as-a-Service) und [Verwalten von Office 365 ProPlus-Updates](../../../sum/deploy-use/manage-office-365-proplus-updates.md#drill-through-required-office-365-updates).


## <a name="office-management"></a><a name="bkmk_o365"></a> Office-Verwaltung

### <a name="office-365-proplus-upgrade-readiness-dashboard"></a>Office 365 ProPlus-Dashboard für die Upgradebereitschaft

<!--4021125-->

Es gibt ein neues Bereitschaftsdashboard, mit dem Sie ermitteln können, welche Geräte für ein Upgrade auf Office 365 ProPlus bereit sind. Es enthält die Kachel **Office 365 ProPlus upgrade readiness** (Office 365 ProPlus-Upgradebereitschaft), die in der aktuellen Configuration Manager-Branchversion 1902 veröffentlicht wurde. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, erweitern Sie **Office 365-Clientverwaltung**, und wählen Sie den Knoten **Office 365 ProPlus Upgrade Readiness** (Office 365 ProPlus-Upgradebereitschaft) aus.

Weitere Informationen zum Dashboard sowie zu Voraussetzungen und zur Verwendung dieser Daten finden Sie unter [Integration für Office 365 ProPlus-Bereitschaft](../../../sum/deploy-use/office-365-dashboard.md#bkmk_readiness-dash).


## <a name="protection"></a><a name="bkmk_protect"></a> Schutz

### <a name="windows-defender-application-guard-file-trust-criteria"></a>Windows Defender Application Guard: Kriterien für die Vertrauenswürdigkeit von Dateien

<!--3555858-->

Es gibt eine neue Richtlinieneinstellung, die es Benutzern ermöglicht, Dateien zu vertrauen, die normalerweise in Windows Defender Application Guard (WDAG) geöffnet werden. Nach erfolgreicher Durchführung werden die Dateien auf dem Hostgerät und nicht in WDAG geöffnet.

Weitere Informationen finden Sie unter [Erstellen und Bereitstellen einer Windows Defender Application Guard-Richtlinie](../../../protect/deploy-use/create-deploy-application-guard-policy.md#bkmk_FM).


## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Configuration Manager-Konsole

### <a name="role-based-access-for-folders"></a>Rollenbasierter Zugriff für Ordner

<!--3600867-->

Sie können nun Sicherheitsbereiche für Ordner festlegen. Wenn Sie Zugriff auf ein Objekt im Ordner, aber keinen Zugriff auf den Ordner haben, können Sie das Objekt nicht anzeigen. Ebenso wird das Objekt nicht angezeigt, wenn Sie Zugriff auf einen Ordner, jedoch nicht auf ein darin enthaltenes Objekt haben. Klicken Sie mit der rechten Maustaste auf einen Ordner, klicken Sie auf **Sicherheitsbereiche festlegen**, und wählen Sie anschließend die anzuwendenden Sicherheitsbereiche aus.

Weitere Informationen finden Sie unter [Using the Configuration Manager console](../../servers/manage/admin-console.md#tips) (Verwenden der Configuration Manager-Konsole) und [Configure role-based administration](../../servers/deploy/configure/configure-role-based-administration.md#bkmk_config-folder) (Konfigurieren der rollenbasierten Verwaltung).

### <a name="add-smbios-guid-column-to-device-and-device-collection-nodes"></a>Hinzufügen der SMBIOS GUID-Spalte zu den Knoten „Geräte“ und „Gerätesammlungen“

<!--4526580-->
Sowohl im Knoten **Geräte** als auch im Knoten **Gerätesammlungen** können Sie nun eine neue Spalte für **SMBIOS GUID** hinzufügen. Dieser Wert ist identisch mit der **BIOS GUID**-Eigenschaft der Klasse „Systemressource“. Es handelt wich um einen eindeutigen Bezeichner für die Gerätehardware.

### <a name="administration-service-support-for-security-nodes"></a>Unterstützung des Verwaltungsdiensts für Sicherheitsknoten

<!--4223683-->
Sie können jetzt einige Knoten der Configuration Manager-Konsole zur Verwendung des Verwaltungsdiensts aktivieren. Diese Änderung ermöglicht der Konsole die Kommunikation mit dem SMS-Anbieter über HTTPS anstatt WMI.

Weitere Informationen finden Sie unter [Verwaltungsdienst](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service).

> [!Note]
> Ab Version 1906 heißt die Registerkarte **Kommunikation mit Clientcomputern** in den Standorteigenschaften **Sichere Kommunikation**.<!-- SCCMDocs#1645 -->  

### <a name="collections-tab-in-devices-node"></a>Registerkarte „Sammlungen“ im Knoten „Geräte“

<!--4616810-->
Wechseln Sie im Arbeitsbereich **Bestand und Konformität** zum Knoten **Geräte**, und wählen Sie ein Gerät aus. Wechseln Sie im Detailbereich zur neuen Registerkarte **Sammlungen**. Auf dieser Registerkarte finden Sie die Sammlungen, zu denen dieses Gerät gehört.

> [!Note]  
> - Diese Registerkarte ist derzeit nicht in einem Unterknoten „Geräte“ unter dem Knoten **Gerätesammlungen** verfügbar. Beispielsweise, wenn Sie die Option **Mitglieder anzeigen** für eine Sammlung auswählen.
> - Diese Registerkarte wird für einige Benutzer möglicherweise nicht erwartungsgemäß aufgefüllt. Sie müssen die Sicherheitsrolle **Hauptadministrator** haben, um die vollständige Liste der Sammlungen anzuzeigen, zu denen ein Gerät gehört. Dies ist ein bekanntes Problem. <!--5107309-->

### <a name="task-sequences-tab-in-applications-node"></a>Registerkarte „Tasksequenzen“ im Knoten „Anwendungen“

<!--4616810-->
Erweitern Sie im Arbeitsbereich **Softwarebibliothek** die Option **Anwendungsverwaltung**. Wechseln Sie dann zum Knoten **Anwendungen**, und wählen Sie eine Anwendung aus. Wechseln Sie im Detailbereich zur neuen Registerkarte **Tasksequenzen**. Diese Registerkarte listet die Tasksequenzen auf, die auf diese Anwendung verweisen.

### <a name="show-collection-name-for-scripts"></a>Anzeigen des Sammlungsnamen für Skripts

<!--4616810-->
Klicken Sie im Arbeitsbereich **Überwachung** auf den Knoten **Skriptstatus**. Er enthält nun zusätzlich zur ID den **Sammlungsnamen**.

### <a name="real-time-actions-from-device-lists"></a>Echtzeitaktionen in Gerätelisten

<!--4616810-->
Es gibt verschiedene Möglichkeiten, eine Liste von Geräten im Arbeitsbereich **Bestand und Konformität** unter dem Knoten **Geräte** anzuzeigen.

- Wählen Sie im Arbeitsbereich **Bestand und Konformität** den Knoten **Gerätesammlungen** aus. Wählen Sie eine Gerätesammlung und dann die Aktion **Mitglieder anzeigen** aus. Diese Aktion öffnet Unterknoten des Knotens **Geräte** mit der Geräteliste für diese Sammlung.  

  - Wenn Sie den Unterknoten „Sammlung“ auswählen, können Sie auf dem Menüband nun **CMPivot** in der Gruppe „Sammlung“ starten.  

- Klicken Sie im Arbeitsbereich **Überwachung** auf den Knoten **Bereitstellungen**. Wählen Sie eine Bereitstellung aus, und klicken Sie auf dem Menüband auf **Status anzeigen**. Doppelklicken Sie im Bereich „Bereitstellungsstatus“ auf den gesamten Bestand, um zu einer Geräteliste zu gelangen.  

  - Wenn Sie ein Gerät in dieser Liste auswählen, können Sie auf dem Menüband in der Gruppe „Gerät“ **CMPivot** und **Skripts ausführen** starten.  

### <a name="order-by-program-name-in-task-sequence"></a>Sortieren nach Programmname in der Tasksequenz

<!--4616810-->
Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und wählen Sie den Knoten **Tasksequenzen** aus. Bearbeiten Sie eine Tasksequenz, um anschließend den Schritt [Paket installieren](../../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) auszuwählen oder hinzuzufügen. Wenn ein Paket mehr als ein Programm enthält, werden die Programme in der Dropdownliste nun alphabetisch sortiert.

### <a name="correct-names-for-client-operations"></a>Richtige Namen für Clientvorgänge

<!--4616810-->
Wählen Sie im Arbeitsbereich **Überwachung** die Option **Clientvorgänge** aus. Der Vorgang **Zum nächsten Softwareupdatepunkt wechseln** ist jetzt ordnungsgemäß benannt.


## <a name="deprecated-features-and-operating-systems"></a><a name="bkmk_deprecated"></a> Veraltete Features und Betriebssysteme

Erfahren Sie mehr zu Änderungen bei der Unterstützung, bevor sie in [entfernte und veraltete Elemente](deprecated/removed-and-deprecated.md) aufgenommen werden.

In Version 1906 wird die Unterstützung für die folgenden Features eingestellt:  

- Sie können keine neuen Anwendungskatalogrollen installieren. Aktualisierte Clients verwenden automatisch den Verwaltungspunkt für Anwendungsbereitstellungen, die Benutzern zur Verfügung stehen. Weitere Informationen finden Sie unter [Planen für Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex).

In Version 1906 wird die Unterstützung für die folgenden Produkte eingestellt:  

- Windows CE 7.0
- Windows 10 Mobile
- Windows 10 Mobile Enterprise


## <a name="other-updates"></a>Weitere Updates

Ab dieser Version sind die folgenden Features keine Vorabfeatures mehr:

- [Verwaltungsdienst für SMS-Anbieter](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service)
- [Verwaltung der Windows Defender-Anwendungssteuerung](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md)

Neben neuen Features umfasst dieses Release auch weitere Änderungen, beispielsweise Fehlerbehebungen. Weitere Informationen finden Sie unter [Zusammenfassung der Änderungen im Current Branch von Configuration Manager, Version 1906](https://support.microsoft.com/help/4514258).

Weitere Informationen zu Änderungen der Windows PowerShell-Cmdlets für Configuration Manager finden Sie in den [Versionshinweisen zu PowerShell 1906](https://docs.microsoft.com/powershell/sccm/1906-release-notes?view=sccm-ps).

Folgender Updaterollup (4517869) ist ab 1. Oktober 2019 in der Konsole verfügbar: [Updaterollup für den aktuellen Branch von Configuration Manager, Version 1906](https://support.microsoft.com/help/4517869).

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!Note]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->


## <a name="next-steps"></a>Nächste Schritte

<!--At this time, version 1906 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-1906.md#early-update-ring). -->
Ab dem 16. August 2019 ist Version 1906 global für alle Kunden zur Installation verfügbar.

Wenn Sie zum Installieren dieser Version bereit sind, finden Sie weitere Informationen dazu unter [Installieren von Updates für Configuration Manager](../../servers/manage/updates.md) und [Checkliste für die Installation von Update 1906](../../servers/manage/checklist-for-installing-update-1906.md).

> [!TIP]  
> Verwenden Sie eine Baselineversion von Configuration Manager, um einen neuen Standort zu installieren.  
>
> Weitere Informationen:
>
> - [Installieren von neuen Standorten](../../servers/deploy/install/installing-sites.md)  
> - [Baseline- und Updateversionen](../../servers/manage/updates.md#bkmk_Baselines)  

Informationen zu bekannten, erheblichen Problemen finden Sie in den [Versionshinweisen](../../servers/deploy/install/release-notes.md).

Nachdem Sie einen Standort aktualisiert haben, überprüfen Sie auch die [Checkliste für Aufgaben nach dem Update](../../servers/manage/checklist-for-installing-update-1906.md#post-update-checklist).
