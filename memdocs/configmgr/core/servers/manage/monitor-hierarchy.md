---
title: Überwachen der Hierarchie
titleSuffix: Configuration Manager
description: Hier erfahren Sie, wie Sie die Infrastruktur in Configuration Manager über den Arbeitsbereich „Überwachung“ in der Konsole überwachen.
ms.date: 06/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 007dbb73-18a7-48a3-a489-97cf9fc4f140
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 66fc6744ef7d1aaf90a5e7339cc9a5174c0d33f6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694398"
---
# <a name="monitor-the-hierarchy"></a>Überwachen der Hierarchie

*Gilt für: Configuration Manager (Current Branch)*

Verwenden Sie zum Überwachen der Hierarchie in Configuration Manager den Arbeitsbereich **Überwachung** in der Configuration Manager-Konsole.  

> [!NOTE]  
> Das Migrieren von Standorten stellt eine Ausnahme hierzu dar. Überwachen Sie diesen Vorgang im Knoten **Migration** im Arbeitsbereich **Verwaltung**. Weitere Informationen finden Sie unter [Vorgänge der Migration](../../migration/operations-for-migration.md).  

Verwenden Sie neben der Configuration Manager-Konsole zur Überwachung die folgenden Funktionen:

- [Introduction to reporting (Einführung in die Berichterstellung)](introduction-to-reporting.md)
- [Protokolldateien](../../plan-design/hierarchy/log-files.md)  

Achten Sie beim Überwachen von Standorten auf Anzeichen für Probleme, die Ihren Eingriff erfordern. Beispiel:  

- Dateirückstand auf Standortservern und Standortsystemen  

- Statusmeldungen, die auf einen Fehler oder ein Problem hinweisen  

- Fehlerhafte standortinterne Kommunikation  

- Fehler- und Warnmeldungen im Systemereignisprotokoll auf Servern  

- Fehler- und Warnmeldungen im Fehlerprotokoll von Microsoft SQL Server  

- Standorte oder Clients, die über einen längeren Zeitraum keinen Status gemeldet haben  

- Lange Antwortzeiten der SQL Server-Datenbank  

- Anzeichen für Hardwareausfälle  

Wenn Überwachungsaufgaben auf Probleme hinweisen, untersuchen Sie die Ursache des Problems. Beheben Sie es dann zeitnah, um das Risiko eines Standortausfalls zu minimieren.  


## <a name="monitor-common-management-tasks"></a><a name="BKMK_MonintorMgmtTasks"></a> Überwachen von allgemeinen Verwaltungsaufgaben

Configuration Manager bietet integrierte Überwachungsfunktionen in der Configuration Manager-Konsole.

### <a name="alerts"></a>Warnungen

Weitere Informationen finden Sie unter [Überwachen von Warnungen](use-alerts-and-the-status-system.md#BKMK_MonitorAlerts).  

### <a name="compliance-settings"></a>Kompatibilitätseinstellungen

Weitere Informationen finden Sie unter [How to monitor compliance settings (Überwachen von Kompatibilitätseinstellungen)](../../../compliance/deploy-use/monitor-compliance-settings.md).

### <a name="content"></a>Content

Allgemeine Informationen zur Überwachung von Inhalten finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur für System Center Configuration Manager](../deploy/configure/manage-content-and-content-infrastructure.md).  

Weitere Informationen zum Überwachen bestimmter Typen von Inhalten:

- [Überwachen von Anwendungen](../../../apps/deploy-use/monitor-applications-from-the-console.md)

