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
ms.openlocfilehash: 8ea2e0de96887e8f7d97633a041721462b81d6c8
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908298"
---
# <a name="setting-the-bitlocker-encryption-algorithm-for-autopilot-devices"></a>Festlegen des BitLocker-Verschlüsselungsalgorithmus für Autopilot-Geräte

**Zielgruppe**

-   Windows 10

Mit Windows Autopilot können Sie die BitLocker-Verschlüsselungseinstellungen so konfigurieren, dass Sie vor dem Start der automatischen Verschlüsselung angewendet werden. Dadurch wird sichergestellt, dass der Standard Verschlüsselungsalgorithmus nicht automatisch angewendet wird, wenn dies nicht die gewünschte Einstellung ist. Andere BitLocker-Richtlinien, die vor der Verschlüsselung angewendet werden müssen, können auch vor Beginn der automatischen BitLocker-Verschlüsselung übermittelt werden. 

Der BitLocker-Verschlüsselungsalgorithmus wird verwendet, wenn BitLocker zum ersten Mal aktiviert wird, und legt die Stärke fest, mit der die vollständige Volumeverschlüsselung erfolgen soll. Folgende Verschlüsselungsalgorithmen sind verfügbar: AES-CBC 128-Bit, AES-CBC 256-Bit, XTS-AES 128-Bit oder XTS-AES-256-Bit-Verschlüsselung. Der Standardwert ist XTS-AES-128-Bit-Verschlüsselung. Informationen zu den empfohlenen Verschlüsselungsalgorithmen finden Sie unter [BitLocker CSP](/windows/client-management/mdm/bitlocker-csp) .

So stellen Sie sicher, dass der gewünschte BitLocker-Verschlüsselungsalgorithmus vor der automatischen Verschlüsselung für Autopilot-Geräte festgelegt wird:

1. Konfigurieren Sie die [Einstellungen der Verschlüsselungsmethode](/intune/endpoint-protection-windows-10#windows-encryption) im Windows 10-Endpoint Protection Profil mit dem gewünschten Verschlüsselungsalgorithmus. 
2. [Weisen Sie die Richtlinie](/intune/device-profile-assign) ihrer Autopilot-Gerätegruppe zu. 
    - **Wichtig**: die Verschlüsselungs Richtlinie muss den **Geräten** in der Gruppe zugewiesen werden, nicht in den Benutzern.
3. Aktivieren Sie die [Seite](enrollment-status.md) Autopilot-Anmeldungs Status (ESP) für diese Geräte. 
    - **Wichtig**: Wenn ESP nicht aktiviert ist, gilt die Richtlinie nicht, bevor die Verschlüsselung gestartet wird.

Unten ist ein Beispiel für Microsoft InTune Windows-Verschlüsselungseinstellungen angegeben.

   ![BitLocker-Verschlüsselungseinstellungen](images/bitlocker-encryption.png)

**Hinweis**: ein automatisch verschlüsseltes Gerät muss vor dem Ändern des Verschlüsselungsalgorithmus entschlüsselt werden.

Die Einstellungen finden Sie unter Gerätekonfiguration-> profile-> Create profile-> Platform = Windows 10 und höher, Profile Type = Endpoint Protection-> configure-> Windows Encryption-> BitLocker Base Settings, configure Encryption Methods = enable.

**Hinweis**: Es wird auch empfohlen, die Windows-Verschlüsselung-> Windows-Einstellungen > Verschlüsselung = **erforderlich**festzulegen.

## <a name="requirements"></a>Requirements (Anforderungen)

Windows 10, Version 1809 oder höher.

## <a name="see-also"></a>Weitere Informationen

[BitLocker-Übersicht](/windows/security/information-protection/bitlocker/bitlocker-overview)