---
title: Diagnose- und Nutzungsdaten
titleSuffix: Configuration Manager
description: Erfahren Sie mehr zu Diagnose- und Nutzungsdaten, die Configuration Manager über sich selbst sammelt.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 88ac4e55-d47b-4c94-b9c3-704c6a48b845
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6fff68eaad52f753d27971562a4bbfaa47a6cf6e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691348"
---
# <a name="diagnostics-and-usage-data-for-configuration-manager"></a>Diagnose- und Nutzungsdaten für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Configuration Manager sammelt Diagnose- und Nutzungsdaten über sich selbst, die von Microsoft zur Verbesserung der Anwendungsinstallation, der Qualität und der Sicherheit künftiger Releases verwendet werden.  

Dieses Sammeln von Diagnose- und Nutzungsdaten ist für alle Configuration Manager-Hierarchien aktiviert. Es geschieht in Form von SQL Server-Abfragen, die wöchentlich an jedem primären Standort sowie am Standort der zentralen Verwaltung ausgeführt werden. Wenn die betreffende Hierarchie einen zentralen Verwaltungsstandort verwendet, werden deren Daten von untergeordneten primären Standorten an diesen zentralen Verwaltungsstandort repliziert. Am obersten Standort Ihrer Hierarchie sendet der [Dienstverbindungspunkt](../../servers/deploy/configure/about-the-service-connection-point.md) diese Informationen, wenn er prüft, ob Updates vorhanden sind. Wenn sich der Dienstverbindungspunkt im Offlinemodus befindet, werden die Informationen mithilfe des [Dienstverbindungstools](../../servers/manage/use-the-service-connection-tool.md) übertragen.

> [!NOTE]  
> Configuration Manager sammelt Daten nur von der SQL Server-Datenbank des Standorts – nicht direkt von Clients oder Standortservern.  

Weitere Informationen finden Sie in der [Datenschutzerklärung von Microsoft](https://go.microsoft.com/fwlink/?LinkID=626527).  

> [!div class="nextstepaction"]
> [Verwenden von Diagnose- und Nutzungsdaten für Configuration Manager](how-diagnostics-and-usage-data-is-used.md)
