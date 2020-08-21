---
title: Checkliste für Version 2006
titleSuffix: Configuration Manager
description: In diesem Artikel erhalten Sie Informationen zu Vorbereitungen, die Sie treffen müssen, bevor Sie ein Update auf Version 2006 von Configuration Manager durchführen.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6d359306-69ae-4873-ba90-964b6ae51d79
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7a3c66863e7768c5ca90151bf85d61aa1e3a0e17
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129521"
---
# <a name="checklist-for-installing-update-2006-for-configuration-manager"></a>Checkliste für die Installation von Update 2006 für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Wenn Sie den Current Branch von Configuration Manager verwenden, können Sie das konsoleninterne Update für Version 2006 installieren, um die Hierarchie einer älteren Version zu aktualisieren. <!-- baseline only statement:Version 2006 is also available as [baseline media](updates.md#bkmk_Baselines), so you can use the installation media to install the first site of a new hierarchy.-->

Für das Update auf Version 2006 müssen Sie einen Dienstverbindungspunkt auf der obersten Ebene Ihrer Hierarchie verwenden. Die Standortsystemrolle kann im Online- oder Offlinemodus erfolgen. [Verwenden Sie das Dienstverbindungstool](use-the-service-connection-tool.md), um das Update herunterzuladen, wenn der Dienstverbindungspunkt offline ist.<!-- SCCMDocs#1946 -->

Nachdem in Ihrer Hierarchie das Updatepaket von Microsoft heruntergeladen wurde, ist dieses in der Konsole enthalten. Wählen Sie im Arbeitsbereich **Verwaltung** den Knoten **Updates und Wartung** aus.

