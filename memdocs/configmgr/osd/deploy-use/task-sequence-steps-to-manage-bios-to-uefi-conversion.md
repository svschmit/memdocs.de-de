---
title: Konvertieren von BIOS zu UEFI
titleSuffix: Configuration Manager
description: In diesem Artikel erfahren Sie, wie Sie eine Tasksequenz zum Bereitstellen eines Betriebssystems anpassen, um eine FAT32-Partition auf die Konvertierung zu UEFI vorzubereiten.
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 761270fe9419330e2d60d0483554ee6c932c1b26
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124884"
---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Tasksequenzschritte für das Verwalten einer Konvertierung von BIOS zu UEFI

Windows 10 bietet viele neue Sicherheitsfunktionen, die UEFI-fähige Geräte erfordern. Möglicherweise verfügen Sie über neuere Windows-Geräte, die UEFI unterstützen, aber das Legacy-BIOS verwenden. Wenn früher ein Geräte zu UEFI konvertieren werden sollte, mussten Sie auf jedem Gerät die Festplatte neu partitionieren und die Firmware neu konfigurieren.

Dank Configuration Manager haben Sie die Möglichkeit, die folgenden Aktionen zu automatisieren:

- Vorbereiten einer Festplatte für die Konvertierung von BIOS zu UEFI
- Konvertieren von BIOS zu UEFI im Rahmen von direkten Upgrades
- Sammeln von UEFI-Informationen im Rahmen der Hardwareinventur

## <a name="hardware-inventory-collects-uefi-information"></a>Die Hardwareinventur sammelt UEFI-Informationen

Die Hardwareinventurklasse (**SMS_Firmware**) und die Hardwareinventureigenschaft (**UEFI**) sollen Ihnen helfen zu erkennen, ob ein Computer im UEFI-Modus startet. Wenn ein Computer im UEFI-Modus gestartet wird, ist die Eigenschaft **UEFI** auf **TRUE** festgelegt. In der Hardwareinventur ist diese Einstellung standardmäßig aktiviert. Weitere Informationen zur Hardwareinventur finden Sie unter [How to configure hardware inventory (Konfigurieren der Hardwareinventur)](../../core/clients/manage/inventory/configure-hardware-inventory.md).

## <a name="create-a-custom-task-sequence-to-prepare-the-hard-drive"></a>Erstellen einer benutzerdefinierten Tasksequenz zur Vorbereitung der Festplatte

Sie können eine Tasksequenz für die Bereitstellung eines Betriebssystem mit der Variable **TSUEFIDrive** anpassen. Im Schritt **Computer neu starten** wird eine FAT32-Partition auf der Festplatte für die Konvertierung zu UEFI vorbereitet. Das folgende Verfahren zeigt exemplarisch, wie Sie Tasksequenzschritte erstellen, um diese Aktion auszuführen.

### <a name="prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>Vorbereiten der FAT32-Partition für die Konvertierung zu UEFI

Fügen Sie in einer vorhandenen Tasksequenz zum Installieren eines Betriebssystems eine neue Gruppe mit Schritten zum Konvertieren von BIOS zu UEFI hinzu.

1. Erstellen Sie eine neue Tasksequenzgruppe nach den Schritten zum Erfassen von Dateien und Einstellungen und vor den Schritten zum Installieren des Betriebssystems. Erstellen Sie z.B. eine Gruppe nach der Gruppe **Dateien und Einstellungen erfassen** namens **BIOS zu UEFI**.

1. Fügen Sie auf der Registerkarte **Optionen** der neuen Gruppe eine neue Tasksequenzvariable als Bedingung hinzu. Legen Sie sie auf **_SMSTSBootUEFI not equal true** fest. Mit dieser Bedingung führt die Tasksequenz diese Schritte nur auf BIOS-Geräten aus.

    :::image type="content" source="media/bios-to-uefi-group.png" alt-text="Bedingung in der Gruppe „BIOS-to-UEFI“":::

1. Fügen Sie der neuen Gruppe den Tasksequenzschritt **Computer neu starten** hinzu. Wählen Sie unter **Geben Sie an, was nach dem Neustart ausgeführt werden soll** die Option **The boot image assigned to this task sequence is selected** (Das Startimage ist ausgewählt, das dieser Tasksequenz zugewiesen ist) aus. Durch diese Aktion wird der Computers in Windows PE neu gestartet.

1. Fügen Sie auf der Registerkarte **Optionen** eine Tasksequenzvariable als Bedingung hinzu. Legen Sie sie auf **_SMSTSInWinPE equals false** fest. Mit dieser Bedingung führt die Tasksequenz diesen Schritt nicht aus, wenn auf dem Computer bereits Windows PE ausgeführt wird.

    :::image type="content" source="media/restart-in-windows-pe.png" alt-text="Bedingung im Schritt „Computer neu starten“":::

1. Fügen Sie einen Schritt zum Starten des OEM-Tools hinzu, das die Firmware von BIOS zu UEFI konvertiert. Dabei handelt es sich üblicherweise um den Schritt **Befehlszeile ausführen**, der den Befehl zum Ausführen des OEM-Tools enthält.

