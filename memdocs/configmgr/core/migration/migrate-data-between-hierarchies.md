---
title: Migrieren von Daten
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Daten aus einer Quellhierarchie in eine Zielhierarchie in Configuration Manager übertragen.
ms.date: 11/05/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cf014eb0-f8c2-4d37-b8d7-368d63a10b89
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a3771011f2822bb93a9569ec534b77259e2e8dc3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701748"
---
# <a name="migrate-data-between-hierarchies-in-configuration-manager"></a>Migrieren von Daten zwischen Hierarchien in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Verwenden Sie die Migration, um Daten aus einer unterstützten Quellhierarchie in Ihre Zielhierarchie in Configuration Manager (Current Branch) zu übertragen. Wenn Sie Daten aus einer Quellhierarchie migrieren:  

- Sie greifen auf Daten aus den Standortdatenbanken in der Quellinfrastruktur zu und übertragen diese Daten in die aktuelle Umgebung.  

- Die Migration ändert die Daten in der Quellhierarchie nicht. Stattdessen werden die Daten ermittelt, und eine Kopie wird in der Datenbank der Zielhierarchie gespeichert.  

Berücksichtigen Sie bei der Planung Ihrer Migrationsstrategie die folgenden Punkte:  

- Sie können eine vorhandene Configuration Manager 2007 SP2-Infrastruktur zu Configuration Manager (Current Branch) migrieren.  

- Sie können einige oder alle unterstützten Daten von einem Quellstandort migrieren.  

- Sie können die Daten eines einzelnen Quellstandorts zu mehreren unterschiedlichen Standorten in der Zielhierarchie migrieren.  

- Sie können Daten von mehreren Quellstandorten an einen einzelnen Standort in der Zielhierarchie verschieben.  


