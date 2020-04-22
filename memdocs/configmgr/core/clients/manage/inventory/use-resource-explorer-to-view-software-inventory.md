---
title: Anzeigen des Softwareinventars mit dem Ressourcen-Explorer
titleSuffix: Configuration Manager
description: Mit dem Ressourcen-Explorer können Sie das Softwareinventar in Configuration Manager anzeigen.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4b7aa5f6-5ebd-49be-b7f3-4206caadc187
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 08905a72b6af6e9eae4d2cef9f4732ef692dc134
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690068"
---
# <a name="how-to-use-resource-explorer-to-view-software-inventory-in-configuration-manager"></a>Anzeigen des Softwareinventars mit dem Ressourcen-Explorer in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Zeigen Sie mithilfe des Ressourcen-Explorers in Configuration Manager Softwareinventurinformationen an, die von Computern in Ihrer Hierarchie gesammelt wurden.  

> [!NOTE]  
>  Der Ressourcen-Explorer zeigt erst dann Inventurdaten an, wenn auf dem Client ein Softwareinventurzyklus ausgeführt wurde.  

 Der Ressourcen-Explorer bietet folgende Informationen zu Hardware- und Softwareinventur:  

-   **Software**:  

    -   **Gesammelte Dateien**: Dateien, die während der Softwareinventur gesammelt wurden.  

    -   **Dateidetails**: Dateien, die bei der Softwareinventur inventarisiert wurden und keinem bestimmten Produkt oder Hersteller zugeordnet sind.  

    -   **Letzte Softwareüberprüfung**: Datum und Uhrzeit der letzten Softwareinventur und Dateisammlung, die auf dem Clientcomputer ausgeführt wurde.  

    -   **Produktdetails**: Nach Herstellern gruppierte Softwareprodukte, die von der Softwareinventur inventarisiert wurden.  

## <a name="to-run-resource-explorer-from-the-configuration-manager-console"></a>So führen Sie den Ressourcen-Explorer über die Configuration Manager-Konsole aus  

1.  Wählen Sie in der Configuration Manager-Konsole **Bestand und Konformität** aus.

2.  Wählen Sie im Arbeitsbereich **Bestand und Konformität** die Option **Geräte** aus, oder öffnen Sie eine beliebige Sammlung, in der Geräte angezeigt werden.  

3.  Wählen Sie den Computer aus, der die anzuzeigende Inventur enthält. Wählen Sie danach auf der Registerkarte **Start** > Gruppe **Geräte** **Start** > **Ressourcen-Explorer** aus.

4.  Sie können mit der rechten Maustaste auf ein beliebiges Element im Fenster „Ressourcen-Explorer“ klicken und **Eigenschaften** auswählen, um die gesammelten Inventurinformationen in einem besser lesbaren Format anzuzeigen.  
 
## <a name="view-and-manage-collected-diagnostic-files"></a><a name="bkmk_diag"> </a> Anzeigen und Verwalten von gesammelten Diagnosedateien

Ab Version 2002 von Configuration Manager verwenden Sie den Ressourcen-Explorer, um die gesammelten Dateien anzuzeigen und zu verwalten, wenn Sie die Clientbenachrichtigung zum [Sammeln von Clientprotokollen](../client-notification.md#client-diagnostics) verwenden. 

1. Klicken Sie über den Knoten **Geräte** mit der rechten Maustaste auf das Gerät, für das Sie Protokolle anzeigen möchten.
1. Wählen Sie **Start** und dann **Ressourcen-Explorer** aus.
1. Klicken Sie in **Ressourcen-Explorer** auf **Diagnosedateien**.
1. In der Liste der **Diagnosedateien** können Sie das Sammlungsdatum für die Dateien anzeigen. Das Namensformat des Clientprotokolls ist `Support_<guid>.zip`.
1. Klicken Sie mit der rechten Maustaste auf die ZIP-Datei, und wählen Sie eine der folgenden Optionen aus:
    - **Supportcenter öffnen:** Das [Supportcenter](../../../support/support-center.md) wird gestartet.
    - **Kopieren:** Die Zeileninformationen aus dem Ressourcen-Explorer werden kopiert.
    - **Datei anzeigen:** Mit dem Datei-Explorer wird ein Ordner geöffnet, in dem sich die ZIP-Datei befindet.
    - **Speichern:** Das Dialogfeld „Datei speichern“ wird für die ausgewählte Datei geöffnet.
    - **Exportieren:** Die unter **Diagnosedateien** angezeigten Spalten von Ressourcen-Explorer werden gespeichert.
    - **Aktualisieren:** Die Dateiliste wird aktualisiert.
    - **Eigenschaften:** Die Eigenschaften für die ausgewählte Datei werden zurückgegeben. 

[![Überprüfen und Speichern der Clientprotokolle über Ressourcen-Explorer](./../media/4226618-view-collected-client-logs.png)](./../media/4226618-view-collected-client-logs.png#lightbox)

## <a name="next-steps"></a>Nächste Schritte

[Verwenden Sie das Supportcenter](../../../support/support-center.md), um gesammelte Diagnosedateien anzuzeigen.
