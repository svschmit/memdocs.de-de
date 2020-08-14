---
title: Diagnosedaten für Version 1511
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über die Ebenen der Diagnose- und Nutzungsdaten, die Configuration Manager-Version 1511 sammelt.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: 9e614ae1-47d2-4a93-ba0a-89dc50d1e266
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 94166557b07050706401c122b835579762bfa982
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128830"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1511-of-configuration-manager"></a>Ebenen der Sammlung von Nutzungsdaten zu Diagnosezwecken für Configuration Manager Version 1511

*Gilt für: Configuration Manager (Current Branch)*

Version 1511 von Configuration Manager sammelt drei Arten von Diagnose- und Nutzungsdaten: **Einfach**, **Erweitert** und **Vollständig**. Standardmäßig ist dieses Feature auf die Ebene „Erweitert“ festgelegt. Die folgenden Abschnitte enthalten zusätzliche Details zu den auf den einzelnen Ebenen gesammelten Daten.  

> [!IMPORTANT]  
>  Configuration Manager sammelt auf den Ebenen „Basis“ und „Erweitert“ keine Standortcodes, Standortnamen, IP-Adressen, Benutzer- oder Computernamen, physischen Adressen oder E-Mail-Adressen. Die auf der Ebene „Vollständig“ erfassten Daten (möglicherweise in erweiterten Diagnoseinformationen wie Protokolldateien oder Arbeitsspeicher-Momentaufnahmen enthaltene Daten) werden nicht zielgerichtet gesammelt. Sie werden von Microsoft auch nicht zu Werbezwecken oder dazu verwendet, Sie zu identifizieren oder sich mit Ihnen in Verbindung zu setzen.  

##  <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> Ändern der Ebene  
 Administratoren mit einem rollenbasierten Verwaltungsbereich, der **Ändern**-Berechtigungen für die **Standort**-Objektklasse umfasst, können in den Einstellungen der Configuration Manager-Konsole unter „Diagnose- und Nutzungsdaten“ die Ebene der erfassten Daten ändern.

 Wechseln Sie dazu in der Konsole zur Registerkarte „Backstage“ (die obere linke Registerkarte mit Dropdownpfeil), und wählen Sie **Nutzungsdaten** und anschließend die Datenebene aus, die Sie verwenden möchten.  


##  <a name="level-1---basic"></a><a name="bkmk_level1"></a> Ebene 1: Basis  
 Die Ebene „Basis“ umfasst Daten über Ihre Hierarchie, Daten, die für die Verbesserung Ihrer Installations- oder Upgradeerfahrung nötig sind, sowie Daten, die zur Ermittlung der für Ihre Hierarchie infrage kommenden Configuration Manager-Updates benötigt werden.  

 Ab Version 1511 von Configuration Manager umfasst diese Ebene folgende Daten:  


-   Setupinformationen
    - Build, Installationstyp, Sprachpakete und Funktionen, die Sie aktiviert haben

    - Bereitstellungsstatus des Updatepakets und Fehler  

-   Metriken zur Datenbankleistung (Informationen zur Replikationsverarbeitung, die wichtigsten gespeicherten SQL Server-Prozeduren nach Prozessor und Datenträgerverwendung)  

-   Grundlegende Informationen zur Datenbankkonfiguration (Prozessoren, Clusterkonfiguration und Konfiguration verteilter Ansichten)  

-   Configuration Manager-Datenbankschema (Hash aller Objektdefinitionen)  

-   Anzahl der Configuration Manager-Client- und -Betriebssystemversionen  

-   Anzahl der Betriebssysteme für verwaltete Geräte und der von Exchange Connector festgelegten Richtlinien  

-   Anzahl der Sprachen und Gebietsschemas der Clients

-   Anzahl von Windows 10-Geräten nach Branch und Build  

-   Grundlegende Daten zur Configuration Manager-Standorthierarchie (Standortliste, Typ, Version, Status, Anzahl von Clients und Zeitzone)  

-   Grundlegende Informationen zum Standortsystemserver (verwendete Standortsystemrollen, Internet- und SSL-Status, Betriebssystem, Prozessoren sowie physischer oder virtueller Computer)  

