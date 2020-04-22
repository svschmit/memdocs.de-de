---
title: Protokollsammler
titleSuffix: Configuration Manager
description: Der Protokollsammler kann hilfreich bei der Problembehandlung in Desktop Analytics sein.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 349b2a69-af46-481f-afb2-24d98774e852
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c101e45eb794ff73599e9612a5aec991be01ae6c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701718"
---
# <a name="desktop-analytics-log-collector"></a>Desktop Analytics-Protokollsammler

Ab Configuration Manager, Version 1906, können Sie das Tool **DesktopAnalyticsLogsCollector.ps1** aus dem Installationsverzeichnis von Configuration Manager zum Behandeln von Problemen beim Registrieren von Geräten in Desktop Analytics verwenden. Es führt einige grundlegende Schritte zur Problembehandlung aus und sammelt die relevanten Protokolle in einem einzelnen Arbeitsverzeichnis. Sie können diesen Inhalt mit dem Microsoft-Support teilen.


## <a name="prerequisites"></a>Voraussetzungen

- Ein Desktop Analytics-Client, auf dem Windows 10, Windows 8.1 oder Windows 7 mit Service Pack 1 ausgeführt wird

- Führen Sie das Skript auf dem Gerät als Administrator aus, und wählen Sie **Als Administrator ausführen** aus.

    > [!Tip]
    > Zusammen mit diesem Tool können Sie die Configuration Manager-Funktion **Skripts** verwenden. Weitere Informationen finden Sie unter [Beispiel 5: Bereitstellen des Skripts über die Configuration Manager-Funktion **Skripts**](#bkmk_ex5).

- Für Windows 7 mit Service Pack 1, PowerShell-Version 4.0 oder höher
    - [.NET Framework, Version 4.6 oder höher](https://dotnet.microsoft.com/download/dotnet-framework)

    - Windows Management Framework [Version 4.0](https://support.microsoft.com/help/2819745) (aka.ms/wmf4download) oder [Version 5.1](https://www.microsoft.com/download/details.aspx?id=54616) (aka.ms/wmf5download)

## <a name="usage"></a>Verwendung

Rufen Sie das Skript aus dem Configuration Manager-Installationsinhalt ab: `SMSSETUP\TOOLS\DesktopAnalyticsLogsCollector\DesktopAnalyticsLogsCollector.ps1`

``` Syntax
DesktopAnalyticsLogsCollector.ps1
    [-LogPath] <String>
    [-LogMode] <Int16>
    [-CollectNetTrace] <Int16>
    [-CollectUTCTrace] <Int16>
```

## <a name="parameters"></a>Parameter

### `-LogPath`

Gibt einen lokalen Pfad oder UNC-Pfad zum Ablegen des Protokolls und anderer Ausgabedateien an.

**Werte**:

- Lokaler Pfad (maximale Länge = 130), beispielsweise: `c:\myfolder`

- UNC-Pfad (maximale Länge = 130), beispielsweise: `\\myserver\myfolder`

**Typ:** Zeichenfolge

**Position**: 1

**Standardwert**: `$Env:SystemDrive\M365AnalyticsLogs` (Wenn dieser Parameter gleich null, leer oder Leerraum ist, erstellt das Skript unter dem Systemlaufwerk den Ordner M365AnalyticsLogs.)

### `-LogMode`

Gibt die Ausführlichkeitsstufe der Protokolle an.

**Werte**:

- `0`: Skriptmeldungen werden nur im PowerShell-Befehlsfenster protokolliert.

- `1`: Skriptmeldungen werden in der Protokolldatei unter dem Ausgabeordner und im PowerShell-Befehlsfenster protokolliert.

- `2`: Skriptmeldungen werden nur in der Protokolldatei unter dem Ausgabeordner protokolliert.

**Typ:** Int16

**Position**: 2

**Standardwert**: `1` (Skriptmeldungen werden in der Protokolldatei und im PowerShell-Befehlsfenster protokolliert.)

### `-CollectNetTrace`

Gibt an, ob die Netzwerkablaufverfolgung vom Skript erfasst wird.

**Werte**:

- `0`: Die Netzwerkablaufverfolgung wird nicht aktiviert.

- `1` (beliebiger ganzzahliger Wert ungleich null): Die Netzwerkablaufverfolgung wird aktiviert, und Ergebnisse werden erfasst.

**Typ:** Int16

**Position**: 3

**Standardwert**: `0` (Die Netzwerkablaufverfolgung wird nicht aktiviert.)

### `-CollectUTCTrace`

Gibt an, ob das Skript die Windows-UTC-Ablaufverfolgung erfasst und die Konnektivitätsdiagnose ausführt.

**Werte**:

- `0`: Die UTC-Ablaufverfolgung wird nicht aktiviert, und die Konnektivitätsdiagnose wird nicht ausgeführt.

- `1` (beliebiger ganzzahliger Wert ungleich null): Die UTC-Ablaufverfolgung wird aktiviert, die Konnektivitätsdiagnose wird ausgeführt, und Ergebnisse werden erfasst.

**Typ:** Int16

**Position**: 4

**Standardwert**: `0` (Die UTC-Ablaufverfolgung wird nicht aktiviert, und die Konnektivitätsdiagnose wird nicht ausgeführt.)


## <a name="output"></a>Ausgabe

Das Skript erstellt einen *Arbeitsordner* unter dem angegebenen Pfad. Beispiel: **M365AnalyticsLogs_yy_MM_dd_HH_mm_ss**. Alle Ausgabedateien werden in diesen Arbeitsordner abgelegt.

Wenn Sie festlegen, dass das Skript in eine *Protokolldatei* schreibt, generiert es eine Protokolldatei im Arbeitsordner. Beispiel: **M365AnalyticsLogs_ yy_MM_dd_HH_mm_ss.txt**.

Das Skript generiert außerdem andere *Diagnosedateien* im Arbeitsordner. Beispiel:

- `installedKBs.txt`: Liste der auf dem Gerät installierten Windows-Updates
- `appcompat`: Daten zur Anwendungskompatibilität
- `Reg*.txt`: Reihe von Dateien mit exportierten Daten aus der Windows-Registrierung


## <a name="examples"></a>Beispiele

### <a name="example-1-run-script-via-powershell-command-window-with-default-values"></a><a name="bkmk_ex1"></a> Beispiel 1: Ausführen des Skripts über das PowerShell-Befehlsfenster mit Standardwerten

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1
```

### <a name="example-2-run-script-via-powershell-command-window-with-specified-parameters"></a><a name="bkmk_ex2"></a> Beispiel 2: Ausführen des Skripts über das PowerShell-Befehlsfenster mit angegebenen Parametern

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogPath "c:\testABC" -LogMode 0 -CollectNetTrace 0 -CollectUTCTrace 0
```

### <a name="example-3-run-script-via-powershell-command-window-with-specified-parameters-in-position"></a><a name="bkmk_ex3"></a> Beispiel 3: Ausführen des Skripts über das PowerShell-Befehlsfenster mit angegebenen Parametern in Position

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 "c:\testABC" 2 0 0
```

### <a name="example-4-run-script-via-powershell-command-window-with-specified-parameter-and-verbose-messages"></a><a name="bkmk_ex4"></a> Beispiel 4: Ausführen des Skripts über das PowerShell-Befehlsfenster mit angegebenem Parametern und ausführlichen Meldungen

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogMode 1 -Verbose
```

### <a name="example-5-deploy-script-via-configuration-manager-scripts"></a><a name="bkmk_ex5"></a> Beispiel 5: Bereitstellen des Skripts über die Configuration Manager-Funktion **Skripts**

Weitere Informationen finden Sie unter [Erstellen und Ausführen von PowerShell-Skripts über die Configuration Manager-Konsole](../apps/deploy-use/create-deploy-scripts.md).

„DesktopAnalyticsLogsCollector.ps1“ wird von Microsoft digital signiert. Möglicherweise müssen Sie das zugehörige Microsoft-Codesignaturzertifikat als vertrauenswürdigen Herausgeber auf dem Zielgerät hinzufügen.

1. Öffnen Sie die Eigenschaften des Skripts in Windows-Explorer. Wechseln Sie zur Registerkarte **Digitale Signaturen**, und wählen Sie **Details**aus.

2. Wählen Sie auf der Registerkarte **Allgemein** die Option **Zertifikat anzeigen** aus.

    > [!Note]
    > Wenn Sie das Zertifikat über andere Mechanismen verteilen möchten, exportieren Sie es zunächst in eine Datei. Wechseln Sie zur Registerkarte **Details**, und wählen Sie **In Datei kopieren** aus.

3. Wählen Sie **Zertifikat installieren** aus. Importieren Sie das Zertifikat, und platzieren Sie es im Speicher **Vertrauenswürdige Herausgeber**.


## <a name="see-also"></a>Weitere Informationen:

- [Problembehandlung bei Desktop Analytics](troubleshooting.md)

- [Erstellen und Ausführen von PowerShell-Skripts über die Configuration Manager-Konsole](../apps/deploy-use/create-deploy-scripts.md)
