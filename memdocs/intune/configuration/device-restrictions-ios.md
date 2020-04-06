---
title: 'iOS/iPadOS-Geräteeinstellungen in Microsoft Intune: Azure | Microsoft-Dokumentation'
titleSuffix: ''
description: Fügen Sie Einstellungen auf iOS/iPadOS-Geräten hinzu, konfigurieren oder erstellen Sie sie, um Funktionen einzuschränken. Zu diesen gehört das Festlegen von Anforderungen für Kennwörter, die Anpassung des Sperrbildschirms, die Verwendung integrierter Apps, das Hinzufügen eingeschränkter oder genehmigter Apps, die Handhabung von Bluetooth-Geräten, die Verbindungsherstellung mit der Cloud für Sicherung und Speicherung, die Aktivierung des Kioskmodus, das Hinzufügen und die Steuerung von Domänen und die Art der Benutzerinteraktion mit dem Safari-Webbrowser in Microsoft Intune.
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
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 897366ba9b7bae15050c0aa5e392ba5255a90b24
ms.sourcegitcommit: e2877d21dfd70c4029c247275fa2b38e76bd22b8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80407814"
---
# <a name="ios-and-ipados-device-settings-to-allow-or-restrict-features-using-intune"></a>iOS- und iPadOS-Geräteeinstellungen zum Zulassen oder Einschränken von Funktionen mit Intune

In diesem Artikel werden die verschiedenen Einstellungen aufgeführt und beschrieben, die Sie auf iOS- und iPadOS-Geräten steuern können. Verwenden Sie als Bestandteil Ihrer Lösung für die mobile Geräteverwaltung (Mobile Device Management, MDM) diese Einstellungen, um Features zuzulassen oder zu deaktivieren, Kennwortregeln festzulegen, bestimmte Apps zu erlauben oder einzuschränken usw.

Diese Einstellungen werden einem Gerätekonfigurationsprofil in Intune hinzugefügt und dann Ihren iOS/iPadOS-Geräten zugewiesen oder auf diesen bereitgestellt.

