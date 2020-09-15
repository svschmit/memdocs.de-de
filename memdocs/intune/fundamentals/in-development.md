---
title: 'In der Entwicklung: Microsoft Intune'
titleSuffix: ''
description: In der Entwicklung befindliche Microsoft Intune-Features
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/28/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: f9ec657e7d2ee83f3f4f54f9a33a5a350faa4229
ms.sourcegitcommit: 7f71d6f776df3ac28e5da3f8c926c88626483ce9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89564243"
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


<!-- ***********************************************-->
## <a name="device-configuration"></a>Gerätekonfiguration

### <a name="create-pkcs-certificate-profiles-for-android-enterprise-fully-managed-devices-cobo---4839686---"></a>Erstellen von PKCS-Zertifikatprofilen für vollständig verwaltete Android Enterprise-Geräte (COBO)<!-- 4839686 -->
Sie können PKCS-Zertifikatprofile erstellen, um Zertifikate für den Besitzer des Android Enterprise-Geräts und für Arbeitsprofilgeräte bereitzustellen (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **Android Enterprise > Nur Gerätebesitzer** oder **Android Enterprise > Nur Arbeitsprofil** als Plattform > **PKCS** als Profil).

Bald können Sie PKCS-Zertifikatprofile für vollständig verwaltete Android Enterprise-Geräte erstellen. Der Intune-PFX-Zertifikatconnector ist erforderlich. Wenn Sie nicht SCEP verwenden, sondern nur PKCS, können Sie den NDES-Connector entfernen, nachdem Sie den neuen PFX-Connector installiert haben. Der neue PFX-Connector importiert PFX-Dateien und stellt PKCS-Zertifikate auf allen Plattformen bereit.

Weitere Informationen zu PKCS-Zertifikaten finden Sie unter [Konfigurieren und Verwenden von PKCS-Zertifikaten mit Intune](../protect/certficates-pfx-configure.md).

Gilt für:
- Vollständig verwaltetes Android Enterprise (COBO)

### <a name="support-for-certificates-with-a-key-size-of-4096-on-ios-and-macos-devices---7659175-----"></a>Unterstützung für Zertifikate mit einer Schlüsselgröße von 4096 Bit auf iOS- und macOS-Geräten<!-- 7659175   -->
Intune wird in Kürze die Verwendung einer Schlüsselgröße von 4096 Bit für SCEP-Zertifikatprofile unterstützen. (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > *Plattform auswählen* > *Profil* = **SCEP-Zertifikat**)

Die Unterstützung von Schlüsseln mit einer Größe von 4096 Bit wird für folgende Plattformen verfügbar sein: 
- iOS 14 und höher
- macOS 11 und höher    

### <a name="new-setting-for-password-complexity-for-android-10-and-later---7992114----"></a>Neue Einstellung für die Kennwortkomplexität für Android 10 und höher<!-- 7992114  -->
Zur Unterstützung neuer Optionen für Android 10 und höher wird es eine neue Einstellung mit der Bezeichnung **Kennwortkomplexität** für die beiden Richtlinien *Gerätekonformität* und *Geräteeinschränkungen* geben. (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **Geräteeinschränkungen** und **Geräte** > **Konformitätsrichtlinien** > **Richtlinie erstellen**) Mit dieser Einstellung können Sie ein Maß für die Kennwortsicherheit verwalten, bei dem Typ, Länge und Qualität des Kennworts berücksichtigt wird. 

Dabei werden die folgenden Komplexitätsstufen unterstützt:
- **Kein**: Kein Kennwort
- **Gering**: Das Kennwort erfüllt eine der folgenden Voraussetzungen:
  - Muster
  - PIN mit sich wiederholenden (4444) oder geordneten (1234, 4321, 2468) Sequenzen
- **Mittel**: Das Kennwort erfüllt eine der folgenden Voraussetzungen:
  - PIN ohne sich wiederholende (4444) oder geordnete (1234, 4321, 2468) Sequenzen, Länge: mindestens 4
  - Alphabetisch, Länge: mindestens 4
  - Alphanumerisch, Länge: mindestens 4
- **Hoch**: Das Kennwort erfüllt eine der folgenden Voraussetzungen:
  - PIN ohne sich wiederholende (4444) oder geordnete (1234, 4321, 2468) Sequenzen, Länge: mindestens 8
  - Alphabetisch, Länge: mindestens 6
  - Alphanumerisch, Länge: mindestens 6

Die Kennwortkomplexität gilt nicht für Samsung Knox-Geräte, auf denen Android 10 und höher ausgeführt wird. Auf diesen Geräten wird die Kennwortkomplexität durch die Einstellungen „Kennwortlänge“ und/oder „Kennworttyp“ überschrieben.

