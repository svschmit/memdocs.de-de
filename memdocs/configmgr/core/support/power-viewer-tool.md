---
title: Power Viewer-Tool
titleSuffix: Configuration Manager
description: Mit dem Power Viewer-Tool können Sie den Status des Features für die Energieverwaltung auf einem Konfigurations-Manager-Client anzeigen.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8143e3bf-d6bd-4c69-aec1-e6989cf2ecd9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: bcab26abe2e2a9062eda5ff80ea958010e8a7f62
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707568"
---
# <a name="power-viewer-tool"></a>Power Viewer-Tool

*Gilt für: Configuration Manager (Current Branch)*

Das Power Viewer-Tool ist eines der [Configuration Manager-Tools](tools.md). Mit diesem Tool können Sie den Status des Features für die Energieverwaltung auf einem Konfigurations-Manager-Client anzeigen.

Führen Sie **PowerVwr.exe** als Administrator aus. Wenn das Tool gestartet wird, werden die Energiefunktionen und die Energieeinstellungen des lokalen Computers auf der Registerkarte **Power Config** (Energiekonfiguration) angezeigt. 

So zeigen Sie die Energieverwaltungsdaten eines Remotecomputers an:  

1. Wechseln Sie zum Menü **Datei**, und klicken Sie auf **Verbinden**. 

2. Geben Sie den **Computernamen** und, falls erforderlich, einen **Benutzernamen** sowie ein **Kennwort** ein. 

Im Power Viewer gibt es drei Registerkarten:  

- **Power Config** (Energiekonfiguration): zeigt die Energiefunktionen und -einstellungen des Zielcomputers an.  

- **Daily Activity** (Tägliche Aktivität): zeigt Diagramme des Clients zur täglichen Aktivität an, die folgende Informationen umfassen:  

    - **Computer Ein:** der Energiestatus des Computers an einem Tag. Der Energiesparmodus gilt als ausgeschaltet.  

    - **Monitor Ein:** Status für ein- oder ausgeschalteten Monitor an einem Tag.  

    - **User Active** (Benutzer aktiv): Informationen zur Benutzeraktivität an einem Tag.  

- **Power Events** (Energieereignisse): zeigt alle Energieereignisse eines Tages an. Der Client fasst diese Ereignisse um 12:00 Uhr zusammen. Bei dieser Zusammenfassung werden Daten für das Aktivitätsdiagramm eines Tages generiert.  
