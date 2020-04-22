---
title: Strategie für Quellhierarchien
titleSuffix: Configuration Manager
description: Konfigurieren Sie eine Quellhierarchie und sammeln Sie Daten von einem Quellstandort, bevor Sie einen Configuration Manager-Migrationsauftrag konfigurieren.
ms.date: 01/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4800a800-66c8-4c35-aebe-e413a23790c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 28960753da06058ef181f94a5d11d9f2327ebf56
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702858"
---
# <a name="plan-a-source-hierarchy-strategy-in-configuration-manager"></a>Planen einer Strategie für Quellhierarchien in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Bevor Sie einen Migrationsauftrag in der Configuration Manager-Umgebung einrichten können, müssen Sie eine Quellhierarchie konfigurieren und Daten aus mindestens einem Quellstandort in dieser Hierarchie sammeln. Verwenden Sie die folgenden Abschnitte, um Quellhierarchien zu planen, Quellstandorte zu konfigurieren und zu bestimmen, wie Configuration Manager Daten von Quellstandorten in der Quellhierarchie sammeln soll. 

##  <a name="source-hierarchies"></a><a name="BKMK_Source_Hierarchies"></a> Quellhierarchien  
Eine Quellhierarchie ist eine Configuration Manager-Hierarchie, die zu migrierende Daten beinhaltet. Beim Einrichten einer Migration und Festlegen der dazugehörigen Quellhierarchie muss zuerst der Standort der obersten Ebene der Quellhierarchie angegeben werden. Dieser Standort wird auch als Quellstandort bezeichnet. Zusätzliche Standorte, aus denen Sie Daten in der Quellhierarchie migrieren können, werden ebenfalls als Quellstandorte bezeichnet.  

-   Wenn Sie einen Migrationsauftrag zum Migrieren von Daten von einer Configuration Manager 2007-Quellhierarchie einrichten, legen Sie fest, dass Daten aus einem oder mehreren bestimmten, der Quellhierarchie angehörenden Quellstandorten überführt werden.  

-   Wenn Sie einen Migrationsauftrag zum Migrieren von Daten aus einer Quellhierarchie für System Center 2012 Configuration Manager oder höher einrichten, müssen Sie nur den Standort der obersten Ebene angeben.  

Sie können jeweils nur eine Quellhierarchie einrichten.  

-   Beim Einrichten einer neuen Quellhierarchie wird diese automatisch zur aktuellen Quellhierarchie und ersetzt die vorherige.  

-   Zum Einrichten einer Quellhierarchie müssen Sie den Standort auf oberster Ebene der Quellhierarchie und die Anmeldeinformationen für Configuration Manager angeben, um eine Verbindung mit dem SMS-Anbieter und mit der Standortdatenbank am Quellstandort herzustellen.  

-   Diese Anmeldeinformationen werden von Configuration Manager für die Datensammlung verwendet, um Informationen über Objekte und Verteilungspunkte vom Quellstandort abzurufen.  

-   Beim Durchführen der Datensammlung werden die untergeordneten Standorte der Quellhierarchie ermittelt.  

-   Handelt es sich bei der Quellhierarchie um eine Configuration Manager 2007-Hierarchie, können Sie diese weiteren Standorte als Quellstandorte einrichten, wobei Sie für jeden Quellstandort eigene Anmeldedaten eingeben können.  

Sie können zwar mehrere Quellhierarchien nacheinander einrichten, die Migration kann aber jeweils nur für eine Quellhierarchie aktiv sein.  

-   Wenn Sie eine zusätzliche Quellhierarchie einrichten, bevor die Migration aus der aktuellen Quellhierarchie abgeschlossen ist, werden alle aktiven Migrationsaufträge in Configuration Manager abgebrochen und alle Migrationsaufträge für die aktuelle Quellhierarchie verschoben.  

-   Die neu konfigurierte Quellhierarchie wird zur aktuellen Quellhierarchie, und die ursprüngliche Quellhierarchie ist nun inaktiv.  

-   Anschließend können Sie Anmeldedaten, weitere Quellstandorte und Migrationsaufträge für die neue Quellhierarchie einrichten.  

Wenn Sie eine inaktive Quellhierarchie wiederherstellen, ohne vorher die Aktion **Migrationsdaten bereinigen** verwendet zu haben, dann können Sie sich die zuvor konfigurierten Migrationsaufträge für diese Quellhierarchie anzeigen lassen. Bevor Sie die Migration aus dieser Hierarchie fortsetzen können, müssen Sie die Anmeldeinformationen neu konfigurieren, um eine Verbindung mit den entsprechenden Quellstandorten in der Hierarchie herzustellen und dann alle Migrationsaufträge neu einplanen, die nicht abgeschlossen werden konnten.  

> [!CAUTION]  
>  Wenn Sie Daten aus mehreren Quellhierarchien migrieren, dann muss jede zusätzliche Quellhierarchie einen eindeutigen Satz von Standortcodes enthalten.  
> Quell- und Zielhierarchien erfordern außerdem andere Sätze von Standortcodes.

