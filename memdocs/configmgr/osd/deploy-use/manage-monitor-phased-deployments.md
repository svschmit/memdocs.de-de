---
title: Verwalten und Überwachen von stufenweisen Bereitstellungen
titleSuffix: Configuration Manager
description: Grundlegendes zur Verwaltung und Überwachung von stufenweisen Bereitstellungen für Software in Configuration Manager.
ms.date: 08/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: dc245916-bc11-4983-9c4d-015f655007c1
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7295e6f74764b378be8315599357424cbf6ead73
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820407"
---
# <a name="manage-and-monitor-phased-deployments"></a>Verwalten und Überwachen von stufenweisen Bereitstellungen

In diesem Artikel wird beschrieben, wie stufenweise Bereitstellungen verwaltet und überwacht werden können. Verwaltungsaufgaben umfassen das manuelle Starten der nächsten Phase sowie das Anhalten oder Fortsetzen einer Phase.

Sie müssen zunächst eine stufenweise Bereitstellung erstellen:

- [Anwendung](create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/apps/toc.json&bc=/mem/configmgr/apps/breadcrumb/toc.json)  
- [Softwareupdate](create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/sum/toc.json&bc=/mem/configmgr/sum/breadcrumb/toc.json)  
- [Tasksequenz](create-phased-deployment-for-task-sequence.md)  

## <a name="move-to-the-next-phase"></a><a name="bkmk_move"></a> Weiter zur nächsten Phase

Wenn Sie die Einstellung **Zweite Phase der Bereitstellung manuell starten** auswählen, startet der Standort die nächste Phase basierend auf Erfolgskriterien nicht automatisch. Sie müssen die stufenweise Bereitstellung in die nächste Phase verschieben.  

1. Wie diese Aktion gestartet wird, hängt von dem Typ der bereitgestellten Software ab:  

    - **Anwendung:** Rufen Sie den Arbeitsbereich **Softwarebibliothek** auf, erweitern Sie **Anwendungsverwaltung**, und wählen Sie dann **Anwendungen** aus.

    - **Softwareupdate:** Rufen Sie den Arbeitsbereich **Softwarebibliothek** auf, und wählen Sie dann einen der folgenden Knoten aus:
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

Ab Version 2002 können Sie das folgenden PowerShell-Cmdlet von Windows für diese Aufgabe verwenden: [Move-CMPhasedDeploymentToNext](/powershell/module/configurationmanager/move-cmphaseddeploymenttonext?view=sccm-ps).

## <a name="suspend-and-resume-phases"></a><a name="bkmk_suspend"></a> Anhalten und Fortsetzen von Phasen

Sie können eine stufenweise Bereitstellung manuell anhalten oder fortsetzen. Beispiel: Sie erstellen für eine Tasksequenz eine stufenweise Bereitstellung. Während Sie die Phase in Ihrer Pilotgruppe überwachen, fällt Ihnen eine Vielzahl an Fehlern auf. Sie halten die stufenweise Bereitstellung an, damit keine weiteren Geräte die Tasksequenz ausführen. Nachdem Sie das Problem behoben haben, setzen Sie die stufenweise Bereitstellung fort, um mit dem Rollout fortzufahren.

1. Wie diese Aktion gestartet wird, hängt von dem Typ der bereitgestellten Software ab:  

    - **Anwendung:** Rufen Sie den Arbeitsbereich **Softwarebibliothek** auf, erweitern Sie **Anwendungsverwaltung**, und wählen Sie dann **Anwendungen** aus.

    - **Softwareupdate:** Rufen Sie den Arbeitsbereich **Softwarebibliothek** auf, und wählen Sie dann einen der folgenden Knoten aus:
        - Softwareupdates  
            - **Alle Softwareupdates**  
            - **Softwareupdategruppen**
        - Windows 10-Wartung, **Alle Windows 10-Updates**  
        - Office 365-Clientverwaltung, **Office 365-Updates**  

    - **Tasksequenz**: Rufen Sie den Arbeitsbereich **Softwarebibliothek** auf, erweitern Sie **Betriebssysteme**, und wählen Sie dann **Tasksequenzen** aus. Wählen Sie eine vorhandene Tasksequenz aus, und klicken Sie anschließend im Menüband auf **Stufenweise Bereitstellung erstellen**.  

