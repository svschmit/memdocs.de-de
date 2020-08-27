---
title: Optimieren der Bereitstellung von Updates für Windows 10
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Updateinhalte mit Configuration Manager verwalten, um stets auf dem neuesten Stand von Windows 10 zu bleiben.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: b670cfaf-96a4-4fcb-9caa-0f2e8c2c6198
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f16a5736d0bebbcb4f3b03989c6983cd55ac8f54
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696989"
---
# <a name="optimize-windows-10-update-delivery-with-configuration-manager"></a>Optimieren der Bereitstellung von Updates für Windows 10 mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Für viele Kunden ist eine gute Strategie der Verteilung von Inhalten mit dem Configuration Manager der ideale Ansatz, die monatlichen Updates von Windows 10 abzurufen und auf dem Laufenden zu bleiben. Die Größe der monatlichen Qualitätsupdates kann bei großen Unternehmen ein Grund zur Sorge sein. Es gibt einige Technologien zur Reduzierung der Bandbreiten- und Netzwerkbelastung, um die Updatebereitstellung zu optimieren. In diesem Artikel werden diese Technologien erläutert, miteinander verglichen und Empfehlungen angeboten, um Sie bei der Entscheidung, welche Sie verwenden möchten, zu unterstützen.  
 
Windows 10 bietet mehrere Arten von Updates. Weitere Informationen finden Sie unter [Bereitstellen von Updates mit Windows Update for Business](/windows/deployment/update/waas-manage-updates-wufb#types-of-updates-managed-by-windows-update-for-business). Dieser Artikel konzentriert sich auf Windows 10-*Qualitätsupdates* mit Configuration Manager. 


## <a name="express-update-delivery"></a>Expressupdatebereitstellung

Downloads von Windows 10-Qualitätsupdates können sehr groß sein. Jedes Paket enthält alle zuvor veröffentlichten Fehlerbehebungen, um Konsistenz und Einfachheit zu gewährleisten. Microsoft konnte die Größe des Windows 10-Updateinhalts, die jeder Client herunterlädt, mit dem Express-Feature reduzieren. Express wird heutzutage von Millionen von Geräten verwendet, die Updates direkt vom Windows Update-Dienst abrufen, und verringert die Downloadgröße erheblich. Diesen Vorteil können auch Kunden nutzen, deren Clients nicht direkt vom Windows Update-Dienst herunterladen. 

Seit Version 1702 unterstützt Configuration Manager [Expressinstallationsdateien](manage-express-installation-files-for-windows-10-updates.md) von Windows 10-Qualitätsupdates. Um optimale Ergebnisse zu erzielen, sollten Sie Configuration Manager Version 1802 oder höher verwenden. Um die beste Downloadgeschwindigkeit zu erzielen, sollten Sie auch Windows 10, Version 1703 oder höher verwenden. 

> [!NOTE]  
> Der Inhalt der Expressversion ist erheblich größer als die vollständige Dateiversion. Eine Expressinstallationsdatei enthält alle möglichen Variationen für jede Datei, die aktualisiert werden soll. Darum ist in der Updatepaketquelle und auf Verteilungspunkten mehr Speicherplatz auf dem Datenträger für Updates erforderlich, wenn Sie die Expressunterstützung im Configuration Manager aktivieren. Obwohl der Bedarf an Speicherplatz auf dem Datenträger auf den Verteilungspunkten ansteigt, verringert sich die Größe der Inhalte, die Clients von diesen Verteilungspunkten herunterladen. Clients laden nur die Bits herunter, die sie benötigen (Deltas), jedoch nicht das gesamte Update.


## <a name="peer-to-peer-content-distribution"></a>Peer-zu-Peer-Inhaltsverteilung

Obwohl Clients nur die Teile des Inhalts herunterladen, die sie benötigen, werden Windows-Updates in Ihrer Umgebung durch Verwendung der Peer-zu-Peer-Inhaltsverteilung beschleunigt. Die Nutzung von Peers als Downloadquelle für Qualitätsupdates kann in Umgebungen vorteilhaft sein, in denen Remotebüros nicht über lokale Verteilungspunkte verfügen. Dieses Verhalten verhindert, dass alle Clients Inhalt über eine langsame WAN-Verbindung von einem Remoteverteilungspunkt herunterladen müssen. Der Einsatz von Peers kann auch hilfreich sein, wenn Clients auf den Windows Update-Dienst ausweichen. Nur ein Peer ist erforderlich, um Updateinhalt aus der Cloud herunterzuladen, bevor er anderen Geräten verfügbar gemacht wird.

Configuration Manager unterstützt viele Peer-zu-Peer-Technologien einschließlich der folgenden:
- Windows-Übermittlungsoptimierung
- Configuration Manager-Peercache
- Windows BranchCache  

Die nächsten Abschnitte bieten weitere Informationen zu diesen Technologien.

### <a name="windows-delivery-optimization"></a>Windows-Übermittlungsoptimierung

[Übermittlungsoptimierung](/windows/deployment/update/waas-delivery-optimization) ist die wichtigste in Windows 10 integrierte Downloadtechnologie und Peer-zu-Peer-Verteilungsmethode. Windows 10-Clients können Inhalt von anderen Geräten in ihrem lokalen Netzwerk abrufen, die dieselben Updates herunterladen. Mithilfe der [für die Übermittlungsoptimierung verfügbaren Windows-Optionen](/windows/deployment/update/waas-delivery-optimization-reference#delivery-optimization-options) können Sie Clients in Gruppen konfigurieren. Diese Gruppierung ermöglicht Ihrer Organisation, Geräte zu identifizieren, die möglicherweise die besten Kandidaten zum Erfüllen der Peer-zu-Peer-Anforderungen sind. Übermittlungsoptimierung reduziert deutlich die gesamte Bandbreite, die verwendet wird, um Geräte auf dem neuesten Stand zu halten, während die Downloadzeit verringert wird.

> [!NOTE]  
> Die Übermittlungsoptimierung ist eine in der Cloud verwaltete Lösung. Der Internetzugriff auf den Clouddienst Übermittlungsoptimierung ist eine Anforderung für den Einsatz der Peer-zu-Peer-Funktionalität. Informationen zu den erforderlichen Internetendpunkten finden Sie unter [Häufig gestellte Fragen zur Übermittlungsoptimierung](/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions). 

Um beste Ergebnisse zu erzielen, müssen Sie möglicherweise den [Downloadmodus](/windows/deployment/update/waas-delivery-optimization-reference#download-mode) der Übermittlungsoptimierung auf **Gruppe (2)** festlegen und *Gruppen-IDs* definieren. Im Gruppenmodus kann das Peering interne Subnetze zwischen Geräten überschreiten, die zur selben Gruppe gehören, Geräte in Remotebüros inbegriffen. Verwenden Sie die [Gruppen-ID-Option](/windows/deployment/update/waas-delivery-optimization-reference#select-the-source-of-group-ids), um Ihre eigene benutzerdefinierte Gruppe unabhängig von Domänen und AD DS-Standorten zu erstellen. Der Downloadmodus „Gruppe“ wird den meisten Organisationen empfohlen, die die beste Bandbreitenoptimierung mit Übermittlungsoptimierung anstreben.

Die manuelle Konfiguration dieser Gruppen-IDs ist schwierig, wenn Clients zwischen verschiedenen Netzwerken wechseln. Seit Version 1802 verfügt Configuration Manager über ein neues Feature, das die Verwaltung dieses Prozesses durch [die Integration von Begrenzungsgruppen mit Übermittlungsoptimierung](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization) vereinfacht. Wenn ein Client reaktiviert wird, kommuniziert er mit seinem Verwaltungspunkt, um Richtlinien abzurufen, und stellt seine Netzwerk- und Begrenzungsgruppeninformationen bereit. Configuration Manager erstellt für jede Begrenzungsgruppe eine eindeutige ID. Der Standort verwendet die Speicherortinformationen des Clients, um automatisch die Übermittlungsoptimierungs-Gruppen-ID des Clients mit der Configuration Manager-Begrenzungsgruppen-ID zu konfigurieren. Wenn der Client zu einer anderen Begrenzungsgruppe wechselt, kommuniziert er mit seinem Verwaltungspunkt und wird automatisch mit einer neuen Begrenzungsgruppen-ID neu konfiguriert. Mit dieser Integration kann die Übermittlungsoptimierung die Begrenzungsgruppeninformationen von Configuration Manager nutzen, um einen Peer zum Herunterladen von Updates zu finden.

### <a name="delivery-optimization-starting-in-version-1910"></a><a name="bkmk_DO-1910"></a> Übermittlungsoptimierung ab Version 1910
<!--4699118-->
Ab Configuration Manager Version 1910 können Sie die Übermittlungsoptimierung für die Verteilung aller Windows Update-Inhalte für Clients mit Windows 10, Version 1709 oder höher, und nicht nur für Express-Installationsdateien verwenden.

Um die Übermittlungsoptimierung für alle Windows Update-Installationsdateien zu verwenden, aktivieren Sie die folgenden [Clienteinstellungen für Softwareupdates](../../core/clients/deploy/about-client-settings.md#software-updates):

- **Clients das Herunterladen von Deltainhalten ermöglichen (falls verfügbar):** Festlegen auf **Ja**
- **Port, die Clients zum Empfangen von Anforderungen für Deltainhalte erhalten:** Festlegen auf 8005 (Standard) oder einen benutzerdefinierten Port
 
> [!IMPORTANT]
> - Die Übermittlungsoptimierung muss aktiviert sein (Standard) und darf nicht umgangen werden. Weitere Informationen finden Sie in der [Referenz zur Windows-Übermittlungsoptimierung](/windows/deployment/update/waas-delivery-optimization-reference).
> - Überprüfen Sie die [Clienteinstellungen für die Übermittlungsoptimierung](../../core/clients/deploy/about-client-settings.md#delivery-optimization), wenn Sie für Deltainhalte die [Clienteinstellungen für Softwareupdates](../../core/clients/deploy/about-client-settings.md#software-updates) ändern.
> - Die Übermittlungsoptimierung kann für Microsoft 365-Apps-Clientupdates verwendet werden, wenn Office COM aktiviert ist. Office COM wird von Configuration Manager verwendet, um Updates für Microsoft 365-Apps-Clients zu verwalten. Sie können die Registrierung von Office COM aufheben, um die Verwendung der Übermittlungsoptimierung für Microsoft 365-Apps-Updates zuzulassen. Wenn Office COM deaktiviert ist, werden Softwareupdates für Microsoft 365-Apps VOM standardmäßigen geplanten Task „Automatische Office-Updates 2.0“ verwaltet. Das bedeutet, dass Configuration Manager den Installationsprozess für Microsoft 365-Apps-Updates weder vorschreibt noch überwacht. Configuration Manager sammelt weiterhin Informationen aus dem Hardwarebestand, um das Dashboard für die Office 365-Clientverwaltung in der Konsole aufzufüllen. Informationen zum Aufheben der Registrierung von Office COM finden Sie unter [Aktivieren von Office 365-Clients für den Erhalt von Updates vom Office CDN anstatt von Configuration Manager](/deployoffice/manage-office-365-proplus-updates-with-configuration-manager#enable-office-365-clients-to-receive-updates-from-the-office-cdn-instead-of-configuration-manager).
> - Bei der Verwendung eines CMG zum Speichern von Inhalten werden die Inhalte für Updates für Drittanbietersoftware nicht auf Clients heruntergeladen, wenn die [Clienteinstellung](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) **Clients das Herunterladen von Deltainhalten ermöglichen (falls verfügbar)** aktiviert ist. <!--6598587-->

#### <a name="configuration-recommendations-for-clients-downloading-delta-content"></a>Konfigurationsempfehlungen für Clients, die Deltainhalte herunterladen
<!--7913814-->
Wenn die [Clienteinstellung](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) **Clients das Herunterladen von Deltainhalten ermöglichen (falls verfügbar)** auf Clients für Inhalte von Softwareupdates aktiviert ist, gelten [Einschränkungen für das Fallbackverhalten von Verteilungspunkten](../../core/servers/deploy/configure/boundary-group-procedures.md#bkmk_site-fallback). Um sicherzustellen, dass diese Clients Inhalte von Softwareupdates ordnungsgemäß herunterladen können, empfehlen wir die folgenden Konfigurationen:

- Stellen Sie sicher, dass sich Clients in einer Begrenzungsgruppe befinden und es einen zuverlässigen Verteilungspunkt gibt, der die benötigten Inhalte dieser Begrenzungsgruppe zugeordnet hat.
- Stellen Sie Softwareupdates mit aktiviertem Fallback zu Microsoft Update für Clients bereit, die Inhalte über das Internet direkt herunterladen können.
   - Die Bereitstellungseinstellung für dieses Fallbackverhalten ist **Inhalt von Microsoft Updates herunterladen, falls Softwareupdates in aktuellen oder benachbarten Begrenzungsgruppen oder in Standortbegrenzungsgruppen am Verteilungspunkt nicht verfügbar sind** auf der Seite **Downloadeinstellungen**. Weitere Informationen finden Sie unter [Bereitstellen von Softwareupdates](manually-deploy-software-updates.md#process-to-manually-deploy-the-software-updates-in-a-software-update-group).

Wenn keine der oben genannten Optionen in Frage kommt, kann **Clients das Herunterladen von Deltainhalten ermöglichen (falls verfügbar)** in den Clienteinstellungen deaktiviert werden, um Fallbackfunktionalität zu ermöglichen. Ein Peering des Typs „Übermittlungsoptimierung“ wird in diesem Fall nicht genutzt, da der Client nicht den Deltakanal verwendet.

### <a name="configuration-manager-peer-cache"></a>Configuration Manager-Peercache

Der [Peercache](../../core/plan-design/hierarchy/client-peer-cache.md) ist ein Feature von Configuration Manager, mit dessen Hilfe Clients Inhalte direkt aus ihrem lokalen Configuration Manager-Cache freigeben können. Peercache ersetzt nicht die Verwendung anderer Peer-Zwischenspeicherlösungen wie Windows BranchCache. Mit ihnen zusammen bietet der Peercache mehr Optionen für das Erweitern herkömmlicher Lösungen für die Inhaltsbereitstellung, wie z.B. Verteilungspunkte. Peercache ist nicht von BranchCache abhängig. Sie können den Peercache kann auch dann verwenden, wenn Sie BranchCache nicht aktivieren oder nutzen.

> [!NOTE]  
> Clients können nur Inhalte von Peercacheclients herunterladen, die sich in ihrer aktuellen Begrenzungsgruppe befinden.  


### <a name="windows-branchcache"></a>Windows BranchCache
[BranchCache](/windows-server/networking/branchcache/branchcache) ist eine Technologie zur Optimierung der Bandbreite in Windows. Jeder Client verfügt über einen Cache und fungiert als alternative Quelle für Inhalte. Geräte, die sich im selben Netzwerk befinden, können diese Inhalte anfordern. Der [Configuration Manager kann BranchCache verwenden](../../core/plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache), um Peers zu ermöglichen, einander als Inhaltsquelle zu nutzen, anstatt stets mit einem Verteilungspunkt Kontakt aufnehmen zu müssen. Mit BranchCache werden Dateien auf jedem einzelnen Client zwischengespeichert, und andere Clients können je nach Bedarf abgerufen werden. Bei diesem Ansatz wird der Cache verteilt, anstatt dass ein einzelner Abrufpunkt vorliegt. Dieses Verhalten spart eine beträchtliche Menge an Bandbreite ein und bewirkt, dass Clients schneller den angeforderten Inhalt empfangen.



## <a name="selecting-the-right-peer-caching-technology"></a>Auswählen der richtigen Peercachingtechnologie

Die Auswahl der richtigen Peercachingtechnologie für Expressinstallationsdateien hängt von Ihrer Umgebung und den Anforderungen ab. Obwohl Configuration Manager alle oben genannten Peer-zu-Peer-Technologien unterstützt, sollten Sie diejenige verwenden, die in Ihrer Umgebung am sinnvollsten ist. Vorausgesetzt, dass Clients die Internetanforderungen für die Übermittlungsoptimierung erfüllen können, sollte das in Windows 10 integrierte Peercaching mit Übermittlungsoptimierung für die meisten Kunden ausreichend sein. Wenn Ihre Clients diese Internetanforderungen nicht erfüllen können, sollten Sie die Verwendung des Peercachefeatures von Configuration Manager in Betracht ziehen. Wenn Sie derzeit BranchCache mit Configuration Manager einsetzen und damit alle Ihre Anforderungen erfüllt werden, sind Expressdateien mit BranchCache möglicherweise die richtige Option für Sie. 

### <a name="peer-cache-comparison-chart"></a>Vergleichsdiagramm für Peercache


| Funktionalität  | Übermittlungsoptimierung  | Peercache  | BranchCache  |
|---------|---------|---------|---------|
| Über Subnetze hinweg unterstützt | Ja | Ja | Nein |
| Bandbreiteneinschränkung | Ja (nativ) | Ja (über BITS) | Ja (über BITS) |
| Unterstützung von Teilinhalt | Ja, für alle unterstützten Inhaltstypen, die in der nächsten Zeile dieser Spalte aufgeführt sind. | Nur für Microsoft 365-Apps- und Express-Updates | Ja, für alle unterstützten Inhaltstypen, die in der nächsten Zeile dieser Spalte aufgeführt sind. |
| Unterstützte Inhaltstypen | **Über ConfigMgr:** </br> Express-Updates </br> Alle Windows-Updates (ab Version 1910). Microsoft 365-Apps-Updates sind nicht eingeschlossen.</br> </br> **Über Microsoft Cloud:**</br> – Windows- und Sicherheitsupdates</br> – Treiber</br> – Windows Store-Apps</br> – Apps aus Microsoft Store für Unternehmen | Alle Configuration Manager-Inhaltstypen einschließlich der in [Windows PE](../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md) heruntergeladenen Images | Alle Configuration Manager-Inhaltstypen mit Ausnahme von Images |
| Steuerung der Cachegröße auf dem Datenträger | Ja | Ja | Ja |
| Ermittlung einer Peerquelle | Automatisch | Manuell (Client-Agent-Einstellung) | Automatisch |
| Peerermittlung | Über Übermittlungsoptimierung-Clouddienst (erfordert Internetzugriff) | Über einen Verwaltungspunkt (basierend auf Clientbegrenzungsgruppen) | Multicast |
| Berichterstellung | Ja (mithilfe von Desktop Analytics) | Dashboard zu Clientdatenquellen im Configuration Manager | Dashboard zu Clientdatenquellen im Configuration Manager |
| Steuerung der WAN-Nutzung | Ja (nativ, kann über Gruppenrichtlinieneinstellungen gesteuert werden) | Begrenzungsgruppen | Nur Subnetzunterstützung |
| Verwaltung durch Configuration Manager | Partiell (Client-Agent-Einstellung) | Ja (Client-Agent-Einstellung) | Ja (Client-Agent-Einstellung) |



## <a name="conclusion"></a>Zusammenfassung

Microsoft empfiehlt Ihnen, die Bereitstellung von Windows 10-Qualitätsupdates mit Configuration Manager je nach Bedarf mit Expressinstallationsdateien und Peercachingtechnologie zu optimieren. Dieser Ansatz sollte den Herausforderungen beim Herunterladen von umfangreichen Inhalten für die Installation von Qualitätsupdates mit Windows 10-Geräten gerecht werden. Außerdem sollten Sie Windows 10-Geräte durch die allmonatliche Bereitstellung von Qualitätsupdates auf dem neuesten Stand halten. Diese Vorgehensweise verringert das Delta des Qualitätsupdateinhalts, das Geräte jeden Monat benötigen. Aus der Reduzierung dieses Inhaltsdeltas resultieren kleinere Downloads von Verteilungspunkten oder Peerquellen. 

Aufgrund der Art der Expressinstallationsdateien übersteigt die Größe ihres Inhalts die Größe des herkömmlichen eigenständigen Dateiinhalts erheblich. Diese Größe verlängert das Herunterladen des Updates vom Windows Update-Dienst auf den Configuration Manager-Standortserver. Der Bedarf an Speicherplatz auf dem Datenträger sowohl des Standortservers als auch der Verteilungspunkte steigt ebenfalls. Die zum Herunterladen und Verteilen von Qualitätsupdates erforderliche Gesamtzeit könnte länger sein. Allerdings dürften die Vorteile auf der Geräteseite während des Downloads und der Installation von Qualitätsupdates durch Windows 10-Geräte deutlich erkennbar sein. Weitere Informationen finden Sie unter [Verwenden von Express-Installationsdateien](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc708456(v=ws.10)#using-express-installation-files).

Wenn die serverseitigen Vor- und Nachteile größerer Updates Hindernisse bei der Einführung der Expressunterstützung darstellen, die geräteseitigen Vorteile aber für Ihr Unternehmen und Ihre Umgebung ausschlaggebend sind, empfiehlt Microsoft Ihnen, [Windows Update for Business](integrate-windows-update-for-business-windows-10.md) mit Configuration Manager zu verwenden. Windows Update for Business bietet alle Vorteile von Express ohne die Notwendigkeit, Expressinstallationsdateien in Ihrer gesamten Umgebung herunterladen, speichern und verteilen zu müssen. Clients laden Inhalte direkt vom Windows Update-Dienst herunter und können weiterhin die Übermittlungsoptimierung verwenden.



## <a name="frequently-asked-questions"></a><a name="bkmk_faq"></a> Häufig gestellte Fragen

#### <a name="how-do-windows-express-downloads-work-with-configuration-manager"></a>Wie funktionieren Windows-Expressdownloads in Verbindung mit Configuration Manager?

Der Windows Update-Agent (WUA) fordert zuerst Expressinhalt an. Wenn er das Expressupdate nicht installieren kann, kann er auf das vollständige Dateiupdate zurückgreifen.  

1. Der Configuration Manager-Client weist den WUA an, den Inhalt des Updates herunterzuladen. Wenn WUA einen Expressdownload initiiert, wird zuerst ein Stub (z.B. `Windows10.0-KB1234567-<platform>-express.cab`) heruntergeladen, der Teil des Expresspakets ist.  

2. WUA übergibt diesen Stub an das Windows-Updateinstallationsprogramm, komponentenbasierte Wartung (Component-Based Servicing, CBS). CBS verwendet den Stub für eine lokale Inventur und vergleicht die Deltas der Datei auf dem Gerät mit dem, was benötigt wird, um auf die aktuell angebotene Version der Datei zu aktualisieren.  

3. Anschließend fordert CBS den WUA auf, die erforderlichen Bereiche aus einer oder mehreren PSF-Expressdateien herunterzuladen.  

4. Wenn die Übermittlungsoptimierung aktiviert ist und festgestellt wird, dass die Peers über die erforderlichen Bereiche verfügen, lädt der Client unabhängig vom ConfigMgr-Client von den Peers herunter. Wenn die Übermittlungsoptimierung deaktiviert ist oder keine Peers über die erforderlichen Bereiche verfügen, lädt der ConfigMgr-Client diese Bereiche von einem lokalen Verteilungspunkt (oder einem Peer oder Microsoft Update) herunter. Die Bereiche werden an den Windows Update-Agent übermittelt, sodass sie für CBS verfügbar sind, um die Bereiche anzuwenden.


#### <a name="why-are-the-express-files-psf-so-large-when-stored-on-configuration-manager-peer-sources-in-the-ccmcache-folder"></a>Warum sind die PSF-Expressdateien so groß, wenn sie auf Configuration Manager-Peerquellen im Ordner „ccmcache“ gespeichert werden?

Die PSF-Expressdateien sind platzsparende Dateien. Um zu bestimmen, wieviel Speicherplatz die Datei auf dem Datenträger benötigt, aktivieren Sie die Eigenschaft **Größe auf Datenträger** der Datei. Die Eigenschaft „Größe auf Datenträger“ sollte erheblich kleiner sein als der Wert für „Größe“.  


#### <a name="does-configuration-manager-support-express-installation-files-with-windows-10-feature-updates"></a>Unterstützt Configuration Manager Expressinstallationsdateien mit Windows 10-Feature-Updates?

Nein, Configuration Manager unterstützt derzeit nur Expressinstallationsdateien mit Windows 10-Qualitätsupdates.  


#### <a name="how-much-disk-space-is-needed-per-quality-update-on-the-site-server-and-distribution-points"></a>Wie viel Speicherplatz auf dem Datenträger ist pro Qualitätsupdate auf dem Standortserver und den Verteilungspunkten erforderlich?

Das kommt auf den Datentyp an. Für jedes Qualitätsupdate wird sowohl die vollständige als auch die Expressversion des Updates auf den Servern gespeichert. Qualitätsupdates für Windows 10 sind kumulativ, d.h. die Größe dieser Dateien nimmt von Monat zu Monat zu. Planen Sie mindestens 5 GB pro Update und Sprache ein. 


#### <a name="do-configuration-manager-clients-still-benefit-from-express-installation-files-when-falling-back-to-the-windows-update-service"></a>Profitieren Configuration Manager-Clients auch dann noch von Expressinstallationsdateien, wenn sie wieder auf den Windows Update-Dienst zurückgreifen?

Ja. Wenn Sie die folgende Option zur Bereitstellung von Softwareupdates nutzen, verwenden Clients weiterhin Expressupdates und Übermittlungsoptimierung, wenn sie wieder auf den Clouddienst zurückgreifen:  

**Falls Softwareupdates am Verteilungspunkt nicht in aktuellen, benachbarten oder Standortgruppen verfügbar sind, Inhalt von Microsoft Updates herunterladen**


#### <a name="why-is-express-file-content-not-downloaded-for-existing-updates-after-i-enable-express-file-support"></a>Warum wird Expressdateiinhalt nicht für vorhandene Updates heruntergeladen, nachdem ich Expressdateiunterstützung aktiviert habe? 

Die Änderungen wirken sich nur auf neue Updates aus, die nach dem Aktivieren der Unterstützung synchronisiert und bereitgestellt werden.


#### <a name="is-there-any-way-to-see-how-much-content-is-downloaded-from-peers-using-delivery-optimization"></a>Gibt es die Möglichkeit, festzustellen, wie viel Inhalt von Peers mithilfe der Optimierung der Übermittlung heruntergeladen wird?
Windows 10, Version 1703 (und höher) enthält zwei neue PowerShell-Cmdlets, **Get-DeliveryOptimizationPerfSnap** und **Get-DeliveryOptimizationStatus**. Diese Cmdlets bieten mehr Einblick in Übermittlungsoptimierung und Cachenutzung. Weitere Informationen finden Sie unter [Übermittlungsoptimierung für Windows 10-Updates](/windows/deployment/update/waas-delivery-optimization#the-cloud-service-doesnt-see-other-peers-on-the-network).


#### <a name="how-do-clients-communicate-with-delivery-optimization-over-the-network"></a>Wie kommunizieren Clients mit der Übermittlungsoptimierung über das Netzwerk?
Weitere Informationen zu Netzwerkports, Proxyanforderungen und Hostnamen für Firewalls finden Sie unter [Häufig gestellte Fragen](/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions).

## <a name="log-files"></a>Protokolldateien

Verwenden Sie die folgenden Protokolldateien, um Downloads von Deltas zu überwachen:

- WUAHandler.log
- DeltaDownload.log

## <a name="next-steps"></a>Nächste Schritte

- [Bereitstellen von Softwareupdates](deploy-software-updates.md)
- [Automatisches Bereitstellen von Softwareupdates](automatically-deploy-software-updates.md)