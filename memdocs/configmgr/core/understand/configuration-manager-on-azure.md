---
title: Configuration Manager in Azure
titleSuffix: Configuration Manager
description: Informationen zur Verwendung von Configuration Manager in einer Azure-Umgebung.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d24257d8-8136-47f4-8e0d-34021356dc37
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c9d398d7fddab61014547fc0f8f64cd180e58ab6
ms.sourcegitcommit: 8a4a86ee8044f273dcece26155132a801f3d8f9a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/30/2020
ms.locfileid: "87438577"
---
# <a name="configuration-manager-on-azure---frequently-asked-questions"></a>Configuration Manager in Azure – Häufig gestellte Fragen

*Gilt für: Configuration Manager (Current Branch)*

Die folgenden Fragen und Antworten können Ihnen helfen, zu verstehen, wann Sie Configuration Manager in Microsoft Azure verwenden und wie Sie diesen konfigurieren können.

## <a name="general-questions"></a>Allgemeine Fragen
### <a name="my-company-is-trying-to-move-as-many-physical-servers-as-possible-to-microsoft-azure-can-i-move-configuration-manager-servers-to-azure"></a>Mein Unternehmen versucht, so viele physische Server wie möglich in Microsoft Azure zu verschieben. Kann ich Configuration Manager-Server in Azure verschieben?
Dabei handelt es sich durchaus um ein unterstütztes Szenario.  Weitere Informationen finden Sie unter [Unterstützung für Virtualisierungsumgebungen für Configuration Manager](../plan-design/configs/support-for-virtualization-environments.md).

### <a name="great-my-environment-requires-multiple-sites-should-all-child-primary-sites-be-in-azure-with-the-central-administration-site-or-on-premises-what-about-secondary-sites"></a>Sehr gut! Meine Umgebung erfordert mehrere Standorte. Sollten sich alle untergeordneten primären Standorte mit dem Standort der zentralen Verwaltung oder lokal in Azure befinden? Wie sieht es mit sekundären Standorten aus?
Die Standort-zu-Standort-Kommunikation (dateibasierte Replikation und Datenbankreplikation) profitiert dadurch, dass sie in Azure gehostet wird, von der Nähe. Der gesamte clientbezogene Datenverkehr erfolgt jedoch remote von Standortservern und Standortsystemen aus. Wenn Sie eine schnelle und zuverlässige Netzwerkverbindung zwischen Azure und Ihrem Intranet mit einem unbegrenzten Datentarif verwenden, stellt das Hosten Ihrer gesamten Infrastruktur in Azure eine Option dar.

Wenn Sie jedoch einen Volumentarif verwenden und die verfügbare Bandbreite bzw. Kosten eine Rolle spielen, oder wenn die Netzwerkverbindung zwischen Azure und Ihrem Intranet nicht schnell und nicht immer zuverlässig ist, ziehen Sie in Betracht, spezifische Standorte (und Standortsysteme) lokal zu platzieren und anschließend die in Configuration Manager integrierte Bandbreitensteuerung zu verwenden.

### <a name="is-having-configuration-manager-in-azure-a-saas-scenario-software-as-a-service"></a>Handelt es sich bei Configuration Manager in Azure um ein SaaS-Szenario (Software-as-a-Service)?
Nein, es handelt sich um ein IaaS-Szenario (Infrastructure-as-a-Service), da Sie Ihre Configuration Manager-Infrastrukturserver in virtuellen Azure-Computern hosten.

### <a name="what-areas-should-i-pay-attention-to-when-considering-a-move-of-my-configuration-manager-infrastructure-to-azure"></a>Auf welche Bereiche sollte ich achten, wenn ich das Verschieben meiner Configuration Manager-Infrastruktur in Azure in Betracht ziehe?
Das ist eine gute Frage. Die folgenden Bereiche sind bei dieser Entscheidung am wichtigsten, jeder dieser Bereiche wird in einem separaten Abschnitt dieses Themas behandelt:
1. Netzwerk
2. Verfügbarkeit
3. Leistung
4. Kosten
5. Benutzererfahrung

