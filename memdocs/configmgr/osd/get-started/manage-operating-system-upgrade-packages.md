---
title: Verwalten von Betriebssystemupgradepaketen
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Betriebssystemupgradepakete in Configuration Manager verwalten können.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: b9b22655-b8c1-461f-8047-3a7e906f647a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a50592815ed4581c01489f90b6c3701e53bb4981
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124413"
---
# <a name="manage-os-upgrade-packages-with-configuration-manager"></a>Verwalten von Betriebssystemupgradepaketen mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Ein Betriebssystemupgradepaket in Configuration Manager enthält die Windows-Setupquelldateien für das Upgrade eines vorhandenen Betriebssystems auf einem Computer. In diesem Artikel wird beschrieben, wie ein Betriebssystemupgradepaket hinzugefügt, verteilt und gewartet wird.

> [!NOTE]
> Betriebssystemupgradepakete können auch für neue Installationen von Windows verwendet werden. Dies hängt jedoch davon ab, ob die Treiber mit dieser Methode kompatibel sind. Bei Neuinstallationen von Windows aus einem Betriebssystemupgradepaket werden die Treiber installiert und nicht einfach eingefügt, während noch die Windows-Vorinstallationsumgebung (Windows PE) ausgeführt wird. Einige Treiber sind jedoch nicht kompatibel mit der Installation in Windows PE. Wenn Treiber mit der Installation in Windows PE nicht kompatibel sind, verwenden Sie stattdessen ein [Betriebssystemabbild](manage-operating-system-images.md) (z. B. **install.wim**).

## <a name="add-an-os-upgrade-package"></a><a name="BKMK_AddOSUpgradePkgs"></a> Hinzufügen eines Betriebssystemupgradepakets  

Bevor Sie ein Betriebssystemupgradepaket verwenden können, fügen Sie es zunächst Ihrem Configuration Manager-Standort hinzu.

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und wählen Sie anschließend den Knoten **Betriebssystemaktualisierungspakete** aus.  

2. Klicken Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Erstellen** auf **Aktualisierungspaket für Betriebssysteme hinzufügen**. Dadurch wird der Assistent zum Hinzufügen des Upgrades für Betriebssysteme gestartet.  

3. Geben Sie auf der Seite **Datenquelle** die folgenden Einstellungen an:

    - Den **Netzwerkpfad** zu den Installationsquelldateien des Betriebssystemupgradepakets. Beispiel: `\\server\share\path`.  

        > [!NOTE]  
        >  Zu den Installationsquelldateien gehören „Setup.exe“ sowie andere Dateien und Ordner zum Installieren des Betriebssystems.  

        > [!IMPORTANT]  
        >  Schränken Sie den Zugriff auf die Installationsquelldateien ein, um unerwünschte Manipulationen zu verhindern.  

    - **Extrahieren Sie einen Index für ein bestimmtes Image aus der install.wim-Datei des ausgewählten Upgradepakets**, und wählen Sie einen Imageindex aus der Liste aus.<!--4931110--> Ab Version 1910 importiert diese Option automatisch einen einzelnen Index, anstatt alle Imageindizes in die Datei zu importieren. Die Verwendung dieser Option resultiert in einer kleineren Imagedatei und schnellerer Offlinewartung. Sie unterstützt außerdem den Prozess zum [Optimieren der Imagewartung](#bkmk_resetbase) für kleinere Imagedateien nach der Anwendung von Softwareupdates.  

        > [!IMPORTANT]  
        > Configuration Manager überschreibt die vorhandene install.wim-Datei im Betriebssystemupgradepaket. Der Image-Index wird an einen temporären Speicherort extrahiert und anschließend in das ursprüngliche Quellverzeichnis verschoben. Bevor Sie ein Paket für ein Betriebssystemupgrade importieren und diese Option aktivieren, müssen Sie die ursprünglichen Quelldateien sichern.

    - Wenn Sie Inhalte eines Clients vorab zwischenspeichern möchten, geben Sie die **Architektur** und **Sprache** des Images an. Weitere Informationen finden Sie unter [Konfigurieren des zwischengespeicherten Inhalts](../deploy-use/configure-precache-content.md).  

4. Geben Sie auf der Seite **Allgemein** die folgenden Informationen an. Diese Informationen sind für Identifikationszwecke hilfreich, wenn Sie über mehrere Betriebssystemupgradepakete verfügen.  

    - **Name:** Ein eindeutiger Name für das Betriebssystemupgradepaket.  

    - **Version**: Ein optionaler Versionsbezeichner. Diese Eigenschaft muss nicht der Betriebssystemversion des Upgradepakets entsprechen. Hierfür wird häufig die Paketversion des Unternehmens verwendet.  

    - **Kommentar**: Eine kurze, optionale Beschreibung.  

5. Schließen Sie den Assistenten ab.  

Verteilen Sie das Betriebssystemupgradepaket als Nächstes an die Verteilungspunkte.  

## <a name="distribute-content-to-a-distribution-point"></a><a name="BKMK_Distribute"></a> Verteilen von Inhalt an einen Verteilungspunkt  

Verteilen Sie die Betriebssystemupgradepakete wie jeden anderen Inhalt an Verteilungspunkte. Verteilen Sie das Betriebssystemupgradepaket an mindestens einen Verteilungspunkt, bevor Sie die Tasksequenz bereitstellen. Weitere Informationen finden Sie unter [Distribute content (Verteilen von Inhalt)](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]

## <a name="next-steps"></a>Nächste Schritte

[Erstellen einer Tasksequenz zum Durchführen eines Betriebssystemupgrades](../deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)
