---
title: Unterstützung für Windows-Funktionen
titleSuffix: Configuration Manager
description: Erfahren Sie, welche Windows-und Netzwerkfeatures in Configuration Manager unterstützt werden.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0cf4bacb-6b6d-4d4f-8640-b13fe15873de
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4f9266668a488b6331857bf860d874a48161fcd0
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700213"
---
# <a name="support-for-windows-features-and-networks-in-configuration-manager"></a>Unterstützung für Windows-Features und -Netzwerke in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

In diesem Artikel erfahren Sie mehr über die Configuration Manager-Unterstützung für übliche Windows- und Netzwerkfeatures.  

## <a name="branchcache"></a><a name="bkmk_branchcache"></a> BranchCache  

Verwenden Sie Windows BranchCache mit Configuration Manager, wenn Sie BranchCache auf Verteilungspunkten aktivieren und Clients zum Verwenden von BranchCache im Modus „Verteilter Cache“ konfigurieren.

Konfigurieren Sie die BranchCache-Einstellungen bei einem Bereitstellungstyp für Anwendungen, bei der Bereitstellung für ein Paket und für Tasksequenzen. Ab Version 1802 ist BranchCache standardmäßig aktiviert.

Wenn die Voraussetzungen für BranchCache erfüllt sind, können mithilfe dieser Funktion Inhalte von lokalen Clients abgerufen werden, auf denen die Inhalte zwischengespeichert sind.  

Wenn beispielsweise der erste Client mit aktivierter BranchCache-Funktion Inhalt von einem Verteilungspunkt anfordert, der als BranchCache-Server konfiguriert ist, lädt der Client den Inhalt herunter und zwischenspeichert ihn. Dieser Inhalt wird dann für Clients in dem Subnetz verfügbar, das den Inhalt auch angefordert hat.

Diese Clients führen auch eine Zwischenspeicherung des Inhalts durch. Andere Clients, die sich im gleichen Subnetz befinden, müssen den Inhalt vom Verteilungspunkt nicht herunterladen. Der Inhalt ist für spätere Übertragungen über mehrere Clients verteilt.  

### <a name="requirements-to-support-branchcache-with-configuration-manager"></a>Anforderungen für die Unterstützung von BranchCache mit Configuration Manager

#### <a name="configure-distribution-points"></a>Konfigurieren von Verteilungspunkten

Fügen Sie das Feature **Windows BranchCache** dem Standortsystemserver hinzu, der als Verteilungspunkt konfiguriert ist.

- Für Verteilungspunkte auf Servern, die für die Unterstützung von BranchCache konfiguriert sind, ist keine zusätzliche Konfiguration erforderlich.
- Windows BranchCache kann keinem cloudbasierten Verteilungspunkt hinzugefügt werden. Der Download von Inhalt durch Clients, die für Windows BranchCache konfiguriert sind, wird von cloudbasierten Verteilungspunkten unterstützt.  

#### <a name="configure-clients"></a>Konfigurieren von Clients

- Die Clients, die BranchCache unterstützen können, müssen für den BranchCache-Modus „Verteilter Cache“ konfiguriert werden.  
- Die Betriebssystemeinstellung für BITS-Clienteinstellungen muss zur Unterstützung von BranchCache aktiviert sein.  