2. Wählen Sie die Software mit der stufenweisen Bereitstellung aus.  

3. Wechseln Sie im Detailbereich zur Registerkarte **Stufenweise Bereitstellungen**.  

4. Wählen Sie die stufenweise Bereitstellung aus, und klicken Sie im Menüband auf **Anhalten** oder **Fortsetzen**.

> [!NOTE]
> Ab dem 21. April 2020 wird Office 365 ProPlus in **Microsoft 365 Apps for Enterprise** umbenannt. Weitere Informationen finden Sie unter [Namensänderung für Office 365 ProPlus](/deployoffice/name-change). Möglicherweise finden Sie während des Updates der Konsole den alten Namen noch im Produkt Configuration Manager und der unterstützenden Dokumentation.

Ab Version 2002 können Sie die folgenden PowerShell-Cmdlets von Windows für diese Aufgabe verwenden:

- [Suspend-CMPhasedDeployment](/powershell/module/configurationmanager/suspend-cmphaseddeployment?view=sccm-ps)
- [Resume-CMPhasedDeployment](/powershell/module/configurationmanager/resume-cmphaseddeployment?view=sccm-ps)

## <a name="monitor"></a><a name="bkmk_monitor"></a> Überwachung
<!--1358577-->

Bereitstellungen in Phasen verfügen ab sofort über einen dedizierten Überwachungsknoten. Damit ist es einfacher, von Ihnen erstellte Bereitstellungen in Phasen zu identifizieren und zur Überwachungsansicht für Bereitstellungen in Phasen zu navigieren. Wählen Sie im Arbeitsbereich **Überwachung** die Option **Stufenweise Bereitstellungen** aus, und doppelklicken Sie auf eine der stufenweisen Bereitstellungen, um den Status anzuzeigen. <!--3555949-->

![Dashboard zum Status der Bereitstellung in Phasen mit Status von zwei Phasen](media/1358577-phased-deployment-status.png)

Dieses Dashboard zeigt für jede Phase in der Bereitstellung die folgenden Informationen an:  

- **Geräte gesamt** oder **Ressourcen gesamt**: auf wie viele Geräte sich diese Phase auswirkt.  

- **Status:** der aktuelle Status dieser Phase. Jede Phase kann einen der folgenden Zustände aufweisen:  

  - **Bereitstellung erstellt:** Bei der Bereitstellung in Phasen wurde eine Bereitstellung der Software für die Sammlung für diese Phase erstellt. An Clients wird diese Software gesendet.  

  - **Warten:** Da die vorherige Phase noch nicht die Erfolgskriterien für die Bereitstellung erfüllt hat, kann noch nicht mit dieser Phase fortgefahren werden.  

  - **Angehalten:** Ein Administrator hat die Bereitstellung angehalten.  

- **Fortschritt:** die farbcodierten Bereitstellungszustände von Clients. Beispiel: „Erfolg“, „In Bearbeitung“, „Fehler“, „Anforderungen nicht erfüllt“ und „Unbekannt“.

### <a name="success-criteria-tile"></a>Kachel „Erfolgskriterien“

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

## <a name="powershell"></a>PowerShell

Verwenden Sie die folgenden PowerShell-Cmdlets von Windows, um Bereitstellungen in Phasen zu verwalten:

### <a name="automatically-create-phased-deployments"></a>Automatisches Erstellen von Bereitstellungen in Phasen

