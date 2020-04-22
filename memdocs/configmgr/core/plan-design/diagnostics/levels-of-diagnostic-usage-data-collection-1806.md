---
title: Diagnose- und Nutzungsdaten für 1806
titleSuffix: Configuration Manager
description: Hier erfahren Sie mehr über die spezifischen Daten, die Configuration Manager auf jeder Ebene in Version 1806 sammelt.
ms.date: 05/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a0287beb-70a9-4b57-a627-e7bfba27fd3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: f455615db6600a39460b0180d46039535d331f86
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695228"
---
# <a name="diagnostic-and-usage-data-for-1806"></a>Diagnose- und Nutzungsdaten für 1806

*Gilt für: Configuration Manager (Current Branch)*

Die folgenden Abschnitte enthalten zusätzliche Details zu den auf den einzelnen Ebenen gesammelten Daten. Weitere Informationen zu den Ebenen und deren Änderung finden Sie unter [Ebenen von Nutzungsdaten zu Diagnosezwecken](levels-overview.md).

Änderungen gegenüber früheren Versionen sind mit ***[Neu]***, ***[Aktualisiert]***, ***[Entfernt]*** oder ***[Verschoben]*** gekennzeichnet.

> [!IMPORTANT]
> Configuration Manager sammelt auf den Ebenen „Einfach“ und „Erweitert“ keine Standortcodes, Standortnamen, IP-Adressen, Benutzer- oder Computernamen, physischen Adressen oder E-Mail-Adressen. Eine Erfassung dieser Informationen auf der Ebene „Vollständig“ ist nicht zielführend. Erst in erweiterten Diagnoseinformationen wie Protokolldateien oder Arbeitsspeicher-Momentaufnahmen sind diese Informationen möglicherweise enthalten. Microsoft nutzt diese Informationen weder, um Sie zu identifizieren oder zu kontaktieren, noch zu Werbezwecken.

## <a name="level-1---basic"></a><a name="bkmk_level1"></a> Ebene 1: Basis

Bei Configuration Manager Version 1806 umfasst diese Ebene folgende Daten:

- Statistik zu den Configuration Manager-Konsolenverbindungen: Betriebssystemversion, Sprache, SKU und Architektur, Systemspeicher, Anzahl der logischen Prozessoren, Verbindungsstandort-ID, installierte .NET-Versionen und Sprachpakete für die Konsole

- Anzahl der grundlegenden Anwendungs- und Bereitstellungstypen: Gesamtzahl der Apps, Gesamtzahl der Apps mit mehreren Bereitstellungstypen, Gesamtzahl der Apps mit Abhängigkeiten, Gesamtzahl der abgelösten Apps und Anzahl der verwendeten Bereitstellungsmethoden

- Grundlegende Daten zur Configuration Manager-Standorthierarchie: Standortliste, Typ, Version, Status, Anzahl von Clients und Zeitzone

- ***[Aktualisiert]*** Grundlegende Datenbankkonfiguration: Prozessoren, Speichergröße, Speichereinstellungen, Datenbankkonfiguration von Configuration Manager, Größe der Configuration Manager-Datenbank, Clusterkonfiguration und Konfiguration verteilter Ansichten

- Grundlegende Statistiken zur Ermittlung: Ermittlungsanzahl und minimale/maximale/durchschnittliche Gruppengrößen; Zeitpunkt, wenn der Standort komplett mit Azure Active Directory-Diensten ausgeführt wird

- Grundlegende Endpoint Protection-Informationen zur Antischadsoftware-Clientversionen

- Anzahl der Images für die grundlegende Betriebssystembereitstellung

- Grundlegende Informationen zum Standortsystemserver: verwendete Standortsystemrollen, Internet- und SSL-Status, Betriebssystem, Prozessoren, physischer oder virtueller Computer und Nutzung der Hochverfügbarkeit des Standortservers

- Configuration Manager-Datenbankschema (Hash aller Objektdefinitionen)

