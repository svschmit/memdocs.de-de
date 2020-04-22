---
title: Migrieren von Objekten
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie die Migration von Objekten zwischen Hierarchien in einer Umgebung mit Configuration Manager (Current Branch) planen.
ms.date: 01/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 066caf00-e419-4efb-93d3-ba4ba878297c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9777fb12a2d63a990587386ac33cb2749bf19a4e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702818"
---
# <a name="plan-for-the-migration-of-configuration-manager-objects-to-configuration-manager-current-branch"></a>Planen der Migration von Configuration Manager-Objekten zu Configuration Manager (Current Branch)

*Gilt für: Configuration Manager (Current Branch)*

Bei Configuration Manager (Current Branch) können Sie viele der unterschiedlichen Objekte migrieren, die mit verschiedenen an einem Quellstandort vorhandenen Funktionen verknüpft sind.

##  <a name="plan-to-migrate-software-updates"></a><a name="Plan_migrate_Software_updates"></a> Planen der Migration von Softwareupdates  
 Softwareupdateobjekte wie Softwareupdatepakete und Softwareupdatebereitstellungen können migriert werden.  

 Damit Softwareupdateobjekte erfolgreich migriert werden können, müssen Sie die Zielhierarchie zunächst so mit Konfigurationen einrichten, dass sie zu Ihrer Quellhierarchieumgebung passt. Dies erfordert die folgenden Aktionen:  

-   Bereitstellen eines aktiven Softwareupdatepunkts in der Zielhierarchie  

-   Einrichten des Katalogs der Produkte und Sprachen entsprechend der Konfiguration Ihrer Quellhierarchie  

-   Synchronisieren des Softwareupdatepunkts in der Zielhierarchie mit Windows Server Update Services (WSUS)  

Beim Migrieren von Softwareupdates ist Folgendes zu beachten:  

-   Die Migration von Softwareupdateobjekten kann fehlschlagen, wenn die Informationen in der Zielhierarchie nicht so synchronisiert sind, dass sie zur Konfiguration Ihrer Quellhierarchie passen.  

    > [!WARNING]  
    >  Configuration Manager unterstützt die Nutzung eines WSUSutil-Tools zur Synchronisierung von Daten zwischen einer Quell- und einer Zielhierarchie nicht.  

-   Es können keine benutzerdefinierten Updates migriert werden, die mit System Center Updates Publisher veröffentlicht werden. Stattdessen müssen benutzerdefinierte Updates neu auf der Zielhierarchie veröffentlicht werden.  

Bei der Migration von einer Configuration Manager 2007-Quellhierarchie werden während des Migrationsverfahrens einige Softwareupdateobjekte in das in der Zielhierarchie verwendete Format geändert. Planen Sie anhand der nachstehenden Tabelle die Migration von Softwareupdateobjekten von Configuration Manager 2007.  

|Configuration Manager 2007-Objekt|Objektname nach der Migration|  
|-----------------------------------|---------------------------------|  
|Softwareupdatelisten|Softwareupdatelisten werden in Softwareupdategruppen konvertiert.|  
|Softwareupdatebereitstellungen|Softwareupdatebereitstellungen werden in Bereitstellungen und Updategruppen konvertiert.<br /><br /> Nach dem Migrieren einer Softwareupdatebereitstellung von Configuration Manager 2007 muss diese in der Zielhierarchie aktiviert werden, bevor sie bereitgestellt werden kann.|  
|Softwareupdatepakete|Softwareupdatepakete bleiben Softwareupdatepakete.|  
|Softwareupdatevorlagen|Softwareupdatevorlagen bleiben Softwareupdatevorlagen.<br /><br /> Der Wert **Dauer** in Configuration Manager 2007-Bereitstellungsvorlagen wird nicht migriert.|  

Die Softwareupdateobjekte werden nicht geändert, wenn Sie Objekte aus einer System Center 2012 Configuration Manager- oder der Configuration Manager (Current Branch)-Quellhierarchie migrieren.  

##  <a name="plan-to-migrate-content"></a><a name="Plan_Migrate_content"></a> Planen der Migration von Inhalten  
 Sie können Inhalte aus einer unterstützten Quellhierarchie zu einer Zielhierarchie migrieren. Bei einer Configuration Manager 2007-Quellhierarchie umfasst dieser Inhalt Softwareverteilungspakete und Programme sowie virtuelle Anwendungen, wie z.B. Microsoft Application Virtualization (App-V). Bei Quellhierarchien von System Center 2012 Configuration Manager und Configuration Manager (Current Branch) umfasst dieser Inhalt Anwendungen und virtuelle App-V-Anwendungen. Beim Migrieren von Inhalten zwischen Hierarchien werden die komprimierten Quelldateien zur Zielhierarchie migriert.  

