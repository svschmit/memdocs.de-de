---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 07/13/2020
ms.openlocfilehash: 8e95fce122a3e153f2aa391dcd5e40439f8e5820
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88703491"
---
<!--This file is shared by the CMPivot overview articles for both Microsoft Endpoint Manager tenant attach and Configuration Manager-->

## <a name="queries"></a>Abfragen

Abfragen können verwendet werden, um nach Begriffen zu suchen, Trends zu ermitteln, Muster zu analysieren und basierend auf Ihren Daten viele weitere Erkenntnisse zu gewinnen. CMPivot verwendet eine Teilmenge des [Azure Log Analytics](/azure/kusto/query)-Datenflussmodells für die tabellarische Ausdrucksanweisung. Die typische Struktur einer tabellarischen Ausdrucksanweisung ist eine Zusammenstellung aus Cliententitäten und tabellarischen Datenoperatoren (z. B. Filter und Projektionen). Die Zusammenstellung wird durch ein Pipe-Zeichen (|) dargestellt, wodurch die Anweisung eine sehr regelmäßige Form erhält, die den Fluss der tabellarischen Daten von links nach rechts visuell darstellt. Jeder Operator akzeptiert einen tabellarischen Datensatz „aus der Pipe“ und weitere Eingaben (einschließlich anderer tabellarischer Datensätze) aus dem Textkörper des Operators und sendet dann wie folgt ein tabellarisches Dataset an den nächsten Operator: `entity | operator1 | operator2 | ...`

Im folgenden Beispiel ist die Entität `CCMRecentlyUsedApplications` (ein Verweis auf die zuletzt verwendeten Anwendungen), und der Operator lautet „where“ (zum Filtern von Datensätzen anhand der Eingabe und einiger datensatzbezogener Prädikate):

```
CCMRecentlyUsedApplications | where CompanyName like '%Microsoft%' | project CompanyName, ExplorerFileName, LastUsedTime, LaunchCount, FolderPath
```

## <a name="entities"></a>Entitäten

Entitäten sind Objekte, die vom Client abgefragt werden können. Derzeit werden die folgenden Entitäten unterstützt:


