---
title: Backup-Standorte
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Ihre Standorte vor einem Ausfall oder Datenverlust in Configuration Manager sichern.
ms.date: 01/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f7832d83-9ae2-4530-8a77-790e0845e12f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8d766a172f934e27398ec2633ef0ec23ba4ade5e
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700683"
---
# <a name="back-up-a-configuration-manager-site"></a>Sichern eines Configuration Manager-Standorts

*Gilt für: Configuration Manager (Current Branch)*

Bereiten Sie Sicherungs- und Wiederherstellungs-Ansätze vor, um Datenverluste zu vermeiden. Für Configuration Manager-Standorte kann ein Ansatz für die Sicherung und Wiederherstellung dazu beitragen, Standorte und Hierarchien schneller und mit geringstem Datenverlust wiederherzustellen.  

Die Abschnitte in diesem Artikel können Ihnen beim Sichern Ihrer Standorte helfen. Informationen zur Wiederherstellung eines Standorts finden Sie unter [Wiederherstellung für Configuration Manager](recover-sites.md).  

<!--/SCCMdocs/issues/2108-->
>[!WARNING]
> Für die Configuration Manager-Standortwiederherstellung werden die beiden folgenden Sicherungsmethoden unterstützt:
>
> - Eine erfolgreiche Sicherung durch die Wartungsaufgabe **Standortserver sichern**
> - Eine manuell wiederhergestellte Standortdatenbanksicherung


## <a name="considerations-before-creating-a-backup"></a>Überlegungen vor dem Erstellen einer Sicherung  

