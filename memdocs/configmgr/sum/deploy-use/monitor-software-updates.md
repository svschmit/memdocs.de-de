---
title: Überwachen von Softwareupdates
titleSuffix: Configuration Manager
description: Die Configuration Manager-Konsole stellt Warnungen und Status zum Überwachen von Updates und Konformität bereit.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/21/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 9afd7b0f-5c8e-48bc-9a65-1f7d74103688
ms.openlocfilehash: aa17e58f2687a48895502d1062a22d0c8630aea3
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110371"
---
# <a name="monitor-software-updates-in-configuration-manager"></a>Überwachen von Softwareupdates in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

In der Configuration Manager-Konsole stehen viele Hilfsmittel zur Überwachung von Objekten, Prozessen und Kompatibilitätsinformationen im Zusammenhang mit Softwareupdates zur Verfügung. Verwenden Sie die folgenden Bereiche, um Softwareupdates zu überwachen.

## <a name="software-updates-dashboard"></a>Dashboard „Softwareupdatepunkt“

*(Eingeführt in Version 1610)*

Ab Version 1610 von Configuration Manager können Sie jetzt das Dashboard „Softwareupdatepunkt“ verwenden, um den aktuellen Konformitätsstatus von Geräten in Ihrer Organisation anzuzeigen, und schnell Daten analysieren, um anzuzeigen, welche Geräte gefährdet sind. Navigieren Sie zum Anzeigen des Dashboards zu **Überwachung** > **Überblick** > **Sicherheit** > **Software Updates Dashboard** (Dashboard „Softwareupdatepunkt“).

## <a name="drill-through-required-updates"></a>Ausführen eines Drillthrough durch erforderliche Updates
<!--4224414-->
*(Eingeführt in Version 1906)*

Sie können einen Drillthrough durch die Konformitätsstatistiken durchführen, um herauszufinden, auf welchen Geräten ein bestimmtes Softwareupdate für Microsoft 365-Apps erforderlich ist. Sie benötigen zum Abrufen der Geräteliste die Berechtigung, Updates und die jeweiligen Sammlungen abzurufen, zu denen die Geräte gehören. Gehen Sie wie folgt vor, um einen Drilldown in der Geräteliste auszuführen:

1. Wechseln Sie zu **Softwarebibliothek** > **Softwareupdates** > **Alle Softwareupdates**.
1. Wählen Sie ein beliebiges Update aus, das für mindestens ein Gerät erforderlich ist.
1. Öffnen Sie die Registerkarte **Zusammenfassung**, und sehen Sie sich das Kreisdiagramm unter **Statistiken** an.
1. Klicken Sie auf der rechten Seite neben dem Kreisdiagramm auf den Link **Erforderliche anzeigen**, um einen Drilldown für die Geräteliste auszuführen.
1. Über diese Aktion gelangen Sie unter **Geräte** zu einem temporären Knoten, unter dem die Geräte angezeigt werden, für die das Update erforderlich ist. Außerdem können Sie Aktionen für den Knoten ausführen, z. B. können Sie eine neue Sammlung aus der Liste erstellen.


##  <a name="alerts-for-software-updates"></a><a name="BKMK_SUAlerts"></a> Warnungen zu Softwareupdates  
 Sie können Warnungen zu Softwareupdates konfigurieren, mit denen Administratoren benachrichtigt werden, wenn die Konformitätsstufen von Softwareupdatebereitstellungen unter dem konfigurierten Prozentsatz liegen. Sie können Warnungen zu Softwareupdatebereitstellungen an den folgenden Stellen konfigurieren:  

-   ADR-Einstellung: Sie können die Warnungseinstellungen im Assistenten zum Erstellen von Regeln für die automatische Bereitstellung und in den ADR-Eigenschaften (Automatic Deployment Rule, ADR) konfigurieren.  

-   Einstellung der Bereitstellung: Sie können die Warnungseinstellungen im Assistenten zum Bereitstellen von Softwareupdates und in den Bereitstellungseigenschaften konfigurieren.  

Nachdem Sie die Warnungseinstellungen konfiguriert haben, wird von Configuration Manager eine Warnung ausgegeben, wenn die angegebenen Bedingungen erfüllt sind. Sie können die Warnungen zu Softwareupdates an den folgenden Stellen prüfen:  

1.  Prüfen Sie die letzten Warnungen im Arbeitsbereich **Softwarebibliothek** im Knoten **Softwareupdates** .  

2.  Verwalten Sie die konfigurierten Warnungen im Arbeitsbereich **Überwachung** im Knoten **Warnungen** .  

##  <a name="software-updates-synchronization-status"></a><a name="BKMK_SUSyncStatus"></a> Status der Softwareupdatesynchronisierung  
 Nach dem Start der Synchronisierung können Sie den Synchronisierungsprozess in der Configuration Manager-Konsole für alle Softwareupdatepunkte in der Hierarchie überwachen. Gehen Sie wie folgt vor, um die Softwareupdatesynchronisierung zu überwachen.  

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>So überwachen Sie die Softwareupdatesynchronisierung  

