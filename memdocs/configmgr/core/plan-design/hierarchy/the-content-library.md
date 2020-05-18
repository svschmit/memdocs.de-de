---
title: Die Inhaltsbibliothek
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über die Inhaltsbibliothek, die Configuration Manager verwendet, um die Gesamtgröße verteilter Inhalte zu reduzieren.
ms.date: 07/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 65c88e54-3574-48b0-a127-9cc914a89dca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d7432b3522d5292e2c2afc1dac6b8db3382cca12
ms.sourcegitcommit: 4c129bb04ea4916c78446e89fbff956397cbe828
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/13/2020
ms.locfileid: "83343166"
---
# <a name="the-content-library-in-configuration-manager"></a>Die Inhaltsbibliothek in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Die Inhaltsbibliothek ist ein Einzelinstanzspeicher für Inhalte in Configuration Manager. Sie wird vom Standort verwendet, um die Gesamtgröße des von Ihnen verteilten kombinierten Inhaltstexts zu reduzieren. In der Inhaltsbibliothek werden alle Inhaltsdateien für Softwarebereitstellungen wie Softwareupdates, Anwendungen und Betriebssystembereitstellungen gespeichert.  

- Der Standort erstellt und verwaltet auf jedem Standortserver und auf jedem Verteilungspunkt automatisch eine Kopie der Inhaltsbibliothek.  

- Bevor von Configuration Manager Inhaltsdateien zum Standortserver hinzugefügt oder die Dateien auf Verteilungspunkte kopiert werden, überprüft Configuration Manager, ob die einzelnen Inhaltsdateien bereits in der Inhaltsbibliothek vorhanden sind.  

- Wenn die Inhaltsdatei verfügbar ist, kopiert Configuration Manager die Datei nicht. Stattdessen wird die vorhandene Inhaltsdatei der Anwendung oder dem Paket zugeordnet.  

Konfigurieren Sie auf Verteilungspunktservern die folgenden Optionen:

- Mindestens ein Laufwerk, auf dem Sie die Inhaltsbibliothek erstellen möchten.  

- Eine Priorität für jedes verwendete Laufwerk.  

Von Configuration Manager werden Inhaltsdateien auf das Laufwerk mit der höchsten Priorität kopiert, sofern auf diesem Laufwerk der von Ihnen angegebene freie Mindestspeicherplatz verfügbar ist.  

- Sie konfigurieren die Laufwerkseinstellungen bei der Installation des Verteilungspunkts.  

- Nach Abschluss der Installation können Sie die Laufwerkseinstellungen nicht mehr in den Verteilungspunkteigenschaften konfigurieren.  

Weitere Informationen zum Konfigurieren der Laufwerkseinstellungen für den Verteilungspunkt finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur](../../servers/deploy/configure/manage-content-and-content-infrastructure.md).  

> [!IMPORTANT]
> Wenn Sie die Inhaltsbibliothek nach der Installation auf einem Verteilungspunkt an einen anderen Speicherort verschieben möchten, verwenden Sie hierzu das Tool für die Inhaltsbibliotheksübertragung (**Content Library Transfer Tool**) in den Configuration Manager-Tools. Weitere Informationen finden Sie unter [Content Library Transfer Tool (Tool für die Inhaltsbibliotheksübertragung)](../../support/content-library-transfer.md).  


## <a name="about-the-content-library-on-the-central-administration-site"></a>Informationen zur Inhaltsbibliothek am Standort der zentralen Verwaltung

Von Configuration Manager wird beim Installieren des Standorts standardmäßig eine Inhaltsbibliothek am Standort der zentralen Verwaltung erstellt. Die Inhaltsbibliothek wird auf dem Standortserver auf dem Laufwerk mit dem meisten freien Speicherplatz gespeichert. Da es Ihnen nicht möglich ist, am Standort der zentralen Verwaltung einen Verteilungspunkt zu installieren, können Sie keine Prioritäten für die Laufwerke zur Verwendung der Inhaltsbibliothek festlegen. Wenn auf dem Laufwerk, auf dem die Inhaltsbibliothek gespeichert ist, nicht mehr genügend Speicherplatz verfügbar ist, wird die Inhaltsbibliothek auf vergleichbare Weise wie eine Inhaltsbibliothek auf anderen Standortservern und Verteilungspunkten automatisch auf das nächste verfügbare Laufwerk ausgedehnt.  

