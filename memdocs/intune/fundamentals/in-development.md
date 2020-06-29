---
title: 'In der Entwicklung: Microsoft Intune'
titleSuffix: ''
description: In der Entwicklung befindliche Microsoft Intune-Features
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 107ac1e2aef18bcb72a6fe1f94eade23c3f85319
ms.sourcegitcommit: 79ffc8afed164c408db6994806d71f64d1fc0b8f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/23/2020
ms.locfileid: "85216517"
---
# <a name="in-development-for-microsoft-intune"></a>In der Entwicklung befindliche Features für Microsoft Intune

Um Ihnen bei Ihrer Vorbereitung und Planung zu helfen, sind auf dieser Seite Updates und Features der Intune-Benutzeroberfläche aufgeführt, die sich in der Entwicklung befinden, aber noch nicht freigegeben wurden. Zusätzlich zu den Informationen auf dieser Seite gilt Folgendes: 

- Wenn wir davon ausgehen, dass Sie vor einer Änderung Maßnahmen ergreifen müssen, werden wir einen ergänzenden Beitrag im Office-Nachrichtencenter veröffentlichen.
- Wenn ein Feature in die Produktionsumgebung wechselt, wird die Featurebeschreibung von dieser Seite auf die Seite [Neuerungen in Microsoft Intune](whats-new.md) verschoben, unabhängig davon, ob es sich um eine Vorschauversion handelt oder ob das Feature bereits allgemein verfügbar ist.
- Diese Seite und die Seite [Neuerungen](whats-new.md) werden regelmäßig aktualisiert. Überprüfen Sie, ob weitere Updates vorliegen.
- In der [Roadmap für Microsoft 365](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) finden Sie strategische Ziele und Zeitpläne.

> [!NOTE]
> Diese Seite spiegelt die aktuellen Planungen von Microsoft für Intune-Funktionen in einem zukünftigen Release wider. Termine und einzelne Features können sich ändern. Auf dieser Seite werden nicht alle Features beschrieben, die gerade entwickelt werden.

**RSS-Feed**: Bleiben Sie auf dem Laufenden, wenn diese Seite aktualisiert wird, indem Sie die folgende URL kopieren und in Ihren Feedreader einfügen: `https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`.

**Dieser Artikel wurde zuletzt an dem Datum aktualisiert, das unter dem obigen Titel aufgeführt ist.**

<!--
## What's coming to Intune in the Azure portal 
## What's coming to Intune apps
## Notices
-->

<!-- Common categories:  
## App management
## Device configuration
## Device enrollment
## Device management
## Intune apps
## Monitor and troubleshoot
## Role-based access control
## Security

-->
 
<!-- ***********************************************-->
<!--## App management-->


<!-- ***********************************************-->
## <a name="device-configuration"></a>Gerätekonfiguration

### <a name="set-device-compliance-state-from-third-party-mdm-partners---6361689-----"></a>Festlegen des Konformitätszustands von Geräten von MDM-Drittanbieterpartnern<!-- 6361689   -->
Microsoft 365-Kunden mit MDM-Lösungen von Drittanbietern können Richtlinien für den bedingten Zugriff für Microsoft 365-Apps auf iOS und Android über die Integration mit dem Microsoft Intune-Gerätekonformitätsdienst erzwingen. MDM-Drittanbieter nutzenden Intune-Gerätekonformitätsdienst zum Senden von Gerätekonformitätsdaten an Intune. Intune wertet dann aus, ob das Gerät vertrauenswürdig ist, und legt die Attribute für den bedingten Zugriff in Azure AD fest.  Kunden müssen Azure AD-Richtlinien für den bedingten Zugriff über Microsoft Endpoint Manager Admin Center oder das Azure AD-Portal festlegen.  


### <a name="new-vpn-settings-for-windows-10-and-newer-devices---6602122----"></a>Neue VPN-Einstellungen für Windows 10 und neuere Geräte<!-- 6602122  -->
Wenn Sie ein VPN-Profil mit dem IKEv2-Verbindungstyp erstellen, können Sie jetzt neue Einstellungen konfigurieren (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **Windows 10 und höher** für Plattform > **VPN** für Profil > **Basis-VPN**):

- **Gerätetunnel**: Ermöglicht Geräten den automatischen Verbindungsaufbau zu einem VPN, ohne dass eine Benutzerinteraktion, einschließlich Benutzeranmeldung, erforderlich ist. Diese Funktion erfordert, dass Sie **Always on** aktivieren und **Computerzertifikate** als Authentifizierungsmethode verwenden.
- Einstellungen der Kryptografie-Suite: Konfigurieren Sie die Algorithmen, die zum Sichern von IKE-und untergeordneten Sicherheitszuordnungen verwendet werden, wodurch Sie die Client-und Servereinstellungen aufeinander abstimmen können.

Informationen zu den Einstellungen, die Sie konfigurieren können, finden Sie unter [Windows-Geräteeinstellungen zum Hinzufügen von VPN-Verbindungen mithilfe von Intune](../configuration/vpn-settings-windows-10.md).

Gilt für:
- Windows 10 und höher


<!-- ***********************************************-->
<!--## Device enrollment-->



