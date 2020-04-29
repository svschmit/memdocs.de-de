---
title: Technische Referenz zum Anwendungsdownload
titleSuffix: Configuration Manager
description: Technische Referenz zur Problembehandlung beim Anwendungsdownload für Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 41c29a07-9bf6-4ec4-b3f2-1c05e001eff7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: effa8115a5023a8e0611f6bc4245a101b3a47e38
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688858"
---
# <a name="application-download-in-configuration-manager"></a>Anwendungsdownload in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Bevor Sie fortfahren, überprüfen Sie die [Clientkomponenten für die Anwendungsbereitstellung](client-components-technical-reference.md), um die Auftragsverarbeitung von DCM- und CI-Agents zu verstehen.

## <a name="download-initiation"></a>Einleiten des Downloads

Der Download des Anwendungsinhalts wird von der CI-Agent-Komponente auf dem Client während der **StateDownloadingContents**-Phase eingeleitet. Dieser Prozess ist derselbe, unabhängig davon, ob die Anwendung in einer Geräte- oder Benutzersammlung bereitgestellt wird.

- Bei Bereitstellungen vom Typ **Verfügbar** wird der Anwendungsinhalt heruntergeladen, wenn der Benutzer die Installation der Anwendung über das Softwarecenter initiiert.
- Für **erforderliche** Bereitstellungen wird der Inhalt der Anwendung heruntergeladen, wenn die Zuweisung aktiviert und die Anwendung nach der Auswertung als anwendbar eingestuft wird. Informationen darüber, wann die Zuweisung aktiviert wird, finden Sie in den Artikeln [Anwendungsbereitstellung für Gerätesammlungen](device-deployment-technical-reference.md) oder [Anwendungsbereitstellung für Benutzersammlungen](user-deployment-technical-reference.md).

Wenn der CI-Agent das Herunterladen des Inhalts initiiert, erstellt er eine Aufgabe, die von der CI-Task-Manager-Komponente bearbeitet wird. Der CI-Task-Manager initiiert dann das Herunterladen der Inhalte. Diese Aktivität kann im **CITaskMgr.log** unter Verwendung der eindeutigen Bereitstellungstyp-ID nachverfolgt werden.

<pre><code class="lang-text"><b>Initiating task ContentDownload</b> for CI ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2 (ConfigMgr Toolkit - Windows Installer (*.msi file)) for target: , consumer: {53EA65C2-D596-4215-83E4-F7007B78E18C}
</code></pre>

## <a name="distribution-point-location"></a>Speicherort des Verteilungspunkts

Alle Downloadaufgaben werden von der Komponente „Zugriff auf Inhalte“ behandelt, die für die Verwaltung des Clientcaches zuständig ist. Nachdem die Downloadaufgabe erstellt wurde, prüft die Komponente „Zugriff auf Inhalte“, ob der Inhalt bereits im Clientcache verfügbar ist. Wenn der Inhalt nicht verfügbar ist, wird eine Standortanforderung erstellt, um eine Liste der Verteilungspunkte zu erhalten, von denen der Inhalt abgerufen werden kann. Diese Aktivität kann in **CAS.log** und **LocationServices.log** auf dem Client anhand der eindeutigen Inhalts-ID nachverfolgt werden.

```text
Requesting locations synchronously for content Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1 with priority Foreground
ContentLocationRequest : <Request XML Body>
Reply Message Body : <Reply XML Body>
```

> [!IMPORTANT]
> Obwohl die Komponente „Ortungsdienste“ die Standortanforderungen bearbeitet, fordert sie Standorte nicht direkt vom Verwaltungspunkt an. Alle Anforderungen für den Verwaltungspunkt laufen in der Regel über die Komponente „CCM-Messaging“, die unter **CcmMessaging.log** protokolliert wird.

