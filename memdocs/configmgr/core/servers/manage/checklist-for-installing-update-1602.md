---
title: Checkliste für Version 1602
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über Aktionen, die Sie durchführen müssen, bevor Sie eine Aktualisierung von Configuration Manager-Version 1511 auf Version 1602 vornehmen.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b63ef197-01f0-4894-b929-5ef8403c5195
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: b330c4049dce06b1e47d1088993b09ec16e724a8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700258"
---
# <a name="checklist-for-installing-update-1602-for-configuration-manager"></a>Checkliste für die Installation von Update 1602 für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Lesen Sie vor dem Aktualisieren von Configuration Manager-Version 1511 auf Version 1602 die folgenden Informationen und die Checkliste mit Aktionen, die vor Beginn des Updates durchgeführt werden müssen.  

 **Informationen über die Installation des Updates 1602:**  

 Update 1602 kann nur am Standort der obersten Ebene Ihrer Hierarchie installiert werden. Das bedeutet, dass Sie die Installation vom Standort der zentralen Verwaltung (falls vorhanden) oder vom eigenständigen primären Standort aus starten.  

-   An untergeordneten primären Standorten wird das Update automatisch installiert, sobald die Installation des Updates am Standort der zentralen Verwaltung abgeschlossen ist. Mithilfe von Wartungsfenstern können Sie steuern, wann Updates an einem Standort installiert werden. Mit der Veröffentlichung des Updates 1602 werden Wartungsfenster in *Dienstfenster* umbenannt. Weitere Informationen finden Sie unter [Dienstfenster für Standortserver](service-windows.md).  

-   Sie müssen sekundäre Standorte von der Configuration Manager-Konsole aus manuell aktualisieren, nachdem die Installation des Updates am primären übergeordneten Standort abgeschlossen wurde. Automatische Aktualisierungen sekundärer Standortserver werden nicht unterstützt.  

Bei der Installation des Updates auf dem Standortserver werden Standortsystemrollen, die auf dem Standortserver und auf Remotecomputern installiert sind, automatisch aktualisiert. Stellen Sie daher vor der Installation des Updates sicher, dass jeder Standortsystemserver die neuen Voraussetzungen für den Betrieb mit der neuen Updateversion erfüllt.  

Bei der ersten Verwendung einer Configuration Manager-Konsole nach Abschluss des Updates werden Sie aufgefordert, die Konsole zu aktualisieren. Dazu müssen Sie das Configuration Manager-Setup auf dem Computer ausführen, der die Konsole hostet, und die Option zum Aktualisieren der Konsole auswählen. Es wird empfohlen, die Installation des Updates auf der Konsole unverzüglich durchzuführen.  

 **Checkliste:**  

 **Stellen Sie sicher, dass an allen Standorten eine unterstützte Configuration Manager-Version ausgeführt wird:**  Auf jedem Standortserver in der Hierarchie muss Version 1511 von Configuration Manager ausgeführt werden, damit Sie die Installation des Updates 1602 starten können.  

 **Überprüfen Sie die installierten Microsoft .NET-Versionen auf den Standortsystemservern:** Bei der Installation von Update 1602 an einem Standort installiert Configuration Manager automatisch .NET Framework 4.5.2 auf jedem Computer, auf dem eine der folgenden Standortsystemrollen gehostet wird (sofern .NET Framework 4.5 oder höher nicht bereits installiert ist):  

-   Anmeldungsproxypunkt  

-   Anmeldungspunkt  

-   Verwaltungspunkt  

-   Dienstverbindungspunkt  

Diese Installation kann den Standortsystemserver in den Zustand „Ausstehender Neustart“ versetzen und Fehler an die Configuration Manager-Komponentenstatusanzeige melden. Darüber hinaus treten bei .NET-Anwendungen auf dem Server gelegentlich Fehler auf, bis der Server neu gestartet wird.  

 Weitere Informationen finden Sie unter [Site and site system prerequisites for System Center Configuration Manager](../../../core/plan-design/configs/site-and-site-system-prerequisites.md) (Standort- und Standortsystemanforderungen für System Center Configuration Manager).  

 **Überprüfen des Standort- und Hierarchiestandorts, um ungelöste Probleme zu beheben:** Bevor Sie das Update für einen Standort durchführen, sollten Sie alle Betriebsprobleme beheben, die den Standortserver, den Standortdatenbankserver und die auf Remotecomputern installierten Standortsystemrollen betreffen. Betriebsprobleme können die Ursache für Fehler beim Update von Standorten sein.  

