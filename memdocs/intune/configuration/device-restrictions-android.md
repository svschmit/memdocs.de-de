---
title: Einstellungen für Geräteeinschränkungen für Android in Microsoft Intune – Azure | Microsoft-Dokumentation
description: 'Hier finden Sie eine Liste aller Android-Geräteadministratoreinstellungen, die Sie in Microsoft Intune steuern und einschränken können. Mit diesen Einstellungen können Sie Folgendes steuern: Kennwort, Zugriff auf Google Play, Zulassen oder Verbieten von Apps, Steuern der Browsereinstellungen, Blockieren von Apps, Sicherung in der Google-Cloud sowie Steuern der Optionen für Nachrichten, Spracheinstellungen, Datenroaming, WLAN und Bluetooth-Verbindungen.'
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/30/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: chmaguir, chrisbal
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 02e07ec75b7c0d07a81a9c6f555cf119310a9a9f
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/19/2020
ms.locfileid: "85093681"
---
# <a name="android-and-samsung-knox-standard-device-restriction-settings-lists-in-intune"></a>Listen der Standardeinstellungen für Geräteeinschränkungen für Android und Samsung KNOX in Intune

In diesem Artikel lernen Sie alle Einstellungen für Geräteeinschränkungen in Microsoft Intune kennen, die Sie für Android-Geräte konfigurieren können.

>[!TIP]
>Wenn Ihre gewünschten Einstellungen nicht verfügbar sind, können Sie Ihre Geräte möglicherweise mit einem [benutzerdefinierten Profil](custom-settings-android.md) konfigurieren.

## <a name="before-you-begin"></a>Vorbereitung

[Erstellen Sie ein Profil für die Gerätekonfiguration.](device-restrictions-configure.md)

## <a name="general"></a>Allgemein

- **Kamera:** Wenn **Blockieren** festgelegt wird, wird der Zugriff auf die Kamera des Geräts verhindert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise den Zugriff auf die Kamera des Geräts zu.

  Intune verwaltet nur den Zugriff auf die Kamera des Geräts. Das Programm kann nicht auf Bilder oder Videos zugreifen.

- **Kopieren und einfügen (nur Samsung KNOX)** : **Blockieren** verhindert das Kopieren und Einfügen. **Nicht konfiguriert** lässt Kopier- und Einfügefunktionen auf Geräten zu.
- **Gemeinsame Nutzung der Zwischenablage durch Apps (nur Samsung KNOX)** : **Blockieren** verhindert die Verwendung der Zwischenablage zum Kopieren und Einfügen zwischen Anwendungen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Kopier- und Einfügefunktionen auf Geräten zulassen.
- **Übermittlung von Diagnosedaten (nur Samsung KNOX)** : **Blockieren** hindert Benutzer daran, Fehlerberichte von Geräten zu übermitteln. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Es besteht die Möglichkeit, dass das Betriebssystem Benutzern erlaubt, die Daten zu übermitteln.
- **Zurücksetzung auf Werkseinstellungen (nur Samsung KNOX)** : Ermöglicht es Benutzern, die Aktion [Zurücksetzen](../remote-actions/devices-wipe.md) auf Geräten auszuführen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Geolocation (nur Samsung KNOX)** : **Blockieren** verhindert, dass Geräte Standortinformationen verwenden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Es besteht die Möglichkeit, dass das Betriebssystem standardmäßig zulässt, dass Geräte die Standortinformationen verwenden.
- **Ausschalten (nur Samsung KNOX)** : **Blockieren** hindert Benutzer daran, das Gerät auszuschalten. Ebenso wird verhindert, dass die Einstellung **Anzahl von Anmeldefehlern, bevor das Gerät zurückgesetzt wird** konfiguriert und ausgeführt wird. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, Geräte auszuschalten.
- **Bildschirmaufnahme (nur Samsung KNOX)** : **Blockieren** verhindert das Aufnehmen von Screenshots. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Das Betriebssystem lässt möglicherweise standardmäßig zu, dass Benutzer den Bildschirminhalt als Bild erfassen.
- **Sprach-Assistent (nur Samsung KNOX)** : **Blockieren** deaktiviert den S Voice-Dienst. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Verwendung des S Voice-Diensts und der -App auf Geräten zulassen. Diese Einstellung gilt nicht für Bixby oder den Sprach-Assistenten für die Bedienungshilfe, der den Bildschirminhalt laut vorliest.
- **YouTube (nur Samsung KNOX)** : **Blockieren** verhindert, dass Benutzer die YouTube-App verwenden können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Verwendung der YouTube-App auf Geräten zulassen.
- **Freigegebene Geräte (nur Samsung KNOX)** : Konfigurieren Sie ein verwaltetes Samsung KNOX-Standardgerät als freigegeben. **Zulassen** ermöglicht Benutzern, sich mit ihren Azure AD-Anmeldeinformationen auf Geräten anzumelden bzw. abzumelden. Geräte werden weiterhin verwaltet, egal ob diese verwendet werden oder nicht.

  In Verbindung mit einem SCEP-Zertifikatsprofil ermöglicht dieses Feature Benutzern die gemeinsame Nutzung eines Geräts mit denselben Apps für alle Benutzer. Aber jeder Benutzer verfügt über ein eigenes SCEP-Benutzerzertifikat. Wenn sich Benutzer abmelden, werden alle App-Daten gelöscht. Dieses Feature ist ausschließlich auf branchenspezifische Apps beschränkt.

  Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Es besteht die Möglichkeit, dass das Betriebssystem standardmäßig mehrere Endbenutzer daran hindert, sich bei der Unternehmensportal-App auf Geräten mit ihren Azure AD-Anmeldeinformationen anzumelden.
