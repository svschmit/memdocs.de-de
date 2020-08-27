---
title: Windows Autopilot-Konfigurations Anforderungen
ms.reviewer: ''
manager: laurawi
description: Informieren Sie sich über die Konfigurations Anforderungen für die Windows Autopilot-Bereitstellung.
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
ms.openlocfilehash: 8731532ff052c626514d9f1a80e3a93c0cbde6dc
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908318"
---
# <a name="windows-autopilot-configuration-requirements"></a>Windows Autopilot-Konfigurations Anforderungen

**Gilt für: Windows 10**

Bevor Windows Autopilot verwendet werden kann, sind einige Konfigurationsaufgaben erforderlich, um die gängigen Autopilot-Szenarien zu unterstützen. 

- Konfigurieren Azure Active Directory automatischen Registrierung. Weitere Informationen zu Microsoft InTune finden Sie unter Aktivieren der automatischen Registrierung von [Windows 10](/intune/windows-enroll#enable-windows-10-automatic-enrollment) . Wenn Sie einen anderen MDM-Dienst verwenden, wenden Sie sich an den Anbieter, um die für diese Dienste erforderlichen URLs oder Konfigurationen zu erhalten.
- Konfigurieren Sie Azure Active Directory benutzerdefiniertes Branding. Um eine organisationsspezifische Anmeldeseite anzuzeigen, müssen Sie Azure Active Directory mit den Bildern und Text konfigurieren, die Sie anzeigen möchten. Weitere Informationen finden Sie [unter Schnellstart: Hinzufügen eines Unternehmensbrandings zur Anmeldeseite in Azure AD](/azure/active-directory/fundamentals/customize-branding). Wichtige Elemente für Autopilot sind das "quadratische Logo", "Text der Anmeldeseite" und Azure Active Directory Mandanten Name. Der Mandanten Name wird separat in den Eigenschaften des Azure AD Mandanten konfiguriert.
- Optional: Aktivieren Sie die [Aktivierung des Windows-Abonnements](/windows/deployment/windows-10-enterprise-subscription-activation), um automatisch von Windows 10 pro zu Windows 10 Enterprise zu wechseln.

Bestimmte Szenarien haben dann zusätzliche Anforderungen. Im Allgemeinen gibt es zwei spezielle Aufgaben:

- Geräteregistrierung. Geräte müssen Windows Autopilot hinzugefügt werden, um die meisten Windows Autopilot-Szenarien zu unterstützen. Weitere Informationen finden Sie unter [Hinzufügen von Geräten zu Windows Autopilot](add-devices.md).
- Profil Konfiguration. Nach dem Hinzufügen von Geräten zu Windows Autopilot muss ein Profil mit Einstellungen auf jedes Gerät angewendet werden. Weitere Informationen finden Sie unter [Konfigurieren von Autopilot-Profilen](profiles.md) .  Microsoft InTune können diese Profil Zuweisung automatisieren. Weitere Informationen finden Sie unter [Erstellen einer Autopilot-Gerätegruppe](/intune/enrollment-Autopilot#create-an-Autopilot-device-group) und [Zuweisen eines Autopilot-Bereitstellungs Profils zu einer Gerätegruppe](/intune/enrollment-Autopilot#assign-an-Autopilot-deployment-profile-to-a-device-group).

Weitere Informationen finden Sie unter [Windows Autopilot-Szenarios](windows-Autopilot-scenarios.md).

Eine exemplarische Vorgehensweise für einige dieser und verwandte Schritte finden Sie in diesem Video:

</br>

<iframe width="560" height="315" src="https://www.youtube.com/embed/KYVptkpsOqs" frameborder="0" allow="accelerometer; autoplay; encrypted-media" gyroscope; picture-in-picture" allowfullscreen></iframe>


Es gibt keine zusätzlichen Hardwareanforderungen für die Verwendung von Windows 10 Autopilot, außer den [Anforderungen zum Ausführen von Windows 10](https://www.microsoft.com/windows/windows-10-specifications).

**Nächste Schritte**

[Übersicht über Windows Autopilot](windows-autopilot.md)