- Konfigurierte Ebene für Diagnose- und Nutzungsdaten, Online- oder Offlinemodus und schnelle Updatekonfiguration

- Anzahl der Sprachen und Gebietsschemas der Clients

- Anzahl der Configuration Manager-Client-, Betriebssystem- und Office-Versionen

- Anzahl der Betriebssysteme für verwaltete Geräte und der von Exchange Connector festgelegten Richtlinien

- Anzahl von Windows 10-Geräten nach Branch und Build

- Anzahl von Windows 10-Clients, die Windows Update für Unternehmen verwenden  

- Metriken zur Datenbankleistung: Datenträgerverwendung, Informationen zur Replikationsverarbeitung, die wichtigsten gespeicherten SQL Server-Prozeduren nach Prozessor

- Informationen zu Verteilungspunkt- und Verwaltungspunkttypen sowie zur grundlegenden Konfiguration: geschützt, vorab bereitgestellt, PXE, Multicast, SSL-Status, Pull-/Peerverteilungspunkte, für MDM aktiviert, SSL-fähig usw.

- Gehashte Liste der Erweiterungen für die Eigenschaftenseiten und Assistenten der Verwaltungskonsole

- Setupinformationen:
     - Build, Installationstyp, Sprachpakete, Funktionen, die Sie aktiviert haben   

     - Verwendung der Vorabversion, Setup Medientyp, Verzweigungstyp

     - Ablaufdatum der Software Assurance      

     - Aktualisieren des Paketbereitstellungsstatus und der Fehler, des Downloadstatus und der Voraussetzungsfehler 

     - Updateverwendung (Fast Ring)

     - Skriptversion nach dem Upgrade

- SQL-Version, Service Pack-Ebene, Edition, Sortierungs-ID und Zeichensatz     

- Statistiken zu Diagnose- und Nutzungsdaten: bei Ausführung, Laufzeit, Fehlern

- Ob die Netzwerkermittlung aktiviert oder deaktiviert ist

- Anzahl der in Azure Active Directory eingebundenen Clients

- Anzahl von stufenweisen Bereitstellungen, nach Typ erstellt

- Anzahl der Clients für erweiterte Interoperabilität

- Gehashte Liste der Eigenschaften der Hardwareinventur mit mehr als 255 Zeichen

- ***[Verschoben]*** Anzahl der Clients mit der Registrierungsmethode „Co-Verwaltung“  

- ***[Verschoben]*** Fehlerstatistiken für die Co-Verwaltungsregistrierung  

- ***[Neu]*** Anzahl der Clients nach dem Alter des Windows-Betriebssystems für das nächste Intervall von drei Monaten  

- ***[Neu]*** Die auf Clients verwendeten Top-10-Prozessornamen  

- ***[Neu]*** Anzahl und Verarbeitungsrate der Configuration Manager-Schlüsselobjekte: Data Discovery Records (DDR), Zustandsmeldungen, Statusmeldungen, Hardwareinventur, Softwareinventur und Gesamtanzahl der Dateien in Posteingängen  

- ***[Neu]*** Informationen zum Datenträger des Standortservers und zur Prozessleistung  

- ***[Neu]*** Informationen zur Betriebszeit und zur Speicherauslastung bei Prozessen auf dem Configuration Manager-Standortserver  

- ***[Neu]*** Anzahl der Abstürze in Prozessen auf dem Configuration Manager-Standortserver und Watson-Signatur-ID (sofern verfügbar)  



## <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> Ebene 2: Erweitert

Bei Configuration Manager Version 1806 umfasst diese Ebene folgende Daten:

### <a name="application-management"></a>Anwendungsverwaltung  

- App-Anforderungen: Anzahl der integrierten Bedingungen, die von der Bereitstellungstechnologie referenziert werden

- App-Ablösung, maximale Kettentiefe

- Statistiken über Genehmigungen für Anwendungen und Häufigkeit der Nutzung

- Größenstatistiken zu Anwendungsinhalten

