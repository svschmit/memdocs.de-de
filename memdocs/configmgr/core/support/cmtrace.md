---
title: CMTrace
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie mit dem CMTrace-Tool Protokolldateien für Configuration Manager anzeigen können.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6a4a3290-5228-4871-918a-554aa1c20834
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8c9c42dcd1e6a6a4ca064953f0513157f5ebb228
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707898"
---
# <a name="cmtrace"></a>CMTrace

*Gilt für: Configuration Manager (Current Branch)*

CMTrace ist eines der [Configuration Manager-Tools](tools.md). Sie können damit Protokolldateien anzeigen und überwachen, einschließlich der folgenden Typen:  

- Protokolldateien im Configuration Manager- oder CCM-Format (CCM = Client Component Manager)  

- Einfache ASCII- oder Unicode-Textdateien, wie z.B. Windows Installer-Protokolle  

Sie können mit dem Tool durch Hervorheben, Filtern und Fehlersuche Protokolldateien analysieren.

Das CMTrace-Protokollanzeigetool wird jetzt automatisch ab Version 1806 mit dem Konfigurations-Manager-Client installiert. Es wird dem Clientinstallationsverzeichnis (standardmäßig `%WinDir%\CCM\CMTrace.exe`) hinzugefügt.<!--1357971-->

