---
title: Policy Spy
titleSuffix: Configuration Manager
description: Verwenden von Policy Spy zum Anzeigen des Richtliniensystems auf Konfigurations-Manager-Clients und zur Fehlerbehebung.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1012ec24-27d9-4193-8236-918d283c7448
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6038a3332c63a58d1f3c423491b1aa17aa28b080
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707548"
---
# <a name="policy-spy"></a>Policy Spy

*Gilt für: Configuration Manager (Current Branch)*

Policy Spy ist eines der [Configuration Manager-Tools](tools.md). Mit diesem Tool wird das Richtliniensystem auf Konfigurations-Manager-Clients angezeigt und die Fehlerbehebung des Systems durchgeführt. Führen Sie **PolicySpy.exe** aus, um die Benutzeroberfläche zu öffnen. Weitere Informationen zur Befehlszeilensyntax finden Sie unter [Befehlszeilensyntax](#bkmk_policyspy-syntax).

> [!Important]  
> Führen Sie Policy Spy als Administrator aus. Wenn Sie Policy Spy **nicht als Administrator ausführen**, wird Ihnen in den Clientinformationen der folgende Fehler angezeigt:  
> `There is no client installed on this machine. Connection to client policy failed with error 80041003`


## <a name="command-line-syntax"></a><a name="bkmk_policyspy-syntax"></a> Befehlszeilensyntax

Policy Spy dient in erster Linie der Verwendung über die Benutzeroberfläche. Es bietet begrenzte Befehlszeilenoptionen zur Unterstützung der Automatisierung und Batchverarbeitung.

`PolicySpy.exe [/export <ExportFilename> [<computername>]]`

### <a name="option-export"></a>Option: `/export`
Diese Option exportiert automatisch die Richtlinie des lokalen Computers bzw. des Remotecomputers. `<ExportFilename>` ist der Name der Datei, in der das Tool die exportierte XML-Richtlinie speichert. Wenn Sie die Option `<computername>` angeben, exportiert Policy Spy die Richtlinie dieses Computers, nicht die Richtlinie des lokalen Computers.

> [!Note]  
> Diese Befehlszeilenoption bietet keine Möglichkeit zur Angabe von Anmeldeinformationen des Benutzers. Verwenden Sie den Befehl **runas**, um eine neue Eingabeaufforderung mit den erforderlichen Sicherheitsanmeldeinformationen zu öffnen, wenn Sie alternative Anmeldeinformationen für den Zugriff auf einen Remotecomputer verwenden möchten.  


## <a name="usage"></a>Verwendung

### <a name="tools-menu"></a>Menü „Extras“

Im Menü **Extras** sind die folgenden Aktionen verfügbar:  

- **Open Remote** (Remote öffnen): Stellt eine Verbindung mit der Richtlinie des Konfigurations-Manager-Clients auf einem Remotecomputer her. Über das Dialogfeld „Verbinden“ können Sie den Namen des Remotecomputers und optionale Anmeldeinformationen des Benutzers abrufen. Schlägt das Herstellen einer Verbindung fehl, werden im Bereich „Clientinformationen“ die Fehlerinformationen angezeigt. Schlägt das Herstellen einer Verbindung erneut fehl, versuchen Sie, durch die Option **Aktualisieren** im Menü **Bearbeiten** oder durch Drücken der Taste F5 eine Verbindung herzustellen.  

- **Datei öffnen**: Öffnet eine Datei für den Richtlinienexport (XML), die über die Option **Richtlinie exportieren** erstellt wurde. Das Tool zeigt die exportierte Richtlinie auf die gleiche Weise wie eine Live-Richtlinie an. Einige Features, die nur bei der Verbindung zu einem tatsächlichen Client Anwendung finden, werden deaktiviert.  

- **Request Machine Assignments** (Computerzuweisungen anfordern): Löst eine Anforderung für Zuweisungen von Computerrichtlinien auf dem Zielcomputer aus. Dieses Feature ist deaktiviert, wenn Sie eine exportierte Richtlinie anzeigen.  

- **Evaluate Machine Policy** (Computerrichtlinie auswerten): Löst die Auswertung einer Computerrichtlinie auf dem Zielcomputer aus. Dieses Feature ist deaktiviert, wenn Sie eine exportierte Richtlinie anzeigen.  

- **Request User Assignments** (Benutzerzuweisungen anfordern): Löst eine Anforderung für Zuweisungen von Benutzerrichtlinien für den derzeit angemeldeten Benutzer aus. Dieses Feature ist nur verfügbar, wenn Sie auf dem lokalen Computer eine Richtlinie anzeigen.  

- **Evaluate User Policy** (Benutzerrichtlinie auswerten): Löst die Auswertung einer Benutzerrichtlinie für den derzeit angemeldeten Benutzer aus. Dieses Feature ist nur verfügbar, wenn Sie auf dem lokalen Computer eine Richtlinie anzeigen.  

- **Reset Policy** (Richtlinie zurücksetzen): Entfernt alle Richtlinien, die nicht der Standardeinstellung entsprechen, und setzt die Richtliniencookies für den Standort zurück. Anschließend wird eine Anforderung für Zuweisungen von Computerrichtlinien ausgelöst. Dieses Feature ist deaktiviert, wenn Sie eine exportierte Richtlinie anzeigen.  

- **Richtlinie exportieren**: Exportiert die Richtlinie des Zielcomputers in eine XML-Datei. Zeigen Sie diese Datei auf einem beliebigen Computer mit Policy Spy an. Wählen Sie zum Öffnen der Exportdatei die Option **Datei öffnen** im Menü **Extras** aus. Dieses Feature ist deaktiviert, wenn Sie eine exportierte Richtlinie anzeigen.  


### <a name="edit-menu"></a>Menü „Bearbeiten“

Im Menü **Bearbeiten** sind die folgenden Aktionen verfügbar:  

- **Löschen** Löscht die Instanz, die im Bereich „Ergebnisse“ ausgewählt wurde. Diese Aktion wird nur für Richtlinieninstanzen unterstützt. Wenn Sie versuchen, etwas anderes als Richtlinieninstanzen zu löschen, zeigt das Tool eine Fehlermeldung an. Dieses Feature ist deaktiviert, wenn Sie eine exportierte Richtlinie anzeigen.  

- **Aktualisieren:** Aktualisiert alle Ergebnisse, um die neuesten Informationen anzuzeigen. Alle Strukturknoten, die vor der Aktualisierung erweitert werden, werden anschließend automatisch erweitert. Wenn Policy Spy keine Verbindung mit der Richtlinie des Zielcomputers herstellen konnte, wird erneut versucht, die Verbindung herzustellen. Dieses Feature ist deaktiviert, wenn Sie eine exportierte Richtlinie anzeigen.  

- **Ereignisse löschen**: Löscht alle Elemente von der Registerkarte „Ereignisse“.  



## <a name="results-pane"></a>Ergebnisbereich

Der Ergebnisbereich werden unterschiedliche Ansichten des Richtliniensystems auf dem Zielcomputer angezeigt. Sie können auf diese Ansichten zugreifen, indem Sie auf eine der folgenden vier Registerkarten klicken: 
- [Tatsächlich](#bkmk_policyspy-actual)
- [Angefordert](#bkmk_policyspy-requested)
- [Standard](#bkmk_policyspy-default)
- [Ereignisse](#bkmk_policyspy-events)


### <a name="actual"></a><a name="bkmk_policyspy-actual"></a> Tatsächlich

Auf dieser Registerkarte wird die aktuelle Richtlinie des Clients angezeigt. Die aktuelle Richtlinie bestimmt das Verhalten eines Clients und das Verhalten der zugehörigen Client-Agents, wie z.B. Softwareverteilung und -inventur. Auf der Registerkarte werden Ergebnisse in einem Baumstrukturformat mit einem Strukturknoten für den Namespace des Computers und die einzelnen benutzerspezifischen Namespaces angezeigt. Erweitern Sie einen Namespaceknoten, um eine Liste der Klassen anzuzeigen. Erweitern Sie eine Klasse, um eine Liste der zugehörigen Instanzen anzuzeigen. Die Liste der Klassen enthält nur die Klassen, die über Instanzen verfügen.


### <a name="requested"></a><a name="bkmk_policyspy-requested"></a> Angefordert

Auf dieser Registerkarte werden Richtlinienzuweisungen angezeigt, die der Client von dem zugehörigen zugewiesenen Standort abgerufen hat. Auf der Registerkarte werden Ergebnisse im Baumstrukturformat mit einem Strukturknoten für den Namespace des Computers und die einzelnen benutzerspezifischen Namespaces angezeigt. Durch die Erweiterung eines Namespaceknotens werden folgende Knoten angezeigt:  

- **Konfiguration** Zeigt eine Liste der Konfigurationsklassen an, die über CCM_Policy_Config abgerufen wurden (einschließlich Richtlinienobjekt, Zuweisungen und andere).  

- **Einstellungen**: Zeigt alle aktiven Einstellungen an, die von Richtlinien generiert wurden. Der Knoten „Einstellungen“ wird unter dem Knoten „Konfiguration“ angezeigt. 

> [!Note]   
> Mehrere Instanzen können den gleichen Namen haben, da der Client diese Einstellungen nicht in ein einen endgültigen Ergebnissatz zusammengeführt hat. Policy Spy zeigt Instanzen unter diesem Knoten an, indem die RealKey-Eigenschaften und nicht die richtigen Richtlinienschlüssel verwendet werden. Gleichen Sie diese Instanzen an den Ergebnissatz an, der auf der Registerkarte „Tatsächlich“ angezeigt wird.  


### <a name="default"></a><a name="bkmk_policyspy-default"></a> Standard

Auf dieser Registerkarte werden die gleichen Informationen wie auf der Registerkarte **Angefordert** angezeigt. Sie weist zudem Inhalte der Namespaces „DefaultMachine“ und „DefaultUser“ auf.


### <a name="events"></a><a name="bkmk_policyspy-events"></a> Ereignisse

Auf dieser Registerkarte werden Ereignisse des Richtlinien-Agents angezeigt. Die Ansicht erstellt ein WMI-Ereignisabonnement für alle Ereignisse, die von CCM_PolicyAgent_Event abgeleitet wurden. In der Ansicht werden maximal 200 Ereignisse angezeigt. Die ältesten Ereignisse werden nach Bedarf aus dem Anfang der Liste entfernt. Wenn Sie das letzte Element in der Liste auswählen, wird automatisch nach unten gescrollt, wenn neue Ereignisse hinzugefügt werden. Andernfalls bleibt die aktuelle Position der Ansicht unverändert, und Sie müssen nach unten scrollen oder die ENDE-Taste drücken, um neue Ereignisse anzuzeigen. Wenn eine exportierte Richtlinie angezeigt wird, ist diese Ansicht immer leer.



## <a name="client-info-pane"></a>Bereich „Clientinformationen“
Im Bereich „Clientinformationen“ wird eine Liste mit Eigenschaften des Zielcomputers angezeigt. Sofern verfügbar, werden folgende Eigenschaften angezeigt:  
- Name
- ID
- Version
- Standort
- Zugewiesener Verwaltungspunkt
- Residenter Verwaltungspunkt
- Proxyverwaltungspunkt
- Proxyzustand



## <a name="details-pane"></a>Detailbereich
Im Bereich „Details“ werden detaillierte Informationen zur aktuellen Auswahl angezeigt. Wenn keine Auswahl aktiv ist, werden Informationen zu Policy Spy, einschließlich der Version, angezeigt. Andernfalls wird eine MOF-Darstellung (Managed Object Format) des ausgewählten Elements angezeigt.

Policy Spy verwendet eine eigene Routine zur MOF-Generierung, damit eine HTML-Anzeige erzeugt wird, die benutzerfreundlicher ist als das von WMI generierte, aus reinem Text bestehende MOF. Durch dieses Verhalten kann Policy Spy folgende Features hinzufügen, durch die das MOF besser lesbar ist:  

- Syntaxhervorhebung  

- Eingezogene Objekte und Arrays  

- Eigenschaften werden in Systemgruppen, geerbten und lokalen Gruppen angeordnet. Die Systemgruppen und geerbten Gruppen werden standardmäßig ausgeblendet. Sie können direkt sehen, welche Eigenschaften aktuell von der Instanz verwendet werden.  

- Kopieren Sie die MOF-Datei bzw. die aus reinem Text bestehende MOF-Datei in die Zwischenablage. Mithilfe dieses Features kann die MOF-Datei durch direktes Aufrufen des MofComp-Tools in andere Anwendungen eingefügt werden.  

Bei Instanzen von Richtlinienobjekten, die von CCM_Policy_Policy abgeleitet wurden, wird der Richtlinientext im Detailbereich unterhalb der angezeigten MOF-Datei dargestellt. Wenn der Client den Richtlinientext nicht heruntergeladen hat, wird in Policy Spy ein Hyperlink angezeigt. Klicken Sie auf den Link, um den Richtlinientext direkt vom Verwaltungspunkt des Clients herunterzuladen. Wenn das Tool den Richtlinientext erfolgreich herunterlädt, wird der Hyperlink durch die Inhalte der Antwort ersetzt. Andernfalls aktualisiert Policy Spy die Anzeige und gibt an, dass die Anforderung fehlgeschlagen ist.

