---
title: Tasksequenzschritte
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über die Schritte, die Sie einer Configuration Manager-Tasksequenz hinzufügen können.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: reference
ms.assetid: 7c888a6f-8e37-4be5-8edb-832b218f266d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 49792ea588f01cc57a1dbce9cc137b94a0e4d291
ms.sourcegitcommit: cba06c182646cb6dceef304b35230bf728d5133e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/15/2020
ms.locfileid: "90574795"
---
# <a name="task-sequence-steps"></a>Tasksequenzschritte

*Gilt für: Configuration Manager (Current Branch)*

Die folgenden Tasksequenzschritte können einer Configuration Manager-Tasksequenz hinzugefügt werden. Weitere Informationen finden Sie unter [Verwenden des Tasksequenz-Editors](task-sequence-editor.md).  

## <a name="common-settings"></a>Allgemeine Einstellungen

Folgende Einstellungen gelten für alle Tasksequenzschritte:

### <a name="properties-for-all-steps"></a>Eigenschaften für alle Schritte

- **Name:** Der Tasksequenz-Editor erfordert, dass Sie einen kurzen Namen zur Beschreibung dieses Schritts angeben. Wenn Sie einen neuen Schritt hinzufügen, legt der Tasksequenz-Editor den Namen standardmäßig auf den Typ fest. Der **Name** darf nicht länger als 50 Zeichen sein.  

- **Beschreibung:** Geben Sie optional ausführlichere Informationen zu diesem Schritt an. Die **Beschreibung** darf nicht länger als 256 Zeichen sein.  

Im weiteren Verlauf dieses Artikels werden andere Einstellungen der Registerkarte **Eigenschaften** für jeden Tasksequenzschritt beschrieben.

### <a name="options-for-all-steps"></a>Optionen für alle Schritte

- **Diesen Schritt deaktivieren**: Die Tasksequenz überspringt diesen Schritt, wenn sie auf einem Computer ausgeführt wird. Das Symbol für diesen Schritt wird im Tasksequenz-Editor abgeblendet.  

