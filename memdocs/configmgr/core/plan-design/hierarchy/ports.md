---
title: Für Verbindungen verwendete Ports
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über die erforderlichen und anpassbaren Netzwerkports, die Configuration Manager für Verbindungen verwendet.
ms.date: 04/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c6777fb0-0754-4abf-8a1b-7639d23e9391
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b75ebe7e768080a1239e817c514b634cdcf64179
ms.sourcegitcommit: b7e5b053dfa260e7383a9744558d50245f2bccdc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/29/2020
ms.locfileid: "82587163"
---
# <a name="ports-used-in-configuration-manager"></a>In Configuration Manager verwendete Ports

*Gilt für: Configuration Manager (Current Branch)*

Dieser Artikel listet die von Configuration Manager verwendeten Netzwerkports auf. Bei einigen Verbindungen werden nicht konfigurierbare Ports verwendet, bei anderen werden benutzerdefinierte Ports unterstützt. Wenn Sie eine Portfiltertechnologie verwenden, stellen Sie sicher, dass die erforderlichen Ports verfügbar sind. Zu diesen Portfiltertechnologien gehören Firewalls, Router, Proxyserver oder IPsec.

> [!NOTE]  
> Wenn Sie internetbasierte Clients über SSL-Bridging unterstützen, müssen Sie möglicherweise zusätzlich zu den Portanforderungen bestimmten HTTP-Verben und -Headern ermöglichen, ihre Firewall zu passieren.

## <a name="ports-you-can-configure"></a><a name="BKMK_ConfigurablePorts"></a> Konfigurierbare Ports

Configuration Manager ermöglicht die Portkonfiguration für folgende Kommunikationsarten:  

- Anwendungskatalog-Websitepunkt zu Anwendungskatalog-Webdienstpunkt  

- Anmeldungsproxypunkt zu Anmeldungspunkt  

- Systeme zwischen Client und Standort, auf denen IIS ausgeführt wird  

- Client zu Internet (als Proxyservereinstellungen)  

- Softwareupdatepunkt zu Internet (als Proxyservereinstellungen)  

- Softwareupdatepunkt zu WSUS-Server  

- Standortserver zu Standortdatenbankserver  

- Standortserver zu WSUS-Datenbankserver

- Reporting Services-Punkte  

  > [!NOTE]  
  > Die Ports, die für die Standortsystemrolle des Reporting Services-Punkts verwendet werden, werden in SQL Server Reporting Services konfiguriert. Diese Ports werden dann von Configuration Manager zur Kommunikation mit dem Reporting Services-Punkt verwendet. Achten Sie darauf, diese Ports beim Definieren der IP-Filterinformationen für IPsec-Richtlinien oder beim Konfigurieren von Firewalls zu überprüfen.  

Für die Kommunikation zwischen Client und Standortsystem werden standardmäßig HTTP-Port 80 und HTTPS-Port 443 verwendet. Die Ports für die Kommunikation zwischen Client und Standortsystem über HTTP oder HTTPS können während des Setups oder in den Standorteigenschaften für Ihren Configuration Manager-Standort geändert werden.  

Die Ports, die für die Standortsystemrolle des Reporting Services-Punkts verwendet werden, werden in SQL Server Reporting Services konfiguriert. Diese Ports werden dann von Configuration Manager zur Kommunikation mit dem Reporting Services-Punkt verwendet. Achten Sie darauf, diese Ports beim Definieren der IP-Filterinformationen für IPsec-Richtlinien oder beim Konfigurieren von Firewalls zu überprüfen.  

## <a name="non-configurable-ports"></a><a name="BKMK_NonConfigurablePorts"></a> Nicht konfigurierbare Ports  

Configuration Manager lässt keine Portkonfiguration für folgende Kommunikationsarten zu:  

- Standort zu Standort  

- Standortserver zu Standortsystem  

- Configuration Manager-Konsole für SMS-Anbieter  

- Configuration Manager-Konsole zu Internet  

- Verbindungen mit Clouddiensten, z. B. Microsoft Intune und Cloudverteilungspunkten  

## <a name="ports-used-by-configuration-manager-clients-and-site-systems"></a><a name="BKMK_CommunicationPorts"></a> Von Configuration Manager-Clients und Standortsystemen verwendete Ports  

In den folgenden Abschnitten sind die Ports beschrieben, die für die Kommunikation in Configuration Manager verwendet werden. Die Pfeile in den Abschnittstiteln zeigen die Kommunikationsrichtung an:  

- > gibt an, dass ein Computer die Kommunikation startet und der andere Computer immer antwortet  

- &lt; > gibt an, dass beide Computer die Kommunikation starten können  

### <a name="asset-intelligence-synchronization-point----microsoft"></a><a name="BKMK_PortsAI"></a> Asset Intelligence-Synchronisierungspunkt > Microsoft  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

### <a name="asset-intelligence-synchronization-point----sql-server"></a><a name="BKMK_PortsAI-to-SQL"></a> Asset Intelligence-Synchronisierungspunkt > SQL Server  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|SQL über TCP|--|1433 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|  

### <a name="application-catalog-web-service-point----sql-server"></a><a name="BKMK_PortsAppCatalogService-SQL"></a> Anwendungskatalog-Webdienstpunkt > SQL Server  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|SQL über TCP|--|1433 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|  

### <a name="application-catalog-website-point----application-catalog-web-service-point"></a><a name="BKMK_PortsAppCatalogWebSitePoint_AppCatalogWebServicePoint"></a> Anwendungskatalog-Websitepunkt > Anwendungskatalog-Webdienstpunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|  
|HTTPS|--|443 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|  

### <a name="client----application-catalog-website-point"></a><a name="BKMK_PortsClient-AppCatalogWebsitePoint"></a> Client > Anwendungskatalog-Websitepunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|  
|HTTPS|--|443 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|  

