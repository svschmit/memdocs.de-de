---
title: Installieren der Konsole
titleSuffix: Configuration Manager
description: Installieren Sie die Configuration Manager-Konsole, um eine Verbindung zu einem Standort der zentralen Verwaltung oder einem primären Standort herzustellen.
ms.date: 04/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f5fda03090f7ec69eb78b20385dfc009bac88f40
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700798"
---
# <a name="install-the-configuration-manager-console"></a>Installieren der Configuration Manager-Konsole

*Gilt für: Configuration Manager (Current Branch)*

Administratoren verwenden die Configuration Manager-Konsole zum Verwalten der Configuration Manager-Umgebung. Jede Configuration Manager-Konsole kann eine Verbindung zu einem Standort der zentralen Verwaltung (Central Administration Site, CAS) oder zu einem primären Standort herstellen. Sie können eine Configuration Manager-Konsole jedoch nicht mit einem sekundären Standort verbinden.

Die Configuration Manager-Konsole wird immer auf dem Standortserver für den CAS oder für einen primären Standort installiert. Wenn Sie die Konsole und den Standortserver getrennt voneinander installieren möchten, müssen Sie den eigenständigen Installer verwenden.  



## <a name="prerequisites"></a>Voraussetzungen

- Sie verfügen über **lokale Administratorrechte** auf dem Zielcomputer für die Konsole.  

- Sie haben eine **Leseberechtigung** für den Speicherort der Installationsdateien der Configuration Manager-Konsole.  



## <a name="source-paths"></a>Quellpfade

Entscheiden Sie, welchen Quellpfad Sie verwenden möchten:  

- Ordner „ConsoleSetup“ auf dem Standortserver: `<Configuration Manager site server installation path>\Tools\ConsoleSetup`  

    Bei der Installation eines Standortservers werden die Installationsdateien für die Konsole und die unterstützten Sprachpakete für den Standort in den Unterordner **Tools\ConsoleSetup** kopiert. Optional können Sie den Ordner **ConsoleSetup** an einen anderen Speicherort kopieren, um mit der Installation zu beginnen. Wenn Sie den Standort aktualisieren, bleibt die im Ordner gespeicherte lokale Version immer auf dem neuesten Stand.  

- Configuration Manager-Installationsmedien: `<Configuration Manager installation media>\SMSSETUP\BIN\I386`  

    Bei der Installation der Configuration Manager-Konsole über das Installationsmedium wird immer die englische Version installiert. Dieses Verhalten tritt auch dann auf, wenn der Standortserver verschiedene Sprachen unterstützt oder für das Betriebssystem des Zielcomputers eine andere Sprache festgelegt wird.  

Starten Sie das Installationsprogramm für die Konsole nach Möglichkeit aus dem Ordner **ConsoleSetup** statt aus den Quellmedien.

