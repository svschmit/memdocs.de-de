---
title: 'In der Entwicklung: Microsoft Intune'
titleSuffix: ''
description: In der Entwicklung befindliche Microsoft Intune-Features
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: e76816768090a624247db7a84da8c6bdffb800bc
ms.sourcegitcommit: 45657123a5db50aaecdb96d068712623d775f31c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/30/2020
ms.locfileid: "87443836"
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

### <a name="set-device-compliance-state-from-third-party-mdm-partners---6361689-----"></a>Festlegen des Konformitätszustands von Geräten von MDM-Drittanbieterpartnern<!-- 6361689   -->
Microsoft 365-Kunden mit MDM-Lösungen von Drittanbietern können Richtlinien für den bedingten Zugriff für Microsoft 365-Apps auf iOS und Android über die Integration mit dem Microsoft Intune-Gerätekonformitätsdienst erzwingen. MDM-Drittanbieter nutzenden Intune-Gerätekonformitätsdienst zum Senden von Gerätekonformitätsdaten an Intune. Intune wertet dann aus, ob das Gerät vertrauenswürdig ist, und legt die Attribute für den bedingten Zugriff in Azure AD fest.  Kunden müssen Azure AD-Richtlinien für den bedingten Zugriff über Microsoft Endpoint Manager Admin Center oder das Azure AD-Portal festlegen.

### <a name="create-pkcs-certificate-profiles-for-android-enterprise-fully-managed-devices-cobo---4839686---"></a>Erstellen von PKCS-Zertifikatprofilen für vollständig verwaltete Android Enterprise-Geräte (COBO)<!-- 4839686 -->
Sie können PKCS-Zertifikatprofile erstellen, um Zertifikate für den Besitzer des Android Enterprise-Geräts und für Arbeitsprofilgeräte bereitzustellen (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **Android Enterprise > Nur Gerätebesitzer** oder **Android Enterprise > Nur Arbeitsprofil** als Plattform > **PKCS** als Profil).

Bald können Sie PKCS-Zertifikatprofile für vollständig verwaltete Android Enterprise-Geräte erstellen. Der Intune-PFX-Zertifikatconnector ist erforderlich. Wenn Sie nicht SCEP verwenden, sondern nur PKCS, können Sie den NDES-Connector entfernen, nachdem Sie den neuen PFX-Connector installiert haben. Der neue PFX-Connector importiert PFX-Dateien und stellt PKCS-Zertifikate auf allen Plattformen bereit.

Weitere Informationen zu PKCS-Zertifikaten finden Sie unter [Konfigurieren und Verwenden von PKCS-Zertifikaten mit Intune](../protect/certficates-pfx-configure.md).

Gilt für:
- Vollständig verwaltetes Android Enterprise (COBO)

### <a name="use-netmotion-as-a-vpn-connection-type-for-iosipados-and-macos-devices---1333631---"></a>Verwenden von NetMotion als VPN-Verbindungstyp für iOS/iPadOS- und macOS-Geräte<!-- 1333631 -->
Wenn Sie ein VPN-Profil erstellen, ist NetMotion als VPN-Verbindungstyp verfügbar (**Geräte** > **Gerätekonfiguration** > **Profil erstellen** > **iOS/iPadOS** oder **macOS** als Plattform > **VPN** als Profil > **NetMotion** als Verbindungstyp).

Weitere Informationen zu VPN-Profilen in Intune finden Sie unter[Erstellen von VPN-Profilen zum Herstellen einer Verbindung mit VPN-Servern](../configuration/vpn-settings-configure.md).

Gilt für:
- iOS/iPadOS
- macOS

### <a name="more-protected-extensible-authentication-protocol-peap-options-for-windows-10-wi-fi-profiles---3805024---"></a>Weitere PEAP-Optionen (Protected Extensible Authentication Protocol) für Windows 10-WLAN-Profile<!-- 3805024 -->
Auf Windows 10-Geräten können Sie WLAN-Profile erstellen, die EAP (Extensible Authentication Protocol, erweiterbares Authentifizierungsprotokoll) verwenden, um WLAN-Verbindungen zu authentifizieren (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **Windows 10 und höher** als Plattform > **WLAN** als Profil > **Enterprise**). Wenn Sie „Protected EAP (PEAP)“ auswählen, stehen neue Einstellungen zur Verfügung:

