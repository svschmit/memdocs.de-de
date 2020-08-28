---
title: Windows Autopilot-Lizenzierungsanforderungen
ms.reviewer: ''
manager: laurawi
description: Informieren Sie sich über Lizenzierungsanforderungen für die Windows Autopilot-Bereitstellung.
keywords: MDM, Setup, Windows, Windows 10, OOBE, Manage, Bereitstellung, Autopilot, ZTD, Zero-Touchscreen, Partner, msfb, InTune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.custom:
- CI 116757
- CSSTroubleshooting
ms.openlocfilehash: 22f9b5f8e93339bc41403b2acf6e4ce53395a139
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993777"
---
# <a name="windows-autopilot-licensing-requirements"></a>Windows Autopilot-Lizenzierungsanforderungen

**Gilt für: Windows 10**

Windows Autopilot ist von bestimmten Funktionen abhängig, die in Windows 10 und Azure Active Directory verfügbar sind. Außerdem ist ein MDM-Dienst erforderlich, z. b. Microsoft InTune. Diese Funktionen können über verschiedene Editionen und Abonnement Programme abgerufen werden:

Eines der folgenden Abonnements ist erforderlich, um die erforderlichen Azure Active Directory (automatische MDM-Registrierung und Unternehmens brandingfeatures) und MDM-Funktionalität bereitzustellen:
- [Premium-Abonnement Microsoft 365 Business](https://www.microsoft.com/microsoft-365/business)
- [Microsoft 365 F1-oder F3-Abonnement](https://www.microsoft.com/microsoft-365/enterprise/firstline)
- [Microsoft 365 Academic a1-, a3-oder A5-Abonnement](https://www.microsoft.com/education/buy-license/microsoft365/default.aspx)
- [Microsoft 365 Enterprise E3-oder E5-Abonnement](https://www.microsoft.com/microsoft-365/enterprise), die alle Features von Windows 10, Microsoft 365 und EM + S (Azure AD und InTune) enthalten.
- [Enterprise Mobility + Security E3-oder E5-Abonnement](https://www.microsoft.com/cloud-platform/enterprise-mobility-security), das alle benötigten Azure AD-und InTune-Features umfasst.
- [InTune for Education-Abonnement](/intune-education/what-is-intune-for-education), das alle benötigten Azure AD-und InTune-Features umfasst.
- [Azure Active Directory Premium P1 oder P2](https://azure.microsoft.com/services/active-directory/) und [Microsoft InTune Abonnement](https://www.microsoft.com/cloud-platform/microsoft-intune) (oder ein alternativer MDM-Dienst).

> [!NOTE]
> Selbst bei Verwendung Microsoft 365 Abonnements müssen Sie [den Benutzern trotzdem InTune-Lizenzen zuweisen](/intune/fundamentals/licenses-assign).

Außerdem wird Folgendes empfohlen (ist jedoch nicht erforderlich):
- [Microsoft 365 Apps für Unternehmen](https://www.microsoft.com/p/office-365-proplus/CFQ7TTC0K8R0), die problemlos über InTune (oder andere MDM-Dienste) bereitgestellt werden können.
- [Windows-Abonnement Aktivierung](/windows/deployment/windows-10-enterprise-subscription-activation), um Geräte von Windows 10 pro zu Windows 10 Enterprise automatisch zu überspringen.

**Nächste Schritte**

[Windows Autopilot-Konfigurations Anforderungen](configuration-requirements.md)