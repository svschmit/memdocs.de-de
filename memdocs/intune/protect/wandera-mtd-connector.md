---
title: Einrichten von Wandera Mobile Security in Intune
titleSuffix: Intune on Azure
description: Einrichten der Wandera Mobile Security-Lösung in Microsoft Intune, um den Zugriff mobiler Geräte auf Ihre Unternehmensressourcen zu steuern.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/2/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 92c0911ff9250fb1b2832df4b7e269f192ee8cda
ms.sourcegitcommit: 41e6e6b7f5c2a87aaf7f23d90d0f175dd63c0579
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2020
ms.locfileid: "89057520"
---
# <a name="wandera-mobile-threat-defense-connector-with-intune"></a>Wandera Mobile Threat Defense-Connector mit Intune  

Steuern Sie den Zugriff mobiler Geräte auf Unternehmensressourcen mithilfe des bedingten Zugriffs basierend auf der Risikobewertung von Wandera. Wandera ist eine Mobile Threat Defense-Lösung (MTD), die in Microsoft Intune integriert ist.  Das Risiko wird basierend auf Telemetriedaten bewertet, die vom Wandera-Dienst auf Geräten erfasst werden, wie z.B.:
- Sicherheitsrisiken des Betriebssystems
- Installierte Apps, die Schadsoftware enthalten
- Netzwerkprofile mit böswilligen Absichten
- Cryptojacking

Sie können Richtlinien für *bedingten Zugriff* basierend auf Risikobewertungen von Wandera konfigurieren, die über Intune-Gerätekonformitätsrichtlinien aktiviert werden. Richtlinien für die Risikobewertung können den Zugriff nicht konformer Geräte auf Unternehmensressourcen basierend auf den erkannten Bedrohungen gewähren oder verweigern.  

## <a name="how-do-intune-and-wandera-mobile-threat-defense-help-protect-your-company-resources"></a>In welcher Form unterstützen Intune und Wandera Mobile Threat Defense den Schutz Ihrer Unternehmensressourcen?  

Die mobile App von Wandera lässt sich mithilfe von Microsoft Intune nahtlos installieren. Diese App erfasst Daten zum Dateisystem, Netzwerkstapel sowie Geräte- und Anwendungstelemetriedaten (sofern verfügbar). Diese Informationen werden mit dem Wandera-Clouddienst synchronisiert, um das Risiko des Geräts für mobile Bedrohungen zu bewerten. Diese Klassifizierungen der Risikostufen sind in der Wandera-Konsole RADAR nach Ihren Bedürfnissen konfigurierbar.

Die Konformitätsrichtlinie in Intune enthält eine Regel für MTD, die auf der Risikobewertung von Wandera basiert. Wenn diese Regel aktiviert ist, bewertet Intune die Gerätekompatibilität mit der von Ihnen aktivierten Richtlinie.

Für nicht konforme Geräte kann der Zugriff auf Ressourcen wie Microsoft 365 blockiert werden. Benutzer auf blockierten Geräten erhalten Anleitungen von der Wandera-App, wie sie das Problem beheben und den Zugriff zurückzuerlangen können.

Wandera aktualisiert Intune mit der neuesten Bedrohungsstufe der einzelnen Geräte (Sicher, Niedrig, Mittel oder Hoch), wenn sich diese ändert. Diese Bedrohungsstufe wird kontinuierlich von der Wandera-Sicherheitscloud neu berechnet und basiert auf dem Gerätestatus, der Netzwerkaktivität und zahlreichen Mobile Threat Intelligence-Feeds für verschiedene Bedrohungskategorien.

Diese Kategorien und die zugehörigen Bedrohungsstufen können in der RADAR-Konsole von Wandera konfiguriert werden, sodass die Gesamtanzahl der berechneten Bedrohungsstufen für jedes Gerät gemäß der Sicherheitsanforderungen Ihrer Organisation angepasst werden kann. Es gibt zwei Arten von Intune-Richtlinien, die die Bedrohungsstufe nutzen können, um den Zugriff auf Unternehmensdaten zu verwalten:

* Mithilfe von **Gerätekonformitätsrichtlinien** mit bedingtem Zugriff können Administratoren Richtlinien festlegen, um ein verwaltetes Gerät anhand der von Wandera gemeldeten Bedrohungsstufe automatisch als „nicht konform“ zu kennzeichnen. Dieses Konformitätsflag ermöglicht Richtlinien für bedingten Zugriff daher das Zulassen oder Blockieren des Zugriffs auf Anwendungen, die die moderne Authentifizierung nutzen.  Informationen zur Konfiguration finden Sie unter [Erstellen einer Mobile Threat Defense-App-Schutzrichtlinie (MTD) mit Intune](../protect/mtd-device-compliance-policy-create.md).

