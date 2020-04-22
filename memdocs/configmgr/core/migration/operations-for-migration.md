---
title: Migrationsvorgänge
titleSuffix: Configuration Manager
description: Erstellen Sie Aufträge zum Migrieren von Daten und Clients zu Current Branch von Configuration Manager, und führen Sie diese aus.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c28e3492-851a-40fc-ba13-67ebc2d8b41a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a93269fc50c7bb39cd47f10e448d30742fc8ab22
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704568"
---
# <a name="operations-for-migrating-to-configuration-manager-current-branch"></a>Vorgänge der Migration zu Current Branch von Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Bei der Migration in Configuration Manager können Sie nach der erfolgreichen Datensammlung von einem Quellstandort in einer unterstützten Quellhierarchie Daten und Clients migrieren. Verwenden Sie die Informationen in den folgenden Abschnitten zum Erstellen und Ausführen von Migrationsaufträgen, um Daten und Clients zu migrieren und den Migrationsprozess abzuschließen.  

-   [Erstellen und Bearbeiten von Migrationsaufträgen](#Create_Edit_migration_Jobs)  

-   [Ausführen von Migrationsaufträgen](#Run_Migration_Jobs)  

-   [Aktualisieren oder erneutes Zuweisen eines freigegebenen Verteilungspunkts](#BKMK_ProcUpgrdSS)  

-   [Überwachen der Migrationsaktivität im Arbeitsbereich „Migration“](#Monitor_MIgration)  

-   [Migrieren von Clients](#BKMK_MigrateClients)  

-   [Fertigstellen der Migration](#Complete_Migration)  

##  <a name="create-and-edit-migration-jobs"></a><a name="Create_Edit_migration_Jobs"></a> Erstellen und Bearbeiten von Migrationsaufträgen  
 Gehen Sie wie folgt vor, um Datenmigrationsaufträge zu erstellen, die Ausschlussliste für sammlungsbasierte Migrationsaufträge zu bearbeiten, freigegebene Verteilungspunkte einzurichten und Zeitpläne für Migrationsaufträge zu bearbeiten.  

> [!NOTE]  
>  Das folgende Verfahren zum Erstellen eines Migrationsauftrags, bei dem anhand von Sammlungen migriert wird, gilt nur für Quellhierarchien, für die eine unterstützte Version von Configuration Manager 2007 ausgeführt wird. Der sammlungsbasierte Migrationsauftragstyp ist nicht verfügbar, wenn Sie aus einer System Center 2012 Configuration Manager-Quellhierarchie oder einer Quellhierarchie mit Current Branch von Configuration Manager migrieren.  

#### <a name="create-a-migration-job-to-migrate-by-collections"></a>Erstellen eines Migrationsauftrags zum Migrieren nach Sammlungen  

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** aus.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** die Option **Migration**, und wählen Sie **Migrationsaufträge** aus.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** die Option **Migrationsauftrag erstellen** aus.  

4.  Richten Sie auf der Seite **Allgemein** des Assistenten zum Erstellen von Migrationsaufträgen die folgenden Optionen ein, und wählen Sie **OK** aus:  

    -   Geben Sie einen Namen für den Migrationsauftrag an.  

    -   Wählen Sie in der Dropdownliste **Auftragstyp** die Option **Sammlungsmigration**aus.  

5.  Richten Sie auf der Seite **Sammlungen auswählen** die folgenden Optionen ein, und wählen Sie **Weiter** aus:  

    -   Wählen Sie die Sammlungen aus, die Sie migrieren möchten.  

    -   Wenn Sie nur die Sammlungen und nicht zusätzlich die diesen Sammlungen zugewiesenen Objekte migrieren möchten, deaktivieren Sie die Option **Objekte migrieren, die den angegebenen Sammlungen zugewiesen sind**. Wenn Sie diese Option deaktivieren, werden bei diesem Auftrag keine zugewiesenen Objekte migriert, und Sie können die Schritte 6 und 7 überspringen.  

6.  Deaktivieren Sie auf der Seite **Objekte auswählen** alle Objekttypen oder bestimmte verfügbare Objekte, die Sie nicht migrieren möchten. Standardmäßig werden alle zugeordneten Objekttypen und verfügbaren Objekte ausgewählt. Wählen Sie **Weiter** aus.  

7.  Weisen Sie auf der Seite **Inhaltsbesitz** den Besitz des Inhalts jedes aufgeführten Quellstandorts einem Standort in der Zielhierarchie zu, und wählen Sie **Weiter** aus.  

8.  Wählen Sie auf der Seite **Sicherheitsbereich** einen oder mehrere rollenbasierte Verwaltungssicherheitsbereiche aus, die den zu migrierenden Objekten dieses Migrationsauftrags zugewiesen werden sollen, und wählen Sie anschließend **Weiter** aus.  

9. Richten Sie auf der Seite **Sammlungsbegrenzung** eine Sammlung der Zielhierarchie zur Begrenzung des Bereichs jeder aufgeführten Sammlung ein, und wählen Sie **Weiter** aus. Wenn keine Sammlungen aufgeführt werden, wählen Sie **Weiter** aus.  

10. Weisen Sie auf der Seite **Ersetzung von Standortcodes** einen Standortcode aus der Zielhierarchie zu, um den Configuration Manager 2007-Standortcode für jede aufgeführte Sammlung zu ersetzen, und wählen Sie anschließend **Weiter** aus. Wenn keine Sammlungen aufgeführt werden, wählen Sie **Weiter** aus.  

11. Wählen Sie auf der Seite **Informationen überprüfen** die Option **In Datei speichern** aus, um die angezeigten Informationen später ggf. erneut anzuzeigen. Wählen Sie zum Fortfahren **Weiter** aus.  

12. Richten Sie auf der Seite **Einstellungen** den Zeitpunkt der Ausführung des Migrationsauftrags und alle zusätzlichen Einstellungen ein, die Sie für diesen Migrationsauftrag benötigen, und wählen Sie anschließend **Weiter** aus.  

13. Bestätigen Sie die Einstellungen, und beenden Sie den Assistenten.  

#### <a name="create-a-migration-job-to-migrate-by-objects"></a>Erstellen eines Migrationsauftrags zum Migrieren nach Objekten  

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** aus.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** die Option **Migration**, und wählen Sie **Migrationsaufträge** aus.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** die Option **Migrationsauftrag erstellen** aus.  

4.  Richten Sie auf der Seite **Allgemein** des Assistenten zum Erstellen von Migrationsaufträgen die folgenden Optionen ein, und wählen Sie **Weiter** aus:  

    -   Geben Sie einen Namen für den Migrationsauftrag an.  

    -   Wählen Sie in der Dropdownliste **Auftragstyp** die Option **Objektmigration**aus.  

5.  Wählen Sie auf der Seite **Objekte auswählen** die Objekttypen aus, die Sie migrieren möchten. Standardmäßig werden für jeden von Ihnen ausgewählten Objekttyp alle verfügbaren Objekte ausgewählt.  

6.  Weisen Sie auf der Seite **Inhaltsbesitz** den Besitz des Inhalts jedes aufgeführten Quellstandorts einem Standort in der Zielhierarchie zu, und wählen Sie **Weiter** aus. Wenn keine Quellstandorte aufgeführt werden, wählen Sie **Weiter** aus.  

7.  Wählen Sie auf der Seite **Sicherheitsbereich** einen oder mehrere rollenbasierte Verwaltungssicherheitsbereiche aus, die den Objekten dieses Migrationsauftrags zugewiesen werden sollen, und wählen Sie anschließend **Weiter** aus.  

8.  Wählen Sie auf der Seite **Informationen überprüfen** die Option **In Datei speichern** aus, um die angezeigten Informationen später ggf. erneut anzuzeigen. Wählen Sie zum Fortfahren **Weiter** aus.  

9. Richten Sie auf der Seite **Einstellungen** den Zeitpunkt der Ausführung des Migrationsauftrags und alle zusätzlichen Einstellungen ein, die Sie für diesen Migrationsauftrag benötigen. Wählen Sie anschließend **Weiter** aus.  

10. Bestätigen Sie die Einstellungen, und beenden Sie den Assistenten.  

#### <a name="create-a-migration-job-to-migrate-changed-objects"></a>Erstellen eines Migrationsauftrags zum Migrieren von geänderten Objekten  

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** aus.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** die Option **Migration**, und wählen Sie **Migrationsaufträge** aus.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** die Option **Migrationsauftrag erstellen** aus.  

4.  Richten Sie auf der Seite **Allgemein** des Assistenten zum Erstellen von Migrationsaufträgen die folgenden Optionen ein, und wählen Sie **Weiter** aus:  

    -   Geben Sie einen Namen für den Migrationsauftrag an.  

    -   Wählen Sie in der Dropdownliste **Auftragstyp** die Option **Nach der Migration geänderte Objekte** aus.  

5.  Wählen Sie auf der Seite **Objekte auswählen** die Objekttypen aus, die Sie migrieren möchten. Standardmäßig werden für jeden von Ihnen ausgewählten Objekttyp alle verfügbaren Objekte ausgewählt.  

6.  Weisen Sie auf der Seite **Inhaltsbesitz** den Besitz des Inhalts jedes aufgeführten Quellstandorts einem Standort in der Zielhierarchie zu, und wählen Sie **Weiter** aus. Wenn keine Quellstandorte aufgeführt werden, wählen Sie **Weiter** aus.  

7.  Wählen Sie auf der Seite **Sicherheitsbereich** einen oder mehrere rollenbasierte Verwaltungssicherheitsbereiche aus, die den Objekten dieses Migrationsauftrags zugewiesen werden sollen, und wählen Sie anschließend **Weiter** aus.  

8.  Wählen Sie auf der Seite **Informationen überprüfen** die Option **In Datei speichern** aus, um die angezeigten Informationen später ggf. erneut anzuzeigen. Wählen Sie zum Fortfahren **Weiter** aus.  

9. Richten Sie auf der Seite **Einstellungen** den Zeitpunkt der Ausführung des Migrationsauftrags und alle zusätzlichen Einstellungen ein, die Sie für diesen Migrationsauftrag benötigen. Im Gegensatz zu anderen Migrationsauftragstypen müssen bei diesem Migrationsauftrag die zuvor migrierten Objekte in der Configuration Manager-Datenbank überschrieben werden. Wählen Sie **Weiter** aus.  

10. Bestätigen Sie die Einstellungen, und beenden Sie den Assistenten.  

###  <a name="modify-the-exclusion-list-for-migration"></a><a name="BKMK_Modify_Exclusion_List"></a> Ändern der Ausschlussliste für die Migration  

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** aus.  

2.  Wählen Sie im Arbeitsbereich **Verwaltung** die Option **Migration** aus, um auf die Ausschlussliste zuzugreifen. Sie können auch über den Knoten **Quellhierarchie** oder **Migrationsaufträge** auf die Ausschlussliste zugreifen.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Migration** die Option **Ausschlussliste bearbeiten** aus.  

4.  Wählen Sie im Dialogfeld **Ausschlussliste bearbeiten** das ausgeschlossene Objekt aus, das Sie aus der Ausschlussliste entfernen möchten, und wählen Sie anschließend **Entfernen** aus.  

5.  Wählen Sie **OK** aus, um die Änderungen zu speichern und die Bearbeitung abzuschließen. Wählen Sie zum Verwerfen der aktuellen Änderungen und zum Wiederherstellen aller entfernten Objekte **Abbrechen** und anschließend **Nein** aus. Dadurch wird das Entfernen der Objekte abgebrochen, und das Dialogfeld **Ausschlussliste bearbeiten** wird geschlossen.  

#### <a name="share-distribution-points-from-the-source-hierarchy"></a>Freigeben von Verteilungspunkten aus der Quellhierarchie  

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** aus.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** die Option **Migration**, wählen Sie **Quellhierarchie** und anschließend den Quellstandort aus, den Sie einrichten möchten.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Quellstandort** die Option **Konfigurieren** aus.  

4.  Wählen Sie im Dialogfeld **Anmeldeinformationen des Quellstandorts** die Option **Gemeinsame Verwendung des Verteilungspunkts für den Quellstandortserver aktivieren** und anschließend **OK** aus.  

5.  Wenn die Datensammlung abgeschlossen ist, wählen Sie **Schließen** aus.  

#### <a name="change-the-schedule-of-a-migration-job"></a>Ändern des Zeitplans eines Migrationsauftrags  

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** aus.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** die Option **Migration**, und wählen Sie **Migrationsaufträge** aus.  

3.  Wählen Sie den Migrationsauftrag aus, den Sie ändern möchten. Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus.  

4.  Wählen Sie in den Eigenschaften des Migrationsauftrags die Registerkarte **Einstellungen** aus, ändern Sie die Laufzeit des Migrationsauftrags, und wählen Sie **OK** aus.  

##  <a name="run-migration-jobs"></a><a name="Run_Migration_Jobs"></a> Ausführen von Migrationsaufträgen  
 Verwenden Sie das folgende Verfahren, um einen Migrationsauftrag auszuführen, der noch nicht gestartet wurde.  


1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** aus.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** die Option **Migration**, und wählen Sie **Migrationsaufträge** aus.  

3.  Wählen Sie den Migrationsauftrag aus, den Sie ausführen möchten. Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Migrationsauftrag** die Option **Starten** aus.  

4.  Wählen Sie **Ja** aus, um den Migrationsauftrag zu starten.  

##  <a name="upgrade-or-reassign-a-shared-distribution-point"></a><a name="BKMK_ProcUpgrdSS"></a> Aktualisieren oder erneutes Zuweisen eines freigegebenen Verteilungspunkts  
 Sie können einen unterstützten Verteilungspunkt, der von einem Configuration Manager 2007-Quellstandort freigegeben wird, als Verteilungspunkt in der Zielhierarchie upgraden. (Alternativ können Sie einen unterstützten Verteilungspunkt, der von einem Configuration Manager-Quellstandort freigegeben wird, als Verteilungspunkt in der Zielhierarchie neu zuweisen.)  

> [!IMPORTANT]  
>  Bevor Sie ein Upgrade für einen Configuration Manager 2007-Zweigverteilungspunkt ausführen, müssen Sie die Configuration Manager 2007-Clientsoftware auf dem Zweigverteilungspunkt-Computer deinstallieren. Wenn die Configuration Manager 2007-Clientsoftware beim Versuch installiert wird, den Verteilungspunkt zu aktualisieren, tritt ein Fehler auf, und Inhalte, die zuvor auf dem Zweigverteilungspunkt bereitgestellt wurden, werden vom Computer entfernt.  

> [!CAUTION]  
>  Beim Upgraden oder erneuten Zuweisen eines freigegebenen Verteilungspunkts werden die Standortsystemrolle Verteilungspunkt und der Standortsystemcomputer am Quellstandort entfernt und dem gewählten Standort in der Zielhierarchie als Verteilungspunkt hinzugefügt.  

#### <a name="upgrade-or-reassign-a-shared-distribution-point"></a>Aktualisieren oder erneutes Zuweisen eines freigegebenen Verteilungspunkts  

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** aus.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** die Option **Migration**, und wählen Sie **Quellhierarchie** aus.  

3.  Wählen Sie den Standort aus, der Besitzer des Verteilungspunkts ist, für den ein Upgrade durchgeführt werden soll. Wählen Sie **Freigegebene Verteilungspunkte** und anschließend den geeigneten Verteilungspunkt aus, den Sie upgraden bzw. neu zuweisen möchten.  

4.  Wählen Sie auf der Registerkarte **Verteilungspunkt** in der Gruppe **Verteilungspunkt** die Option **Neu zuweisen** aus.  

5.  Geben Sie im Assistenten zur Neuzuweisung des freigegebenen Verteilungspunkts dieselben Einstellungen wie bei der Installation eines neuen Verteilungspunkts für die Zielhierarchie an, und fügen Sie Folgendes hinzu:  

    -   Prüfen Sie auf der Seite **Inhaltskonvertierung** die Richtlinien zum Speicherplatz, der zum Konvertieren des vorhandenen Inhalts erforderlich ist. Stellen Sie anschließend auf der Seite **Laufwerkseinstellungen** des Assistenten sicher, dass auf dem Laufwerk des ausgewählten Verteilungspunktcomputers die erforderliche Menge an freiem Festplattenspeicher verfügbar ist.  

6.  Bestätigen Sie die Einstellungen, und beenden Sie den Assistenten.  

##  <a name="monitor-migration-activity-in-the-migration-workspace"></a><a name="Monitor_MIgration"></a> Überwachen der Migrationsaktivität im Arbeitsbereich „Migration“  
 Verwenden Sie die Configuration Manager-Konsole zum Überwachen der Migration.  

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** aus.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** die Option **Migration**, und wählen Sie **Migrationsaufträge** aus.  

3.  Wählen Sie den Migrationsauftrag aus, den Sie überwachen möchten.  

4.  Auf den Registerkarten **Zusammenfassung** und **Objekte in Auftrag**können Sie Details und Status von ausgewählten Migrationsaufträgen anzeigen.  

##  <a name="migrate-clients"></a><a name="BKMK_MigrateClients"></a> Migrieren von Clients  
 Planen Sie die Migration der Clients zur Zielhierarchie, nachdem das Migrieren von Clientdaten zwischen Hierarchien fertig gestellt wurde, die Migration aber noch nicht abgeschlossen ist. Im Rahmen der Clientmigration zwischen Hierarchien muss die Configuration Manager-Clientsoftware von Computern deinstalliert werden, die der Quellhierarchie zugewiesen sind. Anschließend muss die Configuration Manager-Clientsoftware aus der Zielhierarchie installiert werden. Bei der Clientinstallation aus der Zielhierarchie weisen Sie den Client auch einem primären Standort dieser Hierarchie zu. Weitere Informationen zur Clientmigration finden Sie unter [Planen einer Strategie für die Clientmigration](../../core/migration/planning-a-client-migration-strategy.md).  

##  <a name="finish-migration"></a><a name="Complete_Migration"></a> Fertigstellen der Migration  
 Gehen Sie wie folgt vor, um die Migration von der Quellhierarchie fertigzustellen.  

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** aus.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** die Option **Migration**, und wählen Sie **Quellhierarchie** aus.  

3.  Wählen Sie für eine Configuration Manager 2007-Quellhierarchie einen Quellstandort aus, der sich auf der unteren Ebene der Quellhierarchie befindet. Für eine System Center 2012 Configuration Manager-Quellhierarchie oder eine Quellhierarchie mit Current Branch von Configuration Manager wählen Sie den verfügbaren Quellstandort aus.  

4.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Bereinigen** die Option **Sammeln von Daten beenden** aus.  

5.  Wählen Sie zum Bestätigen der Aktion **Ja** aus.  

6.  Bevor Sie für eine Configuration Manager 2007-Quellhierarchie mit dem nächsten Schritt fortfahren, wiederholen Sie die Schritte 3, 4 und 5. Führen Sie diese Schritte für jeden Standort in der Hierarchie von unten nach oben aus. Für eine System Center 2012 Configuration Manager-Quellhierarchie oder eine Quellhierarchie mit Current Branch von Configuration Manager fahren Sie mit dem nächsten Schritt fort.  

7.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Bereinigen** die Option **Migrationsdaten bereinigen** aus.  

8.  Wählen Sie im Dialogfeld **Migrationsdaten bereinigen** in der Dropdownliste **Quellhierarchie** den Standortcode und den Standortserver des Standorts der obersten Ebene der Quellhierarchie und anschließend **OK** aus.  

9. Wählen Sie **Ja** aus, um den Migrationsprozess für die Quellhierarchie fertigzustellen.  