> [!TIP]
> Für diese Einstellungen werden die MDM-Einstellungen von Apple verwendet. Weitere Informationen zu diesen Einstellungen finden Sie auf der Apple-Website zu den [MDM-Einstellungen von Apple](https://support.apple.com/guide/mdm/welcome/web).

## <a name="before-you-begin"></a>Vorbereitung

[Erstellen Sie ein Konfigurationsprofil mit Geräteeinschränkungen](device-restrictions-configure.md).

> [!NOTE]
> Diese Einstellungen gelten für verschiedene Registrierungstypen, wobei einige Einstellungen für alle Registrierungsoptionen gelten. Weitere Informationen zu den verschiedenen Registrierungstypen finden Sie unter [iOS/iPadOS-Registrierung](../enrollment/ios-enroll.md).

## <a name="general"></a>Allgemein

### <a name="settings-apply-to-all-enrollment-types"></a>Die Einstellungen gelten für: Alle Registrierungstypen

- **Nutzungsdaten freigeben**: **Blockieren** verhindert, dass Geräte Diagnose- und Nutzungsdaten an Apple senden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem das Senden dieser Daten zulassen.

- **Bildschirmaufnahme:** **Blockieren** verhindert, dass Screenshots oder Bildschirmaufnahmen auf Geräten vorgenommen werden. Ab iOS/iPadOS 9.0 werden auch Bildschirmaufzeichnungen blockiert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, den Bildschirminhalt als Bild oder Video zu erfassen.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Die Einstellungen gelten für: Geräteregistrierung, automatisierte Geräteregistrierung (überwacht)

- **Nicht vertrauenswürdige TLS-Zertifikate:** **Blockieren** verhindert, dass nicht vertrauenswürdige TLS-Zertifikate (Transport Layer Security) auf Geräte gelangen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem TLS-Zertifikate zulassen.
- **Drahtlose PKI-Updates blockieren**: **Blockieren** verhindert, dass Ihre Benutzer Softwareupdates erhalten, wenn Geräte nicht an einen Computer angeschlossen sind. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem einem Gerät erlauben, Softwareupdates zu empfangen, ohne mit einem Computer verbunden zu sein.
- **Anzeigennachverfolgung begrenzen:** **Begrenzen** deaktiviert die Geräteanzeigen-ID. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem sie aktiviert lassen.
- **Vertrauen für Unternehmens-App:** **Blockieren** entfernt die Schaltfläche **Trust Enterprise Developer** (Unternehmensentwickler vertrauen) über „Einstellungen > Allgemein > Profile & Geräteverwaltung“ auf Geräten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, zu wählen, ob Apps, die nicht aus dem App Store heruntergeladen wurden, vertraut werden soll.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Die Einstellungen gelten für: Automatisierte Geräteregistrierung (überwacht)

- **Änderung der Einstellungen zur Diagnoseübermittlung**: **Blockieren** verhindert, dass Benutzer in den Geräteeinstellungen in **Diagnose & Nutzung** Änderungen an den Einstellungen für Diagnoseübermittlung und App-Analyse vornehmen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, diese Geräteeinstellungen zu ändern.

  Legen Sie **Blockieren** für die Einstellung **Nutzungsdaten freigeben** fest, um diese Einstellung zu verwenden.

  Diese Funktion gilt für:  
  - iOS 9.3.2 und neuer
  - iOS 13.0 und höher

- **Beobachtung von Remotebildschirmen durch Classroom-App**: **Blockieren** verhindert, dass die Classroom-App den Bildschirm der Geräte remote anzeigt. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem der Classroom-App von Apple erlauben, den Bildschirm anzuzeigen.

  Legen Sie **Blockieren** für die Einstellung **Bildschirmaufnahme** fest, um diese Einstellung zu verwenden.

  Diese Funktion gilt für:  
  - iOS 9.3 und höher
  - iOS 13.0 und höher

- **Unangekündigte Bildschirmüberwachung über Classroom-App**: **Zulassen** ermöglicht Lehrkräften, die Bildschirme der iOS/iPadOS-Geräte ihrer Kursteilnehmer mithilfe der Classroom-App zu überwachen, ohne dass die Kursteilnehmer dies mitbekommen. In einer Klasse registrierte Kursteilnehmergeräte, die die Classroom-App verwenden, gewähren dem Kursleiter automatisch die Berechtigung. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem diese Funktion verhindern.

  Legen Sie **Blockieren** für die Einstellung **Bildschirmaufnahme** fest, um diese Einstellung zu verwenden.

- **Kontoänderung**: **Blockieren** hindert Benutzer daran, die gerätespezifischen Einstellungen über die iOS/iPadOS-App „Einstellungen“ zu aktualisieren. Benutzer können z. B. nicht neue Gerätekonten erstellen oder Benutzernamen bzw. Kennwort ändern. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, diese Einstellungen zu ändern.

  Diese Funktion gilt auch für Einstellungen, auf die über die iOS/iPadOS-App „Einstellungen“ zugegriffen werden kann, wie z. B. E-Mail, Kontakte, Kalender, Twitter und mehr. Diese Funktion gilt nicht für Apps mit Kontoeinstellungen, die nicht über die iOS/iPadOS-App „Einstellungen“ konfiguriert werden können, wie z. B. die Microsoft Outlook-App.

- **Bildschirmzeit**: **Blockieren** verhindert, dass Benutzer ihre eigenen Einschränkungen in „Bildschirmzeit“ (Geräteeinstellungen) vornehmen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern das Konfigurieren von Geräteeinschränkungen (z. B. Jugendschutz oder Inhalts- und Datenschutzeinschränkungen) auf Geräten erlauben.

  Diese Einstellung hieß zuvor **Aktivieren von Einschränkungen in den Geräteeinstellungen**. Auswirkungen dieser Änderung:  
  
  - iOS 11.4.1 und älter: **Blockieren** verhindert, dass Benutzer die für sie geltenden Einschränkungen in den Geräteeinstellungen bearbeiten. Dieses Verhalten bewirkt dasselbe, sodass es keine Änderungen für Benutzer gibt.
  - iOS 12.0 und höher: **Blockieren** verhindert, dass Benutzer die für sie geltende **Bildschirmzeit** (einschließlich Einschränkungen von Inhalt und Datenschutz) in den Geräteeinstellungen (Einstellungen > Allgemein > Bildschirmzeit) bearbeiten. Bei auf iOS 12.0 aktualisierten Geräten wird die Registerkarte „Einschränkungen“ in den Geräteeinstellungen nicht mehr angezeigt (Einstellungen > Allgemein > Geräteverwaltung > Verwaltungsprofil > Einschränkungen). Diese Einstellungen befinden sich unter **Bildschirmzeit**.
  
- **Verwendung der Option zum Löschen aller Inhalte und Einstellungen auf dem Gerät**: **Blockieren** verhindert die Verwendung der Option zum Löschen aller Inhalte und Einstellungen auf Geräten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise gewährt das Betriebssystem standardmäßig Benutzern Zugriff auf diese Einstellungen.
- **Bearbeitung des Gerätenamens:** **Blockieren** verhindert das Ändern des Gerätenamens. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, den Namen des Geräts zu ändern.
- **Änderung der Benachrichtigungseinstellungen**: **Blockieren** verhindert das Ändern der Benachrichtigungseinstellungen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, die Benachrichtigungseinstellungen des Geräts zu ändern.
- **Hintergrundbild ändern**: Wählen Sie **Blockieren** aus, um zu verhindern, dass Hintergrundbilder geändert werden können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, das Hintergrundbild von Geräten zu ändern.
- **Konfigurationsprofiländerungen**: **Blockieren** verhindert Konfigurationsprofiländerungen auf Geräten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern die Installation von Konfigurationsprofilen gestatten.
- **Aktivierungssperre**: **Zulassen** aktiviert die Aktivierungssperre auf überwachten iOS/iPadOS-Geräten. Die Aktivierungssperre erschwert die erneute Aktivierung verlorener oder gestohlener Geräte. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Entfernen von Apps blockieren**: **Blockieren** verhindert das Entfernen von Apps. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, Apps von Geräten zu entfernen.
- **USB-Zubehör bei gesperrtem Gerät zulassen**: **Zulassen**: USB-Zubehör kann Daten mit Geräten austauschen, die seit mehr als einer Stunde gesperrt sind. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem den Modus mit USB-Einschränkung auf Geräten nicht aktualisieren, und USB-Zubehör wird daran gehindert, Daten von Geräten zu übertragen, wenn diese länger als eine Stunde gesperrt sind.
- **Automatische Datums- und Uhrzeiteinstellung erzwingen**: **Anfordern** erzwingt, dass überwachte Geräte das Datum und die Uhrzeit automatisch einstellen. Die Zeitzone für das Gerät wird aktualisiert, wenn das Gerät über Mobilfunkverbindungen verfügt oder WLAN mit Standortdiensten aktiviert ist. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Erlaubnis für Kursteilnehmer vor dem Verlassen des Classroom-Kurses erforderlich**: **Anfordern** erzwingt, dass in einem nicht verwalteten Kurs registrierte Kursteilnehmer, die die Classroom-App verwenden, vom Kursleiter eine Berechtigung zum Verlassen des Kurses anfordern müssen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Es besteht die Möglichkeit, dass das Betriebssystem standardmäßig nicht erzwingt, dass Kursteilnehmer um eine Berechtigung bitten müssen.

  Diese Funktion gilt für:  
  - iOS 11.3 und neuer
  - iOS 13.0 und höher

- **Das Beschränken von Classroom auf eine App und das Sperren von Geräten ohne vorherige Aufforderung zulassen**: **Aktivieren** ermöglicht Lehrkräften das Sperren von Apps oder das Sperren von Geräten mithilfe der Classroom-App, ohne den Kursteilnehmer aufzufordern. Das Sperren von Apps bedeutet, dass Geräte nur auf die von der Lehrkraft angegebenen Apps zugreifen können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem verhindern, dass Lehrkräfte Anwendungen oder Geräte, die die Classroom-App verwenden, sperren, ohne die Kursteilnehmer zu fragen.

  Diese Funktion gilt für:  
  - iOS 11.0 und neuer
  - iOS 13.0 und höher

- **Classroom-Kursen automatisch ohne Aufforderung beitreten**: **Aktivieren** erlaubt es Lernenden, einem Kurs in der Classroom-App automatisch beizutreten, ohne die Lehrkraft zu fragen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Lehrkraft fragen, wenn Kursteilnehmer einem Kurs in der Classroom-App beitreten möchten.

  Diese Funktion gilt für:  
  - iOS 11.0 und neuer
  - iOS 13.0 und höher

- **VPN-Erstellung blockieren**: **Blockieren** hindert Benutzer daran, VPN-Konfigurationseinstellungen zu erstellen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern das Erstellen von VPNs auf Geräten erlauben.
- **eSIM-Einstellungen ändern**: **Blockieren** verhindert das Entfernen oder Hinzufügen eines Mobilfunktarifplans zum eSIM auf Geräten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, diese Einstellungen zu ändern.

  Diese Funktion gilt für:  
  - iOS 12.1 und neuer
  - iOS 13.0 und höher

- **Softwareupdates zurückstellen**: **Aktivieren** ermöglicht Ihnen, die Anzeige von Softwareupdates auf Geräten zu verzögern (0-90 Tage). Diese Einstellung steuert nicht, ob Updates installiert werden oder nicht.

  Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Softwareupdates auf Geräten anzeigen, wenn Apple sie veröffentlicht. Wenn beispielsweise ein iOS/iPadOS-Update von Apple an einem bestimmten Datum veröffentlicht wird, wird dieses Update normalerweise am Veröffentlichungsdatum auf Geräten angezeigt.  

  - **Sichtbarkeit von Softwareupdates verzögern**: Geben Sie einen Wert zwischen 0–90 Tagen ein. Nach der Verzögerung erhalten Benutzer eine Benachrichtigung für ein Update auf die früheste verfügbare Version des Betriebssystems, wenn die Verzögerung ausgelöst wird.

    Wenn beispielsweise iOS 12.a am **1. Januar** verfügbar und **Sichtbarkeit verzögern** auf **5 Tage** festgelegt ist, wird iOS 12.a auf Benutzergeräten nicht als verfügbares Update angezeigt. Am **6. Tag** nach Veröffentlichung ist dieses Update verfügbar, sodass Benutzer es installieren können.

    Diese Einstellung gilt für:  
    - iOS 11.3 und neuer
    - iOS 13.0 und höher

## <a name="password"></a>Kennwort

### <a name="settings-apply-to-all-enrollment-types"></a>Die Einstellungen gelten für: Alle Registrierungstypen

- **Kennwort:** Wenn **Erforderlich** festgelegt wird, müssen Benutzer ein Kennwort eingeben, um auf Geräte zuzugreifen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, ohne Kennworteingabe auf Geräte zuzugreifen.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Die Einstellungen gelten für: Geräteregistrierung, automatisierte Geräteregistrierung (überwacht)

> [!IMPORTANT]
> Wenn Sie auf von Benutzern registrierten Geräten eine Kennworteinstellung konfigurieren, wird die Einstellung **Einfache Kennwörter** automatisch auf **Blockieren** festgelegt und eine sechsstellige PIN erzwungen.
>
> Sie konfigurieren beispielsweise die Einstellung **Kennwortablauf** und übertragen diese Richtlinie per Push auf vom Benutzer registrierte Geräte. Auf diesen Geräten geschieht Folgendes:
>
> - Die Einstellung **Kennwortablauf** wird ignoriert.
> - Einfache Passwörter wie `1111` oder `1234` sind nicht zulässig.
> - Eine sechsstellige PIN wird erzwungen.

- **Einfache Kennwörter:** **Blockieren** erfordert komplexere Kennwörter. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem einfache Kennwörter wie z. B. `0000` und `1234` zulassen.

- **Erforderlicher Kennworttyp:** Geben Sie den von Ihrer Organisation geforderten Grad der Kennwortkomplexität an. Folgende Optionen sind verfügbar:
  - **Gerätestandard**
  - **Numerisch**: Das Kennwort darf nur aus Zahlen bestehen, z. B. 123456789.
  - **Alphanumerisch**: Schließt Großbuchstaben, Kleinbuchstaben und Ziffern ein.
- **Anzahl nicht alphanumerischer Zeichen im Kennwort:** Geben Sie die Anzahl von Symbolzeichen wie `#` oder `@` an, die im Kennwort enthalten sein müssen (zwischen 1 und 4). Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

- **Minimale Kennwortlänge:** Geben Sie die Mindestlänge des Kennworts ein (4 bis 16 Zeichen). Geben Sie auf von Benutzern registrierten Geräten eine Länge von 4 bis 6 Zeichen an.
  
  > [!NOTE]
  > Bei Geräten, die vom Benutzer registriert werden, können Benutzer eine PIN angeben, die länger als 6 Zeichen ist. Es werden jedoch nicht mehr als 6 Zeichen auf Geräten erzwungen. Wenn ein Administrator die Mindestlänge beispielsweise auf `8` festlegt, müssen Benutzer von Geräten mit Benutzerregistrierung eine PIN mit nur 6 Ziffern festlegen. Intune erzwingt auf von Benutzern registrierten Geräten keine PINs, die länger als 6 Zeichen sind.

- **Anzahl von fehlgeschlagenen Anmeldungen, bevor das Gerät zurückgesetzt wird:** Geben Sie die Anzahl der fehlgeschlagenen Anmeldungen ein, bevor das Gerät zurückgesetzt wird (zwischen 4 und 11).
  
  Die integrierte iOS/iPadOS-Sicherheit kann sich auf diese Einstellung auswirken. iOS/iPadOS kann die Auslösung der Richtlinie beispielsweise je nach Anzahl der Anmeldefehler verzögern. Die wiederholte Eingabe desselben Kennworts kann beispielsweise auch als ein Versuch anerkannt werden. Der [iOS/iPadOS-Sicherheitsleitfaden von Apple](https://www.apple.com/business/site/docs/iOS_Security_Guide.pdf) (Apple-Website) ist eine gute Ressource mit ausführlichen Informationen zu Passcodes.
  
- **Maximaler Zeitraum der Bildschirmsperre (in Minuten) bis zur Anforderung eines Kennworts<sup>1</sup>:** Geben Sie an, wie lange Geräte im Leerlauf bleiben können, bevor Benutzer sein Kennwort erneut eingeben müssen. Wenn Sie einen längeren Zeitraum eingeben, als derzeit auf dem Gerät eingestellt ist, ignoriert das Gerät Ihre Eingabe.

  Diese Einstellung gilt für:  
  - iOS 8.0 und höher
  - iPadOS 13.0 und höher

- **Maximaler Zeitraum der Inaktivität (in Minuten) bis zur Bildschirmsperrung<sup>1</sup>:** Geben Sie an, wie viele Minuten Geräte höchstens inaktiv sein dürfen, bevor sie automatisch gesperrt werden.

  **iOS/iPadOS-Optionen:**  

  - **Nicht konfiguriert** (Standard): Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
  - **Sofort:** Der Bildschirm wird nach 30 Sekunden Inaktivität gesperrt.
  - **1:** Der Bildschirm wird nach einer Minute Inaktivität gesperrt.
  - **2:** Der Bildschirm wird nach zwei Minuten Inaktivität gesperrt.
  - **3:** Der Bildschirm wird nach drei Minuten Inaktivität gesperrt.
  - **4**: Der Bildschirm wird nach vier Minuten Inaktivität gesperrt.
  - **5:** Der Bildschirm wird nach fünf Minuten Inaktivität gesperrt.

  **iPadOS-Optionen:**  

  - **Nicht konfiguriert** (Standard): Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
  - **Sofort:** Der Bildschirm wird nach zwei Minuten Inaktivität gesperrt.
  - **2:** Der Bildschirm wird nach zwei Minuten Inaktivität gesperrt.
  - **5:** Der Bildschirm wird nach fünf Minuten Inaktivität gesperrt.
  - **10:** Der Bildschirm wird nach zehn Minuten Inaktivität gesperrt.
  - **15:** Der Bildschirm wird nach 15 Minuten Inaktivität gesperrt.

  Wenn ein Wert nicht für iOS und iPadOS zulässig ist, verwendet Apple den *niedrigsten* nächstgelegenen Wert. Wenn Sie beispielsweise `4` Minuten angeben, verwenden iPadOS-Geräte `2` Minuten. Wenn Sie `10` Minuten angeben, verwenden iOS-Geräte `5` Minuten. Dies ist eine Apple-Einschränkung.
  
  > [!NOTE]
  > Die Benutzeroberfläche von Intune für diese Einstellung trennt die von iOS und iPadOS unterstützten Werte nicht voneinander. Diese Benutzeroberfläche wird in einem zukünftigen Release möglicherweise aktualisiert.

- **Kennwortablauf (Tage):** Geben Sie die Anzahl der Tage an, bis das Gerätekennwort geändert werden muss (zwischen 1 und 65.535).
- **Wiederverwendung vorheriger Kennwörter verhindern:** Verwenden Sie diese Einstellung, um zu verhindern, dass Benutzer zuvor verwendete Kennwörter erstellen. Geben Sie die Anzahl der zuvor verwendeten Kennwörter ein, die nicht erneut verwendet werden können, von 1–24. Geben Sie z. B. 5 an, damit ein Benutzer als sein neues Kennwort nicht sein aktuelles Kennwort oder eines seiner vorherigen vier Kennwörter festlegen kann. Wenn kein Wert angegeben ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.
- **Touch ID und Face ID entsperren:** **Blockieren** verhindert die Verwendung eines Fingerabdrucks oder Gesichts zum Entsperren von Geräten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern das Entsperren von Geräten mithilfe von Biometrie erlauben.

  Wenn Sie diese Einstellung blockieren, wird auch die Verwendung der Face ID-Authentifizierung zum Entsperren von Geräten verhindert.

  Face ID gilt für:  
  - iOS 11.0 und neuer
  - iOS 13.0 und höher

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Die Einstellungen gelten für: Automatisierte Geräteregistrierung (überwacht)

- **Passcodeänderung**: **Blockieren** verhindert, dass die Kennung geändert, hinzugefügt oder entfernt wird. Änderungen an Kennungseinschränkungen werden nach der Blockierung dieses Features auf überwachten Geräten ignoriert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem erlauben, Passcodes hinzuzufügen, zu ändern oder zu entfernen.

  - **Touch-ID and Face-ID-Änderungen:** **Blockieren** hindert Benutzer daran, TouchID-Fingerabdrücke und Face ID zu ändern, hinzuzufügen oder zu entfernen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern das Aktualisieren der TouchID-Fingerabdrücke und Face ID auf Geräten erlauben.

    Wenn Sie diese Einstellung blockieren, können Benutzer die Face ID-Authentifizierung nicht ändern, hinzufügen oder entfernen.

    Face ID gilt für:  
    - iOS 11.0 und neuer
    - iOS 13.0 und höher

- **AutoAusfüllen für Kennwörter blockieren**: **Blockieren** verhindert die Verwendung des Features zum automatischen Ausfüllen von Kennwörtern unter iOS/iPadOS. Das Wählen von **Blockieren** bewirkt auch Folgendes:

  - Benutzer werden nicht aufgefordert, in Safari oder beliebigen Apps gespeicherte Kennwörter zu verwenden.
  - Automatische sichere Kennwörter sind deaktiviert, und sichere Kennwörter werden Benutzern nicht empfohlen.

  Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem diese Funktionen zulassen.

- **Kennwortanforderungen durch Näherung blockieren**: Die Einstellung **Blockieren** verhindert, dass Geräte Kennwörter von Geräten in der Nähe anfordern. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem diese Kennwortanforderungen zulassen.
- **Kennwortfreigabe blockieren**: **Blockieren** verhindert die Freigabe von Kennwörtern zwischen Geräten mit AirDrop. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem das Freigeben von Kennwörtern zulassen.
- **Authentifizierung über Touch-ID oder Face-ID für AutoAusfüllen von Kennwörtern und Kreditkarteninformationen erforderlich**: **Anfordern** zwingt Benutzer, sich mit TouchID oder FaceID zu authentifizieren, bevor Kennwörter oder Kreditkarteninformationen in Safari und anderen Anwendungen automatisch eingefügt werden können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, diese Funktion in den Geräteeinstellungen zu steuern.

  Diese Funktion gilt für:  
  - iOS 11.0 und neuer
  - iOS 13.0 und höher
  
<sup>1</sup> Wenn Sie die Einstellungen **Maximaler Zeitraum der Inaktivität (in Minuten) bis zur Bildschirmsperrung** und **Maximaler Zeitraum der Bildschirmsperre (in Minuten) bis zur Anforderung eines Kennworts** konfigurieren, werden diese nacheinander angewendet. Wenn Sie beispielsweise den Wert für beide Einstellungen auf **5** Minuten einstellen, wird der Bildschirm automatisch nach fünf Minuten deaktiviert, und Geräte werden nach weiteren fünf Minuten gesperrt. Wenn Benutzer den Bildschirm jedoch manuell deaktivieren, wird die zweite Einstellung sofort angewendet. Im selben Beispiel wird das Gerät fünf Minuten, nachdem Benutzer den Bildschirm deaktiviert haben, gesperrt.

## <a name="locked-screen-experience"></a>Benutzererfahrung „Gesperrter Bildschirm“

### <a name="settings-apply-to-all-enrollment-types"></a>Die Einstellungen gelten für: Alle Registrierungstypen

- **Kontrollcenterzugriff bei gesperrtem Gerät:** **Blockieren** verhindert den Zugriff auf die Kontrollcenter-App, während das Gerät gesperrt ist. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem den Zugriff auf die Steuerungscenter-App erlauben, wenn Geräte gesperrt sind.
- **Benachrichtigungen bei Gerätesperre:** **Blockieren** verhindert den Zugriff auf Benachrichtigungen, wenn Geräte gesperrt sind. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern den Zugriff auf die Benachrichtigungen erlauben, ohne dass das Gerät entsperrt werden muss.
- **Ansicht „Heute“ bei Gerätesperre:** **Blockieren** verhindert den Zugriff auf die Ansicht „Heute“, wenn Geräte gesperrt sind. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern den Zugriff auf die Ansicht „Heute“ erlauben, wenn Geräte gesperrt sind.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Die Einstellungen gelten für: Geräteregistrierung, automatisierte Geräteregistrierung (überwacht)

- **Wallet-Benachrichtigungen bei gesperrtem Gerät:** **Blockieren** verhindert den Zugriff auf die Wallet-App, wenn Geräte gesperrt sind. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem den Zugriff auf die Wallet-App erlauben, während Geräte gesperrt sind.

## <a name="app-store-doc-viewing-gaming"></a>App Store, Dokumentanzeige, Spiele

### <a name="settings-apply-to-all-enrollment-types"></a>Die Einstellungen gelten für: Alle Registrierungstypen

- **Anzeige von Unternehmensdokumenten in nicht verwalteten Apps:** **Blockieren** verhindert die Anzeige unternehmenseigener Dokumente in nicht verwalteten Apps. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Anzeige von Unternehmensdokumenten in beliebigen Apps zulassen.

  Beispiel: Sie möchten verhindern, dass Benutzer Dateien aus der OneDrive-App in Dropbox speichern. Legen Sie für diese Einstellung **Blockieren** fest. Sobald Geräte die Richtlinie empfangen (z. B. nach einem Neustart), ist kein Speichern mehr möglich.

  > [!NOTE]
  > Wenn diese Einstellung blockiert wird, werden Tastaturen von Drittanbietern, die über den App Store installiert wurden, ebenfalls blockiert.

  - **Lesen aus verwalteten Kontaktkonten für nicht verwaltete Apps zulassen**: **Zulassen** lässt zu, dass nicht verwaltete Apps wie die integrierte iOS/iPadOS-App „Kontakte“ Kontaktinformationen aus verwalteten Apps wie der mobilen Outlook-App lesen und auf diese zugreifen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem verhindern, dass die integrierte App „Kontakte“ auf Geräten gelesen werden kann oder Duplikate entfernt werden können.  
  
    Mit dieser Einstellung kann das Lesen von Kontaktinformationen zugelassen oder verhindert werden. Das Synchronisieren von Kontakten zwischen den Apps wird nicht von dieser Einstellung gesteuert.
  
    Wenn Sie diese Einstellung verwenden möchten, legen Sie die Einstellung **Anzeige von Unternehmensdokumenten in nicht verwalteten Apps**auf **Blockieren** fest.

  Weitere Informationen zu diesen beiden Einstellungen und deren Auswirkung auf die Kontaktexportsynchronisierung von Outlook für iOS/iPadOS finden Sie unter [Tipp zur Unterstützung: Verwenden von benutzerdefinierten Intune-Profileinstellungen mit der nativen iOS/iPadOS-App „Kontakte“](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Use-Intune-custom-profile-settings-with-the-iOS/ba-p/298453).

- **AirDrop als nicht verwaltetes Ziel behandeln:** **Anfordern** erzwingt, dass AirDrop als nicht verwaltetes Drop-Ziel behandelt wird. Es hindert verwaltete Apps daran, Daten mithilfe von AirDrop zu senden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Anzeige nicht unternehmenseigener Dokumente in Unternehmens-Apps:** **Blockieren** verhindert, dass nicht unternehmenseigene Dokumente in Unternehmens-Apps angesehen werden können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Anzeige beliebiger Dokumente in verwalteten Unternehmens-Apps zulassen.

  **Blockieren** verhindert auch die Kontaktexportsynchronisierung in Outlook für iOS/iPadOS. Weitere Informationen finden Sie unter [Tipp zur Unterstützung: Aktivieren der Kontaktsynchronisierung von Outlook für iOS/iPadOS mit iOS12-MDM-Steuerelementen](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Enabling-Outlook-iOS-Contact-Sync-with-iOS12-MDM/ba-p/298453).

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Die Einstellungen gelten für: Geräteregistrierung, automatisierte Geräteregistrierung (überwacht)

- **iTunes Store-Kennwort für alle Käufe erforderlich:** **Erfordert**, dass Benutzer für jeden In-App- oder iTunes-Kauf das Apple-ID-Kennwort eingeben. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Käufe zulassen, ohne dass jedes Mal die Eingabe eines Kennworts angefordert wird.
- **In-App-Einkäufe:** **Blockieren** verhindert In-App-Einkäufe im Store. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Käufe im Store in einer ausgeführten App zulassen.
- **Download content from iBook store flagged as 'Erotica'** (Als „Erotik“ gekennzeichneten Inhalt aus dem iBooks Store herunterladen): **Blockieren** hindert Benutzer daran, Medien aus dem iBook Store herunterzuladen, die als „Erotik“ gekennzeichnet sind. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern das Herunterladen von Büchern aus der Kategorie „Erotik“ erlauben.
- **Schreiben von Kontakten in nicht verwaltete Kontaktkonten für verwaltete Apps zulassen**: **Zulassen** ermöglicht, dass verwaltete Apps wie die mobile Outlook-App Kontaktinformationen (einschließlich Geschäftskontakte) in der integrierten iOS/iPadOS-App „Kontakte“ speichern oder mit ihr synchronisieren. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem verhindern, dass verwaltete Apps Kontaktinformationen in der integrierten iOS/iPadOS-App „Kontakte“ auf Geräten speichern oder mit dieser synchronisieren.
  
  Wenn Sie diese Einstellung verwenden möchten, legen Sie die Einstellung **Anzeige von Unternehmensdokumenten in nicht verwalteten Apps**auf **Blockieren** fest.

- **Bewertungsregion:** Wählen Sie die Bewertungsregion aus, die Sie für zulässige Downloads verwenden möchten. Wählen Sie dann die zulässigen Bewertungen für **Filme**, **Fernsehsendungen** und **Apps** aus.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Die Einstellungen gelten für: Automatisierte Geräteregistrierung (überwacht)

- **App Store:** **Blockieren** verhindert, dass auf überwachten Geräten auf den App Store zugegriffen werden kann. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem den Zugriff erlauben.

  Ab iOS/iPadOS 13.0 muss es sich bei Geräten mit dieser Einstellung um überwachte Geräte handeln.

  - **Installieren von Apps über den App Store**: **Blockieren** zeigt den App Store nicht auf dem Startbildschirm des Geräts an. Benutzer können weiterhin iTunes oder das Apple Configurator-Tool zum Installieren von Apps verwenden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem den App Store auf dem Startbildschirm zulassen.
  - **Automatische App-Downloads**: **Blockieren** verhindert den automatischen Download von Apps, die auf anderen Geräten erworben wurden. Updates vorhandener Apps sind nicht betroffen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem zulassen, Apps auf das Gerät herunterzuladen, die auf anderen iOS/iPadOS-Geräten gekauft wurden.

- **Anstößige iTunes-Musik, Podcasts oder Nachrichteninhalte**: **Blockieren** verhindert anstößige iTunes-Musik, Podcasts oder Nachrichteninhalte. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem zulassen, dass das Gerät im Store auf nicht jugendfreie Inhalte zugreift.

  Ab iOS/iPadOS 13.0 muss es sich bei Geräten mit dieser Einstellung um überwachte Geräte handeln.

- **Hinzufügen von Game Center-Freunden**: **Blockieren** verhindert, dass Benutzer Game Center-Freunde hinzufügen können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern das Hinzufügen von Freunden im Game Center erlauben.

  Ab iOS/iPadOS 13.0 muss es sich bei Geräten mit dieser Einstellung um überwachte Geräte handeln.

- **Game Center**: **Blockieren** verhindert die Verwendung der Game Center-App. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Verwendung der Game Center-App auf Geräten zulassen.
- **Multiplayerspiele:** **Blockieren** verhindert Multiplayerspiele. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, Multiplayerspiele auf Geräten zu spielen.

  Ab iOS/iPadOS 13.0 muss es sich bei Geräten mit dieser Einstellung um überwachte Geräte handeln.

- **Zugriff auf Netzlaufwerk in Dateien-App:** Mithilfe des SMB-Protokolls (Server Message Block) können Geräte auf Dateien und andere Ressourcen auf einem Netzwerkserver zugreifen. Wenn **Deaktivieren** für diese Einstellung festgelegt wird, wird der Zugriff auf Dateien auf einem SMB-Netzwerklaufwerk verhindert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem den Zugriff erlauben.

  Diese Funktion gilt für:  
  - iOS 13.0 und neuer
  - iOS 13.0 und höher

## <a name="built-in-apps"></a>Integrierte Apps

### <a name="settings-apply-to-all-enrollment-types"></a>Die Einstellungen gelten für: Alle Registrierungstypen

- **Siri:** **Blockieren** verhindert den Zugriff auf Siri. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Verwendung des Sprach-Assistenten Siri auf Geräten zulassen.
  - **Siri bei Gerätesperre:** **Blockieren** verhindert den Zugriff auf Siri, wenn Geräte gesperrt sind. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Verwendung des Sprach-Assistenten Siri auf Geräten zulassen, wenn diese gesperrt sind.

- **Safari-Betrugswarnungen**: **Anfordern**, dass Betrugswarnungen im Webbrowser auf Geräten angezeigt werden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem diese Funktion deaktivieren.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Die Einstellungen gelten für: Geräteregistrierung, automatisierte Geräteregistrierung (überwacht)

- **Spotlight-Suche gibt Ergebnisse aus dem Internet zurück**: **Blockieren** verhindert, dass Spotlight Ergebnisse einer Internetsuche zurückgibt. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem der Spotlight-Suchfunktion das Herstellen einer Verbindung mit dem Internet zur Bereitstellung von Suchergebnissen gestatten.

- **Safari-Cookies**: Wählen Sie aus, wie Cookies auf Geräten behandelt werden. Folgende Optionen sind verfügbar:
  - Zulassen
  - Alle Cookies blockieren
  - Cookies von besuchten Websites zulassen
  - Cookies von aktueller Website zulassen

- **Safari-JavaScript**: **Blockieren** verhindert, dass auf Geräten Java-Skripts im Browser ausgeführt werden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Java-Skripts zulassen.

- **Safari-Popups**: **Blockieren** deaktiviert den Popupblocker im Webbrowser. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem den Popupblocker zulassen.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Die Einstellungen gelten für: Automatisierte Geräteregistrierung (überwacht)

- **Kamera:** **Blockieren** verhindert den Zugriff auf die Kamera des Geräts. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem den Zugriff auf die Kamera des Geräts zulassen.

  Intune verwaltet nur den Zugriff auf die Kamera des Geräts. Das Programm kann nicht auf Bilder oder Videos zugreifen.

  Ab iOS/iPadOS 13.0 muss es sich bei Geräten mit dieser Einstellung um überwachte Geräte handeln.

  - **FaceTime:** **Blockieren** verhindert den Zugriff auf die FaceTime-App. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem den Zugriff auf die FaceTime-App auf Geräten zulassen.

    Ab iOS/iPadOS 13.0 muss es sich bei Geräten mit dieser Einstellung um überwachte Geräte handeln.

- **Siri-Filter für anstößige Ausdrücke**: **Anfordern** verhindert, dass Siri anstößige Ausdrücke diktiert oder verwendet. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

  Legen Sie **Blockieren** für die **Siri**-Einstellung fest, um diese Einstellung zu verwenden.

  Diese Funktion gilt für:  
  - iOS 11.0 und neuer

- **Abfrage von benutzergenerierten Inhalten aus dem Internet durch Siri**: **Blockieren** verhindert, dass Siri auf Websites zugreifen darf, um Fragen zu beantworten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Siri den Zugriff auf benutzergenerierten Inhalt aus dem Internet gestatten.

  Legen Sie **Blockieren** für die **Siri**-Einstellung fest, um diese Einstellung zu verwenden.

- **Apple News**: **Blockieren** verhindert auf Geräten den Zugriff auf die Apple News-App. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Verwendung der Apple News-App zulassen.
- **iBooks Store**: **Blockieren** verhindert, dass auf den iBooks-Store zugegriffen werden kann. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, den iBooks Store zu durchsuchen und dort Bücher zu erwerben.
- **Nachrichten-App auf dem Gerät:** Wenn **Blockieren** für diese Einstellung festgelegt wird, werden Benutzer daran gehindert, die Nachrichten-App für iMessage zu verwenden. Wenn Geräte Textnachrichten unterstützen, können Benutzer weiterhin Textnachrichten per SMS senden und empfangen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Verwendung der Nachrichten-App zum Senden und Empfangen von Nachrichten über das Internet zulassen.
- **Podcasts**: **Blockieren** hindert Benutzer an der Verwendung der Podcasts-App. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Verwendung der Podcasts-App zulassen.
- **Musikdienst**: **Blockieren** setzt die Musik-App in den klassischen Modus zurück und deaktiviert den Musikdienst. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Verwendung der Apple Music-App zulassen.
- **iTunes Radio-Dienst**: **Blockieren** verhindert die Verwendung der iTunes Radio-App. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Verwendung der iTunes Radio-App zulassen.
- **iTunes Store:** **Blockieren** verhindert die Verwendung von iTunes auf Geräten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem iTunes erlauben.

  Diese Funktion gilt für:  
  - iOS 4.0 und neuer
  - iOS 13.0 und höher

- **Mein iPhone suchen:** Die Einstellung **Blockieren** verhindert die Verwendung dieses Features der App. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Verwendung des Such-App-Features zum Abrufen des ungefähren Standorts des Geräts zulassen.

  Diese Funktion gilt für:  
  - iOS 13.0 und neuer
  - iOS 13.0 und höher

- **Meine Freunde suchen:** Die Einstellung **Blockieren** verhindert die Verwendung dieses Features der App. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Verwendung des Such-App-Features zum Suchen von Familienmitgliedern und Freunden über ein Apple-Gerät oder iCloud.com zulassen.

  Diese Funktion gilt für:  
  - iOS 13.0 und neuer
  - iOS 13.0 und höher

- **Änderungen an den Einstellungen der App "Meine Freunde suchen"** : **Blockieren** verhindert, dass Änderungen an den Einstellungen der App „Meine Freunde suchen“ durchgeführt werden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern das Ändern von Einstellungen für die App „Meine Freunde suchen“ erlauben.

- **Spotlight-Suche gibt Ergebnisse aus dem Internet zurück**: **Blockieren** verhindert, dass Spotlight Ergebnisse einer Internetsuche zurückgibt. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem der Spotlight-Suchfunktion das Herstellen einer Verbindung mit dem Internet zur Bereitstellung von Suchergebnissen gestatten.

- **Entfernen von System-Apps vom Gerät blockieren**: **Blockieren** deaktiviert die Möglichkeit, System-Apps von Geräten zu entfernen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, System-Apps vom Gerät zu entfernen.

- **Safari**: **Blockieren** der Verwendung des Safari-Browsers auf Geräten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, den Safari-Browser zu verwenden.

  Ab iOS/iPadOS 13.0 muss es sich bei Geräten mit dieser Einstellung um überwachte Geräte handeln.

- **AutoAusfüllen in Safari**: Die Einstellung **Blockieren** deaktiviert das Feature zum automatischen Ausfüllen in Safari auf Geräten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, Einstellungen für AutoVervollständigen im Webbrowser zu ändern.

  Ab iOS/iPadOS 13.0 muss es sich bei Geräten mit dieser Einstellung um überwachte Geräte handeln.

## <a name="restricted-apps"></a>Eingeschränkte Apps

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Die Einstellungen gelten für: Geräteregistrierung, automatisierte Geräteregistrierung (überwacht)

- **Liste der eingeschränkten App-Typen:** Mit dieser Einstellung wird eine Liste der Apps erstellt, die Benutzer nicht installieren oder verwenden dürfen. Folgende Optionen sind verfügbar:

  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem möglicherweise den Zugriff auf von Ihnen zugewiesene Apps und integrierte Apps erlauben.
  - **Unzulässige Apps:** Listen Sie die (nicht von Intune verwalteten) Apps auf, die Benutzer nicht installieren und ausführen dürfen. Benutzer können unzulässige Apps nicht installieren. Wenn ein Benutzer eine App aus dieser Liste installiert, wird dies in Intune gemeldet.
  - **Genehmigte Apps:** Listet die Apps auf, die Benutzer installieren dürfen. Um die Kompatibilität zu gewährleisten, dürfen Benutzer keine anderen Apps installieren. Apps, die von Intune verwaltet werden, sind automatisch zugelassen, einschließlich der Unternehmensportal-App. Benutzer werden nicht daran gehindert, eine App zu installieren, die nicht in der Liste zulässiger Apps enthalten ist. Wenn sie es jedoch tun, wird dies in Intune gemeldet.

Um diesen Listen Apps hinzuzufügen, können Sie:

- Die iTunes App-Store-URL der App **hinzufügen**, die Sie wünschen. Geben Sie beispielsweise zum Hinzufügen der Microsoft Work Folders-App `https://itunes.apple.com/us/app/work-folders/id950878067?mt=8` oder `https://apps.apple.com/us/app/work-folders/id950878067?mt=8` ein.

  Um die URL einer App zu suchen, öffnen Sie den iTunes App Store, und suchen Sie nach der App. Suchen Sie beispielsweise nach `Microsoft Remote Desktop` oder `Microsoft Word`. Wählen Sie die App aus, und kopieren Sie die URL.

  Sie können auch iTunes verwenden, um die App zu suchen, und dann die Aufgabe **Link kopieren**, um die App-URL abzurufen.

- **Importieren** Sie eine CSV-Datei mit den Details der App, einschließlich der URL. Verwenden Sie das Format `<app url>, <app name>, <app publisher>`. **Exportieren** Sie alternativ eine vorhandene Liste, die die Liste der eingeschränkten Apps im gleichen Format enthält.

> [!IMPORTANT]
> Geräteprofile, die Einstellungen für eingeschränkte Apps verwenden, müssen Benutzergruppen zugewiesen werden.

## <a name="show-or-hide-apps"></a>Apps ein- oder ausblenden

Diese Funktion gilt für:

- iOS 9.3 und höher
- iOS 13.0 und höher

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Die Einstellungen gelten für: Automatisierte Geräteregistrierung (überwacht)

- **Liste der App-Typen:** Mit dieser Einstellung wird eine Liste der anzuzeigenden oder auszublendenden Apps erstellt. Sie können sowohl integrierte Apps als auch branchenspezifische Apps anzeigen oder ausblenden. Eine Liste der integrierten Apple-Apps finden Sie auf [dieser Apple-Website](https://support.apple.com/HT208094). Folgende Optionen sind verfügbar:

  - **Ausgeblendete Apps:** Geben Sie eine Liste von Apps an, die für Benutzer ausgeblendet werden. Benutzer können diese Apps weder anzeigen noch öffnen.
  
    Apple verhindert, dass einige native Apps ausgeblendet werden. Beispielsweise können Sie die App **Einstellungen** nicht auf dem Gerät ausblenden. Unter [Delete built-in Apple apps](https://support.apple.com/HT208094) (Löschen integrierter Apple-Apps) werden alle Apps aufgeführt, die ausgeblendet werden können.
  
  - **Sichtbare Apps:** Geben Sie eine Liste von Apps an, die Benutzer anzeigen und starten können. Es können keine anderen Apps angezeigt oder gestartet werden.

- **App-URL**: Geben Sie die App Store-URLs der Apps ein, die angezeigt oder ausgeblendet werden sollen. Beispiel:

  - Geben Sie zum Hinzufügen der Microsoft Work Folders-App `https://itunes.apple.com/us/app/work-folders/id950878067?mt=8` oder `https://apps.apple.com/us/app/work-folders/id950878067?mt=8` ein. 

  - Geben Sie zum Hinzufügen der Microsoft Word-App `https://itunes.apple.com/de/app/microsoft-word/id586447913` oder `https://apps.apple.com/de/app/microsoft-word/id586447913` ein.

  Um die URL einer App zu suchen, öffnen Sie den iTunes App Store, und suchen Sie nach der App. Suchen Sie beispielsweise nach `Microsoft Remote Desktop` oder `Microsoft Word`. Wählen Sie die App aus, und kopieren Sie die URL.

  Sie können auch iTunes verwenden, um die App zu suchen, und dann die Aufgabe **Link kopieren**, um die App-URL abzurufen.

- **App-Bündel-ID:** Geben Sie die [App-Bündel-ID](bundle-ids-built-in-ios-apps.md) der gewünschten App ein. Sie können sowohl integrierte Apps als auch branchenspezifische Apps anzeigen oder ausblenden. Eine Liste der integrierten Apple-Apps finden Sie auf [dieser Apple-Website](https://support.apple.com/HT208094).
- **App-Name:** Geben Sie den App-Namen der gewünschten App ein. Sie können sowohl integrierte Apps als auch branchenspezifische Apps anzeigen oder ausblenden. Eine Liste der integrierten Apple-Apps finden Sie auf [dieser Apple-Website](https://support.apple.com/HT208094).
- **Herausgeber**: Geben Sie den Herausgeber der gewünschten App ein.

Apps können Sie wie folgt hinzufügen:

- **Hinzufügen**: Verwenden Sie diese Option, um Ihre Liste mit Apps zu erstellen.
- **Importieren** Sie eine CSV-Datei mit den Details der App, einschließlich der URL. Verwenden Sie das Format `<app url>, <app name>, <app publisher>`. Oder **exportieren** Sie eine Datei im selben Format, um eine Liste der hinzugefügten eingeschränkten Apps zu erstellen.

## <a name="wireless"></a>Drahtlos

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Die Einstellungen gelten für: Geräteregistrierung, automatisierte Geräteregistrierung (überwacht)

- **Datenroaming:** **Blockieren** verhindert das Datenroaming über das Mobilfunknetzwerk. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Datenroaming zulassen, wenn das Gerät in einem Mobilfunknetz verwendet wird.

  > [!IMPORTANT]
  > Diese Einstellung wird als Remotegeräteaktion behandelt. Diese Einstellung wird also nicht im Verwaltungsprofil auf Geräten angezeigt. Jedes Mal, wenn der Datenroamingstatus auf dem Gerät geändert wird, wird **Datenroaming** durch den Intune-Dienst blockiert. Wenn der Berichtsstatus in Intune als erfolgreich gemeldet wird, können Sie davon ausgehen, dass die Einstellung funktioniert, obwohl sie nicht im Verwaltungsprofil auf dem Gerät angezeigt wird.

- **Globales Abrufen im Hintergrund beim Roaming:** **Blockieren** verhindert, dass das Feature des globalen Abrufens im Hintergrund beim Roaming über das Mobilfunknetz verwendet wird. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem zulassen, dass Geräte Daten wie E-Mails beim Roaming in einem Mobilfunknetz abrufen.
- **Sprachwahlverfahren:** **Blockieren** verhindert die Verwendung des Sprachwahlverfahrens auf Geräten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem das Sprachwahlverfahren auf Geräten zulassen.
- **Sprachroaming:** **Blockieren** verhindert das Sprachroaming über das Mobilfunknetzwerk. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Sprachroaming zulassen, wenn Geräte in einem Mobilfunknetz verwendet werden.
- **Privater Hotspot:** **Blockieren** schaltet den privaten Hotspot auf Geräten bei jeder Gerätesynchronisierung aus. Diese Einstellung kann mit einigen Anbietern nicht kompatibel sein. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Konfiguration des privaten Hotspots als von Benutzern festgelegten Standard beibehalten.

  > [!IMPORTANT]
  > Diese Einstellung wird als Remotegeräteaktion behandelt. Diese Einstellung wird also nicht im Verwaltungsprofil auf Geräten angezeigt. Jedes Mal, wenn der Status des privaten Hotspots auf dem Gerät geändert wird, wird die Einstellung **Privater Hotspot** vom Intune-Dienst blockiert. Wenn der Berichtsstatus in Intune als erfolgreich gemeldet wird, können Sie davon ausgehen, dass die Einstellung funktioniert, obwohl sie nicht im Verwaltungsprofil auf dem Gerät angezeigt wird.

- **Regeln für die Verwendung von Datenverbindungen (nur verwaltete Apps):** **Zulassen** definiert die Datentypen, die von verwalteten Apps genutzt werden können, wenn sie sich in Mobilfunknetzwerken befinden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Folgende Optionen sind verfügbar:
  - **Verwendung von Datenverbindungen blockieren:** Blockieren Sie die Verwendung von Datenverbindungen für **Alle verwalteten Apps**, oder Sie können **Bestimmte Apps wählen**.
  - **Verwendung von Datenverbindungen beim Roaming blockieren:** Blockieren Sie die Verwendung von Datenverbindungen beim Roaming für **Alle verwalteten Apps**, oder Sie können **Bestimmte Apps wählen**.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Die Einstellungen gelten für: Automatisierte Geräteregistrierung (überwacht)

- **Änderungen an den Einstellungen zur App-Mobilfunkdatennutzung**: **Blockieren** verhindert Änderungen an den Einstellungen der Mobilfunkdatennutzung von Apps. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, zu steuern, welche Apps Mobilfunkdaten verwenden dürfen.
- **Änderungen an den Einstellungen des Mobilfunktarifs**: **Blockieren** verhindert die Änderung von Einstellungen am Mobilfunktarifplan. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, Änderungen vorzunehmen.

  Diese Funktion gilt für:  
  - iOS 11.0 und neuer
  - iOS 13.0 und höher

- **Änderung des persönlichen Hotspots durch den Benutzer:** **Blockieren** verhindert die Änderung der Einstellungen für den privaten Hotspot. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, ihren privaten Hotspot zu aktivieren oder deaktivieren.

  Wenn Sie diese Einstellung und die Einstellung **Privater Hotspot** blockieren, wird der private Hotspot deaktiviert.

  Diese Funktion gilt für:  
  - iOS 12.2 und neuer
  - iOS 13.0 und höher

- **WLANs nur unter Verwendung von Konfigurationsprofilen beitreten**: **Anfordern** zwingt Geräte, nur WLAN-Netzwerke zu verwenden, die mithilfe von Intune-Konfigurationsprofilen eingerichtet wurden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Geräten erlauben, andere WLAN-Netzwerke zu verwenden.

  Stellen Sie sicher, dass das Gerät über ein WLAN-Profil verfügt, wenn **Erforderlich** für diese Einstellung festgelegt wird. Wenn Sie kein WLAN-Profil zuweisen, kann diese Einstellung verhindern, dass Geräte eine Verbindung mit dem Internet herstellen. Das bedeutet, dass das Herstellen einer Internetverbindung für das Gerät blockiert werden kann, wenn das Geräteeinschränkungsprofil vor dem WLAN-Profil zugewiesen wird.
  
  Wenn keine Verbindung hergestellt werden kann, heben Sie die Registrierung des Geräts auf, und registrieren Sie es noch mal mit einem WLAN-Profil. Legen Sie für diese Einstellung anschließend in einem Geräteeinschränkungsprofil die Option **Erforderlich** fest, und weisen Sie das Profil dem Gerät zu.

- **WLAN immer aktiviert:** **Erfordern** lässt WLAN in der App „Einstellungen“ aktiviert. Das WLAN kann weder in den Einstellungen noch im Kontrollzentrum deaktiviert werden, selbst wenn das Gerät sich im Flugmodus befindet. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, WLAN zu aktivieren oder auszuschalten.

  Durch die Konfiguration dieser Einstellung werden Benutzer nicht daran gehindert, ein WLAN-Netzwerk auszuwählen.

  Diese Funktion gilt für:  
  - iOS 13.0 und neuer
  - iOS 13.0 und höher

## <a name="connected-devices"></a>Verbundene Geräte

### <a name="settings-apply-to-all-enrollment-types"></a>Die Einstellungen gelten für: Alle Registrierungstypen

- **Handgelenkerkennung für gekoppelte Apple Watch:** **Erfordern** erzwingt, dass eine gekoppelte Apple Watch die Handgelenkerkennung verwendet. Wenn dies erforderlich ist, zeigt die Apple Watch keine Benachrichtigungen an, wenn sie nicht getragen wird. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Die Einstellungen gelten für: Geräteregistrierung, automatisierte Geräteregistrierung (überwacht)

- **Kopplungskennwort für ausgehende AirPlay-Anforderungen anfordern:** **Anfordern** benötigt bei der Verwendung von AirPlay ein Kopplungskennwort zum Streamen von Inhalten auf anderen Apple-Geräten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern das Streamen von Inhalten über AirPlay ohne Kennworteingabe ermöglichen.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Die Einstellungen gelten für: Automatisierte Geräteregistrierung (überwacht)

- **AirDrop**: Die Einstellung **Blockieren** verhindert die Verwendung von AirDrop auf Geräten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Verwendung von AirDrop zum Austauschen von Inhalten mit Geräten in der Nähe zulassen.
- **Apple Watch-Kopplung:** **Blockieren** verhindert die Kopplung mit einer Apple Watch. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Gerätekopplung mit einer Apple Watch zulassen.
- **Bluetooth-Änderung**: **Blockieren** verhindert die Änderung von Bluetootheinstellungen auf Geräten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, diese Einstellungen zu ändern.
- **Hostkopplung zum Steuern der Geräte, mit denen ein iOS/iPadOS-Gerät gekoppelt werden kann**: **Blockieren** verhindert die Hostkopplung. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Hostkopplung zulassen, damit der Administrator steuern kann, mit welchen Geräten ein iOS/iPadOS-Gerät gekoppelt werden darf.
- **AirPrint blockieren**: **Blockieren** verhindert die Verwendung des AirPrint-Features auf Geräten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, AirPrint zu verwenden.
  - **Speicherung von AirPrint-Anmeldeinformationen im Schlüsselbund blockieren**: **Blockieren** verhindert, dass Benutzername und Kennwort auf Geräten im Keychain-Speicher gespeichert werden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem das Speichern von AirPrint-Benutzername und -Kennwort in der Keychain-App zulassen.
  - **Vertrauenswürdiges TLS-Zertifikat für AirPrint erforderlich**: **Anfordern** erzwingt, dass Geräte für die TLS-Druckkommunikation ein vertrauenswürdiges Zertifikat verwenden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
  - **iBeacon-Ermittlung durch AirPrint-Drucker blockieren**: **Blockieren** hindert schädliche Air Print Bluetooth-Beacons am Pishing nach Netzwerkdatenverkehr. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem das Ankündigen von AirPrint-Druckern auf Geräten zulassen.
- **Einrichten neuer Geräte in der Nähe blockieren**: **Blockieren** deaktiviert die Aufforderung zum Einrichten neuer Geräte, die sich in der Nähe befinden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem zulassen, Benutzer aufzufordern, sich mit anderen Apple-Geräten in der Nähe zu verbinden.

  Diese Funktion gilt für:  
  - iOS 11.0 und neuer
  - iOS 13.0 und höher

- **Zugriff auf Dateien in USB-Laufwerk:** Geräte können eine Verbindung mit Dateien auf einem USB-Laufwerk herstellen und diese öffnen. Wenn **Deaktivieren** für diese Einstellung festgelegt wird, wird der Gerätezugriff auf das USB-Laufwerk in der App „Dateien“ blockiert, wenn ein USB-Gerät mit dem Gerät verbunden ist. Wenn dieses Feature deaktiviert wird, können Benutzer auch keine Dateien auf ein USB-Laufwerk verschieben, das mit einem iPad verbunden ist. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem den Zugriff auf ein USB-Laufwerk über die App „Dateien“ zulassen.

  Diese Funktion gilt für:  
  - iOS 13.0 und neuer
  - iOS 13.0 und höher

## <a name="keyboard-and-dictionary"></a>Tastatur und Wörterbuch

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Die Einstellungen gelten für: Automatisierte Geräteregistrierung (überwacht)

- **Suche nach Wortdefinition**: **Blockieren** verhindert die Markierung eines Worts und das anschließende Suchen nach seiner Definition. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem den Zugriff auf die Definitionssuchfunktion zulassen.
- **Tastaturwortvorschläge**: **Blockieren** verhindert die Verwendung von Tastaturwortvorschlägen für Wörter, die der Benutzer möglicherweise verwenden möchte. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Es besteht die Möglichkeit, dass das Betriebssystem dieses Feature standardmäßig nicht zulässt.
- **Autokorrektur**: **Blockieren** verhindert die Verwendung von Autokorrektur. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Geräten die automatische Korrektur falsch geschriebener Wörter gestatten.
- **Rechtschreibprüfung über Tastatur:** **Blockieren** verhindert die Rechtschreibprüfung. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Verwendung der Rechtschreibprüfung zulassen.
- **Tastenkombinationen:** **Blockieren** hindert Benutzer an der Verwendung von Tastenkombinationen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Verwendung von Tastenkombinationen auf Geräten zulassen.
- **Dictation**: **Blockieren** verhindert, dass Benutzer die Spracheingabe zur Eingabe von Text verwenden können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, die Diktatfunktion zu verwenden.
- **QuickPath:** Wenn **Blockieren** festgelegt wird, können Benutzer QuickPath nicht verwenden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, QuickPath zu verwenden, wodurch eine kontinuierliche Eingabe über die Tastatur des Geräts ermöglicht wird. Benutzer können Wörter durch Wischgesten auf den Tasten schreiben.

  Diese Funktion gilt für:  
  - iOS 13.0 und neuer
  - iOS 13.0 und höher

## <a name="cloud-and-storage"></a>Cloud und Speicher

### <a name="settings-apply-to-all-enrollment-types"></a>Die Einstellungen gelten für: Alle Registrierungstypen

- **Verschlüsselte Sicherung:** **Anfordern** erzwingt die Verschlüsselung von Gerätesicherungen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Synchronisierung verwalteter Apps mit der Cloud:** **Blockieren** verhindert, dass mit Intune verwaltete Apps Daten mit dem iCloud-Konto des Benutzers synchronisieren. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem diesen Daten erlauben, eine Synchronisierung mit iCloud durchzuführen.
- **Enterprise Book-Sicherung blockieren:** **Blockieren** verhindert die Sicherung von Enterprise Books. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, diese Bücher zu sichern.
- **Synchronisierung von Enterprise Book-Metadaten blockieren (Notizen und Highlights):** **Blockieren** verhindert, dass Notizen und Highlights in Enterprise Books synchronisiert werden können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Synchronisierung zulassen.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Die Einstellungen gelten für: Geräteregistrierung, automatisierte Geräteregistrierung (überwacht)

- **Synchronisierung von Fotostreams in iCloud:** **Blockieren** verhindert die Fotostream-Synchronisierung mit iCloud. Wenn dieses Feature blockiert wird, kann es zu Datenverlust kommen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern das Aktivieren von **Mein Fotostream** auf ihren Geräten zum Synchronisieren mit iCloud erlauben, damit Fotos auf allen Geräten der Benutzer verfügbar sind.
- **iCloud-Fotomediathek:** **Blockieren** deaktiviert die Verwendung der iCloud-Fotomediathek zum Speichern von Fotos und Videos in der Cloud. Fotos, die nicht vollständig aus der iCloud-Fotomediathek auf Geräte heruntergeladen wurden, werden vom Gerät entfernt. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Verwendung der iCloud-Fotomediathek zulassen.
- **Streaming freigegebener Fotos:** **Blockieren** deaktiviert die **iCloud-Fotofreigabe** auf Geräten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem das Streamen freigegebener Fotos zulassen.
- **Handoff:** **Blockieren** hindert Benutzer daran, Arbeit auf einem iOS/iPadOS-Gerät zu beginnen und diese dann auf einem anderen iOS/iPadOS- oder macOS-Gerät fortzusetzen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Es besteht die Möglichkeit, dass das Betriebssystem diese Übergabe standardmäßig zulässt.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Die Einstellungen gelten für: Automatisierte Geräteregistrierung (überwacht)

- **In iCloud sichern:** **Blockieren** hindert Benutzer daran, Geräte in iCloud zu sichern. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, Geräte in iCloud zu sichern.

  Ab iOS/iPadOS 13.0 muss es sich bei Geräten mit dieser Einstellung um überwachte Geräte handeln.

- **iCloud-Dokumentsynchronisierung blockieren**: **Blockieren** hindert iCloud daran, Dokumente und Daten zu synchronisieren. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Dokument- und Schlüssel-/Wertsynchronisierung in Ihrem iCloud-Speicher zulassen.

  Ab iOS/iPadOS 13.0 muss es sich bei Geräten mit dieser Einstellung um überwachte Geräte handeln.

- **Synchronisierung zwischen iCloud und Keychain blockieren:** **Blockieren** deaktiviert die Synchronisierung in Keychain gespeicherter Anmeldeinformationen mit iCloud. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, diese Anmeldeinformationen zu synchronisieren.

  Ab iOS/iPadOS 13.0 muss es sich bei Geräten mit dieser Einstellung um überwachte Geräte handeln.

## <a name="autonomous-single-app-mode"></a>Modus der autonomen einzelnen App

Verwenden Sie diese Einstellungen, um iOS-/iPadOS-Geräte zur Ausführung bestimmter Apps im autonomen Einzelanwendungsmodus zu konfigurieren. Wenn dieser Modus konfiguriert ist und Benutzer eine der konfigurierten Apps starten, wird das Gerät für diese App gesperrt. Benutzer können die App bzw. den Task erst dann wechseln, wenn sie die zulässige App schließen.

Sie können beispielsweise für eine Schul- oder Universitätsumgebung eine App hinzufügen, mit der Benutzer einen Test auf dem Gerät durchführen können. Alternativ können Sie auch das Gerät in der Unternehmensportal-App sperren, bis sich der Benutzer authentifiziert hat. Wenn Benutzer die App-Aktionen abschließen oder Sie diese Richtlinie entfernen, kehrt das Gerät in seinen normalen Zustand zurück.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Die Einstellungen gelten für: Automatisierte Geräteregistrierung (überwacht)

- **App-Name:** Geben Sie den Namen der gewünschten App ein.
- **App-Bündel-ID:** Geben Sie die [Bündel-ID](bundle-ids-built-in-ios-apps.md) der gewünschten App ein.
- **Hinzufügen**: Verwenden Sie diese Option, um Ihre Liste mit Apps zu erstellen.

**Importieren** Sie alternativ eine CSV-Datei mit der Liste der App-Namen und der Bündel-IDs. **Exportieren** Sie alternativ eine vorhandene Liste, die die Apps enthält.

## <a name="kiosk"></a>Kiosk

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Die Einstellungen gelten für: Automatisierte Geräteregistrierung (überwacht)

- **App zur Ausführung im Kioskmodus:** Wählen Sie die App-Typen aus, die Sie im Kioskmodus ausführen möchten. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Standardmäßig besteht die Möglichkeit, dass das Betriebssystem Kioskeinstellungen nicht anwendet. Das Gerät wird nicht im Kioskmodus ausgeführt.
  - **Store-App:** Geben Sie die URL zu einer App im iTunes App-Store ein.
  - **Verwaltete App:** Wählen Sie eine App aus, die Sie zuvor zu Intune hinzugefügt haben.
  - **Integrierte App:** Geben Sie die [Bündel-ID](bundle-ids-built-in-ios-apps.md) der integrierten App ein.

- **Touch-Unterstützung:** **Anfordern** der Barrierefreiheitseinstellung „Touch-Unterstützung“ auf Geräten. Diese Funktion hilft Benutzern mit Bildschirmgesten bei Vorgängen, die für sie schwierig sein könnten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Es besteht die Möglichkeit, dass das Betriebssystem dieses Feature im Kioskmodus standardmäßig nicht ausführt oder aktiviert.
- **Farben umkehren:** **Anfordern** der Barrierefreiheitseinstellung „Farben umkehren“, die die Anzeige für Benutzer mit eingeschränkter Sehfähigkeit anpasst. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Es besteht die Möglichkeit, dass das Betriebssystem dieses Feature im Kioskmodus standardmäßig nicht ausführt oder aktiviert.
- **Mono-Audio:** **Anfordern** der Barrierefreiheitseinstellung „Mono-Audio“ auf Geräten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Es besteht die Möglichkeit, dass das Betriebssystem dieses Feature im Kioskmodus standardmäßig nicht ausführt oder aktiviert.
- **Sprachsteuerung**: Bei der Einstellung **Erforderlich** wird die Sprachsteuerung auf Geräten aktiviert. Dies ermöglicht Benutzern die vollständige Steuerung des Betriebssystems mithilfe von Siri-Befehlen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Sprachsteuerung deaktivieren.

  Diese Einstellung gilt für:  
  - iOS 13.0 und neuer
  - iOS 13.0 und höher
  
  > [!TIP]
  > Wenn Ihre Organisation über branchenspezifische Apps verfügt, die die **Sprachsteuerung** nicht zum Release von iOS 13.0 unterstützt, wird empfohlen, dass Sie die Einstellung **Nicht konfiguriert** beibehalten.

- **VoiceOver:** **Anfordern** der Barrierefreiheitseinstellung „VoiceOver“, um Text auf dem Bildschirm laut vorlesen zu lassen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Es besteht die Möglichkeit, dass das Betriebssystem dieses Feature im Kioskmodus standardmäßig nicht ausführt oder aktiviert.
- **Zoom:** **Erfordern** der Zoomeinstellung, sodass Benutzer den Bildschirm zum Hereinzoomen berühren können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Es besteht die Möglichkeit, dass das Betriebssystem dieses Feature im Kioskmodus standardmäßig nicht ausführt oder aktiviert.
- **Automatische Sperre:** Bei der Einstellung **Blockieren** wird die automatische Sperrung von Geräten deaktiviert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Es besteht die Möglichkeit, dass das Betriebssystem dieses Feature standardmäßig nicht zulässt.
- **Ruftonschalter:** **Blockieren** deaktiviert den Ruftonschalter (Stummschaltung) an Geräten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Es besteht die Möglichkeit, dass das Betriebssystem dieses Feature standardmäßig nicht zulässt.
- **Automatische Ausrichtung:** **Blockieren** verhindert, dass die Bildschirmausrichtung geändert werden kann, wenn Benutzer das Gerät drehen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Es besteht die Möglichkeit, dass das Betriebssystem dieses Feature standardmäßig nicht zulässt.
- **Standbytaste:** **Blockieren** deaktiviert die Taste für Standby/Aktivierung des Bildschirms an Geräten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Es besteht die Möglichkeit, dass das Betriebssystem dieses Feature standardmäßig nicht zulässt.
- **Touch:** **Blockieren** deaktiviert den Touchscreen der Geräte. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzern erlauben, den Touchscreen zu verwenden.
- **Lautstärkeregler:** Bei der Einstellung **Blockieren** werden die Lautstärkeregler der Geräte deaktiviert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem die Lautstärkeregler zulassen.
- **AssistiveTouch-Steuerung:** Wenn Sie **Zulassen** auswählen, können Benutzer die Funktion „AssistiveTouch“ verwenden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem diese Funktion deaktivieren.
- **Steuerelement zum Umkehren von Farben:** **Zulassen** von Farbumkehr-Anpassungen, mit denen der Benutzer die Funktion zur Farbumkehr individuell verwenden kann. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem diese Funktion deaktivieren.
- **Ausgewählten Text sprechen:** **Zulassen** der Barrierefreiheitseinstellungen „Auswahl vorlesen“ auf Geräten. Diese Funktion liest von Benutzern ausgewählte Texte vor. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem diese Funktion deaktivieren.
- **Änderung der Sprachsteuerung:** Bei der Einstellung **Zulassen** können Benutzer den Zustand der Sprachsteuerung auf ihren Geräten ändern. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Benutzer daran hindern, den Zustand der Sprachsteuerung auf ihren Geräten zu ändern.

  Diese Einstellung gilt für:  
  - iOS 13.0 und neuer
  - iOS 13.0 und höher

- **VoiceOver-Steuerelement:** **Zulassen** von VoiceOver-Änderungen, damit Benutzer die VoiceOver-Funktion aktualisieren können, z. B. wie schnell auf dem Bildschirm ausgegebener Text von der Sprachausgabe vorgelesen wird. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem VoiceOver-Änderungen verhindern.
- **Zoomsteuerelement:** **Zulassen** von Zoomänderungen durch Benutzer. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Zoomänderungen verhindern.

> [!NOTE]
> Damit Sie ein iOS/iPadOS-Gerät für den Kioskmodus konfigurieren können, müssen Sie das Apple Configurator-Tool oder das Apple-Programm zur Geräteregistrierung verwenden, um Geräte in den überwachten Modus zu versetzen. Informationen zur Verwendung des Apple Configurator-Tools finden Sie im Apple-Handbuch.
> Wenn die iOS/iPadOS-App, die Sie eingeben, nach der Zuweisung des Profils installiert wird, wird das Gerät erst nach einem Neustart in den Kioskmodus versetzt.

## <a name="domains"></a>Domänen

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Die Einstellungen gelten für: Geräteregistrierung, automatisierte Geräteregistrierung (überwacht)

- **Nicht markierte E-Mail-Domänen** > **E-Mail-Domänen-URL**: Fügen Sie der Liste eine oder mehrere URLs hinzu. Wenn Benutzer eine E-Mail von einer anderen Domäne als den von Ihnen eingegebenen erhalten, wird die E-Mail in der iOS/iPadOS-Mail-App als nicht vertrauenswürdig gekennzeichnet.

- **Verwaltete Webdomänen** > **Webdomänen-URL**: Fügen Sie der Liste eine oder mehrere URLs hinzu. Wenn Dokumente von den Domänen, die Sie eingeben, heruntergeladen werden, gelten sie als verwaltet. Diese Einstellung gilt nur für Dokumente, die mit dem Safari-Browser heruntergeladen werden.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Die Einstellungen gelten für: Automatisierte Geräteregistrierung (überwacht)

- **Domänen für automatisches Ausfüllen des Safari-Kennworts** > **Domänen-URL**: Fügen Sie der Liste eine oder mehrere URLs hinzu. Benutzer können nur Webkennwörter von URLs in dieser Liste speichern. Diese Einstellung gilt nur für den Safari-Browser und Geräte im überwachten Modus. Wenn Sie keine URLs eingeben, können Kennwörter von allen Websites gespeichert werden.

  Diese Einstellung gilt für:  
  - iOS 9.3 und höher
  - iOS 13.0 und höher

## <a name="settings-that-require-supervised-mode"></a>Einstellungen, die den überwachten Modus erfordern

Der überwachte Modus von iOS/iPadOS kann nur während der ersten Einrichtung des Geräts über das Apple-Programm zur Geräteregistrierung oder mithilfe von Apple Configurator aktiviert werden. Sobald der überwachte Modus aktiviert ist, kann Intune ein Gerät mit folgenden Funktionen konfigurieren:

- App-Sperre (Einzelanwendungsmodus) 
- Globaler HTTP-Proxy 
- Aktivierungssperre deaktivieren 
- Modus der autonomen einzelnen App 
- Webinhaltsfilter 
- Festlegen von Hintergrund und Sperrbildschirm 
- App-Pushbenachrichtigung im Hintergrund 
- Always On-VPN 
- Zulassen von ausschließlich verwalteter App-Installation 
- iBookstore 
- iMessages 
- Gamecenter 
- AirDrop 
- AirPlay 
- Hostkopplung 
- Cloudsynchronisierung 
- Spotlight-Suche 
- Übergabe 
- Gerät löschen 
- Einschränkungen-Benutzeroberfläche 
- Installation von Konfigurationsprofilen von der Benutzeroberfläche 
- News 
- Tastenkombinationen 
- Kennungsänderungen 
- Änderungen des Gerätenamens 
- Automatische App-Downloads 
- Apple Music 
- E-Mail-Ablage 
- Kopplung mit Apple Watch 

> [!NOTE]
> Apple hat angekündigt, dass bestimmte Einstellungen im Jahr 2019 in den überwachten Modus übergehen. Bedenken Sie dies, wenn Sie diese Einstellungen verwenden, und warten Sie nicht, bis Apple diese zum überwachten Modus migriert:
>
> - App-Installation durch Benutzer
> - App-Deinstallation
> - FaceTime
> - Safari
> - iTunes
> - Anstößiger Inhalt
> - Dokumente und Daten von iCloud
> - Multiplayerspiele
> - Game Center-Freunde hinzufügen
> - Siri

## <a name="next-steps"></a>Nächste Schritte

[Zuweisen von Profilen](device-profile-assign.md) und [Überwachen von Profilen](device-profile-monitor.md)

Sie können auch Gerätefeatures und -einstellungen auf [macOS](device-restrictions-macos.md)-Geräten einschränken.
