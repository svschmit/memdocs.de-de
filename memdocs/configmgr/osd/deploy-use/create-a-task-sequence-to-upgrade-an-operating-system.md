---
title: Erstellen einer Upgradetasksequenz für ein Betriebssystem
titleSuffix: Configuration Manager
description: Automatisches Upgrade von Windows 7 oder höher auf Windows 10 mithilfe einer Tasksequenz
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6ad36978f3f3dc5207068a65d76bf8f5c7c3078c
ms.sourcegitcommit: e2ef7231d3abaf3c925b0e5ee9f66156260e3c71
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/26/2020
ms.locfileid: "85383239"
---
# <a name="create-a-task-sequence-to-upgrade-an-os-in-configuration-manager"></a>Erstellen einer Tasksequenz zum Durchführen eines Upgrades für ein Betriebssystem in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Verwenden Sie Tasksequenzen in Configuration Manager, um automatisch ein Upgrade eines Betriebssystems auf einem Zielcomputer auszuführen. Sie können dieses Upgrade von Windows 7 oder höher auf Windows 10 oder von Windows Server 2012 oder höher auf Windows Server 2016 durchführen. Erstellen Sie eine Tasksequenz, die auf das Upgradepaket für das Betriebssystem oder jegliche anderen Inhalte verweist, die installiert werden sollen, z.B. Anwendungen oder Softwareupdates. Die Tasksequenz zum Durchführen eines Upgrades für ein Betriebssystem ist Teil des Szenarios [Upgrade von Windows auf die neueste Version](upgrade-windows-to-the-latest-version.md).  


## <a name="prerequisites"></a>Voraussetzungen

Bevor Sie die Tasksequenz erstellen, müssen folgende Anforderungen erfüllt sein:

### <a name="required"></a>Erforderlich

- Das [Upgradepaket für das Betriebssystem](../get-started/manage-operating-system-upgrade-packages.md) muss in der Configuration Manager-Konsole verfügbar sein.  

- Wenn Sie ein Upgrade auf Windows Server 2016 durchführen, müssen Sie im Tasksequenzschritt „Betriebssystem aktualisieren“ die Einstellung **Ignore any dismissable compatibility messages** (Alle verwerfbaren Konformitätsmeldungen ignorieren) auswählen. Andernfalls tritt beim Upgrade ein Fehler auf.  

### <a name="required-if-used"></a>Erforderlich (sofern verwendet)  

- [Softwareupdates](../../sum/get-started/synchronize-software-updates.md) müssen in der Configuration Manager-Konsole synchronisiert werden.  

- [Anwendungen](../../apps/deploy-use/create-applications.md) müssen zur Configuration Manager-Konsole hinzugefügt werden.  


## <a name="create-a-task-sequence-to-upgrade-an-os"></a><a name="BKMK_UpgradeOS"></a> Erstellen einer Tasksequenz zum Durchführen eines Betriebssystemupgrades  

Erstellen Sie eine Tasksequenz, und wählen Sie im Tasksequenzerstellungs-Assistent die Option **Upgrade an operating system from upgrade package** (Upgrade eines Betriebssystems mit einem Upgradepaket durchführen) aus, um ein Betriebssystemupgrade für Clients durchzuführen. Der Assistent fügt die Tasksequenzschritte zum Durchführen des Betriebssystemupgrades, zum Anwenden von Softwareupdates und zum Installieren von Anwendungen hinzu.

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und wählen Sie anschließend **Tasksequenzen** aus.  

2. Wählen Sie auf der Registerkarte **Start** des Menübands in der Gruppe **Erstellen** die Option **Tasksequenz erstellen** aus.  

3. Wählen Sie auf der Seite **Neue Tasksequenz erstellen** des Tasksequenzerstellungs-Assistenten **Ein Betriebssystem mithilfe eines Aktualisierungspakets aktualisieren** und dann **Weiter** aus.  

4. Geben Sie auf der Seite **Informationen zur Tasksequenz** die folgenden Einstellungen an:  

    - **Tasksequenzname:** Geben Sie einen Namen zur Identifikation der Tasksequenz an.  

    - **Beschreibung:** Geben Sie optional eine Beschreibung an.  

