---
title: 'In der Entwicklung: Microsoft Intune'
titleSuffix: ''
description: In der Entwicklung befindliche Microsoft Intune-Features
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/26/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5afca831e2f3cbcda69150adcbbcff996bf99554
ms.sourcegitcommit: 01c1ca337e82c5e8e92153079ed89f79e20bde9e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/09/2020
ms.locfileid: "86157806"
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

### <a name="smime-for-outlook-on-ios-and-android-enterprise-devices-managed-without-enrollment---6517155----"></a>Verwaltung von S/MIME für Outlook auf iOS- und Android Enterprise-Geräten ohne Registrierung<!-- 6517155  -->
Sie können S/MIME für Outlook auf iOS- und Android Enterprise-Geräten aktivieren, indem Sie App-Konfigurationsrichtlinien für Geräte verwenden, die ohne Registrierung verwaltet werden. Wählen Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) nacheinander **Apps** > **App-Konfigurationsrichtlinien** > **Hinzufügen** > **Verwaltete Anwendungen** aus. Darüber hinaus können Sie wählen, ob Sie Benutzern erlauben möchten, diese Einstellung in Outlook festzulegen oder nicht. Weitere Informationen zum Konfigurieren von Outlook-Einstellungen finden Sie unter [Microsoft Outlook-Konfigurationseinstellungen](../apps/app-configuration-policies-outlook.md).

### <a name="ios-company-portal-will-support-apples-automated-device-enrollment-without-user-affinity---7282707----"></a>Das iOS-Unternehmensportal unterstützt die automatische Geräteregistrierung von Apple ohne Benutzeraffinität<!-- 7282707  --> 
Das iOS-Unternehmensportal wird auf Geräten unterstützt, die mit der automatischen Geräteregistrierung von Apple registriert werden, ohne dass ein zugewiesener Benutzer erforderlich ist. Ein Endbenutzer kann sich beim iOS-Unternehmensportal anmelden, um sich als primärer Benutzer eines iOS-/iPadOS-Geräts einzurichten, das ohne Geräteaffinität registriert ist. Weitere Informationen zur automatischen Geräteregistrierung finden Sie unter [Automatisches Registrieren von iOS-/iPadOS-Geräten mit der automatischen Geräteregistrierung von Apple](../enrollment/device-enrollment-program-enroll-ios.md).

