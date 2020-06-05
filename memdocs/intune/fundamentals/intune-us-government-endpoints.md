---
title: Netzwerkendpunkte für US Government-Bereitstellungen – Microsoft Intune
titleSuffix: ''
description: Überprüfen Sie die US Government-Endpunkte für Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/30/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5f6682cb-5fcd-4018-b7f7-71768ad3152e
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: d1574e07ca58debaef5bbc134a86d76aa21778a3
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347247"
---
# <a name="us-government-endpoints-for-microsoft-intune"></a>US Government-Endpunkte für Microsoft Intune

Auf dieser Seite werden die US Government-Endpunkte aufgelistet, die für die Proxyeinstellungen in Ihren Intune-Bereitstellungen erforderlich sind.

Sie müssen die Kommunikation für Intune aktivieren, um Geräte hinter Firewalls und Proxyservern zu verwalten.

- Der Proxyserver muss sowohl **HTTP** (80) als auch **HTTPS** (443) unterstützen, da Intune-Clients beide Protokolle verwenden.
- Für einige Aufgaben wie das Herunterladen von Software und Updates erfordert Intune nicht authentifizierten Zugriff über Proxyserver auf manage.microsoft.com.

Sie können die Proxyservereinstellungen auf einzelnen Clientcomputern festlegen. Sie können zudem Gruppenrichtlinieneinstellungen verwenden, um die Einstellungen für alle Clientcomputer hinter einem bestimmten Proxyserver anzupassen.

Für verwaltete Geräte sind Konfigurationen erforderlich, über die **Alle Benutzer** über Firewalls auf Dienste zugreifen können.

Weitere Informationen zur automatischen Windows 10-Registrierung und zur Geräteregistrierung für Kunden der US-Registrierung finden Sie unter [Einrichten der Registrierung für Windows-Geräte](../enrollment/windows-enroll.md#windows-10-auto-enrollment-and-device-registration).

In den folgenden Tabellen sind die Ports und Dienste aufgeführt, auf die der Intune-Client zugreift:

|**Endpunkt**|**IP-Adresse**|
|---------------------|-----------|
|*.manage.microsoft.us | 52.243.26.209 <br> 52.247.173.11 <br> 52.227.183.12 <br>52.227.180.205 <br> 52.227.178.107 <br> 13.72.185.168 <br> 52.227.173.179 <br> 52.227.175.242 <br> 13.72.39.209 <br> 52.243.26.209 <br> 52.247.173.11 |
| enterpriseregistration.microsoftonline.us | 13.72.188.239 <br> 13.72.55.179 |

## <a name="us-government-customer-designated-endpoints"></a>Vom Kunden festgelegte US Government-Endpunkte:
- Azure-Portal: https:\//portal.azure.us/ 
- Office 365: https:\//portal.office365.us/ 
- Intune-Unternehmensportal: https:\//portal.manage.microsoft.us/ 
- Microsoft Endpoint Manager Admin Center: https:\//endpoint.microsoft.us/

## <a name="partner-service-endpoints-that-intune-depends-on"></a>Partner-Dienstendpunkte, von denen Intune abhängig ist:
- AAD Sync-Dienst: https:\//syncservice.gov.us.microsoftonline.com/DirectoryService.svc
- Evo STS: https:\//login.microsoftonline.us
- Verzeichnisproxy: https:\//directoryproxy.microsoftazure.us/DirectoryProxy.svc
- AAD Graph: https:\//directory.microsoftazure.us and https:\//graph.microsoftazure.us
- MS Graph: https:\//graph.microsoft.us
- ADRS: https:\//enterpriseregistration.microsoftonline.us

[!INCLUDE [Intune notices](../includes/windows-push-notification-services.md)]

[!INCLUDE [Intune notices](../includes/apple-device-network-information.md)]

## <a name="next-steps"></a>Nächste Schritte
[Netzwerkendpunkte für Microsoft Intune](intune-endpoints.md)