Weitere Informationen zum Konfigurieren einer Quellhierarchie finden Sie unter [Konfigurieren von Quellhierarchien und Quellstandorten für die Migration](../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md).  

##  <a name="source-sites"></a><a name="BKMK_Source_Sites"></a> Quellstandorte  
 Quellstandorte sind Standorte in der Quellhierarchie, die zu migrierende Daten enthalten. Der Standort auf oberster Ebene der Quellhierarchie ist immer der erste Quellstandort. Wenn bei der Migration Daten vom ersten Quellstandort einer neuen Quellhierarchie gesammelt werden, dann werden Informationen zu zusätzlichen Standorten in dieser Hierarchie entdeckt.  

 Nach Abschluss der Datensammlung für den ersten Quellstandort hängt die nachfolgende Aktion von der Produktversion der Quellhierarchie ab.  

### <a name="source-sites-that-run-configuration-manager-2007-sp2"></a>Quellstandorte, die Configuration Manager 2007 SP2 ausführen können  
 Nach dem Sammeln von Daten vom ersten Quellstandort der Configuration Manager 2007-SP2-Hierarchie müssen Sie keine zusätzlichen Quellstandorte einrichten, bevor Sie Migrationsaufträge erstellen. Bevor Sie jedoch Daten aus zusätzlichen Standorten migrieren können, müssen Sie zusätzliche Standorte als Quellstandorte einrichten, und über Configuration Manager müssen von diesen Standorten erfolgreich Daten gesammelt werden.  

 Für das Sammeln von Daten aus zusätzlichen Standorten richten Sie jeden Standort einzeln als Quellstandort ein. Dazu müssen Sie die Anmeldeinformationen für Configuration Manager angeben, um eine Verbindung mit dem SMS-Anbieter und der Standortdatenbank für jeden Quellstandort herzustellen. Nach dem Einrichten der Anmeldeinformationen für einen Quellstandort beginnt der Datensammlungsvorgang für diesen Standort.  

 Wenn Sie zusätzliche Quellstandorte in einer Configuration Manager 2007 SP2-Quellhierarchie einrichten, müssen Sie die Quellstandorte von oben nach unten einrichten, d.h. Sie richten die untersten Standorte zuletzt ein. Sie können Quellstandorte in einem Zweig der Hierarchie jederzeit einrichten, Sie müssen jedoch einen Standort als Quellstandort einrichten, bevor Sie dessen untergeordneten Standorte als Quellstandorte definieren können.  

> [!NOTE]  
>  Für die Migration werden nur primäre Standorte in einer Configuration Manager 2007 SP2-Hierarchie unterstützt.  

### <a name="source-sites-that-run-system-center-2012-configuration-manager-or-later"></a>Quellstandorte, an denen System Center 2012 Configuration Manager oder höher ausgeführt wird  
 Nach dem Sammeln von Daten vom ursprünglichen Quellstandort der System Center 2012 Configuration Manager-Hierarchie oder einer Hierarchie mit einer höheren Version von System Center müssen Sie keine zusätzlichen Quellstandorte in dieser Quellhierarchie einrichten. Das liegt daran, dass im Gegensatz zu Configuration Manager 2007 bei diesen Versionen von Configuration Manager eine freigegebene Datenbank verwendet wird, mit deren Hilfe Sie alle verfügbaren Objekte am ursprünglichen Quellstandort identifizieren und anschließend migrieren können.  

 Wenn Sie die Zugriffskonten für die Datensammlung einrichten, müssen Sie dem **Konto, das für den SMS-Anbieter des Quellstandorts** verwendet wird, möglicherweise Zugriff auf mehrere Computer in der Quellhierarchie gewähren. Dies ist ggf. erforderlich, wenn der Quellstandort mehrere Instanzen des SMS-Anbieters auf jeweils einem anderen Computer unterstützt. Zu Beginn der Datensammlung wird ein Kontakt zwischen dem Standort auf oberster Ebene der Zielhierarchie und dem Standort auf oberster Ebene der Quellhierarchie hergestellt, um die Orte des SMS-Anbieters für diesen Standort zu ermitteln. Es wird nur die erste Instanz des SMS-Anbieters identifiziert. Wenn über den Datensammlungsprozess nicht auf den SMS-Anbieter am angegebenen Ort zugegriffen werden kann, tritt während des Vorgangs ein Fehler auf, und es wird kein Versuch unternommen, eine Verbindung mit zusätzlichen Computern herzustellen, die eine Instanz des SMS-Anbieters für diesen Standort ausführen.  

