---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 10/04/2019
ms.openlocfilehash: 5d65b2c250890c10c16214bcee385c39a4f58204
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697928"
---
### <a name="hardware-inventory-reports"></a><a name="ki_hinv"></a> Berichte zum Hardwarebestand

<!--5468413-->
Wenn Sie einen Bericht ausführen, der auf einem Hardwarebestand basiert, wird ein Fehler zurückgegeben. Ein BitLocker-Bericht gibt beispielsweise einen Fehler ähnlich der folgenden Meldung zurück:

```
Microsoft.Reporting.WinForms.ReportServerException
An error has occurred during report processing. (rsProcessingAborted)
```

Möglicherweise wird auch in der Datei **dataldr.log** folgender Fehler angezeigt:

`[42S22][207][Microsoft][SQL Server Native Client 11.0][SQL Server]Invalid column name 'FileTimeStamp00'. : pOFFICE_ADDIN_DATA`

Konsolendashboards, die auf dem Hardwarebestand basieren, sind möglicherweise auch beeinträchtigt.

Dieses Problem wird durch eine Änderung des Datenbankschemas in bestimmten Hardwarebestandstabellen verursacht.

#### <a name="workaround"></a>Problemumgehung

Die Problemumgehung besteht darin, das vorhandene Attribut aus der Datenbank zu löschen. Die Standortkomponente zum Laden von Daten kann dann ein neues Attribut erstellen. Führen Sie das folgende SQL-Skript auf dem Standortdatenbankserver aus, um das Tabellenschema zu korrigieren:

``` SQL
IF NOT EXISTS (SELECT * FROM SYS.columns WHERE name = 'FileTimestamp00' AND object_id = OBJECT_ID('OFFICE_ADDIN_DATA'))
BEGIN
       DELETE am
       FROM AttributeMap am
       INNER JOIN GroupMap gm ON am.GroupKey=gm.GroupKey
       WHERE gm.GroupClass='MICROSOFT|OFFICE_ADDIN|1.0'
       AND am.AttributeName='FileTimeStamp'

       PRINT 'Fix OFFICE_ADDIN_DATA schema'
END
```
