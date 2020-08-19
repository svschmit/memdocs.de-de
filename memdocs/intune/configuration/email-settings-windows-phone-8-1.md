---
title: Microsoft Intune-E-Mail-Einstellungen für Windows Phone 8.1
titleSuffix: ''
description: In diesem Artikel erhalten Sie Informationen zu den Intune-Einstellungen, die Sie zum Konfigurieren von E-Mail-Verbindungen auf Windows Phone 8.1-Geräten verwenden können.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ROBOTS: NOINDEX
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f5bd00f12ab0f015c6408e2bbc934e1320c7540e
ms.sourcegitcommit: 8999e197f10fb72d1b82f30a599d1e588db237b7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88146139"
---
# <a name="email-profile-settings-in-microsoft-intune-for-devices-running-windows-phone-81"></a>E-Mail-Profileinstellungen in Microsoft Intune für Windows Phone 8.1-Geräte

[!INCLUDE [windows-phone-81-windows-10-mobile-support](../includes/windows-phone-81-windows-10-mobile-support.md)]

In diesem Artikel werden die E-Mail-Profileinstellungen dargestellt, die Sie für Ihre Windows Phone 8.1-Geräte konfigurieren können.

>[!IMPORTANT]
>Windows Phone 8.1-E-Mail-Profile werden auch auf Windows 10-Geräte angewendet.

## <a name="before-you-begin"></a>Vorbereitung

[Erstellen Sie ein Windows Phone 8.1-E-Mail-Profil](email-settings-configure.md).

## <a name="email-settings"></a>E-Mail-Einstellungen

- **E-Mail-Server**: Geben Sie den Hostnamen Ihres Exchange-Servers ein. Geben Sie beispielsweise `outlook.office365.com` ein.
- **Kontoname**: Geben Sie den Anzeigenamen des E-Mail-Kontos ein. Dieser Name wird Benutzern auf ihren Geräten angezeigt.
- **Benutzernamensattribut aus AAD**: Dieser Name ist das Attribut, dass Intune aus Azure Active Directory (AAD) abruft. Intune generiert dynamisch den Benutzernamen, der von diesem Profil verwendet wird. Folgende Optionen sind verfügbar:
  - **Benutzerprinzipalname**: Hiermit wird der Name abgerufen, z. B. `user1` oder `user1@contoso.com`.
  - **Primäre SMTP-Adresse**: Ruft den Namen im Format einer E-Mail-Adresse ab, z. B. `user1@contoso.com`.
  - **SAM-Kontoname**: Erfordert die Domäne, z.B. `domain\user1`. Geben Sie außerdem Folgendes ein:
    - **Quelle für Benutzerdomänenname**: Folgende Optionen sind verfügbar:
      - **AAD** (Azure Active Directory): Geben Sie **Attribut für Benutzerdomänenname aus AAD** ein. Rufen Sie entweder das Attribut **Vollständiger Domänenname** oder das Attribut **NetBIOS-Name** des Benutzers ab.
      - **Benutzerdefiniert**: Geben Sie **Zu verwendender benutzerdefinierter Domänenname** ein. Geben Sie einen Wert ein, den Intune als Domänennamen verwenden kann, z. B. `contoso.com` oder `contoso`.

- **Attribut für E-Mail-Adresse aus AAD**: Intune ruft dieses Attribut aus Azure Active Directory (AAD) ab. Wählen Sie aus, wie die E-Mail-Adresse für den Benutzer generiert wird. Folgende Optionen sind verfügbar:
  - **Benutzerprinzipalname**: Der vollständige Prinzipalname, z. B. `user1@contoso.com` oder `user1`, wird als E-Mail-Adresse verwendet.
  - **Primäre SMTP-Adresse**: Verwendet die primäre SMTP-Adresse, z. B. `user1@contoso.com`, für die Anmeldung bei Exchange.

## <a name="security-settings"></a>Sicherheitseinstellungen

- **SSL**: Mit der Option **Aktivieren** wird die SSL-Kommunikation (Secure Sockets Layer) beim Senden und Empfangen von E-Mails sowie bei der Kommunikation mit dem Exchange-Server verwendet. **Deaktivieren** macht SSL überflüssig.

## <a name="synchronization-settings"></a>Synchronisierungseinstellungen

- **Menge an E-Mails für die Synchronisierung**: Wählen Sie die Anzahl der Tage aus, für die E-Mails synchronisiert werden sollen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Wählen Sie **Unbegrenzt** aus, um alle verfügbaren E-Mails zu synchronisieren.
- **Synchronisierungszeitplan**: Wählen Sie den Zeitplan aus, nach dem Geräte mit Daten vom Exchange-Server synchronisiert werden. Sie können auch **Bei Eintreffen von Nachrichten** auswählen, wodurch Daten synchronisiert werden, sobald sie eintreffen. Oder wählen Sie **Manuell** aus, damit der Gerätebenutzer die Synchronisierung startet.

## <a name="content-sync-settings"></a>Inhaltssynchronisierungseinstellungen

- **Zu synchronisierender Inhaltstyp**: Wählen Sie die Inhaltstypen aus, die auf Geräten synchronisiert werden sollen:
  - **Kontakte:** **Ein** synchronisiert die Kontakte. **Aus** synchronisiert die Kontakte nicht automatisch. Benutzer synchronisieren manuell.
  - **Kalender:** **Ein** synchronisiert den Kalender. **Aus** synchronisiert die Kontakte nicht automatisch. Benutzer synchronisieren manuell.
  - **Aufgaben:** **Ein** synchronisiert die Tasks. **Aus** synchronisiert die Tasks nicht automatisch. Benutzer synchronisieren manuell.

## <a name="next-steps"></a>Nächste Schritte

Sie können auch die E-Mail-Einstellungen auf [Android](email-settings-android.md), [Android Enterprise](email-settings-android-enterprise.md), [iOS/iPadOS](email-settings-ios.md) und [Windows 10](email-settings-windows-10.md) konfigurieren.

[Konfigurieren von E-Mail-Einstellungen in Intune](email-settings-configure.md).
