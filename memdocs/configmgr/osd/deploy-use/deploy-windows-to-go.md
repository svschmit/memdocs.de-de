---
title: Bereitstellen von Windows To Go
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Windows To Go in Configuration Manager bereitstellen, um einen Windows To Go-Arbeitsbereich zu erstellen, der über ein externes Laufwerk neu startet.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 8eed50f5-80a4-422e-8aa6-a7ccb2171475
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a3cf735dfa2dd73ed39a24c2d674a966acddf05a
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125116"
---
# <a name="deploy-windows-to-go-with-configuration-manager"></a>Bereitstellen von Windows To Go mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

In diesem Thema finden Sie die Schritte zum Bereitstellen von Windows To Go in Configuration Manager. Windows To Go ist ein Unternehmensfeature von Windows 8, das die Erstellung eines Windows To Go-Arbeitsbereichs ermöglicht, der von einem externen USB-Laufwerk auf Computern gestartet werden kann, die die Windows 7- oder Windows 8-Zertifizierungsanforderungen erfüllen. Dabei ist es unerheblich, welches Betriebssystem auf dem jeweiligen Computer ausgeführt wird. Von Windows To Go-Arbeitsbereichen kann dasselbe Abbild verwendet werden, das Unternehmen für Desktops und Laptops verwenden. Außerdem können die Arbeitsbereiche auf dieselbe Weise verwaltet werden.  

 Weitere Informationen zu Windows To Go finden Sie unter [Windows To Go: Featureübersicht](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh831833(v=ws.11)).  

## <a name="provision-windows-to-go"></a>Bereitstellen von Windows To Go  
 Windows To Go ist ein Betriebssystem, das auf einem externen USB-Laufwerk gespeichert wird. Sie können das Windows To Go-Laufwerk auf dieselbe Weise wie andere Betriebssystembereitstellungen bereitstellen. Da jedoch Windows To Go als benutzerzentrierte Mobilitätslösung konzipiert ist, müssen Sie beim Bereitstellen dieser Laufwerke einen etwas anderen Ansatz verfolgen.  

 Auf hoher Ebene handelt es sich bei Windows To Go um eine Bereitstellung in zwei Phasen, die es Ihnen ermöglicht, das Windows To Go-Gerät zu konfigurieren und Inhalt für die Betriebssystembereitstellung vorab bereitzustellen. Dies können Sie mit minimalen Beeinträchtigungen des Benutzers und begrenzter Downtime des Benutzercomputers erreichen. Nachdem Sie den Computer vorab bereitgestellt haben, müssen Sie den Bereitstellungsvorgang abschließen, um sicherzustellen, dass der Computer vom Benutzer verwendet werden kann. Der Bereitstellungsvorgang ist mit dem aktuellen Vorgang der Betriebssystembereitstellung vergleichbar. Im Folgenden wird der allgemeine Workflow zum Vorabbereitstellen von Inhalt und zum Bereitstellen von Windows To Go aufgelistet:  

