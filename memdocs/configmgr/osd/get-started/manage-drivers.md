---
title: Verwalten von Treibern
titleSuffix: Configuration Manager
description: Verwenden Sie den Configuration Manager-Treiberkatalog zum Importieren von Gerätetreibern und Gruppentreibern in Paketen und zum Verteilen dieser Pakete an Verteilungspunkte.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 84802d55-112e-4f7f-9a48-74a80d91a0f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8fffa72e45f2f9e063fb0072882c2a5278694cee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708898"
---
# <a name="manage-drivers-in-configuration-manager"></a>Verwalten von Treibern im Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Configuration Manager stellt einen Treiberkatalog bereit, den Sie zum Verwalten der Windows-Gerätetreiber in Ihrer Configuration Manager-Umgebung verwenden können. Verwenden Sie den Treiberkatalog zum Importieren von Gerätetreibern in den Configuration Manager, um sie in Paketen zu gruppieren und diese Pakete an Verteilungspunkte zu verteilen. Sie können Gerätetreiber verwenden, wenn Sie das vollständige Betriebssystem auf dem Zielcomputer installieren und wenn Sie Windows PE in einem Startimage verwenden. Windows-Gerätetreiber bestehen aus einer INF-Datei (Setup Information File) sowie ggf. zusätzlichen Dateien, die für die Geräteunterstützung erforderlich sind. Wenn Sie ein Betriebssystem bereitstellen, werden die Hardware- und Plattforminformationen durch Configuration Manager aus der INF-Datei des Geräts abgerufen. 



## <a name="driver-categories"></a><a name="BKMK_DriverCategories"></a> Treiberkategorien

Wenn Sie Gerätetreiber importieren, können Sie sie einer Kategorie zuweisen. Mithilfe von Gerätetreiberkategorien können Sie ähnlich verwendete Gerätetreiber im Treiberkatalog gruppieren. Weisen Sie z.B. alle Netzwerkkarten-Gerätetreiber einer bestimmten Kategorie zu. Wenn Sie dann eine Tasksequenz erstellen, die den Schritt [Treiber automatisch anwenden](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) enthält, geben Sie eine bestimmte Kategorie von Gerätetreibern an. Configuration Manager überprüft anschließend die Hardware und wählt die anwendbaren Treiber aus dieser Kategorie aus, um sie zur Verwendung durch Windows Setup verfügbar zu machen.  



## <a name="driver-packages"></a><a name="BKMK_ManagingDriverPackages"></a> Treiberpakete

Fassen Sie zur Vereinfachung der Bereitstellung eines Betriebssystems ähnliche Gerätetreiber in Paketen zusammen. Erstellen Sie z.B. ein Treiberpaket für jeden Computerhersteller in Ihrem Netzwerk. Sie können ein Treiberpaket erstellen, wenn Sie Treiber direkt über den Knoten **Treiberpakete** in den Treiberkatalog importieren. Nachdem Sie ein Treiberpaket erstellt haben, verteilen Sie es an Verteilungspunkte. Dann können Configuration Manager-Clientcomputer die Treiber wie erforderlich installieren. 

Beachten Sie folgende Punkte:  

- Wenn Sie ein Treiberpaket erstellen, muss der Quellspeicherort des Pakets einen Verweis auf eine leere Netzwerkfreigabe enthalten, die nicht von einem anderen Treiberpaket verwendet wird. Der SMS-Anbieter benötigt **Vollzugriff**-Berechtigungen für diesen Speicherort.  

- Wenn Sie einem Treiberpaket Gerätetreiber hinzufügen, kopiert Configuration Manager sie an den Quellspeicherort des Pakets. Sie können einem Treiberpaket nur Gerätetreiber hinzufügen, die Sie importiert haben und die im Treiberkatalog aktiviert sind.  

- Sie können eine Teilmenge der Gerätetreiber aus einem vorhandenen Treiberpaket kopieren. Erstellen Sie zuerst ein neues Treiberpaket. Fügen Sie dem neuen Paket dann die Teilmenge der Gerätetreiber hinzu, und stellen Sie das neue Paket an einem Verteilungspunkt bereit.  

- Wenn Sie Tasksequenzen verwenden, um Treiber zu installieren, erstellen Sie Treiberpakete mit weniger als 500 Gerätetreibern.


### <a name="create-a-driver-package"></a><a name="BKMK_CreatingDriverPackages"></a> Erstellen eines Treiberpakets  