-   Grundlegende Statistiken zur Benutzerermittlung (Benutzerermittlungsanzahl und minimale/maximale/durchschnittliche Gruppengröße)  

-   Grundlegende Informationen zu Endpoint Protection (Antischadsoftware-Clientversionen)  

-   Anzahl der grundlegenden Anwendungs- und Bereitstellungstypen (Gesamtzahl der Apps, Gesamtzahl der Apps mit mehreren Bereitstellungstypen, Gesamtzahl der Apps mit Abhängigkeiten, Gesamtzahl der ersetzten Apps und Anzahl der verwendeten Bereitstellungstechnologien)  

-   Anzahl der grundlegenden Betriebssystembereitstellungen (OSDs) (Images)  

-   Informationen zu Verteilungspunkt- und Verwaltungspunkttypen sowie zur grundlegenden Konfiguration (geschützt, vorab bereitgestellt, PXE, Multicast, SSL-Status, Pull-/Peerverteilungspunkte, MDM-aktiviert, SSL-fähig usw.)  

-   Telemetriestatistiken (Ausführungszeit, Laufzeit und Fehler)  

##  <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> Ebene 2: Erweitert  
Die Ebene „Erweitert“ ist die Standardeinstellung nach dem Setup. Diese Ebene enthält die auf der Ebene „Basis“ erfassten Daten und featurespezifische Daten (Häufigkeit und Dauer der Verwendung), Configuration Manager-Clienteinstellungen (Name der Komponente, Status und bestimmte Einstellungen wie Abrufintervalle) sowie grundlegende Informationen zu Softwareupdates.  

Diese Ebene wird empfohlen, da sie Microsoft die Daten bereitstellt, die mindestens erforderlich sind, um in künftigen Versionen der Produkte und Dienste nützliche Verbesserungen vorzunehmen. Diese Ebene erfasst keine Objektnamen (Websites, Benutzer, Computer oder Objekte) und keine Details zu sicherheitsrelevanten Objekten oder Sicherheitsrisiken, wie etwa die Anzahl der Systeme, die Softwareupdates erfordern.  

Ab Version 1511 von Configuration Manager umfasst diese Ebene folgende Daten:  

-   **Anwendungsverwaltung:**  

    -   Grundlegende Informationen zu Verwendung/Zielgruppenadressierung für innerhalb der Organisation verwendete Bereitstellungstypen (adressierter Benutzer/adressiertes Gerät und erforderlich/verfügbar)  

    -   Informationen zur Anwendungsbereitstellung (Installieren/Deinstallieren, Genehmigung erforderlich und Benutzerinteraktion aktiviert/deaktiviert)  

    -   Statistiken zur Anforderung verfügbarer Anwendungen  

    -   Anzahl der Pakete nach Typ  

    -   Anzahl der Anwendungsanwendbarkeit nach Betriebssystem  

    -   Anzahl der Paket-/Programmbereitstellungen  

    -   Anzahl von App-V-Umgebungen und Bereitstellungseigenschaften  

    -   Anzahl von Windows 10-lizenzierten Anwendungslizenzen  

    -   Minimale/maximale/durchschnittliche Anzahl von Anwendungsbereitstellungen pro Benutzer/Gerät  

    -   Wartungsfenstertyp und -dauer  

-   **Client:**  

    -   Liste/Anzahl der aktivierten Client-Agents  

    -   Anzahl der Clientinstallationen von jedem Quellspeicherorttyp  

    -   Anzahl der Fehler bei der Clientinstallation  

-   **Kompatibilitätseinstellungen:**  

    -   Anzahl der Konfigurationselemente nach Typ  

    -   Grundlegende Informationen zur Konfigurationsbaseline (Zählerwert, Anzahl von Bereitstellungen und Anzahl der Verweise)  

    -   Anzahl von Bereitstellungen, die auf integrierte Einstellungen verweisen (der Wert der Einstellung wird nicht erfasst)  

    -   Anzahl der für benutzerdefinierte Einstellungen erstellten Regeln und Bereitstellungen  

    -   Anzahl der bereitgestellten Simple Certificate Enrollment-Protokollvorlagen  

