---
title: Bewährte Methoden für Sammlungen
titleSuffix: Configuration Manager
description: Hier erhalten Sie Empfehlungen zum Konfigurieren von Sammlungen und zur Sammlungsauswertung in Configuration Manager.
ms.date: 06/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b1bc72a3691e4a6f47c29a5a91ef11c92f0f7e7c
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693283"
---
# <a name="best-practices-for-collections-in-configuration-manager"></a>Bewährte Methoden für Sammlungen in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Einige Anleitungen zur Sammlungsverwaltung können einander widersprechen. Aus Leistungsgründen sollten Sie z. B. die Anzahl der häufig aktualisierten Sammlungen begrenzen. Das häufige Aktualisieren von Sammlungen ist aber praktisch, da die meisten Configuration Manager-Funktionen von Sammlungen abhängig sind. Berücksichtigen Sie beim Entwerfen und Konfigurieren von Sammlungen und Sammlungsauswertung sowohl die Auswirkungen auf die Leistung als auch die geschäftlichen Anforderungen sorgfältig.

Verwenden Sie die folgenden bewährten Methoden für Sammlungen in Configuration Manager.  

## <a name="configure-maintenance-window-for-updates"></a>Konfigurieren des Wartungsfenster für Updates

Durch Wartungsfenster für Gerätesammlungen können Sie festlegen, dass Software nur zu bestimmten Zeiten von Configuration Manager auf diesen Geräten installiert werden kann. Wenn Sie ein zu kleines Wartungsfenster konfigurieren, kann der Client wichtige Softwareupdates möglicherweise nicht installieren, sodass er anfällig ist für Probleme, die durch diese Softwareupdates vermieden würden.

Wichtige Überlegungen bei der Planung der Wartungsfenster:

- Die maximale Standardausführungszeit für Softwareupdates beträgt 60 Minuten.
- Bei der Berechnung, ob ein Update installiert werden kann, fügt Configuration Manager der maximalen Ausführungszeit fünf Minuten für einen möglichen Neustart hinzu.
- Die verbleibende Dauer eines Wartungsfensters muss länger sein als die maximale Ausführungszeit des Softwareupdates plus fünf Minuten.

## <a name="avoid-frequent-collection-evaluation"></a>Vermeiden häufiger Sammlungsauswertungen

Bei einer vollständigen Sammlungsauswertung wird nicht nur die vorgesehene Sammlung ausgewertet, sondern auch alle Sammlungen, die die Sammlung einschränkt, wenn ein Update auftritt. Außerdem wird eine Sammlung ohne Zeitplan noch ausgewertet, wenn die begrenzende Sammlung aktualisiert wird. Es ist also möglich, dass einige Sammlungen häufiger ausgewertet werden als erwartet.

In einer ausgelasteten Configuration Manager-Umgebung können Sie die Leistung der Sammlungsauswertung verbessern, indem Sie Zeitpläne reduzieren, um wiederholte Sammlungsauswertungen zu vermeiden. In einer tiefen Struktur können Sie die Häufigkeit der Sammlungsauswertung verringern, je tiefer sich die Sammlungen in der Struktur befinden, da Sammlungsauswertungen auf höherer Ebene auch Sammlungsauswertungen auf niedrigerer Ebene auslösen.

## <a name="understand-the-collection-evaluation-graph"></a>Grundlegendes zum Sammlungsauswertungdiagramm

