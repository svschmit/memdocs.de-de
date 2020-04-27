---
title: Package Conversion Manager
titleSuffix: Configuration Manager
description: Erfahren Sie, wie in Configuration Manager Pakete mit dem Paketkonvertierungs-Manager in Anwendungen konvertiert werden.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: f053fa73-c553-4522-a6b9-f885f23fe57c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 075dd860d20662679e5bdf58dae23d0220fa751e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689008"
---
# <a name="package-conversion-manager"></a>Package Conversion Manager

*Gilt für: Configuration Manager (Current Branch)*

<!--1357861-->

Ab Version 1806 unterstützt Sie der Paketkonvertierungs-Manager bei der Konvertierung von älteren Configuration Manager-Paketen in Anwendungen. Anwendungen bieten zusätzliche Vorteile wie Abhängigkeiten, Anforderungsregeln, Erkennungsmethoden und Affinität zwischen Benutzer und Gerät.

> [!Tip]  
> Dieses Feature wurde erstmals in Version 1806 als [Vorabfeature](../../core/servers/manage/pre-release-features.md) eingeführt. Ab Version 1810 ist dieses Feature kein Vorabfeature mehr.  


Eine Configuration Manager-Anwendung enthält Dateien und Programme, die Sie auf Clientgeräten bereitstellen können. Im Unterschied zu älteren Paketen und Programmen stellt eine Anwendung allerdings zusätzliche benutzerorientierte Funktionen zur Verfügung. Beispielsweise kann eine Anwendung Bereitstellungstypen für die lokale Installation eines Softwarepakets, ein virtuelles Anwendungspaket oder eine Version der Anwendung für mobile Geräte enthalten.

Weitere Informationen finden Sie in den folgenden Artikeln: 
- [Einführung in die Anwendungsverwaltung](../understand/introduction-to-application-management.md)  
- [Pakete und Programme](../deploy-use/packages-and-programs.md)  

> [!Important]  
> Wenn Sie bereits eine ältere Version des Paketkonvertierungs-Managers installiert haben, deinstallieren Sie diese, bevor Sie Ihren Standort aktualisieren. Diese integrierte Version erfordert keine Installation, jedoch kann ein Konflikt mit vorhandenen Versionen auftreten.  

Diese integrierte Version des Paketkonvertierungs-Managers funktioniert für Pakete am aktuellen Current Branch-Standort von Configuration Manager. Sie ist kein eigenständiges Tool. Wenn Sie über Pakete und Programme in einer älteren Version von Configuration Manager verfügen, müssen Sie die Pakete zunächst in Ihren Current Branch-Standort migrieren. Weitere Informationen finden Sie unter [Migrieren von Daten zwischen Hierarchien](../../core/migration/migrate-data-between-hierarchies.md).

<!-- SCCMDocs-pr issue #3357 -->
Configuration Manager, Version 1902, umfasst die folgenden Verbesserungen:
- Geplante Paketanalyse wird standardmäßig alle 7 Tage ausgeführt.
- PowerShell-Cmdlets zum Analysieren und Konvertieren von Paketen
- Allgemeine Fehlerbehebungen und Verbesserungen



## <a name="planning"></a>Planung

Bevor Sie mit der Konvertierung von Paketen in Anwendungen beginnen, erstellen Sie zunächst einen Plan. Es folgt ein Beispielplan:

- [Definieren eines detaillierten Paketkonvertierungsplans](#bkmk_define)  

- [Auswählen und Vorbereiten von Paketen für die Konvertierung](#bkmk_prepare)  

- [Auswählen von Testpaketen](#bkmk_test)  

- [Analysieren, Untersuchen und Konvertieren von Paketen](#bkmk_analyze)  

- [Testen und Bereitstellen der Anwendungen](#bkmk_deploy)  


### <a name="define-a-detailed-package-conversion-plan"></a><a name="bkmk_define"></a> Definieren eines detaillierten Paketkonvertierungsplans

In diesem Abschnitt werden zwei Beispielpläne für die Konvertierung von Paketen beschrieben:  

- [Eine Testumgebung mit umfassenden Ressourcen:](#bkmk_define-high) Sie verfügen über eine Testumgebung mit den Ressourcen, Berechtigungen und der Architektur zur vollständigen Replikation Ihrer Produktionsumgebung.  

- [Eine Testumgebung mit begrenzten Ressourcen:](#bkmk_define-limited) Sie verfügen über keine Testumgebung zur vollständigen Replikation Ihrer Produktionsumgebung.  

Passen Sie diese Pläne nach Bedarf entsprechend anderer Aspekte in Ihrer Umgebung an.

#### <a name="sample-plan-for-a-high-resource-test-environment"></a><a name="bkmk_define-high"></a> Beispielplan für eine Testumgebung mit umfassenden Ressourcen

Ihre Testumgebung verfügt über ähnliche Ressourcen, Berechtigungen und Architekturen wie Ihre Produktionsumgebung. Nutzen Sie die Testumgebung, um alle Ihre Pakete effizient zu analysieren und zu konvertieren. Testen Sie anschließend alle Ihre Configuration Manager-Anwendungen. Übertragen Sie sie nach Abschluss dieser Arbeitsschritte in die Produktionsumgebung. 

Ihr Paketkonvertierungsplan kann vergleichbar mit den folgenden Schritten sein:  

1.  Auswählen der zu konvertierenden Pakete  

2.  Migrieren der zu konvertierenden Pakete in Ihre Testumgebung  

3.  Bereiten Sie die Pakete für die Konvertierung vor.  

4.  Wählen Sie Testpakete aus.  

5.  Analysieren, untersuchen und konvertieren Sie die Testpakete.  

6.  Testen Sie die konvertierten Anwendungen.  

7.  Analysieren und konvertieren Sie die übrigen, nicht zum Test gehörenden Pakete.  

8.  Exportieren der Anwendungen aus der Testumgebung Importieren der Anwendungen in Ihre Produktionsumgebung  

#### <a name="sample-plan-for-a-limited-resource-test-environment"></a><a name="bkmk_define-limited"></a> Beispielplan für eine Testumgebung mit eingeschränkten Ressourcen

Ihre Testumgebung verfügt nicht über ähnliche Ressourcen, Berechtigungen und Architekturen wie Ihre Produktionsumgebung. Sie können nicht alle Ihre Pakete analysieren, testen und konvertieren. In diesem Szenario sollten Sie nur Ihre Testpakete analysieren, untersuchen, konvertieren und testen. Migrieren Sie danach die restlichen Pakete in die Produktionsumgebung, um sie zu analysieren und zu konvertieren. 

Ihr Paketkonvertierungsplan kann vergleichbar mit den folgenden Schritten sein:

1.  Auswählen der zu konvertierenden Pakete  

2.  Wählen Sie Testpakete aus.  

3.  Migrieren Sie die Testpakete zu Ihrer Testumgebung.  

4.  Bereiten Sie die Testpakete für die Konvertierung vor.  

5.  Analysieren, untersuchen und konvertieren Sie die Testpakete.  

6.  Testen Sie die konvertierten Anwendungen.  

7.  Exportieren der Testanwendungen aus der Testumgebung Importieren der Anwendungen in Ihre Produktionsumgebung  

8.  Migrieren Sie die übrigen Pakete zur Produktionsumgebung, und bereiten Sie sie für die Konvertierung vor.  

9.  Analysieren, untersuchen und konvertieren Sie die übrigen Pakete in der Produktionsumgebung.  

10. Geben Sie die übrigen Anwendungen für die Produktionsumgebung frei.  


### <a name="select-and-prepare-packages-for-conversion"></a><a name="bkmk_prepare"></a> Auswählen und Vorbereiten von Paketen für die Konvertierung

#### <a name="select-the-packages-that-you-want-to-convert"></a><a name="bkmk_prepare-select"></a> Auswählen von Paketen für die Konvertierung

Nicht alle Pakete eignen sich für die Konvertierung in Anwendungen. Bevor Sie mit der Konvertierung von Paketen beginnen, bestimmen Sie die Pakete, die nicht konvertiert werden sollen. 

Am besten geeignet für die Konvertierung in Anwendungen sind solche Pakete, die Software mit Benutzerkontakt enthalten. Dazu gehören zum Beispiel:  

- Windows Installer-Dateien (.msi, msu)  

- Microsoft Application Virtualization-Programme (App-V)  

- Ausführbare Windows-Dateien (.exe)  

Folgende Pakettypen sollten am besten als Pakete belassen und nicht in Anwendungen konvertiert werden:

- Systemwartungtools. Beispiele: Skripts oder Sicherungsprogramme.  

- Pakete für Software, die nicht mehr unterstützt werden.

> [!Tip]  
> Nachdem Sie die Pakete ermittelt haben, die für die Konvertierung in Anwendungen nicht geeignet sind, verschieben Sie sie in der Configuration Manager-Konsole in einen separaten Ordner. So erstellen Sie in der Configuration Manager-Konsole einen Paketordner  
> - Klicken Sie mit der rechten Maustaste auf den Knoten **Pakete**.  
> - Wählen Sie **Ordner** aus, und klicken Sie dann auf **Ordner erstellen**.  
> - Geben Sie den Ordnernamen ein, z.B. `Not Converted`.  
> - Klicken Sie auf **OK**.  

#### <a name="prepare-the-packages-for-conversion"></a>Vorbereiten der Pakete für die Konvertierung

Jedes zu konvertierende Paket muss folgenden Anforderungen entsprechen:  

- Der Speicherort der Quelldateien ist ein vollständiger UNC-Pfad, z.B. `\\Server\Share\File`.  

- Windows Installer-Dateien verwenden nur einen eindeutigen Produktcode.  


### <a name="select-test-packages"></a><a name="bkmk_test"></a> Auswählen von Testpaketen

In Ihrer Gruppe von Testpaketen sollten möglichst Pakete enthalten sein, die die folgenden Kriterien erfüllen:  

- Mindestens ein Testpaket mit dem Bereitschaftsstatus **Automatisch**  

- Mindestens ein Testpaket mit dem Bereitschaftsstatus **Manuell**  

Im Idealfall sollte es sich bei den Testpaketen um Kernpakete handeln, wie z.B.:  

- Pakete, mit denen Sie vertraut sind  

- Pakete, die für Ihr Unternehmen äußerst wichtig sind.  

- Pakete, die Sie sehr einfach testen können  

Bestimmen Sie die Pakete, die für Tests geeignet sind. Verschieben Sie sie anschließend in der Configuration Manager-Konsole in einen separaten Ordner.


### <a name="analyze-investigate-and-convert-packages"></a><a name="bkmk_analyze"></a> Analysieren, Untersuchen und Konvertieren von Paketen

#### <a name="analyze-packages"></a>Analysieren von Paketen

Um ein einzelnes Paket oder eine kleine Gruppe zu analysieren, verwenden Sie den in die Configuration Manager-Konsole integrierten Paketkonvertierungs-Manager. Weitere Informationen finden Sie unter [Analysieren und Konvertieren von Paketen](how-to-analyze-and-convert.md).  

> [!NOTE]  
> Wechseln Sie im Arbeitsbereich **Überwachung** zum Knoten **Paketkonvertierungsstatus**. Hier werden Informationen zum Analyse- und Konvertierungsprozess als Zusammenfassung angezeigt.  

#### <a name="investigate-analysis-results"></a>Untersuchen der Analyseergebnisse

Untersuchen Sie nach dem Analysieren der Testpakete alle Pakete mit dem Bereitschaftsstatus **Manuell** oder **Fehler**. Ermitteln Sie die Ursachen für den jeweiligen Status. Zu den häufigen Ursachen für den Bereitschaftsstatus **Manuell** oder **Fehler** gehören:

- Informationen, die zum Erstellen einer Erkennungsmethode im Bereitstellungstyp einer Anwendung erforderlich sind, sind nicht im Paket enthalten.  

- Informationen, die zum Konvertieren von Sammlungen in globale Bedingungen und Anforderungen erforderlich sind, sind nicht im Paket enthalten.  

- Das Paket enthält mehrere Programme.  

- Das Paket ist von einem anderen Paket abhängig, das Sie nicht in eine Anwendung konvertiert haben.  

Weitere Informationen finden Sie in den folgenden Ressourcen:  

- Überprüfen Sie die Fehlermeldungen und -korrekturen unter [Technische Referenz zu Fehlermeldungen im Paketkonvertierungs-Manager](error-messages.md).  

- Überprüfen Sie die Protokolldatei **PCMTrace.log**.  

- Siehe [Beheben von Problemen mit dem Paketkonvertierungs-Manager](troubleshoot-pcm.md).  

#### <a name="convert-the-packages"></a>Konvertieren der Pakete

Weitere Informationen zum Konvertieren von Paketen finden Sie unter [Analysieren und Konvertieren von Paketen](how-to-analyze-and-convert.md).

> [!NOTE]  
> Wechseln Sie im Arbeitsbereich **Überwachung** zum Knoten **Paketkonvertierungsstatus**. Hier werden Informationen zum Analyse- und Konvertierungsprozess als Zusammenfassung angezeigt.  


### <a name="test-and-deploy-the-applications"></a><a name="bkmk_deploy"></a> Testen und Bereitstellen der Anwendungen

Testen Sie die Anwendungen gemäß Ihrem detaillierten Paketkonvertierungsplan entweder in Ihrer Testumgebung oder in der Produktionsumgebung.



## <a name="recommendations"></a>Empfehlungen

- Wechseln Sie anschließend im Arbeitsbereich **Überwachung** zum Knoten **Paketkonvertierungsstatus**. Hier werden Informationen zum Analyse- und Konvertierungsprozess als Zusammenfassung angezeigt.  

- Untersuchen Sie die Programme in Ihren Paketen (die auch Wrapper genannt werden). Verwenden Sie das Plug-In „Paketkonvertierungs-Manager“, um ihre Funktionen in entsprechende Configuration Manager-Funktionen zu konvertieren.  

- Stellen Sie sicher, dass Sie jede konvertierte Anwendung gründlich testen, bevor Sie sie in einer Produktionsumgebung bereitstellen.  



## <a name="next-steps"></a>Nächste Schritte

[Analysieren und Konvertieren von Paketen](how-to-analyze-and-convert.md)
