---
title: Erstellen von VPN-Profilen
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie VPN-Profile in Configuration Manager erstellen.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f338e4db-73b5-45ff-92f4-1b89a8ded989
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 17811d0bb0b72ebee6879d5dab90e165b439081b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694248"
---
# <a name="how-to-create-vpn-profiles-in-configuration-manager"></a>Erstellen von VPN-Profilen in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Configuration Manager unterstützt mehrere VPN-Verbindungstypen. Weitere Informationen zu den für die verschiedenen Geräteplattformen verfügbaren Verbindungstypen finden Sie unter [VPN-Profile](vpn-profiles.md).

Wenn Sie VPN-Lösungen von Drittanbietern verwenden möchten, müssen Sie die entsprechende VPN-App verteilen, bevor Sie das VPN-Profil bereitstellen. Wenn Sie die App nicht bereitstellen, werden die Benutzer dazu aufgefordert, sobald sie versuchen, sich mit dem VPN zu verbinden. Weitere Informationen finden Sie unter [Bereitstellen von Anwendungen](../../apps/deploy-use/deploy-applications.md).

## <a name="create-a-vpn-profile"></a>Erstellen eines VPN-Profils

1. Öffnen Sie in der Configuration Manager-Konsole den Arbeitsbereich **Assets und Konformität**, erweitern Sie **Konformitätseinstellungen** sowie **Zugriff auf Unternehmensressourcen**, und klicken Sie auf den Knoten **VPN-Profile**.

1. Wählen Sie auf der Registerkarte **Start** des Menübands in der Gruppe **Erstellen** die Option **VPN-Profil erstellen** aus.

1. Geben Sie auf der Seite **Allgemein** des Assistenten zum Erstellen von VPN-Profilen die folgenden Informationen an:

    - **Name:** Geben Sie einen eindeutigen Namen ein, um das VPN-Profil in der-Konsole identifizieren zu können.

        > [!NOTE]
        > Verwenden Sie im Namen des VPN-Profils nicht die folgenden Zeichen: `\/:*?<>|; `. Das Windows-VPN-Profil unterstützt diese Sonderzeichen nicht.

    - **Beschreibung:** Sie können eine Beschreibung eingeben, um weitere Informationen zum VPN-Profil bereitzustellen.

    - **VPN-Profiltyp**: Wählen Sie die entsprechende Plattform aus.

        Wenn Sie die **Windows 8.1** als Plattform auswählen, können Sie auch die Option **Aus Datei importieren** aktivieren. Das bedeutet, dass die VPN-Profilinformationen aus einer XML-Datei importiert werden. Wenn Sie diese Option auswählen, werden im Assistenten nur noch die folgenden Seiten angezeigt: **Unterstützte Plattformen** und **VPN-Profil importieren**.

1. Wählen Sie auf der Seite **Unterstützte Plattformen** die Betriebssystemversionen aus, die vom VPN-Profil unterstützt werden.

1. Geben Sie auf der Seite **Verbindung** die folgenden Informationen an:

    - **Verbindungstyp:** Wählen Sie den VPN-Verbindungstyp aus. Weitere Informationen zu den unterstützten Typen finden Sie unter [VPN-Profile](vpn-profiles.md).

    - **Serverliste**: Fügen Sie einen neuen Server zur Verwendung für die VPN-Verbindung hinzu. Abhängig vom Verbindungstyp können Sie einen oder mehrere VPN-Server hinzufügen und den Standardserver angeben.

    - **VPN umgehen, wenn eine Verbindung mit dem Unternehmensnetzwerk besteht**: Konfigurieren Sie Clients so, dass das VPN nicht verwendet wird, wenn sie sich im internen Netzwerk befinden. Geben Sie gegebenenfalls einen verbindungsspezifischen DNS-Namen an.

