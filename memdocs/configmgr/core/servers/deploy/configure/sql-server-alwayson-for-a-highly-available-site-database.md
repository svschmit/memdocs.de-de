---
title: SQL Server Always On
titleSuffix: Configuration Manager
description: Planen der Verwendung einer SQL Server AlwaysOn-Verfügbarkeitsgruppen mit Configuration Manager
ms.date: 07/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9ce8c10d9d59d97caa53ece12dd43d90c78546bb
ms.sourcegitcommit: 488db8a6ab272f5d639525d70718145c63d0de8f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/14/2020
ms.locfileid: "86384841"
---
# <a name="prepare-to-use-sql-server-always-on-availability-groups-with-configuration-manager"></a>Vorbereiten der Verwendung von SQL Server AlwaysOn-Verfügbarkeitsgruppen mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

In diesem Artikel erfahren Sie, wie Sie Configuration Manager für die Verwendung von SQL Server AlwaysOn-Verfügbarkeitsgruppen vorbereiten. Mit diesem Feature erhalten Sie eine Hochverfügbarkeits- und Notfallwiederherstellungslösung für die Standortdatenbank.  

Configuration Manager unterstützt die Verwendung von Verfügbarkeitsgruppen:

- An primären Standorten und am Standort der zentralen Verwaltung.
- Lokal oder in Microsoft Azure.

Wenn Sie Verfügbarkeitsgruppen in Microsoft Azure verwenden, können Sie die Verfügbarkeit Ihrer Standortdatenbank weiter steigern, indem Sie *Azure-Verfügbarkeitsgruppen* einsetzen. Weitere Informationen zu Azure-Verfügbarkeitsgruppen finden Sie unter [Verwalten der Verfügbarkeit von virtuellen Computern](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-manage-availability/).

> [!Important]
> Machen Sie sich mit der Konfiguration von SQL Server und SQL Server-Verfügbarkeitsgruppen vertraut, bevor Sie fortfahren. In den folgenden Informationen wird auf die SQL Server-Dokumentationsbibliothek und entsprechende Verfahren verwiesen.


## <a name="supported-scenarios"></a>Unterstützte Szenarien

Die folgenden Szenarios werden für die Verwendung von Verfügbarkeitsgruppen mit Configuration Manager unterstützt. Ausführliche Informationen und Vorgehensweisen für die einzelnen Szenarien finden Sie unter [Konfigurieren von Verfügbarkeitsgruppen für Configuration Manager](configure-aoag.md).

