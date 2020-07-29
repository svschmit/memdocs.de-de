---
title: Problembehandlung von Android Enterprise-Geräten in Microsoft Intune
description: Vorschläge zur Behandlung einiger der am häufigsten auftretenden Probleme beim Registrieren von Android-Geräten in Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/25/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b51ed6653dff5b7d0aeef40892e16e2826f30204
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461248"
---
# <a name="troubleshoot-android-enterprise-device-problems-in-microsoft-intune"></a>Problembehandlung von Android Enterprise-Geräten in Microsoft Intune

In diesem Artikel finden Intune-Administratoren Informationen zur Behandlung von Problemen mit Android Enterprise-Geräten in Intune.

## <a name="apps-on-android-enterprise-devices"></a>Apps auf Android Enterprise-Geräten

### <a name="managed-google-play-apps-that-arent-deployed-through-intune-are-displayed-in-the-work-profile"></a>Verwaltete Google Play-Apps, die nicht über Intune bereitgestellt werden, werden im Arbeitsprofil angezeigt.
Bei der Erstellung des Arbeitsprofils können System-Apps vom Geräte-OEM aktiviert werden. Dies wird nicht vom MDM-Anbieter verwaltet.

Gehen Sie zur Problembehandlung folgendermaßen vor:

  1. Erfassen Sie Unternehmensportalprotokolle.
  2. Notieren Sie, welche Apps unerwartet im Arbeitsprofil angezeigt werden.
  3. Heben Sie die Registrierung des Geräts in Intune auf, und deinstallieren Sie das Unternehmensportal.
  4. Installieren Sie die App [Test DPC](https://play.google.com/store/apps/details?id=com.afwsamples.testdpc), die die Erstellung eines Arbeitsprofils ohne eine EMM-Lösung für Tests ermöglicht.
  5. Befolgen Sie die Anweisungen in der App [Test DPC](https://play.google.com/store/apps/details?id=com.afwsamples.testdpc), um ein Arbeitsprofil auf dem Gerät zu erstellen.
  6. Überprüfen Sie, welche Apps im Arbeitsprofil angezeigt werden. 
  7. Wenn dieselben Anwendungen in der Test DPC-App angezeigt werden, werden diese Apps vom OEM des Geräts vorausgesetzt.

### <a name="unapproved-managed-google-play-for-work-store-apps-arent-being-removed-from-the-client-apps-page-in-intune"></a>Nicht genehmigte verwaltete Google Play-Apps werden nicht von der Seite Client-Apps in Intune entfernt.
Dieses Verhalten ist normal.

### <a name="managed-google-play-apps-arent-being-reported-under-the-discovered-apps-blade-in-the-intune-portal"></a>Verwaltete Google Play-Apps werden nicht auf dem Blatt „Ermittelte Apps“ im Intune-Portal angezeigt.
Dieses Verhalten ist normal. Nur System-Apps, die im Arbeitsprofil installiert sind, werden auf dem Blatt „Ermittelte Apps“ aufgeführt. Sie können das Blatt **Verwaltete Apps** verwenden, um die installierten verwalteten Google Play-Apps einzusehen.

### <a name="are-web-applications-supported-for-work-profile-enrolled-devices"></a>Werden Web-Apps für Geräte mit Arbeitsprofilen unterstützt?
Ja. Weitere Informationen finden Sie unter [Weblinks für verwaltetes Google Play](../apps/apps-add-android-for-work.md#managed-google-play-web-links).

## <a name="device-management"></a>Geräteverwaltung

### <a name="file-path-internal-storageandroiddatacommicrosoftwindowsintunecompanyportalfiles-missing-on-work-profile-enrolled-devices"></a>Der Dateipfad Internal storage/Android/Data.com.microsoft.windowsintune.companyportal/files fehlt auf Geräten mit Arbeitsprofilen.

  **Antwort:** Dieses Verhalten ist normal. Dieser Pfad wird nur für den Geräteadministrator erstellt (Legacy-Android-Registrierung).

  Führen Sie die folgenden Schritte durch, um Unternehmensportalprotokolle zu erfassen:

  1. Tippen Sie in der Unternehmensportal-App auf **Menü** > **Hilfe** > **E-Mail-Support**, und tippen Sie dann auf **E-Mail senden und Protokolle hochladen**. 
  2. Wenn die Eingabeaufforderung **Hilfeanforderung senden mit** angezeigt wird, wählen Sie eine der E-Mail-Apps aus.
  3. Eine E-Mail an Ihren IT-Administrator wird mit einer Incident-ID generiert, die an den Microsoft-Produktsupport weitergeleitet werden kann.

### <a name="managed-google-play-last-sync-time--hasnt-been-updated-in-days"></a>Der Zeitpunkt der letzten Synchronisierung vom verwalteten Google Play wurde seit Tagen nicht aktualisiert.
Dieses Verhalten ist normal. Die Synchronisierung wird nur ausgelöst, wenn Sie sie manuell ausführen.

### <a name="encryption-is-required-when-a-device-is-enrolled-can-it-be-turned-off"></a>Die Verschlüsselung ist bei der Registrierung eines Geräts erforderlich. Kann sie deaktiviert werden?
Nein, Google erfordert, dass das Gerät verschlüsselt wird, damit ein Arbeitsprofil erstellt werden kann. 

### <a name="samsung-devices-are-blocking-the-use-of-third-party-keyboards-like-swiftkey"></a>Samsung-Geräte blockieren die Verwendung von Drittanbietertastaturen wie SwiftKey.
Samsung hat diese Einschränkung für Geräte mit Android 8.0 und höher eingeführt. Microsoft arbeitet derzeit mit Samsung an einer Lösung für dieses Problem. Weitere Informationen werden alsbald veröffentlicht.

## <a name="remote-actions"></a>Remoteaktionen

### <a name="wipe-factory-reset-option-isnt-available-for-work-profile-enrolled-device"></a>Die Option „Zurücksetzen“ („Auf Werkseinstellungen zurücksetzen“) ist für Geräte mit Arbeitsprofilen nicht verfügbar.
Dieses Verhalten ist normal. Bei Arbeitsprofilen verfügt der MDM-Anbieter nicht über die vollständige Kontrolle über das Gerät. Es steht nur die Option „Abkoppeln“ („Unternehmensdaten entfernen“) zur Verfügung, mit der das gesamte Arbeitsprofil und alle Inhalte entfernt werden.

Das Zurücksetzen wird für [unternehmenseigene Android Enterprise-Geräte mit Arbeitsprofil](android-corporate-owned-work-profile-enroll.md) unterstützt.

### <a name="is-device-passcode-reset-supported"></a>Wird das Zurücksetzen des Gerätepasscodes unterstützt?
Bei Arbeitsprofilgeräten können Sie den Arbeitsprofilpasscode nur auf Android 8.0 und höher zurücksetzen, wenn:
- der Arbeitsprofilpasscode verwaltet wird und
- der Endbenutzer die Zurücksetzung zulässt.

Für dedizierte Geräte (COSU) und vollständig verwaltete Geräte wird die Zurücksetzung des Passcodes unterstützt.


## <a name="next-steps"></a>Nächste Schritte

- [Behandlung von Problemen bei der Geräteregistrierung bei Intune](troubleshoot-device-enrollment-in-intune.md)
- [Stellen Sie eine Frage im Intune-Forum](https://social.technet.microsoft.com/Forums/%7Blang-locale%7D/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc)
- [Lesen Sie den Blog des Microsoft Intune-Supportteams.](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess)
- [Lesen Sie den Blog zu Microsoft Enterprise Mobility + Security.](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Announcing-the-public-preview-of-Azure-AD-group-based-license/ba-p/245210)