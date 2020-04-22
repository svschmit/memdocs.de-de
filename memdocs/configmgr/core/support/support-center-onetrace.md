---
title: 'Supportcenter: OneTrace (Vorschau)'
titleSuffix: Configuration Manager
description: OneTrace ist eine neue Protokollanzeige im Supportcenter, die Verbesserungen gegenüber CMTrace aufweist.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4cde43d1-9b09-4601-b389-0776de451b4e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 150090556d63b1bdf0b35dc9b53b450137d7f9d3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707448"
---
# <a name="support-center-onetrace-preview"></a>Supportcenter: OneTrace (Vorschau)

<!--3555962-->

Ab Version 1906 ist OneTrace als neue Protokollanzeige im Supportcenter verfügbar. Die Funktionsweise ist CMTrace ähnlich und bietet die folgenden Verbesserungen:

- Ansicht im Registerkartenformat
- Andockbare Fenster
- Verbesserte Suchfunktionen
- Fähigkeit, Filter zu aktivieren, ohne die Protokollansicht zu verlassen
- Hinweise auf der Scrollleiste, um Gruppen von Fehlern schnell zu bestimmen
- Schnelles Öffnen von Protokollen bei großen Dateien

[![Screenshot der OneTrace-Protokollanzeige](media/3555962-onetrace.png)](media/3555962-onetrace.png#lightbox)

OneTrace funktioniert mit vielen Protokolldateitypen. Beispiele:

- Configuration Manager-Clientprotokolle
- Configuration Manager-Serverprotokolle
- Statusmeldungen
- Windows Update-ETW-Protokolldatei unter Windows 10
- Windows Update-Protokolldatei unter Windows 7 und Windows 8.1

## <a name="prerequisites"></a>Voraussetzungen

- .NET Framework Version 4.6 oder höher

## <a name="install"></a>Installation

OneTrace wird mit dem Supportcenter installiert. Den Installer für das Supportcenter finden Sie auf dem Standortserver unter dem Pfad `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`.

Standardmäßig wird die OneTrace-Anwendung hier installiert: `C:\Program Files (x86)\Configuration Manager Support Center\CMPowerLogViewer.exe`.

> [!Note]  
> Supportcenter und OneTrace arbeiten mit Windows Presentation Foundation (WPF). Diese Komponente ist unter Windows PE nicht verfügbar. Verwenden Sie CMTrace weiterhin in Startimages mit Tasksequenzbereitstellungen.  

## <a name="log-groups"></a>Protokollgruppen

<!--5559993-->

Seit Version 2002 unterstützt OneTrace anpassbare Protokollgruppen, ähnlich wie in der Funktion im Supportcenter. Mit Protokollgruppen können Sie alle Protokolldateien für ein einzelnes Szenario öffnen. OneTrace umfasst derzeit Gruppen für die folgenden Szenarios:

- Anwendungsverwaltung
- Kompatibilitätseinstellungen (auch als „Verwaltung gewünschter Konfigurationen“ bezeichnet)
- Softwareupdates

Wechseln Sie zum Anzeigen von Protokollgruppen zum Menü **Ansicht**, und wählen Sie **Protokollgruppen** aus.

![Screenshot der OneTrace-Protokollgruppe für die Anwendungsverwaltung](media/5559993-onetrace-log-groups.png)

### <a name="customize-log-groups"></a>Anpassen der Protokolldateigruppen

Sie können diese Gruppen anpassen, indem Sie die XML-Datei für die Konfiguration ändern, die sich standardmäßig unter folgendem Pfad befindet: `C:\Program Files (x86)\Configuration Manager Support Center\LogGroups.xml`.

Das folgende Beispiel ist ein Teil der Standardkonfigurationsdatei:

``` XML
<LogGroups>
  <LogGroup Name="Desired Configuration Management" GroupType="1" GroupFilePath="">
    <LogFile>CIAgent.log</LogFile>
    <LogFile>CIDownloader.log</LogFile>
    <LogFile>CIStateStore.log</LogFile>
    <LogFile>CIStore.log</LogFile>
    <LogFile>CITaskMgr.log</LogFile>
    <LogFile>ccmsdkprovider.log</LogFile>
    <LogFile>DCMAgent.log</LogFile>
    <LogFile>DCMReporting.log</LogFile>
    <LogFile>DcmWmiProvider.log</LogFile>
  </LogGroup>
</LogGroups>
```

Die `GroupType`-Eigenschaft akzeptiert die folgenden Werte:

- `0`: Unbekannt oder sonstige
- `1`: Configuration Manager-Clientprotokolle
- `2`: Configuration Manager-Serverprotokolle

Die `GroupFilePath`-Eigenschaft kann einen expliziten Pfad für die Protokolldateien enthalten. Wenn sie leer ist, beruht OneTrace auf der Registrierungskonfiguration für den Gruppentyp. Wenn Sie z. B. `GroupType=1` festlegen, sucht OneTrace standardmäßig automatisch in `C:\Windows\CCM\Logs` nach den Protokollen in der Gruppe. In diesem Beispiel müssen Sie `GroupFilePath` nicht angeben.

## <a name="see-also"></a>Weitere Informationen:

- [Protokollanzeige des Supportcenters](support-center-ui-reference.md#bkmk_log-viewer)

- [CMTrace](cmtrace.md)
