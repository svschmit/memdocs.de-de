---
title: Verwaltungspunkt-Datenbankreplikate
titleSuffix: Configuration Manager
description: Verwenden Sie ein Datenbankreplikat zum Verringern der CPU-Last des Standortdatenbankservers mithilfe von Verwaltungspunkten.
ms.date: 05/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b06f781b-ab25-4d9a-b128-02cbd7cbcffe
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: db1e0d78263d264c66eed7258db800397baad735
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607576"
---
# <a name="database-replicas-for-management-points-for-configuration-manager"></a>Datenbankreplikate für Verwaltungspunkte für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Configuration Manager-Standorte können ein Datenbankreplikat zum Verringern der CPU-Last des Standortdatenbankservers mithilfe von Verwaltungspunkten verwenden, die Anforderungen von Clients erfüllen.  

-   Bei der Verwendung eines Datenbankreplikats durch einen Verwaltungspunkt werden Daten anstatt vom Standortdatenbankserver vom SQL Server-Computer angefordert, auf dem das Datenbankreplikat gehostet wird.  

-   Dies hilft dabei, die CPU-Verarbeitungsanforderungen des Standortdatenbankservers zu reduzieren, indem häufige clientbezogene Verarbeitungsaufgaben ausgelagert werden.  Ein Beispiel einer häufigen Verarbeitungsaufgabe für Clients sind Standorte, an denen sehr viele Clients eine Clientrichtlinie häufig anfordern.  


##  <a name="prepare-to-use-database-replicas"></a><a name="bkmk_Prepare"></a> Vorbereiten der Verwendung von Datenbankreplikaten  
**Informationen zu Datenbankreplikaten für Verwaltungspunkte:**  

-   Replikate sind eine Teilkopie der Standortdatenbank, die in eine separate SQL Server-Instanz repliziert wird:  

    -   Primäre Standorte unterstützen ein dediziertes Datenbankreplikat für jeden Verwaltungspunkt am Standort (sekundäre Standorte unterstützen keine Datenbankreplikate).  

    -   Ein einzelnes Datenbankreplikat kann von mehreren Verwaltungspunkten am selben Standort verwendet werden.  

    -   Eine SQL Server-Instanz kann mehrere Datenbankreplikate für die Verwendung durch andere Verwaltungspunkte hosten, solange jedes in einer separaten Instanz von SQL Server ausgeführt wird.  

-   Replikate dienen zum Synchronisieren einer Kopie der Standortdatenbank gemäß einem festen Zeitplan mithilfe von Daten, die von Standortdatenbankservern für diesen Zweck veröffentlicht werden.  

-   Verwaltungspunkte können zur Verwendung eines Replikats konfiguriert werden, und zwar, entweder bei ihrer Installation oder später, indem der bereits installierte Verwaltungspunkt zur Verwendung des Datenbankreplikats neu konfiguriert wird.  

-   Überwachen Sie den Standortdatenbankserver und alle Datenbankreplikatserver regelmäßig, um sicherzustellen, dass die Replikation zwischen dem Standortdatenbankserver und jedem Datenbankreplikatserver ordnungsgemäß erfolgt und die Leistung der Datenbankreplikatserver für den Standort und die erforderliche Clientleistung ausreicht.  

**Voraussetzungen für Datenbankreplikate:**  

-   **SQL Server-Anforderungen:**  

    -   Der Computer mit SQL Server, der das Datenbankreplikat hostet, muss die gleichen Anforderungen wie der Standortdatenbankserver erfüllen. Allerdings muss auf dem Replikatserver nicht dieselbe Version oder Edition von SQL Server wie auf dem Standortdatenbankserver ausgeführt werden, solange die ausgeführte SQL Server-Version oder -Edition unterstützt wird. Weitere Informationen finden Sie unter [Unterstützte SQL Server-Versionen für Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md).  

    -   Der SQL Server-Dienst auf dem Computer, auf dem die Replikatdatenbank gehostet wird, muss mit dem Konto **System** ausgeführt werden.  

    -   Sowohl auf dem SQL Server-Computer, auf dem die Standortdatenbank gehostet wird, als auch auf dem SQL Server-Computer, auf dem ein Datenbankreplikat gehostet wird, muss die **SQL Server-Replikation** installiert sein.  

    -   Die Standortdatenbank muss das Datenbankreplikat **veröffentlichen** , und jeder Remoteserver mit einem Datenbankreplikat muss die veröffentlichten Daten **abonnieren** .  

    -   Der SQL Server-Computer, auf dem die Standortdatenbank gehostet wird, und der SQL Server-Computer, auf dem ein Datenbankreplikat gehostet wird, müssen zur Unterstützung einer **maximalen Textgröße für Replikation** von 2 GB konfiguriert werden. Ein Beispiel dafür, wie Sie dies für SQL Server 2012 konfigurieren, finden Sie unter [Konfigurieren der Serverkonfigurationsoption Max. Textgröße für Replikation](/sql/database-engine/configure-windows/configure-the-max-text-repl-size-server-configuration-option).  

-   **Selbstsigniertes Zertifikat:** Zum Konfigurieren eines Datenbankreplikats müssen Sie auf dem Datenbankreplikatserver ein selbstsigniertes Zertifikat erstellen und jedem Verwaltungspunkt, von dem dieser Datenbankreplikatserver verwendet werden soll, verfügbar machen.  

    -   Das Zertifikat ist für einen Verwaltungspunkt, der auf dem Datenbankreplikatserver installiert ist, automatisch verfügbar.  

    -   Sie müssen das Zertifikat exportieren und dann dem Zertifikatspeicher **Vertrauenswürdige Personen** des betreffenden Remoteverwaltungspunkts hinzufügen, um es auch Remoteverwaltungspunkten verfügbar zu machen.  

-   **Clientbenachrichtigung:** Sie müssen die Kommunikation zwischen dem Standortdatenbankserver und dem Datenbankreplikatserver für **SQL Server Service Broker** konfigurieren, um die Clientbenachrichtigung mit einem Datenbankreplikat für einen Verwaltungspunkt zu unterstützen. Dazu müssen Sie diese Schritte ausführen:  

    -   Konfigurieren jeder Datenbank mit Informationen über die andere Datenbank  

    -   Austauschen von Zertifikaten zwischen den beiden Datenbanken für eine sichere Kommunikation  

