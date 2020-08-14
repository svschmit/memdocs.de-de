---
title: Erfassen und Wiederherstellen des Benutzerstatus
titleSuffix: Configuration Manager
description: Mit den Configuration Manager-Tasksequenzen können Sie Benutzerstatusdaten in Betriebssystembereitstellungs-Szenarien erfassen und wiederherstellen.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: d566d85c-bf7a-40e7-8239-57640a1db5f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6a1f11c46689b213b795c0d71221728f916a68bb
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125490"
---
# <a name="create-a-task-sequence-to-capture-and-restore-user-state-in-configuration-manager"></a>Erstellen einer Tasksequenz zum Erfassen und Wiederherstellen eines Benutzerstatus in Configuration Manager

 *Gilt für: Configuration Manager (Current Branch)*

 Mit den Configuration Manager-Tasksequenzen können Sie Benutzerstatusdaten in Betriebssystembereitstellungs-Szenarien erfassen und wiederherstellen. In diesen Szenarien erfahren Sie, wie Sie den Benutzerstatus des aktuellen Betriebssystems beibehalten. Je nach Art der erstellten Tasksequenz werden die Schritte zum Erfassen und Wiederherstellen möglicherweise automatisch zur Tasksequenz hinzugefügt. In anderen Szenarien müssen Sie die Schritte zum Erfassen und Wiederherstellen möglicherweise manuell zur Tasksequenz hinzufügen. Dieser Artikel enthält die Schritte, die Sie einer vorhandenen Tasksequenz hinzufügen müssen, um Benutzerstatusdaten zu erfassen und wiederherzustellen.  



## <a name="task-sequence-steps"></a>Tasksequenzschritte  

Fügen Sie der Tasksequenz die folgenden Schritte hinzu, um den Benutzerstatus zu erfassen und wiederherzustellen:  

