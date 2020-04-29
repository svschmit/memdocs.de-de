---
title: Technische Referenz zu Clientkomponenten für die Anwendungsbereitstellung
titleSuffix: Configuration Manager
description: Zur Problembehandlung verwendete Clientkomponenten für die Anwendungsbereitstellung in Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 701a3456-9dd6-4aaa-9c5a-37c1e1773216
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 35b54bd5868197d607a15ab1d4759d03968b9892
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688848"
---
# <a name="understanding-application-deployment-client-components"></a>Grundlegendes zu Clientkomponenten für die Anwendungsbereitstellung

*Gilt für: Configuration Manager (Current Branch)*

Die Vorgänge zur Auswertung und Erzwingung der Anwendungsbereitstellung werden von den Komponenten DCM-Agent und CI-Agent auf dem Client durchgeführt. In diesem Artikel wird erläutert, wie ein typischer Auftrag eines DCM- und CI-Agents abläuft.

## <a name="dcm-agent"></a>DCM-Agent

Der DCM-Agent ist eine allgemeine Clientkomponente, die für die Auswertung von Konfigurationsobjekten, zu denen auch Anwendungen gehören, verantwortlich ist. Wenn eine Bereitstellung aktiviert oder erzwungen wird, wird ein DCM-Agent-Auftrag erstellt, der die Zuweisungsrichtlinie liest und die durchzuführenden Aktionen bestimmt. Diese Aktivität kann in **DCMAgent.log** auf dem Client unter Verwendung der Auftrags-ID des DCM-Agents nachverfolgt werden, die durch die Suche nach der eindeutigen Anwendungs-ID identifiziert werden kann.

### <a name="device-deployments"></a>Gerätebereitstellungen

- Für **erforderliche** Bereitstellungen würde DCMAgent.log die anwendbaren Aktionen anzeigen. Diese Aktionen können sich je nachdem, ob der Bereitstellungsstichtag bereits abgelaufen ist, unterscheiden.

    ```text
    # Evaluation Job example:
    DCMAgentJob({A9E850E2-91B0-4122-94FD-D14EDF925AF7}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 with actions: Evaluation, Content Download

    # Enforcement Job example:
    DCMAgentJob({4C8A9F6E-390B-450E-B505-B5698DB68EDD}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 with actions: Evaluation, Install, Uninstall, Update, Look-ahead Install, Look-ahead Uninstall, Look-ahead Update
    ```

- Für **verfügbare** Bereitstellungen zeigt DCMAgent.log, dass für die Bereitstellung Folgendes gilt: `is not mandatory`. Für diese Bereitstellungen wird eine Anwendungsauswertung durchgeführt, aber die Erzwingung wird übersprungen, es sei denn, der Benutzer hat die Installation initiiert.

    ```text
    # Evaluation Job example:
    DCMAgentJob({E353BF94-D7ED-4ADD-AF0F-9273F6A67FC1}): CDCMAgentJob::PopulateCIsFromAssignment - [SCAN] CI policy Id :ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 - Assignment:{3AC57DFE-3F87-4C59-930B-B9F57CB41B91} is not mandatory.

    # Enforcement Job (user initiated) example:
    Request to enforce application ConfigMgr Toolkit(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/Application_fc76ef0a-3ab0-4110-8cce-1addc36d0225.3) immediately for target: machine with action(s): Evaluation, Install, Update
    CDCMAgentJobMgr::CreateInteractiveJob - Queuing new job: {D331249E-F7DE-481B-A497-8E8B5E7B91C3}

    ```

### <a name="user-deployments"></a>Benutzerbereitstellungen

- Für **erforderliche** Bereitstellungen würde DCMAgent.log die anwendbaren Aktionen anzeigen. Diese Aktionen können sich je nachdem, ob der Bereitstellungsstichtag bereits abgelaufen ist, unterscheiden.

    ```text
    # Evaluation Job example:
    DCMAgentJob({65D9688D-1781-4DA3-B07A-193D481251C6}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 with actions: Evaluation, Content Download

    # Enforcement Job example:
    DCMAgentJob({2B0DA272-FC65-4F31-9557-C4D840D650F1}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 with actions: Evaluation, Install, Uninstall, Update, Look-ahead Install, Look-ahead Uninstall, Look-ahead Update
    ```

- Für **verfügbare** Bereitstellungen werden DCM-Agent-Aufträge zur Auswertung und Erzwingung erstellt, wenn die Anwendungsinstallation vom Benutzer initiiert wird.

    ```text
    # Evaluation Job example:
    DCMAgentJob({FBB44C84-DB06-41F7-8DC1-D9BA368F0C20}): CDCMAgentJob::PopulateCIsFromAssignment - [SCAN] CI policy Id :ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 - Assignment:{7EA17128-EB4F-448A-88A7-B865E7DA228C} is not mandatory.

    # Enforcement Job example:
    CAppMgmtSDK::EnforceAppPolicy ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98.
    CDCMAgentJobMgr::CreateInteractiveJob - Queuing new job: {7936D7F3-24B0-401D-BADD-59EB5B49C2C2}
    ```

