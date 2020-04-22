---
title: Planen von Migrationsaufträgen
titleSuffix: Configuration Manager
description: Verwenden Sie Migrationsaufträge zur Konfiguration von Daten, die zur Configuration Manager (Current Branch)-Umgebung migriert werden sollen.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a70bfbd4-757a-4468-9312-1c3b373ef9fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 87aac20a2ac70e843bf17982375c92804de2b20e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702848"
---
# <a name="plan-a-migration-job-strategy-in-configuration-manager"></a>Planen einer Strategie für Migrationsaufträge in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Verwenden Sie Migrationsaufträge zur Konfiguration der spezifischen Daten, die zur Configuration Manager (Current Branch)-Umgebung migriert werden sollen. Von Migrationsaufträgen werden die zu migrierenden Objekte identifiziert. Diese Migrationsaufträge werden am Standort der obersten Ebene der Zielhierarchie ausgeführt. Je Quellstandort können ein oder mehrere Migrationsaufträge eingerichtet werden. Dadurch können Sie alle Objekte gleichzeitig oder eine begrenzte Teilmenge von Daten mit jedem Auftrag migrieren.  

 Sie können Migrationsaufträge erstellen, wenn von Configuration Manager erfolgreich Daten von einem oder mehreren Standorten der Quellhierarchie gesammelt wurden. Sie können Daten von Quellstandorten, von denen Daten gesammelt wurden, in beliebiger Reihenfolge migrieren. Bei einem Quellstandort von Configuration Manager 2007 können Sie Daten nur von dem Standort migrieren, an dem ein Objekt erstellt wurde. Bei Quellstandorten mit System Center 2012 Configuration Manager oder höher sind alle Daten, die migriert werden können, am Standort der obersten Ebene der Quellhierarchie verfügbar.  

 Vergewissern Sie sich vor dem Migrieren von Clients zwischen zwei Hierarchien, dass von diesen verwendete Objekte migriert wurden und in der Zielhierarchie verfügbar sind. Wenn Sie beispielsweise von einer Configuration Manager 2007 SP2-Quellhierarchie migrieren, besteht möglicherweise eine Ankündigung für einen Inhalt, der auf einer benutzerdefinierten Sammlung mit einem Client bereitgestellt wird. In diesem Fall wird empfohlen, die Sammlung, die Ankündigung und den zugehörigen Inhalt vor der Migration des Clients zu migrieren. Werden Inhalt, Sammlung und Ankündigung nicht vor dem Client migriert, können diese Daten dem Client in der Zielhierarchie nicht zugeordnet werden. Wenn einem Client die Daten einer zuvor ausgeführten Ankündigung sowie Inhalte nicht zugeordnet sind, kann dem Client der Inhalt für die Installation in der Zielhierarchie zur Verfügung gestellt werden, was jedoch unnötig sein kann. Wenn der Client nach den Daten migriert wird, werden dem Client dieser Inhalt und diese Ankündigung zugeordnet und für den Inhalt der migrierten Ankündigung nicht nochmals zur Verfügung gestellt, es sei denn, die Ankündigung tritt wiederholt auf.  

 Für einige Objekte ist mehr als die Datenmigration von der Quell- zur Zielhierarchie erforderlich. Für eine erfolgreiche Migration von Softwareupdates für Clients zur Zielhierarchie müssen Sie beispielsweise in der Zielhierarchie einen aktiven Softwareupdatepunkt bereitstellen, den Produktkatalog konfigurieren und den Softwareupdatepunkt mit Windows Server Update Services (WSUS) synchronisieren.  

##  <a name="types-of-migration-jobs"></a><a name="Types_of_Migration"></a> Typen von Migrationsaufträgen  
 Configuration Manager unterstützt die folgenden Typen von Migrationsaufträgen. Jeder Auftragstyp dient als Hilfestellung zum Definieren der Objekte, die in diesem Auftrag eingeschlossen werden können.  

 **Sammlungsmigration** (wird nur bei einer Migration von Configuration Manager 2007 SP2 unterstützt): Objekte, die sich auf ausgewählte Sammlungen beziehen, werden migriert. Standardmäßig umfasst die Sammlungsmigration alle Objekte, die Mitgliedern der Sammlung zugeordnet sind. Sie können bestimmte Objektinstanzen ausschließen, wenn Sie einen Sammlungsmigrationsauftrag verwenden.  

 **Objektmigration:** Einzelne ausgewählte Objekte werden migriert. Sie wählen nur die Daten aus, die migriert werden sollen.  

 **Migration zuvor migrierter Objekte:** Objekte, die zuvor während der Aktualisierung dieser Objekte in der Quellhierarchie nach der letzten Migration migriert wurden, werden migriert.  

