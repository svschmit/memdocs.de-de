---
title: Einführung in Zertifikatprofile
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Zertifikatprofile in Configuration Manager mit den Active Directory-Zertifikatdiensten funktionieren.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 41dcc259-f147-4420-bff2-b65bdf8cff77
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 35269e7c727031a9cd66072985f3d9ec362978cf
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706318"
---
# <a name="introduction-to-certificate-profiles-in-configuration-manager"></a>Einführung in Zertifikatprofile in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Zertifikatprofile arbeiten mit Active Directory-Zertifikatdiensten und der Rolle des Registrierungsdiensts für Netzwerkgeräte (NDES, Network Device Enrollment Service). Erstellen Sie Authentifizierungszertifikate für verwaltete Geräte bzw. stellen Sie sie bereit, damit Benutzer einfach auf Organisationsressourcen zugreifen können. Sie können z.B. Zertifikatprofile erstellen und bereitstellen, um Benutzern die erforderlichen Zertifikate zum Herstellen einer Verbindung mit VPN- und Drahtlosverbindungen bereitzustellen.

Zertifikatprofile können Benutzergeräte automatisch für den Zugriff auf Unternehmensressourcen wie WLAN-Netzwerke und VPN-Server konfigurieren. Benutzer können auf diese Ressourcen zugreifen, ohne Zertifikate manuell installieren oder einen Out-of-Band-Prozess verwenden zu müssen. Mit Zertifikatprofilen werden Ressourcen gesichert, da Sie sicherere Einstellungen verwenden können, die von Ihrer Public Key-Infrastruktur (PKI) unterstützt werden. Sie können z.B. eine Serverauthentifizierung für alle WLAN- und VPN-Verbindungen erforderlich machen, da Sie die erforderlichen Zertifikate auf den verwalteten Geräten bereitgestellt haben.

Zertifikatprofile bieten die folgenden Verwaltungsfunktionen:  

- Zertifikatsregistrierung und -erneuerung über eine Zertifizierungsstelle (CA) für Geräte, auf denen verschiedene Betriebssysteme und -versionen ausgeführt werden. Diese Zertifikate können dann für WLAN- und VPN-Verbindungen verwendet werden.  

- Bereitstellen vertrauenswürdiger Zertifikate der Stamm- oder Zwischenzertifizierungsstelle Diese Zertifikate konfigurieren eine Vertrauenskette auf Geräten für VPN- und WLAN-Verbindungen, wenn die Serverauthentifizierung erforderlich ist.  

- Überwachen und Melden der installierten Zertifikate.  

**Beispiel 1**: Alle Mitarbeiter müssen eine Verbindung zu WLAN-Hotspots an mehreren Bürostandorten herstellen. Um die einfache Benutzerverbindung zu ermöglichen, stellen Sie zunächst die Zertifikate bereit, die für die WLAN-Verbindung erforderlich sind. Stellen Sie anschließend die WLAN-Profile bereit, die auf das Zertifikat verweisen.  

**Beispiel 2**: Sie verfügen über eine PKI. Sie möchten zu einer flexibleren und sichereren Methode für die Bereitstellung von Zertifikaten wechseln. Benutzer müssen von ihren persönlichen Geräten aus auf Unternehmensressourcen zugreifen können, ohne die Sicherheit zu gefährden. Konfigurieren Sie Zertifikatprofile mit Einstellungen und Protokollen, die von der jeweiligen Geräteplattform unterstützt werden. Die Geräte können diese Zertifikate dann automatisch von einem mit dem Internet verbundenen Registrierungsserver anfordern. Konfigurieren Sie anschließend VPN-Profile, die diese Zertifikate verwenden, damit das Gerät auf die Organisationsressourcen zugreifen kann.  

## <a name="types"></a>Typen

Es gibt drei Arten von Zertifikatprofilen:  

- **Vertrauenswürdiges Zertifikat der Zertifizierungsstelle**: Stellen Sie ein vertrauenswürdiges Zertifikat der Stamm- oder Zwischenzertifizierungsstelle bereit. Diese Zertifikate bilden eine Vertrauenskette, wenn das Gerät einen Server authentifizieren muss.  

- **Simple Certificate Enrollment-Protokoll (SCEP)** : Fordern Sie mithilfe des SCEP-Protokolls ein Zertifikat für ein Gerät oder einen Benutzer an. Dieser Typ erfordert eine NDES-Rolle (Registrierungsdienst für Netzwerkgeräte) auf einem Server unter Windows Server 2012 R2 oder höher.

    Sie müssen ein **vertrauenswürdiges Zertifikat der Zertifizierungsstelle** erstellen, um ein Zertifikatprofil des Typs **Simple Certificate Enrollment Protocol (SCEP)** erstellen zu können.

