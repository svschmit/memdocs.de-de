---
title: Planen der Standortdatenbank
titleSuffix: Configuration Manager
description: Beachten Sie bei der Planung Ihrer Configuration Manager-Hierarchie die Standortdatenbank und den Standortdatenbankserver.
ms.date: 03/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 104fb4cc-6e83-40a3-8e6b-ac909fb9ec7d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a32f0a59a0b3ce3ad864fecf61fe7281b8ebbdd2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704418"
---
# <a name="plan-for-the-site-database-for-configuration-manager"></a>Planen der Standortdatenbank für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Der Standortdatenbankserver ist ein Computer, auf dem eine unterstützte Version von Microsoft SQL Server ausgeführt wird. Von SQL Server werden Informationen für Configuration Manager-Standorte gespeichert. Jeder Standort in einer Configuration Manager-Hierarchie enthält eine Standortdatenbank und einen Server, dem die Rolle „Standortdatenbankserver“ zugewiesen wird.  

-   Für Standorte der zentralen Verwaltung und primäre Standorte können Sie SQL Server auf dem Standortserver oder auf einem anderen Computer installieren.  

-   Für sekundäre Standorte können Sie anstelle einer vollständigen SQL Server-Installation SQL Server Express verwenden. Der Datenbankserver muss jedoch auf dem sekundären Standortserver ausgeführt werden.  

-  Für die Verwendung mit SQL-Verfügbarkeitsgruppen muss das Modell für die Datenbankwiederherstellung auf VOLLSTÄNDIG festgelegt werden.  

-  Für die Verwendung ohne SQL-Verfügbarkeitsgruppen muss das Modell für die Datenbankwiederherstellung auf EINFACH festgelegt werden.  

Weitere Informationen zu den SQL-Wiederherstellungsmodi finden Sie unter [Wiederherstellungsmodelle (SQL Server)](https://docs.microsoft.com/sql/relational-databases/backup-restore/recovery-models-sql-server).

Die folgenden SQL Server-Konfigurationen können zum Hosten der Standortdatenbank verwendet werden:  

-   Die Standardinstanz von SQL Server  

-   Eine benannte Instanz auf einem einzelnen Computer mit SQL Server  

-   Eine benannte Instanz auf einer gruppierten Instanz von SQL Server  

-   Eine SQL Server Always On-Verfügbarkeitsgruppe (ab Version 1602 von Configuration Manager)


Der SQL Server muss zum Hosten der Standortdatenbank die unter [Unterstützte SQL Server-Versionen für Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md) ausführlich beschriebenen Voraussetzungen erfüllen.  



## <a name="remote-database-server-location-considerations"></a>Beim Standort des Remotedatenbankservers zu berücksichtigen  

Wenn Sie einen Computer als Remotedatenbankserver verwenden, müssen Sie darauf achten, dass die beteiligte Netzwerkverbindung eine hohe Verfügbarkeit und Bandbreite aufweist. Der Standortserver und einige Standortsystemrollen müssen kontinuierlich mit dem Remoteserver kommunizieren, auf dem die Standortdatenbank gehostet wird.

-   Die für die Kommunikation mit dem Datenbankserver erforderliche Bandbreite hängt von einer Kombination vieler verschiedener Standort- und Clientkonfigurationen ab. Die tatsächlich erforderliche Bandbreite kann daher nicht genau vorhergesagt werden.  

-   Die Anforderungen an die Netzwerkbandbreite steigen mit jedem Computer, auf dem der SMS-Anbieter ausgeführt wird und von dem eine Verbindung mit der Standortdatenbank herstellt wird.  

-   Der Computer, auf dem SQL Server ausgeführt wird, muss sich in einer Domäne befinden, die eine bidirektionale Vertrauensstellung mit dem Standortserver und allen Computern hat, auf denen der SMS-Anbieter ausgeführt wird.  

-   Sie können für den Standortdatenbankserver keinen gruppierten SQL Server verwenden, wenn die Standortdatenbank sich auf dem gleichen Computer wie der Standortserver befindet.  


In der Regel unterstützt ein Standortsystemserver nur die Standortsystemrollen von einem einzigen Configuration Manager-Standort. Sie können jedoch verschiedene Instanzen von SQL Server auf gruppierten oder nicht gruppierten Servern mit SQL Server verwenden, um eine Datenbank von verschiedenen Configuration Manager-Standorten zu hosten. Die Unterstützung von Datenbanken von unterschiedlichen Standorten setzt voraus, dass Sie jede SQL Server-Instanz für die Verwendung eindeutiger Kommunikationsports konfigurieren.  
