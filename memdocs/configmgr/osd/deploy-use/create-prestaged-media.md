---
title: Erstellen von vorab bereitgestellten Medien
titleSuffix: Configuration Manager
description: Verwenden Sie vorab bereitgestellte Medien in Configuration Manager, um die Bereitstellung von Windows in verschiedenen Szenarien zu vereinfachen.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: ff6e7267-302a-4563-815e-cdc0d1a4b60f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 82bb02d8154939b4b0e0ee89bcc6637e9393acff
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125218"
---
# <a name="create-prestaged-media"></a>Erstellen von vorab bereitgestellten Medien

*Gilt für: Configuration Manager (Current Branch)*

Bei vorab bereitgestellten Medien in Configuration Manager handelt es sich um eine WIM-Datei (Windows-Image). Sie kann vom Hersteller auf einem Bare-Metal-Computer oder in Ihrem Stagingzentrum ohne Verbindung mit der Configuration Manager-Produktionsumgebung installiert werden. Vorab bereitgestellte Medien enthalten das Startimage, mit dem der Zielcomputer gestartet wird, sowie das Betriebssystemimage, das auf den Zielcomputer angewendet wird. Sie können auch Anwendungen, Pakete und Treiberpakete als Teil der vorab bereitgestellten Medien angeben. Die Tasksequenz zur Bereitstellung des Betriebssystems ist nicht in den Medien enthalten. Vorab bereitgestellte Medien werden auf die Festplatte eines neuen Computers angewendet, bevor dieser an den Endbenutzer ausgeliefert wird.

Vorab bereitgestellte Medien können in folgenden Szenarien für die Betriebssystembereitstellung verwendet werden:  

