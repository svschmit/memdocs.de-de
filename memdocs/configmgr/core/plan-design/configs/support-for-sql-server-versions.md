---
title: Unterstützte Versionen von SQL Server
titleSuffix: Configuration Manager
description: Abrufen der SQL Server-Version und Konfigurationsanforderungen zum Hosten einer Configuration Manager-Standortdatenbank.
ms.date: 06/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 35e237b6-9f7b-4189-90e7-8eca92ae7d3d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b30380f4e272050b7224b52d092f39aa8ab5bad4
ms.sourcegitcommit: e2ef7231d3abaf3c925b0e5ee9f66156260e3c71
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/26/2020
ms.locfileid: "85383171"
---
# <a name="supported-sql-server-versions-for-configuration-manager"></a>Unterstützte SQL Server-Versionen für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Jeder Configuration Manager-Standort erfordert zum Hosten der Standortdatenbank eine unterstützte Version und Konfiguration von SQL Server.  

## <a name="sql-server-instances-and-locations"></a><a name="bkmk_Instances"></a> SQL Server-Instanzen und -Speicherorte

### <a name="central-administration-site-and-primary-sites"></a>Standort der zentralen Verwaltung und primäre Standorte

Die Standortdatenbank muss eine vollständige Installation von SQL Server verwenden.  

SQL Server kann auf den folgenden Computern installiert sein:  

- Standortservercomputer  
- Remotecomputer des Standortservers  

Die folgenden Instanzen werden unterstützt:  

