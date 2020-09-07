---
title: Firewalleinstellungen für Endpunktsicherheit in Intune | Microsoft-Dokumentation
description: Einstellungen der Firewallrichtlinie für Endpunktsicherheit für Windows und macOS in Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/28/2020
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
ms.openlocfilehash: 10d9320932e7835b8c2ecac46e35ea5a57375904
ms.sourcegitcommit: 42882de75c8a984ba35951b1165c424a7e0ba42e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2020
ms.locfileid: "89068132"
---
# <a name="firewall-policy-settings-for-endpoint-security-in-intune"></a>Einstellungen der Firewallrichtlinie für Endpunktsicherheit in Intune

Erfahren Sie, welche Einstellungen Sie im Intune-Knoten „Endpunktsicherheit“ im Rahmen einer [Endpunktsicherheitsrichtlinie](../protect/endpoint-security-policy.md) in Profilen für die *Firewallrichtlinie* konfigurieren können.

Unterstützte Plattformen und Profile:

- **macOS**:
  - Profil: **macOS-Firewall**

- **Windows 10 und höher**:
  - Profil: **Microsoft Defender Firewall**

## <a name="macos-firewall-profile"></a>Profil: macOS-Firewall

### <a name="firewall"></a>Firewall

Die folgenden Einstellungen werden als [Richtlinie für die Endpunktsicherheit für macOS-Firewalls](../protect/endpoint-security-firewall-policy.md) konfiguriert.

- **Firewall aktivieren**

  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Ja**: Aktiviert die Firewall.
  
  Bei Festlegung auf *Ja* können Sie die folgenden Einstellungen konfigurieren.  

  - **Alle eingehenden Verbindungen sperren**

    - **Nicht konfiguriert** (*Standardeinstellung*)
    - **Ja**: Blockiert alle eingehenden Verbindungen mit Ausnahme von Verbindungen, die für grundlegende Internetdienste wie DHCP, Bonjour und IPSec erforderlich sind. Durch diese Einstellung werden alle Freigabedienste blockiert.

  - **Geschützten Modus aktivieren**

    - **Nicht konfiguriert** (*Standardeinstellung*)
    - **Ja**: Verhindert, dass der Computer auf Testanforderungen reagiert. Der Computer antwortet weiterhin auf eingehende Anforderungen von autorisierten Apps.

  - **Firewall-Apps**: Erweitern Sie die Dropdownliste, und wählen Sie **Hinzufügen** aus. Geben Sie dann Apps und Regeln für eingehende Verbindungen für die App an.
    - **Eingehende Verbindungen zulassen**
      - Nicht konfiguriert
      - Blockieren
      - Zulassen

    - **Bundle ID**: Diese ID identifiziert die App. Beispiel: *com.apple.app*

## <a name="microsoft-defender-firewall-profile"></a>Profil „Microsoft Defender Firewall“

### <a name="microsoft-defender-firewall"></a>Microsoft Defender Firewall

Die folgenden Einstellungen werden als [Richtlinie für die Endpunktsicherheit für Windows 10-Firewalls](../protect/endpoint-security-firewall-policy.md) konfiguriert.

