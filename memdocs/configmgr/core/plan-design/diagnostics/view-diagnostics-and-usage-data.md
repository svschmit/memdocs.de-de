---
title: Anzeigen von Diagnosedaten
titleSuffix: Configuration Manager
description: Zeigen Sie Diagnose- und Nutzungsdaten an, um zu bestätigen, dass die Configuration Manager-Hierarchie keine vertraulichen Informationen enthält.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 594eb284-0d93-4c5d-9ae6-f0f71203682a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 993a3549ddca4c2b5ae1dbbfc0346f28b9c3083e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692738"
---
# <a name="how-to-view-diagnostics-and-usage-data-for-configuration-manager"></a>So rufen Sie Diagnose- und Nutzungsdaten für Configuration Manager ab

*Gilt für: Configuration Manager (Current Branch)*

Sie können in Ihrer Configuration Manager-Hierarchie Diagnose- und Nutzungsdaten abrufen, um sicherzustellen, dass keine sensiblen oder identifizierbaren Informationen enthalten sind. Der Standort fasst seine Diagnosedaten zusammen und speichert sie in der Tabelle **TEL_TelemetryResults** der Standortdatenbank. Er formatiert die Daten so, dass sie programmgesteuert verwendbar und effizient sind.

In diesem Artikel erhalten Sie einen Überblick über die genauen Daten, die an Microsoft gesendet werden. Diese Informationen dürfen nicht für andere Zwecke (z. B. die Datenanalyse) verwendet werden.  

## <a name="view-data-in-database"></a>Abrufen von Daten in der Datenbank

Verwenden Sie den folgenden SQL-Befehl, um den Inhalt dieser Tabelle und die Daten abzurufen, die gesendet werden:  

``` SQL
SELECT * FROM TEL_TelemetryResults
```

## <a name="export-the-data"></a>Exportieren der Daten

Wenn sich der Dienstverbindungspunkt im Offlinemodus befindet, können Sie die aktuellen Daten mit dem Dienstverbindungstool in eine durch Trennzeichen getrennte Datei (CSV) exportieren. Führen Sie das Dienstverbindungstool auf dem Dienstverbindungspunkt mit dem Parameter **-Export** aus.

Weitere Informationen finden Sie unter [Use the service connection point (Verwenden des Dienstverbindungspunkts)](../../servers/manage/use-the-service-connection-tool.md).

## <a name="one-way-hashes"></a><a name="bkmk_hashes"></a> Unidirektionale Hashes

Einige Daten bestehen aus Zeichenfolgen aus zufälligen alphanumerischen Zeichen. Configuration Manager verwendet den SHA-256-Algorithmus, um unidirektionale Hashes zu erstellen. Dadurch wird sichergestellt, dass Microsoft keine potenziell sensiblen Daten erfasst. Die Hashdaten können weiterhin zu Korrelations- und Vergleichszwecken verwendet werden.

Anstatt z. B. die Namen von Tabellen in der Standortdatenbank zu erfassen, wird für jeden Tabellennamen ein unidirektionaler Hash erfasst. Dadurch wird sichergestellt, dass benutzerdefinierte Tabellennamen nicht sichtbar sind. Microsoft führt dann denselben unidirektionalen Hashprozess der SQL-Standardtabellennamen aus. Wenn Sie die Ergebnisse der beiden Abfragen vergleichen, wird die Abweichung des Datenbankschemas von der Standardeinstellung des Produkts bestimmt. Diese Informationen werden anschließend verwendet, um Updates zu verbessern, die Änderungen des SQL-Schemas erforderlich machen.  

Beim Anzeigen der Rohdaten enthält jede Datenzeile einen allgemeinen Hashwert. Dies ist die Hierarchie-ID. Sie wird verwendet, um eine Korrelation zwischen den Daten und der Hierarchie herzustellen, ohne den Kunden oder die Quelle zu identifizieren.

### <a name="how-the-one-way-hash-works"></a>So funktioniert ein unidirektionaler Hash

1. Rufen Sie die Hierarchie-ID ab, indem Sie die folgende SQL-Anweisung in SQL Server Management Studio auf die Configuration Manager-Datenbank anwenden:

    ``` SQL
    select [dbo].[fnGetHierarchyID]()
    ```

2. Verwenden Sie das folgende Windows PowerShell-Skript, um den unidirektionalen Hash Ihrer Hierarchie-ID anzuwenden.  

    ``` PowerShell
    Param( [Parameter(Mandatory=$True)] [string]$value )  
      $guid = [System.Guid]::NewGuid()  
      if( [System.Guid]::TryParse($value,[ref] $guid) -eq $true ) {  
      #many of the values we hash are Guids  
      $bytesToHash = $guid.ToByteArray()  
    } else {  
      #otherwise hash as string (unicode)  
      $ue = New-Object System.Text.UnicodeEncoding  
      $bytesToHash = $ue.GetBytes($value)
    }  
      # Load Hash Provider (https://en.wikipedia.org/wiki/SHA-2)
    $hashAlgorithm = [System.Security.Cryptography.SHA256Cng]::Create()
    # Hash the input
    $hashedBytes = $hashAlgorithm.ComputeHash($bytesToHash)
    # Base64 encode the result for transport
    $result = [Convert]::ToBase64String($hashedBytes)
    return $result
    ```

3. Vergleichen Sie die Skriptausgabe mit der GUID in den Rohdaten. Dieser Prozess zeigt, wie die Daten verborgen werden.

## <a name="next-steps"></a>Nächste Schritte

> [!div class="nextstepaction"]
> [Ebenen von Nutzungsdaten zu Diagnosezwecken](levels-overview.md)
