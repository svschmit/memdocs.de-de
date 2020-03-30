---
title: 'Verwenden von benutzerdefinierten Geräteeinstellungen in Microsoft Intune: Azure | Microsoft-Dokumentation'
description: Erstellen Sie ein Profil, oder fügen Sie ein Profil hinzu, um mithilfe von Microsoft Intune benutzerdefinierte Einstellungen für Geräte mit Windows Phone, Windows 8.1, Windows 10 und höher, Android-Geräteadministrator, Android Enterprise, macOS und iOS/iPadOS zu verwenden.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6122f4624cc40152184c1c460afa6a7a39976063
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/21/2020
ms.locfileid: "80083986"
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

    - **Name:** Geben Sie einen aussagekräftigen Namen für die Richtlinie ein. Benennen Sie Ihre Richtlinien so, dass Sie diese später leicht wiedererkennen. Ein guter Richtlinienname ist beispielsweise **Windows 10: Benutzerdefiniertes Profil zur Aktivierung eines benutzerdefinierten AllowVPNOverCellular-OMA-URI**.
    - **Beschreibung:** Geben Sie eine Beschreibung für das Profil ein. Diese Einstellung ist optional, wird jedoch empfohlen.
    - **Plattform**: Wählen Sie die Plattform Ihrer Geräte aus. Folgende Optionen sind verfügbar:

      - **Android-Geräteadministrator**
      - **Android Enterprise**
      - **iOS/iPadOS**
      - **macOS**
      - **Windows 10 und höher**
      - **Windows 8.1 und höher**

    - **Profiltyp**: Klicken Sie auf **Benutzerdefiniert**.

4. Die Einstellungen unterscheiden sich je nach Plattform. Um die Einstellungen für eine bestimmte Plattform anzuzeigen, wählen Sie Ihre Plattform aus:

    - [Android-Geräteadministrator](custom-settings-android.md)
    - [Android Enterprise](custom-settings-android-for-work.md)
    - [iOS/iPadOS](custom-settings-ios.md)
    - [macOS](custom-settings-macos.md)
    - [Windows 10](custom-settings-windows-10.md)
    - [Windows Holographic for Business](custom-settings-windows-holographic.md)
    - [Windows Phone 8.1](custom-settings-windows-phone-8-1.md)

5. Wenn Sie fertig sind, wählen Sie **Profil erstellen** > **Erstellen** aus.

Das Profil wird erstellt und in der Profilliste angezeigt (**Gerätekonfiguration** > **Profile**).

## <a name="next-steps"></a>Nächste Schritte

Nachdem das Profil erstellt wurde, kann es zugewiesen werden. Die nächsten Schritte sind das [Zuweisen von Benutzer- und Geräteprofilen in Microsoft Intune](device-profile-assign.md) und das [Überwachen von Geräteprofilen in Microsoft Intune](device-profile-monitor.md).
