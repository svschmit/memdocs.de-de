---
title: Anforderungen an die Infrastruktur für Betriebssystembereitstellungen
titleSuffix: Configuration Manager
description: Informationen zu externen Abhängigkeiten und Produktabhängigkeiten sowie den Anforderungen für die Betriebssystembereitstellung in Configuration Manager
ms.date: 07/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 1dc74219-7ff5-4e3b-b4f6-5aad663bb75b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c9bb07bd2b82a9411bc527d04a9a64a0bb6e12f8
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697669"
---
# <a name="infrastructure-requirements-for-os-deployment-in-configuration-manager"></a>Anforderungen an die Infrastruktur für die Betriebssystembereitstellung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Für die Betriebssystembereitstellung in Configuration Manager sind sowohl externe als auch produktspezifische Abhängigkeiten vorhanden. Dieser Artikel unterstützt Sie bei der Planung der Infrastruktur für die Betriebssystembereitstellung.  

##  <a name="dependencies-external-to-configuration-manager"></a><a name="BKMK_ExternalDependencies"></a> Externe Abhängigkeiten von Configuration Manager  

Im folgenden Abschnitt finden Sie Informationen zu externen Tools, Installationspaketen und Betriebssystemversionen, die für die Bereitstellung von Betriebssystemen in Configuration Manager erforderlich sind.  

### <a name="windows-adk-for-windows-10"></a>Windows ADK für Windows 10  

Das Windows Assessment and Deployment Kit (ADK) umfasst Tools und Dokumentationen zur Unterstützung der Konfiguration und Bereitstellung von Windows. Mit dem Windows ADK automatisiert Configuration Manager Aktionen wie z.B. das Installieren von Windows, das Erfassen von Images und das Migrieren von Benutzerprofilen und Daten.  

Weitere Informationen finden Sie in den folgenden Artikeln:  

- [Windows ADK für Windows 10-Szenarien für IT-Experten](/windows/deployment/windows-adk-scenarios-for-it-pros)  

- [Windows ADK für Windows 10 herunterladen](/windows-hardware/get-started/adk-install)  

    > [!IMPORTANT]
    > Stellen Sie sicher, dass Sie sowohl das **Windows ADK für Windows 10** als auch das **Windows PE-Add-On für das ADK** herunterladen.

- [Unterstützung für Windows 10](../../core/plan-design/configs/support-for-windows-10.md)  

#### <a name="site-systems"></a>Standortsysteme
Das Windows ADK ist eine Voraussetzung für die folgenden Standortsystemserver:

- Der Standortserver des obersten Standorts in der Hierarchie  

- Der Standortserver eines jeden primären Standorts in der Hierarchie  

- Alle Instanzen des SMS-Anbieters  


> [!NOTE]  
> Installieren Sie das Windows ADK manuell auf allen Standortservern, bevor Sie den Configuration Manager-Standort installieren.  

#### <a name="windows-adk-features"></a>Windows ADK-Features
Installieren Sie die folgenden Features des Windows ADKs:  

-   Migrationsprogramm für den Benutzerzustand (USMT)  

    > [!Note]  
    > USMT ist nicht für den SMS-Anbieter erforderlich.

-   Windows-Bereitstellungstools  

-   Windows-Vorinstallationsumgebung (Windows Preinstallation Environment, Windows PE)  

    > [!Important]  
    > Ab Version 1809 von Windows 10 ist der Installer für Windows PE separat. Es wurden keine anderweitigen Änderungen an der Funktionsweise vorgenommen.<!--SCCMDocs-pr issue 2908-->  

Eine Liste der Versionen des Windows 10 ADKs, die Sie mit verschiedenen Versionen von Configuration Manager verwenden können, finden Sie unter [Unterstützung für Windows 10](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk).


### <a name="user-state-migration-tool-usmt"></a>Migrationsprogramm für den Benutzerzustand (USMT)  

Configuration Manager verwendet ein USMT-Paket mit den USMT 10-Quelldateien, die zum Erfassen und Wiederherstellen des Benutzerzustands als Teil Ihrer Betriebssystembereitstellung verwendet werden. Das Configuration Manager-Setup erstellt am Standort der obersten Ebene das USMT-Paket automatisch. USMT 10 erfasst den Benutzerzustand von Windows 7, Windows 8, Windows 8.1 und Windows 10.  

Weitere Informationen finden Sie in den folgenden Artikeln:  

- [Allgemeine Migrationsszenarien für USMT 10](/windows/deployment/usmt/usmt-common-migration-scenarios)  

- [Verwalten des Benutzerzustands](../get-started/manage-user-state.md)  


### <a name="windows-pe"></a>Windows PE  

