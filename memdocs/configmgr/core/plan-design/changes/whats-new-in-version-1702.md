---
title: Neue Version 1702
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über Änderungen und neue Funktionen, die in Version 1702 von Configuration Manager eingeführt wurden.
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 409e26e1-7716-4f1d-a0ee-34feabf20792
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: a947b332addbc3404617abdbbe199ede4e74dc63
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692790"
---
# <a name="what39s-new-in-version-1702-of-configuration-manager"></a>Neuerungen in Version 1702 von Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Das Update 1702 für Configuration Manager (Current Branch) ist als konsoleninternes Update für zuvor installierte Standorte verfügbar, die Version 1602, 1606 oder 1610 ausführen. Es steht auch als eine Baselineversion zur Verfügung, die Sie beim Installieren einer neuen Bereitstellung verwenden können.

> [!TIP]  
> Sie müssen eine Baselineversion von Configuration Manager verwenden, um einen neuen Standort zu installieren.  
>
> Weitere Informationen:    
> - [Installieren von neuen Standorten](../../servers/deploy/install/installing-sites.md)  
> - [Installieren von Updates an Standorten](../../servers/manage/updates.md)  
> - [Baseline- und Updateversionen](../../servers/manage/updates.md#bkmk_Baselines)

Die folgenden Abschnitte enthalten Details zu Änderungen und neuen Funktionen, die in Version 1702 von Configuration Manager eingeführt wurden.  

## <a name="deprecated-features-and-operating-systems"></a>Veraltete Features und Betriebssysteme
Erfahren Sie mehr zu Supportänderungen, bevor Sie in [entfernten und veralteten Elementen](deprecated/removed-and-deprecated.md) implementiert werden.

Version 1702 löscht die Unterstützung für die folgenden Produkte:
- **SQL Server 2008 R2**, für Standortdatenbankserver. Die Einstellung des Supports wurde [erstmals am 10. Juli 2015](deprecated/removed-and-deprecated-server.md#sql-server) angekündigt. Diese Version von SQL Server wird weiterhin unterstützt, wenn Sie eine Version von Configuration Manager vor Version 1702 verwenden.
- **Windows Server 2008 R2**, für Standortsystemserver und Standortsystemrollen. Die Einstellung des Supports wurde [erstmals am 10. Juli 2015](deprecated/removed-and-deprecated-server.md#server-os) angekündigt. Diese Version von Windows wird weiterhin unterstützt, wenn Sie eine Version von Configuration Manager vor Version 1702 verwenden.  
- **Windows Server 2008**, für Standortsystemserver und die meisten Standortsystemrollen. Die Einstellung des Supports wurde [erstmals am 10. Juli 2015](deprecated/removed-and-deprecated-server.md#server-os) angekündigt.
- **Windows XP Embedded**, als Clientbetriebssystem. Die Einstellung wurde [erstmals am 10. Juli 2015](deprecated/removed-and-deprecated-client.md#deprecated-client-operating-systems) angekündigt. Diese Version von Windows wird weiterhin unterstützt, wenn Sie eine Version von Configuration Manager vor Version 1702 verwenden.




## <a name="site-infrastructure"></a>Infrastruktur von Standorten

### <a name="improvements-for-in-console-search"></a>Verbesserungen für die Suche in der Konsole
Im folgenden finden Sie Verbesserungen der Verwendung der Suche in der Configuration Manager-Konsole:
- **Objektpfad:**  
  Viele Objekte unterstützen jetzt eine Spalte namens **Objektpfad**.  Wenn Sie bei Ihrer Suche diese Spalte bei Ihrer Ergebnisanzeige hinzufügen, können Sie den Pfad für jedes Objekt sehen. Wenn Sie beispielsweise eine Suche nach Apps im Knoten „Anwendungen“ durchführen und auch nach untergeordnete Knoten suchen, wird in der *Objektpfad*-Spalte im Ergebnisbereich der Pfad für jedes zurückgegebene Objekt angezeigt.   

- **Erhalt des Suchtextes:**  
  Wenn Sie Text in das Suchfeld eingeben, und dann zwischen der Suche nach einem untergeordneten und dem aktuellen Knoten wechseln, wird der von Ihnen eingegebene Text beibehalten und für die weitere Verwendung zur Verfügung stehen, ohne dass er erneut eingeben werden muss.

- **Entscheidungserhalt bei der Suche in untergeordneten Knoten:**  
  Wenn Sie den Knoten ändern, in dem Sie arbeiten, wird die Option, die Sie sowohl für die Suche in *aktuellen Knoten* als auch für die Suche in *allen untergeordneten Knoten* auswählen, jetzt beibehalten. Dieses neue Verhalten bedeutet, dass Sie die Entscheidung nicht ständig zurücksetzen müssen, während Sie sich auf der Konsole bewegen. Beim Öffnen der Konsole ist die Option standardmäßig so festgelegt, dass nur im aktuellen Knoten gesucht wird.


### <a name="send-feedback-from-the-configuration-manager-console"></a>Feedback über die Configuration Manager-Konsole geben

Sie können die Feedbackoptionen in der Konsole verwenden, um Feedback direkt an das Entwicklerteam zu senden.

Die **Feedback**optionen finden Sie hier:
- Im Menüband, ganz links von der Registerkarte „Startseite“ jedes Knotens.  
  ![Menüband](./media/feedback-home.png)

- Wenn Sie mit der rechten Maustaste auf ein beliebiges Objekt in der Konsole klicken.   
   ![Rechtsklick](./media/feedback-option.png)   

  Wenn Sie **Feedback** auswählen, öffnet sich die [Configuration Manager UserVoice-Feedback-Website](https://configurationmanager.uservoice.com/forums/300492-ideas).


###  <a name="changes-for-updates-and-servicing"></a>Änderungen an Updates und Wartung
Im Folgenden sind Änderungen an Updates und Wartung aufgeführt:

- **Knotenposition**   
  Nach der Installation von Version 1702, erscheint der Knoten **Updates und Wartung** als Knoten der obersten Ebene unter **Verwaltung**. Er ist nicht länger ein untergeordneter Knoten unten **Clouddienste**.

- **Neue Updatestatus**  
  Wenn Sie in der Konsole verfügbare Updates anzeigen, sind zwei neue Status vorhanden:  
  - **Für die Installation verfügbar**: Dies ist ein Update, das heruntergeladen wurde und zur Installation bereit steht.
  - **Bereit zum Download**: Dieses Update ist verfügbar, wurde aber noch nicht heruntergeladen. Sie können dieses Update herunterladen, jedoch ist es aufgrund eines neueren Updates veraltet.


- **Einfachere Auswahlmöglichkeiten für Updates**  
  Wenn das nächste Mal eins oder mehrere Updates für Ihre Infrastruktur zur Verfügung stehen, wird nur noch das aktuellste Update heruntergeladen. Wenn beispielsweise Ihre aktuelle Standortversion mindestens zwei Versionen älter als die aktuellste verfügbare Version ist, wird lediglich diese aktuellste Updateversion automatisch heruntergeladen.  

  Sie haben die Option, auch die anderen verfügbaren Updates herunterzuladen und zu installieren, auch wenn diese nicht die aktuellsten Versionen sind. Wenn Sie ein älteres Update herunterladen, erhalten Sie eine Warnmeldung, dass das Update von einem aktuelleren ersetzt wurde. Um ein *verfügbares* Update herunterzuladen, wählen Sie das Update in der Konsole aus, und klicken Sie anschließend auf **Herunterladen**.

- **Verbesserte Bereinigung älterer Updates**   
  Wir haben eine automatische Bereinigungsfunktion hinzugefügt, die nicht mehr benötigte Downloads aus dem Ordner „EasySetupPayload“ auf Ihrem Standortserver löscht. Da dies in Version 1702 eingeführt wurde, beginnt der die Bereinigung nach der Installation eines nachfolgenden Updates, z.B. einem Updaterollup oder einer zukünftigen Updateversion.  


### <a name="data-warehouse-service-point"></a>Data Warehouse-Dienstpunkt
Verwenden Sie den Data Warehouse-Dienstpunkt, um langfristige Verlaufsdaten zur Bereitstellung für Configuration Manager zu speichern und hierfür Berichte zu erstellen.

Das Data Warehouse unterstützt ein Datenvolumen von bis zu 2 TB, inklusive der Zeitstempel für Änderungsnachverfolgung. Die Speicherung der Daten wird durch die automatisierte Synchronisierung der Configuration Manager-Standortdatenbank mit der Data Warehouse-Datenbank erreicht. Auf diese Informationen kann dann vom Reporting Services-Punkt aus zugegriffen werden.

Weitere Informationen finden Sie unter [The Data Warehouse service point (Der Data Warehouse-Dienstpunkt)](../../servers/manage/data-warehouse.md).


### <a name="peer-cache-improvements"></a>Verbesserungen des Peercaches
Ab Version 1702 lehnt ein Peercachequellcomputer eine Inhaltsanforderung ab, wenn der Peercachequellcomputer eine der folgenden Bedingungen erfüllt:  
-  Niedriger Akkustand.
-  Zum Zeitpunkt der Anforderungen des Inhalts liegt die CPU-Auslastung bei über 80 %.
-  *AvgDiskQueueLength* der Datenträger-E/A überschreitet 10.
-  Es gibt keine weiteren Verbindungen zum Computer.   
Weitere Informationen finden Sie unter **Eingeschränkter Zugriff auf eine Peercachequelle** und [Peercache für Configuration Manager-Clients](../hierarchy/client-peer-cache.md).   

Darüber hinaus werden dem Berichterstattungspunkt drei neue Berichte hinzugefügt. Sie können diese Berichte verwenden, um weitere Detail zu abgelehnten Inhaltsanforderungen zu verstehen, einschließlich welche Begrenzungsgruppe, Computer und welcher Inhalt involviert war. Weitere Informationen finden Sie im Peercache-Thema unter [Überwachung](../hierarchy/client-peer-cache.md#monitoring).

### <a name="content-library-cleanup-tool"></a>Inhaltsbibliothek-Bereinigungstool
Verwenden Sie das [Inhaltsbibliothek-Bereinigungstool](../hierarchy/content-library-cleanup-tool.md) für die Entfernung von Inhalt von Verteilungspunkten, wenn dieser Inhalt nicht mehr einer Anwendung zugeordnet ist.


### <a name="use-the-oms-connector-with-the-azure-government-cloud"></a>Verwenden des OMS-Connectors mit der Azure Government-Cloud
Sie können den OMS-Connector zum Verbinden von OMS-Protokollanalysen in der Microsoft Azure Government-Cloud verwenden. Dazu müssen Sie vor der Installation des OMS-Connectors eine Konfigurationsdatei ändern, damit der Connector mit der Government-Cloud arbeiten kann. Weitere Informationen finden Sie unter [Verwenden des OMS-Connectors mit der Azure Government-Cloud](/azure/azure-monitor/platform/collect-sccm).

### <a name="software-update-points-are-added-to-boundary-groups"></a>Softwareupdatepunkte werden Begrenzungsgruppen hinzugefügt
Ab Version 1702 verwenden Client Begrenzungsgruppen, um einen neuen Softwareupdatepunkt zu finden, und um ein Fallback durchzuführen und einen neuen Softwareupdatepunkt zu finden, wenn auf ihren aktuellen nicht mehr zugriffen werden kann. Sie können verschiedenen Begrenzungsgruppen einzelne Softwareupdatepunkte hinzufügen, um zu steuern, welchen Server ein Client finden kann. Weitere Informationen finden Sie im Thema [Configuring Boundary Groups (Konfigurieren von Begrenzungsgruppen)](../../servers/deploy/configure/boundary-groups.md) unter [Software Update Points (Softwareupdatepunkte)](../../servers/deploy/configure/boundary-groups.md#bkmk_sup).


<!-- ## Migration  -->

<!-- ## Client management  -->

## <a name="compliance-settings"></a>Kompatibilitätseinstellungen

### <a name="new-compliance-settings-for-ios"></a>Neue Kompatibilitätseinstellungen für iOS

Wir haben viele neue Einstellungen für iOS-Geräte entsprechend den verfügbaren mit Microsoft Intune hinzugefügt.


## <a name="application-management"></a>Anwendungsverwaltung

### <a name="improved-support-for-windows-store-for-business-apps"></a>Verbesserte Unterstützung für Windows Store für Unternehmen

Online lizenzierte Apps können jetzt dem Windows Store für Unternehmen auf Windows 10-PCs bereitgestellt werden, die Sie mithilfe des Configuration Manager-Clients verwalten.
Weitere Informationen finden Sie unter [Verwalten von Apps aus dem Windows Store für Unternehmen](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

### <a name="check-for-running-executable-files-before-installing-an-application"></a>Prüfen Sie auf ausgeführte ausführbare Dateien, bevor Sie eine Anwendung installieren

Sie können jetzt auf der Registerkarte **Installationsverhalten** im Dialogfeld **Eigenschaften** eines Bereitstellungstyps eine von mehreren ausführbaren Dateien festlegen, die, wenn sie ausgeführt wird, die Installation des Bereitstellungstyps verhindert. Der Benutzer muss die ausgeführte ausführbare Datei schließen bevor der Bereitstellungstyp installiert werden kann – die Datei kann aber auch automatisch für Bereitstellungen mit dem Zweck „Erforderlich“ geschlossen werden.

Wenn die Anwendung als **Verfügbar** bereitgestellt wurde, und ein Endbenutzer versucht, eine Anwendung zu installieren, wird er dazu aufgefordert, alle ausgeführten ausführbaren, von Ihnen festgelegten Dateien zu schließen, bevor er mit der Installation fortfahren kann.

Wenn die Anwendung als **Erforderlich** bereitgestellt wurde, und die Option **Ausgeführte ausführbare Dateien automatisch schließen, die im Eigenschaftendialogfeld des Bereitstellungstyps auf der Registerkarte "Installationsverhalten" angegeben wurden** ausgewählt ist, wird dem Endbenutzer ein Dialogfeld angezeigt, das ihn darüber informiert, dass ausführbare, von Ihnen festgelegte Dateien automatisch geschlossen werden, wenn die Frist der Installation abgelaufen ist.

### <a name="app-management-improvements-for-hybrid-mdm"></a>Verbesserungen der App-Verwaltung für die hybride Verwaltung mobiler Geräte (MDM)

- [Deploy volume-purchased iOS apps to device collections (Bereitstellen per Volumenlizenz erworbener iOS-Apps in Gerätesammlungen)](#deploy-volume-purchased-ios-apps-to-device-collections)
- [Support for iOS Volume Purchase Program for Education (Unterstützung für das iOS-Volume Purchase Program for Education)](#support-for-ios-volume-purchase-program-for-education)
- [Support for multiple volume-purchase program tokens (Unterstützung für eine Vielzahl von per Volumenlizenz erworbener Programmtoken)](#support-for-multiple-volume-purchase-program-tokens)


## <a name="operating-system-deployment"></a>Betriebssystembereitstellung

### <a name="expire-stand-alone-media"></a>Ablaufdatum eigenständiger Medien
Beim Erstellen eines eigenständigen Mediums stehen Ihnen nun neue Optionen zur Verfügung, mit denen Sie optional den Beginn und das Ende des Gültigkeitszeitraums dieses Mediums festlegen können. Standardmäßig sind diese Einstellungen deaktiviert. Vor der Ausführung des eigenständigen Mediums werden die Datums- und Zeitangaben für den Zeitraum mit der Systemzeit auf dem Computer verglichen. Wenn die Systemzeit vor der Startzeit oder hinter der Ablaufzeit liegt, wird das eigenständige Medium nicht gestartet. Diese Optionen sind auch über das PowerShell-Cmdlet „New-CMStandaloneMedia“ verfügbar. Weitere Informationen finden Sie unter [Erstellen eigenständiger Medien](../../../osd/deploy-use/create-stand-alone-media.md)

### <a name="package-id-displayed-in-task-sequence-steps"></a>Paket-ID, die in Tasksequenzschritten angezeigt wird
Jeder Tasksequenzschritt, der auf ein Paket, ein Treiberpaket, ein Betriebssystemimage, ein Startimage oder ein Betriebssystem-Upgradepaket verweist, zeigt nun die Paket-ID des Objekts an, auf das verwiesen wird. Wenn in einem Tasksequenzschritt auf eine Anwendung verwiesen wird, wird die Objekt-ID angezeigt.

### <a name="support-for-additional-content-in-stand-alone-media"></a>Unterstützung für zusätzliche Inhalte in eigenständigen Medien
Zusätzlicher Inhalt wird nun in eigenständigen Medien unterstützt. Wählen Sie Pakete, Treiberpakete und Anwendungen aus, die auf den Medien zusätzlich zum anderen Inhalt bereitgestellt werden sollen, auf den in der Tasksequenz verwiesen wird. Bisher wurde nur der Inhalt auf eigenständigen Medien bereitgestellt, auf den in der Tasksequenz verwiesen wurde. Weitere Informationen finden Sie unter [Erstellen eigenständiger Medien](../../../osd/deploy-use/create-stand-alone-media.md)

### <a name="hardware-inventory-collects-uefi-information"></a>Die Hardwareinventur sammelt UEFI-Informationen
Ihnen stehen eine neue Hardwareinventurklasse (**SMS_Firmware**) und eine neue Eigenschaft (**UEFI**) zur Verfügung, mit der Sie bestimmen können, ob ein Computer im UEFI-Modus startet. Wenn ein Computer im UEFI-Modus gestartet wird, ist die Eigenschaft **UEFI** auf **TRUE** festgelegt. Dies ist bei der Hardwareinventur standardmäßig aktiviert. Weitere Informationen zur Hardwareinventur finden Sie unter [How to configure hardware inventory (Konfigurieren der Hardwareinventur)](../../clients/manage/inventory/configure-hardware-inventory.md).

### <a name="improvements-to-software-center-warning-messages-for-high-impact-task-sequences"></a>Verbesserungen bei den Benachrichtigungen für Tasksequenzen mit schwerwiegenden Auswirkungen in Software Center
Dieses Release beinhaltet folgende Verbesserungen für die Benachrichtigungen für Tasksequenzen mit schwerwiegenden Auswirkungen im Softwarecenter:

- In den Eigenschaften der Tasksequenz können Sie jede beliebige Tasksequenz konfigurieren, einschließlich Tasksequenzen, die nicht zum Betriebssystem gehören, wie etwa risikoreiche Bereitstellungen. Jede Tasksequenz, die bestimmte Bedingungen erfüllt, wird automatisch als „high-impact“ (mit schwerwiegenden Auswirkungen) definiert. Weitere Informationen finden Sie unter [Verwalten risikoreicher Bereitstellungen](../../servers/manage/settings-to-manage-high-risk-deployments.md).
- In den Eigenschaften der Tasksequenz können Sie die Standardbenachrichtigung festlegen oder Ihre eigene benutzerdefinierte Benachrichtigung für Bereitstellungen mit schwerwiegenden Auswirkungen erstellen.
- In den Eigenschaften der Tasksequenz können Sie die Eigenschaften vom Softwarecenter konfigurieren, zu denen „Make a restart required“ (Neustart erforderlich), die Downloadgröße der Tasksequenz und die geschätzte Laufzeit gehören.
- Die Standardmeldung für Bereitstellungen mit schwerwiegenden Auswirkungen für direkte Aktualisierungen gibt jetzt an, dass Ihre App, Daten und Einstellungen automatisch migriert werden. Zuvor gab die Standardmeldung für jede Installation des Betriebssystems an, dass alle Apps, Daten und Einstellungen verloren gingen, was jedoch für eine direkte Aktualisierung nicht galt.

Weitere Informationen finden Sie unter [Konfigurieren von Einstellungen für eine Tasksequenz mit schwerwiegenden Auswirkungen](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#set-a-task-sequence-as-a-high-impact-task-sequence)

### <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Rückkehr zur vorherigen Seite, wenn eine Tasksequenz fehlschlägt
Sie können jetzt zu einer vorherigen Seite zurückkehren, wenn Sie eine Tasksequenz ausführen und ein Fehler auftritt. Bevor es diese Version gab, mussten Sie die Tasksequenz neu starten, wenn ein Fehler aufgetreten ist. In den folgenden Szenarios können Sie zum Beispiel die Schaltfläche **Zurück** verwenden:

- Beim Starten eines Computers in Windows PE wird möglicherweise der Bootstrap-Dialog der Tasksequenz angezeigt, bevor die Tasksequenz verfügbar ist. Wenn Sie in diesem Szenario auf „Weiter“ klicken, wird auf der letzten Seite der Tasksequenz eine Nachricht angezeigt, die darüber informiert, dass es keine verfügbaren Tasksequenzen gibt. Klicken Sie jetzt auf **Zurück**, um erneut nach verfügbaren Tasksequenzen zu suchen. Sie können diesen Vorgang wiederholen, bis die Tasksequenz verfügbar ist.
- Wenn die abhängigen Paketinhalte beim Ausführen einer Tasksequenz an den Verteilungspunkten noch nicht verfügbar sind, kann die Tasksequenz nicht ausgeführt werden. Sie können jetzt die fehlende Inhalte verteilen (wenn diese noch nicht verteilt wurden). Sie können auch warten, bis die Inhalte auf den Verteilungspunkten verfügbar sind, und dann auf **Zurück** klicken, damit die Tasksequenz wieder nach den Inhalten sucht.

### <a name="pre-cache-content-for-available-deployments-and-task-sequences"></a>Zwischenspeichern von Inhalt für verfügbare Bereitstellungen und Tasksequenzen
Ab Version 1702 (für verfügbare Bereitstellungen und Tasksequenzen) können Sie zwischengespeicherten Inhalt verwenden. Mit dem Zwischenspeichern von Inhalten können Sie den Client dahingehend einschränken, dass er nur zutreffenden Inhalt herunterladen darf, wenn er die Bereitstellung empfängt. Wenn der Benutzer dann im Softwarecenter auf **Installieren** klickt, steht der Inhalt bereit, und die Installation startet sofort, da der Inhalt bereits auf der lokalen Festplatte gespeichert ist. Informationen finden Sie unter [Konfigurieren des zwischengespeicherten Inhalts](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#configure-pre-cache-content).

### <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Konvertieren von BIOS in UEFI während eines direkten Upgrades
Windows 10 Creators Update führt ein einfaches Konvertierungstool ein, womit der Prozess der Neupartitionierung der Festplatte für UEFI-aktivierte Hardware automatisiert werden kann und das Konvertierungstool in den direkten Upgradeprozess von Windows 7 zu Windows 10 integriert werden kann. Wenn Sie dieses Tool mit Ihrer Tasksequenz des Betriebssystemupgrades und dem OEM-Tool kombinieren, der die Firmware von BIOS zu UEFI konvertiert, können Sie Ihre Computer von BIOS zu UEFI während eines direkten Upgrades zu Windows 10 Creators Update konvertieren. Weitere Informationen finden Sie unter [Task sequence steps to manage BIOS to UEFI conversion (Tasksequenzschritte für das Verwalten einer Konvertierung von BIOS zu UEFI)](../../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu).

### <a name="improvements-to-the-install-applications-task-sequence-step"></a>Verbesserungen am Tasksequenzschritt „Anwendungen installieren“
In dieser Version wurden die folgenden Verbesserungen eingeführt:
- Erhöht die maximale Anzahl von Anwendungen, die Sie im Tasksequenzschritt **Anwendungen installieren** bis 99 installieren können. Vorher war maximal die Installation von neun Anwendungen möglich.
- Wenn Sie im Tasksequenz-Editor Anwendungen zum Tasksequenzschritt **Apps installieren** hinzufügen, können Sie im Bereich **Zu installierende Anwendung auswählen** nun mehrere Anwendungen hinzufügen.

### <a name="improvements-to-the-auto-apply-driver-task-sequence"></a>Verbesserungen an der Tasksequenz „Treiber automatisch anwenden“
Ihnen stehen im Tasksequenzschritt „Treiber automatisch anwenden“ neue Tasksequenzvariablen für die Konfiguration des Timeoutwerts bei Anfragen gegenüber dem HTTP-Katalog zur Verfügung. Die folgenden Variablen und Standardwerte (in Sekunden) sind verfügbar:
- SMSTSDriverRequestResolveTimeOut  
  Standard: 60
- SMSTSDriverRequestConnectTimeOut  
  Standard: 60
- SMSTSDriverRequestSendTimeOut  
  Standard: 60
- SMSTSDriverRequestReceiveTimeOut  
  Standard: 480

### <a name="windows-10-adk-tracked-by-build-version"></a>Windows 10 ADK, von der Buildversion verfolgt
Das Windows 10 ADK wird nun anhand der Buildversion nachverfolgt, um eine kontrollierte Anpassung von Windows 10-Startimages zu gewährleisten. Wird beispielsweise das Windows ADK für Windows 10 in der Version 1607 verwendet, so können nur Startimages mit Version 10.0.14393 in der Konsole angepasst werden. Ausführliche Informationen zum Anpassen von WinPE-Versionen finden Sie unter [Startimages anpassen](../../../osd/get-started/customize-boot-images.md).

### <a name="default-boot-image-source-path-can-no-longer-be-changed"></a>Der Quellpfad des Standardstartimages kann nicht mehr geändert werden
Standard-Startimages werden von Configuration Manager verwaltet, und ihr Quellpfad kann nicht mehr über die Configuration Manager-Konsole oder über das Configuration Manager SDK geändert werden. Sie können weiterhin einen benutzerdefinierten Quellpfad für benutzerdefinierte Startimages konfigurieren.

### <a name="default-boot-images-are-regenerated-after-upgrading-configuration-manager-to-a-new-version"></a>Standard-Startimages werden nach dem Upgrade von Configuration Manager auf eine neue Version neu generiert
Wenn Sie die Windows ADK-Version upgraden und dann Updates und Wartung zum Installieren der neuesten Version von Configuration Manager verwenden, generiert Configuration Manager ab dieser Version die Standardstartimages neu. Dies schließt die neue Windows PE-Version vom aktualisierten Windows ADK ein, die neue Version des Configuration Manager-Clients, Treiber, Anpassungen und so weiter. Benutzerdefinierte Startimages werden nicht geändert. Weitere Informationen finden Sie unter [Manage boot images (Verwalten von Startimages)](../../../osd/get-started/manage-boot-images.md#BKMK_BootImageDefault).

## <a name="software-updates"></a>Softwareupdates

### <a name="deploy-office-365-apps-to-clients"></a>Bereitstellen von Office 365-Apps für Clients
In diesem Release können Sie ab Version 1702 vom Office 365-Clientverwaltungsdashboard aus den Office 365-Installer starten, mit dem Sie Office 365-Installationseinstellungen konfigurieren, Dateien aus Office Content Delivery Networks (CDNs) herunterladen und die Dateien als Anwendung in Configuration Manager bereitstellen können. Weitere Informationen finden Sie unter [Verwalten von Office 365 ProPlus-Updates](../../../sum/deploy-use/manage-office-365-proplus-updates.md#bkmk_deploy).

> [!IMPORTANT]
> Die Office 365-App, die Sie mithilfe des Assistenten für Office 365-Anwendungen in Configuration Manager erstellen und bereitstellen, wird nicht automatisch von Configuration Manager verwaltet. Dies geschieht erst nach Aktivierung der Client-Agent-Einstellungen der Softwareupdates **Verwaltung des Office 365-Client-Agents aktivieren**. Weitere Informationen finden Sie unter [Informationen zu Clienteinstellungen](../../clients/deploy/about-client-settings.md).

### <a name="manage-express-installation-files-for-windows-10-updates"></a>Unterstützung von Express-Installationsdateien für Windows 10-Updates
Configuration Manager unterstützt ab Version 1702 Express-Installationsdateien für Windows 10-Updates. Wenn Sie eine unterstützte Version von Windows 10 verwenden, können Sie jetzt die Configuration Manager-Einstellungen nutzen, um nur das Delta zwischen dem kumulativen Update von Windows 10 des laufenden Monats und dem Updates des Vormonats herunterzuladen. Ohne Express-Installationsdateien lädt Configuration Manager die kompletten kumulativen Updates für Windows 10 (einschließlich aller Updates aus den letzten Monaten) jeden Monat herunter. Mit Expressinstallationsdateien erhalten Sie kleinere Downloads und kürzere Installationszeiten. Informationen finden Sie unter [Verwalten von Express-Installationsdateien für Windows 10-Updates](../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md)


<!-- ## Reporting  -->

<!-- ## Inventory  -->

## <a name="mobile-device-management"></a>Verwaltung mobiler Geräte

### <a name="android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm"></a>Android- und iOS-Versionen werden nicht mehr über den Erstellungsassistenten für hybrides MDM erreicht

Ab Version 1702 für die hybride mobile Geräteverwaltung (MDM) müssen Sie nicht mehr bestimmte Android- und iOS-Versionen auswählen, wenn Sie neue Richtlinien und Profile für mit Intune verwaltete Geräte erstellen wollen. Stattdessen wählen Sie einen der folgenden Gerätetypen aus:

- Android
- Samsung KNOX Standard 4.0 und höher
- iPhone
- iPad

Diese Änderung wirkt sich auf den Assistenten beim Erstellen der folgenden Elemente aus:

- Konfigurationselemente
- Kompatibilitätsrichtlinien
- Zertifikatprofile
- E-Mail-Profile
- VPN-Profile
- WLAN-Profile

Durch diese Änderung können Hybridbereitstellungen schneller neue Android und iOS-Versionen unterstützen, ohne eine neue Configuration Manager-Version oder -Erweiterung zu benötigen. Sobald eine neue Version in Intune standalone unterstützt wird, können Benutzer ihre mobilen Geräte auf diese Version upgraden.

Um Probleme beim Upgrade von vorherigen Configuration Manager-Versionen zu vermeiden, kann auf andere Versionen des mobilen Betriebssystems den Eigenschaftsseiten für diese Elemente zugegriffen werden. Sollten Sie nur auf eine bestimmte Version abzielen, können Sie das neue Element erstellen und diesem dann auf dessen Eigenschaftsseite eine bestimmte Version zuweisen. 

> [!NOTE]
> Die letzte in den Eigenschaftenseiten verfügbare mobile Betriebssystemversion gilt für diese Version und alle nachfolgenden Versionen. Die Eigenschaftenseiten bieten folgende Optionen für höhere Betriebssystemversionen als Android 7 und iOS 10: 
> - **Android 7 und höher**
> - **Alle iPhone- oder iPod-Fingereingabegeräte mit iOS 10 und höher**
> - **Alle iPad-Geräte mit iOS 10 und höher**

### <a name="android-for-work-support"></a>Unterstützung für Android for Work
Ab 1702 unterstützt die hybride Verwaltung mobiler Geräte mit Microsoft Intune jetzt Android for Work für die Registrierung und Verwaltung von Geräten.

### <a name="deploy-volume-purchased-ios-apps-to-device-collections"></a>Bereitstellen per Volumenlizenz erworbener iOS-Apps in Gerätesammlungen

Sie können jetzt sowohl Geräten als auch Benutzern lizenzierte Apps bereitstellen. Je nachdem, inwieweit die App Gerätelizenzierungen unterstützt, wird eine entsprechende Lizenz wie folgt beansprucht:

| Configuration Manager-Version | Unterstützt die App Gerätelizenzierung? | Typ der Bereitstellungssammlung | Beanspruchte Lizenz |
| ----------------------------- | ------------------------------ | -------------------------- | --------------- |
|Früher als 1702|Ja|Benutzer|Benutzerlizenz|
|Früher als 1702|Nein|Benutzer|Benutzerlizenz|
|Früher als 1702|Ja|Gerät|Benutzerlizenz|
|Früher als 1702|Nein|Gerät|Benutzerlizenz|
|1702 und höher|Ja|Benutzer|Benutzerlizenz|
|1702 und höher|Nein|Benutzer|Benutzerlizenz|
|1702 und höher|Ja|Gerät|Gerätelizenz|
|1702 und höher|Nein|Gerät|Benutzerlizenz|

### <a name="support-for-ios-volume-purchase-program-for-education"></a>Unterstützung für das iOS-Volume Purchase Program for Education

Außerdem können Sie Apps bereitstellen und nachverfolgen, die Sie in iOS Volume Purchase Program für Bildungseinrichtungen erworben haben.

### <a name="support-for-multiple-volume-purchase-program-tokens"></a>Unterstützung für eine Vielzahl von per Volumenlizenz erworbener Programmtoken

Sie können Configuration Manager jetzt mehrere Apple VPP-Tokens zuordnen.

### <a name="support-for-line-of-business-apps-in-windows-store-for-business"></a>Support für branchenspezifische Apps im Windows Store für Unternehmen

Sie können jetzt benutzerdefinierte branchenspezifische Apps aus dem Windows Store für Unternehmen synchronisieren.

### <a name="conditional-access-device-compliance-policy-improvements"></a>Verbesserungen bei Gerätekompatibilitätsrichtlinien für bedingten Zugriff

Eine neue Regel für die Gerätekompatibilitätsrichtlinie ist verfügbar; sie hilft Ihnen beim Verweigern des Zugriffs auf Unternehmensressourcen, die bedingten Zugriff unterstützen, wenn Benutzer Anwendungen verwenden, die auf einer Liste nicht kompatibler Anwendungen stehen. Die Liste nicht kompatibler Anwendungen kann von Administrator beim Hinzufügen der neuen Regel **Nicht installierbare Apps** definiert werden. Für diese Regel muss der Administrator den **App-Namen**, die **Apple-ID** und den **App-Herausgeber** (optional) eingeben, wenn er eine Anwendung auf die Liste „Nicht kompatibel“ setzen möchte. Diese Einstellung gilt nur für iOS- und Android-Geräte.

Des Weiteren hilft sie Organisationen dabei, Datenlecks durch unsichere Apps zu beheben und einen außerordentlich hohe Datenverbrauch von gewissen Apps zu verhindern.


### <a name="new-mobile-threat-defense-monitoring-tools"></a>Neue Überwachungstools für Mobile Threat Defense

Sie haben ab Version 1702 die Möglichkeit, den Kompatibilitätsstatus mit Ihrem Dienstanbieter für Mobile Threat Defense zu überwachen.


## <a name="protect-devices"></a>Schützen von Geräten

### <a name="detect-outdated-antimalware-client-versions"></a>Erkennen veralteter Antimalware-Clientversionen
Ab Version 1702 können Sie eine Warnung konfigurieren, um sicherzustellen, dass Endpoint Protection-Clients nicht veraltet sind. Weitere Informationen finden Sie unter [Warnung für veralteten Malwareclient](../../../protect/deploy-use/endpoint-configure-alerts.md#alert-for-outdated-malware-client).

### <a name="device-health-attestation-updates"></a>Updates zum Nachweis der Geräteintegrität
Der Nachweis der Geräteintegrität für lokale Clients kann nun vom Verwaltungspunkt aus konfiguriert und verwaltet werden. Weitere Informationen finden Sie unter [Integritätsnachweis](../../servers/manage/health-attestation.md).

### <a name="certificate-profiles-for-windows-hello-for-business"></a>Zertifikatprofile für Windows Hello for Business

Wenn Sie Zertifikatprofile im Schlüsselcontainer von Windows Hello for Business speichern möchten, und das Zertifikatprofil Smartcard-Anmeldung für die erweiterte Schlüsselverwendung verwendet, müssen Sie die Berechtigungen für die Schlüsselregistrierung konfigurieren, um sicherzustellen, dass das Zertifikat ordnungsgemäß überprüft wurde.
Weitere Informationen finden Sie unter [Configure Windows Hello for Business settings (So konfigurieren Sie Windows Hello for Business-Einstellungen)](../../../protect/deploy-use/windows-hello-for-business-settings.md).

### <a name="new-windows-hello-for-business-notification-for-end-users"></a>Die neue Windows Hello for Business-Benachrichtigung für Endbenutzer
Eine neue Windows 10-Benachrichtigung informiert Benutzer, dass zusätzliche Aktionen abgeschlossen werden müssen, um die Installation von Windows Hello für Business (z.B. Einrichten einer PIN) abzuschließen.