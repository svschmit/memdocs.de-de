---
title: Erstellen eines WLAN-Profils für Geräte in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie ein WLAN-Gerätekonfigurationsprofil in Microsoft Intune erstellen. Erstellen Sie Profile für Android-Geräteadministrator, Android Enterprise, Android-Kiosk, iOS, iPadOS, macOS, Windows 10 und höher sowie für Windows Holographic for Business. Verwenden Sie diese Profile, um beispielsweise eine WLAN-Verbindung zu erstellen, um Zertifikate zu verwenden, einen EAP-Typ und eine Authentifizierungsmethode auszuwählen oder einen Proxy zu aktivieren.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: maholdaa
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 25b07dcbb76f6d4a8aae964d0123a880d179784e
ms.sourcegitcommit: 2e0bc4859f7e27dea20c6cc59d537a31f086c019
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/21/2020
ms.locfileid: "86871932"
---
# <a name="add-and-use-wi-fi-settings-on-your-devices-in-microsoft-intune"></a>Hinzufügen und Verwenden von WLAN-Einstellungen auf Microsoft Intune-Geräten

WLAN ist ein drahtloses Netzwerk, das von vielen mobilen Geräten verwendet wird, um Zugriff auf das Netzwerk zu erhalten. Microsoft Intune umfasst integrierte WLAN-Einstellungen, die für Benutzer und Geräte in Ihrer Organisation bereitgestellt werden können. Diese Gruppe von Einstellungen wird als „Profil“ bezeichnet und kann verschiedenen Benutzern und Gruppen zugewiesen werden. Nach der Zuweisung können Ihre Benutzer Zugriff auf das WLAN Ihrer Organisation erhalten, ohne es selbst zu konfigurieren.

Angenommen, Sie installieren ein neues WLAN mit dem Namen „Contoso-WLAN“. Daraufhin sollten Sie alle iOS-/iPadOS-Geräte so einrichten, dass sie sich mit diesem Netzwerk verbinden. Gehen Sie dazu folgendermaßen vor:

1. Erstellen Sie ein WLAN-Profil mit den Einstellungen zum Herstellen der Verbindung mit dem Drahtlosnetzwerk „Contoso-WLAN“.
2. Weisen Sie das Profil einer Gruppe zu, die alle Benutzer von iOS-/iPadOS-Geräten enthält.
3. Benutzer finden das neue WLAN von Contoso in der Liste der Drahtlosnetzwerke auf ihrem Gerät. Sie können sich dann über die von Ihnen ausgewählte Authentifizierungsmethode mit dem Netzwerk verbinden.

In diesem Artikel sind die Schritte zum Erstellen eines WLAN-Profils aufgelistet. Darüber hinaus enthält er Links, in denen die verschiedenen Einstellungen für die einzelnen Plattformen beschrieben werden.

## <a name="supported-device-platforms"></a>Unterstützte Geräteplattformen

WLAN-Profile unterstützen folgende Geräteplattformen:

- Android 5 und neuer
- Android Enterprise und -Kiosk
- iOS 11.0 und neuer
- iOS 13.0 und höher
- macOS X 10.12 und neuer
- Windows 10 und höher, Windows 10 Mobile und Windows Holographic for Business

> [!NOTE]
> Auf Geräten mit Windows 8.1 können Sie eine WLAN-Konfiguration importieren, die zuvor von einem anderen Gerät exportiert wurde.

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

    - **Profil**: Wählen Sie **WLAN** aus.

      > [!TIP]
      >
      > - Klicken Sie für **Android Enterprise**-Geräte, die als dedizierte Geräte (Kiosk) ausgeführt werden, auf **Vollständig verwaltetes, dediziertes und unternehmenseigenes Arbeitsprofil** > **WLAN**.
      > - Für **Windows 8.1 und neuer** können Sie **WLAN (Import)** auswählen. Mit dieser Option können Sie WLAN-Einstellungen als XML-Datei importieren, die Sie zuvor von einem anderen Gerät exportiert haben.

4. Wählen Sie **Erstellen** aus.
5. Geben Sie in **Grundlagen** die folgenden Eigenschaften ein:

    - **Name:** Geben Sie einen aussagekräftigen Namen für das Profil ein. Benennen Sie Ihre Profile, damit Sie diese später leicht wiedererkennen. Ein angemessener Profilname ist beispielsweise **WLAN-Profil für das gesamte Unternehmen**.
    - **Beschreibung:** Geben Sie eine Beschreibung für das Profil ein. Diese Einstellung ist optional, wird jedoch empfohlen.

6. Wählen Sie **Weiter** aus.
7. Die verfügbaren **Konfigurationseinstellungen** variieren je nach ausgewählter Plattform. Wählen Sie Ihre Plattform aus, um auf die einzelnen Einstellungen zuzugreifen:

    - [Android-Geräteadministrator](wi-fi-settings-android.md)
    - [Android Enterprise](wi-fi-settings-android-enterprise.md), einschließlich dedizierter Geräte
    - [iOS/iPadOS](wi-fi-settings-ios.md)
    - [macOS](wi-fi-settings-macos.md)
    - [Windows 10 und höher](wi-fi-settings-windows.md)
    - [Windows 8.1 und neuer](wi-fi-settings-import-windows-8-1.md) (einschließlich Windows Holographic for Business)

8. Wählen Sie **Weiter** aus.
9. Weisen Sie in **Bereichstags** (optional) ein Tag zu, um das Profil nach bestimmten IT-Gruppen wie `US-NC IT Team` oder `JohnGlenn_ITDepartment` zu filtern. Weitere Informationen zu Bereichstags finden Sie unter [Verwenden der RBAC und von Bereichstags für verteilte IT](../fundamentals/scope-tags.md).

    Wählen Sie **Weiter** aus.

10. Wählen Sie unter **Zuweisungen** die Benutzer oder Gruppen aus, denen das Profil zugewiesen werden soll. Weitere Informationen zum Zuweisen von Profilen finden Sie unter [Zuweisen von Benutzer- und Geräteprofilen](device-profile-assign.md).

    Wählen Sie **Weiter** aus.

11. Überprüfen Sie die Einstellungen unter **Überprüfen + erstellen**. Wenn Sie auf **Erstellen** klicken, werden die Änderungen gespeichert, und das Profil wird zugewiesen. Die Richtlinie wird auch in der Profilliste angezeigt.

> [!TIP]
> Wenn Sie die zertifikatbasierte Authentifizierung für Ihr WLAN-Profil verwenden, stellen Sie das WLAN-Profil, das Zertifikatprofil und das vertrauenswürdige Stammprofil für die gleichen Gruppen bereit, um sicherzustellen, dass jedes Gerät die Rechtmäßigkeit Ihrer Zertifizierungsstelle erkennen kann.  Weitere Informationen finden Sie unter [Verwenden von Zertifikaten zur Authentifizierung in Microsoft Intune](../protect/certificates-configure.md).

## <a name="next-steps"></a>Nächste Schritte

Das Profil ist nun erstellt, führt aber möglicherweise keine Aktionen durch. Die nächsten Schritte sind das [Zuweisen dieses Profils](device-profile-assign.md) und das [Überwachen seines Status](device-profile-monitor.md).

[Problembehandlung für WLAN-Profile in Intune](troubleshoot-wi-fi-profiles.md)
