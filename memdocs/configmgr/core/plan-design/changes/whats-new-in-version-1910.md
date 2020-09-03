---
title: Neuerungen in Version 1910
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über Änderungen und neue Funktionen, die in Version 1910 des Current Branchs von Configuration Manager eingeführt wurden.
ms.date: 01/22/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3e1ddb65-1193-46ce-a7c0-a48dfd9fd833
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3c99716070bf32ae27a7bd8b7a114d8b920814e2
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993470"
---
# <a name="whats-new-in-version-1910-of-configuration-manager-current-branch"></a>Neuerungen in Version 1910 von Configuration Manager (Current Branch)

*Gilt für: Configuration Manager (Current Branch)*

Das Update 1910 für Configuration Manager (Current Branch) ist als konsoleninternes Update verfügbar. Wenden Sie dieses Update auf Standorte an, an denen Version 1806 oder höher ausgeführt wird. <!-- baseline only statement:When installing a new site, it's also available as a baseline version.--> In diesem Artikel werden die Änderungen und neuen Features in Configuration Manager Version 1910 zusammengefasst.

Überprüfen Sie stets die neueste Checkliste für die Installation dieses Updates. Weitere Informationen finden Sie in der [Checkliste für die Installation von Update 1910](../../servers/manage/checklist-for-installing-update-1910.md). Nachdem Sie einen Standort aktualisiert haben, überprüfen Sie auch die [Checkliste für Aufgaben nach dem Update](../../servers/manage/checklist-for-installing-update-1910.md#post-update-checklist).

Wenn Sie die neuen Configuration Manager-Features nach der Aktualisierung des Standorts vollständig nutzen möchten, müssen Sie auch Clients auf die neueste Version aktualisieren. Beim Update des Standorts und der Konsole werden neue Features in der Configuration Manager-Konsole angezeigt. Das vollständige Szenario ist allerdings erst einsatzbereit, wenn auch die Clientversion aktualisiert wird.

> [!TIP]
> Um bei einer Aktualisierung dieser Seite benachrichtigt zu werden, kopieren Sie die folgende URL, und fügen Sie sie in Ihren RSS-Feedreader ein: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1910+-+Configuration+Manager%22&locale=en-us`

## <a name="microsoft-endpoint-configuration-manager"></a><a name="bkmk_mem"></a> Microsoft Endpoint Configuration Manager

<!--4960084-->

Configuration Manager ist jetzt Bestandteil von Microsoft Endpoint Manager.

![Microsoft Endpoint Configuration Manager](media/4960084-endpoint-manager-logo.png)

Microsoft Endpoint Manager ist eine integrierte Lösung für die Verwaltung all Ihrer Geräte. Microsoft vereint Configuration Manager und Intune mit vereinfachter Lizenzierung. Nutzen Sie weiterhin ihre bestehenden Investitionen in Configuration Manager, und profitieren Sie von der Leistungsfähigkeit der Microsoft-Cloud nach Ihren Vorgaben.

Die folgenden Microsoft-Verwaltungslösungen sind nun unter dem Namen Microsoft Endpoint Manager vereint:

- [Configuration Manager](/configmgr)
- [Intune](/intune)
- [Desktop Analytics](../../../desktop-analytics/overview.md)
- [Autopilot](/intune/enrollment/enrollment-autopilot)
- Weitere Features in der [Verwaltungskonsole für die Geräteverwaltung](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/microsoft-intune-rolls-out-an-improved-streamlined-endpoint/ba-p/937760)

Weitere Informationen finden Sie in den folgenden Beiträgen von Brad Anderson, Microsoft Corporate Vice President für Microsoft 365:

- [Ankündigungs-Blogbeitrag](https://aka.ms/cmannounce)
- [Artikel zur Vision](https://aka.ms/MEMVisionPaper)
- [Video mit einer Zusammenfassung der Ankündigung](https://youtu.be/GS7oNPInFuw)

### <a name="what-things-change-in-configuration-manager-with-microsoft-endpoint-manager"></a>Welche Änderungen gibt es in Configuration Manager mit Microsoft Endpoint Manager?

Abgesehen von der Namensänderung funktioniert Configuration Manager in Version 1910 weiterhin gleich. Einige der Namensänderungen haben möglicherweise Auswirkungen auf die Verwendung der folgenden Komponenten:

- **Configuration Manager-Konsole**: Suchen Sie im Windows-Startmenü im Ordner **Microsoft Endpoint Manager** nach Verknüpfungen zur Konsole und dem **Remotesteuerungsviewer**.

- **Softwarecenter**: Suchen Sie im Windows-Startmenü im Ordner **Microsoft Endpoint Manager** die Verknüpfung für das Software Center.

![Symbole für Microsoft Endpoint Manager im Startmenü](media/microsoft-endpoint-manager-start-menu.png)

Stellen Sie sicher, dass Sie jede interne Dokumentation aktualisieren, die Sie beibehalten, um diese neuen Speicherorte einzuschließen.

> [!TIP]
> Wenn Sie in Windows 10 das Startmenü öffnen, geben Sie den Namen ein, um das Symbol zu suchen. Geben Sie beispielsweise `Configuration Manager` oder `Software Center` ein.

## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> Standortinfrastruktur

### <a name="reclaim-sedo-lock"></a>Freigeben der SEDO-Sperre

<!--4786915-->

Ab der [Current Branch-Version 1906](whats-new-in-version-1906.md#reclaim-sedo-lock-for-task-sequences) können Sie die Sperre für eine Tasksequenz löschen. Sie können jetzt die Sperre für ein beliebiges Objekt in der Configuration Manager-Konsole löschen.

Weitere Informationen finden Sie unter [Verwenden der Configuration Manager-Konsole](../../servers/manage/admin-console.md#bkmk_sedo).

### <a name="extend-and-migrate-on-premises-site-to-microsoft-azure"></a>Erweitern und Migrieren eines lokalen Standorts zu Microsoft Azure
<!--3556022-->

Dieses neue Tool unterstützt Sie dabei, Azure-VMs für Configuration Manager programmgesteuert zu erstellen. Es lässt sich mit Standortrollen mit Standardeinstellungen für passive Standortserver, Verwaltungspunkte und Verteilungspunkte installieren. Nachdem Sie die neuen Rollen überprüft haben, können Sie sie als zusätzliche Standortsysteme für Hochverfügbarkeit verwenden. Sie können auch die lokale Standortsystemrolle entfernen und nur die Azure-VM-Rolle beibehalten.

Weitere Informationen finden Sie unter [Erweitern und Migrieren eines lokalen Standorts zu Microsoft Azure](../../support/azure-migration-tool.md).

<!-- ## <a name="bkmk_cloud"></a> Cloud-attached management -->

## <a name="desktop-analytics"></a><a name="bkmk_da"></a> Desktop Analytics

Weitere Informationen zu den monatlichen Änderungen am Desktop Analytics-Clouddienst finden Sie unter [Neues in Desktop Analytics](../../../desktop-analytics/whats-new.md).

## <a name="real-time-management"></a><a name="bkmk_real"></a> Verwaltung in Echtzeit

### <a name="optimizations-to-the-cmpivot-engine"></a>Optimierungen der CMPivot-Engine
<!--3197353-->
Wir haben einige bedeutende Optimierungen der CMPivot-Engine durchgeführt. Sie können nun einen größeren Teil der Verarbeitung auf den ConfigMgr-Client übertragen. Die Optimierungen verringern die Netzwerk- und Server-CPU-Auslastung erheblich, die für die Durchführung von CMPivot-Abfragen benötigt wird. Mit diesen Optimierungen können Sie nun in Echtzeit Gigabytes von Clientdaten durchsehen. 

Weitere Informationen finden Sie unter [Optimierungen der CMPivot-Engine](../../servers/manage/cmpivot-changes.md#bkmk_optimization).

### <a name="additional-cmpivot-entities-and-enhancements"></a>Zusätzliche CMPivot-Entitäten und -Erweiterungen
<!--5410930-->
Wir haben eine Reihe neuer CMPivot-Entitäten und Entitätserweiterungen hinzugefügt, die bei der Problembehandlung und beim Hunting helfen. Wir haben die folgenden Entitäten für die Abfrage hinzugefügt:

- Windows-Ereignisprotokolle ([WinEvent](../../servers/manage/cmpivot-changes.md#bkmk_WinEvent))
- Dateiinhalt ([FileContent](../../servers/manage/cmpivot-changes.md#bkmk_File))
- Durch Prozesse geladene DLLs ([ProcessModule](../../servers/manage/cmpivot-changes.md#bkmk_ProcessModule))
- Azure Active Directory-Informationen ([AADStatus](../../servers/manage/cmpivot-changes.md#bkmk_AadStatus))
- Endpoint Protection-Status ([EPStatus](../../servers/manage/cmpivot-changes.md#bkmk_EPStatus))

Dieses Release umfasst auch zahlreiche [weitere Erweiterungen](../../servers/manage/cmpivot-changes.md#bkmk_Other) für CMPivot. Weitere Informationen finden Sie unter [CMPivot ab Version 1910](../../servers/manage/cmpivot-changes.md#bkmk_cmpivot1910).

## <a name="content-management"></a><a name="bkmk_content"></a> Content Management

### <a name="microsoft-connected-cache-support-for-intune-win32-apps"></a>Microsoft Connected Cache-Unterstützung für Intune Win32-Apps

<!--5032900-->

Wenn Sie Microsoft Connected Cache auf Ihren Configuration Manager-Verteilungspunkten aktivieren, können sie nun Microsoft Intune Win32-Apps für gemeinsam verwaltete Clients verarbeiten.

Weitere Informationen finden Sie unter [Microsoft Connected Cache in Configuration Manager](../hierarchy/microsoft-connected-cache.md#bkmk_intune).

> [!NOTE]
> Current Branch von Configuration Manager, Version 1906 enthält die [Übermittlungsoptimierung für den netzwerkinternen Cache](../hierarchy/microsoft-connected-cache.md), eine unter Windows Server installierte Anwendung, die sich noch in der Entwicklung befindet. Ab der Current Branch-Version 1910 wird dieses Feature als Microsoft Connected Cache bezeichnet.
>
> Wenn Sie Connected Cache auf einem Configuration Manager-Verteilungspunkt installieren, wird Datenverkehr der Übermittlungsoptimierung an lokale Quellen ausgelagert. Connected Cache erzielt dieses Verhalten durch effiziente Zwischenspeicherung von Inhalt auf Bytebereichsebene.

## <a name="client-management"></a><a name="bkmk_client"></a> Clientverwaltung

### <a name="include-custom-configuration-baselines-as-part-of-compliance-policy-assessment"></a>Einbeziehen benutzerdefinierter Konfigurationsbaselines im Rahmen der Konformitätsrichtlinienbewertung
<!--3608345-->

Sie können ab sofort die Auswertung benutzerdefinierter Konfigurationsbaselines als Regel für die Konformitätsrichtlinienbewertung hinzufügen. Wenn Sie eine Konfigurationsbaseline erstellen oder bearbeiten, können Sie nun die Option **Diese Baseline als Teil der Konformitätsrichtlinienbewertung auswerten** verwenden. Beim Hinzufügen oder Bearbeiten einer Konformitätsrichtlinienregel steht Ihnen eine Bedingung mit dem Namen **Konfigurierte Baselines in Konformitätsrichtlinienauswertung einbeziehen** zur Verfügung.

Bei gemeinsam verwalteten Geräten und wenn Sie Intune so konfigurieren, dass die Ergebnisse der Konformitätsbewertung von Configuration Manager als Teil des Gesamtkonformitätsstatus übernommen werden, werden diese Informationen an Azure Active Directory gesendet. Sie können diese dann für den bedingten Zugriff auf Ihre Microsoft 365-Ressourcen verwenden.

Weitere Informationen finden Sie unter [Einbeziehen benutzerdefinierter Konfigurationsbaselines im Rahmen der Konformitätsrichtlinienbewertung](../../../compliance/deploy-use/create-configuration-baselines.md#bkmk_CAbaselines).

### <a name="enable-user-policy-for-windows-10-enterprise-multi-session"></a>Aktivieren der Benutzerrichtlinie für mehrere Windows 10 Enterprise-Sitzungen

<!--4737447-->

In Current Branch-Version 1906 von Configuration Manager wurde Unterstützung für [Windows Virtual Desktop](../configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop)eingeführt. Diese Microsoft Azure-Umgebung unterstützt mehrere Betriebssystemversionen, von denen einige mehrere gleichzeitige aktive Benutzersitzungen zulassen. Eine dieser Betriebssystemversionen ist beispielsweise Windows 10 Enterprise mit mehreren Benutzersitzungen.

Wenn Sie für diese Geräte mit mehreren Sitzungen eine Benutzerrichtlinie benötigen und mögliche Auswirkungen auf die Leistung akzeptieren, können Sie jetzt eine Clienteinstellung konfigurieren, um die Benutzerrichtlinie zu aktivieren. Konfigurieren Sie in der Gruppe **Clientrichtlinie** die Einstellung **Benutzerrichtlinie für mehrere Benutzersitzungen aktivieren**.

Weitere Informationen finden Sie unter [Konfigurieren von Clienteinstellungen](../../clients/deploy/configure-client-settings.md).


<!-- ## <a name="bkmk_comgmt"></a> Co-management -->


## <a name="application-management"></a><a name="bkmk_app"></a> Anwendungsverwaltung

### <a name="deploy-microsoft-edge-version-77-and-later"></a>Bereitstellen von Microsoft Edge Version 77 und später
<!--4561024-->
Die brandneue Version von Microsoft Edge ist einsatzbereit. Sie können jetzt Microsoft Edge, Version 77 und höher, für Ihre Benutzer bereitstellen. Administratoren können den Betakanal (Beta Channel), den Entwicklerkanal (Dev Channel) oder den stabilen Kanal (Stable Channel) sowie eine Version des bereitzustellenden Microsoft Edge-Clients auswählen.

Weitere Informationen finden Sie unter [Bereitstellen von Microsoft Edge, Version 77 und höher](../../../apps/deploy-use/deploy-edge.md).

### <a name="improvements-to-application-groups"></a>Verbesserungen an Anwendungsgruppen

<!--4760058-->

Ab der Current Branch-Version 1906 können Sie eine Gruppe von Anwendungen erstellen, die Sie als einzelne Bereitstellung an eine Gerätesammlung senden können. Dieses Release verbessert dieses Feature:

- Benutzer können für die App-Gruppe im Softwarecenter die Option **Deinstallieren** auswählen.
- Sie können eine App-Gruppe für eine **Benutzersammlung** bereitstellen.

Allgemeinere Informationen finden Sie unter [Erstellen von Anwendungsgruppen](../../../apps/deploy-use/create-app-groups.md).


## <a name="os-deployment"></a><a name="bkmk_osd"></a> Bereitstellung des Betriebssystems

### <a name="improvements-to-the-task-sequence-editor"></a>Verbesserungen am Tasksequenz-Editors

 Der Tasksequenz-Editor umfasst die folgenden Verbesserungen:

- **Durchsuchen des Tasksequenz-Editors:**<!--4621085--> Wenn Sie über eine große Tasksequenz mit vielen Gruppen und Schritte verfügen, kann es schwierig sein, bestimmte Schritte zu finden. Sie können jetzt im Tasksequenz-Editor suchen. Dadurch können Sie Schritte in der Tasksequenz schneller finden.
- **Kopieren und Einfügen von Tasksequenzbedingungen:**<!--4621098--> Die Wiederverwendung der Bedingungen eines Tasksequenzschritts ist ab sofort in einem anderen Tasksequenzschritt möglich. Sie können die Bedingungen im Tasksequenz-Editor kopieren und einfügen.

Weitere Informationen finden Sie im neuen Artikel [Verwenden des Tasksequenz-Editors](../../../osd/understand/task-sequence-editor.md).

### <a name="task-sequence-performance-improvements-power-plans"></a>Leistungsverbesserungen bei der Tasksequenz: Energiesparpläne

<!--3555926-->

Sie können eine Tasksequenz jetzt mit dem Hochleistungsenergiesparplan ausführen. Diese Option verbessert die Gesamtgeschwindigkeit der Tasksequenz. Windows wird zur Verwendung des integrierten Hochleistungsenergiesparplans konfiguriert, der maximale Leistung auf Kosten eines höheren Energieverbrauchs bietet.

Weitere Informationen finden Sie unter [Leistungsverbesserungen für Energiesparpläne](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_perf).

### <a name="task-sequence-download-on-demand-over-the-internet"></a>Bedarfsbasiertes Herunterladen einer Tasksequenz über das Internet

<!--3601238-->

Sie können die Tasksequenz verwenden, um ein direktes Windows 10-Upgrade über Cloud Management Gateway (CMG) bereitzustellen. Für die Bereitstellung muss jedoch der gesamte Inhalt lokal heruntergeladen werden, bevor die Tasksequenz gestartet werden kann.

Ab diesem Release kann die Tasksequenz-Engine Pakete bei Bedarf von einem für Inhalte aktivierten CMG oder einem Cloudverteilungspunkt herunterladen. Diese Änderung bietet noch mehr Flexibilität für Bereitstellungen von direkten Windows 10-Upgrades auf internetbasierten Geräten.

Weitere Informationen finden Sie unter [Bereitstellen eines direkten Upgrades für Windows 10 über das CMG](../../../osd/deploy-use/deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg).

### <a name="improvements-to-os-deployment"></a>Verbesserungen bei der Bereitstellung von Betriebssystemen

Dieses Release umfasst die folgenden Verbesserungen für die Betriebssystembereitstellung:

#### <a name="boot-image-keyboard-layout"></a>Tastaturlayout des Startimages

<!--4910348-->

Konfigurieren Sie das Standardtastaturlayout für ein Startimage. Verwenden Sie auf der Registerkarte **Anpassung** für ein Startimage die neue Option **Standardtastaturlayout in WinPE festlegen**. Wenn Sie eine andere Sprache als „en-us“ auswählen, schließt Configuration Manager „en-us“ weiterhin in die verfügbaren Eingabegebietsschemas ein. Auf dem Gerät entspricht das anfängliche Tastaturlayout dem ausgewählten Gebietsschema, aber der Benutzer kann das Gerät bei Bedarf auf „en-us“ umstellen.

Weitere Informationen finden Sie unter [Verwalten von Startimages](../../../osd/get-started/manage-boot-images.md#customization).

#### <a name="import-a-single-index-of-an-os-upgrade-package"></a>Importieren eines einzelnen Indexes eines Betriebssystemupgradepakets

<!--4931110-->

Beim Importieren eines Pakets für ein Betriebssystemupgrade können Sie die Option **Bestimmten Image-Index aus Datei „install.wim“ des ausgewählten Upgradepakets extrahieren** verwenden. Dieses Verhalten ähnelt [Betriebssystemimages](../../../osd/get-started/manage-operating-system-images.md#BKMK_AddOSImages) mit der Ausnahme, dass die vorhandene Datei „install.wim“ im Paket für das Betriebssystemupgrade überschrieben wird. Der Image-Index wird an einen temporären Speicherort extrahiert und anschließend in das ursprüngliche Quellverzeichnis verschoben.

Weitere Informationen finden Sie unter [Verwalten von Betriebssystem-Upgradepaketen](../../../osd/get-started/manage-operating-system-upgrade-packages.md#BKMK_AddOSUpgradePkgs).

#### <a name="output-the-results-of-a-run-command-line-step-to-a-variable-during-a-task-sequence"></a>Ausgabe der Ergebnisse eines Schritts zur Befehlszeilenausführung in einer Variable während einer Tasksequenz

<!--user story 4977616/bug 4798352-->

Der Schritt **Befehlszeile ausführen** enthält jetzt die Option **Ausgabe an Tasksequenzvariable**. Wenn Sie diese Option aktivieren, speichert die Tasksequenz die Ausgabe des Befehls in einer von Ihnen angegebenen benutzerdefinierten Tasksequenzvariable.

Weitere Informationen finden Sie unter [Befehlszeile ausführen](../../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine).

#### <a name="improvements-to-task-sequence-debugger"></a>Verbesserungen am Tasksequenz-Debugger

Dieses Release umfasst die folgenden Verbesserungen am Tasksequenz-Debugger:

- Verwenden Sie die neue Tasksequenzvariable **TSDebugOnError**, um automatisch den Debugger zu starten, wenn die Tasksequenz einen Fehler zurückgibt.<!-- 5012536 -->
- Wenn Sie im Debugger einen Haltepunkt erstellen und die Tasksequenz den Computer neu startet, behält der Debugger den Haltepunkt nach dem Neustart bei.<!-- 5012509 -->

Weitere Informationen finden Sie unter [Tasksequenz-Debugger](../../../osd/deploy-use/debug-task-sequence.md) und [Tasksequenzvariablen – TSDebugOnError](../../../osd/understand/task-sequence-variables.md#TSDebugOnError).

#### <a name="improved-language-support-in-task-sequence"></a>Verbesserte Sprachunterstützung bei der Tasksequenz

<!--5411057, 5138936-->

Dieses neue Release erweitert die Steuerung der Sprachkonfiguration während der Bereitstellung des Betriebssystems. Wenn Sie diese Spracheinstellungen bereits anwenden, kann diese Änderung Ihnen helfen, Ihre Tasksequenz für die Betriebssystembereitstellung zu vereinfachen. Anstatt für jede Sprache mehrere Schritte oder separate Skripts auszuführen, verwenden Sie pro Sprache eine Instanz des integrierten Schritts **Windows-Einstellungen anwenden** mit einer Bedingung für die entsprechende Sprache.

Verwenden Sie den Tasksequenzschritt **Windows-Einstellungen anwenden**, um die folgenden neuen Einstellungen zu konfigurieren:

- Eingabegebietsschema (Standardtastaturlayout)
- Gebietsschema des Systems
- Sprache der Benutzeroberfläche
- Fallback für die Sprache der Benutzeroberfläche
- Gebietsschema des Benutzers

Weitere Informationen finden Sie unter [Windows-Einstellungen anwenden](../../../osd/understand/task-sequence-steps.md#BKMK_ApplyWindowsSettings).

#### <a name="new-variable-for-windows-10-in-place-upgrade"></a>Neue Variable für das direkte Windows 10-Upgrade

<!--4680263-->

Sie können jetzt eine neue Tasksequenzvariable **SetupCompletePause** festlegen, um Zeitsteuerungsprobleme mit der Tasksequenz für das direkte Upgrade von Window 10 auf Hochleistungsgeräten zu beheben, wenn das Windows-Setup abgeschlossen ist. Wenn Sie dieser Variablen einen Wert in Sekunden zuweisen, wartet der Windows-Setupvorgang diese Zeitspanne, bevor die Tasksequenz gestartet wird. Mit diesem Timeout erhält der Configuration Manager-Client zusätzliche Zeit für die Initialisierung.

Weitere Informationen finden Sie unter [Tasksequenzvariablen – SetupCompletePause](../../../osd/understand/task-sequence-variables.md#SetupCompletePause).

<!-- ## <a name="bkmk_userxp"></a> Software Center -->

## <a name="software-updates"></a><a name="bkmk_sum"></a> Softwareupdates

### <a name="additional-options-for-third-party-update-catalogs"></a>Zusätzliche Optionen für Drittanbieterupdatekataloge
<!--4469002-->
Sie verfügen nun über eine präzisere Steuerung über die Synchronisierung von Katalogen mit Updates von Drittanbietern. Ab Configuration Manager Version 1910 können Sie den Synchronisierungszeitplan für jeden Katalog unabhängig konfigurieren. Wenn Sie Kataloge verwenden, die kategorisierte Updates enthalten, können Sie die Synchronisierung so konfigurieren, dass nur bestimmte Updatekategorien eingeschlossen werden, um eine Synchronisierung des gesamten Katalogs zu vermeiden. Wenn Sie bei kategorisierten Katalogen sicher sind, dass Sie eine Kategorie bereitstellen werden, können Sie sie so konfigurieren, dass sie automatische heruntergeladen und in Windows Server Update Services (WSUS) veröffentlicht wird.

Weitere Informationen finden Sie unter [Aktivieren von Updates von Drittanbietern](../../../sum/deploy-use/third-party-software-updates.md#bkmk_1910).

### <a name="use-delivery-optimization-for-all-windows-updates"></a>Verwenden der Übermittlungsoptimierung für alle Windows-Updates
<!--4699118-->
Bisher konnten Sie die Übermittlungsoptimierung nur für Express-Updates verwenden. Mit Configuration Manager Version 1910 kann die Übermittlungsoptimierung jetzt zur Verteilung aller Windows Update-Inhalte für Clients verwendet werden, auf denen Windows 10, Version 1709 oder höher, ausgeführt wird.

Weitere Informationen finden Sie in folgenden Quellen:
- [Optimieren der Bereitstellung von Updates für Windows 10](../../../sum/deploy-use/optimize-windows-10-update-delivery.md#bkmk_DO-1910)
- [Clienteinstellungen für Softwareupdates](../../clients/deploy/about-client-settings.md#software-updates)
- [Clienteinstellungen für die Übermittlungsoptimierung](../../clients/deploy/about-client-settings.md#delivery-optimization)

### <a name="additional-software-update-filter-for-adrs"></a>Zusätzlicher Softwareupdatefilter für Regeln zur automatischen Bereitstellung
<!--4852033-->
Sie können **Bereitgestellt** jetzt als Updatefilter für die Regeln zur automatischen Bereitstellung verwenden. Mit diesem Filter können neue Updates identifiziert werden, die möglicherweise auf Ihre Pilot- oder Testsammlungen angewendet werden müssen.

Weitere Informationen finden Sie unter [Automatically deploy software updates (Automatisches Bereitstellen von Softwareupdates)](../../../sum/deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process).

## <a name="office-management"></a><a name="bkmk_o365"></a> Office-Verwaltung


### <a name="office-365-proplus-pilot-and-health-dashboard"></a>Office 365 ProPlus-Pilotprojekt und -Integritätsdashboard
<!--4488272, 4488301-->

Mit dem Office 365 ProPlus-Pilotprojekt und -Integritätsdashboard können Sie Office 365 ProPlus planen, testen und bereitstellen. Das Dashboard bietet Einblicke in die Integrität von Geräten mit Office 365 ProPlus, um mögliche Probleme zu identifizieren, die sich möglicherweise auf Ihre Bereitstellungspläne auswirken. Das Office 365 ProPlus-Pilotprojekt und -Integritätsdashboard bieten eine Empfehlung für Pilotgeräte, die auf einem Add-In-Bestand basieren.

Weitere Informationen finden Sie unter [Office 365 ProPlus-Dashboard „Pilot and Health“ (Pilot und Integrität)](../../../sum/deploy-use/office-365-dashboard.md#bkmk_pilot).

## <a name="protection"></a><a name="bkmk_protect"></a> Schutz

### <a name="bitlocker-management"></a>BitLocker-Verwaltung

<!--3601034-->

Configuration Manager bietet nun die folgenden Verwaltungsfunktionen für die BitLocker-Laufwerkverschlüsselung:

- Bereitstellen des BitLocker-Clients auf verwalteten Windows-Geräten
- Verwalten von Geräte-Verschlüsselungsrichtlinien
- Generieren von Konformitätsberichten
- Verwenden einer Website zur Verwaltung und Überwachung für die Schlüsselwiederherstellung
- Zugriff auf ein Self-Service-Portal für Benutzer

Weitere Informationen finden Sie unter [Planen der BitLocker-Verwaltung](../../../protect/plan-design/bitlocker-management.md).

## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Configuration Manager-Konsole

### <a name="view-active-consoles-and-message-administrators-through-console-connections"></a>Anzeigen von aktiven Konsolen und Senden von Nachrichten an Administratoren über Konsolenverbindungen
<!--4923997-->
Wir haben die folgenden Verbesserungen an **Konsolenverbindungen** vorgenommen:

- Die Möglichkeit, anderen Configuration Manager-Administratoren über Microsoft Teams Nachrichten zu senden
- Die Spalte **Zeitpunkt der letzten Verbindung** wurde durch die Spalte **Letzter Konsolentakt** ersetzt.
  - Eine geöffnete Konsole im Vordergrund sendet alle 10 Minuten einen Takt, um zu bestimmen, welche Konsolenverbindungen zurzeit aktiv sind.

Weitere Informationen finden Sie unter [Anzeigen kürzlich verbundener Konsolen](../../servers/manage/admin-console.md#bkmk_viewconnected) und [Senden von Nachrichten an Administratoren](../../servers/manage/admin-console.md#bkmk_message).

### <a name="client-diagnostics-actions"></a>Clientdiagnoseaktionen

<!--4433455-->

In der Configuration Manager-Konsole gibt es neue Geräteaktionen für die **Clientdiagnose**:

- **Aktivieren ausführlicher Protokollierung:** Ändern Sie die globale Protokollebene für die CCM-Komponente in *Ausführlich*, und aktivieren Sie die Debugprotokollierung.
- **Deaktivieren ausführlicher Protokollierung:** Ändern Sie die globale Protokollebene in *Standard*, und deaktivieren Sie die Debugprotokollierung.

Weitere Informationen finden Sie unter [Clientdiagnose](../../clients/manage/client-notification.md#client-diagnostics).

### <a name="improvements-to-console-search"></a>Verbesserungen bei der Konsolensuche
<!--4640570-->

Dieses Release umfasst folgende Verbesserungen bei der Suche in der Configuration Manager-Konsole:

- Sie können nun die Suchoption **Alle Unterordner** aus den Knoten **Treiberpakete** und **Abfragen** verwenden.<!--2841181,5424892-->
- Wenn eine Suche mehr als 1.000 Ergebnisse zurückgibt, wählen Sie **OK** in der Hinweisleiste aus, um weitere Ergebnisse anzuzeigen.<!--4640570-->

## <a name="other-updates"></a>Weitere Updates

Weitere Informationen zu Änderungen der Windows PowerShell-Cmdlets für Configuration Manager finden Sie in den [Versionshinweisen zu PowerShell 1910](/powershell/sccm/1910-release-notes?view=sccm-ps).

Weitere Informationen zu Änderungen an der Verwaltungsdienst-Rest-API finden Sie in den[Versionshinweisen zum Verwaltungsdienst](../../../develop/adminservice/release-notes.md#bkmk_1910).

Neben neuen Features umfasst dieses Release auch weitere Änderungen, beispielsweise Fehlerbehebungen. Weitere Informationen finden Sie unter [Zusammenfassung der Änderungen im Current Branch von Configuration Manager, Version 1910](https://support.microsoft.com/help/4535776).

<!--
As of this version, the following features are no longer pre-release:
- [SMS Provider administration service](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service)
- [Device Guard management](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md)
-->
Folgender Updaterollup (4537079) ist ab 18. Februar 2020 in der Konsole verfügbar: [Updaterollup für den aktuellen Branch von Microsoft Endpoint Configuration Manager, Version 1910](https://support.microsoft.com/help/4537079).



<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4552181](https://support.microsoft.com/help/4552181) | Content distribution stalls in Configuration Manager current branch, version 1910 | 16 March 2020 | No |
| [4552430](https://support.microsoft.com/help/4552430) | Third-party update category synchronization resets to default in Configuration Manager | 18 March 2020 | No |

> [!NOTE]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->

## <a name="next-steps"></a>Nächste Schritte

<!-- At this time, version 1910 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-1910.md#early-update-ring). -->
Ab dem 20. Dezember 2019 ist Version 1910 global für alle Kunden zur Installation verfügbar.

Wenn Sie zum Installieren dieser Version bereit sind, finden Sie weitere Informationen dazu unter [Installieren von Updates für Configuration Manager](../../servers/manage/updates.md) und [Checkliste für die Installation von Update 1910](../../servers/manage/checklist-for-installing-update-1910.md).

> [!TIP]
> Verwenden Sie eine Baselineversion von Configuration Manager, um einen neuen Standort zu installieren.
>
> Weitere Informationen:
>
> - [Installieren von neuen Standorten](../../servers/deploy/install/installing-sites.md) 
> - [Baseline- und Updateversionen](../../servers/manage/updates.md#bkmk_Baselines) 

Informationen zu bekannten, erheblichen Problemen finden Sie in den [Versionshinweisen](../../servers/deploy/install/release-notes.md).

Nachdem Sie einen Standort aktualisiert haben, überprüfen Sie auch die [Checkliste für Aufgaben nach dem Update](../../servers/manage/checklist-for-installing-update-1910.md#post-update-checklist).