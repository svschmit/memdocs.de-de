---
title: Standortkomponenten
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Standortkomponenten so konfiguriert werden, dass sich das Verhalten von Standortsystemrollen und die Statusberichterstellung des Standorts ändert.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5fccbbeb-0faa-4943-83c2-e67db62d392d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a3447e6ac71e9c5441a9e82034ee41eabda59374
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700928"
---
# <a name="site-components-for-configuration-manager"></a>Standortkomponenten für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Für jeden Configuration Manager-Standort können Sie Standortkomponenten konfigurieren, um das Verhalten von Standortsystemrollen und die Statusberichterstellung des Standorts zu ändern. Konfigurationen von Standortkomponenten gelten für einen Standort sowie für jede Instanz einer anwendbaren Standortsystemrolle am Standort.  

Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie den Knoten **Standorte** aus. Wählen Sie einen Standort aus. Klicken Sie in der Menübandgruppe **Einstellungen** auf **Standortkomponenten konfigurieren**. Wählen Sie eine der folgenden Optionen aus:

- [Softwareverteilung](#software-distribution)  
- [Softwareupdatepunkt](#software-update-point) 
- [Betriebssystembereitstellung](#operating-system-deployment)
- [Verwaltungspunkt](#management-point)  
- [Statusberichterstattung](#status-reporting)  
- [E-Mail-Benachrichtigung](#email-notification)
- [Auswertung der Sammlungsmitgliedschaft](#bkmk_colleval)


## <a name="about-site-components"></a>Informationen zu Standortkomponenten  

 Die meisten Optionen für die verschiedenen Standortkomponenten sind bei Anzeige in der Configuration Manager-Konsole selbsterklärend. Allerdings können die folgenden Details Ihnen bei der Erläuterung einiger komplexerer Konfigurationen helfen oder Sie auf zusätzliche Inhalte verweisen.  

> [!Note]  
> Für einige Komponenten variieren die verfügbaren Optionen, je nachdem, ob Sie den Standort der zentralen Verwaltung, einen primären Standort oder einen sekundären Standort auswählen. Einige Komponenten sind für bestimmte Standorttypen nicht verfügbar.  



### <a name="software-distribution"></a>Softwareverteilung  

#### <a name="content-distribution-settings"></a>Einstellungen für die Inhaltsverteilung
Legen Sie auf der Registerkarte **Allgemein** Einstellungen fest, die ändern, wie der Standortserver Inhalte an seine Verteilungspunkte überträgt. Wenn Sie die Werte der Einstellungen für die gleichzeitige Verteilung erhöhen, kann die Inhaltsverteilung mehr Netzwerkbandbreite nutzen.  

#### <a name="pull-distribution-point"></a>Pullverteilungspunkt
Weitere Informationen finden Sie unter [Use a pull-distribution point (Verwenden eines Verteilungspunkts)](../../../plan-design/hierarchy/use-a-pull-distribution-point.md).

#### <a name="network-access-account"></a>Netzwerkzugriffskonto
Weitere Informationen finden Sie unter [Netzwerkzugriffskonto](../../../plan-design/hierarchy/accounts.md#network-access-account).  


### <a name="software-update-point"></a>Softwareupdatepunkt  

Weitere Informationen finden Sie unter [Install a software update point (Installieren eines Softwareupdatepunkts)](../../../../sum/get-started/install-a-software-update-point.md).  


### <a name="operating-system-deployment"></a>Betriebssystembereitstellung

Weitere Informationen finden Sie unter [Angeben des Laufwerks für die Offlinewartung von Betriebssystemimages](../../../../osd/get-started/manage-operating-system-images.md#bkmk_servicing-drive).


### <a name="management-point"></a>Verwaltungspunkt  

Richten Sie den Standort auf der Registerkarte **Allgemein** so ein, dass Informationen zu seinen Verwaltungspunkten in Active Directory Domain Services veröffentlicht werden.  

Verwaltungspunkte werden von Configuration Manager-Clients verwendet, um Dienste zu suchen und Standortinformationen wie Zugehörigkeit zu Begrenzungsgruppen und PKI-Zertifikat-Auswahloptionen zu finden. Clients verwenden auch Verwaltungspunkte, um nach anderen Verwaltungspunkten am Standort sowie nach Verteilungspunkte zu suchen, von denen Software heruntergeladen werden kann. Bei Clients werden Verwaltungspunkte darüber hinaus verwendet, um Standortzuweisungen abzuschließen, Clientrichtlinien herunterzuladen und ihre Clientinformationen hochzuladen.  

Die sicherste Methode für Clients zum Suchen nach Verwaltungspunkten besteht darin, sie in Active Directory Domain Services zu veröffentlichen. Für diese Dienstidentifizierungsmethode müssen folgende Voraussetzungen erfüllt sein:

- Das Schema wird für Configuration Manager erweitert.
- Es gibt einen **System Management**-Container mit entsprechenden Sicherheitsberechtigungen für den Standortserver zum Veröffentlichen in diesen Container.
- Der Configuration Manager-Standort ist zur Veröffentlichung in Active Directory-Domänendiensten eingerichtet.
- Clients gehören derselben Active Directory-Gesamtstruktur an wie die Gesamtstruktur des Standortservers.  

Wenn es für Clients im Intranet nicht möglich ist, Verwaltungspunkte mithilfe von Active Directory Domain Services zu suchen, verwenden Sie die [DNS-Veröffentlichung](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_dns).  

Allgemeine Informationen zur Dienstidentifizierung durch Clients finden Sie unter [Understand how clients find site resources and services (Informationen zur Suche nach Standortressourcen und -diensten durch Clients)](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  


#### <a name="publish-selected-intranet-management-points-in-dns"></a>Ausgewählte Intranetverwaltungspunkte in DNS veröffentlichen
Legen Sie diese Option fest, wenn Clients keine Verwaltungspunkte über Active Directory Domain Services finden können. Stattdessen können sie einen DNS-Ressourceneintrag zur Dienstidentifizierung (SRV RR) verwenden, um einen Verwaltungspunkt am ihnen zugewiesenen Standort zu finden.  

Damit in Configuration Manager Intranetverwaltungspunkte in DNS veröffentlicht werden können, müssen die beiden folgenden Bedingungen erfüllt sein:  

-   Ihre DNS-Server verfügen mindestens über die BIND-Version 8.1.2.  

-   Ihre DNS-Server sind für automatische Updates eingerichtet und unterstützen Ressourceneinträge zur Dienstidentifizierung.  

-   Zu den angegebenen vollständig qualifizierte Domänennamen (FQDNs) für die Verwaltungspunkte in Configuration Manager müssen Hosteinträge (A- oder AAA-Datensätze) in DNS vorhanden sein.  

> [!WARNING]  
>  Damit von Clients in DNS veröffentlichte Verwaltungspunkte gefunden werden können, müssen Sie die Clients einem bestimmten Standort zuweisen, anstatt die automatische Standortzuweisung zu verwenden. Richten Sie diese Clients so aus, dass sie den Standortcode mit dem Domänensuffix ihres Verwaltungspunkts verwenden. Weitere Informationen finden Sie unter [Suchen von Verwaltungspunkten](../../../clients/deploy/assign-clients-to-a-site.md#locating-management-points).  

Wenn es für Configuration Manager-Clients nicht möglich ist, Verwaltungspunkte mithilfe von Active Directory Domain Services oder DNS im Intranet zu finden, wird [WINS](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_wins) verwendet. Der erste für einen Standort installierte Verwaltungspunkt wird automatisch in WINS veröffentlicht, wenn er für das Zulassen von HTTP-Clientverbindungen im Intranet eingerichtet wird.  


### <a name="status-reporting"></a>Statusberichterstattung  

Diese Einstellungen dienen zum direkten Einrichten der Detailebene, die in Statusberichte von Standorten und Clients einbezogen wird.  


### <a name="email-notification"></a>E-Mail-Benachrichtigung  

Geben Sie Konto- und E-Mail-Serverdetails an, um Configuration Manager das Senden von E-Mail-Benachrichtigungen zu Warnungen zu ermöglichen.  

Weitere Informationen finden Sie unter [Verwenden von Benachrichtigungen und Statussystem](../../manage/use-alerts-and-the-status-system.md).


### <a name="collection-membership-evaluation"></a><a name="bkmk_colleval"></a> Auswertung der Sammlungsmitgliedschaft  

Verwenden Sie diese Komponente, um die Häufigkeit der inkrementellen Auswertung der Sammlungsmitgliedschaft festzulegen. Bei der inkrementellen Auswertung wird eine Sammlungsmitgliedschaft nur mit neuen oder geänderten Ressourcen aktualisiert.  

Weitere Informationen finden Sie unter [Bewährte Methoden für Sammlungen](../../../clients/manage/collections/best-practices-for-collections.md).



##  <a name="use-the-configuration-manager-service-manager-to-manage-site-components"></a><a name="BKMK_ServiceMgr"></a> Verwalten von Standortkomponenten mit dem Dienst-Manager für Configuration Manager  

Mit dem Dienst-Manager für Configuration Manager können Sie Configuration Manager-Dienste steuern und den Status von Configuration Manager-Diensten oder -Arbeitsthreads anzeigen. Diese Dienste und Threads werden zusammen als Configuration Manager-Komponenten bezeichnet. Folgendes müssen Sie über Configuration Manager-Komponenten wissen:  

-   Komponenten können auf beliebigen Standortsystemen ausgeführt werden.  

-   Komponenten werden auf dieselbe Weise verwaltet wie Dienste in Windows. Sie können die Configuration Manager-Komponenten starten, beenden, anhalten, fortsetzen oder abfragen.  

Ein Configuration Manager-Dienst wird ausgeführt, wenn es etwas für ihn zu tun gibt. Dies findet in der Regel statt, wenn eine Konfigurationsdatei in den Eingang einer Komponente geschrieben wird. 


### <a name="use-the-configuration-manager-service-manager"></a>So verwenden Sie den Dienst-Manager für Configuration Manager  

1.  Öffnen Sie in der Configuration Manager-Konsole den Arbeitsbereich **Überwachung**, erweitern Sie den **Systemstatus**, und wählen Sie den Knoten **Komponentenstatus** aus.  

2.  Klicken Sie in der Menübandgruppe **Komponente** auf **Starten**, und wählen Sie dann **Dienst-Manager für Configuration Manager** aus.  

3.  Wenn der Dienst-Manager für Configuration Manager geöffnet wird, stellen Sie eine Verbindung mit dem zu verwaltenden Standort her.  

     Wenn der Standort, den Sie verwalten möchten, nicht angezeigt wird, öffnen Sie das Menü **Standort**, und klicken Sie auf **Verbinden**. Geben Sie dann den Namen des Standortservers des gewünschten Standorts ein.  

4.  Erweitern Sie den Standort, und wechseln Sie zu **Komponenten** oder **Server**, je nachdem, wo die zu verwaltenden Komponenten sich befinden.  

5.  Wählen Sie im rechten Fensterbereich eine oder mehrere Komponenten aus. Klicken Sie dann im Menü **Komponente** auf **Abfragen**, um den Status Ihrer Auswahl zu aktualisieren.  

6.  Nachdem der Status der Komponente aktualisiert wurde, verwenden Sie eine der vier aktionsbasierten Optionen im Menü **Komponente**, um das Verhalten der Komponente zu ändern. Nachdem eine Aktion angefordert wurde, müssen Sie die Komponente abfragen, um den neuen Status der Komponente anzuzeigen.  

7.  Schließen Sie den Dienst-Manager für Configuration Manager, wenn Sie das Bearbeiten des Betriebsstatus der Komponenten abgeschlossen haben.  
