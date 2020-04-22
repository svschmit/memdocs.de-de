---
title: Softwareinventur
titleSuffix: Configuration Manager
description: Erhalten Sie eine Einführung in die Softwareinventur in Configuration Manager.
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 79eb49da-cd2b-4ffc-b355-b595aeba3aea
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 07b6f0108125c97128ddc88b663b0af4dabadbe7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695388"
---
# <a name="introduction-to-software-inventory-in-configuration-manager"></a>Einführung in die Softwareinventur in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Sie verwenden die Softwareinventur, um Informationen zu Dateien auf Clientgeräten zu sammeln. Ferner können bei der Softwareinventur Dateien von Clientgeräten gesammelt und auf dem Standortserver gespeichert werden. Das Softwareinventar wird erfasst, wenn Sie in den Clienteinstellungen die Einstellung **Softwareinventur auf Clients aktivieren** aktivieren. Außerdem können Sie den Vorgang in den Clienteinstellungen planen.  

Nachdem die Softwareinventur aktiviert und ein Softwareinventurzyklus von den Clients ausgeführt wurde, werden die vom einzelnen Client gesammelten Informationen an einen Verwaltungspunkt am Standort des Clients gesendet. Der Verwaltungspunkt leitet diese Inventurinformationen dann an den Configuration Manager-Standortserver weiter, auf dem die Informationen in der Standortdatenbank gespeichert werden.

 Sie können Softwareinventurdaten auf verschiedene Weise anzeigen:  

- [Erstellen von Abfragen](../../../../core/servers/manage/create-queries.md), die Geräte mit angegebenen Dateien zurückgeben   

- Erstellen von [abfragebasierten Sammlungen](../../../../core/clients/manage/collections/introduction-to-collections.md), die Geräte mit angegebenen Dateien enthalten   

- [Ausführen von Berichten](../../../servers/manage/introduction-to-reporting.md), die Details zu Dateien auf Geräten bereitstellen

- Verwenden von [Ressourcen-Explorer](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md), um detaillierte Informationen zu den Dateien anzuzeigen, die von Clientgeräten inventarisiert und gesammelt wurden   

 Beim Ausführen der Softwareinventur auf einem Clientgerät enthält der erste Bericht ein vollständiges Inventar. Alle nachfolgenden Berichte enthalten lediglich Deltainventurinformationen. Vom Standortserver werden die Deltainformationen in der empfangenen Reihenfolge verarbeitet. Falls Deltainformationen für einen Client fehlen, werden weitere Deltainformationen vom Standortserver zurückgewiesen, und der Client erhält die Anweisung zur Ausführung einer vollständigen Inventur.  

 Eine Ermittlung von Dual-Boot-Computern ist in Configuration Manager zwar möglich, es werden jedoch nur die Inventurinformationen von dem Betriebssystem zurückgegeben, das zum Zeitpunkt der Inventur aktiv war.  
