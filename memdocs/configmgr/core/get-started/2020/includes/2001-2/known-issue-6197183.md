---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/03/2020
ms.openlocfilehash: fca1d884b75380f90a2e2e3cdc2fb0cac357b6b5
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88703869"
---
### <a name="cant-create-or-edit-some-collections"></a><a name="ki_coll"></a> Erstellen oder Bearbeiten einiger Sammlungen nicht möglich

<!--6197183-->
In dieser Version der Technical Preview-Verzweigung können Sie keine neue Sammlung erstellen. Außerdem können Sie die Eigenschaften einer vorhandenen Benutzersammlung nicht bearbeiten.

Verwenden Sie in Configuration Manager PowerShell-Cmdlets, um neue Sammlungen zu erstellen und vorhandene Benutzersammlungen zu bearbeiten. Einige der verfügbaren Cmdlets zum Verwalten von Sammlungen umfassen Folgendes:

- [New-CMCollection](/powershell/module/configurationmanager/new-cmcollection?view=sccm-ps)

- [Get-CMCollection](/powershell/module/configurationmanager/get-cmcollection?view=sccm-ps)

- [Set-CMCollection](/powershell/module/configurationmanager/set-cmcollection?view=sccm-ps#related-links)

- [Add-CMCollectionMembershipRule](/powershell/module/configurationmanager/add-cmcollectionmembershiprule?view=sccm-ps)