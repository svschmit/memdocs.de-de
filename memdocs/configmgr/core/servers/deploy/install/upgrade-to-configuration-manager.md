---
title: Upgraden auf Current Branch
titleSuffix: Configuration Manager
description: Erfahren Sie die Schritte für die Ausführung eines direkten Upgrades an einem Standort und einer Hierarchie, wo System Center 2012 Configuration Manager ausgeführt wird.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c64e7483-b4bb-4738-95f4-ecdaeb6a2ba6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a2a803a62f2b42c3b62a09e710a3ca74110a4257
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700408"
---
# <a name="upgrade-to-configuration-manager-current-branch"></a>Upgraden auf Current Branch für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Führen Sie ein direktes Upgrade auf Configuration Manager (Current Branch) von einem Standort und einer Hierarchie aus, wo System Center 2012 Configuration Manager ausgeführt wird. Vor dem Upgrade von System Center 2012 Configuration Manager müssen Sie die Standorte vorbereiten. Bei dieser Vorbereitung müssen Sie bestimmte Konfigurationen entfernen, die ein erfolgreiches Upgrade verhindern können. Folgen Sie dann der Upgradesequenz, wenn mehr als ein einzelner Standort beteiligt ist.  

> [!TIP]  
> Beim Verwalten des Configuration Manager-Standorts und der Hierarchieinfrastruktur werden die Begriffe *Upgrade*, *Update* und *Installation* verwendet, um drei verschiedene Konzepte zu beschreiben. Erfahren Sie mehr über die Verwendung der Begriffe unter [Informationen zu Upgrade, Update und Installation für einen Standort und eine Hierarchieinfrastruktur](../../../understand/upgrade-update-install.md).

## <a name="in-place-upgrade-paths"></a><a name="bkmk_path"></a> Pfade für ein direktes Upgrade  

Die folgenden Optionen werden in Pfaden für ein direktes Upgrade derzeit unterstützt:

### <a name="upgrade-to-version-2002"></a>Upgrade auf Version 2002

Sie können die folgenden Produkte auf eine *vollständig lizenzierte* Version von Configuration Manager (Current Branch), Version 2002 aktualisieren:

- Eine *Evaluierungsinstallation* von Configuration Manager (Current Branch), Version 2002
- System Center 2012 Configuration Manager mit Service Pack 1
- System Center 2012 Configuration Manager mit Service Pack 2
- System Center 2012 R2 Configuration Manager
- System Center 2012 R2 Configuration Manager mit Service Pack 1

Weitere Informationen finden Sie unter [Frequently asked questions for Configuration Manager branches and licensing (Häufig gestellte Fragen zu Configuration Manager-Branches und -Lizenzierungen)](../../../understand/product-and-licensing-faq.md).

