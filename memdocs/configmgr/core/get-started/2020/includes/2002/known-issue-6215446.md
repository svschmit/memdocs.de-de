---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/13/2020
ms.openlocfilehash: 979760d1ebdd9d8f91993361921ae437ed5b81b1
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89644056"
---
### <a name="cant-delete-collections"></a><a name="ki_coll"></a> Löschen von Sammlungen nicht möglich

<!--6245446-->
In dieser Version des Technical Preview-Branchs können Sie Sammlungen nicht löschen.

Um dieses Problem zu umgehen, verwenden Sie das folgende Configuration Manager-PowerShell-Cmdlet, um Sammlungen zu löschen:

- [Remove-CMCollection](/powershell/module/configurationmanager/remove-cmcollection)