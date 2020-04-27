---
title: Technical Preview 1804
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über neue Features, die mit der Technical Preview-Version 1804 für System Center Configuration Manager zur Verfügung stehen.
ms.date: 05/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8af43618-ec60-4c3e-a007-12399d1335b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: b30386745244900e7f525f8f45b25a598628bf43
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078735"
---
# <a name="capabilities-in-technical-preview-1804-for-configuration-manager"></a>Funktionen in der Technical Preview 1804 für Configuration Manager

*Gilt für: Configuration Manager (Technical Preview-Branch)*

In diesem Artikel werden die Features vorgestellt, die in der Technical Preview-Version 1804 für System Center Configuration Manager verfügbar sind. Sie können diese Version installieren, um Funktionen für Ihren Technical Preview-Standort zu aktualisieren oder neue Funktionen hinzuzufügen. 

Lesen Sie den [Technical Preview](technical-preview.md)-Artikel vor der Installation dieses Updates. In diesem Artikel erhalten Sie Informationen zu den allgemeinen Anforderungen und Einschränkungen, die für die Verwendung der Technical Preview gelten. Außerdem erfahren Sie, wie Sie Updates zwischen den Versionen ausführen und Feedback übermitteln.     


<!--  Known Issues Template   -->
## <a name="known-issues-in-this-technical-preview"></a>Bekannte Probleme in dieser Technical Preview

### <a name="setup-link-to-download-updates-not-working"></a><a name="bkmk_ki-prereqs"></a> Link beim Setup zum Herunterladen von Updates funktioniert nicht
<!--514334-->
Wenn Sie das Setup über Medien ausführen, enthält die Startseite einen Link mit dem Titel **Get the latest Configuration Manager updates (Aktuelle Configuration Manager-Updates abrufen)** , der in dieser Version nicht funktioniert. Dieser Link ist für den Download der erforderlichen Dateien für das Setup vorgesehen.

#### <a name="workaround"></a>Problemumgehung
Um die erforderlichen Dateien für das Setup herunterzuladen, führen Sie den Setup-Assistenten aus. Verwenden Sie auf der Seite „Download der Voraussetzungskomponenten“ die Option **Erforderliche Dateien herunterladen**. 


### <a name="the-application-catalog-web-service-point-cant-be-https-enabled"></a><a name="bkmk_appcathttps"></a> Der Anwendungskatalog-Webdienstpunkt ist nicht HTTPS-fähig
<!--512637-->
Wenn der Anwendungskatalog-Webdienstpunkt HTTPS-fähig ist, tritt Folgendes auf:

- Anwendungen, die für Benutzer als verfügbar bereitgestellt werden, werden im Softwarecenter nicht angezeigt.  

- In „awebsctl.log“ wird der folgende Fehler angezeigt:  

     `Call to HttpSendRequestSync failed for port 443 with status code 500, text: Internal Server Error`

#### <a name="workaround"></a>Problemumgehung
Konfigurieren Sie den Anwendungskatalog-Webdienstpunkt so neu, dass er über HTTP-Verbindungen kommuniziert.  




</br>

**Im Folgenden werden neue Features aufgelistet, die Sie mit dieser Version ausprobieren können.**  


## <a name="configure-a-remote-content-library-for-the-site-server"></a>Konfigurieren einer remoten Inhaltsbibliothek für den Standortserver  
<!--1357525-->
Verschieben Sie die [Inhaltsbibliothek](../plan-design/hierarchy/the-content-library.md) Ihres primären Standortservers an einen anderen Festplattenspeicherplatz, um Speicherplatz freizugeben. Sie können die Inhaltsbibliothek auf ein anderes Laufwerk auf dem Standortserver, einen separaten Server oder ein fehlertolerantes Laufwerk in einem Storage Area Network (SAN) verschieben. Ein SAN ist empfehlenswert, da dessen flexibler Speicher mit der Zeit größer oder kleiner wird, um Ihre aktuellen Anforderungen zu erfüllen. 

