---
title: 'Intune-Endpunktsicherheit: Einstellungen zur Verringerung der Angriffsfläche | Microsoft-Dokumentation'
description: 'Endpunktsicherheit: Richtlinieneinstellungen zur Verringerung der Angriffsfläche in Microsoft Intune'
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 7f200e5cb5bb4aa0f29cbd3adc0f177bb14e5476
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431695"
---
# <a name="attack-surface-reduction-policy-settings-for-endpoint-security-in-intune"></a>Richtlinieneinstellungen zur Verringerung der Angriffsfläche für die Endpunktsicherheit in Intune

Erfahren Sie, welche Einstellungen Sie im Intune-Knoten „Endpunktsicherheit“ im Rahmen einer [Endpunktsicherheitsrichtlinie](../protect/endpoint-security-policy.md) in Profilen für die Richtlinie zur *Verringerung der Angriffsfläche* konfigurieren können.

Unterstützte Plattformen und Profile:

- **Windows 10 und höher**:
  - Profil: **App- und Browserisolierung**
  - Profil: **Webschutz**
  - Profil: **Anwendungssteuerung**
  - Profil: **Regeln zur Verringerung der Angriffsfläche**
  - Profil: **Gerätesteuerung**
  - Profil: **Exploit-Schutz**

## <a name="app-and-browser-isolation-profile"></a>Profil „App- und Browserisolierung“

### <a name="app-and-browser-isolation"></a>App- und Browserisolierung