5. Geben Sie auf der Seite **Windows-Betriebssystem aktualisieren** die folgenden Einstellungen an:  

    - **Upgradepaket:** Geben Sie das Upgradepaket an, das die Quelldateien für das Upgrade des Betriebssystems enthält. Überprüfen Sie, ob Sie das richtige Paket ausgewählt haben, indem Sie die Informationen im Bereich **Eigenschaften** betrachten. Weitere Informationen finden Sie unter [Verwalten von Betriebssystem-Upgradepaketen](../get-started/manage-operating-system-upgrade-packages.md).  

    - **Editionsindex:** Wenn mehrere Editionsindizes für das Betriebssystem im Paket verfügbar sind, wählen Sie den gewünschten Editionsindex aus. Der Assistent wählt standardmäßig den ersten Index aus.  

    - **Product Key:** Geben Sie den Windows-Product Key für das zu installierende Betriebssystem an. Geben Sie codierte Volumenlizenzschlüssel oder Standard-Product Keys an. Wenn Sie einen Standard-Product Key verwenden, trennen Sie jede Gruppe von fünf Zeichen durch einen Bindestrich (`-`). Beispiel: `XXXXX-XXXXX-XXXXX-XXXXX-XXXXX`. Wenn das Upgrade für eine Volumenlizenzedition vorgesehen ist, ist der Product Key möglicherweise nicht erforderlich.  

        > [!Note]  
        > Dieser Product Key kann ein Mehrfachaktivierungsschüssel oder ein generischer Volumenlizenzschlüssel sein. Ein generischer Volumenlizenzschlüssel wird auch als Clientsetupschlüssel für den Schlüsselverwaltungsdienst (KMS) bezeichnet. Weitere Informationen finden Sie unter [Planen der Volumenaktivierung](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). Eine Liste der KMS-Clientsetupschlüssel finden Sie im Windows Server-Aktivierungshandbuch in [Anhang A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys).

    - **Alle ablehnbaren Kompatibilitätsmeldungen ignorieren:** Wählen Sie diese Einstellung aus, wenn Sie ein Upgrade auf Windows Server 2016 durchführen. Wenn Sie diese Einstellung nicht auswählen, kann die Tasksequenz nicht abgeschlossen werden, weil Windows Setup darauf wartet, dass der Benutzer in einem Bestätigungsdialogfeld in einer Windows-App **Bestätigen** auswählt.  

6. Geben Sie auf der Seite **Updates einschließen** an, ob erforderliche, alle oder keine Softwareupdates installiert werden sollen. Klicken Sie dann auf **Weiter**. Wenn Sie angeben, dass Softwareupdates installiert werden sollen, werden von Configuration Manager nur die Updates installiert, die für Sammlungen bestimmt sind, in denen der Zielcomputer ein Mitglied ist.  

7. Geben Sie auf der Seite **Anwendungen installieren** die Anwendungen an, die auf dem Zielcomputer installiert werden sollen, und wählen Sie dann **Weiter** aus. Wenn Sie mehr als eine Anwendung auswählen, geben Sie auch an, ob die Tasksequenz fortgesetzt werden soll, wenn die Installation einer bestimmten Anwendung fehlschlägt.  

8. Schließen Sie den Assistenten ab.  

> [!Important]  
> Wenn die Tasksequenz auf einem Gerät ausgeführt wird, erstellt der Konfigurations-Manager-Client mehrere Skripts zum Steuern des Verhaltens der Tasksequenz in verschiedenen Szenarios. Wenn die Tasksequenz abgeschlossen ist, entfernt der Client diese Skripts nicht, bis der Computer neu gestartet wird. Diese Skriptdateien enthalten keine vertraulichen Informationen.  

