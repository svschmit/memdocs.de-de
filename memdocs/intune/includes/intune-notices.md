---
title: Datei einfügen
description: Datei einfügen
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 08/10/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: 7027eac119ef36adfdb9a0057a74d276696620b3
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820058"
---
Diese Hinweise enthalten wichtige Informationen, die Ihnen bei der Vorbereitung auf künftige Änderungen und Features im Zusammenhang mit Intune helfen können.

### <a name="microsoft-intune-ends-support-for-windows-phone-81-and-windows-10-mobile---3544938-3544909---"></a>Die Microsoft Intune-Unterstützung für Geräte mit Windows Phone 8.1 und Windows 10 Mobile wird eingestellt<!-- 3544938, 3544909 -->
Der Microsoft-Mainstream-Support für Windows Phone 8.1 wurde im Juli 2017 eingestellt, der erweiterte Support im Juni 2019. Die Unternehmensportal-App für Windows Phone 8.1 befindet sich seit Oktober 2017 im Unterstützungsmodus. Außerdem wird am 20. Februar 2020 die Microsoft Intune-Unterstützung für Windows Phone 8.1 eingestellt. 

Der grundlegende Microsoft-Support für Windows 10 Mobile endet im Dezember 2019. Wie in diesem Supporthinweis erwähnt, erlischt für Benutzer von Windows 10 Mobile der Anspruch auf neue Sicherheitsupdates, nicht sicherheitsrelevante Hotfixes, kostenlose Supportoptionen oder Onlineupdates für technische Inhalte von Microsoft. Auf Grundlage der umfassenden Mobile-Betriebssystemunterstützung stellt Microsoft Intune die Unterstützung sowohl für das Unternehmensportal für die Windows 10 Mobile-App als auch für das Windows 10 Mobile-Betriebssystem am 10. August 2020 ein.

Ab dem 10. August treten bei Registrierungen von Windows Phone 8.1- und Windows 10 Mobile-Geräten Fehler auf, und Windows Mobile-Profiltypen werden aus der Intune-Benutzeroberfläche entfernt. Bereits registrierte Geräte werden nicht mehr in den Intune-Dienst eingecheckt, und Geräte- und Richtliniendaten werden gelöscht.

### <a name="end-of-support-for-legacy-pc-management"></a>Ende der Unterstützung für die Legacy-PC-Verwaltung

Legacy-PC-Verwaltungsfunktionen werden ab 15. Oktober 2020 nicht mehr unterstützt. Führen Sie ein Upgrade der Geräte auf Windows 10 aus, und registrieren Sie die Geräte neu als Geräte der Verwaltung mobiler Geräte (MDM), um diese weiterhin in Intune zu verwalten.

[Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2107122)