###  <a name="objects-that-you-can-migrate"></a><a name="Objects_that_can_migrate"></a> Objekte, die migriert werden können  
 Nicht jedes Objekt kann anhand eines bestimmten Migrationsauftragstyps migriert werden. In der folgenden Liste sind die migrierbaren Objekttypen nach Migrationsauftragstyp aufgeführt.  

> [!NOTE]  
>  Sammlungsmigrationsaufträge sind nur verfügbar, wenn Objekte von einer Configuration Manager 2007 SP2-Quellhierarchie migriert werden.  

 **Auftragstypen, mit denen Sie die einzelnen Objekt migrieren können**  

-   **Ankündigungen** (verfügbar zur Migration von unterstützten Configuration Manager 2007-Quellstandorten)  

    -   Sammlungsmigration  


-   **Asset Intelligence-Katalog**  

    -   Objektmigration  

    -   Migration zuvor migrierter Objekte  

-   **Asset Intelligence-Hardwareanforderungen**  

    -   Objektmigration  

    -   Migration zuvor migrierter Objekte  

-   **Asset Intelligence-Softwareliste**  

    -   Objektmigration  

    -   Migration zuvor migrierter Objekte  

-   **Standortgrenzen**  

    -   Objektmigration  

    -   Migration zuvor migrierter Objekte  

-   **Konfigurationsbaselines**  

    -   Sammlungsmigration  

    -   Objektmigration  

    -   Migration zuvor migrierter Objekte  

-   **Konfigurationselemente**  

    -   Sammlungsmigration  

    -   Objektmigration  

    -   Migration zuvor migrierter Objekte  

-   **Wartungsfenster**  

    -   Sammlungsmigration  


-   **Startimages der Betriebssystembereitstellung**  

    -   Sammlungsmigration  

    -   Objektmigration  

    -   Migration zuvor migrierter Objekte  

-   **Treiberpakete der Betriebssystembereitstellung**  

    -   Sammlungsmigration  

    -   Objektmigration  

    -   Migration zuvor migrierter Objekte  

-   **Treiber der Betriebssystembereitstellung**  

    -   Sammlungsmigration  

    -   Objektmigration  

    -   Migration zuvor migrierter Objekte  

-   **Images der Betriebssystembereitstellung**  

    -   Sammlungsmigration  

    -   Objektmigration  

    -   Migration zuvor migrierter Objekte  

-   **Betriebssystem-Bereitstellungspakete**  

    -   Sammlungsmigration  

    -   Objektmigration  

    -   Migration zuvor migrierter Objekte  

-   **Softwareverteilungspakete**  

    -   Sammlungsmigration  

    -   Objektmigration  

    -   Migration zuvor migrierter Objekte  

-   **Softwaremessungsregeln**  

    -   Objektmigration  

    -   Migration zuvor migrierter Objekte  

-   **Softwareupdate-Bereitstellungspakete**  

    -   Sammlungsmigration  

    -   Objektmigration  

    -   Migration zuvor migrierter Objekte  

-   **Softwareupdate-Bereitstellungsvorlagen**  

    -   Sammlungsmigration  

    -   Objektmigration  

    -   Migration zuvor migrierter Objekte  

-   **Softwareupdatebereitstellungen**  

    -   Sammlungsmigration  


-   **Softwareupdatelisten**  

    -   Objektmigration  

    -   Migration zuvor migrierter Objekte  

-   **Tasksequenzen**  

    -   Sammlungsmigration  

    -   Objektmigration  

    -   Migration zuvor migrierter Objekte  

