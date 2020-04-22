---
title: Configuration Manager und Windows as a Service
titleSuffix: Configuration Manager
description: Erhalten Sie grundlegende Informationen zur Übernahme von Configuration Manager Current Branch, damit Windows as a Service unterstützt wird.
ms.date: 06/15/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c8534a1e-57b8-4688-b6e6-299d82cfcec9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e92a39a91c60734f212c7d1e99e266d0ec9a4008
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701248"
---
# <a name="configuration-manager-and-windows-as-a-service"></a>Configuration Manager und Windows as a Service

*Gilt für: Configuration Manager (Current Branch)*

Configuration Manager bietet eine umfassende Kontrolle über Featureupdates für Windows 10. Damit Sie das Modell „Windows as a Service“ vollständig übernehmen können, müssen Sie auch das Modell „Configuration Manager Current Branch“ übernehmen. Wenn Sie Ihre Windows 10-Version aktuell halten möchten, achten Sie darauf, dass stets die aktuelle Version von Configuration Manager installiert ist. Damit Sie von den praktischen neuen Unternehmensfeatures für Windows 10 profitieren können, müssen Sie immer die neuste Version von Configuration Manager installieren. In diesem Artikel wird auf die wichtigsten Artikel verwiesen, die Ihnen dabei helfen, Configuration Manager Current Branch zu übernehmen. Configuration Manager Current Branch hilft Ihnen dabei, Windows as a Service zu etablieren.

## <a name="key-articles-about-adopting-configuration-manager-current-branch"></a>Wichtige Artikel zur Übernahme von Configuration Manager Current Branch

| Artikel        | Beschreibung          | 
| ------------- |-------------|
|[Overview of Configuration Manager current branch (Übersicht über Configuration Manager Current Branch)](../plan-design/changes/whats-new-incremental-versions.md)|Kurze Zusammenfassung der wichtigsten Punkte zum neuen Servicemodell für Configuration Manager (Current Branch)|
|[Lifecycle-Unterstützung](../servers/manage/current-branch-versions-supported.md)|Erläutert die neue Unterstützung und das Dienstmodell.|
|[Entfernte und veraltete Elemente](../plan-design/changes/deprecated/removed-and-deprecated.md)|Dies dient als frühzeitige Warnung hinsichtlich zukünftiger Änderungen, die sich auf die Verwendung von Configuration Manager auswirken können.|
|[Updates to Configuration Manager current branch (Updates für Configuration Manager Current Branch)](../servers/manage/updates.md)|Erläutert die einfache konsoleninterne Methode zum Anwenden von Featureupdates für Configuration Manager.|
|[Abrufen von verfügbaren Updates](../servers/manage/install-in-console-updates.md#get-available-updates)|Erläutert die beiden verfügbaren Modi zum Abrufen neuer Featureupdates für Configuration Manager.|
|[Updatecheckliste](../servers/manage/install-in-console-updates.md#bkmk_beforeinstall)|Versionsspezifische Updatecheckliste, falls vorhanden.| 
|[Installieren der neuen Featureupdates für Configuration Manager](../servers/manage/install-in-console-updates.md#bkmk_install)|Erläutert die einfachen Schritte zur Installation von Featureupdates.|
|[Unterstützung für Windows 10](../plan-design/configs/support-for-windows-10.md)|Stellt eine Unterstützungsmatrix für Windows 10-Versionen (und ADK-Versionen) zur Verfügung.|
|[Technical Previews für Configuration Manager](../get-started/technical-preview.md)|Stellt Informationen zum Technical Preview-Programm für Configuration Manager zur Verfügung.|


## <a name="key-articles-about-adopting-windows-as-a-service"></a>Wichtige Artikel zur Übernahme von Windows as a Service

| Artikel        | Beschreibung          |
| ------------- |-------------|
|[Verwalten von Windows as a Service](../../osd/deploy-use/manage-windows-as-a-service.md)|Erläuterungen zur Verwendung von Wartungsplänen zum Bereitstellen von Featureupdates für Windows 10.|
|[Upgrade Windows 10 via task sequence (Aktualisieren von Windows 10 über die Tasksequenz)](../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)|Details zum Erstellen einer Tasksequenz, um Windows 10 mit zusätzlichen Empfehlungen zu aktualisieren.|
|[Bereitstellung in Phasen](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)|Bereitstellungen in Phasen automatisieren ein koordiniertes Rollout einer Tasksequenz in einer bestimmten Reihenfolge über mehrere Sammlungen hinweg.|  
|[Optimieren der Bereitstellung von Updates für Windows 10](../../sum/deploy-use/optimize-windows-10-update-delivery.md)|Verwalten Sie Updateinhalte mit Configuration Manager, um stets auf dem neuesten Stand von Windows 10 zu bleiben.|
|[Was ist Desktop Analytics?](../../desktop-analytics/overview.md)|Mit Desktop Analytics können Sie die Bereitschaft von Geräten in Ihrer Umgebung für ein Upgrade auf Windows 10 ermitteln und analysieren.|
|[Windows Update for Business-Integration (optional)](../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md)|Erläuterungen zum Definieren und Bereitstellen von Richtlinien für Windows Update for Business mithilfe von Configuration Manager.|
|[Verwenden der Co-Verwaltung mit Microsoft Intune und Windows Update for Business (optional)](../../comanage/overview.md)|Überblick über die Co-Verwaltung|


## <a name="related-articles"></a>Verwandte Artikel

- [Upgraden auf Current Branch für Configuration Manager](../servers/deploy/install/upgrade-to-configuration-manager.md)
- [Planen der Migration zu Configuration Manager (Current Branch)](../migration/planning-for-migration.md)
