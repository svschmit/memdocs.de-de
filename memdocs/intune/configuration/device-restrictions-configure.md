---
title: Einschränkung der Gerätefeatures durch Richtlinien in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Hinzufügen eines Geräteprofils zum Einschränken von Funktionen auf Android-Geräteadministrator-, Android Enterprise-, macOS-, iOS-, iPadOS- und Windows 10-Geräten in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e710678e3ac4775f5737090b791446c7a6e8285c
ms.sourcegitcommit: 8999e197f10fb72d1b82f30a599d1e588db237b7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88146353"
---
# <a name="configure-device-restriction-settings-in-microsoft-intune"></a>Konfigurieren von Einstellungen für Geräteeinschränkungen in Microsoft Intune

Intune enthält Richtlinien zur Geräteeinschränkung, die Administratoren bei der Steuerung von Android-, iOS-/iPadOS-, macOS- und Windows-Geräten unterstützen. Mit diesen Einschränkungen können Sie eine Vielzahl von Einstellungen und Features steuern, um die Ressourcen Ihres Unternehmens zu schützen. Administratoren können z.B.:

- Lassen Sie die Kamera des Geräts zu, oder blockieren Sie sie.
- den Zugriff auf Google Play, App-Stores, Dokumente und Gaming steuern.
- integrierte Apps blockieren oder eine Liste von Apps erstellen, die zugelassen oder nicht zugelassen werden.
- das Speichern von Dateien in Cloud- und Speicherkonten erlauben oder verhindern.
- eine Mindestlänge für Kennwörter festlegen und einfache Kennwörter blockieren.

Diese Features sind in Intune verfügbar und werden vom Administrator konfiguriert. Intune verwendet „Konfigurationsprofile“ zum Erstellen und Anpassen dieser Einstellungen für die Anforderungen Ihrer Organisation. Nachdem Sie diese Features in einem Profil hinzugefügt haben, können Sie das Profil anschließend auf Geräte in Ihrer Organisation pushen oder bereitstellen.

In diesem Artikel erfahren Sie, wie Sie ein Geräteeinschränkungsprofil erstellen. Sie können auch alle verfügbaren Einstellungen für die verschiedenen Plattformen anzeigen.

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
        - **Windows 8.1 und höher**

    - **Profil**: Wählen Sie **Geräteeinschränkungen** aus.

        Um ein Geräteeinschränkungsprofil für Windows 10 Team-Geräte wie etwa ein Surface Hub zu erstellen, wählen Sie **Geräteeinschränkungen (Windows 10 Team)** aus.

4. Wählen Sie **Erstellen** aus.
5. Geben Sie in **Grundlagen** die folgenden Eigenschaften ein:

    - **Name:** Geben Sie einen aussagekräftigen Namen für die Richtlinie ein. Benennen Sie Ihre Richtlinien so, dass Sie diese später leicht wiedererkennen. Ein guter Richtlinienname ist beispielsweise **iOS/iPadOS: Kamera auf Geräten blockieren**.
    - **Beschreibung:** Geben Sie eine Beschreibung für die Richtlinie ein. Diese Einstellung ist optional, wird jedoch empfohlen.

6. Wählen Sie **Weiter** aus.

7. Die verfügbaren **Konfigurationseinstellungen** variieren je nach ausgewählter Plattform. Wählen Sie Ihre Plattform für detaillierte Einstellungen aus:

    - [Android-Geräteadministrator](device-restrictions-android.md)
    - [Android Enterprise](device-restrictions-android-for-work.md)
    - [iOS/iPadOS](device-restrictions-ios.md)
    - [macOS](device-restrictions-macos.md)
    - [Windows 8.1](device-restrictions-windows-8-1.md)
    - [Windows 10 und höher](device-restrictions-windows-10.md)
    - [Windows 10 Team](device-restrictions-windows-10-teams.md)
    - [Windows Holographic for Business](device-restrictions-windows-holographic.md)

8. Wählen Sie **Weiter** aus.
9. Weisen Sie in **Bereichstags** (optional) ein Tag zu, um das Profil nach bestimmten IT-Gruppen wie `US-NC IT Team` oder `JohnGlenn_ITDepartment` zu filtern. Weitere Informationen zu Bereichstags finden Sie unter [Verwenden der RBAC und von Bereichstags für verteilte IT](../fundamentals/scope-tags.md).

    Wählen Sie **Weiter** aus.

10. Wählen Sie unter **Zuweisungen** die Benutzer oder Gruppen aus, denen Ihr Profil zugewiesen werden soll. Weitere Informationen zum Zuweisen von Profilen finden Sie unter [Zuweisen von Benutzer- und Geräteprofilen](device-profile-assign.md).

    Wählen Sie **Weiter** aus.

11. Überprüfen Sie die Einstellungen unter **Überprüfen + erstellen**. Wenn Sie auf **Erstellen** klicken, werden die Änderungen gespeichert, und das Profil wird zugewiesen. Die Richtlinie wird auch in der Profilliste angezeigt.

## <a name="next-steps"></a>Nächste Schritte

Nachdem das Profil erstellt wurde, kann es zugewiesen werden. Die nächsten Schritte sind das [Zuweisen von Benutzer- und Geräteprofilen in Microsoft Intune](device-profile-assign.md) und das [Überwachen von Geräteprofilen in Microsoft Intune](device-profile-monitor.md).

<!--  Removing image as part of design review; retaining source until we known the disposition.

## Example of device restriction settings

In this high-level example, you'll create a device restriction policy that blocks the use of the built-in camera app on Android devices.

![How to disable the camera on Android devices](./media/device-restrictions-configure/disable-android-camera.png)

-->
