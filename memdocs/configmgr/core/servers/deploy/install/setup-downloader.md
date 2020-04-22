---
title: Setup-Downloadprogramm
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über diese eigenständige Anwendung, die sicherstellen soll, dass Ihre Standortinstallation aktuelle Versionen der wichtigsten Installationsdateien verwendet.
ms.date: 01/22/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2fa1899f8e7dc14812f9f9ecf889350a153b2d25
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700568"
---
# <a name="setup-downloader-for-configuration-manager"></a>Setup-Downloadprogramm für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Bevor Sie das Setup zum Installieren oder Upgraden eines Configuration Manager-Standorts ausführen, können Sie die eigenständige Setup-Downloadanwendung für die zu installierende Version von Configuration Manager verwenden, um aktualisierte Setupdateien herunterzuladen.  

Die Verwendung aktualisierter Setupdateien stellt sicher, dass für Ihre Standortinstallation aktuelle Versionen der wichtigsten Installationsdateien verwendet werden. Übersicht:   
-   Wenn Sie das Setup-Downloadprogramm zum Herunterladen von Dateien vor dem Starten des Setups verwenden, geben Sie einen Ordner zum Speichern der Dateien an.  
-   Das Konto, mit dem Sie das Setup-Downloadprogramm ausführen, benötigt **Vollzugriff**-Berechtigungen für den Downloadordner.  
-   Beim Ausführen von Setup zum Installieren oder Aktualisieren eines Standorts können Sie das Setup anweisen, diese lokale Kopie von Dateien zu verwenden, die Sie zuvor heruntergeladen haben. Dies verhindert, dass das Setup eine Verbindung mit Microsoft herstellen muss, wenn Sie die Installation oder das Upgrade des Standorts starten.  
-   Sie können die gleiche lokale Kopie der Setupdateien für nachfolgende Standortinstallationen oder -upgrades verwenden.  

Die folgenden Dateitypen werden vom Setup-Downloadprogramm heruntergeladen:  
-   Erforderliche verteilbare Dateien  
-   Sprachpakete  
-   Die neuesten Produktupdates für Setup  

Sie haben zwei Optionen zum Ausführen des Setup-Downloadprogramms:
- Die Anwendung mit der Benutzeroberfläche ausführen
- Die Anwendung für Befehlszeilenoptionen an einer Eingabeaufforderung ausführen


## <a name="run-setup-downloader-with-the-user-interface"></a><a name="bkmk_ui"></a> Ausführen des Setup-Downloadprogramm über die Benutzeroberfläche  

1.  Öffnen Sie auf einem Computer mit Internetzugriff den Windows-Explorer, und wechseln Sie zu **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**.  

2.  Doppelklicken Sie auf **Setupdl.exe**, um das Setup-Downloadprogramm zu öffnen.   

3. Geben Sie den Pfad zu dem Ordner mit den aktuellen Installationsdateien an, und klicken Sie dann auf **Herunterladen**. Das Setup-Downloadprogramm überprüft die Dateien im Downloadordner. Es werden nur die Dateien heruntergeladen, die fehlen oder die neuer sind als vorhandene Dateien. Es werden Unterordner für die heruntergeladenen Sprachen und weitere erforderliche Unterordner erstellt.  

4.  Überprüfen Sie die Downloadergebnisse anhand der Datei **ConfigMgrSetup.log** im Stammverzeichnis von Laufwerk C.  

## <a name="run-setup-downloader-from-a-command-prompt"></a><a name="bkmk_cmd"></a> Ausführen des Setup-Downloadprogramms über eine Eingabeaufforderung  

1.  Gehen Sie in einem Eingabeaufforderungsfenster zu **&lt;*Configuration Manager-Installationsmedium*\>\SMSSETUP\BIN\X64**.   

