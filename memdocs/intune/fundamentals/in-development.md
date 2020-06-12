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
ms.openlocfilehash: 90039e9bb75bcf7c266ac033408f87d37e27ef8d
ms.sourcegitcommit: 7a5196d4d9736c5cd52a23155c479523e52a097d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/05/2020
ms.locfileid: "84436753"
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

### <a name="improvements-to-devices-page-of-iosipados-and-macos-company-portals---6055001----"></a>Verbesserungen an der Seite „Geräte“ in iOS/iPadOS- und macOS-Unternehmensportalen<!-- 6055001  -->
Wir haben einige Verbesserungen hinsichtlich der Benutzerfreundlichkeit der Seite **Geräte** in der Unternehmensportal-App für iOS/iPadOS und Mac vorgenommen. Wir haben die Seite **Geräte** überarbeitet, um ihr ein modernere Erscheinungsbild zu geben. Außerdem sind jetzt die Geräteinformationen besser organisiert. Durch Verwendung einer einzelnen Spalte mit definierten Abschnittsüberschriften können die iOS/iPadOS-und macOS-Benutzer Ihrer Organisation den Status Ihrer Geräte problemlos überprüfen, um sicherzustellen, dass ihr Schutz gewährleistet ist und sie auf die Ressourcen Ihrer Organisation zugreifen können. Darüber hinaus haben wir für Benutzer, deren Geräte nicht kompatibel sind, ein klareres Messaging und zusätzliche Problembehandlungsschritte hinzugefügt. Weitere Informationen über das Unternehmensportal finden Sie unter [Anpassen von Intune-Unternehmensportal-Apps, der Unternehmensportal-Website und der Intune-App](../apps/company-portal-app.md).

### <a name="improvements-to-the-company-portal-for-macos-enrollment-experience---6444452----"></a>Verbesserungen am Unternehmensportal für die macOS-Registrierung<!-- 6444452  -->
Das Unternehmensportal für die macOS-Registrierung bietet jetzt einen einfacheren Registrierungsprozess, der stärker an das Unternehmensportal für die iOS-Registrierung angeglichen ist. Gerätebenutzern wird Folgendes angezeigt:  
- Eine schlankere Benutzeroberfläche  
- Eine verbesserte Prüfliste für die Registrierung  
- Deutlichere Anweisungen zum Registrieren ihrer Geräte  
- Verbesserte Optionen zur Problembehandlung  

Weitere Informationen über das Unternehmensportal finden Sie unter [Anpassen von Intune-Unternehmensportal-Apps, der Unternehmensportal-Website und der Intune-App](../apps/company-portal-app.md).

### <a name="use-autonomous-single-app-mode-settings-to-configure-the-ios-company-portal-to-be-a-sign-insign-out-app---7055619----"></a>Verwenden Sie Einstellungen für den autonomen Einzelanwendungsmodus, um das iOS-Unternehmensportal als App für die Anmeldung/Abmeldung zu konfigurieren.<!-- 7055619  -->
Sie können das iOS-Unternehmensportal so konfigurieren, dass es den autonomen Einzelanwendungsmodus (Autonomous Single App Mode, ASAM) verwendet. Mit den ASAM-Einstellungen in der Microsoft Endpoint Manager-Konsole können Sie das iOS-Unternehmensportal so konfigurieren, dass bei Abmeldung und Anmeldung der Einzelanwendungsmodus aktiviert bzw. deaktiviert wird. Wenn sich das Unternehmensportal im ASAM-Modus befindet, können Benutzer keine andere App oder die Home-Taste des Geräts verwenden, bis sie sich im Unternehmensportal anmelden. Nach der Abmeldung wechselt das Unternehmensportal wieder in den Einzelanwendungsmodus. 

