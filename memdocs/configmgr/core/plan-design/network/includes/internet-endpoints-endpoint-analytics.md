---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: c576a4466ce8685cb440d8c804c9a675fbbecb8b
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126456"
---
### <a name="endpoints-required-for-configuration-manager-managed-devices"></a>Endpunkte für von Configuration Manager verwaltete Geräte erforderlich

Von Configuration Manager verwaltete Geräte senden Daten über den Connector für die Rolle „Configuration Manager“ an Intune und benötigen keinen direkten Zugriff auf die öffentliche Cloud von Microsoft.

| Endpunkt  | Funktion  |
|-----------|-----------|
| `https://graph.windows.net` | Dieser Endpunkt wird beim Anfügen Ihrer Hierarchie an die Endpunktanalyse für die Serverrolle „Configuration Manager“ zum automatischen Abrufen von Einstellungen verwendet. Weitere Informationen finden Sie unter [Konfigurieren des Proxys für einen Standortsystemserver](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Dieser Endpunkt wird zum Synchronisieren von Gerätesammlung und Geräten mit der Endpunktanalyse verwendet (nur für die Serverrolle „Configuration Manager“). Weitere Informationen finden Sie unter [Konfigurieren des Proxys für einen Standortsystemserver](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |

### <a name="endpoints-required-for-intune-managed-devices"></a>Endpunkte für von Intune verwaltete Geräte erforderlich

Damit Geräte für die Endpunktanalyse registriert werden können, müssen sie die erforderlichen Funktionsdaten an die öffentliche Cloud von Microsoft senden. Endpoint Analytics nutzt die Windows 10- und Windows Server-Komponente „Benutzererfahrung und Telemetrie im verbundenen Modus“ (DiagTrack), um die Daten der Geräte zu erfassen, die von Intune verwaltet werden. Stellen Sie sicher, dass der Dienst **Benutzererfahrung und Telemetrie im verbundenen Modus** auf dem Gerät ausgeführt wird.

| Endpunkt  | Funktion  |
|-----------|-----------|
| `https://*.events.data.microsoft.com` | Wird von mit Intune verwalteten Geräten verwendet, um [erforderliche, funktionale Daten](../../../../../analytics/data-collection.md#bkmk_datacollection) an den Endpunkt für die Intune-Datensammlung zu senden. |