-   **Virtuelle Anwendungspakete**  

    -   Sammlungsmigration  

    -   Objektmigration  

    > [!IMPORTANT]  
    >  Ein virtuelles Anwendungspaket kann zwar mithilfe der Objektmigration migriert werden, jedoch nicht mithilfe des Migrationsauftragstyps **Migration zuvor migrierter Objekte**. Vielmehr muss das migrierte virtuelle Anwendungspaket am Zielstandort gelöscht werden. Dann muss ein neuer Migrationsauftrag erstellt werden, um die virtuelle Anwendung zu migrieren.  

##  <a name="general-planning-for-all-migration-jobs"></a><a name="About_Migration_Jobs"></a> Allgemeine Planung für alle Migrationsaufträge  
 Erstellen Sie mithilfe des Assistenten zum Erstellen von Migrationsaufträgen einen Migrationsauftrag für die Migration von Objekten zur Zielhierarchie. Mit dem erstellten Migrationsauftragstyp werden die für eine Migration verfügbaren Objekte bestimmt. Sie können mehrere Migrationsaufträge zur Migration von Daten vom selben Quellstandort oder von mehreren Quellstandorten erstellen und verwenden. Die Verwendung eines Migrationsauftragstyps blockiert die Verwendung eines anderen Migrationsauftragstyps nicht.  

 Wenn ein Migrationsauftrag erfolgreich ausgeführt wurde, wird sein Status als **Abgeschlossen** aufgeführt, und er kann nicht erneut ausgeführt werden. Es kann jedoch ein neuer Migrationsauftrag zur Migration von Objekten erstellt werden, die bereits beim ursprünglichen Auftrag migriert wurden. Außerdem kann der neue Migrationsauftrag zusätzliche Objekte enthalten. Bei der Erstellung zusätzlicher Migrationsaufträge wird für die Objekte, die zuvor migriert wurden, der Status **Migriert** angezeigt. Diese Objekte können für eine erneute Migration ausgewählt werden. Solange das Objekt jedoch in der Quellhierarchie nicht aktualisiert wird, ist eine erneute Migration dieser Objekte nicht erforderlich. Wenn ein Objekt nach seiner Migration in der Quellhierarchie aktualisiert wurde, können Sie es identifizieren, wenn Sie den Migrationsauftragstyp **Nach der Migration geänderte Objekte**verwenden.  

 Sie können Migrationsaufträge löschen, bevor sie ausgeführt werden. Wird ein Migrationsauftrag jedoch abgeschlossen, bleibt er in der Configuration Manager-Konsole sichtbar und kann nicht gelöscht werden. Jeder Migrationsauftrag, der abgeschlossen ist oder noch nicht ausgeführt wurde, bleibt in der Configuration Manager-Konsole sichtbar, bis die Migrationsdaten nach Abschluss des Migrationsvorgangs bereinigt werden.  

> [!NOTE]  
>  Nachdem die Migration abgeschlossen und die Aktion **Migrationsdaten bereinigen** ausgeführt ist, kann die gleiche Hierarchie zur aktuellen Quellhierarchie umkonfiguriert werden, um die Übersicht über zuvor migrierte Objekte wiederherzustellen.  

 Sie können die in einem Migrationsauftrag enthaltenen Objekte in der Configuration Manager-Konsole anzeigen, indem Sie den Migrationsauftrag und anschließend die Registerkarte **Objekte in Auftrag** auswählen.  

 Die folgenden Abschnitte helfen Ihnen beim Planen sämtlicher Migrationsaufträge.  

### <a name="data-selection"></a>Datenauswahl  
 Für die Erstellung eines Sammlungsmigrationsauftrags müssen eine oder mehrere Sammlungen ausgewählt werden. Nach Auswahl der Sammlungen werden vom Assistenten zum Erstellen von Migrationsaufträgen die den Sammlungen zugeordneten Objekte angezeigt. Standardmäßig werden alle Objekte migriert, die den ausgewählten Sammlungen zugeordnet sind. Sie können jedoch Objekte deaktivieren, die bei diesem Auftrag nicht migriert werden sollen. Wenn Sie ein Objekt mit abhängigen Objekten deaktivieren, werden auch die abhängigen Objekte deaktiviert. Alle deaktivierten Objekte werden einer Ausschlussliste hinzugefügt. Objekte auf einer Ausschlussliste werden für zukünftige Migrationsaufträge aus der automatischen Auswahl entfernt. Damit Objekte entfernt werden, die automatisch zur Migration bei zukünftig erstellten Migrationsaufträgen ausgewählt werden sollen, müssen Sie die Ausschlussliste manuell bearbeiten.  

