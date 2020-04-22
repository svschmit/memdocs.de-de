---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 05/28/2019
ms.openlocfilehash: e5c15556a7a8dd91db3ae2c4aa4f9830abc8e430
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708878"
---
## <a name="apply-software-updates-to-an-image"></a><a name="BKMK_OSImagesApplyUpdates"></a> Anwenden von Softwareupdates auf ein Image

> [!Note]  
> Dieser Abschnitt gilt sowohl für **Betriebssystemabbilder** als auch für **Betriebssystemaktualisierungspakete**. Der verwendete allgemeine Begriff „Image“ bezieht sich auf die Windows-Imagedatei (WIM). Beide dieser Objekte verfügen über eine WIM, die Windows-Installationsdateien enthält. Softwareupdates sind auf diese Dateien in beiden Objekten anwendbar. Das Verhalten dieses Prozesses ist bei beiden Objekten gleich.  

Jeden Monat sind neue Softwareupdates für das Image verfügbar. Bevor Sie Softwareupdates auf das Image anwenden können, müssen Sie folgende Voraussetzungen erfüllen:

- Sie verfügen über eine Softwareupdateinfrastruktur.  
- Die Softwareupdates wurden erfolgreich synchronisiert.  
- Die Softwareupdates wurden heruntergeladen und in der Inhaltsbibliothek auf dem Standortserver gespeichert.  

Weitere Informationen finden Sie unter [Bereitstellen von Softwareupdates](../../../sum/deploy-use/deploy-software-updates.md).  

Wenden Sie relevante Softwareupdates nach einem festgelegten Zeitplan auf ein Image an. Dieser Vorgang wird auch als *Offlinewartung* bezeichnet. Nach diesem Zeitplan wendet Configuration Manager die ausgewählten Softwareupdates auf das Image an. Das aktualisierte Image kann dann auch neu an Verteilungspunkte verteilt werden.

> [!Important]  
> Sie können zwar je nach Version ein beliebiges anwendbares Softwareupdate für das Image auswählen, jedoch kann DISM nur auf bestimmte Updates für das Image angewendet werden. Die Datei **OfflineServicingMgr.log** enthält den folgenden Eintrag: `Not applying this update binary, it is not supported`.<!-- SCCMDocs issue 1324 -->

Die Standortdatenbank speichert Informationen zum Image. Dazu zählen auch die Softwareupdates, die während des Imports angewendet wurden. Softwareupdates, die Sie nach dem ursprünglichen Hinzufügen auf das Image anwenden, werden ebenfalls in der Standortdatenbank gespeichert. Wenn Sie den Assistenten zum Anwenden von Softwareupdates starten, ruft dieser die Liste der verfügbaren Softwareupdates ab, die vom Standort noch nicht auf das Image angewendet wurden. Configuration Manager kopiert die Softwareupdates, die Sie aus der Inhaltsbibliothek auf dem Standortserver auswählen. Anschließend werden die Softwareupdates auf das Image angewendet.  

### <a name="servicing-process"></a>Wartungsprozess

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und wählen Sie anschließend entweder den Knoten **Betriebssystemabbilder** oder **Betriebssystemaktualisierungspakete** aus.  

2. Wählen Sie das Objekt aus, auf das Sie die Softwareupdates anwenden möchten.  

3. Wählen Sie auf dem Menüband **Updates planen** aus, um den Assistenten zu starten.  

4. Wählen Sie auf der Seite **Updates auswählen** die Softwareupdates aus, die auf das Image angewendet werden sollen. Es kann eine Weile dauern, bis die Liste mit den Updates im Assistenten angezeigt wird. Verwenden Sie den **Filter**, um in den Metadaten nach Zeichenfolgen zu suchen. Verwenden Sie die Dropdownliste **Systemarchitektur**, um nach **X86**, **X64** oder **Alle** zu filtern. Sie können aus der Liste ein Update, mehrere oder alle Updates auswählen. Wenn Sie mit der Auswahl der Updates fertig sind, klicken Sie auf **Weiter**.  

5. Geben Sie auf der Seite **Zeitplan festlegen** die folgenden Einstellungen an, und klicken Sie dann auf **Weiter**.  

    1. **Zeitplan**: Geben Sie den Zeitplan für die Anwendung der Softwareupdates auf das Image durch den Standort an.  

    2. **Bei Fehler fortsetzen**: Aktivieren Sie diese Option, um anzugeben, dass Softwareupdates auch beim Auftreten eines Fehlers auf das Image angewendet werden sollen.  

    3. **Verteilungspunkte mit dem Image aktualisieren**: Wählen Sie diese Option aus, um das Image auf Verteilungspunkten zu aktualisieren, nachdem der Standort die Softwareupdates angewendet hat.  

6. Schließen Sie den Assistenten für das Planen von Updates ab.  

> [!NOTE]  
> Die Wartung der Betriebssystemupgradepakete und Betriebssystemimages entfernt ältere Versionen, um die Nutzlast zu verringern.  

### <a name="servicing-operations"></a>Wartungsvorgänge

Fügen Sie in der Configuration Manager-Konsole entweder im Knoten **Betriebssystemabbilder** oder im Knoten **Betriebssystemaktualisierungspakete** die folgenden Spalten zur Ansicht hinzu:

- **Datum der geplanten Updates**: Diese Eigenschaft zeigt den nächsten Zeitplan an, den Sie definiert haben.  
- **Status der geplanten Updates**: Diese Eigenschaft zeigt den Status an. Beispielsweise **Erfolgreich** oder **Vorgang läuft**.  

Wählen Sie ein bestimmtes Imageobjekt aus, und wechseln Sie anschließend zur Registerkarte **Updatestatus** im Detailbereich. Diese Registerkarte zeigt die Liste der Updates im Image an.