1. Wählen Sie auf der Seite **Authentifizierungsmethode** des Assistenten eine Methode aus, die vom Verbindungstyp unterstützt wird. Die Einstellungen und verfügbaren Optionen auf dieser Seite variieren je nach ausgewähltem Verbindungstyp. Weitere Informationen finden Sie unter [Referenz zur Authentifizierungsmethode](#bkmk_auth).

1. Wenn Ihr VPN einen Proxyserver verwendet, wählen Sie auf der Seite **Proxyeinstellungen** die für Ihre Umgebung geeignete Option aus. Geben Sie dann die Konfigurationsinformationen für den Proxy an.

1. Die Seite **Anwendungen** gilt nur für Windows 10-Profile. Fügen Sie Desktop-Apps und universelle Apps hinzu, die automatisch eine Verbindung mit diesem VPN herstellen. Der App-Typ bestimmt die App-ID:

    - *Desktop-App*: Geben Sie den Dateipfad der App an.

    - *Universelle App*: Geben Sie den PFN (package family name; Paketfamiliennamen) an. Informationen dazu, wie Sie den PFN einer App herausfinden, finden Sie unter [Find a package family name for per-app VPN (Suchen eines Paktefamiliennamens für Pro-App-VPN)](find-a-pfn-for-per-app-vpn.md).

    Sie können auch die Option **Nur die aufgeführten Apps können dieses VPN verwenden** aktivieren.

    > [!IMPORTANT]
    > Sichern Sie alle Listen zugeordneter Apps, die Sie für die Konfiguration eines Pro-App-VPN zusammenstellen. Wenn ein nicht autorisierter Benutzer die Liste ändert und Sie sie in die Liste für ein Pro-App-VPN importieren, gewähren Sie möglicherweise Apps VPN-Zugriff, die keinen Zugriff erhalten sollten.

1. Die Seite **Begrenzungen** zum Konfigurieren von VPN-Grenzen gilt nur für Windows 10-Profile. Sie können die folgenden Optionen hinzufügen:

    - **Network traffic rules** (Regeln für den Netzwerkdatenverkehr): Legen Sie die Protokolle, die lokalen Ports und Remoteports sowie die Adressbereiche fest, die für die VPN-Verbindung aktiviert werden sollen.  

        > [!Note]
        > Wenn Sie keine Regel für den Netzwerkdatenverkehr erstellen, werden alle Protokolle, Ports und Adressbereiche aktiviert. Nachdem Sie eine Regel erstellt haben, werden nur die in dieser oder weiteren Regeln festgelegten Protokolle, Ports und Adressbereiche von der VPN-Verbindung verwendet.

    - **DNS-Namen und -Server**: DNS-Server, die von der VPN-Verbindung verwendet werden, nachdem das Gerät die Verbindung hergestellt hat.

    - **Routen**: Netzwerkrouten, die die VPN-Verbindung verwenden. Die Erstellung von mehr als 60 Routen kann Richtlinienfehler herbeiführen.

1. Schließen Sie den Assistenten ab.

Das neue VPN-Profil wird im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **VPN-Profile** angezeigt.

## <a name="authentication-method-reference"></a><a name="bkmk_auth"></a>Referenz zur Authentifizierungsmethode

Welche VPN-Authentifizierungsmethoden verfügbar sind, hängt vom Verbindungstyp ab:

### <a name="certificates"></a>Zertifikate

Wenn für die Authentifizierung bei einem RADIUS-Server, wie z.B. einem Netzwerkrichtlinienserver, ein Clientzertifikat verwendet wird, legen Sie den alternativen Antragstellernamen im Zertifikat auf den Benutzerprinzipalnamen fest.

Unterstützte Verbindungstypen:

- Pulse Secure
- F5 Edge Client
- Dell SonicWALL Mobile Connect
- Prüfpunkt für mobiles VPN

### <a name="username-and-password"></a>Benutzername und Kennwort

Unterstützte Verbindungstypen:

- Pulse Secure
- F5 Edge Client
- Dell SonicWALL Mobile Connect
- Prüfpunkt für mobiles VPN

### <a name="microsoft-eap-ttls"></a>Microsoft EAP-TTLS

Unterstützte Verbindungstypen:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- PPTP
- IKEv2
- L2TP

### <a name="microsoft-protected-eap-peap"></a>Von Microsoft geschütztes EAP (PEAP)

Unterstützte Verbindungstypen:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="microsoft-secured-password-eap-mschap-v2"></a>Microsoft-gesichertes Kennwort (EAP-MSCHAP v2)

Unterstützte Verbindungstypen:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="smart-card-or-other-certificate"></a>Smartcard- oder anderes Zertifikat

Unterstützte Verbindungstypen:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="mschap-v2"></a>MSCHAP v2

Unterstützte Verbindungstypen:

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="use-machine-certificates"></a>Computerzertifikate verwenden

Unterstützte Verbindungstypen:

- IKEv2

### <a name="additional-authentication-options"></a>Zusätzliche Authentifizierungsoptionen

Die Option zum **Konfigurieren** der Authentifizierungsmethode ist verfügbar, wenn die Windows-Clientversion diese unterstützt. Diese Option öffnet das Dialogfeld „Windows-Eigenschaften“, in dem Sie die Authentifizierungsmethode konfigurieren können.

Je nach ausgewählten Optionen werden Sie möglicherweise aufgefordert, weitere Informationen wie beispielsweise die folgenden anzugeben:

- **Benutzeranmeldeinformationen bei jeder Anmeldung speichern**: Geben Sie die Benutzeranmeldeinformationen ein, die gespeichert werden sollen, damit die Benutzer sie nicht bei jeder Verbindung noch mal eingeben müssen.  

- **Clientzertifikat für Clientauthentifizierung auswählen**: Wählen Sie ein zuvor erstelltes Client-SCEP-Zertifikatsprofil aus, um die VPN-Verbindung zu authentifizieren. Weitere Informationen finden Sie unter [Erstellen von PFX-Zertifikatprofilen](create-certificate-profiles.md).

## <a name="next-steps"></a>Nächste Schritte

- Wenn Sie VPN-Lösungen von Drittanbietern verwenden möchten, müssen Sie die entsprechende VPN-App verteilen, bevor Sie das VPN-Profil bereitstellen. Wenn Sie die App nicht bereitstellen, werden die Benutzer dazu aufgefordert, sobald sie versuchen, sich mit dem VPN zu verbinden. Weitere Informationen finden Sie unter [Bereitstellen von Anwendungen](../../apps/deploy-use/deploy-applications.md).

- Stellen Sie das VPN-Profil bereit. Weitere Informationen finden Sie unter [Bereitstellen von Profilen](deploy-wifi-vpn-email-cert-profiles.md).
