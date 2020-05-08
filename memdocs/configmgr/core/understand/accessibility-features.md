---
title: Barrierefreiheit
titleSuffix: Configuration Manager
description: Enthält Informationen zu den Funktionen, die Configuration Manager für jeden zugänglich machen.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1cb96666-98bf-49a9-85ca-dbb53f0655e9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f04b777f030f9e55e1d5b17ace9ec8b83d9f8679
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906116"
---
# <a name="accessibility-features-in-configuration-manager"></a>Barrierefreiheitsfunktionen in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*


Configuration Manager enthält Funktionen, durch die es für jeden zugänglich gemacht wird.

> [!Note]  
> Um die Barrierefreiheitsfunktionen der Configuration Manager-Konsole zu verbessern, aktualisieren Sie ab Version 1902 .NET auf dem Computer, auf dem die Konsole ausgeführt wird, auf Version 4.7 oder höher. <!-- SCCMDocs-pr issue #3228 -->  
> 
> Weitere Informationen zu den in .NET 4.7.1 und 4.7.2 vorgenommenen Barrierefreiheitsänderungen finden Sie unter [Neuerungen bei der Barrierefreiheit in .NET Framework](https://docs.microsoft.com/dotnet/framework/whats-new/whats-new-in-accessibility).  



## <a name="keyboard-shortcuts"></a>Tastenkombinationen

### <a name="console-workspaces"></a>Konsolenarbeitsbereiche

Verwenden Sie zum Zugriff auf einen Arbeitsbereich die folgenden Tastenkombinationen:  

|Tastenkombination| Arbeitsbereich|
|--------|--------|  
|STRG+1| Bestand und Kompatibilität|
|STRG+2|  Softwarebibliothek|
|STRG+3|  Überwachung|
|STRG+4|  Verwaltung|


### <a name="other-keyboard-shortcuts"></a>Andere Tastenkombinationen

|Tastenkombination|  Zweck|
|--------|--------|  
|STRG+M|legt den Fokus auf den Hauptbereich in der Mitte fest|
|STRG+T|legt den Fokus auf den obersten Knoten im Navigationsbereich fest Wenn sich der Fokus bereits in diesem Bereich befand, wird er auf den letzten besuchten Knoten festgelegt.|
|STRG+I|legt den Fokus auf die Breadcrumb-Leiste unter dem Menüband fest|
|STRG+L|legt den Fokus auf das Feld **Suchen** fest, sofern verfügbar|
|STRG+D|legt den Fokus auf den Detailbereich fest, sofern verfügbar|
|ALT     |schaltet den Fokus auf das Menüband ein und aus|



## <a name="other-accessibility-features"></a>Andere Barrierefreiheitsfunktionen

- Geben Sie zum Navigieren im Navigationsbereich die Buchstaben eines Knotennamens ein.

- Die Tastaturnavigation durch die Hauptansicht und das Menüband erfolgt kreisförmig.

- Die Tastaturnavigation im Detailbereich erfolgt kreisförmig. Um zum vorherigen Objekt oder Bereich zurückzukehren, drücken Sie STRG+D und dann UMSCHALT+TAB.

- Nach der Aktualisierung einer Arbeitsbereichsansicht wird der Fokus auf den Hauptbereich des jeweiligen Arbeitsbereichs festgelegt.

- Wählen Sie zum Zugriff auf ein Arbeitsbereichsmenü die TAB-TASTE, bis der Fokus auf dem Symbol „Erweitern/Reduzieren“ liegt. Wählen Sie die NACH-UNTEN-TASTE, um auf das Arbeitsbereichsmenü zuzugreifen.  

- Verwenden Sie zum Navigieren durch ein Arbeitsbereichsmenü die Pfeiltasten.  

- Verwenden Sie zum Zugriff auf die verschiedenen Bereiche im Arbeitsbereich die TAB-TASTE und die Tastenkombination UMSCHALT+TAB. Verwenden Sie zum Navigieren in einem Bereich des Arbeitsbereichs, z. B. im Menüband, die Pfeiltasten.  

- Verwenden Sie dreimal UMSCHALT+TAB, um auf die Adressleiste zuzugreifen, wenn sich der Fokus auf dem Verzeichnisknoten befindet.  

- Auf einer Assistenten- oder Eigenschaftenseite können Sie per Tastenkombination durch die Felder navigieren. Wählen Sie die ALT-TASTE plus das jeweils unterstrichene Zeichen (ALT+_), um ein bestimmtes Feld auszuwählen.     

- Geben Sie den ersten Buchstaben des Namens eines Knotens ein, um zu den verschiedenen Knoten eines Arbeitsbereichs zu navigieren. Jeder Tastendruck verschiebt den Cursor auf den nächsten Knoten, der mit diesem Buchstaben beginnt. Wenn Sie eine Sprachausgabe verwenden, liest der Reader den Namen des Knotens.



## <a name="see-also"></a>Weitere Informationen:

Weitere Informationen zu den Grundlagen der Navigation in den Configuration Manager-Benutzeroberflächen finden Sie in den folgenden Artikeln:
- [Verwenden der Configuration Manager-Konsole](../servers/manage/admin-console.md)  
- [Benutzerleitfaden des Softwarecenters](software-center.md)

> [!NOTE]  
> Die in diesem Artikel enthaltenen Informationen gelten ggf. nur für Benutzer, die Microsoft-Produkte in den USA lizenzieren lassen. Wenn Sie dieses Produkt außerhalb der USA erworben haben, enthält das Softwarepaket eine Karte mit zusätzlichen Informationen, der die Kontaktinformationen für den Microsoft-Support zu entnehmen sind. Diese Informationen finden Sie auch auf der [Microsoft-Website zur Barrierefreiheit](https://www.microsoft.com/accessibility/). Setzen Sie sich mit der Niederlassung in Ihrer Nähe in Verbindung, um herauszufinden, ob die in diesem Abschnitt aufgeführten Produkte und Dienste in Ihrem Land bzw. Ihrer Region verfügbar sind. Informationen über Eingabehilfen sind in anderen Sprachen verfügbar, darunter auf Japanisch und Französisch.  