- Informationen zur Anwendungsbereitstellung: Installation vs. Deinstallation, Genehmigung erforderlich, Benutzerinteraktion aktiviert/deaktiviert, Abhängigkeit, Ablösung und Verwendungsanzahl des Features „Installationsverhalten“  

- Größe der Anwendungsrichtlinie und Komplexitätsstatistiken

- Statistiken zur Anforderung verfügbarer Anwendungen

- Grundlegende Konfigurationsinformationen für Pakete und Programme: Bereitstellungsoptionen und Programmflags

- Grundlegende Informationen zu Verwendung/Zielgruppenadressierung für Bereitstellungstypen: adressierter Benutzer/adressiertes Gerät, erforderlich/verfügbar und universelle Apps

- Anzahl von App-V-Umgebungen und Bereitstellungseigenschaften

- Anzahl der Anwendungsanwendbarkeit nach Betriebssystem  

- Anzahl der Anwendungen, auf die von einer Tasksequenz verwiesen wird

- Anzahl eindeutiger Brandings für den Anwendungskatalog

- Anzahl der über das Office 365-Dashboard erstellten Anwendungen

- Anzahl der Pakete nach Typ  

- Anzahl der Paket-/Programmbereitstellungen  

- Anzahl von Windows 10-lizenzierten Anwendungslizenzen  

- Anzahl der Windows Installer-Bereitstellungstypen pro Einstellung für die Deinstallation von Inhalten

- Anzahl der Apps im Microsoft Store für Unternehmen und Synchronisierungsstatistiken: zusammengefasste App-Typen, Status lizenzierter Apps und Anzahl der lizenzierten Online- und Offline-Apps  

- Wartungsfenstertyp und -dauer  

- Minimale/maximale/durchschnittliche Anzahl von Anwendungsbereitstellungen pro Benutzer/Gerät in einem bestimmten Zeitraum

- Am häufigsten auftretende Fehlercodes pro Bereitstellungstechnologie

- Konfigurationsoptionen für und Anzahl von MSI

- Statistiken zur Endbenutzerinteraktion mit der Benachrichtigung über erforderliche Softwarebereitstellungen   

- Nutzung des Universal Data Access, Art der Erstellung

- Aggregierte Statistiken zur Affinität zwischen Benutzer und Gerät 

- Maximale und durchschnittliche primäre Benutzer pro Gerät  

- ***[Neu]*** Nutzung globaler Anwendungsbedingungen nach Typ  

- ***[Neu]*** Konfiguration für die Anpassung des Softwarecenters  

- ***[Neu]*** Package Conversion Manager-Bereitschaft und -Anzahl  

- ***[Neu]*** Anzahl der Methoden zur Erkennung von Anwendungen nach Typ  

- ***[Neu]*** Anzahl der Anwendungserzwingungsfehler  

- ***[Neu]*** MSI-Installereigenschaften 

- ***[Neu]*** Statistiken der Anforderungen für die Installation von Benutzern



### <a name="client"></a>Client  

- Clientversion von Active Management Technology (AMT)

- BIOS-Alter in Jahren

- Anzahl der Geräte mit aktiviertem sicheren Start

- Anzahl der Geräte nach TPM-Zustand

- Automatisches Clientupgrade: Konfigurierung der Bereitstellung einschließlich Pilottests von Clients und Verwendung des Ausschlusses (erweiterter Interoperabilitätsclient)

- Konfigurieren der Cachegrößen des Clients

- Downloadfehler in der Clientbereitstellung

- ***[Aktualisiert]*** Clientintegritätsstatistiken und Zusammenfassung wichtiger Probleme nach Clientversion

- Status der Clientbenachrichtigungsaktion: wie oft jede Aktion ausgeführt wird, max. Anzahl von Zielclients und durchschnittliche Erfolgsrate

- Anzahl der Clientinstallationen von jedem Quellspeicherorttyp  

- Anzahl der Fehler bei der Clientinstallation  

