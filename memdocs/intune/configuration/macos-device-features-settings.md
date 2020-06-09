---
title: macOS-Gerätefunktionseinstellungen in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Sehen Sie sich die Einstellungen zur Konfiguration von macOS-Geräten für AirPrint an, und passen Sie das Anmeldefenster so an, dass die Ein-/Ausschaltflächen in Microsoft Intune ein- oder ausgeblendet werden. Beachten Sie die Schritte zum Abrufen der IP-Adresse, des Pfad und der Porteinstellungen eines AirPrint-Servers in Ihrem Netzwerk. Verwenden Sie diese Einstellungen in einem Gerätekonfigurationsprofil, um macOS-Gerätefunktionen zu konfigurieren.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/05/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: kakyker; annovich
ms.suite: ems
search.appverid: ''
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9d4bc2de9e16cfcf9322cf343badafe3c9a35c70
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428897"
---
# <a name="macos-device-feature-settings-in-intune"></a>macOS-Gerätefunktionseinstellungen in Intune

Intune bietet integrierte Einstellungen zum Anpassen von Features auf Ihren macOS-Geräten. Administratoren können beispielsweise AirPrint-Drucker hinzufügen, die Art der Benutzeranmeldung auswählen, die Energiesteuerung konfigurieren, die SSO-Authentifizierung verwenden und mehr.

Nutzen Sie diese Features, um macOS-Geräte im Rahmen Ihrer MDM-Lösung (Mobile Device Management, Verwaltung mobiler Geräte) zu verwalten.

In diesem Artikel werden diese Einstellungen mit ihren Funktionsbeschreibungen aufgeführt. Außerdem werden die Schritte zum Abrufen von IP-Adresse, Pfad und Port von AirPrint-Druckern, die die Terminal-App (Emulator) nutzen, aufgeführt. Weitere Informationen zu Gerätefeatures finden Sie unter [Hinzufügen von Einstellungen für iOS/iPadOS- oder macOS-Gerätefunktionen in Intune](device-features-configure.md).

> [!NOTE]
> Die Benutzeroberfläche stimmt möglicherweise nicht mit den Registrierungstypen in diesem Artikel überein. Die Informationen in diesem Artikel sind richtig. Die Benutzeroberfläche wird in einem zukünftigen Release aktualisiert.

## <a name="before-you-begin"></a>Vorbereitung

[Erstellen Sie ein macOS-Gerätefeatureprofil.](device-features-configure.md)

> [!NOTE]
> Diese Einstellungen gelten für verschiedene Registrierungstypen, wobei einige Einstellungen für alle Registrierungsoptionen gelten. Weitere Informationen zu den verschiedenen Registrierungstypen finden Sie unter [macOS-Registrierung](../enrollment/macos-enroll.md).

## <a name="airprint"></a>AirPrint

### <a name="settings-apply-to-all-enrollment-types"></a>Die Einstellungen gelten für: Alle Registrierungstypen