<!-- ***********************************************-->
## <a name="device-management"></a>Geräteverwaltung

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Unterstützung von PowerShell-Skripts für BYOD-Geräte<!-- 1862833  -->
PowerShell-Skripts unterstützen bei Azure AD registrierte Geräte in Intune. Weitere Informationen zu PowerShell finden Sie unter [Verwenden von PowerShell-Skripts auf Windows 10-Geräten in Intune](../apps/intune-management-extension.md). Diese Funktion unterstützt keine Geräte, auf denen die Windows 10 Home-Edition ausgeführt wird.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics enthält das Gerätedetailprotokoll<!--6014987  -->
Intune-Gerätedetailprotokolle werden unter **Berichte** > **Log Analytics** bereitgestellt. Sie können Gerätedetails korrelieren, um benutzerdefinierte Abfragen und Azure-Workbooks zu erstellen.

### <a name="tenant-attach-device-timeline-in-the-admin-center--7220536-cm7141381---"></a>Mandantenanfügung: Gerätezeitachse im Admin Center<!--7220536, CM7141381 -->
Wenn Configuration Manager ein Gerät über das Anfügen von Mandanten mit dem Microsoft Endpoint Manager synchronisiert, sehen Sie eine Zeitachse der Ereignisse. Diese Zeitachse zeigt die frühere Aktivität auf dem Gerät an, anhand der Sie Probleme beheben können. Weitere Informationen erhalten Sie unter [Technical Preview für Configuration Manager 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_timeline).  

### <a name="tenant-attach-install-an-application-from-the-admin-center---7220536-cm6024389---"></a>Mandantenanfügung: Installieren einer Anwendung über das Admin Center<!-- 7220536, CM6024389 -->
Sie können ab sofort über das Microsoft Endpoint Management Admin Center eine Anwendungsinstallation in Echtzeit für ein Gerät mit Mandantenanfügung einleiten. Weitere Informationen erhalten Sie unter [Technical Preview für Configuration Manager 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_apps).

### <a name="tenant-attach-cmpivot-from-the-admin-center--7220536-cm6024392---"></a>Mandantenanfügung: CMPivot aus dem Admin Center<!--7220536, CM6024392 -->
Holen Sie das Leistungspotenzial von [CMPivot](../../configmgr/tenant-attach/cmpivot-overview-attached.md) in das Microsoft Endpoint Manager Admin Center. Ermöglichen Sie zusätzlichen Rollen, z. B. dem Helpdesk, das Einleiten von Echtzeitabfragen aus der Cloud für ein einzelnes ConfigMgr-verwaltetes Gerät, und geben Sie die Ergebnisse an das Admin Center zurück. Dies bietet alle herkömmlichen Vorteile von CMPivot, mit denen IT-Administratoren und andere festgelegte Rollen schnell den Zustand von Geräten in Ihrer Umgebung bewerten und Maßnahmen ergreifen können. Weitere Informationen erhalten Sie unter [Technical Preview für Configuration Manager 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_cmpivot). 

### <a name="tenant-attach-run-scripts-from-the-admin-center--7220536-cm6234688---"></a>Mandantenanfügung: „Skripts ausführen“ über das Admin Center<!--7220536, CM6234688 -->
Bringen Sie das Leistungspotenzial des lokalen Configuration Manager-Features [Skripts ausführen](../../configmgr/apps/deploy-use/create-deploy-scripts.md) in das Microsoft Endpoint Manager Admin Center. Erlauben Sie zusätzlichen Rollen, z. B. dem Helpdesk, das Ausführen von PowerShell-Skripts aus der Cloud für ein einzelnes verwaltetes Configuration Manager-Gerät. Dies bietet alle herkömmlichen Vorteile von PowerShell-Skripts, die bereits vom Configuration Manager-Administrator definiert und für diese neue Umgebung genehmigt wurden. Weitere Informationen erhalten Sie unter [Technical Preview für Configuration Manager 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_scripts). 

### <a name="new-merge-logic-for-windows-10-devices--179048--"></a>Neue Zusammenführungslogik für Windows 10-Geräte<!--179048-->
Wenn ein Kunde heute das Reimaging für ein Gerät durchführt und es dann erneut registriert, werden in der Microsoft Endpoint Manager-Verwaltungskonsole mehrere Datensätze für das Gerät angezeigt. Eine neue Zusammenführungslogik ist in der Entwicklung, um solche doppelten Datensätze für Windows 10-Geräte zusammenzuführen.

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>Überwachung und Problembehandlung

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Vorlage V2.0 für Power BI-Konformitätsbericht<!-- 636958  -->
Administratoren können die Vorlagenversion für den Power BI-Konformitätsbericht von Version V1.0 auf V2.0 aktualisieren. Version V2.0 umfasst ein verbessertes Design sowie Änderungen an Berechnungen und Daten, die als Bestandteil der Vorlage präsentiert werden. Weitere Informationen finden Sie unter [Verbinden mit dem Data Warehouse mit Power BI](../developer/reports-proc-get-a-link-powerbi.md).

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
<!--## Security-->


<!-- ***********************************************-->
## <a name="notices"></a>Benachrichtigungen

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Weitere Informationen:

Details zu aktuellen Entwicklungen finden Sie unter [Neuerungen in Microsoft Intune](whats-new.md).
