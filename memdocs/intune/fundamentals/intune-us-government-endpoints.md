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
ms.openlocfilehash: 032e6468ce326637e264b232cdd4e4d954ea70d8
ms.sourcegitcommit: dc2cca9eb70aef15037e8f7d18d671c513bfde85
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/14/2020
ms.locfileid: "90081806"
---
# <a name="us-government-endpoints-for-microsoft-intune"></a>US Government-Endpunkte für Microsoft Intune

Auf dieser Seite sind die Endpunkte für die US-Regierung, die Community der US-Regierung (US Government Community (GCC) High) und das US-amerikanische Verteidigungsministerium (Department of Defense, DoD) aufgeführt, die für die Proxyeinstellungen in Ihren Intune-Bereitstellungen benötigt werden.

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
- Microsoft 365: https:\//portal.office365.us/ 
- Intune-Unternehmensportal: https:\//portal.manage.microsoft.us/ 
- Microsoft Endpoint Manager Admin Center: https:\//endpoint.microsoft.us/

## <a name="partner-service-endpoints-that-intune-depends-on"></a>Partner-Dienstendpunkte, von denen Intune abhängig ist:
- Azure AD Sync-Dienst: https:\//syncservice.gov.us.microsoftonline.com/DirectoryService.svc
- Evo STS: https:\//login.microsoftonline.us
- Verzeichnisproxy: https:\//directoryproxy.microsoftazure.us/DirectoryProxy.svc
- Azure AD Graph: https:\//directory.microsoftazure.us and https:\//graph.microsoftazure.us
- MS Graph: https:\//graph.microsoft.us
- ADRS: https:\//enterpriseregistration.microsoftonline.us

[!INCLUDE [Intune notices](../includes/windows-push-notification-services.md)]

[!INCLUDE [Intune notices](../includes/apple-device-network-information.md)]

## <a name="next-steps"></a>Nächste Schritte
[Netzwerkendpunkte für Microsoft Intune](intune-endpoints.md)

