---
title: Überwachen der Datenbankreplikation
titleSuffix: Configuration Manager
description: Hier erfahren Sie, wie Sie die SQL Server-Replikation in Ihrer Configuration Manager-Hierarchie überwachen.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 69550b35-bcdb-4b47-bbec-b3c8bc92bb7b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4a9ae791582911f91e5f76b841248ad5085d8170
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83879817"
---
# <a name="monitor-database-replication"></a>Überwachen der Datenbankreplikation

*Gilt für: Configuration Manager (Current Branch)*

Sie können Details zur Datenbankreplikation in der Configuration Manager-Konsole über den Knoten **Datenbankreplikation** im Arbeitsbereich **Überwachung** überwachen. Sie können den Status von Replikationslinks zwischen Standorten überwachen. Außerdem werden die Initialisierung und Replikation von Replikationsgruppen für den Standort angezeigt, mit dem Sie eine Verbindung herstellen.  

> [!TIP]  
> Obwohl auch im Arbeitsbereich **Verwaltung** unter dem Knoten **Hierarchiekonfiguration** der Knoten **Datenbankreplikation** vorhanden ist, können Sie sich den Replikationsstatus für Datenbankreplikationslinks von diesem Ort aus nicht anzeigen lassen.  

## <a name="replication-link-status"></a><a name="BKMK_MonitorReplicationLinks"></a> Replikationslinkstatus  

Bei der Datenbankreplikation zwischen Standorten werden mehrere Informationssätze, genannt *Replikationsgruppen*, repliziert. Jede Replikationsgruppe sendet und empfängt Daten mit unterschiedlichen Prioritäten. Standardmäßig können weder die in einer Replikationsgruppe enthaltenen Daten noch die Replikationshäufigkeit geändert werden.  

Wenn ein Replikationslink aktiv ist und sein Status nicht fehlerhaft oder heruntergestuft ist, werden alle Gruppen schnell repliziert. Wenn die Replikation einer oder mehrerer Replikationsgruppen nicht innerhalb des erwarteten Zeitraums abgeschlossen wird, dann wird der Link als *Heruntergestuft* angezeigt. Heruntergestufte Links können weiterhin funktionieren, Sie sollten sie jedoch überwachen, um sicherzustellen, dass sie in den aktiven Status zurückkehren. Untersuchen Sie sie, um sicherzustellen, dass keine weitere Herabstufung oder Replikationsfehler auftreten.  