### <a name="site-ownership-for-migrated-content"></a>Standortbesitz migrierter Inhalte  
 Wenn Sie Inhalte für Bereitstellungen migrieren, müssen Sie das Inhaltsobjekt einem Standort in der Zielhierarchie zuweisen. Dieser Standort wird dann zum Besitzer dieses Inhalts in der Zielhierarchie. Vom Standort der obersten Ebene der Zielhierarchie werden die Metadaten der Inhalte zwar eigentlich migriert, doch es ist der zugewiesene Standort, durch den über das Netzwerk ein Zugriff auf die Originalquelle der Inhalte erfolgt.  

 Erwägen Sie, den Besitz auf den nächsten verfügbaren Standort zu übertragen, um die Netzwerkbandbreite zu minimieren, die bei der Migration verwendet wird. Die Inhaltsinformationen sind in Configuration Manager global freigegeben und daher an jedem Standort verfügbar.  

 Inhaltsinformationen werden mithilfe der Datenbankreplikation für alle Standorte freigegeben. Doch alle Inhalte, die einem primären Standort zugewiesen und dann für Verteilungspunkte an anderen primären Standorten bereitgestellt werden, werden mithilfe der dateibasierten Replikation übertragen. Diese Übertragung wird über den zentralen Verwaltungsstandort an jeden zusätzlichen primären Standort weitergeleitet. Bei geringer Netzwerkbandbreite können Sie Datentransfers reduzieren, indem Sie Pakete zentralisieren, die Sie vor oder während der Migration an mehrere primäre Standorte verteilen möchten, wenn Sie einen Standort als Besitzer des Inhalts zuweisen.  

