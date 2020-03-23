---
title: Microsoft Intune-E-Mail-Einstellungen für Windows Phone 8.1
titleSuffix: ''
description: In diesem Artikel erhalten Sie Informationen zu den Intune-Einstellungen, die Sie zum Konfigurieren von E-Mail-Verbindungen auf Windows Phone 8.1-Geräten verwenden können.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 3/6/2018
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: a0dd12ea12e2127c678f8805f3d50b2b24f37c11
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79343556"
---
# <a name="email-profile-settings-in-microsoft-intune-for-devices-running-windows-phone-81"></a>E-Mail-Profileinstellungen in Microsoft Intune für Windows Phone 8.1-Geräte



In diesem Artikel werden die E-Mail-Profileinstellungen dargestellt, die Sie für Ihre Windows Phone 8.1-Geräte konfigurieren können.

>[!IMPORTANT]
>Windows Phone 8.1-E-Mail-Profile werden auch auf Windows 10-Geräte angewendet.

- **E-Mail-Server:** Der Hostname Ihres Exchange-Servers.
- **Kontoname** – Der Anzeigename für das E-Mail-Konto so, wie er den Benutzern auf ihren Geräten angezeigt wird.
- **Benutzernamensattribut aus AAD:** Das Attribut in Active Directory (AD) oder Azure AD, mit dem der Benutzername für dieses E-Mail-Profil generiert wird. Wählen Sie **Primäre SMTP-Adresse** aus, z.B. **user1@contoso.com** , oder **Benutzerprinzipalname**, z.B. **user1** oder **user1@contoso.com** .
- **E-Mail-Adressattribut aus AAD:** Die Art der Generierung der E-Mail-Adresse für den Benutzer auf den einzelnen Geräten. Wählen Sie **Primäre SMTP-Adresse** aus, um die primäre SMTP-Adresse zum Anmelden bei Exchange zu verwenden. Verwenden Sie **Benutzerprinzipalname** aus, um den vollständigen Benutzerprinzipalnamen als E-Mail-Adresse zu verwenden.


## <a name="security-settings"></a>Sicherheitseinstellungen

- **SSL:** Verwenden Sie SSL-Kommunikation (Secure Sockets Layer) beim Senden und Empfangen von E-Mails sowie bei der Kommunikation mit dem Exchange-Server.



## <a name="synchronization-settings"></a>Synchronisierungseinstellungen

- **Menge an E-Mails für die Synchronisierung:** Wählen Sie die Anzahl der Tage von E-Mails aus, die synchronisiert werden sollen, oder wählen Sie **Unbegrenzt** aus, um alle verfügbaren E-Mail-Nachrichten zu synchronisieren.
- **Synchronisierungszeitplan** – Wählen Sie den Zeitplan aus, nach dem Geräte mit Daten vom Exchange-Server synchronisiert werden. Sie können auch **Beim Erhalt von Nachrichten** auswählen, wobei die Daten sofort beim Eintreffen synchronisiert werden, oder **Manuell**, wobei der Benutzer des Geräts die Synchronisierung initiieren muss.

## <a name="content-sync-settings"></a>Inhaltssynchronisierungseinstellungen

- **Zu synchronisierender Inhaltstyp:** Wählen Sie die Inhaltstypen aus, die auf Geräten synchronisiert werden sollen:
  - **Kontakte**
  - **Kalender**
  - **Aufgaben**
