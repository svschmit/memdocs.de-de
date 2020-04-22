---
title: Diagnosedaten für Version 1702
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über die Ebenen der Diagnose- und Nutzungsdaten, die Configuration Manager-Version 1702 sammelt.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d43ab033-2902-4681-8716-b4b17a6df372
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 155d62b3b8876f3bdf7dab218451c38e7cca6aed
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81698128"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1702-of-configuration-manager"></a>Ebenen der Sammlung von Nutzungsdaten zu Diagnosezwecken für Configuration Manager Version 1702

*Gilt für: Configuration Manager (Current Branch)*

Version 1702 von Configuration Manager sammelt drei Arten von Diagnose- und Nutzungsdaten: **Einfach**, **Erweitert** und **Vollständig**. Standardmäßig ist dieses Feature auf die Ebene „Erweitert“ festgelegt. Die folgenden Abschnitte enthalten zusätzliche Details zu den auf den einzelnen Ebenen gesammelten Daten.

Änderungen gegenüber früheren Versionen sind mit ***[Neu]***, ***[Aktualisiert]***, ***[Entfernt]*** oder ***[Verschoben]*** gekennzeichnet.


> [!IMPORTANT]
>  Configuration Manager sammelt auf den Ebenen „Basis“ und „Erweitert“ keine Standortcodes, Standortnamen, IP-Adressen, Benutzer- oder Computernamen, physischen Adressen oder E-Mail-Adressen. Die auf der Ebene „Vollständig“ erfassten Daten (möglicherweise in erweiterten Diagnoseinformationen wie Protokolldateien oder Arbeitsspeicher-Momentaufnahmen enthaltene Daten) werden nicht zielgerichtet gesammelt. Sie werden von Microsoft auch nicht zu Werbezwecken oder dazu verwendet, Sie zu identifizieren oder sich mit Ihnen in Verbindung zu setzen.



##  <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> Ändern der Ebene
 Administratoren mit einem rollenbasierten Verwaltungsbereich, der **Ändern**-Berechtigungen für die **Standort**-Objektklasse umfasst, können in den Einstellungen der Configuration Manager-Konsole unter „Diagnose- und Nutzungsdaten“ die Ebene der erfassten Daten ändern.

Sie können die Datensammlungsebene innerhalb der Konsole ändern, indem Sie zu **Verwaltung** > **Überblick** > **Standortkonfiguration** > **Standorte** navigieren. Öffnen Sie die **Hierarchieeinstellungen**, und wählen Sie die Datenebene aus, die Sie verwenden möchten.  



##  <a name="level-1---basic"></a><a name="bkmk_level1"></a> Ebene 1: Basis
Die Ebene „Basis“ umfasst Daten über Ihre Hierarchie, Daten, die für die Verbesserung Ihrer Installations- oder Upgradeerfahrung nötig sind, sowie Daten, die zur Ermittlung der für Ihre Hierarchie infrage kommenden Configuration Manager-Updates benötigt werden.

Bei Version 1702 von Configuration Manager umfasst diese Ebene folgende Daten:

- Verwaltungskonsole:
   - Statistiken zu den Konsolenverbindungen (Betriebssystemversion, Sprache, SKU und Architektur, Systemspeicher, Anzahl der logischen Prozessoren, Connect-Website-ID, installierte .NET-Versionen und Konsolensprachpakete)

- Anzahl der grundlegenden Anwendungs- und Bereitstellungstypen (Gesamtzahl der Apps, Gesamtzahl der Apps mit mehreren Bereitstellungstypen, Gesamtzahl der Apps mit Abhängigkeiten, Gesamtzahl der ersetzten Apps und Anzahl der verwendeten Bereitstellungstechnologien)

- Grundlegende Daten zur Configuration Manager-Standorthierarchie (Standortliste, Typ, Version, Status, Anzahl von Clients und Zeitzone)

- Grundlegende Informationen zur Datenbankkonfiguration (Prozessoren, Clusterkonfiguration und Konfiguration verteilter Ansichten)

- ***[Aktualisiert]*** Grundlegende Statistiken zur Ermittlung (Ermittlungsanzahl und minimale/maximale/durchschnittliche Gruppengrößen), auch dann, wenn der Standort komplett mit Azure Active Directory-Diensten ausgeführt wird.

- Grundlegende Informationen zu Endpoint Protection (Antischadsoftware-Clientversionen)

- Anzahl der grundlegenden Betriebssystembereitstellungen (OSDs) (Images)

- Grundlegende Informationen zum Standortsystemserver (verwendete Standortsystemrollen, Internet- und SSL-Status, Betriebssystem, Prozessoren sowie physischer oder virtueller Computer)

