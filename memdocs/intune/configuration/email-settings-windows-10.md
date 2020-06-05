---
title: 'E-Mail-Einstellungen für Windows 10-Geräte in Microsoft Intune: Azure | Microsoft-Dokumentation'
description: Erstellen Sie ein E-Mail-Profil für die Gerätekonfiguration, die Exchange-Server verwendet und Attribute von Azure Active Directory abruft. Mit Microsoft Intune können Sie auch SSL aktivieren und E-Mails und Zeitpläne auf Windows 10-Geräten synchronisieren.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/14/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0cd3505d0a0067adfe9082d7aa3882f3421a2183
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429601"
---
# <a name="email-profile-settings-for-devices-running-windows-10-in-microsoft-intune"></a>E-Mail-Profileinstellungen für Geräte in Microsoft Intune, die unter Windows 10 ausgeführt werden

Mit den E-Mail-Profileinstellungen können Sie die E-Mail-App auf Ihren Geräten konfigurieren, die unter Windows 10 und höher ausgeführt werden.

## <a name="before-you-begin"></a>Vorbereitung

[Erstellen Sie das Profil.](email-settings-configure.md)

## <a name="email-settings"></a>E-Mail-Einstellungen

- **E-Mail-Server**: Geben Sie den Hostnamen Ihres Exchange-Servers ein. Geben Sie beispielsweise `outlook.office365.com` ein.
- **Kontoname**: Geben Sie den Anzeigenamen des E-Mail-Kontos ein. Dieser Name wird Benutzern auf ihren Geräten angezeigt.
- **Benutzernamensattribut aus AAD**: Dieser Name ist das Attribut, dass Intune aus Azure Active Directory (AAD) abruft. Intune generiert dynamisch den Benutzernamen, der von diesem Profil verwendet wird. Folgende Optionen sind verfügbar:
  - **Benutzerprinzipalname**: Hiermit wird der Name abgerufen, z. B. `user1` oder `user1@contoso.com`.
  - **Primäre SMTP-Adresse**: Ruft den Namen im Format einer E-Mail-Adresse ab, z. B. `user1@contoso.com`.
  - **SAM-Kontoname**: Erfordert die Domäne, z.B. `domain\user1`. Geben Sie außerdem Folgendes ein:  
    - **Quelle für Benutzerdomänenname**: Wählen Sie zwischen **AAD** (Azure Active Directory) oder **Benutzerdefiniert**.

      Geben Sie beim Abrufen der Attribute von **AAD** auch Folgendes ein:
      - **Attribut für Benutzerdomänenname aus AAD**: Rufen Sie entweder das Attribut **Vollständiger Domänenname** oder das Attribut **NetBIOS-Name** des Benutzers ab.

      Geben Sie bei Verwendung von **benutzerdefinierten Attributen** auch Folgendes ein:
      - **Zu verwendender benutzerdefinierter Domänenname**: Geben Sie einen Wert ein, den Intune als Domänennamen verwenden kann, z. B. `contoso.com` oder `contoso`.

- **Attribut für E-Mail-Adresse aus AAD**: Intune ruft dieses Attribut aus Azure Active Directory (AAD) ab. Wählen Sie aus, wie die E-Mail-Adresse für den Benutzer generiert wird. Folgende Optionen sind verfügbar:
  - **Benutzerprinzipalname**: Der vollständige Prinzipalname, z. B. `user1@contoso.com` oder `user1`, wird als E-Mail-Adresse verwendet.
  - **Primäre SMTP-Adresse**: Verwendet die primäre SMTP-Adresse, z. B. `user1@contoso.com`, für die Anmeldung bei Exchange.

### <a name="security"></a>Sicherheit

- **SSL**: Mit der Option **Aktivieren** wird die SSL-Kommunikation (Secure Sockets Layer) beim Senden und Empfangen von E-Mails sowie bei der Kommunikation mit dem Exchange-Server verwendet. **Deaktivieren** macht SSL überflüssig.

### <a name="synchronization"></a>Synchronisierung

- **Menge an E-Mails für die Synchronisierung**: Wählen Sie die Anzahl der Tage aus, für die E-Mails synchronisiert werden sollen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Wählen Sie **Unbegrenzt** aus, um alle verfügbaren E-Mails zu synchronisieren.
- **Synchronisierungszeitplan**: Wählen Sie den Zeitplan aus, nach dem Geräte mit Daten vom Exchange-Server synchronisiert werden. Sie können auch **Bei Eintreffen von Nachrichten** auswählen, wodurch Daten synchronisiert werden, sobald sie eintreffen. Oder wählen Sie **Manuell** aus, damit der Gerätebenutzer die Synchronisierung startet.

  Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

### <a name="content-sync"></a>Inhaltsynchronisierung

- **Zu synchronisierender Inhaltstyp**: Wählen Sie die Inhaltstypen aus, die auf Geräten synchronisiert werden sollen. Folgende Optionen sind verfügbar:
  - **Kontakte:** **Ein** synchronisiert die Kontakte. **Aus** synchronisiert die Kontakte nicht automatisch. Benutzer synchronisieren manuell.
  - **Kalender:** **Ein** synchronisiert den Kalender. **Aus** synchronisiert die Kontakte nicht automatisch. Benutzer synchronisieren manuell.
  - **Aufgaben:** **Ein** synchronisiert die Tasks. **Aus** synchronisiert die Tasks nicht automatisch. Benutzer synchronisieren manuell.

## <a name="next-steps"></a>Nächste Schritte

Sie können auch die E-Mail-Einstellungen auf [Android](email-settings-android.md), [Android Enterprise](email-settings-android-enterprise.md) und [iOS/iPadOS](email-settings-ios.md) konfigurieren. 

[Erfahren Sie mehr über die E-Mail-Einstellungen in Intune](email-settings-configure.md).

[Weisen Sie das Profil zu](device-profile-assign.md), und [überwachen Sie dessen Status](device-profile-monitor.md).
