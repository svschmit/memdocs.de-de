---
title: Dienstverbindungstool
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über das Dienstverbindungstool, mit dem Sie eine Verbindung mit dem Configuration Manager-Clouddienst herstellen können, um manuell Nutzungsinformationen hochzuladen.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
ms.assetid: 6e4964c5-43cb-4372-9a89-b62ae6a4775c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8b56b849be6abd2634e29d35e58494d4d3215857
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126085"
---
# <a name="use-the-service-connection-tool-for-configuration-manager"></a>Verwenden des Dienstverbindungstools für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Verwenden Sie das **Dienstverbindungstool**, wenn sich der Dienstverbindungspunkt im Offlinemodus befindet. Ebenso können Sie es verwenden, wenn die Configuration Manager-Standortsystemserver nicht mit dem Internet verbunden sind. Mit diesem Tool ist Ihr Standort in Bezug auf Configuration Manager-Updates immer auf dem neuesten Stand.

Wenn Sie dieses Tool ausführen, stellt es eine Verbindung mit dem Configuration Manager-Clouddienst her, um Nutzungsinformationen für Ihre Hierarchie hochzuladen und Updates herunterzuladen. Die Nutzungsdaten müssen hochgeladen werden, damit der Clouddienst die richtigen Updates für Ihre Umgebung bereitstellen kann.

## <a name="prerequisites"></a>Voraussetzungen

- Der Standort verfügt über einen Dienstverbindungspunkt, den Sie für die Einstellung **Offline, Verbindung bei Bedarf** konfigurieren.

- Führen Sie das Tool wie folgt über eine Eingabeaufforderung als Administrator aus. Es gibt keine Benutzeroberfläche.

- Sie führen das Tool über den Dienstverbindungspunkt und einen Computer aus, der eine Verbindung mit dem Internet herstellen kann. Jeder dieser Computer muss über ein x64-Bit-Betriebssystem und über die folgenden Komponenten verfügen:

  - **Visual C++ Redistributable** -Dateien für x86- und x64-Systeme. Standardmäßig installiert Configuration Manager die x64-Version auf dem Computer, der den Dienstverbindungspunkt hostet. Informationen zum Herunterladen dieser Komponente finden Sie unter [Visual C++ Redistributable Packages für Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=40784).

  - **.NET Framework 4.5.2** oder höher

- Das Konto, das Sie verwenden, um das Tool auszuführen, benötigt die folgenden Berechtigungen:

  - **Lokaler Administrator** auf dem Computer, der den Dienstverbindungspunkt hostet.

  - **Leseberechtigungen** für die Standortdatenbank

- Sie benötigen eine Methode zum Übertragen der Dateien zwischen dem Computer mit Internetzugriff und dem Dienstverbindungspunkt, zum Beispiel ein USB-Laufwerk mit genügend freiem Speicherplatz zum Speichern der Dateien und Updates.

## <a name="overview"></a>Übersicht

1. **Vorbereiten:** Führen Sie das Tool auf dem Dienstverbindungspunkt aus. Dieses überträgt Ihre Nutzungsdaten in eine CAB-Datei an einem von Ihnen festgelegten Speicherort. Kopieren Sie die Datendatei auf den Computer mit einer Internetverbindung.

2. **Verbinden:** Führen Sie das Tool auf dem Computer mit einer Internetverbindung aus. Die Nutzungsdaten werden hochgeladen, und anschließend werden die Configuration Manager-Updates heruntergeladen. Kopieren Sie die heruntergeladenen Updates auf den Dienstverbindungspunkt.

    Sie können mehrere Datendateien gleichzeitig aus unterschiedlichen Hierarchien hochladen. Sie können auch einen Proxyserver und einen Benutzer für den Proxyserver angeben.

3. **Importieren:** Führen Sie das Tool auf dem Dienstverbindungspunkt aus. Die Updates werden importiert und Ihrem Standort hinzugefügt. Sie können diese Updates in der Configuration Manager-Konsole anzeigen und [installieren](install-in-console-updates.md).