- [Erstellen einer Verfügbarkeitsgruppe für die Verwendung mit Configuration Manager](configure-aoag.md#bkmk_create)  
- [Konfigurieren eines Standorts für die Verwendung der Verfügbarkeitsgruppe](configure-aoag.md#bkmk_configure)  
- [Hinzufügen oder Entfernen von synchronen Replikationsmitgliedern zu bzw. aus Verfügbarkeitsgruppen, die eine Standortdatenbank hosten](configure-aoag.md#bkmk_sync)  
- [Konfigurieren oder Wiederherstellen eines Standorts über ein Replikat mit asynchronem Commit](configure-aoag.md#bkmk_async)  
- [Verschieben einer Standortdatenbank aus einer Verfügbarkeitsgruppe in eine Standardinstanz oder eine benannte Instanz einer eigenständigen SQL Server-Instanz](configure-aoag.md#bkmk_stop)  


## <a name="prerequisites"></a>Voraussetzungen

Die folgenden Voraussetzungen gelten für alle Szenarien. Wenn zusätzliche Voraussetzungen für ein bestimmtes Szenario gelten, werden sie für das Szenario angegeben.

### <a name="configuration-manager-accounts-and-permissions"></a>Konten und Berechtigungen in Configuration Manager

#### <a name="installation-account"></a>Installationskonto

Für das Konto, mit dem das Configuration Manager-Setup ausgeführt wird, muss Folgendes gelten:

- Es muss auf jedem Computer, der Mitglied der Verfügbarkeitsgruppe ist, ein Mitglied der lokalen Gruppe **Administratoren** sein.
- Es muss ein **Systemadministrator** für jede SQL Server-Instanz sein, die die Standortdatenbank hostet.

#### <a name="site-server-to-replica-member-access"></a>Zugriff des Standortservers auf Replikationsmitglieder

Das Computerkonto des Standortservers muss Mitglied der lokalen Gruppe **Administratoren** auf allen Computern sein, die zur Verfügbarkeitsgruppe gehören.

### <a name="sql-server"></a>SQL Server

#### <a name="version"></a>Version

Jedes Replikat in der Verfügbarkeitsgruppe muss eine Version von SQL Server ausführen, die von Ihrer Configuration Manager-Version unterstützt wird. Wenn von SQL Server unterstützt, können die verschiedenen Knoten einer Verfügbarkeitsgruppe unterschiedliche Versionen von SQL Server ausführen. Weitere Informationen finden Sie unter [Vom Configuration Manager unterstützte SQL Server-Konfigurationen](../../../plan-design/configs/support-for-sql-server-versions.md).<!--SCCMDocs issue 656-->

#### <a name="edition"></a>Edition

Verwenden Sie eine *Enterprise* Edition von SQL Server.

#### <a name="account"></a>Konto

Jede Instanz von SQL Server kann mit einem Domänenbenutzerkonto (**Dienstkonto**) oder mit einem Nicht-Domänenkonto ausgeführt werden. Jedes Replikat in einer Gruppe kann eine andere Konfiguration aufweisen.

- Verwenden Sie ein Konto mit geringstmöglichen Berechtigungen. Weitere Informationen finden Sie unter [Überlegungen zur Sicherheit bei SQL Server-Installationen](https://docs.microsoft.com/sql/sql-server/install/security-considerations-for-a-sql-server-installation).  

- Weitere Informationen zum Konfigurieren von Dienstkonten und Berechtigungen für SQL Server finden Sie unter [Konfigurieren von Windows-Dienstkonten und -Berechtigungen](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions).  

- Sie müssen Zertifikate verwenden, um ein Nicht-Domänenkonto zu verwenden. Weitere Informationen finden Sie unter [Verwenden von Zertifikaten für einen Datenbankspiegelungs-Endpunkt (Transact-SQL)](https://docs.microsoft.com/sql/database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql).  

- Weitere Informationen finden Sie unter [Erstellen eines Endpunkts für die Datenbankspiegelung für AlwaysOn-Verfügbarkeitsgruppen](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell).  


### <a name="database"></a>Datenbank

#### <a name="configure-the-database-on-a-new-replica"></a>Konfigurieren der Datenbank für ein neues Replikat

Konfigurieren Sie die Datenbank der einzelnen Replikate mit den folgenden Einstellungen:  

- Aktivieren Sie die **CLR-Integration**:

    ``` SQL
    sp_configure 'show advanced options', 1;  
    GO  
    RECONFIGURE;  
    GO  
    sp_configure 'clr enabled', 1;  
    GO  
    RECONFIGURE;  
    GO
    ```

    Weitere Informationen finden Sie unter [CLR-Integration: Aktivierung](https://docs.microsoft.com/sql/relational-databases/clr-integration/clr-integration-enabling).  

- Legen Sie **Max. Textgröße für die Replikation** auf `2147483647` fest:  

    ``` SQL
    EXECUTE sp_configure 'max text repl size (B)', 2147483647
    ```

- Legen Sie den Datenbankbesitzer auf das *SA-Konto* fest. Sie müssen dieses Konto nicht aktivieren.

- Legen Sie die Einstellung **TRUSTWORTY** auf **ON** fest:

    ``` SQL
    ALTER DATABASE [CM_xxx] SET TRUSTWORTHY ON;
    ```

    Weitere Informationen finden Sie unter [TRUSTWORTHY-Datenbankeigenschaft](https://docs.microsoft.com/sql/relational-databases/security/trustworthy-database-property).

- Aktivieren Sie den **Service Broker**:  

    ``` SQL
    ALTER DATABASE [CM_xxx] SET ENABLE_BROKER
    ```

    > [!Note]  
    > Sie können die Service Broker-Option nicht für eine Datenbank aktivieren, die bereits einer Verfügbarkeitsgruppe angehört. Sie müssen diese Option aktivieren, bevor Sie sie der Verfügbarkeitsgruppe hinzufügen.<!-- SCCMDocs#1432 -->

- Konfigurieren Sie die Service Broker-Priorität:

    ``` SQL
    ALTER DATABASE [CM_xxx] SET HONOR_BROKER_PRIORITY ON;
    ALTER DATABASE [CM_xxx] SET ENABLE_BROKER WITH ROLLBACK IMMEDIATE

    ```

Legen Sie diese Konfigurationen nur für ein primäres Replikat fest. Um ein sekundäres Replikat konfigurieren zu können, führen Sie zuerst ein Failover für die primäre zur sekundären Datenbank durch. Dadurch wird das sekundäre Replikat zum neuen primären Replikat.

#### <a name="database-verification-script"></a>Datenbank-Überprüfungsskript

Führen Sie das folgende SQL-Skript aus, um die Datenbankkonfigurationen für primäre und sekundäre Replikate zu überprüfen. Bevor Sie für ein sekundäres Replikat ein Problem beheben können, machen Sie dieses sekundäre Replikat zum primären Replikat.

``` SQL
    SET NOCOUNT ON

    DECLARE @dbname NVARCHAR(128)

    SELECT @dbname = sd.name FROM sys.sysdatabases sd WHERE sd.dbid = DB_ID()

    IF (@dbname = N'master' OR @dbname = N'model' OR @dbname = N'msdb' OR @dbname = N'tempdb' OR @dbname = N'distribution' ) BEGIN
    RAISERROR(N'ERROR: Script is targeting a system database.  It should be targeting the DB you created instead.', 0, 1)
    GOTO Branch_Exit;
    END ELSE
    PRINT N'INFO: Targeted database is ' + @dbname + N'.'

    PRINT N'INFO: Running verifications....'

    IF NOT EXISTS (SELECT * FROM sys.configurations c WHERE c.name = 'clr enabled' AND c.value_in_use = 1)
    PRINT N'ERROR: CLR is not enabled!'
    ELSE
    PRINT N'PASS: CLR is enabled.'

    DECLARE @repltable TABLE (
    name nvarchar(max),
    minimum int,
    maximum int,
    config_value int,
    run_value int )

    INSERT INTO @repltable
    EXEC sp_configure 'max text repl size (B)'

    IF NOT EXISTS(SELECT * from @repltable where config_value = 2147483647 and run_value = 2147483647 )
    PRINT N'ERROR: Max text repl size is not correct!'
    ELSE
    PRINT N'PASS: Max text repl size is correct.'

    IF NOT EXISTS (SELECT db.owner_sid FROM sys.databases db WHERE db.database_id = DB_ID() AND db.owner_sid = 0x01)
    PRINT N'ERROR: Database owner is not sa account!'
    ELSE
    PRINT N'PASS: Database owner is sa account.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_trustworthy_on = 1 )
    PRINT N'ERROR: Trustworthy bit is not on!'
    ELSE
    PRINT N'PASS: Trustworthy bit is on.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_broker_enabled = 1 )
    PRINT N'ERROR: Service broker is not enabled!'
    ELSE
    PRINT N'PASS: Service broker is enabled.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_honor_broker_priority_on = 1 )
    PRINT N'ERROR: Service broker priority is not set!'
    ELSE
    PRINT N'PASS: Service broker priority is set.'

    PRINT N'Done!'

    Branch_Exit:
```


### <a name="availability-group-configurations"></a>Konfigurationen von Verfügbarkeitsgruppen

#### <a name="replica-members"></a>Replikationsmitglieder

- Die Verfügbarkeitsgruppe muss ein primäres Replikat besitzen.  

- Nutzen Sie die gleiche Anzahl und Art von Replikaten in einer Verfügbarkeitsgruppe, die Ihre SQL Server-Version unterstützt.

- Sie können ein Replikat mit asynchronem Commit zum Wiederherstellen Ihres synchronen Replikats verwenden. Weitere Informationen finden Sie unter [Wiederherstellungsoptionen für Standortdatenbanken](../../manage/recover-sites.md#site-database-recovery-options).  

    > [!Warning]  
    > Configuration Manager unterstützt nicht, dass *Failover* Replikate mit asynchronem Commit als Standortdatenbank verwenden. Weitere Informationen finden Sie unter [Failover und Failovermodi (AlwaysOn-Verfügbarkeitsgruppen)](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups).  

Configuration Manager prüft den Status des Replikats mit asynchronem Commit nicht auf seine Aktualität. Die Verwendung eines Replikats mit asynchronem Commit als Standortdatenbank kann die Integrität Ihres Standorts und Ihrer Daten gefährden. Dieses Replikat kann immanent asynchron sein. Weitere Informationen finden Sie unter [Übersicht über SQL Server AlwaysOn-Verfügbarkeitsgruppen](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server).

Jedes Replikationsmitglied muss wie folgt konfiguriert sein:

- Entweder die *Standardinstanz* oder eine *benannte Instanz* wird verwendet.  

- Für **Verbindungen in primärer Rolle** ist **Alle Verbindungen zulassen** festgelegt.  

- Die Einstellung **Lesbare sekundäre Rolle** ist auf **Ja** festlegt.  

- **Manuelles Failover** ist aktiviert.

    > [!Note]
    > In Version 1902 und früher müssen Sie alle Verfügbarkeitsgruppen auf dem SQL Server für manuelles Failover konfigurieren. Diese Konfiguration ist selbst dann erforderlich, wenn er nicht als Host für die Standortdatenbank fungiert.
    >
    > Ab Version 1906 unterstützt Configuration Manager bei Festlegung auf **Automatisches Failover** die Verwendung der synchronen Verfügbarkeitsgruppenreplikate. Legen Sie in folgenden Fällen **Manuelles Failover** fest:
    >
    > - Sie führen das Configuration Manager-Setup aus, um die Verwendung der Standortdatenbank in der Verfügbarkeitsgruppe anzugeben.  
    > - Sie installieren ein Update für Configuration Manager. (Nicht nur Updates, die auf die Standortdatenbank angewendet werden).  

- Alle Mitglieder müssen denselben [Seedingmodus](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas) aufweisen.<!-- SCCMDocs-pr#3899 --> Das Configuration Manager-Setup schließt eine Voraussetzungsprüfung für diese Konfiguration ein, wenn eine Datenbank durch Installation oder Wiederherstellung erstellt wird.

    > [!Note]  
    > Wenn Setup die Datenbank erstellt und Sie **automatisches** Seeding konfigurieren, muss die Verfügbarkeitsgruppe über die Berechtigungen zum Erstellen der Datenbank verfügen. Diese Anforderung gilt sowohl für eine neue Datenbank als auch für eine Wiederherstellung. Weitere Informationen finden Sie unter [Automatic seeding for secondary replica](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas#security) (Automatisches Seeding für ein sekundäres Replikat).<!-- SCCMDocs-pr#3900 -->

#### <a name="replica-member-location"></a>Speicherort der Replikationsmitglieder

Alle Replikate in einer Verfügbarkeitsgruppe müssen lokal oder in Microsoft Azure gehostet werden. Eine Gruppe, die ein lokales Mitglied und ein Mitglied in Azure enthält, wird nicht unterstützt.

> [!NOTE]
> Wenn Sie einen virtuellen Azure-Computer für SQL Server verwenden, aktivieren Sie **Floating IP**. Weitere Informationen finden Sie unter [Konfigurieren eines Load Balancers für eine SQL Server-Always On-Verfügbarkeitsgruppe auf virtuellen Azure-Computern](https://docs.microsoft.com/azure/azure-sql/virtual-machines/windows/availability-group-load-balancer-portal-configure).<!-- SCCMDocs#1928 -->

Für das Setup von Configuration Manager muss eine Verbindung mit jedem Replikat hergestellt werden. Wenn Sie eine Verfügbarkeitsgruppe in Azure einrichten und die Gruppe sich hinter einem internen oder externen Lastenausgleich befindet, öffnen Sie die folgenden Standardports:

- RPC-Endpunktzuordnung: **TCP 135**

- SQL Server Service Broker: **TCP 4022**  

- SQL über TCP: **TCP 1433**

Nach Abschluss des Setups müssen die folgenden Ports für Configuration Manager und die Replikationslinkanalyse geöffnet bleiben.<!-- MEMDocs#375 -->

Sie können benutzerdefinierte Ports für diese Konfigurationen verwenden. Verwenden Sie für den Endpunkt und auf allen Replikaten in der Verfügbarkeitsgruppe die gleichen Ports.

Erstellen Sie eine Lastenausgleichsregel für jeden Port des Azure-Lastenausgleichs, damit SQL Daten zwischen Standorten repliziert. Weitere Informationen finden Sie unter [Konfigurieren von Hochverfügbarkeitsports für internen Lastenausgleich](https://docs.microsoft.com/azure/load-balancer/load-balancer-configure-ha-ports).<!-- MEMDocs#252 -->

#### <a name="listener"></a>Listener

Die Verfügbarkeitsgruppe muss mindestens einen *Verfügbarkeitsgruppenlistener*besitzen. Wenn Sie Configuration Manager für die Verwendung der Standortdatenbank in der Verfügbarkeitsgruppe konfigurieren, wird der virtuelle Name dieses Listeners verwendet. Eine Verfügbarkeitsgruppe kann zwar mehrere Listener enthalten, Configuration Manager kann aber nur einen nutzen. Weitere Informationen finden Sie unter [Erstellen oder Konfigurieren eines SQL Server-Verfügbarkeitsgruppenlisteners](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server).

#### <a name="file-paths"></a>Dateipfade

Wenn Sie das Setup von Configuration Manager so ausführen, dass ein Standort für die Verwendung der Datenbank in einer Verfügbarkeitsgruppe konfiguriert wird, muss jeder sekundäre Replikatserver einen SQL Server-Dateipfad aufweisen, der identisch mit dem Dateipfad der Standortdatenbankdateien für das aktuelle primäre Replikat ist. Wenn kein identischer Pfad vorhanden ist, kann das Setup die Instanz für die Verfügbarkeitsgruppe nicht als neuen Speicherort der Standortdatenbank hinzufügen.  

Das lokale SQL Server-Dienstkonto muss über die Berechtigung **Vollzugriff** für diesen Ordner verfügen.

Die sekundären Replikatserver benötigen diesen Dateipfad nur, während Sie das Configuration Manager-Setup verwenden, um die Datenbankinstanz der Verfügbarkeitsgruppe anzugeben. Nachdem die Konfiguration der Standortdatenbank in der Verfügbarkeitsgruppe durchgeführt wurde, können Sie den nicht verwendeten Pfad von sekundären Replikatservern löschen.

Betrachten Sie beispielsweise das folgende Szenario:

- Sie erstellen eine Verfügbarkeitsgruppe, die drei SQL Server-Instanzen verwendet.  

- Ihr primärer Replikatserver ist eine Neuinstallation von SQL Server 2014. Standardmäßig speichert dieser MDF- und LDF-Datenbankdateien unter `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA`.  

- Sie haben für beide sekundäre Replikatserver ein Upgrade von älteren Versionen auf SQL Server 2014 durchgeführt. Mit dem Upgrade behalten diese Server den ursprünglichen Dateipfad zum Speichern von Datenbankdateien dabei: `C:\Program Files\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\DATA`.  

- Bevor Sie die Standortdatenbank in diese Verfügbarkeitsgruppe verschieben, erstellen Sie auf jedem sekundären Replikatserver den folgenden Dateipfad: `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA`. Dieser Pfad ist ein Duplikat des Pfads, der auf dem primären Replikat verwendet wird, auch wenn dieser Dateispeicherort von den sekundären Replikate nicht verwendet wird.  

- Anschließend gewähren Sie dem SQL Server-Dienstkonto für jedes sekundäre Replikat Vollzugriff auf den neu erstellten Speicherort auf dem Server.  

- Sie können nun das Setup von Configuration Manager erfolgreich so ausführen, dass die Standortdatenbank in der Verfügbarkeitsgruppe verwendet wird.  

#### <a name="multi-subnet-failover"></a>Multisubnetz-Failover

<!-- SCCMDocs-pr#3734 -->
Ab Version 1906 können Sie das [Schlüsselwort der MultiSubnetFailover-Verbindungszeichenfolge](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover) in SQL Server aktivieren. Sie müssen auch folgende Werte manuell zur Windows-Registrierung auf dem Standortserver hinzufügen:

``` Registry
HKLM:\SOFTWARE\Microsoft\SMS\Identification
HKLM:\SOFTWARE\Microsoft\SMS\SQL Server

MSF Enabled : 1 (DWORD)
```

> [!Warning]  
> Die Verwendung von [Standortserver-Hochverfügbarkeit](site-server-high-availability.md) und SQL Server Always On mit Multisubnetz-Failover bietet nicht den vollen Funktionsumfang des automatischen Failovers für Szenarien der Notfallwiederherstellung.

Wenn Sie eine Verfügbarkeitsgruppe mit einem Mitglied an einem Remotestandort erstellen müssen, legen Sie Prioritäten gemäß der niedrigsten Netzwerklatenz fest. Eine hohe Netzwerklatenz kann zu Replikationsfehlern führen.<!-- SCCMDocs#1381 -->


## <a name="limitations-and-known-issues"></a>Einschränkungen und bekannte Probleme

Die folgenden Einschränkungen gelten für alle Szenarien.

### <a name="unsupported-sql-server-options-and-configurations"></a>Nicht unterstützte SQL Server-Optionen und -Konfigurationen

- **Basis-Verfügbarkeitsgruppen**: Diese Verfügbarkeitsgruppen, die mit SQL Server 2016 Standard Edition eingeführt wurden, bieten keine Unterstützung für Lesezugriff auf sekundäre Replikate. Für die Konfiguration ist ein derartiger Zugriff jedoch erforderlich. Hintergrundinformationen finden Sie unter [SQL Server-Basisverfügbarkeitsgruppen](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups?view=sql-server-2017).  

- **Failoverclusterinstanz**: Failoverclusterinstanzen werden für ein Replikat, das Sie mit Configuration Manager verwenden, nicht unterstützt. Weitere Informationen finden Sie unter [SQL Server AlwaysOn-Failoverclusterinstanzen](https://docs.microsoft.com/sql/sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server).  

- **MultiSubnetFailover**: In Version 1902 und früher wird das Verwenden einer Verfügbarkeitsgruppe mit Configuration Manager in einer Konfiguration mit mehreren Subnetzen nicht unterstützt. Zudem kann nicht die Schlüsselwortverbindungszeichenfolge [MutliSubnetFailover](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover) verwendet werden.

    Aktualisieren Sie Configuration Manager auf Version 1906 oder höher, damit eine solche Konfiguration unterstützt wird. Weitere Informationen finden Sie unter der [MultiSubnetFailover](sql-server-alwayson-for-a-highly-available-site-database.md#multi-subnet-failover)-Voraussetzung.

### <a name="sql-servers-that-host-additional-availability-groups"></a>SQL Server, die zusätzliche Verfügbarkeitsgruppen hosten

<!--SCCMDocs issue 649-->
Wenn der SQL Server neben der Gruppe, die Sie für Configuration Manager verwenden, eine oder mehrere Verfügbarkeitsgruppen hostet, müssen bei der Ausführung des Configuration Manager-Setups bestimmte Einstellungen für SQL Server festgelegt sein. Diese Einstellungen sind auch für die Installation eines Updates für Configuration Manager erforderlich. Jedes Replikat in den einzelnen Verfügbarkeitsgruppen muss folgende Konfigurationen aufweisen:

- Manuelles Failover  
- Alle schreibgeschützten Verbindungen zulassen  

> [!Note]
> In Version 1902 und früher müssen Sie alle Verfügbarkeitsgruppen auf dem SQL Server für manuelles Failover konfigurieren. Diese Konfiguration ist selbst dann erforderlich, wenn er nicht als Host für die Standortdatenbank fungiert.
>
> Ab Version 1906 unterstützt Configuration Manager bei Festlegung auf **Automatisches Failover** die Verwendung der synchronen Verfügbarkeitsgruppenreplikate. Legen Sie in folgenden Fällen **Manuelles Failover** fest:
>
> - Sie führen das Configuration Manager-Setup aus, um die Verwendung der Standortdatenbank in der Verfügbarkeitsgruppe anzugeben.  
> - Sie installieren ein Update für Configuration Manager. (Nicht nur Updates, die auf die Standortdatenbank angewendet werden).  

### <a name="unsupported-database-use"></a>Nicht unterstützte Datenbankverwendung

#### <a name="configuration-manager-supports-only-the-site-database-in-an-availability-group"></a>Configuration Manager unterstützt nur die Standortdatenbank in einer Verfügbarkeitsgruppe

Die folgenden Datenbanken werden nicht von Configuration Manager in einer SQL Server AlwaysOn-Verfügbarkeitsgruppe unterstützt:  

- Reporting-Datenbank  
- WSUS-Datenbank  

#### <a name="pre-existing-database"></a>Bereits vorhandene Datenbank

Sie können keine neue Datenbank verwenden, die auf dem Replikat erstellt wurde. Wenn Sie eine Verfügbarkeitsgruppe konfigurieren, stellen Sie eine Kopie einer vorhandenen Configuration Manager-Datenbank auf dem primären Replikat wieder her.  

#### <a name="distributed-views"></a>Verteilte Ansichten

<!-- SCCMDocs-pr#3792 -->
Wenn Sie in Version 1902 und früher die Standortdatenbank in einer SQL Server AlwaysOn-Verfügbarkeitsgruppe hosten, können Sie keine [verteilten Ansichten](../../../plan-design/hierarchy/data-transfers-between-sites.md#bkmk_dbrep) für die Datenbankreplikation aktivieren. Aktualisieren Sie auf Version 1906 oder höher, damit eine solche Konfiguration unterstützt wird.


### <a name="setup-errors-in-configmgrsetuplog"></a>Setupfehler in „ConfigMgrSetup.log“

Beim Ausführen des Configuration Manager-Setups zum Verschieben einer Standortdatenbank in eine Verfügbarkeitsgruppe versucht das Setup, Datenbankrollen in den sekundären Replikaten der Verfügbarkeitsgruppe zu verarbeiten. Die Datei **ConfigMgrSetup.log** enthält den folgenden Fehler:  

`ERROR: SQL Server error: [25000][3906][Microsoft][SQL Server Native Client 11.0][SQL Server]Failed to update database "CM_AAA" because the database is read-only. Configuration Manager Setup 1/21/2016 4:54:59 PM 7344 (0x1CB0)`  

Solche Fehler können ignoriert werden.

### <a name="site-expansion"></a>Standorterweiterung

<!--SCCMDocs issue 568-->
Wenn Sie die Standortdatenbank für einen eigenständigen primären Standort mit SQL Server AlwaysOn-Verfügbarkeitsgruppen konfigurieren, kann der Standort nicht auf einen Standort der zentralen Verwaltung erweitert werden. Bei der Ausführung dieses Prozesses tritt dann ein Fehler auf. Um den Standort zu erweitern, entfernen Sie vorübergehend die Datenbank des primären Standorts aus der Verfügbarkeitsgruppe.

Sie müssen keine Änderungen an der Konfiguration vornehmen, wenn Sie einen sekundären Standort hinzufügen.


## <a name="changes-for-site-backup"></a>Änderungen für die Standortsicherung

### <a name="backup-database-files"></a>Sichern von Datenbankdateien
  
Wenn eine Standortdatenbank eine Verfügbarkeitsgruppe verwendet, führen Sie den integrierten Wartungstask **Standortserver sichern** aus, um allgemeine Configuration Manager-Einstellungen und -Dateien zu sichern. Verwenden Sie nicht die MDF- oder LDF-Dateien, die von dieser Sicherung erstellt werden. Erstellen Sie stattdessen mithilfe von SQL Server direkte Sicherungskopien dieser Datenbankdateien.

### <a name="transaction-log"></a>Transaktionsprotokoll  

Legen Sie das Wiederherstellungsmodell der Standortdatenbank auf **Vollständig** fest. Diese Konfiguration ist für die Verwendung von Configuration Manager in einer Verfügbarkeitsgruppe obligatorisch. Planen Sie das Überwachen und Verwalten der Größe des Transaktionsprotokolls für die Standortdatenbank. Beim vollständigen Wiederherstellungsmodell werden Transaktionen erst festgeschrieben, wenn eine vollständige Sicherung der Datenbank oder des Transaktionsprotokolls erfolgt ist. Weitere Informationen finden Sie unter [Sichern und Wiederherstellen von SQL Server-Datenbanken](https://docs.microsoft.com/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases).


## <a name="changes-for-site-recovery"></a>Änderungen für die Standortwiederherstellung

Wenn zumindest ein Knoten der Verfügbarkeitsgruppe funktionsfähig bleibt, verwenden Sie die Sitewiederherstellungsoption **Datenbankwiederherstellung überspringen (diese Option verwenden, wenn die Standortdatenbank nicht betroffen war)** .

Ab Version 1906 kann Site Recovery die Datenbank in einer SQL AlwaysOn-Gruppe neu erstellen. Dieser Prozess funktioniert sowohl mit manuellem als auch mit automatischem Seeding.<!-- SCCMDocs-pr#3846 -->

Wenn in Version 1902 oder früher alle Knoten einer Verfügbarkeitsgruppe verloren gegangen sind, müssen Sie zuerst die Verfügbarkeitsgruppe neu erstellen, bevor Sie den Standort wiederherstellen können. Configuration Manager kann den Verfügbarkeitsknoten nicht neu erstellen oder wiederherstellen. Erstellen Sie die Gruppe neu, stellen Sie die Sicherung wieder her, und konfigurieren Sie SQL neu. Verwenden Sie dann die Sitewiederherstellungsoption **Datenbankwiederherstellung überspringen (diese Option verwenden, wenn die Standortdatenbank nicht betroffen war)** .

Weitere Informationen finden Sie unter [Sicherung und Wiederherstellung](../../manage/backup-and-recovery.md).


## <a name="changes-for-reporting"></a>Änderungen für die Berichterstattung

### <a name="install-the-reporting-service-point"></a>Installieren des Reporting Services-Punkts

Der Reporting Services-Punkt unterstützt nicht die Verwendung des virtuellen Listenernamens der Verfügbarkeitsgruppe. Zudem kann die zugehörige Datenbank nicht in einer SQL Server AlwaysOn-Verfügbarkeitsgruppe gehostet werden.  

- Standardmäßig wird durch die Installation des Reporting Services-Punkts der **Name des Standortdatenbankservers** auf den virtuellen Namen festgelegt, der als Listener angegeben ist. Ändern Sie diese Einstellung, um einen Computernamen und die Instanz eines Replikats in der Verfügbarkeitsgruppe anzugeben.  

- Um die Berichterstellung auszulagern und die Verfügbarkeit zu erhöhen, wenn ein Replikatknoten offline ist, könnten Sie zusätzliche Reporting Services-Punkte auf jedem Replikatknoten installieren. Anschließend konfigurieren Sie jeden Reporting Services-Punkt dahingehend, dass er auf seinen eigenen Computernamen verweist. Bei der Installation eines Reporting Services-Punkts in jedem Replikat der Verfügbarkeitsgruppe kann zur Berichterstattung immer eine Verbindung mit einem aktiven Server mit einem Berichterstattungspunkt hergestellt werden.  

### <a name="switch-the-reporting-services-point-used-by-the-console"></a>Wechseln des Reporting Services-Punkts, der von der Konsole verwendet wird

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Überwachung** den Knoten **Berichterstellung**, und wählen Sie den Knoten **Berichte** aus.

1. Wählen Sie im Menüband die Option **Berichtsoptionen**.  

1. Wählen Sie im Dialogfeld „Berichtsoptionen“ den Reporting Services-Punkt aus, der verwendet werden soll.  


## <a name="next-steps"></a>Nächste Schritte

In diesem Artikel werden die Voraussetzungen, Einschränkungen und Änderungen an allgemeinen Tasks beschrieben, die für Configuration Manager bei der Verwendung von Verfügbarkeitsgruppen erforderlich sind. Anweisungen zum Einrichten und Konfigurieren Ihres Standorts für die Verwendung von Verfügbarkeitsgruppen finden Sie unter [Konfigurieren von Verfügbarkeitsgruppen](configure-aoag.md).