- **Zustandsbehaftetes FTP (File Transfer Protocol) deaktivieren**  
  CSP: [MdmStore/Global/DisableStatefulFtp](https://go.microsoft.com/fwlink/?linkid=872536)

  - **Nicht konfiguriert** (*Standard*): Die Firewall verwendet FTP zum Untersuchen und Filtern sekundärer Netzwerkverbindungen, sodass Ihre Firewallregeln möglicherweise ignoriert werden.
  - **Ja**
  
- **Die Anzahl der Sekunden, die sich eine Sicherheitszuordnung im Leerlauf befinden kann, bevor Sie gelöscht wird**  
  CSP: [MdmStore/Global/SaIdleTime](https://go.microsoft.com/fwlink/?linkid=872539)

  Geben Sie einen Zeitraum zwischen 300 und 3.600 Sekunden an, über den die Sicherheitszuordnungen beibehalten werden, nachdem kein Netzwerkdatenverkehr mehr angezeigt wird.
  
  Wenn Sie keinen Wert angeben, löscht das System eine Sicherheitszuordnung nach 300 Sekunden Leerlauf.
  
- **Codierung vorinstallierter Schlüssel**  
  CSP: [MdmStore/Global/PresharedKeyEncoding](https://go.microsoft.com/fwlink/?linkid=872541)

  Wenn *UTF-8* nicht als erforderlich angegeben ist, werden vorinstallierte Schlüssel anfangs mit UTF-8 verschlüsselt. Anschließend können Gerätebenutzer eine andere Verschlüsselungsmethode auswählen.

  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Keine**
  - **UTF8**

- **Firewall-IPsec-Ausnahmen lassen NDP zu**  
  CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Ja**: Firewall-IPsec-Ausnahmen lassen Nachbarermittlung zu.

- **Firewall-IPsec-Ausnahmen lassen ICMP zu**  
  CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Ja**: Firewall-IPsec-Ausnahmen lassen ICMP zu.

- **Firewall-IPsec-Ausnahmen ermöglichen Routerermittlung**  
  CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Ja**: Firewall-IPsec-Ausnahmen lassen Routerermittlung zu.

- **Firewall-IPsec-Ausnahmen lassen DHCP zu**  
  CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Ja**: Firewall-IPsec-Ausnahmen lassen DHCP zu.

- **Überprüfung der Zertifikatssperrliste (CRL)**  
  CSP: [MdmStore/Global/CRLcheck](https://go.microsoft.com/fwlink/?linkid=872548)

   Geben Sie an, wie die Überprüfung der Zertifikatssperrliste (CRL) durchgesetzt wird.
  - **Nicht konfiguriert** (*Standard*): Clients sind standardmäßig so konfiguriert, dass die CRL-Überprüfung deaktiviert ist.
  - **Keine**
  - **Versuch**
  - **Require**

- **Schlüsselerstellungsmodule dürfen nur die nicht von ihnen unterstützten Authentifizierungssammlungen ignorieren**  
  CSP: [MdmStore/Global/OpportunisticallyMatchAuthSetPerKM](https://go.microsoft.com/fwlink/?linkid=872550)

  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Ja**: Schlüsselerstellungsmodule ignorieren Authentifizierungssammlungen, die sie nicht unterstützen.

- **Paketwarteschlangen**  
  CSP: [MdmStore/Global/EnablePacketQueue](https://go.microsoft.com/fwlink/?linkid=872551)

  Geben Sie an, wie die Skalierung für die Software auf der Empfangsseite für den verschlüsselten Empfang und die Weiterleitung im Klartext für das IPsec-Tunnelgatewayszenario aktiviert werden soll. Auf diese Weise wird die Einhaltung der Paketreihenfolge sichergestellt.
  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung für Paketwarteschlangen wird auf den Standardwert des Clients zurückgesetzt, d. h. diese werden deaktiviert.
  - **Deaktiviert**
  - **Warteschlange für eingehenden Datenverkehr**
  - **Warteschlange für ausgehenden Datenverkehr**
  - **Warteschlange für beide**

- **Microsoft Defender-Firewall für Domänennetzwerke aktivieren**  
  CSP: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **Nicht konfiguriert** (*Standard*): Der Client wird auf die Standardeinstellungen zurückgesetzt, d. h. die Firewall wird aktiviert.
  - **Ja**: Die Microsoft Defender Firewall für den Netzwerktyp **Domäne** wird aktiviert und erzwungen.
  - **Nein**: Deaktiviert die Firewall.

- **Microsoft Defender-Firewall für private Netzwerke aktivieren**  
  CSP: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **Nicht konfiguriert** (*Standard*): Der Client wird auf die Standardeinstellungen zurückgesetzt, d. h. die Firewall wird aktiviert.
  - **Ja**: Die Microsoft Defender Firewall für den Netzwerktyp **Privat** wird aktiviert und erzwungen.
  - **Nein**: Deaktiviert die Firewall.

- **Microsoft Defender-Firewall für öffentliche Netzwerke aktivieren**  
  CSP: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **Nicht konfiguriert** (*Standard*): Der Client wird auf die Standardeinstellungen zurückgesetzt, d. h. die Firewall wird aktiviert.
  - **Ja**: Die Microsoft Defender Firewall für den Netzwerktyp **Öffentlich** wird aktiviert und erzwungen.
  - **Nein**: Deaktiviert die Firewall.

<!-- Microsoft Defender Firewall rules added in 2005  -->

### <a name="microsoft-defender-firewall-rules"></a>Microsoft Defender Firewall-Regeln

*Das Profil befindet sich in der Vorschau*.

Die folgenden Einstellungen werden als [Richtlinie für die Endpunktsicherheit für Windows 10-Firewalls](../protect/endpoint-security-firewall-policy.md) konfiguriert.

#### <a name="windows-firewall-rule"></a>Windows-Firewall-Regel

- **Name**  
  Geben Sie einen Anzeigenamen für Ihre Regel an. Dieser Name wird in der Regelliste angezeigt, damit Sie sie einfacher finden können.

- **Beschreibung**  
  Geben Sie eine Beschreibung für die Regel an.

- **Richtung**  
  - **Nicht konfiguriert** (*Standard*): Diese Regel gilt standardmäßig für ausgehenden Datenverkehr.
  - **Aus**: Diese Regel gilt für ausgehenden Datenverkehr.
  - **Ein**: Diese Regel gilt für eingehenden Datenverkehr.

- **Aktion**  
  - **Nicht konfiguriert** (*Standard*): Diese Regel lässt Datenverkehr standardmäßig zu.
  - **Blockiert**: Datenverkehr wird in der von Ihnen konfigurierten *Richtung* blockiert.
  - **Zugelassen**: Datenverkehr wird in der von Ihnen konfigurierten *Richtung* zugelassen.

- **Netzwerktyp**  
  Geben Sie den Netzwerktyp an, zu dem die Regel gehört. Sie können eine oder mehrere der folgenden Optionen auswählen. Wenn Sie keine Option auswählen, gilt die Regel für alle Netzwerktypen.
  - **Domäne**
  - **Privat**
  - **Öffentlich**
  - **Nicht konfiguriert**

- **Paketfamilienname**  
  [Get-AppxPackage](/previous-versions//hh856044(v=technet.10))

  Paketfamiliennamen können durch Ausführen des Befehls „Get-AppxPackage“ in PowerShell abgerufen werden.

- **Dateipfad**  
  CSP: [FirewallRules/Firewallregelname/App/FilePath](/windows/client-management/mdm/firewall-csp#filepath)

  Geben Sie den App-Speicherort auf dem Clientgerät ein, um den Dateipfad einer App anzugeben. Beispiel: `C:\Windows\System\Notepad.exe` oder `%WINDIR%\Notepad.exe`.

- **Dienstname**  
  [FirewallRules/Firewallregelname/App/ServiceName](/windows/client-management/mdm/firewall-csp#servicename)

  Verwenden Sie den Kurznamen eines Windows-Diensts, wenn Datenverkehr durch einen Dienst gesendet oder empfangen wird, nicht durch eine Anwendung. Um den Kurznamen eines Diensts abzurufen, führen Sie den Befehl `Get-Service` in PowerShell aus.

- **Protokoll**  
  CSP: [FirewallRules/Firewallregelname/Protocol](/windows/client-management/mdm/firewall-csp#protocol)

  Geben Sie das Protokoll für diese Portregel an.
  - Transportschichtprotokolle wie *TCP(6)* und *UDP(17)* ermöglichen die Angabe von Ports oder Portbereichen.
  - Bei benutzerdefinierten Protokollen geben Sie eine Zahl zwischen *0* und *255* ein, die das IP-Protokoll repräsentiert.
  - Wenn Sie keinen Wert angeben, lautet der Standardwert der Regel **Beliebig**.

- **Schnittstellentypen**  
  Geben Sie den Schnittstellentyp an, zu dem die Regel gehört. Sie können eine oder mehrere der folgenden Optionen auswählen. Wenn Sie keine Option auswählen, gilt die Regel für alle Schnittstellentypen:
  - **Remotezugriff**
  - **Drahtlos**
  - **Lokales Netzwerk**
  - **Nicht konfiguriert**

- **Autorisierte Benutzer**  
  [FirewallRules/Firewallregelname/LocalUserAuthorizationList](/windows/client-management/mdm/firewall-csp#localuserauthorizedlist)

  Legen Sie eine Liste autorisierter, lokaler Benutzer für diese Regel fest. Es kann keine Liste autorisierter Benutzer festgelegt werden, wenn der *Dienstname* in dieser Regel auf einen Windows-Dienst festgelegt ist. Wenn kein autorisierter Benutzer angegeben wird, lautet der Standardwert *Alle Benutzer*.

- **Beliebige lokale Adresse**  
  **Nicht konfiguriert** (*Standard*): Verwenden Sie die Einstellung *Lokale Adressbereiche**, um einen Bereich von Adressen zu konfigurieren, die unterstützt werden sollen.
  - **Ja**: Hiermit unterstützen Sie beliebige lokale Adressen und konfigurieren keinen Adressbereich.

- **Lokale Adressbereiche**  
  CSP: [FirewallRules/Firewallregelname/LocalAddressRanges](/windows/client-management/mdm/firewall-csp#localaddressranges)  

  Verwalten Sie lokale Adressbereiche für diese Regel. Sie können:
  - **Hinzufügen** verwenden, um mindestens eine Adresse als eine durch Trennzeichen getrennte Liste von lokalen Adressen hinzuzufügen, die der Regel unterliegen.
  - **Importieren** verwenden, um eine CSV-Datei zu importieren, die eine Liste von Adressen enthält, die als lokale Adressbereiche verwendet werden sollen.
  - **Exportieren** verwenden, um die aktuelle Liste der lokalen Adressbereiche als CSV-Datei zu exportieren.

  Gültige Einträge (Token) umfassen folgende Optionen:
  - **Ein Sternchen**: Ein Sternchen (\*) gibt eine beliebige lokale Adresse an. Falls dieses Zeichen vorhanden ist, darf kein anderes Token enthalten sein.
  - **Ein Subnetz**: Geben Sie Subnetze über die Subnetzmaske oder die Netzwerkpräfixnotation an. Wenn weder eine Subnetzmaske noch ein Netzwerkpräfix angegeben wird, lautet die Subnetzmaske standardmäßig 255.255.255.255.
  - **Eine gültige IPv6-Adresse**
  - **Ein IPv4-Adressbereich**: IPv4-Adressbereiche müssen im Format *Startadresse – Endadresse* ohne Leerzeichen vorliegen, und die Startadresse muss kleiner sein als die Endadresse.
  - **Ein IPv6-Adressbereich**: IPv6-Adressbereiche müssen im Format *Startadresse – Endadresse* ohne Leerzeichen vorliegen, und die Startadresse muss kleiner sein als die Endadresse.

  Wenn kein Wert angegeben wird, lautet der Standardwert für diese Einstellung *Beliebige Adresse*.

- **Beliebige Remoteadresse**  
  **Nicht konfiguriert** (*Standard*): Verwenden Sie die Einstellung *Remoteadressbereiche**, um einen Bereich von Adressen zu konfigurieren, die unterstützt werden sollen.
  - **Ja**: Hiermit unterstützen Sie beliebige Remoteadressen und konfigurieren keinen Adressbereich.

- **Remoteadressbereiche**  
  CSP: [FirewallRules/Firewallregelname/RemoteAddressRanges](/windows/client-management/mdm/firewall-csp#remoteaddressranges)  

  Verwalten Sie Remoteadressbereiche für diese Regel. Sie können:
  - **Hinzufügen** verwenden, um mindestens eine Adresse als eine durch Trennzeichen getrennte Liste von Remoteadressen hinzuzufügen, die der Regel unterliegen.
  - **Importieren** verwenden, um eine CSV-Datei zu importieren, die eine Liste von Adressen enthält, die als Remoteadressbereiche verwendet werden sollen.
  - **Exportieren** verwenden, um die aktuelle Liste der Remoteadressbereiche als CSV-Datei zu exportieren.

  Gültige Einträge (Token) umfassen folgende Optionen, Groß-/Kleinschreibung wird nicht beachtet:
  - **Ein Sternchen**: Ein Sternchen (\*) gibt eine beliebige Remoteadresse an. Falls dieses Zeichen vorhanden ist, darf kein anderes Token enthalten sein.
  - **Defaultgateway**
  - **DHCP**
  - **DNS**
  - **WINS**
  - **Intranet**: Wird auf Geräten unterstützt, auf denen Windows 1809 oder höher ausgeführt wird.
  - **RmtIntranet**: Wird auf Geräten unterstützt, auf denen Windows 1809 oder höher ausgeführt wird.
  - **Ply2Renders**: Wird auf Geräten unterstützt, auf denen Windows 1809 oder höher ausgeführt wird.
  - **LocalSubnet**: Gibt eine beliebige lokale Adresse im lokalen Subnetz an.
  - **Ein Subnetz**: Geben Sie Subnetze über die Subnetzmaske oder die Netzwerkpräfixnotation an. Wenn weder eine Subnetzmaske noch ein Netzwerkpräfix angegeben wird, lautet die Subnetzmaske standardmäßig 255.255.255.255.
  - **Eine gültige IPv6-Adresse**
  - **Ein IPv4-Adressbereich**: IPv4-Adressbereiche müssen im Format *Startadresse – Endadresse* ohne Leerzeichen vorliegen, und die Startadresse muss kleiner sein als die Endadresse.
  - **Ein IPv6-Adressbereich**: IPv6-Adressbereiche müssen im Format *Startadresse – Endadresse* ohne Leerzeichen vorliegen, und die Startadresse muss kleiner sein als die Endadresse.

  Wenn kein Wert angegeben wird, lautet der Standardwert für diese Einstellung *Beliebige Adresse*.

<!-- End of 2005 additions  -->

## <a name="next-steps"></a>Nächste Schritte

[Richtlinie für die Endpunktsicherheit für Firewalls](../protect/endpoint-security-firewall-policy.md)