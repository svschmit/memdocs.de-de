---
title: Verwalten des Microsoft Defender ATP-Webschutzes für Android-Geräte in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Konfigurieren des Webschutzes in Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) für Android in Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1e3b12251117e689f3b4a5456cf20bae3797083a
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/28/2020
ms.locfileid: "87264533"
---
# <a name="configure-microsoft-defender-atp-on-android-devices-you-manage-with-intune"></a>Konfigurieren von Microsoft Defender ATP auf mit Intune verwalteten Android-Geräten

Wenn Sie Microsoft Intune und Microsoft Defender Advanced Threat Protection (ATP) integrieren, können Sie die Geräteverwaltungsprofile verwenden, um einige Einstellungen von Microsoft Defender ATP auf Android-Geräten zu ändern.

Bevor Sie fortfahren, müssen Sie [Microsoft Defender ATP in Intune konfigurieren](../protect/advanced-threat-protection-configure.md) und Android-Geräte per Onboarding in Microsoft Defender ATP integrieren.

## <a name="configure-web-protection-on-devices-that-run-android"></a>Konfigurieren des Features „Webschutz“ für Android-Geräte

Standardmäßig schließt Microsoft Defender ATP für Android das Feature „Webschutz“ ein und aktiviert es. [Webschutz](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/web-protection-overview) unterstützt das Schützen von Geräten vor Bedrohungen im Web und schützt Benutzer vor Phishingangriffen.

Das Feature ist zwar standardmäßig aktiviert, es gibt aber verschiedene Gründe, aus denen dieser Schutz auf manchen Android-Geräten deaktiviert werden sollte. Sie könnten sich beispielsweise dazu entscheiden, nur das Feature zum Scannen von Apps von Microsoft Defender ATP zu verwenden, oder das Feature „Webschutz“ daran zu hindern, Ihr VPN beim Scan schädlicher URLs zu verwenden.

Intune unterstützt das Deaktivieren des gesamten sowie Teilen des Features „Webschutz“. Die Methode, die Sie verwenden, und die Funktionen, die Sie deaktivieren, hängen davon ab, wie das Android-Gerät für Intune registriert wurde:

- **Android-Geräteadministrator**: Verwenden Sie ein Konfigurationsprofil, um benutzerdefinierte OMA-URI-Einstellungen auf dem Gerät festzulegen, um das gesamte Webschutz-Feature zu deaktivieren, oder deaktivieren Sie nur die Verwendung von VPNs. Allgemeine Informationen zu benutzerdefinierten Einstellungen auf Android-Geräten finden Sie unter [Verwenden benutzerdefinierter Einstellungen für Android-Geräte in Microsoft Intune](../configuration/custom-settings-android.md).

