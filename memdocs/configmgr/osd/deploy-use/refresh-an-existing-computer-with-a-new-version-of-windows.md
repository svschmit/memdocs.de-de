---
title: Aktualisieren des Betriebssystems eines vorhandenen Computers
titleSuffix: Configuration Manager
description: Es gibt verschiedene Möglichkeiten in Configuration Manager, um einen vorhandenen Computer zu partitionieren und zu formatieren und ein neues Betriebssystems auf dem Computer zu installieren.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b189a346-8c0d-4870-a876-0719fbb0ab04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9582d6840e1f750d53504da4e8e7f6bf54f44965
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708408"
---
# <a name="refresh-an-existing-computer-with-a-new-version-of-windows"></a>Aktualisieren eines vorhandenen Computers mit einer neuen Version von Windows

*Gilt für: Configuration Manager (Current Branch)*

Verwenden Sie Configuration Manager, um einen vorhandenen Computer zu partitionieren und zu formatieren und dann ein neues Betriebssystem zu installieren. Dieser Prozess wird manchmal auch als *Reimaging* oder *Zurücksetzen und Laden* bezeichnet. In diesem Szenario können Sie aus mehreren unterschiedlichen Bereitstellungsmethoden auswählen, z. B. PXE, startbare Medien oder Softwarecenter. Sie können auch einen Zustandsmigrationspunkt verwenden, um Einstellungen zu speichern und sie dann auf dem neuen Betriebssystem wiederherzustellen.

Informationen zur Auswahl des richtigen Betriebssystembereitstellungsszenarios finden Sie unter [Szenarien zur Bereitstellung von Unternehmensbetriebssystemen](scenarios-to-deploy-enterprise-operating-systems.md).  

## <a name="plan"></a><a name="BKMK_Plan"></a> Plan  

### <a name="plan-for-and-implement-infrastructure-requirements"></a>Planen und Implementieren von Infrastrukturanforderungen

Es gibt verschiedene Infrastrukturanforderungen, die erfüllt sein müssen, bevor Sie ein Betriebssystem bereitstellen können. Einige dieser Anforderungen umfassen das Windows ADK, das Migrationsprogramm für den Benutzerzustand (USMT) und die Windows-Bereitstellungsdienste (WDS). Weitere Informationen finden Sie unter [Anforderungen an die Infrastruktur für die Betriebssystembereitstellung](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

### <a name="install-a-state-migration-point"></a>Installieren eines Zustandsmigrationspunkts

Wenn Sie Einstellungen von einem vorhandenen Computer erfassen und dann die Einstellungen auf dem neuen Betriebssystem wiederherstellen möchten, ziehen Sie die Verwendung eines Zustandsmigrationspunkts in Betracht. Weitere Informationen finden Sie unter [Statusmigrationspunkt](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

## <a name="configure"></a><a name="BKMK_Configure"></a> Konfigurieren  

### <a name="prepare-a-boot-image"></a>Vorbereiten eines Startabbilds

Startimages starten einen Computer in einer Windows PE-Umgebung. Windows PE ist ein minimales Betriebssystem mit eingeschränkten Komponenten und Diensten. Von Windows PE aus kann Configuration Manager dann ein vollständiges Windows-Betriebssystem auf dem Computer installieren.

Weitere Informationen finden Sie in den folgenden Artikeln:

- [Verwalten von Startimages](../get-started/manage-boot-images.md)

- [Anpassen von Startimages](../get-started/customize-boot-images.md)

- [Verteilen von Inhalt](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)

### <a name="prepare-an-os-image"></a>Vorbereiten eines Betriebssystemimages

Das Betriebssystemimage enthält die erforderlichen Dateien zum Installieren des Betriebssystems auf dem Zielcomputer.

Weitere Informationen finden Sie in den folgenden Artikeln:

- [Verwalten von Betriebssystemimages](../get-started/manage-operating-system-images.md)

- [Verteilen von Inhalt](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Erstellen einer Tasksequenz zum Bereitstellen eines Betriebssystems

Verwenden Sie eine Tasksequenz, um die Installation des Betriebssystems zu automatisieren. Abhängig von der gewählten Bereitstellungsmethode sind möglicherweise zusätzliche Aspekte zur Tasksequenz zu berücksichtigen.

Weitere Informationen finden Sie in den folgenden Artikeln:

- [Erstellen einer Tasksequenz zum Installieren eines Betriebssystems](create-a-task-sequence-to-install-an-operating-system.md)

- [Verwalten des Benutzerzustands](../get-started/manage-user-state.md)

## <a name="deploy"></a><a name="BKMK_Deploy"></a> Bereitstellen

- Verwenden Sie eine der folgenden Methoden, um das Betriebssystem bereitzustellen:  

  - [Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk](use-pxe-to-deploy-windows-over-the-network.md)  

  - [Verwenden von Multicast zum Bereitstellen von Windows über das Netzwerk](use-multicast-to-deploy-windows-over-the-network.md)  

  - [Erstellen eines Images für ein OEM-Vorinstallations- oder lokales Depot](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

  - [Use stand-alone media to deploy Windows without using the network (Verwenden eigenständiger Medien zum Bereitstellen von Windows ohne Verwendung des Netzwerks)](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

  - [Verwenden startbarer Medien zum Bereitstellen von Windows über das Netzwerk](use-bootable-media-to-deploy-windows-over-the-network.md)  

  - [Verwenden des Softwarecenters zum Bereitstellen von Windows über das Netzwerk](use-software-center-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>Überwachen  

Weitere Informationen finden Sie unter [Überwachen von Betriebssystembereitstellungen in System Center Configuration Manager](monitor-operating-system-deployments.md).  

> [!Note]
> Wenn Sie ein neues Image für ein UEFI-Gerät erstellen, erstellt der Windows-Start-Manager einen neuen Eintrag im Startladeprogramm. Dieses Verhalten macht sich vor allem dann bemerkbar, wenn Sie wiederholt ein neues Image für ein Gerät erstellen, z. B. in einer Testumgebung oder in einer Kursteilnehmerübung. Im Allgemeinen hat dies keinen Einfluss auf die Leistung oder Nutzung des Geräts. Wenn die Liste zu groß wird, kann es bei einigen bestimmten Hardwaregeräten zu Funktionsproblemen kommen. Beispielsweise wird nicht von einem externen USB-Laufwerk gestartet, oder der aktuelle Starteintrag kann nicht aus der Liste ausgewählt werden. Verwenden Sie den Windows-Befehl **bcdedit**, um unbenutzte Starteinträge zu löschen. Weitere Informationen finden Sie unter [BCDEdit /deletevalue](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--deletevalue).<!-- 2841926 -->
