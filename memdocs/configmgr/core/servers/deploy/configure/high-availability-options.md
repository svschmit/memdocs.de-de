---
title: Hohe Verfügbarkeit
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über das Bereitstellen von Configuration Manager mithilfe von Optionen, die die Hochverfügbarkeit eines Diensts gewährleisten.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1a38421d-24c1-4fef-bf6c-42fce53109ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 32083deb30d3d7345ccad8d31541d3c641eb10c0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707268"
---
# <a name="high-availability-options-for-configuration-manager"></a>Hochverfügbarkeitsoptionen für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

In diesem Artikel wird beschrieben, wie Sie Configuration Manager mithilfe von Optionen bereitstellen, die die Hochverfügbarkeit des Diensts gewährleisten.

Die Hochverfügbarkeit wird von den folgenden Configuration Manager-Optionen unterstützt:

- Konfigurieren eigenständiger primärer Standorte mit einem zusätzlichen Standortserver im passiven Modus  

- Konfigurieren Sie eine Always On-Verfügbarkeitsgruppe für SQL Server für die Standortdatenbank an primären Standorten und für den Standort der zentralen Verwaltung.

- Standorte unterstützen mehrere Instanzen von Standortsystemrollen, die wichtige Dienste für Clients bereitstellen. Dies umfasst beispielsweise Verwaltungs- und Verteilungspunkte.  

- Von Standorten der zentralen Verwaltung und primären Standorten wird die Sicherung der Standortdatenbank unterstützt. In der Standortdatenbank werden sämtlichen Konfigurationen für Standorte und Clients gespeichert. Die verschiedenen Standorte innerhalb einer Hierarchie haben Zugriff auf die Konfigurationsdaten.  

- Mithilfe von integrierten Optionen zur Standortwiederherstellung können Serverausfälle reduziert werden. Diese erweiterten Optionen vereinfachen die Wiederherstellung, wenn Sie über eine Hierarchie mit einem Standort der zentralen Verwaltung verfügen.  

- Typische Probleme können von Clients automatisch und ohne Eingreifen des Administrators behoben werden.  

- Von Standorten werden Warnungen zu Clients ausgegeben, von denen keine aktuellen Daten übermittelt werden. Administratoren werden so auf potenzielle Probleme aufmerksam gemacht.  

- Es sind mehrere Berichte und Dashboards in Configuration Manager integriert. Verwenden Sie diese Berichte und Dashboards, um Probleme und Trends zu identifizieren, bevor diese sich zu Problemen für Server- oder Clientvorgänge entwickeln.  

Configuration Manager umfasst verschiedene Features, die nahezu in Echtzeit ausgeführt werden. Wenn diese Features wichtig sind, damit Ihre Unternehmensanforderungen erfüllt werden, planen und konfigurieren Sie Ihre Standorte und Hierarchien, um Hochverfügbarkeit zu erreichen. Beispiel:  

- Durch [Aktionen zur Benachrichtigung von Clients](../../../clients/manage/manage-clients.md) (z.B. Neustarts) werden Überprüfungen von Windows Defender oder Remotedesktopverbindungen gestartet.  

- Zustandsbasierte Nachrichten zum Überwachen von Features wie Softwareupdates und Endpoint Protection.

- [Skripts](../../../../apps/deploy-use/create-deploy-scripts.md)

- [CMPivot](../../manage/cmpivot.md)

Andere Configuration Manager-Features stellen keine Echtzeitdienste bereit. Diese Features umfassen u.a. Clienteinstellungen, Hardware- und Softwareinventur, Softwarebereitstellungen und Konformitätseinstellungen. Stellen Sie sich auf ein gewisses Maß an Datenlatenz ein, wenn Sie diese Features verwenden. In den meisten Szenario ist es ungewöhnlich, dass sich eine vorübergehende Dienstunterbrechung zu einem kritischen Problem entwickelt. Sie können die Downtime minimieren, indem Sie die Autonomie der Vorgänge aufrechterhalten, einen hohen Servicelevel bereitstellen sowie Ihre Standorte und Hierarchien im Hinblick auf Hochverfügbarkeit konfigurieren.  

