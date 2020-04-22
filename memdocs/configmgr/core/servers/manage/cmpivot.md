---
title: CMPivot für Echtzeitdaten
titleSuffix: Configuration Manager
description: Informationen zur Verwendung von CMPivot in Configuration Manager für die Abfrage von Clients in Echtzeit
ms.date: 04/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 32e2d6b9-148f-45e2-8083-98c656473f82
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: dcd441c7f35748f42adc8824c68ec703291a13e0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702088"
---
# <a name="cmpivot-for-real-time-data-in-configuration-manager"></a>CMPivot für Echtzeitdaten in Configuration Manager

<!--1358456-->

*Gilt für: Configuration Manager (Current Branch)*

Configuration Manager hat immer einen großen zentralen Speicher für Gerätedaten bereitgestellt, die Kunden für Berichtszwecke verwenden. Der Standort erfasst diese Daten in der Regel einmal pro Woche. Ab Version 1806 ist CMPivot ein neues in der Konsole integriertes Hilfsprogramm, das nun Zugriff auf den Status von Geräten in Ihrer Umgebung in Echtzeit ermöglicht. Es führt sofort eine Abfrage aller derzeit verbundenen Geräte in der Zielsammlung durch und gibt die Ergebnisse zurück. Anschließend werden diese Daten im Tool gefiltert und gruppiert. Mit dem Bereitstellen von Echtzeitdaten von Onlineclients können Sie schneller Geschäftsfragen beantworten, Problembehandlungen durchführen sowie auf Sicherheitsvorfälle reagieren.

Beispielsweise ist eine der Anforderungen der [Abhilfe bei vermutlichen Kanalsicherheitsrisiken auf der Ausführungsseite](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974) die Aktualisierung des System-BIOS. Mit CMPivot können Sie schnell Informationen zum System-BIOS abfragen und Clients suchen, die nicht kompatibel sind.

 > [!IMPORTANT]  
 > - Möglicherweise blockiert Ihre Sicherheitssoftware Skripts, die über „c:\windows\ccm\scriptstore“ ausgeführt werden. Dadurch kann es zu Problemen bei der Ausführung von CMPivot-Abfragen kommen. Außerdem kann es sein, dass Ihre Sicherheitssoftware Überwachungsereignisse oder Warnungen generiert, wenn CMPivot unter PowerShell ausgeführt wird.
 > - Bestimmte Antischadsoftware kann unbeabsichtigt Ereignisse auslösen, die gegen die Configuration Manager-Features „Skripts ausführen“ und „CMPivot“ gerichtet sind. Es empfiehlt sich, „%windir%\CCM\ScriptStore“ auszuschließen, damit die Antischadsoftware die störungsfreie Ausführung dieser Features zulässt.


## <a name="prerequisites"></a>Voraussetzungen

Für die Verwendung von CMPivot sind die folgenden Komponenten erforderlich:

- Führen Sie ein Upgrade für die Zielgeräte auf die neueste Version des Konfigurations-Manager-Clients durch.  

- Für Zielclients wird PowerShell, Version 4 oder höher benötigt

- Zum Sammeln von Daten für die folgenden Entitäten benötigen die betreffenden Clients PowerShell Version 5.0:  
  - Administratoren
  - Verbindung
  - IPConfig
  - SMBConfig


- Berechtigungen für CMPivot:
  - **Leseberechtigung** für **SMS-Skripts**-Objekte
  - Berechtigung zum **Ausführen von Skripts** für die **Sammlung**
    - Alternativ können Sie ab Version 1906 **Ausführen von CMPivot** für die **Sammlung** verwenden.
  - **Leseberechtigung** für **Inventurberichte**
  - Der Standardbereich

>[!NOTE]
> **Ausführen von Skripts** ist eine Obermenge der Berechtigung **Ausführen von CMPivot**.
 
## <a name="limitations"></a>Einschränkungen