> [!IMPORTANT]  
> Zum Erstellen eines Treiberpakets benötigen Sie einen leeren Netzwerkordner, der von keinem anderen Treiberpaket verwendet wird. In der Regel erstellen Sie einen neuen Ordner, bevor Sie dieses Verfahren starten.  

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**. Erweitern Sie **Betriebssysteme**, und wählen Sie dann den Knoten **Treiberpakete** aus.  

2. Wählen Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Erstellen** die Option **Treiberpaket erstellen** aus.  

3. Geben Sie einen beschreibenden **Namen** für das Treiberpaket an.  

4. Geben Sie einen optionalen **Kommentar** für das Treiberpaket ein. Verwenden Sie diese Beschreibung, um Informationen zu Inhalt oder Zweck des Treiberpakets anzugeben.  

5. Geben Sie im Feld **Pfad** einen leeren Quellordner für das Treiberpaket an. Von jedem Treiberpaket muss ein eindeutiger Ordner verwendet werden. Dieser Pfad ist als Netzwerkspeicherort erforderlich.  

   > [!IMPORTANT]  
   > Das Standortserverkonto muss über die **Vollzugriff**-Berechtigungen für den angegebenen Quellordner verfügen.  

Das neue Treiberpaket enthält keine Treiber. Im nächsten Schritt werden dem Paket Treiber hinzugefügt.  

Wenn der Knoten **Treiberpakete** mehrere Pakete enthält, können Sie dem Knoten Ordner hinzufügen, um die Pakete in logische Gruppen zu unterteilen.  


### <a name="additional-actions-for-driver-packages"></a><a name="BKMK_PackageActions"></a> Zusätzliche Aktionen für Treiberpakete  

Sie können zusätzliche Aktionen zur Verwaltung von Treiberpaketen ausführen, wenn Sie im Knoten **Treiberpakete** mindestens ein Treiberpaket auswählen. 


#### <a name="create-prestage-content-file"></a>Datei für vorab bereitgestellten Inhalt erstellen
Hiermit werden Dateien erstellt, die Sie zum manuellen Importieren von Inhalt und der zugeordneten Metadaten verwenden können. Verwenden Sie vorab bereitgestellten Inhalt, wenn die Bandbreite zwischen dem Standortserver und den Verteilungspunkten, auf denen das Treiberpaket gespeichert wird, eingeschränkt ist.

#### <a name="delete"></a>Löschen
Hiermit wird das Treiberpaket aus dem Knoten **Treiberpakete** entfernt.

#### <a name="distribute-content"></a>Treiberpakete
Hiermit wird das Treiberpaket an Verteilungspunkte, Verteilungspunktgruppen sowie an Verteilungspunktgruppen, die Sammlungen zugeordnet sind, verteilt.

#### <a name="manage-access-accounts"></a>Zugriffskonten verwalten
Hiermit werden Zugriffskonten für das Treiberpaket hinzugefügt, geändert oder entfernt.

Weitere Informationen zu Paketzugriffskonten finden Sie unter [Technische Referenz für Konten in Configuration Manager](../../core/plan-design/hierarchy/accounts.md).

#### <a name="move"></a>Verschieben
Hiermit wird das Treiberpaket im Knoten **Treiberpakete** in einen anderen Ordner verschoben.

#### <a name="update-distribution-points"></a>Verteilungspunkte aktualisieren
Hiermit wird an allen Verteilungspunkten, auf denen das Gerätetreiberpaket gespeichert wird, ein Update des Pakets ausgeführt. Bei dieser Aktion wird nur der Inhalt kopiert, der sich seit seiner letzten Verteilung geändert hat.

#### <a name="properties"></a>Eigenschaften
Öffnet das Dialogfeld **Eigenschaften**. Überprüfen und ändern Sie Inhalt und Eigenschaften des Treibers. Ändern Sie z.B. Namen und Beschreibung des Treibers, aktivieren oder deaktivieren Sie ihn, und geben Sie an, auf welchen Plattformen er ausgeführt werden kann. 

<!--3607716, fka 1358270-->
Ab Version 1810 verfügen Treiberpakete über zusätzliche Metadatenfelder für **Hersteller** und **Modell**. Verwenden Sie diese Felder, um Treiberpakete mit Informationen für die allgemeine Verwaltung zu kennzeichnen oder um alte und doppelte Treiber zu identifizieren, die gelöscht werden können. Wählen Sie auf der Registerkarte **Allgemein** einen vorhandenen Wert aus den Dropdownlisten aus, oder geben Sie eine Zeichenfolge ein, um einen neuen Eintrag zu erstellen.

