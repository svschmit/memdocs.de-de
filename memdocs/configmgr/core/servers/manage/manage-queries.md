---
title: Verwalten von Abfragen
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Abfragen verwalten. Enthält eine Tabelle für detaillierte Referenzinformationen.
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e562e2a0-8df8-4952-952f-e8c38461c612
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 37050a3a96b732df3f56269592e049077008ab2b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694468"
---
# <a name="how-to-manage-queries-in-configuration-manager"></a>Verwalten von Abfragen in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Dieser Artikel enthält Informationen zum Verwalten von Abfragen in Configuration Manager.  

 Informationen zum Erstellen von Abfragen finden Sie unter [Erstellen von Abfragen](../../../core/servers/manage/create-queries.md).  

## <a name="manage-queries"></a>Verwalten von Abfragen
 Wählen Sie im Arbeitsbereich **Überwachung** die Option **Abfragen**aus, markieren Sie die zu verwaltende Abfrage, und wählen Sie dann einen Verwaltungstask aus.  

 Die folgende Tabelle bietet Informationen zu Verwaltungsaufgaben.  

|Verwaltungstask|Details| 
|---------------------|-------------|
|**Ausführen**|Die ausgewählte Abfrage wird ausgeführt, und die Ergebnisse werden in der Configuration Manager-Konsole angezeigt.|
|**Client installieren**|Öffnet den **Assistenten zum Installieren von Clients**, in dem Sie den Configuration Manager-Client auf Computern installieren können, die von der ausgewählten Abfrage zurückgegeben werden.<br /><br /> Diese Option ist nicht für Abfragen verfügbar, die mobile Geräte, Benutzer oder Benutzergruppen zurückgeben. <br /><br /> Weitere Informationen zum Installieren von Configuration Manager-Clients per Clientpush finden Sie unter [Bereitstellen von Clients auf Windows-Computern](../../clients/deploy/deploy-clients-to-windows-computers.md).| 
|**Exportierenieren**|Öffnet den **Assistenten zum Exportieren von Objekten**. Mit diesem Assistenten können Sie die Abfrage in eine MOF-Datei (Managed Object Format) exportieren, die Sie dann an einem anderen Standort importieren können.
|**Verschieben**|Öffnet das Dialogfeld **Ausgewählte Elemente verschieben**. Dieses Dialogfeld dient zum Verschieben der ausgewählten Abfrage in einen Ordner, den Sie zuvor unter dem Knoten **Abfragen** erstellt haben.|

## <a name="next-steps"></a>Nächste Schritte 
 [Erstellen von Abfragen](../../../core/servers/manage/create-queries.md)
