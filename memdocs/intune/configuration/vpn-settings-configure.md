---
title: Hinzufügen von VPN-Einstellungen für Geräte in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Verwenden Sie auf Android-Geräteadministrator-, Android Enterprise-, iOS-, iPadOS-, macOS- und Windows-Geräten integrierte Einstellungen zum Erstellen von VPN-Verbindungen (virtuelles privates Netzwerk) in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/07/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1c92220fabf8d1cb2a34ac702dd4157ef848762b
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990263"
---
# <a name="create-vpn-profiles-to-connect-to-vpn-servers-in-intune"></a>Erstellen von VPN-Profilen zum Herstellen einer Verbindung mit VPN-Servern in Intune

Über virtuelle private Netzwerke (VPNs) erhalten Benutzer sicheren Remotezugriff auf Ihr Organisationsnetzwerk. Mithilfe eines VPN-Verbindungsprofils stellen Geräte eine Verbindung mit dem VPN-Server her. **VPN-Profile** in Microsoft Intune weisen VPN-Einstellungen zu Benutzern und Geräten in Ihrer Organisation zu. Verwenden Sie diese Einstellungen, damit Benutzer problemlos und sicher eine Verbindung mit Ihrem Organisationsnetzwerk herstellen können.

Angenommen, Sie möchten z. B. alle iOS-/iPadOS-Geräte mit den Einstellungen konfigurieren, die zum Herstellen einer Verbindung mit einer Dateifreigabe im Organisationsnetzwerk erforderlich sind. Erstellen Sie zunächst ein VPN-Profil, das diese Einstellungen enthält. Weisen Sie dieses Profil anschließend allen Benutzern zu, die über iOS-/iPadOS-Geräte verfügen. Die Benutzer sehen die VPN-Verbindung in der Liste der verfügbaren Netzwerke und können mit geringem Aufwand eine Verbindung herstellen.

> [!NOTE]
> Sie können [benutzerdefinierte Intune-Konfigurationsrichtlinien](custom-settings-configure.md) verwenden, um VPN-Profile für die folgenden Plattformen zu erstellen:
>
> * Android 4 und höher
> * Registrierte Geräte unter Windows 8.1 und höher
> * Windows Phone 8.1 und höher
> * Registrierte Geräte unter Windows 10 Desktop
> * Windows 10 Mobile
> * Windows Holographic for Business

## <a name="vpn-connection-types"></a>VPN-Verbindungstypen

Sie können VPN-Profile mit den folgenden Verbindungstypen erstellen:

- Automatisch
  - Windows 10

- Check Point Capsule VPN
  - Android-Geräteadministrator
  - Android Enterprise-Arbeitsprofile
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8.1
  - Windows Phone 8.1

- Cisco AnyConnect
  - Android-Geräteadministrator
  - Android Enterprise-Arbeitsprofile
  - Android Enterprise-Gerätebesitzer (vollständig verwaltet)
  - iOS/iPadOS
  - macOS

- Cisco (IPSec)
  - iOS/iPadOS

- Citrix SSO
  - Android-Geräteadministrator
  - Android Enterprise-Arbeitsprofile: Verwenden von [App-Konfigurationsrichtlinien](../apps/app-configuration-policies-use-android.md)
  - Android Enterprise-Gerätebesitzer (vollständig verwaltet): Verwenden von [App-Konfigurationsrichtlinien](../apps/app-configuration-policies-use-android.md)
  - iOS/iPadOS
  - Windows 10

- Benutzerdefiniertes VPN
  - iOS/iPadOS
  - macOS

  Erstellen benutzerdefinierter VPN-Profile mithilfe von URI-Einstellungen finden Sie unter [Erstellen eines Profils mit benutzerdefinierten Einstellungen in Intune](custom-settings-configure.md).

- F5 Access
  - Android-Geräteadministrator
  - Android Enterprise-Arbeitsprofile
  - Android Enterprise-Gerätebesitzer (vollständig verwaltet)
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8.1
  - Windows Phone 8.1

- IKEv2
  - iOS/iPadOS
  - Windows 10

- L2TP
  - Windows 10

- Palo Alto Networks GlobalProtect
  - Android Enterprise-Arbeitsprofile: Verwenden von [App-Konfigurationsrichtlinien](../apps/app-configuration-policies-use-android.md)
  - iOS/iPadOS
  - Windows 10

- PPTP
  - Windows 10

- Pulse Secure
  - Android-Geräteadministrator
  - Android Enterprise-Arbeitsprofile
  - Android Enterprise-Gerätebesitzer (vollständig verwaltet)
  - iOS/iPadOS
  - Windows 10
  - Windows 8.1
  - Windows Phone 8.1

- SonicWall Mobile Connect
  - Android-Geräteadministrator
  - Android Enterprise-Arbeitsprofile
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8.1
  - Windows Phone 8.1

- Zscaler
  - Android Enterprise-Arbeitsprofile: Verwenden von [App-Konfigurationsrichtlinien](../apps/app-configuration-policies-use-android.md)
  - iOS/iPadOS

> [!IMPORTANT]
> Vor der Verwendung von VPN-Profilen, die auf einem Gerät zugewiesen werden, müssen Sie die entsprechende VPN-App für das Profil installieren. Informationen dazu, wie Sie die App mit Intune zuweisen, finden Sie unter [Was ist die Microsoft Intune App-Verwaltung?](../apps/app-management.md).  