> [!TIP]  
> Wenn Sie das Upgrade für eine Version von System Center 2012 Configuration Manager auf Current Branch ausführen, können Sie den Upgradeprozess unter Umständen vereinfachen. Weitere Informationen finden Sie unter:  
>
> - [Baseline- und Updateversionen](../../manage/updates.md#bkmk_Baselines)  
> - [Der Ordner „CD.Latest“](../../manage/the-cd.latest-folder.md)  

### <a name="unsupported-paths"></a>Nicht unterstützte Pfade

Die folgenden Pfade werden nicht unterstützt:

- Das Upgrade eines Technical Preview-Branch auf eine vollständig lizenzierte Installation wird nicht unterstützt. Eine Technical Preview-Version kann nur auf eine neuere Version der Technical Preview aktualisiert werden.  

- Die Migration von einer Technical Preview auf eine vollständig lizenzierte Version wird nicht unterstützt.  

## <a name="upgrade-checklists"></a><a name="bkmk_checklist"></a> Checklisten zu Aktualisierungen  

Die folgenden Checklisten können Ihnen bei der Planung eines erfolgreichen Upgrades auf System Center Configuration Manager helfen.  

### <a name="before-you-upgrade"></a>Vor dem Upgrade  

Überprüfen Sie diese Schritte, bevor Sie auf Configuration Manager aktualisieren.

#### <a name="review-your-system-center-2012-configuration-manager-environment"></a>Überprüfen Ihrer System Center 2012 Configuration Manager-Umgebung

Beheben Sie Probleme, die im folgenden Microsoft Support-Artikel beschrieben werden: [Konfigurations-Manager-Clients werden, aufgrund eines wiederkehrenden Wiederholungstasks, alle fünf Stunden neu installiert. Dies kann zu einem unbeabsichtigten Clientupgrade führen](https://support.microsoft.com/help/4018655).

#### <a name="make-sure-your-environment-meets-the-supported-configurations"></a>Sicherstellen, dass Ihre Umgebung den unterstützten Konfigurationen entspricht

- Überprüfen Sie die zum Hosten der Standortsystemrollen verwendeten Serverbetriebssysteme:  

  - Einige von System Center 2012 Configuration Manager unterstützte ältere Betriebssystemversionen werden von Configuration Manager (Current Branch) nicht unterstützt. Entfernen Sie vor dem Upgrade Standortsystemrollen für diese Betriebssystemversionen. Weitere Informationen finden Sie unter [Unterstützte Betriebssysteme für Standortsystemserver](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md).

  - Mit der Voraussetzungsprüfung für Configuration Manager werden die Voraussetzungen für Standortsystemrollen auf dem Standortserver oder auf Remotestandortsystemen nicht geprüft.  

- Überprüfen Sie die Voraussetzungen für jeden Computer, auf dem eine Standortsystemrolle gehostet wird. Zum Bereitstellen eines Betriebssystems verwendet Configuration Manager z.B. das Windows 10 Assessment and Deployment Kit (Windows ADK). Vor dem Ausführen von Setup müssen Sie Windows 10 ADK herunterladen und auf dem Standortserver sowie auf jedem Computer installieren, auf dem eine Instanz des SMS-Anbieters ausgeführt wird.  

Weitere Informationen zu unterstützten Plattformen und die Konfiguration von Voraussetzungen finden Sie unter [Unterstützte Konfigurationen](../../../plan-design/configs/supported-configurations.md).  

Weitere Informationen zur Verwendung des Windows ADK mit Configuration Manager finden Sie unter [Anforderungen an die Infrastruktur für die Betriebssystembereitstellung](../../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

#### <a name="review-the-site-and-hierarchy-status-and-verify-that-there-are-no-unresolved-issues"></a>Überprüfen des Standort- und Hierarchiestatus, damit keine ungelösten Probleme vorliegen

Bevor Sie das Upgrade für einen Standort durchführen, sollten Sie alle Betriebsprobleme beheben, die den Standortserver, den Standortdatenbankserver und die auf Remotecomputern installierten Standortsystemrollen betreffen. Betriebsprobleme können die Ursache für Fehler beim Upgrade von Standorten sein.  

#### <a name="install-all-applicable-critical-updates-for-operating-systems-on-computers-that-host-the-site-the-site-database-server-and-remote-site-system-roles"></a>Installieren aller anwendbaren wichtigen Updates für Betriebssysteme auf den Computern, auf denen der Standort, der Standortdatenbankserver und die Remotestandortsystemrollen gehostet werden

Bevor Sie das Upgrade für einen Standort durchführen, sollten Sie für jedes relevante Standortsystem sämtliche wichtigen Updates installieren. Wenn für ein von Ihnen installiertes Update ein Neustart erforderlich ist, starten Sie die jeweiligen Computer neu, bevor Sie mit dem Service Pack-Update beginnen.  

#### <a name="uninstall-the-site-system-roles-not-supported-by-configuration-manager"></a>Deinstallieren der Standortsystemrollen, die von Configuration Manager nicht unterstützt werden

Die folgenden Standortsystemrollen werden in Configuration Manager nicht mehr verwendet. Deinstallieren Sie sie, bevor Sie auf System Center 2012 Configuration Manager aktualisieren:  

- Out-of-Band-Verwaltungspunkt  

- Systemintegritätsprüfungspunkt  

- Anwendungskatalog-Websitepunkt und Webdienstpunkt

#### <a name="disable-database-replicas-for-management-points-at-primary-sites"></a>Deaktivieren von Datenbankreplikaten für Verwaltungspunkte an primären Standorten

Configuration Manager kann kein Upgrade eines primären Standorts durchführen, auf dem es ein Datenbankreplikat für Verwaltungspunkte gibt. Deaktivieren Sie die Datenbankreplikation, bevor Sie folgende Schritte ausführen:  

- Erstellen einer Sicherung der Standortdatenbank zum Testen des Datenbankupgrades  

- Upgrade des Produktionsstandorts auf Configuration Manager (Current Branch)  

Weitere Informationen finden Sie in den folgenden Artikeln:  

- System Center 2012 Configuration Manager: [Konfigurieren von Datenbankreplikaten für Verwaltungspunkte](../configure/database-replicas-for-management-points.md#BKMK_DBReplica_Config)  

- Configuration Manager, Current Branch: [Datenbankreplikate für Verwaltungspunkte](../configure/database-replicas-for-management-points.md)  

#### <a name="reconfigure-software-update-points-that-use-nlb"></a>Erneutes Konfigurieren von Softwareupdatepunkten, die NLBs verwenden

Configuration Manager kann kein Upgrade für Standorte durchführen, an denen Softwareupdatepunkte mithilfe eines NLB-Clusters gehostet werden.  

Wenn Sie für Softwareupdatepunkte NLB-Cluster verwenden, entfernen Sie den NLB-Cluster mithilfe von PowerShell. (Ab System Center 2012 Configuration Manager SP1 gab es in der Configuration Manager-Konsole keine Option zum Konfigurieren von NLB-Cluster)  

#### <a name="disable-all-site-maintenance-tasks-at-each-site-for-the-duration-of-that-sites-upgrade"></a>Deaktivieren aller Standortwartungsaufgaben an allen Standorten für die Dauer des Standortupgrades

Bevor Sie ein Upgrade auf Configuration Manager durchführen, deaktivieren Sie alle Standortwartungstasks, die möglicherweise zu dem Zeitpunkt ausgeführt werden, zu dem der Upgradeprozess aktiv ist. Diese Liste enthält u.a. die folgenden Tasks:  

- Standortserver sichern  
- Veraltete Clientvorgänge löschen  
- Veraltete Ermittlungsdaten löschen  

Wenn während des Upgradeprozesses ein Wartungstask für die Standortdatenbank ausgeführt wird, tritt beim Standortupgrade möglicherweise ein Fehler auf.  

Zeichnen Sie den Zeitplan eines Tasks vor dem Deaktivieren auf, sodass Sie die Konfiguration nach Abschluss des Standortupgrades wiederherstellen können.

Weitere Informationen zu Standortwartungstasks finden Sie in den folgenden Artikeln:  

- System Center 2012 Configuration Manager: [Planen von Standortvorgängen](../../../plan-design/hierarchy/plan-for-the-site-database.md)  

- Configuration Manager, Current Branch: [Referenz für Wartungstasks](../../manage/reference-for-maintenance-tasks.md)  

#### <a name="run-setup-prerequisite-checker"></a>Ausführen der Setup-Voraussetzungsprüfung

Führen Sie vor dem Upgrade eines Standorts die **Voraussetzungsprüfung** unabhängig von Setup aus, um zu prüfen, ob Ihr Standort die Voraussetzungen erfüllt. Beim späteren Durchführen des Upgrades wird die Voraussetzungsprüfung nochmal ausgeführt.  

Die unabhängige Voraussetzungsprüfung überprüft die Website nach Upgrades für die Current Branch-Version und die Long-Term Servicing Branch-Version (LTSB) von Configuration Manager. Da einige Funktionen von der LTSB-Version nicht unterstützt werden, werden im Protokoll **ConfigMgrPrereq.log** möglicherweise Einträge wie in den folgenden Beispielen angezeigt:

- `INFO: The site is a LTSB edition.`
- `Unsupported site system role 'Asset Intelligence synchronization point' for the LTSB edition;    Error;    Configuration Manager has detected that the 'Asset Intelligence synchronization point' is installed. Asset Intelligence is not supported on the LTSB edition. You must uninstall the Asset Intelligence synchronization point site system role before you can continue.`

Wenn Sie ein Upgrade auf die Current Branch-Version planen, können Fehler für die LTSB-Edition einfach ignoriert werden. Sie sind nur dann relevant, wenn Sie ein Upgrade auf die LTSB-Edition planen.

Wenn Sie später Configuration Manager Setup zur Erledigung des Upgrades ausführen, wird die Voraussetzungsprüfung nochmal ausgeführt. Sie wertet Ihren Standort anhand der Branch-Version von Configuration Manager aus, die Sie zum Installieren gewählt haben (Current Branch oder LTSB). Wenn Sie sich für ein Upgrade auf die Current Branch-Version entscheiden, wird die Prüfung auf Features, die von der LTSB-Edition nicht unterstützt werden, nicht ausgeführt.

Weitere Informationen finden Sie unter [Voraussetzungsprüfung](prerequisite-checker.md) und in der [Liste der Voraussetzungsprüfungen](list-of-prerequisite-checks.md).  

#### <a name="download-prerequisite-files-and-redistributable-files-for-configuration-manager"></a>Herunterladen von erforderlichen und weitervertreibbaren Dateien für Configuration Manager

Verwenden Sie das **Setup-Downloadprogramm**, um die erforderlichen weitervertreibbaren Dateien, die Sprachpakete und die neuesten Produktupdates für Configuration Manager herunterzuladen.  

Informationen hierzu finden Sie unter [Setup-Downloadprogramm für System Center Configuration Manager](setup-downloader.md).  

#### <a name="plan-to-manage-server-and-client-languages"></a>Planen Sie die Verwaltung von Server- und Clientsprachen ein.

Beim Aktualisieren eines Standorts werden nur die Sprachpaketversionen installiert, die Sie während des Upgrades auswählen.  

- Setup überprüft die aktuelle Sprachkonfiguration Ihres Standorts. Anschließend ermittelt es, welche Sprachpakete in dem Ordner verfügbar sind, in dem die zuvor heruntergeladenen erforderlichen Dateien gespeichert wurden.  

- Sie können die Auswahl der aktuellen Server- und Clientsprachpakete bestätigen oder ändern oder aber die Unterstützung von Sprachen hinzufügen oder entfernen.  

- Nur Sprachpakete, die bei der Ausführung von Setup verfügbar sind, können ausgewählt werden.  

> [!NOTE]  
> Sie können die Sprachpakete aus System Center 2012 Configuration Manager nicht verwenden, um Sprachen für einen System Center Configuration Manager-Standort zu aktivieren.  

Weitere Informationen zu Sprachpaketen finden Sie unter [Sprachpakete](language-packs.md).  

#### <a name="review-considerations-for-site-upgrades"></a>Sehen Sie sich die Überlegungen zum Upgrade von Standorten an.

Wenn Sie ein Upgrade für einen Standort durchführen, werden einige Funktionen und Konfigurationen auf die Standardkonfiguration zurückgesetzt. Informationen zur Vorbereitung auf diese und ähnliche Änderungen finden Sie unter [Upgradeüberlegungen](#bkmk_considerations).  

#### <a name="create-a-backup-of-the-site-database-at-the-central-administration-site-and-primary-sites"></a>Erstellen einer Sicherung der Standortdatenbank am Standort der zentralen Verwaltung und an primären Standorten

Bevor Sie das Upgrade für einen Standort durchführen, sollten Sie die Standortdatenbank sichern, damit Sie über eine Sicherung für die Notfallwiederherstellung verfügen.  

Weitere Informationen finden Sie unter [Sicherung und Wiederherstellung](../../manage/backup-and-recovery.md).  

#### <a name="back-up-a-customized-configurationmof-file"></a>Erstellen einer Sicherung der benutzerdefinierten Datei „configuration.mof“

Wenn Sie eine benutzerdefinierte Datei „configuration.mof“ verwenden, um die bei der Hardwareinventur verwendeten Datenklassen zu definieren, erstellen Sie eine Sicherung dieser Datei. Nach dem Upgrade stellen Sie diese Datei an ihrem Standort wieder her. Weitere Informationen finden Sie unter [Vorgehensweise: Erweitern der Hardwareinventur](../../../clients/manage/inventory/extend-hardware-inventory.md).  

#### <a name="test-the-database-upgrade-process-on-a-copy-of-the-most-recent-site-database-backup"></a>Testen des Datenbank-Upgradeprozesses mit einer Kopie der letzten Sicherung der Standortdatenbank

Bevor Sie das Upgrade für einen Standort der zentralen Verwaltung oder einen primären Standort von Configuration Manager durchführen, testen Sie den Datenbankupgradeprozess mit einer Kopie der letzten Sicherung der Standortdatenbank.  

- Testen Sie den Datenbank-Upgradeprozess für den Standort. Beim Upgrade eines Standorts wird die Standortdatenbank möglicherweise geändert.  

- Ein Testen des Datenbankupgrades ist zwar nicht erforderlich, doch können dadurch Probleme beim Upgrade ermittelt werden, bevor die Produktionsdatenbank betroffen ist.  

- Wenn beim Upgrade einer Standortdatenbank Fehler auftreten, ist die Datenbank möglicherweise nicht mehr betriebsfähig, und es müsste eine Standortwiederherstellung erfolgen.  

- Obwohl die Standortdatenbank von allen Standorten in einer Hierarchie gemeinsam genutzt wird, sollten Sie die Datenbank an jedem relevanten Standort testen, bevor Sie das Upgrade für diesen Standort durchführen.  

- Wenn Sie an einem primären Standort Datenbankreplikate für Verwaltungspunkte verwenden, deaktivieren Sie die Replikation, bevor Sie die Sicherung der Standortdatenbank erstellen.  

Configuration Manager unterstützt weder die Sicherung sekundärer Standorte noch das Testupgrade einer sekundären Standortdatenbank.  

Das Testen des Datenbankupgrades für die Datenbank des Produktionsstandorts wird nicht unterstützt. Dadurch würde ein Upgrade der Standortdatenbank durchgeführt, und Ihr Standort wäre möglicherweise nicht mehr betriebsfähig.  

Weitere Informationen finden Sie unter [Testen des Standortdatenbankupgrades](#bkmk_test).  

#### <a name="restart-the-site-server-and-each-computer-that-hosts-a-site-system-role"></a>Erneutes Starten des Standortservers und aller Computer, auf denen eine Standortsystemrolle gehostet wird

Führen Sie diese Aktion aus, um sicherzustellen, dass es keine ausstehenden Aktionen aus einer kürzlichen Installation von Updates oder aus Voraussetzungen gibt.  

#### <a name="upgrade-sites"></a>Aktualisieren Sie Standorte.

Beginnen Sie mit dem Standort der obersten Ebene in der Hierarchie, und führen Sie „Setup.exe“ aus dem Quellmedium von Configuration Manager aus.  

Wenn das Upgrade am Standort der obersten Ebene abgeschlossen ist, können Sie mit dem Upgrade der untergeordneten Standorte beginnen. Schließen Sie jeweils das Upgrade eines Standorts ab, bevor Sie das Upgrade des nächsten Standorts durchführen.  

Bis das Upgrade auf Configuration Manager für alle Standorte in der Hierarchie durchgeführt wurde, erfolgt der Betrieb im gemischten Versionsmodus.  

Informationen zum Ausführen des Upgrades finden Sie unter [Aktualisieren Sie Standorte](#bkmk_upgrade).  

### <a name="after-you-upgrade"></a>Nach dem Upgrade  

Überprüfen Sie diese Schritte, nachdem Sie auf Configuration Manager aktualisiert haben.

#### <a name="upgrade-stand-alone-configuration-manager-consoles"></a>Upgrade der eigenständigen Configuration Manager-Konsolen

Standardmäßig wird beim Upgrade eines Standorts der zentralen Verwaltung oder eines primären Standorts auch für eine auf dem Standortserver installierte Configuration Manager-Konsole ein Upgrade durchgeführt. Führen Sie für jede Konsole, die auf einem anderen Computer als dem Standortserver installiert ist, ein manuelles Upgrade durch.  

> [!TIP]  
> Schließen Sie vor dem Starten des Upgrades jede geöffnete Konsole.  

Weitere Informationen finden Sie unter [Installieren von Configuration Manager-Konsolen](install-consoles.md).  

#### <a name="reconfigure-database-replicas-for-management-points-at-primary-sites"></a>Neukonfigurieren von Datenbankreplikaten für Verwaltungspunkte an primären Standorten

Beim Verwenden von Datenbankreplikaten für Verwaltungspunkte an primären Standorten müssen Sie die Datenbankreplikate deinstallieren, bevor Sie den Standort aktualisieren. Konfigurieren Sie das Datenbankreplikat für Verwaltungspunkte nach dem Upgrade eines primären Standorts neu.

Weitere Informationen finden Sie unter [Datenbankreplikate für Verwaltungspunkte](../configure/database-replicas-for-management-points.md).  

#### <a name="reconfigure-any-database-maintenance-tasks-you-disabled-before-the-upgrade"></a>Erneutes Konfigurieren von Datenbankwartungsaufgaben, die Sie vor dem Upgrade deaktiviert haben

Wenn Sie [Datenbankwartungstasks](../../manage/reference-for-maintenance-tasks.md) vor dem Upgrade an einem Standort deaktiviert haben, konfigurieren Sie diese Tasks am Standort mithilfe der vor dem Upgrade verwendeten Einstellungen neu.  

#### <a name="upgrade-clients"></a>Aktualisieren Sie Clients.

Nach der Aktualisierung aller Standorte auf Configuration Manager planen Sie das Upgraden von Clients.  

Wenn Sie ein Upgrade für einen Client ausführen, wird die aktuelle Clientsoftware deinstalliert und die neue Version der Clientsoftware installiert. Für Upgrades von Clients können Sie ein beliebiges Verfahren verwenden, das von Configuration Manager unterstützt wird.  

> [!TIP]  
> Wenn Sie für den Standort der obersten Ebene einer Hierarchie ein Upgrade durchführen, wird das Clientinstallationspaket auf den einzelnen Verteilungspunkten der Hierarchie ebenfalls aktualisiert. Beim Upgrade eines primären Standorts wird das Clientupgradepaket aktualisiert, das vom primären Standort zur Verfügung gestellt wird.  

Weitere Informationen finden Sie unter [Aktualisieren von Clients für Windows-Computer](../../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

## <a name="considerations-for-upgrading"></a><a name="bkmk_considerations"></a> Upgradeüberlegungen  

### <a name="automatic-actions"></a>Automatische Aktionen

Wenn Sie ein Upgrade auf Configuration Manager durchführen, werden die folgenden Aktionen automatisch ausgeführt:  

- Zurücksetzen des Standorts. Diese Aktion umfasst eine Neuinstallation aller Standortsystemrollen.  

- Wenn es sich bei dem Standort um den Standort der obersten Ebene einer Hierarchie handelt, wird das Clientinstallationspaket auf allen Verteilungspunkten der Hierarchie aktualisiert. Vom Standort werden auch die Standardstartabbilder aktualisiert, sodass die neue Windows PE-Version verwendet wird, die in Windows Assessment and Deployment Kit 10 enthalten ist. Beim Durchführen des Upgrades werden vorhandene Medien jedoch nicht für die Verwendung mit der Abbildbereitstellung aktualisiert.  

- Wenn es sich bei dem Standort um einen primären Standort handelt, wird das Clientupgradepaket für den Standort aktualisiert.  

### <a name="manual-actions-after-an-upgrade"></a>Manuelle Aktionen nach einem Upgrade

Nachdem Sie ein Upgrade für einen Standort durchgeführt haben, müssen Sie sicherstellen, dass die folgenden Aktionen ausgeführt werden:  

- Stellen Sie sicher, dass auf Clients, die den einzelnen primären Standorten zugewiesen sind, das Upgrade durchgeführt und die neue Clientversion installiert wird.  

- Führen Sie ein Upgrade für jede Configuration Manager-Konsole aus, die eine Verbindung zum Standort herstellt und auf einem Computer ausgeführt wird, der sich gegenüber dem Standortserver an einem Remotestandort befindet.  

- Konfigurieren Sie die Datenbankreplikate an den primären Standorten neu, an denen Sie Datenbankreplikate für Verwaltungspunkte verwenden.  

- Führen Sie nach den Standortupgrades das Upgrade von physischen Medien wie ISO-Dateien für CDs, DVDs oder USB-Speichersticks manuell durch. Dazu gehören auch vorab bereitgestellte Medien für Hardwareanbieter. Obwohl durch das Standortupgrade die Standardstartabbilder aktualisiert werden, werden diese von Configuration Manager extern verwendeten Mediendateien oder Geräte nicht aktualisiert.  

- Planen Sie die Aktualisierung von benutzerdefinierten Startabbildern ein, wenn die ursprüngliche (ältere) Version von Windows PE nicht erforderlich ist.  

### <a name="actions-that-affect-configurations-and-settings"></a>Aktionen, die sich auf Konfigurationen und Einstellungen auswirken

Wenn für einen Standort ein Upgrade auf Configuration Manager durchgeführt wird, werden einige Konfigurationen und Einstellungen nach dem Upgrade nicht beibehalten. Einige Konfigurationen werden auf einen neuen Standard festgelegt. Die folgende Liste enthält einige Einstellungen, die nicht beibehalten werden oder die sich ändern:  

- **Softwarecenter**  
    Die folgenden Elemente des Softwarecenters werden auf ihre Standardwerte zurückgesetzt:  

  - Die Option**Arbeitsinformationen** wird auf die Geschäftszeiten **5:00 Uhr** bis **22:00 Uhr** Montag bis Freitag zurückgesetzt.  

  - Der Wert für **Computerwartung** wird auf **Softwarecenter-Aktivitäten anhalten, wenn sich der Computer im Präsentationsmodus befindet**festgelegt.  

  - Der Wert für **Remotesteuerung** wird auf den Wert in den Clienteinstellungen festgelegt, die dem Computer zugewiesen sind.  

- **Zeitpläne für Softwareupdate-Zusammenfassung**: Benutzerdefinierte Zusammenfassungszeitpläne für Softwareupdates oder Softwareupdategruppen werden auf den Standardwert von einer Stunde zurückgesetzt. Setzen Sie benutzerdefinierte Zusammenfassungswerte nach Abschluss des Upgrades auf die erforderliche Häufigkeit zurück.  

## <a name="test-the-site-database-upgrade"></a><a name="bkmk_test"></a> Testen des Standortdatenbankupgrades  

Die folgenden Informationen gelten nur, wenn Sie eine vorherige Version wie System Center 2012 Configuration Manager auf System Center Configuration Manager (Current Branch) aktualisieren.

Bevor Sie das Upgrade eines Standorts durchführen, sollten Sie es anhand einer Kopie der Datenbank dieses Standorts testen.  

Zum Testen der Datenbank für ein Upgrade stellen Sie zunächst eine Kopie der Standortdatenbank auf einer Instanz von SQL Server wieder her, von der kein Configuration Manager-Standort gehostet wird. Zum Hosten der Datenbankkopie müssen Sie eine Version von SQL Server verwenden, die von Configuration Manager unterstützt wird.  

Führen Sie nach dem Wiederherstellen der Standortdatenbank auf dem SQL Server-Computer das Configuration Manager-Setup aus dem Ordner auf dem Quellmedium für Configuration Manager aus. Verwenden Sie dazu die Befehlszeilenoption `/TESTDBUPGRADE`.  

Weitere Informationen finden Sie in den folgenden Artikeln:

- [Sichern eines Configuration Manager-Standorts](../../manage/backup-and-recovery.md)  

- [Befehlszeilenoptionen für Setup](command-line-options-for-setup.md#bkmk_setup)  

- [Unterstützung für SQL Server-Versionen](../../../plan-design/configs/support-for-sql-server-versions.md)  

> [!TIP]  
> Wenn Sie Microsoft Intune mit Configuration Manager integrieren:  
>
> Wenn Sie ein Testdatenbankupgrade für eine Kopie der Standortdatenbank ausführen, die mindestens 5 Tage alt ist, wird möglicherweise eine der folgenden Meldungen angezeigt:  
>
> - WARN: Upgrade will force full sync to cloud. (WARNUNG: Upgrade erzwingt eine vollständige Synchronisierung mit der Cloud.)  
> - FEHLER: Database upgrade will force full sync to cloud. (FEHLER: Datenbankupgrade erzwingt eine vollständige Synchronisierung mit der Cloud.)  
>
> Beide können während des Testens eines Datenbankupgrades problemlos ignoriert werden. Sie weisen nicht auf einen Fehler oder ein Problem mit dem Testupgrade hin. Stattdessen zeigen sie an, dass während des tatsächlichen Upgrades Daten aus der Datenbankreplikationsgruppe **Cloud** möglicherweise mit Microsoft Intune synchronisiert werden.  

### <a name="test-a-site-database-for-upgrade"></a>Testen einer Standortdatenbank für ein Upgrade  

Führen Sie für alle Standorte der zentralen Verwaltung sowie für alle primären Standorte, für die ein Upgrade geplant ist, folgende Schritte aus:  

1. Erstellen Sie eine Kopie der Standortdatenbank. Stellen Sie diese Kopie dann auf einer Instanz von SQL Server wieder her, deren Edition der von der Standortdatenbank verwendeten entspricht und von der kein Configuration Manager-Standort gehostet wird. Wird auf der Standortdatenbank beispielsweise eine Instanz der Enterprise Edition von SQL Server ausgeführt, muss die Datenbank auf einer Instanz von SQL Server wiederhergestellt werden, auf der ebenfalls die Enterprise Edition von SQL Server ausgeführt wird.  

2. Führen Sie nach der Wiederherstellung der Datenbankkopie Setup vom Quellmedium für Configuration Manager (Current Branch) aus. Verwenden Sie beim Ausführen von Setup die Befehlszeilenoption `/TESTDBUPGRADE`. Wenn es sich bei der SQL Server-Instanz, von der die Datenbankkopie gehostet wird, nicht um die Standardinstanz handelt, geben Sie auch die Befehlszeilenargumente an. Damit können Sie ermitteln, von welcher Instanz die Kopie der Standortdatenbank gehostet wird.  

    Angenommen, Sie planen das Upgrade einer Standortdatenbank namens „SMS_ABC“. Sie stellen eine Kopie dieser Standortdatenbank auf einer unterstützten Instanz von SQL Server wieder her, die Sie „DBTest“ genannt haben. Verwenden Sie folgende Befehlszeile, um ein Upgrade dieser Kopie der Standortdatenbank zu testen: `Setup.exe /TESTDBUPGRADE DBtest\CM_ABC`.  

    „Setup.exe“ ist an folgendem Speicherort auf dem Configuration Manager-Quellmedium zu finden: `SMSSETUP\BIN\X64`  

3. Überprüfen Sie den Fortschritt und den Erfolg des Upgrades auf der Instanz von SQL Server, auf der Sie den Test ausführen. Die nötigen Angaben dazu finden Sie in der Datei ConfigMgrSetup.log im Stamm des Systemlaufwerks:  

    - Wenn beim Testen des Upgrades ein Fehler auftritt, beheben Sie alle Probleme im Zusammenhang mit diesem Fehler beim Upgrade der Standortdatenbank. Erstellen Sie anschließend eine neue Sicherung der Standortdatenbank, und testen Sie das Upgrade der neuen Datenbankkopie.  

    - Wenn der Prozess erfolgreich abgeschlossen ist, können Sie die Datenbankkopie löschen.  

        > [!NOTE]  
        > Eine Wiederherstellung der für den Upgradetest verwendeten Standortdatenbankkopie, um sie an einem beliebigen Standort als Standortdatenbank zu verwenden, wird nicht unterstützt.  

Nachdem Sie für eine Kopie der Standortdatenbank ein Upgrade erfolgreich durchgeführt haben, setzen Sie das Upgrade des Configuration Manager-Standorts und von dessen Standortdatenbank fort.  

## <a name="upgrade-sites"></a><a name="bkmk_upgrade"></a> Aktualisieren Sie Standorte.  

Sie können das Upgrade Ihres Configuration Manager-Standorts durchführen, nachdem Sie die folgenden Aufgaben abgeschlossen haben:

- Konfigurationen vor dem Upgrade für Ihren Standort
- Testen des Upgrades der Standortdatenbank an einer Datenbankkopie
- Herunterladen der erforderlichen Dateien und Sprachpakete für die Version, die Sie installieren möchten

Beim Durchführen eines Upgrades für einen Standort in einer Hierarchie führen Sie als Erstes ein Upgrade für den Standort der obersten Ebene der Hierarchie durch. Bei dem Standort der obersten Ebene handelt es sich entweder um einen Standort der zentralen Verwaltung oder um einen eigenständigen primären Standort. Nachdem Sie das Upgrade für einen Standort der zentralen Verwaltung abgeschlossen haben, können Sie Upgrades für die untergeordneten primären Standorte in beliebiger Reihenfolge durchführen. Nach dem Durchführen eines Upgrades für einen primären Standort können Sie für dessen untergeordnete sekundäre Standorte oder für zusätzliche primäre Standorte ein Upgrade durchführen, bevor Sie sekundäre Standorte aktualisieren.  

Führen Sie Setup über das Configuration Manager-Quellmedium aus, um ein Upgrade für einen Standort der zentralen Verwaltung oder einen primären Standort durchzuführen. Für ein Upgrade sekundärer Standorte führen Sie Setup nicht aus. Stattdessen verwenden Sie die Configuration Manager-Konsole, um das Upgrade eines sekundären Standorts durchzuführen, nachdem das Upgrade des primären übergeordneten Standorts abgeschlossen ist.  

Schließen Sie die Configuration Manager-Konsole auf dem Standortserver, bevor Sie das Upgrade eines Standorts bis zu seinem Abschluss durchführen. Schließen Sie außerdem jede Configuration Manager-Konsole, die auf anderen Computern als dem Standortserver ausgeführt wird. Sie können die Konsole nach Abschluss des Upgrades wieder verbinden. Bis Sie allerdings das Upgrade einer Configuration Manager-Konsole auf die neue Configuration Manager-Version durchführen, können in dieser Konsole nicht alle Objekte und Informationen angezeigt werden, die in der neuen Configuration Manager-Version verfügbar sind.  

### <a name="upgrade-a-central-administration-site-or-primary-site"></a>Durchführen eines Upgrades für einen Standort der zentralen Verwaltung oder einen primären Standort  

1. Überprüfen Sie, ob der Benutzer, der Setup ausführt, über die folgenden Sicherheitsrechte verfügt:  

    - Lokale **Administrator**rechte auf dem Standortserver  

    - Falls der Standortdatenbankserver im Hinblick auf den Standortserver remote ist, darauf lokale **Administrator**rechte  

2. Öffnen Sie auf dem Standortserver folgendes Programm: `<ConfigMgSourceMedia>\SMSSETUP\BIN\X64\Setup.exe`. Mit dieser Aktion wird der Setup-Assistent für Configuration Manager wird geöffnet.  

3. Lesen Sie die Informationen auf der Seite **Vorbemerkungen**, und wählen Sie **Weiter** aus.  

4. Wählen Sie auf der Seite **Erste Schritte** die Option **Upgrade dieser Configuration Manager-Installation ausführen** und dann **Weiter** aus.  

5. Auf der Seite **Product Key**:  

    Wenn Sie zuvor Configuration Manager Evaluation installiert haben, können Sie **Lizenzierte Edition des Produkts installieren** auswählen. Geben Sie dann Ihren Product Key für die Vollversion von Configuration Manager ein. Mit dieser Aktion wird der Standort auf die Vollversion konvertiert.  

    Sie können auch das **Ablaufdatum von Software Assurance** Ihres Lizenzvertrags als praktische Erinnerung an dieses Datum angeben. Wenn Sie diesen Wert nicht während des Setups eingeben, können Sie ihn später in der Configuration Manager-Konsole angeben.  

    > [!NOTE]  
    > Microsoft überprüft das angegebene Ablaufdatum nicht und verwendet es auch nicht, um die Lizenz zu überprüfen. Sie können es als Erinnerung an das Ablaufdatum verwenden. Configuration Manager überprüft regelmäßig, ob neue Softwareupdates online angeboten werden, und Ihr Software Assurance-Lizenzstatus sollte aktuell sein, damit Sie von diesen zusätzlichen Updates profitieren können.

    Weitere Informationen finden Sie unter [Lizenzierung und Branches](../../../understand/learn-more-editions.md).

6. Lesen und akzeptieren Sie auf der Seite **Microsoft Software-Lizenzbedingungen** die Lizenzbedingungen, und wählen Sie anschließend **Weiter**.  

7. Lesen und akzeptieren Sie auf der Seite **Lizenzen für erforderliche Komponenten** die Lizenzbedingungen für die erforderliche Software. Wählen Sie dann **Weiter** aus. Die Software wird gegebenenfalls heruntergeladen und automatisch auf Standortsystemen oder Clients installiert. Bevor Sie mit der nächsten Seite fortfahren können, müssen Sie allen Bedingungen zustimmen.  

8. Geben Sie auf der Seite **Download der Voraussetzungskomponenten** an, ob Setup die neuesten Inhalte aus dem Internet herunterladen oder zuvor heruntergeladene Dateien verwenden soll. Diese Inhalte umfassen die erforderlichen weitervertreibbaren Dateien, die Sprachpakete und die neuesten Produktupdates. Falls Sie bereits Dateien mit dem Setup-Downloadprogramm heruntergeladen haben, wählen Sie **Bereits heruntergeladene Dateien verwenden** aus, und geben Sie den Downloadordner an. Weitere Informationen finden Sie unter [Setup Downloader (Setup-Downloadprogramm)](setup-downloader.md).  

    > [!NOTE]  
    > Wenn Sie bereits heruntergeladene Dateien verwenden, überprüfen Sie, ob der Downloadordner die aktuellsten Dateiversionen enthält.  

9. Zeigen Sie auf der Seite **Serversprachauswahl** die Liste der Sprachen an, die zurzeit für den Standort installiert sind. Wählen Sie zusätzliche Sprachen aus, die an diesem Standort für die Configuration Manager-Konsole und für Berichte verfügbar sind. Sie können Sprachen, die Sie an diesem Standort nicht mehr unterstützen möchten, auch deaktivieren. Englisch ist standardmäßig aktiviert und kann nicht entfernt werden.  

    > [!IMPORTANT]  
    > Keine Version von Configuration Manager kann Sprachpakete aus einer früheren Configuration Manager-Version verwenden. Soll die Unterstützung einer bestimmten Sprache an einem Configuration Manager-Standort aktiviert werden, der upgegradet wird, müssen Sie die Sprachpaketversion für die neue Softwareversion verwenden. Wenn beispielsweise während des Upgrades von System Center 2012 Configuration Manager auf Configuration Manager (Current Branch) die Current Branch-Version eines Sprachpakets unter den erforderlichen Dateien, die Sie herunterladen, nicht verfügbar ist, können Sie die Unterstützung für diese Sprache nicht installieren.  

10. Zeigen Sie auf der Seite **Clientsprachauswahl** die Liste der Sprachen an, die zurzeit für den Standort installiert sind. Wählen Sie weitere Sprachen aus, die an diesem Standort für Clientcomputer verfügbar sind, oder entfernen Sie Sprachen, die an diesem Standort nicht mehr unterstützt werden sollen. Geben Sie an, ob alle Clientsprachen für mobile Geräteclients aktiviert werden sollen. Klicken Sie dann auf **Weiter**. Englisch ist standardmäßig aktiviert und kann nicht entfernt werden.  

11. Überprüfen Sie auf der Seite **Zusammenfassung der Einstellungen** die Konfiguration. Wenn Sie damit fertig sind, wählen Sie **Weiter** aus, um die Voraussetzungsprüfung zu starten und damit zu prüfen, ob der Server für das Upgrade des Standorts bereit ist.  

12. Wählen Sie auf der Seite **Voraussetzungsprüfung** die Option **Weiter** aus, falls keine Probleme aufgeführt werden. Daraufhin wird das Upgrade des Standorts und der Standortsystemrollen durchgeführt.

    Wenn bei der Voraussetzungsprüfung ein Problem festgestellt wird, wählen Sie in der Liste einen Eintrag aus, um Details zur Behebung des Problems anzuzeigen. Sie können mit der Installation erst dann fortfahren, wenn alle in der Liste mit dem Status **Fehler** aufgeführten Elemente korrigiert wurden. Klicken Sie nach der Problembehebung auf **Prüfung ausführen** , um die Voraussetzungsprüfung zu wiederholen. Sie können die Ergebnisse der Voraussetzungsprüfung überprüfen, indem Sie die Datei ConfigMgrPrereq.log im Stamm des Systemlaufwerks öffnen. Die Protokolldatei enthält möglicherweise weitere Informationen, die auf der Benutzeroberfläche nicht angezeigt werden. Eine Liste der Regeln und Beschreibungen zu den Installationsvoraussetzungen finden Sie unter [Voraussetzungsprüfung](list-of-prerequisite-checks.md).

Auf der Seite **Upgrade** wird der Gesamtstatus der Installation angezeigt. Wenn die Hauptinstallation des Standortservers und des Standortsystems abgeschlossen ist, können Sie den Assistenten schließen. Die Standortkonfiguration wird im Hintergrund fortgesetzt.  

### <a name="upgrade-a-secondary-site"></a>Durchführen des Upgrades für einen sekundären Standort  

1. Überprüfen Sie, ob der Administrator, der die Installation ausführt, über die folgenden Sicherheitsrechte verfügt:  

    - Lokale **Administrator**rechte auf dem sekundären Standortserver  

    - Sicherheitsrolle **Infrastrukturadministrator** oder **Hauptadministrator** am übergeordneten primären Standort  

    - Systemadministratorrechte (**SA**) für die Standortdatenbank des sekundären Standorts  

2. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie die Option **Standortkonfiguration**, und klicken Sie dann auf den Knoten **Standorte**.  

3. Wählen Sie den sekundären Standort aus, für den Sie das Upgrade durchführen möchten. Wählen Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Standort** die Option **Upgrade** aus.  

4. Wählen Sie zum Bestätigen **Ja** aus. Daraufhin wird das Upgrade des sekundären Standorts gestartet.  

Das Upgrade des sekundären Standorts erfolgt im Hintergrund. Bestätigen Sie nach Abschluss des Upgrades den Status in der Configuration Manager-Konsole. Wählen Sie den Server des sekundären Standorts und dann auf der Registerkarte **Startseite** des Menübands in der Gruppe **Standort** die Option **Installationsstatus anzeigen** aus.  

## <a name="post-upgrade-tasks"></a><a name="BKMK_PostUpgrade"></a> Aufgaben nach dem Upgrade  

Nachdem Sie für einen Standort ein Upgrade durchgeführt haben, müssen Sie möglicherweise einige zusätzliche Aufgaben ausführen, um das Upgrade oder die Neukonfiguration des Standorts abzuschließen. Diese Aufgaben können Folgendes umfassen:

- Upgrade von Configuration Manager-Clients
- Upgrade von Configuration Manager-Konsolen
- Erneutes Aktivieren von Datenbankreplikaten für Verwaltungspunkte
- Wiederherstellen von Einstellungen für Configuration Manager-Funktionen, die Sie verwenden und die nach dem Upgrade nicht dauerhaft gespeichert werden  
