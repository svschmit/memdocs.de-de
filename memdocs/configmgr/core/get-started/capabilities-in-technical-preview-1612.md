---
title: Funktionen in Technical Preview 1612
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über Features, die in der Technical Preview-Version 1612 für Configuration Manager zur Verfügung stehen.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bceab2e8-2f05-4a17-9ac8-a7a558670fb7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 0c2464bfba05d640868af7d5c8be7c32c0999946
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705408"
---
# <a name="capabilities-in-technical-preview-1612-for-configuration-manager"></a>Funktionen in der Technical Preview 1612 für Configuration Manager

*Gilt für: Configuration Manager (Technical Preview-Branch)*



In diesem Artikel werden die Features vorgestellt, die in der Technical Preview-Version 1612 für Configuration Manager verfügbar sind. Sie können diese Version installieren, um neue Funktionen für Ihren Configuration Manager Technical Preview-Standort zu aktualisieren oder hinzuzufügen. Bevor Sie diese Version der Technical Preview installieren, lesen Sie das einführende Thema [Technical Preview für Configuration Manager](../../core/get-started/technical-preview.md), um sich mit den allgemeinen Anforderungen und Einschränkungen bei der Verwendung einer Technical Preview vertraut zu machen und um zu erfahren, wie Sie Updates für Versionen durchführen und Feedback zu den Features in einer Technical Preview geben können.    


**Im Folgenden werden neue Features aufgelistet, die Sie mit dieser Version ausprobieren können.**  

## <a name="the-data-warehouse-service-point"></a>Der Data Warehouse-Dienstpunkt
Ab Version 1612 von Technical Preview ermöglicht es der Data Warehouse-Dienstpunkt, langfristige Verlaufsdaten zur Bereitstellung für Configuration Manager zu speichern und hierfür Berichte zu erstellen. Dies wird durch die automatisierte Synchronisierung der Configuration Manager-Standortdatenbank in eine Data Warehouse-Datenbank erreicht. Auf diese Information kann dann vom Reporting Services-Punkt aus zugegriffen werden.

Wenn Sie die neue Standardsystemrolle installieren, erstellt Configuration Manager standardmäßig für Sie die Data Warehouse-Datenbank auf einer von Ihnen angegebenen SQL Server-Instanz. Das Data Warehouse unterstützt ein Datenvolumen von bis zu 2 TB, inklusive der Zeitstempel für Änderungsnachverfolgung.  Standardmäßig gehören zu den Daten, die aus der Standortdatenbank synchronisiert werden, die Datengruppen für globale Daten, Standortdaten, Global_Proxy, Clouddaten und Datenbankansichten. Was synchronisiert wird, kann auch geändert werden, um zusätzliche Tabellen bei den Standardreplikationsätzen zu integrieren oder bestimmte Tabellen daraus auszuschließen.
Zu den synchronisierten Default-Daten gehören Informationen zu:
- Infrastrukturintegrität
- Sicherheit
- Konformität
- Malware   
- Softwarebereitstellungen
- Inventurdetails (Der Inventurverlauf wird allerdings nicht synchronisiert)

Zusätzlich zur Installation und Konfiguration der Data Warehouse-Datenbank werden mehrere neue Berichte installiert. So können Sie ganz einfach nach diesen Daten suchen und über sie berichten.

### <a name="data-warehouse-dataflow"></a>Data Warehouse-Datenfluss   
![Datawarehouse_flow](./media/datawarehouse.png)

| Schritt         | Details  |
|:------:|-----------|  
| **1** | Der Standortserver überträgt und speichert Daten in der Standortdatenbank.  |  
| **2** | Basierend auf Zeitplan und Konfiguration, ruft der Data Warehouse-Dienstpunkt Daten aus der Standortdatenbank ab.  |  
| **3** | Der Data Warehouse-Dienstpunkt überträgt und speichert eine Kopie der synchronisierten Daten in der Data Warehouse-Datenbank. |  
| **A** | Mit integrierten Berichten werden Daten angefragt, die mittels SQL Server Reporting Services an den Reporting Services-Punkt übertragen werden. |  
| **B** | Die meisten Berichte gelten für aktuelle Informationen. Diese Anfragen werden in der Standortdatenbank ausgeführt. |  
| **C** | Wenn ein Bericht Verlaufsdaten mit einem der Berichte mit einer *Kategorie* des **Data Warehouse** anfragt, wird diese Anfrage in der Data Warehouse-Datenbank ausgeführt.   |  

### <a name="prerequisites-for-the-data-warehouse-service-point-and-database"></a>Voraussetzungen für den Data Warehouse-Dienstpunkt und die Datenbank
- Die Installation einer Standortsystemrolle des Reporting Services-Punkts in Ihrer Hierarchie ist notwendig.
- Der Computer, auf dem die Standortsystemrolle installiert ist, erfordert .NET Framework 4.5.2 oder höher.
- Das Computerkonto des Computers, auf dem die Standortsystemrolle installiert wird, muss über die lokalen Administratorrechte auf dem Computer verfügen, auf dem die Data Warehouse-Datenbank gehostet werden soll.
- Das Administratorkonto, das Sie verwenden, um die Standortsystemrolle zu installieren, muss ein Datenbankbesitzer auf der Instanz eines SQL Servers sein, der die Data Warehouse-Datenbank hosten soll.  
- Die Datenbank wird unterstützt:
  - Mit SQL Server 2012 oder höher, Enterprise oder Datacenter Edition.
  - Auf einer Standard- oder einer benannten Instanz
  - Auf einem *SQL Server-Cluster* Diese Konfiguration sollte funktionieren. Sie wurde jedoch noch nicht getestet und der Support tut alles, was möglich ist.
  - Bei Zusammenstellung mit der Standortdatenbank oder der Reporting Services-Punktdatenbank. Wir empfehlen jedoch eine Installation auf einem separaten Server.  
