---
title: Prüflisten für die Migration
titleSuffix: Configuration Manager
description: Verwenden Sie Administratorprüflisten zum Planen einer Strategie zur Migration zu Current Branch von Configuration Manager.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 295fdf07-93cc-490c-acdd-ce3ee88cb36f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e406a2b7674815bb3313200ba850baa249f17ebc
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701808"
---
# <a name="administrator-checklists-for-migration-planning-in-configuration-manager"></a>Administratorchecklisten zur Migrationsplanung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Verwenden Sie die folgenden Administratorprüflisten zum Planen einer Strategie zur Migration zu Current Branch von Configuration Manager.

##  <a name="administrator-checklist-for-migration-planning"></a><a name="Checklist_Migraiton_Planning"></a> Administratorprüfliste zum Planen der Migration  
 Verwenden Sie die folgende Checkliste für die Planungsschritte vor der Migration.  

-   **Bewerten Sie die aktuelle Umgebung:**  

     Identifizieren Sie bestehende Geschäftsanforderungen, die von der Quellhierarchie erfüllt werden, und entwickeln Sie Pläne, wie diese Anforderungen auch in der Zielhierarchie erfüllt werden können.  

-   **Sehen Sie sich die Funktionalität und Änderungen an, die in Ihrer aktuell verwendeten Configuration Manager-Version möglich sind, und nutzen Sie diese Informationen beim Entwerfen der Zielhierarchie:**  

    Weitere Informationen finden Sie unter [Grundlagen von Configuration Manager](../../core/understand/fundamentals.md) und [Neuerungen](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md).  


