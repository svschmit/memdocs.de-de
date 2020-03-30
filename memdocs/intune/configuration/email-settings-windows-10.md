---
title: 'E-Mail-Einstellungen für Windows 10-Geräte in Microsoft Intune: Azure | Microsoft-Dokumentation'
description: Erstellen Sie ein E-Mail-Profil für die Gerätekonfiguration, die Exchange-Server verwendet und Attribute von Azure Active Directory abruft. Mit Microsoft Intune können Sie auch SSL aktivieren und E-Mails und Zeitpläne auf Windows 10-Geräten synchronisieren.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fa861a266f89b82fdd2d6e73d30fdc2e58da33b4
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086909"
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

      Wenn Sie die Attribute von **AAD** abrufen möchten, geben Sie Folgendes ein:
      - **Attribut für Benutzerdomänenname aus AAD**: Rufen Sie entweder das Attribut **Vollständiger Domänenname** oder das Attribut **NetBIOS-Name** des Benutzers ab.

      Wenn Sie sich dazu entscheiden, die Attribute **Benutzerdefiniert** zu verwenden, geben Sie Folgendes ein:
      - **Zu verwendender benutzerdefinierter Domänenname**: Geben Sie einen Wert ein, den Intune als Domänennamen verwenden kann, z. B. `contoso.com` oder `contoso`.

- **Attribut für E-Mail-Adresse aus AAD**: Intune ruft dieses Attribut aus Azure Active Directory (AAD) ab. Wählen Sie aus, wie die E-Mail-Adresse für den Benutzer generiert wird. Folgende Optionen sind verfügbar:
  - **Benutzerprinzipalname**: Der vollständige Prinzipalname, z. B. `user1@contoso.com` oder `user1`, wird als E-Mail-Adresse verwendet.
  - **Primäre SMTP-Adresse**: Verwendet die primäre SMTP-Adresse, z. B. `user1@contoso.com`, für die Anmeldung bei Exchange.

### <a name="security"></a>Sicherheit

- **SSL**: Mit der Option **Aktivieren** wird die SSL-Kommunikation (Secure Sockets Layer) beim Senden und Empfangen von E-Mails sowie bei der Kommunikation mit dem Exchange-Server verwendet. **Deaktivieren** macht SSL überflüssig.

### <a name="synchronization"></a>Synchronisierung

- **Menge an E-Mails für die Synchronisierung**: Wählen Sie die Anzahl der Tage aus, für die E-Mails synchronisiert werden sollen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Wählen Sie **Unbegrenzt** aus, um alle verfügbaren E-Mails zu synchronisieren.
- **Synchronisierungszeitplan**: Wählen Sie den Zeitplan aus, nach dem Geräte mit Daten vom Exchange-Server synchronisiert werden. Sie können auch **Bei Eintreffen von Nachrichten** auswählen, wodurch Daten synchronisiert werden, sobald sie eintreffen. Oder wählen Sie **Manuell** aus, damit der Gerätebenutzer die Synchronisierung startet.

### <a name="content-sync"></a>Inhaltsynchronisierung

- **Zu synchronisierender Inhaltstyp**: Wählen Sie die Inhaltstypen aus, die auf Geräten synchronisiert werden sollen:
  - **Kontakte:** **Ein** synchronisiert die Kontakte. **Aus** synchronisiert die Kontakte nicht automatisch. Benutzer synchronisieren manuell.
  - **Kalender:** **Ein** synchronisiert den Kalender. **Aus** synchronisiert die Kontakte nicht automatisch. Benutzer synchronisieren manuell.
  - **Aufgaben:** **Ein** synchronisiert die Tasks. **Aus** synchronisiert die Tasks nicht automatisch. Benutzer synchronisieren manuell.

## <a name="next-steps"></a>Nächste Schritte

Sie können auch die E-Mail-Einstellungen auf [Android](email-settings-android.md), [Android Enterprise](email-settings-android-enterprise.md) und [iOS/iPadOS](email-settings-ios.md) konfigurieren. 

[Konfigurieren von E-Mail-Einstellungen in Intune](email-settings-configure.md).
