---
title: 'In der Entwicklung: Microsoft Intune'
titleSuffix: ''
description: In der Entwicklung befindliche Microsoft Intune-Features
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/03/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2e5c7ce18cc00934438e945933188d9634b36653
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79362315"
---
# <a name="in-development-for-microsoft-intune---march-2020"></a>In der Entwicklung befindliche Microsoft Intune-Features: März 2020

Um Ihnen bei Ihrer Vorbereitung und Planung zu helfen, sind auf dieser Seite Updates und Features der Intune-Benutzeroberfläche aufgeführt, die sich in der Entwicklung befinden, aber noch nicht freigegeben wurden. Zusätzlich zu den Informationen auf dieser Seite gilt Folgendes: 

- Wenn wir davon ausgehen, dass Sie vor einer Änderung Maßnahmen ergreifen müssen, werden wir einen ergänzenden Beitrag im Office-Nachrichtencenter veröffentlichen.
- Wenn ein Feature in die Produktionsumgebung wechselt, wird die Featurebeschreibung von dieser Seite auf die Seite [Neuerungen in Microsoft Intune](whats-new.md) verschoben, unabhängig davon, ob es sich um eine Vorschauversion handelt oder ob das Feature bereits allgemein verfügbar ist.
- Diese Seite und die Seite [Neuerungen](whats-new.md) werden regelmäßig aktualisiert. Überprüfen Sie, ob weitere Updates vorliegen.
- In der [Roadmap für Microsoft 365](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) finden Sie strategische Ziele und Zeitpläne.

> [!NOTE]
> Diese Seite spiegelt die aktuellen Planungen von Microsoft für Intune-Funktionen in einem zukünftigen Release wider. Termine und einzelne Features können sich ändern. Auf dieser Seite werden nicht alle Features beschrieben, die gerade entwickelt werden.

**RSS-Feed**: Bleiben Sie auf dem Laufenden, wenn diese Seite aktualisiert wird, indem Sie die folgende URL kopieren und in Ihren Feedreader einfügen: `https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`.

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

### <a name="retarget-web-clips-to-microsoft-edge-on-iosipados-devices---5455276---"></a>Festlegen von Microsoft Edge als Zielbrowser für Webclips auf iOS-/iPadOS-Geräten<!-- 5455276 -->
Webclips, die als angeheftete Web-Apps auf iOS-/iPadOS-Geräten fungieren, müssen aktualisiert werden. Neu bereitgestellte Webclips werden in Microsoft Edge geöffnet, anstatt in Intune Managed Browser, wenn sie in einem geschützten Browser geöffnet werden müssen. Bereits vorhandene Webclips müssen neu zugewiesen werden, damit sie in Microsoft Edge anstatt in Managed Browser geöffnet werden.

### <a name="macos-and-ios-company-portal-updates---5779439-5780234----"></a>Aktualisierungen des macOS- und iOS-Unternehmensportals<!-- 5779439, 5780234  -->
Der Bereich „Profil“ des macOS- und iOS-Unternehmensportals wird aktualisiert, sodass die Schaltfläche „Abmelden“ integriert wird. Darüber hinaus enthält dieses Update Verbesserungen der Benutzeroberfläche im Bereich „Profil“ im macOS-Unternehmensportal. Weitere Informationen zum Unternehmensportal finden Sie unter [Konfigurieren der Microsoft Intune-Unternehmensportal-App](../apps/company-portal-app.md).

### <a name="updates-to-branding-and-customization-pane---5236032---"></a>Updates für den Bereich „Branding und Anpassung“<!-- 5236032 -->
Wir aktualisieren aktuell den Intune-Bereich mit der Bezeichnung „Branding und Anpassung“ einschließlich der folgenden Verbesserungen:

- Umbenennung des Bereichs in **Anpassung**
- Verbesserung der Organisation und des Designs der Einstellungen
- Verbesserung des Einstellungstexts und der QuickInfos

Navigieren Sie zum [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431), und klicken Sie auf **Mandantenverwaltung** > **Anpassung**, um diese Einstellung in Intune zu finden. Weitere Informationen zur vorhandenen Anpassung finden Sie unter [Konfigurieren der Microsoft Intune-Unternehmensportal-App](../apps/company-portal-app.md).

