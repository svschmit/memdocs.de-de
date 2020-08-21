---
title: Neues in Version 1606
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über Änderungen und neue Funktionen, die in Version 1606 von Configuration Manager eingeführt wurden.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: df2e57b9-6445-4067-98e7-ace85d4e6aa6
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 2fa46770adfbf3e688bbdc561d8193967f3913cd
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88698587"
---
# <a name="what39s-new-in-version-1606-of-configuration-manager"></a>Neuerungen in Version 1606 von Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Das Update 1606 für Configuration Manager ist nur als konsoleninternes Update für zuvor installierte Standorte verfügbar, die Version 1511 oder 1602 ausführen. 1511 ist die anfängliche Baselineversion, die Sie verwenden, um einen neuen Configuration Manager-Standort zu installieren.
> [!TIP]  
> Weitere Informationen:  
>   
> - [Installing new sites (Installieren von neuen Standorten)](../../servers/deploy/install/prepare-to-install-sites.md) (mithilfe einer Baselineversion wie 1511)  
> - [Installing updates at sites (Installieren von Updates an Standorten)](../../servers/manage/updates.md) (z.B. Update von 1602 oder 1606)  

 Die folgenden Abschnitte enthalten Details zu Änderungen und neue Funktionen, die in Version 1606 von Configuration Manager eingeführt wurden.  



## <a name="updates-and-servicing"></a><a name="updatesandservicing"></a>Updates und Wartung

### <a name="changes-for-the-updates-and-servicing-node"></a>Änderungen am Knoten „Updates und Wartung“
Folgenden Änderungen an Updates und Wartung in der Configuration Manager-Konsole wurden vorgenommen:
> [!NOTE]
> Diese Änderungen sind erst nach der Installation von Version 1606 verfügbar.

- **Änderung des Knotennamen:**

    Im Arbeitsbereich **Überwachung** wurde der Knoten **Wartungsstatus des Standorts** in **Update- und Wartungsstatus** umbenannt.
- **Details der Erweiterung des Installationsstatus:**

    Wenn Sie den Updateinstallationsstatus für einen Standort anzeigen, zeigt die Konsole nun die Details zu den folgenden Aktionen getrennt an:
    - **Herunterladen** (Dies gilt nur für den Standort der obersten Ebene, auf dem die Standortsystemrolle des Dienstverbindungspunkts installiert ist.)
    - **Replikation**
    - **Prüfung der erforderlichen Komponenten**
    - **Installation**

  Darüber hinaus stehen jetzt detailliertere Informationen zu jedem Schritt zur Verfügung, z.B. in welcher Protokolldatei Sie weitere Informationen finden.  
-   **Neue Option zum Wiederholen von Fehlern der erforderlichen Komponente:**

    In den Arbeitsbereichen **Verwaltung** und **Überwachung** enthält der Knoten **Updates und Wartung** eine neue Schaltfläche auf dem Menüband mit der Bezeichnung **Warnungen zu erforderlichen Komponenten ignorieren**.

    Wenn Sie Updates installieren, ohne die Option „Warnungen zu erforderlichen Komponenten ignorieren“ (innerhalb des Update-Assistenten) zu verwenden, und diese Updateinstallation aufgrund einer Warnung angehalten wird, können Sie **Warnungen zu erforderlichen Komponenten** auf dem Menüband auswählen. Dadurch wird die automatische Fortsetzung der Updateinstallation ausgelöst.  



- **Übersichtlichere Ansicht der Updates:**

    Auf dem Knoten **Updates und Wartung** sehen Sie jetzt nur noch die zuletzt installierten Updates und alle neuen Updates, die zur Installation für Sie bereitstehen. Wenn Sie bereits installierte Updates anzeigen möchten, klicken Sie auf die neue Schaltfläche **Verlauf**, die auf dem Menüband angezeigt wird.  

