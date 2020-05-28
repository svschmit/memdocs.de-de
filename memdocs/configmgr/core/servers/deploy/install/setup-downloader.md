---
title: Setupdownloadtool
titleSuffix: Configuration Manager
description: Mit dem eigenständigen Tool können Sie die aktuelle Version der für das Setup wesentlichen Installationsdateien herunterladen.
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2da8aed5cfe4a478010165445094f1fce4627d9a
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428831"
---
# <a name="setup-downloader-for-configuration-manager"></a>Setup-Downloadprogramm für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Bevor Sie das Configuration Manager-Setup ausführen, um einen Standort zu installieren oder zu aktualisieren, können Sie mit dem eigenständigen Setupdownloadtool die aktualisierten Setupdateien herunterladen. Führen Sie das Tool einfach in der Version von Configuration Manager aus, die Sie installieren möchten. Verwenden Sie aktualisierte Setupdateien, um sicherzustellen, dass Ihre Standortinstallation die aktuelle Version der wesentlichen Installationsdateien verwendet:

Wenn Sie das Setupdownloadprogramm verwenden, geben Sie einen Ordner an, der die Dateien enthalten soll. Das Konto, mit dem Sie das Tool ausführen, benötigt die Berechtigung **Vollzugriff** für den Downloadordner. Während des Setups zum Installieren oder Aktualisieren eines Standorts können Sie diese lokale Kopie von Dateien angeben, die Sie zuvor heruntergeladen haben. Dies verhindert, dass beim Setup eine Verbindung zu Microsoft hergestellt wird, wenn Sie die Installation oder das Upgrade des Standorts starten. Sie können die gleiche lokale Kopie der Setupdateien für weitere Standortinstallationen oder -upgrades derselben Version verwenden.

Das Setupdownloadtool lädt die folgenden Dateitypen herunter:

- Erforderliche verteilbare Dateien
- Sprachpakete
- Die neuesten Produktupdates für das Setup

Es gibt zwei Optionen für die Ausführung des Setupdownloadprogramms:

- Die Anwendung mit der Benutzeroberfläche ausführen
- Die Anwendung aufgrund zusätzlicher Befehlszeilenoptionen in einer Eingabeaufforderung ausführen

