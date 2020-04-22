---
title: Bewährte Methoden für Sammlungen
titleSuffix: Configuration Manager
description: Hier finden Sie bewährte Methoden für Sammlungen in Configuration Manager.
ms.date: 09/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7e3e7b108ef48b218ee9d6a31064606b40a68fea
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695238"
---
# <a name="best-practices-for-collections-in-configuration-manager"></a>Bewährte Methoden für Sammlungen in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Verwenden Sie die folgenden bewährten Methoden für Sammlungen in Configuration Manager.  

## <a name="dont-use-incremental-updates-with-many-collections"></a><a name="bkmk_incremental"></a> Keine Verwendung von inkrementellen Updates bei einer Vielzahl von Sammlungen

Wenn Sie die Option **Inkrementelle Updates für diese Sammlung verwenden** für zahlreiche Sammlungen aktivieren, können durch diese Konfiguration Bewertungsverzögerungen bewirkt werden. Dies gilt ab einem Schwellenwert von etwa 200 Sammlungen in Ihrer Hierarchie. Die genaue Anzahl hängt von folgenden Faktoren ab:  

- Gesamtzahl der Sammlungen  

- Häufigkeit, mit der neue Ressourcen der Hierarchie hinzugefügt und darin geändert werden  

- Anzahl der Clients in Ihrer Hierarchie  

- Komplexität der Sammlungsmitgliedschaftsregeln in Ihrer Hierarchie  

## <a name="maintenance-window-size-for-software-updates"></a>Größe des Wartungsfensters für Softwareupdates

Durch Wartungsfenster für Gerätesammlungen können Sie festlegen, dass Software nur zu bestimmten Zeiten von Configuration Manager auf diesen Geräten installiert werden kann. Wenn Sie ein zu kleines Wartungsfenster konfigurieren, kann der Client wichtige Softwareupdates möglicherweise nicht installieren. Dies erhöht das Risiko eines Angriffs, der durch diese Softwareupdates verhindert würde.

> [!Tip]
> Wichtige Überlegungen bei der Planung der Wartungsfenster:
>
> - Die maximale Standardausführungszeit für Softwareupdates beträgt 60 Minuten.
> - Bei der Berechnung, ob ein Update installiert werden kann, fügt Configuration Manager der maximalen Ausführungszeit fünf Minuten für einen möglichen Neustart hinzu.
> - Die verbleibende Dauer eines Wartungsfensters muss länger sein als die maximale Ausführungszeit des Softwareupdates plus fünf Minuten.
