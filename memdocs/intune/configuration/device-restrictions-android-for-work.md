---
title: Android Enterprise-Geräteeinstellungen in Microsoft Intune – Azure | Microsoft-Dokumentation
description: 'Auf Geräten mit Android Enterprise oder Android for Work können Sie auf dem Gerät Einstellungen einschränken, darunter folgende: Kopieren und Einfügen, Benachrichtigungen anzeigen, App-Berechtigungen, Datenfreigabe, Kennwortlänge, Anmeldefehler, Entsperren per Fingerabdruck, Wiederverwenden von Kennwörtern und Aktivieren der Freigabe von Geschäftskontakten per Bluetooth. Konfigurieren Sie Geräte als dedizierten Gerätekiosk zur Ausführung einer oder mehrerer Apps.'
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/31/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: chmaguir, chrisbal, priyar
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure, seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: b213769234d55fd2a542ac166afe59c6e8b9e6c2
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/31/2020
ms.locfileid: "89194105"
---
# <a name="android-enterprise-device-settings-to-allow-or-restrict-features-using-intune"></a>Android Enterprise-Geräteeinstellungen zum Zulassen oder Einschränken von Features mit Intune

In diesem Artikel werden die verschiedenen Einstellungen aufgeführt und beschrieben, die Sie auf Android Enterprise-Geräten steuern können. Verwenden Sie als Bestandteil Ihrer Lösung für die mobile Geräteverwaltung (Mobile Device Management, MDM) diese Einstellungen, um Funktionen zuzulassen oder zu deaktivieren, Apps auf dedizierten Geräten auszuführen, die Sicherheit zu steuern usw.

## <a name="before-you-begin"></a>Vorbereitung

[Erstellen Sie eine Gerätekonfigurationsprofil.](device-restrictions-configure.md)

## <a name="fully-managed-dedicated-and-corporate-owned-work-profile"></a>Vollständig verwaltet, dediziert und unternehmenseigen mit einem Arbeitsprofil

Diese Einstellungen gelten für Android Enterprise-Registrierungstypen, bei denen das gesamte Gerät von Intune verwaltet wird, z. B. vollständig verwaltete Geräte, dedizierte Geräte und unternehmenseigene Android Enterprise-Arbeitsprofilgeräte.

Einige Einstellungen werden nicht von allen Registrierungstypen unterstützt. Informationen dazu, welche Einstellungen von welchen Registrierungstypen unterstützt werden, finden Sie in der Benutzeroberfläche. Jede Einstellung befindet sich unter einer Überschrift, die angibt, von welchen Registrierungstypen diese Einstellung verwendet werden kann.

![Überschriften von Einstellungen](./media/device-restrictions-android-for-work/setting-headers.png)

Einige Einstellungen gelten nur auf Arbeitsprofilebene für unternehmenseigene Geräte mit einem Arbeitsprofil. Diese Einstellungen gelten für vollständig verwaltete und dedizierte Geräte weiterhin auf Geräteebene. Diese Einstellungen sind in der Benutzeroberfläche mit dem Deskriptor *(Arbeitsprofilebene)* gekennzeichnet.

![Überschriften von Einstellungen](./media/device-restrictions-android-for-work/work-profile-level.png)


### <a name="general"></a>Allgemein

- **Bildschirmaufnahme:** **Blockieren** verhindert, dass Screenshots oder Bildschirmaufnahmen auf dem Gerät vorgenommen werden. Zudem wird verhindert, dass der Inhalt auf Anzeigegeräten angezeigt wird, die über keine sichere Videoausgabe verfügen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Das Betriebssystem lässt möglicherweise standardmäßig zu, dass Benutzer den Bildschirminhalt als Bild erfassen.
- **Kamera:** **Blockieren** verhindert den Zugriff auf die Kamera des Geräts. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise den Zugriff auf die Kamera zu.

  Intune verwaltet nur den Zugriff auf die Kamera des Geräts. Das Programm kann nicht auf Bilder oder Videos zugreifen.

- **Standardberechtigungsrichtlinie:** Diese Einstellung definiert die Standardberechtigungsrichtlinie für Anforderungen für Laufzeitberechtigungen. Folgende Optionen sind verfügbar:
  - **Gerätestandard:** Die Standardeinstellung des Geräts wird verwendet.
  - **Eingabeaufforderung:** Benutzer werden dazu aufgefordert, die Berechtigung zu genehmigen.
  - **Automatisch zulassen:** Berechtigungen werden automatisch gewährt.
  - **Automatisch ablehnen:** Berechtigungen werden automatisch verweigert.
- **Datums- und Uhrzeitänderungen:** Wenn **Blockieren** festgelegt wird, können Benutzer das Datum und die Uhrzeit nicht manuell festlegen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Das Betriebssystem erlaubt Benutzern möglicherweise standardmäßig, das Datum und die Uhrzeit auf dem Gerät festzulegen.
- **Änderung der Lautstärke:** **Blockieren** verhindert, dass Benutzer die Lautstärke des Geräts ändern können. Außerdem wird die Hauptlautstärke des Geräts stummgeschaltet. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Das Betriebssystem erlaubt Benutzern möglicherweise standardmäßig, die Lautstärkeeinstellungen auf dem Gerät festzulegen.
- **Auf Werkseinstellungen zurücksetzen:** Wenn **Blockieren** festgelegt wird, können Benutzer die Option zum Zurücksetzen auf Werkseinstellungen in den Einstellungen des Geräts nicht verwenden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Das Betriebssystem erlaubt Benutzern möglicherweise standardmäßig, diese Einstellung auf dem Gerät zu verwenden.
- **Abgesicherter Start:** Wenn **Blockieren** festgelegt wird, können Benutzer das Gerät nicht im abgesicherten Modus neustarten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Das Betriebssystem erlaubt Benutzern möglicherweise standardmäßig, das Gerät im abgesicherten Modus neu zu starten.
- **Statusleiste:** Wenn **Blockieren** festgelegt wird, wird der Zugriff auf die Statusleiste, einschließlich der Benachrichtigungen und Schnelleinstellungen verhindert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Das Betriebssystem erlaubt Benutzern möglicherweise standardmäßig den Zugriff auf die Statusleiste.
- **Roamingdatendienste:** **Blockieren** verhindert das Datenroaming über das Mobilfunknetzwerk. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem Datenroaming zulassen, wenn das Gerät in einem Mobilfunknetz verwendet wird.
- **Änderung der WLAN-Einstellungen:** Wenn **Blockieren** festgelegt wird, werden Benutzer daran gehindert, die vom Gerätebesitzer festgelegten WLAN-Einstellungen zu ändern. Benutzer können eigene WLAN-Konfigurationen erstellen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Das Betriebssystem erlaubt Benutzern möglicherweise standardmäßig, die WLAN-Einstellungen auf dem Gerät zu ändern.
- **Konfiguration des WLAN-Zugriffspunkts:** Wenn **Blockieren** festgelegt wird, können Benutzer WLAN-Konfigurationen weder erstellen noch ändern. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Das Betriebssystem erlaubt Benutzern möglicherweise standardmäßig, die WLAN-Einstellungen auf dem Gerät zu ändern.
- **Bluetooth-Konfiguration:** Wenn **Blockieren** festgelegt wird, können Benutzer das Bluetooth auf dem Gerät nicht konfigurieren. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Das Betriebssystem erlaubt die Verwendung von Bluetooth auf dem Gerät möglicherweise standardmäßig.
- **Tethering und Zugriff auf Hotspots:** Wenn **Blockieren** festgelegt wird, werden Zugriff und Tethering auf portable Hotspots verhindert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Das Betriebssystem erlaubt Tethering und Zugriff auf portable Hotspots möglicherweise standardmäßig.
- **USB-Speicher:** Wählen Sie **Zulassen** aus, um auf USB-Speicher auf dem Gerät zuzugreifen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Das Betriebssystem verhindert den Zugriff auf USB-Speicher möglicherweise standardmäßig.
- **USB-Dateiübertragung:** Wenn **Blockieren** festgelegt wird, wird die Übertragung von Dateien über USB verhindert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Das Betriebssystem erlaubt das Übertragen von Dateien möglicherweise standardmäßig.
- **Externe Medien:** Wenn **Blockieren** festgelegt wird, werden die Verwendung und das Herstellen einer Verbindung mit externen Medien auf dem Gerät verhindert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Das Betriebssystem erlaubt externe Medien auf dem Gerät möglicherweise standardmäßig.
- **Daten mithilfe von NFC übertragen:** Wenn **Blockieren** festgelegt wird, wird die Verwendung der NFC-Technologie zum Übertragen von Daten aus Apps verhindert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Das Betriebssystem erlaubt die Verwendung von NFC zum Freigeben von Daten zwischen Geräten möglicherweise standardmäßig.
- **Debugfunktionen:** Wenn Sie **Zulassen** auswählen, können Benutzer Features zum Debuggen auf dem Gerät verwenden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Das Betriebssystem hindert Benutzer möglicherweise standardmäßig daran, Debuggingfeatures auf dem Gerät zu verwenden.
- **Mikrofonanpassung:** Wenn **Blockieren** festgelegt wird, werden Benutzer daran gehindert, die Stummschaltung der Mikrofons aufzuheben und die Mikrofonlautstärke anzupassen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Das Betriebssystem erlaubt das Verwenden und Anpassen der Lautstärke des Mikrofons möglicherweise standardmäßig.
- **E-Mail-Adressen für Schutz vor Zurücksetzung auf Werkseinstellungen:** Wählen Sie **E-Mail-Adressen für Google-Konto** aus. Geben Sie die E-Mail-Adressen der Geräteadministratoren ein, die das Gerät entsperren können, nachdem es zurückgesetzt wurde. Achten Sie darauf, dass Sie die E-Mail-Adressen durch ein Semikolon trennen, z. B. `admin1@gmail.com;admin2@gmail.com`. Wenn keine E-Mail-Adresse eingegeben wird, kann jeder das Gerät entsperren, sobald die Werkseinstellungen wiederhergestellt sind. Diese E-Mail-Adressen sind nur gültig, wenn eine nicht vom Benutzer gestartete Zurücksetzung auf die Werkseinstellungen durchgeführt wird, z. B. über das Wiederherstellungsmenü.

  Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