### <a name="packages-and-programs"></a>Pakete und Programme  
 Das Migrieren von Paketen und Programmen verändert diese nicht. Dennoch muss jedes Paket vor der Migration für die Verwendung eines UNC-Pfads (Universal Naming Convention) für den Speicherort seiner Quelldatei eingerichtet werden. Ein Teil der Konfiguration zur Migration von Paketen und Programmen besteht aus dem Zuweisen eines Standorts in der Zielhierarchie, damit dieser Inhalt verwaltet werden kann. Die Inhalte werden nicht vom zugeordneten Standort migriert, vielmehr greift der zugeordnete Standort nach der Migration über die UNC-Zuordnung auf den Speicherort der Quelldatei zu.  

 Nach der Migration eines Pakets und Programms zur Zielhierarchie und während die Migration von der Quellhierarchie aktiv ist, können Sie Clients in dieser Hierarchie den Inhalt zur Verfügung stellen, indem Sie einen freigegebenen Verteilungspunkt verwenden. Damit ein freigegebener Verteilungspunkt verwendet werden kann, muss der Inhalt auf dem Verteilungspunkt des Quellstandorts verfügbar bleiben. Weitere Informationen zu freigegebenen Verteilungspunkten finden Sie im Abschnitt [Freigeben von Verteilungspunkten zwischen Quell- und Zielhierarchien](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) des Themas [Planen einer Migrationsstrategie für die Inhaltsbereitstellung](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

 Bei bereits migrierten Inhalten können Clients nicht länger über den freigegebenen Verteilungspunkt der Zielhierarchie auf Inhalte zugreifen, wenn die Inhaltsversion sich entweder in der Quell- oder in der Zielhierarchie geändert hat. In diesem Szenario müssen die Inhalte erneut migriert werden, um in der Quell- und Zielhierarchie eine einheitliche Version des Pakets wiederherzustellen. Diese Informationen werden im Verlauf des Datensammlungszyklus synchronisiert.  

> [!TIP]  
>  Aktualisieren Sie für jedes Paket, das Sie migrieren, in der Zielhierarchie. Dadurch können Probleme bei der Bereitstellung des Pakets an Verteilungspunkte in der Zielhierarchie verhindert werden. Allerdings können bei der Aktualisierung eines Pakets auf dem Verteilungspunkt in der Zielhierarchie Clients in dieser Hierarchie dieses Paket nicht mehr von einem freigegebenen Verteilungspunkt abrufen. Zur Aktualisieren eines Pakets in der Zielhierarchie gehen Sie in der Configuration Manager-Konsole zur Softwarebibliothek, klicken Sie mit der rechten Maustaste auf das Paket, und wählen Sie anschließend **Verteilungspunkte aktualisieren** aus. Führen Sie diese Aktion für jedes Paket durch, das Sie migriert haben.  

> [!TIP]  
> Mit dem Paketkonvertierungs-Manager können Sie Pakete und Programme in Configuration Manager-Anwendungen konvertieren. Weitere Informationen finden Sie unter [Paketkonvertierungs-Manager](../../apps/pcm/package-conversion-manager.md).  

### <a name="virtual-applications"></a>Virtuelle Anwendungen  
Bei der Migration von App-V-Paketen von einem unterstützten Configuration Manager 2007-Standort werden diese beim Migrationsprozess in Anwendungen in der Zielhierarchie umgewandelt. Zusätzlich werden je nach bestehenden Ankündigungen für das App-V-Paket folgende Bereitstellungstypen in der Zielhierarchie erstellt:  

-   Wenn keine Ankündigungen vorhanden sind, wird ein Bereitstellungstyp mit Standardeinstellungen erstellt.  

-   Liegt eine Ankündigung vor, wird ein Bereitstellungstyp erstellt, von dem die Einstellungen der Configuration Manager 2007-Ankündigung verwendet werden.  

-   Liegen mehrere Ankündigungen vor, wird für jede Configuration Manager 2007-Ankündigung anhand der Einstellungen der Anwendung ein Bereitstellungstyp erstellt.  

> [!IMPORTANT]  
>  Wird ein zuvor bereits migriertes Configuration Manager 2007-App-V-Paket migriert, kann die Migration nicht ausgeführt werden, weil das Migrationsüberschreibungsverhalten von virtuellen Anwendungspaketen nicht unterstützt wird. In diesem Szenario muss das migrierte virtuelle Anwendungspaket aus der Zielhierarchie gelöscht werden. Dann muss ein neuer Migrationsauftrag erstellt werden, um die virtuelle Anwendung zu migrieren.  

> [!NOTE]  
>  Nach der Migration eines App-V-Pakets können Sie mithilfe des Assistenten für das Update von Inhalten den Quellpfad für App-V-Bereitstellungstypen ändern. Weitere Informationen zum Aktualisieren von Inhalten für einen Bereitstellungstyp finden Sie im Abschnitt „Verwalten von Bereitstellungstypen“ des Themas [Verwaltungstasks für Configuration Manager-Anwendungen](../../apps/deploy-use/management-tasks-applications.md).  

Bei der Migration einer Quellhierarchie von System Center 2012 Configuration Manager oder Configuration Manager (Current Branch) können Sie zusätzlich zu App-V-Bereitstellungstypen und -Anwendungen Objekte für die virtuelle App-V-Umgebung migrieren. Weitere Informationen zu App-V-Umgebungen finden Sie unter [Bereitstellen virtueller App-V-Anwendungen](../../apps/get-started/deploying-app-v-virtual-applications.md).  

### <a name="advertisements"></a>Ankündigungen  
Ankündigungen können mit sammlungsbasierter Migration von einem unterstützten Configuration Manager 2007-Quellstandort in die Zielhierarchie migriert werden. Wird ein Client aktualisiert, wird der Verlauf zuvor ausgeführter Ankündigungen beibehalten, damit migrierte Ankündigungen auf dem Client nicht erneut ausgeführt werden.  

> [!NOTE]  
>  Ankündigungen für virtuelle Pakete können nicht migriert werden. Dies ist eine Ausnahme bei der Migration von Ankündigungen.  

### <a name="applications"></a>Applications  
 Sie können Anwendungen aus einer unterstützten Quellhierarchie für System Center 2012 Configuration Manager oder Configuration Manager (Current Branch) zu einer Zielhierarchie migrieren. Wenn Sie einer Zielhierarchie erneut einen Client aus der Quellhierarchie zuweisen, behält der Client den Verlauf zuvor installierter Anwendungen bei, damit eine migrierte Anwendung vom Client nicht erneut ausgeführt wird.  

##  <a name="plan-to-migrate-collections"></a><a name="BKMK_MigrateCollections"></a> Planen der Migration von Sammlungen  
 Sie können Kriterien für Sammlungen aus einer unterstützten Quellhierarchie für System Center 2012 Configuration Manager oder Configuration Manager (Current Branch) migrieren. Hierzu verwenden Sie einen objektbasierten Migrationsauftrag. Bei der Migration einer Sammlung werden die Regeln für die Sammlung migriert, nicht die Informationen zu den Mitgliedern der Sammlung oder auf Mitglieder der Sammlung bezogene Informationen bzw. Objekte.  

 Eine Migration des Sammlungsobjekts wird nicht unterstützt, wenn von einer Configuration Manager 2007-Quellhierarchie migriert wird.  

##  <a name="plan-to-migrate-operating-system-deployments"></a><a name="Plan_migrate_OSD"></a> Planen der Migration von Betriebssystembereitstellungen  
Die folgenden Betriebssystem-Bereitstellungsobjekte können von einer unterstützten Quellhierarchie migriert werden:  

-   Betriebssystemabbilder und -pakete. Der Quellpfad der Startimages wird auf den Standardspeicherort für Images des Windows Administrative Installation Kit (Windows AIK) am Zielstandort aktualisiert. Es folgen Anforderungen und Einschränkungen für die Migration von Betriebssystem-Abbildern und -Paketen:  

    -   Zum erfolgreichen Migrieren von Imagedateien benötigt das Computerkonto des SMS-Anbieterservers für den Standort auf höchster Ebene der Zielhierarchien **Lese-** und **Schreibberechtigungen** für die Imagequelldateien des Windows AIK-Speicherorts der Quellstandorte.  

    -   Bei der Migration eines Betriebssysteminstallationspakets muss die Konfiguration des Pakets am Quellstandort auf den Ordner verweisen, der die WIM-Datei enthält, und nicht auf die WIM-Datei selbst. Verweist das Installationspaket auf die WIM-Datei, kann es nicht migriert werden.  

    -   Bei der Migration eines Startimagepakets von einem Configuration Manager 2007-Quellstandort wird die Paket-ID am Zielstandort nicht beibehalten. Daraus ergibt sich, dass von Clients in der Zielhierarchie keine Startabbildpakete auf freigegebenen Verteilungspunkten verwendet werden können.  

-   Tasksequenzen. Bei der Migration einer Tasksequenz, die einen Verweis auf ein Clientinstallationspaket enthält, wird der Verweis durch einen Verweis auf das Clientinstallationspaket der Zielhierarchie ersetzt.  

    > [!NOTE]  
    >  Bei der Migration einer Tasksequenz werden von Configuration Manager möglicherweise Objekte migriert, die in der Zielhierarchie nicht erforderlich sind. Zu diesen Objekten gehören Startimages und Installationspakete des Configuration Manager 2007-Clients.  

-   Treiber und Treiberpakete. Bei der Migration von Treiberpaketen muss das Computerkonto des SMS-Anbieters in der Zielhierarchie über Vollzugriff auf die Paketquelle verfügen.

##  <a name="plan-to-migrate-desired-configuration-management"></a><a name="Plan_Migrate_Compliance_settings"></a> Planen der Migration der Verwaltung gewünschter Konfigurationen  
Es können Konfigurationselemente und Konfigurationsbasislinien migriert werden.  

> [!NOTE]  
>  Die Migration nicht interpretierter Konfigurationselemente aus Configuration Manager 2007-Quellhierarchien wird nicht unterstützt. Sie können solche Konfigurationselemente nicht in die Zielhierarchie migrieren oder importieren. Weitere Informationen zu nicht interpretierten Konfigurationselementen finden Sie im Abschnitt „Nicht interpretierte Konfigurationselemente“ des Themas [Informationen zu Konfigurationselementen in der Verwaltung gewünschter Konfigurationen](https://go.microsoft.com/fwlink/?LinkId=103846) in der Configuration Manager 2007-Dokumentationsbibliothek.  

Sie können Configuration Manager 2007-Konfigurationspakete importieren. Beim Importvorgang wird das Konfigurationspaket automatisch so konvertiert, dass es mit Configuration Manager (Current Branch) kompatibel ist.  

##  <a name="plan-to-migrate-boundaries"></a><a name="Plan_migrate_Boundaries"></a> Planen der Migration von Grenzen  
 Grenzen können zwischen Hierarchien migriert werden. Bei der Migration von Grenzen von Configuration Manager 2007 wird jede Grenze des Quellstandorts zur selben Zeit migriert und einer neuen Grenzgruppe hinzugefügt, die in der Zielhierarchie erstellt wird. Bei der Migration von Grenzen aus einer System Center 2012 Configuration Manager- oder Configuration Manager (Current Branch)-Hierarchie wird jede ausgewählte Grenze einer neuen Grenzgruppe in der Zielhierarchie hinzugefügt.  

 Jede automatisch erstellte Grenzgruppe ist für den Inhaltsort aktiviert, jedoch nicht für die Standortzuweisung. Dies verhindert die Überlappung von Grenzen bei der Standortzuweisung zwischen den Quell- und Zielhierarchien. Dadurch wird bei der Migration von einem Configuration Manager 2007-Quellstandort verhindert, dass neu installierte Configuration Manager 2007-Clients der Zielhierarchie falsch zugewiesen werden. In der Standardeinstellung werden Configuration Manager (Current Branch)-Clients nicht automatisch Configuration Manager 2007-Standorten zugewiesen.  

 Während der Migration werden alle dieser Verteilung zugeordneten Grenzen automatisch zur Zielhierarchie migriert, wenn bei der Zielhierarchie ein Verteilungspunkt freigegeben wird. In der Zielhierarchie wird bei der Migration eine neue schreibgeschützte Grenzgruppe für jeden freigegebenen Verteilungspunkt erstellt. Werden die Grenzen für den Verteilungspunkt in der Quellhierarchie geändert, wird die Grenzgruppe in der Zielhierarchie während des nächsten Datensammlungszyklus mit diesen Änderungen aktualisiert.  

##  <a name="plan-to-migrate-reports"></a><a name="Plan_Migrate_reports"></a> Planen der Migration von Berichten  
Die Migration von Berichten wird von Configuration Manager nicht unterstützt. Verwenden Sie stattdessen den Berichts-Generator von SQL Server Reporting Services, um Berichte von der Quellhierarchie zu exportieren und dann in die Zielhierarchie zu importieren.  

> [!NOTE]  
>  Da Schemaänderungen bei Berichten zwischen Configuration Manager 2007 und Configuration Manager (Current Branch) vorhanden sind, testen Sie jeden Bericht, den Sie aus einer Configuration Manager 2007-Hierarchie importieren, um sicherzustellen, dass er wie erwartet funktioniert.  

Weitere Informationen zur Berichterstellung finden Sie unter [Einführung in die Berichterstellung](../servers/manage/introduction-to-reporting.md).  

##  <a name="plan-to-migrate-organizational-and-search-folders"></a><a name="Plan_Migrate_Org_Folders"></a> Planen der Migration von Organisations- und Suchordnern  
 Sie können Organisations- und Suchordner von einer unterstützten Quellhierarchie zu einer Zielhierarchie migrieren. Sie können darüber hinaus Kriterien für gespeicherte Suchvorgänge aus einer unterstützten Quellhierarchie für System Center 2012 Configuration Manager oder Configuration Manager (Current Branch) zu einer Zielhierarchie migrieren.  

 Bei der Migration werden standardmäßig Ihre Such- und Administrator-Ordnerstrukturen für Objekte und Sammlungen beibehalten. Im Assistenten zum Erstellen von Migrationsaufträgen können Sie auf der Seite **Einstellungen** Migrationsaufträge jedoch auch so einrichten, dass die Organisationsstruktur für Objekte nicht migriert wird. Hierzu deaktivieren Sie das Kontrollkästchen für diese Option. Die Organisationsstrukturen von Sammlungen werden stets beibehalten.  

 Davon ausgenommen sind Suchordner, die virtuelle Anwendungen enthalten. Wird ein App-V-Paket migriert, wird es in Configuration Manager in eine Anwendung umgewandelt. Nach der Migration des Suchordners können nur die verbleibenden Pakete gefunden werden. App-V-Pakete können aufgrund ihrer Umwandlung in Anwendungen bei der Migration vom Suchordner nicht gefunden werden.  

 Bei der Migration einer gespeicherten Suche von einer System Center 2012 Configuration Manager- oder Configuration Manager (Current Branch)-Quellhierarchie werden die Kriterien für die Suche und nicht die Informationen zu den Suchresultaten migriert. Die Migration einer gespeicherten Suche gilt nicht für einen Configuration Manager 2007-Quellstandort.  

##  <a name="plan-to-migrate-asset-intelligence-customizations"></a><a name="Plan_Migrate_AI"></a> Planen der Migration von Asset Intelligence-Anpassungen  
 Sie können Asset Intelligence-Anpassungen von einer unterstützten Quellhierarchie zu einer Zielhierarchie migrieren. Die Struktur der Asset Intelligence-Anpassungen wurde zwischen Configuration Manager 2007 und Configuration Manager (Current Branch) nicht wesentlich verändert.  

> [!NOTE]  
> Configuration Manager (Current Branch) unterstützt keine Migration von Asset Intelligence-Objekten von einem Configuration Manager 2007-Standort, an dem Asset Intelligence Service 2.0 (AIS 2.0) verwendet wird.  

##  <a name="plan-to-migrate-software-metering-rules-customizations"></a><a name="Plan_Migrate_SWM_Rules"></a> Planen der Migration von Anpassungen von Softwaremessungsregeln  
 Softwaremessungsregeln wurden zwischen Configuration Manager 2007 und Configuration Manager (Current Branch) nicht wesentlich verändert. Sie können Softwaremessungsregeln von einer unterstützten Quellhierarchie zu einer Zielhierarchie migrieren.  

 Standardmäßig werden zu einer Zielhierarchie migrierte Softwaremessungsregeln keinem bestimmten Standort in der Zielhierarchie zugewiesen, sondern auf alle Clients in der Hierarchie angewendet. Zum Anwenden einer Softwaremessungsregel auf Clients an einem bestimmten Standort muss die Messungsregel nach der Migration bearbeitet werden.  
