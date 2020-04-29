---
title: Technische Referenz zur Anwendungsauswertung
titleSuffix: Configuration Manager
description: Technische Referenz zur Problembehandlung bei der Anwendungsauswertung für Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: a7035223-d7bd-47b4-896f-08de3416a4eb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fdeec54489adfc0d2a5cceb99c7e7587ce1a41ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688838"
---
# <a name="application-deployment-evaluation"></a>Auswertung der Anwendungsbereitstellung

*Gilt für: Configuration Manager (Current Branch)*

Bevor Sie fortfahren, überprüfen Sie die [Clientkomponenten für die Anwendungsbereitstellung](client-components-technical-reference.md), um die Auftragsverarbeitung von DCM- und CI-Agents zu verstehen.

Die Auswertung der Anwendung wird von den DCM-Agent- und CI-Agent-Komponenten durchgeführt, wenn die Bereitstellung aktiviert wird. Informationen darüber, wann die Zuweisung aktiviert wird, finden Sie in den Artikeln [Anwendungsbereitstellung für Gerätesammlungen](device-deployment-technical-reference.md) oder [Anwendungsbereitstellung für Benutzersammlungen](user-deployment-technical-reference.md).

## <a name="application-detection-and-evaluation"></a>Anwendungserkennung und -auswertung

Die Anwendungsauswertung wird während der **InvokingSdmMethod**-Phase eines CI-Agent-Auftrags durchgeführt. In dieser Phase wertet der Kunde die für die Anwendung definierte Erkennungsmethode aus, um festzustellen, ob die Anwendung auf dem Gerät installiert ist. Diese Aktivität kann in **AppDiscovery.log** unter Verwendung der eindeutigen Bereitstellungstyp-ID oder des Bereitstellungstypnamens nachverfolgt werden.

```text
Performing detection of app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
+++ Did not detect app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
```

> [!NOTE]
> Das obige Beispiel zeigt die Erkennung für eine MSI-Anwendung, bei der die Erkennung durch Überprüfung erfolgt, ob der MSI-Produktcode auf dem Gerät installiert ist. Bei Anwendungen, die alternative Erkennungsmethoden verwenden, wird die entsprechende Erkennungsmethode verwendet, um zu prüfen, ob die Anwendung installiert ist.

Anschließend wertet der Kunde den gewünschten Zustand der Anwendung auf der Grundlage des Bereitstellungszwecks aus. Dieser Schritt umfasst auch die Erkennung, ob die Anwendung Abhängigkeiten oder Ablösungsregeln aufweist, die bei der Anwendung beachtet werden sollten. Diese Aktivität kann in **AppIntentEval.log** unter Verwendung der eindeutigen ID des Anwendungs- und Bereitstellungstyps nachverfolgt werden.

<pre><code class="lang-text"># Available Application Deployment

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = Applicable, ResolvedState = Available</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]

# Required Application Deployment

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = Applicable, ResolvedState = Installed</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]

# Requirement Rules Not Met

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = NotApplicable, ResolvedState = None</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]
</code></pre>

Im obigen Protokolleintrag gibt **Aktueller Zustand** an, ob die Anwendung derzeit auf dem Gerät installiert ist. **Anwendbarkeit** gibt an, ob die Anwendung auf der Grundlage definierter Anforderungsregeln anwendbar ist. **ResolvedState** gibt den gewünschten Zustand der Anwendung auf der Grundlage des Bereitstellungszwecks an.

> [!TIP]
> Verwenden Sie das [Deployment Monitoring Tool](../../core/support/deployment-monitoring-tool.md) (Tool zur Überwachung der Bereitstellung), um Anwendungszustand, Anwendbarkeitszustand und Anforderungsverletzungen anzuzeigen.

## <a name="next-steps"></a>Nächste Schritte

- [Herunterladen der Anwendung](deployment-download-technical-reference.md)