- [Überwachen von Paketen und Programmen](../../../apps/deploy-use/packages-and-programs.md#monitor-packages-and-programs)  

- [Überwachen von Inhalten für Softwareupdates](../../../sum/deploy-use/monitor-software-updates.md#BKMK_MonitorContent)

- [Überwachen von Inhalten für Betriebssystembereitstellungen](../../../osd/deploy-use/monitor-operating-system-deployments.md#BKMK_MonitorContent)

### <a name="endpoint-protection"></a>Endpoint Protection

Weitere Informationen finden Sie unter [How to monitor Endpoint Protection Status (Überwachen des Endpoint Protection-Status)](../../../protect/deploy-use/monitor-endpoint-protection.md).  

### <a name="os-deployment"></a>Bereitstellung des Betriebssystems

Weitere Informationen finden Sie unter [Überwachen von Betriebssystembereitstellungen in System Center Configuration Manager](../../../osd/deploy-use/monitor-operating-system-deployments.md).

### <a name="monitor-power-management"></a>Überwachen der Energieverwaltung

Weitere Informationen finden Sie unter [How to monitor and plan for power management (Überwachen und Planen der Energieverwaltung in Configuration Manager)](../../clients/manage/power/monitor-and-plan-for-power-management.md).  

### <a name="monitor-software-metering"></a>Überwachen der Softwaremessung

Weitere Informationen finden Sie unter [Monitor app usage with software metering (Überwachen der App-Nutzung mit der Softwaremessung)](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

### <a name="monitor-software-updates"></a>Überwachen von Softwareupdates

Weitere Informationen finden Sie unter [Monitor software updates (Überwachen von Softwareupdates)](../../../sum/deploy-use/monitor-software-updates.md).  


## <a name="monitor-the-site-hierarchy"></a><a name="BKMK_SH_Node"></a> Überwachen der Standorthierarchie

Im Knoten **Standorthierarchie** des Arbeitsbereichs **Überwachung** finden Sie eine Übersicht Ihrer Configuration Manager-Hierarchie sowie Links zwischen Standorten. Sie können zwei Ansichten verwenden:  

- **Hierarchiediagramm:** In dieser Ansicht wird Ihre Hierarchie als vereinfachte Topologiezuordnung angezeigt, in der nur wichtige Informationen dargestellt werden. Weitere Informationen finden Sie unter [Hierarchiediagramm](#hierarchy-diagram).  

- **Geografische Ansicht:** In dieser Ansicht werden Ihre Standorte in einer geografischen Zuordnung angezeigt. Dabei werden die geografischen Orte der von Ihnen konfigurierten Standorte dargestellt. Weitere Informationen finden Sie unter [Geografische Ansicht](#geographical-view).  

Mit dem Knoten **Standorthierarchie** können Sie die Integrität der einzelnen Standorte überwachen. Außerdem können Sie die Replikationslinks zwischen Standorten sowie deren Beziehungen zu externen Faktoren wie einem geografischen Standort überwachen.  

Der Standortstatus und der Status von Links zwischen Standorten werden als Standortdaten und nicht als globale Daten repliziert. Wenn Sie die Configuration Manager-Konsole mit einem untergeordneten primären Standort verbinden, können Sie den Standort- oder Linkstatus weder von anderen primären Standorten noch von deren untergeordneten sekundären Standorten anzeigen. Wenn Sie z. B. in einer Hierarchie mit mehreren primären Standorten die Konsole mit einem primären Standort verbinden, können Sie den Status von untergeordneten sekundären Standorten, des primären Standorts und des Standorts der zentralen Verwaltung anzeigen. In dieser Ansicht wird der Status für andere Standorte nicht unterhalb des Standorts der zentralen Verwaltung angezeigt.  

Die Anzeige im Knoten **Standorthierarchie** wird mit der Aktion **Einstellungen konfigurieren** gesteuert. In der Hierarchie werden die Einstellungen repliziert, die Sie in diesem Knoten konfigurieren.  

### <a name="hierarchy-diagram"></a>Hierarchiediagramm

Im Hierarchiediagramm werden Ihre Standorte als Topologiezuordnung dargestellt. Wählen Sie einen Standort aus, und zeigen Sie eine Zusammenfassung der Statusmeldungen für diesen Standort an. Führen Sie einen Drillthrough durch, um die Statusmeldungen anzuzeigen und auf **Eigenschaften** für den Standort zuzugreifen.  

Wenn Sie den übergeordneten Status für einen Standort oder Replikationslink zwischen Standorten anzeigen möchten, halten Sie den Mauszeiger auf das entsprechende Objekt. Der Status der Linkreplikation wird nicht global repliziert. Um Details zu Replikationslinks zwischen allen primären Standorten in einer Hierarchie anzuzeigen, verbinden Sie die Konsole mit dem Standort der zentralen Verwaltung.  

Mit den folgenden Optionen können Sie das Hierarchiediagramm ändern:  

#### <a name="groups"></a>Gruppen

Sie können die Anzahl von primären und sekundären Standorten konfigurieren, von denen Änderungen in der Anzeige des Hierarchiediagramms ausgelöst werden. Durch diese Änderung der Anzeige werden die Standorte zu einem einzigen Objekt kombiniert. So sehen Sie die Gesamtzahl der Standorte und einen allgemeinen Rollup von Statusnachrichten sowie des Standortstatus. Von Gruppenkonfigurationen wird die geografische Ansicht nicht beeinflusst.  

#### <a name="favorite-sites"></a>Favoriten

Sie können einzelne Standorte als Favoriten angeben. Favoriten sind im Hierarchiediagramm mit einem Sternsymbol gekennzeichnet. Favoritenstandorte werden nicht mit anderen Standorten kombiniert, wenn Sie Gruppen verwenden. Sie werden immer einzeln angezeigt.  

### <a name="geographical-view"></a>Geografische Ansicht

Von der geografischen Ansicht werden Ihre Standorte in einer geografischen Zuordnung angezeigt. Dabei werden nur Standorte angezeigt, die mit einem geografischen Ort konfiguriert sind. Wenn Sie in dieser Ansicht einen Standort auswählen, werden Replikationslinks zu über- und untergeordneten Standorten angezeigt. Im Unterschied zur Hierarchiediagrammansicht können Sie in dieser Ansicht keine Details zu Statusmeldungen und Replikationslinks der Standorte anzeigen.  

> [!NOTE]  
> Wenn Sie die geografische Ansicht verwenden möchten, muss auf dem Computer, mit dem Sie Ihre Configuration Manager-Konsole verbinden, Internet Explorer installiert sein, und ein Zugriff auf Bing Maps mithilfe von HTTP muss möglich sein.  

Mit der folgenden Option können Sie die geografische Ansicht ändern:  

#### <a name="site-location"></a>Ort des Standorts

Geben Sie einen geografischen Ort für jeden Standort an, und verwenden Sie dabei einen der folgenden Typen:

- Straße
- Ortname oder Stadt
- Längen- und Breitengrad

Für die Angabe des Längen- und Breitengrads von Redmond Washington würden Sie beispielsweise **N 47 40 26.3572 W 122 7 17.4432** als Ort des Standorts angeben. Sie müssen die Symbole für Grad, Minuten oder Sekunden der geografischen Länge und Breite nicht angeben. Configuration Manager verwendet Bing Maps, um den Ort als geografische Ansicht anzuzeigen. Anschließend können Sie Ihre Hierarchie anhand der geografischen Standorte anzeigen. Diese Ansicht bietet Einblicke in regionale Probleme, die sich auf bestimmte Standorte oder die standortübergreifende Replikation auswirken können.  

Wenn Sie einen geografischen Ort angeben, können Sie das Feld **Ort** verwenden, um nach einem bestimmten Standort in Ihrer Hierarchie zu suchen. Wenn Sie den Standort ausgewählt haben, geben Sie den Ort als Namen einer Stadt oder als Straßenadresse in die Spalte **Ort** ein. Configuration Manager verwendet Bing Maps zur Auflösung des Orts.  

<a name="BKMK_MonitorRepLinksAndStatuss"></a>

## <a name="next-steps"></a>Nächste Schritte

[Überwachen der Datenbankreplikation](monitor-replication.md)
