---
title: 'Benutzerdefiniertes Pro-App-VPN-Profil für den Android-Geräteadministrator in Microsoft Intune: Azure | Microsoft-Dokumentation'
description: Verwenden Sie ein benutzerdefiniertes Pro-App-VPN-Profil für den Android-Geräteadministrator mit den VPN-Verbindungstypen Pulse Secure oder Citrix in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/22/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d035ebf5-85f4-4001-a249-75d24325061a
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3c8e09b6010f7fc846fd81281053eaaa722e5ef4
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262794"
---
# <a name="use-a-microsoft-intune-custom-profile-to-create-a-per-app-vpn-profile-for-android-devices"></a>Verwenden eines benutzerdefinierten Microsoft Intune-Profils zum Erstellen eines VPN-Profils pro App für Android-Geräte

Sie können ein App-bezogenes VPN-Profil für Android 5.0-Geräte oder höher erstellen, die von Intune verwaltet werden. Erstellen Sie zunächst ein VPN-Profil, das den Pulse Secure- oder Citrix-Verbindungstyp verwendet. Erstellen Sie anschließend eine benutzerdefinierte Konfigurationsrichtlinie, die das VPN-Profil angegebenen Apps zuordnet.

Diese Funktion gilt für:

- Android-Geräteadministrator

Um ein Pro-App-VPN-Profil auf Android Enterprise-Geräten zu verwenden, richten Sie eine [App-Konfigurationsrichtlinie](../apps/app-configuration-vpn-ae.md) ein. App-Konfigurationsrichtlinien unterstützen mehr VPN-Client-Apps. Auf Android Enterprise-Geräten können Sie die Schritte in diesem Artikel ausführen. Dies wird jedoch nicht empfohlen, und es stehen nur Pulse Secure- und Citrix-VPN-Verbindungen zur Verfügung.

Nachdem Sie die Richtlinie Ihrem Android-Gerät oder Ihren Benutzergruppen zugewiesen haben, sollten Benutzer den Pulse Secure- oder Citrix-VPN-Client starten. Der VPN-Client lässt dann lediglich Datenverkehr von den angegebenen Apps über die offene VPN-Verbindung zu.

> [!NOTE]
>
> Für den Android-Geräteadministrator werden nur die Verbindungstypen „Pulse Secure“ und „Citrix“ unterstützt. Verwenden Sie auf Android Enterprise-eine [App-Konfigurationsrichtlinie](../apps/app-configuration-vpn-ae.md).

## <a name="step-1-create-a-vpn-profile"></a>Schritt 1: Erstellen eines VPN-Profils

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.
3. Geben Sie die folgenden Eigenschaften ein:

    - **Plattform**: Wählen Sie **Android-Geräteadministrator** aus.
    - **Profil**: Wählen Sie **VPN** aus.

4. Wählen Sie **Erstellen** aus.
5. Geben Sie in **Grundlagen** die folgenden Eigenschaften ein:

    - **Name:** Geben Sie einen aussagekräftigen Namen für das Profil ein. Benennen Sie Ihre Profile, damit Sie diese später leicht wiedererkennen. Ein geeigneter Profilname ist beispielsweise **Pro-App-VPN-Profil für Android-Geräteadministrator für das gesamte Unternehmen**.
    - **Beschreibung:** Geben Sie eine Beschreibung für das Profil ein. Diese Einstellung ist optional, wird jedoch empfohlen.

6. Wählen Sie **Weiter** aus.
7. Konfigurieren Sie unter **Konfigurationseinstellungen** die Einstellungen für das Profil:

    - [VPN-Einstellungen für Geräte des Android-Geräteadministrators](vpn-settings-android.md).

    Notieren Sie den Wert für **Verbindungsname**, den Sie beim Erstellen des VPN-Profils eingeben. Dieser Name wird im nächsten Schritt benötigt. In diesem Beispiel lautet der Verbindungsname **MyAppVpnProfile**.

