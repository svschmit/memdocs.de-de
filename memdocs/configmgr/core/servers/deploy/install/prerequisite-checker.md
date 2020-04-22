---
title: Voraussetzungsprüfung
titleSuffix: Configuration Manager
description: Hier erfahren Sie, wie Sie mit der Voraussetzungsprüfung Probleme erkennen und beheben, die die Installation eines Standorts oder einer Standortsystemrolle verhindern könnten.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aaf13bb8-4ba2-4bd7-9fac-d36a9d88a1b6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1ee871d99285bee3a4489d88bf0d203bf74cde3c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700708"
---
# <a name="prerequisite-checker-for-configuration-manager"></a>Voraussetzungsprüfung für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

 Bevor Sie Setup zum Installieren oder Aktualisieren eines Configuration Manager-Standorts ausführen bzw. bevor Sie auf einem neuen Server eine Standortsystemrolle installieren, können Sie diese eigenständige Anwendung (**Prereqchk.exe**) für die Version von Configuration Manager verwenden, mit der Sie die Serverbereitschaft überprüfen möchten. Erkennen Sie mit der Voraussetzungsprüfung Probleme und beheben Sie die, die die Installation eines Standorts oder einer Standortsystemrolle verhindern würden.  

> [!NOTE]  
>  Die Voraussetzungsprüfung wird immer als Teil von Setup ausgeführt.  

Die Voraussetzungsprüfung führt standardmäßig diese Schritte aus:  

-   Sie überprüft den Server, auf dem sie ausgeführt wird.  
-   Der lokale Computer wird auf einen vorhandenen Standortserver überprüft, und es werden nur die für diesen Standort relevanten Prüfungen ausgeführt.  
-   Wenn keine vorhandenen Standorte erkannt werden, werden alle vorausgesetzten Regeln ausgeführt.  
-   Sie überprüft, ob die Software und die Einstellungen installiert wurden, die für das Setup erforderlich sind. Es ist möglich, dass erforderliche Software zusätzliche Konfigurationen oder Softwareupdates benötigt, die nicht von der Voraussetzungsprüfung überprüft werden.  
-   Sie protokolliert ihre Ergebnisse in der Datei **ConfigMgrPrereq.log** auf dem Systemlaufwerk des Computers. Die Protokolldatei enthält möglicherweise Zusatzinformationen, die nicht auf der Anwendungsoberfläche erscheinen.  

Wenn Sie die Voraussetzungsprüfung bei der Eingabeaufforderung ausführen und spezifische Befehlszeilenoptionen angeben:  

-   Die Voraussetzungsprüfung führt nur die Prüfungen aus, die dem Standortserver oder den Standortsystemen zugeordnet sind, die Sie an der Befehlszeile angegeben haben.  
-   Um einen Remotecomputer zu überprüfen, muss Ihr Benutzerkonto über Administratorrechte für den Remotecomputer verfügen.  

Weitere Informationen zu Voraussetzungsprüfungen finden Sie unter [Liste mit Voraussetzungsprüfungen für Configuration Manager](../../../../core/servers/deploy/install/list-of-prerequisite-checks.md).  

## <a name="copy-prerequisite-checker-files-to-another-computer"></a>Kopieren von Dateien der Voraussetzungsprüfung auf einen anderen Computer  

1.  Gehen Sie in Windows-Explorer zu einem der folgenden Speicherorte:  

    -   **&lt;*Configuration Manager-Installationsmedium*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Configuration Manager-Installationspfad*\>\BIN\X64**  

2.  Kopieren Sie die folgenden Dateien in den Zielordner auf dem anderen Computer:  

    - prereqchk.exe
    - prereqcore.dll
    - prereqchkres.dll
      - Diese Datei befindet sich im Unterordner für die Installationssprache. Englisch beispielsweise befindet sich im Unterordner `00000409`. <!--586808-->
    - basesql.dll
    - basesvr.dll
    - baseutil.dll

##  <a name="run-prerequisite-checker-with-default-checks"></a>Ausführen der Voraussetzungsprüfung mit Standardprüfungen  

1.  Gehen Sie in Windows-Explorer zu einem der folgenden Speicherorte:  

    -   **&lt;*Configuration Manager-Installationsmedium*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Configuration Manager-Installationspfad*\>\BIN\X64**  

