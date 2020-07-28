---
title: Integrieren von Lookout Mobile Endpoint Security mit Microsoft Intune
titleSuffix: Microsoft Intune
description: Informationen zum Integrieren von Intune mit Lookout Mobile Threat Defense (MTD), um den Zugriff von mobilen Geräten auf Ihre Unternehmensressourcen zu steuern.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3a730a5d-2a90-42b0-aa28-aadfc7a18788
ms.reviewer: davera
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9bf06c5057cecd63b5717440eba8bad0542ab642
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461316"
---
# <a name="lookout-mobile-endpoint-security-connector-with-intune"></a>Lookout Mobile Endpoint Security-Connector mit Intune

Sie können den Zugriff mobiler Geräte auf Unternehmensressourcen basierend auf Risikobewertungen steuern, die von Lookout vorgenommen werden, einer Mobile Threat Defense-Lösung, die in Microsoft Intune integriert ist. Das Risiko wird basierend auf Telemetriedaten bewertet, die vom Lookout-Dienst auf Geräten erfasst werden, wie z.B.:
- Sicherheitsrisiken des Betriebssystems
- Installierte Apps, die Schadsoftware enthalten
- Netzwerkprofile mit böswilligen Absichten

Sie können Richtlinien für bedingten Zugriff basierend auf der Lookout-Risikobewertung konfigurieren, die über Intune-Kompatibilitätsrichtlinien für registrierte Geräte aktiviert wird, und so anhand der erkannten Bedrohungen den Zugriff auf Unternehmensressourcen durch nicht konforme Geräte zulassen oder blockieren. Für nicht registrierte Geräte können Sie App-Schutzrichtlinien verwenden, um das Blockieren oder ein selektives Löschen basierend auf erkannten Bedrohungen zu erzwingen.

## <a name="how-do-intune-and-lookout-mobile-endpoint-security-help-protect-company-resources"></a>Wie unterstützen Intune und Lookout Mobile Endpoint Security den Schutz von Unternehmensressourcen?

Die mobile Lookout-App **Lookout for Work** wird auf Mobilgeräten installiert und ausgeführt. Diese App erfasst Telemetriedaten des Dateisystems, Netzwerkstapels sowie von Geräten und Anwendungen, sofern verfügbar, und sendet diese dann an den Lookout-Clouddienst, mit dessen Hilfe die Anfälligkeit des Geräts für mobile Bedrohungen bewertet wird. Sie können die Klassifizierung der Risikostufe für Bedrohungen in der Lookout-Konsole gemäß Ihren Anforderungen ändern.

