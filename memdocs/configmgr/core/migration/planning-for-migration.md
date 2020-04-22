---
title: Planen der Migration
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über Standorte und Hierarchien, bevor Sie Daten in eine Zielhierarchie in Configuration Manager (Current Branch) migrieren.
ms.date: 01/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b2bf493e-1e10-496f-a139-2646522703ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b514e2bb0843801cfa6f0f307af8a5013fc3f9e6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702828"
---
# <a name="plan-for-migration-to-configuration-manager-current-branch"></a>Planen der Migration zu Configuration Manager (Current Branch)

*Gilt für: Configuration Manager (Current Branch)*

Stellen Sie sicher, dass Sie mit Standorten und Hierarchien in Configuration Manager vertraut sind, bevor Sie Daten in eine Configuration Manager (Current Branch)-Zielhierarchie migrieren. Weitere Informationen zu Standorten und Hierarchien finden Sie unter [Grundlagen von Configuration Manager](../../core/understand/fundamentals.md).  

Installieren Sie eine Configuration Manager (Current Branch)-Hierarchie als Zielhierarchie, bevor Sie Daten aus einer unterstützten Quellhierarchie migrieren.  

Richten Sie nach dem Installieren der Zielhierarchie die Verwaltungsfeatures und -funktionen ein, die Sie in Ihrer Zielhierarchie verwenden möchten, bevor Sie mit dem Migrieren von Daten beginnen.  

Möglicherweise müssen Sie zusätzlich Vorkehrungen für eine Überlappung der Quellhierarchie mit der Zielhierarchie treffen. Beispielsweise können Sie beim Einrichten der Quellhierarchie angeben, dass die gleichen Netzwerkspeicherorte oder -grenzen wie für die Zielhierarchie verwendet werden sollen. Anschließend installieren Sie neue Clients für Ihre Zielhierarchie und verwenden die automatische Standortzuweisung. Bei diesem Szenario ist es möglich, dass vom Client eine fehlerhafte Zuweisung zur Quellhierarchie vorgenommen wird, weil vom neu installierten Configuration Manager-Client aus beiden Hierarchien ein Standort für den Beitritt ausgewählt werden kann. Planen Sie daher die Zuweisung jedes neuen Clients in der Zielhierarchie zu einem bestimmten Standort dieser Hierarchie, anstatt die automatische Standortzuweisung zu verwenden.  

Weitere Informationen zu Standortzuweisungen finden Sie im Abschnitt [Überlegungen zur Clientstandortzuweisung](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#BKMK_SupConfigSiteAssignment) des Themas [Interoperabilität zwischen verschiedenen Versionen von Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

Die folgenden Artikel sind bei der Migration einer unterstützten Quellhierarchie in eine Configuration Manager-Zielhierarchie hilfreich:

-   [Voraussetzungen für die Migration](../../core/migration/prerequisites-for-migration.md)  

-   [Administratorchecklisten zum Planen der Migration](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Bestimmen, ob Daten zu Configuration Manager migriert werden sollen](../../core/migration/determine-whether-to-migrate-data.md)  

-   [Planen einer Strategie für Quellhierarchien](../../core/migration/planning-a-source-hierarchy-strategy.md)  

-   [Administratorchecklisten zum Planen der Migration](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Planen einer Strategie für die Clientmigration](../../core/migration/planning-a-client-migration-strategy.md)  

-   [Planen einer Migrationsstrategie für die Inhaltsbereitstellung](../../core/migration/planning-a-content-deployment-migration-strategy.md)  

-   [Planen der Migration von Configuration Manager-Objekten zu Configuration Manager (Current Branch)](../../core/migration/planning-for-the-migration-of-objects.md)  

-   [Planen der Überwachung der Migrationsaktivitäten](../../core/migration/planning-to-monitor-migration-activity.md)  

-   [Planen des Abschließens der Migration](../../core/migration/planning-to-complete-migration.md)  