Im Knoten **Treiberpakete** werden diese Felder als die Spalten **Driver Manufacturer** (Treiberhersteller) und **Driver Model** (Treibermodell) in der Liste angezeigt. Sie können ebenso als Suchkriterium verwendet werden.

Ab Version 1906 können Sie mithilfe dieser Attribute Inhalte in einem vorgeschalteten Cache auf einem Client zwischenspeichern. Weitere Informationen finden Sie unter [Konfigurieren des zwischengespeicherten Inhalts](../deploy-use/configure-precache-content.md).<!--4224642-->  




## <a name="device-drivers"></a><a name="BKMK_DeviceDrivers"></a> Gerätetreiber

Sie können Treiber auf Zielcomputern installieren, ohne sie in das Betriebssystemimage einzuschließen, das bereitgestellt wird. In Configuration Manager ist ein Treiberkatalog enthalten, der Verweise zu allen Treibern enthält, die Sie in Configuration Manager importieren. Der Treiberkatalog befindet sich im Arbeitsbereich **Softwarebibliothek**. Er besteht aus zwei Knoten: **Treiber** und **Treiberpakete**. Im Knoten **Treiber** sind alle Treiber aufgelistet, die Sie in den Treiberkatalog importiert haben.  


### <a name="import-device-drivers-into-the-driver-catalog"></a><a name="BKMK_ImportDrivers"></a> Importieren von Gerätetreibern in den Gerätekatalog  

Bevor Sie einen Treiber verwenden können, wenn Sie ein Betriebssystem bereitstellen, importieren Sie ihn in den Treiberkatalog. Um Treiber besser verwalten zu können, importieren Sie nur die Treiber, die Sie als Teil Ihrer Betriebssystembereitstellungen installieren möchten. Speichern Sie mehrere Versionen der Treiber im Katalog, um vorhandene Gerätetreiber mühelos aktualisieren zu können, wenn die Hardwaregeräteanforderungen in Ihrem Netzwerk sich ändern.  

Im Rahmen des Importvorgangs für den Gerätetreiber liest der Configuration Manager die folgenden Eigenschaften zum Treiber:
- Provider
- Class
- Version
- Signatur
- Unterstützte Hardware
- Unterstützte Plattforminformationen

Der Treiber wird standardmäßig nach dem ersten Hardwaregerät benannt, das er unterstützt. Sie können den Gerätetreiber zu einem späteren Zeitpunkt umbenennen. Die Liste der unterstützten Plattformen beruht auf den Informationen in der INF-Datei des Treibers. Diese Informationen sind jedoch nicht immer vollständig. Überprüfen Sie daher nach dem Import eines Treibers in den Katalog manuell, ob er unterstützt wird.  

Nachdem Sie Gerätetreiber in den Katalog importiert haben, fügen Sie sie Treiberpaketen oder Startimagepaketen hinzu.  

> [!IMPORTANT]  
> Sie können Gerätetreiber nicht direkt in einen Unterordner des Knotens **Treiber** importieren. Zum Importieren eines Gerätetreibers in einen Unterordner importieren Sie den Gerätetreiber zuerst in den Knoten **Treiber** , und verschieben Sie den Treiber dann in den Unterordner.  


#### <a name="process-to-import-windows-device-drivers-into-the-driver-catalog"></a>Vorgehen beim Importieren von Windows-Gerätetreibern in den Treiberkatalog  

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**. Erweitern Sie **Betriebssysteme**, und wählen Sie dann den Knoten **Treiber** aus.  

2. Wählen Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Erstellen** die Option **Treiber importieren** aus, um den **Treiberimport-Assistenten** zu starten.  