-   **Bestimmen Sie das Modell der administrativen Sicherheit, das für die rollenbasierte Verwaltung verwendet werden soll.**  

    Weitere Informationen finden Sie unter [Grundlagen der rollenbasierten Verwaltung für Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

-   **Bewerten Sie Ihre Netzwerk- und Active Directory-Topologie:** Überprüfen Sie Ihre bestehende Domänenstruktur und Netzwerktopologie. Beachten Sie, inwiefern Ihr Hierarchieentwurf dadurch beeinflusst wird.  

-   **Stellen Sie den Entwurf Ihrer Zielhierarchie fertig:**  

    Entscheiden Sie die Platzierung von zentralem Verwaltungsstandort, primären Standorten und sekundären Standorten sowie die Inhaltsverteilungsoptionen.  

-   **Ordnen Sie die Hierarchie den Computern zu, die für die Standorte und Standortserver in der Zielhierarchie verwendet werden sollen:**  

    Identifizieren Sie die Computer, die von Standorten und Standortsystemservern in der Zielhierarchie verwendet werden sollen, und vergewissern Sie sich dann, dass diese über entsprechende Kapazitäten für aktuelle und zukünftige Betriebsanforderungen verfügen.  

-   **Planen Sie Ihre Objektmigrationsstrategie:**  

    Planen Sie den Einsatz der verfügbaren Migrationsaufträge zum Migrieren unterschiedlicher Objekte, z.B. Standortgrenzen, Sammlungen, Ankündigungen und Bereitstellungen. Weitere Informationen finden Sie unter [Typen von Migrationsaufträgen](../../core/migration/planning-a-migration-job-strategy.md#Types_of_Migration) in [Planen einer Strategie für Migrationsaufträge](../../core/migration/planning-a-migration-job-strategy.md).  

    Von Configuration Manager werden nur Objekte migriert, die Sie ausgewählt haben. Alle Objekte, die nicht migriert werden und in der Zielhierarchie erforderlich sind, müssen in der Zielhierarchie neu erstellt werden.  

    Objekte, die migriert werden können, werden beim Konfigurieren von Migrationsaufträgen angezeigt.  

-   **Planen Sie Ihre Clientmigrationsstrategie:**  

    Planen Sie die Migration von Clients anhand eines kontrollierten Ansatzes, mit dem beim Migrieren von Clients zur Zielhierarchie die Netzwerkbandbreite und Serververarbeitung begrenzt wird. Weitere Informationen zum Planen einer Strategie für die Clientmigration finden Sie unter [Planen einer Strategie für die Clientmigration](../../core/migration/planning-a-client-migration-strategy.md).  

-   **Planen Sie Inventur- und Kompatibilitätsdaten:**  

    Von Configuration Manager wird keine Migration von Hardwareinventurdaten, Softwareinventurdaten oder Kompatibilitätsdaten zur Verwaltung gewünschter Konfigurationen für Softwareupdates oder Clients unterstützt.  

    Stattdessen übermittelt der Client diese Informationen an seinen zugewiesenen Standort, nachdem er zu seinem neuen Standort in der Zielhierarchie migriert wurde und Richtlinien für diese Konfigurationen erhalten hat. Bei dieser Aktion wird die Datenbank des Zielstandorts mit aktuellen Inventur- und Kompatibilitätsdaten gefüllt.  

-   **Planen Sie den Abschluss der Migration von der Quellhierarchie:**  

    Entscheiden Sie, wann Objekte und Clients migriert werden. Nach Abschluss der Migration können Sie die Außerbetriebnahme der Standortserver in der Quellhierarchie planen.  

##  <a name="administrator-checklist-for-hierarchy-migration"></a><a name="Checklist_Hierarchy_for_migration"></a> Administratorprüfliste für die Hierarchiemigration  
Verwenden Sie die folgende Checkliste, um eine Zielhierarchie zu planen, bevor Sie mit der Migration beginnen.  

-   **Identifizieren Sie die Computer, die in der Zielhierarchie verwendet werden sollen:**  

    Configuration Manager unterstützt kein direktes Upgrade der Configuration Manager 2007-Infrastruktur. Stattdessen verwenden Sie die Migration zum Verschieben von Daten von Configuration Manager 2007 zu Current Branch von Configuration Manager. Dies erfordert, dass Sie eine parallele Bereitstellung verwenden und Configuration Manager auf neuen Computern installieren.  

    Außerdem müssen Sie beim Migrieren aus einer anderen Configuration Manager-Hierarchie eine neue Zielhierarchie installieren, bei der es sich um eine parallele Bereitstellung zur Quellhierarchie handelt.  

-   **Erstellen Sie die Zielhierarchie:**  

    Installieren und konfigurieren Sie zur Vorbereitung der Migration eine Configuration Manager-Zielhierarchie mit einem primären Standort. Beispiel:  

    -   Installieren Sie einen Standort der zentralen Verwaltung und mindestens einen untergeordneten primären Standort.  

    -   Installieren Sie einen eigenständigen primären Standort, wenn Sie keinen Standort der zentralen Verwaltung verwenden möchten.  

-   **Konfigurieren Sie einen Softwareupdatepunkt in der Zielhierarchie, und synchronisieren Sie Softwareupdates, wenn Sie auf Softwareupdates bezogene Informationen migrieren möchten:**  

    Sie müssen Softwareupdates in der Zielhierarchie konfigurieren und synchronisieren, bevor Sie Softwareupdateinformationen aus der Quellhierarchie migrieren können.  


-   **Installieren und konfigurieren Sie zusätzliche Standortsystemrollen in der Zielhierarchie:**  

    Konfigurieren Sie zusätzliche Standortsystemrollen und Standortsysteme, die Sie benötigen.  

-   **Überprüfen Sie den ordnungsgemäßen Betrieb der Zielhierarchie:**  

    Überprüfen Sie Folgendes:  

    -   Vergewissern Sie sich, dass die Datenbankreplikation zwischen Standorten funktioniert, wenn die Zielhierarchie mehrere Standorte enthält. Die Datenbankreplikation ist nicht auf eigenständige primäre Standorte anwendbar.  

    -   Überprüfen Sie, ob alle installierten Standortsystemrollen betriebsbereit sind.  

    -   Überprüfen Sie, ob die Configuration Manager-Clients, die Sie unter der Zielhierarchie installieren, mit dem jeweils zugewiesenen Standort kommunizieren können.  


##  <a name="administrator-checklist-for-migration"></a><a name="Checklisit_Migration"></a> Administratorprüfliste für die Migration  
Verwenden Sie die folgende Checkliste für die Datenmigration von der Quellhierarchie zur Zielhierarchie.  

-   **Aktivieren Sie die Migration in der Zielhierarchie:**  

    Konfigurieren Sie eine Quellhierarchie, indem Sie den Standort der obersten Ebene der Quellhierarchie angeben. Weitere Informationen zum Angeben des Quellstandorts finden Sie unter [Planen einer Strategie für Quellhierarchien](../../core/migration/planning-a-source-hierarchy-strategy.md).  

-   **Wählen Sie weitere Standorte in der Quellhierarchie aus, und konfigurieren Sie diese, wenn in der Quellhierarchie Configuration Manager 2007 SP2 ausgeführt wird:**  

    Für jeden zusätzlichen Standort in der Configuration Manager 2007 SP2-Quellhierarchie, von dem Sie Daten sammeln möchten, müssen Sie Anmeldeinformationen für die Datensammlung konfigurieren. Wenn Sie die einzelnen Quellstandorte konfigurieren, beginnt der Datensammlungsvorgang sofort und wird während der gesamten Migrationsphase fortgesetzt, bis Sie das Sammeln von Daten für den jeweiligen Standort beenden. Die Datensammlung ermöglicht das Migrieren von Objekten aus der Quellhierarchie, die seit der letzten Datensammlung aktualisiert oder hinzugefügt wurden.

    > [!NOTE]  
    >  Wenn von der Quellhierarchie System Center 2012 Configuration Manager oder höher ausgeführt wird, müssen Sie keine zusätzlichen Quellstandorte konfigurieren.  

-   **Konfigurieren Sie die Verteilungspunktfreigabe:**  

    Sie können Verteilungspunkte zwischen den beiden Hierarchien freigeben, damit Clients in der Zielhierarchie auf Inhalte migrierter Objekte zugreifen können. So bleiben dieselben Inhalte für Clients in beiden Hierarchien verfügbar und können beibehalten werden, bis die Datensammlung beendet und die Migration abgeschlossen ist.  

    Informationen zu freigegebenen Verteilungspunkten finden Sie im Abschnitt [Freigeben von Verteilungspunkten zwischen Quell- und Zielhierarchien](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) des Themas [Planen einer Migrationsstrategie für die Inhaltsbereitstellung](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

-   **Erstellen und führen Sie Migrationsaufträge aus, um die Objekte zu migrieren, die den Clients in der Quellhierarchie zugeordnet sind:**  

    Erstellen Sie Migrationsaufträge zum Migrieren von Objekten zwischen Hierarchien. Die erforderlichen Konfigurationen für die einzelnen Migrationsaufträge können in Abhängigkeit davon variieren, welche Daten im Rahmen des Auftrags migriert werden.  

    Wenn Sie beispielsweise Inhalte migrieren, müssen Sie unabhängig vom verwendeten Migrationsauftrag einen Standort in der Zielhierarchie für die Verwaltung dieser Inhalte zuweisen. Der zugewiesene Standort greift auf den ursprünglichen Quelldateispeicherort für den Inhalt zu und ist für das Verteilen des Inhalts auf die Verteilungspunkte in der Zielhierarchie verantwortlich.  

    Weitere Informationen finden Sie im Abschnitt [Erstellen und Bearbeiten von Migrationsaufträgen für Configuration Manager](../../core/migration/operations-for-migration.md#Create_Edit_migration_Jobs) des Themas [Vorgänge der Migration zu Current Branch von Configuration Manager](../../core/migration/operations-for-migration.md).  

-   **Migrieren Sie Clients in die Zielhierarchie:**  

    Der Prozess für die Migration von Clients richtet sich nach Ihrem Migrationsszenario:  

    -   Beim Migrieren von Clients, deren Clientversion nicht der Version der Zielhierarchie entspricht, müssen Sie für die Clientsoftware ein Upgrade ausführen. Das Upgrade erfordert die Entfernung des aktuellen Configuration Manager-Clients und die anschließende Installation der neuen Clientversion, die der Version des Zielstandorts entspricht.  

    -   Beim Migrieren von Clients, deren Clientversion der Version der Zielhierarchie entspricht, wird für den Client kein Upgrade und keine Neuinstallation ausgeführt. Stattdessen wird der Client einem primären Standort in der Zielhierarchie neu zugewiesen.  

    Wenn Sie einen Client zur Zielhierarchie migrieren, wird der Client seinen Daten zugeordnet, die Sie bereits vorher zur Zielhierarchie migriert haben.  

    Weitere Informationen finden Sie unter [Planen einer Strategie für die Clientmigration](../../core/migration/planning-a-client-migration-strategy.md).  

-   **Führen Sie eine Aktualisierung oder Neuzuweisung freigegebener Verteilungspunkte durch:**  

    Wenn Sie in Ihrer Quellhierarchie keine Clients mehr unterstützen müssen, können Sie freigegebene Verteilungspunkte von einem Configuration Manager 2007-Quellstandort aktualisieren oder solche von einem System Center 2012 Configuration Manager-Quellstandort oder einem Quellstandort mit Current Branch von Configuration Manager neu zuweisen. Beim Aktualisieren oder erneuten Zuweisen eines Verteilungspunkts wird die Standortsystemrolle an einen primären Standort in der Zielhierarchie übertragen, und der Verteilungspunkt wird vom Quellstandort in der Quellhierarchie entfernt. Wenn Sie einen freigegebenen Verteilungspunkt aktualisieren oder neu zuweisen, verbleiben die Inhalte auf dem Verteilungspunktcomputer, sodass Sie sie nicht an neuen Verteilungspunkten der Zielhierarchie erneut bereitstellen müssen.  

    Sie können auch ein Upgrade von einem Configuration Manager 2007-Verteilungspunkt durchführen, der sich auf einem sekundären Standortserver befindet. Hierbei wird der sekundäre Standort entfernt, sodass sich in der Zielhierarchie nur ein Verteilungspunkt ergibt.  

    Informationen zu freigegebenen Verteilungspunkten finden Sie im Abschnitt [Freigeben von Verteilungspunkten zwischen Quell- und Zielhierarchien](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) des Themas [Planen einer Migrationsstrategie für die Inhaltsbereitstellung](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

-   **Fertigstellen der Migration:**  

    Nachdem Sie die Daten und Clients aller Standorte der Quellhierarchie migriert und ein Upgrade der relevanten Verteilungspunkte durchgeführt haben, können Sie die Migration fertig stellen. Beenden Sie das Sammeln von Daten für jeden Quellstandort in der Quellhierarchie, um die Migration fertigzustellen. Dann können nicht benötigte Migrationsinformationen entfernt werden, und die Infrastruktur der Quellhierarchie kann außer Betrieb genommen werden. Weitere Informationen finden Sie unter [Planen des Abschließens der Migration](../../core/migration/planning-to-complete-migration.md).  
