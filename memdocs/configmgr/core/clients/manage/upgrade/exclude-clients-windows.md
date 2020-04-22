---
title: Ausschließen von Clientupgrades für Windows
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Windows-Clients von der Aktualisierung im Configuration Manager ausschließen.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4cd6031f-8844-4d0b-8166-b24d6528a94e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 58a7741bb628a0c8fb346c8f61b446301b138d80
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696848"
---
# <a name="how-to-exclude-clients-from-upgrade-in-configuration-manager"></a>Vorgehensweise: Ausschließen von Clients von der Aktualisierung im Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Sie können eine Clientsammlung von der automatischen Installation aktualisierter Clientversionen ausschließen. Nutzen Sie diesen Ausschluss für eine Sammlung von Computern, bei denen bei einem Upgrade des Clients größere Sorgfalt notwendig ist. Ein Client, der sich in einer ausgeschlossenen Sammlung befindet, ignoriert Anforderungen zur Installation von aktualisierter Clientsoftware.

Dieser Ausschluss gilt für die folgenden Methoden:

- Automatisches Upgrade
- Auf Softwareupdate basierendes Upgrade
- Anmeldeskripts
- Gruppenrichtlinie

> [!NOTE]
> Obwohl die Benutzeroberfläche angibt, dass Upgrades für Clients nicht mit einer beliebigen Methode durchgeführt werden können, gibt es zwei Methoden, die Sie verwenden können, um diese Einstellungen außer Kraft zu setzen. Setzen Sie diese Konfiguration mit Clientpush- oder manueller Clientinstallation außer Kraft. Weitere Informationen finden Sie unter [Aktualisieren eines ausgeschlossenen Clients](#bkmk_override).

## <a name="configure-exclusion"></a><a name="bkmk_exclude"></a> Konfigurieren des Ausschlusses

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**. Erweitern Sie **Standortkonfiguration**, wählen Sie den Knoten **Standorte** aus, und wählen Sie dann im Menüband **Hierarchieeinstellungen** aus.

2. Wechseln Sie zur Registerkarte **Clientupdate**.

3. Wählen Sie die Option **Angegebene Clients von Upgrade ausschließen**  aus. Wählen Sie dann die **Ausschlusssammlung** aus, die Sie ausschließen möchten. Sie können nur eine einzelne Sammlung für den Ausschluss auswählen.

4. Wählen Sie **OK** aus, um die Konfiguration zu schließen und zu speichern.

![Einstellungen für automatische Ausschlüsse aus Upgrades](media/automatic_upgrade_exclusion.png)

Nachdem Clients in der ausgeschlossenen Sammlung die Richtlinie aktualisiert haben, installieren sie Clientupdates nicht automatisch. Weitere Informationen finden Sie unter [Aktualisieren von Clients für Windows-Computer](upgrade-clients-for-windows-computers.md).

> [!NOTE]
> Ausgeschlossene Clients laden weiterhin Ccmsetup herunter und führen es aus, nehmen allerdings kein Upgrade vor.

Wenn Sie einen Client aus der Ausschlusssammlung entfernen, wird dieser nicht automatisch bis zum nächsten automatischen Upgradezyklus aktualisiert.

## <a name="how-to-upgrade-an-excluded-client"></a><a name="bkmk_override"></a> Aktualisieren eines ausgeschlossenen Clients

Wenn ein Gerät Mitglied einer Sammlung ist, die Sie vom Upgrade ausgeschlossen haben, können Sie den Client trotzdem mithilfe einer der folgenden Methoden aktualisieren:

- **Clientpushinstallation**: Ccmsetup ermöglicht die Clientpushinstallation, da sie Ihrer direkten Absicht entspricht. Mit dieser Methode können Sie einen Client aktualisieren, ohne ihn aus der Sammlung zu entfernen oder die gesamte Sammlung aus dem Ausschluss zu entfernen.

- **Manuelle Clientinstallation**: Manuelles Upgrade eines ausgeschlossenen Clients mithilfe des folgenden Ccmsetup-Befehlszeilen Parameters: **:/IgnoreSkipUpgrade**

    Wenn Sie versuchen, einen Client manuell upzugraden, der Mitglied der ausgeschlossenen Sammlung ist, und diesen Parameter nicht verwenden, wird der Client nicht aktualisiert. Weitere Informationen finden Sie im Abschnitt [Manuelle Installation](../../deploy/deploy-clients-to-windows-computers.md#BKMK_Manual).

## <a name="see-also"></a>Weitere Informationen:

- [Aktualisieren von Clients](upgrade-clients.md)

- [Bereitstellen von Clients auf Windows-Computern](../../deploy/deploy-clients-to-windows-computers.md)

- [Client für erweiterte Interoperabilität](../../../understand/interoperability-client.md)
