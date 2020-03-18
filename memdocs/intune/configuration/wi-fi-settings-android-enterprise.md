---
title: WLAN-Einstellungen für Android Enterprise- und Kioskgeräte – Microsoft Intune | Microsoft-Dokumentation
description: Erstellen Sie ein WLAN-Gerätekonfigurationsprofils für Android Enterprise- und Android-Kioskgeräte, oder fügen Sie eines hinzu. Erfahren Sie mehr über die verschiedenen Einstellungen, z.B., wie Sie Zertifikate hinzufügen oder einen EAP-Typ bzw. eine Authentifizierungsmethode in Microsoft Intune auswählen. Geben Sie für Kioskgeräte außerdem den vorinstallierten Schlüssel Ihres Netzwerks ein.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/26/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: maholdaa
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 718ca1a6b17ff967df2267aa9f9b27cd2d5980a6
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79343179"
---
# <a name="add-wi-fi-settings-for-android-enterprise-dedicated-and-fully-managed-devices-in-microsoft-intune"></a>Hinzufügen von WLAN-Einstellungen für dedizierte und vollständig verwaltete Android Enterprise-Geräte in Microsoft Intune

Sie können ein Profil mit bestimmten WLAN-Einstellungen erstellen und dieses dann auf Ihren vollständig verwalteten Android Enterprise- und dedizierten Geräten bereitstellen. Microsoft Intune bietet viele Features, darunter die Authentifizierung bei Ihrem Netzwerk mit einem vorinstallierten Schlüssel.

Dieser Artikel beschreibt diese Einstellungen. [Hinzufügen und Verwenden von WLAN-Einstellungen auf Microsoft Intune-Geräten](wi-fi-settings-configure.md) enthält weitere Informationen über die WLAN-Funktion in Microsoft Intune.

## <a name="before-you-begin"></a>Vorbereitung