Im folgenden Video werden zwei gängige [Migrationsszenarios](#BKMK_MigrationScenarios) behandelt und veranschaulicht. Außerdem werden Optionen zum Einschließen von Microsoft Azure in Migrationspläne angesprochen.
> [!VIDEO https://www.youtube.com/embed/6_0EwW-5b4E]



##  <a name="concepts"></a><a name="BKMK_MigrationConcepts"></a> Konzepte  

 Configuration Manager verwendet folgende Konzepte und Begriffe für die Migration.  

#### <a name="source-hierarchy"></a>Quellhierarchie
Eine Hierarchie mit einer unterstützten Configuration Manager-Version, in der zu migrierende Daten enthalten sind. Beim Einrichten einer Migration legen Sie die Quellhierarchie fest, wenn Sie den Standort der obersten Ebene der Quellhierarchie angeben. Nachdem Sie eine Quellhierarchie angegeben haben, werden am Standort auf oberster Ebene Daten aus der Datenbank des bezeichneten Quellstandorts gesammelt, um die überführbaren Daten zu identifizieren. 

Weitere Informationen finden Sie unter [Quellhierarchien](planning-a-source-hierarchy-strategy.md#BKMK_Source_Hierarchies).

#### <a name="source-sites"></a>Quellstandorte
Standorte in der Quellhierarchie mit Daten, die zur Zielhierarchie migriert werden können. 

Weitere Informationen finden Sie unter [Quellstandorte](planning-a-source-hierarchy-strategy.md#BKMK_Source_Sites).

#### <a name="destination-hierarchy"></a>Zielhierarchie
Eine Hierarchie in Configuration Manager (Current Branch), in die bei der Migration Daten aus einer Quellhierarchie importiert werden.

#### <a name="data-gathering"></a>Datensammlung
Fortlaufender Vorgang zur Identifikation der Informationen in einer Quellhierarchie, die zur Zielhierarchie migriert werden können. Configuration Manager überprüft die Quellhierarchie nach einem Zeitplan. Bei diesem Prozess werden sämtliche Änderungen an Informationen in der Quellhierarchie ermittelt, die Sie zuvor migriert haben und die möglicherweise in der Zielhierarchie aktualisiert werden sollten.

Weitere Informationen finden Sie unter [Datensammlung](planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering).

#### <a name="migration-jobs"></a>Migrationsaufträge
Prozess, mit dem die zu migrierenden Objekte festgelegt ^werden und die Objektmigration zur Zielhierarchie verwaltet wird.

Weitere Informationen finden Sie unter [Planen einer Strategie für Migrationsaufträge](planning-a-migration-job-strategy.md).

#### <a name="client-migration"></a>Clientmigration
Prozess, mit dem von Clients verwendete Daten aus der Datenbank des Quellstandorts in die der Zielhierarchie übertragen werden. Auf diese Datenmigration folgt dann ein Upgrade der auf Geräten installierten Clientsoftware auf die Version der Zielhierarchie.

Weitere Informationen finden Sie unter [Planen einer Strategie für die Clientmigration](planning-a-client-migration-strategy.md).

#### <a name="shared-distribution-points"></a>Freigegebene Verteilungspunkte
Die Verteilungspunkte aus der Quellhierarchie, die in der Migrationsphase für die Zielhierarchie von Configuration Manager freigegeben werden.

Während der Migrationsphase können Clients, die Standorten in der Zielhierarchie zugewiesen sind, Inhalte von freigegebenen Verteilungspunkten erhalten.

Weitere Informationen finden Sie unter [Freigeben von Verteilungspunkten zwischen Quell- und Zielhierarchien](planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration).

#### <a name="monitoring-migration"></a>Migrationsüberwachung
Überwachen der Migrationsaktivitäten. Sie überwachen den Migrationsfortschritt und -erfolg im Arbeitsbereich **Verwaltung** unter dem Knoten **Migration**.

Weitere Informationen finden Sie unter [Planen der Überwachung der Migrationsaktivitäten ](planning-to-monitor-migration-activity.md).

#### <a name="stop-gathering-data"></a>Sammeln von Daten beenden
Das Beenden der Datensammlung von Quellstandorten. Wenn keine weiteren Daten mehr aus einer Quellhierarchie migriert oder die Migrationsaktivitäten angehalten werden sollen, kann die Zielhierarchie entsprechend konfiguriert werden, dass die Datensammlung in der Quellhierarchie beendet wird.

Weitere Informationen finden Sie unter [Datensammlung](planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering).

#### <a name="clean-up-migration-data"></a>Bereinigung der Migrationsdaten
Das Abschließen der Migration von einer Quellhierarchie durch Entfernen von migrationsbezogenen Informationen aus der Datenbank der Zielhierarchie.

Weitere Informationen finden Sie unter [Planen des Abschließens der Migration](planning-to-complete-migration.md).



## <a name="typical-workflow"></a>Typischer Workflow  

So richten Sie einen typischen Workflows bei der Migration ein:

1.  Geben Sie eine unterstützte Quellhierarchie an.  

2.  Richten Sie die Datensammlung ein. Mithilfe der Datensammlung kann Configuration Manager Informationen zu Daten sammeln, die aus der Quellhierarchie migriert werden können.  

     Der Prozess der Datensammlung wird bei Configuration Manager nach einem einfachen Zeitplan automatisch wiederholt, bis Sie den Vorgang beenden. Der Datensammlungsprozess wird standardmäßig alle vier Stunden wiederholt, damit Configuration Manager Änderungen der Daten in der Quellhierarchie identifizieren kann. Die Datensammlung ist auch für die Freigabe von Verteilungspunkten erforderlich.  

3.  Erstellen Sie Migrationsaufträge zum Migrieren von Daten zwischen der Quell- und Zielhierarchie.  

4.  Sie können den Datensammlungsprozess mit der Aktion **Sammeln von Daten beenden** jederzeit beenden. Wenn Sie die Datensammlung beenden, werden keine Änderungen an Daten in der Quellhierarchie von Configuration Manager ermittelt, und Verteilungspunkte können nicht mehr gemeinsam genutzt werden. Normalerweise verwenden Sie diese Aktion, wenn Sie keine Daten mehr migrieren oder Verteilungspunkte der Quellhierarchie mehr freigeben möchten.  

5.  Nachdem die Datensammlung an allen Standorten für die Quellhierarchie beendet wurde, können Sie die Migrationsdaten optional bereinigen, indem Sie die Aktion **Migrationsdaten bereinigen** verwenden. Diese Aktion löscht die Verlaufsdaten zur Migration aus einer Quellhierarchie aus der Datenbank der Zielhierarchie.  

Nach der Datenmigration benötigen Sie die Quellhierarchie nicht mehr zum Verwalten von Geräten in Ihrer Umgebung. Sie können die Quellhierarchie und Infrastruktur außer Betrieb nehmen.  



##  <a name="scenarios"></a><a name="BKMK_MigrationScenarios"></a> Szenarios  

 Configuration Manager unterstützt die folgenden Migrationsszenarios:
- [Migration aus Configuration Manager 2007-Hierarchien](#bkmk_2007)  
- [Migration aus Configuration Manager 2012 oder einer anderen Configuration Manager-Hierarchie](#bkmk_2012)

> [!NOTE]  
>  Die Erweiterung einer Hierarchie, die über einen eigenständigen Standort verfügt, in eine Hierarchie mit einem Standort der zentralen Verwaltung wird nicht als Migration bezeichnet. Weitere Informationen zur Erweiterung von Hierarchien finden Sie unter [Erweitern eines eigenständigen primären Standorts](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand).  


### <a name="migration-from-configuration-manager-2007-hierarchies"></a><a name="bkmk_2007"></a> Migration aus Configuration Manager 2007-Hierarchien  

 Durch Verwendung der Migrationsfunktion zum Migrieren von Daten aus Configuration Manager 2007 können Sie Ihre Investition in die bestehende Standortinfrastruktur sichern und die folgenden Vorteile erzielen:  

#### <a name="site-database-improvements"></a>Verbesserungen der Standortdatenbank
Die Configuration Manager-Datenbank (Current Branch) unterstützt Unicode uneingeschränkt.

#### <a name="database-replication-between-sites"></a>Datenbankreplikation zwischen Standorten
Die Replikation in Configuration Manager (Current Branch) basiert auf Microsoft SQL Server. Dieses Verhalten verbessert die Leistung bei der Datenübertragung zwischen Standorten.

#### <a name="user-centric-management"></a>Benutzerzentrierte Verwaltung
Benutzer stehen im Mittelpunkt von Verwaltungstasks in Configuration Manager (Current Branch). Beispielsweise können Sie Software an einen Benutzer verteilen, auch wenn Ihnen der Gerätename für diesen Benutzer nicht bekannt ist. Außerdem haben die Benutzer bei Configuration Manager deutlich mehr Kontrolle darüber, welche Software wann auf ihren Geräten installiert wird.

#### <a name="hierarchy-simplification"></a>Vereinfachte Hierarchie
Mit Configuration Manager (Current Branch) können Sie eine einfachere Standorthierarchie erstellen. Diese Verbesserung basiert auf der Einführung des Typs „Standort der zentralen Verwaltung“ und Änderungen am Verhalten primärer und sekundärer Standorte. Configuration Manager (Current Branch) nutzt weniger Netzwerkbandbreite und erfordert weniger Server als vorherige Versionen.

#### <a name="role-based-administration"></a>Rollenbasierte Verwaltung
Dieses zentrale Sicherheitsmodell von Configuration Manager (Current Branch) bietet hierarchieweite Sicherheit und eine Verwaltung, die Ihren administrativen und geschäftlichen Anforderungen gerecht wird.

> [!NOTE]  
>  Aufgrund der Designänderungen, die erstmals in System Center 2012 Configuration Manager eingeführt wurden, können Sie kein Upgrade von Configuration Manager 2007 auf Configuration Manager (Current Branch) durchführen. Ein direktes Upgrade von System Center 2012 Configuration Manager auf Configuration Manager (Current Branch) wird unterstützt.  


### <a name="migration-from-configuration-manager-2012-or-another-configuration-manager-hierarchy"></a><a name="bkmk_2012"></a> Migration aus Configuration Manager 2012 oder einer anderen Configuration Manager-Hierarchie  
 Die Vorgehensweisen für die Migration von Daten aus einer System Center 2012 Configuration Manager- oder Configuration Manager-Hierarchie sind identisch. Dazu gehört auch die Datenmigration aus mehreren Quellhierarchien in eine einzelne Zielhierarchie. Sie können diese Vorgehensweise verwenden, wenn Ihr Unternehmen zusätzliche Ressourcen erhält, die von Configuration Manager verwaltet werden. Außerdem können Sie Daten aus einer Testumgebung zu Ihrer Configuration Manager-Produktionsumgebung migrieren. Auf diese Weise können Sie Ihre Investition in die Configuration Manager-Testumgebung weiter nutzen.  



## <a name="see-also"></a>Weitere Informationen:  

-   [Planen der Migration zu Configuration Manager](planning-for-migration.md)  

-   [Konfigurieren von Quellhierarchien und Quellstandorten für die Migration](configuring-source-hierarchies-and-source-sites-for-migration.md)  

-   [Vorgänge der Migration](operations-for-migration.md)  

-   [Sicherheit und Datenschutz für die Migration](security-and-privacy-for-migration.md)  

-   [Starten der Verwendung von Configuration Manager](../servers/deploy/start-using.md)
