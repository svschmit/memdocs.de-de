---
title: Warteschlangen-Manager für Verteilungspunktaufträge
titleSuffix: Configuration Manager
description: Verwenden Sie den Warteschlangen-Manager für Verteilungspunktaufträge zum Beheben von Problemen und Verwalten von Inhaltsverteilungsaufträgen für Configuration Manager-Verteilungspunkte.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4b72922a-d11e-4aef-b309-19f5f0716f32
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9f6269d559bbcb192b1189419a8450a860d70058
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694338"
---
# <a name="dp-job-queue-manager"></a>Warteschlangen-Manager für Verteilungspunktaufträge

*Gilt für: Configuration Manager (Current Branch)*

Der Warteschlangen-Manager für Verteilungspunktaufträge ist eines der [Configuration Manager-Tools](tools.md). Verwenden Sie dieses Tool zum Beheben von Problemen und Verwalten von fortlaufenden Inhaltsverteilungsaufträgen für Configuration Manager-Verteilungspunkte. 

Das Tool zeigt die Liste der Aufträge an, die sich in der Warteschlange der Paketübertragungs-Manager-Komponente befinden. Es zeigt außerdem den Status der Aufträge: „ready to be executed“, „running“ oder „retrying“ („Bereit für die Ausführung“, „Wird ausgeführt“ oder „Wird wiederholt“). Mit dem Tool können Sie Aufträge in der Warteschlange bearbeiten, Aufträge in der Liste nach oben verschieben, Aufträge abbrechen oder einen Auftrag manuell ausführen.

Es ruft außerdem Informationen vom Standortserver ab, auf dem ein Verteilungspunkt einen Auftrag ausführt. Das Tool stellt über den Anbieter eine Verbindung mit dem Standortserver her. Es stellt keine Verbindung mit Remoteverteilungspunkten her, um diese Informationen zu erfassen. Da es Aktionen auslöst und Informationen über den Anbieter abruft, entsteht eine Verzögerung bei der Darstellung von Änderungen an Remoteverteilungspunkten.



## <a name="usage"></a>Verwendung

Führen Sie **DPJobMgr.exe** aus. Das Hauptmenü des Tools umfasst die folgenden Registerkarten: 

