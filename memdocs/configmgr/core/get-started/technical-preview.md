---
title: Technical Preview-Releases
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über den Technical Preview-Branch, mit dem Sie neue Funktionen und Fähigkeiten in Configuration Manager testen können.
ms.date: 09/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a27cd1e7a28b52ccc224f965b678d7d578be75eb
ms.sourcegitcommit: dc2cca9eb70aef15037e8f7d18d671c513bfde85
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/14/2020
ms.locfileid: "90081738"
---
# <a name="technical-preview-for-configuration-manager"></a>Technical Preview für Configuration Manager

*Gilt für: Configuration Manager (Technical Preview-Branch)*

Dieser Artikel enthält Details zum monatlich zur Verfügung gestellten Technical Preview-Branch von Configuration Manager. In der Technical Preview werden neue Funktionen veröffentlicht, an denen Microsoft zurzeit arbeitet. Es werden neue Features veröffentlicht, die noch nicht in Current Branch von Configuration Manager enthalten sind. Diese Features werden möglicherweise zu einem späteren Zeitpunkt in ein Update für Current Branch eingefügt. Vor der Fertigstellung dieser Features möchten wir, dass Sie diese testen und uns Ihr Feedback mitteilen.

Da es sich bei diesem Release um eine Technical Preview handelt, können Details und Funktionen noch Änderungen unterliegen.

Diese Informationen gelten für alle Versionen des Technical Preview-Branch von Configuration Manager. In diesem Artikel werden alle neuen Features mit der Technical Preview-Version aufgelistet, in der diese zuerst eingeführt werden. Beispiel: Version **2001** für Januar (`01`) 2020 (`20`). Die einzelnen Features werden in separaten Artikeln zu den einzelnen Vorschauversion erläutert.

Informationen zu den Neuigkeiten zu *Current Branch* von Configuration Manager finden Sie unter [Neuigkeiten zu inkrementellen Configuration Manager-Versionen](../plan-design/changes/whats-new-incremental-versions.md).

> [!Tip]
> Um bei einer Aktualisierung dieser Seite benachrichtigt zu werden, kopieren Sie die folgende URL, und fügen Sie sie in Ihren RSS-Feedreader ein: `https://docs.microsoft.com/api/search/rss?search=%22technical+preview+releases+-+Configuration+Manager%22&locale=en-us`

## <a name="requirements-and-limitations"></a><a name="bkmk_reqs"></a> Anforderungen und Einschränkungen

> [!IMPORTANT]
> Die Technical Preview-Version ist ausschließlich für die Verwendung in einer Laborumgebung lizenziert. Microsoft bietet möglicherweise keinen Support, und bestimmte Features sind in Technical Previews möglicherweise nicht verfügbar. Darüber hinaus gelten bei Technical Previews im Vergleich zu im Handel erhältlicher Software möglicherweise eingeschränkte oder veränderte Standards in Bezug auf Sicherheit, Datenschutz, Barrierefreiheit, Verfügbarkeit und Zuverlässigkeit.

Informationen zu den meisten Produktvoraussetzungen finden Sie unter [Unterstützte Konfigurationen für System Center Configuration Manager](../plan-design/configs/supported-configurations.md). Für den Technical Preview-Branch gelten folgende Ausnahmen:

- Jede Installation wird nach 90 Tagen deaktiviert.

- Englisch ist die einzige unterstützte Sprache.

- Er unterstützt nur die folgenden Setup-Befehlszeilenparameter:

  - `/silent`
  - `/testdbupgrade`

- Der Dienstverbindungspunkt wird im Onlinemodus installiert. Der Offlinemodus wird nicht unterstützt.

- Die zusätzlichen Artikel zu den einzelnen Versionen der Technical Preview umfassen ggf. zusätzliche Einschränkungen und Anforderungen.

- Die folgenden Features werden nicht beim Technical Preview-Branch unterstützt:

  - [Migration](../migration/migrate-data-between-hierarchies.md) zu oder aus diesem Preview-Branch

  - [Upgrade](../servers/deploy/install/upgrade-to-configuration-manager.md) auf diesen Preview-Branch

  - [Standortwiederherstellung](../servers/manage/recover-sites.md) aus dem Ordner „cd.latest“<!--507106-->

