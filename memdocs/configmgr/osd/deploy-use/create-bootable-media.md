---
title: Erstellen startbarer Medien
titleSuffix: Configuration Manager
description: Verwenden Sie startbare Medien in Configuration Manager, um eine neue Version von Windows zu installieren oder einen Computer zu ersetzen.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: ead79e64-1b63-4d0d-8bd5-addff8919820
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 44c570fc2844093b190e388727dd3799bcbcdb92
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694898"
---
# <a name="create-bootable-media"></a>Erstellen startbarer Medien

*Gilt für: Configuration Manager (Current Branch)*

Startbare Medien in Configuration Manager enthalten das Startimage, optionale Prestart-Befehle und zugehörige Dateien sowie Configuration Manager-Dateien. Vorab bereitgestellte Medien können in folgenden Szenarien für die Betriebssystembereitstellung verwendet werden:  

- [Installieren einer neuen Version von Windows auf einem neuen Computer (Bare-Metal)](install-new-windows-version-new-computer-bare-metal.md)  

- [Ersetzen eines vorhandenen Computers und Übertragen von Einstellungen](replace-an-existing-computer-and-transfer-settings.md)  


## <a name="usage"></a>Verwendung

Beim Starten mit startbaren Medien passiert Folgendes:

1. Der Zielcomputer wird gestartet.
1. Er stellt eine Verbindung mit dem Netzwerk her.
1. Er ruft den folgenden Inhalt von der Website ab:
    - Die angegebene Tasksequenz
    - Betriebssystemabbild
    - Alle anderen erforderlichen Inhalte

Da sich die Tasksequenz nicht auf den Medien befindet, brauchen Sie die Medien nicht neu zu erstellen, wenn Sie die Tasksequenz oder den Inhalt ändern.

Die Pakete auf startbaren Medien sind nicht verschlüsselt. Schützen Sie den Paketinhalt mithilfe geeigneter Sicherheitsmaßnahmen vor dem Zugriff Unbefugter. Fügen Sie beispielsweise ein Kennwort für die Medien hinzu.

## <a name="prerequisites"></a>Voraussetzungen

Vergewissern Sie sich, dass alle der folgenden Bedingungen erfüllt sind, bevor Sie startbare Medien mithilfe des Assistenten zum Erstellen von Tasksequenzmedien erstellen:

### <a name="boot-image"></a>Startabbild

Beachten Sie im Zusammenhang mit dem Startimage, das Sie in der Tasksequenz zum Bereitstellen des Betriebssystems verwenden, die folgenden Punkte:

- Die Architektur des Startimages muss für die Architektur des Zielcomputers geeignet sein. Beispielsweise kann ein x86- oder x64-Startabbild von einem x64-Zielcomputer gestartet und ausgeführt werden. Bei einem x86-Zielcomputer sind jedoch nur der Start und die Ausführung eines x86-Startabbilds möglich.
- Achten Sie darauf, dass das Startimage die zur Bereitstellung des Zielcomputers erforderlichen Netzwerk- und Speichertreiber enthält.

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Erstellen einer Tasksequenz zum Bereitstellen eines Betriebssystems

Als Teil der startbaren Medien müssen Sie die Tasksequenz zum Bereitstellen des Betriebssystems angeben. Weitere Informationen finden Sie unter [Erstellen einer Tasksequenz zum Installieren eines Betriebssystems in System Center Configuration Manager](create-a-task-sequence-to-install-an-operating-system.md).

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Verteilen aller der Tasksequenz zugeordneten Inhalte

Verteilen Sie alle für die Tasksequenz erforderlichen Inhalte auf mindestens einen Verteilungspunkt. Diese Inhalte schließen das Startimage und andere zugehörige Prestart-Dateien ein. Die Inhalte werden vom Assistenten beim Erstellen der startbaren Medien vom Verteilungspunkt abgerufen.

