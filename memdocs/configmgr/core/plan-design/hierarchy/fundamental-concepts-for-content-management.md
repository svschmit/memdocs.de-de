---
title: Grundlagen der Inhaltsverwaltung
titleSuffix: Configuration Manager
description: Verwenden Sie Tools und Optionen in Configuration Manager, um den Inhalt zu verwalten, den Sie bereitstellen.
ms.date: 12/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c201be2a-692c-4d67-ac95-0a3afa5320fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fb3639a1d6734bf63b270e252c39862a33f13401
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697028"
---
# <a name="fundamental-concepts-for-content-management-in-configuration-manager"></a>Grundlegende Konzepte für die Inhaltsverwaltung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Configuration Manager unterstützt ein widerstandsfähiges System von Tools und Optionen zum Verwalten von Softwareinhalten. Softwarebereitstellungen wie Anwendungen, Pakete, Softwareupdates und Betriebssystembereitstellungen benötigen Inhalte. Configuration Manager speichert den Inhalt jeweils auf Standortservern und Verteilungspunkten. Diese Inhalte erfordern bei der Übertragung zwischen den Standorten einen großen Anteil der Netzwerkbandbreite. Zur effektiven Planung und Verwendung der Inhaltsverwaltungsinfrastruktur sollten Sie zunächst die verfügbaren Optionen und Konfigurationen kennen. Wägen Sie dann ab, wie Sie diese am besten an Ihre Anforderungen an die Netzwerkumgebung und die Bereitstellung von Inhalten anzupassen.  

