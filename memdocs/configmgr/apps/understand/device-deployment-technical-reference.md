---
title: Technische Referenz zur App-Bereitstellung für Gerätesammlungen
titleSuffix: Configuration Manager
description: Technische Referenz zur Problembehandlung bei Anwendungsbereitstellungen für Gerätesammlungen für Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 4e62b04d-fe56-42ed-87dc-e673cf061d52
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1965029a1933793057dc5768bacb391afd645404
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688788"
---
# <a name="application-deployment-for-device-collections"></a>Anwendungsbereitstellung für Gerätesammlungen

*Gilt für: Configuration Manager (Current Branch)*

Wenn eine Anwendung in einer Gerätesammlung bereitgestellt wird, richtet sich die Richtlinie an alle Geräte in der Sammlung, unabhängig vom Bereitstellungszweck. Dieser Artikel erläutert das Herunterladen von Richtlinien und die Bereitstellungsverarbeitung auf dem Client.

> [!TIP]
> Alle zur Überprüfung der Clientprotokolle erforderlichen Informationen erhalten Sie durch Ausführen der SQL-Abfrage, auf die im Abschnitt [Vorbereitung](app-deployment-technical-reference.md#before-you-begin) verwiesen wird.

## <a name="policy-download"></a>Richtliniendownload

Nachdem die Richtlinie für die Anwendungsbereitstellung auf den Client ausgerichtet ist, würde der Client die Richtlinie beim nächsten Richtlinienabfragezyklus herunterladen. Wenn der Client die Richtlinie herunterlädt, lädt er zusätzlich zur Bereitstellungsrichtlinie auch die zugehörigen Richtlinien herunter. Diese entsprechenden Richtlinien umfassen die Richtlinie für die Anwendung, den Bereitstellungstyp, die globalen Bedingungen usw. Die Aktivität zum Herunterladen von Richtlinien kann in **PolicyAgent.log** auf dem Client nachverfolgt werden, wobei entweder die eindeutige Anwendungs- oder Zuweisungs-ID verwendet wird.

<pre><code class="lang-text">Download of policy CCM_Policy_Policy5.PolicyID="{<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>}",PolicySource="SMS:PS1",PolicyVersion="1.00" completed (DTS Job ID: {AE88E639-0E59-40D7-AAA9-4403AAE6EE82})
Policy state for [CCM_Policy_Policy5.PolicyID="{<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>}",PolicySource="SMS:PS1",PolicyVersion="1.00"] is currently [Active]
</code></pre>

Nachdem die Richtlinien auf den Client heruntergeladen wurden, erstellt die Planerkomponente Zeitpläne für die Aktivierung und Erzwingung der Bereitstellung.

## <a name="deployment-activation"></a>Bereitstellungsaktivierung

Die Anwendungsauswertung wird initiiert, wenn die Bereitstellung aktiviert wird. Die Planerkomponente erstellt einen Zeitplan zur Aktivierung der Zuweisung zu der in der Bereitstellung konfigurierten verfügbaren Zeit. Diese Aktivität kann in **Scheduler.log** auf dem Client unter Verwendung der eindeutigen ID der Anwendungszuweisung nachverfolgt werden.

- Für **erforderliche** Bereitstellungen wird der Aktivierungszeitplan erstellt, weist jedoch eine Verzögerung von bis zu zwei Stunden auf, um Ressourcenkonflikte auf Standortservern und Verteilungspunkten zu vermeiden. Die Verzögerung hilft, Konflikte zu vermeiden, da der Inhalt des Antrags während der Auswertung heruntergeladen werden kann, wenn die Anwendung auf der Grundlage definierter Anforderungsregeln anwendbar ist.

    <pre><code class="lang-text">SMSTrigger '15AF8C4000080000' for scheduler '<b>Machine/{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' will fire at 08/15/2019 01:44:00 PM with randomization.
    </code></pre>

- Bei **verfügbaren** Bereitstellungen wird der Aktivierungszeitplan so erstellt, dass er zum verfügbaren Zeitpunkt, der in der Bereitstellung konfiguriert ist, ausgelöst wird.

    <pre><code class="lang-text">SMSTrigger '1E4F8C4000080001' for scheduler '<b>Machine/{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</b>' will fire at 08/15/2019 01:13:33 PM without randomization.
    </code></pre>

Wenn die geplante Zeit erreicht ist, sendet die Planerkomponente die Aktivierungsnachricht an den DCM-Agent, um die Anwendungsauswertung durchzuführen.

<pre><code class="lang-text">Sending message for schedule '<b>Machine/{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</b>' (Target: 'direct:DCMAgent', Name: '')
</code></pre>

Der DCM-Agent erhält die Aktivierungsnachricht und erstellt einen Auftrag zur Auswertung der Anwendung.

```text
CDCMAgent::HandleMessage - Message received for machine: '<?xml version='1.0' ?><CIAssignmentMessage MessageType='Activation'><AssignmentID>{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</AssignmentID></CIAssignmentMessage>'
```

## <a name="deployment-enforcement"></a>Bereitstellungserzwingung

Die Installation der Anwendung wird initiiert, wenn die Bereitstellung erzwungen wird.

- Für **erforderliche** Bereitstellungen erstellt der Planer nach dem Herunterladen der Richtlinie einen Terminplan, um die Anwendung am Bereitstellungsstichtag zu erzwingen. Der Terminplan ist standardmäßig nicht randomisiert. Das zufällige Anordnungsverhalten für die Aktivierung kann durch die Clienteinstellung [Zufällige Stichtaganordnung deaktivieren](../../core/clients/deploy/about-client-settings.md#disable-deadline-randomization) gesteuert werden.

    <pre><code class="lang-text">SMSTrigger '15EF8C4000080000' for scheduler '<b>Machine/DEADLINE:{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' will fire at 08/15/2019 03:05:00 PM without randomization.
    </code></pre>

    Am Stichtag sendet die Planerkomponente die Stichtagsnachricht an den DCM-Agent. 

    <pre><code class="lang-text">Sending message for schedule '<b>Machine/DEADLINE:{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' (Target: 'direct:DCMAgent', Name: '')
    </code></pre>

    Der DCM-Agent erhält die Stichtagsnachricht und erstellt einen Auftrag zum Erzwingen der Anwendung.
  
    ```text
    CDCMAgent::HandleMessage - Message received for machine: '<?xml version='1.0' ?><CIAssignmentMessage MessageType='EnforcementDeadline'><AssignmentID>{5F2FA409-C9B2-4100-8BC8-051820311DE1}</AssignmentID></CIAssignmentMessage>'
    ```

    > [!NOTE]
    > Bei Bereitstellungen mit Stichtag in der Vergangenheit wird die Anwendung sofort durch denselben DCM-Agent-Auftrag aktiviert und erzwungen, der auch die Auswertungs-, Download- und Installationsaktionen durchführt.

- Für **verfügbare** Bereitstellungen gibt es keinen Terminplan, da die Erzwingung erfolgt, wenn die Anwendungsinstallation durch den Benutzer vom Softwarecenter aus initiiert wird. Wenn der Benutzer eine Installation startet, wird ein DCM-Agent-Auftrag erstellt, der die Anwendungsauswertung, den Download und die Installation durchführt. Diese Aktivität kann in **DCMAgent.log** auf dem Client nachverfolgt werden.

## <a name="next-steps"></a>Nächste Schritte

- [Grundlegendes zu Clientkomponenten für die Anwendungsbereitstellung](client-components-technical-reference.md)