Geben Sie für jeden Replikationslink an, wie oft das Replizieren einer Gruppe bei einem Fehler wiederholt werden soll. Nach der angegebenen Anzahl von Wiederholungen legt der Standort den Status des Links auf eine Herabstufung oder einen Fehler fest. Dies ist auch der Fall, wenn alle Gruppen bis auf eine erfolgreich repliziert wurden. Dieser Status wird festgelegt, weil eine Replikationsgruppe die Replikation nicht mit der angegebenen Anzahl von Versuchen abschließen kann. Weitere Informationen finden Sie unter [Database replication thresholds (Schwellenwerte für die Datenbankreplikation)](../../plan-design/hierarchy/database-replication.md#BKMK_DBRepThresholds).  

Anhand der folgenden Informationen können Sie den Status von Replikationslinks nachvollziehen und entscheiden, ob weitere Überprüfungen erforderlich sind:  

### <a name="link-is-active"></a>Link ist aktiv

Es wurden keine Probleme erkannt, und die Kommunikation über den Link ist aktuell.

Wenn Sie während des Upgrades eines übergeordneten Standorts auf eine neue Version den Linkstatus des untergeordneten Standorts anzeigen, wird dieser als aktiv angezeigt. Nach dem Update, bis der untergeordnete Standort dieselbe Version wie der übergeordnete Standort aufweist, wird der Linkstatus vom übergeordneten Standort aus betrachtet als aktiv angezeigt. Vom untergeordneten Standort aus wird angezeigt, dass er gerade konfiguriert wird.  

### <a name="link-is-degraded"></a>Link heruntergestuft

Die Replikation ist funktionsfähig, aber es kam bei mindestens einem Replikationsobjekt oder einer Replikationsgruppe zu Verzögerungen. Überwachen Sie Links mit diesem Status. Überprüfen Sie Informationen von beiden beteiligten Standorten auf Hinweise, dass bei diesem Link ein Fehler auftreten könnte.

Von einem Link kann der Status Herabgestuftauch dann angezeigt werden, wenn vom Standort, von dem replizierte Daten empfangen wurden, diese nicht schnell an die Datenbank übergeben werden können. Dies kann geschehen, wenn große Mengen an Daten repliziert werden. Dies ist z. B. der Fall, wenn Sie ein Softwareupdate auf einer großen Anzahl von Computern bereitstellen. Es kann einige Zeit dauern, bis der übergeordnete Standort in dem Link diese Menge an replizierten Daten verarbeitet hat. Ein Verarbeitungsstau am übergeordneten Standort kann dazu führen, dass der Linkstatus auf „Herabgestuft“ gesetzt wird, bis der Datenrückstand erfolgreich verarbeitet werden kann.

### <a name="link-has-failed"></a>Fehler bei Link

Die Replikation ist nicht funktionsfähig. Eine spontane Wiederherstellung des Replikationslinks ohne weitere Aktion ist möglich. Verwenden Sie die Replikationslinkanalyse (RLA), um den Link zu überprüfen und die Replikationsprobleme zu beheben.

Mit diesem Status kann auch ein Problem mit dem physischen Netzwerk zwischen dem übergeordneten und dem untergeordneten Standort des Replikationslinks aufgezeigt werden.


## <a name="monitor-replication-status"></a><a name="BKMK_MonitorReplicationStatus"></a> Überwachen des Replikationsstatus

Mit dem Knoten **Datenbankreplikation** im Arbeitsbereich **Überwachung** können Sie den Status eines Replikationslinks anzeigen. Sie können Details zur Datenbank an den Standorten an beiden Enden des Replikationslinks anzeigen. Sie können auch Details zu Replikationsgruppen anzeigen lassen. Für das Anzeigen dieser Details wählen Sie einen Replikationslink und anschließend die entsprechende Registerkarte für den Replikationsstatus aus, der angezeigt werden soll.

Im folgenden Abschnitt finden Sie Details zu den verschiedenen Registerkarten für den Replikationsstatus:

### <a name="summary"></a>Zusammenfassung

Hier finden Sie wichtige Informationen zur Replikation von Standortdaten und globalen Daten zwischen zwei Standorten über einen Link.  

Wählen Sie **Berichte für Verkehrsverlaufsdaten anzeigen** aus, um einen Bericht mit Details zur Netzwerkbandbreite anzuzeigen, die zur Replikation über den Replikationslink verwendet wird.  

### <a name="parent-site"></a>Übergeordneter Standort

Für den übergeordneten Standort auf einem Replikationslink können Sie Details zur Datenbank anzeigen, darunter auch:  

- Firewallports für den SQL Server  

- Freier Speicherplatz  

- Datenbank-Dateispeicherorte  

- Zertifikate  

### <a name="child-site"></a>Untergeordneter Standort

Für den untergeordneten Standort auf einem Replikationslink können Sie sich Details zur Datenbank anzeigen, darunter auch:  

- Firewallports für den SQL Server  

- Freier Speicherplatz  

- Datenbank-Dateispeicherorte  

- Zertifikate  

### <a name="initialization-detail"></a>Initialisierungsdetail

Hiermit können Sie den Initialisierungsstatus für Replikationsgruppen anzeigen, die über den Replikationslink repliziert werden. Anhand dieser Informationen können Sie ermitteln, wann die Initialisierung der Replikationsdaten durchgeführt wird oder fehlgeschlagen ist.  

Sie können diese Informationen nutzen, um zu ermitteln, wann ein Standort sich im *Interoperabilitätsmodus* befindet. Der Interoperabilitätsmodus bedeutet, dass vom untergeordneten Standort nicht dieselbe Version von Configuration Manager wie vom übergeordneten Standort ausgeführt wird.  

### <a name="replication-detail"></a>Replikationsdetail

Hiermit können Sie den Replikationsstatus für jede Replikationsgruppe anzeigen, die über den Link repliziert wird. Anhand dieser Informationen können Sie Probleme oder Verzögerungen bei der Replikation bestimmter Daten identifizieren. Außerdem können hiermit geeignete Schwellenwerte für die Datenbankreplikation für diesen Link festgelegt werden. Weitere Informationen finden Sie unter [Database replication thresholds (Schwellenwerte für die Datenbankreplikation)](../../plan-design/hierarchy/database-replication.md#BKMK_DBRepThresholds).  

> [!TIP]  
> Replikationsgruppen für Standortdaten werden nur vom untergeordneten Standort an den übergeordneten Standort versendet. Replikationsgruppen für globale Daten werden in beide Richtungen repliziert.  


## <a name="replication-link-analyzer"></a><a name="BKMK_RLA"></a> Replikationslinkanalyse

Configuration Manager schließt die **Replikationslinkanalyse** (RLA) ein, die Sie zum Analysieren und Beheben von Replikationsproblemen verwenden können. Mit RLA können Sie Linkfehler beheben, die bei der Replikation auftreten. Sie ist außerdem hilfreich, wenn die Replikation nicht mehr funktioniert, der Standort jedoch noch keinen Fehler gemeldet hat.

Verwenden Sie RLA, um Replikationsprobleme zwischen den folgenden Computern in der Hierarchie zu beheben:  

- Zwischen einem Standortserver und dem Standortdatenbankserver  

- Zwischen dem Datenbankserver eines Standorts und dem Datenbankserver eines anderen Standorts (Replikation zwischen Standorten)  

> [!Note]  
> Die Richtung des Replikationsfehlers spielt keine Rolle.

Sie können RLA entweder mithilfe der Configuration Manager-Konsole oder über eine Eingabeaufforderung ausführen:  

- Ausführung in der Configuration Manager-Konsole: Navigieren Sie zum Arbeitsbereich **Überwachung**, und wählen Sie den Knoten **Datenbankreplikation** aus. Wählen Sie den Replikationslink aus, den Sie analysieren möchten, und wählen Sie dann im Menüband **Replikationslinkanalyse** aus.  

- Geben Sie an einer Eingabeaufforderung den folgenden Befehl ein: `%ProgramFiles(x86)%\Microsoft Endpoint Manager\AdminConsole\bin\Microsoft.ConfigurationManager.ReplicationLinkAnalyzer.Wizard.exe <source site server FQDN> <destination site server FQDN>`  

    > [!IMPORTANT]
    > Ab Version 1910 wurde dieser Pfad so geändert, dass der `Microsoft Endpoint Manager`-Ordner verwendet wird. Stellen Sie sicher, dass Sie keine ältere Version der Datei verwenden, die möglicherweise in einem anderen Ordner vorhanden ist.

Wenn Sie RLA ausführen, werden mithilfe mehrerer Diagnoseregeln und Prüfungen Probleme erkannt. Anschließend werden die Probleme angezeigt, die vom Tool ermittelt werden. Wenn eine Anleitung zum Beheben eines Problems vorliegt, wird diese angezeigt. Wenn RLA ein Problem automatisch beheben kann, wird diese Option angezeigt.

Bei Abschluss der Replikationslinkanalyse werden die Ergebnisse im folgenden XML-basierten Bericht sowie in der folgenden Protokolldatei auf dem Desktop des Benutzers angezeigt, der das Tool ausgeführt hat:  

- ReplicationAnalysis.xml  

- ReplicationLinkAnalysis.log  

RLA beendet die folgenden Dienste, während Probleme behoben werden. Diese Dienste werden nach Abschluss der Wiederherstellung neu gestartet:  

- SMS_SITE_COMPONENT_MANAGER  

- SMS_EXECUTIVE  

Wenn die Wiederherstellung durch RLA nicht durchgeführt werden kann, starten Sie diese Dienste ggf. auf dem Standortserver neu.  

RLA protokolliert alle Untersuchungs- und Wiederherstellungsaktionen, um zusätzliche Informationen bereitzustellen, die nicht im Assistenten angezeigt werden.  

### <a name="rla-prerequisites"></a>Voraussetzungen für RLA

Das Konto, mit dem Sie RLA ausführen, muss über folgende Berechtigungen verfügen:

- Lokale Administratorrechte auf jedem Computer, der am Replikationslink beteiligt ist.

- Systemadministratorrechte für jede SQL Server-Datenbank, die am Replikationslink beteiligt ist.  

> [!Note]  
> Für das Konto ist keine bestimmte rollenbasierte Configuration Manager-Verwaltungssicherheitsrolle erforderlich. Ein Administrator mit Zugriff auf den Knoten **Datenbankreplikation** kann das Tool in der Configuration Manager-Konsole ausführen. Ein Systemadministrator mit ausreichenden Rechten für jeden Computer kann das Tool an einer Eingabeaufforderung ausführen.  

### <a name="rla-known-issue"></a>Bekannte Probleme mit RLA

RLA generiert SSB-Zertifikatfehler (SQL Server Service Broker) für primäre Standorte, die von System Center 2012 Configuration Manager aktualisiert wurden. Dies ist auf Änderungen bei den Namen der Zertifikate im aktuellen Configuration Manager-Branch zurückzuführen. Sie können diese Fehler ignorieren.  


## <a name="monitoring-database-replication"></a><a name="BKMK_ProcsforMonitoringReplication"></a> Überwachen der Datenbankreplikation  

### <a name="monitor-high-level-site-to-site-database-replication-status"></a>Überwachen des allgemeinen Datenbankreplikationsstatus zwischen Standorten

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Überwachung**.  

2. Wählen Sie den Knoten **Standorthierarchie** aus, um die Ansicht **Hierarchiediagramm** zu öffnen.  

3. Halten Sie den Mauszeiger auf die Linie zwischen den beiden Standorten. Der Status der Replikation von globalen und Standortdaten für diese Standorte wird angezeigt.  

### <a name="monitor-the-status-of-a-replication-link"></a>Überwachen des Status eines Replikationslinks

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Überwachung**.  

2. Wählen Sie den Knoten **Datenbankreplikation** aus, und wählen Sie dann den zu überwachenden Replikationslink aus. Wählen Sie anschließend die entsprechende Registerkarte aus, um sich die verschiedenen Details zum Replikationsstatus für diesen Link anzeigen zu lassen.  
