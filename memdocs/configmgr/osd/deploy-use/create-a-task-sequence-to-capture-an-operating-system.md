---
title: Erstellen einer Tasksequenz zum Erfassen eines Betriebssystems
titleSuffix: Configuration Manager
description: Eine Tasksequenz zum Erstellen und Erfassen erstellt einen Referenzcomputer, der spezifische Treiber und Softwareupdates zusammen mit dem Betriebssystem enthalten kann.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 25e4ac68-0e78-4bbe-b8fc-3898b372c4e8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ceb63560c6000b1a76116d0791c98219a66066b8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707388"
---
# <a name="create-a-task-sequence-to-capture-an-os"></a>Erstellen einer Tasksequenz zum Erfassen eines Betriebssystems

*Gilt für: Configuration Manager (Current Branch)*

Wenn Sie in Operations Manager eine Tasksequenz zum Bereitstellen eines Betriebssystems auf einem Computer verwenden, installiert der Computer das Betriebssystemimage, das Sie in der Tasksequenz angeben. Sie können das Betriebssystemimage anpassen, damit es spezifische Treiber, Anwendungen und Softwareupdates enthält. Verwenden Sie zuerst eine Tasksequenz zum Erstellen und Erfassen, um einen Referenzcomputer zu erstellen. Erfassen Sie dann das Betriebssystemimage von diesem Referenzcomputer. Wenn Sie bereits über einen Referenzcomputer für die Erfassung verfügen, erstellen Sie eine benutzerdefinierte Tasksequenz, um das Betriebssystem zu erfassen.

## <a name="about-the-build-and-capture-task-sequence"></a><a name="BKMK_BuildCaptureTS"></a> Informationen zur Tasksequenz zum Erstellen und Erfassen

Die Tasksequenz zum Erstellen und Erfassen:

- Partitioniert und formatiert den Referenzcomputer
- Installiert das Betriebssystem
- Installiert den Configuration Manager-Client
- Installiert Anwendungen
- Wendet Softwareupdates an
- Erfasst das Betriebssystem vom Referenzcomputer

Die Pakete, die der Tasksequenz zugeordnet sind, z. B. Anwendungen, müssen auf Verteilungspunkten verfügbar sein, bevor Sie die Tasksequenz für die Erstellung und Erfassung bereitstellen.

## <a name="requirements"></a><a name="BKMK_CreatePackages"></a> Anforderungen

Bevor Sie eine Tasksequenz zum Installieren eines Betriebssystems verwenden, sollten Sie sicherstellen, dass die folgenden Komponenten vorhanden sind:  

### <a name="required"></a>Erforderlich

- [Startimage](../get-started/manage-boot-images.md)

- [Betriebssystemimage](../get-started/manage-operating-system-images.md)

### <a name="required-if-used"></a>Erforderlich (sofern verwendet)