Beispielsweise führen Configuration Manager-Clients Verarbeitungsvorgänge in der Regel autonom aus. Dabei werden bekannte Zeitpläne und Konfigurationen für Vorgänge sowie Zeitpläne für die Übermittlung der zu verarbeitenden Daten an den Standort verwendet.  

- Wenn die Clients keine Verbindung mit dem Standort herstellen können, werden die zu übermittelnden Daten so lange zwischengespeichert, bis eine Verbindung hergestellt werden kann.  

- Clients, die keine Verbindung mit dem Standort herstellen können, werden trotzdem weiterhin ausgeführt. Sie verwenden dann so lange die letzten bekannten Zeitpläne und zwischengespeicherten Informationen, bis sie wieder eine Verbindung mit dem Standort herstellen und neue Richtlinien empfangen können. Beispielsweise kann ein Client eine zuvor heruntergeladene Anwendung speichern, die er ausführen und installieren muss.

- Der Standort überprüft seine Standortsysteme und Clients auf regelmäßige Statusaktualisierungen. Er generiert Warnungen, wenn diese Komponenten nicht registriert werden können.  

- Über integrierte Berichte erhalten Sie einen Einblick in den laufenden Betrieb sowie in frühere Vorgänge und aktuelle Trends. Configuration Manager unterstützt auch statusbasierte Meldungen, über die Informationen zu laufenden Vorgängen beinahe in Echtzeit bereitgestellt werden.  


## <a name="high-availability-for-sites-and-hierarchies"></a><a name="bkmk_snh"></a> Hohe Verfügbarkeit für Standorte und Hierarchien  

### <a name="use-a-site-server-in-passive-mode"></a>Verwenden eines Standortservers im passiven Modus

Installieren Sie einen zusätzlichen Standortserver im *passiven* Modus für einen eigenständigen primären Standort. Der Standortserver im passiven Modus dient als Ergänzung zu Ihrem vorhandenen Standortserver im *aktiven* Modus. Ein Standortserver im passiven Modus ist bei Bedarf sofort einsatzbereit. Weitere Informationen finden Sie unter [Site server high availability (Hochverfügbarkeit des Standortservers)](site-server-high-availability.md).  

### <a name="use-a-remote-content-library"></a>Verwenden einer Remoteinhaltsbibliothek