- **Privater Informationsaustausch – PKCS #12 (.PFX)** : Erfordert für ein Gerät oder einen Benutzer ein PFX-Zertifikat (auch als PKCS 12-Zertifikat bezeichnet).<!--1321368--> Es gibt zwei Methoden zur Erstellung von PFX-Zertifikatprofilen:

  - [Importieren von Anmeldeinformationen](../../mdm/deploy-use/import-pfx-certificate-profiles.md) aus vorhandenen Zertifikaten
  - [Definieren einer Zertifizierungsstelle](../../mdm/deploy-use/create-pfx-certificate-profiles.md) für die Verarbeitung von Anforderungen

  > [!Note]  
  > Configuration Manager aktiviert dieses optionale Feature nicht automatisch. Sie müssen dieses Feature aktivieren, bevor Sie es verwenden. Weitere Informationen finden Sie unter [Enable optional features from updates (Aktivieren optionaler Features von Updates)](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

  Sie können Microsoft oder Entrust als Zertifizierungsstellen für **PFX-Zertifikate (Personal information exchange)** nutzen.

## <a name="requirements"></a>Anforderungen

Um Zertifikatprofile bereitzustellen, die SCEP verwenden, installieren Sie den Zertifikatregistrierungspunkt auf einem Standortsystemserver. Installieren Sie ebenso ein Richtlinienmodul für den Registrierungsdienst für Netzwerkgeräte, das Configuration Manager-Richtlinienmodul, auf einem Server, der Windows Server 2012 R2 oder höher ausführt. Dieser Server erfordert die Rolle „Active Directory-Zertifikatdienste“. Er erfordert auch ein funktionierendes NDES, das für die Geräte, die die Zertifikate benötigen, zugänglich ist. Wenn sich Ihre Geräte für Zertifikate aus dem Internet anmelden müssen, dann muss Ihr NDES-Server aus dem Internet zugänglich sein. Zur sicheren Aktivierung des Datenverkehrs zum NDES-Server aus dem Internet können Sie z. B. [Azure-Anwendungsproxy](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy) verwenden.

PFX-Zertifikate erfordern auch einen Zertifikatregistrierungspunkt. Geben Sie auch die Zertifizierungsstelle (Certificate Authority – CA) für das Zertifikat und die notwendigen Anmeldeinformationen an. Sie können entweder Microsoft oder Entrust als Zertifizierungsstelle angeben.  

Weitere Informationen zur Unterstützung von Richtlinienmodulen durch das SCEP, damit Configuration Manager Zertifikate bereitstellen kann, finden Sie unter [Verwenden eines Richtlinienmoduls mit dem Simple Certificate Enrollment-Protokoll](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn473016\(v=ws.11\)).

Configuration Manager unterstützt die anforderungs-, gerätetyp- und betriebssystemabhängige Bereitstellung von Zertifikaten für unterschiedliche Zertifikatspeicher. Folgende Geräte und Betriebssysteme werden unterstützt:  

- Windows 10

- Windows 10 Mobile

- Windows 8.1  

- Windows Phone 8.1  

> [!NOTE]  
> Verwenden Sie die lokale Verwaltung mobiler Geräte von Configuration Manager, um Windows Phone 8.1 und Windows 10 Mobile zu verwalten. Weitere Informationen finden Sie unter [Lokale Verwaltung mobiler Geräte](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).

Ein typisches Szenario für Configuration Manager ist die Installation vertrauenswürdiger Zertifikate einer Stammzertifizierungsstelle zur Authentifizierung von WLAN- und VPN-Servern. Typische Verbindungen verwenden die folgenden Protokolle:

- Authentifizierungsprotokolle: EAP-TLS, EAP-TTLS und PEAP
- VPN-Tunneling-Protokolle: IKEv2, L2TP/IPsec und Cisco IPsec

Ein Zertifikat einer Stammzertifizierungsstelle des Unternehmens muss auf dem Gerät installiert sein. Nur dann können vom Gerät mithilfe eines SCEP-Zertifikatprofils Zertifikate angefordert werden.  

Sie können Einstellungen in einem SCEP-Zertifikatprofil angeben, um benutzerdefinierte Zertifikate für unterschiedliche Umgebungen oder Verbindungsanforderungen anzufordern. Der **Assistent zum Erstellen von Zertifikatprofilen** verfügt über zwei Seiten für Parameter für die Anmeldung. Die erste Seite **SCEP-Anmeldung** enthält Einstellungen für die Anmeldeanforderung sowie zum Installationsort des Zertifikats. Auf der zweiten Seite **Zertifikateigenschaften**wird das angeforderte Zertifikat beschrieben.  

## <a name="deploy"></a>Bereitstellen

Wenn Sie ein SCEP-Zertifikatprofil bereitstellen, verarbeitet der Configuration Manager-Client die Richtlinie. Anschließend fordert er vom Verwaltungspunkt ein SCEP-Abfragekennwort an. Das Gerät erstellt ein Schlüsselpaar aus öffentlichem und privatem Schlüssel und erzeugt eine Zertifikatsignieranforderung (CSR). Diese Anforderung wird an den NDES-Server gesendet. Der NDES-Server leitet die Anforderung über das NDES-Richtlinienmodul an das Standortsystem für den Zertifikatregistrierungspunkt weiter. Der Zertifikatregistrierungspunkt überprüft die Anforderung, prüft das SCEP-Abfragekennwort und verifiziert, dass die Anforderung nicht manipuliert wurde. Er genehmigt dann die Anforderung oder lehnt sie ab. Falls genehmigt, sendet der NDES-Server die Signieranforderung zum Signieren an die verbundene Zertifizierungsstelle (CA). Die Zertifizierungsstelle signiert die Anforderung und sendet das Zertifikat dann an das anfordernde Gerät zurück.

Stellen Sie Zertifikatprofile für Benutzer- oder Gerätesammlungen bereit. Sie können den Zielspeicher für jedes Zertifikat angeben. Die Anwendbarkeitsregeln bestimmen, ob das Gerät das Zertifikat installieren kann.

Beim Bereitstellen von Zertifikatprofilen für Benutzersammlungen wird durch die [Affinität zwischen Benutzer und Gerät](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md) bestimmt, auf welchen Geräten der Benutzer die Zertifikate installiert werden. Wenn Sie ein Zertifikatprofil mit einem Benutzerzertifikat für eine Gerätesammlung bereitstellen, werden die Zertifikate standardmäßig auf jedem der primären Geräte der Benutzer installiert. Das Verhalten, dass das Zertifikat auf allen Geräten der Benutzer bereitgestellt wird, können Sie auf der Seite **SCEP-Anmeldung** des **Assistenten zum Erstellen von Zertifikatprofilen** ändern. Wenn sich die Geräte in einer Arbeitsgruppe befinden, stellt Configuration Manager keine Benutzerzertifikate bereit.  

## <a name="monitor"></a>Überwachen

Sie können Zertifikatprofilbereitstellungen überwachen, indem Sie Konformitätsergebnisse oder -berichte anzeigen. Weitere Informationen finden Sie unter [Überwachen von Zertifikatprofilen](monitor-certificate-profiles.md).

## <a name="automatic-revocation"></a>Automatische Sperrung

Configuration Manager widerruft automatisch Benutzer- und Computerzertifikate, die unter den folgenden Umständen mithilfe von Zertifikatprofilen erstellt wurden:  

- Die Verwaltung in Configuration Manager wurde für dieses Gerät außer Kraft gesetzt.  

- Das Gerät wurde in der Configuration Manager-Hierarchie gesperrt.  

Zum Sperren der Zertifikate wird vom Standortserver ein Sperrbefehl an die ausstellende Zertifizierungsstelle gesendet. Der Grund für die Sperre ist **Vorgangsende**.

> [!NOTE]
> Um ein Zertifikat ordnungsgemäß zu sperren, benötigt das Computerkonto für die Site auf oberster Hierarchieebene die Erlaubnis, **Zertifikate** bei der Zertifizierungsstelle auszustellen und zu verwalten.
>
> Sie können zur Verbesserung der Sicherheit auch Zertifizierungsstellen-Manager für die Zertifizierungsstelle einschränken. Geben Sie diesem Konto dann nur Berechtigungen für die spezifische Zertifikatvorlage, die Sie für die SCEP-Profile auf der Site verwenden.

## <a name="next-steps"></a>Nächste Schritte

- [Erstellen von Zertifikatprofilen](create-certificate-profiles.md)

- [Konfigurieren der Zertifikatinfrastruktur](certificate-infrastructure.md)