Wählen Sie ein bestimmtes Imageobjekt und anschließend im Menüband **Eigenschaften** aus. Die Registerkarte **Installierte Updates** zeigt die Liste der Updates im Image an. Die Registerkarte **Wartung** ist eine schreibgeschützte Ansicht des aktuellen Wartungszeitplans und der Updates, die im Zeitplan vorgesehen sind.

Während des Status **Vorgang läuft** können Sie auf dem Menüband **Geplante Updates abbrechen** auswählen. Durch diese Aktion wird der aktive Wartungsprozess abgebrochen.

Informationen zur Fehlerbehebung in diesem Prozess finden Sie in den Dateien **OfflineServicingMgr.log** und **dism.log** auf dem Standortserver. Weitere Informationen finden Sie in den [Protokolldateien](../../../core/plan-design/hierarchy/log-files.md).

### <a name="specify-the-drive-for-offline-os-image-servicing"></a><a name="bkmk_servicing-drive"></a> Angeben des Laufwerks für die Offlinewartung von Betriebssystemimages

<!--1358924-->

Ab Version 1810 können Sie das Laufwerk angeben, das Configuration Manager während der Offlinewartung von Betriebssystemimages verwendet. Bei diesem Prozess kann eine große Menge Speicherplatz mit temporären Dateien belegt werden. Durch diese Option können Sie das verwendete Laufwerk flexibel auswählen.

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie den Knoten **Standorte** aus. Klicken Sie im Menüband auf **Standortkomponenten konfigurieren** und anschließend auf **Betriebssystembereitstellung**.  

2. Geben Sie auf der Registerkarte **Offlinewartung** die Option für **A local drive to be used by offline servicing of images** (Ein bei der Offlinewartung von Images zu verwendendes lokales Laufwerk) an.  

Diese Einstellung ist standardmäßig auf **Automatisch** festgelegt. Mit diesem Wert wählt Configuration Manager das Laufwerk aus, auf dem es installiert ist.

Wenn Sie ein Laufwerk auswählen, das auf dem Standortserver nicht vorhanden ist, verhält sich Configuration Manager genauso wie bei der Auswahl von **Automatisch**.

Bei der Offlinewartung speichert Configuration Manager temporäre Dateien im Ordner `<drive>:\ConfigMgr_OfflineImageServicing`. Zudem wird das Betriebssystemimage in diesem Ordner eingebunden.

### <a name="optimized-image-servicing"></a><a name="bkmk_resetbase"></a> Optimierte Imagewartung

<!--3555951-->

Beim Anwenden eines Softwareupdates auf ein Betriebssystemimage gibt es ab Version 1902 eine neue Option zum Optimieren der Ausgabe durch Entfernen von ersetzten Updates. Die Optimierung der Offlinewartung betrifft nur Images mit einem einzelnen Index.

Wenn Sie für den Standort die Anwendung von Softwareupdates auf ein Betriebssystemimage planen, verwenden Sie das Windows-Befehlszeilenprogramm „Abbildverwaltung für die Bereitstellung“ (Deployment Image Servicing and Management, DISM). Durch diese Änderung während der Wartung sind nun zusätzlich die folgenden beiden Schritte enthalten:  

- Der Befehl DISM wird für das bereitgestellte Offlineimage mit den Parametern `/Cleanup-Image /StartComponentCleanup /ResetBase` ausgeführt. Wenn bei diesem Befehl ein Fehler auftritt, schlägt der aktuelle Wartungsprozess fehl. Es werden keine Änderungen für das Image übernommen.  

- Nachdem Configuration Manager Änderungen für das Image übernommen und die Bereitstellung für das Image aufgehoben hat, wird das Image in eine andere Datei exportiert. Für diesen Schritt wird der DISM-Parameter `/Export-Image` verwendet. Damit werden nicht benötigte Dateien aus dem Image entfernt und so die Größe reduziert.  

Microsoft empfiehlt die regelmäßige Anwendung von Updates auf Offlineimages. Diese Option müssen Sie nicht bei jeder Wartung eines Images verwenden. Wenn Sie diesen Vorgang einmal im Monat ausführen, profitieren Sie von dieser neuen Option am meisten, wenn Sie sie von Zeit zu Zeit nutzen. Weitere Informationen finden Sie unter [Recommendations for Install Software Updates (Empfehlungen zum Installieren von Softwareupdates)](../../understand/install-software-updates.md#recommendations).

Mit der neuen Option wird zwar die Gesamtgröße des gewarteten Images reduziert, dafür dauert der Prozess länger. Verwenden Sie den Assistenten, um die Wartung für einen passenden Zeitpunkt zu planen. Ferner wird auf dem Standortserver zusätzlicher Speicherplatz benötigt. Sie können den Standort zur Verwendung eines alternativen Standorts anpassen. Weitere Informationen finden Sie unter [Angeben des Laufwerks für die Offlinewartung von Betriebssystemimages](#bkmk_servicing-drive).

#### <a name="process-to-optimize-image-servicing"></a>Prozess zum Optimieren der Imagewartung

1. Starten Sie den [Wartungsprozess](#servicing-process).  

2. Wählen Sie auf der Seite **Zeitplan festlegen** die Option **Abgelöste Updates nach der Imageaktualisierung entfernen** aus. Diese Option wird nicht automatisch aktiviert. Wenn das Image mehrere Indizes enthält, kann diese Option nicht verwendet werden.  

3. Führen Sie zur Planung der Imagewartung den Assistenten aus.  

Überprüfen und überwachen Sie den Prozess mithilfe der Protokolldatei **OfflineServicing.log**.