- Wechseln Sie in der Configuration Manager-Konsole zu **Überwachung** > **Übersicht** > **Synchronisierungsstatus der Softwareupdatepunkte**.  

    Die Softwareupdatepunkte in der Configuration Manager-Hierarchie werden im Ergebnisbereich angezeigt. Von hier können Sie den Synchronisierungsstatus aller Softwareupdatepunkte überwachen. Ausführlichere Informationen zum Synchronisierungsprozess enthält die Datei „wsyncmgr.log“, die sich auf jedem Standortserver unter <*ConfigMgr-Installationspfad*>\Logs befindet.  

##  <a name="software-update-deployment-status"></a><a name="BKMK_SUDeployStatus"></a> Status der Softwareupdatebereitstellung  
 Nach der Bereitstellung der Softwareupdates in einer Softwareupdategruppe bzw. nach der Bereitstellung eines einzelnen Softwareupdates können Sie den Bereitstellungsstatus überwachen. Gehen Sie wie folgt vor, um den Bereitstellungsstatus einer Softwareupdategruppe oder eines Softwareupdates zu überwachen.  

#### <a name="to-monitor-deployment-status"></a>So überwachen Sie den Bereitstellungsstatus  

1.  Wechseln Sie in der Configuration Manager-Konsole zu **Überwachung** > **Übersicht** > **Bereitstellungen**.  

2.  Klicken Sie auf die Softwareupdategruppe oder das Softwareupdate, dessen Bereitstellungsstatus Sie überwachen möchten.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Status anzeigen**.  

##  <a name="software-updates-reports"></a><a name="BKMK_SUReports"></a> Softwareupdateberichte  
 Die Zustandsmeldungen zu Softwareupdates enthalten Informationen zur Konformität von Softwareupdates sowie zu Bewertung und Erzwingungszustand von Softwareupdatebereitstellungen. Zum Anzeigen der Zustandsmeldungen können Sie Softwareupdateberichte ausführen. Mehr als 30 vordefinierte Softwareupdateberichte sind verfügbar. Sie sind in verschiedene Kategorien unterteilt und können dazu verwendet werden, Informationen zu bestimmten Aspekten von Softwareupdates und -bereitstellungen zu liefern. Zusätzlich zu den vorkonfigurierten Berichten können Sie auch benutzerdefinierte Softwareupdateberichte erstellen, die auf die Anforderungen Ihres Unternehmens zugeschnitten sind. Weitere Informationen finden Sie unter [Vorgänge und Wartungstasks für die Berichterstellung](../../core/servers/manage/operations-and-maintenance-for-reporting.md).  

### <a name="recommended-software-updates-reports"></a>Empfohlene Softwareupdateberichte
Im Folgenden finden Sie einige Berichte, die beim Identifizieren von potenziellen Problemen hilfreich sind: 

#### <a name="compliance-9---overall-health-and-compliance-starting-in-version-1806"></a>Konformität 9: Gesamtintegrität und -konformität (ab Version 1806)
Der Bericht enthält die folgenden Teile:

- **„Fehlerlose Clients“ im Vergleich zu „Gesamtzahl Clients“:** In diesem Balkendiagramm werden die „fehlerlosen“ Clients, die im angegebenen Zeitraum mit dem Standort kommuniziert haben, mit der Gesamtanzahl der Clients in der angegebenen Sammlung verglichen.
- **Konformitätsübersicht:** Dieses Tortendiagramm zeigt den gesamten Konformitätszustand für die jeweilige Softwareupdategruppe auf aktiven Clients in der angegebenen Sammlung an.
- **Wichtigste 5 nicht konforme nach Artikel-ID:** Dieses Balkendiagramm zeigt die fünf wichtigsten Softwareupdates in der angegebenen Gruppe an, die auf aktiven Clients in der angegebenen Sammlung nicht konform sind.
- Der untere Rand des Berichts ist eine Tabelle mit zusätzlichen Informationen, in der die Softwareupdates in der angegebenen Gruppe aufgeführt sind.

#### <a name="management-2---updates-required-but-not-deployed"></a>Verwaltung 2 – Erforderliche, aber nicht bereitgestellte Updates

In diesem Bericht werden alle herstellerspezifischen Softwareupdates in einer bestimmten Klassifizierung für Updates angezeigt, die auf Clients als erforderlich ermittelt, jedoch nicht für eine bestimmte Sammlung bereitgestellt wurden. 

#### <a name="troubleshooting-2---deployment-errors"></a>Problembehandlung 2 – Bereitstellungsfehler

In diesem Bericht werden die Bereitstellungsfehler am Standort sowie die Anzahl der von den einzelnen Fehlern betroffenen Computer angegeben. 


