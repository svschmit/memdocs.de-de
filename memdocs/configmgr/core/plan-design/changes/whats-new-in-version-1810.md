---
title: Neuerungen in Version 1810
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über Änderungen und neue Funktionen, die in Version 1810 des Current Branchs von Configuration Manager eingeführt wurden.
ms.date: 04/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4812324b-e6aa-4431-bf1d-9fcd763a8caa
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 549940abdfd69f3998cab8f236a29b8fd097b705
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702288"
---
# <a name="whats-new-in-version-1810-of-configuration-manager-current-branch"></a>Neuerungen in Version 1810 von Configuration Manager (Current Branch)

*Gilt für: Configuration Manager (Current Branch)*

Das Update 1810 für den Current Branch von Configuration Manager ist als konsoleninternes Update verfügbar. Wenden Sie dieses Update auf Standorte an, an denen die Version 1710, 1802 oder 1806 ausgeführt werden. <!-- baseline only statement: When installing a new site, it's also available as a baseline version.--> In diesem Artikel werden die Änderungen und neuen Features in Configuration Manager Version 1810 zusammengefasst.  

Überprüfen Sie stets die neueste Checkliste für die Installation dieses Updates. Informationen finden Sie in der [Checkliste für die Installation von Update 1810](../../servers/manage/checklist-for-installing-update-1810.md). Nachdem Sie einen Standort aktualisiert haben, überprüfen Sie auch die [Checkliste für Aufgaben nach dem Update](../../servers/manage/checklist-for-installing-update-1810.md#post-update-checklist).

Wenn Sie neue Configuration Manager-Features nutzen möchten, müssen Sie zunächst die Clients auf die neueste Version aktualisieren. Beim Update des Standorts und der Konsole werden neue Features in der Configuration Manager-Konsole angezeigt. Das vollständige Szenario ist allerdings erst einsatzbereit, wenn auch die Clientversion aktualisiert wird.

<!--
> [!Note]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized. 
-->  

> [!Tip]  
> Um bei einer Aktualisierung dieser Seite benachrichtigt zu werden, kopieren Sie die folgende URL, und fügen Sie sie in Ihren RSS-Feedreader ein: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1810+-+Configuration+Manager%22&locale=en-us`



## <a name="deprecated-features-and-operating-systems"></a><a name="bkmk_deprecated"></a> Veraltete Features und Betriebssysteme

Erfahren Sie mehr zu Änderungen bei der Unterstützung, bevor sie in [entfernte und veraltete Elemente](deprecated/removed-and-deprecated.md) aufgenommen werden.

Ab dem 14. August 2018 gilt das Feature für die hybride Verwaltung mobiler Geräte als veraltet. Weitere Informationen finden Sie unter [Hybride Verwaltung mobiler Geräte](../../../mdm/understand/what-happened-to-hybrid.md).<!--Intune feature 2683117-->  

Der Support für System Center Endpoint Protection (SCEP) für Mac und Linux (alle Versionen) endet am 31. Dezember 2018. Die Verfügbarkeit der neuen Virusdefinitionen für SCEP für Mac und SCEP für Linux wird möglicherweise nach Ende der Unterstützung eingestellt. Weitere Informationen finden Sie im [Blogbeitrag zum Ende des Supports](https://go.microsoft.com/fwlink/?linkid=870182).

Klassische Dienstbereitstellungen in Azure sind jetzt in Configuration Manager veraltet. Verwenden Sie ab jetzt Azure Resource Manager-Bereitstellungen für Cloud Management Gateway und den Cloudverteilungspunkt. Weitere Informationen finden Sie unter [Planen des Cloudverwaltungsgateways](../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager).



## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> Standortinfrastruktur

### <a name="support-for-windows-server-2019"></a>Unterstützung für Windows Server 2019

<!--1359195-->
Configuration Manager unterstützt jetzt Windows Server 2019 und Windows Server Version 1809 als Standortsysteme.

Weitere Informationen finden Sie unter [Unterstützte Betriebssysteme für Standortsystemserver](../configs/supported-operating-systems-for-site-system-servers.md).


### <a name="hierarchy-support-for-site-server-high-availability"></a>Hierarchieunterstützung für die Hochverfügbarkeit von Standortservern

<!--3607755, fka 1358224-->
Standorte der zentralen Verwaltung und untergeordnete primäre Standorte können jetzt über einen zusätzlichen Standortserver im passiven Modus verfügen.

Weitere Informationen finden Sie unter [Site server high availability (Hochverfügbarkeit des Standortservers)](../../servers/deploy/configure/site-server-high-availability.md).


### <a name="improvements-to-setup-prerequisites"></a>Verbesserungen der Setupvoraussetzungen

Wenn Sie Version 1810 installieren oder ein Upgrade auf diese durchführen, umfasst das Configuration Manager-Setup jetzt die folgenden neuen oder verbesserten Voraussetzungsprüfungen:

- **Ausstehender Systemneustart:** Diese Voraussetzungsprüfung ist jetzt resilienter. Es prüft zusätzliche Registrierungsschlüssel für Windows-Features. Weitere Informationen finden Sie unter [Ausstehender Systemneustart](../../servers/deploy/install/list-of-prerequisite-checks.md#pending-system-restart). <!--SCCMDocs-pr issue 3010-->  

- **SQL-Änderungsnachverfolgungsbereinigung:** Eine wird geprüft, ob die Standortdatenbank über ein Backlog mit Daten zur SQL-Änderungsnachverfolgung verfügt. Weitere Informationen, u.a. auch eine Prozedur zum überprüfen und bereinigen des Backlogs, finden Sie unter [SQL-Änderungsnachverfolgungscleanup](../../servers/deploy/install/list-of-prerequisite-checks.md#bkmk_changetracking). <!--SCCMDocs-pr issue 3023-->  

- **Version des SQL Native Client:** Diese Überprüfung der Voraussetzungen wird für Versionen des SQL Native Client aktualisiert, die TLS 1.2 unterstützen. Die Mindestversion ist [SQL 2012 SP4](https://www.microsoft.com/download/details.aspx?id=50402). Weitere Informationen finden Sie unter [SQL Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client). <!--SCCMDocs-pr issue 3094-->  

- **Standortsystem auf dem Windows-Clusterknoten:** Der Einrichtungsprozess für Configuration Manager blockiert nicht mehr die Installation der Standortserverrolle auf einem Computer mit der Windows-Rolle für Failoverclustering. SQL Always On erfordert diese Rolle, daher konnten Sie die Standortdatenbank auf dem Standortserver bisher nicht gleichzeitig installieren. Mit dieser Änderung haben Sie die Möglichkeit, eine hochverfügbare Website mit weniger Servern zu erstellen, indem Sie SQL Always On und einen Standortserver im passiven Modus verwenden. Weitere Informationen finden Sie unter [Windows-Failovercluster](../../servers/deploy/install/list-of-prerequisite-checks.md#windows-failover-cluster). <!--1359132-->  


### <a name="new-permission-for-client-notification-actions"></a>Neue Berechtigungen für Clientbenachrichtigungsaktionen

<!--SCCMDocs-pr issue #2972-->
Für Clientbenachrichtigungsaktionen ist jetzt die Berechtigung **Ressource benachrichtigen** in der SMS_Collection-Klasse erforderlich. Die folgenden integrierten Rollen verfügen standardmäßig über diese Berechtigung:

- Hauptadministrator  
- Infrastrukturadministrator  

Fügen Sie diese Berechtigung benutzerdefinierten Rollen hinzu, die Clientbenachrichtigungsaktionen verwenden müssen.

Weitere Informationen finden Sie im Artikel zu [Clientbenachrichtigungen](../../clients/manage/client-notification.md).



## <a name="content-management"></a><a name="bkmk_content"></a> Content Management

### <a name="new-boundary-group-options"></a>Neue Begrenzungsgruppenoptionen

<!--1358749-->
Begrenzungsgruppen beinhalten nun die folgenden zusätzlichen Einstellungen, die Ihnen mehr Kontrolle über die Verteilung von Inhalten in Ihrer Umgebung einräumen:

- **Verteilungspunkte über Peers innerhalb desselben Subnetzes vorziehen:** Standardmäßig priorisiert der Verteilungspunkt Peercachequellen ganz oben in der Liste der Inhaltsspeicherorte. Diese Einstellung kehrt diese Priorität für Clients um, die sich im gleichen Subnetz wie die Peercachequelle befinden.  

- **Cloudverteilungspunkte Verteilungspunkten vorziehen:** Wenn Sie eine Niederlassung mit einer schnelleren Internetverbindung haben, können Sie jetzt Cloudinhalte priorisieren.  

Weitere Informationen finden Sie unter [Begrenzungsgruppenoptionen für Peerdownloads](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).


### <a name="management-insights-rule-for-peer-cache-source-client-version"></a>Regel für Verwaltungseinblicke für Clientversionen der Peercachequelle

<!-- 1358008 -->
Eine neue Regel im Knoten **Verwaltungseinblicke** bestimmt Clients, die als Peercachequelle dienen, aber noch nicht von einer Clientversion vor 1806 upgegradet wurden. Die neue Regel lautet **Peercachequellen auf die neueste Version des Configuration Manager-Clients aktualisieren** und ist Teil der neuen Regelgruppe **Proaktive Wartung**. Clients vor Version 1806 können nicht als Peercachequelle für Clients verwendet werden, die Version 1806 oder höher ausführen. Wählen Sie **Aktion ausführen** aus, um eine Geräteansicht zu öffnen, die die Clientliste anzeigt.

Weitere Informationen finden Sie unter [Einblicke für die Verwaltung](../../servers/manage/management-insights.md).



## <a name="client-management"></a><a name="bkmk_client"></a> Clientverwaltung

### <a name="new-client-notification-action-to-wake-up-device"></a>Neue Clientbenachrichtigungsaktion für die Aktivierung von Geräten

<!--1317364-->
Mithilfe der Configuration Manager-Konsole können Sie ab sofort Clients reaktivieren, auch wenn sich der Client nicht im selben Subnetz wie der Standortserver befindet. Wenn Sie Wartungen durchführen oder Geräte abfragen müssen, sind Sie nicht durch Remoteclients eingeschränkt, die sich im Ruhezustand befinden. Der Standortserver verwendet den Clientbenachrichtigungskanal, um einen anderen Client zu bestimmen, der im gleichen Remotesubnetz aktiv ist. Dieser Client wird dann verwendet, um eine Wake-on-LAN-Anforderung (Magic Packet) zu senden.

Weitere Informationen finden Sie unter [Konfigurieren von Wake-On-LAN in System Center Configuration Manager](../../clients/deploy/configure-wake-on-lan.md) und [Planen des Aufweckens von Clients in System Center Configuration Manager](../../clients/deploy/plan/plan-wake-up-clients.md).

### <a name="new-option-to-perform-client-notification-from-devices-node"></a>Neue Option zum Ausführen der Clientbenachrichtigung aus dem Knoten „Geräte“

<!--1317364-->
Bis Version 1810 stand die Option **Clientbenachrichtigung** nur über den Knoten „Gerätesammlung“ oder durch Anzeige der Mitgliedschaft einer Gerätesammlung zur Verfügung. Jetzt können Sie eine **Clientbenachrichtigung** direkt über den Knoten **Geräte** durchführen. Sie müssen sich nicht mehr in einer Ansicht der Sammlungsmitgliedschaft befinden.

Weitere Informationen finden Sie im Artikel zu [Clientbenachrichtigungen](../../clients/manage/client-notification.md).


### <a name="improvements-to-collection-evaluation"></a>Verbesserung der Collectionauswertung

<!--3607726, fka 1358981-->
Die folgenden Änderungen am Verhalten von Sammlungsauswertungen können die Leistung der Website verbessern:  

- Wenn Sie bislang einen Zeitplan für eine abfragebasierte Sammlung konfiguriert haben, hat die Website die Abfrage weiterhin ausgewertet, unabhängig davon, ob die Sammlungseinstellung **Vollständiges Update für diese Sammlung planen** aktiviert ist. Um den Zeitplan vollständig zu deaktivieren, müssen Sie den Zeitplan auf **Kein** festlegen. Nun löscht die Website den Zeitplan, wenn Sie diese Einstellung deaktivieren. Um einen Zeitplan für die Auswertung anzugeben, aktivieren Sie die Option **Vollständiges Update für diese Sammlung planen**.  

- Die Auswertung von integrierten Sammlungen wie **Alle Systeme** lässt sich nicht deaktivieren, doch nun können Sie den Zeitplan konfigurieren. Mit diesem Verhalten können Sie diese Aktion zu einem Zeitpunkt anpassen, der Ihren Geschäftsanforderungen entspricht.

Weitere Informationen finden Sie unter [Erstellen von Sammlungen](../../clients/manage/collections/create-collections.md#bkmk_create).


### <a name="improvement-to-client-installation"></a>Verbesserungen der Clientinstallation

<!--1358840-->
Bei der Installation des Konfigurations-Manager-Clients kontaktiert der Ccmsetup-Vorgang den Verwaltungspunkt, um den erforderlichen Inhalt zu suchen. Zuvor hat der Verwaltungspunkt in diesem Vorgang nur Verteilungspunkte der aktuellen Begrenzungsgruppe des Clients zurückgegeben. Wenn kein Inhalt verfügbar ist, greift der Setupvorgang auf das Herunterladen von Inhalten vom Verwaltungspunkt zurück. Es gibt keine Option für ein Fallback auf Verteilungspunkte in anderen Begrenzungsgruppen, die den erforderlichen Inhalt enthalten könnten. Der Verwaltungspunkt gibt nun Verteilungspunkte basierend auf der Konfiguration der Begrenzungsgruppe zurück.

Weitere Informationen finden Sie unter [Configure boundary groups](../../servers/deploy/configure/boundary-groups.md#bkmk_ccmsetup) (Konfigurieren von Begrenzungsgruppen).



## <a name="co-management"></a><a name="bkmk_comgmt"></a> Die Co-Verwaltung

### <a name="required-app-compliance-policy-for-co-managed-devices"></a>Erforderliche App-Konformitätsrichtlinie für gemeinsam verwaltete Geräte

<!--1358196-->
Definieren Sie Regeln zu Konformitätsrichtlinien im Configuration Manager für die erforderlichen Anwendungen. Diese App-Bewertung ist Teil des gesamten Konformitätszustands, der an Microsoft Intune für gemeinsam verwaltete Geräte gesendet wird.

Weitere Informationen finden Sie unter [Workloads für die Co-Verwaltung](../../../comanage/workloads.md).


### <a name="improvement-to-co-management-dashboard"></a>Verbesserungen am Dashboard für die Co-Verwaltung

<!--1358980-->
Das Dashboard für die Co-Verwaltung wurde durch die folgenden ausführlicheren Informationen erweitert:  

- Die Kachel **Registrierungsstatus der Co-Verwaltung** enthält nun zusätzliche Status

- Eine neue Kachel **Co-Verwaltungsstatus** mit einem Trichterdiagramm, in dem die Status des Registrierungsprozesses gezeigt werden

- Es gibt eine neue Kachel mit der Anzahl von **Registrierungsfehlern**

![Screenshot: Dashboard für die Co-Verwaltung mit den obersten vier Kacheln](media/1358980-comgmt-dashboard.png)

Weitere Informationen finden Sie im Artikel zum [Dashboard für die Co-Verwaltung](../../../comanage/how-to-monitor.md#co-management-dashboard).


### <a name="improvements-to-internet-based-client-setup"></a>Verbesserungen beim Einrichten internetbasierter Clients

<!--3607731, fka 1359181-->
Dieses Release vereinfacht die Einrichtung von internetbasierten Clients in Configuration Manager. Die Website veröffentlicht zusätzliche Azure Active Directory-Informationen (Azure AD) für Cloud Management Gateway. Ein in Azure AD eingebundener Client ruft diese Informationen beim ccmsetup-Prozess von Cloud Management Gateway ab und verwendet dabei den gleichen Mandanten, mit dem er verknüpft ist. Dieses Verhalten vereinfacht das Registrieren von Geräten zur gemeinsamen Verwaltung in einer Umgebung mit mehreren Azure AD-Mandanten. Nun sind die einzigen beiden erforderlichen ccmsetup-Eigenschaften **CCMHOSTNAME** und **SMSSiteCode**.

Weitere Informationen finden Sie unter [Vorbereiten internetbasierter Geräte für die Co-Verwaltung](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client).



## <a name="application-management"></a><a name="bkmk_app"></a> Anwendungsverwaltung

### <a name="convert-applications-to-msix"></a>Konvertieren von Anwendungen in MSIX

<!--3607729, fka 1359029-->
Ab Version 1806 unterstützt Configuration Manager die Bereitstellung des neuen Windows 10-App-Paketformats MSIX. Nun können Sie Ihre vorhandenen Windows Installer-Anwendungen (MSI) in das MSIX-Format konvertiert.

Weitere Informationen finden Sie unter [Erstellen von Windows-Anwendungen](../../../apps/get-started/creating-windows-applications.md#bkmk_msix).  


### <a name="repair-applications"></a>Reparieren von Anwendungen

<!--1357866-->
Geben Sie eine Reparaturbefehlszeile für die Windows Installer- und Skriptinstallationsprogramm-Bereitstellungstypen an. Wenn Sie dann die Option in der Bereitstellung aktivieren, wird im Softwarecenter eine neue Schaltfläche verfügbar, um die Anwendung zu **Reparieren**. Wenn Sie eine Anwendung mit einem Reparaturprogramm konfigurieren, können Benutzer den Befehl über das Softwarecenter starten.

Weitere Informationen finden Sie im Artikel zum [Erstellen von Anwendungen](../../../apps/deploy-use/create-applications.md#bkmk_dt-content) und zum [Bereitstellen von Anwendungen](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings).


### <a name="approve-application-requests-via-email"></a>Genehmigen von Anwendungsanforderungen per E-Mail

<!--1321550-->
Hiermit werden E-Mail-Benachrichtigungen zum Genehmigen von Anwendungsanforderungen konfiguriert. Wenn ein Benutzer eine Anwendung anfordert, erhalten Sie eine E-Mail. Klicken Sie auf die Links in der E-Mail, um die Anforderung ohne die Configuration Manager-Konsole zu genehmigen oder abzulehnen.

Weitere Informationen finden Sie im Artikel zum [Genehmigen von Anwendungen](../../../apps/deploy-use/app-approval.md).


### <a name="detection-methods-dont-load-windows-powershell-profiles"></a>Erkennungsmethoden laden Windows PowerShell-Profile nicht

<!--3607762, fka 1359239-->
Sie können Windows PowerShell-Skripts für Erkennungsmethoden in Anwendungen und Einstellungen in Konfigurationselementen verwenden. Wenn diese Skripts auf Clients ausgeführt werden, ruft der Konfigurations-Manager-Client jetzt PowerShell mit dem Parameter `-NoProfile` auf. Diese Option startet PowerShell ohne Profile.

Ein PowerShell-Profil ist ein Skript, das ausgeführt wird, wenn PowerShell gestartet wird. Sie können ein PowerShell-Profil erstellen, um Ihre Umgebung anzupassen und um sitzungsspezifische Elemente zu jeder gestarteten PowerShell-Sitzung hinzuzufügen.

> [!Note]  
> Diese Verhaltensänderung gilt nicht für [Skripts](../../../apps/deploy-use/create-deploy-scripts.md) oder [CMPivot](../../servers/manage/cmpivot.md). Diese Features verwenden beide diesen PowerShell-Parameter.  

Weitere Informationen finden Sie unter [Erstellen von Anwendungen](../../../apps/deploy-use/create-applications.md) und [Erstellen benutzerdefinierter Konfigurationselemente](../../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md).



## <a name="os-deployment"></a><a name="bkmk_osd"></a> Bereitstellung des Betriebssystems

### <a name="task-sequence-support-of-windows-autopilot-for-existing-devices"></a>Tasksequenzunterstützung für Windows Autopilot für vorhandene Geräte

<!--3607717, fka 1358333-->
[Windows Autopilot für vorhandene Geräte](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) ist nun mit Windows 10-Version 1809 oder höher verfügbar. Mit dieser neuen Funktion können Sie ein Reimaging für ein Windows 7-Gerät für den [benutzergesteuerten Windows Autopilot-Modus](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) mit einer einzigen, nativen Configuration Manager-Tasksequenz durchführen und das Gerät bereitstellen.

Weitere Informationen finden Sie unter [Windows Autopilot für vorhandene Geräte](../../../osd/deploy-use/windows-autopilot-for-existing-devices.md).


### <a name="specify-the-drive-for-offline-os-image-servicing"></a>Angeben des Laufwerks für die Offlinewartung von Betriebssystemimages

<!--1358924-->
Geben Sie jetzt das Laufwerk an, das Configuration Manager verwendet, wenn Softwareupdates zu Betriebssystemimages und Betriebssystemupgradepaketen hinzugefügt werden. Dieser Prozess kann eine große Menge an Speicherplatz auf dem Datenträger mit temporären Dateien beanspruchen, sodass Ihnen diese Option Flexibilität bei der Auswahl des zu verwendenden Laufwerks bietet.

Weitere Informationen finden Sie in den Artikeln zum [Verwalten von Betriebssystemimages](../../../osd/get-started/manage-operating-system-images.md#bkmk_servicing-drive) und zum [Verwalten von Betriebssystemupgradepaketen](../../../osd/get-started/manage-operating-system-upgrade-packages.md#bkmk_servicing-drive).


### <a name="task-sequence-support-for-boundary-groups"></a>Tasksequenzunterstützung für Begrenzungsgruppen

<!--1359025-->
Wenn ein Gerät eine Tasksequenz ausführt und Inhalt abrufen muss, verwendet es nun ähnlich wie der Konfigurations-Manager-Client Verhaltensweisen von Begrenzungsgruppen.

Weitere Informationen finden Sie unter [Begrenzungsgruppen](../../servers/deploy/configure/boundary-groups.md#bkmk_bgr-osd).


### <a name="improvements-to-driver-maintenance"></a>Verbesserungen an der Wartung für den Treiber

<!--3607716, fka 1358270-->
Treiberpakete verfügen nun über zusätzliche Metadatenfelder für **Hersteller** und **Modell**. Verwenden Sie diese Felder, um Treiberpakete mit Informationen für die allgemeine Verwaltung zu kennzeichnen oder um alte und doppelte Treiber zu identifizieren, die gelöscht werden können.

Weitere Informationen finden Sie unter [Verwalten von Treibern](../../../osd/get-started/manage-drivers.md).

### <a name="improvements-to-windows-10-servicing-plan-filters"></a>Verbesserungen an den Wartungsplanfiltern von Windows 10

<!--3098809, 3113836, 3204570 -->
Den Windows 10-Wartungsplänen wurden zusätzliche Filter hinzugefügt. Sie können jetzt nach **Architektur** und **Produktkategorie** und außerdem danach filtern, ob das Upgrade **Abgelöst** wurde.

Weitere Informationen finden Sie unter [Windows 10-Wartungsplan](../../../osd/deploy-use/manage-windows-as-a-service.md#BKMK_ServicingPlan).

### <a name="new-task-sequence-variable-for-last-action-name"></a>Neue Tasksequenzvariable für den Namen der letzten Aktion

<!--SCCMDocs-pr issue #2964-->
Neben der Tasksequenzvariablen _SMSTSLastActionRetCode legt die Tasksequenz auch die neue Variable **_SMSTSLastActionName** fest. Dieser Wert wird auch in der Datei „smsts.log“ erfasst. Diese neue Variable ist bei der Problembehandlung einer Tasksequenz hilfreich. Wenn ein Schritt fehlschlägt, kann ein benutzerdefiniertes Skript den Namen des Schritts sowie den Rückgabecode enthalten.

Weitere Informationen finden Sie unter [Tasksequenzvariablen](../../../osd/understand/task-sequence-variables.md#SMSTSLastActionName).



## <a name="software-updates"></a><a name="bkmk_sum"></a> Softwareupdates

### <a name="phased-deployment-of-software-updates"></a>Bereitstellung in Phasen von Softwareupdates

<!--1358146-->
Erstellen Sie stufenweise Bereitstellungen für Softwareupdates. Mithilfe von Bereitstellungen in Phasen können Sie einen koordinierten, sequenzierten Softwarerollout basierend auf anpassbaren Kriterien und Gruppen orchestrieren.

Weitere Informationen finden Sie unter [Erstellen von stufenweisen Bereitstellungen mit Configuration Manager](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json).


### <a name="improvement-to-maintenance-windows-for-software-updates"></a>Verbesserung der Wartungsfenster für Softwareupdates

<!--vso2839307-->
Die folgende Clienteinstellung befindet sich in der Gruppe **Softwareupdates**, um das Installationsverhalten von Softwareupdates in Wartungsfenstern zu steuern: **Installation von Updates im Wartungsfenster „Alle Bereitstellungen“ aktivieren, wenn das Wartungsfenster „Softwareupdate“ ist**

Standardmäßig ist diese Option **Nein**, um nicht von dem bestehenden Verhalten abzuweichen. Ändern Sie die Option in **Ja**, damit Clients mögliche andere Wartungsfenster verwenden können, um Softwareupdates zu installieren.

Weitere Informationen finden Sie in den [Clienteinstellungen für Softwareupdates](../../clients/deploy/about-client-settings.md#bkmk_SUMMaint).


### <a name="improvement-to-software-updates-maintenance"></a>Verbesserung an der Wartung von Softwareupdates

<!--2839349-->
WSUS-Cleanupaufgaben werden jetzt an sekundären Standorten ausgeführt. Der WSUS-Cleanup für abgelaufene Updates wird ausgeführt, und ersetzte Updates werden in WSUS für sekundäre Standorte abgelehnt.

Weitere Informationen finden Sie unter [WSUS-Cleanupverhalten ab Version 1810](../../../sum/deploy-use/software-updates-maintenance.md#wsus-cleanup-behavior-starting-in-version-1810).

### <a name="improvement-to-software-update-supersedence-rules"></a>Verbesserungen an den Ablösungsregeln für Softwareupdates

<!--3098809, 2977644-->
Sie können Ablösungsregeln für Featureupdates jetzt getrennt von Nicht-Featureupdates festlegen. Dies bedeutet, dass Ihre Upgrades nicht aus Configuration Manager entfernt werden, ehe Sie die Wartung Ihrer Windows 10-Clients abgeschlossen haben.

Weitere Informationen finden Sie unter [Supersedence rules](../../../sum/get-started/install-a-software-update-point.md#supersedence-rules).

## <a name="reporting"></a><a name="bkmk_report"></a> Berichterstellung

### <a name="improvement-to-lifecycle-dashboard"></a>Verbesserung am Dashboard für den Produktlebenszyklus

<!--1358702-->
Das Dashboard für den Produktlebenszyklus enthält nur Informationen über **System Center 2012 Configuration Manager und höher**.

Außerdem gibt es den neuen Bericht **Lebenszyklus 05A: Produktlebenszyklus-Dashboard**. Dieser Bericht enthält ähnliche Informationen wie das Dashboard in der Konsole.

Weitere Informationen zu diesem Dashboard finden Sie unter [Verwenden des Dashboards für den Produktlebenszyklus](../../clients/manage/asset-intelligence/product-lifecycle-dashboard.md).


### <a name="improvement-to-data-warehouse"></a>Verbesserung an Data Warehouse

<!--1358870-->
Sie können jetzt mehr Tabellen aus der Standortdatenbank mit dem Data Warehouse synchronisieren. Diese Änderung ermöglicht es Ihnen, mehr Berichte basierend auf Ihren geschäftlichen Anforderungen zu erstellen.

Weitere Informationen finden Sie unter [Data Warehouse](../../servers/manage/data-warehouse.md).



## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Configuration Manager-Konsole

### <a name="configuration-manager-administrator-authentication"></a>Administratorauthentifizierung in Configuration Manager

<!--1357013-->
Sie können nun die minimale Authentifizierungsebene für Administratoren zum Zugreifen auf Configuration Manager-Standorte festlegen. Diese Funktion verpflichtet Administratoren dazu, sich mit der erforderlichen Ebene bei Windows anzumelden. Sie können diese Einstellung auf der Registerkarte **Authentifizierung** unter **Hierarchieeinstellungen** konfigurieren.

Weitere Informationen finden Sie unter [Planen des SMS-Anbieters](../hierarchy/plan-for-the-sms-provider.md#bkmk_auth).


### <a name="support-center"></a>Supportcenter

<!--1357489-->
Verwenden Sie das Supportcenter zur Behebung von Clientproblemen, Anzeigen von Protokollen in Echtzeit oder zum Erfassen des Zustands eines Configuration Manager-Clientcomputers zur späteren Analyse. Das Supportcenter ist ein Tool, das viele Problembehandlungstools für Administratoren an einer Stelle vereint. Das Installationsprogramm für das Supportcenter finden Sie auf dem Standortserver im Ordner **cd.latest\SMSSETUP\Tools\SupportCenter**.

Weitere Informationen finden Sie im Artikel zum [Supportcenter](../../support/support-center.md).


### <a name="management-insights-dashboard"></a>Dashboard für Einblicke in die Verwaltung

<!--1357979-->
Der Knoten **Verwaltungseinblicke** enthält nun ein grafisches Dashboard. Dieses Dashboard zeigt nun eine Übersicht der Zustände von Regeln an, wodurch das Anzeigen des Fortschritts vereinfacht wird. Das Dashboard umfasst die folgenden Kacheln:

- **Management Insights-Index:** Verfolgt den Gesamtfortschritt von Management Insights-Regeln. Der Index beschreibt einen gewichteten Durchschnitt. Kritische Regeln weisen den höchsten Wert auf. Optionale Regeln weisen für diesen Index die geringste Gewichtung auf.  

- **Management Insights-Gruppen:** Zeigt den Prozentsatz von Regeln in jeder Gruppe an.  

- **Management Insights-Priorität:** Zeigt den Prozentsatz von Regeln nach Priorität an.  

- **Alle Erkenntnisse:** Eine Tabelle der Einblicke, einschließlich der Priorität und des Zustands.  

![Screenshot vom Dashboard für die Einblicke in die Verwaltung](media/1357979-management-insights-dashboard.png)

Weitere Informationen finden Sie unter [Einblicke für die Verwaltung](../../servers/manage/management-insights.md).


### <a name="improvements-to-cmpivot"></a>Verbesserungen an CMPivot

<!--1359068-->
CMPivot umfasst die folgenden Verbesserungen:

- Speichern von **bevorzugten** Abfragen  

- Wählen Sie auf der Registerkarte mit der Zusammenfassung der Abfrage die Anzahl der ausgefallenen oder Offline-Geräte aus, und wählen Sie dann die Option **Sammlung erstellen** aus.

Weitere Informationen über zusätzliche Verbesserungen der Leistung und Problembehandlung bei CMPivot finden Sie unter [Improvements to scripts](#bkmk_scripts) (Verbesserungen bei Skripts).

Weitere Informationen zu CMPivot finden Sie unter [CMPivot](../../servers/manage/cmpivot.md).


### <a name="improvements-to-scripts"></a><a name="bkmk_scripts"></a> Verbesserungen an Skripts

<!--1358239-->
Sie können die ausführliche Skriptausgabe jetzt im nicht formatierten Format oder strukturierten JSON-Format anzeigen. Diese Formatierung vereinfacht das Lesen und Analysieren der Ausgabe.

Die folgenden Verbesserungen an der Leistung und Problembehandlung gelten sowohl für CMPivot als auch für Skripts:

- Aktualisierte Clients geben eine Ausgabe von weniger als 80 KB über einen schnellen Kommunikationskanal an den Standort zurück. Durch diese Änderung wird die Leistung vom Anzeigen des Skripts und Abfragen der Ausgabe verbessert.  

- Zusätzliche Protokolle für die Problembehandlung  

Weitere Informationen finden Sie in den folgenden Artikeln:  

- [Erstellen und Ausführen von PowerShell-Skripts über die Configuration Manager-Konsole](../../../apps/deploy-use/create-deploy-scripts.md)  

- [Problembehandlung bei CMPivot](../../servers/manage/cmpivot-tsg.md)


### <a name="sms-provider-api"></a>SMS-Anbieter-API

<!--3607711, fka 1321523-->
Der SMS-Anbieter bietet nun schreibgeschützten API-Interoperabilitätszugriff auf WMI über HTTPS, der als **Verwaltungsdienst** bezeichnet wird. Diese REST-API kann anstelle eines benutzerdefinierten Webdiensts verwendet werden, um auf Informationen vom Standort zuzugreifen.

Der **SMS-Anbieter** wird als Rolle angezeigt, über die Sie die Kommunikation über Cloud Management Gateway zulassen können. Mit dieser Einstellung können Sie aktuell Genehmigungen von Anwendungen über E-Mail von einem Remotegerät aus zulassen.

Weitere Informationen finden Sie unter [Planen des SMS-Anbieters](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service).



## <a name="on-premises-mdm"></a><a name="bkmk_opmdm"></a> Lokale Verwaltung mobiler Geräte

### <a name="an-intune-connection-is-no-longer-required-for-new-on-premises-mdm-deployments"></a>Keine Intune-Verbindung mehr für neue lokale MDM-Bereitstellungen erforderlich

<!--1359124-->
Für die lokale MDM ist es nicht mehr erforderlich, bei neuen Bereitstellungen ein Microsoft Intune-Abonnement zu konfigurieren. Für Ihre Organisation sind weiterhin Intune-Lizenzen erforderlich, damit dieses Feature genutzt werden kann. Sie können derzeit die Intune-Verbindung nicht aus lokalen MDM-Bereitstellungen entfernen. Weitere Informationen finden Sie im [Blogbeitrag des Intune-Supports](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).



## <a name="other-updates"></a>Weitere Updates

Neben neuen Features umfasst dieses Release auch weitere Änderungen, beispielsweise Fehlerbehebungen. Weitere Informationen finden Sie unter [Zusammenfassung der Änderungen im aktuellen Current Branch von System Center Configuration Manager-Version 1810](https://support.microsoft.com/help/4482169).

Weitere Informationen zu Änderungen der Windows PowerShell-Cmdlets für Configuration Manager finden Sie in den [Versionshinweisen zu PowerShell 1810](https://docs.microsoft.com/powershell/sccm/1810-release-notes?view=sccm-ps).

Folgender Updaterollup (4488598) ist ab dem 25. März 2019 in der Konsole verfügbar: [Update rollup 2 for Configuration Manager current branch, version 1810 (Updaterollup 2 für die Current Branch-Version 1810 von Configuration Manager)](https://support.microsoft.com/help/4488598). Dadurch wird das vorherige Updaterollup, KB 4486457, ersetzt.


### <a name="hotfixes"></a>Hotfixes

Folgende zusätzliche Hotfixes wurden veröffentlicht, um bestimmte Probleme zu beheben:

| ID | Titel | Datum | In der Konsole |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Das Microsoft Intune-Connectorzertifikat wird nicht in Configuration Manager erneuert | 18. Januar 2019 | Ja |
| [4490434](https://support.microsoft.com/help/4490434) | In Configuration Manager werden doppelte Benutzerermittlungsspalten erstellt. | 22. Februar 2019 | Ja |
| [4490575](https://support.microsoft.com/help/4490575) | In Configuration Manager Version 1810 reagieren Updateinstallationen nicht mehr oder werden nie als abgeschlossen angezeigt. | 22. Februar 2019 | Ja |


## <a name="next-steps"></a>Nächste Schritte

Wenn Sie zum Installieren dieser Version bereit sind, finden Sie weitere Informationen unter [Updates und Wartung für Configuration Manager](../../servers/manage/updates.md) und in der [Checkliste für die Installation von Update 1810](../../servers/manage/checklist-for-installing-update-1810.md).

> [!TIP]  
> Verwenden Sie eine Baselineversion von Configuration Manager, um einen neuen Standort zu installieren.  
>
> Weitere Informationen:
>
> - [Installieren von neuen Standorten](../../servers/deploy/install/installing-sites.md)  
> - [Baseline- und Updateversionen](../../servers/manage/updates.md#bkmk_Baselines)  

Informationen zu bekannten, erheblichen Problemen finden Sie in den [Versionshinweisen](../../servers/deploy/install/release-notes.md).

Nachdem Sie einen Standort aktualisiert haben, überprüfen Sie auch die [Checkliste für Aufgaben nach dem Update](../../servers/manage/checklist-for-installing-update-1810.md#post-update-checklist).