- Configuration Manager-Datenbankschema (Hash aller Objektdefinitionen)

- Konfigurierte Telemetrieebene, Modus (online oder offline) und schnelle Updatekonfiguration

- Anzahl der Sprachen und Gebietsschemas der Clients

- Anzahl der Configuration Manager-Client- und -Betriebssystemversionen

- Anzahl der Betriebssysteme für verwaltete Geräte und der von Exchange Connector festgelegten Richtlinien

- Anzahl von Windows 10-Geräten nach Branch und Build

- Metriken zur Datenbankleistung (Informationen zur Replikationsverarbeitung, die wichtigsten gespeicherten SQL Server-Prozeduren nach Prozessor und Datenträgerverwendung)

- Informationen zu Verteilungspunkt- und Verwaltungspunkttypen sowie zur grundlegenden Konfiguration (geschützt, vorab bereitgestellt, PXE, Multicast, SSL-Status, Pull-/Peerverteilungspunkte, MDM-aktiviert, SSL-fähig usw.)

- Setupinformationen:
     - Build, Installationstyp, Sprachpakete, Funktionen, die Sie aktiviert haben   

     - Verwendung der Vorabversion, Setup Medientyp, Verzweigungstyp

     - Ablaufdatum der Software Assurance      

     - Aktualisieren des Paketbereitstellungsstatus und der Fehler, des Downloadstatus und der Voraussetzungsfehler 

     - Updateverwendung (Fast Ring)

     - Skriptversion nach dem Upgrade

- SQL-Version, Service Pack-Ebene, Edition, Sortierungs-ID und Zeichensatz     
- Telemetriestatistiken (Ausführungszeit, Laufzeit, Fehler)

- Verwenden der Netzwerkermittlung (aktiviert oder deaktiviert)




##  <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> Ebene 2: Erweitert
Die Ebene „Erweitert“ ist die Standardeinstellung nach dem Setup. Diese Ebene enthält die auf der Ebene „Basis“ erfassten Daten und featurespezifische Daten (Häufigkeit und Dauer der Verwendung), Configuration Manager-Clienteinstellungen (Name der Komponente, Status und bestimmte Einstellungen wie Abrufintervalle) sowie grundlegende Informationen zu Softwareupdates.

Diese Ebene wird empfohlen, weil sie Microsoft die Daten bereitstellt, die mindestens erforderlich sind, um in künftigen Versionen der Produkte und Dienste nützliche Verbesserungen vorzunehmen. Diese Ebene erfasst keine Objektnamen (Websites, Benutzer, Computer oder Objekte) und keine Details zu sicherheitsrelevanten Objekten oder Sicherheitsrisiken, wie etwa die Anzahl der Systeme, die Softwareupdates erfordern.

Bei Version 1702 von Configuration Manager umfasst diese Ebene folgende Daten:

- **Anwendungsverwaltung:**  

   - App-Anforderungen (Anzahl der integrierten Bedingungen wird von der Bereitstellungstechnologie referenziert)

   - App-Ablösung, maximale Kettentiefe

   - Statistiken über Genehmigungen für Anwendungen und Häufigkeit der Nutzung

   - ***[Aktualisiert]*** Informationen zur Anwendungsbereitstellung (Verwendung von Installation im Vergleich zur Deinstallation, Genehmigung erforderlich, Benutzerinteraktion aktiviert/deaktiviert, Abhängigkeit, Ablösung und Verwendungsanzahl der Funktion „Installationsverhalten“)  

   - Größe der Anwendungsrichtlinie und Komplexitätsstatistiken

   - Statistiken zur Anforderung verfügbarer Anwendungen

   - ***[Neu]*** Grundlegende Konfigurationsinformationen für Pakete und Programme (Bereitstellungsoptionen und Programmflags)

   - Grundlegende Informationen zu Verwendung/Zielgruppenadressierung für innerhalb der Organisation verwendete Bereitstellungstypen (adressierter Benutzer/adressiertes Gerät, erforderlich/verfügbar und universelle Apps)

   - Statistiken für Begrenzungsgruppen (wie viele schnelle, wie viele langsame sowie Anzahl pro Gruppe)

   - Anzahl von App-V-Umgebungen und Bereitstellungseigenschaften

   - Anzahl der Anwendungsanwendbarkeit nach Betriebssystem  

   - ***[Neu]*** Anzahl der Anwendungen, die von einer Tasksequenz verwiesen werden

   - Anzahl der Pakete nach Typ  

   - Anzahl der Paket-/Programmbereitstellungen  

   - Anzahl von Windows 10-lizenzierten Anwendungslizenzen  

   - Anzahl der Apps im Windows Store für Unternehmen und Synchronisierungsstatistiken (einschließlich zusammengefasste App-Typen, Status lizenzierter Apps und Anzahl der Online- und Offline-lizenzierten Apps)  

   - Wartungsfenstertyp und -dauer  

   - Minimale/maximale/durchschnittliche Anzahl von Anwendungsbereitstellungen pro Benutzer/Gerät in einem bestimmten Zeitraum

   - ***[Neu]***  Am häufigsten vorkommende Fehlercodes der Anwendungsinstallation von der Bereitstellungstechnologie

   - Konfigurationsoptionen für und Anzahl von MSI

   - ***[Neu]*** Statistiken für Endbenutzerinteraktionen mit Benachrichtigung für die erforderlichen Softwarebereitstellungen   

   - Nutzung des Universal Data Access (UDA), Art der Erstellung




