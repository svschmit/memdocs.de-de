---
title: Ermitteln von Geräte- und Benutzerressourcen
titleSuffix: Configuration Manager
description: Lesen Sie eine Übersicht über den Ermittlungsprozess und die Ermittlung von Datensätzen.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 30844519-ce14-456f-bfb8-4318b578e9f6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1869c9e6de455b7086a051db91bb26bc00a91a5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700988"
---
# <a name="run-discovery-for-configuration-manager"></a>Ausführen der Ermittlung für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Zum Bestimmen von Geräte- und Benutzerressourcen, die Sie verwalten können, verwenden Sie eine oder mehrere Ermittlungsmethoden in Configuration Manager. Sie können mithilfe der Ermittlung auch die Netzwerkinfrastruktur in Ihrer Umgebung bestimmen. Es gibt verschiedene Methoden, mit denen Sie unterschiedliche Dinge ermitteln können, wobei jede Methode ihre eigenen Konfigurationen und Einschränkungen hat.  

## <a name="overview-of-discovery"></a>Übersicht über die Ermittlung  
 Die Ermittlung ist der Prozess, über den Configuration Manager erfährt, welche Ressourcen Sie verwalten können. Es folgen die verfügbaren Ermittlungsmethoden:  

-   Active Directory-Gesamtstrukturermittlung  

-   Active Directory-Gruppenermittlung  

-   Active Directory-Systemermittlung  

-   Active Directory-Benutzerermittlung  

-   Frequenzermittlung  

-   Netzwerkermittlung  

-   Serverermittlung  

> [!TIP]  
>  Informationen zu den einzelnen Ermittlungsmethoden finden Sie unter [Informationen zu Ermittlungsmethoden in Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md).  
>   
>  Entscheidungshilfen hinsichtlich der Methoden und den Standorten in Ihrer Hierarchie finden Sie unter [Auswählen von Ermittlungsmethoden zur Verwendung in Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md).  

 Für die meisten Ermittlungsmethoden müssen Sie die jeweilige Methode am Standort aktivieren und so einrichten, dass bestimmte Netzwerk- oder Active Directory-Standorte durchsucht werden. Während der Ausführung wird der angegebene Speicherort auf Informationen zu Geräten oder Benutzern abgefragt, die Configuration Manager verwalten kann. Wenn eine Ermittlungsmethode Informationen zu einer Ressource findet, werden diese in einer Datei abgelegt, die als DDR (Discovery Data Record) bezeichnet wird. Diese Datei wird anschließend von einem primären Standort oder einem Standort der zentralen Verwaltung verarbeitet. Bei der Verarbeitung eines DDR wird ein neuer Datensatz in der Standortdatenbank für neu ermittelte Ressourcen erstellt, oder vorhandene Datensätze werden mit neuen Informationen aktualisiert.  

 Bei einigen Ermittlungsmethoden kann hoher Netzwerkdatenverkehr entstehen, und bei der Verarbeitung der von ihnen erstellten DDRs werden gegebenenfalls erhebliche CPU-Ressourcen in Anspruch genommen. Sie sollten sich daher auf die Ermittlungsmethoden beschränken, die zum Erreichen Ihrer Ziele erforderlich sind. Möglicherweise genügen ein oder zwei Ermittlungsmethoden für Ihre Zwecke. Später können Sie weitere Methoden Schritt für Schritt hinzufügen, um die Ermittlung in Ihrer Umgebung auszuweiten.  

 Die der Standortdatenbank hinzugefügten Ermittlungsinformationen werden anschließend an jeden Standort in der Hierarchie repliziert, unabhängig davon, wo sie ermittelt oder verarbeitet wurden. Während Sie an verschiedenen Standorten unterschiedliche Zeitpläne und Einstellungen für Ermittlungsmethoden einrichten können, führen Sie eine bestimmte Ermittlungsmethode möglicherweise nur an einem einzigen Standort aus. Dies verringert die Nutzung der Netzwerkbandbreite durch doppelte Ermittlungsaktionen und reduziert die Verarbeitung redundanter Ermittlungsdaten an mehreren Standorten.  

 Anhand von Ermittlungsdaten können Sie benutzerdefinierte Sammlungen und Abfragen erstellen, mit denen Ressourcen für Verwaltungsaufgaben logisch gruppiert werden. Beispiel:  

-   Pushübertragung von Clientinstallationen oder Upgrades.  

-   Bereitstellen von Inhalten für Benutzer oder Geräte.  

-   Bereitstellen von Clienteinstellungen und zugehörigen Konfigurationen.

##  <a name="about-discovery-data-records"></a><a name="BKMK_DDRs"></a> Informationen zu Discovery Data Records  
 DDRs sind Dateien, die durch eine Ermittlungsmethode erstellt werden. Sie enthalten Informationen zu einer Ressource, die Sie im Konfigurations-Manager verwalten können, wie z.B. Computer, Benutzer und in einigen Fällen die Netzwerkinfrastruktur. Sie werden auf primären Standorten oder auf Standorten der zentralen Verwaltung verarbeitet. Nachdem die im DDR enthaltenen Ressourceninformationen in die Datenbank eingetragen wurden, wird der DDR gelöscht, und die Informationen werden als globale Daten an alle Standorte in der Hierarchie repliziert.  

 Auf welchem Standort ein DDR verarbeitet wird, ist abhängig von den enthaltenen Informationen:  

-   DDRs für neu ermittelte und noch nicht in der Datenbank enthaltene Ressourcen werden auf dem Standort auf der obersten Ebene der Hierarchie verarbeitet. Vom Standort auf der obersten Ebene der Hierarchie wird ein neuer Ressourcendatensatz in der Datenbank erstellt und diesem eine eindeutige ID zugeordnet. DDRs werden mithilfe von dateibasierter Replikation bis auf den Standort auf der obersten Ebene übertragen.  

-   DDRs für bereits ermittelte Objekte werden auf primären Standorten verarbeitet. Von untergeordneten Standorten werden DDRs nicht an den Standort der zentralen Verwaltung übertragen, wenn der DDR Informationen über eine Ressource enthält, die sich bereits in der Datenbank befindet.  

-   DDRs werden von sekundären Standorten nicht verarbeitet, sondern von diesen immer mithilfe von dateibasierter Replikation an den übergeordneten primären Standort übertragen.  

DDR-Dateien verfügen über die Erweiterung DDR und über eine Größe von in der Regel ca. 1 KB.  

## <a name="get-started-with-discovery"></a>Erste Schritte mit der Ermittlung:  
 Vor Verwendung der Configuration Manager-Konsole zum Einrichten der Ermittlung sollten sich mit den Unterschieden zwischen den Methoden, ihren Möglichkeiten und (bei einigen) ihren Einschränkungen vertraut machen.  

Die folgenden Themen bieten grundlegende Informationen zur erfolgreichen Nutzung von Ermittlungsmethoden:  

-   [Ermittlungsmethoden für Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md)  

-   [Auswählen von Ermittlungsmethoden zur Verwendung in Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md)  

Wenn Sie die Methoden kennen, die Sie verwenden möchten, finden Sie einen Leitfaden zum Einrichten der einzelnen Methoden unter [Konfigurieren von Ermittlungsmethoden für Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  