- [Treiberpakete](../get-started/manage-drivers.md), die die erforderlichen Windows-Treiber zur Unterstützung von Hardware auf dem Referenzcomputer enthalten. Weitere Informationen zu Tasksequenzschritten zum Verwalten von Treibern finden Sie unter [Verwenden von Tasksequenzen zum Installieren von Gerätetreibern](../get-started/manage-drivers.md#BKMK_TSDrivers).

- [Softwareupdates](../../sum/get-started/synchronize-software-updates.md)

- [Anwendungen](../../apps/deploy-use/create-applications.md)

## <a name="create-a-build-and-capture-task-sequence"></a><a name="BKMK_CreateBuildCaptureTS"></a> Erstellen einer Tasksequenz zum Erstellen und Erfassen

Gehen Sie wie folgt vor, um eine Tasksequenz zum Erstellen eines Referenzcomputers und zum Erfassen eines Betriebssystems zu verwenden.

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und wählen Sie anschließend den Knoten **Tasksequenzen** aus.  

1. Wählen Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Erstellen** die Option **Tasksequenz erstellen** aus, um den Tasksequenzerstellungs-Assistenten zu starten.  

1. Wählen Sie auf der Seite **Neue Tasksequenz erstellen** die Option **Referenz-Betriebssystemabbild erstellen und erfassen**aus.  

1. Geben Sie auf der Seite **Informationen zur Tasksequenz** die folgenden Einstellungen an:  

    - **Tasksequenzname:** Geben Sie einen Namen zur Identifikation der Tasksequenz an.  

    - **Beschreibung:** Geben Sie eine optionale Beschreibung für die Tasksequenz an. Beschreiben Sie beispielsweise das Betriebssystem, dass die Tasksequenz erstellt.

    - **Startimage:** Legen Sie das Startimage fest, das mit dieser Tasksequenz verwendet werden soll.  

        > [!IMPORTANT]  
        > Die Architektur des Startabbilds muss kompatibel mit der Hardwarearchitektur des Zielcomputers sein.  

1. Legen Sie die folgenden Einstellungen auf der Seite **Windows installieren** fest:  

    - **Imagepaket:** Geben Sie das Betriebssystemimage-Paket an, das die erforderlichen Dateien zum Installieren des Betriebssystems enthält.  

    - **Imageindex:** Geben Sie den Index des Betriebssystems zum Installieren des Images an. Wenn das Betriebssystemimage mehrere Versionen enthält, wählen Sie die Version aus, die Sie installieren möchten.  

    - **Product Key:** Geben Sie bei Bedarf den Product Key für das zu installierende Windows-Betriebssystem an. Sie können codierte Volumenlizenzschlüssel und standardmäßige Product Keys angeben. Wenn Sie einen nicht codierten Product Key verwenden, muss jede Gruppe von fünf Zeichen durch einen Bindestrich (`-`) getrennt werden. Beispiel: `XXXXX-XXXXX-XXXXX-XXXXX-XXXXX`  

    - **Serverlizenzierungsmodus:** Sofern notwendig, geben Sie an, ob die Serverlizenz **pro Arbeitsplatz** oder **pro Server** gilt, bzw. dass keine Lizenz angegeben ist. Wenn die Serverlizenz **Pro Server**gilt, geben Sie auch die maximale Anzahl von Serververbindungen an.  

    - Geben Sie an, wie das Administratorkonto für das bereitgestellte Betriebssystem konfiguriert werden soll:  

        - **Lokales Administratorkennwort zufällig erstellen und das Konto auf allen unterstützten Plattformen deaktivieren:** Erstellen Sie ein zufälliges Kennwort für das lokale Administratorkonto. Deaktivieren Sie das Konto, nachdem Windows eingerichtet ist.

        - **Konto aktivieren und lokales Administratorkennwort angeben:** Verwenden Sie dasselbe Kennwort für das lokale Administratorkonto auf allen Computern, auf denen Sie dieses Betriebssystem bereitstellen.

1. Geben Sie auf der Seite **Netzwerk konfigurieren** die folgenden Einstellungen an:

    - **Einer Arbeitsgruppe beitreten:** Geben Sie an, ob der Zielcomputer einer Arbeitsgruppe hinzugefügt werden soll, wenn das Betriebssystem bereitgestellt wird.  

    - **Einer Domäne beitreten:** Geben Sie an, ob der Zielcomputer einer Domäne hinzugefügt werden soll, wenn das Betriebssystem bereitgestellt wird. Geben Sie unter **Domäne**den Namen der Domäne an.  

        > [!IMPORTANT]  
        > Sie können nach Domänen in der lokalen Gesamtstruktur suchen. Geben Sie den Domänennamen für eine Remotegesamtstruktur an.

        Sie können auch eine Organisationseinheit angeben. Dies ist eine optionale Einstellung, mit welcher der LDAP X.500-definierte Name der Organisationseinheit angegeben wird, in der das Computerkonto erstellt werden soll, sofern das Konto noch nicht vorhanden ist.  

    - **Konto:** Geben Sie den Benutzernamen und das Kennwort für das Konto an, das über die Berechtigungen verfügt, der angegebenen Domäne beizutreten. Beispiel: `domain\user` oder `%variable%`.  

        > [!IMPORTANT]  
        > Stellen Sie sicher, dass Sie hier die richtigen Domänenanmeldeinformationen eingeben, wenn Sie die Domäneneinstellungen oder die Arbeitsgruppeneinstellungen während der Bereitstellung migrieren möchten.  

1. Geben Sie das Configuration Manager-Clientpaket auf der Seite **Configuration Manager installieren** an. Dieses Paket enthält die Quelldateien zum Installieren des Configuration Manager-Clients. Legen Sie außerdem alle zusätzlichen Eigenschaften fest, die zum Installieren des Clients erforderlich sind.  

    Weitere Informationen finden Sie unter [Informationen zu Clientinstallationseigenschaften](../../core/clients/deploy/about-client-installation-properties.md).

1. Geben Sie auf der Seite **Updates einschließen** an, ob erforderliche Softwareupdates, alle Softwareupdates oder keine Softwareupdates installiert werden sollen. Wenn Sie angeben, dass Softwareupdates installiert werden sollen, werden von Configuration Manager nur Softwareupdates installiert, die für Sammlungen bestimmt sind, in denen der Zielcomputer Mitglied ist.  

1. Geben Sie auf der Seite **Anwendungen installieren** die Anwendungen an, die auf dem Zielcomputer installiert werden sollen. Wenn Sie mehrere Anwendungen angeben, können Sie auch angeben, dass die Tasksequenz fortgesetzt werden soll, wenn bei der Installation einer bestimmten Anwendung ein Fehler auftritt.  

    > [!NOTE]
    > Anschließend wird die Seite **Systemvorbereitung** im Assistenten angezeigt. Diese wird jedoch nicht mehr verwendet. Wählen Sie **Weiter** aus, um den Vorgang fortzusetzen.

1. Legen Sie die folgenden Einstellungen für das Betriebssystemimage auf der Seite **Imageeinstellungen** für das Betriebssystemimage fest:

    - **Erstellt von**: Geben Sie den Namen des Benutzers an, um auf den Ersteller des Betriebssystemimages zu verweisen.  

    - **Version:** Geben Sie Ihre Versionsnummer an, die dem Betriebssystemimage zugeordnet ist. Dieses Attribut muss nicht der Version des Betriebssystems entsprechen, da dieser Wert separat gespeichert wird.

    - **Beschreibung:** Geben Sie eine Beschreibung für das Betriebssystemimage an.  

1. Legen Sie die folgenden Einstellungen auf der Seite **Image erfassen** fest:

    - **Pfad:** Geben Sie einen freigegebenen Netzwerkordner an, in dem Configuration Manager die Ausgabeimagedatei (.wim) speichern soll. Diese Datei enthält das Betriebssystemimage, das auf den Einstellungen basiert, die Sie in diesem Assistenten angeben. Wenn Sie einen Ordner festlegen, der eine vorhandene WIM-Datei enthält, wird diese Datei überschrieben.  

    - **Konto:** Geben Sie das Windows-Konto an, das über Berechtigungen für die Netzwerkfreigabe verfügt, in der das Image gespeichert ist.  

1. Schließen Sie den Assistenten ab.  

Wählen Sie die Tasksequenz aus, und klicken Sie dann auf **Bearbeiten**, um weitere Schritte hinzuzufügen. Weitere Informationen zum Bearbeiten einer Tasksequenz finden Sie unter [Verwenden des Tasksequenz-Editors](../understand/task-sequence-editor.md).  

Verwenden Sie eine der folgenden Methoden, um die Tasksequenz auf einem Referenzcomputer bereitzustellen:  

- Wenn es sich beim Referenzcomputer bereits um einen Configuration Manager-Client handelt, stellen Sie die Tasksequenz zum Erstellen und Erfassen für die Sammlung bereit, die den Referenzcomputer enthält. Weitere Informationen finden Sie unter [Deploy a task sequence](deploy-a-task-sequence.md).

- Wenn es sich beim Referenzcomputer nicht um einen Configuration Manager-Client handelt oder Sie die Tasksequenz auf dem Referenzcomputer manuell ausführen möchten, verwenden Sie den **Assistenten zum Erstellen von Tasksequenzmedien**, um startbare Medien zu erstellen. Weitere Informationen finden Sie unter [Erstellen startbarer Medien](create-bootable-media.md).  

Nachdem Sie das Image erfasst haben, können Sie es auf anderen Computern bereitstellen. Weitere Informationen über die Bereitstellung des erfassten Betriebssystemimages finden Sie unter [Erstellen einer Tasksequenz zum Installieren eines Betriebssystems](create-a-task-sequence-to-install-an-operating-system.md).  

## <a name="capture-from-an-existing-reference-computer"></a><a name="BKMK_CaptureExistingRefComputer"></a> Erfassung von einem vorhandenen Referenzcomputer

Wenn Sie bereits über einen Referenzcomputer für die Erfassung verfügen, erstellen Sie eine Tasksequenz, die das Betriebssystem vom Referenzcomputer erfasst. Verwenden Sie den Tasksequenzschritt **Betriebssystemimage erfassen**, um mindestens ein Image von einem Referenzcomputer zu erfassen und in einer Imagedatei (WIM) auf der angegebenen Netzwerkfreigabe zu speichern. Starten Sie den Referenzcomputer in Windows PE mit einem Startimage. Die Tasksequenz erfasst alle Festplatten auf dem Referenzcomputer als separates Image innerhalb der WIM-Datei. Wenn der Referenzcomputer über mehrere Laufwerke verfügt, enthält die erstellte WIM-Datei für jedes Volume ein separates Image. Es werden nur als NTFS oder FAT32 formatierte Volumes erfasst. Volumes in anderen Formaten oder USB-Volumes werden übersprungen.  

Mit dem folgenden Verfahren können Sie ein Betriebssystemimage von einem vorhandenen Referenzcomputer erfassen.

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und wählen Sie anschließend den Knoten **Tasksequenzen** aus.  

1. Wählen Sie auf der Registerkarte **Start** des Menübands in der Gruppe **Erstellen** die Option **Tasksequenz erstellen** aus. Daraufhin wird der Tasksequenzerstellungs-Assistent gestartet.  

1. Wählen Sie auf der Seite **Neue Tasksequenz erstellen** die Option **Neue benutzerdefinierte Tasksequenz erstellen**aus.  

1. Legen Sie auf der Seite **Informationen zur Tasksequenz** einen Namen für die Tasksequenz fest. Fügen Sie optional eine Beschreibung für die Tasksequenz hinzu.  

1. Geben Sie ein Startabbild für die Tasksequenz an. Configuration Manager verwendet dieses Startimage zum Starten des Referenzcomputers mit Windows PE. Weitere Informationen finden Sie unter [Verwalten von Startimages](../get-started/manage-boot-images.md).  

1. Schließen Sie den Assistenten ab.  

1. Wählen Sie die neue Tasksequenz im Knoten **Tasksequenzen** aus. Wählen Sie anschließend auf der Registerkarte **Startseite** des Menübands in der Gruppe **Tasksequenz** die Option **Bearbeiten** aus. Durch diese Aktion wird der Tasksequenz-Editor geöffnet.  

1. Gehen Sie wie folgt vor, wenn der Configuration Manager-Client auf dem Referenzcomputer installiert ist:

    Rufen Sie das Menü **Hinzufügen** auf, wählen Sie **Images** und dann [ConfigMgr-Client für Erfassung vorbereiten](../understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture) aus. Mit diesem Schritt wird der Configuration Manager-Client auf dem Referenzcomputer generalisiert.

    > [!Note]  
    > Diese Tasksequenz unterstützt nicht das Deinstallieren des Configuration Manager-Clients.

1. Rufen Sie das Menü **Hinzufügen** auf, wählen Sie **Images** und dann [Windows für die Erfassung vorbereiten](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture) aus. Dieser Schritt führt Sysprep aus und startet dann den Computer über das für die Tasksequenz angegebene Windows PE-Startimage neu. Binden Sie den Referenzcomputer nicht in eine Domäne ein, damit diese Aktion erfolgreich abgeschlossen werden kann.

1. Rufen Sie das Menü **Hinzufügen** auf, wählen Sie **Images** und dann [Betriebssystemimage erfassen](../understand/task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) aus. Dieser Schritt wird nur von Windows PE ausgeführt, um die Festplatten auf dem Referenzcomputer zu erfassen. Konfigurieren Sie die folgenden Einstellungen:

    - **Name** und **Beschreibung:** Sie können den Namen des Tasksequenzschritts optional ändern und eine Beschreibung bereitstellen.  

    - **Ziel:** Geben Sie einen freigegebenen Netzwerkordner an, in dem die WIM-Ausgabedatei gespeichert ist. Diese Datei enthält das Betriebssystemimage, das auf den Einstellungen basiert, die Sie mit dem Assistenten angeben. Wenn Sie einen Ordner festlegen, der eine vorhandene WIM-Datei enthält, wird diese Datei überschrieben.  

    - **Beschreibung**, **Version** und **Erstellt von:** Stellen Sie optional Informationen zu dem Image bereit, das erfasst werden soll.  

    - **Konto für die Erfassung des Betriebssystemimages:** Geben Sie das Windows-Konto ein, das über Berechtigungen für den Zugriff auf die von Ihnen ausgewählte Netzwerkfreigabe verfügt. Wählen Sie **Festlegen** aus, um den Namen dieses Windows-Kontos anzugeben.  

Klicken Sie auf **OK**, um die Änderungen zu speichern und den Tasksequenz-Editor zu schließen.  

Verwenden Sie eine der folgenden Methoden, um die Tasksequenz auf einem Referenzcomputer bereitzustellen:  

- Wenn es sich beim Referenzcomputer bereits um einen Configuration Manager-Client handelt, stellen Sie die Tasksequenz zum Erfassen für die Sammlung bereit, die den Referenzcomputer enthält. Weitere Informationen finden Sie unter [Deploy a task sequence](deploy-a-task-sequence.md).

- Wenn es sich beim Referenzcomputer nicht um einen Configuration Manager-Client handelt oder Sie die Tasksequenz auf dem Referenzcomputer manuell ausführen möchten, verwenden Sie den **Assistenten zum Erstellen von Tasksequenzmedien**, um Erfassungsmedien zu erstellen. Weitere Informationen finden Sie unter [Erstellen von Erfassungsmedien](create-capture-media.md).  

Nachdem Sie das Image erfasst haben, können Sie es auf anderen Computern bereitstellen. Weitere Informationen über die Bereitstellung des erfassten Betriebssystemimages finden Sie unter [Erstellen einer Tasksequenz zum Installieren eines Betriebssystems](create-a-task-sequence-to-install-an-operating-system.md).

## <a name="example-task-sequence"></a><a name="BKMK_BuildandCaptureTSExample"></a> Tasksequenzbeispiel

Orientieren Sie sich an der folgenden Tabelle, während Sie eine Tasksequenz zum Erstellen und Erfassen eines Betriebssystemimages erstellen. Mithilfe dieser Tabelle können Sie die allgemeine Sequenz für Ihre Tasksequenzschritte festlegen und diese Schritte in logischen Gruppen organisieren. Die Tasksequenz, die Sie erstellen, kann von diesem Beispiel abweichen. Sie kann mehr oder weniger Schritte und Gruppen enthalten.

> [!NOTE]  
> Erstellen Sie diese Art von Tasksequenz stets mithilfe des Tasksequenzerstellungs-Assistenten.
>
> Der Assistent fügt Schritte mit etwas anderen Namen zur Tasksequenz hinzu, als wenn Sie die gleichen Schritte manuell hinzufügen würden.

### <a name="group-build-the-reference-machine"></a>Gruppe: Referenzcomputer erstellen

Diese Gruppe enthält die für das Erstellen eines Referenzcomputers erforderlichen Aktionen.

|Tasksequenzschritt|Beschreibung|  
|-------------------------------|---------------|  
|**Neustart mit Windows PE**|Starten Sie den Zielcomputer mit dem Startimage neu, das der Tasksequenz zugewiesen wurde. In diesem Schritt wird eine Meldung angezeigt, dass der Computer neu gestartet wird, um die Installation fortzusetzen.<br /><br />In diesem Schritt wird die schreibgeschützte Tasksequenzvariable `_SMSTSInWinPE` verwendet. Wenn der Variablen der Wert `false` zugeordnet ist, wird der Tasksequenzschritt fortgesetzt.|
|**Festplatte 0 partitionieren – BIOS**|In diesem Schritt wird die Festplatte des Zielcomputers im BIOS-Modus partitioniert und formatiert. Die standardmäßige Datenträgernummer ist `0`.<br /><br />In diesem Schritt werden mehrere schreibgeschützte Tasksequenzvariablen verwendet. Der Schritt wird beispielsweise nur ausgeführt, wenn der Configuration Manager-Clientcache nicht vorhanden ist, und wird nicht ausgeführt, wenn der Computer für UEFI konfiguriert ist.|
|**Festplatte 0 partitionieren – UEFI**|In diesem Schritt wird die Festplatte des Zielcomputers im UEFI-Modus partitioniert und formatiert. Die standardmäßige Datenträgernummer ist `0`.<br /><br />In diesem Schritt werden mehrere schreibgeschützte Tasksequenzvariablen verwendet. Der Schritt wird beispielsweise nur ausgeführt, wenn der Configuration Manager-Clientcache nicht vorhanden ist und wenn der Computer für UEFI konfiguriert ist.|
|**Betriebssystem anwenden**|Mit diesem Schritt wird das angegebene Betriebssystemimage auf dem Zielcomputer installiert. In diesem Schritt werden zunächst alle Dateien auf diesem Volume mit Ausnahme von Configuration Manager-spezifischen Steuerungsdateien gelöscht. Anschließend werden alle in der WIM-Datei enthaltenen Volumeimages auf das entsprechende sequenzielle Datenträgervolume auf dem Zielcomputer angewendet.|
|**Windows-Einstellungen anwenden**|Konfiguriert die Windows-Einstellungen für den Zielcomputer|
|**Netzwerkeinstellungen anwenden**|Geben Sie die Konfigurationsinformationen des Netzwerks oder der Arbeitsgruppe für den Zielcomputer an.|
|**Gerätetreiber anwenden**|In diesem Schritt werden Treiber im Rahmen der Betriebssystembereitstellung verglichen und installiert. Weitere Informationen finden Sie unter [Treiber automatisch anwenden](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers).<br /><br />In diesem Schritt wird die schreibgeschützte Tasksequenzvariable `_SMSTSMediaType` verwendet. Wenn der zugeordnete Wert nicht `FullMedia` entspricht, wird dieser Schritt nicht ausgeführt.|
|**Windows und Configuration Manager einrichten**|Installiert die Configuration Manager-Client-Software. Mit dem Configuration Manager wird die GUID des Configuration Manager-Clients installiert und registriert. Fügen Sie alle erforderlichen **Installationseigenschaften** ein.|
|**Updates installieren**|In diesem Schritt wird angegeben, wie Softwareupdates auf dem Zielcomputer installiert werden. Der Zielcomputer wird erst dann auf geeignete Softwareupdates überprüft, wenn dieser Schritt ausgeführt wird. An diesem Punkt ähnelt die Auswertung allen anderen von Configuration Manager verwalteten Clients. Weitere Informationen finden Sie unter [Softwareupdates installieren](../understand/install-software-updates.md).<br /><br />In diesem Schritt wird die schreibgeschützte Tasksequenzvariable `_SMSTSMediaType` verwendet. Wenn der zugeordnete Wert nicht `FullMedia` entspricht, wird dieser Schritt nicht ausgeführt.|
|**Anwendungen installieren**|In diesem Schritt werden die Anwendungen angegeben, die auf dem Referenzcomputer installiert werden sollen.|

### <a name="group-capture-the-reference-machine"></a>Gruppe: Referenzcomputer erfassen

Diese Gruppe enthält die für das Vorbereiten und Erfassen eines Referenzcomputers erforderlichen Schritte.

|Tasksequenzschritt|Beschreibung|  
|-------------------------------|---------------|  
|**Configuration Manager-Client vorbereiten**|In diesem Schritt wird der Configuration Manager-Client auf dem Referenzcomputer generalisiert.|
|**Betriebssystem vorbereiten**|In diesem Schritt wird Sysprep zum Generalisieren von Windows ausgeführt. Anschließend wird der Computer mit dem Windows PE-Startimage neugestartet, das für die Tasksequenz festgelegt wurde.|
|**Referenzcomputer erfassen**|In diesem Schritt wird das Image in der angegebenen Netzwerkfreigabe und einer WIM-Datei erfasst.|

> [!IMPORTANT]
> Erfassen Sie kein weiteres Betriebssystemimage vom Referenzcomputer, nachdem Sie ein Image von einem Referenzcomputer erfasst haben. Während der Erstkonfiguration werden Registrierungseinträge erstellt. Erstellen Sie bei jedem Erfassen des Betriebssystemimages einen neuen Referenzcomputer. Wenn Sie denselben Referenzcomputer zum Erstellen weiterer Betriebssystemimages verwenden möchten, deinstallieren Sie den Configuration Manager-Client zunächst, und installieren Sie ihn dann neu.

## <a name="next-steps"></a>Nächste Schritte

[Methoden zum Bereitstellen von Unternehmensbetriebssystemen](methods-to-deploy-enterprise-operating-systems.md)