- Wenn das Update als **Verfügbar** aufgeführt ist, ist das Update zur Installation bereit. Sehen Sie sich vor der Installation von Version 2006 die folgenden Informationen [zur Installation von Update 2006](#about-installing-update-2006) und die [Checkliste](#checklist) für Konfigurationen an, die vor dem Starten des Updates durchgeführt werden müssen.

- Wenn bei dem Update **Downloadvorgang läuft** angezeigt wird und die Meldung sich nicht ändert, überprüfen Sie **hman.log** und **dmpdownloader.log** auf Fehler.

  - „dmpdownloader.log“ weist möglicherweise darauf hin, dass der dmpdownloader-Prozess auf ein Intervall wartet, bevor die Überprüfung auf Updates durchgeführt wird. Starten Sie den Dienst **SMS_Executive** auf dem Standortserver neu, um den Download der Dateien des Updates zur Umverteilung neu zu starten.

  - Ein weiteres häufiges Downloadproblem tritt auf, wenn Proxyservereinstellungen Downloads von `silverlight.dlservice.microsoft.com`, `download.microsoft.com` und `go.microsoft.com` verhindern.

Weitere Informationen zum Installieren von Updates finden Sie unter [Konsoleninterne Updates und Wartung](updates.md#bkmk_inconsole).

Weitere Informationen zu Current Branch-Versionen finden Sie unter [Baseline- und Updateversionen](updates.md#bkmk_Baselines).

## <a name="about-installing-update-2006"></a>Informationen zur Installation des Updates 2006

### <a name="sites"></a>Standorte

Installieren Sie das Update 2006 am Standort der obersten Ebene Ihrer Hierarchie. Starten Sie die Installation von Ihrem Standort der zentralen Verwaltung oder von Ihrem eigenständigen primären Standort aus. Nach dem Installieren des Updates am Standort der obersten Ebene haben untergeordnete Standorte das folgende Updateverhalten:

- An untergeordneten primären Standorten wird das Update automatisch gestartet, sobald die Installation des Updates am Standort der zentralen Verwaltung abgeschlossen ist. Mithilfe von Dienstfenstern können Sie steuern, wann das Update an einem Standort installiert wird. Weitere Informationen finden Sie unter [Dienstfenster für Standortserver](service-windows.md).

- Aktualisieren Sie jeden sekundären Standort manuell von der Configuration Manager-Konsole aus, nachdem die Updateinstallation am primären übergeordneten Standort abgeschlossen wurde. Das automatische Update sekundärer Standortserver wird nicht unterstützt.

### <a name="site-system-roles"></a>Standortsystemrollen

Wenn ein Standortserver das Update installiert, werden sämtliche Standortsystemrollen automatisch ebenfalls aktualisiert. Diese Rollen befinden sich auf dem Standortserver oder wurden auf Remoteservern installiert. Stellen Sie daher vor der Installation des Updates sicher, dass jeder Standortsystemserver die aktuellen Voraussetzungen für die neue Updateversion erfüllt.

### <a name="configuration-manager-consoles"></a>Configuration Manager-Konsolen

Bei der ersten Verwendung einer Configuration Manager-Konsole nach Abschluss des Updates werden Sie aufgefordert, die Konsole zu aktualisieren. Sie können das Configuration Manager-Setup auch auf dem Computer ausführen, der die Konsole hostet, und die Option zum Aktualisieren der Konsole auswählen. Installieren Sie das Update so schnell wie möglich in der Konsole. Weitere Informationen finden Sie unter [Installieren der Configuration Manager-Konsole](../deploy/install/install-consoles.md).

> [!IMPORTANT]  
> Wenn Sie ein Update am Standort der zentralen Verwaltung installieren, beachten Sie folgende Einschränkungen und Verzögerungen, die bis zum Abschluss der Updateinstallation auf allen untergeordneten primären Standorten auftreten:
>
> - **Clientupgrades** starten nicht. Dazu zählen auch automatische Updates für Clients und Präproduktionsclients. Sie können außerdem keine Präproduktionsclients auf die Produktionsphase höherstufen, bis die Updateinstallation auch am letzten Standort abgeschlossen ist. Wenn die Updateinstallation auch am letzten Standort abgeschlossen ist, werden die Clientupdates basierend auf Ihren Konfigurationen durchgeführt.
> - **Neue Funktionen**, die Sie mit dem Update aktivieren, sind nicht verfügbar. Dieses Verhalten soll verhindern, dass der Standort der zentralen Verwaltung mit dieser Funktion verknüpfte Daten an einen Standort repliziert, der das Feature noch nicht unterstützt. Wenn das Update an allen primären Standorten installiert wurde, können Sie das Feature nutzen.
> - **Replikationslinks** zwischen dem Standort der zentralen Verwaltung und untergeordneten primären Standorten werden als nicht aktualisiert angezeigt. Dieser Status wird im Installationsstatus des Updates als *Mit Warnung abgeschlossen* zum Überwachen der Replikationsinitialisierung angezeigt. Im Arbeitsbereich **Überwachung** der Konsole wird dieser Status als *Link wird konfiguriert* angezeigt.

### <a name="early-update-ring"></a>Early Update Ring

<!-- SCCMDocs#1397 -->

<!-- As of May 11, 2020, version 2006 is globally available for all customers to install. If you previously opted in to the early update ring, watch for an update to this current branch version. -->

Derzeit wird Version 2006 für den Early Update Ring freigegeben. Zum Installieren dieses Updates müssen Sie sich anmelden. Mit dem folgenden PowerShell-Skript wird Ihre Hierarchie oder der eigenständige primäre Standort dem Early Update Ring für Version 2006 hinzugefügt:

[Anmeldeskript für Version 2006](https://go.microsoft.com/fwlink/?linkid=2099733) <!-- This fwlink points to the script package on the Download Center, don't change the link here! Make any changes to the fwlink target -->

Microsoft signiert das Skript digital und bündelt es in einer signierten selbst extrahierenden ausführbaren Datei.

> [!NOTE]
> Das Update der Version 2006 gilt nur für Standorte, an denen mindestens Version 1810 ausgeführt wird.

So melden Sie sich beim Early Update Ring an:

1. Öffnen von Windows PowerShell und **Als Administrator ausführen**
1. Führen Sie das Skript **EnableEarlyUpdateRing2006.ps1** mit der folgenden Syntax aus:

    `EnableEarlyUpdateRing2006.ps1 <SiteServer_Name> | SiteServer_IP>`

    Dabei bezieht sich `SiteServer` auf den Standort der zentralen Verwaltung oder den eigenständigen primären Standortserver. Zum Beispiel, `EnableEarlyUpdateRing2006.ps1 cmprimary01`

1. Suchen nach Updates Weitere Informationen finden Sie unter [Abrufen aller verfügbaren Updates](install-in-console-updates.md#get-available-updates).

Das Update der Version 2006 sollte nun in der Konsole verfügbar sein.

> [!IMPORTANT]
> Mit diesem Skript wird Ihr Standort nur dem Early Update Ring für Version 2006 hinzugefügt. Es handelt sich nicht um eine dauerhafte Änderung.

## <a name="checklist"></a>Prüfliste

### <a name="all-sites-run-a-supported-version-of-configuration-manager"></a>An allen Standorten wird eine unterstützte Configuration Manager-Version ausgeführt.

Auf jedem Standortserver in der Hierarchie muss die gleiche Version von Configuration Manager ausgeführt werden, bevor Sie die Installation des Updates 2006 starten können. Für das Update auf Version 2006 müssen Sie mindestens Version 1810 verwenden.

### <a name="review-the-status-of-your-product-licensing"></a>Überprüfen Sie den Status Ihrer Produktlizenzierung

Sie müssen über einen aktiven SA-Vertrag (Software Assurance) oder entsprechende Abonnierungsrechte für die Installation dieses Updates verfügen. Wenn Sie den Standort aktualisieren, haben Sie auf der Seite **Lizenzierung** die Möglichkeit, Ihr **Software Assurance-Ablaufdatum** zu bestätigen.

Dieser Wert ist optional. Sie können diesen als praktische Erinnerung an das Ablaufdatum Ihrer Lizenz angeben. Dieses Datum ist sichtbar, wenn Sie künftige Updates installieren. Möglicherweise haben Sie diesen Wert zuvor während des Setups oder der Installation eines Updates angegeben. Sie können diesen Wert auch in der Configuration Manager-Konsole angeben. Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Standortkonfiguration**, und wählen Sie **Standorte** aus. Wählen Sie im Menüband **Hierarchieeinstellungen** aus, und wechseln Sie zur Registerkarte **Lizenzierung**.

Weitere Informationen finden Sie unter [Lizenzierung und Branches](../../understand/learn-more-editions.md).

### <a name="review-microsoft-net-versions"></a>Überprüfen der Versionen von Microsoft .NET

Wenn dieses Update an einem Standort installiert wird und die mindestens erforderliche .NET Framework-Version 4.5 nicht vorhanden ist, installiert Configuration Manager automatisch .NET Framework 4.5.2. Wenn diese Voraussetzung nicht bereits installiert ist, wird Sie von dem Standort auf jedem Server installiert, der eine der folgenden Standortsystemrollen hostet:

- Verwaltungspunkt
- Dienstverbindungspunkt
- Anmeldungsproxypunkt
- Anmeldungspunkt

Diese Installation kann den Standortsystemserver in den Zustand „Ausstehender Neustart“ versetzen und Fehler an die Configuration Manager-Komponentenstatusanzeige melden. Darüber hinaus treten bei .NET-Anwendungen auf dem Server gelegentlich Fehler auf, bis Sie den Server neu starten.

Weitere Informationen finden Sie in den [Voraussetzungen für Standorte und Standortsysteme](../../plan-design/configs/site-and-site-system-prerequisites.md).

### <a name="review-the-version-of-the-windows-adk-for-windows-10"></a>Überprüfen der Version des Windows ADK für Windows 10

Die Version des Windows 10 ADK (Assessment and Deployment Kit) sollte für Configuration Manager, Version 2006 unterstützt werden. Weitere Informationen zu unterstützten Windows ADK-Versionen finden Sie unter [Windows 10 ADK](../../plan-design/configs/support-for-windows-10.md#windows-10-adk). Wenn Sie das Windows ADK aktualisieren müssen, sollten Sie dies vor dem Update von Configuration Manager durchführen. Durch diese Reihenfolge wird sichergestellt, dass die Standardstartimages automatisch auf die neueste Version der Windows PE aktualisiert werden. Benutzerdefinierte Startimages müssen nach der Aktualisierung des Standorts manuell aktualisiert werden.

Wenn Sie den Standort vor dem Windows ADK aktualisieren, finden Sie unter [Update distribution points with the boot image (Aktualisieren von Verteilungspunkten mithilfe des Startimages)](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image) weitere Informationen.

### <a name="review-sql-server-native-client-version"></a>Überprüfen der SQL Server Native Client-Version

Installieren Sie eine Mindestversion von SQL Server 2012 Native Client, einschließlich der Unterstützung für TLS 1.2. Weitere Informationen finden Sie unter [Liste der Voraussetzungsprüfungen](../deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

### <a name="review-the-site-and-hierarchy-status-for-unresolved-issues"></a>Überprüfen des Standorts und des Hierarchiestatus auf ungelöste Probleme

Betriebsprobleme können die Ursache für Fehler beim Update von Standorten sein. Beheben Sie alle Betriebsprobleme für die folgenden Systeme, bevor Sie einen Standort aktualisieren:  

- Der Standortserver  
- Den Standortdatenbankserver  
- Remote-Standortsystemrollen auf anderen Servern

Weitere Informationen finden Sie unter [Verwenden von Benachrichtigungen und des Statussystems](use-alerts-and-the-status-system.md).

### <a name="review-file-and-data-replication-between-sites"></a>Überprüfen der Datei- und Datenreplikation zwischen Standorten

Stellen Sie sicher, dass die Datei- und Datenreplikation zwischen Standorten betriebsbereit und aktuell ist. Verzögerungen oder Rückstände können ein erfolgreiches Update verhindern.

#### <a name="database-replication"></a>Datenbankreplikation

Verwenden Sie für die [Datenbankreplikation](../../plan-design/hierarchy/database-replication.md) die **Replikationslinkanalyse** (RLA), um Probleme zu beheben, bevor Sie das Update starten. Weitere Informationen finden Sie unter [Überwachen der Datenbankreplikation](monitor-replication.md).

Beantworten Sie mithilfe von RLA die folgenden Fragen:

- Ist die Replikation pro Gruppe in einem guten Zustand?
- Wurden Verknüpfungen heruntergestuft?
- Liegen Fehler vor?

Wenn ein Rückstand vorhanden ist, warten Sie, bis er abgebaut wurde. Wenn der Rückstand groß ist (d. h. Millionen von Datensätzen), befindet sich der Link in einem ungültigen Zustand. Beheben Sie das Replikationsproblem, bevor Sie den Standort aktualisieren. Wenn Sie weitere Unterstützung benötigen, wenden Sie sich an den Microsoft-Support.<!-- 2838129 -->

#### <a name="file-based-replication"></a>dateibasierte Replikation

Überprüfen Sie für die [dateibasierte Replikation](../../plan-design/hierarchy/file-based-replication.md) alle Postfächer sowohl für sendende als auch für empfangende Standorte auf einen Rückstand. Wenn eine Vielzahl an blockierten oder ausstehenden Replikationsaufträgen vorhanden ist, warten Sie, bis sie abgebaut wurden.<!-- SCCMDocs#1792 -->

- Überprüfen Sie für den sendenden Standort **sender.log**.
- Überprüfen Sie für den empfangenden Standort **despooler.log**.

### <a name="install-all-applicable-critical-windows-updates"></a>Installieren aller anwendbaren wichtigen Updates

Bevor Sie ein Update für Configuration Manager installieren, müssen Sie für die einzelnen anwendbaren Standortsysteme sämtliche wichtigen Betriebssystemupdates installieren. Diese Server umfassen die Rollen des Standortservers, des Standortdatenbankservers und des Remotestandortsystems. Wenn für ein von Ihnen installiertes Update ein Neustart erforderlich ist, starten Sie die jeweiligen Server neu, bevor Sie mit dem Upgrade beginnen.

### <a name="disable-database-replicas-for-management-points-at-primary-sites"></a>Deaktivieren von Datenbankreplikaten für Verwaltungspunkte an primären Standorten

Configuration Manager kann kein Update eines primären Standorts durchführen, wenn dort Datenbankreplikate für Verwaltungspunkte aktiviert sind. Deaktivieren Sie die Datenbankreplikation, bevor Sie ein Update für Configuration Manager installieren.

Weitere Informationen finden Sie unter [Datenbankreplikate für Verwaltungspunkte](../deploy/configure/database-replicas-for-management-points.md).

### <a name="set-sql-server-alwayson-availability-groups-to-manual-failover"></a>Festlegen von SQL Server Always On-Verfügbarkeitsgruppen auf manuelles Failover

Wenn Sie eine Verfügbarkeitsgruppe verwenden, stellen Sie sicher, dass diese auf „Manuelles Failover“ festgelegt ist, bevor Sie mit der Installation des Updates beginnen. Nachdem der Standort aktualisiert wurde, können Sie wieder auf „Automatisches Failover“ umstellen. Weitere Informationen finden Sie unter [SQL Server Always On für Standortdatenbanken](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="disable-site-maintenance-tasks-at-each-site"></a>Deaktivieren von Standortwartungstasks an den einzelnen Standorten

Bevor Sie das Update installieren, deaktivieren Sie alle Standortwartungstasks, die möglicherweise zu dem Zeitpunkt ausgeführt werden, zu dem der Updateprozess aktiv ist. Beispiele hierfür sind:

- Standortserver sichern
- Veraltete Clientvorgänge löschen
- Veraltete Ermittlungsdaten löschen

Wenn ein Standortdatenbank-Wartungstask während der Updateinstallation ausgeführt wird, kann bei der Updateinstallation ein Fehler auftreten. Bevor Sie einen Task deaktivieren, zeichnen Sie den Zeitplan des Tasks auf, sodass Sie die Konfiguration nach Abschluss des Updates wiederherstellen können.

Weitere Informationen finden Sie unter [Wartungstasks](maintenance-tasks.md) und in der [Referenz für Wartungstasks](reference-for-maintenance-tasks.md).

### <a name="temporarily-stop-any-antivirus-software"></a>Vorübergehendes Beenden einer Antivirensoftware

Bevor Sie einen Standort aktualisieren, müssen Sie die Antivirensoftware auf den Configuration Manager-Servern beenden. Die Antivirensoftware kann einige Dateien sperren, die aktualisiert werden müssen. Dies führt bei unserem Update zu einem Fehler. <!--SMS.503481-->

### <a name="create-a-backup-of-the-site-database"></a>Erstellen einer Sicherung der Standortdatenbank

Sichern Sie vor der Aktualisierung eines Standorts die Standortdatenbank am Standort der zentralen Verwaltung und an primären Standorten. Durch diese Sicherung wird sichergestellt, dass Sie über eine erfolgreiche Sicherung verfügen, die bei der Notfallwiederherstellung verwendet werden kann.

Weitere Informationen finden Sie unter [Sicherung und Wiederherstellung](backup-and-recovery.md).

### <a name="back-up-customized-files"></a>Sichern angepasster Dateien

Wenn Sie oder ein Drittanbieterprodukt Configuration Manager-Konfigurationsdateien anpassen, speichern Sie eine Kopie Ihrer Anpassungen.

Fügen Sie beispielsweise der Datei **osdinjection.xml** im `bin\X64`-Ordner Ihres Configuration Manager-Installationsverzeichnisses benutzerdefinierte Einträge hinzu. Nachdem Sie Configuration Manager aktualisiert haben, bleiben diese Anpassungen nicht erhalten. Sie müssen Ihre Anpassungen erneut anwenden.

### <a name="plan-for-client-piloting"></a>Planen von Pilottests für Clients

Wenn Sie ein Standortupdate installieren, bei dem auch der Client aktualisiert wird, prüfen Sie das neue Clientupdate in einer Präproduktionsumgebung, bevor Sie alle Produktionsclients aktualisieren. Um diese Option zu nutzen, konfigurieren Sie Ihren Standort für die Unterstützung automatischer Updates für die Präproduktionsphase, bevor Sie die Installation des Updates starten.

Weitere Informationen finden Sie unter [Aktualisieren von Clients](../../clients/manage/upgrade/upgrade-clients.md) und unter [Testen von Clientupgrades in einer Präproduktionssammlung](../../clients/manage/upgrade/test-client-upgrades.md).

### <a name="plan-to-use-service-windows"></a>Planen der Verwendung von Dienstfenstern

Definieren Sie mithilfe von Dienstfenstern einen Zeitraum, in dem Updates an einem Standortserver installiert werden können. Damit können Sie steuern, wann das Update an Standorten in Ihrer Hierarchie installiert werden kann. Weitere Informationen finden Sie unter [Dienstfenster für Standortserver](service-windows.md).

### <a name="review-supported-extensions"></a>Überprüfen der unterstützten Erweiterungen

<!--SCCMdocs#587-->
Wenn Sie Configuration Manager mit anderen Produkten von Microsoft oder Microsoft-Partnern erweitern, vergewissern Sie sich, dass diese Produkte Version 2006 unterstützen. Wenden Sie sich für diese Informationen an den Hersteller des Produkts. Lesen Sie beispielsweise die [Anmerkungen zu dieser Version von Microsoft Deployment Toolkit](../../../mdt/release-notes.md).

### <a name="remove-intune-subscription-hybrid-mdm"></a>Entfernen eines Intune-Abonnements (Hybrid-MDM)

<!-- SCCMDocs-pr#4253 -->
Das Dienstangebot des Hybrid-MDM wird ab dem 1. September 2019 eingestellt. Wenn Ihr Configuration Manager-Standort über ein Microsoft Intune-Abonnement verfügt, müssen Sie es entfernen. Weitere Informationen finden Sie unter [Entfernen von Hybrid-MDM](../../../mdm/understand/what-happened-to-hybrid.md#remove-hybrid-mdm).

### <a name="run-the-setup-prerequisite-checker"></a>Ausführen der Setup-Voraussetzungsprüfung

Wenn das Update in der Konsole als **Verfügbar** aufgeführt wird, können Sie die Voraussetzungsprüfung ausführen, bevor Sie das Update installieren. (Beim Installieren des Updates am Standort wird die Voraussetzungsprüfung erneut ausgeführt.)

Wechseln Sie zum Arbeitsbereich **Verwaltung**, und klicken Sie auf **Updates und Wartung**, um eine Voraussetzungsprüfung durchzuführen. Wählen Sie das Updatepaket **Configuration Manager 2006** und anschließend im Menüband **Voraussetzungsprüfung ausführen** aus.

Weitere Informationen finden Sie unter **Ausführen der DPM-Voraussetzungsprüfung vor der Installation eines Updates** im Artikel [Vor der Installation eines konsoleninternen Updates](install-in-console-updates.md#bkmk_beforeinstall).

> [!IMPORTANT]  
> Wenn die Voraussetzungsprüfung ausgeführt wird, werden vom Prozess einige Produktquelldateien aktualisiert, die für Standortwartungstasks verwendet werden. Wenn Sie daher nach Durchführung der Voraussetzungsprüfung, aber vor Installation des Updates einen Standortwartungstask durchführen müssen, führen Sie  **Setupwpf.exe** (Configuration Manager-Setup) im Ordner „CD.Latest“ auf dem Standortserver aus.

### <a name="update-sites"></a>Aktualisieren von Standorten

Sie können nun die Updateinstallation für Ihre Hierarchie starten. Weitere Informationen zum Installieren des Updates finden Sie unter [Installieren konsoleninterner Updates](install-in-console-updates.md#bkmk_install).

Möglicherweise sollten Sie das Update außerhalb der normalen Geschäftszeiten installieren. Ermitteln Sie, wann der Prozess Ihre Geschäftsvorgänge am wenigsten beeinträchtigt. Durch die Installation des Updates und der zugehörigen Aktionen werden Standortkomponenten und Standortsystemrollen neu installiert.

Weitere Informationen finden Sie unter [Updates für System Center Configuration Manager](updates.md).

## <a name="post-update-checklist"></a>Checkliste nach dem Update

Nachdem der Standort aktualisiert wurde, verwenden Sie die folgende Checkliste, um allgemeine Aufgaben und Konfigurationen durchzuführen.

### <a name="confirm-version-and-restart-if-necessary"></a>Überprüfen der Version und ggf. Neustart

Stellen Sie sicher, dass jeder Standortserver und jede Standortsystemrolle auf Version 2006 aktualisiert wurde. Fügen Sie in der Konsole im Arbeitsbereich **Verwaltung** die Spalte **Version** zu den Knoten **Standorte** und **Verteilungspunkte** hinzu. Wenn dies nötig ist, wird automatisch erneut eine Standortsystemrolle installiert, um diese auf die neueste Version zu aktualisieren.

Ziehen Sie in Erwägung, Remotestandortsysteme erneut zu starten, die nicht erfolgreich aktualisiert werden konnten. Überprüfen Sie Ihre Standortinfrastruktur, und stellen Sie sicher, dass die relevanten Standortserver und Remote-Standortsystemserver erfolgreich neu gestartet wurden. In der Regel werden Standortserver nur neu gestartet, wenn Configuration Manager .NET als Voraussetzung für eine Standortsystemrolle installiert.

### <a name="confirm-site-to-site-replication-is-active"></a>Bestätigen, dass die Replikation zwischen Standorten aktiv ist

Wechseln Sie in der Configuration Manager-Konsole zu den folgenden Orten, um den Status anzuzeigen und sicherzustellen, dass die Replikation aktiv ist:  

- Arbeitsbereich **Überwachung**, Knoten **Standorthierarchie**  

- Arbeitsbereich **Überwachung**, Knoten **Datenbankreplikation**  

Weitere Informationen finden Sie in den folgenden Artikeln:  

- [Überwachen der Hierarchie- und Replikationsinfrastruktur](monitor-hierarchy.md)
- [Informationen zur Replikationslinkanalyse](monitor-replication.md#BKMK_RLA)  

### <a name="update-configuration-manager-consoles"></a>Aktualisieren von Configuration Manager-Konsolen

Aktualisieren Sie alle remoten Configuration Manager-Konsolen auf die gleiche Version. In folgenden Fällen werden Sie zum Aktualisieren der Konsole aufgefordert:  

- Sie öffnen die Konsole.  

- Wenn Sie in der Konsole zu einem neuen Knoten navigieren.  

### <a name="reconfigure-database-replicas-for-management-points"></a>Neu konfigurieren von Datenbankreplikaten für Verwaltungspunkte

Nachdem Sie einen primären Standort aktualisiert haben, konfigurieren Sie das Datenbankreplikat für Verwaltungspunkte neu, die Sie vor dem Standortupdate deinstalliert haben. Weitere Informationen finden Sie unter [Datenbankreplikate für Verwaltungspunkte](../deploy/configure/database-replicas-for-management-points.md).  

### <a name="reconfigure-sql-server-alwayson-availability-groups"></a>Neukonfigurieren von SQL Server AlwaysOn-Verfügbarkeitsgruppen

Wenn Sie eine Verfügbarkeitsgruppe verwenden, setzen Sie die Failoverkonfiguration auf „Automatisch“ zurück. Weitere Informationen finden Sie unter [SQL Server AlwaysOn für eine hoch verfügbare Standortdatenbank für System Center Configuration Manager](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).<!-- SCCMDocs #1366 -->

### <a name="reconfigure-any-disabled-maintenance-tasks"></a>Neu konfigurieren deaktivierter Wartungstasks

Wenn Sie die [Datenbankwartungstasks](maintenance-tasks.md) vor der Installation des Updates an einem Standort deaktiviert haben, konfigurieren Sie diese Tasks neu. Verwenden Sie dazu die Einstellungen, die schon vor dem Update verwendet wurden.  

### <a name="update-clients"></a>Aktualisieren von Clients

Aktualisieren Sie Clients anhand des von Ihnen erstellten Plans, insbesondere, wenn Sie Pilottests für Clients vor der Installation des Updates konfiguriert haben. Weitere Informationen finden Sie unter [Aktualisieren von Clients für Windows-Computer](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

### <a name="third-party-extensions"></a>Drittanbietererweiterungen

Wenn Sie Erweiterungen für Configuration Manager verwenden, aktualisieren Sie diese auf die neueste Version, damit Version 2006 von Configuration Manager unterstützt wird.

### <a name="update-custom-boot-images-and-media"></a>Aktualisieren von benutzerdefinierten Startimages und Medien

<!--SCCMDocs issue 775-->

Verwenden Sie für Startimages – ganz gleich, ob Standard- oder benutzerdefinierte Startimages – die Aktion **Verteilungspunkte aktualisieren**. Dadurch wird sichergestellt, dass Clients die neueste Version verwenden können. Auch wenn es keine neue Windows ADK-Version gibt, können sich die Configuration Manager-Clientkomponenten durch ein Update ändern. Wenn Sie keine Startimages und Medien aktualisieren, können Tasksequenzbereitstellungen Fehler auf Geräten verursachen.

Wenn Sie den Standort aktualisieren, aktualisiert Configuration Manager automatisch die *standardmäßigen* Startimages. Der aktualisierte Inhalt wird nicht automatisch an Verteilungspunkte verteilt. Verwenden Sie die Aktion **Verteilungspunkte aktualisieren** für bestimmte Startimages, wenn Sie diesen Inhalt in Ihrem Netzwerk verteilen möchten.

Aktualisieren Sie *benutzerdefinierte* Startimages nach der Aktualisierung des Standorts manuell. Hierdurch wird das Startimage bei Bedarf mit den neuesten Clientkomponenten aktualisiert. Optional wird es mit der aktuellen Windows PE-Version erneut geladen, und der Inhalt wird an die Verteilungspunkte verteilt.

Weitere Informationen finden Sie unter [Aktualisieren von Verteilungspunkten mithilfe des Startimages](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image).