- Anzahl der von Hyper-V oder Azure virtualisierten Geräte  

- Anzahl der Softwarecenteraktionen   

- Anzahl der Geräte mit aktiviertem UEFI

- Bereitstellungsmethoden für Clients und Anzahl der Clients pro Bereitstellungsmethode

- Liste/Anzahl der aktivierten Client-Agents  

- OS-Alter in Monaten

- Anzahl von Hardwareinventurklassen, Softwareinventurregeln und Dateisammlungsregeln

- Statistiken für den Nachweis der Geräteintegrität: häufigste Fehlercodes, Anzahl der lokalen Server und Anzahl der Geräte in verschiedenen Zuständen

- Anzahl der Geräte nach Standardbrowser  

- ***[Neu]*** Anzahl der Configuration Manager generierte Serverauthentifizierungszertifikate  

- ***[Neu]*** Anzahl der Microsoft Surface-Geräte pro Modell  


### <a name="cloud-services"></a>Cloud Services  

- Ermittlungsstatistiken zu Azure Active Directory

- Statistiken zur Konfiguration und Nutzung von Cloud Management Gateway: Anzahl der Regionen und Umgebungen und Statistiken zur Authentifizierung/Autorisierung

- Anzahl der mit Configuration Manager verbundenen Azure Active Directory-Anwendungen und -Dienste

- Anzahl von Sammlungen, die mit Azure Log Analytics synchronisiert wurden

- Anzahl von Upgrade Analytics-Connectors

- Information, ob der Azure Log Analytics-Cloudconnector aktiviert ist  

- ***[Neu]*** Anzahl der Pullverteilungspunkte mit einem Cloudverteilungspunkt als Quellspeicherort  


### <a name="co-management"></a>Co-Verwaltung  
- Aggregierte Nutzungsstatistiken für die Co-Verwaltung: Anzahl der registrierten Clients; Clients, die Richtlinien erhalten; Workloadstatus; Größe der Pilot-/Ausschlusssammlung; Registrierungsfehler  

- Registrierungszeitplan und Verlaufsstatistik  

- Anzahl der Clients, die für die Co-Verwaltung geeignet sind  

- Verknüpfter Microsoft Intune-Mandant


### <a name="collections"></a>Sammlungen  

- Verwendung der Sammlungs-ID (nicht genügend IDs)

- Statistiken zur Sammlungsauswertung: Abfragezeit, zugewiesene/nicht zugewiesene Anzahl, Anzahl nach Typ, ID-Rollover und Verwendung von Regeln

- Sammlungen ohne eine Bereitstellung


### <a name="compliance-settings"></a>Kompatibilitätseinstellungen  

- Grundlegende Informationen zur Konfigurationsbaseline: Zählerwert, Anzahl von Bereitstellungen und Anzahl der Verweise

- Statistiken zu Konformitätsrichtlinienfehlern

- Anzahl der Konfigurationselemente nach Typ  

- Anzahl von Bereitstellungen, die auf integrierte Einstellungen verweisen, einschließlich wiederhergestellte Einstellungen  

- Anzahl von Regeln und Bereitstellungen, die für benutzerdefinierte Einstellungen erstellt wurden, einschließlich wiederhergestellte Einstellungen  

- Anzahl der bereitgestellten Vorlagen für den Registrierungsdienst für Netzwerkgeräte (Simple Certificate Enrollment Protocol, SCEP), VPN, WLAN, Zertifikate (.pfx) und Konformitätsrichtlinien

- Anzahl der Bereitstellungen von SCEP-Zertifikaten, VPN-, WLAN-, Zertifikaten (.pfx) und Konformitätsrichtlinien pro Plattform

- Windows Hello for Business-Richtlinie (erstellt, bereitgestellt)  

- ***[Neu]*** Anzahl der bereitgestellten Richtlinien für den Microsoft Edge-Browser  


### <a name="content"></a>Content  

- Statistiken für Begrenzungsgruppen: wie viele schnelle, wie viele langsame, Anzahl pro Gruppe und Fallbackbeziehungen

