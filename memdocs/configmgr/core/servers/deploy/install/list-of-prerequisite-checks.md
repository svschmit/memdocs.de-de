---
title: Voraussetzungsprüfungen
titleSuffix: Configuration Manager
description: Referenz zu einzelnen Voraussetzungsprüfungen für Updates von Configuration Manager.
ms.date: 05/07/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6a279624-ffc9-41aa-8132-df1809708dd5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5bdf2adbf4ba5f02869ba5058da84ee7738e0ce2
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89608070"
---
# <a name="list-of-prerequisite-checks-for-configuration-manager"></a>Liste mit Voraussetzungsprüfungen für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

In diesem Artikel werden die Voraussetzungsprüfungen beschrieben, die durchgeführt werden, wenn Sie Configuration Manager installieren oder aktualisieren. Weitere Informationen finden Sie unter [Voraussetzungsprüfungen](prerequisite-checker.md).  



## <a name="errors"></a>Fehler

### <a name="active-migration-mappings-on-the-target-primary-site"></a>Am primären Zielstandort sind aktive Migrationszuordnungen vorhanden

*Gilt für: Standort der zentralen Verwaltung*

Am primären Zielstandort sind aktive Migrationszuordnungen vorhanden.

### <a name="active-replica-mp"></a>Aktives MP-Replikat

*Gilt für: Primären Standort*

Es gibt ein aktives Verwaltungspunktreplikat.

### <a name="administrative-rights-on-expand-primary-site"></a>Administratorrechte für den erweiterten primären Standort

*Gilt für: Standort der zentralen Verwaltung*

Wenn Sie einen primären Standort zu einer Hierarchie erweitern, verfügt das Benutzerkonto, das das Setup ausführt, beim Server des eigenständigen primären Standort über **Administratorrechte**.

### <a name="administrative-rights-on-site-system"></a>Administratorrechte für das Standortsystem

*Gilt für: Standort der zentralen Verwaltung, primären Standort und sekundären Standort*

Das Benutzerkonto, über das das Configuration Manager-Setup ausgeführt wird, verfügt auf dem Standortserver über **Administratorrechte**.

### <a name="administrator-rights-on-central-administration-site"></a>Administratorrechte für Standort der zentralen Verwaltung

*Gilt für: Primären Standort*

Das Benutzerkonto, über das das Configuration Manager-Setup ausgeführt wird, verfügt am Standort der zentralen Verwaltung über **Administratorrechte**.

### <a name="asset-intelligence-synchronization-point-on-the-expanded-primary-site"></a>Asset Intelligence-Synchronisierungspunkt auf dem erweiterten primären Standort

*Gilt für: Standort der zentralen Verwaltung*

Wenn Sie einen primären Standort zu einer Hierarchie erweitern wird die Asset Intelligence-Synchronisierungspunktrolle auf dem eigenständigen primären Standort nicht installiert.

### <a name="bits-enabled"></a>BITS aktiviert

*Gilt für: Verwaltungspunkt*

Der BITS (Background Intelligent Transfer Service) ist auf dem Verwaltungspunkt installiert. Dies Prüfung kann aus den folgenden Gründen fehlschlagen:

- Der BITS ist nicht installiert  

- Die IIS 6.0-WMI-Kompatibilitätskomponente für IIS 7.0 ist auf dem Server oder dem IIS-Remotehost nicht installiert.  

- Das Setup könnte die IIS-Remoteeinstellungen nicht überprüfen. Gängige IIS-Komponenten sind auf dem Standortserver nicht installiert.  

### <a name="case-insensitive-collation-on-sql-server"></a>Sortierung ohne Beachtung der Groß-/Kleinschreibung bei SQL Server

*Gilt für: Standortdatenbankserver*

Die SQL Server-Installation verwendet eine Sortierung ohne Beachtung der Groß-/Kleinschreibung (Beispiel: **SQL_Latin1_General_CP1_CI_AS**).

### <a name="central-administration-site-server-administrative-rights-on-expand-primary-site"></a>Administratorrechte für den Standort der zentralen Verwaltung beim Erweitern eines primären Standorts

*Gilt für: Standort der zentralen Verwaltung*

Wenn Sie einen primären Standort zu einer Hierarchie erweitern, verfügt das Computerkonto des Standorts der zentralen Verwaltung beim Server des eigenständigen primären Standort über **Administratorrechte**.

### <a name="client-version-on-management-point-computer"></a>Clientversion auf Verwaltungspunktcomputer

*Gilt für: Verwaltungspunkt*

Sie installieren den Verwaltungspunkt auf einem Server, auf dem keine andere Version des Configuration Manager-Clients installiert ist.

### <a name="cloud-management-gateway-on-the-expanded-primary-site"></a>Nicht unterstützte Cloud Management Gateway-Rolle am erweiterten primären Standort

*Gilt für: Standort der zentralen Verwaltung*

Wenn Sie einen primären Standort auf eine Hierarchie erweitern, wird die Rolle „ Cloud Management Gateway“ nicht auf dem eigenständigen primären Standort installiert.

### <a name="connection-to-sql-server-on-central-administration-site"></a>Verbindung zu SQL Server am Standort der zentralen Verwaltung

*Gilt für: Primären Standort*

Das Benutzerkonto, das das Configuration Manager-Setup am primären Standort ausführt, verfügt über die Rolle **sysadmin** auf der SQL Server-Instanz für den Standort der zentralen Verwaltung, um einer bereits vorhandenen Hierarchie beizutreten.

### <a name="custom-client-agent-settings-have-nap-enabled"></a>Netzwerkzugriffsschutz für benutzerdefinierte Client-Agent-Einstellungen aktiviert

*Gilt für: Standort der zentralen Verwaltung, primären Standort*

Es gibt keine benutzerdefinierten Clienteinstellungen, die den Netzwerkzugriffsschutz (Network Access Protection, NAP) aktivieren.

### <a name="data-warehouse-service-point-on-the-expanded-primary-site"></a>Data Warehouse-Dienstpunkt für den erweiterten primären Standort

*Gilt für: Standort der zentralen Verwaltung*

Wenn Sie einen primären Standort auf eine Hierarchie erweitern, wird die Rolle des Data Warehouse-Dienstpunkts nicht auf dem eigenständigen primären Standort installiert.

### <a name="dedicated-sql-server-instance"></a>Dedizierte SQL Server-Instanz

*Gilt für: Standort der zentralen Verwaltung, primären Standort und sekundären Standort*

