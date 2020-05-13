---
title: 'Anpassen von Betriebssystemabbildern '
titleSuffix: Configuration Manager
description: Verwenden Sie die Tasksequenzen zum Erfassen und Erstellen, die manuelle Konfiguration oder eine Kombination aus beidem, um ein Betriebssystemimage anzupassen.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 95033a9b-ff13-4b70-b1de-bcb25bcb6024
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 652a0c5e36ce7c4bacf40531a82fdf4e16197d95
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906915"
---
# <a name="customize-operating-system-images-with-configuration-manager"></a>Anpassen von Betriebssystemimages mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Betriebssystemimages in Configuration Manager sind WIM-Dateien und stellen eine komprimierte Sammlung von Referenzdateien und -ordnern dar, die für die erfolgreiche Installation und Konfiguration eines Betriebssystems auf einem Computer erforderlich sind. Ein benutzerdefiniertes Betriebssystemabbild wird von einem Referenzcomputer erstellt und erfasst, den Sie mit allen erforderlichen Betriebssystemdateien, Unterstützungsdateien, Softwareupdates, Tools und sonstigen Softwareapps konfigurieren. Sie entscheiden, in welchem Umfang der Referenzcomputer manuell konfiguriert wird. Mithilfe einer Tasksequenz zum Erstellen und Erfassen können Sie die Konfiguration des Referenzcomputers vollständig automatisieren. Alternativ konfigurieren Sie bestimmte Aspekte des Referenzcomputers manuell und automatisieren dann den Rest, indem Sie Tasksequenzen verwenden, oder Sie konfigurieren Referenzcomputer ohne Tasksequenzen vollständig manuell. Folgende Abschnitte bieten Informationen zum Anpassen eines Betriebssystems.

##  <a name="prepare-for-the--reference-computer"></a><a name="BKMK_PrepareReferenceComputer"></a> Vorbereiten des Referenzcomputers  
 Bevor Sie ein Betriebssystemabbild von einem Referenzcomputer erfassen, müssen einige Punkte bedacht werden.  

###  <a name="decide-between-an-automated-or-manual-configuration"></a><a name="BKMK_RefComputerDecide"></a> Entscheiden zwischen automatisierter oder manueller Konfiguration  
 Im Folgenden werden die Vor- und Nachteile der automatischen und manuellen Konfiguration des Referenzcomputers dargestellt:  

#### <a name="automated-configuration"></a>Automatische Konfiguration  
 **Vorteile**  

- Die Konfiguration kann vollkommen unbeaufsichtigt erfolgen, sodass kein Administrator oder Benutzer anwesend sein muss.  

- Sie können die Tasksequenz wiederverwenden, um die Konfiguration zusätzlicher Referenzcomputer mit einem hohen Maß an Zuverlässigkeit zu wiederholen.  

- Sie können die Tasksequenz ändern, um Unterschiede bei Referenzcomputern zu berücksichtigen. Eine erneute Erstellung der gesamten Tasksequenz ist nicht nötig.  

  **Nachteile**  

- Das erste Erstellen und Testen einer Tasksequenz kann sehr lange dauern.  

- Wenn sich die Anforderungen des Referenzcomputers erheblich ändern, kann das erneute Erstellen und Testen der Tasksequenz ebenfalls viel Zeit in Anspruch nehmen.  

#### <a name="manual-configuration"></a>Manuelle Konfiguration  
 **Vorteile**  

- Sie brauchen keine Tasksequenz zu erstellen, und der Zeitaufwand für Tests und die Problembehandlung für die Tasksequenz entfällt.  

- Die Installation kann direkt von den CDs erfolgen, ohne alle Softwarepakete (einschließlich Windows selbst) in ein Configuration Manager-Paket zu integrieren.  

  **Nachteile**  

- Die Genauigkeit der Konfiguration des Referenzcomputers wird durch den Administrator oder Benutzer vorgegeben, der den Computer konfiguriert.  