- **Application Guard für Microsoft Edge aktivieren (Optionen)**  
  CSP: [AllowWindowsDefenderApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872350)

  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Aktiviert für Microsoft Edge**: Application Guard öffnet nicht genehmigte Websites in einem virtualisierten Hyper-V-Browsercontainer.

  Wenn der Wert *Aktiviert für Microsoft Edge* festgelegt wird, sind die folgenden Einstellungen verfügbar:
  
  - **Verhalten der Zwischenablage**  
    CSP: [ClipboardSettings](https://go.microsoft.com/fwlink/?linkid=872351)

    Hiermit wählen Sie aus, welche Kopier- und Einfügeaktionen zwischen dem lokalen PC und einem virtuellen Application Guard-Browser zulässig sind.
    - **Nicht konfiguriert** (*Standardeinstellung*)
    - **Kopieren und Einfügen zwischen PC und Browser blockieren**
    - **Kopieren und Einfügen nur von Browser zu PC zulassen**
    - **Kopieren und Einfügen nur von PC zu Browser zulassen**
    - **Kopieren und Einfügen zwischen PC und Browser zulassen**

  - **Externen Inhalt von genehmigten Nicht-Unternehmensstandorten blockieren**  
    CSP: [BlockNonEnterpriseContent](https://go.microsoft.com/fwlink/?linkid=872352)

    - **Nicht konfiguriert** (*Standardeinstellung*)
    - **Ja**: Das Laden von Inhalten von nicht genehmigten Websites wird blockiert.

  - **Protokolle für Ereignisse erfassen, die in einer Application Guard-Browsersitzung auftreten**  
    CSP: [AuditApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872418)

    - **Nicht konfiguriert** (*Standardeinstellung*)
    - **Ja**: Hiermit werden Protokolle für Ereignisse erfasst, die in einer virtuellen Application Guard-Browsersitzung auftreten.

  - **Speichern benutzergenerierter Browserdaten zulassen**  
    CSP: [AllowPersistence](https://go.microsoft.com/fwlink/?linkid=872419)

    - **Nicht konfiguriert** (*Standardeinstellung*)
    - **Ja**: Hiermit können während einer virtuellen Application Guard-Browsersitzung erstellte Benutzerdaten gespeichert werden. Kennwörter, Favoriten und Cookies sind Beispiele für solche Benutzerdaten.

  - **Hardwaregrafikbeschleunigung aktivieren**  
    CSP: [AllowVirtualGPU](https://go.microsoft.com/fwlink/?linkid=872420)

    - **Nicht konfiguriert** (*Standardeinstellung*)
    - **Ja**: Hiermit wird in einer virtuellen Application Guard-Browsersitzung ein virtueller Grafikprozessor verwendet, um grafikintensive Websites schneller zu laden.

  - **Benutzern das Herunterladen von Dateien auf den Host gestatten**  
    CSP: [SaveFilesToHost](https://go.microsoft.com/fwlink/?linkid=872421)

    - **Nicht konfiguriert** (*Standardeinstellung*)
    - **Ja**: Hiermit wird Benutzern das Herunterladen von Dateien aus dem virtualisierten Browser in das Hostbetriebssystem gestattet.

- **Application Guard: Drucken auf lokalen Druckern zulassen**  

  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Ja**: Hiermit wird das Drucken auf lokalen Druckern zugelassen.

- **Application Guard: Drucken auf Netzwerkdruckern zulassen**  

  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Ja**: Hiermit wird das Drucken auf Netzwerkdruckern zugelassen.

- **Application Guard: Drucken in PDF zulassen**  

  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Ja**: Hiermit wird das Drucken in PDF zugelassen.

- **Application Guard: Drucken in XPS zulassen**  

  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Ja**: Hiermit wird das Drucken in XPS zugelassen.

- **Richtlinie für Windows-Netzwerkisolation**  
  
  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Ja**: Hiermit können Sie eine Richtlinie für die Windows-Netzwerkisolation konfigurieren.  
  
  Bei Festlegung auf *Konfigurieren* können Sie die folgenden Einstellungen festlegen.

  - **IP-Bereiche**  
    Erweitern Sie die Dropdownliste, wählen Sie **Hinzufügen** aus, und geben Sie eine *untere Adresse* und eine *obere Adresse* an.

  - **Cloudressourcen**  
    Erweitern Sie die Dropdownliste, wählen Sie **Hinzufügen** aus, und geben Sie einen Wert für *IP-Adresse oder FQDN* und einen *Proxy* an.

  - **Netzwerkdomänen**  
   Erweitern Sie die Dropdownliste, wählen Sie **Hinzufügen** aus, und geben Sie *Netzwerkdomänen* an.

  - **Proxyserver**  
    Erweitern Sie die Dropdownliste, wählen Sie **Hinzufügen** aus, und geben Sie *Proxyserver* an.

  - **Interne Proxyserver**  
    Erweitern Sie die Dropdownliste, wählen Sie **Hinzufügen** aus, und geben Sie *Interne Proxyserver* an.

  - **Neutrale Ressourcen**  
    Erweitern Sie die Dropdownliste, wählen Sie **Hinzufügen** aus, und geben Sie *Neutrale Ressourcen* an.

  - **Automatische Erkennung weiterer Unternehmensproxyserver deaktivieren**  
    - **Nicht konfiguriert** (*Standardeinstellung*)
    - **Ja**: Hiermit deaktivieren Sie die automatische Erkennung weiterer Unternehmensproxyserver.

  - **Automatische Erkennung weiterer Unternehmens-IP-Adressbereiche deaktivieren**  
    - **Nicht konfiguriert** (*Standardeinstellung*)
    - **Ja**: Hiermit deaktivieren Sie die automatische Erkennung weiterer Unternehmens-IP-Adressbereiche.

## <a name="web-protection-profile"></a>Profil „Webschutz“

### <a name="web-protection"></a>Webschutz

- **Netzwerkschutz aktivieren**  
  CSP: [EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=872618)

  - **Nicht konfiguriert** (*Standard*): Die Einstellung wird auf den Standardwert von Windows zurückgesetzt, d. h. deaktiviert.
  - **Benutzerdefiniert**
  - **Aktivieren**: Der Netzwerkschutz ist für alle Benutzer im System aktiviert.
  - **Überwachungsmodus**: Benutzer werden nicht für gefährliche Domänen blockiert, stattdessen werden Windows-Ereignisse ausgelöst.

- **SmartScreen für Microsoft Edge anfordern**  
  CSP: [Browser/AllowSmartScreen](https://go.microsoft.com/fwlink/?linkid=2067029)

  - **Ja**: SmartScreen wird verwendet, um Benutzer vor potenziellen betrügerischen Phishing-Versuchen und Schadsoftware zu schützen.
  - **Nicht konfiguriert** (*Standardeinstellung*)

- **Zugriff auf schädliche Websites blockieren**  
  CSP: [Browser/PreventSmartScreenPromptOverride](https://go.microsoft.com/fwlink/?linkid=2067040)  

  - **Ja**: Hiermit wird verhindert, dass Benutzer Warnungen des Microsoft Defender SmartScreen-Filters ignorieren und zu der Website wechseln.
  - **Nicht konfiguriert** (*Standardeinstellung*)

- **Block unverified file download** (Herunterladen nicht überprüfter Dateien blockieren)  
  CSP: [Browser/PreventSmartScreenPromptOverrideForFiles](https://go.microsoft.com/fwlink/?linkid=2067023)  

  - **Ja**: Hiermit wird verhindert, dass Benutzer Warnungen des Microsoft Defender SmartScreen-Filters ignorieren und nicht überprüfte Dateien herunterladen.
  - **Nicht konfiguriert** (*Standardeinstellung*)

## <a name="application-control-profile"></a>Profil „Anwendungssteuerung“

### <a name="microsoft-defender-application-control"></a>Microsoft Defender Application Control

- **AppLocker-Anwendungssteuerung**  
  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Komponenten und Store-Apps erzwingen**
  - **Komponenten und Store-Apps überwachen**
  - **Komponenten, Store-Apps und Smartlocker erzwingen**
  - **Komponenten, Store-Apps und Smartlocker überwachen**

- **Ignorieren von SmartScreen-Warnungen durch die Benutzer blockieren**  
  [PreventOverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

  Diese Einstellung erfordert, dass die Einstellung „Enforce SmartScreen for apps and files“ (SmartScreen für Apps und Dateien erzwingen) aktiviert ist.
  - **Nicht konfiguriert** (*Standard*): Die Einstellung wird auf den Standardwert von Windows zurückgesetzt, d. h. das Überschreiben durch den Benutzer ist zulässig.
  - **Ja**: SmartScreen bietet keine Option, mit der Benutzer die Warnung ignorieren und die App ausführen können. Die Warnung wird angezeigt, der Benutzer kann sie jedoch nicht umgehen.

- **Windows SmartScreen aktivieren**  
  CSP: [SmartScreen/EnableSmartScreenInShell](https://go.microsoft.com/fwlink/?linkid=872784)

  - **Nicht konfiguriert** (*Standard*): Die Einstellung wird auf den Standardwert von Windows zurückgesetzt, d. h. SmartScreen wird aktiviert. Benutzer können diese Einstellung jedoch ändern. Verwenden Sie einen benutzerdefinierten URI, um SmartScreen zu deaktivieren.
  - **Ja**: Die Verwendung von SmartScreen wird für alle Benutzer erzwungen.

## <a name="attack-surface-reduction-rules-profile"></a>Profil „Regeln zur Verringerung der Angriffsfläche“

### <a name="attack-surface-reduction-rules"></a>Regeln zur Verringerung der Angriffsfläche

- **Diebstahl von Anmeldeinformationen aus dem Subsystem für die lokale Sicherheitsautorität (lsass.exe) von Windows blockieren**  
  <!-- Defender ATP security baseline, Device configuration Endpoint protection profile -->
  [Schützen von Geräten vor Exploits](https://go.microsoft.com/fwlink/?linkid=874499)

  Diese Regel zur Verringerung der Angriffsfläche (Attack Surface Reduction, ASR) wird über die folgende GUID gesteuert: 9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2
  - **Nicht konfiguriert** (*Standard*): Die Einstellung wird auf den Standardwert von Windows zurückgesetzt, d. h. deaktiviert.
  - **Benutzerdefiniert**
  - **Aktivieren**: Versuche, Anmeldeinformationen über „lsass.exe“ zu stehlen, werden blockiert.
  - **Überwachungsmodus**: Benutzer werden nicht für gefährliche Domänen blockiert, stattdessen werden Windows-Ereignisse ausgelöst.

- **Adobe Reader am Erstellen von untergeordneten Prozessen hindern**  
  [Reduzieren von Angriffsflächen mit Regeln zur Reduzierung von Angriffsflächen](https://go.microsoft.com/fwlink/?linkid=853979)
  
  Diese ASR-Regel wird über die folgende GUID gesteuert: 7674ba52-37eb-4a4f-a9a1-f0f9a1619a2c
  - **Nicht konfiguriert** *(Standard)* : Die Einstellung wird auf den Standardwert von Windows zurückgesetzt, d. h. die Erstellung von untergeordneten Prozessen wird nicht blockiert.
  - **Benutzerdefiniert**
  - **Aktivieren**: Adobe Reader wird am Erstellen von untergeordneten Prozessen gehindert.
  - **Überwachungsmodus**: Untergeordnete Prozesse werden nicht blockiert, stattdessen werden Windows-Ereignisse ausgelöst.

- **Einschleusung von Code durch Office-Anwendungen in andere Prozesse blockieren**  
  [Schützen von Geräten vor Exploits](https://go.microsoft.com/fwlink/?linkid=872974)

  Diese ASR-Regel wird über die folgende GUID gesteuert: 75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84
  - **Nicht konfiguriert** (*Standard*): Die Einstellung wird auf den Standardwert von Windows zurückgesetzt, d. h. deaktiviert.
  - **Blockieren**: Einschleusungen von Code durch Office-Anwendungen in andere Prozesse werden blockiert.
  - **Überwachungsmodus**: Anstelle von Blockierungen werden Windows-Ereignisse ausgelöst.

- **Erstellung ausführbarer Inhalte durch Office-Anwendungen blockieren**  
  [Schützen von Geräten vor Exploits](https://go.microsoft.com/fwlink/?linkid=872975)

  Diese ASR-Regel wird über die folgende GUID gesteuert: 3B576869-A4EC-4529-8536-B80A7769E899
  - **Nicht konfiguriert** (*Standard*): Die Einstellung wird auf den Standardwert von Windows zurückgesetzt, d. h. deaktiviert.
  - **Blockieren**: Die Erstellung ausführbarer Inhalte durch Office-Anwendungen wird blockiert.
  - **Überwachungsmodus**: Anstelle von Blockierungen werden Windows-Ereignisse ausgelöst.

- **Alle Office-Anwendungen am Erstellen von untergeordneten Prozessen hindern**  
  [Schützen von Geräten vor Exploits](https://go.microsoft.com/fwlink/?linkid=872976)

  Diese ASR-Regel wird über die folgende GUID gesteuert: D4F940AB-401B-4EFC-AADC-AD5F3C50688A
  - **Nicht konfiguriert** (*Standard*): Die Einstellung wird auf den Standardwert von Windows zurückgesetzt, d. h. deaktiviert.
  - **Blockieren**: Die Erstellung untergeordneter Prozesse durch Office-Anwendungen wird blockiert.
  - **Überwachungsmodus**: Anstelle von Blockierungen werden Windows-Ereignisse ausgelöst.

- **Win32-API-Aufrufe über Office-Makros blockieren**  
  [Schützen von Geräten vor Exploits](https://go.microsoft.com/fwlink/?linkid=872977)

  Diese ASR-Regel wird über die folgende GUID gesteuert: 92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B
  - **Nicht konfiguriert** (*Standard*): Die Einstellung wird auf den Standardwert von Windows zurückgesetzt, d. h. deaktiviert.
  - **Blockieren**: Die Verwendung von Win32-API-Aufrufen durch Office-Makros wird blockiert.
  - **Überwachungsmodus**: Anstelle von Blockierungen werden Windows-Ereignisse ausgelöst.

- **Erstellung untergeordneter Prozesse durch Office-Kommunikations-Apps blockieren**  
  [Schützen von Geräten vor Exploits](https://go.microsoft.com/fwlink/?linkid=874499)  

  Diese ASR-Regel wird über die folgende GUID gesteuert: 26190899-1602-49e8-8b27-eb1d0a1ce869.
  - **Nicht konfiguriert** (*Standard*): Die Einstellung wird auf den Standardwert von Windows zurückgesetzt, d. h. die Erstellung von untergeordneten Prozessen wird nicht blockiert.
  - **Benutzerdefiniert**
  - **Aktivieren**:Das Erstellen von untergeordneten Prozessen durch Office-Kommunikationsanwendungen wird blockiert.
  - **Überwachungsmodus**: Untergeordnete Prozesse werden nicht blockiert, stattdessen werden Windows-Ereignisse ausgelöst.

- **Ausführung möglicherweise verschleierter Skripts blockieren (js/vbs/ps)**  
  [Schützen von Geräten vor Exploits](https://go.microsoft.com/fwlink/?linkid=872978)

  Diese ASR-Regel wird über die folgende GUID gesteuert: 5BEB7EFE-FD9A-4556-801D-275E5FFC04CC
  - **Nicht konfiguriert** (*Standard*): Die Einstellung wird auf den Standardwert von Windows zurückgesetzt, d. h. deaktiviert.
  - **Blockieren**: Defender blockiert die Ausführung verborgener Skripts.
  - **Überwachungsmodus**: Anstelle von Blockierungen werden Windows-Ereignisse ausgelöst.

- **Starten heruntergeladener ausführbarer Inhalte durch JavaScript oder VBScript blockieren**  
  [Schützen von Geräten vor Exploits](https://go.microsoft.com/fwlink/?linkid=872979)

   Diese ASR-Regel wird über die folgende GUID gesteuert: D3E037E1-3EB8-44C8-A917-57927947596D
  - **Nicht konfiguriert** (*Standard*): Die Einstellung wird auf den Standardwert von Windows zurückgesetzt, d. h. deaktiviert.
  - **Blockieren**: Defender blockiert das Ausführen von JavaScript- oder VBScript-Dateien, die aus dem Internet heruntergeladen wurden.
  - **Überwachungsmodus**: Anstelle von Blockierungen werden Windows-Ereignisse ausgelöst.

- **Erstellung von Prozessen durch PSExec- und WMI-Befehle blockieren**  
  [Schützen von Geräten vor Exploits](https://go.microsoft.com/fwlink/?linkid=874500)

  Diese ASR-Regel wird über die folgende GUID gesteuert: d1e49aac-8f56-4280-b9ba-993a6d77406c
  - **Nicht konfiguriert** (*Standard*): Die Einstellung wird auf den Standardwert von Windows zurückgesetzt, d. h. deaktiviert.
  - **Blockieren**: Die Prozesserstellung durch PSExec- oder WMI-Befehle wird blockiert.
  - **Überwachungsmodus**: Anstelle von Blockierungen werden Windows-Ereignisse ausgelöst.

- **Nicht vertrauenswürdige und nicht signierte Prozesse, die über USB ausgeführt werden, blockieren**  
  [Schützen von Geräten vor Exploits](https://go.microsoft.com/fwlink/?linkid=874502)

  Diese ASR-Regel wird über die folgende GUID gesteuert: b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4
  - **Nicht konfiguriert** (*Standard*): Die Einstellung wird auf den Standardwert von Windows zurückgesetzt, d. h. deaktiviert.
  - **Blockieren**: Nicht vertrauenswürdige und nicht signierte Prozesse, die über ein USB-Laufwerk ausgeführt werden, werden blockiert.
  - **Überwachungsmodus**: Anstelle von Blockierungen werden Windows-Ereignisse ausgelöst.

- **Ausführung ausführbarer Dateien blockieren, wenn sie kein Kriterium zu Verbreitung, Alter oder vertrauenswürdigen Listen erfüllen**  
  [Schützen von Geräten vor Exploits](https://go.microsoft.com/fwlink/?linkid=874503)

  Diese ASR-Regel wird über die folgende GUID gesteuert: 01443614-cd74-433a-b99e-2ecdc07bfc25e
  - **Nicht konfiguriert** (*Standard*): Die Einstellung wird auf den Standardwert von Windows zurückgesetzt, d. h. deaktiviert.
  - **Blockieren**
  - **Überwachungsmodus**: Anstelle von Blockierungen werden Windows-Ereignisse ausgelöst.

- **Download ausführbarer Inhalte aus E-Mail- und Webmailclients blockieren**  
  [Schützen von Geräten vor Exploits](https://go.microsoft.com/fwlink/?linkid=872980)

  - **Nicht konfiguriert** (*Standard*): Die Einstellung wird auf den Standardwert von Windows zurückgesetzt, d. h. deaktiviert.
  - **Blockieren**: Ausführbare Inhalte, die von E-Mail- oder Webmailclients heruntergeladen wurden, werden blockiert.
  - **Überwachungsmodus**: Anstelle von Blockierungen werden Windows-Ereignisse ausgelöst.

- **Erweiterten Schutz vor Ransomware verwenden**  
   [Schützen von Geräten vor Exploits](https://go.microsoft.com/fwlink/?linkid=874504)

  Diese ASR-Regel wird über die folgende GUID gesteuert: c1db55ab-c21a-4637-bb3f-a12568109d35
  - **Nicht konfiguriert** (*Standard*): Die Einstellung wird auf den Standardwert von Windows zurückgesetzt, d. h. deaktiviert.
  - **Benutzerdefiniert**
  - **Aktivieren**
  - **Überwachungsmodus**: Anstelle von Blockierungen werden Windows-Ereignisse ausgelöst.

- **Ordnerschutz aktivieren**  
  CSP: [EnableControlledFolderAccess](https://go.microsoft.com/fwlink/?linkid=872614)

  - **Nicht konfiguriert** (*Standard*): Diese Einstellung wird auf den Standardwert zurückgesetzt, d. h. Lese- oder Schreibvorgänge werden nicht blockiert.
  - **Aktivieren**: Bei nicht vertrauenswürdigen Apps blockiert Defender Versuche, Dateien in geschützten Ordnern zu ändern oder zu löschen, sowie Versuche, in Datenträgersektoren zu schreiben. Defender ermittelt automatisch, welche Anwendungen vertrauenswürdig sind. Alternativ dazu können Sie eine eigene Liste mit vertrauenswürdigen Anwendungen definieren.
  - **Überwachungsmodus**: Windows-Ereignisse werden ausgelöst, wenn nicht vertrauenswürdige Anwendungen auf kontrollierte Ordner zugreifen, aber keine Blockierungen erzwungen werden.
  - **Datenträgeränderungen blockieren**: Nur Versuche, in Datenträgersektoren zu schreiben, werden blockiert.
  - **Datenträgeränderungen überwachen**: Anstatt Versuche zum Schreiben in Datenträgersektoren zu blockieren, werden Windows-Ereignisse ausgelöst.
  
- **Dateien und Pfade von Regeln zur Verringerung der Angriffsfläche ausschließen**  
  CSP: [AttackSurfaceReductionOnlyExclusions](https://go.microsoft.com/fwlink/?linkid=872981)

  Erweitern Sie die Dropdownliste, und wählen Sie **Hinzufügen** aus, um einen **Pfad** zu einer Datei oder einem Ordner zu definieren, die bzw. der von Ihren Regeln zur Verringerung der Angriffsfläche ausgenommen werden soll.

## <a name="device-control-profile"></a>Profil „Gerätesteuerung“

### <a name="device-control"></a>Gerätesteuerung

- **Hardware device installation by device identifiers** (Installation von Hardwaregeräten anhand der Geräte-ID)  
  [PreventInstallationOfMatchingDeviceIDs](https://go.microsoft.com/fwlink/?linkid=2066794)  
  
  Mit dieser Einstellung können Sie eine Liste von Plug & Play-Hardware-IDs und kompatiblen IDs für Geräte angeben, deren Installation unter Windows verhindert wird. Diese Richtlinieneinstellung hat Vorrang gegenüber jeder anderen Richtlinieneinstellung, die die Installation eines Geräts ermöglicht.  Wenn Sie diese Richtlinieneinstellung auf einem Remotedesktopserver aktivieren, wirkt sich dies auf die Umleitung der angegebenen Geräte von einem Remotedesktopclient an den Remotedesktopserver aus.

  - **Nicht konfiguriert**
  - **Installation von Hardwaregeräten zulassen**: Geräte können installiert und aktualisiert werden, sofern andere Richtlinieneinstellungen dies zulassen.
  - **Installation von Hardwaregeräten blockieren** (*Standardeinstellung*): Windows wird an der Installation gehindert, wenn die zugehörige Hardware-ID oder kompatible ID in der von Ihnen erstellten Liste enthalten ist.

  Wenn diese Option auf *Installation von Hardwaregeräten blockieren* festgelegt wurde, können Sie die folgenden Einstellungen konfigurieren:

  - **Zugehörige Hardwaregeräte entfernen** (Übereinstimmende Hardwaregeräte entfernen)

    Diese Einstellung ist nur verfügbar, wenn die Option *Hardware device installation by device identifiers* (Installation von Hardwaregeräten anhand der Geräte-ID) auf *Block hardware device installation* (Hardwaregeräteinstallation blockieren) festgelegt ist.
    - **Ja**
    - **Nicht konfiguriert**

  - **Hardware device identifiers that are blocked** (Blockierte Bezeichner von Hardwaregeräten)  

    Diese Einstellung ist nur verfügbar, wenn die Option *Hardware device installation by device identifiers* (Installation von Hardwaregeräten anhand der Geräte-ID) auf *Block hardware device installation* (Hardwaregeräteinstallation blockieren) festgelegt ist.

    Klicken Sie auf **Hinzufügen**, und geben Sie die ID des Hardwaregeräts an, das Sie blockieren möchten.

- **Hardware device installation by device identifiers** (Installation von Hardwaregeräten anhand der Setupklassen)  
  CSP: [DeviceInstallation/AllowInstallationOfMatchingDeviceSetupClasses](https://go.microsoft.com/fwlink/?linkid=2067048)  
  
  Mit dieser Richtlinieneinstellung können Sie eine Liste von GUIDs für Gerätesetupklassen angeben, die Gerätetreiber beschreiben, die unter Windows nicht installierbar sind. Diese Richtlinieneinstellung hat Vorrang gegenüber jeder anderen Richtlinieneinstellung, die die Installation eines Geräts ermöglicht. Wenn Sie diese Richtlinieneinstellung auf einem Remotedesktopserver aktivieren, wirkt sich dies auf die Umleitung der angegebenen Geräte von einem Remotedesktopclient an den Remotedesktopserver aus.

  - **Nicht konfiguriert**
  - **Installation von Hardwaregeräten zulassen**: Geräte können von Windows installiert und aktualisiert werden, sofern andere Richtlinieneinstellungen dies zulassen.
  - **Installation von Hardwaregeräten blockieren** (*Standardeinstellung*): Windows wird an der Installation eines Geräts gehindert, dessen GUIDs für Setupklassen in der von Ihnen erstellten Liste enthalten sind.

  Wenn *Installation von Hardwaregeräten blockieren* festgelegt ist, können Sie die Optionen *Übereinstimmende Hardwaregeräte entfernen* und *Hardwaregerätebezeichner, die blockiert werden* konfigurieren.

  - **Zugehörige Hardwaregeräte entfernen** (Übereinstimmende Hardwaregeräte entfernen)

    Diese Einstellung ist nur verfügbar, wenn die Option *Hardware device installation by device identifiers* (Installation von Hardwaregeräten anhand der Geräte-ID) auf *Block hardware device installation* (Hardwaregeräteinstallation blockieren) festgelegt ist.
    - **Ja**
    - **Nicht konfiguriert**

  - **Hardware device identifiers that are blocked** (Blockierte Bezeichner von Hardwaregeräten)

    Diese Einstellung ist nur verfügbar, wenn die Option *Hardware device installation by device identifiers* (Installation von Hardwaregeräten anhand der Geräte-ID) auf *Block hardware device installation* (Hardwaregeräteinstallation blockieren) festgelegt ist.

    Klicken Sie auf **Hinzufügen**, und geben Sie die ID des Hardwaregeräts an, das Sie blockieren möchten.

- **Bei vollständiger Überprüfung Wechseldatenträger überprüfen**  
  CSP: [Defender/AllowFullScanRemovableDriveScanning](https://go.microsoft.com/fwlink/?linkid=2113946)

  - **Nicht konfiguriert** (*Standard*): Die Einstellung wird auf den Standardwert des Clients zurückgesetzt, d. h. Wechseldatenträger werden überprüft. Der Benutzer kann diese Überprüfung jedoch deaktivieren.
  - **Ja**: Bei einer vollständigen Überprüfung werden Wechseldatenträger (z. B. USB-Speichersticks) überprüft.
  
## <a name="exploit-protection-profile"></a>Profil „Exploit-Schutz“

### <a name="exploit-protection"></a>Exploit-Schutz

- **XML hochladen**  
  CSP: [ExploitProtectionSettings](https://go.microsoft.com/fwlink/?linkid=2067035)

  Ermöglicht dem IT-Administrator, eine Konfiguration vorzunehmen, die für alle Geräte in der Organisation die gewünschten Optionen zur Risikominderung für System und Anwendungen abbildet. Die Konfiguration wird in einer XML-Datei vorgenommen. Durch den Exploit-Schutz können Geräte vor Schadsoftware geschützt werden, die Exploits für die Verbreitung und den Befall von Systemen verwendet. Sie können die App „Windows-Sicherheit“ oder PowerShell verwenden, um Lösungen zur Entschärfung (Konfigurationen) zu erstellen. Diese Konfiguration können Sie anschließend als XML-Datei exportieren und für die Computer in Ihrem Netzwerk freigeben, sodass diese über dieselben Einstellungen zur Entschärfung verfügen. Sie können außerdem eine vorhandene XML-Konfigurationsdatei aus EMET in eine XML-Konfigurationsdatei für den Exploit-Schutz konvertieren und importieren.

  Klicken Sie auf **XML-Datei auswählen**, geben Sie die hochgeladene XML-Datei an, und klicken Sie dann auf **Auswählen**.
  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Ja**

- **Blockieren der Bearbeitung der Exploit Guard-Schutzumgebung durch Benutzer**  
  CSP: [DisallowExploitProtectionOverride](https://go.microsoft.com/fwlink/?linkid=2067239)

  - **Nicht konfiguriert** (*Standard*): Lokale Benutzer können Änderungen im Bereich der Exploit-Schutzeinstellungen vornehmen.
  - **Ja**: Benutzer werden daran gehindert, im Microsoft Defender Security Center Änderungen im Bereich der Exploit-Schutzeinstellungen vorzunehmen.

## <a name="next-steps"></a>Nächste Schritte

[Endpunktsicherheitsrichtlinie zur Verringerung der Angriffsfläche](../protect/endpoint-security-asr-policy.md)