Ihr Benutzerkonto muss mindestens über **Lesezugriffsrechte** für die Inhaltsbibliothek am Verteilungspunkt verfügen. Weitere Informationen finden Sie unter [Distribute content (Verteilen von Inhalt)](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### <a name="prepare-the-removable-usb-drive"></a>Vorbereiten des USB-Wechseldatenträgers

Wenn Sie einen USB-Speicherstick verwenden, schließen Sie ihn an den Computer an, auf dem Sie den Assistenten zum Erstellen von Tasksequenzmedien ausführen. Der USB-Speicherstick muss für Windows als Wechseldatenträger erkennbar sein. Beim Erstellen der Medien wird vom Assistenten direkt auf den USB-Datenträger geschrieben.

### <a name="create-an-output-folder"></a>Erstellen eines Ausgabeordners

Legen Sie für die vom Assistenten zum Erstellen von Tasksequenzmedien erstellten Ausgabedateien einen Ordner an, bevor Sie den Assistenten ausführen, um Medien für einen CD- oder DVD-Satz zu erstellen. Die für einen CD- oder DVD-Satz erstellten Medien werden als ISO-Datei direkt in den Ordner geschrieben.


## <a name="process"></a>Prozess

 > [!NOTE]  
 > Stellen Sie bei PKI-Umgebungen sicher, dass die startbaren Medien am primären Standort erstellt werden, da die Stammzertifizierungsstelle am primären Standort angegeben ist. Der CAS-Standort verfügt nicht über die nötigen Stammzertifizierungsstellen-Informationen, um die startbaren Medien ordnungsgemäß erstellen zu können.

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und wählen Sie anschließend den Knoten **Tasksequenzen** aus.  

2. Wählen Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Erstellen** die Option **Tasksequenzmedien erstellen** aus. Daraufhin wird der Assistent zum Erstellen von Tasksequenzmedien gestartet.  

3. Geben Sie auf der Seite **Medientyp wählen** folgende Optionen an:  

    - Wählen Sie **Startbare Medien**aus.  

    - Optional können Sie **Unbeaufsichtigte Betriebssystembereitstellung zulassen** auswählen, wenn Sie die Bereitstellung des Betriebssystems nur ohne Benutzereingabe gestatten möchten.  

        > [!IMPORTANT]  
        > Wenn Sie diese Option auswählen, wird der Benutzer nicht aufgefordert, Informationen zur Netzwerkkonfiguration oder optionale Tasksequenzen anzugeben. Wenn Sie das Medium für Kennwortschutz konfigurieren, wird der Benutzer aber weiterhin zur Eingabe eines Kennworts aufgefordert.  

4. Geben Sie auf der Seite **Medienverwaltung** eine der folgenden Optionen an:  

    - **Dynamisches Medium**: Damit lassen Sie zu, dass ein Verwaltungspunkt das Medium basierend auf dem Clientstandort innerhalb der Standortgrenzen an einen anderen Verwaltungspunkt umleitet.  

    - **Standortbasiertes Medium**: Das Medium nimmt nur Kontakt mit dem angegebenen Verwaltungspunkt auf.  

5. Auf der Seite **Medientyp** geben Sie an, ob das Medium ein **entfernbarer USB-Speicherstick** oder ein **CD/DVD-Satz** ist: Konfigurieren Sie anschließend die folgenden Optionen:  

    > [!IMPORTANT]  
    > Von Medien wird ein FAT32-Dateisystem verwendet. Sie können keine Medien auf einem USB-Speicherstick erstellen, der eine Datei mit einer Größe von mehr als 4 GB enthält.  

    - Wenn Sie **Entfernbarer USB-Speicherstick** auswählen, wählen Sie das Laufwerk aus, auf dem der Inhalt gespeichert werden soll.  

        - **USB-Wechseldatenträger (FAT32) formatieren und startbar machen**: Standardmäßig wird die Vorbereitung des USB-Laufwerks von Configuration Manager vorgenommen. Viele neuere UEFI-Geräte erfordern eine startbare FAT32-Partition. Dieses Format beschränkt jedoch auch die Größe der Dateien und die Gesamtkapazität des Laufwerks. Wenn Sie den Speicherstick bereits formatiert und konfiguriert haben, deaktivieren Sie diese Option.

    - Wenn Sie **CD/DVD-Satz** auswählen, geben Sie die Kapazität der Medien (**Mediengröße**) sowie den Namen und Pfad der Ausgabedatei (**Mediendatei**) an. Die Ausgabedateien werden vom Assistenten an diesen Speicherort geschrieben. Beispiel: `\\servername\folder\outputfile.iso`  

        Wenn die angegebene Medienkapazität zu gering zum Speichern des gesamten Inhalts ist, werden mehrere Dateien erstellt. Anschließend müssen Sie den Inhalt auf mehreren CDs oder DVDs speichern. Falls mehrere Mediendateien erforderlich sind, wird dem Namen jeder von Configuration Manager erstellten Ausgabedatei eine Sequenznummer hinzugefügt.  

        > [!IMPORTANT]  
        > Wenn Sie ein vorhandenes ISO-Abbild auswählen, wird dieses ISO-Abbild vom Assistenten zum Erstellen von Tasksequenzmedien auf dem Laufwerk oder der Freigabe gelöscht, sobald Sie mit der nächsten Seite des Assistenten fortfahren. Das vorhandene Abbild wird selbst dann gelöscht, wenn Sie den Assistenten anschließend abbrechen.  

    - **Stagingordner**<!--1359388-->: Der Medienerstellungsprozess kann viel Speicherplatz auf dem temporären Laufwerk erfordern. Dieser ähnelt standardmäßig dem folgenden Pfad: `%UserProfile%\AppData\Local\Temp`. Ab der Version 1902 können Sie das Laufwerk und den Pfad dieses Werts ändern, um bei der Speicherung der temporären Dateien flexibler zu sein.  

    - **Medienbezeichnung**<!--1359388-->: Ab Version 1902 können Sie Tasksequenzmedien eine Bezeichnung hinzufügen. Damit können Sie die Medien besser identifizieren, nachdem Sie sie erstellt haben. Der Standardwert lautet `Configuration Manager`. Dieses Textfeld wird an den folgenden Stellen angezeigt:  

        - Wenn Sie eine ISO-Datei einlegen, zeigt Windows diese Bezeichnung als Namen des eingelegten Laufwerks an.  

        - Wenn Sie ein USB-Laufwerk formatieren, verwendet es die ersten elf Zeichen der Bezeichnung als Namen.  

        - Configuration Manager schreibt eine Textdatei namens `MediaLabel.txt` in das Stammverzeichnis der Medien. Die Datei enthält standardmäßig eine einzelne Textzeile: `label=Configuration Manager`. Wenn Sie die Bezeichnung für Medien anpassen, enthält diese Zeile Ihre benutzerdefinierte Bezeichnung und nicht den Standardwert.  

    - **Datei "autorun.inf" auf Medium einschließen**<!-- 4090666 -->: Ab Version 1906 fügt Configuration Manager die Datei „autorun.inf“ nicht standardmäßig hinzu. Diese Datei wird in der Regel von Antischadsoftwareprodukten blockiert. Weitere Informationen zum Feature „AutoAusführen“ finden Sie unter [Creating an AutoRun-enabled CD-ROM Application (Erstellen einer CD-ROM-Anwendung, in der das Feature „AutoAusführen“ verwendet werden kann)](https://docs.microsoft.com/windows/desktop/shell/autoplay). Wählen Sie diese Option aus, um die Datei einzuschließen, sollte dies für Ihr Szenario weiterhin erforderlich sein.  

6. Geben Sie auf der Seite **Sicherheit** folgende Optionen an:  

    - **Unterstützung für unbekannte Computer aktivieren:** Lassen Sie zu, dass das Medium ein Betriebssystem auf einem nicht von Configuration Manager verwalteten Computer bereitstellt. Für diese Computer gibt es in der Configuration Manager-Datenbank keine Einträge. Weitere Informationen finden Sie unter [Prepare for unknown computer deployments (Vorbereiten auf Bereitstellungen für unbekannte Computer)](../get-started/prepare-for-unknown-computer-deployments.md).  

    - **Medien durch Kennwort schützen**: Geben Sie ein sicheres Kennwort ein, um das Medium vor nicht autorisierten Zugriffen zu schützen. Wenn Sie ein Kennwort angeben, kann der Benutzer das startbare Medium nur nach Eingabe dieses Kennworts verwenden.  

        > [!IMPORTANT]  
        > Aus Sicherheitsgründen wird empfohlen, zum Schutz startbarer Medien immer ein Kennwort zuzuweisen.  

    - Wählen Sie für die HTTP-Kommunikation die Option **Selbstsigniertes Medienzertifikat erstellen** aus. Geben Sie anschließend das Start- und das Ablaufdatum für das Zertifikat an.  
    
      > [!NOTE]  
      > Wenn Sie diese Option auswählen, können Sie auf der Seite **Startimage** dieses Assistenten keine HTTPS-Verwaltungspunkte auswählen.

    - Wählen Sie für die HTTPS-Kommunikation die Option **PKI-Zertifikat importieren** aus. Geben Sie anschließend das zu importierende Zertifikat und das zugehörige Kennwort an.  

        Weitere Informationen zu diesem von Startimages verwendeten Clientzertifikat finden Sie unter [PKI-Zertifikatanforderungen für System Center Configuration Manager](../../core/plan-design/network/pki-certificate-requirements.md).  

    - **Affinität zwischen Benutzer und Gerät:** Geben Sie an, wie die Zuordnung von Benutzern zum Zielcomputer durch das Medium erfolgen soll, um die benutzerzentrierte Verwaltung in Configuration Manager zu unterstützen. Weitere Informationen dazu, wie die Affinität zwischen Benutzer und Gerät durch die Bereitstellung von Betriebssystemen unterstützt wird, finden Sie unter [Zuordnen von Benutzern zu einem Zielcomputer in Configuration Manager](../get-started/associate-users-with-a-destination-computer.md).  

        - **Affinität zwischen Benutzer und Gerät mit automatischer Genehmigung zulassen:** Das Medium ordnet dem Zielcomputer automatisch Benutzer zu. Diese Funktion basiert auf den Aktionen der Tasksequenz für die Betriebssystembereitstellung. In diesem Fall wird von der Tasksequenz im Zuge der Bereitstellung des Betriebssystems für den Zielcomputer eine Beziehung zwischen den angegebenen Benutzern und dem Zielcomputer erstellt.  

        - **Affinität zwischen Benutzer und Gerät mit ausstehender Genehmigung durch den Administrator zulassen:** Das Medium ordnet dem Zielcomputer nach Erteilung der Genehmigung Benutzer zu. Diese Funktion basiert auf dem Geltungsbereich der Tasksequenz für die Betriebssystembereitstellung. In diesem Szenario wird von der Tasksequenz eine Beziehung zwischen den angegebenen Benutzern und dem Zielcomputer erstellt. Es wird jedoch auf die Genehmigung durch den Administrator gewartet, bevor das Betriebssystem bereitgestellt wird.  

        - **Affinität zwischen Benutzer und Gerät nicht zulassen:** Das Medium ordnet dem Zielcomputer keine Benutzer zu. In diesem Szenario ordnet die Tasksequenz dem Zielcomputer bei der Betriebssystembereitstellung keine Benutzer zu.  

7. Geben Sie auf der Seite **Startimage** folgende Optionen an:  

    > [!IMPORTANT]  
    > Die Architektur des verteilten Startimages muss für die Architektur des Zielcomputers geeignet sein. Beispielsweise kann ein x86- oder x64-Startabbild von einem x64-Zielcomputer gestartet und ausgeführt werden. Bei einem x86-Zielcomputer sind jedoch nur der Start und die Ausführung eines x86-Startabbilds möglich.  

    - **Startimage:** Wählen Sie das Startimage aus, mit dem der Zielcomputer gestartet werden soll.  

    - **Verteilungspunkt:** Wählen Sie den Verteilungspunkt aus, auf dem sich das Startimage befindet. Das Startabbild wird von dem Assistenten vom Verteilungspunkt abgerufen und auf das Medium geschrieben.  

        > [!NOTE]  
        > Ihr Benutzerkonto muss mindestens über **Leseberechtigungen** für die Inhaltsbibliothek an diesem Verteilungspunkt verfügen.  

    - **Verwaltungspunkt**: Wählen Sie einen Verwaltungspunkt eines primären Standorts aus (nur für *Standortbasiertes Medium*).  

    - **Zugehörige Verwaltungspunkte**: Wählen Sie die zu verwendenden Verwaltungspunkte des primären Standorts sowie eine Prioritätsreihenfolge für die erste Kommunikation aus (nur für *Dynamisches Medium*).  
    
        > [!NOTE]  
        > HTTPS-fähige Verwaltungspunkte werden nur angezeigt, wenn ein PKI-Zertifikat auf der Seite **Sicherheit** dieses Assistenten angegeben wird.  

8. Geben Sie auf der Seite **Anpassung** folgende Optionen an:  

    - Fügen Sie alle Variablen hinzu, die in der Tasksequenz verwendet werden.  

    - **Prestart-Befehl aktivieren**: Geben Sie alle Prestart-Befehle an, die Sie vor der Tasksequenz ausführen möchten. Bei Prestart-Befehlen handelt es sich um eine Skriptdatei oder ausführbare Datei, über die eine Interaktion mit dem Benutzer in Windows PE möglich ist, bevor die Tasksequenz ausgeführt wird. Weitere Informationen finden Sie unter [Prestart-Befehle für Tasksequenzmedien](../understand/prestart-commands-for-task-sequence-media.md).  

        > [!TIP]  
        > Während der Medienerstellung werden die Paket-ID und die Prestart-Befehlszeile einschließlich des Werts vorhandener Tasksequenzvariablen von der Tasksequenz in die Datei **CreateTSMedia.log** auf dem Computer geschrieben, auf dem die Configuration Manager-Konsole ausgeführt wird. Sie können diese Protokolldatei überprüfen, um den Wert für die Tasksequenzvariablen zu überprüfen.  

        Sollten für den Prestart-Befehl Inhalte erforderlich sein, wählen Sie die Option **Dateien für den Prestart-Befehl einschließen** aus.  

9. Schließen Sie den Assistenten ab.  


## <a name="alternate-method"></a>Alternative Methode

Sie können startbare Medien auf einem entfernbaren USB-Speicherstick erstellen, wenn der Speicherstick nicht an den Computer angeschlossen ist, auf dem die Configuration Manager-Konsole ausgeführt wird.

1. [Create the task sequence boot media (Erstellen der Tasksquenz-Bootmedien)](#process). Wählen Sie auf der Seite **Medientyp** **CD/DVD-Satz** aus. Die Ausgabedateien werden vom Assistenten an den Speicherort geschrieben, den Sie angeben. Beispiel: `\\servername\folder\outputfile.iso`.  

2. Bereiten Sie den USB-Wechseldatenträger vor. Der Datenträger muss formatiert, leer und startbar sein.

3. Stellen Sie die ISO-Datei aus dem freigegebenen Speicherort bereit, und übertragen Sie die Dateien aus der ISO-Datei in das USB-Laufwerk.


## <a name="next-steps"></a>Nächste Schritte

[Verwenden startbarer Medien zum Bereitstellen von Windows über das Netzwerk](use-bootable-media-to-deploy-windows-over-the-network.md)  
