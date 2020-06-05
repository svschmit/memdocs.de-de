---
title: Kioskeinstellungen für Windows- und Holographic-Geräte in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Konfigurieren Sie Ihre Windows 10- (und höher) sowie Windows Holographic for Business-Geräte als Kiosks mit einer App oder mehreren Apps, und passen Sie das Startmenü an, fügen Sie Apps hinzu, zeigen Sie die Taskleiste an und konfigurieren Sie einen Webbrowser in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: a9be644a47a361cf29e7b7132b2c87a4921553ea
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989431"
---
# <a name="windows-10-and-windows-holographic-for-business-device-settings-to-run-as-a-dedicated-kiosk-using-intune"></a>Geräteeinstellungen bei Windows 10 und Windows Holographic for Business zur Ausführung als dedizierter Kiosk mit Intune

Verwenden Sie Intune, um Geräte mit Windows 10 als Kiosk auszuführen. Diese werden manchmal auch als dedizierte Geräte bezeichnet. Auf einem Gerät im Kioskmodus können eine oder mehrere Apps ausgeführt werden. Sie können ein Startmenü anzeigen und anpassen, verschiedene Apps hinzufügen, einschließlich Win32-Anwendungen, einem Webbrowser eine bestimmte Startseite hinzufügen und vieles mehr. 

Diese Funktion gilt für:

- Windows 10 und höher
- Windows Holographic for Business

Informationen zum Erstellen von Kioskprofilen für andere Plattformen finden Sie in den Abschnitten [Android-Geräteadministrator](device-restrictions-android.md#kiosk), [Android Enterprise](device-restrictions-android-for-work.md#dedicated-devices) und [iOS/iPadOS](device-restrictions-ios.md#kiosk).

Intune unterstützt ein Kioskprofil pro Gerät. Wenn Sie mehrere Kioskprofile auf einem einzelnen Gerät benötigen, können Sie einen [benutzerdefinierten OMA-URI](custom-settings-windows-10.md) verwenden.

Intune verwendet „Konfigurationsprofile“ zum Erstellen und Anpassen dieser Einstellungen für die Anforderungen Ihrer Organisation. Nachdem Sie diese Funktionen in einem Profil hinzugefügt haben, übertragen Sie diese Einstellungen mithilfe von Push auf Gruppen in Ihrer Organisation, oder stellen Sie sie für Gruppen bereit.

In diesem Artikel erfahren Sie, wie Sie ein Gerätekonfigurationsprofil erstellen. Eine Liste mit allen Einstellungen und ihren Funktionen finden Sie unter [Windows 10-Kioskeinstellungen](kiosk-settings-windows.md) und [Windows Holographic for Business-Geräteinstellungen zur Ausführung als Kiosk](kiosk-settings-holographic.md).

## <a name="create-the-profile"></a>Erstellen des Profils

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.
3. Geben Sie die folgenden Eigenschaften ein:

   - **Plattform**: Wählen Sie **Windows 10 und höher** aus.
   - **Profil**: Klicken Sie auf **Kiosk**.

4. Wählen Sie **Erstellen** aus.
5. Geben Sie in **Grundlagen** die folgenden Eigenschaften ein:

   - **Name:** Geben Sie einen aussagekräftigen Namen für das neue Profil ein.
   - **Beschreibung:** Geben Sie eine Beschreibung für das Profil ein. Diese Einstellung ist optional, wird jedoch empfohlen.

6. Wählen Sie **Weiter** aus.
7. Wählen Sie unter **Konfigurationseinstellungen** > **Kioskmodus auswählen** den Typ von Kioskmodus aus, der von der Richtlinie unterstützt wird. Zu den Optionen gehören:

    - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Durch die Richtlinie kann der Kioskmodus nicht aktiviert werden.
    - **Einzelne App, Vollbildkiosk:** Das Gerät wird mit einem einzelnen Benutzerkonto ausgeführt und kann nur auf eine einzige Store-App zugreifen. Wenn sich der Benutzer anmeldet, wird so eine bestimmte App gestartet. Dieser Modus hindert den Benutzer auch daran, neue Apps zu öffnen oder die App zu ändern, die ausgeführt wird.
    - **Kiosk mit mehreren Apps:** Das Gerät führt mehrere Store-Apps, Win32-Apps oder Windows-Posteingangs-Apps unter Verwendung der Anwendungsbenutzermodell-ID (AUMID) aus. Nur die von Ihnen hinzugefügten Apps sind auf dem Gerät verfügbar.

        Der Vorteil eines Kiosks mit mehreren Apps oder eines Geräts mit festem Zweck ist ein leicht verständlicher Prozess für die Benutzer, da diese nur auf die Apps zugreifen, die sie benötigen. Zudem werden Apps, die Benutzer nicht benötigen, aus der Ansicht entfernt.

    Eine Liste aller Einstellungen und ihrer Funktionen finden Sie unter:

      - [Windows 10-Kioskeinstellungen](kiosk-settings-windows.md)
      - [Windows Holographic for Business-Geräteinstellungen zur Ausführung als Kiosk](kiosk-settings-holographic.md)

8. Wählen Sie **Weiter** aus.

9. Weisen Sie in **Bereichstags** (optional) ein Tag zu, um das Profil nach bestimmten IT-Gruppen wie `US-NC IT Team` oder `JohnGlenn_ITDepartment` zu filtern. Weitere Informationen zu Bereichstags finden Sie unter [Verwenden der RBAC und von Bereichstags für verteilte IT](../fundamentals/scope-tags.md).

    Wählen Sie **Weiter** aus.

10. Wählen Sie unter **Zuweisungen** die Benutzer oder Benutzergruppen aus, denen Ihr Profil zugewiesen werden soll. Weitere Informationen zum Zuweisen von Profilen finden Sie unter [Zuweisen von Benutzer- und Geräteprofilen](device-profile-assign.md).

    Wählen Sie **Weiter** aus.

11. Überprüfen Sie die Einstellungen unter **Überprüfen + erstellen**. Wenn Sie auf **Erstellen** klicken, werden die Änderungen gespeichert, und das Profil wird zugewiesen. Die Richtlinie wird auch in der Profilliste angezeigt.

Wenn die Geräte das nächste Mal einchecken, wird die Richtlinie angewendet.

## <a name="next-steps"></a>Nächste Schritte

[Überwachen Sie den Profilstatus](device-profile-monitor.md), [nachdem das Profil zugewiesen wurde](device-profile-assign.md).

Sie können Kioskprofile für Geräte erstellen, die die folgenden Plattformen ausführen:

- [Android-Geräteadministrator](device-restrictions-android.md#kiosk)
- [Android Enterprise](device-restrictions-android-for-work.md#dedicated-devices)
- [Windows 10 und höher](kiosk-settings-windows.md)
- [Windows Holographic for Business](kiosk-settings-holographic.md)
