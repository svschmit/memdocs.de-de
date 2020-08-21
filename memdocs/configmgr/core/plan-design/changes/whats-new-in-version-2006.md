---
title: Neuerungen in Version 2006
titleSuffix: Configuration Manager
description: Hier erfahren Sie mehr über Änderungen und neue Funktionen, die in Version 2006 des Current Branchs von Configuration Manager eingeführt wurden.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4b071746-61e1-404b-8053-60978de028a7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f624a207b5e9afded9b86312d1608a35005355f6
ms.sourcegitcommit: d1bfd5b8481439babc7eae43493f28edaebe647a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/13/2020
ms.locfileid: "88179340"
---
# <a name="whats-new-in-version-2006-of-configuration-manager-current-branch"></a>Neuerungen in Version 2006 von Configuration Manager (Current Branch)

*Gilt für: Configuration Manager (Current Branch)*

Das Update 2006 für Configuration Manager (Current Branch) ist als konsoleninternes Update verfügbar. Wenden Sie dieses Update auf Standorte an, an denen Version 1810 oder höher ausgeführt wird. <!-- baseline only statement:When installing a new site, it's also available as a baseline version. -->In diesem Artikel werden die Änderungen und neuen Features in Configuration Manager, Version 2006 zusammengefasst.

Überprüfen Sie stets die neueste Checkliste für die Installation dieses Updates. Weitere Informationen finden Sie in der [Checkliste für die Installation von Update 2006](../../servers/manage/checklist-for-installing-update-2006.md). Nachdem Sie einen Standort aktualisiert haben, überprüfen Sie auch die [Checkliste für Aufgaben nach dem Update](../../servers/manage/checklist-for-installing-update-2006.md#post-update-checklist).

Wenn Sie die neuen Configuration Manager-Features nach der Aktualisierung des Standorts vollständig nutzen möchten, müssen Sie auch Clients auf die neueste Version aktualisieren. Beim Update des Standorts und der Konsole werden neue Features in der Configuration Manager-Konsole angezeigt. Das vollständige Szenario ist allerdings erst einsatzbereit, wenn auch die Clientversion aktualisiert wird.

<!-- commenting this for now as it doesn't work 7422960
> [!TIP]
> To get notified when this page is updated, copy and paste the following URL into your RSS feed reader:
> `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+2006+-+Configuration+Manager%22&locale=en-us`
 -->

## <a name="microsoft-endpoint-manager-tenant-attach"></a><a name="bkmk_tenant"></a> Anfügen von Mandanten in Microsoft Endpoint Manager

### <a name="install-applications-from-the-admin-center"></a>Installieren von Anwendungen über das Admin Center
<!--7518897, 6024389-->
Sie können über das Admin Center von Microsoft Endpoint Manager eine Anwendungsinstallation in Echtzeit für ein Gerät mit Mandantenanfügung einleiten. Ab Configuration Manager-Version 2006 umfasst die Liste der für das Gerät verfügbaren Anwendungen auch Anwendungen, die für den gegenwärtig angemeldeten Benutzer des Geräts bereitgestellt werden. Weitere Informationen finden Sie unter [Anfügen von Mandanten: Installieren einer Anwendung über das Admin Center](../../../tenant-attach/applications.md).  

### <a name="import-previously-created-azure-ad-application-during-tenant-attach-onboarding"></a> Zuvor erstellte Azure AD-Anwendung beim Onboarding in die Mandantenanfügung importieren
<!--6479246-->
Bei einem neuen Onboarding kann ein Administrator beim Onboarding in die Mandantenanfügung eine zuvor erstellte Anwendung angeben. Weitere Informationen finden Sie unter [Anfügen von Mandanten in Microsoft Endpoint Manager: Gerätesynchronisierung und Geräteaktionen](../../../tenant-attach/device-sync-actions.md#bkmk_aad_app).

## <a name="endpoint-analytics"></a><a name="bkmk_ea"></a> Endpunktanalyse

### <a name="endpoint-analytics-data-collection-enabled-by-default"></a>„Datensammlung für Endpunktanalyse aktivieren“ standardmäßig aktiviert
<!--7065447, 7741111-->
Die Clienteinstellung **Datensammlung für Endpunktanalyse aktivieren** ist nun standardmäßig aktiviert. Diese Einstellung ermöglicht Ihren verwalteten Endpunkten das Senden von Daten, z. B. von Einblicken in die Startleistung, an Ihren Configuration Manager-Standortserver. Diese Änderung wirkt sich nur auf die lokale Datensammlung aus. Endpunktanalysedaten werden erst dann in das Admin Center von Microsoft Endpoint Manager hochgeladen, nachdem Sie [den Datenupload in Configuration Manager aktiviert haben](../../../../analytics/enroll-configmgr.md#bkmk_cm_upload). Der neue Standardwert gilt für die Standardclienteinstellungen und alle benutzerdefinierten Clienteinstellungen, die nach Upgrade auf Version 2006 erstellt wurden.

- Bei einem Upgrade von Version 2002 auf Version 2006 werden in den benutzerdefinierten Clienteinstellungen vorhandene Werte beibehalten. Der Standardwert für **Datensammlung für Endpunktanalyse aktivieren** in der Configuration Manager-Version 2002 ist **Nein**.
- Beim Upgrade von der Configuration Manager-Version 1910 oder früher auf Version 2006 übernehmen alle bereits vorhandenen benutzerdefinierten Clienteinstellungen, die die Einstellungsgruppe **Computer-Agent** enthalten, für  **Aktivieren der Endpunktanalyse-Datensammlung** die neue Standardeinstellung **Ja**.

Weitere Informationen finden Sie unter [Aktivieren der Datensammlung für Endpunktanalyse in Configuration Manager](../../../../analytics/enroll-configmgr.md#bkmk_cm_upload).

## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> Standortinfrastruktur

### <a name="vpn-boundary-type"></a> VPN-Begrenzungstyp

<!--7020519-->

Um die Verwaltung von Remoteclients zu vereinfachen, können Sie nun einen neuen Begrenzungstyp für VPNs erstellen. Zuvor mussten Sie auf der Grundlage der IP-Adresse oder des Subnetzes Begrenzungen für VPN-Clients erstellen. Diese Konfiguration konnte aufgrund der Subnetzkonfiguration oder des VPN-Entwurfs schwierig oder nicht möglich sein.

Wenn ein Client nun eine Standortanforderung sendet, enthält er zusätzliche Informationen über die Netzwerkkonfiguration. Basierend auf diesen Informationen bestimmt der Server, ob sich der Client in einem VPN befindet.

Weitere Informationen finden Sie unter [Definieren von Grenzen](../../servers/deploy/configure/boundaries.md).

### <a name="management-insights-to-optimize-for-remote-workers"></a>Management Insights zur Optimierung für Remoteworker

<!--6982226-->

Diese Version bietet eine neue Gruppe von Verwaltungserkenntnissen, nämlich **Optimierung für Remoteworker**. Diese Einblicke können Ihnen helfen, bessere Funktionen für Remoteworker bereitzustellen und die Last Ihrer Infrastruktur zu verringern. Die Einblicke in dieser Version konzentrieren sich hauptsächlich auf VPN:

- **VPN-Begrenzungsgruppen definieren**
- **Mit dem VPN verbundene Clients für das Vorziehen cloudbasierter Inhaltsquellen konfigurieren**
- **Peer-to-Peer-Inhaltsfreigabe für mit dem VPN verbundene Clients deaktivieren**

Weitere Informationen finden Sie unter [Einblicke für die Verwaltung](../../servers/manage/management-insights.md).

### <a name="improved-support-for-windows-virtual-desktop"></a> Verbesserte Unterstützung für Windows Virtual Desktop

<!--6527576-->

Die Plattform **Windows 10 Enterprise Multi-Session** ist in der Liste unterstützter Betriebssystemversionen für Objekte mit Anforderungsregeln oder Anwendungslisten verfügbar.

Weitere Informationen zur Unterstützung von Configuration Manager für Windows Virtual Desktop finden Sie unter [Unterstützte Betriebssystemversionen für Clients und Geräte](../configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop).

### <a name="intranet-clients-can-use-a-cmg-software-update-point"></a>Intranetclients können einen CMG-Softwareupdatepunkt verwenden
<!--7102873-->
Intranetclients können jetzt auf einen CMG-Softwareupdatepunkt zugreifen, wenn er einer Begrenzungsgruppe zugewiesen ist. Weitere Informationen finden Sie unter [Configure boundary groups](../../servers/deploy/configure/boundary-groups.md#bkmk_cmg-sup) (Konfigurieren von Begrenzungsgruppen).

## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a> Cloudgestützte Verwaltung

### <a name="use-microsoft-azure-china-21vianet-for-co-management"></a>Verwenden von Microsoft Azure China 21ViaNet für die Co-Verwaltung
<!--7133238-->
Sie können jetzt die Azure China-Cloud als Ihre Azure-Umgebung auswählen, wenn die Co-Verwaltung aktiviert wird. Weitere Informationen finden Sie unter [Aktivieren der Co-Verwaltung](../../../comanage/how-to-enable.md).

### <a name="notification-for-azure-ad-app-secret-key-expiration"></a>Benachrichtigung über den Ablauf des geheimen Schlüssels der Azure AD-App

<!--6386392-->

Wenn Sie Azure-Dienste zum Einbinden Ihres Standorts in die Cloud konfigurieren, werden in der Configuration Manager-Konsole jetzt Benachrichtigungen für die folgenden Umstände angezeigt:

- Mindestens ein geheimer Azure AD-Schlüssel für die App läuft bald ab
- Mindestens ein geheimer Azure AD-Schlüssel für die App ist abgelaufen

Weitere Informationen finden Sie unter [Geheimen Schlüssel erneuern](../../servers/deploy/configure/azure-services-wizard.md#bkmk_renew).

### <a name="desktop-analytics"></a>Desktop Analytics

Weitere Informationen zu den monatlichen Änderungen am Desktop Analytics-Clouddienst finden Sie unter [Neues in Desktop Analytics](../../../desktop-analytics/whats-new.md).

#### <a name="change-to-diagnostic-data-labels"></a>Ändern der Bezeichnungen von Diagnosedaten

<!-- 7363467 -->

Zur besseren Abstimmung mit den Desktop Analytics-Anforderungen für Windows-Diagnosedaten haben diese Einstellungen neue Bezeichnungen:

| Version 2006 und höher | Version 2002 und früher |
|---------|---------|
| Erforderlich | Basic |
| Optional (begrenzt) | Erweitert (begrenzt) |
| – | Erweitert |
| Optional | Vollständig |

Wenn Sie zuvor Geräte auf der Ebene **Erweitert** konfiguriert haben, werden diese bei einem Upgrade auf Version 2006 auf **Optional (begrenzt)** zurückgesetzt. Dadurch werden weniger Daten an Microsoft gesendet. Diese Änderung sollte keine Auswirkungen auf die in Desktop Analytics angezeigten Informationen haben.

Weitere Informationen finden Sie unter [Aktivieren der Datenfreigabe für Desktop Analytics](../../../desktop-analytics/enable-data-sharing.md).

## <a name="real-time-management"></a><a name="bkmk_real"></a> Verwaltung in Echtzeit

### <a name="improvements-to-cmpivot"></a>Verbesserungen an CMPivot
<!--6518631-->
Die folgenden Verbesserungen wurden in CMPivot vorgenommen:

- CMPivot in der Konsole und eigenständiges CMPivot wurden zusammengeführt.
- Sie können CMPivot auf einem einzelnen oder mehreren Geräten ausführen, ohne eine Sammlung auswählen oder erstellen zu müssen.
- In den Ergebnissen der CMPivot-Abfrage können Sie ein einzelnes oder mehrere Geräte auswählen und dann eine separate CMPivot-Instanz starten, die auf Ihre Auswahl begrenzt ist.

Weitere Informationen finden Sie unter [CMPivot ab Version 2006](../../servers/manage/cmpivot-changes.md#bkmk_2006).

## <a name="client-management"></a><a name="bkmk_client"></a> Clientverwaltung

### <a name="install-and-upgrade-the-client-on-a-metered-connection"></a> Clientinstallation und -upgrade bei einer getakteten Verbindung

<!--6976145-->

Wenn das Gerät zuvor mit einem getakteten Netzwerk verbunden war, wurden keine neuen Clients installiert. Vorhandene Clients wurden nur aktualisiert, wenn Sie die gesamte Clientkommunikation zuließen. Geräte, die häufig Roaming in einem getakteten Netzwerk ausführen, wurden entweder nicht oder mit einer älteren Clientversion verwaltet. Ab dieser Version können Sie den Client installieren und aktualisieren, wenn Sie die Clienteinstellung **Clientkommunikation über getaktete Internetverbindungen** auf **Zulassen** oder **Begrenzen** festlegen. Mit dieser Einstellung können Sie dem Client erlauben, auf dem aktuellen Stand zu bleiben, aber dennoch die Clientkommunikation in einem getakteten Netzwerk zu verwalten.

Um das Verhalten für eine neue Clientinstallation zu definieren, gibt es einen neuen ccmsetup-Parameter **/AllowMetered**. Wenn Sie die Clientkommunikation über ein getaktetes Netzwerk für ccmsetup zulassen, werden die Inhalte heruntergeladen, beim Standort registriert und die anfängliche Richtlinie heruntergeladen. Jede weitere Clientkommunikation folgt der Konfiguration der Clienteinstellung aus dieser Richtlinie.

Weitere Informationen finden Sie in den folgenden Artikeln:

- [Informationen zu Clienteinstellungen](../../clients/deploy/about-client-settings.md#client-communication-on-metered-internet-connections)
- [Informationen zu Parametern und Eigenschaften für die Clientinstallation in Configuration Manager](../../clients/deploy/about-client-installation-properties.md#allowmetered)

### <a name="improvements-to-managing-device-restarts"></a>Verbesserungen beim Verwalten von Geräteneustarts

<!--3601213-->

Configuration Manager bietet zahlreiche Optionen zum Verwalten von Geräteneustarts und Neustartbenachrichtigungen. Sie können jetzt Clienteinstellungen konfigurieren, um einen automatischen Neustart von Geräten zu verhindern, wenn eine Bereitstellung dies erfordert. Diese Einstellung bietet Ihnen in besonderen Situationen mehr Kontrolle. Standardmäßig ist die Clienteinstellung **Configuration Manager kann einen Neustart des Geräts erzwingen** so aktiviert, dass Configuration Manager Geräte nach wie vor zum Neustart zwingen kann. Diese Einstellung gilt für alle Anwendungs-, Softwareupdate- und Paketbereitstellungen, die einen Neustart erfordern.

Weitere Informationen finden Sie unter [Benachrichtigungen zum Geräteneustart](../../clients/deploy/device-restart-notifications.md).

## <a name="application-management"></a><a name="bkmk_app"></a> Anwendungsverwaltung

### <a name="improvements-to-available-apps-via-cmg"></a>Verbesserungen an verfügbaren Apps über CMG

<!--6935376-->
Dieses Release behebt ein Problem mit dem Softwarecenter und der Azure Active Directory-Authentifizierung (Azure AD). Für einen Client, der als im Intranet befindlich erkannt wurde, aber über das Cloudverwaltungsgateway (Cloud Management Gateway, CMG) kommuniziert, verwendete das vorherige Softwarecenter die Windows-Authentifizierung. Beim Versuch, die Liste der für Benutzer verfügbaren Apps abzurufen, trat ein Fehler auf. Sie verwendet nun Azure AD-Identität (Azure Active Directory) für Geräte, die mit Azure AD verknüpft sind. Diese Geräte können mit der Cloud verbunden oder hybrid eingebunden sein.

Weitere Informationen finden Sie unter [Bereitstellen von für Benutzer verfügbaren Apps](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications).

### <a name="microsoft-365-apps-for-enterprise"></a>Microsoft 365 Apps for Enterprise
<!--6298093-->
Office 365 ProPlus wurde am 21. April 2020 in Microsoft 365 Apps for Enterprise umbenannt. Ab Version 2006 sind die folgenden Änderungen erfolgt:

- Die Configuration Manager-Konsole wurde aktualisiert, um den neuen Namen zu verwenden.
  - Diese Änderung schließt auch Updatekanalnamen für Microsoft 365-Apps ein.
- Eine Bannerbenachrichtigung wurde der Konsole hinzugefügt, um Ihnen mitzuteilen, dass mindestens eine Regel für die automatische Bereitstellung auf veraltete Kanalnamen in den **Titel**-Kriterien für Microsoft 365-Apps-Updates verweist.

Weitere Informationen finden Sie unter [Updatekanäle für Microsoft 365-Apps](../../../sum/deploy-use/manage-office-365-proplus-updates.md#bkmk_channel) und [Dashboard für die Upgradebereitschaft von Microsoft 365-Apps](../../../sum/deploy-use/office-365-dashboard.md#bkmk_readiness-dash).

## <a name="os-deployment"></a><a name="bkmk_osd"></a> Bereitstellung des Betriebssystems

### <a name="task-sequence-media-support-for-cloud-based-content"></a> Unterstützung von Tasksequenzmedien für cloudbasierten Inhalt

<!--6209223-->

Tasksequenzmedien können jetzt cloudbasierte Inhalte herunterladen. Sie können beispielsweise einen USB-Schlüssel an einen Benutzer in einer Zweigniederlassung senden, damit dieser ein Reimaging seines Geräts durchführen kann. Oder eine Filiale verfügt über einen lokalen PXE-Server, aber Sie möchten, dass Geräte nach Möglichkeit Clouddienste priorisieren. Anstatt das WAN weiterhin mit dem Download umfangreicher Inhalte für die Bereitstellung von Betriebssystemen zu belasten, können Startmedien und PXE-Bereitstellungen jetzt Inhalte aus cloudbasierten Quellen abrufen. Beispielsweise ein Cloudverwaltungsgateway (Cloud Management Gateway, CMG), das Sie zum Freigeben von Inhalten aktivieren.

> [!NOTE]
> Das Gerät benötigt weiterhin eine Intranetverbindung mit dem Verwaltungspunkt.

Weitere Informationen finden Sie unter [Verwenden startbarer Medien zum Bereitstellen von Windows über das Netzwerk](../../../osd/deploy-use/use-bootable-media-to-deploy-windows-over-the-network.md#support-for-cloud-based-content).

### <a name="improvements-to-task-sequences-via-cmg"></a> Verbesserungen an Tasksequenzen über CMG

Diese Version enthält die folgenden Verbesserungen zur Bereitstellung von Tasksequenzen für Geräte, die über Cloud Management Gateway (CMG) kommunizieren:

- Unterstützung der Betriebssystembereitstellung<!--6997525-->: Mit einer Tasksequenz, die ein Startimage verwendet, um ein Betriebssystem bereitzustellen, können Sie es auf einem Gerät bereitstellen, das über CMG kommuniziert. Der Benutzer muss die Tasksequenz in Software Center starten. Weitere Informationen finden Sie unter [Planen von Cloud Management Gateway in Configuration Manager: Spezifikationen](../../clients/manage/cmg/plan-cloud-management-gateway.md#specifications).

- In dieser Version wurden die beiden [bekannten Probleme](../../servers/deploy/install/release-notes.md#task-sequences-cant-run-over-cmg) in der Current Branch-Version 2002 von Configuration Manager behoben.<!-- 6983320 --> Sie können jetzt eine Tasksequenz auf einem Gerät ausführen, das über CMG unter den folgenden Voraussetzungen kommuniziert:

  - Ein Arbeitsgruppengerät, das Sie mit einem [Massenregistrierungstoken](../../clients/deploy/deploy-clients-cmg-token.md) registrieren

  - Sie konfigurieren den Standort für [Erweitertes HTTP](../hierarchy/enhanced-http.md), und der Verwaltungspunkt ist HTTP

### <a name="improvements-to-bitlocker-task-sequence-steps"></a>Verbesserungen bei BitLocker-Tasksequenzschritten

<!--6995601-->

Sie können jetzt den Modus für die Datenträgerverschlüsselung in den Tasksequenzschritten **BitLocker aktivieren** und **BitLocker vorab bereitstellen** angeben. Standardmäßig verwenden die Schritte weiterhin die Standardverschlüsselungsmethode für die Betriebssystemversion.

Der Schritt **BitLocker aktivieren** enthält jetzt auch die Einstellung **Diesen Schritt bei Computern überspringen, die nicht über ein TPM verfügen oder bei denen das TPM nicht aktiviert ist**. Wenn Sie diese Einstellung aktivieren, protokolliert der Schritt einen Fehler auf einem Gerät ohne TPM oder einem TPM, das nicht initialisiert wird, und die Tasksequenz wird fortgesetzt. Diese Einstellung erleichtert die Verwaltung des Tasksequenzverhaltens auf Geräten, die BitLocker nicht vollständig unterstützen können.

Weitere Informationen finden Sie unter [Tasksequenzschritte](../../../osd/understand/task-sequence-steps.md).

### <a name="management-insight-rules-for-os-deployment"></a>Regeln für Verwaltungserkenntnisse für die Betriebssystembereitstellung

<!--6982275-->

Wenn die Größe der Tasksequenzrichtlinie 32 MB überschreitet, kann die große Richtlinie vom Client nicht verarbeitet werden. Der Client kann dann die Tasksequenzbereitstellung nicht ausführen. Um Sie bei der Verwaltung der Richtliniengröße von Tasksequenzen zu unterstützen, enthält diese Version die folgenden Verwaltungserkenntnisse:

- **Große Tasksequenzen können zu einer Überschreitung der maximal zulässigen Richtliniengröße beitragen**

- **Die Gesamtgröße der Richtlinien für Tasksequenzen überschreitet den für Richtlinien zulässigen Höchstwert**

> [!TIP]
> Diese Regeln befinden sich in einer neuen Gruppe für die **Betriebssystembereitstellung**. Die vorhandene Regel für **Nicht verwendete Startimages** befindet sich nun ebenfalls in dieser Gruppe.

Weitere Informationen finden Sie unter [Verwaltungserkenntnisse](../../servers/manage/management-insights.md#operating-system-deployment).

### <a name="improvements-to-os-deployment"></a>Verbesserungen bei der Bereitstellung von Betriebssystemen

Diese Version umfasst die folgenden zusätzlichen Verbesserungen für die Betriebssystembereitstellung:

- Sie können mithilfe einer Tasksequenzvariablen das Ziel für den Schritt [Datenträger formatieren und partitionieren](../../../osd/understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk) angeben. Diese neue Variablenoption unterstützt komplexere Tasksequenzen mit dynamischem Verhalten. Beispielsweise kann ein benutzerdefiniertes Skript den Datenträger erkennen und die Variable auf Grundlage des Hardwaretyps festlegen. Anschließend können Sie mehrere Instanzen dieses Schritts verwenden, um verschiedene Hardwaretypen und Partitionen zu konfigurieren.<!--6610288-->

- Der Schritt [Bereitschaft überprüfen](../../../osd/understand/task-sequence-steps.md#BKMK_CheckReadiness) umfasst jetzt eine Überprüfung, um zu bestimmen, ob das Gerät UEFI verwendet. Er enthält auch die neue schreibgeschützte Tasksequenzvariable **_TS_CRUEFI**.<!--6452769-->

- Wenn Sie das [Tasksequenz-Statusfenster](../../../osd/understand/user-experience.md#task-sequence-progress) aktivieren, um ausführlichere Statusinformationen anzuzeigen, zählt es jetzt nicht aktivierte Schritte in einer deaktivierten Gruppe. Durch diese Änderung wird die Fortschrittsschätzung genauer.<!--6448412-->

- Zuvor wurde während einer Tasksequenz zum Upgrade eines Geräts auf Windows 10 während einer der letzten Windows-Konfigurationsphasen ein Eingabeaufforderungsfenster geöffnet. Das Fenster befand sich oben auf der Windows-Begrüßungsseite, und Benutzer konnten damit interagieren, ohne den Upgradevorgang zu unterbrechen. Nun enthalten die Configuration Manager-Skripts „SetupCompleteTemplate.cmd“ und „SetupRollbackTemplate.cmd“ eine Änderung, um dieses Eingabeaufforderungsfenster auszublenden.<!--2837795-->

- Einige Kunden erstellen benutzerdefinierte Tasksequenzschnittstellen mithilfe der Methode **IProgressUI::ShowMessage**, aber es wird kein Wert für die Antwort des Benutzers zurückgegeben. Dieser Version wurde die Methode [IProgressUI::ShowMessageEx](../../../develop/reference/core/clients/client-classes/iprogressui--showmessageex-method.md) hinzugefügt. Diese neue Methode ähnelt der vorhandenen Methode, umfasst aber auch eine neue ganzzahlige Ergebnisvariable, **pResult**.<!--6448458-->

## <a name="protection"></a>Schutz

### <a name="cmg-support-for-endpoint-protection-policies"></a>CMG-Unterstützung für Endpoint Protection-Richtlinien

<!--4773948-->

Wenngleich Cloud Management Gateway (CMG) Endpoint Protection-Richtlinien unterstützt hat, benötigten Geräte Zugriff auf lokale Domänencontroller. Ab dieser Version können Clients, die über ein CMG kommunizieren, Endpoint Protection-Richtlinien sofort anwenden, ohne dass eine aktive Verbindung mit Active Directory besteht.

Weitere Informationen finden Sie unter [Unterstützung für Configuration Manager-Features](../../clients/manage/cmg/plan-cloud-management-gateway.md#support-for-configuration-manager-features).

### <a name="bitlocker-management-support-for-hierarchies"></a>Unterstützung der BitLocker-Verwaltung für Hierarchien

<!-- 5925693 -->

Sie können nun das BitLocker-Self-Service-Portal und die Verwaltungs- und Überwachungswebsite am zentralen Verwaltungsstandort installieren.

Weitere Informationen finden Sie unter [Einrichten von BitLocker-Portalen](../../../protect/deploy-use/bitlocker/setup-websites.md).

## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Configuration Manager-Konsole

### <a name="community-hub-and-github"></a>Community Hub und GitHub
<!--3555935, 3555936, deep link included 4224406-->

*(Erstmals im Juni 2020 eingeführt)*

Die IT-Administratorcommunity hat im Laufe der Jahre einen großen Wissensschatz aufgebaut. Anstatt Elemente wie Skripts und Berichte von Grund auf neu zu erfinden, haben wir einen **Community Hub** für Configuration Manager aufgebaut, auf dem Sie sich untereinander austauschen können. Durch die Nutzung der Arbeit anderer können Sie Stunden an Arbeit sparen. Der Community Hub fördert Kreativität, indem er auf der Arbeit anderer aufbaut und andere auf Ihrer Arbeit aufbauen lässt. GitHub hat bereits branchenweite Prozesse und Tools für die gemeinsame Nutzung entwickelt. Jetzt nutzt der Community Hub diese Tools direkt in der Configuration Manager-Konsole als Grundlage für die Weiterentwicklung dieser neuen Community. Für das erste Release werden die Inhalte, die im Community-Hub verfügbar gemacht werden, nur von Microsoft hochgeladen. 

Weitere Informationen finden Sie unter [Community Hub und GitHub](../../servers/manage/community-hub.md).

### <a name="direct-links-to-community-hub-items"></a><a name="bkmk_deeplink"></a> Direkte Links zu Elementen im Community Hub
<!--4224406-->
Über einen direkten Link können Sie in der Configuration Manager-Konsole einfach zu Elementen im Knoten „Community Hub“ navigieren und auf sie verweisen. Weitere Informationen finden Sie unter [Direkte Links zu Elementen im Community Hub von Configuration Manager](../../servers/manage/community-hub.md#bkmk_deeplink).

### <a name="notifications-from-microsoft"></a>Benachrichtigungen von Microsoft
<!--3953121-->
Sie haben jetzt die Möglichkeit, Benachrichtigungen von Microsoft in der Configuration Manager-Konsole zu empfangen. Mithilfe dieser Benachrichtigungen bleiben Sie über neue oder aktualisierte Features, Änderungen an Configuration Manager und angefügte Dienste sowie Probleme, die Behebungsmaßnahmen erfordern, auf dem Laufenden.

Weitere Informationen finden Sie unter [Configure a site to receive messages from Microsoft](../../servers/manage/admin-console-notifications.md#bkmk_msft) (Konfigurieren eines Standorts zum Empfangen von Nachrichten von Microsoft).

### <a name="power-bi-sample-reports"></a>Power BI-Beispielberichte
<!--5679791-->

*(Erstmals im Juni 2020 eingeführt)*

Wenn Sie den Power BI-Berichtsserver in die Berichtserstellung von Configuration Manager integrieren, stehen Ihnen jetzt Beispiele für Power BI-Berichte zur Verfügung. Laden Sie folgenden Beispielberichte herunter, und installieren Sie sie:

- Status der Softwareupdatekonformität
- Status der Softwareupdatebereitstellung

Weitere Informationen finden Sie unter [Installieren von Power BI-Beispielberichten](../../servers/manage/powerbi-sample-reports.md).

<!-- Unused sections in this release:
## Reporting
## <a name="bkmk_userxp"></a> User experience
## <a name="bkmk_sum"></a> Software updates
## Office management
## <a name="bkmk_content"></a> Content management
## <a name="bkmk_comgmt"></a> Co-management
-->

## <a name="deprecated-operating-systems"></a><a name="bkmk_deprecated"></a> Veraltete Betriebssysteme

Erfahren Sie mehr zu Änderungen bei der Unterstützung, bevor sie in [entfernte und veraltete Elemente](deprecated/removed-and-deprecated.md) aufgenommen werden.

Wie erstmals in Version 1906 angekündigt, wird in Version 2006 die Unterstützung für die folgenden Versionen von Clientbetriebssystemen eingestellt:  

- Windows CE 7.0
- Windows 10 Mobile
- Windows 10 Mobile Enterprise

## <a name="other-updates"></a>Weitere Updates

<!--
Starting with this version, the following features are no longer [pre-release](../../servers/manage/pre-release-features.md):

### Azure Active Directory user group discovery](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco)<!--3611956
-->

Weitere Informationen zu Änderungen der Windows PowerShell-Cmdlets für Configuration Manager finden Sie in den [Versionshinweisen zu PowerShell Version 2006](https://docs.microsoft.com/powershell/sccm/2006-release-notes?view=sccm-ps).

Weitere Informationen zu Änderungen an der Verwaltungsdienst-Rest-API finden Sie in den[Versionshinweisen zum Verwaltungsdienst](../../../develop/adminservice/release-notes.md#bkmk_2006).

<!--
Aside from new features, this release also includes additional changes such as bug fixes. For more information, see [Summary of changes in Configuration Manager current branch, version 2006](https://support.microsoft.com/help/4556203).

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

Derzeit wird Version 2006 für den Early Update Ring freigegeben. Zum Installieren dieses Updates müssen Sie sich anmelden. Weitere Informationen finden Sie unter [Early Update Ring](../../servers/manage/checklist-for-installing-update-2006.md#early-update-ring).

<!-- As of May 11, 2020, version 2006 is globally available for all customers to install. -->

Wenn Sie zum Installieren dieser Version bereit sind, finden Sie dazu unter [Updates und Wartung für Configuration Manager](../../servers/manage/updates.md) und [Checkliste für die Installation von Update 2006](../../servers/manage/checklist-for-installing-update-2006.md) weitere Informationen.

> [!TIP]
> Verwenden Sie eine Baselineversion von Configuration Manager, um einen neuen Standort zu installieren.
>
> Weitere Informationen:
>
> - [Installieren von neuen Standorten](../../servers/deploy/install/installing-sites.md)
> - [Baseline- und Updateversionen](../../servers/manage/updates.md#bkmk_Baselines)

Informationen zu bekannten, erheblichen Problemen finden Sie in den [Versionshinweisen](../../servers/deploy/install/release-notes.md).

Nachdem Sie einen Standort aktualisiert haben, überprüfen Sie auch die [Checkliste für Aufgaben nach dem Update](../../servers/manage/checklist-for-installing-update-2006.md#post-update-checklist).
