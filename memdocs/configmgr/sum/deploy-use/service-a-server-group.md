---
title: Bereitstellung einer Servergruppe
titleSuffix: Configuration Manager
description: Die Configuration Manager-Konsole stellt Warnungen und Status zum Überwachen von Updates und Konformität bereit.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/01/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 304a83ea-0f72-437d-9688-2e6e0c7526dd
ms.openlocfilehash: 7d6d8bef145e14547e5e6a726a93cb9470b94afd
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709188"
---
# <a name="service-a-server-group"></a>Bereitstellung einer Servergruppe

*Gilt für: Configuration Manager (Current Branch)*

>[!IMPORTANT]
> - Ab Configuration Manager, Version 2002, wurden Servergruppen durch Orchestrierungsgruppen ersetzt. Weitere Informationen finden Sie unter [Orchestrierungsgruppen](orchestration-groups.md).
> - Features der Vorabversion sind Features, die in Current Branch enthalten sind, um sie in einem frühen Stadium in einer Produktionsumgebung zu testen. Diese Features werden vollständig unterstützt, unterliegen aber noch der Entwicklung und könnten möglicherweise geändert werden, bis sie die Vorabversionskategorie verlassen. Aktivieren Sie dieses Feature, um es verfügbar zu machen. Weitere Informationen finden Sie unter [Use pre-release features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease) (Verwenden von Vorabfeatures aus Updates).

In Configuration Manager können Sie ab Version 1606 Servergruppeneinstellungen für eine Sammlung konfigurieren und so festlegen, auf wie vielen Computern, auf wie viel Prozent der Computer oder in welcher Reihenfolge auf Computern in der Sammlung Softwareupdates installiert werden. Zudem können Sie auch PowerShell-Skripts zum Ausführen von benutzerdefinierten Aktionen vor und nach der Bereitstellung konfigurieren.

Wenn Sie für eine Sammlung, für die Servergruppeneinstellungen konfiguriert wurden, Softwareupdates bereitstellen, wird von Configuration Manager ermittelt, auf wie vielen Computern in der Sammlung die Softwareupdates zu einem bestimmten Zeitpunkt installiert werden können. Zudem wird diese Anzahl von Bereitstellungssperren zur Verfügung gestellt. Nur auf Computern mit Bereitstellungssperre wird die Installation von Softwareupdates gestartet. Wenn eine Bereitstellungssperre verfügbar ist, wird diese einem Computer zugewiesen. Auf diesem werden die Softwareupdates installiert. Nach der erfolgreichen Installation der Softwareupdates wird die Bereitstellungssperre wieder freigegeben. Danach ist die Bereitstellungssperre für andere Computer verfügbar. Wenn auf einem Computer die Bereitstellungssperre nicht freigegeben werden kann, können Sie alle Bereitstellungssperren der Servergruppe in der Sammlung manuell freigeben.

>[!IMPORTANT]
>Hierzu müssen alle Computer in der Sammlung demselben Standort zugewiesen sein.

#### <a name="to-create-a-collection-for-a-server-group"></a>So erstellen Sie eine Sammlung für eine Servergruppe  
Die Servergruppeneinstellungen werden in den Eigenschaften für eine Gerätesammlung konfiguriert. Damit eine Servergruppe verwaltet werden kann, müssen alle Mitglieder in einer Sammlung demselben Standort zugewiesen sein. Gehen Sie folgendermaßen vor, um eine Sammlung zu erstellen und die Servergruppeneinstellungen zu konfigurieren:
1.  [Erstellen Sie eine Gerätesammlung](../../core/clients/manage/collections/create-collections.md), die die Computer in der Servergruppe enthält.  

2.  Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Gerätesammlungen**, klicken Sie mit der rechten Maustaste auf die Sammlung mit den Computern in der Servergruppe, und klicken Sie anschließend auf **Eigenschaften**.  

3.  Wählen Sie auf der Registerkarte **Allgemein** die Option **Alle Geräte gehören derselben Servergruppe an** aus, und klicken Sie auf **Einstellungen**.  