-   **Umbenannte Option für die Präproduktion:**

    Auf dem Knoten **Updates und Wartung** wurde die Schaltfläche **Clientoptionen** in **Präproduktionsclient höher stufen** umbenannt.


###  <a name="pre-release-features"></a>Features der Vorabversion
Ab Version 1606 müssen Sie für die Verwendung von Features der Vorabversion in Configuration Manager Ihre Zustimmung geben, bevor Sie diese auswählen und verwenden können. Weitere Informationen finden Sie unter [Use pre-release features from updates](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease) (Verwenden von Vorabfeatures aus Updates).

### <a name="new-distribution-point-update-behavior"></a>Neues Updateverhalten von Verteilungspunkten
In Update 1606 werden Änderungen eingeführt, die die Verfügbarkeit von Verteilungspunkten für die Installation von künftigen Updates verbessern.

Wenn Sie nach der Installation von Update 1606 ein Update auf dem Standort durchführen, der die automatische Neuinstallation von Standard- und Verteilungspunkt-Standortsystemrollen voraussetzt, werden nicht mehr alle Verteilungspunkte zur gleichen Zeit offline geschaltet. Stattdessen verwendet der Standortserver die Einstellungen des Standorts zur Inhaltsverteilung, um das Update zu einem beliebigen gegebenen Zeitpunkt auf eine Teilmenge von Verteilungspunkten zu verteilen. Das bedeutet, dass nur manche Verteilungspunkte nach der Installation des Updates offline geschaltet werden. Dadurch können Verteilungspunkte, die noch nicht aktualisiert wurden oder bei denen das Update schon abgeschlossen ist, online bleiben und Inhalt an Clients bereitstellen.



## <a name="accessibility"></a><a name="accessibility"></a> Barrierefreiheit
Zum Navigieren zwischen den verschiedenen Knoten eines Arbeitsbereichs können Sie nun den ersten Buchstaben des Namen eines Knotens eingeben. Jeder Tastendruck verschiebt den Cursor auf den nächsten Knoten, der mit diesem Buchstaben beginnt. Für Benutzer, die eine Sprachausgabe haben, liest der Reader den Namen des Knotens. Weitere Informationen zur Barrierefreiheit finden Sie unter [Barrierefreiheitsfunktionen](../../../core/understand/accessibility-features.md).

## <a name="administration"></a><a name="administration"></a>Verwaltung
Im folgenden finden Sie Änderungen an der Verwaltung in der Configuration Manager-Konsole:
### <a name="oms-connector"></a>OMS-Connector

Sie können jetzt Configuration Manager als Sammlungen von Configuration Manager aus mit [Microsoft Operations Management Suite (OMS)](/azure/azure-monitor/overview) verbinden. Dadurch werden Daten, wie z.B. Sammlungen von Configuration Manager in OMS sichtbar dargestellt. Weitere Informationen finden Sie unter [Synchronisieren von Daten von System Center Configuration Manager mit der Microsoft Operations Management Suite](/azure/azure-monitor/platform/collect-sccm).

Der OMS-Connector ist ein vorab veröffentlichtes Feature. Wie Sie es aktivieren, erfahren Sie unter [Features der Vorabversion in System Center Configuration Manager](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease).

### <a name="support-for-cache-size-in-client-settings"></a>Unterstützen der Cachegröße in den Clienteinstellungen

