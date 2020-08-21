---
title: Erstellen einer Tasksequenz für Nicht-Betriebssystembereitstellungen
titleSuffix: Configuration Manager
description: Erstellen Sie Tasksequenzen, die nicht für die Bereitstellung eines Betriebssystems gedacht sind, um beispielsweise Software zu verteilen oder Tasks zu automatisieren.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1c5ef6d4a17623428f299ff9df676dcba49e7f0c
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88698152"
---
# <a name="create-a-task-sequence-for-non-os-deployments"></a>Erstellen einer Tasksequenz für Nicht-Betriebssystembereitstellungen

*Gilt für: Configuration Manager (Current Branch)*

Mithilfe von Tasksequenzen in Configuration Manager können Sie verschiedene Arten von Aufgaben in Ihrer Umgebung automatisieren. Diese Tasks wurden in erster Linie für die Bereitstellung von Betriebssystemen konzipiert und getestet. Configuration Manager bietet zahlreiche weitere Features, die in folgenden Szenarien als primäre Technologie verwendet werden sollten:

- [Anwendungsinstallation](../../apps/understand/introduction-to-application-management.md)

    > [!NOTE]
    > Ab Version 2002 können Sie komplexe Anwendungen mithilfe von Tasksequenzen über das Anwendungsmodell installieren. Fügen Sie einer App einen Bereitstellungstyp hinzu, der eine Tasksequenz ist, um die App entweder zu installieren oder zu deinstallieren. Weitere Informationen finden Sie unter [Erstellen von Windows-Anwendungen](../../apps/get-started/creating-windows-applications.md#bkmk_tsdt).<!-- 3555953 -->

- [Installation von Softwareupdates](../../sum/understand/software-updates-introduction.md)

- [Konfiguration von Einstellungen](../../compliance/understand/ensure-device-compliance.md)

Darüber hinaus stehen noch weitere Microsoft System Center-Automatisierungstechnologien wie [Orchestrator](/system-center/orchestrator/) und [Service Management Automation](/system-center/sma/) zur Verfügung.  

Die Stärke von Tasksequenzen liegt in ihrer Flexibilität und Verwendung. Sie eignen sich zum Konfigurieren von Clienteinstellungen, zum Verteilen von Software, zum Aktualisieren von Treibern, zum Bearbeiten von Benutzerzuständen sowie für andere Aufgaben (unabhängig von der Betriebssystembereitstellung). Sie können eine benutzerdefinierte Tasksequenz erstellen, der Sie beliebig viele Tasks hinzufügen können. In Configuration Manager wird die Verwendung benutzerdefinierter Tasksequenzen für betriebssystemfremde Bereitstellungen unterstützt. Sollte eine Tasksequenz jedoch ungewollte oder inkonsistente Ergebnisse liefern, versuchen Sie, den Vorgang zu vereinfachen:

- Verwenden Sie einfachere Schritte.
- Teilen Sie die Aktionen auf mehrere Tasksequenzen auf.
- Erstellen und testen Sie die Tasksequenz phasenweise.

## <a name="supported-steps"></a>Unterstützte Schritte

In einer benutzerdefinierten Tasksequenz, die nicht für die Bereitstellung eines Betriebssystems gedacht ist, werden folgende Schritte unterstützt:  

- [Bereitschaft überprüfen](../understand/task-sequence-steps.md#BKMK_CheckReadiness)  

- [Verbindung mit Netzwerkordner herstellen](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  

- [Paketinhalt herunterladen](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)  

- [Anwendung installieren](../understand/task-sequence-steps.md#BKMK_InstallApplication)  

- [Paket installieren](../understand/task-sequence-steps.md#BKMK_InstallPackage)  

- [Softwareupdates installieren](../understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

- [Computer neu starten](../understand/task-sequence-steps.md#BKMK_RestartComputer)  

- [Befehlszeile ausführen](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

- [PowerShell-Skript ausführen](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)  

- [Tasksequenz ausführen](../understand/task-sequence-steps.md#child-task-sequence)  

- [Dynamische Variablen festlegen](../understand/task-sequence-steps.md#BKMK_SetDynamicVariables)  

- [Tasksequenzvariable festlegen](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)  

## <a name="next-steps"></a>Nächste Schritte

[Erstellen einer benutzerdefinierten Tasksequenz](create-a-custom-task-sequence.md)