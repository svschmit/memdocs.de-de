---
title: Verwenden von Multicast zum Bereitstellen von Windows über das Netzwerk
titleSuffix: Configuration Manager
description: Verwenden Sie Multicast in Ihrer Configuration Manager-Umgebung, damit mehrere Computer gleichzeitig das Betriebssystemimage herunterladen können.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 4cafb7fc-380b-41b1-b83e-045aebfb7131
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9f580467ccb26209ed20666733e30959bbf50128
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124704"
---
# <a name="use-multicast-to-deploy-windows-over-the-network-with-configuration-manager"></a>Verwenden von Multicast zum Bereitstellen von Windows über das Netzwerk mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Multicast ist eine Netzwerkoptimierungsmethode, die Sie verwenden können, wenn das gleiche Betriebssystemimage wahrscheinlich von mehreren Clients gleichzeitig heruntergeladen wird. Wenn Sie Multicast verwenden, laden mehrere Computer gleichzeitig das Betriebssystemimage herunter, da es vom Verteilungspunkt über Multicast gesendet wird. Dies ist die Alternative dazu, dass jeder Client eine Kopie des Images über eine separate Verbindung vom Verteilungspunkt herunterlädt.

Stellen Sie in den folgenden Szenarien für die Betriebssystembereitstellung die Betriebssysteme mithilfe von Multicast über das Netzwerk bereitstellen:

- [Aktualisieren eines vorhandenen Computers mit einer neuen Version von Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Installieren einer neuen Version von Windows auf einem neuen Computer (Bare-Metal)](install-new-windows-version-new-computer-bare-metal.md)

Führen Sie die Schritte in einem dieser Szenarien für die Betriebssystembereitstellung aus. Gehen Sie dann nach den folgenden Abschnitten vor, um Multicast zu unterstützen.

## <a name="configure-distribution-points-for-multicast"></a><a name="BKMK_Configure"></a> Konfigurieren von Verteilungspunkten für Multicast

Um Multicast zu verwenden, müssen Sie mindestens einen Verteilungspunkt für die Multicastunterstützung konfigurieren. Weitere Informationen finden Sie unter [Installieren und Konfigurieren von Verteilungspunkten](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast).

Eine Liste der Ports, die für die Multicastunterstützung erforderlich sind, finden Sie unter [Ports](../../core/plan-design/hierarchy/ports.md#BKMK_PortsClient-DP2).

## <a name="prepare-an-os-image-for-multicast"></a>Vorbereiten eines Betriebssystemimages für Multicast

Sie müssen das Betriebssystemimage zur Unterstützung von Multicast konfigurieren. Weitere Informationen finden Sie unter [Vorbereiten des Betriebssystemimages für Multicastbereitstellungen](../get-started/manage-operating-system-images.md#BKMK_OSImageMulticast).

## <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> Bereitstellen der Tasksequenz

Stellen Sie das Betriebssystem in einer Zielauflistung bereit. Weitere Informationen finden Sie unter [Deploy a task sequence](deploy-a-task-sequence.md).

## <a name="next-steps"></a>Nächste Schritte

[Benutzererfahrungen bei der Betriebssystembereitstellung](../understand/user-experience.md)