8. Wählen Sie **Weiter** aus, und setzen Sie die Erstellung des Profils fort. Weitere Informationen finden Sie unter [Erstellen von VPN-Profilen](vpn-settings-configure.md#create-the-profile).

## <a name="step-2-create-a-custom-configuration-policy"></a>Schritt 2: Erstellen einer benutzerdefinierten Konfigurationsrichtlinie

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.
3. Geben Sie die folgenden Eigenschaften ein:

    - **Name:** Geben Sie einen aussagekräftigen Namen für das benutzerdefinierte Profil ein. Benennen Sie Ihre Profile, damit Sie diese später leicht wiedererkennen. Ein geeigneter Profilname ist beispielsweise **Benutzerdefiniertes OMA-URI-VPN-Profil für Android für das gesamte Unternehmen**.
    - **Beschreibung:** Geben Sie eine Beschreibung für das Profil ein. Diese Einstellung ist optional, wird jedoch empfohlen.
    - **Plattform**: Wählen Sie **Android-Geräteadministrator** aus.
    - **Profiltyp**: Klicken Sie auf **Benutzerdefiniert**.

4. Wählen Sie **Einstellungen** > **Konfigurieren** aus.
5. Klicken Sie im Bereich **Custom OMA-URI Settings** (Benutzerdefinierte OMA-URI-Einstellungen) auf **Hinzufügen**.
    - **Name:** Geben Sie einen Namen für Ihre Einstellung ein.
    - **Beschreibung:** Geben Sie eine Beschreibung für das Profil ein. Diese Einstellung ist optional, wird jedoch empfohlen.
    - **OMA-URI**: Geben Sie `./Vendor/MSFT/VPN/Profile/*Name*/PackageList` ein, wobei *Name* der in Schritt 1 notierte Verbindungsname ist. In diesem Beispiel lautet die Zeichenfolge `./Vendor/MSFT/VPN/Profile/MyAppVpnProfile/PackageList`.
    - **Datentyp:** Geben Sie **Zeichenfolge** ein.
    - **Wert:** Geben Sie eine durch Semikolons getrennte Liste der Pakete ein, die dem Profil zugeordnet werden sollen. Wenn z. B. Excel und der Google-Browser Chrome die VPN-Verbindung verwenden sollen, geben Sie `com.microsoft.office.excel;com.android.chrome` ein.

    :::image type="content" source="./media/android-pulse-secure-per-app-vpn/android_per_app_vpn_oma_uri.png" alt-text="Benutzerdefinierte Pro-App-VPN-Richtlinie für den Android-Geräteadministrator in Microsoft Intune":::

### <a name="set-your-blocked-and-allowed-app-list-optional"></a>Festlegen der Listen mit gesperrten und zugelassenen Apps (optional)

Sie können mithilfe des Werts *BLACKLIST* eine Liste von Apps angeben, die die VPN-Verbindung **nicht** verwenden können. Alle anderen Apps stellen über das VPN eine Verbindung her. Alternativ können Sie mithilfe des Werts **WHITELIST** eine Liste von Apps angeben, die die VPN-Verbindung verwenden *können*. Apps, die sich nicht auf der Liste befinden, stellen keine Verbindung über das VPN her.

1. Klicken Sie im Bereich **Custom OMA-URI Settings** (Benutzerdefinierte OMA-URI-Einstellungen) auf **Hinzufügen**.
2. Geben Sie einen Einstellungsnamen ein.
3. Geben Sie in **OMA-URI**`./Vendor/MSFT/VPN/Profile/*Name*/Mode` ein, wobei *Name* der in Schritt 1 notierte Name für das VPN-Profil ist. In unserem Beispiel lautet die Zeichenfolge `./Vendor/MSFT/VPN/Profile/MyAppVpnProfile/Mode`.
4. Geben Sie in **Datentyp** **Zeichenfolge**ein.
5. Geben Sie für **Wert** entweder **BLACKLIST** oder **WHITELIST** ein.

## <a name="step-3-assign-both-policies"></a>Schritt 3: Zuweisen beider Richtlinien

[Weisen Sie beide Geräteprofile](device-profile-assign.md) den erforderlichen Benutzern oder Geräten zu.

## <a name="next-steps"></a>Nächste Schritte

- Eine Liste aller VPN-Einstellungen für einen Android-Geräteadministrator finden Sie unter [Android-Geräteeinstellungen zur VPN-Konfiguration](vpn-settings-android.md).
- Weitere Informationen zu VPN-Einstellungen und Intune finden Sie unter [Erstellen von VPN-Profilen zum Herstellen einer Verbindung mit VPN-Servern in Intune](vpn-settings-configure.md).
