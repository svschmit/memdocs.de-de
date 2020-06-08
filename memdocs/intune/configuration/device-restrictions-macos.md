---
title: 'macOS-Geräteeinstellungen in Microsoft Intune: Azure | Microsoft-Dokumentation'
titleSuffix: ''
description: Fügen Sie Einstellungen auf macOS-Geräten hinzu, und konfigurieren oder erstellen Sie sie, um Funktionen einzuschränken. Hierzu gehören das Festlegen von Anforderungen für Kennwörter, die Anpassung des Sperrbildschirms, die Verwendung integrierter Apps, das Hinzufügen eingeschränkter oder genehmigter Apps, die Handhabung von Bluetooth-Geräten, das Herstellen einer Verbindung zur Cloud für Sicherung und Speicherung, die Aktivierung des Kioskmodus, das Hinzufügen von Domänen und die Steuerung, wie Benutzer mit dem Safari-Webbrowser in Microsoft Intune interagieren.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/06/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: kakyker; annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e48ba131d97e68570f1d6cb85b285ddc3198971c
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429751"
---
# <a name="macos-device-settings-to-allow-or-restrict-features-using-intune"></a>macOS-Geräteeinstellungen zum Zulassen oder Einschränken von Funktionen mit Intune

In diesem Artikel werden die verschiedenen Einstellungen aufgeführt und beschrieben, die Sie auf macOS-Geräten steuern können. Verwenden Sie als Bestandteil Ihrer Lösung für die mobile Geräteverwaltung (Mobile Device Management, MDM) diese Einstellungen, um Features zuzulassen oder zu deaktivieren, Kennwortregeln festzulegen, bestimmte Apps zu erlauben oder einzuschränken usw.

Diese Einstellungen werden einem Gerätekonfigurationsprofil in Intune hinzugefügt und dann Ihren macOS-Geräten zugewiesen oder bereitgestellt.

> [!NOTE]
> Die Benutzeroberfläche stimmt möglicherweise nicht mit den Registrierungstypen in diesem Artikel überein. Die Informationen in diesem Artikel sind richtig. Die Benutzeroberfläche wird in einem zukünftigen Release aktualisiert.

## <a name="before-you-begin"></a>Vorbereitung

[Erstellen Sie ein macOS-Konfigurationsprofil mit Geräteeinschränkungen](device-restrictions-configure.md).

> [!NOTE]
> Diese Einstellungen gelten für verschiedene Registrierungstypen. Weitere Informationen zu den verschiedenen Registrierungstypen finden Sie unter [macOS-Registrierung](../enrollment/macos-enroll.md).

## <a name="built-in-apps"></a>Integrierte Apps

### <a name="settings-apply-to-all-enrollment-types"></a>Die Einstellungen gelten für: Alle Registrierungstypen

- **AutoAusfüllen in Safari blockieren**: Die Einstellung **Ja** deaktiviert das Feature zum automatischen Ausfüllen in Safari auf Geräten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, Einstellungen für AutoVervollständigen im Webbrowser zu ändern.
- **Verwendung der Kamera blockieren**: Die Einstellung **Ja** verhindert den Zugriff auf die Kamera des Geräts. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise den Zugriff auf die Kamera des Geräts zu.

  Intune verwaltet nur den Zugriff auf die Kamera des Geräts. Das Programm kann nicht auf Bilder oder Videos zugreifen.
  
- **Apple Music blockieren**: Die Einstellung **Ja** setzt die Music-App in den klassischen Modus zurück und deaktiviert den Music-Dienst. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Verwendung der Apple Music-App zulassen.
- **Spotlight-Vorschläge blockieren**: **Ja** verhindert, dass Spotlight Ergebnisse einer Internetsuche zurückgibt. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise zu, dass die Spotlight-Suchfunktion eine Verbindung mit dem Internet herstellt und dort Suchergebnisse abruft.
- **Blockieren der Dateiübertragung mit Finder oder iTunes**: **Ja** deaktiviert Dateifreigabedienste der Anwendung. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise Freigabedienste für Anwendungsdateien zu.

  Diese Funktion gilt für:  
  - macOS 10.13 und höher

## <a name="cloud-and-storage"></a>Cloud und Speicher

### <a name="settings-apply-to-all-enrollment-types"></a>Die Einstellungen gelten für: Alle Registrierungstypen

