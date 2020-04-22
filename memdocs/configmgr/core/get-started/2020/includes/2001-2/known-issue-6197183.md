---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/03/2020
ms.openlocfilehash: 0db30a8fdc96bc1e1d2d1ff2a059eca8d454d48e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692098"
---
### <a name="cant-create-or-edit-some-collections"></a><a name="ki_coll"></a> Erstellen oder Bearbeiten einiger Sammlungen nicht möglich

<!--6197183-->
In dieser Version der Technical Preview-Verzweigung können Sie keine neue Sammlung erstellen. Außerdem können Sie die Eigenschaften einer vorhandenen Benutzersammlung nicht bearbeiten.

Verwenden Sie in Configuration Manager PowerShell-Cmdlets, um neue Sammlungen zu erstellen und vorhandene Benutzersammlungen zu bearbeiten. Einige der verfügbaren Cmdlets zum Verwalten von Sammlungen umfassen Folgendes:

- [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection?view=sccm-ps)

- [Get-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollection?view=sccm-ps)

- [Set-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmcollection?view=sccm-ps#related-links)

- [Add-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectionmembershiprule?view=sccm-ps)