- **Serverüberprüfung in PEAP-Phase 1 durchführen**: In Phase 1 der PEAP-Aushandlung überprüfen Geräte das Zertifikat und verifizieren den Server.
  - **Benutzereingabeaufforderungen für Serverüberprüfung in PEAP-Phase 1 deaktivieren**: In Phase 1 der PEAP-Aushandlung werden keine Benutzereingabeaufforderungen zur Autorisierung von neuen PEAP-Servern für vertrauenswürdige Zertifizierungsstellen angezeigt.
- **Kryptografische Bindung erforderlich**: Diese Einstellung verhindert Verbindungen mit PEAP-Servern, die während der PEAP-Aushandlung keine kryptografische Bindung verwenden.

Informationen dazu, welche Einstellungen Sie derzeit konfigurieren können, finden Sie unter [Hinzufügen von WLAN-Einstellungen zu Geräten unter Windows 10 und höher](../configuration/wi-fi-settings-windows.md).

Gilt für: 
- Windows 10 und höher

### <a name="configure-the-macos-microsoft-enterprise-sso-plug-in---5627576---"></a>Konfigurieren des Microsoft Enterprise SSO-Plug-Ins für macOS<!-- 5627576 -->
Das Microsoft Azure AD-Team hat eine App-Erweiterung zum Umleiten beim einmaligen Anmelden (Single Sign-On, SSO) entwickelt. Damit können Benutzer von macOS 10.15 und höher auf Microsoft-Apps, Organisations-Apps und Websites zugreifen, die das SSO-Feature von Apple unterstützen, und sich im gleichen Anmeldevorgang bei Azure AD authentifizieren. Mit dem Microsoft Enterprise SSO-Plug-In können Sie die SSO-Erweiterung mit dem neuen Microsoft Azure AD-App-Erweiterungstyp konfigurieren (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **macOS** als Plattform > **Gerätefeatures** als Profil > **App-Erweiterung für einmaliges Anmelden** > SSO-App-Erweiterung als Typ > **Microsoft Azure AD**).

Um SSO mit dem Microsoft Azure AD-SSO-App-Erweiterungstyp zu aktivieren, müssen Benutzer die Unternehmensportal-App auf ihren macOS-Geräten installieren und sich bei der App anmelden. 

