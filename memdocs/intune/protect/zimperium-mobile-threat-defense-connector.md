---
title: Zimperium MTD-Connector in Intune
titleSuffix: Intune on Azure
description: Informationen zum Integrieren von Zimperium Mobile Threat Defense in Intune, um den Zugriff von mobilen Geräten auf Ihre Unternehmensressourcen zu steuern.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/09/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 975d8d84-792a-41ad-925a-4a7f1ae4dcaf
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ed623abeb602e599866af7b7249756edd87d5a29
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79349198"
---
# <a name="zimperium-mobile-threat-defense-connector-with-intune"></a>Zimperium Mobile Threat Defense-Connector in Intune

Sie können den Zugriff mobiler Geräte auf Unternehmensressourcen mithilfe des bedingten Zugriffs basierend auf Risikobewertungen steuern, die von Zimperium vorgenommen werden, einer Mobile Threat Defense-Lösung (MTD), die in Microsoft Intune integriert werden kann. Das Risiko wird basierend auf Telemetriedaten von Geräten bewertet, auf denen die Zimperium-App ausgeführt wird.

Sie können Richtlinien für bedingten Zugriff basierend auf der Zimperium-Risikobewertung konfigurieren, die über Intune-Gerätekompatibilitätsrichtlinien für registrierte Geräte aktiviert wird, und so anhand der erkannten Bedrohungen den Zugriff auf Unternehmensressourcen durch nicht konforme Geräte zulassen oder blockieren. Für nicht registrierte Geräte können Sie App-Schutzrichtlinien verwenden, um das Blockieren oder ein selektives Löschen basierend auf erkannten Bedrohungen zu erzwingen.

## <a name="supported-platforms"></a>Unterstützte Plattformen

- **Android 4.1 und höher**

- **iOS 8 und höher**

## <a name="prerequisites"></a>Voraussetzungen

- Azure Active Directory Premium

- Microsoft Intune-Abonnement

