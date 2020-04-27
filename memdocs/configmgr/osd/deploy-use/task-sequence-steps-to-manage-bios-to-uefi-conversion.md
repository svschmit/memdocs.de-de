---
title: Tasksequenzschritte für das Verwalten einer Konvertierung von BIOS zu UEFI
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über das Anpassen einer Betriebssystembereitstellungs-Tasksequenz, um eine FAT32-Partition auf die Konvertierung zu UEFI vorzubereiten.
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9183efd622cb425027500d3fe51ed7b86d3a94e4
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079364"
---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Tasksequenzschritte für das Verwalten einer Konvertierung von BIOS zu UEFI
Windows 10 bietet viele neue Sicherheitsfunktionen, die UEFI-fähige Geräte erfordern. Möglicherweise verfügen Sie über moderne Windows-PCs, die UEFI unterstützen, aber das Legacy-BIOS verwenden. Wenn Sie ein Geräte zu UEFI konvertieren wollten, mussten Sie auf jedem PC die Festplatte neu formatieren und die Firmware neu konfigurieren. Mithilfe von Tasksequenzen in Configuration Manager können Sie eine Festplatte für die BIOS UEFI-Konvertierung vorbereiten, von BIOS in UEFI als Teil des direkten Upgrades konvertieren und UEFI-Informationen als Teil der Hardwareinventur sammeln.

## <a name="hardware-inventory-collects-uefi-information"></a>Die Hardwareinventur sammelt UEFI-Informationen
Ihnen stehen eine neue Hardwareinventurklasse (**SMS_Firmware**) und eine neue Eigenschaft (**UEFI**) ab Version 1702 zur Verfügung, mit der Sie bestimmen können, ob ein Computer im UEFI-Modus startet. Wenn ein Computer im UEFI-Modus gestartet wird, ist die Eigenschaft **UEFI** auf **TRUE** festgelegt. Dies ist bei der Hardwareinventur standardmäßig aktiviert. Weitere Informationen zur Hardwareinventur finden Sie unter [How to configure hardware inventory (Konfigurieren der Hardwareinventur)](../../core/clients/manage/inventory/configure-hardware-inventory.md).

## <a name="create-a-custom-task-sequence-to-prepare-the-hard-drive-for-bios-to-uefi-conversion"></a>Erstellen Sie eine benutzerdefinierte Tasksequenz zur Vorbereitung der Festplatte für die Konvertierung von BIOS zu UEFI
In Configuration Manager Version 1610 können Sie eine Tasksequenz einer Betriebssystembereitstellung nun mit der neuen Variablen „TSUEFIDrive“ so anpassen, dass durch den Schritt **Computer neu starten** auf der Festplatte eine FAT32-Partition für die Konvertierung zu UEFI vorbereitet wird. Das folgende Verfahren stellt ein Beispiel dar, wie Sie Tasksequenzschritte erstellen können, um die Festplatte auf die Konvertierung von BIOS zu UEFI vorzubereiten.

### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>So bereiten Sie die FAT32-Partition für die Konvertierung zu UEFI vor:
Fügen Sie in einer vorhandenen Tasksequenz zum Installieren eines Betriebssystems eine neue Gruppe mit Schritten zum Konvertieren von BIOS zu UEFI hinzu.

1. Erstellen Sie eine neue Tasksequenzgruppe nach den Schritten zum Erfassen von Dateien und Einstellungen und vor den Schritten zum Installieren des Betriebssystems. Erstellen Sie z.B. eine Gruppe nach der Gruppe **Dateien und Einstellungen erfassen** namens **BIOS zu UEFI**.
2. Fügen Sie auf der Registerkarte **Optionen** der neuen Gruppe eine neue Tasksequenzvariable als Bedingung hinzu, wobei **_SMSTSBootUEFI** **ungleich** **TRUE** ist. Dadurch wird verhindert, dass die Schritte in der Gruppe ausgeführt werden, wenn sich ein Computer bereits im UEFI-Modus befindet.

   ![Gruppe „BIOS zu UEFI“](../../core/get-started/media/BIOS-to-UEFI-group.png)
3. Fügen Sie der neuen Gruppe den Tasksequenzschritt **Computer neu starten** hinzu. Wählen Sie unter **Geben Sie an, was nach dem Neustart ausgeführt werden soll** **The boot image assigned to this task sequence is selected** (Das dieser Tasksequenz zugewiesene Startimage wird ausgewählt) aus, um den Computer in Windows PE zu starten.  
4. Fügen Sie auf der Registerkarte **Optionen** eine Tasksequenzvariable als Bedingung hinzu, wobei **_SMSTSInWinPE ist gleich FALSE**. Dadurch wird verhindert, dass dieser Schritt ausgeführt, wenn sich der Computer bereits in Windows PE befindet.

   ![Schritt „Computer neu starten“](../../core/get-started/media/restart-in-windows-pe.png)