4.  Legen Sie auf der Seite **Servergruppeneinstellungen** eine der folgenden Einstellungen fest:  

    -   **Allow a percentage of machines to be updated at the same time** (Zulassen, dass ein bestimmter Prozentsatz der Computer gleichzeitig aktualisiert wird): Gibt an, dass nur ein bestimmter Prozentsatz von Clients gleichzeitig aktualisiert wird. Wenn eine Sammlung beispielsweise 10 Clients enthält und für die Sammlung festgelegt wurde, dass 30 % der Clients gleichzeitig aktualisiert werden, werden Softwareupdates immer nur auf 3 Clients gleichzeitig installiert.  

    -   **Allow a number of machines to be updated at the same time** (Zulassen, dass eine bestimmte Anzahl von Computern gleichzeitig aktualisiert wird): Gibt an, dass nur eine bestimmte Anzahl von Clients gleichzeitig aktualisiert wird.  

    -   **Geben Sie die Wartungssequenz an:** Gibt an, dass die Clients in der Sammlung in der von Ihnen festgelegten Reihenfolge nacheinander aktualisiert werden. Auf einem Client werden Softwareupdates erst installiert, nachdem die Installation von Softwareupdates auf dem Client abgeschlossen ist, der sich in der Liste vor diesem Client befindet.  

5.  Geben Sie an, ob ein Skript vor der Bereitstellung (Knoten sperren) oder ein Skript nach der Bereitstellung (Knoten fortsetzen) verwendet werden soll.  

    > [!WARNING]
    > Benutzerdefinierte Skripts werden nicht von Microsoft signiert. Es ist Ihre Aufgabe, die Integrität dieser Skripts zu verwalten.

    > [!TIP]  
    > Die folgenden Beispiele können Sie beim Testen für Skripts vor und nach der Bereitstellung verwenden, die die aktuelle Uhrzeit in eine Textdatei schreiben:  
    >   
    >  **Vor der Bereitstellung**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\Windows\Temp\start.txt`  
    >   
    >  **Nach der Bereitstellung**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\Windows\Temp\end.txt`  

## <a name="deploy-software-updates-to-the-server-group-and-monitor-status"></a>Bereitstellen von Softwareupdates für die Servergruppe und Überwachen des Status  
Softwareupdates werden für die Servergruppensammlung mit dem üblichen Bereitstellungsprozess bereitgestellt. Nach der Bereitstellung der Softwareupdates können Sie die Softwareupdatebereitstellung in der Configuration Manager-Konsole überwachen.
1.  [Stellen Sie Softwareupdates](manually-deploy-software-updates.md) für die Servergruppensammlung bereit.   

2.  [Überwachen der Softwareupdatebereitstellung](monitor-software-updates.md). Hierbei wird neben den üblichen Überwachungsansichten für die Bereitstellung von Softwareupdates auch der Status **Auf Sperre wird gewartet** angezeigt, wenn ein Client auf die Installation der Softwareupdates wartet. In der Protokolldatei „UpdatesDeployment.log“ finden Sie weitere Informationen.


## <a name="clear-the-deployment-locks-for-computers-in-a-server-group"></a>Löschen der Bereitstellungssperren für Computer in einer Servergruppe  
Wenn auf einem Computer die Bereitstellungssperre nicht freigegeben werden kann, können Sie alle Bereitstellungssperren der Servergruppe in der Sammlung manuell freigeben. Löschen Sie Sperren nur, wenn bei einer Bereitstellung das Update von Computern in der Sammlung hängen bleibt und noch nicht kompatible Computer vorhanden sind.  
1.  Klicken Sie zum Löschen von Bereitstellungssperren im Arbeitsbereich **Bestand und Kompatibilität** auf **Gerätesammlungen** und anschließend auf die entsprechende Sammlung.  

2.  Klicken Sie auf der Registerkarte **Start** in der Gruppe **Bereitstellung** auf **Bereitstellungssperren für Servergruppe löschen**. Wenn die Softwareupdates auf einem Client nicht installiert werden konnten und dadurch die Installation der Softwareupdates auf anderen Clients verhindert wird, können die Bereitstellungssperren manuell gelöscht werden.  
