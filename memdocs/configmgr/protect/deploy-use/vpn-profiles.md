---
title: VPN-Profile
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie VPN-Profile in Configuration Manager verwenden, um Benutzern in Ihrer Organisation Einstellungen für VPN bereitzustellen.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: c0f094f1-852e-4606-91db-97846d8f0772
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9463d857599e676da6267313df575c8881436f93
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706248"
---
# <a name="vpn-profiles-in-configuration-manager"></a>VPN-Profile in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

<!--1283610-->
Verwenden Sie VPN-Profile in Configuration Manager, um Benutzern in Ihrer Organisation Einstellungen für VPN bereitzustellen. Durch Bereitstellen dieser Einstellungen erleichtern Sie dem Endbenutzer das Verbinden mit Ressourcen im Unternehmensnetzwerk.  

Möglicherweise möchten Sie z. B. alle Windows 10-Geräte mit den Einstellungen konfigurieren, die zum Verbinden mit einer Dateifreigabe im internen Netzwerk erforderlich sind. Erstellen Sie ein VPN-Profil mit den Einstellungen, die zum Herstellen einer Verbindung mit dem internen Netzwerk erforderlich sind. Stellen Sie dieses Profil anschließend für alle Benutzer bereit, die über Windows 10-Geräte verfügen. Diese Benutzer sehen die VPN-Verbindung in der Liste der verfügbaren Netzwerke und können mit geringem Aufwand eine Verbindung herstellen.

Wenn Sie ein VPN-Profil erstellen, können Sie eine Vielzahl von Sicherheitseinstellungen einrichten. Zu diesen Einstellungen gehören Zertifikate für die Serverüberprüfung und die Clientauthentifizierung, die mithilfe von Configuration Manager-Zertifikatprofilen bereitgestellt wurden. Weitere Informationen finden Sie unter [Zertifikatprofile](introduction-to-certificate-profiles.md).

> [!Note]
> Configuration Manager aktiviert dieses optionale Feature nicht automatisch. Sie müssen dieses Feature aktivieren, bevor Sie es verwenden. Weitere Informationen finden Sie unter [Enable optional features from updates (Aktivieren optionaler Features von Updates)](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

## <a name="supported-platforms"></a>Unterstützte Plattformen

Die folgende Tabelle beschreibt die VPN-Profile, die Sie für verschiedene Geräteplattformen konfigurieren können.

|Verbindungstyp|Windows 8.1|Windows RT|Windows RT 8.1|Windows 10|
|---------------|-----------|----------|--------------|----------|
|**Pulse Secure**|Ja|Nein|Ja|Ja|
|**F5 Edge Client**|Ja|Nein|Ja|Ja|
|**Dell SonicWALL Mobile Connect**|Ja|Nein|Ja|Ja|
|**Prüfpunkt für mobiles VPN**|Ja|Nein|Ja|Ja|
|**Microsoft SSL (SSTP)**|Ja|Ja|Ja|Nein|
|**Microsoft Automatic**|Ja|Ja|Ja|Nein|
|**IKEv2**|Ja|Ja|Ja|Nein|
|**PPTP**|Ja|Ja|Ja|Nein|
|**L2TP**|Ja|Ja|Ja|Nein|

## <a name="next-step"></a>Nächster Schritt

> [!div class="nextstepaction"]
> [Erstellen von VPN-Profilen](create-vpn-profiles.md)

## <a name="see-also"></a>Weitere Informationen:

- [Voraussetzungen für VPN-Profile](../plan-design/prerequisites-for-wifi-vpn-profiles.md)

- [Sicherheit und Datenschutz für VPN-Profile](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
