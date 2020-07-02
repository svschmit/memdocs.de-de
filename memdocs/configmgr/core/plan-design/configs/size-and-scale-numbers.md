---
title: Anpassen und Skalieren
titleSuffix: Configuration Manager
description: Ermitteln Sie die Anzahl der Standortsystemrollen und Standorte, die für die Unterstützung von Geräten in Ihrer Umgebung notwendig sind.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c5a42100-2f60-4952-b495-918025ea6559
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5109ababd00011784618f9c989e1d2b756a322d9
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715627"
---
# <a name="size-and-scale-numbers-for-configuration-manager"></a>Size and scale numbers for Configuration Manager (Größe und Skalierung von Zahlen für Configuration Manager)

*Gilt für: Configuration Manager (Current Branch)*

Jede Bereitstellung von Configuration Manager hat eine maximal zulässige Anzahl von Standorten, Standortsystemrollen und Geräten, die unterstützt werden können. Diese Zahlen sind von Ihrer Hierarchiestruktur (welche Typen und welche Anzahl von Standorten Sie verwenden) und den Standortsystemrollen abhängig, die Sie bereitstellen. Die Informationen in diesem Artikel unterstützen Sie dabei, die Anzahl von Standortsystemrollen und Standorten zu ermitteln, die für die Unterstützung der Geräte notwendig sind, die voraussichtlich verwaltet werden sollen.

Weitere Informationen finden Sie in den folgenden Artikeln:

- [Empfohlene Hardware](recommended-hardware.md)
- [Unterstützte Betriebssysteme für Standortsystemserver](supported-operating-systems-for-site-system-servers.md)  
- [Unterstützte Betriebssysteme für Clients und Geräte](supported-operating-systems-for-clients-and-devices.md)
- [Voraussetzungen für Standorte und Standortsysteme](site-and-site-system-prerequisites.md)

Bei den hier genannten unterstützten Zahlen wird davon ausgegangen, dass die empfohlene Hardware für Configuration Manager verwendet wird. Außerdem basieren sie auf den Standardeinstellungen für alle verfügbaren Configuration Manager-Features. Wenn Sie die empfohlene Hardware nicht verwenden oder strengere benutzerdefinierte Einstellungen festgelegt haben, kann die Leistung von Standortsystemen beeinträchtigt werden. Die Standortsysteme erfüllen möglicherweise nicht den angegebenen Unterstützungsgrad. (Beispiel für strengere Clienteinstellungen: Die Hardware- oder Softwareinventur wird häufiger als die Standardeinstellung, alle sieben Tage, durchgeführt.)

## <a name="site-types"></a><a name="bkmk_SiteSystemScale"></a> Standorttypen  

### <a name="central-administration-site"></a>Standort der zentralen Verwaltung  

- Ein Standort der zentralen Verwaltung unterstützt bis zu 25 untergeordnete primäre Standorte.  

### <a name="primary-site"></a>Primärer Standort  

- Jeder primäre Standort unterstützt bis zu 250 sekundäre Standorte.  

