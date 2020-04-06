---
title: 'Verwenden von benutzerdefinierten Geräteeinstellungen in Microsoft Intune: Azure | Microsoft-Dokumentation'
description: Erstellen Sie ein Profil, oder fügen Sie ein Profil hinzu, um mithilfe von Microsoft Intune benutzerdefinierte Einstellungen für Geräte mit Windows Phone, Windows 8.1, Windows 10 und höher, Android-Geräteadministrator, Android Enterprise, macOS und iOS/iPadOS zu verwenden.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/24/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c96de75557a4817f4e5f034689faecf7374cfe3f
ms.sourcegitcommit: 7687cf8fdecd225216f58b8113ad07a24e43d4a3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80359449"
---
# <a name="create-a-profile-with-custom-settings-in-intune"></a>Erstellen eines Profils mit benutzerdefinierten Einstellungen in Intune

Microsoft Intune umfasst einige integrierte Einstellungen zum Steuern verschiedener Features auf einem Gerät. Sie können auch benutzerdefinierte Profile erstellen, deren Einstellungen denen integrierter Profile ähneln. Benutzerdefinierte Profile eignen sich gut, wenn Sie Geräteeinstellungen und -features verwenden möchten, die nicht in Intune integriert sind. Diese Profile umfassen Features und Einstellungen, die Sie auf Geräten innerhalb Ihrer Organisation steuern können. Sie können beispielsweise ein benutzerdefiniertes Profil erstellen, das für alle iOS/iPadOS-Geräte ein bestimmtes Feature festlegt.

Benutzerdefinierte Einstellungen werden für jede Plattform anders konfiguriert. Bei Android- und Windows-Geräten können Sie beispielsweise OMA-URI-Werte (Open Mobile Alliance Uniform Resource Identifier) zum Steuern von Features auf Geräten eingeben. Sie können für Apple-Geräte eine Datei importieren, die Sie mit [Apple Configurator](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) oder dem [Apple-Profil-Manager](https://support.apple.com/profile-manager) erstellt haben.

Weitere Informationen zu Konfigurationsprofilen finden Sie unter [Was sind Microsoft Intune-Geräteprofile?](device-profiles.md).

Dieser Artikel veranschaulicht, wie Sie ein benutzerdefiniertes Profil für den Android-Geräteadministrator sowie für Android Enterprise, iOS/iPadOS, macOS und Windows erstellen. Sie können auch alle verfügbaren Einstellungen für die verschiedenen Plattformen anzeigen.

## <a name="create-the-profile"></a>Erstellen des Profils

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.
3. Geben Sie die folgenden Eigenschaften ein:

    - **Plattform**: Wählen Sie die Plattform Ihrer Geräte aus. Folgende Optionen sind verfügbar:  

        - **Android-Geräteadministrator**
        - **Android Enterprise**
        - **iOS/iPadOS**
        - **macOS**
        - **Windows 10 und höher**
        - **Windows Phone 8.1**

    - **Profil**: Klicken Sie auf **Benutzerdefiniert**.

4. Wählen Sie **Erstellen** aus.
5. Geben Sie in **Grundlagen** die folgenden Eigenschaften ein:

    - **Name:** Geben Sie einen aussagekräftigen Namen für die Richtlinie ein. Benennen Sie Ihre Richtlinien so, dass Sie diese später leicht wiedererkennen. Ein guter Richtlinienname ist beispielsweise **Windows 10: Benutzerdefiniertes Profil zur Aktivierung eines benutzerdefinierten AllowVPNOverCellular-OMA-URI**.
    - **Beschreibung:** Geben Sie eine Beschreibung für die Richtlinie ein. Diese Einstellung ist optional, wird jedoch empfohlen.

6. Wählen Sie **Weiter** aus.

7. Die verfügbaren **Konfigurationseinstellungen** variieren je nach ausgewählter Plattform. Wählen Sie Ihre Plattform für detaillierte Einstellungen aus:

    - [Android-Geräteadministrator](custom-settings-android.md)
    - [Android Enterprise](custom-settings-android-for-work.md)
    - [iOS/iPadOS](custom-settings-ios.md)
    - [macOS](custom-settings-macos.md)
    - [Windows 10](custom-settings-windows-10.md)
    - [Windows Holographic for Business](custom-settings-windows-holographic.md)
    - [Windows Phone 8.1](custom-settings-windows-phone-8-1.md)

8. Wählen Sie **Weiter** aus.
9. Weisen Sie in **Bereichstags** (optional) ein Tag zu, um das Profil nach bestimmten IT-Gruppen wie `US-NC IT Team` oder `JohnGlenn_ITDepartment` zu filtern. Weitere Informationen zu Bereichstags finden Sie unter [Verwenden der RBAC und von Bereichstags für verteilte IT](../fundamentals/scope-tags.md).

    Wählen Sie **Weiter** aus.

10. Wählen Sie unter **Zuweisungen** die Benutzer oder Gruppen aus, denen Ihr Profil zugewiesen werden soll. Weitere Informationen zum Zuweisen von Profilen finden Sie unter [Zuweisen von Benutzer- und Geräteprofilen](device-profile-assign.md).

    Wählen Sie **Weiter** aus.

11. Überprüfen Sie die Einstellungen unter **Überprüfen + erstellen**. Wenn Sie auf **Erstellen** klicken, werden die Änderungen gespeichert, und das Profil wird zugewiesen. Die Richtlinie wird auch in der Profilliste angezeigt.

## <a name="example"></a>Beispiel

Im folgenden Beispiel wird die Einstellung **Konnektivität > VPN über Mobilfunknetz zulassen** aktiviert. Mit dieser Einstellung kann ein Windows 10-Gerät eine VPN-Verbindung über ein Mobilfunknetz herstellen.

> [!div class="mx-imgBorder"]
> ![Beispiel für eine benutzerdefinierte Richtlinie mit VPN-Einstellungen in Intune und im Endpoint Manager](./media/custom-settings-configure/custom-policy-example.png)

## <a name="next-steps"></a>Nächste Schritte

Das Profil ist nun erstellt, führt aber vielleicht noch keine Aktionen durch. Die nächsten Schritte sind das [Zuweisen von Benutzer- und Geräteprofilen in Microsoft Intune](device-profile-assign.md) und das [Überwachen von Geräteprofilen in Microsoft Intune](device-profile-monitor.md).