- Informationen zur Begrenzungsgruppe: Anzahl der Grenzen und Standortsysteme, die jeder Begrenzungsgruppe zugewiesen sind  

- Begrenzungsgruppenbeziehungen und Fallbackkonfiguration

- Statistiken über Downloads von Clients

- Anzahl der Grenzen nach Typ  

- Peercacheclient-Anzahl, Statistiken zur Nutzung und zu teilweisen Downloads

- Informationen zur Verteilungs-Manager-Konfiguration: Threads, Wiederholungsverzögerung, Anzahl der Wiederholungsversuche und Einstellungen für Pullverteilungspunkte  

- Informationen zur Verteilungspunktkonfiguration: Verwenden von BranchCache und Verteilungspunktüberwachung

- Informationen zur Verteilungspunktgruppe: Anzahl der jeder Verteilungspunktgruppe zugewiesenen Pakete und Verteilungspunkte  

- ***[Neu]*** Typ der Inhaltsbibliothek (lokal oder remote)  


### <a name="endpoint-protection"></a>Endpoint Protection  

- Microsoft Defender Advanced Threat Protection (ATP)-Richtlinien (früher als Windows Defender ATP bekannt): Anzahl der Richtlinien und Angabe, ob Richtlinien bereitgestellt werden

- Anzahl der Warnungen, die für das Endpoint Protection-Feature konfiguriert sind  

- Anzahl der ausgewählten Sammlungen, die im Endpoint Protection-Dashboard angezeigt werden sollen  

- Anzahl von Windows Defender Exploit Guard-Richtlinien, -Bereitstellungen und -Zielclients

- Fehler bei der Endpoint Protection-Bereitstellung, Anzahl der Bereitstellungsfehlercodes für Endpoint Protection-Richtlinien  

- Endpoint Protection-Antischadsoftware und Windows-Firewall-Richtliniennutzung (Anzahl der eindeutigen der Gruppe zugewiesenen Richtlinien)<br /><br /> Diese Daten enthalten keine Informationen über in der Richtlinie enthaltene Einstellungen.  


### <a name="migration"></a>Migration  

- Anzahl der migrierten Objekte (Migrations-Assistent verwenden)


### <a name="mobile-device-management-mdm"></a>Verwaltung mobiler Geräte (MDM)  

- Anzahl der ausgegebenen Aktionen für mobile Geräte: Befehle „Sperren“, „PIN zurücksetzen“, „Zurücksetzen“, „Außerkraftsetzen“ und „Jetzt synchronisieren“

- Anzahl der Richtlinien für mobile Geräte  

- Anzahl der von Configuration Manager und Microsoft Intune verwalteten mobilen Geräte und Art ihrer Registrierung (Massenregistrierung, benutzerbasierte Registrierung)  

- Anzahl der Benutzer mit mehreren registrierten mobilen Geräten  

- Zeitplan zu Abrufvorgängen für mobile Geräte und Statistiken zur Eincheckdauer mobiler Geräte  


### <a name="microsoft-intune-troubleshooting"></a>Problembehandlung für Microsoft Intune  

- Anzahl und Größe von Geräteaktionen (Zurücksetzen, Außerkraftsetzen, Sperren), Nutzungsdaten und Datenmeldungen, die auf Microsoft Intune repliziert wurden

- Anzahl und Größe der von Microsoft Intune heruntergeladenen Meldungen zum Zustand, Status und Mandantenzustand, zur Inventur und Konformität und zu RDR, DDR, UDX, POL, LOG, Cert, CRP, Resync, CFD, RDO, BEX und ISM

- Statistiken zur vollständigen und Deltabenutzersynchronisierung für Microsoft Intune


### <a name="on-premises-mobile-device-management-mdm"></a>Lokale Verwaltung mobiler Geräte (Mobile Device Management, MDM)  

- Anzahl von Windows 10-Massenregistrierungspaketen und -profilen  