> [!Note]  
> Windows legt nicht automatisch fest, dass CMTrace Dateien mit der Erweiterung LOG öffnet. Weitere Informationen finden Sie unter [Dateizuordnungen](#file-associations).  

Ab Version 1906 ist **OneTrace** als neue Protokollanzeige im Supportcenter verfügbar. Die Funktionsweise ähnelt der von CMTrace, bietet jedoch einige Verbesserungen. Weitere Informationen finden Sie unter [Supportcenter – OneTrace](support-center-onetrace.md).

## <a name="usage"></a>Verwendung

Führen Sie **CMTrace.exe** aus. Bei der ersten Ausführung des Tools wird Ihnen eine Eingabeaufforderung zur Dateizuordnung angezeigt. Weitere Informationen finden Sie unter [Dateizuordnungen](#file-associations).

Sie können die meisten Aktionen in CMTrace über die folgenden Menüs ausführen:

- [File](#file-menu)
- [Extras](#tools-menu)

### <a name="file-menu"></a>Menü „Datei“

Im Menü **Datei** sind die folgenden Aktionen verfügbar:  

- [Öffnen](#open)
- [Open on Server](#open-on-server) (Auf Server öffnen)
- [Drucken](#print)
- [Einstellungen](#preferences)

Im Menü „Datei“ werden zudem die acht zuletzt geöffneten Dateien angezeigt. Sie können eines dieser Protokolle ohne großen Aufwand erneut öffnen, indem Sie dieses über das Menü „Datei“ auswählen.

#### <a name="open"></a>Öffnen

Zeigt das Dialogfeld „Öffnen“ an, in dem nach einer Protokolldatei gesucht werden kann.

Filtern Sie die Ansicht nach folgenden Dateitypen:

- Protokolldateien (\*.log)  
- Alte Protokolldateien (\*.lo_)
- Alle Dateien (\*.\*)

Folgende zwei Optionen sind standardmäßig nicht ausgewählt:  

- **Ignore existing lines** (Vorhandene Zeilen ignorieren): Bei Auswahl dieser Option ignoriert CMTrace die vorhandenen Inhalte der ausgewählten Protokolldatei und zeigt neue Zeilen nur an, wenn diese hinzugefügt werden. Verwenden Sie diese Option, wenn Sie nur neue Aktionen überwachen möchten und nicht den vollständigen Verlauf der Protokolldatei benötigen.  

- **Merge selected files** (Ausgewählte Dateien zusammenführen): Wenn Sie diese Option aktivieren und mehrere Protokolldateien auswählen, führt CMTrace die ausgewählten Protokolle in der Ansicht zusammen. Sie werden so angezeigt, als würde es sich um eine einzelne Protokolldatei handeln. Das zusammengeführte Protokoll wird auf gleiche Weise aktualisiert und unterstützt sämtliche weiteren CMTrace-Features, als würde es sich um eine einzelne Protokolldatei handeln.  

#### <a name="open-on-server"></a>Auf Server öffnen

Sie können den Ordner mit den Configuration Manager-Protokollen auf einem Standortsystemcomputer über das Standarddialogfeld „Durchsuchen“ durchsuchen. Zudem können sie das Netzwerk eines Remotecomputers durchsuchen.

Wenn Sie einen Remotecomputer auswählen, der durchsucht werden soll, überprüft CMTrace die Configuration Manager-Freigabe. Wenn keine Freigabe für Configuration Manager-Protokolldateien gefunden werden kann, wird eine Fehlermeldung angezeigt.  

Mithilfe der Aktion [Öffnen](#open) können Sie ohne vorheriges Durchsuchen eine direkte Verbindung mit einem bekannten Computer herstellen. Geben Sie anschließend einen Servernamen ein, und geben Sie diesen im UNC-Format frei.

#### <a name="print"></a>Drucken

Zeigt das Windows-Standarddialogfeld „Drucken“ an. Durch diese Aktion wird die aktuelle Protokolldatei an einen Drucker gesendet. Die Ausgabe wird gemäß den Einstellungen auf der Registerkarte „Drucken“ der CMTrace-Voreinstellungen formatiert.

#### <a name="preferences"></a>Einstellungen

Konfigurieren Sie die Einstellungen für CMTrace. Die folgenden Optionen sind verfügbar:  

- Registerkarte**Allgemein**  

    - **Update Interval** (Updateintervall): Steuert, wie häufig CMTrace Protokolldateien auf Änderungen überprüft und neue Zeilen lädt. Dieser Wert ist standardmäßig auf 500 Millisekunden festgelegt.  

    - **Hervorheben**: Legt die Farbe fest, die CMTrace beim Hervorheben der von Ihnen ausgewählten Protokollzeilen verwendet. Standardmäßig wird als Farbe einfaches Gelb verwendet (Rot: 255, Grün: 255, Blau: 0).  

    - **Spalten:** Konfiguriert die Spalten, die in der Protokollansicht sichtbar sind, und die Reihenfolge, in der diese angezeigt werden. Standardmäßig sind die Spalten in der Reihenfolge „Protokolltext“, „Komponente“, „Datum/Uhrzeit“ und „Thread“ angeordnet.  

- Registerkarte **Wird gedruckt**  

    - **Spalten:** Konfiguriert, welche Spalten beim Drucken von Protokolldateien verwendet werden, sowie die Reihenfolge, in der sie angezeigt werden. Standardmäßig werden die Spalten gedruckt, die angezeigt werden.  

    - **Ausrichtung**: Legt die Standardausrichtung beim Drucken von Protokolldateien fest. Sie können diese Einstellung im Dialogfeld „Drucken“ außer Kraft setzen. Standardmäßig wird die Ausrichtung „Hochformat“ verwendet.  

- Registerkarte **Erweitert**  

    - **Aktualisierungsintervall**: Erzwingt, dass CMTrace die Protokollansicht in einem bestimmten Intervall aktualisiert, wenn eine große Anzahl von Zeilen geladen wird. Diese Option wird standardmäßig mit dem Wert „0“ deaktiviert.  

        > [!Note]  
        > Im Allgemeinen wird das **Aktualisierungsintervall** nicht geändert. Die Dauer zum Öffnen großer Protokolldateien kann dadurch erheblich erhöht werden.

### <a name="tools-menu"></a>Menü „Extras“

Im Menü **Extras** sind die folgenden Aktionen verfügbar:

- [Suchen](#find)
- [Weitersuchen](#find-next)
- [In Zwischenablage kopieren](#copy-to-clipboard)
- [Hervorheben](#highlight)
- [Filtern](#filter)
- [Fehlersuche](#error-lookup)
- [Anhalten](#pause)
- [Details ein-/ausblenden](#showhide-details)
- [Infobereich ein-/ausblenden](#showhide-info-pane)

#### <a name="find"></a>Finden

Durchsucht die offene Protokolldatei nach einer bestimmten Textzeichenfolge.  

#### <a name="find-next"></a>Weitersuchen

Sucht nach der nächsten übereinstimmenden Zeichenfolge, die Sie zuvor im Dialogfeld „Suchen“ angegeben haben.  

#### <a name="copy-to-clipboard"></a>In Zwischenablage kopieren

Kopiert die ausgewählten Zeilen in Form von reinem Text in die Windows-Zwischenablage. Wenn Sie Configuration Manager- und CCM-Protokolldateien überprüfen, werden die Spalten in der gleichen Reihenfolge wie in der Ansicht kopiert. Die einzelnen Spalten werden durch ein Tabstoppzeichen voneinander getrennt. Verwenden Sie diese Aktion, wenn Sie Protokolle in E-Mails oder andere Dokumente kopieren möchten.  

#### <a name="highlight"></a>Hervorheben

Geben Sie eine Zeichenfolge ein, die CMTrace verwendet, um den Text der einzelnen Protokolleinträge zu durchsuchen. Anschließend wird sämtlicher Protokolltext hervorgehoben, der mit der von Ihnen eingegebenen Zeichenfolge übereinstimmt.  

- Bei der Hervorhebung wird die Farbe verwendet, die Sie in den Voreinstellungen angegeben haben.  

- Zur Deaktivierung der Hervorhebung müssen Sie die Zeichenfolge aus diesem Feld löschen.  

- Wenn Sie eine dezimale oder hexadezimale Zahl eingeben, versucht CMTrace, den Wert mit der Spalte „Thread“ abzugleichen. Verwenden Sie dieses Verhalten, um die Verarbeitung eines einzelnen Threads hervorzuheben, ohne andere Threads herauszufiltern, die möglicherweise damit interagieren.  

- Aktivieren Sie die Option **Groß-/Kleinschreibung beachten**, um Zeichenfolgen nach Groß-/Kleinschreibung miteinander zu vergleichen.  

#### <a name="filter"></a>Filter

Blendet Protokollzeilen basierend auf bestimmten Kriterien ein oder aus. Wenden Sie auf alle vier Spalten Filter an, unabhängig davon, ob sie sichtbar sind oder nicht. Diese Einstellungen gelten für alle geöffneten Protokolldateien.

Beispiele:
<!--SCCMDocs issue #603-->

- Filtern Sie **smsts.log** nach einem Texteintrag, der „die Aktion“ oder „die Gruppe“ enthält.
- Filtern Sie **InventoryAgent.log**, wo der Texteintrag „Ziel“ enthält.

#### <a name="error-lookup"></a>Fehlersuche

Geben Sie einen Fehlercode im Dezimal- oder Hexadezimalformat ein, oder fügen Sie einen Fehlercode ein, um eine Beschreibung anzuzeigen. Mögliche Fehlerquellen sind: Windows, WMI oder Winhttp.

#### <a name="pause"></a>Anhalten

Hält die Protokollüberwachung an oder startet diese neu. Die folgenden Anwendungsfälle stellen einige der möglichen Gründe für die Verwendung dieser Aktion dar:  

- Wenn CMTrace Protokolldateiinformationen zu schnell angezeigt  

- Wenn Sie die Protokollüberwachung anhalten, gehen die in CMTrace angezeigten Informationen nicht verloren, wenn in der aktuellen Datei ein Rollover für ein neues Protokoll durchgeführt wird.  

- Wenn CMTrace keine neuen Daten mehr anzeigen soll, während Sie die Protokolldatei überprüfen möchten  

#### <a name="showhide-details"></a>Details ein-/ausblenden

Blendet, mit Ausnahme des Protokolltexts, sämtliche Spalten ein oder aus. Zudem wird die Spalte mit dem Protokolltext auf die Breite des Fensters erweitert. Verwenden Sie diese Aktion, wenn Sie Protokolle auf einem Computer mit niedriger Auflösung anzeigen. Es wird mehr von dem Protokolltext angezeigt.  

> [!Note]  
> Beim Anzeigen von aus reinem Text bestehenden Dateien blendet CMTrace Details automatisch aus, da diese immer leer sind.  

#### <a name="showhide-info-pane"></a>Infobereich ein-/ausblenden

Blendet den Infobereich ein oder aus. Verwenden Sie diese Aktion, wenn Sie Protokolle auf einem Computer mit niedriger Auflösung anzeigen. Es werden weitere Protokollierungsdetails angezeigt.  


## <a name="log-pane"></a>Protokollbereich

Der Protokollbereich befindet sich im oberen Bereich des CMTrace-Fensters. In diesem Bereich werden die Zeilen aus Protokolldateien angezeigt.

Wenn Sie eine Zeile auswählen, wird diese vorübergehend mithilfe des Farbauswahlschemas von Windows hervorgehoben.

Hervorgehobene Zeilen entsprechen den Kriterien, die Sie über die **Hervorheben** im Menü **Extras** definiert haben. Bei der Hervorhebung wird die Farbe verwendet, die Sie unter **Einstellungen** angegeben haben.

CMTrace zeigt fehlerhafte Zeilen mit rotem Hintergrund und gelber Textfarbe an. In Protokollen im CCM-Format weisen Protokolleinträge einen expliziten Eingabetyp auf, der den Eintrag als Fehler angibt. Bei anderen Protokollformaten führt CMTrace für jeden Eintrag mit einer fehlerhaften Textzeichenfolge eine Suche durch, bei der die Groß-/Kleinschreibung nicht beachtet wird.

Die Zeilen mit Warnungen werden mit gelben Hintergrund angezeigt. In Protokollen im CCM-Format weisen Protokolleinträge einen expliziten Eingabetyp auf, der den Eintrag als Warnung angibt. Bei anderen Protokollformaten führt CMTrace für jeden Eintrag mit einer Textzeichenfolge, für die eine Warnung ausgegeben wird, eine Suche durch, bei der die Groß-/Kleinschreibung nicht beachtet wird.


## <a name="info-pane"></a>Infobereich

Der Infobereich befindet sich im unteren Bereich des CMTrace-Fensters. Es umfasst die folgenden Funktionen:

- Details zum aktuell ausgewählten Protokolleintrag  

- Ein Textfeld, in dem der Protokolltext angezeigt wird  

- Es werden Wagenrückläufe angezeigt, damit formatierter Text leichter zu lesen ist.  

- Lange Einträge, die leichter zu lesen und im Protokollbereich nicht vollständig sichtbar sind  

Sie können den Infobereich mithilfe der Option **Infobereich ein-/ausblenden** im Menü **Extras** ein- oder ausblenden. Wenn der Infobereich mehr als die Hälfte des Protokollfensters einnimmt, blendet CMTrace den Bereich automatisch aus.

### <a name="progress-bar"></a>Statusanzeige

Wenn Sie zum ersten Mal eine Protokolldatei öffnen, ersetzt CMTrace den Bereich „Informationen“ durch eine Statusanzeige. Dieser Status gibt an, wie viele der vorhandenen Dateiinhalte geladen wurden. Wenn der Status 100 % erreicht, entfernt CMTrace die Statusanzeige und ersetzt diese durch den Infobereich. Beim Laden großer Dateien gibt dieses Verhalten an, wie viel Zeit der Ladevorgang möglicherweise in Anspruch nimmt.

### <a name="status-bar"></a>Statusleiste

Bei Protokolldateien im Configuration Manager- und CCM-Format wird in der Statusleiste bei den ausgewählten Protokolleinträgen die verstrichene Zeit angezeigt. Wenn Sie einen einzelnen Eintrag auswählen, zeigt das Tool die Zeit vom ersten Protokolleintrag bis zum ausgewählten Eintrag an. Wenn Sie mehrere Einträge auswählen, berechnet das Tool die Zeit vom obersten ausgewählten Eintrag bis zum untersten ausgewählten Eintrag. CMTrace formatiert diese Informationen wie folgt:

`Elapsed time is <hours>h <minutes>m <seconds>s <milliseconds>ms (<seconds+milliseconds> seconds)`


## <a name="windows-shell-integration"></a>Windows-Shellintegration

CMTrace unterstützt [Dateizuordnungen](#file-associations) und [Drag & Drop](#drag-and-drop).

### <a name="file-associations"></a>Dateizuordnungen

CMTrace kann sich selbst die Dateinamenerweiterungen LOG und LO_ zuordnen. Wenn das Programm gestartet wird, wird die Registrierung überprüft, um zu ermitteln, diese Dateinamenerweiterungen dem Tool bereits zugeordnet wurden. Wenn CMTrace noch keine Dateinamenerweiterungen zugeordnet wurden, werden Sie dazu aufgefordert, CMTrace die Dateinamenerweiterungen zuzuordnen. Wenn Sie **Nicht mehr fragen** auswählen, überspringt CMTrace diese Überprüfung bei jeder Ausführung auf diesem Computer.

### <a name="drag-and-drop"></a>Drag & Drop

CMTrace unterstützt die grundlegende Drag & Drop-Funktionalität. Ziehen Sie eine Protokolldatei aus dem Windows-Explorer in CMTrace, um diese zu öffnen.


## <a name="other-tips"></a>Weitere Tipps

### <a name="last-directory-registry-key"></a>Registrierungsschlüssel für „Last Directory“ (Letztes Verzeichnis)

<!--511280-->
CMTrace speichert standardmäßig den letzten von Ihnen geöffneten Protokollspeicherort. Dieses Verhalten ist auf dem Standortserver nützlich, da auf diesem jedes Mal der Protokollpfad als Standardwert festgelegt wird.

Beim ersten Start auf einem Client wird das aktuelle Arbeitsverzeichnis als Standardwert festgelegt. Bei diesem Speicherort handelt es sich möglicherweise um den Pfad, in dem Sie CMTrace gespeichert haben, oder um einen mit `%userprofile%\Desktop` vergleichbaren Pfad.

Der Wert **Last Directory** (Letztes Verzeichnis) im Registrierungsschlüssel `HKEY_CURRENT_USER\Software\Microsoft\Trace32` steuert diesen Standardspeicherort. Wenn Sie diesen Wert auf Ihren Clients auf `%windir%\CCM\Logs` festlegen, öffnet CMTrace bei der ersten Ausführung Dateien im Protokollspeicherort der Clients.


## <a name="see-also"></a>Weitere Informationen:

- [Protokolldateien](../plan-design/hierarchy/log-files.md)

- [Protokolldateianzeige des Supportcenters](support-center.md#support-center-log-file-viewer)

- [Supportcenter – OneTrace](support-center-onetrace.md)
