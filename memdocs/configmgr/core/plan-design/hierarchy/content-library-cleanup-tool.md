---
title: Inhaltsbibliothek-Bereinigungstool
titleSuffix: Configuration Manager
description: Verwenden Sie das Inhaltsbibliotheks-Bereinigungstool zum Entfernen von verwaistem Inhalt, der nicht mehr einer Configuration Manager-Bereitstellung zugeordnet ist.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 226cbbb2-9afa-4e2e-a472-be989c0f0e11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8b1b415d5c24800f003f730426216ac7cf190a4f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703628"
---
# <a name="content-library-cleanup-tool"></a>Inhaltsbibliothek-Bereinigungstool

*Gilt für: Configuration Manager (Current Branch)*

Verwenden Sie das Befehlszeilentool zum Bereinigen der Inhaltsbibliothek, um Inhalte zu entfernen, die nicht mehr einem Paket oder einer Anwendung auf einem Verteilungspunkt zugeordnet sind. Diese Art von Inhalt wird *verwaister Inhalt* genannt. Dieses Tool ersetzt ältere Versionen von ähnlichen Tools, die für frühere Configuration Manager-Produkte veröffentlicht wurden.  

Das Tool wirkt sich nur auf den Inhalt auf dem Verteilungspunkt aus, den Sie angeben, wenn Sie das Tool ausführen. Das Tool kann keinen Inhalt aus der Inhaltsbibliothek auf dem Standortserver entfernen.

Suchen Sie auf dem Standortserver unter `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` nach **ContentLibraryCleanup.exe**.



## <a name="requirements"></a>Anforderungen  

- Führen Sie das Tool immer nur für einen Verteilungspunkt aus.  

- Sie können das Tool direkt auf dem Computer, der den Verteilungspunkt hostet, oder remote über einen anderen Computer ausführen.  

- Das Benutzerkonto, das zum Ausführen des Tools verwendet wird, muss in Configuration Manager über die gleichen Berechtigungen wie die Sicherheitsrolle **Hauptadministrator** verfügen.  



## <a name="modes-of-operation"></a>Betriebsmodi

