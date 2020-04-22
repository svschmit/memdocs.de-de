---
title: Datenbankreplikation
titleSuffix: Configuration Manager
description: In diesem Artikel erfahren Sie, wie die Configuration Manager-Datenbankreplikation SQL Server für die Datenübertragung in der Hierarchie verwendet.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8b495b02-c966-4eb3-92b9-52ebbf5c38ae
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d1a2c8baa349e6499aa483f947d94f7459357be4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703598"
---
# <a name="database-replication"></a>Datenbankreplikation

*Gilt für: Configuration Manager (Current Branch)*

Die Configuration Manager-Datenbankreplikation verwendet SQL Server für die Datenübertragung. Durch dieses Verfahren werden Änderungen in der Standortdatenbank mit den Informationen aus der Datenbank an anderen Standorten in der Hierarchie zusammengeführt.

Bitte beachten Sie bei der Datenbankreplikation die folgenden Punkte:

- Alle Standorte verfügen über die gleichen Informationen.  

- Wenn Sie in einer Hierarchie einen Standort installieren, wird von Configuration Manager automatisch die Datenbankreplikation zwischen dem neuen und dem übergeordneten Standort eingerichtet.  

- Nach Abschluss der Standortinstallation wird die Datenbankreplikation automatisch gestartet.  

Wenn Sie einer Hierarchie einen neuen Standort hinzufügen, wird an diesem neuen Standort eine generische Datenbank von Configuration Manager erstellt. Der übergeordnete Standort erstellt eine Momentaufnahme der relevanten Daten in seiner Datenbank. Anschließend überträgt er die Momentaufnahme im Rahmen der [dateibasierten Replikation](file-based-replication.md) an den neuen Standort. Mithilfe von BCP, eines Massenkopierprogramms für SQL Server, werden die Informationen dann in die lokale Kopie der Configuration Manager-Datenbank am neuen Standort geladen. Nach dem Laden des Snapshots wird an jedem Standort eine Datenbankreplikation mit dem anderen Standort ausgeführt.  

Daten werden von Configuration Manager mithilfe eines Datenbankreplikationsdienstes zwischen Standorten repliziert. Der Datenbankreplikationsdienst verwendet SQL Server-Änderungsverfolgung, um die lokale Standortdatenbank auf Änderungen zu überwachen. Anschließend werden die Änderungen mithilfe von SQL Server Service Broker (SSB) an andere Standorte repliziert. Für diesen Prozess wird standardmäßig TCP-Port 4022 verwendet.  


## <a name="replication-groups"></a>Replikationsgruppen

Daten, die mithilfe der Datenbankreplikation repliziert werden, werden von Configuration Manager in verschiedene Replikationsgruppen unterteilt. Für jede Replikationsgruppe ist ein separater fester Replikationszeitplan festgelegt. Der Standort bestimmt anhand dieses Zeitplans, wie oft Änderungen an andere Standorte repliziert werden.  

Beispielsweise wird eine Änderung an der rollenbasierten Verwaltung rasch auf andere Standorte repliziert. Durch dieses Verhalten wird sichergestellt, dass die Änderung vom anderen Standort so schnell wie möglich erzwungen wird. Eine Konfigurationsänderung mit niedrigerer Priorität, wie etwa die Installation eines neuen sekundären Standorts, wird mit geringerer Dringlichkeit repliziert. Es kann einige Minuten in Anspruch nehmen, bis eine neue Standortanfrage den primären Zielort erreicht hat.  


## <a name="settings"></a>Einstellung

Sie können folgende Einstellungen für die Datenbankreplikation ändern:  

- **Datenbankreplikationslinks**: Steuern, wann bestimmter Datenverkehr das Netzwerk durchläuft.  

- **Verteilte Ansichten**: Wenn ein Standort der zentralen Verwaltung (CAS) ausgewählte Standortdaten anfordert, kann er die Daten direkt aus der Datenbank an einem untergeordneten primären Standort aufrufen.  

- **Zeitpläne**: Legen den Zeitpunkt der Verwendung eines Replikationslinks fest und wann verschiedene Arten von Standortdaten repliziert werden.  