**Einschränkungen beim Verwenden von Datenbankreplikaten:**  

-   Wenn Ihr Standort für das Veröffentlichen von Datenbankreplikaten konfiguriert ist, müssen die folgenden Anweisungen anstelle der normalen Vorgehensweise befolgt werden:  

    -   [Deinstallieren eines Standortservers, der ein Datenbankreplikat veröffentlicht](#BKMK_DBReplicaOps_Uninstall)  

    -   [Verschieben eines Standortservers, der ein Datenbankreplikat veröffentlicht](#BKMK_DBReplicaOps_Move)  

-   **Upgrades auf Configuration Manager (Current Branch)** : Bevor Sie entweder ein Upgrade eines Standorts von System Center 2012 Configuration Manager auf Configuration Manager (Current Branch) ausführen oder Configuration Manager (Current Branch) auf das neueste Release aktualisieren, müssen Sie Datenbankreplikate für Verwaltungspunkte deaktivieren.  Nach dem Upgrade des Standorts können Sie die Datenbankreplikate für Verwaltungspunkte neu konfigurieren.  

-   **Mehrere Replikate auf einer einzelnen SQL Server-Instanz:**  Wenn Sie einen Datenbankreplikatserver zum Hosten mehrerer Datenbankreplikate für Verwaltungspunkte konfigurieren (wobei sich jedes Replikat in einer eigenen Instanz befinden muss), müssen Sie (in Schritt 4 des folgenden Abschnitts) ein geändertes Konfigurationsskript verwenden. Dies verhindert das Überschreiben des selbstsignierten Zertifikats, das von zuvor konfigurierten Datenbankreplikaten auf diesem Server verwendet wird.  

- Benutzerbereitstellungen im Software Center funktionieren nicht mit einem Verwaltungspunkt, der ein SQL-Replikat verwendet. <!--sccmdocs-1011-->

##  <a name="configure-database-replicas"></a><a name="BKMK_DBReplica_Config"></a> Konfigurieren von Datenbankreplikaten  
Zum Konfigurieren eines Datenbankreplikats müssen die folgenden Schritte ausgeführt werden:  

-   [Schritt 1: Konfigurieren des Standortdatenbankservers für die Veröffentlichung des Datenbankreplikats](#BKMK_DBReplica_ConfigSiteDB)  

-   [Schritt 2: Konfigurieren des Datenbankreplikatservers](#BKMK_DBReplica_ConfigSrv)  

-   [Schritt 3: Konfigurieren von Verwaltungspunkten für die Verwendung des Datenbankreplikats](#BKMK_DBReplica_ConfigMP)  

-   [Schritt 4: Konfigurieren eines selbstsignierten Zertifikats für den Datenbankreplikatserver](#BKMK_DBReplica_Cert)  

-   [Schritt 5: Konfigurieren des SQL Server Service Broker für den Datenbankreplikatserver](#BKMK_DBreplica_SSB)  

###  <a name="step-1---configure-the-site-database-server-to-publish-the-database-replica"></a><a name="BKMK_DBReplica_ConfigSiteDB"></a> Schritt 1: Konfigurieren des Standortdatenbankservers für die Veröffentlichung des Datenbankreplikats  
 Verwenden Sie das folgende Verfahren als Beispiel für die Konfiguration des Standortdatenbankservers auf einem Windows Server 2008 R2-Computer für die Veröffentlichung des Datenbankreplikats. Wenn Sie eine andere Betriebssystemversion haben, lesen Sie deren Dokumentation und passen die Schritte in diesem Verfahren entsprechend an.  

##### <a name="to-configure-the-site-database-server"></a>So konfigurieren Sie den Standortdatenbankserver  

1.  Legen Sie auf dem Standortdatenbankserver fest, dass der SQL Server-Agent automatisch gestartet wird.  

2.  Erstellen Sie auf dem Standortdatenbankserver eine lokale Benutzergruppe mit dem Namen **ConfigMgr_MPReplicaAccess**. Sie müssen das Computerkonto jedes Datenbankreplikatservers, den Sie an diesem Standort verwenden, dieser Gruppe hinzufügen, um eine Synchronisierung der Datenbankreplikatserver mit dem veröffentlichten Datenbankreplikat zu ermöglichen.  

3.  Konfigurieren Sie auf dem Standortdatenbankserver eine Dateifreigabe mit dem Namen **ConfigMgr_MPReplica**.  

4.  Fügen Sie der **ConfigMgr_MPReplica** -Freigabe die folgenden Berechtigungen hinzu:  

    > [!NOTE]  
    >  Wenn vom SQL Server-Agent nicht das lokale Systemkonto verwendet wird, ersetzen Sie SYSTEM in der folgenden Liste mit dem entsprechenden Kontennamen.  

    -   **Freigabeberechtigungen**:  

        -   SYSTEM: **Schreiben**  

        -   ConfigMgr_MPReplicaAccess: **Lesen**  

    -   **NTFS-Berechtigungen**:  

        -   SYSTEM: **Vollzugriff**  

        -   ConfigMgr_MPReplicaAccess: **Lesen**, **Lesen und Ausführen**, **Ordnerinhalt auflisten**  

5.  Verwenden Sie **SQL Server Management Studio** , um eine Verbindung zur Standortdatenbank herzustellen, und führen Sie die folgende gespeicherte Prozedur als Abfrage aus: **spCreateMPReplicaPublication**  

Nach Abschluss der gespeicherten Prozedur ist der Standortdatenbankserver für die Veröffentlichung des Datenbankreplikats konfiguriert.  

###  <a name="step-2---configuring-the-database-replica-server"></a><a name="BKMK_DBReplica_ConfigSrv"></a> Schritt 2: Konfigurieren des Datenbankreplikatservers  
Der Datenbankreplikatserver ist ein Computer, auf dem SQL Server ausgeführt und ein Replikat der Standortdatenbank zur Verwendung durch die Verwaltungspunkte gehostet wird. Die Datenbankkopie des Datenbankreplikatservers wird nach einem festen Zeitplan mit dem Datenbankreplikat, das auf dem Datenbankserver veröffentlicht ist, synchronisiert.  

Vom Datenbankreplikatserver müssen die gleichen Anforderungen erfüllt werden wie vom Standortdatenbankserver. Allerdings kann vom Datenbankreplikatserver eine Edition oder Version von SQL Server ausgeführt werden, die von der des Standortdatenbankservers abweicht. Weitere Informationen über die unterstützten SQL Server-Versionen finden Sie unter [Unterstützte SQL Server-Versionen für Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md).  

> [!IMPORTANT]  
>  Der SQL Server-Dienst auf dem Computer, auf dem die Replikatsdatenbank gehostet wird, muss als Systemkonto ausgeführt werden.  

Verwenden Sie das folgende Verfahren als Beispiel für die Konfiguration eines Datenbankreplikatservers auf einem Windows Server 2008 R2-Computer. Wenn Sie eine andere Betriebssystemversion haben, lesen Sie deren Dokumentation und passen die Schritte in diesem Verfahren entsprechend an.  

##### <a name="to-configure-the-database-replica-server"></a>So konfigurieren Sie den Datenbankreplikatserver  

1. Legen Sie auf dem Datenbankreplikatserver fest, dass der SQL Server-Agent automatisch gestartet wird.  

2. Verwenden Sie auf dem Datenbankreplikatserver **SQL Server Management Studio** , um eine Verbindung mit dem lokalen Server herzustellen. Suchen Sie den Ordner **Replikation** , klicken Sie auf **Lokale Abonnements** , und wählen Sie **Neue Abonnements**aus, um den Assistenten zum Erstellen neuer Abonnements zu starten.  

   1. Wählen Sie auf der Seite **Veröffentlichung** im Listenfeld **Herausgeber** die Option **SQL Server-Herausgeber suchen**aus, geben Sie den Namen des Standortdatenbankservers ein, und klicken Sie auf **Verbinden**.  

   2. Wählen Sie **ConfigMgr_MPReplica**aus, und klicken Sie dann auf **Weiter**.  

   3. Wählen Sie auf der Seite **Speicherort des Verteilungs-Agents** die Option **Jeden Agent auf seinem Abonnenten ausführen (Pullabonnements)** aus, und klicken Sie dann auf **Weiter**.  

   4. Führen Sie auf der Seite **Abonnenten** einen der folgenden Schritte aus:  

      -   Wählen Sie auf dem Datenbankreplikatserver eine vorhandene Datenbank zur Verwendung für das Datenbankreplikat aus, und klicken Sie dann auf **OK**.  

      -   Wählen Sie die Option **Neue Datenbank** aus, um eine neue Datenbank für das Datenbankreplikat zu erstellen. Geben Sie auf der Seite **Neue Datenbank** einen Datenbanknamen an, und klicken Sie dann auf **OK**.  

   5. Klicken Sie zum Fortfahren auf **Weiter** .  

   6. Klicken Sie auf der Seite **Sicherheit für den Verteilungs-Agent** in der Zeile „Abonnentenverbindung“ des Dialogfelds auf die Schaltfläche für Eigenschaften **(...)** , und konfigurieren Sie anschließend die Sicherheitseinstellungen für die Verbindung.  

      > [!TIP]  
      >  Sie finden die Eigenschaftenschaltfläche **(...)** in der vierten Spalte des Anzeigefelds.  

      **Sicherheitseinstellungen:**  

      - Konfigurieren Sie das Konto, unter dem der Verteilungs-Agent-Prozess ausgeführt wird (das Prozesskonto), folgendermaßen:  

        -   Wenn der SQL Server-Agent als lokales System ausgeführt wird, wählen Sie **Unter dem SQL Server-Agent-Dienstkonto ausführen (dies ist keine empfohlene bewährte Sicherheitsmethode)** aus.  

        -   Wenn der SQL Server-Agent mit einem anderen Konto ausgeführt wird, wählen Sie **Unter dem folgenden Windows-Konto ausführen**, und konfigurieren Sie dann dieses Konto. Sie können ein Windows-Konto oder ein SQL Server-Konto angeben.  

        > [!IMPORTANT]  
        >  Sie müssen dem Konto, unter dem der Verteilungs-Agent ausgeführt wird, Berechtigungen für den Herausgeber als Pullabonnement erteilen. Informationen zum Konfigurieren dieser Berechtigungen finden Sie unter [Sicherheit für den Verteilungs-Agent](/sql/relational-databases/replication/distribution-agent-security).  

      - Wählen Sie unter **Verbindung mit dem Verteiler herstellen**die Option **Identität des Prozesskontos annehmen**aus.  

      - Wählen Sie unter **Verbindung mit dem Abonnenten herstellen**die Option **Identität des Prozesskontos annehmen**aus.  

        Wenn Sie die Verbindungssicherheitseinstellungen konfiguriert haben, klicken Sie auf **OK** , um sie zu speichern, und dann auf **Weiter**.  

   7. Wählen Sie auf der Seite **Synchronisierungszeitplan** im ‎Listenfeld **Agentzeitplan** die Option **Zeitplan festlegen**aus, und konfigurieren Sie unter **Neuer Auftragszeitplan**einen neuen Auftragszeitplan. Legen Sie die Häufigkeit mit **Täglich**, die Wiederholung **5 Minute(n)** und die Dauer mit **Kein Enddatum**fest. Klicken Sie auf **Weiter** , um den Zeitplan zu speichern, und dann noch einmal auf **Weiter** .  

   8. Aktivieren Sie auf der Seite **Aktionen des Assistenten** das Kontrollkästchen für **Abonnement(s) erstellen**, und klicken Sie dann auf **Weiter**.  

   9. Klicken Sie auf der Seite **Assistenten abschließen** auf **Fertig stellen**, und klicken Sie dann auf **Schließen** , um den Assistenten abzuschließen.  

3. Verwenden Sie sofort nach dem Fertigstellen des Assistenten für neue Abonnements **SQL Server Management Studio** , um eine Verbindung mit der Datenbank des Datenbankreplikatservers herzustellen und die folgende Abfrage zur Aktivierung der TRUSTWORTHY-Datenbankeigenschaft auszuführen:  `ALTER DATABASE <MP Replica Database Name> SET TRUSTWORTHY ON;`  

4. Überprüfen Sie anhand des Synchronisierungsstatus, ob das Abonnement erfolgreich erstellt wurde:  

   -   Auf dem Abonnentencomputer:  

       -   Stellen Sie in **SQL Server Management Studio**eine Verbindung mit dem Datenbankreplikatserver her, und erweitern Sie den Bereich **Replikation**.  

       -   Erweitern Sie den Bereich **Lokale Abonnements**, klicken Sie mit der rechten Maustaste auf das Abonnement der Standortdatenbankveröffentlichung, und wählen Sie **Synchronisierungsstatus anzeigen**aus.  

   -   Auf dem Veröffentlichungscomputer:  

       -   Stellen Sie in **SQL Server Management Studio**eine Verbindung mit dem Standortdatenbankcomputer her, klicken Sie mit der rechten Maustaste auf den Ordner **Replikation** , und wählen Sie dann die Option **Replikationsmonitor starten**aus.  

5. Stellen Sie mit **SQL Server Management Studio** eine Verbindung zum Datenbankreplikat auf dem Datenbankreplikatserver her, und führen Sie die folgende gespeicherte Prozedur als Abfrage aus, um die CLR-Integration (Common Language Runtime) für das Datenbankreplikat zu aktivieren: **exec sp_configure 'clr enabled', 1; RECONFIGURE WITH OVERRIDE**  

6. Fügen Sie der lokalen Gruppe **Administratoren** auf dem Datenbankreplikatserver das Computerkonto jedes Verwaltungspunkts, der einen Datenbankreplikatserver verwendet, hinzu.  

   > [!TIP]  
   >  Dieser Schritt ist nicht erforderlich bei Verwaltungspunkten, die auf dem Datenbankreplikatserver ausgeführt werden.  

   Das Datenbankreplikat kann nun von einem Verwaltungspunkt verwendet werden.  

###  <a name="step-3---configure-management-points-to-use-the-database-replica"></a><a name="BKMK_DBReplica_ConfigMP"></a> Schritt 3: Konfigurieren von Verwaltungspunkten für die Verwendung des Datenbankreplikats  
 Beim Installieren der Verwaltungspunktrolle können Sie einen Verwaltungspunkt an einem primären Standort für die Verwendung eines Datenbankreplikats konfigurieren. Sie können auch einen vorhandenen Verwaltungspunkt für die Verwendung eines Datenbankreplikats neu konfigurieren.  

 Verwenden Sie die folgenden Informationen, um einen Verwaltungspunkt für die Verwendung eines Datenbankreplikats zu konfigurieren:  

-   **So konfigurieren Sie einen neuen Verwaltungspunkt** Wählen Sie auf der Seite **Verwaltungspunktdatenbank** des Assistenten zum Installieren des Verwaltungspunkts die Option **Datenbankreplikat verwenden** aus, und geben Sie den FQDN des Computers an, auf dem das Datenbankreplikat gehostet wird. Geben Sie dann bei **Name der ConfigMgr-Standortdatenbank**den Datenbanknamen des Datenbankreplikats auf diesem Computer an.  

-   **So konfigurieren Sie einen zuvor installierten Verwaltungspunkt** Öffnen Sie die Eigenschaftenseite des Verwaltungspunkts, wählen Sie die Registerkarte **Verwaltungspunktdatenbank** und anschließend die Option **Datenbankreplikat verwenden** aus, und geben Sie den FQDN des Computers an, auf dem das Datenbankreplikat gehostet wird. Geben Sie dann bei **Name der ConfigMgr-Standortdatenbank**den Datenbanknamen des Datenbankreplikats auf diesem Computer an.  

-   **Für jeden Verwaltungspunkt, der ein Datenbankreplikat verwendet**, müssen Sie das Computerkonto des Verwaltungspunktservers zur Rolle **db_datareader** für das Datenbankreplikat hinzufügen.  

Zusätzlich zum Konfigurieren des Verwaltungspunkts für die Verwendung des Datenbankreplikatservers müssen Sie die **Windows-Authentifizierung** in **IIS** auf dem Verwaltungspunkt aktivieren:  

1.  Öffnen Sie das Dialogfeld **Internetinformationsdienste-Manager**.  

2.  Wählen Sie die Website aus, die vom Verwaltungspunkt verwendet wird, und öffnen Sie die **Authentifizierung**.  

3.  Legen Sie für die **Windows-Authentifizierung** die Einstellung **Aktiviert**fest, und schließen Sie dann den **Internetinformationsdienste-Manager**.  

###  <a name="step-4--configure-a-self-signed-certificate-for-the-database-replica-server"></a><a name="BKMK_DBReplica_Cert"></a> Schritt 4: Konfigurieren eines selbstsignierten Zertifikats für den Datenbankreplikatserver  
 Sie müssen auf dem Datenbankreplikatserver ein selbstsigniertes Zertifikat erstellen und für jeden Verwaltungspunkt, von dem dieser Datenbankreplikatserver verwendet werden soll, verfügbar machen.  

 Das Zertifikat ist für einen Verwaltungspunkt, der auf dem Datenbankreplikatserver installiert ist, automatisch verfügbar. Sie müssen das Zertifikat jedoch exportieren und dann dem Zertifikatsspeicher Vertrauenswürdige Personen des betreffenden Remoteverwaltungspunkts hinzufügen, um es auch für Remoteverwaltungspunkte verfügbar zu machen.  

 Verwenden Sie die folgenden Verfahren als Beispiele für die Konfiguration des selbstsignierten Zertifikats auf dem Datenbankreplikatserver für einen Windows Server 2008 R2-Computer. Wenn Sie eine andere Betriebssystemversion haben, lesen Sie deren Dokumentation und passen die Schritte in diesen Verfahren entsprechend an.  

##### <a name="to-configure-a-self-signed-certificate-for-the-database-replica-server"></a>So konfigurieren Sie ein selbstsigniertes Zertifikat für den Datenbankreplikatserver  

1.  Öffnen Sie auf dem Datenbankreplikatserver eine PowerShell-Eingabeaufforderung mit Administratorberechtigungen, und führen Sie dann den folgenden Befehl aus: **set-executionpolicy UnRestricted**  

2.  Kopieren Sie das folgende PowerShell-Skript, und speichern Sie es als Datei mit dem Namen **CreateMPReplicaCert.ps1**. Legen Sie eine Kopie dieser Datei im Stammordner der Systempartition des Datenbankreplikatservers ab.  

    > [!IMPORTANT]  
    >  Wenn Sie mehrere Datenbankreplikate auf einer einzelnen SQL Server-Instanz konfigurieren, müssen Sie für jedes nachfolgende Replikat, das Sie konfigurieren, eine geänderte Version dieses Skripts für dieses Verfahren verwenden. Siehe  [Zusätzliches Skript für zusätzliche Datenbankreplikate auf einem einzelnen Computer mit SQL Server](#bkmk_supscript).  

    ``` PowerShell
    # Script for creating a self-signed certificate for the local machine and configuring SQL Server to use it.  

    Param($SQLInstance)  

    $ConfigMgrCertFriendlyName = "ConfigMgr SQL Server Identification Certificate"  

    # Get local computer name  
    $computerName = "$env:computername"  

    # Get the sql server name  
    #$key="HKLM:\SOFTWARE\Microsoft\SMS\MP"  
    #$value="SQL Server Name"  
    #$sqlServerName= (Get-ItemProperty $key).$value  
    #$dbValue="Database Name"  
    #$sqlInstance_DB_Name= (Get-ItemProperty $key).$dbValue  

    $sqlServerName = [System.Net.Dns]::GetHostByName("localhost").HostName   
    $sqlInstanceName = "MSSQLSERVER"  
    $SQLServiceName = "MSSQLSERVER"  

    if ($SQLInstance -ne $Null)  
    {  
        $sqlInstanceName = $SQLInstance  
        $SQLServiceName = "MSSQL$" + $SQLInstance  
    }  

    # Delete existing cert if one exists  
    function Get-Certificate($storename, $storelocation)  
    {   
        $store=new-object System.Security.Cryptography.X509Certificates.X509Store($storename,$storelocation)   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Certificates   
    }   

    $cert = Get-Certificate "My" "LocalMachine" | ?{$_.FriendlyName -eq $ConfigMgrCertFriendlyName}   
    if($cert -is [Object])  
    {  
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Remove($cert)  
        $store.Close()  

        # Remove this cert from Trusted People too...  
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("TrustedPeople","LocalMachine")   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Remove($cert)  
        $store.Close()      
    }  

    # Create the new cert  
    $name = new-object -com "X509Enrollment.CX500DistinguishedName.1"  
    $name.Encode("CN=" + $sqlServerName, 0)  

    $key = new-object -com "X509Enrollment.CX509PrivateKey.1"  
    $key.ProviderName = "Microsoft RSA SChannel Cryptographic Provider"  
    $key.KeySpec = 1  
    $key.Length = 1024  
    $key.SecurityDescriptor = "D:PAI(A;;0xd01f01ff;;;SY)(A;;0xd01f01ff;;;BA)(A;;0x80120089;;;NS)"  
    $key.MachineContext = 1  
    $key.Create()  

    $serverauthoid = new-object -com "X509Enrollment.CObjectId.1"  
    $serverauthoid.InitializeFromValue("1.3.6.1.5.5.7.3.1")  
    $ekuoids = new-object -com "X509Enrollment.CObjectIds.1"  
    $ekuoids.add($serverauthoid)  
    $ekuext = new-object -com "X509Enrollment.CX509ExtensionEnhancedKeyUsage.1"  
    $ekuext.InitializeEncode($ekuoids)  

    $cert = new-object -com "X509Enrollment.CX509CertificateRequestCertificate.1"  
    $cert.InitializeFromPrivateKey(2, $key, "")  
    $cert.Subject = $name  
    $cert.Issuer = $cert.Subject  
    $cert.NotBefore = get-date  
    $cert.NotAfter = $cert.NotBefore.AddDays(3650)  
    $cert.X509Extensions.Add($ekuext)  
    $cert.Encode()  

    $enrollment = new-object -com "X509Enrollment.CX509Enrollment.1"  
    $enrollment.InitializeFromRequest($cert)  
    $enrollment.CertificateFriendlyName = "ConfigMgr SQL Server Identification Certificate"  
    $certdata = $enrollment.CreateRequest(0x1)  
    $enrollment.InstallResponse(0x2, $certdata, 0x1, "")  

    # Add this cert to the trusted peoples store  
    [Byte[]]$bytes = [System.Convert]::FromBase64String($certdata)  

    $trustedPeople = new-object System.Security.Cryptography.X509certificates.X509Store "TrustedPeople", "LocalMachine"  
    $trustedPeople.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)  
    $trustedPeople.Add([Security.Cryptography.X509Certificates.X509Certificate2]$bytes)  
    $trustedPeople.Close()  

    # Get thumbprint from cert  
    $sha = new-object System.Security.Cryptography.SHA1CryptoServiceProvider  
    $certHash = $sha.ComputeHash($bytes)  
    $certHashCharArray = "";  
    $certThumbprint = "";  

    # Format the bytes into a hexadecimal string  
    foreach($byte in $certHash)  
    {  
        $temp = ($byte | % {"{0:x}" -f $_}) -join ""  
        $temp = ($temp | % {"{0,2}" -f $_})  
        $certHashCharArray = $certHashCharArray+ $temp;  
    }  
    $certHashCharArray = $certHashCharArray.Replace(' ', '0');  

    # SQL needs the thumbprint in lower case  
    foreach($char in $certHashCharArray)  
    {  
        [System.String]$myString = $char;  
        $certThumbprint = $certThumbprint + $myString.ToLower();  
    }  

    # Configure SQL to use this cert  
    $path = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\Instance Names\SQL"  
    $subKey = (Get-ItemProperty $path).$sqlInstanceName  
    $realPath = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\" + $subKey + "\MSSQLServer\SuperSocketNetLib"  
    $certKeyName = "Certificate"  
    Set-ItemProperty -path $realPath -name $certKeyName -Type string -Value $certThumbprint  

    # restart sql service  
    Restart-Service $SQLServiceName -Force  
    ```  

3.  Führen Sie auf dem Datenbankreplikatserver den folgenden Befehl für Ihre SQL Server-Konfiguration aus:  

    -   Bei Standardinstanzen von SQL Server: Klicken Sie mit der rechten Maustaste auf die Datei **CreateMPReplicaCert.ps1**, und wählen Sie die Option **Mit PowerShell ausführen** aus. Beim Ausführen des Skripts wird das selbstsignierte Zertifikat erstellt, und SQL Server wird für die Verwendung des Zertifikats konfiguriert.  

    -   Bei benannten Instanzen von SQL Server: Führen Sie mithilfe von PowerShell den Befehl **%path%\CreateMPReplicaCert.ps1 xxxxxx** aus, wobei **xxxxxx** für den Namen der SQL Server-Instanz steht.  

    -   Stellen Sie nach Beendigung des Skripts sicher, dass der SQL Server-Agent ausgeführt wird. Wenn dies nicht der Fall ist, starten Sie den SQL Server-Agent neu.  

##### <a name="to-configure-remote-management-points-to-use-the-self-signed-certificate-of-the-database-replica-server"></a>So konfigurieren Sie Remoteverwaltungspunkte für die Verwendung des selbstsignierten Zertifikats des Datenbankreplikatservers  

1.  Führen Sie auf dem Datenbankreplikatserver die folgenden Schritte aus, um das selbstsignierte Zertifikat des Servers zu exportieren:  

    1.  Klicken Sie auf **Start**, dann auf **Ausführen**, und geben Sie **mmc.exe**ein. Klicken Sie in der leeren Konsole auf **Datei**und anschließend auf **Snap-In hinzufügen/entfernen**.  

    2.  Wählen Sie im Dialogfeld **Snap-In hinzufügen/entfernen** aus der Liste **Verfügbare Snap-Ins** die Option **Zertifikate**aus, und klicken Sie dann auf **Hinzufügen**.  

    3.  Wählen Sie im Dialogfeld **Zertifikat-Snap-In** die Option **Computerkonto**aus, und klicken Sie auf **Weiter**.  

    4.  Vergewissern Sie sich, dass im Dialogfeld **Computer auswählen** die Option **Lokaler Computer: (der Computer, auf dem diese Konsole ausgeführt wird)** ausgewählt ist. Klicken Sie anschließend auf **Fertig stellen**.  

    5.  Klicken Sie im Dialogfeld **Snap-Ins hinzufügen/entfernen** auf **OK**.  

    6.  In der Konsole erweitern Sie den Bereich **Zertifikate (Lokaler Computer)** , dann den Bereich **Persönlich**, und wählen Sie **Zertifikate**aus.  

    7.  Klicken Sie mit der rechten Maustaste auf das Zertifikat mit dem Anzeigenamen **ConfigMgr SQL Server Identification Certificate**, klicken Sie auf **Alle Tasks**, und wählen Sie dann **Export**aus.  

    8.  Schließen Sie den **Assistenten zum Exportieren** von Zertifikaten mit den Standardoptionen ab, und speichern Sie das Zertifikat mit der Dateinamenerweiterung **.cer** .  

2.  Führen Sie auf dem Verwaltungspunktcomputer die folgenden Schritte aus, um das selbstsignierte Zertifikat für den Datenbankreplikatserver zum Zertifikatsspeicher Vertrauenswürdige Personen des Verwaltungspunkts hinzuzufügen:  

    1.  Wiederholen Sie die Schritte 1.a bis 1.e um das MMC-Snap-In **Zertifikat** auf dem Verwaltungspunktcomputer zu konfigurieren.  

    2.  Erweitern Sie in der Konsole den Bereich **Zertifikate (Lokaler Computer)** , dann den Bereich **Vertrauenswürdige Personen**, klicken Sie mit der rechten Maustaste auf **Zertifikate**, wählen Sie **Alle Tasks**aus, und wählen Sie dann **Importieren** aus, um den **Zertifikatimport-Assistenten** zu starten.  

    3.  Wählen Sie auf der Seite **Importdatei** das in Schritt 1.h gespeicherte Zertifikat aus, und klicken Sie dann auf **Weiter**.  

    4.  Wählen Sie auf der Seite **Zertifikatspeicher** die Option **Alle Zertifikate in folgendem Speicher speichern**aus, legen Sie **Zertifikatspeicher** auf **Vertrauenswürdige Personen**fest, und klicken Sie dann auf **Weiter**.  

    5.  Klicken Sie auf **Fertig stellen** , um den Assistenten zu schließen und die Zertifikatkonfiguration für den Verwaltungspunkt abzuschließen.  

###  <a name="step-5---configure-the-sql-server-service-broker-for-the-database-replica-server"></a><a name="BKMK_DBreplica_SSB"></a> Schritt 5: Konfigurieren des SQL Server Service Broker für den Datenbankreplikatserver  
Sie müssen die Kommunikation zwischen dem Standortdatenbankserver und dem Datenbankreplikatserver für SQL Server Service Broker konfigurieren, um die Clientbenachrichtigung mit einem Datenbankreplikat für einen Verwaltungspunkt zu unterstützen. Dafür müssen Sie beide Datenbanken mit Informationen zur jeweils anderen Datenbank konfigurieren und für eine sichere Kommunikation zwischen den beiden Datenbanken Zertifikate austauschen.  

> [!NOTE]  
>  Bevor Sie die folgende Prozedur verwenden können, muss der Datenbankreplikatserver die Erstsynchronisierung mit dem Standortdatenbankserver erfolgreich abgeschlossen haben.  

 Anhand des folgenden Verfahrens wird der Service Broker-Port nicht modifiziert, der in SQL Server für den Standortdatenbankserver oder den Datenbankreplikatserver konfiguriert ist. Stattdessen wird mit diesem Verfahren jede Datenbank so konfiguriert, dass mit der jeweils anderen Datenbank mithilfe des korrekten Service Broker-Ports kommuniziert wird.  

 Gehen Sie wie folgt vor, um den Service Broker für den Standortdatenbankserver und den Datenbankreplikatserver zu konfigurieren.  

##### <a name="to-configure-the-service-broker-for-a-database-replica"></a>So konfigurieren Sie den Service Broker für ein Datenbankreplikat  

1. Stellen Sie über **SQL Server Management Studio** eine Verbindung mit der Datenbank des Datenbankreplikatservers her, und führen Sie dann die folgende Abfrage aus, um Service Broker auf dem Datenbankreplikatserver zu aktivieren: **ALTER DATABASE &lt;Replikatdatenbankname\> SET ENABLE_BROKER, HONOR_BROKER_PRIORITY ON WITH ROLLBACK IMMEDIATE**  

2. Konfigurieren Sie als Nächstes auf dem Datenbankreplikatserver den Service Broker für Clientbenachrichtigungen und exportieren Sie das Service Broker-Zertifikat. Führen Sie dazu eine gespeicherte SQL Server-Prozedur aus, durch die in einer einzigen Aktion der Service Broker konfiguriert und das Zertifikat exportiert wird. Wenn Sie die gespeicherte Prozedur ausführen, müssen Sie den FQDN des Datenbankreplikatservers, den Namen der Datenbank der Datenbankreplikate sowie einen Ort für den Export der Zertifikatdatei angeben.  

    Führen Sie die folgende Abfrage aus, um die erforderlichen Details auf dem Datenbankreplikatserver zu konfigurieren und das Zertifikat für den Datenbankreplikatserver zu exportieren: **EXEC sp_BgbConfigSSBForReplicaDB '&lt;Replica SQL Server-FQDN\>', '&lt;Replikatdatenbankname\>', '&lt;Dateipfad der Zertifikatsicherung\>'**  

   > [!NOTE]  
   >  Wenn sich der Datenbankreplikatserver nicht auf der Standardinstanz von SQL Server befindet, müssen Sie für diesen Schritt zusätzlich zum Replikatdatenbanknamen den Instanznamen angeben. Ersetzen Sie dafür den **&lt;Replikatdatenbanknamen\>** durch **&lt;Instanzname\\Replikatdatenbankname\>** .  

    Nachdem Sie das Zertifikat vom Datenbankreplikatserver exportiert haben, legen Sie eine Kopie des Zertifikats auf dem Datenbankserver der primären Standorte ab.  

3. Verwenden Sie **SQL Server Management Studio** , um eine Verbindung zur primären Standortdatenbank herzustellen. Nachdem Sie eine Verbindung zur primären Standortdatenbank hergestellt haben, führen Sie eine Abfrage durch, um die Zertifikate zu importieren und geben Sie folgende Informationen an: den Service Broker-Port, der auf dem Datenbankreplikatserver verwendet wird, den FQDN des Datenbankreplikatservers und den Namen der Datenbank zu den Datenbankreplikaten. So wird die Datenbank primärer Standorte zur Verwendung von Service Broker konfiguriert, um eine Verbindung zur Datenbank des Datenbankreplikatservers herzustellen.  

    Führen Sie die folgende Abfrage aus, um das Zertifikat vom Datenbankreplikatserver zu importieren, und geben Sie die erforderlichen Details ein: **EXEC sp_BgbConfigSSBForRemoteService 'REPLICA', '&lt;SQL Service Broker-Port\>', '&lt;Zertifikatsdateipfad\>', '&lt;Replica SQL Server-FQDN\>', '&lt;Replikatdatenbankname\>'**  

   > [!NOTE]  
   >  Wenn sich der Datenbankreplikatserver nicht auf der Standardinstanz von SQL Server befindet, müssen Sie für diesen Schritt zusätzlich zum Replikatdatenbanknamen den Instanznamen angeben. Ersetzen Sie dafür den **&lt;Replikatdatenbanknamen\>** durch **\Instanzname\\Replikatdatenbankname\>** .  

4. Führen Sie anschließend auf dem Standortdatenbankserver folgenden Befehl aus, um das Zertifikat für den Standortdatenbankserver zu exportieren: **EXEC sp_BgbCreateAndBackupSQLCert '&lt;Dateipfad der Zertifikatsicherung\>'**  

    Nachdem Sie das Zertifikat vom Standortdatenbankserver exportiert haben, legen Sie eine Kopie des Zertifikats auf dem Datenbankreplikatserver ab.  

5. Verwenden Sie **SQL Server Management Studio** , um eine Verbindung zur Datenbank des Datenbankreplikatservers herzustellen. Nachdem Sie eine Verbindung zur Datenbank des Datenbankreplikatservers hergestellt haben, führen Sie eine Abfrage aus, um das Zertifikat zu importieren, und geben Sie den Standortcode des primären Standorts sowie den Service Broker-Port an, der auf dem Standortdatenbankserver verwendet wird. So wird der Datenbankreplikatserver zur Verwendung von Service Broker konfiguriert, um eine Verbindung zur Datenbank des primären Standorts herzustellen.  

    Führen Sie die folgende Abfrage aus, um das Zertifikat vom Standortdatenbankserver zu importieren: **EXEC sp_BgbConfigSSBForRemoteService '&lt;Standortcode\>', '&lt;SQL Service Broker-Port\>', '&lt;Zertifikatsdateipfad\>'**  

   Einige Minuten nachdem Sie die Konfiguration der Standortdatenbank und der Datenbank der Datenbankreplikation abgeschlossen haben, wird vom Warnungs-Manager am primären Standort die Service Broker-Konversation zur Clientbenachrichtigung von der primären Standortdatenbank an das Datenbankreplikat eingerichtet.  

###  <a name="supplemental-script-for-additional-database-replicas-on-a-single-sql-server"></a><a name="bkmk_supscript"></a> Zusätzliches Skript für zusätzliche Datenbankreplikate auf einem einzelnen Computer mit SQL Server  
 Wenn Sie das Skript in Schritt 4 zum Konfigurieren eines selbstsignierten Zertifikats für den Datenbankreplikatserver auf einem Computer mit SQL Server konfigurieren, der bereits über ein Datenbankreplikat verfügt, das Sie weiterhin nutzen möchten, müssen Sie eine geänderte Version des Originalskripts verwenden. Die folgenden Änderungen bewirken, dass das Skript ein vorhandenes Zertifikat nicht vom Server löscht und nachfolgende Zertifikate mit eindeutigen Anzeigenamen erstellt werden.  Bearbeiten Sie das Originalskript wie folgt:  

-   Es muss jede Zeile zwischen den Skripteinträgen **# Delete existing cert if one exists** und **# Create the new cert**auskommentiert werden (um die Ausführung zu verhindern). Fügen Sie hierzu jeder betreffenden Zeile  **#**  als erstes Zeichen hinzu.  

-   Für jedes nachfolgende Datenbankreplikat, das Sie mithilfe dieses Skripts konfigurieren, müssen Sie den Anzeigenamen des Zertifikats aktualisieren.  Bearbeiten Sie hierzu die Zeile **$enrollment.CertificateFriendlyName = "ConfigMgr SQL Server Identification Certificate"** , indem Sie **ConfigMgr SQL Server Identification Certificate** durch einen Namen wie  **ConfigMgr SQL Server Identification Certificate1**ersetzen.  

##  <a name="manage-database-replica-configurations"></a><a name="BKMK_DBReplicaOps"></a> Verwalten von Konfigurationen von Datenbankreplikaten  
 Wenn Sie an einem Standort ein Datenbankreplikat verwenden, finden Sie in den folgenden Abschnitten Informationen zum Deinstallieren eines Datenbankreplikats sowie eines Standorts, der ein Datenbankreplikat verwendet. Außerdem erhalten Sie Informationen zum Verschieben der Standortdatenbank auf eine neue Installation von SQL Server. Wenn Sie anhand der Informationen in den folgenden Abschnitten Veröffentlichungen löschen, richten Sie sich nach dem Leitfaden zum Löschen der transaktionalen Replikation für die Version von SQL Server, die Sie für das Datenbankreplikat verwenden. Weitere Informationen finden Sie unter [Löschen einer Veröffentlichung](/sql/relational-databases/replication/publish/delete-a-publication).  

> [!NOTE]  
>  Nachdem Sie eine Standortdatenbank wiederhergestellt haben, die für Datenbankreplikate konfiguriert war, müssen Sie vor der Verwendung der Datenbankreplikate jedes Replikat neu konfigurieren, indem Sie die Veröffentlichungen und die Abonnements neu erstellen.  

###  <a name="uninstall-a-database-replica"></a><a name="BKMK_UninstallDbReplica"></a> Deinstallieren eines Datenbankreplikats  
 Wenn Sie für einen Verwaltungspunkt ein Datenbankreplikat verwenden, müssen Sie das Datenbankreplikat möglicherweise für einen gewissen Zeitraum deinstallieren und es dann zur weiteren Verwendung erneut konfigurieren. Beispiel: Sie müssen Datenbankreplikate entfernen, bevor Sie ein Upgrade eines Configuration Manager-Standorts auf ein neues Service Pack vornehmen. Nachdem Sie das Standortupgrade abgeschlossen haben, können Sie das Datenbankreplikat für die Verwendung wiederherstellen.  

 Gehen Sie folgendermaßen vor, um ein Datenbankreplikat zu deinstallieren.  

1.  Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** die Option **Standortkonfiguration**, wählen Sie dann **Server und Standortsystemrollen** und anschließend im Detailbereich den Standortsystemserver aus, auf dem der Verwaltungspunkt gehostet wird, von dem das zu deinstallierende Datenbankreplikat genutzt wird.  

2.  Klicken Sie im Bereich **Standortsystemrollen** mit der rechten Maustaste auf **Verwaltungspunkt** , und wählen Sie **Eigenschaften**aus.  

3.  Wählen Sie auf der Registerkarte **Verwaltungspunktdatenbank** die Option **Standortdatenbank verwenden** aus, um den Verwaltungspunkt zur Verwendung der Standortdatenbank anstelle des Datenbankreplikats zu konfigurieren. Klicken Sie dann auf **OK** , um die Konfiguration zu speichern.  

4.  Verwenden Sie als Nächstes **SQL Server Management Studio** , um folgende Tasks durchzuführen:  

    -   Löschen der Veröffentlichung für das Datenbankreplikat auf dem Standortdatenbankserver.  

    -   Löschen der Veröffentlichung für das Datenbankreplikat vom Datenbankreplikatserver.  

    -   Löschen der Replikatdatenbank vom Datenbankreplikatserver.  

    -   Deaktivieren der Veröffentlichung und Verteilung auf dem Standortdatenbankserver. Zur Deaktivierung von Veröffentlichung und Verteilung klicken Sie mit der rechten Maustaste auf den Replikationsordner und anschließend auf **Veröffentlichung und Verteilung deaktivieren**.  

5.  Nachdem Sie Veröffentlichung, Abonnement und Replikatdatenbank gelöscht und das Veröffentlichen auf dem Standortdatenbankserver deaktiviert haben, wird das Datenbankreplikat deinstalliert.  

###  <a name="uninstall-a-site-server-that-publishes-a-database-replica"></a><a name="BKMK_DBReplicaOps_Uninstall"></a> Deinstallieren eines Standortservers, der ein Datenbankreplikat veröffentlicht  
 Bevor Sie einen Standort deinstallieren, von dem ein Datenbankreplikat verwendet wird, führen Sie die folgenden Schritte aus, um die Veröffentlichung und vorhandene Abonnements zu bereinigen.  

1.  Verwenden Sie **SQL Server Management Studio** , um die Veröffentlichung des Datenbankreplikats aus der Datenbank des Standortservers zu löschen.  

2.  Verwenden Sie **SQL Server Management Studio** , um das Abonnement des Datenbankreplikats von jedem Remote-SQL Server zu löschen, auf dem ein Datenbankreplikat für diesen Standort gehostet ist.  

3.  Deinstallieren Sie den Standort.  

###  <a name="move-a-site-server-database-that-publishes-a-database-replica"></a><a name="BKMK_DBReplicaOps_Move"></a> Verschieben eines Standortservers, der ein Datenbankreplikat veröffentlicht  
 Gehen Sie wie folgt vor, um die Standortdatenbank auf einen neuen Computer zu verschieben:  

1.  Verwenden Sie **SQL Server Management Studio** , um die Veröffentlichung des Datenbankreplikats aus der Datenbank des Standortservers zu löschen.  

2.  Verwenden Sie **SQL Server Management Studio** , um das Abonnement des Datenbankreplikats von jedem Datenbankreplikatserver für diesen Standort zu löschen.  

3.  Verschieben Sie die Datenbank auf den neuen SQL Server-Computer. Weitere Informationen finden Sie im Abschnitt [Ändern der Konfiguration für die Standortdatenbank](../../../../core/servers/manage/modify-your-infrastructure.md#bkmk_dbconfig) des Themas [Ändern Ihrer Configuration Manager-Infrastruktur](../../../../core/servers/manage/modify-your-infrastructure.md).  

4.  Erstellen Sie die Veröffentlichung des Datenbankreplikats auf dem Standortdatenbankserver erneut. Weitere Informationen finden Sie unter [Schritt 1: Konfigurieren des Standortdatenbankservers für die Veröffentlichung des Datenbankreplikats](#BKMK_DBReplica_ConfigSiteDB) in diesem Thema.  

5.  Erstellen Sie die Abonnements des Datenbankreplikats auf jedem Datenbankreplikatserver erneut. Weitere Informationen finden Sie unter [Schritt 2: Konfigurieren des Datenbankreplikatservers](#BKMK_DBReplica_ConfigSrv) in diesem Thema.