- **Notausstieg für Netzwerk:** Wenn **Aktivieren** festgelegt wird, können Benutzer das Feature „Notausstieg für Netzwerk“ aktivieren. Wenn beim Starten des Geräts keine Netzwerkverbindung hergestellt wird, fordert die Notausstiegsfunktion zum Herstellen einer vorübergehenden Verbindung mit einem Netzwerk und Aktualisieren der Geräterichtlinie auf. Nach dem Anwenden der Richtlinie wird das temporäre Netzwerk ignoriert, und das Gerät setzt den Start fort. Dieses Feature verbindet Geräte mit einem Netzwerk, wenn:
  - Kein geeignetes Netzwerk in der letzten Richtlinie enthalten ist.
  - Das Gerät im Aufgabensperrmodus in eine App startet.
  - Benutzer können die Geräteeinstellungen nicht aufrufen.

  Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Das Betriebssystem hindert Benutzer möglicherweise standardmäßig daran, das Feature „Notausstieg für Netzwerk“ auf dem Gerät zu aktivieren.

- **Systemupdate:** Hier können Sie eine Option auswählen, um zu definieren, wie das Gerät Over-the-Air-Updates verarbeitet. Folgende Optionen sind verfügbar:
  - **Gerätestandard:** Die Standardeinstellung des Geräts wird verwendet.
  - **Automatisch:** Updates werden ohne Interaktion mit dem Benutzer automatisch installiert. Durch das Festlegen dieser Richtlinie werden sofort alle ausstehenden Updates installiert.
  - **Zurückgestellt:** Updates werden für 30 Tage zurückgestellt. Nach Ablauf der 30 Tage fordert Android die Benutzer zur Installation des Updates auf. Gerätehersteller oder Mobilfunkanbieter können verhindern (ausschließen), dass wichtige Sicherheitsupdates zurückgestellt werden. Bei einem ausgeschlossenen Update wird den Benutzern eine Systembenachrichtigung auf dem Gerät angezeigt.
  - **Wartungsfenster:** Updates werden automatisch in einem täglichen Wartungsfenster installiert, das Sie in Intune festlegen. Die Installation wird 30 Tage lang täglich versucht, und es kann aufgrund von zu geringem Speicherplatz oder Akkustand ein Fehler auftreten. Nach 30 Tagen fordert Android die Benutzer zur Installation auf. Dieses Fenster wird auch verwendet, um Updates für Google Play-Apps zu installieren. Verwenden Sie diese Option für dedizierte Geräte wie etwa Kioskgeräte, da Apps, die im Vordergrund auf einem dedizierten Gerät im Einzelanwendungsmodus ausgeführt werden, aktualisiert werden können.

- **Benachrichtigungsfenster:** Wenn **Deaktivieren** ausgewählt ist, werden Fensterbenachrichtigungen, wie Popups, eingehende Anrufe, ausgehende Anrufe, Systemwarnungen und Systemfehler, nicht auf dem Gerät angezeigt. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Das Betriebssystem zeigt Benachrichtigungen möglicherweise standardmäßig an.
- **Hinweise zur ersten Verwendung überspringen:** **Aktivieren** führt dazu, dass Vorschläge von Apps beim Durchführen von Tutorials oder Hinweise beim Start einer App ausgeblendet oder übersprungen werden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Das Betriebssystem zeigt diese Vorschläge möglicherweise standardmäßig beim Starten der App an.

### <a name="system-security"></a>Systemsicherheit

- **Bedrohungsüberprüfung für Apps:** Die Standardeinstellung **Anfordern** aktiviert Google Play Protect so, dass Apps vor und nach der Installation überprüft werden. Wenn eine Bedrohung erkannt wird, wird der Benutzer gewarnt, damit er die App vom Gerät entfernt. Wenn die Einstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert. Google Play Protect wird möglicherweise nicht vom Betriebssystem zum Scannen von Apps aktiviert oder ausgeführt.

### <a name="device-experience"></a>Benutzeroberfläche des Geräts

Verwenden Sie diese Einstellungen, um eine Kioskoberfläche auf Ihren dedizierten Geräten zu konfigurieren oder den Startbildschirm auf vollständig verwalteten Geräten anzupassen. Sie können Geräte zum Ausführen einer oder mehrerer Apps konfigurieren. Im Kioskmodus eines Geräts stehen nur die Apps zur Verfügung, die Sie hinzufügen.

**Registrierungsprofiltyp:** Wählen Sie einen Registrierungsprofiltyp aus, um mit dem Konfigurieren von Microsoft Launcher oder Microsoft Managed Home Screen auf Ihren Geräten zu beginnen. Folgende Optionen sind verfügbar:

- **Nicht konfiguriert:** Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Standardmäßig wird Benutzern möglicherweise die Standardbenutzeroberfläche für den Startbildschirm des Geräts angezeigt.
- **Dediziertes Gerät:** Konfigurieren Sie eine Kioskoberfläche auf Ihren dedizierten Geräten. Stellen Sie vor dem Konfigurieren dieser Einstellungen sicher, dass Sie die gewünschten Apps für die Geräte [hinzufügen](../apps/apps-add-android-for-work.md) und [zuweisen](../apps/apps-deploy.md).

  - **Kioskmodus:** Wählen Sie aus, ob auf dem Gerät eine App oder mehrere Apps ausgeführt werden. Folgende Optionen sind verfügbar:

    - **Nicht konfiguriert:** Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
    - **Einzelne App**: Benutzer können auf dem Gerät nur auf eine einzelne App zugreifen. Wenn das Gerät gestartet wird, wird nur die jeweilige App gestartet. Benutzer können keine neuen Apps öffnen oder die ausgeführte App ändern.

      - **App zur Verwendung im Kioskmodus auswählen:** Wählen Sie die verwaltete Google Play-App aus der Liste aus.

      > [!IMPORTANT]
      > Wenn Sie den Kioskmodus für eine einzelne App verwenden, funktionieren Wähltasten-/Telefon-Apps möglicherweise nicht ordnungsgemäß.
  
    - **Multi-App**: Benutzer können auf dem Gerät nur auf eine begrenzte Anzahl von Apps zugreifen. Wenn das Gerät gestartet wird, werden nur die von Ihnen hinzugefügten Apps gestartet. Sie können auch einige Weblinks hinzufügen, die Benutzer öffnen können. Wenn die Richtlinie angewendet wird, können Benutzer die Symbole für die zulässigen Apps auf dem Startbildschirm sehen.

      > [!IMPORTANT]
      > Für dedizierte Geräte mit mehreren Apps **muss** die [Managed Home Screen-App](https://play.google.com/work/apps/details?id=com.microsoft.launcher.enterprise) aus Google Play:
      >   - [in Intune hinzugefügt sein](../apps/apps-add-android-for-work.md)
      >   - [der Gerätegruppe zugewiesen sein](../apps/apps-deploy.md), die für Ihre dedizierten Geräte erstellt wurde.
      >
      > Die App **Managed Home Screen** muss zwar nicht im Konfigurationsprofil enthalten sein, allerdings muss sie als App hinzugefügt werden. Wenn die App **Managed Home Screen** hinzugefügt wird, werden alle anderen Apps, die Sie im Konfigurationsprofil hinzufügen, in **Managed Home Screen** als Symbole angezeigt.
      >
      > Wenn Sie den Normalmodus (Kiosk mit mehreren Apps) verwenden, funktionieren Apps mit Wähltasten/Telefon-Apps möglicherweise nicht ordnungsgemäß.
      >
      > Weitere Informationen zum verwalteten Startbildschirm finden Sie unter [Einrichten des verwalteten Startbildschirms auf dedizierten Geräten im Kioskmodus mit mehreren Apps](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-managed-home-screen-on-dedicated-devices/ba-p/1388060).

      - **Hinzufügen**: Wählen Sie Ihre Apps aus der Liste aus.

        Wenn die **Managed Home Screen**-App nicht aufgeführt wird, [fügen Sie sie aus Google Play hinzu](https://play.google.com/work/apps/details?id=com.microsoft.launcher.enterprise). Achten Sie darauf, [die App der Gerätegruppe zuzuweisen](../apps/apps-deploy.md), die für Ihre dedizierten Geräte erstellt wurde.

        Sie können auch andere [Android-Apps](../apps/apps-add-android-for-work.md) und [Web-Apps](../apps/web-app.md) hinzufügen, die von Ihrer Organisation für das Gerät erstellt wurden. Achten Sie darauf, [die App der Gerätegruppe zuzuweisen, die für Ihre dedizierten Geräte erstellt wurde](../apps/apps-deploy.md).

      - **Ordnersymbol:** Wählen Sie die Farbe und die Form des Ordnersymbols aus, das auf dem verwalteten Startbildschirm angezeigt wird. Folgende Optionen sind verfügbar:
        - Nicht konfiguriert 
        - Dunkles Design: Rechteck
        - Dunkles Design: Kreis
        - Helles Design: Rechteck
        - Helles Design: Kreis
      - **Symbolgröße für Apps und Ordner:** Wählen Sie die Größe des Ordnersymbols aus, das auf dem verwalteten Startbildschirm angezeigt wird. Folgende Optionen sind verfügbar:
        - Nicht konfiguriert 
        - Sehr klein
        - Klein
        - Mittelwert
        - Groß
        - Sehr groß

          Abhängig von der Bildschirmgröße kann die tatsächliche Symbolgröße abweichen.

      - **Bildschirmausrichtung:** Wählen Sie die Ausrichtung des verwalteten Startbildschirms auf dem Gerät aus. Folgende Optionen sind verfügbar:
        - Nicht konfiguriert
        - Hochformat
        - Querformat
        - Automatisch drehen
      - **App-Infobadges:** Bei Auswahl von **Aktivieren** wird die Anzahl der neuen und ungelesenen Benachrichtigungen für App-Symbole angezeigt. Wenn die Einstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.
      - **Virtuelle Startschaltfläche:** Eine Softkey-Schaltfläche, die Benutzer auf den verwalteten Startbildschirm zurückleitet, damit Benutzer zwischen Apps wechseln können. Folgende Optionen sind verfügbar:
        - **Nicht konfiguriert** (Standardeinstellung): Es wird keine Startschaltfläche angezeigt. Benutzer müssen die Schaltfläche „Zurück“ verwenden, um zwischen Apps wechseln zu können.
        - **Nach oben wischen:** Eine Startschaltfläche wird angezeigt, wenn ein Benutzer auf dem Gerät nach oben wischt.
        - **Unverankert:** Auf dem Gerät wird dauerhaft eine unverankerte Startschaltfläche angezeigt.

      - **Kioskmodus verlassen:** Wenn **Aktivieren** festgelegt wird, können Administratoren der Kioskmodus vorübergehend pausieren, um ein Update für das Gerät durchzuführen. Um dieses Feature verwenden zu können, führt der Administrator Folgendes aus:
  
        1. Weiteres Betätigen der Schaltfläche „Zurück“, bis die Schaltfläche **Kiosk beenden** angezeigt wird. 
        2. Auswählen der Schaltfläche **Kiosk beenden** und Eingabe der PIN für den **Code zum Verlassen des Kioskmodus**.
        3. Wenn Sie fertig sind, wählen Sie die App **Verwalteter Startbildschirm** aus. Mit diesem Schritt wird das Gerät erneut im Multi-App-Kioskmodus gesperrt.

        Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise hindert das Betriebssystem Administratoren standardmäßig am Pausieren des Kioskmodus. Wenn der Administrator weiterhin die Schaltfläche „Zurück“ betätigt und die Schaltfläche **Kiosk beenden** auswählt, wird eine Meldung angezeigt, dass eine Kennung erforderlich ist.

      - **Code zum Verlassen des Kioskmodus:** Geben Sie eine 4-6-stellige numerische PIN ein. Der Administrator verwendet diese PIN zum vorübergehenden Anhalten des Kioskmodus.

      - **Benutzerdefinierten URL-Hintergrund festlegen:** Geben Sie eine URL zum Anpassen des Hintergrundbildschirms auf dem dedizierten Gerät ein. Geben Sie beispielsweise `http://contoso.com/backgroundimage.jpg` ein.

        > [!NOTE]
        > In den meisten Fällen empfehlen wir, mit Bildern mit mindestens den folgenden Größen zu beginnen:
        >
        > - Smartphone: 1080 x 1920 Pixel
        > - Tablet: 1920 × 1080 Pixel
        >
        > Für ein optimales Erlebnis und scharfe Details wird empfohlen, Bildobjekte gerätebezogen gemäß den Displayspezifikationen zu erstellen.
        >
        > Moderne Displays haben höhere Pixeldichten und können entsprechende Bilder mit 2K-/4K-Auflösung anzeigen.

      - **Verknüpfung mit Einstellungsmenü:** Bei Auswahl von **Deaktivieren** wird die Verknüpfung zu den verwalteten Einstellungen auf dem verwalteten Startbildschirm ausgeblendet. Benutzer können weiterhin nach unten wischen, um auf die Einstellungen zuzugreifen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Die Verknüpfung zu den verwalteten Einstellungen wird auf Geräten standardmäßig angezeigt. Benutzer können auch nach unten wischen, um auf diese Einstellungen zuzugreifen.

      - **Schnellzugriff auf Debugmenü:** Mit dieser Einstellung wird gesteuert, wie Benutzer auf das Debugmenü zugreifen. Folgende Optionen sind verfügbar:

        - **Aktivieren**: Benutzer können einfacher auf das Debugmenü zugreifen. Sie können insbesondere nach unten wischen oder die Verknüpfung zu den verwalteten Einstellungen verwenden. Wie immer können sie weiterhin 15 Mal auf die Schaltfläche „Zurück“ tippen.
        - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Der einfache Zugriff auf das Debugmenü ist standardmäßig deaktiviert. Benutzer müssen 15 Mal auf die Schaltfläche „Zurück“ tippen, um das Debugmenü zu öffnen.

        Über das Debugmenü können Benutzer folgende Aktionen durchführen:

        - Anzeigen und Hochladen von Protokollen zum verwalteten Startbildschirm
        - Öffnen der Android Device Policy Manager-App von Google
        - Öffnen der [Microsoft Intune-App](https://play.google.com/store/apps/details?id=com.microsoft.intune)
        - Verlassen des Kioskmodus

      - **WLAN-Konfiguration:** Wenn **Aktivieren** festgelegt wird, wird das WLAN-Steuerelement auf dem verwalteten Startbildschirm angezeigt und Benutzer können das Gerät mit verschiedenen WLAN-Netzwerken verbinden. Durch Aktivieren dieses Features wird auch der Gerätestandort aktiviert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise zeigt das Betriebssystem das WLAN-Steuerelement standardmäßig nicht auf dem verwalteten Startbildschirm an. Dieser Wert verhindert, dass Benutzer Verbindungen mit WLAN-Netzwerken herstellen, während Sie den verwalteten Startbildschirm verwenden.

        - **WLAN-Zulassungsliste:** Erstellen Sie eine Liste gültiger WLAN-Netzwerknamen, auch bekannt als Service Set Identifier (SSID). Benutzer des verwalteten Startbildschirms können nur Verbindungen mit den SSIDs herstellen, die Sie eingeben.

          Wenn kein Wert angegeben wird, ändert oder aktualisiert Intune diese Einstellung nicht. In der Standardeinstellung sind alle verfügbaren WLAN-Netzwerke zulässig.

          **Importieren** Sie eine CSV-Datei, die eine Liste gültiger SSIDs enthält.

          **Exportieren** Sie Ihre aktuelle Liste in eine CSV-Datei.

        - **SSID**: Sie können auch die WLAN-Netzwerknamen (SSID) eingeben, mit denen Benutzer des verwalteten Startbildschirms eine Verbindung herstellen können. Geben Sie gültige SSIDs ein.

      - **Bluetooth-Konfiguration:** Wenn **Aktivieren** festgelegt wird, wird das Bluetooth-Steuerelement auf dem verwalteten Startbildschirm angezeigt und Benutzer können Geräte über Bluetooth koppeln. Durch Aktivieren dieses Features wird auch der Gerätestandort aktiviert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise zeigt das Betriebssystem das Bluetooth-Steuerelement standardmäßig nicht auf dem verwalteten Startbildschirm an. Dieser Wert verhindert, dass Benutzer Bluetooth konfigurieren und Geräte koppeln, während sie den verwalteten Startbildschirm verwenden.

      - **Zugriff auf Taschenlampe:** Wenn **Aktivieren** festgelegt wird, wird das Taschenlampensteuerelement auf dem verwalteten Startbildschirm angezeigt und Benutzer können die Taschenlampenfunktion ein- und ausschalten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise zeigt das Betriebssystem das Taschenlampensteuerelement standardmäßig nicht auf dem verwalteten Startbildschirm an. Dieser Wert verhindert, dass Benutzer die Taschenlampe verwenden, während sie den verwalteten Startbildschirm verwenden.

      - **Medienlautstärkeregler:** Wenn **Aktivieren** festgelegt wird, wird der Medienlautstärkeregler auf dem verwalteten Startbildschirm angezeigt und Benutzer können die Medienlautstärke des Geräts mithilfe eines Reglers anpassen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise zeigt das Betriebssystem das Medienlautstärkesteuerelement standardmäßig nicht auf dem verwalteten Startbildschirm an. Dieser Wert verhindert, dass Benutzer die Medienlautstärke auf dem Gerät anpassen können, während sie den verwalteten Startbildschirm verwenden, außer die Tasten ihrer Hardware unterstützen dies.

      - **Schnellzugriff auf Geräteinformationen:** Bei Auswahl von **Aktivieren** können Benutzer durch Wischen nach unten die Geräteinformationen zum verwalteten Startbildschirm anzeigen, z. B. die Seriennummer, die Herstellungs- und Modellnummer und die SDK-Ebene. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. In der Standardeinstellung werden die Geräteinformationen möglicherweise nicht angezeigt.

      - **Bildschirmschonermodus:** **Aktivieren** zeigt einen Bildschirmschoner auf dem verwalteten Startbildschirm, wenn das Gerät gesperrt ist oder im Fall eines Timeouts. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise zeigt das Betriebssystem keinen Bildschirmschoner auf dem verwalteten Startbildschirm an.

        Wenn diese Einstellung aktiviert ist, konfigurieren Sie auch die folgende Einstellung:

        - **Benutzerdefiniertes Hintergrundbild für Bildschirmschoner festlegen:** Geben Sie die URL zu einem benutzerdefinierten PNG-, JPG-, JPEG-, GIF-, MBP-, WebP- oder ICO-Bild an. Wenn Sie keine URL eingeben, wird das Standardbild des Geräts verwendet, wenn es ein Standardbild gibt.

          Geben Sie z. B. Folgendes ein:

          - `http://www.contoso.com/image.jpg`
          - `www.contoso.com/image.bmp`
          - `https://www.contoso.com/image.webp`

          > [!TIP]
          > Alle URLs zu Dateiressourcen, die in das Bitmap-Format umgewandelt werden können, werden unterstützt.

        - **Die Anzahl von Sekunden, die das Gerät den Bildschirmschoner anzeigt, bevor der Bildschirm deaktiviert wird:** Wählen Sie aus, wie lange der Bildschirmschoner auf dem Gerät angezeigt werden soll. Geben Sie einen Wert zwischen 0 und 9999999 Sekunden ein. Der Standardwert beträgt `0` Sekunden. Wenn das Feld leer gelassen wird oder auf `0` (null) festgelegt ist, ist der Bildschirmschoner solange aktiv, bis ein Benutzer mit dem Gerät interagiert.
        - **Anzahl von Sekunden, in denen das Gerät inaktiv ist, bevor der Bildschirmschoner angezeigt wird:** Wählen Sie aus, wie lange ein Gerät inaktiv sein kann, bevor der Bildschirmschoner angezeigt wird. Geben Sie einen Wert zwischen 1 und 9999999 Sekunden ein. Der Standardwert beträgt `30` Sekunden. Geben Sie eine Zahl ein, die größer als null (`0`) ist.
        - **Vor dem Start des Bildschirmschoners Medien ermitteln:** **Aktivieren** (Standardwert) zeigt den Bildschirmschoner nicht an, wenn auf dem Gerät Audio- oder Videodateien wiedergeben werden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise zeigt das Betriebssystem den Bildschirmschoner standardmäßig an, auch wenn Audiodateien oder Videos abgespielt werden.

- **Vollständig verwaltet:** Mit dieser Einstellung wird die Microsoft Launcher-App auf vollständig verwalteten Geräten konfiguriert.

  - Über **Microsoft Launcher als Standardstartprogramm festlegen:** **Aktivieren** wird Microsoft Launcher als Standardstartprogramm auf dem Startbildschirm festgelegt. Wenn Sie Launcher als Standard festlegen, können Benutzer kein anderes Startprogramm verwenden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig wird Microsoft Launcher nicht als Standardstartprogramm erzwungen.
  - **Konfigurieren des benutzerdefinierten Hintergrundbilds:** Bei Auswahl von **Aktivieren** können Sie Ihr eigenes Bild als Hintergrundbild des Bildschirms verwenden und festlegen, ob Benutzer das Bild ändern können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. In der Standardeinstellung werden die aktuellen Hintergrundbilder der Geräte beibehalten.
    - **Eingeben der URL des Hintergrundbilds:** Geben Sie die URL des Hintergrundbilds ein. Dieses Bild wird auf dem Startbildschirm des Geräts angezeigt. Geben Sie beispielsweise `http://www.contoso.com/image.jpg` ein. 
    - **Benutzern das Ändern des Hintergrundbilds erlauben:** Bei Auswahl von **Aktivieren** können Benutzer das Hintergrundbild ändern. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. In der Standardeinstellung werden Benutzer daran gehindert, den Hintergrund zu ändern.
  - **Aktivieren des Startfeeds:** Bei Auswahl von **Aktivieren** wird der Startfeed mit Anzeige von Kalendern, Dokumenten und aktuellen Aktivitäten aktiviert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. In der Standardeinstellung wird dieser Feed nicht angezeigt.
    - **Benutzern das Aktivieren/Deaktivieren des Feeds erlauben:** Bei Auswahl von **Aktivieren** können Benutzer den Startfeed aktivieren bzw. deaktivieren. Bei Auswahl von **Aktivieren** wird diese Einstellung nur bei der erstmaligen Zuweisung des Profils erzwungen. Bei zukünftigen Profilzuweisungen wird diese Einstellung nicht erzwungen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. In der Standardeinstellung werden Benutzer daran gehindert, die Einstellungen des Startfeeds zu ändern.
  - **Dockanzeige:** Das Dock ermöglicht Benutzern den schnellen Zugriff auf ihre Apps und Tools. Folgende Optionen sind verfügbar:
    - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
    - **Anzeigen:** Das Dock wird auf Geräten angezeigt.
    - **Ausblenden:** Das Dock wird ausgeblendet. Benutzer müssen nach oben wischen, um auf das Dock zuzugreifen.
    - **Deaktiviert:** Das Dock wird auf Geräten nicht angezeigt, und Benutzer können es nicht anzeigen.

  - **Benutzern das Ändern der Dockanzeige erlauben:** Bei Auswahl von **Aktivieren** können Benutzer das Dock anzeigen bzw. ausblenden. Bei Auswahl von **Aktivieren** wird diese Einstellung nur bei der erstmaligen Zuweisung des Profils erzwungen. Bei zukünftigen Profilzuweisungen wird diese Einstellung nicht erzwungen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. In der Standardeinstellung können Benutzer die Gerätedockkonfiguration nicht ändern.

  - **Platzierung der Suchleiste:** Wählen Sie aus, wo die Suchleiste platziert werden soll. Folgende Optionen sind verfügbar:
    - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
    - **Oben:** Die Suchleiste wird oben auf den Geräten angezeigt.
    - **Unten:** Die Suchleiste wird unten auf den Geräten angezeigt.
    - **Ausblenden:** Die Suchleiste wird ausgeblendet.

<!-- MandiA (7.16.2020) The following settings may be in a future release. Per PM, we can leave it in GitHub, not live. Remove comment tags if/when it releases.
  - **Allow user to change search bar placement**: **Enable** allows users to change the location of the search bar. **Enable** only forces this setting the first time the profile is assigned. Any future profile assignments don't force this setting. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, users are prevented from changing the location.
End of comment -->

### <a name="password"></a>Kennwort

- **Sperrbildschirm deaktivieren**: Wenn Sie **Deaktivieren** auswählen, können Benutzer das Bildschirmsperrfeature Keyguard nicht auf dem Gerät verwenden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise erlaubt das Betriebssystem Benutzern standardmäßig die Verwendung der Keyguard-Features.
- **Deaktivierte Sperrbildschirmfeatures**: Wenn Keyguard auf dem Gerät aktiviert ist, wählen Sie die Features aus, die Sie deaktivieren möchten. Ist beispielsweise **Kamera absichern** ausgewählt, ist die Kamerafunktion auf dem Gerät deaktiviert. Alle nicht ausgewählten Features sind auf dem Gerät aktiviert.

  Diese Features sind für Benutzer verfügbar, wenn das Gerät gesperrt ist. Benutzer können mit einem Häkchen versehene Features weder anzeigen noch darauf zugreifen.

- **Erforderlicher Kennworttyp:** Geben Sie den erforderlichen Grad der Kennwortkomplexität ein, und bestimmen Sie, ob biometrische Geräte zulässig sind. Folgende Optionen sind verfügbar:
  - **Gerätestandard**
  - **Kennwort erforderlich, keine Einschränkungen**
  - **Schwach biometrisch**: [Vergleich von stark und schwach biometrisch](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (öffnet Android-Website)
  - **Numerisch**: Kennwort darf nur aus Zahlen bestehen. Beispiel: `123456789`. Geben Sie außerdem Folgendes ein:
    - **Minimale Kennwortlänge:** Geben Sie die Mindestlänge des Kennworts ein (4 bis 16 Zeichen).
  - **Numerisch, komplex:** Sich wiederholende oder fortlaufende Ziffern wie „1111“ oder „1234“ sind nicht zulässig. Geben Sie außerdem Folgendes ein:
    - **Minimale Kennwortlänge:** Geben Sie die Mindestlänge des Kennworts ein (4 bis 16 Zeichen).
  - **Alphabetisch**: Buchstaben des Alphabets sind erforderlich. Zahlen und Symbole sind nicht erforderlich. Geben Sie außerdem Folgendes ein:
    - **Minimale Kennwortlänge:** Geben Sie die Mindestlänge des Kennworts ein (4 bis 16 Zeichen).
  - **Alphanumerisch**: Schließt Großbuchstaben, Kleinbuchstaben und Ziffern ein. Geben Sie außerdem Folgendes ein:
    - **Minimale Kennwortlänge:** Geben Sie die Mindestlänge des Kennworts ein (4 bis 16 Zeichen).
  - **Alphanumerisch mit Symbolen**: Schließt Großbuchstaben, Kleinbuchstaben, Ziffern, Interpunktionszeichen und Symbole ein. Geben Sie außerdem Folgendes ein:

    - **Minimale Kennwortlänge:** Geben Sie die Mindestlänge des Kennworts ein (4 bis 16 Zeichen).
    - **Erforderliche Zeichenanzahl**: Geben Sie die erforderliche Anzahl von Zeichen des Kennworts ein (0 bis 16 Zeichen).
    - **Erforderliche Anzahl Kleinbuchstaben**: Geben Sie die erforderliche Anzahl Kleinbuchstaben für das Kennwort ein, von 0 bis 16 Zeichen.
    - **Erforderliche Anzahl Großbuchstaben**: Geben Sie die erforderliche Anzahl Großbuchstaben für das Kennwort ein, von 0 bis 16 Zeichen.
    - **Erforderliche Anzahl anderer Zeichen als Buchstaben**: Geben Sie die erforderliche Anzahl anderer Zeichen als Buchstaben (alles außer Buchstaben im Alphabet) für das Kennwort ein, von 0 bis 16 Zeichen.
    - **Erforderliche Anzahl numerischer Zeichen**: Geben Sie die erforderliche Anzahl numerischer Zeichen (`1`, `2`, `3` usw.) für das Kennwort ein, von 0 bis 16 Zeichen.
    - **Erforderliche Anzahl Symbole**: Geben Sie die erforderliche Anzahl der Symbole (`&`, `#`, `%` usw.) für das Kennwort ein, von 0 bis 16 Zeichen.

- **Anzahl Tage bis zum Kennwortablauf**: Geben Sie die Anzahl der Tage ein, bis das Gerätekennwort geändert werden muss (von 1 bis 365). Geben Sie beispielsweise `90` an, damit das Kennwort nach 90 Tagen abläuft. Wenn das Kennwort abläuft, werden Benutzer aufgefordert, ein neues Kennwort zu erstellen. Wenn kein Wert angegeben ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.
- **Anzahl erforderlicher Kennwörter, bevor ein Benutzer ein Kennwort wiederverwenden kann**: Verwenden Sie diese Einstellung, um zu verhindern, dass Benutzer zuvor verwendete Kennwörter erstellen. Geben Sie die Anzahl der zuvor verwendeten Kennwörter ein, die nicht erneut verwendet werden können, von 1–24. Geben Sie z.B. `5` an, damit ein Benutzer sein neues Kennwort nicht auf sein aktuelles Kennwort oder eines seiner vorherigen vier Kennwörter festlegen kann. Wenn kein Wert angegeben ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.
- **Anzahl von fehlgeschlagenen Anmeldungen, bevor das Gerät zurückgesetzt wird:** Geben Sie an, wie häufig ein falsches Kennwort eingegeben werden kann, bevor das Gerät zurückgesetzt wird (zwischen 4 und 11). Wenn `0` (null) festgelegt wird, wird möglicherweise die Funktion zum Zurücksetzen des Geräts deaktiviert. Wenn kein Wert angegeben ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.

  > [!NOTE]
  > Auf vollständig verwalteten Geräten, dedizierten Geräten und unternehmenseigenen Arbeitsprofilgeräten wird keine Aufforderung zum Festlegen eines Kennworts angezeigt. Die Einstellungen sind erforderlich, Benutzer werden jedoch möglicherweise nicht benachrichtigt. Benutzer müssen das Kennwort manuell festlegen. Die Richtlinie wird so lange als fehlgeschlagen gemeldet, bis der Benutzer ein Kennwort festlegt, das Ihren Anforderungen entspricht.

### <a name="power-settings"></a>Energieeinstellungen

- **Zeit bis Bildschirmsperre:** Geben Sie die maximale Zeit an, die ein Benutzer als Zeit bis zur Bildschirmsperre festlegen kann. Wenn Sie beispielsweise `10 minutes` für diese Einstellung festlegen, können Benutzer eine beliebige Zeit zwischen 15 Sekunden und 10 Minuten angeben. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

- **Bildschirm aktiviert, wenn Gerät angeschlossen ist:** Hiermit kann ausgewählt werden, bei welchen Stromquellen der Bildschirm des Geräts aktiviert bleibt, wenn es angeschlossen ist.

### <a name="users-and-accounts"></a>Benutzer und Konten

- **Neue Benutzer hinzufügen:** Wenn **Blockieren** festgelegt wird, können Benutzer keine neuen Benutzer hinzufügen. Jeder Benutzer hat einen persönlichen Bereich auf dem Gerät für benutzerdefinierte Startseiten, Konten, Apps und Einstellungen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise erlaubt das Betriebssystem Benutzern das Hinzufügen anderer Benutzer zum Gerät standardmäßig.
- **Entfernen von Benutzern:** Wenn **Blockieren** festgelegt wird, können Benutzer keine Benutzer entfernen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise erlaubt das Betriebssystem Benutzern das Entfernen anderer Benutzer vom Gerät standardmäßig.
- **Kontoänderungen** (nur dedizierte Geräte) Wenn **Blockieren** festgelegt wird, können Benutzer Konten nicht bearbeiten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise erlaubt das Betriebssystem Benutzern standardmäßig das Anpassen von Benutzerkonten auf dem Gerät.

  > [!NOTE]
  > Diese Einstellung gilt nicht für vollständig verwaltete Geräte, dedizierte Geräte und unternehmenseigene Arbeitsprofilgeräte. Wenn Sie diese Einstellung konfigurieren, wird die Einstellung ignoriert und hat keine Auswirkungen.

- **Benutzer kann Anmeldeinformationen konfigurieren:** **Blockieren** verhindert, dass Benutzer Zertifikate konfigurieren, die Geräten zugewiesen sind, auch wenn es sich um Geräte handelt, die keinem Benutzerkonto zugewiesen sind. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise ermöglicht das Betriebssystem Benutzern standardmäßig das Konfigurieren oder Ändern ihrer Anmeldeinformationen, wenn sie im Schlüsselspeicher auf diese zugreifen.
- **Persönliche Google-Konten:** **Blockieren** verhindert, dass Benutzer ihre privaten Google-Konten auf dem Gerät hinzufügen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise erlaubt das Betriebssystem Benutzern standardmäßig das Hinzufügen ihrer persönlichen Google-Konten.

### <a name="applications"></a>Applications

- **Installation aus unbekannten Quellen zulassen:** Wenn **Zulassen** festgelegt wird, können Benutzer **unbekannte Quellen** aktivieren. Diese Einstellung ermöglicht die Installation von Apps aus unbekannten Quellen, einschließlich anderer Quellen als Google Play Store. Sie ermöglicht Benutzern das Querladen von Apps auf das Gerät mit anderen Mitteln als dem Google Play Store. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise hindert das Betriebssystem Benutzer standardmäßig am Aktivieren von **unbekannten Quellen**.
- **Zugriff auf alle Apps im Google Play Store zulassen**: Wenn diese Option auf **Zulassen** festgelegt ist, erhalten Benutzer Zugriff auf alle Apps im Google Play Store. Sie erhalten keinen Zugriff auf die Apps, die der Administrator in [Client-Apps](../apps/apps-add-android-for-work.md) sperrt.

  Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig geht das Betriebssystem möglicherweise wie folgt vor:
  
  - Es erzwingt, dass Benutzer nur auf die vom Administrator zur Verfügung gestellten Apps im Google Play Store oder in [Client-Apps](../apps/apps-add-android-for-work.md) als erforderlich gekennzeichneten Apps zugreifen können. 
  - Es deinstalliert alle Apps, bei denen erkannt wird, dass sie von Benutzern nicht aus dem Google Play Store installiert wurden.

  Wenn Sie das Querladen aktivieren möchten, legen Sie die Einstellungen **Installation über unbekannte Quellen zulassen** und **Zugriff auf alle Apps im Google Play Store zulassen** auf **Zulassen** fest.

- **Automatische App-Updates:** Geräte suchen täglich nach App-Updates. Wählen Sie diese Option aus, wenn automatische Updates installiert werden. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert:** Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
  - **Benutzerauswahl:** Dies ist möglicherweise die Standardoption des Betriebssystems. Benutzer können ihre Einstellungen in der App für verwaltetes Google Play festlegen.
  - **Nie:** Bei dieser Einstellung werden keine Updates installiert. Von der Verwendung dieser Option wird abgeraten.
  - **Nur WLAN:** Bei dieser Einstellung werden Updates nur installiert, wenn das Gerät mit einem WLAN-Netzwerk verbunden ist.
  - **Immer:** Bei dieser Einstellung werden Updates installiert, sobald sie verfügbar sind.

### <a name="connectivity"></a>Verbindung

- **Always On-VPN:** Wenn **Aktivieren** festgelegt wird, wird der VPN-Client so festgelegt, dass er automatisch eine Verbindung mit dem VPN herstellt bzw. wiederherstellt. Always On-VPN-Verbindungen bleiben aktiv. Alternativ wird die Verbindung sofort wiederhergestellt, wenn der Benutzer sein Gerät sperrt, das Gerät neu gestartet wird oder das Drahtlosnetzwerk geändert wird.

  Wählen Sie **Nicht konfiguriert** aus, um das Always On-VPN für alle VPN-Clients zu deaktivieren.

  > [!IMPORTANT]
  > Stellen Sie sicher, dass Sie nur eine Always On-VPN-Richtlinie auf einem einzelnen Gerät bereitstellen. Die Bereitstellung mehrerer Always On-VPN-Richtlinien auf einem einzelnen Gerät wird nicht unterstützt.

- **VPN-Client:** Wählen Sie einen VPN-Client aus, der Always On unterstützt. Folgende Optionen sind verfügbar:
  - Cisco AnyConnect
  - F5 Access
  - Palo Alto Networks GlobalProtect
  - Pulse Secure
  - Benutzerdefiniert
    - **Paket-ID:** Geben Sie die Paket-ID der App im Google Play Store ein. Wenn z. B. die URL für die App im Play Store `https://play.google.com/store/details?id=com.contosovpn.android.prod` lautet, dann ist die Paket-ID `com.contosovpn.android.prod`.

  > [!IMPORTANT]
  > - Der von Ihnen ausgewählte VPN-Client muss auf dem Gerät installiert sein und VPN pro Anwendung in Arbeitsprofilen unterstützen. Andernfalls tritt ein Fehler auf. 
  > - Sie müssen die VPN-Client-App im **verwalteten Google Play Store** genehmigen, die App mit Intune synchronisieren und die App auf dem Gerät bereitstellen. Danach wird die App im Arbeitsprofil des Benutzers installiert.
  > - Sie müssen den VPN-Client dann trotzdem noch mit einem [VPN-Profil](vpn-settings-android-enterprise.md) oder über ein [App-Konfigurationsprofil](../apps/app-configuration-policies-use-android.md) konfigurieren.
  > - Es gibt eventuell bekannte Probleme bei der Verwendung von VPN pro App mit F5 Access for Android 3.0.4. Weitere Informationen finden Sie unter [Versionshinweise zu F5 Access for Android 3.0.4](https://support.f5.com/kb/en-us/products/big-ip_apm/releasenotes/related/relnote-f5access-android-3-0-4.html#relnotes_known_issues_f5_access_android).

- **Sperrmodus:** Wenn **Aktivieren** festgelegt wird, wird jeglicher Netzwerkdatenverkehr durch den VPN-Tunnel erzwungen. Wenn keine Verbindung zum VPN hergestellt wird, hat das Gerät keinen Netzwerkzugriff. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem den Datenverkehr durch den VPN-Tunnel oder über das Mobilfunknetz standardmäßig zu.

- **Empfohlener globaler Proxy:** Wenn **Aktivieren** festgelegt wird, wird ein globaler Proxy zu den Geräten hinzugefügt. Wenn diese Einstellung aktiviert ist, wird für HTTP- und HTTPS-Datenverkehr einschließlich einiger Apps auf dem Gerät den von Ihnen eingegebenen Proxy. Dieser Proxy ist nur eine Empfehlung. Es ist möglich, dass einige Apps den Proxy nicht verwenden. **Nicht konfiguriert** (Standardwert) fügt keinen empfohlenen globalen Proxy hinzu.

  Weitere Informationen zu diesem Feature finden Sie auf der Android-Website zu [setRecommendedGlobalProxy](https://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#setRecommendedGlobalProxy(android.content.ComponentName,%20android.net.ProxyInfo)).

  Wenn diese Einstellung aktiviert ist, geben Sie auch den **Proxytyp** ein. Folgende Optionen sind verfügbar:

  - **Direkt:** Geben Sie die Proxyserverdetails manuell ein, einschließlich der folgenden:
    - **Host:** Geben Sie den Hostnamen oder die IP-Adresse Ihres Proxy Servers ein. Geben Sie beispielsweise `proxy.contoso.com` oder `127.0.0.1` ein.
    - **Portnummer:** Geben Sie die vom Proxyserver verwendete TCP-Portnummer ein. Geben Sie beispielsweise `8080` ein.
    - **Ausgeschlossene Hosts:** Geben Sie eine Liste von Hostnamen oder IP-Adressen ein, die den Proxy nicht verwenden. Diese Liste kann ein Asterisk-Platzhalterzeichen (`*`) und mehrere durch Semikolons (`;`) getrennte Hosts ohne Leerzeichen. Geben Sie beispielsweise `127.0.0.1;web.contoso.com;*.microsoft.com` ein.

  - **Automatische Proxy-Konfiguration:** Geben Sie die **PAC-URL** in einem Proxyautokonfigurationsskript. Geben Sie beispielsweise `https://proxy.contoso.com/proxy.pac` ein.

    Weitere Informationen zu PAC-Dateien finden Sie unter [Proxy Auto-Configuration (PAC) file (Datei für die automatische Proxykonfiguration)](https://developer.mozilla.org/docs/Web/HTTP/Proxy_servers_and_tunneling/Proxy_Auto-Configuration_(PAC)_file) (öffnet eine Drittanbieterwebsite).

  Weitere Informationen zu diesem Feature finden Sie auf der Android-Website zu [setRecommendedGlobalProxy](https://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#setRecommendedGlobalProxy(android.content.ComponentName,%20android.net.ProxyInfo)).

## <a name="work-profile-only"></a>Nur Arbeitsprofil

Diese Einstellung gelten für Android Enterprise-Registrierungstypen, bei denen nur das Arbeitsprofil von Intune verwaltet wird, z. B. die Registrierung für ein Android Enterprise-Arbeitsprofil auf einem privaten oder BYOD-Gerät.

### <a name="work-profile-settings"></a>Arbeitsprofileinstellungen

- **Kopieren und Einfügen zwischen Arbeitsprofilen und persönlichen Profilen:** Wenn **Blockieren** festgelegt wird, werden Kopier- und Einfügevorgänge zwischen Arbeits-Apps und persönlichen Apps verhindert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise erlaubt das Betriebssystem Benutzern standardmäßig das Freigeben von Daten mithilfe von Kopier- und Einfügevorgängen bei Apps im persönlichen Profil.
- **Datenaustausch zwischen Arbeitsprofilen und persönlichen Profilen:** Wählen Sie diese Option aus, damit Apps im Arbeitsprofil Daten mit Apps im persönlichen Profil austauschen können. Sie können z.B. Freigabeaktionen in Anwendungen steuern, wie etwa die Option **Freigeben**. in der Chrome-Browser-App. Diese Einstellung gilt nicht für das Verhalten beim Kopieren/Einfügen der Zwischenablage. Folgende Optionen sind verfügbar:
  - **Gerätestandard:** Das standardmäßige Freigabeverhalten des Geräts variiert je nach Android-Version:
    - Auf Geräten mit Android 6.0 oder höher ist die Freigabe im Arbeitsprofil für das persönliche Profil blockiert. Die Freigabe im persönlichen Profil für das Arbeitsprofil ist zulässig.
    - Auf Geräten mit Android 5.0 und niedriger ist die Freigabe zwischen dem Arbeitsprofil und dem persönlichen Profil in beide Richtungen blockiert.
  - **Apps im Arbeitsprofil können Freigabeanforderungen vom persönlichen Profil verarbeiten:** Dadurch wird das integrierte Android-Feature aktiviert, das die Freigabe vom persönlichen Profil zum Arbeitsprofil erlaubt. Wenn diese Option aktiviert ist, können Daten durch eine Freigabeanfrage einer App im persönlichen Profil für Apps im Arbeitsprofil freigegeben werden. Diese Einstellung ist das Standardverhalten für Android-Geräte, die frühere Versionen als 6.0 ausführen.
  - **Keine Einschränkungen bei Freigabe:** Ermöglicht die Freigabe von Daten in beide Richtungen über die Begrenzung des Arbeitsprofils hinaus. Wenn Sie diese Einstellung auswählen, können Apps im Arbeitsprofil Daten für Apps ohne Badgeverwendung im persönlichen Profil freigeben. Diese Einstellung gestattet es verwalteten Apps im Arbeitsprofil, die Daten für Apps auf der nicht verwalteten Seite des Geräts freizugeben. Verwenden Sie diese Einstellung also mit Bedacht.

- **Arbeitsprofilbenachrichtigungen bei Gerätesperre:** Wenn **Blockieren** festgelegt wird, werden Fensterbenachrichtigungen verhindert, sodass Popups, eingehende Anrufe, ausgehende Anrufe, Systemwarnungen und Systemfehler auf gesperrten Geräten nicht angezeigt werden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Das Betriebssystem zeigt Benachrichtigungen möglicherweise standardmäßig an.
- **Standardmäßige App-Berechtigungen:** Legt die Standardberechtigungsrichtlinie für alle Apps im Arbeitsprofil fest. Ab Android 6 werden Benutzer aufgefordert, bestimmte von den Apps benötigte Berechtigungen zu erteilen, wenn die App gestartet wird. Bei dieser Richtlinieneinstellung können Sie festlegen, ob Benutzer aufgefordert werden sollen, Berechtigungen für alle Apps im Arbeitsprofil zu gewähren. Beispielsweise können Sie dem Arbeitsprofil eine App zuweisen, die Standortzugriff benötigt. In der Regel fordert diese App Benutzer dazu auf, den Standortzugriff durch die App zu genehmigen oder abzulehnen. Verwenden Sie diese Richtlinie, um Berechtigungen automatisch ohne Aufforderung zu erteilen, Berechtigungen ohne Aufforderung automatisch zu verweigern oder die Benutzer entscheiden zu lassen. Folgende Optionen sind verfügbar:
  - **Gerätestandard**
  - **Eingabeaufforderung**
  - **Automatisch gewähren**
  - **Automatisch verweigern**

  Sie können auch eine App-Konfigurationsrichtlinie verwenden, um Berechtigungen für einzelne Anwendungen zu erteilen (**Client-Apps** > **App-Konfigurationsrichtlinien**).

- **Konten hinzufügen und entfernen:** Wenn **Blockieren** festgelegt wird, können Benutzer Konten nicht manuell im Arbeitsprofil hinzufügen oder entfernen. Wenn Sie beispielsweise die Gmail-App in einem Android-Arbeitsprofil bereitstellen, können Sie verhindern, dass Benutzer Konten in diesem Arbeitsprofil hinzufügen oder entfernen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise erlaubt das Betriebssystem das Hinzufügen von Konten im Arbeitsprofil standardmäßig.  

  > [!NOTE]
  > Google-Konten können keinem Arbeitsprofil hinzugefügt werden.

- **Kontaktfreigabe über Bluetooth:** Wenn **Aktivieren** festgelegt wird, wird das Freigeben und Zugreifen auf Arbeitsprofilkontakte über ein anderes Gerät erlaubt, einschließlich Autos, die per Bluetooth gekoppelt werden. Wenn Sie diese Einstellung aktivieren, können bestimmte Bluetooth-Geräte bei der ersten Verbindung Arbeitskontakte zwischenspeichern. Durch das Deaktivieren dieser Richtlinie nach einer ersten Kopplung bzw. Synchronisierung werden die Arbeitskontakte von einem Bluetooth-Gerät möglicherweise nicht entfernt.

  Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise gibt das Betriebssystem Arbeitskontakte standardmäßig nicht frei.

  Diese Einstellung gilt für:

  - Android-Arbeitsprofilgeräte mit Android 6.0 und höher

- **Bildschirmaufnahme:** Wenn **Blockieren** festgelegt wird, werden Screenshots oder Bildschirmaufnahmen auf dem Gerät im Arbeitsprofil verhindert. Zudem wird verhindert, dass der Inhalt auf Anzeigegeräten angezeigt wird, die über keine sichere Videoausgabe verfügen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise erlaubt das Betriebssystem das Aufnehmen von Screenshots standardmäßig.

- **Anrufer-ID des Geschäftskontakts im persönlichen Profil anzeigen:** Wenn **Blockieren** festgelegt wird, wird die Anrufnummer von Arbeitskontakten im persönlichen Profil nicht angezeigt. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise zeigt das Betriebssystem die Anruferkontaktinformationen standardmäßig an.

  Diese Einstellung gilt für:

  - Android 6.0 und höher

- **Geschäftskontakte vom persönlichen Profil aus suchen:** Wenn **Blockieren** festgelegt wird, werden Benutzer daran gehindert, im persönlichen Profil in Apps nach Arbeitskontakten zu suchen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise erlaubt das Betriebssystem die Suche nach Arbeitskontakten im persönlichen Profil standardmäßig.

- **Kamera:** Wenn **Blockieren** festgelegt wird, wird der Zugriff auf die Kamera des Geräts im Arbeitsprofil verhindert. Die Kamera im persönlichen Profil ist von dieser Einstellung nicht betroffen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise den Zugriff auf die Kamera zu.

- **Widgets aus Arbeitsprofil-Apps zulassen:** Wenn **Aktivieren** festgelegt wird, können Benutzer von Apps zur Verfügung gestellte Widgets auf dem Startbildschirm platzieren. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem diese Funktion deaktivieren.

  Angenommen, Outlook ist für das Arbeitsprofil Ihrer Benutzer installiert. Wenn diese Einstellung auf **Aktivieren** festgelegt ist, können Benutzer das Agenda-Widget auf dem Startbildschirm des Geräts platzieren.

- **Arbeitsprofilkennwort erforderlich:** Wenn **Erforderlich** festgelegt wird, wird eine Passcode-Richtlinie erzwungen, die nur für Apps im Arbeitsprofil gilt. Benutzer können die zwei separat definierten PINs standardmäßig verwenden. Alternativ können Benutzer die PINs in die sicherere PIN kombinieren. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise erlaubt das Betriebssystem Benutzern standardmäßig die Verwendung von Arbeits-Apps, ohne die Eingabe eines Passcodes zu erfordern.

  Diese Einstellung gilt für:

  - Android 7.0 und höher mit aktiviertem Arbeitsprofil

  Konfigurieren Sie auch Folgendes:

  - **Minimale Kennwortlänge:** Geben Sie die Mindestlänge des Kennworts ein (4 bis 16 Zeichen).
  - **Maximaler Zeitraum der Inaktivität (in Minuten) bis zur Sperrung des Arbeitsprofils:** Geben Sie den Zeitraum an, für den sich ein Gerät im Leerlauf befinden muss, bevor der Bildschirm automatisch gesperrt wird. Benutzer müssen ihre Anmeldeinformationen eingeben, um wieder Zugriff zu erhalten. Geben Sie zum Beispiel `5` ein, um Geräte nach 5 Minuten im Leerlauf zu sperren. Wenn kein Wert angegeben oder **Nicht konfiguriert** festgelegt ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.

    Benutzer können keinen Zeitwert auf Geräten festlegen, der über dem im Profil konfigurierten Zeitwert liegt. Benutzer können einen niedrigeren Zeitwert festlegen. Wenn das Profil beispielsweise auf `15` Minuten festgelegt wird, können Benutzer einen Wert von 5 Minuten festlegen. Benutzer können den Wert jedoch nicht auf 30 Minuten festlegen.

  - **Anzahl von fehlgeschlagenen Anmeldungen, bevor das Gerät zurückgesetzt wird:** Geben Sie mit einem Wert zwischen 4 und 11 an, wie häufig ein falsches Kennwort eingegeben werden kann, bevor das Arbeitsprofil auf dem Gerät zurückgesetzt wird. Wenn `0` (null) festgelegt wird, wird möglicherweise die Funktion zum Zurücksetzen des Geräts deaktiviert. Wenn kein Wert angegeben ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.

  - **Kennwortablauf (Tage):** Geben Sie die Anzahl der Tage (von **1**-**365**) ein, nach der Benutzerkennwörter geändert werden müssen.
  - **Erforderlicher Kennworttyp:** Geben Sie den erforderlichen Grad der Kennwortkomplexität ein, und bestimmen Sie, ob biometrische Geräte zulässig sind. Folgende Optionen sind verfügbar:
    - **Gerätestandard**
    - **Biometrie auf niedriger Sicherheitsstufe:** [Vergleich von stark und schwach biometrisch](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (öffnet Android-Website)
    - **Erforderlich**
    - **Mindestens numerisch:** Bei dieser Einstellung sind numerische Zeichen wie `123456789` enthalten.
    - **Numerisch, komplex:** Bei dieser Einstellung sind wiederholte oder fortlaufende Zahlen wie `1111` oder `1234` nicht zulässig.
    - **Mindestens alphabetisch**: Bei dieser Einstellung sind Buchstaben des Alphabets enthalten. Zahlen und Symbole sind nicht erforderlich.
    - **Mindestens alphanumerisch**: Schließt Großbuchstaben, Kleinbuchstaben und Ziffern ein.
    - **Mindestens alphanumerisch mit Symbolen**: Schließt Großbuchstaben, Kleinbuchstaben, Ziffern, Interpunktionszeichen und Symbole ein.

  - **Wiederverwendung vorheriger Kennwörter verhindern:** Verwenden Sie diese Einstellung, um zu verhindern, dass Benutzer zuvor verwendete Kennwörter erstellen. Geben Sie die Anzahl der zuvor verwendeten Kennwörter ein, die nicht erneut verwendet werden können, von 1–24. Geben Sie z.B. `5` an, damit ein Benutzer sein neues Kennwort nicht auf sein aktuelles Kennwort oder eines seiner vorherigen vier Kennwörter festlegen kann. Wenn kein Wert angegeben ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.
  - **Entsperrung per Gesichtserkennung**: **Blockieren** verhindert, dass Benutzer die Gesichtserkennung des Geräts zum Entsperren des Arbeitsprofils verwenden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise zu, dass Benutzer das Gerät per Gesichtserkennung entsperren.
  - **Entsperrung durch Fingerabdruck:** **Blockieren** verhindert, dass Benutzer den Fingerabdruckscanner des Geräts zum Entsperren des Arbeitsprofils verwenden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise zu, dass Benutzer das Gerät per Fingerabdruck entsperren.
  - **Entsperrung per Iriserkennung**: **Blockieren** verhindert, dass Benutzer den Irisscanner des Geräts zum Entsperren des Arbeitsprofils verwenden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise zu, dass Benutzer das Gerät mit dem Irisscanner entsperren.
  - **Smart Lock und andere Vertrauens-Agents:** Wenn **Blockieren** festgelegt wird, werden Smart Lock und andere Vertrauens-Agents daran gehindert, die Sperrbildschirmeinstellungen auf kompatiblen Geräten anzupassen. Dieses Feature wird auch als Vertrauens-Agent bezeichnet und ermöglicht es Ihnen, das Kennwort für den Gerätesperrbildschirm zu deaktivieren oder zu umgehen, wenn sich das Gerät an einem vertrauenswürdigen Standort befindet. Beispielsweise können Sie das Arbeitsprofilkennwort umgehen, wenn Geräte mit einem bestimmten Bluetooth-Gerät verbunden sind oder sich in der Nähe eines NFC-Tags befinden. Mit dieser Einstellung können Sie verhindern, dass Benutzer Smart Lock konfigurieren.

    Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

### <a name="password"></a>Kennwort

Diese Kennworteinstellungen gelten für persönliche Profile auf Geräten, die ein Arbeitsprofil verwenden.

- **Minimale Kennwortlänge:** Geben Sie die Mindestlänge des Kennworts ein (4 bis 16 Zeichen).
- **Maximaler Zeitraum der Inaktivität (in Minuten) bis zur Bildschirmsperrung:** Geben Sie den Zeitraum an, für den sich ein Gerät im Leerlauf befinden muss, bevor der Bildschirm automatisch gesperrt wird. Benutzer müssen ihre Anmeldeinformationen eingeben, um wieder Zugriff zu erhalten. Geben Sie zum Beispiel `5` ein, um Geräte nach 5 Minuten im Leerlauf zu sperren. Wenn kein Wert angegeben oder **Nicht konfiguriert** festgelegt ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.

  Benutzer können keinen Zeitwert auf Geräten festlegen, der über dem im Profil konfigurierten Zeitwert liegt. Benutzer können einen niedrigeren Zeitwert festlegen. Wenn das Profil beispielsweise auf `15` Minuten festgelegt wird, können Benutzer einen Wert von 5 Minuten festlegen. Benutzer können den Wert jedoch nicht auf 30 Minuten festlegen.

- **Anzahl von fehlgeschlagenen Anmeldungen, bevor das Gerät zurückgesetzt wird:** Geben Sie mit einem Wert zwischen 4 und 11 an, wie häufig ein falsches Kennwort eingegeben werden kann, bevor das Arbeitsprofil auf dem Gerät zurückgesetzt wird. Wenn `0` (null) festgelegt wird, wird möglicherweise die Funktion zum Zurücksetzen des Geräts deaktiviert. Wenn kein Wert angegeben ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.
- **Kennwortablauf (Tage):** Geben Sie die Anzahl der Tage ein, bis das Gerätekennwort geändert werden muss (von 1 bis 365). Geben Sie beispielsweise `90` an, damit das Kennwort nach 90 Tagen abläuft. Wenn das Kennwort abläuft, werden Benutzer aufgefordert, ein neues Kennwort zu erstellen. Wenn kein Wert angegeben ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.
- **Erforderlicher Kennworttyp:** Geben Sie den erforderlichen Grad der Kennwortkomplexität ein, und bestimmen Sie, ob biometrische Geräte zulässig sind. Folgende Optionen sind verfügbar:
  - **Gerätestandard**
  - **Biometrie auf niedriger Sicherheitsstufe:** [Vergleich von stark und schwach biometrisch](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (öffnet Android-Website)
  - **Erforderlich**
  - **Mindestens numerisch:** Bei dieser Einstellung sind numerische Zeichen wie `123456789` enthalten.
  - **Numerisch, komplex:** Bei dieser Einstellung sind wiederholte oder fortlaufende Zahlen wie `1111` oder `1234` nicht zulässig.
  - **Mindestens alphabetisch**: Bei dieser Einstellung sind Buchstaben des Alphabets enthalten. Zahlen und Symbole sind nicht erforderlich.
  - **Mindestens alphanumerisch**: Schließt Großbuchstaben, Kleinbuchstaben und Ziffern ein.
  - **Mindestens alphanumerisch mit Symbolen**: Schließt Großbuchstaben, Kleinbuchstaben, Ziffern, Interpunktionszeichen und Symbole ein.

- **Wiederverwendung vorheriger Kennwörter verhindern:** Verwenden Sie diese Einstellung, um zu verhindern, dass Benutzer zuvor verwendete Kennwörter erstellen. Geben Sie die Anzahl der zuvor verwendeten Kennwörter ein, die nicht erneut verwendet werden können, von 1–24. Geben Sie z.B. `5` an, damit ein Benutzer sein neues Kennwort nicht auf sein aktuelles Kennwort oder eines seiner vorherigen vier Kennwörter festlegen kann. Wenn kein Wert angegeben ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.
- **Entsperrung durch Fingerabdruck:** **Blockieren** verhindert, dass Benutzer den Fingerabdruckscanner des Geräts zum Entsperren des Geräts verwenden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise zu, dass Benutzer das Gerät per Fingerabdruck entsperren.
- **Entsperrung per Gesichtserkennung**: **Blockieren** verhindert, dass Benutzer die Gesichtserkennung des Geräts zum Entsperren des Geräts verwenden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise zu, dass Benutzer das Gerät per Gesichtserkennung entsperren.
- **Entsperrung per Iriserkennung**: **Blockieren** verhindert, dass Benutzer den Irisscanner des Geräts zum Entsperren des Geräts verwenden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise zu, dass Benutzer das Gerät mit dem Irisscanner entsperren.
- **Smart Lock und andere Vertrauens-Agents:** Wenn **Blockieren** festgelegt wird, werden Smart Lock und andere Vertrauens-Agents daran gehindert, die Sperrbildschirmeinstellungen auf kompatiblen Geräten anzupassen. Dieses Feature wird auch als Vertrauens-Agent bezeichnet und ermöglicht es Ihnen, das Kennwort für den Gerätesperrbildschirm zu deaktivieren oder zu umgehen, wenn sich das Gerät an einem vertrauenswürdigen Standort befindet. Beispielsweise können Sie das Arbeitsprofilkennwort umgehen, wenn Geräte mit einem bestimmten Bluetooth-Gerät verbunden sind oder sich in der Nähe eines NFC-Tags befinden. Mit dieser Einstellung können Sie verhindern, dass Benutzer Smart Lock konfigurieren.

  Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

### <a name="system-security"></a>Systemsicherheit

- **Bedrohungsüberprüfung für Apps:** Die Option **Anfordern** erzwingt, dass die Einstellung **Apps überprüfen** für Arbeitsprofile und persönliche Profile aktiviert ist. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

  Diese Einstellung gilt für:

  - Android 8 (Oreo) und höher

- **App-Installationen aus unbekannten Quellen im persönlichen Profil verhindern:** Entwurfsbedingt können auf Android Enterprise-Geräten mit Arbeitsprofil keine Apps aus Quellen außerhalb des Play Store installiert werden. Diese Einstellung ermöglicht Administratoren eine bessere Kontrolle über App-Installationen aus unbekannten Quellen. Wenn **Blockieren** festgelegt wird, werden App-Installationen im persönlichen Profil aus anderen Quellen als dem Google Play Store verhindert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem App-Installationen im persönlichen Profil möglicherweise nicht aus unbekannten Quellen zu. Geräte mit Arbeitsprofil sind auf zwei Profile ausgelegt:

  - Ein MDM-verwaltetes Arbeitsprofil
  - Ein privates, von der MDM-Verwaltung unabhängiges Profil

### <a name="connectivity"></a>Verbindung

- **Always On-VPN:** **Aktivieren** legt einen VPN-Client so fest, dass er automatisch eine Verbindung mit dem VPN herstellt und erneut herstellt. Always On-VPN-Verbindungen bleiben aktiv. Alternativ wird die Verbindung sofort wiederhergestellt, wenn der Benutzer sein Gerät sperrt, das Gerät neu gestartet wird oder das Drahtlosnetzwerk geändert wird.

  Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig deaktiviert das Betriebssystem Always On-VPN möglicherweise für alle VPN-Clients.

  > [!IMPORTANT]
  > Stellen Sie sicher, dass Sie nur eine Always On-VPN-Richtlinie auf einem einzelnen Gerät bereitstellen. Die Bereitstellung mehrerer Always VPN-Richtlinien auf einem einzelnen Gerät wird nicht unterstützt.

- **VPN-Client:** Wählen Sie einen VPN-Client aus, der Always On unterstützt. Folgende Optionen sind verfügbar:
  - Cisco AnyConnect
  - F5 Access
  - Palo Alto Networks GlobalProtect
  - Pulse Secure
  - Benutzerdefiniert
    - **Paket-ID:** Geben Sie die Paket-ID der App im Google Play Store ein. Wenn z. B. die URL für die App im Play Store `https://play.google.com/store/details?id=com.contosovpn.android.prod` lautet, dann ist die Paket-ID `com.contosovpn.android.prod`.

  > [!IMPORTANT]
  > - Der von Ihnen ausgewählte VPN-Client muss auf dem Gerät installiert sein und VPN pro Anwendung in Arbeitsprofilen unterstützen. Andernfalls tritt ein Fehler auf.
  > - Sie müssen die VPN-Client-App im **verwalteten Google Play Store** genehmigen, die App mit Intune synchronisieren und die App auf dem Gerät bereitstellen. Danach wird die App im Arbeitsprofil des Benutzers installiert.
  > - Es gibt eventuell bekannte Probleme bei der Verwendung von VPN pro App mit F5 Access for Android 3.0.4. Weitere Informationen finden Sie unter [F5's release notes for F5 Access for Android 3.0.4 (Versionshinweise zu F5 Access for Android 3.0.4)](https://support.f5.com/kb/en-us/products/big-ip_apm/releasenotes/related/relnote-f5access-android-3-0-4.html#relnotes_known_issues_f5_access_android).

- **Sperrmodus:** Wenn **Aktivieren** festgelegt wird, wird jeglicher Netzwerkdatenverkehr durch den VPN-Tunnel erzwungen. Wenn keine Verbindung zum VPN hergestellt wird, hat das Gerät keinen Netzwerkzugriff.

  Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem den Datenverkehr durch den VPN-Tunnel oder über das Mobilfunknetz standardmäßig zu.

## <a name="next-steps"></a>Nächste Schritte

[Zuweisen von Profilen](device-profile-assign.md) und [Überwachen von Profilen](device-profile-monitor.md)

Außerdem können Sie Kioskprofile auf dedizierten Geräten für [Android](device-restrictions-android.md#kiosk)- und [Windows 10](kiosk-settings.md)-Geräte erstellen.

[Konfigurieren und Behandeln von Problemen bei Android Enterprise-Geräten in Microsoft Intune](https://support.microsoft.com/help/4476974)