### <a name="upload-multiple-data-files"></a>Hochladen mehrerer Datendateien

- Fügen Sie alle exportierten Datendateien aus separaten Hierarchien in denselben Ordner ein. Benennen Sie jede Datei mit einem eindeutigen Namen. Falls erforderlich, können Sie sie manuell umbenennen.

- Wenn Sie anschließend das Tool zum Hochladen der Daten für Microsoft ausführen, geben Sie den Ordner an, der die Datendateien enthält.

- Wenn Sie das Tool ausführen, um Daten zu importieren, importiert dieses nur die Daten für diese Hierarchie.

### <a name="specify-a-proxy-server"></a>Angeben eines Proxyservers

Wenn für den Computer mit einer Internetverbindung ein Proxyserver erforderlich ist, unterstützt das Tool eine Standardproxykonfiguration. Verwenden Sie die optionalen Parameter **-proxyserveruri** und **-proxyusername**. Weitere Informationen finden Sie unter [Befehlszeilenparameter](#bkmk_cmd).

### <a name="specify-the-type-of-updates-to-download"></a>Angeben des Typs der herunterzuladenden Updates

Das Tool unterstützt Optionen, um zu steuern, welche Dateien heruntergeladen werden. Standardmäßig lädt das Tool nur das letzte verfügbare Update herunter, das für die Version Ihres Standorts gilt. Hotfixes werden nicht heruntergeladen.

Sie können einen der folgenden Parameter verwenden, um zu ändern, welche Dateien heruntergeladen werden:

- **-downloadall:** Mit diesem Parameter werden unabhängig von der Standortversion alle Updates heruntergeladen, einschließlich Hotfixes.
- **-downloadhotfix:** Mit diesem Parameter werden unabhängig von der Standortversion alle Hotfixes heruntergeladen.
- **-downloadsiteversion:** Mit diesem Parameter werden Updates und Hotfixes höherer Versionen als die Standortversion heruntergeladen.

    > [!IMPORTANT]
    > Aufgrund eines bekannten Problems in Configuration Manager 2002 funktioniert das Standardverhalten nicht wie erwartet. Aktualisieren Sie auf Version 2006, oder verwenden Sie den Parameter **-downloadsiteversion**, um die erforderlichen Updates für Version 2002 herunterzuladen.<!-- 7594517 -->

Weitere Informationen finden Sie unter [Befehlszeilenparameter](#bkmk_cmd).

> [!TIP]
> Das Tool bestimmt die Version Ihres Standorts aus der Datendatei. Wenn Sie die Version überprüfen möchten, können Sie in der CAB-Datei nach der Textdatei suchen, in deren Dateinamen die Standortversion enthalten ist.

## <a name="use-the-tool"></a>Verwendung des Tools  

Das Dienstverbindungstool befindet sich auf dem Configuration Manager-Installationsmedium unter dem folgenden Pfad: `SMSSETUP\TOOLS\ServiceConnectionTool\ServiceConnectionTool.exe`. Verwenden Sie immer das Dienstverbindungstool, das der Version von Configuration Manager entspricht, die Sie verwenden. Damit das Dienstverbindungstool funktioniert, müssen sich alle Dateien im selben Ordner befinden.

Kopieren Sie den Ordner **ServiceConnectionTool** mit dem gesamten Inhalt auf einen Computer mit Internetverbindung.

In diesem Verfahren werden in den Befehlszeilenbeispielen die folgenden Dateinamen und Speicherorte für Ordner verwendet. Sie müssen diese Pfade und Dateinamen aber nicht verwenden. Sie können auch Alternativen verwenden, die Ihrer Umgebung und Ihren Anforderungen entsprechen.

- Der Pfad zu den Quelldateien aus den Configuration Manager-Installationsmedien auf dem Dienstverbindungspunkt: `C:\Source`

- Der Pfad zu einem USB-Laufwerk, auf dem Sie die Daten speichern, die zwischen Computern übertragen werden sollen: `D:\USB\`

- Der Name der Datendatei, die Sie vom Standort exportieren: `UsageData.cab`

- Der Name des leeren Ordners, in dem das Tool heruntergeladene Updates für Configuration Manager speichert: `UpdatePacks`

### <a name="prepare"></a>Vorbereiten

1. Öffnen Sie auf dem Computer, auf dem der Dienstverbindungspunkt gehostet wird, eine Eingabeaufforderung als Administrator, und wechseln Sie zum Speicherort des Tools. Beispiel:

    `cd C:\Source\SMSSETUP\TOOLS\ServiceConnectionTool\`

1. Führen Sie den folgenden Befehl aus, um die Datendatei vorzubereiten:

    `ServiceConnectionTool.exe -prepare -usagedatadest D:\USB\UsageData.cab`

    > [!NOTE]
    > Wenn Sie Datendateien aus mehr als einer Hierarchie gleichzeitig hochladen, sollten Sie jeder Datendatei einen eindeutigen Namen geben. Falls erforderlich, können Sie Dateien später umbenennen.

    Die Daten in der Datei basieren auf der Diagnoseebene und den Nutzungsdaten, die Sie für den Standort konfigurieren. Weitere Informationen finden Sie unter [Übersicht zu Diagnose- und Nutzungsdaten](../../plan-design/diagnostics/diagnostics-and-usage-data.md). Sie können das Tool verwenden, um die Daten in eine CSV-Datei zu exportieren und die Inhalte anzuzeigen. Weitere Informationen finden Sie unter [-export](#-export).

1. Nachdem das Tool den Export der Nutzungsdaten abgeschlossen hat, kopieren Sie die Datendatei auf einen Computer mit Internetzugriff.

### <a name="connect"></a>Verbinden

1. Öffnen Sie auf dem Computer mit Internetzugriff eine Eingabeaufforderung als Administrator, und wechseln Sie zum Speicherort des Tools. Dieser Speicherort stellt eine Kopie des gesamten **ServiceConnectionTool**-Ordners dar. Beispiel:

    `cd D:\USB\ServiceConnectionTool\`

1. Führen Sie den folgenden Befehl aus, um die Datendatei hoch- und die Configuration Manager-Updates herunterzuladen:

    `ServiceConnectionTool.exe -connect -usagedatasrc D:\USB -updatepackdest D:\USB\UpdatePacks`

    Weitere Beispiele finden Sie unter [Befehlszeilenparameter](#bkmk_cmd).

    > [!NOTE]  
    > Wenn Sie diese Befehlszeile ausführen, wird möglicherweise der folgende Fehler angezeigt:
    >
    > **Unhandled Exception: System.UnauthorizedAccessException: Access to the path 'C:\Users\jqpublic\AppData\Local\Temp\extractmanifestcab\95F8A562.sql' is denied.** (Ausnahmefehler: System.UnauthorizedAccessException: Der Zugriff auf den Pfad „C:\Users\jqpublic\AppData\Local\Temp\extractmanifestcab\95F8A562.sql“ wurde verweigert.)
    >
    > Sie können diesen Fehler gefahrlos ignorieren. Schließen Sie das Fehlerfenster, um den Vorgang fortzusetzen.

1. Nachdem das Tool die Updates heruntergeladen hat, kopieren Sie diese in den Dienstverbindungspunkt.

### <a name="import"></a>Importieren

1. Öffnen Sie auf dem Computer, auf dem der Dienstverbindungspunkt gehostet wird, eine Eingabeaufforderung als Administrator, und wechseln Sie zum Speicherort des Tools. Beispiel:

    `cd C:\Source\SMSSETUP\TOOLS\ServiceConnectionTool\`

1. Führen Sie folgenden Befehl aus, um die Updates zu importieren:

    `ServiceConnectionTool.exe -import -updatepacksrc D:\USB\UpdatePacks`

1. Schließen Sie nach Abschluss des Imports die Eingabeaufforderung. Es werden nur Updates für die entsprechende Hierarchie importiert.

1. Gehen Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, und wählen Sie den Knoten **Updates und Wartung** aus. Importierte Updates können jetzt installiert werden. Weitere Informationen finden Sie unter [Installieren konsoleninterner Updates](install-in-console-updates.md).

## <a name="log-files"></a>Protokolldateien

- **ServiceConnectionTool.log:** Jedes Mal, wenn Sie das Dienstverbindungstool ausführen, schreibt es in diese Protokolldatei. Diese Protokolldatei wird immer unter demselben Pfad wie das Tool gespeichert. Diese Protokolldatei enthält einfache Details zur Toolverwendung, die auf den von Ihnen verwendeten Parametern basieren. Jedes Mal, wenn Sie das Tool ausführen, ersetzt dieses die vorhandene Protokolldatei.

- **ConfigMgrSetup.log:** Während der [Verbindungsphase](#connect) schreibt das Tool in diese Protokolldatei im Stammverzeichnis des Systemlaufwerks. Diese Protokolldatei enthält ausführlichere Informationen, zum Beispiel, welche Dateien das Tool herunterlädt und ob die Hashüberprüfungen erfolgreich waren.

## <a name="command-line-parameters"></a><a name="bkmk_cmd"></a> Befehlszeilenparameter

In diesem Abschnitt werden alle verfügbaren Parameter für das Dienstverbindungstool in alphabetischer Reihenfolge aufgelistet.

### <a name="-connect"></a>-connect

Verwenden Sie diesen Parameter während der [Verbindungsphase](#connect) auf dem Computer mit Internetzugriff. Er stellt eine Verbindung mit dem Configuration Manager-Clouddienst her, um die Datendatei hoch- und Updates herunterzuladen.

Dafür sind die folgenden Parameter erforderlich:

- **-usagedatasrc:** der Speicherort der Datendatei, die hochgeladen werden soll
- **-updatepackdest:** ein Pfad für die heruntergeladenen Updates

Darüber hinaus können Sie auch die folgenden optionalen Parameter verwenden:

- **-proxyserveruri:** der vollqualifizierter Domänenname des Proxyservers
- **-proxyusername:** ein Benutzername für den Proxyserver
- **-downloadall:** Mit diesem Parameter werden unabhängig von der Standortversion alle Elemente heruntergeladen, einschließlich Updates und Hotfixes.
- **-downloadhotfix:** Mit diesem Parameter werden unabhängig von der Standortversion alle Hotfixes heruntergeladen.
- **-downloadsiteversion:** Mit diesem Parameter werden Updates und Hotfixes höherer Versionen als die Standortversion heruntergeladen.

#### <a name="example-of-connect-without-a-proxy-server"></a>Beispiel für „-connect“ ohne Proxyserver

`ServiceConnectionTool.exe -connect -usagedatasrc D:\USB\ -updatepackdest D:\USB\UpdatePacks`

#### <a name="example-of-connect-with-a-proxy-server"></a>Beispiel für „-connect“ mit Proxyserver

`ServiceConnectionTool.exe -connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks -proxyserveruri itproxy.contoso.com -proxyusername jqpublic`

#### <a name="example-of-connect-to-download-only-site-version-applicable-updates"></a>Beispiel für „-connect“ zum Herunterladen von Updates, die nur für die jeweilige Standortversion gelten

`ServiceConnectionTool.exe -connect -downloadsiteversion -usagedatasrc D:\USB -updatepackdest D:\USB\UpdatePacks`

### <a name="-dest"></a>-dest

Dies ist ein erforderlicher Parameter für den **-export**-Parameter, um den Pfad und den Dateinamen der zu exportierenden CSV-Datei anzugeben. Weitere Informationen finden Sie unter [-export](#-export).

### <a name="-downloadall"></a>-downloadall

Dies ist ein optionaler Parameter für den **-connect**-Parameter, um unabhängig von der Standortversion sämtliche Elemente herunterzuladen, einschließlich Updates und Hotfixes. Weitere Informationen finden Sie unter [-connect](#connect).

### <a name="-downloadhotfix"></a>-downloadhotfix

Dies ist ein optionaler Parameter für den **-connect**-Parameter, um unabhängig von der Standortversion alle Hotfixes herunterzuladen. Weitere Informationen finden Sie unter [-connect](#-connect).

### <a name="-downloadsiteversion"></a>-downloadsiteversion

Dies ist ein optionaler Parameter für den **-connect**-Parameter, um nur Updates und Hotfixes höherer Versionen als die Standortversion herunterzuladen. Weitere Informationen finden Sie unter [-connect](#-connect).

### <a name="-export"></a>-export

Dieser Parameter wird während der [Vorbereitungsphase](#prepare) zum Exportieren von Nutzungsdaten in eine CSV-Datei verwendet. Führen Sie diesen als Administrator auf dem Dienstverbindungspunkt aus. Mit dieser Aktion können Sie den Inhalt der Nutzungsdaten vor dem Hochladen für Microsoft überprüfen. Zum Angeben des Speicherorts der CSV-Datei wird der **-dest**-Parameter benötigt.

#### <a name="example-of-export"></a>Beispiel für „-export“

`-export -dest D:\USB\usagedata.csv`

### <a name="-import"></a>-import

Dieser Parameter wird während der [Importphase](#import) auf dem Dienstverbindungspunkt zum Importieren von Updates auf den Standort verwendet. Zum Angeben des Speicherorts der heruntergeladenen Updates wird der **-updatepacksrc**-Parameter benötigt.

#### <a name="example-of-import"></a>Beispiel für „-import“

`ServiceConnectionTool.exe -import -updatepacksrc D:\USB\UpdatePacks`

### <a name="-prepare"></a>-prepare

Dieser Parameter wird während der [Vorbereitungsphase](#prepare) auf dem Dienstverbindungspunkt zum Exportieren von Nutzungsdaten vom Standort verwendet. Zum Angeben des Speicherorts der exportierten Datendatei wird der **-usagedatadest**-Parameter benötigt.

#### <a name="example-of-prepare"></a>Beispiel für „-prepare“

`ServiceConnectionTool.exe -prepare -usagedatadest D:\USB\UsageData.cab`

### <a name="-proxyserveruri"></a>-proxyserveruri

Hierbei handelt es sich um einen optionalen Parameter für den **-connect**-Parameter, um den vollqualifizierten Domänennamen für Ihren Proxyserver anzugeben. Weitere Informationen finden Sie unter [-connect](#-connect).

### <a name="-proxyusername"></a>-proxyusername

Hierbei handelt es sich um einen **-connect**-Parameter, um den Benutzernamen für eine Authentifizierung beim Proxyserver anzugeben. Weitere Informationen finden Sie unter [-connect](#-connect).

### <a name="-updatepackdest"></a>-updatepackdest

Hierbei handelt es sich um einen erforderlichen Parameter für den **-connect**-Parameter, um einen Pfad für die heruntergeladenen Updates anzugeben. Weitere Informationen finden Sie unter [-connect](#-connect).

### <a name="-updatepacksrc"></a>-updatepacksrc

Hierbei handelt es sich um einen erforderlichen Parameter für den **-import**-Parameter, um einen Pfad für die heruntergeladenen Updates anzugeben. Weitere Informationen finden Sie unter [-import](#-import).

### <a name="-usagedatadest"></a>-usagedatadest

Hierbei handelt es sich um einen erforderlichen Parameter für den **-prepare**-Parameter, um einen Pfad und einen Dateinamen für die exportierte Datendatei anzugeben. Weitere Informationen finden Sie unter [-prepare](#-prepare).

## <a name="next-steps"></a>Nächste Schritte

[Installieren von konsoleninternen Updates](install-in-console-updates.md)

[Anzeigen von Diagnose- und Verwendungsdaten](../../plan-design/diagnostics/view-diagnostics-and-usage-data.md)
