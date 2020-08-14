---
title: Problembehandlung für CMPivot
titleSuffix: Configuration Manager
description: Informationen zur Problembehandlung für CMPivot in Configuration Manager
ms.date: 10/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 36385bea-f05e-4300-947f-cb3927b3bac5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6bddf46df63eac70a536faaee04a2ac7243e534a
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128272"
---
# <a name="troubleshoot-cmpivot"></a>Problembehandlung für CMPivot

CMPivot ist ein Tool, das Zugriff auf den Status der Geräte in Ihrer Umgebung in Echtzeit ermöglicht. CMPivot führt eine Abfrage aller derzeit verbundenen Geräte in der Zielsammlung durch und gibt die Ergebnisse zurück.

Gelegentlich ist für CMPivot eine Problembehandlung erforderlich. Wenn beispielsweise eine Zustandsmeldung von einem Client an CMPivot fehlerhaft ist, kann diese vom Standortserver nicht verarbeitet werden. In diesem Artikel wird der Informationsfluss für CMPivot erläutert.

## <a name="troubleshoot-cmpivot-in-version-1902-and-later"></a><a name="bkmk_CMPivot-1902"></a> Problembehandlung für CMPivot, Version 1902 und höher

In Configuration Manager, Version 1902 und höher, können Sie CMPivot über den Standort der zentralen Verwaltung (Central Administration Site, CAS) in einer Hierarchie ausführen. Die Kommunikation mit dem Client wird nach wie vor vom primären Standort abgewickelt.

