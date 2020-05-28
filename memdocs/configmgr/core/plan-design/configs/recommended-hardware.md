---
title: Empfohlene Hardware
titleSuffix: Configuration Manager
description: Hier finden Sie Informationen über empfohlene Hardware, mit deren Hilfe Sie Ihre Configuration Manager-Umgebung über eine einfache Bereitstellung hinaus skalieren können.
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5267f0af-34d3-47a0-9ab8-986c41276e6c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 36b90627f25c5cf19b867a78e141b69266478c58
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428785"
---
# <a name="recommended-hardware-for-configuration-manager"></a>Recommended hardware for Configuration Manager (Empfohlene Hardware für Configuration Manager)

*Gilt für: Configuration Manager (Current Branch)*

Die folgenden Empfehlungen sind Leitlinien zur Unterstützung der Skalierung Ihrer Configuration Manager-Umgebung, um mehr als eine sehr grundlegende Bereitstellung von Standorten, Standortsystemen und Clients zu unterstützen. Sie sollen nicht jede denkbare Standort- und Hierarchiekonfiguration abdecken.  

Die folgenden Abschnitte sollen Ihnen helfen, Ihre Hardware zu planen. Stellen Sie sicher, dass Ihre Hardware auf die Verarbeitungslasten von Clients und Standorten ausgelegt ist, die die verfügbaren Configuration Manager-Features verwenden.