- **Client:**  

   - Clientversion von Active Management Technology (AMT)

   - BIOS-Alter in Jahren

   - Automatisches Clientupgrade: Konfigurierung der Bereitstellung einschließlich Pilottests von Clients und Verwendung des Ausschlusses (erweiterter Interoperabilitätsclient)

   - Konfigurieren der Cachegrößen des Clients

   - Downloadfehler in der Clientbereitstellung

   - Clientintegritätsstatistiken und Zusammenfassung wichtiger Probleme

   - Status der Clientbenachrichtigungsaktion (wie oft jede Aktion ausgeführt wird, max. Anzahl von Zielclients und durchschnittliche Erfolgsrate)
   - Anzahl der Clientinstallationen von jedem Quellspeicherorttyp  

   - Anzahl der Fehler bei der Clientinstallation  

   - ***[Neu]*** Anzahl der Geräte, die von Hyper-V oder Azure virtualisiert wurden  

   - Anzahl der Softwarecenteraktionen   

   - ***[Neu]*** Anzahl der UEFI-fähigen Geräte

   - Bereitstellungsmethoden für Clients und Anzahl der Clients pro Bereitstellungsmethode

   - Liste/Anzahl der aktivierten Client-Agents  

   - Alter des Betriebssystems in Monaten

   - Anzahl von Hardwareinventurklassen, Softwareinventurregeln und Dateisammlungsregeln

   - ***[Neu]*** Statistiken für den Nachweis der Geräteintegrität, einschließlich der häufigsten Fehlercodes, der Anzahl von lokalen Servern und der Anzahl von Geräten in verschiedenen Zuständen



- **Cloud Services:**

  - Statistiken zur Konfigurierung und Verwendung des Cloudverwaltungsgateways

  - ***[Neu]*** Anzahl der Clients, die in die Azure Active Directory-Dienste eingebunden sind

  - Anzahl der Sammlungen, die mit Operations Management Suite synchronisiert werden

  - Anzahl von Upgrade Analytics-Connectors

  - Angabe, ob der Operations Management Suite-Cloud-Connector aktiviert ist




- **Sammlungen:**

    - Verwendung der Sammlungs-ID (nicht genügend IDs)

    - Statistiken zur Sammlungsauswertung (Abfragezeit, zugewiesene/nicht zugewiesene Anzahl, Anzahl nach Typ, ID-Rollover und Verwendung von Regeln)

    - Sammlungen ohne eine Bereitstellung




- **Kompatibilitätseinstellungen:**  

    - Grundlegende Informationen zur Konfigurationsbaseline (Zählerwert, Anzahl von Bereitstellungen und Anzahl der Verweise)  

    - Anzahl der Konfigurationselemente nach Typ  

    - Anzahl von Bereitstellungen, die auf integrierte Einstellungen verweisen (wiederhergestellte Einstellungen werden jetzt erfasst)  

    - Anzahl von Regeln und Bereitstellungen, die für benutzerdefinierte Einstellungen erstellt wurden (wiederhergestellte Einstellungen werden jetzt erfasst)  
    -  Anzahl der bereitgestellten Simple Certificate Enrollment-Protokollvorlagen (SCEP) und der VPN-, WLAN-, Zertifikat- (.PFX) und Konformitätsrichtlinienvorlagen

    - Anzahl der SCEP-Zertifikat-, VPN-, WLAN-, Zertifikat- (.PFX) und Konformitätsrichtlinienbereitstellungen je Plattform

    - Passport for Work-Richtlinie (erstellt, bereitgestellt)