## <a name="create-the-profile"></a>Erstellen des Profils

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.
3. Geben Sie die folgenden Eigenschaften ein:

    - **Plattform**: Wählen Sie die Plattform Ihrer Geräte aus. Folgende Optionen sind verfügbar:
      - **Android-Geräteadministrator**
      - **Android Enterprise** > **Nur Gerätebesitzer**
      - **Android Enterprise** > **Nur Arbeitsprofil**
      - **iOS/iPadOS**
      - **macOS**
      - **Windows 10 und höher**
      - **Windows 8.1 und höher**
      - **Windows Phone 8.1**
    - **Profil**: Wählen Sie **VPN** aus.

4. Wählen Sie **Erstellen** aus.
5. Geben Sie in **Grundlagen** die folgenden Eigenschaften ein:

    - **Name:** Geben Sie einen aussagekräftigen Namen für das Profil ein. Benennen Sie Ihre Profile, damit Sie diese später leicht wiedererkennen. Ein geeigneter Profilname ist beispielsweise **VPN-Profil für das gesamte Unternehmen**.
    - **Beschreibung:** Geben Sie eine Beschreibung für das Profil ein. Diese Einstellung ist optional, wird jedoch empfohlen.

6. Wählen Sie **Weiter** aus.
7. Die verfügbaren **Konfigurationseinstellungen** variieren je nach ausgewählter Plattform. Wählen Sie Ihre Plattform aus, um auf die einzelnen Einstellungen zuzugreifen:

    - [Android-Geräteadministrator](vpn-settings-android.md)
    - [Android Enterprise](vpn-settings-android-enterprise.md)
    - [iOS/iPadOS](vpn-settings-ios.md)
    - [macOS](vpn-settings-macos.md)
    - [Windows 10](vpn-settings-windows-10.md) (einschließlich Windows Holographic for Business)
    - [Windows 8.1](vpn-settings-windows-8-1.md)
    - [Windows Phone 8.1](vpn-settings-windows-phone-8-1.md)

8. Wählen Sie **Weiter** aus.
9. Weisen Sie in **Bereichstags** (optional) ein Tag zu, um das Profil nach bestimmten IT-Gruppen wie `US-NC IT Team` oder `JohnGlenn_ITDepartment` zu filtern. Weitere Informationen zu Bereichstags finden Sie unter [Verwenden der RBAC und von Bereichstags für verteilte IT](../fundamentals/scope-tags.md).

    Wählen Sie **Weiter** aus.

10. Wählen Sie unter **Zuweisungen** die Benutzer oder Gruppen aus, denen das Profil zugewiesen werden soll. Weitere Informationen zum Zuweisen von Profilen finden Sie unter [Zuweisen von Benutzer- und Geräteprofilen](device-profile-assign.md).

    Wählen Sie **Weiter** aus.

11. Überprüfen Sie die Einstellungen unter **Überprüfen + erstellen**. Wenn Sie auf **Erstellen** klicken, werden die Änderungen gespeichert, und das Profil wird zugewiesen. Die Richtlinie wird auch in der Profilliste angezeigt.

## <a name="secure-your-vpn-profiles"></a>Sichern der VPN-Profile

VPN-Profile können eine Reihe verschiedener Verbindungstypen und Protokolle von unterschiedlichen Herstellern verwenden. Diese Verbindungen werden in der Regel mit den folgenden Methoden gesichert.

### <a name="certificates"></a>Zertifikate

Beim Erstellen des VPN-Profils wählen Sie ein SCEP- oder PKCS-Zertifikatprofil aus, das Sie zuvor in Intune erstellt haben. Dieses Profil wird als Identitätszertifikat bezeichnet. Es dient zur Authentifizierung anhand eines von Ihnen erstellten vertrauenswürdigen Zertifikatprofils (oder eines *Stammzertifikats*), das Sie erstellen, damit das Gerät des Benutzers eine Verbindung herstellen kann. Das vertrauenswürdige Zertifikat wird auf dem Computer zugewiesen, der die VPN-Verbindung authentifiziert, in der Regel ist dies der VPN-Server.

Wenn Sie die zertifikatbasierte Authentifizierung für Ihr VPN-Profil verwenden, stellen Sie das VPN-Profil, das Zertifikatprofil und das vertrauenswürdige Stammprofil für dieselben Gruppen bereit. Diese Zuweisung stellt sicher, dass jedes Gerät die Rechtmäßigkeit Ihrer Zertifizierungsstelle erkennt.

Weitere Informationen zum Erstellen und Verwenden von Zertifikatprofilen in Intune finden Sie unter [Konfigurieren von Zertifikaten mit Microsoft Intune](../protect/certificates-configure.md).

> [!NOTE]
> Zertifikate, die mit dem Profiltyp **Importierte PKCS-Zertifikate** hinzugefügt werden, werden für die VPN-Authentifizierung nicht unterstützt. Zertifikate, die mit dem Profiltyp **PKCS-Zertifikate** hinzugefügt werden, werden für die VPN-Authentifizierung unterstützt.


### <a name="user-name-and-password"></a>Benutzername und Kennwort

Der Benutzer authentifiziert sich beim VPN-Server durch Angabe seines Benutzernamens und Kennworts.

## <a name="next-steps"></a>Nächste Schritte

Das Profil ist nun erstellt, führt aber noch keine Aktionen durch. Die nächsten Schritte sind das [Zuweisen von Profilen](device-profile-assign.md) zu einigen Geräten und das [Überwachen ihres Status](device-profile-monitor.md).

Sie können auch Pro-App-VPNs für [Android-Geräteadministrator-/Android Enterprise](android-pulse-secure-per-app-vpn.md)- und [iOS-/iPadOS-Geräte](vpn-setting-configure-per-app.md) erstellen und verwenden.