### <a name="role-based-administration-security-scopes-for-migrated-data"></a>Rollenbasierte Verwaltungssicherheitsbereiche für migrierte Daten  
 Beim Migrieren von Daten zu einer Zielhierarchie müssen Sie dem Satz von Objekten, dessen Daten migriert werden, mindestens einen rollenbasierten Verwaltungssicherheitsbereich zuweisen. So kann auf diese Daten nach dem Migrieren nur von den entsprechenden Administratoren zugegriffen werden. Die angegebenen Sicherheitsbereiche werden über den Migrationsauftrag definiert und auf jedes Objekt angewendet, das bei diesem Auftrag migriert wird. Sind unterschiedliche Sicherheitsbereiche zur Anwendung auf verschiedene Objektsätze erforderlich, und sollen diese Bereiche während der Migration zugewiesen werden, müssen die verschiedenen Objektsätze in eigenen Migrationsaufträgen migriert werden.  

 Informieren Sie sich vor dem Einrichten eines Migrationsauftrags über die rollenbasierte Verwaltung in Configuration Manager. Richten Sie ggf. mindestens einen Sicherheitsbereich für die zu migrierenden Daten ein, um zu steuern, wer Zugriff auf die migrierten Objekte in der Zielhierarchie hat.  

 Weitere Informationen zu Sicherheitsbereichen und zur rollenbasierten Verwaltung finden Sie unter [Grundlagen der rollenbasierten Verwaltung für Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

### <a name="review-migration-actions"></a>Überprüfen von Migrationsaktionen  
 Beim Einrichten eines Migrationsauftrags wird vom Assistenten zum Erstellen von Migrationsaufträgen eine Liste von Aktionen angezeigt, die Sie ausführen müssen, um eine erfolgreiche Migration zu gewährleisten, sowie eine Liste von Aktionen, die von Configuration Manager beim Migrieren der ausgewählten Daten verwendet werden. Lesen Sie diese Informationen sorgfältig durch, um das erwartete Ergebnis zu überprüfen.  

### <a name="schedule-migration-jobs"></a>Planen von Migrationsaufträgen  
 Standardmäßig wird ein Migrationsauftrag sofort, nachdem er erstellt wurde, ausgeführt. Dennoch können Sie beim Erstellen des Migrationsauftrags oder beim Bearbeiten der Eigenschaften des Auftrags angeben, wann er ausgeführt werden soll. Sie können die Ausführung des Migrationsauftrags wie folgt planen:  

-   Den Auftrag jetzt ausführen  

-   Den Auftrag zu einer bestimmten Startzeit ausführen  

-   Den Auftrag nicht ausführen  

### <a name="specify-conflict-resolution-for-migrated-data"></a>Angeben von Konfliktlösungen für migrierte Daten  
 Standardmäßig werden von Migrationsaufträgen keine Daten in der Zieldatenbank überschrieben, es sei denn, Sie konfigurieren den Migrationsauftrag derart, dass zuvor zur Zieldatenbank migrierte Daten übersprungen oder überschrieben werden.  

##  <a name="plan-for-collection-migration-jobs"></a><a name="About_Collection_Migration"></a> Planen von Sammlungsmigrationsaufträgen  
 Sammlungsmigrationsaufträge sind nur verfügbar, wenn Sie Daten von einer Quellhierarchie migrieren, auf der eine unterstützte Version von Configuration Manager 2007 ausgeführt wird. Sie müssen mindestens eine Sammlung zum Migrieren angeben, wenn Sie sammlungsweise migrieren. Bei jeder angegebenen Sammlung werden vom Migrationsauftrag automatisch alle betreffenden Objekte zur Migration ausgewählt. Wenn Sie beispielsweise eine bestimmte Benutzersammlung auswählen, werden deren Mitglieder identifiziert, und Sie können die Bereitstellungen migrieren, die dieser Sammlung zugeordnet sind. Optional können Sie auch andere den Mitgliedern zugeordnete Bereitstellungsobjekte für die Migration auswählen. Alle ausgewählten Elemente werden der Liste von Objekten hinzugefügt, die migriert werden können.  

 Wenn Sie eine Sammlung migrieren, werden von Configuration Manager auch Sammlungseinstellungen wie Wartungsfenster und Sammlungsvariablen migriert. Sammlungseinstellungen für die AMT-Clientbereitstellung können hingegen nicht migriert werden.  

 In den folgenden Abschnitten werden zusätzliche Konfigurationen erläutert, die bei sammlungsbasierten Migrationsaufträgen gelten können.  

### <a name="exclude-objects-from-collection-migration-jobs"></a>Ausschließen von Objekten aus Sammlungsmigrationsaufträgen  
 Sie können bestimmte Objekte aus einem Sammlungsmigrationsauftrag ausschließen. Wenn Sie ein bestimmtes Objekt aus einem Sammlungsmigrationsauftrag ausschließen, wird dieses Objekt zu einer globalen Ausschlussliste hinzugefügt, die alle Objekte umfasst, die Sie von Migrationsaufträgen ausgeschlossen haben, welche für einen beliebigen Quellstandort in der aktuellen Quellhierarchie erstellt wurden. Objekte auf der Ausschlussliste können bei zukünftigen Migrationsaufträgen migriert werden, sie werden jedoch nicht automatisch eingeschlossen, wenn ein neuer sammlungsbasierter Migrationsauftrag erstellt wird.  

 Sie können die Ausschlussliste bearbeiten, um zuvor ausgeschlossene Objekte daraus zu entfernen. Nach dem Entfernen eines Objekts aus der Ausschlussliste wird das Objekt automatisch ausgewählt, wenn eine zugeordnete Sammlung beim Erstellen eines neuen Migrationsauftrags angegeben wird.  

### <a name="unsupported-collections"></a>Nicht unterstützte Sammlungen  
 Configuration Manager kann sämtliche Standardbenutzer- und Standardgerätesammlungen sowie die meisten benutzerdefinierten Sammlungen von einer Quellenhierarchie von Configuration Manager 2007 migrieren. Sammlungen mit Benutzern und Geräten in derselben Sammlung können jedoch nicht von Configuration Manager migriert werden.  

 Folgende Sammlungen können nicht migriert werden:  

-   Sammlungen, in denen Benutzer und Geräte enthalten sind.  

-   Sammlungen, in denen Verweise auf Sammlungen eines anderen Ressourcentyps enthalten sind. Dies könnten beispielsweise gerätebasierte Sammlungen sein, in denen entweder untergeordnete Sammlungen oder Verknüpfungen zu benutzerbasierten Sammlungen enthalten sind. In diesem Fall würde nur die Sammlung der obersten Ebene migriert.  

-   Sammlungen mit einer Regel zum Einschließen unbekannter Computer. Die Sammlung wird zwar migriert, jedoch nicht die Regel zum Einschließen unbekannter Computer.  

### <a name="empty-collections"></a>Leere Sammlungen  
 Leere Sammlungen sind Sammlungen, denen keine Ressourcen zugeordnet sind. Wenn von Configuration Manager eine leere Sammlung migriert wird, wird die Sammlung in einen Organisationsordner umgewandelt, in dem keine Benutzer oder Geräte enthalten sind. Der Ordner wird mit dem Namen der leeren Sammlung im Knoten **Benutzersammlungen** bzw. **Gerätesammlungen** im Arbeitsbereich **Bestand und Kompatibilität** der Configuration Manager-Konsole erstellt.  

### <a name="linked-collections-and-subcollections"></a>Verknüpfte Sammlungen und untergeordnete Sammlungen  
 Beim Migrieren von Sammlungen, die mit anderen Sammlungen verknüpft sind oder untergeordnete Sammlungen haben, wird zu den verknüpften bzw. untergeordneten Sammlungen von Configuration Manager ein Ordner im Knoten **Benutzersammlungen** bzw. **Gerätesammlungen** erstellt.  

### <a name="collection-dependencies-and-include-objects"></a>Sammlungsabhängigkeiten und Einschließen von Objekten  
 Wenn Sie im Assistenten zum Erstellen von Migrationsaufträgen einen Sammlungsmigrationsauftrag erstellen, werden alle abhängigen Sammlungen automatisch ausgewählt und im Auftrag eingeschlossen. Dadurch wird sichergestellt, dass alle notwendigen Ressourcen nach der Migration verfügbar sind.  

 Beispiel: Sie wählen eine Sammlung mit dem Namen **Win_10** für Geräte aus, auf denen Windows 10 ausgeführt wird. Diese Sammlung wird auf eine Sammlung mit dem Namen **Alle_Clients** begrenzt, in der alle Clientbetriebssysteme enthalten sind. Die Sammlung **Alle_Clients** wird automatisch für die Migration ausgewählt.  

### <a name="collection-limiting"></a>Sammlungsbegrenzung  
 In Configuration Manager (Current Branch) sind Sammlungen globale Daten, die an jedem Standort in der Hierarchie ausgewertet werden. Planen Sie daher das Begrenzen des Umfangs einer Sammlung, nachdem sie migriert wurde. Während der Migration können Sie eine Sammlung in der Zielhierarchie ermitteln, die zum Begrenzen des Bereichs der zu migrierenden Sammlung genutzt wird, sodass in der migrierten Sammlung keine unerwarteten Mitglieder enthalten sind.  

 In Configuration Manager 2007 werden Sammlungen beispielsweise an dem Standort ausgewertet, von dem sie erstellt werden, sowie an untergeordneten Standorten. Eine Ankündigung kann z. B. nur für einen einzigen untergeordneten Standort bereitgestellt werden, wodurch der Bereich für diese Ankündigung auf diesen untergeordneten Standort begrenzt wird. Im Gegensatz dazu werden von Configuration Manager Sammlungen an jedem Standort ausgewertet. Zugeordnete Ankündigungen werden anschließend für jeden Standort ausgewertet. Durch Sammlungsbegrenzung können Sie die Sammlungsmitglieder basierend auf einer anderen Sammlung einschränken, damit unerwartete Sammlungsmitglieder nicht hinzugefügt werden.  

### <a name="site-code-replacement"></a>Ersetzung von Standortcodes  
 Wenn Sie eine Sammlung mit Kriterien migrieren, durch die ein Configuration Manager 2007-Standort identifiziert wird, müssen Sie einen bestimmten Standort in der Zielhierarchie angeben. Dadurch wird sichergestellt, dass die migrierte Sammlung in der Zielhierarchie weiterhin funktioniert und sich der Bereich nicht vergrößert.  

### <a name="specify-behavior-for-migrated-advertisements"></a>Angeben des Verhaltens migrierter Ankündigungen  
 Standardmäßig werden bei sammlungsbasierten Migrationsaufträge Ankündigungen deaktiviert, die in die Zielhierarchie migriert wurden. Dies gilt auch für alle Programme, die mit der Ankündigung verbunden sind. Wenn Sie einen sammlungsbasierten Migrationsauftrag mit Ankündigungen erstellen, wird im Assistenten zum Erstellen von Migrationsaufträgen auf der Seite **Einstellungen** die Option **Enable programs for deployment in Configuration Manager after an advertisement is migrated** (Programme zur Bereitstellung in Configuration Manager aktivieren, nachdem eine Ankündigung migriert wurde) angezeigt. Wenn Sie diese Option auswählen, werden der Ankündigung zugeordnete Programme nach der Migration aktiviert. Es wird empfohlen, diese Option nicht auszuwählen. Aktivieren Sie stattdessen die Programme nach der Migration, wenn Sie die Clients überprüfen können, von denen sie empfangen werden.  

> [!NOTE]  
>  Die Option **Enable programs for deployment in Configuration Manager after an advertisement is migrated** (Programme zur Bereitstellung in Configuration Manager aktivieren, nachdem eine Ankündigung migriert wurde) wird nur angezeigt, wenn Sie einen sammlungsbasierten Migrationsauftrag erstellen, in dem Ankündigungen enthalten sind.  

 Deaktivieren Sie in den Programmeigenschaften auf der Registerkarte **Erweitert** die Option **Dieses Programm auf Computern deaktivieren, auf denen es angekündigt wird**, um ein Programm nach der Migration zu aktivieren.  

##  <a name="plan-for-object-migration-jobs"></a><a name="About_Object_Migration"></a> Planen von Objektmigrationsaufträgen  
 Anders als bei der Sammlungsmigration müssen Sie jedes Objekt und jede Objektinstanz, die Sie migrieren möchten, auswählen. Sie können die einzelnen Objekte auswählen (z. B. Ankündigungen aus einer Configuration Manager 2007-Hierarchie oder eine Veröffentlichung aus einer System Center 2012 Configuration Manager- oder Configuration Manager (Current Branch)-Hierarchie), um sie zur Migration für einen bestimmten Migrationsauftrag zur Objektliste hinzuzufügen. Nur Objekte, die Sie der Migrationsliste hinzufügen, werden über den Objektmigrationsauftrag zum Zielstandort migriert.  

 Für objektbasierte Migrationsaufträge müssen zusätzlich zu den Konfigurationen, die für alle Migrationsaufträge gelten, keine weiteren Konfigurationen geplant werden.  

##  <a name="plan-for-previously-migrated-object-migration-jobs"></a><a name="About_Object_Migrations"></a> Planen von Migrationsaufträgen für zuvor migrierte Objekte  
 Wenn ein bereits zur Zielhierarchie migriertes Objekt in der Quellhierarchie aktualisiert wird, können Sie dieses Objekt über den Auftragstyp **Nach der Migration geänderte Objekte** erneut migrieren. Wenn beispielsweise die Quelldateien eines Pakets in der Quellhierarchie umbenannt oder aktualisiert werden, wird die Paketversion in der Quellhierarchie schrittweise erhöht. Anhand der Erhöhungen der Paketversion kann das Paket von diesem Auftragstyp für die Migration identifiziert werden.  

 Dieser Auftragstyp ähnelt dem Objektmigrationstyp, mit der Ausnahme, dass für eine Migration nur aus den Objekten ausgewählt werden kann, die erst nach der Migration eines vorherigen Migrationsauftrags aktualisiert wurden.   

 Wenn Sie diesen Auftragstyp auswählen, wird das Konfliktauflösungsverhalten im Assistenten zum Erstellen von Migrationsaufträgen auf der Seite **Einstellungen** zum Überschreiben von zuvor migrierten Objekten konfiguriert. Diese Einstellung kann nicht geändert werden.  

> [!NOTE]  
>  Mit diesem Migrationsauftrag können Objekte, die automatisch von der Quellhierarchie und Objekte, die von einem Administrator aktualisiert werden, identifiziert werden.  
