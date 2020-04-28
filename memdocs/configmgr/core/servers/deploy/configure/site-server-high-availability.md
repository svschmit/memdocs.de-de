---
title: Hochverfügbarkeit der Standortserver
titleSuffix: Configuration Manager
description: Konfigurieren der Hochverfügbarkeit für den Configuration Manager-Standortserver durch Hinzufügen eines Standortservers im passiven Modus.
ms.date: 02/07/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6dcef836-c0d1-40af-ad30-cd8d864b09a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 395504f5ccc3635f580bca739f1c4b7273861123
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700898"
---
# <a name="site-server-high-availability-in-configuration-manager"></a>Hochverfügbarkeit der Standortserver in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

<!--1128774-->

In der Vergangenheit konnten Sie für die meisten der Rollen in Configuration Manager Redundanz hinzufügen, indem Sie mehrere Instanzen dieser Rollen in Ihrer Umgebung ausführten. Mit Ausnahme des Standortservers selbst. Hochverfügbarkeit für die Standortserverrolle ist eine auf Configuration Manager basierende Lösung zum Installieren eines weiteren Standortservers im *passiven* Modus. Der zentrale Verwaltungsstandort und untergeordnete primäre Standorte können über einen zusätzlichen Standortserver im passiven Modus verfügen. Der Standortserver im passiven Modus kann entweder lokal oder in der Azure-Cloud vorhanden sein.

Dieses Feature bietet folgende Vorteile:

- Redundanz und Hochverfügbarkeit der Standortserverrolle  
- Einfacherer Wechsel von Hardware oder Betriebssystem des Standortservers  
- Einfacheres Auslagern des Standortservers nach Azure IaaS  

Der Standortserver im passiven Modus ist zusätzlich zu Ihrem primären Standortserver vorhanden, der sich im *aktiven* Modus befindet. Ein Standortserver im passiven Modus ist bei Bedarf sofort einsatzbereit. Schließen Sie diesen zusätzlichen Standortserver im Rahmen Ihres Gesamtentwurfs ein, um den Configuration Manager-Dienst [hochverfügbar](high-availability-options.md) zu machen.  

Ein Standortserver im passiven Modus:

- Verwendet die gleiche Standortdatenbank wie Ihr Standortserver im aktiven Modus
- Schreibt keine Daten in die Standortdatenbank, solange er sich im passiven Modus befindet
- Verwendet dieselbe Inhaltsbibliothek wie Ihr Standortserver im aktiven Modus

Sie müssen den Standortserver im passiven Modus manuell *höher stufen*, damit dieser aktiv wird. Durch diese Aktion wechselt der Standortserver im aktiven Modus in den Standortserver im passiven Modus. Die Standortsystemrollen, die auf dem ursprünglichen Server im aktiven Modus verfügbar sind, bleiben verfügbar, solange auf diesen Computer zugegriffen werden kann. Nur die Standortserverrolle wechselt zwischen aktivem und passivem Modus.