1.  [Voraussetzungen für die Bereitstellung von Windows To Go](#BKMK_Prereqs)  

2.  [Erstellen von vorab bereitgestellten Medien](#BKMK_CreatePrestagedMedia)  

3.  [Erstellen eines Windows To Go Creator-Pakets](#BKMK_CreatePackage)  

4.  [Aktualisieren der Tasksequenz zum Aktivieren von BitLocker für Windows To Go](#BKMK_UpdateTaskSequence)  

5.  [Bereitstellen von Windows To Go Creator-Paket und Tasksequenz](#BKMK_Deployments)  

6.  [Benutzer führt Windows To Go Creator aus](#BKMK_UserExperience)  

7.  [Configuration Manager konfiguriert das Windows To Go-Laufwerk und stellt es vorab bereit](#BKMK_ConfigureStageDrive)  

8.  [Benutzer meldet sich bei Windows 8 an](#BKMK_UserLogsIn)  

###  <a name="prerequisites-to-provision-windows-to-go"></a><a name="BKMK_Prereqs"></a> Voraussetzungen für die Bereitstellung von Windows To Go  
 Vor dem Bereitstellen von Windows To Go müssen Sie die folgenden Aktionen in Configuration Manager ausführen:  

-   **Verteilen eines Startabbilds an einen Verteilungspunkt**  

     Vor dem Erstellen von vorab bereitgestellten Medien müssen Sie das Startabbild an einen Verteilungspunkt verteilen.  

    > [!NOTE]  
    >  Startimages werden zum Installieren des Betriebssystems auf den Zielcomputern in Ihrer Configuration Manager-Umgebung verwendet. Sie enthalten eine Version von Windows PE, von der das Betriebssystem sowie alle zusätzlich erforderlichen Gerätetreiber installiert werden. Configuration Manager stellt zwei Startimages bereit: je eins zur Unterstützung von x86- bzw. x64-Plattformen. Sie können auch Ihre eigenen Startabbilder erstellen. Weitere Informationen finden Sie unter [Verwalten von Startimages](../get-started/manage-boot-images.md).  

-   **Verteilen des Windows 8-Betriebssystemabbilds an einen Verteilungspunkt**  

     Vor dem Erstellen von vorab bereitgestellten Medien müssen Sie das Windows 8-Betriebssystemabbild an einen Verteilungspunkt verteilen.  

    > [!NOTE]  
    >  Betriebssystemabbilder sind Dateien im WIM-Format und stellen eine komprimierte Sammlung von Verweisdateien und -ordnern dar, die für die erfolgreiche Installation und Konfiguration eines Betriebssystems auf einem Computer erforderlich sind. Weitere Informationen finden Sie unter [Manage operating system images (Verwalten von Betriebssystemimages)](../get-started/manage-operating-system-images.md).  

-   **Erstellen einer Tasksequenz zum Bereitstellen von Windows 8**  

     Sie müssen eine Tasksequenz für eine Windows 8-Bereitstellung erstellen, auf die Sie verweisen, wenn Sie vorab bereitgestellte Medien erstellen. Weitere Informationen finden Sie unter [Verwalten von Tasksequenzen zum Automatisieren von Aufgaben](manage-task-sequences-to-automate-tasks.md).  

###  <a name="create-prestaged-media"></a><a name="BKMK_CreatePrestagedMedia"></a> Erstellen von vorab bereitgestellten Medien  
 Vorab bereitgestellte Medien enthalten das Startabbild, mit dem der Zielcomputer gestartet wird, und das Betriebssystemabbild, das auf den Zielcomputer angewendet wird. Der Computer, auf dem Sie vorab bereitgestellte Medien bereitstellen, kann mithilfe des Startabbilds gestartet werden. Auf dem Computer kann dann eine vorhandene Tasksequenz für die Betriebssystembereitstellung ausgeführt werden, um eine vollständige Betriebssystembereitstellung zu installieren. Die Tasksequenz zur Bereitstellung des Betriebssystems ist nicht in den Medien enthalten.  

 Sie können neben dem Betriebssystemabbild und Startabbild in der Vorabbereitstellungsphase auch Inhalte wie Anwendungen und Gerätetreiber hinzufügen. Dadurch wird die zum Bereitstellen eines Betriebssystems benötigte Zeit verringert, und zudem wird der Netzwerkverkehr reduziert, weil sich der Inhalt bereits auf dem Laufwerk befindet.  

 Gehen Sie folgendermaßen vor, um vorab bereitgestellte Medien zu erstellen.  

#### <a name="to-create-prestaged-media"></a>So erstellen Sie vorab bereitgestellte Medien  

1. Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2. Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Tasksequenzen**.  

3. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Tasksequenzmedien erstellen** , um den Assistenten zum Erstellen von Tasksequenzmedien zu starten.  

4. Geben Sie auf der Seite **Medientyp wählen** die folgenden Informationen an, und klicken Sie dann auf **Weiter**.  

   -   Wählen Sie **Vorab bereitgestellte Medien**aus.  

   -   Aktivieren Sie die Option **Unbeaufsichtigte Betriebssystembereitstellung zulassen** , um die Windows To Go-Bereitstellung ohne Benutzereingriff zu starten.  

       > [!IMPORTANT]  
       >  Wenn Sie diese Option mit der (im weiteren Verlauf dieses Verfahrens festgelegten) benutzerdefinierten Variablen SMSTSPreferredAdvertID verwenden, ist kein Benutzereingriff erforderlich, und der Computer wird bei der Bereitstellung von Windows To Go automatisch gestartet, sobald ein Windows To Go-Laufwerk erkannt wird. Der Benutzer wird aber weiterhin zur Eingabe eines Kennworts aufgefordert, wenn die Medien für den Kennwortschutz konfiguriert sind. Wenn Sie die Einstellung **Unbeaufsichtigte Betriebssystembereitstellung zulassen** verwenden, ohne die Variable SMSTSPreferredAdvertID zu konfigurieren, tritt beim Bereitstellen der Tasksequenz ein Fehler auf.  

5. Geben Sie auf der Seite **Medienverwaltung** die folgenden Informationen an, und klicken Sie dann auf **Weiter**.  

   -   Wählen Sie **Dynamisches Medium** aus, wenn Sie zulassen möchten, dass das Medium ausgehend vom Clientstandort innerhalb der Standortgrenzen von einem Verwaltungspunkt an einen anderen Verwaltungspunkt umgeleitet wird.  

   -   Wählen Sie **Standortbasiertes Medium** aus, wenn Sie wünschen, dass von dem Medium nur mit dem angegebenen Verwaltungspunkt Kontakt aufgenommen wird.  

6. Geben Sie auf der Seite **Medieneigenschaften**  die folgenden Informationen an, und klicken Sie dann auf **Weiter**.  

   -   **Erstellt von**: Geben Sie an, von wem das Medium erstellt wurde.  

   -   **Version:** Geben Sie die Versionsnummer des Mediums an.  

   -   **Kommentar**: Geben Sie eine eindeutige Beschreibung des Verwendungszwecks des Mediums ein.  

   -   **Mediendatei**: Geben Sie den Namen und Pfad der Ausgabedateien an. Die Ausgabedateien werden vom Assistenten an diesen Speicherort geschrieben. Beispiel: **\\\Servername\Ordner\Ausgabedatei.wim**  

7. Geben Sie auf der Seite **Sicherheit** die folgenden Informationen an, und klicken Sie dann auf **Weiter**.  

   -   Aktivieren Sie das Kontrollkästchen **Unterstützung für unbekannte Computer aktivieren**, um zuzulassen, dass von dem Medium ein Betriebssystem auf einem nicht von Configuration Manager verwalteten Computer bereitgestellt wird. Für diese Computer gibt es in der Configuration Manager-Datenbank keine Einträge. Zu unbekannten Computern gehören die folgenden:  

       -   Computer, auf denen kein Configuration Manager-Client installiert ist  

       -   Computer, die nicht in Configuration Manager importiert wurden  

       -   Computer, die von Configuration Manager nicht ermittelt wurden  

   -   Aktivieren Sie das Kontrollkästchen **Medien durch Kennwort schützen** , und geben Sie ein sicheres Kennwort ein, um das Medium vor nicht autorisiertem Zugriff zu schützen. Wenn Sie ein Kennwort angeben, kann der Benutzer das vorab bereitgestellte Medium nur nach Eingabe dieses Kennworts verwenden.  

       > [!IMPORTANT]  
       >  Aus Sicherheitsgründen wird empfohlen, zum Schutz vorab bereitgestellter Medien immer ein Kennwort zuzuweisen.  

       > [!NOTE]  
       >  Wenn Sie die vorab bereitgestellten Medien durch ein Kennwort schützen, wird der Benutzer auch dann zur Eingabe des Kennworts aufgefordert, wenn die Medien mit der Einstellung **Unbeaufsichtigte Betriebssystembereitstellung zulassen** konfiguriert sind.  

   -   Wählen Sie für die HTTP-Kommunikation die Option **Selbstsigniertes Medienzertifikat erstellen**aus, und geben Sie dann das Start- und Ablaufdatum des Zertifikats an.  

   -   Wählen Sie für die HTTPS-Kommunikation **PKI-Zertifikat importieren**aus, und geben Sie dann das zu importierende Zertifikat und das zugehörige Kennwort an.  

        Weitere Informationen zu diesem für Startimages verwendeten Clientzertifikat finden Sie unter [PKI certificate requirements (PKI-Zertifikatanforderungen)](../../core/plan-design/network/pki-certificate-requirements.md).  

   -   **Affinität zwischen Benutzer und Gerät**: Geben Sie an, wie die Zuordnung von Benutzern zum Zielcomputer durch das Medium erfolgen soll, um die benutzerzentrierte Verwaltung in Configuration Manager zu unterstützen. Weitere Informationen dazu, wie die Affinität zwischen Benutzer und Gerät durch die Bereitstellung von Betriebssystemen unterstützt wird, finden Sie unter [Associate users with a destination computer (Zuordnen von Benutzern zu einem Zielcomputer)](../get-started/associate-users-with-a-destination-computer.md).  

       -   Geben Sie **Affinität zwischen Benutzer und Gerät mit automatischer Genehmigung zulassen** an, wenn die Zuordnung von Benutzern zum Zielcomputer durch das Medium automatisch erfolgen soll. Diese Funktionalität basiert auf den Aktionen der Tasksequenz, von der das Betriebssystem bereitgestellt wird. In diesem Fall wird von der Tasksequenz während der Bereitstellung des Betriebssystems an den Zielcomputer eine Beziehung zwischen den angegebenen Benutzern und dem Zielcomputer erstellt.  

       -   Geben Sie **Affinität zwischen Benutzer und Gerät mit ausstehender Genehmigung durch den Administrator zulassen** an, wenn die Zuordnung von Benutzern zum Zielcomputer durch das Medium nach einer entsprechenden Genehmigung erfolgen soll. Diese Funktionalität basiert auf dem Geltungsbereich der Tasksequenz, von der das Betriebssystem bereitgestellt wird. In diesem Fall wird von der Tasksequenz eine Beziehung zwischen den angegebenen Benutzern und dem Zielcomputer erstellt. Es wird jedoch auf die Genehmigung durch den Administrator gewartet, bevor das Betriebssystem bereitgestellt wird.  

       -   Geben Sie **Affinität zwischen Benutzer und Gerät nicht zulassen** an, wenn keine Zuordnung von Benutzern zum Zielcomputer durch das Medium erfolgen soll. In diesem Fall wird während der Bereitstellung des Betriebssystems keine Beziehung zwischen Benutzern und dem Zielcomputer erstellt.  

8. Geben Sie auf der Seite **Tasksequenz** die Windows 8-Tasksequenz an, die Sie im vorherigen Abschnitt erstellt haben.  

9. Geben Sie auf der Seite **Startabbild** die folgenden Informationen an, und klicken Sie dann auf **Weiter**.  

    > [!IMPORTANT]  
    >  Die Architektur des verteilten Startabbilds muss für die Architektur des Zielcomputers geeignet sein. Beispielsweise kann ein x86- oder x64-Startabbild von einem x64-Zielcomputer gestartet und ausgeführt werden. Bei einem x86-Zielcomputer sind jedoch nur der Start und die Ausführung eines x86-Startabbilds möglich. Bei Windows 8-zertifizierten Computern im EFI-Modus müssen Sie ein x64-Startabbild verwenden.  

    -   **Startimage:** Geben Sie das Startimage zum Starten des Zielcomputers an.  

    -   **Verteilungspunkt:** Geben Sie den Verteilungspunkt an, auf dem das Startimage gehostet wird. Das Startabbild wird von dem Assistenten vom Verteilungspunkt abgerufen und auf das Medium geschrieben.  

        > [!NOTE]  
        >  Der Administrator muss über das Zugriffsrecht **Lesen** für den Startabbildinhalt auf dem Verteilungspunkt verfügen. Weitere Informationen finden Sie unter [Paketzugriffskonto](../../core/plan-design/hierarchy/accounts.md#package-access-account).  

    -   Wenn Sie auf der Seite **Medienverwaltung** des Assistenten die Option **Standortbasiertes Medium** ausgewählt haben, müssen Sie im Feld **Verwaltungspunkt** einen Verwaltungspunkt eines primären Standorts angeben.  

    -   Wenn Sie auf der Seite **Medienverwaltung** des Assistenten die Option **Dynamisches Medium** ausgewählt haben, müssen Sie im Feld **Zugehörige Verwaltungspunkte** die zu verwendenden Verwaltungspunkte des primären Standorts sowie eine Prioritätsreihenfolge für die erste Kommunikation angeben.  

10. Geben Sie auf der Seite **Abbilder** die folgenden Informationen an, und klicken Sie dann auf **Weiter**.  

    -   **Imagepaket:** Geben Sie das Paket an, das das Windows 8-Betriebssystemimage enthält.  

    -   **Imageindex:** Geben Sie das bereitzustellende Image an, wenn das Paket mehrere Betriebssystemimages enthält.  

    -   **Verteilungspunkt:** Geben Sie den Verteilungspunkt an, auf dem das Betriebssystemimagepaket gehostet wird. Das Betriebssystemabbild wird von dem Assistenten vom Verteilungspunkt abgerufen und auf das Medium geschrieben.  

        > [!NOTE]  
        >  Der Administrator muss über das Zugriffsrecht **Lesen** für den Betriebssystemabbildinhalt auf dem Verteilungspunkt verfügen. Weitere Informationen finden Sie unter [Paketzugriffskonto](../../core/plan-design/hierarchy/accounts.md#package-access-account).  

11. Wählen Sie auf der Seite **Anwendung auswählen** den der Mediendatei hinzuzufügenden Anwendungsinhalt aus, und klicken Sie dann auf **Weiter**.  

12. Wählen Sie auf der Seite **Paket auswählen** zusätzlichen Paketinhalt für die Mediendatei aus, und klicken Sie dann auf **Weiter**.  

13. Wählen Sie auf der Seite **Treiberpaket auswählen** den der Mediendatei hinzuzufügenden Treiberpaketinhalt aus, und klicken Sie dann auf **Weiter**.  

14. Wählen Sie auf der Seite **Verteilungspunkte** mindestens einen Verteilungspunkt aus, der den für die Tasksequenz erforderlichen Inhalt enthält, und klicken Sie dann auf **Weiter**.  

15. Geben Sie auf der Seite **Anpassung** die folgenden Informationen an, und klicken Sie dann auf **Weiter**.  

    - **Variablen:** Geben Sie die Variablen an, die von der Tasksequenz zur Bereitstellung des Betriebssystems verwendet werden. Verwenden Sie für Windows To Go die Variable SMSTSPreferredAdvertID, um die Windows To Go-Bereitstellung im folgenden Format automatisch auszuwählen:  

       SMSTSPreferredAdvertID = {*Bereitstellungs-ID*}: Hierbei stellt „Bereitstellungs-ID“ die Bereitstellungs-ID dar, die der Tasksequenz zugeordnet ist, die Sie zum Ausführen des Bereitstellungsvorgangs für das Windows To Go-Laufwerk verwenden.  

      > [!TIP]  
      >  Wenn Sie diese Variable mit einer Tasksequenz verwenden, die (zuvor in diesem Verfahren) für die unbeaufsichtigte Ausführung konfiguriert wurde, ist kein Benutzereingriff erforderlich, und der Computer wird bei der Bereitstellung von Windows To Go automatisch gestartet, sobald ein Windows To Go-Laufwerk erkannt wird. Der Benutzer wird aber weiterhin zur Eingabe eines Kennworts aufgefordert, wenn die Medien für den Kennwortschutz konfiguriert sind.  

    - **Prestart-Befehle:** Geben Sie alle Prestart-Befehle an, die Sie vor der Tasksequenz ausführen möchten. Bei Prestart-Befehlen kann es sich um eine Skriptdatei oder ausführbare Datei handeln, über die eine Interaktion mit dem Benutzer in Windows PE möglich ist, bevor die Tasksequenz zum Installieren des Betriebssystems ausgeführt wird. Konfigurieren Sie die folgenden Variablen für die Windows To Go-Bereitstellung:  

      - **OSDBitLockerPIN:** BitLocker für Windows To Go erfordert eine Passphrase. Legen Sie die Variable **OSDBitLockerPIN** als Teil eines Prestart-Befehls zum Festlegen der BitLocker-Passphrase für das Windows To Go-Laufwerk fest.  

        > [!WARNING]  
        >  Wenn BitLocker für die Passphrase aktiviert wurde, muss der Benutzer die Passphrase bei jedem Neustart des Computers vom Windows To Go-Laufwerk eingeben.  

      - **SMSTSUDAUsers:** Gibt den primären Benutzer des Zielcomputers an. Verwenden Sie diese Variable, um den Benutzernamen zu erfassen, der dann zum Zuordnen des Benutzers und Geräts verwendet werden kann. Weitere Informationen finden Sie unter [Zuordnen von Benutzern zu einem Zielcomputer](../get-started/associate-users-with-a-destination-computer.md).  

        > [!TIP]  
        >  Zum Abrufen des Benutzernamens können Sie ein Eingabefeld als Teil des Prestart-Befehls erstellen, sodass Benutzer ihren Benutzernamen eingeben müssen, und dann die Variable mit dem Wert festlegen. Sie können der Skriptdatei für den Prestart-Befehl beispielsweise die folgenden Zeilen hinzufügen:  
        >   
        >  `UserID = inputbox("Enter Username" ,"Enter your username:","",400,0)`  
        >   
        >  `env("SMSTSUDAUsers") = UserID`  

        Weitere Informationen zum Erstellen einer Skriptdatei zur Verwendung als Prestart-Befehl finden Sie unter [Prestart commands for task sequence media (Prestart-Befehle für Tasksequenzmedien)](../understand/prestart-commands-for-task-sequence-media.md).  

16. Schließen Sie den Assistenten ab.  

    > [!NOTE]  
    >  Die Erstellung der vorab bereitgestellten Mediendatei durch den Assistenten kann einige Zeit in Anspruch nehmen.  

###  <a name="create-a-windows-to-go-creator-package"></a><a name="BKMK_CreatePackage"></a> Erstellen eines Windows To Go Creator-Pakets  
 Sie müssen im Rahmen der Windows To Go-Bereitstellung ein Paket zum Bereitstellen der vorab bereitgestellten Mediendatei erstellen. Im Paket muss das Tool enthalten sein, mit dem das Windows To Go-Laufwerk konfiguriert und die vorab bereitgestellte Mediendatei auf dem Laufwerk extrahiert wird. Gehen Sie folgendermaßen vor, um das Windows To Go Creator-Paket zu erstellen.  

#### <a name="to-create-the-windows-to-go-creator-package"></a>So erstellen Sie das Windows To Go Creator-Paket  

1. Erstellen Sie auf dem Server zum Hosten der Windows To Go Creator-Paketdateien einen Quellordner für die Paketquelldateien.  

   > [!NOTE]  
   >  Dem Computerkonto des Standortservers muss das Zugriffsrecht **Lesen** für den Quellordner zugewiesen sein.  

2. Kopieren Sie die im Abschnitt [Create prestaged media](#BKMK_CreatePrestagedMedia) erstellte vorab bereitgestellte Mediendatei in den Paketquellordner.  

3. Kopieren Sie das Windows To Go Creator-Tool (WTGCreator.exe) in den Paketquellordner. Dieses Creator-Tool steht auf jedem primären Standortserver im Verzeichnis „<*Configuration Manager-Installationsverzeichnis*>\OSD\Tools\WTG\Creator“ zur Verfügung.  

4. Erstellen Sie mithilfe des Assistenten zum Erstellen von Paketen und Programmen ein Paket und Programm.  

5. Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

6. Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Abschnitt **Anwendungsverwaltung**, und klicken Sie dann auf **Pakete**.  

7. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Paket erstellen**.  

8. Geben Sie auf der Seite **Paket** den Namen und die Beschreibung des Pakets an. Geben Sie beispielsweise **Windows To Go** als Paketnamen ein, und geben Sie **Paket zum Konfigurieren eines Windows To Go-Laufwerks mithilfe von System Center Configuration Manager** als Paketbeschreibung ein.  

9. Aktivieren Sie das Kontrollkästchen **Dieses Paket enthält Quelldateien**, geben Sie den Pfad zu dem in Schritt 1 erstellten Paketquellordner an, und klicken Sie dann auf **Weiter**.  

10. Wählen Sie auf der Seite **Programmtyp** die Option **Standardprogramm**aus, und klicken Sie dann auf **Weiter**.  

11. Geben Sie auf der Seite **Standardprogramm** Folgendes an:  

    -   **Name:** Geben Sie den Namen des Programms an. Geben Sie beispielsweise **Creator** als Programmnamen ein.  

    -   **Befehlszeile:** Geben Sie **WTGCreator.exe /wim:PrestageName.wim** ein, wobei „PrestageName“ den Namen der vorab bereitgestellten Datei darstellt, die Sie erstellt und in den Paketquellordner für das Windows To Go Creator-Paket kopiert haben.  

         Optional können Sie die folgenden Optionen hinzufügen:  

        -   **enableBootRedirect**: Dies ist die Befehlszeilenoption zum Ändern der Windows To Go-Startoptionen, sodass eine Startumleitung zulässig ist. Wenn Sie diese Option verwenden, wird der Computer vom USB-Laufwerk gestartet, ohne dass die Startreihenfolge in der Computerfirmware geändert werden oder der Benutzer beim Start eine Startoption auswählen muss. Wenn ein Windows To Go-Laufwerk erkannt wird, erfolgt der Computerstart von diesem Laufwerk.  

    -   **Run**: Geben Sie **Normal** an, um das Programm basierend auf den Standardeinstellungen des Systems und Programms auszuführen.  

    -   **Programm kann ausgeführt werden:** Geben Sie an, ob das Programm nur ausgeführt werden kann, wenn ein Benutzer angemeldet ist.  

    -   **Ausführmodus:** Geben Sie an, ob das Programm mit den Berechtigungen des angemeldeten Benutzers oder mit Administratorberechtigungen ausgeführt werden soll. Zum Ausführen von Windows To Go Creator sind erhöhte Rechte erforderlich.  

    -   Wählen Sie **Benutzern gestatten, die Programminstallation anzuzeigen und mit ihr zu interagieren**aus, und klicken Sie dann auf **Weiter**.  

12. Geben Sie auf der Seite Anforderungen Folgendes an:  

    - **Plattformanforderungen:** Wählen Sie die entsprechenden Windows 8-Plattformen für die Bereitstellung aus.  

    - **Geschätzter Speicherplatz:** Geben Sie die Größe des Paketquellordners für Windows To Go Creator an.  

    - **Maximal zulässige Laufzeit (Minuten):** Geben Sie die maximale Zeit für die Ausführung des Programms auf dem Clientcomputer an. Standardmäßig ist dieser Wert auf 120 Minuten festgelegt.  

      > [!IMPORTANT]  
      >  Wenn Sie bei der Sammlung, für die dieses Programm ausgeführt wird, Wartungsfenster verwenden, kann ein Konflikt auftreten, wenn die **Maximal zulässige Laufzeit** länger ist als das geplante Wartungsfenster. Wenn für die maximal zulässige Laufzeit der Wert **Unbekannt**festgelegt ist, wird das Programm zwar während des Wartungsfensters gestartet, die Ausführung wird jedoch am Ende des Wartungsfensters nicht unterbrochen, sondern solange fortgesetzt, bis das Programm abgeschlossen ist oder ein Fehler auftritt. Wenn Sie für die maximal zulässige Laufzeit einen bestimmten Zeitraum (und nicht Unbekannt) festlegen, der die Dauer aller verfügbaren Wartungsfenster überschreitet, wird dieses Programm nicht ausgeführt.  

      > [!NOTE]  
      >  Wenn der Wert auf **Unknown** (Unbekannt) festgelegt ist, legt Configuration Manager die maximal zulässige Laufzeit auf 12 Stunden (720 Minuten) fest.  

      > [!NOTE]  
      >  Wird die (vom Benutzer festgelegte oder als Standardwert verwendete) maximal zulässige Laufzeit überschritten, wird das Programm von Configuration Manager beendet, sofern auf der Seite **Standardprogramm** die Option **Mit Administratorrechten ausführen** aktiviert und die Option **Benutzern gestatten, die Programminstallation anzuzeigen und mit ihr zu interagieren** deaktiviert ist.  

      Klicken Sie auf **Weiter** , und schließen Sie den Assistenten ab.  

###  <a name="update-the-task-sequence-to-enable-bitlocker-for-windows-to-go"></a><a name="BKMK_UpdateTaskSequence"></a> Aktualisieren der Tasksequenz zum Aktivieren von BitLocker für Windows To Go  
 Von Windows To Go wird BitLocker auf einem externen Startlaufwerk ohne TPM aktiviert. Deshalb müssen Sie zum Konfigurieren von BitLocker auf dem Windows To Go-Laufwerk ein anderes Tool verwenden. Zum Aktivieren von BitLocker müssen Sie der Tasksequenz nach dem Schritt **Windows und ConfigMgr einrichten** eine Aktion hinzufügen.  

> [!NOTE]  
>  BitLocker für Windows To Go erfordert eine Passphrase. Im Schritt [Create prestaged media](#BKMK_CreatePrestagedMedia) legen Sie die Passphrase als Teil eines Prestart-Befehls mit der Variablen OSDBitLockerPIN fest.  

 Gehen Sie folgendermaßen vor, um die Windows 8-Tasksequenz zum Aktivieren von BitLocker für Windows To Go zu aktualisieren.  

#### <a name="to-update-the-windows-8-task-sequence-to-enable-bitlocker"></a>So aktualisieren Sie die Windows 8-Tasksequenz zum Aktivieren von BitLocker  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Abschnitt **Anwendungsverwaltung**, und klicken Sie dann auf **Pakete**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Paket erstellen**.  

4.  Geben Sie auf der Seite **Paket** den Namen und die Beschreibung des Pakets an. Geben Sie beispielsweise **BitLocker for Windows To Go** für den Paketnamen ein, und geben Sie **Package to update BitLocker for Windows To Go** als Paketbeschreibung an.  

5.  Aktivieren Sie das Kontrollkästchen **Dieses Paket enthält Quelldateien**, geben Sie den Speicherort für das Tool BitLocker für Windows To Go an, und klicken Sie dann auf **Weiter**. Das Tool „BitLocker“ steht auf jedem primären Configuration Manager-Standortserver im Verzeichnis „<*Configuration Manager-Installationsordner*>\OSD\Tools\WTG\BitLocker\“ zur Verfügung.  

6.  Wählen Sie auf der Seite **Programmtyp** die Option **Kein Programm erstellen**aus.  

7.  Klicken Sie auf **Weiter** , und schließen Sie den Assistenten ab.  

8.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

9. Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Tasksequenzen**.  

10. Wählen Sie die Windows 8-Tasksequenz aus, auf die auf dem vorab bereitgestellten Medium verwiesen wird.  

11. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Tasksequenz** auf **Bearbeiten**.  

12. Klicken Sie auf den Schritt **Windows und ConfigMgr einrichten** , dann auf **hinzufügen**, anschließend auf **Allgemein**und schließlich auf **Befehlszeile ausführen**. Der Schritt Befehlszeile ausführen wird nach dem Schritt Windows und ConfigMgr einrichten hinzugefügt.  

13. Fügen Sie auf der Registerkarte **Eigenschaften** des Schritts **Befehlszeile ausführen** Folgendes hinzu:  

    1.  **Name:** Geben Sie einen Namen für die Befehlszeile an, z. B. **BitLocker für Windows To Go aktivieren**.  

    2.  **Befehlszeile**: i386\osdbitlocker_wtg.exe /Enable /pwd:< *None&#124;AD*>  

         Parameter:  

        -   /pwd:<None&#124;AD> – Geben Sie den Modus für die BitLocker-Kennwortwiederherstellung an. Dieser Parameter ist erforderlich, wenn Sie den Parameter /Enable in der Befehlszeile verwenden.  

             Wählen Sie **AD** aus, um die BitLocker-Laufwerkverschlüsselung so zu konfigurieren, dass Wiederherstellungsinformationen für mit BitLocker geschützte Laufwerke in Active Directory-Domänendiensten (AD DS) gesichert werden. Durch die Sicherung von Wiederherstellungskennwörtern für ein mit BitLocker geschütztes Laufwerk können Administratoren das Laufwerk wiederherstellen, wenn es gesperrt ist. Dadurch wird sichergestellt, dass autorisierte Benutzer stets Zugriff auf verschlüsselte Daten des Unternehmens haben. Wenn Sie **Keine**angeben, ist der Benutzer selbst dafür verantwortlich, eine Kopie des Wiederherstellungskennworts oder Wiederherstellungsschlüssels aufzubewahren. Wenn diese Informationen verloren gehen oder ein Benutzer das Laufwerk vor dem Verlassen des Unternehmens nicht entschlüsselt, können Administratoren nicht problemlos auf das Laufwerk zugreifen.  

        -   /wait:<TRUE&#124;FALSE> – Geben Sie an, ob bei einer Tasksequenz auf den Abschluss der Verschlüsselung gewartet wird.  

    3.  Wählen Sie die Option **Paket**aus, und geben Sie anschließend das Paket an, das Sie zu Beginn dieser Prozedur erstellt haben.  

    4.  Fügen Sie auf der Registerkarte **Optionen** die folgenden Bedingungen hinzu:  

        -   Bedingung = Tasksequenzvariable  

        -   Variable = _SMSTSWTG  

        -   Bedingung = Ist gleich  

        -   Wert = Wahr  

    > [!NOTE]  
    >  Mit dem Schritt **BitLocker aktivieren** , welcher häufig auf den neuen Befehlszeilenschritt folgt, kann BitLocker für Windows To Go nicht aktiviert werden. Dennoch können Sie diesen Schritt in der Tasksequenz behalten, um sie für Windows 8-Bereitstellungen ohne Windows To Go-Laufwerk zu verwenden.  

###  <a name="deploy-the-windows-to-go-creator-package-and-task-sequence"></a><a name="BKMK_Deployments"></a> Bereitstellen von Windows To Go Creator-Paket und Tasksequenz  
 Bei Windows To Go handelt es sich um einen Hybrid-Bereitstellungsprozess. Daher müssen Sie das Windows To Go Creator-Paket und die Windows 8-Tasksequenz bereitstellen Verwenden Sie die folgenden Verfahren, um den Bereitstellungsvorgang abzuschließen.  

#### <a name="to-deploy-the-windows-to-go-creator-package"></a>So stellen Sie das Windows To Go Creator-Paket bereit  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Abschnitt **Anwendungsverwaltung**, und klicken Sie dann auf **Pakete**.  

3.  Wählen Sie das Windows To Go Creator-Paket aus, das Sie im Schritt [Erstellen eines Windows To Go Creator-Pakets](#BKMK_CreatePackage) erstellt haben.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Bereitstellen**.  

5.  Geben Sie auf der Seite **Allgemein** die folgenden Einstellungen an:  

    1.  **Software**: Vergewissern Sie sich, dass das Windows To Go-Paket ausgewählt ist.  

    2.  **Sammlung:** Klicken Sie auf **Durchsuchen**, um die Sammlung auszuwählen, für die das Windows To Go-Paket bereitgestellt werden soll.  

    3.  **Standard-Verteilungspunktgruppen verwenden, die dieser Sammlung zugeordnet sind:** Wählen Sie diese Option aus, wenn Sie den Paketinhalt in der standardmäßigen Verteilungspunktgruppe der Sammlung speichern möchten. Wenn die ausgewählte Sammlung keiner Verteilungspunktgruppe zugeordnet ist, ist diese Option nicht verfügbar.  

6.  Klicken Sie auf der Seite **Inhalt** auf **Hinzufügen** , und wählen Sie dann die Verteilungspunkte oder Verteilungspunktgruppen aus, auf denen der diesem Paket und diesem Programm zugeordnete Inhalt bereitgestellt werden soll.  

7.  Wählen Sie auf der Seite **Bereitstellungseinstellungen** als Bereitstellungstyp **Erforderlich** aus, und klicken Sie dann auf **Weiter**.  

8.  Konfigurieren Sie auf der Seite **Zeitplanung**, wann dieses Paket und dieses Programm bereitgestellt oder für Clientgeräte verfügbar gemacht werden.  

     Welche Optionen auf dieser Seite verfügbar sind, ist davon abhängig, ob die Bereitstellungsaktion auf **Verfügbar** oder **Erforderlich**gesetzt ist.  

9. Konfigurieren Sie unter **Zeitplanung**die folgenden Einstellungen, und klicken Sie dann auf **Weiter**.  

    1.  **Verfügbarkeitsdatum der Bereitstellung festlegen:** Geben Sie den Zeitpunkt (Datum und Uhrzeit) an, zu dem das Paket und das Programm zur Ausführung auf dem Zielcomputer verfügbar sind. Wenn Sie das Kontrollkästchen **UTC**aktivieren, sind das Paket und das Programm zum gleichen Zeitpunkt für mehrere Zielcomputer verfügbar, anstatt der lokalen Zeit auf den Zielcomputern entsprechend zu unterschiedlichen Zeitpunkten.  

    2.  **Ablaufdatum der Bereitstellung festlegen**: Geben Sie den Zeitpunkt (Datum und Uhrzeit) an, zu dem das Paket und das Programm auf dem Zielcomputer ablaufen. Wenn Sie **UTC**auswählen, endet die Gültigkeit der Tasksequenz auf mehreren Zielcomputern zum gleichen Zeitpunkt, anstatt der lokalen Zeit auf den Zielcomputern entsprechend zu unterschiedlichen Zeitpunkten.  

10. Geben Sie auf der Seite **Benutzerfreundlichkeit** des Assistenten die folgenden Informationen an:  

    -   **Softwareinstallation:** Ermöglicht die Installation der Software außerhalb konfigurierter Wartungsfenster.  

    -   **Systemneustart (falls dieser zum Abschluss der Installation erforderlich ist)** : Ermöglicht das Neustarten eines Geräts außerhalb konfigurierter Wartungsfenster, wenn dies bei der Softwareinstallation erforderlich ist.  

    -   **Eingebettete Geräte:** Beim Bereitstellen von Paketen und Programmen für Windows Embedded-Geräte mit Schreibfilteraktivierung können Sie angeben, dass die Pakete und Programme auf dem temporären Overlay gespeichert und die Änderungen später ausgeführt werden oder dass sie am Installationsstichtag oder während eines Wartungsfensters ausgeführt werden sollen. Falls die Änderungen am Installationsstichtag oder während eines Wartungsfensters ausgeführt werden, ist ein Neustart erforderlich, und die Änderungen werden auf dem Gerät beibehalten.  

11. Geben Sie auf der Seite **Verteilungspunkte** die folgenden Informationen an:  

    -   **Bereitstellungsoptionen:** Geben Sie **Inhalt vom Verteilungspunkt herunterladen und lokal ausführen** an.  

    -   **Freigeben von Inhalten für andere Clients im gleichen Subnetz zulassen:** Wählen Sie diese Option aus, um das Herunterladen von Inhalten von anderen Clients im Netzwerk zuzulassen, von denen die Inhalte bereits heruntergeladen und zwischengespeichert wurden, und so die Netzwerkauslastung zu reduzieren. Bei dieser Option, die auf Computern verwendet werden kann, auf denen Windows Vista SP2 und höher ausgeführt wird, wird Windows BranchCache verwendet.  

    -   **Die Verwendung eines Fallbackquellpfads für den Inhalt durch Clients zulassen:** Geben Sie an, ob zugelassen werden soll, dass Clients einen nicht bevorzugten Verteilungspunkt als Quellspeicherort für Inhalte verwenden, wenn die Inhalte an keinem bevorzugten Verteilungspunkt verfügbar sind.  

12. Schließen Sie den Assistenten ab.  

#### <a name="to-deploy-the-windows-8-task-sequence"></a>So stellen Sie die Windows 8-Tasksequenz bereit  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Tasksequenzen**.  

3.  Wählen Sie die Windows 8-Tasksequenz aus, die Sie im Schritt [Prerequisites to provision Windows To Go](#BKMK_Prereqs) erstellt haben.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Bereitstellen**.  

5.  Geben Sie auf der Seite **Allgemein** die folgenden Einstellungen an:  

    1.  **Tasksequenz:** Vergewissern Sie sich, dass die Windows 8-Tasksequenz ausgewählt ist.  

    2.  **Sammlung:** Klicken Sie auf **Durchsuchen**, um die Sammlung mit allen Geräten auszuwählen, für die möglicherweise eine Bereitstellung von Windows To Go erforderlich ist.  

        > [!IMPORTANT]  
        >  Wenn vom vorab bereitgestellten Medium, das Sie im Schritt [Erstellen von vorab bereitgestellten Medien](#BKMK_CreatePrestagedMedia) erstellt haben, die Variable **SMSTSPreferredAdvertID** verwendet wird, können Sie die Tasksequenz für die Sammlung **Alle Systeme** bereitstellen und auf der Seite **Inhalt** die Einstellung Nur Windows PE (ausgeblendet) angeben. Da die Tasksequenz ausgeblendet ist, steht sie nur Medien zur Verfügung.  

    3.  **Standard-Verteilungspunktgruppen verwenden, die dieser Sammlung zugeordnet sind**: Wählen Sie diese Option aus, wenn Sie den Paketinhalt in der standardmäßigen Verteilungspunktgruppe der Sammlung speichern möchten. Wenn die ausgewählte Sammlung keiner Verteilungspunktgruppe zugeordnet ist, ist diese Option nicht verfügbar.  

6.  Konfigurieren Sie auf der Seite **Bereitstellungseinstellungen** die folgenden Einstellungen, und klicken Sie dann auf **Weiter**.  

    -   **Zweck:** Wählen Sie **Verfügbar** aus. Wenn die Tasksequenz für einen Benutzer bereitgestellt wird, wird die veröffentlichte Tasksequenz dem Benutzer im Anwendungskatalog angezeigt, wo er sie bei Bedarf anfordern kann. Wenn die Tasksequenz auf einem Gerät bereitgestellt wird, wird sie dem Benutzer im Softwarecenter angezeigt, und der Benutzer kann sie bei Bedarf installieren.  

    -   **Verfügbar machen für:** Geben Sie an, ob die Tasksequenz für Configuration Manager-Clients, Medien oder die PXE verfügbar sein soll.  

        > [!IMPORTANT]  
        >  Verwenden Sie die Einstellung **Nur Medien und PXE (ausgeblendet)** für automatisierte Bereitstellungen von Tasksequenzen. Aktivieren Sie die Option **Unbeaufsichtigte Betriebssystembereitstellung zulassen** , und legen Sie die Variable SMSTSPreferredAdvertID als Teil des vorab bereitgestellten Mediums fest, damit der Computer ohne Benutzerinteraktion bei der Bereitstellung von Windows To Go automatisch gestartet wird, sobald ein Windows To Go-Laufwerk erkannt wird. Weitere Informationen zu den Einstellungen dieser vorab bereitgestellten Medien finden Sie im Abschnitt [Create prestaged media](#BKMK_CreatePrestagedMedia) .  

7.  Konfigurieren Sie auf der Seite **Zeitplanung** die folgenden Einstellungen, und klicken Sie dann auf **Weiter**.  

    1.  **Verfügbarkeitsdatum der Bereitstellung festlegen**: Geben Sie den Zeitpunkt (Datum und Uhrzeit) an, zu dem die Tasksequenz zur Ausführung auf dem Zielcomputer verfügbar ist. Wenn Sie das Kontrollkästchen **UTC**aktivieren, ist die Tasksequenz zum gleichen Zeitpunkt für mehrere Zielcomputer verfügbar, anstatt der lokalen Zeit auf den Zielcomputern entsprechend zu unterschiedlichen Zeitpunkten.  

    2.  **Ablaufdatum der Bereitstellung festlegen:** Geben Sie den Zeitpunkt (Datum und Uhrzeit) an, zu dem die Tasksequenz auf dem Zielcomputer abläuft. Wenn Sie **UTC**auswählen, endet die Gültigkeit der Tasksequenz auf mehreren Zielcomputern zum gleichen Zeitpunkt, anstatt der lokalen Zeit auf den Zielcomputern entsprechend zu unterschiedlichen Zeitpunkten.  

8.  Geben Sie auf der Seite **Benutzerfreundlichkeit** die folgenden Informationen an:  

    -   **Tasksequenzstatus anzeigen:** Geben Sie an, ob der Status der Tasksequenz vom Configuration Manager-Client angezeigt wird.  

    -   **Softwareinstallation**: Geben Sie an, ob der Benutzer nach dem geplanten Zeitpunkt außerhalb eines konfigurierten Wartungsfensters Software installieren darf.  

    -   **Systemneustart (falls dieser zum Abschluss der Installation erforderlich ist):** Ermöglicht das Neustarten eines Geräts außerhalb konfigurierter Wartungsfenster, wenn dies bei der Softwareinstallation erforderlich ist.  

    -   **Eingebettete Geräte:** Beim Bereitstellen von Paketen und Programmen für Windows Embedded-Geräte mit Schreibfilteraktivierung können Sie angeben, dass die Pakete und Programme auf dem temporären Overlay gespeichert und die Änderungen später ausgeführt werden oder dass sie am Installationsstichtag oder während eines Wartungsfensters ausgeführt werden sollen. Falls die Änderungen am Installationsstichtag oder während eines Wartungsfensters ausgeführt werden, ist ein Neustart erforderlich, und die Änderungen werden auf dem Gerät beibehalten.  

    -   **Internetbasierte Clients:** Geben Sie an, ob die Tasksequenz auf einem internetbasierten Client ausgeführt werden darf. Vorgänge, mit denen Software wie ein Betriebssystem installiert wird, werden von dieser Einstellung nicht unterstützt. Verwenden Sie diese Option nur für generische skriptbasierte Tasksequenzen, mit denen Vorgänge im Standardbetriebssystem ausgeführt werden.  

9. Geben Sie auf der Seite **Warnungen** die für diese Tasksequenzbereitstellung gewünschten Warnungseinstellungen an, und klicken Sie dann auf **Weiter**.  

10. Geben Sie auf der Seite **Verteilungspunkte** die folgenden Informationen an, und klicken Sie dann auf **Weiter**.  

    -   **Bereitstellungsoptionen:** Wählen Sie **Inhalt lokal herunterladen, wenn dies für die Ausführung der Tasksequenz erforderlich ist** aus.  

    -   **Remoteverteilungspunkt verwenden, wenn kein lokaler Verteilungspunkt verfügbar ist:** Geben Sie an, ob Clients Verteilungspunkte in langsamen und unzuverlässigen Netzwerken verwenden dürfen, um Inhalte herunterzuladen, die für die Tasksequenz erforderlich sind.  

    -   **Die Verwendung eines Fallbackquellpfads für den Inhalt durch Clients zulassen**:
        - *Vor Version 1610* können Sie das Kontrollkästchen „Fallbackquellpfad für Inhalt zulassen“ aktivieren, um für Clients außerhalb solcher Begrenzungsgruppen ein Ausweichen auf den Verteilungspunkt als Quellort für Inhalt zu ermöglichen, wenn keine anderen Verteilungspunkte verfügbar sind.
        - *Ab Version 1610* können Sie **Fallbackquellpfad für Inhalt zulassen** nicht mehr konfigurieren.  Stattdessen können Sie Beziehungen zwischen Begrenzungsgruppen konfigurieren, die bestimmen, ab wann ein Client mit der Suche nach zusätzlichen Begrenzungsgruppen für einen gültigen Quellspeicherort für den Inhalt suchen kann. 

11. Schließen Sie den Assistenten ab.  

###  <a name="user-runs-the-windows-to-go-creator"></a><a name="BKMK_UserExperience"></a> Benutzer führt Windows To Go Creator aus  
 Nach der Bereitstellung des Windows To Go-Pakets und der Windows 8-Tasksequenz steht dem Benutzer der Windows To Go Creator zur Verfügung. Der Benutzer kann den Softwarekatalog bzw. das Softwarecenter (bei Bereitstellung von Windows To Go auf Geräten) aufrufen und das Programm „Windows To Go Creator“ ausführen. Sobald das Creator-Paket heruntergeladen wurde, wird auf der Taskleiste ein blinkendes Symbol angezeigt. Wenn der Benutzer auf das Symbol klickt, wird ein Dialogfeld angezeigt, in dem das Laufwerk für die Bereitstellung von Windows To Go ausgewählt werden kann (es sei denn, es wird die Befehlszeilenoption /drive verwendet). Wenn die Anforderungen von Windows To Go vom Laufwerk nicht erfüllt werden können oder auf dem Laufwerk nicht genügend freier Speicherplatz vorhanden ist, wird von Creator eine Fehlermeldung angezeigt. Der Benutzer kann Laufwerk und Abbild, die über die Bestätigungsseite angewendet werden, überprüfen. Während der Konfiguration und Vorabbereitstellung von Inhalten auf dem Windows To Go-Laufwerk von Creator wird ein Fortschrittsdialogfeld angezeigt. Nach Abschluss der Vorabbereitstellung wird von Creator eine Aufforderung zum Neustarten des Computers vom Windows To Go-Laufwerk angezeigt.  

> [!NOTE]  
>  Wenn Sie im Abschnitt [Erstellen eines Windows To Go Creator-Pakets](#BKMK_CreatePackage) als Teil der Befehlszeile von Creator nicht die Startumleitung aktiviert haben, muss der Benutzer möglicherweise bei jedem Systemneustart manuell vom Windows To Go-Laufwerk starten.  

###  <a name="configuration-manager-configures-and-stages-the-windows-to-go-drive"></a><a name="BKMK_ConfigureStageDrive"></a> Configuration Manager konfiguriert das Windows To Go-Laufwerk und stellt es vorab bereit  
 Nach dem Neustart des Computers vom Windows To Go-Laufwerk wird vom Laufwerk Windows PE gestartet und eine Verbindung zum Verwaltungspunkt hergestellt, um die Richtlinie zum Abschließen der Bereitstellung des Betriebssystems abzurufen. Configuration Manager konfiguriert das Laufwerk und stellt es vorab bereit. Nach der Bereitstellung des Laufwerks durch Configuration Manager kann der Benutzer den Computer neu starten, um den Bereitstellungsvorgang abzuschließen (z.B. einer Domäne beitreten oder Apps installieren). Dieser Vorgang ist bei allen vorab bereitgestellten Medien identisch.  

###  <a name="user-logs-in-to-windows-8"></a><a name="BKMK_UserLogsIn"></a> Benutzer meldet sich bei Windows 8 an  
 Nach Abschluss des Bereitstellungsvorgangs durch Configuration Manager und sobald der Windows 8-Sperrbildschirm angezeigt wird, kann sich der Benutzer beim Betriebssystem anmelden.  
