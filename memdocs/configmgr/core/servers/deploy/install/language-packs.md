---
title: Sprachpakete
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über die Sprachunterstützung, die in Configuration Manager zur Verfügung steht.
ms.date: 06/29/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cd74e5f5-33f6-4566-8c9d-d6a93bfe71ed
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 53aa7e932e782254f63b422526b315f3ce91f397
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906172"
---
# <a name="language-packs-in-configuration-manager"></a>Sprachpakete in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Dieser Artikel enthält technische Details zur Sprachunterstützung in Configuration Manager. Configuration Manager-Standortserver und -Clients gelten als sprachneutral. Fügen Sie Unterstützung für Anzeigesprachen hinzu, indem Sie **Serversprachpakete** oder **Clientsprachpakete** an einem Standort der zentralen Verwaltung und an primären Standorten installieren. Während der Standortinstallation wählen Sie die an diesem Standort zu unterstützenden Server- und Clientsprachen aus den verfügbaren Sprachpaketdateien aus.
 
Installieren Sie mehrere Sprachen an jedem Standort. Sie müssen nur die Sprachen installieren, die Sie verwenden.  

- Von jedem Standort werden mehrere Sprachen für Configuration Manager-Konsolen unterstützt.  

- Fügen Sie nur Unterstützung für die gewünschten Clientsprachen hinzu, indem Sie an jedem Standort individuelle Clientsprachpakete installieren.  

Wenn Sie Unterstützung für eine Sprache installieren, die folgenden Komponenten entspricht:  

- Die Anzeigesprache eines Computers: Sowohl die Configuration Manager-Konsole als auch die Clientbenutzeroberfläche, die auf dem Computer ausgeführt wird, zeigt Informationen in dieser Sprache an.  

- Die Spracheinstellung, die vom Webbrowser eines Computers verwendet wird: Verbindungen zu webbasierten Informationen, z. B. zum Anwendungskatalog oder zu SQL Server Reporting Services, werden in dieser Sprache angezeigt.  


Wenn Sie das Configuration Manager-Setup ausführen, werden Sprachpaketdateien als Teil der erforderlichen Komponenten und verteilbaren Dateien heruntergeladen. Sie können auch das [Setup-Downloadprogramm](setup-downloader.md) verwenden, um diese Dateien herunterzuladen, bevor Sie Setup ausführen.   



## <a name="server-languages"></a>Serversprachen  

Verwenden Sie die folgende Tabelle, um eine Gebietsschema-ID einer Sprache zuzuordnen, die auf Servern unterstützt werden soll. Weitere Informationen zu Gebietsschema-IDs finden Sie unter [Locale IDs assigned by Microsoft (Von Microsoft zugewiesene Gebietsschema-IDs)](https://docs.microsoft.com/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c).  

|Serversprache|Gebietsschema-ID (LCID)|Dreistelliger Code|  
|---------------------|------------------------|-----------------------|  
|Englisch (Standard)|0409|ENU|  
|Chinesisch (vereinfacht)|0804|CHS|  
|Chinesisch (traditionell, Taiwan)|0404|CHT|  
|Tschechisch|0405|CSY|  
|Niederländisch – Niederlande|0413|NLD|  
|Französisch|040c|FRA|  
|Deutsch|0407|DEU|  
|Ungarisch|040e|HUN|  
|Italienisch – Italien|0410|ITA|  
|Japanisch|0411|JPN|  
|Koreanisch|0412|KOR|  
|Polnisch|0415|PLK|  
|Portugiesisch – Brasilien|0416|PTB|  
|Portugiesisch – Portugal|0816|PTG|  
|Russisch|0419|RUS|  
|Spanisch – Spanien|0c0a|ESN|  
|Schwedisch|041d|SVE|  
|Türkisch|041f|TRK|  



## <a name="client-languages"></a>Clientsprachen  

Verwenden Sie die folgende Tabelle, um eine Gebietsschema-ID einer Sprache zuzuordnen, die auf Clientcomputern unterstützt werden soll. Weitere Informationen zu Gebietsschema-IDs finden Sie unter [Locale IDs assigned by Microsoft (Von Microsoft zugewiesene Gebietsschema-IDs)](https://docs.microsoft.com/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c).  

|Clientsprache|Gebietsschema-ID (LCID)|Dreistelliger Code|  
|---------------------|------------------------|-----------------------|  
|Englisch (Standard)|0409|DE|  
|Chinesisch (vereinfacht)|0804|CHS|  
|Chinesisch (traditionell, Taiwan)|0404|CHT|  
|Tschechisch|0405|CSY|  
|Dänisch|0406|DAN|  
|Niederländisch – Niederlande|0413|NLD|  
|Finnisch|040b|FIN|  
|Französisch|040c|FRA|  
|Deutsch|0407|DEU|  
|Griechisch|0408|ELL|  
|Ungarisch|040e|HUN|  
|Italienisch – Italien|0410|ITA|  
|Japanisch|0411|JPN|  
|Koreanisch|0412|KOR|  
|Norwegisch|0414|NOR|  
|Polnisch|0415|PLK|  
|Portugiesisch (Brasilien)|0416|PTB|  
|Portugiesisch (Portugal)|0816|PTG|  
|Russisch|0419|RUS|  
|Spanisch – Spanien|0c0a|ESN|  
|Schwedisch|041d|SVE|  
|Türkisch|041f|TRK|  


### <a name="mobile-device-client-languages"></a>Clientsprachen für mobile Geräte  
Wenn Sie die Unterstützung für Sprachen mobiler Geräte hinzufügen, werden alle unterstützen Clientsprachen für mobile Geräte einbezogen. Sie können keine einzelnen Sprachpakete für die Unterstützung mobiler Geräte auswählen.  



## <a name="identify-installed-language-packs"></a>Ermitteln installierter Sprachpakete  
Um die Sprachpakete zu ermitteln, die auf einem Computer installiert sind, auf dem der Configuration Manager-Client ausgeführt wird, suchen Sie nach der Gebietsschema-ID (LCID) der installierten Sprachpakete in der Registrierung des Computers. Diese Informationen sind unter folgendem Registrierungspfad verfügbar:  

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCMSetup\InstalledLangs`  

Anpassen der Hardwareinventur zum Sammeln dieser Informationen. Erstellen Sie dann einen benutzerdefinierten Bericht, um die Sprachdetails anzuzeigen. Weitere Informationen zur Hardwareinventur finden Sie unter [How to configure hardware inventory (Konfigurieren der Hardwareinventur)](../../../clients/manage/inventory/configure-hardware-inventory.md). Weitere Informationen finden Sie unter [Erstellen von Berichten](../../manage/operations-and-maintenance-for-reporting.md#create-reports).
