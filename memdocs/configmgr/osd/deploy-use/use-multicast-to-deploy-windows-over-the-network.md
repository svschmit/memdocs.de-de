---
title: Verwenden von Multicast zum Bereitstellen von Windows über das Netzwerk
titleSuffix: Configuration Manager
description: Verwenden Sie Multicast in Ihrer Configuration Manager-Umgebung, damit mehrere Computer gleichzeitig das Betriebssystemimage herunterladen können.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 4cafb7fc-380b-41b1-b83e-045aebfb7131
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f81b23d3783d397d83a3925b98c0c8f601fa4012
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703488"
---
# <a name="use-multicast-to-deploy-windows-over-the-network-with-configuration-manager"></a>Verwenden von Multicast zum Bereitstellen von Windows über das Netzwerk mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Multicast ist eine Netzwerkoptimierungsmethode, die Sie in Ihrer Configuration Manager-Umgebung verwenden können, wenn voraussichtlich mehrere Clients das gleiche Betriebssystemimage gleichzeitig herunterladen. In diesem Fall wird das Betriebssystemabbild vom Verteilungspunkt mithilfe von Multicast übertragen und kann von mehreren Computern gleichzeitig heruntergeladen werden, anstatt dass vom Verteilungspunkt über jeweils eine separate Verbindung Kopien der Daten an jeden Client gesendet werden.  

 Sie können in den folgenden Betriebssystembereitstellungsszenarien die Betriebssysteme mithilfe von Multicasting über das Netzwerk bereitstellen:  

- [Aktualisieren eines vorhandenen Computers mit einer neuen Version von Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [Installieren einer neuen Version von Windows auf einem neuen Computer (Bare-Metal)](install-new-windows-version-new-computer-bare-metal.md)  

  Führen Sie die Schritte in einem der Szenarien für die Betriebssystembereitstellung aus, und verwenden Sie dann die folgenden Abschnitte, um Multicast zu unterstützen.  

##  <a name="configure-a-distribution-point-to-support-multicast"></a><a name="BKMK_Configure"></a> Konfigurieren eines Verteilungspunkts zur Unterstützung von Multicast  
 Zum Verwenden von Multicast zum Bereitstellen von Betriebssystemen müssen Sie einen Verteilungspunkt konfigurieren. Weitere Informationen finden Sie unter [Installieren und Konfigurieren von Verteilungspunkten](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast). Eine Liste der Ports, die für die Multicastunterstützung erforderlich sind, finden Sie unter [Ports](../../core/plan-design/hierarchy/ports.md#BKMK_PortsClient-DP2).  

## <a name="prepare-an-operating-system-image-for-multicast-deployments"></a>Vorbereiten eines Betriebssystemabbilds für Multicastbereitstellungen  
 Informationen zum Konfigurieren des Pakets mit dem Betriebssystemimage zur Unterstützung von Multicast finden Sie unter [Vorbereiten des Betriebssystemimages für Multicastbereitstellungen](../get-started/manage-operating-system-images.md#BKMK_OSImageMulticast).  

##  <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> Bereitstellen der Tasksequenz  
 Stellen Sie das Betriebssystem für eine Zielsammlung bereit. Weitere Informationen finden Sie unter [Deploy a task sequence](deploy-a-task-sequence.md).  
