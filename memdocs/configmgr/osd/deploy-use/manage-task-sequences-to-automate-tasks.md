---
title: Verwalten von Tasksequenzen
titleSuffix: Configuration Manager
description: Sie können Tasksequenzen erstellen, bearbeiten, bereitstellen, importieren und exportieren, um sie zu verwalten und Tasks in Ihrer Umgebung zu automatisieren.
ms.date: 02/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: a1f099f1-e9b5-4189-88b3-f53e3b4e4add
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b38b0c8f28645fa0aae66058b0c93bd8beffc470
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078480"
---
# <a name="manage-task-sequences-to-automate-tasks"></a>Verwalten von Tasksequenzen zum Automatisieren von Tasks

*Gilt für: Configuration Manager (Current Branch)*

Verwenden Sie Tasksequenzen, um Schritte in Ihrer Configuration Manager-Umgebung zu automatisieren. Zu diesen Schritten gehören die Bereitstellung eines Betriebssystemimages für einen Zielcomputer, das Erstellen und Erfassen eines Betriebssystemimages aus mehreren Betriebssystem-Installationsdateien sowie das Erfassen und Wiederherstellen von Benutzerstatusinformationen. Tasksequenzen befinden sich in der Configuration Manager-Konsole. Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Tasksequenzen**. Der Knoten **Tasksequenzen** mit den erstellten Unterordnern wird in der gesamten Configuration Manager-Hierarchie repliziert. Planungsinformationen finden Sie unter [Planungsüberlegungen für das Automatisieren von Tasks](../plan-design/planning-considerations-for-automating-tasks.md).  

## <a name="create"></a><a name="BKMK_CreateTaskSequence"></a> Erstellen

Erstellen Sie Tasksequenzen mithilfe des Tasksequenzerstellungs-Assistenten. Mit diesem Assistenten können Sie die folgenden Typen von Tasksequenzen erstellen:  

- [Tasksequenz zum Installieren eines Betriebssystems:](create-a-task-sequence-to-install-an-operating-system.md) In diesem Fall werden die Schritte zum Installieren eines Betriebssystems erstellt. Er enthält auch Optionen zum Migrieren von Benutzerdaten, einschließen Softwareupdates, und zum Installieren von Anwendungen.

- [Tasksequenz zum Durchführen eines Betriebssystemupgrades:](create-a-task-sequence-to-upgrade-an-operating-system.md) In diesem Fall werden die Schritte zum Durchführen eines Betriebssystemupgrades erstellt. Er enthält auch Optionen zum Einschließen von Softwareupdates, und zum Installieren von Anwendungen.

- [Tasksequenz zum Erfassen eines Betriebssystems](create-a-task-sequence-to-capture-an-operating-system.md): Erstellen Sie die Schritte zum Erstellen und Erfassen eines Betriebssystems auf einem Referenzcomputer. Sie können Softwareupdates einschließen und Anwendungen auf dem Referenzcomputer installieren, bevor Sie das Image erfassen.

- [Tasksequenz zum Erfassen und Wiederherstellen des Benutzerzustands:](create-a-task-sequence-to-capture-and-restore-user-state.md) In diesem Fall werden einer vorhandenen Tasksequenz Schritte zum Erfassen und Wiederherstellen von Benutzerzustandsdaten hinzugefügt.

- [Benutzerdefinierte Tasksequenz](create-a-custom-task-sequence.md): Dieser Tasksequenztyp fügt der Tasksequenz keine Schritte hinzu. Nachdem Sie diese Tasksequenz erstellt haben, bearbeiten Sie diese und fügen Schritte hinzu.

## <a name="edit"></a><a name="BKMK_ModifyTaskSequence"></a> Bearbeiten  

Ändern Sie eine Tasksequenz, indem Sie ihr Schritte oder Gruppen hinzufügen bzw. diese aus ihr entfernen oder die Reihenfolge der Schritte ändern. Weitere Informationen finden Sie unter [Verwenden des Tasksequenz-Editors](../understand/task-sequence-editor.md).

## <a name="software-center-properties"></a><a name="bkmk_prop-general"></a> Eigenschaften des Softwarecenters

Gehen Sie wie folgt vor, um die Angaben für die Tasksequenz, die im Softwarecenter angezeigt werden, zu konfigurieren. Diese Angaben dienen nur zu Informationszwecken.  

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie anschließend auf **Tasksequenzen**.  

2. Wählen Sie die zu bearbeitende Tasksequenz und anschließend die Option **Eigenschaften** aus.  