> [!Important]  
> Installieren Sie die Konsole nicht mit den **CD.Latest**-Quelldateien. Dies ist ein nicht unterstütztes Szenario, das bei der Konsoleninstallation Probleme verursachen kann. Weitere Informationen finden Sie unter [Der Ordner „CD.Latest“](../../manage/the-cd.latest-folder.md#unsupported-scenarios).<!-- SCCMDocs issue 1359 -->  

Wenn Sie ein Paket zum Installieren der Konsole auf anderen Computern erstellen, sorgen Sie dafür, dass das Paket die folgenden Dateien enthält:<!--3612513-->

- ConsoleSetup.exe
- AdminConsole.msi
- ConfigMgr.AC_Extension.i386.cab (ab Version 1902)
- ConfigMgr.AC_Extension.amd64.cab (ab Version 1902)



## <a name="use-the-setup-wizard"></a>Verwenden des Setup-Assistenten  

1. Navigieren Sie zum Quellpfad, und öffnen Sie **ConsoleSetup.exe**.  

    > [!IMPORTANT]  
    > Installieren Sie die Konsole immer mithilfe der Datei **consolesetup.exe**. Sie können die Configuration Manager-Konsole zwar auch durch Ausführen von „AdminConsole.msi“ installieren, doch finden dabei keine Überprüfungen auf erforderliche Komponenten oder Abhängigkeiten statt. Das Installationsprogramm wird in diesem Fall möglicherweise nicht korrekt ausgeführt.  

2. Wählen Sie im Assistenten **Weiter** aus.  

3. Geben Sie auf der Seite **Standortserver** den vollqualifizierten Domänennamen (FQDN) des Standortservers an, mit dem sich die Configuration Manager-Konsole verbindet.  

4. Geben Sie auf der Seite **Installationsordner** den Installationsordner für die Configuration Manager-Konsole ein. Der Ordnerpfad kann keine nachfolgenden Leerzeichen oder Unicode-Zeichen enthalten.  

5. Wählen Sie auf der Seite **Programm zur Verbesserung der Benutzerfreundlichkeit** (CEIP) aus, ob Sie an diesem Programm teilnehmen möchten.  

    > [!Note]  
    > Ab Configuration Manager-Version 1802 ist das CEIP-Feature (Programm zur Verbesserung der Benutzerfreundlichkeit) nicht mehr im Produkt enthalten.

6. Wählen Sie auf der Seite **Produkt kann installiert werden** die Option **Installieren** aus.  



## <a name="install-from-a-command-prompt"></a>Installieren von einer Eingabeaufforderung aus  

> [!TIP]  
> Bei der Installation der Configuration Manager-Konsole über eine Befehlszeile wird immer die englische Version installiert. Dieses Verhalten tritt auch dann auf, wenn für das Betriebssystem des Zielcomputers eine andere Sprache festgelegt wird. Wenn Sie die Configuration Manager-Konsole in einer anderen Sprache als Englisch installieren möchten, [verwenden Sie den Setup-Assistenten](#use-the-setup-wizard).  


### <a name="consolesetupexe-command-line-options"></a>Befehlszeilenoptionen von „ConsoleSetup.exe“

#### <a name="q"></a>/q

Installiert die Configuration Manager-Konsole unbeaufsichtigt Wenn Sie diese Option verwenden, sind die Optionen **EnableSQM**, **TargetDir**und **DefaultSiteServerName** erforderlich.

#### <a name="uninstall"></a>/uninstall

Deinstalliert die Configuration Manager-Konsole Sie müssen diese Option zuerst angeben, wenn Sie sie mit der Option **/q** verwenden.

#### <a name="langpackdir"></a>LangPackDir

Gibt den Pfad zu dem Ordner an, der die Sprachdateien enthält. Sie können die Sprachdateien mit dem **Setup-Downloadprogramm** herunterladen. Wenn Sie diese Option nicht verwenden, wird von Setup im aktuellen Ordner nach dem Sprachordner gesucht. Wenn der Sprachordner nicht gefunden wird, wird nur die Sprache Englisch installiert. Weitere Informationen finden Sie unter [Setup Downloader (Setup-Downloadprogramm)](setup-downloader.md).

#### <a name="targetdir"></a>TargetDir

Gibt den Installationsordner zur Installation der Configuration Manager-Konsole an. Diese Option ist erforderlich, wenn Sie die Option **/q** verwenden.

#### <a name="enablesqm"></a>EnableSQM

Hiermit wird angegeben, ob Sie am Programm zur Verbesserung der Benutzerfreundlichkeit (CEIP) teilnehmen möchten. Verwenden Sie den Wert **1**, um die CEIP-Funktion zu verknüpfen, und den Wert **0**, um nicht am Programm teilzunehmen. Diese Option ist erforderlich, wenn Sie die Option **/q** verwenden.

> [!Important]  
> Ab Configuration Manager-Version 1802 ist das CEIP-Feature (Programm zur Verbesserung der Benutzerfreundlichkeit) nicht mehr im Produkt enthalten. Die Verwendung des Parameters bewirkt, dass bei der Installation ein Fehler auftritt.

#### <a name="defaultsiteservername"></a>DefaultSiteServerName

Damit wird der FQDN des Standortservers angegeben, mit dem beim Start der Konsole eine Verbindung hergestellt wird. Diese Option ist erforderlich, wenn Sie die Option **/q** verwenden.


### <a name="examples"></a>Beispiele

> [!Important]  
> Schließen Sie bei Version 1802 und höheren Versionen nicht den Parameter **EnableSQM** ein.

#### <a name="silent-install"></a>Installation im Hintergrund

`ConsoleSetup.exe /q TargetDir="%ProgramFiles%\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com`

#### <a name="silent-install-with-language-packs"></a>Installation im Hintergrund mit Sprachpaketen

`ConsoleSetup.exe /q TargetDir="C:\Program Files\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com LangPackDir=C:\Downloads\ConfigMgr`  

#### <a name="silent-uninstall"></a>Deinstallation im Hintergrund

`ConsoleSetup.exe /uninstall /q`  



## <a name="see-also"></a>Weitere Informationen:

Administratoren werden Objekte in der Konsole entsprechend den Berechtigungen angezeigt, die ihren Benutzerkonten zugewiesen sind. Weitere Informationen finden Sie unter [Grundlagen der rollenbasierten Verwaltung](../../../understand/fundamentals-of-role-based-administration.md).

Weitere Informationen zu den Grundlagen der Navigation in der Configuration Manager-Konsole finden Sie unter [Verwenden der Konsole](../../manage/admin-console.md).
