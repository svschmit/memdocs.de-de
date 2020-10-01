---
title: Aktualisieren der lokalen Infrastruktur
titleSuffix: Configuration Manager
description: Hier erfahren Sie, wie für eine Infrastruktur wie etwa SQL Server und das Betriebssystem von Standortsystemen ein Upgrade durchgeführt wird.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8ca970dd-e71c-404f-9435-d36e773a0db2
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0c2894bcdf80901171cceba96e7829793f899383
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606788"
---
# <a name="upgrade-on-premises-infrastructure-that-supports-configuration-manager"></a>Upgraden der lokalen Infrastruktur, die Configuration Manager unterstützt

*Gilt für: Configuration Manager (Current Branch)*

Verwenden Sie die Informationen in diesem Artikel, um die Serverinfrastruktur zu aktualisieren, in der Configuration Manager ausgeführt wird.  

- Informationen über das *Upgrade* von einer früheren Version von Configuration Manager (aktueller Branch) finden Sie unter [Upgrade auf Configuration Manager](../deploy/install/upgrade-to-configuration-manager.md).  

- Wenn Sie Ihre Infrastruktur von Configuration Manager (aktueller Branch) auf eine neue Version *aktualisieren* möchten, lesen Sie [Updates für Configuration Manager](updates.md).  


## <a name="upgrade-the-os-of-site-systems"></a><a name="BKMK_SupConfigUpgradeSiteSrv"></a> Upgrade des Betriebssystems der Standortsysteme  

Configuration Manager unterstützt in folgenden Situationen das direkte Upgrade des Betriebssystems des Servers, auf dem ein Standortserver und Standortsystemrollen gehostet werden:  

- Sofern das Windows-Service Pack von Configuration Manager weiterhin unterstützt wird, wird ein direktes Upgrade auf ein höheres Windows Server-Service Pack unterstützt.  

- Direktes Upgrade von:  

    - Windows Server 2016 auf Windows Server 2019  

    - Windows Server 2012 R2 auf Windows Server 2019  

    - Windows Server 2012 R2 auf Windows Server 2016  

    - Windows Server 2012 auf Windows Server 2016  

    - Windows Server 2012 auf Windows Server 2012 R2  

    - Windows Server 2008 R2 auf Windows Server 2012 R2  

Verwenden Sie für das Upgrade eines Servers die Upgradeverfahren, die von dem Betriebssystem bereitgestellt werden, auf das aktualisiert werden soll. Weitere Informationen finden Sie in den folgenden Artikeln:  