- **Android Enterprise (Arbeitsprofil):** Verwenden Sie ein App-Konfigurationsprofil und den *Konfigurations-Designer*, um das Feature „Webschutz“ zu deaktivieren. Diese Methode und dieser Registrierungstyp unterstützen das Deaktivieren aller Funktionen des Webschutz-Features, jedoch nicht das ausschließliche Deaktivieren der Verwendung von VPNs. Allgemeine Informationen zu App-Konfigurationsrichtlinien finden Sie unter [Verwenden des Konfigurations-Designers](../apps/app-configuration-policies-use-android.md#use-the-configuration-designer).

Zum Konfigurieren des Webschutz-Features auf Geräten verwenden Sie das folgende Vorgehen, um die entsprechende Konfiguration zu erstellen und bereitzustellen.

### <a name="disable-web-protection-for-android-device-administrator"></a>Deaktivieren des Features „Webschutz“ für Android-Geräteadministratoren

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.

3. Legen Sie folgende Einstellungen fest:

   - **Plattform**: Wählen Sie **Android-Geräteadministrator** aus.
   - **Profil**: Klicken Sie auf **Benutzerdefiniert**.

   Wählen Sie **Erstellen** aus.

4. Geben Sie unter den **Grundlegenden Einstellungen** die folgenden Informationen ein:

   - **Name:** Geben Sie einen aussagekräftigen Namen für das Profil ein. Benennen Sie Ihre Profile, damit Sie diese später leicht wiedererkennen. Wählen Sie beispielsweise einen Namen wie *Benutzerdefiniertes Android-Profil für das Feature „Webschutz“ in Microsoft Defender ATP* aus.
   - **Beschreibung:** Geben Sie eine Beschreibung für das Profil ein. Diese Einstellung ist optional, wird jedoch empfohlen.

5. Klicken Sie unter **Konfigurationseinstellungen** auf **Hinzufügen**.

   Geben Sie die Einstellungen für die Konfiguration an, die Sie bereitstellen möchten:

   - **Deaktivieren des Features „Webschutz“:**
     - **Name:** Geben Sie einen eindeutigen Namen für diese OMA-URI-Einstellung ein, damit Sie diese leicht finden können. Wählen Sie beispielsweise einen Namen wie *Feature „Webschutz“ in Microsoft Defender ATP deaktivieren* aus.
     - **Beschreibung:** Geben Sie optional eine Beschreibung ein, die einen Überblick über die Einstellung und andere wichtige Details bietet.
     - **OMA-URI**: Geben Sie **./Vendor/MSFT/DefenderATP/AntiPhishing** ein.
     - **Datentyp:** Verwenden Sie das Dropdownmenü, und klicken Sie auf **Integer**.
     - **Wert:** Geben Sie **0** ein, um das Feature „Webschutz“ einschließlich des VPN-basierten Scans zu deaktivieren.
       > [!NOTE]
       > Geben Sie **1** ein, um das Feature „Webschutz“ zu aktivieren. Dies ist die Standardeinstellung für das Feature „Webschutz“.

   - **Ausschließliches Deaktivieren der Verwendung von VPNs durch das Feature „Webschutz“:**
     - **Name:** Geben Sie einen eindeutigen Namen für diese OMA-URI-Einstellung ein, damit Sie diese leicht finden können. Wählen Sie beispielsweise einen Namen wie *Verwendung von VPNs durch das Feature „Webschutz“ in Microsoft Defender ATP deaktivieren* aus.
     - **Beschreibung:** Geben Sie optional eine Beschreibung ein, die einen Überblick über die Einstellung und andere wichtige Details bietet.
     - **OMA-URI**: Geben Sie **./Vendor/MSFT/DefenderATP/Vpn** ein.
     - **Datentyp:** Verwenden Sie das Dropdownmenü, und klicken Sie auf **Integer**.
     - **Wert:** Geben Sie **0** ein, um den VPN-basierten Scan zu deaktivieren.
       > [!NOTE]
       > Geben Sie **1** ein, um das Feature „Webschutz“ zu aktivieren. Dies ist die Standardeinstellung für das Feature „Webschutz“.

   Klicken Sie auf **Hinzufügen**, um die OMA-URI-Einstellungskonfiguration zu speichern, und klicken Sie dann zum Fortfahren auf **Weiter**.

6. Geben Sie auf der Seite **Zuweisungen** die Gruppen an, die dieses Profil erhalten sollen. Weitere Informationen zum Zuweisen von Profilen finden Sie unter [Zuweisen von Benutzer- und Geräteprofilen](../configuration/device-profile-assign.md).

7. Klicken Sie, wenn Sie fertig sind, auf der Seite **Überprüfen + erstellen** auf **Erstellen**. Das neue Profil wird in der Liste angezeigt, wenn Sie den Richtlinientyp für das Profil auswählen, das Sie erstellt haben.

### <a name="disable-web-protection-for-android-enterprise-work-profile"></a>Deaktivieren des Features „Webschutz“ für Android Enterprise (Arbeitsprofil)

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Klicken Sie auf **Apps** > **App-Konfigurationsrichtlinien** > **Hinzufügen**, und klicken Sie dann auf „Verwaltete Geräte“.

3. Geben Sie unter den **Grundlegenden Einstellungen** die folgenden Informationen ein:

   - **Name:** Geben Sie einen aussagekräftigen Namen für das Profil ein. Benennen Sie Ihre Profile, damit Sie diese später leicht wiedererkennen. Wählen Sie beispielsweise einen Namen wie *Android-App-Konfiguration für das Feature „Webschutz“ in Microsoft Defender ATP* aus.
   - **Beschreibung:** Geben Sie eine Beschreibung für das Profil ein. Diese Einstellung ist optional, wird jedoch empfohlen.
   - **Plattform**: Wählen Sie **Android Enterprise** aus.
   - **Profiltyp**: Wählen Sie die Option **Nur Arbeitsprofil** aus.
   - **Ziel-App:** Klicken Sie auf **App auswählen**.

4. Suchen Sie unter **Zugeordnete App** nach **Defender ATP**, und klicken Sie darauf, und klicken Sie dann auf **OK** > **Weiter**.

5. Klicken Sie unter **Einstellungen** im Dropdownmenü **Format der Konfigurationseinstellungen** auf **Konfigurations-Designer verwenden** und dann auf **Hinzufügen**. Der JSON-Editor wird geöffnet.

6. Suchen Sie nach dem Feature **Webschutz**, und klicken Sie darauf, und klicken Sie dann auf **OK**, um zur Seite **Einstellungen** zurückzukehren.

7. Geben Sie als **Konfigurationswert** den Wert **0** ein, um das Feature „Webschutz“ zu deaktivieren.

   > [!NOTE]
   > Geben Sie **1** ein, um das Feature „Webschutz“ zu aktivieren. Dies ist die Standardeinstellung für das Feature „Webschutz“.

   Wählen Sie **Weiter** aus, um den Vorgang fortzusetzen.

8. Geben Sie auf der Seite **Zuweisungen** die Gruppen an, die dieses Profil erhalten sollen. Weitere Informationen zum Zuweisen von Profilen finden Sie unter [Zuweisen von Benutzer- und Geräteprofilen](../configuration/device-profile-assign.md).

9. Klicken Sie, wenn Sie fertig sind, auf der Seite **Überprüfen + erstellen** auf **Erstellen**. Das neue Profil wird in der Liste angezeigt, wenn Sie den Richtlinientyp für das Profil auswählen, das Sie erstellt haben.

## <a name="next-steps"></a>Nächste Schritte

- [Überwachen der Konformität für Risikostufen](../protect/advanced-threat-protection-monitor.md)
- [Verwenden von Intune zum Korrigieren von mit Microsoft Defender ATP identifizierten Sicherheitsrisiken](../protect/atp-manage-vulnerabilities.md)

Weitere Informationen finden Sie in der Dokumentation zu Microsoft Defender ATP:

- [Microsoft Defender ATP – bedingter Zugriff](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/conditional-access)
- [Microsoft Defender ATP – Risikodashboard](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)