### <a name="configure-the-ios-microsoft-azure-ad-sso-app-extension---567534----"></a>Konfigurieren der SSO-App-Erweiterung für iOS von Microsoft Azure AD<!-- 567534  -->
Das Microsoft Azure AD-Team entwickelt gerade eine App-Erweiterung zum Umleiten für einmaliges Anmelden (SSO), um Benutzern von iOS- und iPadOS-Geräten mit Version 13.0 oder höher den nahtlosen Zugriff auf Microsoft-Apps und -Websites mit dem einmaligen Anmelden zu ermöglichen. Wenn die App-Erweiterung für SSO von AAD veröffentlicht wird, können Sie die SSO-Erweiterung mit dem Profil **Gerätefunktionen** > **App-Erweiterung für einmaliges Anmelden** in der Verwaltungskonsole mit nur wenigen Klicks konfigurieren.

Weitere Informationen zu App-Erweiterungen für SSO für iOS oder dem Konfigurieren von Gerätefunktionen finden Sie unter [App-Erweiterung für einmaliges Anmelden](../configuration/device-features-configure.md#single-sign-on-app-extension).

### <a name="company-portal-for-ios-to-support-landscape-mode--6048329----"></a>Unternehmensportal für iOS zur Unterstützung des Querformats<!--6048329  -->
Benutzer können über die Bildschirmausrichtung ihrer Wahl ihre Geräte registrieren, Apps suchen und IT-Support erhalten. Die App erkennt automatisch Bildschirme und passt diese an das Hoch- oder Querformat an, es sei denn, Benutzer sperren den Bildschirm im Hochformat.

### <a name="configure-if-enrollment-is-available-in-company-portal-for-android-and-ios---4260128-idready-idstaged---"></a>Konfigurieren, ob die Registrierung im Unternehmensportal für Android und iOS verfügbar ist<!-- 4260128 idready idstaged -->
Es wird eine neue Einstellung verfügbar, mit der Sie konfigurieren können, ob die Geräteregistrierung im Unternehmensportal auf Android- und iOS-Geräten mit oder ohne Eingabeaufforderungen bzw. nicht für Benutzer verfügbar wird. Navigieren Sie zum [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431), und klicken Sie auf **Mandantenverwaltung** > **Anpassung** > **Bearbeiten** > **Geräteregistrierung**, um diese Einstellung in Intune zu finden. Weitere Informationen zur Anpassung des Unternehmensportals finden Sie unter [Konfigurieren der Microsoft Intune-Unternehmensportal-App](../apps/company-portal-app.md).

### <a name="improved-sign-in-experience-in-company-portal-for-android---6103997----"></a>Verbesserte Anmeldefunktion im Unternehmensportal für Android<!-- 6103997  -->
Wir aktualisieren das Layout mehrerer Anmeldebildschirme in der Unternehmensportal-App für Android, um die Benutzeroberfläche moderner, einfacher und sauberer zu gestalten.

<!-- ***********************************************-->
## <a name="device-configuration"></a>Gerätekonfiguration

### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>Gerätekonfigurationsprofil für das kabelgebundene Netzwerk für macOS-Geräte<!-- 3508686  -->
Ein neues Gerätekonfigurationsprofil für macOS ist verfügbar, das kabelgebundene Netzwerke konfiguriert. Navigieren Sie dafür zu **Gerätekonfiguration** > **Profile** > **Profil erstellen** > **macOS**, um die Plattform auszuwählen, und wählen Sie dann den Profiltyp **Kabelgebundenes Netzwerk** aus. Verwenden Sie dieses Feature zum Erstellen von 802.1x-Profilen für die Verwaltung von kabelgebundenen Netzwerken, und stellen Sie dieses Netzwerke für Ihre macOS-Geräte bereit.

Gilt für:
- macOS

### <a name="vpn-profiles-with-ikev2-vpn-connections-can-use-always-on-with-iosipados-devices----1947932----"></a>VPN-Profile mit IKEv2-VPN-Verbindungen können Always On auf iOS-/iPadOS-Geräten verwenden <!-- 1947932  -->
Auf iOS-/iPadOS-Geräten können Sie ein VPN-Profil erstellen, das eine IKEv2-Verbindung verwendet. Navigieren Sie hierfür zu **Gerätekonfiguration** > **Profile** > **Profil erstellen** > **iOS/iPadOS**, um die Plattform auszuwählen, und wählen Sie anschließend den Profiltyp **VPN** aus. In einem zukünftigen Update können Sie Always On mit IKEv2 konfigurieren. Wenn die IKEv2-VPN-Profile konfiguriert sind, stellen sie automatisch eine Verbindung zum VPN her und bleiben verbunden bzw. stellen im Fall eines Verbindungsverlusts die Verbindung schnell wieder her. Die Verbindung bleibt bestehen, selbst wenn das Netzwerk gewechselt wird oder Geräte neu gestartet werden.

Unter iOS/iPadOS ist das Always On-VPN auf IKEv2-Profile beschränkt.

Die derzeit konfigurierbaren IKEv2-Einstellungen finden Sie unter [Hinzufügen von VPN-Einstellungen auf iOS-/iPadOS-Geräten in Microsoft Intune](../configuration/vpn-settings-ios.md#ikev2-settings).

Gilt für:
- iOS

### <a name="improved-user-interface-experience-when-creating-configuration-profiles-on-iosipados-and-macos-devices---5569008-5569039-5569057-5569110-5569116-5569131-5569139-5569153-5859984----"></a>Verbesserte Benutzeroberfläche für das Erstellen von Konfigurationsprofilen auf iOS-/iPadOS- und macOS-Geräten<!-- 5569008-5569039-5569057-5569110-5569116-5569131-5569139-5569153-5859984  -->
Wenn Sie ein Profil für iOS-/iPadOS- oder macOS-Geräte erstellen, wird das Microsoft Endpoint Manager Admin Center entsprechend aktualisiert. Diese Änderung wirkt sich auf die folgenden Gerätekonfigurationsprofile aus. (Navigieren Sie zu **Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **iOS** oder **macOS**, um die Plattform auszuwählen):

- Benutzerdefiniert: iOS/iPadOS, macOS
- Gerätefunktionen: iOS/iPadOS, macOS
- Geräteeinschränkungen: iOS/iPadOS, macOS
- Endpoint Protection: macOS
- Erweiterungen: macOS
- Einstellungsdatei: macOS

### <a name="improved-user-interface-experience-when-creating-oemconfig-configuration-profiles-on-android-enterprise-devices---5568645-----"></a>Verbesserte Benutzeroberfläche für das Erstellen von OEMConfig-Konfigurationsprofilen auf Android Enterprise-Geräten<!-- 5568645   -->
Wenn Sie ein OEMConfig-Profil für Android Enterprise-Geräte erstellen oder bearbeiten, wird das Microsoft Endpoint Manager Admin Center entsprechend aktualisiert. Nach der Aktualisierung wird eine übersichtliche Zusammenfassung der Einstellungen angezeigt, die Sie konfiguriert haben. Diese Änderungen wirken sich auf die OEMConfig-Gerätekonfigurationsprofile aus. Navigieren Sie zu **Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **Android Enterprise**, um die Plattform auszuwählen, und wählen Sie dann den Profiltyp **OEMConfig** aus.

Diese Funktion gilt für:
- Android Enterprise 

### <a name="enterprise-app-trust-settings-modification-setting-will-be-removed-from-iosipados-device-restriction-profiles---6225131----"></a>Änderung der Vertrauenseinstellungen für Unternehmens-Apps wird von iOS/iPadOS-Geräteeinschränkungsprofilen entfernt<!-- 6225131  -->
Sie können auf iOS/iPadOS-Geräten ein Geräteeinschränkungsprofil erstellen (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **iOS/iPadOS** (für Plattform) > **Geräteeinschränkungen** (für Profiltyp)). Die Einstellung **Änderung der Vertrauenseinstellungen für Unternehmens-Apps** wird von Apple und Intune entfernt. Wenn Sie diese Einstellung derzeit in einem Profil verwenden, hat diese keine Auswirkung und wird in Ihrem Profil beibehalten, bis Sie ein neues Profil erstellen. Diese Einstellung wird auch aus jeder Berichterstattung in Intune entfernt.

Gilt für:
- iOS/iPadOS

Navigieren Sie zu [iOS- und iPadOS-Geräteeinstellungen zum Zulassen oder Einschränken von Funktionen mit Intune](../configuration/device-restrictions-ios.md), um die Einstellungen anzuzeigen, die Sie einschränken können.

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>Einstellungen und Werte für das Gerätekonfigurationsprofil werden für Windows-Plattformen aktualisiert<!-- 4091122 -->
Beim Erstellen von Gerätekonfigurationsprofilen für Windows-Plattformen (**Geräte** > **Konfigurationsprofile** >  **Profil erstellen** > beliebige **Windows**-Option für Plattform) unterscheiden sich einige Einstellungen und deren Werte vom CSP, was verwirrend sein kann. Die Einstellungsnamen und ihre Werte werden aktualisiert, sodass sie eindeutig zu verstehen sind.

Gilt für:

- Gerätekonfigurationsprofile für Windows 10 oder höher
- Gerätekonfigurationsprofile für Windows Holographic for Business
- Gerätekonfigurationsprofile für Windows 8.1
- Gerätekonfigurationsprofile für Windows Phone 8.1

### <a name="improved-user-interface-experience-when-creating-device-restrictions-profiles-on-android-and-android-enterprise-devices---5841361---"></a>Verbesserte Benutzeroberfläche für das Erstellen von Gerätekonfigurationsprofilen auf Android- und Android Enterprise-Geräten<!-- 5841361 -->
Wenn Sie ein Profil für Android- oder Android Enterprise-Geräte erstellen, wird das Microsoft Endpoint Manager Admin Center entsprechend aktualisiert. Diese Änderung wirkt sich auf die folgenden Gerätekonfigurationsprofile aus (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **Android-Geräteadministrator** oder **Android Enterprise** für die Plattform):

- Geräteeinschränkungen: Android-Geräteadministrator
- Geräteeinschränkungen: Android Enterprise-Gerätebesitzer
- Geräteeinschränkungen: Android Enterprise-Arbeitsprofil

Weitere Informationen zu den Geräteeinschränkungen, die Sie konfigurieren können, finden Sie unter [Android-Geräte Administrator](../configuration/device-restrictions-android.md) und [Android Enterprise](../configuration/device-restrictions-android-for-work.md).

### <a name="delete-bundles-and-bundle-arrays-in-oemconfig-device-configuration-profiles-on-android-enterprise-devices---5550355----"></a>Löschen von Bundles und Bundlearrays in OEMConfig-Gerätekonfigurationsprofilen auf Android Enterprise-Geräten<!-- 5550355  -->
Auf Android Enterprise-Geräten können Sie OEMConfig-Profile erstellen und aktualisieren. Benutzer können mithilfe des **Konfigurations-Designers** in Intune Bundles und Bundlearrays löschen.

Weitere Informationen zu OEMConfig-Profilen finden Sie unter [Verwenden und Verwalten von Android Enterprise-Geräten mit OEMConfig in Microsoft Intune](../configuration/android-oem-configuration-overview.md).

Diese Funktion gilt für:
- Android Enterprise

### <a name="support-for-wpa-and-wpa2-in-ios-enterprise-wi-fi-profiles--6215273-----"></a>Unterstützung für WPA und WPA2 in Enterprise-WLAN-Profilen für iOS<!--6215273   -->
Wir fügen das Feld *Sicherheitstyp* zum [Enterprise-WLAN-Profil für iOS](../configuration/wi-fi-settings-ios.md) hinzu (**Geräte** > **Konfigurationsprofile** > **Profil erstellen**, und wählen Sie dann zunächst **iOS/iPadOS** für *Plattform* und **WLAN** für *Profil* aus). Dieses ähnelt den Optionen, die für ein einfaches WLAN-Profil für iOS verfügbar sind. Mit dieser Änderung können Sie neue Profile erstellen, die den Sicherheitstyp **WPA-Enterprise** oder **WPA/WPA2-Enterprise** angeben. Geben Sie dann eine Auswahl für den *EAP-Typ* an.

### <a name="new-user-experience-for-certificate-email-vpn-and-wi-fi-profiles---5615208-----"></a>Neue Benutzeroberflächen für Zertifikat-, E-Mail-, VPN- und WLAN-Profile<!-- 5615208   -->
Die [Benutzeroberflächen](../configuration/device-profile-create.md) im Endpoint Management Admin Center (**Geräte** > **Konfigurationsprofile** > **Profil erstellen**) zum Erstellen und Ändern der folgenden Profiltypen wird aktualisiert. Die neue Benutzeroberfläche umfasst die gleichen Einstellungen wie zuvor, ähnelt nun aber mehr der eines Assistenten, sodass weniger horizontales Scrollen erforderlich ist. Sie müssen vorhandene Konfigurationen angesichts der neuen Oberfläche nicht ändern.
- Abgeleitete Anmeldeinformation
- E-Mail
- PKCS-Zertifikat
- Importiertes PKCS-Zertifikat
- SCEP-Zertifikat
- Vertrauenswürdiges Zertifikat
- VPN
- WLAN

(**Geräte** > **Konfigurationsprofile** > **Profil erstellen**, und wählen Sie dann für *Profiltyp* eines der obigen Profile aus).

### <a name="configure-the-microsoft-defender-atp-app-for-macos-----5520115----"></a>Konfigurieren der Microsoft Defender ATP-App für macOS  <!-- 5520115  -->
In Kürze können Sie die [Einstellungen](../protect/endpoint-protection-macos.md) der Microsoft Defender ATP-App für Geräte konfigurieren, die macOS als Teil eines Endpoint Protection-Gerätekonfigurationsprofils ausführen (**Geräte** > **Konfigurationsprofile** > **Profil erstellen**, und wählen Sie dann **macOS** für *Plattform* und **Endpoint Protection** für *Profiltyp* aus). Es gibt acht Einstellungen für die macOS-Gerätekonfiguration. 

Defender ATP wird unter macOS 10.13 (High Sierra) und höher unterstützt, und die [Microsoft Defender ATP](../apps/apps-advanced-threat-protection-macos.md)-App muss auf dem Gerät bereitgestellt werden, *nachdem* diese Einstellungen angewendet wurden. Die Einstellungen sollten vor der Bereitstellung der App an das Gerät gesendet werden. Betaversionen von macOS werden nicht unterstützt.

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>Neue FileVault-Einstellung für macOS-Endpoint Protection-Gerätekonfigurationsrichtlinie<!-- 5459801   -->
Wir fügen der FileVault-Kategorie innerhalb der [macOS-Endpoint Protection](../protect/endpoint-protection-macos.md)-Vorlage eine neue Einstellung hinzu: „Wiederherstellungsschlüssel ausblenden“ (**Geräte** > **Konfigurationsprofile** > **Profil erstellen**, wählen Sie **macOS** für *Plattform* und dann **Endpoint Protection** für *Profiltyp* aus). Mit dieser Einstellung wird der persönliche Schlüssel während der FileVault 2-Verschlüsselung für den Endbenutzer ausgeblendet. Ein Gerätebenutzer kann den persönlichen Wiederherstellungsschlüssel jederzeit über die iOS-Unternehmensportal-App oder über die Website des Unternehmensportals für das verschlüsselte macOS-Gerät anzeigen. Navigieren Sie einfach zu „Gerätedetails“, und klicken Sie auf *Wiederherstellungsschlüssel abrufen*, um den persönlichen Wiederherstellungsschlüssel anzuzeigen.

Diese Einstellung ist in der zuvor erstellten Richtlinie nicht verfügbar. Sie müssen die FileVault-Richtlinien neu erstellen, um diese Einstellung für die Verwendung zu konfigurieren. 

###  <a name="ui-update-when-configuring-compliance-policy----3961639----"></a>Aktualisierung der Benutzeroberfläche beim Konfigurieren der Konformitätsrichtlinie <!-- 3961639  -->
Wir aktualisieren die Benutzeroberfläche für die Konfiguration von Konformitätsrichtlinien in Microsoft Endpoint Manager (**Geräte** > **Konformitätsrichtlinien** > **Richtlinien** > **Richtlinie erstellen**). Es wird eine neue Benutzeroberfläche angezeigt, die die gleichen Einstellungen und Details bereitstellt, die Sie zuvor verwendet haben. Die neue Benutzeroberfläche zum Erstellen einer Konformitätsrichtlinie ähnelt dem Vorgang eines Assistenten und enthält die Seite, auf der Sie *Zuweisungen* für die Richtlinie hinzufügen können sowie eine Seite *Zusammenfassung*, auf der Sie Ihre Konfiguration überprüfen können, bevor Sie die Richtlinie erstellen. 

### <a name="configure-delivery-optimization-agent-when-downloading-win32-app-content---5410945----"></a>Konfigurieren des Übermittlungsoptimierungs-Agents beim Herunterladen von Win32-App-Inhalten<!-- 5410945  -->
Sie können den Übermittlungsoptimierungs-Agent so konfigurieren, dass Win32-App-Inhalte basierend auf der Zuweisung entweder im Hintergrund oder im Vordergrund heruntergeladen werden. Für vorhandene Win32-Apps wird der Inhalt weiterhin im Hintergrund heruntergeladen. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Apps** > **Alle Apps**, wählen Sie die *Win32-App* aus, und klicken Sie auf **Eigenschaften**. Klicken Sie neben **Zuweisungen** auf **Bearbeiten**.  Bearbeiten Sie die Zuweisung, indem Sie im Abschnitt **Erforderlich** unter **Modus** die Option **Einschließen** auswählen.  Die neue Einstellung finden Sie im Abschnitt **App-Einstellungen**, wenn sie verfügbar ist. Weitere Informationen zur Übermittlungsoptimierung finden Sie unter [Eigenständiges Intune – Win32-App-Verwaltung – Übermittlungsoptimierung](../apps/apps-win32-app-management.md#delivery-optimization).

<!-- ***********************************************-->
<!--## Device enrollment-->

<!-- ***********************************************-->
## <a name="device-management"></a>Geräteverwaltung

### <a name="change-primary-user-for-windows-devices----3794742---"></a>Ändern des primären Benutzers für Windows-Geräte <!-- 3794742 -->
Sie können den primären Benutzer für hybride Windows- und Azure AD-Geräte ändern. Navigieren Sie hierzu zu **Intune** > **Geräte** > **Alle Geräte**, wählen Sie ein Gerät aus, und klicken Sie dann auf **Eigenschaften** > **Primärer Benutzer**.

### <a name="new-android-report-on-android-devices-overview-page---5435435---"></a>Neuer Android-Bericht auf der Übersichtsseite für Android-Geräte<!-- 5435435 -->
Wir fügen einen Bericht zur Microsoft Endpoint Manager-Verwaltungskonsole auf der Seite „Übersicht“ für Android-Geräten hinzu, in der angezeigt wird, wie viele Android-Geräte in jeder Geräteverwaltungslösung registriert wurden. Dieses Diagramm zeigt (wie das gleiche Diagramm in der Azure-Konsole) die Anzahl der Arbeitsprofile, vollständig verwalteten, dedizierten und mit Geräteadministratorregistrierung registrierten Geräte an. Klicken Sie auf **Geräte** > **Android** > **Übersicht**, um den Bericht anzuzeigen.

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Unterstützung von PowerShell-Skripts für BYOD-Geräte<!-- 1862833  -->
PowerShell-Skripts unterstützen bei Azure AD registrierte Geräte in Intune. Weitere Informationen zu PowerShell finden Sie unter [Verwenden von PowerShell-Skripts auf Windows 10-Geräten in Intune](../apps/intune-management-extension.md). Diese Funktion unterstützt keine Geräte, auf denen die Windows 10 Home-Edition ausgeführt wird.

### <a name="additional-data-warehouse-device-inventory-properties---6125732----"></a>Zusätzliche Data Warehouse-Eigenschaften für den Gerätebestand<!-- 6125732  -->
Weitere Gerätebestandseigenschaften werden mithilfe des Intune Data Warehouse verfügbar sein. Die folgenden Eigenschaften werden über die [Geräte](../developer/intune-data-warehouse-collections.md#devices)-Sammlung verfügbar gemacht:

- Speicherkapazität
- Arbeitsspeicherkapazität
- Office 365-Version
- Dies ist das Gerätemodell.

Weitere Informationen zum Data Warehouse finden Sie unter [Microsoft Intune-Data Warehouse-API](../developer/reports-nav-intune-data-warehouse.md).

### <a name="guide-users-from-android-device-administrator-management-to-work-profile-management--5857738--"></a>Leitfaden für Benutzer von der Android-Geräteadministratorverwaltung zur Arbeitsprofilverwaltung<!--5857738-->
Wir veröffentlichen eine neue Konformitätseinstellung für die Plattform für Android-Geräteadministratoren. Mit dieser Einstellung können Sie ein Gerät als nicht konform einstufen, wenn es mit der Plattform für Geräteadministratoren verwaltet wird.

Auf diesen nicht konformen Geräten wird Benutzern auf der Seite **Geräteeinstellungen aktualisieren** die Nachricht **Zum Setup der neuen Geräteverwaltung wechseln** angezeigt. Wenn Benutzer auf die Schaltfläche **Auflösen** klicken, werden sie durch die folgenden Schritte geleitet:

1. Aufheben der Registrierung in der Geräteadministratorverwaltung
2. Registrieren bei der Arbeitsprofilverwaltung
3. Lösen von Konformitätsproblemen

In dem Bestreben, auf eine moderne, umfassendere und sicherere Geräteverwaltung mit Android Enterprise umzusteigen, reduziert Google die Geräteadministratorunterstützung in neuen Android-Releases.  Intune kann nur vollständige Unterstützung für die vom Geräteadministrator verwalteten Android-Geräte bieten, auf denen bis zum zweiten Quartal 2020 Android 10 und höher ausgeführt wird. Geräte, die vom Geräteadministrator verwaltet werden (mit Ausnahme von Samsung) und nach Ablauf dieser Zeit Android 10 oder höher ausführen, können nicht vollständig verwaltet werden. Dies bedeutet, dass betroffene Geräte keine neuen Kennwortanforderungen erhalten. Weitere Informationen finden Sie in diesem [Hinweis](#decreasing-support-for-android-device-administrator).

### <a name="retire-noncompliant-devices---1827291---"></a>Ausmustern nicht konformer Geräte<!-- 1827291 -->
Wir fügen eine neue optionale Konformitätsfunktion zum Abkoppeln eines nicht konformen Geräts hinzu (**Geräte** > **Konformitätsrichtlinien** > **Richtlinien** > **Richtlinie erstellen** und dann verfügbare *Aktionen* auf der Seite *Aktionen bei Inkompatibilität* anzeigen).  Wenn Sie ein nicht konformes Gerät abkoppeln, werden alle Unternehmensdaten darauf entfernt. Außerdem wird das Gerät nicht mehr von Intune verwaltet. Diese Aktion wird ausgeführt, wenn der konfigurierte Wert in Tagen erreicht ist. Der Mindestwert beträgt 30 Tage.  Es ist eine explizite Bestätigung des IT-Administrators erforderlich, um die Geräte mithilfe des Abschnitts *Retire Non-compliant devices* (Nicht konforme Geräte abkoppeln) abzukoppeln, in dem Administratoren alle berechtigten Geräte abkoppeln können.

### <a name="new-information-in-device-details---5604099---"></a>Neue Informationen in den Gerätedetails<!-- 5604099 -->
Die folgenden Informationen finden Sie jetzt auf der Seite **Übersicht** für Geräte:

- Speicherkapazität (Menge des physischen Massenspeichers auf dem Gerät)
- Arbeitsspeicherkapazität (Menge des physischen Arbeitsspeichers auf dem Gerät)

### <a name="script-support-for-macos-devices---4280361----"></a>Skriptunterstützung für macOS-Geräte<!-- 4280361  -->
Sie können Skripts für macOS-Geräte hinzufügen und bereitstellen. Diese Unterstützung erweitert die Funktion zum Konfigurieren von macOS-Geräten um ein Vielfaches, was mit nativen MDM-Funktionen auf macOS-Geräten möglich ist.

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>Überwachung und Problembehandlung

### <a name="help-and-support-workflow-update-to-support-additional-services---5654170---"></a>Hilfe- und Supportworkflowupdate zur Unterstützung zusätzlicher Dienste<!-- 5654170 -->
Wir aktualisieren die Seite „Hilfe und Support“ im Microsoft Endpoint Manager Admin Center, damit Sie den von Ihnen verwendeten Verwaltungstyp auswählen können, um besseren spezifischen Support bieten zu können (**Troubleshooting + support** (Problembehandlung und Support) >  **Hilfe und Support**). Mit dieser Änderung können Sie einen der folgenden Verwaltungstypen auswählen:
- Configuration Manager (umfasst Desktop Analytics)
- Intune
- Co-Verwaltung

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## <a name="security"></a>Sicherheit

### <a name="derived-credentials-support-on-android-cobo-devices--4839592--"></a>Unterstützung für abgeleitete Anmeldeinformationen auf Android-COBO-Geräten<!--4839592-->
Sie können abgeleitete Anmeldeinformationen auf vollständig verwalteten Android Enterprise-Geräten verwenden. Das Abrufen von abgeleiteten Anmeldeinformationen für Entrust Datacard, Intercede und DISA Purebred wird unterstützt. Sie können abgeleitete Anmeldeinformationen für die App-Authentifizierung, für WLAN, VPNs oder S/MIME-Signaturen und/oder -Verschlüsselung für Apps verwenden, die dies unterstützen.

### <a name="use-antivirus-policy-to-manage-settings-for-microsoft-defender-antivirus-and-the-windows-security-experience--6131401---"></a>Verwenden der Antivirusrichtlinie zum Verwalten von Einstellungen für Microsoft Defender Antivirus und der Windows-Sicherheitsumgebung<!--6131401 -->
Über den Knoten *Endpunktsicherheit* können Sie Einstellungen für die Richtlinien **Antivirus** konfigurieren. Wenn Sie die Antivirusrichtlinie konfigurieren, definieren Sie die Einstellungen für Ihre Windows 10-Geräte über zwei Profiltypen:

- Microsoft Defender Antivirus: Verwalten Sie Einstellungen für den Cloudschutz, Antivirenausschlüsse, die Wiederherstellung, Überprüfungsoptionen und vieles mehr.
- Windows-Sicherheitsumgebung: Verwalten Sie, wie Benutzer mit Windows-Sicherheitseinstellungen auf ihren Geräten arbeiten können. Sie können konfigurieren, was Endbenutzer im Microsoft Defender Security Center anzeigen können und welche Benachrichtigungen sie erhalten.

### <a name="users-personal-encrypted-recovery-key---6273943---"></a>Persönlicher verschlüsselter Wiederherstellungsschlüssel des Benutzers<!-- 6273943 -->
Es ist ein neues Intune-Feature verfügbar, mit dem Benutzer ihren persönlichen verschlüsselten **FileVault**-Wiederherstellungsschlüssel für Mac-Geräte über die Android-Unternehmensportal-App oder die Android-Intune-App abrufen können. Sowohl in der Unternehmensportal-App als auch in der Intune-App gibt es einen Link, der einen Chrome-Browser mit dem Webunternehmensportal öffnet, in dem der Benutzer den für den Zugriff auf seine Mac-Geräte benötigten **FileVault**-Wiederherstellungsschlüssel anzeigen kann. Weitere Informationen zur Verschlüsselung finden Sie unter [Verwenden der Geräteverschlüsselung mit Intune](../protect/encrypt-devices.md).

### <a name="privacy-preferences-settings-for-macos-devices---2934232---"></a>Privatsphäreneinstellungen für macOS-Geräte<!-- 2934232 --> 
Apple hat im Rahmen der Veröffentlichung von macOS Catalina 10.15 die Sicherheits- und Privatsphäreneinstellungen erweitert. Standardmäßig können Anwendungen und Prozesse ohne Zustimmung des Benutzers nicht auf bestimmte Daten zugreifen. Wenn Benutzer keine Zustimmung geben, funktionieren die Anwendungen und Prozesse möglicherweise nicht mehr. Intune fügt Unterstützung für Einstellungen hinzu, mit denen IT-Administratoren den Zugriff auf Daten im Namen von Endbenutzern auf Geräten, auf denen macOS 10.14 oder höher ausgeführt wird, zulassen oder nicht zulassen können. Mit diesen Einstellungen wird sichergestellt, dass Anwendungen und Prozesse weiterhin ordnungsgemäß funktionieren und die Anzahl der Eingabeaufforderungen verringert, die Endbenutzern zur Verfügung stehen.

### <a name="updated-ui-text-and-labels-for-windows-10-endpoint-protection-profile-settings---5983747---"></a>Aktualisierter Benutzeroberflächentext und Bezeichnungen für Windows 10 Endpoint Protection-Profileinstellungen<!-- 5983747 -->
Wir aktualisieren den Text für verschiedene Einstellungen, die Sie als Windows 10-Gerätekonfigurationsprofile konfigurieren, um das Verständnis der gewünschten Einstellungen und Ergebnisse zu erleichtern.

Zu den Einstellungen, die wir aktualisieren, gehören Windows 10-Gerätekonfigurationsprofile für Folgendes:

- [Geräteeinschränkungen](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus) > Microsoft Defender Antivirus  
- [Endpoint Protection](../protect/endpoint-protection-windows-10.md) > Microsoft Defender Antivirus

Die Einstellungen, die von Intune unterstützt werden, werden nicht geändert. Dabei handelt es sich lediglich um ein Update für den Benutzeroberflächentext im Microsoft Endpoint Management Admin Center.

<!-- ***********************************************-->
## <a name="notices"></a>Benachrichtigungen

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Weitere Informationen:

Details zu aktuellen Entwicklungen finden Sie unter [Neuerungen in Microsoft Intune](whats-new.md).
