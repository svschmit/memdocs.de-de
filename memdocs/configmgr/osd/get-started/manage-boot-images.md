---
title: Verwalten von Startabbildern (Startimages)
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie in Configuration Manager die Windows PE-Startimages verwalten, die Sie während der BS-Bereitstellung verwenden.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 97f2d81a-2c58-442c-88bc-defd5a1cd48f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 76e0fd3ad8ceaecb43d2a61c3abe15accda5e5d8
ms.sourcegitcommit: 4f10625e8d12aec294067a1d9138cbce19707560
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87912380"
---
# <a name="manage-boot-images-with-configuration-manager"></a>Verwalten von Startimages mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Ein Startimage in Configuration Manager ist ein [Windows PE-Image](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-intro) (WinPE), das während einer BS-Bereitstellung verwendet wird. Mithilfe von Startimages wird ein Computer in WinPE gestartet. Dieses minimale BS enthält begrenzte Komponenten und Dienste. Configuration Manager verwendet WinPE zur Vorbereitung des Zielcomputers für die Windows-Installation.

## <a name="default-boot-images"></a><a name="BKMK_BootImageDefault"></a> Standardstartimages

Configuration Manager stellt zwei Standardstartimages bereit: je eins zur Unterstützung von x86- bzw. x64-Plattformen. Diese Images werden in der folgenden Freigabe in den *X64*- oder *i386*-Ordnern auf dem Standortserver gespeichert: `\\<SiteServerName>\SMS_<sitecode>\osd\boot\`. Die Standardstartimages werden je nach der von Ihnen ausgeführten Aktion aktualisiert oder neu generiert.

Betrachten Sie die folgenden Verhaltensweisen für die Aktionen, die für die standardmäßigen Startimages beschrieben werden:

- Die Quellentreiberobjekte müssen gültig sein. Diese Objekte enthalten die Treiberquellendateien. Wenn die Objekte nicht gültig sind, fügt der Standort die Treiber nicht den Startimages hinzu.  

- Startimages, die nicht auf den standardmäßigen Startimages basieren, werden nicht geändert, selbst wenn sie die gleiche Version von Windows PE verwenden.  

- Verteilen Sie die geänderten Startimages neu auf Verteilungspunkte.  

- Erstellen Sie alle Medien neu, die die geänderten Startimages verwenden.  

- Wenn die benutzerdefinierten oder Standardstartimages nicht automatisch aktualisiert werden sollen, speichern Sie sie nicht am Standardspeicherort.  

> [!NOTE]
> Das Protokolltool von Configuration Manager (**CMTrace**) wird allen Startimages in der **Softwarebibliothek** hinzugefügt. Wenn Sie Windows PE aufgerufen haben, starten Sie das Tool, indem Sie über die Eingabeaufforderung `cmtrace` eingeben.
>
> CMTrace ist der Standardviewer für Protokolldateien in Windows PE.

### <a name="use-updates-and-servicing-to-install-the-latest-version-of-configuration-manager"></a>Verwenden Sie Updates und Wartungen, um die neueste Version des Configuration Manager zu installieren.

Wenn Sie die Windows ADK-Version (Assessment and Deployment Kit) upgraden und anschließend Updates und Wartung zum Installieren der neuesten Version von Configuration Manager verwenden, generiert der Standort die standardmäßigen Startimages neu. Dieses Update schließt die neue WinPE-Version des aktualisierten Windows ADK, die neue Version des Configuration Manager-Clients, Treiber, Anpassungen ein. Der Standort ändern keine benutzerdefinierte Startimages.

### <a name="upgrade-from-configuration-manager-2012-to-current-branch"></a>Aktualisieren von Configuration Manager 2012 auf Current Branch

Wenn Sie Configuration Manager 2012 auf Current Branch aktualisieren, generiert der Standort die standardmäßigen Startimages neu. Dieses Update schließt die neue WinPE-Version des aktualisierten Windows ADK und die neue Version des Configuration Manager-Clients ein. Alle Anpassungen des Startimages bleiben unverändert. Der Standort ändern keine benutzerdefinierte Startimages.

### <a name="update-distribution-points-with-the-boot-image"></a>Aktualisieren von Verteilungspunkten mithilfe des Startabbilds

Wenn Sie die Aktion **Verteilungspunkte aktualisieren** aus dem Knoten **Startimages** in der Konsole verwenden, aktualisiert der Standort das Startimage des Ziels mit den Clientkomponenten, Treibern und Anpassungen.

Sie können das Startimage mit der aktuellen Version von WinPE aus dem Installationsverzeichnis des Windows ADK neu laden. Auf der Seite **Allgemein** des Assistenten für das Update von Verteilungspunkten werden folgende Informationen bereitgestellt:

- Die aktuelle auf dem Standortserver installierte Windows ADK-Version
- Die aktuelle Produktionsclientversion
- Die Windows ADK-Version von WinPE im Startimage
- Die Version des Configuration Manager-Clients im Startimage

Wenn die Versionen im Startimage nicht mehr aktuell sind, verwenden Sie die Option **Dieses Startimage mit der aktuellen Windows PE-Version aus dem Windows ADK neu laden**.

> [!Important]  
> Diese Aktion ist sowohl für Standard- als auch benutzerdefinierte Startimages verfügbar. Während dieses Vorgangs zum erneuten Laden des Startimages behält der Standort keine außerhalb von Configuration Manager vorgenommenen manuellen Anpassungen bei. Diese Anpassungen umfassen die Erweiterungen von Drittanbietern. Diese Option erstellt das Startimage mit der aktuellen Version von WinPE und der neuesten Clientversion neu. Nur die Konfigurationen, die Sie in den Eigenschaften des Startimages angeben, werden erneut angewendet. <!--SCCMDocs issue #1283-->

Der Knoten **Startimages** enthält auch eine neue Spalte für (**Clientversion**). In dieser Spalte können Sie die Configuration Manager-Clientversion in den einzelnen Startimages schnell anzeigen.

## <a name="customize-a-boot-image"></a><a name="BKMK_BootImageCustom"></a> Anpassen eines Startimages  

Wenn ein Startimage auf der WinPE-Version der unterstützten Version des Windows ADK basiert, können Sie es über die Konsole anpassen oder [ändern](#BKMK_ModifyBootImages). Wenn Sie einen Standort aktualisieren und eine neue Version von Windows ADK installieren, werden benutzerdefinierte Startimages nicht mit der neuen Version von Windows ADK aktualisiert. In diesem Fall können Sie die Startimages in der Configuration Manager-Konsole nicht anpassen. Diese funktionieren jedoch weiterhin wie vor dem Upgrade.  

Wenn ein Startimage auf einer anderen Version des an einem Standort installierten Windows ADK basiert, müssen Sie die Startimages anpassen. Passen Sie diese Startimages mit einer anderen Methode an, wie z.B. mit dem Befehlszeilenprogramm DISM (Deployment Image Servicing and Management). DISM ist Bestandteil des Windows ADK. Weitere Informationen zu Startimages finden Sie unter [Anpassen von Startimages](customize-boot-images.md).  

## <a name="add-a-boot-image"></a><a name="BKMK_AddBootImages"></a> Hinzufügen eines Startimages  

Bei einer Standortinstallation fügt Configuration Manager automatisch Startimages hinzu, die auf einer WinPE-Version aus der unterstützten Version von Windows ADK basieren. Abhängig von der Configuration Manager-Version können Sie Startimages hinzufügen, die auf einer anderen WinPE-Version aus der unterstützten Version von Windows ADK basieren. Es tritt ein Fehler auf, wenn Sie versuchen, ein Startimage hinzuzufügen, das eine nicht unterstützte Version von WinPE enthält. Die folgende Liste enthält die derzeit unterstützten Windows ADK- und Windows PE-Versionen:

| Windows-Typ | Unterstützte Versionen |
|--------------|--------------------|
| Windows ADK-Version | Windows ADK für Windows 10 |
| Windows PE-Versionen für Startimages, die über die Configuration Manager-Konsole angepasst werden können | Windows PE 10 |
| Unterstützte Windows PE-Versionen für Startimages, die *nicht* über die Configuration Manager-Konsole angepasst werden können | – Windows PE 3.1<sup>[Hinweis 1](#bkmk_note1)</sup> <br> – Windows PE 5 |

Verwenden Sie beispielsweise die Configuration Manager-Konsole, um Startimages, die auf Windows PE 10 basieren, aus dem Windows ADK für Windows 10 anzupassen. Passen Sie ein Startimage, das auf Windows PE 5 basiert, mithilfe der Version von DISM von einem anderen Computer aus dem Windows ADK für Windows 8 an. Fügen Sie anschließend das benutzerdefinierte Startimage zur Configuration Manager-Konsole hinzu. Weitere Informationen finden Sie in den folgenden Artikeln:

- [Anpassen von Startimages](customize-boot-images.md)
- [Unterstützung für Windows 10 ADK](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk)
- [DISM-unterstützte Plattformen](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms)

<a name="bkmk_note1"></a>

> [!NOTE]
> **Hinweis 1: Unterstützung für Windows PE 3.1**
>
> Fügen Sie Configuration Manager nur dann ein Startimage hinzu, wenn es auf Windows PE *Version 3.1* basiert. Führen Sie ein Upgrade von Windows AIK für Windows 7 (basierend auf Windows PE 3.0) mit der Ergänzung zu Windows AIK für Windows 7 SP1 (basierend auf Windows PE 3.1) durch. Laden Sie die Ergänzung zu Windows AIK für Windows 7 SP1 aus dem [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=5188)herunter.  

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und wählen Sie anschließend den Knoten **Startimages** aus.  

2. Wählen Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Erstellen** die Option **Startimage hinzufügen** aus. Dadurch wird der Assistent zum Hinzufügen des Startimages gestartet.  

3. Geben Sie auf der Seite **Datenquelle** die folgenden Optionen an:  

    - Geben Sie im Feld **Pfad** den Pfad der Startabbilddatei (WIM-Datei) an. Der angegebene Pfad muss ein gültiger Netzwerkpfad im UNC-Format sein. Beispiel: `\\ServerName\ShareName\BootImageName.wim`

    - Wählen Sie das Startabbild in der Dropdownliste **Startabbild** aus. Wenn die WIM-Datei mehrere Startimages enthält, wählen Sie das gewünschte Image aus.  

4. Geben Sie auf der Seite **Allgemein** folgende Optionen an:  

    - Geben Sie im Feld **Name** einen eindeutigen Namen für das Startabbild an.  

    - Geben Sie im Feld **Version** eine Versionsnummer für das Startabbild an.  

    - Geben Sie im Feld **Kommentar** anhand einer kurzen Beschreibung an, wie das Startimage verwendet werden soll.  

5. Schließen Sie den Assistenten ab.  

Das Startimage wird jetzt im Knoten **Startimage** aufgeführt. Bevor das Startimage für die Bereitstellung eines BS verwendet werden kann, müssen Sie dieses an Verteilungspunkte verteilen.

> [!Tip]  
> Im Knoten **Startimage** der Konsole, wird in der Spalte **Größe (KB)** die dekomprimierte Größe der einzelnen Startimages angezeigt. Wenn der Standort über das Netzwerk ein Startimage sendet, sendet er eine komprimierte Kopie. Diese Kopie ist in der Regel kleiner als die in der Spalte **Größe (KB)** aufgeführte Größer.  

## <a name="distribute-boot-images"></a><a name="BKMK_DistributeBootImages"></a> Verteilen von Startimages  

Startabbilder werden genau wie anderer Inhalt an Verteilungspunkte verteilt. Stellen Sie das Startimage an mindestens einem Verteilungspunkt bereit, bevor Sie ein BS bereitstellen oder Medien erstellen.

Weitere Informationen zum Verteilen eines Startimages finden Sie unter [Treiberpakete](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

Wenn Sie PXE verwenden möchten, um ein BS bereitzustellen, sollten Sie folgende Punkte beachten, bevor Sie das Startimage verteilen:  

- Konfigurieren Sie mindestens einen Verteilungspunkt zum Akzeptieren von PXE-Anforderungen.  
- Verteilen Sie sowohl ein x86- als auch ein x64-PXE-fähiges Startimage an mindestens einen PXE-fähigen Verteilungspunkt.  
- Configuration Manager verteilt die Startimages an den Ordner **RemoteInstall** auf dem PXE-fähigen Verteilungspunkt.  
  
Weitere Informationen zur Verwendung von PXE zum Bereitstellen von Betriebssystemen finden Sie unter [Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

## <a name="modify-a-boot-image"></a><a name="BKMK_ModifyBootImages"></a> Ändern eines Startimages  

Fügen Sie dem Image Gerätetreiber hinzu bzw. entfernen Sie Gerätetreiber daraus, oder bearbeiten Sie die Eigenschaften des Startimages. Die Treiber, die Sie hinzufügen oder entfernen, können Netzwerk- oder Speichertreiber umfassen. Berücksichtigen Sie beim Ändern von Startabbildern die folgenden Faktoren:  

- Bevor Sie Treiber dem Startimage hinzufügen, importieren Sie diese in den Gerätetreiberkatalog, und aktivieren Sie sie dort.  

- Wenn Sie ein Startimage ändern, wird keines der zugewiesenen Pakete geändert, auf die das Startimage verweist.  

- Nachdem Sie Änderungen an einem Startimage vorgenommen haben, müssen Sie dieses an den Verteilungspunkten **aktualisieren**, die bereits darüber verfügen. Durch diesen Prozess wird Clients die aktuelle Version des Startimages zur Verfügung gestellt. Weitere Informationen finden Sie unter [Verwalten der Inhalte, die Sie verteilt haben](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage).  

### <a name="modify-the-properties-of-a-boot-image"></a>Ändern der Eigenschaften eines Startimages  

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und wählen Sie anschließend den Knoten **Startimages** aus.  

2. Wählen Sie das Startabbild aus, das Sie ändern möchten.  

3. Klicken Sie auf dem Menüband auf der Registerkarte **Start** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

4. Legen Sie die folgenden Einstellungen fest, um das Verhalten des Startabbilds zu ändern:  

#### <a name="images"></a>Bilder

Klicken Sie auf der Registerkarte **Images** auf die Option **Neu laden**, wenn Sie die Eigenschaften des Startimages mithilfe eines externen Tools geändert haben.  

#### <a name="drivers"></a>Treiber

Fügen Sie auf der Registerkarte **Treiber** die Windows-Gerätetreiber hinzu, die zum Starten von WinPE erforderlich sind. Beachten Sie beim Hinzufügen von Gerätetreibern die folgenden Punkte:  

- Stellen Sie sicher, dass die zum Startimage hinzugefügten Treiber der Architektur des Startimages entsprechen.  

- Wählen Sie **Treiber ausblenden, die nicht mit der Architektur des Startimages übereinstimmen** aus, damit nur Treiber für die Architektur des Startimages angezeigt werden. Die Architektur des Treibers basiert auf der Architektur, die in der INF-Datei vom Hersteller angegeben ist.  

- Windows PE enthält bereits zahlreiche integrierte Treiber. Fügen Sie nur Netzwerk- und Speichertreiber hinzu, die nicht in WinPE enthalten sind.  

- Fügen Sie dem Startimage nur Netzwerk- und Speichertreiber hinzu, es sei denn, für WinPE sind andere Treiber erforderlich.  

- Wählen Sie **Treiber ausblenden, die in keiner Speicher- oder Netzwerkklasse enthalten sind (für Startimages)** aus, damit nur Speicher- und Netzwerktreiber angezeigt werden. Diese Option blendet auch andere Treiber aus, die in der Regel nicht für Startimages benötigt werden, z.B. Video- oder Modemtreiber.  

- Wählen Sie **Treiber ausblenden, die nicht digital signiert sind** aus, um Treiber auszublenden, die keine gültige digitale Signatur aufweisen.  

> [!NOTE]  
> Importieren Sie Gerätetreiber in den Treiberkatalog, bevor Sie sie einem Startimage hinzufügen. Informationen zum Importieren von Gerätetreibern finden Sie unter [Verwalten von Treibern](manage-drivers.md).  

#### <a name="customization"></a>Anpassung

Wählen Sie auf der Registerkarte **Anpassung** die folgenden Einstellungen aus:  

- Wählen Sie die Option **Prestart-Befehl aktivieren** aus, um einen Befehl anzugeben, der vor der Tasksequenz ausgeführt werden soll. Wenn Sie diese Option aktivieren, geben Sie auch die auszuführende Befehlszeile und alle unterstützenden Dateien an, die für den Befehl erforderlich sind.  

    > [!WARNING]  
    > Fügen Sie `cmd /c` am Anfang der Befehlszeile ein. Wenn Sie `cmd /c` nicht angeben, wird der Befehl nach der Ausführung nicht geschlossen. Die Bereitstellung wartet weiterhin auf den Abschluss des Befehls und startet keine weiteren konfigurierten Befehle oder Aktionen.  

    > [!TIP]  
    > Während der Erstellung der Tasksequenzmedien schreibt der Assistent die Paket-ID und die Prestart-Befehlszeile in die Datei **CreateTSMedia.log**. Diese Informationen enthalten die Werte aller Tasksequenzvariablen. Dieses Protokoll befindet sich auf dem Computer, auf dem die Configuration Manager-Konsole ausgeführt wird. Anhand dieser Protokolldatei können Sie die Werte für die Tasksequenzvariablen überprüfen.  

- Geben Sie unter **Windows PE-Hintergrund** an, ob Sie den WinPE-Standardhintergrund oder einen benutzerdefinierten Hintergrund verwenden möchten.  

- Konfigurieren Sie den **temporären Speicherbereich für Windows PE (MB)** . Hierbei handelt es sich um temporären Speicher (RAM), der von WinPE verwendet wird. Wenn eine Anwendung z. B. in WinPE ausgeführt wird und temporäre Dateien geschrieben werden müssen, werden die Dateien von WinPE an den temporären Speicherbereich im Arbeitsspeicher umgeleitet, um das Vorhandensein einer Festplatte zu simulieren. Für Geräte mit mehr als 1GB RAM sind dies standardmäßig 512MB, andernfalls 32MB.  

- Wählen Sie **Befehlsunterstützung aktivieren (nur Test)** aus, um während der Bereitstellung des Startabbilds über die Taste **F8** eine Eingabeaufforderung zu öffnen. Diese Option ist nützlich bei der Behandlung von Problemen, die beim Testen der Bereitstellung auftreten. Aus Sicherheitsgründen sollte diese Einstellung nicht in einer Produktionsbereitstellung verwendet werden.  

- **Standardtastaturlayout in WinPE festlegen:** <!--4910348-->Ab Version 1910 können Sie das Standardtastaturlayout für ein Startimage konfigurieren. Wenn Sie eine andere Sprache als „en-us“ auswählen, schließt Configuration Manager „en-us“ weiterhin in die verfügbaren Eingabegebietsschemas ein. Auf dem Gerät entspricht das anfängliche Tastaturlayout dem ausgewählten Gebietsschema, aber der Benutzer kann das Gerät bei Bedarf auf „en-us“ umstellen.

> [!Tip]
> Verwenden Sie das PowerShell-Cmdlet [Set-CMBootImage](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmbootimage?view=sccm-ps), um diese Einstellungen über ein Skript zu konfigurieren.

#### <a name="optional-components"></a>Optionale Komponenten

Geben Sie auf der Registerkarte **Optionale Komponenten** die Komponenten an, die Windows PE zur Verwendung mit Configuration Manager hinzugefügt werden. Weitere Informationen zu den verfügbaren optionalen Komponenten finden Sie unter [WinPE: Hinzufügen von Paketen (Referenz zu optionalen Komponenten)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference).  

Die folgenden Komponenten werden vom Configuration Manager benötigt und Startimages immer hinzugefügt:

- Skripts (WinPE-Scripting)
- Startup (WinPE-SecureStartup)
- Netzwerk (WinPE-WDS-Tools)
- Skripts (WinPE-WMI)

Die Liste **Komponenten** enthält zusätzliche Elemente, die diesem Startimage hinzugefügt werden. Um weitere Komponenten hinzuzufügen, wählen Sie das goldene Sternchen aus. Um eine Komponente zu entfernen, wählen Sie sie in der Liste aus und dann das rote X.

Die folgenden Komponenten werden häufig von Kunden verwendet werden:

- Microsoft .NET (WinPE-NetFX): Diese Komponente ist eine Voraussetzung für PowerShell. Sie ist eine der größeren optionalen Komponenten.  
- Windows PowerShell (WinPE-PowerShell): Diese Komponente erfordert .NET und fügt eingeschränkte Unterstützung für PowerShell hinzu. Wenn Sie benutzerdefinierte PowerShell-Skripts während der WinPE-Phase der Tasksequenz ausführen, fügen Sie diese Komponente hinzu. Es gibt andere Komponenten, die möglicherweise für andere PowerShell-Cmdlets erforderlich sind.
- HTML (WinPE-HTA): Wenn Sie benutzerdefinierte HTML-Anwendungen während der WinPE-Phase der Tasksequenz ausführen, fügen Sie diese Komponente hinzu.

Weitere Informationen zum Hinzufügen von Sprachen finden Sie unter [Konfigurieren von mehreren Sprachen für die Startimagebereitstellung](#BKMK_BootImageLanguage).

#### <a name="data-source"></a>Datenquelle

Führen Sie auf der Registerkarte **Datenquelle** für die folgenden Einstellungen ein Update aus:  

- Legen Sie **Imagepfad** und **Imageindex** fest, um die Quelldatei des Startimages zu ändern.  

- Wählen Sie **Verteilungspunkte entsprechend einem Zeitplan aktualisieren** aus, um einen Zeitplan dafür zu erstellen, wann der Standort das Startimage aktualisiert.  

- Wählen Sie **Inhalt in Clientcache belassen** aus, wenn Sie nicht möchten, dass der Inhalt dieses Pakets veraltet und aus dem Clientcache gelöscht wird, um Platz für anderen Inhalt zu schaffen.  

- Wählen Sie **Binäre differenzielle Replikation aktivieren** aus, um anzugeben, dass beim Update des Startimagepakets am Verteilungspunkt nur geänderte Dateien verteilt werden sollen. Durch diese Einstellung wird der Netzwerkdatenverkehr zwischen den Standorten minimiert. BDR ist besonders nützlich, wenn das Startimagepaket groß ist und die Änderungen relativ gering sind.  

- Wählen Sie **Dieses Startimage über den PXE-fähigen Verteilungspunkt bereitstellen** aus, wenn Sie das Startimage in einer PXE-fähigen Bereitstellung verwenden. Weitere Informationen finden Sie unter [Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

#### <a name="data-access"></a>Datenzugriff

Auf der Registerkarte **Datenzugriff** können Sie Einstellungen für die Paketfreigabe konfigurieren. Wenn in Ihrer Umgebung erforderlich, legen Sie für die Option **Den Inhalt in diesem Paket in eine Paketfreigabe auf Verteilungspunkten kopieren** fest. Sie können dann als zusätzliche Möglichkeit **Einen benutzerdefinierten Namen für die Paketfreigabe verwenden**, und geben Sie den benutzerdefinierten **Freigabenamen** an. Wenn Sie diese Option aktivieren, ist auf Verwaltungspunkten zusätzlicher Speicherplatz erforderlich. Dies gilt für alle Verteilungspunkte, die dieses Startimage erhalten.

#### <a name="distribution-settings"></a>Verteilungseinstellungen

Wählen Sie auf der Registerkarte **Verteilungseinstellungen** die folgenden Einstellungen aus:  

- Geben Sie in der Liste **Verteilungspriorität** die Prioritätsstufe an. Configuration Manager verwendet diese Prioritätsliste, wenn der Standort mehrere Pakete an denselben Verteilungspunkt verteilt.  

- Wählen Sie **Für bedarfsgesteuerte Verteilung aktivieren** aus, wenn Sie eine bedarfsgesteuerte Inhaltsverteilung an bevorzugte Verteilungspunkte aktivieren möchten. Wenn Sie diese Einstellung aktivieren und der von einem Client angeforderte Inhalt für das Paket auf keinem der Verteilungspunkte verfügbar ist, wird der Inhalt vom Verwaltungspunkt verteilt. Weitere Informationen finden Sie unter [On-demand content distribution (Bedarfsgesteuerte Inhaltsverteilung)](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#on-demand-content-distribution).  

- Geben Sie unter **Einstellungen für vorab bereitgestellten Verteilungspunkt** an, wie das Startimage an Verteilungspunkte verteilt werden soll, die für vorab bereitgestellten Inhalt aktiviert sind. Weitere Informationen zu vorab bereitgestelltem Inhalt finden Sie unter [Prestage content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  

#### <a name="content-locations"></a>Inhaltsorte

Wählen Sie auf der Registerkarte **Inhaltsorte** den Verteilungspunkt bzw. die Verteilungspunktgruppe aus, und führen Sie die folgenden Aktionen aus:  

- **Überprüfen:** Überprüfen Sie die Integrität des Startimagepakets am ausgewählten Verteilungspunkt bzw. in der ausgewählten Verteilungspunktgruppe.  

- **Neu verteilen:** Verteilen Sie das Startimage erneut an den ausgewählten Verteilungspunkt oder die ausgewählte Verteilungspunktgruppe.  

- **Entfernen:** Löschen Sie das Startimage vom ausgewählten Verteilungspunkt oder von der ausgewählten Verteilungspunktgruppe.  

#### <a name="security"></a>Sicherheit

Zeigen Sie auf der Registerkarte **Sicherheit** die Administratoren an, die über Berechtigungen für dieses Objekt verfügen.

## <a name="configure-a-boot-image-for-pxe"></a><a name="BKMK_BootImagePXE"></a> Konfigurieren eines Startimages für PXE  

Bevor Sie ein Startimage für eine PXE-basierte Bereitstellung verwenden können, konfigurieren Sie das Startimage für die Bereitstellung über einen PXE-fähigen Verteilungspunkt.  

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und wählen Sie anschließend den Knoten **Startimages** aus.  

2. Wählen Sie das Startabbild aus, das Sie ändern möchten.  

3. Klicken Sie auf dem Menüband auf der Registerkarte **Start** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

4. Wählen Sie auf der Registerkarte **Datenquelle** die Option **Dieses Startimage über den PXE-fähigen Verteilungspunkt bereitstellen**aus. Weitere Informationen finden Sie unter [Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

## <a name="configure-multiple-languages"></a><a name="BKMK_BootImageLanguage"></a> Konfigurieren mehrerer Sprachen

> [!TIP]
> Ab Version 1910 können Sie das Standardtastaturlayout in den Eigenschaften eines Startimages konfigurieren. Weitere Informationen finden Sie unter [Anpassung](#customization).<!--4910348-->

Startabbilder sind sprachneutral. Mit dieser Funktion können Sie ein Startimage verwenden, um den Text der Tasksequenz in WinPE in mehreren Sprachen anzuzeigen. Schließen Sie die entsprechende Sprachunterstützung von der Registerkarte **Optionale Komponenten** des Startimages ein. Legen Sie anschließend die entsprechende Tasksequenzvariable fest, um die anzuzeigende Sprache anzugeben. Die Sprache des bereitgestellten BS hängt von der Sprache in WinPE ab. Die Sprache, die dem Benutzer in WinPE angezeigt wird, wird wie folgt bestimmt:  

- Wenn ein Benutzer die Tasksequenz unter einem vorhandenen BS ausführt, wird von Configuration Manager automatisch die für den Benutzer konfigurierte Sprache verwendet. Wird die Tasksequenz automatisch als Folge eines obligatorischen Bereitstellungsstichtags ausgeführt, wird von Configuration Manager die Sprache des BS verwendet.  

- Für BS-Bereitstellungen, die PXE oder Medien verwenden, können Sie den Wert für die Sprach-ID in der Variablen **SMSTSLanguageFolder** als Teil eines Prestart-Befehls festlegen. Wenn der Computer mit WinPE gestartet wird, werden Meldungen in der Sprache angezeigt, die Sie in der Variablen angegeben haben. Falls beim Zugreifen auf die Sprachressourcendatei im angegebenen Ordner ein Fehler auftritt oder Sie die Variable nicht festlegen, werden in WinPE Meldungen in der Standardsprache angezeigt.  

    > [!NOTE]  
    > Wenn Sie das Medium mit einem Kennwort schützen, wird der Text, mit dem Benutzer zur Eingabe des Kennworts aufgefordert werden, immer in der WindPE-Sprache angezeigt.  

Verwenden Sie das folgende Verfahren zum Festlegen der WinPE-Sprache für BS-Bereitstellungen, die per PXE oder Startmedium initiiert werden.  

### <a name="set-the-windows-pe-language-for-a-pxe-or-media-initiated-os-deployment"></a>Festlegen der Windows PE-Sprache für eine PXE oder medieninitiierte Betriebssystembereitstellung  

1. Überprüfen Sie vor dem Aktualisieren des Startimages, ob sich die richtige Tasksequenz-Ressourcendatei („tsres.dll“) im entsprechenden Sprachordner auf dem Standortserver befindet. Die Ressourcendatei für Englisch befindet sich z.B. am folgenden Speicherort: `<ConfigMgrInstallationFolder>\OSD\bin\x64\00000409\tsres.dll`  

2. Legen Sie als Teil des Prestart-Befehls die Umgebungsvariable **SMSTSLanguageFolder** auf die gewünschte Sprach-ID fest. Die Sprach-ID muss im Dezimalformat angegeben werden (nicht im Hexadezimalformat). Wenn Sie die Sprach-ID auf Englisch festlegen möchten, geben Sie z.B. den Dezimalwert **1033** an, und nicht den Hexadezimalwert 00000409 für den Ordnernamen.  