- Standard- oder benannte Instanz von SQL Server  
- Konfigurationen mit mehreren Instanzen  
- SQL Server-Cluster Weitere Informationen finden Sie unter [Hosten der Standortdatenbank mit einem SQL Server-Cluster](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md).
- SQL Server Always On-Verfügbarkeitsgruppe. Weitere Informationen finden Sie unter [SQL Server Always On für eine hochverfügbare Standortdatenbank](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="secondary-sites"></a>Sekundäre Standorte

Die Standortdatenbank kann die Standardinstanz einer vollständigen Installation von SQL Server oder SQL Server Express verwenden.  

SQL Server muss auf dem Standortservercomputer installiert sein.  

### <a name="limitations-to-support"></a>Einschränkungen der Unterstützung

Die folgenden Konfigurationen werden nicht unterstützt:

- Ein SQL Server-Cluster in einer Clusterkonfiguration mit Netzwerklastenausgleich (Network Load Balancing, NLB)
- Ein SQL Server-Cluster in einem freigegebenen Clustervolume (Cluster Shared Volume, CSV)
- Technologien zur SQL Server-Datenbankspiegelung sowie Peer-to-Peer-Replikation

Die SQL Server-Transaktionsreplikation wird nur für das Replizieren von Objekten an Verwaltungspunkte unterstützt, die für die Verwendung von [Datenbankreplikaten](../../servers/deploy/configure/database-replicas-for-management-points.md) konfiguriert sind.  

## <a name="supported-versions-of-sql-server"></a><a name="bkmk_SQLVersions"></a> Unterstützte Versionen von SQL Server

In einer Hierarchie mit mehreren Standorten können verschiedene Standorte verschiedene SQL Server-Versionen zum Hosten der Standortdatenbank verwenden. Dies gilt jedoch nur, wenn folgende Voraussetzungen erfüllt sind:

- Configuration Manager unterstützt die von Ihnen verwendeten SQL Server-Versionen.
- Microsoft stellt weiterhin Support für die von Ihnen verwendeten SQL Server-Versionen bereit.
- SQL Server unterstützt Replikationen zwischen beiden SQL Server-Versionen. Weitere Informationen finden Sie unter [SQL Server replication backward compatibility](https://docs.microsoft.com/sql/relational-databases/replication/replication-backward-compatibility) (SQL Server – Abwärtskompatibilität bei Replikationen).

Bei SQL Server 2016 und früher folgt die Unterstützung für jede SQL-Version und jedes Service Pack der [Microsoft-Lebenszyklusrichtlinie](https://aka.ms/sqllifecycle). Der Support für ein bestimmtes Service Pack von SQL Server beinhaltet kumulative Updates, sofern diese nicht gegen die Abwärtskompatibilität für die Basisversion des Service Packs verstoßen. Ab SQL Server 2017 werden keine Service Packs mehr veröffentlicht, da diese Version einem [modernen Wartungsmodell](https://docs.microsoft.com/archive/blogs/sqlreleaseservices/announcing-the-modern-servicing-model-for-sql-server) folgt. Das SQL Server-Team empfiehlt eine fortlaufende, [proaktive Installation kumulativer Updates](https://docs.microsoft.com/archive/blogs/sqlreleaseservices/announcing-updates-to-the-sql-server-incremental-servicing-model-ism), sobald sie verfügbar werden.

Sofern nicht anders angegeben, werden die folgenden SQL Server-Versionen von allen aktiven Versionen von Configuration Manager-Versionen unterstützt. Beim Hinzufügen von Unterstützung für eine neue SQL Server-Version wird die Configuration Manager-Version angegeben, mit der diese Unterstützung hinzugefügt wird. Beachten Sie bei eingestelltem Support ebenfalls die Details zu den betroffenen Versionen von Configuration Manager.

> [!IMPORTANT]  
> Wenn Sie SQL Server Standard für die Datenbank am Standort der zentralen Verwaltung verwenden, ist die Gesamtanzahl der Clients begrenzt, die eine Hierarchie unterstützen kann. Informationen hierzu finden Sie unter [Size and scale numbers for System Center Configuration Manager](size-and-scale-numbers.md)(Anpassen und Skalieren von Zahlen für System Center Configuration Manager).

### <a name="sql-server-2019-standard-enterprise"></a>SQL Server 2019: Standard und Enterprise

Ab Configuration Manager Version 1910 können Sie diese Version mit dem kumulativen Update 5 (CU5) verwenden, sofern Ihre kumulative Updateversion vom SQL-Lebenszyklus unterstützt wird. CU5 ist die Mindestanforderung für SQL Server 2019, da es ein Problem mit [skalarem UDF-Inlining](https://docs.microsoft.com/sql/relational-databases/user-defined-functions/scalar-udf-inlining) behebt.

Diese SQL Server-Version kann für die folgenden Standorte verwendet werden:

- Ein Standort der zentralen Verwaltung
- Primären Standort
- Sekundären Standort

<!--
#### Known issue with SQL Server 2019

There's a known issue<!--6436234 with the new [scalar UDF inlining](https://docs.microsoft.com/sql/relational-databases/user-defined-functions/scalar-udf-inlining) feature in SQL 2019. To work around this issue and disable UDF lining, run the following script on the SQL 2019 server:

```sql
ALTER DATABASE SCOPED CONFIGURATION SET TSQL_SCALAR_UDF_INLINING = OFF  
```

While not always necessary, you may need to restart the SQL server after you run this script. For more information, see [Disabling Scalar UDF Inlining without changing the compatibility level](https://docs.microsoft.com/sql/relational-databases/user-defined-functions/scalar-udf-inlining?view=sql-server-ver15#disabling-scalar-udf-inlining-without-changing-the-compatibility-level).

You can safely disable this SQL feature for the site database server because Configuration Manager doesn't use it.

If you don't disable scalar UDF inlining in SQL 2019, the site server will randomly fail to query the site database. For example, you'll see the following errors in **hman.log**:

```hman.log
*** [HY000][0][Microsoft][SQL Server Native Client 11.0]Unspecified error occurred on SQL Server. Connection may have been terminated by the server.
*** select dbo.fnGetSiteMode(dbo.fnGetSiteCode())
*** [HY000][596][Microsoft][SQL Server Native Client 11.0][SQL Server]Cannot continue the execution because the session is in the kill state.
Failed to execute SQL command select dbo.fnGetSiteMode(dbo.fnGetSiteCode())
```

You may see similar errors in other logs, such as **SmsAdminUI.log**.

SQL Server version 2019 logs the following error:

`Microsoft SQL Server reported SQL message 596, severity 21: [HY000][596][Microsoft][SQL Server Native Client 11.0][SQL Server]Cannot continue the execution because the session is in the kill state.`

You'll also see crash dumps (`.mdump` files) from SQL in its log directory, which by default is `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Log`.
-->

### <a name="sql-server-2017-standard-enterprise"></a>SQL Server 2017: Standard und Enterprise

Sie können diese Version beim [kumulativen Update, Version 2 oder höher](https://support.microsoft.com/help/4052574), verwenden, solange Ihre kumulative Updateversion vom SQL-Lebenszyklus unterstützt wird. Diese SQL Server-Version kann für die folgenden Standorte verwendet werden:

- Ein Standort der zentralen Verwaltung  
- Primären Standort  
- Sekundären Standort  
  <!--SMS.498506-->

### <a name="sql-server-2016-standard-enterprise"></a>SQL Server 2016: Standard und Enterprise  
<!--514985-->
Sie können diese Version beim minimalen Service Pack und bei dem vom SQL-Lebenszyklus unterstützten kumulativen Update verwenden. Diese SQL Server-Version kann für die folgenden Standorte verwendet werden:

- Ein Standort der zentralen Verwaltung  
- Primären Standort  
- Sekundären Standort  

### <a name="sql-server-2014-standard-enterprise"></a>SQL Server 2014: Standard und Enterprise

Sie können diese Version beim minimalen Service Pack und bei dem vom SQL-Lebenszyklus unterstützten kumulativen Update verwenden. Diese SQL Server-Version kann für die folgenden Standorte verwendet werden:

- Ein Standort der zentralen Verwaltung  
- Primären Standort  
- Sekundären Standort

### <a name="sql-server-2012-standard-enterprise"></a>SQL Server 2012: Standard und Enterprise

Sie können diese Version beim minimalen Service Pack und bei dem vom SQL-Lebenszyklus unterstützten kumulativen Update verwenden. Diese SQL Server-Version kann für die folgenden Standorte verwendet werden:

- Ein Standort der zentralen Verwaltung  
- Primären Standort  
- Sekundären Standort  

### <a name="sql-server-2017-express"></a>SQL Server 2017 Express

Sie können diese Version beim [kumulativen Update, Version 2 oder höher](https://support.microsoft.com/help/4052574), verwenden, solange Ihre kumulative Updateversion vom SQL-Lebenszyklus unterstützt wird. Diese SQL Server-Version kann für die folgenden Standorte verwendet werden:

- Sekundären Standort
<!--SMS.498506-->

### <a name="sql-server-2016-express"></a>SQL Server 2016 Express

Sie können diese Version beim minimalen Service Pack und bei dem vom SQL-Lebenszyklus unterstützten kumulativen Update verwenden. Diese SQL Server-Version kann für die folgenden Standorte verwendet werden:

- Sekundären Standort

### <a name="sql-server-2014-express"></a>SQL Server 2014 Express

Sie können diese Version beim minimalen Service Pack und bei dem vom SQL-Lebenszyklus unterstützten kumulativen Update verwenden. Diese SQL Server-Version kann für die folgenden Standorte verwendet werden:

- Sekundären Standort  

### <a name="sql-server-2012-express"></a>SQL Server 2012 Express

Sie können diese Version beim minimalen Service Pack und bei dem vom SQL-Lebenszyklus unterstützten kumulativen Update verwenden. Diese SQL Server-Version kann für die folgenden Standorte verwendet werden:

- Sekundären Standort  

## <a name="required-configurations-for-sql-server"></a><a name="bkmk_SQLConfig"></a> Erforderliche Konfigurationen für SQL Server

Die folgenden Konfigurationen sind für alle Installationen von SQL Server erforderlich, die Sie für eine Standortdatenbank verwenden (einschließlich SQL Server Express). Wenn SQL Server Express von Configuration Manager als Teil einer Installation eines sekundären Standorts installiert wird, werden diese Konfigurationen automatisch erstellt.  

### <a name="sql-server-architecture-version"></a>Version der SQL Server-Architektur

Configuration Manager erfordert eine 64-Bit-Version von SQL Server, um die Standortdatenbank zu hosten.  

### <a name="database-collation"></a>Datenbanksortierung

An jedem Standort muss sowohl die für den Standort als auch die für die Standortdatenbank verwendete Instanz von SQL Server die folgende Sortierung verwenden: **SQL_Latin1_General_CP1_CI_AS**.  

Configuration Manager unterstützt für den Standard China GB18030 zwei Ausnahmen von dieser Sortierung. Weitere Informationen finden Sie unter [Internationale Unterstützung](../hierarchy/international-support.md).  

### <a name="database-compatibility-level"></a>Kompatibilitätsgrad der Datenbank

Configuration Manager erfordert, dass der Kompatibilitätsgrad für die Standortdatenbank nicht kleiner als die niedrigste unterstützte SQL Server-Version für Ihre Configuration Manager-Version ist. Zum Beispiel benötigen Sie ab Version 1702 einen [Datenbank-Kompatibilitätsgrad](https://docs.microsoft.com/sql/relational-databases/databases/view-or-change-the-compatibility-level-of-a-database), der größer als oder gleich 110 ist. <!-- SMS.506266-->

### <a name="sql-server-features"></a>SQL Server-Funktionen

Nur die Funktion **Datenbank-Engine-Dienste** ist für jeden Standortserver erforderlich.  

Für die Configuration Manager-Datenbankreplikation ist die Funktion **SQL Server-Replikation** nicht erforderlich. Diese SQL Server-Konfiguration ist jedoch erforderlich, wenn Sie [Datenbankreplikate für Verwaltungspunkte](../../servers/deploy/configure/database-replicas-for-management-points.md) verwenden.  

### <a name="windows-authentication"></a>Windows-Authentifizierung

Configuration Manager setzt die **Windows-Authentifizierung** zur Überprüfung von Verbindungen mit der Datenbank voraus.  

### <a name="sql-server-instance"></a>SQL Server-Instanz

Verwenden Sie für jeden Standort eine dedizierte Instanz von SQL Server. Die Instanz kann entweder eine **benannte Instanz** oder eine **Standardinstanz** darstellen.  

### <a name="sql-server-memory"></a>SQL Server-Arbeitsspeicher

Reservieren Sie mithilfe von SQL Server Management Studio Arbeitsspeicher für SQL Server. Legen Sie die Einstellung **Minimaler Serverspeicher** unter **Arbeitsspeicheroptionen für den Server** fest. Weitere Informationen zum Konfigurieren dieser Einstellung finden Sie unter [Serverkonfigurationsoptionen für den Serverarbeitsspeicher](https://docs.microsoft.com/sql/database-engine/configure-windows/server-memory-server-configuration-options).  

- **Für einen Datenbankserver, der auf demselben Computer wie der Standortserver installiert ist**: Begrenzen Sie den Arbeitsspeicher für SQL Server auf 50 bis 80 Prozent des verfügbaren adressierbaren Systemspeichers.  

- **Für einen dedizierten Datenbankserver (remote vom Standortserver)** : Begrenzen Sie den Arbeitsspeicher für SQL Server auf 80 bis 90 Prozent des verfügbaren adressierbaren Systemspeichers.  

- **Für eine Arbeitsspeicherreserve für den Pufferpool jeder verwendeten SQL Server-Instanz**:  

  - Für einen Standort der zentralen Verwaltung: Legen Sie mindestens 8 GB fest.  
  - Für einen primären Standort: Legen Sie mindestens 8 GB fest.  
  - Für einen sekundären Standort: Legen Sie mindestens 4 GB fest.  

### <a name="sql-nested-triggers"></a>Geschachtelte SQL-Trigger

Geschachtelte SQL-Trigger müssen aktiviert sein. Weitere Informationen finden Sie unter [Konfigurieren der Serverkonfigurationsoption „Geschachtelte Trigger“](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option).

### <a name="sql-server-clr-integration"></a>SQL Server-CLR-Integration

Die Standortdatenbank erfordert, dass die CLR (Common Language Runtime) von SQL Server aktiviert ist. Diese Option wird bei der Installation von Configuration Manager automatisch aktiviert. Weitere Informationen zur CLR finden Sie unter [Einführung in die CLR-Integration für SQL Server](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration).  

### <a name="sql-server-service-broker-ssb"></a>SQL Server Service Broker (SSB)

Der SQL Server Service Broker ist sowohl für die standortübergreifende Replikation als auch für einen einzelnen primären Standort erforderlich.

### <a name="trustworthy-setting"></a>Einstellung für VERTRAUENSWÜRDIG

Configuration Manager aktiviert automatisch die [SQL-Datenbankeigenschaft VERTRAUENSWÜRDIG](https://docs.microsoft.com/sql/relational-databases/security/trustworthy-database-property). Diese Eigenschaft muss für Configuration Manager auf **ON** festgelegt sein.

## <a name="optional-configurations-for-sql-server"></a><a name="bkmk_optional"></a> Optionale Konfigurationen für SQL Server

Die folgenden Konfigurationen sind für jede Datenbank optional, die eine vollständige SQL Server-Installation verwendet.  

### <a name="sql-server-service"></a>SQL Server-Dienst

Sie können den SQL Server-Dienst für die Ausführung mit den folgenden Konten konfigurieren:  

- Ein *Domänenbenutzerkonto mit geringen Rechten*:  

  - Diese Konfiguration ist eine bewährte Methode und erfordert möglicherweise die manuelle Registrierung des Dienstprinzipalnamens (Service Principal Name, SPN) für das Konto.  

- Konto **Lokales System** des Computers, auf dem SQL Server ausgeführt wird:  

  - Verwenden Sie das lokale Systemkonto, um den Konfigurationsvorgang zu vereinfachen.  
  - Wenn Sie das lokale Systemkonto verwenden, wird der SPN von Configuration Manager automatisch für den SQL Server-Dienst registriert.  
  - Die Verwendung des lokalen Systemkontos für den SQL Server-Dienst ist keine bewährte Methode für SQL Server.  

Wenn der Computer, auf dem SQL Server ausgeführt wird, nicht das zugehörige lokale Systemkonto zum Ausführen des SQL Server-Diensts verwendet, konfigurieren Sie den SPN des Kontos, unter dem SQL Server-Dienste ausgeführt werden, in den Active Directory Domain Services. (Bei Verwendung des Systemkontos wird der SPN automatisch für Sie registriert.)

Weitere Informationen zu SPNs für die Standortdatenbank finden Sie unter [Verwalten des SPN für den Standortdatenbankserver](../../servers/manage/modify-your-infrastructure.md#bkmk_SPN).  

Informationen zum Ändern des vom SQL Server-Dienst verwendeten Kontos finden Sie unter [SCM-Dienste: Ändern des Dienststartkontos](https://docs.microsoft.com/sql/database-engine/configure-windows/scm-services-change-the-service-startup-account).  

### <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

SQL Server Reporting Services sind Voraussetzung für die Installation eines Reporting Services-Punkts, mit dem Sie Berichte ausführen können. Configuration Manager unterstützt die gleichen Versionen von SQL Server für die Berichterstattung wie für die Standortdatenbank.

Weitere Informationen finden Sie unter [Voraussetzungen für die Berichterstattung in Configuration Manager](../../servers/manage/prerequisites-for-reporting.md).

> [!IMPORTANT]  
> Nach dem Upgrade von SQL Server von einer früheren Version wird möglicherweise der folgende Fehler angezeigt: *Report Builder Does Not Exist* (Berichts-Generator nicht vorhanden).  
> Zum Beheben dieses Fehlers müssen Sie die Reporting Services-Standortsystemrolle neu installieren.  

### <a name="data-warehouse-service-point"></a>Data Warehouse-Dienstpunkt

Das Data Warehouse verwendet eine separate Datenbank. Sie können diese auf dem Standortdatenbankserver oder einer separaten SQL Server-Instanz hosten. Weitere Informationen finden Sie unter [Der Data Warehouse-Dienstpunkt für Configuration Manager](../../servers/manage/data-warehouse.md).

### <a name="sql-server-ports"></a>SQL Server-Ports

Für die Kommunikation mit der SQL Server-Datenbank-Engine und die standortübergreifende Replikation können Sie die Standardkonfigurationen für SQL Server-Ports verwenden oder benutzerdefinierte Ports angeben:  

- Die **standortübergreifende Kommunikation** erfolgt über den SQL Server Service Broker, der standardmäßig TCP-Port 4022 verwendet.  
- Die **standortinterne Kommunikation** zwischen der SQL Server-Datenbank-Engine und verschiedenen Configuration Manager-Standortsystemrollen erfolgt standardmäßig über den TCP-Port 1433. Die folgenden Standortsystemrollen kommunizieren direkt mit der SQL Server-Datenbank:  

  - Verwaltungspunkt  
  - SMS-Anbietercomputer  
  - Reporting Services-Punkt  
  - Standortserver  

Wenn ein Computer, auf dem SQL Server ausgeführt wird, Datenbanken von mehreren Standorten hostet, muss jede Datenbank eine separate SQL Server-Instanz verwenden. Außerdem muss jede dieser Instanzen mit einem eindeutigen Portsatz konfiguriert sein.  

> [!WARNING]  
> Dynamische Ports werden von Configuration Manager nicht unterstützt. Da von benannten SQL Server-Instanzen standardmäßig dynamische Ports für die Verbindung mit der Datenbank-Engine verwendet werden, müssen Sie bei der Verwendung einer benannten Instanz den statischen Port, den Sie für die standortinterne Kommunikation einsetzen möchten, manuell konfigurieren.  

Wenn auf dem Computer, auf dem SQL Server ausgeführt wird, eine Firewall aktiviert ist, achten Sie darauf, dass die von Ihrer Bereitstellung verwendeten Ports von der Firewall überall im Netzwerk zwischen Computern zugelassen werden, die mit SQL Server kommunizieren.  

Ein Beispiel zum Konfigurieren von SQL Server für die Verwendung eines bestimmten Ports finden Sie unter [Konfigurieren eines Servers für das Überwachen eines bestimmten TCP-Ports](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port).  

## <a name="upgrade-options-for-sql-server"></a>Upgradeoptionen für SQL Server

Wenn Sie ein Upgrade für Ihre Version von SQL Server durchführen müssen, verwenden Sie eine der folgenden Methoden (angegeben in der Reihenfolge ihrer Komplexität):  

- [Direktes Upgrade von SQL Server](../../servers/manage/upgrade-on-premises-infrastructure.md#to-upgrade-sql-server-on-the-site-database-server) (empfohlen).  

- Installieren Sie eine neue Version von SQL Server auf einem neuen Computer, und [verwenden Sie die Option „Datenbankverschiebung“](../../servers/manage/modify-your-infrastructure.md#bkmk_dbconfig) im Configuration Manager-Setup, um Ihren Standortserver auf die neue SQL Server-Version auszurichten.  

- Verwenden Sie [Sicherung und Wiederherstellung](../../servers/manage/backup-and-recovery.md). Die Sicherung und Wiederherstellung für ein SQL-Upgradeszenario wird unterstützt. Bei den [Überlegungen vor dem Wiederherstellen eines Standorts](../../servers/manage/recover-sites.md#considerations-before-recovering-a-site) können Sie die Anforderung an die SQL-Versionsverwaltung ignorieren.
