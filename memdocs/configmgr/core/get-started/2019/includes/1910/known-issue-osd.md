---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 10/17/2019
ms.openlocfilehash: 668db6aa10fbee0a078eef04f0560973e5ed9454
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697848"
---
### <a name="task-sequences-arent-available-to-pxe-or-media"></a><a name="ki_osd"></a> Tasksequenzen sind für PXE oder Medien nicht verfügbar

<!--5578298-->
Wenn Sie eine Tasksequenz für PXE oder Medien (USB oder DVD) bereitstellen, empfängt der Client die Richtlinie nicht. In **smsts.log** ist die folgende Meldung enthalten:

`There are no task sequences available to this computer.`

#### <a name="workaround"></a>Problemumgehung

Starten Sie die Tasksequenz aus dem Softwarecenter.