Führen Sie das Tool in den folgenden zwei Modi aus: [Was-wäre-wenn](#what-if-mode) und [Löschen](#delete-mode).

> [!Tip]  
> Beginnen Sie mit dem Modus *Was-wäre-wenn*. Wenn Sie mit den Ergebnissen zufrieden sind, führen Sie das Tool im Modus *Löschen* aus.  


### <a name="what-if-mode"></a>Was-wäre-wenn-Modus   

Wenn Sie den `/delete`-Parameter nicht angeben, wird das Tool im Modus „Was-wäre-wenn“ ausgeführt. In diesem Modus wird der Inhalt identifiziert, der vom Verteilungspunkt gelöscht werden würde.

- Wenn das Tool in diesem Modus ausgeführt wird, löscht es keine Daten.  

- Das Tool schreibt Informationen über den Inhalt in die Protokolldatei, der gelöscht werden würde. Sie werden nicht für jeden potenziellen Löschvorgang dazu aufgefordert, diesen zu bestätigen.  


### <a name="delete-mode"></a>Löschmodus   

Wenn Sie das Tool mit dem `/delete`-Parameter ausführen, wird das Tool im Löschmodus ausgeführt.

- Wenn es in diesem Modus ausgeführt wird, können verwaiste Inhalte, die auf dem angegebenen Verteilungspunkt gefunden werden, aus der Inhaltsbibliothek des Verteilungspunktes gelöscht werden.  

- Vergewissern Sie sich vor dem Löschen jeder Datei, dass diese gelöscht werden sollte. Klicken Sie auf **J** für „Ja“, **N** für „Nein“, oder **Ja, alle**, um weitere Aufforderungen zu überspringen und alle verwaisten Inhalte zu löschen.  


### <a name="log-file"></a>Protokolldatei

Wenn das Tool in einem dieser Modi ausgeführt wird, wird automatisch ein Protokoll erstellt. Die Protokolldatei wird mit folgenden Informationen benannt: 
- Der Modus, in dem das Tool ausgeführt wurde  
- Der Name des Verteilungspunkts  
- Datum und Uhrzeit der Ausführung  

Wenn das Tool fertig ist, wird automatisch die Protokolldatei in Windows geöffnet. 

Das Tool schreibt die Protokolldatei standardmäßig in den temporären Ordner des Benutzerkontos, mit dem das Tool ausgeführt wurde. Dieser Speicherort befindet sich auf dem Computer, auf dem das Tool ausgeführt wurde, was nicht immer der Computer ist, für den das Tool ausgeführt wurde. Verwenden Sie den `/log`-Parameter, um die Protokolldatei an einen anderen Speicherort, einschließlich einer Netzwerkfreigabe, weiterzuleiten.



## <a name="run-the-tool"></a>Ausführen des Tools

So führen Sie das Tool aus: 

1. Öffnen Sie eine Eingabeaufforderung als Administrator. Ändern Sie das Verzeichnis in den Ordner, der die Datei **ContentLibraryCleanup.exe** enthält.  

2. Geben Sie eine Befehlszeile ein, die die erforderlichen [Befehlszeilenparameter](#bkmk_params) und optionale Parameter Ihrer Wahl enthält.



## <a name="command-line-parameters"></a><a name="bkmk_params"></a> Befehlszeilenparameter  

Sie können diese Befehlszeilenparameter in beliebiger Reihenfolge verwenden.   

### <a name="required-parameters"></a>Erforderliche Parameter

|Parameter|Details|
|---------|-------|
| `/dp <distribution point FQDN>`  | Geben Sie den vollständig qualifizierten Domänennamen (FQDN) des zu bereinigenden Verteilungspunkts an. |
| `/ps <primary site FQDN>` | Nur *erforderlich*, wenn Inhalt von einem Verteilungspunkt an einem sekundären Standort bereinigt wird. Das Tool stellt eine Verbindung mit dem übergeordneten primären Standort her, um Abfragen des SMS-Anbieters auszuführen. Mithilfe dieser Abfragen kann das Tool bestimmen, welcher Inhalt auf dem Verteilungspunkt sein sollte. Dann kann es den zu entfernenden verwaisten Inhalt identifizieren. Die Verbindung zum übergeordneten primären Standort muss für Verteilungspunkte an einem sekundären Standort hergestellt werden, da die erforderlichen Angaben nicht direkt am sekundären Standort zur Verfügung stehen.|
| `/sc <primary site code>`  | Nur *erforderlich*, wenn Inhalt von einem Verteilungspunkt an einem sekundären Standort bereinigt wird. Geben Sie den Standortcode des übergeordneten primären Standorts an. |

#### <a name="example-scan-and-log-what-content-it-would-delete-what-if"></a>Beispiel: Überprüfen und Protokollieren, welcher Inhalt gelöscht werden würde („was-wäre-wenn“)
`ContentLibraryCleanup.exe /dp server1.contoso.com`

#### <a name="example-scan-and-log-content-for-a-dp-at-a-secondary-site"></a>Beispiel: Überprüfen und Protokollieren von Inhalt für einen Verteilungspunkt an einem sekundären Standort
`ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com /sc ABC` 


### <a name="optional-parameters"></a>Optionale Parameter

|Parameter|Details|
|---------|-------|
|`/delete`| Verwenden Sie diesen Parameter, wenn Sie bereit sind, Inhalt vom Verteilungspunkt zu löschen. Sie werden zur Eingabe aufgefordert, bevor Inhalt gelöscht wird. </br></br> Wenn Sie diesen Parameter nicht verwenden, protokolliert das Tool die Ergebnisse dazu, welchen Inhalt es löschen würde. Ohne diesen Parameter wird kein Inhalt vom Verteilungspunkt gelöscht. |
| `/q` | Mit diesem Parameter wird das Tool im stillen Modus ausgeführt, wodurch alle Eingabeaufforderungen unterdrückt werden. Zu diesen Eingabeaufforderungen gehört auch das Löschen von Inhalt. Außerdem wird die Protokolldatei nicht automatisch geöffnet. |
| `/ps <primary site FQDN>` | Nur optional, wenn Inhalte eines Verteilungspunkts an einem primären Standort bereinigt werden. Geben Sie den FQDN des primäres Standorts an, zu dem der Verteilungspunkt gehört. |
| `/sc <primary site code>` | Nur optional, wenn Inhalte eines Verteilungspunkts an einem primären Standort bereinigt werden. Geben Sie den Standortcode des primäres Standorts an, zu dem der Verteilungspunkt gehört. |
| `/log <log file directory>` | Geben Sie den Speicherort an, in den das Tool die Protokolldatei schreibt. Dieser Speicherort kann sich auf einem lokalen Laufwerk oder auf einer Netzwerkfreigabe befinden.</br></br> Wenn Sie diesen Parameter nicht verwenden, platziert das Tool die Protokolldatei im temporären Verzeichnis des Benutzers auf dem Computer, auf dem das Tool ausgeführt wird.|

#### <a name="example-delete-content"></a>Beispiel: Inhalt löschen 
`ContentLibraryCleanup.exe /dp server1.contoso.com /delete`

#### <a name="example-delete-content-without-prompts"></a>Beispiel: Löschen von Inhalt ohne Eingabeaufforderungen
`ContentLibraryCleanup.exe /q /dp server1.contoso.com /delete` 

#### <a name="example-log-to-local-drive"></a>Beispiel: Erstellen des Protokolls auf einem lokalen Laufwerk
`ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop` 

#### <a name="example-log-to-network-share"></a>Beispiel: Erstellen des Protokolls auf einer Netzwerkfreigabe
`ContentLibraryCleanup.exe /dp server1.contoso.com /log \\server\share`


### <a name="known-issue"></a>Bekanntes Problem

Wenn ein Paket oder eine Bereitstellung fehlgeschlagen oder in Bearbeitung ist, kann das Tool die folgende Fehlermeldung zurückgeben: `System.InvalidOperationException: This content library cannot be cleaned up right now because package <packageID> is not fully installed.`

Hierfür gibt es momentan keine Problemumgehung. Das Tool kann verwaiste Dateien nicht zuverlässig identifizieren, wenn der Inhalt in Bearbeitung ist oder nicht bereitgestellt werden konnte. Das Tool lässt nicht zu, dass Sie Inhalt bereinigen, bis Sie das Problem behoben haben.
