---
title: Verwenden des Softwarecenters zum Bereitstellen von Windows über das Netzwerk
titleSuffix: Configuration Manager
description: Stellen Sie ein Betriebssystem über das Softwarecenter bereit, um einen vorhandenen Computer mit einer neuen Version von Windows zu aktualisieren oder ein Upgrade von Windows auf die neueste Version durchzuführen.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6bd10240ebc7ec478efe122bf7f8a45d3afe9f10
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124600"
---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-configuration-manager"></a>Verwenden des Softwarecenters zum Bereitstellen von Windows über das Netzwerk mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Sie können eine Tasksequenz erstellen, die ein im Softwarecenter verfügbares Betriebssystem installiert. Ein Benutzer kann im Softwarecenter eine Tasksequenz für die folgenden Szenarien der Bereitstellung eines Betriebssystems ausführen:

- [Aktualisieren eines vorhandenen Computers mit einer neuen Version von Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Upgrade von Windows auf die neueste Version](upgrade-windows-to-the-latest-version.md)

- [Erstellen einer Tasksequenz für Nicht-Betriebssystembereitstellungen](create-a-task-sequence-for-non-operating-system-deployments.md)

Führen Sie die Schritte in einem dieser Szenarien für die Betriebssystembereitstellung aus. Befolgen Sie dann die Anweisungen in den folgenden Abschnitten, um die Bereitstellungen vorzubereiten, die im Softwarecenter verfügbar sind.

## <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> Bereitstellen der Tasksequenz

Stellen Sie die Tasksequenz für eine Zielsammlung bereit. Weitere Informationen finden Sie unter [Deploy a task sequence](deploy-a-task-sequence.md).

Wählen Sie auf der Seite **Bereitstellungseinstellungen** der Bereitstellung für die Einstellung **Verfügbar machen für** eine der folgenden Optionen aus:

- Nur Configuration Manager-Clients

- Configuration Manager-Clients, Medien und PXE

Konfigurieren Sie auch, ob die Bereitstellung erforderlich oder verfügbar ist:

- Erforderliche Bereitstellung: Für erforderliche Bereitstellungen ist die Tasksequenz im Softwarecenter verfügbar. Die Bereitstellung startet automatisch zum konfigurierten Termin.

- Verfügbare Bereitstellung: Die Tasksequenz ist im Softwarecenter verfügbar, und Benutzer können sie bei Bedarf installieren.

Nachdem Sie die Bereitstellung erstellt haben, zeigen Clients in der Zielsammlung die Tasksequenz im Softwarecenter an.

## <a name="next-steps"></a>Nächste Schritte

[Benutzererfahrungen bei der Betriebssystembereitstellung](../understand/user-experience.md#software-center)