2.  Führen Sie **Setupdl.exe** aus, um das Setup-Downloadprogramm zu öffnen.

    Sie können die folgenden Befehlszeilenoptionen mit **Setupdl.exe** verwenden:   

    -   **/VERIFY:** Verwenden Sie diese Option, um die Dateien im Downloadordner einschließlich der Sprachdateien zu überprüfen. Überprüfen Sie anhand der Liste in der Datei ConfigMgrSetup.log im Stammverzeichnis des Laufwerks C, welche Dateien veraltet sind. Wenn Sie diese Option verwenden, werden keine Dateien heruntergeladen.  

    -   **/VERIFYLANG:** Verwenden Sie diese Option, um die Sprachdateien im Downloadordner zu überprüfen. Überprüfen Sie anhand der Liste in der Datei ConfigMgrSetup.log im Stammverzeichnis des Laufwerks C, welche Sprachdateien veraltet sind.

    -   **/LANG:** Verwenden Sie diese Option, um nur die Sprachdateien in den Downloadordner herunterzuladen.  

    -   **/NOUI:** Verwenden Sie diese Option, um das Setup-Downloadprogramm zu starten, ohne die Benutzeroberfläche anzuzeigen. Sie müssen dann den **Downloadpfad** als Teil der Befehlszeile bei der Eingabeaufforderung angeben.  

    -   **&lt;DownloadPath:\>** Sie können den Pfad zum Downloadordner angeben, um den Überprüfungs- oder den Downloadvorgang automatisch zu starten. Wenn Sie die Option **/NOUI** verwenden, müssen Sie den Downloadpfad angeben. Geschieht dies nicht, müssen Sie den Pfad angeben, sobald das Setup-Downloadprogramm geöffnet wird. Wenn der Ordner nicht vorhanden ist, wird er vom Setup-Downloadprogramm erstellt.  

    Beispielbefehle:

    -   **setupdl &lt;DownloadPath\>**  

        -   Das Setup-Downloadprogramm wird gestartet. Die Dateien im angegebenen Downloadordner werden überprüft, und nur fehlende Dateien oder Dateien mit aktuelleren Versionen werden heruntergeladen.     

    -   **setupdl /VERIFY &lt;Downloadpfad\>**  

        -   Das Setup-Downloadprogramm wird gestartet. Die Dateien im angegebenen Downloadordner werden überprüft.  

    -   **setupdl /NOUI &lt;Downloadpfad\>**  

        -   Das Setup-Downloadprogramm wird gestartet. Die Dateien im angegebenen Downloadordner werden überprüft, und nur fehlende oder aktuellere Dateien werden heruntergeladen.  

    -   **setupdl /LANG &lt;Downloadpfad\>**  

        -   Das Setup-Downloadprogramm wird gestartet. Die Sprachdateien im angegebenen Downloadordner werden überprüft, und nur fehlende oder aktuellere Sprachdateien werden heruntergeladen.  

    -   **setupdl /VERIFY**  

        -   Das Setup-Downloadprogramm wird gestartet. Anschließend müssen Sie den Pfad für den Downloadordner angeben. Nachdem Sie auf **Überprüfen** geklickt haben, werden die Dateien im Downloadordner vom Setup-Downloadprogramm überprüft.  

3.  Überprüfen Sie die Downloadergebnisse anhand der Datei **ConfigMgrSetup.log** im Stammverzeichnis von Laufwerk C.

## <a name="copy-setup-downloader-files-to-another-computer"></a><a name="bkmk_cp-files"></a> Kopieren von Setup-Downloadprogrammdateien auf einen anderen Computer

1. Gehen Sie im Windows-Explorer zu einem der folgenden Speicherorte:

    - **&lt;Configuration Manager-Installationsmedium>\SMSSETUP\BIN\X64**
    - **&lt;Configuration Manager-Installationspfad>\BIN\X64**
    
1. Kopieren Sie die folgenden Dateien in denselben Zielordner auf dem anderen Computer:
    
    - **setupdl.exe**
    - **.\\&lt;Sprache>\\setupdlres.dll**
      - Diese Datei befindet sich im Unterordner für die Installationssprache. Englisch beispielsweise befindet sich im Unterordner `00000409`.

    Beispielsweise sollten die Zielordnerpfade auf Ihrem Gerät wie folgt aussehen:
    - C:\ConfigManInstall\setupdl.exe
    - C:\ConfigManInstall\00000409\setupdlres.dll

1. Starten Sie das Setup-Downloadprogramm auf dem Computer entweder über die [Benutzeroberfläche](#bkmk_ui) oder die [Eingabeaufforderung](#bkmk_cmd). Wie das funktioniert, wurde in den obigen Abschnitten beschrieben.
