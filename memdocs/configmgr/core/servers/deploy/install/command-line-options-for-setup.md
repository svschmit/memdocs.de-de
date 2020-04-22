---
title: Setup-Befehlszeilenoptionen
titleSuffix: Configuration Manager
description: Erstellen Sie Automatisierungsskripts, um Configuration Manager über die Befehlszeile zu installieren.
ms.date: 08/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0da167f1-52cf-4dfd-8f73-833ca3eb8478
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8e4950e32fa5ddc0a4fc1a13ec8e584dc1ae9ff3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700818"
---
# <a name="command-line-options-for-configuration-manager-setup"></a>Befehlszeilenoptionen für Setup für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Verwenden Sie die folgenden Informationen, um Skripts zu konfigurieren oder Configuration Manager über die Befehlszeile zu installieren.  

## <a name="command-line-options-for-setup"></a><a name="bkmk_setup"></a> Befehlszeilenoptionen für das Setup

Führen Sie Setup aus dem `\BIN\X64`-Verzeichnis aus, das sich auf dem Standortserver im Configuration Manager-Installationspfad befindet.

### `/DEINSTALL`

Deinstallieren Sie den Standort. Führen Sie das Setup vom Standortservercomputer aus.  

### `/DONTSTARTSITECOMP`

Installieren Sie einen Standort, ohne dass der Standortkomponenten-Manager-Dienst gestartet wird. Der Standort wird erst beim Start des Standortkomponenten-Manager-Diensts aktiv. Der Standortkomponenten-Manager ist für die Installation und den Start des Diensts SMS_Executive und für weitere Prozesse am Standort verantwortlich. Wenn Sie den Standortkomponenten-Manager-Dienst nach Abschluss der Standortinstallation starten, werden der Dienst SMS_Executive sowie weitere Prozesse installiert, die für den Betrieb des Standorts erforderlich sind.  

### `/HIDDEN`

Blenden Sie die Benutzeroberfläche beim Setup aus. Verwenden Sie diese Option nur in Verbindung mit der Option **/SCRIPT**. Die Skriptdatei zur unbeaufsichtigten Installation muss alle erforderlichen Optionen bereitstellen, oder das Setup schlägt fehl.  

### `/NOUSERINPUT`

Deaktivieren Sie die Benutzereingabe während des Setups, der Setup-Assistent wird aber trotzdem angezeigt. Verwenden Sie diese Option nur in Verbindung mit der Option **/SCRIPT**. Die Skriptdatei zur unbeaufsichtigten Installation muss alle erforderlichen Optionen bereitstellen, oder das Setup schlägt fehl.  

### `/RESETSITE`

Führen Sie eine Standortrücksetzung aus, bei der die Datenbank und Dienstkonten des Standorts zurückgesetzt werden.

Weitere Informationen finden Sie unter [Ausführen einer Standortrücksetzung](../../manage/modify-your-infrastructure.md#bkmk_reset).  

### `/TESTDBUPGRADE`

Führen Sie einen Test für die Sicherung der Standortdatenbank aus, um sicherzustellen, dass für die Datenbank ein Upgrade durchgeführt werden kann.

> [!IMPORTANT]  
> Führen Sie diese Befehlszeilenoption nicht für die Datenbank Ihres Produktionsstandorts aus. Wenn Sie diese Befehlszeilenoption für die Datenbank des Produktionsstandorts ausführen, wird ein Upgrade auf die Standortdatenbank durchgeführt und Ihr Standort kann außer Funktion gesetzt werden.

#### <a name="usage"></a>Verwendung

Stellen Sie den Instanznamen und den Datenbanknamen der Standortdatenbank bereit. Wenn Sie nur den Datenbanknamen angeben, wird automatisch der Standardinstanzname verwendet.  

`/TESTDBUPGRADE <Instance name>\<Database name>`

`/TESTDBUPGRADE CM_ABC`

`/TESTDBUPGRADE Named\CM_ABC`

### `/UPGRADE`

Führen Sie ein unbeaufsichtigtes Upgrade eines Standorts aus. Geben Sie den Product Key samt den Bindestrichen (`-`) ein. Geben Sie außerdem den Pfad zu den zuvor heruntergeladenen und für das Setup erforderlichen Dateien an.  

Weitere Informationen zu den für das Setup erforderlichen Dateien finden Sie unter [Setup-Downloadprogramm](setup-downloader.md).  

#### <a name="usage"></a>Verwendung

`setupwpf.exe /UPGRADE xxxxx-xxxxx-xxxxx-xxxxx-xxxxx <path to external component files>`  

### `/SCRIPT`

Führen Sie eine unbeaufsichtigte Installation aus. Verwenden Sie eine Setup-Initialisierungsdatei mit dieser Option. Weitere Informationen zur unbeaufsichtigten Installation finden Sie unter [Verwenden einer Befehlszeile zum Installieren von System Center Configuration Manager-Standorten](use-a-command-line-to-install-sites.md).  

#### <a name="usage"></a>Verwendung

`/SCRIPT <setup script path>`

### `/SDKINST`

Installieren Sie den SMS-Anbieter auf dem angegebenen Computer. Stellen Sie den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) für den SMS-Anbietercomputer bereit. Weiter Informationen zum SMS-Anbieter finden Sie unter [Planen des SMS-Anbieters](../../../plan-design/hierarchy/plan-for-the-sms-provider.md).  

#### <a name="usage"></a>Verwendung

`/SDKINST <SMS Provider FQDN>`

### `/SDKDEINST`

Deinstallieren Sie den SMS-Anbieter auf dem angegebenen Computer. Stellen Sie den FQDN für den SMS-Anbietercomputer bereit.  

#### <a name="usage"></a>Verwendung

`/SDKDEINST <SMS Provider FQDN>`

### `/MANAGELANGS`

