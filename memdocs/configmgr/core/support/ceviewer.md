---
title: Collection Evaluation Viewer
titleSuffix: Configuration Manager
description: Verwenden Sie den Collection Evaluation Viewer, um die Sammlungsauswertung in Configuration Manager anzuzeigen und Probleme zu beheben.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: caad2d93-087c-4dc0-a2a7-6a2fd808b4c8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9ab75238e5dd26872847e68863ef603d3ac22671
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707888"
---
# <a name="collection-evaluation-viewer"></a>Collection Evaluation Viewer

*Gilt für: Configuration Manager (Current Branch)*

Der Collection Evaluation Viewer ist ein [Configuration Manager-Tool](tools.md). Verwenden Sie dieses Tool, um die Sammlungsauswertung auf dem primären Standortserver anzuzeigen und Probleme zu beheben.

In dem Tool werden die folgenden Informationen angezeigt:  

- Aktuelle Informationen und Informationen zum Verlauf für vollständige und inkrementelle Sammlungsauswertungen  

- Warteschlangenstatus der Auswertung  

- Die Zeit, die benötigt wird, um eine Sammlungsauswertung durchzuführen  

- Die Sammlungen, die derzeit ausgewertet werden  

- Die Zeit, die schätzungsweise benötigt wird, um eine Sammlungsauswertung zu starten und abzuschließen  



## <a name="about-collection-evaluation"></a>Informationen zu Sammlungsauswertungen

Die Sammlungsauswertung wird ausgeführt, indem Mitgliedschaftsregeln einer Sammlung ausgewertet werden, um deren Mitglieder zu aktualisieren. Die Site platziert eine Sammlung, die ausgewertet werden soll, in eine von vier Warteschlangen:  

- **Manuelle Warteschlange:** für Sammlungen, die ein Administrator manuell über die Konsole ausgewählt hat, damit diese ausgewertet werden  

- **Neue Warteschlange:** für neu erstellte Sammlungen  

- **Vollständige Warteschlange:** für Sammlungen, die vollständig ausgewertet werden sollen  

- **Inkrementelle Warteschlange:** für Sammlungen, für die eine inkrementelle Auswertung durchgeführt werden soll  

Es gibt vier Threads, die ausgeführt werden, um die Sammlungen in den oben genannten Warteschlangen auszuwerten. Jede Warteschlange umfasst eine Reihe von Arrays. Jedes Array umfasst wiederum Sammlungen, die ausgewertet werden sollen. Der Thread, der für die Warteschlange ausgeführt wird, wählt eine Sammlung aus dem Array aus und führt die Auswertung durch. Die Warteschlangenlänge steht für die Anzahl der Arrays in der Warteschlange.



## <a name="requirements"></a>Anforderungen

- Führen Sie das Tool auf dem Standortserver aus.  

- Führen Sie das Tool als Administrator mit der Rolle **Analyst mit Leseberechtigung** (mindestens) aus.  

- Außerdem benötigt der Benutzer **Leseberechtigungen** für die Standortdatenbank in SQL



## <a name="usage"></a>Verwendung

Führen Sie **CEViewer.exe** aus. Das Hauptmenü des Tools umfasst die folgenden Registerkarten: 

