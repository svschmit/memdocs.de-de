---
title: Debuggen einer Tasksequenz
titleSuffix: Configuration Manager
description: Verwenden Sie das Debugtool für Tasksequenzen zur Problembehandlung einer Tasksequenz.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 4b60b0e1-ffa4-4fd5-864e-70a0546c8b3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 99ed8232a74b038b9b1cde4af257353252454c2b
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125150"
---
# <a name="debug-a-task-sequence"></a>Debuggen einer Tasksequenz

*Gilt für: Configuration Manager (Current Branch)*

<!--3612274-->

Ab Version 1906 ist der Debugger für Tasksequenzen ein neues Tool für die Problembehandlung. Sie stellen eine Tasksequenz im Debugmodus für eine kleine Sammlung bereit. In diesem Modus können Sie die Tasksequenz kontrolliert durchlaufen, um die Problembehandlung und -untersuchung zu erleichtern. Der Debugger wird derzeit auf demselben Gerät wie die Tasksequenzengine ausgeführt, es handelt sich nicht um einen Remotedebugger.

> [!Note]  
> In dieser Version von Configuration Manager ist der Tasksequenzdebugger als Vorabfeature enthalten. Wie Sie es aktivieren, erfahren Sie unter [Pre-release features (Features von Vorabreleases)](../../core/servers/manage/pre-release-features.md).  


## <a name="prerequisites"></a>Voraussetzungen

- Aktualisieren des Configuration Manager-Clients auf dem Zielgerät

- Melden Sie sich am Zielgerät als Benutzer in der lokalen Gruppe **Administratoren** an. Der Debugger wird nur für Administratoren ausgeführt.

- Aktualisieren des Startimages, das der Tasksequenz zugeordnet ist, um sicherzustellen, dass die neueste Clientversion vorhanden ist


## <a name="start-the-tool"></a>Starten des Tools

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie anschließend auf **Tasksequenzen**.

1. Wählen Sie eine Tasksequenz aus. Klicken Sie auf dem Menüband in der Gruppe „Bereitstellung“ auf **Debuggen**.

    > [!Tip]  
    > Alternativ können Sie die Variable **TSDebugMode** für eine Sammlung oder ein Computerobjekt, für das die Tasksequenz bereitgestellt wird, auf `TRUE` festlegen. Jedes Geräte, für das diese Variable festgelegt ist, versetzt für das Gerät bereitgestellte Tasksequenzen in den Debugmodus.