- Statistiken zu erfolgreichen und fehlerhaften lokalen MDM-Anwendungsbereitstellungen  


### <a name="os-deployment"></a>Bereitstellung des Betriebssystems  

- Anzahl der Startimages, Treiber, Treiberpakete, multicastfähigen Verteilungspunkte, PXE-fähigen Verteilungspunkte und Tasksequenzen  

- Anzahl der Startimages nach Configuration Manager-Clientversion

- Anzahl der Startimages nach Windows PE-Version

- Anzahl von Editionsaktualisierungsrichtlinien

- Anzahl der von PXE ausgeschlossenen Hardwarebezeichner

- Anzahl der Betriebssystembereitstellungen nach Version des Betriebssystems

- Anzahl der Betriebssystemupgrades im Zeitverlauf

- Anzahl der Tasksequenzbereitstellungen, bei denen Inhalte vorab heruntergeladen wurden

- Anzahl der Tasksequenzschrittnutzung

- Installierte Windows ADK-Version  

- ***[Neu]*** Anzahl der Tasks für die Imagewartung  


### <a name="site-updates"></a>Standortupdates  

- Versionen installierter Configuration Manager-Hotfixes


### <a name="software-updates"></a>Softwareupdates  

- Verfügbare und Stichtagdeltawerte, die in Regeln zur automatischen Bereitstellung verwendet werden  

- Durchschnittliche und maximale Anzahl von Zuweisungen pro Update  

- Clientupdateauswertung und Überprüfungszeitpläne  

- Vom Softwareupdatepunkt synchronisierte Klassifikationen

- Statistiken zu Clusterpatches  

- Konfiguration von Windows 10-Express-Updates

- Konfigurationen, die für aktive Windows 10-Wartungspläne verwendet werden  

- Anzahl der bereitgestellten Office 365-Updates  

- Anzahl der synchronisierten Microsoft Surface-Treiber

- Anzahl der Updategruppen und -zuweisungen  

- Anzahl der Updatepakete und maximale/minimale/durchschnittliche Anzahl der von den Paketen angesprochenen Verteilungspunkte  

- Anzahl der mit System Center Updates Publisher erstellten und bereitgestellten Updates  

- Anzahl der erstellten und bereitgestellten Windows Update for Business-Richtlinien

- Aggregierte Statistiken von Windows Update for Business-Konfigurationen

- Anzahl der an die Synchronisierung gebundenen Regeln zur automatischen Bereitstellung  

- Anzahl der Regeln zur automatischen Bereitstellung, die neue Updates erstellen oder Updates zu einer vorhandenen Gruppe hinzufügen  

- Anzahl der Regeln zur automatischen Bereitstellung mit mehreren Bereitstellungen  

- Anzahl der Updategruppen und minimale/maximale/durchschnittliche Anzahl der Updates pro Gruppe  

- Anzahl von Updates und Prozentsatz der bereitgestellten, abgelaufenen, ersetzten und heruntergeladenen Updates sowie der Updates mit EULAs  

- Statistiken für den Lastenausgleich des Softwareupdatepunkts

- Softwareupdatepunkt-Synchronisierungszeitplan  

- Gesamtzahl bzw. durchschnittliche Anzahl von Sammlungen mit Softwareupdatebereitstellungen sowie maximale/durchschnittliche Anzahl der bereitgestellten Updates  

- Updateüberprüfungs-Fehlercodes und Anzahl der Computer  

- Windows 10-Dashboardinhaltsversionen  

- ***[Neu]*** Abonnements und Nutzung des Updatekatalogs für Drittanbietersoftware  

- ***[Neu]*** Anzahl der mit und ohne Inhalte bereitgestellten Softwareupdates  


### <a name="sqlperformance-data"></a>SQL-/Leistungsdaten  

- Konfiguration und Dauer der Standortzusammenfassung

- Anzahl der größten Datenbanktabellen  

- Operative Ermittlungsstatistik (Anzahl der gefundenen Objekte)