2.  Führen Sie **prereqchk.exe** aus, um die Voraussetzungsprüfung zu starten.   
    Mithilfe der Voraussetzungsprüfung werden vorhandene Standorte erkannt und auf ihre Bereitschaft für Upgrades überprüft. Wenn keine Standorte gefunden werden, werden alle Prüfungen ausgeführt. In der Spalte **Standorttyp** finden Sie Informationen zum Standortserver oder Standortsystem, dem die Rolle zugeordnet ist.  

##  <a name="run-prerequisite-checker-from-a-command-prompt-for-all-default-checks"></a>Ausführen der Voraussetzungsprüfung über eine Eingabeaufforderung für alle Standardprüfungen  

1.  Öffnen Sie ein Eingabeaufforderungsfenster, und wechseln Sie zu einem der folgenden Speicherorte:  

    -   **&lt;*Configuration Manager-Installationsmedium*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Configuration Manager-Installationspfad*\>\BIN\X64**  

2.  Geben Sie  **prereqchk.exe /LOCAL** ein, um die Voraussetzungsprüfung zu starten und alle Prüfungen auf dem Server auszuführen.  

## <a name="run-prerequisite-checker-from-a-command-prompt-to-use-options"></a>Ausführen der Voraussetzungsprüfung über eine Eingabeaufforderung für angegebene Optionen  

1. Öffnen Sie ein Eingabeaufforderungsfenster, und wechseln Sie zu einem der folgenden Speicherorte:  

   -   **&lt;*Configuration Manager-Installationsmedium*\>\SMSSETUP\BIN\X64**  
   -   **&lt;*Configuration Manager-Installationspfad*\>\BIN\X64**  

