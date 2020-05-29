---
title: Grundlegendes zu Protokolldateien
titleSuffix: Configuration Manager
description: Verwenden von Protokolldateien bei der Behebung von Problemen, die bei Configuration Manager-Clients und -Standortsystemen auftreten
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b1751e3c-a60c-4ab7-a943-2595df1eb612
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 588bccc533909f2438dc61d6f25b39c3a582c71b
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83879025"
---
# <a name="about-log-files-in-configuration-manager"></a>Grundlegendes zu Protokolldateien in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Von Client- und Standortserverkomponenten in Configuration Manager werden Prozessinformationen in eigenen Protokolldateien aufgezeichnet. Mithilfe der Informationen in diesen Protokolldateien können Sie eventuell auftretende Probleme beheben. Die Client- und Serverkomponentenprotokollierung ist in Configuration Manager standardmäßig aktiviert.

Dieser Artikel enthält allgemeine Informationen zu den Configuration Manager-Protokolldateien. Darin werden die zu verwendenden Tools behandelt, und es wird beschrieben, wie Sie die Protokolle konfigurieren und wo diese zu finden sind. Weitere Informationen zu bestimmten Protokolldateien finden Sie in der [Referenz zu Protokolldateien](log-files.md).


## <a name="how-it-works"></a><a name="BKMK_AboutLogs"></a> Funktionsweise

Die meisten Prozesse in Configuration Manager schreiben Betriebsinformationen in eine spezielle Protokolldatei für den jeweiligen Prozess. Diese Protokolldateien werden durch die **.LOG** - oder **.LO_** -Erweiterung identifiziert. Configuration Manager schreibt in die LOG-Protokolldatei, bis das Protokoll die maximale Größe erreicht hat. Wenn dies eintritt, wird die LOG-Datei in eine Datei mit dem gleichen Namen, aber der Erweiterung „.LO_“ kopiert, und der Prozess oder die Komponente schreibt weiterhin in die LOG-Datei. Wenn die Größe der LOG-Datei erneut den zulässigen Maximalwert erreicht, wird die LO_-Datei überschrieben und der Prozess wiederholt. Bei einigen Komponenten wird ein Protokolldateiverlauf geführt, indem dem Namen der Protokolldatei ein Datum- und Zeitstempel hinzugefügt wird, wobei die Erweiterung „.LOG“ erhalten bleibt.


## <a name="log-viewer-tools"></a><a name="bkmk_tools"></a> Tools für die Protokollanzeige

Alle Protokolldateien im Configuration Manager liegen im Nur-Text-Format vor, sodass sie in einem Texteditor wie Editor angezeigt werden können. Die Protokolle enthalten eine eindeutige Formatierung, für deren Anzeige sich eines der folgenden spezialisierten Tools empfiehlt:

- [CMTrace](#cmtrace)
- [OneTrace](#onetrace)
- [Protokollanzeige des Supportcenters](#support-center-log-viewer)

### <a name="cmtrace"></a>CMTrace

Verwenden Sie zur Anzeige der Protokolle das Configuration Manager-Protokollanzeigetool **CMTrace**. Es befindet sich im Ordner `\SMSSetup\Tools` der Configuration Manager-Quellmedien. Das CMTrace-Tool wird ebenfalls allen Startimages hinzugefügt, die in die Softwarebibliothek aufgenommen werden. Das CMTrace-Protokollanzeigetool wird automatisch mit dem Configuration Manager-Client installiert.<!--1357971--> Weitere Informationen finden Sie unter [CMTrace](../../support/cmtrace.md).

### <a name="onetrace"></a>OneTrace

Ab Version 1906 ist **OneTrace** als neue Protokollanzeige im Supportcenter verfügbar. Die Funktionsweise ähnelt der von CMTrace, bietet jedoch einige Verbesserungen. Weitere Informationen finden Sie unter [Supportcenter – OneTrace](../../support/support-center-onetrace.md).

### <a name="support-center-log-viewer"></a>Protokollanzeige des Supportcenters

Im **Supportcenter** steht eine moderne Protokollanzeige zur Verfügung. Dieses Tool ersetzt CMTrace und stellt eine anpassbare Benutzeroberfläche mit Registerkarten und andockbaren Fenstern zur Verfügung. Er verfügt über eine Darstellungsschicht und kann große Protokolldateien innerhalb weniger Sekunden laden. Weitere Informationen finden Sie in der [Referenz – Protokollanzeige des Supportcenters](../../support/support-center-ui-reference.md#bkmk_log-viewer).

> [!Note]  
> Supportcenter und OneTrace arbeiten mit Windows Presentation Foundation (WPF). Diese Komponente ist unter Windows PE nicht verfügbar. Verwenden Sie CMTrace weiterhin in Startimages mit Tasksequenzbereitstellungen.


## <a name="configure-logging-options"></a><a name="bkmk_logoptions"></a> Konfigurieren der Protokollierungsoptionen

Sie können die Konfiguration der Protokolldateien ändern, z. B. Ausführlichkeitsstufe, Größe und Verlauf. Es gibt mehrere Möglichkeiten, diese Einstellungen zu ändern:

- [Während der Clientinstallation](#bkmk_logoptions-clientprop)
- [Verwenden des Dienst-Managers für Configuration Manager](#bkmk_logoptions-sm)
- [Mithilfe der Windows-Registrierung](#bkmk_logoptions-registry)
- [über die Configuration Manager-Konsole](#bkmk_logoptions-console)

### <a name="configure-logging-options-during-client-installation"></a><a name="bkmk_logoptions-clientprop"></a> Konfigurieren von Protokollierungsoptionen während der Clientinstallation

Sie können die Konfiguration der Clientprotokolldateien während der Installation festlegen. Verwenden Sie die folgenden Eigenschaften:

- CCMENABLELOGGING
- CCMDEBUGLOGGING
- CCMLOGLEVEL
- CCMLOGMAXHISTORY
- CCMLOGMAXSIZE

Weitere Informationen finden Sie unter [Informationen zu Clientinstallationseigenschaften](../../clients/deploy/about-client-installation-properties.md#clientMsiProps).

### <a name="configure-logging-options-by-using-configuration-manager-service-manager"></a><a name="bkmk_logoptions-sm"></a> Konfigurieren der Protokollierungsoptionen mithilfe des Dienst-Managers für Configuration Manager

Sie können für Configuration Manager den Speicherort von Protokolldateien und die Größe dieser Dateien ändern.  

Führen Sie die folgenden Schritte aus, um die Größe, den Namen und den Speicherort von Protokolldateien zu ändern oder mehrere Komponenten für das Schreiben in eine einzige Protokolldatei zu konfigurieren:  

#### <a name="modify-logging-for-a-component"></a>Ändern der Protokollierung für eine Komponente  

1. Öffnen Sie in der Configuration Manager-Konsole den Arbeitsbereich **Überwachung** erweitern Sie den **Systemstatus**, und wählen Sie den Knoten **Standortstatus** oder **Komponentenstatus** aus.  

2. Klicken Sie im Menüband auf **Starten**, und wählen Sie anschließend **Dienst-Manager für Configuration Manager** aus.  

3. Wenn der Dienst-Manager für Configuration Manager geöffnet wird, stellen Sie eine Verbindung mit dem zu verwaltenden Standort her. Wenn der zu verwaltende Standort nicht angezeigt wird, klicken Sie auf **Standort**, dann auf **Verbinden**, und geben Sie dann den Namen des Standortservers für den gewünschten Standort ein.  

4. Erweitern Sie den Standort und wechseln Sie zu **Komponenten** oder **Server**, je nachdem, wo die zu verwaltenden Komponenten sich befinden.  

5. Wählen Sie im rechten Fensterbereich eine oder mehrere Komponenten aus.  

6. Klicken Sie im Menü **Komponente** auf **Protokollierung**.  

7. Legen Sie im Dialogfeld **Configuration Manager-Komponentenprotokollierung** die verfügbaren Konfigurationsoptionen für Ihre Auswahl fest.  

8. Klicken Sie auf **OK**, um die Konfiguration zu speichern.  

### <a name="configure-logging-options-by-using-the-windows-registry"></a><a name="bkmk_logoptions-registry"></a> Konfigurieren von Protokollierungsoptionen mithilfe der Windows-Registrierung

<!-- SCCMDocs#992 -->
Verwenden Sie die Windows-Registrierung auf den Servern oder Clients, um die folgenden Protokollierungsoptionen zu ändern:

- Ausführlichkeitsstufe
- Maximaler Verlauf
- Maximale Größe

Bei der Problembehebung können Sie die ausführliche Protokollierung für Configuration Manager aktivieren, sodass zusätzliche Details in den Protokolldateien erfasst werden.

> [!Warning]
> Eine falsche Konfiguration dieser Einstellungen kann bewirken, dass Configuration Manager große Informationsmengen oder überhaupt keine Informationen protokolliert. Diese Daten können für die Problembehandlung nützlich sein. Gehen Sie jedoch vorsichtig vor, wenn Sie diese Werte an Produktionsstandorten ändern. Testen Sie diese Änderungen immer zuerst in einer Laborumgebung. Es kann zu einer übermäßigen Protokollierung kommen, wodurch es möglicherweise schwierig wird, die relevanten Informationen in den Protokolldateien zu finden.

Starten Sie nach dem Ändern dieser Registrierungseinstellungen die Komponente neu:

- Wenn Sie die Clienteinstellungen ändern, starten Sie den **SMS-Agent-Host**-Dienst (CcmExec).
- Wenn Sie die Servereinstellungen ändern, starten Sie den **SMS-Executive**-Dienst neu.

Die Registrierungseinstellungen variieren je nach Komponente:

- [Client und Verwaltungspunkt](#bkmk_reg-client)
- [Standortserver](#bkmk_reg-site)
- [Standortsystemrolle](#bkmk_reg-role)
- [Configuration Manager-Konsole](#bkmk_reg-console)

#### <a name="client-and-management-point-logging-options"></a><a name="bkmk_reg-client"></a> Protokollierungsoptionen für Client und Verwaltungspunkt

Wenn Sie Protokollierungsoptionen für alle Komponenten auf einem Client oder in einem Verwaltungspunkt-Standortsystem konfigurieren möchten, konfigurieren Sie diese **REG_DWORD**-Werte unter dem folgenden Windows-Registrierungsschlüssel:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Logging\@Global`

|Name  |Werte  |Beschreibung  |
|---------|---------|---------|
|LogLevel|`0`: Ausführlich<br>`1`: Standard<br>`2`: Warnungen und Fehler<br>`3`: Nur Fehler|Die Detailebene der in die Protokolldateien zu schreibenden Informationen.|
|LogMaxHistory|Eine beliebige ganze Zahl größer als oder gleich 0. Beispiel:<br>`0`: Kein Verlauf<br>`1`: Standard|Wenn eine Protokolldatei die maximale Größe erreicht, benennt der Client diese als Sicherungsdatei um und erstellt eine neue Protokolldatei. Geben Sie an, wie viele frühere Versionen aufbewahrt werden sollen.|
|LogMaxSize|Eine beliebige ganze Zahl größer als oder gleich 10.000. Beispiel:<br>250000|Die maximale Protokolldateigröße in Bytes. Wenn ein Protokoll die angegebene Größe erreicht, benennt der Client diese als Verlaufsdatei um und erstellt eine neue Datei. Der Standardwert beträgt 250.000 Bytes.|

> [!Note]  
> Ändern Sie keine anderen Werte, die in diesem Registrierungsschlüssel möglicherweise vorhanden sind.

Für das erweiterte Debuggen können Sie auch diesen **REG_SZ**-Wert unter dem folgenden Windows-Registrierungsschlüssel hinzufügen:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Logging\DebugLogging`

|Name  |Werte  |Beschreibung  |
|---------|---------|---------|
|Aktiviert | `True`: Debugprotokolle aktivieren<br>`False`: Debugprotokolle deaktivieren |Aktiviert die Debugprotokollierung für die Problembehandlung.|

Diese Einstellung bewirkt, dass der Client Basisinformationen für die Problembehandlung protokolliert. Verwenden Sie diese Einstellung nach Möglichkeit nicht an Produktionsstandorten. Es kann zu einer übermäßigen Protokollierung kommen, wodurch es möglicherweise schwierig wird, die relevanten Informationen in den Protokolldateien zu finden. Sie müssen diese Einstellung nach dem Beheben des Problems deaktivieren.

#### <a name="site-server-logging-options"></a><a name="bkmk_reg-site"></a> Protokollierungsoptionen für den Standortserver

Sie können Einstellungen global oder für eine bestimmte Komponente auf dem Configuration Manager-Standortserver konfigurieren.

Konfigurieren Sie diese Werte unter dem folgenden Windows-Registrierungsschlüssel:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\Tracing`

|Name  |Werte  |Typ  |Beschreibung
|---------|---------|---------|---------|
|SqlEnabled| `1`: SQL-Ablaufverfolgung aktivieren<br> `0`: SQL-Ablaufverfolgung deaktivieren |REG_DWORD|Fügen Sie die SQL-Ablaufprotokollierung allen Standortserverprotokollen hinzu.|
|ArchiveEnabled| `1`: Protokollarchive aktivieren<br> `0`: Protokollarchive deaktivieren | REG_DWORD |Archivieren Sie Standortserverprotokolle an einem separaten Speicherort, um den Verlauf beizubehalten.|
|ArchivePath| Ein gültiger Ordnerpfad, z. B. `C:\Logs\Archive` | REG_SZ |Der Pfad zum Archivieren von Standortserverprotokollen.|

Aktivieren Sie die SQL-Ablaufverfolgung nur für die Problembehandlung. Verwenden Sie sie nach Möglichkeit nicht an Produktionsstandorten. Es kann zu einer übermäßigen Protokollierung kommen, wodurch es möglicherweise schwierig wird, die relevanten Informationen in den Protokolldateien zu finden. Sie müssen diese Einstellung nach dem Beheben des Problems deaktivieren.

> [!Note]  
> Ändern Sie keine anderen Werte, die in diesem Registrierungsschlüssel möglicherweise vorhanden sind.

Wenn Sie Protokollierungsoptionen für eine bestimmte Serverkomponente konfigurieren möchten, konfigurieren Sie diese **REG_DWORD**-Werte unter dem folgenden Windows Registry-Schlüssel:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\Tracing\<ComponentName>`

|Name  |Werte  |Beschreibung  |
|---------|---------|---------|
|LoggingLevel|`0`: Ausführlich<br>`1`: Standard<br>`2`: Warnungen und Fehler<br>`3`: Nur Fehler|Die Detailebene der in die Protokolldateien zu schreibenden Informationen.|
|LogMaxHistory|Eine beliebige ganze Zahl größer als oder gleich 0. Beispiel:<br>`0`: Kein Verlauf<br>`1`: Standard|Wenn eine Protokolldatei die maximale Größe erreicht, benennt der Server diese als Sicherungsdatei um und erstellt eine neue Protokolldatei. Geben Sie an, wie viele frühere Versionen aufbewahrt werden sollen.|
|MaxFileSize|Eine beliebige ganze Zahl größer als oder gleich 10.000. Beispiel:<br>250000|Die maximale Protokolldateigröße in Bytes. Wenn ein Protokoll die angegebene Größe erreicht, benennt der Client diese als Verlaufsdatei um und erstellt eine neue Datei. Der Standardwert beträgt 250.000 Bytes.|
|DebugLogging| `1`: Debugprotokolle aktivieren<br>`0`: Debugprotokolle deaktivieren |Aktiviert die Debugprotokollierung für die Problembehandlung.|

Die DebugLogging-Einstellung bewirkt, dass der Server Basisinformationen für die Problembehandlung protokolliert. Verwenden Sie diese Einstellung nach Möglichkeit nicht an Produktionsstandorten. Es kann zu einer übermäßigen Protokollierung kommen, wodurch es möglicherweise schwierig wird, die relevanten Informationen in den Protokolldateien zu finden. Sie müssen diese Einstellung nach dem Beheben des Problems deaktivieren.

> [!Note]  
> Ändern Sie keine anderen Werte, die in diesem Registrierungsschlüssel möglicherweise vorhanden sind.

#### <a name="site-system-role-logging-options"></a><a name="bkmk_reg-role"></a> Protokollierungsoptionen für Standortsystemrollen

Sie können Einstellungen global oder für eine bestimmte Komponente in einem Standortsystem konfigurieren, das eine Configuration Manager-Serverrolle hostet.

Wenn Sie Protokollierungsoptionen für eine bestimmte Serverkomponente konfigurieren möchten, konfigurieren Sie diese **REG_DWORD**-Werte unter dem folgenden Windows Registry-Schlüssel:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\<ComponentName>\Logging`

Legen Sie für die Verteilungspunktrolle beispielsweise Folgendes fest:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP\Logging`

|Name  |Werte  |Beschreibung  |
|---------|---------|---------|
|LogLevel|`0`: Ausführlich<br>`1`: Standard<br>`2`: Warnungen und Fehler<br>`3`: Nur Fehler|Die Detailebene der in die Protokolldateien zu schreibenden Informationen.|
|LogMaxHistory|Eine beliebige ganze Zahl größer als oder gleich 0. Beispiel:<br>`0`: Kein Verlauf<br>`1`: Standard|Wenn eine Protokolldatei die maximale Größe erreicht, benennt der Server diese als Sicherungsdatei um und erstellt eine neue Protokolldatei. Geben Sie an, wie viele frühere Versionen aufbewahrt werden sollen.|
|LogMaxSize|Eine beliebige ganze Zahl größer als oder gleich 10.000. Beispiel:<br>250000|Die maximale Protokolldateigröße in Bytes. Wenn ein Protokoll die angegebene Größe erreicht, benennt der Server diese als Verlaufsdatei um und erstellt eine neue Datei. Der Standardwert beträgt 250.000 Bytes.|

> [!Note]  
> Ändern Sie keine anderen Werte, die in diesem Registrierungsschlüssel möglicherweise vorhanden sind.

#### <a name="configuration-manager-console-logging-options"></a><a name="bkmk_reg-console"></a> Protokollierungsoptionen für die Configuration Manager-Konsole

Gehen Sie wie folgt vor, um die Ausführlichkeitsstufe der Datei „AdminUI.log“ für die Configuration Manager-Konsole zu ändern:

1. Öffnen Sie die Konsolenkonfigurationsdatei **Microsoft.ConfigurationManagement.exe.config** in einem XML-Editor wie Editor. Die Standardkonfigurationsdatei befindet sich an folgendem Speicherort: `C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`

    > [!IMPORTANT]
    > Ab Version 1910 wurde dieser Pfad so geändert, dass der `Microsoft Endpoint Manager`-Ordner verwendet wird. Stellen Sie sicher, dass Sie keine ältere Version der Datei verwenden, die möglicherweise in einem anderen Ordner vorhanden ist.

1. Ändern Sie unter dem Element **system.diagnostics** > **sources** > **source** das Attribut **switchValue** von `Error` in `Verbose`. Beispiel:

    Original: `<source name="SmsAdminUISnapIn" switchValue="Error">` Neu: `<source name="SmsAdminUISnapIn" switchValue="Verbose" >`

1. Speichern Sie die Datei, und starten Sie die Konsole neu.

### <a name="configure-logging-options-in-the-configuration-manager-console"></a><a name="bkmk_logoptions-console"></a> Konfigurieren von Protokollierungsoptionen in der Configuration Manager-Konsole

<!-- 4433455 -->

Ab Version 1910 können Sie die ausführliche Protokollierung für einen Client oder eine Sammlung über die Konsole aktivieren oder deaktivieren:

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Bestand und Konformität**, wählen Sie den Knoten **Geräte** und dann ein Zielgerät aus.

1. Wählen Sie im Menüband auf der Registerkarte **Home** in der Gruppe **Geräte** die Option **Clientdiagnose** aus. Wählen Sie eine der verfügbaren Aktionen aus.

Weitere Informationen finden Sie unter [Clientdiagnose](../../clients/manage/client-notification.md#client-diagnostics).

## <a name="locating-log-files"></a><a name="BKMK_LogLocation"></a> Suchen von Protokolldateien

In Configuration Manager und abhängigen Komponenten werden Protokolldateien an verschiedenen Speicherorten gespeichert. Diese Speicherorte sind abhängig vom Prozess, mit dem die Protokolldatei erstellt wird, sowie von der Konfiguration Ihrer Umgebung.

Standardmäßig werden folgende Speicherorte verwendet. Wenn Sie die Installationsverzeichnisse in Ihrer Umgebung angepasst haben, können die tatsächlichen Pfade abweichen.

- Client: `C:\Windows\CCM\logs`
- Server: `C:\Program Files\Microsoft Configuration Manager\Logs`
- Verwaltungspunkt: `C:\SMS_CCM\Logs`
- Configuration Manager-Konsole: `C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\AdminUILog`
- IIS: `C:\inetpub\logs\logfiles\w3svc1`

### <a name="task-sequence-log-locations"></a>Protokollspeicherorte für Tasksequenzen

Der Speicherort der Tasksequenzen-Protokolldatei **smsts.log** variiert je nach Phase der Tasksequenz:

- In Windows PE vor dem Schritt [Datenträger formatieren und partitionieren](../../../osd/understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk): `X:\Windows\temp\smstslog\smsts.log` (X ist das Windows PE-RAM-Laufwerk)
- In Windows PE nach dem Schritt **Datenträger formatieren und partitionieren**: `X:\smstslog\smsts.log`, dann nach `C:\_SMSTaskSequence\Logs\smstslog\smsts.log` kopiert, wenn das Laufwerk bereit ist
- Im neuen Windows-Betriebssystem vor dem Installieren des Clients: `C:\_SMSTaskSequence\Logs\smstslog\smsts.log`
- In Windows nach dem Installieren des Clients: `C:\Windows\CCM\Logs\smstslog\smsts.log`
- In Windows nach Abschluss der Tasksequenz: `C:\Windows\CCM\Logs\smsts.log`

> [!Tip]  
> Die schreibgeschützte Tasksequenz-Variable [_SMSTSLogPath](../../../osd/understand/task-sequence-variables.md#SMSTSLogPath) enthält immer den Pfad der aktuellen Protokolldatei.


## <a name="see-also"></a>Weitere Informationen:

- [Protokolldateireferenz](log-files.md)

- [Supportcenter – OneTrace](../../support/support-center-onetrace.md)

- [Protokolldateianzeige des Supportcenters](../../support/support-center.md#support-center-log-file-viewer)

- [CMTrace](../../support/cmtrace.md)
