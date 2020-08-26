---
title: 'In der Entwicklung: Microsoft Intune'
titleSuffix: ''
description: In der Entwicklung befindliche Microsoft Intune-Features
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/06/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0d443cb784c19956f52347a10f4123c622ab82a8
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820059"
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
## <a name="app-management"></a>App-Verwaltung

### <a name="update-to-device-icons-in-company-portal-and-intune-apps-on-android---6057023----"></a>Aktualisieren von Gerätesymbolen im Unternehmensportal und in Intune-Apps unter Android<!-- 6057023  -->
Wir aktualisieren die Gerätesymbole im Unternehmensportal und in Intune-Apps auf Android-Geräten, um ihnen ein moderneres Erscheinungsbild in Einklang mit dem Microsoft Fluent Design System zu geben. Weitere Informationen finden Sie unter [Aktualisieren von Symbolen in der Unternehmensportal-App für iOS/iPadOS und macOS](../fundamentals/whats-new-app-ui.md#update-to-icons-in-company-portal-app-for-iosipados-and-macos-). 

### <a name="ios-company-portal-will-support-apples-automated-device-enrollment-without-user-affinity---7282707----"></a>Das iOS-Unternehmensportal unterstützt die automatische Geräteregistrierung von Apple ohne Benutzeraffinität<!-- 7282707  --> 
Das iOS-Unternehmensportal wird auf Geräten unterstützt, die mit der automatischen Geräteregistrierung von Apple registriert werden, ohne dass ein zugewiesener Benutzer erforderlich ist. Ein Endbenutzer kann sich beim iOS-Unternehmensportal anmelden, um sich als primärer Benutzer eines iOS-/iPadOS-Geräts einzurichten, das ohne Geräteaffinität registriert ist. Weitere Informationen zur automatischen Geräteregistrierung finden Sie unter [Automatisches Registrieren von iOS-/iPadOS-Geräten mit der automatischen Geräteregistrierung von Apple](../enrollment/device-enrollment-program-enroll-ios.md).

### <a name="the-windows-company-portal-adds-configuration-manager-application-support---4297660---"></a>Das Windows-Unternehmensportal unterstützt nun Configuration Manager-Anwendungen<!-- 4297660 -->
Das Windows-Unternehmensportal unterstützt jetzt Configuration Manager-Anwendungen. Dieses Feature ermöglicht es Endbenutzern, sowohl von Configuration Manager als auch von Intune bereitgestellte Anwendungen im Windows-Unternehmensportal für gemeinsam verwaltete Kunden anzuzeigen. Diese Unterstützung hilft Administratoren beim Konsolidieren ihrer verschiedenen Portalumgebungen für Endbenutzer. Weitere Informationen finden Sie unter [Verwenden der Unternehmensportal-App auf gemeinsam verwalteten Geräten](https://docs.microsoft.com/mem/configmgr/core/get-started/2020/technical-preview-2006#bkmk_portal).

<!-- ***********************************************-->
## <a name="device-configuration"></a>Gerätekonfiguration

### <a name="create-pkcs-certificate-profiles-for-android-enterprise-fully-managed-devices-cobo---4839686---"></a>Erstellen von PKCS-Zertifikatprofilen für vollständig verwaltete Android Enterprise-Geräte (COBO)<!-- 4839686 -->
Sie können PKCS-Zertifikatprofile erstellen, um Zertifikate für den Besitzer des Android Enterprise-Geräts und für Arbeitsprofilgeräte bereitzustellen (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **Android Enterprise > Nur Gerätebesitzer** oder **Android Enterprise > Nur Arbeitsprofil** als Plattform > **PKCS** als Profil).

Bald können Sie PKCS-Zertifikatprofile für vollständig verwaltete Android Enterprise-Geräte erstellen. Der Intune-PFX-Zertifikatconnector ist erforderlich. Wenn Sie nicht SCEP verwenden, sondern nur PKCS, können Sie den NDES-Connector entfernen, nachdem Sie den neuen PFX-Connector installiert haben. Der neue PFX-Connector importiert PFX-Dateien und stellt PKCS-Zertifikate auf allen Plattformen bereit.

Weitere Informationen zu PKCS-Zertifikaten finden Sie unter [Konfigurieren und Verwenden von PKCS-Zertifikaten mit Intune](../protect/certficates-pfx-configure.md).

Gilt für:
- Vollständig verwaltetes Android Enterprise (COBO)

<!-- ***********************************************-->
<!-- ## Device enrollment-->




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

### <a name="deploy-software-updates-to-macos-devices----3194876---"></a>Bereitstellen von Softwareupdates auf macOS-Geräten <!-- 3194876 -->
Sie können Softwareupdates für Gruppen von macOS-Geräten bereitstellen. Dieses Feature umfasst kritische, Firmware-, Konfigurationsdatei- und andere Updates. Sie können Updates beim nächsten Einchecken des Geräts senden oder einen Wochenplan auswählen, um Updates innerhalb oder außerhalb der von Ihnen festgelegten Zeitfenster bereitzustellen. Dies ist hilfreich, wenn Sie Geräte außerhalb der üblichen Geschäftszeiten aktualisieren möchten oder wenn Ihr Helpdesk voll besetzt ist. Außerdem erhalten Sie einen detaillierten Bericht zu allen macOS-Geräten mit bereitgestellten Updates. Sie können den Bericht geräteweise detailliert untersuchen, um die Status bestimmter Updates einzusehen.

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>Überwachung und Problembehandlung

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Vorlage V2.0 für Power BI-Konformitätsbericht<!-- 636958  -->
Administratoren können die Vorlagenversion für den Power BI-Konformitätsbericht von Version V1.0 auf V2.0 aktualisieren. Version v2.0 umfasst ein verbessertes Design sowie Änderungen an Berechnungen und Daten, die als Bestandteil der Vorlage präsentiert werden. Weitere Informationen finden Sie unter [Verbinden mit dem Data Warehouse mit Power BI](../developer/reports-proc-get-a-link-powerbi.md).

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## <a name="security"></a>Sicherheit

### <a name="app-protection-policy-support-for-symantec-endpoint-security-and-check-point-sandblast----4452423-4731168---"></a>Unterstützung für App-Schutzrichtlinien für Symantec Endpoint Security und Check Point Sandblast<!--  4452423, 4731168 -->

Im Oktober 2019 wurde in der Intune-App-Schutzrichtlinie die Funktion zum Verwenden von Daten einiger unserer Microsoft Threat Defense-Partnern (MTD) hinzugefügt. Wir fügen Unterstützung für die folgenden Partner hinzu, um eine App-Schutzrichtlinie zum Sperren oder selektiven Löschen von Unternehmensdaten des Benutzers auf der Grundlage der Integrität eines Geräts zu verwenden:

- **Check Point Sandblast** unter Android, iOS und iPadOS
- **Symantec Endpoint Security** unter Android, iOS und iPadOS

Weitere Informationen finden zum Verwenden einer App-Schutzrichtlinie mit MTD-Partnern finden Sie unter [Erstellen einer Mobile Threat Defense-App-Schutzrichtlinie (MTD) mit Intune](../protect/mtd-app-protection-policy.md).

### <a name="microsoft-defender-atp-creates-endpoint-manager-security-task-with-vulnerability-details---5568193----"></a>Microsoft Defender ATP erstellt Endpoint Manager-Sicherheitsaufgabe mit Details zu Sicherheitsrisiken<!-- 5568193  -->
Im Abschnitt „Bedrohungs- und Sicherheitsrisikomanagement“ in Microsoft Defender ATP werden falsch konfigurierte Sicherheitseinstellungen auf Geräten ermittelt. Administratoren können diese Informationen zum Aktualisieren von anfälligen Geräten verwenden.

In Kürze kann Microsoft Defender eine Endpoint Manager-Sicherheitsaufgabe (**Endpoint Manager** > **Endpunktsicherheit** > **Sicherheitsaufgaben**) mit den Details zum Sicherheitsrisiko erstellen und die betroffenen Geräte anzeigen. IT-Administratoren können die Sicherheitsaufgabe akzeptieren und die erforderliche Konfiguration bereitstellen. 

Weitere Informationen zu Sicherheitsaufgaben finden Sie unter [Verwenden von Intune zum Korrigieren von mit Microsoft Defender ATP identifizierten Sicherheitsrisiken](../protect/atp-manage-vulnerabilities.md).


<!-- ***********************************************-->
## <a name="notices"></a>Benachrichtigungen

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Weitere Informationen:

Details zu aktuellen Entwicklungen finden Sie unter [Neuerungen in Microsoft Intune](whats-new.md).
