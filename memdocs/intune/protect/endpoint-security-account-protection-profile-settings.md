---
title: 'Intune-Endpunktsicherheit: Kontoschutz-Richtlinieneinstellungen | Microsoft-Dokumentation'
description: 'Endpunktsicherheit: Kontoschutz-Richtlinieneinstellungen in Microsoft Intune'
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
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
ms.openlocfilehash: f4e67c434af9eb7f88c3e7d3997ef7c7d829c860
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431994"
---
# <a name="account-protection-policy-settings-for-endpoint-security-in-intune"></a>Kontoschutz-Richtlinieneinstellungen für Endpunktsicherheit in Intune

Erfahren Sie, welche Einstellungen Sie in Profilen für die Richtlinie zur *Kontoschutz* im Intune-Knoten „Endpunktsicherheit“ als Teil einer [Endpunktsicherheitsrichtlinie](../protect/endpoint-security-policy.md) konfigurieren können.

Unterstützte Plattformen und Profile:

- **Windows 10 und höher**:
  - Profil: **Kontoschutz (Vorschau)** *(Vorschau)*


## <a name="account-protection-profile"></a>Kontoschutzprofile

### <a name="account-protection"></a>Kontoschutz

- **Windows Hello for Business blockieren**

  Windows Hello for Business ist eine alternative Methode zum Anmelden bei Windows durch Ersetzen von Kennwörtern, Smartcards und virtuellen Smartcards.
  - **Nicht konfiguriert** (*Standardeinstellung*): Geräte stellen Windows Hello for Business bereit.
  - **Deaktiviert**: Geräte stellen Windows Hello for Business bereit.
  - **Aktiviert**: Geräte stellen Windows Hello for Business für keinen Benutzer bereit.
  
- **Aktivieren, um Sicherheitsschlüssel zur Anmeldung zu verwenden**

  Aktivieren Sie den Windows Hello-Sicherheitsschlüssel als Anmeldeinformation zur Anmeldung für alle Computer im Mandanten.
  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Ja**

- **Credential Guard aktivieren**  
  [CSP: []DeviceGuard](https://go.microsoft.com/fwlink/?linkid=872424)

  Credential Guard verwendet Windows Hypervisor, um Schutz zu bieten. Credential Guard erfordert Hardwareunterstützung für sicheren Start und DMA-Schutz. Diese Einstellung ist nur auf Geräten erfolgreich, die die Hardwareanforderungen erfüllen.
  - **Nicht konfiguriert** (*Standardeinstellung*): Die Verwendung von Credential Guard wird deaktiviert. Hierbei handelt es sich um die Windows-Standardeinstellung.
  - **Mit UEFI-Sperre aktivieren**: Credential Guard wird aktiviert und kann nicht remote deaktiviert werden, weil die UEFI-Konfiguration manuell gelöscht werden muss.
  - **Ohne UEFI-Sperre aktivieren**: Credential Guard wird aktiviert und kann ohne physischen Zugriff auf den Computer deaktiviert werden.

## <a name="next-steps"></a>Nächste Schritte

[Endpunktsicherheitsrichtlinie für Kontoschutz](../protect/endpoint-security-account-protection-policy.md)
