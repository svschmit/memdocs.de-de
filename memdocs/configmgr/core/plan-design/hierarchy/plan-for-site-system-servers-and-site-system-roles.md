---
title: Planen von Standortsystemrollen
titleSuffix: Configuration Manager
description: Beachten Sie die Standortsystemserver und Standortsystemrollen bei der Planung Ihrer Configuration Manager-Hierarchie.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0a7415ba-2c53-4433-983e-780e92aa662f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3fb8c54920c10f8d3601a939c3c7b442c95e1dcf
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706498"
---
# <a name="plan-for-site-system-servers-and-site-system-roles-in-configuration-manager"></a>Planen der Standortsystemserver und Standortsystemrollen für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Jeder Configuration Manager-Standort, den Sie installieren, umfasst einen Standortserver, bei dem es sich um einen **Standortsystemserver** handelt. Der Standort kann auch weitere Standortsystemserver auf Computern umfassen, die sich geografisch getrennt vom Standortserver befinden. Die Standortsystemserver (der Standortserver oder ein Remotestandortsystemserver) unterstützen **Standortsystemrollen**.  

## <a name="site-system-servers"></a><a name="bkmk_siteservers"></a> Standortsystemserver  

Wenn Sie eine Standortsystemrolle auf einem Computer installieren, wird dieser Computer zu einem Standortsystemserver. Sie können an jedem Standortsystem mehrere zusätzliche Standortsystemserver installieren. Sie haben auch die Möglichkeit, keine weiteren Standortsystemserver zu installieren und alle Standortsystemrollen direkt auf dem Standortservercomputer auszuführen. Jeder Standortsystemserver unterstützt eine oder mehrere Standortsystemrollen. Zusätzliche Server können die Erweiterung der Funktionalität und Kapazität eines Standorts durch Aufteilen der Verarbeitungslast unterstützen, die durch Standortsystemrollen auf einem Server entsteht.  

Wenn Sie in Erwägung ziehen, einen Standortsystemserver hinzuzufügen, stellen Sie sicher, dass der Server die Voraussetzungen für die beabsichtigte Verwendung erfüllt. Fügen Sie ihn außerdem einer Netzwerkadresse hinzu, die über eine für die Kommunikation mit den voraussichtlichen Endpunkten ausreichende Bandbreite verfügt. Zu diesen Endpunkten zählen der Standortserver, Domänenressourcen, ein cloudbasierter Speicherort, Standortsystemserver sowie Clients.  


## <a name="site-system-roles"></a><a name="bkmk_planroles"></a> Standortsystemrolle  

Installieren Sie Standortsystemrollen auf einem Server, um zusätzliche Funktionen am Standort bereitzustellen. Beispiele:  

- Zusätzliche Verwaltungspunkte, damit ein Standort mehr Geräte verwalten kann (bis die unterstützte Kapazität des Standorts erreicht ist).  

- Zusätzliche Verteilungspunkte für die Erweiterung Ihrer Inhaltsinfrastruktur, wodurch die Leistung bei der Verteilung von Inhalt auf Geräte verbessert wird.  

- Eine oder mehrere featurespezifische Standortsystemrollen. Über einen Softwareupdatepunkt können Sie beispielsweise Softwareupdates für verwaltete Geräte verwalten. Über einen Reporting Services-Punkt können Sie Berichte ausführen, um Informationen zu Ihrer Umgebung zu überwachen, zu verstehen und freizugeben.  

Verschiedene Configuration Manager-Standorte können unterschiedliche Sätze von Standortsystemrollen unterstützen. Welche Standortsystemrollen unterstützt werden, hängt vom Standorttyp ab. (Zu den Standorttypen zählen ein Standort der zentralen Verwaltung, primäre Standorte oder sekundäre Standorte.) Die Topologie Ihrer Hierarchie kann die Platzierung einiger Rollen bei bestimmten Standorttypen einschränken. Der Dienstverbindungspunkt wird beispielsweise nur am Standort auf der obersten Ebene der Hierarchie unterstützt. Bei diesem Standort der obersten Ebene kann es sich entweder um einen Standort der zentralen Verwaltung handeln oder um einen eigenständigen primären Standort. Diese Rolle wird an einem untergeordneten primären Standort oder an sekundären Standorten nicht unterstützt.  