1. Fügen Sie den Tasksequenzschritt **Datenträger formatieren und partitionieren** hinzu. Konfigurieren Sie in diesem Schritt die folgenden Optionen:

    1. Erstellen Sie die FAT32-Partition, um vor der Installation des Betriebssystems die Konvertierung zu UEFI auszuführen. Wählen Sie **GPT** als **Datenträgertyp** aus.

        :::image type="content" source="media/format-and-partition-disk.png" alt-text="Konfiguration des Schritts „Datenträger formatieren und partitionieren“":::

    1. Wechseln Sie zu den Eigenschaften für die FAT32-Partition. Geben Sie in das Feld **Variable** den Wert `TSUEFIDrive` ein. Wenn die Tasksequenz diese Variable erkennt, wird die Partition auf den Wechsel zu UEFI vorbereitet, bevor der Computer neu gestartet wird.

        :::image type="content" source="media/partition-properties.png" alt-text="Konfiguration der Eigenschaften der FAT32-Partition":::

    1. Erstellen Sie eine NTFS-Partition, die von der Tasksequenz verwendet wird, um ihren Zustand und die Protokolldateien zu speichern.

1. Fügen Sie einen weiteren Tasksequenzschritt **Computer neu starten** hinzu. Wählen Sie unter **Geben Sie an, was nach dem Neustart ausgeführt werden soll** **The boot image assigned to this task sequence is selected** (Das dieser Tasksequenz zugewiesene Startimage wird ausgewählt) aus, um den Computer in Windows PE zu starten.

    > [!TIP]
    > Die Standardgröße von EFI-Partitionen beträgt 500 MB. In einigen Umgebungen ist das Startimage zu groß, um auf dieser Partition gespeichert zu werden. Dieses Problem lässt sich umgehen, indem Sie die Größe der EFI-Partition hochsetzen. Legen Sie diese z. B. auf 1 GB fest.<!-- SCCMDocs#1024 -->

## <a name="convert-from-bios-to-uefi-during-in-place-upgrade"></a><a name="bkmk_ipu"></a> Konvertieren von BIOS zu UEFI während eines direkten Upgrades

Windows 10 enthält ein einfaches Konvertierungstool: **MBR2GPT**. Es automatisiert die Neupartitionierung der Festplatte für UEFI-fähige Hardware. Sie können das Konvertierungstool in den direkten Upgradeprozess in Windows 10 integrieren. Kombinieren Sie es einfach mit der Upgradetasksequenz und dem OEM-Tool, das die Firmware von BIOS zu UEFI konvertiert.

### <a name="requirements"></a>Anforderungen

- Eine unterstützte Version von Windows 10
- Computer, die UEFI unterstützen
- OEM-Tool, das die Firmware des Computers vom BIOS zu UEFI konvertiert

### <a name="process-to-convert-from-bios-to-uefi-during-an-in-place-upgrade-task-sequence"></a>Konvertieren von BIOS zu UEFI während einer direkten Upgradetasksequenz

1. [Erstellen einer Tasksequenz zum Durchführen eines Betriebssystemupgrades](create-a-task-sequence-to-upgrade-an-operating-system.md)

1. Bearbeiten Sie die Tasksequenz. Nehmen Sie in der Gruppe **Nachbearbeitung** die folgenden Änderungen vor:

    1. Fügen Sie den Schritt **Befehlszeile ausführen** hinzu. Geben Sie die Befehlszeile für das Tool MBR2GPT an. Wenn Sie sich in der Vollversion des Betriebssystems befinden, konfigurieren Sie es so, dass der Datenträger vom MBR- ins GPT-Format konvertiert wird, ohne dass Daten geändert werden Geben Sie unter **Befehlszeile** den folgenden Befehl ein: `MBR2GPT.exe /convert /disk:0 /AllowFullOS`.

    > [!TIP]
    > Sie können das Tool MBR2GPT.EXE auch ausführen, wenn Sie sich unter Windows PE statt in der Vollversion des Betriebssystems befinden. Fügen Sie vor dem Schritt zum Ausführen von MBR2GPT einen Schritt hinzu, mit dem der Computer in Windows PE neu gestartet wird. Entfernen Sie dann die Option **/AllowFullOS** aus der Befehlszeile.

    Weitere Informationen über das Tool und die verfügbaren Optionen finden Sie unter [MBR2GPT.EXE](https://docs.microsoft.com/windows/deployment/mbr-to-gpt).

    1. Fügen Sie einen Schritt zum Ausführen des OEM-Tools hinzu, das die Firmware von BIOS in UEFI konvertiert. Dabei handelt es sich üblicherweise um den Schritt **Befehlszeile ausführen**, der eine Befehlszeile zum Ausführen des OEM-Tools enthält.

    1. Fügen Sie den Schritt **Computer neu starten** hinzu, und wählen Sie **Aktuell installiertes Standardbetriebssystem** aus.

1. Bereitstellen der Tasksequenz
