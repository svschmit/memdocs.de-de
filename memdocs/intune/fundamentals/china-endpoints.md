---
title: Netzwerkendpunkte für Bereitstellungen in China – Microsoft Intune
titleSuffix: ''
description: Überprüfen Sie die Endpunkte für Intune in China.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/28/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3c451f01af454ec6ed495c080c74d52f9f0ae591
ms.sourcegitcommit: 118587ddb31ce26b27801839db9b3b59f1177f0f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/29/2020
ms.locfileid: "84166594"
---
# <a name="china-endpoints-for-microsoft-intune"></a>Endpunkte für Microsoft Intune in China

Auf dieser Seite werden die Endpunkte in China aufgelistet, die für die Proxyeinstellungen in Ihren Intune-Bereitstellungen erforderlich sind.

Sie müssen die Kommunikation für Intune aktivieren, um Geräte hinter Firewalls und Proxyservern zu verwalten.

- Der Proxyserver muss sowohl **HTTP** (80) als auch **HTTPS** (443) unterstützen, da Intune-Clients beide Protokolle verwenden.
- Für einige Aufgaben wie das Herunterladen von Software und Updates erfordert Intune nicht authentifizierten Zugriff über Proxyserver auf manage.microsoft.com.

Sie können die Proxyservereinstellungen auf einzelnen Clientcomputern festlegen. Sie können zudem Gruppenrichtlinieneinstellungen verwenden, um die Einstellungen für alle Clientcomputer hinter einem bestimmten Proxyserver anzupassen.

Für verwaltete Geräte sind Konfigurationen erforderlich, über die **Alle Benutzer** über Firewalls auf Dienste zugreifen können.

Weitere Informationen zur automatischen Windows 10-Registrierung und zur Geräteregistrierung für Kunden in China finden Sie unter [Einrichten der Registrierung für Windows-Geräte](../enrollment/windows-enroll.md#windows-10-auto-enrollment-and-device-registration).

In den folgenden Tabellen sind die Ports und Dienste aufgeführt, auf die der Intune-Client zugreift:

|**Endpunkt**|**IP-Adresse**|
|---------------------|-----------|
|*.manage.microsoft.cn | 40.73.38.143<br>139.217.97.81<br>52.130.80.24<br>40.73.41.162<br>40.73.58.153<br>139.217.95.85 |


## <a name="intune-customer-designated-endpoints-in-china"></a>Von Intune-Kunden in China festgelegte Endpunkte
- Azure-Portal: https:\//portal.azure.cn/
- Office 365: https:\//portal.partner.microsoftonline.cn/
- Intune-Unternehmensportal: https:\//portal.manage.microsoftonline.cn/
- Microsoft Endpoint Manager Admin Center: https:\//endpoint.microsoftonline.cn/


## <a name="partner-service-endpoints"></a>Partner-Dienstendpunkte

Intune wird von 21ViaNet betrieben und ist von den folgenden Partner-Dienstendpunkten abhängig:
- Azure AD-Synchronisierungsdienst: https:\//syncservice.Partner.microsoftonline.cn/DirectoryService.svc
- Evo STS: https:\//login.chinacloudapi.cn/
- Azure AD Graph: https:\//graph.chinacloudapi.us
- MS Graph: https:\//microsoftgraph.chinacloudapi.cn
- ADRS: https:\//enterpriseregistration.microsoftonline.cn

## <a name="next-steps"></a>Nächste Schritte
[Weitere Informationen zu Intune, betrieben von 21ViaNet in China](china.md)

