---
title: Testen des Datenbankupdates
titleSuffix: Configuration Manager
description: Testen Sie Upgrades der Standortdatenbank bei der Installation von Updates für Configuration Manager.
ms.date: 06/13/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: abb696f3-a816-4f12-a9f1-0503a81e1976
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 56c1422f4157b255f4f7a8624e36d10e01f28fc0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703288"
---
# <a name="test-the-database-upgrade-when-installing-an-update"></a>Testen des Datenbankupgrades bei der Installation eines Updates

*Gilt für: Configuration Manager (Current Branch)*

Mithilfe der Informationen in diesem Thema können Sie einen Test eines Datenbankupgrades ausführen, ehe Sie ein konsoleninternes Update für den Current Branch von Configuration Manager installieren. Allerdings ist das Testen des Upgrades kein erforderlicher oder empfohlener Schritt mehr, es sei denn, Ihre Datenbank ist fehlerverdächtig oder wurde mittels Anpassungen modifiziert, die nicht explizit von Configuration Manager unterstützt werden.

## <a name="do-i-need-to-run-a-test-upgrade"></a>Muss ich ein Testupgrade ausführen?
Die Veraltung dieses Upgradetests wird aufgrund von Änderungen ermöglicht, die in Configuration Manager (Current Branch) eingeführt werden. Diese Änderungen vereinfachen den Prozess und erhöhen das Tempo, mit dem eine Produktionsumgebung auf neuere Versionen aktualisiert werden kann. Dieser Neugestaltung ist erfolgt, um Kunden zu ermöglichen, mit weniger Risiko und Betriebsmehraufwand auf dem neuesten Stand zu bleiben, wenn das jeweilige neue Update installiert wird.

Die Änderungen bei der Installation von Updates schließen Logik ein, die ein fehlerhaftes Update automatisch rückgängig macht, ohne dass eine Standortwiederherstellung erfolgen muss. Diese Änderungen ermöglichen die Verwendung der Konsole zum Verwalten der Installation von Updates und schließen eine Option zum [Wiederholen der Installation eines fehlerhaften Updates](install-in-console-updates.md#bkmk_retry) ein.

> [!TIP]
> Bei einem Upgrade eines älteren Produkts zu Configuration Manager (Current Branch), wie z. B. System Center Configuration Manager 2012, [bleibt das Testen von Datenbankupgrades ein empfohlener Schritt](../deploy/install/upgrade-to-configuration-manager.md#bkmk_test).

Wenn Sie bei der Installation eines konsoleninternen Updates dennoch weiterhin das Upgrade einer Standortdatenbank planen, ergänzen die folgenden Informationen die [Anleitung zum Installieren eines konsoleninternen Updates](install-in-console-updates.md#bkmk_install).

## <a name="prepare-to-run-a-test-database-upgrade"></a>Vorbereiten der Ausführung eines Testdatenbankupgrades  
Vor der Installation eines neuen Updates in Ihrer Hierarchie, beispielsweise 1702, können Sie das Upgrade der Standortdatenbank testen.

Verwenden Sie zum Ausführen des Upgradetests das Configuration Manager-Setup in den Quelldateien im Ordner [CD.Latest](the-cd.latest-folder.md) eines Standorts mit der Version von Configuration Manager, auf die Sie aktualisieren. Für das Testen des Datenbankupdates für das Update auf Version 1702 gelten folgenden Anforderungen:
-   Sie benötigen mindestens ein Standort mit Version 1702, von dem Sie den erforderlichen Ordner „CD.Latest“ abrufen können.
-   Wenn Sie nicht über einen Standort mit der erforderlichen Version verfügen, sollten Sie einen Standort in einer Laborumgebung installieren und anschließend diesen Standort auf die neue Version aktualisieren. Dadurch wird der Ordner „CD.Latest“ mit der richtigen Version der Quelldateien erstellt.

Der Upgradetest erfolgt für eine Sicherung Ihrer Standortdatenbank, die Sie aus einer getrennten Instanz von SQL Server wiederhergestellt haben.  Führen Sie Setup im Ordner **CD.Latest** mit der Befehlszeilenoption **testdbupgrade** aus, um für diese wiederhergestellte Kopie der Datenbank ein Testupgrade auszuführen. Nach Abschluss des Testupgrades wird die aktualisierte Datenbank verworfen. Sie kann nicht von einem Configuration Manager-Standort verwendet werden.

Wenn bei der Installation eines Updates ein Fehler auftritt, sollten Sie den Standort nicht wiederherstellen müssen. Stattdessen können Sie die Installation des Updates in der Konsole wiederholen.

##  <a name="run-the-test-upgrade"></a>Ausführen des Testupgrades    
1. Verwenden Sie das Configuration Manager-Setup und die Quelldateien im Ordner **CD.Latest** eines Standorts mit der Version, auf die Sie aktualisieren möchten.  

2. Kopieren Sie den Ordner **CD.Latest** an einen Speicherort in der SQL Server-Instanz, die Sie zum Ausführen des Testupgrades für die Datenbank verwenden möchten.

3. Erstellen Sie eine Sicherung der Standortdatenbank, deren Upgrade Sie testen möchten. Stellen Sie als Nächstes eine Kopie der Standortdatenbank in einer Instanz von SQL Server wieder her, in der kein Configuration Manager-Standort gehostet wird. Die SQL Server-Instanz muss dieselbe Edition von SQL Server wie die Standortdatenbank aufweisen.  

4. Führen Sie nach dem Wiederherstellen der Datenbankkopie **Setup** im Ordner „CD.Latest“ aus, der die Quelldateien der Version enthält, auf die Sie aktualisieren. Verwenden Sie beim Ausführen von Setup die Befehlszeilenoption **/TESTDBUPGRADE** . Wenn es sich bei der SQL Server-Instanz, von der die Datenbankkopie gehostet wird, nicht um die Standardinstanz handelt, geben Sie die Befehlszeilenargumente an. Damit können Sie ermitteln, von welcher Instanz die Kopie der Standortdatenbank gehostet wird.   

   Angenommen, Sie haben eine Standortdatenbank namens *SMS_ABC*. Sie stellen eine Kopie dieser Standortdatenbank in einer unterstützten Instanz von SQL Server mit dem Namen *DBTest* wieder her. Verwenden Sie die folgende Befehlszeile, um ein Upgrade dieser Kopie der Standortdatenbank zu testen: **Setup.exe /TESTDBUPGRADE DBtest\CM_ABC**.  

   Die Datei „Setup.exe“ befindet sich auf dem Quellmedium für Configuration Manager an folgendem Speicherort: **SMSSETUP\BIN\X64**.  

5. Überprüfen Sie den Fortschritt und Erfolg des Upgradetests in der Instanz von SQL Server, in der Sie den Test ausführen. Die nötigen Angaben dazu finden Sie in der Datei *ConfigMgrSetup.log* im Stamm des Systemlaufwerks.  

    Wenn beim Testen des Upgrades ein Fehler auftritt, beheben Sie alle Probleme im Zusammenhang mit diesem Fehler beim Upgrade der Standortdatenbank. Erstellen Sie anschließend eine neue Sicherung der Standortdatenbank, und testen Sie das Upgrade der neuen Kopie der Datenbank.  



## <a name="next-steps"></a>Nächste Schritte
Nach erfolgreichem Abschluss des Tests des Datenbankupdates verwerfen Sie die aktualisierte Datenbank. Sie kann nicht von einem Configuration Manager-Standort verwendet werden. Sie können dann zu Ihrem aktiven Standort zurückkehren und [mit der Installation des Updates beginnen](install-in-console-updates.md).
