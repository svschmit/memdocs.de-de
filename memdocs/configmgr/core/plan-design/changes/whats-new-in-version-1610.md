---
title: Neues in Version 1610
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über Änderungen und neue Funktionen, die in Version 1610 von Configuration Manager eingeführt wurden.
ms.date: 11/23/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f7eb0803-3f8f-4ab6-825a-99ac11f5ba7d
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 6589b2bd1308f214cce53ac65c806ad7edd51e5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701928"
---
# <a name="what39s-new-in-version-1610-of-configuration-manager"></a>Neuerungen in Version 1610 von Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Das Update 1610 für Configuration Manager (Current Branch) ist als konsoleninternes Update für zuvor installierte Standorte verfügbar, die Version 1511, 1602 oder 1606 ausführen.


> [!TIP]  
> Sie müssen eine Baselineversion von Configuration Manager verwenden, um einen neuen Standort zu installieren.  
>
> Weitere Informationen:    
> - [Installieren von neuen Standorten](https://technet.microsoft.com/library/mt590197.aspx)  
> - [Installieren von Updates an Standorten](https://technet.microsoft.com/library/mt607046.aspx)  
> - [Baseline- und Updateversionen](../../servers/manage/updates.md#bkmk_Baselines)

Die folgenden Abschnitte enthalten Details zu Änderungen und neue Funktionen, die in Version 1610 von Configuration Manager eingeführt wurden.  


## <a name="in-console-monitoring-of-update-installation-status"></a>Überwachung des Updateinstallationsstatus in der Konsole  
Ab Version 1610 gibt es eine neue Phase, wenn Sie ein Updatepaket installieren, und die Installation in der Konsole überwachen: **Post Installation** (Nach der Installation). Diese Phase enthält den Status für Aufgaben wie das Neustarten wichtiger Dienste und die Initialisierung der Replikationsüberwachung. (Diese Phase ist erst in der Konsole enthalten, wenn Ihr Standort auf Version 1610 aktualisiert wurde.) Weitere Informationen über den Updateinstallationsstatus finden Sie unter [Installieren konsoleninterner Updates](../../servers/manage/install-in-console-updates.md#bkmk_install).


## <a name="exclude-clients-from-automatic-upgrade"></a>Ausschließen von Clients von automatischen Upgrades
Sie können Windows-Clients von der Aktualisierung mit neuen Versionen der Clientsoftware ausschließen. Fügen Sie dafür Clientcomputer zu einer Sammlung hinzu, die von Upgrades ausgeschlossen wird. Clients in der ausgeschlossenen Sammlung ignorieren Anfragen zum Aktualisieren der Clientsoftware.  Weitere Informationen finden Sie unter [Exclude Windows clients from upgrades (Ausschließen von Windows-Clients von Upgrades)](../../clients/manage/upgrade/exclude-clients-windows.md).


## <a name="improvements-for-boundary-groups"></a>Verbesserungen für Begrenzungsgruppen
Version 1610 umfasst wichtige Änderungen an Begrenzungsgruppen und deren Zusammenarbeit mit Verteilungspunkten. Diese Änderungen können zur Vereinfachung des Entwurfs Ihrer Inhaltsinfrastruktur beitragen, wobei Sie mehr Kontrolle darüber erhalten, wie und wann ein Fallback der Clients erfolgt, um zusätzliche Verteilungspunkte als Quellspeicherorte für Inhalt zu suchen. Dies schließt sowohl lokale als auch cloudbasierte Verteilungspunkte ein.
Diese Verbesserungen ersetzen Konzepte und Verhaltensweisen, mit denen Sie möglicherweise vertraut sind (z.B. das Konfigurieren von Verteilungspunkten als schnell oder langsam). Das neue Modell ist einfacher einzurichten und zu verwalten. Diese Änderungen stellen auch die Grundlage für zukünftige Änderungen dar, die andere Standortsystemrollen verbessern, die Sie Begrenzungsgruppen zuordnen.

Wenn Sie eine Aktualisierung auf Version 1610 durchführen, konvertiert das Update Ihre aktuellen Begrenzungsgruppenkonfigurationen so, dass sie an das neue Modell angepasst ist, damit diese Änderungen Ihre bestehende Inhaltsverteilungskonfigurationen nicht stören.

Weitere Informationen finden Sie unter [Begrenzungsgruppen](../../servers/deploy/configure/boundary-groups.md).


## <a name="peer-cache-for-content-distribution-to-clients"></a>Peercache zur Verteilung von Inhalten an Clients
Ab Version 1610 unterstützt **Client-Peercache** Sie beim Verwalten von Bereitstellungen von Inhalten an Clients an Remotestandorten. Peercache ist eine integrierte Configuration Manager-Lösung für Clients, um Inhalte für andere Clients direkt aus ihrem lokalen Cache freizugeben.

Nachdem Sie Clienteinstellungen bereitgestellt haben, die Peercache für eine Sammlung aktivieren, können Mitglieder dieser Sammlung als Peerinhaltsquelle für andere Clients in der gleichen Begrenzungsgruppe fungieren.

Sie können auch das neue Dashboard **Clientdatenquellen** verwenden, um mehr über die Verwendung von Inhaltsquellen von Peercache in Ihrer Umgebung zu erfahren.

> [!TIP]  
> Peercache und das Dashboard „Clientdatenquellen“ sind vorab veröffentliche Features in Version 1610. Informationen zum Aktivieren dieser Funktionen finden Sie unter [Verwenden von vorab veröffentlichten Features von Updates](../../servers/manage/install-in-console-updates.md#bkmk_prerelease).

Weitere Informationen finden Sie unter [Peercache für Configuration Manager-Clients](../hierarchy/client-peer-cache.md) und [Dashboard „Clientdatenquellen“](../../servers/deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard).


## <a name="migrate-multiple-shared-distribution-points-at-the-same-time"></a>Gleichzeitiges Migrieren mehrerer freigegebener Verteilungspunkte
Sie können die Option jetzt verwenden, um **Verteilungspunkte neu zuzuweisen**, damit Configuration Manager die Neuzuweisung von bis zu 50 freigegebenen Verteilungspunkten parallel zur selben Zeit ausführen kann. Vor dieser Version wurden neu zugewiesene Punkte nacheinander verarbeitet. Weitere Informationen finden Sie unter [Migrate multiple shared distribution points at the same time (Gleichzeitiges Migrieren von mehreren freigegebenen Verteilungspunkten)](../../migration/planning-a-content-deployment-migration-strategy.md#migrate-multiple-shared-distribution-points-at-the-same-time).

## <a name="cloud-management-gateway-for-managing-internet-based-clients"></a>Cloudverwaltungsgateway zum Verwalten internetbasierter Clients

Das Cloudverwaltungsgateway bietet eine einfache Möglichkeit zum Verwalten von Configuration Manager-Clients im Internet. Der Cloudverwaltungsgateway-Dienst, der in Microsoft Azure bereitgestellt wird und ein Azure-Abonnement erfordert, stellt mithilfe einer neuen Rolle namens „cloud management gateway connection point“ (Verbindungspunkt für Cloudverwaltungsgateway) eine Verbindung mit Ihrer lokalen Configuration Manager-Infrastruktur her. Nachdem er bereitgestellt und konfiguriert wurde, können Clients mit lokalen Configuration Manager-Standortsystemrollen und cloudbasierten Verteilungspunkten kommunizieren, unabhängig davon, ob sie mit dem internen, dem privaten Netzwerk oder über das Internet verbunden sind. Weitere Informationen und einen Vergleich zwischen dem Cloudverwaltungsgateway und der internetbasierten Clientverwaltung finden Sie unter [Manage Clients on the Internet (Verwalten von Clients im Internet)](../../clients/manage/manage-clients-internet.md).

## <a name="improvements-to-the-windows-10-edition-upgrade-policy"></a>Verbesserungen an der Richtlinie für Windows 10-Editionsupgrades
In diesem Release wurden die folgenden Verbesserungen an diesem Richtlinientyp vorgenommen:

- Sie können nun die Richtlinie für Editionsupgrades mit Windows 10-PCs, die den Configuration Manager-Client ausführen, zusätzlich zu Windows 10-PCs verwenden, die in Microsoft Intune registriert sind.
- Sie können von Windows 10 Professional auf beliebige Plattformen im Assistenten aktualisieren, die mit Ihrer Hardware kompatibel sind.

## <a name="manage-hardware-identifiers"></a>Verwalten von Hardware-IDs
Sie können nun eine Liste der Hardware-IDs angeben, die Configuration Manager für den PXE-Start und die Clientregistrierung ignoriert. Es gibt zwei häufige Probleme, die dadurch behandelt werden können:

1. Viele Geräte wie Surface Pro 3 haben keinen integrierten Ethernet-Anschluss. Ein USB-zu-Ethernet-Adapter wird im Allgemeinen verwendet, um eine Kabelverbindung für die Bereitstellung eines Betriebssystems einzurichten. Allerdings handelt es sich hierbei aus Kostengründen und Gründen der allgemeinen Nutzbarkeit oft um gemeinsame Adapter. Nachdem die MAC-Adresse des Adapters zur Identifizierung des Geräts verwendet wird, ist es problematisch, den Adapter ohne zusätzliche Aktionen eines Administrators zwischen den Bereitstellungen wiederzuverwenden. Sie können nun in Configuration Manager, Version 1610, die MAC-Adresse dieses Adapters ausschließen, damit er in diesem Szenario einfach wiederverwendet werden kann.
2. Bei der SMBIOS-ID sollte es sich um eine eindeutige Hardware-ID handeln, aber einige spezielle Hardwaregeräte werden mit doppelten IDs gebaut. Dieses Problem tritt vielleicht nicht so häufig auf wie das zuvor beschriebene Szenario der USB-zu-Ethernet-Adapter, aber Sie können es mithilfe der Liste ausgeschlossener Hardware-IDs beheben.

Weitere Informationen finden Sie unter [Verwalten von in Konflikt stehenden Datensätzen bei Configuration Manager-Clients](../../clients/manage/manage-clients.md#manage-duplicate-hardware-identifiers).

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>Verbesserungen der Integration von Windows Store für Unternehmen in Configuration Manager
Änderungen in diesem Release:
- Bisher konnten nur kostenlose Apps aus dem Windows Store für Unternehmen bereitgestellt werden. Configuration Manager unterstützt darüber hinaus jetzt die Bereitstellung von kostenpflichtigen online-lizenzierten Apps (nur für Geräte, die bei Intune registriert sind).
- Sie können nun eine sofortige Synchronisierung zwischen Windows Store für Unternehmen und Configuration Manager einleiten.
- Sie können jetzt den geheimen Clientschlüssel ändern, den Sie von Azure Active Directory erhalten haben.
- Sie können ein Abonnement für den Store löschen.

Einzelheiten finden Sie unter [Verwalten von Apps aus dem Microsoft Store für Unternehmen mit Configuration Manager](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).


## <a name="policy-sync-for-intune-enrolled-devices"></a>Richtliniensynchronisierung bei Intune-registrierten Geräten
Sie können nun eine Richtliniensynchronisierung auf einem Intune-registrierten Gerät über die Configuration Manager-Konsole anfordern, anstatt die Synchronisierung in der Unternehmensportal-App auf dem Gerät selbst anzufordern. Informationen zum Status der Synchronisierungsanforderung stehen nun in Geräteansichten als neue Spalte **Remote Sync State** (Remotesynchronisierungsstatus) zur Verfügung. Die Informationen sind auch im Dialogfeld **Eigenschaften** für jedes Gerät im Abschnitt mit den Ermittlungsdaten verfügbar.


## <a name="use-compliance-settings-to-configure-windows-defender-settings"></a>Verwenden von Konformitätseinstellungen zum Konfigurieren von Windows Defender-Einstellungen
Sie können Windows Defender-Clienteinstellungen auf Intune-registrierten Windows 10-Computern mithilfe von Konfigurationselementen in der Configuration Manager-Konsole konfigurieren.
Einzelheiten finden Sie im Abschnitt **Windows Defender** unter [How to create configuration items for Windows 8.1 and Windows 10 devices managed without the Configuration Manager client (Erstellen von Konfigurationselementen für Windows 8.1- und Windows 10-Geräte, die ohne den Configuration Manager-Client verwaltet werden)](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).



## <a name="general-improvements-to-software-center"></a>Allgemeine Verbesserungen für Softwarecenter
- Benutzer können Apps jetzt aus dem Softwarecenter und dem Anwendungskatalog anfordern.
- Verbesserungen mit denen die Benutzer besser verstehen, welche Software neu und relevant ist.

## <a name="new-columns-in-device-collection-views"></a>Neue Spalten in Gerätesammlungsansichten
Sie können nun auch Spalten für **IMEI** und **Seriennummer** (bei iOS-Geräten) in Gerätesammlungsansichten anzeigen.

## <a name="customizable-branding-for-software-center-dialogs"></a>Anpassbares Branding für Software Center-Dialogfelder
Benutzerdefiniertes Branding für das Softwarecenter wurde in Configuration Manager-Version 1602 eingeführt. In Version 1610 wird dieses Branding jetzt auf alle zugehörigen Dialogfelder ausgeweitet, um eine konsistentere Erfahrung für Softwarecenter-Benutzer zu bieten.

Benutzerdefiniertes Branding für das Softwarecenter wird gemäß den folgenden Regeln angewendet:

- Wenn die Standortserverrolle „Anwendungskatalog-Websitepunkt“ nicht installiert ist, zeigt das Softwarecenter den Organisationsnamen an, der in der **Computer-Agent**-Clienteinstellung **Im Softwarecenter angezeigter Organisationsname** angegeben ist. Eine Anleitung hierzu finden Sie unter [Konfigurieren von Clienteinstellungen](../../clients/deploy/configure-client-settings.md).

- Wenn die Standortserverrolle „Anwendungskatalog-Websitepunkt“ installiert ist, zeigt das Softwarecenter den Organisationsnamen und die Farbe an, der bzw. die in den Eigenschaften der Standortserverrolle „Anwendungskatalog-Websitepunkt“ angegeben sind. Weitere Informationen finden Sie unter [Konfigurationsoptionen für den Anwendungskatalog-Websitepunkt](../../servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website).

- Wenn ein Microsoft Intune-Abonnement konfiguriert und mit der Configuration Manager-Umgebung verbunden ist, zeigt das Softwarecenter den Organisationsnamen, die Farbe und das Unternehmenslogo entsprechend den Angaben in den Eigenschaften des Intune-Abonnements an.


## <a name="enforcement-grace-period-for-required-application-and-software-update-deployments"></a>Erzwingung der Karenzzeit für erforderliche Anwendungen und Bereitstellungen von Softwareupdates
In einigen Fällen empfiehlt es sich, Benutzern über die von Ihnen angegebenen Fristen hinaus mehr Zeit zum Installieren von erforderlichen Anwendungsbereitstellungen oder Softwareupdates zu geben. Dies ist beispielsweise dann erforderlich, wenn ein Computer für einen längeren Zeitraum ausgeschaltet war und eine große Anzahl von Anwendungs- oder Updatebereitstellungen installiert werden muss. Wenn z.B. ein Endbenutzer gerade aus dem Urlaub zurückgekehrt ist, muss er möglicherweise sehr lange warten, bis überfällige Anwendungsbereitstellungen installiert werden. Sie können jetzt eine zwingende Toleranzperiode definieren, um dieses Problem zu lösen. Dafür müssen Sie die Configuration Manager-Clienteinstellungen für eine Sammlung bereitstellen. 

Führen Sie folgende Aktionen aus, um die Karenzzeit zu konfigurieren:
1. Auf der Seite **Computer-Agent** der Clienteinstellungen müssen Sie die neue Eigenschaft **Karenzzeit für Erzwingung nach Bereitstellungsfrist (Stunden)** mit einem Wert zwischen **1** und **120** Stunden konfigurieren.
2. Aktivieren Sie in einer neuen erforderlichen Anwendungsbereitstellung oder in den Eigenschaften einer vorhandenen Bereitstellung auf der Seite **Planung** das Kontrollkästchen **Erzwingung dieser Bereitstellung entsprechend den Benutzervoreinstellungen verzögern**, bis zu der Toleranzperiode, die in den Clienteinstellungen definiert ist. Alle Bereitstellungen, für die dieses Kontrollkästchen ausgewählt ist, und die für Geräte vorgesehen sind, für die Sie ebenfalls die Clienteinstellungen bereitgestellt haben, werden die Toleranzperiode verwenden.

Wenn Sie eine Toleranzperiode konfigurieren und das Kontrollkästchen aktivieren, wird die Anwendung im ersten, nicht geschäftlichen Fenster installiert werden, das der Benutzer nach Ablauf der Frist konfiguriert. Der Benutzer kann jedoch weiterhin das Software Center öffnen und die Anwendung zu einem beliebigen Zeitpunkt installieren. Nach Ablauf der Toleranzperiode wird die Erzwingung auf normales Verhalten für überfällige Bereitstellungen zurückgesetzt. Ähnliche Optionen wurden zum Bereitstellungsassistenten für Softwareupdates, zum Assistenten für automatische Bereitstellungsregeln und den Eigenschaftenseiten hinzugefügt.



## <a name="improved-functionality-in-dialog-boxes-about-required-software"></a>Verbesserte Funktionalität in Dialogfeldern zur erforderlichen Software
Wenn ein Benutzer erforderliche Software von der Einstellung **Warten und erinnern:** erhält, kann er sie aus der folgenden Dropdownliste von Werten auswählen: 
- **Später**. Gibt an, dass Benachrichtigungen basierend auf den in den Client-Agent-Einstellungen konfigurierten Benachrichtigungseinstellungen geplant sind.
- **Feste Zeit**. Gibt an, dass die Benachrichtigung nach der ausgewählten Zeit erneut angezeigt wird (beispielsweise in 30 Minuten).

![Computer-Agentseite in den Client-Agenteinstellungen](media/client-notification-settings.png)

Die maximale Erinnerungszeit basiert auf Benachrichtigungswerten, die in den Client-Agent-Einstellungen konfiguriert sind. Wenn zum Beispiel die Einstellung **Bereitstellungsstichtag in mehr als 24 Stunden, Benutzer erinnern alle (Stunden)** auf der Seite des Computer-Agents auf 10 Stunden festgelegt ist und es sind mehr als 24 Stunden bis zum Stichtag, erhält der Benutzer einen Satz an Warteoptionen von bis zu, aber nie mehr als 10 Stunden. Wenn sich der Stichtag nähert, stehen weniger Optionen zur Verfügung. Dies stimmt mit den entsprechenden Client-Agent-Einstellungen für jede Komponente der Bereitstellungszeit überein.

Darüber hinaus fällt bei Bereitstellungen mit hohem Risiko, z.B. einer Tasksequenz, die ein Betriebssystem bereitstellen, die Benachrichtigung des Benutzers deutlicher aus. Immer wenn der Benutzer benachrichtigt wird, dass eine kritische Softwarewartung erforderlich ist, wird anstatt einer vorübergehenden Benachrichtigung in der Taskleiste ein Dialogfeld wie das folgende auf dem Computer des Benutzers angezeigt:

![Erforderlicher Softwaredialog](media/client-toast-notification.png)


Weitere Informationen finden Sie unter:
- [Einstellungen zum Verwalten von Bereitstellungen mit hohem Risiko](../../servers/manage/settings-to-manage-high-risk-deployments.md)
- [Konfigurieren von Clienteinstellungen](../../clients/deploy/configure-client-settings.md)

## <a name="software-updates-dashboard"></a>Dashboard „Softwareupdatepunkt“
Verwenden Sie das neue Dashboard für Softwareupdates, um den aktuellen Kompatibilitätsstatus von Geräten in Ihrer Organisation anzuzeigen, und führen Sie eine schnelle Datenanalyse durch, um zu ermitteln, welche Geräte gefährdet sind. Navigieren Sie zum Anzeigen des Dashboards zu **Überwachung** > **Überblick** > **Sicherheit** > **Software Updates Dashboard** (Dashboard „Softwareupdatepunkt“).

Mehr Informationen finden Sie unter [Überwachen von Softwareupdates](../../../sum/deploy-use/monitor-software-updates.md).


## <a name="improvements-to-the-application-request-process"></a>Verbesserungen am Prozess der Anwendungsanforderung
Nachdem Sie eine Anwendung für die Installation genehmigt haben, können Sie anschließend auswählen, die Anforderung zu verweigern, indem Sie in der Configuration Manager-Konsole auf **Verweigern** klicken. Bisher war diese Schaltfläche nach der Genehmigung ausgegraut.

Diese Aktion bewirkt nicht, dass die Anwendung auf Geräten deinstalliert wird. Allerdings werden Benutzer daran gehindert, neue Kopien der Anwendung aus Softwarecenter zu installieren.

## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>Filtern nach Inhaltsgröße in automatischen Bereitstellungsregeln
Sie können jetzt nach Inhaltsgrößen für Softwareupdates in automatischen Bereitstellungsregeln filtern. Um nur Softwareupdates herunterzuladen, die kleiner als 2 MB sind, können Sie z.B. den Filter **Inhaltsgröße (KB)** auf **< 2048** festlegen. Mit diesem Filter wird verhindert, dass große Softwareupdates automatisch heruntergeladen werden. So wird die vereinfachte Windows-Wartung vorheriger Versionen unterstützt, wenn die Bandbreite eingeschränkt ist. Details hierzu finden Sie in den folgenden Abschnitten:
- [Configuration Manager and Simplified Windows Servicing on Down Level Operating Systems](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/) (Configuration Manager und vereinfachte Windows-Wartung auf vorherigen Betriebssystemen)
- [Automatisches Bereitstellen von Softwareupdates](../../../sum/deploy-use/automatically-deploy-software-updates.md)

Führen Sie einen der folgenden Schritte aus, um das Feld **Inhaltsgröße (KB)** zu konfigurieren:
- Wenn Sie eine Regel zur automatischen Bereitstellung erstellen, wechseln Sie im Assistenten zum Erstellen automatischer Bereitstellungsregeln auf die Seite **Softwareupdates**.
- Wechseln Sie in den Eigenschaften für eine vorhandene automatische Bereitstellungsregel zur Registerkarte **Softwareupdates**.

## <a name="office-365-client-management-dashboard"></a>Office 365-Clientverwaltungsdashboard
Das Office 365-Clientverwaltungsdashboard ist nun in der Configuration Manager-Konsole verfügbar. Wechseln Sie zu **Softwarebibliothek** > **Übersicht** > **Office 365 Client Management** (Office 365-Clientverwaltung), um das Dashboard anzuzeigen.

Das Dashboard zeigt Diagramme für Folgendes an:

- Anzahl der Office 365-Clients
- Office 365-Clientversionen
- Office 365-Clientsprachen
- Office 365-Clientkanäle     

Weitere Informationen finden Sie unter [Verwalten von Office 365 ProPlus-Updates](../../../sum/deploy-use/manage-office-365-proplus-updates.md).

## <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Tasksequenzschritte für das Verwalten einer Konvertierung von BIOS zu UEFI
Sie können eine Tasksequenz einer Betriebssystembereitstellung nun mit einer neuen Variable (TSUEFIDrive) so anpassen, dass durch den Schritt **Computer neu starten** auf der Festplatte eine FAT32-Partition für den Übergang zu UEFI vorbereitet wird. Das folgende Verfahren stellt ein Beispiel dar, wie Sie Tasksequenzschritte erstellen können, um die Festplatte auf die Konvertierung von BIOS zu UEFI vorzubereiten. Weitere Informationen finden Sie unter [Tasksequenzschritte für das Verwalten einer Konvertierung von BIOS zu UEFI](../../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md).

##  <a name="improvements-to-the-task-sequence-step-prepare-configmgr-client-for-capture"></a>Verbesserungen am Schritt zum Ausführen der Tasksequenz: Prepare ConfigMgr Client for Capture  
Im Schritt „Configuration Manager-Client vorbereiten“ wird der Configuration Manager-Client nun vollständig entfernt, und nicht nur die wichtigen Informationen. Wenn die Tasksequenz das erfasste Betriebssystemimage bereitstellt, wird jedes Mal ein neuer Configuration Manager-Client installiert. Weitere Informationen finden Sie unter [Tasksequenzschritte](../../../osd/understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture).



## <a name="intune-compliance-policy-charts"></a>Diagramme zu Intune-Konformitätsrichtlinien
Sie können jetzt eine schnelle Übersicht über die gesamte Gerätekonformität und die häufigsten Gründe für Nichtkonformität anzeigen, indem Sie die neuen Diagramme in der Configuration Manager-Konsole im Arbeitsbereich **Überwachung** verwenden. Klicken Sie auf einen Abschnitt im Diagramm, um einen Drilldown in einer Liste der Geräte in dieser Kategorie auszuführen. Weitere Informationen finden Sie unter [Überwachen der Konformitätsrichtlinie](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).


## <a name="lookout-integration-for-hybrid-implementations-to-protect-ios-and-android-devices"></a>Lookout-Integration für Hybridimplementierungen zum Schutz von iOS- und Android-Geräten
Microsoft ist mit der Lösung „Lookout Mobile Threat Protection“ zum Schutz von mobilen iOS- und Android-Geräten integriert. Mit dieser Lösung werden Schadsoftware, riskante Apps und weitere Risiken auf Geräten identifiziert. Die Lösung von Lookout unterstützt Sie beim Bestimmen der Bedrohungsstufe. Dies ist konfigurierbar. Sie können eine Konformitätsrichtlinienregel in Configuration Manager erstellen, um die Gerätekonformität basierend auf der Risikoeinschätzung durch Lookout einzuschätzen. Mithilfe bedingter Zugriffsrichtlinien können Sie den Zugriff auf Unternehmensressourcen basierend auf dem Konformitätsstatus des Geräts zulassen oder verweigern.

Benutzer nicht konformer iOS-Geräte werden zur Registrierung aufgefordert. Sie müssen die Lookout for Work-App auf ihren Geräten installieren, die App aktivieren und Bedrohungen entfernen, die in der Lookout for Work-Anwendung gemeldet werden, um Zugriff auf Unternehmensdaten zu erhalten.


## <a name="new-compliance-settings-for-configuration-items"></a>Neue Kompatibilitätseinstellungen für Konfigurationselemente
Es gibt viele neue Einstellungen, die Sie in Ihren Konfigurationselementen für verschiedene Geräteplattformen verwenden können. Dabei handelt es sich um Einstellungen, die zuvor in Microsoft Intune in einer eigenständigen Konfiguration vorhanden waren, und jetzt verfügbar sind, wenn Sie Intune mit Configuration Manager verwenden.
Weitere Informationen finden Sie unter [Konfigurationselemente für Geräte, die ohne den Configuration Manager-Client verwaltet werden](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).

### <a name="new-settings-for-android-devices"></a>Neue Einstellungen für Android-Geräte
#### <a name="password-settings"></a>Kennworteinstellungen
- **Kennwortverlauf speichern**
- **Fingerabdruckentsperrung zulassen**

#### <a name="security-settings"></a>Sicherheitseinstellungen
- **Verschlüsselung auf Speicherkarten vorschreiben**
- **Bildschirmaufnahme zulassen**
- **Übermitteln von Diagnosedaten zulassen**

#### <a name="browser-settings"></a>Browsereinstellungen
- **Webbrowser zulassen**
- **AutoAusfüllen zulassen**
- **Popupblocker zulassen**
- **Cookies zulassen**
- **Active Scripting zulassen**

#### <a name="app-settings"></a>App-Einstellungen
- **Google Play Store zulassen**

#### <a name="device-capability-settings"></a>Gerätefunktionseinstellungen
- **Wechselspeichermedien zulassen**
- **WLAN-Tethering zulassen**
- **Geolocation zulassen**
- **NFC zulassen**
- **Bluetooth zulassen**
- **Sprachroaming zulassen**
- **Datenroaming zulassen**
- **SMS/MMS-Messaging zulassen**
- **Sprach-Assistent zulassen**
- **Sprachwahl zulassen**
- **Kopieren und Einfügen zulassen**

### <a name="new-settings-for-ios-devices"></a>Neue Einstellungen für iOS-Geräte
#### <a name="password-settings"></a>Kennworteinstellungen
- **Erforderliche Anzahl komplexer Zeichen im Kennwort**
- **Einfache Kennwörter zulassen**
- **Minuten Inaktivität vor Anforderung des Kennworts**
- **Kennwortverlauf speichern**

### <a name="new-settings-for-mac-os-x-devices"></a>Neue Einstellungen für Mac OS X-Geräte
#### <a name="password-settings"></a>Kennworteinstellungen
- **Erforderliche Anzahl komplexer Zeichen im Kennwort**
- **Einfache Kennwörter zulassen**
- **Kennwortverlauf speichern**
- **Minuten Inaktivität bis zur Aktivierung des Bildschirmschoners**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>Neue Einstellungen für Windows 10 Desktop und mobile Geräte
#### <a name="password-settings"></a>Kennworteinstellungen
- **Minimale Anzahl von Zeichensätzen**
- **Kennwortverlauf speichern**
- **Kennworteingabe verlangen, wenn das Gerät aus dem Leerlauf zurückkehrt**

#### <a name="security-settings"></a>Sicherheitseinstellungen
- **Verschlüsselung auf mobilen Geräten vorschreiben**
- **Manuelle Aufhebung der Registrierung zulassen**

#### <a name="device-capability-settings"></a>Gerätefunktionseinstellungen
- **VPN über Mobilfunk zulassen**
- **VPN-Roaming über Mobilfunk zulassen**
- **Handyzurücksetzung zulassen**
- **USB-Verbindung zulassen**
- **Cortana zulassen**
- **Info-Center-Benachrichtigungen zulassen**

### <a name="new-settings-for-windows-10-team-devices"></a>Neue Einstellungen für Windows 10 Team-Geräte
#### <a name="device-settings"></a>Geräteeinstellungen
- **Azure Operational Insights aktivieren**
- **Miracast-Funkprojektion aktivieren**
- **Im Willkommensbildschirm angezeigte Besprechungsinformationen auswählen**
- **URL zum Bild für den Sperrbildschirmhintergrund**

### <a name="new-settings-for-windows-81-devices"></a>Neue Einstellungen für Windows 8.1-Geräte
#### <a name="applicability-settings"></a>Anwendbarkeitseinstellungen
- **Alle Konfigurationen auf Windows 10 anwenden**

#### <a name="password-settings"></a>Kennworteinstellungen
- **Erforderlicher Kennworttyp**
- **Minimale Anzahl von Zeichensätzen**
- **Minimale Kennwortlänge**
- **Anzahl der zulässigen wiederholten Anmeldefehler, bevor die Gerätedaten zurückgesetzt werden**
- **Inaktivität in Minuten bis zur Abschaltung des Bildschirms**
- **Kennwortablauf (Tage)**
- **Kennwortverlauf speichern**
- **Wiederverwendung vorheriger Kennwörter verhindern**
- **Bildkennwort und PIN zulassen**

#### <a name="browser-settings"></a>Browsereinstellungen
- **Automatische Erkennung des Intranets zulassen**

### <a name="new-settings-for-windows-phone-81-devices"></a>Neue Einstellungen für Windows Phone 8.1-Geräte
#### <a name="applicability-settings"></a>Anwendbarkeitseinstellungen
- **Alle Konfigurationen auf Windows 10 anwenden**

#### <a name="password-settings"></a>Kennworteinstellungen
- **Minimale Anzahl von Zeichensätzen**
- **Einfache Kennwörter zulassen**
- **Kennwortverlauf speichern**

#### <a name="device-capability-settings"></a>Gerätefunktionseinstellungen
- **Automatische Verbindung mit freien WLAN-Hotspots zulassen**
