---
title: Updates und Wartung
titleSuffix: Configuration Manager
description: Hier finden Sie Informationen zu der konsoleninternen Dienstmethode „Updates und Wartung“, mit der Sie empfohlene Updates leicht finden und installieren können.
ms.date: 06/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3a832943-580a-4a40-b454-961d0854ac2b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4f92d95b4e1cc814db72b45cfb92cb989b7767c8
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/01/2020
ms.locfileid: "85591016"
---
# <a name="updates-and-servicing-for-configuration-manager"></a>Updates und Wartung für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Configuration Manager verwendet eine konsoleninterne Wartungsmethode namens **Updates und Wartung**. Mit dieser können empfohlene Updates für Ihre Configuration Manager-Infrastruktur problemlos gesucht und installiert werden. Die konsoleninterne Wartung wird durch Out-of-Band-Updates wie Hotfixes ergänzt, die für Kunden bestimmt sind, die möglicherweise für die jeweilige Umgebung spezifische Probleme beheben müssen.  

> [!TIP]  
> Die Begriffe *Upgrade*, *Update* und *Installation* werden verwendet, um die drei separaten Konzepte in Configuration Manager zu beschreiben. Weitere Informationen zur Verwendung der Begriffe finden Sie unter [Informationen zu Upgrade, Update und Installation](../../understand/upgrade-update-install.md).  

## <a name="baseline-and-update-versions"></a><a name="bkmk_Baselines"></a> Baseline- und Updateversionen  

Verwenden Sie die neueste Baselineversion, wenn Sie einen neuen Standort in einer neuen Hierarchie installieren.

- Verwenden Sie ebenfalls eine Baselineversion, um ein Upgrade von System Center 2012 Configuration Manager auszuführen.  

- Verwenden Sie nach dem Upgrade auf Configuration Manager (Current Branch) keine Baselineversionen, um auf dem neuesten Stand zu bleiben. Verwenden Sie stattdessen nur [konsoleninterne Updates](install-in-console-updates.md), um ein Update auf die neueste Version durchzuführen.  

- In regelmäßigen Abständen werden neue Baselineversionen veröffentlicht. Indem Sie die neueste Baselineversion zur Installation einer neuen Hierarchie verwenden, vermeiden Sie die Installation einer veralteten oder nicht unterstützten Version von Configuration Manager und ein zusätzliches Upgrade Ihrer Infrastruktur, das diese auf den neuesten Stand bringt.  

Nach dem Installieren einer Baselineversion sind zusätzliche Versionen von Configuration Manager als konsoleninterne Updates verfügbar. Mit den konsoleninternen Updates wird Ihre Infrastruktur auf die neueste Version von Configuration Manager aktualisiert.  

- Sie installieren konsoleninternen Updates, um die Version Ihres Standorts der obersten Ebene zu aktualisieren.  

- Updates, die Sie an einem Standort der zentralen Verwaltung installieren, werden automatisch an untergeordneten primären Standorten installiert. Steuern Sie diesen Zeitplan, indem Sie ein Wartungsfenster am primären Standort verwenden.  

- Aktualisieren Sie sekundäre Standorte manuell, indem Sie in der Konsole ein Upgrade auf eine neue Version ausführen.  

Wenn Sie ein Update installieren, speichert das Update Installationsdateien für diese Version auf dem Standortserver in einem Ordner namens **CD.Latest**. Weitere Informationen zu diesen Dateien finden Sie unter [Der Ordner „CD.Latest“](the-cd.latest-folder.md).  

- Verwenden Sie die Dateien im Ordner „CD.Latest“ während der Sitewiederherstellung. Wenn in Ihrer Hierarchie keine Baselineversion mehr ausgeführt wird, verwenden Sie diese Dateien, um zusätzliche Standorte zu installieren.  

- Zum Installieren des ersten Standorts einer neuen Hierarchie oder zum Aktualisieren eines Standorts von System Center 2012 Configuration Manager können Sie keine Installationsdateien aus dem Ordner „CD.Latest“ verwenden.  

### <a name="version-details"></a>Versionsdetails

Einige Updates für Configuration Manager sind sowohl eine konsoleninterne Updateversion für vorhandene Infrastruktur als auch eine neue Baselineversion verfügbar.  

#### <a name="supported-versions"></a>Unterstützte Versionen

Die folgenden unterstützten Versionen von Configuration Manager sind derzeit als Baseline- und/oder Updateversion verfügbar:  

