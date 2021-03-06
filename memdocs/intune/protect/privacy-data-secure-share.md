---
title: Datensicherheit und -freigabe in Intune
titleSuffix: Microsoft Intune
description: Erfahren Sie mehr darüber, wie personenbezogene Daten in Intune gesichert und freigegeben werden.
keywords: Datenschutz, Daten
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 68921fd6-5f50-456c-a3af-83d7bc4b134b
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 34e99a53165afdccd5ee9a2f3f190c78f673a507
ms.sourcegitcommit: 15450a1e92d9f67f74ae619ffe192c15948107c5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/08/2020
ms.locfileid: "89516255"
---
# <a name="data-security-and-sharing-in-intune"></a>Datensicherheit und -freigabe in Intune


## <a name="data-security"></a>Datensicherheit

Microsoft Intune ist eine wichtige Komponente des Clouddienstangebots Microsoft Enterprise Mobility and Security Suite. Alle Microsoft Cloud Services werden mit den Methoden [Microsoft Privacy](https://www.microsoft.com/en-us/trustcenter/privacy) und [Microsoft Security](https://www.microsoft.com/en-us/trustcenter/security/) entwickelt, um die [Strategie zur Datenkontrolle](https://www.microsoft.com/en-us/TrustCenter/Security/default.aspx) zu unterstützen.  

Für Microsoft Intune werden die gleichen technischen und organisatorischen Maßnahmen wie bei Microsoft Azure ergriffen, um den Dienst gegen Datenschutzverletzungen zu sichern.

Weitere Informationen finden Sie im [Service Trust Portal](https://www.microsoft.com/en-us/TrustCenter/stp).

### <a name="data-breach-reporting"></a>Melden von Datenschutzverletzungen

Wenn ein Sicherheitsincident identifiziert wird, der den Kunden gemeldet werden sollte, werden diese darüber benachrichtigt. Dieser Prozess umfasst die Zusammenarbeit mit dem Microsoft 365-Team, um Benachrichtigungen über Datenschutzverletzungen mithilfe von Intune an alle Microsoft 365-Kunden zu übermitteln.

## <a name="data-sharing"></a>Datenfreigabe

Wenn Mandantenadministratoren bestimmte Funktionen aktivieren (z.B. das Apple-Programm zur Geräteregistrierung), erhält Microsoft Intune die Zustimmung des Administrators zum Freigeben von Daten an entsprechende Drittanbieter. In solchen Fällen kann Intune personenbezogene Daten für folgende Drittanbieter freigeben:

- Drittanbieter, die im Auftrag von Microsoft handeln.
- Drittanbieter, die nicht im Auftrag von Microsoft handeln, wenn Mandantenadministratoren Intune explizit die Berechtigung hierfür erteilen.

Alle Drittanbieter, die im Auftrag von Microsoft handeln, werden auf der [Liste der Onlinedienst-Zulieferer](https://aka.ms/Online_Serv_Subcontractor_List) aufgeführt.

Das Freigeben von Daten für diese Drittanbieter soll den technischen Support und den Kundensupport, die Wartung von Diensten und andere Vorgänge unterstützen.

Der Vertrag eines Mandanten mit dem Drittanbieter regelt den Umgang mit den personenbezogenen Intune-Daten, die im Drittanbieterdienst vorhanden sind. Dieser erteilt Intune ebenfalls die Berechtigung, Daten an den Drittanbieterdienst zu übertragen.  

Weitere Informationen zu für Drittanbieter freigegebenen Daten finden Sie in folgenden Artikeln:
- [Von Intune an Apple gesendete Daten](data-intune-sends-to-apple.md)
- [Von Intune an Google gesendete Daten](data-intune-sends-to-google.md)
- [Von Apple an Intune gesendete Daten](data-apple-sends-to-intune.md)
- [Von Google an Intune gesendete Daten](data-google-sends-to-intune.md)
- [Data Jamf Pro sends to Intune (Von Jamf Pro an Intune gesendete Daten)](data-jamf-sends-to-intune.md)

### <a name="microsoft-endpoint-configuration-manager-data-sharing"></a>Microsoft Endpoint Configuration Manager-Datenfreigabe

Microsoft Intune gibt keine Daten für Configuration Manager frei. Configuration Manager ist ein lokales Produkt, das direkt vom Kunden bereitgestellt, verwaltet und betrieben wird. Die Diagnose- und Nutzungsdaten, die von Configuration Manager gesammelt werden, dienen ausschließlich zur Verbesserung der Installation, der Qualität und der Sicherheit von zukünftigen Releases.

Weitere Informationen erhalten Sie unter [Diagnose- und Nutzungsdaten für Configuration Manager](/configmgr/core/plan-design/diagnostics/diagnostics-and-usage-data). 


## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie mehr darüber, wie personenbezogene Daten in Intune [angezeigt und korrigiert](privacy-data-view-correct.md) werden.