- [Windows Server Upgrade Center](https://aka.ms/upgradecenter)  

- [Upgrade and conversion options for Windows Server 2016 (Upgrade- und Konvertierungsoptionen für Windows Server 2016)](/windows-server/get-started/supported-upgrade-paths)  

- [Upgrade Options for Windows Server 2012 R2 (Upgradeoptionen für Windows Server 2012 R2)](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn303416(v=ws.11))  

### <a name="upgrade-to-windows-server-2016-or-2019"></a><a name="bkmk_2016-2019"></a> Upgrade auf Windows Server 2016 oder 2019

Die Schritte in diesem Abschnitt sind für die folgenden Szenarios relevant:  

- Upgrade von Windows Server 2012 R2 oder Windows Server 2016 auf Windows Server 2019  

- Upgrade von Windows Server 2012 oder Windows Server 2012 R2 auf Windows Server 2016  

#### <a name="before-upgrade"></a>Vor dem Upgrade

- (Windows Server 2012 oder Windows Server 2012 R2): Entfernen Sie den SCEP-Client (System Center Endpoint Protection). In Windows Server ist jetzt Windows Defender integriert, sodass der SCEP-Client nicht mehr erforderlich ist. Durch das Vorhandensein des SCEP-Clients wird ein Upgrade auf Windows Server möglicherweise verhindert.  

- Entfernen Sie die WSUS-Rolle vom Server, sofern sie installiert ist. Sie können die SUSDB beibehalten und erneut anfügen, sobald WSUS neu installiert wurde.  

- Wenn Sie das Betriebssystem des Standortservers aktualisieren, stellen Sie sicher, dass die [dateibasierte Replikation](../../plan-design/hierarchy/file-based-replication.md) für den Standort fehlerfrei ist. Überprüfen Sie alle Postfächer sowohl für sendende als auch für empfangende Standorte auf einen Rückstand. Wenn eine Vielzahl an blockierten oder ausstehenden Replikationsaufträgen vorhanden ist, warten Sie, bis sie abgebaut wurden.<!-- SCCMDocs#1792 -->
    - Überprüfen Sie für den sendenden Standort **sender.log**.
    - Überprüfen Sie für den empfangenden Standort **despooler.log**.

#### <a name="after-upgrade"></a>Nach dem Upgrade

- Stellen Sie sicher, dass Windows Defender aktiviert ist, automatisch gestartet wird und ausgeführt wird.  

- Stellen Sie sicher, dass die folgenden Configuration Manager-Dienste ausgeführt werden:  

    - SMS_EXECUTIVE  

    - SMS_SITE_COMPONENT_MANAGER  

- Stellen Sie sicher, dass der **Windows-Prozessaktivierungsdienst** und **WWW/W3SVC** aktiviert sind und automatisch gestartet werden. Der Upgradeprozess deaktiviert diese Dienste, also stellen Sie sicher, dass sie für die folgenden Standortsystemrollen ausgeführt werden:  

    - Standortserver  

    - Verwaltungspunkt  

    - Anwendungskatalog-Webdienstpunkt  

    - Anwendungskatalog-Websitepunkt  

- Stellen Sie sicher, dass jeder Server, der eine Standortsystemrolle hostet, weiterhin die [Voraussetzungen](../../plan-design/configs/site-and-site-system-prerequisites.md) erfüllt. Möglicherweise müssen Sie BITS oder WSUS neu installieren oder bestimmte Einstellungen für IIS konfigurieren.  

- Nachdem Sie alle erforderlichen Komponenten wiederhergestellt haben, starten Sie den Server erneut, um sicherzustellen, dass alle Dienste gestartet wurden und funktionsfähig sind.  

- Führen Sie beim Aktualisieren des primären Standortservers eine [Standortrücksetzung](modify-your-infrastructure.md#bkmk_reset) durch.  

#### <a name="known-issue-for-remote-configuration-manager-consoles"></a>Bekanntes Problem für die Configuration Manager-Remotekonsole

Nachdem Sie ein Upgrade für den Standortserver oder eine Instanz des SMS-Anbieters durchgeführt haben, können Sie keine Verbindung mehr zur Configuration Manager-Konsole herstellen. Stellen Sie Berechtigungen für die **SMS-Administratorengruppe** in WMI manuell wieder her, um dieses Problem zu umgehen. Berechtigungen müssen auf dem Standortserver sowie auf allen Remoteservern, auf denen eine Instanz des SMS-Anbieters gehostet wird, festgelegt werden:

1. Öffnen Sie auf den entsprechenden Servern die Microsoft Management Console (MMC), fügen Sie das Snap-In für die **WMI-Steuerung** hinzu, und wählen Sie dann **Lokaler Computer** aus.  

2. Öffnen Sie in der MMC die **Eigenschaften** von **WMI-Steuerung (Lokal)** , und wählen Sie die Registerkarte **Sicherheit** aus.  

3. Erweitern Sie die Struktur unter dem Stamm, wählen Sie den Knoten **SMS** aus, und wählen Sie dann **Sicherheit**.  Stellen Sie sicher, dass die Gruppe **SMS-Administratoren** über folgende Berechtigungen verfügt:  

    - Konto aktivieren  

    - Remoteaktivierung  

4. Wählen Sie auf der Registerkarte **Sicherheit** unter dem Knoten **SMS** den Knoten **Standort_&lt;Standortcode**> und anschließend **Sicherheit** aus. Stellen Sie sicher, dass die Gruppe **SMS-Administratoren** über folgende Berechtigungen verfügt:  

    - Methoden ausführen  

    - Anbieterschreibzugriff  

    - Konto aktivieren  

    - Remoteaktivierung  

5. Speichern Sie die Berechtigungen, um den Zugriff für die Configuration Manager-Konsole wiederherzustellen.  

#### <a name="known-issue-for-remote-site-systems"></a>Bekanntes Problem bei Standortsystemen

Nachdem Sie ein Upgrade auf einen Server durchgeführt haben, der eine Standortsystemrolle hostet, fehlt der Wert `Software\Microsoft\SMS` möglicherweise im folgenden Registrierungsschlüssel: `HKLM\SYSTEM\CurrentControlSet\Control\SecurePipeServers\Winreg\AllowedPaths`

Wenn dieser Wert nach dem Windows-Upgrade auf dem Server fehlt, fügen Sie ihn manuell hinzu. Andernfalls können Standortsystemrollen Probleme haben, Dateien in die Postfächer der Standortserver hochzuladen.

### <a name="upgrade-to-windows-server-2012-r2"></a><a name="bkmk_2012r2"></a> Upgrade auf Windows Server 2012 R2

Wenn Sie Windows Server 2008 R2 oder Windows Server 2012 auf Windows Server 2012 R2 aktualisieren, gelten folgende Bedingungen:

#### <a name="before-upgrade"></a>Vor dem Upgrade

- Auf Windows Server 2012: Entfernen Sie die WSUS-Rolle vom Server, sofern sie installiert ist. Sie können die SUSDB beibehalten und erneut anfügen, sobald WSUS neu installiert wurde.  

- Auf Windows Server 2008 R2: Vor dem Upgrade auf Windows Server 2012 R2 müssen Sie WSUS 3.2 vom Server deinstallieren. Sie können die SUSDB beibehalten und erneut anfügen, sobald WSUS neu installiert wurde. Weitere Informationen finden Sie in der [Übersicht zu Windows Server Update Services](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh852345(v=ws.11)#new-and-changed-functionality).  

- Wenn Sie das Betriebssystem des Standortservers aktualisieren, stellen Sie sicher, dass die [dateibasierte Replikation](../../plan-design/hierarchy/file-based-replication.md) für den Standort fehlerfrei ist. Überprüfen Sie alle Postfächer sowohl für sendende als auch für empfangende Standorte auf einen Rückstand. Wenn eine Vielzahl an blockierten oder ausstehenden Replikationsaufträgen vorhanden ist, warten Sie, bis sie abgebaut wurden.<!-- SCCMDocs#1792 -->
    - Überprüfen Sie für den sendenden Standort **sender.log**.
    - Überprüfen Sie für den empfangenden Standort **despooler.log**.

#### <a name="after-upgrade"></a>Nach dem Upgrade

- Der Upgradeprozess deaktiviert die Windows-Bereitstellungsdienste. Achten Sie darauf, dass der Dienst für die folgenden Standortsystemrollen gestartet wurde und ausgeführt wird:  

    - Standortserver  

    - Verwaltungspunkt  

    - Anwendungskatalog-Webdienstpunkt  

    - Anwendungskatalog-Websitepunkt  

- Stellen Sie sicher, dass der **Windows-Prozessaktivierungsdienst** und **WWW/W3SVC** aktiviert sind und automatisch gestartet werden. Der Upgradeprozess deaktiviert diese Dienste, also stellen Sie sicher, dass sie für die folgenden Standortsystemrollen ausgeführt werden:  

    - Standortserver  

    - Verwaltungspunkt  

    - Anwendungskatalog-Webdienstpunkt  

    - Anwendungskatalog-Websitepunkt  

- Stellen Sie sicher, dass jeder Server, der eine Standortsystemrolle hostet, weiterhin die [Voraussetzungen](../../plan-design/configs/site-and-site-system-prerequisites.md) erfüllt. Möglicherweise müssen Sie BITS oder WSUS neu installieren oder bestimmte Einstellungen für IIS konfigurieren.  

    Nachdem Sie alle erforderlichen Komponenten wiederhergestellt haben, starten Sie den Server erneut, um sicherzustellen, dass alle Dienste gestartet wurden und funktionsfähig sind.  

### <a name="unsupported-upgrade-scenarios"></a>Nicht unterstützte Upgradeszenarios

Die folgenden Windows Server-Upgradeszenarios werden zwar häufig angefragt, werden aber von Configuration Manager nicht unterstützt:  

- Windows Server 2008 auf Windows Server 2012 oder höher  

- Windows Server 2008 R2 auf Windows Server 2012  


## <a name="upgrade-the-os-of-clients"></a><a name="BKMK_SupConfigUpgradeClient"></a> Upgrade des Betriebssystems von Clients  

Configuration Manager unterstützt in den folgenden Situationen ein direktes Upgrade für das Betriebssystem von Configuration Manager-Clients:  

- Sofern das Service Pack von Configuration Manager unterstützt wird, wird ein direktes Upgrade auf ein höheres Windows-Service Pack unterstützt.  

- Direktes Windows-Upgrade von einer unterstützten Version auf Windows 10. Weitere Informationen finden Sie unter [Aktualisieren von Windows auf die neueste Version](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

- Windows 10-Dienstupgrades von Build zu Build. Weitere Informationen finden Sie unter [Manage Windows as a service (Verwalten von Windows as a Service)](../../../osd/deploy-use/manage-windows-as-a-service.md).  


## <a name="upgrade-sql-server"></a><a name="BKMK_SupConfigUpgradeDBSrv"></a> Upgrade von SQL Server  

Configuration Manager unterstützt ein direktes Upgrade von SQL Server auf dem Standortdatenbankserver.

Weitere Informationen über SQL Server-Versionen, die von Configuration Manager unterstützt werden, finden Sie unter [Unterstützung für SQL Server-Versionen](../../plan-design/configs/support-for-sql-server-versions.md).  

### <a name="upgrade-the-service-pack-version-of-sql-server"></a>Upgrade Service Pack-Version von SQL Server

Sofern das SQL Server-Service Pack von Configuration Manager weiterhin unterstützt wird, wird ein direktes Upgrade von SQL Server auf ein höheres Service Pack unterstützt.

Wenn Sie über mehr als einen Configuration Manager-Standort in einer Hierarchie verfügen, kann an jedem Standort eine andere Service Pack-Version von SQL Server ausgeführt werden. Es gibt keine Beschränkung für die Reihenfolge, in der Standorte die Service Pack-Version von SQL Server aktualisieren.

### <a name="upgrade-to-a-new-version-of-sql-server"></a>Upgrade auf eine neue Version von SQL Server

Configuration Manager unterstützt das direkte Upgrade von SQL Server auf die folgenden Versionen:

- SQL Server 2019  

- SQL Server 2017  

- SQL Server 2016  

- SQL Server 2014  

Dies umfasst das Upgrade von SQL Server Express auf eine neuere Version von SQL Server Express an sekundären Standorten.

Wenn Sie für die Version von SQL Server, unter der die Standortdatenbank gehostet wird, ein Upgrade ausführen, müssen Sie die verwendete SQL Server-Version in der folgenden Reihenfolge an den Standorten aktualisieren:

1. Aktualisieren Sie SQL Server zunächst am Standort der zentralen Verwaltung.  

2. Aktualisieren Sie sekundäre Standorte zuerst, bevor Sie übergeordnete primäre Standorte der sekundären Standorte aktualisieren.  

3. Aktualisieren Sie übergeordnete primäre Standorte zuletzt. Zu diesen Standorten gehören sowohl untergeordnete primäre Standorte, die einem Standort der zentralen Verwaltung unterstellt sind, als auch eigenständige primäre Standorte, die den Standort der obersten Ebene einer Hierarchie darstellen.  

### <a name="sql-server-cardinality-estimation-level"></a>SQL Server-Kardinalitätsschätzungsgrad

Wenn Sie eine Standortdatenbank von einer früheren Version von SQL Server aktualisieren, behält die Datenbank den vorhandenen SQL-Kardinalitätsschätzungsgrad (CE-Grad), wenn dieser dem Minimum entspricht, der für diese Instanz von SQL Server zulässig ist. Wenn SQL Server mit einer Datenbank aktualisiert wird, deren Kompatibilitätsgrad niedriger ist als der zulässige Grad, wird die Datenbank automatisch auf den niedrigsten Kompatibilitätsgrad gesetzt, der in SQL Server zulässig ist.

Die folgende Tabelle zeigt die empfohlenen Kompatibilitätsgrade für Standortdatenbanken von Configuration Manager:

|SQL Server-Version | Unterstützte Kompatibilitätsgrade | Empfohlener Grad |
|----------------|--------------------|--------|
| SQL Server 2017 | 140, 130, 120, 110  | 140 |
| SQL Server 2016 | 130, 120, 110  | 130 |
| SQL Server 2014 | 120, 110      | 110 |

Führen Sie die folgende SQL-Abfrage auf dem Standortdatenbankserver aus, um den SQL Server-CE-Kompatibilitätsgrad zu ermitteln, der für Ihre Standortdatenbank verwendet wird:  

```SQL
SELECT name, compatibility_level FROM sys.databases
```

Weitere Informationen zu SQL-CE-Kompatibilitätsgraden und deren Festlegung finden Sie unter [ALTER DATABASE-Kompatibilitätsgrad (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).

Weitere Informationen zum Upgrade von SQL Server finden Sie in den folgenden SQL Server-Artikeln:  

- [Upgrade auf SQL Server 2017](/sql/database-engine/install-windows/supported-version-and-edition-upgrades-2017)  

- [Upgrade auf SQL Server 2016](/sql/database-engine/install-windows/supported-version-and-edition-upgrades)  

- [Upgrade auf SQL Server 2014](/sql/database-engine/install-windows/supported-version-and-edition-upgrades)  

### <a name="to-upgrade-sql-server-on-the-site-database-server"></a>So führen Sie ein SQL Server-Upgrade auf dem Standortdatenbankserver aus  

1. Beenden Sie alle Configuration Manager-Dienste am Standort.  

2. Führen Sie für SQL Server ein Upgrade auf eine unterstützte Version aus.  

3. Starten Sie die Configuration Manager-Dienste neu.  

> [!NOTE]  
> Wenn Sie die SQL Server-Edition des Standorts der zentralen Verwaltung von Standard in eine Datenbank oder Enterprise ändern, ändert sich die Datenbankpartition nicht. Diese Datenbankpartition schränkt die Anzahl der Clients ein, die von der Datenbank unterstützt werden.