### <a name="move-to-the-microsoft-endpoint-manager-admin-center-for-all-your-intune-management"></a>Wechseln zum Microsoft Endpoint Manager Admin Center für die gesamte Intune-Verwaltung
Im Rahmen des im März letzten Jahres veröffentlichten Beitrags MC208118 haben wir eine neue, einfache URL für die Microsoft Endpoint Manager-Verwaltung (Intune) eingeführt: [https://endpoint.microsoft.com](https://endpoint.microsoft.com). Bei Microsoft Endpoint Manager handelt es sich um eine einheitliche Plattform, die Microsoft Intune und Configuration Manager umfasst. **Ab dem 1. August 2020** entfernen wir die Intune-Verwaltung unter [https://portal.azure.com](https://portal.azure.com) und empfehlen stattdessen, [https://endpoint.microsoft.com](https://endpoint.microsoft.com) für die Endpunktverwaltung zu verwenden. 


### <a name="decreasing-support-for-android-device-administrator--7371518--"></a>Verringern der Unterstützung für den Android-Geräteadministrator<!--7371518-->
Die Administratorverwaltung für Android-Geräte wurde im Rahmen von Android 2.2 als Möglichkeit zum Verwalten von Android-Geräten veröffentlicht. Ab Android 5 wurde das modernere Verwaltungsframework von [Android Enterprise](../enrollment/connect-intune-android-enterprise.md) veröffentlicht (für Geräte, die eine zuverlässige Verbindung mit Google Mobile Services herstellen können). Google fördert die Verschiebung der Geräteadministratorverwaltung, indem die Verwaltungsunterstützung in neuen Android-Releases reduziert wird.

#### <a name="how-does-this-affect-me"></a>Wie wirkt sich das auf mich aus?
Aufgrund dieser Änderungen von Google im Oktober 2020 verfügen Sie nicht mehr über die umfassenden Verwaltungsfunktionen auf den betroffenen Geräten, die vom Geräteadministrator verwaltet werden. 

> [!NOTE]
> Diese Änderungen waren ursprünglich für das vierte Quartal 2020 angekündigt, wurden aber basierend auf den [neuesten Informationen von Google](https://www.blog.google/products/android-enterprise/da-migration/) verschoben.

##### <a name="device-types-that-will-be-impacted"></a>Betroffene Gerätetypen
Zu den von der reduzierten Geräteadministratorunterstützung betroffenen Geräten gehören jene, bei denen die folgenden drei Bedingungen zutreffen:
- registriert über die Geräteadministratorverwaltung
- Android 10 oder höher
- kein Samsung-Gerät

Geräte sind nicht betroffen, wenn Folgendes zutrifft:
- nicht über die Geräteadministratorverwaltung registriert
- Android-Version vor Android 10
- Samsung-Geräte: Samsung Knox-Geräte werden in diesem Zeitraum nicht betroffen sein, da Intune durch die Integration mit der Knox-Plattform erweiterte Unterstützung bietet. Dadurch erhalten Sie zusätzliche Zeit, den Übergang der Geräteadministratorverwaltung für Samsung-Geräte zu planen.

##### <a name="settings-that-will-be-impacted"></a>Betroffene Einstellungen
Die [reduzierte Geräteadministratorunterstützung](https://developers.google.com/android/work/device-admin-deprecation) verhindert, dass die Konfiguration dieser Einstellungen auf betroffene Geräte angewendet wird.

###### <a name="configuration-profile-device-restriction-settings"></a>Geräteeinschränkungseinstellungen für Konfigurationsprofile

- **Kamera blockieren**
- Festlegen von **Minimale Kennwortlänge**
- Festlegen der **Anzahl von Anmeldefehlern, bevor das Gerät zurückgesetzt wird** (wird im Gegensatz zu Geräten mit festgelegtem Kennwort nicht auf Geräten ohne festgelegtes Kennwort angewendet)
- Festlegen von **Kennwortablauf (in Tagen)**
- Festlegen von **Erforderlicher Kennworttyp**
- Festlegen von **Prevent use of previous passwords** (Wiederverwendung vorheriger Kennwörter verhindern)
- Blockieren von **Smart Lock und andere Vertrauens-Agents**

###### <a name="compliance-policy-settings"></a>Einstellungen für Kompatibilitätsrichtlinie

- Festlegen von **Erforderlicher Kennworttyp**
- Festlegen von **Minimale Kennwortlänge**
- Festlegen der **Anzahl von Tagen bis zum Kennwortablauf**
- Festlegen der **Anzahl vorheriger Kennwörter, deren Wiederverwendung verhindert wird**


![Screenshot: Seite für Android-Compliancerichtlinie](../fundamentals/media/notices/android-compliance-settings.png)

###### <a name="additional-impacts-based-on-android-os-version"></a>Weitere Auswirkungen auf Grundlage der Android-Betriebssystemversion

**Android 10:** Für alle vom Geräteadministrator verwalteten Geräte (einschließlich Samsung) unter Android 10 und höher hat Google für Geräteadministratorverwaltung-Agents wie z. B. das Unternehmensportal die Möglichkeit beschränkt, auf Gerätebezeichnerinformationen zuzugreifen. Diese Einschränkung wirkt sich nach Geräteupdates auf Android 10 oder höher auf die folgenden Intune-Features wie folgt aus:
- Die Netzwerkzugriffssteuerung für VPN funktioniert nicht mehr.
- Die Identifizierung von Geräten mit IMEI oder Seriennummer als unternehmenseigen kennzeichnet Geräte nicht automatisch als unternehmenseigen.
- Die IMEI und Seriennummer sind für IT-Administratoren in Intune nicht mehr sichtbar.

**Android 11:** Wir testen derzeit die Unterstützung von Android 11 der neuesten Entwicklerbetaversion, um zu ermitteln, ob dies Auswirkungen auf vom Geräteadministrator verwaltete Geräte hat.

#### <a name="user-experience-of-impacted-settings-on-impacted-devices"></a>Verwendung betroffener Einstellungen auf betroffenen Geräten

Betroffene Konfigurationseinstellungen:
- Bei bereits registrierten Geräten, auf die die Einstellungen schon angewendet wurden, werden die betroffenen Konfigurationseinstellungen weiterhin erzwungen.
- Bei neu registrierten Geräten sowie neu zugewiesenen und aktualisierten Einstellungen werden die betroffenen Konfigurationseinstellungen nicht erzwungen. Allerdings werden alle anderen Konfigurationseinstellungen weiterhin erzwungen.

Betroffene Konformitätseinstellungen:
- Bei bereits registrierten Geräten, auf die die Einstellungen schon angewendet wurden, werden die betroffenen Konformitätseinstellungen auf der Seite „Geräteeinstellungen aktualisieren“ weiterhin als Gründe für die Nichtkonformität angezeigt. Das Gerät ist nicht konform, und die Kennwortanforderungen werden in der App „Einstellungen“ weiterhin erzwungen.
- Bei neu registrierten Geräten sowie neu zugewiesenen und aktualisierten Einstellungen werden die betroffenen Konformitätseinstellungen auf der Seite „Geräteeinstellungen aktualisieren“ weiterhin als Gründe für die Nichtkonformität angezeigt. Das Gerät ist nicht konform, aber strengere Kennwortanforderungen werden in der App „Einstellungen“ nicht erzwungen.

#### <a name="cause-of-impact"></a>Ursache der Auswirkung 
Ab Oktober 2020 haben die Änderungen Auswirkungen auf die Geräte. Zu diesem Zeitpunkt wird ein Update für die Unternehmensportal-App bereitgestellt, durch das die Unternehmensportal-API anstelle von Ebene 28 auf Ebene 29 abzielt ([gemäß den Anforderungen von Google](https://www.blog.google/products/android-enterprise/da-migration/)). 

Dann sind von einem Geräteadministrator verwaltete und nicht von Samsung hergestellte Geräte betroffen, sobald der Benutzer diese beiden Aktionen abgeschlossen hat:
- Update auf Android 10 oder höher
- Aktualisieren der Unternehmensportal-App auf die Version, die auf die API-Ebene 29 abzielt

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Was muss ich als Vorbereitung auf diese Veränderung tun?
Um die ab Oktober 2020 geltenden Funktionseinschränkungen zu vermeiden, wird Folgendes empfohlen:
- **Neue Registrierungen:** Integrieren Sie neue Geräte in die [Android Enterprise](../enrollment/connect-intune-android-enterprise.md)-Verwaltung (falls verfügbar) und/oder [App-Schutzrichtlinien](../apps/app-protection-policies.md). Vermeiden Sie das Integrieren neuer Geräte in die Geräteadministratorverwaltung. 
- **Zuvor registrierte Geräte:** Wenn ein von einem Geräteadministrator verwaltetes Gerät unter Android 10 oder höher ausgeführt oder ein Update auf Android 10 oder höher ausgeführt wird (insbesondere, wenn es sich um kein Samsung-Gerät handelt), verschieben Sie es von der Geräteadministratorverwaltung in die [Android Enterprise](../enrollment/connect-intune-android-enterprise.md)-Verwaltung und/oder [App-Schutzrichtlinien](../apps/app-protection-policies.md). Sie können den optimierten Flow verwenden, um [Android-Geräte aus dem Geräteadministrator in die Arbeitsprofilverwaltung zu verschieben](../enrollment/android-move-device-admin-work-profile.md).

#### <a name="additional-information"></a>Zusätzliche Informationen
- [Verschieben von Android-Geräten aus dem Geräteadministrator in die Arbeitsprofilverwaltung](../enrollment/android-move-device-admin-work-profile.md)
- [Einrichten der Registrierung von Android Enterprise-Arbeitsprofilgeräten](../enrollment/android-work-profile-enroll.md)
- [Einrichten der Intune-Registrierung für dedizierte Android Enterprise-Geräte](../enrollment/android-kiosk-enroll.md)
- [Einrichten der Intune-Registrierung von vollständig verwalteten Android Enterprise-Geräten](../enrollment/android-fully-managed-enroll.md)
- [Erstellen und Zuweisen von App-Schutzrichtlinien](../apps/app-protection-policies.md)
- [Verwenden von Intune in Umgebungen ohne Google Mobile Services](../apps/manage-without-gms.md)
- [Anwendungsschutzrichtlinien und Arbeitsprofile für Android Enterprise-Geräte in Intune](../apps/android-deployment-scenarios-app-protection-work-profiles.md)
- [Google-Blog zur Veraltung des Geräteadministrators](https://www.blog.google/products/android-enterprise/da-migration/)
- [Google-Leitfaden für die Migration vom Geräteadministrator zu Android Enterprise](http://static.googleusercontent.com/media/android.com/en/enterprise/static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf)
- [Google-Dokumentation zu veralteten Geräteadministrator-APIs](https://developers.google.com/android/work/device-admin-deprecation)


### <a name="plan-for-change-intune-enrollment-flow-update-for-apples-automated-device-enrollment-for-iosipados"></a>Stellen Sie sich auf eine Änderung ein: Intune-Registrierungsflowaktualisierung für die automatisierte Geräteregistrierung von Apple für iOS/iPadOS
Im Unternehmensportal-Release von Juli ändern wir den iOS/iPadOS-Registrierungsflow für die automatisierte Geräteregistrierung von Apple (früher als Programm zur Geräteregistrierung (DEP) bezeichnet). Die Änderung des Registrierungsflows hat nur Auswirkungen während des Flows „Mit Benutzeraffinität registrieren“. Wenn Sie zuvor im Rahmen Ihrer Konfiguration „Unternehmensportal installieren“ auf „Nein“ festgelegt haben, können Benutzer die Unternehmensportal-App noch immer über den Store installieren, wodurch eine Registrierung ausgelöst wird, bei der der Benutzer die entsprechende Seriennummer hinzufügt. Mit diesem bevorstehenden Unternehmensportal-Release entfernen wir den Bestätigungsbildschirm für die Seriennummer. Stattdessen sollten Sie eine entsprechende App-Konfigurationsrichtlinie erstellen, die zusammen mit dem Unternehmensportal sicherstellt, dass sich Benutzer erfolgreich registrieren können. Andernfalls können Sie die Einstellung „Unternehmensportal installieren“ als Teil Ihrer Konfiguration auf „Ja“ festlegen. 
 - Weitere Informationen finden Sie in [diesem Blogbeitrag](https://techcommunity.microsoft.com/t5/intune-customer-success/intune-enrollment-flow-update-for-apple-s-automated-device/ba-p/1431629).