> [!TIP]  
> Weitere Informationen über den Prozess zur Inhaltsverteilung und Hilfe zur Diagnose und Behebung von allgemeinen Problemen bei der Inhaltsverteilung finden Sie unter [Verstehen und behandeln Content-Verteilung in Configuration Manager](https://support.microsoft.com/help/4000401/content-distribution-in-mcm).

In den folgenden Abschnitten werden Schlüsselkonzepte für die Inhaltsverwaltung behandelt. Wenn für ein Konzept zusätzliche oder komplexe Informationen erforderlich sind, werden Links bereitgestellt, die Sie zu diesen Details leiten.


## <a name="accounts-used-for-content-management"></a>Für das Content Management verwendete Konten

Die folgenden Konten können mit dem Content Management verwendet werden:  

### <a name="network-access-account"></a>Netzwerkzugriffskonto

Wird von Clients verwendet, um die Verbindung zu einem Verteilungspunkt herzustellen und auf Inhalte zuzugreifen. Das Computerkonto wird standardmäßig zuerst ausprobiert.  

Dieses Konto wird auch von Pullverteilungspunkten verwendet, um Inhalte von einem Quellverteilungspunkt in einer Remotegesamtstruktur herunterzuladen.  

Ab Version 1806 ist für einige Szenarios kein Netzwerkzugriffskonto mehr erforderlich. Sie können die Verwendung von erweitertem HTTP mit Azure Active Directory-Authentifizierung für den Standort aktivieren.<!--1358228-->

Weitere Informationen finden Sie unter [Netzwerkzugriffskonto](accounts.md#network-access-account).

### <a name="package-access-account"></a>Paketzugriffskonto

Standardmäßig gewährt Configuration Manager den generischen Zugriffskonten „Benutzer“ und „Administratoren“ Zugriff auf Inhalte auf einem Verteilungspunkt. Sie können jedoch weitere Berechtigungen konfigurieren, um den Zugriff zu beschränken.

Weitere Informationen finden Sie unter [Paketzugriffskonto](accounts.md#package-access-account).


## <a name="bandwidth-throttling-and-scheduling"></a>Zeitplanung und Einschränkung der Bandbreite

Sowohl Einschränkung als auch Zeitplanung sind Optionen, mit denen Sie steuern können, wann Inhalte von einem Standortserver an Verteilungspunkte verteilt werden. Diese Funktionen sind mit der Bandbreitensteuerung für dateibasierte Replikation von Standort zu Standort vergleichbar, stehen damit aber in keinem direkten Zusammenhang.  

Weitere Informationen finden Sie unter [Verwalten der Netzwerkbandbreite für Inhalt](manage-network-bandwidth.md).


## <a name="binary-differential-replication"></a>Binäre differenzielle Replikation

Configuration Manager verwendet die binäre differenzielle Replikation (BDR), um Inhalte zu aktualisieren, die Sie zuvor an andere Standorte oder an Remoteverteilungspunkte verteilt haben. Installieren Sie das Feature **Remotedifferenzialkomprimierung** auf den Verteilungspunkten, um die Reduzierung der Auslastung der Netzwerkbandbreite durch die BDR zu unterstützen. Weitere Informationen finden Sie unter [Voraussetzungen für Verteilungspunkte](../configs/site-and-site-system-prerequisites.md#bkmk_2012dppreq).

Die BDR minimiert die Netzwerkbandbreite, die zum Senden von Updates für verteilten Inhalt verwendet wird. Sie sendet nur den neuen oder geänderten Inhalt anstatt des gesamten Inhalts der Quelldateien, wenn diese Dateien geändert werden.  

Wenn die BDR verwendet wird, werden in Configuration Manager die Änderungen ermittelt, die an Quelldateien für jeden zuvor verteilten Inhaltssatz vorgenommen wurden.  

- Wenn Dateien im Quellinhalt geändert werden, wird vom Standort eine neue inkrementelle Version des Inhalts erstellt. Anschließend werden nur die geänderten Dateien auf Zielstandorte und Verteilungspunkte repliziert. Eine Datei wird als geändert angesehen, wenn Sie sie umbenannt oder verschoben haben oder den Inhalt geändert haben. Wenn Sie beispielsweise eine Treiberdatei für ein Treiberpaket, das Sie zuvor an mehrere Standorte verteilt haben, ersetzen, wird nur die geänderte Treiberdatei repliziert.  

- Von Configuration Manager werden bis zu fünf inkrementelle Versionen eines Inhaltssatzes unterstützt, bevor der gesamte Inhaltssatz erneut gesendet wird. Nach der fünften Aktualisierung führt die nächste Änderung am Inhaltssatz dazu, dass vom Standort eine neue Version des Inhaltssatzes erstellt wird. Configuration Manager verteilt dann die neue Version des Inhaltssatzes, um den früheren Satz und die inkrementellen Versionen zu ersetzen. Nach der Verteilung des neuen Inhaltssatzes werden spätere inkrementelle Änderungen an den Quelldateien erneut durch die BDR repliziert.  

BDR wird zwischen übergeordneten und untergeordneten Standorten in einer Hierarchie unterstützt. Innerhalb eines Standorts wird BDR zwischen dem Standortserver und dessen regulären Verteilungspunkten unterstützt. Von Pullverteilungspunkten und Cloudverteilungspunkten wird die BDR zum Übertragen von Inhalten jedoch nicht unterstützt. Pullverteilungspunkte unterstützen Deltas auf Dateiebene und das Übertragen neuer Dateien, aber keine Blöcke in einer Datei.

Für Anwendungen wird immer die binäre differenzielle Replikation verwendet. Die BDR ist für Pakete optional und standardmäßig nicht aktiviert. Damit Sie die BDR für Pakete verwenden können, müssen Sie diese Funktion für jedes Paket aktivieren. Wählen Sie die Option **Binäre differenzielle Replikation aktivieren** aus, wenn Sie ein Paket erstellen oder bearbeiten.


### <a name="bdr-or-delta-replication"></a>BDR oder Deltareplikation

<!-- SCCMDocs#1209 -->
In den folgenden Listen werden die Unterschiede zwischen der *binären differenziellen Replikation* (BDR) und der *Deltareplikation* zusammengefasst.

#### <a name="summary-of-binary-differential-replication"></a>Zusammenfassung der binären differenziellen Replikation

- Configuration Manager-Begriff für die **Remotedifferenzialkomprimierung** von Windows
- Unterschiede auf *Blockebene*
- Für Apps immer aktiviert
- Optional bei Legacypaketen
- Wenn eine Datei bereits am Verteilungspunkt vorhanden ist und eine Änderung stattfindet, repliziert der Standort mithilfe der BDR die Änderung auf Blockebene anstelle der gesamten Datei.

#### <a name="summary-of-delta-replication"></a>Zusammenfassung der Deltareplikation

- Unterschiede auf *Dateiebene*
- Standardmäßig aktiviert, nicht konfigurierbar
- Wenn ein Paket geändert wird, überprüft der Standort die einzelnen Dateien und nicht das gesamte Paket auf Änderungen.
    - Wenn eine Datei geändert wird, führen Sie den Vorgang mit der BDR aus.
    - Ist eine neue Datei vorhanden, kopieren Sie die neue Datei.


## <a name="peer-caching-technologies"></a>Peercachingtechnologien

<!-- SCCMDocs#1044 -->

Configuration Manager unterstützt verschiedene Optionen für das Verwalten von Inhalten zwischen Peergeräten im selben Netzwerk:

- [BranchCache](#branchcache)
- [Übermittlungsoptimierung](#delivery-optimization)
- [Configuration Manager-Peercache](#peer-cache)

Vergleichen Sie anhand der folgenden Tabelle grundlegende Features dieser Technologien:

| Komponente  | Peercache&nbsp;  | Übermittlungsoptimierung&nbsp;  | BranchCache  |
|---------|---------|---------|---------|
| Subnetzübergreifend | Ja | Ja | Nein |
| Bandbreitendrosselung | Ja (BITS) | Ja (nativ) | Ja (BITS) |
| Teilinhalt | Ja | Ja | Ja |
| Steuerung der Cachegröße auf dem Datenträger | Ja | Ja | Ja |
| Peerquellenermittlung | Manuell (Clienteinstellung) | Automatisch | Automatisch |
| Peerermittlung | Über Verwaltungspunkt mithilfe von Begrenzungsgruppen | Übermittlungsoptimierung-Clouddienst | Übertragen |
| Berichterstellung | Dashboard „Clientdatenquellen“ | Dashboard „Clientdatenquellen“ | Dashboard „Clientdatenquellen“ |
| Steuerung der WAN-Nutzung | Begrenzungsgruppen | Übermittlungsoptimierung-GroupID | Nur Subnetz |
| Unterstützte Inhalte | Alle ConfigMgr-Inhalte | Windows-Updates, Treiber, Store-Apps | Alle ConfigMgr-Inhalte |
| Richtliniensteuerung | Client-Agent-Einstellungen | Client-Agent-Einstellungen (teilweise) | Client-Agent-Einstellungen |

### <a name="recommendations"></a>Empfehlungen

- Moderne Verwaltung: Wenn Sie bereits moderne Tools wie Intune verwenden, implementieren Sie die Übermittlungsoptimierung.

- Configuration Manager und Co-Verwaltung: Verwenden Sie eine Kombination aus Peercache und Übermittlungsoptimierung. Verwenden Sie den Peercache mit lokalen Verteilungspunkten, und nutzen Sie die Übermittlungsoptimierung für Cloudumgebungen.

- Vorhandener BranchCache implementiert: Verwenden Sie alle drei Technologien parallel. Verwenden Sie Peercache und Übermittlungsoptimierung für Szenarien, die von BranchCache nicht unterstützt werden.


## <a name="branchcache"></a>BranchCache

[BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) ist eine Windows-Technologie. Clients, die BranchCache unterstützen und eine von Ihnen für BranchCache konfigurierte Bereitstellung heruntergeladen haben, fungieren anschließend als Inhaltsquelle für andere Clients mit aktivierter BranchCache-Funktion.  

Sie verfügen beispielsweise über einen Verteilungspunkt, der Windows Server 2012 oder höher ausführt und als BranchCache-Sever konfiguriert ist. Wenn der erste BranchCache-fähige Client Inhalt von diesem Server anfordert, lädt er diesen Inhalt herunter und speichert ihn zwischen.  

- Dieser Clientcomputer stellt den Inhalt dann für weitere Clients mit aktivierter BranchCache-Funktion im gleichen Subnetz zur Verfügung, die den Inhalt ebenfalls zwischenspeichern.  
- Andere Clients, die sich im gleichen Subnetz befinden, müssen den Inhalt vom Verteilungspunkt nicht herunterladen.  
- Der Inhalt ist für spätere Übertragungen über mehrere Clients verteilt.  

Weitere Informationen finden Sie unter [Unterstützung für Windows BranchCache](../configs/support-for-windows-features-and-networks.md#bkmk_branchcache).

## <a name="delivery-optimization"></a>Übermittlungsoptimierung

<!-- 1324696 -->
Sie verwenden Configuration Manager-Begrenzungsgruppen, um die Inhaltsverteilung über Ihr gesamtes Unternehmensnetzwerk und Remotebüros hinweg zu definieren und zu regulieren. [Windows-Übermittlungsoptimierung](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) ist eine cloudbasierte Peer-zu-Peer-Technologie zum gemeinsamen Nutzen von Inhalten auf Windows 10-Geräten. Konfigurieren Sie die Übermittlungsoptimierung so, dass bei der Freigabe von Inhalten für Peers Ihre Begrenzungsgruppen verwendet werden. Clienteinstellungen legen die Begrenzungsgruppen-ID als Gruppen-ID für die Übermittlungsoptimierung auf dem Client fest. Wenn der Client mit dem Übermittlungsoptimierungs-Clouddienst kommuniziert, wird diese ID zum Ermitteln von Peers verwendet, auf denen sich die Inhalte befinden. Weitere Informationen finden Sie unter den Clienteinstellungen für die [Übermittlungsoptimierung](../../clients/deploy/about-client-settings.md#delivery-optimization).

Übermittlungsoptimierung ist die empfohlene Technologie zum Optimieren der Windows 10-Updatebereitstellung von Expressinstallationsdateien für Windows 10-Qualitätsupdates. Ab Configuration Manager Version 1910 ist der Internetzugriff auf den Clouddienst Übermittlungsoptimierung eine Anforderung für den Einsatz der Peer-zu-Peer-Funktionalität. Informationen zu den erforderlichen Internetendpunkten finden Sie unter [Häufig gestellte Fragen zur Übermittlungsoptimierung](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions). Die Optimierung kann für alle Windows-Updates verwendet werden. Weitere Informationen finden Sie unter [Optimieren der Bereitstellung von Updates für Windows 10](../../../sum/deploy-use/optimize-windows-10-update-delivery.md).


## <a name="microsoft-connected-cache"></a>Microsoft Connected Cache

<!--3555764-->
Ab Version 1906 können Sie einen Microsoft Connected Cache-Server auf Ihren Verteilungspunkten installieren. Wenn Sie diese Art von Inhalt lokal zwischenspeichern, können Ihre Clients von dem Feature zur Übermittlungsoptimierung profitieren, und Sie können dabei helfen, WAN-Links zu schützen.

> [!NOTE]
> Ab Version 1910 wird dieses Feature als **Microsoft Connected Cache** bezeichnet. Zuvor wurde es als Übermittlungsoptimierung durch netzwerkinternen Cache (Delivery Optimization In-Network Cache, DOINC) bezeichnet.

Dieser Cacheserver dient als bedarfsgesteuerter transparenter Cache für Inhalt, der von der Übermittlungsoptimierung heruntergeladen wird. Verwenden Sie Clienteinstellungen, um sicherzustellen, dass dieser Server nur Mitgliedern der lokalen Begrenzungsgruppe für Configuration Manager angeboten wird.

Dieser Cache ist unabhängig vom Inhalt des Verteilungspunkts für Configuration Manager. Wenn Sie denselben Datenträger auswählen wie die Rolle des Verteilungspunkts, wird der Inhalt separat gespeichert.

Weitere Informationen finden Sie unter [Microsoft Connected Cache in Configuration Manager](microsoft-connected-cache.md).


## <a name="peer-cache"></a>Peercache

Der Clientpeercache unterstützt Sie beim Verwalten von Bereitstellungen von Inhalten an Clients an Remotestandorten. Der Peercache ist eine integrierte Configuration Manager-Lösung, mit deren Hilfe Clients Inhalte für andere Clients direkt aus ihrem lokalen Cache freigeben können.

Stellen Sie zuerst die Clienteinstellungen bereit, die den Peercache für eine Sammlung aktivieren. Mitglieder dieser Sammlung können dann als Peerinhaltsquelle für andere Clients in derselben Begrenzungsgruppe fungieren.

Ab Version 1806 können Clientpeercachequellen Inhalt in mehrere Teile untergliedern. Diese Teile minimieren die Netzwerkdatenübertragung, um die WAN-Auslastung zu reduzieren. Der Verwaltungspunkt erlaubt eine genauere Nachverfolgung der Inhaltsteile. Er versucht, mehrere Downloads desselben Inhalts pro Begrenzungsgruppe zu vermeiden.<!--1357346-->

Weitere Informationen finden Sie unter [Peercache für Configuration Manager-Clients](client-peer-cache.md).


## <a name="windows-pe-peer-cache"></a>Windows PE-Peercache

Wenn Sie ein neues Betriebssystem mit Configuration Manager bereitstellen, können Computer, die die Tasksequenz ausführen, den Windows PE-Peercache verwenden. Es wird Inhalt aus einer Peercachequelle anstatt aus einem Verteilungspunkt heruntergeladen. Auf diese Weise können Sie WAN-Datenverkehr in Zweigstellenszenarios minimieren, wenn kein lokaler Verteilungspunkt vorhanden ist.

Weitere Informationen finden Sie unter [Windows PE-Peercache](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).


## <a name="windows-ledbat"></a>Windows LEDBAT

<!--1358112-->
Windows Low Extra Delay Background Transport (LEDBAT) ist ein Netzwerküberlastungssteuerungs-Feature von Windows Server zum Verwalten von Netzwerkübertragungen im Hintergrund. Für Verteilungspunkte, die auf unterstützten Versionen von Windows Server ausgeführt werden, können Sie eine Option zum Anpassen des Netzwerkdatenverkehrs aktivieren. Dann verwenden Clients die Netzwerkbandbreite nur, wenn sie verfügbar ist.

Weitere allgemeine Informationen zu Windows LEDBAT finden Sie im Blogbeitrag [New transport advancements (Weiterentwicklungen bei der Übertragung)](https://techcommunity.microsoft.com/t5/Networking-Blog/Announcing-Transport-Features-and-Performance-Advancements-in/ba-p/339726).

Weitere Informationen zur Verwendung von Windows LEDBAT mit Configuration Manager-Verteilungspunkten finden Sie in der Einstellung zum **Anpassen der Downloadgeschwindigkeit, um ungenutzte Netzwerkbandbreite zu verwenden (Windows LEDBAT)** , wenn Sie [die allgemeinen Einstellungen eines Verteilungspunkts konfigurieren](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-general).


## <a name="client-locations"></a>Clientstandorte

Clients können auf Inhalte der folgenden Standorte zugreifen:  

- **Intranet** (lokal):  

    - Verteilungspunkte können HTTP oder HTTPs verwenden.  

    - Ein Cloudverteilungspunkt wird nur dann für ein Fallback verwendet, wenn keine lokalen Verteilungspunkte verfügbar sind.  

- **Internet**:  

    - Verteilungspunkte mit Internetzugriff müssen HTTPS akzeptieren.  

    - Ein Cloudverteilungspunkt oder Cloud Management Gateway (CMG) kann verwendet werden.  

        Ab Version 1806 kann ein CMG auch Inhalte für Clients bereitstellen. Diese Funktion reduziert die erforderlichen Zertifikate und Kosten für Azure-VMs. Weitere Informationen finden Sie unter [Ändern eines CMG](../../clients/manage/cmg/setup-cloud-management-gateway.md).

- **Arbeitsgruppe**:  

    - Verteilungspunkte müssen HTTPS akzeptieren.  

    - Ein Cloudverteilungspunkt oder CMG kann verwendet werden.  


## <a name="content-source-priority"></a>Priorität von Inhaltsquellen

Wenn ein Client auf Inhalte zugreifen muss, sendet er eine Inhaltsortsanforderung an den Verwaltungspunkt. Der Verwaltungspunkt gibt eine Liste von Quellspeicherorten zurück, die für den angeforderten Inhalt gültig sind. Diese Liste variiert je nach Szenario, verwendeten Technologien, Standortentwurf, Begrenzungsgruppen und Bereitstellungseinstellungen. Die folgende Liste enthält alle möglichen Quellspeicherorte, die ein Client verwenden kann, in der Reihenfolge, in der sie priorisiert werden:  

1. Der Verteilungspunkt auf dem gleichen Computer wie der Client
2. Eine Peerquelle im gleichen Subnetz des Netzwerks
3. Ein Verteilungspunkt im gleichen Subnetz des Netzwerks
4. Eine Peerquelle in der gleichen Begrenzungsgruppe
5. Ein Verteilungspunkt in der aktuellen Begrenzungsgruppe
6. Ein Verteilungspunkt in einer benachbarten Begrenzungsgruppe, der als Fallback konfiguriert ist
7. Ein Verteilungspunkt in der Standardstandortbegrenzungsgruppe
8. Der Windows Update-Clouddienst
9. Ein Verteilungspunkt mit Internetzugriff
10. Ein Cloudverteilungspunkt in Azure

> [!Note]  
> <!-- SCCMDocs#1607 -->Die Übermittlungsoptimierung kann auf diese Priorisierung von Quellen nicht angewendet werden. In dieser Liste wird angegeben, wie der Configuration Manager-Client nach Inhalten sucht. Der Windows Update-Agent lädt Inhalte für die Übermittlungsoptimierung herunter. Wenn der Windows Update-Agent die Inhalte nicht finden kann, sucht der Configuration Manager-Client anhand dieser Liste danach.

## <a name="content-library"></a>Inhaltsbibliothek

Die Inhaltsbibliothek ist der Inhaltsspeicher mit einer Instanz in Configuration Manager. Durch diese Bibliothek wird die Gesamtgröße des Inhalts verringert, den Sie verteilen.  

- Weitere Informationen zur [Inhaltsbibliothek](the-content-library.md).
- Verwenden Sie das [Inhaltsbibliothek-Bereinigungstool](content-library-cleanup-tool.md) für die Entfernung von Inhalt, der nicht mehr einer Anwendung zugeordnet ist.  


## <a name="distribution-points"></a>Verteilungspunkte

Configuration Manager verwendet Verteilungspunkte, um Dateien zu speichern, die zum Ausführen von Software auf Clientcomputern erforderlich sind. Für die Clients ist zum Herunterladen der Dateien mit den von Ihnen bereitgestellten Inhalten ein Zugriff auf mindestens einen Verteilungspunkt erforderlich.  

Der (nicht spezialisierte) Basisverteilungspunkt wird häufig als Standardverteilungspunkt bezeichnet. Es gibt zwei Variationen auf dem Standardverteilungspunkt, die besondere Aufmerksamkeit erhalten:  

- **Pullverteilungspunkt:** Eine Variante eines Verteilungspunkts, bei der der Verteilungspunkt Inhalt von einem anderen Verteilungspunkt (einem Quellverteilungspunkt) erhält. Dies ähnelt dem Prozess, wie Clients Inhalt von Verteilungspunkten herunterladen. Pullverteilungspunkte können Ihnen dabei helfen, Engpässe bei der Netzwerkbandbreite zu vermeiden, die auftreten, wenn der Standortserver Inhalt an jeden Verteilungspunkt direkt verteilen muss. [Verwenden eines Pullverteilungspunkts](use-a-pull-distribution-point.md)

- **Cloudverteilungspunkt:** Eine Variante eines in Microsoft Azure installierten Verteilungspunkts. [Verwenden eines Cloudverteilungspunkts](use-a-cloud-based-distribution-point.md)  

Standardverteilungspunkte unterstützen eine Reihe von Konfigurationen und Features:  

- Verwenden Sie Steuerelemente wie **Zeitpläne** oder **Bandbreiteneinschränkung**, um diese Übertragung zu überwachen.  

- Verwenden Sie auch andere Optionen, darunter **vorab bereitgestellten Inhalt** und **Pullverteilungspunkte**, um die Netzwerknutzung zu reduzieren und zu steuern.  

- **BranchCache**, **Peercache** und **Übermittlungsoptimierung** sind Peer-zu-Peer-Technologien, um die Netzwerkbandbreite zu reduzieren, die zur Bereitstellung von Inhalt verwendet wird.  

- Für Betriebssystembereitstellungen gibt es unterschiedliche Konfigurationen, z.B. **[PXE](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)** und **[Multicast](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast)** .  

- Optionen für **mobile Geräte**  
  
Cloud- und Pullverteilungspunkte unterstützen viele der gleichen Konfigurationen, jedoch weist jede Verteilungspunktvariante spezifische Einschränkungen auf.  


## <a name="distribution-point-groups"></a>Verteilungspunktgruppen

Verteilungspunktgruppen sind logische Gruppierung von Verteilungspunkten, die die Inhaltsverteilung vereinfachen können.  

Weitere Informationen finden Sie unter [Verwalten von Verteilungspunktgruppen](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage).


## <a name="distribution-point-priority"></a>Verteilungspunktpriorität

Der Wert der Verteilungspunktpriorität basiert darauf, wie lange die Übertragung vorheriger Bereitstellungen auf diesen Verteilungspunkt gedauert hat.  

- Dieser Wert ist selbstoptimierend. Er wird auf jedem Verteilungspunkt festgelegt, damit Configuration Manager ermöglicht wird, Inhalt schneller an mehr Verteilungspunkte zu verteilen.  

- Wenn Sie Inhalt an mehrere Verteilungspunkte gleichzeitig oder an eine Verteilungspunktgruppe verteilen, sendet der Standort zunächst den Inhalt an den Server mit der höchsten Priorität. Anschließend wird der gleiche Inhalt an einen Verteilungspunkt mit einer niedrigeren Priorität gesendet.  

- Mit der Priorität eines Verteilungspunkts wird die Paketverteilungspriorität nicht ersetzt. Die Paketpriorität bleibt der entscheidende Faktor, wenn der Standort unterschiedliche Inhalte sendet.  

Sie besitzen z.B. ein Paket, das über eine hohe Paketpriorität verfügt. Sie verteilen es an einen Server mit einer niedrigen Verteilungspriorität. Dieses Paket mit hoher Priorität wird immer vor einem Paket mit niedriger Priorität umgewandelt. Die Paketpriorität gilt auch, wenn der Standort Pakete mit niedriger Priorität an Server mit höheren Verteilungspunktprioritäten verteilt.

Durch die hohe Priorität eines Pakets wird sichergestellt, dass Inhalt von Configuration Manager an die Verteilungspunkte übertragen wird, bevor Pakete mit niedrigerer Priorität gesendet werden.  

> [!NOTE]  
> Bei Pullverteilungspunkten wird das Konzept der Priorität außerdem verwendet, um die Sequenz von deren Quellverteilungspunkten zu ordnen.  
>
> - Die Verteilungspunktpriorität für Inhaltsübertragungen an den Sever unterscheidet sich von der Priorität, die von Pullverteilungspunkt verwendet wird. Pullverteilungspunkte verwenden Ihre Priorität, wenn sie nach Inhalt von suchen.  
> - Weitere Informationen finden Sie unter [Use a pull-distribution point (Verwenden eines Verteilungspunkts)](use-a-pull-distribution-point.md).  


## <a name="fallback"></a>Fallback

In Configuration Manager-Current Branch hat sich einiges dahingehend verändert, dass Clients einen Verteilungspunkt finden, der Inhalte enthält, einschließlich Fallbacks.

Clients, die keine Inhalte eines Verteilungspunkts finden können, der ihrer aktuellen Begrenzungsgruppe zugeordnet ist, führen einen Fallback aus, um Quellspeicherorte zu verwenden, die benachbarten Begrenzungsgruppen zugeordnet sind. Damit eine benachbarte Begrenzungsgruppe für Fallbacks verwendet werden kann, muss eine Beziehung zu der aktuellen Begrenzungsgruppe des Clients definiert sein. Diese Beziehung muss eine konfigurierte Zeitspanne enthalten. Diese Zeitspanne muss abgelaufen sein, bevor ein Client, der lokal keinen Inhalt findet, Inhaltsquellen der benachbarten Begrenzungsgruppe in seine Suche mit aufnehmen kann.

Die Konzepte der bevorzugten Verteilungspunkte werden nicht mehr verwendet, und Einstellungen für die Option **Allow fallback source locations for content** (Fallbackspeicherorte für Inhalt zulassen) sind nicht mehr verfügbar oder erzwungen.

Weitere Informationen finden Sie unter [Begrenzungsgruppen](../../servers/deploy/configure/boundary-groups.md).


## <a name="network-bandwidth"></a>Netzwerkbandbreite

Zum Verwalten der beim Verteilen von Inhalt verwendeten Menge an Netzwerkbandbreite stehen Ihnen die folgenden Optionen zur Verfügung:  

- **Vorab bereitgestellter Inhalt:** Übertragung von Inhalt an einen Verteilungspunkt, ohne dass Inhalt über das Netzwerk verteilt wird.  

- **Zeitplanung und Bandbreiteneinschränkung:** Konfigurationen, mit denen Sie steuern, wann und wie Inhalt an Verteilungspunkte verteilt wird.  

Weitere Informationen finden Sie unter [Verwalten der Netzwerkbandbreite für Inhalt](manage-network-bandwidth.md).


## <a name="network-connection-speed-to-content-source"></a>Geschwindigkeit der Netzwerkverbindung zur Inhaltsquelle

Einige Dinge haben sich mit Configuration Manager-Current Branch dahingehend geändert, dass Clients einen Verteilungspunkt finden, der Inhalte enthält. Zu den Änderungen gehört z.B. die Netzwerkgeschwindigkeit zu einer Inhaltsquelle.

Netzwerkgeschwindigkeiten die einen Verteilungspunkt als **Schnell** oder **Langsam** definieren, werden nicht mehr verwendet. Stattdessen wird jedes Standortsystem, das einer Begrenzungsgruppe zugeordnet ist, auf die gleiche Weise behandelt.

Weitere Informationen finden Sie unter [Begrenzungsgruppen](../../servers/deploy/configure/boundary-groups.md).


## <a name="on-demand-content-distribution"></a>Bedarfsgesteuerte Inhaltsverteilung

Eine bedarfsgesteuerte Inhaltsverteilung ist eine Option für die individuelle Bereitstellung von Anwendungen und Paketen. Diese Option ermöglicht die bedarfsgesteuerte Inhaltsverteilung an bevorzugte Server.  

- Aktivieren Sie die folgende Option, um diese Einstellung für eine Bereitstellung zu aktivieren: **Den Inhalt für dieses Paket an bevorzugte Verteilungspunkte verteilen**.  

- Wenn Sie diese Option für eine Bereitstellung aktivieren, und ein Client diesen Inhalt anfordert, der Inhalt aber auf den bevorzugten Verteilungspunkten des Clients nicht verfügbar ist, verteilt Configuration Manager diesen Inhalt automatisch an die bevorzugten Verteilungspunkte des Clients.  

- Obwohl dies bewirkt, dass Configuration Manager den Inhalt automatisch an die bevorzugten Verteilungspunkte dieses Clients verteilt, erhält der Client den Inhalt möglicherweise von anderen Verteilungspunkten, bevor die Bereitstellung an die bevorzugten Verteilungspunkte des Clients übertragen wurden. In diesem Fall ist der Inhalt auf diesem Verteilungspunkt anschließend für den nächsten Client verfügbar, der nach der Bereitstellung sucht.  

Weitere Informationen finden Sie unter [Begrenzungsgruppen](../../servers/deploy/configure/boundary-groups.md).


## <a name="package-transfer-manager"></a>Paketübertragungs-Manager

Der Paketübertragungs-Manager ist die Standortserverkomponente, die Inhalt an Verteilungspunkte auf anderen Computern überträgt.  

Weitere Informationen finden Sie unter [Package transfer manager (Paketübertragungs-Manager)](package-transfer-manager.md).  


## <a name="prestage-content"></a>Vorabbereitstellen von Inhalt

Das Vorabbereitstellen von Inhalt ist der Vorgang zum Übertragen von Inhalt an einen Verteilungspunkt, ohne dass der Inhalt im Netzwerk verteilt wird.  

Weitere Informationen finden Sie unter [Verwalten der Netzwerkbandbreite für Inhalt](manage-network-bandwidth.md).
