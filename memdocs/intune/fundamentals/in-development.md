---
title: 'In der Entwicklung: Microsoft Intune'
titleSuffix: ''
description: In der Entwicklung befindliche Microsoft Intune-Features
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f2bb971da483cd86e143673b57e8e5e09f943a5
ms.sourcegitcommit: 9a700a72735f9a316bdb51c44f86f9cc3bfb7be2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/21/2020
ms.locfileid: "83764202"
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

### <a name="company-portal-for-android-will-guide-users-to-get-apps-after-work-profile-enrollment----6103999----"></a>Benutzeranleitung zum Abrufen von Apps im Unternehmensportal für Android nach der Arbeitsprofilregistrierung <!-- 6103999  -->
Wir verbessern die In-App-Anleitungen im Unternehmensportal, um Benutzern das Auffinden und Installieren von Apps zu erleichtern.  Nach der Registrierung in der Arbeitsprofilverwaltung werden Benutzer in einer Meldung darauf hingewiesen, dass sie vorgeschlagene Apps in der Google Play-Version mit Badge finden. Benutzern wird außerdem im Unternehmensportal-Drawer auf der linken Seite ein Link **Apps abrufen** angezeigt. Um Platz für diese neuen und verbesserten Benutzerfunktionen zu schaffen, wird die Registerkarte **APPS** entfernt. 

<!-- ***********************************************-->
## <a name="device-configuration"></a>Gerätekonfiguration

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>Einstellungen und Werte für das Gerätekonfigurationsprofil werden für Windows-Plattformen aktualisiert<!-- 4091122 -->
Beim Erstellen von Gerätekonfigurationsprofilen für Windows-Plattformen (**Geräte** > **Konfigurationsprofile** >  **Profil erstellen** > beliebige **Windows**-Option für Plattform) unterscheiden sich einige Einstellungen und deren Werte vom CSP, was verwirrend sein kann. Die Einstellungsnamen und ihre Werte werden aktualisiert, sodass sie eindeutig zu verstehen sind.

Gilt für:

- Gerätekonfigurationsprofile für Windows 10 oder höher
- Gerätekonfigurationsprofile für Windows Holographic for Business
- Gerätekonfigurationsprofile für Windows 8.1
- Gerätekonfigurationsprofile für Windows Phone 8.1

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>Neue FileVault-Einstellung für macOS-Endpoint Protection-Gerätekonfigurationsrichtlinie<!-- 5459801   -->
Wir fügen der FileVault-Kategorie innerhalb der [macOS-Endpoint Protection](../protect/endpoint-protection-macos.md)-Vorlage eine neue Einstellung hinzu: „Wiederherstellungsschlüssel ausblenden“ (**Geräte** > **Konfigurationsprofile** > **Profil erstellen**, wählen Sie **macOS** für *Plattform* und dann **Endpoint Protection** für *Profiltyp* aus). Mit dieser Einstellung wird der persönliche Schlüssel während der FileVault 2-Verschlüsselung für den Endbenutzer ausgeblendet. Ein Gerätebenutzer kann den persönlichen Wiederherstellungsschlüssel jederzeit über die iOS-Unternehmensportal-App oder über die Website des Unternehmensportals für das verschlüsselte macOS-Gerät anzeigen. Navigieren Sie einfach zu „Gerätedetails“, und klicken Sie auf *Wiederherstellungsschlüssel abrufen*, um den persönlichen Wiederherstellungsschlüssel anzuzeigen.

Diese Einstellung ist in der zuvor erstellten Richtlinie nicht verfügbar. Sie müssen die FileVault-Richtlinien neu erstellen, um diese Einstellung für die Verwendung zu konfigurieren. 


<!-- ***********************************************-->
## <a name="device-enrollment"></a>Geräteregistrierung

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>BYOD-Geräte können VPN für die Bereitstellung verwenden<!--5015344 -->
Dieses Feature ist möglicherweise verzögert.

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


### <a name="duplicate-your-policies-in-endpoint-security---5892558-----"></a>Duplizieren von Richtlinien in „Endpunktsicherheit“<!-- 5892558   -->
Sie können im Microsoft Endpoint Manager Admin Center eine erstellte Richtlinie im Knoten „Endpunktsicherheit“ auswählen und duplizieren, um eine Kopie zu erstellen.  Sie können Richtlinien duplizieren, die Sie für die folgenden Bereiche erstellt haben: 

- Antivirus
- Datenträgerverschlüsselung
- Firewall
- Endpunkterkennung und -antwort
- Verringerung der Angriffsfläche
- Kontoschutz

Beim Duplizieren einer Richtlinie wird eine Kopie der ursprünglichen Richtlinie erstellt, die Sie anschließend umbenennen und bearbeiten können. Die Kopie enthält keine Zuweisungen aus der Originalrichtlinie.

### <a name="new-profile-for-endpoint-security-firewall-policy---5653324-----"></a>Neues Profil für Firewallrichtlinie in Endpunktsicherheit<!-- 5653324   -->
Als Vorschau fügen wir der Firewallrichtlinie in der Endpunktsicherheit von Intune ein zusätzliches Profil für Windows 10 und höher hinzu (**Endpunktsicherheit** > **Firewall** > **Richtlinie erstellen** > **Windows 10 und höher**). 

Jede Instanz dieses neuen Profils unterstützt bis zu 150 benutzerdefinierte *Microsoft Defender-Firewallregeln*. Das Profil für Microsoft Defender-Firewallregeln ermöglicht es Ihnen, fein abgestimmte Windows-Firewallregeln zu definieren, um Ports und Anwendungen in Windows 10 zu blockieren oder zuzulassen.

<!-- ***********************************************-->
## <a name="notices"></a>Benachrichtigungen

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Weitere Informationen:

Details zu aktuellen Entwicklungen finden Sie unter [Neuerungen in Microsoft Intune](whats-new.md).



