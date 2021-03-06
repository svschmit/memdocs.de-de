---
title: Datenübertragungen zwischen Standorten
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Configuration Manager Daten zwischen Standorten verschiebt, und wie Sie die Übertragung von Daten in Ihrem Netzwerk verwalten können.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: dc526e8d-fac3-4bb5-b206-03ad29b0ae11
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c3b74ceab892c67abbd56e8cb2a5c123374a92be
ms.sourcegitcommit: 46d4bc4fa73b22ae2a6a17a2d1cc6ec933a50e89
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88663310"
---
# <a name="data-transfers-between-sites"></a>Datenübertragungen zwischen Standorten

*Gilt für: Configuration Manager (Current Branch)*

Configuration Manager verwendet die *dateibasierte Replikation* und die *Datenbankreplikation* zur Übertragung unterschiedlicher Informationsarten zwischen den Standorten. Erfahren Sie, wie Configuration Manager Daten zwischen Standorten verschiebt, und wie Sie die Übertragung von Daten in Ihrem Netzwerk verwalten können.  

## <a name="types-of-replication"></a>Typen der Replikation

### <a name="file-based-replication"></a><a name="bkmk_fileroute" /></a> File-based replication

Mithilfe der dateibasierten Replikation werden dateibasierte Daten von Configuration Manager zwischen den Standorten in Ihrer Hierarchie übertragen. Zu diesen Daten zählen Anwendungen und Pakete, die Sie an Verteilungspunkten in untergeordneten Standorten bereitstellen möchten. Dazu gehören auch nicht verarbeitete Ermittlungsdatensätze, die an übergeordnete Standorte übertragen und anschließend verarbeitet werden.  

Weitere Informationen finden Sie unter [Dateibasierte Replikation](file-based-replication.md).

### <a name="database-replication"></a><a name="bkmk_dbrep" /></a> Database replication

Die Configuration Manager-Datenbankreplikation verwendet SQL Server für die Datenübertragung. Durch dieses Verfahren werden Änderungen in der Standortdatenbank mit den Informationen aus der Datenbank an anderen Standorten in der Hierarchie zusammengeführt.

Weitere Informationen finden Sie unter [Datenbankreplikation](database-replication.md).

Hilfe zur Problembehandlung bei der SQL-Replikation finden Sie unter [Problembehandlung der SQL-Replikation](../../servers/manage/replication/overview.md).

## <a name="see-also"></a>Weitere Informationen:

[Überwachen der Replikation](../../servers/manage/monitor-replication.md)