|Entität|Beschreibung|
|---|---|
|AadStatus|Status von Azure Active Directory|
|Administratoren|Mitglieder der Gruppe lokaler Administratoren|
|AppCrash|Berichte zu aktuellen Anwendungsabstürzen|
|AppvClientApplication|AppV-Clientanwendung|
|AppVClientPackage|AppV-Clientpaket|
|AutoStartSoftware|Software, die gleichzeitig mit oder unmittelbar nach dem Betriebssystem automatisch gestartet wird|
|BaseBoard|BaseBoard|
|Akku|Akku|
|Bios|BIOS-Systeminformationen|
|BitLocker|BitLocker|
|BitLockerEncryptionDetails|BitLocker-Verschlüsselungsdetails|
|BitLockerPolicy|BitLocker-Richtlinie|
|BootConfiguration|Startkonfiguration|
|BrowserHelperObject|Browserhilfsobjekt|
|BrowserUsage|Browsernutzung|
|CcmLog()|Zeilen innerhalb eines 24-Stunden-Zeitraums (Standardwert) aus einer CCM-Protokolldatei|
|CCMRAX|CCM_RAX|
|CCMRecentlyUsedApplications|Zuletzt verwendete Anwendungen|
|CCMWebAppInstallInfo|Webanwendungen|
|CDROM|CD-ROM-Laufwerk|
|ClientEvents|Clientereignisse|
|ComputerSystem|Computersystem|
|ComputerSystemEx|Computersystem (Erweitert)|
|ComputerSystemProduct|Computersystemprodukt|
|ConnectedDevice|Verbundenes Gerät|
|Verbindung|Eine ein- oder ausgehende aktive TCP-Geräteverbindung|
|desktop-|desktop-|
|DesktopMonitor|Desktopmonitor|
|Gerät|Grundlegende Informationen zum Gerät|
|Datenträger|Informationen zum lokalen Speichergerät auf einem Computersystem unter Windows|
|Gerätespeicheradresse|Gerätespeicheradresse|
|DMAChannel|DMA-Kanal|
|DriverVxD|VxD-Treiber|
|EmbeddedDeviceInformation|Eingebettete Geräteinformationen|
|Umgebung|Umgebung|
|EPStatus|Status der Antischadsoftware auf dem Computer|
|EventLog()|Ereignisse innerhalb eines 24-Stunden-Zeitraums (Standardwert) aus einem Ereignisprotokoll|
|File()|Informationen zu einer spezifischen Datei|
|FileShare|Informationen zur aktiven Dateifreigabe|
|Firmware|Firmware|
|IDEController|IDE-Controller|
|InstalledExecutable|Installierte ausführbare Dateien|
|InstalledSoftware|Eine Anwendung, die auf dem Gerät installiert ist|
|IPConfig|Ruft die Netzwerkkonfiguration ab, einschließlich verwendbarer Schnittstellen, IP-Adressen und DNS-Server|
|IRQTable|IRQ-Tabelle|
|Tastatur|Tastatur|
|LoadOrderGroup|Gruppe für Ladereihenfolge|
|LogicalDisk|Logischer Datenträger|
|MDMDevDetail|Geräteinformationen|
|Arbeitsspeicher|Arbeitsspeicher|
|Modem|Modem|
|Hauptplatine|Hauptplatine|
|NetworkAdapter|Netzwerkkarte|
|NetworkAdapterConfiguration|Netzwerkadapterkonfiguration|
|NetworkClient|Netzwerkclient|
|NetworkLoginProfile|Profil für die Netzwerkanmeldung|
|NTEventlogFile|NT-Ereignisprotokolldatei|
|Office365ProPlusConfigurations|Office 365 ProPlus-Konfigurationen|
|OfficeAddin|Office-Add-Ins|
|OfficeClientMetric|Office-Clientmetriken|
|OfficeDeviceSummary|Office-Gerätezusammenfassung|
|OfficeClientMetric|Metriken von Office-Dokumenten|
|OfficeDocumentSolution|Office-Dokumentlösung|
|OfficeMacroError|Office-Makrofehler|
|OfficeProductInfo|Office-Produktinformationen|
|OfficeVbaRuleViolation|Office VBA-Regelverstöße|
|OfficeVbaSummary|Office VBA-Scans – Zusammenfassung|
|OperatingSystem|Betriebssystem|
|OperatingSystemEx|Betriebssystem (Erweitert)|
|OperatingSystemRecoveryConfiguration|Wiederherstellungskonfiguration des Betriebssystems|
|OptionalFeature|Optionale Features|
|Betriebssystem|Grundlegende Informationen zum Betriebssystem|
|PageFileSetting|Auslagerungsdateieinstellungen|
|ParallelPort|Paralleler Port|
|Partition|Laufwerkpartitionen|
|PCMCIAController|PCMCIA-Controller|
|Physischer Datenträger|Physischer Datenträger|
|PhysicalMemory|Physischer Speicher|
|PNPDEVICEDRIVER|PNP-Gerätetreiber|
|PointingDevice|Zeigegerät|
|PortableBattery|Tragbare Batterie|
|Ports|Ports|
|PowerCapabilities|Energiefunktionen|
|PowerClientOptOutSettings|Ausschlusseinstellungen für die Energieverwaltung|
|PowerConfigurations|Energiekonfiguration|
|PowerManagementDaily|Energieverwaltung – Tagesdaten|
|PowerManagementInsomniaReasons|Ursachen von Energiestörungen|
|PowerManagementMonthly|Energieverwaltung – Monatsdaten|
|PowerSettings|Energieeinstellungen|
|PrinterConfiguration|Druckerkonfiguration|
|PrinterDevice|Druckergerät|
|PrintJobs|Druckaufträge|
|Prozess|Ein Prozess auf einem Betriebssystem|
|ProcessModule()|Von angegebenen Prozessen geladene Module|
|Prozessor|Prozessor|
|ProtectedVolumeInformation|Informationen zu geschützten Volumes|
|Protokoll|Protokoll|
|QuickFixEngineering|Quick Fix Engineering|
|SCSIController|SCSI-Controller|
|SerialPortConfiguration|Serielle Portkonfiguration|
|SerialPorts|Serielle Ports|
|ServerFeature|Serverfunktion|
|Dienst|Ein Dienst auf einem Windows-Computersystem|
|Dienste|Dienste|
|Freigaben|Freigaben|
|SMBConfig|SMB-Konfiguration eines Geräts|
|SMSAdvancedClientPorts|Ports des Configuration Manager-Clients|
|SMSAdvancedClientSSLConfigurations|SSL-Konfigurationen des Configuration Manager-Clients|
|SMSAdvancedClientState|Zustand des Configuration Manager-Clients|
|SMSDefaultBrowser|Standardbrowser|
|SMSSoftwareTag|Softwaretag|
|SMSWindows8Application|Windows-App|
|SMSWindows8ApplicationUserInfo|Benutzerinformationen zu Windows-App|
|SoftwareShortcut|Softwareverknüpfung|
|SoftwareUpdate|Ein anwendbares Softwareupdate, das nicht auf dem Gerät installiert ist|
|SoundDevices|Audiogeräte|
|SWLicensingProduct|Softwarelizenzierungsprodukt|
|SWLicensingService|Softwarelizenzierungsdienst|
|SystemAccount|Systemkonto|
|SystemBootData|Systemstartdaten|
|SystemBootSummary|Systemstartzusammenfassung|
|SystemConsoleUsage|Systemkonsolennutzung|
|SystemConsoleUsage|Systemkonsolenbenutzer|
|SystemDevices|Systemgeräte|
|SystemDrivers|Systemtreiber|
|SystemEnclosure|Systemgehäuse|
|TapeDrive|Bandlaufwerk|
|TimeZone|Zeitzone|
|TPM|TPM|
|TPMStatus|TPM-Status|
|TSIssuedLicense|Für Terminaldienste ausgestellte Lizenzen|
|TSLicenseKeyPack|Lizenzschlüsselpaket für Terminaldienste|
|UninterruptiblePowerSupply|Unterbrechungsfreie Stromversorgung|
|USBController|USB-Controller|
|USBDevice|USB-Gerät|
|Benutzer|Ein Benutzerkonto mit einer aktiven Verbindung mit dem Gerät|
|USMFolderRedirectionHealth|Integrität der Ordnerumleitung|
|USMUserProfile|Integrität des Benutzerprofils|
|VideoController|Videocontroller|
|VirtualMachine|Virtueller Computer|
|VirtualMachine64|Virtuelle Computer (64-Bit)|
|Volume|Volume|
|WindowsUpdate|Windows Update|
|WindowsUpdateAgentVersion|Version des Windows Update-Agents|
|WinEvent()|Ereignisse innerhalb eines 24-Stunden-Zeitraums (Standardwert) aus einem Windows-Ereignisprotokoll|
|WriteFilterState|Schreibfilterzustand|

