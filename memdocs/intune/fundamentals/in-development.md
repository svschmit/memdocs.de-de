---
title: 'In der Entwicklung: Microsoft Intune'
titleSuffix: ''
description: In der Entwicklung befindliche Microsoft Intune-Features
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/06/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3bec2ab1f368b7264348b9b4b51143dbe924dc2f
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81638158"
---
# <a name="in-development-for-microsoft-intune---april-2020"></a>In der Entwicklung befindliche Microsoft Intune-Features: April 2020

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
<!--
## App management
-->

<!-- ***********************************************-->
## <a name="device-configuration"></a>Gerätekonfiguration

### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>Gerätekonfigurationsprofil für das kabelgebundene Netzwerk für macOS-Geräte<!-- 3508686  -->
Ein neues Gerätekonfigurationsprofil für macOS ist verfügbar, das kabelgebundene Netzwerke konfiguriert. Navigieren Sie dafür zu **Gerätekonfiguration** > **Profile** > **Profil erstellen** > **macOS**, um die Plattform auszuwählen, und wählen Sie dann den Profiltyp **Kabelgebundenes Netzwerk** aus. Verwenden Sie dieses Feature zum Erstellen von 802.1x-Profilen für die Verwaltung von kabelgebundenen Netzwerken, und stellen Sie dieses Netzwerke für Ihre macOS-Geräte bereit.

Gilt für:
- macOS

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>Einstellungen und Werte für das Gerätekonfigurationsprofil werden für Windows-Plattformen aktualisiert<!-- 4091122 -->
Beim Erstellen von Gerätekonfigurationsprofilen für Windows-Plattformen (**Geräte** > **Konfigurationsprofile** >  **Profil erstellen** > beliebige **Windows**-Option für Plattform) unterscheiden sich einige Einstellungen und deren Werte vom CSP, was verwirrend sein kann. Die Einstellungsnamen und ihre Werte werden aktualisiert, sodass sie eindeutig zu verstehen sind.

Gilt für:

- Gerätekonfigurationsprofile für Windows 10 oder höher
- Gerätekonfigurationsprofile für Windows Holographic for Business
- Gerätekonfigurationsprofile für Windows 8.1
- Gerätekonfigurationsprofile für Windows Phone 8.1

### <a name="configure-the-microsoft-defender-atp-app-for-macos-----5520115----"></a>Konfigurieren der Microsoft Defender ATP-App für macOS  <!-- 5520115  -->
In Kürze können Sie die [Einstellungen](../protect/endpoint-protection-macos.md) der Microsoft Defender ATP-App für Geräte konfigurieren, die macOS als Teil eines Endpoint Protection-Gerätekonfigurationsprofils ausführen (**Geräte** > **Konfigurationsprofile** > **Profil erstellen**, und wählen Sie dann **macOS** für *Plattform* und **Endpoint Protection** für *Profiltyp* aus). Es gibt acht Einstellungen für die macOS-Gerätekonfiguration. 

Defender ATP wird unter macOS 10.13 (High Sierra) und höher unterstützt, und die [Microsoft Defender ATP](../apps/apps-advanced-threat-protection-macos.md)-App muss auf dem Gerät bereitgestellt werden, *nachdem* diese Einstellungen angewendet wurden. Die Einstellungen sollten vor der Bereitstellung der App an das Gerät gesendet werden. Betaversionen von macOS werden nicht unterstützt.

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>Neue FileVault-Einstellung für macOS-Endpoint Protection-Gerätekonfigurationsrichtlinie<!-- 5459801   -->
Wir fügen der FileVault-Kategorie innerhalb der [macOS-Endpoint Protection](../protect/endpoint-protection-macos.md)-Vorlage eine neue Einstellung hinzu: „Wiederherstellungsschlüssel ausblenden“ (**Geräte** > **Konfigurationsprofile** > **Profil erstellen**, wählen Sie **macOS** für *Plattform* und dann **Endpoint Protection** für *Profiltyp* aus). Mit dieser Einstellung wird der persönliche Schlüssel während der FileVault 2-Verschlüsselung für den Endbenutzer ausgeblendet. Ein Gerätebenutzer kann den persönlichen Wiederherstellungsschlüssel jederzeit über die iOS-Unternehmensportal-App oder über die Website des Unternehmensportals für das verschlüsselte macOS-Gerät anzeigen. Navigieren Sie einfach zu „Gerätedetails“, und klicken Sie auf *Wiederherstellungsschlüssel abrufen*, um den persönlichen Wiederherstellungsschlüssel anzuzeigen.

Diese Einstellung ist in der zuvor erstellten Richtlinie nicht verfügbar. Sie müssen die FileVault-Richtlinien neu erstellen, um diese Einstellung für die Verwendung zu konfigurieren. 