## <a name="networking"></a>Netzwerk
### <a name="what-about-networking-requirements-should-i-use-expressroute-or-an-azure-vpn-gateway"></a>Wie sieht es mit Netzwerkanforderungen aus? Sollte ich ExpressRoute oder ein Azure-VPN Gateway verwenden?
Die Netzwerkentscheidung ist eine sehr wichtige Entscheidung. Die Netzwerkgeschwindigkeit und -latenz kann sich auf die Funktionalität zwischen dem Standortserver und Remotestandortsystemen sowie auf jegliche Clienkommunikation mit den Standortsystemen auswirken. Wir empfehlen, ExpressRoute zu verwenden. Allerdings gibt es keine Configuration Manager-Einschränkung, die Sie davon abhält, ein Azure-VPN Gateway zu verwenden. Sie sollten Ihre Anforderungen von dieser Infrastruktur sorgfältig überprüfen (Leistung, Patchen, Softwareverteilung, Betriebssystembereitstellung) und anschließend Ihre Entscheidung treffen. Folgendes sollte bei jeder Lösung berücksichtigt werden:

- **ExpressRoute** (empfohlen)
  - Natürliche Erweiterung Ihres Rechenzentrums (kann mehrere Rechenzentren verbinden)
  - Private Verbindungen zwischen Azure-Rechenzentren und Ihrer Infrastruktur
  - Datenverkehr erfolgt nicht über das öffentliche Internet
  - Bietet Zuverlässigkeit, hohe Geschwindigkeit, geringere Latenz, hohe Sicherheit
  - Bietet eine Geschwindigkeit von bis zu 10 Gbit/s sowie Optionen für einen unbegrenzten Datentarif
- **VPN Gateway**
  - Standort-zu-Standort/Punkt-zu-Standort-VPNs
  - Datenverkehr erfolgt über das öffentliche Internet
  - Verwendet Internetprotokollsicherheit (IPsec) und Internetschlüsselaustausch (IKE)

### <a name="expressroute-has-many-different-options-like-unlimited-vs-metered-different-speed-options-and-premium-add-on-which-should-i-choose"></a>ExpressRoute verfügt über viele verschiedene Optionen wie den unbegrenzten Datentarif im Vergleich zum Volumentarif, andere Geschwindigkeitsoptionen und das Premium-Add-On. Welche sollte ich auswählen?
Welche Optionen Sie auswählen hängt von dem Szenario ab, das Sie implementieren sowie von der Menge an Daten, die Sie planen zu verteilen. Die Übertragung von Configuration Manager-Daten zwischen Standortservern und Verteilungspunkten kann gesteuert werden, die Kommunikation von Standortserver zu Standortserver kann jedoch nicht gesteuert werden.   Wenn Sie einen Volumentarif verwenden, können Sie durch das lokale Platzieren von spezifischen Standorten (und Standortsystemen) und mithilfe der [in Configuration Manager integrierten Bandbreitensteuerelemente](../plan-design/hierarchy/fundamental-concepts-for-content-management.md) die Kosten kontrollieren, die durch die Verwendung von Azure anfallen.

### <a name="what-about-installation-requirements-like-active-directory-domains-do-i-still-need-to-join-my-site-servers-to-an-active-directory-domain"></a>Wie sieht es mit Installationsanforderungen wie Active Directory-Domänen aus? Muss ich meine Standortserver immer noch mit einer Active Directory-Domäne verknüpfen?
Ja. Wenn Sie in Azure verschieben, bleiben die [unterstützten Konfigurationen](../plan-design/configs/supported-configurations.md) unverändert, einschließlich der Active Directory-Anforderungen für das Installieren von Configuration Manager.

### <a name="i-understand-the-need-to-join-my-site-servers-to-an-active-directory-domain-but-can-i-use-azure-active-directory"></a>Ich verstehe, dass ich meine Standortserver mit einer Active Directory-Domäne verknüpfen muss, kann ich jedoch Azure Active Directory verwenden?
Nein, Azure Active Directory wird derzeit nicht unterstützt. Ihre Standortsysteme müssen immer noch Mitglieder einer [Windows Active Directory-Domäne](../plan-design/configs/support-for-active-directory-domains.md) sein.