- [Verbinden:](#bkmk_connect) Zum Herstellen der ersten Verbindung mit dem primären Standortserver.  

- [Übersicht:](#bkmk_overview) Fasst alle Aufträge in einer Ansicht zusammen, die auf allen Verteilungspunkten ausgeführt werden.  

- [Distribution Point Info](#bkmk_dp-info) (Informationen zu Verteilungspunkten): Hier können Sie mehrere Verteilungspunkte für die Überwachung auswählen und einen einzelnen relevanten Auftrag verwalten.  

- [Aufträge verwalten:](#bkmk_manage-jobs) Zeigt eine flache Ansicht einer Liste aller Aufträge und deren Status an. Bearbeiten Sie Aufträge, verschieben Sie sie nach oben, brechen Sie sie ab, oder starten Sie sie manuell.  


### <a name="connect-tab"></a><a name="bkmk_connect"></a> Registerkarte „Verbinden“

Verwenden Sie diese Registerkarte, um die erste Verbindung mit dem primären Standortserver herzustellen. Hier werden die Anmeldeinformationen des derzeit angemeldeten Benutzers verwendet. Sie können keine Verbindung mit dem Standort der zentralen Verwaltung oder mit sekundären Standorten herstellen. Für diese Verbindung ist die Sicherheitsrolle **Hauptadministrator** erforderlich.

Sobald das Tool erfolgreich eine Verbindung herstellt, bestätigt eine Benachrichtigung am unteren Rand des Tools, das es mit dem Standortserver verbunden ist. 


### <a name="overview-tab"></a><a name="bkmk_overview"></a> Registerkarte „Übersicht“

Zeigt eine Zusammenfassung aller Aufträge auf allen Verteilungspunkten an. Weitere Informationen finden Sie in den folgenden Spalten:  

- **Verteilungspunkt:** Führt die Namen der Verteilungspunkte auf.  

- **Zurzeit ausgeführte Aufträge:** Zeigt die Anzahl von gleichzeitigen Aufträgen an, die auf einem bestimmten Verteilungspunkt ausgeführt werden.  

    > [!Tip]  
    > Die Anzahl von gleichzeitigen Softwareverteilungen ist eine Standorteinstellung. Diese Einstellung können Sie in den Eigenschaften der Softwareverteilungskomponente ändern.  

- **Aufträge insgesamt:** Zeigt die Anzahl aller Aufträge für einen bestimmten Verteilungspunkt an. Diese Anzahl umfasst alle Aufträge unabhängig von ihrem Status.  

- **Wiederholungen gesamt:** Zeigt die Anzahl von Wiederholungen der Aufträge eines bestimmten Verteilungspunkts an. Eine höhere Zahl kann ein allgemeines Problem mit diesem Verteilungspunkt darstellen.  


> [!Tip]  
> - Klicken Sie auf den Spaltennamen, um diese Spalte zu sortieren.  
> 
> - Sie können die Informationen in dieser Registerkarte manuell aktualisieren, indem Sie auf **Aktualisieren** klicken.  
> 
> - Sie können die Aktualisierung auch automatisch durchführen, indem Sie auf **Start Auto Refresh** (Automatische Aktualisierung starten) klicken und das Aktualisierungsintervall festlegen. Das Standardaktualisierungsintervall beträgt zwei Minuten.  


### <a name="distribution-point-info-tab"></a><a name="bkmk_dp-info"></a> Registerkarte „Informationen zu Verteilungspunkten“

Zeigt die Liste aller Verteilungspunkte am verbundenen Standort an. Im linken Bereich werden alle Verteilungspunkte aufgeführt. Klicken Sie nach Bedarf auf **Alle auswählen** oder **Auswahl aufheben**, oder wählen Sie mehrere bestimmte Verteilungspunkte in dieser Liste aus. Der rechte Bereich zeigt die Aufträge der ausgewählten Verteilungspunkte an.

Es gibt acht Spalten:  

- **Statussymbol:** Es gibt drei mögliche Statussymbole:  

    - **Bereit:** Gibt an, dass ein bestimmter Auftrag alle Überprüfungsschritte abgeschlossen hat. Er ist bereit, den gleichzeitig ausgeführten Aufträgen hinzugefügt zu werden. In der Regel befinden sich Aufträge in diesem Status in einer Wartephase. Sie warten darauf, dass der aktuell ausgeführte Prozess beendet wird, damit sie ausgeführt werden können.  

    - **Wird ausgeführt:** Gibt an, dass ein bestimmter Auftrag zurzeit auf einem Verteilungspunkt ausgeführt wird. Bei längeren Aufträgen (großen Paketen) ist es in der Regel möglich, den Auftrag (Fortschritt in %) abzuschließen. Dieser Prozentwert wird in dieser Ansicht in der Spalte **Fortschritt** angezeigt. Bei kleinen Paketen kann die Spalte **Fortschritt** leer bleiben. Der Auftrag ist möglicherweise abgeschlossen, bevor der Status vom Remoteverteilungspunkt empfangen wird.  

    - **Wiederholen:** Gibt an, dass ein bestimmter Auftrag fehlgeschlagen ist und sich jetzt im Status „Wiederholen“ befindet. Dieser Auftrag wird nach dem Wiederholungsintervall wiederholt. Das Intervall ist konfigurierbar und standardmäßig auf 30 Minuten festgelegt.  

- **Software**: Der Name des Pakets, das für einen bestimmten Verteilungspunkt vorgesehen ist.  

- **Paket-ID:** Die Paket-ID des Pakets, das für einen bestimmten Verteilungspunkt vorgesehen ist.  

- **Größe:** Die Größe des Pakets in KB.  

- **Fortschritt:** Der Fortschritt des Auftrags in Prozent. Weitere Informationen finden Sie in der Beschreibung des Statussymbols **Wird ausgeführt**.  

- **Start/Restart Time** (Start-/Neustartzeitpunkt): Für einen aktiven Auftrag ist dies der Startzeitpunkt (grün). Für einen Auftrag, der wiederholt wird, ist dies der Zeitpunkt, an dem der Auftrag neu gestartet wird.  

- **Wiederholungen**: Die Anzahl, wie oft dieses Paket vom Verteilungspunkt ausgeführt wurde.  

- **Name des Verteilungspunkts:** Dies ist der vollständig qualifizierte Domänennamen (FQDN) des Verteilungspunkts.  

> [!Tip]  
> - Klicken Sie auf den Spaltennamen, um diese Spalte zu sortieren.  
> 
> - Sie können die Informationen in dieser Registerkarte manuell aktualisieren, indem Sie auf **Aktualisieren** klicken.  
> 
> - Sie können die Aktualisierung auch automatisch durchführen, indem Sie auf **Start Auto Refresh** (Automatische Aktualisierung starten) klicken und das Aktualisierungsintervall festlegen. Das Standardaktualisierungsintervall beträgt zwei Minuten.  
> 
> - Wenn Sie einen bestimmten Auftrag bearbeiten müssen, klicken Sie in dieser Ansicht mit der rechten Maustaste auf den Auftrag, und wählen Sie **Auftrag verwalten** aus. Die [Registerkarte „Aufträge verwalten“](#bkmk_manage-jobs) wird geöffnet.  


### <a name="manage-jobs-tab"></a><a name="bkmk_manage-jobs"></a> Registerkarte „Aufträge verwalten“

Zeigt eine flache Ansicht einer Liste aller Aufträge und deren Status an. Sie enthält die gleichen acht Spalten wie die [Registerkarte „Informationen zu Verteilungspunkten“](#bkmk_dp-info). Klicken Sie in dieser Ansicht mit der rechten Maustaste auf die Aufträge, um folgende Aktionen auszuführen:  

- **Run**: Startet einen Auftrag, der nicht den Status „Wird ausgeführt“ aufweist.  

- **Move To Top** (An die oberste Position verschieben): Verschiebt mindestens einen Auftrag an die oberste Position in der Warteschlange. Diese Aktion kann dazu führen, dass die Aufträge sofort ausgeführt werden. Ein Auftrag mit niedriger Priorität kann aufgrund dieser Aktion anhalten.  

- **Nach oben verschieben:** Verschiebt einen bestimmten Auftrag um eine Zeile nach oben. Ein Auftrag mit niedriger Priorität kann aufgrund dieser Aktion anhalten.  

- **Nach unten:** Verschiebt einen bestimmten Auftrag um eine Zeile nach unten.  

- **Move To Bottom** (An die unterste Position verschieben): Verschiebt mindestens einen Auftrag an die unterste Position in der Warteschlange.  

    > [!Tip]  
    > Sie können Aufträge per Drag & Drop in der Liste verschieben.  

- **Abbrechen:** Versucht, einen oder mehrere Aufträge abzubrechen.  

    > [!Note]  
    > Sie können keine Aufträge beenden, die fast abgeschlossen sind. Wenn der Standortserver auch ein Verteilungspunkt ist, können Sie auf dem Standortserver keine Aufträge abbrechen.  



## <a name="see-also"></a>Weitere Informationen:

- [Grundlegende Konzepte für das Content Management](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [Paketübertragungs-Manager](../plan-design/hierarchy/package-transfer-manager.md)