Verwalten Sie die Sprachen, die an einem zuvor installierten Standort installiert wurden. Stellen Sie den Speicherort der Sprachskriptdatei bereit, die die Spracheinstellungen enthält. Weitere Informationen finden Sie im Abschnitt [Befehlszeilenoptionen zum Verwalten von Sprachen](#bkmk_Lang).  

#### <a name="usage"></a>Verwendung

`/MANAGELANGS <Language script path>`


## <a name="command-line-options-to-manage-languages"></a><a name="bkmk_Lang"></a> Befehlszeilenoptionen zum Verwalten von Sprachen

### <a name="identification"></a>Identification

- **Schlüsselname:** Aktion  

    - **Erforderlich:** Ja  

    - **Werte:** `ManageLanguages`  

    - **Details:** Damit wird die Sprachunterstützung für Server, Clients und mobile Clients verwaltet.  

### <a name="options"></a>Optionen

- **Schlüsselname:** AddServerLanguages  

    - **Erforderlich:** Nein  

    - **Werte:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK oder ZHH  

    - **Details:** Hiermit werden die Serversprachen angegeben, die für die Configuration Manager-Konsole, Berichte und Configuration Manager-Objekte verfügbar sein werden. Englisch ist standardmäßig verfügbar.  

- **Schlüsselname:** AddClientLanguages  

    - **Erforderlich:** Nein  

    - **Werte:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK oder ZHH  

    - **Details:** Damit werden die Sprachen angegeben, die auf Clientcomputern zur Verfügung stehen werden. Englisch ist standardmäßig verfügbar.  

- **Schlüsselname:** DeleteServerLanguages  

    - **Erforderlich:** Nein  

    - **Werte:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK oder ZHH  

    - **Details:** Gibt die zu entfernenden Sprachen an, die dann nicht mehr für die Configuration Manager-Konsole, Berichte und Configuration Manager-Objekte verfügbar sind. Englisch ist standardmäßig verfügbar. Sie können diese Sprache nicht entfernen.  

- **Schlüsselname:** DeleteClientLanguages  

    - **Erforderlich:** Nein  

    - **Werte:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK oder ZHH  

    - **Details:** Gibt die zu entfernenden Sprachen an, die dann nicht mehr für Clientcomputer verfügbar sind. Englisch ist standardmäßig verfügbar. Sie können diese Sprache nicht entfernen.  

- **Schlüsselname:** MobileDeviceLanguage  

    - **Erforderlich:** Ja  

    - **Werte:**

        - `0` = nicht installieren  

        - `1` = installieren  

    - **Details:** Hiermit wird angegeben, ob die Sprachen für mobile Geräteclients installiert sind.  

- **Schlüsselname:** PrerequisiteComp  

    - **Erforderlich:** Ja  

    - **Werte:**

        - `0` = herunterladen  

        - `1` = bereits heruntergeladen  

    - **Details:** Gibt an, ob die für das Setup erforderlichen Dateien bereits heruntergeladen wurden. Wenn Sie beispielsweise den Wert `0` angeben, werden die Dateien von Setup heruntergeladen.  

- **Schlüsselname:** PrerequisitePath  

    - **Erforderlich:** Ja  

    - **Werte:**  <*Pfad zu den für das Setup erforderlichen Dateien*>  

    - **Details:** Gibt den Pfad zu den für das Setup erforderlichen Dateien an. Je nach **PrerequisiteComp**-Wert wird dieser Pfad beim Setup zum Speichern heruntergeladener Dateien oder zum Suchen der zuvor heruntergeladenen Dateien verwendet.  


## <a name="unattended-setup-script-file-keys"></a><a name="bkmk_Unattended"></a> Skriptdateischlüssel für eine unbeaufsichtigte Installation

In den folgenden Abschnitten erfahren Sie, wie Sie ein Skript für die unbeaufsichtigte Installation erstellen. Den Listen ist Folgendes zu entnehmen:

- Die verfügbaren Setupskriptschlüssel und deren entsprechende Werte
- Ob die Schlüssel erforderlich sind
- Für welchen Installationstyp die Schlüssel verwendet werden
- Eine kurze Beschreibung des jeweiligen Schlüssels

### <a name="unattended-install-for-a-central-administration-site-cas"></a>Unbeaufsichtigtes Installieren eines Standorts der zentralen Verwaltung

Verwenden Sie die folgenden Detailinformationen, um einen Standort der zentralen Verwaltung über eine Skriptdatei für unbeaufsichtigte Installation zu installieren.  

#### <a name="identification"></a>Identification

- **Schlüsselname:** Aktion  

    - **Erforderlich:** Ja  

    - **Werte:** `InstallCAS`  

    - **Details:** Installiert einen Standort der zentralen Verwaltung.  

- **Schlüsselname:** CDLatest  

    - **Erforderlich:** Ja, aber nur bei Verwendung von Medien aus dem Ordner „CD.Latest“.

    - **Werte:**

        - `1` = Sie verwenden Medien aus „CD.Latest“.

        - Ein Wert ungleich 1 = Sie verwenden keine „CD.Latest“-Medien.

    - **Details:** Wenn Sie einen primären Standort oder einen Standort der zentralen Verwaltung installieren oder wiederherstellen, und wenn Sie Setup aus dem Ordner „CD.Latest“ ausführen, schließen Sie diesen Schlüssel und diesen Wert ein. Dieser Wert informiert Setup darüber, dass Sie Medien aus „CD.Latest“ verwenden.

#### <a name="options"></a>Optionen

- **Schlüsselname:** ProductID  

    - **Erforderlich:** Ja  

    - **Werte:**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>` = ein gültiger Product Key mit Bindestrichen

        - `Eval` = Installieren der Evaluierungsversion von Configuration Manager

    - **Details:** Gibt den Product Key für die Configuration Manager-Installation, einschließlich der Gedankenstriche, an.

- **Schlüsselname:** SiteCode  

    - **Erforderlich:** Ja  

    - **Werte:**  <*Standortcode*>, beispielsweise `ABC`

    - **Details:** Gibt drei alphanumerische Zeichen an, durch die der Standort in der Hierarchie eindeutig angegeben wird.  

- **Schlüsselname:** Standortname  

    - **Erforderlich:** Ja  

    - **Werte:**  <*Standortname*>  

    - **Details:** Gibt den Namen für diesen Standort an.  

- **Schlüsselname:** SMSInstallDir  

    - **Erforderlich:** Ja  

    - **Werte:**  <*Configuration Manager-Installationspfad*>  

    - **Details:** Gibt den Installationsordner für die Configuration Manager-Programmdateien an.  

- **Schlüsselname:** SDKServer  

    - **Erforderlich:** Ja  

    - **Werte:**  <*SMS-Anbieter-FQDN*>  

    - **Details:** Hiermit wird der FQDN des Servers angegeben, auf dem der SMS-Anbieter gehostet wird. Nach der Erstinstallation können Sie zusätzliche SMS-Anbieter für den Standort konfigurieren.  

- **Schlüsselname:** PrerequisiteComp  

    - **Erforderlich:** Ja  

    - **Werte:**

        - `0` = herunterladen  

        - `1` = bereits heruntergeladen  

    - **Details:** Gibt an, ob die für das Setup erforderlichen Dateien bereits heruntergeladen wurden. Wenn Sie beispielsweise den Wert `0` angeben, werden die Dateien von Setup heruntergeladen.  

- **Schlüsselname:** PrerequisitePath  

    - **Erforderlich:** Ja  

    - **Werte:**  <*Pfad zu den für das Setup erforderlichen Dateien*>  

    - **Details:** Gibt den Pfad zu den für das Setup erforderlichen Dateien an. Je nach **PrerequisiteComp**-Wert wird dieser Pfad beim Setup zum Speichern heruntergeladener Dateien oder zum Suchen der zuvor heruntergeladenen Dateien verwendet.  

- **Schlüsselname:** AdminConsole  

    - **Erforderlich:** Ja  

    - **Werte:**

        - `0` = nicht installieren  

        - `1` = installieren  

    - **Details:** Damit wird angegeben, ob die Configuration Manager-Konsole installiert werden soll.  

- **Schlüsselname:** JoinCEIP  

    > [!Note]  
    > Ab Configuration Manager Version 1802 ist das CEIP-Feature nicht mehr im Produkt enthalten.

    - **Erforderlich:** Ja  

    - **Werte:**

        - `0` = nicht teilnehmen  

        - `1` = teilnehmen  

    - **Details:** Hiermit wird angegeben, ob Sie am Programm zur Verbesserung der Benutzerfreundlichkeit (CEIP) teilnehmen möchten.  

- **Schlüsselname:** AddServerLanguages  

    - **Erforderlich:** Nein  

    - **Werte:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK oder ZHH  

    - **Details:** Hiermit werden die Serversprachen angegeben, die für die Configuration Manager-Konsole, Berichte und Configuration Manager-Objekte verfügbar sein werden. Englisch ist standardmäßig verfügbar.  

- **Schlüsselname:** AddClientLanguages  

    - **Erforderlich:** Nein  

    - **Werte:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK oder ZHH  

    - **Details:** Damit werden die Sprachen angegeben, die auf Clientcomputern zur Verfügung stehen werden. Englisch ist standardmäßig verfügbar.  

- **Schlüsselname:** DeleteServerLanguages  

    - **Erforderlich:** Nein  

    - **Werte:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK oder ZHH  

    - **Details:** Damit wird ein Standort nach dessen Installation geändert. Gibt die zu entfernenden Sprachen an, die dann nicht mehr für die Configuration Manager-Konsole, Berichte und Configuration Manager-Objekte verfügbar sind. Englisch ist standardmäßig verfügbar. Sie können diese Sprache nicht entfernen.  

- **Schlüsselname:** DeleteClientLanguages  

    - **Erforderlich:** Nein  

    - **Werte:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK oder ZHH  

    - **Details:** Damit wird ein Standort nach dessen Installation geändert. Gibt die zu entfernenden Sprachen an, die dann nicht mehr für Clientcomputer verfügbar sind. Englisch ist standardmäßig verfügbar. Sie können diese Sprache nicht entfernen.  

- **Schlüsselname:** MobileDeviceLanguage  

    - **Erforderlich:** Ja  

    - **Werte:**

        - `0` = nicht installieren  

        - `1` = installieren  

    - **Details:** Hiermit wird angegeben, ob die Sprachen für mobile Geräteclients installiert sind.  

#### <a name="sqlconfigoptions"></a>SQLConfigOptions

- **Schlüsselname:** SQLServerName  

    - **Erforderlich:** Ja  

    - **Werte:**  <*SQL Server-Name*>  

    - **Details:** Gibt den Namen des Servers oder der gruppierten Instanz an, auf dem bzw. in der SQL Server ausgeführt wird, um die Standortdatenbank zu hosten.  

- **Schlüsselname:** DatabaseName  

    - **Erforderlich:** Ja  

    - **Werte:**  <*Standortdatenbankname*> oder <*Instanzname*>\\<*Standortdatenbankname*>  

    - **Details:** Gibt den Namen der SQL Server-Datenbank an, die erstellt oder verwendet werden soll, wenn Setup die Datenbank für den Standort der zentralen Verwaltung installiert.  

        > [!IMPORTANT]  
        > Wenn Sie nicht die Standardinstanz verwenden, geben Sie den Instanznamen und den Namen der Standortdatenbank an.  

- **Schlüsselname:** SQLSSBPort  

    - **Erforderlich:** Nein  

    - **Werte:**  <*SSB-Portnummer*>  

    - **Details:** Gibt den SSB-Port (SQL Server Service Broker) an, der von SQL Server verwendet wird. Standardmäßig wird für SSB der TCP-Port 4022 verwendet, Sie können aber einen anderen Port verwenden.  

- **Schlüsselname:** SQLDataFilePath  

    - **Erforderlich:** Nein  

    - **Werte:**  <*Pfad zur .mdb-Datenbankdatei*>  

    - **Details:** Hiermit wird ein alternativer Speicherort zum Erstellen der MDB-Datei für die Datenbank angegeben.  

- **Schlüsselname:** SQLLogFilePath  

    - **Erforderlich:** Nein  

    - **Werte:**  <*Pfad zur .ldf-Datenbankdatei*>  

    - **Details:** Hiermit wird ein alternativer Speicherort zum Erstellen der LDF-Datei für die Datenbank angegeben.  

#### <a name="cloudconnectoroptions"></a>CloudConnectorOptions

- **Schlüsselname:** CloudConnector  

    - **Erforderlich:** Ja  

    - **Werte:**

        - `0` = nicht installieren  

        - `1` = installieren  

    - **Details:** Gibt an, ob ein Dienstverbindungspunkt an diesem Standort installiert werden soll. Da Sie den Dienstverbindungspunkt nur im obersten Standort einer Hierarchie installieren können, legen Sie diesen Wert für einen untergeordneten primären Standort auf `1` fest.  

- **Schlüsselname:** CloudConnectorServer  

    - **Erforderlich:** Erforderlich, wenn **CloudConnector** gleich 1 ist  

    - **Werte:**  <*FQDN des Servers für den Dienstverbindungspunkt*>  

    - **Details:** Hiermit wird der FQDN des Servers angegeben, auf dem die Standortsystemrolle „Dienstverbindungspunkt“ gehostet wird.  

- **Schlüsselname:** UseProxy  

    - **Erforderlich:** Erforderlich, wenn **CloudConnector** gleich 1 ist  

    - **Werte:**

        - `0` = nicht installieren  

        - `1` = installieren  

    - **Details:** Gibt an, ob der Dienstverbindungspunkt einen Proxyserver verwendet.  

- **Schlüsselname:** ProxyName  

    - **Erforderlich:** Erforderlich, wenn **UseProxy** gleich 1 ist  

    - **Werte:**  <*Proxyserver-FQDN*>  

    - **Details:** Hiermit wird der FQDN des Proxyservers angegeben, der von dem Dienstverbindungspunkt verwendet wird.  

- **Schlüsselname:** ProxyPort  

    - **Erforderlich:** Erforderlich, wenn **UseProxy** gleich 1 ist  

    - **Werte:**  <*Portnummer*>  

    - **Details:** Gibt die für den Proxyport zu verwendende Portnummer an.  

#### <a name="sabranchoptions"></a>SABranchOptions

<!-- SCCMDocs#390 -->

- **Schlüsselname:** SAActive

    - **Erforderlich:** Nein

    - **Werte:**

        - `0` = Sie haben Software Assurance nicht.

        - `1` = Software Assurance ist aktiv.

    - **Details:** Geben Sie an, ob Software Assurance bei Ihnen aktiv ist. Weitere Informationen finden Sie unter [Häufig gestellte Fragen für die Configuration Manager-Verzweigungen und -Lizenzierungen](../../../understand/product-and-licensing-faq.md).

- **Schlüsselname:** CurrentBranch

    - **Erforderlich:** Nein

    - **Werte:**

        - `0` = den LTSB installieren

        - `1` = aktuellen Branch installieren

    - **Details:** Geben Sie an, ob für Configuration Manager der aktuelle Branch oder der Long-Term Servicing Branch (LTSB) verwendet werden soll. Weitere Informationen hierzu finden Sie unter [Welcher Branch von Configuration Manager soll verwendet werden?](../../../understand/which-branch-should-i-use.md).

### <a name="unattended-install-for-a-primary-site"></a>Unbeaufsichtigtes Installieren eines primären Standorts

Im folgenden Abschnitt finden Sie Detailinformationen eines primären Standorts mithilfe einer Skriptdatei zur unbeaufsichtigten Installation.  

#### <a name="identification"></a>Identification

- **Schlüsselname:** Aktion  

    - **Erforderlich:** Ja  

    - **Werte:** `InstallPrimarySite`  

    - **Details:** Installiert einen primären Standort.  

- **Schlüsselname:** CDLatest  

    - **Erforderlich:** Ja, aber nur bei Verwendung von Medien aus dem Ordner „CD.Latest“.

    - **Werte:**

        - `1` = Sie verwenden Medien aus „CD.Latest“.

        - Ein Wert ungleich 1 = Sie verwenden keine „CD.Latest“-Medien.

    - **Details:** Wenn Sie einen primären Standort oder einen Standort der zentralen Verwaltung installieren oder wiederherstellen, und wenn Sie Setup aus dem Ordner „CD.Latest“ ausführen, schließen Sie diesen Schlüssel und diesen Wert ein. Dieser Wert informiert Setup darüber, dass Sie Medien aus „CD.Latest“ verwenden.

#### <a name="options"></a>Optionen

- **Schlüsselname:** ProductID  

    - **Erforderlich:** Ja  

    - **Werte:**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>` = ein gültiger Product Key mit Bindestrichen

        - `Eval` = Installieren der Evaluierungsversion von Configuration Manager

    - **Details:** Gibt den Product Key für die Configuration Manager-Installation, einschließlich der Gedankenstriche, an.

- **Schlüsselname:** SiteCode  

    - **Erforderlich:** Ja  

    - **Werte:**  <*Standortcode*>  

    - **Details:** Gibt drei alphanumerische Zeichen an, durch die der Standort in der Hierarchie eindeutig angegeben wird.  

- **Schlüsselname:** SiteName  

    - **Erforderlich:** Ja  

    - **Werte:**  <*Standortname*>  

    - **Details:** Gibt den Namen für diesen Standort an.  

- **Schlüsselname:** SMSInstallDir  

    - **Erforderlich:** Ja  

    - **Werte:**  <*Configuration Manager-Installationspfad*>

    - **Details:** Gibt den Installationsordner für die Configuration Manager-Programmdateien an.  

- **Schlüsselname:** SDKServer  

    - **Erforderlich:** Ja  

    - **Werte:**  <*SMS-Anbieter-FQDN*>  

    - **Details:** Hiermit wird der FQDN des Servers angegeben, auf dem der SMS-Anbieter gehostet wird. Nach der Erstinstallation können Sie zusätzliche SMS-Anbieter für den Standort konfigurieren.  

- **Schlüsselname:** PrerequisiteComp  

    - **Erforderlich:** Ja  

    - **Werte:**

        - `0` = herunterladen  

        - `1` = bereits heruntergeladen  

    - **Details:** Gibt an, ob die für das Setup erforderlichen Dateien bereits heruntergeladen wurden. Wenn Sie beispielsweise den Wert `0` angeben, werden die Dateien von Setup heruntergeladen.  

- **Schlüsselname:** PrerequisitePath  

    - **Erforderlich:** Ja  

    - **Werte:**  <*Pfad zu den für das Setup erforderlichen Dateien*>  

    - **Details:** Gibt den Pfad zu den für das Setup erforderlichen Dateien an. Je nach **PrerequisiteComp**-Wert wird dieser Pfad beim Setup zum Speichern heruntergeladener Dateien oder zum Suchen der zuvor heruntergeladenen Dateien verwendet.  

- **Schlüsselname:** AdminConsole  

    - **Erforderlich:** Ja  

    - **Werte:**

        - `0` = nicht installieren  

        - `1` = installieren  

    - **Details:** Damit wird angegeben, ob die Configuration Manager-Konsole installiert werden soll.  

- **Schlüsselname:** JoinCEIP  

    > [!Note]  
    > Ab Configuration Manager Version 1802 ist das CEIP-Feature nicht mehr im Produkt enthalten.

    - **Erforderlich:** Ja  

    - **Werte:**

        - `0` = nicht teilnehmen  

        - `1` = teilnehmen  

    - **Details:** Gibt an, ob am Programm zur Verbesserung der Benutzerfreundlichkeit (CEIP) teilgenommen werden soll.  

- **Schlüsselname:** ManagementPoint  

    - **Erforderlich:** Nein  

    - **Werte:**  <*FQDN des Verwaltungspunkt-Standortservers*>  

    - **Details:** Gibt den FQDN des Servers an, auf dem die Standortsystemrolle „Verwaltungspunkt“ gehostet wird.  

- **Schlüsselname:** ManagementPointProtocol  

    - **Erforderlich:** Nein  

    - **Werte:** `HTTPS` oder `HTTP`  

    - **Details:** Gibt das für den Verwaltungspunkt zu verwendende Protokoll an.  

- **Schlüsselname:** DistributionPoint  

    - **Erforderlich:** Nein  

    - **Werte:**  <*FQDN des Verteilungspunkt-Standortservers*>  

    - **Details:** Gibt den FQDN des Servers an, auf dem die Standortsystemrolle „Verteilungspunkt“ gehostet wird.  

- **Schlüsselname:** DistributionPointProtocol  

    - **Erforderlich:** Nein  

    - **Werte:** `HTTPS` oder `HTTP`  

    - **Details:** Gibt das für den Verteilungspunkt zu verwendende Protokoll an.  

- **Schlüsselname:** RoleCommunicationProtocol  

    - **Erforderlich:** Ja  

    - **Werte:** `EnforceHTTPS` oder `HTTPorHTTPS`  

    - **Details:** Mit diesem Schlüssel wird angegeben, ob alle Standortsysteme so konfiguriert werden sollen, dass ausschließlich HTTPS-Kommunikation von Clients akzeptiert wird, oder ob die Kommunikationsmethode für jede Standortsystemrolle konfiguriert werden muss. Wenn Sie `EnforceHTTPS` auswählen, müssen Clients ein gültiges Public Key-Infrastruktur-Zertifikat (PKI) für die Clientauthentifizierung haben.  

- **Schlüsselname:** ClientsUsePKICertificate  

    - **Erforderlich:** Ja  

    - **Werte:**

        - `0` = nicht verwenden  

        - `1` = verwenden  

    - **Details:** Hiermit wird angegeben, ob für die Kommunikation zwischen Clients und Standortsystemrollen ein PKI-Clientzertifikat verwendet werden soll.  

- **Schlüsselname:** AddServerLanguages  

    - **Erforderlich:** Nein  

    - **Werte:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK oder ZHH  

    - **Details:** Hiermit werden die Serversprachen angegeben, die für die Configuration Manager-Konsole, Berichte und Configuration Manager-Objekte verfügbar sein werden. Englisch ist standardmäßig verfügbar.  

- **Schlüsselname:** AddClientLanguages  

    - **Erforderlich:** Nein  

    - **Werte:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK oder ZHH  

    - **Details:** Damit werden die Sprachen angegeben, die auf Clientcomputern zur Verfügung stehen werden. Englisch ist standardmäßig verfügbar.  

- **Schlüsselname:** DeleteServerLanguages  

    - **Erforderlich:** Nein  

    - **Werte:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK oder ZHH  

    - **Details:** Damit wird ein Standort nach dessen Installation geändert. Gibt die zu entfernenden Sprachen an, die dann nicht mehr für die Configuration Manager-Konsole, Berichte und Configuration Manager-Objekte verfügbar sind. Englisch ist standardmäßig verfügbar. Sie können diese Sprache nicht entfernen.  

- **Schlüsselname:** DeleteClientLanguages  

    - **Erforderlich:** Nein  

    - **Werte:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK oder ZHH  

    - **Details:** Damit wird ein Standort nach dessen Installation geändert. Gibt die zu entfernenden Sprachen an, die dann nicht mehr für Clientcomputer verfügbar sind. Englisch ist standardmäßig verfügbar. Sie können diese Sprache nicht entfernen.  

- **Schlüsselname:** MobileDeviceLanguage  

    - **Erforderlich:** Ja  

    - **Werte:**

        - `0` = nicht installieren  

        - `1` = installieren  

    - **Details:** Hiermit wird angegeben, ob die Sprachen für mobile Geräteclients installiert sind.  

#### <a name="sqlconfigoptions"></a>SQLConfigOptions

- **Schlüsselname:** SQLServerName  

    - **Erforderlich:** Ja  

    - **Werte:**  <*SQL Server-Name*>  

    - **Details:** Gibt den Namen des Servers oder der gruppierten Instanz an, auf dem bzw. in der SQL Server ausgeführt wird, um die Standortdatenbank zu hosten.  

- **Schlüsselname:** DatabaseName  

    - **Erforderlich:** Ja  

    - **Werte:**  <*Standortdatenbankname*> oder <*Instanzname*>\\<*Standortdatenbankname*>  

    - **Details:** Gibt den Namen der SQL Server-Datenbank an, der bei der Installation der primären Standortdatenbank erstellt oder verwendet werden soll.  

        > [!IMPORTANT]  
        > Wenn Sie nicht die Standardinstanz verwenden, geben Sie den Instanznamen und den Namen der Standortdatenbank an.  

- **Schlüsselname:** SQLSSBPort  

    - **Erforderlich:** Nein  

    - **Werte:**  <*SSB-Portnummer*>  

    - **Details:** Gibt den SSB-Port an, der von SQL Server verwendet wird. Standardmäßig wird für SSB der TCP-Port 4022 verwendet, Sie können aber einen anderen Port verwenden.  

- **Schlüsselname:** SQLDataFilePath  

    - **Erforderlich:** Nein  

    - **Werte:**  <*Pfad zur .mdb-Datenbankdatei*>  

    - **Details:** Hiermit wird ein alternativer Speicherort zum Erstellen der MDB-Datei für die Datenbank angegeben.  

- **Schlüsselname:** SQLLogFilePath  

    - **Erforderlich:** Nein  

    - **Werte:**  <*Pfad zur .ldf-Datenbankdatei*>  

    - **Details:** Hiermit wird ein alternativer Speicherort zum Erstellen der LDF-Datei für die Datenbank angegeben.  

#### <a name="hierarchyexpansionoption"></a>HierarchyExpansionOption

- **Schlüsselname:** CCARSiteServer  

    - **Erforderlich:** Nein  

    - **Werte:**  <*FQDN des Standorts der zentralen Verwaltung*>  

    - **Details:** Gibt den Standort der zentralen Verwaltung an, dem ein primärer Standort zugeordnet wird, wenn er in die Configuration Manager-Hierarchie eingebunden wird. Geben Sie den Standort der zentralen Verwaltung während des Setups an.  

- **Schlüsselname:** CASRetryInterval  

    - **Erforderlich:** Nein  

    - **Werte:**  <*Intervall in Minuten*>  

    - **Details:** Gibt das Wiederholungsintervall (in Minuten) an, nach dem nach einem Verbindungsfehler versucht werden soll, erneut eine Verbindung mit dem Standort der zentralen Verwaltung herzustellen. Tritt beispielsweise beim Herstellen einer Verbindung mit dem Standort der zentralen Verwaltung (Central Administration Site, CAS) ein Fehler auf, wird am primären Standort entsprechend der Anzahl von Minuten, die Sie für **CASRetryInterval** angegeben haben, gewartet, bevor erneut versucht wird, die Verbindung herzustellen.  

- **Schlüsselname:** WaitForCASTimeout  

    - **Erforderlich:** Nein  

    - **Werte:**  <*Timeout in Minuten von 0 bis 100*>  

    - **Details:** Gibt den maximalen Timeoutwert (in Minuten) an, bis zu dem ein primärer Standort versucht, eine Verbindung mit dem Standort der zentralen Verwaltung (Central Administration Site, CAS) herzustellen. Kann ein primärer Standort beispielsweise keine Verbindung mit einem CAS herstellen, versucht der primäre Standort wiederholt eine Verbindungsherstellung mit dem CAS entsprechend dem **CASRetryInterval**-Wert, bis der für **WaitForCASTimeout** angegebene Zeitraum abgelaufen ist. Sie können einen Wert von `0` bis `100` angeben.  

#### <a name="cloudconnectoroptions"></a>CloudConnectorOptions

- **Schlüsselname:** CloudConnector  

    - **Erforderlich:** Ja  

    - **Werte:**

        - `0` = nicht installieren  

        - `1` = installieren  

    - **Details:** Gibt an, ob ein Dienstverbindungspunkt an diesem Standort installiert werden soll. Da Sie den Dienstverbindungspunkt nur im obersten Standort einer Hierarchie installieren können, legen Sie diesen Wert für einen untergeordneten primären Standort auf `0` fest.  

- **Schlüsselname:** CloudConnectorServer  

    - **Erforderlich:** Erforderlich, wenn **CloudConnector** gleich 1 ist  

    - **Werte:**  <*FQDN des Servers für den Dienstverbindungspunkt*\>  

    - **Details:** Hiermit wird der FQDN des Servers angegeben, auf dem die Standortsystemrolle „Dienstverbindungspunkt“ gehostet wird.  

- **Schlüsselname:** UseProxy  

    - **Erforderlich:** Erforderlich, wenn **CloudConnector** gleich 1 ist  

    - **Werte:**

        - `0` = nicht installieren  

        - `1` = installieren  

    - **Details:** Gibt an, ob der Dienstverbindungspunkt einen Proxyserver verwendet.  

- **Schlüsselname:** ProxyName  

    - **Erforderlich:** Erforderlich, wenn **UseProxy** gleich 1 ist  

    - **Werte:**  <*Proxyserver-FQDN*>  

    - **Details:** Hiermit wird der FQDN des Proxyservers angegeben, der von dem Dienstverbindungspunkt verwendet wird.  

- **Schlüsselname:** ProxyPort  

    - **Erforderlich:** Erforderlich, wenn **UseProxy** gleich 1 ist  

    - **Werte:**  <*Portnummer*>  

    - **Details:** Gibt die für den Proxyport zu verwendende Portnummer an.  

#### <a name="sabranchoptions"></a>SABranchOptions

<!-- SCCMDocs#390 -->

- **Schlüsselname:** SAActive

    - **Erforderlich:** Nein

    - **Werte:**

        - `0` = Sie haben Software Assurance nicht.

        - `1` = Software Assurance ist aktiv.

    - **Details:** Geben Sie an, ob Software Assurance bei Ihnen aktiv ist. Weitere Informationen finden Sie unter [Häufig gestellte Fragen für die Configuration Manager-Verzweigungen und -Lizenzierungen](../../../understand/product-and-licensing-faq.md).

- **Schlüsselname:** CurrentBranch

    - **Erforderlich:** Nein

    - **Werte:**

        - `0` = den LTSB installieren

        - `1` = aktuellen Branch installieren

    - **Details:** Geben Sie an, ob für Configuration Manager der aktuelle Branch oder der Long-Term Servicing Branch (LTSB) verwendet werden soll. Weitere Informationen hierzu finden Sie unter [Welcher Branch von Configuration Manager soll verwendet werden?](../../../understand/which-branch-should-i-use.md).

### <a name="unattended-recovery-for-a-cas"></a>Unbeaufsichtigte Wiederherstellung eines Standorts der zentralen Verwaltung

Verwenden Sie die folgenden Detailinformationen, um einen Standort der zentralen Verwaltung über eine Skriptdatei für unbeaufsichtigte Installation wiederherzustellen.  

#### <a name="identification"></a>Identification

- **Schlüsselname:** Aktion  

    - **Erforderlich:** Ja  

    - **Werte:** `RecoverCCAR`  

    - **Details:** Stellt einen Standort der zentralen Verwaltung wieder her.  

- **Schlüsselname:** CDLatest  

    - **Erforderlich:** Ja, aber nur bei Verwendung von Medien aus dem Ordner „CD.Latest“.

    - **Werte:**

        - `1` = Sie verwenden Medien aus „CD.Latest“.

        - Ein Wert ungleich 1 = Sie verwenden keine „CD.Latest“-Medien.

    - **Details:** Wenn Sie einen primären Standort oder einen Standort der zentralen Verwaltung installieren oder wiederherstellen, und wenn Sie Setup aus dem Ordner „CD.Latest“ ausführen, schließen Sie diesen Schlüssel und diesen Wert ein. Dieser Wert informiert Setup darüber, dass Sie Medien aus „CD.Latest“ verwenden.

#### <a name="recoveryoptions"></a>RecoveryOptions

- **Schlüsselname:** ServerRecoveryOptions  

    - **Erforderlich:** Ja  

    - **Werte:**

        - `1` = Wiederherstellung von Standortserver und SQL Server

        - `2` = nur Wiederherstellung von Standortserver

        - `4` = nur Wiederherstellung von SQL Server  

    - **Details:** Gibt an, ob der Standortserver, die SQL Server-Instanz oder beide beim Setup wiederhergestellt werden. Die folgenden Optionen sind ebenfalls entsprechend dem angegebenen Wert erforderlich:  

        - **1** oder **2**: Um den Standort aus einer Standortsicherung wiederherzustellen, geben Sie einen Wert für **SiteServerBackupLocation** an. Wenn Sie keinen Wert angeben, installiert Setup den Standort erneut, ohne ihn aus einem Sicherungssatz wiederherzustellen.  

        - **4**: Der Schlüssel **BackupLocation** ist erforderlich, wenn Sie für den Schlüssel **DatabaseRecoveryOptions** den Wert **10** konfigurieren, um die Standortdatenbank aus einer Sicherung wiederherstellen zu lassen.  

- **Schlüsselname:** DatabaseRecoveryOptions  

    - **Erforderlich:** Dieser Schlüssel ist erforderlich, wenn für die Einstellung **ServerRecoveryOptions** der Wert **1** oder **4**konfiguriert wurde.  

    - **Werte:**

        - `10` = Wiederherstellen der Standortdatenbank aus einer Sicherung.  

        - `20` = Verwenden einer Standortdatenbank, die Sie mit einer anderen Methode manuell wiederhergestellt haben.  

        - `40` = Erstellen einer neuen Datenbank für den Standort. Verwenden Sie diese Option, wenn keine Standortdatenbank verfügbar ist. Die globalen und die Standortdaten des Standorts werden über Replikation aus anderen Standorten wiederhergestellt.  

        - `80` = Überspringen der Datenbankwiederherstellung.  

    - **Details:** Gibt an, wie die Standortdatenbank in SQL Server beim Setup wiederhergestellt wird.  

- **Schlüsselname:** ReferenceSite  

    - **Erforderlich:** Dieser Schlüssel ist erforderlich, wenn für die Einstellung **DatabaseRecoveryOptions** der Wert **40**vorliegt.  

    - **Werte:**  <*FQDN des Referenzstandorts*>  

    - **Details:** Wenn die Datenbanksicherung so alt ist, dass sie vor der Beibehaltungsdauer der Änderungsnachverfolgung erstellt wurde, oder wenn Sie den Standort ohne Sicherung wiederherstellen, geben Sie den primären Referenzstandort an, der vom Standort der zentralen Verwaltung verwendet wird, um globale Daten wiederherzustellen.  

        Wenn Sie keinen Referenzstandort angeben und die Sicherung so alt ist, dass sie vor der Beibehaltungsdauer der Änderungsnachverfolgung erstellt wurde, werden alle primären Standorte mit den wiederhergestellten Daten vom Standort der zentralen Verwaltung neu initialisiert.  

        Wenn Sie keinen Referenzstandort angeben und die Sicherung innerhalb der Beibehaltungsdauer der Änderungsnachverfolgung liegt, dann werden nur Änderungen, die nach der Sicherung vorgenommen wurden, von den primären Standorten repliziert. Liegen von verschiedenen primären Standorten Änderungen vor, die miteinander in Konflikt stehen, wird vom Standort der zentralen Verwaltung die zuerst empfangene Änderung verwendet.  

- **Schlüsselname:** SiteServerBackupLocation  

    - **Erforderlich:** Nein  

    - **Werte:**  <*Pfad zum Sicherungssatz des Standortservers*>  

    - **Details:** Über diesen Schlüssel wird der Pfad zum Sicherungssatz des Standortservers angegeben. Dieser Schlüssel ist optional, wenn für die Einstellung **ServerRecoveryOptions** der Wert **1** oder **2**festgelegt wurde. Geben Sie einen Wert für den Schlüssel **SiteServerBackupLocation** an, um den Standort aus einer Standortsicherung wiederherstellen zu lassen. Wenn Sie keinen Wert angeben, installiert Setup den Standort erneut, ohne ihn aus einem Sicherungssatz wiederherzustellen.  

- **Schlüsselname:** BackupLocation  

    - **Erforderlich:** Dieser Schlüssel ist erforderlich, wenn Sie für den Schlüssel **ServerRecoveryOptions** den Wert **1** oder **4** und für den Schlüssel **DatabaseRecoveryOptions** den Wert **10** konfigurieren.  

    - **Werte:**  <*Pfad zum Sicherungssatz der Standortdatenbank*>  

    - **Details:** Über diesen Schlüssel wird der Pfad zum Sicherungssatz der Standortdatenbank angegeben.  

#### <a name="options"></a>Optionen

- **Schlüsselname:** ProductID  

    - **Erforderlich:** Ja  

    - **Werte:**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>` = ein gültiger Product Key mit Bindestrichen

        - `Eval` = Installieren der Evaluierungsversion von Configuration Manager

    - **Details:** Gibt den Product Key für die Configuration Manager-Installation, einschließlich der Gedankenstriche, an.

- **Schlüsselname:** SiteCode  

    - **Erforderlich:** Ja  

    - **Werte:**  <*Standortcode*>  

    - **Details:** Gibt drei alphanumerische Zeichen an, durch die der Standort in der Hierarchie eindeutig angegeben wird. Geben Sie den Standortcode an, der vor dem Auftreten des Fehlers vom Standort verwendet wurde.

- **Schlüsselname:** SiteName  

    - **Erforderlich:** Nein  

    - **Werte:**  <*Standortname*>  

    - **Details:** Gibt den Namen für diesen Standort an.  

- **Schlüsselname:** SMSInstallDir  

    - **Erforderlich:** Ja  

    - **Werte:**  <*Configuration Manager-Installationspfad*>  

    - **Details:** Gibt den Installationsordner für die Configuration Manager-Programmdateien an.  

- **Schlüsselname:** SDKServer  

    - **Erforderlich:** Ja  

    - **Werte:**  <*SMS-Anbieter-FQDN*>  

    - **Details:** Gibt den FQDN des Servers an, auf dem der SMS-Anbieter gehostet wird. Geben Sie den Server an, auf dem der SMS-Anbieter vor Auftreten des Fehlers gehostet wurde.  

        Nach der Erstinstallation können Sie zusätzliche SMS-Anbieter für den Standort konfigurieren. Weiter Informationen zum SMS-Anbieter finden Sie unter [Planen des SMS-Anbieters](../../../plan-design/hierarchy/plan-for-the-sms-provider.md).  

- **Schlüsselname:** PrerequisiteComp  

    - **Erforderlich:** Ja  

    - **Werte:**

        - `0` = herunterladen  

        - `1` = bereits heruntergeladen  

    - **Details:** Gibt an, ob die für das Setup erforderlichen Dateien bereits heruntergeladen wurden. Wenn Sie beispielsweise den Wert **0** angeben, werden die Dateien beim Setup heruntergeladen.  

- **Schlüsselname:** PrerequisitePath  

    - **Erforderlich:** Ja  

    - **Werte:**  <*Pfad zu den für das Setup erforderlichen Dateien*>  

    - **Details:** Gibt den Pfad zu den für das Setup erforderlichen Dateien an. Je nach **PrerequisiteComp**-Wert wird dieser Pfad beim Setup zum Speichern heruntergeladener Dateien oder zum Suchen der zuvor heruntergeladenen Dateien verwendet.  

- **Schlüsselname:** AdminConsole  

    - **Erforderlich:** Dieser Schlüssel ist erforderlich, außer wenn für die Einstellung **ServerRecoveryOptions** der Wert **4**vorliegt.  

    - **Werte:**

        - `0` = nicht installieren  

        - `1` = installieren  

    - **Details:** Damit wird angegeben, ob die Configuration Manager-Konsole installiert werden soll.  

- **Schlüsselname:** JoinCEIP  

    > [!Note]  
    > Ab Configuration Manager Version 1802 ist das CEIP-Feature nicht mehr im Produkt enthalten.

    - **Erforderlich:** Ja  

    - **Werte:**

        - `0` = nicht teilnehmen  

        - `1` = teilnehmen  

    - **Details:** Gibt an, ob am Programm zur Verbesserung der Benutzerfreundlichkeit (CEIP) teilgenommen werden soll.  

#### <a name="sqlconfigoptions"></a>SQLConfigOptions

- **Schlüsselname:** SQLServerName  

    - **Erforderlich:** Ja  

    - **Werte:**  <*SQL Server-Name*>  

    - **Details:** Gibt den Namen des Servers oder der gruppierten Instanz an, der bzw. die SQL Server ausführt und auf dem bzw. der die Standortdatenbank gehostet wird. Geben Sie denselben Server an, auf dem die Standortdatenbank vor Auftreten des Fehlers gehostet wurde.  

- **Schlüsselname:** DatabaseName  

    - **Erforderlich:** Ja  

    - **Werte:**  <*Standortdatenbankname*> oder <*Instanzname*>\\<*Standortdatenbankname*>  

    - **Details:** Gibt den Namen der SQL Server-Datenbank an, die erstellt oder verwendet werden soll, wenn die Datenbank für den Standort der zentralen Verwaltung installiert wird. Geben Sie denselben Datenbanknamen an, der vor Auftreten des Fehlers verwendet wurde.  

        > [!IMPORTANT]  
        > Wenn Sie nicht die Standardinstanz verwenden, geben Sie den Instanznamen und den Namen der Standortdatenbank an.  

- **Schlüsselname:** SQLSSBPort  

    - **Erforderlich:** Ja  

    - **Werte:**  <*SSB-Portnummer*>  

    - **Details:** Gibt den SSB-Port an, der von SQL Server verwendet wird. Standardmäßig wird für SSB der TCP-Port 4022 verwendet. Geben Sie denselben SSB-Port an, der vor Auftreten des Fehlers verwendet wurde.  

- **Schlüsselname:** SQLDataFilePath  

    - **Erforderlich:** Nein  

    - **Werte:**  <*Pfad zur .mdb-Datenbankdatei*>  

    - **Details:** Hiermit wird ein alternativer Speicherort zum Erstellen der MDB-Datei für die Datenbank angegeben.  

- **Schlüsselname:** SQLLogFilePath  

    - **Erforderlich:** Nein  

    - **Werte:**  <*Pfad zur .ldf-Datenbankdatei*>  

    - **Details:** Hiermit wird ein alternativer Speicherort zum Erstellen der LDF-Datei für die Datenbank angegeben.  

#### <a name="cloudconnectoroptions"></a>CloudConnectorOptions

- **Schlüsselname:** CloudConnector  

    - **Erforderlich:** Ja  

    - **Werte:**

        - `0` = nicht installieren  

        - `1` = installieren  

    - **Details:** Gibt an, ob ein Dienstverbindungspunkt an diesem Standort installiert werden soll. Da Sie den Dienstverbindungspunkt nur im obersten Standort einer Hierarchie installieren können, muss dieser Wert für einen untergeordneten primären Standort gleich **0** sein.  

- **Schlüsselname:** CloudConnectorServer  

    - **Erforderlich:** Erforderlich, wenn **CloudConnector** gleich 1 ist  

    - **Werte:**  <*FQDN des Servers für den Dienstverbindungspunkt*>  

    - **Details:** Hiermit wird der FQDN des Servers angegeben, auf dem die Standortsystemrolle „Dienstverbindungspunkt“ gehostet wird.  

- **Schlüsselname:** UseProxy  

    - **Erforderlich:** Erforderlich, wenn **CloudConnector** gleich 1 ist  

    - **Werte:**

        - `0` = nicht installieren  

        - `1` = installieren  

    - **Details:** Gibt an, ob der Dienstverbindungspunkt einen Proxyserver verwendet.  

- **Schlüsselname:** ProxyName  

    - **Erforderlich:** Erforderlich, wenn **CloudConnector** gleich 1 ist  

    - **Werte:**  <*Proxyserver-FQDN*>  

    - **Details:** Hiermit wird der FQDN des Proxyservers angegeben, der von dem Dienstverbindungspunkt verwendet wird.  

- **Schlüsselname:** ProxyPort  

    - **Erforderlich:** Erforderlich, wenn **CloudConnector** gleich 1 ist  

    - **Werte:**  <*Portnummer*>  

    - **Details:** Gibt die für den Proxyport zu verwendende Portnummer an.  

### <a name="unattended-recovery-for-a-primary-site"></a>Unbeaufsichtigte Wiederherstellung eines primären Standorts

Im folgenden Abschnitt finden Sie Detailinformationen Wiederherstellung eines primären Standorts mithilfe einer Skriptdatei zur unbeaufsichtigten Installation.  

#### <a name="identification"></a>Identification

- **Schlüsselname:** Aktion  

    - **Erforderlich:** Ja  

    - **Werte:** `RecoverPrimarySite`  

    - **Details:** Mit diesem Schlüssel wird ein primärer Standort wiederhergestellt.  

- **Schlüsselname:** CDLatest  

    - **Erforderlich:** Ja, aber nur bei Verwendung von Medien aus dem Ordner „CD.Latest“.

    - **Werte:**

        - `1` = Sie verwenden Medien aus „CD.Latest“.

        - Ein Wert ungleich 1 = Sie verwenden keine „CD.Latest“-Medien.

    - **Details:** Wenn Sie einen primären Standort oder einen Standort der zentralen Verwaltung installieren oder wiederherstellen, und wenn Sie Setup aus dem Ordner „CD.Latest“ ausführen, schließen Sie diesen Schlüssel und diesen Wert ein. Dieser Wert informiert Setup darüber, dass Sie Medien aus „CD.Latest“ verwenden.

#### <a name="recoveryoptions"></a>RecoveryOptions

- **Schlüsselname:** ServerRecoveryOptions  

    - **Erforderlich:** Ja  

    - **Werte:**

        - `1` = Wiederherstellung von Standortserver und SQL Server

        - `2` = nur Wiederherstellung von Standortserver

        - `4` = nur Wiederherstellung von SQL Server  

    - **Details:** Gibt an, ob der Standortserver, die SQL Server-Instanz oder beide beim Setup wiederhergestellt werden. Die folgenden Optionen sind ebenfalls entsprechend dem angegebenen Wert erforderlich:  

        - **1** oder **2**: Um den Standort aus einer Standortsicherung wiederherzustellen, geben Sie einen Wert für **SiteServerBackupLocation** an. Wenn Sie keinen Wert angeben, installiert Setup den Standort erneut, ohne ihn aus einem Sicherungssatz wiederherzustellen.  

        - **4**: Der Schlüssel **BackupLocation** ist erforderlich, wenn Sie für den Schlüssel **DatabaseRecoveryOptions** den Wert **10** konfigurieren, um die Standortdatenbank aus einer Sicherung wiederherstellen zu lassen.  

- **Schlüsselname:** DatabaseRecoveryOptions  

    - **Erforderlich:** Dieser Schlüssel ist erforderlich, wenn für die Einstellung **ServerRecoveryOptions** der Wert **1** oder **4**konfiguriert wurde.  

    - **Werte:**

        - `10` = Wiederherstellen der Standortdatenbank aus einer Sicherung.  

        - `20` = Verwenden einer Standortdatenbank, die Sie mit einer anderen Methode manuell wiederhergestellt haben.  

        - `40` = Erstellen einer neuen Datenbank für den Standort. Verwenden Sie diese Option, wenn keine Standortdatenbank verfügbar ist. Die globalen und die Standortdaten des Standorts werden über Replikation aus anderen Standorten wiederhergestellt.  

        - `80` = Überspringen der Datenbankwiederherstellung.  

    - **Details:** Gibt an, wie die Standortdatenbank in SQL Server beim Setup wiederhergestellt wird.  

- **Schlüsselname:** SiteServerBackupLocation  

    - **Erforderlich:** Nein  

    - **Werte:**  <*Pfad zum Sicherungssatz des Standortservers*>  

    - **Details:** Über diesen Schlüssel wird der Pfad zum Sicherungssatz des Standortservers angegeben. Dieser Schlüssel ist optional, wenn für die Einstellung **ServerRecoveryOptions** der Wert **1** oder **2**festgelegt wurde. Geben Sie einen Wert für den Schlüssel **SiteServerBackupLocation** an, um den Standort aus einer Standortsicherung wiederherstellen zu lassen. Wenn Sie keinen Wert angeben, installiert Setup den Standort erneut, ohne ihn aus einem Sicherungssatz wiederherzustellen.  

- **Schlüsselname:** BackupLocation  

    - **Erforderlich:** Dieser Schlüssel ist erforderlich, wenn Sie für den Schlüssel **ServerRecoveryOptions** den Wert **1** oder **4** und für den Schlüssel **DatabaseRecoveryOptions** den Wert **10** konfigurieren.  

    - **Werte:**  <*Pfad zum Sicherungssatz der Standortdatenbank*>  

    - **Details:** Über diesen Schlüssel wird der Pfad zum Sicherungssatz der Standortdatenbank angegeben.  

#### <a name="options"></a>Optionen

- **Schlüsselname:** ProductID  

    - **Erforderlich:** Ja  

    - **Werte:**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>` = ein gültiger Product Key mit Bindestrichen

        - `Eval` = Installieren der Evaluierungsversion von Configuration Manager

    - **Details:** Gibt den Product Key für die Configuration Manager-Installation, einschließlich der Gedankenstriche, an.

- **Schlüsselname:** SiteCode  

    - **Erforderlich:** Ja  

    - **Werte:**  <*Standortcode*>  

    - **Details:** Gibt drei alphanumerische Zeichen an, durch die der Standort in der Hierarchie eindeutig angegeben wird. Geben Sie den Standortcode an, der vor dem Auftreten des Fehlers vom Standort verwendet wurde.

- **Schlüsselname:** SiteName  

    - **Erforderlich:** Nein  

    - **Werte:**  <*Standortname*>  

    - **Details:** Gibt den Namen für diesen Standort an.  

- **Schlüsselname:** SMSInstallDir  

    - **Erforderlich:** Ja  

    - **Werte:**  <*Configuration Manager-Installationspfad*>  

    - **Details:** Gibt den Installationsordner für die Configuration Manager-Programmdateien an.  

- **Schlüsselname:** SDKServer  

    - **Erforderlich:** Ja  

    - **Werte:**  <*SMS-Anbieter-FQDN*>  

    - **Details:** Gibt den FQDN des Servers an, auf dem der SMS-Anbieter gehostet wird. Geben Sie den Server an, auf dem der SMS-Anbieter vor Auftreten des Fehlers gehostet wurde. Nach der Erstinstallation können Sie zusätzliche SMS-Anbieter für den Standort konfigurieren. Weiter Informationen zum SMS-Anbieter finden Sie unter [Planen des SMS-Anbieters](../../../plan-design/hierarchy/plan-for-the-sms-provider.md).  

- **Schlüsselname:** PrerequisiteComp  

    - **Erforderlich:** Ja  

    - **Werte:**

        - `0` = herunterladen  

        - `1` = bereits heruntergeladen  

    - **Details:** Gibt an, ob die für das Setup erforderlichen Dateien bereits heruntergeladen wurden. Wenn Sie beispielsweise den Wert **0** angeben, werden die Dateien beim Setup heruntergeladen.  

- **Schlüsselname:** PrerequisitePath  

    - **Erforderlich:** Ja  

    - **Werte:**  <*Pfad zu den für das Setup erforderlichen Dateien*>  

    - **Details:** Gibt den Pfad zu den für das Setup erforderlichen Dateien an. Je nach **PrerequisiteComp**-Wert wird dieser Pfad beim Setup zum Speichern heruntergeladener Dateien oder zum Suchen der zuvor heruntergeladenen Dateien verwendet.  

- **Schlüsselname:** AdminConsole  

    - **Erforderlich:** Dieser Schlüssel ist erforderlich, außer wenn für die Einstellung **ServerRecoveryOptions** der Wert **4**vorliegt.  

    - **Werte:**

        - `0` = nicht installieren  

        - `1` = installieren  

    - **Details:** Damit wird angegeben, ob die Configuration Manager-Konsole installiert werden soll.  

- **Schlüsselname:** JoinCEIP  

    > [!Note]  
    > Ab Configuration Manager Version 1802 ist das CEIP-Feature nicht mehr im Produkt enthalten.

    - **Erforderlich:** Ja  

    - **Werte:**

        - `0` = nicht teilnehmen  

        - `1` = teilnehmen  

    - **Details:** Gibt an, ob am Programm zur Verbesserung der Benutzerfreundlichkeit (CEIP) teilgenommen werden soll.  

#### <a name="sqlconfigoptions"></a>SQLConfigOptions

- **Schlüsselname:** SQLServerName  

    - **Erforderlich:** Ja  

    - **Werte:**  <*SQL Server-Name*>  

    - **Details:** Gibt den Namen des Servers oder der gruppierten Instanz an, auf dem bzw. in der SQL Server ausgeführt wird, um die Standortdatenbank zu hosten. Geben Sie denselben Server an, auf dem die Standortdatenbank vor Auftreten des Fehlers gehostet wurde.  

- **Schlüsselname:** DatabaseName  

    - **Erforderlich:** Ja  

    - **Werte:**  <*Standortdatenbankname*> oder <*Instanzname*>\\<*Standortdatenbankname*>

    - **Details:** Gibt den Namen der SQL Server-Datenbank an, die erstellt oder verwendet werden soll, wenn die Datenbank für den Standort der zentralen Verwaltung installiert wird. Geben Sie denselben Datenbanknamen an, der vor Auftreten des Fehlers verwendet wurde.  

        > [!IMPORTANT]  
        > Wenn Sie nicht die Standardinstanz verwenden, geben Sie den Instanznamen und den Namen der Standortdatenbank an.  

- **Schlüsselname:** SQLSSBPort  

    - **Erforderlich:** Ja  

    - **Werte:**  <*SSB-Portnummer*>  

    - **Details:** Gibt den SSB-Port an, der von SQL Server verwendet wird. Standardmäßig wird für SSB der TCP-Port 4022 verwendet. Geben Sie denselben SSB-Port an, der vor Auftreten des Fehlers verwendet wurde.  

- **Schlüsselname:** SQLDataFilePath  

    - **Erforderlich:** Nein  

    - **Werte:**  <*Pfad zur .mdb-Datenbankdatei*>  

    - **Details:** Hiermit wird ein alternativer Speicherort zum Erstellen der MDB-Datei für die Datenbank angegeben.  

- **Schlüsselname:** SQLLogFilePath  

    - **Erforderlich:** Nein  

    - **Werte:**  <*Pfad zur .ldf-Datenbankdatei*>  

    - **Details:** Hiermit wird ein alternativer Speicherort zum Erstellen der LDF-Datei für die Datenbank angegeben.  

#### <a name="hierarchyexpansionoptions"></a>HierarchyExpansionOptions

- **Schlüsselname:** CCARSiteServer  

    - **Erforderlich:** Siehe Details.  

    - **Werte:**  <*Standortcode für CAS*>  

    - **Details:** Gibt den Standort der zentralen Verwaltung (Central Administration Site, CAS) an, dem ein primärer Standort zugeordnet wird, wenn er in die Configuration Manager-Hierarchie eingebunden wird. Diese Einstellung ist erforderlich, wenn der primäre Standort vor dem Fehler mit einem CAS verbunden war. Geben Sie den Standortcode an, der vor Auftreten des Fehlers für den CAS verwendet wurde.  

- **Schlüsselname:** CASRetryInterval  

    - **Erforderlich:** Nein  

    - **Werte:**  <*Intervall in Minuten*>  

    - **Details:** Gibt das Wiederholungsintervall (in Minuten) an, nach dem nach einem Verbindungsfehler versucht werden soll, erneut eine Verbindung mit dem Standort der zentralen Verwaltung herzustellen. Tritt beispielsweise beim Herstellen einer Verbindung mit dem Standort der zentralen Verwaltung (Central Administration Site, CAS) ein Fehler auf, wird am primären Standort entsprechend der Anzahl von Minuten, die Sie für **CASRetryInterval** angegeben haben, gewartet, bevor versucht wird, die Verbindung erneut herzustellen.  

- **Schlüsselname:** WaitForCASTimeout  

    - **Erforderlich:** Nein  

    - **Werte:**  <*Timeout in Minuten*>  

    - **Details:** Gibt den maximalen Timeoutwert (in Minuten) an, bis zu dem ein primärer Standort versucht, eine Verbindung mit dem Standort der zentralen Verwaltung (Central Administration Site, CAS) herzustellen. Kann ein primärer Standort beispielsweise keine Verbindung mit einem CAS herstellen, versucht der primäre Standort wiederholt eine Verbindungsherstellung mit dem CAS entsprechend dem **CASRetryInterval**-Wert, bis der für **WaitForCASTimeout** angegebene Zeitraum abgelaufen ist. Sie können einen Wert von `0` bis `100` angeben.  

#### <a name="cloudconnectoroptions"></a>CloudConnectorOptions

- **Schlüsselname:** CloudConnector  

    - **Erforderlich:** Ja  

    - **Werte:**

        - `0` = nicht installieren  

        - `1` = installieren  

    - **Details:** Gibt an, ob ein Dienstverbindungspunkt an diesem Standort installiert werden soll. Da Sie den Dienstverbindungspunkt nur im obersten Standort einer Hierarchie installieren können, muss dieser Wert für einen untergeordneten primären Standort gleich `0` sein.  

- **Schlüsselname:** CloudConnectorServer  

    - **Erforderlich:** Erforderlich, wenn **CloudConnector** gleich 1 ist  

    - **Werte:**  <*FQDN des Servers für den Dienstverbindungspunkt*>  

    - **Details:** Hiermit wird der FQDN des Servers angegeben, auf dem die Standortsystemrolle „Dienstverbindungspunkt“ gehostet wird.  

- **Schlüsselname:** UseProxy  

    - **Erforderlich:** Erforderlich, wenn **CloudConnector** gleich 1 ist  

    - **Werte:**

        - `0` = nicht installieren  

        - `1` = installieren  

    - **Details:** Gibt an, ob der Dienstverbindungspunkt einen Proxyserver verwendet.  

- **Schlüsselname:** ProxyName  

    - **Erforderlich:** Erforderlich, wenn **CloudConnector** gleich 1 ist  

    - **Werte:**  <*Proxyserver-FQDN*>  

    - **Details:** Hiermit wird der FQDN des Proxyservers angegeben, der von dem Dienstverbindungspunkt verwendet wird.  

- **Schlüsselname:** ProxyPort  

    - **Erforderlich:** Erforderlich, wenn **CloudConnector** gleich 1 ist  

    - **Werte:**  <*Portnummer*>  

    - **Details:** Gibt die für den Proxyport zu verwendende Portnummer an.  