3. Geben Sie auf der Seite **Treiber suchen** die folgenden Optionen an:  

    - **Alle Treiber im folgenden Netzwerkpfad (UNC) importieren:** Um alle Gerätetreiber in einem bestimmten Ordner zu importieren, geben Sie den Netzwerkpfad ein. Beispiel: `\\servername\share\folder`.  

        > [!NOTE]  
        > Wenn viele Unterordner und Treiber-INF-Dateien vorhanden sind, kann dieser Vorgang zeitintensiv sein.  

    - **Bestimmten Treiber importieren:** Geben Sie den Netzwerkpfad zur INF-Datei des Windows-Gerätetreibers an, um einen bestimmten Treiber aus einem Ordner zu importieren.  

    - **Option für doppelte Treiber angeben:** Geben Sie an, wie Treiberkategorien in Configuration Manager verwaltet werden sollen, wenn Sie einen doppelten Gerätetreiber importieren.  
        - **Treiber importieren und eine neue Kategorie vorhandenen Kategorien hinzufügen**  
        - **Treiber importieren und vorhandene Kategorien beibehalten**  
        - **Treiber importieren und vorhandene Kategorien überschreiben**  
        - **Treiber nicht importieren**  

    > [!IMPORTANT]  
    > Wenn Sie Treiber importieren, muss der Standortserver über die **Leseberechtigung** für diesen Ordner verfügen. Andernfalls tritt beim Import ein Fehler auf.  

4. Geben Sie auf der Seite **Treiberdetails** die folgenden Optionen an:  

    - **Treiber ausblenden, die nicht in einer Speicher- oder Netzwerkklasse (für Startimages) enthalten sind:** Verwenden Sie diese Einstellung, um nur Speicher- und Netzwerktreiber anzuzeigen. Diese Option blendet andere Treiber aus, die in der Regel nicht für Startimages benötigt werden, z.B. Video- oder Modemtreiber.  

    - **Treiber ausblenden, die nicht digital signiert sind:** Microsoft empfiehlt, nur digital signierte Treiber zu verwenden  

    - Wählen Sie in der Treiberliste die Treiber aus, die Sie in den Treiberkatalog importieren möchten.  

    - **Diese Treiber aktivieren und Installation auf Computern zulassen:** Aktivieren Sie diese Einstellung, damit Computer die Gerätetreiber installieren können. Diese Option ist standardmäßig aktiviert.  

        > [!IMPORTANT]  
        > Wenn ein Gerätetreiber ein Problem verursacht, oder Sie die Installation eines Gerätetreibers aussetzen möchten, deaktivieren Sie ihn während des Imports. Sie können Treiber auch deaktivieren, nachdem Sie sie importiert haben.  

    - Wenn Sie die Gerätetreiber zu Filterzwecken einer Verwaltungskategorie wie „Desktops“ oder „Notebooks“ zuweisen möchten, wählen Sie die Schaltfläche **Kategorien** aus. Wählen Sie dann eine vorhandene Kategorie aus, oder erstellen Sie eine neue. Steuern Sie mit Kategorien, welche Gerätetreiber vom Tasksequenzschritt [Treiber automatisch anwenden](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) angewendet werden.  

5. Wählen Sie auf der Seite **Treiber zu Paketen hinzufügen** aus, ob die Treiber einem Paket hinzugefügt werden sollen.  

    - Wählen Sie die Treiberpakete aus, die zur Verteilung der Gerätetreiber verwendet werden.  

        Falls notwendig, wählen Sie **Neues Paket** aus, um ein neues Treiberpaket zu erstellen. Wenn Sie ein neues Treiberpaket erstellen, geben Sie eine Netzwerkfreigabe an, die nicht von anderen Treiberpaketen verwendet wird.  

    - Wenn das Paket bereits an Verteilungspunkte verteilt wurde, wählen Sie im Dialogfeld **Ja** aus, um die Startimages auf Verteilungspunkten zu aktualisieren. Sie können Gerätetreiber erst verwenden, nachdem sie an Verteilungspunkte verteilt wurden. Führen Sie bei Auswahl von **Nein** die Aktion **Verteilungspunkte aktualisieren** vor der Verwendung des Startimages aus. Ist das Treiberpaket nie verteilt worden, müssen Sie am Knoten **Treiberpakete** die Aktion **Inhalt verteilen** verwenden.  

