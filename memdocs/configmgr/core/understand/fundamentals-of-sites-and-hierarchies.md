---
title: Grundlagen von Standorten und Hierarchien
titleSuffix: Configuration Manager
description: Erhalten Sie grundlegende Informationen zu Configuration Manager-Standorten und Hierarchien.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4db1e15f-e832-4cf9-be33-d3971e635a55
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 04ed22436d750572fed8ce898c5ed3a23b71f239
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707028"
---
# <a name="fundamentals-of-sites-and-hierarchies-for-configuration-manager"></a>Grundlagen von Standorten und Hierarchien für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Eine Bereitstellung von Configuration Manager muss in einer Active Directory-Domäne installiert werden. Die Basis dieser Bereitstellung umfasst einen oder mehrere Configuration Manager-Standorte, die zusammen eine Standorthierarchie bilden. Egal ob einzelner Standort oder Hierarchie mit mehreren Standorten – der Typ und der Speicherort der Standorte, die Sie installieren, bieten Ihnen die Möglichkeit, Ihre Bereitstellung bei Bedarf hochzuskalieren, und liefern wichtige Dienste für verwaltete Benutzer und Geräte.

## <a name="hierarchies-of-sites"></a>Hierarchien von Standorten
Wenn Sie Configuration Manager zum ersten Mal installieren, bestimmt der erste Configuration Manager-Standort den Umfang Ihrer Hierarchie. Dieser erste Configuration Manager-Standort bildet die Grundlage für die Verwaltung von Geräten und Benutzern in Ihrem Unternehmen. Hierbei muss es sich entweder um einen Standort der zentralen Verwaltung oder um einen eigenständigen primären Standort handeln.  

 Ein *Standort der zentralen Verwaltung* eignet sich für umfangreiche Bereitstellungen. Er stellt eine Verwaltungszentrale bereit und unterstützt flexibel Geräte, die in einer globalen Netzwerkinfrastruktur verteilt sind. Nach der Installation eines Standorts der zentralen Verwaltung müssen Sie mindestens einen primären Standort als untergeordneten Standort installieren. Diese Konfiguration ist erforderlich, da ein Standort der zentralen Verwaltung die Geräteverwaltung nicht direkt unterstützt. Dies ist die Aufgabe eines primären Standorts. Ein Standort der zentralen Verwaltung unterstützt mehrere untergeordnete primäre Standorte. Die untergeordneten primären Standorte werden zur direkten Verwaltung von Geräten sowie zur Steuerung der Netzwerkbandbreite verwendet, falls sich Ihre verwalteten Geräte an unterschiedlichen geografischen Standorten befinden.  

 Ein *eigenständiger primärer Standort* eignet sich für kleinere Bereitstellungen und kann zum Verwalten von Geräten verwendet werden, ohne dass zusätzliche Standorte installiert werden müssen. Zwar kann ein eigenständiger primärer Standort die Größe Ihrer Bereitstellung begrenzen, er unterstützt jedoch ein Szenario zum Erweitern Ihrer Hierarchie zu einem späteren Zeitpunkt, indem ein neuer Standort der zentralen Verwaltung installiert wird. Bei diesem Standorterweiterungsszenario wird Ihr eigenständiger primärer Standort zu einem untergeordneten primären Standort. Anschließend können Sie zusätzliche untergeordnete primäre Standorte unter Ihrem neuen Standort der zentralen Verwaltung installieren. Sie können dann Ihre anfängliche Bereitstellung bei künftigem Wachstum Ihres Unternehmens erweitern.  

