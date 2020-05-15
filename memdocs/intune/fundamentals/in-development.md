---
title: 'In der Entwicklung: Microsoft Intune'
titleSuffix: ''
description: In der Entwicklung befindliche Microsoft Intune-Features
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/28/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7827c85585d630f64ba9c6d342b6275fca506b1d
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906975"
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

### <a name="support-for-multiple-accounts-in-company-portal-for-mac---5779449----"></a>Unterstützung für mehrere Konten im Unternehmensportal für Mac<!-- 5779449  -->
Das Unternehmensportal auf macOS-Geräten speichert Benutzerkonten jetzt zwischen, wodurch die Anmeldung vereinfacht wird. Benutzer müssen sich nicht länger bei jedem Start der Anwendung beim Unternehmensportal anmelden. Darüber hinaus zeigt das Unternehmensportal eine Kontoauswahl an, wenn mehrere Benutzerkonten zwischengespeichert wurden, sodass die Benutzer nicht ihren Benutzernamen eingeben müssen. 

### <a name="auto-update-vpp-available-apps---3640511----"></a>Automatische Aktualisierung verfügbarer VPP-Apps<!-- 3640511  -->
Als verfügbare VPP-Apps (Volume Purchase Program) veröffentlichte Apps werden automatisch aktualisiert, wenn die Option **Automatische App-Updates** für das VPP-Token aktiviert ist. Aktuell werden verfügbare VPP-Apps nicht automatisch aktualisiert. Stattdessen müssen Endbenutzer zum Unternehmensportal wechseln und die App neu installieren, wenn eine neue Version verfügbar ist. Für erforderliche Apps werden automatische Updates aktuell nicht unterstützt.

### <a name="customize-self-service-device-actions-in-the-company-portal--4393379----"></a>Anpassen von Self-Service-Geräteaktionen für Benutzer im Unternehmensportal<!--4393379  -->
Sie können die verfügbaren Self-Service-Geräteaktionen anpassen, die Endbenutzern in der Unternehmensportal-App und auf der Unternehmensportal-Website angezeigt werden. Um nicht beabsichtigte Geräteaktionen zu vermeiden, können Sie diese Einstellungen für die Unternehmensportal-App durch Auswahl von **Mandantenverwaltung** > **Anpassung** > **Erstellen** > **Features ausblenden** konfigurieren. Die folgenden Aktionen sind verfügbar:
- Schaltfläche **Entfernen** auf unternehmenseigenen Windows-Geräten ausblenden
- Schaltfläche **Zurücksetzen** auf unternehmenseigenen Windows-Geräten ausblenden
- Schaltfläche **Zurücksetzen** auf unternehmenseigenen iOS-Geräten ausblenden
- Schaltfläche **Entfernen** auf unternehmenseigenen iOS-Geräten ausblenden

Weitere Informationen erhalten Sie unter [Self-Service-Geräteaktionen für Benutzer im Unternehmensportal](../apps/company-portal-app.md#user-self-service-device-actions-from-the-company-portal).

### <a name="unified-delivery-of-azure-ad-enterprise-or-office-online-applications-in-the-company-portal--4404429---"></a>Einheitliche Bereitstellung von Azure AD-Enterprise- oder Office Online-Anwendungen im Unternehmensportal<!--4404429 -->
Sie können die Anzeige von Azure AD-Enterprise- oder Office Online-Anwendungen im Unternehmensportal umschalten (**Ausblenden** oder **Anzeigen**). Jeder Benutzer sieht den gesamten Anwendungskatalog für den ausgewählten Microsoft-Dienst. Standardmäßig wird jede zusätzliche App auf **Ausblenden** festgelegt. Dieses Feature wird in der Unternehmensportal-Website im 2005-Release wirksam. Eine Unterstützung in den Windows-, iOS/iPadOS- und macOS-Unternehmensportalen soll in Kürze folgen. Diese künftige Einstellung finden Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) unter **Mandantenverwaltung** > **Anpassung**. Weitere Informationen finden Sie unter [Anpassen von Intune-Unternehmensportal-Apps, der Unternehmensportal-Website und der Intune-App](../apps/company-portal-app.md).

### <a name="search-the-intune-docs-from-the-company-portal---1736480---"></a>Suche in der Intune-Dokumentation aus dem Unternehmensportal<!-- 1736480 -->
Sie können ab sofort direkt aus der Unternehmensportal für macOS-App in der Intune-Dokumentation suchen. Wählen Sie in der Menüleiste **Hilfe** > **Suche** aus, und geben Sie die Schlüsselwörter für Ihre Suche ein, um schnell Antworten auf Ihre Fragen zu finden.