- **Datums- und Uhrzeitänderungen blockieren (Samsung KNOX)** : **Blockieren** verhindert, dass Benutzer auf Geräten die Datums- und Uhrzeiteinstellungen ändern. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, die Einstellungen für Datum und Uhrzeit zu ändern.

## <a name="password"></a>Kennwort

- **Kennwort:** Wenn **Erforderlich** festgelegt wird, müssen Benutzer ein Kennwort eingeben, um auf Geräte zuzugreifen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, ohne Kennworteingabe auf Geräte zuzugreifen.

    > [!NOTE]
    > Samsung Knox-Geräte erfordern automatisch eine vierstellige PIN bei der MDM-Registrierung. Native Android-Geräte erfordern möglicherweise automatisch eine PIN, damit sie mit den bedingten Zugriffsvoraussetzungen konform sind.

- **Minimale Kennwortlänge:** Geben Sie die erforderliche Mindestanzahl von Zeichen ein (zwischen 4 und 16). Geben Sie z. B. `6` ein, um ein mindestens sechs Zeichen langes Kennwort zu verlangen.
- **Maximaler Zeitraum der Inaktivität (in Minuten) bis zur Bildschirmsperrung:** Geben Sie den Zeitraum an, für den sich Geräte im Leerlauf befinden müssen, bevor der Bildschirm automatisch gesperrt wird. Geben Sie zum Beispiel `5` ein, um Geräte nach 5 Minuten im Leerlauf zu sperren. Wenn kein Wert angegeben oder **Nicht konfiguriert** festgelegt ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.

  Benutzer können keinen Zeitwert auf einem Gerät festlegen, der über dem im Profil konfigurierten Zeitwert liegt. Benutzer können einen niedrigeren Zeitwert festlegen. Wenn das Profil beispielsweise auf `15` Minuten festgelegt wird, können Benutzer einen Wert von 5 Minuten festlegen. Benutzer können den Wert jedoch nicht auf 30 Minuten festlegen.

