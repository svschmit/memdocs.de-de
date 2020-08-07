---
title: Überwachen von Clients
titleSuffix: Configuration Manager
description: Ausführliche Anleitungen zur Überwachung von Clients in Configuration Manager
ms.date: 07/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2c8f57cf-1968-48de-87fb-4897432ed6e0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 00a10e169db36c62b083c56114159b54185a1040
ms.sourcegitcommit: 7e34b561d43aa086fc07ab4edf2230d09c04f05b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87525912"
---
# <a name="how-to-monitor-clients-in-configuration-manager"></a>Überwachen von Clients in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Nachdem Sie den Configuration Manager-Client auf den Windows-Geräten in Ihrem Standort installiert haben, überwachen Sie deren Status und Aktivitäten in der Configuration Manager-Konsole.  


## <a name="about-client-status"></a><a name="bkmk_about"></a> Informationen zum Clientstatus

Configuration Manager stellt die folgenden Informationstypen als Clientstatus bereit:  

- **Onlinestatus von Clients**: Der Standort betrachtet ein Gerät als **online**, wenn es mit seinem zugewiesenen Verwaltungspunkt verbunden ist. Um anzugeben, dass der Client online ist, sendet er Ping-ähnliche Nachrichten an den Verwaltungspunkt. Wenn der Verwaltungspunkt innerhalb von fünf Minuten keine Nachricht empfängt, betrachtet der Standort den Client als **offline**.  

- **Clientaktivität**: Der Standort betrachtet den Client als **aktiv**, wenn er während der vergangenen sieben Tage mit Configuration Manager kommuniziert hat. Der Standort betrachtet den Client als **inaktiv**, wenn er innerhalb von sieben Tagen keine der folgenden Aktionen ausgeführt hat:  

    - Eine Richtlinienaktualisierung angefordert  
    - Eine Taktnachricht gesendet  
    - Eine Hardwareinventur gesendet  