- **Zusammenfassung**: Nehmen Änderungen an Einstellungen für die Datenzusammenfassung vor, die den Netzwerkverkehr betrifft, der die Replikationslinks durchläuft. Die Zusammenfassung erfolgt standardmäßig alle 15 Minuten. Sie fließt in Berichte über die Datenbankreplikation ein.  

- **Schwellenwerte für die Datenbankreplikation**: Hiermit wird festgelegt, wann der Standort Links als heruntergestuft oder fehlerhaft meldet. Sie können auch festlegen, wann von Configuration Manager Warnungen zu Replikationslinks mit dem heruntergestuften oder fehlerhaften Status ausgelöst werden.  


## <a name="types-of-data"></a>Datentypen

Von Configuration Manager replizierte Daten werden hauptsächlich entweder als *globale Daten* oder als *Standortdaten* klassifiziert. Im Rahmen der Datenbankreplikation werden Änderungen an globalen Daten und Standortdaten vom Standort über den Datenbankreplikationslink übertragen. Globale Daten werden auf einen übergeordneten oder untergeordneten Standort repliziert. Standortdaten können nur auf übergeordnete Standorte repliziert werden. Die sogenannten *lokalen Daten* als dritter Datentyp werden nicht auf andere Standorte repliziert. Lokale Daten sind Informationen, die von anderen Standorten nicht benötigt werden.  

### <a name="global-data"></a>Globale Daten

Globale Daten sind Objekte, die von Administratoren erstellt wurden und die an alle Standorte innerhalb der Hierarchie repliziert werden. Sekundäre Standorte empfangen nur eine Teilmenge globaler Daten (als globale Proxydaten). Sie erstellen globale Daten am Standort der zentralen Verwaltung und an primären Standorten. Zu diesem Typ zählen folgende Daten:

- Softwarebereitstellungen
- Softwareupdates
- Sammlungsdefinitionen
- Sicherheitsumfang der rollenbasierten Verwaltung

### <a name="site-data"></a>Standortdaten

Standortdaten sind operative Informationen, die von primären Configuration Manager-Standorten und ihren zugehörigen Clients erstellt werden. Standortdaten werden an den Standort der zentralen Verwaltung, jedoch nicht an andere Standorte repliziert. Standortdaten können nur am Standort der zentralen Verwaltung und an dem primären Standort angezeigt werden, von dem sie stammen. Sie können Standortdaten nur an dem primären Standort ändern, an dem sie erstellt wurden. Zu diesem Typ zählen folgende Daten:

- Hardwareinventur
- Statusmeldungen
- Warnungen
- Die Ergebnisse von abfragebasierten Sammlungen

Alle Standortdaten werden an den Standort der zentralen Verwaltung repliziert. Der Standort der zentralen Verwaltung ist Verwaltung und Berichterstattung in der gesamten Standorthierarchie zuständig.  


## <a name="database-replication-links"></a><a name="bkmk_Dblinks"></a> Datenbankreplikationslinks

Wenn Sie in einer Hierarchie einen neuen Standort installieren, wird von Configuration Manager ein Datenbankreplikationslink zwischen dem übergeordneten und neuen Standort erstellt. Für die Verbindung der beiden Standorte wird ein einzelner Link erstellt.  

Um die Datenübertragung über den Datenbank-Replikationslink zu steuern, ändern Sie die Einstellungen für die einzelnen Links. Von jedem Replikationslink werden separate Konfigurationen unterstützt. Für jeden Datenbankreplikationslink kann Folgendes gesteuert werden:  

- Beenden der Replikation ausgewählter Standortdaten von einem primären Standort zum Standort der zentralen Verwaltung. Durch diese Aktion kann der Standort der zentralen Verwaltung direkt aus der Datenbank des primären Standorts auf die Daten zugreifen.  

- Festlegen des Zeitpunkts der Übertragung ausgewählter Standortdaten von einem untergeordneten primären Standort zum Standort der zentralen Verwaltung.

- Definieren der Einstellungen, die bestimmen, wann sich ein Datenbankreplikationslink in einem heruntergestuften oder fehlerhaften Status befindet.

- Angeben, wann Warnungen zu einem fehlgeschlagenen Replikationslink ausgelöst werden sollen.

- Geben Sie an, wie häufig Daten zum Replikationsverkehr, der über den Replikationslink abgewickelt wird, von Configuration Manager zusammengefasst werden. Diese Daten werden in Berichten verwendet.