## <a name="table-operators"></a>Tabellenoperatoren

Tabellenoperatoren können verwendet werden, um Datenströme zu filtern, zusammenzufassen und zu transformieren. Die folgenden Operatoren werden derzeit unterstützt:

|Tabellenoperatoren|Beschreibung|
|---|---|
|count|Gibt eine Tabelle mit einem einzelnen Datensatz zurück, der die Anzahl von Datensätzen enthält|
|distinct|Erzeugt eine Tabelle mit der eindeutig identifizierbaren Kombination aus angegebenen Spalten der Eingabetabelle|
|join|Zusammenführen der Zeilen von zwei Tabellen nach der übereinstimmenden Zeile für das gleiche Gerät, um eine neue Tabelle zu bilden|
|order by|Hiermit werden die Zeilen der Eingabetabelle nach mindestens einer Spalte sortiert|
|project|Hiermit werden Spalten ausgewählt, die eingeschlossen, umbenannt oder gelöscht werden sollen, und neue berechnete Spalten werden eingefügt|
|summarize|Erzeugt eine Tabelle, in der der Inhalt der Eingabetabelle aggregiert wird|
|take|Hiermit werden Zeilen bis zur maximal angegebenen Anzahl zurückgegeben|
|top|Gibt die ersten n Datensätze zurück, sortiert nach der angegebenen Spalte|
|Dabei gilt:|Filtert eine Tabelle auf die Teilmenge der Zeilen, die einem Prädikat entsprechen|

## <a name="scalar-operators"></a>Skalaroperatoren

Die folgende Tabelle fasst Operatoren zusammen:

|Operatoren|Beschreibung|Beispiel
|---|---|---|
|==|Gleich|`1 == 1, 'aBc' == 'AbC'`|
|!=|Ungleich|`1 != 2, 'abc' != 'abcd'`|
|< |Kleiner|`1 < 2, 'abc' < 'DEF'`|
|> |Größer|`2 > 1, 'xyz' > 'XYZ'`|
|<=|Kleiner oder gleich|`1 <= 2, 'abc' <= 'abc'`|
|>=|Größer oder gleich|`2 >= 1, 'abc' >= 'ABC'`|
|+|Add|`2 + 1, now() + 1d`|
|-|Subtrahieren|`2 - 1, now() - 1h`|
|*|Multiplizieren|`2 * 2`|
|/|Dividieren|`2 / 1`|
|%|Modulo|`2 % 1`|
|like|Die linke Seite enthält eine Übereinstimmung für die rechte Seite|`'abc' like '%B%'`|
|!like|Linke Seite enthält keine Übereinstimmung für rechte Seite|`'abc' !like '_d_'`|
|enthält|Rechte Seite kommt als Teilsequenz von linker Seite vor|`'abc' contains 'b'`|
|!contains|Rechte Seite kommt auf linker Seite nicht vor|`'team' !contains 'i'`|
|startswith|Rechte Seite ist eine öffnende Teilsequenz von linker Seite|`'team' startswith 'tea'`|
|!startswith|Rechte Seite ist keine öffnende Teilsequenz von linker Seite|`'abc' !startswith 'bc'`|
|endswith|Rechte Seite ist eine schließende Teilsequenz von linker Seite|`'abc' endswith 'bc'`|
|!endswith|Rechte Seite ist keine schließende Teilsequenz von linker Seite|`'abc' !endswith 'a'`|
|und|TRUE nur dann, wenn rechte und linke Seite TRUE sind|`(1 == 1) and (2 == 2)`|
|oder|TRUE nur dann, wenn rechte oder linke Seite TRUE ist|`(1 == 1) or (1 == 2)`|

