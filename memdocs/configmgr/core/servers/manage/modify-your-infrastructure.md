---
title: Ändern der Infrastruktur
titleSuffix: Configuration Manager
description: Nehmen Sie Änderungen vor oder führen Sie Aktionen aus, die sich auf Ihre Configuration Manager-Infrastruktur auswirken.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a7975dc8-46ab-4dae-86b6-dc3e3cf3b2f0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 92bf86225cf869622fd4b496fd3e8e852b651a70
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694358"
---
# <a name="modify-your-configuration-manager-infrastructure"></a>Ändern der Configuration Manager-Infrastruktur

*Gilt für: Configuration Manager (Current Branch)*

Nachdem Sie einen oder mehrere Standorte installiert haben, müssen Sie möglicherweise Konfigurationen ändern oder Aktionen ausführen, die sich auf Ihre Infrastruktur auswirken.

## <a name="manage-the-sms-provider"></a><a name="BKMK_ManageSMSprovider"></a> Verwalten des SMS-Anbieters

Der SMS-Anbieter stellt den administrativen Kontaktpunkt für mindestens eine Configuration Manager-Konsole bereit. Wenn Sie mehrere SMS-Anbieter installieren, können Sie Redundanz für Kontaktpunkte zur Verwaltung des Standorts und der Hierarchie bereitstellen.

An jedem Configuration Manager-Standort können Sie das Setup mit folgenden Zielen erneut ausführen:

- Hinzufügen einer zusätzlichen Instanz des SMS-Anbieters. Jede zusätzliche Instanz des SMS-Anbieters muss sich auf einem separaten Computer befinden.

- Entfernen einer Instanz des SMS-Anbieters. Sie müssen einen Standort deinstallieren, um den letzten SMS-Anbieter des Standorts zu entfernen.

Überwachen Sie die Installation bzw. das Entfernen eines SMS-Anbieters anhand der Protokolldatei **ConfigMgrSetup.log**. Sie finden die Datei im Stammordner des Standortservers, auf dem Sie das Setup ausführen.

Machen Sie sich mit den Informationen unter [Planen des SMS-Anbieters](../../plan-design/hierarchy/plan-for-the-sms-provider.md) vertraut, bevor Sie den SMS-Anbieter an einem Standort ändern.

### <a name="manage-the-sms-provider-configuration-for-a-site"></a>Verwalten der SMS-Anbieterkonfiguration für einen Standort  

1. Führen Sie das **Configuration Manager-Setup** über `\BIN\X64\setup.exe` im Installationsordner des Configuration Manager-Standorts aus.

1. Wählen Sie auf der Seite **Erste Schritte** die Option **Standortwartung durchführen oder diesen Standort zurücksetzen** aus.

1. Wählen Sie auf der Seite **Standortwartung** die Option **SMS-Anbieterkonfiguration ändern** aus.

1. Wählen Sie auf der Seite **SMS-Anbieter verwalten** eine der folgenden Optionen aus:

    - **Neuen SMS-Anbieter hinzufügen**: Geben Sie den FQDN für einen Computer an, auf dem der SMS-Anbieter gehostet werden soll und auf dem er derzeit nicht gehostet wird.

    - **Uninstall the specified SMS provider** (Angegebenen SMS-Anbieter deinstallieren): Wählen Sie den Namen des Computers aus, von dem Sie den SMS-Anbieter entfernen möchten.

    > [!TIP]  
    > Um den SMS-Anbieter zwischen zwei Computern zu verschieben, installieren Sie ihn zunächst auf dem neuen Computer. Dann entfernen Sie ihn vom ursprünglichen Speicherort. Es gibt keine Möglichkeit, den SMS-Anbieter zwischen den Computern zu verschieben.

Mit dem Beenden des Setup-Assistenten ist die SMS-Anbieterkonfiguration abgeschlossen. Sie können auf der Registerkarte **Allgemein** in den **Eigenschaften** des Standorts die Computer überprüfen, bei denen ein SMS-Anbieter für einen Standort installiert ist.

## <a name="manage-the-configuration-manager-console"></a><a name="bkmk_Console"></a> Verwalten der Configuration Manager-Konsole

Nachfolgend sind Aufgaben aufgeführt, mit denen Sie die Configuration Manager-Konsole verwalten können:

- Informationen zum Ändern der in der Configuration Manager-Konsole angezeigten Sprache finden Sie unter [Verwalten der Sprache der Configuration Manager-Konsole](#BKMK_ManageConsoleLanguages).

- Informationen zum Installieren zusätzlicher Konsolen finden Sie unter [Installieren von Configuration Manager-Konsolen](../deploy/install/install-consoles.md).

- Informationen zum Konfigurieren der DCOM-Berechtigung für das Aktivieren von Konsolen, die sich nicht am selben Ort wie der Standortserver befinden, finden Sie unter [Konfigurieren von DCOM-Berechtigungen für Remotekonsolen](#BKMK_ConfigDCOMforRemoteConsole).

- Informationen zum Ändern von Administratorberechtigungen, sodass die Anzeige und der Bereich möglicher Aktionen in der Konsole für Benutzer begrenzt werden, finden Sie unter [Ändern des Verwaltungsbereichs eines Administrators](../deploy/configure/configure-role-based-administration.md#BKMK_ModAdminUser).

### <a name="manage-configuration-manager-console-language"></a><a name="BKMK_ManageConsoleLanguages"></a> Verwalten der Sprache der Configuration Manager-Konsole

Während der Installation des Standortservers werden die Configuration Manager-Konsoleninstallationsdateien und unterstützten Sprachpakete für den Standort in den Unterordner `\Tools\ConsoleSetup` des Configuration Manager-Installationspfads auf dem Standortserver kopiert.

- Wenn Sie die Installation der Configuration Manager-Konsole von diesem Ordner auf dem Standortserver aus starten, werden die Configuration Manager-Konsole und die unterstützten Sprachpaketdateien auf den Computer kopiert.

- Wenn ein Sprachpaket für die aktuelle Spracheinstellung des Computers verfügbar ist, wird die Configuration Manager-Konsole in der betreffenden Sprache geöffnet

- Anderenfalls wird die Configuration Manager-Konsole in englischer Sprache (US-Englisch) geöffnet.

Angenommen, Sie installieren die Configuration Manager-Konsole von einem Standortserver aus, der die Sprachen Deutsch, Englisch und Französisch unterstützt. Wenn Sie die Configuration Manager-Konsole auf einem Computer mit der konfigurierten Spracheinstellung „Französisch“ öffnen, wird die Konsole in französischer Sprache geöffnet. Wenn Sie die Configuration Manager-Konsole auf einem Computer mit der konfigurierten Spracheinstellung „Japanisch“ öffnen, wird die Konsole in englischer Sprache geöffnet, da das japanische Sprachpaket nicht verfügbar ist.  

Jedes Mal, wenn die Configuration Manager-Konsole geöffnet wird, geschieht Folgendes:

- Die für den Computer konfigurierten Spracheinstellungen werden ermittelt.
- Es wird geprüft, ob ein zugeordnetes Sprachpaket für die Configuration Manager-Konsole verfügbar ist.
- Die Konsole wird mit dem entsprechenden Sprachpaket geöffnet.

Wenn Sie die Configuration Manager-Konsole unabhängig von den konfigurierten Spracheinstellungen des Computers in englischer Sprache öffnen möchten, müssen Sie die Sprachpaketdateien auf dem Computer entfernen oder umbenennen.

Wenden Sie die folgenden Verfahren an, um die Configuration Manager-Konsole unabhängig von der konfigurierten Gebietsschemaeinstellung des Computers in englischer Sprache zu öffnen.  

#### <a name="install-an-english-only-version-of-the-configuration-manager-console-on-computers"></a>Installieren von ausschließlich der englischen Version der Configuration Manager-Konsole auf Computern  

1. Navigieren Sie in Windows-Explorer zu `\Tools\ConsoleSetup\LanguagePack` im Configuration Manager-Installationspfad.

1. Benennen Sie die **.msp** - und **.mst** -Dateien um. Sie könnten beispielsweise **&lt;Dateiname\>.MSP** in **&lt;Dateiname\>.MSP.disabled** ändern.

1. Installieren Sie die Configuration Manager-Konsole auf dem Computer.

    > [!IMPORTANT]
    > Wenn für den Standortserver neue Serversprachen konfiguriert werden, werden die MSP- und MST-Dateien erneut in den Ordner **LanguagePack** kopiert, und Sie müssen dieses Verfahren wiederholen, um Configuration Manager-Konsolen nur auf Englisch zu installieren.  

#### <a name="temporarily-disable-a-console-language-on-an-existing-configuration-manager-console-installation"></a>Vorübergehendes Deaktivieren einer Konsolensprache bei einer vorhandenen Configuration Manager-Konsoleninstallation

1. Schließen Sie auf dem Computer, auf dem die Configuration Manager-Konsole ausgeführt wird, die Configuration Manager-Konsole.

1. Wechseln Sie in Windows Explorer auf dem Computer mit der Configuration Manager-Konsole zu &lt;*ConsoleInstallationPath*>\Bin\.  

1. Benennen Sie den entsprechenden Sprachordner für die Sprache um, die auf dem Computer konfiguriert ist. Wenn beispielsweise beim Computer die Spracheinstellung "Deutsch" konfiguriert ist, könnten Sie den Ordner **de** in **de.deaktiviert**umbenennen.  

1. Wenn Sie die Configuration Manager-Konsole wieder in der Sprache öffnen möchten, die für den Computer konfiguriert ist, benennen Sie den Ordner in den ursprünglichen Namen um. Benennen Sie beispielsweise **de.deaktiviert** wieder in **de**um.  

## <a name="configure-dcom-permissions-for-remote-consoles"></a><a name="BKMK_ConfigDCOMforRemoteConsole"></a> Konfigurieren von DCOM-Berechtigungen für Remotekonsolen

Für das Benutzerkonto, unter dem die Configuration Manager-Konsole ausgeführt wird, sind Berechtigungen für den Zugriff auf die Standortdatenbank über den SMS-Anbieter erforderlich. Administratoren, die eine Configuration Manager-Remotekonsole verwenden, benötigen zudem DCOM-Berechtigungen für eine **Remoteaktivierung** auf folgenden Computern:

- Den Standortservercomputer

- Jedem Computer, der eine Instanz des SMS-Anbieters hostet

Über die Sicherheitsgruppe **SMS-Administratoren** ist der Zugriff auf den SMS-Anbieter auf einem Computer möglich, und auch die erforderlichen DCOM-Berechtigungen können mithilfe dieser Gruppe gewährt werden. Wenn der SMS-Anbieter auf einem Mitgliedsserver ausgeführt wird, ist diese Gruppe eine lokale Computergruppe. Wenn der SMS-Anbieter auf einem Domänencontroller ausgeführt wird, ist diese Gruppe eine lokale Domänengruppe.

> [!IMPORTANT]
> Von der Configuration Manager-Konsole wird mithilfe von WMI eine Verbindung mit dem SMS-Anbieter hergestellt, wobei WMI intern DCOM verwendet. Wenn die Configuration Manager-Konsole auf einem anderen Computer als dem des SMS-Anbieters ausgeführt wird, benötigt sie Berechtigungen zur Aktivierung eines DCOM-Servers auf dem Computer des SMS-Anbieters. Die Berechtigung zur Remoteaktivierung wird standardmäßig nur den Mitgliedern der integrierten Gruppe Administratoren erteilt.
>
> Wenn Sie der Gruppe SMS-Administratoren die Berechtigung Remoteaktivierung erteilen, kann jedes Mitglied dieser Gruppe DCOM-Angriffe gegen den SMS-Anbietercomputer unternehmen. Zudem wird die Angriffsfläche des Computers durch diese Konfiguration erhöht. Überwachen Sie sorgfältig die Mitgliedschaften der Gruppe SMS-Administratoren, um dieses Risiko zu verringern.

Gehen Sie wie folgt vor, um die Standorte der zentralen Verwaltung, die primären Standortserver sowie alle Computer, auf denen der SMS-Anbieter installiert wird, für den Remotezugriff durch Administratoren mithilfe der Configuration Manager-Konsole zu konfigurieren.

### <a name="configure-dcom-permissions-for-remote-configuration-manager-console-connections"></a>Konfigurieren von DCOM-Berechtigungen für Remoteverbindungen der Configuration Manager-Konsole

1. Führen Sie als Administrator auf dem Zielcomputer `Dcomcnfg.exe` aus, um **Komponentendienste** zu öffnen.

1. Erweitern Sie nacheinander **Komponentendienste** und **Computer**, und wählen Sie dann **Arbeitsplatz** aus. Wählen Sie im Menü **Aktion** die Option **Eigenschaften** aus.

1. Wechseln Sie im Fenster **Computereigenschaften** auf die Registerkarte **COM-Sicherheit**. Wählen Sie im Bereich **Start- und Aktivierungsberechtigungen** die Option **Edit Limits** (Grenzwerte bearbeiten) aus.

1. Wählen Sie im Fenster **Start- und Aktivierungsberechtigungen** die Option **Hinzufügen** aus.

1. Geben Sie im Fenster **Benutzer, Computer, Dienstkonten oder Gruppen auswählen** im Feld **Geben Sie die zu verwenden Objektnamen ein** `SMS Admins` ein, und wählen Sie dann **OK**aus.

   > [!TIP]
   > Um die Gruppe der SMS-Administratoren zu suchen, müssen Sie möglicherweise die Einstellung ändern: **Suchpfad**. Wenn der SMS-Anbieter auf einem Mitgliedsserver ausgeführt wird, ist diese Gruppe eine lokale Computergruppe. Wenn der SMS-Anbieter auf einem Domänencontroller ausgeführt wird, ist diese Gruppe eine lokale Domänengruppe.

1. Wählen Sie im Abschnitt **Berechtigungen für SMS-Administratoren** die Spalte **Zulassen** für die Zeile **Remoteaktivierung**, um die Remoteaktivierung zu ermöglichen.

1. Klicken Sie auf **OK**, um die Änderungen zu speichern und alle Fenster zu schließen.

Ihr Computer ist jetzt für den Remotezugriff über die Configuration Manager-Konsole durch Mitglieder der Gruppe „SMS-Administratoren“ konfiguriert.

Wiederholen Sie dieses Verfahren auf jedem SMS-Anbietercomputer, durch den Configuration Manager-Remotekonsolen unterstützt werden.

## <a name="modify-the-site-database-configuration"></a><a name="bkmk_dbconfig"></a> Ändern der Konfiguration für die Standortdatenbank

Nachdem Sie einen Standort installiert haben, können Sie die Konfiguration der Standortdatenbank und des Standortdatenbankservers ändern. Führen Sie das Configuration Manager-Setup auf einem CAS-Server oder einem Primärstandortserver aus, um Änderungen vorzunehmen. Sie können die Standortdatenbank auf eine neue SQL Server-Instanz auf dem gleichen Computer oder auf einen anderen Computer verschieben, auf dem eine unterstützte Version von SQL Server ausgeführt wird. Diese Änderungen werden für die Datenbankkonfiguration an sekundären Standorten nicht unterstützt.

Weitere Informationen zu den Grenzen der Unterstützung finden Sie unter [Supportrichtlinie für manuelle Datenbankänderungen in einer Configuration Manager-Umgebung](https://support.microsoft.com/kb/3106512).  

> [!NOTE]
> Wenn Sie die Datenbankkonfiguration eines Standorts ändern, werden die Configuration Manager-Dienste auf dem Standortserver und den Systemservern von Remotestandorten, von denen aus Kommunikation mit der Datenbank erfolgt, von Configuration Manager neu gestartet oder neu installiert.

### <a name="modify-the-database-configuration"></a>Ändern der Datenbankkonfiguration

Führen Sie das Configuration Manager-Setup für den Standortserver aus, und wählen Sie die Option **Standortwartung durchführen oder diesen Standort zurücksetzen** aus. Wählen Sie dann die Option **SQL Server-Konfiguration ändern** aus. Sie können die folgenden Konfigurationen der Standortdatenbank ändern:

- Den Windows-basierten Server, auf dem die Datenbank gehostet wird

- Die SQL Server-Instanz, die auf einem Server verwendet wird, auf dem die SQL Server-Datenbank gehostet wird

- Der Datenbankname.

- SQL Server-Port wird von Configuration Manager verwendet.

- SQL Server Service Broker-Port wird von Configuration Manager verwendet.

### <a name="move-the-site-database"></a>Verschieben der Standortdatenbank

Wenn Sie die Standortdatenbank verschieben, überprüfen Sie ebenfalls die folgenden Konfigurationen:

- Wenn Sie die Standortdatenbank auf einen neuen Computer verschieben, fügen Sie das Computerkonto des Standortservers der lokalen Gruppe **Administratoren** auf dem Computer, auf dem SQL Server ausgeführt wird, hinzu. Wenn Sie für die Standortdatenbank einen SQL Server-Cluster verwenden, fügen Sie das Computerkonto der lokalen Gruppe **Administratoren** jedes Windows Server-Clusterknotencomputers hinzu.

- Wenn Sie die Standortdatenbank auf eine neue SQL Server-Instanz oder einen neuen SQL Server-Computer verschieben, aktivieren Sie die CLR-Integration (Common Language Runtime). Verwenden Sie **SQL Server Management Studio**, um eine Verbindung mit der SQL Server-Instanz herzustellen, die die Standortdatenbank hostet. Führen Sie dann die folgende gespeicherte Prozedur als Abfrage aus: `sp_configure 'clr enabled',1; reconfigure`

- Stellen Sie sicher, dass die neue SQL Server-Instanz Zugriff auf den Speicherort der Sicherung hat. Wenn Sie eine UNC zum Speichern einer Sicherung der Standortdatenbank verwenden, nachdem diese auf einen neuen Server verschoben wurde, müssen Sie sicherstellen, dass das Computerkonto der neuen SQL Server-Instanz über **Schreibberechtigungen** für den UNC-Standort verfügt. Diese Konfiguration ist enthalten, wenn Sie zu einer Always On-Verfügbarkeitsgruppe von SQL Server oder zu einem SQL Server-Cluster wechseln.

> [!IMPORTANT]
> Vor dem Verschieben einer Datenbank, die über mindestens ein Datenbankreplikat für Verwaltungspunkte verfügt, entfernen Sie zuerst die Datenbankreplikate. Nachdem das Verschieben der Datenbank abgeschlossen ist, können Sie die Datenbankreplikate neu konfigurieren. Weitere Informationen finden Sie unter [Datenbankreplikate für Verwaltungspunkte](../deploy/configure/database-replicas-for-management-points.md).

## <a name="manage-the-spn-for-the-site-database-server"></a><a name="bkmk_SPN"></a> Verwalten des SPN für den Standortdatenbankserver

Sie können das Konto auswählen, mit dem SQL-Dienste für die Standortdatenbank ausgeführt werden:

- Wenn die Dienste mit dem Systemkonto des Computers ausgeführt werden, wird der Dienstprinzipalname (SPN) automatisch für Sie registriert.

- Wenn die Dienste mit einem lokalen Domänenbenutzerkonto ausgeführt werden, registrieren Sie den SPN manuell. Das SPN ermöglicht es SQL-Clients und anderen Standortsystemen, sich mit Kerberos zu authentifizieren. Ohne Kerberos-Authentifizierung kann die Kommunikation mit der Datenbank fehlschlagen.

Weitere Informationen über SPNs und Kerberos-Verbindungen finden Sie unter [Registrieren eines Dienstprinzipalnamens für Kerberos-Verbindungen](https://docs.microsoft.com/sql/database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections).

Registrieren Sie einen SPN für das SQL Server-Dienstkonto des Standortdatenbankservers mithilfe des Tools **Setspn**. Führen Sie Setspn als Domänenadministrator auf einem Computer aus, der sich in derselben Domäne wie die SQL Server-Instanz befindet.

Die folgenden Prozeduren sind Beispiele, wie der SPN für das SQL Server-Dienstkonto verwaltet werden kann. Weitere Informationen zu Setspn finden Sie in der Übersicht zu [Setspn](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc731241\(v=ws.11\)).

### <a name="manually-create-a-domain-user-spn-for-the-sql-server-service-account"></a>Manuelles Erstellen eines Domänenbenutzer-SPN für das SQL Server-Dienstkonto

1. Öffnen Sie eine Eingabeaufforderung als Administrator.

1. Geben Sie einen gültigen Befehl ein, um den SPN sowohl für den NetBIOS-Namen als auch für den FQDN zu erstellen:

    > [!IMPORTANT]
    > Wenn Sie einen SPN für eine gruppierte SQL Server-Instanz erstellen, geben Sie den virtuellen Namen des SQL Server-Clusters als SQL Server-Computernamen an.

    - NetBIOS-Name: `setspn -A MSSQLSvc/<SQL Server computer name>:<port> <Domain\Account>`

        Beispiel: `setspn -A MSSQLSvc/sqlserver:1433 contoso\sqlservice`

    - FQDN: `setspn -A MSSQLSvc/<SQL Server FQDN>:<port> <Domain\Account>`

        Beispiel: `setspn -A MSSQLSvc/sqlserver.contoso.com:1433 contoso\sqlservice`

    > [!NOTE]
    > Der Befehl zum Registrieren eines SPN für eine benannte SQL Server-Instanz ist der gleiche wie zum Registrieren eines SPN für eine Standardinstanz. Allerdings muss die Portnummer mit der von der benannten Instanz verwendeten Portnummer übereinstimmen.

### <a name="verify-the-domain-user-spn-is-registered-correctly"></a>Überprüfen, ob der Domänenbenutzer-SPN richtig registriert ist

1. Öffnen Sie eine Eingabeaufforderung als Administrator.

1. Geben Sie den folgenden Befehl ein: `setspn -L <domain\SQL service account>`

    Beispiel: `setspn -L contoso\sqlservice`

1. Überprüfen Sie den registrierten **Dienstprinzipalnamen**. Stellen Sie sicher, dass Sie einen gültigen SPN für die SQL Server-Instanz erstellt haben.

### <a name="change-the-sql-server-service-account-from-local-system-to-a-domain-user-account"></a>Ändern des SQL Server-Dienstkontos von einem lokalen System in ein Domänenbenutzerkonto

1. Erstellen Sie ein Domänenbenutzerkonto oder ein lokales Systembenutzerkonto, das dann als SQL Server-Dienstkonto verwendet wird, oder wählen Sie es aus.

1. Öffnen Sie **SQL Server Configuration Manager**.

1. Wählen Sie **SQL Server-Dienste**, und öffnen Sie dann **SQL Server&lt;INSTANZNAME\>** .

1. Wechseln Sie zur Registerkarte **Anmelden**. Wählen Sie **Dieses Konto** aus, und geben Sie dann den Benutzernamen und das Kennwort für das Domänenbenutzerkonto aus Schritt 1 ein.

1. Bestätigen Sie die Änderung des Dienstkontos, und starten Sie den SQL Server-Dienst neu.

## <a name="run-a-site-reset"></a><a name="bkmk_reset"></a> Ausführen einer Standortrücksetzung

Wenn eine Standortrücksetzung an einem Standort der zentralen Verwaltung oder primären Standort ausgeführt wird, geschieht Folgendes:

- Die Configuration Manager-Standarddatei und die standardmäßigen Registrierungsberechtigungen werden erneut angewendet

- Alle Standortkomponenten und alle Standortsystemrollen werden neu installiert.

Sekundäre Standorte unterstützen keine Standortrücksetzung.

Sie können einen Standort manuell zurücksetzen. Zudem können Sie das Zurücksetzen automatisch ausführen, nachdem Sie die Standortkonfiguration geändert haben. Beispiel:

- Wenn sich die von Configuration Manager-Komponenten verwendeten Konten geändert haben, ist eine manuelle Standortzurücksetzung sinnvoll. Dadurch wird sichergestellt, dass die Standortkomponenten aktualisiert werden und die neuen Kontodaten verwenden.

- Wenn Sie die Sprachen für Client oder Server an einem Standort ändern, setzt Configuration Manager den Standort automatisch zurück. Dies ist erforderlich, um die neuen Sprachen an dem Standort verwenden zu können.

> [!NOTE]
> Beim Zurücksetzen des Standorts werden ausschließlich die Zugriffsberechtigungen für Configuration Manager-Objekte zurückgesetzt.

### <a name="what-happens-during-a-site-reset"></a>Was geschieht bei einer Standortrücksetzung?

Beim Zurücksetzen eines Standorts geschieht Folgendes:

1. Der Dienst **SMS_SITE_COMPONENT_MANAGER** und die Threadkomponenten des Diensts **SMS_EXECUTIVE** werden beendet und neu gestartet.

1. Der Freigabeordner des Standortsystems und die Komponente **SMS Executive** auf dem lokalen Computer und auf Remote-Standortsystemcomputern werden entfernt und neu erstellt.

1. Der Dienst **SMS_SITE_COMPONENT_MANAGER** wird neu gestartet, und von diesem Dienst werden die Dienste **SMS_EXECUTIVE** und **SMS_SQL_MONITOR** installiert.

Bei einer Standortrücksetzung werden folgende Objekte wiederhergestellt:

- Die Registrierungsschlüssel **SMS** oder **NAL** sowie alle diesen Schlüsseln untergeordneten Schlüssel

- Die Configuration Manager-Dateiverzeichnisstruktur sowie alle Standarddateien und -verzeichnisse in dieser Verzeichnisstruktur.

### <a name="prerequisites-for-site-reset"></a>Voraussetzungen für die Standortzurücksetzung

Das Konto, mit dem Sie einen Standort zurücksetzen, muss über folgende Berechtigungen verfügen:

- So setzen Sie den Standort der zentralen Verwaltung (CAS) zurück

  - Lokaler **Administrator** für den CAS-Server

  - Berechtigungen, die der Sicherheitsrolle **Hauptadministrator** für die rollenbasierte Verwaltung entsprechen

- So setzen Sie einen primären Standort zurück

  - Lokaler **Administrator** für den Server am primären Standort

  - Berechtigungen, die der Sicherheitsrolle **Hauptadministrator** für die rollenbasierte Verwaltung entsprechen
  
  - Wenn sich der primäre Standort in einer Hierarchie mit einem CAS befindet, muss dieses Konto auch ein lokaler **Administrator** auf dem CAS-Server sein.

### <a name="limitations-for-a-site-reset"></a>Einschränkungen für eine Standortrücksetzung

Wenn die Hierarchie so konfiguriert ist, dass sie [das Testen von Clientupgrades in einer Präproduktionssammlung](../../clients/manage/upgrade/test-client-upgrades.md) unterstützt, können Sie eine Standortrücksetzung nicht dazu verwenden, die Server- oder Clientsprachpakete an den Standorten zu ändern.

### <a name="run-a-site-reset"></a>Ausführen einer Standortrücksetzung

1. Starten Sie das Configuration Manager-Setup auf dem Standortserver, indem Sie einen der folgenden Schritte ausführen:

    - Klicken Sie im Menü **Start** auf **Setup für Configuration Manager**.

    - Öffnen Sie im Verzeichnis der *Installationsmedien* für Configuration Manager die Datei `\SMSSETUP\BIN\X64\setup.exe`. Stellen Sie sicher, dass diese Version mit der Version des Standorts übereinstimmt.

    - Öffnen Sie in dem Verzeichnis, in dem Configuration Manager *installiert* ist, die Datei `\BIN\X64\setup.exe`.

1. Wählen Sie auf der Seite **Erste Schritte** die Option **Standortwartung durchführen oder diesen Standort zurücksetzen** aus.

1. Wählen Sie auf der Seite **Standortwartung** die Option **Standort ohne Konfigurationsänderung zurücksetzen** aus.

1. Klicken Sie auf **Ja**, um mit dem Zurücksetzen des Standorts zu beginnen.

## <a name="manage-language-packs-at-a-site"></a><a name="bkmk_sitelang"></a> Verwalten von Sprachpaketen an einem Standort

Nach der Installation eines Standorts können Sie die verwendeten Sprachpakete für Server und Client ändern.

### <a name="server-language-packs"></a>Serversprachpakete

*Gilt für: Configuration Manager-Konsoleninstallationen, Neue Installationen von relevanten Standortsystemrollen*

Nach dem Aktualisieren der Serversprachpakete an einem Standort können Sie Configuration Manager-Konsolen die Unterstützung für die Sprachpakete hinzufügen.

Zum Hinzufügen der Unterstützung für ein Serversprachpaket zu einer Configuration Manager-Konsole installieren Sie die Configuration Manager-Konsole aus dem Ordner **ConsoleSetup** eines Standortservers, der das gewünschte Sprachpaket enthält. Falls die Configuration Manager-Konsole bereits installiert ist, müssen Sie sie zuerst deinstallieren, damit für die neue Installation die aktuelle Liste der unterstützten Sprachpakete identifiziert werden kann.

### <a name="client-language-packs"></a>Clientsprachpakete

Durch Änderungen an den Clientsprachpaketen werden die Quelldateien der Clientinstallation aktualisiert. Neue Clientinstallationen und -upgrades bieten Unterstützung für die aktualisierte Liste der Clientsprachen.

Nachdem Sie die Clientsprachpakete an einem Standort aktualisiert haben, installieren Sie jeden Client, von dem die Sprachpakete verwendet werden, mithilfe der Quelldateien mit den Clientsprachpaketen.

Weitere Informationen zu den von Configuration Manager unterstützten Client- und Serversprachen finden Sie unter [Sprachpakete](../deploy/install/language-packs.md).

### <a name="modify-the-supported-language-packs-at-a-site"></a>Ändern der unterstützten Sprachpakete an einem Standort

1. Starten Sie das Configuration Manager-Setup auf dem Standortserver, indem Sie einen der folgenden Schritte ausführen:

    - Klicken Sie im Menü **Start** auf **Setup für Configuration Manager**.

    - Öffnen Sie im Verzeichnis der *Installationsmedien* für Configuration Manager die Datei `\SMSSETUP\BIN\X64\setup.exe`. Stellen Sie sicher, dass diese Version mit der Version des Standorts übereinstimmt.

    - Öffnen Sie in dem Verzeichnis, in dem Configuration Manager *installiert* ist, die Datei `\BIN\X64\setup.exe`.

1. Wählen Sie auf der Seite **Erste Schritte** die Option **Standortwartung durchführen oder diesen Standort zurücksetzen** aus.

1. Wählen Sie auf der Seite **Standortwartung** die Option **Sprachkonfiguration ändern** aus.

1. Wählen Sie auf der Seite **Erforderliche Downloads** eine der folgenden Optionen aus:

    - **Erforderliche Dateien herunterladen**: Rufen Sie Updates für Sprachpakete ab.

    - **Zuvor heruntergeladene Dateien verwenden**: Verwenden Sie zuvor heruntergeladene Dateien, die die Sprachpakete enthalten, die Sie dem Standort hinzufügen möchten.

1. Wählen Sie auf der Seite **Serversprachauswahl** die Serversprachen aus, die vom Standort unterstützt werden.

1. Wählen Sie auf der Seite **Clientsprachauswahl** die Clientsprachen aus, die vom Standort unterstützt werden.

1. Schließen Sie den Assistenten ab, um die Sprachunterstützung am Standort zu ändern.

    > [!NOTE]
    > Configuration Manager initiiert das Zurücksetzen des Standorts, wobei auch alle Standortsystemrollen des Standorts neu installiert werden.

## <a name="modify-the-database-server-alert-threshold"></a><a name="BKMK_ModDBAlert"></a> Ändern des Warnungsschwellenwerts für Datenbankserver

Configuration Manager gibt standardmäßig Warnungen aus, wenn auf einem Standortdatenbankserver wenig Speicherplatz verfügbar ist:

- Warnung generieren, wenn 10 GB oder weniger freier Speicherplatz vorhanden sind
- Kritische Warnung generieren, wenn 5 GB oder weniger freier Speicherplatz vorhanden sind

Sie können diese Werte ändern oder die Warnungen für die einzelnen Standorte deaktivieren:

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie den Knoten **Standorte** aus.

1. Wählen Sie den Standort aus, den Sie konfigurieren möchten. Wählen Sie im Menüband **Eigenschaften** aus.

1. Wechseln Sie zur Registerkarte **Warnung**, und bearbeiten Sie dann die Einstellungen.

## <a name="uninstall-sites-and-hierarchies"></a>Deinstallieren von Standorten und Hierarchien

Möglicherweise müssen Sie Standortsystemrollen, Standorte oder Hierarchien in Configuration Manager deinstallieren. Weitere Informationen finden Sie unter [Deinstallieren von Rollen, Standorten und Hierarchien](../deploy/install/uninstall-sites-and-hierarchies.md).

Ab Version 2002 können Sie auch den CAS aus einer Hierarchie entfernen und gleichzeitig den primären Standort beibehalten. Weitere Informationen finden Sie unter [Entfernen des Standorts der zentralen Verwaltung](../deploy/install/remove-central-administration-site.md).
