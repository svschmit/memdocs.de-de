---
title: Anzeigen und Korrigieren personenbezogener Daten
titleSuffix: Microsoft Intune
description: Erfahren Sie, wie Sie personenbezogene Daten anzeigen und korrigieren können.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/18/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 1ba77bc7-505e-4eca-a49e-dcdaa75d0043
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 865a6f33053d9e1fe011d6c2cddf94d0e3995148
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914962"
---
# <a name="view-and-correct-personal-data"></a>Anzeigen und Korrigieren personenbezogener Daten

Intune-Administratoren können einige personenbezogene Daten basierend auf ihren Zugriffsberechtigungen anzeigen, aber nur Endbenutzer können die personenbezogenen Daten ihrer Geräte ändern.

[!INCLUDE [GDPR-related guidance](../includes/gdpr-dsr-and-stp-note.md)]


## <a name="view-personal-data"></a>Anzeigen von personenbezogenen Daten

Administratoren können die personenbezogenen Daten von Benutzern in verschiedenen Blättern der Intune-Benutzeroberfläche anzeigen. In den folgenden Artikeln wird erläutert, auf welche Informationen Administratoren zugreifen können:
- [Anzeigen von Gerätedetails in Intune](../remote-actions/device-inventory.md) – hier erfahren Sie, wie Sie Informationen zu Endbenutzergeräten überprüfen können.
- [Überwachen von App-Informationen und -Zuweisungen](../apps/apps-monitor.md) – dieser Artikel erläutert, wie Sie Informationen zu den Apps abrufen können, die auf einem Endbenutzergerät installiert sind.
- Im Artikel [Welche Informationen erhält meine Organisation, wenn ich mein Gerät registriere?](../user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune.md) erhalten Endbenutzer eine Liste der Daten, die ihr Unternehmen sehen bzw. nicht sehen kann. Setzen Sie Ihre Benutzer darüber in Kenntnis, welche Daten Sie erfassen und warum Sie diese erfassen. Dieser Artikel kann den ersten Schritt für diese Transparenz darstellen.

### <a name="who-can-view-the-data"></a>Wer kann die Daten anzeigen?

Microsoft wendet strenge Kontrollen an, um den Zugriff auf Kundendaten zu regeln, gewährt die niedrigste Zugriffsstufe, die für die Erledigung wichtiger Aufgaben erforderlich ist, und widerruft den Zugriff, sobald er nicht mehr benötigt wird. 

Sie können den Zugriff auf personenbezogene Daten von Endbenutzern sichern und steuern, indem Sie die rollenbasierte Zugriffssteuerung (Role-Based Access Control, RBAC) verwenden. Weitere Informationen finden Sie unter [Rollenbasierte Zugriffssteuerung in Microsoft Intune](../fundamentals/role-based-access-control.md).

Weitere Informationen über den Umgang mit Daten durch Microsoft finden Sie in den Nutzungsbedingungen für Onlinedienste und in der [Microsoft Online Services-Datenschutzerklärung](https://go.microsoft.com/fwlink/p/?linkid=131004&clcid=0x409). 

## <a name="correct-end-user-personal-data"></a>Korrigieren personenbezogener Daten von Endbenutzern

Administratoren können gerätespezifische oder App-spezifische Informationen nicht aktualisieren. Wenn ein Endbenutzer personenbezogene Daten korrigieren möchte (z.B. den Gerätenamen), muss dies direkt auf dem Gerät stattfinden. Solche Änderungen werden bei der nächsten Verbindung mit Intune synchronisiert.


## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie, wie Sie personenbezogene Daten in Intune [überwachen, exportieren oder löschen](privacy-data-audit-export-delete.md) können.