Die Inhaltsbibliothek wird in den folgenden Szenarios von Configuration Manager am Standort der zentralen Verwaltung verwendet:  

- Sie erstellen Inhalt am Standort der zentralen Verwaltung  

- Sie migrieren Inhalt von einem anderen Configuration Manager-Standort und legen den Standort der zentralen Verwaltung als Standort für die Inhaltsverwaltung fest  

> [!NOTE]  
> Wenn Sie Inhalt an einem primären Standort erstellen und den Inhalt dann an einen anderen primären Standort oder an einen sekundären Standort unterhalb eines anderen primären Standorts verteilen, wird der Inhalt vorübergehend am Standort der zentralen Verwaltung im Eingang des Planers gespeichert. Der Inhalt wird jedoch nicht der zugehörigen Inhaltsbibliothek hinzugefügt.  

Verwenden Sie die folgenden Optionen zum Verwalten der Inhaltsbibliothek am Standort der zentralen Verwaltung:  

- Um zu verhindern, dass die Inhaltsbibliothek auf einem bestimmten Laufwerk installiert wird, erstellen Sie eine leere Datei namens **no_sms_on_drive.sms**. Kopieren Sie sie in das Stammverzeichnis des Laufwerks, bevor die Inhaltsbibliothek erstellt wird.  

- Verwenden Sie nach dem Erstellen der Inhaltsbibliothek das Tool **Content Library Transfer** der Configuration Manager-Tools, um den Speicherort der Inhaltsbibliothek zu verwalten. Weitere Informationen finden Sie unter [Content Library Transfer Tool (Tool für die Inhaltsbibliotheksübertragung)](../../support/content-library-transfer.md).  

> [!Note]  
> Cloudverteilungspunkte verwenden keinen Einzelinstanzspeicher. Der Standort verschlüsselt Pakete vor dem Versenden an Azure, und jedes Paket verfügt über einen eindeutigen verschlüsselten Schlüssel. Auch wenn zwei Dateien identisch sind, wären die verschlüsselten Versionen nicht identisch.  


## <a name="configure-a-remote-content-library-for-the-site-server"></a><a name="bkmk_remote"></a> Konfigurieren einer Remoteinhaltsbibliothek für den Standortserver

<!--1357525-->
Wenn Sie ab Version 1806 die [Hochverfügbarkeit der Standortserver](../../servers/deploy/configure/site-server-high-availability.md) konfigurieren oder auf Ihrem zentralen Verwaltungsserver oder primären Standortserver Speicherplatz auf einem Laufwerk freigeben möchten, müssen Sie die Inhaltsbibliothek an einen anderen Speicherort verschieben. Verschieben Sie die Inhaltsbibliothek auf ein anderes Laufwerk auf dem Standortserver, einen separaten Server oder ein fehlertolerantes Laufwerk in einem Storage Area Network (SAN). Ein SAN ist empfehlenswert, da er hochverfügbar ist und sein flexibler Speicher mit der Zeit größer oder kleiner wird, um Ihre sich ändernden Anforderungen zu erfüllen. Weitere Informationen finden Sie unter [High availability options (Optionen für Hochverfügbarkeit)](../../servers/deploy/configure/site-server-high-availability.md).

Eine Remoteinhaltsbibliothek ist eine Voraussetzung für die [Hochverfügbarkeit von Standortservern](../../servers/deploy/configure/site-server-high-availability.md).

> [!Note]  
> Diese Aktion verschiebt nur die Inhaltsbibliothek auf den Standortserver. Sie hat keinerlei Auswirkung auf die Position der Inhaltsbibliothek auf Verteilungspunkten. 