Microsoft Core Services Engineering and Operations haben diese Funktion verwendet, um ihren zentralen Verwaltungsstandort nach Microsoft Azure auszulagern. Weitere Informationen finden Sie im [Microsoft IT Showcase-Artikel](https://www.microsoft.com/itshowcase/Article/Content/1065/Migrating-System-Center-Configuration-Manager-onpremises-infrastructure-to-Microsoft-Azure).

## <a name="prerequisites"></a>Voraussetzungen

- Die Inhaltsbibliothek des Standorts muss sich in einer Remote-Netzwerkfreigabe befinden. Beide Standortserver benötigen Berechtigungen für den Vollzugriff auf die Freigabe und die zugehörigen Inhalte. Weitere Informationen finden Sie unter [Verwalten der Inhaltsbibliothek](../../../plan-design/hierarchy/the-content-library.md#bkmk_remote).<!--1357525-->  

  - Das Computerkonto des Standortservers muss über die Berechtigung **Vollzugriff** für den Netzwerkpfad verfügen, auf den Sie die Inhaltsbibliothek verschieben. Diese Berechtigung gilt sowohl für die Freigabe als auch für das Dateisystem. Auf dem Remotesystem werden keine Komponenten installiert.

  - Der Standardserver darf nicht über die Verteilungspunktrolle verfügen. Der Verteilungspunkt verwendet ebenfalls die Inhaltsbibliothek, und diese Rolle unterstützt keine Remoteinhaltsbibliothek. Nachdem die Inhaltsbibliothek verschoben wurde, können Sie die Verteilungspunktrolle nicht mehr zum Standortserver hinzufügen.  

- Der Standortserver im passiven Modus kann entweder lokal oder in der Azure-Cloud vorhanden sein.  

    > [!NOTE]
    > Ein cloudbasierter Standortserver im passiven Modus verwendet Azure Infrastructure-as-a-Service (IaaS). Weitere Informationen finden Sie in den folgenden Artikeln:
    >
    >   - [Virtuelle Azure-Computer (für cloudbasierte Infrastruktur)](../../../understand/use-cloud-services.md#azure-virtual-machines-for-cloud-based-infrastructure)
    >   - [Häufig gestellte Fragen zu Configuration Manager in Azure](../../../understand/configuration-manager-on-azure.md)  

- Beide Standortserver müssen derselben Active Directory-Domäne angehören.  

- Configuration Manager unterstützt Standortserver im passiven Modus in einer Hierarchie. Der zentrale Verwaltungsstandort und untergeordnete primäre Standorte können über einen zusätzlichen Standortserver im passiven Modus verfügen.<!-- 3607755 -->  

- Beide Standortserver müssen dieselbe Standortdatenbank verwenden.  

  - Die Datenbank kann remote von beiden Standortservern installiert sein. Ab Version 1810 blockiert der Einrichtungsprozess für Configuration Manager nicht mehr die Installation der Standortserverrolle auf einem Computer mit der Windows-Rolle für Failoverclustering. SQL Always On erfordert diese Rolle, daher konnten Sie die Standortdatenbank auf dem Standortserver bisher nicht gleichzeitig installieren. Mit dieser Änderung haben Sie die Möglichkeit, eine hochverfügbare Website mit weniger Servern zu erstellen, indem Sie SQL Always On und einen Standortserver im passiven Modus verwenden.<!-- SCCMDocs issue 1074 -->  

  - Die SQL Server-Instanz, die die Standortdatenbank hostet, kann eine Standardinstanz, eine benannte Instanz, einen [SQL Server-Cluster](use-a-sql-server-cluster-for-the-site-database.md) oder eine [SQL Server Always On-Verfügbarkeitsgruppe](sql-server-alwayson-for-a-highly-available-site-database.md) verwenden.  

  - Für beide Standortserver ist die Sicherheitsrolle **sysadmin** für die Instanz von SQL Server erforderlich, auf der die Standortdatenbank gehostet ist. Der ursprüngliche Standortserver sollte bereits über diese Rollen verfügen, fügen Sie sie also dem neuen Standortserver hinzu. Beispielsweise fügt das folgende SQL-Skript diese Rollen dem neuen Standortserver **VM2** in der Contoso-Domäne hinzu:  

    ```SQL
    USE [master]
    GO
    CREATE LOGIN [contoso\vm2$] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[us_english]
    GO
    ALTER SERVER ROLE [sysadmin] ADD MEMBER [contoso\vm2$]
    GO
    ```

  - Beide Standortserver benötigen Zugriff auf die Standortdatenbank auf der Instanz von SQL Server. Der ursprüngliche Standortserver sollte bereits über diesen Zugriff verfügen, fügen Sie ihn also dem neuen Standortserver hinzu. Beispielsweise fügt das folgende SQL-Skript der **CM_ABC**-Datenbank eine Anmeldung für den neuen Standortserver **VM2** in der Contoso-Domäne hinzu:  

    ```SQL
    USE [CM_ABC]
    GO
    CREATE USER [contoso\vm2$] FOR LOGIN [contoso\vm2$] WITH DEFAULT_SCHEMA=[dbo]
    GO
    ```

  - Der Standortserver im passiven Modus ist für die Verwendung der gleichen Standortdatenbank wie der Standortserver im aktiven Modus konfiguriert. Der Standortserver im passiven Modus liest nur aus der Datenbank. Er schreibt erst dann etwas in die Datenbank, nachdem er in den aktiven Modus höher gestuft wurde.  

- Der Standortserver im passiven Modus:  

  - Muss die Voraussetzungen für die Installation eines primären Standorts erfüllen. Beispielsweise .NET Framework, Remotedifferenzialkomprimierung und das Windows-ADK. Die vollständige Liste finden Sie unter [Site and site system prerequisites](../../../plan-design/configs/site-and-site-system-prerequisites.md) (Standort- und Standortsystemanforderungen).<!-- SCCMDocs issue 765 -->  

    > [!NOTE]
    > Stellen Sie sicher, dass Sie den SQL Server Native Client installieren. Wenn dieser nicht installiert wird, meldet die Voraussetzungsprüfung beim Configuration Manager-Setup einen Fehler über fehlende SQL Server-Berechtigungen.<!-- SCCMDocs#2290 -->

  - Das zugehörige Computerkonto muss sich in den lokalen Administratorgruppen auf dem Standortserver im aktiven Modus befinden.<!--516036-->

  - Muss mit Quelldateien installiert werden, deren Version der des Standortservers im aktiven Modus entspricht.  

  - Darf vor der Installation des Standortservers im passiven Modus keine Standortsystemrolle gleich welchen Standorts aufweisen.  

- Beide Standortserver können unterschiedliche Betriebssystem- oder Service Pack-Versionen ausführen, solange beide [von Configuration Manager unterstützt](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md) werden.  

- Hosten Sie nicht die Rolle „Dienstverbindungspunkt“ auf einem der für Hochverfügbarkeit konfigurierten Standortserver. Wenn sie sich aktuell auf dem ursprünglichen Standortserver befindet, entfernen Sie sie, und installieren Sie sie auf einem anderen Standortsystemserver. Weitere Informationen finden Sie unter [About the service connection point (Informationen zum Dienstverbindungspunkt)](about-the-service-connection-point.md).  

- Berechtigungen für das [Standortsystem-Installationskonto](../../../plan-design/hierarchy/accounts.md#site-system-installation-account)  

  - Standardmäßig verwenden viele Kunden das Computerkonto des Standortservers, um neue Standortsysteme zu installieren. In dem Fall besteht die Anforderung, das Computerkonto des Standortservers der lokalen Gruppe **Administratoren** auf dem Remotestandortsystem hinzuzufügen. Wenn Ihre Umgebung diese Konfiguration verwendet, achten Sie darauf, das Computerkonto des neuen Standortservers auf allen Remotestandortsystem zu dieser lokalen Gruppe hinzuzufügen. Beispielsweise alle Remoteverteilungspunkte.  

  - Bei der sichereren und empfohlenen Konfiguration wird jedoch ein Dienstkonto für die Installation des Standortsystems verwendet. Die sicherste Konfiguration verwendet ein lokales Dienstkonto. Wenn Ihre Umgebung diese Konfiguration verwendet, ist keine Änderung erforderlich.  

## <a name="limitations"></a>Einschränkungen

- An jedem Standort wird nur ein einzelner Standortserver im passiven Modus unterstützt.  

- Ein Standortserver im passiven Modus wird an einem sekundären Standort nicht unterstützt.<!--SCCMDocs issue 680-->  

    > [!NOTE]  
    > Sekundäre Standorte unter einem primären Standort mit hoch verfügbaren Standortservern werden weiterhin unterstützt.

- Das Höherstufen des Standortservers im passiven Modus in den aktiven Modus erfolgt manuell. Es findet kein automatisches Failover statt.  

- Standortsystemrollen können erst dann auf dem neuen Server installiert werden, wenn Sie den Standortserver im passiven Modus hinzugefügt haben.  

    > [!NOTE]
    > Nachdem der Standortserver im passiven Modus installiert wurde, können Sie nach Bedarf weitere Rollen hinzufügen. Beispiel: Ein Verwaltungspunkt an einem primären Standort.

- Bei Rollen wie dem Berichterstattungspunkt, die eine Datenbank verwenden, müssen Sie die Datenbank auf einem Server hosten, der für beide Standortserver Remoteserver ist.  

- Die Configuration Manager-Konsole führt die Installation auf dem Standortserver im passiven Modus nicht automatisch durch.  

## <a name="add-a-site-server-in-passive-mode"></a>Hinzufügen eines Standortservers im passiven Modus

Weitere Informationen zum allgemeinen Prozess des Hinzufügens von Rollen finden Sie unter [Installieren von Standortsystemrollen](install-site-system-roles.md).

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, wählen Sie den Knoten **Standorte** aus, und klicken Sie im Menüband auf **Standortsystemserver erstellen**.

2. Geben Sie auf der Seite **Allgemein** des Assistenten zum Erstellen von Standortsystemservern den Server an, auf dem der Standortserver im passiven Modus gehostet werden soll. Der von Ihnen angegebene Server kann Standortsystemrollen erst hosten, nachdem ein Standortserver im passiven Modus installiert wurde.  

3. Wählen Sie auf der Seite **Systemrollenauswahl** nur **Standortserver im passiven Modus** aus.  

    > [!NOTE]  
    > Der Assistent führt die folgenden Anfangsüberprüfungen der Voraussetzungen auf dieser Seite durch:
    >
    > - Bei dem ausgewählten Server handelt es sich nicht um einen sekundären Standortserver
    > - Der ausgewählte Server ist noch kein Standortserver im passiven Modus
    > - Die Inhaltsbibliothek des Standorts befindet sich an einem Remotespeicherort  
    >  
    > Wenn diese Anfangsüberprüfungen der Voraussetzungen fehlschlagen, können Sie nicht mit dem Assistenten fortfahren.  

4. Geben Sie auf der Seite **Standortserver im passiven Modus** die folgenden Informationen an, die zur Ausführung des Setups und zur Installation der Standortserverrolle auf dem angegebenen Server verwendet werden:

     - Wählen Sie eine der folgenden Optionen aus:  

         - **Installationsquelldateien über das Netzwerk vom Standortserver im aktiven Modus kopieren:** Diese Option erstellt ein komprimiertes Paket und sendet es zum neuen Standortserver.  

         - **Die Quelldateien am folgenden Speicherort auf dem Standortserver im passiven Modus verwenden:** Dies ist z.B. ein lokaler Pfad, zu dem Sie die Quelldateien bereits kopiert haben. Stellen Sie sicher, dass diese Inhalte die gleiche Version aufweisen wie der Standortserver im aktiven Modus.  

         - (*Empfohlen:* ) **Quelldateien von folgendem Netzwerkort verwenden:** Geben Sie den direkten Pfad für die Inhalte des Ordners **CD.Latest** auf dem Standortserver im aktiven Modus an. Beispiel: `\\Server\SMS_ABC\CD.Latest`; dabei steht *Server* für den Namen des Standortservers im aktiven Modus und *ABC* für den Standortcode.  

     - Geben Sie den lokalen Pfad an, an dem Configuration Manager auf dem neuen Standortserver installiert werden soll. Beispiel: `C:\Program Files\Configuration Manager`  

5. Schließen Sie den Assistenten ab. Configuration Manager installiert dann den Standortserver im passiven Modus auf dem angegebenen Server.

Wechseln Sie in der Konsole zu **Überwachung**, und wählen Sie den Knoten **Standortserverstatus** aus, um den ausführlichen Installationsstatus anzuzeigen. Der Status des Standortservers im passiven Modus wird als **Wird installiert** angezeigt. Wählen Sie den Server aus, und klicken Sie auf **Status anzeigen**, um ausführlichere Informationen zu erhalten. Durch diese Aktion wird das Fenster „Installationsstatus des Standortservers“ geöffnet. Wenn der Prozess abgeschlossen ist, wird bei beiden Servern der Status **OK** angezeigt.

Weitere Informationen zum Setupvorgang finden Sie unter [Flussdiagramm – Einrichten eines Standortservers im passiven Modus](passive-site-server-flowchart.md).

Nachdem Sie einen Standortserver im passiven Modus hinzugefügt haben, werden auf der Registerkarte **Knoten** im Knoten **Standorte** der Konsole beide Standortserver angezeigt.

Sämtliche Komponenten des Configuration Manager-Standortservers sind auf dem Standortserver im passiven Modus betriebsbereit. Die Windows-Dienste werden weiterhin ausgeführt.

## <a name="site-server-promotion"></a>Höherstufung des Standortservers  

Auf ähnliche Weise wie bei der Sicherung und Wiederherstellung können Sie Ihren Prozess zum Ändern von Standortservern planen und üben. Beachten Sie bei Ihrem Plan zur Höherstufung die folgenden Punkte:  

- Üben Sie eine geplante Höherstufung, bei der beide Standortserver online sind. Darüber hinaus sollten Sie ein ungeplantes Failover üben, indem Sie das Trennen der Verbindung zum Standortserver im aktiven Modus oder das Herunterfahren dieses Servers erzwingen.  

- Ermitteln Sie Ihre betrieblichen Prozesse während des Failovers und was mit anderen Configuration Manager-Administratoren kommuniziert werden soll.  

- Gehen Sie vor einer geplanten Höherstufung wie folgt vor:  

  - Überprüfen Sie den Gesamtstatus des Standorts und der Standortkomponenten. Stellen Sie sicher, dass Ihre Umgebung wie gewohnt fehlerfrei ist.  

  - Überprüfen Sie den Inhaltsstatus der Pakete, die zwischen Standorten aktiv repliziert werden.  

  - Überprüfen Sie den Status und die Standortreplikation des sekundären Standorts.

  - Beginnen Sie keine neuen Aufträge zur Inhaltsverteilung oder Wartung auf untergeordneten Servern oder Servern des sekundären Standorts.

    > [!NOTE]
    > Wenn während des Failovers die Datei- oder Datenbankreplikation zwischen Standorten verarbeitet wird, empfängt der neue Standortserver die replizierten Inhalte möglicherweise nicht. In diesem Fall werden Softwareinhalte neu verteilt, nachdem der neue Standortserver aktiviert wurde.<!--515436--> Für die Datenbankreplikation müssen Sie einen zweiten Standort nach dem Failover möglicherweise wieder initialisieren.<!-- SCCMDocs issue 808 -->

  - Reduzieren oder entfernen Sie gleichzeitig andere geplante Aktivitäten. Planen Sie z. B. kein Höherstufen des Standortservers, wenn er direkt zuvor auf eine neuere Version aktualisiert wurde. Bei Standortupdates laufen andere Tasks ab, die mit der Höherstufung des Standortservers in Konflikt stehen können.

    > [!TIP]
    > Im Folgenden finden Sie ein Beispiel dafür, wie andere Aktivitäten mit der Höherstufung des Standortservers in Konflikt stehen können:
    >
    > - Montag: Aktualisieren Sie den Standortserver auf die neueste Version. Aktivieren Sie das automatische Clientupgrade mit Pilottests für Clients.
    > - Dienstag: Stufen Sie den Standortserver vom passiven Modus höher in den aktiven Modus.
    >
    > Bis Mittwoch oder Donnerstag werden aufgrund dieser Aktion möglicherweise *alle* Clients aktualisiert, nicht nur die Pilotsammlung. Dieses Verhalten kann zu erheblicher Netzwerkauslastung und unerwarteter Last auf den Verteilungspunkten führen.<!-- SCCMDocs-pr#4794 -->

### <a name="process-to-promote-the-site-server-in-passive-mode-to-active-mode"></a>Prozess zur Höherstufung des Standortservers aus dem passiven in den aktiven Modus

In diesem Abschnitt wird beschrieben, wie der Standortserver im passiven Modus in den Standortserver im aktiven Modus geändert wird. Wenn Sie auf den Standort zugreifen und diese Änderungen vornehmen möchten, müssen Sie auf eine Instanz des SMS-Anbieters zugreifen können. Weitere Informationen finden Sie unter [Verwenden mehrerer SMS-Anbieter](../../../plan-design/hierarchy/plan-for-the-sms-provider.md#BKMK_MultiSMSProv).  

> [!IMPORTANT]  
> Wenn alle Instanzen des SMS-Anbieters offline sind, können Sie keine Verbindung mit der Website herstellen, da kein Anbieter verfügbar ist. Wenn Sie den Standortserver im passiven Modus hinzufügen, installiert Setup eine Instanz des SMS-Anbieters auf diesem Server.<!-- SCCMDocs#1613 -->
>
> Die Configuration Manager-Konsole fordert die Liste der verfügbaren SMS-Anbieter von WMI auf dem Standortserver an. Wenn an einem Standort mehrere SMS-Anbieter installiert werden, erfolgt die Zuweisung jeder neuen Verbindungszuweisung an diesem Standort zur Verwendung eines installierten SMS-Anbieters nach dem Zufallsprinzip. Es ist nicht möglich, den Speicherort eines SMS-Anbieters zur Verwendung für eine bestimmte Sitzungsverbindung anzugeben. Wenn Ihre Konsole keine Verbindung mit dem Standort herstellen kann, da der aktuelle Standortserver offline ist, müssen Sie im Fenster „Standortverbindung“ den anderen Standortserver angeben.  

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie den Knoten **Standorte** aus. Wählen Sie den Standort aus, und wechseln Sie anschließend zur Registerkarte **Knoten**. Wählen Sie den Standortserver im passiven Modus aus, und klicken Sie anschließend im Menüband auf **In den aktiven Modus höher stufen**. Klicken Sie zum Bestätigen und Fortfahren auf **Ja**.
  
2. Aktualisieren Sie den Konsolenknoten. Der Spalte **Status** des Servers, den Sie höher stufen, wird auf der Registerkarte **Knoten** als **Wird höher gestuft** angezeigt.  

3. Nach Abschluss der Höherstufung wird in der Spalte **Status** für sowohl den neuen Standortserver im aktiven Modus als auch für den neuen Standortserver im passiven Modus **OK** angezeigt. In der Spalte **Servername** des Standorts wird jetzt der Name des neuen Standortservers im aktiven Modus angezeigt.

Wechseln Sie für einen detaillierten Status zum Arbeitsbereich **Überwachung**, und wählen Sie den Knoten **Site Servicing Status** (Wartungsstatus des Standorts) aus. Die Spalte **Modus** gibt an, welcher Server *Aktiv* oder *Passiv* ist. Wählen Sie beim Höherstufen eines Servers aus dem passiven in den aktiven Modus den Standortserver aus, den Sie auf aktiv höher stufen, und klicken Sie anschließend im Menüband auf **Status anzeigen**. Durch diese Aktion wird das Fenster „Status zum Höherstufen des Standortservers“ mit zusätzlichen Details zum Prozess angezeigt.

Wenn ein Standortserver im aktiven Modus in den passiven Modus wechselt, ändert sich nur die Standortsystemrolle in passiv. Alle anderen Standortsystemrollen, die auf diesem Computer installiert sind, bleiben aktiv, sodass Clients weiter Zugriff darauf haben.

Weitere Informationen zur *geplanten* Höherstufung finden Sie unter [Flussdiagramm – Höherstufen des Standortservers (geplant)](promote-site-server-flowchart.md).

### <a name="unplanned-failover"></a>Ungeplantes Failover

Wenn der aktuelle Standortserver im aktiven Modus offline ist, versucht der Standortserver für die Höherstufung 30 Minuten lang, den aktuellen Standortserver im aktiven Modus zu kontaktieren. Wenn der Offlineserver vor Ablauf dieser 30 Minuten wieder erreichbar ist, war die Benachrichtigung erfolgreich, und die Änderung wird ordnungsgemäß fortgesetzt. Andernfalls erzwingt der Standortserver für die Höherstufung eine Aktualisierung der Standortkonfiguration, damit dieser aktiv ist. Wenn der Offlineserver nach dieser Zeit wieder erreichbar ist, wird zunächst der aktuelle Status in der Standortdatenbank überprüft. Anschließend fährt er damit fort, sich selbst auf den Standortserver im passiven Modus tiefer zu stufen.

In dieser dreißigminütigen Wartezeit verfügt der Standort über keinen Standortserver im aktiven Modus. Clients kommunizieren weiterhin mit Rollen mit Clientkontakt, wie z.B. Verwaltungspunkten, Softwareupdatepunkten und Verteilungspunkten. Benutzer können Software installieren, die bereits bereitgestellt wurde. In diesem Zeitraum ist keine Standortverwaltung möglich. Weitere Informationen finden Sie unter [Auswirkungen von Standortausfällen](../../manage/site-failure-impacts.md).  

Löschen Sie diesen Standortserver von der Konsole, wenn der Offlineserver so beschädigt wurde, dass keine Umstellung mehr möglich ist. Erstellen Sie anschließend einen neuen Standortserver im passiven Modus, um einen hochverfügbaren Dienst wiederherzustellen.

Weitere Informationen zum *ungeplanten* Failoverprozess finden Sie unter [Flussdiagramm – Höherstufen des Standortservers (ungeplant)](promote-site-server-unplanned-flowchart.md).

### <a name="additional-tasks-after-site-server-promotion"></a>Zusätzliche Tasks nach der Höherstufung des Standortservers  

Nach dem Wechsel der Standortserver muss der Großteil der weiteren Tasks nicht ausgeführt werden, die für die [Wiederherstellung eines Standorts](../../manage/recover-sites.md#post-recovery-tasks) erforderlich sind. Sie müssen beispielsweise keine Kennwörter zurücksetzen oder erneut eine Verbindung mit Ihrem Microsoft Intune-Abonnement herstellen.

In Ihrer Umgebung müssen möglicherweise die folgenden Schritte ausgeführt werden:  

- Wenn Sie PKI-Zertifikate für Verteilungspunkte importieren, importieren Sie das Zertifikat für betroffene Server erneut. Weitere Informationen finden Sie unter [Erneutes Generieren der Zertifikate für Verteilungspunkte](../../manage/recover-sites.md#regenerate-the-certificates-for-distribution-points).  

- Wenn Sie Configuration Manager in den Microsoft Store für Unternehmen integrieren, konfigurieren Sie diese Verbindung erneut. Weitere Informationen finden Sie unter [Verwalten von Apps aus dem Microsoft Store für Unternehmen](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).  

## <a name="daily-monitoring"></a>Tägliche Überwachung

Wenn Sie über einen Standortserver im passiven Modus verfügen, sollten Sie diesen täglich überwachen. Stellen Sie sicher, dass der Status weiterhin „OK“ lautet und dass der Server betriebsbereit ist. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Überwachung**, und wählen Sie den Knoten **Standortserverstatus** aus. Zeigen Sie beide Standortserver und den zugehörigen aktuellen Status an. Zeigen Sie auch den Status im Arbeitsbereich **Verwaltung** an. Erweitern Sie **Standortkonfiguration**, und klicken Sie auf den Knoten **Standorte**. Wählen Sie den Standort aus, und wechseln Sie anschließend zur Registerkarte **Knoten**.

> [!NOTE]
> Wenn Sie den Standort auf eine neue Version von Configuration Manager aktualisieren, wird auch der Standortserver im passiven Modus aktualisiert. <!-- SCCMDocs-pr#4293 -->