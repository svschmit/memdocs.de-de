---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: 98e3dd75316acfeaf88715b8f80762b1d6c587c6
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128330"
---
<!--This file is shared by the cmpivot.md file and the cmpivot-changes.md file and contains information on how to run CMPivot standalone. H2s or HJ3s are determined by the article for which the include file is used.-->
<!--3555890, 4619340, 4683130 -->

Ab Version 1906 können Sie CMPivot als eigenständige App verwenden. Die eigenständige CMPivot-Version steht nur in englischer Sprache zur Verfügung. Führen Sie CMPivot außerhalb der Configuration Manager-Konsole aus, um den Echtzeitstatus von Geräten in Ihrer Umgebung anzuzeigen. Diese Änderung ermöglicht Ihnen die Verwendung von CMPivot auf einem Gerät, ohne die Konsole vorher zu installieren.

> [!Tip]  
> Dieses Feature wurde erstmals in Version 1906 als [Vorabfeature](../pre-release-features.md) eingeführt. Ab Version 2002 ist es kein Vorabfeature mehr.  

Sie können die Leistungsfähigkeit von CMPivot mit anderen Personas wie Helpdesk oder Sicherheitsadministratoren teilen, die die Konsole nicht auf ihrem Computer installiert haben. Diese anderen Personas können CMPivot verwenden, um Configuration Manager neben den anderen Tools, die sie traditionell verwenden, abzufragen. Durch die gemeinsame Nutzung dieser umfangreichen Verwaltungsdaten können Sie proaktiv an der Lösung von rollenübergreifenden Geschäftsproblemen arbeiten.

#### <a name="install-cmpivot-standalone"></a>Installieren der eigenständigen CMPivot-Version

1. Richten Sie die erforderlichen Berechtigungen für die Ausführung von CMPivot ein. Weitere Informationen finden Sie unter [Voraussetzungen](../cmpivot.md#prerequisites). Sie können auch die Rolle [Sicherheitsadministrator](../cmpivot-changes.md#bkmk_cmpivot_secadmin1906) verwenden, wenn die Berechtigungen für den Benutzer angemessen sind.
2. Das Installationsprogramm für die CMPivot-App befindet sich unter folgendem Pfad: `<site install path>\tools\CMPivot\CMPivot.msi`. Sie können es von diesem Pfad aus ausführen oder an einen anderen Speicherort kopieren.
3. Beim Ausführen der eigenständigen CMPivot-App werden Sie aufgefordert, eine Verbindung mit einem Standort herzustellen. Geben Sie den vollqualifizierten Domänennamen oder den Computernamen des Servers des Standorts der zentralen Verwaltung oder des primären Standorts an.
   - Wenn Sie die eigenständige CMPivot-Version öffnen, werden Sie jedes Mal aufgefordert, eine Verbindung mit einem Standortserver herzustellen.
4. Durchsuchen Sie die Sammlung, für die Sie CMPivot ausführen möchten, und führen Sie Ihre Abfrage aus.

   ![Navigieren zur Sammlung, für die die Abfrage ausgeführt werden soll](../media/3555890-cmpivot-standalone-browse-collection.png)

> [!NOTE]
> - Kontextmenü-Aktionen wie **Run Scripts** (Skripts ausführen) und **Ressourcen-Explorer** sowie die Websuche sind in der eigenständigen CMPivot-Version nicht verfügbar. Die primäre Verwendung der eigenständigen CMPivot-Version besteht darin, unabhängig von der Configuration Manager-Infrastruktur Abfragen durchzuführen. Eigenständiges CMPivot bietet zur Unterstützung von Sicherheitsadministratoren die Möglichkeit, eine Verbindung mit Microsoft Defender Security Center herzustellen. <!--5605358-->
> - Ab Version 1910 ist die [Abfrageauswertung für lokales Gerät mit der eigenständigen CMPivot-Version](../cmpivot-changes.md#bkmk_local-eval) möglich. <!--3197353--> 