6. Wählen Sie auf der Seite **Treiber zu Startimages hinzufügen** aus, ob die Gerätetreiber vorhandenen Startimages hinzugefügt werden sollen.  

    > [!NOTE]  
    > Fügen Sie den Startimages nur Speicher- und Netzwerktreiber hinzu.  

    - Wählen Sie im Dialogfeld **Ja** aus, um ein Update der Startimages auf Verteilungspunkten auszuführen. Sie können Gerätetreiber erst verwenden, nachdem sie an Verteilungspunkte verteilt wurden. Führen Sie bei Auswahl von **Nein** die Aktion **Verteilungspunkte aktualisieren** vor der Verwendung des Startimages aus. Ist das Treiberpaket nie verteilt worden, müssen Sie am Knoten **Treiberpakete** die Aktion **Inhalt verteilen** verwenden.  

    - Configuration Manager gibt eine Warnung aus, wenn die Architektur für einen oder mehrere Treiber nicht mit der Architektur der von Ihnen ausgewählten Startimages übereinstimmt. Wenn sie nicht übereinstimmen, wählen Sie **OK** aus. Kehren Sie zur Seite **Treiberdetails** zurück, um die Treiber zu deaktivieren, die nicht der Architektur des ausgewählten Startimages entsprechen. Wenn Sie beispielsweise ein x64- und x86-Startabbild auswählen, müssen alle Treiber beide Architekturen unterstützen. Wenn Sie ein x64-Startabbild auswählen, müssen alle Treiber die x64-Architekturen unterstützen.  

        > [!NOTE]  
        > - Die Architektur basiert auf der Architektur, die in der INF-Datei vom Hersteller angegeben ist.  
        > - Wenn für einen Treiber angegeben ist, dass er beide Architekturen unterstützt, können Sie ihn in jedes der Startimages importieren.  

    - Configuration Manager warnt Sie, wenn Sie Gerätetreiber hinzufügen, die keine Netzwerk- oder Speichertreiber für ein Startimage sind. In den meisten Fällen sind sie nicht für das Startimage erforderlich. Wählen Sie **Ja** aus, um die Treiber zum Startimage hinzuzufügen, oder **Nein**, um zurückzukehren und die Treiberauswahl zu ändern.  

    - Configuration Manager gibt eine Warnung aus, wenn einer oder mehrere der ausgewählten Treiber nicht ordnungsgemäß digital signiert sind. Wählen Sie **Ja** aus, um fortzufahren, oder **Nein**, um zurückzukehren und die Treiberauswahl zu ändern.  

7. Schließen Sie den Assistenten ab.  


### <a name="manage-device-drivers-in-a-driver-package"></a><a name="BKMK_ModifyDriverPackage"></a> Verwalten von Gerätetreibern in einem Treiberpaket  

Gehen Sie wie folgt vor, um Treiberpakete und Startabbilder zu ändern. Um einen Treiber hinzuzufügen oder zu entfernen, suchen Sie ihn zunächst im Knoten **Treiber**. Bearbeiten Sie dann die Pakete oder Startimages, denen der ausgewählte Treiber zugeordnet ist.  

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**. Erweitern Sie **Betriebssysteme**, und wählen Sie dann den Knoten **Treiber** aus.  

2. Wählen Sie die Gerätetreiber aus, die Sie einem Treiberpaket hinzufügen möchten.  

3. Wählen Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Treiber** die Option **Bearbeiten** und dann **Treiberpakete** aus.  

4. Zum Hinzufügen eines Gerätetreibers aktivieren Sie das Kontrollkästchen für die Treiberpakete, denen Sie den Gerätetreiber hinzufügen möchten. Zum Entfernen eines Gerätetreibers deaktivieren Sie das Kontrollkästchen für die Treiberpakete, aus denen Sie den Gerätetreiber entfernen möchten.  

    Wenn Sie Gerätetreiber hinzufügen, die Treiberpaketen zugeordnet sind, können Sie optional ein neues Paket erstellen. Wählen Sie **Neues Paket** aus, sodass das Dialogfeld **Neues Treiberpaket** geöffnet wird.  

5. Wenn das Paket bereits an Verteilungspunkte verteilt wurde, wählen Sie im Dialogfeld **Ja** aus, um die Startimages auf Verteilungspunkten zu aktualisieren. Sie können Gerätetreiber erst verwenden, nachdem sie an Verteilungspunkte verteilt wurden. Führen Sie bei Auswahl von **Nein** die Aktion **Verteilungspunkte aktualisieren** vor der Verwendung des Startimages aus. Ist das Treiberpaket nie verteilt worden, müssen Sie am Knoten **Treiberpakete** die Aktion **Inhalt verteilen** verwenden. Bevor die Treiber zur Verfügung stehen, müssen Sie das Treiberpaket auf Verteilungspunkten aktualisieren.  

    Wählen Sie nach der Fertigstellung **OK** aus.  


### <a name="manage-device-drivers-in-a-boot-image"></a><a name="BKMK_ManageDriversBootImage"></a> Verwalten von Gerätetreibern in einem Startabbild  

