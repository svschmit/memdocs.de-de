---
title: Verwalten risikoreicher Bereitstellungen
titleSuffix: Configuration Manager
description: Konfigurieren Sie Standorteinstellungen zur Bereitstellungsüberprüfung in Configuration Manager, um Administratoren zu warnen, wenn diese eine risikoreiche Bereitstellung erstellen.
ms.date: 02/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8d37b983-a964-402c-819d-2512ed2d463b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3f1498c383f9b02f7f322de3ba5708351e84c3b7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703298"
---
# <a name="settings-to-manage-high-risk-deployments-for-configuration-manager"></a>Einstellungen zum Verwalten risikoreicher Bereitstellungen für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Mit Configuration Manager können Sie Standorteinstellungen zur *Bereitstellungsüberprüfung* konfigurieren. Durch diese Einstellungen werden Administratoren gewarnt, wenn diese die Bereitstellung einer risikoreichen Tasksequenz erstellen. Eine risikoreiche Bereitstellung ist z. B.:  

- Eine Bereitstellung, die automatisch installiert wird  

- Eine Bereitstellung mit potenziell unerwünschten Ergebnissen  

Beispiel: Eine Tasksequenz, die als Zweck **Erforderlich** aufweist und ein Betriebssystem bereitstellt, wird als hohes Risiko betrachtet.  

> [!WARNING]
> Wenn Sie PXE-Bereitstellungen verwenden und Gerätehardware mit dem Netzwerkadapter als erstes Startgerät konfigurieren, können diese Geräte automatisch und ohne Benutzerinteraktion eine Tasksequenz für die Betriebssystembereitstellung starten. Diese Konfiguration wird nicht durch die Bereitstellungsüberprüfung verwaltet. Während diese Konfiguration möglicherweise den Prozess vereinfachen und die Benutzerinteraktion reduzieren kann, erhöht sie das Risiko, dass für das Gerät versehentlich ein Reimaging durchgeführt wird.

## <a name="deployment-verification-settings"></a><a name="bkmk_settings"></a> Einstellungen für die Bereitstellungsüberprüfung

Um das Risiko einer unbeabsichtigten Bereitstellung mit hohem Risiko zu reduzieren, können Sie Größenbeschränkungen in Einstellungen zur Bereitstellungsüberprüfung konfigurieren:  

- **Grenzwerte für Sammlungsgröße**: Mit dieser Einstellung werden beim Erstellen einer Bereitstellung die Sammlungen ausgeblendet, die mehr Clients als Ihr Grenzwert enthalten.  

  - **Standardgröße**: Mit dieser Einstellung werden beim Erstellen einer Bereitstellung standardmäßig die Sammlungen ausgeblendet, die mehr Clients als der Grenzwert enthalten. Sie können diese Sammlungen zwar weiterhin beim Erstellen der Bereitstellung anzeigen, standardmäßig sind sie jedoch ausgeblendet. Der Standardwert lautet **100**. Geben Sie den Wert **0** ein, um diese Einstellung zu ignorieren.  

  - **Maximale Größe**: Mit dieser Einstellung werden beim Erstellen einer Bereitstellung immer die Sammlungen ausgeblendet, die mehr Clients als diesen Grenzwert enthalten. Der Standardwert lautet **0**, wodurch diese Einstellung ignoriert wird. Der Wert **Maximale Größe** muss größer sein als der Wert **Standardgröße** .  

    Beispiel: Sie legen **Standardgröße** auf 100 und **Maximale Größe** auf 1000 fest. Wenn Sie eine Bereitstellung mit hohem Risiko erstellen, werden im Fenster **Sammlung auswählen** nur die Sammlungen angezeigt, die weniger als 100 Clients enthalten. Wenn Sie die Einstellung **Sammlungen mit einer Anzahl der Mitglieder, die größer als die minimale Größenkonfiguration des Standorts ist, ausblenden** deaktivieren, werden im Fenster Sammlungen angezeigt, die weniger als 1000 Clients enthalten.  

- **Sammlungen mit Standortsystemservern**: Wenn die Zielsammlung einen Computer mit einer Standortsystemrolle enthält, werden hiermit Bereitstellungen blockiert, oder es wird eine Überprüfung vor dem Erstellen der Bereitstellung angefordert. Wenn eine Bereitstellung blockiert wird, müssen Sie eine andere Sammlung auswählen, die den Kriterien der Bereitstellungsüberprüfung entspricht.  

> [!NOTE]
> Bereitstellungen mit hohem Risiko sind immer auf benutzerdefinierte Sammlungen, von Ihnen erstellte Sammlungen und die integrierte Sammlung **Unbekannte Computer** beschränkt. Beim Erstellen einer Bereitstellung mit hohem Risiko können Sie keine integrierte Sammlung auswählen, wie z.B. **Alle Systeme**.  

## <a name="configure-deployment-verification"></a>Konfigurieren der Bereitstellungsüberprüfung

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, wählen Sie **Standorte** und anschließend den primären Standort aus, der konfiguriert werden soll.

2. Klicken Sie im Menüband auf **Eigenschaften**, und wechseln Sie anschließend zur Registerkarte **Bereitstellungsüberprüfung**.

3. Konfigurieren Sie die [Einstellungen](#bkmk_settings), die Sie verwenden möchten, und klicken Sie auf **OK**, um die Konfiguration zu speichern und die Eigenschaften zu schließen.

## <a name="next-steps"></a>Nächste Schritte

[Abschnitt „Einstellungen mit hoher Auswirkung“ in „Verwalten von Tasksequenzen zum Automatisieren von Tasks“](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#high-impact-settings)

[Konfigurieren von Standorten und Hierarchien](../deploy/configure/configure-sites-and-hierarchies.md)