- **Synchronisierung zwischen iCloud und Keychain blockieren:** **Ja** deaktiviert die Synchronisierung in Keychain gespeicherter Anmeldeinformationen mit iCloud. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, diese Anmeldeinformationen zu synchronisieren.
- **iCloud-Desktop- und -Dokumentsynchronisierung blockieren**: **Ja** hindert iCloud daran, Dokumente und Daten zu synchronisieren. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Dokument- und Schlüssel-/Wertsynchronisierung in Ihrem iCloud-Speicher zulassen.
- **iCloud-E-Mail-Sicherung blockieren**: **Ja** hindert iCloud an der Synchronisierung mit der macOS-App „Mail“. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise die Synchronisierung der Mail-App mit iCloud zu.
- **iCloud-Kontaktsicherung blockieren**: **Ja** hindert iCloud an der Synchronisierung der Kontakte auf dem Gerät. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise die Synchronisierung von Kontakten mit iCloud zu.
- **iCloud-Kalendersicherung blockieren**: **Ja** hindert iCloud an der Synchronisierung mit der Kalender-App von macOS. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise die Synchronisierung der Kalender-App mit iCloud zu.
- **iCloud-Sicherung von Erinnerungen blockieren**: **Ja** hindert iCloud an der Synchronisierung mit der Erinnerungen-App von macOS. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise die Synchronisierung der Erinnerungen-App mit iCloud zu.
- **iCloud-Lesezeichensicherung blockieren**: **Ja** hindert iCloud an der Synchronisierung der Lesezeichen auf dem Gerät. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise die Synchronisierung von Lesezeichen mit iCloud zu.
- **iCloud-Notizensicherung blockieren**: **Ja** hindert iCloud an der Synchronisierung der Notizen auf dem Gerät. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise die Synchronisierung von Notizen mit iCloud zu.
- **Sicherung von iCloud-Fotos blockieren**: **Ja** deaktiviert die iCloud-Fotomediathek und verhindert die Synchronisierung der Fotos auf dem Gerät mit iCloud. Fotos, die nicht vollständig aus der iCloud-Fotomediathek heruntergeladen wurden, werden aus dem lokalen Speicher des jeweiligen Geräts entfernt. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise die Synchronisierung von Fotos zwischen dem Gerät und der iCloud-Fotomediathek zu.
- **Handoff blockieren**: Mit diesem Feature können Benutzer mit der Arbeit auf einem macOS-Gerät beginnen und ihre Arbeit auf einem anderen iOS-/iPadOS- oder macOS-Gerät fortsetzen. **Ja** verhindert, dass das Handoff-Feature auf Geräten verwendet wird. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise dieses Feature auf Geräten zu.

  Diese Funktion gilt für:  
  - macOS 10.15 und neuer

## <a name="connected-devices"></a>Verbundene Geräte

### <a name="settings-apply-to-all-enrollment-types"></a>Die Einstellungen gelten für: Alle Registrierungstypen

- **AirDrop blockieren**: **Ja** verhindert die Verwendung von AirDrop auf Geräten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Verwendung von AirDrop zum Austauschen von Inhalten mit Geräten in der Nähe zulassen.
- **Automatisches Entsperren mit Apple Watch blockieren**: **Ja** hindert Benutzer daran, ihr macOS-Gerät mit ihrer Apple Watch zu entsperren. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise zu, dass Benutzer ihr macOS-Gerät mit ihrer Apple Watch entsperren.

## <a name="domains"></a>Domänen

### <a name="settings-apply-to-all-enrollment-types"></a>Die Einstellungen gelten für: Alle Registrierungstypen

- **Nicht markierte E-Mail-Domänen**: Geben Sie der Liste mindestens eine **E-Mail-Domänen-URL** hinzu. Wenn Benutzer eine E-Mail von einer anderen Domäne als den von Ihnen hinzugefügten senden oder empfangen, wird die E-Mail in der macOS-Mail-App als nicht vertrauenswürdig gekennzeichnet.

## <a name="general"></a>Allgemein

### <a name="settings-apply-to-all-enrollment-types"></a>Die Einstellungen gelten für: Alle Registrierungstypen

