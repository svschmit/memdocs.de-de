---
title: Einführung in Abfragen
titleSuffix: Configuration Manager
description: Erstellen Sie Abfragen, und führen Sie sie aus, um Objekte in einer Configuration Manager-Hierarchie zu suchen, die mit den Abfragekriterien übereinstimmen.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 03d1b3a9-41db-4d3a-a70e-e05ab5dc8141
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ff98645c7892192f2f914a25102454b5e9415fee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694568"
---
# <a name="introduction-to-queries-in-configuration-manager"></a>Einführung in Abfragen in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Sie können Abfragen erstellen und ausführen, um Objekte in einer Configuration Manager-Hierarchie zu suchen, die mit den Abfragekriterien übereinstimmen. Zu diesen Objekten gehören Elemente wie beispielsweise bestimmte Typen von Computern oder Benutzergruppen. In Abfragen können die meisten Configuration Manager-Objekttypen zurückgegeben werden, darunter Standorte, Sammlungen, Anwendungen und Inventurdaten.  

## <a name="query-creation-overview"></a>Übersicht über die Erstellung von Abfragen

 Wenn Sie eine Abfrage erstellen, müssen Sie mindestens zwei Parameter angeben: wo Sie suchen möchten und was Sie suchen möchten. Wenn Sie beispielsweise den verfügbaren Laufwerksspeicherplatz auf allen Computern eines Configuration Manager-Standorts ermitteln möchten, können Sie mit einer Abfrage über das Attribut **Freier Speicher (MB)**  der Attributklasse **Logischer Datenträger** den verfügbaren freien Speicherplatz ermitteln.  

 Nachdem Sie eine Ausgangsabfrage erstellt haben, können Sie zusätzliche Abfragekriterien angeben. Sie können z. B. festlegen, dass in den Abfrageergebnissen nur Computer eingeschlossen werden sollen, die einem bestimmten Standort zugewiesen sind. Sie können darüber hinaus die Darstellungsweise von Ergebnissen ändern, sodass Sie die Ergebnisse in einer für Sie sinnvollen Reihenfolge angezeigt werden. So können Sie beispielsweise angeben, dass die Ergebnisse in aufsteigender oder absteigender Reihenfolge nach Umfang des freien Laufwerksspeicher sortiert werden sollen.  

 Wenn Sie eine Abfrage erstellen, wird diese von Configuration Manager gespeichert und im Knoten **Abfragen** im Arbeitsbereich **Überwachung** angezeigt. Von dieser Stelle aus können Sie neue Abfragen erstellen und bestehende Abfragen ausführen, aktualisieren und verwalten.  

 Sie können eine Abfrage auch in eine Abfrageregel einer Configuration Manager-Sammlung importieren. Weitere Informationen finden Sie unter [Erstellen von Sammlungen](../../../core/clients/manage/collections/create-collections.md).  

## <a name="next-steps"></a>Nächste Schritte

 [Erstellen von Abfragen](../../../core/servers/manage/create-queries.md)