##  <a name="data-gathering"></a><a name="BKMK_Data_Gathering"></a> Datensammlung  
 Direkt nach der Angabe einer Quellhierarchie, nach dem Einrichten von Anmeldeinformationen für einen zusätzlichen Quellstandort in einer Quellhierarchie oder nach der Freigabe der Verteilungspunkte für einen Quellstandort wird die Datensammlung am Quellstandort von Configuration Manager gestartet.  

 Der Datensammlungsvorgang wird dann nach einem einfachen Zeitplan wiederholt, um die Synchronisierung mit allen Änderungen der Daten am Quellstandort aufrechtzuerhalten. In der Standardeinstellung wird der Prozess alle vier Stunden wiederholt. Sie können den Zeitplan für diesen Zyklus verändern, indem Sie die **Eigenschaften** des Quellstandorts bearbeiten. Der erste Datensammlungsvorgang beinhaltet eine Prüfung sämtlicher Objekte in der Configuration Manager-Datenbank und kann einige Zeit in Anspruch nehmen. Bei den nachfolgenden Datensammlungsvorgängen werden nur noch Änderungen an den Daten identifiziert. Diese Vorgänge werden rascher abgeschlossen.  

 Zur Datensammlung wird eine Verbindung des Standorts der obersten Ebene der Zielhierarchie mit dem SMS-Anbieter und der Datenbank des Quellstandorts hergestellt, um eine Liste von Objekten und Verteilungspunkten abzurufen. Für diese Verbindungen werden die Zugriffskonten des Quellstandorts verwendet. Informationen zu erforderlichen Konfigurationen für das Sammeln von Daten finden Sie unter [Voraussetzungen für die Migration](../../core/migration/prerequisites-for-migration.md).  

 Mit den Aktionen **Daten jetzt sammeln** und **Sammeln von Daten beenden** in der Configuration Manager-Konsole können Sie den Datensammlungsprozess starten und beenden.  

 Nachdem Sie die Option **Sammeln von Daten beenden** für einen Quellstandort verwendet haben, müssen Sie die Anmeldeinformationen für den Standort neu konfigurieren, bevor Sie wieder Daten von diesem Standort sammeln können. Bis zur Neukonfiguration des Quellstandorts können von Configuration Manager keine neuen Objekte oder Änderungen an zuvor migrierten Objekten an diesem Standort erkannt werden.  

> [!NOTE]  
>  Bevor Sie einen eigenständigen primären Standort in eine Hierarchie mit einem zentralen Verwaltungsstandort erweitern, müssen Sie sämtliche Datensammlungen stoppen. Sie können die Datensammlung nach Abschluss der Standorterweiterung neu konfigurieren.  

### <a name="gather-data-now"></a>Daten jetzt sammeln  
 Nach dem ersten Datensammlungsvorgang für einen Standort wird der Vorgang wiederholt, um Objekte zu erkennen, die seit dem letzten Datensammlungszyklus aktualisiert wurden. Sie können auch die Aktion **Daten jetzt sammeln** in der Configuration Manager-Konsole verwenden, um den Vorgang sofort zu starten und die Startzeit für den nächsten Zyklus zurückzusetzen.  

 Ist der Datensammlungsvorgang für einen Quellstandort erfolgreich abgeschlossen, können die Verteilungspunkte des Quellstandorts freigegeben und Migrationsaufträge konfiguriert werden, um Daten vom Standort zu migrieren. Der Datensammlungsvorgang wird wiederholt, bis Sie die Quellhierarchie ändern oder **Sammeln von Daten beenden** verwenden, um den Datensammlungsvorgang für diesen Standort zu beenden.  

### <a name="stop-gathering-data"></a>Sammeln von Daten beenden  
 Mit **Sammeln von Daten beenden** können Sie den Datensammlungsvorgang für einen Quellstandort beenden, wenn keine neuen oder geänderten Objekte dieses Standorts mehr von Configuration Manager identifiziert werden sollen. Mit dieser Aktion wird außerdem verhindert, dass den Clients in der Zielhierarchie von Configuration Manager freigegebene Verteilungspunkte aus der Quelle als Inhaltsstandorte für den migrierten Inhalt angeboten werden.  

 Sollen keine Daten mehr von einem Quellstandort gesammelt werden, führen Sie die Aktion **Sammeln von Daten beenden** bei den Quellstandorten der untersten Ebene aus und wiederholen den Vorgang dann bei jedem übergeordneten Standort. Der Standort der obersten Ebene der Quellhierarchie muss der letzte Standort sein, an dem Sie die Datensammlung beenden. Beenden Sie die Datensammlung bei jedem untergeordneten Standort, ehe Sie sie bei einem übergeordneten Standort beenden. Üblicherweise wird die Datensammlung erst dann beendet, wenn der Migrationsprozess abgeschlossen werden kann.  

 Wenn Sie die Datensammlung bei einem Quellstandort beendet haben, bleiben zuvor gesammelte Informationen über Objekte und Sammlungen dieses Standorts verfügbar, wenn Sie neue Migrationsaufträge einrichten. Allerdings werden weder neue Objekte und Sammlungen angezeigt noch Änderungen, die an bestehenden Objekten vorgenommen wurden. Wenn Sie den Quellstandort neu konfigurieren und wieder mit der Datensammlung beginnen, sehen Sie Informationen und Statusangaben zu bereits migrierten Objekten.  