Nach der Installation eines Standorts, können Sie die Adresse einiger Standortsystemrollen von ihrem Standardspeicherort auf dem Standortserver auf einen anderen Server verschieben. Die Verwaltungspunkt- oder Verteilungspunktrolle wird beispielsweise standardmäßig auf einem primären oder sekundären Standortserver installiert. Installieren Sie außerdem zusätzliche Instanzen einiger Standortsystemrollen, um die Funktionalität Ihres Standorts zu erweitern und Ihre geschäftlichen Anforderungen zu erfüllen. Einige Rollen sind erforderlich, andere dagegen optional.  

### <a name="configuration-manager-site-server"></a>Configuration Manager-Standortserver

Diese Rolle identifiziert den Server, auf dem das Configuration Manager-Setup ausgeführt wird, um einen Standort oder den Server zu installieren, auf dem Sie einen sekundären Standort installieren. Diese Rolle kann erst verschoben oder deinstalliert werden, nachdem der Standort deinstalliert wurde.  

### <a name="configuration-manager-site-system"></a>Configuration Manager-Standortsystem

Diese Rolle wird jedem Computer zugewiesen, auf dem Sie einen Standort oder eine Standortsystemrolle installieren. Diese Rolle kann erst verschoben oder deinstalliert werden, nachdem die letzte Standortsystemrolle vom Computer entfernt wurde.  

### <a name="configuration-manager-component-site-system-role"></a>Standortsystemrolle für die Configuration Manager-Komponente

Diese Rolle gibt ein Standortsystem an, auf dem eine Instanz des **SMS Executive**-Diensts ausgeführt wird. Sie wird zur Unterstützung anderer Rollen wie etwa von Verwaltungspunkten benötigt. Diese Rolle kann erst verschoben oder deinstalliert werden, nachdem die letzte anwendbare Standortsystemrolle vom Computer entfernt wurde.  

### <a name="configuration-manager-site-database-server"></a>Configuration Manager-Standortdatenbankserver

Diese Rolle wird vom Standort Standortsystemservern zugeordnet, auf denen sich eine Instanz der Standortdatenbank befindet. Diese Rolle kann nur auf einen neuen Server verschoben werden, wenn zum Ändern des Standorts für die Verwendung einer anderen SQL Server-Instanz zum Hosten der Standortdatenbank ein Setup ausgeführt wird.  

### <a name="sms-provider"></a>SMS-Anbieter

Die Website weist jedem Computer diese Rolle zu, der eine Instanz des SMS-Anbieters hostet. Der Anbieter ist die Schnittstelle zwischen einer Configuration Manager-Konsole und der Standortdatenbank. Standardmäßig wird diese Rolle automatisch auf dem Standortserver eines zentralen Verwaltungsstandorts und von primären Standorten installiert. Installieren Sie aus Gründen der Redundanz zusätzliche Instanzen an jedem Standort, oder um weiteren Administratoren Zugriff zu bieten.  

Führen Sie das Configuration Manager-Setup zum [Verwalten der SMS-Anbieter](../../servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider) aus, um zusätzliche Anbieter zu installieren. Installieren Sie anschließend zusätzliche Anbieter auf weiteren Computern. Installieren Sie auf einem Computer immer nur eine Instanz des SMS-Anbieters. Dieser Computer und der Standortserver müssen sich in derselben Domäne befinden.  

### <a name="application-catalog-web-service-point"></a>Anwendungskatalog-Webdienstpunkt

