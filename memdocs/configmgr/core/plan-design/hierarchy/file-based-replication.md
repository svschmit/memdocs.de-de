---
title: dateibasierte Replikation
titleSuffix: Configuration Manager
description: Hier erfahren Sie, wie mithilfe der dateibasierten Replikation dateibasierte Daten von Configuration Manager zwischen den Standorten in Ihrer Hierarchie übertragen werden.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 65fcc1a8-214e-4dd9-8093-de4cd4a00442
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b7d7f1564057a7a942fc4a32064eb54cdbfa890d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703558"
---
# <a name="file-based-replication"></a>dateibasierte Replikation

*Gilt für: Configuration Manager (Current Branch)*

Mithilfe der dateibasierten Replikation werden dateibasierte Daten von Configuration Manager zwischen den Standorten in Ihrer Hierarchie übertragen. Zu diesen Daten zählen Anwendungen und Pakete, die Sie an Verteilungspunkten in untergeordneten Standorten bereitstellen möchten. Dazu gehören auch nicht verarbeitete Ermittlungsdatensätze, die an übergeordnete Standorte übertragen und anschließend verarbeitet werden.  

Bei der dateibasierten Kommunikation zwischen Standorten wird das *Server Message Block*-Protokoll (SMB) über TCP/IP-Port 445 verwendet. Geben Sie Bandbreiteneinschränkungen und Pulsmodus an, um die Menge der vom Standort über das Netzwerk übertragenen Daten zu steuern. Mithilfe von Zeitplänen können Sie steuern, wann Daten über das Netzwerk gesendet werden sollen.  

## <a name="routes"></a><a name="bkmk_routes"></a> Routen

Die folgenden Informationen unterstützen Sie beim Einrichten und Verwendung von Dateireplikationsrouten:  

### <a name="file-replication-route"></a>Dateireplikationsroute

Von jeder Dateireplikationsroute wird ein Zielstandort identifiziert, an den dateibasierte Daten übertragen werden. Von jedem Standort wird eine Dateireplikationsroute zu einem bestimmten Zielstandort unterstützt.  

Wechseln Sie zum Verwalten einer Dateireplikationsroute zum Arbeitsbereich **Verwaltung**. Erweitern Sie den Knoten **Hierarchiekonfiguration**, und wählen Sie dann **Dateireplikation** aus.  

Folgende Einstellungen können Sie für Dateinreplikationsrouten ändern:  

#### <a name="file-replication-account"></a>Dateireplikationskonto

Dieses Konto stellt eine Verbindung mit dem Zielstandort her und schreibt Daten in die **SMS_Site**-Freigabe dieses Standorts. Der empfangende Standort verarbeitet auf diese Freigabe geschriebene Daten. Wenn Sie der Hierarchie einen Standort hinzufügen, weist Configuration Manager standardmäßig das Computerkonto des neuen Standortservers als sein Dateireplikationskonto zu. Anschließend wird dieses Konto der Gruppe `SMS_SiteToSiteConnection_<sitecode>` des Zielstandorts hinzugefügt. Diese Gruppe ist eine lokale Gruppe auf dem Computer, der den Zugriff auf die SMS_SITE-Freigabe gewährt. Sie können dieses Konto in ein Windows-Benutzerkonto ändern. Wenn Sie das Konto ändern, achten Sie darauf, das neue Konto der Gruppe `SMS_SiteToSiteConnection_<sitecode>` des Zielstandorts hinzuzufügen.  

> [!NOTE]  
> An sekundären Standorten wird stets das Computerkonto des sekundären Standortservers als **Dateireplikationskonto**verwendet.  

#### <a name="schedule"></a>Zeitplan

Legen Sie den Zeitplan für jede Dateireplikationsroute fest. Hiermit werden der Datentyp und der Zeitraum eingeschränkt, in dem Daten an den Zielstandort übertragen werden können.  

#### <a name="rate-limits"></a>Begrenzung der Datenübertragungsrate

Legen Sie Datenratenlimits für jede Dateireplikationsroute fest. Hiermit wird die Netzwerkbandbreite gesteuert, die der Standort für die Datenübertragung an den Zielstandort verwendet:  

- **Pulsmodus:** Hiermit geben Sie die Größe der Datenblöcke an, die vom Standort an den Zielstandort gesendet werden. Sie können auch eine zeitliche Verzögerung zwischen dem Senden der einzelnen Datenblöcke angeben. Wählen Sie diese Option aus, wenn Sie Daten über Netzwerke mit niedriger Bandbreite an den Zielstandort senden müssen.

    Dies kann beispielsweise der Fall sein, wenn eine Beschränkung vorliegt, dass zu einem bestimmten Zeitpunkt nur alle fünf Sekunden 1 KB Daten gesendet werden dürfen und nicht alle drei Sekunden. Diese Einschränkung gilt unabhängig von der Geschwindigkeit des Links oder der Auslastung zu einem bestimmten Zeitpunkt.

