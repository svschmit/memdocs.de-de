---
title: Verwalten von Betriebssystemimages
titleSuffix: Configuration Manager
description: Informationen zu den Methoden zum Verwalten von in Windows-Imagedateien (WIM) gespeicherten Betriebssystemimages.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: fab13949-371c-4a4c-978e-471db1e54966
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2f8b8a45ff83ce903f5737c94144e6ca5ab50826
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697652"
---
# <a name="manage-os-images-with-configuration-manager"></a>Verwalten von Betriebsimages mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Betriebssystemimages in Configuration Manager werden im Dateiformat WIM (Windows Imaging) gespeichert. Es handelt sich bei diesen Images um eine komprimierte Sammlung von Referenzdateien und -ordnern, die zum Installieren und Konfigurieren eines neuen Betriebssystems auf einem Computer verwendet werden. Für viele Betriebssystembereitstellungsszenarios ist ein Betriebssystemimage erforderlich.


## <a name="os-image-types"></a>Betriebssystemimagetypen

Sie können ein [Standardbetriebssystemimage](#default-image) verwenden oder das Betriebssystemimage über einen von Ihnen konfigurierten [Referenzcomputer](#bkmk_capture) erstellen. Wenn Sie einen Referenzcomputer erstellen, müssen Sie Betriebssystemdateien, Treiber, Unterstützungsdateien, Softwareupdates, Tools und Anwendungen zum Betriebssystem hinzufügen. Erfassen Sie diesen anschließend, um eine Imagedatei zu erstellen.

### <a name="default-image"></a>Standardabbild

Die Installationsdateien für Windows umfassen das Standardbetriebssystemimage. Dieses Image ist ein allgemeines Betriebssystemimage, das mehrere Standardtreiber enthält. Wenn Sie das Standardbetriebssystemimage verwenden, führen Sie die Tasksequenzschritte aus, um die Apps zu installieren und andere Konfigurationen zu erstellen, nachdem das Betriebssystem auf einem Gerät installiert wurde. Suchen Sie das Standardbetriebssystemimage in den Windows-Quelldateien: `\Sources\install.wim`.  

#### <a name="default-image-advantages"></a>Vorteile von Standardimages

- Das Image ist kleiner als ein erfasstes Image.  

- Das Installieren von Apps und Konfigurationen mithilfe von Tasksequenzschritten ist dynamischer. Sie können z. B. die Konfigurationen und Apps ändern, die in der Tasksequenz installiert werden, ohne ein Reimaging für das Gerät durchführen zu müssen.  

#### <a name="default-image-disadvantages"></a>Nachteile von Standardimages

- Die Installation des Betriebssystems dauert ggf. länger. Die Anwendungsinstallation und andere Konfigurationen werden erst ausgeführt, wenn die Betriebssysteminstallation abgeschlossen ist.  


### <a name="captured-image-from-a-reference-computer"></a><a name="bkmk_capture"></a> Erfasstes Image von einem Referenzcomputer

Erstellen Sie einen Referenzcomputer mit dem gewünschten Betriebssystem, um ein benutzerdefiniertes Betriebssystemimage zu erstellen. Installieren Sie anschließend Anwendungen, und konfigurieren Sie die Einstellungen. Erfassen Sie dann das Betriebssystemimage auf dem Referenzcomputer, um die WIM-Datei zu erstellen. Sie können den Referenzcomputer manuell erstellen oder eine Tasksequenz zum Automatisieren einiger oder aller Buildschritte verwenden. Weitere Informationen finden Sie unter [Customize OS images (Anpassen von Betriebssystemimages)](customize-operating-system-images.md).  

#### <a name="captured-image-advantages"></a>Vorteile von erfassten Images

- Die Installation kann schneller als bei Verwendung des Standardbilds sein. Beispielsweise können Anwendungen mit dem erfassten Betriebssystemimage vorinstalliert werden. Dann müssen Sie diese Anwendungen nicht später über die Tasksequenzschritte installieren.  

#### <a name="captured-image-disadvantages"></a>Nachteile von erfassten Images

- Das Bild ist möglicherweise größer als das Standardimage.  

- Es muss ein neues Image erstellt werden, wenn Updates für Anwendungen und Tools erforderlich sind.  


## <a name="add-an-os-image"></a><a name="BKMK_AddOSImages"></a> Hinzufügen eines Betriebssystemimage  

Bevor Sie ein Betriebssystemimage verwenden können, fügen Sie es zunächst Ihrem Configuration Manager-Standort hinzu.

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und wählen Sie anschließend den Knoten **Betriebssystemabbilder** aus.  

2. Klicken Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Erstellen** auf **Betriebssystemabbild hinzufügen**. Dadurch wird der Assistent zum Hinzufügen des Betriebssystemimages gestartet.  

3. Geben Sie auf der Seite **Datenquelle** die folgenden Informationen an:

    - Den **Netzwerkpfad** zur Betriebssystemimagedatei. Beispiel: `\\server\share\path\image.wim`.

    - Aktivieren Sie das Kontrollkästchen **Index für ein bestimmtes Image aus der angegebenen WIM-Datei extrahieren**, und wählen Sie einen Imageindex aus der Liste aus.<!--3719699--> Ab Version 1902 importiert diese Option automatisch einen einzelnen Index, anstatt alle Imageindizes in die Datei zu importieren. Die Verwendung dieser Option resultiert in einer kleineren Imagedatei und schnellerer Offlinewartung. Sie unterstützt außerdem den Prozess zum [Optimieren der Imagewartung](#bkmk_resetbase) für kleinere Imagedateien nach der Anwendung von Softwareupdates.  

        > [!Note]  
        > Die Quellimagedatei wird nicht von Configuration Manager geändert. Configuration Manager erstellt eine neue Imagedatei im selben Quellverzeichnis.
        >
        > Dieser Extraktionsprozess kann bei sehr großen Imagedateien (z. B. über 60 GB) fehlschlagen. Die DISM-Fehlermeldung lautet folgendermaßen: `Not enough storage is available to process this command.`. Die von Configuration Manager verwendete Befehlszeile befindet sich in den Dateien „smsprov.log“ und „dism.log“. Führen Sie denselben Befehl manuell aus, und importieren Sie dann das Image.<!-- SCCMDocs-pr issue 3502 -->  

    - Ab Version 1906: Wenn Sie Inhalte eines Clients vorab zwischenspeichern möchten, geben Sie die **Architektur** und **Sprache** des Images an. Weitere Informationen finden Sie unter [Konfigurieren des zwischengespeicherten Inhalts](../deploy-use/configure-precache-content.md).<!--4224642-->  

4. Geben Sie auf der Seite **Allgemein** die folgenden Informationen an. Diese Informationen sind für Identifikationszwecke hilfreich, wenn Sie über mehrere Betriebssystemimages verfügen.  

    - **Name:** ein eindeutiger Name für das Image. Standardmäßig wird der Name anhand des Namens der WIM-Datei festgelegt.  

    - **Version:** Ein optionaler Versionsbezeichner. Diese Eigenschaft muss nicht der Betriebssystemversion des Images entsprechen. Hierfür wird häufig die Paketversion des Unternehmens verwendet.  

    - **Kommentar**: Eine kurze, optionale Beschreibung.  

5. Schließen Sie den Assistenten ab.  

Die PowerShell-Cmdlet-Entsprechung dieses Konsolen-Assistenten finden Sie unter [New-CMOperatingSystemImage](/powershell/module/configurationmanager/new-cmoperatingsystemimage?view=sccm-ps).

Verteilen Sie als nächstes das Betriebssystemimage an Verteilungspunkte.  


## <a name="distribute-content-to-distribution-points"></a><a name="BKMK_DistributeBootImages"></a> Verteilen von Inhalten an Verteilungspunkte  

Verteilen Sie die Betriebssystemimages wie jeden anderen Inhalt an Verteilungspunkte. Verteilen Sie das Betriebssystemimage an mindestens einen Verteilungspunkt, bevor Sie die Tasksequenz bereitstellen. Weitere Informationen finden Sie unter [Distribute content (Verteilen von Inhalt)](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  


[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]


## <a name="prepare-the-os-image-for-multicast-deployments"></a><a name="BKMK_OSImageMulticast"></a> Vorbereiten des Betriebssystemimages für Multicastbereitstellungen  

Verwenden Sie Multicastbereitstellungen, damit mehrere Computer gleichzeitig ein Betriebssystemimage herunterladen können. Es lädt nicht jeder Client eine Kopie des Image über eine separate Verbindung vom Verteilungspunkt herunter, sondern das Image wird vom Verteilungspunkt per Multicast an Clients übertragen. Wenn Sie die Betriebssystembereitstellungsmethode verwenden, [um Windows per Multicast über das Netzwerk bereitzustellen](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md), konfigurieren Sie das Betriebssystemimage, sodass es Multicast unterstützt. Verteilen Sie anschließend das Image an multicastfähige Verteilungspunkte.

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und wählen Sie anschließend den Knoten **Betriebssystemabbilder** aus.  

2. Wählen Sie das Betriebssystemimage aus, das Sie an den multicastfähigen Verteilungspunkt verteilen möchten.  

3. Klicken Sie auf dem Menüband auf der Registerkarte **Start** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

4. Wechseln Sie zur die Registerkarte **Verteilungseinstellungen**, und konfigurieren Sie die folgenden Optionen:  

    - **Dieses Paket darf per Multicast (nur WinPE) übertragen werden:** Wählen Sie diese Option aus, wenn Configuration Manager mithilfe von Multicast Betriebssystemimages gleichzeitig bereitstellen soll.  

    - **Multicastpakete verschlüsseln:** Geben Sie an, ob das Image vor der Übertragung an den Verteilungspunkt durch den Standort verschlüsselt werden soll. Verwenden Sie diese Option, wenn das Image vertrauliche Informationen enthält. Wenn das Image nicht verschlüsselt ist, werden dessen Inhalte in Klartext auf dem Netzwerk angezeigt. Dann könnte ein nicht autorisierter Benutzer die Imageinhalte abfangen und abrufen.  

    - **Dieses Paket nur per Multicast übertragen:** Geben Sie an, ob das Image vom Verteilungspunkt nur während einer Multicastsitzung bereitgestellt werden soll.  

         Bei Auswahl der Option **Transfer this package only via multicast** (Dieses Paket nur per Multicast übertragen) müssen Sie auch Bereitstellungsoption für die Tasksequenz auf **Inhalt lokal herunterladen, wenn dies für die ausgeführte Tasksequenz erforderlich ist** festlegen. Weitere Informationen finden Sie unter [Deploy a task sequence](../deploy-use/deploy-a-task-sequence.md).  

5. Klicken Sie auf **OK**, um die Einstellungen zu speichern und die Imageeigenschaften zu schließen.