Weitere Informationen finden Sie in der Windows-Dokumentation unter [Konfigurieren von Clients für BranchCache](/windows/deployment/update/waas-branchcache#configure-clients-for-branchcache).

Alle von Configuration Manager unterstützten Windows-Versionen unterstützen BranchCache standardmäßig.

Weitere Informationen zu BranchCache finden Sie in der Dokumentation zu Windows Server unter [BranchCache für Windows](/windows-server/networking/branchcache/branchcache).  

## <a name="computers-in-workgroups"></a><a name="bkmk_Workgroups"></a> Computer in Arbeitsgruppen  

Configuration Manager stellt Unterstützung für Clients in Arbeitsgruppen bereit.  

- Configuration Manager unterstützt das Verschieben eines Clients aus einer Arbeitsgruppe in eine Domäne bzw. aus einer Domäne in eine Arbeitsgruppe. Weitere Informationen finden Sie unter [Installieren von Konfigurations-Manager-Clients auf Arbeitsgruppencomputern](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup).  

> [!NOTE]
> Obwohl Clients in Arbeitsgruppen unterstützt werden, müssen alle Standortsysteme Mitglieder einer unterstützten Active Directory-Domäne sein.  

## <a name="data-deduplication"></a><a name="bkmmk_datadedup"></a> Datendeduplizierung

Configuration Manager unterstützt die Verwendung der Datendeduplizierung mit Verteilungspunkten unter Windows Server 2012 oder höher.

> [!IMPORTANT]  
> Das Volume, das Paketquelldateien hostet, kann nicht für die Datendeduplizierung gekennzeichnet werden. Dies liegt daran, dass die Datendeduplizierung Analysepunkte verwendet und Configuration Manager unterstützt keinen Inhaltsquellspeicherort mit Dateien, die auf Analysepunkten gespeichert sind.  

Weitere Informationen finden Sie in den folgenden Beiträgen:

- [Configuration Manager distribution points and Windows Server 2012 data deduplication](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configuration-manager-distribution-points-and-windows-server/ba-p/273385) (Configuration Manager-Verteilungspunkte und Windows Server 2012-Datendeduplizierung) im Configuration Manager-Teamblog

- [Übersicht über die Datendeduplizierung](/windows-server/storage/data-deduplication/overview) in der Windows Server-Dokumentation

## <a name="directaccess"></a><a name="bkmk_DA"></a> DirectAccess  

Configuration Manager unterstützt das DirectAccess-Feature für die Kommunikation zwischen Clients und Standortserversystemen.  

- Wenn alle Voraussetzungen für DirectAccess erfüllt sind, ermöglicht DirectAccess Configuration Manager-Clients, im Internet mit ihrem zugewiesenen Standort zu kommunizieren, als befänden sie sich im Intranet.  

- Für serverseitig initiierte Aktionen, z.B. die Remotesteuerung und Clientpushinstallation, muss auf dem initiierenden Computer IPv6 ausgeführt werden. Dieses Protokoll muss auf allen beteiligten Netzwerkgeräten unterstützt werden.  

Configuration Manager bietet keine DirectAccess-Unterstützung für folgende Funktionalität:  

- Bereitstellung des Betriebssystems

- Kommunikation zwischen Configuration Manager-Standorten  

- Kommunikation zwischen Configuration Manager-Standortsystemservern innerhalb eines Standorts  

## <a name="dual-boot-computers"></a><a name="bkmk_dualboot"></a> Dual-Boot-Computer  

Configuration Manager kann nur jeweils ein Betriebssystem pro Computer verwalten. Wenn auf einem zu verwaltenden Computer mehr als ein Betriebssystem installiert ist, müssen Sie die Ermittlungs- und Installationsmethoden des Standorts so anpassen, dass gewährleistet wird, dass der Konfigurations-Manager-Client nur unter dem zu verwaltenden Betriebssystem installiert wird.  

## <a name="ipv6"></a><a name="bkmk_IPv6"></a> IPv6  

Configuration Manager unterstützt sowohl Internet Protocol Version 4 (IPv4) als auch Internet Protocol Version 6 (IPv6). Dabei gelten folgende Ausnahmen:  

|Funktion| Ausnahmen bei der IPv6-Unterstützung|  
|--------------|-------------------------------|  
|Cloudbasierte Verteilungspunkte|IPv4 ist erforderlich, um Microsoft Azure- und cloudbasierte Verteilungspunkte zu unterstützen.|  
|Cloudverwaltungsgateway|IPv4 ist erforderlich, um Microsoft Azure- und Cloud Management Gateway zu unterstützen.|  
|Mobilgeräte, die von Microsoft Intune und dem Microsoft-Dienstconnector registriert werden|IPv4 ist für die Unterstützung mobiler Geräte erforderlich, die von Microsoft Intune und dem Microsoft-Dienstconnector registriert werden.|  
|Netzwerkermittlung|IPv4 ist erforderlich, wenn Sie für die Suche bei der Netzwerkermittlung einen DHCP-Server konfigurieren.|  
|Bereitstellung des Betriebssystems|In Version 1802 und früher ist IPv4 für die Unterstützung des Betriebssystems erforderlich.  </br> </br> Aktivieren Sie ab Version 1806 einen PXE-Antwortdienst auf einem Verteilungspunkt ohne Windows-Bereitstellungsdienst. Dieser neue PXE-Antwortdienst unterstützt IPv6. Andere Aspekte des Betriebssystembereitstellungsfeatures, z.B. das Erfassen oder Festlegen statischer IP-Adressen während der Tasksequenz, erfordern weiterhin IPv4. |  
|Aktivierungsproxykommunikation|IPv4 ist für die Unterstützung von Aktivierungsproxypaketen auf dem Client erforderlich.|  
|Windows CE|IPv4 ist für die Unterstützung des Configuration Manager-Clients auf Windows CE-Geräten erforderlich.|  

## <a name="network-address-translation"></a><a name="bkmk_NAT"></a> Netzwerkadressübersetzung (Netzwerkadressübersetzung (Network Address Translation, NAT), NAT)  

Die Netzwerkadressenübersetzung wird in Configuration Manager nicht unterstützt, es sei denn, der Standort unterstützt Clients aus dem Internet, und der Client erkennt, dass er mit dem Internet verbunden ist. Weitere Informationen zur internetbasierten Clientverwaltung finden Sie unter [Planen der internetbasierten Clientverwaltung in System Center Configuration Manager](../../clients/manage/plan-internet-based-client-management.md).  

## <a name="specialized-storage-technology"></a><a name="bkmk_storage"></a> Spezielle Speichertechnologien  

Configuration Manager ist für die Hardware ausgelegt, die auf der Windows-Hardwarekompatibilitätsliste für die Version des Betriebssystems zertifiziert ist, auf dem die Configuration Manager-Komponente installiert ist.

Für Standortserverrollen ist NTFS erforderlich, damit Configuration Manager Verzeichnis- und Dateiberechtigungen festlegen kann. Configuration Manager geht davon aus, dass es das logische Laufwerk vollständig besitzt. Standortsysteme auf separaten Computern können in keiner Speichertechnologie logische Partitionen gemeinsam nutzen. Allerdings kann von jedem Computer eine separate logische Partition auf der gleichen physischen Partition eines gemeinsam genutzten Speichergeräts verwendet werden.  

### <a name="support-considerations"></a>Überlegungen zur Unterstützung

- **Storage Area Network (SAN):** SANs werden unterstützt, wenn ein unterstützter Windows-basierter Server direkt mit dem vom SAN gehosteten Volume verbunden ist.  

- **Single Instance Storage (SIS):** Das Konfigurieren von Verteilungspunktpaketen und Signaturordnern auf einem SIS-fähigen Volume wird von Configuration Manager nicht unterstützt.  

     Darüber hinaus wird der Cache eines Konfigurations-Manager-Clients auf einem SIS-fähigen Volume nicht unterstützt.  

- **Laufwerke mit Wechseldatenträger:** Die Installation von Configuration Manager-Standortsystemen oder Konfigurations-Manager-Clients auf einem Laufwerk mit Wechseldatenträger wird von Configuration Manager nicht unterstützt.