- [New-CMApplicationAutoPhasedDeployment](/powershell/module/configurationmanager/new-cmapplicationautophaseddeployment?view=sccm-ps)
- [New-CMSoftwareUpdateAutoPhasedDeployment](/powershell/module/configurationmanager/new-cmsoftwareupdateautophaseddeployment?view=sccm-ps)
- [New-CMTaskSequenceAutoPhasedDeployment](/powershell/module/configurationmanager/new-cmtasksequenceautophaseddeployment?view=sccm-ps)

### <a name="manually-create-phased-deployments"></a>Manuelles Erstellen von Bereitstellungen in Phasen

- [New-CMSoftwareUpdatePhase](/powershell/module/configurationmanager/new-cmsoftwareupdatephase?view=sccm-ps)
- [New-CMSoftwareUpdateManualPhasedDeployment](/powershell/module/configurationmanager/new-cmsoftwareupdatemanualphaseddeployment?view=sccm-ps)
- [New-CMTaskSequencePhase](/powershell/module/configurationmanager/new-cmtasksequencephase?view=sccm-ps)
- [New-CMTaskSequenceManualPhasedDeployment](/powershell/module/configurationmanager/new-cmtasksequencemanualphaseddeployment?view=sccm-ps)

### <a name="get-existing-phased-deployment-objects"></a>Abrufen vorhandener Bereitstellungsobjekte in Phasen

- [Get-CMApplicationPhasedDeployment](/powershell/module/configurationmanager/get-cmapplicationphaseddeployment?view=sccm-ps)
- [Get-CMSoftwareUpdatePhasedDeployment](/powershell/module/configurationmanager/get-cmsoftwareupdatephaseddeployment?view=sccm-ps)
- [Get-CMTaskSequencePhasedDeployment](/powershell/module/configurationmanager/get-cmtasksequencephaseddeployment?view=sccm-ps)
- [Get-CMPhase](/powershell/module/configurationmanager/get-cmphase?view=sccm-ps)

### <a name="monitor-phased-deployment-status"></a>Überwachung des Status von Bereitstellungen in Phasen

- [Get-CMPhasedDeploymentStatus](/powershell/module/configurationmanager/get-cmphaseddeploymentstatus?view=sccm-ps)

### <a name="manage-existing-phased-deployments"></a>Verwalten vorhandener Bereitstellungen in Phasen

- [Move-CMPhasedDeploymentToNext](/powershell/module/configurationmanager/move-cmphaseddeploymenttonext?view=sccm-ps)
- [Resume-CMPhasedDeployment](/powershell/module/configurationmanager/resume-cmphaseddeployment?view=sccm-ps)
- [Suspend-CMPhasedDeployment](/powershell/module/configurationmanager/suspend-cmphaseddeployment?view=sccm-ps)

### <a name="modify-existing-phased-deployments"></a>Bearbeiten vorhandener Bereitstellungen in Phasen

- [Set-CMApplicationPhasedDeployment](/powershell/module/configurationmanager/set-cmapplicationphaseddeployment?view=sccm-ps)
- [Set-CMSoftwareUpdatePhase](/powershell/module/configurationmanager/set-cmsoftwareupdatephase?view=sccm-ps)
- [Set-CMSoftwareUpdatePhasedDeployment](/powershell/module/configurationmanager/set-cmsoftwareupdatephaseddeployment?view=sccm-ps)
- [Set-CMTaskSequencePhase](/powershell/module/configurationmanager/set-cmtasksequencephase?view=sccm-ps)
- [Set-CMTaskSequencePhasedDeployment](/powershell/module/configurationmanager/set-cmtasksequencephaseddeployment?view=sccm-ps)
- [Remove-CMApplicationPhasedDeployment](/powershell/module/configurationmanager/remove-cmapplicationphaseddeployment?view=sccm-ps)
- [Remove-CMSoftwareUpdatePhasedDeployment](/powershell/module/configurationmanager/remove-cmsoftwareupdatephaseddeployment?view=sccm-ps)
- [Remove-CMTaskSequencePhasedDeployment](/powershell/module/configurationmanager/remove-cmtasksequencephaseddeployment?view=sccm-ps)