- **Anzahl von fehlgeschlagenen Anmeldungen, bevor das Gerät zurückgesetzt wird:** Geben Sie an, wie häufig ein falsches Kennwort eingegeben werden kann, bevor Geräte zurückgesetzt werden (zwischen 4 und 11). Wenn `0` (null) festgelegt wird, wird möglicherweise die Funktion zum Zurücksetzen des Geräts deaktiviert. Wenn kein Wert angegeben ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.
- **Kennwortablauf (Tage):** Geben Sie die Anzahl der Tage ein, bis das Gerätekennwort geändert werden muss (von 1 bis 365). Geben Sie beispielsweise `90` an, damit das Kennwort nach 90 Tagen abläuft. Wenn das Kennwort abläuft, werden Benutzer aufgefordert, ein neues Kennwort zu erstellen. Wenn kein Wert angegeben ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.
- **Erforderlicher Kennworttyp:** Geben Sie den erforderlichen Grad der Kennwortkomplexität ein, und bestimmen Sie, ob biometrische Geräte zulässig sind. Folgende Optionen sind verfügbar:
  - **Gerätestandard**
  - **Biometrie auf niedriger Sicherheitsstufe:** [Vergleich von stark und schwach biometrisch](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (öffnet Android-Website)
  - **Mindestens numerisch:** Bei dieser Einstellung sind numerische Zeichen wie `123456789` enthalten.
  - **Numerisch, komplex:** Sich wiederholende oder fortlaufende Ziffern wie „1111“ oder „1234“ sind nicht zulässig. Bevor Sie diese Einstellung Geräten zuweisen, aktualisieren Sie die Unternehmensportal-App auf diesen Geräten auf jeden Fall auf die neueste Version.

    Wenn die Einstellung auf **Numerisch, komplex** festgelegt ist und Sie die Einstellung Geräten zuweisen, die eine frühere Android-Version als 5.0 ausführen, gilt folgendes Verhalten:

    - Wenn die Unternehmensportal-App eine ältere Version als 1704 ausführt, wird keine PIN-Richtlinie auf Geräte angewendet, und eine Fehlermeldung wird im Microsoft Endpoint Manager Admin Center angezeigt.
    - Wenn die Unternehmensportal-App die Version 1704 oder höher ausführt, kann nur eine einfache PIN angewendet werden. Frühere Android-Versionen als 5.0 unterstützen diese Einstellung nicht. Im Microsoft Endpoint Manager Admin Center wird kein Fehler angezeigt.

  - **Mindestens alphabetisch**: Bei dieser Einstellung sind Buchstaben des Alphabets enthalten. Zahlen und Symbole sind nicht erforderlich.
  - **Mindestens alphanumerisch**: Schließt Großbuchstaben, Kleinbuchstaben und Ziffern ein.
  - **Mindestens alphanumerisch mit Symbolen**: Schließt Großbuchstaben, Kleinbuchstaben, Ziffern, Interpunktionszeichen und Symbole ein.

- **Wiederverwendung vorheriger Kennwörter verhindern:** Verwenden Sie diese Einstellung, um zu verhindern, dass Benutzer zuvor verwendete Kennwörter erstellen. Geben Sie die Anzahl der zuvor verwendeten Kennwörter ein, die nicht erneut verwendet werden können, von 1–24. Geben Sie z.B. `5` an, damit ein Benutzer sein neues Kennwort nicht auf sein aktuelles Kennwort oder eines seiner vorherigen vier Kennwörter festlegen kann. Wenn kein Wert angegeben ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.
- **Fingerabdruckentsperrung (nur Samsung KNOX)** : Die Einstellung **Blockieren** verhindert die Verwendung eines Fingerabdrucks zum Entsperren von Geräten. Wenn die Einstellung auf **Nicht konfiguriert** (Standard) festgelegt ist, wird diese von Intune nicht geändert oder aktualisiert. In der Standardeinstellung lässt das Betriebssystem möglicherweise zu, dass Benutzer Geräte mit einem Fingerabdruck entsperren.
- **Smart Lock und andere Vertrauens-Agents:** **Blockieren** verhindert das Anpassen von Sperrbildschirmeinstellungen durch Smart Lock oder andere Vertrauens-Agents. Wenn sich ein Gerät in einer vertrauenswürdigen Umgebung befindet, können Sie mit diesem Feature (das auch als Vertrauens-Agent bekannt ist) das Kennwort für den Gerätesperrbildschirm deaktivieren oder umgehen. Beispielsweise können Sie dieses Feature verwenden, wenn Geräte mit einem bestimmten Bluetooth-Gerät verbunden sind oder sich in der Nähe eines NFC-Tags befinden. Mit dieser Einstellung können Sie verhindern, dass Benutzer Smart Lock konfigurieren.

  Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

  Diese Einstellung gilt für:

  - Samsung KNOX Standard 5.0 und höher

- **Verschlüsselung:** Wählen Sie **Anfordern** aus, sodass die Dateien auf dem Gerät verschlüsselt werden. Nicht alle Geräte unterstützen die Verschlüsselung. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Konfigurieren Sie außerdem Folgendes, um diese Einstellung zu konfigurieren und sie ordnungsgemäß als konform zu melden:
  1. **Kennwort:** Legen sie **Erfordern** fest.
  2. **Erforderlicher Kennworttyp:** Legen Sie **Mindestens Numerisch** fest.
  3. **Minimale Kennwortlänge:** Legen Sie mindestens `4` fest.

  > [!NOTE]
  > Wenn eine Verschlüsselungsrichtlinie erzwungen wird, erfordern Samsung Knox-Geräte, dass Benutzer ein komplexes Kennwort, das aus sechs Zeichen besteht, für die Gerätekennung festlegen.

## <a name="google-play-store"></a>Google Play Store

- **Google Play Store (nur Samsung KNOX)** : **Blockieren** verhindert, dass Benutzer den Google Play Store verwenden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern den Zugriff auf den Google Play Store ermöglichen.

## <a name="restricted-apps"></a>Eingeschränkte Apps

Verwenden Sie diese Einstellungen, um bestimmte Apps auf Geräten zuzulassen oder zu verhindern. Dieses Feature wird auf Android- und Samsung KNOX Standard-Geräten unterstützt.

- **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
- **Unzulässige Apps:** Listen Sie die (nicht von Intune verwalteten) Apps auf, die Benutzer nicht installieren und ausführen dürfen. Wenn ein Benutzer eine App aus dieser Liste installiert, werden Sie von Intune benachrichtigt.
- **Genehmigte Apps:** Listet die Apps auf, die Benutzer installieren dürfen. Um die Kompatibilität zu gewährleisten, dürfen Benutzer keine anderen Apps installieren.  Apps, die von Intune verwaltet werden, sind automatisch zugelassen, einschließlich der Unternehmensportal-App.
- **Liste der Apps:** **Fügen Sie** Ihre App hinzu:
  - **App-Bündel-ID**: Geben Sie die Paket-ID der App ein.
  - **App Store-URL:** Die Google Play Store-URL der App, die Sie wünschen, eingeben. Um z.B. die Microsoft-Remotedesktop-App für Android hinzuzufügen, geben Sie `https://play.google.com/store/apps/details?id=com.microsoft.rdc.android` ein.

    Um die URL einer App zu suchen, öffnen Sie den [Google Play Store](https://play.google.com/store/apps), und suchen Sie nach der App. Suchen Sie beispielsweise nach `Microsoft Remote Desktop Play Store` oder `Microsoft Planner`. Wählen Sie die App aus, und kopieren Sie die URL.
  
  - **App-Name:** Geben Sie den gewünschten Namen ein. Dieser Name wird Benutzern angezeigt.
  - **Herausgeber** (optional): Geben Sie den Herausgeber der App ein, zum Beispiel `Microsoft`.

Sie können auch eine CSV-Datei mit den Details der App **importieren**, einschließlich der URL. Verwenden Sie das Format <*App-URL*>, <*App-Name*>, <*App-Herausgeber*>. **Exportieren** Sie alternativ eine vorhandene Liste, die die Liste der eingeschränkten Apps im gleichen Format enthält.

> [!IMPORTANT]
> Geräteprofile, die Einstellungen für eingeschränkte Apps verwenden, müssen Benutzergruppen (nicht Gerätegruppen) zugewiesen werden.

## <a name="browser"></a>Browser

- **Webbrowser (nur Samsung KNOX )** : **Blockieren** verhindert, dass der Standardwebbrowser auf Geräten verwendet wird. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig ermöglicht das Betriebssystem möglicherweise die Verwendung des Standardwebbrowsers des Geräts.
- **AutoAusfüllen (nur Samsung KNOX)** : **Blockieren** hindert den Browser daran, Text einzugeben. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise automatisches Ausfüllen zu.
- **Cookies (nur Samsung KNOX)** : Wählen Sie aus, wie Sie mit Cookies von Websites auf dem Gerät umgehen möchten. Folgende Optionen sind verfügbar:
  - Zulassen
  - Alle Cookies blockieren
  - Cookies von besuchten Websites zulassen
  - Cookies von aktueller Website zulassen
- **JavaScript (nur Samsung KNOX)** : **Blockieren** verhindert, dass JavaScript im Browser ausgeführt wird. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem diese Skripts zulassen.
- **Popups (nur Samsung KNOX)** : Mit der Einstellung **Blockieren** wird ein Popupblocker eingeschaltet, der Popups im Webbrowser verhindert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Popups erlauben.

## <a name="allow-or-block-apps"></a>Zulassen oder Blockieren von Apps

Verwenden Sie diese Einstellungen zum Zulassen und Blockieren bzw. Ausblenden bestimmter Apps auf Samsung KNOX Standard-Geräten. Ausgeblendete Apps können nicht von Benutzern geöffnet oder ausgeführt werden.

Folgende Optionen sind verfügbar:

- **Zur Installation zugelassene Apps (nur Samsung KNOX Standard):** Fügen Sie Apps hinzu, die von Benutzern installiert werden können. Benutzer können keine Apps installieren, die nicht in der Liste enthalten sind.
- **Apps, deren Start blockiert wird (nur Samsung KNOX Standard):** Geben Sie die Apps ein, die Benutzer nicht auf ihrem Gerät ausführen können.
- **Für den Benutzer ausgeblendete Apps (nur Samsung KNOX Standard):** Geben Sie die Apps ein, die auf Geräten ausgeblendet sind. Benutzer können diese Apps nicht ermitteln oder ausführen.

Fügen Sie für jede Einstellung Ihre Apps hinzu:

- **Apps nach Paketnamen hinzufügen**: Geben Sie den Namen der App und den Namen des App-Pakets ein. Hauptsächlich für branchenspezifische Apps verwendet. 
- **Apps nach URL hinzufügen**: Geben Sie den Namen der App und ihre URL im Google Play Store ein.
- **Store-App hinzufügen:** Wählen Sie eine App aus der vorhandenen Liste von Apps aus, die Sie in Intune verwalten.

## <a name="cloud-and-storage"></a>Cloud und Speicher

- **Google-Sicherung (nur Samsung KNOX)** : **Blockieren** verhindert, dass Geräte mit der Google-Sicherung synchronisiert werden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Verwendung der Google-Sicherung zulassen.
- **Automatische Synchronisierung des Google-Kontos (nur Samsung KNOX)** : **Blockieren** verhindert das Feature zur automatischen Synchronisierung für das Google-Konto auf Geräten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die automatische Synchronisierung der Einstellungen von Google-Konten zulassen.
- **Wechselmedien (nur Samsung KNOX)** : **Blockieren** hindert Geräte daran, Wechselmedien zu verwenden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Geräten ermöglichen, Wechselmedien wie eine SD-Karte zu verwenden.
- **Verschlüsselung auf Speicherkarten (nur Samsung KNOX)** : **Anfordern** erzwingt, dass Speicherkarten verschlüsselt werden müssen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Verwendung nicht verschlüsselter Speicherkarten zulassen. Nicht alle Geräte unterstützen die Speicherkartenverschlüsselung. Wenden Sie sich zur Bestätigung an den Gerätehersteller.

## <a name="cellular-and-connectivity"></a>Mobilfunk und Konnektivität

- **Datenroaming (nur Samsung KNOX)** : **Blockieren** verhindert das Datenroaming über das Mobilfunknetzwerk. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Es besteht die Möglichkeit, dass das Betriebssystem das Datenroaming standardmäßig zulässt.
- **SMS-/MMS-Nachrichten (nur Samsung KNOX)** : **Blockieren** verhindert das Verfassen von Textnachrichten auf Geräten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem das Senden von Nachrichten per SMS und MMS erlauben.
- **Sprachwahlverfahren (nur Samsung KNOX)** : **Blockieren** hindert Benutzer daran, das Sprachwahlverfahren auf Geräten zu verwenden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem das Sprachwahlverfahren zulassen.
- **Sprachroaming (nur Samsung KNOX)** : **Blockieren** verhindert das Sprachroaming über das Mobilfunknetzwerk. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Es besteht die Möglichkeit, dass das Betriebssystem das Sprachroaming standardmäßig zulässt.
- **Bluetooth (nur Samsung KNOX)** : **Blockieren** verhindert die Verwendung von Bluetooth auf dem Gerät. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Das Betriebssystem erlaubt die Verwendung von Bluetooth möglicherweise standardmäßig.
- **NFC (nur Samsung KNOX)** : Wenn **Blockieren** festgelegt wird, werden Vorgänge deaktiviert, die NFC (Near Field Communication, Nahfeldkommunikation) auf Geräten verwenden, die dieses Feature unterstützen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Es besteht die Möglichkeit, dass das Betriebssystem NFC-Vorgänge standardmäßig zulässt.
- **WLAN (nur Samsung KNOX)** : **Blockieren** verhindert die Verwendung von WLAN auf dem Gerät. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Verwendung von WLAN zulassen.
- **WLAN-Tethering (nur Samsung KNOX)** : Wenn **Blockieren** festgelegt wird, wird das WLAN-Tethering auf Geräten verhindert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Verwendung von WLAN-Tethering zulassen.

## <a name="kiosk"></a>Kiosk

Kioskeinstellungen gelten nur für Samsung KNOX Standard-Geräte, und nur für Apps, die Sie mit Intune verwalten.

- Fügen Sie Apps hinzu, die Sie im Kioskmodus des Geräts ausführen möchten. Im Kioskmodus werden nur die Apps ausgeführt, die Sie hinzufügen; nicht hinzugefügte Apps werden nicht ausgeführt. Vorinstallierte Browser werden nicht ausgeführt, wenn das Gerät sich im Kioskmodus befindet. Wenn ein Browser erforderlich ist, erwägen Sie den Einsatz von [Managed Browser](../apps/app-configuration-managed-browser.md).

  Ihre App-Optionen sind:

  - **Apps nach Paketnamen hinzufügen**: Hauptsächlich für branchenspezifische Apps verwendet. Geben Sie den Namen der App und den Namen des App-Pakets ein.
  - **Apps nach URL hinzufügen**: Geben Sie den Namen der App und ihre URL im Google Play Store ein.
  - **Store-App hinzufügen:** Wählen Sie eine App aus der vorhandenen Liste von Apps aus, die Sie in Intune verwalten.

- **Standbytaste:** **Blockieren** verhindert oder blendet die Schaltfläche für den Standbymodus aus. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Schaltfläche für Standby und Aktivieren auf Geräten zulassen.
- **Lautstärkeregler:** **Blockieren** hindert Benutzer daran, die Lautstärke zu regeln, indem die Lautstärkeregler deaktiviert werden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Verwendung der Lautstärkeregler auf Geräten zulassen.

## <a name="next-steps"></a>Nächste Schritte

[Zuweisen von Profilen](device-profile-assign.md) und [Überwachen von Profilen](device-profile-monitor.md)

Außerdem können Sie Kioskmodusprofile für [Android Enterprise](device-restrictions-android-for-work.md#device-experience)- und [Windows 10](kiosk-settings.md)-Geräte erstellen.
