---
title: Cloudverteilungspunkt
titleSuffix: Configuration Manager
description: Planen und Entwerfen der Verteilung von Softwareinhalten in Microsoft Azure über Cloudverteilungspunkte in Configuration Manager.
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3cd9c725-6b42-427d-9191-86e67f84e48c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 52c2b70d2b094d5a89d80aafa61f1db67a53816f
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83987719"
---
# <a name="use-a-cloud-distribution-point-in-configuration-manager"></a>Verwenden eines Cloudverteilungspunkts in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

> [!Important]  
> Die Implementierung für die Freigabe von Inhalten aus Azure hat sich geändert. Verwenden Sie ein inhaltsfähiges Cloud-Management-Gateway, indem Sie die Option **Verwendung dieses Diensts als Cloudverteilungspunkt und zum Verarbeiten von Inhalt aus Azure Storage zulassen** aktivieren. Weitere Informationen finden Sie unter [Ändern eines CMG](../../clients/manage/cmg/setup-cloud-management-gateway.md#modify-a-cmg).
>
> Zukünftig können Sie keinen herkömmlichen Cloudverteilungspunkt mehr erstellen. Weitere Informationen finden Sie unter [Entfernte und veraltete Features](../changes/deprecated/removed-and-deprecated-cmfeatures.md).

Ein Cloudverteilungspunkt ist ein Verteilungspunkt in Configuration Manager, der als Platform-as-a-Service (PaaS) in Microsoft Azure gehostet wird. Dieser Dienst unterstützt die folgenden Szenarios:  

- Bereitstellen von Softwareinhalt an internetbasierte Clients ohne zusätzliche lokale Infrastruktur  

- Verfügbarmachen des Inhaltsverteilungssystems für die Cloud  

- Reduzieren der Notwendigkeit herkömmlicher Verteilungspunkte  

In diesem Artikel erfahren Sie mehr über den Cloudverteilungspunkt, die Planung seiner Verwendung und den Entwurf Ihrer Implementierung. Hierzu gehören folgende Abschnitte:

- [Features und Vorteile](#bkmk_features)
- [Topologieentwurf](#bkmk_topology)
- [Requirements](#bkmk_requirements)
- [Spezifikationen](#bkmk_spec)
- [Kosten](#bkmk_cost)
- [Leistung und Skalierbarkeit](#bkmk_perf)
- [Ports und Datenflüsse](#bkmk_dataflow)
- [Zertifikate](#bkmk_certs)
- [Häufig gestellte Fragen (FAQ)](#bkmk_faq)


## <a name="features-and-benefits"></a><a name="bkmk_features"></a> Features und Vorteile

### <a name="features"></a>Features

Der Cloudverteilungspunkt unterstützt die folgenden Features, die auch von lokalen Verteilungspunkten angeboten werden:  

- Verwaltung von Cloudverteilungspunkten einzeln oder als Mitglieder von Verteilungspunktgruppen  

- Verwendung eines Cloudverteilungspunkts als Fallbackinhaltsquelle  

- Unterstützung von intranet- und internetbasierten Clients  

### <a name="benefits"></a>Vorteile

Cloudverteilungspunkte bieten die folgenden zusätzlichen Vorteile:  

- Die Website verschlüsselt den Inhalt, bevor er an den Cloudverteilungspunkt in Azure übermittelt wird.  

- Um der wachsenden Nachfrage nach Inhaltsanforderungen durch Clients gerecht zu werden, können Sie den Clouddienst manuell in Azure skalieren. Hierfür müssen Sie keine zusätzlichen Verteilungspunkte in Configuration Manager installieren und bereitstellen.  

- Der Inhaltsdownload von Clients, die für andere Inhaltstechnologien konfiguriert wurden, z.B. Windows BranchCache und andere Inhaltsanbieter, wird unterstützt.  

- Ab Version 1806 können Sie Cloudverteilungspunkte als Quellspeicherorte für Pullverteilungspunkte verwenden.  


## <a name="topology-design"></a><a name="bkmk_topology"></a> Topologieentwurf

Die Bereitstellung und der Betrieb des Cloudverteilungspunkts umfassen folgende Komponenten:  

- Einen **Clouddienst** in Azure. Die Website verteilt Inhalt an diesen Dienst, der ihn im Azure-Cloudspeicher speichert. Der Verwaltungspunkt bietet Clients diesen Inhaltsort nach Bedarf in der Liste verfügbarer Quellen an.  

- Die Standortsystemrolle **Verwaltungspunkt** wartet Clientanforderungen regulär.  

    - Lokale Clients verwenden normalerweise einen lokalen Verwaltungspunkt.  

    - Internetbasierte Clients verwenden entweder ein [Cloud Management Gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md) oder einen [internetbasierten Verwaltungspunkt](../../clients/manage/plan-internet-based-client-management.md).  

- Der Cloudverteilungspunkt verwendet einen **zertifikatbasierten HTTPS**-Webdienst für eine sichere Netzwerkkommunikation mit Clients. Clients müssen diesem Zertifikat vertrauen.  

### <a name="azure-resource-manager"></a>Azure Resource Manager

<!--1322209-->
Ab Version 1806 erstellen Sie einen Cloudverteilungspunkt mit einer **Azure Resource Manager-Bereitstellung**. [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) ist eine moderne Plattform zum Verwalten aller Lösungsressourcen als eine einzige Entität, die als [Ressourcengruppe](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups) bezeichnet wird. Beim Bereitstellen eines Cloudverteilungspunkts mit Azure Resource Manager verwendet der Standort Azure Active Directory (Azure AD), um die erforderlichen Cloudressourcen zu authentifizieren und zu erstellen. Für diese modernisierte Bereitstellung ist kein klassisches Azure-Verwaltungszertifikat erforderlich.  

> [!Note]  
> Dieses Feature aktiviert nicht die Unterstützung für Azure-Clouddienstanbieter (Cloud Service Providers, CSP). Die Bereitstellung von Cloudverteilungspunkten mit Azure Resource Manager unterstützt weiterhin den klassischen Clouddienst, der von CSP nicht unterstützt wird. Weitere Informationen finden Sie unter [verfügbare Azure-Dienste in Azure-CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services).  

Ab Configuration Manager Version 1902 ist Azure Resource Manager der einzige Mechanismus zur Bereitstellung neuer Instanzen des Cloudverteilungspunkts. Vorhandene Bereitstellungen funktionieren weiterhin.<!-- 3605704 -->

In Configuration Manager, Version 1810 und früher, bietet der Cloudverteilungspunkt-Assistent weiterhin die Option einer **klassischen Dienstbereitstellung** mit einem Azure-Verwaltungszertifikat. Um die Bereitstellung und Verwaltung von Ressourcen zu vereinfachen, verwenden Sie das Azure Resource Manager-Bereitstellungsmodell für alle neuen Cloudverteilungspunkte. Stellen Sie nach Möglichkeit vorhandene Cloudverteilungspunkte über Resource Manager erneut bereit.

> [!Important]  
> Ab Version 1810 von Configuration Manager ist die Verwendung klassischer Dienstbereitstellungen in Azure veraltet. Diese Version ist die letzte, die das Erstellen dieser Azure-Bereitstellungen unterstützt. Diese Funktionalität wird in einer zukünftigen Version von Configuration Manager entfernt.<!--SCCMDocs-pr issue #2993-->  

Configuration Manager migriert keine vorhandenen klassischen Cloudverteilungspunkte zum Azure Resource Manager-Bereitstellungsmodell. Erstellen Sie neue Cloudverteilungspunkte mit Azure Resource Manager-Bereitstellungen, und entfernen Sie dann klassische Cloudverteilungspunkte.

### <a name="hierarchy-design"></a>Hierarchieentwurf

Der Punkt, an dem Sie Ihren Cloudverteilungspunkt erstellen, hängt von den Clients ab, die Zugriff auf den Inhalt benötigen. Ab Version 1806 gibt es drei Typen von Cloudverteilungspunkten:  

- Azure Resource Manager-Bereitstellung: Erstellen Sie diesen Typ an einem primären Standort oder dem Standort der zentralen Verwaltung.  

- Klassische Dienstbereitstellung: Erstellen Sie diesen Typ nur an einem primären Standort.  

- Cloud Management Gateway kann ebenfalls Inhalt an Clients übermitteln. Diese Funktion reduziert die erforderlichen Zertifikate und Kosten für Azure-VMs. Weitere Informationen finden Sie unter [Planen des Cloudverwaltungsgateways](../../clients/manage/cmg/plan-cloud-management-gateway.md).<!--1358651-->  

Um zu bestimmen, ob Cloudverteilungspunkte in Begrenzungsgruppen aufgenommen werden sollen, können Sie die folgenden Verhaltensweisen in Betracht ziehen:  

- Internetbasierte Clients verlassen sich nicht auf Begrenzungsgruppen. Sie verwenden nur Verteilungspunkte oder Cloudverteilungspunkte mit Internetzugriff. Wenn sie nur Cloudverteilungspunkte verwenden, um diese Clienttypen zu verarbeiten, müssen Sie sie nicht in Begrenzungsgruppen einschließen.  

- Wenn Sie möchten, dass Clients in Ihrem internen Netzwerk einen Cloudverteilungspunkt verwenden, muss sich dieser in derselben Begrenzungsgruppe wie die Clients befinden. Clients räumen Cloudverteilungspunkten in ihrer Liste der Inhaltsquellen die geringste Priorität ein, da mit dem Herunterladen von Inhalten aus Azure Kosten verbunden sind. Daher wird ein Cloudverteilungspunkt normalerweise als Fallbackquelle für intranetbasierte Clients verwendet. Wenn Sie einen Entwurf mit der Cloud an erster Stelle möchten, konfigurieren Sie Ihre Begrenzungsgruppen so, dass sie dieser Unternehmensanforderung gerecht werden. Weitere Informationen finden Sie unter [Configure boundary groups](../../servers/deploy/configure/boundary-groups.md) (Konfigurieren von Begrenzungsgruppen).  

Obwohl Cloudverteilungspunkte in bestimmten Regionen von Azure installiert werden, erfassen Clients keine Azure-Regionen. Sie wählen Cloudverteilungspunkte zufällig aus. Wenn Sie Cloudverteilungspunkte in mehreren Regionen installieren und ein Client mehr als einen Punkt in der Liste der Inhaltsorte empfängt, verwendet der Client möglicherweise keinen Cloudverteilungspunkt aus derselben Azure-Region.  

### <a name="backup-and-recovery"></a>Sicherung und Wiederherstellung  

Wenn Sie einen Cloudverteilungspunkt in der Hierarchie verwenden, dann nutzen Sie folgende Informationen, die bei der Planung der Sicherung und Wiederherstellung hilfreich sind:  

- Wenn Sie den Wartungstask **Standortserver sichern** verwenden, dann werden die Konfigurationen für den Cloudverteilungspunkt automatisch von Configuration Manager berücksichtigt.  

- Sichern und speichern Sie eine Kopie des Serverauthentifizierungszertifikats. Wenn Sie die klassische Dienstbereitstellung in Azure verwenden, sichern und speichern Sie zusätzlich eine Kopie des Azure-Verwaltungszertifikats. Wenn Sie den primären Configuration Manager-Standort auf einem anderen Server wiederherstellen, müssen Sie die Zertifikate erneut importieren.  


## <a name="requirements"></a><a name="bkmk_requirements"></a> Anforderungen

- Sie benötigen ein **Azure-Abonnement** zum Hosten des Diensts.  

    - Ein **Azure-Administrator** muss, abhängig von Ihrem Entwurf, an der Ersterstellung bestimmter Komponenten teilnehmen. Für diese Persona sind keine Berechtigungen in Configuration Manager erforderlich.  

- Der Standortserver benötigt **Internetzugriff** zum Bereitstellen und Verwalten des Clouddiensts.  

- Wenn Sie die **Azure Resource Manager**-Bereitstellungsmethode verwenden, integrieren Sie Configuration Manager mit [Azure Active Directory](../../servers/deploy/configure/azure-services-wizard.md) zur **Cloudverwaltung**. Die Azure Active Directory-*Benutzerermittlung* ist nicht erforderlich.  

- Ein **Serverauthentifizierungszertifikat**. Weitere Informationen finden Sie im Abschnitt [Zertifikate](#bkmk_certs) in diesem Artikel.  

    - Um die Komplexität zu reduzieren, verwenden Sie einen öffentlichen Zertifikatanbieter für das Serverauthentifizierungszertifikat. Dabei benötigen Sie auch ein **CNAME-Alias für DNS**, damit Clients den Namen des Clouddiensts auflösen.  

- Wenn Sie die klassische Azure-Bereitstellungsmethode verwenden, benötigen Sie in Configuration Manager, Version 1810 oder früher, ein **Azure-Verwaltungszertifikat**. Weitere Informationen finden Sie im Abschnitt [Zertifikate](#bkmk_certs) in diesem Artikel.  

    > [!TIP]  
    > Verwenden Sie ab Configuration Manager Version 1806 das **Azure Resource Manager**-Bereitstellungsmodell. Dieses Verwaltungszertifikat ist dafür nicht erforderlich.  
    >
    > Die klassische Bereitstellungsmethode ist ab Version 1810 veraltet.  

- Legen Sie die Clienteinstellung **Allow access to cloud distribution points** (Zugriff auf Cloudverteilungspunkt zulassen) in der Gruppe **Cloud Services** auf **Ja** fest. Dieser Wert ist standardmäßig auf **Nein**eingestellt.  

- Clientgeräte benötigen **Internetkonnektivität** und müssen **IPv4** verwenden.  


## <a name="specifications"></a><a name="bkmk_spec"></a> Spezifikationen

- Der Cloudverteilungspunkt unterstützt alle unter [Unterstützte Betriebssysteme für Clients und Geräte](../configs/supported-operating-systems-for-clients-and-devices.md) aufgeführten Windows-Versionen.  

- Ein Administrator verteilt die folgenden Typen von unterstützten Software-Inhalten:  
  - Applications
  - Pakete
  - Betriebssystemupgradepakete
  - Updates für Drittanbietersoftware  

    > [!Important]  
    > - Während die Configuration Manager-Konsole die Verteilung von Microsoft-Softwareupdates für einen Cloudverteilungspunkt nicht blockiert, fallen Kosten für Azure an, um den Inhalt zu speichern, den Clients nicht verwenden. Internetbasierte Clients erhalten Inhalte der Microsoft-Softwareupdates immer vom Microsoft Update-Clouddienst. Verteilen Sie Microsoft-Softwareupdates nicht für einen Cloudverteilungspunkt.
    > - Bei der Verwendung eines CMG zum Speichern von Inhalten werden die Inhalte für Updates für Drittanbietersoftware nicht auf Clients heruntergeladen, wenn die [Clienteinstellung](../../clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) **Clients das Herunterladen von Deltainhalten ermöglichen (falls verfügbar)** aktiviert ist. <!--6598587--> 

- Konfigurieren Sie ab Version 1806 einen Pullverteilungspunkt, um einen Cloudverteilungspunkt als Quelle zu verwenden. Weitere Informationen finden Sie unter [Informationen zu Quellverteilungspunkten](use-a-pull-distribution-point.md#about-source-distribution-points).<!--1321554-->  

### <a name="deployment-settings"></a>Bereitstellungseinstellungen

- **Inhalt lokal herunterladen, wenn dies für die ausgeführte Tasksequenz erforderlich ist** Ab Version 1910 kann die Tasksequenz-Engine Pakete bei Bedarf von einem für Inhalte aktivierten CMG oder einem Cloudverteilungspunkt herunterladen. Diese Änderung bietet noch mehr Flexibilität für Bereitstellungen von direkten Windows 10-Upgrades auf internetbasierten Geräten.

- **Den gesamten Inhalt vor Starten der Tasksequenz lokal herunterladen** In Configuration Manager, Version 1906 und früher, funktionieren andere Optionen wie **Inhalt lokal herunterladen, wenn dies für die ausgeführte Tasksequenz erforderlich ist** in diesem Szenario nicht. Die Tasksequenzengine kann Inhalte nicht aus einer Cloudquelle herunterladen. Der Configuration Manager-Client muss die Inhalte aus der Cloudquelle herunterladen, bevor die Tasksequenz gestartet wird. Sie können diese Option in der Version 1910 immer noch verwenden, wenn dies erforderlich ist, um Ihren Anforderungen zu entsprechen.

- Ein Cloudverteilungspunkt unterstützt keine Paketbereitstellung mit der Option **Programm vom Verteilungspunkt ausführen**. Verwenden Sie die Bereitstellungsoption **Inhalt vom Verteilungspunkt herunterladen und lokal ausführen**.  

### <a name="limitations"></a>Einschränkungen  

- Ein Cloudverteilungspunkt kann nicht für PXE- oder multicastfähige Bereitstellungen verwendet werden.  

- Ein Cloudverteilungspunkt bietet keine Unterstützung für App-V-Streaminganwendungen.  

- Sie können auf einem Cloudverteilungspunkt keinen [Inhalt vorab bereitstellen](manage-network-bandwidth.md#BKMK_PrestagingContent). Sämtlicher Inhalt wird vom Verteilungs-Manager des primären Standorts übertragen, der den Cloudverteilungspunkt verwaltet.  

- Sie können keinen Cloudverteilungspunkt als Pullverteilungspunkt konfigurieren.  


## <a name="cost"></a><a name="bkmk_cost"></a> Kosten

<!--501018-->
> [!IMPORTANT]  
> Die nachfolgenden Kosteninformationen stellen lediglich Schätzwerte dar. Ihre Umgebung weist möglicherweise andere Variablen auf, die sich auf die Gesamtkosten für die Verwendung eines Cloudverteilungspunkts auswirken.  

Configuration Manager bietet die folgenden Optionen zum Kontrollieren der Kosten und Überwachen des Datenzugriffs:  

- Steuern und überwachen Sie die Menge der Inhalte, die Sie in einem Clouddienst speichern. Weitere Informationen finden Sie unter [Installieren von cloudbasierten Verteilungspunkten](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#bkmk_monitor).  

- Konfigurieren Sie Configuration Manager so, dass Sie gewarnt werden, wenn Schwellenwerte für Clientdownloads monatliche Limits erreichen oder überschreiten. Weitere Informationen finden Sie unter [Data transfer threshold alerts](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#bkmk_alerts) (Warnungen für den Schwellenwert für Datenübertragung).

- Verwenden Sie eine der folgenden Peercachingtechnologien, um die Anzahl von Datenübertragungen von Cloudverteilungspunkten durch Clients zu reduzieren:  
  - Configuration Manager-Peercache
  - Windows BranchCache
  - Windows 10 Übermittlungsoptimierung  

    Weitere Informationen finden Sie unter [Fundamental concepts for content management in System Center Configuration Manager (Grundlegende Konzepte für das Content Management)](fundamental-concepts-for-content-management.md).  

### <a name="components"></a>Komponenten

Ein Cloudverteilungspunkt verwendet folgende Azure-Komponenten, durch die Gebühren für das Azure-Abonnementkonto anfallen:  

> [!Tip]  
> Ab Version 1806 kann Cloud Management Gateway ebenfalls Inhalt an Clients übermitteln. Diese Funktion reduziert die Kosten durch die Konsolidierung der Azure-VMs. Weitere Informationen finden Sie unter [Kosten von Cloud Management Gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md#cost).  

#### <a name="virtual-machine"></a>Virtuelle Maschine

- Der Cloudverteilungspunkt verwendet Azure Cloud Services als Platform-as-a-Service (PaaS). Dieser Dienst verwendet virtuelle Computer (Virtual Machines, VM), durch die Computekosten anfallen.  

- Jeder Cloudverteilungspunktdienst verwendet zwei Standard A0-VMs.  

- Der [Azure-Preisrechner](https://azure.microsoft.com/pricing/calculator/) hilft Ihnen, die potenziellen Kosten zu ermitteln.

    > [!NOTE]  
    > Die Kosten für virtuelle Computer variieren je nach Region.

#### <a name="outbound-data-transfer"></a>Ausgehende Datenübertragungen

- Alle Datenflüsse in Azure sind kostenlos (eingehender Datenverkehr oder Upload). Die Verteilung von Inhalten vom Standort an den Cloudverteilungspunkt erfolgt über das Hochladen in Azure.  

- Die aus Azure fließenden Daten (ausgehender Datenverkehr oder Download) bilden die Grundlage für die Gebühren. Die aus Azure fließenden Cloudverteilungspunkt-Datenflüsse bestehen aus den Softwareinhalten, die von Clients heruntergeladen werden.  

- Weitere Informationen finden Sie unter [Installieren von cloudbasierten Verteilungspunkten](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#bkmk_monitor).  

- Beachten Sie die [Preisübersicht „Bandbreite“ für Azure](https://azure.microsoft.com/pricing/details/bandwidth/), um die potenziellen Kosten zu ermitteln. Die Preise für Datenübertragungen sind gestaffelt. Je größer die Datennutzung ist, desto weniger zahlen Sie pro Gigabyte.  

#### <a name="content-storage"></a>Inhaltsspeicher

- Internetbasierte Clients erhalten kostenlos Inhalte der Microsoft-Softwareupdates vom Microsoft Update-Clouddienst. Verteilen Sie keine Softwareupdate-Bereitstellungspakete mit Microsoft-Softwareupdates ein einen Cloudverteilungspunkt. Andernfalls entstehen Kosten für die Datenspeicherung von Inhalten, die Clients nie verwenden.  

- Cloudverteilungspunkte verwenden je nach Bereitstellungsmodell den folgenden Standardblobspeicher:  

    - Eine Azure Resource Manager-Bereitstellung verwendet lokal redundanten Speicher (LRS) von Azure. Diese Änderung reduziert die Kosten für das Speicherkonto. Die klassische Bereitstellung verwendet keine zusätzlichen Features des GRS. Weitere Informationen finden Sie unter [Lokal redundanter Speicher (LRS)](https://docs.microsoft.com/azure/storage/common/storage-redundancy-lrs).  

    - Klassische Bereitstellungen mit Configuration Manager, Version 1810 oder früher, verwenden georedundanten Speicher (GRS) von Azure. Weitere Informationen finden Sie unter [Georedundanter Speicher (GRS)](https://docs.microsoft.com/azure/storage/common/storage-redundancy-grs).  

#### <a name="other-costs"></a>Sonstige Kosten

- Jeder Clouddienst verfügt über eine dynamische IP-Adresse. Jeder eindeutige Cloudverteilungspunkt verwendet eine neue dynamische IP-Adresse. Durch das Hinzufügen zusätzlicher VMs pro Clouddienst wird die Anzahl dieser Adressen nicht erhöht.  


## <a name="ports-and-data-flow"></a><a name="bkmk_dataflow"></a> Ports und Datenflüsse

Es gibt zwei primäre Datenflüsse für den Cloudverteilungspunkt:  

- Der Standortserver stellt eine Verbindung mit Azure her, um den Cloudverteilungspunktdienst einzurichten.  

- Ein Client stellt eine Verbindung mit dem Cloudverteilungspunkt her, um Inhalt herunterzuladen.  

### <a name="site-server-to-azure"></a>Standortserver zu Azure

Sie müssen keine eingehenden Ports für Ihr lokales Netzwerk öffnen. Der Standortserver initiiert die gesamte Kommunikation mit Azure und dem Cloudverteilungspunkt zum Bereitstellen, Aktualisieren und Verwalten des Clouddiensts. Der Standortserver muss ausgehende Verbindungen mit der Microsoft-Cloud erstellen können. Diese Aktion entspricht der Installation der Standortsystemrolle „Verteilungspunkt“ an einem bestimmten Standort.  

### <a name="client-to-cloud-distribution-point"></a>Client zu Cloudverteilungspunkt

Sie müssen keine eingehenden Ports für Ihr lokales Netzwerk öffnen. Internetbasierte Clients kommunizieren direkt mit dem Azure-Dienst. Clients in Ihrem internen Netzwerk, die einen Cloudverteilungspunkt verwenden, müssen eine Verbindung mit der Microsoft-Cloud herstellen können.

Weitere Informationen zur Priorität des Inhaltsorts und zum Zeitpunkt, zu dem internetbasierte Clients einen Cloudverteilungspunkt verwenden, finden Sie unter [Verteilungspunktpriorität](fundamental-concepts-for-content-management.md#content-source-priority).

Wenn ein Client einen Cloudverteilungspunkt als Inhaltsort verwendet, tritt Folgendes auf:  

1. Der Verwaltungspunkt stellt dem Client ein Zugriffstoken und eine Liste der Inhaltsquellen zur Verfügung. Dieses Token ist 24 Stunden lang gültig und gewährt dem Client Zugriff auf den Cloudverteilungspunkt.  

2. Der Verwaltungspunkt reagiert auf die Anforderung des Speicherorts mit dem **Dienst-FQDN** des Cloudverteilungspunkts. Diese Eigenschaft entspricht dem allgemeinen Namen des Serverauthentifizierungszertifikats.  

    Bei der Verwendung eines Domänennamens, z.B. „WallaceFalls.contoso.com“, versucht der Client zuerst, diesen FQDN aufzulösen. Sie benötigen einen CNAME-Alias im DNS mit Internetzugriff Ihrer Domäne, um den Namen des Azure-Diensts aufzulösen, z.B. „WallaceFalls.cloudapp.net“.  

3. Der Client löst anschließend den Namen des Azure-Diensts, z.B. „WallaceFalls.cloudapp.net“, in eine gültige IP-Adresse auf. Diese Antwort sollte durch Azure DNS behandelt werden.  

4. Der Client stellt eine Verbindung mit dem Cloudverteilungspunkt her. Azure nimmt einen Lastausgleich der Verbindung mit einer der VM-Instanzen vor. Der Client authentifiziert sich mithilfe des Zugriffstokens selbst.  

5. Der Cloudverteilungspunkt authentifiziert das Zugriffstoken des Clients und gibt dem Client den genauen Inhaltsort in Azure Storage zurück.  

6. Wenn der Client dem Serverauthentifizierungszertifikat des Cloudverteilungspunkts vertraut, stellt er eine Verbindung mit Azure Storage her, um den Inhalt herunterzuladen.


## <a name="performance-and-scale"></a><a name="bkmk_perf"></a> Leistung und Skalierbarkeit

<!--494872-->

Wie bei jedem Entwurf eines Verteilungspunkts müssen Sie die folgenden Faktoren bedenken:  

- Anzahl gleichzeitiger Clientverbindungen
- Größe des Inhalts, den der Client herunterlädt
- Zeitraum den Sie für ihre Unternehmensanforderungen benötigen

Abhängig von Ihrem [Topologieentwurf](#bkmk_topology) wählen Clients zufällig innerhalb dieser Clouddienste aus, wenn ein oder mehr Cloudverteilungspunkte für beliebigen Inhalt zur Verfügung stehen. Wenn Sie nur einen bestimmten Teil des Inhalts für einen einzelnen Cloudverteilungspunkt verteilen, und viele Clients diesen Inhalt gleichzeitig herunterladen möchten, führt diese Aktion zu einer höheren Auslastung dieses einzelnen Cloudverteilungspunkts. Das Hinzufügen eines zusätzlichen Cloudverteilungspunkts benötigt auch einen separaten Azure Storage-Dienst. Weitere Informationen dazu, wie der Client mit den Cloudverteilungspunkt-Komponenten kommuniziert und Inhalt herunterlädt, finden Sie unter [Ports und Datenflüsse](#bkmk_dataflow).  

Der Cloudverteilungspunkt verwendet zwei Azure-VMs als Front-End für Azure Storage. Diese Standardbereitstellung wird den Anforderungen der meisten Kunden gerecht. In einigen extremen Fällen mit einer großen Anzahl gleichzeitiger Clientverbindungen (z.B. 150.000 Clients) kann die CPU-Kapazität der Azure-VMs nicht mit den Clientanforderungen Schritt halten. Sie können die Größe der für den Cloudverteilungspunkt verwendeten Azure-VMs nicht ändern. Sie können die Anzahl der VM-Instanzen für den Cloudverteilungspunkt in Configuration Manager nicht ändern. Wenn nötig, können Sie aber den Clouddienst im Azure-Portal neu konfigurieren. Fügen Sie entweder manuell mehr VM-Instanzen hinzu, oder konfigurieren Sie den Dienst für das automatische Skalieren.

> [!Important]  
> Wenn Sie Configuration Manager aktualisieren, stellt der Standort den Clouddienst erneut bereit. Wenn Sie den Clouddienst im Azure-Portal manuell neu konfigurieren, wird die Anzahl der Instanzen auf den Standardwert von zwei Instanzen zurückgesetzt.  

Der Azure Storage-Dienst unterstützt 500 Anforderungen pro Sekunde für eine einzelne Datei. Leistungstests eines einzelnen Cloudverteilungspunkts haben die Verteilung einer einzelnen Datei mit 100 MB auf 50.000 Clients in 24 Stunden unterstützt.<!--512106-->  


## <a name="certificates"></a><a name="bkmk_certs"></a> Zertifikate  

Abhängig vom Entwurf Ihres Cloudverteilungspunkts benötigen Sie ein oder mehrere digitale Zertifikate.  

### <a name="general-information"></a>Allgemeine Informationen

<!--SCCMDocs issue #779-->
Zertifikate für Cloudverteilungspunkte unterstützen die folgenden Konfigurationen:  

- Schlüssellänge von 4096 Bit.

- Zertifikate der Version 3. Weitere Informationen finden Sie in der [Übersicht über CNG-Zertifikate](../network/cng-certificates-overview.md).  

- Ab Version 1802 gilt Folgendes für die Konfiguration von Windows mit der folgenden Richtlinie: **Systemkryptografie: FIPS-konformen Algorithmus für Verschlüsselung, Hashing und Signatur verwenden**.  

- Ab Version 1802 wird TLS 1.2 unterstützt. Weitere Informationen finden Sie in der [technischen Referenz für kryptografische Steuerelemente](../security/cryptographic-controls-technical-reference.md#about-ssl-vulnerabilities).  

### <a name="server-authentication-certificate"></a>Serverauthentifizierungszertifikat

*Dieses Zertifikat ist für alle Bereitstellungen von Cloudverteilungspunkten erforderlich.*

Weitere Informationen finden Sie unter [CMG-Serverauthentifizierungszertifikat](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_serverauth) und bei Bedarf in den folgenden Unterabschnitten:  

- Vertrauenswürdige CMG-Stammzertifikate für Clients
- Von einem öffentlichen Anbieter ausgestellte Serverauthentifizierungszertifikate
- Über eine Unternehmens-PKI ausgestellte Serverauthentifizierungszertifikate

Der Cloudverteilungspunkt verwendet diesen Typ Zertifikat auf die gleiche Weise wie das Cloud Management Gateway. Clients müssen auch diesem Zertifikat vertrauen. Microsoft empfiehlt zur Reduzierung der Komplexität die Verwendung eines Zertifikats, das von einem öffentlichen Anbieter ausgestellt wurde.

Wenn Sie ein Platzhalterzertifikat verwenden, setzten Sie dieses nicht noch einmal ein. Jede Instanz des Cloudverteilungspunkts und Cloud Management Gateways erfordert ein eindeutiges Serverauthentifizierungszertifikat.

Weitere Informationen zum Erstellen dieses Zertifikats über PKI finden Sie unter [Bereitstellen des Dienstzertifikats für cloudbasierte Verteilungspunkte](../network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012).  

### <a name="azure-management-certificate"></a>Azure-Verwaltungszertifikat

*Dieses Zertifikat ist für klassische Dienstbereitstellungen erforderlich. Für Azure Resource Manager-Bereitstellungen wird es nicht benötigt.*

> [!Important]  
> Verwenden Sie ab Configuration Manager Version 1806 das **Azure Resource Manager**-Bereitstellungsmodell. Dieses Verwaltungszertifikat ist dafür nicht erforderlich.  
>
> Die klassische Bereitstellungsmethode ist ab Version 1810 veraltet.  
>
> Ab Configuration Manager Version 1902 ist Azure Resource Manager der einzige Mechanismus zur Bereitstellung neuer Instanzen des Cloudverteilungspunkts. Dieses Zertifikat wird in Configuration Manager, Version 1902 und höher, nicht benötigt.<!-- 3605704 -->

Wenn Sie die klassische Azure-Bereitstellungsmethode mit Configuration Manager, Version 1810 oder früher, verwenden, benötigen Sie ein **Azure-Verwaltungszertifikat**. Weitere Informationen finden Sie im Abschnitt [Azure-Verwaltungszertifikat](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_azuremgmt) des Artikels „Zertifikate für das Cloudverwaltungsgateway“. Der Configuration Manager-Standortserver verwendet dieses Zertifikat zur Authentifizierung mit Azure, um die klassische Bereitstellung zu erstellen und zu verwalten.  

Verwenden Sie zur Reduzierung der Komplexität dasselbe Azure-Verwaltungszertifikat für alle klassischen Bereitstellungen von Cloudverteilungspunkten und Cloud Management Gateways in allen Azure-Abonnements und Configuration Manager-Standorten.


## <a name="frequently-asked-questions-faq"></a><a name="bkmk_faq"></a> Häufig gestellte Fragen (FAQ)

### <a name="does-a-client-need-a-certificate-to-download-content-from-a-cloud-distribution-point"></a>Benötigt ein Client für das Herunterladen von Inhalt von einem Cloudverteilungspunkt ein Zertifikat?

Es ist kein Clientauthentifizierungszertifikat erforderlich. Der Client muss dem Serverauthentifizierungszertifikat nicht vertrauen, das vom Cloudverteilungspunkt verwendet wird. Wenn dieses Zertifikat von einem öffentlichen Zertifikatanbieter ausgestellt wurde, enthalten die meisten Windows-Geräte bereits vertrauenswürdige Stammzertifikate für diese Anbieter. Wenn Sie ein Serverauthentifizierungszertifikat von der PKI Ihrer Organisation ausgestellt haben, müssen Ihre Clients dem Ausstellerzertifikat in der gesamten Kette vertrauen. Diese Kette enthält die Stammzertifizierungsstelle und alle Zwischenzertifizierungsstellen. Abhängig vom PKI-Entwurf kann dieses Zertifikat zu zusätzlicher Komplexität der Bereitstellung des Cloudverteilungspunkts führen. Um diese Komplexität zu vermeiden, empfiehlt Microsoft die Verwendung eines öffentlichen Zertifikatanbieters, dem Ihre Clients bereits vertrauen.  

### <a name="can-my-on-premises-clients-use-a-cloud-distribution-point"></a>Können meine lokalen Clients einen Cloudverteilungspunkt verwenden?

Ja. Wenn Sie möchten, dass Clients in Ihrem internen Netzwerk einen Cloudverteilungspunkt verwenden, muss sich dieser in derselben Begrenzungsgruppe wie die Clients befinden. Clients räumen Cloudverteilungspunkten in ihrer Liste der Inhaltsquellen die geringste Priorität ein, da mit dem Herunterladen von Inhalten aus Azure Kosten verbunden sind. Daher wird ein Cloudverteilungspunkt normalerweise als Fallbackquelle für intranetbasierte Clients verwendet. Wenn Sie einen Entwurf mit der Cloud an erster Stelle möchten, konfigurieren Sie Ihre Begrenzungsgruppen entsprechend. Weitere Informationen finden Sie unter [Configure boundary groups](../../servers/deploy/configure/boundary-groups.md) (Konfigurieren von Begrenzungsgruppen).  

### <a name="do-i-need-azure-expressroute"></a>Benötige ich Azure ExpressRoute?

Mit [Azure ExpressRoute](/azure/expressroute/expressroute-introduction) können Sie Ihr lokales Netzwerk mit der Microsoft-Cloud verbinden und dadurch erweitern. ExpressRoute oder andere virtuelle Netzwerkverbindungen sind nicht für den Cloudverteilungspunkt von Configuration Manager erforderlich.  

Wenn Ihre Organisation ExpressRoute verwendet, isolieren Sie das Azure-Abonnement für den Cloudverteilungspunkt von dem Abonnement, das ExpressRoute verwendet. Durch diese Konfiguration wird verhindert, dass der Cloudverteilungspunkt versehentlich eine Verbindung herstellt.  

### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>Muss ich virtuelle Azure-Computer warten?

Eine Wartung ist nicht erforderlich. Der Entwurf des Cloudverteilungspunkts verwendet die Azure-Plattform als Dienst (PaaS). Mit dem von Ihnen bereitgestellten Abonnement erstellt Configuration Manager die notwendigen VMs, den Speicher und das Netzwerk. Azure sichert und aktualisiert die virtuellen Computer. Anders als bei Infrastructure-as-a-Service (IaaS) sind diese VMs kein Teil Ihrer lokalen Umgebung. Der Cloudverteilungspunkt ist ein PaaS-Dienst, mit dem die Configuration Manager-Umgebung mit der Cloud verbunden und dadurch erweitert wird. Weitere Informationen finden Sie unter [Sicherheitsvorteile eines PaaS-Clouddienstmodells](https://docs.microsoft.com/azure/security/security-paas-deployments#security-advantages-of-a-paas-cloud-service-model).  

### <a name="does-the-cloud-distribution-point-use-azure-cdn"></a>Verwendet der Cloudverteilungspunkt Azure CDN?

Azure Content Delivery Network (CDN) ist eine weltweite Lösung für die schnelle Lieferung von Inhalt mit hoher Bandbreite, indem der Inhalt an strategisch platzierten physischen Knoten auf der ganzen Welt zwischengespeichert wird. Weitere Informationen finden Sie unter [Was ist ein Content Delivery Network?](https://docs.microsoft.com/azure/cdn/cdn-overview).

Der Cloudverteilungspunkt von Configuration Manager unterstützt Azure CDN derzeit nicht.


## <a name="next-steps"></a>Nächste Schritte

[Installieren von cloudbasierten Verteilungspunkten](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)
