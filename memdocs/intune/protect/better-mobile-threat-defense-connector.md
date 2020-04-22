---
title: Better Mobile Threat Defense-Connector mit Intune
titleSuffix: Intune on Azure
description: Richten Sie Better Mobile Threat Defense-Connector mit Intune ein.
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
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 05dec05cdc5a16078328d736d2f622cea1b2aa00
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "79353982"
---
# <a name="better-mobile-threat-defense-connector-with-intune"></a>Better Mobile Threat Defense-Connector mit Intune

Sie können den Zugriff mobiler Geräte auf Unternehmensressourcen mithilfe des bedingten Zugriffs basierend auf Risikobewertungen steuern, die von Better Mobile vorgenommen werden, einer Mobile Threat Defense-Lösung (MTD), die in Microsoft Intune integriert werden kann. Das Risiko wird basierend auf Telemetriedaten von Geräten bewertet, auf denen die Better Mobile-App ausgeführt wird.

Sie können Richtlinien für bedingten Zugriff basierend auf der Better Mobile-Risikobewertung konfigurieren, die über Intune-Gerätekompatibilitätsrichtlinien für registrierte Geräte aktiviert wird, und so anhand der erkannten Bedrohungen den Zugriff auf Unternehmensressourcen durch nicht konforme Geräte zulassen oder blockieren. Für nicht registrierte Geräte können Sie App-Schutzrichtlinien verwenden, um das Blockieren oder ein selektives Löschen basierend auf erkannten Bedrohungen zu erzwingen.

## <a name="how-do-intune-and-better-mobile-help-protect-your-company-resources"></a>Wie helfen Intune und Better Mobile beim Schutz von Unternehmensressourcen?

Die Better Mobile-App wird auf Mobilgeräten installiert und ausgeführt. Diese App erfasst Telemetriedaten des Dateisystems, Netzwerkstapels, von Geräten und Anwendungen, sofern verfügbar, und sendet diese Daten dann an den Better Mobile-Clouddienst, mit dessen Hilfe die Anfälligkeit des Geräts für mobile Bedrohungen bewertet wird.

