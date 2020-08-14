---
title: Erstellen von Erfassungsmedien
titleSuffix: Configuration Manager
description: Verwenden Sie Erfassungsmedien in Configuration Manager, um ein Betriebssystemimage von einem Referenzcomputer zu erfassen.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 10eb8958-3848-49d7-95c0-16119b624580
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d85ab7e9d66c1206c6741117d7b379c998078708
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125371"
---
# <a name="create-capture-media"></a>Erstellen von Erfassungsmedien

*Gilt für: Configuration Manager (Current Branch)*

Mithilfe von Erfassungsmedien in Configuration Manager können Sie ein Betriebssystemimage von einem Referenzcomputer erfassen. Die Erfassungsmedien enthalten das Startimage zum Starten des Referenzcomputers und die Tasksequenz zum Erfassen des Betriebssystemimages. Verwenden Sie Erfassungsmedien für das Szenario zum [Erstellen einer Tasksequenz zum Erfassen eines Betriebssystems](create-a-task-sequence-to-capture-an-operating-system.md).  


## <a name="prerequisites"></a>Voraussetzungen

Vergewissern Sie sich, dass alle der folgenden Bedingungen erfüllt sind, bevor Sie Erfassungsmedien mithilfe des Assistenten zum Erstellen von Tasksequenzmedien erstellen:

### <a name="boot-image"></a>Startabbild

Beachten Sie im Zusammenhang mit dem Startimage, das Sie in der Tasksequenz zum Bereitstellen des Betriebssystems verwenden, die folgenden Punkte:

- Die Architektur des Startimages muss für die Architektur des Zielcomputers geeignet sein. Beispielsweise kann ein x86- oder x64-Startabbild von einem x64-Zielcomputer gestartet und ausgeführt werden. Bei einem x86-Zielcomputer sind jedoch nur der Start und die Ausführung eines x86-Startabbilds möglich.
- Achten Sie darauf, dass das Startimage die zur Bereitstellung des Zielcomputers erforderlichen Netzwerk- und Speichertreiber enthält.

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Verteilen aller der Tasksequenz zugeordneten Inhalte

Verteilen Sie alle für die Tasksequenz erforderlichen Inhalte auf mindestens einen Verteilungspunkt. Zu diesen Inhalten gehören das Startimage, das Betriebssystemimage und andere dazugehörige Dateien. Die Inhalte werden vom Assistenten beim Erstellen der Erfassungsmedien vom Verteilungspunkt abgerufen.

Ihr Benutzerkonto muss mindestens über **Lesezugriffsrechte** für die Inhaltsbibliothek am Verteilungspunkt verfügen. Weitere Informationen finden Sie unter [Distribute content (Verteilen von Inhalt)](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### <a name="prepare-the-removable-usb-drive"></a>Vorbereiten des USB-Wechseldatenträgers

Wenn Sie einen USB-Speicherstick verwenden, schließen Sie ihn an den Computer an, auf dem Sie den Assistenten zum Erstellen von Tasksequenzmedien ausführen. Der USB-Speicherstick muss für Windows als Wechseldatenträger erkennbar sein. Beim Erstellen der Medien wird vom Assistenten direkt auf den USB-Datenträger geschrieben.

### <a name="create-an-output-folder"></a>Erstellen eines Ausgabeordners

Legen Sie für die vom Assistenten zum Erstellen von Tasksequenzmedien erstellten Ausgabedateien einen Ordner an, bevor Sie den Assistenten ausführen, um Medien für einen CD- oder DVD-Satz zu erstellen. Die für einen CD- oder DVD-Satz erstellten Medien werden als ISO-Datei direkt in den Ordner geschrieben.


## <a name="process"></a>Prozess

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und wählen Sie anschließend den Knoten **Tasksequenzen** aus.  

2. Wählen Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Erstellen** die Option **Tasksequenzmedien erstellen** aus. Daraufhin wird der Assistent zum Erstellen von Tasksequenzmedien gestartet.  

3. Wählen Sie auf der Seite **Medientyp wählen** die Option **Erfassungsmedien**aus.  

4. Auf der Seite **Medientyp** geben Sie an, ob das Medium ein **entfernbarer USB-Speicherstick** oder ein **CD/DVD-Satz** ist. Konfigurieren Sie anschließend die folgenden Optionen:  

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

5. Geben Sie auf der Seite **Startimage** folgende Optionen an:  

    > [!IMPORTANT]  
    > Die Architektur des verteilten Startimages muss für die Architektur des Zielcomputers geeignet sein. Beispielsweise kann ein x86- oder x64-Startabbild von einem x64-Zielcomputer gestartet und ausgeführt werden. Bei einem x86-Zielcomputer sind jedoch nur der Start und die Ausführung eines x86-Startabbilds möglich.  

    - **Startimage:** Wählen Sie das Startimage aus, mit dem der Zielcomputer gestartet werden soll.  

    - **Verteilungspunkt:** Wählen Sie den Verteilungspunkt aus, auf dem sich das Startimage befindet. Das Startabbild wird von dem Assistenten vom Verteilungspunkt abgerufen und auf das Medium geschrieben.  

        > [!NOTE]  
        > Ihr Benutzerkonto muss mindestens über **Leseberechtigungen** für die Inhaltsbibliothek an diesem Verteilungspunkt verfügen.  

6. Schließen Sie den Assistenten ab.  


## <a name="next-steps"></a>Nächste Schritte

[Erstellen einer Tasksequenz zum Erfassen eines Betriebssystems](create-a-task-sequence-to-capture-an-operating-system.md)
