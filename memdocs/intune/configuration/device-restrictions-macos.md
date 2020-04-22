---
title: 'macOS-Geräteeinstellungen in Microsoft Intune: Azure | Microsoft-Dokumentation'
titleSuffix: ''
description: Fügen Sie Einstellungen auf macOS-Geräten hinzu, und konfigurieren oder erstellen Sie sie, um Funktionen einzuschränken. Hierzu gehören das Festlegen von Anforderungen für Kennwörter, die Anpassung des Sperrbildschirms, die Verwendung integrierter Apps, das Hinzufügen eingeschränkter oder genehmigter Apps, die Handhabung von Bluetooth-Geräten, das Herstellen einer Verbindung zur Cloud für Sicherung und Speicherung, die Aktivierung des Kioskmodus, das Hinzufügen von Domänen und die Steuerung, wie Benutzer mit dem Safari-Webbrowser in Microsoft Intune interagieren.
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
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 50dd3d245b9a89836e3858d71a7ad124189e0973
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "80407846"
---
# <a name="macos-device-settings-to-allow-or-restrict-features-using-intune"></a>macOS-Geräteeinstellungen zum Zulassen oder Einschränken von Funktionen mit Intune

In diesem Artikel werden die verschiedenen Einstellungen aufgeführt und beschrieben, die Sie auf macOS-Geräten steuern können. Verwenden Sie als Bestandteil Ihrer Lösung für die mobile Geräteverwaltung (Mobile Device Management, MDM) diese Einstellungen, um Features zuzulassen oder zu deaktivieren, Kennwortregeln festzulegen, bestimmte Apps zu erlauben oder einzuschränken usw.

Diese Einstellungen werden einem Gerätekonfigurationsprofil in Intune hinzugefügt und dann Ihren macOS-Geräten zugewiesen oder bereitgestellt.

## <a name="before-you-begin"></a>Vorbereitung

[Erstellen Sie ein Konfigurationsprofil mit Geräteeinschränkungen](device-restrictions-configure.md).

> [!NOTE]
> Diese Einstellungen gelten für verschiedene Registrierungstypen. Weitere Informationen zu den verschiedenen Registrierungstypen finden Sie unter [macOS-Registrierung](../enrollment/macos-enroll.md).

## <a name="general"></a>Allgemein

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Die Einstellungen gelten für: Geräteregistrierung und Automatische Geräteregistrierung