### <a name="cope-preview-update-new-settings-to-create-requirements-for-the-work-profile-password-for-android-enterprise-corporate-owned-devices-with-a-work-profile--7088355---"></a>Aktualisierung der Vorschauversion von COPE: Neue Einstellungen zum Erstellen von Anforderungen für das Arbeitsprofilkennwort für unternehmenseigene Android Enterprise-Geräte mit einem Arbeitsprofil<!--7088355 -->
Zukünftige Einstellungen ermöglichen es Administratoren, Anforderungen für das Arbeitsprofilkennwort für unternehmenseigene Android Enterprise-Geräte mit einem Arbeitsprofil festzulegen.  (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **Android Enterprise** als Plattform > **Vollständig verwaltetes, dediziertes und unternehmenseigenes Arbeitsprofil** > **Geräteeinschränkungen** für Profil > **Arbeitsprofilkennwort**):

- Erforderlicher Kennworttyp
- Minimale Kennwortlänge
- Anzahl von Tagen bis zum Kennwortablauf
- Anzahl erforderlicher Kennwörter, bevor ein Benutzer ein Kennwort wiederverwenden kann
- Anzahl von fehlgeschlagenen Anmeldungen, bevor das Gerät zurückgesetzt wird


### <a name="new-settings-using-per-app-vpn-or-on-demand-vpn-on-iosipados-and-macos-devices---7758772-7758837-7758886----"></a>Neue Einstellungen, für die ein Pro-App-VPN oder ein bedarfsgesteuertes VPN auf iOS/iPadOS- und macOS-Geräten verwendet wird<!-- 7758772 7758837 7758886  -->
- **Deaktivierung des automatischen VPN durch Benutzer verhindern**: Beim Erstellen einer automatischen **Pro-App-VPN**- **bedarfsgesteuerten VPN**-Verbindung können Sie erzwingen, dass das automatische VPN aktiviert bleibt und ausgeführt wird.
- **Zugeordnete Domänen**: Beim Erstellen einer automatischen **Pro-App-VPN**-Verbindung können Sie zugeordnete Domänen im VPN-Profil angeben, mit denen die VPN-Verbindung automatisch gestartet wird. 
- **Ausgeschlossene Domänen**: Beim Erstellen einer automatischen **Pro-App-VPN**-Verbindung können Sie eine Liste mit Domänen erstellen, mit denen die VPN-Verbindung umgangen wird, wenn das Pro-App-VPN verbunden wird.

Unter **Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **iOS/iPadOS** oder **macOS** als Plattform > **VPN** als Profil > **Automatisches VPN** können Sie Profile für das automatische VPN konfigurieren.

