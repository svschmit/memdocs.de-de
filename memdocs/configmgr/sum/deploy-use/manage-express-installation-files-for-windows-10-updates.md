---
title: Verwalten von Windows 10-Express-Updates
titleSuffix: Configuration Manager
description: Configuration Manager unterstützt Express-Installationsdateien für Windows 10, die kleinere Downloads und kürzere Installationszeiten für Clients bieten.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 11/02/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b8d8af88-e8ac-4deb-921b-975e2d2afd80
ms.openlocfilehash: ff018bc81ecdb3d11ebb71f1850804a5679c67f7
ms.sourcegitcommit: 7a099ff53668f50b37adab97ecd7ba98c5324676
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/12/2020
ms.locfileid: "84746577"
---
# <a name="manage-express-installation-files-for-windows-10-updates"></a>Verwalten von Express-Installationsdateien für Windows 10-Updates

Configuration Manager unterstützt Express-Installationsdateien für Windows 10-Updates. Konfigurieren Sie den Client, um nur die Änderungen zwischen dem kumulativen Windows 10-Qualitätsupdate des aktuellen Monats und dem Update des vorherigen Monats herunterzuladen. Ohne Express-Installationsdateien laden Configuration Manager-Clients jeden Monat das komplette kumulative Update für Windows 10 einschließlich aller Updates aus den letzten Monaten herunter. Mit Expressinstallationsdateien erhalten Sie kleinere Downloads und kürzere Installationszeiten.

Informationen zur Verwendung von Configuration Manager zum Verwalten von Updateinhalten, um stets auf dem neuesten Stand von Windows 10 zu bleiben, finden Sie unter [Optimieren der Bereitstellung von Updates für Windows 10](optimize-windows-10-update-delivery.md).  


> [!IMPORTANT]  
> Die Betriebssystem-Clientunterstützung ist in Windows 10, Version 1607 mit einem Update des Windows Update-Agents verfügbar. Dieses Update ist in den Updates vom 11. April 2017 enthalten. Weitere Informationen zu diesen Updates finden Sie im [Supportartikel 4015217](https://support.microsoft.com/kb/4015217). Zukünftige Updates nutzen Express für kleinere Downloads. Ältere Versionen von Windows 10 und Windows 10 Version 1607 ohne dieses Update unterstützen die Expressinstallationsdateien nicht.  


## <a name="enable-the-site-to-download-express-installation-files-for-windows-10-updates"></a>Aktivieren des Standorts zum Herunterladen von Expressinstallationsdateien für Windows 10-Updates
Um mit der Synchronisierung der Metadaten für Windows 10-Expressinstallationsdateien zu beginnen, aktivieren Sie dies in den Eigenschaften des Softwareupdatepunkts.  

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie den Knoten **Standorte** aus.  

2. Wählen Sie entweder den Standort der zentralen Verwaltung oder den eigenständigen primären Standort aus.  

3. Klicken Sie im Menüband auf **Standortkomponenten konfigurieren** und dann auf **Softwareupdatepunkt**. Wechseln Sie zur Registerkarte **Updatedateien**, und wählen Sie die Option **Die beiden vollständigen Dateien für alle genehmigten Windows 10-Expressinstallationsdateien herunterladen** aus.

> [!NOTE]    
> Sie können die Softwareupdatepunkt-Komponente nicht so konfigurieren, dass *nur* Expressupdates heruntergeladen werden.  Die Website lädt die Expressinstallationsdateien zusätzlich zu den vollständigen Dateien herunter. Dies erhöht die Menge an Inhalten, die in der Inhaltsbibliothek gespeichert und an Ihre Verteilungspunkte verteilt und dort gespeichert werden.

> [!Tip]  
> Um zu bestimmen, wieviel Speicherplatz die Datei auf dem Datenträger benötigt, aktivieren Sie die Eigenschaft **Größe auf Datenträger** der Datei. Die Eigenschaft „Größe auf Datenträger“ sollte erheblich kleiner sein als der Wert für „Größe“. Weitere Informationen finden Sie unter [Häufig gestellte Fragen zum Optimieren der Windows 10-Updatebereitstellung](optimize-windows-10-update-delivery.md#bkmk_faq).  


## <a name="enable-clients-to-download-and-install-express-installation-files"></a>Aktivieren der Clients zum Herunterladen und Installieren von Expressinstallationsdateien
Um die Unterstützung der Expressinstallationsdateien auf Clients zu aktivieren, aktivieren Sie die Expressinstallationsdateien in der Gruppe **Softwareupdates** der Clienteinstellungen. Diese Einstellung erstellt einen neuen HTTP-Listener, der Anfragen zum Herunterladen von Expressinstallationsdateien auf den Port, den Sie angeben, abruft.

> [!NOTE]    
> Dies ist ein lokaler Port, auf dem Clients auf Anforderungen der Übermittlungsoptimierung oder des Intelligenten Hintergrundübertragungsdiensts (Background Intelligent Transfer Service, BITS) lauschen, um Expressinhalte vom Verteilungspunkt herunterzuladen. Sie müssen diesen Port nicht in Firewalls öffnen, da sämtlicher Datenverkehr auf dem lokalen Computer erfolgt.  

Sobald Sie die Clienteinstellungen zur Aktivierung dieser Funktionalität auf dem Client bereitstellen, wird diese versuchen, das Delta zwischen dem kumulativen Update von Windows 10 des aktuellen Monats und dem Update des Vormonats herunterzuladen. Clients müssen eine Version von Windows 10 ausführen, die Expressinstallationsdateien unterstützt.  

1. Aktivieren Sie die Unterstützung von Expressinstallationsdateien in der Softwareupdatepunkt-Komponente (vorheriger Vorgang).  

2. Gehen Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, und wählen Sie **Clienteinstellungen** aus.  

3. Wählen Sie die entsprechenden Clienteinstellungen aus, und klicken Sie dann im Menüband auf **Eigenschaften**.  

4. Wählen Sie die Gruppe **Softwareupdates** aus. Konfigurieren Sie die Einstellung **Installation von Express-Updates auf Clients aktivieren** mit **Ja**. Konfigurieren Sie den Port, der vom HTTP-Listener für den Client verwendet wird, als **Port zum Herunterladen von Inhalten für Express-Updates**.
    - In Version 1902 wurde **Installation von Express-Installationsdateien auf Clients aktivieren** in **Clients das Herunterladen von Deltainhalten ermöglichen (falls verfügbar)** geändert.
    - In Version 1902 wurde **Zum Herunterladen von Inhalt für Express-Updates verwendeter Port** in **Von Clients verwendeter Port zum Empfang von Anforderungen für Deltainhalte** geändert.
    

## <a name="next-steps"></a>Nächste Schritte

[Bereitstellen von Softwareupdates](deploy-software-updates.md)