- **Unterstützung für registrierte Geräte**: Die Intune-Gerätekonformitätsrichtlinie enthält eine Regel für Mobile Threat Defense (MTD), die Risikobewertungsinformationen aus Better Mobile verwenden kann. Wenn die MTD-Regel aktiviert ist, bewertet Intune die Gerätekompatibilität mit der von Ihnen aktivierten Richtlinie. Wird das Gerät als nicht kompatibel eingestuft, wird der Zugriff auf Ressourcen wie Exchange Online und SharePoint Online für Benutzer blockiert. Benutzer erhalten zudem einen Leitfaden von der auf ihren Geräten installierten Better Mobile-App, um das Problem zu beheben und den Zugriff auf Unternehmensressourcen zurückzuerlangen. So unterstützen Sie die Verwendung von Better Mobile mit registrierten Geräten:
  - [Hinzufügen von MTD-Apps zu Geräten](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [Erstellen einer Gerätekonformitätsrichtlinie mit MTD-Unterstützung](../protect/mtd-device-compliance-policy-create.md)
  - [Aktivieren des MTP-Connectors in Intune](../protect/mtd-connector-enable.md)

- **Unterstützung für nicht registrierte Geräte**: Intune kann die Risikobewertungsdaten der Better Mobile-App auf nicht registrierten Geräten verwenden, wenn Sie Intune-App-Schutzrichtlinien verwenden. Administratoren können diese Kombination verwenden, um Unternehmensdaten in einer [durch Microsoft Intune geschützten App](../apps/apps-supported-intune-apps.md) zu schützen. Sie können zudem initiieren, dass Unternehmensdaten auf nicht registrierten Geräten blockiert oder teilweise gelöscht werden. So unterstützen Sie die Verwendung von Better Mobile mit nicht registrierten Geräten:
  - [Hinzufügen der MTD-App zu nicht registrierten Geräten](../protect/mtd-add-apps-unenrolled-devices.md)
  - [Erstellen einer Mobile Threat Defense-App-Schutzrichtlinie (MTD)](../protect/mtd-app-protection-policy.md)
  - [Aktivieren des MTD-Connectors in Intune für nicht registrierte Geräte](../protect/mtd-enable-unenrolled-devices.md)

## <a name="supported-platforms"></a>Unterstützte Plattformen

- **Android 4.1 und höher**

- **iOS 8.0 und höher**

## <a name="prerequisites"></a>Voraussetzungen

- Azure Active Directory Premium

- Microsoft Intune-Abonnement

- Better Mobile Threat Defense-Abonnement

  - Weitere Informationen finden Sie auf der [Better Mobile-Website](https://www.better.mobi/).

## <a name="sample-scenarios"></a>Beispielszenarios

Es folgen einige gängige Szenarios.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Steuern des Zugriffs basierend auf Bedrohungen durch Apps, die Schadsoftware enthalten

Wenn Apps, die Schadsoftware enthalten, auf Geräten erkannt werden, können Sie Geräte an folgenden Aktionen hindern, bis die Bedrohung beseitigt ist:

- Herstellen einer Verbindung mit Unternehmens-E-Mail

- Synchronisieren von Unternehmensdateien mithilfe der OneDrive for Work-App

- Zugreifen auf Unternehmens-Apps

Blockieren, wenn Apps mit Schadsoftware erkannt werden:

![Darstellung: Apps mit Schadsoftware wurden erkannt](./media/better-mobile-threat-defense-connector/better-mobile-maliciousapps-blocked.png)

Nach der Behebung wird der Zugriff wieder erteilt:

![Apps mit Schadsoftware entdeckt, Zugriff gewährt](./media/better-mobile-threat-defense-connector/better-mobile-maliciousapps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>Steuern des Zugriffs basierend auf Bedrohung für das Netzwerk

Erkennen von Bedrohungen wie **Man-in-the-Middle-Angriffe** für Ihr Netzwerk und Schützen des Zugriffs auf WLAN-Netzwerke basierend auf dem Geräterisiko.

Blockieren des Netzwerkzugriffs über WLAN:

![Blockieren des Netzwerkzugriffs über WLAN](./media/better-mobile-threat-defense-connector/better-mobile-network-wifi-blocked.png)

Nach der Behebung wird der Zugriff wieder erteilt:

![Darstellung: Zugriff nach der Behebung erteilt](./media/better-mobile-threat-defense-connector/better-mobile-network-wifi-unblocked.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Steuern des Zugriffs auf SharePoint Online basierend auf Netzwerkbedrohungen

Erkennen von Bedrohungen wie **Man-in-the-Middle-Angriffe** für Ihr Netzwerk und Verhindern der Synchronisierung von Unternehmensdateien basierend auf dem Geräterisiko.

Blockieren von SharePoint Online bei Erkennung von Bedrohungen für das Netzwerk:

![Blockieren von SharePoint Online bei Erkennung von Bedrohungen für das Netzwerk](./media/better-mobile-threat-defense-connector/better-mobile-network-spo-blocked.png)

Zugriff erteilt nach der Sanierung:

![Zugriff erteilt nach der Behebung für Sharepoint-Beispiel](./media/better-mobile-threat-defense-connector/better-mobile-network-spo-unblocked.png)

### <a name="control--access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>Steuern des Zugriffs auf nicht registrierte Geräte bei Bedrohungen durch Apps mit Schadsoftware

Wenn die MTD-Lösung von Better Mobile ein Gerät für infiziert hält: ![App-Schutzrichtlinie blockiert Zugriff aufgrund erkannter Schadsoftware](./media/better-mobile-threat-defense-connector/better-mobile-app-policy-block.png)

Nach der Behebung wird der Zugriff wieder erteilt:

![Zugriff wird nach Behebung durch die App-Schutzrichtlinie wieder gewährt](./media/better-mobile-threat-defense-connector/better-mobile-app-policy-remediated.png)

## <a name="next-steps"></a>Nächste Schritte

- [Integrieren von Better Mobile in Intune](better-mobile-mtd-connector-integration.md)

- [Einrichten von Better Mobile-Apps](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Erstellen einer Better Mobile -Gerätekompatibilitätsrichtlinie](mtd-device-compliance-policy-create.md)

- [Aktivieren des Better Mobile MTD-Connectors](mtd-connector-enable.md)

- [Erstellen einer MTD-App-Schutzrichtlinie](mtd-app-protection-policy.md) 