Weitere Informationen finden Sie im [Configuration Manager Perf and Scale Guidance Whitepaper](https://gallery.technet.microsoft.com/Configuration-Manager-ba55428e) (Whitepaper zur Leistung und Skalierung von Configuration Manager).

## <a name="site-systems"></a><a name="bkmk_ScaleSieSystems"></a> Standortsysteme

In diesem Abschnitt werden die empfohlenen Hardwarekonfigurationen für Configuration Manager-Standortsysteme aufgeführt. Anhand dieser Empfehlungen können Sie die maximale Anzahl von Clients und die meisten oder alle Configuration Manager-Features verwenden. Wenn Ihre Umgebung weniger als die maximale Anzahl von Clients unterstützt und dort nicht alle verfügbaren Features verwendet werden, werden unter Umständen weniger Ressourcen benötigt. Im Allgemeinen beschränken die folgenden Hauptfaktoren die Gesamtleistung des Systems:

1. E/A-Festplattenleistung

2. Verfügbarer Arbeitsspeicher

3. CPU

Verwenden Sie zur Leistungsoptimierung RAID 10-Konfigurationen für alle Datenlaufwerke und 1 GBit/s-Ethernet-Netzwerkverbindungen.

### <a name="site-servers"></a><a name="bkmk_ScaleSiteServer"></a> Standortserver

|Standortkonfiguration|CPU (Kerne)|Arbeitsspeicher (GB)|Speicherbelegung für SQL Server (%)|  
|-------------------------------|---------------|---------------|----------------------------------------|  
|Eigenständiger primärer Standortserver mit einer Datenbankstandortrolle auf dem gleichen Server<sup>[Hinweis 1](#bkmk_note1)</sup>|16|96|80|  
|Eigenständiger primärer Standortserver mit einer Remotestandortdatenbank|8|16|-|  
|Remotedatenbankserver für einen eigenständigen primären Standort|16|72|90|  
|Standortserver der zentralen Verwaltung mit einer Datenbankstandortrolle auf dem gleichen Server<sup>[Hinweis 1](#bkmk_note1)</sup>|20|128|80|  
|Standortserver der zentralen Verwaltung mit einer Remotestandortdatenbank|8|16|-|  
|Remotedatenbankserver für einen Standort der zentralen Verwaltung|16|96|90|  
|Untergeordneter primärer Standort mit einer Datenbankstandortrolle auf dem gleichen Server|16|96|80|  
|Untergeordneter primärer Standortserver mit einer Remotestandortdatenbank|8|16|-|  
|Remotedatenbankserver für einen untergeordneten primären Standort|16|72|90|  
|Sekundärer Standortserver|8|16|-|  

#### <a name="note-1-collocated-sql"></a><a name="bkmk_note1"></a> Hinweis 1: Koinstallation von SQL Server

Wenn der Standortserver und SQL Server auf demselben Computer installiert sind, unterstützt die Bereitstellung eine maximale [Größe und Anzahl](size-and-scale-numbers.md) von Standorten und Clients. Diese Konfiguration kann jedoch [hoch verfügbare Optionen](../../servers/deploy/configure/high-availability-options.md) wie die Verwendung eines SQL Server-Clusters einschränken. Wenn Ihre Umgebung größer ist, sollten Sie aufgrund der höheren E/A-Anforderungen (zwecks Unterstützung beider Rollen auf demselben Computer) in Betracht ziehen, einen Remoteserver unter SQL Server zu verwenden.

### <a name="remote-site-system-servers"></a><a name="bkmk_RemoteSiteSystem"></a> Remote-Standortsystemserver

Der folgende Leitfaden gilt für Computer, die eine einzelne Standortsystemrolle innehaben. Planen Sie Anpassungen ein, wenn Sie mehrere Standortsystemrollen auf demselben Computer installieren.

|Standortsystemrolle|CPU (Kerne)|Arbeitsspeicher (GB)|Speicherplatz (GB)|  
|----------------------|---------------|---------------|--------------------|  
|Verwaltungspunkt|4|8|50|  
|Verteilungspunkt|2|8|Je nach Anforderungen des Betriebssystems und zum Speichern von bereitgestelltem Inhalt erforderlich|  
|Softwareupdatepunkt <sup>[Hinweis 2](#bkmk_note2)</sup>|8|16|Je nach Anforderungen des Betriebssystems und zum Speichern von bereitgestellten Updates erforderlich|  
|Alle anderen Standortsystemrollen|4|8|50|  

#### <a name="note-2-wsus-configurations"></a><a name="bkmk_note2"></a> Hinweis 2: WSUS-Konfigurationen

Der Computer, auf dem ein Softwareupdatepunkt gehostet wird, erfordert die folgenden Konfigurationen für IIS-Anwendungspools:  

- Erhöhen Sie die **WsusPool-Warteschlangenlänge** auf **2000**.  

- Erhöhen Sie die **Begrenzung des privaten Speichers für WsusPool** auf das Vierfache, oder legen Sie den Wert auf **0** (unbegrenzt) fest.  

### <a name="disk-space-for-site-systems"></a><a name="bkmk_DiskSpace"></a> Speicherplatz für Standortsysteme

Die Zuordnung und -konfiguration von Datenträgern trägt zur Leistung von Configuration Manager bei. Da jede Configuration Manager-Umgebung anders ist, können die gewählten Werte vom folgenden Leitfaden abweichen.

Platzieren Sie jedes Objekt zur Leistungsoptimierung auf einem separaten, dedizierten RAID-Volume. Verwenden Sie zur Leistungsoptimierung für alle Datenvolumes (Configuration Manager und Datenbankdateien) RAID 10.

|Datennutzung|Mindesspeicherplatz auf dem Datenträger|25.000 Clients|50.000 Clients|100.000 Clients|150.000 Clients|700.000 Clients (Standort der zentralen Verwaltung)|  
|----------------|------------------------|--------------------|--------------------|---------------------|---------------------|-----------------------------------------------------|  
|Configuration Manager-Anwendung und Protokolldateien|25 GB|50 GB|100 GB|200 GB|300 GB|200 GB|  
|MDF-Standortdatenbankdatei|75 GB je 25.000 Clients|75 GB|150 GB|300 GB|500 GB|2 TB|  
|LDF-Standortdatenbankdatei|25 GB je 25.000 Clients|25 GB|50 GB|100 GB|150 GB|100 GB|  
|Temporäre Datenbankdateien (MDF und LDF)|Nach Bedarf|Nach Bedarf|Nach Bedarf|Nach Bedarf|Nach Bedarf|Nach Bedarf|  

Weitere Informationen zum Windows-Systemdatenträger finden Sie im Größenleitfaden zur installierten Betriebssystemversion.

Bei Inhalten in Verteilungspunkten hängt die Größe von Ihren Bereitstellungen ab. Der für die Inhaltsbibliothek auf dem Standortserver oder für die Verteilungspunkte erforderliche Speicherplatz wird in diesem Leitfaden nicht angegeben. Weitere Informationen finden Sie unter [Die Inhaltsbibliothek](../../../core/plan-design/hierarchy/the-content-library.md).

Wenn Sie die Speicherplatzanforderungen planen, sollten Sie zusätzlich die folgenden Leitlinien berücksichtigen:

- Für jeden Client sind ca. 5–10 MB Speicherplatz in der Datenbank erforderlich. Diese Zahl hängt vom Typ der Hierarchie, von der Konfiguration und von der Anzahl der Clients ab. Die Größe fällt in größeren Umgebungen im Allgemeinen geringer aus. Kleinere Standorte haben eine höhere Datenbanknutzung pro Client.<!-- SCCMDocs#1048 -->

- Rechnen Sie für die temporäre Datenbank eines primären Standorts mit einer Gesamtgröße, die 25–30 % der MDF-Datei der Standortdatenbank beträgt. Die tatsächliche Größe kann kleiner oder größer ausfallen. Dies ist von der Leistung des Standortservers und der Datenmenge abhängig, die innerhalb von kurzen und langen Zeiträumen eingehen.

  > [!NOTE]
  > Wenn Sie über 50.000 oder mehr Clients an einem Standort verfügen, sollten Sie vier oder mehr MDF-Dateien für temporäre Datenbanken einplanen.

- Die Größe einer temporären Datenbank für einen Standort der zentralen Verwaltung ist in der Regel deutlich kleiner als die für einen primären Standort.

- Wenn Sie für die Datenbank des sekundären Standorts SQL Server Express verwenden, ist die Datenbankgröße auf 10 GB beschränkt.

## <a name="clients"></a><a name="bkmk_ScaleClient"></a> Clients

In diesem Abschnitt werden die empfohlenen Hardwarekonfigurationen für Computer bestimmt, die durch die Verwendung von Configuration Manager-Clientsoftware verwaltet werden.

### <a name="client-for-windows-computers"></a>Client für Windows-Computer

Die folgenden Mindestanforderungen gelten für Windows-Computer, die mit Configuration Manager verwaltet werden. Dazu zählen auch Embedded-Betriebssysteme:

- **Prozessor und Arbeitsspeicher:** Weitere Informationen entnehmen Sie den Prozessor- und RAM-Anforderungen des Betriebssystems.

- **Speicherplatz:** 500 MB verfügbarer Speicherplatz, 5 GB für den Configuration Manager-Clientcache empfohlen. Wenn Sie den Configuration Manager-Client über benutzerdefinierte Einstellungen installieren, ist weniger Speicherplatz erforderlich:

  - Verwenden Sie die „client.msi“-Eigenschaft **SMSCACHESIZE**, um eine Cachegröße festzulegen, die kleiner als die Standardgröße von 5120 MB ist. Die Mindestgröße beträgt 1 MB. Im folgenden Beispiel wird ein Cache mit 2 MB erstellt: `CCMSetup.exe SMSCACHESIZE=2`

    Weitere Informationen finden Sie unter [Informationen zu Clientinstallationseigenschaften](../../../core/clients/deploy/about-client-installation-properties.md).

    > [!TIP]
    > Die Clientinstallation mit minimalem Speicherplatz ist hilfreich für Windows Embedded-Geräte, die in der Regel über kleinere Datenträgergrößen als Windows-Standardcomputer verfügen.

Die folgenden zusätzlichen Mindestanforderungen an die Hardware gelten für optionale Funktionen in Configuration Manager:

- **Bereitstellung des Betriebssystems:** mindestens 384 MB RAM

- **Softwarecenter:** mindestens ein 500-MHz-Prozessor

- **Remotesteuerung:** Für eine optimale Leistung mindestens ein Pentium 4 mit Hyperthreading und 3 GHz (einzelner Kern) oder einer vergleichbaren CPU und mindestens 1 GB RAM

### <a name="client-for-linux-and-unix"></a>Client für Linux und UNIX

Die folgenden Mindestanforderungen gelten für Linux- und UNIX-Server, die mit Configuration Manager verwaltet werden.

|Anforderungen|Details|  
|-----------------|-------------|  
|Prozessor und Arbeitsspeicher|Weitere Informationen entnehmen Sie den Prozessor- und RAM-Anforderungen des Computerbetriebssystems.|  
|Speicherplatz|500 MB verfügbarer Speicherplatz, 5 GB für den Configuration Manager-Clientcache empfohlen|  
|Netzwerkverbindungen|Configuration Manager-Clientcomputer müssen über eine Netzwerkverbindung mit Configuration Manager-Standortsystemen verfügen, um die Verwaltung zu ermöglichen.|  

## <a name="configuration-manager-console"></a><a name="bkmk_ScaleConsole"></a> Configuration Manager-Konsole

Die folgenden minimalen Hardwareanforderungen gelten für alle Computer, auf denen die Configuration Manager-Konsole ausgeführt wird:

- Intel i3 oder vergleichbare CPU  

- 2 GB RAM  

- 2 GB Speicherplatz  

|DPI-Einstellung|Mindestauflösung|  
|-----------------|------------------------|  
|96 / 100 %|1024 x 768|  
|120 /125 %|1280 x 960|  
|144 / 150 %|1600 x 1200|  
|196 / 200 %|2500 x 1600|  

## <a name="lab-deployments"></a><a name="bkmk_ScaleLab"></a> Laborbereitstellungen

Verwenden Sie die folgenden Hardwaremindestempfehlungen für Labor- und Testbereitstellungen von Configuration Manager. Diese Empfehlungen gelten für alle Standorttypen mit bis zu 100 Clients:  

|Role-Eigenschaft|CPU (Kerne)|Arbeitsspeicher (GB)|Speicherplatz (GB)|  
|----------|---------------|-------------------|-----------------------|  
|Standort- und Datenbankserver|2 - 4|8 - 12|100|  
|Standortsystemserver|1 - 4|2 - 4|50|  
|Client|1 - 2|1 - 3|30|  