- **Inhalt:**  

    - Informationen zur Begrenzungsgruppe (Anzahl der jeder Begrenzungsgruppe zugewiesenen Grenzen und Standortsysteme)  

    - Begrenzungsgruppenbeziehungen und Fallbackkonfiguration

    - Statistiken über Downloads von Clients

    - Anzahl der Grenzen nach Typ  

    - Anzahl von Peercacheclients und Nutzungsstatistiken

    - Informationen zur Verteilungs-Manager-Konfiguration (Threads, Wiederholungsverzögerung, Anzahl der Wiederholungsversuche und Einstellungen für Pullverteilungspunkte)  

    - Informationen zur Verteilungspunktkonfiguration (Verwenden von Branch-Cache und Verteilungspunktüberwachung)

    - Informationen zur Verteilungspunktgruppe (Anzahl der jeder Verteilungspunktgruppe zugewiesenen Pakete und Verteilungspunkte)  



- **Endpoint Protection:**  

   - Advanced Threat Protection-Richtlinien (ATP) (Anzahl der Richtlinien und Angabe, ob Richtlinien bereitgestellt werden)

   - Anzahl der Warnungen, die für das Endpoint Protection-Feature konfiguriert sind  

   - Anzahl der ausgewählten Sammlungen, die im Endpoint Protection-Dashboard angezeigt werden sollen  

   - Fehler bei der Endpoint Protection-Bereitstellung (Anzahl der Endpoint Protection-Richtlinien-Bereitstellungsfehlercodes)  

   - Endpoint Protection-Antischadsoftware und Windows-Firewall-Richtliniennutzung (Anzahl der eindeutigen der Gruppe zugewiesenen Richtlinien)<br /><br /> Dies umfasst keine Informationen über in der Richtlinie enthaltene Einstellungen.  



- **Migration:**

  - Anzahl der migrierten Objekte (Migrations-Assistent verwenden)



- **Verwaltung mobiler Geräte (MDM):**  

    - Anzahl der ausgegebenen Aktionen für mobile Geräte: Befehle „Sperren“, „PIN zurücksetzen“, „Zurücksetzen“, „Außerkraftsetzen“ und „Jetzt synchronisieren“

    - Anzahl der Richtlinien für mobile Geräte  

    - Anzahl der von Configuration Manager und Microsoft Intune verwalteten mobilen Geräte und Art ihrer Registrierung (Massenregistrierung, benutzerbasierte Registrierung)  

    - Anzahl der Benutzer mit mehreren registrierten mobilen Geräten  

    - Zeitplan zu Abrufvorgängen für mobile Geräte und Statistiken zur Eincheckdauer mobiler Geräte  




- **Problembehandlung für Microsoft Intune:**

    - Anzahl und Größe von Geräteaktionen (Zurücksetzen, Außerkraftsetzen, Sperren), Telemetrie und Datenmeldungen, die auf Microsoft Intune repliziert wurden

    - Anzahl und Größe der von Microsoft Intune heruntergeladenen Meldungen zum Zustand, Status und Mandantenzustand, zur Inventur und Konformität und zu RDR, DDR, UDX, POL, LOG, Cert, CRP, Resync, CFD, RDO, BEX und ISM

    - Statistiken zur vollständigen und Deltabenutzersynchronisierung für Microsoft Intune



- **Lokale Verwaltung mobiler Geräte (MDM):**  

    - Anzahl von Windows 10-Massenregistrierungspaketen und -profilen  

    - Statistiken zu erfolgreichen und fehlerhaften lokalen MDM-Anwendungsbereitstellungen  




- **Betriebssystembereitstellung:**  

    - Anzahl der Startimages, Treiber, Treiberpakete, multicastfähigen Verteilungspunkte, PXE-fähigen Verteilungspunkte und Tasksequenzen  

    - Anzahl von Editionsaktualisierungsrichtlinien

    - Anzahl der Tasksequenzschrittnutzung



- **Standortupdates:**

    - Versionen installierter Configuration Manager-Hotfixes



- **Softwareupdates:**  

    - Verfügbare und Stichtagdeltawerte, die in Regeln zur automatischen Bereitstellung verwendet werden  

    - Durchschnittliche und maximale Anzahl von Zuweisungen pro Update  

    - Clientupdateauswertung und Überprüfungszeitpläne  

    - Vom Softwareupdatepunkt synchronisierte Klassifikationen

    - Statistiken zu Clusterpatches  

    - Konfiguration von Windows 10-Express-Updates

    - Konfigurationen, die für aktive Windows 10-Wartungspläne verwendet werden  

    - Anzahl der bereitgestellten Office 365-Updates  

    - Anzahl der Updategruppen und -zuweisungen  

    - Anzahl der Updatepakete und maximale/minimale/durchschnittliche Anzahl der von den Paketen angesprochenen Verteilungspunkte  

    - Anzahl der mit System Center Updates Publisher erstellten und bereitgestellten Updates  

    - Anzahl von Windows 10-Clients, die Windows Update für Unternehmen verwenden  

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



