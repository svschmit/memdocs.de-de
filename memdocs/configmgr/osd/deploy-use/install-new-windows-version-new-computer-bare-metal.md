---
title: Installieren von Windows auf einem neuen Computer
titleSuffix: Configuration Manager
description: Verwenden Sie Configuration Manager, um mithilfe von PXE, OEM oder einem eigenständigen Medium ein Betriebssystem auf einem neuen Computer (Bare-Metal-Computer) zu installieren.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: f5ad22d5-7df1-49c6-8a0f-db1c3f0cda19
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6a70269839b4a550fbef4dc5cab1b7ff3d426d87
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690668"
---
# <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal-with-configuration-manager"></a>Installieren einer neuen Version von Windows auf einem neuen Computer (Bare-Metal) mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Dieses Thema enthält die allgemeinen Schritte für Configuration Manager, um ein Betriebssystem auf einem neuen Computer zu installieren. In diesem Szenario können Sie aus vielen unterschiedlichen Bereitstellungsmethoden auswählen, z. B. PXE, OEM oder eigenständige Medien. Wenn Sie nicht sicher sind, ob dies das richtige Szenario der Betriebssystembereitstellung für Sie ist, ziehen Sie [Szenarien für die Bereitstellung von Unternehmensbetriebssystemen](scenarios-to-deploy-enterprise-operating-systems.md) zurate.  

Verwenden Sie die folgenden Abschnitte, um einen vorhandenen Computer mit einer neuen Version von Windows zu aktualisieren.  

##  <a name="plan"></a><a name="BKMK_Plan"></a> Plan  

-   **Planen und Implementieren von Anforderungen an die Infrastruktur**  

     Vor der Bereitstellung von Betriebssystemen müssen verschiedene Anforderungen an die Infrastruktur erfüllt sein, z. B. Windows ADK, Windows Deployment Services (WDS), unterstützte Festplattenkonfigurationen usw. Weitere Informationen finden Sie unter [Infrastructure requirements for operating system deployment (Anforderungen an die Infrastruktur für die Betriebssystembereitstellung)](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).

##  <a name="configure"></a><a name="BKMK_Configure"></a> Konfigurieren  

1.  **Vorbereiten eines Startabbilds**  

     Ein Startabbild startet einen Computer in einer Windows PE-Umgebung (ein minimales Betriebssystem mit begrenzten Komponenten und Diensten), die dann ein vollständiges Windows-Betriebssystem auf dem Computer installieren kann.   Wenn Sie Betriebssysteme bereitstellen, müssen Sie das zu verwendende Startimage auswählen und das Image auf einen Verteilungspunkt verteilen. Bereiten Sie das Startimage unter Berücksichtigung folgender Informationen vor:  

    -   Weitere Informationen zu Startimages finden Sie unter [Manage boot images (Verwalten von Startimages)](../get-started/manage-boot-images.md).  

    -   Weitere Informationen zum Anpassen eines Startimages [Anpassen von Startimages mit System Center Configuration Manager](../get-started/customize-boot-images.md).  

    -   Verteilen Sie das Startabbild an Verteilungspunkte. Weitere Informationen finden Sie unter [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

2.  **Vorbereiten eines Betriebssystemabbilds**  

     Das Betriebssystemimage enthält die erforderlichen Dateien zum Installieren des Betriebssystems auf dem Zielcomputer. Bereiten Sie das Betriebssystemimage unter Berücksichtigung folgender Informationen vor:  

    -   Weitere Informationen zum Erstellen eines Betriebssystemimages finden Sie unter [Manage operating system images (Verwalten von Betriebssystemimages)](../get-started/manage-operating-system-images.md).

    -   Verteilen Sie die Betriebssystemimages an Verteilungspunkte. Weitere Informationen finden Sie unter [Distribute content (Verteilen von Inhalt)](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

    > [!NOTE]
    > Neuinstallationen von Windows können auch über Betriebssystemupgradepakete mit den Installationsquelldateien ausgeführt werden, doch sollten Sie stattdessen Betriebsystemabbilder (z. B. **install.wim**) verwenden.
    >
    > Das Bereitstellen von Windows-Neuinstallationen über Betriebssystemupgradepakete wird zwar weiterhin unterstützt, hängt aber davon ab, ob die Treiber mit dieser Methode kompatibel sind. Bei Neuinstallationen von Windows aus einem Betriebssystemupgradepaket werden die Treiber installiert und nicht einfach eingefügt, während noch die Windows-Vorinstallationsumgebung (Windows PE) ausgeführt wird. Einige Treiber sind jedoch nicht kompatibel mit der Installation in Windows PE. Wenn Treiber mit der Installation in Windows PE nicht kompatibel sind, verwenden Sie stattdessen ein Betriebssystemabbild.  

3.  **Erstellen einer Tasksequenz zum Bereitstellen von Betriebssystemen über das Netzwerk**  

     Verwenden Sie eine Tasksequenz, um die Installation des Betriebssystems über das Netzwerk zu automatisieren. Führen Sie die Schritte im Artikel [Erstellen einer Tasksequenz zum Installieren eines Betriebssystems](create-a-task-sequence-to-install-an-operating-system.md) aus, um die Tasksequenz zum Bereitstellen des Betriebssystems zu erstellen. Abhängig von der gewählten Bereitstellungsmethode sind möglicherweise zusätzliche Aspekte zur Tasksequenz zu berücksichtigen.  

##  <a name="deploy"></a><a name="BKMK_Deploy"></a> Bereitstellen  

-   Verwenden Sie eine der folgenden Bereitstellungsmethoden, um das Betriebssystem bereitzustellen:  

    -   [Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk](use-pxe-to-deploy-windows-over-the-network.md)  

    -   [Verwenden von Multicast zum Bereitstellen von Windows über das Netzwerk](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [Erstellen eines Images für ein OEM-Vorinstallations- oder lokales Depot](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

    -   [Use stand-alone media to deploy Windows without using the network (Verwenden eigenständiger Medien zum Bereitstellen von Windows ohne Verwendung des Netzwerks)](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

    -   [Verwenden startbarer Medien zum Bereitstellen von Windows über das Netzwerk](use-bootable-media-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>Überwachen  

-   **Überwachen der Tasksequenzbereitstellung**  

     Weitere Informationen zum Überwachen der Tasksequenzbereitstellung zum Installieren des Betriebssystems finden Sie unter [Überwachen von Betriebssystembereitstellungen](monitor-operating-system-deployments.md).  