3. Auf der Registerkarte **Allgemein** stehen folgende neuen Einstellungen für das Softwarecenter zur Verfügung:  

    - **Neustart erforderlich:** Informiert den Benutzer, ob während der Installation ein Neustart erforderlich ist.  

    - **Downloadgröße (MB):** Gibt an, wie viele Megabytes für die Tasksequenz im Softwarecenter angezeigt werden.  

    - **Geschätzte Laufzeit (Min.):** Gibt die geschätzte Laufzeit in Minuten an, die für die Tasksequenz im Softwarecenter angezeigt wird.  

## <a name="advanced-settings"></a><a name="bkmk_prop-advanced"></a> Erweiterte Einstellungen

Verwenden Sie die folgende Vorgehensweise, um das Verhalten der Tasksequenz im Configuration Manager-Client zu konfigurieren.  

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie anschließend auf **Tasksequenzen**.  

2. Wählen Sie die zu bearbeitende Tasksequenz und anschließend die Option **Eigenschaften** aus.  

3. Auf der Registerkarte **Erweitert** sind die folgenden Einstellungen verfügbar:  

    - **Ein anderes Programm zuerst ausführen**: Wählen Sie diese Option aus, um ein Programm in einem anderen Paket auszuführen, bevor die Tasksequenz ausgeführt wird. Standardmäßig ist dieses Kontrollkästchen deaktiviert. Das zuerst auszuführende Programm muss nicht gesondert bereitgestellt werden.  

        > [!IMPORTANT]
        > Diese Einstellung gilt nur für Tasksequenzen, die auf dem vollständigen Betriebssystem ausgeführt werden. Wenn Sie die Tasksequenz mithilfe von PXE oder Startmedien starten, wird diese Einstellung von Configuration Manager ignoriert.  

        - **Paket**: Suchen Sie nach dem Paket mit dem Programm, das vor dieser Tasksequenz ausgeführt werden soll.  

        - **Programm**: Wählen Sie das Programm aus, das vor dieser Tasksequenz ausgeführt werden soll.  

        > [!NOTE]  
        > Wenn das ausgewählte Programm auf einem Client nicht ausgeführt werden kann, wird die Tasksequenz nicht ausgeführt. Bei erfolgreicher Ausführung des ausgewählten Programms wird dieses auch bei erneuter Ausführung der Tasksequenz auf demselben Client nicht erneut ausgeführt.  

    - **Tasksequenzbenachrichtigungen unterdrücken:** Aktivieren Sie diese Option, um die Popupbenachrichtigung **Neue Software ist verfügbar** auszublenden. Das Symbol **Neue Software** des Softwarecenters wird weiterhin im Infobereich angezeigt. Diese Option ist standardmäßig deaktiviert.  

    - **Diese Tasksequenz auf Computern, auf denen sie bereitgestellt ist, deaktivieren**: Wenn Sie diese Option auswählen, deaktiviert Configuration Manager vorübergehend alle Bereitstellungen, die diese Tasksequenz enthalten. Zudem entfernt es die Tasksequenz aus der Liste der verfügbaren ausführbaren Bereitstellungen. Die Tasksequenz wird erst ausgeführt, wenn Sie sie aktivieren. Diese Option ist standardmäßig deaktiviert.  

    - **Maximal zulässige Laufzeit**: Gibt die maximale Zeit (in Minuten) an, die für die Ausführung der Tasksequenz auf dem Zielcomputer erwartet wird. Verwenden Sie eine ganze Zahl, die gleich oder größer als null ist. Standardmäßig ist dieser Wert auf 120 Minuten festgelegt.  

        > [!IMPORTANT]  
        > Wenn Sie bei der Sammlung, für die diese Tasksequenz bereitgestellt wird, Wartungsfenster verwenden, kann ein Konflikt auftreten, wenn die **Maximal zulässige Laufzeit** länger ist als das geplante Wartungsfenster. Wenn Sie die maximal zulässige Laufzeit auf **0** festlegen, wird die Tasksequenz innerhalb des Wartungsfensters gestartet. Sie wird solange ausgeführt, bis sie abgeschlossen ist oder nach dem Schließen des Wartungsfensters fehlschlägt. Entsprechend werden Tasksequenzen, bei denen für die maximal zulässige Laufzeit der Wert **0** festgelegt ist, möglicherweise über das Ende ihrer Wartungsfenster hinaus ausgeführt. Wenn Sie für die maximal zulässige Laufzeit einen bestimmten Zeitraum (nicht 0) festlegen, der die Dauer aller verfügbaren Wartungsfenster überschreitet, wird diese Tasksequenz nicht ausgeführt. Weitere Informationen finden Sie unter [Verwenden von Wartungsfenstern](../../core/clients/manage/collections/use-maintenance-windows.md).  

        Wenn Sie den Wert auf **0** festlegen, verwendet Configuration Manager als maximal zulässige Laufzeit **12** Stunden (720 Minuten) für die Überwachung des Fortschritts. Allerdings wird die Tasksequenz gestartet, solange die Dauer des Countdowns den Wert für das Wartungsfenster nicht überschreitet.  

        > [!NOTE]
        > Wenn sie die maximale Runtime erreicht und Sie nicht zulassen, dass Benutzer mit einer erforderlichen Bereitstellung interagieren, wird die Tasksequenz von Configuration Manager beendet. Wenn die Tasksequenz selbst nicht beendet wird, beendet Configuration Manager die Überwachung der Tasksequenz, sobald es die maximal zulässige Laufzeit erreicht.

    - **Startimage verwenden**: Bei dieser Option verwenden Sie das ausgewählte Startimage, wenn die Tasksequenz ausgeführt wird. Wählen Sie **Durchsuchen** aus, um ein anderes Startimage auszuwählen. Deaktivieren Sie diese Option, um bei der Ausführung der Tasksequenz die Verwendung des ausgewählten Startimages zu deaktivieren.  

    - **Diese Tasksequenz kann auf jeder Plattform ausgeführt werden**: Wenn Sie diese Option auswählen, überprüft Configuration Manager nicht den Plattformtyp des Zielcomputers beim Ausführen der Tasksequenz. Diese Option ist standardmäßig ausgewählt.  

    - **Diese Tasksequenz kann nur auf den angegebenen Clientplattformen ausgeführt werden**: Mit dieser Option werden die Prozessoren, Betriebssystemversionen und Service Packs angegeben, mit denen diese Tasksequenz ausgeführt werden kann. Wenn Sie diese Option auswählen, wählen Sie mindestens eine Plattform aus der Liste aus. Standardmäßig ist keine Plattform ausgewählt. Configuration Manager bewertet mithilfe dieser Informationen, welche Zielcomputer in einer Sammlung die bereitgestellte Tasksequenz erhalten sollen.  

        > [!NOTE]  
        > Beim Ausführen einer Tasksequenz über Startmedien oder PXE ignoriert Configuration Manager diese Option. Die Tasksequenz wird ausgeführt, als ob die Option **Dieses Programm kann auf jeder Plattform ausgeführt werden.** ausgewählt ist.  