Sie haben eine dedizierte SQL Server-Instanz zum Hosten der Configuration Manager-Standortdatenbank konfiguriert.

Wenn die Instanz von einem anderen Standort verwendet wird, müssen Sie eine andere Instanz für den neuen Standort auswählen. Alternativ können Sie den anderen Standort deinstallieren oder dessen Datenbank in eine andere SQL Server-Instanz verschieben.

### <a name="default-client-agent-settings-have-nap-enabled"></a>NAP für Standardeinstellungen für den Client-Agent aktiviert

*Gilt für: Standort der zentralen Verwaltung, primären Standort*

Die Standardeinstellungen für den Client-Agent aktivieren den NAP nicht.

### <a name="domain-membership-error"></a>Domänenmitgliedschaft (Fehler)

*Gilt für: Standort der zentralen Verwaltung, primären Standort, SMS-Anbieter, SQL Server*

Der Configuration Manager-Computer ist Mitglied einer Windows-Domäne.

### <a name="endpoint-protection-point-on-the-expanded-primary-site"></a>Endpoint Protection-Punkt auf dem erweiterten primären Standort

*Gilt für: Standort der zentralen Verwaltung*

Wenn Sie einen primären Standort zu einer Hierarchie erweitern, wird die Endpoint Protection-Punktrolle auf dem eigenständigen primären Standort nicht installiert.

### <a name="existing-configuration-manager-server-components-on-server"></a>Auf dem Server vorhandene Komponenten des Configuration Manager-Servers

*Gilt für: Standort der zentralen Verwaltung, primären Standort und sekundären Standort*

Auf dem für die Installation des Standorts ausgewählten Server wurde noch kein Standortserver oder keine Standortsystemrolle installiert.

### <a name="existing-stand-alone-primary-site-for-version-and-site-code"></a>Eigenständiger primärer Standort für Versions- und Standortcode

*Gilt für: Standort der zentralen Verwaltung, primären Standort*

Der primäre Standort, den Sie erweitern möchten, ist ein eigenständiger primärer Standort. Er weist dieselbe Version wie Configuration Manager auf, hat aber einen anderen Standortcode als der Standort der zentralen Verwaltung, der installiert werden soll.

### <a name="firewall-exception-for-sql-server"></a>Firewallausnahme für SQL Server

*Gilt für: Standort der zentralen Verwaltung, primären Standort, sekundären Standort, Verwaltungspunkt*

Die Windows-Firewall ist deaktiviert, oder es existiert eine entsprechende Firewallausnahme für SQL Server.

Erlauben Sie einen Remotezugriff auf „sqlservr.exe“ bzw. die TCP-Ports. Standardmäßig wird TCP-Port 1433 von SQL Server überwacht, und TCP-Port 4022 wird vom SQL-Server-Dienst-Broker (SSB) verwendet.

### <a name="free-disk-space-on-site-server"></a>Freier Speicherplatz auf Standortserver

*Gilt für: Standort der zentralen Verwaltung, primären Standort und sekundären Standort*

Dem Standortservercomputer müssen mindestens 15 GB freier Speicherplatz für die Installation des Standortservers zur Verfügung stehen. Wenn Sie den SMS-Anbieter auf demselben Server installieren, ist ein weiteres GB an verfügbarem Speicherplatz erforderlich.

### <a name="iis-service-running"></a>IIS-Dienst wird ausgeführt

*Gilt für: Verwaltungspunkt, Verteilungspunkt*

IIS ist installiert und wird auf dem Server für den Verwaltungs- oder Verwaltungspunkt ausgeführt.

### <a name="incompatible-collection-references"></a>Nicht kompatible Sammlungsverweise

*Gilt für: Standort der zentralen Verwaltung*

Bei einem Upgrade verweisen Collections nur auf Collections desselben Typs.

### <a name="match-collation-of-expand-primary-site"></a>Sortierung des erweiterten primären Standorts übernehmen

*Gilt für: Standort der zentralen Verwaltung*

Die Standortdatenbank für den eigenständigen primären Standort weist die gleiche Sortierung wie die Standortdatenbank am Standort der zentralen Verwaltung auf, wenn Sie einen primären Standort zu einer Hierarchie erweitern.

### <a name="maximum-text-replication-size-for-sql-server-always-on-availability-groups"></a>Maximale Textgröße für die Replikation für SQL Server Always On-Verfügbarkeitsgruppen

*Gilt für: Standortdatenbankserver*

