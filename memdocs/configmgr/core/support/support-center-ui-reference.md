---
title: Referenz zur Benutzeroberfläche des Supportcenters
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie die Tools im Supportcenter verwenden können.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 41cdebfe-b595-40aa-a385-32e0746255ed
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 79d483f95c12c1da1e34ca556836a1f42bbffbef
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699448"
---
# <a name="support-center-user-interface-reference"></a>Referenz zur Benutzeroberfläche des Supportcenters

*Gilt für: Configuration Manager (Current Branch)*

In diesem Artikel wird die Benutzeroberfläche der Tools des Supportcenters beschrieben:
- Supportcenter
- Protokollanzeige des Supportcenters
- Supportcenteranzeige



## <a name="support-center-reference"></a>Referenz zum Supportcenter

In diesem Abschnitt wird die Benutzeroberfläche des **Supportcentertools** beschrieben. 
- [Menü „Fenster“](#bkmk_support-window)  
- [Registerkarte „Startseite“](#bkmk_support-home)  
- [Registerkarte „Client“](#bkmk_support-client)  
- [Registerkarte „Richtlinie“](#bkmk_support-policy)  
- [Registerkarte „Inhalt“](#bkmk_support-content)  
- [Registerkarte „Inventur“](#bkmk_support-inventory)  
- [Registerkarte „Problembehandlung“](#bkmk_support-troubleshoot)  
- [Registerkarte „Protokolle“](#bkmk_support-logs)  


### <a name="window-menu"></a><a name="bkmk_support-window"></a> Menü „Fenster“

Klicken Sie in der oberen linken Ecke des Supportcenters auf den Pfeil im blauen Kästchen, um dieses Menü zu öffnen.

#### <a name="local-machine-connection"></a>Lokale Computerverbindung
Im Supportcenter werden Protokolldateien gesammelt, und die Problembehandlung wird für den Client durchgeführt, auf dem das Supportcenter ausgeführt wird.

#### <a name="remote-connection"></a>Remoteverbindung
Stellen Sie eine Remoteverbindung mit einem anderen Konfigurations-Manager-Client her. Nach der Verbindung werden im Supportcenter Protokolldateien gesammelt, und die Problembehandlung wird für den Client durchgeführt, mit dem es verbunden ist.

#### <a name="about"></a>Informationen zu
Stellt Informationen zum Supportcenter bereit.

#### <a name="options"></a>Optionen
Im Dialogfeld **Optionen** können Sie folgende Einstellungen vornehmen:
- Sie können die Bewegung der animierten Benutzeroberflächenelemente reduzieren.  
- Sie können den Standardspeicherort für Datenpaketdateien ändern.  
- Sie können den Speicherort für temporäre Dateien ändern.    
- Sie können Warnungen zurücksetzen. Alle Warnmeldungen, die Sie zuvor unterdrückt haben, werden erneut angezeigt, wenn sie ausgelöst werden.  
- Sie können den Pfad für temporäre Dateien auf die Standardeinstellung (`%UserProfile%\AppData\Local\Microsoft\ConfigMgrSupportCenter`) zurücksetzen.

#### <a name="exit"></a>Beenden
Schließt das Supportcenter.



### <a name="home-tab"></a><a name="bkmk_support-home"></a> Registerkarte „Startseite“

#### <a name="collect-selected-data"></a>Ausgewählte Daten sammeln
Das Supportcenter sammelt Informationen aus dem Konfigurations-Manager-Client. Standardmäßig wird Folgendes gesammelt:
- Protokolldateien
- Clientkonfigurationsammler
- Betriebssystem

Sie können andere Arten von Informationen sammeln, indem Sie das Kontrollkästchen neben dem jeweiligen Namen aktivieren.

Wählen Sie das Dropdownmenü unter der Schaltfläche **Ausgewählte Daten sammeln** auf dem Menüband aus, und klicken Sie auf **Alle Daten sammeln**. Dadurch werden alle Daten über den Clientzustand gesammelt.

Sie können während der Datensammlung auf **Cancel collection** (Sammlung abbrechen) klicken, um diese zu beenden.

#### <a name="data-types"></a>Datentypen
Wenn Sie das Kontrollkästchen für eine Option aktivieren, sammelt das Supportcenter diese Daten, wenn Sie das nächste Mal auf **Ausgewählte Daten sammeln** klicken. Folgende Dateitypen sind verfügbar:  

- **Protokolldateien:** Clientprotokolldateien, einschließlich Setupprotokollen  

- **Richtlinie:** Clientrichtliniensammlung  

- **Zertifikate:** Informationen zu öffentlichen Schlüsseln für Clientzertifikate. Das Supportcenter sammelt keine privaten Zertifikatschlüssel.  

- **Clientkonfigurationsammler:** Informationen zum Konfigurations-Manager-Client. Sie können diesen Datentyp nicht deaktivieren.  

- **Clientregistrierung:** Sammelt Informationen zur Clientkonfiguration aus der Registrierung. Das Supportcenter sammelt nur Informationen zur Configuration Manager-Registrierung.  

- **Client-WMI:** Informationen zur Clientkonfiguration aus der Windows-Verwaltungsinstrumentation (WMI). Das Supportcenter sammelt keine Clientrichtlinien.  

- **Problembehandlung:** Echtzeit-Problembehandlungsdaten für die Diagnose von üblichen Clientproblemen mit Active Directory, Verwaltungspunkten, Netzwerken, Richtlinienzuweisungen und der Registrierung.  

    > [!NOTE]  
    > Dieser Datentyp wird nicht unterstützt, wenn Sie eine Remoteverbindung mit einem anderen Client herstellen.  

- **Debugdumps:** Führt einen Debugdump für den Client und die verwandten Prozesse durch. Debugdumps können sehr groß sein. Aktivieren Sie diese Option nur, wenn Sie Probleme mit der Leistung des Clients beheben müssen.  

    > [!WARNING]  
    > Die Sammlung von Debugdumps führt zu sehr großen Datenpaketen (in einigen Fällen mehrere hundert MB).  
    >  
    > Debugdumps enthalten möglicherweise vertrauliche Informationen, z.B. Kennwörter, kryptografische Schlüssel oder Benutzerdaten. Debugdumps sollten nur auf Empfehlung eines Mitarbeiters des Microsoft-Supports gesammelt werden. Datenpakete, die Debugdumps enthalten, sollten sorgfältig verwaltet werden, um diese vor nicht autorisiertem Zugriff zu schützen.  
    >  
    > Dieser Datentyp wird nicht unterstützt, wenn Sie eine Remoteverbindung mit einem anderen Client herstellen.  

- **Betriebssystem:** Erfasst Konfigurationsinformationen über den lokalen Computer. Zu diesen Daten zählen Informationen über die Windows-Installation, die Netzwerkadapter und die Konfiguration des Systemdiensts. Sie können diesen Datentyp nicht deaktivieren.  



### <a name="client-tab"></a><a name="bkmk_support-client"></a> Registerkarte „Client“

#### <a name="load-or-refresh"></a>Laden oder aktualisieren
Das Supportcenter lädt oder aktualisiert Details zum Konfigurations-Manager-Client.

#### <a name="control-client-agent-service"></a>Client-Agent-Dienst steuern
Führen Sie eine der folgenden Aktionen im Dienst des Konfigurations-Manager-Client-Agents (ccmexec) auf dem verbundenen Client durch:  

- **Client neu starten**  

    > [!IMPORTANT]  
    > Wenn der Client-Agent-Dienst nicht neu gestartet wird, kann der Client nicht vom Configuration Manager verwaltet werden, bis der Dienst neugestartet wird.  

- **Client starten**  

- **Client beenden**  

    > [!IMPORTANT]  
    > Der Client kann nicht von Configuration Manager verwaltet werden, bis der Dienst neu gestartet wird.  

#### <a name="properties"></a>Eigenschaften
Wenn Sie Details zu Clients laden, zeigt das Supportcenter folgende Eigenschaften an:  

- **Client-ID:** Ein eindeutiger Bezeichner, der von Configuration Manager zum Identifizieren des Clients verwendet wird  

- **Hardware-ID:** Ein eindeutiger Bezeichner, der von Configuration Manager zum Identifizieren der Clienthardware verwendet wird  

- **Genehmigt:** Gibt an, dass der Client in Configuration Manager genehmigt wurde  

- **Registrierungsstatus:** Gibt an, ob der Client bei Configuration Manager registriert ist  

- **Internet-facing** (Internetzugriff): Gibt an, ob der Client mit dem Internet verbunden ist  

- **Version:** Die Versionsnummer des installierten Konfigurations-Manager-Clients  

- **Standortcode:** Der Standortcode für den primären Standort, dem der Client zugewiesen ist  

- **Zugewiesener Verwaltungspunkt:** Der vollqualifizierte Domänenname (FQDN) des Verwaltungspunkts, der dem Client derzeit zugewiesen ist  

- **Residenter Verwaltungspunkt:** Der FQDN des residenten Verwaltungspunkts  

- **Proxyverwaltungspunkt:** Der Hostname oder FQDN des Proxyverwaltungspunkts (falls vorhanden)  

- **Proxystandortcode:** Der Standortcode für den sekundären Standort (falls vorhanden)  

- **Proxyzustand:** Der Zustand des Proxyverwaltungspunkts des Konfigurations-Manager-Clients, z.B. **Aktiv** oder **Ausstehend**  



### <a name="policy-tab"></a><a name="bkmk_support-policy"></a> Registerkarte „Richtlinie“

Verwenden Sie die Aktionen auf dieser Registerkarte anstelle des älteren Tools [PolicySpy](policy-spy.md).

#### <a name="load-policy"></a>Richtlinie laden
Diese Option variiert je nach Ansicht:

- **Tatsächliche Richtlinie laden:** Wählen Sie **Tatsächlich** in der Gruppe „Ansicht“ aus, und wählen Sie diese Option dann in der Gruppe „Richtlinie“ aus. Das Supportcenter lädt die Clientrichtlinie, die Sie derzeit ausgewählt haben.  

- **Angeforderte Richtlinie laden:** Wählen Sie **Angefordert** in der Gruppe „Ansicht“ aus, und wählen Sie diese Option dann in der Gruppe „Richtlinie“ aus. Das Supportcenter lädt die Clientrichtlinie, die vom Client angefordert wird.  

- **Standardrichtlinie laden:** Wählen Sie **Standard** in der Gruppe „Ansicht“ aus, und wählen Sie diese Option dann in der Gruppe „Richtlinie“ aus. Das Supportcenter lädt die Standardrichtlinie für diesen Client.  

Wählen Sie die Dropdownliste unter dieser Schaltfläche aus, um zusätzliche Optionen anzuzeigen:

- **Alle laden oder aktualisieren:** Lädt oder aktualisiert gleichzeitig die aktuelle, die angeforderte und die Standardrichtlinie  

#### <a name="actual-view"></a>Ansicht „Aktuell“
Öffnet die aktuelle Richtlinienansicht

#### <a name="requested-view"></a>Ansicht „Angefordert“
Öffnet die angeforderte Richtlinienansicht

#### <a name="default-view"></a>Ansicht „Standard“
Öffnet die Ansicht für die Standardrichtlinie. (Diese Richtlinie wird von Geräten abgerufen, wenn Sie den Konfigurations-Manager-Client installieren.)

#### <a name="request-and-evaluate-policy"></a>Richtlinie anfordern oder auswerten
Das Supportcenter fordert die Clientrichtlinie vom Verwaltungspunkt an und wertet sie dann auf dem Client aus.

Wählen Sie die Dropdownliste unter dieser Schaltfläche aus, um zusätzliche Optionen anzuzeigen:  

- **Richtlinie anfordern:** Das Supportcenter fordert die Clientrichtlinie vom Verwaltungspunkt an.  

- **Richtlinie auswerten:** Das Supportcenter wertet die Clientrichtlinie auf dem Client aus.  

- **Standardrichtlinie wiederherstellen:** Das Supportcenter weist den Konfigurations-Manager-Client dazu an, die Standardrichtlinie erneut anzuwenden. Alle Computer- und Benutzerrichtlinien werden vom Client entfernt.  

#### <a name="listen-for-policy-events"></a>Richtlinienereignisse überwachen
Das Supportcenter lauscht Richtlinienereignissen. Deaktivieren Sie diese Option, um das Lauschen auf Richtlinienereignisse zu deaktivieren. Klicken Sie auf den Pfeil im unteren Bereich dieser Registerkarte, um die **Richtlinienereignisse** anzuzeigen. 

#### <a name="clear-events"></a>Ereignisse löschen
Das Supportcenter löscht alle Richtlinienereignisse.



### <a name="content-tab"></a><a name="bkmk_support-content"></a> Registerkarte „Inhalt“

Hier können Sie alle Inhalte auf dem Client anzeigen, auch zwischengespeicherte Inhalte. Überwachen Sie den Fortschritt der Bereitstellung von Softwareupdates und Anwendungen. 

#### <a name="load-or-refresh"></a>Laden oder aktualisieren
*Gilt für die Ansichten „Inhalt“ und „Cache“*

Das Supportcenter lädt oder aktualisiert die Liste des aktuellen Inhalts des Clients.

#### <a name="invoke-trigger"></a>Invoke trigger (Trigger aufrufen)
Mithilfe der folgenden Elemente in diesem Menü können mit dem Inhalt im Zusammenhang stehende Clientaktionen angefordert werden:  

- **Standortdienste**  

    - **Refresh content locations** (Inhaltsorte aktualisieren): Aktualisiert die von aktiven Inhaltsdownloads verwendeten Verteilungspunkte.  

    - **Refresh management points** (Verwaltungspunkte aktualisieren): Aktualisiert die interne Liste der vom Client verwendeten Verwaltungspunkte.  

    - **Time out content requests** (Zeitüberschreitung bei Inhaltsanforderungen): Wenn Anforderungen von Inhaltsspeicherorten zu lange ausgeführt werden, beendet diese Aktion die Anforderung.  

- **Application deployment evaluation** (Auswertung der Anwendungsbereitstellung): Startet eine Aufgabe, die bereitgestellte Anwendungen auswertet.  

- **Software updates deployment evaluation** (Auswertung der Softwareupdatebereitstellungen): Startet eine Aufgabe, die bereitgestellte Softwareupdates auswertet.  

- **Software updates source scan** (Überprüfung der Softwareupdatequellen): Startet eine Aufgabe, die Updatequellspeicherorte überprüft.  

- **Windows Installer source list update** (Aktualisierung der Windows Installer-Quellenliste): Startet eine Aufgabe, die den Quellspeicherort für Installationen von Windows Installer (MSI) aktualisiert.  

#### <a name="content-view"></a>Inhaltsansicht
Hier werden die auf dem Client geladenen Anwendungen, Pakete und Updates angezeigt. Wenn Sie auf eine Anwendung, ein Paket oder Update klicken, werden Details zu diesem Inhalt angezeigt. Für einige Anwendungen können Sie zudem folgende Aktionen ausführen:  

- **Aktualisieren:** Aktualisiert die Detailansicht  

- **Überprüfen/Herunterladen:** Überprüft, ob eine Anwendung zum Download verfügbar ist.  

- **Installieren:** Installiert die Anwendung  

- **Deinstallieren:** Die Anwendung deinstallieren  

#### <a name="cache-view"></a>Ansicht „Cache“
Hier werden die Clientcachekonfiguration und Details zum Cacheinhalt angezeigt. Wenn Sie das Supportcenter mit einem lokalen Client verbinden, können Sie zudem folgende Aktionen durchführen:  

- Klicken Sie neben dem Feld **Cachespeicherort** auf **Ändern**, um den Cachespeicherort zu ändern.  

- Klicken Sie neben dem Feld **Cachegröße** auf **Ändern**, um die Cachegröße anzupassen.  

- Klicken Sie neben dem Feld **Verwendeter Cache** auf **Löschen**, um den Clientcache zu löschen.  

Diese Ansicht zeigt die folgenden Eigenschaften an:  

- **Speicherort:** Der Speicherort der einzelnen Cacheordner. Klicken Sie auf den Link, um den Ordner im Windows-Explorer zu öffnen.   
- **Inhalts-ID**  
- **Cache-ID**  
- **Size**  
- **Last Referenced** (Zuletzt referenziert): Diese Eigenschaft entspricht dem Datum, an dem der Client dieses Element im Cache zuletzt gelesen oder in dieses geschrieben hat.  

#### <a name="monitoring-view"></a>Ansicht „Überwachung“
Wählen Sie **Überwachung** aus, um den aktiven Fortschritt der Bereitstellung von Softwareupdates und Anwendungsupdates anzuzeigen. In dieser Ansicht werden Zustandsmeldungen angezeigt, die von Anwendungs- und WMI-Ereignismeldungen für Softwareupdates ausgelöst werden.

Diese Ansicht zeigt für jedes Ereignis die folgenden Eigenschaften an:  

- **Zeit**: Der Zeitpunkt, zu dem der Client das Ereignis ausgelöst hat  
- **Thementyp:** Der Typ der Zustandsmeldung  
- **Themen-ID:** ID der Zustandsmeldung, die zum Zuordnen von Ereignissen in Protokolldateien verwendet wurde  
- **Themen-ID-Typ:** Der Untertyp der Zustandsmeldung  
- **Zustands-ID:** Das Ergebnis der überwachten Aktion  
- **Details** und **Ereignisdaten**: Weitere Informationen zu den Zustandsmeldungen, die in dieser Ansicht angezeigt werden Zustandsdetails können auch leer sein.  



### <a name="inventory-tab"></a><a name="bkmk_support-inventory"></a> Registerkarte „Inventur“

#### <a name="load-or-refresh"></a>Laden oder aktualisieren
Das Supportcenter lädt oder aktualisiert die Clientinventurliste für die derzeit ausgewählte Ansicht.

#### <a name="invoke-trigger"></a>Invoke trigger (Trigger aufrufen)

> [!Note]  
> Für andere Aufgaben als **Softwaremessungs-Berichtszyklus**:  
> - Wenn Sie den Task angefordert haben, während ein anderer Inventurtask ausgeführt wird, wird der neue Task vom Client in die Warteschlange eingereiht, damit dieser ausgeführt wird, nachdem der aktuelle Task und andere Tasks in der Warteschlange ausgeführt wurden.  
> - Sie können den Fortschritt des Tasks in **InventoryAgent.log** nachverfolgen.  

Mithilfe der folgenden Elemente in diesem Menü können mit der Inventur im Zusammenhang stehende Clientaktionen angefordert werden:  

- **Ermittlungsdaten-Sammlungszyklus (Takt):** Löst den zur Sammlung von Geräteermittlungsdaten verwendeten Clienttask aus.  

- **Dateisammlungszyklus:** Löst den zur Sammlung von lokalen Dateien verwendeten Clienttask aus.  

- **Hardwareinventurzyklus:** Löst den zur Sammlung von Hardwareinventurdaten verwendeten Clienttask aus.  

- **IDMIF-Sammlungszyklus:** Löst den zur Sammlung von IDMIF-Daten verwendeten Clienttask aus.  

- **Softwareinventurzyklus:** Löst den zur Sammlung von Softwareinventurdaten verwendeten Clienttask aus.  

- **Berichtzyklus für Softwaremessungsnutzung:** Löst die zum Erstellen und Senden eines Softwaremessungsberichts an den Verwaltungspunkt verwendete Clientaufgabe aus. Sie können den Fortschritt dieses Tasks in **SWMTRReportGen.log** nachverfolgen.

- **Nicht gesendete Zustandsmeldungen in Warteschlange senden:** Löst die zum Leeren der Warteschlange von Zustandsmeldungen verwendete Clientaufgabe aus.

- **Erweitert**  
    - **Hardwareinventurzyklus (vollständige Neusynchronisierung)**  
    - **Softwareinventurzyklus (vollständige Neusynchronisierung)**  


#### <a name="views"></a>Ansichten
Wenn ein Feature nicht aktiviert ist, zeigt die Ansicht keine Daten an. 

- **Status:** Zeigt die Inventurdatasets an, die der Client gesammelt hat  

- **DDR:** Informationen zu den vom Client gesammelten Clientermittlungsdaten  

- **HINV:** Informationen zu den vom Client gesammelten Hardwareinventurdaten  

- **SINV:** Informationen zu den vom Client gesammelten Softwareinventurdaten  

- **Dateisammlung:** Informationen zu den vom Client gesammelten Dateien  

- **IDMIF:** Informationen zu den vom Client gesammelten IDMIF- und NOIDMIF-Daten  

- **Messung:** Informationen zu den vom Client gesammelten Softwaremessungsdaten  



### <a name="troubleshooting-tab"></a><a name="bkmk_support-troubleshoot"></a> Registerkarte „Problembehandlung“

Hier können einige der am häufigsten auftretenden Probleme mit Konfigurations-Manager-Clients behoben werden:  
- Probleme mit Active Directory  
- Windows-Netzwerke  
- Configuration Manager   
    - Verwaltungspunkte  
    - Richtlinienzuweisung  
    - Registrierung  


> [!NOTE]  
> Diese Registerkarte ist nicht verfügbar, wenn Sie eine Verbindung mit einem Konfigurations-Manager-Remoteclient herstellen.


#### <a name="start"></a>Starten
Startet die Problembehandlung beim Client

- **Active Directory:** Fragt Active Directory zum Abrufen veröffentlichter Configuration Manager-Standortinformationen ab  
- **MPCERTIFICATE:** Ruft Verwaltungspunktzertifikate ab  
- **MPLIST:** Ruft eine Liste von Verwaltungspunkten ab  
- **MPKEYINFORMATION:** Ruft kryptografische Schlüsselinformationen von Verwaltungspunkten ab  
- **Netzwerk:** Behebt Probleme mit Netzwerken  
- **Richtlinienzuweisungen:** Ruft die Richtlinienzuweisungen ab  
- **Registrierung:** Überprüft, ob der Client am Standort registriert ist  

#### <a name="view-selected-log"></a>Ausgewähltes Protokoll anzeigen
Nachdem Sie eine Zeile auf der Registerkarte „Problembehandlung“ ausgewählt haben, können Sie diese Aktion ausführen, um die Protokolldatei anzuzeigen.

#### <a name="keep-previous-results"></a>Vorherige Ergebnisse beibehalten
Wenn Sie die Problembehandlung beim Client erneut durchführen möchten, wählen Sie diese Option aus, um die Ergebnisse des ersten Versuchs beizubehalten. Andernfalls überschreibt das Supportcenter die vorherigen Protokolldateien der Problembehandlung.



### <a name="logs-tab"></a><a name="bkmk_support-logs"></a> Registerkarte „Protokolle“

Dieser Abschnitt führt die Elemente der Registerkarte **Protokolle** des Supportcentertools auf. 

Diese Registerkarte ist fast identisch mit dem Tool **Protokollanzeige**. Die **Protokollanzeige** enthält die Features **Clientprotokollierung konfigurieren** und **Protokollgruppen**, die in diesem Abschnitt beschrieben werden, jedoch nicht. Im Abschnitt [Referenz zur Protokollanzeige des Supportcenters](#bkmk_log-viewer) werden die anderen Optionen erläutert, die auf dieser Registerkarte verfügbar sind.

#### <a name="configure-client-logging"></a>Clientprotokollierung konfigurieren

Legen Sie die folgenden Optionen fest: 
- **Client log level** (Clientprotokollebene): Ausführlichkeitsgrad und Dateigröße von Protokollen  
- **Maximum file count** (Maximale Dateianzahl): Lässt mehr als eine Protokolldatei eines bestimmten Typs zu  
- **Maximale Dateigröße:** die Größe einer bestimmten Protokolldatei in Byte (festzulegen, bevor der Client ein neues Protokoll erstellt)  

> [!NOTE]  
> Wenn Sie diese Werte zu niedrig festlegen, protokolliert der Client wichtige Informationen möglicherweise nicht. Wenn Sie diese Werte zu hoch festlegen, verbrauchen die Clientprotokolle möglicherweise sehr viel Speicherplatz.  

#### <a name="log-groups"></a>Protokollgruppen

Anstatt Protokolldateien manuell mit der Schaltfläche **Protokolle öffnen** auszuwählen, können Sie diese Dropdownliste verwenden, um alle Protokolldateien zu öffnen, die folgenden Bereichen zugeordnet sind: 
- **Verwaltung gewünschter Konfigurationen**
- **Inventur**
- **Softwareverteilung**
- **Softwareupdates**
- **Anwendungsverwaltung:**
- **Richtlinie**
- **Clientregistrierung**
- **Betriebssystembereitstellung**


## <a name="support-center-log-viewer-reference"></a><a name="bkmk_log-viewer"></a> Referenz zur Protokollanzeige des Supportcenters

In diesem Abschnitt wird die Benutzeroberfläche der **Protokollanzeige des Supportcenters** beschrieben. 

- [Menü „Fenster“](#bkmk_log-window)  
- [Registerkarte „Startseite“](#bkmk_log-home)  

Die **Protokollanzeige** ist mit der Registerkarte **Protokolle** des **Supportcenters** fast identisch. Die **Protokollanzeige** enthält die Optionen **Clientprotokollierung konfigurieren** und **Protokollgruppen** jedoch nicht.


### <a name="window-menu"></a><a name="bkmk_log-window"></a> Menü „Fenster“

Klicken Sie in der oberen linken Ecke der Protokollanzeige des Supportcenters auf den Pfeil im blauen Kästchen, um dieses Menü zu öffnen.

#### <a name="open-logs"></a>Protokolle öffnen
Navigieren Sie zum Speicherort der Protokolldateien, um diese zu öffnen. 

#### <a name="options"></a>Optionen
Im Dialogfeld **Optionen** können Sie folgende Einstellungen vornehmen:
- Sie können die Bewegung der animierten Benutzeroberflächenelemente reduzieren.  
- Legen Sie die Protokollanzeige als Standard-App für Protokolldateien mit den Erweiterungen LOG und LO_ fest.  
- Sie können Warnungen zurücksetzen. Alle Warnmeldungen, die Sie zuvor unterdrückt haben, werden erneut angezeigt, wenn sie ausgelöst werden.  

#### <a name="about"></a>Informationen zu
Zeigt Informationen zur Protokollanzeige des Supportcenters an

#### <a name="close"></a>Schließen
Schließt die Protokollanzeige des Supportcenters


### <a name="home-tab"></a><a name="bkmk_log-home"></a> Registerkarte „Startseite“

#### <a name="open-logs"></a>Protokolle öffnen 
Das Supportcenter fordert Sie dazu auf, mindestens eine zu öffnende Protokolldatei auszuwählen.

Klicken Sie auf die Dropdownliste unter der Schaltfläche **Protokolle öffnen** im Menüband, und wählen Sie eine der folgenden zusätzlichen Optionen aus: 
- **Open logs in current view** (Protokolle in der aktuellen Ansicht öffnen): Öffnet die ausgewählten Protokolldateien in der aktuellen Ansicht  
- **Open logs in new window** (Protokolle in neuem Fenster öffnen): Öffnet die ausgewählten Dateien in einem neuen Fenster der **Protokollanzeige**  

#### <a name="close-and-clear-logs"></a>Protokolle schließen und löschen
Schließt alle geöffneten Protokolldateien. Löscht zudem alle angezeigten Protokolldateieinträge aus dem Fenster. Das Supportcenter zeigt diese Einträge in Zukunft nicht mehr an.

Klicken Sie auf die Dropdownliste unter der Schaltfläche **Protokolle schließen und löschen** im Menüband, und wählen Sie eine der folgenden zusätzlichen Optionen aus: 
- **Alle Einträge löschen:** Löscht alle angezeigten Protokolldateieinträge aus dem Fenster. Das Supportcenter zeigt diese Einträge in Zukunft nicht mehr an.  
- **Alle Protokolle schließen:** Schließt alle geöffneten Protokolldateien.  

#### <a name="find"></a>Finden
Öffnet das Dialogfeld **Suchen**. Geben Sie eine Zeichenfolge ein, nach der gesucht werden soll. Sie können ganze Wörter abgleichen, um zu vermeiden, dass Übereinstimmungen von kurzen Zeichenfolgen in anderen Zeichenfolgen auftreten. Sie können außerdem nach Übereinstimmungen mit der Groß-/Kleinschreibung der Zeichenfolge suchen.

#### <a name="find-next"></a>Weitersuchen
Nachdem eine Übereinstimmung mit der zu suchenden Zeichenfolge festgestellt wurde, gelangen Sie mit dieser Option zur nächsten Übereinstimmung.

#### <a name="find-previous"></a>Vorheriges suchen
Nachdem zwei oder mehr Übereinstimmungen mit der zu suchenden Zeichenfolge festgestellt wurde, gelangen Sie mit dieser Option zur vorherigen Übereinstimmung.

#### <a name="options"></a>Optionen

- **Live aktualisieren:** Mit dieser Option kann eine aktuell geöffnete Protokolldatei auf Änderungen überwacht werden. Dieses Feature kann nicht ausgewählt werden, wenn mehrere Protokolldateien geöffnet sind. Diese Option ist standardmäßig aktiviert.  

- **Auto-scroll** (Automatisches Scrollen): Wenn Sie ebenfalls die Option **Live aktualisieren** aktivieren, wird automatisch zu den neu hinzugefügten Einträgen in der Protokollanzeige gescrollt. Dieses Feature kann nicht ausgewählt werden, wenn mehrere Protokolldateien geöffnet sind. Diese Option ist standardmäßig aktiviert.  

- **Details anzeigen:** Wenn Sie eine Protokolldateimeldung auswählen, werden im unteren Bereich der Registerkarte **Protokolle** die Details der Protokolldateimeldung angezeigt. Diese Option ist standardmäßig aktiviert.  

- **Schnelles Filtern:** Filtert die Protokolldateimeldungen in allen geöffneten Protokolldateien, um eine bestimmte Zeichenfolge zu suchen. Sie können nach Protokolltext, Komponentenname und Thread-ID filtern. Klicken Sie mit der rechten Maustaste auf eine Protokollmeldung, und klicken Sie im Protokolltext auf **Schnelles Filtern**, um eine ähnliche Protokollmeldung zu suchen.  

- **Protokolltext umbrechen:** Führt einen Umbruch für lange und mehrzeilige Meldungen durch, damit diese in eine einzige Spalte passen. Dadurch sind die Meldungen einfacher lesbar. Diese Option ist standardmäßig aktiviert.  

- **Raw log entry display** (Anzeige des unformatierten Protokolleintrags): Zeigt nicht verarbeitete Protokollzeilen an.  

- **Erweiterte Filter:** Öffnet das Dialogfeld **Erweiterte Filter**. Weitere Informationen finden Sie unter [Erweiterte Protokolldateifilter](#bkmk_adv-filters).  

- **Error code links** (Links für Fehlercodes): Fehlercodes im Protokolltext werden hervorgehoben und klickbar. Diese Option ist standardmäßig aktiviert.  

#### <a name="error-lookup"></a>Fehlersuche
Geben Sie einen Fehlercode ein, um in den aktuell geöffneten Protokolldateien nach diesem zu suchen. Verwenden Sie die folgenden Fehlercodeformate:
- **Ganze 32-Bit-Zahl (mit Vorzeichen):** Beispiel: `-2147024891`  
- **Ganze 32-Bit-Zahl (ohne Vorzeichen):** Beispiel: `2147942405`  
- **32-Bit-Hexadezimalzahl:** Beispiel: `0x80070005`  

#### <a name="decode-certificate"></a>Zertifikat decodieren
Fügen Sie in das Dialogfeld **Zertifikat decodieren** den serialisierten Zertifikatwert für alle Zertifikate auf dem Client ein. Suchen Sie diesen Wert in der Registrierung, in Protokolldateien oder in der Windows-Verwaltungsinstrumentation. Klicken Sie auf **Prozess**, um die allgemeinen Informationen und Details für das Zertifikat anzuzeigen. Zu diesen Informationen zählt unter anderem der Zertifizierungspfad. Klicken Sie auf **Exportieren**, um das Zertifikat als **CER**-Datei zu exportieren.



## <a name="advanced-log-file-filters"></a><a name="bkmk_adv-filters"></a> Erweiterte Protokolldateifilter

Mithilfe von erweiterten Protokolldateifiltern können Sie bestimmte Zeichenfolgen einschließen, ausschließen oder hervorheben. Diese Zeichenfolgen können in einer Protokolldatei oder in einer Protokolldateigruppe auftreten, wenn Sie Protokolldateieinträge durchgehen. Verwenden Sie Platzhaltersuchen, wenn Sie einen Filter erstellen. Wenn Sie eine nützliche Filterkombination ermittelt haben, können Sie diese als *Filterset* speichern. 

Erweiterte Protokolldateifilter lösen Schnellfilter ab. Sie können beide zusammen verwenden, Schnellfilter werden jedoch nur auf die angezeigten Protokolldaten angewendet. Mithilfe von erweiterten Filtern wird bestimmt, welche Daten angezeigt werden, bevor Schnellfilter darauf angewendet werden.

Im Dialogfeld „Erweiterte Filter“ können Sie komplexe Filtersets erstellen. Diese Filtersets durchsuchen viele Protokolldateikomponenten nach Zeichenfolgen. Dazu zählen Meldungen, Threads, Protokollierungsebenen und Komponenten. Ein Filterset enthält mehrere Filteranweisungen, mit denen Protokolldateimeldungen eingeschlossen, ausgeschlossen oder hervorgehoben werden. Ein Filter definiert eine Spalte einer Protokolldatei, die durchsucht werden soll, einen Operator und einen Wert. Der Wert kann reguläre Ausdrücke enthalten (z.B. das *Platzhalterzeichen*`*`).


### <a name="add-a-filter"></a>Hinzufügen eines Filters

1. Klicken Sie in der **Protokollanzeige** oder auf der Registerkarte **Protokolle** des Supportcenters auf **Erweiterte Filter**.  

2. Klicken Sie im Dialogfeld „Erweiterte Filter“ auf **Hinzufügen**. Wählen Sie dann eine der folgenden Optionen aus, die auf die Protokolleinträge angewendet werden sollen, die mit Ihrem Filter übereinstimmen:  
    - **Einschließen**  
    - **Ausschließen**  
    - **Hervorheben**  

3. Wählen Sie im Dialogfeld **Advanced filter configuration** (Erweiterte Filter konfigurieren) eine Spalte und einen Operator aus:  

    - **Spalte:** Wählen Sie den Ort aus, der nach mit Ihrem Filter übereinstimmenden Zeichenfolgen durchsucht werden soll:  

         - **Protokolltext:** Suche innerhalb des Protokolldateitexts  

         - **Protokollschweregrad:** Suche nach Protokollen mit einem bestimmten Schweregrad. Legen Sie die Schweregrade im Feld **Wert** fest.  

         - **Komponente:** Suche nach einer bestimmten Komponente anhand des Namens  

         - **Thread-ID:** Suche nach Protokollmeldungen mit einer bestimmten Thread-ID  

         - **Quelldatei:** Suche nach Protokollmeldungen, die in einer bestimmten Protokolldatei auftreten  

    - **Operator:** Wählt einen Operator für den Filter aus  

4. Geben Sie im Feld **Wert** einen Wert ein, nach dem gefiltert werden soll. Wenn Ihr Wert reguläre Ausdrücke enthält, aktivieren Sie **Enable regular expression matching** (Suche mit regulären Ausdrücken aktivieren).  


### <a name="manage-filter-sets"></a>Verwalten von Filtersets

- Wählen Sie einen Filter aus, und klicken Sie auf **Bearbeiten**, um einen Filter zu bearbeiten.  

- Wählen Sie einen Filter aus, und klicken Sie auf **Löschen**, um einen Filter zu löschen.  

- Klicken Sie auf **Alle Filter löschen**, um alle Filter zu löschen.  

- Klicken Sie auf **Filter speichern**, um das aktuelle Filterset zu speichern. Speichern Sie Ihr Filterset als **FILTERSET**-Datei.  

- Klicken Sie auf **Filter laden**, um ein gespeichertes Filterset zu laden. Navigieren Sie anschließend zu einer zuvor gespeicherten **FILTERSET**-Datei.  



## <a name="support-center-viewer-reference"></a><a name="bkmk_viewer"></a> Referenz zur Supportcenteranzeige

In diesem Abschnitt wird die Benutzeroberfläche für das Tool **Supportcenteranzeige** von Configuration Manager beschrieben. Die verfügbaren Registerkarten hängen vom Inhalt des Pakets zur Problembehandlung ab. Das [Menü „Fenster“](#bkmk_viewer-window) und die [Registerkarte „Startseite“](#bkmk_viewer-home) werden standardmäßig angezeigt.
- [Menü „Fenster“](#bkmk_viewer-window)
- [Registerkarte „Startseite“](#bkmk_viewer-home)
- [Registerkarte „Konfiguration“](#bkmk_viewer-config)
- [Registerkarte „Protokolle“](#bkmk_viewer-logs)
- [Registerkarte „Debugdumps“](#bkmk_viewer-debug)
- [Registerkarte „WMI“](#bkmk_viewer-wmi)
- [Registerkarte „Registrierung“](#bkmk_viewer-registry)
- [Registerkarte „Richtlinie“](#bkmk_viewer-policy)
- [Registerkarte „Zertifikate“](#bkmk_viewer-certs)
- [Registerkarte „Problembehandlung“](#bkmk_viewer-troubleshoot)


### <a name="window-menu"></a><a name="bkmk_viewer-window"></a> Menü „Fenster“

Klicken Sie in der oberen linken Ecke der Supportcenteranzeige auf den Pfeil im blauen Kästchen, um dieses Menü zu öffnen.

#### <a name="open-bundle"></a>Paket öffnen
Navigiert zum Speicherort eines Datenpakets, das vom Supportcenter erstellt wurde.

#### <a name="about"></a>Informationen zu
Zeigt Informationen zur Supportcenteranzeige an.

#### <a name="options"></a>Optionen
Im Dialogfeld **Optionen** können Sie folgende Einstellungen vornehmen:
- Sie können die Bewegung der animierten Benutzeroberflächenelemente reduzieren.  
- Sie können den Speicherort für temporäre Dateien ändern.    
- Sie können Warnungen zurücksetzen. Alle Warnmeldungen, die Sie zuvor unterdrückt haben, werden erneut angezeigt, wenn sie ausgelöst werden.  
- Sie können den Pfad für temporäre Dateien auf die Standardeinstellung (`%UserProfile%\AppData\Local\Microsoft\ConfigMgrSupportCenterViewer`) zurücksetzen.  


#### <a name="exit"></a>Beenden
Beendet die Supportcenteranzeige


### <a name="home-tab"></a><a name="bkmk_viewer-home"></a> Registerkarte „Startseite“

#### <a name="open-bundle"></a>Paket öffnen
Navigiert zum Speicherort eines Datenpakets, das vom Supportcenter erstellt wurde.

#### <a name="open-log-file"></a>Protokolldatei öffnen
Wählen Sie eine oder mehrere Protokolldateien aus, die geöffnet werden sollen.

#### <a name="decode-certificate"></a>Zertifikat decodieren
Fügen Sie in das Dialogfeld **Zertifikat decodieren** den serialisierten Zertifikatwert für alle Zertifikate auf dem Client ein. Suchen Sie diesen Wert in der Registrierung, in Protokolldateien oder in der Windows-Verwaltungsinstrumentation. Klicken Sie auf **Prozess**, um die allgemeinen Informationen und Details für das Zertifikat anzuzeigen. Zu diesen Informationen zählt unter anderem der Zertifizierungspfad. Klicken Sie auf **Exportieren**, um das Zertifikat als **CER**-Datei zu exportieren.


### <a name="configuration-tab"></a><a name="bkmk_viewer-config"></a> Registerkarte „Konfiguration“

Die Registerkarte **Konfiguration** des Supportcenteranzeigetools enthält die folgenden Ansichten, die unter Verwendung von Daten von WMI-Anbietern abgerufen werden:

#### <a name="client"></a>Client
Diese Ansicht zeigt die gleichen Informationen an, die auf der Registerkarte **Client** im Supportcenter angezeigt werden.

#### <a name="operating-system"></a>Betriebssystem
Details zum Betriebssystem des Clients. Hierfür wird die Klasse [Win32_OperatingSystem](/windows/desktop/CIMWin32Prov/win32-operatingsystem) verwendet.

#### <a name="computer"></a>Computer
Details zum Clientcomputer. Hierfür wird die Klasse [Win32_OperatingSystem](/windows/desktop/CIMWin32Prov/win32-operatingsystem) verwendet.

#### <a name="services"></a>Dienste
Details zu den Diensten, die auf dem Clientcomputer ausgeführt werden. Hierfür wird die Klasse [Win32_Service](/windows/desktop/CIMWin32Prov/win32-service) verwendet.

#### <a name="network-adapters"></a>Netzwerkadapter
Details zu den Netzwerkadaptern, die auf dem Clientcomputer installiert sind. Hierfür wird die Klasse [Win32_NetworkAdapterConfiguration](/windows/desktop/CIMWin32Prov/win32-networkadapterconfiguration) verwendet.


### <a name="logs-tab"></a><a name="bkmk_viewer-logs"></a> Registerkarte „Protokolle“

Auf der Registerkarte **Protokolle** wird eine Liste der im Paket enthaltenen Protokolldateien angezeigt. Jede Zeile auf dieser Registerkarte enthält den Pfad, den Namen und die Größe der Protokolldatei. 

#### <a name="open"></a>Öffnen
Nachdem Sie eine Protokolldatei ausgewählt haben, können Sie auf diese Schaltfläche klicken, um die **Protokollanzeige** zu öffnen. Diese bietet eine Teilmenge der Funktionen, die auf der Registerkarte „Protokolle“ des Supportcenters verfügbar sind.

#### <a name="decode-certificate"></a>Zertifikat decodieren
Fügen Sie in das Dialogfeld **Zertifikat decodieren** den serialisierten Zertifikatwert für alle Zertifikate auf dem Client ein. Suchen Sie diesen Wert in der Registrierung, in Protokolldateien oder in der Windows-Verwaltungsinstrumentation. Klicken Sie auf **Prozess**, um die allgemeinen Informationen und Details für das Zertifikat anzuzeigen. Zu diesen Informationen zählt unter anderem der Zertifizierungspfad. Klicken Sie auf **Exportieren**, um das Zertifikat als **CER**-Datei zu exportieren.


### <a name="debug-dumps-tab"></a><a name="bkmk_viewer-debug"></a> Registerkarte „Debugdumps“

Jede Zeile auf dieser Registerkarte enthält detaillierte Informationen zu den zu exportierenden Debugdumpdateien. Verwenden Sie diese Registerkarte, um Debugdumpdateien (DMP-Dateien) zur weiteren Analyse zu exportieren. Diese Analyse verwendet ein Tool zum Debuggen (z.B. WinDbg). 

> [!WARNING]  
> Debugdumps enthalten möglicherweise vertrauliche Informationen, z.B. Kennwörter, kryptografische Schlüssel oder Benutzerdaten. Sammeln Sie Debugdumps nur auf Empfehlung eines Mitarbeiters des Microsoft-Supports. Datenpakete, die Debugdumps enthalten, sollten sorgfältig verwaltet werden, um diese vor nicht autorisiertem Zugriff zu schützen.  

#### <a name="export"></a>Exportieren
Speichert eine Kopie der ausgewählten Debugdumpdatei.


### <a name="wmi-tab"></a><a name="bkmk_viewer-wmi"></a> Registerkarte „WMI“

Diese Registerkarte enthält ein WMI-Dataset aus dem Konfigurations-Manager-Client, der im Datenpaket enthalten ist. 

#### <a name="find"></a>Finden
Öffnet das Dialogfeld „Suchen“ mit den folgenden Features:  

- **Suchen:** Geben Sie eine Zeichenfolge ein, nach der im WMI-Dataset gesucht werden soll. Platzhalterzeichen werden unterstützt.  

- **Suchoptionen**: Geben Sie an, ob Sie im WMI-Dataset nach **Klasse- oder Instanzname**, **Eigenschaft** oder **Wert** suchen möchten.  

- **Nur ganze Zeichenfolge suchen:** Standardmäßig wird im Dialogfeld „Suchen“ nach Zeichenfolgen gesucht, die die gesuchte Zeichenfolge enthalten. Aktivieren Sie dieses Kontrollkästchen, um nur nach Zeichenfolgen zu suchen, die exakt mit der angegebenen Zeichenfolge übereinstimmen.  

#### <a name="find-next"></a>Weitersuchen
Mit dieser Schaltfläche wird die nächste Instanz der Zeichenfolge geöffnet, die Sie im Dialogfeld „Suchen“ im WMI-Dataset angegeben haben.

#### <a name="decode-certificate"></a>Zertifikat decodieren
Fügen Sie in das Dialogfeld **Zertifikat decodieren** den serialisierten Zertifikatwert für alle Zertifikate auf dem Client ein. Suchen Sie diesen Wert in der Registrierung, in Protokolldateien oder in der Windows-Verwaltungsinstrumentation. Klicken Sie auf **Prozess**, um die allgemeinen Informationen und Details für das Zertifikat anzuzeigen. Zu diesen Informationen zählt unter anderem der Zertifizierungspfad. Klicken Sie auf **Exportieren**, um das Zertifikat als **CER**-Datei zu exportieren.


### <a name="registry-tab"></a><a name="bkmk_viewer-registry"></a> Registerkarte „Registrierung“

Verwenden Sie die Registerkarte **Registrierung**, um die im Datenpaket enthaltenen Registrierungsdaten anzuzeigen und für die weitere Analyse zu exportieren.

#### <a name="export"></a>Exportieren
Speichert eine Kopie des Registrierungsschlüssels und der Unterschlüssel, die Sie als Registrierungsdatei (REG-Datei) ausgewählt haben.

#### <a name="find"></a>Finden
Öffnet das Dialogfeld „Suchen“ mit den folgenden Features:  

- **Suchen:** Geben Sie eine Zeichenfolge ein, nach der im WMI-Dataset gesucht werden soll. Platzhalterzeichen werden unterstützt.  

- **Suchoptionen**: Geben Sie an, ob Sie im WMI-Dataset nach **Klasse- oder Instanzname**, **Eigenschaft** oder **Wert** suchen möchten.  

- **Nur ganze Zeichenfolge suchen:** Standardmäßig wird im Dialogfeld „Suchen“ nach Zeichenfolgen gesucht, die die gesuchte Zeichenfolge enthalten. Aktivieren Sie dieses Kontrollkästchen, um nur nach Zeichenfolgen zu suchen, die exakt mit der angegebenen Zeichenfolge übereinstimmen.  

#### <a name="find-next"></a>Weitersuchen
Mit dieser Schaltfläche wird die nächste Instanz der Zeichenfolge geöffnet, die Sie im Dialogfeld „Suchen“ im WMI-Dataset angegeben haben.

#### <a name="decode-certificate"></a>Zertifikat decodieren
Fügen Sie in das Dialogfeld **Zertifikat decodieren** den serialisierten Zertifikatwert für alle Zertifikate auf dem Client ein. Suchen Sie diesen Wert in der Registrierung, in Protokolldateien oder in der Windows-Verwaltungsinstrumentation. Klicken Sie auf **Prozess**, um die allgemeinen Informationen und Details für das Zertifikat anzuzeigen. Zu diesen Informationen zählt unter anderem der Zertifizierungspfad. Klicken Sie auf **Exportieren**, um das Zertifikat als **CER**-Datei zu exportieren.


### <a name="policy-tab"></a><a name="bkmk_viewer-policy"></a> Registerkarte „Richtlinie“

Mithilfe der Registerkarte **Richtlinie** werden die im Datenpaket enthaltenen Richtliniendaten angezeigt. 

#### <a name="find"></a>Finden
Öffnet das Dialogfeld „Suchen“ mit den folgenden Features:  

- **Suchen:** Geben Sie eine Zeichenfolge ein, nach der im WMI-Dataset gesucht werden soll. Platzhalterzeichen werden unterstützt.  

- **Suchoptionen**: Geben Sie an, ob Sie im WMI-Dataset nach **Klasse- oder Instanzname**, **Eigenschaft** oder **Wert** suchen möchten.  

- **Nur ganze Zeichenfolge suchen:** Standardmäßig wird im Dialogfeld „Suchen“ nach Zeichenfolgen gesucht, die die gesuchte Zeichenfolge enthalten. Aktivieren Sie dieses Kontrollkästchen, um nur nach Zeichenfolgen zu suchen, die exakt mit der angegebenen Zeichenfolge übereinstimmen.  

#### <a name="find-next"></a>Weitersuchen
Mit dieser Schaltfläche wird die nächste Instanz der Zeichenfolge geöffnet, die Sie im Dialogfeld „Suchen“ im WMI-Dataset angegeben haben.

#### <a name="decode-certificate"></a>Zertifikat decodieren
Fügen Sie in das Dialogfeld **Zertifikat decodieren** den serialisierten Zertifikatwert für alle Zertifikate auf dem Client ein. Suchen Sie diesen Wert in der Registrierung, in Protokolldateien oder in der Windows-Verwaltungsinstrumentation. Klicken Sie auf **Prozess**, um die allgemeinen Informationen und Details für das Zertifikat anzuzeigen. Zu diesen Informationen zählt unter anderem der Zertifizierungspfad. Klicken Sie auf **Exportieren**, um das Zertifikat als **CER**-Datei zu exportieren.


### <a name="certificates-tab"></a><a name="bkmk_viewer-certs"></a> Registerkarte „Zertifikate“

Mit der Registerkarte **Zertifikate** werden die im Datenpaket enthaltenen Zertifikate angezeigt und exportiert.

#### <a name="view-certificate"></a>Zertifikat anzeigen
Zeigt Informationen über ein ausgewähltes Zertifikat an.

#### <a name="export"></a>Exportieren
Öffnet das Dialogfeld **Speichern unter**, um eine Kopie des ausgewählten Zertifikats zu speichern.


### <a name="troubleshooting-tab"></a><a name="bkmk_viewer-troubleshoot"></a> Registerkarte „Problembehandlung“

Verwenden Sie die Registerkarte **Problembehandlung**, um Protokolldateien anzuzeigen, die mithilfe der Registerkarte „Problembehandlung“ des Supportcenters erstellt wurden.

#### <a name="view-log"></a>Protokoll anzeigen
Nachdem Sie eine Zeile auf der Registerkarte **Problembehandlung** ausgewählt haben, können Sie diese Option auswählen, um die Protokolldatei mit der Protokollanzeige anzuzeigen.