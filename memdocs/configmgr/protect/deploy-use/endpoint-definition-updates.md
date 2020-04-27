---
title: Konfigurieren von Definitionsupdates
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Methoden mit Endpoint Protection in Configuration Manager auswählen und konfigurieren, um Antischadsoftwaredefinitionen auf den Clientcomputern auf dem neuesten Stand zu halten.
ms.date: 11/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 537dd2a7-4e44-4877-b8dd-5e1499407f8d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ce11ba0cbe4298d32a11de409910ebc3e14c097b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697348"
---
# <a name="configure-definition-updates-for-endpoint-protection"></a>Konfigurieren von Definitionsupdates für Endpoint Protection  

*Gilt für: Configuration Manager (Current Branch)*

 Mit Endpoint Protection in Configuration Manager können Sie anhand einer Reihe verfügbarer Methoden die Antischadsoftwaredefinitionen auf Clientcomputern in Ihrer Hierarchie auf dem neuesten Stand halten. Die Informationen in diesem Thema helfen Ihnen beim Auswählen und Konfigurieren dieser Methoden.

 Zum Aktualisieren von Antischadsoftwaredefinitionen können Sie eine oder mehrere der folgenden Methoden verwenden:

- [Von Configuration Manager verteilte Updates](endpoint-definitions-configmgr.md) ‒ Diese Methode verwendet Configuration Manager-Softwareupdates, um Definitions- und Engine-Updates auf Computern in Ihrer Hierarchie bereitzustellen.

- [Von WSUS (Windows Server Update Services) verteilte Updates](endpoint-definitions-wsus.md) ‒ Diese Methode verwendet Ihre WSUS-Infrastruktur, um Definitions- und Engine-Updates auf Computern bereitzustellen.

- [Von Microsoft Update verteilte Updates](endpoint-definitions-microsoft-updates.md) ‒ Bei dieser Methode können Computer eine direkte Verbindung mit Microsoft Update herstellen, um die Definitions- und Engine-Updates herunterzuladen. Diese Methode kann bei Computern nützlich sein, die nicht oft mit dem Firmennetzwerk verbunden sind.

- [Von Microsoft Malware Protection Center verteilte Updates](endpoint-definitions-protection-center.md) ‒ bei dieser Methode werden Definitionsupdates vom Microsoft Malware Protection Center heruntergeladen.

- [Updates von UNC-Dateifreigaben](endpoint-definitions-network.md) ‒ Mit dieser Methode können Sie die neuesten Definitions- und Engine-Updates in einer Freigabe auf dem Netzwerk speichern. Clients können dann zum Installieren der Updates auf das Netzwerk zugreifen.

  Sie können mehrere Definitionsupdatequellen konfigurieren und die Reihenfolge steuern, in der diese bewertet und angewendet werden. Dies erfolgt über das Dialogfeld **Definitionsupdatequellen konfigurieren** beim Erstellen einer Richtlinie für Antischadsoftware.

> [!IMPORTANT]
>  Auf Windows 10-PCs müssen Sie Endpoint Protection konfigurieren, um Antischadsoftwaredefinitionen für Windows Defender zu aktualisieren.

## <a name="how-to-configure-definition-update-sources"></a>Konfigurieren von Definitionsupdatequellen
 Verwenden Sie das folgende Verfahren, um die Definitionsupdatequellen zu konfigurieren, die für die einzelnen Richtlinien für Antischadsoftware verwendet werden sollen.

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.

2.  Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** den Knoten **Endpoint Protection**, und klicken Sie dann auf **Richtlinien für Antischadsoftware**.

3.  Öffnen Sie die Eigenschaftenseite für die **Standardrichtlinie für Antischadsoftware** , oder erstellen Sie eine neue Richtlinie für Antischadsoftware. Weitere Informationen zum Erstellen von Antimalware-Richtlinien finden Sie unter [Erstellen und Bereitstellen von Richtlinien für Antischadsoftware für Endpoint Protection](endpoint-antimalware-policies.md).

4.  Klicken Sie im Abschnitt **Security Intelligence-Updates** des Dialogfelds mit Eigenschaften von Antischadsoftware auf **Quelle festlegen**.
    - Der Abschnitt **Definitionsupdates** wurde ab Configuration Manager Version 1902 in **Security Intelligence-Updates** umbenannt.

5.  Wählen Sie im Dialogfeld **Definitionsupdatequellen konfigurieren** die Quellen aus, die für Definitionsupdates verwendet werden sollen. Sie können auf **Nach oben** oder **Nach unten** klicken, um die Reihenfolge zu ändern, in der diese Quellen verwendet werden.

6.  Klicken Sie auf **OK** , um das Dialogfeld **Definitionsupdatequellen konfigurieren** zu schließen.

## <a name="configure-endpoint-protection-definitions"></a>Konfigurieren von Endpoint Protection-Definitionen

-   [Von Configuration Manager verteilte Updates](endpoint-definitions-configmgr.md) ‒ Diese Methode verwendet Configuration Manager-Softwareupdates, um Definitions- und Engine-Updates auf Computern in Ihrer Hierarchie bereitzustellen.

-   [Von WSUS (Windows Server Update Services) verteilte Updates](endpoint-definitions-wsus.md) ‒ Diese Methode verwendet Ihre WSUS-Infrastruktur, um Definitions- und Engine-Updates auf Computern bereitzustellen.

-   [Von Microsoft Update verteilte Updates](endpoint-definitions-microsoft-updates.md) ‒ Bei dieser Methode können Computer eine direkte Verbindung mit Microsoft Update herstellen, um die Definitions- und Engine-Updates herunterzuladen. Diese Methode kann bei Computern nützlich sein, die nicht oft mit dem Firmennetzwerk verbunden sind.

-   Von Microsoft Malware Protection Center verteilte Updates ‒ Bei dieser Methode werden Definitionsupdates vom Microsoft Malware Protection Center heruntergeladen.

-   [Updates von UNC-Dateifreigaben](endpoint-definitions-network.md) ‒ Mit dieser Methode können Sie die neuesten Definitions- und Engine-Updates in einer Freigabe auf dem Netzwerk speichern. Clients können dann zum Installieren der Updates auf das Netzwerk zugreifen.