## <a name="availability"></a>Verfügbarkeit
### <a name="one-of-the-reasons-i-am-moving-infrastructure-to-azure-is-the-promise-of-high-availability-can-i-take-advantage-of-high-availability-options-like-azure-vm-availability-sets-for-vms-that-i-will-use-for-configuration-manager"></a>Einer der Gründe, aus denen ich meine Infrastruktur in Azure verschiebe, ist das Versprechen der hohen Verfügbarkeit. Kann ich Optionen für hohe Verfügbarkeit wie Azure-VM-Verfügbarkeitsgruppen für VMs nutzen, die ich für Configuration Manager verwenden werde?
Ja! Azure-VM-Verfügbarkeitsgruppen können für redundante Standortsystemrollen wie Verteilungspunkte oder Verwaltungspunkte verwendet werden.

Sie können sie auch für die Configuration Manager-Standortserver verwenden. Beispielsweise können sich Standorte der zentralen Verwaltung und primäre Standorte alle in derselben Verfügbarkeitsgruppe befinden, wodurch Sie sicherstellen können, dass sie nicht alle zur gleichen Zeit neu gestartet werden.

### <a name="how-can-i-make-my-database-highly-available-can-i-use-azure-sql-database-or-do-i-have-to-use-microsoft-sql-server-in-a-vm"></a>Wie kann ich meine Datenbank hoch verfügbar machen? Kann ich Azure SQL-Datenbank verwenden? Oder muss ich auf einer VM Microsoft SQL Server verwenden?
Sie müssen auf einer VM Microsoft SQL Server verwenden. Azure SQL Server wird von Configuration Manager derzeit nicht unterstützt. Sie können jedoch Funktionen wie Always On-Verfügbarkeitsgruppen für Ihren SQL Server verwenden. [Always On-Verfügbarkeitsgruppen](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md) werden empfohlen und ab Version 1602 von Configuration Manager offiziell unterstützt.

### <a name="can-i-use-azure-load-balancers-with-site-system-roles-like-management-points--or-software-update-points"></a>Kann ich Azure Load Balancer mit Standortsystemrollen wie Verwaltungspunkten oder Softwareupdatepunkten verwenden?
Obwohl Configuration Manager nicht mit Azure Load Balancer getestet wurde, sollte dies keine negativen Auswirkungen auf normale Vorgänge haben, wenn die Funktionalität für die Anwendung transparent ist.


## <a name="performance"></a>Leistung
### <a name="what-factors-affect-performance-in-this-scenario"></a>Welche Faktoren beeinflussen die Leistung in diesem Szenario?
[Azure-VM-Größe und -Typ](/azure/virtual-machines/sizes), Azure-VM-Datenträger (Storage Premium wird empfohlen, vor allem für SQL Server), Netzwerklatenz und Geschwindigkeit sind die wichtigsten Bereiche.

### <a name="so-tell-me-more-about-azure-virtual-machines-what-size-vms-should-i-use"></a>Erzählen Sie mir also mehr über virtuelle Azure-Computer, welche VM-Größe sollte ich verwenden?
Im Allgemeinen muss Ihre Rechenleistung (CPU und Arbeitsspeicher) der [empfohlenen Hardware für Configuration Manager](../plan-design/configs/recommended-hardware.md) entsprechen. Es bestehen jedoch einige Unterschiede zwischen regulärer Computerhardware und Azure-VMs, besonders bei den Datenträgern, die von diesen VMs verwendet werden.  Welche VM-Größe Sie verwenden, hängt von der Größe Ihrer Umgebung ab. Im Folgenden finden Sie jedoch einige Empfehlungen:
- Für Produktionsbereitstellungen von signifikanter Größe empfehlen wir Azure-VMs der Klasse „**S**“. Der Grund dafür ist, dass diese Storage Premium-Datenträger nutzen können.  VMs, die nicht zur Klasse „S“ gehören, verwenden Blob Storage und erfüllen in der Regel die Anforderungen für eine akzeptable Produktionserfahrung nicht.
- Mehrere Storage Premium-Datenträger sollten für eine höhere Skalierung verwendet und für maximale IOPS in der Windows-Datenverwaltungskonsole in Stripes aufgeteilt werden.  
- Wir empfehlen die Verwendung besserer oder mehrerer Premium-Datenträger während der Erstbereitstellung Ihres Standorts (wie P30 statt P20 und 2xP30 in einem Stripesetvolume statt 1xP30). Wenn Ihr Standort dann später aufgrund zusätzlicher Last hinsichtlich der VM-Größe aufgestockt werden muss, können Sie die zusätzliche CPU und den zusätzlichen Speicher verwenden, die bzw. den eine größere VM-Größe bietet. Außerdem verfügen Sie dadurch bereits über Datenträger, die den zusätzlichen IOPS-Durchsatz nutzen können, der durch eine größere VM-Größe ermöglicht wird.