- **Suche blockieren**: **Ja** hindert Benutzer daran, ein Wort zu markieren und dann auf dem Gerät nach seiner Definition zu suchen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise das Feature Definitionssuche zu.
- **Diktatfunktion blockieren**: **Ja** verhindert, dass Benutzer die Spracheingabe zur Eingabe von Text verwenden können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, die Diktatfunktion zu verwenden.
- **Content Caching blockieren**: **Ja** verhindert das Zwischenspeichern von Inhalten. Beim Zwischenspeichern von Inhalten werden u. a. App- und Webbrowserdaten und Downloads lokal auf dem Gerät gespeichert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig ist im Betriebssystem möglicherweise das Zwischenspeichern von Inhalten aktiviert.

  Weitere Informationen zum Zwischenspeichern von Inhalten unter macOS finden Sie unter [Verwalten des Inhaltscaching auf dem Mac](https://support.apple.com/guide/mac-help/manage-content-caching-on-mac-mchl3b6c3720/mac) (öffnet eine andere Website).

  Diese Funktion gilt für:  
  - macOS 10.13 und höher

- **Softwareupdates zurückstellen**: **Ja** ermöglicht Ihnen, die Anzeige von Softwareupdates auf Geräten zu verzögern (0 bis 90 Tage). Diese Einstellung steuert nicht, ob Updates installiert werden oder nicht. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig zeigt das Betriebssystem möglicherweise Updates auf dem Gerät an, wenn Apple sie veröffentlicht. Wenn beispielsweise ein macOS-Update von Apple an einem bestimmten Datum veröffentlicht wird, wird dieses Update normalerweise um das Veröffentlichungsdatum auf dem Gerät angezeigt. Updates von Seedbuilds sind ohne Verzögerung zulässig.  

  - **Sichtbarkeit von Softwareupdates verzögern**: Geben Sie einen Wert zwischen 0–90 Tagen ein. Nach der Verzögerung erhalten Benutzer eine Benachrichtigung für ein Update auf die früheste Version des Betriebssystems, die verfügbar war, als die Verzögerung ausgelöst wurde.

    Wenn beispielsweise ein macOS-Update am **1. Januar** verfügbar ist und **Delay visibility** (Sichtbarkeit verzögern) auf **5 Tage** festgelegt ist, wird das Update nicht als verfügbares Update angezeigt. Am **6. Tag** nach Veröffentlichung ist dieses Update verfügbar, sodass Benutzer es installieren können.

    Diese Funktion gilt für:  
    - macOS 10.13.4 und höher

- **Screenshots und Bildschirmaufzeichnungen blockieren**: Das Gerät muss bei der automatischen Geräteregistrierung (DEP) von Apple registriert sein. **Ja** verhindert, dass Benutzer Screenshots des Displays speichern. Außerdem wird verhindert, dass die Classroom-App Remotebildschirme überwacht. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise zu, dass Benutzer Screenshots erstellen und die Classroom-App Remotebildschirme anzeigt.

  - **AirPlay, Bildschirmanzeige durch Classroom-App und Bildschirmübertragung blockieren**: **Ja** blockiert AirPlay und verhindert die Bildschirmfreigabe für andere Geräte. Die Einstellung verhindert außerdem, dass Lehrkräfte über die Classroom-App die Bildschirme der Kursteilnehmer anzeigen können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise zu, dass Lehrkräfte die Bildschirme der Kursteilnehmer anzeigen.

    Legen Sie hierfür die Einstellung **Screenshots und Bildschirmaufzeichnungen blockieren** auf **Nicht konfiguriert** fest (Screenshots sind zulässig).

  - **Der Classroom-App das Ausführen von Airplay und die Bildschirmanzeige ohne Bestätigung erlauben**: Mit der Einstellung **Ja** ist es Lehrkräften möglich, die Bildschirme der Kursteilnehmer ohne deren Zustimmung anzuzeigen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig ist im Betriebssystem möglicherweise die Zustimmung der Kursteilnehmer erforderlich, damit Lehrkräfte die Bildschirme anzeigen können.

    Legen Sie hierfür die Einstellung **Screenshots und Bildschirmaufzeichnungen blockieren** auf **Nicht konfiguriert** fest (Screenshots sind zulässig).

- **Dozentenberechtigung zum Verlassen von nicht verwalteten Classroom-App-Kursen erforderlich**: Mit der Einstellung **Ja** müssen Kursteilnehmer, die bei einem nicht verwalteten Classroom-Kurs angemeldet sind, zum Verlassen des Kurses die Erlaubnis der Lehrkraft anfordern. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise zu, dass die Kursteilnehmer den Kurs jederzeit verlassen können.

- **Classroom das Sperren des Geräts ohne Bestätigung erlauben**: Durch die Einstellung **Ja** können Lehrkräfte das Gerät oder die App eines Kursteilnehmers ohne dessen Genehmigung sperren. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig ist im Betriebssystem möglicherweise die Zustimmung der Kursteilnehmer erforderlich, damit Lehrkräfte das Gerät oder die App sperren können.

- **Schülern den automatischen Beitritt zur Classroom-Klasse ohne Bestätigung erlauben**: Durch die Einstellung **Ja** können Kursteilnehmer ohne Aufforderung des Lehrers einem Kurs beitreten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig ist im Betriebssystem möglicherweise für den Beitritt zu einer Klasse die Zustimmung der Lehrkraft erforderlich.

## <a name="password"></a>Kennwort

### <a name="settings-apply-to-all-enrollment-types"></a>Die Einstellungen gelten für: Alle Registrierungstypen

- **Kennwort anfordern**: Wenn **Ja** festgelegt wird, müssen Benutzer ein Kennwort eingeben, um auf Geräte zuzugreifen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig fordert das Betriebssystem möglicherweise kein Kennwort. Außerdem werden keine Einschränkungen erzwungen, wie z. B. das Blockieren einfacher Kennwörter oder das Festlegen einer Mindestlänge.
  - **Erforderlicher Kennworttyp:** Geben Sie den von Ihrer Organisation geforderten Grad der Kennwortkomplexität an. Wenn kein Wert angegeben wird, ändetr oder aktualisiert Intune diese Einstellung nicht. Folgende Optionen sind verfügbar:
    - **Nicht konfiguriert:** Verwendet den Standardwert des Geräts.
    - **Alphanumerisch**: Schließt Großbuchstaben, Kleinbuchstaben und Ziffern ein.
    - **Numerisch**: Das Kennwort darf nur aus Zahlen bestehen, z. B. 123456789.

    Diese Funktion gilt für:  
    - macOS 10.10.3 und höher

  - **Anzahl nicht alphanumerischer Zeichen im Kennwort:** Geben Sie die Anzahl komplexer Zeichen ein, die das Kennwort enthalten muss (0 bis 4). Bei komplexen Zeichen handelt es sich um Symbole, z. B. `?`. Wenn kein Wert angegeben oder die Einstellung auf **Nicht konfiguriert** festgelegt wird, wird diese Einstellung von Intune nicht geändert oder aktualisiert.
  - **Minimale Kennwortlänge:** Geben Sie die Mindestlänge des Kennworts ein (4 bis 16 Zeichen). Wenn kein Wert angegeben wird, ändetr oder aktualisiert Intune diese Einstellung nicht.
  - **Einfache Kennwörter blockieren**: **Ja** verhindert, dass einfache Kennwörter wie `0000` oder `1234` verwendet werden können. Wenn kein Wert angegeben oder **Nicht konfiguriert** festgelegt ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem einfache Kennwörter zulassen.
  - **Maximaler Zeitraum der Inaktivität (in Minuten) bis zur Bildschirmsperrung:** Geben Sie den Zeitraum an, für den sich ein Gerät im Leerlauf befinden muss, bevor der Bildschirm automatisch gesperrt wird. Geben Sie zum Beispiel `5` ein, um Geräte nach 5 Minuten im Leerlauf zu sperren. Wenn kein Wert angegeben oder **Nicht konfiguriert** festgelegt ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.
  - **Maximaler Zeitraum der Bildschirmsperre (in Minuten) bis zur Anforderung eines Kennworts**: Geben Sie an, wie lange ein Gerät inaktiv sein muss, bevor es mithilfe eines Kennworts entsperrt werden muss. Wenn kein Wert angegeben oder **Nicht konfiguriert** festgelegt ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.
  - **Kennwortablauf (Tage):** Geben Sie die Anzahl der Tage von 1 bis 65535 an, bis das Gerätekennwort geändert werden muss. Geben Sie beispielsweise `90` an, damit das Kennwort nach 90 Tagen abläuft. Wenn das Kennwort abläuft, werden Benutzer aufgefordert, ein neues Kennwort zu erstellen. Wenn kein Wert angegeben oder **Nicht konfiguriert** festgelegt ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.
  - **Wiederverwendung vorheriger Kennwörter verhindern:** Verhindert, dass Benutzer zuvor verwendete Kennwörter erstellen. Geben Sie die Anzahl der zuvor verwendeten Kennwörter ein, die nicht erneut verwendet werden können, von 1–24. Geben Sie z. B. 5 an, damit ein Benutzer als sein neues Kennwort nicht sein aktuelles Kennwort oder eines seiner vorherigen vier Kennwörter festlegen kann. Wenn kein Wert angegeben ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.

- **Ändern des Passcodes durch Benutzer blockieren**: **Ja** verhindert, dass der Passcode geändert, hinzugefügt oder entfernt wird. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem erlauben, Passcodes hinzuzufügen, zu ändern oder zu entfernen.

- **Touch ID zum Entsperren des Geräts blockieren**: **Ja** verhindert die Verwendung von Fingerabdrücken zum Entsperren von Geräten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise zu, dass Benutzer das Gerät per Fingerabdruck entsperren.

- **AutoAusfüllen für Kennwörter blockieren**: **Ja** verhindert die Verwendung des Features zum automatischen Ausfüllen von Kennwörtern unter macOS. Das Auswählen von **Ja** bewirkt auch Folgendes:

  - Benutzer werden nicht aufgefordert, in Safari oder beliebigen Apps gespeicherte Kennwörter zu verwenden.
  - Automatische sichere Kennwörter sind deaktiviert, und sichere Kennwörter werden Benutzern nicht empfohlen.

  Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem diese Funktionen zulassen.

- **Kennwortanforderungen durch Näherung blockieren**: **Ja** verhindert, dass Geräte Kennwörter von Geräten in der Nähe anfordern. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem diese Kennwortanforderungen zulassen.

- **Kennwortfreigabe blockieren**: **Ja** verhindert die Freigabe von Kennwörtern zwischen Geräten mit AirDrop. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem das Freigeben von Kennwörtern zulassen.

## <a name="privacy-preferences"></a>Datenschutzeinstellungen

Auf macOS-Geräten fordern Anwendungen und Prozesse Benutzer häufig auf, den Zugriff auf Gerätefunktionen wie Kamera, Mikrofon, Kalender, Ordner „Dokumente“ und mehr zu erlauben oder zu verweigern. Diese Einstellungen ermöglichen es Administratoren, den Zugriff auf diese Gerätefunktionen vorab zu genehmigen oder zu verweigern. Wenn Sie diese Einstellungen konfigurieren, verwalten Sie die Datenzugriffseinwilligung für Ihre Benutzer. Ihre Einstellungen überschreiben die vorherigen Entscheidungen der Benutzer.

Ziel dieser Einstellungen ist die Reduzierung der Anzahl von Eingabeaufforderungen durch Apps und Prozesse.

Diese Funktion gilt für:

- macOS 10.14 und höher
- Einige Einstellungen gelten für macOS 10.15 und höher.
- Diese Einstellungen gelten nur für Geräte, auf denen das Profil für Datenschutzeinstellungen installiert wurde, bevor Sie aktualisiert werden.

### <a name="settings-apply-to-user-approved-device-enrollment-automated-device-enrollment"></a>Die Einstellungen gelten für: Vom Benutzer genehmigte Geräteregistrierung, automatisierte Geräteregistrierung

- **Apps und Prozesse:** : **Fügen** Sie Apps oder Prozesse hinzu, um den Zugriff zu konfigurieren. Geben Sie außerdem Folgendes ein:
  - **Name:** Geben Sie einen Namen für Ihre App oder Ihren Prozess ein. Geben Sie beispielsweise `Microsoft Remote Desktop` oder `Microsoft Office 365` ein.
  
  - **Bezeichnertyp**: Folgende Optionen sind verfügbar:
    - **Paket-ID**: Wählen Sie diese Option für Apps aus.
    - **Pfad:** Wählen Sie diese Option für nicht gebündelte Binärdateien aus, die ein Prozess oder eine ausführbare Datei sind.

    Hilfstools, die in ein Anwendungspaket eingebettet sind, erben automatisch die Berechtigungen Ihres umschließenden Anwendungspakets.

  - **Bezeichner:** Geben Sie die App-Paket-ID oder den Installationsdateipfad des Prozesses oder der ausführbaren Datei ein. Geben Sie beispielsweise `com.contoso.appname` ein.

    Um die App-Paket-ID abzurufen, öffnen Sie die Terminal-App, und führen Sie den Befehl `codesign` aus. Dieser Befehl identifiziert die Codesignatur. So können Sie die ID des Pakets und die Codesignatur gleichzeitig abrufen.

  - **Codeanforderung**: Geben Sie die Codesignatur für die Anwendung oder den Prozess ein.

    Eine Codesignatur wird erstellt, wenn eine App oder eine Binärdatei mit einem Entwicklerzertifikat signiert wird. Um die Bezeichnung zu ermitteln, führen Sie den Befehl `codesign` manuell in der Terminal-App aus: `codesign --display -r -/path/to/app/binary`. Die Codesignatur ist alles, was nach `=>`angezeigt wird.

  - **Statische Codeüberprüfung aktivieren**: Wählen Sie für die App oder den Prozess **Ja** aus, um die Codeanforderung statisch zu validieren. Wenn die Einstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.

    Aktivieren Sie diese Einstellung nur, wenn die dynamische Codesignatur durch den Prozess ungültig wird. Verwenden Sie andernfalls **Nicht konfiguriert**.  

  - **Kamera blockieren**: **Ja** verhindert, dass die App auf die Systemkamera zugreift. Sie können den Zugriff auf die Kamera nicht zulassen. Wenn die Einstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.

  - **Mikrofon blockieren:** **Ja** verhindert, dass die App auf das Systemmikrofon zugreifen kann. Sie können den Zugriff auf das Mikrofon nicht zulassen. Wenn die Einstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.

  - **Bildschirmaufzeichnung blockieren**: **Ja** hindert die App daran, den Inhalt der Systemanzeige zu erfassen. Sie können den Zugriff auf die Bildschirmaufzeichnung und Bildschirmerfassung nicht zulassen. Wenn die Einstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.

    Erfordert macOS 10.15 oder höher.

  - **Eingabeüberwachung blockieren**: **Ja** verhindert, dass die App CoreGraphics und HID-APIs verwendet, um auf CGEvents- und HID-Ereignisse von allen Prozessen zu lauschen. **Ja** verhindert außerdem, dass Apps und Prozesse auf Daten von Eingabegeräten (z. B. Maus, Tastatur oder Trackpad) lauschen und diese sammeln. Sie können den Zugriff auf die CoreGraphics- und HID-APIs nicht zulassen.

    Wenn die Einstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.

    Erfordert macOS 10.15 oder höher.

  - **Referenz zur Spracherkennung**: Folgende Optionen sind verfügbar:
    - **Nicht konfiguriert:** Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
    - **Zulassen:** Ermöglicht der App den Zugriff auf die Systemspracherkennung und ermöglicht das Senden von Sprachdaten an Apple.
    - **Blockieren:** Verhindert, dass die System auf die Systemspracherkennung zugreift, und verhindert außerdem, dass Sprachdaten an Apple gesendet werden.

    Erfordert macOS 10.15 oder höher.

  - **Barrierefreiheit**: Folgende Optionen sind verfügbar:
    - **Nicht konfiguriert:** Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
    - **Zulassen:** Ermöglicht der App den Zugriff auf die Systembarrierefreiheits-App. Diese App umfasst Untertitel für Hörgeschädigte, Hovertext und Sprachsteuerung.
    - **Blockieren:** Verhindert, dass die App auf die Systembarrierefreiheits-App zugreifen kann.

  - **Kontakte:** Folgende Optionen sind verfügbar:
    - **Nicht konfiguriert:** Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
    - **Zulassen:** Ermöglicht der App den Zugriff auf Kontaktinformationen, die von der Systemkontakte-App verwaltet werden.  
    - **Blockieren:** Verhindert, dass die App auf diese Kontaktinformationen zugreift.

  - **Kalender:** Folgende Optionen sind verfügbar:
    - **Nicht konfiguriert:** Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
    - **Zulassen:** Ermöglicht der App den Zugriff auf Kalenderinformationen, die von der Systemkalender-App verwaltet werden.
    - **Blockieren:** Verhindert, dass die App auf diese Kalenderinformationen zugreift.

  - **Erinnerungen**: Folgende Optionen sind verfügbar:
    - **Nicht konfiguriert:** Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
    - **Zulassen:** Ermöglicht der App den Zugriff auf Erinnerungsinformationen, die von der Systemerinnerungs-App verwaltet werden.
    - **Blockieren:** Verhindert, dass die App auf diese Erinnerungsinformationen zugreift.

  - **Fotos**: Folgende Optionen sind verfügbar:
    - **Nicht konfiguriert:** Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
    - **Zulassen:** Ermöglicht der App den Zugriff auf die Bilder, die von der Systemfoto-App in `~/Pictures/.photoslibrary` verwaltet werden.
    - **Blockieren:** Verhindert, dass die App auf diese Bilder zugreift.

  - **Medienbibliothek**: Folgende Optionen sind verfügbar:
    - **Nicht konfiguriert:** Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
    - **Zulassen:** Ermöglicht der App den Zugriff auf Apple Music, Musik- und Videoaktivitäten und die Medienbibliothek.  
    - **Blockieren:** Verhindert, dass die App auf diese Medienobjekte zugreift.

    Erfordert macOS 10.15 oder höher.

  - **Dateianbieterpräsenz**: Folgende Optionen sind verfügbar:
    - **Nicht konfiguriert:** Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
    - **Zulassen:** Ermöglicht der App den Zugriff auf die Dateianbieter-App und erkennt, wenn Benutzer Dateien verwenden, die vom Dateianbieter verwaltet werden. Eine Dateianbieter-App ermöglicht anderen Dateianbieter-Apps den Zugriff auf die Dokumente und Verzeichnisse, die von der enthaltenden App gespeichert und verwaltet werden.
    - **Blockieren:** Verhindert, dass die App auf die Dateianbieter-App zugreift.

    Erfordert macOS 10.15 oder höher.

  - **Vollständiger Datenträgerzugriff**: Folgende Optionen sind verfügbar:
    - **Nicht konfiguriert:** Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
    - **Zulassen:** Ermöglicht der App, auf alle geschützten Dateien einschließlich der Systemverwaltungsdateien zuzugreifen. Wenden Sie diese Einstellung mit Vorsicht an.
    - **Blockieren:** Verhindert, dass die App auf diese geschützten Dateien zugreift.

  - **Systemadministratordateien**: Folgende Optionen sind verfügbar:
    - **Nicht konfiguriert:** Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
    - **Zulassen:** Ermöglicht der App den Zugriff auf einige Dateien, die in der Systemverwaltung verwendet werden.
    - **Blockieren:** Verhindert, dass die App auf diese Dateien zugreift.

  - **Ordner „Desktop“** : Folgende Optionen sind verfügbar:
    - **Nicht konfiguriert:** Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
    - **Zulassen:** Ermöglicht der App den Zugriff auf Dateien im Ordner „Desktop“ des Benutzers.
    - **Blockieren:** Verhindert, dass die App auf diese Dateien zugreift.

    Erfordert macOS 10.15 oder höher.

  - **Ordner „Dokumente“** : Folgende Optionen sind verfügbar:
    - **Nicht konfiguriert:** Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
    - **Zulassen:** Ermöglicht der App den Zugriff auf Dateien im Ordner „Dokumente“ des Benutzers.
    - **Blockieren:** Verhindert, dass die App auf diese Dateien zugreift.

    Erfordert macOS 10.15 oder höher.

  - **Ordner „Downloads“** : Folgende Optionen sind verfügbar:
    - **Nicht konfiguriert:** Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
    - **Zulassen:** Ermöglicht der App den Zugriff auf Dateien im Ordner „Downloads“ des Benutzers.
    - **Blockieren:** Verhindert, dass die App auf diese Dateien zugreift.

    Erfordert macOS 10.15 oder höher.

  - **Netzwerkvolumes**: Folgende Optionen sind verfügbar:
    - **Nicht konfiguriert:** Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
    - **Zulassen:** Ermöglicht der App, auf Dateien auf Netzwerkvolumes zuzugreifen.
    - **Blockieren:** Verhindert, dass die App auf diese Dateien zugreift.

    Erfordert macOS 10.15 oder höher.

  - **Wechselmedien**: Folgende Optionen sind verfügbar:
    - **Nicht konfiguriert:** Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
    - **Zulassen:** Ermöglicht der App den Zugriff auf Dateien auf Wechselmedien, z. B. auf eine Festplatte.
    - **Blockieren:** Verhindert, dass die App auf diese Dateien zugreift.

    Erfordert macOS 10.15 oder höher.

  - **Systemereignisse** : Folgende Optionen sind verfügbar:
    - **Nicht konfiguriert:** Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
    - **Zulassen:** Ermöglicht der App, CoreGraphics-APIs zu verwenden, um CGEvents an den Systemereignisstream zu senden.
    - **Blockieren:** Verhindert, dass die App CoreGraphics-APIs verwendet, um CGEvents an den Systemereignisstream zu senden.

  - **Apple-Ereignisse**: Diese Einstellung ermöglicht es Apps, ein eingeschränktes Apple-Ereignis an eine andere App oder einen anderen Prozess zu senden. Wählen Sie **Hinzufügen** aus, um eine empfangende App oder einen Prozess hinzuzufügen. Geben Sie die folgenden Informationen der empfangenden App oder des empfangenden Prozesses ein:

    - **Bezeichnertyp**: Wählen Sie **Paket-ID** aus, wenn der empfangende Bezeichner eine Anwendung ist. Wählen Sie **Pfad** aus, wenn der empfangende Bezeichner ein Prozess oder eine ausführbare Datei ist.
    
    - **Bezeichner:** Geben Sie die App-Paket-ID oder den Installationspfad des Prozesses ein, der Apple-Ereignis empfängt.  

    - **Codeanforderung**: Geben Sie die Codesignatur für die empfangende Anwendung oder den Prozess ein.

      Eine Codesignatur wird erstellt, wenn eine App oder eine Binärdatei mit einem Entwicklerzertifikat signiert wird. Um die Bezeichnung zu ermitteln, führen Sie den Befehl `codesign` manuell in der Terminal-App aus: `codesign --display -r -/path/to/app/binary`. Die Codesignatur ist alles, was nach `=>`angezeigt wird.

    - **Zugriff**: Lässt das Senden eines macOS-Apple-Ereignisses an die empfangende App oder den empfangenden Prozess zu. Folgende Optionen sind verfügbar:
      - **Nicht konfiguriert:** Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
      - **Zulassen:** Ermöglicht der App oder dem Prozess, das eingeschränkte Apple-Ereignis an die empfangende App oder den empfangenden Prozess zu senden.
      - **Blockieren:** Verhindert, dass die App oder der Prozess ein eingeschränktes Apple-Ereignis an die empfangende App oder den empfangenden Prozess sendet.

  - **Speichern** Sie die Änderungen.

## <a name="restricted-apps"></a>Eingeschränkte Apps

### <a name="settings-apply-to-all-enrollment-types"></a>Die Einstellungen gelten für: Alle Registrierungstypen

- **Liste der eingeschränkten App-Typen:** Mit dieser Einstellung wird eine Liste der Apps erstellt, die Benutzer nicht installieren oder verwenden dürfen. Folgende Optionen sind verfügbar:

  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Standardmäßig können Benutzer möglicherweise auf von Ihnen zugewiesene Apps und integrierte Apps zugreifen.
  - **Genehmigte Apps:** Listet die Apps auf, die Benutzer installieren dürfen. Um die Kompatibilität zu gewährleisten, dürfen Benutzer keine anderen Apps installieren. Apps, die von Intune verwaltet werden, sind automatisch zugelassen, einschließlich der Unternehmensportal-App. Benutzer werden nicht daran gehindert, eine App zu installieren, die nicht in der Liste zulässiger Apps enthalten ist. Wenn sie es jedoch tun, wird dies in Intune gemeldet.
  - **Unzulässige Apps:** Listen Sie die (nicht von Intune verwalteten) Apps auf, die Benutzer nicht installieren und ausführen dürfen. Benutzer können unzulässige Apps nicht installieren. Wenn ein Benutzer eine App aus dieser Liste installiert, wird dies in Intune gemeldet.

- **Liste der Apps:** **Fügen Sie der Liste Apps hinzu**:
  - **App-Bündel-ID:** Geben Sie die [Paket-ID](bundle-ids-built-in-ios-apps.md) der App ein. Sie können integrierte Apps und branchenspezifische Apps hinzufügen. Eine Liste der integrierten Apple-Apps finden Sie auf [dieser Apple-Website](https://support.apple.com/HT208094).

    Um die URL einer App zu suchen, öffnen Sie den iTunes App Store, und suchen Sie nach der App. Suchen Sie beispielsweise nach `Microsoft Remote Desktop` oder `Microsoft Word`. Wählen Sie die App aus, und kopieren Sie die URL. Sie können auch iTunes verwenden, um die App zu suchen, und dann die Aufgabe **Link kopieren**, um die App-URL abzurufen.

  - **App-Name:** Geben Sie einen benutzerfreundlichen Namen ein, damit Sie die Bündel-ID einfacher identifizieren können. Geben Sie beispielsweise `Intune Company Portal app` ein.
  - **Herausgeber**: Geben Sie den Herausgeber der App an.

- **Importieren** Sie eine CSV-Datei mit den Details der App, einschließlich der URL. Verwenden Sie das Format `<app bundle ID>, <app name>, <app publisher>`. Oder **exportieren** Sie eine Datei im selben Format, um eine Liste der hinzugefügten Apps zu erstellen.

## <a name="next-steps"></a>Nächste Schritte

[Zuweisen von Profilen](device-profile-assign.md) und [Überwachen von Profilen](device-profile-monitor.md)

Sie können auch Gerätefunktionen und -einstellungen auf [iOS-/iPadOS](device-restrictions-ios.md)-Geräten einschränken.