Um das Unternehmensportal für den ASAM-Modus zu konfigurieren, wählen Sie im Microsoft Endpoint Manager **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus. Wählen Sie **iOS/iPadOS** als Plattform aus, und wählen Sie **Geräteeinschränkungen** als Profil aus. Wählen Sie auf der Registerkarte **Konfigurationseinstellungen** die Option **Modus der autonomen einzelnen App** aus. Geben Sie `Company Portal` für den **App-Namen** und `com.app.CompanyPortal` für die **App-Bündel-ID** an. Weitere Informationen finden Sie unter [Autonomer Einzelanwendungsmodus (ASAM)](../configuration/device-restrictions-ios.md#autonomous-single-app-mode-asam) und [Einzelanwendungsmodus](https://support.apple.com/guide/mdm/single-app-mode-mdm80a981/1/web/1).

<!-- ***********************************************-->
## <a name="device-configuration"></a>Gerätekonfiguration

### <a name="set-device-compliance-state-from-third-party-mdm-partners---6361689-----"></a>Festlegen des Konformitätszustands von Geräten von MDM-Drittanbieterpartnern<!-- 6361689   -->
In Kürze können Sie den Konformitätszustand von iOS- oder Android-Geräten, die von MDM-Drittanbieterpartnern (Mobile Device Management) verwaltet werden, in Azure Active Directory (Azure AD) festlegen.

Wenn Intune für die Partnerkonformität konfiguriert ist, werden dann Konformitätsdaten für Geräte, die vom MDM-Drittanbieterpartner verwaltet werden, zur Konformitätsbewertung an Intune gesendet. Die Ergebnisse werden dann an Azure AD weitergeleitet, wo die Konformitätsdaten verwendet werden, um Ihre Richtlinien für den bedingten Zugriff für diese Geräte zu erzwingen.

In Kürze werden die folgenden Partner unterstützt:
- VMware WorkspaceONE (zuvor bekannt als AirWatch)

Um einen Gerätekonformitätspartner zu aktivieren, verwenden Sie einen neuen Knoten im Microsoft Endpoint Manager Admin Center: **Mandantenverwaltung** > **Connectors und Token** > **Partnerkonformitätsverwaltung**, wo Sie dann **Konformitätspartner hinzufügen** auswählen.

### <a name="add-a-link-to-your-company-portal-support-website-to-emails-for-noncompliance---7225498------"></a>Hinzufügen eines Links zur Support-Website Ihres Unternehmensportals zu E-Mails bei Nichtkonformität<!-- 7225498    -->
Wir ergänzen die E-Mail-Benachrichtigungsvorlage um eine neue Einstellung: Sie fügt den Link zu Ihrer Unternehmensportal-Website in die E-Mail-Benachrichtigungen ein, die an Benutzer von nicht konformen Geräten gesendet werden. (**Endpoint Security** > **Gerätekonformität** > **Benachrichtigungen** > **Benachrichtigung erstellen**).  Benutzer, die eine E-Mail erhalten, weil Sie über ein nicht konformes Gerät verfügen, können den Link zum Öffnen einer Website verwenden, wo sie mehr darüber erfahren, warum Ihr Gerät nicht konform ist.

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>Neue FileVault-Einstellung für macOS-Endpoint Protection-Gerätekonfigurationsrichtlinie<!-- 5459801   -->
Wir fügen der FileVault-Kategorie innerhalb der [macOS-Endpoint Protection](../protect/endpoint-protection-macos.md)-Vorlage eine neue Einstellung hinzu: „Wiederherstellungsschlüssel ausblenden“ (**Geräte** > **Konfigurationsprofile** > **Profil erstellen**, wählen Sie **macOS** für *Plattform* und dann **Endpoint Protection** für *Profiltyp* aus). Mit dieser Einstellung wird der persönliche Schlüssel während der FileVault 2-Verschlüsselung für den Endbenutzer ausgeblendet. Ein Gerätebenutzer kann den persönlichen Wiederherstellungsschlüssel jederzeit über die iOS-Unternehmensportal-App oder über die Website des Unternehmensportals für das verschlüsselte macOS-Gerät anzeigen. Navigieren Sie einfach zu „Gerätedetails“, und klicken Sie auf *Wiederherstellungsschlüssel abrufen*, um den persönlichen Wiederherstellungsschlüssel anzuzeigen.

Diese Einstellung ist in der zuvor erstellten Richtlinie nicht verfügbar. Sie müssen die FileVault-Richtlinien neu erstellen, um diese Einstellung für die Verwendung zu konfigurieren. 

### <a name="configure-content-caching-on-macos-devices---7106872---"></a>Konfigurieren des Content Caching auf macOS-Geräten<!-- 7106872 -->
Auf macOS-Geräten können Sie ein Konfigurationsprofil erstellen, mit dem das Content Caching konfiguriert wird (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **macOS** für Plattform > **Gerätefunktionen** für Profil). Verwenden Sie diese Einstellungen unter anderem, um den Cache zu löschen, die Cache-Freigabe zuzulassen und ein Cachelimit auf dem Datenträger festzulegen.

Weitere Informationen zum Content Caching finden Sie unter [Content Caching](https://developer.apple.com/documentation/devicemanagement/contentcaching) (öffnet die Apple-Website).

Informationen zu den Funktionen, die Sie derzeit konfigurieren können, finden Sie unter [macOS-Gerätefunktionseinstellungen in Intune](../configuration/macos-device-features-settings.md).

Gilt für:
- macOS

### <a name="new-vpn-settings-for-windows-10-and-newer-devices---6602122----"></a>Neue VPN-Einstellungen für Windows 10 und neuere Geräte<!-- 6602122  -->
Wenn Sie ein VPN-Profil mit dem IKEv2-Verbindungstyp erstellen, können Sie jetzt neue Einstellungen konfigurieren (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **Windows 10 und höher** für Plattform > **VPN** für Profil > **Basis-VPN**):

- **Gerätetunnel**: Ermöglicht Geräten den automatischen Verbindungsaufbau zu einem VPN, ohne dass eine Benutzerinteraktion, einschließlich Benutzeranmeldung, erforderlich ist. Diese Funktion erfordert, dass Sie **Always on** aktivieren und **Computerzertifikate** als Authentifizierungsmethode verwenden.
- Einstellungen der Kryptografie-Suite: Konfigurieren Sie die Algorithmen, die zum Sichern von IKE-und untergeordneten Sicherheitszuordnungen verwendet werden, wodurch Sie die Client-und Servereinstellungen aufeinander abstimmen können.

Informationen zu den Einstellungen, die Sie konfigurieren können, finden Sie unter [Windows-Geräteeinstellungen zum Hinzufügen von VPN-Verbindungen mithilfe von Intune](../configuration/vpn-settings-windows-10.md).

Gilt für:
- Windows 10 und höher

### <a name="block-shared-ipad-temporary-sessions-on-shared-ipad-devices---6613794---"></a>Blockieren von temporären Shared iPad-Sitzungen auf Shared iPad-Geräten blockieren<!-- 6613794 -->
In Intune gibt es die neue Einstellung **Temporäre Shared iPad-Sitzungen blockieren**. Sie blockiert temporäre Sitzungen auf Shared iPad-Geräten (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **iOS/iPadOS** für Plattform > **Geräteeinschränkungen** für Profiltyp > **Shared iPad**). Wenn diese Einstellung aktiviert ist, können Endbenutzer das Gastkonto nicht verwenden. Sie müssen sich mit Ihrer verwalteten Apple-ID und dem dazugehörigen Kennwort am Gerät anmelden. 

Weitere Informationen zu den konfigurierbaren Einstellungen finden Sie unter [iOS- und iPadOS-Geräteeinstellungen zum Zulassen oder Einschränken von Funktionen](../configuration/device-restrictions-ios.md).

Gilt für:
- Shared iPad-Geräte, auf denen iOS/iPadOS 13,4 und höher ausgeführt wird

### <a name="use-microsoft-launcher-as-the-default-launcher-for-fully-managed-android-enterprise-devices---4927976----"></a>Verwenden von Microsoft Launcher als Standardstartprogramm für vollständig verwaltete Android Enterprise-Geräte<!-- 4927976  -->
Auf Geräten von Android Enterprise-Gerätebesitzern können Sie Microsoft Launcher als Standardstartprogramm für vollständig verwaltete Geräte festlegen (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **Android Enterprise** für Plattform > **Gerätebesitzer** > **Geräteeinschränkungen** für Profil > **Gerätefunktionen**). Verwenden Sie App-Konfigurationsrichtlinien, um alle anderen Microsoft Launcher-Einstellungen zu konfigurieren. 

Außerdem gibt es einige weitere Aktualisierungen der Benutzeroberfläche. Unter anderem wurde **Dedizierte Geräte** in **Gerätefunktionen** umbenannt.

Informationen zu den Funktionen, die Sie einschränken können, finden Sie unter [Android Enterprise-Geräteeinstellungen zum Zulassen oder Einschränken von Features mit Intune](../configuration/device-restrictions-android-for-work.md). 

Gilt für:
- Vollständig verwaltete Geräte von Android Enterprise-Gerätebesitzern (COBO)

### <a name="add-new-schema-settings-and-search-for-existing-schema-settings-using-oemconfig-on-android-enterprise---6394386----"></a>Hinzufügen neuer Schemaeinstellungen und Suchen nach vorhandene Schemaeinstellungen mithilfe von OEMConfig unter Android Enterprise<!-- 6394386  -->
In Intune können Sie mithilfe von OEMConfig die Einstellungen auf Android Enterprise-Geräten verwalten (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **Android Enterprise** für Plattform > **OEMConfig** für Profil). Wenn Sie den **Konfigurations-Designer**verwenden, werden die Eigenschaften im App-Schema angezeigt. Im **Konfigurations-Designer** können Sie nun folgende Aktionen ausführen:
- Hinzufügen neuer Einstellungen zum App-Schema
- Suchen nach neuen und vorhandenen Einstellungen im App-Schema

Weitere Informationen zu OEMConfig-Profilen in Intune finden Sie unter [Verwenden und Verwalten von Android Enterprise-Geräten mit OEMConfig in Microsoft Intune](../configuration/android-oem-configuration-overview.md).

Gilt für:
- Android Enterprise

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Geräteregistrierung

### <a name="automated-device-enrollment-sync-errors---6988214---"></a>Synchronisierungsfehler bei der automatischen Geräteregistrierung<!-- 6988214 -->
Für iOS/iPadOS- und macOS-Geräte werden neue Fehler gemeldet, einschließlich:
- Ungültige Zeichen in der Telefonnummer oder Feld ist leer 
- Ungültiger oder leerer Konfigurationsname für das Profil 
- Ungültiger/abgelaufener Cursorwert oder kein Cursor gefunden
- Zurückgewiesenes oder abgelaufenes Token 
- Das Feld „Abteilung“ ist leer oder enthält zu viele Zeichen 
- Das Profil wurde von Apple nicht gefunden, und es muss ein neues erstellt werden. 
- Die Anzahl der entfernten Apple Business Manager-Geräte wird zur Seitenübersicht hinzugefügt, auf der Sie den Status Ihrer Geräte sehen.

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>BYOD-Geräte können VPN für die Bereitstellung verwenden<!--5015344 -->
Mit der neuen Autopilot-Profiloption **Überprüfung der Domänenkonnektivität überspringen** können Sie hybrid in Azure AD eingebundene Geräte ohne Zugriff auf Ihr Unternehmensnetzwerk mithilfe Ihres eigenen Drittanbieter-Win32-VPN-Clients bereitstellen. Die neue Option finden Sie unter [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Geräte**  > **Windows** > **Windows-Registrierung** > **Bereitstellungsprofile** > **Profil erstellen** > **Willkommensseite**.

### <a name="shared-ipads-for-business--6367326---"></a>Gemeinsam genutzte iPads für Unternehmen<!--6367326 -->
Sie können mit Intune und Apple Business Manager problemlos und sicher gemeinsam genutzte iPads einrichten, sodass Geräte durch mehrere Mitarbeiter verwendet werden können. Das Apple-Feature [Gemeinsam genutztes iPad](https://developer.apple.com/education/shared-ipad/) bietet eine personalisierte Benutzeroberfläche für mehrere Benutzer, während Benutzerdaten beibehalten werden. Durch Verwendung einer verwalteten Apple-ID können Benutzer auf ihre Apps, Daten und Einstellungen zugreifen, nachdem sie sich in ihrer Organisation an einem gemeinsam genutzten iPad angemeldet haben. Gemeinsam genutzte iPads arbeiten mit Verbundidentitäten.

Wechseln Sie zur Anzeige dieses Features zu [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Geräte** > **iOS** > **iOS-Registrierung** > **Token für Registrierungsprogramm** > ein Token auswählen > **Profile** > **Profil erstellen** > **iOS**. Wählen Sie auf der Seite **Verwaltungseinstellungen** die Option **Ohne Benutzeraffinität registrieren** aus. Daraufhin wird die Option **Gemeinsam genutztes iPad** angezeigt.

**Gilt für:** iPadOS 13.4 und höher. In diesem Release wird Unterstützung für temporäre Sitzungen mit gemeinsam genutzten iPads hinzugefügt, sodass Benutzer ohne eine verwaltete Apple-ID auf ein Gerät zugreifen können. Nach der Abmeldung werden alle Benutzerdaten vom Gerät gelöscht, sodass das Gerät sofort wieder zur Verwendung bereitsteht, ohne dass eine Gerätezurücksetzung durchgeführt werden muss. 

<!-- ***********************************************-->
## <a name="device-management"></a>Geräteverwaltung

### <a name="change-primary-user-on-co-managed-devices--7319183---"></a>Ändern des primären Benutzers auf gemeinsam verwalteten Geräten<!--7319183 -->
Sie können den primären Benutzer eines Geräts für gemeinsam verwaltete Windows-Geräte ändern. Weitere Informationen zum Suchen und ändern dieses Benutzers finden Sie unter [Suchen des primären Benutzers eines Intune-Geräts](../remote-actions/find-primary-user.md).

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Unterstützung von PowerShell-Skripts für BYOD-Geräte<!-- 1862833  -->
PowerShell-Skripts unterstützen bei Azure AD registrierte Geräte in Intune. Weitere Informationen zu PowerShell finden Sie unter [Verwenden von PowerShell-Skripts auf Windows 10-Geräten in Intune](../apps/intune-management-extension.md). Diese Funktion unterstützt keine Geräte, auf denen die Windows 10 Home-Edition ausgeführt wird.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics enthält das Gerätedetailprotokoll<!--6014987  -->
Intune-Gerätedetailprotokolle werden unter **Berichte** > **Log Analytics** bereitgestellt. Sie können Gerätedetails korrelieren, um benutzerdefinierte Abfragen und Azure-Workbooks zu erstellen.

### <a name="setting-the-intune-primary-user-also-sets-the-azure-ad-owner-property--7319227---"></a>Beim Festlegen des primären Intune-Benutzers wird auch die Azure AD Owner-Eigenschaft festgelegt.<!--7319227 -->
Mit diesem geplanten Feature wird die Owner-Eigenschaft auf neu registrierten in Azure AD Hybrid eingebundenen Geräten automatisch gleichzeitig festgelegt, wenn der primäre Intune-Benutzer festgelegt wird. Weitere Informationen zum primären Benutzer finden Sie unter [Suchen des primären Benutzers eines Intune-Geräts](../remote-actions/find-primary-user.md).

Dies ist eine Änderung am Registrierungsprozess und gilt nur für neu registrierte Geräte. Bei vorhandenen in Azure AD Hybrid eingebundenen Geräten müssen Sie die Azure AD Owner-Eigenschaft manuell aktualisieren. Zu diesem Zweck können Sie die [Funktion zum Ändern des primären Benutzers](../remote-actions/find-primary-user.md#change-a-devices-primary-user) oder [ein Skript](https://github.com/microsoftgraph/powershell-intune-samples/tree/master/ManagedDevices) verwenden.

Wenn Windows 10-Geräte den Status „In Azure Hybrid Directory eingebunden“ erhalten, wird der erste Benutzer des Geräts in Endpoint Manager zum primären Benutzer.  Derzeit wird der Benutzer nicht für das entsprechende Azure AD-Geräteobjekt festgelegt. Dies führt zu einer Inkonsistenz beim Vergleich der *Owner*-Eigenschaft aus einem Azure AD Portal mit der Eigenschaft *Primärer Benutzer* im Microsoft Endpoint Manager Admin Center. Die Azure AD Owner-Eigenschaft wird zum Sichern des Zugriffs auf die BitLocker-Wiederherstellungsschlüssel verwendet. Die Eigenschaft wird auf in Azure AD Hybrid eingebundenen Geräten nicht aufgefüllt. Diese Einschränkung verhindert das Einrichten der Self-Service-Wiederherstellung von BitLocker aus Azure AD. Dieses geplante Feature beseitigt diese Einschränkung.

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

### <a name="remote-lock-pin-availability-for-macos-devices--7281557--"></a>Verfügbarkeit von Remote-Sperr-PINs für macOS-Geräte<!--7281557-->
Die Verfügbarkeit von Remote-Sperr-PINs für macOS-Geräte wird von 7 Tagen auf 30 Tage verlängert.

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