2. Geben Sie **prereqchk.exe** sowie eine oder mehrere der folgenden Befehlszeilenoptionen ein.  

   Um z.B. einen primären Standort zu überprüfen, können Sie Folgendes verwenden:  

      **prereqchk.exe [/NOUI] /PRI /SQL &lt;FQDN von SQL Server\> /SDK &lt;FQDN des SMS-Anbieters\> [/JOIN &lt;FQDN des Standorts der zentralen Verwaltung\>] [/MP &lt;FQDN des Verwaltungspunkts\>] [/DP &lt;FQDN des Verteilungspunkts\>]**  

   **Standortserver der zentralen Verwaltung:**  

   -   **/NOUI**  

        Nicht erforderlich. Startet die Voraussetzungsprüfung, ohne die Benutzeroberfläche anzuzeigen. Sie müssen diese Option vor allen anderen Optionen in der Befehlszeile angeben.  

   -   **/CAS**  

        Erforderlich. Mit dieser Option wird überprüft, ob der lokale Computer die Anforderungen für den Standort der zentralen Verwaltung erfüllt.  

   -   **/SQL &lt;*FQDN von SQL Server*>**  

        Erforderlich. Das Verwenden des vollqualifizierten Domänennamens (fully qualified domain name, FQDN) überprüft, ob auf dem angegebenen Computer die Voraussetzungen für SQL Server zum Hosten der Configuration Manager-Standortdatenbank erfüllt sind.  

   -   **/SDK &lt;*FQDN des SMS-Anbieters*>**  

        Erforderlich. Mit dieser Option wird überprüft, ob der angegebene Computer die Anforderungen für den SMS-Anbieter erfüllt.  

   -   **/Ssbport**  

        Nicht erforderlich. Mit dieser Option wird überprüft, ob eine Firewallausnahme eingerichtet wurde, um die Kommunikation auf dem SSB-Port (SQL Server Service Broker) zuzulassen. Der Standard-SSB-Port ist 4022.  

   -   **InstallDir &lt;*Configuration Manager-Installationspfad*>**  

        Nicht erforderlich. Mit dieser Option wird überprüft, ob der benötigte Mindestspeicherplatz für die Standortinstallation verfügbar ist.  

   **Primärer Standortserver:**  

   -   **/NOUI**  

       Nicht erforderlich. Startet die Voraussetzungsprüfung, ohne die Benutzeroberfläche anzuzeigen. Sie müssen diese Option vor allen anderen Optionen in der Befehlszeile angeben.  

   -   **/PRI**  

        Erforderlich. Mit dieser Option wird überprüft, ob der lokale Computer die Anforderungen für den primären Standort erfüllt.  

   -   **/SQL &lt;*FQDN von SQL Server*>**  

        Erforderlich. Mit dieser Option wird überprüft, ob auf dem angegebenen Computer die Voraussetzungen für SQL Server zum Hosten der Configuration Manager-Standortdatenbank erfüllt sind.  

   -   **/SDK &lt;*FQDN des SMS-Anbieters*>**  

        Erforderlich. Mit dieser Option wird überprüft, ob der angegebene Computer die Anforderungen für den SMS-Anbieter erfüllt.  

   -   **/JOIN &lt;*FQDN des Standorts der zentralen Verwaltung*>**  

        Nicht erforderlich. Mit dieser Option wird überprüft, ob der lokale Computer die Anforderungen für die Verbindung mit dem Standortserver der zentralen Verwaltung erfüllt.  

   -   **/MP &lt;*FQDN des Verwaltungspunkts*>**  

        Nicht erforderlich. Mit dieser Option wird überprüft, ob der angegebene Computer die Anforderungen für die Standortsystemrolle „Verwaltungspunkt“ erfüllt. Diese Option wird nur unterstützt, wenn Sie die Option **/PRI** verwenden.  

   -   **/DP &lt;*FQDN des Verteilungspunkts*>**  

        Nicht erforderlich. Mit dieser Option wird überprüft, ob der angegebene Computer die Anforderungen für die Standortsystemrolle „Verteilungspunkt“ erfüllt. Diese Option wird nur unterstützt, wenn Sie die Option **/PRI** verwenden.  

   -   **/Ssbport**  

        Nicht erforderlich. Mit dieser Option wird überprüft, ob eine Firewallausnahme eingerichtet wurde, um die Kommunikation über den SSB-Port zuzulassen. Der Standard-SSB-Port ist 4022.  

   -   **InstallDir &lt;*Configuration Manager-Installationspfad*>**  

        Nicht erforderlich. Mit dieser Option wird überprüft, ob der benötigte Mindestspeicherplatz für die Standortinstallation verfügbar ist.  

   **Sekundärer Standortserver:**  

   -   **/NOUI**  

        Nicht erforderlich. Startet die Voraussetzungsprüfung, ohne die Benutzeroberfläche anzuzeigen. Sie müssen diese Option vor allen anderen Optionen in der Befehlszeile angeben.  

   -   **/SEC &lt;*FQDN des sekundären Standortservers*>**  

        Erforderlich. Mit dieser Option wird überprüft, ob der angegebene Computer die Anforderungen für den sekundären Standort erfüllt.  

   -   **/INSTALLSQLEXPRESS**  

        Nicht erforderlich. Mit dieser Option wird überprüft, ob SQL Server Express auf dem angegebenen Computer installiert werden kann.  

   -   **/Ssbport**  

        Nicht erforderlich. Mit dieser Option wird überprüft, ob eine Firewallausnahme eingerichtet wurde, um die Kommunikation für den SSB-Port zuzulassen. Der Standard-SSB-Port ist 4022.  

   -   **/Sqlport**  

        Nicht erforderlich. Mit dieser Option wird überprüft, ob eine Firewallausnahme eingerichtet wurde, um die Verbindung mit dem SQL Server-Dienstport zuzulassen, und ob der Port von keiner anderen benannten SQL Server-Instanz verwendet wird. Der Standardport ist 1433.  

   -   **InstallDir &lt;*Configuration Manager-Installationspfad*>**  

        Nicht erforderlich. Mit dieser Option wird überprüft, ob der benötigte Mindestspeicherplatz für die Standortinstallation verfügbar ist.  

   -   **/SourceDir**  

        Nicht erforderlich. Mit dieser Option wird überprüft, ob das Computerkonto des sekundären Standorts auf den Ordner zugreifen kann, von dem die Quelldateien für Setup gehostet werden.  

   **Configuration Manager-Konsole:**  

   -   **/Adminui**  

        Erforderlich. Überprüft, ob der lokale Computer die Anforderungen für die Installation von Configuration Manager erfüllt.  

3. Im Bereich **Ergebnis der Voraussetzungsprüfung** auf der Benutzeroberfläche der Voraussetzungsprüfung werden alle erkannten Probleme aufgelistet.  

   -   Klicken Sie in der Liste auf einen Eintrag, um Details zur Behebung des Problems anzuzeigen.  
   -   Sie können mit der Installation des Standortservers, des Standortsystems oder der Configuration Manager-Konsole erst dann fortfahren, wenn alle in der Liste mit dem Status **Fehler** aufgeführten Elemente korrigiert wurden.  
   -   Sie können die Ergebnisse der Voraussetzungsprüfung auch überprüfen, indem Sie die Datei **ConfigMgrPrereq.log** im Stamm des Systemlaufwerks öffnen. Die Protokolldatei enthält möglicherweise weitere Informationen, die nicht auf der Benutzeroberfläche der Voraussetzungsprüfung angezeigt werden.  