### <a name="client----client"></a><a name="BKMK_PortsClient-ClientWakeUp"></a> Client > Client  

Der Aktivierungsproxy verwendet auch ICMP-Echoanforderungsmeldungen von einem Client zu einem anderen Client. Clients verwenden diese Kommunikation, um zu überprüfen, ob der andere Client im Netzwerk aktiviert ist. ICMP (Internet Control Message Protocol) wird gelegentlich als Ping-Befehle bezeichnet. ICMP hat keine UDP- oder TCP-Protokollnummer und wird daher in der folgenden Tabelle nicht aufgeführt. Von allen hostbasierten Firewalls auf diesen Clientcomputern oder beteiligten Netzwerkgeräten im Subnetz muss jedoch der ICMP-Datenverkehr zugelassen werden, damit die Aktivierungsproxykommunikation erfolgreich durchgeführt werden kann.  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|-Wake-On-LAN|9 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|--|  
|Aktivierungsproxy|25536 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|--|  
|Windows PE-Peercacheübertragung|8004|--|  
|Windows PE-Peercachedownload|--|8003|  

Weitere Informationen finden Sie unter [Windows PE-Peercache](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md#BKMK_PeerCacheRequirements).

### <a name="client----configuration-manager-network-device-enrollment-service-ndes-policy-module"></a><a name="BKMK_PortsClient-PolicyModule"></a> Client > Configuration Manager-Richtlinienmodul des Registrierungsdiensts für Netzwerkgeräte (NDES)

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP||80|  
|HTTPS|--|443|  

### <a name="client----cloud-distribution-point"></a><a name="BKMK_PortsClient-CloudDP"></a> Client > Cloudverteilungspunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

Weitere Informationen finden Sie unter [Ports und Datenflüsse](use-a-cloud-based-distribution-point.md#bkmk_dataflow).

### <a name="client----cloud-management-gateway-cmg"></a><a name="bkmk_client-cmg"></a> Client > Cloudverwaltungsgateway (CMG)  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

Weitere Informationen finden Sie unter [CMG-Ports und -Datenflüsse](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow).

### <a name="client----distribution-point-both-standard-and-pull"></a><a name="BKMK_PortsClient-DP"></a> Client > Verteilungspunkt, sowohl Standard- als auch Pullversion  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|  
|HTTPS|--|443 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|
|Express-Updates|--|8005 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|<!-- SCCMDocs#2091 -->

> [!NOTE]
> Verwenden Sie Clienteinstellungen, um den alternativen Port für Express-Updates zu konfigurieren. Weitere Informationen finden Sie unter [Von Clients verwendeter Port zum Empfang von Anforderungen für Deltainhalte](../../clients/deploy/about-client-settings.md#port-that-clients-use-to-receive-requests-for-delta-content).

### <a name="client----distribution-point-configured-for-multicast-both-standard-and-pull"></a><a name="BKMK_PortsClient-DP2"></a> Client > für Multicast konfigurierter Verteilungspunkt, sowohl Standard- als auch Pullversion  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Multicast-Protokoll|63000-64000|--|  

### <a name="client----distribution-point-configured-for-pxe-both-standard-and-pull"></a><a name="BKMK_PortsClient-DP3"></a> Client > für PXE konfigurierter Verteilungspunkt, sowohl Standard- als auch Pullversion  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|DHCP|67 und 68|--|  
|TFTP|69 <sup>[Hinweis 4](#bkmk_note4)</sup> |--|  
|Boot Information Negotiation Layer (BINL)|4011|--|  

> [!Important]  
> Wenn Sie eine hostbasierte Firewall aktivieren, stellen Sie sicher, dass die Regeln dem Server den Versand und den Empfang über diese Ports erlauben. Wenn Sie einen Verteilungspunkt für PXE aktivieren, kann Configuration Manager die eingehenden Regeln (Empfangsregeln) auf der Windows-Firewall aktivieren. Die ausgehenden Regeln (Senderegeln) werden nicht konfiguriert.<!--SCCMDocs issue #744-->  

### <a name="client----fallback-status-point"></a><a name="BKMK_PortsClient-FSP"></a> Client > Fallbackstatuspunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|  

### <a name="client----global-catalog-domain-controller"></a><a name="BKMK_PortsClient-GCDC"></a> Client > Domänencontroller des globalen Katalogs

Ein Configuration Manager-Client stellt keine Verbindung mit einem globalen Katalogserver her, wenn er für die reine Internetkommunikation konfiguriert ist oder einen Arbeitsgruppencomputer darstellt.  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Globales Katalog-LDAP|--|3268|  

### <a name="client----management-point"></a><a name="BKMK_PortsClient-MP"></a> Client > Verwaltungspunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Clientbenachrichtigung (Standardkommunikation vor Fallback auf HTTP oder HTTPS)|--|10123 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|  
|HTTP|--|80 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|  
|HTTPS|--|443 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|  

### <a name="client----software-update-point"></a><a name="BKMK_PortsClient-SUP"></a> Client > Softwareupdatepunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 oder 8530 <sup>[Hinweis 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 oder 8531 <sup>[Hinweis 3](#bkmk_note3)</sup>|  

### <a name="client----state-migration-point"></a><a name="BKMK_PortsClient-SMP"></a> Client > Zustandsmigrationspunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|  
|HTTPS|--|443 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|  
|Server Message Block (SMB)|--|445|  

### <a name="cmg-connection-point----cmg-cloud-service"></a><a name="bkmk_cmgcp-cmg"></a> CMG-Verbindungspunkt > CMG-Clouddienst  

Configuration Manager verwendet diese Verbindungen zum Erstellen des CMG-Kanals. Weitere Informationen finden Sie unter [CMG-Ports und -Datenflüsse](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow).

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|TCP-TLS (bevorzugt)|--|10140-10155|  
|HTTPS (Fallback mit einem virtuellen Computer)|--|443|  
|HTTPS (Fallback mit zwei oder mehr virtuellen Computern)|--|10124-10139|  

### <a name="cmg-connection-point----management-point"></a><a name="bkmk_cmgcp-mp"></a> CMG-Verbindungspunkt > Verwaltungspunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|

Weitere Informationen finden Sie unter [CMG-Ports und -Datenflüsse](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow).

### <a name="cmg-connection-point----software-update-point"></a><a name="bkmk_cmgcp-sup"></a> CMG-Verbindungspunkt > Softwareupdatepunkt  

Der spezielle Port hängt von der Konfiguration des Softwareupdatepunkts ab.

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|
|HTTP|--|80|  

Weitere Informationen finden Sie unter [CMG-Ports und -Datenflüsse](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow).

### <a name="configuration-manager-console----client"></a><a name="BKMK_PortsConsole-Client"></a> Configuration Manager-Konsole > Client  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Remotesteuerung (Steuerung)|--|2701|  
|Remoteunterstützung (RDP und RTC)|--|3389|  

### <a name="configuration-manager-console----internet"></a><a name="BKMK_PortsConsole-Internet"></a> Configuration Manager-Konsole > Internet  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80|  
|HTTPS|--|443|

Die Configuration Manager-Konsole benötigt für folgende Aktionen einen Internetzugang:

- Herunterladen von Softwareupdates von Microsoft Update für Bereitstellungspakete
- Das Feedbackelement im Menüband.
- Links zu Dokumentation innerhalb der Konsole
<!--506823-->

### <a name="configuration-manager-console----reporting-services-point"></a><a name="BKMK_PortsConsole-RSP"></a> Configuration Manager-Konsole > Reporting Services-Punkt  

|Beschreibung|UDP|TCP|
|-----------------|---------|---------|
|HTTP|--|80 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|  
|HTTPS|--|443 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|  

### <a name="configuration-manager-console----site-server"></a><a name="BKMK_PortsConsole-Site"></a> Configuration Manager-Konsole > Standortserver  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|RPC (erstes Verbinden mit WMI zur Suche des Anbietersystems)|--|135|  

### <a name="configuration-manager-console----sms-provider"></a><a name="BKMK_PortsConsole-Provider"></a> Configuration Manager-Konsole > SMS-Anbieter  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|RPC-Endpunktzuordnung|135|135|  
|RPC|--|DYNAMIC <sup>[Hinweis 6](#bkmk_note6)</sup>|  

### <a name="configuration-manager-network-device-enrollment-service-ndes-policy-module----certificate-registration-point"></a><a name="BKMK_PortsCertificateRegistationPoint_PolicyModule"></a> Configuration Manager-Richtlinienmodul des Registrierungsdiensts für Netzwerkgeräte (NDES) > Zertifikatregistrierungspunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|  

### <a name="data-warehouse-service-point----sql-server"></a><a name="BKMK_PortsDWSPSQL"></a> Data Warehouse-Dienstpunkt > SQL Server  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|SQL über TCP|--|1433 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|  

### <a name="distribution-point-both-standard-and-pull----management-point"></a><a name="BKMK_PortsDist_MP"></a> Verteilungspunkt, sowohl Standard- als auch Pullversion > Verwaltungspunkt

Ein Verteilungspunkt kommuniziert mit dem Verwaltungspunkt in den folgenden Szenarien:  

- Um den Status von vorab bereitgestellten Inhalten zu melden  

- Um die Verwendungsdatenzusammenfassung zu melden  

- Um die Inhaltsprüfung zu melden  

- Um den Status von Paketdownloads zu melden (nur Pullverteilungspunkt)

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|  
|HTTPS|--|443 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|  

### <a name="endpoint-protection-point----internet"></a><a name="BKMK_PortsEndpointProtection_Internet"></a> Endpoint Protection-Punkt > Internet  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80|  

### <a name="endpoint-protection-point----sql-server"></a><a name="BKMK_PortsEP-to-SQL"></a> Endpoint Protection-Punkt > SQL Server  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|SQL über TCP|--|1433 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|  

### <a name="enrollment-proxy-point----enrollment-point"></a><a name="BKMK_PortsEnrollmentProxyEnrollmentPoint"></a> Anmeldungsproxypunkt > Anmeldungspunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|  

### <a name="enrollment-point----sql-server"></a><a name="BKMK_PortsEnrollmentEnrollmentSQL"></a> Anmeldungspunkt > SQL Server  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|SQL über TCP|--|1433 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|  

### <a name="exchange-server-connector----exchange-online"></a><a name="BKMK_PortsExchangeConnectorHosted"></a> Exchange Server-Connector > Exchange Online  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Windows-Remoteverwaltung über HTTPS|--|5986|  

### <a name="exchange-server-connector----on-premises-exchange-server"></a><a name="BKMK_PortsExchangeConnectorOnPrem"></a> Exchange Server-Connector > Exchange Server (lokal)  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Windows-Remoteverwaltung über HTTP|--|5985|  

### <a name="mac-computer----enrollment-proxy-point"></a><a name="BKMK_PortsMacEnrollmentProxyPoint"></a> Macintosh-Computer > Anmeldungsproxypunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

### <a name="management-point----domain-controller"></a><a name="BKMK_PortsMP-DC"></a> Verwaltungspunkt > Domänencontroller  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Lightweight Directory Access-Protokoll (LDAP)|389|389|  
|Secure LDAP (LDAPS, für Signatur und Bindung)|636|636|  
|Globales Katalog-LDAP|--|3268|  
|RPC-Endpunktzuordnung|--|135|  
|RPC|--|DYNAMIC <sup>[Hinweis 6](#bkmk_note6)</sup>|  

### <a name="management-point-lt---site-server"></a><a name="BKMK_PortsMP-Site"></a> Verwaltungspunkt &lt; > Standortserver

<sup>[Hinweis 5](#bkmk_note5)</sup>

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|RPC-Endpunktzuordnung|--|135|  
|RPC|--|DYNAMIC <sup>[Hinweis 6](#bkmk_note6)</sup>|  
|Server Message Block (SMB)|--|445|  

### <a name="management-point----sql-server"></a><a name="BKMK_PortsMP-SQL"></a> Verwaltungspunkt > SQL Server  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|SQL über TCP|--|1433 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|  

### <a name="mobile-device----enrollment-proxy-point"></a><a name="BKMK_PortsMobileDeviceClient-EnrollmentProxyPoint"></a> Mobiles Gerät > Anmeldungsproxypunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

###  <a name="reporting-services-point----sql-server"></a><a name="BKMK_PortsRSP-SQL"></a> Reporting Services-Punkt > SQL Server  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|SQL über TCP|--|1433 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|  

### <a name="service-connection-point----azure-cmg"></a><a name="bkmk_scp-cmg"></a> Dienstverbindungspunkt > Azure (CMG)  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS für CMG-Dienstbereitstellung|--|443|

Weitere Informationen finden Sie unter [CMG-Ports und -Datenflüsse](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow).

### <a name="site-server-lt---application-catalog-web-service-point"></a><a name="BKMK_PortsAppCatalogWebServicePoint_SiteServer"></a> Standortserver &lt; > Anwendungskatalog-Webdienstpunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-Endpunktzuordnung|135|135|  
|RPC|--|DYNAMIC <sup>[Hinweis 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---application-catalog-website-point"></a><a name="BKMK_PortsAppCatalogWebSitePoint_SiteServer"></a> Standortserver &lt; > Anwendungskatalog-Websitepunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-Endpunktzuordnung|135|135|  
|RPC|--|DYNAMIC <sup>[Hinweis 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---asset-intelligence-synchronization-point"></a><a name="BKMK_PortsSite-AISP"></a> Standortserver &lt; > Asset Intelligence-Synchronisierungspunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-Endpunktzuordnung|135|135|  
|RPC|--|DYNAMIC <sup>[Hinweis 6](#bkmk_note6)</sup>|  

### <a name="site-server----client"></a><a name="BKMK_PortsSite-Client"></a> Standortserver > Client  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|-Wake-On-LAN|9 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|--|  

### <a name="site-server----cloud-distribution-point"></a><a name="BKMK_PortsSiteServer-CloudDP"></a> Standortserver > Cloudverteilungspunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

Weitere Informationen finden Sie unter [Ports und Datenflüsse](use-a-cloud-based-distribution-point.md#bkmk_dataflow).

### <a name="site-server----distribution-point-both-standard-and-pull"></a><a name="BKMK_PortsSite-DP"></a> Standortserver > Verteilungspunkt, sowohl Standard- als auch Pullversion

<sup>[Hinweis 5](#bkmk_note5)</sup>  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-Endpunktzuordnung|135|135|  
|RPC|--|DYNAMIC <sup>[Hinweis 6](#bkmk_note6)</sup>|  

### <a name="site-server----domain-controller"></a><a name="BKMK_PortsSite-DC"></a> Standortserver > Domänencontroller  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Lightweight Directory Access-Protokoll (LDAP)|389|389|
|Secure LDAP (LDAPS, für Signatur und Bindung)|636|636|
|Globales Katalog-LDAP|--|3268|  
|RPC-Endpunktzuordnung|--|135|  
|RPC|--|DYNAMIC <sup>[Hinweis 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---certificate-registration-point"></a><a name="BKMK_PortsCertificateRegistrationPoint_SiteServer"></a> Standortserver &lt; > Zertifikatregistrierungspunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-Endpunktzuordnung|135|135|  
|RPC|--|DYNAMIC <sup>[Hinweis 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---cmg-connection-point"></a><a name="BKMK_CMGCP_SiteServer"></a> Standortserver &lt; > CMG-Verbindungspunkt

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-Endpunktzuordnung|135|135|  
|RPC|--|DYNAMIC <sup>[Hinweis 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---endpoint-protection-point"></a><a name="BKMK_PortsEndpointProtection_SiteServer"></a> Standortserver &lt; > Endpoint Protection-Punkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-Endpunktzuordnung|135|135|  
|RPC|--|DYNAMIC <sup>[Hinweis 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---enrollment-point"></a><a name="BKMK_EnrollmentPoint_SiteServer"></a> Standortserver &lt; > Anmeldungspunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-Endpunktzuordnung|135|135|  
|RPC|--|DYNAMIC <sup>[Hinweis 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---enrollment-proxy-point"></a><a name="BKMK_EnrollmentProxyPoint_SiteServer"></a> Standortserver &lt; > Anmeldungsproxypunkt  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-Endpunktzuordnung|135|135|  
|RPC|--|DYNAMIC <sup>[Hinweis 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---fallback-status-point"></a><a name="BKMK_PortsSite-FSP"></a> Standortserver &lt; > Fallbackstatuspunkt

<sup>[Hinweis 5](#bkmk_note5)</sup>  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-Endpunktzuordnung|135|135|  
|RPC|--|DYNAMIC <sup>[Hinweis 6](#bkmk_note6)</sup>|  

### <a name="site-server----internet"></a><a name="BKMK_PortSite-Internet"></a> Standortserver > Internet  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[Hinweis 1](#bkmk_note1)</sup>|  

### <a name="site-server-lt---issuing-certification-authority-ca"></a><a name="BKMK_PortsIssuingCA_SiteServer"></a> Standortserver &lt; > Ausstellende Zertifizierungsstelle (CA)

Diese Kommunikation wird verwendet, wenn Sie Zertifikatprofile über den Zertifikatregistrierungspunkt bereitstellen. Diese Kommunikation wird nicht für jeden Standortserver in der Hierarchie verwendet. Stattdessen wird sie nur für die Standortserver verwendet, die sich in der Hierarchie an oberster Stelle befinden.  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|RPC-Endpunktzuordnung|135|135|  
|RPC (DCOM)|--|DYNAMIC <sup>[Hinweis 6](#bkmk_note6)</sup>|  

### <a name="site-server----server-hosting-remote-content-library-share"></a><a name="BKMK_PortsSite-RCL"></a> Standortserver > Hostserver für die Bibliotheksfreigabe von Remoteinhalt

Sie können die Inhaltsbibliothek an einen anderen Speicherort verschieben, um auf Ihrem zentralen Verwaltungsserver oder Ihren primären Standortservern Speicherplatz auf einem Laufwerk freizugeben. Weitere Informationen finden Sie unter [Konfigurieren einer Remoteinhaltsbibliothek für den Standortserver](the-content-library.md#bkmk_remote).

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  

### <a name="site-server-lt---service-connection-point"></a><a name="BKMK_SCP_SiteServer"></a> Standortserver &lt; > Dienstverbindungspunkt

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-Endpunktzuordnung|135|135|  
|RPC|--|DYNAMIC <sup>[Hinweis 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---reporting-services-point"></a><a name="BKMK_PortsSite-RSP"></a> Standortserver &lt; > Reporting Services-Punkt

<sup>[Hinweis 5](#bkmk_note5)</sup>  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-Endpunktzuordnung|135|135|  
|RPC|--|DYNAMIC <sup>[Hinweis 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---site-server"></a><a name="BKMK_PortsSite-Site"></a> Standortserver &lt; > Standortserver  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  

### <a name="site-server----sql-server"></a><a name="BKMK_PortsSite-SQL"></a> Standortserver > SQL Server  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|SQL über TCP|--|1433 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|  

Während der Installation eines Standorts, der einen SQL Server-Remotehost für die Standortdatenbank verwendet, öffnen Sie die folgenden Ports zwischen Standortserver und SQL-Server:  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-Endpunktzuordnung|135|135|  
|RPC|--|DYNAMIC <sup>[Hinweis 6](#bkmk_note6)</sup>|  

### <a name="site-server----sql-server-for-wsus"></a><a name="BKMK_PortsSite-SQL-WSUS"></a> Standortserver > SQL Server für WSUS  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|SQL über TCP|--|1433 <sup>[Hinweis 3](#bkmk_note3) Alternativer Port verfügbar</sup>|  

### <a name="site-server----sms-provider"></a><a name="BKMK_PortsSite-Provider"></a> Standortserver > SMS-Anbieter  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-Endpunktzuordnung|135|135|  
|RPC|--|DYNAMIC <sup>[Hinweis 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---software-update-point"></a><a name="BKMK_PortsSite-SUP"></a> Standortserver &lt; > Softwareupdatepunkt

<sup>[Hinweis 5](#bkmk_note5)</sup>  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|HTTP|--|80 oder 8530 <sup>[Hinweis 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 oder 8531 <sup>[Hinweis 3](#bkmk_note3)</sup>|  

### <a name="site-server-lt---state-migration-point"></a><a name="BKMK_PortsSite-SMP"></a> Standortserver &lt; > Zustandsmigrationspunkt

<sup>[Hinweis 5](#bkmk_note5)</sup>  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-Endpunktzuordnung|135|135|  

### <a name="sms-provider----sql-server"></a><a name="BKMK_PortsProvider-SQL"></a> SMS-Anbieter > SQL Server  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|SQL über TCP|--|1433 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|  

### <a name="software-update-point----internet"></a><a name="BKMK_PortsSUP-Internet"></a>Softwareupdatepunkt > Internet  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[Hinweis 1](#bkmk_note1)</sup>|  

### <a name="software-update-point----upstream-wsus-server"></a><a name="BKMK_PortsSUP-WSUS"></a> Softwareupdatepunkt > WSUS-Upstreamserver  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 oder 8530 <sup>[Hinweis 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 oder 8531 <sup>[Hinweis 3](#bkmk_note3)</sup>|  

### <a name="sql-server----sql-server"></a><a name="BKMK_PortsSQL-SQL"></a> SQL Server -- &gt; SQL Server

Für die standortübergreifende Datenbankreplikation ist die direkte Kommunikation von SQL Server an einem Standort mit SQL Server am über- oder untergeordneten Standort erforderlich.  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|SQL Server-Dienst|--|1433 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|  
|SQL Server Service Broker|--|4022 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|  

> [!TIP]  
> Configuration Manager erfordert keinen SQL Server-Browser, der den Port UDP 1434 verwendet.  

### <a name="state-migration-point----sql-server"></a><a name="BKMK_PortsStateMigrationPoint-to-SQL"></a> Zustandsmigrationspunkt > SQL Server  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|SQL über TCP|--|1433 <sup>[Hinweis 2](#bkmk_note2) Alternativer Port verfügbar</sup>|  

### <a name="notes-for-ports-used-by-configuration-manager-clients-and-site-systems"></a><a name="BKMY_PortNotes"></a> Hinweise für von Configuration Manager-Clients und Standortsystemen verwendete Ports  

#### <a name="note-1-proxy-server-port"></a><a name="bkmk_note1"></a> Hinweis 1: Proxyserverport

Dieser Port kann nicht konfiguriert, aber durch einen konfigurierten Proxyserver weitergeleitet werden.  

#### <a name="note-2-alternate-port-available"></a><a name="bkmk_note2"></a> Hinweis 2: Alternativer Port verfügbar

Sie können in Configuration Manager einen alternativen Port für diesen Wert definieren. Wenn Sie einen benutzerdefinierten Port definieren, verwenden Sie diesen benutzerdefinierten Port in den IP-Filterinformationen für IPsec-Richtlinien oder zum Konfigurieren von Firewalls.  

#### <a name="note-3-windows-server-update-services-wsus"></a><a name="bkmk_note3"></a> Hinweis 3: Windows Server Update Services (WSUS)

WSUS können installiert werden, um die Ports 80/443 oder 8530/8531 für die Clientkommunikation zu verwenden. Wenn Sie WSUS unter Windows Server 2012 oder Windows Server 2016 ausführen, wird WSUS standardmäßig für die Verwendung von Port 8530 für HTTP und Port 8531 für HTTPS konfiguriert.  

Sie können den Port nach der Installation ändern. Es ist nicht erforderlich, in der gesamten Standorthierarchie dieselbe Portnummer zu verwenden.  

- Wenn der HTTP-Port 80 verwendet wird, muss der HTTPS-Port 443 sein.  

- Wenn ein anderer HTTP-Port verwendet wird, muss der HTTPS-Port 1 oder höher sein, z.B. 8530 oder 8531.

    > [!NOTE]  
    >  Wenn Sie den Softwareupdatepunkt zur Verwendung von HTTPS konfigurieren, muss auch der HTTP-Port geöffnet sein. Der HTTP-Port wird für unverschlüsselte Daten, z. B. den EULA für bestimmte Updates, verwendet.

- Der Standortserver stellt eine Verbindung mit der SQL Server-Instanz her, die die SUSDB-Datenbank hostet, wenn Sie die folgenden Optionen für die WSUS-Bereinigung aktivieren:
  - Hinzufügen nicht gruppierter Indizes zur WSUS-Datenbank, um die WSUS-Bereinigungsleistung zu verbessern
  - Entfernen veralteter Updates aus der WSUS-Datenbank
  
  Wenn der standardmäßige SQL Server-Port mit dem SQL Server-Konfigurations-Manager in einen alternativen Port geändert wird, müssen Sie sicherstellen, dass der Standortserver eine Verbindung über den definierten Port herstellen kann. Dynamische Ports werden von Configuration Manager nicht unterstützt. Standardmäßig verwenden benannte SQL Server-Instanzen dynamische Ports für die Verbindungsherstellung mit der Datenbank-Engine. Wenn Sie eine benannte Instanz verwenden, konfigurieren Sie den statischen Port manuell.

#### <a name="note-4-trivial-ftp-tftp-daemon"></a><a name="bkmk_note4"></a> Hinweis 4: Daemon für „Trivial FTP“ (TFTP)

Der Daemon für „Trivial FTP“ (TFTP) erfordert weder einen Benutzernamen noch ein Kennwort und ist integraler Bestandteil der Windows-Bereitstellungsdienste (Windows Deployment Services, WDS). Der Daemondienst für „Trivial FTP“ unterstützt das TFTP-Protokoll, das über folgende RFCs definiert ist:  

- RFC 1350: TFTP  

- RFC 2347: Optionserweiterung  

- RFC 2348: Blockgrößenoption  

- RFC 2349: Timeoutintervall und Optionen zur Übertragungsgröße  

Das FTP wurde zur Unterstützung von Startumgebungen ohne Datenträger entwickelt. TFTP-Daemons hören den UDP-Port 69 ab, antworten jedoch von einem dynamisch zugewiesenen, hohen Port. Wenn Sie diesen Port aktivieren, kann der TFTP-Dienst eingehende TFTP-Anforderungen empfangen. Der ausgewählte Server kann jedoch nicht auf diese Anforderungen reagieren. Der ausgewählte Server kann erst dann auf eingehende TFTP-Anforderungen reagieren, wenn Sie den TFTP-Server so konfigurieren, dass seine Antwort über Port 69 erfolgt.  

Der PXE-fähige Verteilungspunkt und der Client in Windows PE wählen dynamisch zugewiesene, hohe Ports für TFTP-Übertragungen aus. Diese Ports werden von Microsoft zwischen 49152 und 65535 definiert. Weitere Informationen finden Sie unter [Dienstübersicht und Netzwerkportanforderungen für Windows](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows).

Während des eigentlichen PXE-Starts wählt die Netzwerkkarte auf dem Gerät jedoch den dynamisch zugewiesenen, hohen Port für die TFTP-Übertragung aus. Die Netzwerkkarte auf dem Gerät ist nicht an die von Microsoft definierten dynamisch zugewiesenen, hohen Ports gebunden. Sie ist lediglich an die in RFC 1350 definierten Ports gebunden. Dies kann ein beliebiger Port von 0 bis 65535 sein. Weitere Informationen darüber, welche dynamisch zugewiesenen, hohen Ports von der Netzwerkkarte genutzt werden, erhalten Sie beim Hersteller der Gerätehardware.

#### <a name="note-5-communication-between-the-site-server-and-site-systems"></a><a name="bkmk_note5"></a> Hinweis 5: Kommunikation zwischen dem Standortserver und Standortsystemen

Standardmäßig erfolgt zwischen dem Standortserver und Standortsystemen eine bidirektionale Kommunikation. Der Standortserver startet die Kommunikation zum Konfigurieren des Standortsystems. Die meisten Standortsysteme stellen dann wiederum eine Verbindung mit dem Standortserver her, um Statusinformationen zu senden. Von Reporting Services-Punkten und Verteilungspunkten werden keine Statusinformationen gesendet. Wenn Sie nach der Installation des Standortsystems in dessen Eigenschaften die Option **Verbindungen mit diesem Standortsystem müssen vom Standortserver hergestellt werden** auswählen, startet das Standortsystem keine Kommunikation mit dem Standortserver. Stattdessen startet der Standortserver die Kommunikation. Er verwendet das Installationskonto des Standortsystems für die Authentifizierung beim Standortsystemserver.  

#### <a name="note-6-dynamic-ports"></a><a name="bkmk_note6"></a> Hinweis 6: Dynamische Ports

Dynamische Ports verwenden eine Reihe von Portnummern, die von der Version des Betriebssystems definiert werden. Diese Ports werden auch als kurzlebige Ports bezeichnet. Weitere Informationen über die Standardportbereiche finden Sie unter [Dienstübersicht und Netzwerkportanforderungen für das Windows Server-System](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows).  

## <a name="additional-lists-of-ports"></a><a name="BKMK_AdditionalPorts"></a> Zusätzliche Portlisten  

In den folgenden Abschnitten finden Sie zusätzliche Informationen zu Ports, die von Configuration Manager verwendet werden.

### <a name="client-to-server-shares"></a><a name="BKMK_ClientShares"></a> Client-zu-Server-Freigaben

Von Clients wird SMB (Server Message Block) verwendet, wenn eine Verbindung zu UNC-Freigaben hergestellt wird. Beispiel:

- Manuelle Clientinstallation, bei der die Befehlszeileneigenschaft CCMSetup.exe **/source:** angegeben wird  

- Endpoint Protection-Clients, von denen Definitionsdateien über einen UNC-Pfad heruntergeladen werden

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  

### <a name="connections-to-microsoft-sql-server"></a><a name="BKMK_SQLPorts"></a> Verbindungen zu Microsoft SQL Server

Für die Kommunikation mit der SQL Server-Datenbank-Engine und für die standortübergreifende Replikation können Sie den SQL Server-Standardport verwenden oder benutzerdefinierte Ports angeben:  

- Die Kommunikation zwischen Standorten erfolgt über:  

  - SQL Server Service Broker (standardmäßig TCP-Port 4022).  

  - SQL Server-Dienst, erfolgt standardmäßig über TCP-Port 1433.  

- Die standortinterne Kommunikation zwischen der SQL Server-Datenbank-Engine und verschiedenen Configuration Manager-Standortsystemrollen erfolgt standardmäßig über TCP-Port 1433.  

- Configuration Manager verwendet die gleichen Ports und Protokolle zur Kommunikation mit jedem SQL-Verfügbarkeitsgruppenreplikat, das die Standortdatenbank hostet, als wäre das Replikat eine eigenständige SQL Server-Instanz.

Wenn Sie Azure verwenden und die Standortdatenbank sich hinter einem internen oder externen Lastenausgleich befindet, konfigurieren Sie die folgenden Komponenten:

- Firewallausnahmen für jedes Replikat
- Lastenausgleichsregeln

Konfigurieren Sie die folgenden Ports:

- SQL über TCP: TCP 1433
- SQL Server Service Broker: TCP 4022
- Server Message Block (SMB): TCP 445
- RPC-Endpunktzuordnung: TCP 135

> [!WARNING]  
> Dynamische Ports werden von Configuration Manager nicht unterstützt. Standardmäßig verwenden benannte SQL Server-Instanzen dynamische Ports für Verbindungen zur Datenbank-Engine. Wenn Sie eine benannte Instanz verwenden, konfigurieren Sie den statischen Port manuell für die Intrasitekommunikation.  

Die folgenden Standortsystemrollen kommunizieren direkt mit der SQL Server-Datenbank:  

- Anwendungskatalog-Webdienstpunkt  

- Zertifikatregistrierungspunktrolle  

- Anmeldungspunktrolle  

- Verwaltungspunkt  

- Standortserver  

- Reporting Services-Punkt  

- SMS-Anbieter  

- SQL Server -- > SQL Server  

Wenn ein SQL Server-Computer Datenbanken von mehreren Standorten hostet, muss jede Datenbank eine separate SQL Server-Instanz verwenden. Konfigurieren Sie jede Instanz mit einem eindeutigen Satz von Ports.  

Wenn Sie eine hostbasierte Firewall auf dem SQL Server-Computer aktivieren, konfigurieren Sie sie so, dass sie die richtigen Ports zulässt. Konfigurieren Sie auch Netzwerkfirewalls zwischen Computern, die mit dem SQL Server-Computer kommunizieren.  

Ein Beispiel zum Konfigurieren von SQL Server für die Verwendung eines bestimmten Ports finden Sie unter [Konfigurieren eines Servers für das Überwachen eines bestimmten TCP-Ports](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port).  

### <a name="discovery-and-publishing"></a><a name="bkmk_discovery"> </a> Ermittlung und Veröffentlichung

Configuration Manager verwendet die folgenden Ports für die Ermittlung und Veröffentlichung von Standortinformationen:

- Lightweight Directory Access Protocol (LDAP): 389
- Secure LDAP (LDAPS, für Signatur und Bindung): 636
- Globales Katalog-LDAP: 3268
- RPC-Endpunktzuordnung: 135
- RPC: Dynamisch zugewiesene, hohe TCP-Ports
- TCP: 1024: 5000
- TCP:  49152: 65535

### <a name="external-connections-made-by-configuration-manager"></a><a name="BKMK_External"></a> Externe Verbindungen von Configuration Manager

Lokale Configuration Manager-Clients oder -Standortsysteme können die folgenden externen Verbindungen erstellen:  

- [Asset Intelligence-Synchronisierungspunkt --&gt; Microsoft](#BKMK_PortsAI)  

- [Endpoint Protection-Punkt --&gt; Internet](#BKMK_PortsEndpointProtection_Internet)  

- [Client --&gt; Domänencontroller des globalen Katalogs](#BKMK_PortsClient-GCDC)  

- [Configuration Manager-Konsole --&gt; Internet](#BKMK_PortsConsole-Internet)  

- [Verwaltungspunkt --&gt; Domänencontroller](#BKMK_PortsMP-DC)  

- [Standortserver --&gt; Domänencontroller](#BKMK_PortsSite-DC)  

- [Standortserver &lt; --&gt; Ausstellende Zertifizierungsstelle (CA)](#BKMK_PortsIssuingCA_SiteServer)  

- [Softwareupdatepunkt --&gt; Internet](#BKMK_PortsSUP-Internet)  

- [Softwareupdatepunkt --&gt; WSUS-Upstreamserver](#BKMK_PortsSUP-WSUS)  

- [Dienstverbindungspunkt > Azure](#bkmk_scp-cmg)  

- [CMG-Verbindungspunkt > CMG-Clouddienst](#bkmk_cmgcp-cmg)  

### <a name="installation-requirements-for-site-systems-that-support-internet-based-clients"></a><a name="BKMK_IBCMports"></a> Installationsanforderungen für Standortsysteme, die internetbasierte Clients unterstützen

> [!Note]  
> Dieser Abschnitt gilt nur für das internetbasierte Kundenmanagement (IBCM). Er gilt nicht für das Cloudverwaltungsgateway. Weitere Informationen finden Sie unter [Verwalten von Clients im Internet](../../clients/manage/manage-clients-internet.md).  

Internetbasierte Verwaltungspunkte, Verteilungspunkte, die internetbasierte Clients unterstützen, sowie der Softwareupdatepunkt und der Fallbackstatuspunkt verwenden für die Installation und Reparatur die folgenden Ports:  

- Standortserver --> Standortsystem: RPC-Endpunktzuordnung, verwendet UDP und TCP-Port 135.  

- Standortserver --> Standortsystem: RPC Dynamic TCP-Ports  

- Standortserver &lt; --> Standortsystem: Server Message Blocks (SMB), verwenden TCP-Port 445

Für die Anwendungs- und Paketinstallation auf Verteilungspunkten sind die folgenden RPC-Ports erforderlich:  

- Standortserver -- > Verteilungspunkt: RPC-Endpunktzuordnung, verwendet UDP und TCP-Port 135

- Standortserver -- > Verteilungspunkt: RPC Dynamic TCP-Ports  

Verwenden Sie IPsec zur Sicherung des Datenverkehrs zwischen dem Standortserver und den Standortsystemen. Zur Einschränkung der von RPC verwendeten dynamischen Ports können Sie das RPC-Konfigurationstool von Microsoft (rpccfg.exe) verwenden. Verwenden Sie das Tool, um einen eingeschränkten Bereich von Ports für diese RPC-Pakete zu konfigurieren. Weitere Informationen finden Sie unter [Konfigurieren von RPC für die Verwendung bestimmter Ports und Schützen dieser Ports mit IPsec](https://support.microsoft.com/help/908472/how-to-configure-rpc-to-use-certain-ports-and-how-to-help-secure-those).  

> [!IMPORTANT]
> Überprüfen Sie vor der Installation dieser Standortsysteme, ob der Remoteregistrierungsdienst auf dem Standortsystemserver ausgeführt wird und Sie ein Standortsystem-Installationskonto angegeben haben, falls sich das Standortsystem in einer anderen Active Directory-Gesamtstruktur ohne Vertrauensstellung befindet. Der Remoteregistrierungsdienst wird beispielsweise auf Servern verwendet, auf denen Standortsysteme wie z. B. Verteilungspunkte (sowohl Standard- als auch Pullversion), Remote-SQL-Server und der Anwendungskatalog ausgeführt werden.

### <a name="ports-used-by-configuration-manager-client-installation"></a><a name="BKMK_PortsClientInstall"></a> Von der Configuration Manager-Clientinstallation verwendete Ports

Welche Ports Configuration Manager während der Clientinstallation verwendet, hängt von der Bereitstellungsmethode ab.

- Eine Liste der für jede Clientbereitstellungsmethode verwendeten Ports finden Sie unter [Bei der Clientbereitstellung von Configuration Manager verwendete Ports](../../clients/deploy/windows-firewall-and-port-settings-for-clients.md#ports-used-during-configuration-manager-client-deployment).  

- Informationen zum Konfigurieren der Windows-Firewall auf dem Client für die Clientinstallation und die Kommunikation nach der Installation finden Sie unter [Windows-Firewall und Porteinstellungen für Clients](../../clients/deploy/windows-firewall-and-port-settings-for-clients.md).  

### <a name="ports-used-by-migration"></a><a name="BKMK_MigrationPorts"></a> Für die Migration verwendete Ports

Der Standortserver, der die Migration ausführt, verwendet verschiedene Ports für die Verbindung zu entsprechenden Standorten in der Quellhierarchie. Weitere Informationen finden Sie unter [Erforderliche Konfigurationen für die Migration](../../migration/prerequisites-for-migration.md#BKMK_Required_Configurations).  

### <a name="ports-used-by-windows-server"></a><a name="BKMK_ServerPorts"></a> Von Windows Server verwendete Ports

In der folgenden Tabelle werden die wichtigsten von Windows Server verwendeten Ports aufgelistet.

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|DNS|53|53|  
|DHCP|67 und 68|--|  
|NetBIOS-Namensauflösung|137|--|  
|NetBIOS-Datagrammdienst|138|--|  
|NetBIOS-Sitzungsdienst|--|139|  
|Kerberos-Authentifizierung|--|88|

Weitere Informationen finden Sie in den folgenden Artikeln:

- [Dienstübersicht und Netzwerkportanforderungen für Windows](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows).

- [Konfigurieren einer Firewall für Domänen und Vertrauensstellungen](https://support.microsoft.com/help/179442/how-to-configure-a-firewall-for-domains-and-trusts)