Die folgenden Tabellen enthalten die anfänglich vorgeschlagene Anzahl von Datenträgern, die an Standorten der primären und zentralen Verwaltung für verschiedene Größeninstallationen verwendet werden sollen:

**Zusammengestellte Standortdatenbank** – Standort der primären oder zentralen Verwaltung mit der Standortdatenbank auf dem Standortserver:

| Desktopclients    |Empfohlene VM-Größe|Empfohlene Datenträger|
|--------------------|-------------------|-----------------|
|**Bis zu 25.000**       |   DS4_V2          |2xP30 (Stripeset)  |
|**25.000-50.000**      |   DS13_V2         |2xP30 (Stripeset)  |
|**50.000-100.000**     |   DS14_V2         |3xP30 (Stripeset)  |


**Remotestandortdatenbank** – Standort der primären oder zentralen Verwaltung mit der Standortdatenbank auf einem Remoteserver:

| Desktopclients    |Empfohlene VM-Größe|Empfohlene Datenträger |
|--------------------|-------------------|------------------|
|**Bis zu 25.000**       | Standortserver: F4S </br>Datenbankserver: DS12_V2 | Standortserver: 1xP30 </br>Datenbankserver: 2xP30 (Stripeset)  |
|**25.000-50.000**      | Standortserver: F4S </br>Datenbankserver: DS13_V2 | Standortserver: 1xP30 </br>Datenbankserver: 2xP30 (Stripeset)   |
|**50.000-100.000**     | Standortserver: F8S </br>Datenbankserver: DS14_V2 | Standortserver: 2xP30 (Stripeset)   </br>Datenbankserver: 3xP30 (Stripeset)   |

Die folgende Abbildung zeigt eine Beispielkonfiguration für 50.000 bis 100.000 Clients auf DS14_V2 mit 3xP30-Datenträgern in einem Stripesetvolume mit separaten logischen Volumes für die Installations- und Datenbankdateien von Configuration Manager: ![VM-Datenträger](media/vm_disks.png)  



## <a name="user-experience"></a>Benutzererfahrung
### <a name="you-mention-that-user-experience-is-one-of-the-main-areas-of-importance-why-is-that"></a>Sie erwähnen, dass die Benutzerfreundlichkeit einen der wichtigsten Bereiche darstellt. Wieso ist das so?
Die Entscheidungen, die Sie hinsichtlich Netzwerk, Verfügbarkeit, Leistung und Platzieren Ihrer Configuration Manager-Standortserver treffen, können direkte Auswirkungen auf Ihre Benutzer haben. Wir glauben, dass das Verschieben in Azure für Ihre Benutzer transparent sein sollte, damit keine Veränderungen in deren täglichen Interaktionen mit Configuration Manager auftreten.

### <a name="ok-i-get-it-i-plan-to-install-a-single-stand-alone-primary-site-on-an-azure-virtual-machine-and-i-want-to-make-sure-my-costs-are-low-should-i-place-remote-site-systems-like-management-points-distribution-points-and-software-update-points-on-azure-virtual-machines-as-well-or-on-premises"></a>OK, das verstehe ich. Ich plane die Installation eines eigenständigen primären Standorts auf einer Azure-VM und möchte sicherstellen, dass die Kosten dafür gering sind. Sollte ich (Remote-) Standortsysteme (wie Verwaltungspunkte, Verteilungspunkte und Softwareupdatepunkte) auch auf Azure-VMs platzieren oder lokal?
Die Kommunikation zwischen den Servern an einem Standort kann jederzeit und ohne Steuerung der Verwendung der Netzwerkbandbreite auftreten. Dies trifft nicht auf die Kommunikation zwischen dem Standortserver und einem Verteilungspunkt zu. Da Sie die Kommunikation zwischen Standortsystemen nicht steuern können, sollten jegliche mit dieser Kommunikation in Verbindung stehenden Kosten berücksichtigt werden.