- Das Update dieses Preview-Branch auf Current Branch wird nicht unterstützt.

    > [!Note]
    > Wenn Updates für eine Vorschauversion verfügbar sind, finden Sie diese nach wie vor im Knoten **Updates und Wartung** der Configuration Manager-Konsole, von wo aus Sie sie installieren können. Ein Video zum Upgradeprozess über die Konsole finden Sie unter [Installieren von Configuration Manager-Updatepaketen](https://www.youtube.com/embed/KBd_EGFbUT8) auf „youtube.com“.

- Nur eigenständige primäre Standorte werden unterstützt. Standorte der zentralen Verwaltung, mehrere primäre Standorte oder sekundäre Standorte werden nicht unterstützt.

Der Technical Preview-Branch von Configuration Manager unterstützt die folgenden Produkte und Technologien:

- Sofern nicht anders angegeben, unterstützt der Technical Preview-Branch dieselben Versionen von SQL Server wie Current Branch. Weitere Informationen finden Sie unter [Unterstützte SQL Server-Versionen](../plan-design/configs/support-for-sql-server-versions.md).

- Dieser Standort unterstützt bis zu 10 Clients, auf denen jede [unterstützte Clientbetriebssystemversion](../plan-design/configs/supported-operating-systems-for-clients-and-devices.md) ausgeführt werden kann.<!-- SCCMDocs#1656 -->

> [!Note]
> Die Einbeziehung dieser Produkte in diesen Inhalten bedeutet nicht, dass die Unterstützung für eine Version, deren Supportlebenszyklus überschritten ist, erweitert wird. Configuration Manager unterstützt keine Produkte, deren Supportlebenszyklus überschritten ist. Weitere Informationen finden Sie unter [Microsoft-Lebenszyklusrichtlinie](https://support.microsoft.com/lifecycle).

## <a name="install-and-update"></a><a name="bkmk_install"></a> Installieren und Aktualisieren

Der Technical Preview-Branch von Configuration Manager für Labs unterscheidet sich von Current Branch von Configuration Manager für die Produktion.

Installieren Sie zunächst eine Baselineversion des Technical Preview-Branch. Nach der Installation einer Baselineversion können Sie Ihre Installation mithilfe konsoleninterner Updates auf den neuesten Stand der aktuellen Preview-Version bringen. In der Regel werden neue Technical Preview-Versionen jeden Monat zur Verfügung gestellt.

Microsoft unterstützt bis zu drei aufeinander folgende Technical Preview-Versionen. Wenn zum Beispiel Version 1908 veröffentlicht wurde, wird die Version 1904 nicht mehr unterstützt. Die Versionen 1905, 1906 und 1907 werden hingegen weiterhin unterstützt. Wenn eine Baselineversion nicht mehr unterstützt wird, wird weiterhin die Installation eines neuen Technical Preview-Standorts unterstützt, vorausgesetzt, Sie führen umgehend ein Update auf eine unterstützte Version durch. Die ältere Baseline wird unterstützt, bis eine neue Baselineversion verfügbar ist. Führen Sie ein Update auf die neuste verfügbare Baselineversion aus, und wiederholen Sie den Updatevorgang dann solange, bis die neuste Technical Preview-Version installiert ist.

> [!TIP]
> Bei der Installation eines Updates für die Technical Preview-Version wird Ihre Installation auf die jeweils neueste Technical Preview-Version aktualisiert. Eine Technical Preview-Installation bietet nie die Möglichkeit eines Upgrades auf eine Current Branch-Installation. Zudem erhält sie keine Updates vom Current Branch-Release.
>
> Mehrmals im Jahr werden Technical Preview-Branch- und Current Branch-Versionen mit derselben Versionsnummer veröffentlicht. Beispielsweise gibt es die Technical Preview-Version 1910 und die Current Branch-Version 1910.

### <a name="active-baseline-versions"></a>Aktive Baselineversionen

Installieren Sie Baselineversionen bis zu ein Jahr nach deren Veröffentlichung. Verwenden Sie die neueste Baselineversion, wenn Sie einen neuen Technical Preview-Standort installieren. Die folgenden Technical Preview-Branchversionen für Configuration Manager werden als konsoleninterne Updates und als neue Baselineversionen zur Verfügung gestellt:

- **Technical Preview, Version 2007**

Laden Sie eine Baselineversion über das [Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview) herunter.

## <a name="providing-feedback"></a><a name="BKMK_TPFeedback"></a> Übermitteln von Feedback

Wir würden uns über Ihr Feedback zu den neuen Features der Technical Preview freuen. Weitere Informationen finden Sie unter [Produktfeedback](../understand/find-help.md#product-feedback).

Außerdem interessieren uns Ihre Ideen zu neuen Funktionen, die Sie in Zukunft gerne nutzen möchten. Teilen Sie uns diese gerne mit. Übermitteln Sie neue Ideen, und stimmen Sie über die Ideen anderer ab: [Configuration Manager UserVoice](https://configurationmanager.uservoice.com)

<!--
## <a name="bdmk_tpknownissues"></a> General changes introduced in technical preview branch

<!-- (explanatory comment)
Enable this section if needed to include any broad change to the tech preview branch
-->

## <a name="features-in-the-most-recent-version"></a><a name="bkmk_tpCaps"></a> Features in der neuesten Version

<!-- (explanatory comment)
This is the full list of new features in the latest TP release

bullet format:
<!-- - [title](2020/technical-preview-2009.md) <!--ID-->

Nachfolgend sind die Features der neusten Technical Preview-Versionen für Configuration Manager dargestellt:

### <a name="technical-preview-version-2009"></a>Technical Preview, Version 2009

- [Cloud Management Gateway mit VM Scale Set](2020/technical-preview-2009.md#bkmk_cmgvmss) <!--3601040-->
- [ Verbesserungen an der Remotesteuerung](2020/technical-preview-2009.md#bkmk_remctrl) <!--4575930-->
- [Bereitstellen eines Betriebssystems über CMG mithilfe von Startmedien](2020/technical-preview-2009.md#bkmk_osdcmg) <!--3555923-->
- [Anzeigen von Sammlungsbeziehungen](2020/technical-preview-2009.md#bkmk_coll) <!--3608121-->
- [Aktivieren des Computers am Bereitstellungsstichtag mithilfe der Peeraktivierung](2020/technical-preview-2009.md#bkmk_wol) <!--3734819-->
- [Verbesserungen bei Benachrichtigungen in der Konsole](2020/technical-preview-2009.md#bkmk_notifications) <!--7410221-->
- [Benachrichtigungen für Geräte, die keine Updates mehr erhalten](2020/technical-preview-2009.md#bkmk_patch) <!--7520646-->
- [Verbesserte Funktionalität des Windows Server-Neustarts für Nicht-Administratorkonten](2020/technical-preview-2009.md#bkmk_server) <!--7821529-->
- [Verbesserungen bei der Bereitstellung von Betriebssystemen](2020/technical-preview-2009.md#bkmk_osd) <!--7799892,7068388-->

> [!NOTE]
> Features, die in einer Vorgängerversion der Technical Preview verfügbar waren, bleiben auch in späteren Versionen enthalten. Ebenso bleiben Features, die Current Branch von Configuration Manager hinzugefügt wurden, in weiteren Branches der Technical Preview enthalten.

## <a name="features-in-recent-technical-previews"></a>Features in aktuellen Technical Preview-Versionen

<!-- (explanatory comment)
This is the full list of new features in the past TP releases since the last CB release.
Each month, add features from the list above to a new H3 section at the top of this section.
When there's a new CB, add any features not in that CB to the table in H2 "Features in previous technical previews"
-->

Die folgenden Features wurden in früheren Versionen des Technical Preview-Branchs für Configuration Manager seit der Current Branch-Version 2006 veröffentlicht:

> [!TIP]
> Sobald ein neues Current Branch-Release verfügbar ist, werden die in dieser Version verfügbaren Features im aktuellen Artikel mit *Neuerungen* aufgeführt. Weitere Informationen finden Sie unter den [Neuigkeiten zu inkrementellen Versionen](../plan-design/changes/whats-new-incremental-versions.md#supported-versions).

### <a name="technical-preview-version-2008"></a>Technical Preview, Version 2008

- [Sammlungsabfrage – Vorschau](2020/technical-preview-2008.md#collection-query-preview) <!--7380401-->
- [Analysieren von SetupDiag-Fehlern für Featureupdates](2020/technical-preview-2008.md#bkmk_setupdiag) <!--4385028-->
- [Überwachen der Szenariointegrität](2020/technical-preview-2008.md#bkmk_health) <!--7699463-->
- [Ansicht der Sammlungsauswertung](2020/technical-preview-2008.md#bkmk_colleval) <!--6251274-->
- [Anzeigen der Größe einer Tasksequenz in der Konsole](2020/technical-preview-2008.md#bkmk_tssize) <!--7645732-->
- [Task „Veraltete gesammelte Dateien löschen“](2020/technical-preview-2008.md#bkmk_logs) <!--6503308-->
- [Importieren von Objekten in den aktuellen Ordner](2020/technical-preview-2008.md#bkmk_folder) <!--6601203-->

### <a name="technical-preview-version-2007"></a>Technical Preview, Version 2007

- [Mandantenanfügung: Anzeigen des Hardwarebestands in Microsoft Endpoint Manager Admin Center](2020/technical-preview-2007.md#bkmk_mem) <!--6479284-->
- [Verbesserungen am Dashboard „Clientdatenquellen“](2020/technical-preview-2007.md#bkmk_content) <!--7102084-->
- [Verwendung der Schriftart mit fester Breite in einigen Konsolenbereichen](2020/technical-preview-2007.md#bkmk_font) <!--7632637-->
- [Verwalten der Größe von Tasksequenzrichtlinien](2020/technical-preview-2007.md#bkmk_tspol) <!--6888853-->
- [Verbesserungen an der Gerätezeitachse im Admin Center](2020/technical-preview-2007.md#bkmk_timeline)<!--7141381-->

## <a name="features-in-previous-technical-previews"></a>Features in älteren Technical Preview-Versionen

<!-- (explanatory comment)
This is the list of individual features that are still in TP (not in CB). 
Copy from the lists above any individual features that are still in TP and add to the top of this list
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

Nachfolgend sind die folgenden Features der Vorgängerversionen des Technical Preview-Branch für Configuration Manager dargestellt. Diese Features werden in späteren Versionen weiterhin unterstützt, sind aber in Current Branch noch nicht verfügbar.

| Komponente        | Technical Preview-Version |
|----------------|---------------------------|
| Verbesserungen an verfügbaren Apps über CMG <!--7033501--> | [Technical Preview 2006](2020/technical-preview-2006.md#bkmk_availapp) |
| Mandantenanfügung: „Skripts ausführen“ über das Admin Center <!--6234688--> | [Technical Preview 2005](2020/technical-preview-2005.md#bkmk_scripts) |
| Verbesserungen an Cloudverwaltungsgateway-Cmdlets <!--6978300--> | [Technical Preview 2005](2020/technical-preview-2005.md#bkmk_pwshcmg) |
| Melden von Setup- und Upgradefehlern bei Microsoft <!--5622909--> | [Technical Preview 2005](2020/technical-preview-2005.md#report-setup-and-upgrade-failures-to-microsoft) |
| Verbesserungen des Inhaltsbibliothek-Bereinigungstools <!--6887878--> | [Technical Preview 2005](2020/technical-preview-2005.md#bkmk_content) |
| Kopieren von Ermittlungsdaten aus der Konsole <!--6890051--> | [Technical Preview 2004](2020/technical-preview-2004.md#bkmk_copydisco) |
| Unterstützung für PowerShell-Version 7 <!--6023299--> | [Technical Preview 2004](2020/technical-preview-2004.md#bkmk_pwsh7) |
| Neuer Feedback-Assistent <!--3180826--> | [Technical Preview 2003](2020/technical-preview-2003.md#bkmk_feedback) |
| Abfragen des an Microsoft gesendeten Feedbacks <!--6488450--> | [Technical Preview 2003](2020/technical-preview-2003.md#bkmk_smile) |
| Anfügen von Dateien an Feedback <!--3556011--> | [Tech Preview 1910](2019/technical-preview-1910.md#attach-files-to-feedback) |
| Verbesserungen an multicastfähigen Verteilungspunkten <!--3785535--> | [Tech Preview 1908.2](2019/technical-preview-1908-2.md#bkmk_multicast) |
| Vorlagen für eine Bereitstellung in Phasen <!--4961086--> | [Tech Preview 1908](2019/technical-preview-1908.md#phased-deployment-templates) |
| Remotesteuerung an beliebigem Ort mit Cloud Management Gateway <!--4575930--> | [Tech Preview 1906](2019/technical-preview-1906.md#remote-control-anywhere-using-cloud-management-gateway) |
| Kostenschätzung für Clouddienste <!--3555774--> | [Tech Preview 1903](2019/technical-preview-1903.md#bkmk_cmg) |
| Clientbasierter PXE-Antwortdienst <!--3556018, fka 1357148--> | [Technical Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
| PXE-Netzwerkstartunterstützung für IPv6 <!--3601254, fka 1269793--> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
| Verwenden von Azure Active Directory <!--3607315, fka 1322145--> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
| Verbesserungen bei Asset Intelligence <!--3601024, fka 1307390--> | [Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence) |

## <a name="see-also"></a>Weitere Informationen:

Weitere Informationen finden Sie in den folgenden Artikeln:

- [Auswerten von Configuration Manager in einer Laborumgebung](evaluate-with-lab-environment.md)
- [Neuigkeiten zu inkrementellen Versionen von Configuration Manager](../plan-design/changes/whats-new-incremental-versions.md)
- [Einführung in Configuration Manager](../understand/introduction.md)

> [!Tip]
> Weitere Informationen zu Current Branch-Features, die Zustimmung für die Aktivierung erfordern, finden Sie in den [Features der Vorabversion](../servers/manage/pre-release-features.md).
>
> Weitere Informationen zu Current Branch-Features, die Sie zuerst aktivieren müssen, finden Sie unter [Aktivieren optionaler Features von Updates](../servers/manage/install-in-console-updates.md#bkmk_options).