* Mithilfe von **App-Schutzrichtlinien** mit bedingtem Start können Administratoren Richtlinien festlegen, die anhand der von Wandera gemeldeten Bedrohungsstufe auf der nativen Anwendungsebene erzwungen werden (z. B. Android- und iOS-/iPadOS-Apps wie Outlook, OneDrive usw.).  Diese Richtlinien können auch mit nicht verwalteten Geräten (MAM-WE) verwendet werden, um einheitliche Richtlinien für alle Geräteplattformen und Eigentumsmodi bereitzustellen. Informationen zur Konfiguration finden Sie unter [Erstellen einer Mobile Threat Defense-App-Schutzrichtlinie (MTD) mit Intune](../protect/mtd-app-protection-policy.md).

## <a name="supported-platforms"></a>Unterstützte Plattformen  

Bei Registrierung in Intune werden die folgenden Plattformen für Wandera unterstützt:

- Android 5.0 und höher  
- iOS 10.2 und höher 

Weitere Informationen zu Plattform und Gerät finden Sie auf der [Website von Wandera](https://www.wandera.com/mobile-threat-defense/).

## <a name="prerequisites"></a>Voraussetzungen  

- Microsoft Intune-Abonnement  
- Azure Active Directory  
- Wandera Mobile Threat Defense (früher Wandera Secure)  

Weitere Informationen finden Sie unter [Wandera Mobile Security](https://www.wandera.com/mobile-security/).
 
## <a name="sample-scenarios"></a>Beispielszenarios

Im Folgenden finden Sie allgemeine Szenarien für die Verwendung von Wandera MTD mit Intune.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Steuern des Zugriffs basierend auf Bedrohungen durch Apps, die Schadsoftware enthalten  

Wenn Apps mit Schadsoftware auf Geräten erkannt werden, können Sie Geräte an gängigen Aktionen hindern, bis die Bedrohung beseitigt ist. Dazu gehören u.a.:  
- Herstellen einer Verbindung mit Unternehmens-E-Mail  
- Synchronisieren von Unternehmensdateien mithilfe der OneDrive for Work-App  
- Zugreifen auf Unternehmens-Apps  

*Blockieren, wenn Apps mit Schadsoftware erkannt werden*:

![Darstellung des Szenarios, wenn Apps mit Schadsoftware erkannt werden](./media/wandera-mtd-connector/wandera-malicious-apps-blocked.png)  

*Zugriff erteilt nach der Behebung*: 

![Darstellung des Szenarios, wenn der Zugriff nach der Behebung wieder erteilt wird](./media/wandera-mtd-connector/wandera-malicious-apps-unblocked.png)


### <a name="control-access-based-on-threat-to-network"></a>Steuern des Zugriffs basierend auf Bedrohung für das Netzwerk  

Erkennen Sie Bedrohungen Ihres Netzwerks, wie etwa Man-in-the-Middle-Angriffe, und schützen Sie den Zugriff auf WLANs auf der Grundlage des Geräterisikos.  

*Blockieren des Netzwerkzugriffs über WLAN*:  

![Blockieren des Netzwerkzugriffs über WLAN](./media/wandera-mtd-connector/wandera-network-wifi-blocked.png)

*Zugriff erteilt nach der Behebung*:  

![Zugriff nach Beseitigung gewährt](./media/wandera-mtd-connector/wandera-network-wifi-unblocked.png)  

## <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Steuern des Zugriffs auf SharePoint Online basierend auf Netzwerkbedrohungen

Erkennen Sie Bedrohungen für Ihr Netzwerk wie Man-in-the-Middle-Angriffe, und verhindern Sie die Synchronisierung von Unternehmensdateien basierend auf den Risiken für Geräte.

*Blockieren von SharePoint Online bei Erkennung von Bedrohungen für das Netzwerk*:  

![Blockieren von SharePoint Online bei Erkennung von Bedrohungen für das Netzwerk](./media/wandera-mtd-connector/wandera-network-spo-blocked.png)  

*Zugriff erteilt nach der Behebung*:  

![Zugriff erteilt nach der Behebung für SharePoint – Beispiel](./media/wandera-mtd-connector/wandera-network-spo-unblocked.png)  

### <a name="control-access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>Steuern des Zugriffs auf nicht registrierte Geräte bei Bedrohungen durch Apps mit Schadsoftware

Wenn die Mobile Threat Defense-Lösung von Wandera ein Gerät für infiziert hält:

![App-Schutzrichtlinie blockiert aufgrund erkannter Schadsoftware](./media/wandera-mtd-connector/wandera-mobile-app-policy-block.png)

Nach der Behebung wird der Zugriff wieder erteilt:

![Zugriff wird nach Behebung durch die App-Schutzrichtlinie wieder gewährt](./media/wandera-mtd-connector/wandera-mobile-app-policy-remediated.png)

## <a name="next-steps"></a>Nächste Schritte

- [Integrieren von Wandera in Intune](wandera-mtd-connector-integration.md)
- [Einrichten von Wandera-Apps](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Erstellen einer Wandera-Konformitätsrichtlinie für Geräte](mtd-device-compliance-policy-create.md)
- [Aktivieren des Wandera MTD-Connectors](mtd-connector-enable.md)
