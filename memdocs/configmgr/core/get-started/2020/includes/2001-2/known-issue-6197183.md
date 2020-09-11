---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/03/2020
ms.openlocfilehash: c7fce3664d23d6402d28b053129fb2b15b540a87
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89644367"
---
### <a name="cant-create-or-edit-some-collections"></a><a name="ki_coll"></a> Erstellen oder Bearbeiten einiger Sammlungen nicht möglich

<!--6197183-->
In dieser Version der Technical Preview-Verzweigung können Sie keine neue Sammlung erstellen. Außerdem können Sie die Eigenschaften einer vorhandenen Benutzersammlung nicht bearbeiten.

Verwenden Sie in Configuration Manager PowerShell-Cmdlets, um neue Sammlungen zu erstellen und vorhandene Benutzersammlungen zu bearbeiten. Einige der verfügbaren Cmdlets zum Verwalten von Sammlungen umfassen Folgendes:

- [New-CMCollection](/powershell/module/configurationmanager/new-cmcollection)

- [Get-CMCollection](/powershell/module/configurationmanager/get-cmcollection)

- [Set-CMCollection](/powershell/module/configurationmanager/set-cmcollection#related-links)

- [Add-CMCollectionMembershipRule](/powershell/module/configurationmanager/add-cmcollectionmembershiprule)