---
title: Ersetzen eines vorhandenen Computers und Übertragen von Einstellungen
titleSuffix: Configuration Manager
description: Wählen Sie in Configuration Manager eine Bereitstellungsmethode wie startbare Medien, Multicast oder Softwarecenter aus, um einen vorhandenen Computer durch einen neuen Computer zu ersetzen.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: d28f4363-9e8a-4c54-9cb7-0594fabfff26
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8b494fd5d9623af9de16d68e3d30e0e78a4ef338
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708398"
---
# <a name="replace-an-existing-computer-and-transfer-settings-with-configuration-manager"></a>Ersetzen eines vorhandenen Computers und Übertragen von Einstellungen mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Dieses Thema enthält die allgemeinen Schritte, mit denen Sie in Configuration Manager einen vorhandenen Computer durch einen neuen Computer ersetzen können. In diesem Szenario können Sie aus vielen unterschiedlichen Bereitstellungsmethoden auswählen, z. B. startbare Medien, Multicast oder Softwarecenter. Sie können auch einen Zustandsmigrationspunkt installieren, um Einstellungen zu speichern, und diese Einstellungen dann nach der Installation im neuen Betriebssystem wiederherstellen. Wenn Sie nicht sicher sind, ob dies das richtige Szenario der Betriebssystembereitstellung für Sie ist, ziehen Sie [Scenarios to deploy enterprise operating systems with System Center Configuration Manager (Szenarios für die Bereitstellung von Unternehmensbetriebssystemen)](scenarios-to-deploy-enterprise-operating-systems.md) zurate.  

 Verwenden Sie die folgenden Abschnitte, um einen vorhandenen Computer mit einer neuen Version von Windows zu aktualisieren.  

##  <a name="plan"></a><a name="BKMK_Plan"></a> Plan  

-   **Planen und Implementieren von Anforderungen an die Infrastruktur**  

     Vor der Bereitstellung von Betriebssystemen müssen verschiedene Anforderungen an die Infrastruktur erfüllt sein, z. B. Windows ADK, User State Migration Tool (USMT), Windows Deployment Services (WDS) unterstützte Festplattenkonfigurationen usw. Weitere Informationen finden Sie unter [Infrastructure requirements for operating system deployment (Anforderungen an die Infrastruktur für die Betriebssystembereitstellung)](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

-   **Installieren eines Zustandsmigrationspunkts (nur erforderlich, wenn Sie Einstellungen übertragen)**  

     Wenn Sie Einstellungen eines vorhandenen Computers erfassen und dann im neuen Betriebssystem wiederherstellen möchten, müssen Sie einen Zustandsmigrationspunkt installieren. Weitere Informationen finden Sie unter [Statusmigrationspunkt](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

##  <a name="configure"></a><a name="BKMK_Configure"></a> Konfigurieren  

1.  **Vorbereiten eines Startabbilds**  

     Ein Startabbild startet einen Computer in einer Windows PE-Umgebung (ein minimales Betriebssystem mit begrenzten Komponenten und Diensten), die dann ein vollständiges Windows-Betriebssystem auf dem Computer installieren kann. Wenn Sie Betriebssysteme bereitstellen, müssen Sie das zu verwendende Startimage auswählen und das Image auf einen Verteilungspunkt verteilen. Bereiten Sie das Startimage unter Berücksichtigung folgender Informationen vor:  

    -   Weitere Informationen zu Startimages finden Sie unter [Manage boot images (Verwalten von Startimages)](../get-started/manage-boot-images.md).  

    -   Weitere Informationen zum Anpassen eines Startimages [Anpassen von Startimages mit System Center Configuration Manager](../get-started/customize-boot-images.md).  

    -   Verteilen Sie das Startabbild an Verteilungspunkte. Weitere Informationen finden Sie unter [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

2.  **Vorbereiten eines Betriebssystemabbilds**  

     Das Betriebssystemimage enthält die erforderlichen Dateien zum Installieren des Betriebssystems auf dem Zielcomputer. Bereiten Sie das Betriebssystemimage unter Berücksichtigung folgender Informationen vor:  

    -   Weitere Informationen zum Erstellen eines Betriebssystemimages finden Sie unter [Manage operating system images (Verwalten von Betriebssystemimages)](../get-started/manage-operating-system-images.md).  

    -   Verteilen Sie die Betriebssystemimages an Verteilungspunkte. Weitere Informationen finden Sie unter [Distribute content (Verteilen von Inhalt)](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

3.  **Erstellen einer Tasksequenz zum Bereitstellen von Betriebssystemen über das Netzwerk**  

     Verwenden Sie eine Tasksequenz, um die Installation des Betriebssystems über das Netzwerk zu automatisieren. Führen Sie die Schritte im Artikel [Erstellen einer Tasksequenz zum Installieren eines Betriebssystems](create-a-task-sequence-to-install-an-operating-system.md) aus, um die Tasksequenz zum Bereitstellen des Betriebssystems zu erstellen. Abhängig von der gewählten Bereitstellungsmethode sind möglicherweise zusätzliche Aspekte zur Tasksequenz zu berücksichtigen.  

    > [!NOTE]  
    >  Wenn Sie in diesem Szenario Benutzereinstellungen und Dateien erfassen und wiederherstellen, können Sie entweder einen Zustandsmigrationspunkt verwenden oder die Dateien lokal speichern. Weitere Informationen finden Sie unter [Verwalten des Benutzerstatus](../get-started/manage-user-state.md).  

##  <a name="deploy"></a><a name="BKMK_Deploy"></a> Bereitstellen  

-   Verwenden Sie eine der folgenden Bereitstellungsmethoden, um das Betriebssystem bereitzustellen:  

    -   [Verwenden des Softwarecenters zum Bereitstellen von Windows über das Netzwerk](use-software-center-to-deploy-windows-over-the-network.md)  

    -   [Verwenden startbarer Medien zum Bereitstellen von Windows über das Netzwerk](use-bootable-media-to-deploy-windows-over-the-network.md)  

    -   [Verwenden von Multicast zum Bereitstellen von Windows über das Netzwerk](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [Erstellen eines Images für ein OEM-Vorinstallations- oder lokales Depot](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

## <a name="monitor"></a>Überwachen  

-   **Überwachen der Tasksequenzbereitstellung**  

     Weitere Informationen zum Überwachen der Tasksequenzbereitstellung zum Installieren des Betriebssystems finden Sie unter [Monitor operating system deployments (Überwachen von Betriebssystembereitstellungen)](monitor-operating-system-deployments.md).  
