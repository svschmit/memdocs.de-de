---
title: Verwenden von VPN-Einstellungen für Android Enterprise in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Lernen Sie alle Einstellungen kennen, die Sie zum Erstellen von VPN-Verbindungen auf Android Enterprise-Geräten in Microsoft Intune benötigen. Geben Sie den Namen der Verbindung und die IP-Adresse oder FQDN des VPN-Servers ein. Wählen Sie die Art der Authentifizierung von Benutzern sowie die Verbindungstypen Citrix, SonicWall, Check Point Capsule und Pulse Secure aus.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3981f40650544cdfdbfd0208e127a3e0aaecb823
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2020
ms.locfileid: "86462013"
---
# <a name="android-enterprise-device-settings-to-configure-vpn-in-intune"></a>Android Enterprise-Geräteeinstellungen zur VPN-Konfiguration in Intune

In diesem Artikel werden die verschiedenen VPN-Verbindungseinstellungen aufgeführt und beschrieben, die Sie auf Android Enterprise-Geräten steuern können. Verwenden Sie diese Einstellungen als Teil Ihrer MDM-Lösung (Mobile Device Management, Verwaltung mobiler Geräte), um etwa eine VPN-Verbindung zu erstellen und die Art der Authentifizierung sowie den VPN-Servertyp auszuwählen.

Als Intune-Administrator können Sie für Ihre Android Enterprise-Geräte VPN-Einstellungen erstellen und ihnen zuweisen. 

Weitere Informationen zu VPN-Profilen in Intune finden Sie unter [VPN-Profile](vpn-settings-configure.md).

> [!NOTE]
> Erstellen Sie zur Konfiguration des Always On-VPN ein VPN-Profil sowie ein Profil für [Geräteeinschränkungen](device-restrictions-android-for-work.md#connectivity) mit konfigurierter Always On-VPN-Einstellung.

## <a name="before-you-begin"></a>Vorbereitung

[Erstellen Sie ein Gerätekonfigurationsprofil](vpn-settings-configure.md), und klicken Sie auf **Android Enterprise**.

## <a name="fully-managed-dedicated-and-corporate-owned-work-profile"></a>Vollständig verwaltet, dediziert und unternehmenseigen mit einem Arbeitsprofil

- **Verbindungsname**: Geben Sie einen Namen für diese Verbindung ein. Benutzern wird dieser Name angezeigt, wenn sie auf ihrem Gerät die verfügbaren VPN-Verbindungen durchsuchen. Geben Sie beispielsweise `Contoso VPN` ein.
- **IP-Adresse oder FQDN:** Geben Sie die IP-Adresse oder den vollqualifizierten Domänennamen (FQDN) des VPN-Servers ein, mit dem Geräte eine Verbindung herstellen. Geben Sie beispielsweise **192.168.1.1** oder **vpn.contoso.com** ein.

  - **Authentifizierungsmethode:** Wählen Sie aus, wie sich Geräte beim VPN-Server authentifizieren. Folgende Optionen sind verfügbar:
  
    - **Zertifikate:** Wählen ein vorhandenes SCEP- oder PKCS-Zertifikatprofil zum Authentifizieren der Verbindung aus. Unter [Konfigurieren eines Zertifikatprofils](../protect/certificates-configure.md) werden die Schritte aufgeführt, die zum Erstellen eines Zertifikatprofils erforderlich sind.
    - **Benutzername und Kennwort:** Endbenutzer werden bei der Anmeldung beim VPN-Server dazu aufgefordert, ihren Benutzernamen und ein Kennwort einzugeben.

- **Verbindungstyp:** Wählen Sie den VPN-Verbindungstyp aus. Folgende Optionen sind verfügbar:

  - **Cisco AnyConnect**
  - **F5 Access**
  - **Pulse Secure**

## <a name="work-profile-only"></a>Nur Arbeitsprofil

- **Verbindungsname**: Geben Sie einen Namen für diese Verbindung ein. Benutzern wird dieser Name angezeigt, wenn sie auf ihrem Gerät die verfügbaren VPN-Verbindungen durchsuchen. Geben Sie beispielsweise `Contoso VPN` ein.
- **IP-Adresse oder FQDN:** Geben Sie die IP-Adresse oder den vollqualifizierten Domänennamen (FQDN) des VPN-Servers ein, mit dem Geräte eine Verbindung herstellen. Geben Sie beispielsweise **192.168.1.1** oder **vpn.contoso.com** ein.

  - **Authentifizierungsmethode:** Wählen Sie aus, wie sich Geräte beim VPN-Server authentifizieren. Folgende Optionen sind verfügbar:
  
    - **Zertifikate:** Wählen ein vorhandenes SCEP- oder PKCS-Zertifikatprofil zum Authentifizieren der Verbindung aus. Unter [Konfigurieren eines Zertifikatprofils](../protect/certificates-configure.md) werden die Schritte aufgeführt, die zum Erstellen eines Zertifikatprofils erforderlich sind.
    - **Benutzername und Kennwort:** Endbenutzer werden bei der Anmeldung beim VPN-Server dazu aufgefordert, ihren Benutzernamen und ein Kennwort einzugeben.

- **Verbindungstyp:** Wählen Sie den VPN-Verbindungstyp aus. Folgende Optionen sind verfügbar:

  - **Cisco AnyConnect**
  - **F5 Access**
  - **Pulse Secure**
  - **SonicWall Mobile Connect**
  - **Check Point Capsule VPN**

## <a name="next-steps"></a>Nächste Schritte

[Zuweisen von Profilen](device-profile-assign.md) und [Überwachen von Profilen](device-profile-monitor.md)

Sie können VPN-Profile auch für Geräte erstellen, die unter [Android](vpn-settings-android.md), [iOS/iPadOS](vpn-settings-ios.md), [macOS](vpn-settings-macos.md), [Windows 10 und höher](vpn-settings-windows-10.md), [Windows 8.1](vpn-settings-windows-8-1.md) sowie [Windows Phone 8.1](vpn-settings-windows-phone-8-1.md) ausgeführt werden.