- Ermittlungstypen, aktiviert und Zeitplan (vollständig, inkrementell)

- Informationen zu SQL Always On-Replikat, Nutzung und Integritätsstatus

- Leistungsprobleme der verfolgten SQL-Änderungen, Beibehaltungsdauer und Status der automatischen Bereinigung

- Beibehaltungsdauer der verfolgten SQL-Änderungen

- Leistungsstatistiken zu Status und Statusmeldungen, einschließlich der häufigsten und kostspieligsten Meldungstypen


### <a name="miscellaneous"></a>Verschiedenes  

- Konfiguration des Data Warehouse-Dienstpunkts, einschließlich Synchronisierungszeitplan und durchschnittliche Dauer

- Statistiken zur Anzahl von Skripts und der Ausführung

- Anzahl der Wake-On-LAN-Standorte (WOL)

- Berichte von Nutzungs- und Leistungsstatistiken

- Nutzungsstatistiken für die stufenweise Bereitstellung  

- ***[Neu]*** CMPivot-Nutzungsstatistiken  

- ***[Neu]*** Anzahl und Status der Elemente für Verwaltungseinblicke  

- ***[Neu]*** Anzahl der Abstürze in eindeutigen Prozessen außerhalb von Configuration Manager auf dem Standortserver und die Watson-Signatur-ID (sofern verfügbar)



##  <a name="level-3---full"></a><a name="bkmk_level3"></a> Ebene 3: Vollständig

Bei Configuration Manager Version 1806 umfasst diese Ebene folgende Daten:

- Informationen zum Zeitplan für die Auswertung der automatischen Bereitstellungsregel

- Zusammenfassung zur ATP-Integrität

- Statistiken zur Sammlungsauswertung und -aktualisierung

- Statistiken zu Konformitätsrichtlinien zu Konformität und Fehlern

- Konformitätseinstellungen: Konfigurationsdetails für SCEP-, VPN-, WLAN- und Konformitätsrichtlinienvorlagen

- DCM-Konfigurationspaket für die Configuration Manager-Nutzung

- Detaillierte Installationsfehler der Client-Bereitstellung

- Zusammenfassung zur Endpoint Protection-Integrität: einschließlich Anzahl der geschützten, gefährdeten, unbekannten und nicht unterstützten Clients

- Endpoint Protection-Richtlinienkonfiguration

- Liste der Prozesse, die mit dem Installationsverhalten für Anwendungen konfiguriert wurden

- Minimale/maximale/durchschnittliche Anzahl von Stunden seit der letzten Überprüfung auf Softwareupdates

- Minimale/maximale/durchschnittliche Anzahl der inaktiven Clients in Softwareupdate-Bereitstellungssammlungen

- Minimale/maximale/durchschnittliche Anzahl von Softwareupdates pro Paket

- Statistiken zur MSI-Produktcodebereitstellung 

- Gesamtkompatibilität der Softwareupdatebereitstellungen

- Anzahl der Gruppen mit abgelaufenen Softwareupdates

- Codes und Anzahl der Fehler bei der Softwareupdatebereitstellung

- Informationen zur Softwareupdatebereitstellung: Prozentsatz der Zielbereitstellungen mit Client- bzw. UTC-Zeit, erforderlich bzw. optional bzw. automatisch, Neustartunterdrückung

- Vom Softwareupdatepunkt synchronisierte Softwareupdateprodukte

- Prozentsätze der erfolgreichen Überprüfungen auf Softwareupdates

- Die besten 50 CPUs in der Umgebung

- Typ der Exchange Active Sync-Richtlinien (EAS) für den bedingten Zugriff (blockiert oder in Quarantäne) für mit Microsoft Intune verwaltete Geräte

- Details zu Microsoft Store für Unternehmen-Anwendungen: nicht-aggregierte Liste synchronisierter Anwendungen, darunter App-ID, Online- oder Offlinestatus und die Gesamtzahl erworbener Lizenzen