Weitere Informationen zu macOS-SSO-App-Erweiterungen finden Sie unter [App-Erweiterung für einmaliges Anmelden](../configuration/device-features-configure.md#single-sign-on-app-extension).

Gilt für:
- macOS 10.15 und neuer

### <a name="use-sso-app-extensions-on-more-iosipados-apps-with-the-microsoft-enterprise-sso-plug-in---7369991---"></a>Verwenden von SSO-App-Erweiterungen in weiteren iOS/iPadOS-Apps mit dem Microsoft Enterprise SSO-Plug-In<!-- 7369991 -->
Das [Microsoft Enterprise SSO-Plug-In für Apple-Geräte](https://docs.microsoft.com/azure/active-directory/develop/apple-sso-plugin) kann mit allen Apps verwendet werden, die SSO-App-Erweiterungen unterstützen. In Intune bedeutet dieses Feature, dass das Plug-In mit mobilen iOS/iPadOS-Apps funktioniert, die nicht die Microsoft Authentication Library (MSAL) für Apple-Geräte verwenden. Die Apps müssen die MSAL nicht verwenden, weil sie sich nicht bei Azure AD-Endpunkten authentifizieren müssen.

Um Ihre iOS/iPadOS-Apps für die Verwendung von SSO mit dem Plug-In zu konfigurieren, fügen Sie die App-Bundle-IDs in einem iOS/iPadOS-Konfigurationsprofil hinzu (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **iOS/iPadOS** als Plattform > **Gerätefeatures** als Profil > **App-Erweiterung für einmaliges Anmelden** > **Microsoft Azure AD** als SSO-App-Erweiterungstyp > **App-Bundle-IDs**).

Informationen zu den SSO-App-Erweiterungseinstellungen, die Sie konfigurieren können, finden Sie unter [App-Erweiterung für einmaliges Anmelden](../configuration/ios-device-features-settings.md#single-sign-on-app-extension).

Gilt für:
- iOS/iPadOS

### <a name="improvement-to-update-device-settings-page-in-company-portal-app-for-android-to-show-descriptions---7414768---"></a>Verbesserungen an der Seite „Geräteeinstellungen aktualisieren“ in der Unternehmensportal-App für Android zur Anzeige von Beschreibungen<!-- 7414768 -->
In der Unternehmensportal-App auf Android-Geräten werden auf der Seite **Geräteeinstellungen aktualisieren** die Einstellungen aufgelistet, die ein Benutzer aktualisieren muss, um die Konformität sicherzustellen. Wir haben die Benutzeroberfläche verbessert: Die aufgeführten Einstellungen sind jetzt standardmäßig aufgeklappt und zeigen die Beschreibung sowie die Schaltfläche **Auflösen** an (sofern zutreffend). Zuvor waren die Einstellungen standardmäßig zugeklappt. Dieses neue Standardverhalten reduziert die Anzahl von notwendigen Klicks, sodass Benutzer Probleme schneller beheben können.

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

### <a name="associated-licenses-revoked-before-deletion-of-apple-vpp-token--6195322---"></a>Zugeordnete Lizenzen vor dem Löschen des Apple-VPP-Tokens widerrufen<!--6195322 -->
In einem zukünftigen Update werden Sie folgendes Verhalten bemerken: Wenn Sie ein Apple-VPP-Token in Microsoft Endpoint Manager löschen, werden alle von Intune zugewiesenen Lizenzen, die diesem Token zugeordnet sind, vor dem Löschen automatisch widerrufen.

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

### <a name="changes-for-endpoint-security-antivirus-policy-exclusions--5583940-6018119----"></a>Änderungen an Ausschlüssen der Antivirus-Richtlinie für Endpunktsicherheit<!--5583940, 6018119  -->
Wir führen zwei Änderungen bei der Verwaltung der Microsoft Defender Antivirus-Ausschlusslisten ein, die Sie im Rahmen einer Antivirenrichtlinie für die Endpunktsicherheit konfigurieren. (**Endpunktsicherheit** > **Antivirus** > **Richtlinie erstellen** > **Windows 10 und höher**  als Plattform). Mit diesen beiden Änderungen lassen sich Konflikte zwischen Richtlinien vermeiden, und Konflikte bei vorhandenen Richtlinien in Bezug auf die Liste der Ausschlüsse werden aufgehoben:

- Erstens haben wir einen neuen Profiltyp für Windows 10 und höher hinzugefügt: **Microsoft Defender Antivirus-Ausschlüsse**.  Dieser neue Profiltyp enthält nur die Einstellungen für die Angabe einer Liste von Defender-*Prozessen*, sowie von *Dateierweiterungen*, *Dateien* und *Ordnern*, die Microsoft Defender nicht überprüfen soll. So können Sie die Verwaltung Ihrer Ausschlusslisten vereinfachen, indem Sie sie von anderen Richtlinienkonfigurationen trennen.
- Durch die zweite Änderung werden die von Ihnen in verschiedenen Profilen definierten Ausschlusslisten in eine einzelne Ausschlussliste für jedes Gerät oder jeden Benutzer zusammengeführt, basierend auf den jeweiligen Richtlinien, die für einen bestimmten Benutzer oder ein bestimmtes Gerät gelten. Wenn beispielsweise für einen Benutzer drei Richtlinien gelten, werden die Ausschlusslisten für diese drei Richtlinien in eine einzelne übergeordnete Gruppe von Microsoft Defender Antivirus-Ausschlüssen zusammengeführt, die dann auf den Benutzer angewendet werden. Dies betrifft die Ausschlusslisten des neu hinzugefügten Profiltyps sowie alle vorhandenen, in einem *Microsoft Defender Antivirus*-Profil konfigurierten Richtlinien.



<!-- ***********************************************-->
## <a name="notices"></a>Benachrichtigungen

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Weitere Informationen:

Details zu aktuellen Entwicklungen finden Sie unter [Neuerungen in Microsoft Intune](whats-new.md).
