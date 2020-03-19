---
title: 'Schutzeinstellungen für Windows 10-Geräte in Microsoft Intune: Azure | Microsoft-Dokumentation'
description: Verwenden oder konfigurieren Sie Einstellungen zu Endpoint Protection auf Windows 10-Geräten, um Microsoft Defender-Features zu aktivieren, darunter Application Guard, Firewall, SmartScreen, Verschlüsselung und BitLocker, Exploit Guard, Anwendungssteuerung, Security Center und Sicherheit auf lokalen Geräten in Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/13/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 3af7c91b-8292-4c7e-8d25-8834fcf3517a
ms.reviewer: mattsha
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7817a747a01a137fd29ee8aae117cd604da233a5
ms.sourcegitcommit: 4815f07c8c0399c077b71721c6e6b61047c75ae6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/17/2020
ms.locfileid: "79437097"
---
# <a name="windows-10-and-later-settings-to-protect-devices-using-intune"></a>Einstellungen für Windows 10 (und höher), um Geräte zu schützen, die Intune verwenden.

In Microsoft Intune gibt es viele Einstellungen, die dazu dienen, Ihre Geräte zu schützen. In diesem Artikel werden alle Einstellungen erläutert, die Sie auf Geräten mit Windows 10 oder höher aktivieren und konfigurieren können. Diese Einstellungen werden in einem Endpoint Protection-Konfigurationsprofil in Intune erstellt, um die Optionen für Sicherheitsfunktionen festzulegen, einschließlich BitLocker und Microsoft Defender.  

Informationen zum Konfigurieren von Microsoft Defender Antivirus finden Sie unter den [Geräteeinschränkungen für Windows 10](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus).  

## <a name="before-you-begin"></a>Vorbereitung  

[Hinzufügen der Endpoint Protection-Einstellungen in Intune](endpoint-protection-configure.md)  

Weitere Informationen übers CSPs (Konfigurationsdienstanbieter) finden Sie unter [Referenz zu Konfigurationsdienstanbietern](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference).  

## <a name="microsoft-defender-application-guard"></a>Microsoft Defender Application Guard  

Während der Verwendung von Microsoft Edge schützt Microsoft Defender Application Guard Ihre Umgebung vor Websites, die von Ihrer Organisation nicht als vertrauenswürdig definiert wurden. Wenn Benutzer Websites besuchen, die nicht in Ihrer isolierten Netzwerkgrenze aufgelistet sind, werden die Websites in einer virtuellen Hyper-V-Browsersitzung geöffnet. Vertrauenswürdige Websites werden durch eine Netzwerkgrenze definiert, die in der Gerätekonfiguration konfiguriert werden kann.  

Application Guard ist nur für Windows 10-Geräte (64-Bit) verfügbar. Mithilfe dieses Profils wird eine Win32-Komponente zur Aktivierung von Application Guard installiert.  