- **AirPrint-Ziele**: **Fügen Sie mindestens einen AirPrint-Drucker hinzu**, damit Benutzer von ihren Geräten drucken können. Geben Sie außerdem Folgendes ein:
  - **Port** (iOS 11.0+, iPadOS 13.0+): Geben Sie den Lauschport des AirPrint-Ziels ein. Wenn Sie diese Eigenschaft leer lassen, verwendet AirPrint den Standardport.
  - **IP-Adresse**: Geben Sie die IPv4- oder IPv6-Adresse des Druckers ein. Geben Sie beispielsweise `10.0.0.1` ein. Wenn Sie den Hostnamen verwenden, um Drucker zu identifizieren, erhalten Sie die IP-Adresse, indem Sie den Drucker in der Terminal-App pingen. Der Abschnitt zum [Abrufen von IP-Adresse und Pfad](#get-the-ip-address-and-path) (in diesem Artikel) enthält weitere Details dazu.
  - **Pfad:** Geben Sie den Ressourcenpfad des Druckers ein. Der Pfad ist für Drucker in Ihrem Netzwerk in der Regel `ipp/print`. Der Abschnitt zum [Abrufen von IP-Adresse und Pfad](#get-the-ip-address-and-path) (in diesem Artikel) enthält weitere Details dazu.
  - **TLS** (iOS 11.0+, iPadOS 13.0+): Folgende Optionen sind verfügbar:
    - **Nein** (Standard): Transport Layer Security (TLS) wird beim Herstellen einer Verbindung mit AirPrint-Druckern nicht erzwungen.
    - **Ja**: Sichert AirPrint-Verbindungen mit Transport Layer Security (TLS).

- **Importieren** Sie eine durch Trennzeichen getrennte Datei (CSV-Datei), die eine Liste der AirPrint-Drucker enthält. Nachdem Sie AirPrint-Drucker in Intune hinzugefügt haben, können Sie diese Liste **Exportieren**.

### <a name="get-the-ip-address-and-path"></a>Abrufen von IP-Adresse und Pfad

Um AirPrinter-Server hinzuzufügen, benötigen Sie die IP-Adresse des Druckers, den Ressourcenpfad und den Port. Die folgenden Schritte zeigen Ihnen, wie Sie diese Informationen abrufen.

1. Öffnen Sie das **Terminal** auf einem Mac, der mit demselben lokalen Netzwerk (Subnetz) verbunden ist wie die AirPrint-Drucker (über **/Programme/Dienstprogramme**).
2. Geben Sie in der Terminal-App `ippfind` ein, und wählen Sie „Eingabe“ aus.

    Beachten Sie die Druckerinformationen. Es könnte z.B. `ipp://myprinter.local.:631/ipp/port1` zurückgegeben werden. Der erste Teil ist der Name des Druckers. Der letzte Teil (`ipp/port1`) ist der Pfad der Ressource.

3. Geben Sie im Terminal `ping myprinter.local` ein, und wählen Sie „Eingabe“ aus.

   Beachten Sie die IP-Adresse. Es könnte z.B. `PING myprinter.local (10.50.25.21)` zurückgegeben werden.

4. Verwenden Sie die Werte von IP-Adresse und Ressourcenpfad. In diesem Beispiel ist die IP-Adresse `10.50.25.21` und der Ressourcenpfad `/ipp/port1`.

## <a name="associated-domains"></a>Zugeordnete Domänen

In Intune können Sie folgende Aktionen ausführen:

- Hinzufügen von mehreren Zuordnungen zwischen Apps und Domänen
- Zuordnen von mehreren Domänen zur selben App

Diese Funktion gilt für:

- macOS 10.15 und neuer

### <a name="settings-apply-to-user-approved-device-enrollment-and-automated-device-enrollment"></a>Die Einstellungen gelten für: Vom Benutzer genehmigte Geräteregistrierung und automatisierte Geräteregistrierung

- **Zugeordnete Domänen**: **Fügen** Sie eine Zuordnung zwischen Ihrer Domäne und einer App hinzu. Diese Funktion gibt Anmeldeinformationen zwischen einer Contoso-App und einer Contoso-Website frei. Geben Sie außerdem Folgendes ein:

  - **App-ID**: Geben Sie den App-Bezeichner der App ein, die einer Website zugeordnet werden soll. Der App-Bezeichner enthält die Team-ID und eine Bundle-ID: `TeamID.BundleID`.

    Die Team-ID ist eine aus 10 Zeichen bestehende alphanumerische (Ziffern und Buchstaben) Zeichenfolge, die von Apple für Ihre App-Entwickler generiert wird, z. B. `ABCDE12345`. Auf der [Seite zur Team-ID-Ermittlung](https://help.apple.com/developer-account/#/dev55c3c710c)  (öffnet die Website von Apple) finden Sie weitere Informationen.

    Die Bundle-ID identifiziert die App eindeutig und ist üblicherweise in umgekehrter Domänennamennotation formatiert. Beispielsweise lautet die Bundle-ID des Finders `com.apple.finder`. Um die Bundle-ID zu finden, verwenden Sie das AppleScript-Skript im Terminal:

    `osascript -e 'id of app "ExampleApp"'`

  - **Domäne:** Geben Sie die Websitedomäne ein, die einer App zugeordnet werden soll. Die Domäne enthält einen Diensttyp und einen vollqualifizierten Hostnamen, beispielsweise `webcredentials:www.contoso.com`.

    Sie können alle Unterdomänen einer zugeordneten Domäne einschließen, indem Sie vor dem Domänennamen `*.` (Sternchen-Platzhalter und Punkt) eingeben. Der Punkt ist erforderlich. Exakte Domänen haben eine höhere Priorität als Platzhalterdomänen. Daher werden Muster aus übergeordneten Domänen abgeglichen, *wenn* in der vollqualifizierten Unterdomäne keine Übereinstimmung gefunden wird.

    Der Diensttyp kann wie folgt lauten:

    - **authsrv**: App-Erweiterung für einmaliges Anmelden
    - **applink:** universeller Link
    - **webcredentials:** AutoAusfüllen für Kennwörter

> [!TIP]
> Wechseln Sie zur Problembehandlung auf Ihrem macOS-Gerät zu **Systemeinstellungen** > **Profile**. Vergewissern Sie sich, dass das erstellte Profil in der Liste der Geräteprofile aufgeführt ist. Wenn das Profil aufgelistet wird, stellen Sie sicher, dass **Konfiguration der zugeordneten Domänen** im Profil enthalten ist und die richtige App-ID und die richtigen Domänen aufweist.

## <a name="login-items"></a>Anmeldeelemente

### <a name="settings-apply-to-all-enrollment-types"></a>Die Einstellungen gelten für: Alle Registrierungstypen

- **Fügen Sie die Dateien, Ordner und benutzerdefinierten Apps hinzu, die bei der Anmeldung gestartet werden sollen**: **Fügen Sie den Pfad zu einer Datei, einem Ordner, einer benutzerdefinierten App oder einer System-App hinzu**, die geöffnet werden soll, wenn sich ein Benutzer auf dem Gerät anmeldet. Geben Sie außerdem Folgendes ein:

  - **Pfad des Elements**: Geben Sie den Pfad zur Datei, zum Ordner oder zur App ein. System-Apps oder Apps, die für Ihre Organisation entwickelt oder angepasst wurden, befinden sich üblicherweise im Ordner `Applications` und weisen einen Pfad ähnlich wie `/Applications/AppName.app` auf.

    Sie können zahlreiche Dateien, Ordner und Apps hinzufügen. Geben Sie beispielsweise Folgendes ein:  
  
    - `/Applications/Calculator.app`
    - `/Applications`
    - `/Applications/Microsoft Office/root/Office16/winword.exe`
    - `/Users/UserName/music/itunes.app`
  
    Wenn Sie eine App, einen Ordner oder eine Datei hinzufügen, stellen Sie sicher, dass Sie den richtigen Pfad eingeben. Nicht alle Elemente befinden sich im Ordner `Applications`. Wenn ein Benutzer ein Element von einem Speicherort an einen anderen verschiebt, ändert sich der Pfad. Dieses verschobene Element wird nicht geöffnet, wenn sich der Benutzer anmeldet.

  - **Ausblenden:** Sie können die App einblenden oder ausblenden. Folgende Optionen sind verfügbar:
    - **Nicht konfiguriert:** Dies ist der Standardwert. Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Standardmäßig zeigt das Betriebssystem Elemente in der Liste der Anmeldeelemente für Benutzer und Gruppen an, wenn die Option „Ausblenden“ deaktiviert wird.
    - **Ja**: Die App wird nicht in der Liste der Anmeldeelemente für Benutzer und Gruppen angezeigt.

## <a name="login-window"></a>Fenster „Anmeldung“

### <a name="settings-apply-to-all-enrollment-types"></a>Die Einstellungen gelten für: Alle Registrierungstypen

- **Zusätzliche Informationen in der Menüleiste anzeigen**: Wenn der Zeitbereich auf der Menüleiste ausgewählt ist, zeigt **Ja** den Hostnamen und die macOS-Version an. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig zeigt das Betriebssystem diese Informationen möglicherweise nicht in der Menüleiste an.
- **Banner**: Geben Sie eine Meldung ein, die auf dem Anmeldebildschirm des Geräts angezeigt wird. Geben Sie beispielsweise Ihre Unternehmensinformationen, eine Begrüßungsmeldung, Informationen bei Verlust eines Geräts usw. ein.
- **Textfelder für Benutzernamen und Kennwort sind erforderlich**: Wählen Sie aus, wie Benutzer sich beim Gerät anmelden können. **Ja** erfordert, dass Benutzer einen Benutzernamen und ein Kennwort eingeben. Wenn die Einstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert. Standardmäßig verlangt das Betriebssystem möglicherweise, dass Benutzer Ihren Benutzernamen aus einer Liste auswählen und dann ihr Kennwort eingeben.

  Geben Sie außerdem Folgendes ein:

  - **Lokale Benutzer ausblenden**: **Ja** zeigt die lokalen Benutzerkonten nicht in der Benutzerliste an, wozu auch Standard- und Administratorkonten gehören können. Nur die Netzwerk- und Systembenutzerkonten werden gezeigt. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig zeigt das Betriebssystem möglicherweise die lokalen Benutzerkonten in der Benutzerliste an.
  - **Mobile Konten ausblenden**: **Ja** zeigt mobile Konten nicht in der Benutzerliste an. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig zeigt das Betriebssystem möglicherweise die mobilen Konten in der Benutzerliste an. Einige mobile Konten werden möglicherweise als Netzwerkbenutzer angezeigt.
  - **Netzwerkbenutzer anzeigen**: Wählen Sie **Ja** aus, um die Netzwerkbenutzer in der Benutzerliste aufzulisten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig zeigt das Betriebssystem möglicherweise die Netzwerkbenutzerkonten nicht in der Benutzerliste an.
  - **Administratoren des Computers ausblenden**: **Ja** zeigt Administratorbenutzerkonten nicht in der Benutzerliste an. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig zeigt das Betriebssystem möglicherweise die Administratorbenutzerkonten in der Benutzerliste an.
  - **Andere Benutzer anzeigen**: Wählen Sie **Ja** aus, um **Weitere...** Benutzer in der Benutzerliste aufzulisten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig zeigt das Betriebssystem möglicherweise die anderen Benutzerkonten nicht in der Benutzerliste an.

- **Schaltfläche "Herunterfahren" ausblenden**: **Ausblenden** zeigt die Schaltfläche „Herunterfahren“ nicht auf dem Anmeldebildschirm an. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig zeigt das Betriebssystem möglicherweise die Schaltfläche „Ausschalten“ an.
- **Schaltfläche „Neustart“ ausblenden**: **Ja** zeigt die Schaltfläche „Neu starten“ nicht auf dem Anmeldebildschirm an. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig zeigt das Betriebssystem möglicherweise die Schaltfläche „Neustart“ an.
- **Schaltfläche „Ruhezustand“ ausblenden**: **Ja** zeigt die Schaltfläche „Standby“ nicht auf dem Anmeldebildschirm an. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig zeigt das Betriebssystem möglicherweise die Schaltfläche „Ruhezustand“ an.
- **Benutzeranmeldung über Konsole deaktivieren**: **Ja** blendet die macOS-Befehlszeile zum Anmelden aus. Für typische Benutzer legen Sie diese Einstellung auf **Ja** fest. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise zu, dass fortgeschrittene Benutzer sich über die macOS-Befehlszeile anmelden. Um in den Konsolenmodus zu wechseln, müssen Benutzer `>console` in das Feld „Benutzername“ eingeben und sich im Konsolenfenster authentifizieren.
- **Herunterfahren bei Anmeldung deaktivieren**: **Ja** verhindert, dass Benutzer die Option **Herunterfahren** auswählen können, nachdem sie sich angemeldet haben. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise zu, dass Benutzer auf dem Gerät auf das Menüelement **Ausschalten** klicken.
- **Neustart bei Anmeldung deaktivieren**: **Ja** verhindert, dass Benutzer die Option **Neu starten** auswählen können, nachdem sie sich angemeldet haben. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise zu, dass Benutzer auf dem Gerät auf das Menüelement **Neustart** klicken.
- **Ausschalten bei Anmeldung deaktivieren**: **Ja** verhindert, dass Benutzer die Option **Ausschalten** auswählen können, nachdem sie sich angemeldet haben. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise zu, dass Benutzer auf dem Gerät auf das Menüelement **Power off** (Abschalten) klicken.
- **Abmelden bei Anmeldung deaktivieren** (macOS 10.13 oder höher): **Ja** verhindert, dass Benutzer die Option **Abmelden** auswählen können, nachdem sie sich angemeldet haben. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise zu, dass Benutzer auf dem Gerät auf das Menüelement **Abmelden** klicken.
- **Sperrbildschirm bei Anmeldung deaktivieren** (macOS 10.13 oder höher): **Ja** verhindert, dass Benutzer die Option **Sperrbildschirm** auswählen können, nachdem sie sich angemeldet haben. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise zu, dass Benutzer auf dem Gerät auf das Menüelement **Lock screen** (Bildschirm sperren) klicken.

## <a name="single-sign-on-app-extension"></a>App-Erweiterung für einmaliges Anmelden

Diese Funktion gilt für:

- macOS 10.15 und neuer

### <a name="settings-apply-to-user-approved-device-enrollment-and-automated-device-enrollment"></a>Die Einstellungen gelten für: Vom Benutzer genehmigte Geräteregistrierung und automatisierte Geräteregistrierung

- **Typ der SSO-App-Erweiterung:** Wählen Sie den Typ der SSO-App-Erweiterung für Anmeldeinformationen aus. Folgende Optionen sind verfügbar:

  - **Nicht konfiguriert:** Es werden keine App-Erweiterungen verwendet. Um eine App-Erweiterung zu deaktivieren, ändern Sie den Typ der SSO-App-Erweiterung in **Nicht konfiguriert**.
  - **Umleiten:** Verwenden Sie eine generische, anpassbare App-Erweiterung für die Umleitung, um das einmalige Anmelden (Single Sign-On, SSO) mit modernen Authentifizierungsflows zu nutzen. Stellen Sie sicher, dass Sie die Erweiterung und die Team-ID für die App-Erweiterung Ihrer Organisation kennen.
  - **Anmeldeinformationen:** Verwenden Sie eine generische, anpassbare App-Erweiterung für Anmeldeinformationen, um das einmalige Anmelden mit Challenge-Response-Authentifizierungsflows zu nutzen. Stellen Sie sicher, dass Sie die Erweiterungs-ID und die Team-ID für die SSO-App-Erweiterung Ihrer Organisation kennen.  
  - **Kerberos**: Verwenden Sie die integrierte Kerberos-Erweiterung von Apple, die in macOS Catalina 10.15 und höher enthalten ist. Bei dieser Option handelt es sich um eine Kerberos-spezifische Version der App-Erweiterung vom Typ **Anmeldeinformationen**.

  > [!TIP]
  > Mit den Typen **Umleitung** und **Anmeldeinformationen** fügen Sie eigene Konfigurationswerte hinzu, die über die Erweiterung übergeben werden. Erwägen Sie bei Auswahl von **Anmeldeinformationen** die Verwendung integrierter Konfigurationseinstellungen, die von Apple für den Typ **Kerberos** bereitgestellt werden.

- **Erweiterungs-ID** („Umleiten“ und „Anmeldeinformationen“): Geben Sie den Bundlebezeichner ein, der Ihre SSO-App-Erweiterung identifiziert, z. B. `com.apple.ssoexample`.
- **Team-ID** („Umleiten“ und „Anmeldeinformationen“): Geben Sie den Teambezeichner Ihrer SSO-App-Erweiterung ein. Eine Team-ID ist eine aus 10 Zeichen bestehende alphanumerische (Ziffern und Buchstaben) Zeichenfolge, die von Apple generiert wird, z. B. `ABCDE12345`. 

  Auf der [Seite zur Team-ID-Ermittlung](https://help.apple.com/developer-account/#/dev55c3c710c) (öffnet die Website von Apple) finden Sie weitere Informationen.

- **Bereich** („Anmeldeinformationen“ und „Kerberos“): Geben Sie den Namen Ihres Authentifizierungsbereichs ein. Der Bereichsname sollte groß geschrieben werden, z. B. `CONTOSO.COM`. In der Regel ist Ihr Bereichsname mit dem DNS-Domänennamen identisch, besteht aber nur aus Großbuchstaben.

- **Domänen** („Anmeldeinformationen“ und „Kerberos“): Geben Sie die Domänen- oder Hostnamen der Websites ein, auf denen eine Authentifizierung über SSO möglich ist. Wenn Ihre Website beispielsweise `mysite.contoso.com` lautet, ist `mysite` der Hostname und `contoso.com` der Domänenname. Wenn Benutzer eine Verbindung mit einer dieser Websites herstellen, verarbeitet die App-Erweiterung die Authentifizierung. Diese Authentifizierung ermöglicht es Benutzern Face ID, Touch ID oder eine PIN/einen Passcode von Apple für die Anmeldung zu verwenden.

  - Alle Domänen in den Intune-Profilen für Ihre SSO-App-Erweiterung müssen eindeutig sein. Sie können eine Domäne nicht mehrfach in einem SSO-App-Erweiterungsprofil verwenden – selbst dann nicht, wenn Sie verschiedene Arten von SSO-App-Erweiterungen verwenden.
  - Für diese Domänen erfolgt keine Beachtung der Groß-/Kleinschreibung.

- **URLs** (nur „Umleiten“): Geben Sie die URL-Präfixe der Identitätsanbieter ein, in deren Auftrag die Umleitungs-App-Erweiterung die SSO-Authentifizierung nutzt. Wenn Benutzer auf diese URLs umgeleitet werden, greift die SSO-App-Erweiterung ein und fordert eine SSO-Authentifizierung an.

  - Alle URLs in Ihren Intune-SSO-Erweiterungsprofilen müssen eindeutig sein. Sie können eine Domäne nicht mehrfach in einem SSO-App-Erweiterungsprofil verwenden – selbst dann nicht, wenn Sie verschiedene Arten von SSO-App-Erweiterungen verwenden.
  - Die URLs müssen mit „http://“ oder „https://“ beginnen.

- **Zusätzliche Konfiguration** („Umleiten“ und „Anmeldeinformationen“): Geben Sie zusätzliche erweiterungsspezifische Daten ein, die an die SSO-App-Erweiterung übergeben werden sollen:
  - **Schlüssel:** Geben Sie den Namen des Elements ein, das Sie hinzufügen möchten, z. B. `user name`.
  - **Typ:** Geben Sie den Datentyp ein. Folgende Optionen sind verfügbar:

    - Zeichenfolge
    - Boolean: Geben Sie unter **Konfigurationswert** entweder `True` oder `False` ein.
    - Integer: Geben Sie unter **Konfigurationswert** eine Zahl ein.

  - **Wert:** Geben Sie die Daten ein.
  
  - **Hinzufügen**: Tippen Sie auf diese Option, um Ihre Konfigurationsschlüssel hinzuzufügen.

- **Verwendung des Schlüsselbunds** (nur „Kerberos“): Wählen Sie **Blockieren** aus, um zu verhindern, dass Kennwörter im Schlüsselbund gespeichert und aufbewahrt werden. Wenn diese Option blockiert ist, werden Benutzer nicht aufgefordert, Ihr Kennwort zu speichern, sondern müssen es noch einmal eingeben, wenn das Kerberos-Ticket abläuft. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise das Speichern von Kennwörtern im Schlüsselbund zu. Benutzer werden nicht aufgefordert, Ihr Kennwort noch einmal einzugeben, wenn das Ticket abgelaufen ist.
- **Face ID, Touch ID, or passcode** (Face ID, Touch ID oder Passcode) (nur „Kerberos“): Bei der Option **Anfordern** werden Benutzer dazu gezwungen, ihre Face-ID, ihre Touch-ID oder ihren Gerätepasscode einzugeben, wenn die Anmeldeinformationen zum Aktualisieren des Kerberos-Tickets benötigt werden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig fordert das Betriebssystem möglicherweise nicht, dass Benutzer sich mit biometrischen Daten oder einem Gerätepasscode authentifizieren, um das Kerberos-Ticket zu aktualisieren. Wenn die Einstellung **Verwendung des Schlüsselbunds** blockiert ist, wird diese Einstellung nicht angewendet.
- **Default realm** (Standardbereich) (nur „Kerberos“): Klicken Sie auf **Aktivieren**, um den von Ihnen unter **Bereich** eingegebenen Wert als Standardbereich festzulegen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig legt das Betriebssystem möglicherweise keinen Standardbereich fest.

  > [!TIP]
  > - **Aktivieren** Sie diese Einstellung, wenn Sie mehrere Kerberos-SSO-App-Erweiterungen in Ihrer Organisation konfigurieren.
  > - **Aktivieren** Sie diese Einstellung, wenn Sie mehrere Bereiche verwenden. Der von Ihnen eingegebene **Bereich** wird als Standardbereich festgelegt.
  > - Wenn Sie nur über einen Bereich verfügen, behalten Sie die Einstellung **Nicht konfiguriert** (Standardeinstellung) bei.

- **AutoErmittlung** (nur „Kerberos“): Wenn diese Option auf **Blockieren** festgelegt ist, verwendet die Kerberos-Erweiterung nicht automatisch LDAP und DNS, um ihren Active Directory-Standortnamen zu ermitteln. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise zu, dass die Erweiterung den Namen des Active Directory-Standorts automatisch ermittelt.
- **Password changes** (Kennwortänderungen) (nur „Kerberos“): Die Option **Blockieren** hindert Benutzer daran, die Kennwörter zu ändern, mit denen sie sich bei den von Ihnen eingegebenen Domänen anmelden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise das Ändern von Kennwörtern zu.  
- **Password sync** (Kennwortsynchronisierung) (nur „Kerberos“): Klicken Sie auf **Aktivieren**, um die lokalen Kennwörter Ihrer Benutzer mit Azure AD zu synchronisieren. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig deaktiviert das Betriebssystem möglicherweise die Kennwortsynchronisierung mit Azure AD. Verwenden Sie diese Einstellung als Alternative oder Backuplösung für das einmalige Anmelden (SSO). Diese Einstellung funktioniert nicht, wenn Benutzer mit einem mobilen Apple-Konto angemeldet sind.
- **Windows Server Active Directory password complexity** (Windows Server Active Directory-Kennwortkomplexität) (nur „Kerberos“): Klicken Sie auf **Anfordern**, um durchzusetzen, dass Benutzer die Anforderungen an die Kennwortkomplexität erfüllen müssen, die Active Directory stellt. Weitere Informationen finden Sie unter [Kennwort muss Komplexitätsvoraussetzungen entsprechen](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements). Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig fordert das Betriebssystem möglicherweise nicht, dass Benutzer die Active Directory-Kennwortanforderungen erfüllen.
- **Mindestkennwortlänge** (nur „Kerberos“): Geben Sie die Mindestanzahl von Zeichen ein, aus denen das Kennwort eines Benutzers bestehen muss. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig erzwingt das Betriebssystem möglicherweise keine Mindestlänge für Benutzerkennwörter.
- **Limit für die Wiederverwendung von Kennwörtern** (nur „Kerberos“): Geben Sie die Anzahl neuer Kennwörter ein (1–24), die verwendet werden müssen, bis ein vorheriges Kennwort für die Domäne wiederverwendet werden kann. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig erzwingt das Betriebssystem möglicherweise kein Limit für die Wiederverwendung von Kennwörtern.
- **Minimum password age** (Mindestkennwortalter) (nur „Kerberos“): Geben Sie die Anzahl von Tagen ein, die ein Kennwort für die Domäne verwendet werden muss, bevor ein Benutzer es ändern kann. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig erzwingt das Betriebssystem möglicherweise kein Mindestkennwortalter, bevor ein Kennwort geändert werden kann.
- **Password expiration notification** (Benachrichtigung über Kennwortablauf) (nur „Kerberos“): Geben Sie an, wie viele Tage vor Ablauf eines Kennworts Benutzer über den bevorstehenden Ablauf ihres Kennworts benachrichtigt werden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig verwendet das Betriebssystem möglicherweise `15` Tage.
- **Kennwortablauf** (nur Kerberos): Geben Sie die Anzahl der Tage an, bis das Gerätekennwort geändert werden muss. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig ist im Betriebssystem möglicherweise eingestellt, dass Kennwörter nie ablaufen.
- **URL für Kennwortänderung** (nur „Kerberos“): Geben Sie die URL ein, die aufgerufen wird, wenn der Benutzer eine Kerberos-Kennwortänderung einleitet.
- **Prinzipalname** (nur „Kerberos“): Geben Sie den Benutzernamen des Kerberos-Prinzipals ein. Sie müssen den Bereichsnamen nicht einschließen. In `user@contoso.com` lautet der Prinzipalname beispielsweise `user`, und `contoso.com` ist der Bereichsname.

  > [!TIP]
  > - Sie können auch Variablen im Prinzipalnamen verwenden, indem Sie geschweifte Klammern `{{ }}` eingeben. Geben Sie z. B. `Username: {{username}}` ein, um den Benutzernamen anzuzeigen. 
  > - Verwenden Sie die Variablenersetzung jedoch mit Bedacht, da die Variablen in der Benutzeroberfläche nicht validiert werden und die Groß- und Kleinschreibung berücksichtigt wird. Stellen Sie sicher, dass die eingegebenen Informationen korrekt sind.
  
- **Active Directory site code** (Active Directory-Standortcode) (nur „Kerberos“): Geben Sie den Namen des Active Directory-Standorts ein, der von der Kerberos-Erweiterung verwendet werden soll. Möglicherweise müssen Sie diesen Wert nicht ändern, weil die Kerberos-Erweiterung den Active Directory-Standortcode ggf. automatisch ermittelt.
- **Cachename** (nur „Kerberos“): Geben Sie den Generic Security Services-Namen (GSS) für den Kerberos-Cache ein. Dieser Wert muss höchstwahrscheinlich nicht festgelegt werden.  
- **Password requirements message** (Meldung zu Kennwortanforderungen) (nur „Kerberos“): Geben Sie eine Textversion der Kennwortanforderungen Ihrer Organisation ein, die den Benutzern angezeigt wird. Die Meldung wird angezeigt, wenn Sie keine Active Directory-Kennwortkomplexitätsanforderungen erzwingen oder keine Mindestkennwortlänge eingeben.  
- **App-Bundle-IDs** (nur „Kerberos“): Mit **Hinzufügen** werden die App-Bundle-IDs hinzugefügt, für die auf Ihren Geräten SSO verwendet werden soll. Diese Apps erhalten Zugriff auf das Kerberos-TGT (Ticket Granting Ticket) sowie das Authentifizierungsticket. Außerdem authentifizieren diese Apps Benutzer für Dienste, für die sie über Zugriffsberechtigungen verfügen.
- **Domänenbereichszuordnung** (nur „Kerberos“): Mit **Hinzufügen** werden die Domänen-DNS-Suffixe hinzugefügt, die Ihrem Bereich zugeordnet werden sollen. Verwenden Sie diese Einstellung, wenn die DNS-Namen der Hosts nicht mit dem Bereichsnamen identisch sind. Wahrscheinlich ist es nicht erforderlich, diese Zuordnung zwischen benutzerdefinierter Domäne und Bereich zu erstellen.
- **PKINIT-Zertifikat** (nur „Kerberos“): Mit **Auswählen** legen Sie das PKINIT-Zertifikat (Public Key Cryptography for Initial Authentication) fest, das für die Kerberos-Authentifizierung verwendet werden kann. Sie können aus [PKCS](../protect/certficates-pfx-configure.md)- oder [SCEP](../protect/certificates-scep-configure.md)-Zertifikaten auswählen, die Sie in Intune hinzugefügt haben. Weitere Informationen zu Zertifikaten finden Sie unter [Verwenden von Zertifikaten zur Authentifizierung in Microsoft Intune](../protect/certificates-configure.md).

## <a name="next-steps"></a>Nächste Schritte

[Zuweisen von Profilen](device-profile-assign.md) und [Überwachen von Profilen](device-profile-monitor.md)

Sie können außerdem Gerätefeatures für [iOS/iPadOS](ios-device-features-settings.md) konfigurieren.
