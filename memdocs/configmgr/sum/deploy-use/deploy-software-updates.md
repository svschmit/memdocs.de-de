---
title: Bereitstellen von Softwareupdates
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Softwareupdates in der Configuration Manager-Konsole manuell oder automatisch bereitstellen.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 11/27/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 04536d51-3bf7-45e5-b4af-36ceed10583d
ms.openlocfilehash: 8104bbab04e2c8741bfbbc9c6fb61039033941c9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696138"
---
# <a name="deploy-software-updates"></a>Bereitstellen von Softwareupdates  

*Gilt für: Configuration Manager (Current Branch)*

In der Softwareupdate-Bereitstellungsphase werden Softwareupdates bereitgestellt. Der Standort führt unabhängig von der Bereitstellungsmethode für Softwareupdates die folgenden Vorgänge aus:
- Die Updates werden einer Softwareupdategruppe hinzugefügt.
- Die Updateinhalte werden an die Verteilungspunkte verteilt.
- Die Updategruppe wird für Clients bereitgestellt.  

Nach dem Erstellen der Bereitstellung sendet der Standort eine zugehörige Softwareupdaterichtlinie an die Zielclients. Die Clients laden die Inhaltsdateien des Softwareupdates aus einer Inhaltsquelle herunter und speichern diese in ihrem lokalen Cache. Clients im Internet laden Inhalte stets über den Microsoft Update-Clouddienst herunter. Die Softwareupdates sind anschließend für die Installation durch den Client verfügbar.   

> [!Tip]  
>  Wenn ein Verteilungspunkt nicht verfügbar ist, können Clients im Intranet auch Softwareupdates über Microsoft Update herunterladen.  

