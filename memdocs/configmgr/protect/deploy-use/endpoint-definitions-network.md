---
title: Herunterladen der Definitionen von einer Netzwerkfreigabe
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie die neuesten Definitionsupdates von Microsoft herunterladen und anschließend Clients so konfigurieren, dass sie diese Definitionen herunterladen.
ms.date: 11/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ddef4d2a-f481-4020-9ddd-9cca5f9795cb
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9afeee7f7111994f0ae3891c7ecd99a11d7edd7d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697228"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-a-network-share"></a>Aktivieren der Endpoint Protection-Schadsoftwaredefinitionen zum Herunterladen von einer Netzwerkfreigabe

*Gilt für: Configuration Manager (Current Branch)*

 Sie können die neuesten Definitionsupdates von Microsoft manuell herunterladen und dann die Clients so konfigurieren, dass diese Definitionen aus einem freigegebenen Ordner im Netzwerk heruntergeladen werden. Bei Verwendung dieser Updatequelle können auch die Benutzer Definitionsupdates einleiten.

> [!NOTE]
>  Die Clients benötigen Lesezugriff auf den freigegebenen Ordner, um Definitionsupdates herunterladen zu können.

 Weitere Informationen zum Herunterladen der Definitions- und Engine-Updates zum Speichern in der Dateifreigabe finden Sie unter [Installieren der neuesten Antischadsoftware und Antispyware von Microsoft](https://www.microsoft.com/wdsi/definitions).

## <a name="to-configure-definition-downloads-from-a-file-share"></a>So konfigurieren Sie das Herunterladen von Definitionen von einer Dateifreigabe

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.

2.  Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** den Knoten **Endpoint Protection**, und klicken Sie dann auf **Richtlinien für Antischadsoftware**.

3.  Öffnen Sie die Eigenschaftenseite für die **Standardrichtlinie für Antischadsoftware** , oder erstellen Sie eine neue Richtlinie für Antischadsoftware. Weitere Informationen zum Erstellen von Antimalware-Richtlinien finden Sie unter [Erstellen und Bereitstellen von Richtlinien für Antischadsoftware für Endpoint Protection](endpoint-antimalware-policies.md).

4.  Klicken Sie im Abschnitt **Security Intelligence-Updates** des Dialogfelds mit Eigenschaften von Antischadsoftware auf **Quelle festlegen**.
    - Der Abschnitt **Definitionsupdates** wurde ab Configuration Manager Version 1902 in **Security Intelligence-Updates** umbenannt.

5.  Wählen Sie im Dialogfeld **Definitionsupdatequellen konfigurieren** die Option **Updates von UNC-Dateifreigaben**aus.

6.  Klicken Sie auf **OK** , um das Dialogfeld **Definitionsupdatequellen konfigurieren** zu schließen.

7.  Klicken Sie auf **Pfade festlegen**. Fügen Sie dann im Dialogfeld **UNC-Pfade für Definitionsupdates konfigurieren** mindestens einen UNC-Pfad zum Speicherort der Definitionsupdatedateien in einer Netzwerkfreigabe hinzu.

8.  Klicken Sie auf **OK** , um das Dialogfeld **UNC-Pfade für Definitionsupdates konfigurieren** zu schließen.


> [!div class="button"]
> [Nächster Schritt >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [Zurück >](endpoint-configure-alerts.md)