- **Clientprüfung**: Der Status der regelmäßigen Überprüfung, die der Configuration Manager-Client auf dem Gerät ausführt. Bei dieser Prüfung gefundene Probleme können teilweise behoben werden. Weitere Informationen finden Sie unter [Clientintegritätsprüfungen](#BKMK_ClientHealth).  

     Auf Geräten mit Windows 7 wird die Clientüberprüfung als geplante Aufgabe ausgeführt. Bei höheren Betriebssystemversionen wird die Clientüberprüfung während des Windows-Wartungsfensters automatisch ausgeführt.  

     Sie können die Wiederherstellung so konfigurieren, dass sie auf bestimmten Geräten, beispielsweise einem geschäftskritischen Server, nicht ausgeführt wird. Wenn es zusätzliche Elemente gibt, die Sie auswerten möchten, verwenden Sie Configuration Manager-Konformitätseinstellungen, um zusätzliche Konfigurationen zu überwachen. Weitere Informationen zu Konformitätseinstellungen finden Sie unter [Planen und Konfigurieren von Konformitätseinstellungen](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md).  

- **Außer Betrieb gesetzt**: Der Standort hat den Gerätedatensatz zum Löschen markiert. Dieses Verhalten kann auftreten, wenn eine neue Registrierung für dasselbe Gerät demselben oder einem anderen primären Standort in einer Hierarchie zugewiesen wird. Der Standort löscht diese Geräte bei der nächsten Ausführung des Standortwartungstasks **Veraltete Ermittlungsdaten löschen**.<!-- SCCMDocs issue #1418 -->  

- **Veraltet**: Weil der Standort einen neuen Gerätedatensatz mit derselben Hardware-ID ermittelt hat, markiert er den alten Datensatz als veraltet. In Berichten werden veraltete Datensätze desselben Geräts nicht mehrmals gezählt. Sie können Richtlinien veralteten Geräten weiterhin zuordnen. Wenn der Standort nach 90 Tagen Inaktivität keine Taktnachricht für einen veralteten Datensatz erhalten hat, entfernt er das veraltete Gerät bei der Ausführung des Standortwartungstasks **Veraltete Clientermittlungsdaten löschen**.


## <a name="monitor-individual-clients"></a><a name="bkmk_indStatus"></a> Überwachen von einzelnen Clients

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Assets und Konformität**. Wählen Sie entweder den Knoten **Geräte** oder unter **Gerätesammlungen** die gewünschte Sammlung aus.  

    Die Symbole am Anfang jeder Zeile geben den Onlinestatus des Geräts an:  

    | Symbol | Beschreibung |
    | ---- | ----------- |  
    |![Symbol für den Onlinestatus des Clients](../../../core/clients/manage/media/online-status-icon.png)|Gerät ist online.|  
    |![Symbol für den Offlinestatus des Clients](../../../core/clients/manage/media/offline-status-icon.png)|Gerät ist offline.|  
    |![Symbol für den unbekannten Status des Clients](../../../core/clients/manage/media/unknown-status-icon.png)|Onlinestatus ist unbekannt.|  
    |![Client ist nicht installiert](../../../core/clients/manage/media/client-not-installed.png)|Client ist auf dem Gerät nicht installiert.|  

2. Wenn Sie mehr über den Onlinestatus wissen möchten, fügen Sie der Geräteansicht die Informationen zum Onlinestatus von Clients hinzu. Klicken Sie mit der rechten Maustaste auf den Spaltenkopf, und wählen Sie die Onlinestatusfelder aus, die Sie hinzufügen möchten:

    - **Onlinestatus des Geräts**: Gibt an, ob der Client derzeit online oder offline ist. (Dieser Status entspricht den von den Symbolen angezeigten Informationen.)  

    - **Zuletzt online**: Gibt an, wann sich der Status des Clients in „online“ geändert hat.  

    - **Zuletzt offline** gibt an, wann sich der Status des Clients in „offline“ geändert hat.  

3. Wählen Sie einen einzelnen Client im Listenbereich aus, um weitere Statusinformationen im Detailbereich anzuzeigen. Diese Informationen umfassen die Clientaktivitäten und den Status der Clientprüfung.  


## <a name="client-health-dashboard"></a><a name="bkmk_health"></a> Dashboard „Clientintegrität“

<!--3599209-->
Softwareupdates und andere Apps werden zum Schutz der Umgebung bereitgestellt. Diese Bereitstellungen erreichen jedoch nur fehlerfreie Clients. Fehlerhafte Configuration Manager-Clients beeinträchtigen die Konformität insgesamt. Je nach Nenner – Anzahl der Geräte, die insgesamt verwaltet werden sollen – kann die Ermittlung der Clientintegrität eine gewisse Herausforderung darstellen. Der Nenner ist umso größer, wenn Sie alle Systeme aus Active Directory ermitteln, auch wenn einige dieser Datensätze zu ausgemusterten Computern gehören.

Ab Version 1902 können Sie ein Dashboard mit Informationen zur Integrität von Configuration Manager-Clients in Ihrer Umgebung anzeigen. Zeigen Sie die Clientintegrität, Szenariointegrität und allgemeine Fehler an. Filtern Sie die Ansicht nach verschiedenen Attributen, um alle potenziellen Probleme nach Betriebssystem- und Clientversion anzuzeigen.

Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Überwachung**. Erweitern Sie **Clientstatus**, und wählen Sie den Knoten **Dashboard „Clientintegrität“** aus.

![Screenshot des Dashboards „Clientintegrität“](media/3599209-client-health-dashboard.png)

> [!Tip]  
> Es gibt keine Änderungen an ccmeval.  

Standardmäßig werden im Dashboard „Clientintegrität“ nur Onlineclients und Clients angezeigt, die in den letzten drei Tagen aktiv waren. Deshalb werden möglicherweise andere Zahlen im Dashboard als in anderen verlaufsbezogenen Quellen der Clientintegrität angezeigt, beispielsweise andere Knoten unter **Clientstatus** oder Berichte in der Kategorie „Clientstatus“.

### <a name="filters"></a>Filter

Oben im Dashboard werden Filter zum Anpassen der im Dashboard angezeigten Daten angezeigt.

- **Sammlung:** Standardmäßig werden im Dashboard Geräte in der Sammlung **Alle Systeme** angezeigt. Wählen Sie in der Liste eine Gerätesammlung aus, um die Ansicht auf eine Teilmenge von Geräten in einer bestimmten Sammlung zu begrenzen.  

- **Online/offline**: Standardmäßig werden im Dashboard nur Onlineclients angezeigt. Dieser Status stammt vom Clientbenachrichtigungskanal, über den der Status eines Clients alle fünf Minuten aktualisiert wird. Weitere Informationen finden Sie unter [Informationen zum Clientstatus](monitor-clients.md#bkmk_about).  

- **Aktive \# Tage**: Standardmäßig werden im Dashboard Clients angezeigt, die während der letzten drei Tage aktiv waren.  

- **Failure only** (Nur Fehler): Die Ansicht wird auf die Geräte beschränkt, die einen Clientintegritätsfehler melden.  

    > [!Tip]  
    > Verwenden Sie diesen Filter zusammen mit den Kacheln für Client- und Betriebssystemversion. Weitere Informationen finden Sie unter [Versionskacheln](#version-tiles).

### <a name="client-health-percentage"></a>Prozentsatz für Clientintegrität

Auf dieser Kachel wird die Clientintegrität insgesamt in der Hierarchie angezeigt.

Ein fehlerfreier Configuration Manager-Client weist folgende Eigenschaften auf:

- Online  
- Sendet aktiv Daten  
- Erhält bei allen Prüfungen der Clientintegrität eine gute Bewertung  

Weitere Informationen finden Sie unter [Informationen zum Clientstatus](monitor-clients.md#bkmk_about).

Ein fehlerfreier Client kommuniziert erfolgreich mit dem Standort. Er meldet alle Daten basierend auf den in den Clienteinstellungen definierten Zeitplänen.

Wählen in diesem Diagramm ein Segment aus, um in einer Listenansicht mit Geräten Detailinformationen anzuzeigen.

### <a name="version-tiles"></a>Versionskacheln

Es gibt zwei Kacheln, auf denen die Clientintegrität nach der Version des Configuration Manager-Clients bzw. nach der Betriebssystemversion angezeigt wird. Diese Kacheln sind nützlich, wenn Sie an den Filtern wie etwa am Filter **Failure only** (Nur Fehler) Änderungen vornehmen. Damit kann hervorgehoben werden, ob Probleme in einer bestimmten Version konsistent auftreten. Verwenden Sie diese Informationen für Ihre Entscheidung hinsichtlich eines Upgrades.

Wählen in diesen Diagrammen ein Segment aus, um in einer Listenansicht mit Geräten Detailinformationen anzuzeigen.

### <a name="scenario-health"></a>Szenariointegrität

In diesem Balkendiagramm wird die Gesamtintegrität für folgende Kernszenarios dargestellt:

- Clientrichtlinie
- Taktermittlung
- Hardwareinventur
- Softwareinventur
- Statusmeldungen

Richten Sie mithilfe der Selektoren den Fokus auf bestimmte Szenarios im Diagramm.

Die folgenden beiden Balken werden immer angezeigt:

- **Kombiniert (alle)** : Kombination aller Szenarios (UND)  
- **Kombiniert (beliebig)** : mindestens ein Szenario (ODER)

> [!Tip]  
> Die Szenariointegrität wird nicht über Ihre Konfiguration der Clienteinstellungen gemessen. Diese Werte können je nach Richtlinienergebnissatz pro Gerät variieren. Führen Sie die folgenden Schritte aus, um die Auswertungszeiträume für die Szenariointegrität anzupassen:
>
> - Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Überwachung**, und wählen Sie den Knoten **Clientstatus** aus.  
> - Wählen Sie im Menüband **Client-Statuseinstellungen** aus.  
>
> Wenn ein Client innerhalb von **7 Tagen** keine szenariospezifischen Daten sendet, wird er von Configuration Manager standardmäßig als fehlerhaft eingestuft.

### <a name="top-10-client-health-failures"></a>Top 10 der Clientintegritätsfehler

In diesem Diagramm werden die in Ihrer Umgebung am häufigsten auftretenden Fehler aufgeführt. Diese Fehler stammen von Windows oder Configuration Manager.

<!-- The following list includes some of the more common failures overall:

#### Failure 1 title
Failure 1 description

Solution for failure 1 -->


## <a name="monitor-the-status-of-all-clients"></a><a name="bkmk_allStatus"></a> Überwachen des Status aller Clients

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Überwachung**, und wählen Sie den Knoten **Clientstatus** aus. Überprüfen Sie die Gesamtstatistiken für Clientaktivitäten und Clientprüfungen für den gesamten Standort. Ändern Sie den Umfang der Informationen, indem Sie eine andere Sammlung auswählen.  

2. Um Detailinformationen zu den gemeldeten Statistiken anzuzeigen, wählen Sie den Namen der gemeldeten Information aus. Zum Beispiel: **Active clients that have passed client check or no results** (Aktive Clients, die die Clientprüfung bestanden haben oder für die keine Ergebnisse vorliegen). Überprüfen Sie dann die Informationen zu den einzelnen Clients.  

3. Wählen Sie **Clientaktivität** aus, um Diagramme mit den Clientaktivitäten an Ihrem Configuration Manager-Standort anzuzeigen.  

4. Wählen Sie **Clientprüfung** aus, um Diagramme zum Status von Clientprüfungen an Ihrem Configuration Manager-Standort anzuzeigen.  

    Konfigurieren Sie Warnungen, damit Sie benachrichtigt werden, wenn die Ergebnisse der Clientprüfung oder die Clientaktivitäten unter einen angegebenen Prozentsatz sinken. Der Standort kann sie auch warnen, wenn die Wiederherstellung bei einem angegebenen Prozentsatz von Clients nicht ausgeführt werden kann. Weitere Informationen finden Sie unter [Konfigurieren des Clientstatus](../deploy/configure-client-status.md).  


## <a name="client-health-checks"></a><a name="BKMK_ClientHealth"></a> Client-Integritätsprüfungen

Die Clientprüfung führt die folgenden Prüfungen und Wiederherstellungsmaßnahmen aus:  

|Clientprüfung|Wiederherstellungsmaßnahme|Weitere Informationen|  
|------------------|------------------------|----------------------|  
|Überprüfen Sie, ob die Clientprüfung vor Kurzem ausgeführt wurde|Führen Sie die Clientprüfung aus|Es wird überprüft, ob die Clientprüfung mindestens einmal innerhalb der letzten drei Tage ausgeführt wurde.|  
|Überprüfen Sie, ob die erforderlichen Clientkomponenten installiert sind|Installieren Sie die erforderlichen Clientkomponenten|Es wird überprüft, ob die erforderlichen Clientkomponenten installiert sind. Es wird die Datei ccmsetup.xml im Installationsordner des Clients ausgelesen, um die erforderlichen Komponenten herauszufinden.|  
|WMI-Repository-Integritätstest|Installieren Sie den Configuration Manager-Client erneut.|Überprüft, ob Configuration Manager-Clienteinträge in WMI vorhanden sind|  
|Überprüfen Sie, ob der Clientdienst ausgeführt wird|Starten Sie den Clientdienst (SMS-Agent-Host)|Keine zusätzlichen Informationen|  
|WMI-Ereignissenkentest.|Starten Sie den Clientdienst neu|Überprüfen Sie, ob die Configuration Manager-bezogene WMI-Ereignissenke verloren gegangen ist|  
|Überprüfen Sie, ob der WMI-Dienst (Windows-Verwaltungsinstrumentation) vorhanden ist|Keine Behebung|Keine zusätzlichen Informationen|  
|Überprüfen Sie, ob der Client ordnungsgemäß installiert wurde|Installieren Sie den Client erneut|Keine zusätzlichen Informationen|  
|Überprüfen Sie, ob der Antischadsoftware-Dienststarttyp auf Automatisch eingestellt ist|Setzen Sie den Dienststarttyp zurück auf Automatisch|Keine zusätzlichen Informationen|  
|Stellen Sie sicher, dass der Antischadsoftwaredienst ausgeführt wird.|Starten Sie den Antischadsoftwaredienst|Keine zusätzlichen Informationen|  
|Überprüfen Sie, ob der Dienststarttyp für Windows Update auf Automatisch oder Manuell eingestellt ist|Setzen Sie den Dienststarttyp zurück auf Automatisch|Keine zusätzlichen Informationen|  
|Überprüfen Sie, ob der Starttyp des Clientdienstes (SMS-Agent-Host) auf Automatisch eingestellt ist|Setzen Sie den Dienststarttyp zurück auf Automatisch|Keine zusätzlichen Informationen|  
|Überprüfen Sie, ob der WMI-Dienst (Windows-Verwaltungsinstrumentation) ausgeführt wird.|Starten Sie den Dienst Windows-Verwaltungsinstrumentation (WMI)|Keine zusätzlichen Informationen|  
|Überprüfen Sie die Integrität der Microsoft SQL CE-Datenbank|Installieren Sie den Configuration Manager-Client erneut.|Keine zusätzlichen Informationen|  
|WMI-Integritätstest der Microsoft Policy Platform|Reparieren der Microsoft Policy Platform|Keine zusätzlichen Informationen|  
|Stellen Sie sicher, dass der Microsoft Policy Platform-Dienst vorhanden ist|Reparieren der Microsoft Policy Platform|Keine zusätzlichen Informationen|  
|Überprüfen Sie, ob der Dienststarttyp der Microsoft Policy Platform auf Manuell eingestellt ist.|Setzen Sie den Dienststarttyp zurück auf Manuell|Keine zusätzlichen Informationen|  
|Überprüfen Sie, ob der intelligente Hintergrundübertragungsdienst (BITS) vorhanden ist|Keine Behebung|Keine zusätzlichen Informationen|  
|Überprüfen Sie, ob der Starttyp für den intelligenten Hintergrundübertragungsdienst auf Automatisch oder Manuell eingestellt ist|Setzen Sie den Dienststarttyp zurück auf Automatisch|Keine zusätzlichen Informationen|  
|Überprüfen Sie, ob der Starttyp für den Netzwerkinspektionsdienst auf Manuell eingestellt ist|Setzen Sie den Dienststarttyp zurück auf Manuell, falls er installiert ist|Keine zusätzlichen Informationen|  
|Überprüfen Sie, ob der Dienststarttyp für Windows-Verwaltungsinstrumentation (WMI) auf Automatisch eingestellt ist|Setzen Sie den Dienststarttyp zurück auf Automatisch|Keine zusätzlichen Informationen|  
|Überprüfen Sie, ob der Dienststarttyp für Windows Update auf Windows 8-Geräten auf Automatisch oder Manuell eingestellt ist|Setzen Sie den Dienststarttyp zurück auf Manuell|Keine zusätzlichen Informationen|  
|Überprüfen Sie, ob der Clientdienst (SMS-Agent-Host) vorhanden ist.|Keine Behebung|Keine zusätzlichen Informationen|  
|Überprüfen Sie, ob der Dienststarttyp für die Remotesteuerung in Configuration Manager auf Automatisch oder Manuell eingestellt ist|Setzen Sie den Dienststarttyp zurück auf Automatisch|Keine zusätzlichen Informationen|  
|Überprüfen Sie, ob der Dienst „Remotesteuerung in Configuration Manager“ ausgeführt wird|Starten Sie den Remotesteuerungsdienst|Keine zusätzlichen Informationen|  
|Überprüfen Sie, ob der Aktivierungsproxydienst (ConfigMgr-Aktivierungsproxy) ausgeführt wird|Starten Sie den ConfigMgr-Aktivierungsproxydienst|Diese Clientprüfung wird nur vorgenommen, wenn die Clienteinstellung unter **Energieverwaltung**: **Aktivierungsproxy zulassen** auf unterstützten Clientbetriebssystemen auf **Ja** festgelegt ist.|  
|Überprüfen Sie, ob der Starttyp für den Aktivierungsproxydienst (ConfigMgr-Aktivierungsproxy) auf Automatisch eingestellt ist|Setzen Sie den Dienststarttyp für den ConfigMgr-Aktivierungsproxy zurück auf Automatisch|Diese Clientprüfung wird nur vorgenommen, wenn die Clienteinstellung unter **Energieverwaltung**: **Aktivierungsproxy zulassen** auf unterstützten Clientbetriebssystemen auf **Ja** festgelegt ist.|  


<!-- 
5/31/2019 ACz: need to confirm if these checks are still applicable
|WMI repository read and write test|Reset the WMI repository and reinstall the Configuration Manager client|Remediation of this client check is only performed on devices that run Windows Server 2003, Windows XP (64-bit) or earlier versions.|  
|Verify that the client WMI provider is healthy|Restart the Windows Management Instrumentation service|Remediation of this client check is only performed on devices that run Windows Server 2003, Windows XP (64-bit) or earlier.|  
 -->


## <a name="client-deployment-log-files"></a>Clientbereitstellungs-Protokolldateien

Weitere Informationen zu den Protokolldateien, die von Clientbereitstellungs- und -verwaltungsvorgängen verwendet werden, finden Sie unter [Protokolldateien](../../plan-design/hierarchy/log-files.md#BKMK_ClientLogs).
