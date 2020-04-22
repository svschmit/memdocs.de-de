---
title: Verwenden startbarer Medien zum Bereitstellen von Windows über das Netzwerk
titleSuffix: Configuration Manager
description: Verwenden Sie Bereitstellungen mit startbaren Medien in Configuration Manager zum Bereitstellen des Betriebssystems beim Starten des Zielcomputers.
ms.date: 06/16/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 22a3219cdf0bb09061e57f34e52ca7a061f55a2f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709238"
---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-configuration-manager"></a>Verwenden startbarer Medien zum Bereitstellen von Windows über das Netzwerk mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Sie können das Betriebssystem bereitstellen, wenn der Zielcomputer mithilfe einer Bereitstellung mit startbaren Medien gestartet wird. Die Medien enthalten einen Zeiger auf die Tasksequenz, das Betriebssystemabbild und andere erforderliche Inhalte aus dem Netzwerk. Beim Starten des Zielcomputers ruft der Computer die Elemente ab, auf die im Zeiger verwiesen wird. Wenn die startbaren Medien ohne Inhalt sind, können Sie das Ziel aktualisieren, ohne es auf den Medien ersetzen zu müssen.

Sie können in den folgenden Szenarien für die Betriebssystembereitstellung die Betriebssysteme mithilfe von Multicast über das Netzwerk bereitstellen:

-   [Aktualisieren eines vorhandenen Computers mit einer neuen Version von Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [Installieren einer neuen Version von Windows auf einem neuen Computer (Bare-Metal)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Ersetzen eines vorhandenen Computers und Übertragen von Einstellungen](replace-an-existing-computer-and-transfer-settings.md)  

Führen Sie die Schritte in einem der Betriebssystembereitstellungsszenarien aus, und verwenden Sie dann die folgenden Abschnitte, um startbare Medien zum Bereitstellen des Betriebssystems zu verwenden.  

## <a name="configure-deployment-settings"></a>Konfigurieren von Bereitstellungseinstellungen  
Wenn Sie startbare Medien verwenden, um den Bereitstellungsprozess für das Betriebssystem zu starten, konfigurieren Sie die Bereitstellung so, dass das Betriebssystem für die Medien zur Verfügung gestellt wird. Sie können diese Option auf der Seite **Bereitstellungseinstellungen** im Assistenten zum Bereitstellen von Software oder auf der Registerkarte **Bereitstellungseinstellungen** in den Eigenschaften der Bereitstellung konfigurieren. Konfigurieren Sie eine der folgenden Optionen für die Einstellung **Verfügbar machen für** :

-   Configuration Manager-Clients, Medien und PXE

-   Nur Medien und PXE

-   Nur Medien und PXE (ausgeblendet)

## <a name="create-the-bootable-media"></a>Erstellen der startbaren Medien
Sie können angeben, ob das startbare Medium ein USB-Flashlaufwerk oder ein CD/DVD-Satz ist. Der Computer, der die Medien startet, muss die Option unterstützen, die Sie als startbares Laufwerk auswählen. Weitere Informationen finden Sie unter [Erstellen startbarer Medien](create-bootable-media.md).  

##  <a name="install-the-operating-system-from--bootable-media"></a><a name="BKMK_Deploy"></a> Installieren des Betriebssystems von startbaren Medien  
Legen Sie die startbaren Medien in ein startfähiges Laufwerk des Computer ein. Schalten Sie dann den Computer ein, um das Betriebssystem zu installieren.
