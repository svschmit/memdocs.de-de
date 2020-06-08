---
title: Einstellungen für Windows Holographic for Business-Geräte – Microsoft Intune – Azure | Microsoft-Dokumentation
description: In diesem Artikel erhalten Sie Informationen zum Konfigurieren von Einstellungen zur Geräteeinschränkung in Microsoft Intune für Windows Holographic for Business. Aufhebung einer Registrierung, Geolocation, Kennwörter, Installieren von Apps aus dem App Store, Cookies und Popupmenüs in Microsoft Edge, Microsoft Defender, Suchen, Cloud und Speicher, Bluetooth-Verbindungen, Systemzeit und Nutzungsdaten in Azure.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 301cdd9403b0bb3e2d64c8707782ecbc639dc044
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556046"
---
# <a name="windows-holographic-for-business-device-settings-to-allow-or-restrict-features-using-intune"></a>Windows Holographic for Business-Geräteeinstellungen zum Zulassen oder Einschränken von Features mit Intune

In diesem Artikel werden die verschiedenen Einstellungen aufgeführt und beschrieben, die Sie für Windows Holographic for Business-Geräte steuern können, z.B. Microsoft Hololens. Als Bestandteil Ihrer Lösung für die mobile Geräteverwaltung (Mobile Device Management, MDM) verwenden Sie diese Einstellungen, um Features zuzulassen oder zu deaktivieren, die Sicherheit zu steuern und mehr.

Als Intune-Administrator können Sie für Ihre Geräte diese Einstellungen erstellen und ihnen zuweisen.

## <a name="before-you-begin"></a>Vorbereitung