- Zimperium Mobile Threat Defense-Abonnement

  - Weitere Informationen finden Sie auf der [Zimperium-Website](https://www.zimperium.com/zips-mobile-ips).

## <a name="how-do-intune-and-zimperium-help-protect-your-company-resources"></a>Wie helfen Intune und Zimperium beim Schutz von Unternehmensressourcen?

Die Zimperium-App für Android oder iOS/iPadOS erfasst Telemetriedaten des Dateisystems, Netzwerkstapels sowie von Geräten und Anwendungen, sofern verfügbar, und sendet diese dann an den Zimperium-Clouddienst, mit dessen Hilfe die Anfälligkeit des Geräts für mobile Bedrohungen bewertet wird.

- **Unterstützung für registrierte Geräte**: Die Intune-Gerätekonformitätsrichtlinie enthält eine Regel für Mobile Threat Defense (MTD), die Risikobewertungsinformationen aus Zimperium verwenden kann. Wenn die MTD-Regel aktiviert ist, bewertet Intune die Gerätekompatibilität mit der von Ihnen aktivierten Richtlinie. Wird das Gerät als nicht kompatibel eingestuft, wird der Zugriff auf Ressourcen wie Exchange Online und SharePoint Online für Benutzer blockiert. Benutzer erhalten zudem einen Leitfaden von der auf ihren Geräten installierten Zimperium-App, um das Problem zu beheben und den Zugriff auf Unternehmensressourcen zurückzuerlangen. So unterstützen Sie die Verwendung von Zimperium mit registrierten Geräten:
  - [Hinzufügen von MTD-Apps zu Geräten](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [Erstellen einer Gerätekonformitätsrichtlinie mit MTD-Unterstützung](../protect/mtd-device-compliance-policy-create.md)
  - [Aktivieren des MTP-Connectors in Intune](../protect/mtd-connector-enable.md)

- **Unterstützung für nicht registrierte Geräte**: Intune kann die Risikobewertungsdaten der Zimperium-App auf nicht registrierten Geräten verwenden, wenn Sie Intune-App-Schutzrichtlinien verwenden. Administratoren können diese Kombination verwenden, um Unternehmensdaten in einer [durch Microsoft Intune geschützten App](../apps/apps-supported-intune-apps.md) zu schützen. Sie können zudem initiieren, dass Unternehmensdaten auf nicht registrierten Geräten blockiert oder teilweise gelöscht werden. So unterstützen Sie die Verwendung von Zimperium mit nicht registrierten Geräten:
  - [Hinzufügen der MTD-App zu nicht registrierten Geräten](../protect/mtd-add-apps-unenrolled-devices.md)
  - [Erstellen einer Mobile Threat Defense-App-Schutzrichtlinie (MTD)](../protect/mtd-app-protection-policy.md)
  - [Aktivieren des MTD-Connectors in Intune für nicht registrierte Geräte](../protect/mtd-enable-unenrolled-devices.md)
  
## <a name="sample-scenarios"></a>Beispielszenarios

Nachstehend finden Sie einige Szenarios für die Integration von Zimperium in Intune:

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Steuern des Zugriffs basierend auf Bedrohungen durch Apps, die Schadsoftware enthalten

Wenn Apps, die Schadsoftware enthalten, auf Geräten erkannt werden, können Sie Geräte blockieren, bis die Bedrohung beseitigt ist:

- Herstellen einer Verbindung mit Unternehmens-E-Mail

- Synchronisieren von Unternehmensdateien mithilfe der OneDrive for Work-App

- Zugreifen auf Unternehmens-Apps

*Blockieren, wenn Apps mit Schadsoftware entdeckt werden:*

> [!div class="mx-imgBorder"]
> ![Darstellung des Szenarios, wenn Apps mit Schadsoftware erkannt werden](./media/zimperium-mobile-threat-defense-connector/Maliciousapps-blocked-zimperium.png)

*Zugriff nach Beseitigung gewährt:*

> [!div class="mx-imgBorder"]
> ![Darstellung des Szenarios, wenn der Zugriff nach der Behebung wieder erteilt wird](./media/zimperium-mobile-threat-defense-connector/maliciousapps-unblocked-zimperium.png)

### <a name="control-access-based-on-threat-to-network"></a>Steuern des Zugriffs basierend auf Bedrohung für das Netzwerk

Erkennen Sie Bedrohungen wie **Man-in-the-Middle** im Netzwerk, und schützen Sie den Zugriff auf WLAN-Netzwerke auf der Grundlage des Geräterisikos.

*Blockieren des Netzwerkzugriffs über WLAN:*

> [!div class="mx-imgBorder"]
> ![Blockieren des Netzwerkzugriffs über WLAN](./media/zimperium-mobile-threat-defense-connector/network-wifi-blocked-zimperium.png)

*Zugriff nach Beseitigung gewährt:*

> [!div class="mx-imgBorder"]
> ![Zugriff erteilt nach der Behebung](./media/zimperium-mobile-threat-defense-connector/network-wifi-unblocked-zimperium.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Steuern des Zugriffs auf SharePoint Online basierend auf Netzwerkbedrohungen

Erkennen von Bedrohungen wie **Man-in-the-Middle** im Netzwerk und Verhindern der Synchronisierung von Unternehmensdateien auf der Grundlage des Geräterisikos.

*Blockieren des Zugriffs auf SharePoint Online bei Erkennen von Bedrohungen für das Netzwerk*

> [!div class="mx-imgBorder"]
> ![Blockieren von SharePoint Online bei Erkennung von Bedrohungen für das Netzwerk](./media/zimperium-mobile-threat-defense-connector/network-spo-blocked-zimperium.png)

*Zugriff nach Beseitigung gewährt:*

> [!div class="mx-imgBorder"]
> ![Zugriff erteilt nach der Behebung für SharePoint – Beispiel](./media/zimperium-mobile-threat-defense-connector/network-spo-unblocked-zimperium.png)

### <a name="control-access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>Steuern des Zugriffs auf nicht registrierte Geräte bei Bedrohungen durch böswillige Apps

Wenn die MTD-Lösung von Zimperium ein Gerät für infiziert hält:

> [!div class="mx-imgBorder"]
> ![App-Schutzrichtlinie blockiert Zugriff aufgrund erkannter Schadsoftware](./media/zimperium-mobile-threat-defense-connector/zimperium-mobile-app-policy-block.png)

Nach der Behebung wird der Zugriff wieder erteilt:

> [!div class="mx-imgBorder"]
> ![Zugriff wird nach Behebung durch die App-Schutzrichtlinie wieder gewährt](./media/zimperium-mobile-threat-defense-connector/zimperium-mobile-app-policy-remediated.png)

## <a name="next-steps"></a>Nächste Schritte

- [Integrate Zimperium with Intune (Integrieren von Zimperium in Intune)](zimperium-mtd-connector-integration.md)

- [Einrichten von Zimperium-Apps](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Erstellen einer Zimperium-Gerätekompatibilitätsrichtlinie](mtd-device-compliance-policy-create.md)

- [Aktivieren des Zimperium MTD-Connectors](mtd-connector-enable.md)

- [Erstellen einer Mobile Threat Defense-App-Schutzrichtlinie (MTD) mit Intune](../protect/mtd-app-protection-policy.md)