1. Erstellen Sie eine Debugbereitstellung. Die Bereitstellungseinstellungen sind dieselben wie bei einer normalen Tasksequenzbereitstellung. Weitere Informationen finden Sie unter [Deploy a task sequence](deploy-a-task-sequence.md#process).

    > [!Note]  
    > Sie können nur eine kleine Sammlung für eine Debugbereitstellung auswählen. Sie zeigt nur Gerätesammlungen mit 10 oder weniger Mitgliedern an.

Verwenden Sie ab Version 1910 die neue Tasksequenzvariable **TSDebugOnError**, um automatisch den Debugger zu starten, wenn die Tasksequenz einen Fehler zurückgibt.<!-- 5012536 --> Weitere Informationen finden Sie unter [Tasksequenzvariablen – TSDebugOnError](../understand/task-sequence-variables.md#TSDebugOnError).

## <a name="use-the-tool"></a>Verwendung des Tools

Wenn die Tasksequenz auf dem Gerät ausgeführt wird, öffnet sich das Fenster „Tasksequenz-Debugger“ ähnlich wie im folgenden Screenshot:

![Screenshot des Tasksequenz-Debuggers](media/3612274-tsdebug.png)

Der Debugger bietet die folgenden Steuerelemente:

- **Step** (Schritt): Ab der *aktuellen* Position nur den nächsten Schritt in der Tasksequenz ausführen.  

    > [!Note]  
    > Wenn sich die Tasksequenz im Debugmodus befindet und bei einem Schritt ein schwerwiegender Fehler zurückgegeben wird, schlägt die Tasksequenz nicht wie üblich fehl. Dieses Verhalten gibt Ihnen die Möglichkeit, einen Schritt zu wiederholen, nachdem Sie eine externe Änderung vorgenommen haben.

- **Run**: Von der *aktuellen* Position die Tasksequenz normal bis zum Ende ausführen oder bei einem Fehler in einem Schritt bis zum nächsten *Haltepunkt* ausführen. Bevor Sie diese Aktion verwenden, stellen Sie sicher, dass Sie alle Haltepunkte mit der Aktion **Set Break** (Haltepunkt festlegen) festlegen.

- **Set Current** (Als aktuell festlegen): Einen Schritt im Debugger auswählen und dann auf **Set Current** klicken. Diese Aktion verschiebt den *aktuellen* Zeiger zu diesem Schritt. Mit dieser Aktion können Sie Schritte überspringen oder sich zurück bewegen.  

    > [!Warning]  
    > Der Debugger berücksichtigt die Art des Schritts nicht, wenn Sie die aktuelle Position in der Sequenz ändern. Einige Schritte können Tasksequenzvariablen festlegen, die für die Bedingungsauswertung in späteren Schritten erforderlich sind. Wenn Schritte nicht in der richtigen Reihenfolge erfolgen, können einige Schritte fehlschlagen oder erhebliche Schäden an einem Gerät verursachen. Sie verwenden diese Option auf eigene Gefahr.  

- **Set Break** (Haltepunkt festlegen): Einen Schritt im Debugger auswählen und dann auf **Set Break** klicken. Dieser Vorgang fügt im Debugger einen *Haltepunkt* hinzu. Wenn Sie die Tasksequenz **ausführen**, wird sie beim *Haltepunkt* unterbrochen.  

    - Bevor Sie die Aktion **Ausführen** verwenden, legen Sie Haltepunkte fest.

    - Wenn Sie ab Version 1910 im Debugger einen Haltepunkt erstellen und die Tasksequenz den Computer neu startet, behält der Debugger Ihren Haltepunkt nach dem Neustart bei.<!-- 5012509 -->

    - In Version 1906 werden Haltepunkte nach dem Neustart des Computers nicht gespeichert, wie beim Schritt [Computer neu starten](../understand/task-sequence-steps.md#BKMK_RestartComputer). Wenn Sie z. B. den Debugger aus dem Softwarecenter für die Tasksequenz „Imageerstellung“ starten, legen Sie in der Windows PE-Phase keine Haltepunkte fest. Wenn der Computer in Windows PE neu gestartet wird, pausiert der Debugger die Tasksequenz, sodass Sie Haltepunkte festlegen können.

- **Alle Haltepunkte löschen**: Entfernen Sie alle Haltepunkte.

- **Protokolldatei**: Öffnet die aktuelle Protokolldatei der Tasksequenz, **smsts.log**, mit [CMTrace](../../core/support/cmtrace.md). Sie können Protokolleinträge anzeigen, wenn die Tasksequenzengine auf den Debugger wartet.

- **Eingabeaufforderung**: Öffnet in Windows PE eine Eingabeaufforderung.

- **Abbrechen:** Schließen Sie den Debugger und bei der Tasksequenz tritt ein Fehler auf.

- **Quit** (Beenden): Trennen und schließen Sie den Debugger, aber die Tasksequenz wird weiterhin normal ausgeführt.

Das Fenster **Tasksequenzvariablen** zeigt die aktuellen Werte für alle Variablen in der Tasksequenzumgebung an. Weitere Informationen finden Sie unter [Tasksequenzvariablen](../understand/task-sequence-variables.md). Wenn Sie den Schritt [Tasksequenzvariable festlegen](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) mit der Option **Diesen Wert nicht anzeigen** verwenden, zeigt der Debugger den Variablenwert nicht an. Sie können die Variablenwerte im Debugger nicht bearbeiten.

> [!Note]
> Einige Tasksequenzvariablen sind nur für den internen Gebrauch bestimmt und nicht in der Referenzdokumentation aufgeführt.

Der Tasksequenzdebugger wird nach dem Schritt [Computer neu starten](../understand/task-sequence-steps.md#BKMK_RestartComputer) weiter ausgeführt, aber Sie müssen alle Haltepunkte neu erstellen. Auch wenn die Tasksequenz dies möglicherweise nicht vorschreibt, da der Debugger eine Benutzerinteraktion erfordert, müssen Sie sich bei Windows anmelden, um fortfahren zu können. Wenn Sie sich nach einer Stunde nicht anmelden, um das Debuggen fortzusetzen, tritt ein Fehler in der Tasksequenz auf.

Sie wechselt auch in eine untergeordnete Tasksequenz mit dem Schritt [Tasksequenz ausführen](../understand/task-sequence-steps.md#child-task-sequence). Das Debuggerfenster zeigt die Schritte der untergeordneten Tasksequenz zusammen mit der Haupttasksequenz an.


## <a name="known-issues"></a>Bekannte Probleme

Wenn Sie sowohl auf eine normale Bereitstellung als auch eine Debugbereitstellung über mehrere Bereitstellungen auf dasselbe Gerät ausgerichtet sind, startet der Tasksequenzdebugger möglicherweise nicht.


## <a name="see-also"></a>Weitere Informationen:

- [Informationen zu Tasksequenzschritten](../understand/task-sequence-steps.md)
- [Tasksequenzvariablen](../understand/task-sequence-variables.md)
- [Verwenden von Tasksequenzvariablen](../understand/using-task-sequence-variables.md)
- [Bereitstellen einer Tasksequenz](deploy-a-task-sequence.md)
