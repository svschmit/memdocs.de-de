---
title: Supportcenter
titleSuffix: Configuration Manager
description: Problembehandlung für Konfigurations-Manager-Clients mithilfe des Supportcenters.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c631197d-7daa-4faa-9e22-980cd6d604c2
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 21279eb2f7d7962d1286d60a599411912d38313a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701318"
---
# <a name="support-center-for-configuration-manager"></a>Supportcenter für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

<!--1357489-->
Verwenden Sie ab Version 1810 das Supportcenter zur Behebung von Clientproblemen, zum Anzeigen von Protokollen in Echtzeit oder zum Erfassen des Zustands eines Konfigurations-Manager-Clientcomputers zur späteren Analyse. Das Supportcenter ist ein einziges Tool, das viele Problembehandlungstools für Administratoren konsolidiert.


## <a name="about"></a>Informationen zu

Durch das Supportcenter soll die Problembehandlung für Konfigurations-Manager-Clientcomputer vereinfacht werden. Bisher mussten Protokolldateien und andere für die Problembehebung nützlichen Informationen im Falle einer Zusammenarbeit mit dem Support bei der Behebung von Problemen mit Konfigurations-Manager-Clients manuell gesammelt werden. So konnte schnell eine wichtige Protokolldatei versehentlich ausgelassen werden, was die Problembehandlung für Sie und die Supportmitarbeitern zusätzlich erschwert hat.

Mit Supportcenter können Sie die Supportabläufe optimieren. Dies ermöglicht Ihnen Folgendes:

- Sie können ein Paket für die Problembehandlung (ZIP-Datei) erstellen, das die Protokolldateien des Konfigurations-Manager-Clients enthält. Sie müssen dann nur eine Datei an den Support senden.  

- Sie können Protokolldateien, Zertifikate, Registrierungseinstellungen, Debugdumps und Clientrichtlinien des Konfigurations-Manager-Clients anzeigen.  

- Sie können eine Diagnose des Inventurcaches (ersetzt ContentSpy), des Richtliniencaches (ersetzt PolicySpy) und des Clientcaches in Echtzeit durchführen.  

### <a name="support-center-viewer"></a>Supportcenteranzeige

Im Supportcenter steht die Supportcenteranzeige zur Verfügung. Mit diesem Tool öffnen die Supportmitarbeiter das Dateipaket, das Sie mit dem Supportcenter erstellt haben. Der Datensammler des Supportcenters sammelt und packt Diagnoseprotokolle von einem lokalen Konfigurations-Manager-Client oder einem Konfigurations-Manager-Remoteclient. Verwenden Sie den Viewer, um die Pakete des Datensammlers anzuzeigen.

### <a name="support-center-log-file-viewer"></a>Protokolldateianzeige des Supportcenters

Im Supportcenter steht eine moderne Protokollanzeige zur Verfügung. Dieses Tool ersetzt CMTrace und stellt eine anpassbare Benutzeroberfläche mit Registerkarten und andockbaren Fenstern zur Verfügung. Er verfügt über eine Darstellungsschicht und kann große Protokolldateien innerhalb weniger Sekunden laden.

### <a name="support-center-onetrace-preview"></a>Supportcenter: OneTrace (Vorschau)

<!--3555962-->
Ab Version 1906 ist **OneTrace** als neue Protokollanzeige im Supportcenter verfügbar. Die Funktionsweise ähnelt der von CMTrace, bietet jedoch einige Verbesserungen. Weitere Informationen finden Sie unter [Supportcenter – OneTrace](support-center-onetrace.md).

### <a name="powershell-cmdlets"></a>PowerShell-Cmdlets