> [!Important]
> Die Silverlight-Benutzeroberfläche für den Anwendungskatalog wird ab Current Branch-Version 1806 nicht unterstützt. Ab Version 1906 verwenden aktualisierte Clients automatisch den Verwaltungspunkt für Anwendungsbereitstellungen, die Benutzern zur Verfügung stehen. Zudem können Sie keine neuen Anwendungskatalogrollen installieren. Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910.  
>
> Weitere Informationen finden Sie in den folgenden Artikeln:
>
> - [Konfigurieren des Softwarecenters](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Entfernte und veraltete Features](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Über diese Standortsystemrolle werden der Anwendungskatalogwebsite Softwareinformationen aus der Softwarebibliothek bereitgestellt. Diese Rolle wird zwar nur an primären Standorten unterstützt, Sie können jedoch mehrere Instanzen dieser Rolle an einem Standort oder an mehreren Standorten in der gleichen Hierarchie installieren.  

### <a name="application-catalog-website-point"></a>Anwendungskatalog-Websitepunkt

> [!Important]
> Die Silverlight-Benutzeroberfläche für den Anwendungskatalog wird ab Current Branch-Version 1806 nicht unterstützt. Ab Version 1906 verwenden aktualisierte Clients automatisch den Verwaltungspunkt für Anwendungsbereitstellungen, die Benutzern zur Verfügung stehen. Zudem können Sie keine neuen Anwendungskatalogrollen installieren. Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910.  
>
> Weitere Informationen finden Sie in den folgenden Artikeln:
>
> - [Konfigurieren des Softwarecenters](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Entfernte und veraltete Features](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Über diese Standortsystemrolle wird Benutzern eine Liste der verfügbaren Software aus dem Anwendungskatalog bereitgestellt. Diese Rolle wird zwar nur an primären Standorten unterstützt, Sie können jedoch mehrere Instanzen dieser Rolle an einem Standort oder an mehreren Standorten in der gleichen Hierarchie installieren.  

### <a name="asset-intelligence-synchronization-point"></a>Asset Intelligence-Synchronisierungspunkt

Eine Standortsystemrolle, die eine Verbindung mit Microsoft herstellt, um Informationen für den Asset Intelligence-Katalog herunterzuladen. Diese Rolle lädt außerdem nicht kategorisierte Titel hoch, damit diese von Microsoft für die zukünftige Aufnahme in den Katalog berücksichtigt werden können. Eine Hierarchie unterstützt nur eine einzelne Instanz dieser Rolle am Standort der obersten Ebene Ihrer Hierarchie. Wenn Sie einen eigenständigen primären Standort in eine größere Hierarchie erweitern, deinstallieren Sie diese Rolle am primären Standort. Anschließend installieren Sie sie am Standort der zentralen Verwaltung.

Weitere Informationen finden Sie unter [Asset Intelligence in Configuration Manager](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

### <a name="certificate-registration-point"></a>Zertifikatregistrierungspunkt

Eine Standortsystemrolle, die mit einem Server kommuniziert, der den Registrierungsdienst für Netzwerkgeräte (NDES) ausführt. Diese Rolle verwaltet Gerätezertifikatanforderungen, die das SCEP (Simple Certificate Enrollment Protocol) verwenden. Diese Rolle wird nur an primären Standorten und am Standort der zentralen Verwaltung unterstützt.

Zwar kann ein einzelner Zertifikatregistrierungspunkt die erforderliche Funktionalität für die gesamte Hierarchie bereitstellen, aber möglicherweise möchten Sie mehrere Instanzen dieser Rolle an einem Standort sowie an mehreren Standorten in der gleichen Hierarchie installieren. Dieser Entwurf hilft beim Lastenausgleich. Wenn in einer Hierarchie mehrere Instanzen vorhanden sind, werden Clients nach dem Zufallsprinzip einem der Zertifikatregistrierungspunkte zugewiesen.  

Jeder Zertifikatregistrierungspunkt benötigt Zugriff auf eine separate NDES-Instanz. Die Verwendung derselben NDES-Instanz darf nicht für zwei oder mehr Zertifikatregistrierungspunkte konfiguriert werden. Zudem darf der Zertifikatregistrierungspunkt nicht auf dem Server installiert werden, auf dem NDES ausgeführt wird.  

### <a name="cloud-management-gateway-connection-point"></a>Verbindungspunkt für das Cloud Management Gateway

Eine neue Standortsystemrolle für die Kommunikation mit dem [Cloudverwaltungsgateway](../../clients/manage/cmg/plan-cloud-management-gateway.md).  

### <a name="data-warehouse-service-point"></a>Data Warehouse-Dienstpunkt

Verwenden Sie den Data Warehouse-Dienstpunkt, um langfristige Verlaufsdaten in Ihrer Configuration Manager-Umgebung zu speichern und hierfür Berichte zu erstellen. Weitere Informationen finden Sie unter [Data Warehouse](../../servers/manage/data-warehouse.md).  

### <a name="distribution-point"></a>Verteilungspunkt

Eine Standortsystemrolle enthält Quelldateien, die von Clients heruntergeladen werden können. Beispiele:

- Anwendungsinhalt
- Softwarepakete
- Softwareupdates
- Betriebssystemimages
- Startabbilder  

Diese Rolle wird beim Installieren eines neuen primären oder sekundären Standorts standardmäßig auf dem Standortserver installiert. Diese Rolle wird am zentralen Verwaltungsstandort nicht unterstützt. Installieren Sie mehrere Instanzen dieser Rolle an einem unterstützten Standort oder an mehreren Standorten in der gleichen Hierarchie. Weitere Informationen finden Sie unter [Grundlegende Konzepte für das Content Management](fundamental-concepts-for-content-management.md) und unter [Verwalten von Inhalt und Inhaltsinfrastruktur](../../servers/deploy/configure/manage-content-and-content-infrastructure.md).  

### <a name="endpoint-protection-point"></a>Endpoint Protection-Punkt

Mithilfe dieser Standortsystemrolle werden die Endpunkt Protection-Lizenzbedingungen in Configuration Manager akzeptiert und die Standardmitgliedschaft für Cloud Protection Service konfiguriert. Eine Hierarchie unterstützt nur eine einzelne Instanz dieser Rolle, und diese muss sich am Standort der obersten Ebene befinden. Wenn Sie einen eigenständigen primären Standort in eine größere Hierarchie erweitern, deinstallieren Sie diese Rolle am primären Standort, und installieren Sie sie anschließend am Standort der zentralen Verwaltung. Weitere Informationen finden Sie unter [Endpoint Protection in Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

### <a name="enrollment-point"></a>Anmeldungspunkt

Diese Standortsystemrolle verwendet die PKI-Zertifikate für Configuration Manager, um mobile Geräte und macOS-Computer zu registrieren. Diese Rolle wird zwar nur an primären Standorten unterstützt, Sie können jedoch mehrere Instanzen dieser Rolle an einem Standort oder an mehreren Standorten in der gleichen Hierarchie installieren.  

Wenn ein Benutzer mobile Geräte bei Configuration Manager registriert und sein Active Directory-Konto sich in einer Gesamtstruktur befindet, die von der Gesamtstruktur des Standortservers als nicht vertrauenswürdig eingestuft wird, installieren Sie in der Gesamtstruktur des Benutzers einen Registrierungspunkt. Danach kann Configuration Manager den Benutzer authentifizieren.  

### <a name="enrollment-proxy-point"></a>Anmeldungsproxypunkt

Eine Standortsystemrolle, mit der Configuration Manager-Anmeldungsanforderungen von mobilen Geräten und macOS-Computern verwaltet werden. Diese Rolle wird zwar nur an primären Standorten unterstützt, Sie können jedoch mehrere Instanzen dieser Rolle an einem Standort oder an mehreren Standorten in der gleichen Hierarchie installieren.  

Installieren Sie einen Anmeldungsproxypunkt in einem Umkreisnetzwerk und einen im Intranet, wenn Sie mobile Geräte im Internet unterstützen.

### <a name="exchange-server-connector"></a>Exchange Server-Connector

Informationen zu dieser Lösung finden Sie unter [Verwalten mobiler Geräte mit Configuration Manager und Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

### <a name="fallback-status-point"></a>Fallbackstatuspunkt

Eine Standortsystemrolle, die Sie bei der Überwachung der Clientinstallation unterstützt. Sie ermittelt Clients, die nicht verwaltet werden, weil die Kommunikation mit dem zugehörigen Verwaltungspunkt nicht möglich ist. Diese Rolle wird zwar nur an primären Standorten unterstützt, Sie können jedoch mehrere Instanzen dieser Rolle an einem Standort und an mehreren Standorten in der gleichen Hierarchie installieren.

### <a name="management-point"></a>Verwaltungspunkt

Über diese Standortsystemrolle werden Informationen zu Richtlinien und Dienstorten für Clients bereitgestellt. Zudem gehen über diese Rolle Konfigurationsdaten von Clients ein.  

Diese Rolle wird beim Installieren eines neuen primären oder sekundären Standorts standardmäßig auf dem Standortserver installiert. Primäre Standorte unterstützen mehrere Instanzen dieser Rolle. Sekundäre Standorte unterstützen einen einzelnen Verwaltungspunkt. Diese Rolle, die auch als Proxyverwaltungspunkt bezeichnet wird, stellt an einem sekundären Standort einen lokalen Kontaktpunkt bereit, über den Clients Computer- und Benutzerrichtlinien abrufen können.  

Richten Sie Verwaltungspunkte zur Unterstützung von HTTP oder HTTPS ein. Diese können auch mobile Geräte unterstützen, die Sie mit der lokalen Verwaltung mobiler Geräte (Mobile Device Management, MDM) von Configuration Manager verwalten. Verwenden Sie [Datenbankreplikate für Verwaltungspunkte ](../../servers/deploy/configure/database-replicas-for-management-points.md), um die Verarbeitungslast des Standortdatenbankservers mithilfe von Verwaltungspunkten zu verringern, da Verwaltungspunkte Anforderungen von Clients erfüllen.  

### <a name="reporting-services-point"></a>Reporting Services-Punkt

Diese in SQL Server Reporting Services integrierte Standortsystemrolle wird zum Erstellen und Verwalten von Berichten für Configuration Manager verwendet. Diese Rolle wird an primären Standorten und dem Standort der zentralen Verwaltung unterstützt, und Sie können mehrere Instanzen dieser Rolle an einem unterstützten Standort installieren. Weitere Informationen finden Sie unter [Planen der Berichterstellung](../../servers/manage/planning-for-reporting.md).  

### <a name="service-connection-point"></a>Dienstverbindungspunkt

Eine Standortsystemrolle, die Nutzungsdaten von Ihrem Standort hochlädt und erforderlich ist, um Updates für Configuration Manager durchzuführen, die in der Konsole verfügbar sind. Eine Hierarchie unterstützt nur eine einzelne Instanz dieser Rolle, und diese muss sich am Standort der obersten Ebene Ihrer Hierarchie befinden. Wenn Sie einen eigenständigen primären Standort in eine größere Hierarchie erweitern, deinstallieren Sie diese Rolle am primären Standort, und installieren Sie sie anschließend am Standort der zentralen Verwaltung. Weitere Informationen finden Sie unter [About the service connection point (Informationen zum Dienstverbindungspunkt)](../../servers/deploy/configure/about-the-service-connection-point.md).  

### <a name="software-update-point"></a>Softwareupdatepunkt

Diese Standortsystemrolle ist in Windows Server Update Services (WSUS) integriert, um Softwareupdates für Configuration Manager-Clients bereitzustellen. Diese Rolle wird an allen Standorten unterstützt:  

- Installieren Sie dieses Standortsystem am Standort der zentralen Verwaltung, um eine Synchronisierung mit WSUS zu ermöglichen.  

- Richten Sie jede Instanz dieser Rolle an den primären untergeordneten Standorten so ein, dass eine Synchronisierung mit dem Standort der zentralen Verwaltung erfolgt.  

- Erwägen Sie, einen Softwareupdatepunkt an sekundären Standorten zu installieren, wenn die Datenübertragung über das Netzwerk langsam ist.  

Weitere Informationen finden Sie unter [Planen von Softwareupdates](../../../sum/plan-design/plan-for-software-updates.md).  

### <a name="state-migration-point"></a>Zustandsmigrationspunkt

Über diese Standortsystemrolle werden Benutzerzustandsdaten gespeichert, wenn ein Computer zu einem neuen Betriebssystem migriert wird. Diese Rolle wird an untergeordneten primären Standorten oder an sekundären Standorten unterstützt. Installieren Sie mehrere Instanzen dieser Rolle an einem Standort oder an mehreren Standorten in der gleichen Hierarchie. Weitere Informationen zur Speicherung des Benutzerzustands bei der Bereitstellung eines Betriebssystems finden Sie unter [Verwalten des Benutzerzustands](../../../osd/get-started/manage-user-state.md).  


## <a name="next-steps"></a>Nächste Schritte

Einige Configuration Manager-Standortsystemrollen müssen eine Verbindung mit dem Internet herstellen können. Wenn in Ihrer Umgebung ein Proxyserver für den Internetdatenverkehr erforderlich ist, können Sie für Ihre Standortsystemrollen einen Proxy einrichten. Weitere Informationen finden Sie unter [Unterstützung von Proxyservern](../network/proxy-server-support.md).  
