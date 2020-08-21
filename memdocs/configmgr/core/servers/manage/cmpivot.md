---
title: CMPivot für Echtzeitdaten
titleSuffix: Configuration Manager
description: Informationen zur Verwendung von CMPivot in Configuration Manager für die Abfrage von Clients in Echtzeit
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 32e2d6b9-148f-45e2-8083-98c656473f82
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 06e2a90e8c481fba834cbd1b6b1f5233572e4b17
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128329"
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

- Der [Microsoft Edge](../../../apps/deploy-use/deploy-edge.md)-Installer und CMPivot werden mit dem **Codesignierungszertifikat von Microsoft** signiert. Wenn dieses Zertifikat nicht im Speicher **Vertrauenswürdige Herausgeber** aufgeführt ist, müssen Sie es hinzufügen. Andernfalls werden der Microsoft Edge-Installer und CMPivot nicht ausgeführt, wenn die PowerShell-Ausführungsrichtlinie auf **AllSigned** festgelegt ist. <!--7585106-->

## <a name="permissions"></a>Berechtigungen

Die folgenden Berechtigungen sind für CMPivot erforderlich:

- **Leseberechtigung** für **SMS-Skripts**-Objekte
- Berechtigung zum **Ausführen von Skripts** für die **Sammlung**
   - Alternativ können Sie ab Version 1906 **Ausführen von CMPivot** für die **Sammlung** verwenden.
- **Leseberechtigung** für **Inventurberichte**
- Der Standardbereich

> [!NOTE]
> - **Ausführen von Skripts** ist eine Obermenge der Berechtigung **Ausführen von CMPivot**.
> - Ab Version 1906 wurden der in Configuration Manager integrierten Rolle **Sicherheitsadministrator** die [Berechtigungen für CMPivot hinzugefügt](cmpivot-changes.md#bkmk_cmpivot_secadmin1906).
 
## <a name="limitations"></a>Einschränkungen

- Verbinden Sie die Configuration Manager-Konsole in einer Hierarchie mit einem *primären Standort*, um CMPivot auszuführen. Die Aktion **CMPivot starten** wird nicht in der Konsole angezeigt, wenn diese mit einem Standort der zentralen Verwaltung (Central Administration Site, CAS) verbunden ist.
  - Ab Configuration Manager, Version 1902 können Sie CMPivot über einen CAS ausführen. In manchen Umgebungen werden zusätzliche Berechtigungen benötigt. Weitere Informationen finden Sie unter [CMPivot-Änderungen in Version 1902](cmpivot-changes.md#bkmk_cmpivot1902).

- CMPivot gibt nur Daten für Clients zurück, die mit dem aktuellen Standort verbunden sind.  

- Wenn eine Sammlung Geräte von anderen Standorten enthält, stammen CMPivot-Ergebnisse nur von Geräten im aktuellen Standort.  

- Entitätseigenschaften, Spalten für Ergebnisse oder Aktionen auf Geräten können nicht angepasst werden.  

- Auf einem Computer, auf dem die Configuration Manager-Konsole ausgeführt wird, kann nur jeweils eine CMPivot-Instanz ausgeführt werden.  

- In Version 1806 funktioniert die Abfrage für die Entität **Administrators** nur, wenn die Gruppe „Administrators“ heißt. Sie funktioniert nicht, wenn der Gruppenname lokalisiert wird. Beispiel: „Administrateurs“ auf Französisch.<!--SCCMDocs issue 759-->  


## <a name="start-cmpivot"></a>Starten von CMPivot

1. Stellen Sie in der Configuration Manager-Konsole eine Verbindung mit dem primären Standort her. Wechseln Sie zum Arbeitsbereich **Bestand und Konformität**, und wählen Sie den Knoten **Gerätesammlungen** aus. Wählen Sie eine Zielsammlung aus, und klicken Sie im Menüband auf **CMPivot starten**, um das Tool zu starten. Überprüfen Sie die folgenden Konfigurationen, wenn Ihnen diese Option nicht angezeigt wird:  
   - Vergewissern Sie sich bei einem Standortadministrator, dass Ihr Konto über die erforderlichen Berechtigungen verfügt. Weitere Informationen finden Sie unter [Voraussetzungen](#prerequisites).  
   - Verbinden Sie die Konsole mit einem *primären Standort*.  

2. Die Benutzeroberfläche bietet weitere Informationen zur Verwendung des Tools.  

     - Sie können im oberen Bereich manuell Abfragezeichenfolgen eingeben oder auf die Links in der Inlinedokumentation klicken.  

     - Klicken Sie auf eine der **Entitäten**, um sie der Abfragezeichenfolge hinzuzufügen.  

     - Die Links für **Tabellenoperatoren**, **Aggregationsfunktionen** und **Skalarfunktionen** öffnen die Sprachreferenzdokumentation im Webbrowser. CMPivot verwendet die [Kusto-Abfragesprache (KQL)](https://docs.microsoft.com/azure/kusto/query/).  

3. Lassen Sie das CMPivot-Fenster geöffnet, um die Ergebnisse der Clients anzuzeigen. Wenn Sie das CMPivot-Fenster schließen, wird die Sitzung beendet.
   - Wenn die Abfrage gesendet wurde, senden Clients weiterhin eine Statusmeldung an den Server.  



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
         - Ab Version 2006 wurde **Pivotieren nach** durch **Gerätepivot** ersetzt. Weitere Informationen finden Sie unter [CMPivot-Änderungen für Version 2006](cmpivot-changes.md#bkmk_2006).

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


## <a name="cmpivot-standalone"></a><a name="bkmk_standalone"></a> Eigenständige Verwendung von CMPivot

[!INCLUDE [CMPivot standalone](includes/cmpivot-standalone.md)]


 
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

- [Änderungen an CMPivot](cmpivot-changes.md)
- [Problembehandlung für CMPivot](cmpivot-tsg.md)
- [Erstellen und Ausführen von PowerShell-Skripts](../../../apps/deploy-use/create-deploy-scripts.md)