-   **Inhalt:**  

    -   Anzahl der Grenzen nach Typ  

    -   Informationen zur Begrenzungsgruppe (Anzahl der jeder Begrenzungsgruppe zugewiesenen Grenzen und Standortsysteme)  

    -   Informationen zur Verteilungspunktgruppe (Anzahl der jeder Verteilungspunktgruppe zugewiesenen Pakete und Verteilungspunkte)  

    -   Informationen zur Verteilungspunktkonfiguration (Verwenden von Branch-Cache und Verteilungspunktüberwachung)  

    -   Informationen zur Verteilungs-Manager-Konfiguration (Threads, Wiederholungsverzögerung, Anzahl der Wiederholungsversuche und Einstellungen für Pullverteilungspunkte)  

-   **Endpoint Protection:**  

    -   Endpoint Protection-Antischadsoftware und Windows-Firewall-Richtliniennutzung (Anzahl der eindeutigen der Gruppe zugewiesenen Richtlinien)<br /><br />Dies umfasst keine Informationen über in der Richtlinie enthaltene Einstellungen.  

    -   Fehler bei der Endpoint Protection-Bereitstellung (Anzahl der Endpoint Protection-Richtlinien-Bereitstellungsfehlercodes)  

    -   Anzahl der ausgewählten Sammlungen, die im Endpoint Protection-Dashboard angezeigt werden sollen  

    -   Anzahl der Warnungen, die für das Endpoint Protection-Feature konfiguriert sind  

-   **Verwaltung mobiler Anwendungen (MAM):**  

    -   Anzahl der MAM-fähigen Office- und Branchenanwendungen und -richtlinien je Betriebssystem  

    -   Anzahl der MAM-Anwendungs-/-richtlinienbereitstellungen  

    -   Anzahl der pro MAM-Einstellung erstellten Regeln  

-   **Verwaltung mobiler Geräte (MDM):**  

    -   Anzahl der ausgegebenen Aktionen für mobile Geräte: Sperr-, PIN-Rücksetzungs-, Zurücksetzungs- und Außerkraftsetzungsbefehle

    -   Anzahl der von Configuration Manager und Microsoft Intune verwalteten mobilen Geräte und Art ihrer Registrierung (Massenregistrierung oder benutzerbasierte Registrierung)  

    -   Zeitplan zu Abrufvorgängen für mobile Geräte und Statistiken zur Eincheckdauer mobiler Geräte  

    -   Anzahl der Richtlinien für mobile Geräte  

    -   Anzahl der Benutzer mit mehreren registrierten mobilen Geräten  

-   **Problembehandlung für Microsoft Intune:**  

    -   Anzahl und Größe der von Microsoft Intune heruntergeladenen Meldungen zum Zustand, Status und Mandantenzustand, zur Inventur und Konformität und zu RDR, DDR, UDX, POL, LOG, Cert, CRP, Resync, CFD, RDO, BEX und ISM  

    -   Anzahl und Größe von Geräteaktionen (Zurücksetzen, Außerkraftsetzen, Sperren), Telemetrie und Datenmeldungen, die auf Microsoft Intune repliziert wurden  

    -   Statistiken zur vollständigen und Deltabenutzersynchronisierung für Microsoft Intune  

-   **Lokale Verwaltung mobiler Geräte (MDM):**  

    -   Statistiken zu erfolgreichen und fehlerhaften lokalen MDM-Anwendungsbereitstellungen  

    -   Anzahl von Windows 10-Massenregistrierungspaketen und -profilen  

-   **Betriebssystembereitstellung:**  

    -   Anzahl der Startimages, Treiber, Treiberpakete, multicastfähigen Verteilungspunkte, PXE-fähigen Verteilungspunkte und Tasksequenzen  