### <a name="additional-options-in-sso-and-sso-app-extension-profiles-on-iosipados-devices---6504155----"></a>Zusätzliche Optionen in SSO und SSO-App-Erweiterungsprofile auf iOS/iPadOS-Geräten<!-- 6504155  -->
Auf iOS/iPadOS-Geräten können Sie:

- in SSO-Profilen (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **iOS/iPadOS** (Plattform) > **Gerätefeatures** (Profil) > **Einmaliges Anmelden**) den Kerberos-Prinzipalnamen auf den Namen der Sicherheitskontenverwaltung festlegen. 
- in SSO-App-Erweiterungsprofilen (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **iOS/iPadOS** (Plattform) > **Gerätefeatures** (Profil) > **App-Erweiterung für einmaliges Anmelden**) die Microsoft Azure AD-Erweiterung für iOS/iPadOS mithilfe eines neuen SSO-App-Erweiterungstyps mit weniger Klicks konfigurieren. Sie können die Azure AD-Erweiterung für freigegebene Geräte aktivieren und erweiterungsspezifische Daten an die Erweiterung senden.

Gilt für:
- iOS/iPadOS 13.0 und höher

Weitere Informationen zur Verwendung des einmaligen Anmeldens auf iOS/iPadOS-Geräten finden Sie unter [Übersicht über die App-Erweiterung für einmaliges Anmelden](../configuration/device-features-configure.md#single-sign-on-app-extension) und [Einstellungen für einmaliges Anmelden](../configuration/ios-device-features-settings.md#single-sign-on-app-extension).

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Geräteregistrierung

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>BYOD-Geräte können VPN für die Bereitstellung verwenden<!--5015344 -->
Mit der neuen Autopilot-Profiloption **Überprüfung der Domänenkonnektivität überspringen** können Sie hybrid in Azure AD eingebundene Geräte ohne Zugriff auf Ihr Unternehmensnetzwerk mithilfe Ihres eigenen Drittanbieter-Win32-VPN-Clients bereitstellen. Die neue Option finden Sie unter [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Geräte**  > **Windows** > **Windows-Registrierung** > **Bereitstellungsprofile** > **Profil erstellen** > **Willkommensseite**.

<!-- ***********************************************-->
## <a name="device-management"></a>Geräteverwaltung

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Unterstützung von PowerShell-Skripts für BYOD-Geräte<!-- 1862833  -->
PowerShell-Skripts unterstützen bei Azure AD registrierte Geräte in Intune. Weitere Informationen zu PowerShell finden Sie unter [Verwenden von PowerShell-Skripts auf Windows 10-Geräten in Intune](../apps/intune-management-extension.md). Diese Funktion unterstützt keine Geräte, auf denen die Windows 10 Home-Edition ausgeführt wird.

### <a name="script-support-for-macos-devices---4280361----"></a>Skriptunterstützung für macOS-Geräte<!-- 4280361  -->
Sie können Skripts für macOS-Geräte hinzufügen und bereitstellen. Diese Unterstützung erweitert die Funktion zum Konfigurieren von macOS-Geräten um ein Vielfaches, was mit nativen MDM-Funktionen auf macOS-Geräten möglich ist.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics enthält das Gerätedetailprotokoll<!--6014987  -->
Intune-Gerätedetailprotokolle werden unter **Berichte** > **Log Analytics** bereitgestellt. Sie können Gerätedetails korrelieren, um benutzerdefinierte Abfragen und Azure-Workbooks zu erstellen.


<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
<!--
## Monitor and troubleshoot
-->

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## <a name="security"></a>Sicherheit

### <a name="derived-credentials-support-for-disa-purebred-on-android-devices--4839592---"></a>Unterstützung abgeleiteter Anmeldeinformationen für DISA Purebred auf Android-Geräten<!--4839592 -->
Sie können *DISA Purebred* als Anbieter für [abgeleitete Anmeldeinformationen](../protect/derived-credentials.md) auf vollständig verwalteten Android Enterprise-Geräten (**Mandantenverwaltung** > **Connectors und Token** > **Abgeleitete Anmeldeinformationen**) verwenden. Unterstützung wird beim Abrufen abgeleiteter Anmeldeinformationen für DISA Purebred einbezogen. Sie können abgeleitete Anmeldeinformationen für die App-Authentifizierung, für WLAN, VPNs oder S/MIME-Signaturen und/oder -Verschlüsselung für Apps verwenden, die dies unterstützen. 

Im April hat Intune die Unterstützung für *Entrust Datacard* und *Intercede* als Anbieter für abgeleitete Anmeldeinformationen hinzugefügt. 

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



