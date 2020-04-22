---
title: Verwalten und Überwachen von stufenweisen Bereitstellungen
titleSuffix: Configuration Manager
description: Grundlegendes zur Verwaltung und Überwachung von stufenweisen Bereitstellungen für Software in Configuration Manager.
ms.date: 04/16/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: dc245916-bc11-4983-9c4d-015f655007c1
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: fa36d3782f75605221c03b7c0791e9b75b68f6e5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690558"
---
# <a name="manage-and-monitor-phased-deployments"></a>Verwalten und Überwachen von stufenweisen Bereitstellungen

In diesem Artikel wird beschrieben, wie stufenweise Bereitstellungen verwaltet und überwacht werden können. Verwaltungsaufgaben umfassen das manuelle Starten der nächsten Phase sowie das Anhalten oder Fortsetzen einer Phase. 

Sie müssen zunächst eine stufenweise Bereitstellung erstellen: 
- [Anwendung](create-phased-deployment-for-task-sequence.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  
- [Softwareupdate](create-phased-deployment-for-task-sequence.md?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json)  
- [Tasksequenz](create-phased-deployment-for-task-sequence.md)  



## <a name="move-to-the-next-phase"></a><a name="bkmk_move"></a> Weiter zur nächsten Phase

Wenn Sie die Einstellung **Zweite Phase der Bereitstellung manuell starten** auswählen, startet der Standort die nächste Phase basierend auf Erfolgskriterien nicht automatisch. Sie müssen die stufenweise Bereitstellung in die nächste Phase verschieben.  

1. Wie diese Aktion gestartet wird, hängt von dem Typ der bereitgestellten Software ab:  

    - **Anwendung** (nur in der Version 1806 oder höher): Rufen Sie den Arbeitsbereich **Softwarebibliothek** auf, erweitern Sie **Anwendungsverwaltung**, und wählen Sie dann **Anwendungen** aus.   

    - **Softwareupdate** (nur in der Version 1810 oder höher): Rufen Sie den Arbeitsbereich **Softwarebibliothek** auf, und wählen Sie dann einen der folgenden Knoten aus:    
        - Softwareupdates  
            - **Alle Softwareupdates**  
            - **Softwareupdategruppen**   
        - Windows 10-Wartung, **Alle Windows 10-Updates**  
        - Office 365-Clientverwaltung, **Office 365-Updates**  

    - **Tasksequenz**: Rufen Sie den Arbeitsbereich **Softwarebibliothek** auf, erweitern Sie **Betriebssysteme**, und wählen Sie dann **Tasksequenzen** aus.   

2. Wählen Sie die Software mit der stufenweisen Bereitstellung aus.  

3. Wechseln Sie im Detailbereich zur Registerkarte **Stufenweise Bereitstellungen**.  

4. Wählen Sie die stufenweise Bereitstellung aus, und klicken Sie im Menüband auf **Move to next phase** (Weiter zur nächsten Phase).  

    ![Kontextmenü mit Aktionen für eine stufenweise Bereitstellung](media/Suspend-phased-deployment.PNG)



## <a name="suspend-and-resume-phases"></a><a name="bkmk_suspend"></a> Anhalten und Fortsetzen von Phasen 

Sie können eine stufenweise Bereitstellung manuell anhalten oder fortsetzen. Beispiel: Sie erstellen für eine Tasksequenz eine stufenweise Bereitstellung. Während Sie die Phase in Ihrer Pilotgruppe überwachen, fällt Ihnen eine Vielzahl an Fehlern auf. Sie halten die stufenweise Bereitstellung an, damit keine weiteren Geräte die Tasksequenz ausführen. Nachdem Sie das Problem behoben haben, setzen Sie die stufenweise Bereitstellung fort, um mit dem Rollout fortzufahren. 

1. Wie diese Aktion gestartet wird, hängt von dem Typ der bereitgestellten Software ab:  

    - **Anwendung** (nur in der Version 1806 oder höher): Rufen Sie den Arbeitsbereich **Softwarebibliothek** auf, erweitern Sie **Anwendungsverwaltung**, und wählen Sie dann **Anwendungen** aus.   

    - **Softwareupdate** (nur in der Version 1810 oder höher): Rufen Sie den Arbeitsbereich **Softwarebibliothek** auf, und wählen Sie dann einen der folgenden Knoten aus:    
        - Softwareupdates  
            - **Alle Softwareupdates**  
            - **Softwareupdategruppen**   
        - Windows 10-Wartung, **Alle Windows 10-Updates**  
        - Office 365-Clientverwaltung, **Office 365-Updates**  

    - **Tasksequenz**: Rufen Sie den Arbeitsbereich **Softwarebibliothek** auf, erweitern Sie **Betriebssysteme**, und wählen Sie dann **Tasksequenzen** aus. Wählen Sie eine vorhandene Tasksequenz aus, und klicken Sie anschließend im Menüband auf **Stufenweise Bereitstellung erstellen**.  

2. Wählen Sie die Software mit der stufenweisen Bereitstellung aus.  

3. Wechseln Sie im Detailbereich zur Registerkarte **Stufenweise Bereitstellungen**.  

4. Wählen Sie die stufenweise Bereitstellung aus, und klicken Sie im Menüband auf **Anhalten** oder **Fortsetzen**.  

<!-- Removed for 1806, need to clarify behavior with engineering
When you suspend a phased deployment, it sets the available and deadline times on the active deployments to a future time. When you resume, it generates a new schedule based on when you resume the phased deployment. The new schedule helps to avoid problems if you resume after the original deadline. For example, the initial schedule has the required deadline seven days after the deployment is available. You suspend it on the second day. If you aren't ready to resume it until day eight, you don't want the deployment to be immediately past the deadline. So it generates a new deadline starting from when you resume the phased deployment on day eight. 
-->


## <a name="monitor"></a><a name="bkmk_monitor"></a> Überwachung
<!--1358577-->
Stufenweise Bereitstellungen verfügen ab Version 1902 über einen dedizierten Überwachungsknoten. Damit ist es einfacher, von Ihnen erstellte stufenweise Bereitstellungen zu identifizieren und zur Überwachungsansicht für stufenweise Bereitstellungen zu navigieren. Wählen Sie im Arbeitsbereich **Überwachung** die Option **Stufenweise Bereitstellungen** aus, und doppelklicken Sie auf eine der stufenweisen Bereitstellungen, um den Status anzuzeigen. <!--3555949-->

In Configuration Manager 1806 und 1810 können Sie die native Überwachungsoberfläche für stufenweise Bereitstellungen anzeigen. Wählen Sie im Knoten **Bereitstellungen** im Arbeitsbereich **Überwachung** eine Bereitstellung in Phasen aus, und klicken Sie dann im Menüband auf **Status der Bereitstellung in Phasen**.

![Dashboard zum Status der Bereitstellung in Phasen mit Status von zwei Phasen](media/1358577-phased-deployment-status.png)

Dieses Dashboard zeigt für jede Phase in der Bereitstellung die folgenden Informationen an:  

- **Geräte gesamt** oder **Ressourcen gesamt**: auf wie viele Geräte sich diese Phase auswirkt.  

- **Status:** der aktuelle Status dieser Phase. Jede Phase kann einen der folgenden Zustände aufweisen:  

    - **Bereitstellung erstellt:** Bei der Bereitstellung in Phasen wurde eine Bereitstellung der Software für die Sammlung für diese Phase erstellt. An Clients wird diese Software gesendet.  

    - **Warten:** Da die vorherige Phase noch nicht die Erfolgskriterien für die Bereitstellung erfüllt hat, kann noch nicht mit dieser Phase fortgefahren werden.  

    - **Angehalten:** Ein Administrator hat die Bereitstellung angehalten.  

- **Fortschritt:** die farbcodierten Bereitstellungszustände von Clients. Beispiel: „Erfolg“, „In Bearbeitung“, „Fehler“, „Anforderungen nicht erfüllt“ und „Unbekannt“. 

#### <a name="success-criteria-tile"></a>Kachel „Erfolgskriterien“

Sie können in der Dropdownliste **Phase auswählen** die Anzeige der Kachel **Erfolgskriterien** ändern. Auf dieser Kachel wird das **Ziel der Phase** mit der aktuellen Konformität der Bereitstellung verglichen. Bei den Standardeinstellungen sind 95 % das Ziel der Phase. Dieser Wert bedeutet, dass die Bereitstellung eine Konformität in Höhe von 95 % benötigt, um mit der nächsten Phase fortfahren zu können.

In diesem Beispiel stellen 65 Prozent das Ziel der Phase und 66,7 Prozent die aktuelle Konformität dar. Die stufenweise Bereitstellung ist automatisch in die zweite Phase gewechselt, da die Erfolgskriterien in der ersten Phase erfüllt wurden.  

   ![Beispielkachel „Erfolgskriterien“ zum Status der stufenweisen Bereitstellung mit dem Ziel 65 Prozent](media/pod-status-success-criteria-tile.png)

Das Ziel der Phase entspricht dem **Bereitstellungserfolg in Prozent** in den Phaseneinstellungen für die *nächste* Phase. Diese zweite Phase definiert die Erfolgskriterien für die erste Phase, damit die stufenweise Bereitstellung in die nächste Phase wechseln kann. So zeigen Sie diese Einstellung an: 

1. Wechseln Sie in der Software zu dem Objekt mit der stufenweisen Bereitstellung, und öffnen Sie „Eigenschaften der stufenweisen Bereitstellung“.  

2. Wechseln Sie zur Registerkarte **Phasen**. Wählen Sie **Phase 2** aus, und klicken Sie auf **Anzeigen**.  

3. Wechseln Sie im Fenster „Eigenschaften“ der Phase zur Registerkarte **Phaseneinstellungen**.  

4. Zeigen Sie den Wert für den **Bereitstellungserfolg in Prozent** in der Gruppe *Kriterien für den Erfolg der vorherigen Phase* an.  

Die folgenden Eigenschaften beziehen sich beispielsweise auf die gleiche Phase wie die oben dargestellte Kachel „Erfolgskriterien“, bei der die Kriterien 65 % betragen:  
![Registerkarte „Phaseneinstellungen“ in den Phaseneigenschaften](media/phase-properties-phase-settings.png)

