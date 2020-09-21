---
title: Datenspeicherung und -verarbeitung in Intune
titleSuffix: Microsoft Intune
description: Erfahren Sie mehr darüber, wie personenbezogene Daten in Intune gespeichert und verarbeitet werden.
keywords: Daten, Datenschutz
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: edb07842-6a16-482e-8c1d-541a29e169a8
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 92c7c597a6d196ab5f8c3170cd5880682a280e73
ms.sourcegitcommit: e2deac196e5e79a183aaf8327b606055efcecc82
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/14/2020
ms.locfileid: "90076062"
---
# <a name="data-storage-and-processing-in-intune"></a>Datenspeicherung und -verarbeitung in Intune

### <a name="storing-customer-data"></a>Speichern von Kundendaten

Nach dem [Sammeln von Daten](privacy-data-collect.md) befolgt Intune die Microsoft 365-Standardrichtlinie für die Datenverarbeitung, die regelt, wie Kundendaten gespeichert und verarbeitet werden. Informationen dazu finden Sie unter [Informationen dazu, wo Ihre Microsoft 365-Kundendaten gespeichert werden](https://docs.microsoft.com/microsoft-365/enterprise/o365-data-locations). Personenbezogene Daten werden innerhalb der überwachten Konformitätsgrenzen des Intune-Diensts im Rahmen der technischen Sicherheitsmaßnahmen verarbeitet, die in den [Microsoft-Bestimmungen für Onlinedienste (OST)](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46) zugesichert werden.

### <a name="storage-locations"></a>Speicherorte

Microsoft betreibt Intune-Dienste in vielen Regionen weltweit. Intune berücksichtigt die Auswahl des Speicherorts, die vom Administrator für Kundendaten festgelegt wurde.

Weitere Informationen finden Sie unter [Standorte von Rechenzentren](https://docs.microsoft.com/microsoft-365/enterprise/o365-data-locations?view=o365-worldwide#data-center-locations).

### <a name="personal-data-retention"></a>Aufbewahrung personenbezogener Daten

Die Microsoft 365-Standardrichtlinie für die Datenverarbeitung regelt, wie lange Kundendaten nach dem Löschen aufbewahrt werden. Kundendaten werden in den beiden folgenden Szenarien gelöscht:

-**Aktives Löschen**: Der Mandant besitzt ein aktives Abonnement, und ein Benutzer oder Administrator löscht Daten, oder ein Administrator löscht einen Benutzer.
-**Passives Löschen**: Das Mandantenabonnement endet.

Informationen zu beiden Szenarien finden Sie unter [Aufbewahren, Löschen und Zerstören von Daten in Microsoft 365](https://docs.microsoft.com/microsoft-365/enterprise/microsoft-365-data-retention-deletion-and-destruction-overview?view=o365-worldwide).  

Im Allgemeinen werden von Intune gesammelte Daten innerhalb von 30 Tagen nach dem Löschen entfernt. Überwachungsprotokolle werden aus Sicherheitsgründen bis zu ein Jahr lang aufbewahrt. 


## <a name="processing-personal-data"></a>Verarbeiten von personenbezogenen Daten

Intune verarbeitet personenbezogene Daten mit ISO-zertifizierten Systemen. Weitere Informationen finden Sie im [Service Trust Portal](https://www.microsoft.com/en-us/TrustCenter/stp).

### <a name="profiling-and-marketing"></a>Profilerstellung und Marketing

Microsoft Intune verwendet keine personenbezogenen Daten, die durch den Dienst gesammelt wurden, für Profilerstellungs- oder Marketingzwecke. 

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie mehr darüber, wie Intune personenbezogene Daten [sichert und freigibt](privacy-data-secure-share.md). 
