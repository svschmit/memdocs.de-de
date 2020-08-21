---
title: Änderungen an CMPivot
titleSuffix: Configuration Manager
description: Erfahren Sie, welche Änderungen an CMPivot in den verschiedenen Versionen von Configuration Manager vorgenommen wurden.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: a49a9564-0863-44c3-991e-a8e271fed586
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 20b23cec74ae3d201bc81fe1834e87e7eb8fcc13
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129526"
---
# <a name="changes-to-cmpivot"></a>Änderungen an CMPivot

Anhand der folgenden Informationen erfahren Sie, welche Änderungen an [CMPivot](cmpivot.md) in den verschiedenen Versionen von Configuration Manager vorgenommen wurden:

## <a name="cmpivot-changes-for-version-2006"></a><a name="bkmk_2006"></a> Änderungen an CMPivot in Version 2006
<!--6518631-->

Ab Version 2006 sind die folgenden Verbesserungen an CMPivot erfolgt:

- [Eigenständig verwendetes CMPivot](cmpivot.md#bkmk_standalone) und das über die Verwaltungskonsole gestartete CMPivot wurden zusammengeführt. Wenn Sie CMPivot über die Verwaltungskonsole starten, wird die gleiche zugrunde liegende Technologie wie bei der eigenständigen CMPivot-Version verwendet, um ein einheitliches Szenario zu erzielen.

- Verbesserte Tastaturnavigation in CMPivot.

- CMPivot kann nun auf einem einzelnen oder mehreren Geräten im Knoten „Geräte“ ausgeführt werden, ohne eine Gerätesammlung auswählen zu müssen. Durch diese Verbesserung können Benutzer, z. B. Helpdesk-Mitarbeiter, CMPivot-Abfragen für bestimmte Geräte außerhalb einer vorab erstellten Sammlung leichter erstellen.
   - Wählen Sie in einer Gerätesammlung ein einzelnes oder mehrere Geräte aus und dann **CMPivot starten** aus.

- Sie können nach Rückgabe von Geräten in einer Abfragelistenansicht **Gerätepivot** für ein oder mehrere Geräte auswählen, dann pivotieren und Abfragen nur für diese Geräte ausführen, um detaillierte Informationen zu erhalten. Durch diese Änderung können Sie einen Drilldown durchführen, ohne die größere Gruppe von Geräten aus der ursprünglichen Sammlung abzufragen. **Pivotieren nach** wurde durch **Gerätepivot** ersetzt.
   - Wählen Sie innerhalb eines vorhandenen CMPivot-Vorgangs in der Ausgabe ein einzelnes oder mehrere Geräte aus. Klicken Sie mit der rechten Maustaste, und pivotieren Sie mithilfe der Option **Gerätepivot**. Mit dieser Aktion wird eine separate CMPivot-Instanz gestartet, die sich auf die ausgewählten Geräte beschränkt. Dies vereinfacht das Pivotieren und Abfragen nur der Geräte, die Sie benötigen, ohne dafür eine Sammlung erstellen zu müssen.

- Wenn Sie CMPivot für ein einzelnes Gerät ausführen, wird der Gerätename oben im Fenster aufgeführt. Bei mehreren Geräten wird die Anzahl der ausgewählten Geräte oben im Fenster angegeben.
- Die Option **Sammlung erstellen** auf der Registerkarte „Abfragezusammenfassung“ wurde entfernt, da für CMPivot keine Sammlung mehr abgefragt werden muss. Führen Sie den Vorgang **Gerätepivot** aus, um eine neue Instanz von CMPivot zu öffnen, die auf die Geräte beschränkt ist, die Sie abfragen möchten. **Sammlung erstellen** ist weiterhin im Hauptmenü verfügbar.

![Gerätepivot für mehrere Geräte mit mithilfe von CMPivot](./media/6518631-cmpivot-multi-select.png)


## <a name="cmpivot-changes-for-version-2002"></a><a name="bkmk_2002"></a> Änderungen an CMPivot in Version 2002
<!--5870934-->
Das Navigieren zu CMPivot-Entitäten wurde vereinfacht. Ab Configuration Manager, Version 2002 können Sie CMPivot-Entitäten durchsuchen. Außerdem wurden neue Symbole hinzugefügt, um die Entitäten und Entitätsobjekttypen leicht unterscheiden zu können.

![Suchen von CMPivot-Entitäten](./media/5870934-search-cmpivot-entities.png)


## <a name="cmpivot-changes-for-version-1910"></a><a name="bkmk_cmpivot1910"></a> Änderungen an CMPivot in Version 1910
<!--5410930, 3197353-->
Ab Version 1910 wurde CMPivot erheblich optimiert, um den Netzwerkdatenverkehr und die Auslastung von Servern zu reduzieren. Außerdem wurden mehrere Entitäten und Entitätserweiterungen hinzugefügt, um Unterstützung bei der Problembehandlung und Suche zu bieten. Die folgenden Änderungen wurden für CMPivot in Version 1910 eingeführt:

- [Optimierungen der CMPivot-Engine](#bkmk_optimization)
- Zusätzliche Entitäten und Entitätserweiterungen:
  - Windows-Ereignisprotokolle ([WinEvent](#bkmk_WinEvent))
  - Dateiinhalt ([FileContent](#bkmk_File))
  - Durch Prozesse geladene DLLs ([ProcessModule](#bkmk_ProcessModule))
  - Azure Active Directory-Informationen ([AADStatus](#bkmk_AadStatus))
  - Endpoint Protection-Status ([EPStatus](#bkmk_EPStatus))
- [Abfrageauswertung für lokales Gerät mit der eigenständigen CMPivot-Version](#bkmk_local-eval)
- [Weitere Erweiterungen für CMPivot](#bkmk_Other)


### <a name="optimizations-to-the-cmpivot-engine"></a><a name="bkmk_optimization"></a> Optimierungen der CMPivot-Engine
<!--3197353-->
CMPivot wurde in Version 1910 optimiert, um den Netzwerkdatenverkehr und die Auslastung von Servern zu reduzieren. Viele Abfragevorgänge werden jetzt direkt auf dem Client und nicht auf den Servern ausgeführt. Diese Änderung bedeutet auch, dass bei einigen CMPivot-Vorgängen minimale Daten aus der ersten Abfrage zurückgegeben werden. Wenn Sie die Daten genauer untersuchen möchten, um weitere Informationen zu erhalten, können Sie eine neue Abfrage ausführen, um die zusätzlichen Daten vom Client abzurufen. Wenn Sie eine „summarize count“-Abfrage ausgeführt haben, wurde zuvor beispielsweise ein großes Dataset an den Server zurückgegeben.  Zwar konnten die Daten bei der Rückgabe eines großen Datasets sofort angezeigt werden, allerdings war oft nur die zusammengefasste Anzahl erforderlich. Wenn Sie in Version 1910 einen bestimmten Client genauer untersuchen möchten, wird eine andere Sammlung der Daten durchgeführt, um die von Ihnen angeforderten zusätzlichen Daten zurückzugeben. Diese Änderung führt zu einer besseren Leistung und Skalierbarkeit bei Abfragen für eine große Anzahl von Clients. <!--3197353, 5458337-->

#### <a name="examples"></a>Beispiele

Die Optimierungen von CMPivot verringern die Netzwerk- und Server-CPU-Auslastung erheblich, die für die Durchführung von CMPivot-Abfragen benötigt wird. Mit diesen Optimierungen können wir nun in Echtzeit Gigabytes von Clientdaten durchsehen. Die folgenden Abfragen veranschaulichen diese Optimierungen:

- Durchsuchen aller Ereignisprotokolle auf allen Clients in Ihrem Unternehmen auf Authentifizierungsfehler:

   ``` Kusto
   EventLog('Security')
   | where  EventID == 4673
   | summarize count() by Device
   | order by count_ desc
   ```

- Suchen nach einer Datei nach Hash:

   ``` Kusto
   Device
   | join kind=leftouter ( File('%windir%\\system32\\*.exe')
   | where SHA256Hash == 'A92056D772260B39A876D01552496B2F8B4610A0B1E084952FE1176784E2CE77')
   | project Device, MalwareFound = iif( isnull(FileName), 'No', 'Yes')
   ```

### <a name="wineventlognametimespan"></a><a name="bkmk_WinEvent"></a> WinEvent(\<logname>,[\<timespan>])

Mit dieser Entität werden Ereignisse aus Ereignisprotokollen und Protokolldateien der Ereignisablaufverfolgung abgerufen. Die Entität ruft Daten aus Ereignisprotokollen ab, die von der Windows-Ereignisprotokolltechnologie generiert werden. Die Entität ruft auch Ereignisse in Protokolldateien ab, die von der Ereignisablaufverfolgung für Windows (Event Tracing for Windows, ETW) generiert werden. WinEvent berücksichtigt standardmäßig Ereignisse, die innerhalb der letzten 24 Stunden aufgetreten sind. Diese Standardeinstellung kann jedoch durch Einschließen eines timespan-Werts überschrieben werden.

``` Kusto
WinEvent('Microsoft-Windows-HelloForBusiness/Operational', 1d)
| where LevelDisplayName =='Error'
| summarize count() by Device
```

### <a name="filecontentfilename"></a><a name="bkmk_File"></a> FileContent(\<filename>)

FileContent wird verwendet, um den Inhalt einer Textdatei abzurufen.

``` Kusto
FileContent('c:\\windows\\SMSCFG.ini')
| where Content startswith  'SMS Unique Identifier='
| project Device, SMSId= substring(Content,22)
```

### <a name="processmoduleprocessname"></a><a name="bkmk_ProcessModule"></a> ProcessModule(\<processname>)  

Mit dieser Entität werden die von einem bestimmten Prozess geladenen Module (DLLs) enumeriert. ProcessModule ist sehr hilfreich beim Hunting nach Schadsoftware, die in sich in legitimen Prozessen verbirgt.  

``` Kusto
ProcessModule('powershell')
| summarize count() by ModuleName
| order by count_ desc
```

### <a name="aadstatus"></a><a name="bkmk_AadStatus"></a> AadStatus

Diese Entität kann verwendet werden, um die aktuellen Azure Active Directory-Identitätsinformationen von einem Gerät abzurufen.

``` Kusto
AadStatus
| project Device, IsAADJoined=iif( isnull(DeviceId),'No','Yes')
| summarize DeviceCount=count() by IsAADJoined
| render piechart
```

### <a name="epstatus"></a><a name="bkmk_EPStatus"></a> EPStatus

Mit EPStatus wird der Status von Antischadsoftware abgerufen, die auf dem Computer installiert ist.

``` Kusto
EPStatus
| project Device, QuickScanAge=datetime_diff('day',now(),QuickScanEndTime)
| summarize DeviceCount=count() by QuickScanAge
| order by QuickScanAge
| render barchart
```

### <a name="local-device-query-evaluation-using-cmpivot-standalone"></a><a name="bkmk_local-eval"></a> Abfrageauswertung für lokales Gerät mit der eigenständigen CMPivot-Version
<!--3197353-->
Wenn Sie CMPivot außerhalb der Configuration Manager-Konsole verwenden, können Sie nur das lokale Gerät abfragen, ohne dass hierzu die Configuration Manager-Infrastruktur erforderlich ist. Sie können ab sofort die CMPivot-Azure Log Analytics-Abfragen nutzen, um schnell WMI-Informationen auf dem lokalen Gerät anzuzeigen. Dies ermöglicht auch die Überprüfung und Optimierung von CMPivot-Abfragen, bevor diese in einer größeren Umgebung ausgeführt werden. Die eigenständige CMPivot-Version steht nur in englischer Sprache zur Verfügung. Weitere Informationen zur eigenständigen CMPivot-Version finden Sie unter [Installieren der eigenständigen CMPivot-Version](#bkmk_standalone).

#### <a name="known-issues-for-local-device-query-evaluation"></a>Bekannte Probleme bei der Abfrageauswertung für lokale Geräte

 - Wenn Sie auf **diesem PC** eine Abfrage für eine WMI-Entität durchführen, auf die Sie keinen Zugriff haben (z. B. eine gesperrte WMI-Klasse), wird möglicherweise ein Absturz in CMPivot angezeigt. Führen Sie CMPivot mit einem Konto mit erhöhten Rechten aus, um diese Entitäten abzufragen. <!--5753242-->
- Wenn Sie auf **diesem PC** eine Abfrage für nicht WMI-basierte Entitäten durchführen, wird ein **ungültiger Namespace** oder eine mehrdeutige Ausnahme angezeigt.
- Führen Sie die eigenständige CMPivot-Version über die Startmenüverknüpfung und nicht direkt über den Pfad der ausführbaren Datei aus. <!--5787962-->

### <a name="other-enhancements"></a><a name="bkmk_Other"></a> Weitere Erweiterungen

- Sie können mithilfe des neuen `like`-Operators Abfragen für reguläre Ausdrücke ausführen. Beispiel:<!--3056858-->
  
   ```kusto
   //Find BIOS manufacture that contains any word like Micro, such as Microsoft
   Bios
   | where Manufacturer like '%Micro%'
   ```

- Wir haben die Entitäten **CcmLog()** und **EventLog()** aktualisiert, sodass diese standardmäßig nur Meldungen der letzten 24 Stunden berücksichtigen. Dieses Verhalten kann durch Übergeben eines optionalen timespan-Werts überschrieben werden. Beispielsweise werden bei der folgenden Abfrage Ereignisse der letzten Stunde berücksichtigt:

   ```kusto
   CcmLog('Scripts',1h)
   ```

- Die Entität **File()** wurde aktualisiert, um Informationen zu ausgeblendeten und Systemdateien zu erfassen, und enthält den MD5-Hash. Ein MD5-Hash ist zwar nicht so genau wie ein SHA256-Hash, ist jedoch tendenziell der am häufigsten gemeldete Hash in den meisten Bulletins zu Schadsoftware.  

- Sie können Kommentare zu Abfragen hinzufügen.<!-- 5431463 --> Dieses Verhalten ist sehr nützlich bei der Freigabe von Abfragen. Beispiel:

    ``` Kusto
    //Get the top ten devices sorted by user
    Device
    | top 10 by UserName
    ```

- CMPivot stellt automatisch eine Verbindung zum letzten Speicherort her.<!-- 5420395 --> Nach dem Start von CMPivot können Sie bei Bedarf eine Verbindung mit einem neuen Speicherort herstellen.

- Wählen Sie im Menü **Export** die neue Option **Abfragelink in Zwischenablage**.<!-- 5431577 --> Diese Aktion kopiert einen Link in die Zwischenablage, den Sie für andere Benutzer freigeben können. Beispiel:

    `cmpivot:Ly8gU2FtcGxlIHF1ZXJ5DQpPcGVyYXRpbmdTeXN0ZW0NCnwgc3VtbWFyaXplIGNvdW50KCkgYnkgQ2FwdGlvbg0KfCBvcmRlciBieSBjb3VudF8gYXNjDQp8IHJlbmRlciBiYXJjaGFydA==`

    Dieser Link öffnet CMPivot in einer eigenständigen Version mit der folgenden Abfrage:

    ``` Kusto
    // Sample query
    OperatingSystem
    | summarize count() by Caption
    | order by count_ asc
    | render barchart
    ```

    > [!TIP]
    > Damit dieser Link funktioniert, müssen Sie die [eigenständige CMPivot-Version installieren](#bkmk_standalone).

- Wenn das Gerät in Microsoft Defender Advanced Threat Protection (ATP) registriert ist, klicken Sie in den Abfrageergebnissen mit der rechten Maustaste auf das Gerät, um das Onlineportal für **Microsoft Defender Security Center** zu starten.

### <a name="known-issues-for-cmpivot-in-version-1910"></a>Bekannte Probleme für CMPivot in Version 1910

- Das Banner „Maximale Ergebnisse“ wird möglicherweise nicht angezeigt, wenn der Grenzwert erreicht ist. <!--5431427-->
  - Jeder Client ist auf 128 KB pro Abfrage beschränkt.
  - Die Ergebnisse werden möglicherweise abgeschnitten, wenn die Ergebnisse der Abfrage 128 KB überschreiten.

## <a name="cmpivot-changes-for-version-1906"></a><a name="bkmk_cmpivot1906"></a> Änderungen an CMPivot in Version 1906

Ab Version 1906 wurden CMPivot die folgenden Elemente hinzugefügt:

- [Verknüpfungen, zusätzliche Operatoren und Aggregatoren](#bkmk_cmpivot_joins)
- [Zur Rolle „Sicherheitsadministrator“ hinzugefügte CMPivot-Berechtigungen](#bkmk_cmpivot_secadmin1906)
- [Eigenständige Verwendung von CMPivot](#bkmk_standalone)

### <a name="add-joins-additional-operators-and-aggregators-in-cmpivot"></a><a name="bkmk_cmpivot_joins"></a> Hinzufügen von Verknüpfungen, zusätzlichen Operatoren und Aggregatoren in CMPivot
<!--4054074-->
Sie verfügen nun über zusätzliche arithmetische Operatoren, Aggregatoren und die Möglichkeit, Abfrageverknüpfungen hinzuzufügen, wie etwa Registrierung und Datei gemeinsam zu verwenden. Die folgenden Elemente wurden hinzugefügt:

#### <a name="table-operators"></a>Tabellenoperatoren

|Tabellenoperatoren| Beschreibung|
|-----|-----|
| [join](https://docs.microsoft.com/azure/kusto/query/joinoperator)| Zusammenführen der Zeilen von zwei Tabellen nach der übereinstimmenden Zeile für das gleiche Gerät, um eine neue Tabelle zu bilden|
|render|Gibt die Ergebnisse als grafische Ausgabe wieder|

Der render-Operator ist in CMPivot bereits vorhanden. Unterstützung für mehrere Reihen und **with**-Anweisung wurden hinzugefügt. Weitere Informationen finden Sie im Abschnitt [Beispiele](#bkmk_cmpivot_examples1906) und im Artikel [join-Operator](https://docs.microsoft.com/azure/kusto/query/joinoperator) von Kusto.

#### <a name="limitations-for-joins"></a>Einschränkungen für Verknüpfungen

1. Die Spaltenverknüpfung erfolgt immer implizit über das **Device**-Feld.
1. Sie können maximal 5 Verknüpfungen pro Abfrage verwenden.
1. Sie können maximal 64 kombinierte Spalten verwenden.

#### <a name="scalar-operators"></a>Skalaroperatoren

|Operator| BESCHREIBUNG|Beispiel|
|-----|-----|-----|
| + | Add| `2 + 1, now() + 1d`|
| - |  Subtrahieren| `2 - 1, now() - 1d`|
| * | Multiplizieren| `2 * 2`|
| / | Dividieren | `2 / 1`|
| % | Modulo | `2 % 1`

#### <a name="aggregation-functions"></a>Aggregationsfunktionen

|Funktion| Beschreibung|
|-----|-----|
| percentile()| Gibt eine Schätzung für das angegebene Quantil des nächsten Rangs der durch Expr definierten Auffüllung zurück.|
| sumif() | Gibt eine Summe von Expr zurück, für die das Prädikat als „true“ ausgewertet wird.|

#### <a name="scalar-functions"></a>Skalarfunktionen

|Funktion| Beschreibung|
|-----|-----|
| case()| Wertet eine Liste von Prädikaten aus und gibt den ersten Ergebnisausdruck zurück, dessen Prädikat erfüllt ist. |
| iff() | Wertet das erste Argument aus und gibt entweder den Wert des zweiten oder dritten Arguments aus, abhängig davon, ob das Prädikat als „true“ (zweites) oder „false“ (drittes) ausgewertet wird.|
 | indexof() | Die Funktion meldet den nullbasierten (0) Index des ersten Vorkommens einer angegebenen Zeichenfolge in der Eingabezeichenfolge.|
| strcat() | Verkettet zwischen 1 und 64 Argumente. |
| strlen()| Gibt die Länge der Eingabezeichenfolge in Zeichen zurück.|
| substring() | Extrahiert eine Teilzeichenfolge aus einer Quellzeichenfolge beginnend bei einem Index bis zum Ende der Zeichenfolge. |
| tostring() | Konvertiert eine Eingabe in eine Zeichenfolgenoperation. |

#### <a name="examples"></a><a name="bkmk_cmpivot_examples1906"></a> Beispiele

- Anzeigen von Gerät, Hersteller, Modell und OSVersion:

   ``` Kusto
   ComputerSystem
   | project Device, Manufacturer, Model
   | join (OperatingSystem | project Device, OSVersion=Caption)
   ```

- Anzeigen des Diagramms der Startzeiten für ein Gerät:

   ``` Kusto
   SystemBootData
   | where Device == 'MyDevice'
   | project SystemStartTime, BootDuration, OSStart=EventLogStart, GPDuration, UpdateDuration
   | order by SystemStartTime desc
   | render barchart with (kind=stacked, title='Boot times for MyDevice', ytitle='Time (ms)')
   ```

   ![Gestapeltes Balkendiagramm der Startzeiten für ein Gerät in Millisekunden](./media/4054074-render-using-with-statement.png)

### <a name="added-cmpivot-permissions-to-the-security-administrator-role"></a><a name="bkmk_cmpivot_secadmin1906"></a> Zur Rolle „Sicherheitsadministrator“ hinzugefügte CMPivot-Berechtigungen
<!--4683130-->

Ab Version 1906 wurden der in den Configuration Manager integrierten Rolle **Sicherheitsadministrator** die folgenden Berechtigungen hinzugefügt:

 - **Lesen** des SMS-Skripts
 - **Ausführen von CMPivot** für eine Sammlung
 - **Lesen** des Inventarberichts

>[!NOTE]
> **Ausführen von Skripts** ist eine Obermenge der Berechtigung **Ausführen von CMPivot**.

### <a name="cmpivot-standalone"></a><a name="bkmk_standalone"></a> Eigenständige Verwendung von CMPivot

[!INCLUDE [CMPivot standalone](includes/cmpivot-standalone.md)] 

## <a name="cmpivot-changes-for-version-1902"></a><a name="bkmk_cmpivot1902"></a> Änderungen an CMPivot in Version 1902
<!--3610960-->
Ab Configuration Manager, Version 1902 können Sie CMPivot über den CAS in einer Hierarchie ausführen. Die Kommunikation mit dem Client wird nach wie vor vom primären Standort abgewickelt. Beim Ausführen von CMPivot über den Standort der zentralen Verwaltung kommuniziert der Client mit dem primären Standort über den Hochgeschwindigkeitskanal des Nachrichtenabonnements. Diese Kommunikation ist nicht von der standardmäßigen SQL-Replikation zwischen Standorten abhängig.

Zum Ausführen von CMPivot für den CAS benötigen Sie zusätzliche Berechtigungen, wenn SQL oder der Anbieter nicht denselben Computer verwenden oder wenn eine SQL Always On-Konfiguration vorliegt. Bei diesen Remotekonfigurationen liegt ein Double-Hop-Szenario für CMPivot vor.

Damit CMPivot in einem solchen Szenario für den CAS funktioniert, können Sie eine eingeschränkte Delegierung definieren. Informationen zu den Auswirkungen auf die Sicherheit durch diese Konfiguration finden Sie in dem Artikel [Kerberos constrained delegation (Eingeschränkte Kerberos-Delegierung)](https://docs.microsoft.com/windows-server/security/kerberos/kerberos-constrained-delegation-overview). Kerberos muss alle Hops zwischen den Computern durchlaufen.<!--5746133--> Wenn Sie über mehr als eine Remotekonfiguration (z. B. SQL oder SMS-Anbieter – mit dem CAS verbunden oder nicht) oder mehrere vertrauenswürdige Gesamtstrukturen verfügen, benötigen Sie möglicherweise verschiedene Berechtigungseinstellungen. Im Folgenden sehen Sie die Schritte, die Sie möglicherweise ausführen müssen:

### <a name="cas-has-a-remote-sql-server"></a>CAS mit einer Remoteinstanz von SQL Server

1. Gehen Sie zu den SQL Server-Instanzen der einzelnen primären Standorte.
   1. Fügen Sie die CAS-Remoteinstanz von SQL Server und den CAS-Standortserver zur Gruppe [Configmgr_DviewAccess](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess) hinzu.
   ![Configmgr_DviewAccess-Gruppe für die SQL Server-Instanz eines primären Standorts](media/cmpivot-dviewaccess-group.png)
1. Öffnen Sie Active Directory-Benutzer und -Computer.
   1. Klicken Sie erst mit der rechten Maustaste auf die einzelnen Server für die primären Standorte und anschließend mit der linken auf **Eigenschaften**.
      1. Wählen Sie auf der Registerkarte „Delegierung“ die Option **Computer nur bei Delegierungen angegebener Dienste vertrauen** aus. 
      1. Klicken Sie anschließend auf **Nur Kerberos verwenden**.
      1. Fügen Sie den Dienst der SQL Server-Instanz für den CAS zusammen mit einem Port und einer Instanz hinzu.
      1. Vergewissern Sie sich, dass diese Änderungen gemäß den Sicherheitsrichtlinien Ihres Unternehmens vorgenommen werden.
   1. Klicken Sie erst mit der rechten Maustaste auf den CAS-Standort und dann mit der linken auf **Eigenschaften**.
      1. Wählen Sie auf der Registerkarte „Delegierung“ die Option **Computer nur bei Delegierungen angegebener Dienste vertrauen** aus. 
      1. Klicken Sie anschließend auf **Nur Kerberos verwenden**.
      1. Fügen Sie den Dienst der SQL Server-Instanz für die einzelnen primären Standorte zusammen mit einem Port und einer Instanz hinzu.
      1. Vergewissern Sie sich, dass diese Änderungen gemäß den Sicherheitsrichtlinien Ihres Unternehmens vorgenommen werden.

   ![Beispiel für ein Double-Hops-Szenario mit einer Active Directory-Delegierung für CMPivot](media/cmpivot-ad-delegation.png)

### <a name="cas-has-a-remote-provider"></a>CAS mit einem Remoteanbieter

1. Gehen Sie zu den SQL Server-Instanzen der einzelnen primären Standorte.
   1. Fügen Sie das Konto für den CAS-Anbietercomputer und den CAS-Standortserver zur Gruppe [Configmgr_DviewAccess](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess) hinzu.
1. Öffnen Sie Active Directory-Benutzer und -Computer.
   1. Klicken Sie erst mit der rechten Maustaste auf den CAS-Anbietercomputer und anschließend mit der linken auf **Eigenschaften**.
      1. Wählen Sie auf der Registerkarte „Delegierung“ die Option **Computer nur bei Delegierungen angegebener Dienste vertrauen** aus. 
      1. Klicken Sie anschließend auf **Nur Kerberos verwenden**.
      1. Fügen Sie den Dienst der SQL Server-Instanz für die einzelnen primären Standorte zusammen mit einem Port und einer Instanz hinzu.
      1. Vergewissern Sie sich, dass diese Änderungen gemäß den Sicherheitsrichtlinien Ihres Unternehmens vorgenommen werden.
   1. Klicken Sie erst mit der rechten Maustaste auf den CAS-Standortserver und anschließend mit der linken auf **Eigenschaften**.
      1. Wählen Sie auf der Registerkarte „Delegierung“ die Option **Computer nur bei Delegierungen angegebener Dienste vertrauen** aus. 
      1. Klicken Sie anschließend auf **Nur Kerberos verwenden**.
      1. Fügen Sie den Dienst der SQL Server-Instanz für die einzelnen primären Standorte zusammen mit einem Port und einer Instanz hinzu.
      1. Vergewissern Sie sich, dass diese Änderungen gemäß den Sicherheitsrichtlinien Ihres Unternehmens vorgenommen werden.
1. Starten Sie den CAS-Remoteanbietercomputer neu.

### <a name="sql-always-on"></a>SQL Always On

1. Gehen Sie zu den SQL Server-Instanzen der einzelnen primären Standorte.
   1. Fügen Sie den CAS-Standortserver zur Gruppe [Configmgr_DviewAccess](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess) hinzu.
1. Öffnen Sie Active Directory-Benutzer und -Computer.
   1. Klicken Sie erst mit der rechten Maustaste auf die einzelnen Server für die primären Standorte und anschließend mit der linken auf **Eigenschaften**.
      1. Wählen Sie auf der Registerkarte „Delegierung“ die Option **Computer nur bei Delegierungen angegebener Dienste vertrauen** aus. 
      1. Klicken Sie anschließend auf **Nur Kerberos verwenden**.
      1. Fügen Sie die Dienstkonten der SQL Server-Instanz für den CAS zusammen mit einem Port und einer Instanz hinzu.
      1. Vergewissern Sie sich, dass diese Änderungen gemäß den Sicherheitsrichtlinien Ihres Unternehmens vorgenommen werden.
   1. Klicken Sie erst mit der rechten Maustaste auf den CAS-Standortserver und anschließend mit der linken auf **Eigenschaften**.
      1. Wählen Sie auf der Registerkarte „Delegierung“ die Option **Computer nur bei Delegierungen angegebener Dienste vertrauen** aus. 
      1. Klicken Sie anschließend auf **Nur Kerberos verwenden**.
      1. Fügen Sie den Dienst der SQL Server-Instanz für die einzelnen primären Standorte zusammen mit einem Port und einer Instanz hinzu.
      1. Vergewissern Sie sich, dass diese Änderungen gemäß den Sicherheitsrichtlinien Ihres Unternehmens vorgenommen werden.
1. Vergewissern Sie sich, dass der [Dienstprinzipalname (Service Principal Name, SPN)](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/listeners-client-connectivity-application-failover?view=sql-server-2017#SPNs) für den CAS-SQL-Listener und der jeweilige Name des primären SQL-Listeners öffentlich sind.
1. Starten Sie die primären SQL Server-Instanzen neu.
1. Starten Sie den CAS-Standortserver und die SQL-Serverinstanzen für den CAS neu.


## <a name="cmpivot-changes-for-version-1810"></a><a name="bkmk_cmpivot"></a> Änderungen an CMPivot in Version 1810
<!--1359068, 3607759-->

Ab Configuration Manager-Version 1810 umfasst CMPivot die folgenden Verbesserungen:

- [CMPivot-Hilfsprogramm und Leistung](#bkmk_cmpivot-perf)
- [Skalarfunktionen](#bkmk_cmpivot-functions)  
- [Rendern von Visualisierungen](#bkmk_cmpivot-charts)  
- [Hardwareinventur](#bkmk_cmpivot-hinv)  
- [Skalaroperatoren](#bkmk_cmpivot-operators)  
- [Abfragezusammenfassung](#bkmk_cmpivot-summary)  
- [Überprüfen von Statusmeldungen](#cmpivot-audit-status-messages)

### <a name="cmpivot-utility-and-performance"></a><a name="bkmk_cmpivot-perf"></a> CMPivot-Hilfsprogramm und Leistung

- CMPivot gibt bis zu 100.000 Zellen anstelle von 20.000 Zeilen zurück.
  - Wenn die Entität fünf Eigenschaften aufweist (d. h. fünf Spalten), werden bis zu 20.000 Zeilen angezeigt.
  - Für eine Entität mit zehn Eigenschaften werden bis zu 10.000 Zeilen angezeigt.
  - Die Daten, die insgesamt angezeigt werden, umfassen höchstens 100.000 Zellen.
- Wählen Sie auf der Registerkarte mit der Zusammenfassung der Abfrage die Anzahl der ausgefallenen oder Offline-Geräte aus, und wählen Sie dann die Option **Sammlung erstellen** aus. Mit dieser Option lassen sich einfach die Geräte mit einer Bereitstellung für die Wiederherstellung erreichen.
   - Diese Option wurde aus Version 2006 entfernt, da für CMPivot keine Sammlung mehr abgefragt werden muss.
- Sie können **Abfragefavoriten** speichern, indem Sie auf das Ordnersymbol klicken.
   ![Beispiel für das Speichern eines Abfragefavoriten in CMPivot](media/cmpivot-favorite.png)

- Clients, die auf Version 1810 aktualisiert wurden, geben eine Ausgabe von weniger als 80 KB über einen schnellen Kommunikationskanal an den Standort zurück.
  - Durch diese Änderung wird die Leistung vom Anzeigen des Skripts und Abfragen der Ausgabe verbessert.
  - Wenn die Ausgabe des Skripts oder der Abfrage 80 KB überschreitet, sendet der Client die Daten über eine Zustandsmeldung.
  - Wenn der Client nicht auf Version 1810 aktualisiert wurde, verwendet er weiterhin Zustandsmeldungen.

- Beim Starten von CMPivot wird möglicherweise der folgende Fehler angezeigt:  **Sie können CMPivot aufgrund einer inkompatiblen Skriptversion zurzeit nicht verwenden. Die Ursache dieses Problems kann sein, dass die Hierarchie gerade eine Site aktualisiert. Warten Sie, bis das Upgrade beendet ist, und versuchen Sie es dann erneut.**

  - Wenn diese Meldung angezeigt wird, könnte dies Folgendes bedeuten:
    - Der Sicherheitsbereich ist nicht ordnungsgemäß eingerichtet.
    - Es sind Probleme mit einem gerade durchgeführten Upgrade aufgetreten.
    - Das zugrunde liegende CMPivot-Skript ist nicht kompatibel.


### <a name="scalar-functions"></a><a name="bkmk_cmpivot-functions"></a> Skalarfunktionen
CMPivot unterstützt die folgenden Skalarfunktionen:
- **ago():** subtrahiert den angegebenen Zeitraum von der aktuellen UTC-Uhrzeit  
- **datetime_diff():** berechnet den Abstand zwischen zwei datetime-Werten  
- **now():** gibt die aktuelle UTC-Zeit zurück  
- **bin():** rundet die Werte auf eine ganze Zahl ab, die ein Vielfaches einer bestimmten Intervallgröße ist  

> [!Note]  
> Der Datentyp datetime stellt einen Zeitpunkt dar, der normalerweise als Datum und Uhrzeit angegeben wird. Zeitwerte werden in ganzen Sekunden gemessen. Ein datetime-Wert wird immer in UTC angegeben. Schreiben Sie datetime-Literale immer nach der ISO 8601-Norm, z.B. `yyyy-mm-dd HH:MM:ss`.  

#### <a name="examples"></a>Beispiele
- `datetime(2015-12-31 23:59:59.9)`: ein Datum-Uhrzeit-Literal   
- `now()`: die aktuelle Uhrzeit  
- `ago(1d)`: die aktuelle Uhrzeit minus einen Tag  


### <a name="rendering-visualizations"></a><a name="bkmk_cmpivot-charts"></a> Rendern von Visualisierungen

CMPivot umfasst nun grundlegende Unterstützung für den KQL-Operator [render](https://docs.microsoft.com/azure/kusto/query/renderoperator). Diese Unterstützung umfasst die folgenden Typen:  
- **barchart** (Balkendiagramm): Die erste Spalte ist die X-Achse. Diese kann Text, einen datetime-Wert oder Zahlen enthalten. Die zweite Spalte muss numerisch sein und wird als horizontale Leiste angezeigt.  
- **columnchart** (Säulendiagramm): ein Säulendiagramm, das vergleichbar mit einem Balkendiagramm ist, jedoch über vertikale statt horizontale Flächen verfügt.  
- **piechart** (Kreisdiagramm): Die erste Spalte ist eine Farbachse, die zweite Spalte enthält Zahlen.  
- **timechart** (Zeitdiagramm): ein Liniendiagramm. Die erste Spalte ist die X-Achse und muss einen datetime-Wert enthalten. Die zweite Spalte ist die Y-Achse.  

#### <a name="example-bar-chart"></a>Beispiel: Balkendiagramm
Die folgende Abfrage rendert die zuletzt verwendeten Anwendungen als Balkendiagramm:

``` Kusto
CCMRecentlyUsedApplications
| summarize dcount( Device ) by ProductName
| top 10 by dcount_
| render barchart
```

![Beispielvisualisierung: CMPivot-Balkendiagramm](media/1359068-cmpivot-barchart.png)

#### <a name="example-time-chart"></a>Beispiel: Zeitdiagramm
Verwenden Sie den Operator **bin()** zum zeitlichen Gruppieren von Ereignissen, um ein Zeitdiagramm zu rendern. Die folgende Abfrage zeigt, zu welchem Zeitpunkt innerhalb der letzten sieben Tage Geräte gestartet wurden:

``` Kusto
OperatingSystem
| where LastBootUpTime <= ago(7d)
| summarize count() by bin(LastBootUpTime,1d)
| render timechart
```

![Beispielvisualisierung: CMPivot-Zeitdiagramm](media/1359068-cmpivot-timechart.png)

#### <a name="example-pie-chart"></a>Beispiel: Kreisdiagramm
Die folgende Abfrage zeigt alle Betriebssystemversionen in einem Kreisdiagramm an:

``` Kusto
OperatingSystem
| summarize count() by Caption
| render piechart
```

![Beispielvisualisierung: CMPivot-Kreisdiagramm](media/1359068-cmpivot-piechart.png)


### <a name="hardware-inventory"></a><a name="bkmk_cmpivot-hinv"></a> Hardwareinventur
Verwenden Sie CMPivot zum Abfragen einer beliebigen Hardwareinventurklasse. Zu diesen Klassen zählen benutzerdefinierte Erweiterungen, die Sie an der Hardwareinventur vornehmen. CMPivot gibt unverzüglich zwischengespeicherte Ergebnisse des letzten Hardwareinventurscans zurück, die in der Standortdatenbank gespeichert wurden. Gleichzeitig aktualisiert es die Ergebnisse bei Bedarf anhand der Livedaten von Onlineclients.

Je nachdem, ob es sich um Livedaten oder zwischengespeicherte Daten handelt, unterscheidet sich die Farbsättigung der Daten in der Tabelle oder dem Diagramm mit den Ergebnissen. Dunkelblau steht z.B. für Echtzeit eines Onlineclients. Hellblau kennzeichnet zwischengespeicherte Daten.

#### <a name="example"></a>Beispiel

``` Kusto
LogicalDisk
| summarize sum( FreeSpace ) by Device
| order by sum_ desc
| render columnchart
```

![Beispielvisualisierung: CMPivot-Inventurabfrage mit einem Säulendiagramm](media/1359068-cmpivot-inventory.png)

#### <a name="limitations"></a>Einschränkungen
- Die folgenden Entitäten der Hardwareinventur werden nicht unterstützt:  
    - Arrayeigenschaften, z.B. IP-Adressen  
    - Real32/Real64 <!--example?-->  
    - Eigenschaften eingebetteter Objekte <!--example?-->  
- Inventurentitätsnamen müssen mit einem Zeichen beginnen.
- Sie können die integrierten Entitäten nicht überschreiben, indem Sie eine Entität mit dem gleichen Namen erstellen.  


### <a name="scalar-operators"></a><a name="bkmk_cmpivot-operators"></a> Skalaroperatoren
CMPivot enthält die folgenden Skalaroperatoren:  

> [!Note]  
> - Linke Seite: Zeichenfolge links des Operators  
> - Rechte Seite: Zeichenfolge rechts des Operators  


|Operator|Beschreibung|Beispiel (gibt TRUE zurück)|
|--------|-----------|---------------------|
|==|Gleich|`"aBc" == "aBc"`|
|!=|Ungleich|`"abc" != "ABC"`|
|like|Linke Seite enthält eine Übereinstimmung für rechte Seite|`"FabriKam" like "%Brik%"`|
|!like|Linke Seite enthält keine Übereinstimmung für rechte Seite|`"Fabrikam" !like "%xyz%"`|
|enthält|Rechte Seite kommt als Teilsequenz von linker Seite vor|`"FabriKam" contains "BRik"`|
|!contains|Rechte Seite kommt auf linker Seite nicht vor|`"Fabrikam" !contains "xyz"`|
|startswith|Rechte Seite ist eine öffnende Teilsequenz von linker Seite|`"Fabrikam" startswith "fab"`|
|!startswith|Rechte Seite ist keine öffnende Teilsequenz von linker Seite|`"Fabrikam" !startswith "kam"`|
|endswith|Rechte Seite ist eine schließende Teilsequenz von linker Seite|`"Fabrikam" endswith "Kam"`|
|!endswith|Rechte Seite ist keine schließende Teilsequenz von linker Seite|`"Fabrikam" !endswith "brik"`|


### <a name="query-summary"></a><a name="bkmk_cmpivot-summary"></a> Abfragezusammenfassung

Klicken Sie auf die Registerkarte **Query Summary** (Abfragezusammenfassung) unten im CMPivot-Fenster. Mit dem dort angezeigten Status können Sie Offlineclients bestimmen oder etwaige Probleme beheben. Wählen Sie einen Wert in der Spalte „Count“ aus. Dann wird eine Liste mit Geräten mit diesem Status geöffnet. 

Klicken Sie z.B. auf die Anzahl der Geräte mit dem Status „Failure“ (Fehler). Sehen Sie sich die entsprechenden Fehlermeldungen an, und exportieren Sie eine Liste dieser Geräte. Wenn ein Fehler auftritt, weil ein bestimmtes Cmdlet nicht erkannt wurde, erstellen Sie eine Sammlung über die exportierte Geräteliste, um ein Windows PowerShell-Update durchzuführen.  

### <a name="cmpivot-audit-status-messages"></a>Überwachungsstatusmeldungen für CMPivot

Ab Version 1810 wird eine Überwachungsstatusmeldung mit der **MessageID 40805** erstellt, wenn Sie CMPivot ausführen. Sie können die Statusmeldungen unter **Überwachung** > **Systemstatus** > **Statusmeldungsabfragen** abrufen. Sie können **Alle Überwachungsstatusmeldungen für einen bestimmten Benutzer** oder **All Audit status Messages for a Specific Site** (Alle Überwachungsstatusmeldungen für einen bestimmten Standort) ausführen oder eine eigene Statusmeldungsabfrage erstellen.

Für die Meldung wird das folgende Format verwendet:

MessageId 40805: User &lt;UserName> ran script &lt;Script-Guid> with hash &lt;Script-Hash> on collection &lt;Collection-ID>. (Der Benutzer &lt;Benutzername> hat das Skript &lt;Skript-GUID> mit dem Hash &lt;Skripthash> für die Sammlung &lt;Sammlungs-ID> ausgeführt.)

- 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 ist die Skript-GUID für CMPivot.
- Den Skripthash können Sie der Datei „scripts.log“ des Clients entnehmen.
- Sie finden den Hash auch im Skriptspeicher des Clients. Der Dateiname für den Client lautet &lt;Skript-GUID>_&lt;Skripthash>.
    - Beispieldateiname: C:\Windows\CCM\ScriptStore\7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14_abc1d23e45678901fabc123d456ce789fa1b2cd3e456789123fab4c56789d0123.ps
   

![Beispiel für eine Überwachungsstatusmeldung für CMPivot](media/cmpivot-audit-status-message.png)

## <a name="next-steps"></a>Nächste Schritte
 
[Problembehandlung für CMPivot](cmpivot-tsg.md)