| Version | Verfügbarkeitsdatum | [Supportenddatum](current-branch-versions-supported.md) | Baseline | Konsoleninternes Update |  
|-------------|-----------|------------|--------------|------------------------|  
| [**2002**](../../plan-design/changes/whats-new-in-version-2002.md)<br /> (5.00.8968) | 1\. April 2020 | 1\. Oktober 2021 | Ja<sup>[Hinweis 1](#bkmk_note1)</sup> | Ja |
| [**1910**](../../plan-design/changes/whats-new-in-version-1910.md)<br /> (5.00.8913) | 29. November 2019 | 29. Mai 2021 | Nein | Ja |
| [**1906**](../../plan-design/changes/whats-new-in-version-1906.md)<br /> (5.00.8853) | 26. Juli 2019 | 26. Januar 2021 | Nein | Ja |
| [**1902**](../../plan-design/changes/whats-new-in-version-1902.md)<br /> (5.00.8790) | 27. März 2019 | 27. September 2020 | Ja<sup>[Hinweis 1](#bkmk_note1)</sup> | Ja |
| [**1810**](../../plan-design/changes/whats-new-in-version-1810.md)<br /> (5.00.8740) | 27. November 2018 | 1\. Dezember 2020 | Nein | Ja |

Das **Verfügbarkeitsdatum** entspricht dem Freigabedatum für den [Early Update Ring](checklist-for-installing-update-2002.md#early-update-ring). Baselinemedien stehen im Volume License Service Center bereit, sobald das Update global verfügbar ist.

<a name="bkmk_note1"></a>

> [!Note]  
> <sup>**Hinweis 1:** </sup> Die Baselinemedien sind als Teil der folgenden Releases im [Volume License Service Center](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) (VLSC) enthalten:
>
> - Microsoft Endpoint Configuration Manager (Current Branch)
> - System Center Datacenter
> - System Center Standard  
>
> Suchen Sie in VLSC beispielsweise nach `Microsoft Endpoint Configmgr (current branch)`. Suchen Sie die Baselinemedien in der Liste der Dateien, und laden Sie dieses Release herunter.  

#### <a name="historical-versions"></a>Vorgängerversionen

In der folgenden Tabelle werden Vorgängerversionen der Current Branch-Version von Configuration Manager aufgeführt, die nicht mehr unterstützt werden:

| Version | Verfügbarkeitsdatum | Supportenddatum | Baseline | Konsoleninternes Update |  
|-------------|-----------|------------|--------------|------------------------|  
| **1806** <br /> (5.00.8692) | 31. Juli 2018 | 31. Januar 2020 | Nein | Ja |
| **1802** <br /> (5.00.8634) | 22. März 2018 | 22. September 2019 | Ja | Ja |
| **1710** <br /> (5.00.8577) | 20. November 2017 | Mai 20, 2019 | Nein | Ja |
| **1706** <br /> (5.00.8540) | 31. Juli 2017 | 31. Juli 2018 | Nein | Ja |
| **1702** <br /> (5.00.8498) | 27. März 2017 | 27. März 2018 | Ja | Ja |
| **Version 1610** <br /> (5.00.8458) | 18. November 2016 | 18. November 2017 | Nein | Ja |
| **1606** <br /> (5.00.8412.1000) | 22. Juli 2016 | 22. Juli 2017 | Nein | Ja |
| **1606 mit KB3186654** <br />(5.00.8412.1307) | 12. Oktober 2016 | 12. Oktober 2017 | Ja | Nein |
| **1602** <br /> (5.00.8355) | 11. März 2016 | 11. März 2017 | Nein | Ja |
| **1511** <br /> (5.00.8325) | 8\. Dezember 2015 | 8\. Dezember 2016 | Ja | Nein |  

#### <a name="how-to-check-the-version"></a>Version überprüfen

Wechseln Sie oben links in der Konsole zu **Info**, um die Version Ihres Configuration Manager-Standorts zu überprüfen. Dieses Dialogfeld zeigt die Version des Standorts und der Konsole an.  

> [!Note]  
> Die Konsolenversion unterscheidet sich etwas von der Standortversion. Die Nebenversion der Konsole entspricht der Release-Version von Configuration Manager. In Configuration Manager Version 1802 lautet die anfängliche Standortversion beispielsweise 5.0.8634.1000 und die erste Konsolenversion 5.**1802**.1082.1700. Die Build- (1082) und Revisionsnummern (1700) können sich mit zukünftigen Hotfixes ändern.

## <a name="in-console-updates-and-servicing"></a><a name="bkmk_inconsole"></a> Konsoleninterne Updates und Wartung  

Wenn Sie eine produktionsbereite Installation von Configuration Manager (Current Branch) verwenden, sind die meisten Updates über den Kanal **Updates und Wartung** verfügbar. Mit dieser Methode können Sie die Updates für Ihre aktuelle Infrastrukturversion und Konfiguration ermitteln, herunterladen und zur Verfügung stellen. Dies umfasst nur Updates, die Microsoft allen Kunden empfiehlt.

Enthaltene Updates:  

- Neue Versionen wie z. B. 1906, 1910 oder 2002.

- Updates, die neue Features für die aktuelle Version enthalten

- Hotfixes, die für Ihre Version von Configuration Manager verfügbar sind und die alle Kunden installieren sollten

    > [!Note]  
    > Ab Version 1902 haben konsoleninterne Hotfixes jetzt Ablösungsbeziehungen. Weitere Informationen finden Sie unter [Ablösung für konsoleninterne Hotfixes](#bkmk_supersede).

Die konsoleninternen Updates bieten höhere Stabilität und beheben häufig auftretende Probleme. Sie ersetzen die Updatetypen für frühere Produktversionen wie Service Packs, kumulative Updates und Hotfixes, die für alle Kunden verfügbar sind, sowie die Erweiterung für Microsoft Intune.

Diese konsoleninternen Updates können für eine oder mehrere der folgenden Systeme gelten:  

- Server des primären Standorts und des Standorts der zentralen Verwaltung  

- Standortsystemrollen und -server  

- Instanzen des SMS-Anbieters  

- Configuration Manager-Konsolen  

- Configuration Manager-Clients  

Configuration Manager ermittelt neue Updates für Sie. Synchronisieren Sie Ihren Configuration Manager-Dienstverbindungspunkt mit dem Microsoft-Clouddienst, und beachten Sie dabei folgende Verhaltensweisen:  

- Wenn Ihr Dienstverbindungspunkt sich im Onlinemodus befindet, wird Ihr Standort täglich mit Microsoft synchronisiert. Neue Updates für Ihre Infrastruktur werden automatisch ermittelt. Zum Herunterladen von Updates und verteilbaren Dateien verwendet der Computer, auf dem die Standortsystemrolle „Dienstverbindungspunkt“ gehostet wird, den **Systemkontext** für den Zugriff auf die Internetadressen go.microsoft.com und download.microsoft.com. Weitere Informationen zu den zusätzlichen Standorten, die vom Dienstverbindungspunkt verwendet werden, finden Sie unter [Internetzugriffsanforderungen](../deploy/configure/about-the-service-connection-point.md#bkmk_urls).  

- Wenn Ihr Dienstverbindungspunkt sich im Offlinemodus befindet, verwenden Sie das Dienstverbindungstool, um eine manuelle Synchronisierung mit der Microsoft-Cloud auszuführen. Weitere Informationen finden Sie unter [Use the service connection point (Verwenden des Dienstverbindungspunkts)](use-the-service-connection-tool.md).  

- Durch konsoleninterne Updates entfällt die Notwendigkeit, verfügbare Updates, Service Packs und neue Features einzeln zu suchen und zu installieren.  

- Installieren Sie nur die von Ihnen ausgewählten konsoleninternen Updates. Wenn Sie Updates installieren, können Sie einzelne Features auswählen, die aktiviert und verwendet werden sollen. Weitere Informationen finden Sie unter [Enable optional features from updates (Aktivieren optionaler Features von Updates)](install-in-console-updates.md#bkmk_options).  

Wenn Sie ein konsoleninternes Update installieren, geschieht Folgendes:  

- Wird automatisch eine Voraussetzungsprüfung durchgeführt. Sie können diese Überprüfung auch vor dem Start der Installation manuell ausführen.  

- Es wird automatisch auf oberster Ebene in Ihrer Umgebung installiert. Dieser Standort entspricht dem Standort der zentralen Verwaltung (falls vorhanden). In einer Hierarchie wird das Update automatisch an primären Standorten installiert. Mit [Dienstfenster für Standortserver](service-windows.md) können Sie steuern, wann ein Update für die einzelnen primären Standortserver ausgeführt werden darf.  

- Nach dem Aktualisieren eines Standortservers werden alle Standortsystemrollen automatisch aktualisiert. Zu diesen Rollen zählen Instanzen des SMS-Anbieters. Nachdem das Update für den Standort installiert wurde, fordert die Configuration Manager-Konsole den Konsolenbenutzer dazu auf, die Konsole zu aktualisieren.  

- Wenn ein Update den Konfigurations-Manager-Client umfasst, können Sie auswählen, ob Sie das Update in der Präproduktionsumgebung testen oder sofort auf allen Clients installieren möchten.  

- Nach der Aktualisierung eines primären Standorts werden die sekundären Standorte nicht automatisch aktualisiert. Stattdessen müssen Sie die Aktualisierung der sekundären Standorte manuell initiieren.  

> [!NOTE]  
> Bei Configuration Manager (Current Branch), Long-Term Servicing Branch und Technical Preview-Branch handelt es sich um unterschiedliche Releases. Updates für einen Branch sind nicht als konsoleninterne Updates für andere Branches verfügbar. Weitere Informationen zu den verschiedenen Branches finden Sie unter [Welcher Branch von Configuration Manager soll verwendet werden?](../../understand/which-branch-should-i-use.md).

### <a name="supersedence-for-in-console-hotfixes"></a><a name="bkmk_supersede"></a>Ablösung für konsoleninterne Hotfixes

<!-- 3229613 -->
Ab Version 1902 haben konsoleninterne Hotfixes jetzt Ablösungsbeziehungen. Wenn Microsoft einen neuen Configuration Manager-Hotfix veröffentlicht, zeigt die Konsole keine Hotfixes an, die von diesem neuen Hotfix abgelöst werden. Mit diesem neuen Verhalten können Sie besser bestimmen, welche Hotfixes installiert werden müssen.

### <a name="supersedence-example"></a>Ablösungsbeispiel

Es gibt drei Hotfixes: Hotfix-A, Hotfix-B und Hotfix-C. Hotfix-A wird von Hotfix-B abgelöst und Hotfix-B von Hotfix-C.

|Hotfix-A|Hotfix-B|Hotfix-C|Konsoleninterne Ansicht|
|--------|--------|--------|---------------|
|Nicht installiert|Nicht installiert|Nicht installiert|Anzeige aller drei Hotfixes|
|Installiert|Installiert|Nicht installiert|Hotfix-B wird als installiert angezeigt.<br/>Hotfix-C wird als installationsbereit angezeigt.|
|Nicht installiert|Nicht installiert|Installiert|Hotfix-C wird als installiert angezeigt.|

## <a name="out-of-band-hotfixes"></a><a name="bkmk_outofband"></a> Out-of-Band-Hotfixes  

Einige Hotfixes werden mit eingeschränkter Verfügbarkeit veröffentlicht, um spezielle Probleme zu beheben. Andere Hotfixes sind für alle Kunden verfügbar, können jedoch nicht mit der konsoleninternen Methode installiert werden. Diese Hotfixes werden Out-of-Band bereitgestellt und vom Microsoft-Clouddienst nicht ermittelt.  

Wenn Sie ein Problem mit Ihrer Bereitstellung von Configuration Manager beheben möchten, finden Sie über den Microsoft-Kundendienst, über Knowledge Base-Artikel des Microsoft-Supports oder über den [Teamblog für Configuration Manager](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/bg-p/ConfigurationManagerBlog) in der Regel weitere Informationen zu Out-of-Band-Hotfixes.

Installieren Sie diese Hotfixes manuell, indem Sie eine der beiden folgenden Methoden verwenden:  

### <a name="update-registration-tool"></a>Tool zur Updateregistrierung

Dieses Tool importiert den Hotfix manuell in Ihre Configuration Manager-Konsole. Installieren Sie das Update anschließend wie ein automatisch erkanntes konsoleninternes Update.  

Diese Methode wird für Hotfixes mit folgender Dateinamenstruktur verwendet:  
    `<Product>-<product version>-<KB article ID>-ConfigMgr.Update.exe`

Weitere Informationen finden Sie unter [Use the update registration tool to import hotfixes (Verwenden des Tools zur Updateregistrierung zum Importieren von Hotfixes)](use-the-update-registration-tool-to-import-hotfixes.md).  

### <a name="hotfix-installer"></a>Hotfixinstallationsprogramm

Verwenden Sie dieses Tool, um einen Hotfix, der nicht mit der konsoleninternen Methode installiert werden kann, manuell zu installieren.  

Diese Methode wird für Hotfixes mit folgender Dateinamenstruktur verwendet:  
    `<Product>-<product version>-<KB article ID>-<platform>-<language>.exe`  

Weitere Informationen finden Sie unter [Use the hotfix installer to install updates (Verwenden des Hotfix-Installers zum Installieren von Updates)](use-the-hotfix-installer-to-install-updates.md).  

## <a name="next-steps"></a>Nächste Schritte

In den folgenden Artikeln wird erläutert, wie Sie die verschiedenen Updatetypen für Configuration Manager suchen und installieren:  

- [Installieren von konsoleninternen Updates](install-in-console-updates.md)  

- [Verwenden des Dienstverbindungstools](use-the-service-connection-tool.md)  

- [Verwenden des Tools zur Updateregistrierung zum Importieren von Hotfixes](use-the-update-registration-tool-to-import-hotfixes.md)  

- [Verwenden des Hotfix-Installers zum Installieren von Updates](use-the-hotfix-installer-to-install-updates.md)  

Weitere Informationen über den Technical Preview-Branch finden Sie unter [Technical Preview für Configuration Manager](../../get-started/technical-preview.md).
