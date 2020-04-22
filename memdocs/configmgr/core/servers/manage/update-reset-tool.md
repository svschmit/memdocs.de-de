---
title: Tool zum Zurücksetzen von Updates
titleSuffix: Configuration Manager
description: Verwenden Sie das Tool zum Zurücksetzen von Updates für konsoleninterne Updates für Configuration Manager.
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 25fa89d6-7e47-45a6-8f4e-70b77560fba6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b4aa67280c879d6f7feaf549ac7f13ba0136ca91
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704328"
---
# <a name="update-reset-tool"></a>Tool zum Zurücksetzen von Updates

*Gilt für: Configuration Manager (Current Branch)*  


Ab Version 1706 enthalten primäre Standorte von Configuration Manager und Standorte der zentralen Verwaltung das Configuration Manager-Tool zum Zurücksetzen von Updates **CMUpdateReset.exe**. Mit diesem Tool können Sie Probleme beheben, die bei konsoleninternen Updates während des Herunterladens oder Replizierens auftreten. Das Tool befindet sich auf dem Standortserver im Ordner ***\cd.latest\SMSSETUP\TOOLS***.

Sie können dieses Tool mit jeder Version (Current Branch) verwenden, die weiterhin unterstützt wird.

Der Einsatz dieses Tools ist erforderlich, wenn ein [konsoleninternes Update](install-in-console-updates.md) nicht vollständig installiert wurde und sich in einem fehlerhaften Zustand befindet. Unter „fehlerhafter Zustand“ wird verstanden, dass das Update zwar heruntergeladen wird, der Vorgang jedoch deutlich länger als üblich dauert. „Deutlich länger als üblich“ bedeutet, dass das Herunterladen von Update-Paketen mit vergleichbarer Größe viele Stunden mehr in Anspruch nimmt, als Sie es von früheren Updates gewohnt sind. Es kann sich auch um einen Fehler beim Replizieren des Updates an untergeordnete primäre Standorte handeln.  

Wenn Sie das Tool ausführen, wird es für das Update ausgeführt, das Sie angeben. Erfolgreich installierte oder heruntergeladene Updates werden von diesem Tool standardmäßig nicht gelöscht.  

### <a name="prerequisites"></a>Voraussetzungen
Das Konto, das Sie verwenden, um das Tool auszuführen, benötigt die folgenden Berechtigungen:
- Die Berechtigungen **Lesen** und **Schreiben** für die Standortdatenbank des Standorts der zentralen Verwaltung und jeden primären Standort in Ihrer Hierarchie Zum Festlegen dieser Berechtigungen können Sie das Benutzerkonto der Configuration Manager-Datenbank an jedem Standort als Mitglied der [festen Datenbankrollen](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles) **db_datawriter** und **db_datareader** hinzufügen. Das Tool interagiert nicht mit sekundären Standorten.
- **Lokaler Administrator** am Standort der obersten Ebene Ihrer Hierarchie.
- **Lokaler Administrator** auf dem Computer, der den Dienstverbindungspunkt hostet.

Sie benötigen die GUID des Updatepakets, das Sie zurücksetzen möchten. So rufen Sie die GUID ab
  1.   Navigieren Sie in der Konsole zu **Verwaltung** > **Updates und Wartung**.
  2.   Klicken Sie im Anzeigebereich mit der rechten Maustaste auf die Überschrift einer der Spalten (z.B. **Status**), und wählen Sie anschließend **Paket-GUID** aus, um diese Spalte der Anzeige hinzuzufügen.
  3.   In der Spalte wird nun die Paket-GUID des Updates angezeigt.

> [!TIP]  
> Um die GUID zu kopieren, wählen Sie die Zeile des Updatepakets aus, das Sie zurücksetzen möchten, und drücken dann STRG+C, um diese Zeile zu kopieren. Wenn Sie die kopierte Auswahl in einen Text-Editor einfügen, können Sie anschließend nur die GUID zur Verwendung als Befehlszeilenparameter kopieren, wenn Sie das Tool ausführen.

### <a name="run-the-tool"></a>Ausführen des Tools    
Das Tool muss für den Standort der obersten Ebene der Hierarchie ausgeführt werden.

Wenn Sie das Tool ausführen, verwenden Sie Befehlszeilenparameter, um Folgendes anzugeben:
- den SQL Server am Standort der obersten Ebene in der Hierarchie
- den Namen der Standortdatenbank am Standort der obersten Ebene
- die GUID des Updatepakets, das Sie zurücksetzen möchten

Das Tool ermittelt anhand des Updatestatus die zusätzlichen Server, auf die es Zugriff benötigt.   

Wenn das Updatepaket den Status*Nach Download* hat, wird das Paket nicht vom Tool bereinigt. Optional können Sie das Entfernen eines erfolgreich heruntergeladenen Updates mithilfe des Parameters „FDELETE“ erzwingen (siehe die Befehlszeilenparameter weiter unten in diesem Thema).

Nach Ausführung des Tools:
- Wenn ein Paket gelöscht wurde, starten Sie den SMS_Executive-Dienst am Standort der obersten Ebene neu. Überprüfen Sie anschließend, ob Updates zur Verfügung stehen, damit Sie das Paket erneut herunterladen können.
- Wenn ein Paket nicht gelöscht wurde, sind keine Maßnahmen erforderlich. Das Update wird zuerst erneut initialisiert. Anschließend wird die Replikation oder Installation neu gestartet.

**Befehlszeilenparameter**  


|                        Parameter                         |                                                       Beschreibung                                                        |
|----------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| **-S &lt;Vollqualifizierter Domänenname der SQL Server-Instanz Ihres Standorts der obersten Ebene>** | *Erforderlich* <br> Geben Sie den vollqualifizierten Domänennamen der SQL Server-Instanz an, die die Standortdatenbank für den Standort der obersten Ebene Ihrer Hierarchie hostet. |
|                **-D &lt;Datenbankname>**                 |                          *Erforderlich* <br> Geben Sie den Namen der Datenbank am Standort der obersten Ebene an.                          |
|                 **-P &lt;Paket-GUID>**                 |                        *Erforderlich* <br> Geben Sie die GUID des Updatepakets an, das Sie zurücksetzen möchten.                        |
|           **-I &lt;SQL Server-Instanzname>**           |                    *Optional* <br> Bestimmen Sie die SQL Server-Instanz, die die Standortdatenbank hostet.                     |
|                       **-FDELETE**                       |                       *Optional* <br> Erzwingen Sie das Löschen eines erfolgreich heruntergeladenen Updatepakets.                        |

**Beispiele:**  
In einem typischen Szenario möchten Sie ein Update zurücksetzen, wenn beim Herunterladen Probleme aufgetreten sind. Der vollqualifizierte Domänenname Ihrer SQL Server-Instanz lautet *server1.fabrikam.com*, die Standortdatenbank heißt *CM_XYZ*, und die Paket-GUID lautet *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Führen Sie Folgendes aus: ***CMUpdateReset.exe -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

In einem extremeren Szenario möchten Sie das Löschen eines problematischen Updatepakets erzwingen. Der vollqualifizierte Domänenname Ihrer SQL Server-Instanz lautet *server1.fabrikam.com*, die Standortdatenbank heißt *CM_XYZ*, und die Paket-GUID lautet *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Führen Sie Folgendes aus: ***CMUpdateReset.exe  -FDELETE -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***