[Erstellen Sie ein Geräteprofil.](wi-fi-settings-configure.md#create-a-device-profile)

## <a name="device-owner-only"></a>Nur Gerätebesitzer

Diese Option eignet sich für das Bereitstellen auf einem dedizierten oder vollständig verwalteten Android Enterprise-Gerät.  Für dedizierte und vollständig verwaltete Android Enterprise-Geräte wird derzeit die SCEP-Zertifikatbereitstellung unterstützt, jedoch nicht die Bereitstellung mit PKCS-Zertifikaten.

### <a name="basic"></a>Einfach

- **WLAN-Typ**: Wählen Sie **Standard**.
- **Netzwerkname**: Geben Sie einen Namen für diese WLAN-Verbindung ein. Benutzern wird dieser Name angezeigt, wenn sie auf ihrem Gerät die verfügbaren WLAN-Verbindungen durchsuchen. Geben Sie z.B. **Contoso WiFi** ein.
- **SSID**: Geben Sie den **Service Set Identifier** ein. Dabei handelt es sich um den tatsächlichen Namen des Drahtlosnetzwerks, mit dem Geräte eine Verbindung herstellen. Den Benutzern wird beim Auswählen der Verbindung jedoch nur der **Netzwerkname** angezeigt, den Sie konfiguriert haben.
- **Ausgeblendetes Netzwerk**: Wählen Sie **Aktivieren** aus, um dieses Netzwerk in der Liste der verfügbaren Netzwerke auf dem Gerät auszublenden. Die SSID wird nicht übertragen. Wählen Sie **Deaktivieren** aus, um dieses Netzwerk in der Liste der verfügbaren Netzwerke auf dem Gerät anzuzeigen.
- **WLAN-Typ**: Wählen Sie das Sicherheitsprotokoll zur Authentifizierung beim WLAN-Netzwerk aus. Folgende Optionen sind verfügbar:

  - **Offen (keine Authentifizierung)** : Verwenden Sie diese Option nur, wenn das Netzwerk nicht gesichert ist.
  - **Vorinstallierter WEP-Schlüssel**: Geben Sie das Kennwort unter **Vorinstallierter Schlüssel** ein. Wenn das Netzwerk Ihrer Organisation eingerichtet oder konfiguriert wird, wird auch ein Kennwort oder ein Netzwerkschlüssel konfiguriert. Geben Sie dieses Kennwort oder den Netzwerkschlüssel für den Wert des vorinstallierten Schlüssels ein.
  - **Vorinstallierter WPA-Schlüssel**: Geben Sie das Kennwort unter **Vorinstallierter Schlüssel** ein. Wenn das Netzwerk Ihrer Organisation eingerichtet oder konfiguriert wird, wird auch ein Kennwort oder ein Netzwerkschlüssel konfiguriert. Geben Sie dieses Kennwort oder den Netzwerkschlüssel für den Wert des vorinstallierten Schlüssels ein.

### <a name="enterprise"></a>Enterprise

- **WLAN-Typ**: Wählen Sie **Unternehmen** aus.
- **SSID**: Geben Sie den **Service Set Identifier** ein. Dabei handelt es sich um den tatsächlichen Namen des Drahtlosnetzwerks, mit dem Geräte eine Verbindung herstellen. Den Benutzern wird beim Auswählen der Verbindung jedoch nur der **Netzwerkname** angezeigt, den Sie konfiguriert haben.
- **Ausgeblendetes Netzwerk**: Wählen Sie **Aktivieren** aus, um dieses Netzwerk in der Liste der verfügbaren Netzwerke auf dem Gerät auszublenden. Die SSID wird nicht übertragen. Wählen Sie **Deaktivieren** aus, um dieses Netzwerk in der Liste der verfügbaren Netzwerke auf dem Gerät anzuzeigen.
- **EAP-Typ**: Wählen Sie die den EAP-Typ (Extensible Authentication-Protokoll) zur Authentifizierung von gesicherten Drahtlosverbindungen aus. Folgende Optionen sind verfügbar:

  - **EAP-TLS**: Geben Sie außerdem Folgendes ein:

    - **Serververtrauensstellung** - **Stammzertifikat zur Servervalidierung**: Wählen Sie ein vorhandenes, vertrauenswürdiges Stammzertifikatprofil aus. Wenn sich der Client mit dem Netzwerk verbindet, wird dieses Zertifikat dem Server bereitgestellt und zur Authentifizierung der Verbindung verwendet.

    - **Clientauthentifizierung** - **Clientzertifikat zur Clientauthentifizierung (Identitätszertifikat)** : Wählen Sie das SCEP-Clientzertifikatprofil aus, das auch auf dem Gerät bereitgestellt wird. Dieses Zertifikat ist die Identität, die das Gerät dem Server zur Authentifizierung der Verbindung bereitstellt.

    - **Identitätsschutz (äußere Identität)** : Geben Sie den Text ein, der als Antwort auf eine EAP-Identitätsanforderung gesendet werden soll. Dieser Text kann einen beliebigen Wert haben, z.B. `anonymous`. Während der Authentifizierung wird zuerst diese anonyme Identität gesendet und anschließend die echte Kennung über einen sicheren Tunnel.

  - **EAP-TTLS**: Geben Sie außerdem Folgendes ein:

    - **Serververtrauensstellung** - **Stammzertifikat zur Servervalidierung**: Wählen Sie ein vorhandenes, vertrauenswürdiges Stammzertifikatprofil aus. Wenn sich der Client mit dem Netzwerk verbindet, wird dieses Zertifikat dem Server bereitgestellt und zur Authentifizierung der Verbindung verwendet.

    - **Clientauthentifizierung:** Wählen Sie eine **Authentifizierungsmethode** aus. Folgende Optionen sind verfügbar:

      - **Benutzername und Kennwort**: Fordern Sie den Benutzer zur Eingabe des Benutzernamens und Kennworts für die Authentifizierung der Verbindung auf. Geben Sie außerdem Folgendes ein:
        - **Nicht-EAP-Methode (innere Identität)** : Wählen Sie aus, wie Sie die Verbindung authentifizieren möchten. Achten Sie darauf, dass Sie das gleiche Protokoll auswählen, das auch in Ihrem WLAN konfiguriert ist. Folgende Optionen sind verfügbar:

          - **Unverschlüsseltes Kennwort (PAP)**
          - **Microsoft CHAP (MS-CHAP)**
          - **Microsoft CHAP, Version 2 (MS-CHAP v2)**

      - **Zertifikate:** Wählen Sie das SCEP-Clientzertifikatprofil aus, das auch auf dem Gerät bereitgestellt wird. Dieses Zertifikat ist die Identität, die das Gerät dem Server zur Authentifizierung der Verbindung bereitstellt.

      - **Identitätsschutz (äußere Identität)** : Geben Sie den Text ein, der als Antwort auf eine EAP-Identitätsanforderung gesendet werden soll. Dieser Text kann einen beliebigen Wert haben, z.B. `anonymous`. Während der Authentifizierung wird zuerst diese anonyme Identität gesendet und anschließend die echte Kennung über einen sicheren Tunnel.

  - **PEAP**: Geben Sie außerdem Folgendes ein:

    - **Serververtrauensstellung** - **Stammzertifikat zur Servervalidierung**: Wählen Sie ein vorhandenes, vertrauenswürdiges Stammzertifikatprofil aus. Wenn sich der Client mit dem Netzwerk verbindet, wird dieses Zertifikat dem Server bereitgestellt und zur Authentifizierung der Verbindung verwendet.

    - **Clientauthentifizierung:** Wählen Sie eine **Authentifizierungsmethode** aus. Folgende Optionen sind verfügbar:

      - **Benutzername und Kennwort**: Fordern Sie den Benutzer zur Eingabe des Benutzernamens und Kennworts für die Authentifizierung der Verbindung auf. Geben Sie außerdem Folgendes ein:
        - **Nicht-EAP-Authentifizierungsmethode (innere Identität)** : Wählen Sie aus, wie Sie die Verbindung authentifizieren möchten. Achten Sie darauf, dass Sie das gleiche Protokoll auswählen, das auch in Ihrem WLAN konfiguriert ist. Folgende Optionen sind verfügbar:

          - **Keine**
          - **Microsoft CHAP, Version 2 (MS-CHAP v2)**

      - **Zertifikate:** Wählen Sie das SCEP-Clientzertifikatprofil aus, das auch auf dem Gerät bereitgestellt wird. Dieses Zertifikat ist die Identität, die das Gerät dem Server zur Authentifizierung der Verbindung bereitstellt.

      - **Identitätsschutz (äußere Identität)** : Geben Sie den Text ein, der als Antwort auf eine EAP-Identitätsanforderung gesendet werden soll. Dieser Text kann einen beliebigen Wert haben, z.B. `anonymous`. Während der Authentifizierung wird zuerst diese anonyme Identität gesendet und anschließend die echte Kennung über einen sicheren Tunnel.

## <a name="work-profile-only"></a>Nur Arbeitsprofil

### <a name="basic"></a>Einfach

- **WLAN-Typ**: Wählen Sie **Standard**.
- **SSID**: Geben Sie den **Service Set Identifier** ein. Dabei handelt es sich um den tatsächlichen Namen des Drahtlosnetzwerks, mit dem Geräte eine Verbindung herstellen. Den Benutzern wird beim Auswählen der Verbindung jedoch nur der **Netzwerkname** angezeigt, den Sie konfiguriert haben.
- **Ausgeblendetes Netzwerk**: Wählen Sie **Aktivieren** aus, um dieses Netzwerk in der Liste der verfügbaren Netzwerke auf dem Gerät auszublenden. Die SSID wird nicht übertragen. Wählen Sie **Deaktivieren** aus, um dieses Netzwerk in der Liste der verfügbaren Netzwerke auf dem Gerät anzuzeigen.

### <a name="enterprise"></a>Enterprise

- **WLAN-Typ**: Wählen Sie **Unternehmen** aus.
- **SSID**: Geben Sie den **Service Set Identifier** ein. Dabei handelt es sich um den tatsächlichen Namen des Drahtlosnetzwerks, mit dem Geräte eine Verbindung herstellen. Den Benutzern wird beim Auswählen der Verbindung jedoch nur der **Netzwerkname** angezeigt, den Sie konfiguriert haben.
- **Ausgeblendetes Netzwerk**: Wählen Sie **Aktivieren** aus, um dieses Netzwerk in der Liste der verfügbaren Netzwerke auf dem Gerät auszublenden. Die SSID wird nicht übertragen. Wählen Sie **Deaktivieren** aus, um dieses Netzwerk in der Liste der verfügbaren Netzwerke auf dem Gerät anzuzeigen.
- **EAP-Typ**: Wählen Sie die den EAP-Typ (Extensible Authentication-Protokoll) zur Authentifizierung von gesicherten Drahtlosverbindungen aus. Folgende Optionen sind verfügbar:

  - **EAP-TLS**: Geben Sie außerdem Folgendes ein:

    - **Serververtrauensstellung** - **Stammzertifikat zur Servervalidierung**: Wählen Sie ein vorhandenes, vertrauenswürdiges Stammzertifikatprofil aus. Wenn sich der Client mit dem Netzwerk verbindet, wird dieses Zertifikat dem Server bereitgestellt und zur Authentifizierung der Verbindung verwendet.

    - **Clientauthentifizierung** - **Clientzertifikat zur Clientauthentifizierung (Identitätszertifikat)** : Wählen Sie das SCEP- oder PKCS-Clientzertifikatprofil aus, das auch auf dem Gerät bereitgestellt wird. Dieses Zertifikat ist die Identität, die das Gerät dem Server zur Authentifizierung der Verbindung bereitstellt.

    - **Identitätsschutz (äußere Identität)** : Geben Sie den Text ein, der als Antwort auf eine EAP-Identitätsanforderung gesendet werden soll. Dieser Text kann einen beliebigen Wert haben, z.B. `anonymous`. Während der Authentifizierung wird zuerst diese anonyme Identität gesendet und anschließend die echte Kennung über einen sicheren Tunnel.

  - **EAP-TTLS**: Geben Sie außerdem Folgendes ein:

    - **Serververtrauensstellung** - **Stammzertifikat zur Servervalidierung**: Wählen Sie ein vorhandenes, vertrauenswürdiges Stammzertifikatprofil aus. Wenn sich der Client mit dem Netzwerk verbindet, wird dieses Zertifikat dem Server bereitgestellt und zur Authentifizierung der Verbindung verwendet.

    - **Clientauthentifizierung:** Wählen Sie eine **Authentifizierungsmethode** aus. Folgende Optionen sind verfügbar:

      - **Benutzername und Kennwort**: Fordern Sie den Benutzer zur Eingabe des Benutzernamens und Kennworts für die Authentifizierung der Verbindung auf. Geben Sie außerdem Folgendes ein:
        - **Nicht-EAP-Methode (innere Identität)** : Wählen Sie aus, wie Sie die Verbindung authentifizieren möchten. Achten Sie darauf, dass Sie das gleiche Protokoll auswählen, das auch in Ihrem WLAN konfiguriert ist. Folgende Optionen sind verfügbar:

          - **Unverschlüsseltes Kennwort (PAP)**
          - **Microsoft CHAP (MS-CHAP)**
          - **Microsoft CHAP, Version 2 (MS-CHAP v2)**

      - **Zertifikate:** Wählen Sie das SCEP- oder PKCS-Clientzertifikatprofil aus, das auch auf dem Gerät bereitgestellt wird. Dieses Zertifikat ist die Identität, die das Gerät dem Server zur Authentifizierung der Verbindung bereitstellt.

      - **Identitätsschutz (äußere Identität)** : Geben Sie den Text ein, der als Antwort auf eine EAP-Identitätsanforderung gesendet werden soll. Dieser Text kann einen beliebigen Wert haben, z.B. `anonymous`. Während der Authentifizierung wird zuerst diese anonyme Identität gesendet und anschließend die echte Kennung über einen sicheren Tunnel.

  - **PEAP**: Geben Sie außerdem Folgendes ein:

    - **Serververtrauensstellung** - **Stammzertifikat zur Servervalidierung**: Wählen Sie ein vorhandenes, vertrauenswürdiges Stammzertifikatprofil aus. Wenn sich der Client mit dem Netzwerk verbindet, wird dieses Zertifikat dem Server bereitgestellt und zur Authentifizierung der Verbindung verwendet.

    - **Clientauthentifizierung:** Wählen Sie eine **Authentifizierungsmethode** aus. Folgende Optionen sind verfügbar:

      - **Benutzername und Kennwort**: Fordern Sie den Benutzer zur Eingabe des Benutzernamens und Kennworts für die Authentifizierung der Verbindung auf. Geben Sie außerdem Folgendes ein:
        - **Nicht-EAP-Authentifizierungsmethode (innere Identität)** : Wählen Sie aus, wie Sie die Verbindung authentifizieren möchten. Achten Sie darauf, dass Sie das gleiche Protokoll auswählen, das auch in Ihrem WLAN konfiguriert ist. Folgende Optionen sind verfügbar:

          - **Keine**
          - **Microsoft CHAP, Version 2 (MS-CHAP v2)**

      - **Zertifikate:** Wählen Sie das SCEP- oder PKCS-Clientzertifikatprofil aus, das auch auf dem Gerät bereitgestellt wird. Dieses Zertifikat ist die Identität, die das Gerät dem Server zur Authentifizierung der Verbindung bereitstellt.

      - **Identitätsschutz (äußere Identität)** : Geben Sie den Text ein, der als Antwort auf eine EAP-Identitätsanforderung gesendet werden soll. Dieser Text kann einen beliebigen Wert haben, z.B. `anonymous`. Während der Authentifizierung wird zuerst diese anonyme Identität gesendet und anschließend die echte Kennung über einen sicheren Tunnel.

- **Proxyeinstellungen:** Legen Sie die Proxykonfiguration fest, die von Ihrer Organisation verwendet wird. Folgende Optionen sind verfügbar:

  - **Keine:** Sie verwenden keinen Proxyserver.
  - **Automatisch:** Wählen Sie diese Option aus, um die Einstellung für die *Proxyserver-URL* zur Verfügung zu stellen, mit der Sie den Proxyserver oder eine Datei für die automatische Proxykonfiguration (Proxy Auto-Configuration, PAC) angeben, die eine Liste Ihrer Proxyserver enthält.

- **Proxyserver-URL:** Diese Einstellung ist verfügbar, wenn Sie die *Proxyeinstellungen* auf *Automatisch* festlegen. Geben Sie eine der folgenden Optionen an, um Geräte an Ihren Proxyserver weiterzuleiten:

  - IP-Adresse. Beispiel: `10.0.0.11`
  - Eine URL. Beispiel: `http://proxyserver.contoso.com`.
  - Die URL einer PAC-Datei. Beispiel: `http://proxy.contoso.com/proxy.pac`.

  Weitere Informationen zu PAC-Dateien finden Sie unter [Proxy Auto-Configuration (PAC) file (Datei für die automatische Proxykonfiguration)](https://developer.mozilla.org/docs/Web/HTTP/Proxy_servers_and_tunneling/Proxy_Auto-Configuration_(PAC)_file) (öffnet eine Drittanbieterwebsite).

## <a name="next-steps"></a>Nächste Schritte

Das Profil ist nun erstellt. Die nächsten Schritte sind das [Zuweisen dieses Profils](device-profile-assign.md) und das [Überwachen seines Status](device-profile-monitor.md).

Sie können WLAN-Profile auch für Geräte erstellen, die unter [Android](wi-fi-settings-android.md), [iOS/iPadOS](wi-fi-settings-ios.md), [macOS](wi-fi-settings-macos.md), [Windows 10](wi-fi-settings-windows.md) und [Windows 8.1](wi-fi-settings-import-windows-8-1.md) ausgeführt werden.