- [Statusspeicher anfordern:](../understand/task-sequence-steps.md#BKMK_RequestStateStore) Dieser Schritt ist erforderlich, wenn Sie den Benutzerstatus auf dem Zustandsmigrationspunkt speichern.  

- [Benutzerstatus erfassen:](../understand/task-sequence-steps.md#BKMK_CaptureUserState) Bei diesem Schritt werden die Benutzerstatusdaten erfasst. Anschließend werden die Daten entweder auf dem Zustandsmigrationspunkt oder auf dem lokalen Datenträger über feste Links gespeichert.  

- [Benutzerstatus wiederherstellen:](../understand/task-sequence-steps.md#BKMK_RestoreUserState) Mit diesem Schritt werden die Benutzerzustandsdaten auf dem Zielcomputer wiederhergestellt. Die Daten lassen sich aus einem Zustandsmigrationspunkt oder – falls ein fester Link vorhanden ist – aus einem lokalen Datenträger abrufen.  

- [Statusspeicher freigeben:](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore) Dieser Schritt ist erforderlich, wenn Sie den Benutzerstatus auf dem Zustandsmigrationspunkt speichern. Bei diesem Schritt werden die Daten aus dem Zustandsmigrationspunkt entfernt.  


 Gehen Sie wie folgt vor, um die zum Erfassen und Wiederherstellen des Benutzerstatus erforderlichen Tasksequenzschritte hinzuzufügen. Weitere Informationen zum Erstellen von Tasksequenzen finden Sie unter [Verwalten von Tasksequenzen zum Automatisieren von Aufgaben](manage-task-sequences-to-automate-tasks.md).  



## <a name="capture-the-user-state"></a>Erfassen des Benutzerstatus  

 Mithilfe der folgenden Anleitung können Sie Tasksequenzschritte zum Erfassen des Benutzerstatus hinzufügen:

1.  Wählen Sie in der Liste **Tasksequenz** eine Tasksequenz aus, und klicken Sie dann auf **Bearbeiten**.  

2.  Wenn Sie einen Zustandsmigrationspunkt zum Speichern des Benutzerstatus verwenden, fügen Sie der Tasksequenz den Schritt **Statusspeicher anfordern** hinzu. Klicken Sie im **Tasksequenz-Editor** auf **Hinzufügen**. Zeigen Sie auf **Benutzerstatus**, und klicken Sie dann auf **Statusspeicher anfordern**. Konfigurieren Sie die Eigenschaften und die Optionen für diesen Schritt, und klicken Sie dann auf **Übernehmen**. Weitere Informationen zu den verfügbaren Einstellungen finden Sie unter [Statusspeicher anfordern](../understand/task-sequence-steps.md#BKMK_RequestStateStore).  

3.  Fügen Sie der Tasksequenz den Schritt **Benutzerzustand erfassen** hinzu. Klicken Sie im **Tasksequenz-Editor** auf **Hinzufügen**. Zeigen Sie auf **Benutzerstatus**, und klicken Sie dann auf **Benutzerstatus erfassen**. Konfigurieren Sie die Eigenschaften und die Optionen für diesen Schritt, und klicken Sie dann auf **Übernehmen**. Weitere Informationen zu den verfügbaren Einstellungen finden Sie unter [Benutzerstatus erfassen](../understand/task-sequence-steps.md#BKMK_CaptureUserState).  

    > [!IMPORTANT]  
    >  Legen Sie beim Hinzufügen dieses Schritts zur Tasksequenz auch die Tasksequenzvariable **OSDStateStorePath** fest, um den Speicherort der Benutzerstatusdaten anzugeben. Wenn Sie den Benutzerstatus lokal speichern, geben Sie keinen Stammordner an, da dies dazu führen kann, dass für die Tasksequenz ein Fehler auftritt. Verwenden Sie immer einen Ordner oder Unterordner, wenn Sie die Benutzerdaten lokal speichern. Weitere Informationen zu dieser Variablen finden Sie unter [Tasksequenzvariablen](../understand/task-sequence-variables.md#OSDStateStorePath).  

4.  Wenn Sie einen Zustandsmigrationspunkt verwenden, fügen Sie der Tasksequenz den Schritt **Statusspeicher freigeben** hinzu. Klicken Sie im **Tasksequenz-Editor** auf **Hinzufügen**. Zeigen Sie auf **Benutzerstatus**, und klicken Sie dann auf **Statusspeicher freigeben**. Konfigurieren Sie die Eigenschaften und die Optionen für diesen Schritt, und klicken Sie dann auf **Übernehmen**. Weitere Informationen zu den verfügbaren Einstellungen finden Sie unter [Statusspeicher freigeben](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore).  

    > [!IMPORTANT]  
    >  Die Tasksequenzaktion, die vor dem Schritt **Statusspeicher freigeben** ausgeführt wird, muss erfolgreich sein, bevor der Schritt **Statusspeicher freigeben** gestartet wird.  


 Stellen Sie diese Tasksequenz bereit, um den Benutzerzustand auf einem Zielcomputer zu erfassen. Informationen zum Bereitstellen von Tasksequenzen finden Sie unter [Tasksequenz bereitstellen](deploy-a-task-sequence.md).  



## <a name="restore-the-user-state"></a>Wiederherstellen des Benutzerstatus  

 Mithilfe der folgenden Anleitung können Sie Tasksequenzschritte zum Wiederherstellen des Benutzerstatus hinzufügen:

1. Wählen Sie in der Liste **Tasksequenz** eine Tasksequenz aus, und klicken Sie dann auf **Bearbeiten**.  

2. Fügen Sie den Schritt **Benutzerzustand wiederherstellen** zur Tasksequenz hinzu. Klicken Sie im **Tasksequenz-Editor** auf **Hinzufügen**. Zeigen Sie auf **Benutzerstatus**, und klicken Sie dann auf **Benutzerstatus wiederherstellen**. Durch diesen Schritt wird bei Bedarf eine Verbindung mit dem Zustandsmigrationspunkt hergestellt. Konfigurieren Sie die Eigenschaften und die Optionen für diesen Schritt, und klicken Sie dann auf **Übernehmen**. Weitere Informationen zu den verfügbaren Einstellungen finden Sie unter [Benutzerstatus wiederherstellen](../understand/task-sequence-steps.md#BKMK_RestoreUserState).  

   > [!Important]  
   >  Wenn Sie den Schritt [Benutzerstatus erfassen](../understand/task-sequence-steps.md#BKMK_CaptureUserState) mit der Option **Alle Benutzerprofile mit Standardoptionen erfassen** verwenden, wählen Sie in Schritt **Benutzerstatus wiederherstellen** die Einstellung **Lokale Computerbenutzerprofile wiederherstellen** aus. Andernfalls tritt ein Fehler für die Tasksequenz auf.  

   > [!Note]  
   > Wenn Sie den Benutzerstatus über lokale feste Links speichern und die Wiederherstellung nicht erfolgreich ist, können Sie die festen Links manuell löschen, die zum Speichern der Daten erstellt wurden. Die Tasksequenz kann das USMTUtils-Tool ausführen, um diese Aktion mit dem Schritt [Befehlszeile ausführen](../understand/task-sequence-steps.md#BKMK_RunCommandLine) zu automatisieren. Wenn Sie feste Links mit USMTUtils löschen, fügen Sie nach dem Ausführen von USMTUtils den Schritt [Computer neu starten](../understand/task-sequence-steps.md#BKMK_RestartComputer) hinzu.  

3. Wenn Sie einen Zustandsmigrationspunkt zum Speichern des Benutzerstatus verwenden, fügen Sie der Tasksequenz den Schritt **Statusspeicher freigeben** hinzu. Klicken Sie im **Tasksequenz-Editor** auf **Hinzufügen**. Zeigen Sie auf **Benutzerstatus**, und klicken Sie dann auf **Statusspeicher freigeben**. Konfigurieren Sie die Eigenschaften und die Optionen für diesen Schritt, und klicken Sie dann auf **Übernehmen**. Weitere Informationen zu den verfügbaren Einstellungen finden Sie unter [Statusspeicher freigeben](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore).  

   > [!IMPORTANT]  
   >  Die Tasksequenzaktion, die vor dem Schritt **Statusspeicher freigeben** ausgeführt wird, muss erfolgreich sein, bevor der Schritt **Statusspeicher freigeben** gestartet wird.  


 Stellen Sie diese Tasksequenz bereit, um den Benutzerzustand auf einem Zielcomputer wiederherzustellen. Informationen zum Bereitstellen von Tasksequenzen finden Sie unter [Bereitstellen einer Tasksequenz](deploy-a-task-sequence.md).  



## <a name="next-steps"></a>Nächste Schritte

[Überwachen der Tasksequenzbereitstellung](monitor-operating-system-deployments.md#BKMK_TSDeployStatus)