- **Application Guard**  
  **Standardeinstellung:** Nicht konfiguriert  
   Application Guard-CSP: [Settings/AllowWindowsDefenderApplicationGuard](https://docs.microsoft.com/windows/client-management/mdm/windowsdefenderapplicationguard-csp#allowwindowsdefenderapplicationguard)  

  - **Aktiviert für Edge**: Aktiviert dieses Feature, das nicht vertrauenswürdige Websites in einem virtualisierten Hyper-V-Browsercontainer öffnet.  
  - **Nicht konfiguriert:** Alle Websites (vertrauenswürdige und nicht vertrauenswürdige) können auf dem Gerät geöffnet werden.  

- **Verhalten der Zwischenablage**  
  **Standardeinstellung:** Nicht konfiguriert  
   Application Guard-CSP: [Settings/ClipboardSettings](https://go.microsoft.com/fwlink/?linkid=872351)  

  Legen Sie zulässige Aktionen für das Kopieren und Einfügen zwischen dem lokalen Computer und dem virtuellen Browser von Application Guard fest.  
  - **Nicht konfiguriert**  
  - **Kopieren und Einfügen nur von PC zu Browser zulassen**  
  - **Kopieren und Einfügen nur von Browser zu PC zulassen**  
  - **Kopieren und Einfügen zwischen PC und Browser zulassen**  
  - **Kopieren und Einfügen zwischen PC und Browser blockieren**  

- **Inhalt der Zwischenablage**  
  Diese Einstellung ist nur verfügbar, wenn das *Verhalten der Zwischenablage* auf eine der Einstellungen zum *Zulassen* festgelegt ist.  
  **Standardeinstellung:** Nicht konfiguriert  
  Application Guard-CSP: [Settings/ClipboardFileType](https://docs.microsoft.com/windows/client-management/mdm/windowsdefenderapplicationguard-csp#clipboardfiletype)  

  Hiermit wählen Sie den zulässigen Inhalt der Zwischenablage aus.  
  - **Nicht konfiguriert**  
  - **Text**  
  - **Bilder**  
  - **Text und Bilder**  

- **Externer Inhalt auf Unternehmenswebsites**  
  **Standardeinstellung:** Nicht konfiguriert  
  Application Guard-CSP: [Settings/BlockNonEnterpriseContent](https://go.microsoft.com/fwlink/?linkid=872352)  

  - **Blockieren**: Verhindert, dass Inhalte von nicht genehmigten Websites geladen werden können.  
  - **Nicht konfiguriert**: Websites, bei denen es sich nicht um Unternehmenswebsites handelt, können auf dem Gerät geöffnet werden.  
 
- **Aus virtuellem Browser drucken**  
  **Standardeinstellung:** Nicht konfiguriert  
  Application Guard-CSP: [Settings/PrintingSettings](https://go.microsoft.com/fwlink/?linkid=872354)  

  - **Zulassen:** Mit dieser Einstellung wird das Drucken des ausgewählten Inhalts aus dem virtuellen Browser zugelassen.  
  - **Nicht konfiguriert:** Wenn diese Standardeinstellung festgelegt ist, werden alle Druckfunktionen deaktiviert.  

  Wenn Sie das Drucken *zulassen*, können Sie die folgende Einstellung konfigurieren:
  - **Drucktypen:** Wählen Sie mindestens eine der folgenden Optionen aus:  
    - PDF  
    - XPS  
    - Lokale Drucker
    - Netzwerkdrucker  

- **Protokolle sammeln**  
  **Standardeinstellung:** Nicht konfiguriert  
  Application Guard-CSP: [Audit/AuditApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872418)  

  - **Zulassen**: Protokolle werden für Ereignisse erfasst, die während einer Browsersitzung von Application Guard auftreten.  
  - **Nicht konfiguriert**: Protokolle werden während einer Browsersitzung nicht erfasst.  

- **Benutzergenerierte Browserdaten beibehalten**  
  **Standardeinstellung:** Nicht konfiguriert  
  Application Guard-CSP: [Settings/AllowPersistence](https://go.microsoft.com/fwlink/?linkid=872419)  

  - **Zulassen**: Benutzerdaten (z. B. Kennwörter, Favoriten und Cookies) werden gespeichert, die während einer virtuellen Browsersitzung von Application Guard erstellt werden.  
  - **Nicht konfiguriert**: Vom Benutzer heruntergeladene Dateien und Daten werden gelöscht, wenn das Gerät neu gestartet wird oder ein Benutzer sich abmeldet.  

- **Grafikbeschleunigung**  
 **Standardeinstellung:** Nicht konfiguriert  
  Application Guard-CSP: [Settings/AllowVirtualGPU](https://go.microsoft.com/fwlink/?linkid=872420)  
      
  - **Aktivieren**: Grafisch anspruchsvolle Websites und Videos werden schneller geladen, indem der Zugriff auf einen virtuellen Grafikprozessor gewährt wird.  
  - **Nicht konfiguriert:** Wenn diese Standardeinstellung konfiguriert ist, wird die CPU des Geräts für die Darstellung von Grafiken verwenden. Der virtuelle Grafikprozessor wird dann nicht verwendet.  

- **Dateien auf Hostdateisystem herunterladen**  
  **Standardeinstellung:** Nicht konfiguriert  
  Application Guard-CSP: [Settings/SaveFilesToHost](https://go.microsoft.com/fwlink/?linkid=872421)  

  - **Aktivieren**: Benutzer können Dateien aus dem virtualisierten Browser auf das Hostbetriebssystem herunterladen.  
  - **Nicht konfiguriert**: Die Dateien werden lokal auf dem Gerät gespeichert, und es werden keine Dateien auf das Hostdateisystem heruntergeladen.  

## <a name="microsoft-defender-firewall"></a>Microsoft Defender Firewall  
 
### <a name="global-settings"></a>Globale Einstellungen  

Diese Einstellungen können auf alle Netzwerktypen angewendet werden.  

- **Dateiübertragungsprotokoll**  
  **Standardeinstellung:** Nicht konfiguriert  
   Firewall-CSP: [MdmStore/Global/DisableStatefulFtp](https://go.microsoft.com/fwlink/?linkid=872536)  

  - **Blockieren**: Deaktiviert statusbehaftetes FTP.  
  - **Nicht konfiguriert**: Die Firewall filtert statusbehaftetes FTP, um sekundäre Verbindungen zu ermöglichen.  

- **Leerlaufzeit für Sicherheitszuordnung vor Löschvorgang**  
  **Standardeinstellung:** *Nicht konfiguriert*  
   Firewall-CSP: [MdmStore/Global/SaIdleTime](https://go.microsoft.com/fwlink/?linkid=872539)  

   Mit dieser Einstellung können Sie eine Leerlaufzeit in Sekunden angeben, nach der Sicherheitszuordnungen gelöscht werden.   

- **Codierung vorinstallierter Schlüssel**  
  **Standardeinstellung:** Nicht konfiguriert  
   Firewall-CSP: [MdmStore/Global/PresharedKeyEncoding](https://go.microsoft.com/fwlink/?linkid=872541)  

   - **Aktivieren:** Mit dieser Einstellung werden vorinstallierte Schlüssel mit UTF-8 verschlüsselt.  
   - **Nicht konfiguriert:** Mit dieser Standardeinstellung werden Schlüssel mit dem lokalen Speicherwert verschlüsselt.  

- **IPsec-Ausnahmen**  
  **Standardeinstellung:** *0 ausgewählt*  
   Firewall-CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

   Wählen Sie mindestens einen der folgenden Datenverkehrstypen aus, der von IPsec ausgenommen werden soll:  
   - **Neighbor Discovery-IPv6-Codes vom Typ ICMP**  
   - **ICMP**  
   - **Router Discovery-IPv6-Codes vom Typ ICMP**  
   - **IPv4- und IPv6-DHCP-Netzwerkdatenverkehr**  

- **Überprüfung der Zertifikatssperrliste**  
  **Standardeinstellung:** Nicht konfiguriert  
  Firewall-CSP: [MdmStore/Global/CRLcheck](https://go.microsoft.com/fwlink/?linkid=872548)  

  Wählen Sie aus, wie das Gerät die Zertifikatssperrliste überprüft. Zu den Optionen gehören:  
  - **Überprüfung der Zertifikatssperrliste deaktivieren**  
  - **Überprüfung der Zertifikatssperrliste nur bei gesperrtem Zertifikat fehlerhaft**  
  - **Überprüfung der Zertifikatssperrliste bei jedem Fehler fehlerhaft**  
 

- **Authentifizierungssatz opportunistisch pro Schlüsselerstellungsmodul abgleichen**  
  **Standardeinstellung:** Nicht konfiguriert  
  Firewall-CSP: [MdmStore/Global/OpportunisticallyMatchAuthSetPerKM](https://go.microsoft.com/fwlink/?linkid=872550)  
  
  - **Aktivieren**: Schlüsselerstellungsmodule müssen nur die Authentifizierungssätze ignorieren, die sie nicht unterstützen.  
  - **Nicht konfiguriert**: Schlüsselerstellungsmodule müssen den gesamten Authentifizierungssatz ignorieren, wenn sie nicht alle Authentifizierungssuites unterstützen, die im Satz angegeben sind.  


- **Paketwarteschlangen**  
  **Standardeinstellung:** Nicht konfiguriert  
  Firewall-CSP: [MdmStore/Global/EnablePacketQueue](https://go.microsoft.com/fwlink/?linkid=872551)  

  Legen Sie fest, wie die Skalierung für die Software auf der Empfangsseite für den verschlüsselten Empfang und die Weiterleitung im Klartext für das IPsec-Tunnelgatewayszenario aktiviert wird. Durch diese Einstellung wird die Paketreihenfolge beibehalten. Zu den Optionen gehören:  
  - **Nicht konfiguriert**  
  - **Alle Paketwarteschlangen deaktivieren**  
  - **Nur eingehende verschlüsselte Pakete in Warteschlange einreihen**  
  - **Pakete nach der Entschlüsselung nur zur Weiterleitung in Warteschlange einreihen**  
  - **Eingehende und ausgehende Pakete konfigurieren**  

### <a name="network-settings"></a>Netzwerkeinstellungen  

Die folgenden Einstellungen werden in diesem Artikel nur einmal aufgeführt, gelten aber für die drei spezifischen Netzwerktypen:  
- **Domänennetzwerk (Arbeitsbereichsnetzwerk)**  
- **Privates Netzwerk (sichtbar)**  
- **Öffentliches Netzwerk (nicht sichtbar)**  

#### <a name="general-settings"></a>Allgemeine Einstellungen  

- **Microsoft Defender Firewall**  
  **Standardeinstellung:** Nicht konfiguriert  
  Firewall-CSP: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)  
  
  - **Aktivieren**: Aktivieren Sie die Firewall und die erweiterte Sicherheit. 
  - **Nicht konfiguriert**: Sämtlicher Netzwerkdatenverkehr wird unabhängig von anderen Richtlinieneinstellungen zugelassen.  

- **Geschützter Modus**  
  **Standardeinstellung:** Nicht konfiguriert  
  Firewall-CSP: [DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)  
  - **Nicht konfiguriert**  
  - **Blockieren:** Mit dieser Einstellung wird der geschützte Modus für die Firewall blockiert. Wenn Sie den geschützten Modus blockieren, ermöglichen Sie ebenfalls das Blockieren von **durch IPsec gesicherten Paketausnahmen**.  
  - **Zulassen:** Mit dieser Einstellung wird die Firewall im geschützten Modus betrieben, wodurch Antworten auf Suchanforderungen verhindert werden.  

- **Ausnahme für durch IPsec geschützte Pakete bei geschütztem Modus**  
  **Standardeinstellung:** Nicht konfiguriert  
  Firewall-CSP: [DisableStealthModeIpsecSecuredPacketExemption](https://go.microsoft.com/fwlink/?linkid=872560)  

  Diese Option wird ignoriert, wenn der *Geschützte Modus* auf *Blockieren* festgelegt ist.  

  - **Nicht konfiguriert**  
  - **Blockieren:** Mit dieser Einstellung werden keine Ausnahmen für mit IPsec gesicherte Pakete zugelassen.  
  - **Zulassen:** Mit dieser Einstellung werden Ausnahmen zugelassen. Der geschützte Modus der Firewall DARF NICHT den Hostcomputer daran hindern, auf unerwünschten Netzwerkdatenverkehr zu antworten, der durch IPsec geschützt wird.  

- **Geschützt**  
  **Standardeinstellung:** Nicht konfiguriert  
  Firewall-CSP: [Geschützt](https://go.microsoft.com/fwlink/?linkid=872561)  
    - **Nicht konfiguriert**  
    - **Blockieren:** Wenn die Microsoft Defender-Firewall aktiviert und diese Einstellung auf *Blockieren* festgelegt ist, wird jeglicher eingehende Datenverkehr unabhängig von anderen Richtlinieneinstellungen blockiert. 
    - **Zulassen:** Wenn diese Einstellung auf *Zulassen* festgelegt ist, wird diese Einstellung deaktiviert, wodurch eingehender Datenverkehr anhand anderer Richtlinieneinstellungen zugelassen wird.

- **Unicastantworten auf Multicastbroadcasts**  
  **Standardeinstellung:** Nicht konfiguriert  
  Firewall-CSP: [DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)  
  
  Sie möchten wohl keine Unicastantworten auf Multicast- oder Broadcastmeldungen empfangen. Diese Antworten können auf einen DoS-Angriff (Denial of Service) hinweisen, oder einen Angreifer, der versucht, einen bekannten aktiven Computer zu testen.  
  - **Nicht konfiguriert**  
  - **Block**: Deaktivieren Sie Unicastantworten auf Multicastbroadcasts.  
  - **Zulassen**: Lassen Sie Unicastantworten auf Multicastbroadcasts zu.  

- **Eingehende Benachrichtigungen**  
  **Standardeinstellung:** Nicht konfiguriert  
  Firewall-CSP: [DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=8725630)  

  - **Nicht konfiguriert**  
  - **Blockieren:** Bei dieser Einstellung werden Benachrichtigungen für Benutzer ausgeblendet, wenn eine App daran gehindert wird, an einem Port zu lauschen.  
  - **Zulassen**: Die Einstellung wird aktiviert, und Benutzern werden Benachrichtigungen angezeigt, wenn eine App für das Lauschen auf einen Port blockiert ist.  

- **Standardaktion für ausgehende Verbindungen**  
  **Standardeinstellung:** Nicht konfiguriert  
  Firewall-CSP: [DefaultOutboundAction](https://aka.ms/intune-firewall-outboundaction)  
  
  Hiermit konfigurieren Sie die Standardaktion, die von der Firewall bei ausgehenden Verbindungen durchgeführt wird. Diese Einstellung wird auf Windows-Version 1809 und höher angewendet.  

  - **Nicht konfiguriert**  
  - **Blockieren:** Mit dieser Einstellung wird die Standardaktion der Firewall nicht für ausgehenden Datenverkehr ausgeführt, es sei denn, es ist explizit festgelegt, dass sie nicht blockiert werden soll.  
  - **Zulassen:** Mit dieser Einstellung werden die Standardaktionen der Firewall für ausgehende Verbindungen ausgeführt.  

- **Standardaktion für eingehende Verbindungen**  
  **Standardeinstellung:** Nicht konfiguriert  
  Firewall-CSP: [DefaultInboundAction](https://go.microsoft.com/fwlink/?linkid=872564)  
 
  - **Nicht konfiguriert**  
  - **Blockieren**: Die Standardaktion der Firewall wird für eingehende Verbindungen nicht ausgeführt.  
  - **Zulassen:** Mit dieser Einstellung werden die Standardaktionen der Firewall für eingehende Verbindungen ausgeführt.  

#### <a name="rule-merging"></a>Regelzusammenführung  

- **Microsoft Defender-Firewallregeln für autorisierte Anwendungen aus dem lokalen Speicher**  
  **Standardeinstellung:** Nicht konfiguriert  
  Firewall-CSP: [AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)  

  - **Nicht konfiguriert**  
  - **Blockieren**: Die Firewallregeln für autorisierte Anwendungen im lokalen Speicher werden ignoriert und nicht erzwungen.  
  - **Zulassen:** -
   Wenn Sie diese Einstellung **aktivieren**, werden die Firewallregeln im lokalen Speicher angewendet, sodass sie erkannt und erzwungen werden.  

- **Microsoft Defender Firewall-Regeln für den globalen Port aus dem lokalen Speicher**  
  **Standardeinstellung:** Nicht konfiguriert  
  Firewall-CSP: [GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)  

  - **Nicht konfiguriert**  
  - **Blockieren:** Mit dieser Einstellung werden die Firewallregeln im lokalen Speicher für den globalen Port ignoriert und nicht erzwungen.  
  - **Aktivieren**: Wenden Sie Firewallregeln für den globalen Port auf dem lokalen Speicher an, sodass sie erkannt und erzwungen werden.  

- **Microsoft Defender Firewall-Regeln aus dem lokalen Speicher**  
  **Standardeinstellung:** Nicht konfiguriert  
  Firewall-CSP: [AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)  

  - **Nicht konfiguriert**  
  - **Blockieren:** Mit dieser Einstellung werden Firewallregeln aus dem lokalen Speicher ignoriert und nicht erzwungen.
  - **Aktivieren**: Wenden Sie Firewallregeln auf dem lokalen Speicher an, sodass sie erkannt und erzwungen werden.  

- **IPsec-Regeln aus dem lokalen Speicher**  
  **Standardeinstellung:** Nicht konfiguriert  
  Firewall-CSP: [AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)  

  - **Nicht konfiguriert**  
  - **Blockieren**: Die Verbindungssicherheitsregeln im lokalen Speicher werden unabhängig von der Schemaversion und der Version der Verbindungssicherheitsregeln ignoriert und nicht erzwungen.  
  - **Zulassen**: Wenden Sie Verbindungssicherheitsregeln aus dem lokalen Speicher an, die unabhängig vom Schema oder den Versionen der Verbindungssicherheitsregeln gelten.  

### <a name="firewall-rules"></a>Firewallregeln  

Sie können benutzerdefinierte Firewallregeln **hinzufügen**. Weitere Informationen finden Sie unter [Hinzufügen benutzerdefinierter Firewallregeln für Windows 10-Geräte](endpoint-protection-configure.md#add-custom-firewall-rules-for-windows-10-devices).  

Benutzerdefinierte Firewallregeln unterstützen die folgenden Optionen:  

#### <a name="general-settings"></a>Allgemeine Einstellungen:  

- **Name**  
  **Standardeinstellung:** *Kein Name*  

  Geben Sie einen Anzeigenamen für Ihre Regel an. Dieser Name wird in der Regelliste angezeigt, damit Sie sie einfacher finden können.  

- **Beschreibung**  
  **Standardeinstellung:** *Keine Beschreibung*  

  Geben Sie eine Beschreibung für die Regel an.  

- **Richtung**   
  **Standardeinstellung:** Nicht konfiguriert  
  Firewall-CSP: [FirewallRules/*FirewallRuleName*/Direction](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#direction)  
  
  Legen Sie fest, ob diese Regel für **eingehenden** oder **ausgehenden** Datenverkehr gilt. Wenn **Nicht konfiguriert** festgelegt wird, wird die Regel automatisch auf ausgehenden Datenverkehr angewendet.  

- **Aktion**  
  **Standardeinstellung:** Nicht konfiguriert  
  Firewall-CSP: [FirewallRules/*FirewallRuleName*/Action](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#action) und [FirewallRules/*FirewallRuleName*/Action/Type](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#type)  

  Wählen Sie **Zulassen** oder **Blockieren** aus. Wenn **Nicht konfiguriert** festgelegt wird, lässt die Regen den Datenverkehr standardmäßig zu.  

- **Netzwerktyp**  
  **Standardeinstellung:** 0 ausgewählt  
  Firewall-CSP: [FirewallRules/*FirewallRuleName*/Profiles](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#profiles)  

  Wählen Sie bis zu drei Netzwerktypen aus, für die die Regel gilt. Zu den Optionen gehören **Domäne**, **Privat** und **Öffentlich**.  Wenn keine Netzwerktypen ausgewählt sind, gilt die Regel für alle drei Netzwerktypen.  

#### <a name="application-settings"></a>Anwendungseinstellungen  

- **Anwendung(en)**  
  **Standardeinstellung:** Alle  

  Hiermit können Sie Verbindungen für eine App oder ein Programm steuern. Wählen Sie eine der folgenden Optionen aus, und führen Sie dann die zusätzliche Konfiguration durch:  
  - **Paketfamilienname:** Legen Sie einen Paketfamiliennamen fest. Verwenden Sie den PowerShell-Befehl **Get-AppxPackage**, um den Paketfamiliennamen zu ermitteln.   
    Firewall-CSP: [FirewallRules/*FirewallRuleName*/App/PackageFamilyName](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#packagefamilyname)  
 
  - **Dateipfad:** Sie müssen einen Dateipfad zu einer App auf dem Clientgerät festlegen. Dabei kann es sich um einen absoluten oder einen relativen Pfad handeln. Beispiel:  C:\Windows\System\Notepad.exe oder %WINDIR%\Notepad.exe.  
    Firewall-CSP: [FirewallRules/*FirewallRuleName*/App/FilePath](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#filepath)  

  - **Windows-Dienst:** Legen Sie den Kurznamen des Windows-Diensts fest, wenn es sich um einen Dienst und nicht um eine Anwendung handelt, die Datenverkehr sendet oder empfängt. Verwenden Sie den PowerShell-Befehl **Get-Service**, um den Kurznamen des Diensts zu ermitteln.  
    Firewall-CSP: [FirewallRules/*FirewallRuleName*/App/ServiceName](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#servicename)  

  - **Alle:** *Es ist keine weitere Konfiguration erforderlich*.  

#### <a name="ip-address-settings"></a>Einstellungen für IP-Adressen  

Legen Sie die lokalen und die Remoteadressen fest, für die diese Regel gilt.  

- **Lokale Adressen**    
  **Standardeinstellung:** Beliebige Adresse  
  Firewall-CSP: [FirewallRules/*FirewallRuleName*/LocalPortRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localportranges)  

  Wählen Sie **Beliebige Adresse** oder **Angegebene Adresse** aus.  

  Wenn Sie die Option *Angegebene Adresse* verwenden, fügen Sie mindestens eine Adresse in einer durch Trennzeichen getrennte Liste lokaler Adressen hinzu, die der Regel unterliegen. Die folgenden Tokens sind gültig:  
  - Verwenden Sie ein Sternchenzeichen „*“ für *beliebige* lokale Adressen. Wenn Sie ein Sternchensymbol verwenden, dürfen Sie nur dieses Token verwenden.  
  - Verwenden Sie entweder die Subnetzmaske oder die Netzwerkpräfixnotation, um ein Subnetz anzugeben. Wenn weder eine Subnetzmaske noch ein Netzwerkpräfix angegeben wird, lautet die Subnetzmaske standardmäßig 255.255.255.255.  
  - Eine gültige IPv6-Adresse  
  - Ein IPv4-Adressbereich im Format „Startadresse – Endadresse“ ohne Leerzeichen.  
  - Ein IPv6-Adressbereich im Format „Startadresse – Endadresse“ ohne Leerzeichen.  

- **Remoteadressen**  
  **Standardeinstellung:** Beliebige Adresse  
  Firewall-CSP: [FirewallRules/*FirewallRuleName*/RemoteAddressRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#remoteaddressranges)  
 
  Wählen Sie **Beliebige Adresse** oder **Angegebene Adresse** aus.  

  Wenn Sie die Option *Angegebene Adresse* verwenden, fügen Sie mindestens eine Adresse in einer durch Trennzeichen getrennte Liste von Remoteadressen hinzu, die der Regel unterliegen. Tokens beachten die Groß-/Kleinschreibung nicht. Die folgenden Tokens sind gültig:  
  - Verwenden Sie ein Sternchenzeichen „*“ für *beliebige* Remoteadressen. Wenn Sie ein Sternchensymbol verwenden, dürfen Sie nur dieses Token verwenden.  
  - „Defaultgateway“  
  - „DHCP“  
  - „DNS“  
  - „WINS“  
  - „Intranet“ (wird ab der Windows-Version 1809 unterstützt)  
  - „RmtIntranet“ (wird ab der Windows-Version 1809 unterstützt)  
  - „Internet“ (wird ab der Windows-Version 1809 unterstützt)  
  - „Ply2Renders“ (wird ab der Windows-Version 1809 unterstützt)  
  - „LocalSubnet“ steht für beliebige lokale Adressen im lokalen Subnetz.  
  - Verwenden Sie entweder die Subnetzmaske oder die Netzwerkpräfixnotation, um ein Subnetz anzugeben. Wenn weder eine Subnetzmaske noch ein Netzwerkpräfix angegeben wird, lautet die Subnetzmaske standardmäßig 255.255.255.255.  
  - Eine gültige IPv6-Adresse  
  - Ein IPv4-Adressbereich im Format „Startadresse – Endadresse“ ohne Leerzeichen.  
  - Ein IPv6-Adressbereich im Format „Startadresse – Endadresse“ ohne Leerzeichen.  

#### <a name="port-and-protocol-settings"></a>Port- und Protokolleinstellungen  
Geben Sie die lokalen und die Remoteports an, für die diese Regel gilt.  

- **Protokoll**  
  **Standardeinstellung:** Beliebig  
  Firewall-CSP: [FirewallRules/*FirewallRuleName*/Protocol](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#protocol)  
  Wählen Sie aus den folgenden Optionen aus, und führen Sie die jeweiligen erforderlichen Konfigurationen durch:  
  - **Alle:** Es ist keine weitere Konfiguration erforderlich.  
  - **TCP:** Konfigurieren Sie die lokalen und Remoteports. Beide Optionen unterstützen die Optionen „Alle Ports“ und „Angegebene Ports“. Geben Sie „Angegebene Ports“ mithilfe einer durch Trennzeichen getrennte Liste ein.  
    - **Lokale Ports:** Firewall-CSP: [FirewallRules/*FirewallRuleName*/LocalPortRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localportranges)  
    - **Remoteports:** Firewall-CSP: [FirewallRules/*FirewallRuleName*/RemotePortRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#remoteportranges)  
  - **UDP:** Konfigurieren Sie die lokalen und Remoteports. Beide Optionen unterstützen die Optionen „Alle Ports“ und „Angegebene Ports“. Geben Sie „Angegebene Ports“ mithilfe einer durch Trennzeichen getrennte Liste ein.  
    - **Lokale Ports:** Firewall-CSP: [FirewallRules/*FirewallRuleName*/LocalPortRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localportranges)  
    - **Remoteports:** Firewall-CSP: [FirewallRules/*FirewallRuleName*/RemotePortRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#remoteportranges)  
  - **Benutzerdefiniert:** Legen Sie eine benutzerdefinierte **Protokollnummer** zwischen 0 bis 255 fest.  

#### <a name="advanced-configuration"></a>Erweiterte Konfiguration  
- **Schnittstellentypen**  
  **Standardeinstellung:** 0 ausgewählt  
  Firewall-CSP: [FirewallRules/*FirewallRuleName*/InterfaceTypes](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#interfacetypes)  

  Wählen Sie eine der folgenden Optionen aus:  
  - **Remotezugriff**  
  - **Drahtlos**  
  - **Lokales Netzwerk**  

- **Nur Verbindungen von diesen Benutzern zulassen**  
  **Standardeinstellung:** Alle Benutzer *(Standardeinstellung, wenn keine Liste angegeben wird)*  
  Firewall-CSP: [FirewallRules/*FirewallRuleName*/LocalUserAuthorizationList](https://aka.ms/intunefirewallauthorizedusers)  

  Legen Sie eine Liste autorisierter, lokaler Benutzer für diese Regel fest. Es kann keine Liste autorisierter Benutzer festgelegt werden, wenn diese Regel auf einen Windows-Dienst angewendet wird.  


## <a name="microsoft-defender-smartscreen-settings"></a>Einstellungen für Microsoft Defender SmartScreen  
 
Microsoft Edge muss auf dem Gerät installiert sein.  

- **SmartScreen für Apps und Dateien**  
  **Standardeinstellung:** Nicht konfiguriert  
   SmartScreen-CSP: [SmartScreen/EnableSmartScreenInShell](https://go.microsoft.com/fwlink/?linkid=872784)  

  - **Nicht konfiguriert:** Bei dieser Standardeinstellung wird die Verwendung von SmartScreen deaktiviert.  
  - **Aktivieren**: Aktivieren Sie Windows SmartScreen für die Datei- und App-Ausführung. SmartScreen ist eine cloudbasierte Komponente gegen Phishing- und Schadsoftware.  

- **Ausführung nicht überprüfter Dateien**  
  **Standardeinstellung:** Nicht konfiguriert  
   SmartScreen-CSP: [SmartScreen/PreventOverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

  - **Nicht konfiguriert**: Deaktiviert dieses Feature, sodass Endbenutzer keine Dateien ausführen können, die nicht überprüft wurden.  
  - **Blockieren**: Sperren Sie die Ausführung von Dateien durch den Benutzer, die nicht durch Windows SmartScreen überprüft wurden.  

## <a name="windows-encryption"></a>Windows-Verschlüsselung  
 
### <a name="windows-settings"></a>Windows-Einstellungen  

- **Geräte verschlüsseln**  
  **Standardeinstellung:** Nicht konfiguriert  
  BitLocker-CSP: [RequireDeviceEncryption](https://go.microsoft.com/fwlink/?linkid=872523)  

  - **Anfordern**: Fordern Sie Benutzer dazu auf, die Geräteverschlüsselung zu aktivieren. Je nach Windows-Edition und Systemkonfiguration können Benutzer zu Folgendem aufgefordert werden:  
    - Zur Bestätigung, dass keine Verschlüsselung eines anderen Anbieters aktiviert ist  
    - Zum Deaktivieren der BitLocker-Laufwerksverschlüsselung und zum anschließenden Aktivieren von BitLocker  
  - **Nicht konfiguriert**  
  
  Wenn die Windows-Verschlüsselung eingeschaltet wird, während eine andere Verschlüsselungsmethode aktiv ist, wird das Gerät möglicherweise instabil.  

- **Speicherkarte verschlüsseln (nur Mobilgeräte)**  
  *Diese Einstellung gilt nur für Windows 10 Mobile.*  
  **Standardeinstellung:** Nicht konfiguriert  
  BitLocker-CSP: [RequireStorageCardEncryption](https://go.microsoft.com/fwlink/?linkid=872524)  

  - Legen Sie diese Einstellung auf **Anfordern** fest, um alle vom Gerät verwendeten wechselbaren Speicherkarten zu verschlüsseln.  
  - **Nicht konfiguriert**: Es ist keine Speicherkartenverschlüsselung erforderlich, und der Benutzer wird nicht dazu aufgefordert, diese zu aktivieren.  

### <a name="bitlocker-base-settings"></a>BitLocker-Grundeinstellungen  

Bei den Grundeinstellungen handelt es sich um universelle BitLocker-Einstellungen, die für alle Typen von Datenträgern gelten. Durch diese Einstellungen wird verwaltet, welche Aufgaben für die Laufwerkverschlüsselung oder Konfigurationsoptionen der Benutzer auf allen Typen von Laufwerken ändern kann.  

- **Warnung zu anderer Datenträgerverschlüsselung**  
  **Standardeinstellung:** Nicht konfiguriert  
  BitLocker-CSP: [AllowWarningForOtherDiskEncryption](https://go.microsoft.com/fwlink/?linkid=872525)  

  - **Blockieren**: Deaktivieren Sie die Warnung, die angezeigt wird, wenn ein anderer Dienst zur Datenträgerverschlüsselung auf dem Gerät vorhanden ist.  
  - **Nicht konfiguriert:** Bei dieser Standardeinstellung wird zugelassen, dass die Warnung für andere Datenträgerverschlüsselungen angezeigt wird.  

  > [!TIP]  
  > Diese Einstellung muss auf *Blockieren* festgelegt werden, damit BitLocker automatisch und ohne Meldung auf einem in Azure AD eingebundenen Gerät installiert werden kann, auf dem Windows 1809 oder höher ausgeführt wird. Weitere Informationen finden Sie unter [Aktivieren von BitLocker auf Geräten ohne Meldung](../protect/encrypt-devices.md#silently-enable-bitlocker-on-devices).

  Wenn *Blockieren* festgelegt ist, können Sie die folgende Einstellung konfigurieren:  

  - **Standardbenutzern erlauben, die Verschlüsselung während Azure AD Join zu aktivieren**  
    *Diese Einstellung gilt nur für in Azure Active Directory eingebunden Geräte und hängt von der vorherigen Einstellung `Warning for other disk encryption` ab.*  
    **Standardeinstellung:** Nicht konfiguriert  
    BitLocker-CSP: [AllowStandardUserEncryption](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp#allowstandarduserencryption)

     - **Zulassen:** Standardbenutzer (Nichtadministratoren) können die BitLocker-Verschlüsselung aktivieren, wenn sie angemeldet sind.  
     - **Nicht konfiguriert**: Nur Administratoren können die BitLocker-Verschlüsselung auf dem Gerät aktivieren.  

  > [!TIP]  
  > Diese Einstellung muss auf *Zulassen* festgelegt werden, damit BitLocker automatisch und ohne Meldung auf einem in Azure AD eingebundenen Gerät installiert werden kann, auf dem Windows 1809 oder höher ausgeführt wird. Weitere Informationen finden Sie unter [Aktivieren von BitLocker auf Geräten ohne Meldung](../protect/encrypt-devices.md#silently-enable-bitlocker-on-devices).

- **Verschlüsselungsmethoden konfigurieren**  
  **Standardeinstellung:** Nicht konfiguriert  
  BitLocker-CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  

  - **Aktivieren**: Konfigurieren Sie Verschlüsselungsalgorithmen für Betriebssystem- und Datenlaufwerke sowie für Wechseldatenträger.  
  - **Nicht konfiguriert**: BitLocker verwendet XTS-AES 128-Bit als Standardverschlüsselungsmethode oder die Verschlüsselungsmethode, die von einem Setupskript festgelegt wird.  

  Bei der Einstellung *Aktivieren* können Sie folgende Einstellungen konfigurieren:  

  - **Verschlüsselung für Betriebssystemlaufwerke**  
    **Standardeinstellung:** XTS-AES, 128 Bit  
   
    Wählen Sie die Verschlüsselungsmethode für Betriebssystemlaufwerke aus. Es wird empfohlen, dass Sie den XTS-AES-Algorithmus verwenden.  
    - **AES-CBC, 128 Bit**  
    - **AES-CBC, 256 Bit**  
    - **XTS-AES 128-Bit**  
    - **XTS-AES 256-Bit**  

  - **Verschlüsselung für Festplattenlaufwerke**  
    **Standardeinstellung:** AES-CBC 128 Bit  
   
    Wählen Sie die Verschlüsselungsmethode für Festplattenlaufwerke (integriert) aus. Es wird empfohlen, dass Sie den XTS-AES-Algorithmus verwenden.  
    - **AES-CBC, 128 Bit**  
    - **AES-CBC, 256 Bit**  
    - **XTS-AES 128-Bit**  
    - **XTS-AES 256-Bit**  

  - **Verschlüsselung für Wechseldatenträger**  
    **Standardeinstellung:** AES-CBC 128 Bit  

    Wählen Sie die Verschlüsselungsmethode für Wechseldatenträger aus. Wenn der Wechseldatenträger mit Geräten verwendet wird, auf denen nicht Windows 10 ausgeführt wird, wird empfohlen, den AES-CBC-Algorithmus zu verwenden.  
    - **AES-CBC, 128 Bit**  
    - **AES-CBC, 256 Bit**  
    - **XTS-AES 128-Bit**  
    - **XTS-AES 256-Bit**  

### <a name="bitlocker-os-drive-settings"></a>Einstellung für BitLocker-OS-Datenträger  

Diese Einstellungen gelten speziell für Betriebssystemlaufwerke.  

- **Zusätzliche Authentifizierung beim Start**  
  **Standardeinstellung:** Nicht konfiguriert  
  BitLocker-CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)  

  - **Anfordern**: Konfigurieren Sie die Authentifizierungsanforderungen für den Computerstart, einschließlich der Verwendung von Trusted Platform Module (TPM).  
  - **Nicht konfiguriert:** Bei dieser Standardeinstellung werden nur grundlegende Optionen auf Geräten mit einem TPM konfiguriert.  

  Bei der Einstellung *Anfordern* können Sie folgende Einstellungen konfigurieren:  

  - **BitLocker mit nicht kompatiblem TPM-Chip**  
    **Standardeinstellung:** Nicht konfiguriert  

    - **Blockieren**: Deaktivieren Sie die Verwendung von BitLocker, wenn ein Gerät nicht über einen kompatiblen TPM-Chip verfügt.  
    - **Nicht konfiguriert**: Benutzer können BitLocker ohne einen kompatiblen TPM-Chip verwenden. BitLocker kann ein Kennwort oder einen Systemstartschlüssel erfordern.  

  - **Systemstart für kompatibles TPM**  
    **Standardeinstellung:** TPM zulassen  

    Hiermit wird konfiguriert, ob das TPM zulässig, erforderlich oder unzulässig ist.  

    - **TPM zulassen**  
    - **TPM nicht zulassen**  
    - **TPM erforderlich**  

  - **Systemstart-PIN für kompatibles TPM**  
    **Standardeinstellung:** Systemstart-PIN mit TPM zulassen  

    Legen Sie fest, ob mit dem TPM-Chip eine Systemstart-PIN zugelassen, nicht zugelassen oder erforderlich ist. Für das Aktivieren einer Systemstart-PIN ist ein Eingreifen des Endbenutzers erforderlich.  

    - **Systemstart-PIN mit TPM zulassen**  
    - **Systemstart-PIN mit TPM nicht zulassen**  
    - **Systemstart-PIN mit TPM erforderlich**

    > [!TIP]
    > Diese Einstellung darf nicht auf *Systemstart-PIN mit TPM erforderlich* festgelegt werden, damit BitLocker automatisch und ohne Meldung auf einem in Azure AD eingebundenen Gerät installiert werden kann, auf dem Windows 1809 oder höher ausgeführt wird. Weitere Informationen finden Sie unter [Aktivieren von BitLocker auf Geräten ohne Meldung](../protect/encrypt-devices.md#silently-enable-bitlocker-on-devices).

  - **Systemstartschlüssel für kompatibles TPM**  
    **Standardeinstellung:** Systemstartschlüssel mit TPM zulassen  

    Legen Sie fest, ob die Verwendung eines Systemstartschlüssels mit dem TPM-Chip zugelassen, nicht zugelassen oder erforderlich ist. Für das Aktivieren eines Systemstartschlüssels ist ein Eingreifen des Endbenutzers erforderlich.  

    - **Systemstartschlüssel mit TPM zulassen**  
    - **Systemstartschlüssel mit TPM nicht zulassen**  
    - **Systemstartschlüssel mit TPM erforderlich**  

    > [!TIP]
    > Diese Einstellung darf nicht auf *Systemstartschlüssel mit TPM erforderlich* festgelegt werden, damit BitLocker automatisch und ohne Meldung auf einem in Azure AD eingebundenen Gerät installiert werden kann, auf dem Windows 1809 oder höher ausgeführt wird. Weitere Informationen finden Sie unter [Aktivieren von BitLocker auf Geräten ohne Meldung](../protect/encrypt-devices.md#silently-enable-bitlocker-on-devices).

  - **Systemstartschlüssel und -PIN für kompatibles TPM**  
    **Standardeinstellung:** Systemstartschlüssel und -PIN mit TPM zulassen  

    Legen Sie fest, ob die Verwendung eines Systemstartschlüssels und einer PIN mit dem TPM-Chip zugelassen, nicht zugelassen oder erforderlich ist. Für das Aktivieren eines Systemstartschlüssels und einer Systemstart-PIN ist ein Eingreifen des Endbenutzers erforderlich.  
    - **Systemstartschlüssel und -PIN mit TPM zulassen**  
    - **Systemstartschlüssel und -PIN mit TPM nicht zulassen**  
    - **Systemstartschlüssel und -PIN mit TPM erforderlich**   

    > [!TIP]  
    > Diese Einstellung darf nicht auf *Systemstartschlüssel und -PIN mit TPM erforderlich* festgelegt werden, damit BitLocker automatisch und ohne Meldung auf einem in Azure AD eingebundenen Gerät installiert werden kann, auf dem Windows 1809 oder höher ausgeführt wird. Weitere Informationen finden Sie unter [Aktivieren von BitLocker auf Geräten ohne Meldung](../protect/encrypt-devices.md#silently-enable-bitlocker-on-devices).

- **PIN-Mindestlänge**  
    **Standardeinstellung:** Nicht konfiguriert  
    BitLocker-CSP: [SystemDrivesMinimumPINLength](https://go.microsoft.com/fwlink/?linkid=872528)   

    - **Aktivieren:** Konfigurieren Sie mit dieser Einstellung eine Mindestlänge für die TPM-Systemstart-PIN.  
    - **Nicht konfiguriert**: Benutzer können eine Systemstart-PIN zwischen 6 und 20 Ziffern konfigurieren.  

  Wenn *Aktivieren* festgelegt ist, können Sie die folgende Einstellung konfigurieren:  

  - **Mindestanzahl von Zeichen**  
    **Standardeinstellung:** *Nicht konfiguriert* BitLocker-CSP: [SystemDrivesMinimumPINLength](https://go.microsoft.com/fwlink/?linkid=872528)  

    Geben Sie die Zahl an Zeichen (**4**-**20**) an, die für die Systemstart-PIN erforderlich sind.  

- **Wiederherstellung von Betriebssystemlaufwerken**  
  **Standardeinstellung:** Nicht konfiguriert   
  BitLocker-CSP: [SystemDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872529)  

  - **Aktivieren**: Sie können festlegen, wie durch BitLocker geschützte Betriebssystemdatenträger wiederhergestellt werden, wenn die erforderlichen Systemstartinformationen nicht verfügbar sind.  
  - **Nicht konfiguriert**: Die Standardwiederherstellungsoptionen werden für die BitLocker-Wiederherstellung unterstützt. Standardmäßig ist DRA zulässig, die Wiederherstellungsoptionen (einschließlich Wiederherstellungskennwort und -schlüssel) werden vom Benutzer angegeben, und Wiederherstellungsinformationen werden nicht in AD DS gesichert.  

  Bei der Einstellung *Aktivieren* können Sie folgende Einstellungen konfigurieren:  

  - **Zertifikatbasierter Datenwiederherstellungs-Agent**  
    **Standardeinstellung:** Nicht konfiguriert  
     
    - **Blockieren:** Mit dieser Einstellung können Sie die Verwendung des Datenwiederherstellungs-Agents für mit BitLocker geschützte Betriebssystemlaufwerke verhindern.  
    - **Nicht konfiguriert:** Mit dieser Standardeinstellung wird die Verwendung von Datenwiederherstellungs-Agents für mit BitLocker geschützte Betriebssystemlaufwerke zugelassen.  

  - **Erstellung des Wiederherstellungskennworts durch den Benutzer**  
    **Standardeinstellung:** 48-stelliges Wiederherstellungskennwort zulassen  

    Legen Sie fest, ob Benutzer ein 48-stelliges Wiederherstellungskennwort generieren dürfen oder müssen.  
    - **48-stelliges Wiederherstellungskennwort zulassen**  
    - **48-stelliges Wiederherstellungskennwort nicht zulassen**  
    - **48-stelliges Wiederherstellungskennwort erforderlich**  

  - **Erstellung des Wiederherstellungsschlüssels durch den Benutzer**  
    **Standardeinstellung:** 256-Bit-Wiederherstellungsschlüssel zulassen  

    Legen Sie fest, ob Benutzer einen 256-Bit-Wiederherstellungsschlüssel generieren dürfen oder müssen.  
    - **256-Bit-Wiederherstellungsschlüssel zulassen**  
    - **256-Bit-Wiederherstellungsschlüssel nicht zulassen**  
    - **256-Bit-Wiederherstellungsschlüssel erforderlich**  

  - **Wiederherstellungsoptionen im BitLocker-Setup-Assistenten**  
    **Standardeinstellung:** Nicht konfiguriert  

    - **Blockieren**: Benutzer können Wiederherstellungsoptionen nicht anzeigen oder ändern. (Diese Option müssen Sie selbst festlegen.) 
    - **Nicht konfiguriert**: Benutzer können die Wiederherstellungsoptionen anzeigen und ändern, wenn sie BitLocker aktivieren. 
 
  - **BitLocker-Wiederherstellungsinformationen in Azure Active Directory speichern**  
    **Standardeinstellung:** Nicht konfiguriert  

    - **Aktivieren**: Speichern Sie die BitLocker-Wiederherstellungsinformationen in Azure Active Directory (AAD).  
    - **Nicht konfiguriert:** Wenn diese Standardeinstellung festgelegt ist, werden die BitLocker-Wiederherstellungsinformationen nicht in AAD gespeichert.  

  - **BitLocker-Wiederherstellungsinformationen in Azure Active Directory gespeichert**  
    **Standardeinstellung:** Wiederherstellungskennwörter und Schlüsselpakete sichern  

    Konfigurieren Sie, welche BitLocker-Wiederherstellungsinformationen in Azure AD gespeichert werden. Es stehen die folgenden Optionen zur Auswahl:  
    - **Wiederherstellungskennwörter und Schlüsselpakete sichern**  
    - **Nur Wiederherstellungskennwörter sichern**  

  - **Rotation von clientgesteuerten Wiederherstellungskennwörtern**  
    **Standardeinstellung:** Schlüsselrotation für Azure AD-eingebundene Geräte aktiviert  
    BitLocker-CSP: [ConfigureRecoveryPasswordRotation](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp)  
    
    Mit dieser Einstellung wird nach der Wiederherstellung eines Betriebssystemlaufwerks eine vom Client gesteuerte Rotation des Wiederherstellungskennworts gestartet (über bootmgr oder WinRE).  

    - Nicht konfiguriert  
    - Schlüsselrotation deaktiviert  
    - Schlüsselrotation für Azure AD-eingebundene Geräte aktiviert  
    - Schlüsselrotation für Azure AD- und hybrid eingebundene Geräte aktiviert  

  - **Vor dem Aktivieren von BitLocker Wiederherstellungsinformationen in Azure Active Directory speichern**  
    **Standardeinstellung:** Nicht konfiguriert  
 
     Hiermit können Sie Benutzer daran hindern, BitLocker zu aktivieren, es sei denn, der Computer sichert die BitLocker-Wiederherstellungsinformationen erfolgreich in Azure Active Directory.  

    - **Anfordern**: Verhindern Sie, dass Benutzer BitLocker aktivieren, es sei denn, die BitLocker-Wiederherstellungsinformationen wurden erfolgreich in Azure AD gespeichert.  
    - **Nicht konfiguriert**: Benutzer können BitLocker aktivieren, auch wenn die Wiederherstellungsinformationen nicht erfolgreich in Azure AD gespeichert wurden.  

- **Pre-Boot-Wiederherstellungsmeldung und -URL**  
  **Standardeinstellung:** Nicht konfiguriert  
  BitLocker-CSP: [SystemDrivesRecoveryMessage](https://go.microsoft.com/fwlink/?linkid=872530)  

  - **Aktivieren:** Mit dieser Einstellung können Sie die Meldung und URL konfigurieren, die auf dem Bildschirm für die Pre-Boot-Schlüsselwiederherstellung angezeigt werden.  
  - **Nicht konfiguriert**: Deaktivieren Sie dieses Feature.  
  
  Wenn *Aktivieren* festgelegt ist, können Sie die folgende Einstellung konfigurieren:  
  - **Pre-Boot-Wiederherstellungsmeldung**  
    **Standardeinstellung:** Standardmäßige Wiederherstellungsmeldung und -URL verwenden   
 
    Legen Sie fest, wie die Pre-Boot-Wiederherstellungsmeldung Benutzern angezeigt wird. Es stehen die folgenden Optionen zur Auswahl:  
    - **Standardmäßige Wiederherstellungsmeldung und -URL verwenden**  
    - **Leere Wiederherstellungsmeldung und -URL verwenden**  
    - **Benutzerdefinierte Wiederherstellungsmeldung**  
    - **Benutzerdefinierte Wiederherstellungs-URL**  

### <a name="bitlocker-fixed-data-drive-settings"></a>Einstellungen für das BitLocker-Festplattenlaufwerk  

Diese Einstellungen gelten speziell für Festplattenlaufwerke.  

- **Schreibzugriff auf nicht durch BitLocker geschützte Festplattenlaufwerke**  
  **Standardeinstellung:** Nicht konfiguriert  
  BitLocker-CSP: [FixedDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872534)  

  - **Blockieren**: Gewähren Sie nur Lesezugriff auf nicht durch BitLocker geschützte Datenträger.  
  - **Nicht konfiguriert:** Wenn diese Standardeinstellung festgelegt ist, wird der Lese- und Schreibzugriff auf Datenträger gewährt, die nicht verschlüsselt sind.  

- **Wiederherstellung von Festplattenlaufwerken**  
  **Standardeinstellung:** Nicht konfiguriert  
  BitLocker-CSP: [FixedDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872538)  

  - **Aktivieren**: Steuern Sie, wie durch BitLocker geschützte Festplattenlaufwerke wiederhergestellt werden, wenn die erforderlichen Systemstartinformationen nicht vorliegen.  
  - **Nicht konfiguriert**: Deaktivieren Sie dieses Feature.  

  Bei der Einstellung *Aktivieren* können Sie folgende Einstellungen konfigurieren:  

  - **Datenwiederherstellungs-Agent**  
    **Standardeinstellung:** Nicht konfiguriert  
 
    - **Blockieren**: Blockieren Sie die Verwendung des Datenwiederherstellungs-Agents mit dem Richtlinien-Editor für durch BitLocker geschützte Festplattenlaufwerke. 
    - **Nicht konfiguriert**: Ermöglicht die Verwendung von Datenwiederherstellungs-Agents auf durch BitLocker geschützten Festplattenlaufwerken.  

  - **Erstellung des Wiederherstellungskennworts durch den Benutzer**  
    **Standardeinstellung:** 48-stelliges Wiederherstellungskennwort zulassen  

    Legen Sie fest, ob Benutzer ein 48-stelliges Wiederherstellungskennwort generieren dürfen oder müssen.  
    - **48-stelliges Wiederherstellungskennwort zulassen**  
    - **48-stelliges Wiederherstellungskennwort nicht zulassen**  
    - **48-stelliges Wiederherstellungskennwort erforderlich**  

  - **Erstellung des Wiederherstellungsschlüssels durch den Benutzer**  
    **Standardeinstellung:** 256-Bit-Wiederherstellungsschlüssel zulassen

    Legen Sie fest, ob Benutzer einen 256-Bit-Wiederherstellungsschlüssel generieren dürfen oder müssen.
    - **256-Bit-Wiederherstellungsschlüssel zulassen**  
    - **256-Bit-Wiederherstellungsschlüssel nicht zulassen**  
    - **256-Bit-Wiederherstellungsschlüssel erforderlich**  

  - **Wiederherstellungsoptionen im BitLocker-Setup-Assistenten**  
    **Standardeinstellung:** Nicht konfiguriert  

    - **Blockieren**: Benutzer können Wiederherstellungsoptionen nicht anzeigen oder ändern. (Diese Option müssen Sie selbst festlegen.) 
    - **Nicht konfiguriert**: Benutzer können die Wiederherstellungsoptionen anzeigen und ändern, wenn sie BitLocker aktivieren.
 
  - **BitLocker-Wiederherstellungsinformationen in Azure Active Directory speichern**  
    **Standardeinstellung:** Nicht konfiguriert  

    - **Aktivieren**: Speichern Sie die BitLocker-Wiederherstellungsinformationen in Azure Active Directory (AAD).  
    - **Nicht konfiguriert:** Wenn diese Standardeinstellung festgelegt ist, werden die BitLocker-Wiederherstellungsinformationen nicht in AAD gespeichert.

  - **BitLocker-Wiederherstellungsinformationen in Azure Active Directory gespeichert**  
    **Standardeinstellung:** Wiederherstellungskennwörter und Schlüsselpakete sichern  

    Konfigurieren Sie, welche BitLocker-Wiederherstellungsinformationen in Azure AD gespeichert werden. Es stehen die folgenden Optionen zur Auswahl:  
    - **Wiederherstellungskennwörter und Schlüsselpakete sichern**  
    - **Nur Wiederherstellungskennwörter sichern**  

  - **Rotation von clientgesteuerten Wiederherstellungskennwörtern**  
    **Standardeinstellung:** Schlüsselrotation für Azure AD-eingebundene Geräte aktiviert  
    BitLocker-CSP: [ConfigureRecoveryPasswordRotation](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp)  
    
    Mit dieser Einstellung wird nach der Wiederherstellung eines Betriebssystemlaufwerks eine vom Client gesteuerte Rotation des Wiederherstellungskennworts gestartet (über bootmgr oder WinRE).  

    - Nicht konfiguriert  
    - Schlüsselrotation deaktiviert  
    - Schlüsselrotation für Azure AD-eingebundene Geräte aktiviert  
    - Schlüsselrotation für Azure AD- und hybrid eingebundene Geräte aktiviert  

  - **Vor dem Aktivieren von BitLocker Wiederherstellungsinformationen in Azure Active Directory speichern**  
    **Standardeinstellung:** Nicht konfiguriert  
 
    Hiermit können Sie Benutzer daran hindern, BitLocker zu aktivieren, es sei denn, der Computer sichert die BitLocker-Wiederherstellungsinformationen erfolgreich in Azure Active Directory.  

    - **Anfordern**: Verhindern Sie, dass Benutzer BitLocker aktivieren, es sei denn, die BitLocker-Wiederherstellungsinformationen wurden erfolgreich in Azure AD gespeichert.  
    - **Nicht konfiguriert**: Benutzer können BitLocker aktivieren, auch wenn die Wiederherstellungsinformationen nicht erfolgreich in Azure AD gespeichert wurden.  

### <a name="bitlocker-removable-data-drive-settings"></a>Einstellungen für den BitLocker-Wechseldatenträger  

Diese Einstellungen gelten speziell für Wechseldatenträger.  

- **Schreibzugriff auf nicht durch BitLocker geschützte Wechseldatenträger**  
  **Standardeinstellung:** Nicht konfiguriert  
  BitLocker-CSP: [RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)  

  - **Blockieren**: Gewähren Sie nur Lesezugriff auf nicht durch BitLocker geschützte Datenträger.  
  - **Nicht konfiguriert:** Wenn diese Standardeinstellung festgelegt ist, wird der Lese- und Schreibzugriff auf Datenträger gewährt, die nicht verschlüsselt sind.  

  Wenn *Aktivieren* festgelegt ist, können Sie die folgende Einstellung konfigurieren:  

  - **Schreibzugriff auf in einer anderen Organisation konfigurierte Geräte**  
    **Standardeinstellung:** Nicht konfiguriert  

    - **Blockieren**: Blockieren Sie den Schreibzugriff auf in einer anderen Organisation konfigurierte Geräte.  
    - **Nicht konfiguriert:** Bei dieser Standardeinstellung wird der Schreibzugriff verweigert.  
 
## <a name="microsoft-defender-exploit-guard"></a>Microsoft Defender Exploit Guard  

Verwenden Sie den [Exploit-Schutz](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/exploit-protection), um die Angriffsfläche von Apps zu verwalten und zu reduzieren, die von Ihren Angestellten verwendet werden.  

### <a name="attack-surface-reduction"></a>Verringerung der Angriffsfläche  

Die Regeln zur Verringerung der Angriffsfläche schützen vor Verhalten, das oft von Schadsoftware zum Infizieren von Computern mit böswilligem Code verwendet wird.  

#### <a name="attack-surface-reduction-rules"></a>Regeln zur Verringerung der Angriffsfläche  

- **Abgreifen von Anmeldeinformationen über das Subsystem der lokalen Sicherheitsautorität von Windows kennzeichnen**  
  **Standardeinstellung:** Nicht konfiguriert  
  Regel: [Diebstahl von Anmeldeinformationen aus dem Subsystem für die lokale Sicherheitsautorität (lsass.exe) von Windows blockieren](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-credential-stealing-from-the-windows-local-security-authority-subsystem-lsassexe)

  Wehren Sie Aktionen und Apps ab, die üblicherweise von Schadsoftware verwendet wird, die nach Sicherheitsproblemen sucht, um Computer zu infizieren.  

  - **Nicht konfiguriert**  
  - **Aktivieren**: Kennzeichnen Sie das Abgreifen von Anmeldeinformationen über das Subsystem zur lokalen Sicherheitsautorität von Windows (lsass.exe).  
  - **Nur überwachen**  

- **Prozesserstellung über Adobe Reader (Beta)**  
  **Standardeinstellung:** Nicht konfiguriert  
  Regel: [Adobe Reader am Erstellen von untergeordneten Prozessen hindern](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-adobe-reader-from-creating-child-processes)  

  - **Nicht konfiguriert**  
  - **Aktivieren:** Mit dieser Einstellung werden untergeordnete Prozesse blockiert, die von Adobe Reader erstellt werden.  
  - **Nur überwachen**  

#### <a name="rules-to-prevent-office-macro-threats"></a>Regeln zum Verhindern von Bedrohungen durch Office-Makros  

Blockieren Sie folgende Aktionen, die Office-Apps durchführen können:  

- **Einschleusung von Code durch Office-Apps in andere Prozesse (keine Ausnahmen)**  
  **Standardeinstellung:** Nicht konfiguriert  
  Regel: [Einschleusung von Code durch Office-Anwendungen in andere Prozesse blockieren](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-office-applications-from-injecting-code-into-other-processes)  

  - **Nicht konfiguriert**  
  - **Blockieren:** Mit dieser Einstellung wird die Einschleusung von Code durch Office-Apps in andere Prozesse blockiert.  
  - **Nur überwachen**  

- **Erstellung ausführbarer Inhalte in Office-Apps und -Makros**  
  **Standardeinstellung:** Nicht konfiguriert  
  Regel: [Erstellung ausführbarer Inhalte durch Office-Anwendungen blockieren](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-office-applications-from-creating-executable-content)  

  - **Nicht konfiguriert**  
  - **Blockieren:** Mit dieser Einstellung wird die Erstellung ausführbarer Inhalte in Office-Apps und -Makros blockiert.  
  - **Nur überwachen**  

- **Starten untergeordneter Prozesse in Office-Apps**  
  **Standardeinstellung:** Nicht konfiguriert  
  Regel: [Alle Office-Anwendungen am Erstellen von untergeordneten Prozessen hindern](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-all-office-applications-from-creating-child-processes)  

  - **Nicht konfiguriert**  
  - **Blockieren:** Mit dieser Einstellung werden Office-Apps am Starten von untergeordneten Prozessen gehindert.  
  - **Nur überwachen**  
  
- **Win32-Importe aus Office-Makrocode**  
  **Standardeinstellung:** Nicht konfiguriert  
  Regel: [Win32-API-Aufrufe über Office-Makros blockieren](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-win32-api-calls-from-office-macros)  

  - **Nicht konfiguriert**  
  - **Blockieren:** Mit dieser Einstellung blockieren Sie Win32-Importe aus Makrocode in Office.  
  - **Nur überwachen**  
  
- **Prozesserstellung über Office-Kommunikationsprodukte**  
  **Standardeinstellung:** Nicht konfiguriert  
  Regel: [Office-Kommunikationsanwendung am Erstellen von untergeordneten Prozessen hindern](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-office-communication-application-from-creating-child-processes)  

  - **Nicht konfiguriert**  
  - **Aktivieren:** Hiermit wird die Erstellung untergeordneter Prozesse über Office-Kommunikations-Apps blockiert.  
  - **Nur überwachen**  

#### <a name="rules-to-prevent-script-threats"></a>Regeln zum Verhindern von Bedrohungen durch Skripts  

Blockieren Sie diese Optionen, um Bedrohungen durch Skripts zu verhindern:  

- **Verborgener JS-/VBS-/PS-/Makrocode**  
  **Standardeinstellung:** Nicht konfiguriert  
  Regel: [Ausführung möglicherweise verschleierter Skripts blockieren](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-execution-of-potentially-obfuscated-scripts)    

  - **Nicht konfiguriert**  
  - **Blockieren:** Hiermit blockieren Sie verborgenen JS-/VBS-/PS-/Makrocode.  
  - **Nur überwachen**  

- **Ausführung von aus dem Internet heruntergeladener Nutzlast über JS/VBS (keine Ausnahmen)**  
  **Standardeinstellung:** Nicht konfiguriert  
  Regel: [Starten heruntergeladener ausführbarer Inhalte durch JavaScript oder VBScript blockieren](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-javascript-or-vbscript-from-launching-downloaded-executable-content)  

  - **Nicht konfiguriert**  
  - **Blockieren:** Mit dieser Einstellung blockieren Sie die Ausführung von aus dem Internet heruntergeladener Payload über JS/VBS.  
  - **Nur überwachen**  

- **Prozesserstellung über die Befehle „PSExec“ und „WMI“**  
  **Standardeinstellung:** Nicht konfiguriert  
  Regel: [Erstellung von Prozessen durch PSExec- und WMI-Befehle blockieren](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-process-creations-originating-from-psexec-and-wmi-commands)  

  - **Nicht konfiguriert**  
  - **Blockieren**: Blockiert Prozesserstellungen über die Befehle „PSExec“ und „WMI“.  
  
  - **Nur überwachen**  

- **Nicht vertrauenswürdige und nicht signierte Prozesse, die über USB ausgeführt werden**  
  **Standardeinstellung:** Nicht konfiguriert  
  Regel: [Nicht vertrauenswürdige und nicht signierte Prozesse, die über USB ausgeführt werden, blockieren](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-untrusted-and-unsigned-processes-that-run-from-usb)    

  - **Nicht konfiguriert**  
  - **Blockieren**: Blockiert nicht vertrauenswürdige und nicht signierte Prozesse, die über USB ausgeführt werden.  
  - **Nur überwachen**  
  
- **Ausführbare Dateien, die keinem Listenkriterium zur Verbreitung, zum Alter oder zur Vertrauenswürdigkeit entsprechen**  
  **Standardeinstellung:** Nicht konfiguriert  
  Regel: [Ausführbare Dateien an der Ausführung hindern, außer sie erfüllen Kriterium zur Verbreitung, zum Alter oder zu vertrauenswürdigen Listen](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-executable-files-from-running-unless-they-meet-a-prevalence-age-or-trusted-list-criterion)    

  - **Nicht konfiguriert**  
  - **Blockieren**: Blockiert das Ausführen ausführbarer Dateien, wenn sie keinem Listenkriterium zur Verbreitung, zum Alter oder zur Vertrauenswürdigkeit entsprechen.  
  - **Nur überwachen**  

#### <a name="rules-to-prevent-email-threats"></a>Regeln zum Verhindern von Bedrohungen durch E-Mails  

Blockieren Sie diese Optionen, um Bedrohungen durch E-Mails zu verhindern:  

- **Ausführung ausführbarer Inhalte (EXE, DLL, PS, JS, VBS usw.), die per E-Mail (Webmail-/E-Mail-Client) zugestellt werden (keine Ausnahmen)**  
  **Standardeinstellung:** Nicht konfiguriert  
  Regel: [Ausführbare Inhalte von E-Mail-Clients und Webmail blockieren](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-executable-content-from-email-client-and-webmail)  

  - **Nicht konfiguriert**  
  - **Blockieren**: Blockiert die Ausführung ausführbarer Inhalte (EXE, DLL, PS, JS, VBS usw.), die per E-Mail (Webmail-/E-Mail-Client) zugestellt werden.  
  - **Nur überwachen**  

#### <a name="rules-to-protect-against-ransomware"></a>Regeln zum Schutz vor Ransomware  

- **Erweiterter Schutz vor Ransomware**  
  Standard:  Nicht konfiguriert  
  Regel: [Erweiterten Schutz vor Ransomware verwenden](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#use-advanced-protection-against-ransomware)  

  - **Nicht konfiguriert**  
  - **Aktivieren**: Verwenden Sie einen offensiven Schutz vor Ransomware.  
  - **Nur überwachen**  

#### <a name="attack-surface-reduction-exceptions"></a>Ausnahmen von der Verringerung der Angriffsfläche

- **Von Regeln zur Verringerung der Angriffsfläche auszuschließende Dateien und Ordner**  
  Defender-CSP: [AttackSurfaceReductionOnlyExclusions](https://go.microsoft.com/fwlink/?linkid=872981)  

  - **Importieren** Sie eine CSV-Datei, die Dateien und Ordner enthält, die von den Regeln zur Verringerung der Angriffsfläche ausgeschlossen werden sollen.  
  - Lokale Dateien oder Ordner können Sie manuell **hinzufügen**.  

> [!IMPORTANT]  
> Durch die entsprechenden Antischadsoftwareeinstellungen sollte die Überprüfung der folgenden Verzeichnisse ausgeschlossen werden, damit Win32-Branchenanwendungen ordnungsgemäß installiert und ausgeführt werden können:  
> **Auf X64-Clientcomputern:**  
> *C:\Program Files (x86)\Microsoft Intune Management Extension\Content*  
> *C:\windows\IMECache*  
>  
> **Auf X86-Clientcomputern:**  
> *C:\Program Files\Microsoft Intune Management Extension\Content*  
> *C:\windows\IMECache*  

### <a name="controlled-folder-access"></a>Überwachter Ordnerzugriff  

[Schützen Sie wichtige Daten](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/controlled-folders) vor schädlichen Apps und Bedrohungen, z. B. vor Ransomware.  

- **Ordnerschutz**  
  **Standardeinstellung:** Nicht konfiguriert  
  Defender-CSP: [EnableControlledFolderAccess](https://go.microsoft.com/fwlink/?linkid=872614)  

  Hiermit schützen Sie Dateien und Ordner vor unbefugten Änderungen durch bösartige Apps.  

  - **Nicht konfiguriert**  
  - **Aktivieren**  
  - **Nur überwachen**  
  - **Nur die Änderung des Datenträgers blockieren**  
  - **Änderung des Datenträgers überprüfen**  

  Wenn Sie eine andere Einstellung als die Standardeinstellung *Nicht konfiguriert* festlegen möchten, stehen Ihnen folgende Optionen zur Verfügung:  
  - **Liste der Apps, die auf geschützte Ordner zugreifen können**  
    Defender-CSP: [ControlledFolderAccessAllowedApplications](https://go.microsoft.com/fwlink/?linkid=872616)  

    - **Importieren** Sie eine CSV-Datei, die eine Liste der Apps enthält.  
    - Sie können Apps manuell zu dieser Liste **hinzufügen**.  

  - **Liste zusätzlicher Ordner, die geschützt werden müssen**  
    Defender-CSP: [ControlledFolderAccessProtectedFolders](https://go.microsoft.com/fwlink/?linkid=872617)  

    - **Importieren** Sie eine CSV-Datei, die eine Liste der Ordner enthält.  
    - Sie können Ordner manuell zu dieser Liste **hinzufügen**.  

### <a name="network-filtering"></a>Netzwerkfilterung  

Sie können von beliebigen Apps ausgehende Verbindungen an nicht vertrauenswürdige IP-Adressen oder Domänen blockieren. Die Netzwerkfilterung wird sowohl im Überwachungs- als auch im Blockierungsmodus unterstützt.  

- **Netzwerkschutz**  
  **Standardeinstellung:** Nicht konfiguriert  
  Defender-CSP: [EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=872618)  

  Diese Einstellung soll Endbenutzer vor Apps mit Zugriff auf Phishing-Angriffe, Websites mit Exploits und schädlichen Inhalten im Internet schützen. Außerdem wird verhindert, dass Drittanbieterbrowser Verbindungen mit gefährlichen Websites herstellen.  

  - **Nicht konfiguriert**: Deaktivieren Sie dieses Feature. Benutzer und Apps werden nicht daran gehindert, Verbindungen mit gefährlichen Domänen herzustellen. Administratoren wird diese Aktivität im Microsoft Defender Security Center nicht angezeigt.  
  - **Aktivieren:** Mit dieser Einstellung wird der Netzwerkschutz aktiviert, und Benutzer und Apps werden daran gehindert, Verbindungen mit gefährlichen Domänen herzustellen. Administratoren wird diese Aktivität im Microsoft Defender Security Center angezeigt.  
  - **Nur überwachen:** Benutzer und Apps werden nicht daran gehindert, Verbindungen mit gefährlichen Domänen herzustellen. Administratoren wird diese Aktivität im Microsoft Defender Security Center angezeigt.  

### <a name="exploit-protection"></a>Exploit-Schutz  

- **XML hochladen**  
  **Standardeinstellung:** *Nicht konfiguriert*  

  Erstellen Sie eine XML-Datei, die die gewünschten System- und Anwendungsschutzeinstellungen enthält, um den Exploit-Schutz [zum Schützen Ihrer Geräte vor Exploits](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) zu verwenden. Es gibt zwei Methoden zum Erstellen dieser XML-Datei:  

  - *PowerShell*: Verwenden Sie mindestens eines der PowerShell-Cmdlets *Get-ProcessMitigation*, *Set-ProcessMitigation* und *ConvertTo-ProcessMitigationPolicy*. Die Cmdlets konfigurieren Einstellungen zur Risikominderung und exportieren eine XML-Darstellung von ihnen.  

  - *Benutzeroberfläche von Microsoft Defender Security Center*: Klicken Sie im Microsoft Defender Security Center auf „App- und Browsersteuerung“, und scrollen Sie zum unteren Ende des entsprechenden Bildschirms, um den Exploit-Schutz zu finden. Verwenden Sie zuerst die Registerkarten „Systemeinstellungen“ und „Programmeinstellungen“, um die Einstellungen für die Risikominderung zu konfigurieren. Suchen Sie anschließend den Link mit den Exporteinstellungen im unteren Bildschirmbereich, um eine XML-Darstellung zu exportieren.  

- **Bearbeitung der Exploit-Schutzumgebung durch Benutzer**  
  **Standardeinstellung:** Nicht konfiguriert  
  ExploitGuard-CSP: [ExploitProtectionSettings](https://go.microsoft.com/fwlink/?linkid=872887)  


  - **Blockieren:** Laden Sie eine XML-Datei hoch, mit der Sie den Arbeitsspeicher, die Ablaufsteuerung und die Richtlinieneinschränkungen konfigurieren können. Die Einstellungen in der XML-Datei können eine Anwendung vor Exploits schützen.  
  - **Nicht konfiguriert:** Mit dieser Einstellung wird keine benutzerdefinierte Konfiguration verwendet.  

## <a name="microsoft-defender-application-control"></a>Microsoft Defender-Anwendungssteuerung  

Wählen Sie zusätzliche Apps aus, die von der Microsoft Defender-Anwendungssteuerung überwacht werden muss oder als vertrauenswürdig eingestuft und ausgeführt werden kann. Windows-Komponenten und alle Apps aus dem Windows Store werden automatisch als zur Ausführung vertrauenswürdig eingestuft.  


- **Anwendungssteuerungscode-Integritätsrichtlinien**  
  **Standardeinstellung:** Nicht konfiguriert  
   CSP: [AppLocker-CSP](https://go.microsoft.com/fwlink/?linkid=874543)  

  - **Erzwingen:** Mit dieser Einstellung können Sie die Anwendungssteuerungscode-Integritätsrichtlinien für die Geräte Ihrer Benutzer auswählen.  
  
    Sobald die Anwendungssteuerung auf einem Gerät aktiviert wurde, kann sie nur noch deaktiviert werden, indem der Modus von *Erzwingen* in *Nur überwachen* geändert wird. Wenn der Modus von *Erzwingen* in *Nicht konfiguriert* geändert wird, wird die Anwendungssteuerung weiterhin auf zugewiesenen Geräten erzwungen.  

  - **Nicht konfiguriert:** Bei dieser Einstellung wird die Anwendungssteuerung nicht zu den Geräten hinzugefügt. Zuvor hinzugefügte Einstellungen werden jedoch weiterhin für die zugewiesenen Geräte erzwungen. 
 
  - **Nur überwachen:** Anwendungen werden nicht blockiert. Alle Ereignisse werden in den Protokollen des lokalen Clients protokolliert.  

## <a name="microsoft-defender-credential-guard"></a>Microsoft Defender Credential Guard  

Microsoft Defender Credential Guard schützt vor Angriffen zum Diebstahl von Anmeldeinformationen. Geheime Schlüssel werden isoliert, damit nur privilegierte Systemsoftware darauf zugreifen kann.  

- **Credential Guard**  
  **Standardeinstellung:** Deaktivieren  
  [DeviceGuard-CSP](https://go.microsoft.com/fwlink/?linkid=872424)  

  - **Deaktivieren**: Deaktiviert Credential Guard per Remoteverbindung, wenn das Programm zuvor über die Option **Ohne UEFI-Sperre aktivieren** aktiviert wurde.  

  - **Mit UEFI-Sperre aktivieren**: Credential Guard kann nicht per Remoteverbindung mit einem Registrierungsschlüssel oder über eine Gruppenrichtlinie deaktiviert werden.  

    > [!NOTE]
    > Wenn Sie diese Einstellung verwenden und dann später Credential Guard deaktivieren möchten, müssen Sie die Gruppenrichtlinie auf **Deaktiviert** setzen. Außerdem müssen Sie die UEFI-Konfigurationsinformationen physisch von den einzelnen Computern löschen. Solange die UEFI-Konfiguration bestehen bleibt, ist Credential Guard weiter aktiviert.  

  - **Ohne UEFI-Sperre aktivieren**: Ermöglicht, Credential Guard über eine Remoteverbindung mithilfe einer Gruppenrichtlinie zu deaktivieren. Die Geräte, die diese Einstellung verwenden, müssen Windows 10 (Version 1511) oder höher ausführen.  

  Wenn Sie Credential Guard *aktivieren*, werden auch die folgenden erforderlichen Features aktiviert:  
  
  - **Virtualization-based Security (VBS)** (Virtualisierungsbasierte Sicherheit (VBS))  
    Wird im Rahmen des nächsten Neustarts aktiviert. Virtualisierungsbasierte Sicherheit verwendet Windows Hypervisor, um die Sicherheitsdienste zu unterstützen.  
  - **Sicherer Start und DMA-Schutz**  
    Aktiviert die VBS mit den Schutzmaßnahmen für sicheren Start und DMA (Direct Memory Access, direkter Speicherzugriff). Für die DMA-Schutzfunktionen ist Hardwaresupport erforderlich. Außerdem werden sie nur auf richtig konfigurierten Geräten aktiviert.  

## <a name="microsoft-defender-security-center"></a>Microsoft Defender Security Center  

Microsoft Defender Security Center fungiert als separate App bzw. separater Prozess der einzelnen Features. Sie zeigt Benachrichtigungen über das Info-Center an. Sie dienst als Collector oder zentraler Ort, um den Status anzuzeigen und Konfigurationen für die verschiedenen Features auszuführen. Weitere Informationen finden Sie in der Dokumentation zu [Windows Defender](https://docs.microsoft.com/windows/threat-protection/windows-defender-security-center/windows-defender-security-center).  

### <a name="microsoft-defender-security-center-app-and-notifications"></a>Microsoft Defender Security Center-App und -Benachrichtigungen  

Blockieren Sie den Benutzerzugriff auf die verschiedenen Bereiche der Microsoft Defender Security Center-App. Durch das Ausblenden eines Abschnitts werden auch die zugehörigen Benachrichtigungen blockiert.  

- **Viren- und Bedrohungsschutz**  
  **Standardeinstellung:** Nicht konfiguriert  
  WindowsDefenderSecurityCenter-CSP: [DisableVirusUI](https://go.microsoft.com/fwlink/?linkid=873662)  

  Konfigurieren Sie diese Einstellung, wenn Endbenutzer den Viren- und Bedrohungsschutzbereich in Microsoft Defender Security Center anzeigen können. Wenn dieser Abschnitt ausgeblendet wird, werden auch alle Benachrichtigungen zum Viren- und Bedrohungsschutz blockiert.  

  - **Nicht konfiguriert**  
  - **Ausblenden**  

- **Ransomware-Schutz**  
  **Standardeinstellung:** Nicht konfiguriert  
  WindowsDefenderSecurityCenter-CSP: [HideRansomwareDataRecovery](https://go.microsoft.com/fwlink/?linkid=873664)  

  Konfigurieren Sie diese Einstellung, wenn Endbenutzer den Ransomware-Schutzbereich in Microsoft Defender Security Center anzeigen können. Wenn dieser Abschnitt ausgeblendet wird, werden auch alle Benachrichtigungen zum Ransomware-Schutz blockiert.  

  - **Nicht konfiguriert**  
  - **Ausblenden**  

- **Kontoschutz**  
  **Standardeinstellung:** Nicht konfiguriert  
  WindowsDefenderSecurityCenter-CSP: [DisableAccountProtectionUI](https://go.microsoft.com/fwlink/?linkid=873666)  

  Konfigurieren Sie diese Einstellung, wenn Endbenutzer den Kontenschutzbereich in Microsoft Defender Security Center anzeigen können. Wenn dieser Abschnitt ausgeblendet wird, werden auch alle Benachrichtigungen zum Kontenschutz blockiert.  

  - **Nicht konfiguriert**  
  - **Ausblenden**  

- **Firewall- und Netzwerkschutz**  
  **Standardeinstellung:** Nicht konfiguriert  
  WindowsDefenderSecurityCenter-CSP: [DisableNetworkUI](https://go.microsoft.com/fwlink/?linkid=873668)  

  Konfigurieren Sie diese Einstellung, wenn Endbenutzer den Firewall- und Netzwerkschutzbereich in Microsoft Defender Security Center anzeigen können. Wenn dieser Abschnitt ausgeblendet wird, werden auch alle Benachrichtigungen zum Firewall- und Netzwerkschutz blockiert.  

  - **Nicht konfiguriert**  
  - **Ausblenden**  

- **App- und Browsersteuerung**  
  **Standardeinstellung:** Nicht konfiguriert  
  WindowsDefenderSecurityCenter-CSP: [DisableAppBrowserUI](https://go.microsoft.com/fwlink/?linkid=873669)  

  Konfigurieren Sie diese Einstellung, wenn App- und Browsersteuerungsbereich in Microsoft Defender Security Center anzeigen können. Wenn dieser Abschnitt ausgeblendet wird, werden auch alle Benachrichtigungen zur App- und Browsersteuerung blockiert.  

  - **Nicht konfiguriert**  
  - **Ausblenden**  

- **Hardwareschutz**  
  **Standardeinstellung:** Nicht konfiguriert  
  WindowsDefenderSecurityCenter-CSP: [DisableDeviceSecurityUI](https://go.microsoft.com/fwlink/?linkid=873670)  

  Konfigurieren Sie diese Einstellung, wenn Endbenutzer den Hardwareschutzbereich in Microsoft Defender Security Center anzeigen können. Wenn dieser Abschnitt ausgeblendet wird, werden auch alle Benachrichtigungen zum Hardwareschutz blockiert.  

  - **Nicht konfiguriert**  
  - **Ausblenden**  

- **Geräteleistung und -integrität**  
  **Standardeinstellung:** Nicht konfiguriert  
  WindowsDefenderSecurityCenter-CSP: [DisableHealthUI](https://go.microsoft.com/fwlink/?linkid=873671)  

  Konfigurieren Sie diese Einstellung, wenn Endbenutzer den Geräteleistungs- und Integritätsbereich in Microsoft Defender Security Center anzeigen können. Wenn dieser Abschnitt ausgeblendet wird, werden auch alle Benachrichtigungen zur Geräteleistung und Integrität blockiert.  
  
  - **Nicht konfiguriert**  
  - **Ausblenden**  

- **Familienoptionen**  
  **Standardeinstellung:** Nicht konfiguriert  
  WindowsDefenderSecurityCenter-CSP: [DisableFamilyUI](https://go.microsoft.com/fwlink/?linkid=873673)  

  Konfigurieren Sie diese Einstellung, wenn Endbenutzer den Bereich für Familienoptionen in Microsoft Defender Security Center anzeigen können. Wenn dieser Abschnitt ausgeblendet wird, werden auch alle Benachrichtigungen zu Familienoptionen blockiert.  
  
  - **Nicht konfiguriert**  
  - **Ausblenden**  

- **Benachrichtigungen aus den angezeigten Bereichen der App**  
  **Standardeinstellung:** Nicht konfiguriert  
  WindowsDefenderSecurityCenter-CSP: [DisableNotifications](https://go.microsoft.com/fwlink/?linkid=873675)  

  Wählen Sie aus, welche Benachrichtigungen Endbenutzern angezeigt werden. Zu den nicht kritischen Benachrichtigungen gehören Zusammenfassungen der Aktivitäten von Microsoft Defender Antivirus, Benachrichtigungen zum Abschluss von Überprüfungen eingeschlossen. Alle übrigen Benachrichtigungen gelten als kritisch.  

  - **Nicht konfiguriert**  
  - **Nicht kritische Benachrichtigungen blockieren**  
  - **Alle Benachrichtigungen blockieren**  

- **Symbol für das Windows Security Center in der Taskleiste**  
  **Standardeinstellung:** Nicht konfiguriert  

  Hiermit können Sie die Anzeige des Steuerelements für den Benachrichtigungsbereich konfigurieren. Der Benutzer muss sich entweder abmelden und anmelden oder den Computer neu starten, damit diese Einstellung wirksam wird.  
  
  - **Nicht konfiguriert**  
  - **Ausblenden**  

- **Schaltfläche „TPM löschen“**  
  **Standardeinstellung:** Nicht konfiguriert  

  Hiermit konfigurieren Sie die Anzeige der Schaltfläche „TPM löschen“.  
  
  - **Nicht konfiguriert**  
  - **Deaktivieren**  

- **Warnung zu TPM-Firmwareupdate**  
  **Standardeinstellung:** Nicht konfiguriert  
  
  Hiermit konfigurieren Sie die Anzeige des TPM-Firmwareupdates, wenn eine anfällige Firmware erkannt wird.  

  - **Nicht konfiguriert**  
  - **Ausblenden**  

- **Manipulationsschutz**  
  **Standardeinstellung:** Nicht konfiguriert

  Hiermit können Sie den Manipulationsschutz für Geräte ein- und ausschalten. Zum Verwenden des Manipulationsschutzes müssen Sie [Microsoft Defender Advanced Threat Protection mit Intune integrieren](advanced-threat-protection.md) und [Enterprise Mobility + Security E5-Lizenzen](../fundamentals/licenses.md) besitzen.  
  - **Nicht konfiguriert:** Bei dieser Einstellung werden keine Änderungen an den Geräteeinstellungen vorgenommen.
  - **Aktiviert:** Bei dieser Einstellung wird der Manipulationsschutz aktiviert und Einschränkungen werden für die Geräte erzwungen.
  - **Deaktiviert:** Bei dieser Einstellung wird der Manipulationsschutz deaktiviert und keine Einschränkungen werden erzwungen.

### <a name="it-contact-information"></a>IT-Kontaktinformationen  

Stellen Sie IT-Kontaktinformationen bereit, die in der Microsoft Defender Security Center-App und in den App-Benachrichtigungen angezeigt werden.  

Sie können **In Apps und Benachrichtigungen anzeigen**, **Nur in App anzeigen**, **Nur in Benachrichtigungen anzeigen** oder **Don‘t display** (Nicht anzeigen) auswählen. Geben Sie den **Namen der IT-Organisation** und mindestens eine der folgenden Kontaktoptionen ein:  


- **IT-Kontaktinformationen**  
  **Standardeinstellung:** Nicht anzeigen  
  WindowsDefenderSecurityCenter-CSP: [EnableCustomizedToasts](https://go.microsoft.com/fwlink/?linkid=873676)  
  
  Hiermit konfigurieren Sie, ob den Benutzern IT-Kontaktinformationen angezeigt werden.  
  
  - **In App und Benachrichtigungen anzeigen**  
  - **Nur in App anzeigen**  
  - **Nur in Benachrichtigungen anzeigen**  
  - **Nicht anzeigen**  

  Wenn Sie die Anzeige aktivieren, können Sie die folgenden Einstellungen konfigurieren:  

  - **Name der IT-Organisation**  
    **Standardeinstellung:** *Nicht konfiguriert*  
    WindowsDefenderSecurityCenter-CSP: [CompanyName](https://go.microsoft.com/fwlink/?linkid=873677)  

  - **Telefonnummer oder Skype-ID der IT-Abteilung**  
    **Standardeinstellung:** *Nicht konfiguriert*  
    WindowsDefenderSecurityCenter-CSP: [Phone](https://go.microsoft.com/fwlink/?linkid=873678) 

  - **E-Mail-Adresse der IT-Abteilung**  
    **Standardeinstellung:** *Nicht konfiguriert*  
    WindowsDefenderSecurityCenter-CSP: [E-Mail](https://go.microsoft.com/fwlink/?linkid=873679)  

  - **URL der IT-Supportwebsite**  
    **Standardeinstellung:** *Nicht konfiguriert*  
    WindowsDefenderSecurityCenter-CSP: [URL](https://go.microsoft.com/fwlink/?linkid=873680)  
 
## <a name="local-device-security-options"></a>Sicherheitsoptionen für lokale Geräte  

Konfigurieren Sie mit diesen Optionen die lokalen Sicherheitseinstellungen auf Windows 10-Geräten.  

### <a name="accounts"></a>Konten  

- **Neue Microsoft-Konten hinzufügen**  
  **Standardeinstellung:** Nicht konfiguriert  
  LocalPoliciesSecurityOptions-CSP: [Accounts_BlockMicrosoftAccounts](https://go.microsoft.com/fwlink/?linkid=867916)  


  - **Blockieren**: Verhindert, dass Benutzer diesem Gerät neue Microsoft-Konten hinzufügen.  
  - **Nicht konfiguriert:** Benutzer können Microsoft-Konten auf dem Gerät verwenden.  

- **Remoteanmeldung ohne Kennwort**  
  **Standardeinstellung:** Nicht konfiguriert  
  LocalPoliciesSecurityOptions-CSP: [Accounts_LimitLocalAccountUseOfBlankPasswordsToConsoleLogonOnly](https://go.microsoft.com/fwlink/?linkid=867890)  


   - **Blockieren**: Nur lokale Konten ohne Kennwörter können über die Tastatur des Geräts angemeldet werden.  
   - **Nicht konfiguriert**: Lokale Konten ohne Kennwort können sich auch von anderen Standorten als dem physischen Gerät aus anmelden.  

#### <a name="admin"></a>Administrator  

- **Lokales Administratorkonto**  
  **Standardeinstellung:** Nicht konfiguriert  
  LocalPoliciesSecurityOptions-CSP: [Accounts_LimitLocalAccountUseOfBlankPasswordsToConsoleLogonOnly](https://go.microsoft.com/fwlink/?linkid=867850)  


  - **Blockieren:** Mit dieser Einstellung verhindern Sie die Verwendung von lokalen Administratorkonten.  
  - **Nicht konfiguriert**  

- **Administratorkonto umbenennen**  
  **Standardeinstellung:** *Nicht konfiguriert*  
  LocalPoliciesSecurityOptions-CSP: [Accounts_RenameAdministratorAccount](https://go.microsoft.com/fwlink/?linkid=867917)  
 

  Definieren Sie einen anderen Kontonamen, der der Sicherheits-ID (SID) für das Administratorkonto zugeordnet werden soll.  

 #### <a name="guest"></a>Gast  

- **Gastkonto**  
  **Standardeinstellung:** Nicht konfiguriert  
  LocalPoliciesSecurityOptions-CSP: [LocalPoliciesSecurityOptions](https://go.microsoft.com/fwlink/?linkid=867853)  

  - **Blockieren:** Mit dieser Einstellung verhindern Sie die Verwendung von Gastkonten.  
  - **Nicht konfiguriert**  

- **Gastkonto umbenennen**  
  **Standardeinstellung:** *Nicht konfiguriert*  
  LocalPoliciesSecurityOptions-CSP: [Accounts_RenameGuestAccount](https://go.microsoft.com/fwlink/?linkid=867918)  
  
  Definieren Sie einen anderen Kontonamen, der der Sicherheits-ID (SID) für das Gastkonto zugeordnet werden soll.  

### <a name="devices"></a>Geräte  

- **Gerät ohne Anmeldung abdocken**  
  **Standardeinstellung:** Nicht konfiguriert  
  LocalPoliciesSecurityOptions-CSP: [Devices_AllowUndockWithoutHavingToLogon](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-devices-allowundockwithouthavingtologon)  

  
  - **Blockieren**: Benutzer können auf die physische Schaltfläche zum Auswerfen eines angedockten portablen Geräts drücken, um dieses sicher abzudocken.  
  - **Nicht konfiguriert:** Bei dieser Einstellung muss sich der Benutzer beim Gerät anmelden und die Berechtigung dafür erhalten, das Gerät abzudocken.  

- **Druckertreiber für freigegebene Drucker installieren**  
  **Standardeinstellung:**  Nicht konfiguriert  
  LocalPoliciesSecurityOptions-CSP: [Devices_PreventUsersFromInstallingPrinterDriversWhenConnectingToSharedPrinters](https://go.microsoft.com/fwlink/?linkid=867921)  


  - **Aktiviert**: Alle Benutzer können einen Druckertreiber installieren, wenn sie eine Verbindung mit einem freigegebenen Drucker herstellen.  
  - **Nicht konfiguriert**: Nur Administratoren können einen Druckertreiber installieren, wenn sie eine Verbindung mit einem freigegebenen Drucker herstellen.  

- **CD-ROM-Zugriff auf lokale aktive Benutzer beschränken**  
  **Standardeinstellung:**  Nicht konfiguriert  
  CSP: [Devices_RestrictCDROMAccessToLocallyLoggedOnUserOnly](https://go.microsoft.com/fwlink/?linkid=867922)  


  - **Aktiviert**: Nur der interaktiv angemeldete Benutzer kann CD-ROM-Medien verwenden. Wenn diese Richtlinie aktiviert ist und kein Benutzer interaktiv angemeldet ist, wird über das Netzwerk auf die CD-ROM zugegriffen.  
  - **Nicht konfiguriert:** Bei dieser Einstellung kann jeder Benutzer auf die CD-ROM zugreifen.  

- **Wechselmedien formatieren und auswerfen**  
  **Standardeinstellung:** Administratoren  
  CSP: [Devices_AllowedToFormatAndEjectRemovableMedia](https://go.microsoft.com/fwlink/?linkid=867920)  
 

  Definieren Sie, wer NTFS-Medien formatieren und auswerfen darf:  
  - **Nicht konfiguriert**  
  - **Administratoren**  
  - **Administratoren und Poweruser**  
  - **Administratoren und interaktive Benutzer**  

### <a name="interactive-logon"></a>Interaktive Anmeldung  

- **Minutes of lock screen inactivity until screen saver activates** (Inaktivität in Minuten für Anmeldebildschirm bis zur Aktivierung des Bildschirmschoners)  
  **Standardeinstellung:** *Nicht konfiguriert*  
  LocalPoliciesSecurityOptions-CSP: [InteractiveLogon_MachineInactivityLimit](https://go.microsoft.com/fwlink/?linkid=867891)  


  Geben Sie an, wie viele Minuten auf dem Anmeldebildschirm des interaktiven Desktops maximal Inaktivität herrschen darf, bis sich der Bildschirmschoner einschaltet. (**0** - **99999**)  

- **STRG+ALT+ENTF zur Anmeldung erforderlich**  
  **Standardeinstellung:** Nicht konfiguriert  
  LocalPoliciesSecurityOptions-CSP: [InteractiveLogon_DoNotRequireCTRLALTDEL](https://go.microsoft.com/fwlink/?linkid=867951)  


  - **Aktivieren**: Benutzer müssen STRG+ALT+ENTF drücken, um sich anzumelden.  
  - **Nicht konfiguriert**: Benutzer müssen STRG+ALT+ENTF drücken, bevor sie sich bei Windows anmelden.  

- **Smart card removal behavior** (Verhalten beim Entfernen von Smartcards)  
  **Standardeinstellung:** Arbeitsstation sperren   
  LocalPoliciesSecurityOptions-CSP: [InteractiveLogon_SmartCardRemovalBehavior](https://go.microsoft.com/fwlink/?linkid=868437)  
    
  Bestimmt, was geschieht, wenn die Smartcard für einen angemeldeten Benutzer aus dem Smartkartenleser entfernt wird. Folgende Optionen sind verfügbar:  

  - **Arbeitsstation sperren**: Die Arbeitsstation wird gesperrt, wenn die Smartcard entfernt wird. Diese Option ermöglicht es dem Benutzer, den Bereich zu verlassen, die Smartcard mitzunehmen und dennoch eine geschützte Sitzung beizubehalten.  
  - **Keine Aktion**  
  - **Abmeldung erzwingen**: Der Benutzer wird automatisch abgemeldet, wenn die Smartcard entfernt wird.  
  - **Bei Remotedesktopdienste-Sitzung trennen**: Das Entfernen der Smartcard beendet die Sitzung, ohne den Benutzer abzumelden. Diese Option ermöglicht es dem Benutzer, die Smartcard einzulegen und die Sitzung später oder auf einem anderen Computer mit Smartcard-Leser fortzusetzen, ohne sich erneut anmelden zu müssen. Wenn die Sitzung lokal stattfindet, funktioniert diese Richtlinie genau wie „Arbeitsstation sperren“.  

#### <a name="display"></a>Anzeige  

- **Benutzerinformationen auf Sperrbildschirm**  
  **Standardeinstellung:** Nicht konfiguriert  
  LocalPoliciesSecurityOptions-CSP: [InteractiveLogon_DisplayUserInformationWhenTheSessionIsLocked](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-interactivelogon-displayuserinformationwhenthesessionislocked)  

  Konfigurieren Sie die Benutzerinformationen, die angezeigt werden, wenn die Sitzung gesperrt ist. Wenn nicht konfiguriert, werden Anzeigename des Benutzers, Domäne und Benutzername angezeigt.  

  - **Nicht konfiguriert**  
  - **Anzeigename des Benutzers, Domäne und Benutzername**  
  - **Nur Anzeigename des Benutzers**  
  - **Benutzerinformationen nicht anzeigen**  

- **Zuletzt angemeldeten Benutzer ausblenden**  
  **Standardeinstellung:** Nicht konfiguriert  
  LocalPoliciesSecurityOptions-CSP: [InteractiveLogon_DoNotDisplayLastSignedIn](https://go.microsoft.com/fwlink/?linkid=868437)  
  
  
  - **Aktivieren:** Mit dieser Einstellung wird der Benutzername ausgeblendet.  
  - **Nicht konfiguriert:** Mit dieser Standardeinstellung wird der letzte Benutzername angezeigt.  

- **Benutzername bei der Anmeldung ausblenden**
  **Standardeinstellung:** Nicht konfiguriert  
  LocalPoliciesSecurityOptions-CSP: [InteractiveLogon_DoNotDisplayUsernameAtSignIn](https://go.microsoft.com/fwlink/?linkid=867959)  

  
  - **Aktivieren:** Mit dieser Einstellung wird der Benutzername ausgeblendet.  
  - **Nicht konfiguriert:** Mit dieser Standardeinstellung wird der letzte Benutzername angezeigt.  

- **Logon message title** (Titel der Anmeldenachricht)  
  **Standardeinstellung:** *Nicht konfiguriert*  
  LocalPoliciesSecurityOptions-CSP: [InteractiveLogon_MessageTitleForUsersAttemptingToLogOn](https://go.microsoft.com/fwlink/?linkid=867964)  

  Legen Sie den Nachrichtentitel für Benutzer fest, die sich anmelden.  

- **Logon message text** (Text der Anmeldenachricht)  
  **Standardeinstellung:** *Nicht konfiguriert*  
  LocalPoliciesSecurityOptions-CSP: [InteractiveLogon_MessageTextForUsersAttemptingToLogOn](https://go.microsoft.com/fwlink/?linkid=867962)  

  Legen Sie den Nachrichtext für Benutzer fest, die sich anmelden.  
  
### <a name="network-access-and-security"></a>Netzwerkzugriff und Sicherheit

- **Anonymer Zugriff auf Named Pipes und Freigaben**  
  **Standardeinstellung:** Nicht konfiguriert  
  LocalPoliciesSecurityOptions-CSP: [NetworkAccess_RestrictAnonymousAccessToNamedPipesAndShares](https://go.microsoft.com/fwlink/?linkid=868432)  

  - **Nicht konfiguriert**: Schränken Sie den anonymen Zugriff auf Freigabe- und Named Pipe-Einstellungen ein. Gilt für die Einstellungen, auf die anonym zugegriffen werden kann.  
  - **Blockieren:** Indem Sie diese Richtlinie mit dieser Einstellung deaktivieren, stellen Sie den anonymen Zugriff zur Verfügung.  

- **Anonyme Aufzählung von SAM-Konten**  
  **Standardeinstellung:** Nicht konfiguriert  
  LocalPoliciesSecurityOptions-CSP: [NetworkAccess_DoNotAllowAnonymousEnumerationOfSAMAccounts](https://go.microsoft.com/fwlink/?linkid=868434)  
  
  - **Nicht konfiguriert:** Bei dieser Einstellung können anonyme Benutzer SAM-Konten aufzählen.  
  - **Blockieren**: Verhindern Sie anonyme Enumerationen von SAM-Konten.  

- **Anonyme Aufzählung von SAM-Konten und Freigaben**  
  **Standardeinstellung:** Nicht konfiguriert  
  LocalPoliciesSecurityOptions-CSP: [NetworkAccess_DoNotAllowAnonymousEnumerationOfSamAccountsAndShares](https://go.microsoft.com/fwlink/?linkid=868435)  

  - **Nicht konfiguriert**: Anonyme Benutzer können die Namen der Domänenkonten und Netzwerkfreigaben auflisten.  
  - **Blockieren**: Verhindern Sie die anonyme Aufzählung von SAM-Konten und Freigaben. 

- **LAN-Manager-Hashwert bei Kennwortänderung speichern**  
  **Standardeinstellung:** Nicht konfiguriert  
  LocalPoliciesSecurityOptions-CSP: [NetworkSecurity_DoNotStoreLANManagerHashValueOnNextPasswordChange](https://go.microsoft.com/fwlink/?linkid=868431)  
   
  Mit dieser Einstellung bestimmen Sie, ob der Hashwert für Kennwörter bei der nächsten Kennwortänderung gespeichert wird. 
  - **Nicht konfiguriert:** Bei dieser Einstellung wird der Hashwert nicht gespeichert.  
  - **Blockieren:** Der LAN-Manager (LM) speichert bei dieser Einstellung den Hashwert für das neue Kennwort.  

- **PKU2U-Authentifizierungsanforderungen**  
  **Standardeinstellung:** Nicht konfiguriert  
  LocalPoliciesSecurityOptions-CSP: [NetworkSecurity_AllowPKU2UAuthenticationRequests](https://go.microsoft.com/fwlink/?linkid=867892)  

  - **Nicht konfiguriert:** Bei dieser Einstellung werden PKU2U-Anforderungen zugelassen.  
  - **Blockieren:** Bei dieser Einstellung werden PKU2U-Authentifizierungsanforderungen an das Gerät blockiert.  

- **RPC-Remoteverbindungen mit SAM einschränken**  
  **Standardeinstellung:** Nicht konfiguriert  
  LocalPoliciesSecurityOptions-CSP: [NetworkAccess_RestrictClientsAllowedToMakeRemoteCallsToSAM](https://go.microsoft.com/fwlink/?linkid=867893)  
  
  - **Nicht konfiguriert:** Bei dieser Einstellung wird die SDDL-Zeichenfolge (Security Descriptor Definition Language) verwendet, wodurch Benutzer und Gruppen RPC-Remoteaufrufe an den SAM (Security Account Manager, Sicherheitskonten-Manager) ausführen können.
  - **Zulassen:** Bei dieser Einstellung können Benutzer und Gruppen keine RPC-Remoteaufrufe an den SAM ausführen, der Benutzerkonten und Kennwörter speichert. Außerdem können Sie mit der Einstellung **Zulassen** die SDDL-Zeichenfolge ändern, um Benutzern und Gruppen das Ausführen dieser Remoteaufrufe explizit zu erlauben oder zu verweigern.  

    - **Sicherheitsbeschreibung**  
      **Standardeinstellung:** *Nicht konfiguriert*  
    
- **Minimum session security for NTLM SSP based clients** (Minimale Sitzungssicherheit für NTLM-basierte SSP-Clients)  
  **Standardeinstellung:** Keine  
  LocalPoliciesSecurityOptions-CSP: [NetworkSecurity_MinimumSessionSecurityForNTLMSSPBasedClients](https://aka.ms/policy-csp-localpoliciessecurityoptions-networksecurity-minimumsessionsecurityforntlmsspbasedclients)  
  
  Mit dieser Sicherheitseinstellung kann die Aushandlung der 128-Bit-Verschlüsselung und bzw. oder der NTLMv2-Sitzungssicherheit für einen Server als erforderlich festgelegt werden.  

  - **Keine**  
  - **NTLMv2-Sitzungssicherheit erfordern**  
  - **128-Bit-Verschlüsselung erfordern**  
  - **NTLMv2- und 128-Bit-Verschlüsselung erfordern**  
 
- **Minimum session security for NTLM SSP based servers** (Minimale Sitzungssicherheit für NTLM-basierte SSP-Server)  
  **Standardeinstellung:** Keine  
  LocalPoliciesSecurityOptions-CSP: [NetworkSecurity_MinimumSessionSecurityForNTLMSSPBasedServers](https://aka.ms/policy-csp-localpoliciessecurityoptions-networksecurity-minimumsessionsecurityforntlmsspbasedservers)  

  Mit dieser Sicherheitseinstellung wird festgelegt, welches Abfrage/Antwort-Authentifizierungsprotokoll für Netzwerkanmeldungen verwendet wird.  

  - **Keine**  
  - **NTLMv2-Sitzungssicherheit erfordern**  
  - **128-Bit-Verschlüsselung erfordern**  
  - **NTLMv2- und 128-Bit-Verschlüsselung erfordern**  

- **LAN-Manager-Authentifizierungsebene**  
  **Standardeinstellung:** LM und NTLM  
  LocalPoliciesSecurityOptions-CSP: [NetworkSecurity_LANManagerAuthenticationLevel](https://aka.ms/policy-csp-localpoliciessecurityoptions-lanmanagerauthenticationlevel)  


  - **LM und NTLM**  
  - **LM, NTLM und NTLMv2**  
  - **NTLM**  
  - **NTLMv2**  
  - **NTLMv2 und nicht LM**  
  - **NTLMv2 und nicht LM oder NTLM**  
  
- **Unsichere Gastanmeldungen**  
  **Standardeinstellung:** Nicht konfiguriert  
  LanmanWorkstation-CSP: [LanmanWorkstation](https://aka.ms/policy-csp-lanmanworkstation-enableinsecureguestlogons)  

  Wenn Sie diese Einstellung aktivieren, lehnt der SMB-Client unsichere Gastanmeldungen ab.  

  - **Nicht konfiguriert**  
  - **Blockieren:** Bei dieser Einstellung lehnt der SMB-Client unsichere Gastanmeldungen ab.  

### <a name="recovery-console-and-shutdown"></a>Wiederherstellungskonsole und Herunterfahren  

- **Virtuellen Arbeitsspeicher beim Herunterfahren löschen**  
  **Standardeinstellung:** Nicht konfiguriert  
   LocalPoliciesSecurityOptions-CSP: [Shutdown_ClearVirtualMemoryPageFile](https://go.microsoft.com/fwlink/?linkid=867914)  


  - **Aktivieren**: Der virtuelle Arbeitsspeicher wird beim Herunterfahren des Geräts gelöscht.  
  - **Nicht konfiguriert**: Der virtuelle Arbeitsspeicher wird nicht gelöscht.  

- **Shut down without log on** (Herunterfahren ohne Anmeldung)  
  **Standardeinstellung:** Nicht konfiguriert  
  LocalPoliciesSecurityOptions-CSP: [Shutdown_AllowSystemToBeShutDownWithoutHavingToLogOn](https://go.microsoft.com/fwlink/?linkid=867912)  

  
  - **Blockieren**: Auf dem Windows-Anmeldebildschirm wird die Option zum Herunterfahren ausgeblendet. Benutzer müssen sich beim Gerät anmelden und es dann herunterfahren.  
  - **Nicht konfiguriert**: Benutzer können das Gerät über den Windows-Anmeldebildschirm herunterfahren.  

### <a name="user-account-control"></a>Benutzerkontensteuerung  

- **UIA-Integrität ohne sicheren Speicherort**  
  **Standardeinstellung:** Nicht konfiguriert  
  LocalPoliciesSecurityOptions-CSP: [UserAccountControl_OnlyElevateUIAccessApplicationsThatAreInstalledInSecureLocations](https://go.microsoft.com/fwlink/?linkid=867897)  
  
  - **Blockieren:** Bei dieser Einstellung werden Apps, die sich an einem sicheren Speicherort im Dateisystem befinden, nur mit UIAccess-Integrität ausgeführt.  
  - **Nicht konfiguriert**: Apps können mit UIAccess-Integrität ausgeführt werden, auch wenn sie sich nicht an einem sicheren Ort im Dateisystem befinden.  

- **Fehler bei Schreibvorgängen für Dateien und Registrierung basierend auf Benutzerspeicherorten virtualisieren**  
  **Standardeinstellung:** Nicht konfiguriert  
  LocalPoliciesSecurityOptions-CSP: [UserAccountControl_VirtualizeFileAndRegistryWriteFailuresToPerUserLocations](https://go.microsoft.com/fwlink/?linkid=867900)  

  - **Aktiviert**: Bei Anwendungen, die Daten in geschützte Orte schreiben, treten Fehler auf.  
  - **Nicht konfiguriert**. Anwendungsschreibfehler werden zur Laufzeit sowohl für das Dateisystem als auch für die Registrierung an festgelegte Benutzerstandorte weitergeleitet.  

- **Rechte nur für ausführbare Dateien erhöhen, die signiert und validiert wurden**  
  **Standardeinstellung:** Nicht konfiguriert  
  LocalPoliciesSecurityOptions-CSP: [UserAccountControl_OnlyElevateUIAccessApplicationsThatAreInstalledInSecureLocations](https://go.microsoft.com/fwlink/?linkid=867965)  

  - **Aktiviert**: Erzwingen Sie die PKI-Zertifizierungspfadüberprüfung für eine ausführbare Datei vor ihrer Ausführung.  
  - **Nicht konfiguriert**: Erzwingen Sie keine Überprüfung des PKI-Zertifizierungspfads, bevor eine ausführbare Datei ausgeführt werden kann.  

#### <a name="uia-elevation-prompt-behavior"></a>Verhalten der UIA-Eingabeaufforderung für erhöhte Rechte  

- **Eingabeaufforderung für erhöhte Rechte für Administratoren**  
  **Standardeinstellung:** Zustimmungsaufforderung für Nicht-Windows-Binärdateien  
  LocalPoliciesSecurityOptions-CSP: [UserAccountControl_BehaviorOfTheElevationPromptForAdministrators](https://go.microsoft.com/fwlink/?linkid=867895)  

  Definieren Sie das Verhalten der Eingabeaufforderung für erhöhte Rechte für Administratoren im Administratorgenehmigungsmodus.  

  - **Nicht konfiguriert**  
  - **Rechte ohne Eingabeaufforderung erhöhen**  
  - **Eingabeaufforderung zu Anmeldeinformationen auf dem sicheren Desktop**  
  - **Eingabeaufforderung zu Anmeldeinformationen**  
  - **Eingabeaufforderung zur Zustimmung**  
  - **Zustimmungsaufforderung für Nicht-Windows-Binärdateien**  


- **Eingabeaufforderung für erhöhte Rechte für Standardbenutzer**  
  **Standardeinstellung:** Anmeldeinformationen anfordern  
  LocalPoliciesSecurityOptions-CSP: [UserAccountControl_BehaviorOfTheElevationPromptForStandardUsers](https://go.microsoft.com/fwlink/?linkid=867896)  

  Definieren Sie das Verhalten der Eingabeaufforderung für erhöhte Rechte für Standardbenutzer.  

  - **Nicht konfiguriert**  
  - **Anforderungen für erhöhte Rechte automatisch ablehnen**  
  - **Eingabeaufforderung zu Anmeldeinformationen auf dem sicheren Desktop**  
  - **Eingabeaufforderung zu Anmeldeinformationen**  

- **Eingabeaufforderung für erhöhte Rechte an interaktiven Desktop des Benutzers umleiten**  
  **Standardeinstellung:** Nicht konfiguriert  
  LocalPoliciesSecurityOptions-CSP: [UserAccountControl_SwitchToTheSecureDesktopWhenPromptingForElevation](https://go.microsoft.com/fwlink/?linkid=867899)  


  - **Aktiviert:** Bei dieser Einstellung werden alle Anforderungen für erhöhte Rechte an den interaktiven Desktop des Benutzers gerichtet, und nicht an den sicheren Desktop. Alle Richtlinieneinstellungen für das Verhalten der Eingabeaufforderung für Administratoren und Standardbenutzer werden verwendet.  
  - **Nicht konfiguriert**: Erzwingen Sie, dass alle Anforderungen für erhöhte Rechte an den sicheren Desktop umgeleitet werden, unabhängig von den Richtlinieneinstellungen für das Verhalten der Eingabeaufforderung für Administratoren und Standardbenutzer.

- **Eingabeaufforderung für erhöhte Rechte bei App-Installationen**  
  **Standardeinstellung:** Nicht konfiguriert  
  LocalPoliciesSecurityOptions-CSP: [UserAccountControl_DetectApplicationInstallationsAndPromptForElevation](https://go.microsoft.com/fwlink/?linkid=867901)  

   - **Aktiviert**: Anwendungsinstallationspakete werden nicht erkannt, und es wird keine Eingabeaufforderung für erhöhte Rechte angezeigt.
   - **Nicht konfiguriert**: Benutzer werden aufgefordert, den Benutzernamen und das Kennwort eines Administrators einzugeben, wenn ein Anwendungsinstallationspaket erhöhte Rechte erfordert.

- **UIA-Eingabeaufforderung für erhöhte Rechte ohne sicheren Desktop**  
  **Standardeinstellung:** Nicht konfiguriert  
  LocalPoliciesSecurityOptions-CSP: [UserAccountControl_AllowUIAccessApplicationsToPromptForElevation](https://go.microsoft.com/fwlink/?linkid=867894)  

- **Aktivieren**: Erlauben Sie, dass UIAccess-Anwendungen erhöhte Rechte ohne sicheren Desktop anfordern können.  
- **Nicht konfiguriert:** Bei dieser Einstellungen verwenden Eingabeaufforderungen für erhöhte Rechte einen sicheren Desktop.  

#### <a name="admin-approval-mode"></a>Administratorgenehmigungsmodus  

- **Administratorgenehmigungsmodus für integrierten Administrator**  
  **Standardeinstellung:** Nicht konfiguriert  
  LocalPoliciesSecurityOptions-CSP: [UserAccountControl_UseAdminApprovalMode](https://go.microsoft.com/fwlink/?linkid=867902)  

  - **Aktiviert**: Erlauben Sie, dass das integrierte Administratorkonto den Administratorgenehmigungsmodus verwenden kann. Der Benutzer wird bei jedem Vorgang, der eine Rechteerweiterungen erfordert, zur Genehmigung aufgefordert.  
  - **Nicht konfiguriert**: Alle Apps werden mit vollständigen Administratorrechten ausgeführt.  

- **Alle Administratoren im Administratorgenehmigungsmodus ausführen**  
  **Standardeinstellung:** Nicht konfiguriert  
  LocalPoliciesSecurityOptions-CSP: [UserAccountControl_RunAllAdministratorsInAdminApprovalMode](https://go.microsoft.com/fwlink/?linkid=867898)  


  - **Aktiviert:** Bei dieser Einstellung wird der Administratorgenehmigungsmodus aktiviert.  
  - **Nicht konfiguriert**: Deaktivieren Sie den Administratorgenehmigungsmodus und alle verwandten UAC-Richtlinieneinstellungen.  

### <a name="microsoft-network-client"></a>Microsoft-Netzwerkclient  

- **Kommunikation digital signieren (wenn Server zustimmt)**  
  **Standardeinstellung:** Nicht konfiguriert  
  LocalPoliciesSecurityOptions-CSP: [MicrosoftNetworkClient_DigitallySignCommunicationsIfServerAgrees](https://go.microsoft.com/fwlink/?linkid=868423)  

  Diese Einstellung legt fest, ob der SMB-Client die SMB-Paketsignatur aushandelt.  
  - **Blockieren:** Bei dieser Einstellung handelt der SMB-Client die SMB-Paketsignatur nie aus.
  - **Nicht konfiguriert**: Der Microsoft-Netzwerkclient fordert den Server zur Durchführung der SMB-Paketsignatur beim Setup der Sitzung auf. Wenn die Paketsignatur auf dem Server aktiviert ist, wird die Paketsignatur ausgehandelt.  

- **Unverschlüsseltes Kennwort an SMB-Server von Drittanbietern senden**  
  **Standardeinstellung:** Nicht konfiguriert  
  LocalPoliciesSecurityOptions-CSP: [MicrosoftNetworkClient_SendUnencryptedPasswordToThirdPartySMBServers](https://go.microsoft.com/fwlink/?linkid=868426)  


  - **Blockieren**: Der SMB-Redirector (Server Message Block) kann Klartextkennwörter an SMB-Server senden, die nicht von Microsoft stammen und keine Kennwortverschlüsselung während der Authentifizierung unterstützen.  
  - **Nicht konfiguriert:** Bei dieser Einstellung wird das Senden von Kennwörtern als Klartext verhindert. Die Kennwörter werden verschlüsselt.  

- **Kommunikation digital signieren (immer)**  
  **Standardeinstellung:** Nicht konfiguriert  
  LocalPoliciesSecurityOptions-CSP: [MicrosoftNetworkClient_DigitallySignCommunicationsAlways](https://go.microsoft.com/fwlink/?linkid=868425)  


  - **Aktivieren**: Der Microsoft-Netzwerkserver kommuniziert nur dann mit einem Microsoft-Netzwerkclient, wenn dieser der SMB-Paketsignatur zustimmt.  
  - **Nicht konfiguriert:** Mit dieser Standardeinstellung wird die SMB-Paketsignatur zwischen dem Client und dem Server ausgehandelt.  

### <a name="microsoft-network-server"></a>Microsoft-Netzwerkserver  
  
- **Kommunikation digital signieren (wenn Client zustimmt)**  
  **Standardeinstellung:** Nicht konfiguriert  
  CSP: [MicrosoftNetworkServer_DigitallySignCommunicationsIfClientAgrees](https://go.microsoft.com/fwlink/?linkid=868429)  

  - **Aktivieren**: Der Microsoft-Netzwerkserver handelt die SMB-Paketsignatur wie vom Client angefordert aus. Genau gesagt: Wenn die Paketsignatur auf dem Client aktiviert ist, wird die Paketsignatur ausgehandelt.  
  - **Nicht konfiguriert:** Bei dieser Einstellung handelt der SMB-Client die SMB-Paketsignatur nie aus.  

- **Kommunikation digital signieren (immer)**  
  **Standardeinstellung:** Nicht konfiguriert  
  CSP: [MicrosoftNetworkServer_DigitallySignCommunicationsAlways](https://go.microsoft.com/fwlink/?linkid=868428)  

  - **Aktivieren**: Der Microsoft-Netzwerkserver kommuniziert nur dann mit einem Microsoft-Netzwerkclient, wenn dieser der SMB-Paketsignatur zustimmt.  
  - **Nicht konfiguriert:** Mit dieser Standardeinstellung wird die SMB-Paketsignatur zwischen dem Client und dem Server ausgehandelt.  

## <a name="xbox-services"></a>Xbox-Dienste

- **Task zum Speichern von Xbox-Spiel**  
  **Standardeinstellung:** Nicht konfiguriert  
  CSP: [TaskScheduler/EnableXboxGameSaveTask](https://go.microsoft.com/fwlink/?linkid=875480)  
   
  Mit dieser Einstellung wird festgelegt, ob der Task zum Speichern von Xbox-Spielen aktiviert oder deaktiviert ist.  
  - **Enabled**
  - **Nicht konfiguriert**

- **Xbox-Zubehörverwaltungsdienst**  
  **Standardeinstellung:** Manuell  
  CSP: [SystemServices/ConfigureXboxAccessoryManagementServiceStartupMode](https://go.microsoft.com/fwlink/?linkid=875481)  

  Mit dieser Einstellung wird der Starttyp des Zubehörverwaltungsdiensts bestimmt.  
  - **Manuell**
  - **Automatisch**
  - **Deaktiviert**

- **Xbox Live Authentifizierungs-Manager-Dienst**  
  **Standardeinstellung:** Manuell  
  CSP: [SystemServices/ConfigureXboxLiveAuthManagerServiceStartupMode](https://go.microsoft.com/fwlink/?linkid=875482)  
 
  Mit dieser Einstellung wird der Starttyp des Xbox Live Authentifizierungs-Manager-Diensts bestimmt.  
  - **Manuell**
  - **Automatisch**
  - **Deaktiviert**
 
- **Dienst zum Speichern von Xbox Live-Spielen**  
  **Standardeinstellung:** Manuell  
  CSP: [SystemServices/ConfigureXboxLiveGameSaveServiceStartupMode](https://go.microsoft.com/fwlink/?linkid=875483)  

  Mit dieser Einstellung wird der Starttyp des Diensts zum Speichern von Xbox Live-Spielen bestimmt.  
  - **Manuell**
  - **Automatisch**
  - **Deaktiviert**

- **Xbox Live-Netzwerkdienst**  
  **Standardeinstellung:** Manuell  
  CSP: [SystemServices/ConfigureXboxLiveNetworkingServiceStartupMode](https://go.microsoft.com/fwlink/?linkid=875484)  

  Mit dieser Einstellung wird der Starttyp des Netzwerkdiensts bestimmt.  
  - **Manuell**
  - **Automatisch**
  - **Deaktiviert**

## <a name="next-steps"></a>Nächste Schritte

Das Profil ist nun erstellt, führt aber noch keine Aktionen durch. Die nächsten Schritte sind das [Zuweisen von Benutzer- und Geräteprofilen in Microsoft Intune](../configuration/device-profile-assign.md) und das [Überwachen von Geräteprofilen in Microsoft Intune](../configuration/device-profile-monitor.md).  

Konfigurieren von Endpoint Protection-Einstellungen auf [macOS](endpoint-protection-macos.md)-Geräten.  
