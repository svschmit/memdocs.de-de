---
title: Neues in Microsoft Intune – Azure | Microsoft-Dokumentation
titleSuffix: ''
description: Erfahren Sie, welche Neuerungen es im Intune-Azure-Portal gibt
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/30/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 791ed23f-bd13-4ef0-a3dd-cd2d7332c5cc
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 677f85874ddf206b716e70a0cc6c659e10b99fef
ms.sourcegitcommit: 6a6a713fc1090e03893d80f4259dc7300fb1d5ff
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80438802"
---
# <a name="whats-new-in-microsoft-intune"></a>Neuerungen in Microsoft Intune

In diesem Artikel werden die Neuheiten im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) von Microsoft Intune behandelt. Hier finden Sie auch [wichtige Hinweise](#notices), [frühere Releases](whats-new-archive.md) und Informationen zur [Veröffentlichung von Intune-Dienstupdates](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728). 

> [!Note]
> Bei jedem [monatlichen Update](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728) kann das Rollout bis zu drei Tage dauern und erfolgt in dieser Reihenfolge:
>
> - 1\. Tag: Asien-Pazifik (APAC)
> - 2\. Tag: Europa, Naher Osten und Afrika (EMEA)
> - 3\. Tag: Nordamerika
> - 4\. Tag und später: Intune for Government
>
> Die Einführung einiger Funktionen dauert möglicherweise mehrere Wochen, sodass sie in der ersten Woche nicht für alle Kunden verfügbar sind.
>
> Auf der Seite [Features in der Entwicklung](in-development.md) finden Sie eine Liste der neuen Features in einem Release.

**RSS-Feed**: Lassen Sie sich benachrichtigen, wenn diese Seite aktualisiert wird, indem Sie die folgende URL kopieren und in Ihren Feedreader einfügen: `https://docs.microsoft.com/api/search/rss?search=%22What%27s+new+in+microsoft+intune%3F+-+Azure%22&locale=en-us`

<!-- Common categories:  
### App management
### Device configuration
### Device enrollment
### Device management
### Device security
### Intune apps
### Monitor and troubleshoot
### Role-based access control
-->  

<!-- ########################## -->
## <a name="week-of-march-30-2020"></a>Woche ab 30. März 2020

### <a name="new-url-for-the-microsoft-endpoint-manager-admin-center---3704810---"></a>Neue URL des Microsoft Endpoint Manager Admin Centers<!-- 3704810 -->
Die URL für das Microsoft Endpoint Manager Admin Center (zuvor Microsoft 365-Geräteverwaltung) wurde gemäß der Ankündigung zu Microsoft Endpoint Manager bei der Ignite im letzten Jahr in [https://endpoint.microsoft.com](https://endpoint.microsoft.com) geändert. Die alte Admin Center-URL ([https://devicemanagement.microsoft.com](https://devicemanagement.microsoft.com)) wird weiterhin funktionieren, es wird jedoch empfohlen, dass Sie über die neue URL auf das Microsoft Endpoint Manager Admin Center zugreifen.

Weitere Informationen finden Sie unter [Vereinfachen von IT-Aufgaben mit dem Microsoft Endpoint Manager Admin Center](what-is-device-management.md#simplify-it-tasks-using-the-device-management-admin-center).

### <a name="app-management"></a>App-Verwaltung

#### <a name="script-support-for-macos-devices-public-preview---4280361-wnready---"></a>Skriptunterstützung für macOS-Geräte (Public Preview)<!-- 4280361 wnready -->
Sie können Skripts für macOS-Geräte hinzufügen und bereitstellen. Diese Unterstützung erweitert die Funktion zum Konfigurieren von macOS-Geräten um ein Vielfaches, was mit nativen MDM-Funktionen auf macOS-Geräten möglich ist. Weitere Informationen finden Sie unter [Verwenden von Shellskripts auf macOS-Geräten in Intune](../apps/macos-shell-scripts.md).

<!-- ########################## -->
## <a name="week-of-march-24-2020"></a>Woche ab 24. März 2020

### <a name="improved-user-interface-experience-when-creating-device-restrictions-profiles-on-android-and-android-enterprise-devices---5841361---"></a>Verbesserte Benutzeroberfläche für das Erstellen von Gerätekonfigurationsprofilen auf Android- und Android Enterprise-Geräten<!-- 5841361 -->

Wenn Sie ein Profil für Android- oder Android Enterprise-Geräte erstellen, wird das Microsoft Endpoint Manager Admin Center entsprechend aktualisiert. Diese Änderung wirkt sich auf die folgenden Gerätekonfigurationsprofile aus (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **Android-Geräteadministrator** oder **Android Enterprise** für die Plattform):

- Geräteeinschränkungen: Android-Geräteadministrator
- Geräteeinschränkungen: Android Enterprise-Gerätebesitzer
- Geräteeinschränkungen: Android Enterprise-Arbeitsprofil

Weitere Informationen zu den Geräteeinschränkungen, die Sie konfigurieren können, finden Sie unter [Android-Geräte Administrator](../configuration/device-restrictions-android.md) und [Android Enterprise](../configuration/device-restrictions-android-for-work.md).

### <a name="improved-user-interface-experience-when-creating-configuration-profiles-on-iosipados-and-macos-devices---5569002-5568997---"></a>Verbesserte Benutzeroberfläche für das Erstellen von Konfigurationsprofilen auf iOS-/iPadOS- und macOS-Geräten<!-- 5569002 5568997 -->

Wenn Sie ein Profil für iOS- oder macOS-Geräte erstellen, wird das Microsoft Endpoint Manager Admin Center entsprechend aktualisiert. Diese Änderung wirkt sich auf die folgenden Gerätekonfigurationsprofile aus. (Navigieren Sie zu **Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **iOS/iPadOS** oder **macOS**, um die Plattform auszuwählen):

- Benutzerdefiniert: iOS/iPadOS, macOS
- Gerätefunktionen: iOS/iPadOS, macOS
- Geräteeinschränkungen: iOS/iPadOS, macOS
- Endpoint Protection: macOS
- Erweiterungen: macOS
- Einstellungsdatei: macOS

### <a name="hide-from-user-configuration-setting-in-device-features-on-macos-devices---6524869---"></a>Ausblenden der Benutzerkonfigurationseinstellung in Gerätefeatures auf macOS-Geräten<!-- 6524869 -->

Beim Erstellen eines Konfigurationsprofils für Gerätefeatures auf macOS-Geräten gibt es die neue Einstellung **Aus Benutzerkonfiguration ausblenden** (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **macOS** (Plattform) > **Gerätefeatures** (Profil) > **Anmeldeelemente**).

Dieses Feature aktiviert das Kontrollkästchen zum Ausblenden einer App in den **Benutzer und Gruppen**-Anmeldeelementen der App-Liste auf macOS-Geräten. Vorhandene Profile zeigen diese Einstellung innerhalb der Liste als nicht konfiguriert an. Administratoren können vorhandene Profile aktualisieren, um diese Einstellung zu konfigurieren.

Wenn **Ausblenden** festgelegt wird, wird das Kontrollkästchen zum Ausblenden für die App aktiviert, und Benutzer können die Einstellung nicht ändern. Außerdem wird die App für Benutzer ausgeblendet, wenn sie sich bei ihren Geräten anmelden.

> [!div class="mx-imgBorder"]
> ![Ausblenden von Apps auf macOS-Geräten, nachdem Benutzer sich am Gerät in Microsoft Intune und Endpoint Manager anmelden](./media/whats-new/macos-hide-checkmark-users-groups-login-items-apps-list.png)

Weitere Informationen zu diesen Einstellungen finden Sie unter [macOS-Gerätefeatureeinstellungen](../configuration/macos-device-features-settings.md).

Diese Funktion gilt für:

- macOS

## <a name="week-of-march-16-2020-2003-service-release"></a>Woche ab 16. März 2020 (Dienstrelease 2003)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>App-Verwaltung

#### <a name="macos-and-ios-company-portal-updates---5779439-5780234----"></a>Aktualisierungen des macOS- und iOS-Unternehmensportals<!-- 5779439, 5780234  -->
Der Bereich „Profil“ des macOS- und iOS-Unternehmensportals wurde aktualisiert, und die Schaltfläche „Abmelden“ wurde integriert. Darüber hinaus wurden weitere Verbesserungen an der Benutzeroberfläche im Bereich „Profil“ im macOS-Unternehmensportal vorgenommen. Weitere Informationen zum Unternehmensportal finden Sie unter [Konfigurieren der Microsoft Intune-Unternehmensportal-App](../apps/company-portal-app.md).

#### <a name="retarget-web-clips-to-microsoft-edge-on-ios-devices---5455276-----"></a>Festlegen von Microsoft Edge als Zielbrowser für Webclips auf iOS-Geräten<!-- 5455276   -->
Neue Webclips (angeheftete Web-Apps) auf iOS-Geräten, die in einem geschützten Browser geöffnet werden müssen, werden in Microsoft Edge statt in Intune Managed Browser geöffnet. Bereits vorhandene Webclips müssen neu zugewiesen werden, damit sie in Microsoft Edge anstatt in Managed Browser geöffnet werden. Weitere Informationen finden Sie unter [Verwalten des Webzugriffs mithilfe von Microsoft Edge mit Microsoft Intune](../apps/manage-microsoft-edge.md) und [Hinzufügen von Web-Apps zu Microsoft Intune](../apps/web-app.md).

#### <a name="use-the-intune-diagnostic-tool-with-microsoft-edge-for-android---4735244----"></a>Verwenden des Intune-Diagnosetools mit Microsoft Edge für Android<!-- 4735244  -->
Microsoft Edge für Android ist jetzt in das Intune-Diagnosetool integriert. Ebenso wie bei Microsoft Edge für iOS startet bei Eingabe von „about:intunehelp“ in die URL-Leiste (Adressfeld) von Microsoft Edge auf dem Gerät das Intune-Diagnosetool. Dieses Tool stellt detaillierte Protokolle bereit. Benutzer erhalten eine Anleitung, wie sie diese Protokolle sammeln und an ihre IT-Abteilung senden oder MAM-Protokolle für bestimmte Apps anzeigen.

#### <a name="updates-to-intune-branding-and-customization---5236032----"></a>Updates für den Bereich „Branding und Anpassung“ in Intune<!-- 5236032  -->
Wir haben den Intune-Bereich mit der Bezeichnung „Branding und Anpassung“ u. a. mit folgenden Verbesserungen aktualisiert:

- Umbenennung des Bereichs in **Anpassung**
- Verbesserung der Organisation und des Designs der Einstellungen
- Verbesserung des Einstellungstexts und der QuickInfos

Um diese Einstellungen in Intune zu finden, navigieren Sie zum [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) und wählen **Mandantenverwaltung** > **Anpassung** aus. Weitere Informationen zur vorhandenen Anpassung finden Sie unter [Konfigurieren der Microsoft Intune-Unternehmensportal-App](../apps/company-portal-app.md).

#### <a name="users-personal-encrypted-recovery-key---6273943----"></a>Persönlicher verschlüsselter Wiederherstellungsschlüssel des Benutzers<!-- 6273943  -->
Es ist ein neues Intune-Feature verfügbar, mit dem Benutzer ihren persönlichen verschlüsselten **FileVault**-Wiederherstellungsschlüssel für Mac-Geräte über die Android-Unternehmensportal-App oder die Android-Intune-App abrufen können. Sowohl in der Unternehmensportal-App als auch in der Intune-App gibt es einen Link, der einen Chrome-Browser mit dem Webunternehmensportal öffnet, in dem Benutzer den für den Zugriff auf ihre Mac-Geräte benötigten **FileVault**-Wiederherstellungsschlüssel anzeigen können. Weitere Informationen zur Verschlüsselung finden Sie unter [Verwenden der Geräteverschlüsselung mit Intune](../protect/encrypt-devices.md).

#### <a name="optimized-dedicated-device-enrollment----6114580-wnready---"></a>Optimierte Registrierung von dedizierten Geräten <!-- 6114580 wnready -->
Wir optimieren die Registrierung von dedizierten Android Enterprise-Geräten und vereinfachen die Anwendung von SCEP-Zertifikaten, die mit einem WLAN verknüpft sind, auf dedizierte Geräte, die vor dem 22. November 2019 registriert wurden. Bei neuen Registrierungen wird die Intune-App weiterhin installiert, aber Endbenutzer können den Schritt **Intune-Agent aktivieren** während der Registrierung nicht mehr ausführen. Die Installation erfolgt automatisch im Hintergrund, und SCEP-Zertifikate, die mit einem WLAN verknüpft sind, können ohne Interaktion durch den Endbenutzer bereitgestellt und festgelegt werden.  

Diese Änderungen werden im Verlauf des März im Rahmen der Bereitstellung des Intune-Dienst-Back-Ends phasenweise eingeführt. Bis Ende ist dieses neue Verhalten in allen Mandanten bereitgestellt. Weitere Informationen finden Sie unter [Support for SCEP certificates in Android Enterprise dedicated devices](https://techcommunity.microsoft.com/t5/intune-customer-success/support-for-scep-certificates-in-android-enterprise-dedicated/ba-p/928147) (Unterstützung für SCEP-Zertifikate auf dedizierten Android Enterprise-Geräten).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Gerätekonfiguration

#### <a name="new-user-experience-when-creating-administrative-templates-on-windows-devices--5096036---"></a>Neue Benutzeroberfläche für die Erstellung von administrativen Vorlagen auf Windows-Geräten<!--5096036 -->
Basierend auf dem Feedback unserer Kunden und im Zuge der Einführung der neuen Vollbildansicht für Azure haben wir die Benutzeroberfläche für Profile für administrative Vorlagen neu erstellt und eine Ordneransicht hinzugefügt. Einstellungen oder vorhandene Profile wurden nicht geändert. Ihre vorhandenen Profile bleiben also unverändert und können in der neuen Ansicht verwendet werden. Sie können weiterhin durch alle Einstellungsoptionen navigieren, indem Sie **Alle Einstellungen** auswählen und die Suche verwenden. Die Strukturansicht ist in „Computerkonfigurationen“ und „Benutzerkonfigurationen“ unterteilt. Die Einstellungen für Windows, Office und Edge finden Sie in den jeweiligen Ordnern.  

Gilt für:
- Windows 10 und höher

#### <a name="vpn-profiles-with-ikev2-vpn-connections-can-use-always-on-with-iosipados-devices---1947932-----"></a>VPN-Profile mit IKEv2-VPN-Verbindungen können Always On auf iOS-/iPadOS-Geräten verwenden<!-- 1947932   -->
Auf iOS-/iPadOS-Geräten können Sie ein VPN-Profil erstellen, das eine IKEv2-Verbindung verwendet (Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **iOS/iPadOS** als Plattform und **VPN** als Profiltyp aus). Sie können jetzt Always On mit IKEv2 konfigurieren. Wenn die IKEv2-VPN-Profile konfiguriert sind, stellen sie automatisch eine Verbindung zum VPN her und bleiben verbunden bzw. stellen im Fall eines Verbindungsverlusts die Verbindung schnell wieder her. Die Verbindung bleibt bestehen, selbst wenn das Netzwerk gewechselt wird oder Geräte neu gestartet werden.

Unter iOS/iPadOS ist das Always On-VPN auf IKEv2-Profile beschränkt.

Die konfigurierbaren IKEv2-Einstellungen finden Sie unter [Hinzufügen von VPN-Einstellungen auf iOS-Geräten in Microsoft Intune](../configuration/vpn-settings-ios.md#ikev2-settings).

Gilt für:
- iOS/iPadOS

#### <a name="delete-bundles-and-bundle-arrays-in-oemconfig-device-configuration-profiles-on-android-enterprise-devices---5550355-----"></a>Löschen von Bundles und Bundlearrays in OEMConfig-Gerätekonfigurationsprofilen auf Android Enterprise-Geräten<!-- 5550355   -->
Auf Android Enterprise-Geräten können Sie OEMConfig-Profile erstellen und aktualisieren (Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **Android Enterprise** als Plattform und **OEMConfig** als Profiltyp aus). Benutzer können jetzt mit dem **Konfigurations-Designer** in Intune Bundles und Bundlearrays löschen.

Weitere Informationen zu OEMConfig-Profilen finden Sie unter [Verwenden und Verwalten von Android Enterprise-Geräten mit OEMConfig in Microsoft Intune](../configuration/android-oem-configuration-overview.md).

Gilt für:
- Android Enterprise

#### <a name="configure-the-iosipados-microsoft-azure-ad-sso-app-extension---5672534-----"></a>Konfigurieren der SSO-App-Erweiterung von Microsoft Azure AD für iOS/iPadOS<!-- 5672534   -->
Das Microsoft Azure AD-Team hat eine App-Erweiterung zum Umleiten beim einmaligen Anmelden (SSO) entwickelt, um Benutzern von iOS- und iPadOS-Geräten mit Version 13.0 oder höher den Zugriff auf Microsoft-Apps und -Websites mit nur einer Anmeldung zu ermöglichen. Alle Apps, die bisher eine brokerbasierte Authentifizierung über die Microsoft Authenticator-App verwendet haben, können das einmalige Anmelden mit der neuen SSO-Erweiterung weiterhin nutzen. Für die Azure AD-Erweiterung für SSO können Sie den Typ der SSO-App-Erweiterung für die Umleitung konfigurieren (Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **iOS/iPadOS** als Plattform, **Gerätefeatures** als Profiltyp und dann **App-Erweiterung für einmaliges Anmelden** aus).

Gilt für:
- iOS 13.0 und neuer
- iOS 13.0 und höher

Weitere Informationen zu iOS-SSO-App-Erweiterungen finden Sie unter [App-Erweiterung für einmaliges Anmelden](../configuration/device-features-configure.md#single-sign-on-app-extension).

#### <a name="enterprise-app-trust-settings-modification-setting-is-removed-from-iosipados-device-restriction-profiles---6225131-----"></a>Änderung der Vertrauenseinstellungen für Unternehmens-Apps wurde aus iOS/iPadOS-Geräteeinschränkungsprofilen entfernt<!-- 6225131   -->
Sie können auf iOS/iPadOS-Geräten ein Geräteeinschränkungsprofil erstellen (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **iOS/iPadOS** (für Plattform) > **Geräteeinschränkungen** (für Profiltyp)). Die Einstellung **Änderung der Vertrauenseinstellungen für Unternehmens-Apps** wurde von Apple und aus Intune entfernt. Wenn Sie diese Einstellung derzeit in einem Profil verwenden, hat diese keine Auswirkungen mehr, und sie wird aus vorhandenen Profilen entfernt. Diese Einstellung wurde auch aus allen Berichterstattungsfunktionen in Intune entfernt.

Gilt für:
- iOS/iPadOS

Navigieren Sie zu [iOS- und iPadOS-Geräteeinstellungen zum Zulassen oder Einschränken von Funktionen mit Intune](../configuration/device-restrictions-ios.md), um die Einstellungen anzuzeigen, die Sie einschränken können.

#### <a name="troubleshooting-pending-mam-policy-notification-changed-to-informational-icon--6348954---"></a>Problembehandlung: Benachrichtigung zu ausstehenden MAM-Richtlinien in Informationssymbol geändert<!--6348954 -->
Das Benachrichtigungssymbol für eine ausstehende MAM-Richtlinie auf der Blatt „Problembehandlung“ wurde in ein Informationssymbol geändert.

####  <a name="ui-update-when-configuring-compliance-policy---3961639------"></a>Aktualisierung der Benutzeroberfläche beim Konfigurieren der Konformitätsrichtlinie<!-- 3961639    -->
Wir haben die Benutzeroberfläche für die [Erstellung von Konformitätsrichtlinien](../protect/create-compliance-policy.md#create-the-policy) in Microsoft Endpoint Manager aktualisiert (**Geräte** > **Konformitätsrichtlinien** > **Richtlinien** > **Richtlinie erstellen**). Wir verwenden eine neue Benutzeroberfläche, die dieselben Einstellungen und Details enthält, die Sie zuvor verwendet haben. Die neue Benutzeroberfläche ähnelt den Vorgängen eines Assistenten zum Erstellen von Konformitätsrichtlinien und enthält eine Seite, auf der Sie *Zuweisungen* für die Richtlinie hinzufügen können sowie eine Seite *Überprüfen + erstellen*, auf der Sie Ihre Konfiguration überprüfen können, bevor Sie die Richtlinie erstellen.

#### <a name="retire-noncompliant-devices---1827291---------"></a>Ausmustern nicht konformer Geräte<!-- 1827291       -->
Wir haben eine neue Aktion für nicht konforme Geräte hinzugefügt, die Sie allen Richtlinien hinzufügen können, um ein [nicht konformes Gerät zurückzuziehen](../protect/actions-for-noncompliance.md#add-actions-for-noncompliance).  Die neue Aktion **Nicht konformes Gerät zurückziehen** führt dazu, dass alle Unternehmensdaten vom Gerät entfernt werden und das Gerät nicht mehr von Intune verwaltet wird.  Diese Aktion wird ausgeführt, wenn der konfigurierte Wert (Tage) erreicht ist. An diesem Punkt ist ein Zurückziehen des Geräts berechtigt. Der Mindestwert beträgt 30 Tage.  Es ist eine explizite Bestätigung des IT-Administrators erforderlich, um die Geräte mithilfe des Abschnitts *Retire Non-compliant devices* (Nicht konforme Geräte abkoppeln) abzukoppeln, in dem Administratoren alle berechtigten Geräte abkoppeln können.

#### <a name="support-for-wpa-and-wpa2-in-ios-enterprise-wi-fi-profiles--6215273-----"></a>Unterstützung für WPA und WPA2 in Enterprise-WLAN-Profilen für iOS<!--6215273   -->
[Unternehmens-WLAN-Profile für iOS](../configuration/wi-fi-settings-ios.md#enterprise-profiles) unterstützen jetzt das Feld *Sicherheitstyp*. Sie können als *Sicherheitstyp* entweder **WPA Enterprise** oder **WPA/WPA2 Enterprise** auswählen und dann eine Auswahl für den *EAP-Typ* angeben.  (**Geräte** > **Konfigurationsprofile** > **Profil erstellen**. Wählen Sie dann **iOS/iPadOS** als *Plattform* und **WLAN** als *Profil* aus.) 

Die neuen Optionen für „Enterprise“ ähneln denen, die bereits für ein grundlegendes WLAN-Profil für iOS verfügbar sind.

#### <a name="new-user-experience-for-certificate-email-vpn-and-wi-fi-vpn-profiles---5615208-----"></a>Neue Benutzeroberflächen für Zertifikat-, E-Mail-, VPN- und WLAN-Profile<!-- 5615208   -->
Wir haben die [Benutzeroberflächen](../configuration/device-profile-create.md) im Endpoint Management Admin Center (**Geräte** > **Konfigurationsprofile** > **Profil erstellen**) zum Erstellen und Ändern der folgenden Profiltypen aktualisiert. Die neue Benutzeroberfläche umfasst die gleichen Einstellungen wie zuvor, ähnelt nun aber mehr der Vorgehensweise eines Assistenten, sodass weniger horizontales Scrollen erforderlich ist. Sie müssen vorhandene Konfigurationen angesichts der neuen Oberfläche nicht ändern.

- Abgeleitete Anmeldeinformation
- E-Mail
- PKCS-Zertifikat
- Importiertes PKCS-Zertifikat
- SCEP-Zertifikat
- Vertrauenswürdiges Zertifikat
- VPN
- WLAN

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Geräteregistrierung

#### <a name="configure-if-enrollment-is-available-in-company-portal-for-android-and-ios---4260128----"></a>Konfigurieren, ob die Registrierung im Unternehmensportal für Android und iOS verfügbar ist<!-- 4260128  -->
Sie können konfigurieren, ob die Geräteregistrierung im Unternehmensportal auf Android- und iOS-Geräten mit oder ohne Eingabeaufforderungen bzw. nicht für Benutzer verfügbar sein soll. Navigieren Sie zum [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431), und klicken Sie auf **Mandantenverwaltung** > **Anpassung** > **Bearbeiten** > **Geräteregistrierung**, um diese Einstellung in Intune zu finden.  

Damit die Einstellung „Geräteregistrierung“ unterstützt wird, müssen Endbenutzer über eine der folgenden Unternehmensportalversionen verfügen:
-    Unternehmensportal unter iOS: Version 4.4 oder höher
-    Unternehmensportal unter Android: Version 5.0.4715.0 oder höher

Weitere Informationen zur Anpassung des Unternehmensportals finden Sie unter [Konfigurieren der Microsoft Intune-Unternehmensportal-App](../apps/company-portal-app.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Geräteverwaltung

#### <a name="new-android-report-on-android-devices-overview-page---5435435-----"></a>Neuer Android-Bericht auf der Übersichtsseite für Android-Geräte<!-- 5435435   -->
Wir haben auf der Übersichtsseite für Android-Geräte einen Bericht zur Microsoft Endpoint Manager-Verwaltungskonsole hinzugefügt, der anzeigt, wie viele Android-Geräte in jeder Geräteverwaltungslösung registriert sind. Dieses Diagramm zeigt (wie das gleiche Diagramm in der Azure-Konsole) die Anzahl der Arbeitsprofile, vollständig verwalteten, dedizierten und mit Geräteadministratorregistrierung registrierten Geräte an. Klicken Sie auf **Geräte** > **Android** > **Übersicht**, um den Bericht anzuzeigen.

#### <a name="guide-users-from-android-device-administrator-management-to-work-profile-management--5857738-idready-wnready-wnstaged--"></a>Leitfaden für Benutzer von der Android-Geräteadministratorverwaltung zur Arbeitsprofilverwaltung<!--5857738 idready wnready wnstaged-->
Wir veröffentlichen eine neue Konformitätseinstellung für die Plattform für Android-Geräteadministratoren. Mit dieser Einstellung können Sie ein Gerät als nicht konform einstufen, wenn es mit der Plattform für Geräteadministratoren verwaltet wird.

Auf diesen nicht konformen Geräten wird Benutzern auf der Seite **Geräteeinstellungen aktualisieren** die Nachricht **Zum Setup der neuen Geräteverwaltung wechseln** angezeigt. Wenn Benutzer auf die Schaltfläche **Auflösen** tippen, werden sie durch die folgenden Schritte geleitet:

1. Aufheben der Registrierung in der Geräteadministratorverwaltung
2. Registrieren bei der Arbeitsprofilverwaltung
3. Lösen von Konformitätsproblemen 
 
In dem Bestreben, auf eine moderne, umfassendere und sicherere Geräteverwaltung mit Android Enterprise umzusteigen, reduziert Google die Geräteadministratorunterstützung in neuen Android-Releases.  Intune kann nur vollständige Unterstützung für die vom Geräteadministrator verwalteten Android-Geräte bieten, auf denen bis zum zweiten Quartal 2020 Android 10 und höher ausgeführt wird. Geräte, die vom Geräteadministrator verwaltet werden (mit Ausnahme von Samsung) und nach Ablauf dieser Zeit Android 10 oder höher ausführen, können nicht vollständig verwaltet werden. Dies bedeutet, dass betroffene Geräte keine neuen Kennwortanforderungen erhalten.

Weitere Informationen zu dieser Einstellung finden Sie unter [Verschieben von Android-Geräten aus dem Geräteadministrator in die Arbeitsprofilverwaltung](../enrollment/android-move-device-admin-work-profile.md). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Überwachung und Problembehandlung

#### <a name="the-data-warehouse-now-provides-the-mac-address---6123680----"></a>Data Warehouse stellt jetzt die MAC-Adresse bereit<!-- 6123680  -->
Das Intune Data Warehouse stellt die MAC-Adresse jetzt als neue Eigenschaft (`EthernetMacAddress`) in der Entität `device` bereit, damit Administratoren Zuordnungen zwischen Benutzer und MAC-Adresse des Hosts vornehmen können. Diese Eigenschaft hilft dabei, bestimmte Benutzer zu erreichen und im Netzwerk auftretende Incidents zu beheben. Administratoren können diese Eigenschaft auch in [Power BI-Berichten](../developer/reports-proc-get-a-link-powerbi.md) verwenden, um informativere Berichte zu erstellen. Weitere Informationen finden Sie in der Dokumentation der Intune Data Warehouse-Entität [device](../developer/intune-data-warehouse-collections.md#devices).

#### <a name="additional-data-warehouse-device-inventory-properties---6125732----"></a>Zusätzliche Data Warehouse-Eigenschaften für den Gerätebestand<!-- 6125732  -->
Im Intune Data Warehouse stehen weitere Gerätebestandseigenschaften zur Verfügung. Die folgenden Eigenschaften werden jetzt über die Sammlung [devices](../developer/intune-data-warehouse-collections.md#devices) verfügbar gemacht:
- Model: das Gerätemodell
- Office365Version: die auf dem Gerät installierte Version von Office 365
- PhysicalMemoryInBytes: der physische Speicher in Bytes
- `TotalStorageSpaceInBytes`: Gesamtspeicherkapazität in Bytes

Weitere Informationen finden Sie unter [Microsoft Intune-Data Warehouse-API](../developer/reports-nav-intune-data-warehouse.md) und in der Dokumentation der Intune Data Warehouse-Entität [device](../developer/intune-data-warehouse-collections.md#devices).

#### <a name="help-and-support-workflow-update-to-support-additional-services---5654170-----"></a>Hilfe- und Supportworkflowupdate zur Unterstützung zusätzlicher Dienste<!-- 5654170   -->
Wir haben die Seite „Hilfe und Support“ im Microsoft Endpoint Manager Admin Center aktualisiert – dort können Sie jetzt [den von Ihnen verwendeten Verwaltungstyp auswählen](../fundamentals/get-support.md#options-to-access-help-and-support). Mit dieser Änderung können Sie einen der folgenden Verwaltungstypen auswählen:

- Configuration Manager (umfasst Desktop Analytics)
- Intune
- Co-Verwaltung

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>Sicherheit

#### <a name="use-a-preview-of-security-administrator-focused-policies-as-part-of-endpoint-security--6131401----"></a>Verwenden einer Vorschau der Sicherheitsadministrator-Richtlinien im Rahmen der Endpunktsicherheit<!--6131401  -->
Wir haben im Microsoft Endpoint Management Admin Center unter dem Knoten „Endpunktsicherheit“ einige neue Richtliniengruppen als öffentliche Vorschau hinzugefügt. Als Sicherheitsadministrator können Sie diese neuen Richtlinien verwenden, um sich auf bestimmte Aspekte der Gerätesicherheit zu konzentrieren. Sie können einzelne Gruppen miteinander verwandter Einstellungen verwalten, ohne sich mit dem Gesamtkontext der Gerätekonfigurationsrichtlinie beschäftigen zu müssen.

Mit Ausnahme der neuen *Virenschutzrichtlinie für Microsoft Defender Antivirus* (siehe unten) sind die Einstellungen in jeder dieser neuen Vorschaurichtlinien und -profile dieselben, die Sie möglicherweise heute bereits über [Gerätekonfigurationsprofile](../configuration/device-profile-create.md) konfigurieren.

Im Folgenden finden Sie die neuen Richtlinientypen, die sich in der Vorschau befinden, sowie die für sie verfügbaren Profiltypen:

- **Antivirus (Vorschau)** :
  - macOS:
    - **Antivirus**: Legen Sie [Einstellungen für Virenschutzrichtlinien](../protect/antivirus-microsoft-defender-settings-macos.md) für macOS fest, um [Microsoft Defender ATP für Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) zu verwalten.

  - Windows 10 und höher:
    - **Microsoft Defender Antivirus**: Verwalten Sie [Einstellungen für Virenschutzrichtlinien](../protect/antivirus-microsoft-defender-settings-windows.md) für Cloudschutz, Antivirus-Ausschlüsse, Wartung, Überprüfungsoptionen und vieles mehr.

      Das Antivirus-Profil für *Microsoft Defender Antivirus* ist eine Ausnahme – dieses Profil führt eine neue Instanz von Einstellungen ein, die zum Einschränkungsprofil eines Geräts gehören. Für diese neuen Antivirus-Einstellungen gilt Folgendes:

        - Es handelt sich um dieselben Einstellungen wie in Geräteeinschränkungen, aber sie unterstützen eine dritte Option für die Konfiguration, die in einer Geräteeinschränkung nicht verfügbar ist.
        - Sie werden auf Geräte mit Co-Verwaltung mit Configuration Manager angewendet, wenn der [Schieberegler für die Co-Verwaltungs-Workload](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads) für Endpoint Protection auf „Intune“ festgelegt ist.

     Planen Sie die Verwendung des neuen Profils *Antivirus* > *Microsoft Defender Antivirus*, anstatt diese Einstellungen über ein Geräteeinschränkungsprofil zu konfigurieren.

  - **Windows-Sicherheitseinstellungen**: Verwalten Sie die Einstellungen für Windows-Sicherheit, die Endbenutzer im Microsoft Defender Security Center anzeigen können. Verwalten Sie auch die Benachrichtigungen, die an Benutzer gesendet werden. Diese Einstellungen unterscheiden sich nicht von den Einstellungen, die in einem Endpoint Protection-Profil für die Gerätekonfiguration verfügbar sind.

- **Datenträgerverschlüsselung (Vorschau)** :
  - macOS:
    - **FileVault**
  - Windows 10 und höher:
    - **BitLocker**
- **Firewall (Vorschau)** :
  - macOS:
    - **macOS-Firewall**
  - Windows 10 und höher:
    - **Microsoft Defender Firewall**
- **Endpunkterkennung und Reaktion (Vorschau)** :
  - Windows 10 und höher: -**Windows 10 Intune**
- **Verringerung der Angriffsfläche (Vorschau)** :
  - Windows 10 und höher:
    - **App- und Browserisolierung**
    - **Webschutz**
    - **Anwendungssteuerung**
    - **Regeln zur Verringerung der Angriffsfläche**
    - **Gerätesteuerung**
    - **Exploit-Schutz**
- **Kontoschutz (Vorschau)** :
  - Windows 10 und höher:
    - **Kontoschutz**

<!-- ########################## -->
## <a name="week-of-march-9-2020"></a>Woche ab 9. März 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>App-Verwaltung

#### <a name="configure-delivery-optimization-agent-when-downloading-win32-app-content---5410945---"></a>Konfigurieren des Übermittlungsoptimierungs-Agents beim Herunterladen von Win32-App-Inhalten<!-- 5410945 -->

Sie können den Übermittlungsoptimierungs-Agent so konfigurieren, dass Win32-App-Inhalte basierend auf der Zuweisung entweder im Hintergrund oder im Vordergrund heruntergeladen werden. Für vorhandene Win32-Apps wird der Inhalt weiterhin im Hintergrund heruntergeladen. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Apps** > **Alle Apps**, wählen Sie die  > *Win32-App* aus, und klicken Sie auf  > **Eigenschaften**. Klicken Sie neben **Zuweisungen** auf **Bearbeiten**.  Bearbeiten Sie die Zuweisung, indem Sie im Abschnitt **Erforderlich** unter **Modus** die Option **Einschließen** auswählen.  Die neue Einstellung finden Sie im Abschnitt **App-Einstellungen**. Weitere Informationen zur Übermittlungsoptimierung finden Sie unter [Eigenständiges Intune – Win32-App-Verwaltung – Übermittlungsoptimierung](../apps/apps-win32-app-management.md#delivery-optimization).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Geräteverwaltung

#### <a name="change-primary-user-for-windows-devices---3794742-----"></a>Ändern des primären Benutzers für Windows-Geräte<!-- 3794742   -->
Sie können den primären Benutzer für hybride Windows-Geräte und mit Azure AD verknüpfte Geräte ändern. Navigieren Sie hierzu zu **Intune** > **Geräte** > **Alle Geräte**, wählen Sie ein Gerät aus, und klicken Sie dann auf **Eigenschaften** > **Primärer Benutzer**. Weitere Informationen finden Sie unter [Ändern des primären Benutzers eines Geräts](../remote-actions/find-primary-user.md#change-a-devices-primary-user).

Für diese Aufgabe wurde ebenfalls eine neue RBAC-Berechtigung (Verwaltete Geräte/Primären Benutzer festlegen) erstellt. Die Berechtigung wurde den integrierten Rollen (einschließlich Helpdeskoperator, Schuladministrator und Endpunktsicherheits-Manager) hinzugefügt.

Dieses Feature wird für Kunden weltweit nach und nach als Vorschauversion veröffentlicht. Das Feature sollte in den nächsten Wochen verfügbar sein.


<!-- ########################## -->
## <a name="week-of-march-2-2020"></a>Woche des 2. März 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Geräteverwaltung

#### <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions---6317104-cm3555758--"></a>Anfügen von Mandanten in Microsoft Endpoint Manager: Gerätesynchronisierung und Geräteaktionen<!-- 6317104, CM3555758-->
Microsoft Endpoint Manager vereint Configuration Manager und Intune in einer einzigen Konsole. Ab Configuration Manager Technical Preview 2002.2 können Sie Ihre Configuration Manager-Geräte in den Clouddienst hochladen und Aktionen für diese über das Admin Center durchführen. Weitere Informationen finden Sie unter [Features in der Technical Preview-Version 2002.2 von Configuration Manager](https://docs.microsoft.com/configmgr/core/get-started/2020/technical-preview-2002-2#bkmk_attach).

Lesen Sie den [Technical Preview](https://docs.microsoft.com/configmgr/core/get-started/technical-preview)-Artikel für Configuration Manager vor der Installation dieses Updates. In diesem Artikel erhalten Sie Informationen zu den allgemeinen Anforderungen und Einschränkungen, die für die Verwendung der Technical Preview gelten. Außerdem erfahren Sie, wie Sie Updates zwischen den Versionen ausführen und Feedback übermitteln.

#### <a name="bulk-remote-actions--4576882--"></a>Massenremoteaktionen<!--4576882-->
Sie können jetzt Massenbefehle für die folgenden Remoteaktionen ausgeben: Neu starten, Autopilot-Zurücksetzung, Zurücksetzen und Delete (Löschen). Navigieren Sie zu [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Geräte** > **Alle Geräte** > **Bulk actions** (Massenvorgänge), um die neuen Massenvorgänge anzuzeigen.

#### <a name="all-devices-list-improved-search-sort-and-filter--6179023--"></a>Liste „Alle Geräte“ für Suchen, Sortieren und Filtern optimiert<!--6179023-->
Die Liste „Alle Geräte“ wurde hinsichtlich Leistung, Suche, Sortieren und Filtern verbessert. Weitere Informationen finden Sie in diesem [Supportartikel](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-changes-in-all-devices-list-and-reporting-in-intune/ba-p/1220946).  

### <a name="app-management"></a>App-Verwaltung  
####  <a name="improved-sign-in-experience-in-company-portal-for-android"></a>Verbesserte Anmeldefunktion im Unternehmensportal für Android    
Wir haben das Layout mehrerer Anmeldebildschirme in der Unternehmensportal-App für Android aktualisiert, um die Benutzeroberfläche moderner, einfacher und übersichtlicher zu gestalten. Weitere Informationen zu den Verbesserungen finden Sie in den [Neuerungen für die App-Benutzeroberfläche](https://docs.microsoft.com/mem/intune/fundamentals/whats-new-app-ui).

<!-- ########################## -->
## <a name="week-of-february-24-2020"></a>Woche des 24. Februar 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>App-Verwaltung

#### <a name="macos-company-portal-user-experience-improvements---5568987---"></a>Verbesserungen an den Funktionen des macOS-Unternehmensportals<!-- 5568987 -->
Wir haben Verbesserungen für die Geräteregistrierung für macOS sowie die Unternehmensportal-App für Mac durchgeführt. Sie werden auch die folgenden Verbesserungen feststellen:
- Eine bessere **AutoUpdate**-Umgebung von Microsoft während der Registrierung, mit der sichergestellt wird, dass Ihre Benutzer über die neueste Version des Unternehmensportals verfügen
- Eine erweiterte Konformitätsüberprüfung während der Registrierung
- Unterstützung für kopierte Incident-IDs, sodass Ihre Benutzer Fehler über ihre Geräte schneller an das Supportteam Ihres Unternehmens schicken können

Weitere Informationen zur Registrierung und der Unternehmensportal-App für Mac finden Sie unter [Registrieren Ihres macOS-Geräts mit der Unternehmensportal-App](../user-help/enroll-your-device-in-intune-macos-cp.md).

#### <a name="app-protection-policies-for-better-mobile-now-supports-ios-and-ipados---6224512----"></a>App-Schutzrichtlinien für Better Mobile unterstützen jetzt iOS und iPadOS<!-- 6224512  -->

Im Oktober 2019 wurde von der Intune-App-Schutzrichtlinie die Funktion zum Verwenden von Daten von unseren Microsoft Threat Defense-Partnern hinzugefügt. Mit diesem Update können Sie jetzt eine App-Schutzrichtlinie verwenden, um die Unternehmensdaten der Benutzer basierend auf der Integrität eines Geräts zu blockieren oder selektiv zu löschen, indem Sie Better Mobile auf iOS- und iPadOS-Geräten verwenden.  Weitere Informationen finden Sie unter [Erstellen einer Mobile Threat Defense-App-Schutzrichtlinie (MTD) mit Intune](../protect/mtd-app-protection-policy.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Geräteverwaltung

#### <a name="exports-from-the-all-devices-list--now-in-zipped-csv-format--6343117--"></a>Exporte aus der Liste „Alle Geräte“ jetzt im gezippten CSV-Format<!--6343117-->
Exporte von der Seite **Geräte** > **Alle Geräte** sind jetzt im gezippten CSV-Format verfügbar.


<!-- ########################## -->
## <a name="week-of-february-17-2020-2002-service-release"></a>Woche des 17. Februar 2020 (Dienstrelease 2002)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>App-Verwaltung

#### <a name="microsoft-defender-advanced-threat-protection-atp-app-for-macos---5424618---"></a>App für Microsoft Defender Advanced Threat Protection (ATP) für macOS<!-- 5424618 -->
Intune bietet eine einfache Möglichkeit, die Microsoft Defender Advanced Threat Protection-App (ATP) für macOS auf verwalteten Mac-Geräten bereitzustellen. Weitere Informationen finden Sie unter [Hinzufügen von Microsoft Defender ATP zu macOS-Geräten mithilfe von Microsoft Intune](../apps/apps-advanced-threat-protection-macos.md) und [Microsoft Defender Advanced Threat Protection für Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac).  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Gerätekonfiguration

#### <a name="enable-network-access-control-nac-with-cisco-anyconnect-vpn-on-ios-devices---4860111----"></a>Aktivieren der Netzwerkzugriffssteuerung (NAC) mit Cisco AnyConnect-VPN auf iOS-Geräten<!-- 4860111  -->
Auf iOS-Geräten können Sie ein VPN-Profil erstellen und verschiedene Verbindungstypen einschließlich Cisco AnyConnect verwenden (**Gerätekonfiguration** > **Profile** > **Profil erstellen** > **iOS** für Plattform > **VPN** für Profiltyp > **Cisco AnyConnect** für Verbindungstyp).

Sie können die Netzwerkzugriffssteuerung (NAC) mit Cisco AnyConnect aktivieren. Zur Nutzung dieses Features ist Folgendes erforderlich:

1. Befolgen Sie die Schritte im [Cisco Identity Services Engine-Administratorhandbuch](https://www.cisco.com/c/en/us/td/docs/security/ise/2-1/admin_guide/b_ise_admin_guide_21/b_ise_admin_guide_20_chapter_01000.html) unter **Configuring Microsoft Intune as an MDM Server (Konfigurieren von Microsoft Intune als MDM-Server)** , um die Cisco Identity Services-Engine (ISE) in Azure zu konfigurieren.
2. Klicken Sie im Intune-Gerätekonfigurationsprofil auf die Einstellung **Netzwerkzugriffssteuerung (NAC) aktivieren**.

Sie finden alle VPN-Einstellungen unter [Hinzufügen von VPN-Einstellungen auf iOS- und iPadOS-Geräten in Microsoft Intune](../configuration/vpn-settings-ios.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Geräteregistrierung

#### <a name="serial-number-on-the-apple-mdm-push-certificate-page--5947765----"></a>Seriennummer auf der Seite des Apple-MDM-Push-Zertifikats<!--5947765  -->
Auf der Seite des Apple-MDM-Push-Zertifikats wird jetzt die Seriennummer angezeigt. Die Seriennummer ist erforderlich, um erneut auf das Apple-MDM-Push-Zertifikat zuzugreifen, wenn der Zugriff auf die Apple-ID, über die das Zertifikat erstellt wurde, verloren gegangen ist. Wenn Sie die Seriennummer anzeigen möchten, wechseln Sie zu **Geräte** > **iOS** > **iOS-Registrierung** > **Apple-MDM-Push-Zertifikat**.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Geräteverwaltung

#### <a name="new-update-schedule-options-for-pushing-os-updates-to-enrolled-iosipados-devices--5879689----"></a>Neue Optionen für den Updatezeitplan zum Übertragen von Betriebssystemupdates per Push an iOS/iPadOS-Geräte<!--5879689  -->
Bei der Planung von Betriebssystemupdates für iOS/iPadOS-Geräte können Sie aus folgenden Optionen wählen. Diese Optionen gelten für Geräte, auf denen die Registrierungstypen Apple Business Manager oder Apple School Manager verwendet wurden.
- Beim nächsten Einchecken aktualisieren
- Update innerhalb des geplanten Zeitraums
- Update außerhalb des geplanten Zeitraums

Für die beiden letztgenannten Optionen können Sie mehrere Zeitfenster erstellen.

Wenn Sie die neuen Optionen anzeigen möchten, wechseln Sie zu MEM > **Geräte** > **iOS** > **Richtlinien für iOS/iPadOS aktualisieren** > **Profil erstellen**.

#### <a name="choose-which-iosipados-updates-to-push-to-enrolled-devices--5879689----"></a>Auswählen, welche iOS/iPadOS-Updates an registrierte Geräte gepusht werden sollen<!--5879689  -->
Sie können ein bestimmtes iOS/iPadOS-Update auswählen (mit der Ausnahme des neuesten Updates), das mithilfe von Push auf Geräte übertragen werden soll, die entweder mit Apple Business Manager oder Apple School Manager registriert wurden. Für solche Geräte muss eine Gerätekonfigurationsrichtlinie festgelegt werden, um die Sichtbarkeit von Softwareupdates für einige Tage zu verzögern. Um dieses Feature anzuzeigen, wechseln Sie zu MEM > **Geräte** > **iOS** > **Richtlinien für iOS/iPadOS aktualisieren** > **Profil erstellen**.



<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Gerätesicherheit

#### <a name="improved-intune-reporting-experience---3791418-----"></a>Verbesserte Intune-Berichterstellung<!-- 3791418   -->
Intune bietet nun verbesserte Berichtserstellungsfunktionen, einschließlich neuer Berichtstypen, besserer Berichtsorganisation, fokussierterer Ansichten, verbesserter Berichtsfunktionen sowie konsistenterer und aktuellerer Daten. Die Berichterstellungsfunktion ist bald allgemein verfügbar und befindet sich dann nicht mehr in der öffentlichen Vorschau. Zusätzlich bietet dieses Release Lokalisierungsunterstützung, Fehlerbehebungen, Verbesserungen am Design sowie aggregierte Gerätekonformitätsdaten auf Kacheln im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).

Neue Berichtstypen für folgende Informationen:

- **Operational** (betriebsbedingt): stellt neue Berichte mit einem negativen Integritätsfokus bereit 
- **Organisationsbezogen**: stellt eine umfassendere Zusammenfassung des Gesamtzustands bereit
- **Historical** (verlaufsbezogen): bietet Informationen zu Mustern und Trends für einen bestimmten Zeitraum.
- **Specialist** (spezialisiert): ermöglicht die Verwendung von Rohdaten zur Erstellung Ihrer eigenen benutzerdefinierten Berichte

Die ersten neuen Berichte konzentrieren sich auf die Gerätekonformität. Weitere Informationen finden Sie im Blogbeitrag [Neues Berichtserstellungsframework für Microsoft Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/New-Reporting-Framework-Coming-to-Intune/ba-p/1009553) und unter [Intune-Berichte](reports.md).

#### <a name="consolidated-the-location-of-security-baselines-in-the-ui---6177074-----"></a>Konsolidierter Speicherort für Sicherheitsbaselines in der Benutzeroberfläche<!-- 6177074   -->
Wir haben die Pfade für die Suche nach [Sicherheitsbaselines](../protect/security-baselines.md) im Microsoft Endpoint Manager Admin Center konsolidiert, indem *Sicherheitsbaselines* aus allen UI-Speicherorten entfernt werden. Verwenden Sie nun den folgenden Pfad für die Suche nach Sicherheitsbaselines:  **Endpunktsicherheit** > **Sicherheitsbaselines**.

#### <a name="expanded-support-for-imported-pkcs-certificates---6044197----"></a>Erweiterte Unterstützung für importierte PKCS-Zertifikate<!-- 6044197  -->
Wir haben die Unterstützung für die Verwendung von [importierten PKCS-Zertifikaten](../protect/certificates-imported-pfx-configure.md#supported-platforms) erweitert, um *vollständig verwaltete Android Enterprise-Geräte zu unterstützen*. Im Allgemeinen wird das Importieren von PFX-Zertifikaten für S/MIME-Verschlüsselungsszenarios verwendet, in denen die Verschlüsselungszertifikate eines Benutzers auf allen Geräten erforderlich sind, damit die E-Mail-Entschlüsselung erfolgen kann.

Die folgenden Plattformen unterstützen den Import von PFX-Zertifikaten:

- Android: Geräteadministrator
- Android Enterprise: vollständig verwaltet
- Android Enterprise: Arbeitsprofil
- iOS
- Mac
- Windows 10

#### <a name="view-the-endpoint-security-configuration-for-devices---6206460----"></a>Anzeigen der Endpunktsicherheitskonfiguration für Geräte<!-- 6206460  -->
Wir haben im Microsoft Endpoint Manager Admin Center den Namen der Option für das Anzeigen von [Endpunktsicherheitskonfigurationen aktualisiert, die für ein bestimmtes Gerät gelten](../protect/security-baselines-monitor.md#view-endpoint-security-configurations-per-device). Diese Option wird in **Endpoint security configuration** (Konfiguration der Endpunktsicherheit) umbenannt, da entsprechende Sicherheitsbaselines und zusätzliche Richtlinien angezeigt werden, die außerhalb der Sicherheitsbaselines erstellt wurden. Diese Option hieß zuvor *Sicherheitsbaselines*.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Rollenbasierte Zugriffssteuerung

#### <a name="intune-roles-user-interface-changes-coming--5801612-----"></a>Benutzeroberfläche für Intune-Rollen wird bald geändert<!--5801612   -->
Die Benutzeroberfläche für [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Mandantenverwaltung** > **Rollen** wurde verbessert und ist jetzt benutzerfreundlicher und intuitiver. Nach der Aktualisierung haben Sie Zugriff auf dieselben Einstellungen und Details wie bisher. Der neue Prozess ähnelt dann aber eher einem Assistenten.

<!-- ########################## -->
## <a name="week-of-february-17-2020"></a>Woche des 17. Februar 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>App-Verwaltung

#### <a name="microsofts-new-office-app---5859926---"></a>Neue Office-App von Microsoft<!-- 5859926 -->
Die neue Office-App von Microsoft steht jetzt allgemein für den Download und die Nutzung bereit. Die Office-App ist eine konsolidierte Funktion, mit der Ihre Benutzer innerhalb einer App in Word, Excel und PowerPoint arbeiten können. Sie können eine App-Schutzrichtlinie für die App einrichten, um sicherzustellen, dass die Daten geschützt sind, auf die zugegriffen wird.

Weitere Informationen finden Sie unter [Aktivieren von App-Schutzrichtlinien für Intune mit der mobilen Vorschauversion der Office-App](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-how-to-enable-intune-app-protection-policies-with/ba-p/1045493).

<!-- ########################## -->

## <a name="week-of-february-10-2020"></a>Woche des 10. Februar 2020

### <a name="windows-7-ends-extended-support--3042987---"></a>Ende des erweiterten Supports für Windows 7<!--3042987 -->
Der erweiterte Support für Windows 7 endete am 14. Januar 2020. Gleichzeitig wurde die Intune-Unterstützung für Geräte eingestellt, auf denen Windows 7 ausgeführt wird. Technische Unterstützung und automatische Updates zum Schutz Ihres PCs sind nicht mehr verfügbar. Führen Sie ein Upgrade auf Windows 10 durch. Weitere Informationen finden Sie im [Blogbeitrag zum Planen der Änderung](https://aka.ms/Windows7_Intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>App-Verwaltung

#### <a name="microsoft-edge-version-77-and-later-on-windows-10-devices---5843584---"></a>Hiermit wird Microsoft Edge, Version 77 und höher auf Windows 10-Geräten hinzugefügt.<!-- 5843584 -->
Intune unterstützt nun die Deinstallation der Microsoft Edge-Version 77 und später auf Windows 10-Geräten. Weitere Informationen finden Sie unter [Hinzufügen von Microsoft Edge für Windows 10 zu Microsoft Intune](../apps/apps-windows-edge.md).

#### <a name="screen-removed-from-company-portal-android-work-profile-enrollment--6103987---"></a>Bildschirm aus dem Unternehmensportal bzw. der Android-Arbeitsprofilregistrierung entfernt<!--6103987 -->
Der Bildschirm **Wie geht es weiter?** wurde aus dem Registrierungsflow des Android-Arbeitsprofils im Unternehmensportal entfernt, um die Handhabung zu optimieren. Wechseln Sie zu [Registrieren mit dem Android-Arbeitsprofil](../user-help/enroll-device-android-work-profile.md), um den aktualisierten Registrierungsflow für das Android-Arbeitsprofil anzuzeigen.  

#### <a name="company-portal-app-improved-performance---6178652---"></a>Verbesserte Leistung der Unternehmensportal-App<!-- 6178652 -->
Die Unternehmensportal-App wurde aktualisiert und unterstützt jetzt eine verbesserte Leistung für Geräte mit ARM64-Prozessoren, z. B. das Surface Pro X. Zuvor wurde das Unternehmensportal in einem emulierten ARM32-Modus betrieben. In Version 10.4.7080.0 und höher ist jetzt die Unternehmensportal-App nativ für ARM64 kompiliert. Weitere Informationen zur Unternehmensportal-App finden Sie unter [Konfigurieren der Microsoft Intune-Unternehmensportal-App](../apps/company-portal-app.md).

<!-- ########################## -->
## <a name="week-of-january-27-2020"></a>Woche ab 27. Januar 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>App-Verwaltung

#### <a name="intune-support-for-additional-microsoft-edge-version-77-deployment-channel-for-macos---5983950----"></a>Intune-Unterstützung für einen zusätzlichen Bereitstellungskanal für macOS in Microsoft Edge-Version 77<!-- 5983950  -->
Microsoft Intune unterstützt jetzt den zusätzlichen Bereitstellungskanal **Stable** für die Microsoft Edge-App für macOS. Der **Stable Channel** wird für die umfassende Bereitstellung von Microsoft Edge in Unternehmensumgebungen empfohlen. Der Kanal wird alle sechs Wochen aktualisiert, und jedes Release umfasst Verbesserungen aus dem Kanal **Beta**. Zusätzlich zu den Kanälen **Stable** und **Beta** unterstützt Intune einen **Dev**-Kanal. Die öffentliche Vorschau bietet die Kanäle „Stable“ und „Dev“ für Microsoft Edge, Version 77 und höher, für macOS. Automatische Updates des Browsers sind standardmäßig aktiviert. Weitere Informationen finden Sie unter [Hinzufügen von Microsoft Edge zu macOS-Geräten mit Microsoft Intune](../apps/apps-edge-macos.md).

#### <a name="retirement-of-intune-managed-browser--5728447---"></a>Außerbetriebnahme von Intune Managed Browser<!--5728447 -->
Der Intune Managed Browser wird eingestellt. Verwenden Sie Microsoft Edge für Ihre geschützte Intune-Browserumgebung. Weitere Informationen finden Sie unter [Maßnahme erforderlich: Verwenden von Microsoft Edge für Ihre geschützte Intune-Browserumgebung](whats-new.md#take-action-use-microsoft-edge-for-your-protected-intune-browser-experience) im Abschnitt [Hinweise](whats-new.md#notices) weiter unten.

<!-- ########################## -->
## <a name="week-of-january-20-2020-2001-service-release"></a>Woche ab 20. Januar 2020 (Dienstrelease 2001)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>App-Verwaltung

#### <a name="user-experience-change-when-adding-apps-to-intune---4705829-----"></a>Veränderte Benutzeroberfläche beim Hinzufügen von Apps zu Intune<!-- 4705829   -->
Zum Hinzufügen von Apps zu Intune steht Ihnen eine neue Benutzeroberfläche zur Verfügung. Auf dieser Oberfläche können Sie auf dieselben Einstellungen und Details wie bisher zugreifen, allerdings ähnelt der neue Prozess zum Hinzufügen einer App zu Intune eher einem Assistenten. Diese neue Oberfläche bietet auch eine Seite zum Überprüfen der Einstellungen, bevor die App hinzugefügt wird. Wählen Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) die Option **Apps** > **Alle Apps** > **Hinzufügen** aus. Weitere Informationen finden Sie unter [Hinzufügen von Apps zu Microsoft Intune](../apps/apps-add.md).

#### <a name="require-win32-apps-to-restart----5622282-----"></a>Obligatorischer Neustart von Win32-Apps <!-- 5622282   -->
Sie können festlegen, dass eine Win32-App nach einer erfolgreichen Installation neu gestartet werden muss. Darüber hinaus können die Zeitspanne auswählen, die vergehen darf, bevor der Neustart erfolgen muss (Karenzzeit).

#### <a name="user-experience-change-when-configuring-apps-in-intune---4207990-----"></a>Änderung der Benutzeroberfläche beim Konfigurieren von Apps in Intune<!-- 4207990   -->
Beim Erstellen von App-Konfigurationsrichtlinien in Intune steht Ihnen jetzt eine neue Benutzeroberfläche zur Verfügung. Auf dieser Oberfläche können Sie auf dieselben Einstellungen und Details wie bisher zugreifen, allerdings ähnelt der neue Prozess zum Hinzufügen einer Richtlinie zu Intune eher einem Assistenten. Wählen Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) die Optionen **Apps** > **App-Konfigurationsrichtlinien** > **Hinzufügen** aus. Weitere Informationen finden Sie unter [App-Konfigurationsrichtlinien für Microsoft Intune](../apps/app-configuration-policies-overview.md). 

#### <a name="intune-support-for-additional-microsoft-edge-for-windows-10-deployment-channel---5861774---"></a>Intune-Unterstützung für einen zusätzlichen Bereitstellungskanal für Microsoft Edge für Windows 10<!-- 5861774 -->
Microsoft Intune unterstützt jetzt den zusätzlichen Bereitstellungskanal **Stable** für die Microsoft Edge-App (Version 77 und höher) für Windows 10. Der **Stable Channel** wird für die umfassende Bereitstellung von Microsoft Edge für Windows 10 in Unternehmensumgebungen empfohlen. Der Kanal wird alle sechs Wochen aktualisiert, und jedes Release umfasst Verbesserungen aus dem Kanal **Beta**. Zusätzlich zu den Kanälen **Stable** und **Beta** unterstützt Intune einen **Dev**-Kanal. Weitere Informationen finden Sie unter [Microsoft Edge für Windows 10 – Konfigurieren von App-Einstellungen](../apps/apps-windows-edge.md#configure-app-settings).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Gerätekonfiguration

#### <a name="improved-user-interface-experience-when-configuring-exchange-activesync-on-premises-connector-ui---5695492-----"></a>Verbesserte Benutzeroberfläche beim Konfigurieren des lokalen Connectors von Exchange ActiveSync<!-- 5695492   -->
Wir haben die Benutzeroberfläche beim [Konfigurieren des lokalen Connectors von Exchange ActiveSync](../protect/exchange-connector-install.md) aktualisiert. Die aktualisierte Benutzeroberfläche bietet einen zentralen Bereich zum Konfigurieren, Bearbeiten und Zusammenfassen der Details zu Ihrem lokalen Connector.

#### <a name="add-automatic-proxy-settings-to-wi-fi-profiles-for-android-enterprise-work-profiles---4490822-----"></a>Hinzufügen automatischer Proxyeinstellungen zu WLAN-Profilen für Android Enterprise-Arbeitsprofile<!-- 4490822   -->
Auf Geräten mit Android Enterprise-Arbeitsprofilen können Sie WLAN-Profile erstellen. Wenn Sie den Typ „Unternehmen“ für das WLAN auswählen, können Sie auch den EAP-Typ (Extensible Authentication Protocol) eingeben, der in Ihrem WLAN verwendet wird.

Wenn Sie jetzt den Typ „Unternehmen“ auswählen, können Sie auch automatische Proxyeinstellungen eingeben, z. B. eine Proxyserver-URL wie `proxy.contoso.com`.

Informationen zu den aktuellen WLAN-Einstellungen, die Sie konfigurieren können, finden Sie unter [Hinzufügen von WLAN-Einstellungen für Geräte mit Android Enterprise und Android-Kioskgeräte in Microsoft Intune](../configuration/wi-fi-settings-android-enterprise.md#work-profile-only).

Gilt für:
- Android Enterprise-Arbeitsprofil

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Geräteregistrierung

#### <a name="block-android-enrollments-by-device-manufacturer--5197392----"></a>Blockieren von Android-Registrierungen nach Gerätehersteller<!--5197392  -->
Sie können die Registrierung eines Geräts basierend auf dem Hersteller des Geräts blockieren. Dieses Feature gilt für Geräte mit Android-Geräteadministrator und dem Android Enterprise-Arbeitsprofil. Zum Anzeigen der Registrierungseinschränkungen navigieren Sie zu [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Geräte** > **Registrierungseinschränkungen**.

#### <a name="improvements-to-the-iosipados-create-enrollment-type-profile-ui---6055005---"></a>Verbesserungen an der Benutzeroberfläche zum Erstellen von Registrierungstypprofilen unter iOS/iPadOS<!-- 6055005 -->
Die Seite **Profil für Registrierungstyp erstellen** **Einstellungen** für die Registrierung von iOS/iPadOS-Benutzern wurde optimiert, um die Auswahl des **Registrierungstyps** zu verbessern und die Funktionalität beizubehalten. Sie finden die neue Benutzeroberfläche auf der Seite [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Geräte** > **iOS** > **iOS-Registrierung** > **Registrierungstypen** > **Profil erstellen** > **Einstellungen**. Weitere Informationen finden Sie unter [Erstellen eines Benutzerregistrierungsprofils in Intune](../enrollment/ios-user-enrollment.md#create-a-user-enrollment-profile-in-intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Geräteverwaltung

#### <a name="new-information-in-device-details---4471759-5604099----"></a>Neue Informationen in den Gerätedetails<!-- 4471759 5604099  -->
Die folgenden Informationen finden Sie jetzt auf der Seite **Übersicht** für Geräte:
- Arbeitsspeicherkapazität (Menge des physischen Arbeitsspeichers auf dem Gerät)
- Speicherkapazität (Menge des physischen Massenspeichers auf dem Gerät) 
- CPU-Architektur

#### <a name="ios-bypass-activation-lock-remote-action-renamed-to-disable-activation-lock---5904591----"></a>Remoteaktion „Aktivierungssperre umgehen“ für iOS umbenannt in „Aktivierungssperre deaktivieren“ <!--5904591  -->
Die Remoteaktion **Aktivierungssperre umgehen** wurde in **Aktivierungssperre deaktivieren** umbenannt. Weitere Informationen finden Sie unter [Deaktivieren der Aktivierungssperre für iOS mit Intune](../remote-actions/device-activation-lock-disable.md).

#### <a name="windows-10-feature-update-deployment-support-for-autopilot-devices---5948137-----"></a>Unterstützung der Bereitstellung von Windows 10-Featureupdates für Autopilot-Geräte<!-- 5948137   -->
Intune unterstützt jetzt die [Bereitstellung von Windows 10-Featureupdates](../protect/windows-update-for-business-configure.md#windows-10-feature-updates) für registrierte Autopilot-Geräte.

Richtlinien für Windows 10-Featureupdates können bei Autopilot-Ausführung über die Windows-Willkommensseite (Out Of Box Experience, OOBE) nicht angewendet werden und gelten erst bei der ersten Windows Update-Überprüfung nach der Bereitstellung eines Geräts (in der Regel ein Tag).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Überwachung und Problembehandlung

#### <a name="windows-autopilot-deployment-reports-preview----3856172-----"></a>Bereitstellungsberichte für Windows Autopilot (Vorschau) <!-- 3856172   -->
In einem neuen Bericht werden Informationen zu allen Geräten angegeben, die mit Windows Autopilot bereitgestellt wurden. Weitere Informationen finden Sie im [Autopilot-Bereitstellungsbericht](../enrollment/enrollment-autopilot.md#autopilot-deployments-report).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Rollenbasierte Zugriffssteuerung

#### <a name="new-intune-built-in-role-endpoint-security-manager--4253397-----"></a>Neue integrierte Intune-Rolle: Endpunktsicherheits-Manager<!--4253397   -->
Eine neue integrierte Intune-Rolle steht zur Verfügung: Endpunktsicherheits-Manager. Mit dieser neuen Rolle erhalten Administratoren Vollzugriff auf den Endpoint Manager-Knoten in Intune und schreibgeschützten Zugriff auf andere Bereiche. Die Rolle ist eine Erweiterung der Rolle „Sicherheitsadministrator“ aus Azure AD. Wenn Sie aktuell nur über die Rolle „Globale Administratoren“ verfügen, sind keine Änderungen erforderlich. Wenn Sie Rollen verwenden und die Granularität der Rolle „Endpoint Security Manager“ (Endpunktsicherheits-Manager) nutzen möchten, weisen Sie diese Rolle zu, wenn sie verfügbar ist. Weitere Informationen zu integrierten Rollen finden Sie unter [Rollenbasierte Zugriffssteuerung für Microsoft Intune](role-based-access-control.md).

<!-- ########################## -->
## <a name="week-of-january-6-2020"></a>Woche vom 6. Januar 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>App-Verwaltung

#### <a name="smime-support-for-microsoft-outlook-for-ios---2669398---"></a>S/MIME-Unterstützung für Microsoft Outlook für iOS<!-- 2669398 -->
Intune unterstützt die Bereitstellung von S/MIME-Signatur- und Verschlüsselungszertifikaten, die mit Outlook für iOS auf iOS-Geräten verwendet werden können. Weitere Informationen finden Sie unter [Vertraulichkeitsbezeichnung und Schutz in Outlook für iOS-und Android-](https://aka.ms/omsmime).

#### <a name="cache-win32-app-content-using-microsoft-connected-cache-server---6030314---"></a>Zwischenspeichern von Win32-App-Inhalten mithilfe eines Microsoft Connected Cache-Servers<!-- 6030314 -->
Sie können einen Microsoft Connected Cache-Server auf Ihren Configuration Manager-Verteilungspunkten installieren, um Inhalte von Intune Win32-Apps zwischenzuspeichern. Weitere Informationen finden Sie unter [Microsoft Connected Cache in Configuration Manager – Unterstützung für Intune Win32-Apps](https://docs.microsoft.com/configmgr/core/plan-design/hierarchy/microsoft-connected-cache#bkmk_intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Rollenbasierte Zugriffssteuerung

#### <a name="windows-10-administrative-templates-admx-profiles-now-support-scope-tags---5137390---"></a>Windows 10-Profile für administrative Vorlagen (ADMX) unterstützen jetzt Bereichsmarkierungen <!--5137390 -->
Sie können Bereichsmarkierungen jetzt Profilen für administrative Vorlagen (ADMX) zuweisen. Wechseln Sie zu diesem Zweck zu **Intune** > **Geräte** > **Konfigurationsprofile**. Wählen Sie in der Liste ein Profil für administrative Vorlagen und dann **Eigenschaften** > **Bereichsmarkierungen** aus. Weitere Informationen zu Bereichsmarkierungen finden Sie unter [Zuweisen von Bereichsmarkierungen zu anderen Objekten](../fundamentals/scope-tags.md#assign-scope-tags-to-other-objects).

<!-- ########################## -->
## <a name="week-of-december-30-2019"></a>Woche vom 30. Dezember 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>App-Verwaltung

#### <a name="retrieve-personal-recovery-key-from-mem-encrypted-macos-devices---4851745---"></a>Abrufen eines persönlichen Wiederherstellungsschlüssels von MEM-verschlüsselten macOS-Geräten<!-- 4851745 -->
Endbenutzer können mithilfe der Unternehmensportal-App für iOS ihren persönlichen Wiederherstellungsschlüssel (FileVault-Schlüssel) abrufen. Das Gerät mit dem persönlichen Wiederherstellungsschlüssel muss bei Intune registriert und über Intune mit FileVault verschlüsselt sein. Endbenutzer können mit der Unternehmensportal-App für iOS ihre persönlichen Wiederherstellungsschlüssel auf dem verschlüsselten macOS-Gerät abrufen, indem sie auf **Wiederherstellungsschlüssel abrufen** klicken. Sie können den Wiederherstellungsschlüssel auch aus Intune abrufen, indem Sie **Geräte** > *das verschlüsselte und registrierte macOS-Gerät* > **Wiederherstellungsschlüssel abrufen** auswählen. Weitere Informationen zu FileVault finden Sie unter [FileVault-Verschlüsselung für macOS](../protect/encrypt-devices.md#filevault-encryption-for-macos).

#### <a name="ios-and-ipados-user-licensed-vpp-apps---5619268---"></a>Von iOS- und iPadOS-Benutzern lizenzierte VPP-Apps<!-- 5619268 -->
Für benutzerseitig registrierte iOS- und iPadOS-Geräte werden den Endbenutzern keine neu erstellten und bereitgestellten VPP-Anwendungen mit Gerätelizenzierung mehr als verfügbar angeboten. Den Endbenutzern werden aber weiterhin alle benutzerseitig lizenzierten VPP-Apps im Unternehmensportal angezeigt. Weitere Informationen zu VPP-Apps finden Sie unter [Verwalten von iOS- und macOS-Apps, die über das Apple Volume Purchase Program mit Microsoft Intune erworben wurden](../apps/vpp-apps-ios.md).

<!-- ########################## -->
## <a name="week-of-december-23-2019"></a>Woche vom 23. Dezember 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>App-Verwaltung

#### <a name="notice---windows-10-1703-rs2-will-be-moving-out-of-support----5026679---"></a>Hinweis: Die Unterstützung für Windows 10 1703 (RS2) wird eingestellt. <!-- 5026679 -->
Am 9. Oktober 2018 endete für Windows 10 1703 (RS2) die Microsoft-Plattformunterstützung für die Home-, Pro- und Pro for Workstations-Editionen. Für Windows 10 Enterprise und die Education-Editionen endete die Plattformunterstützung für Windows 10 1703 (RS2) am 8. Oktober 2019. Am 26. Dezember 2019 wurde die mindestens erforderliche Version der Windows-Unternehmensportalanwendung auf Windows 10 1709 (RS3) angehoben. Computer, auf denen eine ältere als Version 1709 ausgeführt wird, werden nicht mehr mit aktualisierten Versionen der Anwendung aus dem Microsoft Store versorgt. Diese Änderung wurde den Kunden mit einer ältere Version von Windows 10 im Vorfeld über das Message Center mitgeteilt. Weitere Informationen finden Sie im [Informationsblatt zum Lebenszyklus von Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).

<!-- ########################## -->

## <a name="week-of-december-16-2019"></a>Woche vom 16. Dezember 2019

### <a name="device-configuration"></a>Gerätekonfiguration

#### <a name="updates-to-administrative-templates-for-windows-10-devices----5941568---"></a>Aktualisierungen an den administrativen Vorlagen für Windows 10-Geräte <!-- 5941568 -->

Sie können in Microsoft Intune mithilfe von ADMX-Vorlagen Einstellungen für Microsoft Edge, Office und Windows steuern und verwalten. Für die administrativen Vorlagen in Intune gelten die folgenden Aktualisierungen der Richtlinieneinstellungen:

- Unterstützung für Microsoft Edge-Versionen 78 und 79 hinzugefügt
- Umfasst die ADMX-Dateien vom 11. November 2019 in [Administrative Vorlagendateien (ADMX/ADML) und Office-Anpassungstool für Office 365 ProPlus, Office 2019 und Office 2016](https://www.microsoft.com/download/details.aspx?id=49030)

Weitere Informationen zu ADMX-Vorlagen in Intune finden Sie unter [Verwenden von Windows 10-Vorlagen zum Konfigurieren von Gruppenrichtlinieneinstellungen in Microsoft Intune](../configuration/administrative-templates-windows.md).

Gilt für:

- Windows 10 und höher

## <a name="week-of-december-9-2019-1912-service-release"></a>Woche vom 9. Dezember 2019 (1912 Dienstrelease)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>App-Verwaltung

#### <a name="migrating-to-microsoft-edge-for-managed-browsing-scenarios---5173762---"></a>Migrieren zu Microsoft Edge für das verwaltete Durchsuchen<!-- 5173762 -->
Im Hinblick auf die Einstellung von Intune Managed Browser wurden Änderungen an den App-Schutzrichtlinien vorgenommen, um die erforderlichen Schritte zu vereinfachen, die für die Umstellung Ihrer Benutzer auf Edge nötig sind. Die Optionen für die App-Schutzrichtlinieneinstellung **Übertragung von Webinhalt in andere Apps einschränken** wurden aktualisiert, sodass die folgenden Optionen verfügbar sind:

- Jede App
- Intune Managed Browser
- Microsoft Edge
- Nicht verwalteter Browser 

Wenn Sie **Microsoft Edge** auswählen, wird Ihren Endbenutzern Messaging für bedingten Zugriff angezeigt, das sie darüber benachrichtigt, dass Microsoft Edge für das verwaltete Durchsuchen erforderlich ist. Sie werden dazu aufgefordert, Microsoft Edge herunterzuladen und sich mit ihren AAD-Konten anzumelden, wenn sie dies noch nicht getan haben.  Dies entspricht einer Anwendung der App-Konfigurationseinstellung `com.microsoft.intune.useEdge`, die auf **True** festgelegt ist, auf Ihre MAM-fähigen Apps. In den vorhandenen App-Schutzrichtlinien, die die Einstellung **Mit Richtlinien verwaltete Browser** verwendet haben, ist jetzt **Intune Managed Browser** ausgewählt. Dabei ist keine Verhaltensänderung erkennbar. Das bedeutet, dass Ihren Benutzern Messaging zur Verwendung von Microsoft Edge angezeigt wird, wenn Sie die App-Konfigurationseinstellung **useEdge** auf **True** festgelegt haben. Wir empfehlen allen Kunden, die verwalteten Browserszenarios nutzen, ihre App-Schutzrichtlinien mit der Einstellung **Übertragung von Webinhalt in andere Apps einschränken** zu aktualisieren, um sicherzustellen, dass Benutzer die richtigen Anleitungen für den Übergang zu Microsoft Edge sehen, unabhängig davon, welche App sie verwenden. 

#### <a name="configure-app-notification-content-for-organization-accounts---2576686----"></a>Konfigurieren von App-Benachrichtigungsinhalt für Organisationskonten<!-- 2576686  -->
Intune-App-Schutzrichtlinien auf Android- und iOS-Geräten ermöglichen es Ihnen, den App-Benachrichtigungsinhalt für Organisationskonten zu steuern. Sie können eine Option („Zulassen“, „Organisationsdaten blockieren“ oder „Blockiert“) auswählen, um anzugeben, wie Benachrichtigungen für Organisationskonten für die ausgewählte App angezeigt werden. Dieses Feature erfordert Unterstützung von Anwendungen und ist möglicherweise nicht für alle Anwendungen mit APP-Aktivierung verfügbar. Outlook für iOS, Version 4.15.0 (oder höher) und Outlook für Android, Version 4.83.0 (oder höher) unterstützen diese Einstellung. Die Einstellung ist in der Konsole verfügbar, aber die Funktionalität ist erst ab dem 16. Dezember 2019 in Kraft. Weitere Informationen zu Intune-App-Schutzrichtlinien finden Sie unter [Was sind App-Schutzrichtlinien?](../apps/app-protection-policy.md)

#### <a name="microsoft-app-icons-update--4677605----"></a>Aktualisierung der Microsoft-App-Symbole<!--4677605  -->
Die für Microsoft-Apps im App-Zielbereich verwendeten Symbole für App-Schutzrichtlinien und App-Konfigurationsrichtlinien wurden aktualisiert.

#### <a name="require-use-of-approved-keyboards-on-android--4761794----"></a>Erforderliche Verwendung von genehmigten Tastaturen unter Android<!--4761794  -->
Im Rahmen einer App-Schutzrichtlinie können Sie die Einstellung [**Zugelassene Tastaturen**](../apps/app-protection-policy-settings-android.md#data-protection) festlegen, um zu verwalten, welche Android-Tastaturen mit verwalteten Android-Apps verwendet werden können. Wenn ein Benutzer die verwaltete App öffnet und nicht bereits eine genehmigte Tastatur für diese App verwendet, wird er aufgefordert, zu einer der genehmigten Tastaturen zu wechseln, die bereits auf seinem Gerät installiert sind. Bei Bedarf wird den Benutzern ein Link zum Download einer genehmigten Tastatur aus dem Google Play Store angezeigt, die sie installieren und einrichten können. Die Benutzer können nur dann Textfelder in einer verwalteten App bearbeiten, wenn die aktive Tastatur eine genehmigte Tastatur ist.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Gerätekonfiguration

#### <a name="updated-single-sign-on-experience-for-apps-and-websites-on-your-ios-ipados-and-macos-devices---4999578----"></a>Aktualisiertes SSO-Verhalten für Apps und Websites auf iOS-, iPadOS- und macOS-Geräten<!-- 4999578  -->
In Intune wurden weitere Einstellungen für das einmalige Anmelden (Single Sign-On, SSO) für iOS-, iPadOS- und macOS-Geräte hinzugefügt. Sie können ab sofort eine Umleitung für SSO-App-Erweiterungen konfigurieren, die von Ihrer Organisation oder Ihrem Identitätsanbieter geschrieben wurden. Verwenden Sie diese Einstellungen, um ein nahtloses SSO-Verhalten für Apps und Websites zu konfigurieren, die moderne Authentifizierungsmethoden wie beispielsweise OAuth und SAML2 verwenden. 

Diese neuen Einstellungen erweitern die bisherigen Einstellungen für SSO-App-Erweiterungen und die integrierte Kerberos-Erweiterung von Apple (**Geräte** > **Gerätekonfiguration** > **Profile** > **Profil erstellen** > **iOS/iPadOS** oder **macOS** für den Plattformtyp > **Gerätefunktionen** für den Profiltyp). 

Um eine vollständige Liste der Einstellungen für SSO-App-Erweiterungen anzuzeigen, die Sie konfigurieren können, wechseln Sie zu [SSO unter iOS](../configuration/ios-device-features-settings.md#single-sign-on-app-extension) und [SSO unter macOS](../configuration/macos-device-features-settings.md#single-sign-on-app-extension).

Gilt für:

- iOS/iPadOS
- macOS

#### <a name="we-have-updated-two-device-restriction-settings-for-ios-and-ipados-devices-to-correct-their-behavior---5701352------"></a>Wir haben zwei Einstellungen zur Geräteeinschränkung für iOS- und iPadOS-Geräte aktualisiert, um deren Verhalten zu korrigieren<!-- 5701352    -->
Für iOS-Geräte können Sie Geräteeinschränkungsprofile mit den Einstellungen **Drahtlose PKI-Updates zulassen** und **Modus mit USB-Einschränkung blockieren**. (**Geräte** > **Gerätekonfiguration** > **Profile** > **Profil erstellen** > **iOS/iPadOS** für Plattform > **Geräteeinschränkungen** für Profiltyp). Vor diesem Release waren die Benutzeroberflächeneinstellungen und Beschreibungen für die folgenden Einstellungen falsch, diese wurden nun korrigiert. Ab diesem Release lautet das Einstellungsverhalten wie folgt:

**Drahtlose PKI-Updates blockieren**: **Blockieren**: Verhindert, dass Ihre Benutzer Softwareupdates erhalten, wenn das Gerät nicht an einen Computer angeschlossen ist. **Nicht konfiguriert** (Standardeinstellung): Ermöglicht es einem Gerät, Softwareupdates zu empfangen, ohne mit einem Computer verbunden zu sein.
- Bisher konnte diese Einstellung auf **Zulassen** festgelegt werden, um es Ihren Benutzern zu ermöglichen, Softwareupdates zu empfangen, ohne ihre Geräte mit einem Computer verbinden zu müssen.
**USB-Zubehör bei gesperrtem Gerät zulassen**: **Zulassen**: USB-Zubehör kann Daten mit einem Gerät austauschen, das seit mehr als einer Stunde gesperrt ist. **Nicht konfiguriert** (Standardeinstellung): Der Modus mit USB-Einschränkung auf dem Gerät wird nicht aktualisiert, und USB-Zubehör wird daran gehindert, Daten vom Gerät zu übertragen, wenn dieses länger als eine Stunde gesperrt ist.
- Bisher konnte diese Einstellung auf **Blockieren** festgelegt werden, um den Modus mit USB-Einschränkung auf überwachten Geräten zu deaktivieren.

Weitere Informationen zu allen konfigurierbaren Einstellungen finden Sie unter [iOS- und iPadOS-Geräteeinstellungen zum Zulassen oder Einschränken von Funktionen mit Intune](../configuration/device-restrictions-ios.md).

Diese Funktion gilt für:

- OS/iPadOS

#### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>Gerätekonfigurationsprofil für das kabelgebundene Netzwerk für macOS-Geräte<!-- 3508686  -->
   > [!NOTE]
   > Diese Funktion hat sich verzögert, wird aber bald veröffentlicht.

#### <a name="block-users-from-configuring-certificate-credentials-in-the-managed-keystore-on-android-enterprise-device-owner-devices---3311998---"></a>Sperren der Konfiguration von Zertifikatanmeldeinformationen im verwalteten Schlüsselspeicher auf Android Enterprise-Gerätebesitzergeräten durch die Benutzer<!-- 3311998 -->
Auf Android Enterprise-Gerätebesitzergeräten können Sie die Benutzer mithilfe einer neuen Einstellung daran hindern, ihre Zertifikatanmeldeinformationen im verwalteten Schlüsselspeicher zu konfigurieren (**Gerätekonfiguration** > **Profile** > **Profil erstellen** > **Android Enterprise** für Plattform > **Nur Gerätebesitzer > Geräteeinschränkungen** für Profiltyp > **Benutzer und Konten**).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Geräteverwaltung

#### <a name="protected-wipe-action-now-available--51150000---"></a>Geschütztes Zurücksetzen ab sofort verfügbar<!--51150000 -->
Sie haben jetzt die Möglichkeit, die Aktion „Gerät zurücksetzen“ zu verwenden, um Ihr Gerät geschützt zurückzusetzen. Das geschützte Zurücksetzen entspricht der Standardzurücksetzung, mit dem Unterschied, dass der Vorgang nicht durch Ausschalten des Geräts umgangen werden kann. Beim geschützten Zurücksetzen wird solange versucht, das Gerät zurückzusetzen, bis der Vorgang erfolgreich ist. In einigen Konfigurationen kann das Gerät aufgrund dieser Aktion nicht neu gestartet werden. Weitere Informationen finden Sie auf der Seite [Abkoppeln oder Zurücksetzen von Geräten](../remote-actions/devices-wipe.md).

#### <a name="device-ethernet-mac-address-added-to-devices-overview-page--5562275---"></a>Ethernet-MAC-Geräteadresse auf der Übersichtsseite des Geräts hinzugefügt<!--5562275 -->
Sie können ab sofort die Ethernet-MAC-Geräteadresse auf der Seite mit den Gerätedetails anzeigen (**Geräte** > **Alle Geräte** > Auswählen eines Geräts > **Übersicht**.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Gerätesicherheit

#### <a name="improved-experience-on-a-shared-device-when-device-based-conditional-access-policies-are-enabled---1734096----"></a>Verbesserte Funktionalität auf einem gemeinsam genutzten Gerät, wenn gerätebasierte Richtlinien für bedingten Zugriff aktiviert sind<!-- 1734096  -->
Das Benutzererlebnis für ein gemeinsam genutztes Gerät mit mehreren Benutzern, für die gerätebasierte Richtlinien für bedingten Zugriff gelten, wurde verbessert, indem bei der Erzwingung der Richtlinie die neueste Konformitätsbewertung für den Benutzer überprüft wird. Weitere Informationen finden Sie in den folgenden Artikeln:
- [Azure-Übersicht zum bedingten Zugriff](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
- [Übersicht über die Intune-Gerätekonformität](../protect/device-compliance-get-started.md)

#### <a name="use-pkcs-certificate-profiles-to-provision-devices-with-certificates---2317124-2317130-2317139-2340517-2340528-2340529----"></a>Verwendung von PKCS-Zertifikatprofilen zum Bereitstellen von Geräten mit Zertifikaten<!-- 2317124, 2317130, 2317139, 2340517, 2340528, 2340529  -->
Sie können ab sofort PKCS-Zertifikatprofile verwenden, um Zertifikate für *Geräte* auszustellen, die Android for Work, iOS/iPadOS und Windows ausführen, wenn sie mit Profilen wie denen für WLAN und VPN verknüpft sind. Zuvor unterstützten diese drei Plattformen nur benutzerbasierte Zertifikate, die gerätebasierte Unterstützung war auf macOS beschränkt.

> [!NOTE]
> PKCS-Zertifikatprofile werden nicht mit WLAN-Profilen unterstützt. Wählen Sie stattdessen SCEP-Zertifikatsprofile, wenn Sie einen [EAP-Typ](../configuration/wi-fi-settings-windows.md#enterprise-profile) verwenden.

Um ein gerätebasiertes Zertifikat zu erstellen, wählen Sie [während der Erstellung eines PKCS-Zertifikatprofils](../protect/certficates-pfx-configure.md#create-a-pkcs-certificate-profile) für die unterstützten Plattformen **Einstellungen** aus. Daraufhin wird die Einstellung **Zertifikattyp** angezeigt, die Optionen für Gerät oder Benutzer unterstützt.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Überwachung und Problembehandlung

#### <a name="centralized-audit-logs--5603185-5697164---"></a>Zentralisierte Überwachungsprotokolle<!--5603185, 5697164 -->
Eine neue zentralisierte Benutzeroberfläche für Überwachungsprotokolle sammelt erfasst ab sofort die Überwachungsprotokolle für alle Kategorien auf einer Seite. Sie können die Protokolle filtern, um die Daten abzurufen, nach denen Sie suchen. Wechseln Sie zum Anzeigen der Überwachungsprotokolle zu **Mandantenverwaltung** > **Überwachungsprotokolle**. 

#### <a name="scope-tag-information-included-in-audit-log-activity-details--5763534---"></a>Einschluss von Informationen zu Bereichstags in Aktivitätsdetails von Überwachungsprotokollen<!--5763534 -->
Die Details zu Überwachungsprotokollaktivitäten enthalten ab sofort auch Informationen zu den Bereichstags (für Intune-Objekte, die Bereichstags unterstützen). Weitere Informationen zu Überwachungsprotokollen finden Sie unter [Verwenden von Überwachungsprotokollen zum Nachverfolgen und Überwachen von Ereignissen](monitor-audit-logs.md).

<!-- ########################## -->
## <a name="week-of-december-2-2019"></a>Woche des 2. Dezember 2019

#### <a name="new-microsoft-endpoint-configuration-manager-co-management-licensing--5027281--"></a>Neue Lizenzierung der Co-Verwaltung von Microsoft Endpoint Configuration Manager<!--5027281-->
Configuration Manager-Kunden mit Software Assurance können die Intune-Co-Verwaltung für Windows 10-PCs nutzen, ohne eine zusätzliche Intune-Lizenz für die Co-Verwaltung erwerben zu müssen. Kunden müssen ihren Endbenutzern nicht mehr einzelne Intune-/EMS-Lizenzen für die Co-Verwaltung von Windows 10 zuweisen.
- Geräte, die von Configuration Manager verwaltet und bei der Co-Verwaltung registriert werden, verfügen nahezu über die gleichen Rechte wie über MDM in eigenständigem Intune verwaltete PCs. Nach dem Zurücksetzen können sie jedoch nicht mithilfe von Autopilot nochmals bereitgestellt werden.
- Windows 10-Geräte, die anderweitig bei Intune registriert sind, benötigen vollständige Intune-Lizenzen.
- Geräte auf anderen Plattformen benötigen weiterhin vollständige Intune-Lizenzen.

Weitere Informationen finden Sie unter [Lizenzierungsbestimmungen](https://www.microsoft.com/en-us/Licensing/product-licensing/products).

<!-- ########################## -->
## <a name="week-of-november-18-2019-1911-service-release"></a>Woche vom 18. November 2019 (1911 Dienstrelease)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>App-Verwaltung

#### <a name="ui-update-when-selectively-wiping-app-data---4102028---"></a>Benutzeroberflächenupdate beim selektiven Löschen von App-Daten<!-- 4102028 -->
Die Benutzeroberfläche zum selektiven Löschen von App-Daten in Intune wurde aktualisiert. Die Änderungen der Benutzeroberfläche umfassen:
- eine vereinfachte Funktion mithilfe eines Formats im Assistentenstil in einem einzigen Bereich
- Ein Update für den Erstellungsflow zum Einschließen von Zuweisungen.
- Eine zusammengefasste Seite aller festgelegten Einstellungen beim Anzeigen der Eigenschaften, bevor eine neue Richtlinie erstellt wird oder bei der Bearbeitung einer Eigenschaft. Beim Bearbeiten von Eigenschaften zeigt die Zusammenfassung nur eine Liste der Elemente aus der Kategorie der Eigenschaften an, die bearbeitet werden.

Weitere Informationen finden Sie unter [Zurücksetzen nur von Unternehmensdaten aus mit Intune verwalteten Apps](../apps/apps-selective-wipe.md).

#### <a name="ios-and-ipados-third-party-keyboard-support---4922950---"></a>Unterstützung von Tastaturen von Drittanbietern in iOS und iPadOS<!-- 4922950 -->
Im März 2019 haben wir angekündigt, dass die Unterstützung für die App-Schutzrichtlinie „Tastaturen von Drittanbietern“ für iOS aufgehoben wurde. Das Feature kehrt sowohl mit iOS- als auch mit iPadOS-Unterstützung zu Intune zurück. Wählen Sie die Registerkarte **Datenschutz** einer neuen oder bestehenden iOS/iPadOS-App-Schutzrichtlinie aus, um diese Einstellung zu aktivieren, und suchen Sie die Einstellung **Tastaturen von Drittanbietern** unter **Datenübertragung**.

Das Verhalten dieser Richtlinieneinstellung unterscheidet sich leicht von der vorherigen Implementierung. In Apps mit mehreren Identitäten mit SDK-Version 12.0.16 und höher, für die App-Schutzrichtlinien gelten, für die diese Einstellung als **Blockieren** konfiguriert ist, können Endbenutzer weder in ihrem Organisations- noch in ihrem persönlichen Konto Drittanbietertastaturen auswählen. Apps, die SDK-Versionen 12.0.12 und früher verwenden, zeigen weiterhin das Verhalten, das in unserem Blogbeitrag mit dem Titel [Bekanntes Problem: Tastaturen von Drittanbietern werden in iOS für persönliche Konten nicht blockiert](https://aka.ms/3rdparty_iOS_Intune) dokumentiert ist.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Gerätekonfiguration

#### <a name="target-macos-user-groups-to-require-jamf-management---4061739----"></a>Erzwingen der Jamf-Verwaltung für macOS-Benutzergruppen<!-- 4061739  --> 
Sie können festlegen, dass für bestimmte Benutzergruppen [macOS-Geräte von Jamf verwaltet werden](../protect/conditional-access-integrate-jamf.md). Auf diese Weise können Sie die Integration der Jamf-Konformität auf eine Teilmenge von macOS-Geräten anwenden, während andere Geräte von Intune verwaltet werden. Wenn Sie bereits die Jamf-Integration verwenden, werden standardmäßig alle Benutzer für die Integration festgelegt.

#### <a name="new-exchange-activesync-settings-when-creating-an-email-device-configuration-profile-on-ios-devices---4892824-----"></a>Neue Exchange ActiveSync-Einstellungen beim Erstellen eines E-Mail-Gerätekonfigurationsprofils auf iOS-Geräten<!-- 4892824   --> 
Sie können auf iOS- und iPadOS-Geräten die E-Mail-Konnektivität in einem Gerätekonfigurationsprofil konfigurieren (**Gerätekonfiguration** > **Profile** > **Profil erstellen** > **iOS/iPadOS** für Plattform > **E-Mail** für den Profiltyp). 

Es sind neue Exchange ActiveSync-Einstellungen verfügbar, einschließlich:
- **Zu synchronisierende Exchange-Daten:** Wählen Sie die zu synchronisierenden (oder zu blockierenden) Exchange-Dienste für Kalender, Kontakte, Erinnerungen und E-Mail aus.
- **Benutzern das Ändern der Synchronisierungseinstellungen erlauben:** Erlauben Sie Benutzern, die Synchronisierungseinstellungen für diese Dienste auf ihren Geräten zu ändern (oder blockieren Sie sie).  

Weitere Informationen zu diesen Einstellungen finden Sie unter [E-Mail-Profileinstellungen für iOS-Geräte in Intune](../configuration/email-settings-ios.md). 

Gilt für:

- iOS 13.0 und neuer
- iOS 13.0 und höher

#### <a name="prevent-users-from-adding-personal-google-accounts-to-android-enterprise-fully-managed-and-dedicated-devices---5353228-----"></a>Verhindern, dass Benutzer persönliche Google-Konten zu vollständig verwalteten und dedizierten Geräten von Android Enterprise hinzufügen<!-- 5353228   -->
Auf vollständig verwalteten und dedizierten Android Enterprise-Geräten gibt es eine neue Einstellung, die Benutzer daran hindert, persönliche Google-Konten zu erstellen (**Gerätekonfiguration** > **Profile** > **Profil erstellen** > **Android Enterprise** als Plattform > **Nur Gerätebesitzer > Geräteeinschränkungen** als Profiltyp > **Benutzer- und Konteneinstellungen** > **Persönliche Google-Konten**).

Sie finden die konfigurierbaren Einstellungen unter [Android Enterprise-Geräteeinstellungen zum Zulassen oder Einschränken von Features mit Intune](../configuration/device-restrictions-android-for-work.md).

Gilt für:

- Vollständig verwaltete Android Enterprise-Geräte
- Dedizierte Android Enterprise-Geräte

#### <a name="server-side-logging-for-siri-commands-setting-is-removed-in-iosipados-device-restrictions-profile----5468501-----"></a>Entfernung der serverseitigen Protokollierung für die Einstellung der Siri-Befehle im iOS/iPadOS-Profil zur Geräteeinschränkung <!-- 5468501   -->
Auf iOS- und iPadOS-Geräten wird die Einstellung **Serverseitige Protokollierung für Siri-Befehle** aus der Microsoft Endpoint Manager-Verwaltungskonsole entfernt (**Gerätekonfiguration** > **Profile** > **Profil erstellen** > **iOS/iPadOS** für Plattform > **Geräteeinschränkungen** für Profiltyp > **integrierte Apps**). 

Diese Einstellung hat keinen Einfluss auf die Geräte. Öffnen Sie das Profil, nehmen Sie alle Änderungen vor, und speichern Sie das Profil, um die Einstellung aus bestehenden Profilen zu entfernen. Das Profil wird aktualisiert, und die Einstellung wird von den Geräten gelöscht.

Sie finden alle konfigurierbaren Einstellungen unter [iOS- und iPadOS-Geräteeinstellungen zum Zulassen oder Einschränken von Funktionen mit Intune](../configuration/device-restrictions-ios.md).

Gilt für:

- iOS/iPadOS

#### <a name="windows-10-feature-updates-public-preview---2384877---"></a>Windows 10-Featureupdates (öffentliche Vorschau)<!-- 2384877 -->
Sie können [Windows 10-Featureupdates](../protect/windows-update-for-business-configure.md#windows-10-feature-updates) nun auf Windows 10-Geräten bereitstellen. Windows 10-Featureupdates stellen eine neue Softwareupdaterichtlinie dar, die die Version von Windows 10 festgelegt, die von Geräten installiert und beibehalten werden soll Sie können diesen neuen Richtlinientyp zusammen mit Ihren vorhandenen Windows 10-Updateringen verwenden.

Geräte, die Windows 10-Featureupdaterichtlinien erhalten, installieren die angegebene Windows-Version und verbleiben anschließend bei dieser Version, bis die Richtlinie geändert oder entfernt wird. Geräte, auf denen eine spätere Version von Windows ausgeführt wird, verbleiben bei ihrer aktuellen Version. Geräte, auf denen eine bestimmte Version von Windows eingerichtet ist, können noch immer Qualitäts- und Sicherheitsupdates für diese Version über die Windows 10-Updateringe installieren.

Dieser neue Richtlinientyp wird diese Woche für Mandanten eingeführt. Wenn diese Richtlinie noch nicht für Ihren Mandanten verfügbar ist, wird sie in Kürze verfügbar sein.

#### <a name="add-and-change-key-information-in-plist-files-for-macos-applications---4736278---"></a>Hinzufügen und Ändern von Schlüsselinformationen in PLIST-Dateien für macOS-Anwendungen<!-- 4736278 -->
Auf macOS-Geräten können Sie nun ein Gerätekonfigurationsprofil erstellen, das eine Datei mit der Eigenschaftenliste (.plist) hochlädt, die einer App oder dem Gerät zugeordnet ist (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **macOS** für Plattform > **Einstellungsdatei** für Profiltyp).

Nur einige Apps unterstützen verwaltete Einstellungen, und diese Apps erlauben es Ihnen möglicherweise nicht, alle Einstellungen zu verwalten. Stellen Sie sicher, dass Sie eine Datei mit Eigenschaftenliste hochladen, die die Gerätekanaleinstellungen und nicht die Benutzerkanaleinstellungen konfiguriert.

Weitere Informationen zu diesem Feature finden Sie unter [Hinzufügen einer Datei mit Eigenschaftenliste zu macOS-Geräten mit Microsoft Intune](../configuration/preference-file-settings-macos.md).

Gilt für:

- macOS-Geräte mit Version 10.7 und höher

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Geräteverwaltung

#### <a name="edit-device-name-value-for-autopilot-devices---2640074---"></a>Bearbeiten des Werts des Gerätenamens für Autopilot-Geräte<!-- 2640074 -->
Sie können den Wert für den Gerätenamen für in Azure AD eingebundene Autopilot-Geräte bearbeiten.  Weitere Informationen finden Sie unter [Bearbeiten von Attributen für Autopilot-Geräte](../enrollment/enrollment-autopilot.md#edit-autopilot-device-attributes).

#### <a name="edit-group-tag-value-for-autopilot-devices---4816775-----"></a>Bearbeiten des Werts des Gruppentags für Autopilot-Geräte<!-- 4816775   -->
Sie können den Wert des Gruppentags für Autopilot-Geräte bearbeiten. Weitere Informationen finden Sie unter [Bearbeiten von Attributen für Autopilot-Geräte](../enrollment/enrollment-autopilot.md#edit-autopilot-device-attributes).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Überwachung und Problembehandlung

#### <a name="updated-support-experience---5012398---"></a>Aktualisierte Benutzeroberfläche für Support<!-- 5012398 -->

Ab heute wird eine aktualisierte und optimierte konsoleninterne Benutzeroberfläche für [Hilfe und Support für Intune](get-support.md) an die Mandanten verteilt. Wenn diese neue Benutzeroberfläche noch nicht für Sie verfügbar ist, wird sie in Kürze verfügbar sein.

Wir haben die konsoleninterne Suche und das Feedback zu häufigen Problemen sowie den Workflow, den Sie zum Kontaktieren des Supports verwenden, verbessert. Wenn Sie ein Supportproblem öffnen, sehen Sie Echtzeitschätzwerte für den Zeitraum, in dem Sie mit einem Rückruf oder einer E-Mail-Antwort rechnen können, und Premier Support- und Unified Support-Kunden können problemlos einen Schweregrad für ihr Problem festlegen, um schneller Support zu erhalten.

#### <a name="improved-intune-reporting-experience-public-preview----3791418---"></a>Verbesserte Berichterstellungsfunktionen (öffentliche Vorschauversion) in Intune <!-- 3791418 -->
Intune bietet nun verbesserte Berichtserstellungsfunktionen, einschließlich neuer Berichtstypen, besserer Berichtsorganisation, fokussierterer Ansichten, verbesserter Berichtsfunktionen sowie konsistenterer und aktuellerer Daten. Neue Berichtstypen konzentrieren sich auf Folgendes:

- **Operational** (betriebsbedingt): stellt neue Berichte mit einem negativen Integritätsfokus bereit 
- **Organizational** (organisationsbedingt): stellt eine umfassendere Zusammenfassung des Gesamtzustands bereit
- **Historical** (verlaufsbedingt): stellt Muster und Trends über einen bestimmten Zeitraum bereit
- **Specialist** (spezialisiert): ermöglicht die Verwendung von Rohdaten zur Erstellung Ihrer eigenen benutzerdefinierten Berichte

Die ersten neuen Berichte konzentrieren sich auf die Gerätekonformität. Weitere Informationen finden Sie im Blogbeitrag [Neues Berichtserstellungsframework für Microsoft Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/New-Reporting-Framework-Coming-to-Intune/ba-p/1009553) und unter [Intune-Berichte](reports.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Rollenbasierte Zugriffssteuerung

#### <a name="duplicate-custom-or-built-in-roles----1081938-----"></a>Duplizieren benutzerdefinierter und integrierter Rollen <!-- 1081938   -->
Sie können jetzt integrierte und benutzerdefinierte Rollen kopieren. Weitere Informationen finden Sie unter [Kopieren einer Rolle](../fundamentals/create-custom-role.md#copy-a-role).

#### <a name="new-permissions-for-school-administrator-role----5621805----"></a>Neue Berechtigungen für die Rolle „Schuladministrator“ <!-- 5621805  -->  
Zwei neue Berechtigungen (**Profil zuweisen** und **Gerät synchronisieren**) wurden der Rolle „Schuladministrator“ hinzugefügt > **Berechtigungen** > **Registrierungsprogramme**. Die Berechtigung für das Synchronisierungsprofil ermöglicht es Gruppenadministratoren, Windows Autopilot-Geräte zu synchronisieren. Mit der Berechtigung zum Zuweisen von Profilen können sie benutzerinitiierte Apple-Registrierungsprofile löschen. Es gibt ihnen auch die Berechtigung, die Zuweisung von Autopilot-Geräten und Autopilot-Bereitstellungsprofilen zu verwalten. Eine Liste aller Schuladministrator-/Gruppenadministratorrechte finden Sie unter [Zuweisen von Gruppenadministratoren](https://docs.microsoft.com/intune-education/group-admin-delegate).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>Sicherheit

#### <a name="bitlocker-key-rotation---2564951----"></a>BitLocker-Schlüsselrotation<!-- 2564951  -->
Sie können eine Intune-Geräteaktion verwenden, um [BitLocker-Wiederherstellungsschlüssel](../protect/encrypt-devices.md#rotate-bitlocker-recovery-keys) für verwaltete Geräte, die mit Windows Version 1909 oder höher ausgeführt werden, remote zu rotieren. Geräte müssen so konfiguriert sein, dass sie die Rotation von Wiederherstellungsschlüssel unterstützen, damit sie für die Rotation von Wiederherstellungsschlüsseln qualifiziert sind.  

#### <a name="updates-to-dedicated-device-enrollment-to-support-scep-device-certificate-deployment----5198878----"></a>Updates zur Registrierung für dedizierte Geräte zur Unterstützung der Bereitstellung von SCEP-Gerätezertifikaten <!-- 5198878  -->
Intune unterstützt nun die Bereitstellung von SCEP-Gerätezertifikaten auf dedizierten Android Enterprise-Geräten für den zertifikatbasierten Zugriff auf WLAN-Profile. Die Microsoft Intune-App muss auf dem Gerät vorhanden sein, damit die Bereitstellung funktioniert. Aus diesem Grund wurde die Registrierungsfunktion für dedizierte Android Enterprise-Geräte aktualisiert. Der Registrierungsvorgang ist am Anfang gleich (mit QR, NFC, ohne Benutzereingriff oder Gerätebezeichner), aber jetzt ist ein Schritt dazugekommen, der die Installation der Intune-App durch den Benutzer erfordert. Bestehende Geräte werden jetzt die App automatisch und fortlaufend installieren.

#### <a name="intune-audit-logs-for-business-to-business-collaboration--5670211---"></a>Intune-Überwachungsprotokolle für die Business-to-Business Zusammenarbeit<!--5670211 -->
Die Business-to-Business-Zusammenarbeit (B2B) ermöglicht es Ihnen, die Anwendungen und Dienste Ihres Unternehmens sicher mit Gastbenutzern aus anderen Organisationen zu teilen, während Sie die Kontrolle über Ihre eigenen Unternehmensdaten behalten. Intune unterstützt nun Überwachungsprotokolle für B2B-Gastbenutzer. Wenn Gastbenutzer beispielsweise Änderungen vornehmen, kann Intune diese Daten über Überwachungsprotokolle erfassen. Weitere Informationen hierzu finden Sie unter [Was ist der Gastzugriff in Azure Active Directory-B2B?](https://docs.microsoft.com/azure/active-directory/b2b/what-is-b2b)

<!-- ########################## -->
## <a name="week-of-november-11-2019"></a>Woche vom 11. November 2019  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>App-Verwaltung  

#### <a name="improved-macos-enrollment-experience-in-company-portal----5074349----"></a>Verbesserte macOS-Registrierungsoberfläche im Unternehmensportal <!-- 5074349  -->  
Das Unternehmensportal für die macOS-Registrierung verfügt über einen einfacheren Registrierungsprozess, der sich enger an das Unternehmensportal für die iOS-Registrierung ausrichtet. Gerätebenutzer wird jetzt Folgendes angezeigt:  

- Eine schlankere Benutzeroberfläche  
- Eine verbesserte Prüfliste für die Registrierung  
- Deutlichere Anweisungen zum Registrieren ihrer Geräte  
- Verbesserte Optionen zur Problembehandlung  

#### <a name="web-apps-launched-from-the-windows-company-portal-app---5030972---"></a>Web-Apps, die aus der Windows-Unternehmensportal-App gestartet werden<!-- 5030972 -->
Endbenutzer können Web-Apps jetzt direkt aus der Windows-Unternehmensportal-App starten. Endbenutzer können die Web-App und dann die Option **Im Browser öffnen** auswählen. Die veröffentlichte Web-URL wird direkt einem Webbrowser geöffnet. Diese Funktionalität wird in der nächsten Woche eingeführt. Weitere Informationen über Web-Apps finden Sie unter [Hinzufügen von Web-Apps zu Microsoft Intune](../apps/web-app.md).  

#### <a name="new-assignment-type-column-in-company-portal-for-windows-10----5459950----"></a>Neue Spalte für den Zuweisungstyp im Unternehmensportal für Windows 10 <!-- 5459950  -->
Die Spalte im Unternehmensportal unter **Installierte Apps** > **Zuweisungstyp** wurde in **Von Ihrer Organisation als erforderlich festgelegt** umbenannt.  Unter dieser Spalte wird den Benutzern der Wert **Yes** (Ja) oder **No** (Nein) angezeigt, um anzugeben, dass eine App entweder erforderlich oder von ihrer Organisation als optional angesehen wird. Diese Änderungen wurden durchgeführt, da Gerätebenutzer über das Konzept der verfügbaren Apps irritiert waren. Ihre Benutzer können weitere Informationen zum Installieren von Apps im Unternehmensportal unter [Installieren und Freigeben von Apps auf Ihrem Gerät](../user-help/install-apps-cpapp-windows.md) finden. Weitere Informationen zum Konfigurieren der Unternehmensportal-App für Ihre Benutzer finden Sie unter [Konfigurieren der Microsoft Intune-Unternehmensportal-App](../apps/company-portal-app.md).  

<!-- ########################## -->
## <a name="week-of-november-4-2019"></a>Woche vom 4. November 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Gerätesicherheit

#### <a name="security-baselines-are-supported-on-microsoft-azure-government---4062552---"></a>Sicherheitsbaselines werden auf Microsoft Azure Government unterstützt.<!-- 4062552 -->

Intune-Instanzen, die auf *Microsoft Azure Government* gehostet werden, können nun [Sicherheitsbaselines](../protect/security-baselines.md) verwenden, mit denen Sie Ihre Benutzer und Geräte sichern und schützen können.

## <a name="whats-new-archive"></a>Archiv der Neuheiten
Die Neuigkeiten vorheriger Monate finden Sie im [Archiv für Neuheiten](whats-new-archive.md).

## <a name="notices"></a>Benachrichtigungen

[!INCLUDE [Intune notices](../includes/intune-notices.md)]