- Verbinden Sie die Configuration Manager-Konsole in einer Hierarchie mit einem *primären Standort*, um CMPivot auszuführen. Die Aktion **CMPivot starten** wird nicht in der Konsole angezeigt, wenn diese mit einem Standort der zentralen Verwaltung (Central Administration Site, CAS) verbunden ist.
  - Ab Configuration Manager, Version 1902 können Sie CMPivot über einen CAS ausführen. In manchen Umgebungen werden zusätzliche Berechtigungen benötigt. Weitere Informationen finden Sie unter [CMPivot ab Version 1902](#bkmk_cmpivot1902).

- CMPivot gibt nur Daten für Clients zurück, die mit dem aktuellen Standort verbunden sind.  

- Wenn eine Sammlung Geräte von anderen Standorten enthält, stammen CMPivot-Ergebnisse nur von Geräten im aktuellen Standort.  

- Entitätseigenschaften, Spalten für Ergebnisse oder Aktionen auf Geräten können nicht angepasst werden.  

- Auf einem Computer, auf dem die Configuration Manager-Konsole ausgeführt wird, kann nur jeweils eine CMPivot-Instanz ausgeführt werden.  

- In Version 1806 funktioniert die Abfrage für die Entität **Administrators** nur, wenn die Gruppe „Administrators“ heißt. Sie funktioniert nicht, wenn der Gruppenname lokalisiert wird. Beispiel: „Administrateurs“ auf Französisch.<!--SCCMDocs issue 759-->  


## <a name="start-cmpivot"></a>Starten von CMPivot

1. Stellen Sie in der Configuration Manager-Konsole eine Verbindung mit dem primären Standort her. Wechseln Sie zum Arbeitsbereich **Bestand und Konformität**, und wählen Sie den Knoten **Gerätesammlungen** aus. Wählen Sie eine Zielsammlung aus, und klicken Sie im Menüband auf **CMPivot starten**, um das Tool zu starten.  

    > [!Tip]  
    > Überprüfen Sie die folgenden Konfigurationen, wenn Ihnen diese Option nicht angezeigt wird:  
    > 
    > - Vergewissern Sie sich bei einem Standortadministrator, dass Ihr Konto über die erforderlichen Berechtigungen verfügt. Weitere Informationen finden Sie unter [Voraussetzungen](#prerequisites).  
    > 
    > - Verbinden Sie die Konsole mit einem *primären Standort*.  

2. Die Benutzeroberfläche bietet weitere Informationen zur Verwendung des Tools.  

     - Sie können im oberen Bereich manuell Abfragezeichenfolgen eingeben oder auf die Links in der Inlinedokumentation klicken.  

     - Klicken Sie auf eine der **Entitäten**, um sie der Abfragezeichenfolge hinzuzufügen.  

     - Die Links für **Tabellenoperatoren**, **Aggregationsfunktionen** und **Skalarfunktionen** öffnen die Sprachreferenzdokumentation im Webbrowser. CMPivot verwendet die [Kusto-Abfragesprache (KQL)](https://docs.microsoft.com/azure/kusto/query/).  

3. Lassen Sie das CMPivot-Fenster geöffnet, um die Ergebnisse der Clients anzuzeigen. Wenn Sie das CMPivot-Fenster schließen, wird die Sitzung beendet.  

    > [!Note]  
    > Wenn die Abfrage gesendet wurde, senden Clients weiterhin eine Statusmeldung an den Server.  



## <a name="how-to-use-cmpivot"></a>Verwenden von CMPivot

![Beispiel für ein CMPivot-Fenster](media/1358456-cmpivot-sample.png)

Das CMPivot-Fenster enthält die folgenden Elemente:  

1. Die Sammlung, die CMPivot aktuell anvisiert, befindet sich im oberen Bereich des Fensters in der Titelliste, und die Statusleiste befindet sich im unteren Bereich. Beispiel: „PM_Team_Machines“ im obigen Screenshot.  

2. In dem Bereich auf der linken Seite werden die **Entitäten** aufgeführt, die auf Clients verfügbar sind. Einige Entitäten sind auf WMI angewiesen, während andere PowerShell verwenden, um Daten von Clients abzurufen.   

    - Klicken Sie mit der rechten Maustaste auf eine Entität, um die folgenden Aktionen auszuführen:  

       - **Einfügen:** Fügt die Entität an der aktuellen Cursorposition zur Abfrage hinzu. Die Abfrage wird nicht automatisch ausgeführt. Dies ist die Standardaktion, wenn Sie auf eine Entität doppelklicken. Verwenden Sie diese Aktion beim Erstellen einer Abfrage.  

       - **Alle abfragen:** Führt eine Abfrage für diese Entität einschließlich sämtlicher Eigenschaften aus. Verwenden Sie diese Aktion, um schnell Abfragen für eine einzelne Entität auszuführen.  

       - **Nach Gerät abfragen:** Führt eine Abfrage für diese Entität aus und gruppiert die Ergebnisse. Beispiel: `Disk | summarize dcount( Device ) by Name`  

    - Erweitern Sie eine Entität, um die spezifischen Eigenschaften anzuzeigen, die für die einzelnen Entitäten verfügbar sind. Doppelklicken Sie auf eine Eigenschaft, um diese an der aktuellen Cursorposition zur Abfrage hinzuzufügen.  

3. Auf der Registerkarte **Home** werden allgemeine Informationen zu CMPivot angezeigt, einschließlich Links zu Beispielabfragen und begleitender Dokumentation.  

4. Auf der Registerkarte **Abfrage** werden der Abfragebereich, der Ergebnisbereich und die Statusleiste angezeigt. Die Registerkarte „Abfrage“ wurde im obigen Beispiel mit dem Screenshot ausgewählt.  

5. Im Abfragebereich können Sie eine Abfrage erstellen oder eingeben, die auf Clients in der Sammlung ausgeführt werden soll.  

    - CMPivot verwendet einen Teil der [Kusto-Abfragesprache (KQL)](https://docs.microsoft.com/azure/kusto/query/).  

    - Im Abfragebereich können Sie Inhalte ausschneiden, kopieren oder einfügen.  
    <!-- markdownlint-disable MD038 -->
    - In diesem Bereich wird standardmäßig IntelliSense verwendet. Wenn Sie beispielsweise mit der Eingabe von `D` beginnen, schlägt IntelliSense sämtliche Entitäten vor, die mit diesem Buchstaben beginnen. Wählen Sie eine Option aus, und drücken Sie die TAB-Taste, um diese einzufügen. Geben Sie ein Pipezeichen und ein Leerzeichen `| ` ein. IntelliSense schlägt Ihnen anschließend sämtliche Tabellenoperatoren vor. Fügen Sie `summarize` ein, und geben Sie ein Leerzeichen ein. IntelliSense schlägt Ihnen anschließend sämtliche Aggregationsfunktionen vor. Klicken Sie auf die Registerkarte **Home** in CMPivot, um weitere Informationen zu diesen Operatoren und Funktionen zu erhalten.  

    - Im Abfragebereich werden darüber hinaus folgende Optionen bereitgestellt:  

        - Ausführen der Abfrage  

        - Vorwärts- und Rückwärtsbewegung in der Verlaufsliste der Abfragen  

        - Erstellen einer Sammlung direkter Mitgliedschaften  

        - Exportieren der Ergebnisse der Abfrage in CSV oder die Zwischenablage  

6. Im Ergebnisbereich werden die Daten angezeigt, die von aktiven Clients für die Abfrage zurückgegeben wurden.  

   - Welche Spalten verfügbar sind, hängt von der Entität und der Abfrage ab.  

   - Klicken Sie auf einen Spaltennamen, um die Ergebnisse nach dieser Eigenschaft zu sortieren.  

   - Klicken Sie mit der rechten Maustaste auf einen Spaltennamen, um die Ergebnisse nach den gleichen Informationen in dieser Spalte zu gruppieren oder um die Ergebnisse zu sortieren.  

   - Klicken Sie mit der rechten Maustaste auf einen Gerätenamen, um die folgenden zusätzlichen Aktionen auf dem Gerät auszuführen:  

      - **Pivotieren nach:** Führt eine Abfrage für eine andere Entität auf diesem Gerät aus.  

      - **Skript ausführen:** Startet den Assistenten zum Ausführen von Skripts für die Ausführung eines vorhandenen PowerShell-Skripts auf diesem Gerät. Weitere Informationen finden Sie unter [Ausführen eines Skripts](../../../apps/deploy-use/create-deploy-scripts.md#run-a-script).  

      - **Remotesteuerung:** Startet auf diesem Gerät eine Remoteüberwachungssitzung in Configuration Manager. Weitere Informationen finden Sie unter [Remoteverwaltung eines Windows-Clientcomputers](../../clients/manage/remote-control/remotely-administer-a-windows-client-computer.md).  

      - **Ressourcen-Explorer:** Startet den Ressourcen-Explorer von Configuration Manager auf diesem Gerät. Weitere Informationen finden Sie unter [Anzeigen der Hardwareinventur](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) oder [Anzeigen der Softwareinventur](../../clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

   - Klicken Sie mit der rechten Maustaste auf eine Zelle ohne Geräteunterstützung, um die folgenden zusätzlichen Aktionen auszuführen:  

     - **Kopieren:** Kopiert den Text der Zelle in die Zwischenablage.  

     - **Geräte anzeigen mit:** Führt eine Abfrage für Geräte mit diesem Wert für diese Eigenschaft aus. Sie können diese Option beispielsweise aus den Ergebnissen der Abfrage `OS` in einer Zelle in der Zeile „Version“ auswählen: `OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ > 0)`  

     - **Geräte anzeigen ohne:** Führt eine Abfrage für Geräte ohne diesen Wert für diese Eigenschaft aus. Sie können diese Option beispielsweise aus den Ergebnissen der Abfrage `OS` in einer Zelle in der Zeile „Version“ auswählen: `OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ == 0) | project Device`  

     - **Mit Bing suchen:** Startet den Standardwebbrowser mit https://www.bing.com mit diesem Wert als Abfragezeichenfolge.  

   - Klicken Sie auf einen als Hyperlink formatierten Text, um die Ansicht zu diesen bestimmten Informationen zu pivotieren.  

   - Im Ergebnisbereich werden maximal 20.000 Zeilen angezeigt. Passen Sie die Abfrage entweder so an, dass die Daten weiter gefiltert werden, oder starten Sie CMPivot in einer kleineren Sammlung neu.  

7. In der Statusleiste werden die folgenden Informationen angezeigt (von links nach rechts):  

   - Der Status der aktuellen Abfrage für die Zielsammlung. Dieser Status umfasst:  
     - Die Anzahl der aktiven Clients, die die Abfrage (3) abgeschlossen haben  
     - Die Gesamtanzahl der Clients (5)  
     - Die Gesamtanzahl der Offlineclients (2)  
     - Alle Clients, die Fehler (0) zurückgegeben haben  

       Beispiel: `Query completed on 3 of 5 clients (2 clients offline and 0 failure)`  

   - Die ID des Clientvorgangs. Beispiel: `id(16780221)`  

   - Die aktuelle Sammlung. Beispiel: `PM_Team_Machines`  

   - Die Gesamtanzahl der Zeilen im Ergebnisbereich. Beispiel: `1 objects`  



## <a name="example-scenarios"></a>Beispielszenarien

Die folgenden Abschnitte enthalten Beispiele für die Verwendung von CMPivot in Ihrer Umgebung:


### <a name="example-1-stop-a-running-service"></a>Beispiel 1: Beenden eines ausgeführten Diensts

Ihr Sicherheitsadministrator fordert Sie dazu auf, den Computersuchdienst so schnell wie möglich auf sämtlichen Geräten in der Buchhaltung zu beenden und zu deaktivieren. Starten Sie CMPivot in einer Sammlung für alle Geräte in der Buchhaltung, und wählen Sie bei der Entität **Dienst** die Option **Alle abfragen** aus. 

`Service`

Wenn die Ergebnisse angezeigt werden, klicken Sie mit der rechten Maustaste auf die Spalte **Name**, und wählen Sie **Gruppieren nach** aus. 

`Service | summarize dcount( Device ) by Name`

Klicken Sie in der Zeile für den Dienst **Browser** in der Spalte **dcount_** auf die durch einen Hyperlink verbundene Zahl. 

`Service | where (Name == 'Browser') | summarize count() by Device`

Wählen Sie per Mehrfachauswahl sämtliche Geräte aus, klicken Sie mit der rechten Maustaste auf die Auswahl, und wählen Sie **Skript ausführen** aus. Durch diese Aktion wird der Assistent zur Ausführung von Skripts gestartet, über den Sie ein vorhandenes Skript zum Beenden und Deaktivieren eines Diensts ausführen. Mit CMPivot können Sie auf allen aktiven Computern schnell auf den Sicherheitsvorfall reagieren und die Ergebnisse im Assistenten zur Ausführung von Skripts anzeigen. Fahren Sie anschließend fort, indem Sie eine Konfigurationsbaseline erstellen, um weitere Computer der Sammlung zu warten, da diese zukünftig aktiviert werden. 

![CMPivot-Beispiel für den Suchdienst und die Aktion „Skript ausführen“](media/cmpivot-example1.png)


### <a name="example-2-proactively-resolve-application-failures"></a>Beispiel 2: Proaktives Beheben von Anwendungsfehlern  

Für einen proaktiven Umgang mit der betrieblichen Wartung müssen Sie CMPivot einmal pro Woche für eine Sammlung von Servern ausführen, die von Ihnen verwaltet werden, und auf der Entität **AppCrash** die Option **Alle abfragen** auswählen. Klicken Sie mit der rechten Maustaste auf die Spalte **FileName**, und wählen Sie **Aufsteigend sortieren** aus. Ein Gerät gibt täglich sieben Ergebnisse für „sqlsqm.exe“ mit dem ungefähren Zeitstempel „03:00 Uhr“ zurück. Wählen Sie den Dateinamen in einer der Zeilen aus, klicken Sie mit der rechten Maustaste darauf, und wählen Sie **Mit Bing suchen** aus. Beim Navigieren durch die Suchergebnisse im Webbrowser finden Sie einen Microsoft-Supportartikel zu diesem Problem, der weitere Informationen und eine Lösung enthält. 


### <a name="example-3-bios-version"></a>Beispiel 3: BIOS-Version

Wenn Sie [Abhilfe bei vermutlichen Kanalsicherheitsrisiken auf der Ausführungsseite](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974) schaffen möchten, besteht eine der Anforderungen in der Aktualisierung des System-BIOS. Beginnen Sie mit einer Abfrage für die **BIOS**-Entität. Anschließend führen Sie für die Eigenschaft **Version** die Option **Gruppieren nach** aus. Klicken Sie anschließend mit der rechten Maustaste auf einen bestimmten Wert, z.B. „LENOVO – 1140“, und wählen Sie **Geräte anzeigen mit** aus.  

`Bios | summarize countif( (Version == 'LENOVO - 1140') ) by Device | where (countif_ > 0)`


### <a name="example-4-free-disk-space"></a>Beispiel 4: Freier Speicherplatz

Sie müssen vorübergehend eine große Datei auf einem Netzwerkdateiserver speichern, sind aber nicht sicher, welcher Dateiserver genügend Kapazitäten hat. Starten Sie CMPivot für eine Sammlung von Dateiservern, und fragen Sie die Entität **Datenträger** ab. Ändern Sie die Abfrage für CMPivot so, dass schnell eine Liste der aktiven Server mit Daten zum Echtzeitspeicher zurückgegeben wird:  

`Disk | where (Description == 'Local Fixed Disk') | where isnotnull( FreeSpace ) | order by FreeSpace asc`


## <a name="cmpivot-starting-in-version-1810"></a><a name="bkmk_cmpivot"></a> CMPivot ab Version 1810
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

## <a name="cmpivot-starting-in-version-1902"></a><a name="bkmk_cmpivot1902"></a> CMPivot ab Version 1902
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

## <a name="cmpivot-starting-in-version-1906"></a><a name="bkmk_cmpivot1906"></a> CMPivot ab Version 1906

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

|Operator| Beschreibung|Beispiel|
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
<!--3555890, 4619340, 4683130 -->

Ab Version 1906 können Sie CMPivot als eigenständige App verwenden. Die eigenständige CMPivot-Version steht nur in englischer Sprache zur Verfügung. Führen Sie CMPivot außerhalb der Configuration Manager-Konsole aus, um den Echtzeitstatus von Geräten in Ihrer Umgebung anzuzeigen. Diese Änderung ermöglicht Ihnen die Verwendung von CMPivot auf einem Gerät, ohne die Konsole vorher zu installieren.

> [!Tip]  
> Dieses Feature wurde erstmals in Version 1906 als [Vorabfeature](pre-release-features.md) eingeführt. Ab Version 2002 ist es kein Vorabfeature mehr.  

Sie können die Leistungsfähigkeit von CMPivot mit anderen Personas wie Helpdesk oder Sicherheitsadministratoren teilen, die die Konsole nicht auf ihrem Computer installiert haben. Diese anderen Personas können CMPivot verwenden, um Configuration Manager neben den anderen Tools, die sie traditionell verwenden, abzufragen. Durch die gemeinsame Nutzung dieser umfangreichen Verwaltungsdaten können Sie proaktiv an der Lösung von rollenübergreifenden Geschäftsproblemen arbeiten.

#### <a name="install-cmpivot-standalone"></a>Installieren der eigenständigen CMPivot-Version

1. Richten Sie die erforderlichen Berechtigungen für die Ausführung von CMPivot ein. Weitere Informationen finden Sie unter [Voraussetzungen](#prerequisites). Sie können auch die Rolle [Sicherheitsadministrator](#bkmk_cmpivot_secadmin1906) verwenden, wenn die Berechtigungen für den Benutzer angemessen sind.
2. Das Installationsprogramm für die CMPivot-App befindet sich unter folgendem Pfad: `<site install path>\tools\CMPivot\CMPivot.msi`. Sie können es von diesem Pfad aus ausführen oder an einen anderen Speicherort kopieren.
3. Beim Ausführen der eigenständigen CMPivot-App werden Sie aufgefordert, eine Verbindung mit einem Standort herzustellen. Geben Sie den vollqualifizierten Domänennamen oder den Computernamen des Servers des Standorts der zentralen Verwaltung oder des primären Standorts an.
   - Wenn Sie die eigenständige CMPivot-Version öffnen, werden Sie jedes Mal aufgefordert, eine Verbindung mit einem Standortserver herzustellen.
4. Durchsuchen Sie die Sammlung, für die Sie CMPivot ausführen möchten, und führen Sie Ihre Abfrage aus.

   ![Navigieren zur Sammlung, für die die Abfrage ausgeführt werden soll](./media/3555890-cmpivot-standalone-browse-collection.png)

> [!NOTE]
> Kontextmenü-Aktionen wie **Run Scripts** (Skripts ausführen) und **Ressourcen-Explorer** sowie die Websuche sind in der eigenständigen CMPivot-Version nicht verfügbar. Die primäre Verwendung der eigenständigen CMPivot-Version besteht darin, unabhängig von der Configuration Manager-Infrastruktur Abfragen durchzuführen. Die eigenständige CMpivot-Version bietet zur Unterstützung von Sicherheitsadministratoren die Möglichkeit, eine Verbindung mit Microsoft Defender Security Center herzustellen. <!--5605358-->

## <a name="cmpivot-starting-in-version-1910"></a><a name="bkmk_cmpivot1910"></a> CMPivot ab Version 1910
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

### <a name="wineventlognametimespan"></a><a name="bkmk_WinEvent"></a> WinEvent(\<Protokollname>,[\<timespan>])

Mit dieser Entität werden Ereignisse aus Ereignisprotokollen und Protokolldateien der Ereignisablaufverfolgung abgerufen. Die Entität ruft Daten aus Ereignisprotokollen ab, die von der Windows-Ereignisprotokolltechnologie generiert werden. Die Entität ruft auch Ereignisse in Protokolldateien ab, die von der Ereignisablaufverfolgung für Windows (Event Tracing for Windows, ETW) generiert werden. WinEvent berücksichtigt standardmäßig Ereignisse, die innerhalb der letzten 24 Stunden aufgetreten sind. Diese Standardeinstellung kann jedoch durch Einschließen eines timespan-Werts überschrieben werden.

``` Kusto
WinEvent('Microsoft-Windows-HelloForBusiness/Operational', 1d)
| where LevelDisplayName =='Error'
| summarize count() by Device
```

### <a name="filecontentfilename"></a><a name="bkmk_File"></a> FileContent(\<Dateiname>)

FileContent wird verwendet, um den Inhalt einer Textdatei abzurufen.

``` Kusto
FileContent('c:\\windows\\SMSCFG.ini')
| where Content startswith  'SMS Unique Identifier='
| project Device, SMSId= substring(Content,22)
```

### <a name="processmoduleprocessname"></a><a name="bkmk_ProcessModule"></a> ProcessModule(\<Prozessname>)  

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
Wenn Sie CMPivot außerhalb der Configuration Manager-Konsole verwenden, können Sie nur das lokale Gerät abfragen, ohne dass hierzu die Configuration Manager-Infrastruktur erforderlich ist. Sie können ab sofort die CMPivot-Azure Log Analytics-Abfragen nutzen, um schnell WMI-Informationen auf dem lokalen Gerät anzuzeigen. Dies ermöglicht auch die Überprüfung und Optimierung von CMPivot-Abfragen, bevor diese in einer größeren Umgebung ausgeführt werden. Die eigenständige CMPivot-Version steht nur in englischer Sprache zur Verfügung. Weitere Informationen zum Installieren der eigenständigen CMPivot-Version finden Sie unter [Installieren der eigenständigen CMPivot-Version](#install-cmpivot-standalone).

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
    > Damit dieser Link funktioniert, müssen Sie die [eigenständige CMPivot-Version installieren](#install-cmpivot-standalone).

- Wenn das Gerät in Microsoft Defender Advanced Threat Protection (ATP) registriert ist, klicken Sie in den Abfrageergebnissen mit der rechten Maustaste auf das Gerät, um das Onlineportal für **Microsoft Defender Security Center** zu starten.

### <a name="known-issues-for-cmpivot-in-version-1910"></a>Bekannte Probleme für CMPivot in Version 1910

- Das Banner „Maximale Ergebnisse“ wird möglicherweise nicht angezeigt, wenn der Grenzwert erreicht ist. <!--5431427-->
  - Jeder Client ist auf 128 KB pro Abfrage beschränkt.
  - Die Ergebnisse werden möglicherweise abgeschnitten, wenn die Ergebnisse der Abfrage 128 KB überschreiten.
  
## <a name="cmpivot-starting-in-version-2002"></a><a name="bkmk_2002"></a> CMPivot ab Version 2002
<!--5870934-->
Das Navigieren zu CMPivot-Entitäten wurde vereinfacht. Ab Configuration Manager, Version 2002 können Sie CMPivot-Entitäten durchsuchen. Außerdem wurden neue Symbole hinzugefügt, um die Entitäten und Entitätsobjekttypen leicht unterscheiden zu können.

![Suchen von CMPivot-Entitäten](./media/5870934-search-cmpivot-entities.png)

 
## <a name="inside-cmpivot"></a>Innerhalb von CMPivot

CMPivot sendet über den „schnellen Kanal“ von Configuration Manager Abfragen an Clients. Dieser Kommunikationskanal zwischen Server und Client wird auch von anderen Features verwendet, wie z.B. Aktionen zur Clientbenachrichtigung, Clientstatus und Endpoint Protection. Clients geben Ergebnisse über das Zustandsmeldungssystem zurück, das ebenso schnell ist. Zustandsmeldungen werden vorübergehend in der Datenbank gespeichert. Weitere Informationen zu den Ports, die für die Clientbenachrichtigung verwendet werden, finden Sie in dem Artikel [Ports](../../plan-design/hierarchy/ports.md#BKMK_PortsClient-MP).

Die Abfragen und Ergebnisse bestehen alle nur aus Text. Die Entitäten **InstallSoftware** und **Prozess** geben einige der größten Resultsets zurück. Während der Leistungstests betrug die Größe der umfangreichsten Datei in den Zustandsmeldungen, die von einem Client für diese Abfragen zurückgegeben wurden, weniger als **1 KB**. Bei einer Skalierung auf eine große Umgebung mit 50.000 aktiven Clients würde diese einmalige Abfrage netzwerkübergreifend weniger als 50 MB an Daten generieren. Sämtliche unterstrichenen Elemente unter „Home“ geben weniger als 1 KB an Informationen pro Client zurück.

![Beispiel für unterstrichene CMPivot-Entitäten](media/cmpivot-underlined-entities.png)

Ab Configuration Manager, Version 1810 kann CMPivot Hardwareinventurdaten (einschließlich erweiterter Hardwareinventurdaten) abfragen. Diese neuen Entitäten (unter „Home“ nicht unterstrichen) geben möglicherweise viel größere Datasets zurück. Dies hängt davon ab, wie viele Daten für eine bestimmte Hardwareinventureigenschaft definiert wurden. Beispielsweise kann eine InstalledExecutable-Entität in Abhängigkeit davon, welche Daten genau abgefragt werden, mehrere Megabyte an Daten pro Client zurückgeben. Berücksichtigen Sie die Leistung und Skalierbarkeit auf Ihrem System, wenn Sie mithilfe von CMPivot größere Hardwareinventurdatasets aus größeren Sammlungen zurückgeben.

Nach einer Stunde wird das Zeitlimit für eine Abfrage überschritten. Beispiel: Eine Sammlung umfasst 500 Geräte, und 450 der Clients sind aktuell online. Diese aktiven Geräte empfangen die Abfrage und geben die Ergebnisse unmittelbar danach zurück. Wenn Sie das CMPivot-Fenster geöffnet lassen, während die anderen 50 Clients online kommen, empfangen diese ebenfalls die Abfrage und geben Ergebnisse zurück. 

## <a name="log-files"></a>Protokolldateien

 CMPivot-Interaktionen werden in den folgenden Protokolldateien protokolliert:

**Serverseitig**:
- SmsProv.log
- BgbServer.log
- StateSys.log

**Clientseitig**:
- CCMNotificationAgent.log
- Scripts.log
- StateMessage.log

Weitere Informationen finden sie unter [Protokolldateien](../../plan-design/hierarchy/log-files.md) und [Problembehandlung für CMPivot](cmpivot-tsg.md).

## <a name="next-steps"></a>Nächste Schritte
 
[Problembehandlung für CMPivot](cmpivot-tsg.md)

[Erstellen und Ausführen von PowerShell-Skripts](../../../apps/deploy-use/create-deploy-scripts.md)


