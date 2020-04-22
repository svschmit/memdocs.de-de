---
title: Tool für den Inhaltsbesitz
titleSuffix: Configuration Manager
description: Mit dem Tool für den Inhaltsbesitz können Sie den Besitz verwaister Pakete in Configuration Manager ändern.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 753d2681-ea72-4f47-94d1-ac10188d9d5b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ee1a24a93bb71178af3a4cfbba2a406bdd958d19
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707848"
---
# <a name="content-ownership-tool"></a>Tool für den Inhaltsbesitz

*Gilt für: Configuration Manager (Current Branch)*

Das Tool für den Inhaltsbesitz ist eines der [Configuration Manager-Tools](tools.md). Es ändert den Besitz verwaister Pakete in Configuration Manager. Verwaiste Paketen verfügen über keinen besitzenden Standortserver. Pakete können verwaist werden, indem der Standortserver entfernt wird, während die Pakete weiterhin zum Standortserver gehören.

Führen Sie das Tool für den Inhaltsbesitz auf einem beliebigen Standortserver in der Configuration Manager-Hierarchie aus. Melden Sie sich als Administrator mit Zugriffsberechtigungen für Pakete an.  

> [!Tip]  
> Verwenden Sie **ContentLibraryCleanup.exe** in `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup`, um verwaiste Inhalte von einem Verteilungspunkt zu *entfernen*. Weitere Informationen finden Sie unter [Inhaltsbibliothek-Bereinigungstool](../plan-design/hierarchy/content-library-cleanup-tool.md).  



## <a name="features"></a>Features

- Anzeigen sämtlicher verwaister Pakete  

- Anzeigen sämtlicher Pakete, selbst wenn diese nicht verwaist sind  

- Anzeigen des Status der Verbindung mit einem Standort  

- Filtern von Paketen nach Name, Standortcode oder Pakettyp  

- Sortieren nach einer beliebigen angezeigten Spalte  

- Ändern einer Zuweisung von mindestens einem Paket mit einer einzigen Aktion  

- Anzeigen des Fortschritts der Aktivität zur Besitzübertragung  



## <a name="usage"></a>Verwendung

Führen Sie **ContentOwnershipTool.exe** aus, um das Tool zu starten. Für die Ausführung des Tools sind keine lokalen Administratorberechtigungen erforderlich.

Es sind keine Befehlszeilenparameter vorhanden.

> [!Important]   
> Dieses Tool ändert den Besitz eines verwaisten Pakets. Das Paket selbst wird nicht vom Verteilungspunkt verschoben, auf dem es gespeichert ist. Durch diese Besitzänderung wird keine Aktualisierung des Pakets auf Verteilungspunkten verursacht. Darüber hinaus führt die Besitzänderung nicht dazu, dass die Richtlinie für die Bereitstellung des Pakets neu ausgewertet wird. Stellen Sie nach der Änderung des Besitzes sicher, dass der neue Standortserver auf die Quelldateien zugreifen kann. Er sollte zumindest über **Leseberechtigungen** für die Quelldateien der einzelnen Pakete verfügen. 



## <a name="see-also"></a>Weitere Informationen:

- [Grundlegende Konzepte für das Content Management](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [Die Inhaltsbibliothek](../plan-design/hierarchy/the-content-library.md)
