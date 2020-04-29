---
title: Technische Referenz zur Anwendungsinstallation
titleSuffix: Configuration Manager
description: Technische Referenz zur Problembehandlung bei der Anwendungsinstallation für Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 2af4f9c3-16b8-4691-a59d-aea6241d288e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 13c96e9ad4f0608084d87bed3973221730cb2d5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688818"
---
# <a name="application-installation"></a>Anwendungsinstallation

*Gilt für: Configuration Manager (Current Branch)*

Bevor Sie fortfahren, überprüfen Sie die [Clientkomponenten für die Anwendungsbereitstellung](client-components-technical-reference.md), um die Auftragsverarbeitung von DCM- und CI-Agents zu verstehen.

Die Installation der Anwendung wird von DCM-Agent- und CI-Agent-Komponenten durchgeführt, wenn die Bereitstellung erzwungen wird. Die Erzwingungszeit unterscheidet sich für verfügbare und erforderliche Bereitstellungen. Informationen darüber, wann die Zuweisung erzwungen wird, finden Sie in den Artikeln [Anwendungsbereitstellung für Gerätesammlungen](device-deployment-technical-reference.md) oder [Anwendungsbereitstellung für Benutzersammlungen](user-deployment-technical-reference.md).

## <a name="enforcement-initiation"></a>Einleitung der Erzwingung

Die Installation der Anwendung wird von der CI-Agent-Komponente auf dem Client während der **StateEnforcingCIs**-Phase eingeleitet. Dieser Prozess ist derselbe, unabhängig davon, ob die Anwendung in einer Geräte- oder Benutzersammlung bereitgestellt wird.

- Bei Bereitstellungen vom Typ **Verfügbar** wird die Anwendung installiert, wenn der Benutzer die Installation der Anwendung über das Softwarecenter initiiert.
- Bei Bereitstellungen vom Typ **Erforderlich** wird die Anwendung zum Bereitstellungsstichtag installiert. Der Benutzer kann die Installation jedoch vor dem Stichtag über das Softwarecenter initiieren.

Wenn der CI-Agent die Installation der Anwendung initiiert, erstellt er eine Aufgabe, die von der CI-Task-Manager-Komponente bearbeitet wird. Der CI-Task-Manager leitet dann die Installation ein. Diese Aktivität kann in **CITaskMgr.log** unter Verwendung der eindeutigen Bereitstellungstyp-ID nachverfolgt werden.

<pre><code class="lang-text"><b>Initiating task Enforce</b> for CI ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2 (ConfigMgr Toolkit - Windows Installer (*.msi file)) for target: , consumer: {9BC3154A-98F1-4595-A967-173D536A3F94}
Initiated application enforcement. : CITask(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2..Install.Enforce)
</code></pre>

## <a name="application-enforcement"></a>Anwendungserzwingung

Nachdem die Anwendungserzwingung eingeleitet wurde, führt der Client die Anwendungserkennung erneut durch, um sicherzustellen, dass die Anwendung nicht bereits installiert ist. Sobald festgestellt wird, dass die Anwendung nicht installiert ist, wird die Installation der Anwendung initiiert. Diese Aktivität kann in **AppEnforce.log** auf dem Client unter Verwendung der eindeutigen Bereitstellungstyp-ID nachverfolgt werden.

```text
+++ Starting Install enforcement for App DT "ConfigMgr Toolkit - Windows Installer (*.msi file)" ApplicationDeliveryType - ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, Revision - 2, ContentPath - C:\WINDOWS\ccmcache\2, Execution Context - System
    Executing Command line: "C:\WINDOWS\system32\msiexec.exe" /i "ConfigMgrTools.msi" /q /qn with user context
    Process 7292 terminated with exitcode: 0
Status is switching to Success
```

## <a name="installation-verification"></a>Überprüfung der Installation

Nachdem die Anwendung installiert wurde, wird die Anwendungserkennungsmethode erneut verwendet, um sicherzustellen, dass die Anwendung als installiert erkannt wurde.

<pre><code class="lang-text">Performing detection of app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
+++ <b>Discovered MSI application</b> [AppDT Id: ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, Revision: 2, MSI Product code: {4FFF7ECC-CCF7-4530-B938-E7812BB91186}, MSI Product version: ]
++++++ <b>App enforcement completed</b> (3 seconds) for App DT "ConfigMgr Toolkit - Windows Installer (*.msi file)" [ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44], Revision: 2, User SID: ] ++++++
</code></pre>

Nachdem die Erzwingung abgeschlossen ist, erhält der CI-Agent schließlich die Benachrichtigung, dass die Aufgabe abgeschlossen ist, und der Auftrag des CI-Agents geht in die nächste Phase über.

<pre><code class="lang-text">CIAgentJob({2BF84225-C9E8-49A6-A308-A160C4B799D3}): CAgentJob::HandleEvent(<b>Event=CITaskComplete, CurrentState=StateEnforcingCIs</b>)
</code></pre>

## <a name="next-steps"></a>Nächste Schritte

[Problembehandlung bei Anwendungsbereitstellungen](../deploy-use/troubleshoot-application-deployment.md)
