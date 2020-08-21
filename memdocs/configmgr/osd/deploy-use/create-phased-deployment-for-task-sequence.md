---
title: Bereitstellung in Phasen
titleSuffix: Configuration Manager
description: Verwenden Sie die stufenweise Bereitstellung, um das Rollout von Software für mehrere Sammlungen zu automatisieren.
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: b634ff68-b909-48d2-9e2c-0933486673c5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d9dcefe942309ad57c823ec669b7aa6630974fa8
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88698026"
---
# <a name="create-phased-deployments-with-configuration-manager"></a>Erstellen von stufenweisen Bereitstellungen mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Bereitstellungen in Phasen automatisieren ein koordiniertes Rollout von Software in einer bestimmten Reihenfolge über mehrere Sammlungen hinweg. Sie können die Software beispielsweise für eine Pilotsammlung bereitstellen, und anschließend wird der Rollout basierend auf Erfolgskriterien automatisch fortgesetzt. Erstellen Sie stufenweise Bereitstellungen mit einer von zwei Standardphasen, oder konfigurieren Sie mehrere Phasen manuell. 

Erstellen Sie stufenweise Bereitstellungen für die folgenden Objekte:
- **Tasksequenz**  
    - Die stufenweise Bereitstellung von Tasksequenzen unterstützt keine PXE- oder Medieninstallation.   
- **Anwendung** (ab Version 1806) <!--1358147-->  
- **Softwareupdate** (ab Version 1810) <!--1358146-->  
    - Sie können keine automatische Bereitstellungsregel bei der stufenweisen Bereitstellung verwenden.

> [!Tip]  
> Das Feature für die stufenweise Bereitstellung wurde erstmals in Version 1802 als [Vorabfeature](../../core/servers/manage/pre-release-features.md) eingeführt. Ab Version 1806 ist es kein Vorabfeature mehr.<!--1356837-->  



## <a name="prerequisites"></a>Voraussetzungen

#### <a name="security-scope"></a>Sicherheitsbereich
Bereitstellungen, die von stufenweisen Bereitstellungen erstellt werden, können von keinem Administrator angezeigt werden, der nicht über den Sicherheitsbereich **Alles** verfügt. Weitere Informationen finden Sie unter [Sicherheitsbereiche](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope).

#### <a name="distribute-content"></a>Verteilen von Inhalt
Bevor Sie die stufenweise Bereitstellung erstellen, verteilen Sie den zugehörigen Inhalt an einen Verteilungspunkt.<!--518293-->  

- **Anwendung:** Wählen Sie die Zielanwendung in der Konsole aus, und verwenden Sie die Menübandaktion **Inhalt verteilen**. Weitere Informationen finden Sie unter [Bereitstellen und Verwalten von Inhalt](../../core/servers/deploy/configure/deploy-and-manage-content.md).   

- **Tasksequenz**: Sie müssen Objekte wie das Betriebssystemaktualisierungspaket erstellen, auf die verwiesen wird, bevor Sie die Tasksequenz erstellen. Verteilen Sie diese Objekte, bevor Sie eine Bereitstellung erstellen. Verwenden Sie die Aktion **Inhalt verteilen** oder die Tasksequenz für jedes Objekt. Wählen Sie die Tasksequenz aus, und wechseln Sie zur Registerkarte **Verweise** im Detailbereich, um die Status aller Inhalte anzuzeigen, auf die verwiesen wird. Weitere Informationen zu den einzelnen Objekttypen finden Sie unter [Vorbereiten auf die Betriebssystembereitstellung](../get-started/prepare-for-operating-system-deployment.md).   

- **Softwareupdate:** Erstellen Sie das Bereitstellungspaket, und verteilen Sie es. Verwenden Sie hierzu den Assistenten zum Herunterladen von Softwareupdates. Weitere Informationen finden Sie unter [Herunterladen von Softwareupdates](../../sum/deploy-use/download-software-updates.md).  