- **Definitionssuche**: **Blockieren** hindert Benutzer daran, ein Wort zu markieren und dann auf dem Gerät nach seiner Definition zu suchen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise das Feature Definitionssuche zu.
- **Dictation**: **Blockieren** verhindert, dass Benutzer die Spracheingabe zur Eingabe von Text verwenden können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, die Diktatfunktion zu verwenden.
- **Inhalte zwischenspeichern**: Die Einstellung **Blockieren** verhindert das Zwischenspeichern von Inhalten. Beim Zwischenspeichern von Inhalten werden u. a. App- und Webbrowserdaten und Downloads lokal auf dem Gerät gespeichert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig ist im Betriebssystem möglicherweise das Zwischenspeichern von Inhalten aktiviert.

  Weitere Informationen zum Zwischenspeichern von Inhalten unter macOS finden Sie unter [Verwalten des Inhaltscaching auf dem Mac](https://support.apple.com/guide/mac-help/manage-content-caching-on-mac-mchl3b6c3720/mac) (öffnet eine andere Website).

  Diese Funktion gilt für:  
  - macOS 10.13 und höher

- **Softwareupdates zurückstellen**: **Aktivieren** ermöglicht Ihnen, die Anzeige von Softwareupdates auf Geräten zu verzögern (0-90 Tage). Diese Einstellung steuert nicht, ob Updates installiert werden oder nicht. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig zeigt das Betriebssystem möglicherweise Updates auf dem Gerät an, wenn Apple sie veröffentlicht. Wenn beispielsweise ein macOS-Update von Apple an einem bestimmten Datum veröffentlicht wird, wird dieses Update normalerweise um das Veröffentlichungsdatum auf dem Gerät angezeigt. Updates von Seedbuilds sind ohne Verzögerung zulässig.  

  - **Sichtbarkeit von Softwareupdates verzögern**: Geben Sie einen Wert zwischen 0–90 Tagen ein. Nach der Verzögerung erhalten Benutzer eine Benachrichtigung für ein Update auf die früheste Version des Betriebssystems, die verfügbar war, als die Verzögerung ausgelöst wurde.

    Wenn beispielsweise ein macOS-Update am **1. Januar** verfügbar ist und **Delay visibility** (Sichtbarkeit verzögern) auf **5 Tage** festgelegt ist, wird das Update nicht als verfügbares Update angezeigt. Am **6. Tag** nach Veröffentlichung ist dieses Update verfügbar, sodass Benutzer es installieren können.

    Diese Funktion gilt für:  
    - macOS 10.13.4 und höher

- **Screenshots**: Das Gerät muss bei der automatischen Geräteregistrierung (DEP) von Apple registriert sein. Die Einstellung **Blockieren** verhindert, dass Benutzer Screenshots des Displays speichern. Außerdem wird verhindert, dass die Classroom-App Remotebildschirme überwacht. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise zu, dass Benutzer Screenshots erstellen und die Classroom-App Remotebildschirme anzeigt.

### <a name="settings-apply-to-automated-device-enrollment"></a>Die Einstellungen gelten für: Automatisierte Geräteregistrierung

- **Remotebildschirmüberwachung über Classroom-App** Mit der Einstellung **Deaktivieren** wird verhindert, dass Lehrkräfte über die Classroom-App die Bildschirme der Kursteilnehmer anzeigen können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise zu, dass Lehrkräfte die Bildschirme der Kursteilnehmer anzeigen.

  Legen Sie hierfür den Wert für **Screenshots** auf **Nicht konfiguriert** fest (Screenshots sind zulässig).

- **Unangekündigte Bildschirmüberwachung über Classroom-App**: Mit der Einstellung **Zulassen** ist es Lehrkräften möglich, die Bildschirme der Kursteilnehmer ohne deren Zustimmung anzuzeigen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig ist im Betriebssystem möglicherweise die Zustimmung der Kursteilnehmer erforderlich, damit Lehrkräfte die Bildschirme anzeigen können.

  Legen Sie hierfür den Wert für **Screenshots** auf **Nicht konfiguriert** fest (Screenshots sind zulässig).

- **Schüler müssen die Berechtigung zum Verlassen der Classroom-Klasse anfordern**: Mit der Einstellung **Anfordern** müssen Kursteilnehmer, die bei einem nicht verwalteten Classroom-Kurs angemeldet sind, zum Verlassen des Kurses die Erlaubnis der Lehrkraft anfordern. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise zu, dass die Kursteilnehmer den Kurs jederzeit verlassen können.

- **Lehrkräfte können Geräte oder Apps in der Classroom-App automatisch sperren**: Durch die Einstellung **Zulassen** können Lehrkräfte das Gerät oder die App eines Kursteilnehmers ohne dessen Genehmigung sperren. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig ist im Betriebssystem möglicherweise die Zustimmung der Kursteilnehmer erforderlich, damit Lehrkräfte das Gerät oder die App sperren können.

- **Schüler können der Classroom-Klasse automatisch beitreten:** Durch die Einstellung **Zulassen** können Kursteilnehmer ohne Aufforderung des Lehrers einem Kurs beitreten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig ist im Betriebssystem möglicherweise für den Beitritt zu einer Klasse die Zustimmung der Lehrkraft erforderlich.

## <a name="password"></a>Kennwort

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Die Einstellungen gelten für: Geräteregistrierung und Automatische Geräteregistrierung

- **Kennwort:** Wenn **Erforderlich** festgelegt wird, müssen Benutzer ein Kennwort eingeben, um auf Geräte zuzugreifen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig fordert das Betriebssystem möglicherweise kein Kennwort. Außerdem werden keine Einschränkungen erzwungen, wie z. B. das Blockieren einfacher Kennwörter oder das Festlegen einer Mindestlänge.
  - **Erforderlicher Kennworttyp:** Geben Sie den von Ihrer Organisation geforderten Grad der Kennwortkomplexität an. Folgende Optionen sind verfügbar:
    - **Nicht konfiguriert:** Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
    - **Numerisch**: Das Kennwort darf nur aus Zahlen bestehen, z. B. 123456789.
    - **Alphanumerisch**: Schließt Großbuchstaben, Kleinbuchstaben und Ziffern ein.

    Diese Funktion gilt für:  
    - macOS 10.10.3 und höher

  - **Anzahl nicht alphanumerischer Zeichen im Kennwort:** Geben Sie die Anzahl komplexer Zeichen ein, die das Kennwort enthalten muss (0 bis 4). Bei komplexen Zeichen handelt es sich um Symbole, z. B. `?`.
  - **Minimale Kennwortlänge:** Geben Sie die Mindestlänge des Kennworts ein (4 bis 16 Zeichen).
  - **Einfache Kennwörter:** Einfache Kennwörter wie `0000` oder `1234` sind zulässig.
  - **Maximaler Zeitraum der Bildschirmsperre (in Minuten) bis zur Anforderung eines Kennworts**: Geben Sie an, wie lange ein Gerät inaktiv sein muss, bevor es mithilfe eines Kennworts entsperrt werden muss. Wenn kein Wert angegeben oder **Nicht konfiguriert** festgelegt ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.
  - **Maximaler Zeitraum der Inaktivität (in Minuten) bis zur Bildschirmsperrung:** Geben Sie den Zeitraum an, für den sich ein Gerät im Leerlauf befinden muss, bevor der Bildschirm automatisch gesperrt wird. Geben Sie zum Beispiel 5 ein, um Geräte nach 5 Minuten im Leerlauf zu sperren. Wenn kein Wert angegeben oder **Nicht konfiguriert** festgelegt ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.
  - **Kennwortablauf (Tage):** Geben Sie die Anzahl der Tage von 1 bis 65535 an, bis das Gerätekennwort geändert werden muss. Geben Sie beispielsweise `90` an, damit das Kennwort nach 90 Tagen abläuft. Wenn das Kennwort abläuft, werden Benutzer aufgefordert, ein neues Kennwort zu erstellen. Wenn kein Wert angegeben ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.
  - **Wiederverwendung vorheriger Kennwörter verhindern:** Verwenden Sie diese Einstellung, um zu verhindern, dass Benutzer zuvor verwendete Kennwörter erstellen. Geben Sie die Anzahl der zuvor verwendeten Kennwörter ein, die nicht erneut verwendet werden können, von 1–24. Geben Sie z. B. 5 an, damit ein Benutzer als sein neues Kennwort nicht sein aktuelles Kennwort oder eines seiner vorherigen vier Kennwörter festlegen kann. Wenn kein Wert angegeben ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.

- **Ändern des Passcodes durch Benutzer blockieren**: **Blockieren** verhindert, dass die Kennung geändert, hinzugefügt oder entfernt wird. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem erlauben, Passcodes hinzuzufügen, zu ändern oder zu entfernen.
- **Entsperren per Fingerabdruck blockieren**: Die Einstellung **Blockieren** verhindert die Verwendung von Fingerabdrücken zum Entsperren von Geräten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise zu, dass Benutzer das Gerät per Fingerabdruck entsperren.

- **AutoAusfüllen für Kennwörter blockieren**: Die Einstellung **Blockieren** verhindert die Verwendung des Features zum automatischen Ausfüllen von Kennwörtern unter macOS. Das Wählen von **Blockieren** bewirkt auch Folgendes:

  - Benutzer werden nicht aufgefordert, in Safari oder beliebigen Apps gespeicherte Kennwörter zu verwenden.
  - Automatische sichere Kennwörter sind deaktiviert, und sichere Kennwörter werden Benutzern nicht empfohlen.

  Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem diese Funktionen zulassen.

- **Kennwortanforderungen durch Näherung blockieren**: Die Einstellung **Blockieren** verhindert, dass Geräte Kennwörter von Geräten in der Nähe anfordern. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem diese Kennwortanforderungen zulassen.

- **Kennwortfreigabe blockieren**: **Blockieren** verhindert die Freigabe von Kennwörtern zwischen Geräten mit AirDrop. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem das Freigeben von Kennwörtern zulassen.

## <a name="built-in-apps"></a>Integrierte Apps

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Die Einstellungen gelten für: Geräteregistrierung und Automatische Geräteregistrierung

- **AutoAusfüllen in Safari blockieren**: Die Einstellung **Blockieren** deaktiviert das Feature zum automatischen Ausfüllen in Safari auf Geräten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, Einstellungen für AutoVervollständigen im Webbrowser zu ändern.
- **Kamera blockieren**: Die Einstellung **Blockieren** verhindert den Zugriff auf die Kamera des Geräts. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise den Zugriff auf die Kamera des Geräts zu.

  Intune verwaltet nur den Zugriff auf die Kamera des Geräts. Das Programm kann nicht auf Bilder oder Videos zugreifen.

- **Apple Music blockieren**: Die Einstellung **Blockieren** setzt die App Music in den klassischen Modus zurück und deaktiviert den Dienst Music. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Verwendung der Apple Music-App zulassen.
- **Internetsuchergebnisse für Spotlight blockieren**: **Blockieren** verhindert, dass Spotlight Ergebnisse einer Internetsuche zurückgibt. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise zu, dass die Spotlight-Suchfunktion eine Verbindung mit dem Internet herstellt und dort Suchergebnisse abruft.
- **Dateiübertragung über iTunes blockieren**: **Blockieren** deaktiviert Dateifreigabedienste der Anwendung. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise Freigabedienste für Anwendungsdateien zu.

  Diese Funktion gilt für:  
  - macOS 10.13 und höher

## <a name="restricted-apps"></a>Eingeschränkte Apps

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Die Einstellungen gelten für: Geräteregistrierung und Automatische Geräteregistrierung

- **Liste der eingeschränkten App-Typen:** Mit dieser Einstellung wird eine Liste der Apps erstellt, die Benutzer nicht installieren oder verwenden dürfen. Folgende Optionen sind verfügbar:

  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Standardmäßig können Benutzer möglicherweise auf von Ihnen zugewiesene Apps und integrierte Apps zugreifen.
  - **Unzulässige Apps:** Listen Sie die (nicht von Intune verwalteten) Apps auf, die Benutzer nicht installieren und ausführen dürfen. Benutzer können unzulässige Apps nicht installieren. Wenn ein Benutzer eine App aus dieser Liste installiert, wird dies in Intune gemeldet.
  - **Genehmigte Apps:** Listet die Apps auf, die Benutzer installieren dürfen. Um die Kompatibilität zu gewährleisten, dürfen Benutzer keine anderen Apps installieren. Apps, die von Intune verwaltet werden, sind automatisch zugelassen, einschließlich der Unternehmensportal-App. Benutzer werden nicht daran gehindert, eine App zu installieren, die nicht in der Liste zulässiger Apps enthalten ist. Wenn sie es jedoch tun, wird dies in Intune gemeldet.

- **App-Bündel-ID:** Geben Sie die [App-Bündel-ID](bundle-ids-built-in-ios-apps.md) der gewünschten App ein. Sie können sowohl integrierte Apps als auch branchenspezifische Apps anzeigen oder ausblenden. Eine Liste der integrierten Apple-Apps finden Sie auf [dieser Apple-Website](https://support.apple.com/HT208094).
- **App-Name:** Geben Sie den App-Namen der gewünschten App ein. Sie können sowohl integrierte Apps als auch branchenspezifische Apps anzeigen oder ausblenden. Eine Liste der integrierten Apple-Apps finden Sie auf [dieser Apple-Website](https://support.apple.com/HT208094).
- **Herausgeber**: Geben Sie den Herausgeber der App an.

Um diesen Listen Apps hinzuzufügen, können Sie:

- **Hinzufügen**: Verwenden Sie diese Option, um Ihre Liste mit Apps zu erstellen.
- **Importieren** Sie eine CSV-Datei mit den Details der App, einschließlich der URL. Verwenden Sie das Format `<app bundle ID>, <app name>, <app publisher>`. Oder **exportieren** Sie eine Datei im selben Format, um eine Liste der hinzugefügten Apps zu erstellen.

## <a name="connected-devices"></a>Verbundene Geräte

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Die Einstellungen gelten für: Geräteregistrierung und Automatische Geräteregistrierung

- **AirDrop blockieren**: Die Einstellung **Blockieren** verhindert die Verwendung von AirDrop auf Geräten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Verwendung von AirDrop zum Austauschen von Inhalten mit Geräten in der Nähe zulassen.
- **Automatisches Entsperren mit Apple Watch blockieren**: **Blockieren** hindert Benutzer daran, ihr macOS-Gerät mit ihrer Apple Watch zu entsperren. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise zu, dass Benutzer ihr macOS-Gerät mit ihrer Apple Watch entsperren.

## <a name="cloud-and-storage"></a>Cloud und Speicher

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Die Einstellungen gelten für: Geräteregistrierung und Automatische Geräteregistrierung

- **Synchronisierung zwischen iCloud und Keychain blockieren:** **Blockieren** deaktiviert die Synchronisierung in Keychain gespeicherter Anmeldeinformationen mit iCloud. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, diese Anmeldeinformationen zu synchronisieren.
- **iCloud-Dokumentsynchronisierung blockieren**: **Blockieren** hindert iCloud daran, Dokumente und Daten zu synchronisieren. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Dokument- und Schlüssel-/Wertsynchronisierung in Ihrem iCloud-Speicher zulassen.
- **iCloud-E-Mail-Sicherung blockieren**: **Blockieren** hindert iCloud an der Synchronisierung mit der macOS-App „Mail“. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise die Synchronisierung der Mail-App mit iCloud zu.
- **iCloud-Kontaktsicherung blockieren**: Die Einstellung **Blockieren** hindert iCloud an der Synchronisierung der Kontakte auf dem Gerät. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise die Synchronisierung von Kontakten mit iCloud zu.
- **iCloud-Kalendersicherung blockieren**: **Blockieren** hindert iCloud an der Synchronisierung mit der Kalender-App von macOS. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise die Synchronisierung der Kalender-App mit iCloud zu.
- **iCloud-Sicherung von Erinnerungen blockieren**: **Blockieren** hindert iCloud an der Synchronisierung mit der Erinnerungen-App von macOS. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise die Synchronisierung der Erinnerungen-App mit iCloud zu.
- **iCloud-Lesezeichensicherung blockieren**: Die Einstellung **Blockieren** hindert iCloud an der Synchronisierung der Lesezeichen auf dem Gerät. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise die Synchronisierung von Lesezeichen mit iCloud zu.
- **iCloud-Notizensicherung blockieren**: Die Einstellung **Blockieren** hindert iCloud an der Synchronisierung der Notizen auf dem Gerät. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise die Synchronisierung von Notizen mit iCloud zu.
- **iCloud-Fotomediathek blockieren**: Mit der Einstellung **Blockieren** wird die iCloud-Fotomediathek deaktiviert und die Synchronisierung der Fotos auf dem Gerät mit iCloud verhindert. Fotos, die nicht vollständig aus der iCloud-Fotomediathek heruntergeladen wurden, werden aus dem lokalen Speicher des jeweiligen Geräts entfernt. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise die Synchronisierung von Fotos zwischen dem Gerät und der iCloud-Fotomediathek zu.
- **Handoff:** Mit diesem Feature können Benutzer mit der Arbeit auf einem macOS-Gerät beginnen und ihre Arbeit auf einem anderen iOS-/iPadOS- oder macOS-Gerät fortsetzen. Mit der Einstellung **Blockieren** wird verhindert, dass das Handoff-Feature auf dem Gerät verwendet wird. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise dieses Feature auf Geräten zu.

  Diese Funktion gilt für:  
  - macOS 10.15 und neuer

## <a name="domains"></a>Domänen

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Die Einstellungen gelten für: Geräteregistrierung und Automatische Geräteregistrierung

- **E-Mail-Domänen-URL**: **Fügen** Sie der Liste eine oder mehrere URLs hinzu. Wenn Benutzer eine E-Mail von einer Domäne erhalten, die Sie nicht konfiguriert haben, wird die E-Mail in der macOS-Mail-App als nicht vertrauenswürdig gekennzeichnet.

## <a name="next-steps"></a>Nächste Schritte

[Zuweisen von Profilen](device-profile-assign.md) und [Überwachen von Profilen](device-profile-monitor.md)

Sie können auch Gerätefunktionen und -einstellungen auf [iOS-/iPadOS](device-restrictions-ios.md)-Geräten einschränken.
