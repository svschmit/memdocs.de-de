---
title: Überwachen der Migration
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie die Configuration Manager-Konsole verwenden, um den Fortschritt und Erfolg der Migrationsaufträge zu überwachen.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: fc731d3f-edd7-4049-b17b-653d6693a564
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f9d1766a374c7abd8b13f503c3c7a64e35a5ac2c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693398"
---
# <a name="planning-to-monitor-migration-activity-in-configuration-manager"></a>Planen der Überwachung der Migrationsaktivitäten in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Mit Configuration Manager können Sie die Migration in der Configuration Manager-Konsole überwachen, die eine Verbindung mit der Zielhierarchie herstellt. Verwenden Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** den Knoten **Migration**, um Fortschritt und Erfolg der Migrationsaufträge zu überwachen. Sie können für jeden Migrationsauftrag zusammenfassende Informationen darüber anzeigen, welche Objekte migriert wurden, welche Objekte noch nicht migriert wurden und wie viele Objekte vom Migrationsauftrag ausgeschlossen sind. Außerdem finden Sie hier Informationen zu Migrationsproblemen.  

## <a name="view-migration-progress"></a>Migrationsfortschritt anzeigen  
 Für die Fortschrittanzeigen in Bezug auf einen Migrationsauftrag führen Sie eine der folgenden Aktionen durch:  

-   Erweitern Sie im Arbeitsbereich **Verwaltung** der Configuration Manager-Konsole den Knoten **Migrationsaufträge**, und wählen Sie einen Migrationsauftrag und anschließend die Registerkarte **Objekte in Auftrag** aus.  

-   Zur Überprüfung des Migrationsfortschritts oder der Identifikation von Problemen können Sie auch die Configuration Manager-Protokolldateien verwenden. Der Migrations-Manager ist der Configuration Manager-Prozess zum Nachverfolgen der Migrationsaktionen und zu deren Aufzeichnung in der Datei „migmctrl.log“ im Ordner **\&lt;InstallationPath\>\\LOGS** auf dem Standortserver.  

    > [!NOTE]  
    >  Kann ein Migrationsauftrag nicht ausgeführt werden, überprüfen Sie umgehend die Informationen in der Datei "migmctrl.log". Es werden kontinuierlich Protokolleinträge zur Datei hinzugefügt. Alte Daten werden überschrieben. Wenn Daten überschrieben werden, können Sie möglicherweise nicht mehr herausfinden, ob Probleme mit migrierten Objekten in Zusammenhang mit Migrationsproblemen stehen. Unabhängig davon, mit welchem Standort eine Verbindung Ihrer Configuration Manager-Konsole beim Konfigurieren der Migration hergestellt wird, werden Migrationsaktivitäten auf dem Standort der obersten Ebene der Hierarchie protokolliert.  

-   Verwenden Sie die Berichterstellung in Configuration Manager. In Configuration Manager stehen mehrere integrierte Berichte für Migrationsaufträge zur Verfügung, die Sie bei Bedarf auch an Ihre Anforderungen anpassen können. Weitere Informationen zu Configuration Manager-Berichten finden Sie unter [Einführung in die Berichterstellung](../servers/manage/introduction-to-reporting.md).  