- [Erstellen eines Images für ein OEM-Vorinstallations- oder lokales Depot](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

- [Installieren einer neuen Version von Windows auf einem neuen Computer (Bare-Metal)](install-new-windows-version-new-computer-bare-metal.md)  

- [Bereitstellen von Windows To Go](deploy-windows-to-go.md)  


## <a name="usage"></a>Verwendung

Wenn der Computer nach Anwendung der vorab bereitgestellten Medien zum ersten Mal gestartet wird, wird Windows PE gestartet. Es wird eine Verbindung mit einem Verwaltungspunkt hergestellt, um nach der Tasksequenz zum Abschließen der Betriebssystembereitstellung zu suchen. Wenn Sie eine Tasksequenz mit vorab bereitgestellten Medien bereitstellen, prüft der Client zunächst den lokalen Tasksequenzcache auf gültige Inhalte. Falls keine Inhalte gefunden werden oder die Inhalte geändert wurden, lädt der Client die Inhalte von einem Verteilungspunkt oder von einem Peer herunter.  


## <a name="prerequisites"></a>Voraussetzungen

Vergewissern Sie sich, dass alle der folgenden Bedingungen erfüllt sind, bevor Sie vorab bereitgestellte Medien mithilfe des Assistenten zum Erstellen von Tasksequenzmedien erstellen:

### <a name="boot-image"></a>Startabbild

Beachten Sie im Zusammenhang mit dem Startimage, das Sie in der Tasksequenz zum Bereitstellen des Betriebssystems verwenden, die folgenden Punkte:

- Die Architektur des Startimages muss für die Architektur des Zielcomputers geeignet sein. Beispielsweise kann ein x86- oder x64-Startabbild von einem x64-Zielcomputer gestartet und ausgeführt werden. Bei einem x86-Zielcomputer sind jedoch nur der Start und die Ausführung eines x86-Startabbilds möglich.
- Achten Sie darauf, dass das Startimage die zur Bereitstellung des Zielcomputers erforderlichen Netzwerk- und Speichertreiber enthält.

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Erstellen einer Tasksequenz zum Bereitstellen eines Betriebssystems

Als Teil der vorab bereitgestellten Medien müssen Sie die Tasksequenz zum Bereitstellen des Betriebssystems angeben. Weitere Informationen finden Sie unter [Erstellen einer Tasksequenz zum Installieren eines Betriebssystems in System Center Configuration Manager](create-a-task-sequence-to-install-an-operating-system.md).

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Verteilen aller der Tasksequenz zugeordneten Inhalte

Verteilen Sie alle für die Tasksequenz erforderlichen Inhalte auf mindestens einen Verteilungspunkt. Zu diesen Inhalten gehören das Startimage, das Betriebssystemimage und andere dazugehörige Dateien. Die Inhalte werden vom Assistenten beim Erstellen vorab bereitgestellter Medien vom Verteilungspunkt abgerufen.

Ihr Benutzerkonto muss mindestens über **Lesezugriffsrechte** für die Inhaltsbibliothek am Verteilungspunkt verfügen. Weitere Informationen finden Sie unter [Distribute content (Verteilen von Inhalt)](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### <a name="hard-drive-on-the-destination-computer"></a>Festplatte auf dem Zielcomputer

Die Festplatte des Zielcomputers muss vor der Anwendung der vorab bereitgestellten Medien formatiert werden. Wenn die Festplatte bei Anwendung des Mediums nicht formatiert ist und die Tasksequenz für die Betriebssystembereitstellung versucht, den Zielcomputer zu starten, tritt in der Tasksequenz ein Fehler auf.

> [!NOTE]  
> Der Assistent zum Erstellen von Tasksequenzvariablen legt die folgende medienbezogene Bedingung für Tasksequenzvariablen fest: **_SMSTSMediaType = OEMMedia**. Sie können diese Bedingung in der Tasksequenz verwenden.  


## <a name="process"></a>Prozess

 > [!NOTE]  
 > Stellen Sie bei PKI-Umgebungen sicher, dass die vorab bereitgestellten Medien am primären Standort erstellt werden, da die Stammzertifizierungsstelle am primären Standort angegeben ist. Der CAS-Standort verfügt nicht über die nötigen Stammzertifizierungsstellen-Informationen, um die vorab bereitgestellten Medien ordnungsgemäß erstellen zu können.

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und wählen Sie anschließend den Knoten **Tasksequenzen** aus.  

2. Wählen Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Erstellen** die Option **Tasksequenzmedien erstellen** aus. Daraufhin wird der Assistent zum Erstellen von Tasksequenzmedien gestartet.  

3. Geben Sie auf der Seite **Medientyp wählen** folgende Optionen an:  

    - Wählen Sie **Vorab bereitgestellte Medien**aus.  

    - Optional können Sie **Unbeaufsichtigte Betriebssystembereitstellung zulassen**auswählen, wenn Sie die Bereitstellung des Betriebssystems nur ohne Benutzereingabe gestatten möchten.  

        > [!IMPORTANT]  
        > Wenn Sie diese Option auswählen, wird der Benutzer nicht aufgefordert, Informationen zur Netzwerkkonfiguration oder optionale Tasksequenzen anzugeben. Wenn Sie das Medium für Kennwortschutz konfigurieren, wird der Benutzer aber weiterhin zur Eingabe eines Kennworts aufgefordert.  

4. Geben Sie auf der Seite **Medienverwaltung** eine der folgenden Optionen an:  

    - **Dynamisches Medium**: Damit lassen Sie zu, dass ein Verwaltungspunkt das Medium basierend auf dem Clientstandort innerhalb der Standortgrenzen an einen anderen Verwaltungspunkt umleitet.  

    - **Standortbasiertes Medium**: Das Medium nimmt nur Kontakt mit dem angegebenen Verwaltungspunkt auf.  

5. Geben Sie auf der Seite **Medieneigenschaften** die folgenden Informationen an:  

    - **Erstellt von**: Geben Sie an, von wem das Medium erstellt wurde.  

    - **Version:** Geben Sie die Versionsnummer des Mediums an.  

    - **Kommentar**: Geben Sie eine eindeutige Beschreibung des Verwendungszwecks des Mediums ein.  

    - **Mediendatei**: Geben Sie den Namen und Pfad der Ausgabedateien an. Die Ausgabedateien werden vom Assistenten an diesen Speicherort geschrieben. Beispiel: `\\servername\folder\outputfile.wim`  

    - **Stagingordner**<!--1359388-->: Der Medienerstellungsprozess kann viel Speicherplatz auf dem temporären Laufwerk erfordern. Dieser ähnelt standardmäßig dem folgenden Pfad: `%UserProfile%\AppData\Local\Temp`. Ab der Version 1902 können Sie das Laufwerk und den Pfad dieses Werts ändern, um bei der Speicherung der temporären Dateien flexibler zu sein.  

6. Geben Sie auf der Seite **Sicherheit** folgende Optionen an:  

    - **Unterstützung für unbekannte Computer aktivieren:** Lassen Sie zu, dass das Medium ein Betriebssystem auf einem nicht von Configuration Manager verwalteten Computer bereitstellt. Für diese Computer gibt es in der Configuration Manager-Datenbank keine Einträge. Weitere Informationen finden Sie unter [Prepare for unknown computer deployments (Vorbereiten auf Bereitstellungen für unbekannte Computer)](../get-started/prepare-for-unknown-computer-deployments.md).  

    - **Medien durch Kennwort schützen**: Geben Sie ein sicheres Kennwort ein, um das Medium vor nicht autorisierten Zugriffen zu schützen. Wenn Sie ein Kennwort angeben, kann der Benutzer das vorab bereitgestellte Medium nur nach Eingabe dieses Kennworts verwenden.  

        > [!IMPORTANT]  
        > Aus Sicherheitsgründen wird empfohlen, zum Schutz vorab bereitgestellter Medien immer ein Kennwort zuzuweisen.  
 
    - Wählen Sie für die HTTP-Kommunikation die Option **Selbstsigniertes Medienzertifikat erstellen** aus. Geben Sie anschließend das Start- und das Ablaufdatum für das Zertifikat an.  
    
        > [!NOTE] 
        > Wenn Sie diese Option auswählen, können Sie auf der Seite **Startimage** dieses Assistenten keine HTTPS-Verwaltungspunkte auswählen.

    - Wählen Sie für die HTTPS-Kommunikation die Option **PKI-Zertifikat importieren** aus. Geben Sie anschließend das zu importierende Zertifikat und das zugehörige Kennwort an.  

        Weitere Informationen zu diesem von Startimages verwendeten Clientzertifikat finden Sie unter [PKI-Zertifikatanforderungen für System Center Configuration Manager](../../core/plan-design/network/pki-certificate-requirements.md).  

    - **Affinität zwischen Benutzer und Gerät:** Geben Sie an, wie die Zuordnung von Benutzern zum Zielcomputer durch das Medium erfolgen soll, um die benutzerzentrierte Verwaltung in Configuration Manager zu unterstützen. Weitere Informationen dazu, wie die Affinität zwischen Benutzer und Gerät durch die Bereitstellung von Betriebssystemen unterstützt wird, finden Sie unter [Zuordnen von Benutzern zu einem Zielcomputer in Configuration Manager](../get-started/associate-users-with-a-destination-computer.md).  

        - **Affinität zwischen Benutzer und Gerät mit automatischer Genehmigung zulassen:** Das Medium ordnet dem Zielcomputer automatisch Benutzer zu. Diese Funktion basiert auf den Aktionen der Tasksequenz für die Betriebssystembereitstellung. In diesem Fall wird von der Tasksequenz im Zuge der Bereitstellung des Betriebssystems für den Zielcomputer eine Beziehung zwischen den angegebenen Benutzern und dem Zielcomputer erstellt.  

        - **Affinität zwischen Benutzer und Gerät mit ausstehender Genehmigung durch den Administrator zulassen:** Das Medium ordnet dem Zielcomputer nach Erteilung der Genehmigung Benutzer zu. Diese Funktion basiert auf dem Geltungsbereich der Tasksequenz für die Betriebssystembereitstellung. In diesem Szenario wird von der Tasksequenz eine Beziehung zwischen den angegebenen Benutzern und dem Zielcomputer erstellt. Es wird jedoch auf die Genehmigung durch den Administrator gewartet, bevor das Betriebssystem bereitgestellt wird.  

        - **Affinität zwischen Benutzer und Gerät nicht zulassen:** Das Medium ordnet dem Zielcomputer keine Benutzer zu. In diesem Szenario ordnet die Tasksequenz dem Zielcomputer bei der Betriebssystembereitstellung keine Benutzer zu.  

7. Wählen Sie auf der Seite **Tasksequenz** die auf dem Zielcomputer ausgeführte Tasksequenz aus. Überprüfen Sie die Liste mit den Inhalten, auf die durch die Tasksequenz verwiesen wird.  

    - **Zugeordnete Anwendungsabhängigkeiten erkennen und diesem Medium hinzufügen**: Fügen Sie dem Medium auch Inhalte für Anwendungsabhängigkeiten hinzu.  

        > [!TIP]  
        > Sollten die erwarteten Anwendungsabhängigkeiten nicht angezeigt werden, heben Sie die Auswahl auf, und wählen Sie die Option erneut aus, um die Liste zu aktualisieren.  

8. Geben Sie auf der Seite **Startimage** folgende Optionen an:  

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

9. Geben Sie auf der Seite **Images** folgende Optionen an:  

    - **Imagepaket:** Geben Sie das zu verwendende Betriebssystemimage an. Weitere Informationen finden Sie unter [Verwalten von Betriebssystemimages](../get-started/manage-operating-system-images.md).  

    - **Imageindex:** Geben Sie den Index des bereitzustellenden Images an, wenn das Paket mehrere Betriebssystemimages enthält.  

    - **Verteilungspunkt:** Geben Sie den Verteilungspunkt mit dem Betriebssystemimagepaket an. Der Assistent ruft das Startimage vom Verteilungspunkt ab und schreibt es auf das Medium.  

10. Wählen Sie auf der Seite **Anwendung auswählen** zusätzliche Anwendungen aus, die der vorab bereitgestellten Mediendatei hinzugefügt werden sollen.  

11. Wählen Sie auf der Seite **Paket auswählen** zusätzliche Pakete aus, die der vorab bereitgestellten Mediendatei hinzugefügt werden sollen.  

12. Wählen Sie auf der Seite **Treiberpaket auswählen** zusätzliche Treiberpakete aus, die der vorab bereitgestellten Mediendatei hinzugefügt werden sollen.  

13. Wählen Sie auf der Seite **Verteilungspunkte** mindestens einen Verteilungspunkt zum Abrufen von Inhalten aus.  

    Configuration Manager zeigt nur Verteilungspunkte an, die Inhalt aufweisen. Verteilen Sie alle der Tasksequenz zugeordneten Inhalte auf mindestens einen Verteilungspunkt, bevor Sie fortfahren. Nachdem Sie den Inhalt verteilt haben, aktualisieren Sie die Liste der Verteilungspunkte. Entfernen Sie alle Verteilungspunkte, die Sie bereits auf dieser Seite ausgewählt haben, wechseln Sie zur vorherigen Seite, und gehen Sie dann zurück zur Seite **Verteilungspunkte**. Alternativ können Sie den Assistenten neu starten. Weitere Informationen finden Sie unter [Verteilen von Inhalt, auf den von einer Tasksequenz verwiesen wird](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS) und [Verwalten von Inhalt und Inhaltsinfrastruktur](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

14. Geben Sie auf der Seite **Anpassung** folgende Optionen an:  

    - Fügen Sie alle Variablen hinzu, die in der Tasksequenz verwendet werden.  

    - **Prestart-Befehl aktivieren**: Geben Sie alle Prestart-Befehle an, die Sie vor der Tasksequenz ausführen möchten. Bei Prestart-Befehlen handelt es sich um eine Skriptdatei oder ausführbare Datei, über die eine Interaktion mit dem Benutzer in Windows PE möglich ist, bevor die Tasksequenz ausgeführt wird. Weitere Informationen finden Sie unter [Prestart-Befehle für Tasksequenzmedien](../understand/prestart-commands-for-task-sequence-media.md).  

        > [!TIP]  
        > Während der Medienerstellung werden die Paket-ID und die Prestart-Befehlszeile einschließlich des Werts vorhandener Tasksequenzvariablen von der Tasksequenz in die Datei **CreateTSMedia.log** auf dem Computer geschrieben, auf dem die Configuration Manager-Konsole ausgeführt wird. Sie können diese Protokolldatei überprüfen, um den Wert für die Tasksequenzvariablen zu überprüfen.  

        Sollten für den Prestart-Befehl Inhalte erforderlich sein, wählen Sie die Option **Dateien für den Prestart-Befehl einschließen** aus.  

15. Schließen Sie den Assistenten ab.  


## <a name="next-steps"></a>Nächste Schritte

[Erstellen eines Images für ein OEM-Vorinstallations- oder lokales Depot](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)
