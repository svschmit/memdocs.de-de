---
title: Funktionen in Technical Preview 1511
titleSuffix: Configuration Manager
description: Erfahren Sie mehr zu Features, die in Technical Preview für Configuration Manager-Version 1511 zur Verfügung stehen.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 69473706-21b3-498b-a67e-670fdc988f0d
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 337b494bdce24463c19dd22ae975af5e99d6d895
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905847"
---
# <a name="capabilities-in-technical-preview-1511-for-configuration-manager"></a>Funktionen in der Technical Preview 1511 für Configuration Manager

*Gilt für: Configuration Manager (Technical Preview-Branch)*

In diesem Artikel werden die Features vorgestellt, die in der Technical Preview-Version 1511 für Configuration Manager verfügbar sind. Bei dieser Version handelt es sich um eine Basisinstallation für die Technical Preview, die Sie verwenden können, um einen neuen Technical Preview-Standort zu installieren oder um ein Upgrade von einer früheren Version der Technical Preview durchzuführen.   Bevor Sie diese Version der Technical Preview installieren, lesen Sie das einführende Thema [Technical Preview für Configuration Manager](technical-preview.md), um sich mit den allgemeinen Anforderungen und Einschränkungen bei der Verwendung einer Technical Preview vertraut zu machen und um zu erfahren, wie Sie Updates für Versionen durchführen und Feedback zu den Features in einer Technical Preview geben können.  

Im Folgenden werden neue Funktionen aufgelistet, die Sie mit dieser Version ausprobieren können.  

##  <a name="integration-with-windows-update-for-business-in-windows-10"></a><a name="BKMK_WUfB"></a> Integration mit Windows Update für Unternehmen in Windows 10  
 Configuration Manager verfügt jetzt über die Möglichkeit, einen Windows 10-Computer, der direkt über Windows Update für Unternehmen (WUfB, Windows Update for Business) verbunden ist, von solchen zu unterscheiden, die mit WSUS verbunden sind, um Windows 10-Updates und -Upgrades abzurufen.  Bei Computern, die über WUfB verbunden sind, können die Updates und Upgrades in dem vom administrativen Benutzer mittels Gruppenrichtlinien oder MDM-Richtlinien festgelegten Rhythmus verwaltet werden, und diese Updates/Upgrades können direkt aus WUfB installiert werden.    
Für Computer, die über WUfB verbunden sind, kann Configuration Manager keine Meldungen zum Kompatibilitätsstatus abgeben (einschließlich Windows Updates oder Definitionsupdates). Außerdem kann Configuration Manager auf diesen Computern weder Microsoft-Updates noch Updates von Drittanbietern bereitstellen.  

 **Voraussetzungen für dieses Szenario:**  

-   Windows 10 Desktop Pro oder Windows 10 Enterprise Edition, Version 1511 oder höher  