- **Unterstützung für registrierte Geräte**: Die Intune-Gerätekonformitätsrichtlinie enthält eine Regel für Mobile Threat Defense (MTD), die Risikobewertungsinformationen aus Lookout for Work verwenden kann. Wenn die MTD-Regel aktiviert ist, bewertet Intune die Gerätekompatibilität mit der von Ihnen aktivierten Richtlinie. Wird das Gerät als nicht kompatibel eingestuft, wird der Zugriff auf Ressourcen wie Exchange Online und SharePoint Online für Benutzer blockiert. Benutzer erhalten außerdem einen Leitfaden von der auf ihren Geräten installierten Lookout for Work-App, um das Problem zu beheben und den Zugriff auf Unternehmensressourcen zurückzuerlangen. So unterstützen Sie die Verwendung von Lookout for Work für registrierte Geräte:
  - [Hinzufügen von MTD-Apps zu Geräten](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [Erstellen einer Gerätekonformitätsrichtlinie mit MTD-Unterstützung](../protect/mtd-device-compliance-policy-create.md)
  - [Aktivieren des MTP-Connectors in Intune](../protect/mtd-connector-enable.md)

- **Unterstützung für nicht registrierte Geräte**: Intune kann die Risikobewertungsdaten der Lookout for Work-App auf nicht registrierten Geräten verwenden, wenn Sie Intune-App-Schutzrichtlinien verwenden. Administratoren können diese Kombination verwenden, um Unternehmensdaten in einer [durch Microsoft Intune geschützten App](../apps/apps-supported-intune-apps.md) zu schützen. Sie können zudem initiieren, dass Unternehmensdaten auf nicht registrierten Geräten blockiert oder teilweise gelöscht werden. So unterstützen Sie die Verwendung von Lookout for Work für nicht registrierte Geräte:
  - [Hinzufügen der MTD-App zu nicht registrierten Geräten](../protect/mtd-add-apps-unenrolled-devices.md)
  - [Erstellen einer Mobile Threat Defense-App-Schutzrichtlinie (MTD)](../protect/mtd-app-protection-policy.md)
  - [Aktivieren des MTD-Connectors in Intune für nicht registrierte Geräte](../protect/mtd-enable-unenrolled-devices.md)

## <a name="supported-platforms"></a>Unterstützte Plattformen

Bei Registrierung in Intune werden die folgenden Plattformen für Lookout unterstützt:

- **Android 4.1 und höher**  
- **iOS 8 und höher**  

Weitere Informationen zur Plattform- und Sprachunterstützung finden Sie auf der [Lookout-Website](https://personal.support.lookout.com/hc/articles/114094140253).  

## <a name="prerequisites"></a>Voraussetzungen

- Ein Enterprise-Abonnement für Lookout Mobile EndPoint Security.  
- Microsoft Intune-Abonnement
- Azure Active Directory Premium
- Enterprise Mobility + Security (EMS) E3 oder E5 mit Lizenzen, die Benutzern zugewiesen wurden.  

Weitere Informationen finden Sie unter [Lookout Mobile Endpoint Security](https://www.lookout.com/products/mobile-endpoint-security)

## <a name="sample-scenarios"></a>Beispielszenarios

Im Folgenden finden Sie allgemeine Szenarien für die Verwendung von Mobile Endpoint Security mit Intune.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Steuern des Zugriffs basierend auf Bedrohungen durch Apps, die Schadsoftware enthalten

Wenn Apps, die Schadsoftware enthalten, auf Geräten erkannt werden, können Sie Geräte an folgenden Aktionen hindern, bis die Bedrohung beseitigt ist:

- Herstellen einer Verbindung mit Unternehmens-E-Mail
- Synchronisieren von Unternehmensdateien mithilfe der OneDrive for Work-App
- Zugreifen auf Unternehmens-Apps

*Blockieren, wenn Apps mit Schadsoftware entdeckt werden:*

> [!div class="mx-imgBorder"]
> ![Darstellung der Richtlinie, die den Zugriff aufgrund von Apps mit Schadsoftware blockiert](./media/lookout-mobile-threat-defense-connector/malicious-apps-blocked.png)

*Zugriff nach Beseitigung gewährt:*

> [!div class="mx-imgBorder"]
> ![Darstellung des gewährten Zugriffs auf Geräte nach der Beseitigung](./media/lookout-mobile-threat-defense-connector/malicious-apps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>Steuern des Zugriffs basierend auf Bedrohung für das Netzwerk

Erkennen Sie Bedrohungen Ihres Netzwerks, wie etwa Man-in-the-Middle-Angriffe, und Schützen Sie den Zugriff auf WLANs auf der Grundlage des Geräterisikos.

*Blockieren des Netzwerkzugriffs über WLAN:*

> [!div class="mx-imgBorder"]
> ![Darstellung des blockierten WLAN-Zugriffs basierend auf Netzwerkbedrohungen](./media/lookout-mobile-threat-defense-connector/network-wifi-blocked.png)

*Zugriff nach Beseitigung gewährt:*

> [!div class="mx-imgBorder"]
> ![Darstellung des bedingten Zugriffs, der nach Beseitigung der Bedrohung den Zugriff gewährt](./media/lookout-mobile-threat-defense-connector/network-wifi-unblocked.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Steuern des Zugriffs auf SharePoint Online basierend auf Netzwerkbedrohungen

Erkennen Sie Bedrohungen für Ihr Netzwerk wie Man-in-the-Middle-Angriffe, und verhindern Sie die Synchronisierung von Unternehmensdateien basierend auf den Risiken für Geräte.

*Blockieren des Zugriffs auf SharePoint Online bei Erkennen von Bedrohungen für das Netzwerk*

> [!div class="mx-imgBorder"]
> ![Darstellung des blockierten Zugriffs auf SharePoint Online](./media/lookout-mobile-threat-defense-connector/network-spo-blocked.png)

*Zugriff nach Beseitigung gewährt:*

> [!div class="mx-imgBorder"]
> ![Darstellung des gewährten Zugriffs, nachdem die Netzwerkbedrohung beseitigt wurde](./media/lookout-mobile-threat-defense-connector/network-spo-unblocked.png)

### <a name="control-access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>Steuern des Zugriffs auf nicht registrierte Geräte bei Bedrohungen durch Apps mit Schadsoftware

Wenn die MTD-Lösung von Lookout for Work ein Gerät für infiziert hält:
> [!div class="mx-imgBorder"]
> ![App-Schutzrichtlinie blockiert Zugriff aufgrund erkannter Schadsoftware](./media/lookout-mobile-threat-defense-connector/lookout-app-policy-block.png)

Nach der Behebung wird der Zugriff wieder erteilt:

> [!div class="mx-imgBorder"]
> ![Zugriff wird nach Behebung durch die App-Schutzrichtlinie wieder gewährt](./media/lookout-mobile-threat-defense-connector/lookout-app-policy-remediated.png)

## <a name="next-steps"></a>Nächste Schritte

Hier sind die wichtigsten Schritte, die Sie ausführen müssen, um diese Lösung zu implementieren:

- [Einrichten Ihrer Lookout-Integration](lookout-mtd-connector-integration.md)
- [Aktivieren von Mobile Endpoint Security in Intune](mtd-connector-enable.md)
- [Die Lookout for Work-App hinzufügen und zuweisen](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Die Lookout-Gerätekonformitätsrichtlinie konfigurieren](mtd-device-compliance-policy-create.md)
- [Erstellen einer MTD-App-Schutzrichtlinie](mtd-app-protection-policy.md)