-   Wenn Sie eine Always On-Verfügbarkeitsgruppe für SQL Server zum Hosten der Standortdatenbank verwenden: Passen Sie Ihre Sicherungs- und Wiederherstellungspläne an wie in [Vorbereiten der Verwendung von SQL Server Always On-Verfügbarkeitsgruppen mit Configuration Manager](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#changes-for-site-backup) beschrieben.  

-   Configuration Manager kann die Standortdatenbank über den Sicherungstask von Configuration Manager wiederherstellen. Zudem kann eine Sicherung der Standortdatenbank verwendet werden, die Sie mit einem anderen Prozess erstellen.   

     Beispielsweise können Sie die Standortdatenbank anhand einer Sicherung wiederherstellen, die im Rahmen des Microsoft SQL Server-Wartungsplans erstellt wurde. Sie können auch eine Sicherung, die mithilfe von Data Protection Manager erstellt wurde, zur Sicherung Ihrer Standortdatenbank verwenden.  

-   Ab Version 1806 wird ein zusätzlicher Standortserver im *passiven* Modus installiert. Der Standortserver im passiven Modus dient als Ergänzung zu Ihrem vorhandenen Standortserver im *aktiven* Modus. Ein Standortserver im passiven Modus ist bei Bedarf sofort einsatzbereit. Weitere Informationen finden Sie unter [Standortserver-Hochverfügbarkeit](../deploy/configure/site-server-high-availability.md). Durch diese Rolle wird die Notwendigkeit zum Planen und Durchführen von Sicherungs- und Wiederherstellungsvorgängen zwar nicht hinfällig, allerdings kann der Aufwand zur Wiederherstellung eines Standorts deutlich verringert werden.  
  

####  <a name="using-data-protection-manager-to-back-up-your-site-database"></a>Verwenden von Data Protection Manager zur Sicherung der Standortdatenbank
Sie können Ihre Configuration Manager-Standortdatenbank mit System Center Data Protection Manager (DPM) sichern.

Erstellen Sie in DPM eine neue Schutzgruppe für den Standortdatenbankcomputer. Auf der Seite **Gruppenmitglieder auswählen** des Assistenten zum Erstellen neuer Schutzgruppen wählen Sie den SMS-Writer-Dienst aus der Datenquellenliste aus. Anschließend wählen Sie die Standortdatenbank als geeignetes Mitglied aus. Weitere Informationen zur Verwendung von DPM finden Sie in der [Data Protection Manager-Dokumentationsbibliothek](/system-center/dpm).  

> [!IMPORTANT]  
>  Configuration Manager unterstützt nicht die DPM-Sicherung für einen SQL Server-Cluster, der eine benannte Instanz verwendet. Die Lösung unterstützt die DPM-Sicherung auf einem SQL Server-Cluster, der die Standardinstanz von SQL Server verwendet.  

Nachdem Sie die Standortdatenbank wiederhergestellt haben, befolgen Sie die Schritte im Setup, um den Standort wiederherzustellen. Wenn Sie die Standortdatenbank verwenden möchten, die Sie mit Data Protection Manager gesichert haben, müssen Sie die Wiederherstellungsoption **Manuell wiederhergestellte Standortdatenbank verwenden** auswählen.  



## <a name="backup-maintenance-task"></a>Sicherungswartungstask
Durch Planen des vordefinierten Wartungstasks „Standortserver sichern“ können Sie die Sicherung von Configuration Manager-Standorten automatisieren. Dieser Task zeichnet sich durch folgende Features aus:

-   Wird nach einem Zeitplan ausgeführt
-   Sichert die Standortdatenbank
-   Sichert bestimmte Registrierungsschlüssel
-   Sichert bestimmte Ordner und Dateien
-   Sichert den Ordner [CD.Latest](the-cd.latest-folder.md)   

Planen Sie, den Standardtask für die Standortsicherung mindestens alle fünf Tage auszuführen. Der Grund für diesen Zeitplan ist, dass Configuration Manager für die *Beibehaltungsdauer der Änderungsnachverfolgung für SQL Server* einen Zeitraum von fünf Tagen verwendet. Weitere Informationen finden Sie unter [Beibehaltungsdauer der Änderungsnachverfolgung für SQL Server](recover-sites.md#sql-server-change-tracking-retention-period).

Zur Vereinfachung des Sicherungsprozesses können Sie die Datei **AfterBackup.bat** erstellen. Dieses Skript führt automatisch Aktionen nach der Sicherung durch, nachdem der Sicherungstask erfolgreich abgeschlossen wurde. Verwenden Sie die Datei „AfterBackup.bat“ zur Archivierung der Sicherungsmomentaufnahme an einem sicheren Speicherort. Sie können mit der Datei „AfterBackup.bat“ auch Dateien in Ihren Sicherungsordner kopieren oder andere Sicherungstasks starten.  

Sie können einen Standort der zentralen Verwaltung und einen primären Standort sichern. Für sekundäre Standorte oder Standortsystemserver gibt es keine Sicherungstasks.

Wenn der Sicherungsdienst von Configuration Manager ausgeführt wird, läuft dieser Vorgang entsprechend den in der Sicherungssteuerungsdatei definierten Anweisungen ab: `<ConfigMgrInstallationFolder>\Inboxes\Smsbkup.box\Smsbkup.ctl`. Sie können die Sicherungssteuerungsdatei ändern, um das Verhalten des Sicherungsdienstes zu ändern.  
> [!NOTE]
> Änderungen an **Smsbkup.ctl** werden nach einem Neustart des SMS_SITE_VSS_WRITER-Diensts auf dem Standortserver wirksam.

Informationen zum Status der Standortsicherung werden in die Datei **Smsbkup.log** geschrieben. Diese Datei wird in dem Zielordner erstellt, den Sie in den Eigenschaften des Wartungstasks „Standortserver sichern“ angeben.  

#### <a name="to-enable-the-site-backup-maintenance-task"></a>So aktivieren Sie den Wartungstask zur Standortsicherung  
1.  Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie den Knoten **Standorte** aus.  

2.  Wählen Sie den Standort aus, für den Sie den Wartungstask zur Standortsicherung aktivieren möchten.  

3.  Klicken Sie im Menüband auf **Standortwartungstasks**.  

4.  Wählen Sie den Task **Standortserver sichern** aus, und klicken Sie auf **Bearbeiten**.  

5.  Wählen Sie die Option **Enable this task** (Diesen Task aktivieren) aus. Klicken Sie auf **Pfade festlegen**, um das Sicherungsziel anzugeben. Hierzu stehen Ihnen folgende Optionen zur Verfügung:  

    > [!IMPORTANT]  
    >  Speichern Sie die Dateien an einem sicheren Ort, um einer Manipulation der Sicherungsdateien vorzubeugen. Der sicherste Pfad für eine Sicherung ist ein lokales Laufwerk, sodass Sie NTFS-Dateiberechtigungen für den Ordner einrichten können. Configuration Manager verschlüsselt nicht die Sicherungsdaten, die im Sicherungspfad gespeichert sind.  

    -   **Lokales Laufwerk auf Standortserver für Standortdaten und -datenbank:** Bei Auswahl dieser Option werden die Sicherungsdateien für den Standort und die Standortdatenbank im angegebenen Pfad auf dem lokalen Laufwerk des Standortservers gespeichert. Erstellen Sie den lokalen Ordner, bevor der Sicherungstask ausgeführt wird. Das lokale Systemkonto auf dem Standortserver muss über die NTFS-Dateiberechtigung **Schreiben** für den lokalen Ordner verfügen, der für die Sicherung des Standorts vorgesehen ist. Das lokale Systemkonto auf dem Computer, auf dem SQL Server ausgeführt wird, muss über die NTFS-Berechtigung **Schreiben** für den Ordner verfügen, der für die Sicherung der Standortdatenbank vorgesehen ist.  

    -   **Netzwerkpfad (UNC-Name) für Standortdaten und -datenbank:** Bei Auswahl dieser Option werden die Sicherungsdateien für den Standort und die Standortdatenbank im angegebenen Netzwerk-Pfad gespeichert. Erstellen Sie die Freigabe, bevor der Sicherungstask ausgeführt wird. Für das Computerkonto des Standortservers müssen die NTFS-Berechtigung **Schreiben** und die Freigabeberechtigungen für den freigegebenen Netzwerkordner vorliegen. Wenn SQL Server auf einem anderen Computer installiert ist, muss das Computerkonto von SQL Server die gleichen Berechtigungen aufweisen.  

    -   **Lokale Laufwerke auf dem Standortserver und SQL Server:** Gibt an, dass der Task die Sicherungsdateien für den Standort im angegebenen Pfad auf dem lokalen Laufwerk des Standortservers speichert. Der Task speichert die Sicherungsdateien für die Standortdatenbank im angegebenen Pfad auf dem lokalen Laufwerk des Standortdatenbankservers. Erstellen Sie die lokalen Ordner, bevor der Sicherungstask ausgeführt wird. Für das Computerkonto des Standortservers müssen die NTFS-Berechtigungen **Schreiben** für den Ordner vorliegen, den Sie auf dem Standortserver erstellen. Für das Computerkonto des SQL Servers müssen die NTFS-Berechtigungen **Schreiben** für den Ordner vorliegen, den Sie auf dem Standortdatenbankserver erstellen. Diese Option ist nur verfügbar, wenn die Standortdatenbank nicht auf dem Standortserver installiert ist.  

    > [!NOTE]  
    > Die Option zum Durchsuchen des Sicherungsziels ist nur verfügbar, wenn Sie den Netzwerkpfad des Sicherungsziels angeben.  
    >  
    > Der Ordner- oder Freigabename, der für das Sicherungsziel verwendet wird, darf keine Unicode-Zeichen enthalten.  

6.  Konfigurieren Sie einen Zeitplan für den Standortsicherungstask. Ziehen Sie einen Sicherungszeitplan in Erwägung, der außerhalb der Arbeitszeit liegt. Wenn Sie über eine Hierarchie verfügen, sollten Sie einen Zeitplan in Erwägung ziehen, der mindestens zweimal pro Woche ausgeführt wird. Treten am Standort Fehler auf, wird durch diesen Zeitplan eine maximale Datenaufbewahrung sichergestellt.  

    Wenn Sie die Configuration Manager-Konsole auf dem gleichen Standortserver ausführen, den Sie für die Sicherung konfigurieren, wird bei dem Sicherungstask die lokale Zeit für den Zeitplan verwendet. Wenn Sie die Configuration Manager-Konsole von einem anderen Computer aus ausführen, wird bei dem Sicherungstask die Koordinierte Weltzeit (UTC) für den Zeitplan verwendet.  

7.  Geben Sie an, ob eine Warnung erstellt werden soll, wenn der Standortsicherungstask fehlschlägt. Bei Auswahl erstellt Configuration Manager eine kritische Warnung für den Sicherungsfehler. Sie können diese Warnungen im Arbeitsbereich **Überwachung** über den Knoten **Warnungen** anzeigen.  

#### <a name="verify-that-the-backup-site-server-maintenance-task-is-running"></a>Überprüfen, ob der Wartungstask „Standortserver sichern“ ausgeführt wird  

-   Überprüfen Sie den Zeitstempel auf den Dateien im Sicherungszielordner, die vom Task erstellt wurden. Überprüfen Sie, ob der Zeitstempel auf die Zeit aktualisiert wird, zu der die Ausführung des Tasks laut Zeitplan zuletzt vorgesehen war.  

-   Wechseln Sie im Arbeitsbereich **Überwachung** zum Knoten **Komponentenstatus**. Überprüfen Sie die Statusmeldungen für **SMS_SITE_BACKUP**. Wenn die Standortsicherung erfolgreich abgeschlossen wird, wird Ihnen die Nachrichten-ID **5035** angezeigt. Diese Meldung zeigt an, dass die Standortsicherung ohne Fehler abgeschlossen wurde.  

-   Wenn Sie den Sicherungstask so konfigurieren, dass eine Warnung erstellt wird, wenn dieser fehlschlägt, suchen Sie im Arbeitsbereich **Überwachung** im Knoten **Alerts** nach Warnungen zu Sicherungsfehlern.  

-   Öffnen Sie Windows-Explorer auf dem Standortserver, und navigieren Sie zu dem Ordner `<ConfigMgrInstallationFolder>\Logs`. Überprüfen Sie die Datei **Smsbkup.log** auf Warnungen und Fehler. Wenn die Standortsicherung erfolgreich abgeschlossen wird, zeigt das Protokoll `Backup completed` mit der Nachrichten-ID `STATMSG: ID=5035` an.  

    > [!TIP]  
    >  Wenn bei dem Sicherungswartungstask ein Fehler auftritt, können Sie den Task durch Anhalten und Neustarten des Windows-Diensts **SMS_SITE_BACKUP** neu starten.  



## <a name="archive-the-backup-snapshot"></a>Archivieren der Sicherungsmomentaufnahme  
Der Sicherungstask erstellt bei der ersten Ausführung eine Sicherungsmomentaufnahme. Sie können Ihren Standortserver mithilfe dieser Momentaufnahme wiederherstellen, falls auf diesem ein Fehler auftreten sollte. Wenn der Sicherungstask erneut ausgeführt wird, wird jeweils eine neue Sicherungsmomentaufnahme erstellt, durch welche die vorherige Momentaufnahme überschrieben wird. Für einen Standort gibt es daher immer nur eine Sicherungsmomentaufnahme, und es ist nicht möglich, eine frühere Sicherungsmomentaufnahme abzurufen.  

Sie sollten aus den folgenden Gründen mehrere Archive der Sicherungsmomentaufnahme aufbewahren:  

-   Es kommt häufig vor, dass Sicherungsmedien ausfallen, verlegt werden oder nur eine unvollständige Sicherung enthalten. Das Wiederherstellen eines ausgefallenen eigenständigen primären Standorts anhand einer älteren Sicherung ist besser als das Wiederherstellen ohne Sicherung. Bei einem Standortserver in einer Hierarchie muss die Sicherung innerhalb der Beibehaltungsdauer der Änderungsnachverfolgung für SQL Server liegen. Andernfalls ist die Sicherung nicht erforderlich.  

-   Eine Beschädigung im Standort kann über mehrere Sicherungszyklen hinweg unentdeckt bleiben. Sie müssen möglicherweise eine Sicherungsmomentaufnahme verwenden, die vor der Beschädigung des Standorts erstellt wurde. Dies gilt für einen eigenständigen primären Standort und Standorte in einer Hierarchie, bei denen die Sicherung innerhalb der Beibehaltungsdauer der Änderungsnachverfolgung für SQL Server liegt.  

-   Möglicherweise gibt es für den Standort gar keine Sicherungsmomentaufnahme. Dies ist beispielsweise der Fall, wenn der Wartungstask „Standortserver sichern“ fehlschlägt. Da der Sicherungstask die vorherige Sicherungsmomentaufnahme entfernt, bevor mit dem Sichern der aktuellen Daten begonnen wird, gibt es zeitweise keine gültige Sicherungsmomentaufnahme.  



## <a name="using-the-afterbackupbat-file"></a>Verwenden der Datei „AfterBackup.bat“  
Nach der erfolgreichen Sicherung des Standorts versucht der Sicherungstask automatisch, ein Skript mit dem Namen **AfterBackup.bat** auszuführen. Erstellen Sie die Datei „AfterBackup.bat“ manuell auf den Standortserver in `<ConfigMgrInstallationFolder>\Inboxes\Smsbkup.box`. Wenn die Datei „AfterBackup.bat“ im richtigen Ordner vorhanden ist, wird sie nach Abschluss des Sicherungstasks automatisch ausgeführt.

Mithilfe der Datei „AfterBackup.bat“ können Sie die Sicherungsmomentaufnahme am Ende jedes Sicherungsvorgangs archivieren. Zudem können automatisch Tasks nach der Sicherung durchgeführt werden, die nicht Teil des Wartungstasks „Standortserver sichern“ sind. Mit der Datei AfterBackup.bat werden die Archivierungs- und Sicherungsvorgänge integriert. Dadurch wird sichergestellt, dass jede neue Sicherungsmomentaufnahme archiviert wird.

Wenn die Datei „AfterBackup.bat“ nicht vorhanden ist, wird sie vom Sicherungstask übersprungen. Dies hat keine Auswirkungen auf den Sicherungsvorgang. Prüfen Sie im Arbeitsbereich **Überwachung** im Knoten **Komponentenstatus** die Statusmeldungen für **SMS_SITE_BACKUP**. Daran erkennen Sie, ob der Sicherungstask dieses Skript erfolgreich ausgeführt hat. Wenn der Task die Befehlsdatei „AfterBackup.bat“ erfolgreich startet, wird Ihnen die Nachrichten-ID **5040** angezeigt.  

> [!TIP]  
>  Zur Archivierung der Sicherungsdateien für den Standortserver mithilfe der Datei „AfterBackup.bat“ müssen Sie in der Batchdatei ein Kopierbefehlstool verwenden. [Robocopy](/windows-server/administration/windows-commands/robocopy) in Windows Server ist beispielsweise ein solches Tool. Erstellen Sie die Datei „AfterBackup.bat“ beispielsweise mit dem folgenden Befehl: `Robocopy E:\ConfigMgr_Backup \\ServerName\ShareName\ConfigMgr_Backup /MIR`  

Die Datei „AfterBackup.bat“ ist zwar zum Archivieren von Sicherungsmomentaufnahmen vorgesehen, Sie können aber auch die Datei „AfterBackup.bat“ erstellen, um am Ende jedes Sicherungsvorgangs zusätzliche Tasks auszuführen.  



##  <a name="supplemental-backup-tasks"></a>Zusätzliche Sicherungstasks  
Der Wartungstask „Standortserver sichern“ stellt eine Sicherungsmomentaufnahme für die Standortserverdateien und die Standortdatenbank bereit. Bei der Ausarbeitung Ihrer Strategie müssen weitere Elemente berücksichtigt werden, die noch nicht gesichert wurden. In den folgenden Abschnitten erfahren Sie, wie Sie eine Configuration Manager-Sicherungsstrategie vervollständigen.  

### <a name="back-up-custom-reports"></a>Sichern benutzerdefinierter Berichte   
Wenn Sie vordefinierte oder erstellte benutzerdefinierte Berichte in SQL Server Reporting Services ändern, müssen Sie eine Sicherung für die Berichtsserver-Datenbankdateien erstellen. Die Sicherung für den Berichtsserver muss folgende Komponenten umfassen:
- Die Quelldateien für Berichte und Modelle
- Verschlüsselungsschlüssel
- Benutzerdefinierte Assemblys oder Erweiterungen
- Konfigurationsdateien
- In benutzerdefinierten Berichten verwendete benutzerdefinierte SQL Server-Ansichten
- Benutzerdefinierte gespeicherte Prozeduren  

> [!IMPORTANT]  
>  Wenn Configuration Manager auf eine neuere Version aktualisiert wird, werden die vordefinierten Berichte möglicherweise von neuen Berichten überschrieben. Wenn Sie einen vordefinierten Bericht ändern, sollten Sie sicherstellen, dass der Bericht gesichert wurde, und ihn anschließend in Reporting Services wiederherstellen.  

Weitere Informationen zum Sichern benutzerdefinierter Berichte in Reporting Services finden Sie unter [Sicherungs- und Wiederherstellungsvorgänge für Reporting Services](/sql/reporting-services/install-windows/backup-and-restore-operations-for-reporting-services).  

### <a name="back-up-content-files"></a>Sichern von Inhaltsdateien  
Die Inhaltsbibliothek in Configuration Manager ist der Ort, an dem alle Inhaltsdateien für sämtliche Softwarebereitstellungen gespeichert werden. Sie befindet sich auf dem Standortserver und an jedem Verteilungspunkt. Der Wartungstask „Standortserver sichern“ führt keine Sicherung der Inhaltsbibliothek oder der Paketquelldateien aus. Beim Ausfall eines Standortservers werden die Informationen zur Inhaltsbibliothek in der Standortdatenbank wiederhergestellt. Sie müssen jedoch die Inhaltsbibliothek sowie die Paketquelldateien wiederherstellen.  

-   Die Inhaltsbibliothek muss wiederhergestellt werden, damit Sie Inhalt erneut an Verteilungspunkte verteilen können. Wenn Sie die Neuverteilung des Inhalts starten, werden die Dateien von Configuration Manager aus der Inhaltsbibliothek des Standortservers auf die Verteilungspunkte kopiert. Weitere Informationen finden Sie unter [Die Inhaltsbibliothek](../../plan-design/hierarchy/the-content-library.md).  

-   Die Paketquelldateien müssen wiederhergestellt werden, damit Sie ein Update des Inhalts an Verteilungspunkten ausführen können. Wenn Sie ein Inhaltsupdate starten, werden neue oder geänderte Dateien von Configuration Manager aus der Paketquelle in die Inhaltsbibliothek kopiert. Von dort werden die Dateien auf die zugeordneten Verteilungspunkte kopiert. Führen Sie in der Standortdatenbank die folgende Abfrage in SQL Server aus, um den Quellspeicherort für alle Pakete und Anwendungen zu ermitteln: `SELECT * FROM v_Package`. Sie können den Paketquellstandort anhand der ersten drei Zeichen der Paket-ID identifizieren. Wenn beispielsweise die Paket-ID „CEN00001“ lautet, ist „CEN“ der Standortcode für den Quellstandort. Paketquelldateien müssen an den gleichen Speicherort wiederhergestellt werden wie vor dem Fehler.  

Achten Sie darauf, bei der Dateisystemsicherung für den Standortserver sowohl die Inhaltsbibliothek als auch die Paketquelldateien einzuschließen.  

### <a name="back-up-custom-software-updates"></a>Sichern benutzerdefinierter Softwareupdates  
System Center Updates Publisher ist ein eigenständiges Tool, mit dem Sie benutzerdefinierte Softwareupdates verwalten können. Updates Publisher verwendet eine lokale Datenbank für das Softwareupdaterepository. Wenn Sie den Updates Publisher zur Verwaltung benutzerdefinierter Softwareupdates verwenden, legen Sie fest, ob die Updates Publisher-Datenbank in Ihrem Sicherungsplan enthalten sein muss. Weitere Informationen finden Sie unter [System Center Updates Publisher](../../../sum/tools/updates-publisher.md).  

Gehen Sie wie folgt vor, um die Updates Publisher-Datenbank zu sichern.  

#### <a name="back-up-the-updates-publisher-database"></a>Sichern der Updates Publisher-Datenbank  

1.  Navigieren Sie auf dem Computer, auf dem Updates Publisher ausgeführt wird, zur Updates Publisher-Datenbankdatei **Scupdb.sdf** in `%USERPROFILE%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\`. Für jeden Benutzer, der Updates Publisher ausführt, gibt es eine eigene Datenbankdatei.  

2.  Kopieren Sie die Datenbankdatei in das Sicherungsziel. Wenn das Sicherungsziel beispielsweise `E:\ConfigMgr_Backup` lautet, können Sie die Updates Publisher-Datenbankdatei in `E:\ConfigMgr_Backup\SCUP` kopieren.  

    > [!TIP]  
    >  Wenn es auf einem Computer mehrere Datenbankdateien gibt, empfiehlt es sich, die Datei in einem Unterordner zu speichern, der den Namen des mit der Datenbankdatei verbundenen Benutzerprofils trägt. Beispielsweise kann sich eine Datenbankdatei in `E:\ConfigMgr_Backup\SCUP\User1` und eine andere Datenbankdatei in `E:\ConfigMgr_Backup\SCUP\User2` befinden.  



## <a name="user-state-migration-data"></a>Daten zur Benutzerzustandsmigration  
Sie können die Tasksequenzen von Configuration Manager zum Erfassen und Wiederherstellen der Benutzerzustandsdaten in Bereitstellungsszenarios für Betriebssysteme verwenden. In den Eigenschaften des Zustandsmigrationspunkts werden die Ordner aufgeführt, in denen die Benutzerzustandsdaten gespeichert werden. Diese Daten werden im Rahmen des Wartungstasks „Standortserver sichern“ nicht gesichert. Im Rahmen Ihres Sicherungsplans müssen Sie die Ordner, in denen die Daten zur Benutzerzustandsmigration gespeichert werden, manuell sichern.   

### <a name="determine-the-folders-used-to-store-user-state-migration-data"></a>Bestimmen der Ordner, in denen die Daten zur Benutzerzustandsmigration gespeichert werden  

1.  Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie den Knoten **Server und Standortsystemrollen** aus.  

2.  Wählen Sie das Standortsystem aus, das die Zustandsmigrationsrolle hostet. Wählen Sie anschließend im Bereich **Standortsystemrollen** den Eintrag **Zustandsmigrationspunkt** aus.  

3.  Klicken Sie im Menüband auf **Eigenschaften**.  

4.  Die Ordner, in denen die Daten zur Benutzerzustandsmigration gespeichert werden, werden auf der Registerkarte **Allgemein** im Abschnitt **Ordnerdetails** aufgeführt.  



## <a name="about-the-sms-writer-service"></a>Informationen zum SMS-Writer-Dienst  
Während des Sicherungsprozesses findet zwischen dem SMS-Writer-Dienst und dem Volumeschattenkopie-Dienst von Windows (Volume Shadow Copy Service, VSS) eine Interaktion statt. Der SMS-Writer-Dienst muss ausgeführt werden, damit die Configuration Manager-Standortsicherung erfolgreich abgeschlossen werden kann.  

### <a name="process"></a>Prozess  
1. SMS-Writer wird beim VSS registriert und an dessen Schnittstellen und Ereignissse gebunden. 
2. Wenn vom VSS Ereignisse übertragen oder bestimmte Benachrichtigungen an SMS-Writer gesendet werden, wird von SMS-Writer daraufhin eine entsprechende Aktion ausgeführt. 
3. Zunächst wird die Sicherungssteuerungsdatei **smsbkup.ctl**, die sich in `<ConfigMgrInstallationPath>\inboxes\smsbkup.box` befindet, von SMS-Writer gelesen, und anschließend werden die zu sichernden Dateien und Daten ermittelt. 
4. Anschließend werden von SMS-Writer Metadaten erstellt, die sich aus verschiedenen Komponenten einschließlich bestimmter Daten aus den SMS-Registrierungsschlüsseln und -Unterschlüsseln zusammensetzen. 
    a. Die Metadaten werden an den VSS gesendet, wenn sie angefordert werden. 
    b. Der VSS sendet die Metadaten wiederum an die anfordernde Anwendung, den Configuration Manager-Sicherungs-Manager. 
5. Der Sicherungs-Manager wählt die zu sichernden Daten aus und sendet diese Daten über den VSS an SMS-Writer. 
6. Von SMS-Writer werden geeignete Maßnahmen zur Vorbereitung der Sicherung ergriffen. 
7. Später, wenn VSS für die Momentaufnahme bereit ist: a. VSS sendet ein Ereignis: b. Der SMS-Writer beendet sämtliche Configuration Manager-Dienste: c. Dadurch wird sichergestellt, dass die Configuration Manager-Aktivitäten während der Erstellung der Momentaufnahme fixiert sind. 
8. Nachdem die Momentaufnahme erstellt wurde, werden die Dienste und Aktivitäten von SMS-Writer neu gestartet.

Der SMS-Writer-Dienst wird automatisch installiert. Dieser Dienst muss ausgeführt werden, wenn eine Sicherungs- oder Wiederherstellungsanforderung von der VSS-Anwendung eingeht.  

### <a name="writer-id"></a>Writer-ID  
Die Writer-ID für den SMS-Writer lautet **03ba67dd-dc6d-4729-a038-251f7018463b**.  

### <a name="permissions"></a>Berechtigungen  
Der SMS-Writer-Dienst muss unter dem lokalen Systemkonto ausgeführt werden.  

### <a name="volume-shadow-copy-service"></a>Volumeschattenkopie-Dienst  
Der Volumeschattenkopie-Dienst (Volume Shadow Copy Service, VSS) ist ein Satz COM APIs, mit denen ein Framework implementiert wird. Dank dieses Frameworks können Volumesicherungen ausgeführt werden, während von Anwendungen auf einem System weiterhin auf die Volumes geschrieben wird. Mit dem VSS wird eine konsistente Schnittstelle bereitgestellt, mit der Benutzeranwendungen, die zum Ausführen eines Updates für Daten auf einem Datenträger dienen (SMS-Writer-Dienst), und Benutzeranwendungen, die zur Anwendungssicherung verwendet werden (Sicherungs-Manager-Dienst), koordiniert werden können. Weitere Informationen finden Sie unter [Volumeschattenkopie-Dienst](/windows-server/storage/file-server/volume-shadow-copy-service).  



## <a name="next-steps"></a>Nächste Schritte
Üben Sie nach der Erstellung einer Sicherung die [Standortwiederherstellung](recover-sites.md) mit dieser Sicherung. Mit dieser Methode können Sie sich mit dem Wiederherstellungsprozess vertraut machen, bevor Sie diesen verwenden müssen. Zudem dient sie zur Bestätigung, dass die Sicherung für die beabsichtigten Zwecke erfolgreich war.