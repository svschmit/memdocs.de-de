---
title: Neues in Microsoft Intune – Azure | Microsoft-Dokumentation
titleSuffix: ''
description: Erfahren Sie, welche Neuerungen es im Intune-Azure-Portal gibt
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/17/2020
ms.topic: reference
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
ms.openlocfilehash: 2cd5e8f6e1975adf33131ca47049eb2d4a6f68cd
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262879"
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
### Scripts


<!-- ########################## -->
## <a name="week-of-july-13-2020--2007-service-release"></a>Woche vom 13. Juli 2020 (Dienstrelease 2007)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>App-Verwaltung

#### <a name="win32-app-installation-notifications-and-the-company-portal---7485945----"></a>Win32-App-Installationsbenachrichtigungen und das Unternehmensportal<!-- 7485945  -->
Endbenutzer können nun entscheiden, ob die in der [Webversion des Microsoft Intune-Unternehmensportals](https://portal.manage.microsoft.com/) angezeigten Anwendungen über die Unternehmensportal-App oder die Unternehmensportalwebsite geöffnet werden sollen. Diese Option steht nur zur Verfügung, wenn der Endbenutzer die Unternehmensportal-App installiert hat und eine Webunternehmensportal-Anwendung außerhalb eines Browsers startet. 

#### <a name="exchange-on-premises-connector-support---7138486----"></a>Unterstützung für den Connector für Microsoft Exchange lokal<!-- 7138486  -->
Ab Release Nr. 2007 (Juli) wird im Intune-Dienst die Unterstützung für den Connector für Exchange lokal eingestellt. Bestandskunden mit einem aktiven Connector können die aktuelle Funktionalität weiterhin nutzen. Neu- und Bestandskunden, die nicht über einen aktiven Connector verfügen, können keine neuen Connectors mehr erstellen oder Exchange ActiveSync-Geräte (EAS) über Intune verwalten. Diesen Kunden empfiehlt Microsoft die [hybride moderne Authentifizierung (HMA)](https://docs.microsoft.com/office365/enterprise/hybrid-modern-auth-overview) für Exchange, um den Zugriff auf Exchange lokal zu schützen. Die hybride moderne Authentifizierung ermöglicht sowohl Intune-App-Schutz-Richtlinien (auch MAM) als auch den bedingten Zugriff über Outlook Mobile für Exchange lokal.

#### <a name="smime-for-outlook-on-ios-and-android-enterprise-devices-managed-without-enrollment---6517155----"></a>Verwaltung von S/MIME für Outlook auf iOS- und Android Enterprise-Geräten ohne Registrierung<!-- 6517155  -->
Sie können nun S/MIME für Outlook auf iOS- und Android Enterprise-Geräten aktivieren, indem Sie App-Konfigurationsrichtlinien für Geräte einrichten, die ohne Registrierung verwaltet werden. Wählen Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) nacheinander **Apps** > **App-Konfigurationsrichtlinien** > **Hinzufügen** > **Verwaltete Anwendungen** aus. Darüber hinaus können Sie wählen, ob Sie Benutzern erlauben möchten, diese Einstellung in Outlook festzulegen oder nicht. Allgemeine Informationen zu S/MIME finden Sie unter [S/MIME-Übersicht zum Signieren und Verschlüsseln von E-Mails in Intune](../protect/certificates-s-mime-encryption-sign.md). Weitere Informationen zu den Outlook-Konfigurationseinstellungen finden Sie unter [Microsoft Outlook-Konfigurationseinstellungen](../apps/app-configuration-policies-outlook.md) und [Hinzufügen von App-Konfigurationsrichtlinien für verwaltete Apps ohne Geräteregistrierung](../apps/app-configuration-policies-managed-app.md). Informationen zu S/MIME, die speziell für Microsoft Exchange gelten, finden Sie unter [S/MIME-Szenarios](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune#smime-scenarios) und [Konfigurationsschlüssel – S/MIME-Einstellungen](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune#smime-settings).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Gerätekonfiguration

#### <a name="new-vpn-settings-for-windows-10-and-newer-devices---6602122-----"></a>Neue VPN-Einstellungen für Windows 10 und neuere Geräte<!-- 6602122   -->

Wenn Sie ein VPN-Profil mit dem IKEv2-Verbindungstyp erstellen, können Sie jetzt neue Einstellungen konfigurieren (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **Windows 10 und höher** für Plattform > **VPN** für Profil > **Basis-VPN**):

- **Gerätetunnel**: Ermöglicht Geräten den automatischen Verbindungsaufbau zu einem VPN, ohne dass eine Benutzerinteraktion, einschließlich Benutzeranmeldung, erforderlich ist. Diese Funktion erfordert, dass Sie **Always on** aktivieren und **Computerzertifikate** als Authentifizierungsmethode verwenden.
- Einstellungen der Kryptografie-Suite: Konfigurieren Sie die Algorithmen, die zum Sichern von IKE-und untergeordneten Sicherheitszuordnungen verwendet werden, wodurch Sie die Client-und Servereinstellungen aufeinander abstimmen können.

Informationen zu den Einstellungen, die Sie konfigurieren können, finden Sie unter [Windows-Geräteeinstellungen zum Hinzufügen von VPN-Verbindungen mithilfe von Intune](../configuration/vpn-settings-windows-10.md).

Gilt für:

- Windows 10 und höher

#### <a name="configure-more-microsoft-launcher-settings-in-a-device-restrictions-profile-on-android-enterprise-devices-cobo---6285001----"></a>Konfigurieren weiterer Microsoft Launcher-Einstellungen in einem Profil für Geräteeinschränkungen auf Android Enterprise-Geräten (COBO)<!-- 6285001  -->

Auf vollständig verwalteten Android Enterprise-Geräten können Sie mithilfe eines Profils für Geräteeinschränkungen weitere Microsoft Launcher-Einstellungen konfigurieren (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **Android Enterprise** für Plattform > **Nur Gerätebesitzer** > **Geräteeinschränkungen** > **Geräteoberfläche** > **Vollständig verwaltet**). 

Eine Liste dieser Einstellungen finden Sie unter [Android Enterprise-Geräteeinstellungen zum Zulassen oder Einschränken von Features](../configuration/device-restrictions-android-for-work.md#device-experience).

Die Einstellungen für Microsoft Launcher können auch mithilfe eines [App-Konfigurationsprofils](../apps/configure-microsoft-launcher.md) konfiguriert werden.

Gilt für:

- Vollständig verwaltete Geräte von Android Enterprise-Gerätebesitzern (COBO)

#### <a name="new-features-for-managed-home-screen-on-android-enterprise-device-owner-dedicated-devices-cosu---7414175-7133328-7133720-7134873-7135184---idstaged---"></a>Neue Features für Managed Home Screen auf dedizierten benutzereigenen Android Enterprise-Geräte (COSU)<!-- 7414175 7133328 7133720 7134873 7135184   idstaged -->

Auf Android Enterprise-Geräten können Administratoren mithilfe von Gerätekonfigurationsprofilen und dem Kioskmodus mit mehreren Apps den verwalteten Startbildschirm auf dedizierten Geräten konfigurieren (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **Android Enterprise** für Plattform > **Nur Gerätebesitzer** > **Geräteeinschränkungen** für Profil > **Geräteoberfläche** > **Dediziertes Gerät** > **Multi-App**).

Insbesondere bestehen die folgenden Möglichkeiten:

- Anpassen von Symbolen, Ändern der Bildschirmausrichtung und Anzeigen von App-Benachrichtigungen auf Badgesymbolen <!--7414175-->
- Ausblenden der Verknüpfung „Managed Settings“ (Verwaltete Einstellungen) <!--7133328-->
- Einfacherer Zugriff auf das Debugmenü <!--7133720-->
- Erstellen einer Zulassungsliste mit WLAN-Netzwerken <!-- 7134873-->
- Einfacherer Zugriff auf die Geräteinformationen <!-- 7135184-->

Weitere Informationen finden Sie unter [Android Enterprise-Geräteeinstellungen zum Zulassen oder Einschränken von Features](../configuration/device-restrictions-android-for-work.md) und in [diesem Blog](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-managed-home-screen-on-dedicated-devices/ba-p/1388060).

Gilt für:

- Dedizierte benutzereigene Android Enterprise-Geräte (COSU)

#### <a name="administrative-templates-updated-for-microsoft-edge-84--7722068--"></a>Administrative Vorlagen für Microsoft Edge 84 aktualisiert<!--7722068-->
Die für Microsoft Edge verfügbaren ADMX-Einstellungen wurden aktualisiert. Endbenutzer können jetzt neue ADMX-Einstellungen konfigurieren und bereitstellen, die in Edge 84 hinzugefügt wurden. Weitere Informationen finden Sie in den [Versionshinweisen zu Edge 84](https://docs.microsoft.com/deployedge/microsoft-edge-relnote-stable-channel#policy-updates).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Geräteregistrierung

#### <a name="corporate-owned-personally-enabled-devices-preview--4442275----"></a>Unternehmenseigene, persönlich aktivierte Geräte (Vorschau)<!--4442275  -->
Intune unterstützt nun für Betriebssystemversionen ab Android 8 unternehmenseigene Android Enterprise-Geräte mit einem Arbeitsprofil. Unternehmenseigene Geräte mit einem Arbeitsprofil sind eines der Unternehmensverwaltungsszenarien in der Android Enterprise-Lösungspalette. Dieses Szenario bezieht sich auf Geräte für Einzelbenutzer, die für den geschäftlichen und privaten Gebrauch bestimmt sind. Dieses Szenario unternehmenseigener, persönlich aktivierter Geräte bietet Folgendes:

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

Weitere Informationen zur Vorschau für unternehmenseigene Geräte mit einem Arbeitsprofil finden Sie im [Supportblog](https://techcommunity.microsoft.com/t5/intune-customer-success/microsoft-announces-public-preview-for-android-enterprise/ba-p/1524325).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Geräteverwaltung

#### <a name="updates-to-the-remote-lock-action-for-macos-devices--7032805-----"></a>Aktualisierungen der Aktion „Remotesperre“ für macOS-Geräte<!--7032805   -->
Beispiele für Änderungen an der Aktion „Remotesperre“ für macOS-Geräte:
- Die Wiederherstellungs-PIN wird 30 Tage lang angezeigt, ehe sie gelöscht wird (anstelle von 7 Tagen).
- Wenn ein Administrator einen zweiten Browser geöffnet hat und versucht, den Befehl noch einmal über eine andere Registerkarte oder einen anderen Browser auszulösen, lässt Intune den Befehl passieren. Der Meldestatus wird jedoch auf „fehlschlagen“ festgelegt, anstatt eine neue PIN zu generieren.
- Der Administrator darf keinen weiteren Remotesperrbefehl ausführen, wenn der vorherige Befehl noch aussteht oder das Gerät nicht wieder eingecheckt wurde.
Diese Änderungen sollen verhindern, dass die richtige PIN nach mehreren Remotesperrbefehlen überschrieben wird.

#### <a name="device-actions-report-differentiates-between-wipe-and-protected-wipe--7118901---"></a>Im Bericht „Device actions“ (Geräteaktionen) wird zwischen dem Löschen und dem geschützten Löschen unterschieden.<!--7118901 -->
Im Bericht **Device actions** (Geräteaktionen) wird nun zwischen dem Löschen und dem geschützten Löschen unterschieden. Wenn Sie diesen Bericht anzeigen möchten, navigieren Sie zu [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Geräte** > **Überwachung** > **Device Actions** (unter **Sonstige**).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Gerätesicherheit

#### <a name="microsoft-defender-firewall-rule-migration-tool-preview---6423187-----"></a>Vorschau für das Migrationstool für Microsoft Defender Firewall-Regeln<!-- 6423187   -->
Derzeit wird an einer Public Preview eines auf PowerShell basierenden Tools gearbeitet, mit dem Windows Defender Firewall-Regeln migriert werden können. Wenn Sie das Tool installieren und ausführen, werden für Intune automatisch Richtlinien für Firewallregeln zur Endpunktsicherheit erstellt, die auf der aktuellen Konfiguration eines Windows 10-Clients basieren. Weitere Informationen finden Sie unter [Übersicht über das Migrationstool für Firewallregeln zur Endpunktsicherheit](../protect/endpoint-security-firewall-rule-tool.md).

#### <a name="endpoint-detection-and-response-policy-for-onboarding-tenant-attached-devices-to-mdatp-is-generally-available---7303816-----"></a>Richtlinien zur Endpunkterkennung und -antwort für das Onboarding von als Mandanten angefügten Geräten in Microsoft Defender Advanced Threat Protection jetzt allgemein verfügbar<!-- 7303816   -->
Zur Stärkung der Endpunktsicherheit in Intune wurde die *Vorschauphase* der [Richtlinien zur Endpunkterkennung und -antwort (Endpoint Detection and Response, EDR) für Geräte beendet, die mit Configuration Manager verwaltet werden](../protect/endpoint-security-edr-policy.md). Die Richtlinien sind nun *allgemein verfügbar*.

Wenn Sie die EDR-Richtlinien mit Geräten verwenden möchten, die über eine unterstützte Version von Configuration Manager verfügen, müssen Sie die [Mandantenanfügung für Configuration Manager](../../configmgr/tenant-attach/device-sync-actions.md) konfigurieren. Wenn Sie Konfiguration der Mandantenanfügung abgeschlossen haben, können Sie die EDR-Richtlinien bereitstellen, um für Geräte, die von Configuration Manager verwaltet werden, ein Onboarding in Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) durchzuführen.

#### <a name="bluetooth-settings-are-available-in-device-control-profiles-for-endpoint-security-attack-surface-reduction-policy---7032084-----"></a>Bluetooth-Einstellungen für Gerätesteuerungsprofile jetzt in der Richtlinie zur Verringerung der Angriffsfläche für Endpunktsicherheit verfügbar <!--7032084   -->
Dem [Gerätesteuerungsprofil](../protect/endpoint-security-asr-profile-settings.md#device-control-profile) für die *Richtlinie zur Verringerung der Angriffsfläche für Endpunktsicherheit* wurden nun Einstellungen für die Verwaltung von Bluetooth auf Windows 10-Geräten hinzugefügt.  Dabei handelt es sich um dieselben Einstellungen, die auch in Geräteeinschränkungsprofilen für die *Gerätekonfiguration* verfügbar sind.

#### <a name="manage-source-locations-for-definition-updates-with-endpoint-security-antivirus-policy-for-windows-10-devices---6347801-----"></a>Verwalten der Quellspeicherorte für Definitionsaktualisierungen der Antivirenrichtlinie von Endpunkten für Windows 10-Geräte<!-- 6347801   -->  
Der Kategorie *Updates* der [Endpunktsicherheits-Antivirenrichtlinie für Windows 10-Geräte](../protect/antivirus-microsoft-defender-settings-windows.md#updates) wurden zwei neue Einstellungen hinzugefügt. Diese bieten Ihnen die Möglichkeit zu verwalten, wie Geräte Updatedefinitionen abrufen:

- *Dateifreigaben zum Herunterladen von Definitionsupdates definieren*
- *Reihenfolge der Quellen zum Herunterladen von Definitionsupdates definieren*

Mit den neuen Einstellungen können Sie nun UNC-Dateifreigaben als Quellspeicherorte zum Herunterladen von Definitionsaktualisierungen hinzufügen und die Reihenfolge festlegen, in der die verschiedenen Quellspeicherorte abgerufen werden.

#### <a name="improved-security-baselines-node---7433136------"></a>Verbesserter Sicherheitsbaselineknoten<!-- 7433136    -->
Es wurden einige Änderungen vorgenommen, um die Verwendbarkeit des [Sicherheitsbaselineknotens](../protect/security-baselines.md) im Microsoft Endpoint Manager Admin Center zu verbessern. Wenn Sie nun **Endpunktsicherheit** > **Sicherheitsbaselines** aufrufen und einen Sicherheitsbaselinetyp wie die MDM-Sicherheitsbaseline auswählen, wird der Bereich **Profile** angezeigt. Im Bereich „Profile“ sind die Profile aufgeführt, die Sie für diesen Baselinetyp erstellt haben.  Zuvor wurde in der Konsole ein Übersichtsbereich angezeigt, der einen zusammengefassten Datenrollup enthielt. Dieses stimmte nicht immer mit den Details aus den Berichten für einzelne Profile überein.

Im Bereich „Profile“ können Sie weiterhin ein Profil auswählen, für das Sie einen Drilldown ausführen können, um die Eigenschaften sowie verschiedene Berichte anzuzeigen, die unter *Überwachung* verfügbar sind.  Ebenso können Sie auf derselben Ebene wie „Profile“ weiterhin **Versionen** auswählen, um die verschiedenen Versionen des Profiltyps anzuzeigen, die Sie bereitgestellt haben. Wenn Sie für eine Version einen Drilldown ausführen, erhalten Sie auch Zugriff auf Berichte, die den Profilberichten ähneln. 

#### <a name="derived-credentials-support-for-windows---4886090-----"></a>Unterstützung von abgeleiteten Anmeldeinformationen für Windows<!-- 4886090   -->
Sie können von nun an abgeleitete Anmeldeinformationen auf Ihren Windows-Geräten einsetzen. Dadurch wird die vorhandene Unterstützung für iOS/iPadOS und Android erweitert. Die folgenden Anbieter von abgeleiteten Anmeldeinformationen werden unterstützt:
- Entrust Datacard
- Intercede
- DISA Purebred

Für Windows wird auch die Verwendung abgeleiteter Anmeldeinformationen für die Authentifizierung bei WLAN- oder VPN-Profilen unterstützt. Die abgeleiteten Anmeldeinformationen für Windows-Geräte werden von einer Client-App ausgegeben, die von Ihrem Anbieter für abgeleiteten Anmeldeinformationen bereitgestellt wird.

#### <a name="manage-filevault-encryption-for-devices-that-were-encrypted-by-the-device-user-and-not-by-intune--5239424----"></a>Verwalten der FileVault-Verschlüsselung für Geräte, die vom Gerätebenutzer und nicht von Intune verschlüsselt wurden<!--5239424  -->
Intune kann nun [auf macOS-Geräten die Verwaltung der FileVault-Verschlüsselung von Datenträgern übernehmen, die vom Gerätebenutzer](../protect/encrypt-devices-filevault.md#assume-management-of-filevault-on-previously-encrypted-devices) und nicht von einer Intune-Richtlinie verschlüsselt wurden.  Dieses Szenario erfordert Folgendes:
- Ein Gerät, auf das die Datenträgerverschlüsselungsrichtlinien von Intune angewendet wird und das FileVault unterstützt
- Ein Gerätebenutzer, der über die Website des Unternehmensportals seinen persönlichen Wiederherstellungsschlüssel für das verschlüsselte Gerät in Intune hochlädt Zum Hochladen des Schlüssels muss der Benutzer für sein verschlüsseltes macOS-Gerät die Option *Store recovery key* (Wiederherstellungsschlüssel speichern) auswählen.

Nachdem der Benutzer den Wiederherstellungsschlüssel hochgeladen hat, wird der Schlüssel in Intune rotiert, um zu überprüfen, ob er gültig ist. Anschließend kann Intune den Schlüssel und die Verschlüsselung so verwalten, als wäre das Gerät direkt mithilfe einer Richtlinie verschlüsselt worden. Sollte ein Benutzer sein Gerät wiederherstellen müssen, kann er über die folgenden Ressourcen auf jedem beliebigen Gerät auf den Wiederherstellungsschlüssel zugreifen:   
- Unternehmensportal-Website
- Unternehmensportal-App für iOS oder iPadOS 
- Unternehmensportal-App für Android
- Intune-App

#### <a name="hide-the-personal-recovery-key-from-a-device-user-during-macos-filevault-disk-encryption----5475632--"></a>Ausblenden des persönlichen Wiederherstellungsschlüssels vor einem Gerätebenutzer während der Datenträgerverschlüsselung mit FileVault unter macOS<!--  5475632-->
Wenn Sie die FileVault-Datenträgerverschlüsselung für macOS-Geräte mithilfe einer Endpunktsicherheitsrichtlinie konfigurieren, sollten Sie mithilfe der Einstellung [**Wiederherstellungsschlüssel ausblenden**](../protect/endpoint-security-disk-encryption-profile-settings.md#filevault) verhindern, dass dem Gerätebenutzer der *persönliche Wiederherstellungsschlüssel* angezeigt wird, während das Gerät verschlüsselt wird. Indem der Schlüssel während der Verschlüsselung ausgeblendet wird, ist er besser geschützt, da Benutzer ihn nicht in ihrer Wartezeit aufschreiben können. 

Sollte ein Benutzer sein Gerät später wiederherstellen müssen, kann er seinen persönlichen Wiederherstellungsschlüssel stattdessen jederzeit mithilfe eines beliebigen Geräts über die Website, die iOS/iPadOS-App, die Android-App oder die Intune-App des Intune-Unternehmensportals einsehen.

#### <a name="improved-view-of-security-baseline-details-for-devices---5536846----"></a>Verbesserte Ansicht der Details zur Sicherheitsbaseline für Geräte<!-- 5536846  -->
Sie können nun für die Details eines Geräts einen Drilldown ausführen, um die Einstellungsdetails zu den Sicherheitsbaselines aufzurufen, die für das Gerät gelten. Die Einstellungen werden in einer einfachen, flachen Liste angezeigt, die die Einstellungskategorie, den Einstellungsnamen und den Status enthält. Weitere Informationen finden Sie unter [Anzeigen der Endpunktsicherheitskonfigurationen pro Gerät](../protect/security-baselines-monitor.md#view-endpoint-security-configurations-per-device).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Überwachung und Problembehandlung

#### <a name="device-compliance-logs-now-in-english--6014904----"></a>Protokolle zur Gerätekonformität jetzt in englischer Sprache<!--6014904  -->
Die DeviceComplianceOrg-Protokolle in Intune enthielten zuvor nur Enumerationen für ComplianceState, OwnerType und DeviceHealthThreatLevel. Die Spalten in diesen Protokollen enthalten jetzt auch englischsprachige Informationen.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Rollenbasierte Zugriffssteuerung

#### <a name="assign-profile-and-update-profile-permission-changes--7177586-idready-wnready-wnstaged--"></a>Änderungen an den Berechtigungen „Profil zuweisen“ und „Profil aktualisieren“<!--7177586 idready wnready wnstaged-->
Für den Flow für die automatische Geräteregistrierung wurden die Berechtigungen „Profil zuweisen“ und „Profil aktualisieren“ der rollenbasierten Zugriffssteuerung geändert:

Profil zuweisen: Administratoren mit dieser Berechtigung können den Profilen auch Token zuweisen und einem Token ein Standardprofil für die automatische Geräteregistrierung zuweisen.

Profil aktualisieren: Administratoren mit dieser Berechtigung können vorhandene Profile nur für die automatische Geräteregistrierung aktualisieren.

Navigieren Sie zum Anzeigen dieser Rollen zu [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Mandantenverwaltung** > **Rollen** > **Alle Rollen** > **Erstellen** > **Berechtigungen** > **Rollen**.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="scripting"></a>Skripterstellung

#### <a name="additional-data-warehouse-v10-properties---6125732-wnready---"></a>Zusätzliche Data Warehouse v1.0-Eigenschaften<!-- 6125732 wnready -->
Mithilfe von Intune Data Warehouse v1.0 stehen weitere Eigenschaften zur Verfügung. Die folgenden Eigenschaften werden jetzt über die Entität [devices](../developer/reports-ref-devices.md#devices) verfügbar gemacht:
- `ethernetMacAddress`: Der eindeutige Netzwerkbezeichner dieses Geräts.
- `office365Version`: Die auf dem Gerät installierte Version von Office 365.

Die folgenden Eigenschaften werden jetzt über die Entität [devicePropertyHistories](../developer/reports-ref-devices.md#devicepropertyhistories) verfügbar gemacht:
- `physicalMemoryInBytes`: Der physische Speicher in Byte.
- `totalStorageSpaceInBytes`: Gesamtspeicherkapazität in Bytes

Weitere Informationen finden Sie unter [Microsoft Intune Data Warehouse-API](../developer/reports-nav-intune-data-warehouse.md).

<!-- ########################## -->
## <a name="week-of-july-06-2020"></a>Woche ab 06. Juli 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>App-Verwaltung

#### <a name="update-to-device-icons-in-company-portal-and-intune-apps-on-android---6057023---"></a>Aktualisieren von Gerätesymbolen im Unternehmensportal und in Intune-Apps unter Android<!-- 6057023 -->
Wir haben die Gerätesymbole im Unternehmensportal und in Intune-Apps auf Android-Geräten aktualisiert, um ihnen ein moderneres Erscheinungsbild in Einklang mit dem Microsoft Fluent Design System zu verleihen. Weitere Informationen finden Sie unter [Aktualisieren von Symbolen in der Unternehmensportal-App für iOS/iPadOS und macOS](../fundamentals/whats-new-app-ui.md#update-to-icons-in-company-portal-app-for-iosipados-and-macos-). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Geräteregistrierung

#### <a name="ios-company-portal-will-support-apples-automated-device-enrollment-without-user-affinity---7282707---"></a>Das iOS-Unternehmensportal unterstützt die automatische Geräteregistrierung von Apple ohne Benutzeraffinität<!-- 7282707 --> 
Das iOS-Unternehmensportal wird jetzt auf Geräten unterstützt, die mit der automatischen Geräteregistrierung von Apple registriert werden, ohne dass ein zugewiesener Benutzer erforderlich ist. Ein Endbenutzer kann sich beim iOS-Unternehmensportal anmelden, um sich als primärer Benutzer eines iOS-/iPadOS-Geräts einzurichten, das ohne Geräteaffinität registriert ist. Weitere Informationen zur automatischen Geräteregistrierung finden Sie unter [Automatisches Registrieren von iOS-/iPadOS-Geräten mit der automatischen Geräteregistrierung von Apple](../enrollment/device-enrollment-program-enroll-ios.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Geräteverwaltung

#### <a name="tenant-attach-configmgr-client-details-in-the-admin-center-preview---7552762---"></a>Mandantenanfügung: Configuration Manager-Clientdetails im Admin Center (Vorschau)<!-- 7552762 -->

Im Admin Center von Microsoft Endpoint Manager werden jetzt Configuration Manager-Clientdetails angezeigt, wie z. B. Sammlungen, die Zugehörigkeit zu Begrenzungsgruppen und Clientinformationen in Echtzeit für ein bestimmtes Gerät. Weitere Informationen finden Sie unter [Anfügen von Mandanten: Configuration Manager-Clientdetails im Admin Center (Vorschau)](../../configmgr/tenant-attach/client-details.md).

## <a name="week-of-june-22-2020"></a>Woche ab 22. Juni 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>App-Verwaltung

#### <a name="newly-available-protected-apps-for-intune---7248952---"></a>Neu verfügbare geschützte Apps für Intune<!-- 7248952 -->
Ab sofort sind die folgenden geschützten Apps verfügbar:
- BlueJeans-Videokonferenzen
- Cisco Jabber for Intune
- Tableau Mobile for Intune
- ZERØ for Intune

Weitere Informationen zu geschützten Apps finden Sie unter [Durch Microsoft Intune geschützte Apps](../apps/apps-supported-intune-apps.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Überwachung und Problembehandlung

#### <a name="use-endpoint-analytics-to-improve-user-productivity-and-reduce-it-support-costs---5653063---"></a>Verwenden von Endpunktanalysen zur Verbesserung der Benutzerproduktivität und Senkung der IT-Supportkosten<!-- 5653063 --> 
Dieses Feature wird in der nächsten Woche eingeführt. Die Endpunktanalyse zielt darauf ab, durch Erkenntnisse über die Benutzerfreundlichkeit die Benutzerproduktivität zu verbessern und die IT-Supportkosten zu senken. Anhand der gewonnenen Erkenntnisse können IT-Mitarbeitern die Endbenutzererfahrung durch proaktiven Support optimieren und durch Bewertung der Auswirkungen von Konfigurationsänderungen auf Benutzer Beeinträchtigungen der Benutzerfreundlichkeit erkennen. Weitere Informationen finden Sie unter [Endpunktanalyse (Vorschau)](https://aka.ms/uea).

#### <a name="proactively-remediate-end-user-device-issues-using-script-packages---5933328---"></a>Proaktive Behebung von Geräteproblemen bei Endbenutzern mithilfe von Skriptpaketen<!-- 5933328 -->
Sie können Skriptpakete auf Endbenutzergeräten erstellen und ausführen, um die häufigsten Supportfälle in Ihrer Organisation proaktiv zu ermitteln und zu beheben. Durch die Bereitstellung von Skriptpaketen können Sie den Supportbedarf verringern. Sie können ein eigenes Skriptpaket erstellen oder eines der Skriptpakete bereitstellen, die wir geschrieben und in unserer Umgebung verwendet haben, um die Zahl der Supporttickets zu verringern. Über Intune können Sie den Status der bereitgestellten Skriptpakete anzeigen und die Ergebnisse der Problemerkennung und -behebung überwachen. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Berichte** > **Endpunktanalyse** > **Proaktive Korrekturen**. Weitere Informationen finden Sie unter [Proaktive Korrekturen](https://aka.ms/uea_prs).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Gerätesicherheit

#### <a name="use-microsoft-defender-atp-in-compliance-policies-for-android---4425686----"></a>Verwenden von Microsoft Defender ATP in Compliancerichtlinien für Android<!-- 4425686  -->

Sie können Intune jetzt für das [Onboarding von Android-Geräten in Microsoft Defender Advanced Threat Protection](../protect/advanced-threat-protection-configure.md#onboard-devices) (Microsoft Defender ATP) verwenden. Nachdem das Onboarding für die registrierten Geräte abgeschlossen ist, können Ihre Compliancerichtlinien für Android die Signale für die *Bedrohungsstufen* von Microsoft Defender ATP verwenden. Diese sind mit den Signalen identisch, die Sie bereits für Windows 10-Geräte verwenden können.

#### <a name="configure-defender-atp-web-protection-for-android-devices---6185563----"></a>Konfigurieren des Defender ATP-Webschutzes für Android-Geräte<!-- 6185563  -->

Wenn Sie Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) für Android-Geräte verwenden, können Sie den [Webschutz](../protect/advanced-threat-protection-manage-android.md) so konfigurieren, dass Phishingscans deaktiviert werden oder für Scans kein VPN verwendet werden kann.

Je nachdem, wie Ihr Android-Gerät bei Intune registriert ist, sind die folgenden Optionen verfügbar:

- Android-Geräteadministrator: Verwenden Sie benutzerdefinierte OMA-URI-Einstellungen, um den Webschutz zu deaktivieren, oder deaktivieren Sie nur die Verwendung von VPNs bei Scanvorgängen.
- Android Enterprise-Workerprofil: Verwenden Sie ein App-Konfigurationsprofil und den Konfigurations-Designer, um den Webschutz vollständig zu deaktivieren.

<!-- ########################## -->
## <a name="week-of-june-15-2020--2006-service-release"></a>Woche ab 15. Juni 2020 (Dienstrelease 2006)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>App-Verwaltung  

#### <a name="telecommunications-data-transfer-protection-for-managed-apps---6884491----"></a>Datenübertragungsschutz bei der Telekommunikation für verwaltete Apps<!-- 6884491  -->
Wenn in einer verknüpften App eine per Hyperlink verknüpfte Telefonnummer ermittelt wird, überprüft Intune, ob eine Schutzrichtlinie angewendet wurde, die die Übertragung dieser Nummer an eine Wähltasten-App zulässt. Sie können festlegen, wie Inhalte dieser Art übertragen werden sollen, wenn die Übertragung von einer durch Richtlinien verwaltete App initiiert wird. Wenn Sie eine App-Schutzrichtlinie in Microsoft Endpoint Manager erstellen, müssen Sie eine Option für verwaltete Apps unter **Organisationsdaten an andere Apps senden** auswählen. Anschließend müssen Sie noch eine Option unter **Transfer telecommunications data to** (Empfänger der Telekommunikationsdaten) auswählen. Weitere Informationen zu dieser Datenschutzeinstellung finden Sie unter [Einstellungen für App-Schutzrichtlinien für Android in Microsoft Intune](../apps/app-protection-policy-settings-android.md) und [Einstellungen für App-Schutzrichtlinien für iOS](../apps/app-protection-policy-settings-ios.md). 

#### <a name="unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-company-portal---7414033----"></a>Einheitliche Bereitstellung von Azure AD-Enterprise- und Office Online-Anwendungen im Unternehmensportal<!-- 7414033  -->
Sie können im Bereich **Anpassung** von Intune **Azure AD-Unternehmensanwendungen** und **Office Online-Anwendungen** im Unternehmensportal **ausblenden** oder **anzeigen**. Jeder Endbenutzer sieht den gesamten Anwendungskatalog für den ausgewählten Microsoft-Dienst. Standardmäßig wird jede zusätzliche App auf **Ausblenden** festgelegt. Dieses Feature wird zuerst auf der Unternehmensportal-Website wirksam. Eine Unterstützung im Windows-Unternehmensportal soll in Kürze folgen. Diese Konfigurationseinstellung finden Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) unter **Mandantenverwaltung** > **Anpassung**. Weitere Informationen finden Sie unter [Anpassen von Intune-Unternehmensportal-Apps, der Unternehmensportal-Website und der Intune-App](../apps/company-portal-app.md).

#### <a name="improvements-to-the-company-portal-for-macos-enrollment-experience---6444452----"></a>Verbesserungen am Unternehmensportal für die macOS-Registrierung<!-- 6444452  -->
Das Unternehmensportal für die macOS-Registrierung verfügt über einen einfacheren Registrierungsprozess, der sich enger an das Unternehmensportal für die iOS-Registrierung ausrichtet. Gerätebenutzern wird Folgendes angezeigt:  
- Eine schlankere Benutzeroberfläche  
- Eine verbesserte Prüfliste für die Registrierung  
- Deutlichere Anweisungen zum Registrieren ihrer Geräte  
- Verbesserte Optionen zur Problembehandlung  

Weitere Informationen zum Unternehmensportal finden Sie unter [Anpassen von Intune-Unternehmensportal-Apps, der Unternehmensportal-Website und der Intune-App](../apps/company-portal-app.md).

#### <a name="improvements-to-devices-page-of-iosipados-and-macos-company-portals---6055001---"></a>Verbesserungen an der Seite „Geräte“ in iOS/iPadOS- und macOS-Unternehmensportalen<!-- 6055001 -->
Es wurden Änderungen an der Unternehmensportal-Seite **Geräte** vorgenommen, um die App-Nutzung für iOS-, iPadOS- und Mac-Benutzer zu optimieren. Die Darstellung und das Verhalten wurden modernisiert, zudem wurden die Gerätedetails in eine einzige Spalte mit definierten Headern zentralisiert, sodass Benutzer den Gerätestatus einfacher überprüfen können. Darüber hinaus haben wir für Benutzer, deren Geräte nicht kompatibel sind, eindeutige Hinweise und Problembehandlungsschritte hinzugefügt. Weitere Informationen zum Unternehmensportal finden Sie unter [Anpassen von Intune-Unternehmensportal-Apps, der Unternehmensportal-Website und der Intune-App](../apps/company-portal-app.md). Informationen zum manuellen Synchronisieren eines Geräts finden Sie unter [Manuelles Synchronisieren von iOS-Geräten](../user-help/sync-your-device-manually-ios.md).  

#### <a name="cloud-setting-for-iosipados-company-portal-app---7071303----"></a>Cloudeinstellung für die Unternehmensportal-App unter iOS und iPadOS<!-- 7071303  -->
Mithilfe einer neuen **Cloudeinstellung** für das Unternehmensportal unter iOS und iPadOS können Benutzer die Authentifizierung jetzt an die entsprechende Cloud ihrer Organisation weiterleiten. Standardmäßig ist diese Einstellung auf **Automatisch** festgelegt. Das bedeutet, dass die Authentifizierung automatisch an die Cloud weitergeleitet wird, die vom Gerät des Benutzers erkannt wird. Wenn die Authentifizierung für Ihre Organisation nicht an die automatisch erkannte Cloud erfolgen soll (zum Beispiel eine öffentliche Cloud oder Government Cloud), kann der Benutzer die geeignete Cloud manuell über **Einstellungen** > **Unternehmensportal** > **Cloud** auswählen. Benutzer sollten nur dann eine andere **Cloudeinstellung** als **Automatisch** auswählen, wenn sie sich von einem anderen Gerät aus anmelden und die entsprechende Cloud nicht automatisch erkannt wird. 

#### <a name="duplicate-apple-vpp-tokens---7101606----"></a>Doppelte Apple Volume Purchase Program-Tokens<!-- 7101606  -->
Apple Volume Purchase Program-Tokens mit demselben **Tokenspeicherort** werden jetzt als **Doppelt vorhanden** gekennzeichnet und können wiederholt synchronisiert werden, wenn das doppelte Token entfernt wurde. Sie können weiterhin Lizenzen für Tokens zuweisen und widerrufen, die als Duplikate markiert sind. Lizenzen für neue Apps und erworbene Bücher werden jedoch möglicherweise nicht berücksichtigt, wenn ein Token als Duplikat markiert ist. Sie können Apple Volume Purchase Program-Tokens für Ihren Mandanten suchen, indem Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Mandantenverwaltung** > **Connectors und Token** > **Apple-VPP-Token** klicken. Weitere Informationen zu VPP-Tokens finden Sie unter [Verwalten von iOS- und macOS-Apps, die über das Apple Volume Purchase Program mit Microsoft Intune erworben wurden](../apps/vpp-apps-ios.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Gerätekonfiguration

#### <a name="add-multiple-root-certificates-for-eap-tls-authentication-in-wi-fi-profiles-on-macos-devices---2077871----"></a>Hinzufügen mehrerer Stammzertifikate für die EAP-TLS-Authentifizierung in WLAN-Profilen auf macOS-Geräten<!-- 2077871  -->

Auf macOS-Geräten können Sie ein WLAN-Profil erstellen und dann den EAP-Authentifizierungstyp (Extensible Authentication Protocol, erweiterbares Authentifizierungsprotokoll) auswählen. Klicken Sie hierfür auf **Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **macOS**. Wählen Sie dann den Profiltyp **WLAN** aus, und legen Sie **WLAN-Typ** auf „Unternehmen“ fest.

Wenn Sie den **EAP-Typ** auf die **EAP-TLS**-, **EAP-TTLS**- oder **PEAP**-Authentifizierung festlegen, können Sie mehrere Stammzertifikate hinzufügen. Zuvor konnten Sie nur ein Stammzertifikat hinzufügen.

Weitere Informationen zu den konfigurierbaren Einstellungen finden Sie unter [Hinzufügen von WLAN-Einstellungen für macOS-Geräte in Microsoft Intune](../configuration/wi-fi-settings-macos.md).

Gilt für:
- macOS

#### <a name="use-pkcs-certificates-with-wi-fi-profiles-on-windows-10-and-newer-devices---3246388-----"></a>Verwenden von PKCS-Zertifikaten mit WLAN-Profilen auf Windows 10-Geräten und neueren Geräten<!-- 3246388   -->
Sie können Windows-WLAN-Profile mit SCEP-Zertifikaten authentifizieren. Klicken Sie hierfür auf **Gerätekonfiguration** > **Profile** > **Profil erstellen** > **Windows 10 und höher**. Wählen Sie dann den Profiltyp **WLAN** aus, und klicken Sie auf **Unternehmen** > **EAP-Typ**. Nun können Sie PKCS-Zertifikate mit Ihren Windows-WLAN-Profilen verwenden. Mithilfe dieses Features können Benutzer WLAN-Profile mit neuen oder vorhandenen PKCS-Zertifikatprofilen in Ihrem Mandanten authentifizieren. 

Weitere Informationen zu den konfigurierbaren WLAN-Einstellungen finden Sie unter [Hinzufügen von WLAN-Einstellungen für Windows 10-Geräte oder neuere Geräte in Intune](../configuration/wi-fi-settings-windows.md).

Gilt für:
- Windows 10 und höher

#### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>Gerätekonfigurationsprofil für das kabelgebundene Netzwerk für macOS-Geräte<!-- 3508686  -->
Ein neues Gerätekonfigurationsprofil für macOS ist verfügbar, das kabelgebundene Netzwerke konfiguriert. Klicken Sie auf **Geräte** > **Konfigurationsprofile > **Profil erstellen** > **macOS**, und wählen Sie das Profil **Kabelgebundenes Netzwerk** aus. Verwenden Sie dieses Feature zum Erstellen von 802.1x-Profilen für die Verwaltung von kabelgebundenen Netzwerken, und stellen Sie dieses Netzwerke für Ihre macOS-Geräte bereit.

Weitere Informationen zu diesem Feature finden Sie unter [Kabelgebundene Netzwerke unter macOS](../configuration/wired-networks-configure.md).

Gilt für:
- macOS

#### <a name="use-microsoft-launcher-as-the-default-launcher-for-fully-managed-android-enterprise-devices---4927976-----"></a>Verwenden von Microsoft Launcher als Standardstartprogramm für vollständig verwaltete Android Enterprise-Geräte<!-- 4927976   -->
Auf Geräten von Android Enterprise-Gerätebesitzern können Sie Microsoft Launcher als Standardstartprogramm für vollständig verwaltete Geräte festlegen (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **Android Enterprise** für Plattform > **Gerätebesitzer** > **Geräteeinschränkungen** für Profil > **Gerätefunktionen**). Verwenden Sie [App-Konfigurationsrichtlinien](../apps/configure-microsoft-launcher.md), um alle anderen Microsoft Launcher-Einstellungen zu konfigurieren. 

Außerdem gibt es einige weitere Aktualisierungen der Benutzeroberfläche. Unter anderem wurde **Dedizierte Geräte** in **Gerätefunktionen** umbenannt.

Informationen zu den Funktionen, die Sie einschränken können, finden Sie unter [Android Enterprise-Geräteeinstellungen zum Zulassen oder Einschränken von Features mit Intune](../configuration/device-restrictions-android-for-work.md). 

Gilt für:
- Vollständig verwaltete Geräte von Android Enterprise-Gerätebesitzern (COBO)

#### <a name="use-autonomous-single-app-mode-settings-to-configure-the-ios-company-portal-app-to-be-a-sign-insign-out-app---7055619-----"></a>Verwenden Sie Einstellungen für den autonomen Einzelanwendungsmodus, um das iOS-Unternehmensportal als App für die An- und Abmeldung zu konfigurieren.<!-- 7055619   -->
Auf iOS- und iPadOS-Geräten können Sie Apps so konfigurieren, dass sie im autonomen Einzelanwendungsmodus (Autonomous Single-App Mode, ASAM) ausgeführt werden. Jetzt unterstützt die Unternehmensportal-App auch den ASAM und kann als App für An- und Abmeldung festgelegt werden. In diesem Modus müssen sich Benutzer bei der Unternehmensportal-App anmelden, um andere Apps und die Schaltfläche „Startbildschirm“ auf dem Gerät zu verwenden. Wenn sie sich von der Unternehmensportal-App abmelden, kehrt das Gerät in den Einzelanwendungsmodus zurück und sperrt die Unternehmensportal-App.

Navigieren Sie zu **Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **iOS/iPadOS** > **Geräteeinschränkungen** > **Autonomer Einzelanwendungsmodus**, um das Unternehmensportal für den ASAM zu konfigurieren.

Weitere Informationen finden Sie unter [Autonomer Einzelanwendungsmodus (ASAM)](../configuration/device-restrictions-ios.md#autonomous-single-app-mode-asam) und [Einzelanwendungsmodus](https://support.apple.com/guide/mdm/single-app-mode-mdm80a981/1/web/1) (öffnet die Apple-Website).

Gilt für:
- iOS/iPadOS

#### <a name="configure-content-caching-on-macos-devices---7106872-----"></a>Konfigurieren des Content Caching auf macOS-Geräten<!-- 7106872   -->
Auf macOS-Geräten können Sie ein Konfigurationsprofil erstellen, mit dem das Content Caching konfiguriert wird (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **macOS** für Plattform > **Gerätefunktionen** für Profil). Verwenden Sie diese Einstellungen unter anderem, um den Cache zu löschen, die Cache-Freigabe zuzulassen und ein Cachelimit auf dem Datenträger festzulegen.

Weitere Informationen zum Content Caching finden Sie unter [Content Caching](https://developer.apple.com/documentation/devicemanagement/contentcaching) (öffnet die Apple-Website).

Informationen zu den konfigurierbaren Einstellungen finden Sie unter [macOS-Gerätefunktionseinstellungen in Intune](../configuration/macos-device-features-settings.md).

Gilt für:
- macOS

#### <a name="add-new-schema-settings-and-search-for-existing-schema-settings-using-oemconfig-on-android-enterprise---6394386-----"></a>Hinzufügen neuer Schemaeinstellungen und Suchen nach vorhandene Schemaeinstellungen mithilfe von OEMConfig unter Android Enterprise<!-- 6394386   -->
In Intune können Sie mithilfe von OEMConfig die Einstellungen auf Android Enterprise-Geräten verwalten (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **Android Enterprise** für Plattform > **OEMConfig** für Profil). Wenn Sie den **Konfigurations-Designer**verwenden, werden die Eigenschaften im App-Schema angezeigt. Im **Konfigurations-Designer** können Sie nun folgende Aktionen ausführen:

- Hinzufügen neuer Einstellungen zum App-Schema
- Suchen nach neuen und vorhandenen Einstellungen im App-Schema

Weitere Informationen zu OEMConfig-Profilen in Intune finden Sie unter [Verwenden und Verwalten von Android Enterprise-Geräten mit OEMConfig in Microsoft Intune](../configuration/android-oem-configuration-overview.md).

Gilt für:
- Android Enterprise

#### <a name="block-shared-ipad-temporary-sessions-on-shared-ipad-devices---6613794----"></a>Blockieren von temporären Shared iPad-Sitzungen auf Shared iPad-Geräten blockieren<!-- 6613794  -->
In Intune gibt es die neue Einstellung **Temporäre Shared iPad-Sitzungen blockieren**. Sie blockiert temporäre Sitzungen auf Shared iPad-Geräten (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **iOS/iPadOS** für Plattform > **Geräteeinschränkungen** für Profiltyp > **Shared iPad**). Wenn diese Einstellung aktiviert ist, können Endbenutzer das Gastkonto nicht verwenden. Sie müssen sich mit Ihrer verwalteten Apple-ID und dem dazugehörigen Kennwort am Gerät anmelden. 

Weitere Informationen finden Sie unter [iOS- und iPadOS-Geräteeinstellungen zum Zulassen oder Einschränken von Features mit Intune](../configuration/device-restrictions-ios.md).

Gilt für:
- Shared iPad-Geräte, auf denen iOS/iPadOS 13,4 und höher ausgeführt wird

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Geräteregistrierung

#### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344----"></a>BYOD-Geräte können VPN für die Bereitstellung verwenden<!--5015344  -->
Mit der neuen Autopilot-Profiloption **Überprüfung der Domänenkonnektivität überspringen** können Sie hybrid in Azure AD eingebundene Geräte ohne Zugriff auf Ihr Unternehmensnetzwerk mithilfe Ihres eigenen Drittanbieter-Win32-VPN-Clients bereitstellen. Die neue Option finden Sie unter [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Geräte**  > **Windows** > **Windows-Registrierung** > **Bereitstellungsprofile** > **Profil erstellen** > **Willkommensseite**.

#### <a name="enrollment-status-page-profiles-can-be-set-to-device-groups--3952138---"></a>Festlegen von Profilen für die Seite zum Registrierungsstatus auf Gerätegruppen<!--3952138 -->
Zuvor konnten ESP-Profile (Enrollment Status Page, Seite zum Registrierungsstatus) nur für Benutzergruppen verwendet werden. Nun können Sie diese auch als Zielgerätegruppen festlegen. Weitere Informationen finden Sie unter [Einrichten einer Seite zum Registrierungsstatus](../enrollment/windows-enrollment-status.md).

#### <a name="automated-device-enrollment-sync-errors---6988214---"></a>Synchronisierungsfehler bei der automatischen Geräteregistrierung<!-- 6988214 -->
Für iOS/iPadOS- und macOS-Geräte werden neue Fehler gemeldet, einschließlich:
- Ungültige Zeichen in der Telefonnummer oder Feld ist leer 
- Ungültiger oder leerer Konfigurationsname für das Profil 
- Ungültiger/abgelaufener Cursorwert oder kein Cursor gefunden
- Zurückgewiesenes oder abgelaufenes Token 
- Das Feld „Abteilung“ ist leer oder enthält zu viele Zeichen 
- Das Profil wurde von Apple nicht gefunden, und es muss ein neues erstellt werden. 
- Die Anzahl der entfernten Apple Business Manager-Geräte wird zur Seitenübersicht hinzugefügt, auf der Sie den Status Ihrer Geräte sehen.

#### <a name="shared-ipads-for-business--6367326-----"></a>Gemeinsam genutzte iPads für Unternehmen<!--6367326   -->
Sie können mit Intune und Apple Business Manager problemlos und sicher gemeinsam genutzte iPads einrichten, sodass Geräte von mehreren Mitarbeitern verwendet werden können. Das Apple-Feature [Gemeinsam genutztes iPad](https://developer.apple.com/education/shared-ipad/) bietet eine personalisierte Benutzeroberfläche für mehrere Benutzer, während Benutzerdaten beibehalten werden. Durch Verwendung einer verwalteten Apple-ID können Benutzer auf ihre Apps, Daten und Einstellungen zugreifen, nachdem sie sich in ihrer Organisation an einem gemeinsam genutzten iPad angemeldet haben. Gemeinsam genutzte iPads arbeiten mit Verbundidentitäten.

Wechseln Sie zur Anzeige dieses Features zu [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Geräte** > **iOS** > **iOS-Registrierung** > **Registrierungsprogrammtoken**, wählen Sie ein Token aus, und klicken Sie dann auf **Profile** > **Profil erstellen** > **iOS**. Wählen Sie auf der Seite **Verwaltungseinstellungen** die Option **Ohne Benutzeraffinität registrieren** aus. Daraufhin wird die Option **Gemeinsam genutztes iPad** angezeigt.

Voraussetzung: iPadOS 13.4 und höher In diesem Release wird Unterstützung für temporäre Sitzungen mit gemeinsam genutzten iPads hinzugefügt, sodass Benutzer ohne eine verwaltete Apple-ID auf ein Gerät zugreifen können. Nach der Abmeldung werden alle Benutzerdaten vom Gerät gelöscht, sodass das Gerät sofort wieder zur Verwendung bereitsteht, ohne dass eine Gerätezurücksetzung durchgeführt werden muss. 

#### <a name="updated-user-interface-for-apples-automated-device-enrollment--7430322---"></a>Aktualisierte Benutzeroberfläche für die automatische Geräteregistrierung von Apple<!--7430322 -->
Die Benutzeroberfläche wurde aktualisiert, um Apple-Programm zur Geräteregistrierung durch die automatische Geräteregistrierung zu ersetzen, damit die Apple-Terminologie eingehalten wird.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Geräteverwaltung

#### <a name="device-remote-lock-pin-available-for-macos--7281557-----"></a>Verfügbare Remote-Sperr-PINs für macOS-Geräte<!--7281557   -->
Die Verfügbarkeit von Remote-Sperr-PINs für macOS-Geräte wurde von 7 Tagen auf 30 Tage verlängert.

#### <a name="change-primary-user-on-co-managed-devices--7319183----"></a>Ändern des primären Benutzers auf gemeinsam verwalteten Geräten<!--7319183  -->
Sie können den primären Benutzer eines Geräts für gemeinsam verwaltete Windows-Geräte ändern. Weitere Informationen zum Suchen und ändern dieses Benutzers finden Sie unter [Suchen des primären Benutzers eines Intune-Geräts](../remote-actions/find-primary-user.md). Dieses Feature wird in den nächsten Wochen schrittweise eingeführt.

#### <a name="setting-the-intune-primary-user-also-sets-the-azure-ad-owner-property--7319227---"></a>Beim Festlegen des primären Intune-Benutzers wird auch die Azure AD Owner-Eigenschaft festgelegt.<!--7319227 -->
Mit diesem neuen Feature wird die Owner-Eigenschaft auf neu registrierten und in Azure AD Hybrid eingebundenen Geräten automatisch gleichzeitig festgelegt, wenn der primäre Intune-Benutzer festgelegt wird. Weitere Informationen zum primären Benutzer finden Sie unter [Suchen des primären Benutzers eines Intune-Geräts](../remote-actions/find-primary-user.md).

Dies ist eine Änderung am Registrierungsprozess und gilt nur für neu registrierte Geräte. Bei vorhandenen in Azure AD Hybrid eingebundenen Geräten müssen Sie die Azure AD Owner-Eigenschaft manuell aktualisieren. Zu diesem Zweck können Sie die [Funktion zum Ändern des primären Benutzers](../remote-actions/find-primary-user.md#change-a-devices-primary-user) oder [ein Skript](https://github.com/microsoftgraph/powershell-intune-samples/tree/master/ManagedDevices) verwenden.

Wenn Windows 10-Geräte den Status „In Azure Hybrid Directory eingebunden“ erhalten, wird der erste Benutzer des Geräts in Endpoint Manager zum primären Benutzer.  Derzeit wird der Benutzer nicht für das entsprechende Azure AD-Geräteobjekt festgelegt. Dies führt zu einer Inkonsistenz beim Vergleich der *Owner*-Eigenschaft aus einem Azure AD Portal mit der Eigenschaft *Primärer Benutzer* im Microsoft Endpoint Manager Admin Center. Die Azure AD Owner-Eigenschaft wird zum Sichern des Zugriffs auf die BitLocker-Wiederherstellungsschlüssel verwendet. Die Eigenschaft wird auf in Azure AD Hybrid eingebundenen Geräten nicht aufgefüllt. Diese Einschränkung verhindert das Einrichten der Self-Service-Wiederherstellung von BitLocker aus Azure AD. Dieses geplante Feature beseitigt diese Einschränkung.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Gerätesicherheit

#### <a name="hide-the-recovery-key-from-users-during-filevault-2-encryption-for-macos-devices---5459801----"></a>Ausblenden des Wiederherstellungsschlüssels für Benutzer während der FileVault 2-Verschlüsselung für macOS-Geräte<!-- 5459801  -->
Wir haben der *FileVault*-Kategorie innerhalb der [Endpoint Protection-Vorlage für macOS](../protect/endpoint-protection-macos.md#filevault) eine neue Einstellung hinzugefügt: **Hide recovery key** (Wiederherstellungsschlüssel ausblenden). Mit dieser Einstellung wird der persönliche Schlüssel während der FileVault 2-Verschlüsselung für den Endbenutzer ausgeblendet. 

Der Gerätebenutzer kann den persönlichen Wiederherstellungsschlüssel eines verschlüsselten macOS-Geräts anzeigen, indem dieser zu einem der folgenden Orte navigiert und auf *Wiederherstellungsschlüssel abrufen* für das macOS-Gerät klickt: 

- Die Unternehmensportal-App für iOS oder iPadOS
- Die Intune-App
- Die Unternehmensportalwebsite
- Die Unternehmensportal-App für Android

#### <a name="support-for-smime-signing-and-encryption-certificates-with-outlook-on-android-fully-managed--5896415-----"></a>Unterstützung für S/MIME-Signatur- und -Verschlüsselungszertifikate mit Outlook unter Android (vollständig verwaltet)<!--5896415   -->
Sie können ab sofort Zertifikate für die S/MIME-Signatur und -Verschlüsselung mit Outlook auf Geräten verwenden, auf denen ein vollständig verwaltetes Android Enterprise-Betriebssystem ausgeführt wird.

Dadurch wird die im letzten Monat für andere Android-Versionen hinzugefügte Unterstützung (Unterstützung für S/MIME-Signatur- und -Verschlüsselungszertifikate mit Outlook unter Android) ergänzt. Sie können diese Zertifikate über importierte SCEP- und PKCS-Zertifikatprofile bereitstellen.

Weitere Informationen zu dieser Unterstützung finden Sie in der Exchange-Dokumentation unter [Vertraulichkeitsbezeichnung und Schutz in Outlook für iOS-und Android-](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/sensitive-labeling-and-protection-outlook-for-ios-android).

#### <a name="add-a-link-to-your-company-portal-support-website-to-emails-for-noncompliance---7225498------"></a>Hinzufügen eines Links zur Support-Website Ihres Unternehmensportals zu E-Mails bei Nichtkonformität<!-- 7225498    -->
Wenn Sie eine [Vorlage für Benachrichtigungen](../protect/actions-for-noncompliance.md#create-a-notification-message-template) für das Senden von E-Mail-Benachrichtigungen bei Nichtkonformität konfigurieren, können Sie die neue Einstellung **Link zur Unternehmensportalwebsite** verwenden, um automatisch einen Link zur Website des Unternehmensportals einzufügen. Wenn Sie diese Option auf *Aktiviert* festlegen, können Benutzer mit nicht konformen Geräten, die auf Grundlage dieser Vorlage eine E-Mail erhalten, die Website über den Link öffnen, um sich darüber zu informieren, warum ihr Gerät nicht konform ist. 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="licensing"></a>Lizenzierung

#### <a name="admins-no-longer-require-an-intune-license-to-access-microsoft-endpoint-manager-admin-console--1335430---"></a>Administratoren: Keine Intune-Lizenz für den Zugriff auf die Microsoft Endpoint Manager-Administratorkonsole mehr erforderlich<!--1335430 -->
Sie können jetzt eine mandantenweite Umschaltfläche benutzen, die es Administratoren ermöglicht, auch ohne Intune-Lizenz auf die Microsoft Endpoint Manager-Administratorkonsole und die APIs für Abfragediagramme zuzugreifen. Sobald Sie jedoch festgelegt haben, dass keine Lizenz erforderlich ist, können Sie den Vorgang nicht mehr rückgängig machen. 



<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="scripts"></a>Skripts 

#### <a name="availability-of-shell-scripts-on-macos-devices---7134839----"></a>Verfügbarkeit von Shellskripts auf macOS-Geräten<!-- 7134839  -->
Shellskripts für macOS-Geräte sind jetzt für Government Cloud-Kunden und Kunden in China verfügbar. Weitere Informationen zu Shellskripts finden Sie unter [Verwenden von Shellskripts auf macOS-Geräten in Intune](../apps/macos-shell-scripts.md).



<!-- ########################## -->
## <a name="week-of-june-8-2020"></a>Woche ab 8. Juni 2020   

### <a name="app-management"></a>App-Verwaltung  

#### <a name="updates-to-informational-screen-in-company-portal-for-iosipados---7032452---"></a>Updates für den Informationsbildschirm im Unternehmensportal für iOS und iPadOS <!--7032452 -->
Auf dem Informationsbildschirm für iOS und iPadOS im Unternehmensportal wird jetzt besser erklärt, welche Einblicke und Möglichkeiten Administratoren für Geräte zur Verfügung stehen. Diese Erläuterungen werden nur für unternehmenseigene Geräte angezeigt. Nur der angezeigte Text wurde aktualisiert, nicht die Einblicke und Möglichkeiten, die Administratoren für Benutzergeräte zur Verfügung stehen. Um die aktualisierten Bildschirme anzuzeigen, gehen Sie zu [Updates der Benutzeroberfläche für Endbenutzer-Apps von Intune](./whats-new-app-ui.md).

#### <a name="updated-android-app-conditional-launch-end-user-experience---5736084---"></a>Aktualisierte Endbenutzerbedienung für den bedingten Start von Android-Apps<!-- 5736084 -->
Die Änderungen im Release 2006 des Unternehmensportals für Android bauen auf den Updates des Releases 2005 auf. Im Release 2005 haben wir ein Update eingeführt, durch das Endbenutzern von Android-Geräten eine ganze Meldungsseite angezeigt wurde, wenn eine Warnung, Blockierung oder Löschung durch eine App-Schutzrichtlinie ausgelöst wurde. Auf dieser werden auch die Ursache und Schritte zur Problembehebung angezeigt. Im Release 2006 werden Benutzer, die Android-Apps mit zugewiesener App-Schutzrichtlinie zum ersten Mal benutzen, durch den Ablauf zur Behandlung der Probleme geführt, die zur Blockierung des App-Zugriffs führen. 

<!-- ########################## -->
## <a name="week-of-may-25-2020"></a>Woche vom 25. Mai 2020

### <a name="app-management"></a>App-Verwaltung

#### <a name="windows-32-bit-x86-apps-on-arm64-devices---5477661---"></a>Windows-32-Bit-Apps (x86) auf ARM64-Geräten<!-- 5477661 -->
Windows-32-Bit-Apps (x86), die für ARM64-Geräte bereitgestellt werden können, werden jetzt im Unternehmensportal angezeigt. Weitere Informationen zu Windows-32-Bit-Apps finden Sie unter [Win32-App-Verwaltung](../apps/apps-win32-app-management.md).

#### <a name="windows-company-portal-app-icon---7114635---"></a>Symbol für Windows-Unternehmensportal-App<!-- 7114635 -->
Das Symbol für die Windows-Unternehmensportal-App wurde aktualisiert. Weitere Informationen zum Unternehmensportal finden Sie unter [Anpassen von Intune-Unternehmensportal-Apps, der Unternehmensportal-Website und der Intune-App](../apps/company-portal-app.md).


<!-- ########################## -->
## <a name="week-of-may-18-2020"></a>Woche vom 18. Mai 2020

### <a name="app-management"></a>App-Verwaltung  

#### <a name="update-to-icons-in-company-portal-app-for-iosipados-and-macos--6057697---"></a>Aktualisierung von Symbolen in der Unternehmensportal-App für iOS/iPadOS und macOS<!--6057697 -->
Wir haben die Symbole im Unternehmensportal aktualisiert, um ihnen ein moderneres Erscheinungsbild zu geben, das auch auf Geräten mit zwei Bildschirmen unterstützt wird und mit dem Fluent Design System von Microsoft in Einklang steht. Um sich die aktualisierten Symbole anzusehen, wechseln Sie zu [Updates der Benutzeroberfläche für Endbenutzer-Apps von Intune](./whats-new-app-ui.md). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Gerätesicherheit

#### <a name="use-endpoint-detection-and-response-policy-to-onboard-devices-to-defender-atp---7130165----"></a>Verwenden der Richtlinie für Endpunkterkennung und -antwort zum Onboarding von Geräten in Defender ATP<!-- 7130165  -->

Verwenden Sie die [Richtlinie für die Endpunkterkennung und -antwort](../protect/endpoint-security-edr-policy.md) im Rahmen der Endpunktsicherheit, um Geräte für Ihre Bereitstellung von Microsoft Defender Advanced Threat Protection (Defender ATP) zu integrieren und zu konfigurieren. Das Feature „Endpunkterkennung und -antwort“ unterstützt eine Richtlinie für Windows-Geräte, die von Intune verwaltet werden (MDM), sowie eine separate Richtlinie für Windows-Geräte, die über Configuration Manager verwaltet werden. 

Um die Richtlinie für Configuration Manager-Geräte zu verwenden, müssen Sie [Configuration Manager zur Unterstützung der Richtlinie für Endpunkterkennung und -antwort einrichten](../protect/endpoint-security-edr-policy.md#set-up-configuration-manager-to-support-edr-policy). Die Einrichtung umfasst folgende Schritte:

- Konfigurieren Sie Ihre Configuration Manager-Instanz für die *Mandantenanfügung*.
- Installieren Sie ein konsoleninternes Update für Configuration Manager, um die Unterstützung der Richtlinien für Endpunkterkennung und -antwort zu aktivieren. Dieses Update gilt nur für Hierarchien mit aktivierter *Mandantenanfügung*.
- Synchronisieren Sie Ihre Gerätesammlung aus Ihrer Hierarchie mit dem Microsoft Endpoint Manager Admin Center.


<!-- ########################## -->
## <a name="week-of-may-11-2020-2005-service-release"></a>Woche vom 11. Mai 2020 (Dienstrelease 2005)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>App-Verwaltung

#### <a name="customize-self-service-device-actions-in-the-company-portal--4393379---"></a>Anpassen von Self-Service-Geräteaktionen für Benutzer im Unternehmensportal<!--4393379 -->
Sie können die verfügbaren Self-Service-Geräteaktionen anpassen, die Endbenutzern in der App und auf der Website des Unternehmensportals angezeigt werden. Damit nicht beabsichtigte Geräteaktionen vermieden werden, können Sie Einstellungen für die Unternehmensportal-App konfigurieren. Klicken Sie dazu auf **Mandantenverwaltung** > **Anpassung**. Die folgenden Aktionen sind verfügbar:
- Schaltfläche **Entfernen** auf unternehmenseigenen Windows-Geräten ausblenden
- Schaltfläche **Zurücksetzen** auf unternehmenseigenen Windows-Geräten ausblenden
- Schaltfläche **Zurücksetzen** auf unternehmenseigenen iOS-Geräten ausblenden
- Schaltfläche **Entfernen** auf unternehmenseigenen iOS-Geräten ausblenden
Weitere Informationen erhalten Sie unter [Self-Service-Geräteaktionen für Benutzer im Unternehmensportal](../apps/company-portal-app.md#user-self-service-device-actions-from-the-company-portal).

#### <a name="auto-update-vpp-available-apps---3640511----"></a>Automatische Aktualisierung verfügbarer VPP-Apps<!-- 3640511  -->
Als verfügbare VPP-Apps (Volume Purchase Program) veröffentlichte Apps werden automatisch aktualisiert, wenn die Option **Automatische App-Updates** für das VPP-Token aktiviert ist. Bisher wurden verfügbare VPP-Apps nicht automatisch aktualisiert. Stattdessen mussten Endbenutzer zum Unternehmensportal wechseln und die App neu installieren, wenn eine neue Version zur Verfügung stand. Für erforderliche Apps werden weiterhin automatische Updates unterstützt.




#### <a name="android-company-portal-user-experience---5736084----"></a>Benutzeroberfläche des Android-Unternehmensportals<!-- 5736084  -->
In der 2005-Version des Android-Unternehmensportals wird Endbenutzern von Android-Geräten, die eine Warnungs-, Blockierungs- oder Zurücksetzungsmeldung über eine App-Schutzrichtlinie erhalten, eine neue Benutzeroberfläche angezeigt. Anstelle der aktuellen Dialogbenutzeroberfläche wird den Endbenutzern eine ganzseitige Meldung angezeigt, in der die Ursachen für die Warnung, Blockierung oder Zurücksetzung sowie die Schritte zur Problembeseitigung beschrieben werden. Weitere Informationen finden Sie unter [Benutzeroberfläche zum App-Schutz für Android-Geräte](../apps/app-protection-policy.md#app-protection-experience-for-android-devices) und [Einstellungen für App-Schutzrichtlinien in Microsoft Intune](../apps/app-protection-policy-settings-android.md).

#### <a name="support-for-multiple-accounts-in-company-portal-for-macos---5779449----"></a>Unterstützung für mehrere Konten im Unternehmensportal für macOS<!-- 5779449  -->
Das Unternehmensportal auf macOS-Geräten speichert Benutzerkonten jetzt zwischen, wodurch die Anmeldung vereinfacht wird. Benutzer müssen sich nicht länger bei jedem Start der Anwendung beim Unternehmensportal anmelden. Darüber hinaus zeigt das Unternehmensportal eine Kontoauswahl an, wenn mehrere Benutzerkonten zwischengespeichert wurden, sodass die Benutzer nicht ihren Benutzernamen eingeben müssen. 

#### <a name="newly-available-protected-apps---7060934-----"></a>Neu verfügbare geschützte Apps<!-- 7060934   -->
Ab sofort sind die folgenden geschützten Apps verfügbar:
- Board Papers
- Breezy for Intune
- Hearsay Relate for Intune
- ISEC7 Mobile Exchange Delegate for Intune
- Lexmark for Intune
- Meetio Enterprise
- Microsoft Whiteboard
- Now® Mobile – Intune
- Qlik Sense Mobile 
- ServiceNow® Agent – Intune
- ServiceNow® Onboarding – Intune
- Smartcrypt for Intune
- Tact for Intune
- Zero – email for attorneys

Weitere Informationen zu geschützten Apps finden Sie unter [Durch Microsoft Intune geschützte Apps](../apps/apps-supported-intune-apps.md).

#### <a name="search-the-intune-docs-from-the-company-portal---1736480-----"></a>Suche in der Intune-Dokumentation aus dem Unternehmensportal<!-- 1736480   -->
Sie können ab sofort direkt aus der Unternehmensportal für macOS-App in der Intune-Dokumentation suchen. Wählen Sie in der Menüleiste **Hilfe** > **Suche** aus, und geben Sie die Schlüsselwörter für Ihre Suche ein, um schnell Antworten auf Ihre Fragen zu finden.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Gerätekonfiguration

#### <a name="improvements-to-oemconfig-support-for-zebra-technologies-devices---4184154---"></a>Verbesserungen an der OEMConfig-Unterstützung für Zebra Technologies-Geräte<!-- 4184154 -->
Intune bietet vollständige Unterstützung für alle über Zebra OEMConfig bereitgestellten Features. Kunden, die Zebra Technologies-Geräte mit Android Enterprise und OEMConfig verwalten, können mehrere OEMConfig-Profile auf einem Gerät bereitstellen. Kunden können außerdem umfangreiche Berichte zum Status ihrer Zebra OEMConfig-Profile anzeigen.

Weitere Informationen finden Sie unter [Bereitstellen mehrerer OEMConfig-Profile für Zebra-Geräte in Microsoft Intune](../configuration/oemconfig-zebra-android-devices.md).

Für andere OEMs gelten keine Änderungen in Bezug auf das OEMConfig-Verhalten.

Gilt für:
- Android Enterprise
- Zebra Technologies-Geräte, die OEMConfig unterstützen. Wenden Sie sich zwecks spezifischer Details zur Unterstützung an Zebra.

#### <a name="configure-system-extensions-on-macos-devices---6255624---"></a>Konfigurieren von Systemerweiterungen auf macOS-Geräten<!-- 6255624 -->
Auf macOS-Geräten können Sie ein Kernelerweiterungsprofil erstellen, um Einstellungen auf Kernelebene zu konfigurieren (**Geräte** > **Konfigurationsprofile** > **macOS** für die Plattform > **Kernelerweiterungen** für das Profil). Apple wird Kernelerweiterungen als veraltet einstufen und in einer zukünftigen Version durch Systemerweiterungen ersetzen.

Systemerweiterungen werden im Benutzerbereich ausgeführt und haben keinen Zugriff auf den Kernel. Das Ziel besteht darin, die Sicherheit zu erhöhen und dem Benutzer mehr Kontrolle zu ermöglichen, während gleichzeitig die Angriffe auf Kernelebene begrenzt werden. Sowohl Kernel- als auch Systemerweiterungen ermöglichen den Benutzern das Installieren von App-Erweiterungen, die die nativen Funktionen des Betriebssystems erweitern.

In Intune können Sie sowohl Kernelerweiterungen als auch Systemerweiterungen konfigurieren (**Geräte** > **Konfigurationsprofile** > **macOS** für die Plattform > **Kernelerweiterungen** für das Profil). Kernelerweiterungen gelten für Version 10.13.2 und höher. Systemerweiterungen gelten für Version 10.15 und höher. Für macOS 10.15 bis macOS 10.15.4 können Kernelerweiterungen und Systemerweiterungen parallel ausgeführt werden. 

Weitere Informationen zu diesen Erweiterungen auf macOS-Geräten finden Sie unter [Hinzufügen von macOS-Erweiterungen](../configuration/kernel-extensions-overview-macos.md).

Gilt für:
- macOS 10.15 und neuer

#### <a name="configure-app-and-process-privacy-preferences-on-macos-devices---2934232-----"></a>Konfigurieren von Datenschutzeinstellungen für Apps und Prozesse auf macOS-Geräten<!-- 2934232   --> 
Apple hat im Rahmen der Veröffentlichung von macOS Catalina 10.15 die Sicherheits- und Privatsphäreneinstellungen erweitert. Standardmäßig können Anwendungen und Prozesse ohne Zustimmung des Benutzers nicht auf bestimmte Daten zugreifen. Wenn Benutzer nicht ihre Einwilligung geben, funktionieren die Anwendungen und Prozesse möglicherweise nicht mehr. Intune fügt Unterstützung für Einstellungen hinzu, mit denen IT-Administratoren den Zugriff auf Daten im Namen von Endbenutzern auf Geräten, auf denen macOS 10.14 oder höher ausgeführt wird, zulassen oder nicht zulassen können. Mit diesen Einstellungen wird sichergestellt, dass Anwendungen und Prozesse weiterhin ordnungsgemäß funktionieren und die Anzahl der Eingabeaufforderungen verringert wird. 

Weitere Informationen zu den Einstellungen, die Sie verwalten können, finden Sie unter [macOS-Datenschutzeinstellungen](../configuration/device-restrictions-macos.md#privacy-preferences).

Gilt für:
- macOS 10.14 und höher

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Geräteregistrierung

#### <a name="enrollment-restrictions-support-scope-tags--4209550----"></a>Registrierungsbeschränkungen unterstützen Bereichstags<!--4209550  -->
Sie können ab sofort Registrierungsbeschränkungen zu Bereichstags hinzufügen. Wechseln Sie hierzu im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) zu  > **Geräte** > **Registrierungsbeschränkungen** > **Einschränkung erstellen**. Wenn Sie eine Beschränkung des gewünschten Typs erstellen, wird die Seite **Bereichstags** angezeigt. Weitere Informationen finden Sie unter [Festlegen von Registrierungseinschränkungen](../enrollment/enrollment-restrictions-set.md).

#### <a name="autopilot-support-for-hololens-2-devices--6305220----"></a>Autopilot-Unterstützung für Hololens 2-Geräte<!--6305220  -->
Windows Autopilot unterstützt ab sofort HoloLens 2-Geräte. Weitere Informationen zur Verwendung von Autopilot für HoloLens finden Sie unter [Windows Autopilot für HoloLens 2](https://docs.microsoft.com/hololens/hololens2-autopilot).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Geräteverwaltung

#### <a name="use-sync-remote-action-in-bulk-for-ios--6440956--idmiss--"></a>Verwenden der Remoteaktion zur Synchronisierung als Massenvorgang für iOS<!--6440956  idmiss-->
Sie können die Remoteaktion zur Synchronisierung jetzt in einem Arbeitsschritt für bis zu 100 iOS-Geräte gleichzeitig ausführen. Navigieren Sie zu [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Geräte** > **Alle Geräte** > **Massengeräteaktionen**, um dieses Feature anzuzeigen. 

#### <a name="automated-device-sync-interval-down-to-12-hours--3077535----"></a>Herabsetzung es Intervalls für die Gerätesynchronisierung auf 12 Stunden<!--3077535  -->
Für die automatische Geräteregistrierung von Apple wurde das Intervall für die automatische Gerätesynchronisierung zwischen Intune und Apple Business Manager von 24 Stunden auf 12 Stunden abgesenkt. Weitere Informationen zur Synchronisierung finden Sie unter [Synchronisieren verwalteter Geräte](../enrollment/device-enrollment-program-enroll-ios.md#sync-managed-devices).


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Gerätesicherheit

#### <a name="derived-credentials-support-for-disa-purebred-on-android-devices---6939073-------"></a>Unterstützung abgeleiteter Anmeldeinformationen für DISA Purebred auf Android-Geräten<!-- 6939073     -->
Sie können ab sofort *DISA Purebred* als Anbieter für [abgeleitete Anmeldeinformationen](../protect/derived-credentials.md) für vollständig verwaltete Android Enterprise-Geräte verwenden. Die Unterstützung umfasst das Abrufen abgeleiteter Anmeldeinformationen für DISA Purebred. Sie können abgeleitete Anmeldeinformationen für die App-Authentifizierung, WLAN-, VPN- oder S/MIME-Signaturen und/oder -Verschlüsselung für Apps verwenden, die dies unterstützen. 

#### <a name="send-push-notifications-as-an-action-for-noncompliance----1733150-----"></a>Senden von Pushbenachrichtigungen als Aktion bei Nichtkonformität <!-- 1733150   -->
Sie können jetzt eine [Aktion bei Nichtkonformität](../protect/actions-for-noncompliance.md#available-actions-for-noncompliance) konfigurieren, die eine Pushbenachrichtigung an einen Benutzer sendet, wenn dessen Gerät die Bedingungen einer Konformitätsrichtlinie nicht erfüllt. Die neue Aktion heißt **Pushbenachrichtigung an Benutzer senden** und wird auf Android- und iOS-Geräten unterstützt.

Wenn Benutzer die Pushbenachrichtigung auf ihrem Gerät auswählen, wird entweder das Unternehmensportal oder die Intune-App geöffnet, um Details zur Nichtkonformität anzuzeigen.

#### <a name="endpoint-security-content-and-new-features---5720009-5892558-7130145-5653324-7140602----"></a>Inhalte zur Endpunktsicherheit und neue Features<!-- 5720009 5892558, 7130145, 5653324, 7140602  -->

Ab sofort steht eine Dokumentation zur [Endpunktsicherheit](../protect/endpoint-security.md) in Intune zur Verfügung. Der Knoten „Endpunktsicherheit“ im Microsoft Endpoint Manager Admin Center bietet folgende Möglichkeiten:

- Erstellen und Bereitstellen gezielter Sicherheitsrichtlinien für Ihre verwalteten Geräte
- Konfigurieren der Integration in Microsoft Defender Advanced Threat Protection und Verwalten von Sicherheitsaufgaben zum Entschärfen von Risiken für gefährdete Geräte nach Identifizierung durch Ihr ATP-Team
- Konfigurieren von Sicherheitsbaselines
- Verwalten von Richtlinien für Gerätekonformität und bedingten Zugriff
- Anzeigen des Konformitätsstatus für all Ihre Geräte – sowohl für Intune als auch für Configuration Manager –, wenn Configuration Manager für die Clientanfügung konfiguriert ist.

Zusätzlich zur Verfügbarkeit der Inhalte zur Endpunktsicherheit werden in diesem Monat die folgenden neuen Features bereitgestellt:

- Die [**Richtlinien zur Endpunktsicherheit**](../protect/endpoint-security-policy.md) **befinden sich nicht mehr in der** ***Vorschau*** und können als *allgemein verfügbare Features* ab sofort in Produktionsumgebungen eingesetzt werden. Es gelten jedoch zwei Ausnahmen:

  - In einer *öffentlichen Vorschau* können Sie das [**Microsoft Defender Firewall**-Profil](../protect/endpoint-security-firewall-policy.md#firewall-profiles) für die Windows 10-Firewallrichtlinie verwenden. Mit jeder Instanz dieses Profils können Sie bis zu 150 Firewallregeln zur Ergänzung Ihrer Microsoft Defender Firewall-Profile konfigurieren. 
  - Die Sicherheitsrichtlinie zum Kontoschutz verbleibt in der Vorschau. 

- Sie können ab sofort [**ein Duplikat der Richtlinien zur Endpunktsicherheit erstellen**](../protect/endpoint-security-policy.md#duplicate-a-policy). Für Duplikate wird die Einstellungskonfiguration der ursprünglichen Richtlinie beibehalten, die Richtlinie erhält jedoch einen neuen Namen. Die neue Richtlinieninstanz umfasst keine Zuweisungen zu Gruppen. Diese müssen Sie durch Bearbeitung der neuen Richtlinieninstanz hinzufügen. Sie können Richtlinien des folgenden Typs duplizieren:
  - Antivirus
  - Datenträgerverschlüsselung
  - Firewall
  - Endpunkterkennung und -antwort
  - Verringerung der Angriffsfläche
  - Kontoschutz

- Ab sofort ist es möglich, [**ein Duplikat einer Sicherheitsbaseline zu erstellen**](../protect/security-baselines.md#duplicate-a-security-baseline). Für Duplikate wird die Einstellungskonfiguration der ursprünglichen Baseline beibehalten, die Baseline erhält jedoch einen neuen Namen. Die neue Baseline-Instanz umfasst keine Zuweisungen zu Gruppen. Diese müssen Sie durch Bearbeitung der neuen Baseline-Instanz hinzufügen.

- Für die Antivirusrichtlinie im Rahmen der Endpunktsicherheit ist ein neuer Bericht verfügbar: [**Fehlerhafte Windows 10-Endpunkte**](../protect/endpoint-security-antivirus-policy.md#windows-10-unhealthy-endpoints). Dieser Bericht ist eine neue Seite, die Sie bei der Anzeige der Antivirusrichtlinie im Rahmen der Endpunktsicherheit auswählen können. Der Bericht zeigt den Antivirusstatus Ihrer MDM-verwalteten Windows 10-Geräte an.  

#### <a name="support-for-smime-signing-and-encryption-certificates-with-outlook-on-android---7207474----"></a>Unterstützung für S/MIME-Signatur- und Verschlüsselungszertifikate mit Outlook unter Android<!-- 7207474  -->
Sie können ab sofort Zertifikate für S/MIME-Signatur und Verschlüsselung mit Outlook unter Android nutzen. Dank dieser Unterstützung können Sie diese Zertifikate über importierte SCEP-, PKCS- und PKCS-Zertifikatprofile bereitstellen. Folgende Android-Plattformen werden unterstützt:

- Android Enterprise: Arbeitsprofil
- Android-Geräteadministrator

Die Unterstützung für vollständig verwaltete Android Enterprise-Geräte folgt in Kürze.

Weitere Informationen zu dieser Unterstützung finden Sie in der Exchange-Dokumentation unter [Vertraulichkeitsbezeichnung und Schutz in Outlook für iOS-und Android-](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/sensitive-labeling-and-protection-outlook-for-ios-android).


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Überwachung und Problembehandlung

#### <a name="device-reports-ui-update---6269408---"></a>Aktualisierte Benutzeroberfläche für Geräteberichte<!-- 6269408 -->
Der Bereich mit der Berichtsübersicht umfasst jetzt die Registerkarten **Zusammenfassung** und **Berichte**. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Berichte**, und wählen Sie dann die Registerkarte **Berichte** aus, um die verfügbaren Berichtstypen anzuzeigen. Weitere Informationen finden Sie unter [Intune-Berichte](../fundamentals/reports.md).


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="scripting"></a>Skripterstellung

#### <a name="macos-script-support---6376978----"></a>macOS-Skriptunterstützung<!-- 6376978  -->
Die Skriptunterstützung für macOS ist jetzt allgemein verfügbar. Darüber hinaus wurde Unterstützung für benutzerseitig zugewiesene Skripts und für macOS-Geräte hinzugefügt, die über die automatische Geräteregistrierung von Apple (vormals Programm zur Geräteregistrierung) registriert wurden. Weitere Informationen finden Sie unter [Verwenden von Shellskripts auf macOS-Geräten in Intune](../apps/macos-shell-scripts.md).


<!-- ########################## -->
## <a name="week-of-may-4-2020"></a>Woche vom 4. Mai 2020  

### <a name="company-portal-for-android-guides-users-to-get-apps-after-work-profile-enrollment----6103999---"></a>Benutzeranleitung zum Abrufen von Apps im Unternehmensportal für Android nach der Arbeitsprofilregistrierung <!-- 6103999 -->
Wir haben die In-App-Anleitungen im Unternehmensportal verbessert, um Benutzern das Auffinden und Installieren von Apps zu erleichtern. Nach der Registrierung in der Arbeitsprofilverwaltung werden Benutzer in einer Meldung darüber informiert, dass sie vorgeschlagene Apps in der Google Play-Version mit Badge finden. Der letzte Schritt von [Registrieren eines Geräts mit dem Android-Profil](../user-help/enroll-device-android-work-profile.md) wurde aktualisiert, um die neue Meldung anzuzeigen. Benutzern wird außerdem im Unternehmensportal-Drawer auf der linken Seite ein Link **Apps abrufen** angezeigt. Um Platz für diese neuen und verbesserten Benutzerfunktionen zu schaffen, wurde die Registerkarte **APPS** entfernt. Um die aktualisierten Bildschirme anzuzeigen, gehen Sie zu [Updates der Benutzeroberfläche für Endbenutzer-Apps von Intune](./whats-new-app-ui.md). 

<!-- ########################## -->
## <a name="week-of-april-20-2020"></a>Woche vom 20. April 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Geräteverwaltung

#### <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions---6317104-cm3555758----"></a>Anfügen von Mandanten in Microsoft Endpoint Manager: Gerätesynchronisierung und Geräteaktionen<!-- 6317104, CM3555758  -->
Microsoft Endpoint Manager vereint Configuration Manager und Intune in einer einzigen Konsole. Ab Configuration Manager 2002 können Sie Ihre Configuration Manager-Geräte in den Clouddienst hochladen und Aktionen für diese über das Admin Center durchführen. Weitere Informationen finden Sie unter [Anfügen von Mandanten in Microsoft Endpoint Manager: Gerätesynchronisierung und Geräteaktionen](../../configmgr/tenant-attach/device-sync-actions.md). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>App-Verwaltung

#### <a name="microsoft-office-365-proplus-rename---6368143---"></a>Umbenennung von Microsoft Office 365 ProPlus<!-- 6368143 -->
Microsoft Office 365 ProPlus wird in **Microsoft 365 Apps for Enterprise** umbenannt. Weitere Informationen finden Sie unter [Namensänderung für Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). In unserer Dokumentation wird üblicherweise Microsoft 365-Apps verwendet. Im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) finden Sie die Apps-Suite, indem Sie auf **Apps** > **Windows** > **Hinzufügen** klicken. Weitere Informationen zum Hinzufügen von Apps finden Sie unter [Hinzufügen von Apps zu Microsoft Intune](../apps/apps-add.md).

<!-- ########################## -->
## <a name="week-of-april-13-2020-2004-service-release"></a>Woche vom 13. April 2020 (2004 Dienstrelease)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>App-Verwaltung

#### <a name="manage-smime-settings-for-outlook-on-android-enterprise-devices---6517085-----"></a>Verwalten von S/MIME-Einstellungen für Outlook auf Android Enterprise-Geräten<!-- 6517085   -->
Sie können App-Konfigurationsrichtlinien zum Verwalten der S/MIME-Einstellung für Outlook auf Geräten mit Android Enterprise verwenden. Außerdem können Sie festlegen, ob Gerätebenutzer S/MIME in den Outlook-Einstellungen aktivieren oder deaktivieren dürfen. Navigieren Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) zu **Apps** > **App-Konfigurationsrichtlinien** > **Hinzufügen** > **Verwaltete Geräte**, um App-Konfigurationsrichtlinien für Android zu verwenden. Weitere Informationen zum Konfigurieren von Einstellungen für Outlook finden Sie unter [Microsoft Outlook-Konfigurationseinstellungen](../apps/app-configuration-policies-outlook.md).

#### <a name="pre-release-testing-for-managed-google-play-apps---2681933----"></a>Pre-Release-Tests für verwaltete Google Play-Apps<!-- 2681933  -->
Organisationen, die [Tracks für geschlossene Tests von Google Play für Pre-Release-Tests von Apps](https://support.google.com/googleplay/android-developer/answer/3131213) verwenden, können diese Tracks mit Intune verwalten. Sie können Apps selektiv zuweisen, die in den Präproduktionstracks für Pilotgruppen von Google Play veröffentlicht werden, um Tests durchzuführen. In Intune wird außerdem angezeigt, ob eine App über einen veröffentlichten Präproduktionsbuild in einem Testtrack verfügt. Sie können diesen Track auch AAD-Benutzer- oder Gerätegruppen zuweisen. Dieses Feature ist für alle unserer derzeit unterstützten Android Enterprise-Szenarios verfügbar (Arbeitsprofil, vollständig verwaltet und dediziert). Sie können eine Managed Google Play-App im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) hinzufügen, indem Sie auf **Apps** > **Android** > **Hinzufügen** klicken. Weitere Informationen finden Sie unter [Arbeiten mit Managed Google Play-Tracks für geschlossene Tests](../apps/apps-add-android-for-work.md#working-with-managed-google-play-closed-testing-tracks).

#### <a name="microsoft-teams-is-now-included-in-the-office-365-suite-for-macos---5903936----"></a>Microsoft Teams ist nun in der Office 365 Suite für macOS enthalten<!-- 5903936  -->
Benutzer, denen Microsoft Office für macOS in Microsoft Endpoint Manager zugewiesen ist, erhalten nun Microsoft Teams zusätzlich zu den vorhandenen Microsoft Office-Apps (Word, Excel, PowerPoint, Outlook und OneNote). Intune erkennt die vorhandenen Mac-Geräte, auf denen die anderen Office für macOS-Apps installiert sind, und versucht, Microsoft Teams beim nächsten Check-In des Geräts bei Intune zu installieren. Im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) finden Sie die **Office 365 Suite** für macOS, indem Sie auf **Apps** > **macOS** > **Hinzufügen** klicken. Weitere Informationen finden Sie unter [Zuweisen von Office 365 zu macOS-Geräten mit Microsoft Intune](../apps/apps-add-office365-macos.md).

#### <a name="update-to-android-app-configuration-policies---6113334----"></a>Update der Richtlinien zur Konfiguration von Android-Apps<!-- 6113334  -->
Die Konfigurationsrichtlinien für Android-Apps wurden aktualisiert, damit Administrator den Gerätebereitstellungstyp auswählen können, bevor sie ein App-Konfigurationsprofil erstellen. Die Funktionalität wird für Zertifikatprofile hinzugefügt, die auf dem Registrierungstyp basieren (Arbeitsprofil oder Gerätebesitzer).  Dieses Update bietet Folgendes:

1. Wenn ein neues Profil erstellt und der Typ „Arbeitsprofil und Gerätebesitzerprofil“ ausgewählt wird, können Sie kein Zertifikatprofil mit der App-Konfigurationsrichtlinie zuordnen.
2. Wenn ein neues Profil erstellt und der Typ „Arbeitsprofil und Gerätebesitzerprofil“ ausgewählt wird, können Arbeitsprofil-Zertifikatrichtlinien verwendet werden, die in der Gerätekonfiguration erstellt wurden.
3. Wenn ein neues Profil erstellt und der Typ „Nur Gerätebesitzer“ ausgewählt wird, können Gerätebesitzer-Zertifikatrichtlinien verwendet werden, die in der Gerätekonfiguration erstellt wurden. 

> [!IMPORTANT]
> Vorhandene Richtlinien, die vor dem Release dieses Features (April 2020 Release – 2004) erstellt wurden und denen keine Zertifikatprofile zugeordnet ist, verwenden standardmäßig den Geräteregistrierungstyp „Arbeitsprofil und Gerätebesitzerprofil“. Vorhandene Richtlinien, die vor dem Release dieses Features erstellt wurden und denen Zertifikatprofile zugeordnet sind, verwenden zudem standardmäßig den Geräteregistrierungstyp „Nur Arbeitsprofil“.

Außerdem werden E-Mail-Konfigurationsprofile für Gmail und Nine hinzugefügt, die für die Registrierungstypen „Arbeitsprofil“ und „Gerätebesitzer“ verwendet werden können. Außerdem können Zertifikatprofile für beide E-Mail-Konfigurationstypen verwendet werden.  Alle Gmail- oder Nine-Richtlinien, die Sie in der Gerätekonfiguration für Arbeitsprofile erstellt haben, gelten weiterhin für das Gerät und müssen nicht in App-Konfigurationsrichtlinien verlagert werden.

Im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) finden Sie App-Konfigurationsrichtlinien unter **Apps** > **App-Konfigurationsrichtlinien**. Weitere Informationen über App-Konfigurationsrichtlinien finden Sie unter [App-Konfigurationsrichtlinien für Microsoft Intune](../apps/app-configuration-policies-overview.md).

#### <a name="push-notification-when-device-ownership-type-is-changed---5575875---"></a>Pushbenachrichtigung bei Änderungen am Gerätebesitzertyp<!-- 5575875 -->
Sie können eine Pushbenachrichtigung konfigurieren, die an Android- und iOS-Unternehmensportalbenutzer gesendet wird, wenn ihr Gerätebesitzertyp von „Persönlich“ in „Unternehmen“ geändert wird. Diese Pushbenachrichtigung ist standardmäßig deaktiviert. Die Einstellung finden Sie im Microsoft Endpoint Manager, indem Sie auf **Mandantenverwaltung** > **Anpassen** klicken. Weitere Informationen dazu, wie sich der Gerätebesitz auf Ihre Endbenutzer auswirkt, finden Sie unter [Ändern des Gerätebesitzes](../enrollment/corporate-identifiers-add.md#change-device-ownership).

#### <a name="group-targeting-support-for-customization-pane---4722837----"></a>Unterstützung von Gruppenzielen im Anpassungsbereich<!-- 4722837  -->
Sie können die Einstellungen im Bereich **Anpassung** auf Benutzergruppen ausrichten. Um diese Einstellungen in Intune zu finden, navigieren Sie zum [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) und wählen **Mandantenverwaltung** > **Anpassung** aus. Weitere Informationen zur Anpassung finden Sie unter [Anpassen der Intune-Unternehmensportal-Apps, der Unternehmensportal-Website und der Intune-App](../apps/company-portal-app.md).


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Gerätekonfiguration

#### <a name="multiple-evaluate-each-connection-attempt-on-demand-vpn-rules-supported-on-ios-ipados-and-macos---6424615----"></a>Mehrere bedarfsgesteuerte VPN-Regeln vom Typ „Jeden Verbindungsversuch auswerten“ werden unter iOS, iPadOS und macOS unterstützt.<!-- 6424615  -->
Die Intune-Benutzererfahrung ermöglicht mehrere bedarfsgesteuerte VPN-Regeln im gleichen VPN-Profil mit der Aktion **Jeden Verbindungsversuch auswerten** anfordern (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **iOS/iPadOS** oder **macOS** für Plattform > **VPN** für Profil > **Automatisches VPN** > **Bedarfsgesteuert**).

Sie hat nur die erste Regel in der Liste eingehalten. Dieses Verhalten ist festgelegt, und Intune wertet alle Regeln in der Liste aus. Jede Regel wird in der Reihenfolge ausgewertet, in der sie in der Liste der bedarfsgesteuerten Regeln angezeigt wird.

> [!NOTE]
> Wenn Sie über vorhandene VPN-Profile verfügen, die diese bedarfsgesteuerten VPN-Regeln verwenden, gilt die Korrektur, wenn Sie das VPN-Profil das nächste Mal ändern. Nehmen Sie z. B. eine geringfügige Änderung vor (ändern Sie beispielsweise den Namen der Verbindung), und speichern Sie dann das Profil.
>
> Wenn Sie SCEP-Zertifikate zur Authentifizierung verwenden, führt diese Änderung dazu, dass die Zertifikate für dieses VPN-Profil neu ausgestellt werden.

Gilt für:
- iOS/iPadOS
- macOS

Weitere Informationen zu VPN-Profilen finden Sie unter [Erstellen von VPN-Profilen](../configuration/vpn-settings-configure.md).

#### <a name="additional-options-in-sso-and-sso-app-extension-profiles-on-iosipados-devices---6504155-----"></a>Zusätzliche Optionen in SSO und SSO-App-Erweiterungsprofile auf iOS/iPadOS-Geräten<!-- 6504155   -->

Auf iOS/iPadOS-Geräten können Sie:
- in SSO-Profilen (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **iOS/iPadOS** (Plattform) > **Gerätefeatures** (Profil) > **Einmaliges Anmelden**) den Kerberos-Prinzipalnamen auf den Namen der Sicherheitskontenverwaltung festlegen. 
- in SSO-App-Erweiterungsprofilen (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **iOS/iPadOS** (Plattform) > **Gerätefeatures** (Profil) > **App-Erweiterung für einmaliges Anmelden**) die Microsoft Azure AD-Erweiterung für iOS/iPadOS mithilfe eines neuen SSO-App-Erweiterungstyps mit weniger Klicks konfigurieren. Sie können die Azure AD-Erweiterung für Geräte im Freigabemodus aktivieren und erweiterungsspezifische Daten an die Erweiterung senden.

Gilt für:
- iOS/iPadOS 13.0 und höher

Weitere Informationen zur Verwendung des einmaligen Anmeldens auf iOS/iPadOS-Geräten finden Sie unter [Übersicht über die App-Erweiterung für einmaliges Anmelden](../configuration/device-features-configure.md#single-sign-on-app-extension) und [Einstellungen für einmaliges Anmelden](../configuration/ios-device-features-settings.md#single-sign-on-app-extension).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Geräteregistrierung

#### <a name="delete-apple-automated-device-enrollment-token-when-default-profile-is-present--6393220---"></a>Löschen des Tokens für die automatische Geräteregistrierung von Apple, wenn das Standardprofil vorhanden ist<!--6393220 -->
Zuvor konnten Sie ein Standardprofil nicht löschen, was bedeutete, dass Sie das ihm zugeordnete Token für die automatische Geräteregistrierung nicht löschen konnten. Jetzt können Sie das Token in folgenden Situationen löschen:
- Dem Token sind keine Geräte zugewiesen.
- Es ist ein Standardprofil vorhanden. Dazu löschen Sie das Standardprofil und dann das zugehörige Token.
Weitere Informationen finden Sie unter [Löschen eines ADE-Tokens aus Intune](../enrollment/device-enrollment-program-enroll-ios.md#delete-an-automated-device-enrollment-token-from-intune).

#### <a name="scaled-up-support-for-apple-automated-device-enrollment-and-apple-configurator-2-devices-profiles-and-tokens--3542402---"></a>Erweiterte Unterstützung für Geräte, Profile und Token der automatischen Geräteregistrierung von Apple und von Apple Configurator 2<!--3542402 -->
Intune unterstützt jetzt bis zu 1000 Registrierungsprofile pro Token, 2000 Token für die automatisierte Geräteregistrierung (früher bekannt als DEP) pro Intune-Konto und 75.000 Geräte pro Token, um verteilte IT-Abteilungen und Organisationen zu unterstützen. Es gibt keine bestimmte Obergrenze für Geräte pro Registrierungsprofil unterhalb der maximalen Anzahl von Geräten pro Token.

Intune unterstützt jetzt bis zu 1000 Apple Configurator 2-Profile.

Weitere Informationen finden Sie unter [Unterstütztes Volume](../enrollment/device-enrollment-program-enroll-ios.md#supported-volume).

#### <a name="all-devices-page-column-entry-changes--6967616---"></a>Änderungen der Spalteneinträge auf der Seite „Alle Geräte“<!--6967616 -->
Auf der Seite **Alle Geräte** haben sich die Einträge für die Spalte **Verwaltet von** geändert:
- *Intune* wird jetzt anstelle von *MDM* angezeigt.
- *Gemeinsam verwaltet* wird jetzt anstelle von *MDM/ConfigMgr-Agent* angezeigt.

Die Exportwerte sind unverändert.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Geräteverwaltung

#### <a name="trusted-platform-manager-tpm-version-information-now-on-device-hardware-page--6224914-idmiss---"></a>TPM-Versionsinformationen (Trusted Platform Manager) befinden sich jetzt auf der Seite „Gerätehardware“.<!--6224914 idmiss -->
Sie können jetzt die TPM-Versionsnummer auf der Hardwareseite eines Geräts anzeigen ([Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Geräte** > Gerät auswählen > **Hardware** > siehe unter **Systemgehäuse**).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Überwachung und Problembehandlung

#### <a name="collect-logs-to-better-troubleshoot-scripts-assigned-to-macos-devices---6359853----"></a>Sammeln von Protokollen zur besseren Problembehandlung bei Skripts, die macOS-Geräten zugeordnet sind<!-- 6359853  -->
Sie können jetzt Protokolle zur verbesserten Problembehandlung bei Skripts sammeln, die macOS-Geräten zugeordnet sind. Sie können Protokolle bis zu 60 MB (komprimiert) oder 25 Dateien sammeln, je nachdem, was zuerst eintritt. Weitere Informationen finden Sie unter [Behandeln von Problemen mit macOS-Shellskriptrichtlinien mithilfe einer Protokollsammlung](../apps/macos-shell-scripts.md#troubleshoot-macos-shell-script-policies-using-log-collection).
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>Sicherheit

#### <a name="derived-credentials-to-provision-android-enterprise-fully-managed-devices-with-certificates--4839592------"></a>Abgeleitete Anmeldeinformationen, um vollständig verwaltete Android Enterprise-Geräte mit Zertifikaten auszustatten<!--4839592    -->
Intune unterstützt jetzt die Verwendung von [abgeleiteten Anmeldeinformationen](../protect/derived-credentials.md) als Authentifizierungsmethode für Android-Geräte. Abgeleitete Anmeldeinformationen sind eine Implementierung der NIST-Standards 800-157 (National Institute of Standards and Technology) für die Bereitstellung von Zertifikaten auf Geräten. Unsere Unterstützung für Android erweitert unsere Unterstützung für Geräte, die iOS/iPadOS ausführen.

Abgeleitete Anmeldeinformationen stützen sich auf die Verwendung einer PIV- (Personal Identity Verification) oder CAC-Karte (Common Access Card), z. B. eine Smartcard. Zum Abrufen von abgeleiteten Anmeldeinformationen für ihr mobiles Gerät beginnen Benutzer in der Microsoft Intune-App und befolgen einen Workflow für die Registrierung, die für den verwendeten Anbieter eindeutig ist. Alle Anbieter haben die Voraussetzung zur Verwendung einer Smartcard auf Computern gemein, um den Anbieter der abgeleiteten Anmeldeinformationen zu authentifizieren. Dieser Anbieter gibt dann ein Zertifikat an das Gerät aus, das von der Smartcard des Benutzers abgeleitet wird.

Sie können abgeleitete Anmeldeinformationen als Authentifizierungsmethode für Gerätekonfigurationsprofile für VPN und WLAN verwenden. Sie können sie auch für die App-Authentifizierung, S/MIME-Signatur und Verschlüsselung für Anwendungen verwenden, die dies unterstützen.

Intune unterstützt jetzt die folgenden Anbieter abgeleiteter Anmeldeinformationen mit Android:
- Entrust Datacard
- Intercede

Ein dritter Anbieter, DISA Purebred, wird in einer zukünftigen Version für Android verfügbar sein.

#### <a name="microsoft-edge-security-baseline-is-now-generally-available--6586139---"></a>Die Microsoft Edge-Sicherheitsbaseline ist jetzt allgemein verfügbar.<!--6586139 -->

Eine neue Version der [Microsoft Edge-Sicherheitsbaseline](../protect/security-baselines.md#available-security-baselines) ist jetzt verfügbar und wird als allgemein verfügbar (GA) veröffentlicht. Die vorherige Microsoft Edge-Baseline befand sich in der Vorschauversion.  Die neue Basisversion ist April 2020 (Microsoft Edge-Version 80 und höher). 

Mit der Veröffentlichung dieser neuen Baseline sind Sie nicht mehr in der Lage, Profile auf Grundlage der vorherigen Baselineversion zu erstellen, aber Sie können weiterhin Profile verwenden, die Sie mit diesen Versionen erstellt haben. Sie haben auch die Möglichkeit, vorhandene Profile zu [aktualisieren, damit Sie die neueste Baselineversion](../protect/security-baselines.md#change-the-baseline-version-for-a-profile) verwenden können. 

<!-- ########################## -->
## <a name="week-of-april-6-2020"></a>Woche vom 6. April 2020

#### <a name="new-shell-script-settings-for-macos-devices---6884363---"></a>Neue Shellskripteinstellungen für macOS-Geräte<!-- 6884363 -->
Wenn Sie Shellskripts für macOS-Geräte konfigurieren, können Sie nun die folgenden neuen Einstellungen konfigurieren: 
- Skriptbenachrichtigungen auf Geräten ausblenden
- Häufigkeit der Skriptausführung
- Maximale Anzahl von Wiederholungsversuchen bei Skriptfehlern

Weitere Informationen finden Sie unter [Verwenden von Shellskripts auf macOS-Geräten in Intune](../apps/macos-shell-scripts.md).

<!-- ########################## -->
## <a name="week-of-march-30-2020"></a>Woche ab 30. März 2020

### <a name="new-url-for-the-microsoft-endpoint-manager-admin-center---3704810---"></a>Neue URL des Microsoft Endpoint Manager Admin Centers<!-- 3704810 -->
Die URL für das Microsoft Endpoint Manager Admin Center (zuvor Microsoft 365-Geräteverwaltung) wurde gemäß der Ankündigung zu Microsoft Endpoint Manager bei der Ignite im letzten Jahr in [https://endpoint.microsoft.com](https://endpoint.microsoft.com) geändert. Die alte Admin Center-URL ([https://devicemanagement.microsoft.com](https://devicemanagement.microsoft.com)) wird weiterhin funktionieren, es wird jedoch empfohlen, dass Sie über die neue URL auf das Microsoft Endpoint Manager Admin Center zugreifen.

Weitere Informationen finden Sie unter [Vereinfachen von IT-Aufgaben mit dem Microsoft Endpoint Manager Admin Center](what-is-device-management.md#simplify-it-tasks-using-the-device-management-admin-center).  


### <a name="app-management"></a>App-Verwaltung  

#### <a name="company-portal-for-ios-supports-landscape-mode--6048329----"></a>Unternehmensportal für iOS zur Unterstützung des Querformats<!--6048329  -->   
Benutzer können jetzt über die Bildschirmausrichtung ihrer Wahl ihre Geräte registrieren, Apps suchen und IT-Support erhalten. Die App erkennt automatisch Bildschirme und passt diese an das Hoch- oder Querformat an, es sei denn, Benutzer sperren den Bildschirm im Hochformat.  

#### <a name="script-support-for-macos-devices-public-preview---4280361----"></a>Skriptunterstützung für macOS-Geräte (Public Preview)<!-- 4280361  -->
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

<!-- ########################## -->
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

#### <a name="optimized-dedicated-device-enrollment----6114580----"></a>Optimierte Registrierung von dedizierten Geräten <!-- 6114580  -->
Wir optimieren die Registrierung von dedizierten Android Enterprise-Geräten und vereinfachen die Anwendung von SCEP-Zertifikaten, die mit einem WLAN verknüpft sind, auf dedizierte Geräte, die vor dem 22. November 2019 registriert wurden. Bei neuen Registrierungen wird die Intune-App weiterhin installiert, aber Endbenutzer können den Schritt **Intune-Agent aktivieren** während der Registrierung nicht mehr ausführen. Die Installation erfolgt automatisch im Hintergrund, und SCEP-Zertifikate, die mit einem WLAN verknüpft sind, können ohne Interaktion durch den Endbenutzer bereitgestellt und festgelegt werden.  

Diese Änderungen werden im Verlauf des März im Rahmen der Bereitstellung des Intune-Dienst-Back-Ends phasenweise eingeführt. Bis Ende ist dieses neue Verhalten in allen Mandanten bereitgestellt. Weitere Informationen finden Sie unter [Support for SCEP certificates in Android Enterprise dedicated devices](https://techcommunity.microsoft.com/t5/intune-customer-success/support-for-scep-certificates-in-android-enterprise-dedicated/ba-p/928147) (Unterstützung für SCEP-Zertifikate auf dedizierten Android Enterprise-Geräten).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Gerätekonfiguration

#### <a name="new-user-experience-when-creating-administrative-templates-on-windows-devices--5096036---"></a>Neue Benutzeroberfläche für die Erstellung von administrativen Vorlagen auf Windows-Geräten<!--5096036 -->
Basierend auf dem Feedback unserer Kunden und im Zuge der Einführung der neuen Vollbildansicht für Azure haben wir die Benutzeroberfläche für Profile für administrative Vorlagen neu erstellt und eine Ordneransicht hinzugefügt. Einstellungen oder vorhandene Profile wurden nicht geändert. Ihre vorhandenen Profile bleiben also unverändert und können in der neuen Ansicht verwendet werden. Sie können weiterhin durch alle Einstellungsoptionen navigieren, indem Sie **Alle Einstellungen** auswählen und die Suche verwenden. Die Strukturansicht ist in „Computerkonfigurationen“ und „Benutzerkonfigurationen“ unterteilt. Die Einstellungen für Windows, Office und Microsoft Edge finden Sie in den jeweiligen Ordnern.  

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
Sie können konfigurieren, ob die Geräteregistrierung im Unternehmensportal auf Android- und iOS-Geräten mit oder ohne Eingabeaufforderungen bzw. nicht für Benutzer verfügbar sein soll. Navigieren Sie zum [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431), und klicken Sie auf **Mandantenverwaltung** > **Anpassung** > **Bearbeiten** > **Geräteregistrierung**, um diese Einstellungen in Intune zu finden.  

Damit die Einstellung „Geräteregistrierung“ unterstützt wird, müssen Endbenutzer über eine der folgenden Unternehmensportalversionen verfügen:
-    Unternehmensportal unter iOS: Version 4.4 oder höher
-    Unternehmensportal unter Android: Version 5.0.4715.0 oder höher

Weitere Informationen zur Anpassung des Unternehmensportals finden Sie unter [Konfigurieren der Microsoft Intune-Unternehmensportal-App](../apps/company-portal-app.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Geräteverwaltung

#### <a name="new-android-report-on-android-devices-overview-page---5435435-----"></a>Neuer Android-Bericht auf der Übersichtsseite für Android-Geräte<!-- 5435435   -->
Wir haben auf der Übersichtsseite für Android-Geräte einen Bericht zur Microsoft Endpoint Manager-Verwaltungskonsole hinzugefügt, der anzeigt, wie viele Android-Geräte in jeder Geräteverwaltungslösung registriert sind. Dieses Diagramm zeigt (wie das gleiche Diagramm in der Azure-Konsole) die Anzahl der Arbeitsprofile, vollständig verwalteten, dedizierten und mit Geräteadministratorregistrierung registrierten Geräte an. Klicken Sie auf **Geräte** > **Android** > **Übersicht**, um den Bericht anzuzeigen.

#### <a name="guide-users-from-android-device-administrator-management-to-work-profile-management--5857738-----"></a>Leitfaden für Benutzer von der Android-Geräteadministratorverwaltung zur Arbeitsprofilverwaltung<!--5857738   -->
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
Im Intune Data Warehouse stehen weitere Gerätebestandseigenschaften zur Verfügung. Die folgenden Eigenschaften werden jetzt über die Betasammlung [devices](../developer/reports-ref-devices.md#devices) verfügbar gemacht:
- `ethernetMacAddress`: Der eindeutige Netzwerkbezeichner dieses Geräts.
- `model`: Das Gerätemodell.
- `office365Version`: Die auf dem Gerät installierte Version von Office 365.
- `windowsOsEdition`: Die Betriebssystemversion.

Die folgenden Eigenschaften werden jetzt über die Betasammlung [devicePropertyHistory](../developer/reports-ref-devices.md#devicepropertyhistories) verfügbar gemacht:
- `physicalMemoryInBytes`: Der physische Speicher in Byte.
- `totalStorageSpaceInBytes`: Gesamtspeicherkapazität in Bytes

Weitere Informationen finden Sie unter [Microsoft Intune Data Warehouse-API](../developer/reports-nav-intune-data-warehouse.md).

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

## <a name="whats-new-archive"></a>Archiv der Neuheiten
Die Neuigkeiten vorheriger Monate finden Sie im [Archiv für Neuheiten](whats-new-archive.md).

## <a name="notices"></a>Benachrichtigungen

[!INCLUDE [Intune notices](../includes/intune-notices.md)]