Standortantwort-XML enthält die Liste der Verteilungspunkte basierend auf der Begrenzungsgruppe des Kunden. Diese Liste wird in WMI auf dem Client gemäß der [Priorität von Inhaltsquellen](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#content-source-priority) analysiert und beibehalten. Diese Aktivität kann in **ContentTransferManager.log** angezeigt werden, indem die eindeutige Inhalts-ID verwendet und nach `Persisted location` gesucht wird. 

Wenn der Standortantwort-XML-Code keine Verteilungspunkte enthält, zeigt **ContentTransferManager.log** `Received empty location update` an und der Client bleibt möglicherweise beim Herunterladen der Anwendung bei 0 % hängen. Diese Antwort kann in der Regel aufgrund von Problemen bei der Konfiguration von Begrenzungsgruppen erfolgen. Weitere Informationen finden Sie unter [Fehler beim Download](../deploy-use/troubleshoot-application-deployment.md#download-failures).

## <a name="content-download"></a>Inhaltsdownload

Nachdem die Standorte der Verteilungspunkte erhalten wurden, erstellt die Komponente „Zugriff auf Inhalte“ einen Auftrag zur Übertragung von Inhalten. Diese Aktivität kann in **CAS.log** anhand der eindeutigen Inhalts-ID nachverfolgt werden.

<pre><code class="lang-text">Submitted CTM job <b>{6D0EA720-EB4E-4893-8395-8B27470A6CFB}</b> to download Content <b>Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1</b> under context System
</code></pre>

Der Content Transfer Manager erstellt dann einen Auftrag für den Datenübertragungsdienst, um den Download der Inhalte durchzuführen. Diese Aktivität kann in **ContentTransferManager.log** auf dem Client unter Verwendung der eindeutigen Inhalts-ID nachverfolgt werden.

<pre><code class="lang-text">CTM job <b>{6D0EA720-EB4E-4893-8395-8B27470A6CFB}</b> (corresponding DTS job <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b>) started download from '<Distribution Point URL>/<b>Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1</b>' for full content download.
</code></pre>

> [!NOTE]
> Dieser Protokolleintrag kann zur Identifizierung der CTM- und DTS-Auftrags-IDs verwendet werden, die zur Nachverfolgung des Fortschritts der Inhaltsübertragung in **ContentTransferManager.log** bzw. **DataTransferService.log** verwendet werden können.

Der Datenübertragungsdienst führt den Download des Anwendungsinhalts durch, indem er einen BITS-Auftrag (Background Intelligent Transfer Service) erstellt und darauf wartet, dass der Download abgeschlossen wird. Diese Aktivität kann in **DataTransferService.log** auf dem Client unter Verwendung der DTS-Auftrags-ID nachverfolgt werden, die von **ContentTransferService.log** abgerufen wird.

<pre><code class="lang-text">Starting BITS job '{40263E01-2EDD-462F-ABBA-A5E892CB9229}' for DTS job '<b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b>' under user 'S-1-5-18'.
DTSJob <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b> in state 'DownloadingData'.
DTS job <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b> has completed
</code></pre>

Nachdem der Download abgeschlossen ist, wird die Komponente „Zugriff auf Inhalte“ benachrichtigt. Die Komponente „Zugriff auf Inhalte“ überprüft dann den heruntergeladenen Inhalt, um sicherzustellen, dass der Inhalt beim Herunterladen nicht verändert wurde. Diese Aktivität kann in **CAS.log** anhand der eindeutigen Inhalts-ID nachverfolgt werden.

```text
Hash verification succeeded for content Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1 downloaded under context System
```

Nachdem der Inhalt überprüft wurde, erhält der CI-Agent schließlich die Benachrichtigung, dass die Aufgabe abgeschlossen ist, und der Auftrag des CI-Agents geht in die nächste Phase über.

<pre><code class="lang-text">CIAgentJob({2BF84225-C9E8-49A6-A308-A160C4B799D3}): CAgentJob::HandleEvent(<b>Event=CITaskComplete, CurrentState=StateDownloadingContents</b>)
</code></pre>

## <a name="next-steps"></a>Nächste Schritte

- [Anwendungsinstallation](deployment-install-technical-reference.md)