Verschieben Sie die Inhaltsbibliothek eines Standorts auf einen Remotestandort, der einen Speicher mit Hochverfügbarkeit bereitstellt. Dieses Feature ist erforderlich, um Hochverfügbarkeit für den Standortserver zu gewährleisten. Weitere Informationen finden Sie unter [Die Inhaltsbibliothek](../../../plan-design/hierarchy/the-content-library.md#bkmk_remote).

### <a name="centralize-content-sources"></a>Zentralisieren von Inhaltsquellen

Für sämtliche Softwareinhalte in Configuration Manager ist es erforderlich, dass ein Paketquellspeicher auf dem Netzwerk gespeichert ist. Verwenden Sie zentralisierte Speicher mit Hochverfügbarkeit, um einen gebräuchlichen Speicherort für Paketquellen für sämtlichen Inhalt zu hosten.

### <a name="use-a-sql-server-always-on-availability-group-to-host-the-site-database"></a>Verwenden einer Always On-Verfügbarkeitsgruppe für SQL Server zum Hosten der Standortdatenbank

Hosten Sie die Standortdatenbank an primären Standorten und den Standort der zentralen Verwaltung für Always On-Verfügbarkeitsgruppen für SQL Server. Weitere Informationen finden Sie unter [Vorbereiten der Verwendung von SQL Server Always On-Verfügbarkeitsgruppen mit Configuration Manager](sql-server-alwayson-for-a-highly-available-site-database.md).  

### <a name="use-a-sql-server-cluster-to-host-the-site-database"></a>Hosten der Standortdatenbank mit einem SQL Server-Cluster

Wenn Sie für die Datenbank an einem Standort der zentralen Verwaltung oder einem primären Standort einen SQL Server-Cluster verwenden, profitieren Sie von der in SQL Server integrierten Failoverunterstützung.  

Sekundäre Standorte können keine SQL Server-Cluster verwenden, und die Sicherung oder Wiederherstellung ihrer Standortdatenbank wird nicht unterstützt. Zur Wiederherstellung eines sekundären Standorts installieren Sie den sekundären Standort vom übergeordneten primären Standort aus neu.  

### <a name="deploy-a-hierarchy-of-sites-with-a-central-administration-site-and-one-or-more-child-primary-sites"></a>Bereitstellen einer Standorthierarchie mit einem Standort der zentralen Verwaltung und untergeordneten primären Standorten

Mithilfe dieser Konfiguration kann eine Fehlertoleranz bereitgestellt werden, falls überlappende Netzwerksegmente von den Standorten verwaltet werden. Darüber hinaus beinhaltet diese Konfiguration eine zusätzliche Wiederherstellungsoption. So ist es möglich, die Standortdatenbank am wiederhergestellten Standort anhand der Informationen in der an einem anderen Standort verfügbaren freigegebenen Datenbank neu zu erstellen. Verwenden Sie diese Option, um eine fehlerhafte oder nicht verfügbare Sicherung der fehlerhaften Standortdatenbank zu ersetzen.  

### <a name="create-regular-backups-at-central-administration-sites-and-primary-sites"></a>Erstellen regelmäßiger Sicherungen am Standort der zentralen Verwaltung und an primären Standorten

Wenn Sie regelmäßig Standortsicherungen erstellen und testen, wird sichergestellt, dass Sie über die Daten verfügen, die für die Standortwiederherstellung benötigt werden. Außerdem üben Sie so, wie Sie in möglichst kurzer Zeit einen Standort wiederherstellen.  

### <a name="install-multiple-instances-of-site-system-roles"></a>Installieren mehrerer Instanzen von Standortsystemrollen

Wenn Sie mehrere Instanzen von wichtigen Standortsystemrollen installieren, werden redundante Kontaktpunkte für Clients bereitgestellt. Beispielsweise wird durch Verwaltungs- und Verteilungspunkte ein redundanter Dienst bereitgestellt, wenn ein bestimmter Server offline ist.  

### <a name="install-multiple-instances-of-the-sms-provider-at-a-site"></a>Installieren mehrerer Instanzen des SMS-Anbieters an einem Standort

Der SMS-Anbieter stellt den administrativen Kontaktpunkt für mindestens eine Configuration Manager-Konsole bereit. Installieren Sie mehrere SMS-Anbieter, um Redundanz für Kontaktpunkte bereitzustellen, die zur Verwaltung Ihres Standorts und Ihrer Hierarchie dienen.  


## <a name="high-availability-for-site-system-roles"></a><a name="bkmk_ssr"></a> Hohe Verfügbarkeit für Standortsystemrollen

Sie stellen an jedem Standort Standortsystemrollen bereit, um die Dienste verfügbar zu machen, die an diesem Standort von Clients verwendet werden sollen. Die Standortdatenbank enthält die Konfigurationsinformationen für den Standort und sämtliche Clients. Verwenden Sie mindestens eine der verfügbaren Optionen, um die Hochverfügbarkeit der Standortdatenbank sowie bei Bedarf die Wiederherstellung des Standorts und der Standortdatenbank zu ermöglichen.  

### <a name="redundancy-for-important-site-system-roles"></a>Redundanz für wichtige Standortsystemrollen

- Anwendungskatalog-Webdienstpunkt  

- Anwendungskatalog-Websitepunkt  

- Verteilungspunkt  

- Verwaltungspunkt  

- Softwareupdatepunkt  

- Zustandsmigrationspunkt  

Sie können mehrere Instanzen der Reporting Services-Punkte installieren, um Redundanz für die Berichterstattung an Standorten und auf Clients bereitzustellen.

Verwenden Sie zur Failoverunterstützung mit dem Softwareupdatepunkt Windows PowerShell, um diese Rolle auf einem Windows-Cluster für den Netzwerklastenausgleich zu installieren.  

### <a name="built-in-site-backup"></a>Integrierte Standortsicherung

Configuration Manager enthält einen integrierten Sicherungstask, mit dessen Hilfe Sie einen Standort und kritische Informationen regelmäßig sichern können. Darüber hinaus unterstützt der Setup-Assistent von Configuration Manager Standortwiederherstellungsaktionen, mit denen Sie die Betriebsfähigkeit eines Standorts wiederherstellen können.  

### <a name="publishing-to-active-directory-domain-services-and-dns"></a>Veröffentlichen in Active Directory-Domänendiensten und DNS

Konfigurieren Sie jeden Standort so, dass er seine Daten zum Standort in Active Directory Domain Services und DNS veröffentlicht. Durch diese Veröffentlichung können Clients den Server auf dem Netzwerk ermitteln, der am besten zugänglich ist. Außerdem wird die Veröffentlichung von Clients verwendet, um zu ermitteln, ob neue Standortsystemserver verfügbar sind, damit wichtige Dienste wie Verwaltungspunkte bereitgestellt werden können.  

### <a name="sms-provider-and-configuration-manager-console"></a>SMS-Anbieter und Configuration Manager-Konsole

Configuration Manager unterstützt die Installation mehrerer SMS-Anbieter auf separaten Servern, damit die Konsole auf mehrere Zugriffspunkte zugreifen kann. Wenn ein Server eines SMS-Anbieters offline ist, können Sie trotzdem weiterhin Standorte und Clients abrufen und verwalten.  

Beim Herstellen einer Verbindung mit einem Standort stellt eine Configuration Manager-Konsole eine Verbindung mit einer Instanz des SMS-Anbieters an diesem Standort her. Die Instanz des SMS-Anbieters wird zufällig ausgewählt. Wenn der ausgewählte SMS-Anbieter nicht verfügbar ist, haben Sie folgende Möglichkeiten:  

- Verbinden Sie die Konsole erneut mit dem Standort. Jeder neuen Verbindungsanforderung wird zufällig eine Instanz des SMS-Anbieters zugewiesen. Möglicherweise wird der neuen Verbindungsanforderung auch eine verfügbare Instanz zugewiesen.  

- Verbinden Sie die Konsole mit einem anderen Configuration Manager-Standort, und verwalten Sie die Konfiguration über diese Verbindung. Diese Option ruft bei Konfigurationsänderungen eine kurze Verzögerung von wenigen Minuten hervor. Sobald der SMS-Anbieter des Standorts online ist, verbinden Sie die Configuration Manager-Konsole wieder direkt mit dem zu verwaltenden Standort.  

Sie können die Configuration Manager-Konsole auf mehreren Computern installieren, die von Administratoren verwendet werden sollen. Sämtliche SMS-Anbieter unterstützen Verbindungen, die von mehreren Konsolen ausgehen.  

### <a name="management-point"></a>Verwaltungspunkt

Installieren Sie an jedem primären Standort mehrere Verwaltungspunkte, und sorgen Sie dafür, dass die Veröffentlichung von Standortdaten in der Active Directory-Infrastruktur und DNS durch die Standorte möglich ist.  

Sind mehrere Verwaltungspunkte vorhanden, können Sie einen Lastenausgleich vornehmen, wenn ein einzelner Verwaltungspunkt von mehreren Clients in Anspruch genommen wird. Sie sollten auch in Betracht ziehen, mindestens ein Datenbankreplikat für Verwaltungspunkte zu installieren. Diese Konfiguration schwächt prozessorintensive Vorgänge des Verwaltungspunkts ab. Außerdem wird die Verfügbarkeit dieser wichtigen Standortsystemrolle erhöht.  

Sekundäre Standorte unterstützen nur die Installation eines Verwaltungspunkts, der sich auf dem sekundären Standortserver befinden muss. Verwaltungspunkte auf sekundären Standorten werden nicht als Konfiguration mit Hochverfügbarkeit angesehen.  

> [!NOTE]  
> Von der lokalen mobilen Geräteverwaltung verwaltete Geräte werden nur mit einem einzigen Verwaltungspunkt an einem primären Standort verbunden. Der Verwaltungspunkt wird während der Registrierung von Configuration Manager dem mobilen Gerät zugewiesen und danach nicht mehr geändert. Wenn Sie mehrere Verwaltungspunkte installieren und für mobile Geräte mehr als einen dieser Punkte aktivieren, ist der Verwaltungspunkt, der einem Client für mobile Geräte zugewiesen ist, nicht deterministisch.  
>
> Falls der von einem mobilen Geräteclient verwendete Verwaltungspunkt nicht mehr verfügbar ist, müssen Sie das Problem für diesen Verwaltungspunkt beheben. Sie können das mobile Gerät auch zurücksetzen und neu registrieren, damit es einem betriebsbereiten Verwaltungspunkt zugewiesen werden kann, der für mobile Geräte aktiviert ist.  

### <a name="distribution-point"></a>Verteilungspunkt

Installieren Sie mehrere Verteilungspunkte, und stellen Sie Inhalte für mehrere Verteilungspunkte bereit. Fügen Sie mehr als einen Verteilungspunkt pro Begrenzungsgruppe hinzu, um sicherzustellen, dass die Clients mehrere Optionen in ihren Inhaltsanforderungen erhalten. Konfigurieren Sie Beziehungen von Begrenzungsgruppen, damit ihr Fallbackverhalten für andere Begrenzungsgruppen oder Cloudverteilungspunkte vorhersagbar ist. Weitere Informationen finden Sie unter [Configure boundary groups](boundary-groups.md) (Konfigurieren von Begrenzungsgruppen).  

### <a name="application-catalog-web-service-point-and-application-catalog-website-point"></a>Anwendungskatalog-Webdienstpunkt und Anwendungskatalog-Websitepunkt

> [!Important]
> Die Silverlight-Benutzeroberfläche für den Anwendungskatalog wird ab Current Branch-Version 1806 nicht unterstützt. Ab Version 1906 verwenden aktualisierte Clients automatisch den Verwaltungspunkt für Anwendungsbereitstellungen, die Benutzern zur Verfügung stehen. Zudem können Sie keine neuen Anwendungskatalogrollen installieren. Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910.  
>
> Weitere Informationen finden Sie in den folgenden Artikeln:
>
> - [Konfigurieren des Softwarecenters](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Entfernte und veraltete Features](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Installieren Sie mehrere Instanzen jeder Standortsystemrolle. Stellen Sie jeweils eine Instanz pro Rolle auf dem Standortsystemserver bereit, um optimale Leistung zu erzielen.  

Jede Standortsystemrolle des Anwendungskatalogs stellt die gleichen Informationen wie andere Instanzen dieser Rolle bereit, unabhängig davon, wo sich diese in der Hierarchie befindet. Wenn ein Client eine Anforderung an den Anwendungskatalog sendet und Sie die Clients so konfiguriert haben, dass sie den Standartanwendungskatalog-Websitepunkt automatisch ermitteln, wird der Client auf eine verfügbare Instanz weitergeleitet. Clients bevorzugen lokale Instanzen des Anwendungskatalogs basierend auf der aktuellen Netzwerkadresse des Clients.  

Weitere Informationen zu dieser Clienteinstellung und zur automatischen Ermittlung finden Sie unter den Clienteinstellungen für [Computer-Agent](../../../clients/deploy/about-client-settings.md#computer-agent).  


## <a name="high-availability-for-clients"></a><a name="bkmk_client"></a> Hohe Verfügbarkeit für Clients  

### <a name="client-operations-are-autonomous"></a>Autonomie von Clientvorgängen

Die Clientautonomie von Configuration Manager umfasst die folgenden Verhaltensweisen:  

- Für Clients ist keine ständige Verbindung mit bestimmten Standortsystemservern erforderlich. Von den Clients werden bekannte Konfigurationen verwendet, um vorkonfigurierte Aktionen nach einem Zeitplan auszuführen.  

- Clients können jede beliebige Instanz der Standortsystemrolle verwenden, die Dienste für Clients bereitstellt. Sie versuchen, so lange bekannte Server zu kontaktieren, bis sie einen verfügbaren Server gefunden haben.  

- Von Clients können Inventuren, Softwarebereitstellungen und ähnliche geplante Aktionen auch ohne direkte Verbindung mit Standortsystemservern ausgeführt werden.  

- Von Clients, die zur Verwendung eines Fallbackstatuspunkts konfiguriert sind, können Details an den Fallbackstatuspunkt gesendet werden, wenn die Kommunikation mit einem Verwaltungspunkt nicht möglich ist.  

### <a name="clients-can-repair-themselves"></a>Automatische Wartung von Clients

Die meisten typischen Probleme werden von Clients automatisch und ohne direkten Eingriff durch einen Administrator behoben.  

- Clients bewerten ihren Zustand in regelmäßigen Abständen selbst. Standardprobleme werden ggf. mithilfe der lokal zwischengespeicherten Wiederherstellungsschritte und Quelldateien behoben.  

- Wenn von einem Client keine Statusinformationen an den ihm zugewiesenen Standort übermittelt werden, kann vom Standort eine Warnung ausgegeben werden. Administratoren, bei denen diese Warnungen eingehen, können sofort handeln, um den normalen Betrieb des Clients wiederherzustellen.  

### <a name="clients-cache-information-to-use-in-the-future"></a>Zwischenspeicherung von Informationen zur späteren Verwendung

Bei der Kommunikation eines Clients mit einem Verwaltungspunkt können die folgenden Informationen vom Client abgerufen und zwischengespeichert werden:  

- Clienteinstellungen  

- Clientzeitpläne  

- Informationen über Softwarebereitstellungen und einen Download der Software, die laut Zeitplan vom Client installiert werden soll, sofern die Bereitstellung für diese Aktion konfiguriert ist  

Wenn ein Client mit keinem Verwaltungspunkt eine Verbindung herstellen kann, speichern die Clients den Status, den Zustand und die Clientinformationen lokal zwischen, die sie dem Standort melden. Der Client überträgt diese Daten, nachdem er Kontakt zu einem Verwaltungspunkt aufgenommen hat.  

### <a name="client-can-submit-status-to-a-fallback-status-point"></a>Übermittlung des Status an einen Fallbackstatuspunkt

Wenn Sie einen Client zur Verwendung eines Fallbackstatuspunkts konfigurieren, weisen Sie dem Client einen zusätzlichen Kontaktpunkt für die Übermittlung wichtiger Details zu seinen Vorgängen zu. Von Clients, die zur Verwendung eines Fallbackstatuspunkts konfiguriert sind, werden auch dann weiterhin Statusinformationen über ihre Vorgänge an diese Standortsystemrolle gesendet, wenn keine Verbindung mit einem Verwaltungspunkt hergestellt werden kann.  

### <a name="central-management-of-client-data-and-client-identity"></a>Zentrale Verwaltung von Clientdaten und Clientidentität

Wichtige Informationen über die Identität eines Clients werden nicht jeweils vom Client selbst, sondern von der Standortdatenbank gespeichert und einem bestimmten Computer oder Benutzer zugeordnet.  

- Die Clientquelldateien auf einem Computer können ohne Auswirkungen auf die historischen Datensätze für den Computer mit dem installierten Client deinstalliert und erneut installiert werden.  

- Fehler auf einem Clientcomputer wirken sich nicht auf die Integrität der in der Datenbank gespeicherten Informationen aus. Diese Informationen können für die Berichterstellung verfügbar bleiben.  


## <a name="options-for-sites-and-site-system-roles-that-arent-highly-available"></a><a name="bkmk_nonHAoptions"></a> Optionen für Standorte und Standortsystemrollen ohne Hochverfügbarkeit

Von einigen Standortsystemen wird nur eine Instanz an einem Standort oder in der Hierarchie unterstützt. Die Informationen können Ihnen bei der Vorbereitung auf das Offlineschalten dieser Standortsysteme helfen.  

### <a name="asset-intelligence-synchronization-point-hierarchy"></a>Asset Intelligence-Synchronisierungspunkt (Hierarchie)

Diese Standortsystemrolle wird als nicht erfolgskritisch betrachtet. Sie stellt optionale Funktionen in Configuration Manager bereit. Wenn dieses Standortsystem offline geschaltet wird, verwenden Sie eine der folgenden Optionen:  

- Beseitigen Sie die Ursache für den Offlinezustand des Standortsystems.  

- Deinstallieren Sie die Rolle vom aktuellen Server, und installieren Sie sie auf einem neuen Server.  

### <a name="endpoint-protection-point-hierarchy"></a>Endpoint Protection-Punkt (Hierarchie)

Diese Standortsystemrolle wird als nicht erfolgskritisch betrachtet. Sie stellt optionale Funktionen in Configuration Manager bereit. Wenn dieses Standortsystem offline geschaltet wird, verwenden Sie eine der folgenden Optionen:  

- Beseitigen Sie die Ursache für den Offlinezustand des Standortsystems.  

- Deinstallieren Sie die Rolle vom aktuellen Server, und installieren Sie sie auf einem neuen Server.  

### <a name="enrollment-point-site"></a>Anmeldungspunkt (Standort)

Diese Standortsystemrolle wird als nicht erfolgskritisch betrachtet. Sie stellt optionale Funktionen in Configuration Manager bereit. Wenn dieses Standortsystem offline geschaltet wird, verwenden Sie eine der folgenden Optionen:  

- Beseitigen Sie die Ursache für den Offlinezustand des Standortsystems.  

- Deinstallieren Sie die Rolle vom aktuellen Server, und installieren Sie sie auf einem neuen Server.  

### <a name="enrollment-proxy-point-site"></a>Anmeldungsproxypunkt (Standort)

Diese Standortsystemrolle wird als nicht erfolgskritisch betrachtet. Sie stellt optionale Funktionen in Configuration Manager bereit. Allerdings können Sie mehrere Instanzen dieser Standortsystemrolle auf einem Standort sowie auf mehreren Standorten in der Hierarchie installieren. Wenn dieses Standortsystem offline geschaltet wird, verwenden Sie eine der folgenden Optionen:  

- Beseitigen Sie die Ursache für den Offlinezustand des Standortsystems.  

- Deinstallieren Sie die Rolle vom aktuellen Server, und installieren Sie sie auf einem neuen Server.  

Wenn Sie auf einem Standort über mehrere Anmeldungsproxypunkte verfügen, verwenden Sie für den Servernamen einen DNS-Alias. Wenn Sie diese Konfiguration verwenden, werden Benutzern beim Anmelden Ihrer mobilen Geräte mithilfe von DNS-Roundrobin Fehlertoleranz und Lastenausgleich zur Verfügung gestellt.  

### <a name="fallback-status-point-site-or-hierarchy"></a>Fallbackstatuspunkt (Standort oder Hierarchie)

Diese Standortsystemrolle wird als nicht erfolgskritisch betrachtet. Sie stellt optionale Funktionen in Configuration Manager bereit. Wenn dieses Standortsystem offline geschaltet wird, verwenden Sie eine der folgenden Optionen:  

- Beseitigen Sie die Ursache für den Offlinezustand des Standortsystems.  

- Deinstallieren Sie die Rolle vom aktuellen Server, und installieren Sie sie auf einem neuen Server. Da Clients der Fallbackstatuspunkt während der Clientinstallation zugewiesen wird, müssen Sie vorhandene Clients ändern, damit sie den neuen Standortsystemserver verwenden können.  

### <a name="service-connection-point-hierarchy"></a>Dienstverbindungspunkt (Hierarchie)

Diese Standortsystemrolle ist wichtig, damit der aktuelle Configuration Manager-Branch immer auf dem neusten Stand bleibt. Er wird in der Regel nur selten verwendet. Wenn dieses System offline geschaltet wird, verwenden Sie eine der folgenden Optionen:

- Beseitigen Sie die Ursache für den Offlinezustand des Standortsystems.  

- Deinstallieren Sie die Rolle vom aktuellen Server, und installieren Sie sie auf einem neuen Server.  


## <a name="see-also"></a>Weitere Informationen:

- [Unterstützte Konfigurationen](../../../plan-design/configs/supported-configurations.md)  

- [Empfohlene Hardware](../../../plan-design/configs/recommended-hardware.md)  

- [Unterstützte Betriebssysteme für Standortsystemserver](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md)

- [Voraussetzungen für Standorte und Standortsysteme](../../../plan-design/configs/site-and-site-system-prerequisites.md)  

- [Auswirkungen von Standortausfällen](../../manage/site-failure-impacts.md)  