Die Netzwerkgeschwindigkeit und -latenz sind weitere Faktoren, die berücksichtigt werden sollten. Langsame oder unzuverlässige Netzwerke könnten sich auf die Funktionalität zwischen dem Standortserver und Remotestandortsystemen sowie auf jegliche Clienkommunikation mit den Standortsystemen auswirken. Die Anzahl der verwalteten Clients, die ein bestimmtes Standortsystem verwenden, sowie die Funktionen, die Sie aktiv verwenden, sollten ebenfalls berücksichtigt werden.
Im Allgemeinen können Sie die normale Anleitung nutzen, da sich diese auf WAN-Links und Standortsysteme als Startpunkt bezieht. Im Idealfall wird der Netzwerkdurchsatz zwischen Azure und Ihrem Intranet, den Sie auswählen und empfangen, mit einem WAN übereinstimmen, das gut mit einem schnellen Netzwerk verbunden ist.

### <a name="what-about-content-distribution-and-content-management-should-standard-distribution-points-be-in-azure-or-on-premises-and-should-i-use-branchcache-or-pull-distribution-points-on-premises-or-should-i-make-exclusive-use-of-cloud-distribution-points"></a>Wie sieht es mit der Inhaltsverteilung und Content Management aus? Sollten sich Standardverteilungspunkte in Azure oder lokal befinden, und sollte Ich BranchCache oder Pullverteilungspunkte lokal verwenden? Oder sollte ich Cloudverteilungspunkte exklusiv verwenden?
Der Ansatz für das Content Management ist ähnlich wie bei Standortservern und Standortsystemen.
- Wenn Sie eine schnelle und zuverlässige Netzwerkverbindung zwischen Azure und Ihrem Intranet mit einem unbegrenzten Datentarif verwenden, könnte das Hosten von Standardverteilungspunkten in Azure eine Option darstellen.
- Wenn Sie einen Volumentarif verwenden und Bandbreitenkosten eine Rolle spielen oder die Netzwerkverbindung zwischen Azure und Ihrem Intranet nicht schnell oder nicht immer zuverlässig ist, ziehen Sie möglicherweise andere Ansätze in Betracht. Hierzu gehören das Suchen von lokalen Standard- oder Pullverteilungspunkten sowie das Verwenden von BranchCache. Die Verwendung von cloudbasierten Verteilungspunkten ist ebenfalls eine Option, jedoch gelten einige Einschränkungen bei den unterstützten Inhaltstypen (z.B. kein Support für Softwareupdatepakete).

> [!NOTE]
>  Wenn PXE- oder Multicast-Support erforderlich ist, müssen Sie lokale Verteilungspunkte (Standard oder Pull) verwenden, um auf Startanforderungen zu reagieren.


