---
title: Voraussetzungen von Standorten
titleSuffix: Configuration Manager
description: Erfahren Sie, wie ein Windows-Computer als Configuration Manager-Standortsystemserver konfiguriert wird.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1392797b-76cb-46b4-a3e4-8f349ccaa078
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ce3420a6e229b5987616c5c0c1c41d50cdc499c8
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700349"
---
# <a name="site-and-site-system-prerequisites-for-configuration-manager"></a>Voraussetzungen für Standorte und Standortsysteme für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Windows-basierte Computer erfordern bestimmte Konfigurationen zur Unterstützung ihrer Verwendung als Configuration Manager-Standortsystemserver.

Bei einigen Produkten wie Windows Server Update Services (WSUS) für den Softwareupdatepunkt finden Sie Informationen zu weiteren Voraussetzungen und Einschränkungen zur Nutzung in der Produktdokumentation. Hier werden nur Konfigurationen beschrieben, die sich direkt auf die Verwendung mit Configuration Manager beziehen.

Weitere Informationen zu .NET Framework finden Sie unter [Häufig gestellte Fragen zu Lifecycle – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework).


## <a name="general-requirements-and-limitations"></a><a name="bkmk_generalprerewq"></a> Allgemeine Anforderungen und Einschränkungen

Folgende Anforderungen gelten für alle Standortsystemserver:

- Jeder Standortsystemserver muss ein 64-Bit-Betriebssystem verwenden. Die einzige Ausnahme gilt für die Standortsystemrolle „Verteilungspunkt“, die unter manchen 32-Bit-Betriebssystemen installiert werden kann.  

- Standortsysteme werden unter keinem Betriebssystem auf Server Core-Installationen unterstützt. Eine Ausnahme ist, dass Server Core-Installationen für die Standortsystemrolle „Verteilungspunkt“ unterstützt werden. Weitere Informationen finden Sie unter [Unterstützte Betriebssysteme für Clients und Geräte für Configuration Manager](supported-operating-systems-for-site-system-servers.md).  

- Nach der Installation eines Standortsystemservers können folgende Elemente nicht geändert werden:  

    - Der Domänenname der Domäne, in der sich der Standortsystemcomputer befindet (wird auch als **Domänenumbenennung** bezeichnet)  

    - Die Domänenmitgliedschaft des Computers  

    - Der Name des Computers.  

    Wenn Sie eines dieser Elemente ändern müssen, entfernen Sie zuerst die Standortsystemrolle vom Computer. Nachdem Sie die Änderung durchgeführt haben, installieren Sie die Rolle neu. Bei Änderungen, die sich auf den Standortserver auswirken, deinstallieren Sie zunächst den Standort. Nachdem Sie die Änderung durchgeführt haben, installieren Sie den Standort neu.  

- Standortsystemrollen werden auf Instanzen von Windows Server-Clustern nicht unterstützt. Die einzige Ausnahme gilt für den Standortdatenbankserver. Weitere Informationen finden Sie unter [Verwenden eines SQL Server-Clusters für die Standortdatenbank von Configuration Manager](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md).  

    Ab Version 1810 blockiert der Einrichtungsprozess für Configuration Manager nicht mehr die Installation der Standortserverrolle auf einem Computer mit der Windows-Rolle für Failoverclustering. SQL Always On erfordert diese Rolle, daher konnten Sie die Standortdatenbank auf dem Standortserver bisher nicht gleichzeitig installieren. Mit dieser Änderung haben Sie die Möglichkeit, eine hochverfügbare Website mit weniger Servern zu erstellen, indem Sie SQL Always On und einen Standortserver im passiven Modus verwenden. Weitere Informationen finden Sie unter [High availability options (Optionen für Hochverfügbarkeit)](../../servers/deploy/configure/high-availability-options.md). <!--3607761, fka 1359132-->  

- Die Änderung der Einstellungen für Starttyp und „Anmelden als“ für beliebige Configuration Manager-Dienste wird nicht unterstützt. Wenn Sie die Einstellungen trotzdem ändern, werden wichtige Dienste möglicherweise nicht ordnungsgemäß ausgeführt.  

### <a name="prerequisites-for-windows-server-2012-and-later-operating-systems"></a><a name="bkmk_2012Prereq"></a> Voraussetzungen für Windows Server 2012 und höhere Betriebssysteme  

Informationen zu den jeweiligen Voraussetzungen für Standortsystemserver und -rollen unter Windows Server 2012 und höher finden Sie in den Hauptabschnitten dieses Artikels:

- [Standort der zentralen Verwaltung und primäre Standortserver](#bkmk_2012sspreq)
- [Sekundärer Standortserver](#bkmk_2012secpreq)
- [Datenbankserver](#bkmk_2012dbpreq)
- [SMS-Anbieterserver](#bkmk_2012smsprovpreq)
- [Anwendungskatalog-Websitepunkt](#bkmk_2012acwspreq)
- [Anwendungskatalog-Webdienstpunkt](#bkmk_2012ACwsitepreq)
- [Asset Intelligence-Synchronisierungspunkt](#bkmk_2012AIpreq)
- [Zertifikatregistrierungspunkt](#bkmk_2012crppreq)
- [Verteilungspunkt](#bkmk_2012dppreq)
- [Endpoint Protection-Punkt](#bkmk_2012EPPpreq)
- [Registrierungspunkt](#bkmk_2012Enrollpreq)
- [Anmeldungsproxypunkt](#bkmk_2012EnrollProxpreq)
- [Fallbackstatuspunkt](#bkmk_2012FSPpreq)
- [Verwaltungspunkt](#bkmk_2012MPpreq)
- [Reporting Services-Punkt](#bkmk_2012RSpoint)
- [Dienstverbindungspunkt](#bkmk_SCPpreq)
- [Softwareupdatepunkt](#bkmk_2012SUPpreq)
- [Zustandsmigrationspunkt](#bkmk_2012SMPpreq)

## <a name="central-administration-site-and-primary-site-servers"></a><a name="bkmk_2012sspreq"></a> Standort der zentralen Verwaltung und primäre Standortserver

### <a name="windows-server-roles-and-features"></a>Windows Server-Rollen und -Features

- .NET Framework 3.5

- Remotedifferenzialkomprimierung  

- Wenn Sie einen Softwareupdatepunkt auf einem anderen Server als dem Standortserver verwenden, installieren Sie auf dem Standortserver die WSUS-Verwaltungskonsole.

### <a name="net-framework"></a>.NET Framework

Aktivieren Sie das Windows-Feature für .NET Framework 3.5.

Installieren Sie außerdem eine unterstützte Version von .NET Framework Version 4.5 oder höher. Ab Version 1906 unterstützt Configuration Manager .NET Framework 4.8.

Weitere Informationen zu .NET Framework-Versionen finden Sie in den folgenden Artikeln:

- [.NET Framework – Versionen und Abhängigkeiten](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Häufig gestellte Fragen zu Lifecycle – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="windows-adk"></a>Windows ADK  

- Bevor Sie einen Standort der zentralen Verwaltung oder einen primären Standort installieren oder aktualisieren, installieren Sie die Version von Windows ADK (Assessment and Deployment Kit), die die Version von Configuration Manager erfordert, die Sie installieren oder aktualisieren. Weitere Informationen finden Sie unter [Windows 10 ADK](support-for-windows-10.md#windows-10-adk).  

- Weitere Informationen zu dieser Anforderung finden Sie unter [Anforderungen an die Infrastruktur für die Betriebssystembereitstellung](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

### <a name="visual-c-redistributable"></a>Visual C++ Redistributable  

- Configuration Manager installiert Microsoft Visual C++ 2013 Redistributable Package auf jedem Computer, auf dem ein Standortserver installiert wird.  

- Standorte der zentralen Verwaltung und primäre Standorte erfordern sowohl die x86- als auch die x64-Version der betreffenden Redistributable-Datei.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Wenn Sie einen neuen Standort installieren, installiert Configuration Manager automatisch SQL Server Native Client als weitervertreibbare Komponente. Nach der Installation des Standorts führt Configuration Manager kein Upgrade für den SQL Server Native Client durch. Stellen Sie sicher, dass diese Komponente auf dem neuesten Stand ist. Weitere Informationen finden Sie unter [Voraussetzungsprüfungen – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="secondary-site-server"></a><a name="bkmk_2012secpreq"></a> Sekundärer Standortserver

### <a name="windows-server-roles-and-features"></a>Windows Server-Rollen und -Features

- .NET Framework 3.5

- Remotedifferenzialkomprimierung  

### <a name="net-framework"></a>.NET Framework

Aktivieren Sie das Windows-Feature für .NET Framework 3.5.

Installieren Sie außerdem eine unterstützte Version von .NET Framework Version 4.5 oder höher. Ab Version 1906 unterstützt Configuration Manager .NET Framework 4.8.

Weitere Informationen zu .NET Framework-Versionen finden Sie in den folgenden Artikeln:

- [.NET Framework – Versionen und Abhängigkeiten](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Häufig gestellte Fragen zu Lifecycle – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="visual-c-redistributable"></a>Visual C++ Redistributable

- Configuration Manager installiert Microsoft Visual C++ 2013 Redistributable Package auf jedem Computer, auf dem ein Standortserver installiert wird.  

- Sekundäre Standorte erfordern nur die x64-Version.  

### <a name="default-site-system-roles"></a>Standard-Standortsystemrollen  

- Standardmäßig werden von einem sekundären Standort ein **Verwaltungspunkt** und ein **Verteilungspunkt** installiert.  

- Stellen Sie sicher, dass der sekundäre Standortserver die Voraussetzungen für diese Standortsystemrollen erfüllt.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Wenn Sie einen neuen Standort installieren, installiert Configuration Manager automatisch SQL Server Native Client als weitervertreibbare Komponente. Nach der Installation des Standorts führt Configuration Manager kein Upgrade für den SQL Server Native Client durch. Stellen Sie sicher, dass diese Komponente auf dem neuesten Stand ist. Weitere Informationen finden Sie unter [Voraussetzungsprüfungen – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="database-server"></a><a name="bkmk_2012dbpreq"></a> Datenbankserver  

### <a name="remote-registry-service"></a>Remote-Registrierungsdienst  

- Aktivieren Sie während der Installation des Configuration Manager-Standorts den **Remoteregistrierungsdienst** auf dem Computer, auf dem die Standortdatenbank gehostet wird.  

### <a name="sql-server"></a>SQL Server  

- Bevor Sie einen Standort der zentralen Verwaltung oder einen primären Standort installieren, installieren Sie eine unterstützte Version von SQL Server zum Hosten der Standortdatenbank. Weitere Informationen finden Sie unter [Unterstützte SQL Server-Versionen](support-for-sql-server-versions.md).  

- Bevor Sie einen sekundären Standort installieren, können Sie eine unterstützte Version von SQL Server installieren.  

- Wenn Sie entscheiden, dass Configuration Manager im Rahmen der Installation des sekundären Standorts SQL Server Express installieren soll, stellen Sie sicher, dass der Computer die Voraussetzungen zur Ausführung von SQL Server Express erfüllt.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Wenn Sie einen neuen Standort installieren, installiert Configuration Manager automatisch SQL Server Native Client als weitervertreibbare Komponente. Nach der Installation des Standorts führt Configuration Manager kein Upgrade für den SQL Server Native Client durch. Stellen Sie sicher, dass diese Komponente auf dem neuesten Stand ist. Weitere Informationen finden Sie unter [Voraussetzungsprüfungen – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="sms-provider-server"></a><a name="bkmk_2012smsprovpreq"></a> SMS-Anbieterserver  

### <a name="windows-adk"></a>Windows ADK

- Auf dem Computer, auf dem Sie eine SMS-Anbieterinstanz installieren, muss die Windows ADK-Version installiert sein, die für die von Ihnen installierte bzw. aktualisierte Version von Configuration Manager erforderlich ist. Weitere Informationen finden Sie unter [Windows 10 ADK](support-for-windows-10.md#windows-10-adk).  

- Weitere Informationen zu dieser Anforderung finden Sie unter [Anforderungen an die Infrastruktur für die Betriebssystembereitstellung](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

### <a name="windows-server-roles-and-features"></a>Windows Server-Rollen und -Features

- Wenn Sie den [Verwaltungsdienst](../../../develop/adminservice/overview.md) verwenden, ist für den Server, auf dem die SMS-Anbieterrolle ausgeführt wird, .NET 4.5 oder höher erforderlich  <!-- SCCMDocs issue #1203 -->

    > [!NOTE]
    > Für Configuration Manager, Version 1810, ist .NET 4.5.2 oder höher erforderlich.

- Web Server (IIS): Jeder Anbieter versucht, den [Verwaltungsdienst](../../../develop/adminservice/overview.md) zu installieren. Dieser Dienst hat eine Abhängigkeit von IIS, um ein Zertifikat an HTTPS-Port 443 zu binden. Configuration Manager verwendet IIS-APIs, um diese Zertifikatkonfiguration zu überprüfen. Wenn Sie den Standort für [Erweitertes HTTP](../hierarchy/enhanced-http.md) konfigurieren, verwendet Configuration Manager IIS-APIs, um eine Bindung an das vom Standort generierte Zertifikat herzustellen. Ab Version 2002 verwendet der Standort automatisch das selbst signierte Zertifikat des Standorts.

### <a name="sql-server-native-client"></a>SQL Server Native Client

Wenn Sie einen neuen Standort installieren, installiert Configuration Manager automatisch SQL Server Native Client als weitervertreibbare Komponente. Nach der Installation des Standorts führt Configuration Manager kein Upgrade für den SQL Server Native Client durch. Stellen Sie sicher, dass diese Komponente auf dem neuesten Stand ist. Weitere Informationen finden Sie unter [Voraussetzungsprüfungen – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="application-catalog-website-point"></a><a name="bkmk_2012acwspreq"></a> Anwendungskatalog-Websitepunkt  

> [!Important]  
> Die Silverlight-Benutzeroberfläche für den Anwendungskatalog wird ab Current Branch-Version 1806 nicht unterstützt. Ab Version 1906 verwenden aktualisierte Clients automatisch den Verwaltungspunkt für Anwendungsbereitstellungen, die Benutzern zur Verfügung stehen. Zudem können Sie keine neuen Anwendungskatalogrollen installieren. Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910.  
>
> Weitere Informationen finden Sie in den folgenden Artikeln:
>
> - [Konfigurieren des Softwarecenters](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Entfernte und veraltete Features](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

### <a name="windows-server-roles-and-features"></a>Windows Server-Rollen und -Features

- .NET Framework 3.5

- ASP.NET 4.5  

### <a name="net-framework"></a>.NET Framework

Aktivieren Sie das Windows-Feature für .NET Framework 3.5.

Installieren Sie außerdem eine unterstützte Version von .NET Framework Version 4.5 oder höher.

Weitere Informationen zu .NET Framework-Versionen finden Sie in den folgenden Artikeln:

- [.NET Framework – Versionen und Abhängigkeiten](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Häufig gestellte Fragen zu Lifecycle – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS-Konfiguration  

- Allgemeine HTTP-Features:  

    - Standarddokument  

    - Statischer Inhalt  

- Anwendungsentwicklung:  

    - ASP.NET 3.5 (und automatisch ausgewählte Optionen)  

    - ASP.NET 4.5 (und automatisch ausgewählte Optionen)  

    - .NET-Erweiterbarkeit 3.5  

    - .NET-Erweiterbarkeit 4.5  

- Sicherheit:  

    - Windows-Authentifizierung  

- IIS 6-Verwaltungskompatibilität:  

    - IIS 6-Metabasiskompatibilität  


## <a name="application-catalog-web-service-point"></a><a name="bkmk_2012ACwsitepreq"></a> Anwendungskatalog-Webdienstpunkt  

> [!Important]  
> Die Silverlight-Benutzeroberfläche für den Anwendungskatalog wird ab Current Branch-Version 1806 nicht unterstützt. Ab Version 1906 verwenden aktualisierte Clients automatisch den Verwaltungspunkt für Anwendungsbereitstellungen, die Benutzern zur Verfügung stehen. Zudem können Sie keine neuen Anwendungskatalogrollen installieren. Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910.  
>
> Weitere Informationen finden Sie in den folgenden Artikeln:
>
> - [Konfigurieren des Softwarecenters](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Entfernte und veraltete Features](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

### <a name="windows-server-roles-and-features"></a>Windows Server-Rollen und -Features

- .NET Framework 3.5

- ASP.NET 4.5:  

    - HTTP-Aktivierung (und automatisch ausgewählte Optionen)  

### <a name="net-framework"></a>.NET Framework

Aktivieren Sie das Windows-Feature für .NET Framework 3.5.

Installieren Sie außerdem eine unterstützte Version von .NET Framework Version 4.5 oder höher.

Weitere Informationen zu .NET Framework-Versionen finden Sie in den folgenden Artikeln:

- [.NET Framework – Versionen und Abhängigkeiten](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Häufig gestellte Fragen zu Lifecycle – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS-Konfiguration

- Allgemeine HTTP-Features:  

    - Standarddokument  

- IIS 6-Verwaltungskompatibilität:  

    - IIS 6-Metabasiskompatibilität  

- Anwendungsentwicklung:  

    - ASP.NET 3.5 (und automatisch ausgewählte Optionen)  

    - .NET-Erweiterbarkeit 3.5  

    - ASP.NET 4.5 (und automatisch ausgewählte Optionen)  

    - .NET-Erweiterbarkeit 4.5  

### <a name="computer-memory"></a>Arbeitsspeicher  

- Auf dem Computer, der diese Standortsystemrolle hostet, müssen mindestens 5 % des verfügbaren Speicher frei sein, um die Verarbeitung von Anforderungen durch die Standortsystemrolle zu ermöglichen.  

- Wenn diese Standortsystemrolle zusammen mit einer anderen Standortsystemrolle installiert wird, für die dieselbe Anforderung gilt, wird die Speicheranforderung für den Computer nicht erhöht, die Mindestanforderung von 5 % besteht jedoch weiter.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Wenn Sie einen neuen Standort installieren, installiert Configuration Manager automatisch SQL Server Native Client als weitervertreibbare Komponente. Nach der Installation des Standorts führt Configuration Manager kein Upgrade für den SQL Server Native Client durch. Stellen Sie sicher, dass diese Komponente auf dem neuesten Stand ist. Weitere Informationen finden Sie unter [Voraussetzungsprüfungen – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="asset-intelligence-synchronization-point"></a><a name="bkmk_2012AIpreq"></a> Asset Intelligence-Synchronisierungspunkt  

### <a name="net-framework"></a>.NET Framework

Installieren Sie eine unterstützte Version von .NET Framework, Version 4.5 oder höher. Ab Version 1906 unterstützt Configuration Manager .NET Framework 4.8.

Weitere Informationen zu .NET Framework-Versionen finden Sie in den folgenden Artikeln:

- [.NET Framework – Versionen und Abhängigkeiten](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Häufig gestellte Fragen zu Lifecycle – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="sql-server-native-client"></a>SQL Server Native Client

Wenn Sie einen neuen Standort installieren, installiert Configuration Manager automatisch SQL Server Native Client als weitervertreibbare Komponente. Nach der Installation des Standorts führt Configuration Manager kein Upgrade für den SQL Server Native Client durch. Stellen Sie sicher, dass diese Komponente auf dem neuesten Stand ist. Weitere Informationen finden Sie unter [Voraussetzungsprüfungen – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="certificate-registration-point"></a><a name="bkmk_2012crppreq"></a> Zertifikatregistrierungspunkt  

### <a name="windows-server-roles-and-features"></a>Windows Server-Rollen und -Features

- .NET Framework

    - HTTP-Aktivierung  

### <a name="net-framework"></a>.NET Framework

Installieren Sie eine unterstützte Version von .NET Framework, Version 4.5 oder höher. Ab Version 1906 unterstützt Configuration Manager .NET Framework 4.8.

Weitere Informationen zu .NET Framework-Versionen finden Sie in den folgenden Artikeln:

- [.NET Framework – Versionen und Abhängigkeiten](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Häufig gestellte Fragen zu Lifecycle – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS-Konfiguration

- Anwendungsentwicklung:  

    - ASP.NET 3.5 (und automatisch ausgewählte Optionen)  

    - ASP.NET 4.5 (und automatisch ausgewählte Optionen)  

- IIS 6-Verwaltungskompatibilität:  

    - IIS 6-Metabasiskompatibilität  

    - IIS 6-WMI-Kompatibilität  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Wenn Sie einen neuen Standort installieren, installiert Configuration Manager automatisch SQL Server Native Client als weitervertreibbare Komponente. Nach der Installation des Standorts führt Configuration Manager kein Upgrade für den SQL Server Native Client durch. Stellen Sie sicher, dass diese Komponente auf dem neuesten Stand ist. Weitere Informationen finden Sie unter [Voraussetzungsprüfungen – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="distribution-point"></a><a name="bkmk_2012dppreq"></a> Verteilungspunkt  

### <a name="windows-server-roles-and-features"></a>Windows Server-Rollen und -Features

- Remotedifferenzialkomprimierung  

#### <a name="iis-configuration"></a>IIS-Konfiguration

- Anwendungsentwicklung:  

    - ISAPI-Erweiterungen  

- Sicherheit:  

    - Windows-Authentifizierung  

- IIS 6-Verwaltungskompatibilität:  

    - IIS 6-Metabasiskompatibilität  

    - IIS 6-WMI-Kompatibilität  

### <a name="powershell"></a>PowerShell  

- Unter Windows Server 2012 oder höher ist PowerShell 3.0 oder 4.0 vor der Installation des Verteilungspunkts erforderlich.  

### <a name="visual-c-redistributable"></a>Visual C++ Redistributable

- Configuration Manager installiert Microsoft Visual C++ 2013 Redistributable Package auf jedem Computer, auf dem ein Verteilungspunkt gehostet wird.  

- Welche Version installiert wird, hängt von der Computerplattform (x86 oder x64) ab.  

### <a name="microsoft-azure"></a>Microsoft Azure  

- Sie können einen Clouddienst in Microsoft Azure verwenden, um einen Verteilungspunkt zu hosten.  

### <a name="to-support-pxe-or-multicast"></a>So unterstützen Sie PXE oder Multicast  

- Aktivieren Sie einen PXE-Antwortdienst auf einem Verteilungspunkt ohne Windows-Bereitstellungsdienst.  

- Installieren und konfigurieren Sie die Windows Serverrolle „Windows-Bereitstellungsdienste“ (Windows Deployment Services, WDS).  

    > [!NOTE]  
    > WDS wird automatisch installiert und konfiguriert, wenn Sie einen Verteilungspunkt zur Unterstützung von PXE oder Multicast auf einem Server konfigurieren, der Windows Server 2012 oder höher ausführt.  

- Stellen Sie bei einem multicastfähigen Verteilungspunkt sicher, dass der SQL Server Native Client installiert und auf dem neuesten Stand ist. Weitere Informationen finden Sie unter [Voraussetzungsprüfungen – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

Weitere Informationen finden Sie unter [Installieren und Konfigurieren von Verteilungspunkten](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).

<!--sms.503672 -Clarified BITS use-->
> [!NOTE]  
> Wenn der Verteilungspunkt Inhalte überträgt, erfolgt die Übertragung über den in Windows integrierten **Background Intelligent Transfer Service** (BITS). Für die Verteilungspunktrolle muss nicht das optionale BITS-IIS-Servererweiterungsfeature installiert werden, da der Client keine Informationen in die Rolle hochlädt.  


## <a name="endpoint-protection-point"></a><a name="bkmk_2012EPPpreq"></a> Endpoint Protection-Punkt  

### <a name="windows-server-roles-and-features"></a>Windows Server-Rollen und -Features  

- .NET Framework 3.5

- Windows Defender-Features (ab Windows Server 2016)  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Wenn Sie einen neuen Standort installieren, installiert Configuration Manager automatisch SQL Server Native Client als weitervertreibbare Komponente. Nach der Installation des Standorts führt Configuration Manager kein Upgrade für den SQL Server Native Client durch. Stellen Sie sicher, dass diese Komponente auf dem neuesten Stand ist. Weitere Informationen finden Sie unter [Voraussetzungsprüfungen – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="enrollment-point"></a><a name="bkmk_2012Enrollpreq"></a> Anmeldungspunkt  

### <a name="windows-server-roles-and-features"></a>Windows Server-Rollen und -Features

- .NET Framework 3.5

    - HTTP-Aktivierung (und automatisch ausgewählte Optionen)  

    - ASP.NET 4.5  

    - Windows Communication Foundation (WCF)<!-- SCCMDocs issue #1168 -->  

### <a name="net-framework"></a>.NET Framework

Aktivieren Sie das Windows-Feature für .NET Framework 3.5.

Installieren Sie außerdem eine unterstützte Version von .NET Framework Version 4.5 oder höher. Ab Version 1906 unterstützt Configuration Manager .NET Framework 4.8.

> [!Note]
> Bei der Installation dieser Standortsystemrolle installiert Configuration Manager automatisch .NET Framework 4.5.2. Diese Installation kann den Server in den Status „Ausstehender Neustart“ setzen. Wenn für .NET Framework ein Neustart aussteht, können .NET-Anwendungen möglicherweise erst nach dem Neustart des Servers und dem Abschluss der Installation ausgeführt werden.  

Weitere Informationen zu .NET Framework-Versionen finden Sie in den folgenden Artikeln:

- [.NET Framework – Versionen und Abhängigkeiten](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Häufig gestellte Fragen zu Lifecycle – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS-Konfiguration

- Allgemeine HTTP-Features:  

    - Standarddokument  

- Anwendungsentwicklung:  

    - ASP.NET 3.5 (und automatisch ausgewählte Optionen)  

    - .NET-Erweiterbarkeit 3.5  

    - ASP.NET 4.5 (und automatisch ausgewählte Optionen)  

    - .NET-Erweiterbarkeit 4.5  

- IIS 6-Verwaltungskompatibilität:  

    - IIS 6-Metabasiskompatibilität  

### <a name="computer-memory"></a>Arbeitsspeicher

- Auf dem Computer, der diese Standortsystemrolle hostet, müssen mindestens 5 % des verfügbaren Speicher frei sein, um die Verarbeitung von Anforderungen durch die Standortsystemrolle zu ermöglichen.  

- Wenn diese Standortsystemrolle zusammen mit einer anderen Standortsystemrolle installiert wird, für die dieselbe Anforderung gilt, wird die Speicheranforderung für den Computer nicht erhöht, die Mindestanforderung von 5 % besteht jedoch weiter.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Wenn Sie einen neuen Standort installieren, installiert Configuration Manager automatisch SQL Server Native Client als weitervertreibbare Komponente. Nach der Installation des Standorts führt Configuration Manager kein Upgrade für den SQL Server Native Client durch. Stellen Sie sicher, dass diese Komponente auf dem neuesten Stand ist. Weitere Informationen finden Sie unter [Voraussetzungsprüfungen – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="enrollment-proxy-point"></a><a name="bkmk_2012EnrollProxpreq"></a> Anmeldungsproxypunkt  

### <a name="windows-server-roles-and-features"></a>Windows Server-Rollen und -Features

- .NET Framework 3.5

### <a name="net-framework"></a>.NET Framework

Aktivieren Sie das Windows-Feature für .NET Framework 3.5.

Installieren Sie außerdem eine unterstützte Version von .NET Framework Version 4.5 oder höher. Ab Version 1906 unterstützt Configuration Manager .NET Framework 4.8.

> [!Note]
> Bei der Installation dieser Standortsystemrolle installiert Configuration Manager automatisch .NET Framework 4.5.2. Diese Installation kann den Server in den Status „Ausstehender Neustart“ setzen. Wenn für .NET Framework ein Neustart aussteht, können .NET-Anwendungen möglicherweise erst nach dem Neustart des Servers und dem Abschluss der Installation ausgeführt werden.  

Weitere Informationen zu .NET Framework-Versionen finden Sie in den folgenden Artikeln:

- [.NET Framework – Versionen und Abhängigkeiten](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Häufig gestellte Fragen zu Lifecycle – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS-Konfiguration

- Allgemeine HTTP-Features:  

    - Standarddokument  

    - Statischer Inhalt  

- Anwendungsentwicklung:  

    - ASP.NET 3.5 (und automatisch ausgewählte Optionen)  

    - ASP.NET 4.5 (und automatisch ausgewählte Optionen)  

    - .NET-Erweiterbarkeit 3.5  

    - .NET-Erweiterbarkeit 4.5  

- Sicherheit:  

    - Windows-Authentifizierung  

- IIS 6-Verwaltungskompatibilität:  

    - IIS 6-Metabasiskompatibilität  

### <a name="computer-memory"></a>Arbeitsspeicher

- Auf dem Computer, der diese Standortsystemrolle hostet, müssen mindestens 5 % des verfügbaren Speicher frei sein, um die Verarbeitung von Anforderungen durch die Standortsystemrolle zu ermöglichen.  

- Wenn diese Standortsystemrolle zusammen mit einer anderen Standortsystemrolle installiert wird, für die dieselbe Anforderung gilt, wird die Speicheranforderung für den Computer nicht erhöht, die Mindestanforderung von 5 % besteht jedoch weiter.  


## <a name="fallback-status-point"></a><a name="bkmk_2012FSPpreq"></a> Fallbackstatuspunkt

### <a name="windows-server-roles-and-features"></a>Windows Server-Rollen und -Features

- BITS-Servererweiterungen (und automatisch ausgewählte Optionen) oder intelligenter Hintergrundübertragungsdienst (Background Intelligent Transfer Service, BITS) (und automatisch ausgewählte Optionen)

#### <a name="iis-configuration"></a>IIS-Konfiguration

Die IIS-Standardkonfiguration mit den folgenden Ergänzungen ist erforderlich:  

- IIS 6-Verwaltungskompatibilität:  

    - IIS 6-Metabasiskompatibilität  


## <a name="management-point"></a><a name="bkmk_2012MPpreq"></a> Verwaltungspunkt  

### <a name="windows-server-roles-and-features"></a>Windows Server-Rollen und -Features

- BITS-Servererweiterungen (und automatisch ausgewählte Optionen) oder intelligenter Hintergrundübertragungsdienst (Background Intelligent Transfer Service, BITS) (und automatisch ausgewählte Optionen)  

### <a name="net-framework"></a>.NET Framework

Installieren Sie eine unterstützte Version von .NET Framework, Version 4.5 oder höher. Ab Version 1906 unterstützt Configuration Manager .NET Framework 4.8.

Weitere Informationen zu .NET Framework-Versionen finden Sie in den folgenden Artikeln:

- [.NET Framework – Versionen und Abhängigkeiten](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Häufig gestellte Fragen zu Lifecycle – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS-Konfiguration

- Anwendungsentwicklung:  

    - ISAPI-Erweiterungen  

- Sicherheit:  

    - Windows-Authentifizierung  

- IIS 6-Verwaltungskompatibilität:  

    - IIS 6-Metabasiskompatibilität  

    - IIS 6-WMI-Kompatibilität  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Wenn Sie einen neuen Standort installieren, installiert Configuration Manager automatisch SQL Server Native Client als weitervertreibbare Komponente. Nach der Installation des Standorts führt Configuration Manager kein Upgrade für den SQL Server Native Client durch. Stellen Sie sicher, dass diese Komponente auf dem neuesten Stand ist. Weitere Informationen finden Sie unter [Voraussetzungsprüfungen – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="reporting-services-point"></a><a name="bkmk_2012RSpoint"></a> Reporting Services-Punkt  

### <a name="net-framework"></a>.NET Framework

Installieren Sie eine unterstützte Version von .NET Framework, Version 4.5 oder höher. Ab Version 1906 unterstützt Configuration Manager .NET Framework 4.8.

Weitere Informationen zu .NET Framework-Versionen finden Sie in den folgenden Artikeln:

- [.NET Framework – Versionen und Abhängigkeiten](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Häufig gestellte Fragen zu Lifecycle – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="sql-server-reporting-services"></a>SQL Server Reporting Services  

- Installieren und konfigurieren Sie zur Unterstützung von SQL Server Reporting Services vor dem Installieren des Berichterstattungspunkts mindestens eine SQL Server-Instanz.  

- Sie können für SQL Server Reporting Services die gleiche Instanz wie für die Standortdatenbank verwenden.  

- Darüber hinaus kann die verwendete Instanz für andere System Center-Produkte freigegeben werden, solange die anderen System Center-Produkte keiner Einschränkung für die Freigabe von SQL Server-Instanzen unterliegen.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Wenn Sie einen neuen Standort installieren, installiert Configuration Manager automatisch SQL Server Native Client als weitervertreibbare Komponente. Nach der Installation des Standorts führt Configuration Manager kein Upgrade für den SQL Server Native Client durch. Stellen Sie sicher, dass diese Komponente auf dem neuesten Stand ist. Weitere Informationen finden Sie unter [Voraussetzungsprüfungen – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="service-connection-point"></a><a name="bkmk_SCPpreq"></a> Dienstverbindungspunkt  

### <a name="net-framework"></a>.NET Framework

Aktivieren Sie das Windows-Feature für .NET Framework 3.5.

Installieren Sie außerdem eine unterstützte Version von .NET Framework Version 4.5 oder höher. Ab Version 1906 unterstützt Configuration Manager .NET Framework 4.8.

> [!Note]
> Bei der Installation dieser Standortsystemrolle installiert Configuration Manager automatisch .NET Framework 4.5.2. Diese Installation kann den Server in den Status „Ausstehender Neustart“ setzen. Wenn für .NET Framework ein Neustart aussteht, können .NET-Anwendungen möglicherweise erst nach dem Neustart des Servers und dem Abschluss der Installation ausgeführt werden.  

Weitere Informationen zu .NET Framework-Versionen finden Sie in den folgenden Artikeln:

- [.NET Framework – Versionen und Abhängigkeiten](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Häufig gestellte Fragen zu Lifecycle – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="visual-c-redistributable"></a>Visual C++ Redistributable

- Configuration Manager installiert Microsoft Visual C++ 2013 Redistributable Package auf jedem Computer, auf dem ein Verteilungspunkt gehostet wird.  

- Die Standortsystemrolle erfordert die x64-Version.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Wenn Sie einen neuen Standort installieren, installiert Configuration Manager automatisch SQL Server Native Client als weitervertreibbare Komponente. Nach der Installation des Standorts führt Configuration Manager kein Upgrade für den SQL Server Native Client durch. Stellen Sie sicher, dass diese Komponente auf dem neuesten Stand ist. Weitere Informationen finden Sie unter [Voraussetzungsprüfungen – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="software-update-point"></a><a name="bkmk_2012SUPpreq"></a> Softwareupdatepunkt  

### <a name="windows-server-roles-and-features"></a>Windows Server-Rollen und -Features

- .NET Framework 3.5

Die IIS-Standardkonfiguration ist erforderlich.

### <a name="net-framework"></a>.NET Framework

Aktivieren Sie das Windows-Feature für .NET Framework 3.5.

Installieren Sie außerdem eine unterstützte Version von .NET Framework Version 4.5 oder höher. Ab Version 1906 unterstützt Configuration Manager .NET Framework 4.8.

Weitere Informationen zu .NET Framework-Versionen finden Sie in den folgenden Artikeln:

- [.NET Framework – Versionen und Abhängigkeiten](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Häufig gestellte Fragen zu Lifecycle – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="windows-server-update-services"></a>Windows Server Update Services  

- Installieren Sie die Windows Server-Rolle „Windows Server Update Services“ auf einem Computer, bevor Sie einen Softwareupdatepunkt installieren.  

- Weitere Informationen finden Sie unter [Planen von Softwareupdates](../../../sum/plan-design/plan-for-software-updates.md).  

> [!NOTE]  
> Wenn Sie einen Softwareupdatepunkt auf einem Server verwenden, der von dem des Standortservers abweicht, müssen Sie auf dem Standortserver die WSUS-Administrationskonsole installieren.

### <a name="sql-server-native-client"></a>SQL Server Native Client

Wenn Sie einen neuen Standort installieren, installiert Configuration Manager automatisch SQL Server Native Client als weitervertreibbare Komponente. Nach der Installation des Standorts führt Configuration Manager kein Upgrade für den SQL Server Native Client durch. Stellen Sie sicher, dass diese Komponente auf dem neuesten Stand ist. Weitere Informationen finden Sie unter [Voraussetzungsprüfungen – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="state-migration-point"></a><a name="bkmk_2012SMPpreq"></a> Zustandsmigrationspunkt

<!--SCCMDocs issue 645-->
### <a name="windows-server-roles-and-features"></a>Windows Server-Rollen und -Features

- .NET Framework 3.5

    - HTTP-Aktivierung (und automatisch ausgewählte Optionen)  

    - ASP.NET 4.5  

### <a name="net-framework"></a>.NET Framework

Aktivieren Sie das Windows-Feature für .NET Framework 3.5.

Installieren Sie außerdem eine unterstützte Version von .NET Framework Version 4.5 oder höher. Ab Version 1906 unterstützt Configuration Manager .NET Framework 4.8.

> [!Note]
> Bei der Installation dieser Standortsystemrolle installiert Configuration Manager automatisch .NET Framework 4.5.2. Diese Installation kann den Server in den Status „Ausstehender Neustart“ setzen. Wenn für .NET Framework ein Neustart aussteht, können .NET-Anwendungen möglicherweise erst nach dem Neustart des Servers und dem Abschluss der Installation ausgeführt werden.  

Weitere Informationen zu .NET Framework-Versionen finden Sie in den folgenden Artikeln:

- [.NET Framework – Versionen und Abhängigkeiten](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Häufig gestellte Fragen zu Lifecycle – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS-Konfiguration

- Allgemeine HTTP-Features:  

    - Standarddokument  

- Anwendungsentwicklung:  

    - ASP.NET 3.5 (und automatisch ausgewählte Optionen)  

    - .NET-Erweiterbarkeit 3.5  

    - ASP.NET 4.5 (und automatisch ausgewählte Optionen)  

    - .NET-Erweiterbarkeit 4.5  

- IIS 6-Verwaltungskompatibilität:  

    - IIS 6-Metabasiskompatibilität  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Wenn Sie einen neuen Standort installieren, installiert Configuration Manager automatisch SQL Server Native Client als weitervertreibbare Komponente. Nach der Installation des Standorts führt Configuration Manager kein Upgrade für den SQL Server Native Client durch. Stellen Sie sicher, dass diese Komponente auf dem neuesten Stand ist. Weitere Informationen finden Sie unter [Voraussetzungsprüfungen – SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).