## <a name="aggregation-functions"></a>Aggregationsfunktionen

Aggregationsfunktionen können mit dem summarize-Tabellenoperator verwendet werden, um zusammengefasste Werte zu berechnen. Aktuell werden die folgenden Aggregationsfunktionen unterstützt:

|Funktion|Beschreibung|
|---|---|
|avg()|Gibt den Durchschnitt der Werte innerhalb der Gruppe zurück.|
|count()|Gibt die Anzahl von Datensätzen pro Zusammenfassungsgruppe zurück.|
|countif()|Gibt die Anzahl von Zeilen zurück, für die „Predicate“ als TRUE ausgewertet wird.|
|dcount()|Gibt die Anzahl unterschiedlicher Werte in der Gruppe zurück.|
|max()|Gibt den Höchstwert in der Gruppe zurück.|
|min()|Gibt den Mindestwert in der Gruppe zurück.|
|percentile()|Gibt eine Schätzung für das angegebene Quantil des nächsten Rangs der durch Expr definierten Auffüllung zurück.|
|sum()|Gibt die Summe der Werte innerhalb der Gruppe zurück.|
|sumif()|Gibt eine Summe von Expr zurück, für die das Prädikat als „true“ ausgewertet wird.|

## <a name="scalar-functions"></a>Skalarfunktionen

Skalarfunktionen können in Ausdrücken verwendet werden. Aktuell werden die folgenden Skalarfunktionen unterstützt:

|Funktion|Beschreibung|
|---|---|
|ago()|subtrahiert den angegebenen Zeitraum von der aktuellen UTC-Uhrzeit|
|bin()|Rundet die Werte auf eine datetime-Zahl ab, die ein Vielfaches einer bestimmten Diskretisierungsgröße darstellt.|
|case()|Wertet eine Liste von Prädikaten aus und gibt den ersten Ergebnisausdruck zurück, dessen Prädikat erfüllt ist.|
|datetime_add()|Berechnet einen neuen datetime-Wert aus einem angegebenen datepart-Wert, der mit einem angegebenen Betrag multipliziert und zu einem angegebenen datetime-Wert addiert wird.|
|datetime_diff()|Berechnet die Differenz zwischen zwei Datums-/Uhrzeitwerten.|
|iif()|Wertet das erste Argument aus und gibt entweder den Wert des zweiten oder dritten Arguments aus, abhängig davon, ob das Prädikat als „true“ (zweites) oder „false“ (drittes) ausgewertet wird.|
|indexof()|Die Funktion meldet den nullbasierten (0) Index des ersten Vorkommens einer angegebenen Zeichenfolge in der Eingabezeichenfolge.|
|isnotnull()|Wertet das einzige Argument aus und gibt einen booleschen Wert zurück, der angibt, ob das Argument auf einen Wert ungleich NULL ausgewertet wurde.|
|isnull()|Wertet das einzige Argument aus und gibt einen booleschen Wert zurück, der angibt, ob das Argument auf einen NULL-Wert ausgewertet wurde.|
|now()|gibt die aktuelle UTC-Zeit zurück|
|strcat()|Verkettet zwischen 1 und 64 Argumente.|
|strlen()|Gibt die Länge der Eingabezeichenfolge in Zeichen zurück.|
|substring()|Extrahiert eine Teilzeichenfolge aus einer Quellzeichenfolge beginnend bei einem Index bis zum Ende der Zeichenfolge.|
|tostring()|Konvertiert die Eingabe in eine Zeichenfolgendarstellung.|

## <a name="additional-entities-operators-and-functions-for-cmpivot-from-configuration-manager"></a><a name="bkmk_onprem_only"></a> Zusätzliche Entitäten, Operatoren und Funktionen für CMPivot aus Configuration Manager

> [!Important]
> Diese Elemente werden nicht unterstützt, wenn Sie CMPivot über das Microsoft Endpoint Manager Admin Center ausführen.

|Typ|Element|Beschreibung|
|--|--|---|
|Entität|AccountSID|Konto-SID|
|Entität|FileContent()|Inhalt einer bestimmten Datei|
|Entität|NAPClient|NAP-Client|
|Entität|NAPSystemHealthAgent|NAP-Systemintegritäts-Agent|
|Entität|Registry()|Alle Werte für einen bestimmten Registrierungsschlüssel<!--7371183-->|
|Tabellenoperator|render|Gibt die Ergebnisse als grafische Ausgabe wieder|