[Erstellen Sie ein Konfigurationsprofil für Windows 10-Geräteeinschränkungen](device-restrictions-configure.md#create-the-profile).

Beim Erstellen eines Konfigurationsprofils für Windows 10-Geräteeinschränkungen gibt es mehr Einstellungen, als in diesem Artikel aufgeführt werden. Die Einstellungen in diesem Artikel werden auf Geräten mit Windows Holographic for Business unterstützt.

## <a name="app-store"></a>App Store

- **Apps aus Store automatisch aktualisieren**: Mit der Option **Blockieren** wird verhindert, dass Updates automatisch über den Microsoft Store installiert werden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass Apps, die aus dem Microsoft Store heruntergeladen und installiert werden, automatisch aktualisiert werden.

  [ApplicationManagement/AllowAppStoreAutoUpdate-CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowappstoreautoupdate)

- **Installation vertrauenswürdiger Apps**: Wählen Sie diese Option aus, wenn Apps installiert werden können, die nicht aus dem Microsoft Store stammen. Dies wird auch als Querladen bezeichnet. Querladen bedeutet Installieren und anschließendes Ausführen oder Testen einer App, die nicht durch den Microsoft Store zertifiziert ist. Beispielsweise kann es sich um eine App handeln, die nur für Ihr Unternehmen intern ist. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
  - **Blockieren:** Verhindert Querladen. Apps, die nicht auf dem Microsoft Store stammen, können nicht installiert werden.
  - **Zulassen:** Ermöglicht Querladen. Apps, die nicht auf dem Microsoft Store stammen, können installiert werden.

  [ApplicationManagement/AllowAllTrustedApps-CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowalltrustedapps)

- **Entwicklersperre aufheben**: Ermöglicht es Benutzern, Windows-Entwicklereinstellungen – z. B. das Zulassen quergeladener Apps – zu ändern. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
  - **Blockieren:** Verhindert den Entwicklermodus und das Querladen von Apps.
  - **Zulassen:** Erlaubt den Entwicklermodus und das Querladen von Apps.

  [ApplicationManagement/AllowDeveloperUnlock-CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowdeveloperunlock)

## <a name="cellular-and-connectivity"></a>Mobilfunk und Konnektivität

- **Bluetooth**: **Blockieren** verhindert, dass Benutzer Bluetooth aktivieren können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Das Betriebssystem erlaubt die Verwendung von Bluetooth auf dem Gerät möglicherweise standardmäßig.

  [Connectivity/AllowBluetooth-CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-connectivity#connectivity-allowbluetooth)

- **Bluetooth-Erkennbarkeit**: **Blockieren** verhindert die Erkennung dieses Geräts durch andere für Bluetooth aktivierte Geräte. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass andere Bluetooth-fähige Geräte (z. B. ein Kopfhörer) das Gerät erkennen.

  [Bluetooth/AllowDiscoverableMode-CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

- **Bluetooth-Ankündigung**: **Blockieren** verhindert, dass das Gerät Bluetooth-Ankündigungen sendet. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass das Gerät Bluetooth-Ankündigungen sendet.

  [Bluetooth/AllowAdvertising-CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowadvertising)

## <a name="cloud-and-storage"></a>Cloud und Speicher

- **Microsoft-Konto**: Wenn **Blockieren** festgelegt wird, werden Benutzer daran gehindert, dem Gerät ein Microsoft-Konto zuzuordnen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass ein Microsoft-Konto hinzugefügt und verwendet wird.

  [Accounts/AllowMicrosoftAccountConnection-CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-accounts#accounts-allowmicrosoftaccountconnection)

## <a name="control-panel-and-settings"></a>Systemsteuerung und Einstellungen

- **Änderung der Systemzeit**: **Blockieren** hindert Benutzer daran, die Datums- und Uhrzeiteinstellungen auf dem Gerät zu ändern. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, diese Einstellungen zu ändern.

  [Settings/AllowDateTime-CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-settings#settings-allowdatetime)

## <a name="general"></a>Allgemein

- **Manuelles Aufheben der Registrierung**: **Blockieren** verhindert, dass Benutzer das Arbeitsplatzkonto über die Arbeitsplatz-Systemsteuerung auf dem Gerät löschen können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

  [Experience/AllowManualMDMUnenrollment-CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowmanualmdmunenrollment)

- **Geolocation**: **Blockieren** verhindert, dass Benutzer Ortungsdienste auf dem Gerät aktivieren können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

  [Experience/AllowFindMyDevice-CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowfindmydevice)

- **Cortana**: **Blockieren** deaktiviert den Sprach-Assistenten Cortana auf dem Gerät. Wenn Cortana deaktiviert ist, können Benutzer trotzdem suchen, um Elemente auf dem Gerät zu finden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem Cortana standardmäßig zu.

  [Experience/AllowCortana-CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowcortana)

## <a name="microsoft-edge-browser"></a>Microsoft Edge-Browser

- **Startoberfläche** > **Popups zulassen**: **Ja** (Standard) lässt Popups im Webbrowser zu. **Nein** verhindert Popupfenster im Browser.

  [Browser/AllowPopups-CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpopups)

- **Favoriten und Suche** > **Suchvorschläge anzeigen**: **Ja** (Standard) ermöglicht es der Suchmaschine, Websites während der Eingabe von Suchausdrücken in der Adressleiste vorzuschlagen. **Nein** verhindert die Verwendung dieser Funktion.

  [Browser/AllowSearchSuggestionsinAddressBar-CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar)

- **Datenschutz-und Sicherheit** > **Kennwort-Manager zulassen**: **Ja** (Standard) ermöglicht es, dass Microsoft Edge automatisch den Kennwort-Manager verwendet. Dies ermöglicht es Benutzern, Kennwörter auf dem Gerät zu speichern und zu verwalten. **Nein** verhindert, dass Microsoft Edge den Kennwort-Manager verwendet.

  [Browser/AllowPasswordManager-CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)

- **Datenschutz und Sicherheit** > **Cookies**: Wählen Sie aus, wie Cookies im Webbrowser verarbeitet werden sollen. Folgende Optionen sind verfügbar:
  - **Zulassen:** ermöglicht das Speichern von Cookies auf dem Gerät.
  - **Block all cookies** (Alle Cookies blockieren): Cookies werden nicht auf dem Gerät gespeichert.
  - **Nur Cookies von Drittanbietern blockieren:** Cookies von Drittanbietern oder Partnern werden nicht auf dem Gerät gespeichert.

  [Browser/AllowCookies-CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowcookies)

- **Datenschutz-und Sicherheit** > **DNT-Kopfzeilen senden**: **Ja** sendet DNT-Kopfzeilen an Websites, die Nachverfolgungsinformationen anfordern (empfohlen). **Nein** (Standard) sendet keine Header, die Websites das Nachverfolgen von Benutzern ermöglichen. Diese Einstellung kann von Benutzern konfiguriert werden.

  [Browser/AllowDoNotTrack-CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack)

## <a name="microsoft-defender-smartscreen"></a>Microsoft Defender SmartScreen

- **SmartScreen für Microsoft Edge**: **Erforderlich** aktiviert Microsoft Defender SmartScreen und hindert Benutzer an der Deaktivierung dieses Features. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Das Betriebssystem aktiviert SmartScreen möglicherweise standardmäßig und gestattet Benutzern das Aktivieren/Deaktivieren dieses Features.

  [Browser/AllowSmartScreen-CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

## <a name="password"></a>Kennwort

- **Kennwort:** Wenn **Anfordern** festgelegt wird, müssen Benutzer ein Kennwort eingeben, um auf das Gerät zuzugreifen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem den Zugriff auf Geräte möglicherweise ohne Kennwort zu. Diese Einstellung gilt nur für lokale Konten. Kennwörter für Domänenkonten werden weiterhin von Active Directory (AD) und Azure AD konfiguriert.

  [DeviceLock/DevicePasswordEnabled-CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordenabled)

- **Kennwort anfordern, wenn das Gerät aus Leerlaufzustand zurückkehrt**: **Anfordern** zwingt Benutzer zur Eingabe eines Kennworts, um das Gerät zu entsperren, nachdem es im Leerlauf war. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig fordert das Betriebssystem möglicherweise keine PIN und kein Kennwort nach dem Leerlauf an.

  [DeviceLock/AllowIdleReturnWithoutPassword-CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-allowidlereturnwithoutpassword)

## <a name="reporting-and-telemetry"></a>Berichterstellung und Telemetrie

- **Nutzungsdaten freigeben**: Wählen Sie die Ebene der Diagnosedaten aus, die gesendet werden. Folgende Optionen sind verfügbar:

  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Es wird keine Einstellung erzwungen. Benutzer wählen die Ebene für die Übermittlung aus. Möglicherweise gibt das Betriebssystem standardmäßig keine Daten frei.
  - **Sicherheit**: Informationen, die erforderlich sind, um Windows sicherer zu machen, einschließlich Daten zu den Einstellungen der Komponente „Benutzererfahrung und Telemetrie im verbundenen Modus“, zum Tool zum Entfernen bösartiger Software und zu Microsoft Defender
  - **Standard**: Grundlegende Geräteinformationen, z. B. qualitätsbezogene Daten, App-Kompatibilität, App-Nutzungsdaten und Daten aus der Sicherheitsebene
  - **Erweitert**: Zusätzliche Informationen, z. B. zur Verwendung von Windows, Windows Server, System Center oder Anwendungen, Leistungsdaten, erweiterte Zuverlässigkeitsdaten sowie Daten der Ebenen „Standard“ und „Sicherheit“
  - **Vollständig**: Alle Daten, die zur Identifizierung und Behebung von Problemen erforderlich sind, sowie Daten der Ebenen „Sicherheit“, „Standard“ und „Erweitert“.

  [System/AllowTelemetry-CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-allowtelemetry)

## <a name="search"></a>Suchen

- **Standortsuche**: **Blockieren** verhindert, dass Windows Search den Standort verwendet. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Es besteht die Möglichkeit, dass das Betriebssystem dieses Feature standardmäßig nicht zulässt.

  [Search/AllowSearchToUseLocation-CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-allowsearchtouselocation)

## <a name="next-steps"></a>Nächste Schritte

[Weisen Sie das Profil zu](device-profile-assign.md), und [überwachen Sie seinen Status](device-profile-monitor.md).
