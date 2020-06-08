---
title: Verwalten von Einstellungen für den Schutz von Konten vor Angriffen mit Endpunktsicherheitsrichtlinien in Microsoft Intune | Microsoft-Dokumentation
description: Konfigurieren und Bereitstellen von Richtlinien für Geräte, die Sie mithilfe von Einstellungen für den Schutz von Konten vor Angriffen mit Endpunktsicherheitsrichtlinien in Microsoft Intune verwalten.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 6fb5702b7c809c7810004a53d084f19fa94dea9e
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431851"
---
# <a name="account-protection-policy-for-endpoint-security-in-intune"></a>Kontoschutzrichtlinie für Endpunktsicherheit in Intune

Verwenden Sie Intune-Endpunktsicherheitsrichtlinien für den Kontoschutz, um die Identität und die Konten Ihrer Benutzer zu schützen. Die Kontoschutzrichtlinie konzentriert sich auf Einstellungen für Windows Hello and Credential Guard, die Teil der Windows-Identitäts- und Zugriffsverwaltung sind.

- *Windows Hello for Business-* ersetzt Kennwörter auf PCs und mobilen Geräten durch starke zweistufige Authentifizierung.
- *Credential Guard* hilft beim Schutz von Anmeldeinformationen und Geheimnissen, die Sie mit Ihren Geräten verwenden.

Weitere Informationen finden Sie unter [Identitäts- und Zugriffsverwaltung](https://docs.microsoft.com/windows/security/identity-protection/) in der Dokumentation zur Windows-Identitäts- und Zugriffsverwaltung.

Die Endpunktsicherheitsrichtlinien für Kontenschutz finden Sie unter *Verwalten* im Knoten **Endpunktsicherheit** des [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).

Zeigen Sie [Einstellungen für Kontoschutzprofile](../protect/endpoint-security-asr-profile-settings.md) an.

## <a name="prerequisites-for-account-protection-profiles"></a>Voraussetzungen für Kontoschutzprofile

- Windows 10 oder höher

## <a name="account-protection-profiles"></a>Kontoschutzprofile

*Kontoschutzprofile befinden sich in der Vorschau*.

**Windows 10-Profile**:

- **Kontoschutz** *(Vorschau)* – Einstellungen für Kontoschutzrichtlinien unterstützen Sie beim Schutz von Benutzeranmeldeinformationen.

## <a name="next-steps"></a>Nächste Schritte

[Konfigurieren von Endpunktsicherheitsrichtlinien](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
