---
title: Codes bei Nichtkonformität
titleSuffix: Configuration Manager
description: Eine technische Referenz für die möglichen Codes von einem Configuration Manager-Client, der nicht mit der BitLocker-Richtlinie konform ist.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 6c28fa29-fc97-49ef-9fc3-cb062bdba908
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e8ee130929605f8087eb7fbef55e8a27618c3aed
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705958"
---
# <a name="non-compliance-codes"></a>Codes bei Nichtkonformität

*Gilt für: Configuration Manager (Current Branch)*

<!--3601034-->

WMI auf dem Client stellt die folgenden Codes für die Nichtkonformität zur Verfügung. Außerdem werden die Gründe beschrieben, warum ein bestimmtes Gerät als nicht konform gemeldet wird.

Es gibt verschiedene Methoden zum Anzeigen von WMI. Verwenden Sie beispielsweise den folgenden PowerShell-Befehl:

``` PowerShell
(Get-WmiObject -Class mbam_Volume -Namespace root\microsoft\mbam).ReasonsForNoncompliance
```

> [!TIP]
> Wenn das Gerät konform ist, gibt dieser Befehl nichts zurück.
>
> Sie können auch das `Compliant`-Attribut dieser Klasse prüfen, das `1` lautet, wenn das Gerät konform ist.

|Codes bei Nichtkonformität|Grund für Nichtkonformität|
|--- |--- |
|0|Verschlüsselungsstärke ist nicht AES 256.|
|1|Die BitLocker-Richtlinie erfordert, dass dieses Volume verschlüsselt wird, aber das ist es nicht.|
|2|Die BitLocker-Richtlinie erfordert, dass dieses Volume *nicht* verschlüsselt werden darf, aber es ist verschlüsselt.|
|3|Die BitLocker-Richtlinie erfordert, dass dieses Volume eine TPM-Schutzvorrichtung verwendet, was aber nicht der Fall ist.|
|4|Die BitLocker-Richtlinie erfordert, dass dieses Volume eine TPM+PIN-Schutzvorrichtung verwendet, was aber nicht der Fall ist.|
|5|Die BitLocker-Richtlinie gestattet es Nicht-TPM-Computern nicht, als konform gemeldet zu werden.|
|6|Das Volume verfügt über eine TPM-Schutzvorrichtung, aber die TPM ist nicht sichtbar.|
|7|Die BitLocker-Richtlinie erfordert, dass dieses Volume eine Kennwortschutzvorrichtung verwendet, aber es besitzt keine.|
|8|Die BitLocker-Richtlinie erfordert, dass dieses Volume *keine* Kennwortschutzvorrichtung verwendet, aber es besitzt eine.|
|9|Die BitLocker-Richtlinie erfordert, dass dieses Volume eine Schutzvorrichtung für automatisches Entsperren verwendet, aber es besitzt keine.|
|10|Die BitLocker-Richtlinie erfordert, dass dieses Volume *keine* Schutzvorrichtung für automatisches Entsperren verwendet, aber es besitzt eine.|
|11|BitLocker erkennt einen Richtlinienkonflikt, wodurch verhindert wird, dieses Volume als konform zu melden.|
|12|Zum Verschlüsseln des Betriebssystemvolumes wird ein Systemvolume benötigt, aber es ist nicht vorhanden.|
|13|Die Schutzmaßnahme für das Volume wurde angehalten.|
|14|Die Schutzvorrichtung für automatisches Entsperren ist nicht sicher, wenn das Betriebssystemvolume nicht verschlüsselt ist.|
|15|Die Richtlinie erfordert eine minimale Verschlüsselungsstärke von XTS-AES-128 Bit, die tatsächliche Verschlüsselungsstärke ist niedriger.|
|16|Die Richtlinie erfordert eine minimale Verschlüsselungsstärke von XTS-AES-256 Bit, die tatsächliche Verschlüsselungsstärke ist niedriger.|