## <a name="phase-settings"></a><a name="bkmk_settings"></a> Phaseneinstellungen

Diese Einstellungen werden nur für stufenweise Bereitstellungen verwendet. Konfigurieren Sie diese Einstellungen beim Erstellen oder Bearbeiten der Phasen, um die Zeitplanung und das Verhalten des stufenweisen Bereitstellungsprozesses zu steuern. 


#### <a name="criteria-for-success-of-the-first-phase"></a>Kriterien für den Erfolg der ersten Phase  

- **Bereitstellungserfolg in Prozent**: Geben Sie den Prozentsatz der Geräte an, für die die Bereitstellung der ersten Phase erfolgreich abgeschlossen werden muss. Der Standardwert beträgt 95 %. Das heißt, der Standort betrachtet die erste Phase als erfolgreich abgeschlossen, wenn der Konformitätszustand für 95 % der Geräte für diese Bereitstellung **Erfolgreich** ist. Der Standort fährt dann mit der zweiten Phase fort und erstellt eine Softwarebereitstellung für die nächste Sammlung.  
- **Anzahl erfolgreich bereitgestellter Geräte**: Hinzugefügt in Configuration Manager, Version 1902. Geben Sie die Anzahl von Geräten an, für die die Bereitstellung der ersten Phase erfolgreich abgeschlossen werden muss. Diese Option ist nützlich, wenn die Größe der Sammlung variabel ist und Sie eine bestimmte Anzahl von Geräten haben, die Erfolg zeigen müssen, bevor mit der nächsten Phase fortgefahren wird. <!--3555946-->


#### <a name="conditions-for-beginning-second-phase-of-deployment-after-success-of-the-first-phase"></a>Bedingungen für den Start der zweiten Phase der Bereitstellung nach erfolgreichem Abschluss der ersten Phase  

- **Diese Phase nach Verzögerung (in Tagen) automatisch starten**: Legen Sie fest, wie viele Tage nach dem erfolgreichen Abschluss der vorherigen Phase die nächste beginnen soll. Dieser Wert entspricht standardmäßig einem Tag.  