Wechseln Sie zum Konfigurieren eines Datenbank-Replikationslinks in der Configuration Manager-Konsole zum Arbeitsbereich **Überwachung**. Wählen Sie den Knoten **Datenbankreplikation** aus, und bearbeiten Sie die Eigenschaften für den Link. Dieser Knoten befindet sich auch im Arbeitsbereich **Verwaltung** unter dem Knoten **Hierarchiekonfiguration**. Bearbeiten Sie einen Replikationslink entweder am übergeordneten Standort oder am untergeordneten Standort des Replikationslinks.  

> [!TIP]  
> Sie können Datenbankreplikationslinks über den Knoten **Datenbankreplikation** in beiden Arbeitsbereichen bearbeiten. Wenn Sie jedoch den Knoten **Datenbankreplikation** im Arbeitsbereich **Überwachung** verwenden, können Sie auch den Status der Datenbankreplikation verfolgen. Er bietet auch Zugriff auf das Tool [Replikationslinkanalyse](../../servers/manage/monitor-replication.md#BKMK_RLA). Mithilfe dieses Tools können Sie Probleme bei der Datenbankreplikation untersuchen.  

Weitere Informationen zum Konfigurieren von Replikationslinks finden Sie unter [Steuerelemente für die Replikation von Standortdatenbanken](#BKMK_DBRepControls). Weitere Informationen zum Überwachen der Replikation finden Sie unter [Überwachen der Datenbankreplikation](../../servers/manage/monitor-replication.md).  


## <a name="distributed-views"></a><a name="bkmk_distviews"></a> Verteilte Ansichten  

Über verteilte Ansichten wird bei Senden einer Anforderung an den Standort der zentralen Verwaltung direkt auf den untergeordneten primären Standort zugegriffen. Durch die Gewährung eines direkten Zugriffs müssen Standortdaten nicht mehr vom primären Standort an den Standort der zentralen Verwaltung repliziert werden. Sie können verteilte Ansichten auf den von Ihnen ausgewählten Replikationslinks verwenden, da Replikationslinks voneinander unabhängig sind. Sie können verteilte Ansichten nicht zwischen einem primären und einem sekundären Standort verwenden.  

Aus verteilten Ansichten ergeben sich die folgenden Vorteile:  

- Verringerung der CPU-Last bei der Verarbeitung von Datenbankänderungen am Standort der zentralen Verwaltung und an primären Standorten

- Verringerung der Datenmengen, die über das Netzwerk an den Standort der zentralen Verwaltung übertragen werden

- Verbesserung der Leistung der SQL Server-Instanz, auf dem die Datenbank des Standorts der zentralen Verwaltung gehostet wird

- Verringern des von der Datenbank des Standorts der zentralen Verwaltung genutzten Speicherplatzes

Die Verwendung verteilter Ansichten bietet sich an, wenn sich ein primärer Standort im Netzwerk in der Nähe des Standorts der zentralen Verwaltung befindet und beide Standorte stets aktiviert und verbunden sind. Die Replikation ausgewählter Daten zwischen den Standorten wird dank der verteilten Ansichten durch direkte Verbindungen zwischen den SQL Server-Instanzen an beiden Standorten ersetzt. Der Standort der zentralen Verwaltung stellt bei jeder Anforderung dieser Daten eine direkte Verbindung her.

Der Standort fordert beispielsweise in den folgenden Szenarien Daten der verteilten Ansichten an:

- Beim Ausführen von Berichten oder Abfragen
- Beim Anzeigen von Informationen in Ressourcen-Explorer
- Sammlungsauswertung für Sammlungen, die auf Standortdaten basierende Regeln enthalten

Verteilte Ansichten sind standardmäßig für alle Replikationslinks deaktiviert. Wenn Sie verteilte Ansichten aktivieren, wählen Sie Standortdaten aus, die nicht über diesen Link an den Standort der zentralen Verwaltung repliziert werden. Der Zugriff auf diese Daten in der Datenbank des primären Standorts erfolgt direkt von der Datenbank des untergeordneten primären Standorts aus, der den Link freigibt. Sie können die folgenden Arten von Standortdaten für verteilte Ansichten konfigurieren:  

- **Hardwareinventurdaten** von Clients
- **Softwareinventurdaten und Softwaremessungsdaten** von Clients
- **Statusmeldungen** von Clients, vom primären Standort und von allen sekundären Standorten

Wenn Sie Daten in der Configuration Manager-Konsole oder in Berichten anzeigen, sind verteilte Daten für Sie operativ nicht sichtbar. Wenn Sie Daten anfordern, die für verteilte Ansichten aktiviert sind, greift der Datenbankserver des Standorts der zentralen Verwaltung direkt auf die Datenbank des untergeordneten primären Standorts zu, um die Informationen abzurufen.

Sie verwenden beispielsweise eine Configuration Manager-Konsole, die mit dem Standort der zentralen Verwaltung verbunden ist. Sie fordern Informationen zur Hardwareinventur von zwei primären Standorten an: ABC und XYZ. Sie haben nur die Hardwareinventur für verteilte Ansichten an Standort ABC aktiviert. Der Standort der zentralen Verwaltung ruft Inventurinformationen für XYZ-Clients aus seiner eigenen Datenbank ab. Der Standort der zentralen Verteilung ruft Inventurinformationen für ABC-Clients direkt aus der Datenbank an Standort ABC ab. Diese Informationen werden in der Configuration Manager-Konsole bzw. in einem Bericht ohne Hinweise auf die Quelle angezeigt.  

Wenn bei einem Replikationslink ein Datentyp für verteilte Ansichten aktiviert ist, werden diese Daten nicht vom untergeordneten primären Standort auf den Standort der zentralen Verwaltung repliziert. Wenn verteilte Ansichten für einen Datentyp deaktiviert werden, setzt der untergeordnete primäre Standort die normale Datenreplikation auf den Standort der zentralen Verwaltung fort. Bevor diese Daten am Standort der zentralen Verwaltung verfügbar werden, müssen die Replikationsgruppen für diese Daten zwischen dem primären Standort und dem Standort der zentralen Verwaltung neu initialisiert werden. Nach der Deinstallation eines primären Standorts mit aktivierten verteilten Ansichten müssen die Daten des Standorts der zentralen Verwaltung komplett neu initialisiert werden, damit Sie auf Daten zugreifen können, die am Standort der zentralen Verwaltung für verteilte Ansichten aktiviert waren.  

> [!IMPORTANT]  
> Wenn Sie verteilte Ansichten auf einem Replikationslink in der Standorthierarchie verwenden, deaktivieren Sie vor dem Deinstallieren eines primären Standorts verteilte Ansichten für alle Replikationslinks. Weitere Informationen finden Sie unter [Deinstallieren eines primären Standorts, der die verteilten Ansichten verwendet](../../servers/deploy/install/uninstall-sites-and-hierarchies.md#bkmk_distviews).  

### <a name="prerequisites-and-limitations-for-distributed-views"></a>Voraussetzungen und Einschränkungen für verteilte Ansichten  

- Verwenden Sie verteilte Ansichten nur auf Replikationslinks zwischen dem Standort der zentralen Verwaltung und einem primären Standort.

- Der Standort der zentralen Verwaltung muss eine Enterprise Edition von SQL Server verwenden. Für den primären Standort gilt diese Anforderung nicht.

- Der Standort der zentralen Verwaltung kann nur über eine SMS-Anbieter-Instanz verfügen. Installieren Sie diese eine Instanz auf dem Standortdatenbankserver. Diese Konfiguration unterstützt die Kerberos-Authentifizierung. Der SQL-Server am Standort der zentralen Verwaltung erfordert Kerberos, um auf den SQL-Server am untergeordneten primären Standort zuzugreifen. Für den SMS-Anbieter am untergeordneten primären Standort gelten keine Einschränkungen.

- Sie können nur einen Reporting Services-Punkt am Standort der zentralen Verwaltung installieren. Installieren Sie den SQL Server Reporting Services-Punkt auf dem Standortdatenbankserver. Diese Konfiguration unterstützt die Kerberos-Authentifizierung. Der SQL-Server am Standort der zentralen Verwaltung erfordert Kerberos, um auf den SQL-Server am untergeordneten primären Standort zuzugreifen.

- Sie können die Standortdatenbank nicht in einem [SQL Server-Cluster](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md) hosten.

- In Version 1902 und früher konnte die Standortdatenbank nicht in einer [Always On-Verfügbarkeitsgruppe für SQL Server](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md) gehostet werden. Aktualisieren Sie auf Version 1906 oder höher, damit eine solche Konfiguration unterstützt wird.<!-- SCCMDocs-pr#3792 -->

- Das Computerkonto des Datenbankservers des Standorts der zentralen Verwaltung muss über **Leseberechtigungen** für die Datenbank des primären Standorts verfügen.

> [!IMPORTANT]  
> Bei einem Datenbankreplikationslink schließen verteilte Ansichten und [Zeitpläne](#BKMK_schedules) für die Datenreplikation einander aus.  


## <a name="schedule-transfers-of-site-data"></a><a name="BKMK_schedules"></a> Planen der Übertragung von Standortdaten

Legen Sie einen Zeitplan für die Verwendung eines Replikationslinks fest, um die Steuerung der Netzwerkbandbreite für die Replikation von Standortdaten von einem untergeordneten primären Standort zum Standort der zentralen Verwaltung zu erleichtern. Geben Sie anschließend an, wann verschiedene Typen von Standortdaten repliziert werden. Sie können festlegen, wann Statusmeldungen, Inventurdaten und Messungsdaten vom primären Standort repliziert werden. Zeitpläne für Standortdaten werden von Datenbankreplikationslinks sekundärer Standorte nicht unterstützt. Für die Übertragung globaler Daten kann kein Zeitplan festgelegt werden.  

Wenn Sie einen Zeitplan für Datenbankreplikationslinks konfigurieren, können Sie die Übertragung ausgewählter Standortdaten vom primären Standort an den Standort der zentralen Verwaltung beschränken. Sie können auch unterschiedliche Zeiten für die Replikation verschiedener Typen von Standortdaten konfigurieren.  

> [!IMPORTANT]  
> Bei einem Datenbankreplikationslink schließen [verteilte Ansichten](#bkmk_distviews) und Zeitpläne für die Datenreplikation einander aus.  


## <a name="summarization-of-traffic"></a><a name="BKMK_SummarizeDBReplication"></a> Zusammenfassung des Datenverkehrs  

Daten zum Netzwerkverkehr, der über die Datenbankreplikationslinks der Standorte abgewickelt wird, werden von jedem Standort regelmäßig zusammengefasst. Der Standort nutzt zusammengefasste Daten in Berichten über die Datenbankreplikation. Der der über einen Replikationslink abgewickelte Netzwerkverkehr wird von beiden Standorten des Replikationslinks zusammengefasst. Die Daten werden vom Standortdatenbankserver zusammengefasst. Nach dem Zusammenfassen der Daten werden die Informationen als globale Daten an andere Standorte repliziert.  

Die Zusammenfassung erfolgt standardmäßig alle 15 Minuten. Sie können die Häufigkeit, mit der der Netzwerkverkehr zusammengefasst wird, ändern. Bearbeiten Sie dazu das **Zusammenfassungsintervall** in den Eigenschaften des Datenbankreplikationslinks. Die Häufigkeit der Zusammenfassung wirkt sich auf die Informationen aus, die Sie in Berichten über die Datenbankreplikation sehen. Sie können ein Intervall zwischen 5 und 60 Minuten auswählen. Wenn Sie die Häufigkeit der Zusammenfassung erhöhen, steigern Sie die Verarbeitungslast des SQL Servers an jedem Standort des Replikationslinks.  

## <a name="database-replication-thresholds"></a><a name="BKMK_DBRepThresholds"></a> Schwellenwerte für die Datenbankreplikation

Mit Schwellenwerten für die Datenbankreplikation wird bestimmt, wann ein Datenbankreplikationslink von Configuration Manager als heruntergestuft oder fehlerhaft gemeldet wird. Ein Link wird standardmäßig als *heruntergestuft* festgelegt, wenn eine Replikationsgruppe die Replikation zwölf Mal hintereinander nicht abschließen kann. Der Link wird als *fehlerhaft* festgelegt, wenn eine Replikationsgruppe die Replikation 24 Mal hintereinander nicht abschließen kann.  

Sie können benutzerdefinierte Werte für den Status „heruntergestuft“ oder „fehlerhaft“ angeben. Wenn Sie diese Werte anpassen, können Sie die Integrität der Datenbankreplikation für die Links genauer überwachen.  

Möglicherweise werden eine oder mehrere Replikationsgruppen nicht repliziert, während andere Replikationsgruppen weiterhin erfolgreich repliziert werden. Planen Sie die Überprüfung des Replikationsstatus eines Links, wenn dieser erstmalig als „heruntergestuft“ gemeldet wird.

Erwägen Sie in folgenden Situationen, die Werte für Wiederholungsversuche für den heruntergestuften oder fehlerhaften Status des Links zu ändern:

- Es gibt wiederholte Verzögerungen für bestimmte Replikationsgruppen, diese Verzögerung stellt jedoch kein Problem dar.

- Für die Netzwerkverbindung zwischen Standorten ist nur eine geringe Bandbreite verfügbar.

Wenn Sie die Anzahl der Wiederholungen erhöhen, nach denen der Link vom Standort als heruntergestuft oder fehlerhaft eingestuft wird, können Sie falsche Warnungen für bekannte Probleme verhindern. Mit dieser Aktion können Sie den Status des Links genauer nachverfolgen.  

Sie sollten auch das Synchronisierungsintervall jeder Replikationsgruppe in Betracht ziehen, um zu verstehen, wie häufig diese Gruppe repliziert wird. Wenn Sie das **Synchronisierungsintervall** für Replikationsgruppen überprüfen möchten, wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Überwachung**. Wählen Sie im Knoten **Datenbankreplikation** die Registerkarte **Replikationsdetail** des Replikationslinks aus.  

Weitere Informationen zum Überwachen der Datenbankreplikation, u. a. zum Anzeigen des Replikationsstatus, finden Sie unter [Überwachen der Datenbankreplikation](../../servers/manage/monitor-replication.md).  


## <a name="site-database-replication-controls"></a><a name="BKMK_DBRepControls"></a> Steuerelemente für die Replikation von Standortdatenbanken  

Ändern Sie die Einstellungen für jede Standortdatenbank, damit Sie die für die Datenbankreplikation verwendete Netzwerkbandbreite steuern können. Die Einstellungen gelten nur für die Standortdatenbank, in der Sie die Einstellungen konfigurieren. Die Einstellungen kommen immer dann zur Anwendung, wenn der Standort beliebige Daten mithilfe von Datenbankreplikation auf jeden anderen Standort repliziert.  

Folgende Steuerelemente können Sie für jede Datenbank ändern:  

- SSB-Port  

- Hiermit konfigurieren Sie den Zeitraum, nach dessen Ablauf der Standort aufgrund von Replikationsfehlern dazu veranlasst wird, seine Kopie der Standortdatenbank neu zu initiieren.  

- Komprimieren Sie die Daten, die von einem Standort repliziert werden. Sie werden nur für die Übertragung zwischen Standorten komprimiert, nicht aber für die Speicherung in den Standortdatenbanken der Standorte.  

Zum Ändern der Einstellungen der Replikationssteuerelemente für eine Standortdatenbank müssen Sie die Eigenschaften der Standortdatenbank in der Configuration Manager-Konsole über den Knoten **Datenbankreplikation** bearbeiten. Dieser Knoten befindet sich unter dem Knoten **Hierarchiekonfiguration** im Arbeitsbereich **Verwaltung** sowie im Arbeitsbereich **Überwachung**. Zur Bearbeitung der Eigenschaften der Standortdatenbank wählen Sie den Replikationslink zwischen den Standorten aus und öffnen dann entweder **Eigenschaften der übergeordneten Datenbank** oder **Eigenschaften der untergeordneten Datenbank**.  

> [!TIP]  
> In beiden Arbeitsbereichen können Sie Steuerelemente für die Datenbankreplikation über den Knoten **Datenbankreplikation** konfigurieren. Wenn Sie aber den Knoten **Datenbankreplikation** im Arbeitsbereich **Überwachung** verwenden, können Sie auch den Status der Datenbankreplikation für einen Replikationslink anzeigen. Außerdem haben Sie Zugriff auf die Replikationslinkanalyse, mit der Sie Probleme bei der Replikation untersuchen können.  


## <a name="see-also"></a>Weitere Informationen:

[Überwachen der Replikation](../../servers/manage/monitor-replication.md)

[Problembehandlung der SQL-Replikation](../../servers/manage/replication/overview.md)
