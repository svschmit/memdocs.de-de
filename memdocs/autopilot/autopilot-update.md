---
title: Windows Autopilot-Update
ms.reviewer: ''
manager: laurawi
description: Windows Autopilot-Update
keywords: Autopilot, Update, Windows 10
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
ms.openlocfilehash: 34db88c53cdd7db46c126f15bb60a7fd2941a627
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/04/2020
ms.locfileid: "87756759"
---
# <a name="windows-autopilot-update"></a>Windows Autopilot-Update

**Zielgruppe**

-   Windows 10, Version 1903

Mit dem Windows Autopilot-Update können Sie die neuesten Autopilot-Features und wichtige Problem Behebungen erhalten, ohne auf die neueste Version des Windows-Betriebssystems umsteigen zu müssen. Mit Autopilot Update können Organisationen ihre aktuelle Betriebssystemversion behalten und weiterhin von neuen Autopilot-Features und Fehlerbehebungen profitieren.
 
Während des Autopilot-Bereitstellungs Prozesses wurde das Windows Autopilot-Update nach der kritischen Überprüfung von [Windows Zero Day Patch (ZDP)](https://docs.microsoft.com/windows-hardware/customize/desktop/windows-updates-during-oobe) als neuer Knoten hinzugefügt. Während des Aktualisierungs Vorgangs wenden sich Windows Autopilot-Geräte an Windows Update, um nach einem neuen Autopilot-Update zu suchen.  Wenn ein Autopilot-Update verfügbar ist, wird das Update vom Gerät heruntergeladen und installiert und anschließend automatisch neu gestartet. Siehe folgendes Beispiel.

   ![Autopilot-Update 1](images/update1.png)<br>
   ![Autopilot-Update 2](images/update2.png)<br>
   ![Autopilot-Update 3](images/update3.png)

Das folgende Diagramm veranschaulicht eine typische Windows Autopilot-Bereitstellungs Orchestrierung während der Out-of-Box-Darstellung (OOBE) mit dem neuen Windows Autopilot Update-Knoten.

   ![Autopilot-Aktualisierungs Fluss](images/update-flow.png)

## <a name="release-cadence"></a>Versionsrhythmus

- Wenn ein Autopilot-Update verfügbar ist, wird es in der Regel am 4. Dienstag des Monats veröffentlicht. Das Update kann in einer anderen Woche veröffentlicht werden, wenn eine Ausnahme vorliegt.
- Es wird auch ein Knowledge Base-Artikel (KB) veröffentlicht, um die Änderungen zu dokumentieren, die im Update enthalten sind.

Eine Liste der veröffentlichten Updates finden Sie unter [Autopilot Update History](windows-autopilot-whats-new.md#windows-autopilot-update-history).

## <a name="see-also"></a>Weitere Informationen

[Während des OOBE-Windows Update](https://docs.microsoft.com/windows-hardware/customize/desktop/windows-updates-during-oobe)<br>
[Neues in Windows Autopilot](windows-autopilot-whats-new.md)<br>