Sie können Startimages Windows-Gerätetreiber hinzufügen, die in den Treiberkatalog importiert wurden. Verwenden Sie die folgenden Richtlinien, wenn Sie einem Startabbild Gerätetreiber hinzufügen:  

- Fügen Sie Startimages nur Speicher- und Netzwerktreiber hinzu. Andere Arten von Treibern sind in der Regel nicht in Windows PE erforderlich. Nicht erforderliche Treiber setzen die Größe des Startimages unnötig herauf.  

- Fügen Sie einem Startimage nur Gerätetreiber für Windows 10 hinzu. Die erforderliche Version von Windows PE basiert auf Windows 10.  

- Stellen Sie sicher, dass Sie die richtigen Gerätetreiber für die Startimagearchitektur verwenden. Fügen Sie einem x64-Startimage keinen x86-Gerätetreiber hinzu.  

#### <a name="process-to-modify-the-device-drivers-associated-with-a-boot-image"></a>Vorgehen beim Ändern der Gerätetreiber, die einem Startimage zugeordnet sind  

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**. Erweitern Sie **Betriebssysteme**, und wählen Sie dann den Knoten **Treiber** aus.  

2. Wählen Sie die Gerätetreiber aus, die Sie dem Treiberpaket hinzufügen möchten.  

3. Wählen Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Treiber** die Option **Bearbeiten** und dann **Startimages** aus.  

4. Zum Hinzufügen eines Gerätetreibers aktivieren Sie das Kontrollkästchen für das Startabbild, dem Sie den Gerätetreiber hinzufügen möchten. Zum Entfernen eines Gerätetreibers aktivieren Sie das Kontrollkästchen für das Startabbild, aus dem Sie den Gerätetreiber entfernen möchten.  

5. Deaktivieren Sie das Kontrollkästchen **Verteilungspunkte nach Abschluss aktualisieren**, wenn Sie kein Update der Verteilungspunkte, auf denen das Startimage gespeichert wird, ausführen möchten. Standardmäßig wird ein Update der Verteilungspunkte ausgeführt, wenn ein Update des Startabbilds ausgeführt wird.  

    - Wählen Sie im Dialogfeld **Ja** aus, um ein Update der Startimages auf Verteilungspunkten auszuführen. Sie können Gerätetreiber erst verwenden, nachdem sie an Verteilungspunkte verteilt wurden. Führen Sie bei Auswahl von **Nein** die Aktion **Verteilungspunkte aktualisieren** vor der Verwendung des Startimages aus. Ist das Treiberpaket nie verteilt worden, müssen Sie am Knoten **Treiberpakete** die Aktion **Inhalt verteilen** verwenden.  

    - Configuration Manager gibt eine Warnung aus, wenn die Architektur für einen oder mehrere Treiber nicht mit der Architektur der von Ihnen ausgewählten Startimages übereinstimmt. Wenn sie nicht übereinstimmen, wählen Sie **OK** aus. Kehren Sie zur Seite **Treiberdetails** zurück, um die Treiber zu deaktivieren, die nicht der Architektur des ausgewählten Startimages entsprechen. Wenn Sie beispielsweise ein x64- und x86-Startabbild auswählen, müssen alle Treiber beide Architekturen unterstützen. Wenn Sie ein x64-Startabbild auswählen, müssen alle Treiber die x64-Architekturen unterstützen.  

        > [!NOTE]
        > - Die Architektur basiert auf der Architektur, die in der INF-Datei vom Hersteller angegeben ist.  
        > - Wenn für einen Treiber angegeben ist, dass er beide Architekturen unterstützt, können Sie ihn in jedes der Startabbilder importieren.  

    - Configuration Manager warnt Sie, wenn Sie Gerätetreiber hinzufügen, die keine Netzwerk- oder Speichertreiber für ein Startimage sind. In den meisten Fällen sind sie nicht für das Startimage erforderlich. Wählen Sie **Ja** aus, um die Treiber zum Startimage hinzuzufügen, oder **Nein**, um zurückzukehren und die Treiberauswahl zu ändern.  

    - Configuration Manager gibt eine Warnung aus, wenn einer oder mehrere der ausgewählten Treiber nicht ordnungsgemäß digital signiert sind. Wählen Sie **Ja** aus, um fortzufahren, oder **Nein**, um zurückzukehren und die Treiberauswahl zu ändern.  


