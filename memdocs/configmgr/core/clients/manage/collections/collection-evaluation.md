---
title: Sammlungsauswertungen
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über Sammlungsauswertung, Typen und Trigger. Grundlegendes zum Sammlungsauswertungdiagramm und der Hierarchie.
ms.date: 06/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d17e1188-d277-438f-9236-db9cd213b421
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: af90154b848ddcd7cbff21917ef122ab10585098
ms.sourcegitcommit: 1d8bf691780b94a945e94945115d4d1df4242808
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/10/2020
ms.locfileid: "84663860"
---
# <a name="collection-evaluation-in-configuration-manager"></a>Sammlungsauswertung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Configuration Manager aktualisiert mit der *Sammlungsauswertung* die Sammlungsmitgliedschaft basierend auf den von Ihnen definierten Sammlungsregeln. Der Sammlungsauswertungsbereich und das Timing unterscheiden sich je nach Standort, Sammlungskonfiguration und Auswertungstyp. 

Sie müssen das Verhalten der Sammlungsauswertung verstehen, um geeignete Entscheidungen zum Sammlungsentwurf treffen zu können. Anleitungen und Empfehlungen zur Sammlungsauswertung finden Sie unter [Bewährte Methoden für Sammlungen](best-practices-for-collections.md).

## <a name="evaluation-process"></a>Auswertungsvorgang

