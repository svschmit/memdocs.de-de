---
title: 'Intune-Endpunktsicherheit: Einstellungen für Endpunkterkennung und -antwort | Microsoft-Dokumentation'
description: Endpunktsicherheits-Richtlinieneinstellungen für Endpunkterkennung und -antwort in Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
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
ms.openlocfilehash: e26719bb9bf322e3e4bf11b39911e98788707629
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2020
ms.locfileid: "86460415"
---
# <a name="endpoint-detection-and-response-policy-settings-for-endpoint-security-in-intune"></a>Richtlinieneinstellungen für Endpunkterkennung und -antwort für Endpunktsicherheit in Intune

Zeigen Sie die Einstellungen an, die Sie in Profilen für die [Richtlinie für Endpunkterkennung und -antwort](../protect/endpoint-security-edr-policy.md) im Endpunktsicherheitsknoten von Intune konfigurieren können.

Unterstützte Plattformen und Profile:

- **Windows 10 und höher**: Verwenden Sie diese Plattform für Richtlinien, die Sie für mit Intune verwaltete Geräte bereitstellen.
  - Profil: **Endpunkterkennung und -antwort (MDM)**

- **Windows 10 und Windows Server**: Verwenden Sie diese Plattform für Richtlinien, die Sie auf Geräten bereitstellen, die von Configuration Manager verwaltet werden.
  - Profil: **Endpunkterkennung und -antwort (ConfigMgr)**

## <a name="endpoint-detection-and-response-mdm"></a>Endpunkterkennung und -antwort (MDM)

**Endpunkterkennung und -antwort**:

- **Pakettyp für die Microsoft Defender ATP-Clientkonfiguration**

  Laden Sie ein signiertes Konfigurationspaket hoch, das zum Onboarding des Microsoft Defender ATP-Clients verwendet wird.

  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Blob für Onboarding**  
  - **Blob für Offboarding**  

  Bei Festlegung auf *Blob für Onboarding* können Sie die folgenden Einstellungen festlegen:

  - **Advanced Threat Protection: Blob für Onboarding**  
    Klicken Sie auf **Onboardingdatei auswählen**, um den Bereich *Onboardingdatei auswählen* zu öffnen, in dem Sie eine `.onboarding`-Datei angeben.

  Bei Festlegung auf *Blob für Offboarding* können Sie die folgenden Einstellungen festlegen:
  
  - **Advanced Threat Protection: Blob für Offboarding**  
     Klicken Sie auf **Offboardingdatei auswählen**, um den Bereich *Offboardingdatei auswählen* zu öffnen, in dem Sie eine `.offboarding`-Datei angeben.

- **Beispielfreigabe für alle Dateien**  

  Hiermit wird der Konfigurationsparameter für die Microsoft Defender Advanced Threat Protection-Beispielfreigabe zurückgegeben oder festgelegt.  
  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Ja**

- **Häufigkeit von Telemetrieberichten erhöhen**

  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Ja**: Erhöht die Häufigkeit von Microsoft Defender Advanced Threat Protection-Telemetrieberichten.

## <a name="endpoint-detection-and-response-configmgr"></a>Endpunkterkennung und -antwort (ConfigMgr)

**Endpunkterkennung und -antwort**:

- **Beispielfreigabe für alle Dateien**  

  Hiermit wird der Konfigurationsparameter für die Microsoft Defender Advanced Threat Protection-Beispielfreigabe zurückgegeben oder festgelegt.  
  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Ja**

- **Häufigkeit von Telemetrieberichten erhöhen**

  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Ja**: Erhöht die Häufigkeit von Microsoft Defender Advanced Threat Protection-Telemetrieberichten.

## <a name="next-steps"></a>Nächste Schritte

[Endpunktsicherheitsrichtlinie für EDR](../protect/endpoint-security-edr-policy.md)
