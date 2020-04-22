---
title: Verwenden von Wartungsfenstern
titleSuffix: Configuration Manager
description: Verwenden Sie Sammlungen und Wartungsfenster zur effektiven Veraltung von Clients in Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4564ebcb-41a8-4eb0-afdb-2e1f0795cfa2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6c2128c9e26137c268577e68e5ee12e3a71f8513
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695458"
---
# <a name="how-to-use-maintenance-windows-in-configuration-manager"></a>Verwenden von Wartungsfenstern in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Mithilfe von Wartungsfenstern können Sie einen Zeitpunkt definieren, an dem Configuration Manager-Vorgänge auf einer Gerätesammlung durchgeführt werden können. Sie verwenden die Wartungsfenster, um Konfigurationsänderungen bei den Clients dann vorzunehmen, wenn sie die Produktivität nicht beeinträchtigen. Ab Version 1806 von Configuration Manager können Ihre Benutzer sehen, wenn das nächste Wartungsfenster von der Registerkarte **Installationsstatus** im **Softwarecenter** stammt. <!--1358131-->

 Die folgenden Vorgänge unterstützen Wartungsfenster:  

- Softwarebereitstellungen  

- Softwareupdatebereitstellungen  

- Bereitstellen und Bewerten von Kompatibilitätseinstellungen  

- Betriebssystembereitstellungen  

- Tasksequenzbereitstellungen  

  Konfigurieren Sie Wartungsfenster mit einem Startdatum, einer Start- und Endzeit sowie einem Wiederholungsmuster. Die maximale Dauer eines Fensters muss weniger als 24 Stunden betragen. In der Standardeinstellung sind Computerneustarts durch Bereitstellungen außerhalb von Wartungsfenstern nicht zulässig. Sie können die Standardeinstellung jedoch außer Kraft setzen. Wartungsfenster beziehen sich nur auf den Zeitraum, in dem das Bereitstellungsprogramm ausgeführt wird. Von Anwendungen, die für den lokalen Download und die lokale Ausführung konfiguriert sind, können auch außerhalb des Fensters Inhalte heruntergeladen werden.  

  Wenn ein Clientcomputer Mitglied einer Gerätesammlung mit Wartungsfenster ist, wird ein Bereitstellungsprogramm nur dann ausgeführt, wenn die maximal zulässige Laufzeit nicht die Dauer überschreitet, die für das Fenster konfiguriert ist. Kann das Programm nicht ausgeführt werden, wird eine Warnung ausgegeben, und die Bereitstellung wird während des nächsten geplanten Wartungsfensters ausgeführt, das Zeitkapazitäten hat.  

## <a name="using-multiple-maintenance-windows"></a>Verwenden mehrerer Wartungsfenster  
 Wenn ein Clientcomputer Mitglied mehrerer Gerätesammlungen mit Wartungsfenstern ist, gelten die folgenden Regeln:  

- Wenn sich die Wartungsfenster nicht überschneiden, werden sie als zwei unabhängige Wartungsfenster behandelt.  

- Wenn sich die Wartungsfenster überschneiden, werden sie als ein einziges Wartungsfenster behandelt, das den Zeitraum beider Wartungsfenster umfasst. Beispiel: Bei zwei Fenstern von jeweils einer Stunde Dauer, die sich um 30 Minuten überschneiden, beträgt die effektive Dauer des Wartungsfensters 90 Minuten.  

  Wenn ein Benutzer im Softwarecenter eine Anwendungsinstallation initiiert, wird die Anwendung unabhängig von Wartungsfenstern sofort installiert.  

  Wenn die Installationsfrist einer als **erforderlich** eingestuften Anwendungsbereitstellung außerhalb der Geschäftszeiten abläuft, die von einem Benutzer im Softwarecenter konfiguriert wurden, wird die Anwendung installiert. 

### <a name="how-to-configure-maintenance-windows"></a>Konfigurieren von Wartungsfenstern  

1.  Wählen Sie in der Configuration Manager-Konsole **Bestand und Konformität**>  **Gerätesammlungen** aus.  

3.  Wählen Sie in der Liste **Gerätesammlungen** eine Sammlung aus. Es können keine Wartungsfenster für die Sammlung **Alle Systeme** erstellt werden.  

4.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus.  

5.  Wählen Sie auf der Registerkarte **Wartungsfenster** des Dialogfelds **&lt;Sammlungsname\> Eigenschaften** das Symbol **Neu** aus.  

6.  Füllen Sie das Dialogfeld **&lt;neu\> Zeitplan** aus.  

7.  Wählen Sie einen Wert in der Dropdownliste **Diesen Zeitplan anwenden auf** aus.  

8.  Wählen Sie **OK** aus, und schließen Sie dann das Dialogfeld **&lt;Sammlungsname\> Eigenschaften**.  
 
## <a name="using-powershell"></a><a name="bkmk_powershell"></a> Verwenden von PowerShell

PowerShell kann zum Konfigurieren von Wartungsfenstern verwendet werden.  Weitere Informationen finden Sie in folgenden Quellen:

* [Set-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmmaintenancewindow)
* [Get-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmmaintenancewindow)
* [New-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmmaintenancewindow)
* [Remove-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmmaintenancewindow)