### <a name="while-i-am-ok-with-the-limitations-of-cloud-based-distribution-points-i-dont-want-to-put-my-management-point-into-a-dmz-even-though-that-is-needed-to-support-my-internet-based-clients-do-i-have-any-other-options"></a>Die Einschränkungen cloudbasierter Verteilungspunkte sind für mich in Ordnung, trotzdem möchte ich meinen Verwaltungspunkt nicht in einer DMZ platzieren, obwohl dies für den Support meiner internetbasierten Clients erforderlich ist. Stehen mir irgendwelche anderen Optionen zur Verfügung?
Ja! Mit Version 1610 von Configuration Manager wurde das [Cloudverwaltungsgateway](../clients/manage/manage-clients-internet.md#cloud-management-gateway) als Vorabfunktion eingeführt. (Dieses Feature erschien in der Technical Preview-Version 1606 zunächst als [Cloudproxydienst](../get-started/capabilities-in-technical-preview-1606.md#cloud_proxy)).

Das **Cloud Management Gateway** bietet eine einfache Möglichkeit zum Verwalten von Configuration Manager-Clients im Internet. Der Dienst, der in Microsoft Azure bereitgestellt wird und ein Azure-Abonnement erfordert, stellt mithilfe einer neuen Rolle namens Cloudverwaltungsgateway eine Verbindung mit Ihrer lokalen Configuration Manager-Infrastruktur her. Nachdem er bereitgestellt und konfiguriert wurde, können Clients auf lokale Configuration Manager-Standortsystemrollen zugreifen, unabhängig davon, ob sie mit dem internen, privaten Netzwerk oder über das Internet verbunden sind.

Sie können damit beginnen, das Cloudverwaltungsgateway in Ihrer Umgebung zu testen und uns Feedback zu geben, um es zu verbessern. Weitere Informationen finden Sie unter [Use pre-release features from updates (Verwenden von Vorabfeatures aus Updates)](../servers/manage/install-in-console-updates.md#bkmk_prerelease).

### <a name="i-also-heard-that-you-have-another-new-feature-called-peer-cache-introduced-as-a-pre-release-feature-in-version-1610-is-that-different-than-branchcache-which-one-should-i-choose"></a>Außerdem habe ich gehört, dass es eine weitere neue Funktion namens Peercache gibt, die vorab in der Version 1610 eingeführt wurde. Unterscheidet sich diese von BranchCache? Welche sollte ich auswählen?
Ja, sie unterscheidet sich komplett. Bei [Peercache](../plan-design/hierarchy/client-peer-cache.md) handelt es sich um eine 100% native Configuration Manager-Technologie, wobei BranchCache eine Windows-Funktion ist. Beide können hilfreich sein. BranchCache verwendet eine Übertragung, um den erforderlichen Inhalt zu suchen, während Peercache den üblichen Verteilungsworkflow und die Begrenzungsgruppeneinstellungen von Configuration Manager verwendet.

Sie können jeden Client so konfigurieren, dass er eine Peercache-Quelle darstellt. Wenn Verwaltungspunkte Clients anschließend Informationen zu Quellspeicherorten für Inhalt bereitstellen, bieten sie Details sowohl zu den Verteilungspunkten als auch zu allen Peercache-Quellen, die über den Inhalt verfügen, den der Client benötigt.


## <a name="cost"></a>Kosten
### <a name="ok-tell-me-a-bit-about-the-cost-will-this-be-a-cost-effective-solution-for-me"></a>OK, erzählen Sie mir etwas über die Kosten. Wird das eine kostengünstige Lösung für mich sein?
Das ist schwer zu sagen, da jede Umgebung anders ist. Am besten ermitteln Sie die Kosten für Ihre Umgebung, indem Sie den Preisrechner von Microsoft Azure verwenden: https://azure.microsoft.com/pricing/calculator/.

## <a name="additional-resources"></a>Zusätzliche Ressourcen
**Grundlagen:** https://azure.microsoft.com/documentation/articles/fundamentals-introduction-to-azure/

**Azure-VM-Computertypen:**
- Größe von Azure-Computern: https://docs.microsoft.com/azure/virtual-machines/sizes  
- VM-Preise: https://azure.microsoft.com/pricing/details/virtual-machines/  
- Speicherpreise: https://azure.microsoft.com/pricing/details/storage/

**Überlegungen zur Datenträgerleistung:**    
- Einführung in Premium-Datenträger: https://azure.microsoft.com/blog/2014/12/11/introducing-premium-storage-high-performance-storage-for-azure-virtual-machine-workloads/  
- Ausführlichere Informationen zu Premium-Datenträgern: https://azure.microsoft.com/documentation/articles/storage-premium-storage-preview-portal/   
- Praktische Sammlung von Diagrammen für die maximale Größe und die Leistungsziele der Speicherung: https://azure.microsoft.com/documentation/articles/storage-scalability-targets/  
- Eine weitere Einführung und einige interessante Profi-Daten zur Funktionsweise von Storage Premium hinter den Kulissen: https://azure.microsoft.com/blog/2015/04/16/azure-premium-storage-now-generally-available-2/

**Verfügbarkeit:**
- Azure IaaS-Betriebszeit-SLAs: https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/  
- Erklärungen zu Verfügbarkeitsgruppen: https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability

**Konnektivität:**
- ExpressRoute im Vergleich zu Azure-VPN: https://azure.microsoft.com/blog/2014/06/10/expressroute-or-virtual-network-vpn-whats-right-for-me/
- ExpressRoute-Preise: https://azure.microsoft.com/pricing/details/expressroute/
- Weitere Informationen zu ExpressRoute: https://azure.microsoft.com/documentation/articles/expressroute-introduction/
