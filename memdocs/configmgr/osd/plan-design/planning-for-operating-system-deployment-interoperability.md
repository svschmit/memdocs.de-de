---
title: Interoperabilität der Betriebssystembereitstellung
titleSuffix: Configuration Manager
description: Grundlegendes zu Interoperabilitätsproblemen, wenn verschiedene Configuration Manager-Standorte in einer einzelnen Hierarchie verschiedene Versionen verwenden.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: e327ce38-6c07-4a27-b6eb-7e5bf74ed04b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5931c43f0f8513ea1819e00f4eac7ecfd35dc717
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708078"
---
# <a name="plan-for-os-deployment-interoperability"></a>Planen der Interoperabilität der Betriebssystembereitstellung

*Gilt für: Configuration Manager (Current Branch)*

Wenn verschiedene Configuration Manager-Standorte in einer einzelnen Hierarchie verschiedene Versionen verwenden, sind einige Configuration Manager-Funktionen nicht verfügbar. Normalerweise sind Funktionen aus neueren Configuration Manager-Versionen für Standorte oder Clients mit einer niedrigeren Version nicht verfügbar. Weitere Informationen finden Sie unter [Interoperabilität zwischen verschiedenen Versionen von Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  


## <a name="objects"></a>Objects

Berücksichtigen Sie Folgendes beim Upgrade des Standorts der obersten Ebene in Ihrer Hierarchie, wenn andere Standorte in Ihrer Hierarchie Configuration Manager in einer niedrigeren Version ausführen:  

### <a name="client-installation-package"></a>Clientinstallationspaket  

- Die Qu für das Standard-Clientinstallationspaket wird automatisch aktualisiert. Alle Verteilungspunkte in der Hierarchie werden mit dem neuen Clientinstallationspaket aktualisiert. Dieses Verhalten tritt auch bei Verteilungspunkten an Standorten in der Hierarchie mit einer niedrigeren Version auf.  

- Sie können Clients der neuen Version nicht zu Standorten zuweisen, die Sie noch nicht mit der neuen Version aktualisiert haben. Die Zuordnung wird am Verwaltungspunkt gesperrt.  

### <a name="boot-images"></a>Startabbilder  

- Wenn Sie den Standort der obersten Hierarchieebene auf die neueste Version von Configuration Manager aktualisieren, werden die Standardbootimages (x86 und x64) automatisch aktualisiert. Das Update verwendet das Windows ADK für Windows 10, das Windows PE 10 enthält. Die Dateien, die den Standardstartimages zugeordnet sind, werden auf die neueste Configuration Manager-Version der Dateien aktualisiert. Der Standort aktualisiert benutzerdefinierte Bootimages nicht automatisch. Sie müssen benutzerdefinierte Startimages, die ältere Versionen von Windows PE enthalten, manuell aktualisieren.  

- Vermeiden Sie die Verwendung von dynamischen Medien, wenn Ihre Standorthierarchie Standorte mit unterschiedlichen Versionen von Configuration Manager enthält. Verwenden Sie stattdessen standortbasierte Medien, um einen bestimmten Verwaltungspunkt zu kontaktieren. Nachdem Sie alle Standorte auf die gleiche Version von Configuration Manager aktualisiert haben, können Sie wieder dynamische Medien verwenden.

- Stellen Sie sicher, dass die neuesten Configuration Manager-Bootimages Ihre Anpassungen enthalten. Aktualisieren Sie dann alle Verteilungspunkte der Standorte der neuesten Version mit der neuesten Version der neuen Bootimages.  

### <a name="user-state-migration-tool-usmt"></a>Migrationsprogramm für den Benutzerzustand (USMT)  

Wenn Sie den Standort der obersten Hierarchieebene auf die neueste Version von Configuration Manager aktualisieren, wird das Standardpaket von USMT automatisch auf die neueste Version aktualisiert. Benutzerdefinierte USMT-Pakete werden nicht automatisch aktualisiert. Sie müssen diese Pakete manuell aktualisieren.  

### <a name="new-task-sequence-steps"></a>Neue Tasksequenzschritte  

Mit neuen Versionen von Configuration Manager werden regelmäßig neue Tasksequenzschritte eingeführt. Wenn Sie eine Tasksequenz mit einem neuen Schritt auf älteren Clients bereitstellen, schlägt der Tasksequenzschritt fehl. Bevor Sie eine Tasksequenz mit einem neuen Schritt bereitstellen, vergewissern Sie sich, dass die Clients in der Zielsammlung auf die neue Version aktualisiert wurden.  

### <a name="os-deployment-media"></a>Medien für die Betriebssystembereitstellung  

Wenn der Standort auf eine neue Version aktualisiert wird, aktualisieren Sie alle Medien mit dem neuen Configuration Manager-Clientpaket. Zu diesen Medientypen gehören startbare, erfasste, vorab bereitgestellte und eigenständige.

### <a name="third-party-extensions-to-os-deployment"></a>Drittanbietererweiterungen für die Betriebssystembereitstellung  

Wenn Sie über Drittanbietererweiterungen für die Betriebssystembereitstellung und verschiedene Versionen von Configuration Manager-Standorten oder Configuration Manager-Clients verfügen, können Probleme mit den Erweiterungen auftreten.  


## <a name="latest-version-of-configuration-manager-sites-in-a-mixed-hierarchy"></a>Neueste Version von Configuration Manager auf Standorten in einer gemischten Hierarchie  

Wenn Sie für einen Standort ein Upgrade auf die neueste Version von Configuration Manager durchführen, starten Tasksequenzen, die sich auf das Standard-Clientinstallationspaket beziehen, automatisch die Bereitstellung der neuesten Clientversion von Configuration Manager.

Tasksequenzen, die ein benutzerdefiniertes Clientinstallationspaket referenzieren, stellen weiterhin die Clientversion bereit, die im benutzerdefinierten Paket enthalten ist. Benutzerdefinierte Pakete enthalten wahrscheinlich eine frühere Version des Configuration Manager-Clients. Aktualisieren Sie benutzerdefinierte Clientinstallationspakete auf die neueste Version, um Fehler bei der Tasksequenzbereitstellung zu vermeiden.

Wenn Sie eine Tasksequenz konfigurieren, um ein benutzerdefiniertes Clientinstallationspaket zu verwenden, führen Sie eine der folgenden Aktionen durch:

- Aktualisieren Sie den Tasksequenzschritt zur Verwendung der neuesten Version des Clientinstallationspakets von Configuration Manager
- Aktualisieren Sie das benutzerdefinierte Paket zur Verwendung der neuesten Configuration Manager-Clientinstallationsquelle

> [!IMPORTANT]  
> Stellen Sie für Clients an einem älteren Configuration Manager-Standort keine Tasksequenz bereit, die sich auf das neueste Configuration Manager-Clientinstallationspaket bezieht. Wenn Clients, die einem älteren Configuration Manager-Standort zugewiesen sind, auf die neueste Configuration Manager-Clientversion aktualisiert werden, blockiert Configuration Manager die Zuweisung zum älteren Configuration Manager-Standort. Diese Clients sind keinem Standort mehr zugewiesen. Bis Sie den Client manuell dem neuesten Configuration Manager-Standort zuweisen oder die ältere Configuration Manager-Clientversion wieder auf dem Computer installieren, werden diese Clients nicht verwaltet.


## <a name="older-versions-of-configuration-manager-in-a-mixed-hierarchy"></a>Ältere Versionen von Configuration Manager in einer gemischten Hierarchie  

Stellen Sie sicher, dass die von Ihnen bereitgestellten Tasksequenzen für die Betriebssystembereitstellung keine Clients im nicht verwalteten Zustand zurücklassen, wenn Sie Ihren Standort der zentralen Verwaltung auf die neueste Version von Configuration Manager aktualisieren. Wenn Sie die Bereitstellung beispielsweise für Clients durchführen, die einem älteren Configuration Manager-Standort zugewiesen sind, den Sie noch nicht auf die neueste Version von Configuration Manager aktualisiert haben.

Erstellen Sie eine Kopie der Tasksequenz, die Sie zum Bereitstellen der Clients für die neueste Version des Configuration Manager-Standorts verwenden. Passen Sie dann die Tasksequenz an, damit Sie sie für Clients an älteren Configuration Manager-Standorten bereitstellen können. Konfigurieren Sie die Tasksequenz so, dass sie auf ein benutzerdefiniertes Clientinstallationspaket verweist, das die ältere Configuration Manager-Clientinstallationsquelle verwendet. Wenn Sie nicht bereits über ein benutzerdefiniertes Clientinstallationspaket verfügen, das auf die ältere Configuration Manager-Clientinstallationsquelle verweist, erstellen Sie ein solches Paket manuell.  

> [!Important]  
> Ab Version 1902 können Sie ein Paket oder eine Tasksequenz nicht für einen Client der Version 5.7730 oder älter bereitstellen. Dies können Sie umgehen, indem Sie den Client auf eine neuere Version aktualisieren.<!-- SCCMDocs-pr issue #3493 -->