- **SQL-/Leistungsdaten:**  

    - ***[Neu]*** Konfiguration und Dauer der Standortzusammenfassung

    - Anzahl der größten Datenbanktabellen  

    - Operative Ermittlungsstatistik (Anzahl der gefundenen Objekte)

    - Ermittlungstypen, aktiviert und Zeitplan (vollständig, inkrementell)

    - Informationen zu SQL Always On-Replikat, Nutzung und Integritätsstatus

    - Leistungsprobleme der verfolgten SQL-Änderungen, Beibehaltungsdauer und Status der automatischen Bereinigung

    - Beibehaltungsdauer der verfolgten SQL-Änderungen

    - ***[Neu]*** Status und Statusmeldung zu Leistungsstatistiken, einschließlich der häufigsten und kostspieligsten Meldungstypen



- **Verschiedenes**

    - ***[Neu]*** Konfiguration des Data Warehouse-Dienstpunkts, einschließlich Zeitplan und Durchschnittszeit der Synchronisierung

    - Anzahl der Wake-On-LAN-Standorte (WOL)

    - Berichte von Nutzungs- und Leistungsstatistiken  



##  <a name="level-3---full"></a><a name="bkmk_level3"></a> Ebene 3: Vollständig
Die Ebene „Vollständig“ umfasst alle Daten der Ebenen „Basis“ und „Erweitert“. Darüber hinaus werden zusätzliche Informationen zu Endpoint Protection, die Prozentsätze zur Updatekompatibilität sowie Informationen zu Softwareupdates erfasst.  Diese Ebene kann auch erweiterte Diagnoseinformationen wie Systemdateien und Momentaufnahmen des Arbeitsspeichers einschließen. Darin können wiederum personenbezogene Informationen enthalten sein, die zum Zeitpunkt der Erfassung im Arbeitsspeicher oder in Protokolldateien vorhanden waren.

Bei Version 1702 von Configuration Manager umfasst diese Ebene folgende Daten:

- Informationen zum Zeitplan für die Auswertung der automatischen Bereitstellungsregel

- Zusammenfassung zur ATP-Integrität

- Statistiken zur Sammlungsauswertung und -aktualisierung

- Konformitätseinstellungen: Konfigurationsdetails zu SCEP-, VPN-, WLAN- und Konformitätsrichtlinienvorlagen; Anzahl von Gruppen, deren Softwareupdates abgelaufen sind

- DCM-Konfigurationspaket für die Configuration Manager-Nutzung

- Detaillierte Installationsfehler der Client-Bereitstellung
- Zusammenfassung zur Endpoint Protection-Integrität (einschließlich Anzahl der geschützten, gefährdeten, unbekannten und nicht unterstützten Clients)

- Endpoint Protection-Richtlinienkonfiguration

- ***[Neu]*** Liste der Prozesse, die mit dem Installationsverhalten für Anwendungen konfiguriert wurden

- Minimale/maximale/durchschnittliche Anzahl von Stunden seit der letzten Überprüfung auf Softwareupdates

- Minimale/maximale/durchschnittliche Anzahl der inaktiven Clients in Softwareupdate-Bereitstellungssammlungen

- Minimale/maximale/durchschnittliche Anzahl von Softwareupdates pro Paket

- MSI-Produktcode (gängige Apps, die Kunden bereitstellen)

- Gesamtkompatibilität der Softwareupdatebereitstellungen

- Codes und Anzahl der Fehler bei der Softwareupdatebereitstellung

- Informationen zur Softwareupdatebereitstellung (Prozentsatz der Zielbereitstellungen mit Client- bzw. UTC-Zeit, erforderlich bzw. optional bzw. automatisch und Neustartunterdrückung)

- Vom Softwareupdatepunkt synchronisierte Softwareupdateprodukte

- Prozentsätze der erfolgreichen Überprüfungen auf Softwareupdates

- Die besten 50 CPUs in der Umgebung

- Typ der EAS-Richtlinien für den bedingten Zugriff (blockiert oder in Quarantäne) für mit Intune verwaltete Geräte

- Anwendungsdetails zu Windows Store für Unternehmen (nicht-aggregierte Liste synchronisierter Anwendungen, darunter App-ID, Online- oder Offlinestatus und die Gesamtzahl erworbener Lizenzen)