> [!NOTE]  
>  Im Gegensatz zu anderen Bereitstellungstypen werden alle Softwareupdates in den Clientcache heruntergeladen. Dies ist unabhängig von der maximalen Cachegröße auf dem Client. Weitere Informationen zu den Einstellungen des Clientcaches finden Sie unter [Konfigurieren des Clientcaches für Konfigurations-Manager-Clients](../../core/clients/manage/manage-clients.md#BKMK_ClientCache).  

Wenn Sie eine erforderliche Softwareupdatebereitstellung konfigurieren, werden die Softwareupdates automatisch am geplanten Stichtag installiert. Alternativ kann der Benutzer die Softwareupdateinstallation auf dem Clientcomputer auch vor dem Stichtag einplanen oder initiieren. Nach dem Installationsversuch werden von den Clientcomputern Zustandsmeldungen zurück an den Standortserver gesendet, aus denen hervorgeht, ob die Softwareupdateinstallation erfolgreich war. Weitere Informationen zu Softwareupdatebereitstellungen  finden Sie unter [Software update deployment workflows](../understand/software-updates-introduction.md#BKMK_DeploymentWorkflows).  

Es gibt drei Hauptszenarios für das Bereitstellen von Softwareupdates: 
- [Manuelle Bereitstellung](#BKMK_ManualDeployment)  
- [Automatische Bereitstellung](#bkmk_auto)  
- [Stufenweise Bereitstellung](#bkmk_phased)  

In der Regel beginnen Sie damit, Softwareupdates manuell bereitzustellen, um eine Baseline für die Clients zu erstellen. Die Verwaltung der Softwareupdates auf Clients erfolgt dann durch die automatische oder stufenweise Bereitstellung.  

> [!Note]  
> Sie können keine automatische Bereitstellungsregel bei der stufenweisen Bereitstellung verwenden.



## <a name="manually-deploy-software-updates"></a><a name="BKMK_ManualDeployment"></a> Manuelles Bereitstellen von Softwareupdates
Sie können Softwareupdates in der Configuration Manager-Konsole auswählen und den Bereitstellungsprozess manuell starten. Diese Bereitstellungsmethode verwenden Sie in der Regel,  

- um Clients durch erforderliche Softwareupdates zu aktualisieren, bevor Sie Regeln für automatische monatliche Bereitstellungen erstellen,  

- und um Out-of-band-Softwareupdates bereitzustellen.  


Der allgemeine Workflow für die manuelle Bereitstellung von Softwareupdates umfasst die folgenden Schritte:  

1. Filtern Sie Softwareupdates mit bestimmten Anforderungen heraus. Beispielsweise können Sie mithilfe geeigneter Kriterien angeben, dass alle sicherheitsrelevanten oder kritischen Softwareupdates abgerufen werden sollen, die auf mehr als 50 Clients benötigt werden.  

2. Erstellen Sie eine Softwareupdategruppe, die die Softwareupdates enthält.  

3. Laden Sie den Inhalt für die Softwareupdates in der Softwareupdategruppe herunter.  

4. Stellen Sie die Softwareupdategruppe manuell bereit.  

Weitere Informationen und ausführliche Anleitungen finden Sie unter [Manuelles Bereitstellen von Softwareupdates](manually-deploy-software-updates.md).

> [!Tip]  
> Wenn Sie Office 365-Clientupdates manuell bereitstellen möchten, können Sie diese im Arbeitsbereich **Softwarebibliothek** unter **Office 365-Clientverwaltung** unter dem Knoten **Office 365-Updates** abrufen.  



## <a name="automatically-deploy-software-updates"></a><a name="bkmk_auto"></a> Automatisches Bereitstellen von Softwareupdates

Die automatische Bereitstellung von Softwareupdates wird mithilfe der zugehörigen automatischen Bereitstellungsregel (ADR) konfiguriert. Diese Bereitstellungsmethode wird häufig für monatliche Softwareupdates (auch als „Patch-Dienstag“ bekannt) und für die Verwaltung von Definitionsupdates verwendet. Zur Automatisierung des Bereitstellungsprozesses legen Sie ADR-Kriterien fest. Die folgende Liste bietet den allgemeinen Workflow, um Softwareupdates automatisch bereitzustellen:  

1.  Erstellen Sie eine automatische Bereitstellungsregel, die Bereitstellungseinstellungen angibt.  

2.  Der Standort fügt einer Softwareupdategruppe die Softwareupdates hinzu.  

3.  Der Standort stellt die Softwareupdategruppe für Clients in der Zielsammlung bereit.  

Zunächst müssen Sie eine Bereitstellungsstrategie für automatische Softwareupdates festlegen. Sie können beispielsweise eine ADR erstellen, die zunächst auf eine Sammlung von Testclients angewendet wird. Nachdem Sie überprüft haben, ob die Testgruppe die Softwareupdates erfolgreich installiert hat, können Sie der Regel eine neue Bereitstellung hinzufügen. Sie können innerhalb der vorhandenen Bereitstellung auch eine andere Zielsammlung festlegen, die mehr Clients enthält. Bei der Wahl der Strategie sollten Sie folgende Verhalten berücksichtigen:  

- Sie können die Eigenschaften der Softwareupdateobjekte ändern, die von der ADR erstellt werden.   

- Die ADR stellt automatisch Softwareupdates für Clients bereit, wenn Sie diese der Zielsammlung hinzufügen.  

- Wenn Sie oder die ADR der Softwareupdategruppe neue Softwareupdates hinzufügen, stellt der Standort diese automatisch für Clients in der Zielsammlung bereit.  

- Sie können Bereitstellungen für die ADR jederzeit aktivieren oder deaktivieren.  


Nach der Erstellung einer ADR können Sie der Regel zusätzliche Bereitstellungen hinzufügen. Dies hilft Ihnen dabei, die Komplexität der Bereitstellung verschiedener Updates für verschiedene Sammlungen zu verwalten. Jede neue Bereitstellung verfügt über sämtliche Funktionen und die Bereitstellungsüberwachungsumgebung.  

Für jede neue Bereitstellung, die Sie hinzufügen:  

- werden dieselben Updategruppen und -pakete verwendet, die bei der ersten Ausführung der ADR erstellt wurden.  
- kann eine andere Zielsammlung verwendet werden.  
- Werden eindeutige Bereitstellungseigenschaften unterstützt, einschließlich:  
  -   Aktivierungszeitpunkt  
  -   Stichtag  
  -   Benutzerfreundlichkeit  
  -   unterschiedliche Warnungen für die jeweiligen Bereitstellungen  


Weitere Informationen und ausführliche Anleitungen finden Sie unter [Automatisches Bereitstellen von Softwareupdates](automatically-deploy-software-updates.md).



## <a name="deploy-software-updates-in-phases"></a><a name="bkmk_phased"></a> Stufenweises Bereitstellen von Softwareupdates

<!--1358146-->
Erstellen Sie ab Version 1810 stufenweise Bereitstellungen für Softwareupdates. Mithilfe von Bereitstellungen in Phasen können Sie einen koordinierten, sequenzierten Softwarerollout basierend auf anpassbaren Kriterien und Gruppen orchestrieren.

Weitere Informationen finden Sie unter [Erstellen von stufenweisen Bereitstellungen mit Configuration Manager](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json).