Wenn Sie SQL Server Always On verwenden, muss die Einstellung **max text repl size** (Maximale Textgröße für die Replikation) richtig konfiguriert sein. Weitere Informationen finden Sie unter [Vorbereiten der Verwendung von SQL Server Always On-Verfügbarkeitsgruppen mit Configuration Manager](../configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="microsoft-intune-connector-on-the-expanded-primary-site"></a>Microsoft Intune-Connector auf dem erweiterten primären Standort

*Gilt für: Standort der zentralen Verwaltung*

Wenn Sie einen primären Standort zu einer Hierarchie erweitern, wird die Microsoft Intune-Connectorrolle auf dem eigenständigen primären Standort nicht installiert.

### <a name="microsoft-remote-differential-compression-rdc-library-registered"></a>Microsoft Remote Differential Compression-Bibliothek (RDC) registriert

*Gilt für: Standort der zentralen Verwaltung, primären Standort und sekundären Standort*

Die RDC-Bibliothek ist auf dem Configuration Manager-Standortserver registriert.

### <a name="microsoft-windows-installer"></a>Microsoft Windows Installer

*Gilt für: Standort der zentralen Verwaltung, primären Standort und sekundären Standort*

Überprüft die Version von Windows Installer.

Wenn bei dieser Überprüfung Fehler auftreten, konnte Setup die Version nicht überprüfen, oder die installierte Version erfüllt nicht die Mindestanforderungen von Windows Installer Version 4.5.

### <a name="minimum-net-framework-version-for-configuration-manager-console"></a>Mindestversion vom .NET Framework für die Configuration Manager-Konsole

*Gilt für: Configuration Manager-Konsole*

Microsoft .NET Framework 4.0 ist auf dem Computer mit der Configuration Manager-Konsole installiert.

### <a name="minimum-net-framework-version-for-configuration-manager-site-server"></a>Mindestversion vom .NET Framework für den Configuration Manager-Standortserver

*Gilt für: Standort der zentralen Verwaltung, primären Standort und sekundären Standort*

.NET Framework 3.5 ist auf dem Configuration Manager-Standortserver installiert oder aktiviert.

### <a name="minimum-net-framework-version-for-sql-server-express-edition-installation-for-configuration-manager-secondary-site"></a>Mindestversion von .NET Framework zur Installation der SQL Server Express-Edition für einen sekundären Configuration Manager-Standort

*Gilt für: Sekundären Standort*

.NET Framework 4.0 ist auf dem Configuration Manager-Server des sekundären Standorts installiert oder aktiviert. Diese Version ist für SQL Server Express erforderlich.

### <a name="parent-database-collation"></a>Sortierung der übergeordneten Datenbank

*Gilt für: Primären Standort, sekundären Standort*

Die Sortierung der Standortdatenbank entspricht der Sortierung der Datenbank des übergeordneten Standorts. Für alle Standorte in einer Hierarchie muss die gleiche Datenbanksortierung verwendet werden.

### <a name="parent-site-replication-status"></a>Replikationsstatus des übergeordneten Standorts

*Gilt für: Standort der zentralen Verwaltung, primären Standort*

Der Replikationsstatus des übergeordneten Standorts lautet **Replikation aktiv** (entspricht Status **125**).

### <a name="pending-system-restart"></a>Ausstehender Systemneustart

*Gilt für: Standort der zentralen Verwaltung, primären Standort und sekundären Standort*

Ein anderes Programm benötigt einen Serverneustart, bevor Sie das Setup ausführen können.

Ab Version 1810 ist diese Prüfung widerstandsfähiger. Die folgenden Registrierungsspeicherorte werden geprüft, um zu bestimmen, ob ein Neustart des Computers aussteht:<!--SCCMDocs-pr issue 3010-->  

- `HKLM:Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\RebootPending`  

- `HKLM:SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired`  

- `HKLM:SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations`  

- `HKLM:Software\Microsoft\ServerManager, CurrentRebootAttempts`  

### <a name="primary-fqdn"></a>Primärer FQDN

*Gilt für: Standort der zentralen Verwaltung, primären Standort, Standortdatenbankserver*

Der NetBIOS-Name des Computers entspricht dem Namen des lokalen Hosts im vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN).

### <a name="read-only-domain-controller"></a>Schreibgeschützte Domänencontroller

*Gilt für: Standort der zentralen Verwaltung, primären Standort und sekundären Standort*

Standortdatenbankserver und sekundäre Standortserver werden auf einem schreibgeschützten Domänencontroller nicht unterstützt.