Weitere Informationen finden Sie unter [Verwenden von Benachrichtigungen und des Statussystems für Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

 **Überprüfen Sie die Datei- und Datenreplikation zwischen Standorten:**  Stellen Sie sicher, dass die Datei- und Datenreplikation zwischen Standorten betriebsbereit und aktuell ist. Verzögerungen oder Rückstände können ein reibungsloses und erfolgreiches Update verhindern.    

Für die Datenbankreplikation können Sie die Replikationslinkanalyse verwenden, um Probleme vor Beginn des Updates zu lösen.    

 Weitere Informationen finden Sie unter [Informationen zur Replikationslinkanalyse](monitor-replication.md#BKMK_RLA).  

 **Installieren Sie alle anwendbaren wichtigen Updates für Betriebssysteme auf den Computern, auf denen der Standort, der Standortdatenbankserver und die Remotestandortsystemrollen gehostet werden:** Bevor Sie ein Update für Configuration Manager installieren, müssen Sie für die einzelnen anwendbaren Standortsysteme sämtliche wichtigen Updates installieren. Wenn für ein von Ihnen installiertes Update ein Neustart erforderlich ist, starten Sie die jeweiligen Computer neu, bevor Sie mit dem Upgrade beginnen.  

 **Deaktivieren von Datenbankreplikaten für Verwaltungspunkte an primären Standorten:** Configuration Manager kann kein Update eines primären Standorts durchführen, wenn dort Datenbankreplikate für Verwaltungspunkte aktiviert sind. Deaktivieren Sie die Datenbankreplikation, bevor Sie folgende Schritte ausführen:  

-   Erstellen einer Sicherung der Standortdatenbank zum Testen des Datenbankupgrades.  

-   Installieren eines Updates für Configuration Manager.  

Weitere Informationen finden Sie unter [Datenbankreplikate für Verwaltungspunkte für Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

 **Erneutes Konfigurieren von Softwareupdatepunkten, die NLBs verwenden:** Configuration Manager kann kein Update für Standorte durchführen, an denen Softwareupdatepunkte mithilfe eines NLB-Clusters gehostet werden.  Wenn Sie für Softwareupdatepunkte NLB-Cluster verwenden, entfernen Sie den NLB-Cluster mithilfe von Windows PowerShell.    

 Weitere Informationen finden Sie unter [Planen von Softwareupdates](../../../sum/plan-design/plan-for-software-updates.md).  

 **Deaktivieren Sie alle Standortwartungstasks an jedem Standort für die Dauer der Updateinstallation an diesem Standort:** Bevor Sie Updates installieren, deaktivieren Sie alle Standortwartungstasks, die möglicherweise zu dem Zeitpunkt ausgeführt werden, zu dem der Updateprozess aktiv ist. Zu diesen Aufgaben gehören u.a. folgende:  

-   Standortserver sichern  

-   Veraltete Clientvorgänge löschen  

-   Veraltete Ermittlungsdaten löschen  

Wenn ein Standortdatenbank-Wartungstask während der Updateinstallation ausgeführt wird, kann bei der Updateinstallation ein Fehler auftreten. Bevor Sie einen Task deaktivieren, zeichnen Sie den Zeitplan des Tasks auf, sodass Sie die Konfiguration nach Abschluss des Updates wiederherstellen können.  

 Weitere Informationen finden Sie unter [Wartungstasks für Configuration Manager](../../../core/servers/manage/maintenance-tasks.md) und [Referenz für Wartungstasks im Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md). 

**Beenden Sie vorübergehend jede Anitivirussoftware auf den Configuration Manager-Servern:** Bevor Sie einen Standort aktualisieren, stellen Sie sicher, dass die Antivirensoftware auf den Configuration Manager-Servern beendet wurde. <!--SMS.503481--> 

 **Erstellen einer Sicherung der Standortdatenbank am Standort der zentralen Verwaltung und an primären Standorten:** Bevor Sie ein Update für einen Standort durchführen, sollten Sie die Standortdatenbank sichern, damit Sie über eine Sicherung für die Notfallwiederherstellung verfügen.   

Weitere Informationen finden Sie unter [Sicherung und Wiederherstellung in Configuration Manager](backup-and-recovery.md).  

 **Erstellen Sie eine Sicherung der benutzerdefinierten Datei „Configuration.mof“:** Wenn Sie eine benutzerdefinierte „Configuration.mof“-Datei verwenden, um die bei der Hardwareinventur verwendeten Datenklassen zu definieren, müssen Sie vor dem Update des Standorts eine Sicherung dieser Datei erstellen. Nach dem Update stellen Sie diese Datei am Standort der Version 1602 wieder her. Beim Update eines Standorts wird die aktuelle Datei durch die Originalversion (Standard) der Datei überschrieben. Weitere Informationen zur Verwendung dieser Datei finden Sie unter [Erweitern der Hardwareinventur](../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

 **Testen des Datenbank-Upgrades mit einer Kopie der letzten Sicherung der Standortdatenbank:** Bevor Sie einen Standort der zentralen Verwaltung oder einen primären Standort von Configuration Manager aktualisieren, testen Sie den Datenbankupgradeprozess mit einer Kopie der letzten Sicherung der Standortdatenbank.  

-   Sie sollten den Standortdatenbank-Upgradeprozess testen, da die Standortdatenbank während der Aktualisierung eines Standorts geändert werden kann.  

-   Ein Testdatenbankupgrade ist zwar nicht erforderlich, doch können dadurch Probleme beim Upgrade ermittelt werden, bevor die Produktionsdatenbank betroffen ist.  

-   Wenn beim Upgrade einer Standortdatenbank Fehler auftreten, ist die Datenbank möglicherweise nicht mehr betriebsfähig, und es müsste eine Standortwiederherstellung erfolgen.  

-   Obwohl die Standortdatenbank von allen Standorten in einer Hierarchie gemeinsam genutzt wird, sollten Sie die Datenbank an jedem relevanten Standort testen, bevor Sie das Upgrade für diesen Standort durchführen.  

-   Wenn Sie an einem primären Standort Datenbankreplikate für Verwaltungspunkte verwenden, deaktivieren Sie die Replikation, bevor Sie die Sicherung der Standortdatenbank erstellen.  

Configuration Manager unterstützt weder die Sicherung sekundärer Standorte noch das Testupgrade einer sekundären Standortdatenbank.   
Führen Sie kein Testdatenbankupgrade für die Datenbank des Produktionsstandorts aus. Dadurch würde ein Update der Standortdatenbank durchgeführt, und Ihr Standort wäre möglicherweise nicht mehr betriebsfähig. Weitere Informationen finden Sie im Abschnitt [Schritt 2: Testen des Datenbankupgrades vor der Installation eines Updates](install-in-console-updates.md#bkmk_step2) unter **Vor der Installation eines konsoleninternen Updates**.  

 **Planen von Pilottests für Clients:** Bei der Installation eines Updates, das den Client aktualisiert, können Sie das neue Clientupdate in der Präproduktionsphase testen, bevor es bereitgestellt wird und all Ihre aktiven Clients aktualisiert.   

 Um diese Option zu nutzen, müssen Sie Ihren Standort für die Unterstützung automatischer Updates für die Präproduktionsphase konfigurieren, bevor Sie die Installation des Updates starten. Weitere Informationen finden Sie unter [Upgraden von Clients](../../../core/clients/manage/upgrade/upgrade-clients.md) und   
[Testen von Clientupgrades in einer Präproduktionssammlung](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

 **Mithilfe von Wartungsfenstern können Sie planen, wann Standortserver Updates an einem Standort installieren:** Mithilfe der Wartungsfenster können Sie einen Zeitraum definieren, in dem Updates auf dem Standortserver installiert werden können. Damit können Sie steuern, wann das Update an Standorten in Ihrer Hierarchie installiert werden kann.   

Mit der Veröffentlichung des Updates 1602 werden Wartungsfenster in *Dienstfenster* umbenannt. Weitere Informationen finden Sie unter [Dienstfenster für Standortserver](service-windows.md).  

 **Führen Sie die Setup-Voraussetzungsprüfung aus:**  Vor der Installation des Updates 1602 können Sie die Voraussetzungsprüfung unabhängig von der Updateinstallation ausführen. Beim Installieren des Updates am Standort wird die Voraussetzungsprüfung erneut ausgeführt.  

Weitere Informationen finden Sie im Abschnitt **Schritt 3: Ausführen der Voraussetzungsprüfung vor der Installation eines Updates** im Artikel zu [Updates für Configuration Manager](../../../core/servers/manage/updates.md).  

> [!IMPORTANT]  
>  Wenn die Voraussetzungsprüfung im Rahmen einer Updateinstallation oder unabhängig davon ausgeführt wird, werden vom Prozess einige Produktquelldateien aktualisiert, die für Standortwartungstasks verwendet werden. Wenn Sie daher nach Durchführung der Voraussetzungsprüfung, aber vor Installation des Updates 1602 einen Standortwartungstask durchführen müssen, führen Sie **Setupwfe.exe** (Configuration Manager-Setup) im Ordner „CD.Latest“ auf dem Standortserver aus.  

 **Aktualisieren von Standorten:** Sie können nun die Updateinstallation für Ihre Hierarchie starten. Es wird empfohlen, die Installation des Updates für jeden Standort außerhalb der normalen Geschäftszeiten zu planen, wenn die Installation des Updates und die zugehörigen Aktionen zum Neuinstallieren von Standortkomponenten und Standortsystemrollen die geringsten Auswirkungen auf die Geschäftsvorgänge haben.

Weitere Informationen finden Sie unter [Updates für System Center Configuration Manager](../../../core/servers/manage/updates.md).  

## <a name="see-also"></a>Weitere Informationen:  
 [Updates für Configuration Manager](../../../core/servers/manage/updates.md)