- **Manually begin the second phase of deployment** (Die zweite Bereitstellungsphase manuell starten): Der Standort beginnt nach erfolgreichem Abschluss der ersten Phase nicht automatisch mit der zweiten Phase. Diese Option erfordert, dass Sie die zweite Phase manuell starten. Weitere Informationen finden Sie unter [Move to the next phase (Einleiten der nächsten Phase)](manage-monitor-phased-deployments.md#bkmk_move).  

    > [!Note]  
    > Diese Option ist für die stufenweise Bereitstellung von Anwendungen nicht verfügbar.  


#### <a name="gradually-make-this-software-available-over-this-period-of-time-in-days"></a>Diese Software in diesem Zeitraum (in Tagen) schrittweise zur Verfügung stellen
<!--1358578-->
Konfigurieren Sie ab Version 1806 diese Einstellung für das Rollout so, dass es in jeder Phase schrittweise erfolgt. Dieses Verhalten mindert das Risiko von Bereitstellungsproblemen und verringert die Belastung des Netzwerks durch die Verteilung von Inhalten an Clients. Der Standort stellt die Software abhängig von der Konfiguration der einzelnen Phasen nach und nach zur Verfügung. Für jeden Client in einer Phase gilt eine zu dem Zeitpunkt, zu dem die Software zur Verfügung gestellt wird, relative Frist. Das Zeitfenster zwischen dem Zeitpunkt der Verfügbarkeit und der Frist ist für alle Clients in einer Phase identisch. Der Standardwert für diese Einstellung ist 0 (null), sodass die Bereitstellung standardmäßig nicht gedrosselt wird. Legen Sie keinen Wert fest, der 30 übersteigt.<!--SCCMDocs-pr issue 2767--> 

![Kriterien der stufenweisen Bereitstellung für Erfolgseinstellungen](media/phased-deployment-criteria-for-success.png)

#### <a name="configure-the-deadline-behavior-relative-to-when-the-software-is-made-available"></a>Konfigurieren des Verhaltens am Stichtag relativ zu dem Zeitpunkt, an dem die Software zur Verfügung gestellt wird  

- **Installation ist so schnell wie möglich erforderlich:** Hiermit wird festgelegt, dass die Software installiert wird, sobald ein Gerät bestimmt wird.  

- **Installation ist nach dieser Zeitspanne erforderlich:** Legt die Frist der Installation auf eine bestimmte Anzahl von Tagen nach der Bestimmung des Geräts fest. Dieser Wert ist standardmäßig auf sieben Tage festgelegt.   


<!--### Examples
Include a timeline diagram
-->



## <a name="automatically-create-a-default-two-phase-deployment"></a><a name="bkmk_auto"></a> Automatisches Erstellen einer 2-Phasen-Standardbereitstellung

1. Starten Sie den Assistenten zum Erstellen der stufenweisen Bereitstellung über die Configuration Manager-Konsole. Diese Aktion variiert je nach Typ der Software, die Sie bereitstellen:  

    - **Anwendung** (nur in der Version 1806 oder höher): Wechseln Sie zur **Softwarebibliothek**, und erweitern Sie **Anwendungsverwaltung**, und wählen Sie dann **Anwendungen** aus. Wählen Sie eine vorhandene Anwendung aus, und klicken Sie dann im Menüband auf **Stufenweise Bereitstellung erstellen**.  

    - **Softwareupdate** (nur in der Version 1810 oder höher): Wechseln Sie zur **Softwarebibliothek**, und erweitern Sie **Softwareupdates**, und wählen Sie dann **Softwareupdates** aus. Wählen Sie mindestens ein Update aus, und klicken Sie dann im Menüband auf **Stufenweise Bereitstellung erstellen**.  

        Diese Aktion steht für Softwareupdates über die folgenden Knoten zur Verfügung:  
        - Softwareupdates  
            - **Alle Softwareupdates**  
            - **Softwareupdategruppen**   
        - Windows 10-Wartung, **Alle Windows 10-Updates**  
        - Office 365-Clientverwaltung, **Office 365-Updates**  

    - **Tasksequenz**: Rufen Sie den Arbeitsbereich **Softwarebibliothek** auf, erweitern Sie **Betriebssysteme**, und wählen Sie dann **Tasksequenzen** aus. Wählen Sie eine vorhandene Tasksequenz aus, und klicken Sie dann im Menüband auf **Stufenweise Bereitstellung erstellen**.  

2. Vergeben Sie auf der Seite **Allgemein** einen **Namen** für die stufenweise Bereitstellung, fügen Sie (optional) eine **Beschreibung** hinzu, und klicken Sie auf **Automatisch 2-Phasen-Standardbereitstellung erstellen**.  

3. Klicken Sie auf **Durchsuchen**, und wählen Sie eine Zielsammlung für die Felder **Erste Sammlung** und **Zweite Sammlung** aus. Wählen Sie für eine Tasksequenz und für Softwareupdates aus Gerätesammlungen aus. Wählen Sie für eine Anwendung aus Benutzer- oder Gerätesammlungen aus. Wählen Sie **Weiter** aus.  

    > [!Important]  
    > Der Assistent zum Erstellen der stufenweisen Bereitstellung benachrichtigt Sie nicht, wenn eine Bereitstellung möglicherweise einem hohen Risiko ausgesetzt ist. Weitere Informationen finden Sie unter [Settings to manage high-risk deployments (Einstellungen zum Verwalten von Bereitstellungen mit hohem Risiko)](../../core/servers/manage/settings-to-manage-high-risk-deployments.md) und im Hinweis beim [Bereitstellen einer Tasksequenz](deploy-a-task-sequence.md).  

4. Wählen Sie auf der Seite **Einstellungen** für jede Einstellung des Zeitplans eine Option aus. Weitere Informationen finden Sie unter [Einstellungen für Phasen](#bkmk_settings). Wenn Sie fertig sind, klicken Sie auf **Weiter**.  

5. Die zwei Phasen, die der Assistent für die angegebenen Sammlungen erstellt, finden Sie auf der Seite **Phasen**. Wählen Sie **Weiter** aus. In diesen Anweisungen wird der Vorgang zum automatischen Erstellen einer Standardbereitstellung in zwei Phasen behandelt. Mit dem Assistent können Sie Phasen für eine stufenweise Bereitstellung hinzufügen, entfernen, neu anordnen, bearbeiten oder anzeigen. Weitere Informationen zu diesen zusätzlichen Aktionen finden Sie unter [Erstellen einer stufenweisen Bereitstellung mit manuell konfigurierten Phasen](#bkmk_manual).  

6. Bestätigen Sie Ihre Auswahl auf der Registerkarte **Zusammenfassung**, und klicken Sie auf **Weiter**, um den Assistenten abzuschließen.  

> [!NOTE]
> Ab dem 21. April 2020 wird Office 365 ProPlus in **Microsoft 365 Apps for Enterprise** umbenannt. Weitere Informationen finden Sie unter [Namensänderung für Office 365 ProPlus](/deployoffice/name-change). Möglicherweise finden Sie während des Updates der Konsole den alten Namen noch im Produkt Configuration Manager und der unterstützenden Dokumentation.  

## <a name="create-a-phased-deployment-with-manually-configured-phases"></a><a name="bkmk_manual"></a> Erstellen einer stufenweisen Bereitstellung mit manuell konfigurierten Phasen
<!--1358148--> 

Erstellen Sie ab Version 1806 eine stufenweise Bereitstellung mit manuell konfigurierten Phasen für eine Tasksequenz. Fügen Sie bis zu 10 weitere Phasen aus der Registerkarte **Phasen** des Assistenten zum Erstellen der stufenweisen Bereitstellung hinzu. 

> [!Note]  
> Derzeit können Sie Phasen für eine Anwendung nicht manuell erstellen. Der Assistent erstellt automatisch zwei Phasen für Bereitstellungen von Anwendungen.


1. Starten Sie den Assistenten zum Erstellen der stufenweisen Bereitstellung entweder für eine Tasksequenz oder für Softwareupdates.  

2. Geben auf der Seite **Allgemein** des Assistenten zum Erstellen der stufenweisen Bereitstellung einen **Namen** und eine (optionale) **Beschreibung** für die stufenweise Bereitstellung ein, und wählen Sie die Option **Alle Phasen manuell konfigurieren** aus.  

3. Auf der Seite **Phasen** des Assistenten zum Erstellen der stufenweisen Bereitstellung sind die folgenden Aktionen verfügbar:  

    - **Filtern** der Liste von Bereitstellungsphasen. Geben Sie eine Zeichenfolge ein, um ohne Beachtung der Groß-/Kleinschreibung nach einer Übereinstimmung mit den Spalten Reihenfolge, Name oder Sammlung suchen. 

    - **Hinzufügen** einer neuen Phase:  

        1. Geben Sie auf der Seite **Allgemein** des Assistenten zum Hinzufügen von Phasen einen **Namen** für die Phase ein, und navigieren Sie zum Ziel **Phasensammlung**. Die zusätzlichen Einstellungen auf dieser Seite sind identisch mit der herkömmlichen Bereitstellung einer Tasksequenz oder von Softwareupdates.  

        2. Konfigurieren Sie die Zeitplaneinstellungen auf der Seite **Phaseneinstellungen** des Assistenten zum Hinzufügen von Phasen, und klicken Sie anschließend auf **Weiter**. Weitere Informationen finden Sie unter [Einstellungen](#bkmk_settings).   

            > [!Note]  
            > In der ersten Phase können Sie die Phaseneinstellungen (**Bereitstellungserfolg in Prozent** bzw. **Anzahl erfolgreich bereitgestellter Geräte** (ab Version 1902)) nicht bearbeiten. Diese Einstellung gilt nur für Phasen, die auf eine vorherige Phase folgen.  

        3. Die Einstellungen auf den Seiten **Benutzerfreundlichkeit** und **Verteilungspunkte** des Assistenten zum Hinzufügen von Phasen sind identisch mit der herkömmlichen Bereitstellung einer Tasksequenz oder von Softwareupdates.  

        4. Überprüfen Sie die Einstellungen auf der Seite **Zusammenfassung**, und schließen Sie dann den Assistenten zum Hinzufügen von Phasen ab.  

    - **Bearbeiten:** Diese Aktion öffnet das Eigenschaftenfenster der ausgewählten Phase, das über die gleichen Registerkarten wie die Seiten des Assistenten zum Hinzufügen von Phasen verfügt.  

    - **Entfernen:** Diese Aktion löscht die ausgewählte Phase.  

       > [!Warning]  
       > Diese Aktion fordert Sie nicht zur Bestätigung auf und kann nicht Rückgängig gemacht werden.  

    - **Nach oben** oder **Nach unten**: Der Assistent ordnet die Phasen in der Reihenfolge an, in der Sie sie hinzufügen. Die zuletzt hinzugefügte Phase ist die letzte Phase in der Liste. Wählen Sie eine Phase aus, und klicken Sie auf eine dieser Schaltflächen, um die Phase in der Liste zu verschieben.  

       > [!Important]  
       > Überprüfen Sie die Phaseneinstellungen, nachdem Sie die Reihenfolge geändert haben. Stellen Sie sicher, dass die folgenden Einstellungen weiterhin mit Ihren Anforderungen für diese stufenweise Bereitstellung übereinstimmen:  
       > 
       > - Kriterien für den Erfolg der vorherigen Phase  
       > - Bedingungen für den Start dieser Bereitstellungsphase nach dem erfolgreichen Abschluss der vorherigen Phase   

5. Wählen Sie **Weiter** aus. Überprüfen Sie die Einstellungen auf der Seite **Zusammenfassung**, und schließen Sie dann den Assistenten zum Erstellen der stufenweisen Bereitstellung ab.  


Nachdem Sie eine stufenweise Bereitstellung erstellt haben, öffnen Sie die Eigenschaften, um Änderungen vorzunehmen:  

- Zusätzliche Phasen zu einer vorhandenen stufenweisen Bereitstellung **hinzufügen**.  

- Wenn eine Phase nicht aktiv ist, können Sie sie **bearbeiten**, **entfernen** oder nach oben oder unten **verschieben**. Sie können sie nicht vor eine aktive Phase verschieben.  

- Wenn eine Phase aktiv ist, ist diese schreibgeschützt. Sie können sie nicht bearbeiten, entfernen oder in der Liste verschieben. Die einzige verfügbare Option ist die Eigenschaften der Phase **anzuzeigen**.  

- Die stufenweise Bereitstellung einer Anwendung ist immer schreibgeschützt.  



## <a name="next-steps"></a>Nächste Schritte

Verwalten und Überwachen von stufenweisen Bereitstellungen:
- [Anwendung](manage-monitor-phased-deployments.md?toc=/mem/configmgr/apps/toc.json&bc=/mem/configmgr/apps/breadcrumb/toc.json)
- [Softwareupdate](manage-monitor-phased-deployments.md?toc=/mem/configmgr/sum/toc.json&bc=/mem/configmgr/sum/breadcrumb/toc.json)  
- [Tasksequenz](manage-monitor-phased-deployments.md)  