## <a name="ci-agent"></a>CI-Agent

Der CI-Agent ist die Clientkomponente, die für die Auswertung und Wartung von Konfigurationselementen zuständig ist. Der DCM-Agent liest die Zuweisungsrichtlinie und erstellt einen Auftrag für die CI-Agent-Komponente, um die angeforderten Aktionen auszuführen. **DCMAgent.log** zeichnet die Auftrags-ID des CI-Agents auf, die zur Verfolgung der CI-Agent-Aktivität in **CIAgent.log** auf dem Client hilfreich ist.

<pre><code class="lang-text">DCMAgentJob({E353BF94-D7ED-4ADD-AF0F-9273F6A67FC1}): CDCMAgent::InitiateCIAgentJob - <b>Starting CI Agent Job</b> {57AF6FA1-3482-4469-9881-A63F41D18406} for target: machine. Refer to this CI agent job ID in ciagent.log for more details
</code></pre>

Ein typischer CI-Agent-Auftrag durchläuft mehrere Phasen, die durch Filtern von **CIAgent.log** nach der Auftrags-ID des CI-Agents und durch anschließendes Suchen nach `TransitionState` identifiziert werden können. Einige der Schlüsselphasen für einen CI-Agent-Auftrag zur Anwendungsbereitstellung sind:

- **DownloadingCIs**
  - Während dieser Phase werden die zur Auswertung der Anwendung erforderlichen Anwendungsmetadaten heruntergeladen. Die Metadaten umfassen Erkennungsmethode, Anforderungsregeln, globale Bedingungen usw. Diese Aktivität kann in **CIDownloader.log** und **DataTransferService.log** nachverfolgt werden. Für **verfügbare** Bereitstellungen erfolgt dieser Prozess bei der ersten Auswertung der Anwendung. Für **erforderliche** Bereitstellungen erfolgt dieser Prozess jedoch unmittelbar nach dem Herunterladen der Richtlinie.

- **InvokingSdmMethod**
  - In dieser Phase wird mithilfe der Anwendungserkennungsmethode geprüft, ob die Anwendung installiert ist, und der gewünschte Zustand ermittelt. Diese Aktivität kann in **AppDiscovery.log** und **AppIntentEval.log** nachverfolgt werden. Weitere Informationen zu dieser Phase finden Sie unter [Anwendungsauswertung](deployment-evaluation-technical-reference.md).

- **StateDownloadingContents**
  - In dieser Phase wird der Anwendungsinhalt bei Bedarf heruntergeladen. Diese Aktivität kann in **CAS.log**, **ContentTransferManager.log**, **LocationServices.log** und **DataTransferService.log** nachverfolgt werden. Weitere Informationen zu dieser Phase finden Sie unter [Anwendungsdownload](deployment-download-technical-reference.md).

- **StateEnforcingCIs**
  - In dieser Phase wird die Installation der Anwendung initiiert. Diese Aktivität kann in **AppEnforce.log** nachverfolgt werden. Weitere Informationen zu dieser Phase finden Sie unter [Anwendungsinstallation](deployment-install-technical-reference.md).

- **StateEnforcementReporting**
  - In dieser Phase wird der Installationszustand der Anwendung zur Berichterstellung für den Verwaltungspunkt aufgezeichnet. Diese Aktivität kann in **StateMessage.log** nachverfolgt werden.

Obwohl der Auftrag des CI-Agents alle Phasen durchläuft, überspringt er die Phase, wenn sie nicht erforderlich ist. Für **verfügbare** Bereitstellungen werden z. B. die Phasen „StateDownloadingContents“ und „StateEnforcingCIs“ übersprungen, bis der Benutzer versucht, die Anwendung vom Softwarecenter aus zu installieren. Bei **erforderlichen** Bereitstellungen wird jedoch in der Phase „StateDownloadingContents“ der Inhalt der Anwendung (falls erforderlich) heruntergeladen, wenn die Zuweisung aktiviert wird, während die Phase „StateEnforcingCIs“ übersprungen wird, wenn der Stichtag in der Zukunft liegt. Dieses Verhalten kann in CIAgent.log beobachtet werden, indem nach der Auftrags-ID des CI-Agents gefiltert und nach `Skipping policy` gesucht wird.

```text
{57AF6FA1-3482-4469-9881-A63F41D18406} - Skipping policy CI <CI Unique ID> and all dependents for ContentDownload task since CI action was not requested.
{57AF6FA1-3482-4469-9881-A63F41D18406} - Skipping policy CI <CI Unique ID> and all dependents for Enforce task since CI action was not requested.
```

## <a name="next-steps"></a>Nächste Schritte

- [Auswerten der Anwendung](deployment-evaluation-technical-reference.md)
- [Herunterladen der Anwendung](deployment-download-technical-reference.md)
- [Anwendungsinstallation](deployment-install-technical-reference.md)