Beachten Sie, wie das Sammlungsauswertungsdiagramm funktioniert, damit Sie eine geeignete Sammlungsstruktur entwerfen können. Verlassen Sie sich nicht auf die vollständige Sammlungsauswertung, um stets alle Sammlungen zu aktualisieren. Wenn eine inkrementell aktualisierte Sammlung nach Plan aktualisiert wird, werden verweisende Sammlungen, die nicht für inkrementelle Updates aktiviert sind, möglicherweise nicht aktualisiert. Da Updates bei inkrementellen Auswertungen wahrscheinlich aufgetreten sind, wird die Sammlung durch eine vollständige Auswertung möglicherweise nicht aktualisiert, sodass das Sammlungsauswertungsdiagramm für diesen Zyklus endet. In diesem Fall finden keine Auswertungen verweisender Sammlungen statt. Weitere Informationen finden Sie unter [Sammlungsauswertungsdiagramm](collection-evaluation.md#collection-evaluation-graph).

## <a name="limit-incremental-updates"></a><a name="bkmk_incremental"></a> Begrenzen inkrementeller Updates

Das Aktivieren inkrementeller Updates für viele Sammlungen kann zu Auswertungsverzögerungen führen. Es empfiehlt sich, die Anzahl der inkrementell aktualisierten Sammlungen auf 200 zu begrenzen. Die genaue Anzahl hängt von Folgendem ab:

- Gesamtzahl der Sammlungen
- Häufigkeit, mit der neue Ressourcen der Hierarchie hinzugefügt und darin geändert werden
- Anzahl der Clients in einer Hierarchie
- Komplexität der Sammlungsmitgliedschaftsregeln in einer Hierarchie

Wenn der inkrementelle Auswertungszyklus länger dauert als die konfigurierte Aktualisierungshäufigkeit, verarbeitet Configuration Manager ständig Sammlungsauswertungen, was sich auf die Systemleistung auswirken könnte. Reduzieren Sie die Anzahl inkrementell aktualisierter Sammlungen, oder setzen Sie den Zeitraum zwischen inkrementellen Auswertungszyklen herauf.

Angesichts der möglichen Auswirkung inkrementeller Sammlungen ist eine Richtlinie oder Prozedur zum Erstellen der Sammlungen und zum Zuweisen von Updatezeitplänen wichtig. Beispiele für Richtlinienüberlegungen:

- Verwenden Sie nur inkrementelle Updates für Sammlungen, die für Sicherheitsbereiche, Clienteinstellungen und Wartungsfenster verwendet werden. Diese Sammlungsupdates wirken sich auf das Clientverhalten und den Zugriff auf Ressourcen aus.
- Kündigen Sie für Anwendungen ohne Lizenzierungsgenehmigung Anwendungen auf bestehende Sammlungen an, und verwenden Sie globale Bedingungen, um die Verfügbarkeit einzuschränken.
- Gliedern Sie die entsprechenden Zeiträume für andere Sammlungen, für die vollständige Sammlungsupdates geplant sind.

## <a name="avoid-evaluation-of-large-trees-from-the-cas"></a>Vermeiden der Auswertung großer Strukturen von der CAS aus

In einer Configuration Manager-Umgebung wertet der Standort der zentralen Verwaltung (Central Administration Site, CAS) die Sammlungsmitgliedschaft nicht aus. Primäre Standorte sind die einzigen Standorte, die Sammlungen auswerten. Sekundäre Standorte fungieren als Proxys, die nur Daten verwenden, die sie von Ihrem primären Standort replizieren.

Um ein Sammlungsupdate anzufordern, sendet die CAS an jeden primären Standort eine Anforderung. Die primären Standorte werten die Sammlung aus und senden die Ergebnisse zurück an die CAS. Die Ergebnisse der Sammlungsauswertung werden erst angezeigt, nachdem alle Anweisungen zur Sammlungsauswertung an alle Standorte repliziert worden sind, alle Standorte alle Sammlungen ausgewertet haben und alle Daten an die CAS zurückgegeben und konsolidiert worden sind.

Das folgende Diagramm veranschaulicht den Ablauf, wenn die CAS ein manuelles Sammlungsupdate anfordert:

![Manuelles Sammlungsupdate von einer CAS](media/manual-collection-update-from-cas.png)

Ein Sammlungsupdate von einer CAS mit mehreren primären Standorten kann zeitaufwändig sein. Wenn eine Sammlung nicht rechtzeitig ausgewertet wird, reizt dies dazu, die Anforderung zu wiederholen.

Wenn ein Sammlungsauswertungsthread beginnt und das Auswertungsdiagramm lädt, wird die Auswertung fortgesetzt, bis das Sammlungsauswertungsdiagramm leer ist. Der Thread wird dann beendet und ist für die nächste Auswertung verfügbar. Wenn jedoch ein anderer Sammlungsauswertungszyklus in der Warteschlange steht, während der Thread Sammlungen auswertet, wird der Thread sofort neu gestartet, um eine Auswertung des „verpassten“ Zyklus zu versuchen.

Jede Auswertungsmethode führt einen eigenen Thread aus. Configuration Manager könnte innerhalb des Threads versuchen, von derselben Sammlung mehrere Diagramme zu erstellen. Configuration Manager löscht dann die zweite und nachfolgende Anforderungen.

Um diese Szenarien zu verhindern, sollten Sie manuelle Sammlungsauswertungen großer Strukturen vermeiden, insbesondere bei der Arbeit mit mehreren Standorten von der CAS aus.

## <a name="consider-collection-depth-and-cross-referencing"></a>Berücksichtigung von Sammlungstiefe und Querverweisen

Um ein ausgewogenes Verhältnis zwischen Geschäftsanforderungen und Leistung zu erreichen, müssen Sie die Sammlungsstruktur, die Sie erstellen, und ihre Abhängigkeiten von anderen Sammlungen verstehen. Wenn Sie eine Sammlung mit Regeln erstellen, die auf eine oder mehrere Sammlungen verweisen, die ihrerseits auf andere Sammlungen verweisen, werden alle diese Sammlungen ausgewertet, um die Mitgliedschaft der Sammlung zu erstellen.

Die Sammlungsregeln zum Einschließen und Ausschließen in Configuration Manager machen das Verweisen auf Sammlungen einfacher als das Schreiben einer benutzerdefinierten WQL-Abfrage. Wenn die Verwendung von Include- und Exclude-Sammlungen jedoch eine zu hohe Leistung beansprucht, können Sie stattdessen die WQL-Abfragemethode verwenden:

Einschließen:

`Select * from SMSRSystem where SMSRSystem.ResourceId in (select ResourceID from SMS_CM_RES_COLL_[collection id])`

Ausschließen:

`Select * from SMSRSystem where SMSRSystem.ResourceId not in (select ResourceID from SMS_CM_RES_COLL_[collection id])`

## <a name="use-ceviewer-to-monitor-collection-evaluation"></a>Verwenden von CEViewer zum Überwachen der Sammlungsauswertung

Mit dem [Collection Evaluation Viewer (CEViewer)](../../../support/ceviewer.md) können Sie überwachen, wie viele Sammlungen ausgewertet werden und wie lange das Aktualisieren der einzelnen Sammlungen dauert. Der CEViewer befindet sich auf dem Standortserver im *CD.Latest*-Ordner.

Sie können die folgende Abfrage verwenden, um eine ähnliche Überprüfung mit SQL manuell durchzuführen:

```sql
SELECT [t2].[CollectionName], [t2].[SiteID], [t2].[value] AS [Seconds], [t2].[LastIncrementalRefreshTime], [t2].[IncrementalMemberChanges] AS [IncChanges], [t2].[LastMemberChangeTime] AS [MemberChangeTime]
FROM (
    SELECT [t0].[CollectionName], [t0].[SiteID], DATEDIFF(Millisecond, [t1].[IncrementalEvaluationStartTime], [t1].[LastIncrementalRefreshTime]) * 0.001 AS [value], [t1].[LastIncrementalRefreshTime], [t1].[IncrementalMemberChanges], [t1].[LastMemberChangeTime], [t1].[IncrementalEvaluationStartTime], v1.[RefreshType]
    FROM [dbo].[Collections_G] AS [t0]
    INNER JOIN [dbo].[Collections_L] AS [t1] ON [t0].[CollectionID] = [t1].[CollectionID]
    inner join v_Collection v1 on [t0].[siteid] = v1.CollectionID
    ) AS [t2]
WHERE ([t2].[IncrementalEvaluationStartTime] IS NOT NULL) AND ([t2].[LastIncrementalRefreshTime] IS NOT NULL) and (refreshtype='4' or refreshtype='6')
ORDER BY [t2].[value] DESC
```