- **Bei Fehler fortsetzen**: Wenn beim Ausführen des Schritts ein Fehler auftritt, wird die Tasksequenz fortgesetzt. Weitere Informationen finden Sie unter [Planungsüberlegungen für das Automatisieren von Tasks](../plan-design/planning-considerations-for-automating-tasks.md#BKMK_TSGroups).  

- **Bedingung hinzufügen**: Die Tasksequenz wertet diese bedingten Anweisungen aus, um zu bestimmen, ob der Schritt ausgeführt wird. Ein Beispiel für die Verwendung einer Tasksequenzvariablen als Bedingung finden Sie unter [Verwenden von Tasksequenzvariablen](using-task-sequence-variables.md#bkmk_access-condition). Weitere Informationen zu Bedingungen finden Sie unter [Tasksequenz-Editor – Bedingungen](task-sequence-editor.md#bkmk_conditions).

In den folgenden Abschnitten werden andere mögliche Einstellungen für bestimmte Tasksequenzschritte auf der Registerkarte **Optionen** beschrieben.



## <a name="apply-data-image"></a><a name="BKMK_ApplyDataImage"></a> Anwenden von Datenimages

Mithilfe dieses Schritts können Sie das Datenimage auf die angegebene Zielpartition kopieren.  

Dieser Schritt wird nur in Windows PE ausgeführt. Er kann nicht in der Vollversion des Betriebssystems ausgeführt werden.

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Images** und dann **Datenimage anwenden** aus.

### <a name="variables-for-apply-data-image"></a>Variablen für „Datenimage anwenden“

Verwenden Sie die folgenden Tasksequenzvariablen in diesem Schritt:  

- [OSDDataImageIndex](task-sequence-variables.md#OSDDataImageIndex)  
- [OSDWipeDestinationPartition](task-sequence-variables.md#OSDWipeDestinationPartition)  

### <a name="cmdlets-for-apply-data-image"></a>Cmdlets für „Datenimage anwenden“

Verwalten Sie diesen Schritt mit den folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyDataImage](/powershell/module/configurationmanager/Get-CMTSStepApplyDataImage)
- [New-CMTSStepApplyDataImage](/powershell/module/configurationmanager/New-CMTSStepApplyDataImage)
- [Remove-CMTSStepApplyDataImage](/powershell/module/configurationmanager/Remove-CMTSStepApplyDataImage)
- [Set-CMTSStepApplyDataImage](/powershell/module/configurationmanager/Set-CMTSStepApplyDataImage)

### <a name="properties-for-apply-data-image"></a>Eigenschaften für „Datenimage anwenden“

Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

#### <a name="image-package"></a>Abbildpaket

Wird Sie **Durchsuchen** aus, um das **Imagepaket** festzulegen, das von dieser Tasksequenz verwendet wird. Wählen Sie das zu installierende Paket im Dialogfeld **Paket auswählen** aus. Unten im Dialogfeld werden die zugeordneten Eigenschaftsinformationen für jedes vorhandene Imagepaket angezeigt. Wählen Sie mithilfe der Dropdownliste das zu installierende **Abbild** aus dem ausgewählten **Abbildpaket**aus.  

> [!NOTE]  
> In dieser Tasksequenzaktion wird das Image als Datendatei behandelt. Diese Aktion führt kein Setup aus, um das Image als Betriebssystem zu starten.  

#### <a name="destination"></a>Ziel

Konfigurieren Sie eine der folgenden Optionen:

- **Nächste verfügbare Partition**: Verwenden Sie die nächste verfügbare Partition, die in dieser Tasksequenz nicht bereits für den Schritt **Betriebssystem anwenden** oder **Datenimage anwenden** verwendet wurde.  

- **Bestimmter Datenträger und Partition:** Wählen Sie die Nummer des **Datenträgers** (beginnend mit 0) und die Nummer der **Partition** (beginnend mit 1) aus.  

- **Bestimmter Buchstabe für logisches Laufwerk:** Geben Sie den **Laufwerkbuchstaben** an, den Windows PE der Partition zuweist. Dieser Laufwerkbuchstabe kann vom Laufwerkbuchstaben abweichen, den das neu bereitgestellte Betriebssystem zugewiesen hat.  

- **In Variable gespeicherter Buchstabe für logisches Laufwerk**: Geben Sie die Tasksequenzvariable an, die den Laufwerkbuchstaben enthält, den Windows PE der Partition zugewiesen hat. Diese Variable wird in der Regel im Bereich „Erweitert“ des Dialogfelds **Partitionseigenschaften** für den Tasksequenzschritt **Datenträger formatieren und partitionieren** festgelegt.  

#### <a name="delete-all-content-on-the-partition-before-applying-the-image"></a>Vor dem Anwenden des Abbilds den gesamten Inhalt der Partition löschen  

Legt fest, dass die Tasksequenz alle Dateien auf der Zielpartition löscht, bevor das Image installiert wird. Indem der Inhalt dieser Partition nicht gelöscht wird, können mit dieser Aktion einer zuvor eingerichteten Partition Inhalte zugewiesen werden.  



## <a name="apply-driver-package"></a><a name="BKMK_ApplyDriverPackage"></a> Treiberpaket anwenden  

Verwenden Sie diesen Schritt, um alle Treiber im Treiberpaket herunterzuladen und auf dem Windows-Betriebssystem zu installieren.

Mit dem Tasksequenzschritt **Treiberpaket anwenden** können Sie alle Gerätetreiber eines Treiberpakets zur Verwendung in Windows bereitstellen. Fügen Sie diesen Schritt zwischen den Schritten **Betriebssystem anwenden** und **Windows und ConfigMgr einrichten** hinzu, um die Treiber in diesem Paket für Windows zur Verfügung zu stellen. Der Tasksequenzschritt **Treiberpaket anwenden** ist auch für die Bereitstellung mithilfe eigenständiger Medien nützlich.  

Fassen Sie ähnliche Gerätetreiber in einem Treiberpaket zusammen, und verteilen Sie diese auf die entsprechenden Verteilungspunkte. Packen Sie beispielsweise alle Treiber eines Herstellers in ein Treiberpaket. Verteilen Sie das Paket anschließend an Verteilungspunkte, auf die die entsprechenden Computer zugreifen können.

Der Schritt **Treiberpaket anwenden** ist für eigenständige Medien nützlich. Dieser Schritt ist ebenfalls nützlich, um einen bestimmten Treibersatz zu installieren. Zu diesen Treibern gehören Geräte, die nicht durch Plug & Play von Windows erkannt werden, z.B. Netzwerkdrucker.  

Dieser Tasksequenzschritt wird nur in Windows PE ausgeführt. Er kann nicht in der Vollversion des Betriebssystems ausgeführt werden.

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Treiber** und dann **Treiberpaket anwenden** aus.

> [!TIP]
> Eine Übersicht über die Treiber in Configuration Manager erhalten Sie unter [Verwenden von Tasksequenzen zum Installieren von Treibern](../get-started/manage-drivers.md#BKMK_TSDrivers).
>
> Verwenden Sie ein vorgeschaltetes Zwischenspeichern für Inhalte, um ein geeignetes Treiberpaket herunterzuladen, bevor ein Benutzer die Tasksequenz installiert. Weitere Informationen finden Sie unter [Konfigurieren des zwischengespeicherten Inhalts](../deploy-use/configure-precache-content.md).

### <a name="variables-for-apply-driver-package"></a>Variablen für „Treiberpaket anwenden“

Verwenden Sie die folgenden Tasksequenzvariablen in diesem Schritt:  

- [OSDApplyDriverBootCriticalContentUniqueID](task-sequence-variables.md#OSDApplyDriverBootCriticalContentUniqueID)  
- [OSDApplyDriverBootCriticalHardwareComponent](task-sequence-variables.md#OSDApplyDriverBootCriticalHardwareComponent)  
- [OSDApplyDriverBootCriticalID](task-sequence-variables.md#OSDApplyDriverBootCriticalID)  
- [OSDApplyDriverBootCriticalINFFile](task-sequence-variables.md#OSDApplyDriverBootCriticalINFFile)  
- [OSDInstallDriversAdditionalOptions](task-sequence-variables.md#OSDInstallDriversAdditionalOptions)<!--516679/2840016-->

### <a name="cmdlets-for-apply-driver-package"></a>Cmdlets für „Treiberpaket anwenden“

Verwalten Sie diesen Schritt mit den folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyDriverPackage](/powershell/module/configurationmanager/Get-CMTSStepApplyDriverPackage)
- [New-CMTSStepApplyDriverPackage](/powershell/module/configurationmanager/New-CMTSStepApplyDriverPackage)
- [Remove-CMTSStepApplyDriverPackage](/powershell/module/configurationmanager/Remove-CMTSStepApplyDriverPackage)
- [Set-CMTSStepApplyDriverPackage](/powershell/module/configurationmanager/Set-CMTSStepApplyDriverPackage)

### <a name="properties-for-apply-driver-package"></a>Eigenschaften für „Treiberpaket anwenden“

Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

#### <a name="driver-package"></a>Treiberpaket

Geben Sie das Treiberpaket an, das die benötigten Gerätetreiber enthält. Wählen Sie **Durchsuchen** aus, um das Dialogfeld **Paket auswählen** zu starten. Wählen Sie ein vorhandenes Treiberpaket aus, das Sie anwenden möchten. Unten im Dialogfeld werden die zugehörigen Paketeigenschaften angezeigt.  

#### <a name="install-driver-package-via-running-dism-with-recurse-option"></a>Treiberpaket über ausgeführten DISM mit rekursiver Option installieren

Wählen Sie diese Option aus, um den `/recurse`-Parameter in der DISM-Befehlszeile hinzuzufügen, wenn Windows das Treiberpaket anwendet.

Wenn Sie diese Option aktivieren, können Sie auch weitere DISM-Befehlszeilenparameter angeben. Verwenden Sie die Tasksequenzvariable [OSDInstallDriversAdditionalOptions](task-sequence-variables.md#OSDInstallDriversAdditionalOptions), um weitere Optionen einzuschließen. Weitere Informationen finden Sie unter [Windows 10-DISM-Befehlszeilenoptionen](/windows-hardware/manufacture/desktop/deployment-image-servicing-and-management--dism--command-line-options).<!-- SCCMDocs#2125 -->

#### <a name="select-the-mass-storage-driver-within-the-package-that-needs-to-be-installed-before-setup-on-pre-windows-vista-operating-systems"></a>Wählen Sie den Massenspeichertreiber im Paket aus, der installiert werden muss, bevor das Setup auf Betriebssystemen vor Windows Vista ausgeführt werden kann.

Geben Sie alle Massenspeichertreiber an, die für die Installation eines klassischen Betriebssystems erforderlich sind.  

##### <a name="driver"></a>Treiber

Wählen Sie die Datei für die Installation der Massenspeichertreiber aus, bevor Sie ein klassisches Betriebssystem einrichten. Die Dropdownliste wird mit den Treibern aus dem angegebenen Paket aufgefüllt.  

##### <a name="model"></a>Modell

Geben Sie das für den Systemstart erforderliche Gerät an, das für Bereitstellungen von Betriebssystemen vor Windows Vista erforderlich ist.  

#### <a name="do-unattended-installation-of-unsigned-drivers-on-version-of-windows-where-this-is-allowed"></a>Unbeaufsichtigte Installation von nicht signierten Treibern bei Windows-Versionen ausführen, wenn zulässig

Durch diese Option können Sie unter Windows Treiber ohne digitale Signatur installieren.  



## <a name="apply-network-settings"></a><a name="BKMK_ApplyNetworkSettings"></a> Anwenden von Netzwerkeinstellungen  

Mithilfe dieses Schritts können Sie die Konfigurationsinformationen für das Netzwerk oder die Arbeitsgruppe des Zielcomputers angeben. Die Tasksequenz speichert diese Werte in der entsprechenden Antwortdatei. Windows Setup verwendet diese Antwortdatei während der Aktion **Windows und ConfigMgr einrichten**.  

Dieser Tasksequenzschritt wird nur in Windows PE ausgeführt. Er kann nicht in der Vollversion des Betriebssystems ausgeführt werden.

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Einstellungen** und dann **Netzwerkeinstellungen anwenden** aus.

> [!NOTE]
> Wenn Sie mehrere Instanzen dieses Schritts in einer Tasksequenz einschließen, gelten die Bedingungen nicht. Die Einstellungen der letzten Instanz dieses Schritts in der Tasksequenz werden auf das Gerät angewendet. Als Umgehung dieses Verhaltens können Sie jeden Schritt in einer eigenen Gruppe mit Bedingungen für die jeweilige Gruppe einschließen.

### <a name="variables-for-apply-network-settings"></a>Variablen für „Netzwerkeinstellungen anwenden“

Verwenden Sie die folgenden Tasksequenzvariablen in diesem Schritt:  

- [OSDAdapter](task-sequence-variables.md#OSDAdapter)  
- [OSDAdapterCount](task-sequence-variables.md#OSDAdapterCount)  
- [OSDDNSDomain](task-sequence-variables.md#OSDDNSDomain)  
- [OSDDNSSuffixSearchOrder](task-sequence-variables.md#OSDDNSSuffixSearchOrder)  
- [OSDDomainName](task-sequence-variables.md#OSDDomainName)  
- [OSDDomainOUName](task-sequence-variables.md#OSDDomainOUName)  
- [OSDEnableTCPIPFiltering](task-sequence-variables.md#OSDEnableTCPIPFiltering)  
- [OSDJoinAccount](task-sequence-variables.md#OSDJoinAccount)  
- [OSDJoinPassword](task-sequence-variables.md#OSDJoinPassword)  
- [OSDWorkgroupName](task-sequence-variables.md#OSDWorkgroupName)  

### <a name="cmdlets-for-apply-network-settings"></a>Cmdlets für „Netzwerkeinstellungen anwenden“

Verwalten Sie diesen Schritt mit den folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyNetworkSetting](/powershell/module/configurationmanager/Get-CMTSStepApplyNetworkSetting)
- [New-CMTSStepApplyNetworkSetting](/powershell/module/configurationmanager/New-CMTSStepApplyNetworkSetting)
- [Remove-CMTSStepApplyNetworkSetting](/powershell/module/configurationmanager/Remove-CMTSStepApplyNetworkSetting)
- [Set-CMTSStepApplyNetworkSetting](/powershell/module/configurationmanager/Set-CMTSStepApplyNetworkSetting)

### <a name="properties-for-apply-network-settings"></a>Eigenschaften für „Netzwerkeinstellungen anwenden“

Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

#### <a name="join-a-workgroup"></a>Einer Arbeitsgruppe beitreten

Wählen Sie diese Option aus, um den Zielcomputer einer angegebenen Arbeitsgruppe hinzuzufügen. Geben Sie den Namen der Arbeitsgruppen in die Zeile **Arbeitsgruppe** ein. Der Wert, den der Tasksequenzschritt **Netzwerkeinstellungen erfassen** erfasst, kann diesen Wert überschreiben.

#### <a name="join-a-domain"></a>Einer Domäne beitreten

Wählen Sie diese Option aus, um den Zielcomputer einer angegebenen Domäne hinzuzufügen. Geben Sie die Domäne an, oder klicken Sie auf Durchsuchen, um die Domäne auszuwählen, z. B. `fabricam.com`. Geben Sie einen LDAP-Pfad (Lightweight Directory Access Protocol) für eine Organisationseinheit an, oder suchen Sie nach einem LDAP-Pfad. Beispiel: `LDAP//OU=computers, DC=Fabricam.com, C=com`.  

> [!NOTE]
> Wenn ein in Azure Active Directory (Azure AD) eingebundener Client eine Tasksequenz für die Bereitstellung eines Betriebssystems ausführt, wird der Client im neuen Betriebssystem nicht automatisch in Azure AD eingebunden. Auch wenn der Client nicht in Azure AD eingebunden ist, wird er dennoch verwaltet.

#### <a name="account"></a>Konto

Wählen Sie **Festlegen** aus, um ein Konto anzugeben, das die für den Beitritt zur Domäne erforderlichen Berechtigungen aufweist. Geben Sie im Dialogfeld **Windows-Benutzerkonto** den Benutzernamen in folgendem Format ein: `Domain\User`. Weitere Informationen finden Sie unter [Domänenbeitrittskonto](../../core/plan-design/hierarchy/accounts.md#task-sequence-domain-join-account).

#### <a name="adapter-settings"></a>Netzwerkkarteneinstellungen

Geben Sie die Netzwerkkonfigurationen für alle Netzwerkadapter auf dem Computer an. Wählen Sie **Neu** aus, um das Dialogfeld **Netzwerkeinstellungen** zu öffnen, und geben Sie dann die Netzwerkeinstellungen an.

- Wenn Sie ebenfalls den Schritt **Netzwerkeinstellungen erfassen** verwenden, wendet die Tasksequenz die zuvor erfassten Einstellungen auf den Netzwerkadapter an.
- Wenn die Tasksequenz zuvor keine Netzwerkeinstellungen erfasst hat, werden die in diesem Schritt angegebenen Einstellungen angewendet.
- Die Tasksequenz wendet diese Einstellungen in der Reihenfolge der Windows-Gerätenummern auf Netzwerkadapter an.  
- Die Tasksequenz wendet die in diesem Schritt angegebenen Einstellungen nicht sofort auf den Computer an.



## <a name="apply-operating-system-image"></a><a name="BKMK_ApplyOperatingSystemImage"></a> Betriebssystemimage anwenden  

Verwenden Sie diesen Schritt, um ein Betriebssystem auf dem Zielcomputer zu installieren.

Nachdem die Aktion **Betriebssystem anwenden** ausgeführt wurde, wird die Variable **OSDTargetSystemDrive** auf den Laufwerkbuchstaben der Partition festgelegt, in der sich die Betriebssystemdateien befinden.  

Dieser Tasksequenzschritt wird nur in Windows PE ausgeführt. Er kann nicht in der Vollversion des Betriebssystems ausgeführt werden.

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Images** und dann **Betriebssystemimage anwenden** aus.

> [!TIP]
> Ab Windows 10 (Version 1709) enthalten Medien mehrere Editionen. Wenn Sie eine Tasksequenz konfigurieren, um ein Betriebssystemupgradepaket oder ein Betriebssystemimage zu verwenden, achten Sie darauf, eine [unterstützte Edition](../../core/plan-design/configs/support-for-windows-10.md#windows-10-as-a-client) auszuwählen.  
>
> Verwenden Sie ein vorgeschaltetes Zwischenspeichern für Inhalte, um ein geeignetes Betriebssystemupgradepaket herunterzuladen, bevor ein Benutzer die Tasksequenz installiert. Weitere Informationen finden Sie unter [Konfigurieren des zwischengespeicherten Inhalts](../deploy-use/configure-precache-content.md).
>
> Der Schritt **Windows und ConfigMgr einrichten** startet die Installation von Windows.

### <a name="variables-for-apply-os-image"></a>Variablen für „Betriebssystemimage anwenden“

Verwenden Sie die folgenden Tasksequenzvariablen in diesem Schritt:  

- [OSDConfigFileName](task-sequence-variables.md#OSDConfigFileName)  
- [OSDImageIndex](task-sequence-variables.md#OSDImageIndex)  
- [OSDTargetSystemDrive](task-sequence-variables.md#OSDTargetSystemDrive)  

### <a name="cmdlets-for-apply-os-image"></a>Cmdlets für „Betriebssystemimage anwenden“

Verwalten Sie diesen Schritt mit den folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyOperatingSystem](/powershell/module/configurationmanager/Get-CMTSStepApplyOperatingSystem)
- [New-CMTSStepApplyOperatingSystem](/powershell/module/configurationmanager/New-CMTSStepApplyOperatingSystem)
- [Remove-CMTSStepApplyOperatingSystem](/powershell/module/configurationmanager/Remove-CMTSStepApplyOperatingSystem)
- [Set-CMTSStepApplyOperatingSystem](/powershell/module/configurationmanager/Set-CMTSStepApplyOperatingSystem)

### <a name="behaviors-for-apply-os-image"></a>Verhalten für „Betriebssystemimage anwenden“

Die Aktionen dieses Schritts hängen davon ab, ob ein Betriebssystemimage oder ein Betriebssystemupgradepaket verwendet wird.  

#### <a name="os-image-actions"></a>Aktionen für Betriebssystemimages

Wenn ein Betriebssystemimage verwendet wird, werden mit dem Schritt **Betriebssystemimage anwenden** folgende Aktionen ausgeführt:  

1. Alle Inhalte auf dem Zielvolume werden gelöscht, mit der Ausnahme von Dateien in dem durch die Variable **\_SMSTSUserStatePath** angegebenen Ordner.  

2. Alle Inhalte der angegebenen WIM-Datei werden in die angegebene Zielpartition extrahiert.  

3. Die Antwortdatei wird vorbereitet:  

    1. Eine neue Standardantwortdatei für Windows Setup („sysprep.inf“ oder „unattend.xml“) wird für das bereitgestellte Betriebssystem erstellt.  

    2. Alle Werte aus der vom Benutzer bereitgestellten Antwortdatei werden zusammengeführt.  

4. Windows-Startladeprogramme werden in die aktive Partition kopiert.  

5. Die Datei „boot.ini“ bzw. die Startkonfigurationsdaten (BCD) werden so festgelegt, dass auf das neu installierte Betriebssystem verwiesen wird.  

#### <a name="os-upgrade-package-actions"></a>Aktionen für Betriebssystemupgrade-Pakete

Wenn ein Betriebssystemupgradepaket verwendet wird, werden mit dem Schritt **Betriebssystemimage anwenden** folgende Aktionen ausgeführt:  

1. Alle Inhalte auf dem Zielvolume werden gelöscht, mit der Ausnahme von Dateien in dem durch die Variable **\_SMSTSUserStatePath** angegebenen Ordner.  

2. Die Antwortdatei wird vorbereitet:  

    1. Eine neue Antwortdatei mit von Configuration Manager erstellten Standardwerten wird erstellt.  

    2. Alle Werte aus der vom Benutzer bereitgestellten Antwortdatei werden zusammengeführt.  

### <a name="properties-for-apply-os-image"></a>Eigenschaften für „Betriebssystemimage anwenden“

Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

#### <a name="apply-operating-system-from-a-captured-image"></a>Betriebssystem von einem erfassten Abbild übernehmen

Ein erfasstes Betriebssystemimage wird installiert. Wählen Sie **Durchsuchen** aus, um das Dialogfeld **Paket auswählen** zu öffnen. Wählen Sie dann das vorhandene Imagepaket aus, das Sie installieren möchten. Wenn mehrere Images mit dem angegebenen **Imagepaket**verknüpft sind, wählen Sie aus der Dropdownliste das entsprechende Image für diese Bereitstellung aus. Sie können grundlegende Informationen zu jedem vorhandenen Image anzeigen, indem Sie es auswählen.  

#### <a name="apply-operating-system-image-from-an-original-installation-source"></a>Betriebssystem von einer ursprünglichen Installationsquelle übernehmen

Installiert ein Betriebssystem mit einem Betriebssystemupgrade-Paket, das auch eine ursprüngliche Installationsquelle ist. Wählen Sie **Durchsuchen** aus, um das Dialogfeld **Aktualisierungspaket für Betriebssystem auswählen** zu öffnen. Wählen Sie dann das vorhandene Betriebssystemupgradepaket aus, das Sie verwenden möchten. Sie können grundlegende Informationen zu jeder vorhandenen Imagequelle anzeigen, indem Sie sie auswählen. Der Ergebnisbereich unten im Dialogfeld zeigt die zugehörigen Eigenschaften der Imagequelle an. Falls dem angegebenen Paket mehrere Editionen zugeordnet sind, wählen Sie aus der Dropdownliste die gewünschte **Edition** aus.  

> [!NOTE]  
> **Betriebssystemupgradepakete** sind in erster Linie für die Verwendung bei direkten Upgrades und nicht für Neuinstallationen von Windows gedacht. Wenn Sie Neuinstallationen von Windows bereitstellen, verwenden Sie die Option **Betriebssystem aus erfasstem Image anwenden** und **install.wim** aus den Quelldateien der Installation.
>
> Das Bereitstellen von Windows-Neuinstallationen über **Betriebssystemupgradepakete** wird zwar weiterhin unterstützt, hängt aber davon ab, ob die Treiber mit dieser Methode kompatibel sind. Bei Neuinstallationen von Windows aus einem Betriebssystemupgradepaket werden die Treiber installiert und nicht einfach eingefügt, während noch die Windows-Vorinstallationsumgebung (Windows PE) ausgeführt wird. Einige Treiber sind jedoch nicht kompatibel mit der Installation in Windows PE.
>
> Wenn Treiber nicht mit der Installation in Windows PE kompatibel sind, erstellen Sie aus den ursprünglichen Installationsquelldateien ein **Betriebssystemimage** mit **install.wim**. Führen Sie die Bereitstellung anschließend stattdessen über die Option **Betriebssystem aus erfasstem Image anwenden** durch.

#### <a name="use-an-unattended-or-sysprep-answer-file-for-a-custom-installation"></a>Datei für unbeaufsichtigte Installation oder Antwortdatei für Systemvorbereitung bei benutzerdefinierter Installation verwenden

Stellen Sie mit dieser Option je nach Betriebssystemversion und Installationsmethode eine Windows Setup-Antwortdatei (**unattend.xml**, **unattend.txt** oder **sysprep.inf**) bereit. Die von Ihnen angegebene Datei kann alle Standardkonfigurationsoptionen enthalten, die von Windows-Antwortdateien unterstützt werden. Sie können damit beispielsweise die Standardstartseite im Internet Explorer angeben. Geben Sie das Paket mit der Antwortdatei sowie den entsprechenden Pfad zu der Datei im Paket an.  

> [!NOTE]  
> Die bereitgestellte Windows Setup-Antwortdatei kann eingebettete Tasksequenzvariablen im Format `%varname%` enthalten, wobei *varname* der Name der Variable ist. Der Schritt **Windows und ConfigMgr einrichten** ersetzt die Variablenzeichenfolge durch den tatsächlichen Variablenwert. Diese eingebetteten Tasksequenzvariablen können nicht in den rein numerischen Feldern in einer Antwortdatei „unattend.xml“ verwendet werden.  

Wenn Sie keine Windows Setup-Antwortdatei bereitstellen, generiert diese Tasksequenz automatisch eine Antwortdatei.  

#### <a name="destination"></a>Ziel

Konfigurieren Sie eine der folgenden Optionen:  

- **Nächste verfügbare Partition**: Verwenden Sie die nächste verfügbare Partition, die in dieser Tasksequenz nicht bereits für den Schritt **Betriebssystem anwenden** oder **Datenimage anwenden** verwendet wurde.  

- **Bestimmter Datenträger und Partition:** Wählen Sie die Nummer des **Datenträgers** (beginnend mit 0) und die Nummer der **Partition** (beginnend mit 1) aus.  

- **Bestimmter Buchstabe für logisches Laufwerk:** Geben Sie den **Laufwerkbuchstaben** ein, der der Partition von Windows PE zugewiesen wurde. Dieser Laufwerkbuchstabe kann vom Laufwerkbuchstaben abweichen, den das neu bereitgestellte Betriebssystem zugewiesen hat.  

- **In Variable gespeicherter Buchstabe für logisches Laufwerk**: Geben Sie die Tasksequenzvariable an, die den Laufwerksbuchstaben enthält, der von Windows PE der Partition zugewiesen wurde. Diese Variable wird in der Regel im Bereich „Erweitert“ des Dialogfelds **Partitionseigenschaften** für den Tasksequenzschritt **Datenträger formatieren und partitionieren** festgelegt.  

### <a name="options-for-apply-os-image"></a>Optionen für „Betriebssystemimage anwenden“

Konfigurieren Sie neben den Standardoptionen auch folgende zusätzliche Einstellungen auf der Registerkarte **Optionen** dieses Tasksequenzschritts:  

#### <a name="access-content-directly-from-the-distribution-point"></a>Auf Inhalt direkt vom Verteilungspunkt aus zugreifen

Konfigurieren Sie die Tasksequenz so, dass sie direkt vom Verteilungspunkt aus auf das Betriebssystemimage zugreift. Verwenden Sie diese Option, wenn Sie beispielsweise Betriebssysteme für eingebettete Geräte mit begrenzter Speicherkapazität bereitstellen. Wenn Sie diese Option aktivieren, müssen Sie auch die Einstellungen für die Paketfreigabe auf der Registerkarte **Datenzugriff** der Betriebssystem-Paketeigenschaften konfigurieren.  

> [!NOTE]  
> Diese Einstellung setzt die Bereitstellungsoption außer Kraft, die Sie auf der Seite **Verteilungspunkte** des **Assistenten zum Bereitstellen von Software** konfigurieren. Diese Außerkraftsetzung gilt nur für das von diesem Schritt angegebene Betriebssystemimage, nicht für alle Inhalte der Tasksequenz.  

> [!IMPORTANT]  
> Aus Sicherheitsgründen wird dringend davon abgeraten, diese Option auszuwählen. Diese Option ist in erster Linie für Geräte mit begrenzter Speicherkapazität vorgesehen. Sie ist nicht zur Beschleunigung der Tasksequenz gedacht. Wenn diese Option ausgewählt wird, wird der Hashwert des Betriebssystempakets nicht überprüft. Somit kann die Paketintegrität nicht gewährleistet werden, da Benutzer mit Administratorrechten Paketinhalte ändern oder manipulieren können.



## <a name="apply-windows-settings"></a><a name="BKMK_ApplyWindowsSettings"></a> Windows-Einstellungen anwenden

Mithilfe dieses Schritts können Sie die Windows-Einstellungen für den Zielcomputer konfigurieren. Die Tasksequenz speichert diese Werte in der entsprechenden Antwortdatei. Windows Setup verwendet diese Antwortdatei für den Schritt **Windows und ConfigMgr einrichten**.  

Dieser Tasksequenzschritt wird nur in Windows PE ausgeführt. Er kann nicht in der Vollversion des Betriebssystems ausgeführt werden.  

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Einstellungen** und dann **Windows-Einstellungen anwenden** aus.

### <a name="variables-for-apply-windows-settings"></a>Variablen für „Windows-Einstellungen anwenden“

Verwenden Sie die folgenden Tasksequenzvariablen in diesem Schritt:  

- [OSDComputerName](task-sequence-variables.md#OSDComputerName-input)  
- [OSDLocalAdminPassword](task-sequence-variables.md#OSDLocalAdminPassword)  
- [OSDProductKey](task-sequence-variables.md#OSDProductKey)  
- [OSDRandomAdminPassword](task-sequence-variables.md#OSDRandomAdminPassword)  
- [OSDRegisteredOrgName](task-sequence-variables.md#OSDRegisteredOrgName-input)  
- [OSDRegisteredUserName](task-sequence-variables.md#OSDRegisteredUserName)  
- [OSDServerLicenseConnectionLimit](task-sequence-variables.md#OSDServerLicenseConnectionLimit)  
- [OSDServerLicenseMode](task-sequence-variables.md#OSDServerLicenseMode)  
- [OSDTimeZone](task-sequence-variables.md#OSDTimeZone-input)  
- [OSDWindowsSettingsInputLocale](task-sequence-variables.md#OSDWindowsSettingsInputLocale)
- [OSDWindowsSettingsSystemLocale](task-sequence-variables.md#OSDWindowsSettingsSystemLocale)
- [OSDWindowsSettingsUILanguage](task-sequence-variables.md#OSDWindowsSettingsUILanguage)
- [OSDWindowsSettingsUILanguageFallback](task-sequence-variables.md#OSDWindowsSettingsUILanguageFallback)
- [OSDWindowsSettingsUserLocale](task-sequence-variables.md#OSDWindowsSettingsUserLocale)

### <a name="cmdlets-for-apply-windows-settings"></a>Cmdlets für „Windows-Einstellungen anwenden“

Verwalten Sie diesen Schritt mit den folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyWindowsSetting](/powershell/module/configurationmanager/Get-CMTSStepApplyWindowsSetting)
- [New-CMTSStepApplyWindowsSetting](/powershell/module/configurationmanager/Get-CMTSStepApplyWindowsSetting)
- [Remove-CMTSStepApplyWindowsSetting](/powershell/module/configurationmanager/Remove-CMTSStepApplyWindowsSetting)
- [Set-CMTSStepApplyWindowsSetting](/powershell/module/configurationmanager/Set-CMTSStepApplyWindowsSetting)

### <a name="properties-for-apply-windows-settings"></a>Eigenschaften für „Windows-Einstellungen anwenden“

Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

#### <a name="user-name"></a>Benutzername

Geben Sie den registrierten Benutzernamen an, der dem Zielcomputer zugeordnet wird. Der Wert, den der Tasksequenzschritt **Windows-Einstellungen erfassen** erfasst, kann diesen Wert überschreiben.  

#### <a name="organization-name"></a>Organisationsname

Geben Sie den registrierten Organisationsnamen an, der dem Zielcomputer zugeordnet wird. Der Wert, den der Tasksequenzschritt **Windows-Einstellungen erfassen** erfasst, kann diesen Wert überschreiben.  

#### <a name="product-key"></a>Product Key  

Geben Sie den Product Key an, der für die Windows-Installation auf dem Zielcomputer verwendet wird.  

#### <a name="server-licensing"></a>Serverlizenzierung

Geben Sie den Serverlizenzierungsmodus an.

- Wählen Sie als Lizenzierungsmodus **Pro Server** oder **Pro Benutzer** aus.  
- Wenn Sie **Pro Server** auswählen, geben Sie ebenfalls die maximale Anzahl von Verbindungen an, die gemäß Ihrem Lizenzvertrag zulässig ist.  
- Falls der Zielcomputer kein Server ist oder Sie den Lizenzierungsmodus nicht angeben möchten, wählen Sie **Nicht angeben** aus.  

#### <a name="maximum-connections"></a>Maximale Verbindungen

> [!NOTE]
> Diese Einstellung gilt nur für alte Windows-Versionen, die nicht mehr unterstützt werden.<!-- #4833 -->

#### <a name="randomly-generate-the-local-administrator-password-and-disable-the-account-on-all-supported-platforms-recommended"></a>Lokales Administratorkennwort zufällig erstellen und das Konto auf allen unterstützten Plattformen deaktivieren (empfohlen)  

Wählen Sie diese Option aus, um das lokale Administratorkennwort auf eine zufällig generierte Zeichenfolge festzulegen. Diese Option deaktiviert das lokale Administratorkonto auf allen Plattformen, die diese Funktion unterstützen.  

#### <a name="enable-the-account-and-specify-the-local-administrator-password"></a>Konto aktivieren und lokales Administratorkennwort angeben  

Wählen Sie diese Option aus, um das lokale Administratorkonto mithilfe des angegebenen Kennworts zu aktivieren. Geben Sie das Kennwort in der Zeile **Kennwort** ein, und bestätigen Sie es in der Zeile **Kennwort bestätigen** .  

#### <a name="time-zone"></a>Zeitzone

Geben Sie die zu konfigurierende Zeitzone auf dem Zielcomputer an. Der Wert, den der Tasksequenzschritt **Windows-Einstellungen erfassen** erfasst, kann diesen Wert überschreiben.  

#### <a name="language-settings"></a>Spracheinstellungen

<!--5411057, 5138936-->

Ab Version 1910 können Sie die Sprachkonfiguration während der Betriebssystembereitstellung steuern. Wenn Sie diese Spracheinstellungen bereits anwenden, kann diese Änderung Ihnen helfen, Ihre Tasksequenz für die Betriebssystembereitstellung zu vereinfachen. Anstatt für jede Sprache mehrere Schritte oder separate Skripts auszuführen, verwenden Sie pro Sprache eine Instanz dieses integrierten Schritts mit einer Bedingung für die entsprechende Sprache.

Konfigurieren Sie die folgenden Einstellungen:

- Eingabegebietsschema (Standardtastaturlayout)
- Gebietsschema des Systems
- Sprache der Benutzeroberfläche
- Fallback für die Sprache der Benutzeroberfläche
- Gebietsschema des Benutzers

Weitere Informationen zu diesen Werten für die Antwortdatei des Windows-Setups finden Sie unter [Microsoft-Windows-International-Core](/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core).

> [!NOTE]
> Wenn Sie eine benutzerdefinierte Windows-Setup-Antwortdatei (unattend.xml) erstellen, überschreibt dieser Schritt alle vorhandenen Werte. Um einen dynamischen Prozess für diese Einstellungen zu automatisieren, verwenden Sie die zugehörigen Tasksequenzvariablen. Beispiel: [OSDWindowsSettingsInputLocale](task-sequence-variables.md#OSDWindowsSettingsInputLocale). 

## <a name="auto-apply-drivers"></a><a name="BKMK_AutoApplyDrivers"></a> Treiber automatisch anwenden

Verwenden Sie diesen Schritt, um Gerätetreiber anzupassen und als Teil der Betriebssystembereitstellung zu installieren.  

> [!IMPORTANT]  
> Eigenständige Medien können den Schritt **Treiber automatisch anwenden** nicht verwenden. Die Tasksequenz hat in diesem Szenario keine Verbindung zum Configuration Manager-Standort.  

Dieser Tasksequenzschritt wird nur in Windows PE ausgeführt. Er kann nicht in der Vollversion des Betriebssystems ausgeführt werden.

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Treiber** und dann **Treiber automatisch anwenden** aus.

> [!TIP]
> Eine Übersicht über die Treiber in Configuration Manager erhalten Sie unter [Verwenden von Tasksequenzen zum Installieren von Treibern](../get-started/manage-drivers.md#BKMK_TSDrivers).

### <a name="behaviors-for-auto-apply-drivers"></a>Verhalten für „Treiber automatisch anwenden“

Mit dem Tasksequenzschritt **Treiber automatisch anwenden** werden folgende Aktionen ausgeführt:  

1. Überprüft die Hardware und ermittelt die Plug & Play-IDs für alle auf dem System vorhandenen Geräte.  

2. Sendet die Liste mit den Geräten und den ihnen zugeordneten Plug & Play-IDs an den Verwaltungspunkt. Der Verwaltungspunkt gibt für jedes Hardwaregerät eine Liste mit kompatiblen Treibern aus dem Treiberkatalog zurück. Die Liste enthält alle aktivierten Treiber, unabhängig von ihrem Treiberpaket, und Treiber, die mit der angegebenen Treiberkategorie gekennzeichnet sind.  

3. Die Tasksequenz wählt für jedes Hardwaregerät den besten Treiber aus. Dieser Treiber ist für das bereitgestellte Betriebssystem geeignet und befindet sich auf einem verfügbaren Verteilungspunkt.  

4. Die Tasksequenz lädt die ausgewählten Treiber von einem Verteilungspunkt herunter und stellt diese auf dem Zielbetriebssystem bereit.  

    1. Beim Verwenden eines Betriebssystemimages platziert die Tasksequenz die Treiber im Betriebssystem-Treiberspeicher.  

    2. Beim Verwenden eines Betriebssystemupgrade-Pakets als ursprüngliche Installationsquelle, konfiguriert die Tasksequenz Windows Setup mit dem Speicherort der Treiber.  

5. Während der Schritt **Windows und ConfigMgr einrichten** in der Tasksequenz ausgeführt wird, sucht Windows Setup nach den von diesem Schritt bereitgestellten Treibern.  

### <a name="variables-for-auto-apply-drivers"></a>Variablen für „Treiber automatisch anwenden“

Verwenden Sie die folgenden Tasksequenzvariablen in diesem Schritt:  

- [OSDAutoApplyDriverBestMatch](task-sequence-variables.md#OSDAutoApplyDriverBestMatch)  
- [OSDAutoApplyDriverCategoryList](task-sequence-variables.md#OSDAutoApplyDriverCategoryList)  
- [SMSTSDriverRequestConnectTimeOut](task-sequence-variables.md#SMSTSDriverRequestConnectTimeOut)  
- [SMSTSDriverRequestReceiveTimeOut](task-sequence-variables.md#SMSTSDriverRequestReceiveTimeOut)  
- [SMSTSDriverRequestResolveTimeOut](task-sequence-variables.md#SMSTSDriverRequestResolveTimeOut)  
- [SMSTSDriverRequestSendTimeOut](task-sequence-variables.md#SMSTSDriverRequestSendTimeOut)  

### <a name="cmdlets-for-auto-apply-drivers"></a>Cmdlets für „Treiber automatisch anwenden“

Verwalten Sie diesen Schritt mit den folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepAutoApplyDriver](/powershell/module/configurationmanager/Get-CMTSStepAutoApplyDriver)
- [New-CMTSStepAutoApplyDriver](/powershell/module/configurationmanager/New-CMTSStepAutoApplyDriver)
- [Remove-CMTSStepAutoApplyDriver](/powershell/module/configurationmanager/Remove-CMTSStepAutoApplyDriver)
- [Set-CMTSStepAutoApplyDriver](/powershell/module/configurationmanager/Set-CMTSStepAutoApplyDriver)

### <a name="properties-for-auto-apply-drivers"></a>Eigenschaften für „Treiber automatisch anwenden“

Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

#### <a name="install-only-the-best-matched-compatible-drivers"></a>Nur Treiber mit der höchsten Kompatibilität installieren

Hiermit wird angegeben, dass vom Tasksequenzschritt nur der am besten geeignete Treiber für das jeweilige erkannte Hardwaregerät installiert wird.  

#### <a name="install-all-compatible-drivers"></a>Alle kompatiblen Treiber installieren

Die Tasksequenz installiert alle Treiber, die mit dem jeweiligen ermittelten Hardwaregerät kompatibel sind. Windows Setup wählt anschließend den besten Treiber aus. Diese Option beansprucht mehr Netzwerkbandbreite und Festplattenspeicher. Die Tasksequenz lädt mehr Treiber herunter, wodurch Windows jedoch einen besseren Treiber auswählen kann.  

#### <a name="consider-drivers-from-all-categories"></a>Treiber aller Kategorien berücksichtigen

Die Tasksequenz durchsucht alle verfügbaren Treiberkategorien nach den geeigneten Gerätetreibern.  

#### <a name="limit-driver-matching-to-only-consider-drivers-in-selected-categories"></a>Nur Treiber in bestimmten Kategorien berücksichtigen

Die Tasksequenz durchsucht die angegebenen Treiberkategorien nach den geeigneten Gerätetreibern.  

Wenn Sie mehrere Kategorien auswählen, werden alle passenden Treiber aus den Kategorien zurückgegeben. Dies entspricht einem Vorgang vom Typ `OR`.<!-- SCCMDocs issue 851 -->

#### <a name="do-unattended-installation-of-unsigned-drivers-on-versions-of-windows-where-this-is-allowed"></a>Unbeaufsichtigte Installation von nicht signierten Treibern bei Windows-Versionen ausführen, wenn zulässig

Durch diese Option können Sie unter Windows Treiber ohne digitale Signatur installieren.  

> [!IMPORTANT]  
> Diese Option gilt nicht für Betriebssysteme, deren Richtlinie für Treibersignierung nicht konfiguriert werden kann.  



## <a name="capture-network-settings"></a><a name="BKMK_CaptureNetworkSettings"></a> Netzwerkeinstellungen erfassen

Verwenden Sie diesen Schritt zum Erfassen der Microsoft-Netzwerkeinstellungen des Computers, auf dem die Tasksequenz ausgeführt wird. Die Tasksequenz speichert diese Einstellungen in Tasksequenzvariablen. Diese Einstellungen setzen die Standardeinstellungen außer Kraft, die Sie im Schritt **Netzwerkeinstellungen anwenden** konfigurieren.  

Dieser Tasksequenzschritt wird nur in der Vollversion des Betriebssystems ausgeführt. Er kann nicht in Windows PE ausgeführt werden.  

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Einstellungen** und dann **Netzwerkeinstellungen erfassen** aus.

### <a name="variables-for-capture-network-settings"></a>Variablen für „Netzwerkeinstellungen erfassen“

Verwenden Sie die folgenden Tasksequenzvariablen in diesem Schritt:  

- [OSDMigrateAdapterSettings](task-sequence-variables.md#OSDMigrateAdapterSettings)  
- [OSDMigrateNetworkMembership](task-sequence-variables.md#OSDMigrateNetworkMembership)  

### <a name="cmdlets-for-capture-network-settings"></a>Cmdlets für „Netzwerkeinstellungen erfassen“

Verwalten Sie diesen Schritt mit den folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureNetworkSettings](/powershell/module/configurationmanager/Get-CMTSStepCaptureNetworkSettings)
- [New-CMTSStepCaptureNetworkSettings](/powershell/module/configurationmanager/New-CMTSStepCaptureNetworkSettings)
- [Remove-CMTSStepCaptureNetworkSettings](/powershell/module/configurationmanager/Remove-CMTSStepCaptureNetworkSettings)
- [Set-CMTSStepCaptureNetworkSettings](/powershell/module/configurationmanager/Set-CMTSStepCaptureNetworkSettings)

### <a name="properties-for-capture-network-settings"></a>Eigenschaften für „Netzwerkeinstellungen erfassen“

Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

#### <a name="migrate-domain-and-workgroup-membership"></a>Domänen- und Arbeitsgruppenmitgliedschaft migrieren

Hiermit werden Informationen zur Domänen- und Arbeitsgruppenmitgliedschaft des Zielcomputers erfasst.  

#### <a name="migrate-network-adapter-configuration"></a>Netzwerkkartenkonfiguration migrieren

Hiermit wird die Netzwerkadapterkonfiguration des Zielcomputers erfasst. Die folgenden Informationen werden erfasst:

- Globale Netzwerkeinstellungen  
- Anzahl von Adaptern  
- Die folgenden Netzwerkeinstellungen, die jedem Adapter zugeordnet sind: DNS, WINS, IP und Portfilter



## <a name="capture-operating-system-image"></a><a name="BKMK_CaptureOperatingSystemImage"></a> Betriebssystemabbild erfassen

Dieser Schritt erfasst mindestens ein Image von einem Referenzcomputer. Die Tasksequenz erstellt eine Windows-Imagedatei (WIM) auf der angegebenen Netzwerkfreigabe. Verwenden Sie dann den Assistenten zum **Hinzufügen eines Betriebssystemimagepakets**, um dieses Image für imagebasierte Betriebssystembereitstellungen in Configuration Manager zu importieren.  

Configuration Manager erfasst jedes Volume (Laufwerk) des Referenzcomputers in einem separaten Image innerhalb der WIM-Datei. Wenn der Referenzcomputer über mehrere Volumes verfügt, enthält die erstellte WIM-Datei für jedes Volume ein separates Image. Dieser Schritt erfasst nur als NTFS oder FAT32 formatierte Volumes. Volumes in anderen Formaten und USB-Volumes werden übersprungen.  

Das auf dem Referenzcomputer installierte Betriebssystem muss eine von Configuration Manager unterstützte Windows-Version sein. Verwenden Sie das SysPrep-Tool, um das Betriebssystem auf dem Referenzcomputer vorzubereiten. Bei dem Betriebssystemvolume und dem Startvolume muss es sich um dasselbe Volume handeln.  

Geben Sie ein Konto mit Schreibberechtigungen für die ausgewählte Netzwerkfreigabe an. Weitere Informationen zu Konten für die Erfassung des Betriebssystemimages finden Sie unter [Konten](../../core/plan-design/hierarchy/accounts.md#capture-os-image-account).

Dieser Tasksequenzschritt wird nur in Windows PE ausgeführt. Er kann nicht in der Vollversion des Betriebssystems ausgeführt werden.

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Images** und dann **Betriebssystemimage erfassen** aus.

### <a name="variables-for-capture-os-image"></a>Variablen für „Betriebssystemimage erfassen“

Verwenden Sie die folgenden Tasksequenzvariablen in diesem Schritt:  

- [OSDCaptureAccount](task-sequence-variables.md#OSDCaptureAccount)  
- [OSDCaptureAccountPassword](task-sequence-variables.md#OSDCaptureAccountPassword)  
- [OSDCaptureDestination](task-sequence-variables.md#OSDCaptureDestination)  
- [OSDImageCreator](task-sequence-variables.md#OSDImageCreator)  
- [OSDImageDescription](task-sequence-variables.md#OSDImageDescription)  
- [OSDImageVersion](task-sequence-variables.md#OSDImageVersion)  
- [OSDTargetSystemRoot](task-sequence-variables.md#OSDTargetSystemRoot-input)  

### <a name="cmdlets-for-capture-os-image"></a>Cmdlets für „Betriebssystemimage erfassen“

Verwalten Sie diesen Schritt mit den folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureSystemImage](/powershell/module/configurationmanager/Get-CMTSStepCaptureSystemImage)
- [New-CMTSStepCaptureSystemImage](/powershell/module/configurationmanager/New-CMTSStepCaptureSystemImage)
- [Remove-CMTSStepCaptureSystemImage](/powershell/module/configurationmanager/Remove-CMTSStepCaptureSystemImage)
- [Set-CMTSStepCaptureSystemImage](/powershell/module/configurationmanager/Set-CMTSStepCaptureSystemImage)

### <a name="properties-for-capture-os-image"></a>Eigenschaften für „Betriebssystemimage erfassen“

Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

#### <a name="target"></a>Ziel  

Diesen Dateisystempfad verwendet Configuration Manager zum Speichern des erfassten Betriebssystemimages.  

#### <a name="description"></a>Beschreibung  

Diese optionale benutzerdefinierte Beschreibung des erfassten Betriebssystemimages wird in der Imagedatei gespeichert.  

#### <a name="version"></a>Version  

Diese optionale benutzerdefinierte Versionsnummer wird dem erfassten Betriebssystemimage zugewiesen. Dieser Wert kann aus einer beliebigen Kombination aus Buchstaben und Ziffern bestehen. Er wird in der Imagedatei gespeichert.  

#### <a name="created-by"></a>Erstellt von  

Dieser optionale Name des Benutzers wird vom Betriebssystemimage erstellt. Er wird in der Imagedatei gespeichert.  

#### <a name="capture-operating-system-image-account"></a>Konto für die Erfassung des Betriebssystemabbilds  

Geben Sie das Windows-Konto ein, das über Berechtigungen für die angegebene Netzwerkfreigabe verfügt. Wählen Sie **Festlegen** aus, um den Namen des Windows-Kontos anzugeben.  



## <a name="capture-user-state"></a><a name="BKMK_CaptureUserState"></a> Benutzerzustand erfassen

Dieser Schritt erfasst mithilfe des Migrationstools für den Benutzerstatus (USMT) den Benutzerstatus und die Einstellungen des Computers, der die Tasksequenz ausführt. Dieser Tasksequenzschritt wird in Verbindung mit dem Tasksequenzschritt **Benutzerzustand wiederherstellen** verwendet. Dieser Schritt verschlüsselt den USMT-Statusspeicher immer mit einem Verschlüsselungsschlüssel, den Configuration Manager generiert und verwaltet.  

Weitere Informationen zum Verwalten des Benutzerzustands beim Bereitstellen von Betriebssystemen finden Sie unter [Verwalten des Benutzerzustands](../get-started/manage-user-state.md).  

Wenn Sie die Einstellungen für den Benutzerstatus von einem Zustandsmigrationspunkt aus speichern und wiederherstellen möchten, verwenden Sie diesen Schritt mit den Schritten **Statusspeicher anfordern** und **Statusspeicher freigeben**.  

Dieser Schritt ermöglicht die Steuerung über eine begrenzte Teilmenge der am häufigsten verwendeten USMT-Optionen. Geben Sie zusätzliche Befehlszeilenoptionen mithilfe der Tasksequenzvariablen **OSDMigrateAdditionalCaptureOptions** an.  

Dieser Tasksequenzschritt wird nur in Windows PE ausgeführt. Er kann nicht in der Vollversion des Betriebssystems ausgeführt werden.  

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Benutzerstatus** und dann **Benutzerstatus erfassen** aus.

### <a name="variables-for-capture-user-state"></a>Variablen für „Benutzerzustand erfassen“

Verwenden Sie die folgenden Tasksequenzvariablen in diesem Schritt:  

- [_OSDMigrateUsmtPackageID](task-sequence-variables.md#OSDMigrateUsmtPackageID)  
- [OSDMigrateAdditionalCaptureOptions](task-sequence-variables.md#OSDMigrateAdditionalCaptureOptions)  
- [OSDMigrateConfigFiles](task-sequence-variables.md#OSDMigrateConfigFiles)  
- [OSDMigrateContinueOnLockedFiles](task-sequence-variables.md#OSDMigrateContinueOnLockedFiles)  
- [OSDMigrateEnableVerboseLogging](task-sequence-variables.md#OSDMigrateEnableVerboseLogging)  
- [OSDMigrateMode](task-sequence-variables.md#OSDMigrateMode)  
- [OSDMigrateSkipEncryptedFiles](task-sequence-variables.md#OSDMigrateSkipEncryptedFiles)  
- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-capture-user-state"></a>Cmdlets für „Benutzerzustand erfassen“

Verwalten Sie diesen Schritt mit den folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureUserState](/powershell/module/configurationmanager/Get-CMTSStepCaptureUserState)
- [New-CMTSStepCaptureUserState](/powershell/module/configurationmanager/New-CMTSStepCaptureUserState)
- [Remove-CMTSStepCaptureUserState](/powershell/module/configurationmanager/Remove-CMTSStepCaptureUserState)
- [Set-CMTSStepCaptureUserState](/powershell/module/configurationmanager/Set-CMTSStepCaptureUserState)

### <a name="properties-for-capture-user-state"></a>Eigenschaften für „Benutzerzustand erfassen“

Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

#### <a name="user-state-migration-tool-package"></a>USMT-Paket (Migrationsprogramm für den Benutzerzustand)

Geben Sie das Paket an, das das Migrationstool für den Benutzerstatus (USMT) enthält. Die Tasksequenz verwendet diese Version von USMT, um den Benutzerzustand und die Benutzereinstellungen zu erfassen. Für dieses Paket ist kein Programm erforderlich. Geben Sie ein Paket an, das die 32-Bit- oder 64-Bit-Version von USMT enthält. Die USMT-Architektur richtet sich nach der Architektur des Betriebssystems, dessen Status die Tasksequenz erfasst.  

#### <a name="capture-all-user-profiles-with-standard-options"></a>Alle Benutzerprofile mit Standardoptionen erfassen

Migrieren Sie alle Benutzerprofilinformationen. Dies ist die Standardoption.  

Wenn Sie diese Option festlegen, ohne in Schritt **Benutzerstatus wiederherstellen** **Lokale Computerbenutzerprofile wiederherstellen** auszuwählen, schlägt die Tasksequenz fehl. Configuration Manager kann neue Konten nicht migrieren, ohne diesen Kennwörter zuzuweisen.

Wenn Sie die Option **Install an existing image package** (Bestehendes Imagepaket installieren) des Assistenten **Neue Tasksequenz** verwenden, wird die resultierende Tasksequenz standardmäßig auf **Alle Benutzerprofile mit Standardoptionen erfassen** festgelegt. Diese Standardtasksequenz wählt nicht die Option **Lokale Computerbenutzerprofile wiederherstellen** oder Benutzerkonten außerhalb der Domäne aus.  

Wählen Sie **Lokale Computerbenutzerprofile wiederherstellen** aus, und geben Sie für das zu migrierende Konto ein Kennwort ein. In einer manuell erstellten Tasksequenz finden Sie diese Einstellung in Schritt **Benutzerstatus wiederherstellen**. Wird die Tasksequenz vom **Tasksequenzerstellungs-Assistenten** erstellt, befindet sich diese Einstellung auf der Seite **Benutzerdateien und -einstellungen wiederherstellen** des Assistenten.  

Wenn Sie keine lokalen Benutzerkonten haben, ist diese Einstellung nicht relevant.  

#### <a name="customize-how-user-profiles-are-captured"></a>Erfassung der Benutzerprofile anpassen

Wählen Sie diese Option aus, um eine benutzerdefinierte Profildatei für die Migration anzugeben. Wählen Sie **Dateien** aus, um die von USMT bei diesem Schritt zu verwendenden Konfigurationsdateien auszuwählen. Geben Sie eine benutzerdefinierte XML-Datei an, die Regeln zur Definition der zu migrierenden Benutzerzustandsdateien enthält.  

#### <a name="click-here-to-select-configuration-files"></a>Klicken Sie zum Auswählen der Konfigurationsdateien auf diese Schaltfläche

Wählen Sie diese Option aus, um im USMT-Paket die Konfigurationsdateien auszuwählen, die Sie zum Erfassen von Benutzerprofilen verwenden möchten. Wählen Sie die Schaltfläche **Dateien** aus, um das Dialogfeld **Konfigurationsdateien** zu öffnen. Zum Angeben einer Konfigurationsdatei geben Sie in die Zeile **Dateiname** den Dateinamen ein und wählen die Schaltfläche **Hinzufügen** aus.  

#### <a name="enable-verbose-logging"></a>Ausführliche Protokollierung aktivieren

Aktivieren Sie diese Option, um ausführlichere Protokolldateiinformationen zu generieren. Wenn der Status erfasst wird, generiert die Tasksequenz standardmäßig die Datei **ScanState.log** im Tasksequenz-Protokollordner `%WinDir%\ccm\logs`.  

#### <a name="skip-files-using-encrypted-file-system"></a>Dateien mit EFS (Encrypted File System) überspringen

Aktivieren Sie diese Option, um das Erfassen von Dateien zu überspringen, die mit EFS (Encrypted File System, verschlüsselndes Dateisystem) verschlüsselt wurden. Diese Dateien enthalten Benutzerprofildateien. Je nach Betriebssystem und USMT-Version sind verschlüsselte Dateien nach der Wiederherstellung möglicherweise nicht lesbar. Weitere Informationen finden Sie in der USMT-Dokumentation.  

#### <a name="copy-by-using-file-system-access"></a>Mithilfe des normalen Dateisystemzugriffs kopieren

Aktivieren Sie diese Option, um alle oder einige der folgenden Einstellungen anzugeben:  

- **Fortsetzen, wenn einige Dateien nicht erfasst werden können**: Aktivieren Sie diese Einstellung, um den Migrationsprozess auch dann fortzusetzen, wenn einige Dateien nicht erfasst werden können. Wenn Sie diese Option deaktivieren und eine Datei nicht erfasst wird, kann dieser Schritt nicht ausgeführt werden. Diese Option ist standardmäßig aktiviert.  

- **Lokal erfassen mithilfe von Links statt durch Kopieren von Dateien**: Aktivieren Sie diese Einstellung, um feste NTFS-Links zum Erfassen von Dateien zu verwenden.  

    Weitere Informationen zum Migrieren von Daten mit festen Links finden Sie unter [Migrationsspeicher mit festem Link](/windows/deployment/usmt/usmt-hard-link-migration-store).  

- **Im Offlinemodus erfassen (nur Windows PE)** : Aktivieren Sie diese Einstellung, um den Benutzerstatus nicht im vollständigen Betriebssystem, sondern in Windows PE zu erfassen.  

#### <a name="capture-by-using-volume-copy-shadow-services-vss"></a>Mithilfe des Volumeschattenkopie-Diensts (VSS) erfassen

Mithilfe dieser Option können Sie Dateien sogar dann erfassen, wenn sie durch eine andere Anwendung zur Bearbeitung gesperrt sind.  



## <a name="capture-windows-settings"></a><a name="BKMK_CaptureWindowsSettings"></a> Windows-Einstellungen erfassen

Verwenden Sie diesen Schritt zum Erfassen der Windows-Einstellungen des Computers, auf dem die Tasksequenz ausgeführt wird. Die Tasksequenz speichert diese Einstellungen in Tasksequenzvariablen. Diese erfassten Einstellungen setzen die Standardeinstellungen außer Kraft, die Sie im Schritt **Windows-Einstellungen anwenden** konfigurieren.  

Dieser Tasksequenzschritt wird in der Vollversion des Betriebssystems oder Windows PE ausgeführt.  

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Einstellungen** und dann **Windows-Einstellungen erfassen** aus.

### <a name="variables-for-capture-windows-settings"></a>Variablen für „Windows-Einstellungen erfassen“

Verwenden Sie die folgenden Tasksequenzvariablen in diesem Schritt:  

- [OSDComputerName](task-sequence-variables.md#OSDComputerName-output)  
- [OSDMigrateComputerName](task-sequence-variables.md#OSDMigrateComputerName)  
- [OSDMigrateRegistrationInfo](task-sequence-variables.md#OSDMigrateRegistrationInfo)  
- [OSDMigrateTimeZone](task-sequence-variables.md#OSDMigrateTimeZone)  
- [OSDRegisteredOrgName](task-sequence-variables.md#OSDRegisteredOrgName-output)  
- [OSDTimeZone](task-sequence-variables.md#OSDTimeZone-output)  

### <a name="cmdlets-for-capture-windows-settings"></a>Cmdlets für „Windows-Einstellungen erfassen“

Verwalten Sie diesen Schritt mit den folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureWindowsSettings](/powershell/module/configurationmanager/Get-CMTSStepCaptureWindowsSettings)
- [New-CMTSStepCaptureWindowsSettings](/powershell/module/configurationmanager/New-CMTSStepCaptureWindowsSettings)
- [Remove-CMTSStepCaptureWindowsSettings](/powershell/module/configurationmanager/Remove-CMTSStepCaptureWindowsSettings)
- [Set-CMTSStepCaptureWindowsSettings](/powershell/module/configurationmanager/Set-CMTSStepCaptureWindowsSettings)

### <a name="properties-for-capture-windows-settings"></a>Eigenschaften für „Windows-Einstellungen erfassen“

Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

#### <a name="migrate-computer-name"></a>Computernamen migrieren

Erfassen Sie den NetBIOS-Computernamen des Computers.  

#### <a name="migrate-registered-user-and-organization-names"></a>Registrierte Benutzer- und Organisationsnamen migrieren

Erfassen Sie auf dem Computer die Namen registrierter Benutzer und Organisationen.  

#### <a name="migrate-time-zone"></a>Zeitzone migrieren

Erfassen Sie die Zeitzoneneinstellungen auf dem Computer.  


## <a name="check-readiness"></a><a name="BKMK_CheckReadiness"></a> Bereitschaft überprüfen

Verwenden Sie diesen Schritt, um zu überprüfen, ob der Zielcomputer die Voraussetzungen für die Bereitstellung erfüllt.  

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Allgemein** und dann **Bereitschaft überprüfen** aus.

Ab Version 2002 beinhaltet dieser Schritt acht neue Überprüfungen. Keine dieser neuen Überprüfungen sind in neuen oder vorhandenen Instanzen des Schritts standardmäßig ausgewählt.<!--6005561--> Weitere Informationen zu den einzelnen Überprüfungen finden Sie in den entsprechenden Abschnitten unten.

- **Architektur des aktuellen Betriebssystems**
- **Minimales Release des Betriebssystems**
- **Maximales Release des Betriebssystems**
- **Mindestversion des Clients**
- **Sprache des aktuellen Betriebssystems**
- **Netzteil angeschlossen**
- **Netzwerkadapter verbunden**
  - **Netzwerkadapter nicht drahtlos**

Ab Version 2006 umfasst dieser Schritt eine Überprüfung, um zu ermitteln, ob das Gerät UEFI verwendet: **Überprüfen, ob sich der Computer im UEFI-Modus befindet**.<!--6452769-->

> [!IMPORTANT]
> Wenn Sie diese neuen Configuration Manager-Features nach der Aktualisierung des Standorts nutzen möchten, müssen Sie auch Clients auf die neueste Version aktualisieren. Beim Update des Standorts und der Konsole werden neue Features in der Configuration Manager-Konsole angezeigt. Das vollständige Szenario ist allerdings erst einsatzbereit, wenn auch die Clientversion aktualisiert wird.

**smsts.log** enthält das Ergebnis aller Überprüfungen. Wenn eine Überprüfung fehlschlägt, wertet die Tasksequenz-Engine trotzdem alle anderen Überprüfungen aus. Der Schritt schlägt also nicht fehl, bevor alle Überprüfungen abgeschlossen wurden. Wenn mindestens eine Überprüfung fehlschlägt, schlägt der gesamte Schritt fehl, und der Fehlercode **4316** wird zurückgegeben. Dieser Fehlercode bedeutet, dass die für diesen Vorgang erforderliche Ressource nicht vorhanden ist.

### <a name="variables-for-check-readiness"></a>Variablen für „Bereitschaft überprüfen“

Verwenden Sie die folgenden Tasksequenzvariablen in diesem Schritt:  

- [_TS_CRMEMORY](task-sequence-variables.md#TSCRMEMORY)
- [_TS_CRSPEED](task-sequence-variables.md#TSCRSPEED)
- [_TS_CRDISK](task-sequence-variables.md#TSCRDISK)
- [_TS_CROSTYPE](task-sequence-variables.md#TSCROSTYPE)
- [_TS_CRARCH](task-sequence-variables.md#TSCRARCH) (ab Version 2002)
- [_TS_CRMINOSVER](task-sequence-variables.md#TSCRMINOSVER) (ab Version 2002)
- [_TS_CRMAXOSVER](task-sequence-variables.md#TSCRMAXOSVER) (ab Version 2002)
- [_TS_CRCLIENTMINVER](task-sequence-variables.md#TSCRCLIENTMINVER) (ab Version 2002)
- [_TS_CROSLANGUAGE](task-sequence-variables.md#TSCROSLANGUAGE) (ab Version 2002)
- [_TS_CRACPOWER](task-sequence-variables.md#TSCRACPOWER) (ab Version 2002)
- [_TS_CRNETWORK](task-sequence-variables.md#TSCRNETWORK) (ab Version 2002)
- [_TS_CRUEFI](task-sequence-variables.md#TSCRUEFI) (ab Version 2006)
- [_TS_CRWIRED](task-sequence-variables.md#TSCRWIRED) (ab Version 2002)

### <a name="cmdlets-for-check-readiness"></a>Cmdlets für „Bereitschaft überprüfen“

Verwalten Sie diesen Schritt mit den folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPrestartCheck](/powershell/module/configurationmanager/Get-CMTSStepPrestartCheck)
- [New-CMTSStepPrestartCheck](/powershell/module/configurationmanager/New-CMTSStepPrestartCheck)
- [Remove-CMTSStepPrestartCheck](/powershell/module/configurationmanager/Remove-CMTSStepPrestartCheck)
- [Set-CMTSStepPrestartCheck](/powershell/module/configurationmanager/Set-CMTSStepPrestartCheck)

### <a name="properties-for-check-readiness"></a>Eigenschaften für „Bereitschaft überprüfen“

Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

#### <a name="minimum-memory-mb"></a>Minimaler Arbeitsspeicher (MB)

Stellen Sie sicher, dass die Größe des Arbeitsspeichers (in Megabyte bzw. MB) der angegebenen Größe entspricht oder diese übersteigt. Der Schritt aktiviert diese Einstellung standardmäßig.  

#### <a name="minimum-processor-speed-mhz"></a>Mindestens erforderliche Prozessorgeschwindigkeit (MHz)  

Überprüfen Sie, dass die Geschwindigkeit des Prozessors (in Megahertz bzw. MHz) der angegebenen Geschwindigkeit entspricht oder diese übersteigt. Der Schritt aktiviert diese Einstellung standardmäßig.  

#### <a name="minimum-free-disk-space-mb"></a>Mindestens erforderlicher freier Speicherplatz (MB)

Stellen Sie sicher, dass die Größe des freien Speicherplatzes auf dem Datenträger (in Megabyte bzw. MB) der angegebenen Größe entspricht oder diese übersteigt.  

#### <a name="current-os-to-be-refreshed-is"></a>Aktuelles Betriebssystem, das aktualisiert wird

Überprüfen Sie, ob das auf dem Zielcomputer installierte Betriebssystem die angegebene Anforderung erfüllt. Der Schritt legt diese Einstellung standardmäßig auf **CLIENT** fest.  

#### <a name="architecture-of-current-os"></a>Architektur des aktuellen Betriebssystems

Ab Version 2002 sollten Sie überprüfen, ob es sich beim aktuellen Betriebssystem um eine **32 Bit**- oder eine **64 Bit**-Version handelt.

#### <a name="minimum-os-version"></a>Minimale Version des Betriebssystems

Ab Version 2002 sollten Sie überprüfen, ob das aktuell ausgeführte Betriebssystem eine Version aufweist, die höher als angegeben ist. Geben Sie die Version mit Hauptversion, Nebenversion und Buildnummer an. Beispiel: `10.0.16299`.

#### <a name="maximum-os-version"></a>Maximale Version des Betriebssystems

Ab Version 2002 sollten Sie überprüfen, ob das aktuell ausgeführte Betriebssystem eine Version aufweist, die älter als angegeben ist. Geben Sie die Version mit Hauptversion, Nebenversion und Buildnummer an. Beispiel: `10.0.18356`.

#### <a name="minimum-client-version"></a>Mindestversion des Clients

Ab Version 2002 sollten Sie überprüfen, ob die Version des Konfigurations-Manager-Clients mindestens die angegebene Version aufweist. Geben Sie die Clientversion im folgenden Format an: `5.00.8913.1005`.

#### <a name="language-of-current-os"></a>Sprache des aktuellen Betriebssystems

Ab Version 2002 sollten Sie überprüfen, ob die aktuelle Sprache des Betriebssystems mit der angegebenen übereinstimmt. Wählen Sie den Name der Sprache aus. In dem Schritt wird er mit dem zugeordneten Sprachcode verglichen. Diese Prüfung vergleicht die von Ihnen ausgewählte Sprache mit der **OSLanguage**-Eigenschaft der WMI-Klasse **Win32_OperatingSystem** auf dem Client.

#### <a name="ac-power-plugged-in"></a>Netzteil angeschlossen

Ab Version 2002 sollten Sie dafür sorgen, dass das Netzteil des Geräts angeschlossen ist und dass das Gerät nicht über Akku läuft.

#### <a name="network-adapter-connected"></a>Netzwerkadapter verbunden

Ab Version 2002 sollten Sie überprüfen, ob das Gerät über einen Netzwerkadapter verfügt, der mit dem Netzwerk verbunden ist. Sie können auch die entsprechende Überprüfung ausführen, um zu bestätigen, dass es sich um keinen **drahtlosen Netzwerkadapter** handelt.

#### <a name="computer-is-in-uefi-mode"></a>Computer befindet sich im UEFI-Modus

Ab Version 2006 können Sie ermitteln, ob das Gerät für UEFI oder BIOS konfiguriert ist.

### <a name="options-for-check-readiness"></a>Optionen für „Bereitschaft überprüfen“

> [!NOTE]  
> Wenn Sie die Einstellung **Bei Fehler fortsetzen** auf der Registerkarte **Optionen** dieses Schritts aktivieren, werden nur die Ergebnisse der Überprüfung auf Bereitschaft protokolliert. Wenn eine Überprüfung fehlschlägt, wird die Tasksequenz nicht beendet.  



## <a name="connect-to-network-folder"></a><a name="BKMK_ConnectToNetworkFolder"></a> Verbindung mit Netzwerkordner herstellen

Verwenden Sie diesen Schritt, um eine Verbindung mit einem freigegebenen Netzwerkordner herzustellen.  

Dieser Tasksequenzschritt wird in der Vollversion des Betriebssystems oder Windows PE ausgeführt.  

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Allgemein** und dann **Verbindung mit Netzwerkordner herstellen** aus.

### <a name="variables-for-connect-to-network-folder"></a>Variablen für „Verbindung mit Netzwerkordner herstellen“

Verwenden Sie die folgenden Tasksequenzvariablen in diesem Schritt:  

- [SMSConnectNetworkFolderAccount](task-sequence-variables.md#SMSConnectNetworkFolderAccount)  
- [SMSConnectNetworkFolderDriveLetter](task-sequence-variables.md#SMSConnectNetworkFolderDriveLetter)  
- [SMSConnectNetworkFolderPassword](task-sequence-variables.md#SMSConnectNetworkFolderPassword)  
- [SMSConnectNetworkFolderPath](task-sequence-variables.md#SMSConnectNetworkFolderPath)  

### <a name="cmdlets-for-connect-to-network-folder"></a>Cmdlets für „Verbindung mit Netzwerkordner herstellen“

Verwalten Sie diesen Schritt mit den folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepConnectNetworkFolder](/powershell/module/configurationmanager/Get-CMTSStepConnectNetworkFolder)
- [New-CMTSStepConnectNetworkFolder](/powershell/module/configurationmanager/New-CMTSStepConnectNetworkFolder)
- [Remove-CMTSStepConnectNetworkFolder](/powershell/module/configurationmanager/Remove-CMTSStepConnectNetworkFolder)
- [Set-CMTSStepConnectNetworkFolder](/powershell/module/configurationmanager/Set-CMTSStepConnectNetworkFolder)

### <a name="properties-for-connect-to-network-folder"></a>Eigenschaften für „Verbindung mit Netzwerkordner herstellen“

Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

#### <a name="path"></a>Pfad  

Wählen Sie **Durchsuchen** aus, um den Netzwerkordnerpfad anzugeben. Verwenden Sie das Format `\\server\share`.

#### <a name="drive"></a>Laufwerk  

Wählen Sie den Buchstaben des lokalen Laufwerks aus, das Sie dieser Verbindung zuweisen möchten.

#### <a name="account"></a>Konto

Wählen Sie **Festlegen** aus, um das Benutzerkonto mit den Berechtigungen zum Herstellen einer Verbindung mit diesem Netzwerkordner anzugeben. Weitere Informationen zu Netzwerkorder-Verbindungskonten der Tasksequenz finden Sie unter [Konten](../../core/plan-design/hierarchy/accounts.md#task-sequence-network-folder-connection-account).



## <a name="disable-bitlocker"></a><a name="BKMK_DisableBitLocker"></a> BitLocker deaktivieren

Verwenden Sie diesen Schritt, um die BitLocker-Verschlüsselung auf dem aktuellen Betriebssystemlaufwerk oder auf einem bestimmten Laufwerk zu deaktivieren. Danach sind die Schlüsselschutzvorrichtungen im Klartext auf der Festplatte sichtbar. Die Laufwerkinhalte werden nicht entschlüsselt. Diese Aktion wird fast sofort abgeschlossen.  

> [!NOTE]  
> BitLocker-Laufwerkverschlüsselung bietet eine niedrige Verschlüsselungsstufe der Inhalte eines Datenträgervolumes.  

Wenn Sie mehrere verschlüsselte Laufwerke haben, deaktivieren Sie BitLocker auf allen Datenlaufwerken, bevor Sie BitLocker auf dem Betriebssystemlaufwerk deaktivieren.  

Dieser Schritt wird nur in der Vollversion des Betriebssystems ausgeführt. Er kann nicht in Windows PE ausgeführt werden.  

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Datenträger** und dann **BitLocker deaktivieren** aus.

### <a name="variables-for-disable-bitlocker"></a>Variablen für „BitLocker deaktivieren“

Verwenden Sie ab Version 1906 bei diesem Schritt die folgenden Tasksequenzvariablen:  

- [OSDBitLockerRebootCount](task-sequence-variables.md#OSDBitLockerRebootCount)  
- [OSDBitLockerRebootCountOverride](task-sequence-variables.md#OSDBitLockerRebootCountOverride)  

### <a name="cmdlets-for-disable-bitlocker"></a>Cmdlets für „BitLocker deaktivieren“

Verwalten Sie diesen Schritt mit den folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepDisableBitLocker](/powershell/module/configurationmanager/Get-CMTSStepDisableBitLocker)
- [New-CMTSStepDisableBitLocker](/powershell/module/configurationmanager/New-CMTSStepDisableBitLocker)
- [Remove-CMTSStepDisableBitLocker](/powershell/module/configurationmanager/Remove-CMTSStepDisableBitLocker)
- [Set-CMTSStepDisableBitLocker](/powershell/module/configurationmanager/Set-CMTSStepDisableBitLocker)

### <a name="properties-for-disable-bitlocker"></a>Eigenschaften für „BitLocker deaktivieren“

Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

#### <a name="current-operating-system-drive"></a>Aktuelles Betriebssystemlaufwerk

Deaktiviert BitLocker auf dem aktuellen Betriebssystemlaufwerk.  

#### <a name="specific-drive"></a>Bestimmtes Laufwerk  

Deaktiviert BitLocker auf einem bestimmten Laufwerk. Geben Sie in der Dropdownliste das Laufwerk an, auf dem BitLocker deaktiviert ist.  

#### <a name="resume-protection-after-windows-has-been-restarted-the-specified-number-of-times"></a>Reaktivieren des Schutzes, nachdem Windows so oft wie angegeben neu gestartet wurde

<!-- 4512937 -->
Ab Version 1906: Legen Sie mit dieser Option die Anzahl der Neustarts fest, um BitLocker deaktiviert zu halten. Anstatt mehrere Instanzen dieses Schritts hinzuzufügen, legen Sie einen Wert von 1 (Standard) bis 15 fest.

Sie können dieses Verhalten mit den Tasksequenzvariablen [OSDBitLockerRebootCount](task-sequence-variables.md#OSDBitLockerRebootCount) und [OSDBitLockerRebootCountOverride](task-sequence-variables.md#OSDBitLockerRebootCountOverride) festlegen und ändern.


## <a name="download-package-content"></a><a name="BKMK_DownloadPackageContent"></a> Paketinhalt herunterladen

Verwenden Sie diesen Schritt, um einen der folgenden Pakettypen herunterzuladen:  

- Betriebssystemimages  
- Betriebssystemupgradepakete  
- Treiberpakete  
- Pakete  
- Startimages <sup>[Hinweis 1](#bkmk_note1)</sup>  

Dieser Schritt eignet sich gut in einer Tasksequenz, um ein Betriebssystem in den folgenden Szenarien zu aktualisieren:  

- Zum Verwenden einer einzigen Upgradetasksequenz für x86- und x64-Plattformen. Fügen Sie der Gruppe **Vorbereitung auf das Upgrade** zwei **Paketinhalt herunterladen**-Schritte hinzu. Legen Sie auf der Registerkarte **Optionen** Bedingungen fest, um die Clientarchitektur zu ermitteln und nur das entsprechende Betriebssystemupgrade-Paket herunterzuladen. Konfigurieren Sie jeden **Paketinhalt herunterladen**-Schritt, sodass dieselbe Variable verwendet wird. Verwenden Sie die Variable für den Medienpfad im Schritt **Betriebssystem aktualisieren**.  

- Um dynamisch ein passendes Treiberpaket herunterzuladen, verwenden Sie zwei **Paketinhalt herunterladen** -Schritte mit Bedingungen zum Ermitteln des geeigneten Hardwaretyps für jedes Treiberpaket. Konfigurieren Sie jeden **Paketinhalt herunterladen**-Schritt, sodass dieselbe Variable verwendet wird. Verwenden Sie die Variable für den Wert **Bereitgestellter Inhalt** im Abschnitt „Treiber“ des Schritts **Betriebssystem aktualisieren**.  

> [!NOTE]  
> Wenn Sie eine Tasksequenz bereitstellen, die diesen Schritt enthält, aktivieren Sie im Assistenten zum Bereitstellen von Software auf der Seite **Verteilungspunkte** für **Bereitstellungsoptionen** nicht **Den gesamten Inhalt vor Starten der Tasksequenz lokal herunterladen** oder **Auf Inhalt direkt vom Verteilungspunkt aus zugreifen**.  

Dieser Schritt wird in der Vollversion des Betriebssystems oder Windows PE ausgeführt. Windows PE unterstützt nicht die Option, Pakete im Configuration Manager-Clientcache zu speichern.

> [!NOTE]  
> Der Task **Paketinhalt herunterladen** wird für eigenständige Medien nicht unterstützt. Weitere Informationen finden Sie unter [Nicht unterstützte Aktionen für eigenständige Medien](../deploy-use/create-stand-alone-media.md#unsupported-actions-for-stand-alone-media).  

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Software** und dann **Paketinhalt herunterladen** aus.

### <a name="cmdlets-for-download-package-content"></a>Cmdlets für „Paketinhalt herunterladen“

Verwalten Sie diesen Schritt mit den folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepDownloadPackageContent](/powershell/module/configurationmanager/Get-CMTSStepDownloadPackageContent)
- [New-CMTSStepDownloadPackageContent](/powershell/module/configurationmanager/New-CMTSStepDownloadPackageContent)
- [Remove-CMTSStepDownloadPackageContent](/powershell/module/configurationmanager/Remove-CMTSStepDownloadPackageContent)
- [Set-CMTSStepDownloadPackageContent](/powershell/module/configurationmanager/Set-CMTSStepDownloadPackageContent)

### <a name="properties-for-download-package-content"></a>Eigenschaften für „Paketinhalt herunterladen“

Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

#### <a name="select-package"></a>Paket auswählen  

Wählen Sie das Symbol aus, um das Paket zum Herunterladen auszuwählen. Nachdem Sie ein Paket ausgewählt haben, wählen Sie erneut das Symbol aus, um ein anderes Paket auszuwählen.  

#### <a name="place-into-the-following-location"></a>In folgendem Verzeichnis speichern

Wählen Sie einen der folgenden Speicherorte für das Paket aus:  

- **Arbeitsverzeichnis für Tasksequenz**: Dieser Speicherort wird auch als Tasksequenzcache bezeichnet.  

- **Configuration Manager-Clientcache**: Verwenden Sie diese Option, um den Inhalt im Clientcache zu speichern. Dieser Pfad ist standardmäßig `%WinDir%\ccmcache`.  

- **Benutzerdefinierter Pfad**: Die Tasksequenz-Engine lädt das Paket zuerst in das Tasksequenz-Arbeitsverzeichnis herunter. Dann wird der Inhalt in den angegebenen Pfad verschoben. Die Tasksequenzengine hängt den Pfad mit der Paket-ID an.  

#### <a name="save-path-as-a-variable"></a>Pfad als Variable speichern

Speichern Sie den Paketpfad in einer benutzerdefinierten Tasksequenzvariablen. Verwenden Sie diese Variable dann in einem anderen Tasksequenzschritt.

Configuration Manager fügt dem Variablennamen ein numerisches Suffix hinzu. Sie geben beispielsweise eine Variable von `%MyContent%` als benutzerdefinierte Variable an. Es ist das Stammverzeichnis, in dem die Tasksequenz alle referenzierten Inhalte für diesen Schritt speichert. Diese Inhalte können mehrere Pakete enthalten. Wenn Sie auf die Variable verweisen, fügen Sie ein numerisches Suffix hinzu. Verweisen Sie für das erste Paket auf `%MyContent01%`. Wenn Sie in nachfolgenden Schritten auf die Variable verweisen, z.B. in **Betriebssystem aktualisieren**, verwenden Sie `%MyContent02%` oder `%MyContent03%`. Die Nummer entspricht der Reihenfolge, in der Schritt **Paketinhalt herunterladen** die Pakete auflistet.  

#### <a name="if-a-package-download-fails-continue-downloading-other-packages-in-the-list"></a>Wenn ein Fehler bei einem Paketdownload auftritt, mit anderen Paketen in der Liste fortfahren

Wenn die Tasksequenz ein Paket nicht herunterladen kann, startet es den Download des nächsten Pakets in der Liste.  

### <a name="note-1-use-of-boot-images-in-the-download-package-content-step"></a><a name="bkmk_note1"></a> Hinweis 1: Verwenden von Startimages im beim Download des Paketinhalts

*Gilt für Version 1910 und höher*<!-- SCCMDocs-pr #4202 -->

Wenn Sie die [Tasksequenzeigenschaften](../deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_prop-advanced) für das **Verwenden eines Startimages** konfigurieren, ist das Hinzufügen eines Startimages zu diesem Schritt überflüssig. Fügen Sie diesem Schritt nur dann ein Startimage hinzu, wenn es nicht in den Eigenschaften der Tasksequenz angegeben ist.

#### <a name="example-use-case"></a>Beispielanwendungsfall

- Eine einzelne Tasksequenz, um Inhalte vorab herunterzuladen:
  - Kein zugeordnetes Startimage.
  - Wird nur im vollständigen Betriebssystem ausgeführt, wahrscheinlich ohne Benutzerinteraktion.
  - Verwendet mehrere Schritte des Typs **Paketinhalt herunterladen** mit Bedingungen. Je nach spezifischer Sprache und Architektur werden Inhalte in den Clientcache heruntergeladen, um die Tasksequenz für die Bereitstellung des Betriebssystems vorzubereiten.
  - Es gibt nur eine Instanz dieser Tasksequenz, und zwar mit allen möglichen Inhaltsoptionen.

- Tasksequenzen für die Bereitstellung mehrerer Betriebssysteme:
  - eine Tasksequenz für eine normale Betriebssystembereitstellung
  - Auf ein Startimage wird in dessen Eigenschaften verwiesen.
  - Es gibt mehrere Instanzen dieser Tasksequenz, und zwar mit unterschiedlichen Startimages je nach Architektur und Sprache

## <a name="enable-bitlocker"></a><a name="BKMK_EnableBitLocker"></a> BitLocker aktivieren

BitLocker-Laufwerkverschlüsselung bietet eine niedrige Verschlüsselungsstufe der Inhalte eines Datenträgervolumes. Verwenden Sie diesen Schritt, um die BitLocker-Verschlüsselung auf mindestens zwei Partitionen auf der Festplatte zu aktivieren. Die erste aktive Partition enthält den Windows-Bootstrap-Code. Eine andere Partition beinhaltet das Betriebssystem. Die Bootstrap-Partition muss unverschlüsselt bleiben.  

Um BitLocker auf einem Laufwerk in Windows PE zu aktivieren, verwenden Sie den Schritt [BitLocker vorab bereitstellen](#BKMK_PreProvisionBitLocker).

Dieser Schritt wird nur in der Vollversion des Betriebssystems ausgeführt. Er kann nicht in Windows PE ausgeführt werden.

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Datenträger** und dann **BitLocker aktivieren** aus.

Wenn Sie **Nur TPM**, **TPM und Schlüssel zum Systemstart auf USB** oder **TPM-und-PIN** angeben, muss das Trusted Platform Module (TPM) sich in folgendem Zustand befinden, bevor Sie den Schritt **BitLocker aktivieren** ausführen können:  

- Aktiviert  
- Aktiviert  
- Besitz zulässig  

Ab Version 2006 können Sie diesen Schritt für Computer überspringen, die kein TPM besitzen oder auf denen das TPM nicht aktiviert ist. Eine neue Einstellung erleichtert die Verwaltung des Tasksequenzverhaltens auf Geräten, die BitLocker nicht vollständig unterstützen können.<!--6995601-->

Dieser Schritt schließt alle verbleibenden TPM-Initialisierungen ab. Die verbleibenden Aktionen erfordern keine physische Anwesenheit und keine Neustarts. Der Schritt **BitLocker aktivieren** führt die folgenden verbleibenden TPM-Initialisierungsaktionen bei Bedarf transparent aus:

- Endorsement Key-Paar erstellen  
- Besitzerauthentifizierungswert erstellen und in Active Directory hinterlegen, welches zur Unterstützung dieses Werts erweitert worden sein muss  
- Besitz übernehmen  
- Storage Root Key (SRK, Speicherstammschlüssel) erstellen bzw. zurücksetzen, falls bereits einer vorhanden ist, der jedoch inkompatibel ist  

Wenn die Tasksequenz auf den Schritt **BitLocker aktivieren** warten soll, bevor der Vorgang der Laufwerkverschlüsselung abgeschlossen wird, aktivieren Sie die Option **Warten**. Wenn Sie die Option **Warten** nicht auswählen, wird die Laufwerkverschlüsselung im Hintergrund ausgeführt. Die Tasksequenz fährt sofort mit dem nächsten Schritt fort.  

Mit BitLocker können Sie mehrere Laufwerke in einem Computersystem verschlüsseln. Dies gilt für Datenlaufwerke sowie für das Betriebssystem. Um ein Datenlaufwerk zu verschlüsseln, verschlüsseln Sie zunächst das Betriebssystemlaufwerk, und schließen Sie den Verschlüsselungsvorgang ab. Diese Anforderung ist darauf zurückzuführen, dass das Betriebssystemlaufwerk die Schlüsselschutzvorrichtungen für die Datenlaufwerke speichert. Wenn Sie das Betriebssystem und die Datenlaufwerke in derselben Tasksequenz verschlüsseln, aktivieren Sie in Schritt **BitLocker aktivieren** die Option **Warten** für das Betriebssystemlaufwerk.  

Wenn die Festplatte bereits verschlüsselt, aber BitLocker deaktiviert ist, aktiviert der Schritt **BitLocker aktivieren** die Schlüsselschutzvorrichtungen erneut und wird schnell abgeschlossen. Eine erneute Verschlüsselung der Festplatte ist in diesem Fall nicht erforderlich.  

### <a name="variables-for-enable-bitlocker"></a>Variablen für „BitLocker aktivieren“

Verwenden Sie die folgenden Tasksequenzvariablen in diesem Schritt:  

- [OSDBitLockerPIN](task-sequence-variables.md#OSDBitLockerPIN)
- [OSDBitLockerRecoveryPassword](task-sequence-variables.md#OSDBitLockerRecoveryPassword)
- [OSDBitLockerStartupKey](task-sequence-variables.md#OSDBitLockerStartupKey)

### <a name="cmdlets-for-enable-bitlocker"></a>Cmdlets für „BitLocker aktivieren“

Verwalten Sie diesen Schritt mit den folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepEnableBitLocker](/powershell/module/configurationmanager/Get-CMTSStepEnableBitLocker)
- [New-CMTSStepEnableBitLocker](/powershell/module/configurationmanager/New-CMTSStepEnableBitLocker)
- [Remove-CMTSStepEnableBitLocker](/powershell/module/configurationmanager/Remove-CMTSStepEnableBitLocker)
- [Set-CMTSStepEnableBitLocker](/powershell/module/configurationmanager/Set-CMTSStepEnableBitLocker)

### <a name="properties-for-enable-bitlocker"></a>Eigenschaften für „BitLocker aktivieren“

Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

#### <a name="choose-the-drive-to-encrypt"></a>Wählen Sie das zu verschlüsselnde Laufwerk aus.

Gibt das zu verschlüsselnde Laufwerk an. Um das aktuelle Betriebssystemlaufwerk zu verschlüsseln, wählen Sie **Aktuelles Betriebssystemlaufwerk** aus. Konfigurieren Sie dann ein der folgenden Optionen für die Schlüsselverwaltung:  

- **Nur TPM**: Wählen Sie diese Option aus, um nur das Trusted Platform Module (TPM) zu verwenden.  

- **Nur Schlüssel zum Systemstart auf USB**: Wählen Sie diese Option aus, um einen auf einem USB-Flashlaufwerk gespeicherten Systemstartschlüssel zu verwenden. Wenn Sie diese Option auswählen, sperrt BitLocker den normalen Startvorgang, bis ein USB-Gerät mit einem BitLocker-Systemstartschlüssel an den Computer angeschlossen wird.  

- **TPM & Schlüssel zum Systemstart auf USB**: Wählen Sie diese Option aus, um das TPM und einen auf einem USB-Flashlaufwerk gespeicherten Systemstartschlüssel zu verwenden. Wenn Sie diese Option auswählen, sperrt BitLocker den normalen Startvorgang, bis ein USB-Gerät mit einem BitLocker-Systemstartschlüssel an den Computer angeschlossen wird.  

- **TPM-und-PIN**: Wählen Sie diese Option aus, um das TPM und eine persönliche Identifikationsnummer (PIN) zu verwenden. Wenn Sie diese Option auswählen, sperrt BitLocker den normalen Startvorgang, bis der Benutzer die PIN eingibt.  

Um ein bestimmtes Datenlaufwerk zu verschlüsseln, das kein Betriebssystem enthält, wählen Sie **Bestimmtes Laufwerk** aus. Wählen Sie dann das Laufwerk aus der Liste aus.  

#### <a name="disk-encryption-mode"></a>Datenträgerverschlüsselungsmodus

<!--6995601-->
Ab Version 2006 können Sie einen der folgenden Verschlüsselungsalgorithmen auswählen:

- AES_128
- AES_256
- XTS_AES256
- XTS_AES128

Standardmäßig oder bei nicht erfolgter Festlegung verwendet der Schritt weiterhin die Standardverschlüsselungsmethode für die Betriebssystemversion. Wenn der Schritt für eine Version von Windows ausgeführt wird, die den angegebenen Algorithmus nicht unterstützt, wird auf den Standardwert des Betriebssystems zurückgegriffen. Unter diesen Umständen sendet die Tasksequenz-Engine die Statusmeldung 11911.

#### <a name="use-full-disk-encryption"></a>Vollständige Datenträgerverschlüsselung verwenden

<!--SCCMDocs-pr issue 2671-->
Standardmäßig verschlüsselt dieser Schritt nur belegten Speicherplatz auf dem Laufwerk. Dieses Standardverhalten wird aufgrund der Schnelligkeit und Effizienz empfohlen. Aktivieren Sie diese Option, wenn Ihre Organisation während des Setups das gesamte Laufwerk verschlüsseln muss. Windows Setup wartet, bis das gesamte Laufwerk verschlüsselt wurde. Dieser Vorgang kann viel Zeit in Anspruch nehmen, insbesondere auf großen Laufwerken.

> [!TIP]
> Ab Version 1910 können Sie BitLocker-Verwaltungsrichtlinien erstellen und bereitstellen, in denen die *vollständige Datenträgerverschlüsselung* vorgesehen ist. Aktivieren Sie diese Option, um BitLocker auf Geräten zu verwalten, nachdem die Tasksequenz das Betriebssystem bereitgestellt hat. Weitere Informationen finden Sie unter [Planen der BitLocker-Verwaltung](../../protect/plan-design/bitlocker-management.md).

#### <a name="choose-where-to-create-the-recovery-key"></a>Wählen Sie aus, wo der Wiederherstellungsschlüssel erstellt werden soll

Um festzulegen, dass BitLocker das Wiederherstellungskennwort erstellt und in Active Directory hinterlegt, wählen Sie **In Active Directory** aus. Diese Option erfordert, dass Sie Active Directory für BitLocker-Schlüsselhinterlegung erweitern. BitLocker kann die zugehörigen Wiederherstellungsinformationen dann in Active Directory speichern. Wählen Sie **Do not create recovery key** (Keinen Wiederherstellungsschlüssel erstellen) aus, um kein Kennwort zu erstellen. Es wird empfohlen, ein Kennwort zu erstellen.  

#### <a name="wait-for-bitlocker-to-complete-the-drive-encryption-process-on-all-drives-before-continuing-task-sequence-execution"></a>Vor dem Fortsetzen der Tasksequenzausführung warten, bis BitLocker den Laufwerkverschlüsselungsvorgang auf allen Laufwerken abgeschlossen hat

Wählen Sie diese Option aus, damit die BitLocker-Laufwerkverschlüsselung abgeschlossen wird, bevor der nächste Schritt in der Tasksequenz ausgeführt wird. Wenn Sie diese Option auswählen, verschlüsselt BitLocker das gesamte Datenträgervolume, bevor der Benutzer sich auf dem Computer anmelden kann.  

Beim Verschlüsseln einer großen Festplatte kann der Verschlüsselungsvorgang mehrere Stunden andauern. Wenn diese Option nicht ausgewählt wird, kann die Tasksequenz sofort fortgesetzt werden.  

#### <a name="skip-this-step-for-computers-that-do-not-have-a-tpm-or-when-tpm-is-not-enabled"></a>Überspringen Sie diesen Schritt für Computer, die nicht über TPM verfügen, oder wenn TPM nicht aktiviert ist.

<!--6995601-->
Ab Version 2006 können Sie diese Option auswählen, um die Laufwerkverschlüsselung auf einem Computer zu überspringen, der kein unterstütztes oder aktiviertes TPM enthält. Verwenden Sie diese Option beispielsweise, um ein Betriebssystem auf einer VM bereitzustellen. Diese Einstellung ist für den Schritt **BitLocker aktivieren** standardmäßig deaktiviert. Wenn Sie diese Einstellung aktivieren und das Gerät nicht über ein funktionierendes TPM verfügt, protokolliert die Tasksequenz-Engine einen Fehler in „smsts.log“ und sendet die Statusmeldung 11912. Die Tasksequenz wird über diesen Schritt hinaus fortgesetzt.


## <a name="format-and-partition-disk"></a><a name="BKMK_FormatandPartitionDisk"></a> Datenträger formatieren und partitionieren

Mit diesem Schritt können Sie einen angegebenen Datenträger auf einem Zielcomputer formatieren und partitionieren.  

> [!IMPORTANT]  
> Jede Einstellung, die Sie für diesen Schritt festlegen, gilt für einen einzelnen angegebenen Datenträger. Wenn Sie einen anderen Datenträger auf dem Zielcomputer formatieren und partitionieren möchten, fügen Sie der Tasksequenz den zusätzlichen Schritt **Datenträger formatieren und partitionieren** hinzu.  

Dieser Schritt wird nur in Windows PE ausgeführt. Er kann nicht in der Vollversion des Betriebssystems ausgeführt werden.  

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Datenträger** und dann **Datenträger formatieren und partitionieren** aus.

### <a name="variables-for-format-and-partition-disk"></a>Variablen für „Datenträger formatieren und partitionieren“

Verwenden Sie die folgenden Tasksequenzvariablen in diesem Schritt:  

- [OSDDiskIndex](task-sequence-variables.md#OSDDiskIndex)  
- [OSDGPTBootDisk](task-sequence-variables.md#OSDGPTBootDisk)  
- [OSDPartitions](task-sequence-variables.md#OSDPartitions)  
- [OSDPartitionStyle](task-sequence-variables.md#OSDPartitionStyle)  

### <a name="cmdlets-for-format-and-partition-disk"></a>Cmdlets für „Datenträger formatieren und partitionieren“

Verwalten Sie diesen Schritt mit den folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPartitionDisk](/powershell/module/configurationmanager/get-cmtssteppartitiondisk)
- [New-CMTSStepPartitionDisk](/powershell/module/configurationmanager/new-cmtssteppartitiondisk)
- [Remove-CMTSStepPartitionDisk](/powershell/module/configurationmanager/remove-cmtssteppartitiondisk)
- [Set-CMTSStepPartitionDisk](/powershell/module/configurationmanager/set-cmtssteppartitiondisk)

### <a name="properties-for-format-and-partition-disk"></a>Eigenschaften für „Datenträger formatieren und partitionieren“

Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

#### <a name="disk-number"></a>Datenträgernummer

Die Nummer des physischen Datenträgers, der formatiert werden soll Die Nummer basiert auf der Reihenfolge der Datenträgerenumeration in Windows.  

#### <a name="variable-name-to-store-disk-number"></a>Variablenname zum Speichern der Datenträgernummer

<!--6610288-->

Ab Version 2006 können Sie eine Tasksequenzvariable verwenden, um den zu formatierenden Zieldatenträger anzugeben. Diese Variablenoption unterstützt komplexere Tasksequenzen mit dynamischem Verhalten. Beispielsweise kann ein benutzerdefiniertes Skript den Datenträger erkennen und die Variable auf Grundlage des Hardwaretyps festlegen. Anschließend können Sie mehrere Instanzen dieses Schritts verwenden, um verschiedene Hardwaretypen und Partitionen zu konfigurieren.

Wenn Sie diese Eigenschaft auswählen, geben Sie einen benutzerdefinierten Variablennamen ein. Fügen Sie einen früheren Schritt in der Tasksequenz hinzu, um den Wert dieser benutzerdefinierten Variablen auf einen ganzzahligen Wert für den physischen Datenträger festzulegen.

Die folgenden Schritte zeigen ein Beispiel:

- **PowerShell-Skript ausführen**: benutzerdefiniertes Skript zum Sammeln von Zieldatenträgern
  - Legt `myOSDisk` auf `1` fest.
  - Legt `myDataDisk` auf `2` fest.

- **Datenträger formatieren und partitionieren** für Betriebssystemdatenträger: gibt die `myOSDisk`-Variable an
  - Konfiguriert Datenträger 1 als Systemdatenträger.

- **Datenträger formatieren und partitionieren** für Datenträger: gibt die `myDataDisk`-Variable an
  - Konfiguriert Datenträger 2 für unformatierten Speicher.

Bei einer Variante dieses Beispiels werden Datenträgernummern und Partitionierungspläne für unterschiedliche Hardwaretypen verwendet.

> [!NOTE]
> Sie können weiterhin die vorhandene Tasksequenzvariable **OSDDiskIndex** verwenden. Allerdings wird für jede Instanz des Schritts **Datenträger formatieren und partitionieren** derselbe Indexwert verwendet. Wenn Sie die Datenträgernummer für mehrere Instanzen dieses Schritts programmgesteuert festlegen möchten, verwenden Sie diese Variableneigenschaft.

#### <a name="disk-type"></a>Datenträgertyp

Dies ist der Typ des zu formatierenden Datenträgers. In der Dropdownliste stehen zwei Optionen zur Auswahl zur Verfügung:

- **Standard (MBR)** : Master Boot Record  
- **GPT**: GUID-Partitionstabelle  

> [!NOTE]  
> Wenn Sie den Datenträgertyp von **Standard (MBR)** in **GPT** ändern und das Partitionslayout eine erweiterte Partition enthält, entfernt die Tasksequenz alle erweiterten und logischen Partitionen aus dem Layout. Der Tasksequenz-Editor fordert Sie dazu auf, diese Aktion vor dem Ändern des Datenträgertyps zu bestätigen.  

#### <a name="volume"></a>Volume

Weitere Informationen zu der Partition oder dem Volume, die bzw. das von der Tasksequenz erstellt wird, einschließlich folgender Attribute:  

- Name  
- Verbleibender Speicherplatz  

Zum Erstellen einer neuen Partition wählen Sie **Neu** aus, um das Dialogfeld **Partitionseigenschaften** aufzurufen. Geben Sie die Größe sowie den Typ der Partition an und ob es sich um eine Startpartition handelt. Um eine vorhandene Partition zu ändern, wählen Sie die zu ändernde Partition und dann die Schaltfläche **Eigenschaften** aus. Weitere Informationen zum Konfigurieren von Festplattenpartitionen finden Sie in einem der folgenden Artikel:  

- [UEFI-/GPT-basierte Festplattenpartitionen](/windows-hardware/manufacture/desktop/configure-uefigpt-based-hard-drive-partitions)  
- [BIOS-/MBR-basierte Festplattenpartitionen](/windows-hardware/manufacture/desktop/configure-biosmbr-based-hard-drive-partitions)  

Um eine Partition zu löschen, wählen Sie die zu löschende Partition und dann **Löschen** aus.  



## <a name="install-application"></a><a name="BKMK_InstallApplication"></a> Anwendung installieren

Dieser Schritt installiert die angegebenen Anwendungen oder eine von einer dynamischen Liste mit Tasksequenzvariablen definierte Anwendungsgruppe. Wenn die Tasksequenz diesen Schritt ausführt, beginnt die Anwendungsinstallation sofort. d.h. das nächste Richtlinienabrufintervall wird nicht abgewartet.  

Die Anwendung muss folgende Kriterien erfüllen:  

- Ihr Bereitstellungstyp muss **Windows Installer** oder **Skript** sein. Bereitstellungstypen des Windows-App-Pakets (APPX-Datei) werden nicht unterstützt.  

- Sie muss unter dem lokalen Systemkonto ausgeführt werden – nicht unter dem Benutzerkonto.  

- Es darf keine Interaktion mit dem Desktop erfolgen. Das Programm muss im Hintergrund oder in einem unbeaufsichtigten Modus ausgeführt werden.  

- Es darf durch die Anwendung kein eigenständiger Computerneustart initiiert werden. Sie muss einen Computerneustart über den Standardneustartcode 3010 anfordern. Dieses Verhalten stellt sicher, dass dieser Schritt den Neustart korrekt verarbeitet. Wenn die Anwendung einen Exitcode 3010 zurückgibt, startet die Tasksequenz-Engine den Computer neu. Nach dem Neustart wird die Tasksequenz automatisch fortgesetzt.  

> [!Note]
> Wenn die Anwendung [auf ausgeführte ausführbare Dateien prüft](../../apps/deploy-use/deploy-applications.md#bkmk_exe-check), kann sie nicht von der Tasksequenz installiert werden. Wenn Sie diesen Schritt nicht so konfigurieren, dass er auch bei einem Fehler fortgesetzt wird, schlägt die gesamte Tasksequenz fehl.

Wenn dieser Schritt ausgeführt wird, überprüft die Anwendung die Anwendbarkeit der Anforderungsregeln und der Erkennungsmethode für die Bereitstellungstypen. Auf Basis der Ergebnisse dieser Überprüfung wird der anwendbare Bereitstellungstyp installiert. Wenn ein Bereitstellungstyp Abhängigkeiten enthält, wird der abhängige Bereitstellungstyp im Rahmen dieses Schritts ausgewertet und installiert. Abhängigkeiten von Anwendungen werden für eigenständige Medien nicht unterstützt.  

> [!NOTE]  
> Zum Installieren einer Anwendung, die eine andere Anwendung ablöst, müssen die Inhaltsdateien für die abgelöste Anwendung verfügbar sein. Andernfalls tritt beim Tasksequenzschritt ein Fehler auf. Beispiel: Microsoft Visio 2010 ist auf einem Client oder in einem erfassten Abbild installiert. Wenn der Schritt **Anwendung installieren** Microsoft Visio 2013 installiert, müssen die Inhaltsdateien für Microsoft Visio 2010 (die abgelöste Anwendung) an einem Verteilungspunkt verfügbar sein. Wenn Microsoft Visio auf einem Client oder einem erfassten Image nicht installiert ist, installiert die Tasksequenz Microsoft Visio 2013, ohne nach den Inhaltsdateien von Microsoft Visio 2010 zu suchen.  
>
> Wenn Sie eine abgelöste Anwendung außer Betrieb nehmen und in einer Tasksequenz auf die neue Anwendung verwiesen wird, kann die Tasksequenz nicht gestartet werden.
Dieses Verhalten ist beabsichtigt, denn die Tasksequenz benötigt alle App-Verweise.<!-- SCCMDocs 1711 -->  

Dieser Tasksequenzschritt wird nur in der Vollversion des Betriebssystems ausgeführt. Er kann nicht in Windows PE ausgeführt werden.  

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Software** und dann **Anwendung installieren** aus.

### <a name="variables-for-install-application"></a>Variablen für „Anwendung installieren“

Verwenden Sie die folgenden Tasksequenzvariablen in diesem Schritt:  

- [_TSAppInstallStatus](task-sequence-variables.md#TSAppInstallStatus)  
- [SMSTSMPListRequestTimeoutEnabled](task-sequence-variables.md#SMSTSMPListRequestTimeoutEnabled)  
- [SMSTSMPListRequestTimeout](task-sequence-variables.md#SMSTSMPListRequestTimeout)  
- [TSErrorOnWarning](task-sequence-variables.md#TSErrorOnWarning)  

> [!NOTE]  
> Wenn der Client die Verwaltungspunktliste nicht aus den Ortungsdiensten abrufen kann, verwenden Sie die Tasksequenzvariablen **SMSTSMPListRequestTimeoutEnabled** und **SMSTSMPListRequestTimeout**. Diese Variablen geben an, wie viele Millisekunden eine Tasksequenz wartet, bevor sie erneut versucht, eine Anwendung zu installieren. Weitere Informationen finden Sie unter [Tasksequenzvariablen](task-sequence-variables.md).

### <a name="cmdlets-for-install-application"></a>Cmdlets für „Anwendung installieren“

Verwalten Sie diesen Schritt mit den folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepInstallApplication](/powershell/module/configurationmanager/get-cmtsstepinstallapplication)
- [New-CMTSStepInstallApplication](/powershell/module/configurationmanager/new-cmtsstepinstallapplication)
- [Remove-CMTSStepInstallApplication](/powershell/module/configurationmanager/remove-cmtsstepinstallapplication)
- [Set-CMTSStepInstallApplication](/powershell/module/configurationmanager/set-cmtsstepinstallapplication)

### <a name="properties-for-install-application"></a>Eigenschaften für „Anwendung installieren“

Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

#### <a name="install-the-following-applications"></a>Folgende Anwendungen installieren

Die Tasksequenz installiert diese Anwendungen in der angegebenen Reihenfolge.  

Deaktivierte Anwendungen und Anwendungen mit den folgenden Einstellungen werden von Configuration Manager herausgefiltert:  

- Nur wenn ein Benutzer angemeldet ist  
- Mit Benutzerrechten ausführen  

Diese Anwendungen werden nicht im Dialogfeld **Zu installierende Anwendung auswählen** angezeigt.

#### <a name="install-applications-according-to-dynamic-variable-list"></a>Anwendungen entsprechend der dynamischen Variablenliste installieren

Die Tasksequenz installiert Anwendungen mithilfe dieses Basisvariablennamens. Der Basisvariablenname gilt für eine Gruppe von Tasksequenzvariablen, die für eine Sammlung oder für einen Computer definiert wurden. Von diesen Variablen werden die Anwendungen angegeben, die von der Tasksequenz für die Sammlung bzw. für den Computer installiert werden. Jeder Variablenname besteht aus einem allgemeinen Basisnamen sowie einem numerischen bei 01 beginnenden Suffix Der Wert jeder Variable darf nur den Namen der Anwendung und nichts anderes enthalten.  

Damit die Tasksequenz Anwendungen mithilfe einer dynamischen Variablenliste installiert, aktivieren Sie die folgende Einstellung auf der Registerkarte **Allgemein** in den **Eigenschaften** der Anwendung: **Installation dieser Anwendung durch die Tasksequenzaktion „Anwendung installieren“ statt durch manuelle Bereitstellung zulassen**.  

> [!NOTE]  
> Sie können Anwendungen nicht mithilfe einer dynamischen Variablenliste für eigenständige Medienbereitstellungen installieren.  

Um z.B. eine einzelne Anwendung mit einer Tasksequenzvariablen namens AA01 zu installieren, geben Sie die folgende Variable an:  

|Variablenname|Variablenwert|  
|-------------------|--------------------|  
|AA01|Microsoft Office|  

Um zwei Anwendungen zu installieren, geben Sie die folgenden Variablen an:  

|Variablenname|Variablenwert|  
|-------------------|--------------------|  
|AA01|Microsoft Lync|  
|AA02|Microsoft Office|  

Folgende Bedingungen wirken sich auf die Anwendungen aus, die von der Tasksequenz installiert wurden:  

- Der Variablenwert enthält noch andere bzw. keine anderen Informationen als den Namen der Anwendung. Die Tasksequenz installiert die Anwendung nicht und wird fortgesetzt.  

- Wenn die Tasksequenz keine Variable mit dem angegebenen Basisnamen und dem Suffix „01“ findet, installiert sie keine Anwendungen.  

> [!Important]  
> Die Werte werden nach Groß-/Kleinschreibung unterschieden. Beispielsweise unterscheidet sich „install“ von „Install“. Wenn Sie den Wert ändern müssen, wird eine Änderung der Groß-/Kleinschreibung vom Tasksequenz-Editor nicht erkannt. Nehmen Sie gleichzeitig eine weitere Bearbeitung vor, ändern Sie z. B. die Beschreibung der Schritte.<!--509714-->

#### <a name="if-an-application-fails-continue-installing-other-applications-in-the-list"></a>Wenn ein Fehler bei einer Anwendungsinstallation auftritt, mit anderen Anwendungen in der Liste fortfahren

Mit dieser Einstellung geben Sie an, dass der Schritt fortgesetzt werden soll, wenn bei einer einzelnen Anwendungsinstallation ein Fehler auftritt. Wenn Sie diese Einstellungen angeben, wird die Tasksequenz unabhängig von Installationsfehlern fortgesetzt. Wenn Sie diese Einstellung nicht angeben und die Installation fehlschlägt, wird der Schritt sofort beendet.  

#### <a name="clear-application-content-from-cache-after-installing"></a>Anwendungsinhalt nach der Installation aus dem Cache löschen

<!--4485675-->
Ab Version 1906 müssen Sie den App-Inhalt aus dem Clientcache löschen, nachdem der Schritt ausgeführt wurde. Dieses Verhalten ist auf Geräten mit kleinen Festplattenlaufwerken nützlich, oder wenn viele umfangreiche Apps nacheinander installiert werden.


### <a name="options-for-install-application"></a>Optionen für „Anwendung installieren“

> [!NOTE]  
> Wenn Sie auf der Registerkarte **Optionen** dieses Schritts die Option **Bei Fehler fortsetzen** auswählen, wird die Tasksequenz bei einem Fehler der Anwendungsinstallation fortgesetzt. Wenn Sie diese Option nicht aktivieren, tritt bei der Tasksequenz ein Fehler auf, und verbleibende Anwendungen werden nicht installiert.  

Konfigurieren Sie neben den Standardoptionen auch folgende zusätzliche Einstellungen auf der Registerkarte **Optionen** dieses Tasksequenzschritts:  

#### <a name="retry-this-step-if-computer-unexpectedly-restarts"></a>Führen Sie diesen Schritt erneut aus, wenn der Computer unerwartet neu gestartet wird

Wenn eine der Anwendungsinstallationen den Computer unerwartet neu startet, wiederholen Sie diesen Schritt. Der Schritt aktiviert diese Einstellung standardmäßig mit zwei Wiederholungen. Sie können eine bis fünf Wiederholungen angeben.  



## <a name="install-package"></a><a name="BKMK_InstallPackage"></a> Paket installieren

Verwenden Sie diesen Schritt, um ein Softwarepaket als Teil der Tasksequenz zu installieren. Wenn dieser Schritt ausgeführt wird, beginnt die Installation sofort, d.h. das nächste Richtlinienabrufintervall wird nicht abgewartet.  

Das Paket muss folgende Kriterien erfüllen:  

- Es muss unter dem lokalen Systemkonto ausgeführt werden – nicht unter einem Benutzerkonto.  

- Es darf nicht mit dem Desktop interagieren. Das Programm muss im Hintergrund oder in einem unbeaufsichtigten Modus ausgeführt werden.  

- Es darf durch die Anwendung kein eigenständiger Computerneustart initiiert werden. Die Software muss einen Neustart über den Standardneustartcode 3010 anfordern. Dieses Verhalten stellt sicher, dass die Tasksequenz den Neustart ordnungsgemäß verarbeitet. Wenn die Software einen Exitcode 3010 zurückgibt, startet die Tasksequenz-Engine den Computer neu. Nach dem Neustart wird die Tasksequenz automatisch fortgesetzt.  

Programme, die die Option **Ein anderes Programm zuerst ausführen** zur Installation eines abhängigen Programms verwenden, werden beim Bereitstellen eines Betriebssystems nicht unterstützt. Wenn Sie die Paketoption **Ein anderes Programm zuerst ausführen** aktivieren und das abhängige Programm bereits auf dem Zielcomputer ausgeführt wurde, wird dieses ausgeführt und die Tasksequenz wird fortgesetzt. Wenn das abhängige Programm jedoch noch nicht auf dem Zielcomputer ausgeführt wurde, schlägt der Tasksequenzschritt fehl.  

> [!NOTE]  
> Dem Standort der zentralen Verwaltung fehlen die erforderlichen Clientkonfigurationsrichtlinien, um den Softwareverteilungs-Agent während der Tasksequenz zu aktivieren. Wenn Sie am Standort der zentralen Verwaltung eigenständige Medien für eine Tasksequenz erstellen und die Tasksequenz den Schritt **Paket installieren** enthält, kann in der Datei "CreateTsMedia.log" der folgende Fehler enthalten sein:  
>
> `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`  
>
> Bei eigenständigen Medien, die den Schritt **Paket installieren** enthalten, erstellen Sie das eigenständige Medium an einem primären Standort, bei dem der Softwareverteilungs-Agent aktiviert ist. Fügen Sie alternativ den Schritt **Befehlszeile ausführen** nach dem Schritt **Windows und ConfigMgr einrichten** und vor dem ersten **Paket installieren**-Schritt hinzu. Im Schritt **Befehlszeile ausführen** wird ein WMIC-Befehl ausgeführt, um den Softwareverteilungs-Agent vor dem ersten Schritt **Paket installieren** zu aktivieren. Verwenden Sie im Schritt **Befehlszeile ausführen** folgenden Befehl:  
>
> `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`  
>
> Weitere Informationen zum Erstellen eigenständiger Medien finden Sie unter [Erstellen eigenständiger Medien](../deploy-use/create-stand-alone-media.md).  

Dieser Tasksequenzschritt wird nur in der Vollversion des Betriebssystems ausgeführt. Er kann nicht in Windows PE ausgeführt werden.  

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Software** und dann **Paket installieren** aus.

### <a name="variables-for-install-package"></a>Variablen für „Paket installieren“

Verwenden Sie die folgenden Tasksequenzvariablen in diesem Schritt:  

- [OSDDoNotLogCommand](task-sequence-variables.md#OSDDoNotLogCommand) <!--1358493-->  

### <a name="cmdlets-for-install-package"></a>Cmdlets für „Paket installieren“

Verwalten Sie diesen Schritt mit den folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepInstallSoftware](/powershell/module/configurationmanager/get-cmtsstepinstallsoftware)
- [New-CMTSStepInstallSoftware](/powershell/module/configurationmanager/new-cmtsstepinstallsoftware)
- [Remove-CMTSStepInstallSoftware](/powershell/module/configurationmanager/remove-cmtsstepinstallsoftware)
- [Set-CMTSStepInstallSoftware](/powershell/module/configurationmanager/set-cmtsstepinstallsoftware)

> [!TIP]
> Verwenden Sie ein vorgeschaltetes Zwischenspeichern für Inhalte, um ein geeignetes Betriebssystemupgradepaket herunterzuladen, bevor ein Benutzer die Tasksequenz installiert. Weitere Informationen finden Sie unter [Konfigurieren des zwischengespeicherten Inhalts](../deploy-use/configure-precache-content.md).

### <a name="properties-for-install-package"></a>Eigenschaften für „Paket installieren“

Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

#### <a name="install-a-single-software-package"></a>Einzelnes Softwarepaket installieren

Diese Einstellung gibt ein Configuration Manager-Softwarepaket an. Bei diesem Schritt wird gewartet, bis die Installation abgeschlossen ist.  

#### <a name="install-software-packages-according-to-dynamic-variable-list"></a>Softwarepakete entsprechend der dynamischen Variablenliste installieren

Die Tasksequenz installiert Pakete mithilfe dieses Basisvariablennamens. Der Basisvariablenname gilt für eine Gruppe von Tasksequenzvariablen, die für eine Sammlung oder für einen Computer definiert wurden. Von diesen Variablen werden die Pakete angegeben, die von der Tasksequenz für die Sammlung bzw. für den Computer installiert werden. Jeder Variablenname besteht aus einem allgemeinen Basisnamen sowie einem numerischen bei 001 beginnenden Suffix. Der Wert jeder Variablen muss eine Paket-ID und den Namen der Software (durch einen Doppelpunkt getrennt) enthalten.  

Damit die Tasksequenz Software mithilfe einer dynamischen Variablenliste installiert, aktivieren Sie die folgende Einstellung auf der Registerkarte **Erweitert** in den **Eigenschaften** des Pakets: **Installation dieses Programms aus der Tasksequenz „Paket installieren“ ohne Bereitstellung zulassen**.  

> [!NOTE]  
> Sie können Softwarepakete nicht mithilfe einer dynamischen Variablenliste für eigenständige Medienbereitstellungen installieren.  

Beispiel: Geben Sie folgende Variable an, um ein einzelnes Softwarepaket mithilfe einer Tasksequenzvariablen namens AA001 zu installieren:  

|Variablenname|Variablenwert|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  

Bei der Installation von drei Softwarepaketen sind folgende zusätzliche Variablen anzugeben:  

|Variablenname|Variablenwert|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  
|AA002|CEN00107:Install Silent|  
|AA003|CEN00031:Install|  

Folgende Bedingungen wirken sich auf die Pakete aus, die von der Tasksequenz installiert wurden:  

- Wenn Sie den Wert einer Variablen nicht im richtigen Format erstellen oder dieser keine gültige Paket-ID und keinen gültigen Namen angibt, schlägt die Softwareinstallation fehl.  

- Wenn die Paket-ID Kleinbuchstaben enthält, schlägt die Installation der Software fehl.  

- Wenn die Tasksequenz keine Variable mit dem angegebenen Basisnamen und dem Suffix „001“ findet, installiert sie keine Pakete. Die Tasksequenz wird fortgesetzt.  

> [!Important]  
> Die Werte werden nach Groß-/Kleinschreibung unterschieden. Beispielsweise unterscheidet sich „install“ von „Install“. Wenn Sie den Wert ändern müssen, wird eine Änderung der Groß-/Kleinschreibung vom Tasksequenz-Editor nicht erkannt. Nehmen Sie gleichzeitig eine weitere Bearbeitung vor, ändern Sie z. B. die Beschreibung der Schritte.<!--509714-->

#### <a name="if-installation-of-a-software-package-fails-continue-installing-other-packages-in-the-list"></a>Wenn ein Fehler bei einer Softwarepaketinstallation auftritt, mit anderen Paketen in der Liste fortfahren

Mit dieser Einstellung geben Sie an, dass der Schritt fortgesetzt werden soll, wenn bei einer einzelnen Softwarepaketinstallation ein Fehler auftritt. Wenn Sie diese Einstellungen angeben, wird die Tasksequenz unabhängig von Installationsfehlern fortgesetzt. Wenn Sie diese Einstellung nicht angeben und die Installation fehlschlägt, wird der Schritt sofort beendet.  



## <a name="install-software-updates"></a><a name="BKMK_InstallSoftwareUpdates"></a> Softwareupdates installieren

Verwenden Sie diesen Schritt, um Softwareupdates auf dem Zielcomputer zu installieren. Der Zielcomputer wird erst dann auf geeignete Softwareupdates überprüft, wenn dieser Tasksequenzschritt ausgeführt wird. An diesem Punkt wird der Zielcomputer wie jeder andere Configuration Manager-Client hinsichtlich Softwareupdates ausgewertet. Damit in diesem Schritt Softwareupdates installiert werden können, stellen Sie zuerst die Updates für eine Sammlung bereit, der der Zielcomputer angehört.  

> [!IMPORTANT]  
> Um die beste Leistung zu erzielen, installieren Sie die neueste Version des Windows Update-Agents.  

Dieser Tasksequenzschritt wird nur in der Vollversion des Betriebssystems ausgeführt. Er kann nicht in Windows PE ausgeführt werden.

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Software** und dann **Softwareupdates installieren** aus.

### <a name="variables-for-install-software-updates"></a>Variablen für „Softwareupdates installieren“

Verwenden Sie die folgenden Tasksequenzvariablen in diesem Schritt:  

- [SMSInstallUpdateTarget](task-sequence-variables.md#SMSInstallUpdateTarget)  
- [SMSTSMPListRequestTimeoutEnabled](task-sequence-variables.md#SMSTSMPListRequestTimeoutEnabled)  
- [SMSTSMPListRequestTimeout](task-sequence-variables.md#SMSTSMPListRequestTimeout)  
- [SMSTSSoftwareUpdateScanTimeout](task-sequence-variables.md#SMSTSSoftwareUpdateScanTimeout)  
- [SMSTSWaitForSecondReboot](task-sequence-variables.md#SMSTSWaitForSecondReboot)  

> [!NOTE]  
> Wenn der Client die Verwaltungspunktliste nicht aus den Ortungsdiensten abrufen kann, verwenden Sie die Variablen **SMSTSMPListRequestTimeoutEnabled** und **SMSTSMPListRequestTimeout**. Diese Variablen geben an, wie viele Millisekunden eine Tasksequenz wartet, bevor sie erneut versucht, eine Anwendung oder ein Softwareupdate zu installieren. Weitere Informationen finden Sie unter [Tasksequenzvariablen](task-sequence-variables.md).  

### <a name="cmdlets-for-install-software-updates"></a>Cmdlets für „Softwareupdates installieren“

Verwalten Sie diesen Schritt mit den folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepInstallUpdate](/powershell/module/configurationmanager/get-cmtsstepinstallupdate)
- [New-CMTSStepInstallUpdate](/powershell/module/configurationmanager/new-cmtsstepinstallupdate)
- [Remove-CMTSStepInstallUpdate](/powershell/module/configurationmanager/remove-cmtsstepinstallupdate)
- [Set-CMTSStepInstallUpdate](/powershell/module/configurationmanager/set-cmtsstepinstallupdate)

Weitere Empfehlungen und ein technisches Flussdiagramm für diesen Schritt finden Sie unter [Softwareupdates installieren](install-software-updates.md).

### <a name="properties-for-install-software-updates"></a>Eigenschaften für „Softwareupdates installieren“

Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

#### <a name="required-for-installation---mandatory-software-updates-only"></a>Erforderlich für die Installation – Nur obligatorische Softwareupdates

Wählen Sie diese Option aus, um alle erforderlichen Softwareupdates mit einem vom Administrator definierten Installationsstichtag zu installieren.  

#### <a name="available-for-installation---all-software-updates"></a>Verfügbar zur Installation – Alle Softwareupdates

Wählen Sie diese Option aus, um alle verfügbaren Softwareupdates zu installieren. Stellen Sie zuerst diese Updates für eine Sammlung bereit, der der Computer angehört. Die Tasksequenz installiert alle verfügbaren Softwareupdates auf den Zielcomputern.  

#### <a name="evaluate-software-updates-from-cached-scan-results"></a>Bewerten von Softwareupdates aus zwischengespeicherten Überprüfungsergebnissen

Standardmäßig verwendet dieser Schritt zwischengespeicherte Überprüfungsergebnisse des Windows Update-Agents. Deaktivieren Sie diese Option, damit der Windows Update-Agent den aktuellen Katalog vom Softwareupdatepunkt herunterlädt. Aktivieren Sie diese Option, wenn Sie eine Tasksequenz verwenden, um ein [Betriebssystemimage zu erfassen und zu erstellen](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md). In diesem Szenario sind zahlreiche Softwareupdates zu erwarten.

Viele dieser Updates weisen Abhängigkeiten auf. Ein Beispiel: Update ABC muss installiert werden, bevor Update XYZ angewendet werden kann. Wenn Sie diese Einstellung deaktivieren und die Tasksequenz für viele Clients bereitstellen, werden alle zur selben Zeit mit dem Softwareupdatepunkt verbunden. Dieses Verhalten kann beim Prozess und Download des Updatekatalogs zu Leistungsproblemen führen.

Verwenden Sie in der Regel die Standardeinstellung, um zwischengespeicherte Überprüfungsergebnisse zu nutzen.

Die Variable **SMSTSSoftwareUpdateScanTimeout** steuert in diesem Schritt das Zeitlimit beim Überprüfen der Softwareupdates. Der Standardwert beträgt 60 Minuten. Weitere Informationen finden Sie unter [Tasksequenzvariablen](task-sequence-variables.md#SMSTSSoftwareUpdateScanTimeout).

### <a name="options-for-install-software-updates"></a>Optionen für „Softwareupdates installieren“

Konfigurieren Sie neben den Standardoptionen auch folgende zusätzliche Einstellungen auf der Registerkarte **Optionen** dieses Tasksequenzschritts:  

#### <a name="retry-this-step-if-computer-unexpectedly-restarts"></a>Führen Sie diesen Schritt erneut aus, wenn der Computer unerwartet neu gestartet wird

Wenn eines der Updates den Computer unerwartet neu startet, wiederholen Sie diesen Schritt. Der Schritt aktiviert diese Einstellung standardmäßig mit zwei Wiederholungen. Sie können eine bis fünf Wiederholungen angeben.  

> [!NOTE]  
> Konfigurieren Sie die Variable **SMSTSWaitForSecondReboot**, um anzugeben, wie viele Sekunden die Tasksequenz pausiert, nachdem der Computer in diesem Szenario neu gestartet wurde. Weitere Informationen finden Sie unter [Tasksequenzvariablen](task-sequence-variables.md#SMSTSWaitForSecondReboot).  



## <a name="join-domain-or-workgroup"></a><a name="BKMK_JoinDomainorWorkgroup"></a> Einer Domäne oder Arbeitsgruppe beitreten

Verwenden Sie diesen Schritt, um den Zielcomputer einer Arbeitsgruppe oder einer Domäne hinzuzufügen.  

> [!NOTE]
> Wenn ein in Azure Active Directory (Azure AD) eingebundener Client eine Tasksequenz für die Bereitstellung eines Betriebssystems ausführt, wird der Client im neuen Betriebssystem nicht automatisch in Azure AD eingebunden. Auch wenn der Client nicht in Azure AD eingebunden ist, wird er dennoch verwaltet.

Dieser Tasksequenzschritt wird nur in der Vollversion des Betriebssystems ausgeführt. Er kann nicht in Windows PE ausgeführt werden.

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Allgemein** und dann **Domäne oder Arbeitsgruppe beitreten** aus.

### <a name="variables-for-join-domain-or-workgroup"></a>Variablen für „Einer Domäne oder Arbeitsgruppe beitreten“

Verwenden Sie die folgenden Tasksequenzvariablen in diesem Schritt:  

- [OSDJoinAccount](task-sequence-variables.md#OSDJoinAccount)  
- [OSDJoinDomainName](task-sequence-variables.md#OSDJoinDomainName)  
- [OSDJoinDomainOUName](task-sequence-variables.md#OSDJoinDomainOUName)  
- [OSDJoinPassword](task-sequence-variables.md#OSDJoinPassword)  
- [OSDJoinSkipReboot](task-sequence-variables.md#OSDJoinSkipReboot)  
- [OSDJoinType](task-sequence-variables.md#OSDJoinType)  
- [OSDJoinWorkgroupName](task-sequence-variables.md#OSDJoinWorkgroupName)  

### <a name="cmdlets-for-join-domain-or-workgroup"></a>Cmdlets für „Einer Domäne oder Arbeitsgruppe beitreten“

Verwalten Sie diesen Schritt mit den folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepJoinDomainWorkgroup](/powershell/module/configurationmanager/Get-CMTSStepJoinDomainWorkgroup)
- [New-CMTSStepJoinDomainWorkgroup](/powershell/module/configurationmanager/New-CMTSStepJoinDomainWorkgroup)
- [Remove-CMTSStepJoinDomainWorkgroup](/powershell/module/configurationmanager/Remove-CMTSStepJoinDomainWorkgroup)
- [Set-CMTSStepJoinDomainWorkgroup](/powershell/module/configurationmanager/Set-CMTSStepJoinDomainWorkgroup)

### <a name="properties-for-join-domain-or-workgroup"></a>Eigenschaften für „Einer Domäne oder Arbeitsgruppe beitreten“

Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

#### <a name="join-a-workgroup"></a>Einer Arbeitsgruppe beitreten

Wählen Sie diese Option aus, um den Zielcomputer einer angegebenen Arbeitsgruppe hinzuzufügen. Wenn der Computer derzeit Mitglied einer Domäne ist, wird er durch Auswählen dieser Option neu gestartet.  

#### <a name="join-a-domain"></a>Einer Domäne beitreten

Wählen Sie diese Option aus, um den Zielcomputer einer angegebenen Domäne hinzuzufügen.  

Sie können optional eine Organisationseinheit (OU), der der Computer beitreten soll, eingeben oder in der angegebenen Domäne danach suchen. Wenn der Computer derzeit Mitglied einer anderen Domäne oder Arbeitsgruppe ist, wird er durch diese Option neu gestartet. Wenn der Computer bereits Mitglied einer anderen Organisationseinheit ist, ignoriert Windows Setup diese Einstellung, da Active Directory Domain Services das Ändern der Organisationseinheit über diese Methode nicht zulässt.  

#### <a name="enter-the-account-which-has-permission-to-join-the-domain"></a>Geben Sie das Konto ein, das zum Beitreten zur Domäne berechtigt ist

Wählen Sie **Festlegen** aus, um den Benutzernamen und das Kennwort für ein Konto mit der Berechtigung für den Domänenbeitritt einzugeben. Geben Sie das Konto in diesem Format ein: `Domain\account`. Weitere Informationen zum Tasksequenz-Domänenbeitrittskonto finden Sie unter [Konten](../../core/plan-design/hierarchy/accounts.md#task-sequence-domain-join-account).  



## <a name="prepare-configmgr-client-for-capture"></a><a name="BKMK_PrepareConfigMgrClientforCapture"></a> ConfigMgr-Client für Erfassung vorbereiten

Verwenden Sie diesen Schritt, um den Configuration Manager-Client auf dem Referenzcomputer zu konfigurieren oder um ihn von diesem zu entfernen. Diese Aktion bereitet den Computer auf die Erfassung im Rahmen des Imageerstellungsprozesses vor.

Dieser Schritt entfernt den Configuration Manager-Client vollständig – und nicht nur wichtige Informationen. Wenn die Tasksequenz das erfasste Betriebssystemimage bereitstellt, wird jedes Mal ein neuer Configuration Manager-Client installiert.  

> [!TIP]
> Die Tasksequenz-Engine entfernt während der Tasksequenz **Referenz-Betriebssystemabbild erstellen und erfassen** standardmäßig nur den Client. Die Tasksequenz-Engine entfernt den Client nicht bei anderen Erfassungsmethoden (z.B. Erfassungsmedien oder benutzerdefinierte Tasksequenz). Sie können dieses Verhalten für Tasksequenzen für die Betriebssystembereitstellung überschreiben. Legen Sie die Tasksequenzvariable **SMSTSUninstallCCMClient** vor dem Schritt **ConfigMgr-Client für Erfassung vorbereiten** auf **TRUE** fest. Diese Variable und dieses Verhalten gelten nur für Tasksequenzen für die Betriebssystembereitstellung. Der Client wird nach dem nächsten Neustart des Geräts entfernt.

Dieser Tasksequenzschritt wird nur in der Vollversion des Betriebssystems ausgeführt. Er kann nicht in Windows PE ausgeführt werden.  

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Images** und dann **ConfigMgr-Client für Erfassung vorbereiten** aus.


### <a name="variables-for-prepare-configmgr-client-for-capture"></a>Variablen für „ConfigMgr-Client für Erfassung vorbereiten“

Verwenden Sie die folgenden Tasksequenzvariablen in diesem Schritt:  

- SMSTSUninstallCCMClient


### <a name="cmdlets-for-prepare-configmgr-client-for-capture"></a>Cmdlets für „Konfigurations-Manager für Erfassung vorbereiten“

Verwalten Sie diesen Schritt mit den folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPrepareConfigMgrClient](/powershell/module/configurationmanager/Get-CMTSStepPrepareConfigMgrClient)
- [New-CMTSStepPrepareConfigMgrClient](/powershell/module/configurationmanager/New-CMTSStepPrepareConfigMgrClient)
- [Remove-CMTSStepPrepareConfigMgrClient](/powershell/module/configurationmanager/Remove-CMTSStepPrepareConfigMgrClient)
- [Set-CMTSStepPrepareConfigMgrClient](/powershell/module/configurationmanager/Set-CMTSStepPrepareConfigMgrClient)



## <a name="prepare-windows-for-capture"></a><a name="BKMK_PrepareWindowsforCapture"></a> Windows für die Erfassung vorbereiten

Verwenden Sie diesen Schritt, um die Sysprep-Optionen beim Erfassen eines Betriebssystemimages auf dem Referenzcomputer anzugeben. Dieser Schritt führt Sysprep aus und startet dann den Computer über das für die Tasksequenz angegebene Windows PE-Startimage neu. Diese Aktion schlägt fehl, wenn der Referenzcomputer einer Domäne angehört.  

Dieser Schritt wird nur in der Vollversion des Betriebssystems ausgeführt. Er kann nicht in Windows PE ausgeführt werden.

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Images** und dann **Windows für die Erfassung vorbereiten** aus.

### <a name="variables-for-prepare-windows-for-capture"></a>Variablen für „Windows für die Erfassung vorbereiten“

Verwenden Sie die folgenden Tasksequenzvariablen in diesem Schritt:  

- [OSDKeepActivation](task-sequence-variables.md#OSDKeepActivation)  
- [OSDTargetSystemRoot](task-sequence-variables.md#OSDTargetSystemRoot-output)  

### <a name="cmdlets-for-prepare-windows-for-capture"></a>Cmdlets für „Windows für die Erfassung vorbereiten“

Verwalten Sie diesen Schritt mit den folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPrepareWindows](/powershell/module/configurationmanager/Get-CMTSStepPrepareWindows)
- [New-CMTSStepPrepareWindows](/powershell/module/configurationmanager/New-CMTSStepPrepareWindows)
- [Remove-CMTSStepPrepareWindows](/powershell/module/configurationmanager/Remove-CMTSStepPrepareWindows)
- [Set-CMTSStepPrepareWindows](/powershell/module/configurationmanager/Set-CMTSStepPrepareWindows)

### <a name="properties-for-prepare-windows-for-capture"></a>Eigenschaften für „Windows für die Erfassung vorbereiten“

Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

#### <a name="automatically-build-mass-storage-driver-list"></a>Automatisch Liste der Massenspeichertreiber erstellen

Wählen Sie diese Option aus, damit Sysprep automatisch eine Liste der Massenspeichertreiber vom Referenzcomputer erstellt. Mit dieser Option wird die Option „Build Mass Storage Drivers“ (Massenspeichertreiber erstellen) in der Datei Sysprep.inf auf dem Referenzcomputer aktiviert. Weitere Informationen zu dieser Option finden Sie in der Sysprep-Dokumentation.  

#### <a name="do-not-reset-activation-flag"></a>Aktivierungskennzeichnung nicht zurücksetzen

Wählen Sie diese Option aus, damit Sysprep das Produktaktivierungsflag nicht zurücksetzt.  

#### <a name="shutdown-the-computer-after-running-this-action"></a>Computer nach dem Ausführen dieser Aktion herunterfahren

<!--SCCMDocs-pr issue 2695-->
Diese Option weist Sysprep an, den Computer herunterzufahren (anstelle des standardmäßigen Neustartverhaltens).

Die Tasksequenz [Windows Autopilot für vorhandene Geräte](../../../autopilot/existing-devices.md) verwendet diesen Schritt mit dieser Option.

- Wenn Sie möchten, dass die Tasksequenz das Gerät aktualisiert und dann sofort OOBE für Autopilot startet, lassen Sie diese Option deaktiviert.  

- Aktivieren Sie diese Option zum Herunterfahren des Geräts nach der Imageerstellung. Dann können Sie das Gerät einem Benutzer bereitstellen, der OOBE mit dem Autopilot startet, wenn er es zum ersten Mal aktiviert.  



## <a name="pre-provision-bitlocker"></a><a name="BKMK_PreProvisionBitLocker"></a> BitLocker vorab bereitstellen

Verwenden Sie diesen Schritt, um BitLocker auf einem Laufwerk in Windows PE zu aktivieren. Standardmäßig wird nur der belegte Speicherplatz des Laufwerks verschlüsselt, sodass die Verschlüsselung wesentlich schneller ausgeführt wird. Wenden Sie die Schlüsselverwaltungsoptionen an, indem Sie den Schritt [BitLocker aktivieren](#BKMK_EnableBitLocker) nach der Betriebssysteminstallation ausführen.

> [!IMPORTANT]
> Eine Vorabbereitstellung von BitLocker erfordert, dass der Computer über ein unterstütztes und aktiviertes Trusted Platform Module (TPM) verfügt.

Dieser Schritt wird nur in Windows PE ausgeführt. Er kann nicht in der Vollversion des Betriebssystems ausgeführt werden.  

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Datenträger** und dann **BitLocker vorab bereitstellen** aus.

### <a name="cmdlets-for-pre-provision-bitlocker"></a>Cmdlets für „BitLocker vorab bereitstellen“

Verwalten Sie diesen Schritt mit den folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepOfflineEnableBitLocker](/powershell/module/configurationmanager/Get-CMTSStepOfflineEnableBitLocker)
- [New-CMTSStepOfflineEnableBitLocker](/powershell/module/configurationmanager/New-CMTSStepOfflineEnableBitLocker)
- [Remove-CMTSStepOfflineEnableBitLocker](/powershell/module/configurationmanager/Remove-CMTSStepOfflineEnableBitLocker)
- [Set-CMTSStepOfflineEnableBitLocker](/powershell/module/configurationmanager/Set-CMTSStepOfflineEnableBitLocker)

### <a name="properties-for-pre-provision-bitlocker"></a>Eigenschaften für „BitLocker vorab bereitstellen“

Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

#### <a name="apply-bitlocker-to-the-specified-drive"></a>BitLocker auf das angegebene Laufwerk anwenden

Geben Sie das Laufwerk aus, für das Sie BitLocker aktivieren möchten. BitLocker verschlüsselt nur den belegten Speicherplatz auf dem Laufwerk.  

#### <a name="disk-encryption-mode"></a>Datenträgerverschlüsselungsmodus

<!--6995601-->
Ab Version 2006 können Sie einen der folgenden Verschlüsselungsalgorithmen auswählen:

- AES_128
- AES_256
- XTS_AES256
- XTS_AES128

Standardmäßig oder bei nicht erfolgter Festlegung verwendet der Schritt weiterhin die Standardverschlüsselungsmethode für die Betriebssystemversion. Wenn der Schritt für eine Version von Windows ausgeführt wird, die den angegebenen Algorithmus nicht unterstützt, wird auf den Standardwert des Betriebssystems zurückgegriffen. Unter diesen Umständen sendet die Tasksequenz-Engine die Statusmeldung 11911.

#### <a name="use-full-disk-encryption"></a>Vollständige Datenträgerverschlüsselung verwenden

<!--SCCMDocs-pr issue 2671-->
Standardmäßig verschlüsselt dieser Schritt nur belegten Speicherplatz auf dem Laufwerk. Dieses Standardverhalten wird aufgrund der Schnelligkeit und Effizienz empfohlen. Aktivieren Sie diese Option, wenn Ihre Organisation während des Setups das gesamte Laufwerk verschlüsseln muss. Windows Setup wartet, bis das gesamte Laufwerk verschlüsselt wurde. Dieser Vorgang kann viel Zeit in Anspruch nehmen, insbesondere auf großen Laufwerken.

#### <a name="skip-this-step-for-computers-that-do-not-have-a-tpm-or-when-tpm-is-not-enabled"></a>Überspringen Sie diesen Schritt für Computer, die nicht über TPM verfügen, oder wenn TPM nicht aktiviert ist.

Wählen Sie diese Option aus, um die Laufwerkverschlüsselung auf einem Computer zu überspringen, der kein unterstütztes oder aktiviertes TPM enthält. Verwenden Sie diese Option beispielsweise, um ein Betriebssystem auf einer VM bereitzustellen. Diese Einstellung ist für den Schritt **BitLocker vorab bereitstellen** standardmäßig aktiviert. Der Schritt kann auf einem Gerät ohne TPM oder mit einem TPM, das nicht initialisiert werden kann, nicht ausgeführt werden. Ab Version 2006 gilt Folgendes: Wenn das Gerät kein funktionierendes TPM besittz, protokolliert die Tasksequenz-Engine eine Warnung in „smsts.log“ und sendet die Statusmeldung 11912.



## <a name="release-state-store"></a><a name="BKMK_ReleaseStateStore"></a> Zustandsspeicher freigeben

Verwenden Sie diesen Schritt, um den Zustandsmigrationspunkt darüber zu benachrichtigen, dass die Erfassungs- oder Wiederherstellungsaktion abgeschlossen ist. Verwenden Sie diesen Schritt zusammen mit den Schritten **Zustandsspeicher anfordern**, **Benutzerzustand erfassen** und **Benutzerzustand wiederherstellen**. Verwenden Sie diese Schritte, um Benutzerzustanddaten mithilfe eines Zustandsmigrationspunkts und des Migrationstools für den Benutzerstatus zu migrieren.  

Weitere Informationen zum Verwalten des Benutzerzustands beim Bereitstellen von Betriebssystemen finden Sie unter [Verwalten des Benutzerzustands](../get-started/manage-user-state.md).  

Wenn Sie den Schritt **Zustandsspeicher anfordern** verwenden, um Zugriff auf einen Zustandsmigrationspunkt für die *Erfassung* des Benutzerzustands anzufordern, meldet dieser Schritt dem Zustandsmigrationspunkt, dass der Erfassungsvorgang abgeschlossen ist. Der Zustandsmigrationspunkt markiert die Benutzerzustandsdaten dann als für die Wiederherstellung verfügbar. Der Zustandsmigrationspunkt legt die Zugriffssteuerungsberechtigungen für die Benutzerzustandsdaten so fest, dass nur der wiederherstellende Computer über Lesezugriff verfügt.  

Wenn Sie den Schritt **Zustandsspeicher anfordern** verwenden, um Zugriff auf einen Zustandsmigrationspunkt für die *Wiederherstellung* des Benutzerzustands anzufordern, meldet dieser Schritt dem Zustandsmigrationspunkt, dass der Wiederherstellungsvorgang abgeschlossen ist. Der Zustandsmigrationspunkt aktiviert anschließend die konfigurierten Einstellungen für die Datenaufbewahrung.  

> [!IMPORTANT]  
> Legen Sie die Option **Bei Fehler fortsetzen** für alle Schritte zwischen **Statusspeicher anfordern** und **Statusspeicher freigeben** fest. Für jeden **Zustandsspeicher anfordern**-Schritt muss ein übereinstimmender **Zustandsspeicher freigeben**-Schritt vorhanden sein.  

Dieser Schritt wird nur in der Vollversion des Betriebssystems ausgeführt. Er kann nicht in Windows PE ausgeführt werden.

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Benutzerstatus** und dann **Statusspeicher freigeben** aus.

### <a name="variables-for-release-state-store"></a>Variablen für „Zustandsspeicher freigeben“

Verwenden Sie die folgenden Tasksequenzvariablen in diesem Schritt:  

- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-release-state-store"></a>Cmdlets für „Zustandsspeicher freigeben“

Verwalten Sie diesen Schritt mit den folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepReleaseStateStore](/powershell/module/configurationmanager/Get-CMTSStepReleaseStateStore)
- [New-CMTSStepReleaseStateStore](/powershell/module/configurationmanager/New-CMTSStepReleaseStateStore)
- [Remove-CMTSStepReleaseStateStore](/powershell/module/configurationmanager/Remove-CMTSStepReleaseStateStore)
- [Set-CMTSStepReleaseStateStore](/powershell/module/configurationmanager/Set-CMTSStepReleaseStateStore)

### <a name="properties-for-release-state-store"></a>Eigenschaften für „Zustandsspeicher freigeben“

Dieser Schritt erfordert keine Einstellungen auf der Registerkarte **Eigenschaften**.



## <a name="request-state-store"></a><a name="BKMK_RequestStateStore"></a> Zustandsspeicher anfordern

Mit diesem Schritt können Sie beim Erfassen oder Wiederherstellen eines Zustands Zugriff auf einen Zustandsmigrationspunkt anfordern.  

Weitere Informationen zum Verwalten des Benutzerzustands beim Bereitstellen von Betriebssystemen finden Sie unter [Verwalten des Benutzerzustands](../get-started/manage-user-state.md).  

Verwenden Sie diesen Schritt zusammen mit den Schritten **Zustandsspeicher freigeben**, **Benutzerzustand erfassen** und **Benutzerzustand wiederherstellen**. Verwenden Sie diese Schritte, um den Computerzustand mithilfe eines Zustandsmigrationspunkts und des Migrationstools für den Benutzerstatus zu migrieren.  

> [!NOTE]  
> Wenn Sie einen neuen Zustandsmigrationspunkt erstellen, kann es bis zu einer Stunde dauern, bis der Benutzerstatusspeicher verfügbar ist. Für eine beschleunigte Verfügbarkeit können Sie alle Eigenschaftseinstellungen des Zustandsmigrationspunkts so einstellen, dass das Update einer Standortsteuerungsdatei ausgelöst wird.  

Dieser Schritt wird in der Vollversion des Betriebssystems und in Windows PE für USMT im Offlinemodus ausgeführt.

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Benutzerstatus** und dann **Statusspeicher anfordern** aus.

### <a name="variables-for-request-state-store"></a>Variablen für „Zustandsspeicher anfordern“

Verwenden Sie die folgenden Tasksequenzvariablen in diesem Schritt:  

- [OSDStateFallbackToNAA](task-sequence-variables.md#OSDStateFallbackToNAA)  
- [OSDStateSMPRetryCount](task-sequence-variables.md#OSDStateSMPRetryCount)  
- [OSDStateSMPRetryTime](task-sequence-variables.md#OSDStateSMPRetryTime)  
- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-request-state-store"></a>Cmdlets für „Zustandsspeicher anfordern“

Verwalten Sie diesen Schritt mit den folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRequestStateStore](/powershell/module/configurationmanager/Get-CMTSStepRequestStateStore)
- [New-CMTSStepRequestStateStore](/powershell/module/configurationmanager/New-CMTSStepRequestStateStore)
- [Remove-CMTSStepRequestStateStore](/powershell/module/configurationmanager/Remove-CMTSStepRequestStateStore)
- [Set-CMTSStepRequestStateStore](/powershell/module/configurationmanager/Set-CMTSStepRequestStateStore)

### <a name="properties-for-request-state-store"></a>Eigenschaften für „Zustandsspeicher anfordern“

Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

#### <a name="capture-state-from-the-computer"></a>Zustand des Computers erfassen

Suchen Sie einen Zustandsmigrationspunkt, der die in den Einstellungen für Zustandsmigrationspunkte konfigurierten Mindestanforderungen erfüllt. Zum Beispiel **Maximale Anzahl von Clients** und **Minimum amount of free disk space** (Mindestens erforderliche Menge an freiem Speicherplatz). Diese Option garantiert nicht, dass zum Zeitpunkt der Zustandsmigration genügend freier Speicherplatz bereitsteht. Durch diese Option wird Zugriff auf den Zustandsmigrationspunkt angefordert, um den Benutzerzustand und die Einstellungen eines Computers zu erfassen.  

Wenn der Configuration Manager-Standort über mehrere aktive Zustandsmigrationspunkte verfügt, sucht dieser Schritt einen Zustandsmigrationspunkt mit verfügbarem Speicherplatz. Die Tasksequenz fragt den Verwaltungspunkt nach einer Liste der Zustandsmigrationspunkte ab und wertet diese dann aus, bis einer davon die Mindestanforderungen erfüllt.  

#### <a name="restore-state-from-another-computer"></a>Zustand von anderem Computer wiederherstellen

Fordern Sie Zugriff auf einen Zustandsmigrationspunkt an, um einen zuvor erfassten Benutzerzustand sowie Einstellungen auf einem Zielcomputer wiederherzustellen.  

Wenn es mehrere Zustandsmigrationspunkte gibt, sucht dieser Schritt den Zustandsmigrationspunkt, dessen Zustand dem des Zielcomputers entspricht.  

#### <a name="number-of-retries"></a>Anzahl der Wiederholungen

Die Anzahl der Versuche, die von diesem Schritt unternommen werden, um einen entsprechenden Zustandsmigrationspunkt zu suchen, bevor ein Fehler auftritt  

#### <a name="retry-delay-in-seconds"></a>Wiederholungsverzögerung (in Sekunden)

Hiermit wird die Anzahl der Sekunden angegeben, die vom Tasksequenzschritt zwischen Wiederholversuchen gewartet wird.  

#### <a name="if-computer-account-fails-to-connect-to-a-state-store-use-the-network-access-account"></a>Das Netzwerkzugriffskonto verwenden, wenn vom Computerkonto keine Verbindung mit dem Statusspeicher hergestellt werden kann

Wenn die Tasksequenz mit dem Computerkonto nicht auf den Zustandsmigrationspunkt zugreifen kann, verwendet sie die Anmeldeinformationen für das Netzwerkzugriffskonto, um eine Verbindung herzustellen. Diese Option ist nicht so sicher wie andere, da andere Computer das Netzwerkzugriffskonto verwenden könnten, um auf den gespeicherten Zustand zuzugreifen. Diese Option ist möglicherweise erforderlich, wenn der Zielcomputer nicht in eine Domäne eingebunden ist.  



## <a name="restart-computer"></a><a name="BKMK_RestartComputer"></a> Computer neu starten

Verwenden Sie diesen Schritt, um den Computer neu zu starten, der die Tasksequenz ausführt. Nach dem Neustart führt der Computer automatisch den nächsten Schritt der Tasksequenz aus.  

Dieser Schritt kann in der Vollversion des Betriebssystems oder in Windows PE ausgeführt werden.

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Allgemein** und dann **Computer neu starten** aus.

### <a name="variables-for-restart-computer"></a>Variablen für „Computer neu starten“

Verwenden Sie die folgenden Tasksequenzvariablen in diesem Schritt:  

- [SMSRebootMessage](task-sequence-variables.md#SMSRebootMessage)  
- [SMSRebootTimeout](task-sequence-variables.md#SMSRebootTimeout)  

### <a name="cmdlets-for-restart-computer"></a>Cmdlets für „Computer neu starten“

Verwalten Sie diesen Schritt mit den folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepReboot](/powershell/module/configurationmanager/get-cmtsstepreboot)
- [New-CMTSStepReboot](/powershell/module/configurationmanager/new-cmtsstepreboot)
- [Remove-CMTSStepReboot](/powershell/module/configurationmanager/remove-cmtsstepreboot)
- [Set-CMTSStepReboot](/powershell/module/configurationmanager/set-cmtsstepreboot)

### <a name="properties-for-restart-computer"></a>Eigenschaften für „Computer neu starten“

Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

#### <a name="the-boot-image-assigned-to-this-task-sequence"></a>Der Tasksequenz zugewiesenes Startabbild

Wenn Sie diese Option auswählen, wird das der Tasksequenz zugewiesene Startimage vom Zielcomputer verwendet. Die Tasksequenz verwendet das Startimage, um nachfolgende Schritte in Windows PE auszuführen.  

#### <a name="the-currently-installed-default-operating-system"></a>Aktuell installiertes Standardbetriebssystem

Wählen Sie diese Option aus, damit der Zielcomputer unter dem installierten Betriebssystem neu gestartet wird.  

#### <a name="notify-the-user-before-restarting"></a>Benutzer vor dem Neustart benachrichtigen

Wenn Sie diese Option auswählen, wird dem Benutzer vor dem Neustart des Zielcomputers eine Benachrichtigung angezeigt. Der Schritt wählt diese Option standardmäßig aus.  

#### <a name="notification-message"></a>Benachrichtigungsmeldung

Geben Sie eine Benachrichtigungsmeldung ein, die dem Benutzer vor dem Neustart des Zielcomputers angezeigt werden soll.  

#### <a name="message-display-time-out"></a>Timeout der Meldungsanzeige

Geben Sie den Zeitraum in Sekunden an, der bis zum Neustart des Zielcomputers verbleibt. Der Standardwert ist 60 Sekunden.  



## <a name="restore-user-state"></a><a name="BKMK_RestoreUserState"></a> Benutzerzustand wiederherstellen

Mithilfe dieses Schritts können Sie das Migrationstool für den Benutzerstatus dazu initiieren, den Benutzerzustand und die Benutzereinstellungen auf einem Zielcomputer wiederherzustellen. Verwenden Sie diesen Schritt zusammen mit dem Schritt **Benutzerzustand erfassen**.  

Weitere Informationen zum Verwalten des Benutzerzustands beim Bereitstellen von Betriebssystemen finden Sie unter [Verwalten des Benutzerzustands](../get-started/manage-user-state.md).  

Verwenden Sie diesen Schritt zusammen mit den Schritten **Zustandsspeicher anfordern** und **Zustandsspeicher freigeben**, um die Zustandseinstellungen mit einem Zustandsmigrationspunkt zu speichern oder wiederherzustellen. Diese Option entschlüsselt den USMT-Statusspeicher immer mit einem Verschlüsselungsschlüssel, den Configuration Manager generiert und verwaltet.  

Mit dem Schritt **Benutzerzustand wiederherstellen** kann eine begrenzte Teilmenge der am häufigsten verwendeten USMT-Optionen gesteuert werden. Geben Sie zusätzliche Befehlszeilenoptionen mit der Variablen **OSDMigrateAdditionalRestoreOptions** an.  

> [!IMPORTANT]  
> Wenn Sie diesen Schritt für keine Betriebssystembereitstellung verwenden, fügen Sie den Schritt [Computer neu starten](#BKMK_RestartComputer) direkt nach dem Schritt **Benutzerstatus wiederherstellen** hinzu.  

Dieser Schritt wird nur in der Vollversion des Betriebssystems ausgeführt. Er kann nicht in Windows PE ausgeführt werden.

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Benutzerstatus** und dann **Benutzerstatus wiederherstellen** aus.

### <a name="variables-for-restore-user-state"></a>Variablen für „Benutzerzustand wiederherstellen“

Verwenden Sie die folgenden Tasksequenzvariablen in diesem Schritt:  

- [_OSDMigrateUsmtRestorePackageID](task-sequence-variables.md#OSDMigrateUsmtRestorePackageID)  
- [OSDMigrateAdditionalRestoreOptions](task-sequence-variables.md#OSDMigrateAdditionalRestoreOptions)  
- [OSDMigrateContinueOnRestore](task-sequence-variables.md#OSDMigrateContinueOnRestore)  
- [OSDMigrateEnableVerboseLogging](task-sequence-variables.md#OSDMigrateEnableVerboseLogging)  
- [OSDMigrateLocalAccounts](task-sequence-variables.md#OSDMigrateLocalAccounts)  
- [OSDMigrateLocalAccountPassword](task-sequence-variables.md#OSDMigrateLocalAccountPassword)  
- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-restore-user-state"></a>Cmdlets für „Benutzerzustand wiederherstellen“

Verwalten Sie diesen Schritt mit den folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRestoreUserState](/powershell/module/configurationmanager/Get-CMTSStepRestoreUserState)
- [New-CMTSStepRestoreUserState](/powershell/module/configurationmanager/New-CMTSStepRestoreUserState)
- [Remove-CMTSStepRestoreUserState](/powershell/module/configurationmanager/Remove-CMTSStepRestoreUserState)
- [Set-CMTSStepRestoreUserState](/powershell/module/configurationmanager/Set-CMTSStepRestoreUserState)

### <a name="properties-for-restore-user-state"></a>Eigenschaften für „Benutzerzustand wiederherstellen“

Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

#### <a name="user-state-migration-tool-package"></a>USMT-Paket (Migrationsprogramm für den Benutzerzustand)

Geben Sie das Paket an, das die Version von USMT enthält, die für diesen Schritt verwendet werden soll. Für dieses Paket ist kein Programm erforderlich. Wenn der Schritt ausgeführt wird, verwendet die Tasksequenz die Version von USMT, die sich im angegebenen Paket befindet. Geben Sie ein Paket an, das die 32-Bit- oder 64-Bit-Version von USMT enthält. Die USMT-Architektur richtet sich nach der Architektur des Betriebssystems, dessen Status die Tasksequenz wiederherstellt.

#### <a name="restore-all-captured-user-profiles-with-standard-options"></a>Alle erfassten Benutzerprofile mit Standardoptionen wiederherstellen

Stellt die erfassten Benutzerprofile mit den Standardoptionen wieder her. Wählen Sie zum Anpassen der von USMT wiederherzustellenden Optionen **Erfassung der Benutzerprofile anpassen** aus.  

#### <a name="customize-how-user-profiles-are-restored"></a>Wiederherstellung von Benutzerprofilen anpassen

Ermöglicht Ihnen die Anpassung der Dateien, die Sie auf dem Zielcomputer wiederherstellen möchten. Wählen Sie **Dateien** aus, um im USMT-Paket die Konfigurationsdateien anzugeben, die Sie für die Wiederherstellung der Benutzerprofile verwenden möchten. Zum Hinzufügen einer Konfigurationsdatei geben Sie einen Namen im Feld **Dateiname** an, und wählen Sie dann **Hinzufügen** aus. Der Bereich „Dateien“ listet die Konfigurationsdateien auf, die USMT verwendet. Die von Ihnen angegebene XML-Datei legt fest, welche Benutzerdatei von USMT wiederhergestellt wird.  

#### <a name="restore-local-computer-user-profiles"></a>Lokale Computerbenutzerprofile wiederherstellen

Stellt die lokalen Computerbenutzerprofile wieder her. Diese Profile sind nicht für Domänenbenutzer vorgesehen. Weisen Sie den wiederhergestellten lokalen Benutzerkonten neue Kennwörter zu. USMT kann die ursprünglichen Kennwörter nicht migrieren. Geben Sie das Kennwort im Feld **Kennwort** ein, und bestätigen Sie es im Feld **Kennwort bestätigen** .  

#### <a name="continue-if-some-files-cannot-be-restored"></a>Fortsetzen, wenn einige Dateien nicht wiederhergestellt werden können

Setzt die Wiederherstellung des Benutzerzustands und der Benutzereinstellungen auch dann fort, wenn USMT einige Dateien nicht wiederherstellen kann. Der Schritt aktiviert diese Option standardmäßig. Wenn Sie diese Option deaktivieren und USMT beim Wiederherstellen von Dateien Fehler feststellt, schlägt dieser Schritt sofort fehl. USMT stellt nicht alle Dateien wieder her.

#### <a name="enable-verbose-logging"></a>Ausführliche Protokollierung aktivieren

Aktivieren Sie diese Option, um ausführlichere Protokolldateiinformationen zu generieren. Beim Wiederherstellen des Status erzeugt die Tasksequenz standardmäßig **Loadstate.log** im Tasksequenz-Protokollordner `%WinDir%\ccm\logs`.  



## <a name="run-command-line"></a><a name="BKMK_RunCommandLine"></a> Befehlszeile ausführen

Verwenden Sie diesen Schritt, um die angegebene Befehlszeile auszuführen.  

Der Befehl, der ausgeführt wird, muss die folgenden Kriterien erfüllen:  

- Es darf nicht mit dem Desktop interagieren. Der Befehl muss im Hintergrund oder in einem unbeaufsichtigten Modus ausgeführt werden.  

- Es darf durch die Anwendung kein eigenständiger Computerneustart initiiert werden. Der Befehl muss einen Neustart über den Standardneustartcode 3010 anfordern. Dieses Verhalten stellt sicher, dass die Tasksequenz den Neustart ordnungsgemäß verarbeitet. Wenn der Befehl den Exitcode 3010 zurückgibt, startet die Tasksequenz-Engine den Computer neu. Nach dem Neustart wird die Tasksequenz automatisch fortgesetzt.

Dieser Schritt kann in der Vollversion des Betriebssystems oder in Windows PE ausgeführt werden.

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Allgemein** und dann **Befehlszeile ausführen** aus.

### <a name="variables-for-run-command-line"></a>Variablen für „Befehlszeile ausführen“

Verwenden Sie die folgenden Tasksequenzvariablen in diesem Schritt:  

- [OSDDoNotLogCommand](task-sequence-variables.md#OSDDoNotLogCommand) (ab Version 1902)<!--3654172-->  
- [SMSTSDisableWow64Redirection](task-sequence-variables.md#SMSTSDisableWow64Redirection)  
- [SMSTSRunCommandLineUserName](task-sequence-variables.md#SMSTSRunCommandLineUserName)  
- [SMSTSRunCommandLineUserPassword](task-sequence-variables.md#SMSTSRunCommandLineUserPassword)  
- [SMSTSRunCommandLineAsUser](task-sequence-variables.md#SMSTSRunCommandLineAsUser) (ab Version 2002)<!-- 5573175 -->
- [WorkingDirectory](task-sequence-variables.md#WorkingDirectory)  

### <a name="cmdlets-for-run-command-line"></a>Cmdlets für „Befehlszeile ausführen“

Verwalten Sie diesen Schritt mit den folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRunCommandLine](/powershell/module/configurationmanager/get-cmtsstepruncommandline)
- [New-CMTSStepRunCommandLine](/powershell/module/configurationmanager/new-cmtsstepruncommandline)
- [Remove-CMTSStepRunCommandLine](/powershell/module/configurationmanager/remove-cmtsstepruncommandline)
- [Set-CMTSStepRunCommandLine](/powershell/module/configurationmanager/set-cmtsstepruncommandline)

### <a name="properties-for-run-command-line"></a>Eigenschaften für „Befehlszeile ausführen“

Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

#### <a name="command-line"></a>Befehlszeile

Gibt die Befehlszeile an, die die Tasksequenz ausführt. Dieses Feld ist erforderlich. Fügen Sie Dateinamenerweiterungen hinzu, z.B. „.vbs“ und „.exe“. Schließen Sie außerdem alle erforderlichen Einstellungsdateien und Befehlszeilenoptionen ein.  

Wenn Sie die Dateinamenerweiterung nicht angeben, verwendet Configuration Manager die Erweiterung „.com“, „.exe“ oder „.bat“. Wenn die Dateinamenerweiterung keinem ausführbaren Typ zugeordnet ist, wendet Configuration Manager eine lokale Zuordnung an. Lautet die Befehlszeile z.B. „readme.gif“, startet Configuration Manager die Anwendung, die auf dem Zielcomputer zum Öffnen von GIF-Dateien angegeben ist.  

Beispiele:  

`setup.exe /a`  

`cmd.exe /c copy Jan98.dat c:\sales\Jan98.dat`  

> [!NOTE]  
> Für eine erfolgreiche Ausführung sollte Befehlszeilenoptionen der Befehl **cmd.exe /c** vorausgehen. Zu den Beispielen für diese Aktionen zählen die Umleitung der Ausgabe, das Piping und das Kopieren von Befehlen.  

#### <a name="output-to-task-sequence-variable"></a>Ausgabe an Tasksequenzvariable

<!--user story 4977616/bug 4798352-->

Speichern Sie die Befehlsausgabe ab der Version 1910 in einer benutzerdefinierten Tasksequenzvariablen.

> [!Note]  
> Configuration Manager beschränkt diese Ausgabe auf die letzten 1000 Zeichen.

#### <a name="disable-64-bit-file-system-redirection"></a>64-Bit-Dateisystemumleitung deaktivieren

64-Bit-Betriebssysteme verwenden standardmäßig den WOW64-Dateisystemredirector, um Befehlszeilen auszuführen. Durch dieses Verhalten können 32-Bit-Versionen von ausführbaren Betriebssystemdateien und Bibliotheken ordnungsgemäß gesucht werden. Wählen Sie diese Option aus, um die Verwendung des Dateisystem-Redirectors von WOW64 zu deaktivieren. Windows führt den Befehl mithilfe nativer 64-Bit-Versionen von ausführbaren Betriebssystemdateien und Bibliotheken aus. Unter einem 32-Bit-Betriebssystem hat diese Option keine Auswirkungen.  

#### <a name="start-in"></a>Starten in

Gibt den ausführbaren Ordner für das Programm mit bis zu 127 Zeichen an. Für diesen Ordner kann ein absoluter Pfad auf dem Zielcomputer oder ein relativer Pfad zum Verteilungspunktordner mit dem Paket angegeben werden. Dieses Feld ist optional.  

Beispiele:  

`c:\officexp`  

`i386`  

> [!NOTE]  
> Die Schaltfläche **Durchsuchen** durchsucht den lokalen Computer nach Dateien und Ordnern. Jede Auswahl muss auch auf dem Zielcomputer vorhanden sein. Der Speicherort sowie die Datei- und Ordnernamen müssen identisch sein.  

#### <a name="package"></a>Paket

Wenn Sie Dateien oder Programme in der Befehlszeile angeben, die sich nicht bereits auf dem Zielcomputer befinden, wählen Sie diese Option aus, um das Configuration Manager-Paket anzugeben, das die erforderlichen Dateien enthält. Für das Paket ist kein Programm erforderlich. Diese Option wird nicht benötigt, wenn die angegebenen Dateien auf dem Zielcomputer vorhanden sind.  

#### <a name="time-out"></a>Timeout in

Legt einen Wert fest, der angibt, wie lange Configuration Manager das Ausführen der Befehlszeile zulässt. Dieser Wert kann zwischen 1 und 999 Minuten liegen. Der Standardwert beträgt 15 Minuten. Diese Option ist standardmäßig deaktiviert.  

> [!IMPORTANT]  
> Wenn Sie einen Wert eingeben, der nicht genügend Zeit zum erfolgreichen Abschließen des angegebenen Befehls zur Verfügung stellt, schlägt dieser Schritt fehl. Je nach Schritt- und Gruppenbedingungen schlägt möglicherweise die gesamte Tasksequenz fehl. Wenn das Timeout abläuft, beendet Configuration Manager den Befehlszeilenprozess.  

#### <a name="run-this-step-as-the-following-account"></a>Diesen Schritt unter folgendem Konto ausführen

Gibt an, dass die Befehlszeile unter einem anderen Windows-Benutzerkonto als dem lokalen Systemkonto ausgeführt wird.  

> [!NOTE]  
> Um einfache Skripts oder Befehle nach der Installation des Betriebssystems mit einem anderen Konto auszuführen, fügen Sie zuerst dieses Konto dem Computer hinzu. Zudem müssen Sie ggf. das Windows-Benutzerkontoprofil wiederherstellen, um komplexere Programme wie Windows Installer auszuführen.  

#### <a name="account"></a>Konto

Gibt das Windows-Benutzerkonto an, mit dem dieser Schritt die Befehlszeile ausführt. Die Befehlszeile wird mit den Berechtigungen des angegebenen Kontos ausgeführt. Wählen Sie **Festlegen** aus, um das lokale Benutzer- oder Domänenkonto anzugeben. Weitere Informationen zum ausführenden Tasksequenzkonto finden Sie unter [Konten](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account).

> [!IMPORTANT]  
> Wenn dieser Schritt ein Benutzerkonto angibt und unter Windows PE ausgeführt wird, schlägt die Aktion fehl. Sie können Windows PE nicht mit einer Domäne verknüpfen. Die Datei **smsts.log** zeichnet diesen Fehler auf.  

### <a name="options-for-run-command-line"></a>Optionen für „Befehlszeile ausführen“

Konfigurieren Sie neben den Standardoptionen auch folgende zusätzliche Einstellungen auf der Registerkarte **Optionen** dieses Tasksequenzschritts:  

#### <a name="success-codes"></a>Erfolgscodes

Fügen Sie andere Exitcodes aus dem Skript hinzu, die vom Schritt als „Erfolgreich“ ausgewertet werden sollen.



## <a name="run-powershell-script"></a><a name="BKMK_RunPowerShellScript"></a> PowerShell-Skript ausführen

Verwenden Sie diesen Schritt, um das angegebene Windows PowerShell-Skript auszuführen.  

Das Skript muss folgende Kriterien erfüllen:  

- Es darf nicht mit dem Desktop interagieren. Das Skript muss im Hintergrund oder in einem unbeaufsichtigten Modus ausgeführt werden.  

- Es darf durch die Anwendung kein eigenständiger Computerneustart initiiert werden. Das Skript muss einen Neustart über den Standardneustartcode 3010 anfordern. Dieses Verhalten stellt sicher, dass die Tasksequenz den Neustart ordnungsgemäß verarbeitet. Wenn das Skript den Exitcode 3010 zurückgibt, startet die Tasksequenz-Engine den Computer neu. Nach dem Neustart wird die Tasksequenz automatisch fortgesetzt.

Dieser Schritt kann in der Vollversion des Betriebssystems oder in Windows PE ausgeführt werden. Um diesen Schritt in Windows PE auszuführen, aktivieren Sie PowerShell im Startimage. Aktivieren Sie die Windows PE-PowerShell-Komponente auf der Registerkarte **Optionale Komponenten** in den Eigenschaften des Startimages. Weitere Informationen dazu, wie ein Startimage geändert wird, finden Sie unter [Verwalten von Startimages](../get-started/manage-boot-images.md).  

> [!NOTE]  
> PowerShell ist unter Windows Embedded-Betriebssystemen standardmäßig nicht aktiviert.  

> [!WARNING]
> Bestimmte Antischadsoftware kann unbeabsichtigt Ereignisse auslösen, die gegen den Tasksequenzschritt „PowerShell-Skript ausführen“ von Configuration Manager gerichtet sind. Es empfiehlt sich, „%windir%\temp\smstspowershellscripts“ auszuschließen, damit die Antischadsoftware die störungsfreie Ausführung dieser Skripts zulässt.

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Allgemein** und dann **PowerShell-Skript ausführen** aus.

### <a name="variables-for-run-powershell-script"></a>Variablen für „PowerShell-Skript ausführen“

Verwenden Sie die folgenden Tasksequenzvariablen in diesem Schritt:  

- [OSDLogPowerShellParameters](task-sequence-variables.md#OSDLogPowerShellParameters) (ab Version 1902)<!--3556028-->  
- [SMSTSRunPowerShellAsUser](task-sequence-variables.md#SMSTSRunPowerShellAsUser) (ab Version 2002)<!-- 5573175 -->
- [SMSTSRunPowerShellUserName](task-sequence-variables.md#SMSTSRunPowerShellUserName)  
- [SMSTSRunPowerShellUserPassword](task-sequence-variables.md#SMSTSRunPowerShellUserPassword)  

### <a name="cmdlets-for-run-powershell-script"></a>Cmdlets für „PowerShell-Skript ausführen“

Verwalten Sie diesen Schritt mit den folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRunPowerShellScript](/powershell/module/configurationmanager/get-cmtssteprunpowershellscript)
- [New-CMTSStepRunPowerShellScript](/powershell/module/configurationmanager/new-cmtssteprunpowershellscript)
- [Remove-CMTSStepRunPowerShellScript](/powershell/module/configurationmanager/remove-cmtssteprunpowershellscript)
- [Set-CMTSStepRunPowerShellScript](/powershell/module/configurationmanager/set-cmtssteprunpowershellscript)

> [!Note]  
> Verwenden Sie signierte PowerShell-Skripts im Unicode-Format. Das ANSI-Format (Standardeinstellung) funktioniert in diesem Schritt nicht.

### <a name="properties-for-run-powershell-script"></a>Eigenschaften für „PowerShell-Skript ausführen“

Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

#### <a name="package"></a>Paket

Gibt das Configuration Manager-Paket mit dem PowerShell-Skript an. Ein Paket kann mehrere PowerShell-Skripts enthalten.  

#### <a name="script-name"></a>Skriptname

Gibt den Namen des auszuführenden PowerShell-Skripts an. Dieses Feld ist erforderlich.  

#### <a name="enter-a-powershell-script"></a>PowerShell-Skript eingeben

<!-- 3556028 -->
Ab der Version 1902 können Sie in diesem Schritt Windows PowerShell-Code direkt eingeben. Dank dieses Features können Sie PowerShell-Befehle während einer Tasksequenz ausführen, ohne zuerst ein Paket mit dem Skript erstellen und verteilen zu müssen.

Beim Hinzufügen oder Bearbeiten eines Skripts im PowerShell-Skriptfenster haben Sie folgende Möglichkeiten:  

- Direktes Bearbeiten des Skripts  

- Öffnen eines vorhandenen Skripts aus einer Datei  

- Navigieren zu einem bereits vorhandenen, genehmigten [Skript](../../apps/deploy-use/create-deploy-scripts.md) in Configuration Manager

> [!Important]  
> Wenn Sie diese neuen Configuration Manager-Features nach der Aktualisierung des Standorts nutzen möchten, müssen Sie auch Clients auf die neueste Version aktualisieren. Beim Update des Standorts und der Konsole werden neue Features in der Configuration Manager-Konsole angezeigt. Das vollständige Szenario ist allerdings erst einsatzbereit, wenn auch die Clientversion aktualisiert wird.

#### <a name="parameters"></a>Parameter

Gibt die Parameter an, die an das PowerShell-Skript übergeben werden. Diese Parameter sind identisch mit den PowerShell-Skriptparametern in der Befehlszeile.  

Geben Sie die Parameter an, die vom Skript verwendet werden, nicht die für die Windows PowerShell-Befehlszeile.  
Das folgende Beispiel enthält gültige Parameter:  

`-MyParameter1 MyValue1 -MyParameter2 MyValue2`  

Das folgende Beispiel enthält ungültige Parameter. Bei den ersten beiden Elementen handelt es sich um Windows PowerShell-Befehlszeilenparameter ( **-NoLogo** und **-ExecutionPolicy Unrestricted**). Das Skript verarbeitet diese Parameter nicht.  

`-NoLogo -ExecutionPolicy Unrestricted -File MyScript.ps1 -MyParameter1 MyValue1 -MyParameter2 MyValue2`

<!-- SCCMDocs-pr issue 3561 -->
Wenn ein Parameterwert ein Sonderzeichen enthält, setzen Sie den Wert in einfache Anführungszeichen (`'`). Bei Verwendung doppelter Anführungszeichen (`"`) wird der Parameter möglicherweise nicht ordnungsgemäß verarbeitet.

Beispiel: `-Arg1 '%TSVar1%' -Arg2 '%TSVar2%'`

Ab Version 2002 sollten Sie diese Eigenschaft auf eine Variable festlegen.<!-- 5690481 --> Wenn Sie beispielsweise `%MyScriptVariable%` angeben, wird von der Tasksequenz beim Ausführen des Skripts der Wert dieser benutzerdefinierten Variable zur PowerShell-Befehlszeile hinzugefügt.

#### <a name="powershell-execution-policy"></a>PowerShell-Ausführungsrichtlinie

Bestimmen Sie, welche PowerShell-Skripts auf dem Computer ausgeführt werden dürfen. Wählen Sie eine der folgenden Ausführungsrichtlinien aus:  

- **Alle signiert:** Nur Skripts, die von einem vertrauenswürdigen Herausgeber signiert wurden, werden ausgeführt.  

- **Nicht definiert:** Es sind keine Ausführungsrichtlinien definiert.  

- **Umgehung**: Alle Konfigurationsdateien werden geladen und alle Skripts ausgeführt. Wenn Sie ein nicht signiertes Skript aus dem Internet herunterladen, fordert Windows PowerShell Sie vor der Skriptausführung nicht zum Erteilen der Berechtigung auf.  

> [!IMPORTANT]  
> PowerShell 1.0 unterstützt nicht die Ausführungsrichtlinien „Nicht definiert“ und „Umgehung“.  

#### <a name="output-to-task-sequence-variable"></a>Ausgabe an Tasksequenzvariable

<!-- 3556028 -->
Speichern Sie die Skriptausgabe ab der Version 1902 in einer benutzerdefinierten Tasksequenzvariablen.

> [!Note]  
> Ab Version 1910 wird diese Ausgabe von Configuration Manager auf die letzten 1000 Zeichen beschränkt.

Ein Beispiel für die Verwendung dieser Schritteigenschaft finden Sie unter [Festlegen von Variablen](using-task-sequence-variables.md#bkmk_run-ps).

#### <a name="start-in"></a>Starten in

<!-- 3556028 -->
Gaben Sie ab der Version 1902 den Startordner für das Skript an (maximal 127 Zeichen). Für diesen Ordner kann ein absoluter Pfad auf dem Zielcomputer oder ein relativer Pfad zum Verteilungspunktordner mit dem Paket angegeben werden. Dieses Feld ist optional.  

> [!NOTE]  
> Die Schaltfläche **Durchsuchen** durchsucht den lokalen Computer nach Dateien und Ordnern. Jede Auswahl muss auch auf dem Zielcomputer vorhanden sein. Der Speicherort sowie die Datei- und Ordnernamen müssen identisch sein.  

#### <a name="time-out"></a>Timeout in

<!-- 3556028 -->
Geben Sie ab der Version 1902 an, wie lange Configuration Manager die Ausführung des PowerShell-Skripts zulassen soll. Dieser Wert kann zwischen 1 und 999 Minuten liegen. Der Standardwert beträgt 15 Minuten. Diese Option ist standardmäßig deaktiviert.  

> [!IMPORTANT]  
> Wenn Sie einen Wert eingeben, der nicht genügend Zeit zum erfolgreichen Abschließen des angegebenen Skripts lässt, ist dieser Schritt nicht erfolgreich. Je nach Schritt- und Gruppenbedingungen schlägt möglicherweise die gesamte Tasksequenz fehl. Nach Ablauf des Timeouts beendet Configuration Manager den PowerShell-Prozess.  

#### <a name="run-this-step-as-the-following-account"></a>Diesen Schritt unter folgendem Konto ausführen

<!-- 3556028 -->
Geben Sie ab der Version 1902 an, dass das PowerShell-Skript unter einem Windows-Benutzerkonto ausgeführt wird, bei dem es sich nicht um das lokale Systemkonto handelt.  

> [!NOTE]  
> Um einfache Skripts oder Befehle nach der Installation des Betriebssystems mit einem anderen Konto auszuführen, fügen Sie zuerst dieses Konto dem Computer hinzu. Zudem müssen Sie ggf. Windows-Benutzerprofile wiederherstellen, um komplexere Aktionen ausführen zu können.  

#### <a name="account"></a>Konto

<!-- 3556028 -->
Geben Sie ab der Version 1902 das Windows-Benutzerkonto an, das von diesem Schritt zum Ausführen des PowerShell-Skripts verwendet wird. Das angegebene Konto muss einem lokalen Administrator auf dem System gehören, und das Skript wird mit den Berechtigungen dieses Kontos ausgeführt. Wählen Sie **Festlegen** aus, um das lokale Benutzer- oder Domänenkonto anzugeben. Weitere Informationen zum ausführenden Tasksequenzkonto finden Sie unter [Konten](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account).

> [!IMPORTANT]  
> Wenn dieser Schritt ein Benutzerkonto angibt und unter Windows PE ausgeführt wird, schlägt die Aktion fehl. Sie können Windows PE nicht mit einer Domäne verknüpfen. Die Datei **smsts.log** zeichnet diesen Fehler auf.  

### <a name="options-for-run-powershell-script"></a>Optionen für „PowerShell-Skript ausführen“

Konfigurieren Sie neben den Standardoptionen auch folgende zusätzliche Einstellungen auf der Registerkarte **Optionen** dieses Tasksequenzschritts:  

#### <a name="success-codes"></a>Erfolgscodes

<!-- 3556028 -->
Fügen Sie ab der Version 1902 andere Exitcodes aus dem Skript hinzu, die von dem Schritt als „Erfolgreich“ ausgewertet werden sollen.



## <a name="run-task-sequence"></a><a name="child-task-sequence"></a> Ausführen einer Tasksequenz

> [!Note]  
> In Version 1910 wird dieses Feature standardmäßig von Configuration Manager aktiviert. In Version 1906 oder früher aktiviert Configuration Manager dieses optionale Feature nicht automatisch. Aktivieren Sie diese Funktion, bevor Sie sie verwenden. Weitere Informationen finden Sie unter [Enable optional features from updates (Aktivieren optionaler Features von Updates)](../../core/servers/manage/install-in-console-updates.md#bkmk_options).

Dieser Schritt führt eine weitere Tasksequenz aus. Er erstellt eine Über-/Unterordnungsbeziehung zwischen den Tasksequenzen. Mithilfe einer untergeordneten Tasksequenz können Sie weitere modular aufgebaute, wiederverwendbare Tasksequenzen erstellen.

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Allgemein** und dann **Tasksequenz ausführen** aus.

### <a name="specifications-and-limitations-for-run-task-sequence"></a>Spezifikationen und Einschränkungen für „Tasksequenz ausführen“

Berücksichtigen Sie Folgendes, wenn Sie eine untergeordnete Tasksequenz einer Tasksequenz hinzufügen:  

- Die über- und untergeordneten Tasksequenzen werden effektiv in einer einzigen Richtlinie kombiniert, die der Client ausführt.  

- Die Umgebung ist global. Wenn die übergeordnete Tasksequenz eine Variable festlegt und die untergeordnete Tasksequenz diese Variable ändert, behält diese den aktuellen Wert bei. Wenn die untergeordnete Tasksequenz eine neue Variable erstellt, ist diese für den Rest der übergeordneten Tasksequenz verfügbar.  

- Statusmeldungen werden in der Regel für einen einzelnen Tasksequenzvorgang gesendet.  

- Die Tasksequenz schreibt Einträge in die Datei **smsts.log**, mit neuen Protokolleinträgen, die den Start einer untergeordneten Tasksequenz deutlich machen.  

<!--the following points are from SCCMdocs issue #1079-->

- Sie können keine Tasksequenz mit einem Startimageverweis auswählen. Geben sie für jede Bereitstellung, die ein Startimage erfordert, diese auf der übergeordneten Tasksequenz an.  

- Wenn eine untergeordnete Tasksequenz deaktiviert ist, tritt bei der Bereitstellung ein Fehler auf. Sie können diese Einschränkung nicht mit der **Bei Fehler fortsetzen**-Option umgehen.  

- Wenn eine untergeordnete Tasksequenz Schritte enthält, die *wirkungsvoll* sein können, erkennt das Software Center dies nicht und zeigt nicht die „Wirkungsvoll“-Benachrichtigung an. Ändern Sie die Eigenschaften der übergeordneten Tasksequenz auf der Registerkarte „Benutzerbenachrichtigung“, um Folgendes anzugeben: **Dies ist eine wirkungsvolle Tasksequenz**.  

- Wenn einer untergeordneten Tasksequenz ein Paketverweis fehlt, wird dieser Zustand beim Anzeigen der übergeordneten Tasksequenz nicht erkannt. Wenn Sie die übergeordnete Tasksequenz bearbeiten, erkennt sie alle fehlenden Verweise in untergeordneten Tasksequenzen, wenn Sie Änderungen am übergeordneten Element vornehmen.  

### <a name="cmdlets-for-run-task-sequence"></a>Cmdlets für „Tasksequenz ausführen“

Ab Version 1906 können Sie diesen Schritt mit den folgenden PowerShell-Cmdlets verwalten:<!-- 2839943, SCCMDocs#1118 -->

- [Get-CMTSStepRunTaskSequence](/powershell/module/configurationmanager/get-cmtsstepruntasksequence)
- [New-CMTSStepRunTaskSequence](/powershell/module/configurationmanager/new-cmtsstepruntasksequence)
- [Remove-CMTSStepRunTaskSequence](/powershell/module/configurationmanager/remove-cmtsstepruntasksequence)
- [Set-CMTSStepRunTaskSequence](/powershell/module/configurationmanager/set-cmtsstepruntasksequence)

Weitere Informationen finden Sie unter [Anmerkungen zu Version 1906 – Neue Cmdlets](/powershell/sccm/1906-release-notes#new-cmdlets).

### <a name="properties-for-run-task-sequence"></a>Eigenschaften für „Tasksequenz ausführen“

Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

#### <a name="select-task-sequence-to-run"></a>Auszuführende Tasksequenz auswählen

Wählen Sie **Durchsuchen** aus, um die untergeordnete Tasksequenz auszuwählen. Das Dialogfeld **Tasksequenz auswählen** zeigt die übergeordnete Tasksequenz nicht an.



## <a name="set-dynamic-variables"></a><a name="BKMK_SetDynamicVariables"></a> Dynamische Variablen festlegen

Verwenden Sie diesen Schritt, um folgende Aktionen durchzuführen:  

1. Sammeln Sie Informationen vom Computer und seiner Umgebung. Legen Sie anhand dieser Informationen dann die angegebenen Tasksequenzvariablen fest.  

2. Werten Sie definierte Regeln aus. Legen Sie Tasksequenzvariablen anhand der Regeln fest, die als TRUE ausgewertet wurden.  

Dieser Schritt kann in der Vollversion des Betriebssystems oder in Windows PE ausgeführt werden.  

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Allgemein** und dann **Dynamische Variablen festlegen** aus.

### <a name="variables-for-set-dynamic-variables"></a>Variablen für „Dynamische Variablen festlegen“

Die Tasksequenz legt automatisch die folgenden schreibgeschützten Tasksequenzvariablen fest:  

- [\_SMSTSMake](task-sequence-variables.md#SMSTSMake)  
- [\_SMSTSModel](task-sequence-variables.md#SMSTSModel)  
- [\_SMSTSMacAddresses](task-sequence-variables.md#SMSTSMacAddresses)  
- [\_SMSTSIPAddresses](task-sequence-variables.md#SMSTSIPAddresses)  
- [\_SMSTSSerialNumber](task-sequence-variables.md#SMSTSSerialNumber)  
- [\_SMSTSAssetTag](task-sequence-variables.md#SMSTSAssetTag)  
- [\_SMSTSUUID](task-sequence-variables.md#SMSTSUUID)  

### <a name="cmdlets-for-set-dynamic-variables"></a>Cmdlets für „Dynamische Variablen festlegen“

Verwalten Sie diesen Schritt mit den folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepSetDynamicVariable](/powershell/module/configurationmanager/get-cmtsstepsetdynamicvariable)
- [New-CMTSStepSetDynamicVariable](/powershell/module/configurationmanager/new-cmtsstepsetdynamicvariable)
- [Remove-CMTSStepSetDynamicVariable](/powershell/module/configurationmanager/remove-cmtsstepsetdynamicvariable)
- [Set-CMTSStepSetDynamicVariable](/powershell/module/configurationmanager/set-cmtsstepsetdynamicvariable)

### <a name="properties-for-set-dynamic-variables"></a>Eigenschaften für „Dynamische Variablen festlegen“

Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

#### <a name="dynamic-rules-and-variables"></a>Dynamische Regeln und Variablen

Fügen Sie eine Regel hinzu, um eine dynamische Variable für die Verwenden in der Tasksequenz festzulegen. Legen Sie dann einen Wert für jede Variable fest, die in der Regel angegeben wurde. Fügen Sie zusätzlich mindestens eine Variable hinzu, ohne eine Regel hinzuzufügen. Wenn Sie eine Regel hinzufügen, können Sie aus den folgenden Kategorien auswählen:  

- **Computer**: Werte für das Hardwarebestandskennzeichen, die UUID, Seriennummer oder MAC-Adresse werden ausgewertet. Legen Sie bei Bedarf mehrere Werte fest. Wenn ein Wert TRUE ist, wird die Regel als TRUE gewertet. Folgende Regel wird beispielsweise als TRUE ausgewertet, wenn die Seriennummer des Geräts „5892087“ und die MAC-Adresse „22-A4-5A-13-78-26“ ist:  

    `IF Serial Number = 5892087 OR MAC address = 26-78-13-5A-A4-22 THEN`  

- **Speicherort**: Werte für das Standardgateway des Netzwerks werden ausgewertet.  

- **Typ und Modell**: Werte für den Typ und das Modell eines Computers werden ausgewertet. Sowohl Hersteller als auch Modell müssen als „Wahr“ ausgewertet werden, damit die Regel als „Wahr“ ausgewertet wird.

    Geben Sie ein Sternchen (`*`) und ein Fragezeichen (`?`) als Platzhalter an. Das Sternchen steht für mehrere und das Fragezeichen für ein einzelnes Zeichen. Die Zeichenfolge `DELL*900?` entspricht beispielsweise sowohl `DELL-ABC-9001` als auch `DELL9009`.  

- **Tasksequenzvariable**: Fügt eine Tasksequenzvariable, eine Bedingung und einen Wert zum Auswerten hinzu. Die Regel wird als „Wahr“ ausgewertet, wenn der für die Variable festgelegte Wert die angegebene Bedingung erfüllt.  

    Geben Sie eine oder mehrere Variablen an, die für eine Regel festgelegt werden sollen, die als TRUE ausgewertet wird, oder legen Sie Variablen ohne Verwendung einer Regel fest. Wählen Sie eine vorhandene Variable aus, oder erstellen Sie eine benutzerdefinierte Variable.  

  - **Vorhandene Tasksequenzvariablen**: Eine oder mehrere Variablen werden aus einer Liste vorhandener Tasksequenzvariablen ausgewählt. Arrayvariablen stehen nicht zur Auswahl.  

  - **Benutzerdefinierte Tasksequenzvariablen**: Eine benutzerdefinierte Tasksequenzvariable wird definiert. Sie können auch eine vorhandene Tasksequenzvariable angeben. Diese Einstellung ist nützlich, um ein vorhandenes Variablenarray wie **OSDAdapter** anzugeben, da Variablenarrays nicht in der Liste der vorhandenen Tasksequenzvariablen enthalten sind.  

Nachdem Sie die Variablen für eine Regel ausgewählt haben, geben Sie einen Wert für jede Variable an. Die Variable wird auf den angegebenen Wert festgelegt, wenn die Regel als „Wahr“ ausgewertet wird. Sie können für jede Variable die Option **Diesen Wert nicht anzeigen** auswählen, um den Wert der Variable auszublenden. Standardmäßig blenden einige vorhandene Variablen Werte aus, z.B. die Variable **OSDCaptureAccountPassword**.  

> [!IMPORTANT]  
> Wenn Sie eine Tasksequenz mit dem Schritt **Dynamische Variablen festlegen** importieren, entfernt Configuration Manager alle Variablenwerte, die als **Diesen Wert nicht anzeigen** gekennzeichnet sind. Nachdem Sie die Tasksequenz importiert haben, geben Sie den Wert für die dynamische Variable erneut ein.

Bei Verwendung der Option **Diesen Wert nicht anzeigen** wird der Wert der Variable im Tasksequenz-Editor nicht angezeigt. In der Tasksequenz-Protokolldatei (**smsts.log**) oder im Tasksequenz-Debugger wird der Wert der Variable ebenfalls nicht angezeigt. Die Variable kann allerdings weiterhin von der Tasksequenz während der Ausführung verwendet werden. Wenn diese Variablen nicht mehr ausgeblendet sein sollen, löschen Sie diese zuerst. Definieren Sie dann erneut die Variablen, und lassen Sie die Option zum Ausblenden dieser Variablen dieses Mal deaktiviert.  

> [!WARNING]  
> Wenn Sie Variablen in die Befehlszeile des Schritts **Befehlszeile ausführen** einfügen, zeigt die Protokolldatei der Tasksequenz die vollständige Befehlszeile einschließlich der Variablenwerte an. Um zu verhindern, dass möglicherweise vertrauliche Daten in der Protokolldatei angezeigt werden, legen Sie die Tasksequenzvariable **OSDDoNotLogCommand** auf `TRUE` fest.


## <a name="set-task-sequence-variable"></a><a name="BKMK_SetTaskSequenceVariable"></a> Tasksequenzvariable festlegen

Verwenden Sie diesen Schritt, um den Wert einer Variablen festzulegen, die mit der Tasksequenz verwendet wird.  

Dieser Schritt kann in der Vollversion des Betriebssystems oder in Windows PE ausgeführt werden.

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Allgemein** und dann **Tasksequenzvariable festlegen** aus.

### <a name="variables-for-set-task-sequence-variable"></a>Variablen für „Tasksequenzvariable festlegen“

Tasksequenzvariablen werden von Tasksequenzaktionen gelesen und definieren das Verhalten dieser Aktionen. Weitere Informationen zu bestimmten Tasksequenzvariablen und ihrer Verwendung finden Sie in den folgenden Artikeln:  

- [Verwenden von Tasksequenzvariablen](using-task-sequence-variables.md)  
- [Tasksequenzvariablen](task-sequence-variables.md)  

### <a name="cmdlets-for-set-task-sequence-variable"></a>Cmdlets für „Tasksequenzvariable festlegen“

Verwalten Sie diesen Schritt mit den folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepSetVariable](/powershell/module/configurationmanager/get-cmtsstepsetvariable)
- [New-CMTSStepSetVariable](/powershell/module/configurationmanager/new-cmtsstepsetvariable)
- [Remove-CMTSStepSetVariable](/powershell/module/configurationmanager/remove-cmtsstepsetvariable)
- [Set-CMTSStepSetVariable](/powershell/module/configurationmanager/set-cmtsstepsetvariable)

### <a name="properties-for-set-task-sequence-variable"></a>Eigenschaften für „Tasksequenzvariable festlegen“

Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

#### <a name="task-sequence-variable"></a>Tasksequenzvariable

Geben Sie den Namen einer integrierten Tasksequenzvariablen oder einer Tasksequenz-Aktionsvariablen an, oder geben Sie einen benutzerdefinierten Variablennamen an.  

#### <a name="do-not-display-this-value"></a>Diesen Wert nicht anzeigen

<!--1358330-->
Aktivieren Sie diese Option, um vertrauliche Daten zu maskieren, die in Tasksequenzvariablen gespeichert sind. Dies ist beispielsweise bei der Angabe eines Kennworts der Fall.

> [!NOTE]
> Aktivieren Sie diese Option aus, und legen Sie den Wert der Tasksequenzvariablen fest. Andernfalls wird der Wert der Variablen nicht so festgelegt, wie Sie es beabsichtigen, was bei der Ausführung der Tasksequenz zu unerwartetem Verhalten führen kann.<!--SCCMdocs issue #800-->

Bei Verwendung der Option **Diesen Wert nicht anzeigen** wird der Wert der Variable im Tasksequenz-Editor nicht angezeigt. In der Tasksequenz-Protokolldatei (**smsts.log**) oder im Tasksequenz-Debugger wird der Wert der Variable ebenfalls nicht angezeigt. Die Variable kann allerdings weiterhin von der Tasksequenz während der Ausführung verwendet werden. Wenn diese Variable nicht mehr verborgen werden soll, löschen Sie sie zuerst. Definieren Sie die Variable dann neu, und wählen Sie die Option zum Ausblenden nicht aus.

> [!WARNING]
> Wenn Sie Variablen in die Befehlszeile des Schritts **Befehlszeile ausführen** einfügen, zeigt die Protokolldatei der Tasksequenz die vollständige Befehlszeile einschließlich der Variablenwerte an. Um zu verhindern, dass möglicherweise vertrauliche Daten in der Protokolldatei angezeigt werden, legen Sie die Tasksequenzvariable **OSDDoNotLogCommand** auf `TRUE` fest.<!-- 6963278 -->

#### <a name="value"></a>Wert  

Die Tasksequenz legt die Variable auf diesen Wert fest. Legen Sie diese Tasksequenzvariable auf den Wert einer anderen Tasksequenzvariablen mit der Syntax `%varname%` fest.  



## <a name="setup-windows-and-configmgr"></a><a name="BKMK_SetupWindowsandConfigMgr"></a> Windows und ConfigMgr einrichten

Verwenden Sie diesen Schritt, um den Übergang von Windows PE zum neuen Betriebssystem auszuführen. Dieser Tasksequenzschritt muss bei jeder Betriebssystembereitstellung ausgeführt werden. Er installiert den Configuration Manager-Client im neuen Betriebssystem und bereitet die Tasksequenz für die Ausführung im neuen Betriebssystem vor.  

Dieser Schritt ist für den Umstieg der Tasksequenz von Windows PE zum vollständigen Betriebssystem zuständig. Der Schritt wird aufgrund dieses Umstiegs in Windows PE und im vollständigen Betriebssystem ausgeführt. Da der Umstieg jedoch in Windows PE beginnt, kann er nur während des Windows PE-Teils der Tasksequenz hinzugefügt werden.  

Dieser Schritt ersetzt die Verzeichnisvariablen „sysprep.inf“ oder „unattend.xml“, z.B. `%WINDIR%` und `%ProgramFiles%`, durch das Windows PE-Installationsverzeichnis `X:\Windows`. Die Tasksequenz ignoriert Variablen, die mithilfe dieser Umgebungsvariablen angegeben wurden.  

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Images** und dann **Windows und ConfigMgr einrichten** aus.

### <a name="behaviors-for-setup-windows-and-configmgr"></a>Verhalten für „Windows und Konfigurations-Manager einrichten“

Dieser Schritt führt die folgenden Aktionen aus:  

#### <a name="preliminaries-windows-pe"></a>Vorbereitende Maßnahmen: Windows PE  

1. Ersetzt Tasksequenzvariablen in der Datei „unattend.xml“.  

2. Lädt das Paket herunter, das den Configuration Manager-Client enthält. Fügt das Paket zum bereitgestellten Image hinzu.  

#### <a name="set-up-windows"></a>Einrichten von Windows  

- Imagebasierte Installation  

    1. Deaktivieren Sie den Configuration Manager-Client im Image, falls dieser vorhanden ist. Deaktivieren Sie also den automatischen Start für den Configuration Manager-Clientdienst.  

    2. Aktualisieren Sie die Registrierung im bereitgestellten Image, um das bereitgestellte Betriebssystem mit dem gleichen Laufwerkbuchstaben wie der Referenzcomputer zu starten.  

    3. Führen Sie einen Neustart für das bereitgestellte Betriebssystem aus.  

    4. Die Windows-Miniinstallation wird unter Verwendung der zuvor angegebenen Antwortdatei „sysprep.inf“ oder „unattend.xml“ ausgeführt. Bei diesem Vorgang werden alle Interaktionen mit Benutzern unterdrückt. Wenn Sie den Schritt **Netzwerkeinstellungen anwenden** verwenden, um eine Verknüpfung mit einer Domäne zu erstellen, befindet sich diese Information in der Antwortdatei. Die Windows-Miniinstallation verknüpft den Computer mit der Domäne.  

- Setup.exe-basierte Installation. Führt „Setup.exe“ aus. Dieser Vorgang entspricht dem normalen Windows-Installationsprozess:  

    1. Kopieren Sie das Betriebssystemupgradepaket, das im Schritt **Betriebssystem anwenden** angegeben wurde, auf das Festplattenlaufwerk.  

    2. Führen Sie einen Neustart für das neu bereitgestellte Betriebssystem aus.  

    3. Die Windows-Miniinstallation wird unter Verwendung der zuvor angegebenen Antwortdatei „sysprep.inf“ oder „unattend.xml“ ausgeführt. Bei diesem Vorgang werden alle Einstellungen der Benutzeroberfläche unterdrückt. Wenn Sie den Schritt **Netzwerkeinstellungen anwenden** verwenden, um eine Verknüpfung mit einer Domäne zu erstellen, befindet sich diese Information in der Antwortdatei. Die Windows-Miniinstallation verknüpft den Computer mit der Domäne.  

#### <a name="set-up-the-configuration-manager-client"></a>Einrichten des Configuration Manager-Clients  

1. Nachdem die Windows-Miniinstallation abgeschlossen ist, wird die Tasksequenz mithilfe von „setupcomplete.cmd“ fortgesetzt. Weitere Informationen finden Sie unter [Ausführen eines Skripts nach Abschluss des Setups (SetupComplete.cmd)](/windows-hardware/manufacture/desktop/add-a-custom-script-to-windows-setup#run-a-script-after-setup-is-complete-setupcompletecmd).  

2. Aktivieren oder deaktivieren Sie das lokale Administratorkonto gemäß der in Schritt **Windows-Einstellungen anwenden** ausgewählten Option.  

3. Installieren Sie den Configuration Manager-Client mithilfe des zuvor heruntergeladenen Downloadpakets und der in diesem Schritt angegebenen Installationseigenschaften. Der Client wird im „Bereitstellungsmodus“ installiert. So muss der Client keine neuen Richtlinienanforderungen verarbeiten, bevor die Tasksequenz abgeschlossen ist. Weitere Informationen finden Sie unter [Provisioning mode (Bereitstellungsmodus)](provisioning-mode.md).  

4. Warten Sie, bis der Client voll funktionstüchtig ist.  

#### <a name="the-step-completes"></a>Schritt wird abgeschlossen

Die Tasksequenz fährt mit der Ausführung des nächsten Schritts fort.  

> [!Note]  
> Die Windows-Gruppenrichtlinie wird in der Regel erst nach Abschluss der Tasksequenz verarbeitet. Dieses Verhalten ist unabhängig von der Windows-Version. Die Gruppenrichtlinienauswertung kann durch andere benutzerdefinierte Aktionen während der Tasksequenz ausgelöst werden. Weitere Informationen zur Reihenfolge der Vorgänge finden Sie unter [Ausführen eines Skripts nach Abschluss des Setups (SetupComplete.cmd)](/windows-hardware/manufacture/desktop/add-a-custom-script-to-windows-setup#run-a-script-after-setup-is-complete-setupcompletecmd). <!-- 2841304 -->


### <a name="variables-for-setup-windows-and-configmgr"></a>Variablen für „Windows und Konfigurations-Manager einrichten“

Verwenden Sie die folgenden Tasksequenzvariablen in diesem Schritt:  

- [SMSClientInstallProperties](task-sequence-variables.md#SMSClientInstallProperties)  

### <a name="cmdlets-for-setup-windows-and-configmgr"></a>Cmdlets für „Windows und Konfigurations-Manager einrichten“

Verwalten Sie diesen Schritt mit den folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepSetupWindowsAndConfigMgr](/powershell/module/configurationmanager/get-cmtsstepsetupwindowsandconfigmgr)
- [New-CMTSStepSetupWindowsAndConfigMgr](/powershell/module/configurationmanager/new-cmtsstepsetupwindowsandconfigmgr)
- [Remove-CMTSStepSetupWindowsAndConfigMgr](/powershell/module/configurationmanager/remove-cmtsstepsetupwindowsandconfigmgr)
- [Set-CMTSStepSetupWindowsAndConfigMgr](/powershell/module/configurationmanager/set-cmtsstepsetupwindowsandconfigmgr)

### <a name="properties-for-setup-windows-and-configmgr"></a>Eigenschaften für „Windows und Konfigurations-Manager einrichten“

Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

#### <a name="client-package"></a>Clientpaket

Wählen Sie **Durchsuchen** und dann das Installationspaket für den Configuration Manager-Client aus, das in diesem Schritt verwendet werden soll.  

#### <a name="use-pre-production-client-package-when-available"></a>Präproduktionsclient-Paket bei Verfügbarkeit verwenden

Wenn ein Präproduktions-Clientpaket verfügbar und der Computer Mitglied der Pilotsammlung ist, verwendet die Tasksequenz dieses Paket statt des Produktionsclientpakets. Bei einem Präproduktionsclient handelt es sich um eine neuere Version für das Testen in der Produktionsumgebung. Wählen Sie **Durchsuchen** und dann das Präproduktions-Clientpaket aus, das in diesem Schritt verwendet werden soll.  

#### <a name="installation-properties"></a>Installationseinstellungen

Der Tasksequenzschritt gibt die Standortzuweisung und die Standardkonfiguration automatisch an. Verwenden Sie dieses Feld, um zusätzliche Installationseigenschaften anzugeben, die bei der Clientinstallation verwendet werden sollen. Wenn sie mehrere Installationseigenschaften eingeben möchten, müssen Sie sie durch ein Leerzeichen trennen.  

Geben Sie Befehlszeilenoptionen für die Clientinstallation an. Geben Sie beispielsweise `/skipprereq: silverlight.exe` ein, um „CCMSetup.exe“ anzuweisen, die Voraussetzungen für Microsoft Silverlight nicht zu installieren. Weitere Informationen zu diesen Befehlszeileneigenschaften für CCMSetup.exe finden Sie unter [Informationen zu Clientinstallationseigenschaften](../../core/clients/deploy/about-client-installation-properties.md).  

Wenn Sie eine Tasksequenz zum Bereitstellen eines Betriebssystems auf einem internetbasierten Client ausführen, der entweder in Azure AD eingebunden ist oder die tokenbasierte Authentifizierung verwendet, müssen Sie die Eigenschaft [CCMHOSTNAME](../../core/clients/deploy/about-client-installation-properties.md#ccmhostname) im Schritt **Windows und ConfigMgr einrichten** angeben. Beispiel: `CCMHOSTNAME=OTTERFALLS.CLOUDAPP.NET/CCM_Proxy_MutualAuth/12345678907927939`.

### <a name="options-for-setup-windows-and-configmgr"></a>Optionen für „Windows und Konfigurations-Manager einrichten“

> [!NOTE]  
> Aktivieren Sie auf der Registerkarte **Optionen** nicht **Bei Fehler fortsetzen**. Wenn bei diesem Schritt ein Fehler auftritt, schlägt die Tasksequenz fehl – unabhängig davon, ob diese Einstellung aktiviert ist.  



## <a name="upgrade-operating-system"></a><a name="BKMK_UpgradeOS"></a> Betriebssystem aktualisieren

Verwenden Sie diesen Schritt, um ein Upgrade einer älteren Version von Windows auf eine neuere Version von Windows 10 durchzuführen.  

Dieser Tasksequenzschritt wird nur in der Vollversion des Betriebssystems ausgeführt. Er kann nicht in Windows PE ausgeführt werden.  

Um diesen Schritt im Tasksequenz-Editor hinzuzufügen, wählen Sie **Hinzufügen**, **Images** und dann **Betriebssystem aktualisieren** aus.

> [!TIP]
> Ab Windows 10 (Version 1709) enthalten Medien mehrere Editionen. Wenn Sie eine Tasksequenz konfigurieren, um ein Betriebssystemupgradepaket oder ein Betriebssystemimage zu verwenden, achten Sie darauf, eine [unterstützte Edition](../../core/plan-design/configs/support-for-windows-10.md#windows-10-as-a-client) auszuwählen.  
>
> Verwenden Sie ein vorgeschaltetes Zwischenspeichern für Inhalte, um ein geeignetes Betriebssystemupgradepaket herunterzuladen, bevor ein Benutzer die Tasksequenz installiert. Weitere Informationen finden Sie unter [Konfigurieren des zwischengespeicherten Inhalts](../deploy-use/configure-precache-content.md).

### <a name="variables-for-upgrade-os"></a>Variablen für „Betriebssystem aktualisieren“

Verwenden Sie die folgenden Tasksequenzvariablen in diesem Schritt:  

- [_SMSTSOSUpgradeActionReturnCode](task-sequence-variables.md#SMSTSOSUpgradeActionReturnCode)  
- [SetupCompletePause](task-sequence-variables.md#SetupCompletePause)
- [OSDSetupAdditionalUpgradeOptions](task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions)  

### <a name="cmdlets-for-upgrade-os"></a>Cmdlets für „Betriebssystem aktualisieren“

Verwalten Sie diesen Schritt mit den folgenden PowerShell-Cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepUpgradeOperatingSystem](/powershell/module/configurationmanager/Get-CMTSStepUpgradeOperatingSystem)
- [New-CMTSStepUpgradeOperatingSystem](/powershell/module/configurationmanager/New-CMTSStepUpgradeOperatingSystem)
- [Remove-CMTSStepUpgradeOperatingSystem](/powershell/module/configurationmanager/Remove-CMTSStepUpgradeOperatingSystem)
- [Set-CMTSStepUpgradeOperatingSystem](/powershell/module/configurationmanager/Set-CMTSStepUpgradeOperatingSystem)

### <a name="properties-for-upgrade-os"></a>Eigenschaften für „Betriebssystem aktualisieren“

Konfigurieren Sie die in diesem Abschnitt beschriebenen Einstellungen auf der Registerkarte **Eigenschaften** für diesen Schritt.  

#### <a name="upgrade-package"></a>Upgradepaket

Wählen Sie diese Option aus, um das zu verwendende Paket für das Windows 10-Betriebssystemupgrade anzugeben.  

#### <a name="source-path"></a>Quellpfad

Gibt einen lokalen Pfad oder einen Netzwerkpfad für die Windows 10-Medien an, die Windows Setup verwendet. Diese Einstellung entspricht der Windows Setup-Befehlszeilenoption `/InstallFrom`.

Sie können auch eine Variable angeben, z.B. `%MyContentPath%` oder `%DPC01%`. Wenn Sie eine Variable für den Quellpfad verwenden, legen Sie ihren Wert zuvor in der Tasksequenz fest. Verwenden Sie beispielsweise den Schritt [Paketinhalt herunterladen](#BKMK_DownloadPackageContent), um eine Variable für den Speicherort des Betriebssystemupgrade-Pakets anzugeben. Verwenden Sie diese Variable dann für den Quellpfad für diesen Schritt.  

#### <a name="edition"></a>Edition

Geben Sie die für das Upgrade zu verwendende Edition in den Betriebssystemmedien an.  

#### <a name="product-key"></a>Product Key

Geben Sie den auf das Upgrade anzuwendenden Product Key an.  

#### <a name="provide-the-following-driver-content-to-windows-setup-during-upgrade"></a>Windows Setup während des Upgrades folgenden Treiberinhalt bereitstellen

Fügt während des Upgradevorgangs Treiber auf dem Zielcomputer hinzu. Die Treiber müssen mit Windows 10 kompatibel sein. Diese Einstellung entspricht der Windows Setup-Befehlszeilenoption `/InstallDriver`. Weitere Informationen finden Sie unter [Windows Setup-Befehlszeilenoptionen](/windows-hardware/manufacture/desktop/windows-setup-command-line-options#installdrivers).

Geben Sie eine der folgenden Optionen an:  

- **Treiberpaket**: Wählen Sie **Durchsuchen** und ein vorhandenes Treiberpaket aus der Liste aus.

- **Bereitgestellter Inhalt**: Wählen Sie diese Option aus, um den Speicherort für die Treiberinhalte anzugeben. Sie können einen lokalen Ordner, einen Netzwerkpfad oder eine Tasksequenzvariable angeben. Wenn Sie eine Variable für den Quellpfad verwenden, legen Sie ihren Wert zuvor in der Tasksequenz fest. Verwenden Sie dazu beispielsweise den Schritt [Paketinhalt herunterladen](task-sequence-steps.md#BKMK_DownloadPackageContent).  

> [!TIP]
> Wenn Sie dynamische Inhalte für verschiedene Hardwaretypen verwenden möchten, führen Sie Folgendes aus:
>
> - Verwenden Sie mehrere Instanzen dieses Schritts mit Bedingungen für Hardwaretypen und eigenen Treiberinhalten.
>
> - Verwenden Sie mehrere Instanzen des Schritts [Paketinhalt herunterladen](task-sequence-steps.md#BKMK_DownloadPackageContent). Speichern Sie die Inhalte an einem häufig verwendeten Speicherort, und verwenden Sie dann die Option **bereitgestellter Inhalt**. Der Vorteil dieser Methode besteht darin, dass die Tasksequenz über einen einzelnen **Betriebssystem aktualisieren**-Schritt verfügt.

#### <a name="time-out-minutes"></a>Timeout (Minuten)

Geben Sie die Anzahl von Minuten an, bevor Configuration Manager diesen Schritt als fehlgeschlagen wertet. Diese Option ist nützlich, wenn Windows Setup die Verarbeitung stoppt, aber nicht beendet wird.  

#### <a name="perform-windows-setup-compatibility-scan-without-starting-upgrade"></a>Ausführen einer Windows Setup-Kompatibilitätsüberprüfung ohne Starten des Upgrades

Führt die Kompatibilitätsprüfung für Windows Setup durch, ohne den Upgradevorgang zu starten. Diese Einstellung entspricht der Windows Setup-Befehlszeilenoption `/Compat ScanOnly`. Stellen Sie das gesamte Betriebssystemupgrade-Paket mit dieser Option bereit.

<!--SCCMDocs-pr issue 2812-->
Wenn Sie diese Option aktivieren, versetzt dieser Schritt den Configuration Manager-Client nicht in den Bereitstellungsmodus. Windows-Setup wird im Hintergrund und der Client weiterhin standardmäßig ausgeführt. Weitere Informationen finden Sie unter [Provisioning mode (Bereitstellungsmodus)](provisioning-mode.md).

Setup gibt als Ergebnis der Überprüfung einen Exitcode zurück. Die folgende Tabelle enthält einige der gängigsten Exitcodes:  

|Exitcode|Details|  
|-|-|  
|MOSETUP_E_COMPAT_SCANONLY (0xC1900210)|Keine Kompatibilitätsprobleme (Erfolg).|  
|MOSETUP_E_COMPAT_INSTALLREQ_BLOCK (0xC1900208)|Kompatibilitätsprobleme mit Handlungsbedarf.|  
|MOSETUP_E_COMPAT_MIGCHOICE_BLOCK (0xC1900204)|Die ausgewählte Migrationsoption ist nicht verfügbar. z. B. Enterprise zu Professional.|  
|MOSETUP_E_COMPAT_SYSREQ_BLOCK (0xC1900200)|Nicht für Windows 10 geeignet.|  
|MOSETUP_E_COMPAT_INSTALLDISKSPACE_BLOCK (0xC190020E)|Nicht genügend freier Speicherplatz.|  

Weitere Informationen zu diesem Parameter finden Sie unter [Windows Setup-Befehlszeilenoptionen](/windows-hardware/manufacture/desktop/windows-setup-command-line-options#compat).  

#### <a name="ignore-any-dismissible-compatibility-messages"></a>Alle Kompatibilitätsmeldungen, die verworfen werden können, ignorieren

Gibt an, dass das Setup die Installation abschließt und dabei alle vernachlässigbaren Kompatibilitätsmeldungen ignoriert. Diese Einstellung entspricht der Windows Setup-Befehlszeilenoption `/Compat IgnoreWarning`.  

#### <a name="dynamically-update-windows-setup-with-windows-update"></a>Windows Setup dynamisch mit Windows Update aktualisieren

Ermöglicht, dass das Setup dynamische Updatevorgänge durchführt, z.B. das Suchen, Herunterladen und Installieren von Updates. Diese Einstellung entspricht der Windows Setup-Befehlszeilenoption `/DynamicUpdate`. Diese Einstellung ist nicht mit Configuration Manager-Softwareupdates kompatibel. Aktivieren Sie diese Option, wenn Sie Updates mit eigenständigen Versionen von Windows Server Update Services (WSUS) oder Windows Update for Business verwalten.  

#### <a name="override-policy-and-use-default-microsoft-update"></a>Richtlinie überschreiben und Standard-Microsoft-Update verwenden

Die lokale Richtlinie wird vorübergehend in Echtzeit überschrieben, damit dynamische Updatevorgänge ausgeführt werden. Der Computer ruft Updates über Windows Update ab.
