---
title: Planen der Clientmigration
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über die Tasks, mit denen Clients aus einer Quellhierarchie zu einer Zielhierarchie mit Current Branch von Configuration Manager migriert werden.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2e27b0b7-7bd3-45cd-bc99-9c991606c637
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c0885cab43deacf7e7f487e5c20e171f6475b302
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704558"
---
# <a name="plan-a-client-migration-strategy-in-configuration-manager"></a>Planen einer Strategie für die Clientmigration in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Sie müssen zwei Tasks ausführen, um Clients aus einer Quellhierarchie zu einer Zielhierarchie mit Current Branch von Configuration Manager zu migrieren. Sie müssen die mit dem Client verknüpften Objekte migrieren und die Clients aus der Quellhierarchie in der Zielhierarchie neu installieren oder neu zuweisen. Migrieren Sie zuerst die Objekte, damit diese verfügbar sind, wenn die Clients migriert werden. Die dem Client zugeordneten Objekte werden über Migrationsaufträge migriert. Informationen dazu, wie Sie mit dem Client verknüpfte Objekte migrieren können, finden Sie unter [Planen einer Strategie für Migrationsaufträge](../../core/migration/planning-a-migration-job-strategy.md).  

 Verwenden Sie die folgenden Abschnitte, um zu planen, wie Sie Clients zur Zielhierarchie migrieren.  

