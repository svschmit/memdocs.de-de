---
title: Benutzerdefinierte Speicherorte von Datenbankdateien
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie benutzerdefinierte Speicherorte für SQL Server-Datenbankdateien angeben.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 500a9aa6-68aa-44eb-bf49-350c1314a697
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e8e4bf4eb11502d798ffa97500436494bc639aae
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607597"
---
# <a name="custom-locations-for-configuration-manager-site-database-files"></a>Benutzerdefinierte Dateispeicherorte für Standortdatenbanken mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

 Configuration Manager unterstützt benutzerdefinierte Speicherorte für SQL Server-Datenbankdateien.  

> [!NOTE]  
>  Die Option zur Angabe der vom Standard abweichenden Speicherorte ist nicht verfügbar, wenn Sie einen SQL Server-Cluster verwenden.  

 **Während des Setups** eines neuen primären Standorts oder eines Standorts der zentralen Verwaltung haben Sie folgende Möglichkeiten:  

-   **Angeben nicht standardmäßiger Dateispeicherorte für die Standortdatenbank:** Das Configuration Manager-Setup erstellt dann die Standortdatenbank mithilfe dieser Speicherorte.  

-   **Angeben der Nutzung einer vorab erstellten SQL Server-Datenbank, die benutzerdefinierte Dateispeicherorte verwendet:**  Das Configuration Manager-Setup verwendet dann diese vorab erstellte Datenbank und ihre vorkonfigurierten Dateispeicherorte.  

**Nach dem Setup** können Sie den Speicherort der Standortdatenbankdateien ändern. Dazu müssen Sie den Standort beenden und den Dateispeicherort in SQL Server bearbeiten:  

-   Beenden Sie auf dem Configuration Manager-Standortserver den Dienst **SMS_Executive**.  

-   Weitere Informationen zum Verschieben einer Benutzerdatenbank finden Sie unter [Verschieben von Benutzerdatenbanken](/sql/relational-databases/databases/move-user-databases).  

-   Starten Sie nach dem Verschieben der Datenbankdateien den Dienst **SMS_Executive** auf dem Configuration Manager-Standortserver neu.