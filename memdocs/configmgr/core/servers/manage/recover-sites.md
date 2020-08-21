---
title: Standortwiederherstellung
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Ihre Standorte in Configuration Manager wiederherstellen können.
ms.date: 06/02/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 19539f4d-1667-4b4c-99a1-9995f12cf5f7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9e71baef06349a00d49bc7fdc799d078c29939d8
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699516"
---
# <a name="recover-a-configuration-manager-site"></a>Wiederherstellen eines Configuration Manager-Standorts

*Gilt für: Configuration Manager (Current Branch)*

Führen Sie nach einem Standortausfall oder bei einem Datenverlust in der Standortdatenbank eine Configuration Manager-Sitewiederherstellung aus. Bei der Standortwiederherstellung geht es primär darum, Daten zu reparieren und erneut zu synchronisieren, um eine Unterbrechung von Vorgängen zu vermeiden.

Die Abschnitte in diesem Artikel helfen Ihnen bei der Wiederherstellung eines Configuration Manager-Standorts. Informationen zum Erstellen einer Sicherung finden Sie unter [Sichern eines Configuration Manager-Standorts](backup-and-recovery.md).

## <a name="considerations-before-recovering-a-site"></a>Überlegungen vor dem Wiederherstellen eines Standorts

> [!Important]  
> Diese Informationen gelten nur für Szenarien zur Standortwiederherstellung. Wenn Sie ein Upgrade Ihrer lokalen Infrastruktur durchführen und einen ausgefallenen Standort nicht aktiv wiederherstellen, lesen Sie die Informationen in den folgenden Artikeln:
>
> - [Ausführen eines Upgrades für die lokale Infrastruktur](upgrade-on-premises-infrastructure.md)
> - [Ändern der Infrastruktur](modify-your-infrastructure.md)

### <a name="prepare-the-server-hardware"></a>Vorbereiten der Serverhardware

<!-- 2841893 -->

Stellen Sie sicher, dass auf dem Standortserver keine Konfigurationen vorhanden sind. Vorherige Konfigurationen können während des Prozesses der Sitewiederherstellung zu Konflikten führen. Wählen Sie eine der folgenden Optionen für die Serverhardware aus:

- Verwenden Sie einen neuen Server, der die allgemeinen und Wiederherstellungsanforderungen erfüllt.

- Formatieren Sie die Datenträger, und installieren Sie das Betriebssystem auf dem vorhandenen Server neu. Stellen Sie sicher, dass er die allgemeinen und Wiederherstellungsanforderungen erfüllt.

- Verwenden Sie einen vorhandenen Server erneut, den Sie bereinigt haben.

Verwenden Sie eines der folgenden Verfahren, um einen vorhandenen Server zu bereinigen:

#### <a name="clean-an-existing-server-for-site-server-recovery-only"></a>Bereinigen eines vorhandenen Servers nur für die Wiederherstellung des Standortservers

1. Löschen Sie die SMS-Registrierungsschlüssel: `HKLM\Software\Microsoft\SMS`
2. Löschen Sie alle Registrierungseinträge, die mit `SMS` beginnen, aus `HKLM\System\CurrentControlSet\Services`. Beispiel:
    - SMS_DISCOVERY_DATA_MANAGER
    - SMS_EXECUTIVE
    - SMS_INBOX_MONITOR
    - SMS_INVENTORY_DATA_LOADER
    - SMS_LAN_SENDER
    - SMS_MP_FILE_DISPATCH_MANAGER
    - SMS_SCHEDULER
    - SMS_SITE_BACKUP
    - SMS_SITE_COMPONENT_MANAGER
    - SMS_SITE_SQL_BACKUP
    - SMS_SITE_VSS_WRITER
    - SMS_SOFTWARE_METERING_PROCESSOR
    - SMS_STATE_SYSTEM
    - SMS_STATUS_MANAGER
    - SMS_WSUS_SYNC_MANAGER
    - SMSvcHost 3.0.0.0
    - SMSvcHost 4.0.0.0
3. Deinstallieren Sie die Configuration Manager-Konsole.
4. Starten Sie den Server neu.
5. Vergewissern Sie sich, dass alle oben aufgeführten Registrierungsschlüssel gelöscht wurden.

Der Server ist nun für die Configuration Manager-Wiederherstellungsprozedur bereit.

#### <a name="clean-an-existing-server-for-site-database-recovery-only"></a>Bereinigen eines vorhandenen Servers nur für die Wiederherstellung der Standortdatenbank

1. Sichern Sie die Standortdatenbank. Sichern Sie außerdem alle anderen unterstützenden Datenbanken, wie z. B. WSUS.
2. Notieren Sie unbedingt den Namen des Servers für SQL Server und der Instanz.
3. Löschen Sie die Standortdatenbank manuell auf dem Server für SQL Server.
4. Starten Sie den Server für SQL Server neu.

Der Server ist nun für die Configuration Manager-Wiederherstellungsprozedur bereit.

#### <a name="clean-an-existing-server-for-full-recovery"></a>Bereinigen eines vorhandenen Servers für die vollständige Wiederherstellung

1. Sichern Sie die Standortdatenbank. Sichern Sie außerdem alle anderen unterstützenden Datenbanken, wie z. B. WSUS.
2. Erstellen Sie eine Kopie der Inhaltsbibliothek
3. Löschen Sie die Standortdatenbank manuell auf dem Server für SQL Server.
4. Deinstallieren Sie den Configuration Manager-Standort.
5. Löschen Sie den Configuration Manager-Installationsordner und alle anderen Configuration Manager-Ordner manuell.
6. Starten Sie den Server neu.
7. Stellen Sie die Inhaltsbibliothek und andere Datenbanken wie WSUS wieder her.