### <a name="company-portal-for-android-will-guide-users-to-get-apps-after-work-profile-enrollment----6103999----"></a>Benutzeranleitung zum Abrufen von Apps im Unternehmensportal für Android nach der Arbeitsprofilregistrierung <!-- 6103999  -->
Wir verbessern die In-App-Anleitungen im Unternehmensportal, um Benutzern das Auffinden und Installieren von Apps zu erleichtern.  Nach der Registrierung in der Arbeitsprofilverwaltung werden Benutzer in einer Meldung darauf hingewiesen, dass sie vorgeschlagene Apps in der Google Play-Version mit Badge finden. Benutzern wird außerdem im Unternehmensportal-Drawer auf der linken Seite ein Link **Apps abrufen** angezeigt. Um Platz für diese neuen und verbesserten Benutzerfunktionen zu schaffen, wird die Registerkarte **APPS** entfernt. 

### <a name="android-company-portal-user-experience---5736084---"></a>Benutzeroberfläche des Android-Unternehmensportals<!-- 5736084 -->
In der 2005-Version des Android-Unternehmensportals wird Endbenutzern von Android-Geräten, die eine Warnungs-, Blockierungs- oder Zurücksetzungsmeldung über eine App-Schutzrichtlinie erhalten, eine neue Benutzeroberfläche angezeigt. Anstelle der aktuellen Dialogbenutzeroberfläche wird den Endbenutzern eine ganzseitige Meldung angezeigt, in der die Ursachen für die Warnung, Blockierung oder Zurücksetzung sowie die Schritte zur Problembeseitigung beschrieben werden. Weitere Informationen finden Sie unter [Benutzeroberfläche zum App-Schutz für Android-Geräte](../apps/app-protection-policy.md#app-protection-experience-for-android-devices) und [Einstellungen für App-Schutzrichtlinien in Microsoft Intune](../apps/app-protection-policy-settings-android.md).


<!-- ***********************************************-->
## <a name="device-configuration"></a>Gerätekonfiguration

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

### <a name="configure-system-extensions-on-macos-devices---6255624----"></a>Konfigurieren von Systemerweiterungen auf macOS-Geräten<!-- 6255624  -->
Auf macOS-Geräten können Sie ein Kernelerweiterungsprofil erstellen, um Einstellungen auf Kernelebene zu konfigurieren (**Geräte** > **Konfigurationsprofile** > **macOS** für die Plattform > **Kernelerweiterungen** für das Profil). Apple wird Kernelerweiterungen als veraltet einstufen und in einer zukünftigen Version durch Systemerweiterungen ersetzen. Systemerweiterungen werden im Benutzerbereich ausgeführt und ermöglichen keinen Zugriff auf den Kernel. Das Ziel besteht darin, die Sicherheit zu erhöhen und dem Benutzer mehr Kontrolle zu ermöglichen, während gleichzeitig die Angriffe auf Kernelebene begrenzt werden. Sowohl Kernel- als auch Systemerweiterungen ermöglichen den Benutzern das Installieren von App-Erweiterungen, die die nativen Funktionen des Betriebssystems erweitern.

In Intune können Sie sowohl Kernelerweiterungen als auch Systemerweiterungen konfigurieren (**Geräte** > **Konfigurationsprofile** > **macOS** für die Plattform > **Kernelerweiterungen** für das Profil). Kernelerweiterungen gelten für Version 10.13.2 und höher. Systemerweiterungen gelten für Version 10.15 und höher. Für macOS 10.15 bis macOS 10.15.4 können Kernelerweiterungen und Systemerweiterungen parallel ausgeführt werden. 

Weitere Informationen zu Kernelerweiterungen auf macOS-Geräten finden Sie unter [Hinzufügen von macOS-Kernelerweiterungen](../configuration/kernel-extensions-overview-macos.md).

Gilt für:
- macOS 10.15 und neuer

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Geräteregistrierung

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>BYOD-Geräte können VPN für die Bereitstellung verwenden<!--5015344 -->
Dieses Feature ist möglicherweise verzögert.

### <a name="automated-device-sync-interval-down-to-12-hours--3077535---"></a>Herabsetzung es Intervalls für die Gerätesynchronisierung auf 12 Stunden<!--3077535 -->
Für die automatische Geräteregistrierung von Apple wird das Intervall für die automatische Gerätesynchronisierung zwischen Intune und Apple Business Manager von 24 Stunden auf 12 Stunden abgesenkt. Weitere Informationen zur Synchronisierung finden Sie unter [Synchronisieren verwalteter Geräte](../enrollment/device-enrollment-program-enroll-ios.md#sync-managed-devices).

### <a name="autopilot-support-for-hololens-2-devices--6305220--"></a>Autopilot-Unterstützung für Hololens 2-Geräte<!--6305220-->
Windows Autopilot unterstützt Hololens 2-Geräte. Weitere Informationen zur Verwendung von Autopilot finden Sie unter [Registrieren von Windows-Geräten in Intune mithilfe von Windows Autopilot](../enrollment/enrollment-autopilot.md).

### <a name="enrollment-restrictions-will-support-scope-tags--4209550---"></a>Registrierungsbeschränkungen unterstützen Bereichstags<!--4209550 -->
Sie können Registrierungsbeschränkungen Bereichstags hinzufügen. Wechseln Sie hierzu im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) zu  > **Geräte** > **Registrierungsbeschränkungen** > **Einschränkung erstellen**. Wenn Sie eine Beschränkung des gewünschten Typs erstellen, wird die Seite **Bereichstags** angezeigt.

### <a name="shared-ipads-for-business--6367326---"></a>Gemeinsam genutzte iPads für Unternehmen<!--6367326 -->
Sie können mit Intune und Apple Business Manager problemlos und sicher gemeinsam genutzte iPads einrichten, sodass Geräte durch mehrere Mitarbeiter verwendet werden können. Das Apple-Feature [Gemeinsam genutztes iPad](https://developer.apple.com/education/shared-ipad/) bietet eine personalisierte Benutzeroberfläche für mehrere Benutzer, während Benutzerdaten beibehalten werden. Durch Verwendung einer verwalteten Apple-ID können Benutzer auf ihre Apps, Daten und Einstellungen zugreifen, nachdem sie sich in ihrer Organisation an einem gemeinsam genutzten iPad angemeldet haben. Gemeinsam genutzte iPads arbeiten mit Verbundidentitäten.

Wechseln Sie zur Anzeige dieses Features zu [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Geräte** > **iOS** > **iOS-Registrierung** > **Registrierungsprogrammtoken**, wählen Sie ein Token aus, und klicken Sie dann auf **Profile** > **Profil erstellen** > **iOS**. Wählen Sie auf der Seite **Verwaltungseinstellungen** die Option **Ohne Benutzeraffinität registrieren** aus. Daraufhin wird die Option **Gemeinsam genutztes iPad** angezeigt.

**Gilt für:** iPadOS 13.4 und höher. In diesem Release wird Unterstützung für temporäre Sitzungen mit gemeinsam genutzten iPads hinzugefügt, sodass Benutzer ohne eine verwaltete Apple-ID auf ein Gerät zugreifen können. Nach der Abmeldung werden alle Benutzerdaten vom Gerät gelöscht, sodass das Gerät sofort wieder zur Verwendung bereitsteht, ohne dass eine Gerätezurücksetzung durchgeführt werden muss. 

<!-- ***********************************************-->
## <a name="device-management"></a>Geräteverwaltung

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Unterstützung von PowerShell-Skripts für BYOD-Geräte<!-- 1862833  -->
PowerShell-Skripts unterstützen bei Azure AD registrierte Geräte in Intune. Weitere Informationen zu PowerShell finden Sie unter [Verwenden von PowerShell-Skripts auf Windows 10-Geräten in Intune](../apps/intune-management-extension.md). Diese Funktion unterstützt keine Geräte, auf denen die Windows 10 Home-Edition ausgeführt wird.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics enthält das Gerätedetailprotokoll<!--6014987  -->
Intune-Gerätedetailprotokolle werden unter **Berichte** > **Log Analytics** bereitgestellt. Sie können Gerätedetails korrelieren, um benutzerdefinierte Abfragen und Azure-Workbooks zu erstellen.


### <a name="macos-script-support---6376978----"></a>macOS-Skriptunterstützung<!-- 6376978  -->
Die Skriptunterstützung für macOS ist jetzt allgemein verfügbar. Darüber hinaus wird Unterstützung für benutzerseitig zugewiesene Skripts und für macOS-Geräte hinzugefügt, die über die automatische Geräteregistrierung von Apple (vormals Programm zur Geräteregistrierung) registriert wurden. Weitere Informationen finden Sie unter [Verwenden von Shellskripts auf macOS-Geräten in Intune](../apps/macos-shell-scripts.md).

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
## <a name="security"></a>Sicherheit

### <a name="derived-credentials-support-for-disa-purebred-on-android-devices--4839592---"></a>Unterstützung abgeleiteter Anmeldeinformationen für DISA Purebred auf Android-Geräten<!--4839592 -->
Sie können *DISA Purebred* als Anbieter für [abgeleitete Anmeldeinformationen](../protect/derived-credentials.md) auf vollständig verwalteten Android Enterprise-Geräten (**Mandantenverwaltung** > **Connectors und Token** > **Abgeleitete Anmeldeinformationen**) verwenden. Unterstützung wird beim Abrufen abgeleiteter Anmeldeinformationen für DISA Purebred einbezogen. Sie können abgeleitete Anmeldeinformationen für die App-Authentifizierung, für WLAN, VPNs oder S/MIME-Signaturen und/oder -Verschlüsselung für Apps verwenden, die dies unterstützen. 

Im April hat Intune die Unterstützung für *Entrust Datacard* und *Intercede* als Anbieter für abgeleitete Anmeldeinformationen hinzugefügt. 

### <a name="privacy-preferences-settings-for-macos-devices---2934232---"></a>Privatsphäreneinstellungen für macOS-Geräte<!-- 2934232 --> 
Apple hat im Rahmen der Veröffentlichung von macOS Catalina 10.15 die Sicherheits- und Privatsphäreneinstellungen erweitert. Standardmäßig können Anwendungen und Prozesse ohne Zustimmung des Benutzers nicht auf bestimmte Daten zugreifen. Wenn Benutzer keine Zustimmung geben, funktionieren die Anwendungen und Prozesse möglicherweise nicht mehr. Intune fügt Unterstützung für Einstellungen hinzu, mit denen IT-Administratoren den Zugriff auf Daten im Namen von Endbenutzern auf Geräten, auf denen macOS 10.14 oder höher ausgeführt wird, zulassen oder nicht zulassen können. Mit diesen Einstellungen wird sichergestellt, dass Anwendungen und Prozesse weiterhin ordnungsgemäß funktionieren und die Anzahl der Eingabeaufforderungen verringert, die Endbenutzern zur Verfügung stehen.


### <a name="duplicate-your-policies-in-endpoint-security---5892558-----"></a>Duplizieren von Richtlinien in „Endpunktsicherheit“<!-- 5892558   -->
Sie können im Microsoft Endpoint Manager Admin Center eine erstellte Richtlinie im Knoten „Endpunktsicherheit“ auswählen und duplizieren, um eine Kopie zu erstellen.  Sie können Richtlinien duplizieren, die Sie für die folgenden Bereiche erstellt haben: 

- Antivirus
- Datenträgerverschlüsselung
- Firewall
- Endpunkterkennung und -antwort
- Verringerung der Angriffsfläche
- Kontoschutz

Beim Duplizieren einer Richtlinie wird eine Kopie der ursprünglichen Richtlinie erstellt, die Sie anschließend umbenennen und bearbeiten können. Die Kopie enthält keine Zuweisungen aus der Originalrichtlinie.

### <a name="send-push-notifications-as-an-action-for-non-compliance----1733150-----"></a>Senden von Pushbenachrichtigungen als Aktion bei Nichtkonformität <!-- 1733150   -->
Auf iOS- und Android-Plattformen wird eine neue Aktion für Nichtkonformität hinzugefügt, mit der eine App-Pushbenachrichtigung über die Unternehmensportal-App gesendet wird. Benutzer können auf die Benachrichtigung klicken, wodurch die Unternehmensportal-App gestartet wird, die dann den Grund für die Nichtkonformität anzeigt. Administratoren können diese neue Aktion für Nichtkonformität dann im Microsoft Endpoint Manager Admin Center konfigurieren, indem sie zu **Geräte** > **Konformitätsrichtlinien** > **Richtlinie erstellen** navigieren und die *Aktion* zum Senden einer App-Pushbenachrichtigung auswählen. 

### <a name="new-profile-for-endpoint-security-firewall-policy---5653324-----"></a>Neues Profil für Firewallrichtlinie in Endpunktsicherheit<!-- 5653324   -->
Als Vorschau fügen wir der Firewallrichtlinie in der Endpunktsicherheit von Intune ein zusätzliches Profil für Windows 10 und höher hinzu (**Endpunktsicherheit** > **Firewall** > **Richtlinie erstellen** > **Windows 10 und höher**). 

Jede Instanz dieses neuen Profils unterstützt bis zu 150 benutzerdefinierte *Microsoft Defender-Firewallregeln*. Das Profil für Microsoft Defender-Firewallregeln ermöglicht es Ihnen, fein abgestimmte Windows-Firewallregeln zu definieren, um Ports und Anwendungen in Windows 10 zu blockieren oder zuzulassen.

<!-- ***********************************************-->
## <a name="notices"></a>Benachrichtigungen

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Weitere Informationen:

Details zu aktuellen Entwicklungen finden Sie unter [Neuerungen in Microsoft Intune](whats-new.md).



