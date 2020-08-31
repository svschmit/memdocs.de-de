---
title: Festlegen des BitLocker-Verschlüsselungsalgorithmus für Autopilot-Geräte
ms.reviewer: ''
manager: laurawi
description: Microsoft InTune bietet eine umfassende Reihe von Konfigurationsoptionen für die Verwaltung von BitLocker auf Windows 10-Geräten.
keywords: Autopilot, BitLocker, Encryption, 256-Bit, Windows 10
ms.prod: w10
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: deploy
ms.localizationpriority: medium
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: f72410d0570e1b9ebbc324f26a288100e744f422
ms.sourcegitcommit: 41e6e6b7f5c2a87aaf7f23d90d0f175dd63c0579
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2020
ms.locfileid: "89056989"
---
# <a name="setting-the-bitlocker-encryption-algorithm-for-autopilot-devices"></a>Festlegen des BitLocker-Verschlüsselungsalgorithmus für Autopilot-Geräte

**Zielgruppe**

-  Windows 10

Mit Windows Autopilot können Sie die BitLocker-Verschlüsselungseinstellungen so konfigurieren, dass Sie vor dem Start der automatischen Verschlüsselung angewendet werden. Mit dieser Konfiguration wird sichergestellt, dass der Standard Verschlüsselungsalgorithmus nicht automatisch angewendet wird. Andere BitLocker-Richtlinien können auch angewendet werden, bevor die automatische BitLocker-Verschlüsselung beginnt. 

Der BitLocker-Verschlüsselungsalgorithmus wird verwendet, wenn BitLocker zum ersten Mal aktiviert wird. Der Algorithmus legt die Stärke für die vollständige Volumeverschlüsselung fest. Folgende Verschlüsselungsalgorithmen sind verfügbar: AES-CBC 128-Bit, AES-CBC 256-Bit, XTS-AES 128-Bit oder XTS-AES-256-Bit-Verschlüsselung. Der Standardwert ist XTS-AES-128-Bit-Verschlüsselung. Informationen zu den empfohlenen Verschlüsselungsalgorithmen finden Sie unter [BitLocker CSP](/windows/client-management/mdm/bitlocker-csp) .

Um sicherzustellen, dass der gewünschte BitLocker-Verschlüsselungsalgorithmus festgelegt wird, bevor die automatische Verschlüsselung für Autopilot-Geräte erfolgt:

1. Konfigurieren Sie die [Einstellungen der Verschlüsselungsmethode](/intune/endpoint-protection-windows-10#windows-encryption) im Windows 10-Endpoint Protection Profil mit dem gewünschten Verschlüsselungsalgorithmus. 
2. [Weisen Sie die Richtlinie](/intune/device-profile-assign) ihrer Autopilot-Gerätegruppe zu. Die Verschlüsselungs Richtlinie muss den **Geräten** in der Gruppe zugewiesen werden, nicht an den Benutzern.
3. Aktivieren Sie die [Seite](enrollment-status.md) Autopilot-Anmeldungs Status (ESP) für diese Geräte. Wenn das ESP nicht aktiviert ist, gilt die Richtlinie nicht, bevor die Verschlüsselung gestartet wird.

Unten ist ein Beispiel für Microsoft InTune Windows-Verschlüsselungseinstellungen angegeben.

![BitLocker-Verschlüsselungseinstellungen](images/bitlocker-encryption.png)

Ein Gerät, das automatisch verschlüsselt wird, muss vor dem Ändern des Verschlüsselungsalgorithmus entschlüsselt werden.

Die Einstellungen sind unter **Geräte Konfigurations**  >  **profile**  >  **Profil**  >  **Plattform** erstellen = Windows 10 und höher, Profiltyp = Endpoint Protection > **Konfigurieren**der  >  BitLocker-Basis Einstellungen für die**Windows-Verschlüsselung**  >  **BitLocker base settings**, Konfigurieren der Verschlüsselungsmethoden = enable verfügbar.

Außerdem wird empfohlen, Windows- **Verschlüsselung**  >  **Windows-Einstellungen**  >  **verschlüsseln** = erforderlich festzulegen.

## <a name="requirements"></a>Anforderungen

Windows 10, Version 1809 oder höher.

## <a name="next-steps"></a>Nächste Schritte

[BitLocker-Übersicht](/windows/security/information-protection/bitlocker/bitlocker-overview)