- Die maximale Anzahl sekundärer Standorte pro primärem Standort wurde auf Basis von kontinuierlich verbundenen und stabilen WAN (Wide Area Network)-Verbindungen ermittelt. Für Standorte mit weniger als 500 Clients können Sie einen Verteilungspunkt anstatt eines sekundären Standorts erwägen.  

  Informationen zur Anzahl von Clients und Geräten, die von einem primären Standort unterstützt werden können, finden Sie unter [Anzahl der Clients für Standorte und Hierarchien](#bkmk_clientnumbers).  

### <a name="secondary-site"></a>Sekundärer Standort  

- Sekundäre Standorte unterstützen keine untergeordneten Standorte.  

## <a name="site-system-roles"></a><a name="bkmk_roles"></a> Standortsystemrolle

### <a name="application-catalog-web-service-point"></a>Anwendungskatalog-Webdienstpunkt  

> [!Important]
> Die Silverlight-Benutzeroberfläche für den Anwendungskatalog wird ab Current Branch-Version 1806 nicht unterstützt. Ab Version 1906 verwenden aktualisierte Clients automatisch den Verwaltungspunkt für Anwendungsbereitstellungen, die Benutzern zur Verfügung stehen. Zudem können Sie keine neuen Anwendungskatalogrollen installieren. Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910.  
>
> Weitere Informationen finden Sie in den folgenden Artikeln:
>
> - [Konfigurieren des Softwarecenters](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Entfernte und veraltete Features](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

- An primären Standorten können Sie mehrere Instanzen des Anwendungskatalog-Webservicepunkts installieren.  

### <a name="application-catalog-website-point"></a>Anwendungskatalog-Websitepunkt  

> [!Important]
> Die Silverlight-Benutzeroberfläche für den Anwendungskatalog wird ab Current Branch-Version 1806 nicht unterstützt. Ab Version 1906 verwenden aktualisierte Clients automatisch den Verwaltungspunkt für Anwendungsbereitstellungen, die Benutzern zur Verfügung stehen. Zudem können Sie keine neuen Anwendungskatalogrollen installieren. Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910.  
>
> Weitere Informationen finden Sie in den folgenden Artikeln:
>
> - [Konfigurieren des Softwarecenters](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Entfernte und veraltete Features](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

- An primären Standorten können Sie mehrere Instanzen des Anwendungskatalog-Websitepunkts installieren.  

### <a name="cloud-management-gateway"></a><a name="bkmk_cmg"></a> Cloud Management Gateway

- Sie können mehrere Instanzen des Cloud Management Gateways (CMG) an primären Standorten oder dem Standort der zentralen Verwaltung installieren.  

    > [!Tip]  
    > Erstellen Sie das CMG in einer Hierarchie am Standort der zentralen Verwaltung.  

  - Ein CMG unterstützt zwischen einer und 16 Instanzen virtueller Computer (VMs) im Azure-Clouddienst.  

  - Jede CMG-VM-Instanz unterstützt 6.000 gleichzeitige Clientverbindungen. Wenn das CMG unter hoher Beanspruchung steht, da die unterstützte Anzahl der Clients überschritten wurde, werden Anforderungen weiterhin verarbeitet, jedoch möglicherweise verzögert.  

Weitere Informationen finden Sie im Artikel zur [Leistung und Skalierbarkeit des CMG](../../clients/manage/cmg/plan-cloud-management-gateway.md#performance-and-scale).

### <a name="cloud-management-gateway-connection-point"></a>Verbindungspunkt für das Cloud Management Gateway

- Sie können an primären Standorten mehrere Instanzen des CMG-Verbindungspunkts installieren.  

- Ein CMG-Verbindungspunkt unterstützt ein CMG mit bis zu vier VM-Instanzen. Wenn das CMG über mehr als vier VM-Instanzen verfügt, fügen Sie einen zweiten CMG-Verbindungspunkt zum Lastenausgleich hinzu. Ein CMG mit 16 VM-Instanzen sollte mit vier CMG-Verbindungspunkten verknüpft sein.

Weitere Informationen finden Sie im Artikel zur [Leistung und Skalierbarkeit des CMG](../../clients/manage/cmg/plan-cloud-management-gateway.md#performance-and-scale).

> [!NOTE]
> Informationen zu den Hardwareanforderungen für den CMG-Verbindungspunkt finden Sie unter [Empfohlene Hardware für Remote-Standortsystemserver](recommended-hardware.md#bkmk_RemoteSiteSystem).<!-- SCCMDocs#2276 -->

### <a name="distribution-point"></a>Verteilungspunkt  

- Verteilungspunkte pro Standort:  

  - An jedem primären und sekundären Standort werden bis zu 250 Verteilungspunkte unterstützt.  

  - Jeder primäre und sekundäre Standort unterstützt bis zu 2000 zusätzliche Verteilungspunkte, die als Pullverteilungspunkte konfiguriert sind. **Beispiel:** Ein einzelner primärer Standort unterstützt 2250 Verteilungspunkte, wenn 2000 dieser Verteilungspunkte als Pullverteilungspunkte konfiguriert sind.  

  - Jeder Verteilungspunkt unterstützt Verbindungen von bis zu 4.000 Clients.  

  - Ein Pullverteilungspunkt verhält sich wie ein Client, wenn er auf Inhalte von einem Quellverteilungspunkt zugreift.  

- An jedem primären Standort werden insgesamt bis zu 5.000 Verteilungspunkte unterstützt. Darin eingeschlossen sind alle Verteilungspunkte des primären Standorts und alle Verteilungspunkte, die zu den untergeordneten sekundären Standorten des primären Standorts gehören.  

- Jeder Verteilungspunkt unterstützt eine Gesamtgröße von bis zu 10.000 Paketen und Anwendungen.  

> [!WARNING]  
> Die tatsächliche Anzahl von Clients, die von einem Verteilungspunkt unterstützt werden können, hängt von der Netzwerkgeschwindigkeit und der Hardwarekonfiguration des Servers ab.  
>
> Die Anzahl von Pullverteilungspunkten, die von einem Quellverteilungspunkt unterstützt werden, hängt entsprechend von der Netzwerkgeschwindigkeit und der Hardwarekonfiguration des Quellverteilungspunkts ab. Ein weiterer Faktor ist die bereitgestellte Menge von Inhalten. Dies liegt daran, dass alle Pullverteilungspunkte – im Gegensatz zu Clients, die Inhalte an verschiedenen Punkten während der Bereitstellung anfordern – Inhalte gleichzeitig anfordern. Pullverteilungspunkte können allen verfügbaren Inhalt anfordern und nicht nur den Inhalt, der für sie gilt. Wenn die Verarbeitungslast für einen Quellverteilungspunkt zu hoch wird, kann dies zu unerwarteten Verzögerungen bei der Verteilung von Inhalten an die Zielverteilungspunkte führen.  

### <a name="fallback-status-point"></a>Fallbackstatuspunkt  

- Von jedem Fallbackstatuspunkt können bis zu 100.000 Clients unterstützt werden.  

### <a name="management-point"></a>Verwaltungspunkt  

- Jeder primäre Standort unterstützt bis zu 15 Verwaltungspunkte.  

    > [!TIP]  
    > Installieren Sie Verwaltungspunkte nicht auf Servern, die über eine langsame Verbindung mit dem primären Standortserver oder Standortdatenbankserver verbunden sind.  

- An jedem sekundären Standort wird nur ein Verwaltungspunkt unterstützt, der auf dem sekundären Standortserver installiert sein muss.  

Informationen zur Anzahl von Clients und Geräten, die von einem Verwaltungspunkt unterstützt werden können, finden Sie in im Abschnitt [Verwaltungspunkte](#bkmk_mp) in diesem Artikel.  

> [!NOTE]
> Wenn Sie den Verwaltungspunkt für die Unterstützung von [Cloud Management Gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md) aktivieren, erfüllt er die Anforderungen internetbasierter Clients wie gewohnt. Die Größenempfehlungen für einen Verwaltungspunkt ändern sich nicht abhängig davon, ob er Anforderungen lokaler oder internetbasierter Clients erfüllt.

### <a name="software-update-point"></a>Softwareupdatepunkt  

Verwenden Sie die folgenden Empfehlungen als Orientierung. Sie können hilfreich sein, um die für Ihre Organisation geeigneten Informationen zur Kapazitätsplanung für Softwareupdates zu ermitteln. Der tatsächliche Kapazitätsbedarf kann von den Empfehlungen in diesem Artikel in Abhängigkeit der folgenden Kriterien abweichen:

- Ihre spezifische Netzwerkumgebung
- Die Hardware, die Sie verwenden, um das Softwareupdatepunktsystem zu hosten
- Die Anzahl der verwalteten Clients
- Die sonstigen auf dem Server installierten Standortsystemrollen  

> [!NOTE]
> Wenn Sie den Softwareupdatepunkt für die Unterstützung von [Cloud Management Gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md) aktivieren, erfüllt er die Anforderungen internetbasierter Clients wie gewohnt. Die Größenempfehlungen für einen Softwareupdatepunkt ändern sich nicht abhängig davon, ob er Anforderungen lokaler oder internetbasierter Clients erfüllt.

#### <a name="capacity-planning-for-the-software-update-point"></a><a name="BKMK_SUMCapacity"></a> Kapazitätsplanung für den Softwareupdatepunkt  

Die Anzahl der unterstützten Clients hängt von der Version der Windows Server Update Services (WSUS) ab, die auf dem Softwareupdatepunkt ausgeführt wird. Außerdem hängt sie davon ab, ob neben der Softwareupdatepunkt-Standortsystemrolle noch eine weitere Standortsystemrolle vorhanden ist:  

- Vom Softwareupdatepunkt werden bis zu 25.000 Clients unterstützt, wenn WSUS auf dem Softwareupdatepunktserver ausgeführt wird und neben dem Softwareupdatepunkt noch eine weitere Standortsystemrolle vorhanden ist.  

- Der Softwareupdatepunkt kann bis zu 150.000 Clients unterstützen, wenn ein Remoteserver die WSUS-Anforderungen erfüllt, WSUS mit Configuration Manager verwendet wird und Sie die folgenden Einstellungen konfigurieren:

  IIS-Anwendungspools:

  - Erhöhen Sie die WsusPool-Warteschlangenlänge auf 2000.
  - Erhöhen Sie die Begrenzung des privaten Speichers für WsusPool auf das Vierfache, oder legen Sie den Wert auf 0 (unbegrenzt) fest. Wenn die Standardbegrenzung beispielsweise 1.843.200 KB beträgt, erhöhen Sie sie auf 7.372.800. Weitere Informationen finden Sie in folgendem [Blogbeitrag des Configuration Manager-Supportteams](https://www.phoenixtekk.com/configmgr-2012-support-tip-wsus-sync-fails-with-http-503-errors/).  

    Weitere Informationen zu den Hardwareanforderungen für den Softwareupdatepunkt finden Sie unter [Empfohlene Hardware für Standortsysteme](recommended-hardware.md#bkmk_ScaleSieSystems).  

#### <a name="capacity-planning-for-software-updates-objects"></a><a name="bkmk_sum-capacity-obj"></a> Kapazitätsplanung für Softwareupdateobjekte  

Verwenden Sie die folgenden Kapazitätsinformationen zur Planung von Softwareupdateobjekten:  

- **Maximal 1000 Softwareupdates in einer Bereitstellung**: Begrenzen Sie die Anzahl von Softwareupdates in einer einzelnen Softwareupdatebereitstellung auf 1000. Geben Sie beim Erstellen einer Regel für die automatische Bereitstellung ein Kriterium an, durch das die Anzahl der Softwareupdates beschränkt wird. Die automatische Bereitstellungsregel schlägt fehl, wenn die angegebenen Kriterien mehr als 1000 Softwareupdates zurückgeben. Sie können den Status der automatischen Bereitstellungsregel im Knoten **Automatische Bereitstellungsregeln** in der Configuration Manager-Konsole überprüfen. Wählen Sie höchstens 1000 Updates zur Bereitstellung aus, wenn Sie Softwareupdates manuell bereitstellen.  

  Begrenzen Sie auch die Anzahl der Softwareupdates in einer Konfigurationsbaseline auf 1000. Weitere Informationen finden Sie unter [Erstellen von Konfigurationsbaselines](../../../compliance/deploy-use/create-configuration-baselines.md).

- **Maximal 580 Sicherheitsbereiche für automatische Bereitstellungsregeln** -<!--ado 4962928-->
Begrenzen Sie die Anzahl der Sicherheitsbereiche für automatische Bereitstellungsregeln auf weniger als 580. Wenn Sie eine automatische Bereitstellungsregel erstellen, werden die Sicherheitsbereiche, die Zugriff auf die Regel haben, automatisch hinzugefügt. Wenn mehr als 580 Sicherheitsbereiche festgelegt sind, kann die automatische Bereitstellungsregel nicht ausgeführt werden, und in „ruleengine.log“ wird ein Fehler protokolliert.

### <a name="sms-provider"></a>SMS-Anbieter

<!-- SCCMDocs#1958 -->

Jede Instanz des SMS-Anbieters unterstützt gleichzeitige Verbindungen von mehreren Anforderungen. Diese Verbindungen unterliegen nur zwei Einschränkungen. Dabei handelt es sich um die Anzahl der Serververbindungen sowie um die zur Bearbeitung der Verbindungsanforderungen erforderlichen Ressourcen, die unter Windows bzw. auf dem Server verfügbar sind.

Weitere Informationen finden Sie unter [Planen des SMS-Anbieters](../hierarchy/plan-for-the-sms-provider.md).

## <a name="client-numbers-for-sites-and-hierarchies"></a><a name="bkmk_clientnumbers"></a> Anzahl der Clients für Standorte und Hierarchien

Ermitteln Sie anhand der folgenden Informationen, wie viele Clients – und welchen Typs – Sie an einem Standort oder in einer Hierarchie unterstützen können.  

### <a name="hierarchy-with-a-central-administration-site"></a><a name="bkmk_cas"></a> Hierarchie mit Standort der zentralen Verwaltung

Ein Standort der zentralen Verwaltung unterstützt eine Gesamtanzahl an Geräten, die maximal der Anzahl an Geräten entspricht, die für die folgenden drei Gruppen aufgelistet ist:  

- 700.000 Windows-Desktops. Weitere Informationen finden Sie auch in der Unterstützung für [Embedded-Geräte](#embedded).

- 25.000 Macintosh- und Windows CE 7.0-Geräte  

- 100.000 Geräte, die Sie mithilfe der lokalen Verwaltung mobiler Geräte verwalten.

In einer Hierarchie können beispielsweise 700.000 Desktops, bis zu 25.000 Clients für Mac- und Windows CE 7.0-Geräte sowie bis zu 100.000 mobile Geräte unterstützt werden, die lokal verwaltet werden. Das sind insgesamt 825.000 unterstützte Geräte.

> [!IMPORTANT]  
> In einer Hierarchie, in der für den Standort der zentralen Verwaltung eine Standardedition von SQL Server verwendet wird, werden in der Hierarchie bis zu 50.000 Desktops und Geräte unterstützt. Um mehr als 50.000 Desktop-PCs und Geräte zu unterstützen, müssen Sie eine Enterprise-Edition von SQL Server verwenden. Diese Anforderung gilt nur für einen Standort der zentralen Verwaltung. Sie gilt nicht für einen eigenständigen primären oder einen untergeordneter primärer Standort. Die verwendete SQL Server-Edition eines primären Standorts schränkt nicht die Anzahl der unterstützten Clients ein.

Die an einem eigenständigen primären Standort eingesetzte Edition von SQL Server beschränkt nicht die Kapazität dieses Standorts zur Unterstützung der angegebenen maximalen Anzahl von Clients.  

### <a name="child-primary-site"></a><a name="bkmk_chipri"></a> Untergeordneter primärer Standort

Jeder untergeordnete primäre Standort in einer Hierarchie mit einem zentralen Verwaltungsstandort unterstützt die folgende Anzahl von Clients:  

- Insgesamt 150.000 Clients und Geräte, nicht beschränkt auf bestimmte Gruppen oder Typen, solange die unterstützte Gesamtanzahl in der Hierarchie nicht überschritten wird. Weitere Informationen finden Sie auch in der Unterstützung für [Embedded-Geräte](#embedded).

Ein primärer Standort unterstützt beispielsweise 25.000 Mac- und Windows CE 7.0-Geräte. Das ist die maximale Anzahl in einer Hierarchie. Dieser primäre Standort kann zusätzlich 125.000 Desktopcomputer unterstützen. Somit beträgt die maximale Anzahl der insgesamt unterstützten Geräte für einen untergeordneten primären Standort 150.000 Geräte.

### <a name="stand-alone-primary-site"></a><a name="bkmk_pri"></a> Eigenständiger primärer Standort

Ein eigenständiger primärer Standort unterstützt die folgende Anzahl von Geräten:  

- 175.000 Clients und Geräte insgesamt, nicht überschreiten:  

  - 150.000 Desktops (Computer, auf denen Windows, Linux und UNIX ausgeführt wird). Weitere Informationen finden Sie auch in der Unterstützung für [Embedded-Geräte](#embedded).

  - 25.000 Macintosh- und Windows CE 7.0-Geräte

  - 50.000 Geräte, die mithilfe der lokalen Verwaltung mobiler Geräte verwaltet werden  

Beispielsweise kann ein eigenständiger primärer Standort, der 150.000 Desktops und 10.000 Macs unterstützt nur 15.000 mobile Geräte zusätzlich unterstützen, die lokal verwaltet werden.

### <a name="primary-sites-and-windows-embedded-devices"></a><a name="embedded"></a> Primäre Standorte und Windows Embedded-Geräte

Primäre Standorte unterstützen Windows Embedded-Geräte, für die dateibasierte Schreibfilter (File Based Write Filter, FBWF) aktiviert sind. Wenn für eingebettete Geräte keine Schreibfilter aktiviert sind, kann ein primärer Standort eingebettete Geräte bis zur zulässigen Anzahl von Geräten für diesen Standort unterstützen. Wenn für eingebettete Geräte FBWF oder UWF (Unified Write Filter) aktiviert sind, kann ein primärer Standort maximal 10.000 Windows Embedded-Geräte unterstützen. Diese Geräte müssen mit den Ausnahmen konfiguriert sein, die unter [Planen der Clientbereitstellung für Windows Embedded-Geräte in System Center Configuration Manager](../../clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md) aufgelistet sind. Ein primärer Standort unterstützt nur 3.000 Windows Embedded-Geräte, für die EWF aktiviert ist. Für diese Geräte dürfen keine Ausnahmen konfiguriert werden.

### <a name="secondary-sites"></a><a name="bkmk_sec"></a> Sekundäre Standorte

Sekundäre Standorte unterstützen die folgende Anzahl an Geräten:  

- 15.000 Desktops (Computer, auf denen Windows, Linux und UNIX ausgeführt wird)  

### <a name="management-points"></a><a name="bkmk_mp"></a> Verwaltungspunkte

Von jedem Verwaltungspunkt kann die folgende Anzahl von Geräten unterstützt werden:  

- 25.000 Clients und Geräte insgesamt, nicht überschreiten:  

  - 25.000 Desktops (Computer, auf denen Windows, Linux und UNIX ausgeführt wird)  

  - Eine der folgenden Alternativen (nicht beide):  

    - 10.000 Geräte, die mithilfe der lokalen Verwaltung mobiler Geräte verwaltet werden  

    - 10.000 Macintosh- und Windows CE 7.0-Clients