> [!TIP]  
>  Ein eigenständiger primärer Standort und ein untergeordneter primärer Standort sind eigentlich der gleiche Standorttyp: ein primärer Standort. Der unterschiedliche Name basiert auf der Hierarchiebeziehung, die dann erstellt wird, wenn Sie auch einen Standort der zentralen Verwaltung verwenden. Durch diese Hierarchiebeziehung kann auch die Installation bestimmter Standortsystemrollen eingeschränkt sein, mit denen die Funktionalität von Configuration Manager erweitert wird. Diese Rolleneinschränkung ist dadurch begründet, dass bestimmte Standortsystemrollen nur am Standort der obersten Ebene der Hierarchie, an einem Standort der zentralen Verwaltung oder an einem eigenständigen primären Standort installiert werden können.  

 Nach der Installation Ihres ersten Standorts können Sie weitere Standorte installieren. Wenn Ihr erster Standort ein Standort der zentralen Verwaltung war, können Sie einen oder mehrere untergeordnete primäre Standorten installieren. Nach der Installation eines primären Standorts (eigenständig oder untergeordnet primär) können Sie einen oder mehrere sekundäre Standorte installieren.  

 Ein *sekundärer Standort* kann nur als untergeordneter Standort unter einem primären Standort installiert werden. Mit diesem Standorttyp können Sie die Reichweite eines primären Standorts zur Verwaltung von Geräten an Orten erweitern, die eine langsame Netzwerkverbindung mit dem primären Standort haben. Obwohl ein sekundärer Standort den primären Standort erweitert, werden alle Clients weiterhin vom primären Standort verwaltet. Der sekundäre Standort bietet Unterstützung für Geräte am Remotestandort. Er bietet Unterstützung, indem er Daten, die Sie an Clients senden (bereitstellen), und die Clients zurück an den Standort senden, komprimiert und ihre Übertragung über Ihr Netzwerk verwaltet.  

 Die folgenden Diagramme enthalten einige Beispiele für Standortentwürfe.  

 ![Beispiele für die Hierarchie](media/Hierarchy_examples.png)  

 Weitere Informationen finden Sie unter den folgenden Themen:  

-   [Einführung in Configuration Manager](../../core/understand/introduction.md)  

-   [Entwerfen einer Hierarchie von Standorten für Configuration Manager](../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)  

-   [Installieren von Configuration Manager-Standorten](../servers/deploy/install/installing-sites.md)  

## <a name="site-system-servers-and-site-system-roles"></a>Standortsystemserver und Standortsystemrollen  
 An jedem Configuration Manager-Standort werden *Standortsystemrollen* installiert, die Verwaltungsvorgänge unterstützen. Die folgenden Rollen werden standardmäßig installiert, wenn Sie einen Standort installieren:

-   Die Standortserverrolle wird dem Computer zugewiesen, auf dem Sie den Standort installieren.

-   Die Standortdatenbankserverrolle wird dem SQL Server zugewiesen, der die Standortdatenbank hostet.

Andere Standortsystemrollen sind optional und werden nur verwendet, wenn Sie die Funktionalität verwenden möchten, die in einer Standortsystemrolle aktiv ist. Jeder Computer, der eine Standortsystemrolle hostet, wird als Standortsystemserver bezeichnet.  

 Für eine kleinere Bereitstellung von Configuration Manager können Sie anfänglich ggf. alle Ihre Standortsystemrollen direkt auf dem Standortservercomputer ausführen. Sobald Ihre verwaltete Umgebung wächst und die Anforderungen zunehmen, können Sie zusätzliche Standortsystemserver installieren, um weitere Standortsystemrollen zu hosten. Dadurch können die Standorte weiteren Geräten Dienste effizienter bieten.  

 Informationen zu den verschiedenen Standortsystemrollen finden Sie im Abschnitt über [Standortsystemrollen](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles) des Artikels [Planen der Standortsystemserver und Standortsystemrollen für Configuration Manager](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).

## <a name="publishing-site-information-to-active-directory-domain-services"></a>Veröffentlichen von Standortinformationen in Active Directory-Domänendiensten  
 Um die Verwaltung von Configuration Manager zu vereinfachen, können Sie das Active Directory-Schema so erweitern, dass es Details unterstützt, die von Configuration Manager verwendet werden. Anschließend können Sie Standorte ihre wichtigsten Informationen in Active Directory-Domänendiensten (AD DS) veröffentlichen lassen. So können Computer, die Sie verwalten möchten, Standortinformationen aus der vertrauenswürdigen AD DS-Quelle geschützt abrufen. Die Informationen, die Clients abrufen können, bestimmen verfügbare Standorte, Standortsystemserver und die Dienste, die diese Standortsystemserver bereitstellen.  

 Die *Erweiterung des Active Directory-Schemas* erfolgt nur einmal pro Gesamtstruktur und kann vor oder nach der Installation von Configuration Manager stattfinden.   Wenn Sie das Schema erweitern, müssen Sie in jeder Domäne einen neuen Active Directory-Container namens Systemverwaltung erstellen. Der Container enthält einen Configuration Manager-Standort, der Daten veröffentlicht, die die Clients finden können. Weitere Informationen finden Sie unter [Vorbereiten von Active Directory für die Veröffentlichung eines Standorts](../../core/plan-design/network/extend-the-active-directory-schema.md).  

 Die *Veröffentlichung von Standortdaten* erhöht die Sicherheit Ihrer Configuration Manager-Hierarchie und reduziert den Verwaltungsaufwand, ist aber für eine grundlegende Configuration Manager-Funktionalität nicht erforderlich.  