- [Verbinden:](#bkmk_connect) stellt die erste Verbindung mit dem primären Standortserver und dem Server für SQL Server her  

- [Vollständige Auswertung:](#bkmk_full-eval) listet ausführliche Informationen zu allen vergangenen vollständigen Auswertungen auf   

- [Inkrementelle Auswertung:](#bkmk_incremental-eval) listet ausführliche Informationen zu allen vergangenen inkrementellen Auswertungen auf  

- [Alle Warteschlangen:](#bkmk_all-q) fasst die aktuellen Sammlungsauswertungen für alle vier Warteschlangen zusammen  

- [Manuelle Warteschlange:](#bkmk_manual-q) listet ausführliche Informationen zu der aktuellen Sammlungsauswertung in der manuellen Warteschlange auf  

- [Neue Warteschlange:](#bkmk_new-q) listet ausführliche Informationen zu der aktuellen Sammlungsauswertung in der neuen Warteschlange auf  

- [Vollständige Warteschlange:](#bkmk_full-q) listet ausführliche Informationen zu der aktuellen Sammlungsauswertung in der vollständigen Warteschlange auf  

- [Inkrementelle Warteschlange:](#bkmk_incremental-q) listet ausführliche Informationen zu der aktuellen Sammlungsauswertung in der inkrementellen Warteschlange auf  


### <a name="connect-tab"></a><a name="bkmk_connect"></a> Registerkarte „Verbinden“

Über diese Registerkarte können Sie die erste Verbindung mit dem primären Standortserver herstellen. Außerdem stellt das Tool eine Verbindung mit dem Server mit SQL Server her, der die Standortdatenbank hostet.

Sowohl für die Verbindung mit dem primären Standortserver als auch für die Verbindung mit dem Server mit SQL Server werden die Anmeldeinformationen des zu diesem Zeitpunkt angemeldeten Benutzers verwendet. Verbindungen mit dem Standort der zentralen Verwaltung oder einem sekundären Standort werden nicht unterstützt. Für diese Standorte wird keine Sammlungsauswertung durchgeführt.

Wenn das Tool erfolgreich eine Verbindung herstellt, wird unten im Collection Evaluation Viewer eine Benachrichtigung angezeigt, in der bestätigt wird, dass das Tool mit dem Server mit SQL Server verbunden ist. 


### <a name="full-evaluation-tab"></a><a name="bkmk_full-eval"></a> Registerkarte „Vollständige Auswertung“

Auf dieser Registerkarte werden ausführliche Informationen zu vollständigen Sammlungsauswertungen angezeigt. Es gibt acht Spalten:  

- **Sammlungsnamen:** Der Name der Sammlung  

- **Standort-ID:** Die Standort-ID der Sammlung   

- **Laufzeit:** Dauer der letzten Sammlungsauswertung in Sekunden  

- **Zeitpunkt des Abschlusses der letzte Auswertung:** Der Zeitpunkt, zu dem der letzte Auswertungsvorgang abgeschlossen wurde  

- **Zeitpunkt der nächsten Auswertung:** Startzeitpunkt der nächsten vollständigen Auswertung  

- **Änderungen von Mitgliedern:** geänderte Mitglieder in der letzten Sammlungsauswertung. Diese Änderungen werden entweder durch „plus“ (hinzugefügte Mitglieder) oder „minus“ (entfernte Mitglieder) gekennzeichnet.  

- **Zeitpunkt der letzten Änderung eines Mitglieds:** der letzte Zeitpunkt, zu dem ein Mitglied in der Sammlungsauswertung geändert wurde  

- **Prozentsatz:** der Anteil der Dauer der Sammlungsauswertung im Vergleich zur Gesamtdauer der Auswertung aller Sammlungen  


### <a name="incremental-evaluation-tab"></a><a name="bkmk_incremental-eval"></a> Registerkarte „Inkrementelle Auswertung“

Auf dieser Registerkarte werden ausführliche Informationen zu inkrementellen Sammlungsauswertungen angezeigt. Es gibt sieben Spalten:  

- **Sammlungsnamen:** Der Name der Sammlung  

- **Standort-ID:** Die Standort-ID der Sammlung   

- **Laufzeit:** Dauer der letzten Sammlungsauswertung in Sekunden  

- **Zeitpunkt des Abschlusses der letzte Auswertung:** Der Zeitpunkt, zu dem der letzte Auswertungsvorgang abgeschlossen wurde  

- **Änderungen von Mitgliedern:** geänderte Mitglieder in der letzten Sammlungsauswertung. Diese Änderungen werden entweder durch „plus“ (hinzugefügte Mitglieder) oder „minus“ (entfernte Mitglieder) gekennzeichnet.  

- **Zeitpunkt der letzten Änderung eines Mitglieds:** der letzte Zeitpunkt, zu dem ein Mitglied in der Sammlungsauswertung geändert wurde  

- **Prozentsatz:** der Anteil der Dauer der Sammlungsauswertung im Vergleich zur Gesamtdauer der Auswertung aller Sammlungen  


### <a name="all-queues-tab"></a><a name="bkmk_all-q"></a> Registerkarte „Alle Warteschlangen“

Auf dieser Registerkarte werden die aktuellen Sammlungsauswertungen für alle vier Warteschlangen zusammengefasst. Es gibt sechs Abschnitte:  

- **Zusammenfassung:** listet die Gesamtanzahl der Sammlungen und die Länge der Warteschlange für sämtliche Sammlungen in allen vier Warteschlangen auf  

- **Laufende Auswertung:** führt auf, welche Sammlung aktuell in den einzelnen Warteschlangen ausgewertet und wie lange sie bereits ausgeführt wird  

- **Manuelles Update:** zeigt eine kurze Zusammenfassung der Sammlungen, die ausgewertet werden, den Zeitpunkt, an dem die Auswertung voraussichtlich abgeschlossen wird und die Reihenfolge der Auswertungen in der manuellen Warteschlange an  

- **Neue Sammlung:** zeigt eine kurze Zusammenfassung der Sammlungen, die ausgewertet werden, den Zeitpunkt, an dem die Auswertung voraussichtlich abgeschlossen wird und die Reihenfolge der Auswertungen in der Warteschlange für neue Sammlungen an  

- **Vollständige Auswertung:** zeigt eine kurze Zusammenfassung der Sammlungen, die ausgewertet werden, den Zeitpunkt, an dem die Auswertung voraussichtlich abgeschlossen wird und die Reihenfolge der Auswertungen in der Warteschlange für vollständige Auswertungen an  

- **Inkrementelle Auswertung:** zeigt eine kurze Zusammenfassung der Sammlungen, die ausgewertet werden, den Zeitpunkt, an dem die Auswertung voraussichtlich abgeschlossen wird und die Reihenfolge der Auswertungen in der Warteschlange für inkrementelle Auswertungen an  


### <a name="manual-queue-tab"></a><a name="bkmk_manual-q"></a> Registerkarte „Manuelle Warteschlange“

Auf dieser Registerkarte werden Informationen zu der manuellen Sammlungsauswertung angezeigt, die zum aktuellen Zeitpunkt ausgeführt wird. Die Reihenfolge der Liste stellt die Reihenfolge dar, in der die Sammlungen ausgewertet werden. Es gibt vier Spalten:  

- **Sammlungsnamen:** Der Name der Sammlung  

- **Standort-ID:** Die Standort-ID der Sammlung   

- **Geschätzte Abschlusszeit:** geschätzter Endzeitpunkt der Auswertung  

- **Geschätzte Laufzeit:** geschätzte Dauer der Auswertung im Format Tag:Stunde:Minute:Sekunde  


### <a name="new-queue-tab"></a><a name="bkmk_new-q"></a> Registerkarte „Neue Warteschlange“

Auf dieser Registerkarte werden Liveinformationen zu der neuen Sammlungsauswertung angezeigt, die zum aktuellen Zeitpunkt ausgeführt wird. Die Reihenfolge der Liste stellt die Reihenfolge dar, in der die Sammlungen ausgewertet werden. Es gibt vier Spalten:  

- **Sammlungsnamen:** Der Name der Sammlung  

- **Standort-ID:** Die Standort-ID der Sammlung   

- **Geschätzte Abschlusszeit:** geschätzter Endzeitpunkt der Auswertung  

- **Geschätzte Laufzeit:** geschätzte Dauer der Auswertung im Format Tag:Stunde:Minute:Sekunde  


### <a name="full-queue-tab"></a><a name="bkmk_full-q"></a> Registerkarte „Vollständige Warteschlange“

Auf dieser Registerkarte werden Informationen zu der vollständigen Sammlungsauswertung angezeigt, die zum aktuellen Zeitpunkt ausgeführt wird. Die Reihenfolge der Liste stellt die Reihenfolge dar, in der die Sammlungen ausgewertet werden. Es gibt vier Spalten:  

- **Sammlungsnamen:** Der Name der Sammlung  

- **Standort-ID:** Die Standort-ID der Sammlung   

- **Geschätzte Abschlusszeit:** geschätzter Endzeitpunkt der Auswertung  

- **Geschätzte Laufzeit:** geschätzte Dauer der Auswertung im Format Tag:Stunde:Minute:Sekunde  


### <a name="incremental-queue-tab"></a><a name="bkmk_incremental-q"></a> Registerkarte „Inkrementelle Warteschlange“

Auf dieser Registerkarte werden Informationen zu der inkrementellen Sammlungsauswertung angezeigt, die zum aktuellen Zeitpunkt ausgeführt wird. Die Reihenfolge der Liste stellt die Reihenfolge dar, in der die Sammlungen ausgewertet werden. Es gibt vier Spalten:  

- **Sammlungsnamen:** Der Name der Sammlung  

- **Standort-ID:** Die Standort-ID der Sammlung   

- **Geschätzte Abschlusszeit:** geschätzter Endzeitpunkt der Auswertung  

- **Geschätzte Laufzeit:** geschätzte Dauer der Auswertung im Format Tag:Stunde:Minute:Sekunde  



