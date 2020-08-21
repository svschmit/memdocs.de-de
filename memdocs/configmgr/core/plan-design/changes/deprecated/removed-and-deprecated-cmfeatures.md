---
title: Veraltete Features
titleSuffix: Configuration Manager
description: Hier finden Sie Informationen zu den Features, die von Configuration Manager nicht mehr unterstützt werden.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 287a6324-ae65-4d38-b2ef-198d47c91231
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 29b5dd8fdceb803de77aff9adbd0614d1e201b18
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694253"
---
# <a name="removed-and-deprecated-features-for-configuration-manager"></a>Entfernte und veraltete Features für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

In diesem Artikel werden Features beschrieben, die veraltet sind oder nicht mehr von Configuration Manager unterstützt und deswegen entfernt werden. Veraltete Features werden in einem zukünftigen Update entfernt. Diese Änderungen werden sich möglicherweise auf Configuration Manager auswirken.  

Die folgenden Informationen können sich bei zukünftigen Releases ändern. Möglicherweise sind daher nicht alle veralteten Configuration Manager-Features aufgeführt.

## <a name="deprecated-features"></a>Veraltete Features

Die folgenden Features sind veraltet. Sie können sie derzeit noch verwenden, aber Microsoft plant, den Support bald einzustellen.

|Komponente|Erste Ankündigung als veraltetes Feature|Nicht mehr &nbsp;unterstützt ab|
|-----------|---|--------------|
|Die Implementierung für die Freigabe von Inhalten aus Azure hat sich geändert. Verwenden Sie ein inhaltsfähiges Cloud-Management-Gateway. Zukünftig können Sie keinen herkömmlichen Cloudverteilungspunkt mehr erstellen.|Februar 2019|Noch festzulegen<sup>[Hinweis 1](#bkmk_note1)</sup>|
|Klassische Dienstbereitstellung in Azure für Cloud Management Gateway und den Cloudverteilungspunkt. Weitere Informationen finden Sie unter [Planen des Cloudverwaltungsgateways](../../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager).|November 2018|Noch festzulegen<sup>[Hinweis 1](#bkmk_note1)</sup>|

### <a name="note-1-support-removed-tbd"></a><a name="bkmk_note1"></a> Hinweis 1: Support eingestellt (noch festzulegen)

Der genaue Zeitrahmen muss noch festgelegt werden. Es wird von Microsoft empfohlen, den neuen Prozess oder das neue Feature zu verwenden. In der nächsten Zeit können Sie aber weiterhin den veralteten Prozess oder das veraltete Feature verwenden.

## <a name="unsupported-and-removed-features"></a>Nicht unterstützte und entfernte Features

Die folgenden Features werden nicht mehr unterstützt. Teilweise sind sie auch nicht mehr in dem Produkt enthalten.

|Komponente|Erste Ankündigung als veraltetes Feature|Nicht mehr &nbsp;unterstützt ab|  
|-----------|---|--------------|  
| Desktop Analytics-Option **Aktuelle Daten anzeigen** für die Geräteregistrierung und Sicherheitsupdates.<!-- 7080949 --> Weitere Informationen finden Sie unter [Datenlatenz](../../../../desktop-analytics/troubleshooting.md#data-latency).|Mai 2020|Juli 2020|
| Integration von Windows Analytics und Upgradebereitschaft. Weitere Informationen finden Sie unter [KB 4521815: Windows Analytics-Deaktivierung am 31. Januar 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement). | 14. Oktober 2019 | 31. Januar 2020 |
| Bewertung des Integritätsnachweises für Geräte für Konformitätsrichtlinien für bedingten Zugriff <!--1235616 aka 3608202--> Weitere Informationen finden Sie unter [Hybride Verwaltung mobiler Geräte](../../../../mdm/understand/what-happened-to-hybrid.md).| 3\. Juli 2019 | Version 1910 |
| Die Configuration Manager-Unternehmensportal-App | 21.Mai 2019 | Version 1910 |
| Der Anwendungskatalog einschließlich beider Standortsystemrollen: Anwendungskatalog-Websitepunkt und -Webdienstpunkt. Weitere Informationen finden Sie unter [Entfernen des Anwendungskatalogs](../../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat). | 21.Mai 2019 | Version 1910 |
|Zertifikatbasierte Authentifizierung mit Windows Hello for Business-Einstellungen in Configuration Manager<br>Weitere Informationen finden Sie unter [Configure Windows Hello for Business settings (So konfigurieren Sie Windows Hello for Business-Einstellungen)](../../../../protect/deploy-use/windows-hello-for-business-settings.md).|Dezember 2017|Version 1910|
|System Center Endpoint Protection für Mac und Linux.<br>Weitere Informationen finden Sie im [Blogbeitrag zum Ende des Supports](https://techcommunity.microsoft.com/t5/configuration-manager-blog/end-of-support-for-scep-for-mac-and-scep-for-linux-on-december/ba-p/286257).|Oktober 2018|31. Dezember 2018|
|Lokaler bedingter Zugriff<br>Weitere Informationen finden Sie unter [Hybride Verwaltung mobiler Geräte](../../../../mdm/understand/what-happened-to-hybrid.md).|30. Januar 2019|1\. September 2019|
|Hybridverwaltung mobiler Geräte (MDM)<br>Weitere Informationen finden Sie unter [Hybride Verwaltung mobiler Geräte](../../../../mdm/understand/what-happened-to-hybrid.md).<br><br>Ab Dienstversion 1902 von Intune, die voraussichtlich Ende Februar 2019 veröffentlicht wird, können Kunden keine neue Hybridverbindung mehr erstellen.<!--Intune feature 2683117-->|14. August 2018|1\. September 2019|
|Security Content Automation Protocol-Erweiterungen (SCAP) <!--3607889--><br>Die vorherige, zertifizierte Version ist weiterhin im [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=48741) verfügbar.|September 2018|Version 1810|
|Die **Silverlight-Benutzeroberfläche** für den Anwendungskatalog-Websitepunkt wird nicht mehr unterstützt. Benutzer sollten das neue Softwarecenter verwenden. Weitere Informationen finden Sie unter [Konfigurieren des Softwarecenters](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex).<!--1358309-->|11. August 2017| Version 1806|
|Vorherige Version des Softwarecenters.<br><br>Weitere Informationen zum neuen Softwarecenter finden Sie unter [Planen und Konfigurieren der Anwendungsverwaltung ](../../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_userex).|13. Dezember 2016|Version 1802|
|Verwaltung von virtuellen Festplatten (VHDs) mit Configuration Manager. <br><br>Gleichzeitig mit der Kennzeichnung als veraltete Features werden Optionen zum Erstellen einer neuen virtuellen Festplatte oder zum Verwalten einer virtuellen Festplatte mithilfe einer Tasksequenz entfernt. Außerdem ist der Knoten „Virtuelle Festplatten“ nicht mehr in der Configuration Manager-Konsole verfügbar. <br><br>Vorhandene virtuelle Festplatten werden nicht gelöscht. Auf diese kann jedoch nicht mehr über die Configuration Manager-Konsole zugegriffen werden.  |6\. Januar 2017 |Version 1710|
|Tasksequenzen: <br /> - In dynamischen Datenträger konvertieren <br /> - Bereitstellungstools installieren |18. November 2016|Version 1710|
|Upgradebewertungstool<br><br>Das Upgradebewertungstool ist sowohl von Configuration Manager als auch vom Anwendungskompatibilitäts-Toolkit (Application Compatibility Toolkit, ACT) 6.x abhängig. Die letzte Version von ACT war im Windows 10 v1511 ADK enthalten. Da es keine weiteren Updates für ACT geben wird, wird auch das Upgradebewertungstool nicht mehr unterstützt. Hinweise zu veralteten Funktionen wurden am 12. September 2016 auf der [Downloadseite des Upgradebewertungstools](https://www.microsoft.com/software-download/windows10) hinzugefügt. | 12. September 2016  | 11. Juli 2017 |
|Softwareupdatepunkte mit einem Cluster für den Netzwerklastenausgleich | 27. Februar 2016 | Version 1702 |
|Tasksequenzen: <br /> – OSDPreserveDriveLetter  <br /><br /> Während einer standardmäßigen Betriebssystembereitstellung bestimmt Windows Setup den Laufwerkbuchstaben, der am besten zur Verwendung geeignet ist (in der Regel C:). Wenn Sie ein anderes Laufwerk zur Verwendung angeben möchten, können Sie den Speicherort im Tasksequenzschritt „Betriebssystem anwenden“ ändern. Wechseln Sie zu der Einstellung **Wählen Sie den Standort aus, an dem Sie dieses Betriebssystem anwenden möchten**. Wählen Sie **Bestimmter Buchstabe für logisches Laufwerk** und anschließend das Laufwerk, das Sie verwenden möchten. |20. Juni 2016 |Version 1606 |
|Netzwerkzugriffsschutz (Network Access Protection, NAP) wie in System Center 2012 Configuration Manager|10. Juli 2015|Version 1511|  
|Out-of-Band-Verwaltung wie in System Center 2012 Configuration Manager|16. Oktober 2015|Version 1511|

### <a name="features-removed-in-version-1511"></a>Features, die ab Version 1511 nicht mehr enthalten sind

Die folgenden Abschnitte enthalten zusätzliche Information zu Features, die ab Version 1511 nicht mehr verfügbar sind:

#### <a name="out-of-band-management"></a><a name="bkmk_amt"></a> Out-of-Band-Verwaltung  

Mit Configuration Manager wurde der native Support für AMT-basierte Computer in der Configuration Manager-Konsole entfernt.  

- AMT-basierte Computer werden weiterhin vollständig verwaltet, wenn Sie das [Intel SCS-Add-On für Configuration Manager](https://www.intel.com/content/www/us/en/software/setup-configuration-software.html) verwenden. Über das Add-On haben Sie Zugriff auf die neuesten AMT-Verwaltungsfunktionen. Gleichzeitig werden die Beschränkungen aufgehoben, die vor der Einbindung dieser Änderungen durch Configuration Manager eingeführt wurden.  

- Die Out-Band-Verwaltung in System Center 2012 Configuration Manager ist von dieser Änderung nicht betroffen.  

#### <a name="network-access-protection"></a><a name="bkmk_nap"></a> Netzwerkzugriffsschutz

Configuration Manager hat die Unterstützung für den Netzwerkzugriffsschutz eingestellt. Das Feature wurde in Windows Server 2012 R2 als veraltet markiert und aus Windows 10 entfernt.  

Alternativen für den Netzwerkzugriffsschutz finden Sie im Abschnitt *Veraltete Funktionalität* unter [Netzwerkrichtlinien- und Zugriffsdienste: Übersicht](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831683(v=ws.11)).

## <a name="see-also"></a>Weitere Informationen:

- [Entfernte und veraltete Elemente](removed-and-deprecated.md)
- [Microsoft-Support-Lifecycle-Richtlinien](https://support.microsoft.com/lifecycle)
- [Support für die Current Branch-Versionen von Configuration Manager](../../../servers/manage/current-branch-versions-supported.md)