##  <a name="monitor-content"></a><a name="BKMK_MonitorContent"></a> Überwachen von Inhalt  
 Sie können den Inhalt in der Configuration Manager-Konsole überwachen, und so den Status aller Pakettypen im Zusammenhang mit den zugeordneten Verteilungspunkten prüfen. Dies kann den Inhaltsprüfungsstatus des Paketinhalts, den Status von Inhalt, der einer bestimmten Verteilungspunktgruppe zugeordnet ist, den Zustand von Inhalt, der einem Verteilungspunkt zugeordnet ist, und den Status optionaler Funktionen jedes Verteilungspunkts (Inhaltsprüfung, PXE und Multicast) umfassen.  

###  <a name="content-status-monitoring"></a><a name="BKMK_ContentStatus"></a> Überwachung des Inhaltsstatus  
 Im Arbeitsbereich **Überwachung** finden Sie im Knoten **Inhaltsstatus** Informationen zu Inhaltspaketen. Sie können allgemeine Informationen zum Paket, den Verteilungsstatus des Pakets sowie detaillierte Statusinformationen zum Paket prüfen. Gehen Sie wie folgt vor, um den Inhaltsstatus anzuzeigen.  

#### <a name="to-monitor-content-status"></a>So überwachen Sie den Inhaltsstatus  

1.  Wechseln Sie in der Configuration Manager-Konsole zu **Überwachung** > **Übersicht** > **Verteilungsstatus** > **Inhaltsstatus**. Die Pakete werden angezeigt.  

2.  Wählen Sie das Paket aus, für das Sie detaillierte Statusinformationen anzeigen möchten.  

3.  Klicken Sie auf der Registerkarte **Startseite** auf **Status anzeigen**. Detaillierte Statusinformationen zum Paket werden angezeigt.  

###  <a name="distribution-point-group-status"></a><a name="BKMK_DPGroupStatus"></a> Status der Verteilungspunktgruppe  
 Im Arbeitsbereich **Überwachung** finden Sie im Knoten **Status der Verteilungspunktgruppe** Informationen zu Verteilungspunktgruppen. Sie können allgemeine Informationen zur Verteilungspunktgruppe, wie beispielsweise den Status der Verteilungspunktgruppe und die Kompatibilitätsstufe, sowie detaillierte Informationen zur Verteilungspunktgruppe anzeigen. Gehen Sie wie folgt vor, um den Status einer Verteilungspunktgruppe anzuzeigen.  

#### <a name="to-monitor-distribution-point-group-status"></a>So überwachen Sie den Status einer Verteilungspunktgruppe  

1.  Wechseln Sie in der Configuration Manager-Konsole zu **Überwachung** > **Übersicht** > **Verteilungsstatus** > **Status der Verteilungspunktgruppe**. Die Verteilungspunktgruppen werden angezeigt.  

2.  Wählen Sie die Verteilungspunktgruppe aus, für die detaillierte Statusinformationen angezeigt werden sollen.  

3.  Klicken Sie auf der Registerkarte **Startseite** auf **Status anzeigen**. Detaillierte Statusinformationen zur Verteilungspunktgruppe werden angezeigt.  

###  <a name="distribution-point-configuration-status"></a><a name="BKMK_DPConfigStatus"></a> Status der Verteilungspunktkonfiguration  
 Im Arbeitsbereich **Überwachung** finden Sie im Knoten **Status der Verteilungspunktkonfiguration** Informationen zum Verteilungspunkt. Sie können prüfen, welche Attribute für den Verteilungspunkt aktiviert sind, wie z. B. PXE, Multicast und Inhaltsprüfung. Außerdem können Sie detaillierte Statusinformationen zum Verteilungspunkt anzeigen. Gehen Sie wie folgt vor, um den Status einer Verteilungspunktkonfiguration anzuzeigen.  

#### <a name="to-monitor-distribution-point-configuration-status"></a>So überwachen Sie den Status einer Verteilungspunktkonfiguration  

1.  Wechseln Sie in der Configuration Manager-Konsole zu **Überwachung** > **Übersicht** > **Verteilungsstatus** > **Status der Verteilungspunktkonfiguration**. Die Verteilungspunkte werden angezeigt.  

2.  Wählen Sie den Verteilungspunkt aus, für den Statusinformationen angezeigt werden sollen.  

3.  Klicken Sie im Ergebnisbereich auf die Registerkarte **Details** . Statusinformationen zum Verteilungspunkt werden angezeigt.  

## <a name="next-steps"></a>Nächste Schritte

- [Protokolldateien für Softwareupdates](../../core/plan-design/hierarchy/log-files.md#BKMK_SU_NAPLog)

- [Whitepaper: Software Updates Management](https://www.microsoft.com/download/confirmation.aspx?id=44578)
