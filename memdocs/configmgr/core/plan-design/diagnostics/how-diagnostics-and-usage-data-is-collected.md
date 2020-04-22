---
title: Diagnosedatensammlung
titleSuffix: Configuration Manager
description: Erfahren Sie mehr darüber, wie Configuration Manager Diagnose- und Nutzungsdaten über sich selbst sammelt.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ca40891c840e954f2828833c179f01bcbc6e7448
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688468"
---
# <a name="how-configuration-manager-collects-diagnostics-and-usage-data"></a>Wie Configuration Manager Diagnose- und Nutzungsdaten sammelt

*Gilt für: Configuration Manager (Current Branch)*

An jedem primären Standort werden wöchentlich SQL Server-Abfragen ausgeführt, um Diagnose- und Nutzungsdaten für Configuration Manager zu sammeln. In einer Hierarchie mit mehreren Standorten werden die Daten an den zentralen Verwaltungsstandort repliziert.  

Am obersten Standort einer Hierarchie sendet der Dienstverbindungspunkt diese Informationen, wenn er prüft, ob Updates vorhanden sind. Wie die Daten übermittelt werden, hängt vom Modus des Dienstverbindungspunkts ab:

- **Online:** Diagnose- und Nutzungsdaten werden automatisch einmal pro Woche vom Dienstverbindungspunkt an den Clouddienst gesendet.

- **Offline**: Diagnose- und Nutzungsdaten werden manuell mithilfe des [Dienstverbindungstools](../../servers/manage/use-the-service-connection-tool.md) übertragen.

Weitere Informationen finden Sie unter [About the service connection point (Informationen zum Dienstverbindungspunkt)](../../servers/deploy/configure/about-the-service-connection-point.md).

> [!div class="nextstepaction"]
> [Anzeigen von Diagnose- und Verwendungsdaten](view-diagnostics-and-usage-data.md)