### <a name="win32-app-installation-notifications-and-the-company-portal---7485945----"></a>Win32-App-Installationsbenachrichtigungen und das Unternehmensportal<!-- 7485945  -->
Endbenutzer können entscheiden, ob die im [Microsoft Intune-Webunternehmensportal](https://portal.manage.microsoft.com/) gezeigten Anwendungen über die Unternehmensportal-App oder das Webunternehmensportal geöffnet werden sollen. Diese Option steht nur zur Verfügung, wenn der Endbenutzer die Unternehmensportal-App installiert hat und eine Webunternehmensportal-Anwendung außerhalb eines Browsers startet.

### <a name="the-company-portal-adds-configuration-manager-application-support---4297660---"></a>Das Unternehmensportal unterstützt nun Configuration Manager-Anwendungen<!-- 4297660 -->
Das Unternehmensportal unterstützt jetzt Configuration Manager-Anwendungen. Dieses Feature ermöglicht Endbenutzern, sowohl von Configuration Manager als auch von Intune bereitgestellte Anwendungen im Unternehmensportal für gemeinsam verwaltete Kunden anzuzeigen. Diese Unterstützung hilft Administratoren beim Konsolidieren ihrer verschiedenen Portalumgebungen für Endbenutzer. Weitere Informationen finden Sie unter [Verwenden der Unternehmensportal-App auf gemeinsam verwalteten Geräten](https://docs.microsoft.com/mem/configmgr/core/get-started/2020/technical-preview-2006#bkmk_portal).

<!-- ***********************************************-->
## <a name="device-configuration"></a>Gerätekonfiguration

### <a name="set-device-compliance-state-from-third-party-mdm-partners---6361689-----"></a>Festlegen des Konformitätszustands von Geräten von MDM-Drittanbieterpartnern<!-- 6361689   -->
Microsoft 365-Kunden mit MDM-Lösungen von Drittanbietern können Richtlinien für den bedingten Zugriff für Microsoft 365-Apps auf iOS und Android über die Integration mit dem Microsoft Intune-Gerätekonformitätsdienst erzwingen. MDM-Drittanbieter nutzenden Intune-Gerätekonformitätsdienst zum Senden von Gerätekonformitätsdaten an Intune. Intune wertet dann aus, ob das Gerät vertrauenswürdig ist, und legt die Attribute für den bedingten Zugriff in Azure AD fest.  Kunden müssen Azure AD-Richtlinien für den bedingten Zugriff über Microsoft Endpoint Manager Admin Center oder das Azure AD-Portal festlegen.  


### <a name="new-vpn-settings-for-windows-10-and-newer-devices---6602122----"></a>Neue VPN-Einstellungen für Windows 10 und neuere Geräte<!-- 6602122  -->
Wenn Sie ein VPN-Profil mit dem IKEv2-Verbindungstyp erstellen, können Sie jetzt neue Einstellungen konfigurieren (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **Windows 10 und höher** für Plattform > **VPN** für Profil > **Basis-VPN**):

- **Gerätetunnel**: Ermöglicht Geräten den automatischen Aufbau der Verbindung mit einem VPN, ohne dass eine Benutzerinteraktion, einschließlich Benutzeranmeldung, erforderlich ist. Diese Funktion erfordert, dass Sie **Always on** aktivieren und **Computerzertifikate** als Authentifizierungsmethode verwenden.
- Einstellungen der Kryptografie-Suite: Konfigurieren Sie die Algorithmen, die zum Sichern von IKE-und untergeordneten Sicherheitszuordnungen verwendet werden, wodurch Sie die Client-und Servereinstellungen aufeinander abstimmen können.

Informationen zu den Einstellungen, die Sie konfigurieren können, finden Sie unter [Windows-Geräteeinstellungen zum Hinzufügen von VPN-Verbindungen mithilfe von Intune](../configuration/vpn-settings-windows-10.md).

Gilt für:
- Windows 10 und höher

### <a name="new-features-for-managed-home-screen-on-android-enterprise-device-owner-dedicated-devices-cosu---7414175-7133328-7133720-7134873-7135184----"></a>Neue Features für Managed Home Screen auf dedizierten benutzereigenen Android Enterprise-Geräte (COSU)<!-- 7414175 7133328 7133720 7134873 7135184  -->
Auf Android Enterprise-Geräten können Administratoren mithilfe von Gerätekonfigurationsprofilen den Managed Home Screen auf dedizierten Geräten mithilfe des Kioskmodus mit mehreren Apps konfigurieren (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **Android Enterprise** für Plattform > **Gerätebesitzer** > **Geräteeinschränkungen** für Profil > **Gerätefunktionen**).

Insbesondere bestehen die folgenden Möglichkeiten:

- Anpassen von Symbolen, Ändern der Bildschirmausrichtung und Anzeigen von App-Benachrichtigungen auf Badgesymbolen <!--7414175-->
- Ausblenden des Einstiegspunkts „Verwaltete Einstellungen“ <!--7133328-->
- Einfacherer Zugriff auf das Menü „Debuggen“ <!--7133720-->
- Erstellen einer Zulassungsliste mit WLAN-Netzwerken <!-- 7134873-->
- Einfacherer Zugriff auf die Geräteinformationen <!-- 7135184-->

Weitere Informationen finden Sie unter [Android Enterprise-Geräteeinstellungen zum Zulassen oder Einschränken von Features mit Intune](../configuration/device-restrictions-android-for-work.md).

Gilt für:

- Dedizierte benutzereigene Android Enterprise-Geräte (COSU)

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Geräteregistrierung

### <a name="corporate-owned-personally-enabled-devices-preview--4442275---"></a>Unternehmenseigene, persönlich aktivierte Geräte (Vorschau)<!--4442275 -->
Intune unterstützt für Betriebssystemversionen ab Android 8 unternehmenseigene Android Enterprise-Geräte mit einem Arbeitsprofil. Unternehmenseigene Geräte mit einem Arbeitsprofil sind eines der Unternehmensverwaltungsszenarien in der Android Enterprise-Lösungspalette. Dieses Szenario bezieht sich auf Geräte für Einzelbenutzer, die für den geschäftlichen und privaten Gebrauch bestimmt sind. Dieses Szenario unternehmenseigener, persönlich aktivierter Geräte bietet Folgendes:

- Containerisierung von Arbeits- und persönlichen Profilen
- Steuerung auf Geräteebene für Administratoren
- Garantie für Endbenutzer, dass ihre persönlichen Daten und Anwendungen privat bleiben

Die erste Public Preview-Version enthält eine Teilmenge der Features, die in der allgemein verfügbaren Version enthalten sein werden. Weitere Features werden laufend hinzugefügt. Zu den Features, die in der ersten Vorschau verfügbar sein werden, gehören:

- Registrierung: Administratoren können mehrere Registrierungsprofile mit eindeutigen Token erstellen, die nicht ablaufen. Die Registrierung von Geräten kann über NFC, Tokeneingabe, QR-Code, Zero Touch oder Knox Mobile Enrollment erfolgen.
- Gerätekonfiguration: Eine Teilmenge der vorhandenen Einstellungen für vollständig verwaltete und dedizierte Geräte.
- Gerätekonformität: Die Konformitätsrichtlinien, die derzeit für vollständig verwaltete Geräte verfügbar sind.
- Geräteaktionen: Gerät löschen (Zurücksetzen auf Werkseinstellungen), Gerät neu starten und Gerät sperren.  
- App-Verwaltung: Zuweisungen und Konfiguration von Apps und die damit verbundenen Berichtsfunktionen 
- Bedingter Zugriff



<!-- ***********************************************-->
## <a name="device-management"></a>Geräteverwaltung

### <a name="device-compliance-logs-now-in-english--6014904---"></a>Protokolle zur Gerätekonformität jetzt in englischer Sprache<!--6014904 -->
Die IntuneDeviceComplianceOrg-Protokolle enthalten nur Enumerationen für ComplianceState, OwnerType und DeviceHealthThreatLevel. In einem künftigen Update werden diese Protokolle in den Spalten englischsprachige Informationen enthalten.

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

### <a name="updates-to-the-remote-lock-action-for-macos-devices--7032805---"></a>Aktualisierungen der Aktion „Remotesperre“ für macOS-Geräte<!--7032805 -->
Aktualisierungen der Aktion „Remotesperre" für macOS-Geräte umfassen Folgendes:
- Die PIN für die Wiederherstellung wird 30 Tage angezeigt, ehe sie gelöscht wird (anstelle von sieben Tagen).
- Wenn ein Administrator einen zweiten Browser geöffnet hat und versucht, den Befehl erneut über eine andere Registerkarte oder einen anderen Browser auszulösen, lässt Intune den Befehl passieren. Doch der Meldestatus wird auf „Fehlschlagen“ festgelegt, anstatt eine neue PIN zu generieren.
- Der Administrator kann keinen weiteren Remotesperrbefehl ausführen, wenn der vorherige Befehl noch aussteht oder das Gerät nicht wieder eingecheckt wurde.
Diese Änderungen sollen verhindern, dass die richtige PIN nach mehreren Remotesperrbefehlen überschrieben wird.

### <a name="deploy-software-updates-to-macos-devices----3194876---"></a>Bereitstellen von Softwareupdates auf macOS-Geräten <!-- 3194876 -->
Sie können Softwareupdates für Gruppen von macOS-Geräten bereitstellen. Dieses Feature umfasst kritische, Firmware-, Konfigurationsdatei- und andere Updates. Sie können Updates beim nächsten Einchecken des Geräts senden oder einen Wochenplan auswählen, um Updates innerhalb oder außerhalb der von Ihnen festgelegten Zeitfenster bereitzustellen. Dies ist hilfreich, wenn Sie Geräte außerhalb der üblichen Geschäftszeiten aktualisieren möchten oder wenn Ihr Helpdesk voll besetzt ist. Außerdem erhalten Sie einen detaillierten Bericht zu allen macOS-Geräten mit bereitgestellten Updates. Sie können den Bericht geräteweise detailliert untersuchen, um die Status bestimmter Updates einzusehen.

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>Überwachung und Problembehandlung

### <a name="additional-data-warehouse-v10-properties---6125732-----"></a>Zusätzliche Data Warehouse v1.0-Eigenschaften<!-- 6125732   -->
Mithilfe von Intune Data Warehouse v1.0 stehen weitere Eigenschaften zur Verfügung. Die folgenden Eigenschaften werden jetzt über die Entität [devices](../developer/reports-ref-devices.md#devices) verfügbar gemacht:
- `ethernetMacAddress`: Der eindeutige Netzwerkbezeichner dieses Geräts.
- `office365Version`: Die auf dem Gerät installierte Version von Office 365.

Die folgenden Eigenschaften werden jetzt über die Entität [devicePropertyHistories](../developer/reports-ref-devices.md#devicepropertyhistories) verfügbar gemacht:
- `physicalMemoryInBytes`: Der physische Speicher in Byte.
- `totalStorageSpaceInBytes`: Gesamtspeicherkapazität in Bytes

Weitere Informationen finden Sie unter [Microsoft Intune Data Warehouse-API](../developer/reports-nav-intune-data-warehouse.md).

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Vorlage V2.0 für Power BI-Konformitätsbericht<!-- 636958  -->
Administratoren können die Vorlagenversion für den Power BI-Konformitätsbericht von Version V1.0 auf V2.0 aktualisieren. Version v2.0 umfasst ein verbessertes Design sowie Änderungen an Berechnungen und Daten, die als Bestandteil der Vorlage präsentiert werden. Weitere Informationen finden Sie unter [Verbinden mit dem Data Warehouse mit Power BI](../developer/reports-proc-get-a-link-powerbi.md).

<!-- ***********************************************-->
## <a name="role-based-access-control"></a>Rollenbasierte Zugriffssteuerung

### <a name="scope-tag-support-for-customization-policies--6182440---"></a>Unterstützung von Bereichsmarkierungen für Anpassungsrichtlinien<!--6182440 -->
Sie können Anpassungsrichtlinien Bereichsmarkierungen hinzufügen. Wechseln Sie dazu zu [Microsoft Endpoint Manager Administrations Center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Mandantenverwaltung**> **Anpassung**, wo Sie Konfigurationsoptionen für **Bereichsmarkierungen** finden.

### <a name="assign-profile-and-update-profile-permission-changes--7177586---"></a>Änderungen an den Berechtigungen „Profil zuweisen“ und „Profil aktualisieren“<!--7177586 -->
Für „Profil zuweisen“ und „Profil aktualisieren“ wurden rollenbasierte Zugriffssteuerungsberechtigungen geändert:
- Profil zuweisen: Administratoren mit dieser Berechtigung können die Profile auch Token zuweisen und einem Token ein Standardprofil zuweisen.
- Profil aktualisieren: Administratoren mit dieser Berechtigung können nur vorhandene Profile aktualisieren.

<!-- ***********************************************-->
## <a name="security"></a>Sicherheit

### <a name="app-protection-policy-support-for-symantec-endpoint-security-and-check-point-sandblast----4452423-4731168---"></a>Unterstützung für App-Schutzrichtlinien für Symantec Endpoint Security und Check Point Sandblast<!--  4452423, 4731168 -->

Im Oktober 2019 wurde in der Intune-App-Schutzrichtlinie die Funktion zum Verwenden von Daten einiger unserer Microsoft Threat Defense-Partnern (MTD) hinzugefügt. Wir fügen Unterstützung für die folgenden Partner hinzu, um eine App-Schutzrichtlinie zum Sperren oder selektiven Löschen von Unternehmensdaten des Benutzers auf der Grundlage der Integrität eines Geräts zu verwenden:

- **Check Point Sandblast** unter Android, iOS und iPadOS
- **Symantec Endpoint Security** unter Android, iOS und iPadOS

Weitere Informationen finden zum Verwenden einer App-Schutzrichtlinie mit MTD-Partnern finden Sie unter [Erstellen einer Mobile Threat Defense-App-Schutzrichtlinie (MTD) mit Intune](../protect/mtd-app-protection-policy.md).

### <a name="store-the-recovery-key-for-a-macos-device-that-was-encrypted-with-filevault-before-enrolling-with-intune--5239424-----"></a>Speichern des Wiederherstellungsschlüssels eines macOS-Geräts, das vor der Registrierung bei Intune mit FileVault verschlüsselt wurde<!--5239424   -->
Bald müssen Benutzer eines macOS-Geräts, das nicht gemäß der FileVault-Richtlinie von Intune verschlüsselt oder vor der Registrierung bei Intune verschlüsselt wurde, ihr Gerät nicht mehr entschlüsseln, damit es anschließend von Intune wieder verschlüsselt werden kann. Stattdessen kann die aktuelle Verschlüsselung unverändert bleiben. Der Benutzer kann die Website des Unternehmensportals besuchen, auf der er *Wiederherstellungsschlüssel speichern* wählen kann, um seinen persönlichen Wiederherstellungsschlüssel für das verschlüsselte macOS-Gerät zu übermitteln. Nach Übermittlung eines gültigen Schlüssels lässt Intune den persönlichen Schlüssel rotieren, um einen neuen Schlüssel zu generieren. Dieser bleibt für den Benutzer über die Website des Unternehmensportals, das iOS- bzw. Android-Unternehmensportal oder die Intune-App verfügbar. Benutzer können dann von jedem Gerät aus auf diese Speicherorte zugreifen, um den Schlüssel anzuzeigen, falls sie von ihrem macOS-Gerät ausgesperrt werden sollten.

### <a name="hide-the-personal-recovery-key-from-a-device-user-during-macos-filevault-disk-encryption----5475632----"></a>Ausblenden des persönlichen Wiederherstellungsschlüssels vor einem Gerätebenutzer während der Datenträgerverschlüsselung mit FileVault unter macOS<!--  5475632  -->
Wir fügen eine neue Einstellung namens *Wiederherstellungsschlüssel ausblenden* zur Richtlinie zur Datenträgerverschlüsselung für Endpunktsicherheit für FileVault hinzu (**Endpunktsicherheit** > **Datenträgerverschlüsselung** > **Profil erstellen** > **macOS** > **FileVault**). Wenn Sie die neue Einstellung aktivieren, verbirgt Intune während der Verschlüsselung den persönlichen Wiederherstellungsschlüssel vor dem Benutzer des macOS-Geräts. Indem Sie den Schlüssel zu diesem Zeitpunkt ausblenden, können Sie ihn sicherer machen, da Benutzer nicht in der Lage sind, ihn aufzuschreiben, während sie darauf warten, dass das Gerät verschlüsselt wird. Stattdessen kann ein Benutzer, wenn eine Wiederherstellung erforderlich ist, jederzeit ein beliebiges Gerät verwenden, um seinen persönlichen Wiederherstellungsschlüssel auf der Website des Intune-Unternehmensportals einzusehen.

### <a name="improved-view-of-security-baseline-details-for-devices---5536846-----"></a>Verbesserte Ansicht der Details zur Sicherheitsbaseline für Geräte<!-- 5536846   -->
Wir arbeiten daran, die Anzeige von Einstellungsdetails in der Sicherheitsbaseline zu verbessern, wenn Sie die Details eines Geräts genauer untersuchen (**Endpunktsicherheit** > **Geräte**).  Für jede zugewiesene Sicherheitsbaseline können Sie eine flache Liste mit Details für jede Einstellung anzeigen, die Einstellungskategorien, Einstellungsnamen und den Status jeder Einstellung auf diesem Gerät enthält.

### <a name="manage-source-locations-for-definition-updates-with-endpoint-security-antivirus-policy-for-windows-10-devices---6347801----"></a>Verwalten der Quellspeicherorte für Definitionsaktualisierungen der Antivirenrichtlinie von Endpunkten für Windows 10-Geräte<!-- 6347801  -->  
Wir fügen der Kategorie *Updates* der Antivirenrichtlinie für Endpunktsicherheit für Windows 10-Geräte zwei neue Einstellungen hinzu, mit deren Hilfe Sie verwalten können, wie Geräte Definitionsaktualisierungen erhalten (**Endpunktsicherheit** > ** Antivirus** > **Richtlinie erstellen** > **Windows 10 und höher** > **Microsoft Defender Antivirus**).

Mit den neuen Einstellungen können Sie nun UNC-Dateifreigaben als Quellspeicherorte zum Herunterladen von Definitionsaktualisierungen hinzufügen und die Reihenfolge festlegen, in der die verschiedenen Quellspeicherorte kontaktiert werden. Mit den neuen Einstellungen werden die folgenden Defender-CSPs verwaltet:

- [signatureupdatefilesharessources](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefilesharessources)
- [signatureupdatefallbackorder](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefallbackorder)

### <a name="endpoint-detection-and-response-policy-for-onboarding-tenant-attached-devices-to-mdatp-is-moving-out-of-preview---7303816-----"></a>Ende der Vorschauphase für die Richtlinie „Endpunkterkennung und -antwort“ für das Onboarding von Geräten mit Mandantenanfügung an Microsoft Defender Advanced Threat Protection (MDATP)<!-- 7303816   -->
Als Teil der Endpunktsicherheit in Intune wechselt die Unterstützung von Richtlinien des Typs „Endpunkterkennung und -antwort“ für den Einsatz mit von Configuration Manager verwalteten Geräten bald aus der Vorschauphase in den Status „Allgemein verfügbar“ (**Endpunktsicherheit** > **Endpunkterkennung und -antwort** > **Richtlinie erstellen** > **Windows 10 und Windows Server**). Wenn Sie [Mandantenanfügung für Configuration Manager](../../configmgr/tenant-attach/device-sync-actions.md) konfigurieren, können Sie anschließend diese Richtlinien für das Onboarding von Geräten, die von Configuration Manager verwaltet werden, in Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) nutzen. 

### <a name="improvements-for-the-security-baselines-node---7433136-----"></a>Verbesserungen für den Knoten „Sicherheitsbaselines“<!-- 7433136   -->
Um die Zweckmäßigkeit des Knotens „Sicherheitsbaseline“ im Microsoft Endpoint Manager Admin Center zu verbessern, entfernen wir die Registerkarte *Übersicht* für jede Baseline und öffnen stattdessen die Registerkarte **Profil** für Baselines (**Endpunktsicherheit** > **Sicherheitsbaselines** > *Baseline*).

Auf der Seite *Übersicht* für jede Baseline werden Diagramme und Kacheln angezeigt, die die Ergebnisse der letzten von Ihnen bereitgestellten Baselineversion aggregieren. Wenn Sie eine Version untersuchen, um mehr Details zu erfahren, werden diese Informationen von dem, was Sie sehen, dupliziert. Nachdem die Seite *Übersicht* entfernt wurde, bleiben diese Diagramme und Aggregatdetails verfügbar, wenn Sie die Version direkt detailliert untersuchen.  

### <a name="firewall-rule-migration-tool-preview---6423187----"></a>Vorschau auf das Migrationstool für Firewallregeln<!-- 6423187  -->
Als Public Preview-Version bieten wir ein auf PowerShell basierendes Tool an, mit dem die Firewallregeln von Windows Defender migriert werden können. Wenn Sie das Tool installieren und ausführen, erstellt es für Intune automatisch Richtlinien für Firewallregeln zur Endpunktsicherheit, die auf der aktuellen Konfiguration eines Windows 10-Clients basieren.

### <a name="new-settings-for-the-device-control-profile-in-endpoint-security-attack-surface-reduction-policy--7032084---"></a>Neue Einstellungen für das Profil „Gerätesteuerung“ in der Richtlinie zur Verringerung der Angriffsfläche für Endpunktsicherheit<!--7032084 -->
Wir fügen auf Windows 10-Geräten für mehr Endpunktsicherheit dem Profil „Gerätesteuerung“ mehrere Einstellungen für die Richtlinie zur Verringerung der Angriffsfläche hinzu (**Endpunktsicherheit** > **Angriffsfläche verringern** > **Richtlinie erstellen** > **Windows 10 und höher** > **Gerätesteuerung**). 

Die neuen Einstellungen entsprechen den Einstellungen, die derzeit in [Geräteeinschränkungsprofilen](../configuration/device-restrictions-windows-10.md) für *Gerätekonfiguration* verfügbar sind. Die Einstellungen, die dem Profil *Gerätesteuerung* hinzugefügt werden, sollen verschiedene Bluetooth-Einstellungen umfassen.  


<!-- ***********************************************-->
## <a name="notices"></a>Benachrichtigungen

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Weitere Informationen:

Details zu aktuellen Entwicklungen finden Sie unter [Neuerungen in Microsoft Intune](whats-new.md).
