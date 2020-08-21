---
title: Unterstützte Clients und Geräte
titleSuffix: Configuration Manager
description: Erfahren Sie, welche Betriebssystemversionen Configuration Manager für Clients und Geräte unterstützt.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 87f4e041-67df-4c61-aa98-7444faffe565
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e573a2887bd527daac9a05fec2e83ef39fbfc4e1
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700315"
---
# <a name="supported-os-versions-for-clients-and-devices-for-configuration-manager"></a>Unterstützte Betriebssystemversionen für Clients und Geräte für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Configuration Manager unterstützt die Installation von Clientsoftware auf Windows- und Mac-Computern.  

## <a name="general-requirements-and-limitations"></a>Allgemeine Anforderungen und Einschränkungen

Machen Sie sich mit den folgenden Anforderungen und Einschränkungen für alle Clients vertraut:

- Die Änderung der Einstellungen für Starttyp und **Anmelden als** für beliebige Configuration Manager-Dienste wird nicht unterstützt. Wenn Sie diese Änderung trotzdem vornehmen, werden wichtige Dienste möglicherweise nicht ordnungsgemäß ausgeführt.

## <a name="windows-computers"></a>Windows-Computer  

Verwenden Sie den Client, der bei Configuration Manager enthalten ist, um die folgenden Windows-Betriebssystemversionen zu verwalten. Weitere Informationen finden Sie unter [Gewusst wie: Bereitstellen von Clients für Windows-Computer in Configuration Manager](../../clients/deploy/deploy-clients-to-windows-computers.md).  

### <a name="supported-client-os-versions"></a>Unterstützte Client-Betriebssystemversionen

- **Windows 10**  

    Weitere Informationen unter [Unterstützung für Windows 10](support-for-windows-10.md)  

- **Windows 8.1** (x86, x64): Professional, Enterprise

#### <a name="windows-virtual-desktop"></a>Windows Virtual Desktop

<!--3556025-->
[Windows Virtual Desktop](/azure/virtual-desktop/) ist ein Desktop- und App-Virtualisierungsdienst, der auf Microsoft Azure ausgeführt wird. Verwenden Sie ab Version 1906 Configuration Manager zum Verwalten dieser unter Windows ausgeführten virtuellen Geräte in Azure.

Ähnlich wie bei einem Terminalserver ermöglichen einige diese virtuellen Geräte mehrere gleichzeitige aktive Benutzersitzungen. Um bei der Clientleistung zu helfen, deaktiviert Configuration Manager jetzt Benutzerrichtlinien auf jedem Gerät, dass mehrere Benutzersitzungen zulässt. Auch wenn Sie Benutzerrichtlinien aktivieren, deaktiviert der Client sie standardmäßig auf diesen Geräten, zu denen Windows 10 Enterprise mit mehreren Benutzersitzungen und Terminalserver zählen.

Der Client deaktiviert eine Benutzerrichtlinie nur, wenn er diesen Gerätetyp während einer neuen Installation erkennt. Für einen vorhandenen Client dieses Typs, den Sie auf diese Version aktualisieren, bleibt das vorherige Verhalten bestehen. Bei einem bestehenden Gerät wird die Benutzerrichtlinieneinstellung auch dann konfiguriert, wenn erkannt wird, dass das Gerät mehrere Benutzersitzungen ermöglicht.

Wenn Sie in diesem Szenario eine Benutzerrichtlinie benötigen und mögliche Auswirkungen auf die Leistung akzeptieren, verwenden Sie eine der folgenden Methoden, um die Benutzerrichtlinie zu aktivieren:

- Verwenden Sie [Clienteinstellungen](../../clients/deploy/configure-client-settings.md) in Version 1910 und höher. Konfigurieren Sie in der Gruppe **Clientrichtlinie** die folgende Einstellung: **Aktivieren der Benutzerrichtlinie für mehrere Benutzersitzungen**.<!-- 4737447 -->

- Verwenden Sie in Version 1906 die Configuration Manager-SDK mit der [WMI-Klasse „SMS_PolicyAgentConfig“ des Servers](../../../develop/reference/core/clients/config/sms_policyagentconfig-server-wmi-class.md). Legen Sie für die neue `PolicyEnableUserPolicyOnTS`-Eigenschaft `true` fest.

> [!Note]  
> Sie können die Co-Verwaltung nicht mit einem Client verwenden, auf dem Windows 10 Enterprise mit mehreren Benutzersitzungen ausgeführt wird. <!-- SCCMDocs-pr#3950 -->

