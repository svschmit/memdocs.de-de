---
title: Verwenden des Ressourcen-Explorers
titleSuffix: Configuration Manager
description: Verwenden des Ressourcen-Explorers zum Anzeigen der Hardwareinventur in Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: daa673169825638474fea05156fd837acbf0ba98
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690098"
---
# <a name="how-to-use-resource-explorer-to-view-hardware-inventory-in-configuration-manager"></a>Verwenden des Ressourcen-Explorers zum Anzeigen der Hardwareinventur in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Verwenden Sie den Ressourcen-Explorer in Configuration Manager zum Anzeigen von Informationen über die Hardwareinventur. Der Standort sammelt diese Informationen von Clients in Ihrer Hierarchie.  

> [!Tip]  
>  Im Ressourcen-Explorer werden keine Daten angezeigt, bis ein Hardwareinventurzyklus auf dem Client durchgeführt wird, mit dem Sie eine Verbindung herstellen.  



## <a name="overview"></a>Übersicht

Der Ressourcen-Explorer enthält die folgenden Bereiche im Zusammenhang mit Hardwareinventur:  

- **Hardware:** zeigt die neueste Hardwareinventur an, die vom angegebenen Clientgerät erfasst wird.  

    - Der Knoten **Status der Arbeitsstation** zeigt Uhrzeit und Datum der letzten Hardwareinventur des Geräts an.  

- **Hardwareverlauf:** ein Verlauf inventarisierter Elemente, die seit dem letzten Hardwareinventurzyklus verändert wurden.  

    - Erweitern Sie ein Element, um den Knoten **Aktuell** und mindestens einen Knoten mit den Verlaufsdaten anzuzeigen. Vergleichen Sie die Informationen im aktuellen Knoten mit denen des Verlaufsknotens, um die geänderten Elemente anzuzeigen.  

> [!NOTE]  
> Configuration Manager löscht standardmäßig Inventurdaten zu Hardware, die 90 Tage lang nicht mehr aktiv war. Passen Sie die Anzahl der Tage im Standortwartungstask **Veralteten Inventurverlauf löschen** an. Weitere Informationen finden Sie unter [Wartungstasks](../../../servers/manage/maintenance-tasks.md).  



## <a name="how-to-open-resource-explorer"></a><a name="bkmk_open"></a> Öffnen des Ressourcen-Explorers   

1.  Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Assets und Konformität**, und wählen Sie den Knoten **Geräte** aus. Sie können auch eine beliebige Sammlung im Knoten **Gerätesammlungen** auswählen.  

2.  Wählen Sie ein Gerät aus. Klicken Sie im Menüband auf der Registerkarte **Start** in der Gruppe **Geräte** auf **Starten**, und wählen Sie dann **Ressourcen-Explorer** aus.   

> [!Tip]  
> Klicken Sie für weitere Aktionen im Ressourcen-Explorer mit der rechten Maustaste auf ein Element im rechten Ergebnisbereich. Klicken Sie auf **Eigenschaften**, um das Element in einem anderen Format anzuzeigen.  



## <a name="use-of-large-integer-values"></a><a name="bkmk_bigint"></a> Verwenden großer ganzzahliger Werte
<!--1357880-->
In Configuration Manager 1802 und früheren Versionen war die Hardwareinventur für ganze Zahlen größer als 4.294.967.296 (2^32) eingeschränkt. Attribute wie z.B. die Festplattengröße in Bytes können diesen Grenzwert erreichen. Da der Verwaltungspunkt keine höheren ganzen Zahlen verarbeitet, werden diese Werte nicht in der Datenbank gespeichert. 

Mit Version 1806 wurde der Höchstwert auf 18.446.744.073.709.551.616 (2^64) erhöht. 

Für eine Eigenschaft mit einem Wert, der sich nicht ändert, wie die gesamte Festplattengröße, wird nach dem Upgrade des Standorts möglicherweise nicht sofort der Wert angezeigt. Die Hardwareinventur ist meistens ein Deltabericht. Der Client sendet nur die Werte, die sich ändern. Um dieses Verhalten zu umgehen, fügen Sie derselben Klasse eine andere Eigenschaft hinzu. Diese Aktion bewirkt, dass der Client alle Eigenschaften in der Klasse aktualisiert, die sich geändert haben. 



## <a name="see-also"></a>Weitere Informationen:

Informationen zum Anzeigen der Hardwareinventur von Clients, auf denen Linux oder UNIX ausgeführt wird, finden Sie unter [Überwachen von Clients für Linux- und UNIX-Server](../monitor-clients-for-linux-and-unix-servers.md).  

Ressourcen-Explorer zeigt auch die Softwareinventur an. Weitere Informationen finden Sie unter [Anzeigen der Softwareinventur mit dem Ressourcen-Explorer](use-resource-explorer-to-view-software-inventory.md).