-   [Planen der Migration von Clients in die Zielhierarchie](#Planning_for_Client_Agent_Migration)  

-   [Planen der Behandlung von auf Clients hinterlegten Daten während der Migration](#Planning_for_Client_Data_Migration)  

-   [Planen der Inventur- und Konformitätsdaten während der Migration](#Planning_for_Inventory_data_migration)  

##  <a name="plan-to-migrate-clients-to-the-destination-hierarchy"></a><a name="Planning_for_Client_Agent_Migration"></a> Planen der Migration von Clients in die Zielhierarchie  
 Wenn Sie Clients von einer Quellhierarchie migrieren, wird für die Clientsoftware auf dem Clientcomputer ein Upgrade durchgeführt, sodass sie mit der Produktversion der Zielhierarchie übereinstimmt.  

-   **Quellhierarchie für Configuration Manager 2007:** Wenn Sie Clients aus einer Quellhierarchie migrieren, in der eine unterstützte Version von Configuration Manager ausgeführt wird, wird für die Zielhierarchie von der Clientsoftware ein Upgrade auf die Clientversion durchgeführt.  

-   **Quellhierarchie für System Center 2012 Configuration Manager oder höher:** Wenn Sie Clients zwischen Hierarchien der gleichen Produktversion migrieren, werden keine Änderungen und keine Upgrades der Clientsoftware vorgenommen. Stattdessen wird der Client aus der Quellhierarchie einem Standort in der Zielhierarchie neu zugewiesen.  

    > [!NOTE]  
    >  Wenn für die Produktversion einer Hierarchie die Migration zu Ihrer Zielhierarchie nicht unterstützt wird, führen Sie für alle Standorte und Clients in der Quellhierarchie ein Upgrade auf eine kompatible Produktversion aus. Nach der Aktualisierung der Quellhierarchie auf eine unterstützte Produktversion können Sie Migrationen zwischen den einzelnen Hierarchien ausführen. Weitere Informationen finden Sie im Abschnitt [Versionen von Configuration Manager, die für die Migration unterstützt werden](../../core/migration/prerequisites-for-migration.md#BKMK_SupportedMigrationVersions) des Artikels [Voraussetzungen für die Migration](../../core/migration/prerequisites-for-migration.md).  

Die folgenden Informationen helfen Ihnen bei der Planung der Clientmigration:  

-   Sie können jede Clientbereitstellungsmethode verwenden, die für die Bereitstellung von Clients in der Zielhierarchie unterstützt wird, um Upgrades oder Neuzuweisungen von Clients von einem Quellstandort an einen Zielstandort auszuführen. Typische Clientbereitstellungsmethoden sind Clientpushinstallation, Softwareverteilung, Gruppenrichtlinien und softwareupdatebasierte Clientinstallation. Weitere Informationen finden Sie unter [Informationen zu Clientinstallationsmethoden](../../core/clients/deploy/plan/client-installation-methods.md).  

-   Stellen Sie sicher, dass das Gerät, auf dem die Clientsoftware in der Quellhierarchie ausgeführt wird, die Mindesthardwareanforderungen erfüllt und dass auf dem Gerät ein Betriebssystem ausgeführt wird, das von der Version von Configuration Manager in der Zielhierarchie unterstützt wird.  

-   Bevor Sie einen Client migrieren, führen Sie einen Migrationsauftrag aus, um die Informationen zu migrieren, die vom Client in der Zielhierarchie verwendet werden.  

-   Für Clients, für die ein Upgrade durchgeführt wird, wird der Ausführungsverlauf beibehalten. So wird verhindert, dass Bereitstellungen in der Zielhierarchie unnötigerweise erneut ausgeführt werden.  

    -   Für Configuration Manager 2007-Clients wird der Ausführungsverlauf der Ankündigungen beibehalten.  

    -   Für System Center 2012 Configuration Manager-Clients oder Clients mit Current Branch von Configuration Manager wird der Ausführungsverlauf der Bereitstellungen beibehalten.  

-   Sie können Clients in beliebiger Reihenfolge von Standorten in der Quellhierarchie migrieren. Es wird jedoch empfohlen, eine begrenzte Anzahl von Clients in mehreren Phasen zu migrieren, anstelle einer großen Anzahl von Clients auf einmal. Eine Migration in Phasen reduziert die Anforderungen an Netzwerkbandbreite und Serververarbeitung, wenn von den aktualisierten Clients die erste vollständige Inventur und die Kompatibilitätsdaten an den zugewiesenen Standort übermittelt werden.  

-   Wenn Sie Configuration Manager 2007-Clients migrieren, wird die vorhandene Clientsoftware auf dem Clientcomputer deinstalliert und die neue Clientsoftware installiert.  

-   Configuration Manager kann einen Configuration Manager 2007-Client mit installiertem App-V-Client nur migrieren, wenn die App-V-Clientversion 4.6 SP1 oder neuer ist.  

Sie können den Clientmigrationsprozess im Knoten **Migration** des Arbeitsbereichs **Verwaltung** in der Configuration Manager-Konsole überwachen.  

Nachdem Sie den Client zur Zielhierarchie migriert haben, können Sie das Gerät nicht mehr über die Quellhierarchie verwalten, und Sie sollten den Client aus der Quellhierarchie entfernen. Dieser Vorgang ist keine Anforderung des Migrationsprozesses für Hierarchien, kann aber die Identifizierung eines migrierten Clients in einem Quellhierarchiebericht oder eine unkorrekte Anzahl von Ressourcen zwischen den beiden Hierarchien während des Migrationsvorgangs verhindern. Wenn ein migrierter Client beispielsweise in der Datenbank des Quellstandorts verbleibt, kann es passieren, dass ein Softwareupdatebericht ausgeführt wird, von dem der Computer fälschlicherweise als nicht verwaltete Ressource identifiziert wird, da der Client nun von der Zielhierarchie verwaltet wird.  

##  <a name="plan-to-handle-data-maintained-on-clients-during-migration"></a><a name="Planning_for_Client_Data_Migration"></a> Planen der Behandlung von auf Clients hinterlegten Daten während der Migration  
Wenn Sie einen Client aus seiner Quellhierarchie zu einer Zielhierarchie migrieren, bleiben einige Informationen auf dem Gerät zurück, während andere nach der Migration nicht mehr verfügbar sind.  

Folgende Informationen werden auf dem Clientgerät beibehalten:  

-   Der eindeutige Bezeichner (GUID), durch den ein Client seinen Informationen in der Configuration Manager-Datenbank zugeordnet wird  

-   Der Ankündigungs- oder Bereitstellungsverlauf, von dem verhindert wird, dass von Clients Ankündigungen oder Bereitstellungen unnötigerweise wiederholt in der Zielhierarchie ausgeführt werden.  

Folgende Informationen werden auf dem Clientgerät nicht beibehalten:  

-   Die Dateien im Clientcache. Falls diese Dateien vom Client für das Installieren von Software benötigt werden, werden sie erneut aus der Zielhierarchie heruntergeladen.  

-   Informationen aus der Quellhierarchie zu noch nicht ausgeführten Ankündigungen oder Bereitstellungen. Wenn Sie möchten, dass der Client Ankündigungen oder Bereitstellungen nach der Migration durchführt, dann müssen Sie diese für den Client in der Zielhierarchie erneut bereitstellen.  

-   Informationen zur Inventur. Diese Informationen werden vom Client nach der Migration erneut an den zugewiesenen Standort in der Zielhierarchie gesendet, und die neuen Clientdaten werden generiert.  

-   Kompatibilitätsdaten. Diese Informationen werden vom Client nach der Migration erneut an den zugewiesenen Standort in der Zielhierarchie gesendet, und die neuen Clientdaten werden generiert.  

Wenn ein Client migriert wird, werden die in der Configuration Manager-Clientregistrierung und im Configuration Manager-Dateipfad gespeicherten Informationen nicht beibehalten. Nach der Migration müssen diese Einstellungen erneut angewendet werden. Typische Einstellungen können Folgendes umfassen:  

-   Energieschemata  

-   Protokollierungseinstellungen  

-   Einstellungen lokaler Richtlinien  

Darüber hinaus müssen Sie einige Anwendungen eventuell erneut installieren.  

##  <a name="plan-for--inventory-and-compliance-data-during-migration"></a><a name="Planning_for_Inventory_data_migration"></a> Planen der Inventur- und Kompatibilitätsdaten während der Migration  
Die Inventur- und Kompatibilitätsdaten des Clients werden nicht gespeichert, wenn Sie einen Client zu einer Zielhierarchie migrieren. Stattdessen werden diese Informationen erneut in der Zielhierarchie erstellt, wenn von Clients das erste Mal Informationen an den zugewiesenen Standort gesendet werden. Damit die Anforderungen an Netzwerkbandbreite und Serververarbeitung verringert werden, wird empfohlen, eine begrenzte Anzahl von Clients in mehreren Phasen zu migrieren, anstelle einer großen Anzahl von Clients auf einmal.  

 Außerdem können Sie keine Anpassungen der Hardwareinventur aus einer Quellhierarchie migrieren. Diese müssen Sie unabhängig von der Migration in der Zielhierarchie einfügen. Informationen zum Erweitern der Hardwareinventur finden Sie unter [Konfigurieren der Hardwareinventur](../../core/clients/manage/inventory/configure-hardware-inventory.md).  