Ab Version 2006 ist die Plattform **Windows 10 Enterprise Multi-Session** in der Liste unterstützter Betriebssystemversionen für Objekte mit Anforderungsregeln oder Anwendungslisten verfügbar.<!--6527576-->

> [!NOTE]
> Wenn Sie zuvor die **Windows 10**-Plattform auf der obersten Ebene ausgewählt haben, wurden dadurch automatisch alle untergeordneten Plattformen ausgewählt. Diese neue Plattform wird nicht automatisch ausgewählt. Wenn Sie **Alle Windows 10 Enterprise Multi-Session** hinzufügen möchten, wählen Sie die Plattform manuell in der Liste aus.

Weitere Informationen finden Sie in den folgenden Artikeln:

- [Unterstützung für Virtualisierungsumgebungen](support-for-virtualization-environments.md)
- [Verwalten von Configuration Manager-Clients in einer virtuellen Desktopinfrastruktur (Virtual Desktop Infrastructure, VDI)](../../clients/deploy/plan/considerations-for-managing-clients-in-a-vdi.md)

### <a name="supported-server-os-versions"></a>Unterstützte Server-Betriebssystemversionen

- **Windows Server 2019:** Standard, Datacenter <sup>[Hinweis 1](#bkmk_note1)</sup>  
    (Ab Configuration Manager, Version 1806)

- **Windows Server 2016:** Standard, Datacenter <sup>[Hinweis 1](#bkmk_note1)</sup>  

- **Windows Storage Server 2016:** Arbeitsgruppe, Standard  

- **Windows Server 2012 R2** (x64): Standard, Datacenter <sup>[Hinweis 1](#bkmk_note1)</sup>

- **Windows Storage Server 2012 R2** (x64)

- **Windows Server 2012** (x64): Standard, Datacenter <sup>[Hinweis 1](#bkmk_note1)</sup>

- **Windows Storage Server 2012** (x64)

#### <a name="server-core"></a>Server Core

Die folgenden Versionen beziehen sich auf die Server Core-Installation des Betriebssystems. <sup>[Hinweis 3](#bkmk_note3)</sup>  

Halbjährliche Kanalversionen von Windows Server sind Server Core-Installationen, z. B. Windows Server, Version 1809. Als Configuration Manager-Client werden sie genauso unterstützt wie die zugehörige halbjährliche Kanalversion von Windows 10. Weitere Informationen finden Sie unter [Unterstützung für Windows 10](support-for-windows-10.md).

- **Windows Server 2019** (x64) <sup>[Hinweis 2](#bkmk_note2)</sup>

- **Windows Server 2016** (x64) <sup>[Hinweis 2](#bkmk_note2)</sup>

- **Windows Server 2012 R2** (x64) <sup>[Hinweis 2](#bkmk_note2)</sup>

- **Windows Server 2012** (x64) <sup>[Hinweis 2](#bkmk_note2)</sup>

#### <a name="note-1"></a><a name="bkmk_note1"></a> Hinweis 1

Configuration Manager testet und unterstützt Windows Server Datacenter-Editionen, ist jedoch nicht offiziell für Windows Server zertifiziert. Es wird keine Configuration Manager-Hotfixunterstützung für Probleme bereitgestellt, die ausschließlich Windows Server Datacenter betreffen. Weitere Informationen zum Windows Server-Zertifizierungsprogramm finden Sie in [Windows Server Catalog](https://www.windowsservercatalog.com/).

#### <a name="note-2"></a><a name="bkmk_note2"></a> Hinweis 2

Um die [Clientpushinstallation](../../clients/deploy/plan/client-installation-methods.md#client-push-installation) zu unterstützen, fügen Sie den Dateiserverdienst der Serverrolle „Datei- und Speicherdienste“ hinzu. Weitere Informationen zum Installieren von Windows-Features auf einer Server Core-Instanz finden Sie unter [Installieren von Rollen, Rollendiensten und Features mithilfe von Windows PowerShell-Cmdlets](/windows-server/administration/server-manager/install-or-uninstall-roles-role-services-or-features#install-roles-role-services-and-features-by-using-windows-powershell-cmdlets).  

#### <a name="note-3"></a><a name="bkmk_note3"></a> Hinweis 3

Die neue Softwarecenter-App wird nicht von jeder Windows Server Core-Version unterstützt.<!--SCCMDocs issue 683-->

## <a name="windows-embedded-computers"></a>Windows Embedded-Computer  

Verwalten Sie Windows Embedded-Geräte durch die Installation des Configuration Manager-Clients auf dem Gerät. Weitere Informationen finden Sie unter [Planen der Clientbereitstellung auf Windows Embedded-Geräten](../../clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

### <a name="requirements-and-limitations"></a>Anforderungen und Einschränkungen

- Alle Clientfeatures werden auf Windows Embedded-Systemen ohne aktivierte Schreibfilter unterstützt.  

- Clients, die einen der folgenden Filter verwenden, werden für alle Features (ausgenommen Energieverwaltung) unterstützt:  

  - Erweiterte Schreibfilter (Enhanced Write Filters, EWF)

  - RAM-dateibasierte Schreibfilter (File Based Write Filters, FBWF)

  - Vereinheitlichte Schreibfilter (Unified Write Filters, UWF)  

- Der Anwendungskatalog wird nicht für Windows Embedded-Geräte unterstützt.  

### <a name="supported-os-versions"></a>Unterstützte Betriebssystemversionen  

- **Windows 10 Enterprise** (x86, x64)  

- **Windows 10 IoT Enterprise** (x86, x64)  
    Diese Version unterstützt LTSC (Long-Term Servicing Channel). Weitere Informationen finden Sie unter [Übersicht über Windows 10 IoT Enterprise](/windows/iot-core/windows-iot-enterprise).<!--SCCMDocs issue 560-->  

- **Windows Embedded 8.1 Industry** (x86, x64)

- **Windows Embedded 8 Standard** (x86, x64)

- **Windows Thin PC** (x86, x64)

- **Windows Embedded POSReady 7** (x86, x64)

- **Windows Embedded Standard 7 mit SP1** (x86, x64)

## <a name="windows-ce-computers"></a>Windows CE-Computer

Verwalten Sie Windows CE-Geräte mit dem Configuration Manager-Legacyclient für Mobilgeräte, der in Configuration Manager enthalten ist.  

### <a name="requirements-and-limitations"></a>Anforderungen und Einschränkungen

- Zur Installation des Clients für mobile Geräte sind 0,78 MB Speicherplatz erforderlich. Die Anmeldung auf dem mobilen Gerät kann bis zu 256 KB zusätzlichen Speicherplatz erfordern.

- Die für diese mobilen Geräte verfügbaren Funktionen sind von Plattform und Clienttyp abhängig. Informationen dazu, welche Verwaltungsfunktionen unterstützt werden, finden Sie unter [Wählen einer Geräteverwaltungslösung für System Center Configuration Manager](../choose-a-device-management-solution.md).  

### <a name="supported-os-versions"></a>Unterstützte Betriebssystemversionen

- Windows CE 7.0 (ARM- und x86-Prozessoren)  

    > [!IMPORTANT]
    > In Version 2006 von Configuration Manager wird der Support für Windows CE 7.0 als Client eingestellt. Die Einstellung wurde mit [Version 1906](../changes/whats-new-in-version-1906.md#bkmk_deprecated) angekündigt.

#### <a name="supported-languages-include"></a>Unterstützte Sprachen

- Chinesisch (vereinfacht und traditionell)

- Englisch (USA)

- Französisch (Frankreich)

- Deutsch

- Italienisch

- Japanisch  

- Koreanisch  

- Portugiesisch (Brasilien)  

- Russisch  

- Spanisch (Spanien)  

## <a name="extended-security-updates-and-configuration-manager"></a><a name="bkmk_ESU"></a> Erweiterte Sicherheitsupdates und Configuration Manager

Das Programm [Extended Security Updates (ESU)](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates) ist ein letzter Ausweg für Kunden, die bestimmte ältere Microsoft-Produkte über das Supportende hinaus ausführen müssen. Beispiel: Windows 7. Es umfasst kritische und/oder wichtige Sicherheitsupdates (wie durch das [Microsoft Security Response Center](https://www.microsoft.com/msrc) definiert), die für maximal drei Jahre nach dem Ende des erweiterten Supports für das Produkt bereitgehalten werden.

Produkte, deren Supportlebenszyklus abgelaufen ist, werden nicht mehr für die Verwendung mit Configuration Manager unterstützt. Hierzu gehören alle Produkte im ESU-Programm. Sicherheitsupdates, die im Rahmen des ESU-Programms zur Verfügung gestellt werden, werden in den Windows Server Update Services (WSUS) veröffentlicht. Diese Updates werden in der Configuration Manager-Konsole angezeigt. Während Produkte, die durch das ESU-Programm abgedeckt sind, nicht mehr für die Verwendung mit Configuration Manager unterstützt werden, kann die [letzte veröffentlichte Version des aktuellen Configuration Manager-Branchs](../../servers/manage/updates.md#version-details) zum Bereitstellen und Installieren von im Rahmen des Programms veröffentlichten Windows-Sicherheitsupdates verwendet werden. Mit der neuesten veröffentlichten Version kann auch Windows 10 auf Geräten mit Windows 7 bereitgestellt werden.

Clientverwaltungsfeatures, die nicht im Zusammenhang mit der Verwaltung von Windows-Softwareupdates oder der Betriebssystembereitstellung stehen, werden unter Betriebssystemen, die durch das ESU-Programm abgedeckt werden, nicht mehr getestet, und wir garantieren nicht, dass diese weiterhin funktionsfähig sind. Es wird dringend empfohlen, so schnell wie möglich ein Upgrade oder eine Migration zu einer aktuellen Version der Betriebssysteme durchzuführen, um Unterstützung für die Clientverwaltung zu erhalten.

## <a name="mac-computers"></a>Mac-Computer  

Verwalten Sie Apple Mac-Computer mit dem Configuration Manager-Client für macOS.  

Das macOS-Clientinstallationspaket wird nicht mit den Configuration Manager-Medien geliefert. Laden Sie ihn aus dem Microsoft Download Center herunter, [Microsoft Endpoint Configuration Manager – macOS-Client (64-Bit)](https://www.microsoft.com/download/details.aspx?id=100850).  

Weitere Informationen finden Sie unter [Gewusst wie: Bereitstellen von Clients für Mac-Computer](../../clients/deploy/deploy-clients-to-macs.md).  

### <a name="requirements-and-limitations"></a>Anforderungen und Einschränkungen

- Die Installation oder Ausführung des Configuration Manager-Clients für macOS auf Computern unter einem anderen Konto als dem Stammkonto wird nicht unterstützt. Wenn Sie die Einstellungen trotzdem ändern, werden wichtige Dienste möglicherweise nicht ordnungsgemäß ausgeführt.  

### <a name="supported-versions"></a>Unterstützte Versionen

- **macOS Catalina (10.15)** (erfordert Configuration Manager-Websiteversion 1910 oder höher und Configuration Manager-Client für macOS Version 5.0.8742.1000 oder höher)

- **macOS Mojave (10.14)**

- **macOS High Sierra (10.13)**

## <a name="linux-and-unix-servers"></a>Linux- und UNIX-Server  

> [!Important]  
> In Configuration Manager, Version 1902 wird der Support für Linux und UNIX als Client eingestellt. Die Einstellung wurde mit [Version 1802](../changes/whats-new-in-version-1802.md#deprecation-announcement-for-linux-and-unix-client-support) angekündigt. Ziehen Sie deshalb Microsoft Azure Management zum Verwalten von Linux-Servern in Betracht. Azure-Lösungen verfügen über umfangreiche Linux-Unterstützung, die i.d.R. über die Funktionen von Configuration Manager hinausgeht (einschließlich der End-to-End-Patchverwaltung für Linux).

Die Clientinstallationspakete für Linux und UNIX werden nicht mit den Configuration Manager-Medien bereitgestellt. Laden Sie die **Clients für weitere Betriebssysteme** aus dem [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=47719) herunter. Zusätzlich zu den Clientinstallationspaketen umfasst der Clientdownload das Skript zur Verwaltung der Clientinstallation auf den einzelnen Computern.  

### <a name="requirements-and-limitations"></a>Anforderungen und Einschränkungen

- Informationen zum Überprüfen von Betriebssystemdateiabhängigkeiten für den Client für Linux und UNIX finden Sie unter [Voraussetzungen für die Clientbereitstellung auf Linux- und UNIX-Servern](../../clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_ClientDeployPrereqforLnU).  

- Eine Übersicht über die Verwaltungsfunktionen, die für Computer unterstützt werden, auf denen Linux oder UNIX ausgeführt wird, finden Sie unter [Gewusst wie: Bereitstellen von Clients auf UNIX- und Linux-Servern in System Center Configuration Manager](../../clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

- Für unterstützte Versionen von Linux- und UNIX-Clients schließt die aufgeführte Version alle nachfolgenden Nebenversionen ein. Die CentOS-Version 6 enthält beispielsweise CentOS 6.3. Ebenso schließt die Unterstützung für ein Betriebssystem, das Service Packs verwendet (z.B. SUSE Linux Enterprise Server 11 SP1), die Unterstützung für alle nachfolgenden Service Packs für diese Betriebssystemversion ein.  

- Informationen zu Clientinstallationspaketen und zum universellen Agent finden Sie unter [Gewusst wie: Bereitstellen von Clients auf UNIX- und Linux-Servern in System Center Configuration Manager](../../clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

### <a name="supported-versions"></a>Unterstützte Versionen

Die folgenden Versionen werden mit der angegebenen TAR-Datei unterstützt.  

#### <a name="aix"></a>AIX  

|Version|TAR-Datei|  
|-|-|  
|Version 6.1 (Power)|ccm-Aix61ppc.&lt;build\>.tar|  
|Version 7.1 (Power)|ccm-Aix71ppc.&lt;build\>.tar|  

#### <a name="centos"></a>CentOS  

|Version|TAR-Datei|  
|-|-|  
|Version 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 7 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="debian"></a>Debian  

|Version|TAR-Datei|  
|-|-|  
|Version 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 7 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 7 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 8 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 8 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="hp-ux"></a>HP-UX  

|Version|TAR-Datei|  
|-|-|  
|Version 11iv3 IA64|ccm-HpuxB.11.31i64.&lt;build\>.tar|  

#### <a name="oracle-linux"></a>Oracle Linux  

|Version|TAR-Datei|  
|-|-|  
|Version 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 7 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|Version|TAR-Datei|  
|-|-|  
|Version 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 7 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="solaris"></a>Solaris  

|Version|TAR-Datei|  
|-|-|  
|Version 10 x86|ccm-Sol10x86.&lt;build\>.tar|  
|Version 10 SPARC|ccm-Sol10sparc.&lt;build\>.tar|  
|Version 11 x86|ccm-Sol11x86.&lt;build\>.tar|  
|Version 11 SPARC|ccm-Sol11sparc.&lt;build\>.tar|  

#### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|Version|TAR-Datei|  
|-|-|  
|Version 10 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 10 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 11 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 11 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 12 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="ubuntu"></a>Ubuntu  

|Version|TAR-Datei|  
|-|-|  
|Version 10.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 10.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 12.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 12.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 14.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 14.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Version 16.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Version 16.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  


## <a name="on-premises-mdm"></a><a name="bkmk_OnpremOS"></a> Lokale Verwaltung mobiler Geräte

Configuration Manager verfügt über integrierte Funktionen zum Verwalten von lokalen mobilen Geräten ohne Installation der Clientsoftware. Weitere Informationen finden Sie unter [Lokale MDM (Mobile Device Management) in System Center Configuration Manager](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

### <a name="supported-operating-systems"></a>Unterstützte Betriebssysteme

- **Windows 10 Pro** (x86, x64)  

- **Windows 10 Pro Enterprise** (x86, x64)  

- **Windows 10 IoT Enterprise** (x86, x64)  
    Diese Version unterstützt LTSC (Long-Term Servicing Channel). Weitere Informationen finden Sie unter [Übersicht über Windows 10 IoT Enterprise](/windows/iot-core/windows-iot-enterprise).<!--SCCMDocs issue 560-->  

- **Windows 10 IoT Mobile Enterprise**  

- **Windows 10 Team für Surface Hub**  

- **Windows 10 Mobile**  

- **Windows 10 Mobile Enterprise**  

    > [!IMPORTANT]
    > In Version 2006 von Configuration Manager wird der Support für Windows 10 Mobile und Windows 10 Mobile Enterprise als Client eingestellt. Die Einstellung wurde mit [Version 1906](../changes/whats-new-in-version-1906.md#bkmk_deprecated) angekündigt.

## <a name="exchange-server-connector"></a><a name="bkmk_ExSrvConOS"></a> Exchange Server-Connector  

Configuration Manager unterstützt mit Einschränkungen die Verwaltung der Geräte, die Sie mit Ihrem Exchange-Server verbinden, ohne den Configuration Manager-Client zu installieren. Weitere Informationen finden Sie unter [Verwalten von Mobilgeräten mit System Center Configuration Manager und Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

### <a name="supported-versions-of-exchange-server"></a>Unterstützte Versionen von Exchange Server

- **Exchange Online (Office 365):** Diese Version umfasst die Business Productivity Online Standard Suite.  

- **Exchange Server 2016**  

- **Exchange Server 2013**  

- **Exchange Server 2010 SP1** oder **Exchange Server 2010 SP2**