Die Datei [colleval.log](https://docs.microsoft.com/mem/configmgr/core/plan-design/hierarchy/log-files#BKMK_ServerLogs) zeichnet Datensätze auf, wenn der Sammlungsauswerter Sammlungen erstellt, ändert und löscht.

Auf hoher Ebene entspricht jede individuelle Sammlungsauswertung und jedes Update diesen Schritten:

![Sammlungsaktualisierungsprozess auf hoher Ebene](media/high-level-collection-update-process.png)

1. Ausführen der Sammlungsabfrage.
1. Ggf. Hinzufügen von Systemen, die direkte Mitglieder sind.
1. Auswerten aller *Include*-Sammlungen.
   
   Wenn die Include-Sammlungen auch Abfrageregeln oder Include- bzw. Exclude-Sammlungen aufweisen, werten Sie diese ebenfalls aus. Wenn die Include-Sammlungen selbst Sammlungen einschränken, sollten Sie alle darunter liegenden Sammlungen auswerten. Nachdem Sie die Struktur vollständig ausgewertet haben, geben Sie die Ergebnisse an die aufrufende Sammlung zurück.
   
1. Setzen Sie ein logisches `AND` zwischen die zurückgegebenen Ergebnisse und die einschränkende Sammlung.
1. Werten Sie die *Exclude*-Sammlungen aus.
   
   Wenn die Exclude-Sammlungen auch Abfrageregeln oder Include- bzw. Exclude-Sammlungen aufweisen, werten Sie diese ebenfalls aus. Wenn diese Sammlungen selbst Sammlungen einschränken, sollten Sie alle darunter liegenden Sammlungen auswerten. Nachdem Sie die Struktur vollständig ausgewertet haben, geben Sie die Ergebnisse an die aufrufende Sammlung zurück.
   
1. Vergleichen Sie das Resultset der Auswertung der direkten Mitglieder und Include-Sammlungen mit den Ergebnissen der Auswertung der Exclude-Sammlungen.
1. Schreiben Sie die Änderungen in die Datenbank, und führen Sie Updates durch.
1. Lösen Sie auch die Aktualisierung abhängiger Sammlungen aus. Abhängige Sammlungen sind Sammlungen, die von der aktuellen Sammlung eingeschränkt werden oder mithilfe von Include- oder Exclude-Regeln auf die aktuelle Sammlung verweisen.

## <a name="collection-evaluation-types-and-triggers"></a>Sammlungsauswertungstypen und -trigger

Diese Typen von Threads behandeln die Sammlungsauswertung abhängig vom Auswertungstyp:

- **Primär** für geplante Sammlungsupdates
- **Zusätzlich** zum manuellen Aktualisieren von Sammlungen mit abhängigen Sammlungen
- **Einzeln** zum manuellen Aktualisieren von Sammlungen ohne abhängige Sammlungen
- **Express** für inkrementelle Sammlungsupdates

In der folgenden Tabelle werden Sammlungsauswertungstrigger und ihre entsprechenden Auswertungstypen beschrieben. 

| Trigger | Auswertungstyp | Beschreibung |
|---------|-----------------|-------------|
|Manuell|„Einzeln“ oder „Zusätzlich“|„Manuell“ ist die Sammlungsauswertung mit der höchsten Priorität. Wenn ein Administrator eine manuelle Sammlungsauswertung anfordert, weist der Sammlungsauswerter den nächsten verfügbaren Auswertungsthread der Auswertung zu.|
|Scheduled|Primär|Der Prozess der geplanten Auswertung ist mit der manuellen Auswertung identisch, mit der Ausnahme, dass die Auswertung nicht ereignisgesteuert, sondern zeitgesteuert ist.|
|Staging|„Einzeln“ oder „Zusätzlich“|Alle Sammlungen sind direkt oder indirekt von **Alle Systeme** oder **Alle Benutzer und Benutzergruppen** abhängig. Für beide Sammlungen wird täglich um 4:00 Uhr eine vollständige Sammlungsauswertung ausgeführt. Durch eine Änderung an einer dieser Sammlungen werden basierend auf einem [vollständigen Sammlungsdiagramm](#collection-evaluation-graph) Updates abhängiger Sammlungen ausgelöst.
|Inkrementell|Express|Bei der inkrementellen Auswertung wird ein Sammlungsauswertungsdiagramm verwendet, um abhängige Sammlungen auszuwerten und zu aktualisieren, wenn sich ein Update der Mitgliedschaft in der inkrementellen Sammlung ändert. Configuration Manager überwacht und aktualisiert Ressourcenobjekte in allen Sammlungen, die für inkrementelle Updates konfiguriert sind.<br /><br />Wenn eine Sammlungsabfrage auf Informationen basiert, die später aktualisiert werden, wie z. b. der Hardwarebestand, fügt Configuration Manager der Sammlung die Ressource nur während der geplanten Sammlungsaktualisierung hinzu bzw. entfernt sie daraus.|

## <a name="collection-evaluation-graph"></a>Sammlungsauswertungsdiagramm

Ein *Sammlungsauswertungsdiagramm* ordnet alle Sammlungen zu, die mit der für die Auswertung vorgesehenen Sammlung in Beziehung stehen. Eine Sammlungsauswertung bezieht die vorgesehene Sammlung und alle zugehörigen Sammlungen in das Sammlungsauswertungsdiagramm ein.

Wenn die Sammlungsauswertung gestartet wird, erstellt Configuration Manager mit der höchsten Ebene im Zyklus beginnend ein Diagramm mit allen Sammlungen, die möglicherweise als Ergebnis von Änderungen an der vorgesehenen Sammlung ausgewertet werden müssen. Der Sammlungsauswerter durchläuft dann der Reihe nach das Diagramm und wertet jede Sammlungsmitgliedschaft aus. Sobald die Sammlung vollständig ausgewertet ist, entfernt der Sammlungsauswerter Sammlungen auf untergeordneten Ebenen, die von diesem Zyklus nicht betroffen sind, aus dem Sammlungsauswertungsdiagramm.

Wenn eine oder mehrere der ausgewerteten Sammlungen Include- oder Exclude-Regeln aufweisen, fügt der Sammlungsauswerter die ein- oder ausgeschlossene Sammlung zusammen mit allen Sammlungen, die Sammlungen einschränken, dem Diagramm hinzu. Wenn während der Auswertung der Include- und Exclude-Sammlungen Änderungen vorgenommen wurden, wird das Diagramm auf dieser Verzweigung fortgesetzt, bevor es zur Hauptverzweigung zurückkehrt.

Configuration Manager erstellt zwei Arten von Auswertungsdiagrammen, *inkrementelle* oder *vollständige*.

### <a name="incremental-collection-evaluation"></a>Inkrementelle Sammlungsauswertung

Wenn sich Tabellendaten ändern, fügt ein SQL-Trigger eine Zeile in die Tabelle **CollectionNotifications** ein. Wenn das nächste Mal ein Sammlungsauswertungs-Zeitplan ausgelöst wird, wird die Ressourcen-ID mittels `AND` mit der vorhandenen Sammlungsabfrage verknüpft, und es werden Updates für Sammlungen ausgelöst, die für *inkrementelle* Sammlungen aktiviert sind.

Die inkrementelle Sammlungsauswertung führt eine Abfrage pro Computer aus. Gemäß standardmäßiger Standortkonfiguration wird die inkrementelle Sammlungsauswertung alle fünf Minuten durchgeführt.

Ein inkrementelles Sammlungsauswertungsdiagramm ordnet referenzierte Sammlungen nur dann zu, wenn sie für die inkrementelle Auswertung aktiviert sind. Wenn eine inkrementelle Auswertung auf eine Sammlung beschränkt ist, die nicht für die inkrementelle Auswertung aktiviert ist, wertet das Diagramm die Sammlung basierend auf der vorhandenen Mitgliedschaft der einschränkenden Sammlung aus. 

Im folgenden Diagramm werden z. B. die neu ermittelten Ressourcen angezeigt, die für alle Sammlungen gelten. Bei der Sammlungsauswertung werden jedoch nur die Sammlungen **Alle Server** und **Alle Domänencontroller** aktualisiert. Der Sammlungsauswerter wertet die anderen Sammlungen nicht aus, da die Sammlung **Alle Mitgliedsserver** nicht für die inkrementelle Auswertung aktiviert ist.

![Beispiel eines inkrementellen Sammlungsauswertungsdiagramms](media/incremental-collection-evaluation-graph.png)

### <a name="full-collection-evaluation"></a>Vollständige Sammlungsauswertung

Manuelle oder geplante Sammlungsauswertungen erstellen ein *vollständiges* Sammlungsauswertungsdiagramm aller abhängigen Sammlungen. Das Diagramm enthält alle Sammlungen, die auf die Sammlung verweisen, die aktualisiert wird, und nachfolgende Sammlungen. Der Configuration Manager wertet weiterhin gemäß dem Diagramm aus, solange Aktualisierungen für die verarbeiteten Sammlungen durchgeführt werden.

Das folgende Diagramm zeigt, wie eine geplante oder manuelle Sammlungsupdateanforderung für die Sammlung **Alle Server** ein vollständiges Diagramm erzeugt, das alle anwendbaren Sammlungen enthält. Die neuen DNS-Server- und Domänencontrollerressourcen befinden sich im Bereich der Mitgliedschaftsabfragen aller Sammlungen, sodass alle Sammlungen aktualisiert werden.

![Beispiel 1 eines vollständigen Sammlungsauswertungsdiagramms](media/full-collection-evaluation-graph-1.png)

Bei einer vollständigen Auswertung werden nicht immer alle Sammlungen ausgewertet. Das Sammlungsauswertungsdiagramm fährt nur dann mit dem Auswerten abhängiger Sammlungen fort, wenn ein Update für die aktuell referenzierte Sammlung erfolgt. Wenn bei geplanten inkrementellen Auswertungen eine inkrementell aktualisierte Sammlung aktualisiert wird, werden verweisende Sammlungen, die nicht für inkrementelle Updates aktiviert sind, möglicherweise nicht aktualisiert. Bei einer vollständigen Auswertung wird die Sammlung nicht aktualisiert, und das Sammlungsauswertungsdiagramm und alle Auswertungen verweisender Sammlungen für diesen Zyklus werden beendet. 

Im folgenden Beispiel macht die Installation von DNS auf dem vorhandenen Server diesen zu einem Mitglied der Sammlung **DNS-Server**, aber da kein Update seiner beschränkenden Sammlung **Alle Mitgliedsserver** vorliegt, wertet die vollständige Auswertung die Sammlung **DNS-Server** nicht aus. Der nächste inkrementelle Auswertungszyklus wertet die Sammlung **DNS-Server** aus, da es sich um eine inkrementelle Sammlung handelt.

![Beispiel 2 eines vollständigen Sammlungsauswertungsdiagramms](media/full-collection-evaluation-graph-2.png)

## <a name="next-steps"></a>Nächste Schritte
- [How to create collections (Erstellen von Sammlungen)](create-collections.md)
- [Bewährte Methoden für Sammlungen](best-practices-for-collections.md)
- [Viewer für die Auswertung von Sammlungen](https://docs.microsoft.com/mem/configmgr/core/support/ceviewer)
- [ConfigMgrDogs Troubleshoot ConfigMgr 2012](https://channel9.msdn.com/Events/TechEd/Australia/2014/DCI411)-Sitzung bei TechEd Australia