Im Supportcenter können zudem [Windows PowerShell-Cmdlets](https://go.microsoft.com/fwlink/?linkid=397830) verwendet werden. Verwenden Sie diese Cmdlets, um eine Remoteverbindung zu einem anderen Konfigurations-Manager-Client herzustellen, um die Optionen für die Datensammlung zu konfigurieren und um die Datensammlung zu starten.


## <a name="prerequisites"></a>Voraussetzungen

Installieren Sie folgende Komponenten auf dem Server oder Clientcomputer, auf dem Sie das Supportcenter installiert haben:

- Eine von Configuration Manager unterstützte Betriebsystemversion. Weitere Informationen finden Sie unter [Unterstützte Betriebssystemversionen für Clients ](../plan-design/configs/supported-operating-systems-for-clients-and-devices.md). Mobile Geräte werden vom Supportcenter nicht unterstützt.  

- Auf dem Computer, auf dem Sie das Supportcenter und die zugehörigen Komponenten ausführen, muss .NET Framework 4.5.2 vorhanden sein.  


## <a name="install"></a>Installation

Den Installer für das Supportcenter finden Sie auf dem Standortserver unter dem Pfad `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`.

Nach der Installation sind folgende Elemente im Startmenü der Gruppe **Microsoft System Center** vorhanden:  

- Supportcenter (ConfigMgrSupportCenter.exe)  
- Protokolldateianzeige des Supportcenters (CMLogViewer.exe)  
- Supportcenteranzeige (ConfigMgrSupportCenterViewer.exe)  


## <a name="known-issues"></a>Bekannte Probleme

### <a name="you-cant-install-the-latest-version-if-an-older-version-is-already-installed"></a>Sie können nicht die neueste Version installieren, wenn bereits eine ältere Version installiert ist.

<!--SCCMDocs-pr issue #3090-->
*Gilt für die Versionen 1810 und 1902*

Wenn Sie bereits eine ältere Version von Supportcenter installiert haben, tritt beim neuen Installationsprogramm ein Fehler auf. Dieses Problem tritt aufgrund der Versionsangaben der Dateien zwischen der ursprünglichen Version und der aktuellen Version auf. Um dieses Problem zu umgehen, deinstallieren Sie zuerst die ältere Version des Supportcenters. Installieren Sie anschließend die neueste Version.

### <a name="remote-connections-must-include-computer-name-or-domain-as-part-of-the-user-name"></a>Remoteverbindungen müssen den Computernamen oder die Domäne im Benutzernamen enthalten.

Wenn Sie eine Verbindung mit einem Remoteclient des Supportcenters herstellen, müssen Sie den Computernamen oder den Domänennamen für das Benutzerkonto beim Herstellen der Verbindung angeben. Wenn Sie eine Kurzschreibweise des Computer- oder Domänennamens verwenden (z.B. `.\administrator`), wird die Verbindung zwar erfolgreich hergestellt, aber das Supportcenter sammelt keine Daten vom Client.

Verwenden Sie folgende Formate für Benutzernamen, wenn Sie eine Verbindung mit einem Remoteclient herstellen, um dieses Problem zu vermeiden:

- `ComputerName\UserName`  
- `DomainName\UserName`  

### <a name="scripted-server-message-block-connections-to-remote-clients-might-require-removal"></a>SMB-Skriptverbindungen (Server Message Block, SMB) zu Remoteclients müssen möglicherweise entfernt werden.

Wenn Sie über das PowerShell-Cmdlet [New-CMMachineConnection](https://go.microsoft.com/fwlink/p/?linkid=390542) eine Verbindung mit Remoteclients herstellen, erstellt das Supportcenter eine SMB-Verbindung mit jedem Remoteclient. Diese Verbindungen werden nach der Datensammlung beibehalten. Verwenden Sie den Befehl `net use`, um die aktiven Remoteverbindungen anzuzeigen und um zu vermeiden, dass die maximale Anzahl der Remoteverbindungen für Windows überschritten wird. Deaktivieren Sie nicht benötigte Verbindungen über den Befehl `net use <connection_name> /d`.
Hierbei entspricht `<connection_name>` dem Namen der Remoteverbindung.

### <a name="application-deployment-evaluation-cycle-request-isnt-sent-correctly-to-remote-machines"></a>Die Anforderung an den Auswertungszyklus für die Anwendungsbereitstellung wird nicht ordnungsgemäß an Remotecomputer gesendet

<!--2849356-->
*Gilt für Version 1810*

Wenn Sie im Supportcenter auf der Registerkarte **Inhalt** in der Aktion **Invoke trigger** (Trigger aufrufen) auf **Application deployment evaluation** (Auswertung der Anwendungsbereitstellung) klicken, startet diese Aktion einen Task, der bereitgestellte Anwendungen auswertet. Wenn Sie mit einem lokalen Client verbunden sind, wertet er sowohl Computer- als auch Benutzeranwendungsbereitstellungen aus. Wenn Sie jedoch mit einem Remoteclient verbunden sind, werden nur Computeranwendungsbereitstellungen ausgewertet.


## <a name="next-steps"></a>Nächste Schritte

[Support Center quickstart (Schnellstart für das Supportcenter)](support-center-quickstart.md)
