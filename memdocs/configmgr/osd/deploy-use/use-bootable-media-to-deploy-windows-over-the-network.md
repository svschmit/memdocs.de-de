---
title: Verwenden startbarer Medien zum Bereitstellen von Windows über das Netzwerk
titleSuffix: Configuration Manager
description: Verwenden Sie Bereitstellungen mit startbaren Medien in Configuration Manager, um ein Betriebssystem beim Starten des Zielcomputers bereitzustellen.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: db28c89e88ba08f92618c6d5fde1d1516b74afe4
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124755"
---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-configuration-manager"></a>Verwenden startbarer Medien zum Bereitstellen von Windows über das Netzwerk mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Startbare Medien enthalten nur das Startimage und einen Zeiger zur Tasksequenz. Betriebssystemimage und weitere referenzierte Inhalte werden aus dem Netzwerk heruntergeladen. Da startbare Medien nur wenig Inhalt aufweisen, können Sie die Tasksequenz und den größten Teil des Inhalts aktualisieren, ohne das Medium austauschen zu müssen.

Stellen Sie in folgenden Szenarien Betriebssysteme mit startbaren Medien über das Netzwerk bereit:

- [Aktualisieren eines vorhandenen Computers mit einer neuen Version von Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Installieren einer neuen Version von Windows auf einem neuen Computer (Bare-Metal)](install-new-windows-version-new-computer-bare-metal.md)

- [Ersetzen eines vorhandenen Computers und Übertragen von Einstellungen](replace-an-existing-computer-and-transfer-settings.md)

Führen Sie die Schritte in einem der Szenarien zur Betriebssystembereitstellung aus, und verwenden Sie dann die folgenden Abschnitte, um startbare Medien zum Bereitstellen des Betriebssystems zu verwenden.

## <a name="configure-deployment-settings"></a>Konfigurieren von Bereitstellungseinstellungen

Wenn Sie startbare Medien verwenden, um den Bereitstellungsprozess für das Betriebssystem zu starten, konfigurieren Sie die Tasksequenzbereitstellung so, dass das Betriebssystem für das Medium zur Verfügung gestellt wird. Legen Sie diese Option auf der Seite **Bereitstellungseinstellungen** der Bereitstellung fest. Wählen Sie für die Einstellung **Verfügbar machen für** eine der folgenden Optionen aus:

- Configuration Manager-Clients, Medien und PXE

- Nur Medien und PXE

- Nur Medien und PXE (ausgeblendet)

Weitere Informationen finden Sie unter [Deploy a task sequence](deploy-a-task-sequence.md).

## <a name="create-the-bootable-media"></a>Erstellen der startbaren Medien

Wenn Sie startbare Medien erstellen, geben Sie an, ob es sich um ein USB-Flashlaufwerk oder einen CD/DVD-Satz handelt. Der Computer, der die Medien startet, muss die Option unterstützen, die Sie als startbares Laufwerk auswählen. Weitere Informationen finden Sie unter [Erstellen startbarer Medien](create-bootable-media.md).

## <a name="install-the-os-from-bootable-media"></a><a name="BKMK_Deploy"></a> Installieren des Betriebssystems über startbare Medien

Um das Betriebssystem zu installieren, legen Sie das startbare Medium ein,und schalten Sie dann den Computer ein.

## <a name="support-for-cloud-based-content"></a>Unterstützung für cloudbasierte Inhalte

<!--6209223-->

Ab Version 2006 können startbare Medien cloudbasierte Inhalte herunterladen. Sie können beispielsweise einen USB-Schlüssel an einen Benutzer in einer Zweigniederlassung senden, damit dieser ein Reimaging seines Geräts durchführen kann. Oder eine Filiale verfügt über einen lokalen PXE-Server, aber Sie möchten, dass Geräte nach Möglichkeit Clouddienste priorisieren. Anstatt das WAN weiterhin mit dem Download umfangreicher Inhalte für die Bereitstellung von Betriebssystemen zu belasten, können Startmedien und PXE-Bereitstellungen jetzt Inhalte aus cloudbasierten Quellen abrufen. Beispielsweise ein Cloudverwaltungsgateway (Cloud Management Gateway, CMG), das Sie zum Freigeben von Inhalten aktivieren.

> [!NOTE]
> Das Gerät benötigt weiterhin eine Intranetverbindung mit dem Verwaltungspunkt.

Wenn die Tasksequenz ausgeführt wird, werden Inhalte aus den cloudbasierten Quellen heruntergeladen. Überprüfen Sie **smsts.log** auf dem Client.

### <a name="prerequisites"></a>Voraussetzungen

- Aktivieren Sie die folgende Clienteinstellung in der Gruppe **Clouddienste**: **Zugriff auf Cloudverteilungspunkt zulassen**. Stellen Sie sicher, dass die Clienteinstellung für die Zielclients bereitgestellt wird. Weitere Informationen finden Sie unter [Informationen zu Clienteinstellungen – Clouddienste](../../core/clients/deploy/about-client-settings.md#cloud-services).

- Führen Sie für die Begrenzungsgruppe, in der sich der Client befindet, Folgendes aus:

  - Ordnen Sie die CMG- oder Cloudverteilungspunkt-Standortsysteme zu, in denen sich Inhalte befinden. Weitere Informationen finden Sie unter [Konfigurieren einer Begrenzungsgruppe](../../core/servers/deploy/configure/boundary-group-procedures.md#bkmk_config).

  - Aktivieren Sie die folgende Option: **Cloudbasierte Quellen lokalen Quellen vorziehen**. Weitere Informationen finden Sie unter [Begrenzungsgruppenoptionen für Peerdownloads](../../core/servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).

- Verteilen Sie den Inhalt, auf den die Tasksequenz verweist, auf das für Inhalte aktivierte CMG oder einen Cloudverteilungspunkt.

## <a name="next-steps"></a>Nächste Schritte

[Benutzererfahrungen bei der Betriebssystembereitstellung](../understand/user-experience.md#task-sequence-wizard)