Weitere Informationen finden Sie in dem Artikel zum Microsoft-Support unter [Problems when installing SQL Server on a domain controller (Probleme, die beim Installieren eines SQL Servers auf einem Domänencontroller auftreten können)](https://support.microsoft.com/help/2032911).

### <a name="required-sql-server-collation"></a>Erforderliche SQL Server-Sortierung

*Gilt für: Standort der zentralen Verwaltung, primären Standort und sekundären Standort*

Die SQL Server-Instanz wird so konfiguriert, dass sie die Sortierung **SQL_Latin1_General_CP1_CI_AS** verwendet.

Wenn die Configuration Manager-Standortdatenbank bereits installiert wurde, wird diese Prüfung auch für die Datenbank durchgeführt. Weitere Informationen zum Ändern der Sortierung Ihrer SQL Server-Instanz und -Datenbank finden Sie unter [SQL collation and unicode support (SQL-Sortierung und Unicode-Unterstützung)](/sql/relational-databases/collations/collation-and-unicode-support).

Wenn Sie ein chinesisches Betriebssystem verwenden und die Unterstützung für GB18030 erforderlich ist, gilt diese Prüfung nicht. Weitere Informationen zum Aktivieren der GB18030-Unterstützung finden Sie unter [Internationale Unterstützung](../../../plan-design/hierarchy/international-support.md).

### <a name="server-service-is-running"></a>Serverdienst wird ausgeführt

*Gilt für: Standort der zentralen Verwaltung, primären Standort und sekundären Standort*

Der Serverdienst wurde gestartet und wird ausgeführt.

### <a name="setup-source-folder"></a>Setupquellordner

*Gilt für: Sekundären Standort*

Das Computerkonto des sekundären Standorts verfügt über die Berechtigungen für den Setupquellordner und die Freigabe:

- **Leseberechtigung** für das NTFS-Dateisystem  

- **Leseberechtigung** für die Freigabe  

> [!Note]  
> Wenn Sie administrative Freigaben verwenden z.B. C$ und D$, muss das Computerkonto des sekundären Standorts ein **Administrator** auf dem Computer sein.  

### <a name="setup-source-version"></a>Version der Setupquelle

*Gilt für: Sekundären Standort*

Die Configuration Manager-Version im Quellordner, den Sie für die Installation auf dem sekundären Standort angegeben haben, entspricht der Configuration Manager-Version des primären Standorts.

### <a name="site-code-in-use"></a>Standortcode verwendet

*Gilt für: Primären Standort*

Der angegebene Standortcode wird noch nicht in der Configuration Manager-Hierarchie verwendet. Geben Sie für diesen Standort einen eindeutigen Code an.

### <a name="site-server-computer-account-administrative-rights"></a>Administratorrechte für das Computerkonto des Standortservers

*Gilt für: Primären Standort, Standortdatenbankserver*

Das Standortserverkonto verfügt über **Administratorrechte** für den SQL-Server und den Verwaltungspunkt.

### <a name="site-server-fqdn-length"></a>Länge des vollqualifizierter Domänennamens des Standortservers

*Gilt für: Standort der zentralen Verwaltung, primären Standort und sekundären Standort*

Die Länge des FQDN des Standortservers.

### <a name="site-server-in-passive-mode-on-the-expanded-primary-site"></a>Passiver Standortserver am erweiterten primären Standort

*Gilt für: Standort der zentralen Verwaltung*

Wenn Sie einen primären Standort auf eine Hierarchie erweitern, wird der Standortserver nicht im passiven Modus auf dem eigenständigen primären Standort installiert.

### <a name="sms-provider-in-same-domain-as-site-server"></a>Der SMS-Anbieter befindet sich in der gleichen Domäne wie der Standortserver

*Gilt für: SMS-Anbieter*

Jede Instanz des SMS-Anbieters befindet sich in der gleichen Domäne wie der Standortserver.

### <a name="software-update-point-in-nlb-configuration"></a>Softwareupdatepunkt in NLB-Konfiguration

*Gilt für: Softwareupdatepunkt*

Der Standort verwendet keinen Netzwerklastenausgleich (Network Load Balancing, NLB) für aktive Softwareupdatepunkte für virtuelle Standorte.

### <a name="software-update-point-using-a-load-balancer"></a>Softwareupdatepunkt mit Lastenausgleich

*Gilt für: Softwareupdatepunkt*

Configuration Manager unterstützt keine Softwareupdatepunkte für den Netzwerk- oder Hardwarelastenausgleich.

### <a name="sql-server-always-on-availability-groups"></a>SQL Server Always On-Verfügbarkeitsgruppen

*Gilt für: Standortdatenbankserver*

Wenn Sie SQL Server Always On verwenden, müssen die Mindestanforderungen zum Hosten von Verfügbarkeitsgruppen erfüllt sein. Weitere Informationen finden Sie unter [Vorbereiten der Verwendung von SQL Server Always On-Verfügbarkeitsgruppen mit Configuration Manager](../configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="sql-server-availability-group-configured-for-readable-secondaries"></a>Konfigurierte SQL Server-Verfügbarkeitsgruppe für lesbare sekundäre Replikate

*Gilt für: Standortdatenbankserver*

Wenn Sie SQL Server Always On verwenden, überprüfen Sie den sekundären Lesezustand von Replikaten von Verfügbarkeitsgruppen.

### <a name="sql-server-availability-group-configured-for-manual-failover"></a>SQL Server-Verfügbarkeitsgruppe für manuelle Failover konfiguriert

*Gilt für: Standortdatenbankserver*

Bei der Verwendung von SQL Server Always On werden Verfügbarkeitsgruppenreplikate für manuelle Failover konfiguriert.

### <a name="sql-server-availability-group-replicas-on-default-instance"></a>SQL Server-Verfügbarkeitsgruppenreplikate auf Standardinstanz

*Gilt für: Standortdatenbankserver*

Bei der Verwendung von SQL Server Always On befinden sich die Verfügbarkeitsgruppenreplikate auf der Standardinstanz.

### <a name="sql-availability-group-replicas-must-all-have-the-same-seeding-mode"></a>SQL-Verfügbarkeitsgruppenreplikate müssen alle denselben Seedingmodus aufweisen.

<!-- SCCMDocs-pr#3899 -->
*Gilt für: Standortdatenbankserver*

Ab Version 1906 müssen Sie beim Verwenden von SQL Server Always On Verfügbarkeitsgruppenreplikate mit demselben [Seedingmodus](/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas) konfigurieren.

### <a name="sql-availability-group-replicas-must-be-healthy"></a>SQL-Verfügbarkeitsgruppenreplikate müssen fehlerfrei sein.

<!-- SCCMDocs-pr#3899 -->
*Gilt für: Standortdatenbankserver*

Ab Version 1906 sind beim Verwenden von SQL Server Always On Verfügbarkeitsgruppenreplikate fehlerfrei.

### <a name="sql-server-configuration-for-site-upgrade"></a>SQL Server-Konfiguration für Standortupgrade

*Gilt für: Standortdatenbankserver*

SQL Server erfüllt die Mindestanforderungen für ein Standortupgrade. Weitere Informationen finden Sie unter [Unterstützte SQL Server-Versionen](../../../plan-design/configs/support-for-sql-server-versions.md).

### <a name="sql-server-edition"></a>SQL Server-Edition

*Gilt für: Standortdatenbankserver*

Die SQL Server-Edition am Standort ist nicht SQL Server Express.

### <a name="sql-server-express-on-secondary-site"></a>SQL Server Express an sekundärem Standort

*Gilt für: Sekundären Standort*

SQL Server Express kann am sekundären Standort installiert werden.

### <a name="sql-server-on-the-secondary-site-server"></a>SQL Server auf dem Server des sekundären Standorts

*Gilt für: Sekundären Standort*

SQL Server ist auf dem Server des sekundären Standorts installiert. SQL Server kann nicht auf einem Remotestandortsystem für einen sekundären Standort installiert werden.

> [!Warning]  
> Diese Prüfung gilt nur dann, wenn Sie auswählen, dass das Setup eine vorhandene SQL Server-Instanz verwenden soll.  

### <a name="sql-server-service-running-account"></a>SQL Server-Dienst, von dem das Konto ausgeführt wird

*Gilt für: Standort der zentralen Verwaltung, primären Standort und sekundären Standort*

Das Anmeldekonto für den SQL Server-Dienst ist kein lokales Benutzerkonto oder **LOCAL SERVICE**.

Konfigurieren Sie den SQL Server-Dienst, damit dieser ein gültiges Domänenkonto verwendet, entweder **NETWORK SERVICE** oder **LOCAL SYSTEM**.

### <a name="sql-server-site-database-consistency"></a>SQL Server-Standortdatenbankkonsistenz

*Gilt für: Standortdatenbankserver*

Überprüfen Sie die Datenbankkonsistenz.

### <a name="sql-server-sysadmin-rights"></a>Systemadministratorrechte für SQL Server

*Gilt für: Standortdatenbankserver*

Das Benutzerkonto, über das das Configuration Manager-Setup ausgeführt wird, verfügt über die Rolle **sysadmin** für die SQL Server-Instanz, die Sie für die Datenbankinstallation ausgewählt haben. Bei dieser Überprüfung tritt auch dann ein Fehler auf, wenn vom Setup nicht auf die SQL Server-Instanz zugegriffen werden kann, um die Berechtigungen zu prüfen.

### <a name="sql-server-sysadmin-rights-for-reference-site"></a>SQL Server-Systemadministratorrechte für Referenzstandort

*Gilt für: Standortdatenbankserver*

Das Benutzerkonto, über das das Configuration Manager-Setup ausgeführt wird, verfügt über die Rolle **sysadmin** für die SQL Server-Rolleninstanz, die Sie als Datenbank des Referenzstandorts ausgewählt haben. **sysadmin**-Rollenberechtigungen für SQL Server sind erforderlich, um Standortdatenbanken zu ändern.

### <a name="sql-server-tcp-port"></a>SQL Server-TCP-Port

*Gilt für: Standortdatenbankserver*

TCP ist für die Instanz von SQL Server aktiviert und verwendet einen statischen Port.

### <a name="sql-server-version"></a>SQL Server-Version

*Gilt für: Standortdatenbankserver*

Eine unterstützte Version von SQL Server wird auf dem angegebenen Standortdatenbankserver installiert.

Weitere Informationen finden Sie unter [Unterstützte SQL Server-Versionen](../../../plan-design/configs/support-for-sql-server-versions.md).

### <a name="unsupported-os-for-configuration-manager-console"></a>Nicht unterstützte Betriebssysteme für Configuration Manager-Konsolen

*Gilt für: Configuration Manager-Konsole*

Installieren Sie die Configuration Manager-Konsole auf Computern, auf denen eine unterstützte Betriebssystemversion ausgeführt wird.

Weitere Informationen finden Sie unter [Unterstützte Betriebssysteme für die System Center Configuration Manager-Konsole](../../../plan-design/configs/supported-operating-systems-consoles.md).

### <a name="unsupported-os-for-site-server"></a>Nicht unterstützte Betriebssysteme für den Standortserver

*Gilt für: Standort der zentralen Verwaltung, primären Standort, sekundären Standort, Configuration Manager-Konsole, Verwaltungspunkt, Verteilungspunkt*

Der Server führt eine unterstützte Betriebsystemversion aus.

Weitere Informationen finden Sie unter [Supported OS versions for Configuration Manager site system servers (Unterstützte Betriebssysteme für Configuration Manager-Standortsystemserver)](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md).

### <a name="unsupported-site-system-role-out-of-band-service-point"></a>Nicht unterstützte Standortsystemrolle „Out-of-Band-Dienstpunkt“

*Gilt für: Primären Standort*

Die Standortsystemrolle „Out-of-Band-Dienstpunkt“ wurde nicht installiert.

### <a name="unsupported-site-system-role-system-health-validation-point"></a>Nicht unterstützte Standortsystemrolle „Systemintegritätsprüfungspunkt“

*Gilt für: Primären Standort*

Die Standortsystemrolle „Systemintegritätsprüfungspunkt“ ist nicht installiert.

### <a name="unsupported-upgrade-path"></a>Der Upgradepfad wird nicht unterstützt

*Gilt für: Standort der zentralen Verwaltung, primären Standort*

Für alle Standortserver in der Hierarchie ist die mindestens für das Upgrade erforderliche Version von Configuration Manager installiert.

### <a name="usmt-installed"></a>USMT ist installiert

*Gilt für: Standort der zentralen Verwaltung, primären Standort (nur eigenständig)*

Die Komponente „Migrationstool für den Benutzerstatus“ (User State Migration Tool, USMT) des Assessment and Deployment Kits (ADK) für Windows ist installiert.

### <a name="validate-fqdn-of-sql-server"></a>FQDN von SQL Server überprüfen

*Gilt für: Standortdatenbankserver*

Geben Sie einen gültigen FQDN für den SQL Server-Computer an.

### <a name="verify-central-administration-site-version"></a>Version des Standorts der zentralen Verwaltung überprüfen

*Gilt für: Primären Standort*

Der Standort der zentralen Verwaltung hat die gleiche Version von Configuration Manager.

### <a name="verify-database-consistency"></a>Datenbankkonsistenz überprüfen

*Gilt für: Standort der zentralen Verwaltung, primären Standort*

Überprüft die Konsistenz der Standortdatenbank in SQL Server.  

### <a name="windows-deployment-tools-installed"></a>Die Windows-Bereitstellungstools sind installiert

*Gilt für: SMS-Anbieter*

Die Komponente „Windows-Bereitstellungstools“ des Windows ADK ist installiert.

### <a name="windows-failover-cluster"></a>Windows-Failovercluster

*Gilt für: Standortserver, Verwaltungspunkt, Verteilungspunkt*

Server mit der Standortserverrolle, Verwaltungspunktrolle oder der Verteilungspunktrolle sind nicht Teil eines Windows-Clusters.

Ab Version 1810 blockiert der Einrichtungsprozess für Configuration Manager nicht mehr die Installation der Standortserverrolle auf einem Computer mit der Windows-Rolle für Failoverclustering. SQL Always On erfordert diese Rolle, daher konnten Sie die Standortdatenbank auf dem Standortserver bisher nicht gleichzeitig installieren. Mit dieser Änderung haben Sie die Möglichkeit, eine hochverfügbare Website mit weniger Servern zu erstellen, indem Sie SQL Always On und einen Standortserver im passiven Modus verwenden. Weitere Informationen finden Sie unter [High availability options (Optionen für Hochverfügbarkeit)](../configure/high-availability-options.md). <!--1359132-->  

### <a name="windows-pe-installed"></a>Windows PE ist installiert

*Gilt für: SMS-Anbieter*

Die Komponente „Windows Preinstallation Environment“ des Windows ADK ist installiert.



## <a name="warnings"></a>Warnungen

### <a name="active-directory-domain-functional-level"></a>Active Directory-Domänenfunktionsebene

*Gilt für: Standort der zentralen Verwaltung, primären Standort*

Die Mindestfunktionsebene der Active Directory-Domäne und -Gesamtstruktur ist Windows Server 2008 R2. Weitere Informationen finden Sie unter [Unterstützung für Active Directory-Domänen](../../../plan-design/configs/support-for-active-directory-domains.md).

### <a name="administrative-rights-on-distribution-point"></a>Administratorrechte für den Verteilungspunkt

*Gilt für: Verteilungspunkt*

Das Benutzerkonto, das das Setup ausführt, verfügt über **Administratorrechte** für den Verteilungspunkt.

### <a name="administrative-rights-on-management-point"></a>Administratorrechte für den Verwaltungspunkt

*Gilt für: Verwaltungspunkt, Verteilungspunkt*

Das Computerkonto des Standortservers verfügt über **Administratorrechte** für den Verwaltungspunkt und den Verteilungspunkt.

### <a name="administrative-share-site-system"></a>Administrative Freigabe (Standortsystem)

*Gilt für: Verwaltungspunkt*

Die erforderlichen administrativen Freigaben sind auf dem Standortsystemcomputer vorhanden.

### <a name="application-compatibility"></a>Anwendungskompatibilität

*Gilt für: Standort der zentralen Verwaltung, primären Standort*

Alle aktuellen Anwendungen sind mit dem Anwendungsschema kompatibel.

### <a name="backlogged-inboxes"></a>Eingangsboxen in Rückstand

*Gilt für: Standort der zentralen Verwaltung, primären Standort*

Der Standortserver bearbeitet wichtige Eingangsboxen in kurzer Zeit. Deshalb sind in den Eingangsboxen keine Dateien enthalten, die älter als einen Tag sind.

Die folgenden Ordner werden überprüft:

- `despoolr.box\receive\*.i??`

- `despoolr.box\receive\*.s??`

- `despoolr.box\receive\*.nil`

- `schedule.box\requests\*.sr?`

Überprüfen Sie, ob der Despooler und die Zeitplankomponenten für das Standortsystem ausgeführt werden, um diese Warnung zu entfernen.

### <a name="bits-installed"></a>BITS installiert

*Gilt für: Verwaltungspunkt*

Der BITS (Background Intelligent Transfer Service) ist in IIS installiert und aktiviert.

### <a name="check-if-the-site-uses-upgrade-readiness-cloud-service-connector"></a>Überprüfen, ob der Clouddienstconnector für Upgradebereitschaft am Standort verwendet wird

*Gilt für: Standort der zentralen Verwaltung, primären Standort*

Der Upgradebereitschaft-Dienst wurde am 31. Januar 2020 eingestellt. Weitere Informationen finden Sie unter [KB 4521815: Windows Analytics-Deaktivierung am 31. Januar 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).

Desktop Analytics ist die Weiterentwicklung von Windows Analytics. Weitere Informationen finden Sie unter [Was ist Desktop Analytics?](../../../../desktop-analytics/overview.md)

Wenn Ihr Configuration Manager-Standort mit der Upgradebereitschaft verbunden war, müssen Sie ihn entfernen und Clients neu konfigurieren. Weitere Informationen finden Sie unter [Entfernen der Upgradebereitschaftsverbindung](../../../clients/manage/upgrade-readiness.md#bkmk_remove).

Wenn Sie diese Voraussetzungswarnung ignorieren, entfernt das Configuration Manager-Setup den Upgradebereitschaft-Connector automatisch.<!-- #4898 -->

### <a name="cloud-management-gateway-requires-either-token-based-authentication-or-an-https-management-point"></a>Cloud Management Gateway erfordert entweder eine tokenbasierte Authentifizierung oder einen HTTPS-Verwaltungspunkt.

*Gilt für: Cloud Management Gateway*

Bei einigen Configuration Manager-Versionen können Sie keinen HTTP-Verwaltungspunkt mit Cloud Management Gateway (CMG) verwenden. Konfigurieren Sie CMG entweder für HTTPS, oder konfigurieren Sie den Standort für erweitertes HTTP. Weitere Informationen finden Sie unter [Planen des Cloudverwaltungsgateways](../../../clients/manage/cmg/plan-cloud-management-gateway.md).

### <a name="configuration-for-sql-server-memory-usage"></a>Konfiguration der Speichernutzung durch SQL Server

*Gilt für: Standortdatenbankserver*

Für SQL Server wurde kein Speicherlimit konfiguriert. Konfigurieren Sie einen Maximalwert für den SQL Server-Speicher.

### <a name="distribution-point-package-version"></a>Version des Verteilungspunktpakets

*Gilt für: Verteilungspunkte*

Alle Verteilungspunkte des Standorts verfügen über die aktuelle Version der Softwareverteilungspakete.

### <a name="domain-membership-warning"></a>Domänenmitgliedschaft (Warnung)

*Gilt für: Verwaltungspunkt, Verteilungspunkt*

Der Configuration Manager-Computer ist Mitglied einer Windows-Domäne.

### <a name="firewall-exception-for-sql-server-standalone-primary-site"></a>Firewallausnahme für SQL Server (eigenständiger primärer Standort)

*Gilt für: Primären Standort (nur eigenständig)*

Die Windows-Firewall ist deaktiviert, oder es existiert eine entsprechende Firewallausnahme für SQL Server.

Erlauben Sie einen Remotezugriff auf „sqlservr.exe“ bzw. die TCP-Ports. Standardmäßig wird TCP-Port 1433 von SQL Server überwacht, und TCP-Port 4022 wird vom Server Service Broker (SSB) verwendet.

### <a name="firewall-exception-for-sql-server-for-management-point"></a>Firewallausnahme bei SQL Server für Verwaltungspunkt

*Gilt für: Verwaltungspunkt*

Die Windows-Firewall ist deaktiviert, oder es existiert eine entsprechende Firewallausnahme für SQL Server.

### <a name="iis-https-configuration"></a>IIS-HTTPS-Konfiguration

*Gilt für: Verwaltungspunkt, Verteilungspunkt*

Die IIS-Website verfügt über Bindungen für das HTTPS-Kommunikationsprotokoll.

Wenn Sie die Installation von Standortrollen, für die HTTPS erforderlich ist, vorgenommen haben, konfigurieren Sie die IIS-Websitebindungen auf dem angegebenen Server mit einem gültigen Public-Key-Infrastructure-Serverzertifikat (PKI).

### <a name="invalid-discovery-records"></a>Ungültige Ermittlungsdatensätze

*Gilt für den Standort der zentralen Verwaltung*

Es sind Ermittlungsdatensätze vorhanden, die nicht mehr gültig sind. Diese Datensätze werden zur Löschung gekennzeichnet.

### <a name="microsoft-xml-core-services-60-msxml60"></a>Microsoft XML Core Services 6.0 (MSXML60)

*Gilt für den Standort der zentralen Verwaltung, den primären Standort, den sekundären Standort, die Configuration Manager-Konsole, den Verwaltungspunkt, den Verteilungspunkt*

Auf dem Computer ist MSXML Version 6.0 oder höher installiert.

### <a name="network-access-protection-nap-is-no-longer-supported"></a>Netzwerkzugriffsschutz (Network Access Protection, NAP) wird nicht länger unterstützt.

*Gilt für: Primären Standort*

Es sind keine Softwareupdates für den Netzwerkzugriffsschutz aktiviert.

### <a name="ntfs-drive-on-site-server"></a>NTFS-Laufwerk auf dem Standortserver

*Gilt für: Primären Standort*

Das Laufwerk wird mit dem NTFS-Dateisystem formatiert. Installieren Sie für eine erhöhte Sicherheit die Standortserverkomponenten auf Laufwerken, die mit dem NTFS-Dateisystem für mehr Sicherheit formatiert sind.

### <a name="pending-configuration-item-policy-updates"></a><a name="bkmk_pending-policy"></a> Ausstehende Richtlinienupdates für Konfigurationselemente

<!--SCCMDocs-pr issue 2814-->

*Gilt für: Primären Standort*

Wenn Sie ab Version 1806 ein Update von Version 1706 oder höher durchführen, wird möglicherweise diese Warnung angezeigt, wenn Sie über mehrere Anwendungsbereitstellungen verfügen und mindestens eine davon genehmigt werden muss.

Sie haben zwei Möglichkeiten:  

- Sie können die Warnung ignorieren und mit dem Update fortfahren. Dies hätte zur Folge, dass der Standortserver während des Updates höhere Leistungen erbringen muss, um die Richtlinien zu verarbeiten. Außerdem wäre dann nach dem Update möglicherweise die Prozessorauslastung auf dem Verwaltungspunkt höher.  

- Sie können eine der Anwendungen überarbeiten, für die es keine Anforderung oder nur eine bestimmte Betriebssystemanforderung gibt. Verarbeiten Sie dann zunächst einen Teil der aktuellen Last auf dem Standortserver. Prüfen Sie die Datei **objreplmgr.log**, und überwachen Sie anschließend den Prozessor auf dem Verwaltungspunkt. Aktualisieren Sie den Standort im Anschluss an die Verarbeitung. Es werden zwar nach dem Update weiterhin zusätzliche Verarbeitungsvorgänge ausgeführt, aber wenn Sie wie oben beschrieben die Warnung ignorieren, ist der nachträgliche Aufwand größer.  

### <a name="pending-system-restart-on-the-remote-sql-server"></a>Ausstehender Systemneustart auf dem SQL-Remoteserver

*Gilt für: Version 1902 und höher, SQL-Remoteserver*

Ein anderes Programm benötigt einen Serverneustart, bevor Sie das Setup ausführen können.

Die folgenden Registrierungsspeicherorte werden geprüft, um zu bestimmen, ob ein Neustart des Computers aussteht:<!--SCCMDocs-pr issue 3377-->  

- `HKLM:Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\RebootPending`  

- `HKLM:SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired`  

- `HKLM:SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations`  

- `HKLM:Software\Microsoft\ServerManager, CurrentRebootAttempts`  

### <a name="powershell-20-on-site-server"></a>PowerShell 2.0 auf dem Standortserver

*Gilt für: Primären Standort mit dem Exchange-Connector*

Windows PowerShell Version 2.0 oder höher ist auf dem Standortserver für den Configuration Manager Exchange Connector installiert.

### <a name="remote-connection-to-wmi-on-secondary-site"></a>Remoteverbindung mit WMI am sekundären Standort

*Gilt für: Sekundären Standort*

Das Setup kann eine Remoteverbindung mit WMI am Server des sekundären Standorts herstellen.

### <a name="schema-extensions"></a>Schemaerweiterungen

*Gilt für: Standort der zentralen Verwaltung, primären Standort*

Das Active Directory-Schema wurde erweitert. Wenn es erweitert wird, entspricht die Version den Schemaerweiterungen, die verwendet wurden.

Configuration Manager erfordert keine Active Directory-Schemaerweiterungen für die Standortserverinstallation. Sie werden von Microsoft empfohlen, damit Sie alle Configuration Manager-Features verwenden können. Weitere Informationen zu den Vorteilen einer Schemaerweiterung finden Sie unter [Vorbereiten von Active Directory für die Veröffentlichung eines Standorts](../../../plan-design/network/extend-the-active-directory-schema.md).

### <a name="share-name-in-package"></a>Freigabename in Paket

*Gilt für: Standort der zentralen Verwaltung, primären Standort*

Freigabenamen für Pakete enthalten keine ungültigen Zeichen wie `#`.

### <a name="site-system-to-sql-server-communication"></a>Kommunikation zwischen Standortsystem und SQL Server

*Gilt für: Sekundären Standort, Verwaltungspunkt*

Das Konto, das Sie zum Ausführen des SQL Server-Diensts für die Standortdatenbankinstanz konfiguriert haben, verfügt über einen gültigen Dienstprinzipalnamen (Service Principal Name, SPN) in Active Directory Domain Services. Registrieren Sie einen gültigen SPN in Active Directory, um die Kerberos-Authentifizierung zu unterstützen.

### <a name="sql-server-change-tracking-cleanup"></a><a name="bkmk_changetracking"></a> Änderungsnachverfolgungsbereinigung für SQL Server

*Gilt für: Standortdatenbankserver*

Prüfen Sie ab Version 1810, ob die Standortdatenbank über ein Backlog mit Daten zur SQL-Änderungsnachverfolgung verfügt.<!--SCCMDocs-pr issue 3023-->  

Überprüfen Sie diese Prüfung manuell, indem Sie eine gespeicherte Diagnoseprozedur in der Standortdatenbank ausführen. Stellen Sie zunächst eine [Diagnoseverbindung](/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators) mit der Standortdatenbank her. Dies erreichen Sie am einfachsten mithilfe des Abfrage-Editors für die Datenbank-Engine von SQL Server Management Studio und einer Verbindung mit `admin:<instance name>`.

Führen Sie in einem Abfragefenster für dedizierte Administratorverbindungen die folgenden Befehle aus:

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking
```

Je nach Größe Ihrer Datenbank und des Backlogs kann diese gespeicherte Prozedur zwischen wenigen Minuten und mehreren Stunden in Anspruch nehmen. Wenn die Abfrage abgeschlossen wird, werden zwei Abschnitte mit Daten angezeigt, die mit dem Backlog in Zusammenhang stehen. Sehen Sie sich zunächst **CT_Days_Old** an. Dieser Wert gibt das Alter des ältesten Eintrags in Ihrer syscommittab-Tabelle (in Tagen) an. Er sollte fünf Tage betragen. Dies ist der Standardwert von Configuration Manager. Ändern Sie diesen Standardwert nicht. Bei einem hohen Volumen an Datenverarbeitungen oder Datenreplikationen kann es sein, dass der älteste Eintrag in syscommittab älter als fünf Tage ist. Wenn diese Wert höher als sieben Tage ist, führen Sie ein manuelles Cleanup der Daten zu Änderungsnachverfolgung durch.  

Führen Sie den folgenden Befehl in der dedizierten Administratorverbindung aus, um die Änderungsnachverfolgungsdaten zu bereinigen:

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking @CleanupChangeTracking = 1
```

Dieser Befehl startet ein Cleanup für syscommittab und alle verwandten untergeordneten Tabellen. Die Ausführung kann wenige Minuten bis mehrere Stunden in Anspruch nehmen. Fragen Sie die **vLogs**-Ansicht ab, um den Fortschritt zu überwachen. Führen Sie die folgende Abfrage aus, um den aktuellen Fortschritt anzuzeigen:

```SQL
SELECT * FROM vLogs WHERE ProcedureName = 'spDiagChangeTracking'
```

### <a name="sql-server-native-client"></a>SQL Server Native Client

<!--SCCMDocs-pr issue 3094-->

Wenn Sie einen neuen Standort installieren, installiert Configuration Manager automatisch SQL Server Native Client als weitervertreibbare Komponente. Nach der Installation des Standorts führt Configuration Manager kein Upgrade für den SQL Server Native Client durch. Für eine Aktualisierung des SQL Server Native Clients ist möglicherweise ein Neustart erforderlich, der Auswirkungen auf den Standortinstallationsvorgang haben kann.

Diese Überprüfung stellt sicher, dass der Standortserver über eine unterstützte Version von SQL Native Client verfügt. Bei der Voraussetzungsprüfung wird die Version von SQL Native Client auf Remotestandortsystemen nicht überprüft.

Die Mindestversion ist SQL 2012 SP4 (`11.*.7001.0`). Diese SQL Native Client-Version unterstützt TLS 1.2. Weitere Informationen finden Sie in den folgenden Artikeln:

- [Unterstützung für Microsoft SQL Server TLS 1.2 ](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)  

- [Aktivieren von TLS 1.2 für den Konfigurations-Manager](../../../plan-design/security/enable-tls-1-2.md)  

Configuration Manager verwendet den SQL Server Native Client für die folgenden Standortsystemrollen:<!-- SCCMDocs issue 1150 -->

- Standortdatenbankserver
- Standortserver: Standort der zentralen Verwaltung, primärer Standort, sekundärer Standort
- Verwaltungspunkt
- Geräteverwaltungspunkt
- Zustandsmigrationspunkt
- SMS-Anbieter
- Softwareupdatepunkt
- Multicast-fähiger Verteilungspunkt
- Asset Intelligence-Aktualisierungsdienstpunkt
- Reporting Services-Punkt
- Anwendungskatalog-Webdienst
- Anmeldungspunkt
- Endpoint Protection-Punkt
- Dienstverbindungspunkt
- Zertifikatregistrierungspunkt
- Data Warehouse-Dienstpunkt

### <a name="sql-server-process-memory-allocation"></a>Speicherreservierung für SQL Server-Prozess

*Gilt für: Standortdatenbankserver*

SQL Server reserviert mindestens 8 GB Speicherplatz für den zentralen Verwaltungsstandort und den primären Standort und mindestens 4 GB für den sekundären Standort.

Weitere Informationen finden Sie unter [So konfigurieren Sie Arbeitsspeicheroptionen mithilfe von SQL Server Management Studio](/sql/database-engine/configure-windows/server-memory-server-configuration-options#how-to-configure-memory-options-using-).

> [!NOTE]  
> Diese Prüfung gilt nicht für SQL Server Express an einem sekundären Sekundärer Standort. Diese Edition ist auf 1 GB reservierten Speicherplatz eingeschränkt.  

### <a name="sql-server-security-mode"></a>SQL Server-Sicherheitsmodus

*Gilt für: Standortdatenbankserver*

Die Windows-Authentifizierungssicherheit ist für SQL Server konfiguriert.

### <a name="unsupported-site-system-os-version-for-upgrade"></a>Nicht unterstützte Version des Standortsystembetriebssystems für ein Upgrade

*Gilt für: Primären Standort, sekundären Standort*

Standortsystemrollen, die keine Verteilungspunktrollen sind, werden auf Servern mit Windows Server 2012 und höher installiert.

Weitere Informationen finden Sie unter [Unterstützte Betriebssysteme für Clients und Geräte für Configuration Manager](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md).

> [!NOTE]  
> Diese Prüfung kann den Status von Standortsystemrollen nicht auflösen, die in Azure oder im von Microsoft Intune verwendeten Cloudspeicher installiert wurden. Ignorieren Sie Warnungen für diese Rollen. Dabei handelt es sich um falsch positive Ergebnisse.

### <a name="upgrade-assessment-toolkit-is-unsupported"></a>Toolkit zur Upgradebewertung wird nicht unterstützt

*Gilt für: Standort der zentralen Verwaltung, primären Standort*

Das Toolkit zur Upgradebewertung ist nicht installiert. Weitere Informationen finden Sie unter [Entfernte und veraltete Features](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).

### <a name="verify-site-server-permissions-to-publish-to-active-directory"></a>Standortserverberechtigungen überprüfen, um Veröffentlichungen in Active Directory vorzunehmen

*Gilt für: Standort der zentralen Verwaltung, primären Standort und sekundären Standort*

Das Computerkonto für den Standortserver verfügt über die Berechtigung **Vollzugriff** für den Container **Systemverwaltung** in der Active Directory-Domäne.

Weitere Informationen finden Sie unter [Vorbereiten von Active Directory für die Veröffentlichung eines Standorts](../../../plan-design/network/extend-the-active-directory-schema.md).

> [!NOTE]  
> Sie können diese Warnung ignorieren, wenn Sie die Berechtigungen manuell überprüft haben.

### <a name="windows-remote-management-winrm-v11"></a>Windows Remote Management (WinRM) Version 1

*Gilt für: Primären Standort, Configuration Manager-Konsole*

WinRM Version 1.1 ist auf dem Computer des primären Standortservers oder der Configuration Manager-Konsole installiert, um die Out-of-band-Verwaltungskonsole auszuführen.

WinRM wird automatisch mit allen derzeit unterstützten Versionen von Windows installiert. Weitere Informationen finden Sie unter [Installation und Konfiguration für die Windows-Remoteverwaltung](/windows/win32/winrm/installation-and-configuration-for-windows-remote-management).

### <a name="wsus-on-site-server"></a>WSUS auf Standortserver

*Gilt für: Standort der zentralen Verwaltung, primären Standort*

Die Windows Server Update Services (WSUS) sind auf dem Standortserver installiert.

Wenn Sie einen Softwareupdatepunkt auf einem Server verwenden, der von dem des Standortservers abweicht, müssen Sie auf dem Standortserver die WSUS-Administrationskonsole installieren. Weitere Informationen über WSUS finden Sie unter [Windows Server Update Services](/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus).