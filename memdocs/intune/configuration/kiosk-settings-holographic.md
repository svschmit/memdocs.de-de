---
title: Kioskeinstellungen für Windows Holographic for Business in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Konfigurieren Sie Ihre Windows Holographic for Business-Geräte als Kiosks mit einer App oder mehreren Apps, und passen Sie das Startmenü an, fügen Sie Apps hinzu, zeigen Sie die Taskleiste an und konfigurieren Sie einen Webbrowser in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: d18ea0a12f0525b71fbcb8660187af36f1148bee
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/19/2020
ms.locfileid: "85093164"
---
# <a name="windows-holographic-for-business-device-settings-to-run-as-a-kiosk-in-intune"></a>Geräteeinstellungen bei Windows Holographic for Business zur Ausführung als Kiosk in Intune

Sie können Windows Holographic for Business-Geräte so konfigurieren, dass sie im Single-App- oder im Multi-App-Kioskmodus ausgeführt werden. Einige Funktionen werden unter Windows Holographic for Business nicht unterstützt.

In diesem Artikel werden die verschiedenen Einstellungen aufgeführt und beschrieben, die Sie für Windows Holographic for Business-Geräte steuern können. Als Bestandteil Ihrer Lösung für die mobile Geräteverwaltung (Mobile Device Management, MDM) verwenden Sie diese Einstellungen, um Ihre Geräte mit Windows Holographic for Business für die Ausführung im Kioskmodus zu konfigurieren.

Als Intune-Administrator können Sie für Ihre Geräte diese Einstellungen erstellen und ihnen zuweisen.

Weitere Informationen zur Windows-Kioskfunktion in Intune finden Sie unter [Konfigurieren der Kiosk-Einstellungen](kiosk-settings.md).

## <a name="before-you-begin"></a>Vorbereitung

- [Erstellen Sie ein Windows 10-Konfigurationsprofil für Kioskgeräte für mehrere Benutzer](kiosk-settings.md#create-the-profile).

  Beim Erstellen eines Windows 10-Konfigurationsprofils für Kioskgeräte für mehrere Benutzer gibt es mehr Einstellungen, als in diesem Artikel aufgeführt werden. Die Einstellungen in diesem Artikel werden auf Geräten mit Windows Holographic for Business unterstützt.

- Dieses Kioskprofil steht in direktem Zusammenhang mit dem Geräteeinschränkungsprofil, das Sie mithilfe der [Microsoft Edge-Kioskeinstellungen](device-restrictions-windows-holographic.md#microsoft-edge-browser) erstellen. Zusammenfassung:

  1. Erstellen Sie das Kioskprofil, um das Gerät im Kioskmodus auszuführen.
  2. Erstellen Sie das [Geräteeinschränkungsprofil](device-restrictions-windows-holographic.md#microsoft-edge-browser), und konfigurieren Sie spezifische Features und Einstellungen, die in Microsoft Edge zulässig sind.

> [!IMPORTANT]
> Achten Sie darauf, dass Sie dieses Kioskprofil den gleichen Geräten wie Ihr [Microsoft Edge-Profil](device-restrictions-windows-holographic.md#microsoft-edge-browser) zuweisen.

## <a name="single-app-full-screen-kiosk"></a>Einzelne App, Vollbildkiosk

Hiermit wird nur eine App auf dem Gerät ausgeführt. Wenn sich der Benutzer anmeldet, wird eine bestimmte App gestartet. Dieser Modus hindert den Benutzer auch daran, neue Apps zu öffnen oder die App zu ändern, die ausgeführt wird.

- **Typ der Benutzeranmeldung:** Wählen Sie den Kontotyp aus, der die App ausführt. Folgende Optionen sind verfügbar:

  - **Automatische Anmeldung (Windows 10, Version 1803 und neuer):** Wird unter Windows Holographic for Business nicht unterstützt.
  - **Lokales Benutzerkonto:** Geben Sie das lokale Benutzerkonto (auf dem Gerät) an. Geben Sie alternativ ein Microsoft Account-Konto (MSA) ein, das der Kiosk-App zugeordnet ist. Das von Ihnen eingegebene Konto wird zum Anmelden im Kiosk verwendet.

    Für Kioske in öffentlichen Umgebungen sollte ein Benutzertyp mit dem geringsten Privileg verwendet werden.

- **Anwendungstyp:** Wählen Sie **Store-App hinzufügen** aus.

  - **App zur Ausführung im Kioskmodus:** Wählen Sie eine App in der Liste aus.

    Es sind keine Apps aufgelistet? Fügen Sie einige mithilfe der Schritte unter [Client-Apps](../apps/apps-add.md) hinzu.

## <a name="multi-app-kiosk"></a>Kiosk mit mehreren Apps

Apps, die sich in diesem Modus befinden, sind über das Startmenü verfügbar. Diese Apps sind die einzigen Apps, die der Benutzer öffnen kann. Wenn bei einer App eine Abhängigkeit von einer anderen App vorliegt, müssen beide in der Liste zulässiger Apps enthalten sein.

- **Geräte unter Windows 10 im S Modus als Ziel verwenden:** Klicken Sie auf **Nein**. Der S Modus wird unter Windows Holographic for Business nicht unterstützt.

- **Typ der Benutzeranmeldung:** Fügen Sie mindestens ein Benutzerkonto hinzu, das die von Ihnen hinzugefügten Apps verwenden kann. Folgende Optionen sind verfügbar:

  - **Automatische Anmeldung (Windows 10, Version 1803 und neuer):** Wird unter Windows Holographic for Business nicht unterstützt.
  - **Lokale Benutzerkonten:** **Fügen Sie das lokale Benutzerkonto (auf dem Gerät) hinzu**. Das von Ihnen eingegebene Konto wird zum Anmelden im Kiosk verwendet.
  - **Azure AD-Benutzer oder Gruppe (Windows 10, Version 1803 und höher):** Bei dieser Option sind Benutzeranmeldeinformationen für die Anmeldung auf dem Gerät erforderlich. Wählen Sie **Hinzufügen** aus, um Azure AD-Benutzer oder Gruppen aus der Liste auszuwählen. Sie können mehrere Benutzer und Gruppen auswählen. Wählen Sie **OK** aus, um die Änderungen zu speichern.
  - **HoloLens-Besucher:** Beim Besucherkonto handelt es sich um ein Gastkonto, für das keine Anmeldeinformationen oder Authentifizierung erforderlich ist. Weitere Informationen dazu finden Sie unter [shared PC mode concepts (Konzepte für den Modus „Freigegebener Computer“)](https://docs.microsoft.com/windows/configuration/set-up-shared-or-guest-pc#shared-pc-mode-concepts).

- **Browser und Anwendungen**: Wählen Sie die Apps aus, die auf dem Kioskgerät ausgeführt werden sollen. Denken Sie daran, dass Sie mehrere Apps hinzufügen können.

  - **Browser**
    - **Microsoft Edge hinzufügen**: Microsoft Edge wird dem App-Raster hinzugefügt, und alle Anwendungen können in diesem Kiosk ausgeführt werden. Wählen Sie den Microsoft Edge-Kioskmodustyp aus:

      - **Normalmodus (Vollversion von Microsoft Edge)** : Führt eine Vollversion von Microsoft Edge mit sämtlichen Funktionen für das Browsen aus. Benutzerdaten und -zustand werden zwischen Sitzungen beibehalten.
      - **Öffentliches Browsen (InPrivate)** : Hiermit wird eine Version von Microsoft Edge InPrivate mit mehreren Registerkarten mit einer für Kioske ausgelegten Benutzeroberfläche im Vollbildmodus ausgeführt.

      Weitere Informationen zu diesen Optionen finden Sie unter [Bereitstellen des Microsoft Edge-Kioskmodus](https://docs.microsoft.com/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types).

      > [!NOTE]
      > Mit dieser Einstellung wird der Microsoft Edge-Browser auf dem Gerät aktiviert. Erstellen Sie zum Konfigurieren spezifischer Microsoft Edge-Einstellungen ein Geräteeinschränkungsprofil (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **Windows 10** (Plattform) > **Geräteeinschränkungen** > **Microsoft Edge-Browser**). Der [Microsoft Edge-Browser](device-restrictions-windows-holographic.md#microsoft-edge-browser) beschreibt und führt alle Holographic for Business-Einstellungen auf.

    - **Kioskbrowser hinzufügen**: Wird unter Windows Holographic for Business nicht unterstützt.

  - **Anwendungen**
    - **Store-App hinzufügen:** Wählen Sie eine vorhandene App aus, die Sie zu Intune hinzugefügt oder dort unter [Client-Apps](../apps/apps-add.md) bereitgestellt haben, einschließlich branchenspezifischer Apps. Wenn keine Apps in der Liste aufgeführt sind, unterstützt Intune zahlreiche [App-Typen](../apps/apps-add.md), die Sie [zu Intune hinzufügen](../apps/store-apps-windows.md) können.
    - **Win32-App hinzufügen:** Wird unter Windows Holographic for Business nicht unterstützt.
    - **Nach AUMID hinzufügen:** Mit dieser Option können Sie Windows-Posteingangs-Apps wie Editor oder Rechner hinzufügen. Geben Sie die folgenden Eigenschaften ein:

      - **Anwendungsname:** Erforderlich. Geben Sie einen Namen für die Anwendung ein.
      - **Anwendungsbenutzermodell-ID (AUMID):** Erforderlich. Geben Sie die AUMID der Windows-App ein. Weitere Informationen zum Abrufen dieser ID finden Sie unter [Ermitteln der Anwendungsbenutzermodell-ID einer installierten App](https://docs.microsoft.com/windows-hardware/customize/enterprise/find-the-application-user-model-id-of-an-installed-app).

    - **AutoLaunch**: (Optional) Nachdem Sie Ihre Apps und Ihren Browser hinzugefügt haben, wählen Sie eine App oder einen Browser aus, die bzw. der jeweils automatisch geöffnet werden soll, wenn sich der Benutzer anmeldet. Nur eine App oder ein Browser kann mit automatisch gestartet werden.
    - **Kachelgröße:** Erforderlich. Nachdem Sie Ihre Apps hinzugefügt haben, wählen Sie eine kleine, mittlere, breite oder große App-Kachelgröße aus.

- **Alternatives Startlayout verwenden:** Wählen Sie **Ja** aus, um eine XML-Datei einzufügen, die beschreibt, wie die Apps im Startmenü dargestellt werden (u. a. die Reihenfolge der Apps). Verwenden Sie diese Option, wenn Sie in Ihrem Startmenü weitere Anpassungen vornehmen möchten. [Startlayout anpassen und exportieren](https://docs.microsoft.com/hololens/hololens-kiosk#start-layout-for-hololens): Diese Option umfasst eine Anleitung und eine XML-Datei für Windows Holographic for Business-Geräte.

- **Windows-Taskleiste:** Wird unter Windows Holographic for Business nicht unterstützt.
- **Zugriff auf Downloadordner zulassen**: Wird unter Windows Holographic for Business nicht unterstützt.
- **Wartungsfenster für App-Neustarts angeben**: Wird unter Windows Holographic for Business nicht unterstützt.

## <a name="next-steps"></a>Nächste Schritte

[Zuweisen von Profilen](device-profile-assign.md) und [Überwachen von Profilen](device-profile-monitor.md)

Außerdem können Sie Kioskprofile für [Android](device-restrictions-android.md#kiosk)-, [Android Enterprise](device-restrictions-android-for-work.md#device-experience)- und [Windows 10](kiosk-settings-windows.md)-Geräte erstellen.
