---
title: Verwenden von PXE für die Betriebssystembereitstellung über das Netzwerk
titleSuffix: Configuration Manager
description: Verwenden Sie mit PXE initiierte Betriebssystembereitstellungen, um das Betriebssystem eines Computers zu aktualisieren oder eine neue Version von Windows auf einem neuen Computer zu installieren.
ms.date: 02/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: da5f8b61-2386-4530-ad54-1a5c51911f07
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cff249bf5289ebcf354851258b5c9d598314ce3b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709058"
---
# <a name="use-pxe-to-deploy-windows-over-the-network-with-configuration-manager"></a>Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Bei einer mithilfe von PXE (Pre-Boot eXecution Environment) ausgelösten Betriebssystembereitstellung in Configuration Manager werden Betriebssysteme von Clients über das Netzwerk angefordert und bereitgestellt. In diesem Bereitstellungsszenario senden Sie das Betriebssystemimage und die Startimages an einen PXE-fähigen Verteilungspunkt.

> [!NOTE]  
> Wenn Sie eine Betriebssystembereitstellung nur für x64-BIOS-Computer erstellen, müssen das x64-Startimage und das x86-Startimage auf dem Verteilungspunkt verfügbar sein.

Sie können über PXE initiierte Bereitstellungen in den folgenden Szenarios verwenden:

- [Aktualisieren eines vorhandenen Computers mit einer neuen Version von Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [Installieren einer neuen Version von Windows auf einem neuen Computer (Bare-Metal)](install-new-windows-version-new-computer-bare-metal.md)  

Führen Sie die Schritte in einem der Szenarios für die Betriebssystembereitstellung aus, und bereiten Sie dann die von PXE ausgelösten Bereitstellungen anhand der Abschnitte in diesem Artikel vor.

> [!WARNING]
> Wenn Sie PXE-Bereitstellungen verwenden und Gerätehardware mit dem Netzwerkadapter als erstes Startgerät konfigurieren, können diese Geräte automatisch und ohne Benutzerinteraktion eine Tasksequenz für die Betriebssystembereitstellung starten. Diese Konfiguration wird nicht durch die Bereitstellungsüberprüfung verwaltet. Während diese Konfiguration möglicherweise den Prozess vereinfachen und die Benutzerinteraktion reduzieren kann, erhöht sie das Risiko, dass für das Gerät versehentlich ein Reimaging durchgeführt wird.

## <a name="configure-at-least-one-distribution-point-to-accept-pxe-requests"></a><a name="BKMK_Configure"></a> Konfigurieren mindestens eines Verteilungspunkts zum Akzeptieren von PXE-Anforderungen

Zum Bereitstellen von Betriebssystemen für Configuration Manager-Clients, die PXE-Startanforderungen ausführen, müssen Sie mindestens einen Verteilungspunkt so konfigurieren, dass er PXE-Anforderungen akzeptiert. Sobald der Verteilungspunkt konfiguriert ist, reagiert er auf PXE-Startanforderungen und ermittelt die geeigneten Bereitstellungsaktionen. Weitere Informationen finden Sie unter [Installieren oder Modifizieren eines Verteilungspunkts](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).  

> [!NOTE]  
> Wenn Sie einen einzelnen PXE-fähigen Verteilungspunkt so konfigurieren, dass dieser mehrere Subnetze unterstützt, werden keine DHCP-Optionen unterstützt. Konfigurieren Sie IP-Hilfsprogramme auf den Routern, um zuzulassen, dass PXE-Anforderungen an Ihren PXE-fähigen Verteilungspunkt weitergeleitet werden.
>
> In Version 1810 wird die Verwendung des PXE-Antwortdiensts ohne WDS auf Servern, auf denen auch ein DHCP-Server ausgeführt wird, nicht unterstützt.
>
> Ab der Version 1902 gilt: Wenn Sie einen PXE-Antwortdienst auf einem Verteilungspunkt ohne Windows-Bereitstellungsdienst aktivieren, kann er sich nun auf dem gleichen Server befinden wie der DHCP-Dienst.<!--3734270, SCCMDocs-pr #3416--> Fügen Sie die folgenden Einstellungen hinzu, um diese Konfiguration zu unterstützen:  
>
> - Setzen Sie den DWord-Wert **DoNotListenOnDhcpPort** auf `1` im folgenden Registrierungsschlüssel: `HKLM\Software\Microsoft\SMS\DP`.
> - Legen Sie die DHCP-Option 60 auf `PXEClient` fest.  
> - Starten Sie die Dienste „SCCMPXE“ und „DHCP“ auf dem Server neu.  

## <a name="prepare-a-pxe-enabled-boot-image"></a>Vorbereiten eines PXE-fähigen Startabbilds

Um PXE zum Bereitstellen eines Betriebssystems zu verwenden, muss sowohl ein PXE-fähiges x86-Startimage als auch ein PXE-fähiges x64-Startimage an mindestens einen PXE-fähigen Verteilungspunkt verteilt sein. Verwenden Sie die Informationen zum Aktivieren von PXE in einem Startimage, verteilen Sie das Startimage an Verteilungspunkte:

- Um PXE für ein Startabbild zu aktivieren, wählen Sie in den Startabbildeinstellungen auf der Registerkarte **Datenquelle** die Option **Dieses Startabbild über den PXE-fähigen Verteilungspunkt bereitstellen** aus.

- Wenn Sie die Eigenschaften für das Startabbild ändern, aktualisieren Sie das Startabbild, und verteilen Sie es erneut an Verteilungspunkte. Weitere Informationen finden Sie unter [Distribute content (Verteilen von Inhalt)](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

## <a name="manage-duplicate-hardware-identifiers"></a>Verwalten von in Konflikt stehenden Datensätzen bei Configuration Manager-Clients

Configuration Manager erkennt möglicherweise mehrere Computer als ein einziges Gerät, wenn sie über doppelte SMBIOS-Attribute verfügen oder Sie einen gemeinsam genutzten Netzwerkadapter verwenden. Sie können diese Probleme verringern, indem Sie doppelte Hardwarebezeichner in den Hierarchieeinstellungen verwalten. Weitere Informationen finden Sie unter [Verwalten von in Konflikt stehenden Datensätzen bei Configuration Manager-Clients](../../core/clients/manage/manage-clients.md#manage-duplicate-hardware-identifiers).

## <a name="create-an-exclusion-list-for-pxe-deployments"></a><a name="BKMK_PXEExclusionList"></a> Erstellen einer Ausschlussliste für PXE-Bereitstellungen

> [!Note]  
> Unter bestimmten Bedingungen ist der Prozess zum [Verwalten von in Konflikt stehenden Datensätzen bei Configuration Manager-Clients](../../core/clients/manage/manage-clients.md#manage-duplicate-hardware-identifiers) ggf. einfacher.<!-- SCCMDocs issue 802 -->
>
> Das jeweilige Verhalten kann in manchen Szenarien zu abweichenden Ergebnissen führen. Die Ausschlussliste startet niemals einen Client mit der aufgeführten MAC-Adresse.
>
> Die Liste doppelter IDs sucht die Tasksequenzrichtlinie für einen Client nicht anhand der MAC-Adresse. Wenn sie mit der SMBIOS-ID übereinstimmt oder eine Tasksequenzrichtlinie für unbekannte Computer vorhanden ist, startet der Client trotzdem.

Wenn Sie Betriebssysteme mit PXE bereitstellen, können Sie für jeden Verteilungspunkt eine Ausschlussliste erstellen. Fügen Sie der Ausschlussliste die MAC-Adressen der Computer hinzu, die vom Verteilungspunkt ignoriert werden sollen. Aufgeführte Computer empfangen nicht die Bereitstellungstasksequenzen, die Configuration Manager für die PXE-Bereitstellung verwendet.

### <a name="process-to-create-the-exclusion-list"></a>Prozess zum Erstellen der Ausschlussliste

1. Erstellen Sie eine Textdatei auf dem Verteilungspunkt, der für PXE aktiviert ist. Geben Sie dieser Textdatei beispielsweise den Namen **pxeExceptions.txt**.  

2. Verwenden Sie einen Standardtexteditor wie Editor, und fügen Sie die MAC-Adressen der Computer hinzu, die vom PXE-fähigen Verteilungspunkt ignoriert werden sollen. Trennen Sie die MAC-Adresswerte mit Kommas, und geben Sie jede Adresse in einer eigenen Zeile ein. Beispiel: `01:23:45:67:89:ab`  

3. Speichern Sie die Textdatei auf dem PXE-fähigen Verteilungspunkt-Standortsystemserver. Die Textdatei kann auf dem Server an einem beliebigen Speicherort gespeichert werden.  

4. Bearbeiten Sie die Registrierung des PXE-fähigen Verteilungspunkts so, dass der Registrierungsschlüssel **MACIgnoreListFile** erstellt wird. Fügen Sie den Zeichenfolgenwert des vollständigen Pfads der Textdatei dem PXE-fähigen Standortsystemserver mit dem Verteilungspunkt hinzu. Verwenden Sie den folgenden Registrierungspfad:  

    `HKLM\Software\Microsoft\SMS\DP`  

    > [!WARNING]  
    > Durch unsachgemäße Verwendung des Registrierungs-Editors können schwerwiegende Fehler auftreten, die möglicherweise eine Neuinstallation von Windows erforderlich machen. Microsoft kann nicht garantieren, dass Probleme, die aufgrund unsachgemäßer Verwendung des Registrierungs-Editors entstehen, behoben werden können. Die Verwendung des Registrierungs-Editors erfolgt auf Ihr eigenes Risiko.  

5. Starten Sie den WDS-Dienst oder den PXE-Antwortdienst neu, nachdem Sie die Registrierungsänderung vorgenommen haben. Der Server muss nicht neu gestartet werden.<!--512129-->  

## <a name="ramdisk-tftp-block-size-and-window-size"></a><a name="BKMK_RamDiskTFTP"></a> RamDisk-TFTP-Blockgröße und Fenstergröße

Sie können die Größe des RamDisk-TFTP-Blocks und des Fensters für PXE-fähige Verteilungspunkte anpassen. Wenn Sie Ihr Netzwerk angepasst haben, kann eine übermäßige Block- oder Fenstergröße zu einem Timeout beim Herunterladen des Startimages führen. Durch Anpassen der Größe des RamDisk-TFTP-Blocks und des Fensters können Sie den TFTP-Datenverkehr bei Verwendung von PXE für Ihre spezifischen Netzwerkanforderungen optimieren. Um die effizienteste Einstellung zu ermitteln, müssen Sie die benutzerdefinierten Einstellungen in Ihrer Umgebung testen. Weitere Informationen finden Sie unter [Customize the RamDisk TFTP block size and window size on PXE-enabled distribution points (Anpassen der RamDisk-TFTP-Blockgröße und der Fenstergröße auf PXE-fähigen Verteilungspunkten)](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP).

## <a name="configure-deployment-settings"></a>Konfigurieren von Bereitstellungseinstellungen

Um eine PXE-initiierte Betriebssystembereitstellung zu verwenden, müssen Sie die Bereitstellung konfigurieren, um das Betriebssystem für PXE-Startanforderungen verfügbar zu machen. Konfigurieren Sie die verfügbaren Betriebssysteme in den Bereitstellungseigenschaften auf der Registerkarte **Bereitstellungseinstellungen**. Wählen Sie für die Einstellung **Verfügbar machen für** eine der folgenden Optionen aus:

- Configuration Manager-Clients, Medien und PXE

- Nur Medien und PXE

- Nur Medien und PXE (ausgeblendet)

## <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> Bereitstellen der Tasksequenz

Stellen Sie das Betriebssystem in einer Zielauflistung bereit. Weitere Informationen finden Sie unter [Deploy a task sequence](deploy-a-task-sequence.md). Beim Bereitstellen von Betriebssystemen unter Verwendung von PXE können Sie konfigurieren, ob die Bereitstellung erforderlich oder verfügbar ist.

- **Erforderliche Bereitstellung**: Bei erforderlichen Bereitstellungen wird PXE ohne jegliches Eingreifen des Benutzers verwendet. Der Benutzer kann den PXE-Start nicht umgehen. Wenn ein Benutzer den PXE-Startvorgang jedoch abbricht, bevor der PXE-Verteilungspunkt antwortet, wird das Betriebssystem nicht bereitgestellt.

- **Verfügbare Bereitstellung**: Bei verfügbaren Bereitstellungen muss der Benutzer am Zielcomputer anwesend sein. Ein Benutzer muss die Taste **F12** drücken, um den PXE-Startvorgang fortzusetzen. Wenn der Benutzer nicht anwesend ist und nicht die Taste **F12** drücken kann, startet der Computer mit dem aktuellen Betriebssystem oder vom nächsten verfügbaren Startgerät.

Sie können eine erforderliche PXE-Bereitstellung erneut bereitstellen, indem Sie den Status der letzten PXE-Bereitstellung löschen, die einer Configuration Manager-Sammlung oder einem Computer zugewiesen ist. Weitere Informationen zur Aktion **Erforderliche PXE-Bereitstellungen löschen** finden Sie unter [Verwalten von Clients](../../core/clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode) oder [Verwalten von Sammlungen](../../core/clients/manage/collections/manage-collections.md#bkmk_device). Mit dieser Aktion wird der Status der Bereitstellung zurückgesetzt, und die letzten erforderlichen Bereitstellungen werden erneut installiert.

> [!IMPORTANT]  
> Das PXE-Protokoll ist nicht sicher. Stellen Sie sicher, dass sich der PXE-Server und der PXE-Client in einem physisch sicheren Netzwerk (z.B. in einem Rechenzentrum) befinden, um unbefugten Zugriff auf den Standort zu verhindern.

## <a name="how-the-boot-image-is-selected-for-pxe"></a>Auswählen des Startimages für PXE

Wenn ein Client mit PXE gestartet wird, stellt Configuration Manager ein Startimage für den Client bereit. Configuration Manager verwendet ein Startimage mit einer exakten architektonischen Übereinstimmung. Ist dies nicht der Fall, verwendet Configuration Manager ein Startabbild mit einer kompatiblen Architektur.

In der folgenden Liste finden Sie Informationen dazu, wie ein Startimage für Clients ausgewählt wird, die mit PXE gestartet werden:  

1. Configuration Manager sucht in der Standortdatenbank nach dem Systemdatensatz, bei dem die MAC-Adresse oder das SMBIOS des Clients übereinstimmt, der gestartet werden soll.  

    > [!NOTE]  
    > Wenn ein Computer, der einem Standort zugewiesen ist, für einen anderen Standort mit PXE gestartet wird, werden die Richtlinien für den Computer nicht angezeigt. Wenn z.B. ein Client bereits Standort A zugewiesen ist, können ein Verwaltungspunkt und ein Verteilungspunkt an Standort B nicht auf die Richtlinien von Standort A zugreifen. Der Client wird deshalb nicht erfolgreich mit PXE gestartet.  

2. Configuration Manager sucht nach Tasksequenzen, die für den Systemdatensatz in Schritt 1 bereitgestellt werden.  

3. In der Liste mit Tasksequenzen in Schritt 2 sucht Configuration Manager nach einem Startimage mit einer Architektur, die mit der des Clients übereinstimmt, der gestartet werden soll. Wenn ein Startimage mit derselben Architektur gefunden wird, wird dieses Startimage verwendet.  

    Sollten mehrere Startimages gefunden werden, wird die Tasksequenz mit der *höchsten* oder neuesten Bereitstellungs-ID verwendet. In einer Hierarchie mit mehreren Standorten hat der Standort mit dem *höheren* Buchstaben Vorrang. Beispiel: Wenn beide Standorte ansonsten identisch sind, wird anstelle der Bereitstellung des Standorts AAA vom Vortag eine Bereitstellung des Standorts ZZZ verwendet, die ein Jahr alt ist.<!-- SCCMDocs issue 877 -->  

4. Wenn kein Startimage mit derselben Architektur gefunden wird, sucht Configuration Manager nach einem Startimage, das mit der Architektur des Clients kompatibel ist. Hierfür wird die Liste der Tasksequenzen in Schritt 2 verwendet. Ein 64-Bit-BIOS/MBR-Client ist beispielsweise mit 32-Bit- und 64-Bit-Startimages kompatibel. Ein 32-Bit-BIOS/MBR-Client ist nur mit 32-Bit-Startimages kompatibel. UEFI-Clients sind nur mit entsprechender Architektur kompatibel. Ein 64-Bit-UEFI-Client ist nur mit 64-Bit-Startimages kompatibel, und ein 32-Bit-UEFI-Client ist nur mit 32-Bit-Startimages kompatibel.