- **Begrenzt auf angegebene maximale Übertragungsraten pro Stunde:** Der Standort sendet Daten an einen Zielstandort, wobei nur die angegebene prozentuale Zeit maßgebend ist. Configuration Manager ermittelt die verfügbare Netzwerkbandbreite nicht. Stattdessen wird die Zeit, während der Daten gesendet werden können, in Abschnitte aufgeteilt. Die Daten werden dann innerhalb eines kurzen Zeitblocks gesendet. In den darauf folgenden Zeitblöcken werden keine Daten gesendet.

    Legen Sie die maximale Rate beispielsweise auf **50 %** fest. Configuration Manager überträgt Daten für eine bestimmte Dauer, und für eine ebenso lange Dauer werden anschließend keine Daten übertragen. Die tatsächliche Datenmenge bzw. die Größe der Datenblöcke wird nicht verwaltet. Der Standort verwaltet nur die Zeitspanne, während der Daten gesendet werden.  

    > [!CAUTION]  
    > Von einem Standort können standardmäßig bis zu 3 **gleichzeitige Sendevorgänge** zur Datenübertragung an einen Zielstandort verwendet werden. Wenn Sie für eine Dateireplikationsroute die Begrenzung der Datenübertragungsroute aktivieren, ist die Anzahl **gleichzeitiger Sendevorgänge** an den entsprechenden Standort auf 1 begrenzt. Dieses Verhalten gilt auch dann, wenn für die Option **Verfügbare Bandbreite beschränken (%)** der Wert **100 %** festgelegt wurde. Wenn Sie beispielsweise für den Sender die Standardeinstellungen verwenden, wird hierdurch die Übertragungsrate an den Zielstandort auf ein Drittel der Standardkapazität reduziert.  

#### <a name="routes-between-secondary-sites"></a>Routen zwischen sekundären Standorten

Konfigurieren Sie eine Dateireplikationsroute zwischen zwei sekundären Standorten zum Weiterleiten dateibasierter Inhalte zwischen diesen Standorten.  


### <a name="sender"></a>Sender

An jedem Standort ist ein Sender verfügbar. Der Sender verwaltet die Netzwerkverbindung zwischen einem Standort und einem Zielstandort. Es können gleichzeitig Verbindungen mit mehreren Standorten hergestellt werden. Zum Herstellen einer Verbindung mit einem Standort wird vom Sender mithilfe der Dateireplikationsroute zum Standort das Konto identifiziert, über das die Verbindungsherstellung erfolgt. Dieses Konto wird vom Sender auch dazu verwendet, Daten in die „SMS_Site“-Freigabe des Zielstandorts zu schreiben.  

Vom Sender werden Daten standardmäßig mithilfe von **gleichzeitigen Sendevorgängen** oder eines *Threads* in den Zielstandort geschrieben. Von jedem Thread kann ein anderes dateibasiertes Objekt an den Zielstandort übertragen werden. Nachdem der Sendevorgang für ein Objekt gestartet wurde, werden vom Sender so lange Datenblöcke für dieses Objekt geschrieben, bis die Übertragung des gesamten Objekts abgeschlossen ist. Anschließend kann der Sendevorgang über diesen Thread für ein weiteres Objekt gestartet werden.  

Wenn Sie den Absender für einen Standort verwalten möchten, wechseln Sie zum Arbeitsbereich **Verwaltung**, und erweitern Sie den Knoten **Standortkonfiguration**. Wählen Sie den Knoten **Standorte** aus, und wählen Sie für den zu verwaltenden Standort **Eigenschaften** aus. Wechseln Sie zur Registerkarte **Sender**, um die Sendereinstellungen zu ändern.  

Sie können die folgenden Einstellungen für einen Sender ändern:  

#### <a name="maximum-concurrent-sendings"></a>Maximale Anzahl gleichzeitiger Sendevorgänge

Standardmäßig werden von jedem Standort fünf gleichzeitige Sendevorgänge (Threads) verwendet. Drei Threads stehen zur Verfügung, wenn Daten an einen Zielstandort gesendet werden. Wenn Sie diese Anzahl erhöhen, nimmt der Datendurchsatz zwischen Standorten zu. Mehr Threads bedeuten, dass Configuration Manager mehr Dateien gleichzeitig übertragen kann. Die Erhöhung dieser Anzahl bedeutet auch höhere Anforderungen an die Netzwerkbandbreite zwischen Standorten.  

#### <a name="retry-settings"></a>Wiederholungseinstellungen

Standardmäßig wiederholt jeder Standort die Herstellung einer problematischen Verbindung zweimal im Abstand von einer Minute. Sie können sowohl die Anzahl der Verbindungsversuche als auch deren Abstand ändern.  


## <a name="next-steps"></a>Nächste Schritte

[Database replication](database-replication.md)