-   **Softwareupdates:**  

    -   Gesamtzahl bzw. durchschnittliche Anzahl von Sammlungen mit Softwareupdatebereitstellungen sowie maximale/durchschnittliche Anzahl der bereitgestellten Updates  

    -   Anzahl der an die Synchronisierung gebundenen Regeln zur automatischen Bereitstellung  

    -   Anzahl der Regeln zur automatischen Bereitstellung, die neue Updates erstellen oder Updates zu einer vorhandenen Gruppe hinzufügen  

    -   Verfügbare und Stichtagdeltawerte, die in Regeln zur automatischen Bereitstellung verwendet werden  

    -   Durchschnittliche und maximale Anzahl von Zuweisungen pro Update  

    -   Anzahl der mit System Center Updates Publisher erstellten und bereitgestellten Updates  

    -   Anzahl der Updategruppen und -zuweisungen  

    -   Anzahl der Updatepakete und maximale/minimale/durchschnittliche Anzahl der von den Paketen angesprochenen Verteilungspunkte  

    -   Anzahl der Updategruppen und minimale/maximale/durchschnittliche Anzahl der Updates pro Gruppe  

    -   Anzahl von Updates und Prozentsatz der bereitgestellten, abgelaufenen, ersetzten und heruntergeladenen Updates sowie der Updates mit EULAs  

    -   Updateüberprüfungs-Fehlercodes und Anzahl der Computer  

    -   Clientupdateauswertung und Überprüfungszeitpläne  

    -   Softwareupdatepunkt-Synchronisierungszeitplan  

    -   Anzahl der Regeln zur automatischen Bereitstellung mit mehreren Bereitstellungen  

    -   Konfigurationen, die für aktive Windows 10-Wartungspläne verwendet werden  

    -   Windows 10-Dashboardinhaltsversionen  

    -   Anzahl von Windows 10-Clients, die Windows Update für Unternehmen verwenden  

    -   Statistiken zu Clusterpatches  

    -   Anzahl der bereitgestellten Office 365-Updates  

-   **SQL-/Leistungsdaten:**  

    -   Anzahl der größten Datenbanktabellen  

    -   Informationen zum SQL Always-On-Replikat  

    -   Anzahl von Sammlungen nach Typ  

##  <a name="level-3---full"></a><a name="bkmk_level3"></a> Ebene 3: Vollständig  
Die Ebene „Vollständig“ umfasst alle Daten der Ebenen „Basis“ und „Erweitert“. Darüber hinaus werden zusätzliche Informationen zu Endpoint Protection, die Prozentsätze zur Updatekompatibilität sowie Informationen zu Softwareupdates erfasst. Diese Ebene kann auch erweiterte Diagnoseinformationen wie Systemdateien und Momentaufnahmen des Arbeitsspeichers einschließen. Darin können wiederum personenbezogene Informationen enthalten sein, die zum Zeitpunkt der Erfassung im Arbeitsspeicher oder in Protokolldateien vorhanden waren.  

Ab Version 1511 von Configuration Manager umfasst diese Ebene folgende Daten:  

-   Statistiken zur Sammlungsauswertung und -aktualisierung  

-   Zusammenfassung zur Endpoint Protection-Integrität (einschließlich Anzahl der geschützten, gefährdeten, unbekannten und nicht unterstützten Clients)  

-   Endpoint Protection-Richtlinienkonfiguration  

-   Informationen zur Softwareupdatebereitstellung (Prozentsatz der Zielbereitstellungen mit Client- bzw. UTC-Zeit, erforderlich bzw. optional bzw. automatisch und Neustartunterdrückung)  

-   Gesamtkompatibilität der Softwareupdatebereitstellungen  

-   Informationen zum Zeitplan für die Auswertung der automatischen Bereitstellungsregel  

-   Anzahl der Clients mit Netzwerkzugriffsschutz-Richtlinien  

-   Codes und Anzahl der Fehler bei der Softwareupdatebereitstellung  

-   Minimale/maximale/durchschnittliche Anzahl der inaktiven Clients in Softwareupdate-Bereitstellungssammlungen  

-   Anzahl der Gruppen mit abgelaufenen Softwareupdates  

-   Minimale/maximale/durchschnittliche Anzahl von Softwareupdates pro Paket  

-   Prozentsätze der erfolgreichen Überprüfungen auf Softwareupdates  

-   Minimale/maximale/durchschnittliche Anzahl von Stunden seit der letzten Überprüfung auf Softwareupdates  