Wenn Ihre Organisation die Netzwerkkommunikation mit dem Internet über ein- Firewall oder Proxygerät einschränkt, müssen Sie dem Tool den Zugriff auf Internetendpunkte gestatten. Das Gerät, auf dem das Tool ausgeführt wird, benötigt Internetzugriff, so wie auch der Dienstverbindungspunkt. Weitere Informationen finden Sie unter [Internetzugriffsanforderungen](../../../plan-design/network/internet-endpoints.md#bkmk_scp).<!-- SCCMDocs#677 -->

## <a name="run-setup-downloader-with-the-user-interface"></a><a name="bkmk_ui"></a> Ausführen des Setupdownloadprogramms über die Benutzeroberfläche

1. Navigieren Sie auf einem Computer mit Internetzugriff zu den Installationsmedien für die Version von Configuration Manager, die Sie installieren möchten.

1. Führen Sie im Unterordner **SMSSETUP\BIN\X64** die Datei **Setupdl.exe** aus.

1. Geben Sie den Pfad zu dem Ordner ein, in dem die aktualisierten Installationsdateien gespeichert werden sollen, und klicken Sie dann auf **Herunterladen**. Das Setupdownloadprogramm überprüft die Dateien, die derzeit im Downloadordner enthalten sind. Es werden nur die Dateien heruntergeladen, die fehlen oder die neuer sind als vorhandene Dateien. Außerdem erstellt das Programm Unterordner für die heruntergeladenen Sprachen und weitere erforderliche Komponenten.

1. Die Downloadergebnisse können Sie sich unter **C:\ConfigMgrSetup.log** ansehen.

## <a name="run-setup-downloader-from-a-command-prompt"></a><a name="bkmk_cmd"></a> Ausführen des Setupdownloadprogramms in einer Eingabeaufforderung

1. Öffnen Sie eine Eingabeaufforderung, und ändern Sie den Pfad zu den Installationsmedien für die Version von Configuration Manager, die Sie installieren möchten.

1. Wechseln Sie in den Unterordner **SMSSETUP\BIN\X64**, und führen Sie **Setupdl.exe** mit den erforderlichen Optionen aus.

1. Die Downloadergebnisse können Sie sich unter **C:\ConfigMgrSetup.log** ansehen.

### <a name="command-line-options"></a>Befehlszeilenoptionen

Sie können die folgenden Befehlszeilenoptionen mit **Setupdl.exe** verwenden:

- **/VERIFY:** Mit dieser Option werden die Dateien im Downloadordner überprüft, einschließlich der Sprachdateien. Die Liste der veralteten Dateien finden Sie unter **C:\ConfigMgrSetup.log**. Wenn Sie diese Option verwenden, werden keine Dateien heruntergeladen.

- **/VERIFYLANG:** Mit dieser Option werden die Sprachdateien im Downloadordner überprüft. Die Liste der veralteten Sprachdateien finden Sie unter **C:\ConfigMgrSetup.log**.

- **/LANG:** Mit dieser Option werden nur die Sprachdateien in den Downloadordner heruntergeladen.

- **/NOUI:** Mit dieser Option wird das Setupdownloadprogramm ohne Verwendung der Benutzeroberfläche gestartet. Wenn Sie diese Option verwenden, ist der **Downloadpfad** erforderlich.

- **Download path** (Downloadpfad): Damit die Überprüfungs- oder der Download automatisch gestartet wird, müssen Sie den Pfad zum Downloadordner angeben. Wenn Sie die Option **/NOUI** verwenden, ist der Downloadpfad erforderlich. Wenn Sie keinen Downloadpfad angeben, werden Sie vom Setupdownloadprogramm aufgefordert, den Pfad anzugeben. Wenn der Ordner nicht vorhanden ist, wird er vom Setupdownloadprogramm erstellt.

### <a name="example-commands"></a>Beispielbefehle

#### <a name="example-1"></a>Beispiel 1

Das Setupdownloadprogramm überprüft die Dateien im angegebenen Downloadordner und lädt anschließend Dateien herunter.

`setupdl.exe C:\Download`

#### <a name="example-2"></a>Beispiel 2

Das Setupdownloadprogramm überprüft nur die Dateien im angegebenen Downloadordner.

`setupdl.exe /VERIFY C:\Download`

#### <a name="example-3"></a>Beispiel 3

Das Setupdownloadprogramm überprüft die Dateien im angegebenen Downloadordner und lädt anschließend Dateien herunter. Das Tool weist keine Benutzeroberfläche auf.

`setupdl.exe /NOUI C:\Download`

#### <a name="example-4"></a>Beispiel 4

Das Setupdownloadprogramm überprüft die Sprachdateien im angegebenen Downloadordner und lädt anschließend nur die Sprachdateien herunter.

`setupdl.exe /LANG C:\Download`

## <a name="copy-setup-downloader-files-to-another-computer"></a><a name="bkmk_cp-files"></a> Kopieren von Dateien des Setupdownloadprogramms auf einen anderen Computer

1. Gehen Sie im Windows-Explorer zu einem der folgenden Speicherorte:

    - **&lt;Configuration Manager-Installationsmedium>\SMSSETUP\BIN\X64**

    - **&lt;Configuration Manager-Installationspfad>\BIN\X64**

1. Kopieren Sie die folgenden Dateien in denselben Zielordner auf dem anderen Computer:

    - **setupdl.exe**

    - **.\\&lt;Sprache>\\setupdlres.dll**

        > [!NOTE]
        > Diese Datei befindet sich im Unterordner für die Installationssprache. Englisch beispielsweise befindet sich im Unterordner `00000409`.

    Die Zielordnerpfade auf Ihrem Gerät wie folgt aussehen:

    - `C:\ConfigManInstall\setupdl.exe`

    - `C:\ConfigManInstall\00000409\setupdlres.dll`

1. Führen Sie das Setupdownloadprogramm auf dem Zielcomputer aus. Verwenden Sie dazu entweder die [Benutzeroberfläche](#bkmk_ui) oder die [Eingabeaufforderung](#bkmk_cmd).
