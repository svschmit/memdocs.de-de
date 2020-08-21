---
title: Erstellen eines Images für ein OEM-Vorinstallations- oder lokales Depot
titleSuffix: Configuration Manager
description: Verwenden Sie vorab bereitgestellte Medienbereitstellungen zum Reduzieren des Netzwerkverkehrs, während Sie ein Betriebssystem für Computer bereitstellen, die nicht vollständig bereitgestellt sind.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: a7d3df90-062d-4d57-9e9d-e137d3e7cd7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 15145cccf73e517d0e49444fbdaf834de342865e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125439"
---
# <a name="create-an-image-for-an-oem-in-factory-or-a-local-depot-with-configuration-manager"></a>Erstellen eines Images für ein OEM-Vorinstallations- oder lokales Depot mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Bei Bereitstellungen mit vorab bereitgestellten Medien in Configuration Manager können Sie ein Betriebssystem für Computer bereitstellen, die nicht vollständig bereitgestellt sind. Die vorab bereitgestellten Medien sind Windows-Imagedateien (WIM). Der Hersteller (OEM) kann sie auf einem Bare-Metal-Computer installieren, oder Sie können sie in einem Staging Center verwenden, das von Ihrer Produktionsumgebung getrennt ist.

Durch diese Bereitstellungsmethode wird der Netzwerkdatenverkehr reduziert, da das Start- und Betriebssystemimage bereits auf dem Zielcomputer vorhanden sind. Sie können Anwendungen, Pakete und Treiberpakete angeben, um sie auch in die vorab bereitgestellte Medien einzubeziehen. Nach der Installation des Betriebssystems auf dem Computer überprüft die Tasksequenz zuerst den Cache für vorab bereitgestellte Medien auf Anwendungen, Pakete oder Treiberpakete. Wenn der erforderliche Inhalt nicht gefunden werden kann oder eine neuere Revision online verfügbar ist, wird der Inhalt von der Tasksequenz von einem Verteilungspunkt heruntergeladen.

Vorab bereitgestellte Medien können in folgenden Szenarien für die Betriebssystembereitstellung verwendet werden:

- [Installieren einer neuen Version von Windows auf einem neuen Computer (Bare-Metal)](install-new-windows-version-new-computer-bare-metal.md)

- [Ersetzen eines vorhandenen Computers und Übertragen von Einstellungen](replace-an-existing-computer-and-transfer-settings.md)

Führen Sie die Schritte in einem dieser Szenarien für die Betriebssystembereitstellung aus. Bereiten Sie dann anhand der folgenden Abschnitte die vorab bereitgestellten Medien vor und erstellen Sie sie.

## <a name="configure-deployment-settings"></a>Konfigurieren von Bereitstellungseinstellungen

Wählen Sie auf der Seite **Bereitstellungseinstellungen** der Bereitstellung für die Einstellung **Verfügbar machen für** eine der folgenden Optionen aus:

- Configuration Manager-Clients, Medien und PXE

- Nur Medien und PXE

- Nur Medien und PXE (ausgeblendet)

## <a name="create-the-prestaged-media"></a>Erstellen der vorab bereitgestellten Medien

Erstellen der vorab bereitgestellten Mediendatei zum Versand an den OEM oder Ihr lokales Depot. Weitere Informationen finden Sie unter [Erstellen von vorab bereitgestellten Medien](create-prestaged-media.md).

## <a name="send-the-prestaged-media-file"></a>Senden der vorab bereitgestellten Mediendatei

Senden Sie die Medien an den OEM oder Ihr lokales Depot, um sie auf den Computern vorab bereitzustellen. Die Imagedatei wird auf eine formatierte Festplatte des Computers angewendet.

## <a name="deliver-the-computer"></a>Ausliefern des Computers

Wenn Sie den Computer an einen Benutzer ausliefern und ihn zum ersten Mal einschalten:

1. Der Computer beginnt mit dem vorab bereitgestellten Startimage.

1. Er überprüft einen Hash auf den vorab bereitgestellten Medien, um sicherzustellen, dass er gültig ist.

1. Der Computer stellt eine Verbindung mit dem Verwaltungspunkt für verfügbare Tasksequenzen her, um den Vorgang abzuschließen.

## <a name="next-steps"></a>Nächste Schritte

[Benutzererfahrungen bei der Betriebssystembereitstellung](../understand/user-experience.md)