Die Standardvorlage der Tasksequenz für das direkte Windows 10-Upgrade enthält zusätzliche Gruppen mit empfohlenen Aktionen, die vor und nach dem Upgradevorgang hinzugefügt werden können. Diese Aktionen werden häufig von Kunden eingesetzt, die erfolgreiche Upgrades ihrer Geräte auf Windows 10 durchführen. Weitere Informationen finden Sie in den empfohlenen Tasksequenzschritten [zum Vorbereiten des Upgrades](#recommended-task-sequence-steps-to-prepare-for-upgrade) und [zur Nachbearbeitung](#recommended-task-sequence-steps-for-post-processing).

Ab Version 1806 enthält diese Tasksequenzvorlage auch eine Gruppe mit Aktionen, die empfohlen werden, wenn der Upgradeprozess fehlschlägt. Diese Aktionen erleichtern die Problembehandlung. Weitere Informationen finden Sie unter [Empfohlene Tasksequenzschritte bei Fehlern](#recommended-task-sequence-steps-on-failure).<!--1358500-->  


## <a name="configure-pre-cache-content"></a>Konfigurieren des zwischengespeicherten Inhalts

<!--1021244-->
Clients können mithilfe des Features zum Vorabzwischenspeichern für verfügbare Bereitstellungen von Tasksequenzen relevante Betriebssystem-Upgradepakete herunterladen, bevor der Benutzer die Tasksequenz installiert.  

Weitere Informationen finden Sie unter [Konfigurieren des zwischengespeicherten Inhalts](configure-precache-content.md).


## <a name="recommended-task-sequence-steps-to-prepare-for-upgrade"></a>Empfohlene Tasksequenzschritte zur Vorbereitung von Upgrades

Die Standardvorlage der Tasksequenz für das direkte Windows 10-Upgrade enthält zusätzliche Gruppen mit empfohlenen Aktionen, die vor dem Upgradevorgang hinzugefügt werden können. Diese Aktionen in der Gruppe **Vorbereitung auf das Upgrade** werden häufig von Kunden eingesetzt, die erfolgreiche Upgrades ihrer Geräte auf Windows 10 durchführen. Wenn es bereits eine Tasksequenz gibt, die diese Aktionen noch nicht enthält, fügen Sie diese der Tasksequenz in der Gruppe **Vorbereitung auf das Upgrade** manuell hinzu.  

### <a name="battery-checks"></a>Stromversorgung überprüfen

Hiermit fügen Sie dieser Gruppe Schritte hinzu, um zu überprüfen, ob der Computer sich im Akku- oder Netzbetrieb befindet. Für diese Aktion ist ein benutzerdefiniertes Skript oder ein Hilfsprogramm erforderlich, um diese Prüfung auszuführen.

#### <a name="battery-check-example"></a>Beispiel einer Überprüfung der Stromversorgung

Verwenden Sie WbemTest, und stellen Sie eine Verbindung mit dem Namespace `root\cimv2` her. Führen Sie dann die folgende Abfrage aus:

`Select BatteryStatus From Win32_Battery where BatteryStatus != 2`

Wenn sie keine Ergebnisse zurückgibt, wird das Gerät im Akkubetrieb ausgeführt. Andernfalls ist das Gerät an eine kabelgebundene Stromversorgung angeschlossen.  

### <a name="networkwired-connection-checks"></a>Netzwerk-/Drahtlosverbindung überprüfen

Fügen Sie dieser Gruppe Schritte hinzu, um sicherzustellen, dass der Computer keine Drahtlos-, sondern eine Netzwerkverbindung verwendet. Für diese Aktion ist ein benutzerdefiniertes Skript oder ein Hilfsprogramm erforderlich, um diese Prüfung auszuführen.

#### <a name="network-check-example"></a>Beispiel einer Netzwerküberprüfung

Verwenden Sie WbemTest, und stellen Sie eine Verbindung mit dem Namespace `root\cimv2` her. Führen Sie dann die folgende Abfrage aus:

`Select * From Win32_NetworkAdapter Where NetConnectionStatus = 2 and PhysicalAdapter = 'True' and NetConnectionID = 'Wi-Fi'`

Wenn sie keine Ergebnisse zurückgibt, wird das Gerät im WLAN ausgeführt. Andernfalls weist das Gerät eine kabelgebundene Netzwerkverbindung auf.

### <a name="remove-incompatible-applications"></a>Inkompatible Anwendungen entfernen

Hiermit fügen Sie dieser Gruppe Schritte hinzu, um alle Anwendungen zu entfernen, die nicht mit dieser Version von Windows 10 kompatibel sind. Die Methoden zum Deinstallieren einer Anwendung variieren.  

Wenn die Anwendung den Windows Installer verwendet, kopieren Sie die Befehlszeile **Programm deinstallieren** von der Registerkarte **Programme** in den Eigenschaften des Windows Installer-Bereitstellungstyps der Anwendung. Fügen Sie dann in diese Gruppe mit der Befehlszeile zum Deinstallieren des Programms einen Schritt **Befehlszeile ausführen** ein. Beispiel:

`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`  

### <a name="remove-incompatible-drivers"></a>Inkompatible Treiber entfernen

Hiermit fügen Sie dieser Gruppe Schritte hinzu, um alle Treiber zu entfernen, die nicht mit dieser Version von Windows 10 kompatibel sind.  

### <a name="removesuspend-third-party-security"></a>Sicherheitsprogramme von Drittanbietern entfernen/anhalten

Hiermit fügen Sie dieser Gruppe Schritte hinzu, um Sicherheitsprogramme von Drittanbietern – z.B. Antivirenprogramme – zu entfernen.  

Wenn Sie ein Drittanbieterprogramm zur Datenträgerverschlüsselung verwenden, geben Sie den Verschlüsselungstreiber in Windows Setup mit der [Befehlszeilenoption](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#reflectdrivers) `/ReflectDrivers` an. Fügen Sie der Tasksequenz in dieser Gruppe einen Schritt [Tasksequenzvariable festlegen](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) hinzu. Legen Sie die Tasksequenzvariable auf **OSDSetupAdditionalUpgradeOptions** fest. Legen Sie den Wert auf `/ReflectDrivers` mit dem Pfad zum Treiber fest. Diese [Tasksequenzvariable](../understand/task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions) fügt die von der Tasksequenz verwendete Windows Setup-Befehlszeile an. Wenden Sie sich an den Anbieter Ihrer Software, um weitere Informationen zu diesem Vorgang zu erhalten.  

### <a name="download-package-content-task-sequence-step"></a>Paketinhalt herunterladen – Tasksequenzschritt  

Führen Sie den Schritt [Paketinhalt herunterladen](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) in den folgenden Szenarios vor dem Schritt **Betriebssystem aktualisieren** aus:  

- Sie verwenden eine einzelne Upgradetasksequenz, die sowohl für x86- als auch für x64-Plattformen verwendet werden kann. Fügen Sie der Gruppe **Vorbereitung auf das Upgrade** zwei **Paketinhalt herunterladen**-Schritte hinzu. Legen Sie für jeden Schritt Bedingungen fest, um die Clientarchitektur zu ermitteln. Diese Bedingung hat zur Folge, dass in diesem Schritt nur das passende Upgradepaket für das Betriebssystem heruntergeladen wird. Konfigurieren Sie jeden **Paketinhalt herunterladen** -Schritt zur Verwendung derselben Variablen, und verwenden Sie die Variable für den Medienpfad im Schritt **Betriebssystem aktualisieren** .  

- Um dynamisch ein passendes Treiberpaket herunterzuladen, verwenden Sie zwei **Paketinhalt herunterladen** -Schritte mit Bedingungen zum Ermitteln des geeigneten Hardwaretyps für jedes Treiberpaket. Konfigurieren Sie jeden **Paketinhalt herunterladen**-Schritt, sodass dieselbe Variable verwendet wird. Verwenden Sie anschließend diese Variable für den Wert **Bereitgestellter Inhalt** im Abschnitt „Treiber“ des Schritts **Betriebssystem aktualisieren**.  

    > [!NOTE]  
    > Configuration Manager fügt diesem Variablennamen ein numerisches Suffix hinzu. Wenn Sie beispielsweise `%mycontent%` als benutzerdefinierte Variable festlegen, speichert der Client an diesem Speicherort sämtlichen Inhalt, auf den verwiesen wird. Wenn Sie in einem späteren Schritt auf die Variable verweisen, z.B. **Betriebssystem aktualisieren**, verwenden Sie die Variable mit einem numerischen Suffix. In diesem Beispiel wird `%mycontent01%` oder `%mycontent02%` verwendet, wobei die Nummer der Reihenfolge entspricht, in der diese Inhalte im Schritt **Paketinhalt herunterladen** aufgelistet sind.  


## <a name="recommended-task-sequence-steps-for-post-processing"></a>Empfohlene Tasksequenzschritte für die Nachbearbeitung

Nachdem Sie die Tasksequenz erstellt haben, fügen Sie diese zusätzlichen Schritte in der Gruppe **Nachbearbeitung** der Tasksequenz hinzu.  

> [!NOTE]  
> Diese Tasksequenz ist nicht linear. Es gibt Bedingungen für die einzelnen Schritte, die sich auf die Ergebnisse der Tasksequenz auswirken können. Dieses Verhalten hängt davon ab, ob das Upgrade des Clientcomputers erfolgreich verläuft oder ob ein Rollback auf das ursprüngliche Betriebssystem ausgeführt werden muss.  

Die Standardvorlage der Tasksequenz für das direkte Windows 10-Upgrade enthält zusätzliche Gruppen mit empfohlenen Aktionen, die nach dem Upgradevorgang hinzugefügt werden können. Diese Aktionen in der Gruppe **Nachbearbeitung** werden häufig von Kunden eingesetzt, die erfolgreiche Upgrades ihrer Geräte auf Windows 10 durchführen. Wenn es bereits eine Tasksequenz gibt, die diese Aktionen noch nicht enthält, fügen Sie diese der Tasksequenz in der Gruppe **Nachbearbeitung** manuell hinzu.  

### <a name="apply-setup-based-drivers"></a>Setupbasierte Treiber anwenden

Hiermit fügen Sie dieser Gruppe Schritte hinzu, um setupbasierte Treiber (EXE) aus Paketen zu installieren.  

### <a name="installenable-third-party-security"></a>Sicherheitsprogramme von Drittanbietern installieren/aktivieren

Hiermit fügen Sie dieser Gruppe Schritte hinzu, um Sicherheitsprogramme von Drittanbietern – z.B. Antivirenprogramme – zu installieren oder zu aktivieren.  

### <a name="set-windows-default-apps-and-associations"></a>Windows-Standard-Apps und Zuordnungen festlegen

Hiermit fügen Sie dieser Gruppe Schritte hinzu, um Windows-Standard-Apps und Dateizuordnungen festzulegen.

1. Bereiten Sie einen Referenzcomputer mit den gewünschten App-Zuordnungen vor.
1. Führen Sie die folgende Befehlszeile für den Export aus:  
    `dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`  
1. Fügen Sie die XML-Datei zu einem Paket hinzu.
1. Fügen Sie in dieser Gruppe den Schritt [Befehlszeile ausführen](../understand/task-sequence-steps.md#BKMK_RunCommandLine) hinzu. Geben Sie das Paket, das die XML-Datei enthält, sowie die folgende Befehlszeile an:  
    `dism /online /Import-DefaultAppAssociations:DefaultAppAssociations.xml`  

Weitere Informationen finden Sie unter [Exportieren oder Importieren von standardmäßigen Anwendungszuordnungen](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations).

### <a name="apply-customizations-and-personalization"></a>Anpassungen und Personalisierungen anwenden

Hiermit fügen Sie dieser Gruppe Schritte hinzu, um Startmenüanpassungen, z.B. das Organisieren von Programmgruppen, anzuwenden. Weitere Informationen finden Sie unter [Anpassen des Startbildschirms](/windows-hardware/manufacture/desktop/customize-the-start-screen).  


## <a name="optional-task-sequence-steps-for-rollback"></a>Optionale Tasksequenzschritte für ein Rollback  

Wenn nach dem Neustart des Computers ein Fehler beim Upgradevorgang auftreten sollte, führt Windows Setup ein Rollback auf das vorherige Betriebssystem aus. Die Tasksequenz fährt dann mit einem beliebigen Schritt in der **Rollback**-Gruppe fort. Nach dem Erstellen der Tasksequenz können Sie in dieser Gruppe nach Bedarf optionale Schritte hinzufügen. Sie können z.B. alle Änderungen am System in der Gruppe „Prepare for Upgrade“ rückgängig machen, z.B. nicht kompatible Software deinstallieren.


## <a name="recommended-task-sequence-steps-on-failure"></a>Empfohlene Tasksequenzschritte bei Fehlern

<!--1358500-->
Ab Version 1806 enthält die standardmäßige Tasksequenzvorlage für das direkte Windows 10-Upgrade eine Gruppe, mit der Sie **Aktionen bei Fehler ausführen** können. Diese Gruppe enthält empfohlene Aktionen, für den Fall, dass der Upgradeprozess fehlschlägt. Diese Aktionen erleichtern die Problembehandlung.

### <a name="collect-logs"></a>Protokolle sammeln

Um Protokolle auf dem Client zu sammeln, fügen Sie in dieser Gruppe Schritte hinzu.  

- Üblicherweise werden die Protokolldateien in eine Netzwerkfreigabe kopiert. Um diese Verbindung herzustellen, führen Sie den Schritt [Verbindung mit Netzwerkordner herstellen](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder) aus.  

- Um den Kopiervorgang auszuführen, verwenden Sie ein benutzerdefiniertes Skript oder ein Hilfsprogramm zusammen mit dem Schritt [Befehlszeile ausführen](../understand/task-sequence-steps.md#BKMK_RunCommandLine) oder [PowerShell-Skript ausführen](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript).  

- Zu den zu sammelnden Dateien könnten folgende Protokolle zählen:  
     `%_SMSTSLogPath%\*.log`  
     `%SystemDrive%\$Windows.~BT\Sources\Panther\setupact.log`  

- Weitere Informationen zu „setupact.log“ und anderen Windows Setup-Protokollen finden Sie unter [Protokolldateien](https://docs.microsoft.com/windows/deployment/upgrade/log-files).  

- Weitere Informationen zu Konfigurations-Manager-Clientprotokollen finden Sie unter [Konfigurations-Manager-Clientprotokolle](../../core/plan-design/hierarchy/log-files.md#BKMK_ClientLogs).  

- Weitere Informationen zu **_SMSTSLogPath** und anderen nützlichen Variablen finden Sie unter [Tasksequenzvariablen](../understand/task-sequence-variables.md).  

### <a name="run-diagnostic-tools"></a>Diagnosetools ausführen

Fügen Sie zum Ausführen zusätzlicher Diagnosetools Schritte in dieser Gruppe hinzu. Automatisieren Sie diese Tools, um so bald wie möglich nach Auftreten eines Fehlers zusätzliche Informationen aus dem System zu sammeln.  

Ein solches Tool ist Windows [SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag). Mit diesem eigenständigen Diagnosetool können Sie Details zur Ursache des erfolglosen Versuchs eines Windows 10-Upgrades abrufen.  

- Im Configuration Manager [erstellen Sie ein Paket](../../apps/deploy-use/packages-and-programs.md#create-a-package-and-program) für das Tool.  

- Fügen Sie dieser Gruppe Ihrer Tasksequenz den Schritt [Befehlszeile ausführen](../understand/task-sequence-steps.md#BKMK_RunCommandLine) hinzu. Verweisen Sie mit der Option **Paket** auf das Tool. Die folgende Zeichenfolge ist das Beispiel einer **Befehlszeile**:  
    `SetupDiag.exe /Output:"%_SMSTSLogPath%\SetupDiagResults.log"`  

> [!TIP]
> Verwenden Sie stets die neueste Version von SetupDiag, um die neuesten Funktionen und Korrekturen bekannter Probleme zu erhalten. Weitere Informationen finden Sie unter [SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag).

## <a name="additional-recommendations"></a>Weitere Empfehlungen

### <a name="windows-documentation"></a>Windows-Dokumentation

Lesen Sie die Windows-Dokumentation zum [Beheben von Windows 10-Upgradefehlern](https://docs.microsoft.com/windows/deployment/upgrade/resolve-windows-10-upgrade-errors). Dieser Artikel enthält auch detaillierte Informationen zum Upgradeprozess.  

### <a name="check-minimum-disk-space"></a>Überprüfen des Mindestspeicherplatzes

Aktivieren Sie im Standardschritt **Bereitschaft überprüfen** die Option **Mindestens erforderlicher freier Speicherplatz (MB)** . Legen Sie den Wert für das Upgrade eines 32-Bit-Betriebssystems auf mindestens **16384** (16 GB) fest. Für ein 64-Bit-System beträgt der Wert **20480** (20 GB).  

### <a name="retry-downloading-policy"></a>Download der Richtlinie erneut versuchen

Verwenden Sie die [Tasksequenzvariable](../understand/task-sequence-variables.md#SMSTSDownloadRetryCount) **SMSTSDownloadRetryCount**, um erneut zu versuchen, die Richtlinie herunterzuladen. Derzeit ist die Variable standardmäßig auf „2“ festgelegt, der Client unternimmt also zwei Wiederholungsversuche. Wenn Ihre Clients keine kabelgebundene Verbindung zum Intranet verwenden, können weitere Wiederholungen dabei helfen, dass der Client die Richtlinie abrufen kann. Die Verwendung dieser Variablen hat keine negativen Auswirkungen, außer dass ein verzögerter Fehler auftritt, wenn die Richtlinie nicht heruntergeladen werden kann.<!--501016--> Erhöhen Sie auch die Variable **SMSTSDownloadRetryDelay** vom Standardwert „15 Sekunden“.  

### <a name="perform-an-inline-compatibility-assessment"></a>Ausführen einer Inline-Kompatibilitätsbewertung

1. Fügen Sie an einem frühen Punkt in der Gruppe **Für Aktualisierung vorbereiten** einen zweiten Schritt **Betriebssystem aktualisieren** hinzu.  

    1. Nennen Sie den Schritt *Upgradebewertung*.
    1. Geben Sie das gleiche Upgradepaket an, und aktivieren Sie die Option **Kompatibilitätsprüfung für Windows Setup ausführen, ohne Upgrade zu starten**.
    1. Aktivieren Sie **Bei Fehler fortsetzen** auf der Registerkarte „Optionen“.  

1. Fügen Sie unmittelbar nach dem Schritt *Upgradebewertung* einen Schritt **Befehlszeile ausführen** hinzu. Geben Sie die folgende Befehlszeile an:

    `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`

1. Fügen Sie auf der Registerkarte **Optionen** die folgende Bedingung hinzu:

    `Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400`

Dieser Rückgabecode ist die dezimale Entsprechung von MOSETUP_E_COMPAT_SCANONLY (0xC1900210), einer erfolgreichen Kompatibilitätsüberprüfung ohne Fehler. Wenn der Schritt *Upgradebewertung* erfolgreich ausgeführt wurde und diesen Code zurückgibt, überspringt die Tasksequenz diesen Schritt. Wenn der Bewertungsschritt einen anderen Rückgabecode zurückgibt, führt dieser Schritt in der Tasksequenz mit dem Rückgabecode aus der Windows Setup-Kompatibilitätsüberprüfung zu einem Fehler. Weitere Informationen zu **_SMSTSOSUpgradeActionReturnCode** finden Sie unter [Tasksequenzvariablen](../understand/task-sequence-variables.md#SMSTSOSUpgradeActionReturnCode).

Weitere Informationen finden Sie unter [Betriebssystem aktualisieren](../understand/task-sequence-steps.md#BKMK_UpgradeOS).  

### <a name="convert-from-bios-to-uefi"></a>Konvertieren von BIOS in UEFI

Wenn Sie das Gerät während dieser Tasksequenz von BIOS zu UEFI konvertieren möchten, finden Sie weitere Informationen unter [Tasksequenzschritte für das Verwalten einer Konvertierung von BIOS zu UEFI](task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu).  

### <a name="manage-bitlocker"></a>Verwalten von BitLocker

<!--SCCMDocs issue #494-->
Wenn Sie die Datenträgerverschlüsselung von BitLocker verwenden, wird diese während des Upgrades standardmäßig und automatisch durch Windows Setup angehalten. Ab Windows 10-Version 1803 enthält Windows Setup den Befehlszeilenparameter `/BitLocker`, mit dem dieses Verhalten gesteuert werden kann. Wenn Ihre Sicherheitsanforderungen erfordern, dass die Datenträgerverschlüsselung jederzeit aktiviert ist, verwenden Sie die [Tasksequenzvariable](../understand/task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions) **OSDSetupAdditionalUpgradeOptions** in der Gruppe **Vorbereitung auf das Upgrade**, um `/BitLocker TryKeepActive` einzuschließen. Weitere Informationen finden Sie unter [Windows Setup-Befehlszeilenoptionen](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#bitlocker).

### <a name="remove-default-apps"></a>Entfernen von Standard-Apps

<!--SCCMDocs issue #526-->
Einige Kunden entfernen standardmäßig unter Windows 10 bereitgestellte Apps, z.B. die Bing Wetter-App oder die Microsoft Solitaire Collection. In einigen Fällen werden diese Apps durch Windows 10-Updates erneut installiert. Weitere Informationen finden Sie unter [How to keep apps removed from Windows 10 (Verhindern der erneuten Installation von Apps unter Windows 10)](https://docs.microsoft.com/windows/application-management/remove-provisioned-apps-during-update).

Fügen Sie der Tasksequenz den Schritt **Befehlszeile ausführen** in der Gruppe **Vorbereitung auf das Upgrade** hinzu. Geben Sie eine Befehlszeile an, die dem folgenden Beispiel ähnelt:

`cmd /c reg add "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Appx\AppxAllUserStore\Deprovisioned\Microsoft.BingWeather_8wekyb3d8bbwe" /f`
