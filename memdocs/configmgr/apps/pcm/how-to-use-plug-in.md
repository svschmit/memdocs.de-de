---
title: Verwenden des Konvertierungs-Plug-Ins
titleSuffix: Configuration Manager
description: Mit dem Plug-In „Paketkonvertierungs-Manager“ können Sie die Analyse- und Konvertierungsprozesse anpassen.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 83cf156c-36de-483f-a9e6-2e06158f3b20
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 4ca16ade5f8581cb124df39294c3cfc27627a346
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688958"
---
# <a name="how-to-use-the-package-conversion-manager-plug-in"></a>Verwenden des Plug-Ins „Paketkonvertierungs-Manager“

*Gilt für: Configuration Manager (Current Branch)*

<!--1357861-->

Mit dem Plug-In „Paketkonvertierungs-Manager“ können Sie den Analyse- und Konvertierungsprozess anpassen. Um das Plug-In „Paketkonvertierungs-Manager“ zu verwenden, schreiben Sie eine ausführbare Datei oder Skriptdatei, die benutzerdefinierte Vorgänge ausführt. Bearbeiten Sie dann die Konfigurationsdatei „Microsoft.ConfigurationManagement.exe.config“, um die ausführbare Datei bzw. Skriptdatei aufzurufen. Die am häufigsten verwendeten Skriptsprachen sind VBScript und PowerShell.

Das Plug-In „Paketkonvertierungs-Manager“ wird für jedes Paket einmal ausgeführt. Wenn Sie mehrere Pakete gleichzeitig analysieren oder konvertieren, wird das Plug-In „Paketkonvertierungs-Manager“ jedes Mal ausgeführt.

> [!NOTE]  
> Weitere Informationen zu den Elementen des Paketkonvertierungs-Managers in der Configuration Manager-Konfigurationsdatei finden Sie unter [Technische Referenz für das Plug-In „Paketkonvertierungs-Manager“ in der XML-Konfigurationsdatei](plugin-config-xml.md).



## <a name="default-process"></a>Standardprozess

Der Paketkonvertierungs-Manager führt standardmäßig die folgenden Aktionen aus:

1.  Lesen eines Configuration Manager-Pakets  

2.  Erstellen einer Anwendung aus dem Paket und Hinzufügen von Standardattributen  

3.  Analysieren der Anwendung und Bestimmen des Bereitschaftsstatus des Pakets  

4.  Führen Sie je nach Vorgang des Paketkonvertierungs-Managers eine der folgenden Aktionen aus:  

    - **Analysieren:** Zeigt den Bereitschaftsstatus des Pakets in der Configuration Manager-Konsole an.  

    - **Konvertieren:** Schreibt die Anwendung in die Configuration Manager-Datenbank.  


## <a name="plug-in-based-process"></a>Plug-in-basierter Prozess 

Der Paketkonvertierungs-Manager führt standardmäßig die folgenden Aktionen aus:

1.  Lesen eines Configuration Manager-Pakets.  

2.  Erstellen einer Anwendung aus dem Paket und Hinzufügen von Standardattributen.  

3.  Konvertieren der Anwendung in XML. Speichern der Datei auf dem Datenträger.  

4.  Ausführen des Plug-In-Skripts zum Ändern der XML-Elemente der Anwendung. Weitere Informationen finden Sie unter [Technische Referenz für die XML-Elemente in der Konfigurationsdatei des Plug-Ins „Paketkonvertierungs-Manager“](plugin-config-xml.md).  

5.  Konvertieren der XML-Elemente der Anwendung in eine Configuration Manager-Anwendung.  

6.  Analysieren der Anwendung und Bestimmen des Bereitschaftsstatus des Pakets.  

7.  Führen Sie je nach Vorgang des Paketkonvertierungs-Managers eine der folgenden Aktionen aus:  

    - **Analysieren:** Zeigt den Bereitschaftsstatus des Pakets in der Configuration Manager-Konsole an.  

    - **Konvertieren:** Schreibt die Anwendung in die Configuration Manager-Datenbank.  



## <a name="see-also"></a>Weitere Informationen:

[Technische Referenz für die XML-Elemente in der Konfigurationsdatei des Plug-Ins „Paketkonvertierungs-Manager“](plugin-config-xml.md)
