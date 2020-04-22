---
title: Run Meter Summarization-Tool
titleSuffix: Configuration Manager
description: Verwenden Sie das Run Meter Summarization-Tool, um Tasks für die Zusammenfassung von Softwaremessungen in Configuration Manager auszulösen.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d27f88fe-817f-4af4-b290-c16f2e46cf31
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 599cc2f552b975fa9b40c94ea413f6b80b04a1a3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707538"
---
# <a name="run-meter-summarization-tool"></a>Run Meter Summarization-Tool

*Gilt für: Configuration Manager (Current Branch)*

Das Run Meter Summarization-Tool gehört zu den [Configuration Manager-Tools](tools.md). Verwenden Sie dieses Tool, um Wartungstasks für die Zusammenfassung von Softwaremessungen für primäre Standorte sofort auszulösen. Standardmäßig werden diese Tasks nach Zeitplan in **Standortwartungstasks** ausgeführt. Diese starten täglich um 0 Uhr. 

Sie fassen die Daten in der SQL-Tabelle **MeterData** zusammen und schreiben die Ergebnisse dieser Zusammenfassungen in die Tabellen **FileUsageSummary** und **MonthlyUsageSummary**. Anschließend wird das Ergebnis in Softwaremessungsberichten angezeigt. Jeder Configuration Manager-Benutzer mit Administratorrechten, der eine Verbindung mit der Datenbank für den primären Standort herstellen kann, kann das Tool ausführen, um den Zusammenfassungsvorgang auszuführen. 

Dieses Tool führt die Tasks **Dateiverwendungszusammenfassung** und **Monatliche Verwendungsdatenzusammenfassung** aus, die für die Zusammenfassung von Daten zu Softwaremessungen zuständig sind. Es fasst sämtliche vorhandenen Messdaten sofort zusammen. Die gewöhnliche Wartezeit von 12 Stunden gilt nicht. Führen Sie es auf dem Server für SQL Server aus, der die Standortdatenbank hostet. Wenn der Zusammenfassungsvorgang erfolgreich abgeschlossen werden kann, wird der Exitcode auf `0` festgelegt. Wenn ein Fehler auftritt, wird der Exitcode auf `1` festgelegt.



## <a name="usage"></a>Verwendung

### <a name="command-line"></a>Befehlszeile

`runmetersumm  [sms database name]  <delay in hours for summarization <default=0>>`


### <a name="options"></a>Optionen

#### <a name="database-name"></a>Datenbankname
Der Name der Standortdatenbank auf dem Server für SQL Server.

#### <a name="delay-in-hours-for-summarization"></a>Verzögerung der Zusammenfassung in Stunden
Das Tool fasst die Softwaremessungsnutzung vor der entstandenen Verzögerung zusammen. Standardmäßig ist diese Verzögerung auf 0 (null) festgelegt.


### <a name="example"></a>Beispiel

#### <a name="summarize-the-software-metering-usage-generated-12-hours-ago"></a>Zusammenfassen der Softwaremessungsnutzung der vergangenen 12 Stunden

`runmetersumm CCM_ABC <12>`



## <a name="see-also"></a>Weitere Informationen:

- [Wartungstasks](../servers/manage/maintenance-tasks.md)
- [Überwachen der App-Nutzung mittels Softwaremessung](../../apps/deploy-use/monitor-app-usage-with-software-metering.md)
