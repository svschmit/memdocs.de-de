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
ms.openlocfilehash: a677dec0d722f0ef17a8c16248a41dea1b0be947
ms.sourcegitcommit: 42882de75c8a984ba35951b1165c424a7e0ba42e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2020
ms.locfileid: "89068120"
---
# <a name="windows-autopilot-update"></a>Windows Autopilot-Update

**Zielgruppe**

- Windows 10, Version 1903

Das Windows Autopilot-Update installiert die neuesten Autopilot-Features und-Korrekturen für Autopilot-Geräte Ihrer Organisation. Die Geräte werden nicht in die aktuelle Version des Windows-Betriebssystems verschoben. Mit Autopilot Update können Sie die aktuelle Betriebssystemversion des Geräts beibehalten und dennoch von neuen Autopilot-Features und Fehlerbehebungen profitieren.

Der Windows Autopilot-Aktualisierungs Vorgang tritt nach der wichtigen Update Überprüfung für [Windows Zero Day Patch (ZDP)](/windows-hardware/customize/desktop/windows-updates-during-oobe) auf. Während des Aktualisierungs Vorgangs überprüfen die Geräte Windows Update nach einem neuen Autopilot-Update. Wenn ein Autopilot-Update verfügbar ist, wird das Update vom Gerät heruntergeladen und installiert und anschließend automatisch neu gestartet. Siehe folgendes Beispiel.

 ![Autopilot-Update 1](images/update1.png)<br>
 ![Autopilot-Update 2](images/update2.png)<br>
 ![Autopilot-Update 3](images/update3.png)

Das folgende Diagramm veranschaulicht eine typische Windows Autopilot-Bereitstellungs Orchestrierung während der Out-of-Box-Darstellung (OOBE) mit dem neuen Windows Autopilot Update-Knoten.

 ![Autopilot-Aktualisierungs Fluss](images/update-flow.png)

## <a name="release-cadence"></a>Versionsrhythmus

- Wenn ein Autopilot-Update verfügbar ist, wird es in der Regel am vierten Dienstag des Monats veröffentlicht. Das Update kann in einer anderen Woche veröffentlicht werden, wenn eine Ausnahme vorliegt.
- Es wird auch ein Knowledge Base-Artikel (KB) veröffentlicht, um die Änderungen zu dokumentieren, die im Update enthalten sind.

Eine Liste der veröffentlichten Updates finden Sie unter [Autopilot Update History](windows-autopilot-whats-new.md#windows-autopilot-update-history).

## <a name="see-also"></a>Weitere Informationen

[Während des OOBE-Windows Update](/windows-hardware/customize/desktop/windows-updates-during-oobe)<br>
[Neues in Windows Autopilot](windows-autopilot-whats-new.md)<br>