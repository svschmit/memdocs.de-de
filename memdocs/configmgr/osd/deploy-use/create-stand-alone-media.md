---
title: Erstellen eigenständiger Medien
titleSuffix: Configuration Manager
description: Verwenden Sie eigenständige Medien, um das Betriebssystem auf einem Computer ohne Netzwerkverbindung bereitzustellen.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: c6b9ccd2-78d9-4f0e-b25a-70d0866300ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 57b353dd9dd9fcf7f97d10480f4067bd65a1f483
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697975"
---
# <a name="create-stand-alone-media"></a>Erstellen eigenständiger Medien

*Gilt für: Configuration Manager (Current Branch)*

Eigenständige Medien in Configuration Manager enthalten alles, was zur Bereitstellung des Betriebssystems auf einem Computer ohne Netzwerkverbindung erforderlich ist.

Verwenden Sie eigenständige Medien bei folgenden Szenarien für die Betriebssystembereitstellung:  

- [Aktualisieren eines vorhandenen Computers mit einer neuen Version von Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [Installieren einer neuen Version von Windows auf einem neuen Computer (Bare-Metal)](install-new-windows-version-new-computer-bare-metal.md)  

- [Upgraden von Windows auf die neueste Version](upgrade-windows-to-the-latest-version.md)  


## <a name="usage"></a>Verwendung

Eigenständige Medien enthalten die Tasksequenz, die die Schritte zur Betriebssysteminstallation automatisiert, und alle anderen erforderlichen Inhalte. Zu diesen Inhalten gehören das Startimage, das Betriebssystemimage und Gerätetreiber. Da in den eigenständigen Medien sämtliche Informationen für die Bereitstellung des Betriebssystems gespeichert sind, benötigen sie mehr Speicherplatz als für andere Medientypen erforderlich ist.

Wenn Sie an einem Standort der zentralen Verwaltung eigenständige Medien erstellen, ruft der Client seinen zugewiesenen Standortcode aus Active Directory ab. An einem untergeordneten Standort erstellte eigenständige Medien werden automatisch dem Client und dem Standortcode für diesen Standort zugewiesen.  


## <a name="prerequisites"></a>Voraussetzungen

Vergewissern Sie sich, dass alle der folgenden Bedingungen erfüllt sind, bevor Sie eigenständige Medien mithilfe des Assistenten zum Erstellen von Tasksequenzmedien erstellen:

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Erstellen einer Tasksequenz zum Bereitstellen eines Betriebssystems

Als Teil der eigenständigen Medien müssen Sie die Tasksequenz zum Bereitstellen des Betriebssystems angeben. Weitere Informationen finden Sie unter [Erstellen einer Tasksequenz zum Installieren eines Betriebssystems in System Center Configuration Manager](create-a-task-sequence-to-install-an-operating-system.md).

#### <a name="unsupported-actions-for-stand-alone-media"></a>Nicht unterstützte Aktionen für eigenständige Medien

Die folgenden Aktionen werden für eigenständige Medien nicht unterstützt:

- Der Schritt [Treiber automatisch anwenden](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) in der Tasksequenz. Die automatische Anwendung von Gerätetreibern aus dem Treiberkatalog wird von eigenständigen Medien nicht unterstützt. Verwenden Sie den Schritt [Treiberpaket anwenden](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage), um eine festgelegte Gruppe von Treibern für Windows Setup verfügbar zu machen.  

- Der Schritt [Paketinhalt herunterladen](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) in der Tasksequenz. Die Informationen vom Verwaltungspunkt sind nicht auf eigenständigen Medien verfügbar. Aus diesem Grund tritt bei dem Schritt ein Fehler auf, wenn versucht wird, die Inhaltsspeicherorte aufzulisten.  

- Installieren von Softwareupdates  

- Installieren von Software vor dem Bereitstellen des Betriebssystems  

- Anpassen von Tasksequenzen für Nicht-Betriebssystembereitstellungen  

- Zuweisen von Benutzern zum Zielcomputer, um die Affinität zwischen Benutzer und Gerät zu unterstützen  

- Dynamische Paketinstallationen über den Schritt [Pakete installieren](../understand/task-sequence-steps.md#BKMK_InstallPackage)  

- Dynamische Anwendungsinstallationen über den Schritt [Anwendung installieren](../understand/task-sequence-steps.md#BKMK_InstallApplication)

- Einstellung **Clientpaket vor der Produktion verwenden, wenn verfügbar** im Tasksequenzschritt **Windows und ConfigMgr einrichten** Weitere Informationen zu dieser Einstellung finden Sie unter [Windows und ConfigMgr einrichten](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).  

> [!NOTE]  
> Es kann ein Fehler auftreten, wenn die Tasksequenz den Schritt [Paket installieren](../understand/task-sequence-steps.md#BKMK_InstallPackage) enthält und Sie die eigenständigen Medien an einem Standort der zentralen Verwaltung erstellen. Die erforderlichen Clientkonfigurationsrichtlinien sind für den Standort der zentralen Verwaltung nicht vorhanden. Diese Richtlinien sind erforderlich, um den Softwareverteilungs-Agent während der Ausführung der Tasksequenz zu aktivieren. In der Datei **CreateTsMedia.log** wird möglicherweise der folgenden Fehler angezeigt:  
>
> `WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)`
>
> Bei eigenständigen Medien, die den Schritt **Paket installieren** enthalten, erstellen Sie das eigenständige Medium an einem primären Standort, bei dem der Softwareverteilungs-Agent aktiviert ist.
>
> Verwenden Sie alternativ den benutzerdefinierten Schritt [Befehlszeile ausführen](../understand/task-sequence-steps.md#BKMK_RunCommandLine). Fügen Sie ihn nach dem Schritt [Windows und ConfigMgr einrichten](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) und vor dem ersten Schritt **Paket installieren** hinzu. Im Schritt **Befehlszeile ausführen** wird der folgende WMIC-Befehl ausgeführt, um den Softwareverteilungs-Agent vor dem ersten Schritt „Paket installieren“ zu aktivieren:  
>
> `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Verteilen aller der Tasksequenz zugeordneten Inhalte

Verteilen Sie alle für die Tasksequenz erforderlichen Inhalte auf mindestens einen Verteilungspunkt. Zu diesen Inhalten gehören das Startimage, das Betriebssystemimage und andere dazugehörige Dateien. Die Inhalte werden vom Assistenten beim Erstellen der Medien vom Verteilungspunkt abgerufen.

Ihr Benutzerkonto muss mindestens über **Lesezugriffsrechte** für die Inhaltsbibliothek am Verteilungspunkt verfügen. Weitere Informationen finden Sie unter [Distribute content (Verteilen von Inhalt)](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### <a name="prepare-the-removable-usb-drive"></a>Vorbereiten des USB-Wechseldatenträgers

Wenn Sie einen USB-Speicherstick verwenden, schließen Sie ihn an den Computer an, auf dem Sie den Assistenten zum Erstellen von Tasksequenzmedien ausführen. Der USB-Speicherstick muss für Windows als Wechseldatenträger erkennbar sein. Beim Erstellen der Medien wird vom Assistenten direkt auf den USB-Datenträger geschrieben.

Von eigenständigen Medien wird ein FAT32-Dateisystem verwendet. Sie können keine eigenständigen Medien auf einem entfernbaren USB-Speicherstick erstellen, der eine Datei mit einer Größe von mehr als 4 GB enthält.

### <a name="create-an-output-folder"></a>Erstellen eines Ausgabeordners

Legen Sie für die vom Assistenten zum Erstellen von Tasksequenzmedien erstellten Ausgabedateien einen Ordner an, bevor Sie den Assistenten ausführen, um Medien für einen CD- oder DVD-Satz zu erstellen. Die für einen CD- oder DVD-Satz erstellten Medien werden als ISO-Datei direkt in den Ordner geschrieben.


## <a name="process"></a>Prozess

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und wählen Sie anschließend den Knoten **Tasksequenzen** aus.  

2. Wählen Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Erstellen** die Option **Tasksequenzmedien erstellen** aus. Daraufhin wird der Assistent zum Erstellen von Tasksequenzmedien gestartet.  

3. Geben Sie auf der Seite **Medientyp wählen** folgende Optionen an:  

    - Wählen Sie **Eigenständige Medien**aus.  

    - Optional können Sie **Unbeaufsichtigte Betriebssystembereitstellung zulassen** auswählen, wenn Sie die Bereitstellung des Betriebssystems nur ohne Benutzereingabe gestatten möchten.  

        > [!IMPORTANT]  
        > Wenn Sie diese Option auswählen, wird der Benutzer nicht aufgefordert, Informationen zur Netzwerkkonfiguration oder optionale Tasksequenzen anzugeben. Wenn Sie das Medium für Kennwortschutz konfigurieren, wird der Benutzer aber weiterhin zur Eingabe eines Kennworts aufgefordert.  

4. Auf der Seite **Medientyp** geben Sie an, ob das Medium ein **entfernbarer USB-Speicherstick** oder ein **CD/DVD-Satz** ist: Konfigurieren Sie anschließend die folgenden Optionen:  

    > [!IMPORTANT]  
    > Von Medien wird ein FAT32-Dateisystem verwendet. Sie können keine Medien auf einem USB-Speicherstick erstellen, der eine Datei mit einer Größe von mehr als 4 GB enthält.  

    - Wenn Sie **Entfernbarer USB-Speicherstick** auswählen, wählen Sie das Laufwerk aus, auf dem der Inhalt gespeichert werden soll.  

        - **USB-Wechseldatenträger (FAT32) formatieren und startbar machen**: Standardmäßig wird die Vorbereitung des USB-Laufwerks von Configuration Manager vorgenommen. Viele neuere UEFI-Geräte erfordern eine startbare FAT32-Partition. Dieses Format beschränkt jedoch auch die Größe der Dateien und die Gesamtkapazität des Laufwerks. Wenn Sie den Speicherstick bereits formatiert und konfiguriert haben, deaktivieren Sie diese Option.

    - Wenn Sie **CD/DVD-Satz** auswählen, geben Sie die Kapazität der Medien (**Mediengröße**) sowie den Namen und Pfad der Ausgabedatei (**Mediendatei**) an. Die Ausgabedateien werden vom Assistenten an diesen Speicherort geschrieben. Beispiel: `\\servername\folder\outputfile.iso`  

        Wenn die angegebene Medienkapazität zu gering zum Speichern des gesamten Inhalts ist, werden mehrere Dateien erstellt. Anschließend müssen Sie den Inhalt auf mehreren CDs oder DVDs speichern. Falls mehrere Mediendateien erforderlich sind, wird dem Namen jeder von Configuration Manager erstellten Ausgabedatei eine Sequenznummer hinzugefügt.  

        Die Anwendung wird von Configuration Manager auf mehreren Medien gespeichert, wenn Sie eine Anwendung zusammen mit dem Betriebssystem bereitstellen und die Anwendung nicht auf ein einzelnes Medium passt. Wenn das eigenständige Medium ausgeführt wird, wird der Benutzer von Configuration Manager zum Angeben des nächsten Mediums aufgefordert, auf dem die Anwendung gespeichert ist.  

        > [!IMPORTANT]  
        > Wenn Sie ein vorhandenes ISO-Abbild auswählen, wird dieses ISO-Abbild vom Assistenten zum Erstellen von Tasksequenzmedien auf dem Laufwerk oder der Freigabe gelöscht, sobald Sie mit der nächsten Seite des Assistenten fortfahren. Das vorhandene Abbild wird selbst dann gelöscht, wenn Sie den Assistenten anschließend abbrechen.  

    - **Stagingordner**<!--1359388-->: Der Medienerstellungsprozess kann viel Speicherplatz auf dem temporären Laufwerk erfordern. Dieser ähnelt standardmäßig dem folgenden Pfad: `%UserProfile%\AppData\Local\Temp`. Ab der Version 1902 können Sie das Laufwerk und den Pfad dieses Werts ändern, um bei der Speicherung der temporären Dateien flexibler zu sein.  

    - **Medienbezeichnung**<!--1359388-->: Ab Version 1902 können Sie Tasksequenzmedien eine Bezeichnung hinzufügen. Damit können Sie die Medien besser identifizieren, nachdem Sie sie erstellt haben. Der Standardwert lautet `Configuration Manager`. Dieses Textfeld wird an den folgenden Stellen angezeigt:  

        - Wenn Sie eine ISO-Datei einlegen, zeigt Windows diese Bezeichnung als Namen des eingelegten Laufwerks an.  

        - Wenn Sie ein USB-Laufwerk formatieren, verwendet es die ersten elf Zeichen der Bezeichnung als Namen.  

        - Configuration Manager schreibt eine Textdatei namens `MediaLabel.txt` in das Stammverzeichnis der Medien. Die Datei enthält standardmäßig eine einzelne Textzeile: `label=Configuration Manager`. Wenn Sie die Bezeichnung für Medien anpassen, enthält diese Zeile Ihre benutzerdefinierte Bezeichnung und nicht den Standardwert.  

    - **Datei "autorun.inf" auf Medium einschließen**<!-- 4090666 -->: Ab Version 1906 fügt Configuration Manager die Datei „autorun.inf“ nicht standardmäßig hinzu. Diese Datei wird in der Regel von Antischadsoftwareprodukten blockiert. Weitere Informationen zum Feature „AutoAusführen“ finden Sie unter [Creating an AutoRun-enabled CD-ROM Application (Erstellen einer CD-ROM-Anwendung, in der das Feature „AutoAusführen“ verwendet werden kann)](/windows/desktop/shell/autoplay). Wählen Sie diese Option aus, um die Datei einzuschließen, sollte dies für Ihr Szenario weiterhin erforderlich sein.  

5. Geben Sie auf der Seite **Sicherheit** folgende Optionen an:

    - **Medien durch Kennwort schützen**: Geben Sie ein sicheres Kennwort ein, um das Medium vor nicht autorisierten Zugriffen zu schützen. Wenn Sie ein Kennwort angeben, kann der Benutzer das Medium nur nach Eingabe dieses Kennworts verwenden.  

        > [!IMPORTANT]  
        > Aus Sicherheitsgründen wird empfohlen, zum Schutz von Medien immer ein Kennwort zuzuweisen.  
        >
        > Auf eigenständigen Medien werden nur die Tasksequenzschritte und die dazugehörigen Variablen verschlüsselt. Die übrigen Inhalte der Medien werden nicht verschlüsselt. Nehmen Sie keine vertraulichen Informationen in Tasksequenzskripts auf. Speichern und implementieren Sie alle vertraulichen Informationen mithilfe von Tasksequenzvariablen.  

    - **Datumsbereich für dieses eigenständige Medium auswählen, damit es gültig ist**: Optionale Start- und Ablaufdaten auf den Medien festlegen. Diese Einstellung ist standardmäßig deaktiviert. Vor der Ausführung des eigenständigen Mediums werden die Datums- und Zeitangaben für den Zeitraum mit der Systemzeit auf dem Computer verglichen. Wenn die Systemzeit vor der Startzeit oder nach der Ablaufzeit liegt, wird das eigenständige Medium nicht gestartet. Diese Optionen sind auch über das PowerShell-Cmdlet [New-CMStandaloneMedia](/powershell/module/configurationmanager/new-cmstandalonemedia?view=sccm-ps) verfügbar.  

6. Wählen Sie auf der Seite **Eigenständige CD/DVD** die Tasksequenz aus, die das Betriebssystem bereitstellt. Sie können nur die Tasksequenzen auswählen, die einem Startimage zugewiesen sind. Überprüfen Sie die Liste mit den Inhalten, auf die durch die Tasksequenz verwiesen wird.  

    - **Zugeordnete Anwendungsabhängigkeiten erkennen und diesem Medium hinzufügen**: Fügen Sie dem Medium auch Inhalte für Anwendungsabhängigkeiten hinzu.  

        > [!TIP]  
        > Sollten die erwarteten Anwendungsabhängigkeiten nicht angezeigt werden, heben Sie die Auswahl auf, und wählen Sie die Option erneut aus, um die Liste zu aktualisieren.  

7. Geben Sie auf der Seite **Anwendung auswählen** zusätzliche Anwendungsinhalte an, die als Teil der Mediendatei aufgenommen werden sollen.  

8. Geben Sie auf der Seite **Paket auswählen** zusätzliche Paketinhalte an, die als Teil der Mediendatei aufgenommen werden sollen.  

9. Geben Sie auf der Seite **Treiberpaket auswählen** zusätzliche Treiberpaketinhalte an, die als Teil der Mediendatei aufgenommen werden sollen.  

10. Geben Sie auf der Seite **Verteilungspunkte** die Verteilungspunkte an, die den erforderlichen Inhalt enthalten.  

    Configuration Manager zeigt nur Verteilungspunkte an, die Inhalt aufweisen. Verteilen Sie alle der Tasksequenz zugeordneten Inhalte auf mindestens einen Verteilungspunkt, bevor Sie fortfahren. Nachdem Sie den Inhalt verteilt haben, aktualisieren Sie die Liste der Verteilungspunkte. Entfernen Sie alle Verteilungspunkte, die Sie bereits auf dieser Seite ausgewählt haben, wechseln Sie zur vorherigen Seite, und gehen Sie dann zurück zur Seite **Verteilungspunkte**. Alternativ können Sie den Assistenten neu starten. Weitere Informationen finden Sie unter [Verteilen von Inhalt, auf den von einer Tasksequenz verwiesen wird](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS) und [Verwalten von Inhalt und Inhaltsinfrastruktur](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

11. Geben Sie auf der Seite **Anpassung** folgende Optionen an:  

    - Fügen Sie alle Variablen hinzu, die in der Tasksequenz verwendet werden.  

    - **Prestart-Befehl aktivieren**: Geben Sie alle Prestart-Befehle an, die Sie vor der Tasksequenz ausführen möchten. Bei Prestart-Befehlen handelt es sich um eine Skriptdatei oder ausführbare Datei, über die eine Interaktion mit dem Benutzer in Windows PE möglich ist, bevor die Tasksequenz ausgeführt wird. Weitere Informationen finden Sie unter [Prestart-Befehle für Tasksequenzmedien](../understand/prestart-commands-for-task-sequence-media.md).  

        > [!TIP]  
        > Während der Medienerstellung werden die Paket-ID und die Prestart-Befehlszeile einschließlich des Werts vorhandener Tasksequenzvariablen von der Tasksequenz in die Datei **CreateTSMedia.log** auf dem Computer geschrieben, auf dem die Configuration Manager-Konsole ausgeführt wird. Sie können diese Protokolldatei überprüfen, um den Wert für die Tasksequenzvariablen zu überprüfen.  

        Sollten für den Prestart-Befehl Inhalte erforderlich sein, wählen Sie die Option **Dateien für den Prestart-Befehl einschließen** aus.  

12. Schließen Sie den Assistenten ab.  

Die Dateien der eigenständigen Medien (ISO) werden im Zielordner erstellt. Wenn Sie **CD/DVD-Satz**ausgewählt haben, kopieren Sie die Ausgabedateien auf einen Satz von CDs oder DVDs.


## <a name="next-steps"></a>Nächste Schritte

[Use stand-alone media to deploy Windows without using the network (Verwenden eigenständiger Medien zum Bereitstellen von Windows ohne Verwendung des Netzwerks)](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)