Windows PE wird für Startabbilder verwendet, um einen Computer zu starten. Es handelt sich um eine Windows-Version mit begrenzten Diensten, die vor der Installation und während der Bereitstellung von Windows verwendet wird. In der folgenden Liste sind die unterstützten Versionen des Windows ADK für Configuration Manager (Current Branch) aufgeführt:  

#### <a name="windows-adk-version"></a>Windows ADK-Version  
Windows ADK für Windows 10. Weitere Informationen finden Sie unter [Unterstützung für Windows 10](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk).

#### <a name="windows-pe-versions-for-boot-images-customizable-from-the-configuration-manager-console"></a>Windows PE-Versionen für Startimages, die über die Configuration Manager-Konsole angepasst werden können  
Windows PE 10  

#### <a name="supported-windows-pe-versions-for-boot-images-not-customizable-from-the-configuration-manager-console"></a>Unterstützte Windows PE-Versionen für Startimages, die nicht über die Configuration Manager-Konsole angepasst werden können  
Windows PE 3.1<sup>1</sup> und Windows PE 5  

<sup>1</sup> Sie können zu Configuration Manager nur dann ein Startimage hinzufügen, wenn es auf Windows PE 3.1 basiert. Installieren Sie die Ergänzung zu Windows AIK für Windows 7 SP1, um ein Upgrade von Windows AIK für Windows 7 (basierend auf Windows PE 3) mit der Ergänzung zu Windows AIK für Windows 7 SP1 (basierend auf Windows PE 3.1) durchzuführen. Laden Sie die Ergänzung zu Windows AIK für Windows 7 SP1 aus dem [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=5188)herunter.  

Im Fall von Configuration Manager etwa können Sie Startimages aus Windows ADK für Windows 10 (das auf Windows PE 10 basiert) über die Configuration Manager-Konsole anpassen. Zwar werden auf Windows PE 5 basierende Startimages unterstützt, jedoch müssen Sie sie von einem anderen Computer aus anpassen und die mit dem Windows ADK für Windows 8 installierte DISM-Version verwenden. Fügen Sie danach das Startimage zur Configuration Manager-Konsole hinzu. Weitere Informationen und Vorgehensweisen zum Anpassen eines Startimages (Hinzufügen von optionalen Komponenten und Treibern), zum Aktivieren der Befehlsunterstützung für das Startimage, zum Hinzufügen des Startimages zur Configuration Manager-Konsole und zum Aktualisieren der Verteilungspunkte mit dem Startimage finden Sie unter [Anpassen von Startimages](../get-started/customize-boot-images.md). Weitere Informationen zu Startabbildern finden Sie im Thema [Verwalten von Startabbildern (Startimages)](../get-started/manage-boot-images.md).  


### <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)  

WSUS wird vom Softwareupdatepunkt benötigt, der zum Installieren von Softwareupdates bei der Betriebssystembereitstellung erforderlich ist. Weitere Informationen finden Sie unter [Installieren und Konfigurieren eines Softwareupdatepunkts](../../sum/get-started/install-a-software-update-point.md).


### <a name="internet-information-services-iis-on-the-site-system-servers"></a>Internetinformationsdienste (IIS) auf den Standortsystemservern  

IIS ist für den Verteilungspunkt, Zustandsmigrationspunkt und Verwaltungspunkt erforderlich. Weitere Informationen finden Sie unter [Site and site system prerequisites for System Center Configuration Manager](../../core/plan-design/configs/site-and-site-system-prerequisites.md) (Standort- und Standortsystemanforderungen für System Center Configuration Manager).  


### <a name="windows-deployment-services-wds"></a>Windows-Bereitstellungsdienste (Windows Deployment Services, WDS)  

