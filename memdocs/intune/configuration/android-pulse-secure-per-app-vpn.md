---
title: 'Benutzerdefiniertes VPN-Profil pro App für Android in Microsoft Intune: Azure | Microsoft-Dokumentation'
description: Erfahren Sie, wie Sie ein App-bezogenes VPN-Profil für Geräte des Android-Geräteadministrators erstellen, die von Microsoft Intune verwaltet werden.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: conceptual
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
ms.openlocfilehash: d58ab666929e1e28cab4e19f2e2cec668f428452
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "80083868"
---
# <a name="use-a-microsoft-intune-custom-profile-to-create-a-per-app-vpn-profile-for-android-devices"></a>Verwenden eines benutzerdefinierten Microsoft Intune-Profils zum Erstellen eines VPN-Profils pro App für Android-Geräte

Sie können ein App-bezogenes VPN-Profil für Android 5.0-Geräte oder höher erstellen, die von Intune verwaltet werden. Erstellen Sie zunächst ein VPN-Profil, das den Pulse Secure- oder Citrix-Verbindungstyp verwendet. Erstellen Sie anschließend eine benutzerdefinierte Konfigurationsrichtlinie, die das VPN-Profil angegebenen Apps zuordnet.

> [!NOTE]
> Sie können die folgenden Schritte auch ausführen, um App-bezogenes VPN auf Android Enterprise-Geräten zu verwenden. Es wird jedoch empfohlen, eine [App-Konfigurationsrichtlinie](../apps/app-configuration-policies-use-android.md) für Ihre VPN-Client-App zu verwenden.

Nachdem Sie die Richtlinie Ihrem Android-Gerät oder Ihren Benutzergruppen zugewiesen haben, sollten Benutzer den Pulse Secure- oder Citrix-VPN-Client starten. Der VPN-Client lässt dann lediglich Datenverkehr von den angegebenen Apps über die offene VPN-Verbindung zu.

> [!NOTE]
>
> Es werden nur die Verbindungstypen „Pulse Secure“ und „Citrix“ für dieses Profil unterstützt.

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

8. Klicken Sie auf **Weiter**, und setzen Sie die Erstellung des Profils fort. Weitere Informationen finden Sie unter [Erstellen von VPN-Profilen](vpn-settings-configure.md#create-the-profile).

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

    > [!div class="mx-imgBorder"]
    >![Beispiel für eine benutzerdefinierte Pro-App-VPN-Richtlinie für einen Android-Geräteadministrator](./media/android-pulse-secure-per-app-vpn/android_per_app_vpn_oma_uri.png)

### <a name="set-your-app-list-to-blacklist-or-whitelist-optional"></a>Festlegen, ob Ihre App-Liste eine Positivliste (Whitelist) oder eine Negativliste (Blacklist) sein soll (optional)

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