Sie können jetzt die Größe des Cacheordners auf Clientcomputern mit **Clienteinstellungen** in der Configuration Manager-Konsole konfigurieren. Bisher konnten Sie die Cachegröße des Clients nur beim Installieren oder Neuinstallieren der Clientsoftware festlegen. Jetzt können Sie die Cachegröße als Clienteinstellung (Standardeinstellung oder benutzerdefinierte Einstellung) angeben und diese Einstellungen dann in der nächsten Richtlinienaktualisierung auf den Client anwenden, ohne den Client vorher neu installieren zu müssen. Weitere Informationen finden Sie unter [Konfigurieren des Clientcaches für Configuration Manager-Clients](../../../core/clients/manage/manage-clients.md#BKMK_ClientCache).

## <a name="on-premises-mobile-device-management"></a>Lokale Verwaltung mobiler Geräte

### <a name="support-for-multiple-device-management-points"></a>Unterstützung für mehrere Geräteverwaltungspunkte

Die lokale Verwaltung mobiler Geräte (On-premises Mobile Device Management, MDM) unterstützt jetzt eine neue Funktion in Windows 10 Anniversary Update, die automatisch ein registriertes Gerät so konfiguriert, dass mehr als ein Geräteverwaltungspunkt zur Verwendung zur Verfügung steht. Diese Funktion lässt Fallbacks des Geräts auf einen anderen Geräteverwaltungspunkt zu, wenn der normalerweise verwendete Punkt nicht verfügbar ist. Diese Funktion ist nur auf PCs und Geräten verfügbar, auf denen Windows 10 Anniversary Update installiert ist.


## <a name="application-management"></a>Anwendungsverwaltung

### <a name="manage-apps-from-the-windows-store-for-business"></a>Verwalten von Apps aus dem Windows Store für Unternehmen

Im [Windows Store für Unternehmen](https://www.microsoft.com/business-store) können Sie Windows-Apps für Ihre Organisation finden und entweder einzeln oder per Volumenlizenz kaufen. Durch Herstellen einer Verbindung des Store mit Configuration Manager können Sie die Liste der Apps, die Sie erworben haben, mit Configuration Manager synchronisieren, sie in der Configuration Manager-Konsole anzeigen und wie jede andere App auch bereitstellen.

Einzelheiten finden Sie unter [Verwalten von Apps aus dem Microsoft Store für Unternehmen mit Configuration Manager](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

### <a name="manage-ios-volume-purchased-apps"></a>Verwalten von iOS-Apps aus einem Volumenprogramm

Der Workflow zum Verwalten von iOS-Apps, die per Volumenlizenz gekauft wurden, und zum Bereitstellen der Apps mit Configuration Manager wurde verbessert.


### <a name="software-center-user-interface"></a>Benutzeroberfläche des Softwarecenters

Die Benutzeroberfläche des Softwarecenters wurde im Hinblick auf eine einfachere Ermittlung optimiert.
*  Die Registerkarten **Installationsstatus** und **Installierte Software** wurden auf der Registerkarte **Installationsstatus** zusammengefasst.
*  **Updates**, **Betriebssysteme** und **Anwendungen** wurden auf drei separate Registerkarten aufgeteilt.
* Es können jetzt mehrere Updates auf einmal zur Installation ausgewählt werden, oder alle Updates können auf einmal installiert werden, indem Sie auf die Schaltfläche **Install All** (Alle installieren) klicken.

### <a name="content-status-links"></a>Verknüpfungen zum Inhaltsstatus
Die Eigenschaften einer Anwendung oder eines Pakets bieten nun einen Link, über den Sie den Status des zugehörigen Objekts aufrufen können.

## <a name="software-updates"></a>Softwareupdates

### <a name="client-setting-to-manage-the-office-365-client-agent"></a>Clienteinstellung zum Verwalten des Office 365-Client-Agent
Sie können jetzt eine Clienteinstellung von Configuration Manager verwenden, um den Office 365-Client-Agent zu verwenden. Nachdem Sie dies eingerichtet und Updates für Office 365 bereitgestellt haben, arbeitet der Configuration Manager-Client-Agent mit dem Office 365-Client-Agent zusammen, um Office 365-Updates von einem Verteilungspunkt herunterzuladen und zu installieren.

Einzelheiten finden Sie unter [Manage Office 365 ProPlus updates with Configuration Manager (Verwalten von Office 365 ProPlus-Updates mit System Center Configuration Manager)](../../../sum/deploy-use/manage-office-365-proplus-updates.md).

### <a name="manually-switch-clients-to-a-new-software-update-point"></a>Manuelles Wechseln von Clients auf einen neuen Softwareupdatepunkt
Sie können jetzt eine Option aktivieren, die Configuration Manager-Clients den Wechsel zu einem neuen Softwareupdatepunkt ermöglichen, wenn beim aktiven Softwareupdatepunkt Probleme auftreten. Nach der Aktivierung suchen die Clients nach anderen Softwareupdatepunkten bei der nächsten Überprüfung.

Einzelheiten finden Sie unter [Plan for software updates in Configuration Manager (Planen von Softwareupdates in Configuration Manager)](../../../sum/plan-design/plan-for-software-updates.md#BKMK_ManuallySwitchSUPs).

### <a name="restart-options-for-windows-10-clients-after-software-update-installation"></a>Neustartoptionen für Windows 10-Clients nach der Installation von Softwareupdates
Wenn ein Softwareupdate, das einen Neustart benötigt, mit Configuration Manager bereitgestellt und auf einem Computer installiert wird, wird ein ausstehender Neustart geplant. Ein Dialogfeld für den Neustart wird ebenfalls angezeigt. Ab Version 1606 von Configuration Manager sind die Optionen **Aktualisieren und neu starten** sowie **Aktualisieren und herunterfahren** bei jedem ausstehenden Neustart für ein Configuration Manager-Softwareupdate verfügbar. Die Optionen sind in den Windows-Energieoptionen von Windows 10-Computern verfügbar. Nach der Verwendung einer dieser Optionen, wird das Dialogfeld „Neustart“ nicht nach dem Neustart des Computers angezeigt.

Mehr Informationen finden Sie unter [Planen von Softwareupdates](../../../sum/plan-design/plan-for-software-updates.md#BKMK_RestartOptions).

### <a name="run-software-updates-compliance-scan-immediately-after-a-client-installs-software-updates-and-restarts"></a>Ausführen von Softwareupdate-Konformitätsprüfungen unmittelbar nach der Installation von Softwareupdates und dem Neustart eines Clients
Sie können nun eine Konformitätsprüfung unmittelbar nach der Installation von Softwareupdates und dem Neustart eines Clients ausführen. Wählen Sie auf der Seite **Benutzerfreundlichkeit** des Assistenten zum Bereitstellen von Softwareupdates die Option **Nach dem Neustart Auswertungszyklus für Updatebereitstellung ausführen, wenn ein Update in dieser Bereitstellung einen Systemneustart erfordert** aus, um dies für eine Bereitstellung zu konfigurieren. Der Client kann dann nach zusätzlichen Softwareupdates suchen, die nach dem Neustart des Clients relevant werden, und diese im gleichen Wartungsfenster installieren (und so für Konformität sorgen). Weitere Informationen finden Sie unter [Automatisches Bereitstellen von Softwareupdates](../../../sum/deploy-use/automatically-deploy-software-updates.md) oder [Manuelles Bereitstellen von Softwareupdates](../../../sum/deploy-use/manually-deploy-software-updates.md).

## <a name="operating-system-deployment"></a>Betriebssystembereitstellung

### <a name="improvements-to-the-task-sequence-step-install-software-updates"></a>Verbesserungen am Schritt zum Ausführen der Tasksequenz: Softwareupdates installieren
Eine neue Einstellung, **Softwareupdates anhand von zwischengespeicherten Überprüfungsergebnissen auswerten**, bietet Ihnen die Möglichkeit, eine vollständige Überprüfung für Softwareupdates durchzuführen, anstatt die zwischengespeicherten Überprüfungsergebnisse zu verwenden. Weitere Informationen finden Sie unter [Tasksequenzschritte](../../../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates).

Darüber hinaus ist eine neue Aufgabensequenzvariable, **SMSTSSoftwareUpdateScanTimeout**, verfügbar. Die Variable bietet Ihnen die Möglichkeit, das Timeout für die Überprüfung auf Softwareupdates während des Tasksequenzschritts „Softwareupdates installieren“ zu steuern. Der Standardwert beträgt 30 Minuten. Weitere Informationen finden Sie unter [Verwenden von Tasksequenzvariablen](../../../osd/understand/task-sequence-variables.md).

### <a name="osdpreservedriveletter-task-sequence-variable-has-been-deprecated"></a>Tasksequenzvariable „OSDPreserveDriveLetter“ als veraltet markiert
Die Tasksequenzvariable „OSDPreserveDriveLetter“ wurde als veraltet markiert. Ab Configuration Manager Version 1606 bestimmt Windows Setup standardmäßig den Laufwerkbuchstaben, der während der Bereitstellung eines Betriebssystems am besten verwendet wird (in der Regel C:).

Weitere Informationen finden Sie unter [Verwenden von Tasksequenzvariablen](../../../osd/understand/task-sequence-variables.md).

### <a name="customize-the-ramdisk-tftp-window-size-for-pxe-enabled-distribution-points"></a>Anpassen der RamDisk-TFTP-Fenstergröße für PXE-fähige Verteilungspunkte
Sie können jetzt die RamDisk-TFTP-Fenstergröße für PXE-fähige Verteilungspunkte anpassen. Wenn Sie Ihr Netzwerk angepasst haben, kann dies wegen des zu großen Fensters zu einem Timeout beim Herunterladen des Startimages führen. Durch Anpassen der Fenstergröße von RamDisk Trivial File Transfer Protocol (TFTP) können Sie den TFTP-Datenverkehr bei Verwendung von PXE für Ihre spezifischen Netzwerkanforderungen optimieren.

Einzelheiten finden Sie unter [Vorbereiten von Standortsystemrollen für Betriebssystembereitstellungen mit Configuration Manager](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP).

## <a name="compliance-settings"></a>Kompatibilitätseinstellungen

### <a name="smart-lock-setting-for-android-devices"></a>Smart Lock-Einstellung für Android-Geräte
Eine neue Einstellung, **Zulassen von Smart Lock und anderen Vertrauens-Agents**, wurde dem Konfigurationselement Android und Samsung KNOX Standard hinzugefügt.

Mit dieser Einstellung können Sie die Smart Lock-Funktion auf kompatiblen Android-Geräten steuern. Diese Telefonfunktion wird manchmal als Vertrauens-Agent bezeichnet und ermöglicht Ihnen, das Kennwort für den Gerätesperrbildschirm zu deaktivieren oder zu umgehen, wenn sich das Gerät an einem vertrauenswürdigen Standort befindet. Beispiel: Ein vertrauenswürdiger Speicherort kann bei Verbindung mit einem bestimmten Bluetooth-Gerät oder der Nähe eines NFC-Tags gegeben sein. Mit dieser Einstellung können Sie verhindern, dass Benutzer Smart Lock konfigurieren.


## <a name="device-configuration-and-protection"></a>Gerätekonfiguration und -schutz

### <a name="product-name-changes"></a>Änderungen des Produktnamens

* „Microsoft Passport for Work“ wird jetzt **Windows Hello for Business** genannt.
* Unternehmensdatenschutz wird jetzt **Windows Information Protection** genannt.

### <a name="deployment-of-windows-hello-for-business-passport-for-work"></a>Bereitstellung von „Windows Hello for Business“ (Passport for Work)

Sie können jetzt Richtlinien von „Windows Hello for Business“ für Windows 10-Geräte bereitstellen, die in eine Domäne eingebunden sind, und vom Configuration Manager-Client verwaltet werden.

Die Configuration Manager-Konsole wurde aktualisiert, um diese Änderungen widerzuspiegeln.

### <a name="ios-activation-lock"></a>iOS-Aktivierungssperre
Configuration Manager kann Sie beim Verwalten der iOS-Aktivierungssperre unterstützen, einem Feature der App „Mein iPhone suchen“ für iOS 7.1 und höher. Wenn die Aktivierungssperre aktiviert ist, müssen die Apple-ID und das Kennwort des Benutzers eingegeben werden, bevor folgende Vorgänge möglich sind:
* Deaktivieren Sie „Mein iPhone suchen“.
* Löschen Sie das Gerät.
* Reaktivieren Sie das Gerät.

Configuration Manager hilft Ihnen dabei, die Aktivierungssperre zu verwalten. Dazu gibt es zwei Möglichkeiten:

- Aktivieren der Aktivierungssperre auf überwachten Geräten.
- Umgehen der Aktivierungssperre auf überwachten Geräten.


### <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender Advanced Threat Protection

Endpoint Protection kann Sie beim Verwalten und Überwachen von Microsoft Defender Advanced Threat Protection (ATP) unterstützen. Microsoft Defender ATP ist ein neuer Dienst, der Unternehmen dabei unterstützt, erweiterte Angriffe auf ihre Netzwerke zu entdecken, zu untersuchen, und darauf zu reagieren. Richtlinien von Configuration Manager können Sie dabei unterstützen, verwaltetes Windows 10, Version 1607, (Build 14328) oder höher zu integrieren und zu verwalten.

Einzelheiten finden Sie unter [Microsoft Defender Advanced Threat Protection](../../../protect/deploy-use/defender-advanced-threat-protection.md).

### <a name="device-categories"></a>Gerätekategorien
Sie können Gerätekategorien erstellen, mit denen Geräte automatisch in Gerätesammlungen platziert werden, wenn Sie Configuration Manager mit Microsoft Intune verwenden. Benutzer müssen eine Gerätekategorie auswählen, wenn sie ein Gerät in Intune registrieren. Sie können außerdem die Kategorie eines Geräts in der Configuration Manager-Konsole ändern.

Einzelheiten finden Sie unter [Automatisches Kategorisieren von Geräten in Sammlungen](../../../core/clients/manage/collections/automatically-categorize-devices-into-collections.md).

### <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Vorabdeklarieren von Geräten mit IMEI- oder iOS-Seriennummern

Sie können unternehmenseigene Geräte identifizieren, indem Sie deren IMEI-Nummern (International Station Mobile Equipment Identity) oder iOS-Seriennummern importieren. Sie können eine CSV-Datei (comma-separated values, durch Trennzeichen getrennte Datei) hochladen, die die IMEI-Nummern der Geräte enthält, oder Geräteinformationen manuell eingeben. Importierte Informationen legen den Besitz der registrierten Geräte in der Liste der Geräte auf „Unternehmen“ fest. Dennoch wird für jeden Benutzer, der auf den Dienst zugreift, eine Intune-Lizenz benötigt.

### <a name="on-premises-health-attestation-service-communication"></a>Lokale Kommunikation mit dem Integritätsnachweisdienst

Sie können jetzt Überwachung durch Integritätsnachweisdienste für Windows 10-PCs aktivieren, die nur die lokale Infrastruktur verwenden, damit Computer ohne Internetzugang den Nachweis der Geräteintegrität (Device Health Attestation, DHA) melden können.

Weitere Informationen finden Sie unter [Integritätsnachweis für Configuration Manager](../../../core/servers/manage/health-attestation.md#how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers).  

## <a name="remote-control"></a>Remotesteuerung
Geben Sie Benutzern die Möglichkeit, Datenübertragungen zu akzeptieren oder zu verweigern, bevor Inhalt aus der freigegebenen Zwischenablage in einer Remotesteuerungssitzung übertragen wird. Benutzer müssen nur einmal pro Sitzung die Berechtigung erteilen, und die anzeigenden Benutzer können sich nicht selbst die Erlaubnis erteilen, mit der Datenübertragung fortzufahren. Sie finden diese neue Einstellung im Arbeitsbereich **Verwaltung**. Wechseln Sie zu **Clienteinstellungen**, und öffnen Sie dann in **Standardeinstellungen** den Bereich **Remotetools**.