Bis Version 1802 wird WDS für PXE-Bereitstellungen benötigt. Ab Version 1806 können Sie PXE auf einem Verteilungspunkt ohne WDS aktivieren. Weitere Informationen finden Sie unter [Windows-Bereitstellungsdienste](#BKMK_WDS) in diesem Artikel. 


### <a name="dynamic-host-configuration-protocol-dhcp"></a>Dynamic Host Configuration-Protokoll (DHCP)  

DHCP ist für PXE-Bereitstellungen erforderlich. Sie müssen über einen betriebsbereiten DHCP-Server mit einem aktiven Host verfügen, um Betriebssysteme per PXE bereitstellen zu können. Weitere Informationen zu PXE-Bereitstellungen finden Sie unter [Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  


### <a name="supported-operating-systems-and-hard-disk-configurations"></a>Unterstützte Betriebssysteme und Festplattenkonfigurationen  

Weitere Informationen zu den Betriebssystemversionen und Festplattenkonfigurationen, die Configuration Manager bei der Betriebssystembereitstellung unterstützt, finden Sie unter [Unterstützte Betriebssysteme](#BKMK_SupportedOS) und [Unterstützte Festplattenkonfigurationen](#BKMK_SupportedDiskConfig).  


### <a name="windows-device-drivers"></a>Windows-Gerätetreiber  

Bei der Installation des Betriebssystems auf dem Zielcomputer können Windows-Gerätetreiber verwendet werden. Diese werden auch verwendet, wenn Sie Windows PE über ein Startimage ausführen. Weitere Informationen finden Sie unter [Verwalten von Treibern](../get-started/manage-drivers.md).  



##  <a name="configuration-manager-dependencies"></a><a name="BKMK_InternalDependencies"></a> Abhängigkeiten in Configuration Manager  

Im folgenden Abschnitt finden Sie Informationen zu den Voraussetzungen für die Configuration Manager-Betriebssystembereitstellung.  


### <a name="os-image"></a>Betriebssystemabbild  

Betriebssystemimages in Configuration Manager werden im WIM-Dateiformat (Windows Imaging) gespeichert. Sie stellen eine komprimierte Sammlung von Verweisdateien und Ordnern dar. Diese Images sind für die erfolgreiche Installation und Konfiguration eines Betriebssystems auf einem Computer erforderlich. Weitere Informationen finden Sie unter [Verwalten von Betriebssystemimages](../get-started/manage-operating-system-images.md).  


### <a name="driver-catalog"></a>Treiberkatalog  

Zur Bereitstellung eines Gerätetreibers müssen Sie den Gerätetreiber importieren, aktivieren und auf einem Verteilungspunkt verfügbar machen, auf den der Konfigurations-Manager-Client zugreifen kann. Weitere Informationen finden Sie unter [Verwalten von Treibern](../get-started/manage-drivers.md).  


### <a name="management-point"></a>Verwaltungspunkt  

Daten zwischen Clients und dem Configuration Manager-Standort werden über Verwaltungspunkte übertragen. Der Client verwendet einen Verwaltungspunkt zum Ausführen der Tasksequenz, um die Bereitstellung des Betriebssystems abzuschließen. Weitere Informationen zu Tasksequenzen finden Sie unter [Planungsüberlegungen für das Automatisieren von Tasks](planning-considerations-for-automating-tasks.md).  


### <a name="distribution-point"></a>Verteilungspunkt  

Verteilungspunkte werden in den meisten Bereitstellungen verwendet, um Daten für die Betriebssystembereitstellung wie Treiberpakete oder das Image zu speichern. In Tasksequenzen werden Daten normalerweise von einem Verteilungspunkt abgerufen, um das Betriebssystem bereitzustellen. Weitere Informationen zum Installieren von Verteilungspunkten und Verwalten von Inhalt finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  


### <a name="pxe-enabled-distribution-point"></a>PXE-fähiger Verteilungspunkt  

Konfigurieren Sie für mit PXE-initiierte Bereitstellungen einen Verteilungspunkt so, dass die von Clients gestellten PXE-Anforderungen vom Verteilungspunkt akzeptiert werden. Weitere Informationen finden Sie unter [Konfigurieren eines Verteilungspunkts](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).


### <a name="multicast-enabled-distribution-point"></a>Multicast-fähiger Verteilungspunkt  

Wenn Sie Ihre Betriebssystembereitstellungen mithilfe von Multicast optimieren möchten, müssen Sie einen Verteilungspunkt für die Unterstützung von Multicast konfigurieren. Weitere Informationen finden Sie unter [Konfigurieren eines Verteilungspunkts](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast).   


### <a name="state-migration-point"></a>Zustandsmigrationspunkt  

Wenn Sie Benutzerzustandsdaten für parallele oder aktualisierte Bereitstellungen erfassen und wiederherstellen möchten, müssen Sie einen Zustandsmigrationspunkt zum Speichern der Benutzerzustandsdaten auf einem anderen Computer konfigurieren.  

Weitere Informationen zum Konfigurieren des Zustandsmigrationspunkts finden Sie unter [Zustandsmigrationspunkt](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

Weitere Informationen zum Erfassen und Wiederherstellen des Benutzerzustands finden Sie unter [Verwalten des Benutzerzustands](../get-started/manage-user-state.md).  


### <a name="reporting-services-point"></a>Reporting Services-Punkt  

Installieren und Konfigurieren Sie zur Verwendung von Configuration Manager-Berichten für Betriebssystembereitstellungen einen Berichterstattungspunkt. Weitere Informationen finden Sie unter [Einführung in die Berichterstellung](../../core/servers/manage/introduction-to-reporting.md).  


### <a name="security-permissions-for-os-deployments"></a>Sicherheitsberechtigungen für Betriebssystembereitstellungen  

Die Sicherheitsrolle **Betriebssystembereitstellungs-Manager** ist eine integrierte Rolle und kann nicht geändert werden. Sie können jedoch eine Kopie dieser Sicherheitsrolle erstellen, ändern und als neue benutzerdefinierte Sicherheitsrolle speichern. Zu den Berechtigungen, die direkt auf Betriebssystembereitstellungen angewendet werden, gehören die folgenden:  

- **Startabbildpaket**: Erstellen, Löschen, Ändern, Ordner ändern, Objekt verschieben, Lesen, Sicherheitsbereich festlegen  

- **Gerätetreiber**: Erstellen, Löschen, Ändern, Ordner ändern, Bericht ändern, Objekt verschieben, Lesen, Bericht ausführen  

- **Treiberpaket**: Erstellen, Löschen, Ändern, Ordner ändern, Objekt verschieben, Lesen, Sicherheitsbereich festlegen  

- **Betriebssystemabbild**: Erstellen, Löschen, Ändern, Ordner ändern, Objekt verschieben, Lesen, Sicherheitsbereich festlegen  

- **Aktualisierungspaket für das Betriebssystem**: Erstellen, Löschen, Ändern, Ordner ändern, Objekt verschieben, Lesen, Sicherheitsbereich festlegen  

- **Tasksequenzpaket**: Erstellen, Tasksequenzmedien erstellen, Löschen, Ändern, Ordner ändern, Bericht ändern, Objekt verschieben, Lesen, Bericht ausführen, Sicherheitsbereich festlegen  

Weitere Informationen finden Sie unter [Erstellen benutzerdefinierter Sicherheitsrollen](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole).  


### <a name="security-scopes-for-os-deployments"></a>Sicherheitsbereiche für Betriebssystembereitstellungen  

Verwenden Sie Sicherheitsbereiche, um Administratoren Zugriff auf in Betriebssystembereitstellungen verwendete sicherungsfähige Objekte wie Betriebssystemimages, Startimages, Treiberpakete und Tasksequenzpakete zu gewähren. Weitere Informationen finden Sie unter [Sicherheitsbereiche](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope).  



##  <a name="windows-deployment-services"></a><a name="BKMK_WDS"></a> Windows-Bereitstellungsdienste  

Bis Version 1802 müssen die Windows-Bereitstellungsdienste (Windows Deployment Services, WDS) auf dem gleichen Server installiert sein wie die Verteilungspunkte, die Sie für die Unterstützung von PXE oder Multicast konfigurieren. Die WDS sind im Serverbetriebssystem enthalten. Bei PXE-Bereitstellungen wird der PXE-Start von den Windows-Bereitstellungsdiensten ausgeführt. Wenn der Verteilungspunkt installiert und PXE-fähig ist, erstellt Configuration Manager einen Anbieter in WDS, von dem die PXE-Startfunktionen der Windows-Bereitstellungsdienste verwendet werden.  

Ab Version 1806 können Sie PXE auf einem Verteilungspunkt ohne WDS aktivieren. Weitere Informationen finden Sie unter **Aktivieren eines PXE-Antwortdienst ohne Windows-Bereitstellungsdienste** im Artikel [Installieren und Konfigurieren von Verteilungspunkten](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).


> [!NOTE]  
>  Wenn der Server einen Neustart fordert, kann die Installation der WDS fehlschlagen. 


### <a name="wds-requirements"></a>WDS-Anforderungen  

-   Zur Installation von WDS auf dem Server muss der Administrator Mitglied der lokalen Administratorgruppe sein.  

-   Der WDS-Server muss entweder Mitglied einer Active Directory-Domäne oder ein Domänencontroller für eine Active Directory-Domäne sein. Alle Windows-Domänen- und Gesamtstrukturkonfigurationen unterstützen WDS.  

-   Wenn der Anbieter auf einem Remoteserver installiert ist, installieren Sie die WDS auf dem Standortserver und dem Remoteanbieter.  


###  <a name="considerations-when-you-have-wds-and-dhcp-on-the-same-server"></a><a name="BKMK_WDSandDHCP"></a> Aspekte, wenn sich Windows-Bereitstellungsdienst und DHCP auf demselben Server befinden  

Wenn Sie planen, den Verteilungspunkt auf dem gleichen Server zu hosten, auf dem DHCP ausgeführt wird, sollten Sie die folgenden Konfigurationsoptionen in Erwägung ziehen:  

-   Sie benötigen einen funktionsfähigen DHCP-Server mit einem aktiven Bereich. WDS verwendet PXE, wofür ein DHCP-Server erforderlich ist.  

-   Zum Ausführen von WDS wird ein DNS-Server benötigt.  

-   Folgende UDP-Ports müssen auf dem WDS-Server geöffnet sein:  

    -   Port 67 (DHCP)  

    -   Port 69 (TFTP)  

    -   Port 4011 (PXE)  

    > [!NOTE]  
    >  Falls eine DHCP-Autorisierung auf dem Server erforderlich ist, muss auf diesem der DHCP-Clientport 68 geöffnet sein.  

-   Sowohl für DHCP als auch für WDS muss die Portnummer 67 verwendet werden. Wenn Sie WDS und DHCP zusammen hosten, können Sie den DHCP-Server oder den für PXE konfigurierten Verteilungspunkt auf einen separaten Server verschieben. Alternativ können Sie mit den folgenden Schritten den WDS-Server so konfigurieren, dass dieser auf einem anderen Port lauscht.  

#### <a name="to-configure-the-wds-server-to-listen-on-a-different-port"></a>So konfigurieren Sie den WDS-Server zum Lauschen auf einem anderen Port:  

1.  Ändern Sie den folgenden Registrierungsschlüssel:  

     `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WDSServer\Providers\WDSPXE`  

2.  Legen Sie den Registrierungswert **UseDHCPPorts** auf **0** fest.  

3.  Damit die neue Konfiguration wirksam wird, führen Sie den folgenden Befehl auf dem Server aus:  

     `WDSUTIL /Set-Server /UseDHCPPorts:No /DHCPOption60:Yes`  

> [!NOTE]
> Bis zur Version 1810 wird die Verwendung des PXE-Antwortdiensts ohne WDS auf Servern, auf denen auch ein DHCP-Server ausgeführt wird, nicht unterstützt.
>
> Ab der Version 1902 gilt: Wenn Sie einen PXE-Antwortdienst auf einem Verteilungspunkt ohne Windows-Bereitstellungsdienst aktivieren, kann er sich nun auf dem gleichen Server befinden wie der DHCP-Dienst. Weitere Informationen finden Sie unter [Configure at least one distribution point to accept PXE requests (Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk mit Configuration Manager)](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md#BKMK_Configure).


##  <a name="supported-operating-systems"></a><a name="BKMK_SupportedOS"></a> Unterstützte Betriebssysteme  

Alle Windows-Betriebssysteme, die unter [Unterstützte Betriebssysteme für Clients und Geräte](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md) aufgeführt sind, werden für Betriebssystembereitstellungen unterstützt.  



##  <a name="supported-disk-configurations"></a><a name="BKMK_SupportedDiskConfig"></a> Unterstützte Festplattenkonfigurationen  

In der folgenden Tabelle sind die für die Configuration Manager-Betriebssystembereitstellung unterstützten Kombinationen der Festplattenkonfiguration auf dem Referenz- und Zielcomputer aufgelistet:  

|Festplattenkonfiguration auf Referenzcomputer|Festplattenkonfiguration auf Zielcomputer|  
|------------------------------------------------|--------------------------------------------------|  
|Basisfestplatte|Basisfestplatte|  
|Einfaches Volume auf einer dynamischen Festplatte|Einfaches Volume auf einer dynamischen Festplatte|  

Configuration Manager unterstützt das Erfassen eines Betriebssystemimages nur über Computer, die mit einfachen Volumes konfiguriert sind. Die folgenden Festplattenkonfigurationen werden nicht unterstützt:  

-   Übergreifende Volumes  

-   Stripesetvolumes (RAID 0)  

-   Gespiegelte Volumes (RAID 1)  

-   Paritätsvolumes (RAID 5)  

Die zusätzliche, in der folgenden Tabelle angegebene Festplattenkonfiguration auf dem Referenz- und Zielcomputer wird in Configuration Manager bei der Betriebssystembereitstellung nicht unterstützt.  

|Festplattenkonfiguration auf Referenzcomputer|Festplattenkonfiguration auf Zielcomputer|  
|------------------------------------------------|--------------------------------------------------|  
|Basisfestplatte|Dynamische Festplatte|  



## <a name="next-steps"></a>Nächste Schritte

- [Vorbereiten von Standortsystemrollen für Betriebssystembereitstellungen](../get-started/prepare-site-system-roles-for-operating-system-deployments.md)
- [Prepare for OS deployment (Vorbereiten der Betriebssystembereitstellung)](../get-started/prepare-for-operating-system-deployment.md)