Der Server ist nun für die Configuration Manager-Wiederherstellungsprozedur bereit.

### <a name="use-a-supported-version-and-same-edition-of-sql-server"></a>Verwenden einer unterstützten Version und derselben Edition von SQL Server

<!-- SCCMDocs#751 -->

Verwenden Sie nach Möglichkeit dieselbe Version von SQL Server. Allerdings wird die Wiederherstellung einer Datenbank auf eine neuere Version unterstützt.

Ändern Sie die SQL Server-Edition nicht. Das Wiederherstellen einer Standortdatenbank aus der Standard Edition in der Enterprise Edition wird nicht unterstützt.

Zusätzliche Anforderungen an die SQL Server-Konfiguration:

- SQL Server darf nicht auf den **Einzelbenutzermodus** festgelegt werden.
- Stellen Sie sicher, dass die MDF- und LDF-Dateien gültig sind. Wenn Sie einen Standort wiederherstellen, wird der Status der Dateien nicht überprüft.  

### <a name="sql-server-always-on-availability-groups"></a>SQL Server Always On-Verfügbarkeitsgruppen

Wenn Sie SQL Server Always On-Verfügbarkeitsgruppen zum Hosten der Standortdatenbank verwenden, ändern Sie Ihre Wiederherstellungspläne gemäß der Anleitung unter [Prepare to use SQL Server Always On (Vorbereiten der Verwendung von SQL Server Always On)](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#changes-for-site-recovery).

### <a name="database-replicas"></a>Datenbankreplikate

Nachdem Sie eine für Datenbankreplikate konfigurierte Standortdatenbank wiederhergestellt haben, konfigurieren Sie jedes Replikat neu. Bevor Sie die Datenbankreplikate verwenden können, erstellen Sie die Veröffentlichungen und die Abonnements neu.

## <a name="determine-your-recovery-options"></a>Bestimmen der Wiederherstellungsoptionen

Bei der Wiederherstellung des primären Standortservers und des Standorts der zentralen Verwaltung (Central Administration Site, CAS) von Configuration Manager müssen Sie zwei wesentliche Aspekte berücksichtigen: den **Standortserver** und die **Standortdatenbank**.
Die folgenden Abschnitte helfen Ihnen bei der Auswahl der besten Optionen für Ihr Wiederherstellungsszenario.

> [!NOTE]  
> Wenn beim Setup von Configuration Manager ein vorhandener Standort auf dem Server erkannt wird, können Sie eine Sitewiederherstellung starten. Allerdings sind die Wiederherstellungsoptionen für den Standortserver beschränkt. Wenn Sie Setup beispielsweise auf einem vorhandenen Standortserver ausführen und die Wiederherstellung auswählen, können Sie zwar den Standortdatenbankserver wiederherstellen, aber die Option zum Wiederherstellen des Standortservers ist deaktiviert.

### <a name="site-server-recovery-options"></a>Wiederherstellungsoptionen für den Standortserver

Starten Sie das Setup von Configuration Manager über eine Kopie des Ordners **CD.Latest**, die Sie außerhalb des Configuration Manager-Installationsordners erstellt haben.  

- Wenn Sie Setup über das Menü **Start** auf dem Standortserver ausführen, ist die Option **Recover a site** (Standort wiederherstellen) nicht verfügbar.  

- Wenn Sie vor der Sicherung Updates mithilfe der Configuration Manager-Konsole installiert haben, können Sie den Standort nicht neu installieren, indem Sie das Setup von den folgenden Speicherorten verwenden:

  - Installationsmedien
  - Configuration Manager-Installationspfad

Wählen Sie dann die Option **Standort wiederherstellen** aus. Für den ausgefallenen Standortserver stehen die folgenden Wiederherstellungsoptionen zur Verfügung:  

#### <a name="recover-the-site-server-using-an-existing-backup"></a>Wiederherstellen des Standortservers mit vorhandener Sicherung

Verwenden Sie diese Option, wenn Sie über eine Configuration Manager-Sicherung des Standortservers von vor dem Standortausfall verfügen. Der Standort erstellt diese Sicherung als Teil des Wartungstasks **Standortserver sichern**. Der Standort wird erneut installiert, und die Standorteinstellungen werden anhand des gesicherten Standorts konfiguriert.  

#### <a name="reinstall-the-site-server"></a>Installieren Sie den Standortserver neu.

Verwenden Sie diese Option, wenn Sie über keine Sicherung des Standortservers verfügen. Der Standortserver wird erneut installiert, und Sie müssen die Standorteinstellungen wie bei einer Erstinstallation angeben.  

- Verwenden Sie den gleichen Standortcode und den gleichen Namen der Standortdatenbank, die Sie bei der Erstinstallation des ausgefallenen Standorts angegeben haben.  

- Sie können den Standort auf einem neuen Computer neu installieren, auf dem eine neue Betriebssystemversion ausgeführt wird.  

- Der Server muss den gleichen Hostnamen und den vollqualifizierten Domänennamen (FQDN) des ursprünglichen Standortservers verwenden.

### <a name="site-database-recovery-options"></a>Wiederherstellungsoptionen für die Standortdatenbank

Beim Ausführen des Configuration Manager-Setups stehen für die Standortdatenbank die folgenden Wiederherstellungsoptionen zur Verfügung:  

#### <a name="recover-the-site-database-using-a-backup-set"></a>Wiederherstellen der Standortdatenbank mit unterschiedlichen Sicherungen

Verwenden Sie diese Option, wenn Sie über eine Configuration Manager-Sicherung der Standortdatenbank von vor dem Datenbankfehler verfügen. Der Standort erstellt diese Sicherung als Teil des Wartungstasks **Standortserver sichern**. Wenn Sie in einer Hierarchie einen primären Standort wiederherstellen, ruft der Wiederherstellungsprozess vom CAS etwaige Änderungen ab, die nach der letzten Sicherung an der Standortdatenbank vorgenommen wurden. Wenn Sie den CAS wiederherstellen, ruft der Wiederherstellungsprozess diese Änderungen von einem primären Referenzstandort ab. Wenn Sie die Standortdatenbank für einen eigenständigen primären Standort wiederherstellen, gehen die Standortänderungen seit der letzten Sicherung verloren.  

Wenn Sie die Standortdatenbank für einen Standort in einer Hierarchie wiederherstellen, unterscheidet sich das Wiederherstellungsverhalten für einen CAS vom Wiederherstellungsverhalten für einen primären Standort. Das Verhalten unterscheidet sich auch, wenn die letzte Sicherung innerhalb oder außerhalb der Beibehaltungsdauer der Änderungsnachverfolgung für SQL Server liegt. Weitere Informationen finden Sie im Abschnitt [Wiederherstellungsszenarios für die Standortdatenbank](#site-database-recovery-scenarios) in diesem Artikel.  

> [!NOTE]  
> Die Wiederherstellung ist nicht möglich, wenn Sie angeben, dass die Standortdatenbank anhand eines Sicherungssatzes wiederhergestellt werden soll, die Standortdatenbank aber bereits vorhanden ist.  

#### <a name="create-a-new-database-for-this-site"></a>Erstellen einer neuen Datenbank für diesen Standort

Verwenden Sie diese Option, wenn Sie nicht über eine Sicherung der Standortdatenbank verfügen. In einer Hierarchie erstellt der Wiederherstellungsprozess eine neue Standortdatenbank. Wenn Sie einen untergeordneten primären Standort wiederherstellen, werden die Daten durch Replikation vom CAS wiederhergestellt. Wenn Sie den CAS wiederherstellen, werden Daten von einem primären Referenzstandort repliziert. Diese Option ist beim Wiederherstellen eines eigenständigen primären Standorts oder eines CAS, der keine primären Standorte hat, nicht verfügbar.  

#### <a name="use-a-site-database-that-has-been-manually-recovered"></a>Verwenden einer manuell wiederhergestellten Standortdatenbank

Verwenden Sie diese Option, wenn Sie die Configuration Manager-Standortdatenbank bereits wiederhergestellt haben, den Wiederherstellungsprozess aber noch abschließen müssen.  

- Configuration Manager kann die Standortdatenbank aus einem der folgenden Prozesse wiederherstellen:  

  - Dem Configuration Manager-Sicherungswartungstask  
  - Einer Standortdatenbanksicherung unter Verwendung von Data Protection Manager (DPM)  
  - Einem anderen Sicherungsprozess  

    Nachdem Sie die Standortdatenbank mithilfe einer Methode außerhalb von Configuration Manager wiederhergestellt haben, führen Sie Setup aus und wählen Sie diese Option aus, um die Wiederherstellung der Standortdatenbank abzuschließen.  

    > [!NOTE]  
    > Wenn Sie DPM verwenden, um die Standortdatenbank zu sichern, dann verwenden Sie DPM-Prozeduren, um die Standortdatenbank an einem angegebenen Ort wiederherzustellen, bevor Sie den Wiederherstellungsprozess in Configuration Manager fortsetzen. Weitere Informationen zu DPM finden Sie in der Dokumentationsbibliothek zu [Data Protection Manager](/system-center/dpm).  

- Wenn Sie in einer Hierarchie die Datenbank eines primären Standorts wiederherstellen, ruft der Wiederherstellungsprozess vom CAS etwaige Änderungen ab, die nach der letzten Sicherung an der Standortdatenbank vorgenommen wurden. Wenn Sie den CAS wiederherstellen, ruft der Wiederherstellungsprozess diese Änderungen von einem primären Referenzstandort ab. Wenn Sie die Standortdatenbank für einen eigenständigen primären Standort wiederherstellen, gehen die Standortänderungen seit der letzten Sicherung verloren.  

#### <a name="skip-database-recovery"></a>Überspringen der Datenbankwiederherstellung

Verwenden Sie diese Option, wenn es auf dem Configuration Manager-Standortdatenbankserver keine Datenverluste gab. Diese Option gilt nur, wenn sich die Standortdatenbank auf einem anderen Computer als der Standortserver befindet, den Sie wiederherstellen.  

### <a name="sql-server-change-tracking-retention-period"></a>Beibehaltungsdauer der Änderungsnachverfolgung für SQL Server

Configuration Manager ermöglicht die Änderungsnachverfolgung für die Standortdatenbank in SQL Server. Bei der Änderungsnachverfolgung können von Configuration Manager Informationen über die Änderungen abgefragt werden, die seit einem früheren Zeitpunkt an den Datenbanktabellen vorgenommen wurden. Mit der Beibehaltungsdauer wird angegeben, wie lange Informationen zur Änderungsnachverfolgung beibehalten werden. Für die Standortdatenbank ist standardmäßig eine Beibehaltungsdauer von fünf Tagen konfiguriert. Beim Wiederherstellen einer Standortdatenbank richtet sich der Wiederherstellungsprozess danach, ob die Sicherung innerhalb oder außerhalb der Beibehaltungsdauer liegt. Wenn beispielsweise Ihr Server von SQL Server ausfällt und die letzte Sicherung vor sieben Tagen erstellt wurde, liegt die Sicherung außerhalb der Beibehaltungsdauer.

Weitere Informationen zur SQL Server-Änderungsnachverfolgung finden Sie in den folgenden Blogbeiträgen des SQL Server-Teams: [Change Tracking Cleanup – part 1 (Cleanup für die Änderungsnachverfolgung – Teil 1)](/archive/blogs/sql_server_team/change-tracking-cleanup-part-1) und [Change Tracking Cleanup – part 2 (Cleanup für die Änderungsnachverfolgung – Teil 2)](/archive/blogs/sql_server_team/change-tracking-cleanup-part-2).

### <a name="reinitialization-of-site-or-global-data"></a>Erneute Initialisierung von Standortdaten oder globalen Daten

Beim erneuten Initialisieren der Standortdaten oder der globalen Daten werden in der Standortdatenbank vorhandene Daten durch Daten aus einer anderen Standortdatenbank ersetzt. Wenn beispielsweise an Standort ABC Daten von Standort XYZ erneut initialisiert werden, werden die folgenden Schritte ausgeführt:

- Die Daten werden von Standort XYZ zu Standort ABC kopiert.
- Die für Standort XYZ vorhandenen Daten werden aus der Standortdatenbank an Standort ABC entfernt.
- Die von Standort XYZ kopierten Daten werden in die Standortdatenbank an Standort ABC eingefügt.

#### <a name="example-scenario-1-the-primary-site-reinitializes-the-global-data-from-the-cas"></a>Beispielszenario 1: Die globalen Daten vom CAS werden am primären Standort erneut initialisiert.

Bei der Wiederherstellung werden die vorhandenen globalen Daten für den primären Standort aus der Datenbank des primären Standorts entfernt und durch die am CAS kopierten globalen Daten ersetzt.

#### <a name="example-scenario-2-the-cas-reinitializes-the-site-data-from-a-primary-site"></a>Beispielszenario 2: Die Standortdaten von einem primären Standort werden am CAS erneut initialisiert.

Bei der Wiederherstellung werden die vorhandenen Standortdaten für diesen primären Standort aus der Datenbank des CAS entfernt. Die Daten werden durch die vom primären Standort kopierten Standortdaten ersetzt. Die Standortdaten für andere primäre Standorte bleiben unverändert.

### <a name="site-database-recovery-scenarios"></a>Wiederherstellungsszenarien für die Standortdatenbank

Nach der Wiederherstellung einer Standortdatenbank anhand einer Sicherung versucht Configuration Manager, die seit der letzten Datenbanksicherung an den Standortdaten und den globalen Daten vorgenommenen Änderungen wiederherzustellen. Configuration Manager startet die folgenden Aktionen, nachdem eine Standortdatenbank anhand einer Sicherung wiederhergestellt wurde:  

#### <a name="recovered-site-is-a-cas"></a>Wiederhergestellter Standort ist ein CAS

- Datenbanksicherung innerhalb der Beibehaltungsdauer der Änderungsnachverfolgung  

  - **Globale Daten:** Die Änderungen in globalen Daten nach der Sicherung werden von allen primären Standorten repliziert.  

  - **Standortdaten:** Die Änderungen in Standortdaten nach der Sicherung werden von allen primären Standorten repliziert.  

- Datenbanksicherung, die älter ist als die Beibehaltungsdauer der Änderungsnachverfolgung  

  - **Globale Daten:** Am CAS werden die globalen Daten vom primären Referenzstandort, sofern angegeben, neu initialisiert. Anschließend werden die globalen Daten vom CAS auf allen anderen primären Standorten neu initialisiert. Wenn Sie keinen Referenzstandort angeben, werden alle primären Standorte mithilfe der globalen Daten vom CAS neu initialisiert. Bei diesen Daten handelt es sich um die von Ihnen aus der Sicherung wiederhergestellten Daten.  

  - **Standortdaten:** Die Standortdaten von jedem primären Standort werden am CAS erneut initialisiert.  

#### <a name="recovered-site-is-a-primary-site"></a>Wiederhergestellter Standort ist ein primärer Standort

- Datenbanksicherung innerhalb der Beibehaltungsdauer der Änderungsnachverfolgung  

  - **Globale Daten:** Die Änderungen in globalen Daten nach der Sicherung werden vom CAS repliziert.  

  - **Standortdaten:** Die Standortdaten von einem primären Standort werden am CAS erneut initialisiert. Änderungen nach der Sicherung gehen verloren. Clients generieren die meisten Daten, wenn sie Informationen an den primären Standort senden.  

- Datenbanksicherung, die älter ist als die Beibehaltungsdauer der Änderungsnachverfolgung  

  - **Globale Daten:** Die globalen Daten vom CAS werden am primären Standort erneut initialisiert.  

  - **Standortdaten:** Die Standortdaten von einem primären Standort werden am CAS erneut initialisiert. Änderungen nach der Sicherung gehen verloren. Clients generieren die meisten Daten, wenn sie Informationen an den primären Standort senden.  

## <a name="site-recovery-procedures"></a>Verfahren zur Standortwiederherstellung

Wenden Sie eines der folgenden Verfahren an, um Ihren Standortserver und Ihre Standortdatenbank wiederherzustellen:

### <a name="start-a-site-recovery-in-the-setup-wizard"></a>Starten einer Sitewiederherstellung im Setup-Assistenten

1. Kopieren Sie den Ordner [CD.Latest](the-cd.latest-folder.md) an einen Speicherort außerhalb des Configuration Manager-Installationsordners. Führen Sie aus der Kopie des Ordners „CD.Latest“ den Configuration Manager-Setup-Assistenten aus.  

2. Wählen Sie auf der Seite **Erste Schritte** die Option **Standort wiederherstellen** aus, und wählen Sie dann **Weiter** aus.  

3. Wählen Sie die Optionen aus, die für die Standortwiederherstellung geeignet sind, und schließen Sie den Assistenten ab.  

     - Während der Wiederherstellung wird der Port von SQL Server Service Broker (SSB), der von SQL Server verwendet wird, vom Setup identifiziert. Ändern Sie die Einstellung für diesen Port während der Wiederherstellung nicht, da andernfalls die Datenreplikation nach Abschluss der Wiederherstellung nicht ordnungsgemäß ausgeführt werden kann.  

     - Sie können den ursprünglichen oder einen neuen Pfad für die Configuration Manager-Installation im Setup-Assistenten angeben.  

### <a name="start-an-unattended-site-recovery"></a>Starten einer unbeaufsichtigten Sitewiederherstellung

1. Bereiten Sie das Skript für eine unbeaufsichtigte Installation mit den für die Standortwiederherstellung erforderlichen Optionen vor. Weitere Informationen finden Sie unter [Unattended site recovery (Unbeaufsichtigte Sitewiederherstellung)](unattended-recovery.md).  

2. Führen Sie das Configuration Manager-Setup mit der Befehlszeilenoption `/script` aus. Erstellen Sie beispielsweise eine Setup-Initialisierungsdatei **ConfigMgrUnattend.ini**. Speichern Sie die Datei im Verzeichnis `C:\Temp` des Computers, auf dem Sie das Setup ausführen. Verwenden Sie den folgenden Befehl:  

    `setup.exe /script C:\temp\ConfigMgrUnattend.ini`  

> [!NOTE]  
> Nach dem Wiederherstellen eines CAS kann es bei der Replikation bestimmter Standortdaten von untergeordneten Standorten zu Fehlern kommen. Diese Daten können Hardwareinventur, Softwareinventur und Statusmeldungen umfassen.
>
> Wenn dieses Problem auftritt, müssen Sie **ConfigMgrDRSSiteQueue** für die Datenbankreplikation erneut initialisieren. Verwenden Sie **SQL Server Manager** zum Ausführen der folgenden Abfrage über die Standortdatenbank am CAS:
>
> ``` SQL
> IF EXISTS (SELECT * FROM sys.service_queues WHERE name = 'ConfigMgrDRSSiteQueue' AND is_receive_enabled = 0)  
>  
> ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON
> ```

## <a name="post-recovery-tasks"></a>Aufgaben nach der Wiederherstellung

Nach der Wiederherstellung Ihres Standorts müssen Sie ggf. einige zusätzliche Tasks ausführen, bevor die Sitewiederherstellung abgeschlossen ist. In den folgenden Abschnitten erfahren Sie, wie Sie Ihre Standortwiederherstellung abschließen.

### <a name="reenter-user-account-passwords"></a>Erneutes Eingeben der Kennwörter von Benutzerkonten

Geben Sie nach der Wiederherstellung eines Standortservers die Kennwörter für alle Benutzerkonten am Standort erneut ein. Diese Kennwörter werden während der Sitewiederherstellung zurückgesetzt. Die Konten werden nach Abschluss der Sitewiederherstellung im Setup-Assistenten auf der Seite **Fertig gestellt** aufgelistet. Die Liste wird auch unter `C:\ConfigMgrPostRecoveryActions.html` auf dem wiederhergestellten Standortserver gespeichert.

#### <a name="reenter-user-account-passwords-after-site-recovery"></a>Erneutes Eingeben von Kennwörtern für Benutzerkonten nach der Sitewiederherstellung

1. Öffnen Sie die Configuration Manager-Konsole, und stellen Sie eine Verbindung mit dem wiederhergestellten Standort her.  

2. Erweitern Sie im Arbeitsbereich **Verwaltung** den Eintrag **Sicherheit**, und wählen Sie dann **Konten** aus.  

3. Geben Sie für jedes Konto das Kennwort wie folgt erneut ein:  

     1. Wählen Sie das Konto aus der nach der Sitewiederherstellung identifizierten Liste aus.  

     2. Wählen Sie im Menüband **Eigenschaften** aus.  

     3. Wählen Sie auf der Registerkarte **Allgemein** die Option **Festlegen** aus, und geben Sie dann das Kennwort für das Konto erneut ein.  

     4. Wählen Sie **Überprüfen** aus, wählen Sie die entsprechende Datenquelle für das ausgewählte Benutzerkonto aus, und wählen Sie dann **Testverbindung** aus. Mit diesem Schritt wird geprüft, ob eine Verbindung des Benutzerkontos mit der Datenquelle möglich ist. Ferner werden die Anmeldeinformationen überprüft.  

     5. Wählen Sie **OK** aus, um das geänderte Kennwort zu speichern, und dann **OK**, um die Eigenschaftenseite für das Konto zu schließen.  

#### <a name="reenter-pxe-passwords"></a>Erneutes Eingeben von PXE-Kennwörtern

<!-- SCCMDocs#1683 -->

1. Gehen Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, und wählen Sie dann den Knoten **Verteilungspunkte** aus. Jeder lokale Verteilungspunkt, dessen **PXE**-Spalte **Ja** enthält, ist für PXE aktiviert und kann ein Kennwort für die erneute Eingabe haben.

1. Wählen Sie einen PXE-fähigen Verteilungspunkt und dann **Eigenschaften** im Menüband aus.

1. Wechseln Sie zur **PXE**-Registerkarte.

1. Wenn die Option **Kennwort erforderlich, wenn PXE von Computern verwendet wird** aktiviert ist, geben Sie das Kennwort ein, und bestätigen Sie es.

1. Wählen Sie **OK** aus, um zu speichern und die Eigenschaften zu schließen.

Wiederholen Sie diesen Vorgang für jeden anderen PXE-fähigen lokalen Verteilungspunkt.

#### <a name="reenter-task-sequence-passwords"></a>Erneutes Eingeben von Tasksequenzkennwörtern

<!-- SCCMDocs#1683 -->

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und wählen Sie anschließend den Knoten **Tasksequenzen** aus.

1. Wählen Sie eine Tasksequenz aus, und wählen Sie dann im Menüband **Bearbeiten** aus.

1. Beachten Sie die folgenden Schritte für Kennwörter für die erneute Eingabe:

    - **Windows-Einstellungen anwenden**: Wenn Sie das lokale Administratorkennwort aktivieren und angeben, geben Sie das Kennwort erneut ein, und bestätigen Sie es.

    - **Netzwerkeinstellungen anwenden**: Wählen Sie für das Konto, das zum Beitreten zur Domäne berechtigt ist, **Festlegen** aus. Geben Sie das Kennwort ein, bestätigen Sie es, und wählen Sie dann **Überprüfen** aus.

    - **Betriebssystemabbild erfassen**: Wählen Sie für das Konto und den Zugriff auf das Ziel **Festlegen** aus. Geben Sie das Kennwort ein, bestätigen Sie es, und wählen Sie dann **Überprüfen** aus.

    - **Verbindung mit Netzwerkordner herstellen**: Wählen Sie für das Konto, das zum Herstellen einer Verbindung mit einem Netzwerkordner verwendet wird, **Festlegen** aus. Geben Sie das Kennwort ein, bestätigen Sie es, und wählen Sie dann **Überprüfen** aus.

    - **BitLocker aktivieren**: Wenn Sie die Schlüsselverwaltungsoption **TPM und PIN** verwenden, geben Sie die PIN erneut ein.

    - **Einer Domäne oder Arbeitsgruppe beitreten**: Wählen Sie für das Konto, das zum Beitreten zur Domäne berechtigt ist, **Festlegen** aus. Geben Sie das Kennwort ein, bestätigen Sie es, und wählen Sie dann **Überprüfen** aus.

    - **Befehlszeile ausführen**: Wenn Sie die Option **Diesen Schritt unter folgendem Konto ausführen** verwenden, wählen Sie **Festlegen** aus. Geben Sie das Kennwort ein, bestätigen Sie es, und wählen Sie dann **Überprüfen** aus.

    - **PowerShell-Skript ausführen**: Wenn Sie die Option **Diesen Schritt unter folgendem Konto ausführen** verwenden, wählen Sie **Festlegen** aus. Geben Sie das Kennwort ein, bestätigen Sie es, und wählen Sie dann **Überprüfen** aus.

Wiederholen Sie diesen Vorgang für alle Tasksequenzen.

### <a name="recreate-bootable-media-and-prestaged-media-in-non-pki-environments"></a>Neuerstellen von startbaren Medien und vorab bereitgestellten Medien in Nicht-PKI-Umgebungen

In Nicht-PKI-Umgebungen basieren selbstsignierte Zertifikate in startbaren und vorab bereitgestellten Medien auf den Computerschlüsseln des Servers, auf dem die Medien erstellt wurden. Aus diesem Grund müssen alle auf diesem Server erstellten startbaren und vorab bereitgestellten Medien neu erstellt werden, wenn im Rahmen einer Wiederherstellung die Hardware des Servers geändert oder das Betriebssystem neu installiert wird. Weitere Informationen zum Erstellen von startbaren und vorab bereitgestellten Medien finden Sie unter [Erstellen von startbaren Medien](../../../osd/deploy-use/create-bootable-media.md) und [Erstellen von vorab bereitgestellten Medien](../../../osd/deploy-use/create-prestaged-media.md).

### <a name="reenter-sideloading-keys"></a>Erneutes Eingeben von Sideload-Schlüsseln

Geben Sie nach der Wiederherstellung eines Standortservers Windows-Sideload-Schlüssel für den Standort an. Diese Schlüssel werden bei der Sitewiederherstellung zurückgesetzt. Nach dem erneuten Eingeben der Sideload-Schlüssel setzt der Standort den Zähler in der Spalte **Verwendete Aktivierungen** für Windows-Sideload-Schlüssel zurück.

Angenommen, die Zahl der **Aktivierungen insgesamt** betrug vor dem Standortausfall **100**. Die Anzahl der Schlüssel, die Geräte verwendet haben, bzw. der Wert unter **Verwendete Aktivierungen** beträgt **90**. Nach der Sitewiederherstellung beträgt der Wert von **Aktivierungen insgesamt** weiterhin **100**, aber in der Spalte **Verwendete Aktivierungen** wird fälschlicherweise **0** angezeigt. Wenn nun jedoch Sideload-Schlüssel von zehn weiteren Geräten verwendet werden, sind anschließend keine Sideload-Schlüssel mehr übrig, und für das elfte Gerät kann kein Sideload-Schlüssel mehr angewendet werden.

### <a name="recreate-azure-services"></a>Erneutes Erstellen von Azure-Diensten

<!-- SCCMDocs#1022 -->

In Configuration Manager-Version 1806 wird in der Datei „cloudmgr.log“ nach der Sitewiederherstellung folgende Fehlermeldung angezeigt:

`Index (zero-based) must be greater than or equal to zero`

Um dieses Problem zu beheben, [erneuern Sie den geheimen Schlüssel](../deploy/configure/azure-services-wizard.md#bkmk_renew) für jede Azure-Mandantenverbindung.

### <a name="configure-ssl-for-site-system-roles-that-use-iis"></a>Konfigurieren von SSL für Standortsystemrollen, die IIS verwenden

Wenn Sie Standortsysteme wiederherstellen, auf denen IIS ausgeführt werden und die für HTTPS konfiguriert sind, müssen Sie IIS für die Verwendung des Webserverzertifikats neu konfigurieren.

### <a name="reinstall-hotfixes"></a>Erneutes Installieren von Hotfixes

Nach der Wiederherstellung eines Standorts müssen Sie alle [Out-of-Band-Hotfixes](updates.md#bkmk_outofband) neu installieren, die auf den Standortserver angewendet worden waren. Zeigen Sie nach Abschluss der Sitewiederherstellung die Liste der zuvor installierten Hotfixes im Setup-Assistenten auf der Seite **Fertig gestellt** an. Diese Liste wird auch unter `C:\ConfigMgrPostRecoveryActions.html` auf dem wiederhergestellten Standortserver gespeichert.

### <a name="recover-custom-reports"></a>Wiederherstellen benutzerdefinierter Berichte

Einige Kunden erstellen benutzerdefinierter Berichte in SQL Server Reporting Services. Wenn bei dieser Komponente ein Fehler auftritt, stellen Sie die Berichte aus einer Sicherung des Berichtsservers wieder her. Weitere Informationen zum Wiederherstellen Ihrer benutzerdefinierten Berichte in Reporting Services finden Sie unter [Sicherungs- und Wiederherstellungsvorgänge für Reporting Services](/sql/reporting-services/install-windows/backup-and-restore-operations-for-reporting-services).

### <a name="recover-content-files"></a>Wiederherstellen von Inhaltsdateien

Die Standortdatenbank verfolgt, wo der Standortserver die Inhaltsdateien speichert. Die Inhaltsdateien selbst werden im Rahmen der Sicherung bzw. Wiederherstellung nicht gesichert oder wiederhergestellt. Zum vollständigen Wiederherstellen von Inhaltsdateien stellen Sie die Inhaltsbibliothek und die Paketquelldateien am Originalspeicherort wieder her. Es gibt verschiedene Methoden für das Wiederherstellen Ihrer Inhaltsdateien. Die einfachste Methode besteht darin, die Dateien aus einer Dateisystemsicherung des Standortservers wiederherzustellen.

Wenn Sie nicht über eine Sicherung des Dateisystems für die Paketquelldateien verfügen, kopieren Sie die Dateien manuell bzw. laden Sie sie manuell herunter. Dieser Prozess ähnelt dem Prozessen, mit dem Sie das Paket ursprünglich erstellt haben. Führen Sie die folgende Abfrage in SQL Server aus, um den Quellspeicherort für alle Pakete und Anwendungen zu ermitteln: `SELECT * FROM v_Package`. Identifizieren Sie den Paketquellstandort anhand der ersten drei Zeichen der Paket-ID. Wenn beispielsweise die Paket-ID „CEN00001“ lautet, ist „CEN“ der Standortcode für den Quellstandort. Paketquelldateien müssen an den gleichen Speicherort wiederhergestellt werden wie vor dem Fehler.

Wenn eine Sicherung des Dateisystems mit der Inhaltsbibliothek nicht verfügbar ist, gibt es folgende Möglichkeiten zur Wiederherstellung:  

- **Importieren einer vorab bereitgestellten Inhaltsdatei:** In einer Configuration Manager-Hierarchie können Sie eine vorab bereitgestellte Inhaltsdatei mit allen Paketen und Anwendungen von einem anderen Speicherort erstellen. Importieren Sie dann die vorab bereitgestellte Inhaltsdatei, um die Inhaltsbibliothek auf dem Standortserver wiederherzustellen.  

- **Aktualisieren von Inhalten:** Configuration Manager kopiert den Inhalt aus der Paketquelle in die Inhaltsbibliothek. Die Paketquelldateien müssen am ursprünglichen Speicherort verfügbar sein, damit diese Aktion erfolgreich ausgeführt werden kann. Führen Sie diese Aktion für jedes Paket und jede Anwendung aus.

### <a name="recover-custom-software-updates"></a>Wiederherstellen benutzerdefinierter Softwareupdates

Wenn Sie System Center Updates Publisher-Datenbankdateien in Ihren Sicherungsplan einbezogen haben, können Sie die Datenbanken wiederherstellen, falls auf dem Computer, auf dem Updates Publisher ausgeführt wird, ein Fehler auftritt. Weitere Informationen zu Updates Publisher finden Sie unter [System Center Updates Publisher](../../../sum/tools/updates-publisher.md).

#### <a name="restore-the-updates-publisher-database"></a>Wiederherstellen der Updates Publisher-Datenbank

1. Installieren Sie Updates Publisher auf dem wiederhergestellten Computer neu.  

2. Kopieren Sie die Datenbankdatei **Scupdb.sdf** von Ihrem Sicherungsziel nach `%USERPROFILE%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\` auf dem Computer, auf dem Updates Publisher ausgeführt wird.  

3. Wenn Updates Publisher auf dem Computer mehrerer Benutzer ausgeführt wird, kopieren Sie jede Datenbankdatei in den Speicherort für das entsprechende Benutzerprofil.  

### <a name="user-state-migration-data"></a>Daten zur Benutzerzustandsmigration

Geben Sie in den Eigenschaften des Zustandsmigrationspunkts die Ordner an, in denen Benutzerzustandsdaten gespeichert werden. Nachdem Sie einen Zustandsmigrationspunkt wiederhergestellt haben, stellen Sie die Benutzerzustandsdaten manuell auf dem Server wieder her. Verwenden Sie für die Wiederherstellung dieselben Ordner, in denen die Daten vor Auftreten des Fehlers gespeichert waren.

### <a name="regenerate-the-certificates-for-distribution-points"></a>Generieren der Zertifikate für Verteilungspunkte

Nach der Wiederherstellung eines Standorts ist in der Datei **distmgr.log** möglicherweise der folgende Eintrag für einen oder mehrere Verteilungspunkte enthalten: `Failed to decrypt cert PFX data`. Dieser Eintrag gibt an, dass die Zertifikatdaten des Verteilungspunkts nicht vom Standort entschlüsselt werden können. Generieren oder importieren Sie das Zertifikat für die betroffenen Verteilungspunkte erneut, um das Problem zu beheben. Verwenden Sie dazu das PowerShell-Cmdlet [Set-CMDistributionPoint](/powershell/module/configurationmanager/set-cmdistributionpoint).

### <a name="update-certificates-used-for-cloud-based-distribution-points"></a>Aktualisieren von Zertifikaten, die für cloudbasierte Verteilungspunkte verwendet werden

Für Configuration Manager ist ein Azure-Verwaltungszertifikat erforderlich, das für die Kommunikation zwischen Standortserver und cloudbasierten Verteilungspunkten verwendet wird. Aktualisieren Sie nach einer Sitewiederherstellung die Zertifikate für cloudbasierte Verteilungspunkte.

## <a name="recover-a-secondary-site"></a>Wiederherstellen eines sekundären Standorts

Die Sicherung der Datenbank an einem sekundären Standort wird von Configuration Manager nicht unterstützt. Die Wiederherstellung durch Neuinstallation des sekundären Standorts wird hingegen unterstützt. Bei einem Fehler auf einem sekundären Standort von Configuration Manager ist eine Wiederherstellung des sekundären Standorts erforderlich.

### <a name="requirements"></a>Anforderungen

- Der Server muss alle Voraussetzungen für einen sekundären Standort erfüllen, und es müssen die entsprechenden Sicherheitsrechte konfiguriert sein.  

- Verwenden Sie denselben Installationspfad, der für den fehlerhaften Standort verwendet wurde.  

- Verwenden Sie einen Server mit derselben Konfiguration wie der ausgefallene Server. Diese Konfiguration umfasst seinen vollqualifizierten Domänennamen (FQDN).  

- Der Server muss dieselbe SQL Server-Konfiguration wie der ausgefallene Standort aufweisen.  

  - Während der Wiederherstellung eines sekundären Standorts wird SQL Server Express nicht von Configuration Manager installiert, wenn diese Software noch nicht auf dem Computer installiert ist.  

  - Verwenden Sie dieselbe Version und Instanz von SQL Server, die Sie vor Auftreten des Fehlers für die sekundäre Standortdatenbank verwendet haben.  

### <a name="procedure"></a>Vorgehensweise

Verwenden Sie die Aktion **Sekundären Standort wiederherstellen** des Knotens **Standorte** in der Configuration Manager-Konsole. Anders als bei anderen Arten von Standorten wird bei der Wiederherstellung eines sekundären Standorts keine Sicherungsdatei verwendet. Bei diesem Prozess werden die Dateien des sekundären Standorts wieder auf dem ausgefallenen Server installiert. Nach der Neuinstallation des Standorts werden die Daten des sekundären Standorts vom übergeordneten primären Standort neu initialisiert.

Während des Wiederherstellungsprozesses prüft Configuration Manager, ob die Inhaltsbibliothek auf dem Server des sekundären Standorts vorhanden ist. Ferner prüft Configuration Manager, ob der entsprechende Inhalt verfügbar ist. Der sekundäre Standort verwendet die vorhandene Inhaltsbibliothek, sofern sie den entsprechenden Inhalt enthält. Andernfalls müssen Sie für die Wiederherstellung der Inhaltsbibliothek am sekundären Standort den Inhalt erneut auf dem Server verteilen oder vorab bereitstellen.

Bei einem Verteilungspunkt, der sich nicht auf dem sekundären Standortserver befindet, müssen Sie während der Wiederherstellung des sekundären Standorts den Verteilungspunkt nicht neu installieren. Nach der Wiederherstellung des sekundären Standorts wird der Standort automatisch mit dem Verteilungspunkt synchronisiert.

Sie können den Status der Wiederherstellung des sekundären Standorts überprüfen, indem Sie in der Configuration Manager-Konsole die Aktion **Installationsstatus anzeigen** unter dem Knoten **Standorte** verwenden.