Diese Remoteinhaltsbibliothek ist eine neue Voraussetzung für die [Hochverfügbarkeit der Standortserverrolle](capabilities-in-technical-preview-1706.md#site-server-role-high-availability). 

> [!Note]  
> Diese Aktion verschiebt nur die Inhaltsbibliothek auf den Standortserver. Sie hat keinerlei Auswirkung auf die Position der Inhaltsbibliothek auf Verteilungspunkten. 

### <a name="prerequisites"></a>Voraussetzungen  
- Das Computerkonto des Standortservers muss über **Lese-** und **Schreibberechtigungen** für den Netzwerkpfad verfügen, auf den Sie die Inhaltsbibliothek verschieben. Auf dem Remotesystem werden keine Komponenten installiert. 

### <a name="try-it-out"></a>Probieren Sie es aus!
 Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie uns anschließend Ihr [Feedback](#bkmk_feedback), und lassen Sie uns wissen, wie es gelaufen ist.

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**. Erweitern Sie **Standortkonfiguration**, und wählen Sie **Standorte** aus. Auf der Registerkarte **Zusammenfassung** am Ende des Detailbereichs erscheint eine neue Spalte für die **Inhaltsbibliothek**.  

2. Klicken Sie auf dem Menüband auf **Inhaltsbibliothek verwalten**.  

3. Wählen Sie **On a network share** (Auf einer Netzwerkfreigabe) aus, und geben Sie einen gültigen Netzwerkpfad ein. Dieser Pfad ist der Speicherort, auf den die Inhaltsbibliothek verschoben wird. Klicken Sie auf **OK**.  

4. Beachten Sie die Eigenschaft **Status** in der Spalte „Content Library“ (Inhaltsbibliothek) im Detailbereich. Sie zeigt den aktuellen Fortschritt des Standorts beim Verschieben der Inhaltsbibliothek an. Während des Verschiebens zeigt sie den abgeschlossenen Prozentsatz an. Wenn ein Fehler auftritt, zeigt sie den Fehler an. Häufige Fehler sind `access denied` oder `disk full`. Nach dem vollständigen Verschieben zeigt sie `OK` an. In **distmgr.log** finden Sie weitere Einzelheiten. Weitere Informationen finden Sie unter [Protokolle für Standortserver und Standortsystemserver](../plan-design/hierarchy/log-files.md#BKMK_SiteSiteServerLog).  

Wenn Sie die Inhaltsbibliothek wieder zurück auf den Standortserver verschieben müssen, wiederholen Sie den hier beschriebenen Vorgang. Wählen Sie dieses Mal jedoch die Option **Local to the site server** (Lokal auf den Standortserver) aus.  

> [!Tip]  
> Verwenden Sie das Tool zum Übertragen der Inhaltsbibliothek (**Content Library Transfer**), um den Inhalt auf ein anderes Laufwerk auf dem Standortserver zu verschieben. Weitere Informationen finden Sie unter [Configuration Manager-Toolkit](#configuration-manager-toolkit).  



## <a name="submit-feedback-from-the-configuration-manager-console"></a><a name="bkmk_feedback"></a> Übermitteln von Feedback über die Configuration Manager-Konsole  
<!--1357542-->

Senden Sie ein Lächeln! Sie können dem Configuration Manager-Team jetzt direkt Ihre Erfahrungen mitteilen. Das Senden von Feedback über die Configuration Manager-Konsole ist ein Kinderspiel. Wir möchten Ihr gesamtes Feedback hören: Lob, Probleme und Vorschläge.  

### <a name="try-it-out"></a>Probieren Sie es aus!
 Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie uns anschließend Ihr **Feedback**, und lassen Sie uns wissen, wie es gelaufen ist.  

1. Klicken Sie in der Configuration Manager-Konsole auf die Schaltfläche „Lächeln“ in der oberen rechten Ecke des Menübands.  

2. Wählen Sie in der Dropdownliste eine der verfügbaren Optionen aus:  

   - **Lächeln senden**: Ihnen hat etwas sehr gut gefallen! Geben Sie bei dieser Option Einzelheiten zu Ihrem Feedback ein. Optional können Sie einen Screenshot und Ihre E-Mail-Adresse einfügen.  

   - **Stirnrunzeln senden**: Sie haben in der Konsole ein Problem festgestellt, oder etwas funktioniert nicht wie erwartet. Geben Sie bei dieser Option die Einzelheiten des potentiellen Produktproblems ein. Optional können Sie einen Screenshot, Ihre E-Mail-Adresse und Diagnosedaten einfügen.  

   - **Vorschlag senden**: Sie haben Ideen für Änderungen und Verbesserungen von Configuration Manager. Diese Option öffnet die Seite [UserVoice](https://configurationmanager.uservoice.com) in Ihrem Webbrowser.  

Dieses Feedback erreicht direkt das Microsoft-Produktteam für Configuration Manager. Obwohl der Feedback-Hub von Windows 10 weiterhin unterstützt wird, sollten Sie vom konsoleninternen Feedback-Mechanismus Gebrauch machen.  

Aus Kontextgründen werden die folgenden anonymen Informationen immer mit dem Feedback übermittelt:  

- Version und Sprache der Configuration Manager-Konsole  

- Standortversion von Configuration Manager  

- Support-ID, auch bekannt als Hierarchie-ID  

- Version des Betriebssystems und die Sprache des Systems, auf dem die Konsole ausgeführt wird  

- Der genaue Speicherort in der Konsole, von dem Sie auf „Lächeln“ geklickt haben  

Diese Daten stimmen mit der Sammlung der Diagnose- und Nutzungsdaten überein. Weitere Informationen finden Sie unter [Diagnose- und Nutzungsdaten](../plan-design/diagnostics/diagnostics-and-usage-data.md).

### <a name="known-issues"></a>Bekannte Probleme

Wenn Sie versuchen, Feedback von einem Gerät zu senden, das nicht auf das Internet zugreifen kann, wird die Anwendung möglicherweise unerwartet geschlossen. Stellen Sie sicher, dass das Gerät auf petrol.office.microsoft.com zugreifen kann, damit Sie Lächeln oder Stirnrunzeln senden können.



## <a name="support-center"></a>Supportcenter
<!--1357489-->

Verwenden Sie das Supportcenter zur Behebung von Clientproblemen, Anzeigen von Protokollen in Echtzeit oder zum Erfassen des Zustands eines Configuration Manager-Clientcomputers zur späteren Analyse. Das Supportcenter ist ein einziges Tool, das viele Problembehandlungstools für Administratoren konsolidiert. In Technical Preview steht eine Vorschau der neuesten Version des Supportcenters zur Verfügung. Diese enthält Fehlerbehebungen, Verbesserungen und eine Vorschau der neuen Protokollanzeige. Das Installationsprogramm für das Supportcenter finden Sie auf dem Standortserver im Ordner **cd.latest\SMSSETUP\Tools\SupportCenter**.

 > [!Tip]  
 > Ältere Dokumentationen zu vorhandenen Funktionen im Supportcenter stehen unter [TechNet](https://technet.microsoft.com/library/dn688621.aspx) zur Verfügung. Relevante Informationen werden derzeit zur docs.microsoft.com-Bibliothek migriert.  

### <a name="new-support-center-features"></a>Neue Features des Supportcenters  

- OneTrace, eine neue Protokollanzeige. Sie funktioniert ähnlich wie CMTrace und enthält Verbesserungen, z.B. eine Registerkartenansicht und andockbare Fenster.  

- Ein neues Feature zur Sammlung von Daten sammelt Diagnoseprotokolle von lokalen oder remoten Configuration Manager-Clients. Sie bietet eine Diagnose des Inventurcaches (ersetzt Client Spy), des Richtliniencaches (ersetzte Policy Spy) und des Clientcaches in Echtzeit.  



## <a name="configuration-manager-toolkit"></a>Configuration Manager-Toolkit
<!--1357145-->

Die Configuration Manager-Server- und Client-Tools sind jetzt in Technical Preview enthalten. Sie finden Sie im Ordner **cd.latest\SMSSETUP\Tools** auf dem Standortserver. Es ist keine weitere Installation erforderlich.

#### <a name="server-tools"></a>Servertools  

- **DP Job Manager** (Manager für Verteilungspunktaufträge): Beheben von Problemen bei Inhaltsverteilungsaufträgen zu Verteilungspunkten  

- **Collection Evaluation Viewer** (Sammlungsauswertungs-Viewer): Anzeigen von Details der Sammlungsauswertung  

- **Content Library Explorer** (Inhaltsbibliothek-Explorer): Anzeigen des Single Instance Store der Inhaltsbibliothek  

- **Content Library Transfer** (Inhaltsbibliotheksübertragung): Übertragen von Inhaltsbibliotheken zwischen Laufwerken  

- **Content Ownership Tool** (Tool für den Inhaltsbesitz): Ändern des Besitzes von verwaisten Paketen. Diese Pakete sind am Standort ohne besitzenden Standortserver vorhanden.  

- **Role-based Administration and Auditing Tool** (Tool für die rollenbasierte Verwaltung und Überwachung): Unterstützung für Administratoren bei der Überwachung der Rollenkonfiguration  

#### <a name="client-tools"></a>Clienttools

- **CMTrace**: Anzeigen von Protokollen  

- **Deployment Monitoring Tool** (Tool zur Überwachung der Bereitstellung): Problembehandlung bei Anwendungen, Updates und Basislinienbereitstellungen  

- **Policy Spy** (Richtlinien-Spion): Anzeigen von Richtlinienzuweisungen  

- **Power Viewer Tool** (Tool für die Energieanzeige): Anzeigen des Status der Energieverwaltungsfunktion  

- **Send Schedule Tool** (Tool zum Übermitteln von Zeitplänen): Auslösen von Zeitplänen und Auswertungen von DCM-Basislinien  

> [!Important]  
> [Supportcenter](#support-center) wird für die meisten Anwendungsfälle empfohlen, da es die gleichen oder verbesserten Funktionen der folgenden Tools enthält:  
> - Client Spy
> - CMTrace<sup>1</sup> 
> - Deployment Monitoring Tool
> - Policy Spy
> - Send Schedule Tool
> 
> <sup>1</sup> CMTrace ist nicht von .NET oder Windows Presentation Foundation (WPF) abhängig und wird deswegen noch in Windows PE-Startimages verwendet.

### <a name="known-issues"></a>Bekannte Probleme
Einige Client- und Servertools können unerwartet beim Start beendet werden. Dieses Problem beruht auf einer fehlenden Datei auf dem Medium. Als Problemumgehung können Sie die Datei **Microsoft.Diagnostics.Tracing.EventSource.dll** aus dem Verzeichnis „AdminConsole\bin“ jeweils in die Verzeichnisse „SMSSETUP\Tools\ClientTools“ und „ServerTools“ kopieren. Diese Datei muss die gleiche Version sein, die auch von der Configuration Manager-Konsole verwendet wird. Andere Versionen funktionieren möglicherweise nicht. <!--513977-->



## <a name="uninstall-application-on-approval-revocation"></a>Deinstallieren von Anwendungen bei Widerruf von Genehmigungen
<!--1357891-->

Dieses Verhalten hat sich geändert, wenn Sie die Genehmigung für eine Anwendung widerrufen. Wenn Sie die Anforderung der Anwendung ablehnen, deinstalliert der Client nun die Anwendung vom Gerät des Benutzers. 

### <a name="prerequisites"></a>Voraussetzungen
- Aktivieren Sie das Feature **Genehmigen von Anwendungsanforderungen für Benutzer pro Gerät**.

### <a name="try-it-out"></a>Probieren Sie es aus!
 Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie uns anschließend Ihr [Feedback](#bkmk_feedback), und lassen Sie uns wissen, wie es gelaufen ist.

1. Stellen Sie in der Configuration Manager-Konsole einem Benutzer eine Anwendung bereit, die eine Genehmigung erfordert. Aktivieren Sie auf der Registerkarte **Bereitstellungseinstellungen** der Bereitstellung die Option **An administrator must approve a request for this application on the device** (Ein Administrator muss eine Anforderung für diese Anwendung auf dem Gerät genehmigen).  

2. Der Benutzer fordert die Genehmigung zur Installation der Anwendung auf dem Configuration Manager-Client im Softwarecenter an.  

3. Genehmigen Sie in der Configuration Manager-Konsole die Anforderung dieses Benutzers, die Anwendung auf seinem Gerät zu installieren. Anforderungen zur Genehmigung von Anwendungen werden im Arbeitsbereich **Softwarebibliothek** unter **Anwendungsverwaltung** auf dem Knoten **Approval Requests** (Anforderungen von Genehmigungen) angezeigt.  

4. Der Benutzer installiert die Anwendung auf dem Client im Softwarecenter.  

5. Lehnen Sie in der Configuration Manager-Konsole die Anforderung dieses Benutzers ab, die Anwendung auf seinem Gerät zu installieren.  

### <a name="known-issues"></a>Bekannte Probleme
- Aktualisieren Sie die Benutzerrichtlinie, nachdem der Benutzer die Anwendung auf dem Client installiert hat. Wechseln Sie im Softwarecenter zur Registerkarte **Optionen**, erweitern Sie **Computerwartung**, und klicken Sie auf **Sync Policy** (Synchronisierungsrichtlinie).<!--480609-->  

- Der Anwendungskatalog-Webdienstpunkt muss HTTPS-fähig sein. Weitere Informationen finden Sie unter [Bekannte Probleme in dieser Technical Preview](#bkmk_appcathttps).<!--512637-->  



## <a name="exclude-active-directory-containers-from-discovery"></a>Ausschließen von Active Directory-Containern von der Ermittlung
<!--1358143-->
Um die Anzahl der ermittelten Objekte zu reduzieren, können Sie jetzt bestimmte Container aus der Active Directory-Systemermittlung ausschließen. Dieses Feature ist das Ergebnis Ihres [UserVoice-Feedbacks](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8414520-exclude-virtual-cluster-and-ou-from-discovery).

### <a name="try-it-out"></a>Probieren Sie es aus!
 Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie uns anschließend Ihr [Feedback](#bkmk_feedback), und lassen Sie uns wissen, wie es gelaufen ist.

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**. Erweitern Sie **Hierarchiekonfiguration**, und wählen Sie **Ermittlungsmethoden** aus. Wählen Sie **Active Directory-Systemermittlung** aus, und klicken Sie dann im Menüband auf **Eigenschaften**.  

2. Klicken Sie auf das Symbol „Neu“, um einen neuen Active Directory-Container anzugeben.   

3. Navigieren Sie im Dialogfeld „Active Directory Container“ zum **Pfad** im Bereich „Speicherort“, oder geben Sie diesen ein, um die Ermittlung zu starten.  

4. Aktivieren Sie im Bereich „Suchoptionen“ die Option **Untergeordnete Active Directory-Container rekursiv durchsuchen**. Klicken Sie anschließend auf **Hinzufügen**, um Untercontainer auszuwählen, die von dieser Ermittlung ausgeschlossen werden sollen.  

5. Wählen Sie im Dialogfeld „Neuer Container“ einen untergeordneten Container aus, der ausgeschlossen werden soll. Klicken Sie auf **OK**, um das Dialogfeld „Neuer Container“ zu schließen.  

6. Klicken Sie auf **OK**, um das Dialogfeld „Active Directory-Container“ zu schließen.  

7. Im Eigenschaftenfenster der Active Directory-Systemermittlung sehen Sie den Pfad des Active Directory-Containers, an dem die Ermittlung startet. Die Spalte **Recursive** (rekursiv) zeigt **Ja** an, und die neue Spalte **Has Exclusions** (Ausnahmen vorhanden) zeigt ebenfalls **Ja** an. Klicken Sie auf **OK**, um das Eigenschaftenfenster der Active Directory-Systemermittlung zu schließen.  



## <a name="specify-the-visibility-of-the-application-catalog-website-link-in-software-center"></a>Angeben der Sichtbarkeit des Links zur Anwendungskatalog-Website im Softwarecenter
<!--1358214-->

Sie können nun steuern, ob die Verknüpfung **Open the Application Catalog web site** (Website des Anwendungskatalogs öffnen) auf dem Knoten **Installationsstatus** des Softwarecenters erscheint.  

> [!Note]  
> Die Unterstützung für die Benutzeroberfläche der Anwendungskatalog-Website endet mit dem ersten Update, das nach dem 1. Juni 2018 veröffentlicht wird. Weitere Informationen finden Sie unter [Entfernte und veraltete Features](../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).  

### <a name="try-it-out"></a>Probieren Sie es aus!
 Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie uns anschließend Ihr [Feedback](#bkmk_feedback), und lassen Sie uns wissen, wie es gelaufen ist.

1. Erstellen Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** im Knoten **Clienteinstellungen** eine neue benutzerdefinierte Richtlinie für Clientgeräteeinstellungen.  

2. Wählen Sie die Gruppe **Softwarecenter** aus.  

3. Klicken Sie unter **Software Center settings** (Softwarecenter-Einstellungen) auf **Anpassen**.  

4. Aktivieren Sie die Option **Hide the Application Catalog web site link in Software Center** (Ausblenden der Verknüpfung zur Anwendungskatalog-Website im Softwarecenter).   

Weitere Informationen zu Clienteinstellungen finden Sie unter [Konfigurieren von Clienteinstellungen](../clients/deploy/configure-client-settings.md).




## <a name="filter-automatic-deployment-rules-by-software-update-architecture"></a>Filtern der automatischen Bereitstellungsregeln durch Softwareupdates für Architektur
 <!--1322266-->
Sie können jetzt automatische Bereitstellungsregeln filtern, um Architekturen auszuschließen, z.B. Itanium und ARM64.

### <a name="try-it-out"></a>Probieren Sie es aus!
Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie uns anschließend Ihr [Feedback](#bkmk_feedback), und lassen Sie uns wissen, wie es gelaufen ist.

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**. Erweitern Sie den Eintrag **Softwareupdates**, und klicken Sie auf **Automatische Bereitstellungsregeln**. Wählen Sie auf dem Menüband **Automatische Bereitstellungsregel erstellen** aus.  

2. Tragen Sie in den Registerkarten **Allgemein** und **Bereitstellungseinstellungen** die entsprechenden Einstellungen ein.  

3. Wählen Sie auf der Registerkarte **Softwareupdates** **Architektur** aus, und klicken Sie anschließend in den **Suchkriterien** auf **items to find** (zu suchende Elemente).  

4. Wählen Sie die Architekturen aus, die Sie in die automatische Bereitstellungsregel aufnehmen möchten.  

5. Klicken Sie auf **Weiter**, und fahren Sie mit der Erstellung der automatischen Bereitstellungsregel fort.  

> [!IMPORTANT]  
> Denken Sie daran, dass es 32-Bit (x86)-Anwendungen und Komponenten gibt, die auf 64-Bit (x64)-Systemen ausgeführt werden. Wenn Sie sich nicht sicher sind, ob Sie x86 nicht benötigen, aktivieren Sie es bei der Auswahl von x64 ebenfalls.  

### <a name="known-issues"></a>Bekannte Probleme
Nach dem Hinzufügen der Kriterien für die Architektur zeigt die Eigenschaftenseite der automatischen Bereitstellungsregel in den Suchkriterien **Titel** an. Die automatische Bereitstellungsregel funktioniert dennoch wie erwartet und wählt die richtigen Softwareupdates aus. Allerdings dürfen Sie zu diesem Zeitpunkt die Kriterien **Architektur** und **Titel** nicht zusammen verwenden. <!--512634,512632-->



## <a name="improvements-to-os-deployment"></a>Verbesserungen bei der Bereitstellung von Betriebssystemen
Teilweise basierend auf dem Feedback von Benutzern haben wir die folgenden Verbesserungen an der Betriebssystembereitstellung vorgenommen.  

- [Sensible Daten maskieren, die in Tasksequenzvariablen gespeichert sind](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed): Wählen Sie im Schritt [Tasksequenzvariable festlegen](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) die neue Option **Diesen Wert nicht anzeigen** aus. Dies ist beispielsweise bei der Angabe eines Kennworts der Fall.<!--1358330--> Wenn Sie diese Option aktivieren, tritt das folgende Verhalten auf:
  - Der Wert der Variable wird nicht in „smsts.log“ angezeigt.
  - Die Configuration Manager-Konsole und SMS-Anbieter behandeln diesen Wert genauso wie andere sensible Daten, z.B. Kennwörter.
  - Der Wert ist nicht enthalten, wenn Sie die Tasksequenz exportieren.
  - Wenn Sie diesen Schritt bearbeiten, kann der Tasksequenz-Editor diesen Wert nicht lesen. Geben Sie den gesamten Wert erneut ein, um Änderungen vorzunehmen.

  > [!Important]  
  > Variablen und deren Werte werden mit der Tasksequenz als XML gespeichert und in der Datenbank verborgen. Wenn der Client eine Tasksequenzrichtlinie vom Verwaltungspunkt anfordert, wird diese während der Übertragung und bei der Speicherung auf dem Client verschlüsselt. Alle Variablenwerte werden jedoch während der Laufzeit auf dem Client in der Tasksequenzumgebung im Arbeitsspeicher als Nur-Text behandelt. Wenn die Tasksequenz einen Schritt zum Ausgeben dieses Variablenwerts enthält, erfolgt diese Ausgabe als Nur-Text. Für dieses Verhalten muss der Administrator eindeutig festlegen, dass solch ein Schritt in die Tasksequenz aufgenommen werden soll. 


- [Programmnamen während des Schritts „Befehlszeile ausführen“ einer Tasksequenz maskieren](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed): Wenn Sie verhindern möchten, dass möglicherweise vertrauliche Daten angezeigt oder protokolliert werden, müssen Sie die Tasksequenzvariable **OSDDoNotLogCommand** auf `TRUE` festlegen. Diese Variable verbirgt den Programmnamen in „smsts.log“ während der Schritt [Befehlszeile ausführen](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) einer Tasksequenz ausgeführt wird. <!--1358493-->  



## <a name="improvements-to-the-configuration-manager-console"></a>Verbesserungen der Configuration Manager-Konsole
- Informationen zum primären Benutzer werden durch Anzeigen der Mitglieder einer Sammlung unter **Assets und Konformität** > **Gerätesammlungen** angezeigt.<!--510252-->  



## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen zur Installation oder dem Update der Technical Preview finden Sie unter [Technical Preview für Configuration Manager](technical-preview.md).    