-   Computer, die über [Windows Update für Unternehmen](https://docs.microsoft.com/windows/deployment/update/waas-manage-updates-wufb)verwaltet werden sollen.  

### <a name="try-it-out"></a>Probieren Sie es aus!  
 Versuchen Sie, die folgende Aufgabe auszuführen, und verwenden Sie dann die Feedbackinformationen oben in diesem Thema, um uns Ihre Erfahrungen mitzuteilen:  

1.  Deaktivieren Sie den Windows Update-Agent, damit er nicht auf WSUS sucht, wenn er zuvor aktiviert war.   
    Der Registrierungsschlüssel **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\useWSUSServer** kann so festgelegt werden, dass er anzeigt, ob der Computer auf WSUS oder Windows Update sucht.  Wenn der Wert „2“ ist, sucht er nicht auf WSUS.  

2.  Notieren Sie sich das neue Attribut **UseWUServer**unter dem Knoten **Windows Update** im Ressourcen-Explorer von Configuration Manager.  

3.  Erstellen Sie eine Sammlung auf Basis des **UseWUServer** -Attributs für alle Computer, die für Updates und Upgrades über WUfB verbunden sind.  

4.  Erstellen Sie eine Client-Agent-Einstellung, um den Softwareupdate-Workflow zu deaktivieren, und stellen Sie die Einstellung in der Sammlung von Computern bereit, die direkt mit WUfB verbunden sind.  

5.  Die Computer, die über WUfB verwaltet werden, zeigen als Kompatibilitätsstatus **Unbekannt** an und werden im Gesamtprozentsatz der Kompatibilität nicht berücksichtigt.  

##  <a name="managing-office-365-proplus-client-update-through-configuration-manager"></a><a name="BKMK_Office365ProPlus"></a> Verwalten von Office 365 ProPlus-Clientupdates über Configuration Manager  
 Configuration Manager verfügt jetzt über die Möglichkeit zum Verwalten von Office 365-Desktopclientupdates mithilfe des Softwareupdateverwaltungs-Workflows von Configuration Manager.    
Wenn Microsoft ein neues Office 365-Desktopclientupdate in Windows Server Updates Services (WSUS) veröffentlicht, kann Configuration Manager das Update mit seinem Katalog synchronisieren, wenn das Office 365-Update als Teil der Katalogsynchronisierung konfiguriert ist.  Der Configuration Manager-Standortserver lädt dann die Office 365-Clientupdates herunter, und verteilt das Paket an die Configuration Manager-Verteilungspunkte.  Der Configuration Manager-Client informiert dann die Office 365-Desktopclients, wo sie die Updates abrufen können und wann der Installationsvorgang gestartet werden soll.  

**Voraussetzungen für dieses Szenario:**  

### <a name="try-it-out"></a>Probieren Sie es aus!  
 Versuchen Sie, die folgende Aufgabe auszuführen, und verwenden Sie dann die Feedbackinformationen oben in diesem Thema, um uns Ihre Erfahrungen mitzuteilen:  

1. Sie können Office 365-Updates mit dem Configuration Manager-Standortserver synchronisieren und sie über die Configuration Manager-Konsole anzeigen.  

2. Sie können Office 365-Updates genehmigen und erfolgreich bereitstellen.  

3. Sie können Office 365-Updates herunterladen und erfolgreich für Clients bereitstellen.  

4. Sie können die Kompatibilität für Office 365-Updates mithilfe der Überwachung und Berichte in der Konsole überprüfen.  

   Detaillierte Anweisungen finden Sie unter [Verwalten von Updates für Office 365 ProPlus mit dem Microsoft Endpoint Configuration Manager](https://docs.microsoft.com/deployoffice/manage-microsoft-365-apps-updates-configuration-manager).  

##  <a name="support-for-sql-server-alwayson-for-highly-available-databases"></a><a name="BKMK_AlwasyOn"></a> Unterstützung für SQL Server AlwaysOn für hoch verfügbare Datenbanken  
 Configuration Manager unterstützt jetzt die Verwendung einer SQL Server Always On-Verfügbarkeitsgruppe zum Hosten der Standortdatenbank.  Wenn Sie einen neuen Standort installieren, können Sie das Setup anweisen, anstatt einer normalen Instanz von SQL Server die Verfügbarkeitsgruppe zu verwenden.  

> [!NOTE]  
>  Eine erfolgreiche Konfiguration und Verwendung von Verfügbarkeitsgruppen setzt voraus, dass Sie mit der Konfiguration von SQL Server-Verfügbarkeitsgruppen vertraut sind, und basiert auf der Dokumentation und den Verfahren in der SQL Server-Dokumentationsbibliothek.  

Das allgemeine Vorgehen beim Konfigurieren und Verwenden von Verfügbarkeitsgruppen umfasst folgende Schritte:  

1.  Konfigurieren Sie die Verfügbarkeitsgruppe in SQL Server.  

2.  Installieren Sie einen neuen Configuration Manager-Standort, und weisen Sie den Standort während des Setups an, die Verfügbarkeitsgruppe zu verwenden, indem Sie den Endpunkt der Gruppe angeben.  

**Voraussetzungen für dieses Szenario:**  

-   Eine Version von SQL Server ist erforderlich, die von der Configuration Manager Technical Preview unterstützt wird.  

-   Sie müssen die SQL Server-Verfügbarkeitsgruppe vor der Installation von Configuration Manager erstellen und konfigurieren.  

-   Die Verfügbarkeitsgruppe muss ein primäres Replikat und kann bis zu zwei synchrone sekundäre Replikate enthalten.  

-   Die Verfügbarkeitsgruppe muss mindestens einen Endpunkt besitzen.  

-   Sie benötigen einen Speicherort im Netzwerk, auf den jede SQL Server-Instanz in der Verfügbarkeitsgruppe zugreifen kann. Dieser Speicherort wird von Setup bei der Konfiguration der Verfügbarkeitsgruppe verwendet und kann nach Abschluss des Setups entfernt werden.  

**Bekannte Probleme in diesem Release:**  

-   Sie können zu einer Verfügbarkeitsgruppe, die bereits als Standortdatenbank verwendet wird, kein neues Replikatmitglied erfolgreich hinzufügen. Stattdessen müssen Sie den Standort neu installieren, nachdem das neue Replikatmitglied hinzugefügt wurde.  

-   In diesem Szenario müssen Sie möglicherweise **SQL Server 2012 Native Client** ([aus dem SQL Server 2012 Feature Pack](https://www.microsoft.com/download/details.aspx?id=29065)) auf dem Verwaltungspunktserver installieren. Dadurch werden SQL-Verbindungsfehler verhindert (die in der Datei **mp_getauth.log** auf dem Verwaltungspunktserver protokolliert werden).  

### <a name="try-it-out"></a>Probieren Sie es aus!  
Versuchen Sie, die folgende Aufgabe auszuführen, und verwenden Sie dann die Feedbackinformationen oben in diesem Thema, um uns Ihre Erfahrungen mitzuteilen:  

-   Ich kann einen primären Standort installieren, der einen für SQL AlwaysOn-Verfügbarkeitsgruppen konfigurierten Datenbankserver verwendet.  

-   Ich konnte ein Failover meiner SQL AlwaysOn-Verfügbarkeitsgruppe auf ein neues Replikat in der Gruppe ausführen, und der primäre Standort ist immer noch betriebsbereit.  

### <a name="configuring-sql-server-alwayson-for-configuration-manager"></a>Konfigurieren von SQL Server AlwaysOn für Configuration Manager  
 Verwenden Sie die folgenden Verfahren, um zuerst die Verfügbarkeitsgruppe zu erstellen und zu konfigurieren, und installieren Sie dann einen neuen Configuration Manager-Standort, der die Verfügbarkeitsgruppe verwendet.  

#### <a name="to-create-a-sql-server-alwayson-availability-group"></a>So erstellen Sie eine SQL Server AlwaysOn-Verfügbarkeitsgruppe  
Das Verfahren zum [Erstellen einer SQL Server-Verfügbarkeitsgruppe](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server?view=sql-server-ver15) wird in der SQL Server-Dokumentationsbibliothek beschrieben.  Wenn Sie eine Verfügbarkeitsgruppe erstellen, vergewissern Sie sich, dass die folgenden Anforderungen für die Verwendung mit Configuration Manager erfüllt sind:  

-   Maximal drei Mitglieder:  

    -   Ein primäres Replikat und bis zu zwei sekundäre Replikate  

    -   Sekundäre Replikate müssen synchron sein.  

        > [!TIP]  
        >  Es wird empfohlen, dass sekundäre Replikate als schreibgeschützt konfiguriert werden. Dadurch können Sie ein sekundäres Replikat für Funktionen wie Berichterstellung verwenden ohne die Leistung des primären Replikats für Standortvorgänge zu beeinträchtigen.  

-   Mindestens ein Endpunkt. Der virtuelle Name dieses Endpunkts wird bei der Installation des Configuration Manager-Standorts verwendet.  

    > [!TIP]  
    >  Die Gruppe kann zwar mehrere Endpunkte enthalten, Configuration Manager kann aber nur einen Endpunkt nutzen.  

#### <a name="to-install-a-configuration-manager-site-that-uses-the-availability-group"></a>So installieren Sie einen Configuration Manager-Standort, der die Verfügbarkeitsgruppe verwendet  
So installieren Sie einen Standort, der eine SQL Server-Verfügbarkeitsgruppe verwendet:  

1.  Ersetzen Sie Folgendes, wenn Sie vom Configuration Manager-Setup dazu aufgefordert werden:  

    -   **SQL Server-Name:** Geben Sie den virtuellen Namen für den Endpunkt ein, den Sie beim Erstellen der Verfügbarkeitsgruppe konfiguriert haben. Der virtuelle Name sollte ein vollständiger DNS-Name sein, wie z.B. **&lt;Endpunktserver\>.fabrikam.com**.  

    -   **Instanz:**  Dieser Wert sollte leer bleiben. In dieser Konfiguration ist keine Instanz vorhanden.  

    -   **Datenbank:** Geben Sie den Namen der Datenbank ein, die Sie im primären Replikat der Verfügbarkeitsgruppe erstellt haben.  

2.  Als Nächstes müssen Sie einen Speicherort im Netzwerk angeben, auf den jede SQL Server-Instanz in der Gruppe zugreifen kann.  

    -   Das Computerkonto und das Dienstkonto jeder SQL Server-Instanz benötigen den Vollzugriff auf diesen Speicherort.  

    -   Dieser Speicherort wird nur während des Setups verwendet. Nachdem das Setup abgeschlossen und der Standort installiert ist, kann die Freigabe des Speicherorts entfernt oder der Speicherort gelöscht werden.  

3.  Nachdem Sie diese Informationen bereitgestellt haben, schließen Sie das Setup mit der üblichen Vorgehensweise und den normalen Konfigurationen ab.  

##  <a name="service-a--server-cluster"></a><a name="BKMK_ClusterServerUpdates"></a> Wartung eines Serverclusters  
Sie können jetzt eine Sammlung mit Servern in einem Cluster erstellen und anschließend die Clustereinstellungen konfigurieren, die beim Bereitstellen von Updates für den Cluster verwendet werden. Sie können den Prozentsatz der Server steuern, die zu jedem beliebigen Zeitpunkt online sind, und Sie können PowerShell-Skripts mit den vor und nach der Bereitstellung auszuführenden benutzerdefinierten Aktionen konfigurieren.  

**Bekannte Probleme in diesem Release:**  

-   Es ist keine Berichterstellung zur Überprüfung des Status der Bereitstellung von Softwareupdates für Clusterserver verfügbar.  

-   Die Wartungssequenzoption auf der Seite **Clustereinstellungen** ist deaktiviert und in dieser Version nicht verfügbar.  

### <a name="try-it-out"></a>Probieren Sie es aus!  
Versuchen Sie, die folgende Aufgabe auszuführen, und verwenden Sie dann die Feedbackinformationen oben in diesem Thema, um uns Ihre Erfahrungen mitzuteilen:  

-   Ich kann eine Sammlung erstellen, die einen Cluster von Servern darstellt. Für diesen Test können Sie Ihre Sammlungsmitgliedschaftsregeln  für zwei Computer in dieser Sammlung konfigurieren.  

-   Ich kann festlegen, dass zu jedem Zeitpunkt des Clusterbetriebs nur 50 % der Server im Cluster offline sein dürfen. Verwenden Sie die Beispielskripts in der Prozedur, um die Skripts für die vor und nach der Bereitstellung auszuführenden Aktionen festzulegen.  

-   Stellen Sie ein Update für diese Sammlung bereit. Überprüfen Sie die in den Dateien "start.txt" und "end.txt" in "C:\temp" angegebenen Start- und Endzeiten für die Bereitstellung auf den Servern im Cluster. In der Protokolldatei "UpdatesDeployment.log" finden Sie weitere Informationen.  

#### <a name="to-create-a-collection-for-a-server-cluster"></a>So erstellen Sie eine Sammlung für einen Servercluster  

1.  [Erstellen Sie eine Gerätesammlung](../clients/manage/collections/create-collections.md), die die Server im Cluster enthält.  

2.  Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Gerätesammlungen**, klicken Sie mit der rechten Maustaste auf die Sammlung mit den Servern im Cluster, und klicken Sie dann auf **Eigenschaften**.  

3.  Wählen Sie auf der Registerkarte **Allgemein** die Option **All devices are part of the same server cluster** (Alle Geräte sind Teil des gleichen Serverclusters) aus, und klicken Sie dann auf **Einstellungen**.  

4.  Wählen Sie auf der Seite **Clustereinstellungen** aus, wie viel Prozent der Server zum Installieren von Softwareupdates gleichzeitig offline geschaltet werden dürfen. Unabhängig von dem hier angegebenen Prozentwert darf immer nur ein Clusterserver offline geschaltet werden. Bei der Auswahl der Anzahl der Server, die gleichzeitig gewartet werden, wird von Configuration Manager abgerundet. Wenn Sie beispielsweise 51 % auswählen, und im Cluster 4 Server vorhanden sind, werden gleichzeitig 2 Server offline geschaltet.  

5.  Geben Sie an, ob ein Skript vor der Bereitstellung (Knoten sperren) oder ein Skript nach der Bereitstellung (Knoten fortsetzen) verwendet werden soll.  

    > [!TIP]  
    >  Die folgenden Beispiele können Sie beim Testen für Skripts vor und nach der Bereitstellung verwenden, die die aktuelle Uhrzeit in eine Textdatei schreiben:  
    >   
    >  **Vor der Bereitstellung**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\start.txt`  
    >   
    >  **Nach der Bereitstellung**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\end.txt`  

#### <a name="to-deploy-software-updates-to-the-server-cluster"></a>So stellen Sie Softwareupdates für den Servercluster bereit  

1.  [Stellen Sie Softwareupdates](../../sum/deploy-use/deploy-software-updates.md) für die Serverclustersammlung bereit.  

2.  [Überwachen Sie die Softwareupdatebereitstellung](../../sum/deploy-use/monitor-software-updates.md).  