Wenn Sie CMPivot über den CAS ausführen, wird zur Kommunikation mit dem primären Standort der Hochgeschwindigkeits-Abonnementkanal für Meldungen verwendet. CMPivot verwendet keine standardmäßige SQL-Replikation zwischen Standorten. Wenn Ihre SQL Server-Instanz oder Ihr SQL-Anbieter remote arbeiten oder Sie SQL Always On verwenden, liegt für CMPivot ein „Double-Hop-Szenario“ vor. Informationen zum Definieren der eingeschränkten Delegierung für ein solches Double-Hop-Szenario finden Sie unter [CMPivot ab Version 1902](cmpivot-changes.md#bkmk_cmpivot1902).

>[!IMPORTANT]
> Aktivieren Sie bei der Problembehandlung für CMPivot die ausführliche Protokollierung in Ihren Verwaltungspunkten (MPs) und der SMS_MESSAGE_PROCESSING_ENGINE des Standortservers, um weitere Informationen zu erhalten. Wenn die Clientausgabe zudem größer als 80 KB ist, aktivieren Sie die ausführliche Protokollierung im MP und in der SMS_STATE_SYSTEM-Komponenten des Standortservers. Weitere Informationen zum Aktivieren der ausführlichen Protokollierung finden Sie unter [Protokollierungsoptionen für den Standortserver](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-site).

### <a name="get-information-from-the-site-server"></a>Abrufen von Informationen des Standortservers

Die Protokolldateien des Standortserver befinden sich standardmäßig unter `C:\Program Files\Microsoft Configuration Manager\logs`. Es wird aber möglicherweise ein anderer Speicherort verwendet, wenn ein nicht standardmäßiges Installationsverzeichnis angegeben wurde oder wenn Sie Elemente wie den SMS-Anbieter auf einen anderen Server ausgelagert haben. Wenn Sie CMPivot über den CAS ausführen, befinden sich die Protokolle auf dem primären Standortserver.

Suchen Sie in `smsprov.log` nach folgenden Zeilen:

- Configuration Manager, Version 1906:
  <pre><code lang="Log">Auditing: User &ltusername> initiated client operation 145 to collection &ltCollectionId>. </code></pre>

- Configuration Manager, Version 1902:
  <pre><code lang="Log">Type parameter is 135.
  Auditing: User &ltusername> ran script 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 with hash dc6c2ad05f1bfda88d880c54121c8b5cea6a394282425a88dd4d8714547dc4a2 on collection &ltCollectionId>. </code></pre>

 `7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14` ist die Skript-GUID für CMPivot. Sie finden diese GUID auch unter [Überwachungsstatusmeldungen für CMPivot](cmpivot-changes.md#cmpivot-audit-status-messages).

Suchen Sie als Nächstes die ID im CMPivot-Fenster. Diese ID ist die `ClientOperationID`.

![CMPivot-Fenster, „ClientOperationID“ hervorgehoben](media/cmpivot-client-operationid-1902.png)

Suchen Sie die `TaskID` in der Tabelle „ClientAction“. Die `TaskID` entspricht der `UniqueID` in der Tabelle „ClientAction“.

``` SQL
select * from ClientAction where ClientOperationId=<id>
```

Suchen Sie in `BgbServer.log` nach der `TaskID`, die Sie aus SQL erfasst haben, und notieren Sie sich die `PushID`. Die `TaskID` ist mit `TaskGUID` gekennzeichnet. Beispiele:

<pre><code lang="Log">Starting to send push task (<b>PushID: 9</b> TaskID: 12 <b>TaskGUID: 9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0</b> TaskType: 15 TaskParam: PFNjcmlwdENvbnRlbnQgU2NyaXB0R3VpZD0nN0RDNkI2RjEtRTdGNi00M0MxL (truncated log entry)
Finished sending push task (<b>PushID: 9</b> TaskID: 12) to 2 clients
</code></pre>

### <a name="client-logs"></a>Clientprotokolle

Sobald Sie die Informationen vom Standortserver erhalten haben, überprüfen Sie die Clientprotokolle. Standardmäßig werden die Clientprotokolle unter `C:\Windows\CCM\Logs` gespeichert.

Suchen Sie in `CcmNotificationAgent.log` nach Protokolleinträgen, die wie die folgenden Zeilen aussehen:  

<pre><code lang="Log">Receive task from server with <b>pushid=9</b>, taskid=12, <b>taskguid=9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0</b>, tasktype=15 and taskParam=PFNjcmlwdEhhc2ggU2NyaXB0SGF (truncated log entry)
Send Task response message &ltBgbResponseMessage TimeStamp="2019-09-13T17:29:09Z"><b>&ltPushID>5</b>&lt/PushID>&ltTaskID>4&lt/TaskID>&ltReturnCode>1&lt/ReturnCode>&lt/BgbResponseMessage> successfuly.
 </code></pre>

Suchen Sie in `Scripts.log` die `TaskID`. Im folgenden Beispiel sehen Sie `Task ID` `{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}`:

<pre><code lang="Log">Sending script state message (fast): <b>{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}</b>
Result are sent for ScriptGuid: 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 and <b>TaskID: {9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}</b>
</code></pre>

> [!NOTE]
> Wenn in `Scripts.log` nicht „fast“ angezeigt wird, sind die Daten wahrscheinlich größer als 80 KB. In diesem Fall werden die Informationen als Statusmeldung an den Standortserver gesendet. Verwenden Sie das `StateMessage.log` des Clients und das `Statesys.log` des Standortservers.

### <a name="review-messages-on-the-site-server"></a>Überprüfen von Meldungen auf dem Standortserver

Wenn die [ausführliche Protokollierung](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-client) auf dem Verwaltungspunkt aktiviert ist, können Sie sehen, wie eingehende Clientmeldungen verarbeitet werden. Suchen Sie in `MP_RelayMsgMgr.log` nach der `TaskID`.

Im Beispiel `MP_RelayMsgMgr.log` sehen Sie die Client-ID `(GUID:83F67728-2E6D-4E4F-8075-ED035C31B783)` und die `Task ID {9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}`. Der Clientantwort wird eine Meldungs-ID zugewiesen, bevor die Antwort an die Engine zur Meldungsverarbeitung gesendet wird:

<pre><code lang="Log">MessageKey: GUID:83F67728-2E6D-4E4F-8075-ED035C31B783<b>{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}</b>
Create message succeeded for <b>message id 22f00adf-181e-4bad-b35e-d18912f39f89</b>
Add message payload succeeded for message id 22f00adf-181e-4bad-b35e-d18912f39f89
Put message succeeded for message id 22f00adf-181e-4bad-b35e-d18912f39f89
CRelayMsgMgrHandler::HandleMessage(): ExecuteTask() succeeded
</code></pre>

Wenn die [ausführliche Protokollierung ](../../plan-design/hierarchy/about-log-files.md#bkmk_logoptions) in `SMS_MESSAGE_PROCESSING_ENGINE.log` aktiviert ist, werden die Clientergebnisse verarbeitet. Verwenden Sie die Meldungs-ID, die Sie in `MP_RelayMsgMgr.log` finden. Die Einträge des Verarbeitungsprotokolls ähneln dem folgenden Beispiel:

<pre><code lang="Log">Processing 2 messages with type Instant and IDs <b>22f00adf-181e-4bad-b35e-d18912f39f89[19]</b>, 434d80ae-09d4-4d84-aebf-28a4a29a9852[20]...
Processed 2 messages with type Instant. Failed to process 0 messages. All message IDs <b>22f00adf-181e-4bad-b35e-d18912f39f89[19]</b>, 434d80ae-09d4-4d84-aebf-28a4a29a9852[20]
</code></pre>

> [!TIP]
> Wenn während der Verarbeitung eine Ausnahme auftritt, können Sie diese anzeigen, indem Sie die folgende SQL-Abfrage ausführen und sich die Spalte „Exception“ ansehen. Nachdem die Meldung verarbeitet wurde, befindet sie sich nicht mehr in der Tabelle `MPE_RequestMessages_Instant`.
>
> ```SQL
> select * from MPE_RequestMessages_Instant where MessageID=<ID from SMS_MESSAGE_PROCESSING_ENGINE.log>
> ```

Suchen Sie in der Datei `BgbServer.log` nach der `PushID`, um die Anzahl von Clients zu sehen, die eine Meldung gesendet haben oder bei denen ein Fehler aufgetreten ist.

<pre><code lang="Log">Generated BGB task status report c:\ConfigMgr\inboxes\bgb.box\Bgb5c1db.BTS at 09/16/2019 16:46:39. (<b>PushID: 9</b> ReportedClients: 2 FailedClients: 0)
</code></pre>

Überprüfen Sie mithilfe der `TaskID` die Überwachungsansicht für CMPivot über SQL.

``` SQL
select * from vSMS_CMPivotStatus where TaskID='{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}'
```

[ ![CMPivot-SQL-Abfragen für die Problembehandlung in Version 1902](media/cmpivot-sql-queries-1902.png)](media/cmpivot-sql-queries-1902.png#lightbox)

## <a name="troubleshoot-cmpivot-in-1810-and-earlier"></a><a name="bkmk_CMPivot-1810"></a> Problembehandlung für CMPivot in Version 1810 und früher

In Configuration Manager, Version 1810 und früher, wird die Kommunikation mit dem Client vom Standortserver verarbeitet.

### <a name="get-information-from-the-site-server"></a>Abrufen von Informationen des Standortservers

Die Protokolldateien des Standortserver befinden sich standardmäßig unter `C:\Program Files\Microsoft Configuration Manager\logs`. Es wird aber möglicherweise ein anderer Speicherort verwendet, wenn ein nicht standardmäßiges Installationsverzeichnis angegeben wurde oder wenn Sie Elemente wie den SMS-Anbieter auf einen anderen Server ausgelagert haben.

Suchen Sie in `smsprov.log` nach der folgenden Zeile:

<pre><code lang="Log">Auditing: User <username> initiated client operation 135 to collection &ltCollectionId>.
</code></pre>

Suchen Sie die ID im Fenster „CMPivot“. Diese ID ist die `ClientOperationID`.

![CMPivot-Fenster, „ClientOperationID“ hervorgehoben](media/cmpivot-clientoperationid.png)

Suchen Sie die `TaskID` in der Tabelle „ClientAction“. Die `TaskID` entspricht der `UniqueID` in der Tabelle „ClientAction“.

``` SQL
select * from ClientAction where ClientOperationId=<id>
```

Suchen Sie in `BgbServer.log` nach der `TaskID`, die Sie aus SQL erfasst haben. Sie ist mit `TaskGUID` gekennzeichnet. Beispiele:

<pre><code lang="Log">Starting to send push task (PushID: 260 TaskID: 258 TaskGUID: <b>F8C7C37F-B42B-4C0A-B050-2BB44DF1098A</b> TaskType: 15
TaskParam: PFNjcmlwdEhhc2ggU2NyaXB0SGF...truncated...to 5 clients with throttling (strategy: 1 param: 42)
Finished sending push task (PushID: 260 TaskID: 258) to 5 clients
</code></pre>

### <a name="client-logs"></a>Clientprotokolle

Sobald Sie die Informationen vom Standortserver erhalten haben, überprüfen Sie die Clientprotokolle. Standardmäßig werden die Clientprotokolle unter `C:\Windows\CCM\Logs` gespeichert.

Suchen Sie in `CcmNotificationAgent.log` nach Protokollen, die dem folgenden Eintrag ähneln:  

<pre><code lang="Log"><b>Error! Bookmark not defined.</b>+PFNjcmlwdEhhc2ggU2NyaXB0SGFzaEFsZz0nU0hBMjU2Jz42YzZmNDY0OGYzZjU3M2MyNTQyNWZiNT
g2ZDVjYTIwNzRjNmViZmQ1NTg5MDZlMWI5NDRmYTEzNmFiMDE0ZGNjPC9TY3JpcHRIYXNoPjxTY3Jp (truncated log entry)
</code></pre>

Suchen Sie in `Scripts.log` nach der `TaskID`. Im folgenden Beispiel sehen wir die `Task ID {F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}`:

<pre><code lang="Log">Sending script state message: 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14
State message: Task Id <b>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</b>
</code></pre>

Suchen Sie in `StateMessage.log`. Im folgenden Beispiel sehen Sie, dass sich die `TaskID` am Ende der Meldung neben `<Param>` befindet:

``` XML
StateMessage body: <?xml version="1.0" encoding="UTF-16"?>
<Report><ReportHeader><Identification><Machine><ClientInstalled>1</ClientInstalled><ClientType>1
</ClientType><ClientID>GUID:DBAC52C9-57E6-47D7-A8D6-E0A5A64B57E6</ClientID><ClientVersion>5.00.8670.1000</ClientVersion>
<NetBIOSName>R613924</NetBIOSName><CodePage>437</CodePage>
<SystemDefaultLCID>1033</SystemDefaultLCID><Priority>0</Priority></Machine></Identification>
<ReportDetails><ReportContent>State Message Data</ReportContent><ReportType>Full</ReportType>
<Date>20180703184447.673000+000</Date><Version>1.0</Version><Format>1.0</Format>
</ReportDetails></ReportHeader><ReportBody><StateMessage MessageTime="20180703184447.517000+000"><Topic ID="7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14" Type="9003" IDType="0" User="" UserSID=""/><State ID="1" Criticality="0"/>
<StateDetails Type="1"><![CDATA["PAA/AHgAbQBsACAAdgBlAHIAcwBpAG8AbgA9ACIAMQAuADAAIgAgAGUAbgBjAG8AZABpAG4AZwA9ACIAdQB0AGYALQAxADYAIgA/AD4APAByAGUAcwB1AGwAdAAgAFIAZQBzAHUAbAB0AEMAbwBkAGUAPQAiADAAIgA+ADwAZQAgAE4AYQBtAGUAPQAiAEkAbgB0AGUAbAAoAFIAKQAgAFgAZQBvAG4AKABSACkAIABDAFAAVQAgAEUANQAtADIANgA3ADMAIAB2ADQAIABAACAAMgAuADMAMABHAEgAegAiACAATQBhAG4AdQBmAGEAYwB0AHUAcgBlAHIAPQAiAEEAbQBlAHIAaQBjAGEAbgAgAE0AZQBnAGEAdAByAGUAbgBkAHMAIABJAG4AYwAuACIAIABWAGUAcgBzAGkAbwBuAD0AIgBWAFIAVABVAEEATAAgAC0AIAA2ADAAMAAxADcAMAAyACIAIABSAGUAbABlAGEAcwBlAEQAYQB0AGUAPQAiADIAMAAxADcALQAwADYALQAwADIAIAAwADAAOgAwADAAOgAwADAAIgAgAFMAZQByAGkAYQBsAE4AdQBtAGIAZQByAD0AIgAwADAAMAAwAC0AMAAwADEAOAAtADMANgA4ADIALQA0ADcAMAA4AC0ANwA2ADQAMAAtADcANgAwADAALQAzADMAIgAgAFMATQBCAEkATwBTAEIASQBPAFMAVgBlAHIAcwBpAG8AbgA9ACIAMAA5ADAAMAAwADcAIAAiACAALwA+ADwALwByAGUAcwB1AGwAdAA+AA=="~~]]></StateDetails><UserParameters Flags="0" Count="2">
<Param>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</Param><Param>0</Param></UserParameters></StateMessage></ReportBody></Report>

Successfully forwarded State Messages to the MP StateMessage 7/3/2018 11:44:47 AM 5036 (0x13AC)
```

### <a name="review-messages-on-the-site-server"></a>Überprüfen von Meldungen auf dem Standortserver

Öffnen Sie die Datei `statesys.log`, um zu überprüfen, ob die Meldung empfangen und verarbeitet wird. Im folgenden Beispiel sehen Sie `TaskID` am Ende der Meldung neben `<Param>`: Aktivieren Sie die [ausführliche Protokollierung](../../plan-design/hierarchy/about-log-files.md#bkmk_logoptions) in der SMS_STATE_SYSTEM-Komponente, um diese Protokolleinträge anzuzeigen.

``` XML
CMessageProcessor - the cmdline to DB exec dbo.spProcessStateReport N'?<?xml version="1.0" encoding="UTF-
16"?>~~<Report><ReportHeader><Identification><Machine><ClientInstalled>1</ClientInstalled><ClientType>1
</ClientType><ClientID>GUID:DBAC52C9-57E6-47D7-A8D6-E0A5A64B57E6</ClientID><ClientVersion>5.00.8670.1000</ClientVersion>
<NetBIOSName>R613924</NetBIOSName><CodePage>437</CodePage>
<SystemDefaultLCID>1033</SystemDefaultLCID><Priority>0</Priority></Machine></Identification>
<ReportDetails><ReportContent>State Message Data</ReportContent><ReportType>Full</ReportType>
<Date>20180703184447.673000+000</Date><Version>1.0</Version><Format>1.0</Format>
</ReportDetails></ReportHeader><ReportBody><StateMessage MessageTime="20180703184447.517000+000"><Topic ID="7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14" Type="9003" IDType="0" User="" UserSID=""/><State ID="1" Criticality="0"/>
<StateDetails Type="1"><![CDATA["PAA/AHgAbQBsACAAdgBlAHIAcwBpAG8AbgA9ACIAMQAuADAAIgAgAGUAbgBjAG8AZABpAG4AZwA9ACIAdQB0AGYALQAxADYAIgA/AD4APAByAGUAcwB1AGwAdAAgAFIAZQBzAHUAbAB0AEMAbwBkAGUAPQAiADAAIgA+ADwAZQAgAE4AYQBtAGUAPQAiAEkAbgB0AGUAbAAoAFIAKQAgAFgAZQBvAG4AKABSACkAIABDAFAAVQAgAEUANQAtADIANgA3ADMAIAB2ADQAIABAACAAMgAuADMAMABHAEgAegAiACAATQBhAG4AdQBmAGEAYwB0AHUAcgBlAHIAPQAiAEEAbQBlAHIAaQBjAGEAbgAgAE0AZQBnAGEAdAByAGUAbgBkAHMAIABJAG4AYwAuACIAIABWAGUAcgBzAGkAbwBuAD0AIgBWAFIAVABVAEEATAAgAC0AIAA2ADAAMAAxADcAMAAyACIAIABSAGUAbABlAGEAcwBlAEQAYQB0AGUAPQAiADIAMAAxADcALQAwADYALQAwADIAIAAwADAAOgAwADAAOgAwADAAIgAgAFMAZQByAGkAYQBsAE4AdQBtAGIAZQByAD0AIgAwADAAMAAwAC0AMAAwADEAOAAtADMANgA4ADIALQA0ADcAMAA4AC0ANwA2ADQAMAAtADcANgAwADAALQAzADMAIgAgAFMATQBCAEkATwBTAEIASQBPAFMAVgBlAHIAcwBpAG8AbgA9ACIAMAA5ADAAMAAwADcAIAAiACAALwA+ADwALwByAGUAcwB1AGwAdAA+AA=="~~]]></StateDetails><UserParameters Flags="0" Count="2">
<Param>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</Param><Param>0</Param></UserParameters></StateMessage></ReportBody></Report>~~'
```

Überprüfen Sie den Posteingang für Zustandsmeldungen, wenn die Meldungen nicht verarbeitet wurden. Der Standardspeicherort für den Posteingang ist `C:\Program Files\Microsoft Configuration Manager\inboxes\auth\statesys.box\`. Suchen Sie die Dateien an den folgenden Speicherorten:

- Eingehend
- Beschädigt
- Prozess

Überprüfen Sie mithilfe der `TaskID` die Überwachungsansicht für CMPivot über SQL.

``` SQL
select * from vSMS_CMPivotStatus where TaskID='{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}'
```

>[!NOTE]
>Bei Clients, die Version 1810 oder höher verwenden, werden Statusmeldungen nur dann gesendet, wenn die Ausgabe größer als 80 KB ist. Aktivieren Sie bei der Problembehandlung für CMPivot in diesen Fällen die ausführliche Protokollierung in Ihren MPs und der SMS_MESSAGE_PROCESSING_ENGINE des Standortservers, um weitere Informationen zu erhalten. Weitere Informationen zum Aktivieren der ausführlichen Protokollierung finden Sie unter [Protokollierungsoptionen für den Standortserver](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-site).
>
> Verwenden Sie zur Problembehandlung folgende Protokolle:
>
> - `MP_Relay.log`
> - `SMS_MESSAGE_PROCESSING_ENGINE.log`

## <a name="next-steps"></a>Nächste Schritte

- [Using CMPivot (Verwenden von CMPivot)](cmpivot.md)
- [Erstellen und Ausführen von PowerShell-Skripts](../../../apps/deploy-use/create-deploy-scripts.md)