- Sich müssen weiterhin überprüfen und testen, ob der Referenzcomputer ordnungsgemäß konfiguriert ist.  

- Sie können die Konfigurationsmethode nicht wiederverwenden.  

- Erfordert eine Person, die aktiv am gesamten Prozess beteiligt ist.  

###  <a name="considerations-for-the-reference-computer"></a><a name="BKMK_RefComputerConsiderations"></a> Überlegungen zum Referenzcomputer  
 Im Folgenden werden die grundlegenden Punkte aufgezeigt, die Sie bei der Konfiguration eines Referenzcomputers beachten müssen.  

-   **Bereitzustellendes Betriebssystem**  

     Auf dem Referenzcomputer muss das Betriebssystem installiert sein, das Sie auf Ihren Zielcomputern bereitstellen möchten. Weitere Informationen zu den Betriebssystemen, die Sie bereitstellen können, finden Sie unter [Anforderungen an die Infrastruktur für die Betriebssystembereitstellung](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

-   **Mit dem entsprechenden Service Pack**  

     Auf dem Referenzcomputer muss das Betriebssystem installiert sein, das Sie auf Ihren Zielcomputern bereitstellen möchten.  

-   **Mit den entsprechenden Softwareupdates**  

     Installieren Sie alle Softwareanwendungen, die in das vom Referenzcomputer zu erfassende Betriebssystemabbild eingeschlossen werden sollen. Sie können Softwareanwendungen auch bei der Bereitstellung eines Betriebssystemabbilds auf Ihren Zielcomputern installieren.  

-   **Mitgliedschaft in einer Arbeitsgruppe**  

     Der Referenzcomputer muss als Mitglied einer Arbeitsgruppe konfiguriert sein.  

-   **Sysprep**  

     Das Tool für die Systemvorbereitung (Sysprep) ist eine Technologie, die Sie in Verbindung mit anderen Bereitstellungstools zum Installieren von Windows-Betriebssystemen auf neuer Hardware verwenden können. Mithilfe von Sysprep wird ein Computer für die Erstellung eines Festplattenabbilds oder für die Bereitstellung für einen Kunden vorbereitet, indem der Computer so konfiguriert wird, dass beim Neustart des Computers eine neue Sicherheitskennung (SID) erstellt wird. Außerdem werden mit Sysprep benutzer- und computerspezifische Einstellungen und Daten bereinigt, die nicht auf den Zielcomputer kopiert werden dürfen.  

     Sie können Sysprep mithilfe des folgenden Befehls manuell auf dem Referenzcomputer ausführen:  

     `Sysprep /quiet /generalize /reboot`  

     Die /generalize-Option bewirkt, dass Sysprep systemspezifische Daten aus der Windows-Installation entfernt. Systemspezifische Daten sind Ereignisprotokolle, eindeutige Sicherheits-IDs (SIDs) und weitere eindeutige Informationen. Nachdem die eindeutigen Systeminformationen entfernt wurden, wird der Computer neu gestartet.  

     Sie können Sysprep mithilfe des Tasksequenzschritts [Prepare Windows for Capture](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture) oder mithilfe von Erfassungsmedien automatisieren.  

    > [!IMPORTANT]  
    >  Im Tasksequenzschritt [Prepare Windows for Capture](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture) wird versucht, das lokale Administratorkennwort auf dem Referenzcomputer vor der Ausführung von Sysprep auf einen leeren Wert zurückzusetzen. Wenn die lokale Sicherheitsrichtlinie **Kennwort muss Komplexitätsvoraussetzungen entsprechen** aktiviert ist, kann das Administratorkennwort nicht von diesem Tasksequenzschritt zurückgesetzt werden. Deaktivieren Sie in diesem Fall die Richtlinie, bevor Sie die Tasksequenz ausführen.  

     Weitere Informationen zu Sysprep finden Sie unter [Sysprep (Systemvorbereitung) – Übersicht](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--system-preparation--overview).  

-   **Mit den entsprechenden erforderlichen Tools und Skripts für die Installationsszenarien**  

     Mit den entsprechenden erforderlichen Tools und Skripts für die Installationsszenarien  

-   **Mit der entsprechenden Desktopanpassung (Hintergrundbild, Branding, Standardbenutzerprofil)**  

     Sie können den Referenzcomputer mit entsprechenden benutzerdefinierten Desktopeigenschaften konfigurieren, die beim Erfassen des Betriebssystemabbilds vom Referenzcomputer berücksichtigt werden sollen. Zu den Desktopeigenschaften zählen Hintergrundbild, Branding und ein Standardbenutzerprofil.  

##  <a name="manually-build-a-reference-computer"></a><a name="BKMK_ManuallyBuildReference"></a> Manuelles Erstellen eines Referenzcomputers  
 Gehen Sie wie folgt vor, um einen Referenzcomputer manuell zu erstellen.  

> [!NOTE]  
>  Wenn Sie den Referenzcomputer manuell erstellen, können Sie das Betriebssystemabbild mithilfe von Erfassungsmedien erfassen. Weitere Informationen finden Sie unter [Erstellen von Erfassungsmedien](../deploy-use/create-capture-media.md).  

#### <a name="to-manually-build-the-reference-computer"></a>So erstellen Sie den Referenzcomputer manuell  

1. Identifizieren Sie den Computer, der als Referenzcomputer verwendet werden soll.  

2. Konfigurieren Sie den Referenzcomputer mit dem geeigneten Betriebssystem sowie weiterer Software, die zum Erstellen des bereitzustellenden Betriebssystemabbilds erforderlich ist.  

   > [!WARNING]  
   >  Installieren Sie mindestens das entsprechende Betriebssystem und Service Pack, die Supporttreiber und die erforderlichen Softwareupdates.  

3. Konfigurieren Sie den Referenzcomputer als Mitglied einer Arbeitsgruppe.  

4. Setzen Sie das lokale Administratorkennwort auf dem Referenzcomputer zurück, sodass es leer ist.  

5. Führen Sie Sysprep mithilfe des folgenden Befehls aus:  **sysprep /quiet /generalize /reboot**. Die /generalize-Option bewirkt, dass Sysprep systemspezifische Daten aus der Windows-Installation entfernt. Systemspezifische Daten sind Ereignisprotokolle, eindeutige Sicherheits-IDs (SIDs) und weitere eindeutige Informationen. Nachdem die eindeutigen Systeminformationen entfernt wurden, wird der Computer neu gestartet.  

   Sobald der Referenzcomputer bereit ist, erfassen Sie mithilfe einer Tasksequenz das Betriebssystemabbild vom Referenzcomputer.  Detaillierte Anweisungen finden Sie unter [Erfassen eines Betriebssystemabbilds von einem vorhandenen Referenzcomputer](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md#BKMK_CaptureExistingRefComputer).  

##  <a name="use-a-task-sequence-to-build-a-reference-computer"></a><a name="BKMK_UseTSToBuildReference"></a> Verwenden einer Tasksequenz zum Erstellen eines Referenzcomputers  
 Sie können den Prozess zum Erstellen eines Referenzcomputers automatisieren, indem Sie mithilfe einer Tasksequenz das Betriebssystem, Treiber, Anwendungen usw. bereitstellen.  Führen Sie die folgenden Schritte aus, um den Referenzcomputer zu erstellen, von dem Sie anschließend das Betriebssystemabbild erfassen.  

-   Nutzen Sie eine Tasksequenz zum Erstellen und Erfassen des Betriebssystemabbilds vom Referenzcomputer.  Eine Schritt-für-Schritt-Anleitung finden Sie unter [Verwenden einer Tasksequenz zum Erstellen und Erfassen eines Referenzcomputers](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md#BKMK_BuildCaptureTS).  