5. Fügen Sie einen Schritt zum Starten des OEM-Tools hinzu, das die Firmware von BIOS in UEFI konvertiert. Dabei handelt es sich normalerweise um einen Tasksequenzschritt **Befehlszeile ausführen** mit einer Befehlszeile zum Starten des OEM-Tools.
6. Fügen Sie den Tasksequenzschritt „Datenträger formatieren und partitionieren“ hinzu, durch den die Festplatte formatiert und partitioniert wird. Führen Sie im Schritt Folgendes aus:
   1. Erstellen Sie die FAT32-Partition, die in UEFI konvertiert wird, bevor das Betriebssystem installiert wird. Wählen Sie **GPT** als **Datenträgertyp** aus.
    ![Schritt „Datenträger formatieren und partitionieren“](../media/format-and-partition-disk.png)
   2. Wechseln Sie zu den Eigenschaften für die FAT32-Partition. Geben Sie **TSUEFIDrive** in das Feld **Variable** ein. Wenn diese Variable von der Tasksequenz erkannt wird, wird diese sich vor dem Neustart des Computers auf den Übergang zu UEFI vorbereiten.
    ![Partitionseigenschaften](../../core/get-started/media/partition-properties.png)
   3. Erstellen Sie eine NTFS-Partition, die von der Tasksequenz-Engine verwendet wird, um dessen Zustand sowie Protokolldateien zu speichern.
7. Fügen Sie den Tasksequenzschritt **Computer neu starten** hinzu. Wählen Sie unter **Geben Sie an, was nach dem Neustart ausgeführt werden soll** **The boot image assigned to this task sequence is selected** (Das dieser Tasksequenz zugewiesene Startimage wird ausgewählt) aus, um den Computer in Windows PE zu starten.  

## <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Konvertieren von BIOS zu UEFI während eines direkten Upgrades
Windows 10 Creators Update führt ein einfaches Konvertierungstool ein, womit der Prozess der Neupartitionierung der Festplatte für UEFI-aktivierte Hardware automatisiert werden kann und das Konvertierungstool in den direkten Upgradeprozess von Windows 7 zu Windows 10 integriert werden kann. Wenn Sie dieses Tool mit Ihrer Tasksequenz des Betriebssystemupgrades und dem OEM-Tool kombinieren, der die Firmware von BIOS zu UEFI konvertiert, können Sie Ihre Computer von BIOS zu UEFI während eines direkten Upgrades zu Windows 10 Creators Update konvertieren.

**Anforderungen**:
- Windows 10 Creators Update
- Computer, die UEFI unterstützen
- OEM-Tool, das die Firmware des Computers vom BIOS zu UEFI konvertiert

### <a name="to-convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Konvertieren von BIOS zu UEFI während eines direkten Upgrades
1. Erstellen Sie eine Tasksequenz für ein Betriebssystemupgrade, die ein direktes Upgrade auf Windows 10 Creators Update durchführt.
2. Bearbeiten Sie die Tasksequenz. Fügen Sie diese zusätzlichen Tasksequenzschritte in der **Nachbearbeitungsgruppe** hinzu.
   1. Fügen Sie den Schritt **Befehlszeile ausführen** unter „Allgemein“ hinzu. Sie werden die Befehlszeile für das MBR2GPT-Tool hinzufügen, das einen Datenträger von MBR zu GPT konvertiert, ohne Daten zu ändern oder vom Datenträger zu löschen. Geben Sie Folgendes in die Befehlszeile ein:  **MBR2GPT /convert /disk:0 /AllowFullOS**. Sie können auch das MBR2GPT.EXE-Tool ausführen, wenn Sie sich unter Windows PE statt in der Vollversion des Betriebssystems befinden. Sie können dazu einen Schritt vor dem Schritt zum Ausführen des MBR2GPT.EXE-Tools zum Neustart des Computers zu WinPE hinzufügen und die /AllowFullOS-Option aus der Befehlszeile entfernen. Weitere Informationen über das Tool und die verfügbaren Optionen finden Sie unter [MBR2GPT.EXE](https://technet.microsoft.com/itpro/windows/deploy/mbr-to-gpt).
   2. Fügen Sie einen Schritt zum Starten des OEM-Tools hinzu, das die Firmware von BIOS in UEFI konvertiert. Dabei handelt es sich normalerweise um einen Tasksequenzschritt „Befehlszeile ausführen“ mit einer Befehlszeile zum Starten des OEM-Tools.
   3. Fügen Sie den Schritt **Computer neu starten** unter „Allgemein“ hinzu. Für „Geben Sie an, was nach dem Neustart ausgeführt werden soll“, wählen Sie **Aktuell installiertes Standardbetriebssystem** aus.
3. Bereitstellen der Tasksequenz