> [!Tip]  
> Planen Sie auch die Verwaltung des Paketquelleninhalts, der sich außerhalb der Inhaltsbibliothek befindet. Alle Softwareobjekte in Configuration Manager verfügen über eine Paketquelle auf einer Netzwerkfreigabe. Ziehen Sie eine zentrale Verwaltung aller Quellen auf einer einzelnen Freigabe in Erwägung, stellen Sie dabei jedoch sicher, dass dieser Speicherort redundant und hochverfügbar ist.
>
> Wenn Sie die Inhaltsbibliothek auf das gleiche Speichervolume wie für Ihre Paketquellen verschieben, können Sie dieses Volume nicht für die Datendeduplizierung markieren. Während die Inhaltsbibliothek Datendeduplizierung unterstützt, ist dies beim Volume mit Paketquellen nicht der Fall. Weitere Informationen finden Sie unter [Datendeduplizierung](../configs/support-for-windows-features-and-networks.md#bkmmk_datadedup).<!--SCCMDOcs issue #831-->  

### <a name="prerequisites"></a>Voraussetzungen  

- Das Computerkonto des Standortservers muss über die Berechtigung **Vollzugriff** für den Netzwerkpfad verfügen, auf den Sie die Inhaltsbibliothek verschieben. Diese Berechtigung gilt sowohl für die Freigabe als auch für das Dateisystem. Auf dem Remotesystem werden keine Komponenten installiert.

- Der Standardserver darf nicht über die Verteilungspunktrolle verfügen. Der Verteilungspunkt verwendet ebenfalls die Inhaltsbibliothek, und diese Rolle unterstützt keine Remoteinhaltsbibliothek. Nachdem die Inhaltsbibliothek verschoben wurde, können Sie die Verteilungspunktrolle nicht mehr zum Standortserver hinzufügen.  

- Das Remotesystem für die Inhaltsbibliothek muss sich in einer vertrauenswürdigen Domäne befinden.

> [!Important]  
> Verwenden Sie einen freigegebenen Netzwerkspeicherort nicht erneut für mehrere Standorte. Verwenden Sie beispielsweise nicht denselben Pfad für einen Standort der zentralen Verwaltung und einen untergeordneten primären Standort. Diese Konfiguration könnte die Inhaltsbibliothek beschädigen, und Sie müssten diese neu erstellen.<!--SCCMDocs-pr issue 2764-->  

### <a name="process-to-manage-the-content-library"></a>Verwalten der Inhaltsbibliothek

1. Erstellen Sie einen Ordner in einer Netzwerkfreigabe als Ziel für die Inhaltsbibliothek. Beispiel: `\\server\share\folder`.  

    > [!Warning]  
    > Verwenden Sie einen vorhandenen Ordner mit Inhalt nicht erneut. Verwenden Sie beispielsweise nicht den gleichen Ordner wie für Ihre Paketquellen. Vor dem Kopieren der Inhaltsbibliothek entfernt der Configuration Manager alle vorhandenen Inhalte aus dem von Ihnen angegebenen Speicherort.  

2. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**. Erweitern Sie die **Standortkonfiguration**, und wählen Sie den Knoten **Standorte** und danach den Standort aus. Auf der Registerkarte **Zusammenfassung** am Ende des Detailbereichs erscheint eine neue Spalte für die **Inhaltsbibliothek**.  

3. Wählen Sie auf dem Menüband **Inhaltsbibliothek verwalten** aus.  

4. Das Fenster „Inhaltsbibliothek verwalten“ zeigt im Feld **Aktueller Pfad** das lokale Laufwerk und den Pfad an. Geben Sie einen gültigen Netzwerkpfad für **Neuer Speicherort** an. Dieser Pfad ist der Speicherort, auf den die Inhaltsbibliothek verschoben wird. Er muss einen Ordnernamen enthalten, der bereits auf der Freigabe vorhanden ist, beispielsweise `\\server\share\folder`. Klicken Sie auf **OK**.  

5. Beachten Sie den Wert **Status** in der Spalte „Inhaltsbibliothek“ auf der Registerkarte „Zusammenfassung“ im Detailbereich. Sie zeigt den aktuellen Fortschritt des Standorts beim Verschieben der Inhaltsbibliothek an.  

   - Während der Phase **In Bearbeitung** zeigt der Wert für **Fortschritt der Verschiebung (%)** an, in wieweit der Vorgang bereits prozentual abgeschlossen ist.  

        > [!Note]  
        > Wenn Ihre Inhaltsbibliothek groß ist, sehen Sie den Status `0%` möglicherweise eine ganze Zeit lang. Bei einer Bibliothek von 1 TB müssen beispielsweise 10 GB kopiert werden, bevor `1%` angezeigt wird. Überprüfen Sie **distmgr.log**, dort können Sie die Anzahl der kopierten Dateien und Bytes ersehen. Ab Version 1810 zeigt die Protokolldatei außerdem eine Schätzung der verbleibenden Zeit.

   - Wenn ein Fehler auftritt, zeigt der Status den Fehler an. Häufige Fehler sind **Zugriff verweigert** oder **Datenträger voll**.  

   - Nach dem vollständigen Verschieben wird **Abgeschlossen** angezeigt.  

     In **distmgr.log** finden Sie weitere Einzelheiten. Weitere Informationen finden Sie unter [Protokolle für Standortserver und Standortsystemserver](log-files.md#BKMK_SiteSiteServerLog).  

Weitere Informationen zu diesem Prozess finden Sie unter [Flussdiagramm – Verwalten der Inhaltsbibliothek](manage-content-library-flowchart.md).

Der Standort *kopiert* in Wirklichkeit die Dateien der Inhaltsbibliothek auf den Remotestandort. Bei diesem Vorgang werden die Dateien der Inhaltsbibliothek am ursprünglichen Speicherort auf dem Standortserver nicht gelöscht. Um Speicherplatz freizugeben, muss ein Administrator diese Originaldateien manuell löschen.

Wenn sich die ursprüngliche Inhaltsbibliothek über zwei Laufwerke erstreckt, wird sie am neuen Zielort in einem Ordner zusammengeführt.

Ab Version 1810 verarbeiten die Komponenten **Despooler** und **Verteilungs-Manager** während des Kopiervorgangs keine neuen Pakete. Dadurch wird sichergestellt, dass der Bibliothek während ihrer Verschiebung keine Inhalte hinzugefügt werden. Unabhängig davon sollten Sie diese Änderung während einer Systemwartung planen.

Wenn Sie die Inhaltsbibliothek wieder zurück auf den Standortserver verschieben müssen, wiederholen Sie den hier beschriebenen Vorgang. Wählen Sie dieses Mal jedoch ein lokales Laufwerk und einen lokalen Pfad für die Option **Neuer Speicherort** aus. Er muss einen Ordnernamen enthalten, der bereits auf dem Laufwerk vorhanden ist, beispielsweise `D:\SCCMContentLib`. Wenn der ursprüngliche Inhalt noch vorhanden ist, verschiebt der Prozess einfach die Konfiguration vom lokalen Speicherort auf den Standortserver.

> [!Tip]  
> Verwenden Sie das Tool zum Übertragen der Inhaltsbibliothek (**Content Library Transfer**), um den Inhalt auf ein anderes Laufwerk auf dem Standortserver zu verschieben. Weitere Informationen finden Sie unter [Content Library Transfer Tool (Tool für die Inhaltsbibliotheksübertragung)](../../support/content-library-transfer.md).  


## <a name="inside-the-content-library"></a>Inhalt der Inhaltsbibliothek

> [!Warning]  
> Der folgende Abschnitt wird nur zu Informationszwecken bereitgestellt. Sie dürfen keine Dateien oder Ordner in der Inhaltsbibliothek verändern, zu dieser hinzufügen oder aus ihr entfernen. Andernfalls könnten Pakete, Inhalte oder die Inhaltsbibliothek als Ganzes beschädigt werden. Wenn Sie den Eindruck haben, dass Daten fehlen, beschädigt sind oder anderweitig ungültig sind, verwenden Sie das Feature zur Validierung in der Configuration Manager-Konsole, um derartige Probleme zu erkennen. Verteilen Sie dann den betroffenen Inhalt neu, um die Probleme zu beheben.

Standardmäßig befindet sich die Inhaltsbibliothek im Stammverzeichnis eines Laufwerks in einem Ordner namens **SCCMContentLib**. Dieser Ordner ist standardmäßig als **SCCMContentLib$** freigegeben. Der Ordner und die Freigabe haben eingeschränkte Berechtigungen, um eine versehentliche Beschädigung zu verhindern. Sämtliche Änderungen sollten über die Configuration Manager-Konsole vorgenommen werden. In diesem Ordner befinden sich die folgenden Objekte:  

- Die Paketbibliothek (Ordner **PkgLib**): Informationen dazu, welche Pakete auf dem Verteilungspunkt vorhanden sind.  

- Die Datenbibliothek (Ordner **DataLib**): Informationen über die ursprüngliche Struktur der Pakete.  

- Die Dateibibliothek (Ordner **FileLib**): Die ursprünglichen Dateien im Paket. Dieser Ordner wird in der Regel für den Großteil der zu speichernden Daten verwendet.  

![Übersichtsdiagramm zur Inhaltsbibliothek von Configuration Manager](media/content-library-overview.png)

> [!Tip]  
> Verwenden Sie das Tool **Content Library Explorer** der Configuration Manager-Tools, um den Inhalt der Inhaltsbibliothek zu durchsuchen. Mit diesem Tool können Sie jedoch keine Inhalte ändern. Es gibt einen Einblick in die vorhandenen Inhalte und ermöglicht die Validierung und Neuverteilung. Weitere Informationen finden Sie unter [Content Library Explorer](../../support/content-library-explorer.md).  

### <a name="package-library"></a>Paketbibliothek

Der Ordner der Paketbibliothek, **PkgLib**, enthält eine Datei für jedes Paket, das an den Verteilungspunkt verteilt wurde. Der Dateiname entspricht der Paket-ID, beispielsweise `ABC00001.INI`. In dieser Datei befinden sich im Abschnitt `[Packages]` neben einer Liste der Inhalts-IDs, die Bestandteil des Pakets sind, weitere Informationen wie beispielsweise die Version. **ABC00001** ist beispielsweise ein Legacypaket mit Version **1**. Die Inhalts-ID dieser Datei lautet `ABC00001.1`.

### <a name="data-library"></a>Datenbibliothek

Der Ordner für die Datenbibliothek, **DataLib**, enthält eine Datei und einen Ordner für jeden Inhalt der einzelnen Pakete. Diese Datei und der Ordner haben beispielsweise den Namen `ABC00001.1.INI` bzw. `ABC00001.1`. Die Datei enthält Informationen zur Validierung. Der Ordner erstellt die Ordnerstruktur aus dem ursprünglichen Paket neu.

Die Dateien in der Datenbibliothek werden durch INI-Dateien mit dem Namen der ursprünglichen Datei im Paket ersetzt. Beispiel: `MyFile.exe.INI`. Diese Dateien enthalten Informationen über die ursprüngliche Datei wie Größe, Uhrzeit der Änderung und Hash. Verwenden Sie die ersten vier Zeichen des Hashs, um die ursprüngliche Datei in der Dateibibliothek zu suchen. Der Hash in MyFile.exe.INI lautet beispielsweise **DEF98765**, und die ersten vier Zeichen lauten **DEF9**.

### <a name="file-library"></a>Dateibibliothek

Wenn die Inhaltsbibliothek auf mehrere Laufwerke aufgeteilt ist, befinden sich die Paketdateien möglicherweise im Dateibibliotheksordner **FileLib** auf einem dieser Laufwerke.

Sie suchen nach einer bestimmten Datei, indem Sie die ersten vier Zeichen des in der Datenbibliothek gefundenen Hashs verwenden. Im Dateibibliotheksordner befindet sich zahlreiche Ordner mit einem jeweils aus vier Zeichen bestehenden Namen. Suchen Sie den Ordner, der den ersten vier Zeichen des Hashs entspricht. Dieser Ordner enthält einen oder mehrere Sätze von drei Dateien. Diese Dateien haben denselben Namen, eine der Dateien hat jedoch die Erweiterung INI, die zweite hat die Erweiterung SIG und die dritte Datei weist keine Dateierweiterung auf. Die ursprüngliche Datei ist die Datei ohne Erweiterung, deren Name mit dem Hash aus der Datenbibliothek übereinstimmt.

Der Ordner **DEF9** umfasst beispielsweise `DEF98765.INI`, `DEF98765.SIG` und `DEF98765`. `DEF98765` ist die ursprüngliche `MyFile.exe`. Die INI-Datei enthält eine Liste von „Benutzern“ oder Inhalts-IDs, die sich dieselbe Datei teilen. Der Standort entfernt eine Datei nicht, es sei denn, es werden auch alle diese Inhalte entfernt.

### <a name="drive-spanning"></a>Aufteilung auf mehrere Laufwerke

Die Inhaltsbibliothek kann auf mehrere Laufwerke aufgeteilt sein. Sie wählen diese Laufwerke aus, wenn Sie den Verteilungspunkt erstellen. Standardmäßig wählt Configuration Manager automatisch die Laufwerke aus, wenn die Inhaltsbibliothek aufgeteilt wird.

Wenn Sie die Laufwerke auswählen, wählen Sie ein primäres und ein sekundäres Laufwerk aus. Der Standort speichert alle Metadaten auf dem primären Laufwerk. Die Dateibibliothek erstreckt sich dabei nur auf das sekundäre Laufwerk. Der Freigabename des Ordners für sekundäre Laufwerke umfasst den Laufwerkbuchstaben. Wenn D: und E: beispielsweise sekundäre Laufwerke für die Inhaltsbibliothek sind, lauten die Freigabenamen **SCCMContentLibD$** und **SCCMContentLibE$** .

Wenn Sie die Option **Automatisch** auswählen, wählt Configuration Manager das Laufwerk mit dem meisten verfügbaren freien Speicherplatz als primäres Laufwerk aus. Alle Metadaten werden auf diesem Laufwerk gespeichert. Der Standort teilt die Dateibibliothek somit nur auf sekundäre Laufwerke auf.

Während der Konfiguration geben Sie einen Wert für den Reservespeicher an. Configuration Manager versucht, ein sekundäres Laufwerk zu verwenden, wenn auf dem besten verfügbaren Laufwerk nur noch dieser Reservespeicherplatz frei ist. Bei jeder Auswahl eines neuen zu verwendenden Laufwerks wird das Laufwerk mit dem meisten verfügbaren freien Speicherplatz ausgewählt.

Sie können nicht angeben, dass ein Verteilungspunkt alle Laufwerke mit Ausnahme einer bestimmten Gruppe verwenden soll. Sie können dieses Verhalten verhindern, indem Sie im Stammverzeichnis des Laufwerks eine leere Datei namens `NO_SMS_ON_DRIVE.SMS` erstellen. Erstellen Sie diese Datei, bevor Configuration Manager das Laufwerk für die Verwendung auswählt. Wenn Configuration Manager diese Datei im Stammverzeichnis des Laufwerks erkennt, verwendet er das Laufwerk nicht für die Inhaltsbibliothek.


## <a name="troubleshooting"></a>Problembehandlung

Die folgenden Tipps können Ihnen beim Beheben von Problemen mit der Inhaltsbibliothek helfen:  

- Überprüfen Sie die Protokolle auf dem Standortserver (**distmgr.log** und **PkgXferMgr.log**) und auf dem Verteilungspunkt (**smsdpprov.log**) auf etwaige Verweise auf Fehler.  

- Verwenden Sie das Tool [Content Library Explorer](../../support/content-library-explorer.md).  

- Prüfen Sie, ob Dateien durch andere Prozesse gesperrt sind, beispielsweise durch Antivirussoftware. Schließen Sie die Inhaltsbibliothek auf allen Laufwerken von automatischen Virenprüfungen aus. Schließen Sie ferner das temporäre Stagingverzeichnis **SMS_DP$** auf allen Laufwerken aus.  

- Um festzustellen, ob Hashkonflikte vorliegen, überprüfen Sie das Paket von der Configuration Manager-Konsole.  

- Verteilen Sie als letzte Möglichkeit zur Problembehebung den Inhalt erneut. Dadurch sollten die meisten Probleme beheben werden.  

Ausführlichere Informationen finden Sie unter [Grundlegendes zur Inhaltsverteilung in Configuration Manager und Fehlerbehebung](https://support.microsoft.com/help/4482728/understand-troubleshoot-content-distribution-in-configuration-manager).