## <a name="high-impact-settings"></a>Einstellungen mit hoher Auswirkung

Konfigurieren Sie eine Tasksequenz als Tasksequenz mit schwerwiegenden Auswirkungen, und passen Sie die Meldungen an, die Benutzer erhalten, wenn sie die Tasksequenz ausführen.

> [!WARNING]
> Wenn Sie PXE-Bereitstellungen verwenden und Gerätehardware mit dem Netzwerkadapter als erstes Startgerät konfigurieren, können diese Geräte automatisch und ohne Benutzerinteraktion eine Tasksequenz für die Betriebssystembereitstellung starten. Diese Konfiguration wird nicht durch die Bereitstellungsüberprüfung verwaltet. Während diese Konfiguration möglicherweise den Prozess vereinfachen und die Benutzerinteraktion reduzieren kann, erhöht sie das Risiko, dass für das Gerät versehentlich ein Reimaging durchgeführt wird.

### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Festlegen einer Tasksequenz als Tasksequenz mit schwerwiegenden Auswirkungen

Gehen Sie wie folgt vor, um eine Tasksequenz als Tasksequenz mit schwerwiegenden Auswirkungen festzulegen:

> [!NOTE]  
> Jede Tasksequenz, die bestimmte Bedingungen erfüllt, wird automatisch als „high-impact“ (mit schwerwiegenden Auswirkungen) definiert. Weitere Informationen finden Sie unter [Verwalten risikoreicher Bereitstellungen](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie anschließend auf **Tasksequenzen**.  

2. Wählen Sie die zu bearbeitende Tasksequenz und anschließend die Option **Eigenschaften** aus.  

3. Wählen Sie in der Registerkarte **Benutzerbenachrichtigung** **Dies ist eine Tasksequenz mit schwerwiegenden Auswirkungen** aus.  

### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Erstellen einer benutzerdefinierten Benachrichtigung für risikoreiche Bereitstellungen

Verwenden Sie die folgende Prozedur, um eine benutzerdefinierte Benachrichtigung zu Bereitstellungen mit schwerwiegenden Auswirkungen zu erstellen.

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie anschließend auf **Tasksequenzen**.  

2. Wählen Sie die zu bearbeitende Tasksequenz und anschließend die Option **Eigenschaften** aus.  

3. Wählen Sie in der Registerkarte **Benutzerbenachrichtigung** **Benutzerdefinierten Text verwenden** aus.  

    > [!NOTE]
    > Sie können den Text von Benutzerbenachrichtigungen nur festlegen, wenn Sie die Option **Dies ist eine Tasksequenz mit schwerwiegenden Auswirkungen** auswählen.  

4. Konfigurieren Sie die folgenden Einstellungen:  

    > [!Note]  
    > Jedes Textfeld weist einen maximalen Grenzwert von 255 Zeichen auf.  

    - **Überschriftentext für Benutzerbenachrichtigung**: Gibt den blauen Text an, der in der Benutzerbenachrichtigung vom Softwarecenter angezeigt wird. In der Standardbenutzerbenachrichtigung enthält dieser Abschnitt den folgenden Text: „Bestätigen Sie, dass Sie das Betriebssystem auf diesem Computer aktualisieren möchten.“.  

    - **Text der Benutzerbenachrichtigung**: Es gibt drei Textfelder, die den Text der benutzerdefinierten Benachrichtigungen enthalten. Sie müssen in jedes Textfeld Text eingeben.  

        - Erstes Textfeld: Gibt den Hauptteil des Texts an, der üblicherweise Anweisungen an den Benutzer enthält. In der Standardbenutzerbenachrichtigung enthält dieser Abschnitt den folgenden Text: „Upgrading the operating system takes time and your computer might restart several times.“ (Das Upgrade des Betriebssystems kann einige Zeit dauern und mehrere Neustarts des Computers erfordern.).  

        - Zweites Textfeld: Gibt den fettmarkierten Text unterhalb des Hauptteils an. In der Standardbenutzerbenachrichtigung enthält dieser Abschnitt den folgenden Text: „Dieses direkte Upgrade installiert das neue Betriebssystem und führt eine automatische Migration Ihrer Apps, Daten und Einstellungen durch.“.  

        - Drittes Textfeld: Gibt die letzte Textzeile unterhalb des fettmarkierten Texts an. In der Standardbenutzerbenachrichtigung enthält dieser Abschnitt den folgenden Text: „Klicken Sie zum Beginnen auf „Installieren“. Klicken Sie andernfalls auf Abbrechen.“  

#### <a name="example"></a>Beispiel

Angenommen, Sie konfigurieren folgende benutzerdefinierte Benachrichtigung in den Eigenschaften.

![Registerkarte für benutzerdefinierte Benachrichtigung der Tasksequenzeigenschaften](../media/user-notification.png)

Folgende Benachrichtigung wird angezeigt, wenn der Endbenutzer die Installation im Softwarecenter öffnet.

![Benutzerdefinierte Tasksequenzbenachrichtigung für den Endbenutzer im Softwarecenter](../media/user-notification-enduser.png)

## <a name="performance-improvements-for-power-plans"></a><a name="bkmk_perf"></a> Leistungsverbesserungen bei Energiesparplänen

<!--3555926-->

Ab Version 1910 können Sie eine Tasksequenz jetzt mit dem Hochleistungs-Energiesparplan ausführen. Diese Option verbessert die Gesamtgeschwindigkeit der Tasksequenz. Windows wird zur Verwendung des integrierten Hochleistungs-Energiesparplans konfiguriert, der maximale Leistung auf Kosten eines höheren Energieverbrauchs bietet. Diese Option ist für neue Tasksequenzen standardmäßig aktiviert.

Wenn die Tasksequenz startet, wird in den meisten Fällen der aktuell aktivierte Energiesparplan aufgezeichnet. Dann wird der aktive Energiesparplan auf den Windows-Standardplan **Höchstleistung** umgestellt. Wenn die Tasksequenz den Computer neu startet, wird dieser Vorgang wiederholt. Am Ende der Tasksequenz wird der Energiesparplan auf den gespeicherten Wert zurückgesetzt. Diese Funktionalität steht sowohl in Windows als auch in Windows PE zur Verfügung, hat aber keine Auswirkung auf VMs.

- Wenn die Tasksequenz unter Windows PE gestartet wird, zeichnet die Tasksequenz den derzeit aktivierten Energiesparplan nicht für eine spätere Wiederverwendung auf.

- Eine Tasksequenz für die Betriebssystembereitstellung, die ein Reimaging des Computers durchführt (Zurücksetzen und Laden), behält die Einstellung für den Energiesparplan des alten Betriebssystems nicht bei. Am Ende der Tasksequenz wird der Standardenergiesparplan **Ausgeglichen** wiederhergestellt.

> [!Important]
> Um dieses neue Configuration Manager-Features zu nutzen, müssen Sie nach dem Aktualisieren des Standorts auch die Clients auf die neueste Version aktualisieren. Aktualisieren Sie außerdem die Startimages, um die neuesten Clientkomponenten einzuschließen. Beim Update des Standorts und der Konsole werden neue Features in der Configuration Manager-Konsole angezeigt. Das vollständige Szenario ist allerdings erst einsatzbereit, wenn auch die Clientversion aktualisiert wird.

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**. Erweitern Sie **Betriebssystem**, und wählen Sie den Knoten **Tasksequenzen** aus.

1. Erstellen Sie eine Tasksequenz, oder wählen Sie eine vorhandene Tasksequenz aus, und klicken Sie dann auf **Eigenschaften**.

1. Wechseln Sie zur Registerkarte **Leistung**.

1. Aktivieren Sie die Option **Als Hochleistungs-Energiesparplan ausführen**.

> [!Warning]
> Setzen Sie diese Einstellung auf Hardware mit niedriger Leistung vorsichtig ein. Die Ausführung leistungsintensiver Systemvorgänge über einen längeren Zeitraum kann Low-End-Hardware überlasten. Lassen Sie sich von Ihrem Hardwarehersteller beraten.

### <a name="known-issue"></a>Bekanntes Problem

<!-- 5554928 -->

Sie müssen eine neue Tasksequenzbereitstellung erstellen, um diese Hochleistungseinstellung zu aktivieren oder zu deaktivieren. Die neue Einstellung wird in vorhandenen Bereitstellungen zwar angezeigt, kann jedoch nicht darauf angewendet werden.<!-- SCCMDocs#2107 -->

## <a name="distribute-referenced-content"></a><a name="BKMK_DistributeTS"></a> Verteilen von referenziertem Inhalt  

Verteilen Sie den Inhalt, auf den von einer Tasksequenz verwiesen wird, an Verteilungspunkte, bevor diese Tasksequenz von Clients ausgeführt wird. Sie können die Tasksequenz jederzeit auswählen und ihren Inhalt verteilen, um eine neue Liste von Referenzpaketen für die Verteilung zu erstellen. Wenn Sie die Tasksequenz mit aktualisiertem Inhalt ändern, verteilen Sie den Inhalt erneut, bevor er für Clients verfügbar ist. Gehen Sie wie folgt vor, um den Inhalt, auf den von einer Tasksequenz verwiesen wird, zu verteilen.  

### <a name="process-to-distribute-referenced-content-to-distribution-points"></a>Vorgang zum Verteilen von referenziertem Inhalt an Verteilungspunkte  

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und wählen Sie anschließend den Knoten **Tasksequenzen** aus.  

2. Wählen Sie in der Liste **Tasksequenz** die Tasksequenz aus, die Sie verteilen möchten.  

3. Wählen Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Bereitstellung** die Option **Inhalt verteilen** aus. Mit dieser Aktion wird der Assistent für die Verteilung von Inhalt gestartet.  

4. Vergewissern Sie sich auf der Seite **Allgemein**, dass die richtige Tasksequenz für die Verteilung ausgewählt ist.  

5. Überprüfen Sie auf der Seite **Inhalt** den zu verteilenden Inhalt, z. B. das Startimage, auf das von der Tasksequenz verwiesen wird.  

6. Geben Sie auf der Seite **Inhaltsziel** die Sammlungen, den Verteilungspunkt oder die Verteilungspunktgruppe an, an die der Inhalt der Tasksequenz verteilt werden soll.  

    > [!IMPORTANT]  
    > Wenn von der ausgewählten Tasksequenz auf Inhalt verwiesen wird, der bereits an einen bestimmten Verteilungspunkt verteilt wurde, führt der Assistent nicht den betreffende Verteilungspunkt auf.  

7. Schließen Sie den Assistenten ab.  

Sie können den Inhalt, auf den in der Tasksequenz verwiesen wird, auch vorab bereitstellen. Configuration Manager erstellt eine komprimierte, vorab bereitgestellte Inhaltsdatei, die die Dateien, zugeordnete Abhängigkeiten und zugeordnete Metadaten für den von Ihnen ausgewählten Inhalt umfasst. Importieren Sie den Inhalt dann manuell auf einen Standortserver, an einen sekundären Standort oder einen Verteilungspunkt. Weitere Informationen zum Vorabbereitstellen von Inhaltsdateien finden Sie unter [Vorabbereitstellen von Inhalt](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  

## <a name="deploy"></a><a name="BKMK_DeployTS"></a> Bereitstellen  

Weitere Informationen finden Sie unter [Deploy a task sequence](deploy-a-task-sequence.md).

## <a name="export-and-import"></a><a name="BKMK_ExportImport"></a> Exportieren und Importieren  

Exportieren und importieren Sie Tasksequenzen mit den dazugehörigen Objekten oder ohne diese Objekte. Dieser Inhalt, auf den verwiesen wird, enthält die folgenden Objekte:  

- Betriebssystemimages  
- Startabbilder  
- Pakete wie etwa das Clientinstallationspaket  
- Treiberpakete  
- Anwendungen mit Abhängigkeiten  

Beachten Sie beim Exportieren und Importieren von Tasksequenzen die folgenden Punkte:  

- Configuration Manager exportieren keine Kennwörter in der Tasksequenz. Wenn Sie eine Tasksequenz exportieren und importieren, die Kennwörter enthält, bearbeiten Sie die importierte Tasksequenz, um sämtliche Kennwörter erneut einzugeben. Überprüfen Sie die folgenden Schritte, die die Eingabe eines Kennworts umfassen können:  

  - [Einer Domäne oder Arbeitsgruppe beitreten](../understand/task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  
  - [Verbindung mit Netzwerkordner herstellen](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  
  - [Befehlszeile ausführen](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

- Wenn Sie eine Tasksequenz mit dem Schritt **Dynamische Variablen festlegen** exportieren, exportiert Configuration Manager keine Werte für Variablen, die Sie mit der Einstellung **Geheimniswert** konfigurieren. Geben Sie die Werte für diese Variablen erneut ein, nachdem Sie die Tasksequenz importiert haben.  

- Wenn mehrere primäre Standorte vorliegen, importieren Sie Tasksequenzen am Standort der zentralen Verwaltung.  

### <a name="process-to-export-task-sequences"></a>Vorgang zum Exportieren von Tasksequenzen  

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und wählen Sie anschließend den Knoten **Tasksequenzen** aus.  

2. Wählen Sie in der Liste **Tasksequenz** die Tasksequenzen aus, die Sie exportieren möchten. Wenn Sie mehrere Tasksequenzen auswählen, werden diese in einer Exportdatei gespeichert.  

3. Wählen Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Tasksequenz** die Option **Exportieren** aus. Daraufhin wird der Assistent zum Exportieren von Tasksequenzen gestartet.  

4. Geben Sie auf der Seite **Allgemein** die folgenden Einstellungen an:  

    - **Datei:** Geben Sie den Speicherort und den Namen der Exportdatei an. Wenn Sie den Dateinamen direkt eingeben, achten Sie darauf, an den Dateinamen die Erweiterung ZIP anzuhängen. Wenn Sie nach der Exportdatei suchen, wird diese Dateinamenerweiterung vom Assistenten automatisch hinzugefügt.  

    - Wenn Sie keine Tasksequenzabhängigkeiten exportieren möchten, heben Sie die Auswahl für die Option **Alle Tasksequenzabhängigkeiten exportieren** auf. Standardmäßig werden alle zugehörigen Objekte vom Assistenten gesucht und zusammen mit der Tasksequenz exportiert. Dazu gehören alle Abhängigkeiten für Anwendungen.  

    - Wenn Sie den Inhalt nicht von der Paketquelle in den Exportspeicherort kopieren möchten, heben Sie die Auswahl für die Option **Alle Inhalte für die ausgewählten Tasksequenzen und Abhängigkeiten exportieren** auf. Wenn Sie diese Option auswählen, wird der Importpfad vom Assistenten zum Importieren von Tasksequenzen als neuer Paketquellpfad verwendet.  

    - **Administratorkommentare**: Fügen Sie eine Beschreibung der zu exportierenden Tasksequenzen hinzu.  

5. Schließen Sie den Assistenten ab.  

Die folgenden Ausgabedateien werden vom Assistenten erstellt:  

- Wenn Sie keinen Inhalt exportieren, wird eine ZIP-Datei erstellt.  

- Wenn Sie Inhalt exportieren, werden eine ZIP-Datei und ein Ordner namens *Export*_files erstellt. Dabei ist *Export* der Name der ZIP-Datei mit dem exportierten Inhalt.  

Wenn Sie beim Exportieren einer Tasksequenz auch den Inhalt einschließen, müssen Sie die ZIP-Datei und den Ordner „*export*_files“ kopieren. Andernfalls tritt beim Import ein Fehler auf.  

### <a name="process-to-import-task-sequences"></a>Vorgang zum Importieren von Tasksequenzen  

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und wählen Sie anschließend den Knoten **Tasksequenzen** aus.  

2. Wählen Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Erstellen** die Option **Tasksequenz importieren** aus. Daraufhin wird der Assistent zum Importieren von Tasksequenzen gestartet.  

3. Geben Sie auf der Seite **Allgemein** des Menübands die exportierte ZIP-Datei an.  

4. Wählen Sie auf der Seite **Dateiinhalt** für jedes importierte Objekt die gewünschte Aktion aus. Auf dieser Seite werden alle Objekte angezeigt, die Configuration Manager importieren kann.  

    - Wenn ein Objekt noch nie importiert wurde, wählen Sie **Neu erstellen**aus.  

    - Wenn ein Objekt bereits importiert wurde, wählen Sie eine der folgenden Aktionen aus:  

        - **Duplikat ignorieren** (Standard): Bei dieser Aktion wird das Objekt nicht importiert. Stattdessen wird das vorhandene Objekt vom Assistenten mit der Tasksequenz verknüpft.  

        - **Überschreiben**: Diese Aktion überschreibt das vorhandene Objekt mit dem importierten Objekt. Sie können Anwendungen eine Revision hinzufügen, um ein Update der vorhandenen Anwendung auszuführen oder eine neue Anwendung zu erstellen.  

5. Schließen Sie den Assistenten ab.  

Bearbeiten Sie die Tasksequenz nach dem Import, um Kennwörter anzugeben, die bei der ursprünglichen Tasksequenz verwendet wurden. Kennwörter werden aus Sicherheitsgründen nicht exportiert.  

## <a name="return-to-previous-page-on-failure"></a>Bei einem Fehler zurück zur vorherigen Seite

Wenn Sie eine Tasksequenz ausführen und ein Fehler auftritt, können Sie zu einer vorherigen Seite des Tasksequenz-Assistenten zurückkehren. In früheren Versionen von Configuration Manager mussten Sie die Tasksequenz neu starten, wenn ein Fehler auftrat. Verwenden Sie die Schaltfläche **Zurück** in den folgenden Szenarios:

- Beim Starten eines Computers in Windows PE wird möglicherweise der Bootstrap-Dialog der Tasksequenz angezeigt, bevor die Tasksequenz verfügbar ist. Wenn Sie in diesem Szenario „Weiter“ auswählen, wird auf der letzten Seite der Tasksequenz eine Nachricht angezeigt, die darüber informiert, dass es keine verfügbaren Tasksequenzen gibt. Sie können nun **Zurück** auswählen, um erneut nach verfügbaren Tasksequenzen zu suchen. Sie können diesen Vorgang wiederholen, bis die Tasksequenz verfügbar ist.  

- Wenn die abhängigen Inhaltspakete beim Ausführen einer Tasksequenz noch nicht an den Verteilungspunkten verfügbar sind, verursacht die Tasksequenz einen Fehler. Wenn der fehlende Inhalt noch nicht verteilt wurde, können Sie diesen Schritt nun nachholen. Alternativ können Sie auch warten, bis der Inhalt an Verteilungspunkten verfügbar wird. Wählen Sie anschließend **Zurück** aus, damit die Tasksequenz erneut nach dem Inhalt sucht.

## <a name="collection-and-device-variables"></a><a name="BKMK_CreateTSVariables"></a> Sammlungs- und Gerätevariablen

Sie können benutzerdefinierte Tasksequenzvariablen für Computer und Sammlungen definieren. Für einen Computer definierte Variablen werden als computerspezifische Tasksequenzvariablen bezeichnet. Für eine Sammlung definierte Variablen werden als sammlungsspezifische Tasksequenzvariablen bezeichnet. Weitere Informationen finden Sie unter [Sammlungs- und Gerätevariablen](../understand/using-task-sequence-variables.md#bkmk_set-coll-var).

## <a name="additional-actions"></a><a name="BKMK_AdditionalActionsTS"></a> Zusätzliche Aktionen  

Für die Verwaltung von Tasksequenzen können Sie zusätzliche Aktionen verwenden, wenn Sie die Tasksequenz auswählen.  

### <a name="edit"></a>Bearbeiten

Weitere Informationen finden Sie unter [Verwenden des Tasksequenz-Editors](../understand/task-sequence-editor.md#bkmk_edit).

### <a name="enable"></a>Aktivieren Sie

Hiermit wird die Tasksequenz aktiviert, damit Clients sie ausführen können. Es ist nicht notwendig, eine Tasksequenz nach der Aktivierung erneut bereitzustellen.  

### <a name="disable"></a>Deaktivieren

Hiermit wird die Tasksequenz deaktiviert, damit sie nicht auf Computern ausgeführt werden kann. Sie können zwar eine deaktivierte Tasksequenz bereitstellen, aber Computer führen diese erst dann aus, wenn Sie sie aktivieren.  

### <a name="export"></a>Exportieren

Weitere Informationen finden Sie unter [Exportieren und Importieren von Tasksequenzen](#BKMK_ExportImport).

### <a name="copy"></a>Kopieren

Hiermit wird eine Kopie der ausgewählten Tasksequenz erstellt. Diese Aktion ist nützlich, wenn Sie eine neue Tasksequenz erstellen möchten, die auf einer vorhandenen Tasksequenz basiert.

Wenn Sie in einem Ordner eine Kopie einer Tasksequenz erstellen, wird die Kopie in diesem Ordner aufgeführt, bis Sie den Tasksequenzknoten aktualisieren. Nach der Aktualisierung wird die Kopie im Stammordner angezeigt.  

### <a name="refresh"></a>Aktualisieren

Hiermit werden die Details für die ausgewählte Tasksequenz aktualisiert.

### <a name="delete"></a>Löschen

Hiermit wird die ausgewählte Tasksequenz gelöscht.

### <a name="create-phased-deployment"></a>Stufenweise Bereitstellung erstellen

Weitere Informationen finden Sie unter [Erstellen von stufenweisen Bereitstellungen mit Configuration Manager](create-phased-deployment-for-task-sequence.md).

### <a name="deploy"></a>Bereitstellen

Weitere Informationen finden Sie unter [Deploy a task sequence](deploy-a-task-sequence.md).

### <a name="distribute-content"></a>Treiberpakete

Hiermit wird der Assistent für die Verteilung von Inhalt gestartet, um Inhalte, auf die verwiesen wird, an Verteilungspunkte zu senden.

### <a name="create-prestaged-content-file"></a>Datei für vorab bereitgestellten Inhalt erstellen

Hiermit wird der Assistenten zum Erstellen von vorab bereitgestellten Inhaltsdateien gestartet, mit dem der Inhalt der Tasksequenz vorab bereitgestellt wird. Informationen zum Erstellen einer vorab bereitgestellten Inhaltsdatei finden Sie unter [Vorabbereitstellen von Inhalt](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).

### <a name="move"></a>Verschieben

Hiermit wird die ausgewählte Tasksequenz in einen anderen Ordner im Knoten **Tasksequenzen** verschoben.

### <a name="set-security-scopes"></a>Sicherheitsbereiche festlegen

Hiermit können Sicherheitsbereiche für die ausgewählte Tasksequenz ausgewählt werden. Weitere Informationen finden Sie unter [Sicherheitsbereiche](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope).

### <a name="properties"></a>Eigenschaften

Weitere Informationen finden Sie unter [Konfigurieren der Eigenschaften des Softwarecenters](#bkmk_prop-general) und [Konfigurieren von erweiterten Tasksequenzeinstellungen](#bkmk_prop-advanced).

### <a name="view"></a>Anzeigen

<!--3633146-->
Ab Version 1902 ist **Ansicht** die Standardaktion für Tasksequenzen. Mit dieser Aktion können Sie die Schritte der Tasksequenz anzeigen, ohne sie für die Bearbeitung sperren zu müssen. Weitere Informationen finden Sie unter [Verwenden des Tasksequenz-Editors](../understand/task-sequence-editor.md#bkmk_view).

## <a name="see-also"></a>Weitere Informationen:

- [Szenarien für die Bereitstellung von Unternehmensbetriebssystemen](scenarios-to-deploy-enterprise-operating-systems.md)

- [Verwenden des Tasksequenz-Editors](../understand/task-sequence-editor.md)

- [Bereitstellen einer Tasksequenz](deploy-a-task-sequence.md)

- [Tasksequenzschritte](../understand/task-sequence-steps.md)

- [Sammlungs- und Gerätevariablen](../understand/using-task-sequence-variables.md#bkmk_set-coll-var)

- [Erstellen von stufenweisen Bereitstellungen](create-phased-deployment-for-task-sequence.md)