### <a name="additional-actions-for-device-drivers"></a><a name="BKMK_DriverActions"></a> Zusätzliche Aktionen für Gerätetreiber  

Sie können zusätzliche Aktionen zum Verwalten von Treibern ausführen, wenn Sie diese im Knoten **Treiber** auswählen.  

#### <a name="categorize"></a>Kategorisieren
Hiermit wird eine Verwaltungskategorie für die ausgewählten Treiber gelöscht, verwaltet oder festgelegt.

#### <a name="delete"></a>Löschen
Hiermit wird der Treiber aus dem Knoten **Treiber** entfernt. Außerdem wird der Treiber aus den zugeordneten Verteilungspunkten entfernt.

#### <a name="disable"></a>Deaktivieren
Hiermit wird die Installation des Treibers verhindert. Diese Aktion deaktiviert den Treiber vorübergehend. Die Tasksequenz kann einen deaktivierten Treiber nicht installieren, wenn Sie ein BS bereitstellen. 

> [!Note]  
> Diese Aktion verhindert nur, dass Treiber mit dem Tasksequenzschritt **Treiber automatisch anwenden** installiert werden.

#### <a name="enable"></a>Aktivieren Sie
Hiermit wird den Configuration Manager-Clientcomputern und Tasksequenzen gestattet, den Gerätetreiber zu installieren, wenn Sie das BS bereitstellen.

#### <a name="move"></a>Verschieben
Hiermit wird der Gerätetreiber im Knoten **Treiber** in einen anderen Ordner verschoben.

#### <a name="properties"></a>Eigenschaften
Öffnet das Dialogfeld **Eigenschaften**. Überprüfen Sie die Eigenschaften des Treibers, und ändern Sie sie. Ändern Sie z.B. Namen und Beschreibung, aktivieren oder deaktivieren Sie ihn, und geben Sie an, auf welchen Plattformen er ausgeführt werden kann.



## <a name="use-task-sequences-to-install-drivers"></a><a name="BKMK_TSDrivers"></a> Verwenden von Tasksequenzen zum Installieren von Treibern  

Verwenden Sie Tasksequenzen, um die Art der Bereitstellung des BS zu automatisieren. Jeder Schritt in der Tasksequenz kann eine bestimmte Aktion ausführen, beispielsweise die Installation eines Gerätetreibers. Sie können die folgenden beiden Tasksequenzschritte verwenden, um Gerätetreiber zu installieren, während Sie ein BS bereitstellen:  

- [Treiber automatisch anwenden:](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) Mit diesem Schritt werden Gerätetreiber automatisch als Teil einer Betriebssystembereitstellung ausgewählt und installiert. Sie können den Tasksequenzschritt so konfigurieren, dass nur der für das jeweilige erkannte Hardwaregerät optimal geeignete Treiber installiert wird. Geben Sie alternativ an, dass der Schritt alle kompatiblen Treiber für das jeweilige erkannte Hardwaregerät installiert und Windows Setup dann den besten Treiber auswählen kann. Sie können auch eine Kategorie von Treibern angeben, um die für diesen Schritt verfügbaren Treiber zu begrenzen.  

- [Treiberpaket anwenden:](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage) Mit diesem Schritt können Sie alle Gerätetreiber in einem bestimmten Treiberpaket für Windows Setup zur Verfügung stellen. Die angegebenen Treiberpakete werden von Windows Setup nach den erforderlichen Gerätetreibern durchsucht. Beim Erstellen eigenständiger Medien müssen Sie diesen Schritt zum Installieren von Gerätetreibern ausführen.  

Wenn Sie diese Tasksequenzschritte verwenden, können Sie auch angeben, wie die Treiber auf dem Computer, auf dem Sie das BS bereitstellen, installiert werden sollen. Weitere Informationen finden Sie unter [Verwalten von Tasksequenzen zum Automatisieren von Aufgaben](../deploy-use/manage-task-sequences-to-automate-tasks.md).  



## <a name="driver-reports"></a><a name="BKMK_DriverReports"></a> Treiberberichte  

Sie können mehrere Berichte in der Berichtkategorie **Treiberverwaltung** verwenden, um allgemeine Informationen zu den Gerätetreibern im Treiberkatalog zu erhalten. Weitere Informationen zu Berichten finden Sie unter [Einführung in die Berichterstellung](../../core/servers/manage/introduction-to-reporting.md).