Weitere Informationen zu zugeordneten Domänen finden Sie unter [Zugeordnete Domänen](../configuration/device-features-configure.md#associated-domains).

Informationen zu den Einstellungen, die Sie konfigurieren können, finden Sie unter [Einrichten eines Pro-App-VPN für iOS/iPadOS-Geräte](../configuration/vpn-setting-configure-per-app.md#create-a-per-app-vpn-profile).

Gilt für:
- iOS/iPadOS 14 und höher
- macOS Big Sur (macOS 11)

### <a name="cope-preview-update-new-settings-to-configure-the-personal-profile-for-android-enterprise-corporate-owned-devices-with-a-work-profile---7086356----"></a>Aktualisierung der Vorschauversion von COPE: Neue Einstellungen zum Konfigurieren des persönlichen Profils für unternehmenseigene Android Enterprise-Geräte mit einem Arbeitsprofil<!-- 7086356  -->
Für unternehmenseigene Android Enterprise-Geräte mit einem Arbeitsprofil gibt es neue Einstellungen, die konfiguriert werden können und nur für das persönliche Profil gelten (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **Android Enterprise** als Plattform > **Vollständig verwaltetes, dediziertes und unternehmenseigenes Arbeitsprofil** > **Geräteeinschränkungen** als Profil > **Persönliches Profil**):

- **Kamera:** Verwenden Sie diese Einstellung, um den Zugriff auf die Kamera während der persönlichen Nutzung zu blockieren.
- **Bildschirmaufnahme:** Verwenden Sie diese Einstellung, um Bildschirmaufnahmen während der persönlichen Nutzung zu blockieren.
- **Benutzern erlauben, die App-Installation über unbekannte Quellen im persönlichen Profil zu aktivieren**: Verwenden Sie diese Einstellung, um Benutzern die Installation von Apps über unbekannte Quellen im persönlichen Profil zu ermöglichen. 

Sie finden die aktuellen konfigurierbaren Einstellungen unter [Android Enterprise-Geräteeinstellungen zum Zulassen oder Einschränken von Features](../configuration/device-restrictions-android-for-work.md).

### <a name="block-app-clips-on-iosipados-and-defer-non-os-software-updates-on-macos-devices---7518422----"></a>Blockieren von App-Clips unter iOS/iPadOS und Zurückstellen von Nicht-BS-Softwareupdates auf macOS-Geräten<!-- 7518422  -->
Zum Erstellen eines Profils für Geräteeinschränkungen auf iOS/iPadOS- und macOS-Geräten gibt es neue Einstellungen:

**iOS/iPadOS 14.0 und höher: Blockieren von App-Clips**
- Gilt für iOS/iPadOS 14.0 und höher.
- Geräte müssen mit der Geräteregistrierung oder der automatischen Geräteregistrierung (überwachte Geräte) registriert werden.
- Mit der Einstellung **App-Clips blockieren** werden App-Clips auf verwalteten Geräten blockiert (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **iOS/iPadOS** als Plattform > **Geräteeinschränkungen** als Profil > **Allgemein**). Wenn App-Clips blockiert werden, können Benutzer keine App-Clips hinzufügen und auf dem Gerät vorhandene App-Clips werden entfernt.  

**macOS 11 und höher: Zurückstellen von Softwareupdates**
- Gilt für macOS 11 und höher. Bei überwachten macOS-Geräten muss das Gerät über eine vom Benutzer genehmigte Geräteregistrierung verfügen oder über die automatische Geräteregistrierung registriert worden sein.
- Mit der Einstellung **Softwareupdates zurückstellen** wird die Sichtbarkeit von Nicht-BS-Softwareupdates für Benutzer verzögert (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **macOS** als Plattform > **Geräteeinschränkungen** als Profil > **Allgemein**). Wenn Sie diese Updates zurückstellen, werden neu veröffentlichte Updates erst nach dem mit der Einstellung **Sichtbarkeit von Softwareupdates verzögern** konfigurierten Zurückstellungszeitraum für Benutzer sichtbar. Die Zurückstellung von Nicht-BS-Softwareupdates hat keine Auswirkungen auf geplante Updates.
- Die vorhandene Einstellung **Softwareupdates zurückstellen** lässt sich mit dieser neuen Einstellung kombinieren. Mit der neuen Einstellung können Sie BS-Softwareupdates und Nicht-BS-Softwareupdates zurückstellen. Die Einstellung **Sichtbarkeit von Softwareupdates verzögern** wird weiterhin verwendet, um die Anzahl der Tage festzulegen, die für beide Einstellungen zum Zurückstellen von Softwareupdates gilt.
- Das Verhalten von vorhandenen Richtlinien wird nicht verändert, beeinträchtigt oder gelöscht. Vorhandene Richtlinien werden automatisch zur neuen Einstellung mit der gleichen Konfiguration migriert.

### <a name="disable-mac-address-randomization-on-wi-fi-networks-on-iosipados-devices---7758689----"></a>Deaktivieren der Randomisierung von MAC-Adressen in WLAN-Netzwerken auf iOS/iPadOS-Geräten<!-- 7758689  -->
Ab iOS/iPadOS 14 wird auf Geräten beim Herstellen einer Verbindung mit einem Netzwerk anstelle der physischen MAC-Adresse standardmäßig eine randomisierte MAC-Adresse angezeigt. Dieses Verhalten wird aus Gründen des Datenschutzes empfohlen, da es schwieriger ist, ein Gerät anhand der MAC-Adresse zu verfolgen. Mit diesem Feature werden auch Funktionen wie etwa die Netzwerkzugriffssteuerung (Network Access Control, NAC) eingestellt, die auf einer statischen MAC-Adresse beruhen. 

Die Randomisierung von MAC-Adressen kann in WLAN-Profilen für jedes einzelne Netzwerk deaktiviert werden (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **iOS/iPadOS** als Plattform > **WLAN** als Profil > **Grundlegend** oder **Unternehmen** als WLAN-Typ).

Informationen dazu, welche Einstellungen Sie derzeit konfigurieren können, finden Sie unter [Hinzufügen von WLAN-Einstellungen für iOS- und iPadOS-Geräte](../configuration/wi-fi-settings-ios.md).

Gilt für:
- iOS/iPadOS 14 und höher

### <a name="set-maximum-transmission-unit-for-ikev2-vpn-connections-on-iosipados-devices---7758937----"></a>Festlegen der maximalen Übertragungseinheit für IKEv2-VPN-Verbindungen auf iOS/iPadOS-Geräten<!-- 7758937  -->
Ab iOS/iPadOS 14 und bei neueren Geräten kann bei Verwendung von IKEv2-VPN-Verbindungen eine benutzerdefinierte maximale Übertragungseinheit (Maximum Transmission Unit, MTU) konfiguriert werden (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **iOS/iPadOS** als Plattform > **VPN** als Profil -> IKEv2 als Verbindungstyp).

Weitere Informationen zu diesen Einstellungen finden Sie unter [IKEv2-Einstellungen](../configuration/vpn-settings-ios.md#ikev2-settings).

Gilt für:
- iOS/iPadOS 14 und höher

### <a name="per-account-vpn-connection-for-email-profiles-on-iosipados-devices---7759116----"></a>Kontobasierte VPN-Verbindung für E-Mail-Profile auf iOS/iPadOS-Geräten<!-- 7759116  -->
Ab iOS/iPadOS 14 kann der E-Mail-Datenverkehr für die native E-Mail-App über ein VPN geleitet werden, das auf dem vom Benutzer verwendeten Konto beruht. Ab dieser Version kann pro App ein VPN-Profil angegeben werden, das für diese kontobasierte VPN-Verbindung verwendet werden soll.  Die Pro-App-VPN-Verbindung wird automatisch aktiviert, wenn Benutzer ihr Organisationskonto in der E-Mail-App verwenden.

Informationen dazu, welche Einstellungen Sie derzeit konfigurieren können, finden Sie unter [Hinzufügen von E-Mail-Einstellungen für iOS- und iPadOS-Geräte](../configuration/email-settings-ios.md).

Gilt für:
- iOS/iPadOS 14 und höher

### <a name="use-netmotion-as-a-vpn-connection-type-for-android-enterprise-work-profile-devices---7764263---"></a>Verwenden von NetMotion als VPN-Verbindungstyp für Android Enterprise-Geräte mit Arbeitsprofil<!-- 7764263 -->
Beim Erstellen eines VPN-Profils ist NetMotion als VPN-Verbindungstyp verfügbar (**Geräte** > **Gerätekonfiguration** > **Profil erstellen** > **Android Enterprise-Arbeitsprofil** als Plattform > **VPN** als Profil > **NetMotion** als Verbindungstyp).

Weitere Informationen zu VPN-Profilen in Intune finden Sie unter[Erstellen von VPN-Profilen zum Herstellen einer Verbindung mit VPN-Servern](../configuration/vpn-settings-configure.md).

Gilt für:
- Android Enterprise-Arbeitsprofil

### <a name="changes-for-password-settings-in-device-restriction-profiles-for-android-device-administrator---7662279----"></a>Änderungen für Kennworteinstellungen in Geräteeinschränkungsprofilen für Android-Geräteadministrator<!-- 7662279  --> 
Mit dieser Version werden einige Änderungen an den Kennworteinstellungen für die Richtlinien *Geräteeinschränkungen* und *Konformität* für den *Android-Geräteadministrator* eingeführt. (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **Geräteeinschränkungen** und **Geräte** > **Konformitätsrichtlinien** > **Richtlinie erstellen**) Diese Änderungen helfen Intune, Änderungen bei Android Version 10 und höher zu berücksichtigen, um sicherzustellen, dass Einstellungen für Kennwörter weiterhin erwartungsgemäß für Geräte gelten.
 
Die Änderungen umfassen Folgendes:
- Entfernen der allgemeinen Option für **Kennwörter**.  
- Die Einstellungen werden in Abschnitte gegliedert, die darauf basieren, für welche Geräte sie gelten.
- Die Verwendung der Option **Minimale Kennwortlänge** ist deaktiviert, es sei denn, **Kennworttyp** wurde mit einem Wert konfiguriert, für den die Kennwortlänge gilt.
- Weitere Änderungen an Bezeichnungen und Beispieltexten.

Diese Änderungen gelten für die Benutzeroberfläche für Einstellungen und haben keine Auswirkungen auf vorhandene Profile. 

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Geräteregistrierung

### <a name="ending-support-for-ios-11--7327321---"></a>Beenden der Unterstützung für iOS 11<!--7327321 -->
Nach der Veröffentlichung von iOS 14 wird von der Intune-Registrierung und der Unternehmensportal-App iOS ab Version 12 unterstützt. Ältere Versionen werden nicht unterstützt, erhalten jedoch weiterhin Richtlinien.

### <a name="ending-support-for-macos-1012--7327326---"></a>Beenden der Unterstützung für macOS 10.12<!--7327326 -->
Nach der Veröffentlichung von macOS 11 wird von der Intune-Registrierung und dem Unternehmensportal macOS ab Version 10.13 unterstützt. Ältere Versionen werden nicht unterstützt.


<!-- ***********************************************-->
## <a name="device-management"></a>Geräteverwaltung

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Unterstützung von PowerShell-Skripts für BYOD-Geräte<!-- 1862833  -->
PowerShell-Skripts unterstützen bei Azure AD registrierte Geräte in Intune. Weitere Informationen zu PowerShell finden Sie unter [Verwenden von PowerShell-Skripts auf Windows 10-Geräten in Intune](../apps/intune-management-extension.md). Diese Funktion unterstützt keine Geräte, auf denen die Windows 10 Home-Edition ausgeführt wird.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics enthält das Gerätedetailprotokoll<!--6014987  -->
Intune-Gerätedetailprotokolle werden unter **Berichte** > **Log Analytics** bereitgestellt. Sie können Gerätedetails korrelieren, um benutzerdefinierte Abfragen und Azure-Workbooks zu erstellen.

### <a name="tenant-attach-run-scripts-from-the-admin-center--7220536-cm6234688---"></a>Mandantenanfügung: „Skripts ausführen“ über das Admin Center<!--7220536, CM6234688 -->
Bringen Sie das Leistungspotenzial des lokalen Configuration Manager-Features [Skripts ausführen](../../configmgr/apps/deploy-use/create-deploy-scripts.md) in das Microsoft Endpoint Manager Admin Center. Erlauben Sie zusätzlichen Rollen, z. B. dem Helpdesk, das Ausführen von PowerShell-Skripts aus der Cloud für ein einzelnes verwaltetes Configuration Manager-Gerät. Dies bietet alle herkömmlichen Vorteile von PowerShell-Skripts, die bereits vom Configuration Manager-Administrator definiert und für diese neue Umgebung genehmigt wurden. Weitere Informationen erhalten Sie unter [Technical Preview für Configuration Manager 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_scripts). 

### <a name="deploy-software-updates-to-macos-devices----3194876---"></a>Bereitstellen von Softwareupdates auf macOS-Geräten <!-- 3194876 -->
Sie können Softwareupdates für Gruppen von macOS-Geräten bereitstellen. Dieses Feature umfasst kritische, Firmware-, Konfigurationsdatei- und andere Updates. Sie können Updates beim nächsten Einchecken des Geräts senden oder einen Wochenplan auswählen, um Updates innerhalb oder außerhalb der von Ihnen festgelegten Zeitfenster bereitzustellen. Dies ist hilfreich, wenn Sie Geräte außerhalb der üblichen Geschäftszeiten aktualisieren möchten oder wenn Ihr Helpdesk voll besetzt ist. Außerdem erhalten Sie einen detaillierten Bericht zu allen macOS-Geräten mit bereitgestellten Updates. Sie können den Bericht geräteweise detailliert untersuchen, um die Status bestimmter Updates einzusehen.

### <a name="cope-preview-update-reset-work-profile-password-for-android-enterprise-corporate-owned-devices-with-a-work-profile---7217228---"></a>Aktualisierung der Vorschauversion von COPE: Zurücksetzen des Arbeitsprofilkennworts für unternehmenseigene Android Enterprise-Geräte mit einem Arbeitsprofil <!--7217228 -->
Mithilfe einer neuen Administratoraktion können Administratoren das Arbeitsprofilkennwort auf unternehmenseigenen Android Enterprise-Geräten mit einem Arbeitsprofil zurücksetzen.

### <a name="rename-a-co-managed-device-that-is-azure-active-directory-joined--7728043---"></a>Umbenennen eines gemeinsam verwalteten Geräts, das mit Azure Active Directory verknüpft ist<!--7728043 -->
Sie können ein gemeinsam verwaltetes Gerät, das mit Azure AD verknüpft ist, umbenennen. Wechseln Sie hierzu zu MEM > **Geräte** > **Alle Geräte**, und wählen Sie ein Gerät aus. Klicken Sie dann auf **...**  > **Gerät umbenennen**.

### <a name="support-for-powerprecision-and-powerprecision-batteries-for-zebra-devices--3724987---"></a>Unterstützung für PowerPrecision- und PowerPrecision+-Akkus für Zebra-Geräte<!--3724987 -->
Auf der Hardwaredetailsseite eines Geräts werden folgende Informationen zu Zebra-Geräten mit PowerPrecision- und PowerPrecision+-Akkus angezeigt:
- Zustandsbewertung laut Zebra (nur PowerPrecision+-Akkus)
- Anzahl der verbrauchten Vollladezyklen
- Datum des letzten Check-Ins für den zuletzt im Gerät befindlichen Akku
- Seriennummer des zuletzt im Gerät befindlichen Akkus

<!-- ***********************************************-->
## <a name="intune-apps"></a>Intune-Apps

### <a name="unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-windows-company-portal---1817861----"></a>Einheitliche Bereitstellung von Azure AD-Enterprise- und Office Online-Anwendungen im Windows-Unternehmensportal<!-- 1817861  -->
Bei Version 2006 haben wir eine [einheitliche Bereitstellung von Azure AD-Enterprise- und Office Online-Anwendungen im Unternehmensportal](../fundamentals/whats-new.md#unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-company-portal) angekündigt. Dieses Feature wird im Windows-Unternehmensportal unterstützt. Sie können im Bereich **Anpassung** von Intune **Azure AD-Unternehmensanwendungen** und **Office Online-Anwendungen** im Windows-Unternehmensportal **ausblenden** oder **anzeigen**. Jeder Endbenutzer sieht den gesamten Anwendungskatalog für den ausgewählten Microsoft-Dienst. Standardmäßig wird jede zusätzliche App auf **Ausblenden** festgelegt. Diese Konfigurationseinstellung finden Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) unter **Mandantenverwaltung** > **Anpassung**. Weitere Informationen finden Sie unter [Anpassen von Intune-Unternehmensportal-Apps, der Unternehmensportal-Website und der Intune-App](../apps/company-portal-app.md).
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>Überwachung und Problembehandlung

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Vorlage V2.0 für Power BI-Konformitätsbericht<!-- 636958  -->
Administratoren können die Vorlagenversion für den Power BI-Konformitätsbericht von Version V1.0 auf V2.0 aktualisieren. Version v2.0 umfasst ein verbessertes Design sowie Änderungen an Berechnungen und Daten, die als Bestandteil der Vorlage präsentiert werden. Weitere Informationen finden Sie unter [Verbinden mit dem Data Warehouse mit Power BI](../developer/reports-proc-get-a-link-powerbi.md).


### <a name="new-and-improved-microsoft-defender-antivirus-reporting-for-windows-10-and-newer---6018169----"></a>Neue und verbesserte Microsoft Defender Antivirus-Berichterstellung für Windows 10 und höher<!-- 6018169  -->
In der neuen Version gibt es für Windows 10 unter **Endpunktsicherheit** > **Antivirus** vier neue Microsoft Defender Antivirus-Berichte.
- Zwei Betriebsberichte: *Geräte mit erkannter Schadsoftware* und *Agent-Status*.
- Zwei Organisationsberichte *Erkannte Schadsoftware* und *Agent-Status*.

Im Betriebsbericht *Agent-Status* wird beispielsweise eine Übersicht über Gerätename, Benutzername, E-Mail-Adresse des Benutzers und Benutzerprinzipalname angezeigt. Zudem wird angegeben, ob der Echtzeitschutz und der Netzwerkschutz aktiviert sind. Wir werden weitere Einzelheiten mitteilen, sobald diese Berichte verfügbar sind.

Weitere Informationen zur Endpunktsicherheit in Intune finden Sie unter [Verwalten der Endpunktsicherheit in Microsoft Intune](../protect/endpoint-security.md).

### <a name="analyze-your-on-premises-gpos-using-group-policy-analytics-preview--7200950---"></a>Analysieren der lokalen GPOs mithilfe der Gruppenrichtlinienanalyse (Vorschau)<!--7200950 -->
In **Geräte** > **Gruppenrichtlinienanalyse (Vorschau)** können Sie Gruppenrichtlinienobjekte (Group Policy Objects, GPOs) in das Endpoint Manager Admin Center importieren. Beim Import wird das Gruppenrichtlinienobjekt automatisch von Intune analysiert. Zudem werden die Richtlinien mit entsprechenden Einstellungen in Intune angezeigt. Darüber hinaus werden auch Gruppenrichtlinienobjekte angezeigt, die veraltet sind oder nicht mehr unterstützt werden.

Gilt für:
- Windows 10 und höher

#### <a name="new-windows-10-feature-update-report---6473128----"></a>Neuer Bericht über Windows 10-Featureupdates<!-- 6473128  -->
Der Bericht **Windows-Featureupdates** enthält eine allgemeine Übersicht über die Konformität für Geräte, die Ziel einer **Windows 10-Featureupdates**-Richtlinie sind. Wählen Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) **Berichte** > **Windows-Updates (Vorschau)**  > **Fehler bei Featureupdate**, um die Zusammenfassung für diesen Bericht anzuzeigen. Wenn Sie Berichte für bestimmte Richtlinien anzeigen möchten, wählen Sie die Registerkarte **Berichte** aus, und öffnen Sie den **Bericht zu Windows-Featureupdates**. 

#### <a name="new-windows-10-feature-failures-update-report---6473121-----"></a>Neuer Bericht für Fehler bei Featureupdates unter Windows 10<!-- 6473121   -->
Der Bericht **Fehler bei Featureupdate** enthält Fehlerdetails für Geräte, die Ziel einer **Windows 10-Featureupdates**-Richtlinie sind und bei denen versucht wurde, ein Update durchzuführen. Wählen Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) **Geräte** > **Überwachen** > **Fehler bei Featureupdates** aus, um diesen Bericht anzuzeigen.

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

### <a name="improved-certificate-deployment-for-android-enterprise----6296499----"></a>Verbesserte Zertifikatbereitstellung für Android Enterprise <!-- 6296499  -->
Für Geräte, auf denen vollständig verwaltete, dedizierte und unternehmenseigene Android Enterprise-Arbeitsprofile ausgeführt werden, können in Kürze S/MIME-Zertifikate für Outlook verwendet werden, ohne dass ein Gerätebenutzer den Zugriff zulassen muss. S/MIME-Zertifikate werden mit einem importierten PKCS-Zertifikatprofil für die Gerätekonfiguration bereitgestellt. (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **Android Enterprise** > **Importiertes PKCS-Zertifikat** aus der Kategorie für *Vollständig verwaltetes, dediziertes und unternehmenseigenes Arbeitsprofil*).

### <a name="tri-state-options-for-settings-are-coming-to-endpoint-security-firewall-policy---6586159-----"></a>Firewallrichtlinie für Endpunktsicherheit bald mit Optionen für dritten Zustand für Einstellungen<!-- 6586159   -->
Für die Konfiguration von Einstellungen bei Firewallrichtlinien für die Endpunktsicherheit gibt es in der neuen Version einen dritten Zustand, mit dem die Plattform (Windows oder macOS) die zusätzliche Option (**Endpunktsicherheit** > **Firewall**) unterstützen kann.

Wenn eine Einstellung derzeit die Optionen **Nicht konfiguriert** und bei entsprechender Unterstützung durch die Plattform **Ja** bereitstellt, gibt es in der neuen Version nun auch die Option **Nein**.

### <a name="new-security-baseline-for-office---3150261----"></a>Neue Sicherheitsbaseline für Office<!-- 3150261  -->
Die neue Version enthält eine neue Sicherheitsbaseline (**Endpunktsicherheit** > **Sicherheitsbaselines**) zum Verwalten von Einstellungen für *Microsoft Office O365*. Die Einstellungen in der Baseline beinhalten Konfigurationen für Office-Apps wie *Add-On-Verwaltung*, *MIME-Verarbeitung* usw.

### <a name="improved-status-details-in-security-baseline-reports---7221051------"></a>Verbesserte Statusdetails in Sicherheitsbaselineberichten<!-- 7221051    -->
Wir verbessern die Statusdetails, die mit den Ergebnissen der bereitgestellten Sicherheitsbaselines angezeigt werden. (**Endpunktsicherheit** > **Sicherheitsbaselines** >  *Auswahl eines Sicherheitsbaselinetyps wie* **Windows 10-Sicherheitsbaselines** > **Profile** > *Auswahl einer Instanz dieses Profils zum Anzeigen des Status* > *Auswahl eines Profilberichts wie*  **Gerätestatus**)

Mit den Verbesserungen werden die für den Status verwendeten allgemeinen Bezeichnungen und Definitionen neu formuliert, um das Ziel des Status besser zu beschreiben. Beispiel:
- **Stimmt mit Baseline überein** heißt nun **Stimmt mit Standardeinstellungen überein**. Damit wird das Ziel besser beschrieben, bei dem es darum geht, zu erkennen, wenn eine Gerätekonfiguration mit der standardmäßigen (unveränderten) Baselinekonfiguration übereinstimmt.
- **Falsch konfiguriert** wird in spezifischere Details wie **Fehler**, **Konflikt** und **Ausstehend** gegliedert. Die neuen Status sorgen für Konsistenz mit anderen Bereichen der Konsole.

### <a name="expanded-rbac-permissions-for-the-endpoint-security-role--7312374--idstaged---"></a>Erweiterte RBAC-Berechtigungen für die Rolle „Endpunktsicherheit“<!--7312374  idstaged -->
Die Rolle **Endpunktsicherheits-Manager** für Intune erhält zusätzliche RBAC-Berechtigungen (Role-Based Access Control, rollenbasierte Zugriffssteuerung) für Remoteaufgaben. Mit dieser Rolle erhalten Sie Zugriff auf das Admin Center von Microsoft Endpoint Manager. Diese Rolle kann von Einzelbenutzern für die Verwaltung von Sicherheits- und Konformitätsfeatures verwendet werden (z. B. Sicherheitsbaselines, Gerätekonformität, bedingter Zugriff und Microsoft Defender Advanced Threat Protection).

Wechseln Sie zu **Mandantenadministrator** > **Intune-Rollen** > *wählen Sie eine Rolle aus* > **Berechtigungen**, um die Berechtigungen für eine Intune RBAC-Rolle anzuzeigen.

Erweiterte Berechtigungen für Remote Aufgaben umfassen Folgendes:

- Jetzt neu starten
- Remotesperre
- BitLockerKeys drehen (Vorschau)
- Rotate FileVault key (FileVault-Schlüssel rotieren)
- Geräte synchronisieren
- Microsoft Defender
- Configuration Manger-Aktion initiieren

### <a name="updates-for-security-baselines---7102146-7103916----"></a>Updates für Sicherheitsbaselines<!-- 7102146, 7103916  -->
Wir werden in Kürze Updates für die folgenden Sicherheitsbaselines (**Endpunktsicherheit** > **Sicherheitsbaselines**) veröffentlichen:
- **MDM-Sicherheitsbaseline** (Windows 10-Sicherheit)
- **Microsoft Defender ATP-Baseline**

Aktualisierte Baselineversionen bieten Unterstützung für aktuelle Einstellungen, sodass Sie die von den jeweiligen Produktteams empfohlenen bewährten Konfigurationen beibehalten können.

### <a name="use-endpoint-security-configuration-details-to-identify-the-source-of-policy-conflicts-for-devices---7567503--idstaged----"></a>Verwenden von Konfigurationsdetails der Endpunktsicherheit zur Ermittlung der Quelle von Richtlinienkonflikten für Geräte<!-- 7567503  idstaged  -->
Bei der Konfliktauflösung werden Sie in Kürze einen Drilldown in ein Sicherheitbaselineprofil durchführen können, um die *Konfiguration der Endpunktsicherheit* für ein ausgewähltes Gerät anzuzeigen. Dort können Sie Einstellungen auswählen, die einen *Konflikt* oder *Fehler* anzeigen, und einen weiteren Drilldown durchführen, um eine Liste mit Details anzuzeigen. Zu diesen Details gehören die Profile und Richtlinien, die am Konflikt beteiligt sind. Wenn Sie dann eine Richtlinie auswählen, die eine Quelle eines Konflikts darstellt, wird in Intune der Bereich „Übersicht“ dieser Richtlinie geöffnet. In diesem Bereich können Sie die Richtlinienkonfiguration prüfen bzw. ändern. (**Geräte** > *wählen Sie ein Gerät aus* > **Konfiguration der Endpunktsicherheit** > *wählen Sie ein Profil oder eine Baseline aus* > *wählen Sie in der Liste mit für das Gerät ausgewählten Einstellungen eine Einstellung aus*).

Die folgenden Richtlinientypen können Sie beim Durchführen eines Drilldowns bei einer Sicherheitsbaseline als Quelle eines Konflikts identifiziert werden:
- Richtlinie zur Gerätekonfiguration
- Endpunktsicherheitsrichtlinien

### <a name="new-details-in-the-endpoint-security-configuration-for-a-device---7745029-----"></a>Neue Details bei der Konfiguration der Endpunktsicherheit für ein Gerät<!-- 7745029   -->
In der neuen Version können neue Details für Geräte als Teil der Konfiguration der Endpunktsicherheit von Geräten angezeigt werden. (**Endpunktsicherheit** > **Sicherheitsbaselines** > *ausgewählte Baseline* > **Profile** > *ausgewähltes Profil* > **Gerätestatus** > **Konfiguration der Endpunktsicherheit**). Die neuen Details:

- **UPN** (User Principle Name, Benutzerprinzipalname): Der UPN gibt an, welches Endpunktsicherheitsprofil einem bestimmten Benutzer am Gerät zugewiesen ist. Das ist hilfreich, um zwischen mehreren Benutzern an einem Gerät und mehreren Einträgen eines Profils oder einer Baseline zu unterscheiden, das bzw. die dem Gerät zugewiesen ist. 
- **Schlechtester Status**: Dieses Detail gibt die am wenigsten vorteilhafte Statusbedingung für das Gerät an. Wenn für diesen Status **Erfolg** angezeigt wird, weist das Gerät keine Richtlinienkonflikte oder -fehler auf.

### <a name="android-11-deprecates-deployment-of-trusted-root-certificates-to-device-administrator-enrolled-devices--7662775----"></a>Mit Android 11 wird die Bereitstellung von vertrauenswürdigen Stammzertifikaten für vom Geräteadministrator registrierte Geräte eingestellt<!--7662775  -->
Ab Android 11 können für Geräte, die als *Android-Geräteadministrator* registriert werden, keine vertrauenswürdigen Stammzertifikate mehr bereitgestellt werden. Von dieser Änderung sind Samsung Knox-Geräte aufgrund der Integration von Intune in die Knox-Plattform betroffen. Bei anderen Geräten (nicht Samsung) müssen Benutzer das vertrauenswürdige Stammzertifikat manuell auf dem Gerät installieren. 

Wenn auf einem Gerät das vertrauenswürdige Stammzertifikat manuell installiert wurde, können auf dem Gerät Zertifikate mit SCEP bereitgestellt werden. In diesem Fall muss aber immer noch eine Richtlinie für *vertrauenswürdige Zertifikate* für das Gerät erstellt und bereitgestellt und die Richtlinie mit dem Profil des *SCEP-Zertifikats* verknüpft werden.

- Wenn sich das vertrauenswürdige Stammzertifikat auf dem Gerät befindet, kann das SCEP-Zertifikatprofil erfolgreich installiert werden. 
- Wird das vertrauenswürdige Zertifikat jedoch nicht gefunden, kann das SCEP-Zertifikatprofil nicht installiert werden.

<!-- ***********************************************-->
## <a name="notices"></a>Benachrichtigungen

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Weitere Informationen:

Details zu aktuellen Entwicklungen finden Sie unter [Neuerungen in Microsoft Intune](whats-new.md).
