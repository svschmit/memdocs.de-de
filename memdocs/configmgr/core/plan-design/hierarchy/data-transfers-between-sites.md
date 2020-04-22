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
ms.openlocfilehash: 6b6d4eab77d0543f9001cef2c1e2b618ba3e4328
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703618"
---
# <a name="data-transfers-between-sites"></a>Datenübertragungen zwischen Standorten

*Gilt für: Configuration Manager (Current Branch)*

Configuration Manager verwendet die *dateibasierte Replikation* und die *Datenbankreplikation* zur Übertragung unterschiedlicher Informationsarten zwischen den Standorten. Erfahren Sie, wie Configuration Manager Daten zwischen Standorten verschiebt, und wie Sie die Übertragung von Daten in Ihrem Netzwerk verwalten können.  

## <a name="types-of-replication"></a>Typen der Replikation

### <a name="file-based-replication"></a><a name="bkmk_fileroute" /> Dateibasierte Replikation

Mithilfe der dateibasierten Replikation werden dateibasierte Daten von Configuration Manager zwischen den Standorten in Ihrer Hierarchie übertragen. Zu diesen Daten zählen Anwendungen und Pakete, die Sie an Verteilungspunkten in untergeordneten Standorten bereitstellen möchten. Dazu gehören auch nicht verarbeitete Ermittlungsdatensätze, die an übergeordnete Standorte übertragen und anschließend verarbeitet werden.  

Weitere Informationen finden Sie unter [Dateibasierte Replikation](file-based-replication.md).

### <a name="database-replication"></a><a name="bkmk_dbrep" /> Datenbankreplikation

Die Configuration Manager-Datenbankreplikation verwendet SQL Server für die Datenübertragung. Durch dieses Verfahren werden Änderungen in der Standortdatenbank mit den Informationen aus der Datenbank an anderen Standorten in der Hierarchie zusammengeführt.

Weitere Informationen finden Sie unter [Datenbankreplikation](database-replication.md).

Hilfe zur Problembehandlung bei der SQL-Replikation finden Sie unter [Problembehandlung der SQL-Replikation](../../servers/manage/replication/overview.md).

## <a name="see-also"></a>Weitere Informationen:

[Überwachen der Replikation](../../servers/manage/monitor-replication.md)