- Das als *Konto des Reporting Services-Punkts* verwendete Konto benötigt die Berechtigung **db_datareader** für die Data Warehouse-Datenbank.  
- Auf einer *SQL Server Always On-Verfügbarkeitsgruppe* wird die Datenbank nicht unterstützt.

### <a name="install-the-data-warehouse"></a>So installieren Sie Data Warehouse
Installieren Sie die Data Warehouse-Standortsystemrolle auf einem Standort der zentralen Verwaltung oder einem primären Standort, indem Sie den **Assistenten zum Hinzufügen von Standortsystemrollen** oder den **Assistenten zum Erstellen von Standortsystemservern** verwenden. Weitere Informationen finden Sie unter [Installieren von Standortsystemrollen](../servers/deploy/configure/install-site-system-roles.md). Eine Hierarchie unterstützt mehrere Instanzen dieser Rolle, aber es wird von jedem Standort nur eine Instanz unterstützt.  

Bei der Installation einer Rolle erstellt Configuration Manager die Data Warehouse-Datenbank auf der von Ihnen bestimmten Instanz von SQL Server für Sie. Wenn Sie den Namen einer vorhandenen Datenbank angeben (wie beim [Verschieben der Data Warehouse-Datenbank auf einen neuen SQL Server](#move-the-data-warehouse-database)), erstellt Configuration Manager keine neue Datenbank, sondern verwendet die von Ihnen angegebene Datenbank.

#### <a name="configurations-used-during-installation"></a>Konfigurationen, die während der Installation verwendet werden.
Verwenden Sie die folgenden Informationen, um die Installation der Standortsystemrolle abzuschließen:

Seite **Auswahl der Systemrolle**:  
Bevor der Assistent eine Option zur Auswahl und Installation des Data Warehouse-Dienstpunkts installiert, müssen Sie einen Reporting Services-Punkt installiert haben.

Seite **Allgemein**: Die folgenden allgemeinen Informationen werden benötigt:
- **Configuration Manager-Datenbankeinstellungen:**   
  - **Servername**: Geben Sie den FQDN des Servers an, der die Standortdatenbank hostet. Wenn Sie nicht die Standardinstanz von SQL Server verwenden, müssen Sie die Instanz nach dem FQDN im folgenden Format angeben: ***&lt;Sqlserver_FQDN>\&lt; Instanzname>***
  - **Name der Datenbank**: Geben Sie den Namen der Standortdatenbank an.
  - **Überprüfen**: Klicken Sie auf **Überprüfen**, um sicherzustellen, dass die Verbindung mit der Standortdatenbank funktioniert.
</br></br>
- **Data Warehouse-Datenbankeinstellungen:**
  - **Servername**: Geben Sie den FQDN des Servers an, der den Data Warehouse-Dienstpunkt hostet. Wenn Sie nicht die Standardinstanz von SQL Server verwenden, müssen Sie die Instanz nach dem FQDN im folgenden Format angeben: ***&lt;Sqlserver_FQDN>\&lt; Instanzname>***
  - **Name der Datenbank**: Geben Sie den FQDN für die Data Warehouse-Datenbank an.  Configuration Manager erstellt die Datenbank mit diesem Namen. Wenn ein Datenbankname angegeben wird, der bereits in der Instanz von SQL Server existiert, verwendet Configuration Manager diese Datenbank.
  - **Überprüfen**: Klicken Sie auf **Überprüfen**, um sicherzustellen, dass die Verbindung mit der Standortdatenbank funktioniert.

Seite **Synchronisierungseinstellungen**:   
- **Dateneinstellungen:**
  - **Replikationsgruppen synchronisieren**: Wählen Sie die Datengruppen aus, die Sie synchronisieren möchten. Informationen zu den verschiedenen Datengruppentypen finden Sie unter [Datenbankreplikation](../plan-design/hierarchy/data-transfers-between-sites.md#bkmk_dbrep) und **Verteilte Ansichten** unter [Datenübertragungen zwischen Standorten](../plan-design/hierarchy/data-transfers-between-sites.md).
  - **Beim Synchronisieren eingeschlossene Tabellen**: Geben Sie den Namen jeder zusätzlichen Tabelle an, die Sie synchronisieren möchten. Trennen Sie mehrere Tabellen mit einem Komma. Diese Tabellen werden von der Standortdatenbank zusätzlich zu den von Ihnen ausgewählten Replikationsgruppen synchronisiert.
  - **Beim Synchronisieren ausgeschlossene Tabellen**: Geben Sie den Namen jeder einzelnen Tabelle der Replikationsgruppen an, die Sie synchronisieren. Die von Ihnen angegebenen Tabellen werden davon ausgeschlossen. Trennen Sie mehrere Tabellen mit einem Komma.
- **Synchronisierungseinstellungen:**
  - **Synchronisierungsintervall (Minuten)** : Geben Sie einen Wert in Minuten an. Wenn das Intervall erreicht ist, wird eine neue Synchronisierung gestartet. Es wird ein Bereich von 60 bis 1440 Minuten (24 Stunden) unterstützt.
  - **Zeitplan**: Geben Sie die Tage an, an denen die Synchronisierung ausgeführt werden soll.

**Berichterstattungspunktzugriff**:   
Stellen Sie nach dem Installieren der Data Warehouse-Rolle sicher, dass das als *Konto des Reporting Services-Punkts* verwendete Konto über die Berechtigung **db_datareader** für die Data Warehouse-Datenbank verfügt.

#### <a name="troubleshoot-installation-and-data-synchronization"></a>Problembehandlung bei Installation und Datensynchronisierung
Verwenden Sie die folgenden Protokolle zur Untersuchung von Problemen bei der Installation des Data Warehouse-Dienstpunktes oder der Synchronisierung von Daten:
- **DWSSMSI.log** und **DWSSSetup.log**: Verwenden Sie diese Protokolle, um Fehler bei der Installation des Data Warehouse-Dienstpunktes zu untersuchen.
- **Microsoft.ConfigMgrDataWarehouse.log**: Verwenden Sie dieses Protokoll, um die Datensynchronisation zwischen der Standortdatenbank und der Data Warehouse-Datenbank zu untersuchen.

### <a name="reporting"></a>Berichterstellung
Nach der Installation einer Data Warehouse-Standortsystemrolle sind die folgenden Berichte auf Ihrem Reporting Services-Punkt mit einer *Kategorie* des **Data Warehouse** verfügbar:

|Bericht                   | Details                                  |
|-------------------------|------------------------------------------|
| **Anwendungsbereitstellungsbericht** | Anzeigen von Details zur Anwendungsbereitstellung für eine bestimmte Anwendung und einen bestimmten Computer|
| **Endpoint Protection und Software Update-Konformitätsbericht**   | Anzeigen von Computern, auf denen Softwareupdates fehlen.|
| **Bestandsbericht zur gesamten Hardware**  | Anzeigen des gesamten Hardwarebestands für einen bestimmten Computer.|
| **Bestandsbericht zur gesamten Software**  | Anzeigen des gesamten Softwarebestands für einen bestimmten Computer.|
| **Übersicht der Infrastrukturintegrität**  |Zeigt eine Übersicht der Integrität der Configuration Manager-Infrastruktur an.|
| **Liste der erkannten Malware**  |Zeigt Malware an, die in der Organisation gefunden wurde.|
| **Softwareverteilung – Zusammenfassungsbericht** | Eine Zusammenfassung der Softwareverteilung für eine bestimmte Ankündigung und einen bestimmten Computer.|

### <a name="move-the-data-warehouse-database"></a>Verschieben der Data Warehouse-Datenbank
Führen Sie zum Verschieben der Data Warehouse-Datenbank auf einen neuen Server von SQL Server die folgenden Schritte aus:

1. Überprüfen Sie die aktuelle Datenbankkonfiguration, und notieren Sie die Konfigurationsdetails, einschließlich:  
   - Die Datengruppen, die Sie synchronisieren
   - Tabellen, die Sie bei der Synchronisierung ein- oder ausschließen       

   Diese Datengruppen und Tabellen werden erneut konfiguriert werden, nachdem Sie die Datenbank auf einem neuen Server wiederherstellen und die Standortsystemrolle erneut installieren.  

2. Verwenden Sie SQL Server Management Studio zum Sichern der Data Warehouse-Datenbank und dann ebenfalls zum Wiederherstellen dieser Datenbank auf einem SQL-Server auf dem neuen Computer, der das Data Warehouse hostet.

   Nachdem Sie die Datenbank auf dem neuen Server wiederhergestellt haben, stellen Sie sicher, dass die Zugriffsberechtigungen der neuen Data Warehouse-Datenbank identisch zu den ursprüngliche Data Warehouse-Datenbank sind.

3. Verwenden Sie die Configuration Manager-Konsole, um die Standortsystemrolle des Data Warehouse-Dienstpunktes vom aktuellen Server zu entfernen.

4. Installieren Sie einen neuen Data Warehouse-Dienstpunkt, und geben Sie den Namen des neuen Servers von SQL Server und der Instanz an, die die von Ihnen wiederhergestellte Data Warehouse-Datenbank hosten.

5. Nach der Installation der Standortsystemrolle ist der Verschiebevorgang abgeschlossen.

Sie können die folgenden Configuration Manager-Protokolle überprüfen, um sicherzugehen, dass die Standortsystemrolle erfolgreich neu installiert wurde:  
- **DWSSMSI.log** und **DWSSSetup.log**: Verwenden Sie diese Protokolle, um Fehler bei der Installation des Data Warehouse-Dienstpunktes zu untersuchen.
- **Microsoft.ConfigMgrDataWarehouse.log**: Verwenden Sie dieses Protokoll, um die Datensynchronisation zwischen der Standortdatenbank und der Data Warehouse-Datenbank zu untersuchen.


## <a name="content-library-cleanup-tool"></a>Inhaltsbibliothek-Bereinigungstool
Ab Version 1612 von Technical Preview, können Sie ein neues Befehlszeilentool verwenden (**ContentLibraryCleanup.exe**), um Inhalt zu entfernen, der keinem Paket oder keiner Anwendung eines Verteilungspunktes mehr zugeordnet ist (verwaister Inhalt). Dieses Tool heißt Inhaltsbibliothek-Bereinigungstool

Dieses Tool beeinflusst den Inhalt des von Ihnen angegebenen Verteilungspunktes nur dann, wenn Sie das Tool ausführen, und keinen Inhalt aus der Inhaltsbibliothek des Standortservers entfernen können.

Nach der Installation von Technical Preview 1612, finden Sie **ContentLibraryCleanup.exe** im Ordner *%CM_Installation_Path%\cd.latest\SMSSETUP\TOOLS\ContentLibraryCleanup\* auf dem Standortserver von Technical Preview.

Das Tool, das mit dieser Technical Preview herausgegeben wird, soll ältere Versionen von ähnlichen Tools, die für ältere Configuration Manager-Produkte herausgegeben wurden, ersetzen. Obwohl diese Toolversion ab dem 1. März 2017 nicht mehr funktionieren wird, werden neue Versionen mit zukünftigen Technical Previews herausgegeben, bis dieses Tool als Teil von Current Branch oder einer einsatzbereiten Out-of-Band Version herausgegeben wird.

### <a name="requirements"></a>Anforderungen  
- Das Tool kann direkt auf dem Computer ausgeführt werden, der den Verteilungspunkt hostet, oder remote auf einem anderen Server. Das Tool kann jeweils immer nur für einen einzelnen Verteilungspunkt ausgeführt werden.
- Das Benutzerkonto, das das Tool ausführt, muss direkt über die rollenbasierten Administratorenrechte verfügen, die in der Configuration Manager-Hierarchie einem vollständigen Administratorenkonto entsprechen würden.  Das Tool funktioniert nicht, wenn dem Benutzerkonto Mitgliedsrechte einer Windows-Sicherheitsgruppe mit vollständigen Administratorrechten gewährt werden.

### <a name="modes-of-operation"></a>Betriebsmodi
Das Tool kann in zwei Modi ausgeführt werden:
1. **Was-wäre-wenn-Modus**:   
   Wenn Sie den **/delete**-Schalter nicht angeben, wird das Tool im „Was-wäre-wenn“-Modus ausgeführt. Es identifiziert dann den Inhalt, der am Verteilungspunkt gelöscht werden würde, löscht jedoch tatsächlich keine Daten.

   - Wenn das Tool in diesem Modus ausgeführt wird, werden Informationen zu dem Inhalt, der gelöscht werden würde, automatisch in die Protokolldatei des Tools geschrieben. Der Benutzer wird nicht für jeden potentiellen Löschvorgang aufgefordert, diesen zu bestätigen.
   - Standardmäßig wird die Protokolldatei auf dem Computer in den Ordner für temporäre Dateien des Benutzers (temp-Ordner) geschrieben, auf dem das Tool ausgeführt wird. Sie können aber den /log-Schalter verwenden, um die Protokolldatei an einen anderen Speicherort umzuleiten.  
   </br>

   Wir empfehlen Ihnen das Tool in diesem Modus auszuführen und die daraus resultierenden Protokolldateien zu überprüfen, bevor Sie das Tool mit dem /delete-Schalter ausführen.  

2. **Löschmodus**: Wenn Sie das Tool mit dem **/delete**-Schalter ausführen, wird das Tool im Löschmodus ausgeführt.

   - Wenn das Tool in diesem Modus ausgeführt wird, können verwaiste Inhalte, die auf dem angegebenen Verteilungspunkt gefunden werden, aus der Inhaltsbibliothek des Verteilungspunktes gelöscht werden.
   -  Vor dem Löschen jeder Datei, wird der Benutzer aufgefordert, zu bestätigen, dass die Datei gelöscht werden soll.  Sie können **Y** für „Ja“, **N** für „Nein“, oder **Ja, alle** auswählen, um weitere Aufforderungen zu überspringen und alle verwaisten Inhalte zu löschen.  
   </br>

   Wir empfehlen Ihnen das Tool im „Was-wäre-wenn“-Modus auszuführen und die daraus resultierenden Protokolldateien zu überprüfen, bevor Sie das Tool mit dem /delete-Schalter ausführen.  

Wenn das Inhaltsbibliothek-Bereinigungstool in einem der beiden Modi ausgeführt wird, erstellt es automatisch ein Protokoll mit einem Namen, in dem der vom Tool ausgeführte Modus, der Name des Verteilungspunktes sowie Datum und Uhrzeit des Vorgangs enthalten sind. Die Protokolldatei wird automatisch geöffnet, wenn das Tool fertig ist. Standardmäßig wird die Protokolldatei in den **temp**-Ordner des Benutzers auf dem Computer geschrieben, auf dem das Tool ausgeführt wird. Sie können aber einen Befehlslinien-Schalter verwenden, um die Protokolldatei an einen anderen Speicherort umzuleiten. Dazu zählen auch freigegebene Netzwerke.   


### <a name="run-the-tool"></a>Ausführen des Tools
So führen Sie das Tool aus:
1. Öffnen Sie eine administrative Eingabeaufforderung in einen Ordner, in dem sich **ContentLibraryCleanup.exe** befindet.  
2. Geben Sie als nächstes eine Befehlszeile mit den erforderlichen Befehlszeilen-Switches ein sowie die optionalen Switches, die Sie verwenden möchten.

**Bekanntes Problem** Wenn das Tool ausgeführt wird, kann eine Fehlermeldung wie die folgende zurückgegeben werden, wenn ein Paket oder eine Bereitstellung fehlgeschlagen oder gerade in Bearbeitung ist:
-  *System.InvalidOperationException: Diese Inhaltsbibliothek kann jetzt nicht bereinigt werden, da das Paket \<Paket-ID> nicht vollständig installiert ist*.

**Problemumgehung**: Keine. Das Tool kann nicht zuverlässig verwaiste Dateien identifizieren, wenn der Inhalt in Bearbeitung ist oder nicht bereitgestellt werden konnte. Aus diesem Grund kann das Tool den Inhalt nicht bereinigen, bis das Problem gelöst wurde.



### <a name="command-line-switches"></a>Befehlszeilen-Switches  
Die folgenden Befehlszeilen-Switches können in jeglicher Reihenfolge verwendet werden.   

|Schalter|Details|
|---------|-------|
|**/delete**  |**Optional** </br> Verwenden Sie diesen Schalter, wenn Sie Inhalte vom Verteilungspunkt löschen möchten. Sie erhalten eine Aufforderung bevor Inhalt gelöscht wird. </br></br> Wenn dieser Schalter nicht verwendet wird, protokolliert das Tool, welcher Inhalt gelöscht werden würde, löscht aber keine Inhalte vom Verteilungspunkt. </br></br> Beispiel: ***ContentLibraryCleanup.exe /dp server1.contoso.com /delete*** |
| **/q**       |**Optional** </br> Führen Sie das Tool im stillen Modus aus. Hier werden alle Eingabeaufforderungen unterdrückt (z.B. Aufforderungen beim Löschen von Inhalt). Öffnen Sie die Protokolldatei nicht automatisch. </br></br> Beispiel: ***ContentLibraryCleanup.exe /q /dp server1.contoso.com*** |
| **/dp &lt;distribution point FQDN>**  | **Erforderlich** </br> Geben Sie den vollständig qualifizierten Domänennamen (FQDN) des Verteilungspunkts an, den Sie bereinigen möchten. </br></br> Beispiel:  ***ContentLibraryCleanup.exe /dp server1.contoso.com***|
| **/ps &lt;primary site FQDN>**       | **Optional** wenn Inhalt von einem Verteilungspunkt an einem primären Standort bereinigt wird.</br>**Erforderlich** wenn Inhalt von einem Verteilungspunkt an einem sekundären Standort bereinigt wird. </br></br> Geben Sie den FQDN des primären Standorts an, zu dem der Verteilungspunkt gehört, oder geben Sie den übergeordneten primären Standort an, wenn sich der Verteilungspunkt an einem sekundären Standort befindet. </br></br> Beispiel: ***ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com*** |
| **/sc &lt;primary site code>**  | **Optional** wenn Inhalt von einem Verteilungspunkt an einem primären Standort bereinigt wird.</br>**Erforderlich** wenn Inhalt von einem Verteilungspunkt an einem sekundären Standort bereinigt wird. </br></br> Geben Sie den Standordcode des primären Standorts an, zu dem der Verteilungspunkt gehört, oder geben Sie den übergeordneten primären Standort an, wenn sich der Verteilungspunkt an einem sekundären Standort befindet.</br></br> Beispiel: ***ContentLibraryCleanup.exe /dp server1.contoso.com /sc ABC*** |
| **/log \<Protokolldateiverzeichnis>**       |**Optional** </br> Bestimmen Sie ein Verzeichnis zur Ablage der Protokolldateien. Dies kann ein lokales Laufwerk oder eine Netzwerkfreigabe sein.</br></br> Wenn dieser Schalter nicht verwendet wird, werden die Protokolldateien automatisch im temporären Ordner des Benutzers abgelegt.</br></br> Beispiel für ein lokales Laufwerk: ***ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop*** </br></br>Beispiel für eine Netzwerkfreigabe: ***ContentLibraryCleanup.exe /dp server1.contoso.com /log \\&lt;Freigabe>\&lt;Ordner>***|


## <a name="improvements-for-in-console-search"></a>Verbesserungen für die Suche in der Konsole
Aufgrund des User Voice-Feedbacks haben wir die folgenden Verbesserungen für die Suche in der Konsole hinzugefügt:
- **Objektpfad:**  
  Viele Objekte unterstützen jetzt eine neue Spalte namens **Objektpfad**.  Wenn Sie bei Ihrer Suche diese Spalte bei Ihrer Ergebnisanzeige hinzufügen, können Sie den Pfad für jedes Objekt sehen. Wenn Sie beispielsweise eine Suche nach Apps im Knoten „Anwendungen“ durchführen und auch nach untergeordnete Knoten suchen, wird in der *Objektpfad*-Spalte im Ergebnisbereich der Pfad für jedes zurückgegebene Objekt angezeigt.   

- **Erhalt des Suchtextes:**  
  Wenn Sie Text in das Suchfeld eingeben, und dann zwischen der Suche nach einem untergeordneten und dem aktuellen Knoten wechseln, wird der von Ihnen eingegebene Text beibehalten und für die weitere Verwendung zur Verfügung stehen, ohne dass er erneut eingeben werden muss.

- **Entscheidungserhalt bei der Suche in untergeordneten Knoten:**  
  Wenn Sie den Knoten ändern, in dem Sie arbeiten, wird die Option, die Sie sowohl für die Suche in *aktuellen Knoten* als auch für die Suche in *allen untergeordneten Knoten* auswählen, jetzt beibehalten.   Dieses neue Verhalten bedeutet, dass Sie die Entscheidung nicht ständig zurücksetzen müssen, während Sie sich auf der Konsole bewegen.  Beim Öffnen der Konsole ist die Option standardmäßig so festgelegt, dass nur im aktuellen Knoten gesucht wird.

## <a name="prevent-installation-of-an-application-if-a-specified-program-is-running"></a>Verhindern der Anwendungsinstallation, wenn ein bestimmtes Programm ausgeführt wird
Sie können jetzt eine Liste der ausführbaren Dateien (mit der Erweiterung .exe) in den Bereitstellungstyp-Eigenschaften konfigurieren, die, wenn sie ausgeführt werden, die Installation einer Anwendung blockieren. Nach der versuchten Installation, wird den Benutzern ein Dialogfeld angezeigt, in dem sie dazu aufgefordert werden, die Prozesse zu schließen, die die Installation blockieren.

### <a name="try-it-out"></a>Probieren Sie es aus
So konfigurieren Sie eine Liste mit ausführbaren Dateien
1. Wählen Sie auf der Eigenschaftenseite eines beliebigen Bereitstellungstyps die Registerkarte **Installer Handling** (Handler für Installer) aus.
2. Klicken Sie auf **Hinzufügen**, um eine weitere ausführbare Datei zur Liste hinzuzufügen (z.B. **Edge.exe**)
3. Klicken Sie auf **OK**, um das Dialogfeld zu Bereitstellungstyp-Eigenschaften zu schließen.

Wenn Sie diese Anwendung jetzt für einen Benutzer oder ein Gerät bereitstellen und eine der von Ihnen hinzugefügten ausführbaren Dateien ausgeführt wird, sieht der Endbenutzer ein Software Center-Dialogfeld, das ihn darüber informiert, dass die Installation fehlgeschlagen ist, weil eine Anwendung ausgeführt wird.

## <a name="new-windows-hello-for-business-notification-for-end-users"></a>Die neue Windows Hello for Business-Benachrichtigung für Endbenutzer

Eine neue Windows 10-Benachrichtigung informiert Benutzer, dass zusätzliche Aktionen abgeschlossen werden müssen, um die Installation von Windows Hello für Business (z.B. Einrichten einer PIN) abzuschließen.

## <a name="windows-store-for-business-support-in-configuration-manager"></a>Support des Windows Store für Unternehmen in Configuration Manager

Online lizenzierte Apps können jetzt mit dem Bereitstellungszweck **Verfügbar** aus dem Windows Store für Unternehmen auf PCs bereitgestellt werden, die den Configuration Manager-Client ausführen.
Weitere Einzelheiten finden Sie unter [Verwalten von Apps aus dem Microsoft Store für Unternehmen mit Configuration Manager](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

Die Unterstützung dieser Funktion ist derzeit nur für PCs mit der Vorabversion von Windows 10 RS2 verfügbar.

## <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Zurück zur vorherigen Seite, wenn eine Tasksequenz fehlschlägt
Sie können jetzt zu einer vorherigen Seite zurückkehren, wenn Sie eine Tasksequenz ausführen und ein Fehler auftritt. Bevor es diese Version gab, mussten Sie die Tasksequenz neu starten, wenn ein Fehler aufgetreten ist. In den folgenden Szenarios können Sie zum Beispiel die Schaltfläche **Zurück** verwenden:

- Beim Starten eines Computers in Windows PE wird möglicherweise der Bootstrap-Dialog der Tasksequenz angezeigt, bevor die Tasksequenz verfügbar ist. Wenn Sie in diesem Szenario auf „Weiter“ klicken, wird auf der letzten Seite der Tasksequenz eine Nachricht angezeigt, die darüber informiert, dass es keine verfügbaren Tasksequenzen gibt. Klicken Sie jetzt auf **Zurück**, um erneut nach verfügbaren Tasksequenzen zu suchen. Sie können diesen Vorgang wiederholen, bis die Tasksequenz verfügbar ist.
- Wenn die abhängigen Paketinhalte beim Ausführen einer Tasksequenz an den Verteilungspunkten noch nicht verfügbar sind, kann die Tasksequenz nicht ausgeführt werden. Sie können jetzt die fehlende Inhalte verteilen (wenn diese noch nicht verteilt wurden). Sie können auch warten, bis die Inhalte auf den Verteilungspunkten verfügbar sind, und dann auf **Zurück** klicken, damit die Tasksequenz wieder nach den Inhalten sucht.

## <a name="express-installation-files-support-for-windows-10-updates"></a>Unterstützung von Express-Installationsdateien für Windows 10-Updates
Für Windows 10-Updates wurde Support für die Expressinstallationsdateien in Configuration Manager hinzugefügt. Wenn Sie eine unterstützte Version von Windows 10 verwenden, können Sie jetzt die Configuration Manager-Einstellungen nutzen, um nur das Delta zwischen dem kumulativen Update von Windows 10 des laufenden Monats und dem Updates des Vormonats herunterzuladen. Im Moment werden die kompletten kumulativen Updates für Windows 10 (einschließlich aller Updates aus den letzten Monaten) jeden Monat im aktuellen Branch des Configuration Manager heruntergeladen. Mit Expressinstallationsdateien erhalten Sie kleinere Downloads und kürzere Installationszeiten.

> [!IMPORTANT]
> Während die Einstellungen zur Unterstützung der Verwendung von Express-Installationsdateien in Configuration Manager zur Verfügung stehen, wird diese Funktion nur von Windows 10 Version 1607 mit einem Update von Windows Update-Agent, das Teil der am 10.01.2017 (Patch-Dienstag) veröffentlichten Updates ist, unterstützt. Weitere Informationen zu diesen Updates finden Sie im [Supportartikel 3213986](https://support.microsoft.com/help/4009938/january-10-2017-kb3213986-os-build-14393-693). Sie können von Schnellinstallationsdateien profitieren, wenn die nächste Reihe von Updates am 14.02.2017 veröffentlicht wird. Die Expressinstallationsdateien werden von älteren Versionen von Windows und von Windows 10 Version 1607 ohne Update nicht unterstützt.


### <a name="to-enable-the-download-of-express-installation-files-for-windows-10-updates-on-the-server"></a>So aktivieren Sie den Download von Expressinstallationsdateien für Windows 10-Updates auf dem Server
Um mit der Synchronisierung der Metadaten für Windows 10-Expressinstallationsdatein zu beginnen, müssen Sie dies in den Punkteigenschaften des Software Updates aktivieren.
1. Wechseln Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Standortkonfiguration** > **Standorte**.
2. Wählen Sie entweder den Standort der zentralen Verwaltung oder den eigenständigen primären Standort aus.
3. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Einstellungen** auf **Standortkomponenten konfigurieren**, und klicken Sie dann auf **Softwareupdatepunkt**. Wählen Sie auf der Registerkarte **Updatedateien** die Option  **Vollständige Dateien für alle genehmigten Windows 10-Expressinstallationsdateien herunterladen** aus.

### <a name="to-enable-support-for-clients-to-download-and-install-express-installation-files"></a>So aktivieren Sie die Clientunterstützung für das Herunterladen und Installieren von Expressinstallationsdateien
Um die Unterstützung der Expressinstallationsdatein auf Clients zu aktivieren, müssen Sie die Expressinstallationsdateien auf Clients im Bereich Software Updates der Clienteinstellungen aktivieren. Dadurch wird ein neuer HTTP-Listener erstellt, der Anfragen zum Herunterladen von Expressinstallationsdateien auf den Port, den Sie angeben, abruft. Sobald Sie die Clienteinstellungen zur Aktivierung dieser Funktionalität auf dem Client bereitstellen, wird diese versuchen, das Delta zwischen dem kumulativen Update von Windows 10 des aktuellen Monat und dem Update des Vormonats herunterzuladen (Clients müssen eine Version von Windows 10 ausführen, die Espressinstallationsdateien unterstützt).
1. Aktivieren Sie „Expressinstallationsdateien unterstützten“ in den Komponenteneigenschaften des Softwareupdatepunks (vorheriger Vorgang).
2. Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Clienteinstellungen**.
3. Wählen Sie die entsprechenden Clienteinstellungen aus, und klicken Sie dann in der Registerkarte **Home** auf **Eigenschaften**.
4. Wählen Sie die Seite **Softwareupdates** aus, konfigurieren Sie **Ja** für die Einstellung **Enable installation of Express Updates on clients** (Installation von Express-Updates auf Clients aktivieren), und konfigurieren Sie den Port, der für den HTTP-Listener auf dem Client für die Einstellung **Port used to download content for Express Updates** (Zum Herunterladen von Inhalt für Express-Updates verwendeter Port) verwendet wird.


## <a name="odata-endpoint-data-access"></a>Datenzugriff für OData-Endpunkt

 Configuration Manager bietet jetzt einen RESTful OData-Endpunkt für den Zugriff auf Configuration Manager-Daten. Der Endpunkt ist kompatibel mit Version 4 von Odata, die es Tools wie Excel oder Power BI ermöglicht, über einen einzelnen Endpunkt problemlos auf Configuration Manager-Daten zuzugreifen. Technical Preview 1612 unterstützt nur den Lesezugriff auf Objekte in Configuration Manager.  

Auf Daten, die aktuell im [Configuration Manager-WMI-Anbieter](../../develop/reference/configuration-manager-reference.md) verfügbar sind, kann jetzt auch mit dem neuen OData RESTful-Endpunkt zugegriffen werden. Die Entitätenmengen, die vom OData-Endpunkt verfügbar gemacht werden, machen es möglich, die gleichen Daten aufzulisten, die auch mit dem WMI-Anbieter abgefragt werden können.

### <a name="try-it-out"></a>Probieren Sie es aus

Bevor Sie den OData-Endpunkt verwenden können, müssen Sie ihn für die Seite aktivieren.

1.  Klicken Sie auf **Verwaltung** > **Standortkonfiguration** > **Standorte**.
2.  Wählen Sie den primären Standort aus, und klicken Sie auf **Eigenschaften**.
3.  Klicken Sie auf der Seite zu Eigenschaften des primären Standorts auf der Registerkarte „Allgemein“ auf **Enable REST endpoint for all providers on this site** (REST-Endpunkt für alle Anbieter an diesem Standort aktivieren), und klicken Sie dann auf **OK**.

Versuchen Sie in Ihrem bevorzugten OData-Abfrageviewer ähnliche Abfragen, wie in den folgenden Beispielen angegeben, durchzuführen, um verschiedene Objekte in Configuration Manager zurückzugeben.

| Zweck | OData-Abfrage |
|---|---|
| Alle Sammlungen abrufen | `http://localhost/CMRestProvider/Collection` |
| Sammlungen abrufen | `http://localhost/CMRestProvider/Collection('SMS00001')`
| Die wichtigsten 100 Geräte in der Sammlung abrufen | `http://localhost/CMRestProvider/Collection('SMS00001')/Device?$top=100` |
| Ein Gerät mit einer Ressourcen-ID in der Sammlung abrufen | `http://localhost/CMRestProvider/Collection('SMS00001')/Device(16777573)` |
| Betriebssystem des Geräts in der Sammlung abrufen | `http://localhost/CMRestProvider/Collection('SMS00001')/Device(16777573)/OPERATING_SYSTEM` |
| Benutzer in der Sammlung abrufen | `http://localhost/CMRestProvider/Collection('SMS00001')/User` |

> [!NOTE]
> Die Beispielabfragen, wie in der Tabelle angezeigt, verwenden *Localhost* als Hostname in der URL und können auf dem Computer verwendet werden, die den SMS-Anbieter ausführen. Wenn Sie Ihre Abfragen auf einem anderen Computer ausführen, ersetzen Sie Localhost mit dem FQDN des Servers, auf dem der SMS-Anbieter installiert ist.

## <a name="azure-active-directory-onboarding"></a>Azure Active Directory-Onboarding

Das Onboarding von Azure Active Directory (AD) stellt eine Verbindung zwischen Configuration Manager und Azure Active Directory für die Verwendung von anderen Clouddiensten her. Dies kann momentan dazu verwendet werden, die notwendige Verbindung mit dem Cloudverwaltungsgateway herzustellen.

Führen Sie diese Aufgabe als Azure-Administrator aus, denn Sie werden die Azure-Anmeldeinformationen als Administrator benötigen.

#### <a name="to-create-the-connection"></a>So stellen Sie eine Verbindung her:

2. Wählen Sie **Clouddienste** > **Azure Active Directory** > **Add Azure Active Directory** (Hinzufügen von Azure Active Directory) im Arbeitsbereich **Verwaltung** aus.
2. Wählen Sie **Anmelden** aus, um eine Verbindung mit Azure AD herzustellen.

#### <a name="configuration-manager-client-requirements"></a>Anforderungen für Configuration Manager-Client

Es gibt mehrere Anforderungen für die Aktivierung der Benutzerrichtlinieneinrichtung im Cloudverwaltungsgateway.

- Der Azure AD-Onboardingprozess muss abgeschlossen sein, und der Client muss zunächst mit dem Unternehmensnetzwerk verbunden sein, um die Verbindungsinformationen zu erhalten.
- Clients müssen sowohl einer Domäne angehören (in Active Directory registriert) als auch einer Clouddomäne (in Azure AD registriert) angehören.
- Konfigurieren einer [Active Directory-Benutzerermittlung](../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)
- Sie müssen den Configuration Manager-Client ändern, um Benutzerrichtlinienanforderung über das Internet zu ermöglichen, und dem Client die Änderung bereitzustellen. Da der Client *auf dem Clientgerät* geändert wird,kann das Cloudverwaltungsgateway bereitgestellt werden, obwohl die erforderlichen Konfigurationsänderungen für die Benutzerrichtlinie noch nicht abgeschlossen sind.
- Ihr Verwaltungspunkt muss konfiguriert werden, um HTTPS zu verwenden, um den Token auf dem Netzwerk zu speichern. Es muss außerdem .NET 4.5 installiert sein.

Nachdem Sie diese Konfigurationsänderungen vollzogen haben, können Sie eine Benutzerrichtlinie erstellen und Clients ins Internet verschieben, um die Richtlinie zu testen. Benutzerrichtlinienanforderungen über das Cloudverwaltungsgateway werden mit der tokenbasierten Authentifizierung von Azure AD authentifiziert.

## <a name="change-to-configuring-multi-factor-authentication-for-device-enrollment"></a>Ändern der Konfiguration der Multi-Factor Authentication zur Registrierung des Geräts

Jetzt da Sie Multi-Factor Authentication (MFA) zur Geräteregistrierung im Azure-Portal einrichten können, wurde die MFA-Option aus der Configuration Manager-Konsole entfernt. Weitere Informationen zum Einrichten von MFA bei der Anmeldung finden Sie [in diesem Microsoft Intune-Thema](/mem/intune/enrollment/multi-factor-authentication)
