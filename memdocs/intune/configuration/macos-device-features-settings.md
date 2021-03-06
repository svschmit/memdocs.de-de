---
title: macOS-Gerätefunktionseinstellungen in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Sehen Sie sich die Einstellungen zur Konfiguration von macOS-Geräten für AirPrint an, und passen Sie das Anmeldefenster so an, dass die Ein-/Ausschaltflächen in Microsoft Intune ein- oder ausgeblendet werden. Beachten Sie die Schritte zum Abrufen der IP-Adresse, des Pfad und der Porteinstellungen eines AirPrint-Servers in Ihrem Netzwerk. Verwenden Sie diese Einstellungen in einem Gerätekonfigurationsprofil, um macOS-Gerätefunktionen zu konfigurieren.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/27/2020
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
ms.openlocfilehash: e70952b0d90222bd31a4e9df997d70e9d528ef24
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/31/2020
ms.locfileid: "89194197"
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

## <a name="content-caching"></a>Zwischenspeicherung von Inhalten

Bei der Zwischenspeicherung von Inhalten wird eine lokale Kopie des Inhalts gespeichert. Diese Informationen können von anderen Apple-Geräten ohne Verbindung mit dem Internet abgerufen werden. Dieses Zwischenspeichern beschleunigt Downloads, indem Softwareupdates, Apps, Fotos und andere Inhalte beim ersten Herunterladen gespeichert werden. Da Apps einmal heruntergeladen und für andere Geräte, Schulen und Organisationen mit vielen Geräten freigegeben werden, wird Bandbreite gespart.

> [!NOTE]
> Verwenden Sie nur ein Profil für diese Einstellungen. Wenn Sie diese Einstellungen mehreren Profilen zuweisen, tritt ein Fehler auf.
>
> Weitere Informationen zum Überwachen der Zwischenspeicherung von Inhalten finden Sie unter [Anzeigen der Protokolle und Statistiken für das Inhaltscaching auf dem Mac](https://support.apple.com/guide/mac-help/view-content-caching-logs-statistics-mac-mchl0d8533cd/10.15/mac/10.15) (Apple-Website wird geöffnet).

Diese Funktion gilt für:

- macOS 10.13.4 und höher

### <a name="settings-apply-to-all-enrollment-types"></a>Die Einstellungen gelten für: Alle Registrierungstypen

Weitere Informationen zu diesen Einstellungen finden Sie unter [Einstellungen der Payload „Inhaltscaching“](https://support.apple.com/guide/mdm/content-caching-mdm163612d39/1/web/1) (Apple-Website wird geöffnet).

**Enable content caching** (Zwischenspeicherung aktivieren): Mit **Ja** wird die Zwischenspeicherung von Inhalten aktiviert, und Benutzer können diese nicht deaktivieren. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Diese Einstellung wird vom Betriebssystem möglicherweise standardmäßig deaktiviert.

- **Type of content to cache** (Inhaltstyp für Zwischenspeicherung): Folgende Optionen sind verfügbar:
  - **All content** (Alle Inhalte): Bei dieser Einstellung werden iCloud- und freigegebene Inhalte zwischengespeichert.
  - **User content only** (Nur Benutzerinhalte): Bei dieser Einstellung werden iCloud-Inhalte einschließlich Fotos und Dokumente zwischengespeichert.
  - **Shared content only** (Nur freigegebene Inhalte): Hier werden Apps und Softwareupdates zwischengespeichert.

- **Maximale Cachegröße:** Geben Sie den maximalen Speicherplatz (in Bytes) an, der zum Zwischenspeichern von Inhalten verwendet wird. Wenn kein Wert angegeben wird (Standardeinstellung), ändert oder aktualisiert Intune diese Einstellung nicht. Standardmäßig wird dieser Wert vom Betriebssystem auf `0` Bytes (Null) festgelegt, wodurch unbegrenzter Speicherplatz für den Cache zur Verfügung gestellt wird.

  Stellen Sie sicher, dass der verfügbare Speicherplatz auf den Geräten nicht überschritten wird. Weitere Informationen zur Gerätespeicherkapazität finden Sie unter [Angabe der Speicherkapazität in iOS und macOS](https://support.apple.com/HT201402) (Apple-Website wird geöffnet).

- **Cache location** (Cachespeicherort): Geben Sie den Pfad zum Speichern der zwischengespeicherten Inhalte ein. Der Standardspeicherort ist `/Library/Application Support/Apple/AssetCache/Data`. Es wird empfohlen, diesen Speicherort nicht zu ändern.

  Wenn Sie diese Einstellung ändern, wird der zwischengespeicherte Inhalt nicht in den neuen Speicherort verschoben. Benutzer müssen den Speicherort auf dem Gerät ändern, um den Inhalt automatisch zu verschieben (**Systemeinstellungen** > **Freigabe** > **Inhalte zwischenspeichern**).

- **Port:** Geben Sie die TCP-Portnummer auf den Geräten ein (0 bis 65535), damit der Zwischenspeicher Download- und Uploadanforderungen akzeptiert. Geben Sie „`0`“ (Null; Standardeinstellung) ein, um einen beliebigen verfügbaren Port zu verwenden.
- **Block internet connection and cache content sharing** (Internetverbindung und Freigabe von Cacheinhalten blockieren): Dies wird auch als Tethered Caching bezeichnet. Mit der Option **Ja** wird die Freigabe von Internetverbindungen und gespeicherten Inhalten für iOS/iPadOS-Geräte verhindert, die über USB-Verbindungen mit dem Mac verbunden sind. Benutzer können diese Funktion nicht aktivieren. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

- **Enable internet connection sharing** (Freigabe der Internetverbindung aktivieren): Dies wird auch als Tethered Caching bezeichnet. Mit der Option **Ja** wird die Freigabe von Internetverbindungen und gespeicherten Inhalten für iOS/iPadOS-Geräte ermöglicht, die über USB-Verbindungen mit dem Mac verbunden sind. Benutzer können diese Funktion nicht deaktivieren. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Diese Einstellung wird vom Betriebssystem möglicherweise standardmäßig deaktiviert.

  Diese Funktion gilt für:

  - macOS 10.15.4 und höher

- **Enable cache to log client details** (Protokollieren von Clientdetails im Cache erlauben): Wenn diese Einstellung auf **Ja** festgelegt ist, werden die IP-Adresse und die Portnummer der Geräte protokolliert, von denen Inhalt angefordert wird. Wenn Sie Probleme mit Geräten beheben möchten, kann diese Protokolldatei helfen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Diese Informationen werden vom Betriebssystem möglicherweise standardmäßig nicht protokolliert.

- **Always keep content from the cache, even when the system needs disk space for other apps** (Inhalte aus dem Cache immer beibehalten, selbst wenn das System Speicherplatz für andere Apps benötigt): Bei der Einstellung **Ja** wird der Cacheinhalt gespeichert und sichergestellt, dass nichts gelöscht wird, selbst wenn nur wenig Speicherplatz verfügbar ist. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig kann das Betriebssystem Inhalte automatisch aus dem Cache löschen, wenn Speicherplatz für andere Apps benötigt wird.

  Diese Funktion gilt für:

  - macOS 10.15 und neuer

- **Show status alerts** (Statusmeldungen anzeigen): Bei **Ja** werden Warnungen als Systembenachrichtigungen angezeigt. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise zeigt das Betriebssystem diese Warnungen nicht als Systembenachrichtigungen an.

  Diese Funktion gilt für:

  - macOS 10.15 und neuer

- **Prevent the device from sleeping while caching is turned on** (Bei aktivierter Zwischenspeicherung den Standbymodus des Geräts verhindern): Bei **Ja** wird verhindert, dass der Computer in den Standbymodus wechselt, wenn das Zwischenspeichern aktiviert ist. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig erlaubt das Betriebssystem möglicherweise den Standbymodus.

  Diese Funktion gilt für:

  - macOS 10.15 und neuer

- **Devices to cache** (Geräte für Zwischenspeicherung): Wählen Sie die Geräte aus, die Inhalte zwischenspeichern können. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. 
  - **Devices using the same local network** (Geräte, die das gleiche lokale Netzwerk verwenden): Der Inhaltscache bietet Geräten im gleichen unmittelbaren Netzwerk die Möglichkeit, Inhalte zu nutzen. Geräten in anderen Netzwerken einschließlich der Geräte, die für den Inhaltscache erreichbar sind, werden keine Inhalte bereitgestellt.
  - **Devices using the same public IP address** (Geräte, die die gleiche öffentliche IP-Adresse verwenden): Der Inhaltscache bietet Geräten, die die gleiche öffentliche IP-Adresse verwenden, die Möglichkeit, Inhalte zu nutzen. Geräten in anderen Netzwerken einschließlich der Geräte, die für den Inhaltscache erreichbar sind, werden keine Inhalte bereitgestellt.
  - **Devices using custom local networks** (Geräte, die benutzerdefinierte lokale Netzwerke verwenden): Der Inhaltscache stellt Inhalte für Geräte in den von Ihnen eingegebenen IP-Adressbereichen bereit.
    - **Client listen ranges** (Clientlauschbereiche): Geben Sie den Bereich der IP-Adressen ein, die den Inhaltscache empfangen können.
  - **Devices using custom local networks with fallback** (Geräte, die benutzerdefinierte lokale Netzwerke mit Fallback verwenden): Der Inhaltscache stellt Inhalte für Geräte in den Lauschbereichen, Peerlauschbereichen und für Geräte mit übergeordneten IP-Adressen bereit.
    - **Client listen ranges** (Clientlauschbereiche): Geben Sie den Bereich der IP-Adressen ein, die den Inhaltscache empfangen können.

- **Custom public IP addresses** (Benutzerdefinierte öffentliche IP-Adressen): Geben Sie einen Bereich öffentlicher IP-Adressen ein. Die Cloudserver verwenden diesen Bereich, um Clientgeräte mit Caches abzugleichen.

- **Share content with other caches** (Inhalte für andere Caches freigeben): Wenn Ihr Netzwerk über mehr als einen Inhaltscache verfügt, werden die Inhaltscaches auf anderen Geräten automatisch zu Peers. Diese Geräte können zwischengespeicherte Software einsehen und freigeben. 

  Wenn ein angefordertes Element nicht in einem Inhaltscache verfügbar ist, werden seine Peers auf das Element überprüft. Wenn das Element verfügbar ist, wird es aus dem Inhaltscache auf dem Peergerät heruntergeladen. Wenn es immer noch nicht verfügbar ist, lädt der Inhaltscache das Element über die folgenden Optionen herunter:

  - übergeordnete IP-Adresse (sofern konfiguriert)
  
    oder
    
  - von Apple über das Internet

  Wenn mehr als ein Inhaltscache verfügbar ist, wählen Geräte automatisch den richtigen Inhaltscache aus. 

  Folgende Optionen sind verfügbar:

  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
  - **Content caches using the same local networks** (Inhaltscaches, die dasselbe lokale Netzwerk verwenden): Ein Inhaltscache stellt nur mit anderen Inhaltscaches im gleichen unmittelbaren lokalen Netzwerk eine Peerverbindung her.
  - **Content caches using the same public IP address** (Inhaltscaches, die dieselbe öffentliche IP-Adresse verwenden): Ein Inhaltscache stellt nur mit anderen Inhaltscaches mit der gleichen öffentlichen IP-Adresse eine Peerverbindung her.
  - **Content caches using custom local networks** (Inhaltscaches, die benutzerdefinierte lokale Netzwerke verwenden): Ein Inhaltscache stellt nur mit anderen Inhaltscaches mit dem von Ihnen eingegebenen IP-Adressenlauschbereich eine Peerverbindung her:

    - **Peer listen ranges** (Peerlauschbereiche): Geben Sie den Anfang und das Ende der IPv4- oder IPv6-IP-Adressen für Ihren Bereich ein. Der Inhaltscache antwortet nur auf Peercacheanforderungen von Inhaltscaches mit den von Ihnen eingegebenen IP-Adressbereichen.
    - **Peer filter ranges** (Peerfilterbereiche): Geben Sie den Anfang und das Ende der IPv4- oder IPv6-IP-Adressen für Ihren Bereich ein. Der Inhaltscache filtert die Peerliste mithilfe der von Ihnen eingegebenen IP-Adressbereiche.

- **Parent IP addresses** (IP-Adressen übergeordneter Caches): Geben Sie die lokale IP-Adresse eines anderen Inhaltscaches ein, der als übergeordneter Cache hinzugefügt werden soll. Der Cache lädt Inhalte in diese Caches hoch und daraus herunter, anstatt sie direkt über Apple hoch- bzw. herunterzuladen. Fügen Sie nur einmal eine übergeordnete IP-Adresse hinzu.
- **Parent selection policy** (Richtlinie für Auswahl übergeordneter Caches): Wenn viele übergeordnete Caches vorhanden sind, wählen Sie aus, wie die übergeordnete IP-Adresse ausgewählt wird. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
  - **Round robin** (Roundrobin): Verwenden Sie die übergeordneten IP-Adressen in der angegebenen Reihenfolge. Diese Option eignet sich für Lastenausgleichsszenarios.
  - **First available** (Erste verfügbare IP-Adresse): Verwenden Sie immer die erste verfügbare IP-Adresse in der Liste.
  - **Hash:** Hiermit wird ein Hashwert für den Pfadteil der angeforderten URL erstellt. Mit dieser Option wird sichergestellt, dass immer dieselbe übergeordnete IP-Adresse für dieselbe URL verwendet wird.
  - **Random** (Zufällig): Hier wird zufällig eine IP-Adresse in der Liste verwendet. Diese Option eignet sich für Lastenausgleichsszenarios.
  - **Sticky available** (Festgelegte Reihenfolge verfügbarer IP-Adressen): Verwenden Sie immer die erste IP-Adresse in der Liste. Wenn diese nicht verfügbar ist, verwenden Sie die zweite IP-Adresse in der Liste. Verwenden Sie weiterhin die zweite IP-Adresse, bis sie nicht verfügbar ist, und setzen Sie diesen Vorgang fort.

## <a name="login-items"></a>Anmeldeelemente

### <a name="settings-apply-to-all-enrollment-types"></a>Die Einstellungen gelten für: Alle Registrierungstypen

- **Fügen Sie die Dateien, Ordner und benutzerdefinierten Apps hinzu, die bei der Anmeldung gestartet werden sollen**: Stellen Sie durch **Hinzufügen** des Pfads einer Datei, eines Ordners, einer benutzerdefinierten App oder System-App sicher, dass diese geöffnet werden, wenn sich der Benutzer auf seinem Gerät anmeldet. Geben Sie außerdem Folgendes ein:

  - **Pfad des Elements**: Geben Sie den Pfad zur Datei, zum Ordner oder zur App ein. System-Apps oder Apps, die für Ihre Organisation entwickelt oder angepasst wurden, befinden sich üblicherweise im Ordner `Applications` und weisen einen Pfad ähnlich wie `/Applications/AppName.app` auf.

    Sie können zahlreiche Dateien, Ordner und Apps hinzufügen. Geben Sie beispielsweise Folgendes ein:  
  
    - `/Applications/Calculator.app`
    - `/Applications`
    - `/Applications/Microsoft Office/root/Office16/winword.exe`
    - `/Users/UserName/music/itunes.app`
  
    Wenn Sie eine App, einen Ordner oder eine Datei hinzufügen, stellen Sie sicher, dass Sie den richtigen Pfad eingeben. Nicht alle Elemente befinden sich im Ordner `Applications`. Wenn ein Benutzer ein Element von einem Speicherort an einen anderen verschiebt, ändert sich der Pfad. Dieses verschobene Element wird nicht geöffnet, wenn sich der Benutzer anmeldet.

  - **Ausblenden:** Sie können die App einblenden oder ausblenden. Folgende Optionen sind verfügbar:
    - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Standardmäßig zeigt das Betriebssystem möglicherweise Elemente in der Liste der Anmeldeelemente für Benutzer und Gruppen an, wenn die Option „Ausblenden“ deaktiviert wird.
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

- **Typ der SSO-App-Erweiterung:** Wählen Sie den Typ der SSO-App-Erweiterung aus. Folgende Optionen sind verfügbar:

  - **Nicht konfiguriert:** Es werden keine App-Erweiterungen verwendet. Um eine App-Erweiterung zu deaktivieren, ändern Sie den Typ der SSO-App-Erweiterung in **Nicht konfiguriert**.
  - **Microsoft Azure AD**: 

    > [!IMPORTANT]
    > Die Microsoft Azure AD SSO-Erweiterung befindet sich derzeit noch in der Entwicklung. Sie wird zwar auf der Benutzeroberfläche von Intune angezeigt, funktioniert aber nicht erwartungsgemäß. Verwenden Sie daher **Microsoft Azure AD** nicht für den SSO-App-Erweiterungstyp.

    Verwendet das Microsoft Enterprise SSO-Plug-In, das eine SSO-App-Erweiterung vom Typ „Umleitung“ ist. Dieses Plug-In aktiviert das einmalige Anmelden für Active Directory-Konten in allen macOS-Anwendungen, die das Feature [Enterprise Single Sign-On von Apple](https://developer.apple.com/documentation/authenticationservices) unterstützen. Verwenden Sie diesen SSO-App-Erweiterungstyp, um einmaliges Anmelden in Microsoft-Apps, Unternehmens-Apps und auf Websites zu aktivieren, die die Authentifizierung mit Azure AD durchführen.

    Das SSO-Plug-In fungiert als erweiterter Authentifizierungsbroker, der eine Verbesserung der Sicherheit und der Benutzerfreundlichkeit bietet.

    > [!IMPORTANT]
    > Um das einmalige Anmelden mit dem SSO-App-Erweiterungstyp von Microsoft Azure AD zu ermöglichen, installieren Sie die macOS-Unternehmensportal-App auf den Geräten. Die Unternehmensportal-App stellt das Microsoft Enterprise SSO-Plug-In auf den Geräten bereit. Die MDM-SSO-App-Erweiterungseinstellungen aktivieren das Plug-In. Wenn die Unternehmensportal-App und das SSO-App-Erweiterungsprofil auf den Geräten installiert sind, müssen die Benutzer sich mit ihren Anmeldeinformationen anmelden und eine Sitzung auf ihren Geräten erstellen. Diese Sitzung wird für verschiedene Anwendungen verwendet, ohne dass sich die Benutzer erneut authentifizieren müssen.
    >
    > Weitere Informationen zur Unternehmensportal-App finden Sie unter [Was geschieht, wenn Sie die Unternehmensportal-App installieren und Ihr macOS-Gerät bei Intune registrieren?](../user-help/what-happens-if-you-install-the-Company-Portal-app-and-enroll-your-device-in-intune-macos.md). Laden Sie die Unternehmensportal-App unter [diesem Link](https://go.microsoft.com/fwlink/?linkid=853070) herunter.

  - **Umleiten:** Verwenden Sie eine generische, anpassbare App-Erweiterung für die Umleitung, um das einmalige Anmelden (Single Sign-On, SSO) mit modernen Authentifizierungsflows zu nutzen. Stellen Sie sicher, dass Sie die Erweiterung und die Team-ID für die App-Erweiterung Ihrer Organisation kennen.
  - **Anmeldeinformationen:** Verwenden Sie eine generische, anpassbare App-Erweiterung für Anmeldeinformationen, um das einmalige Anmelden mit Challenge-Response-Authentifizierungsflows zu nutzen. Stellen Sie sicher, dass Sie die Erweiterungs-ID und die Team-ID für die SSO-App-Erweiterung Ihrer Organisation kennen.  
  - **Kerberos**: Verwenden Sie die integrierte Kerberos-Erweiterung von Apple, die in macOS Catalina 10.15 und höher enthalten ist. Bei dieser Option handelt es sich um eine Kerberos-spezifische Version der App-Erweiterung vom Typ **Anmeldeinformationen**.

  > [!TIP]
  > Mit den Typen **Umleitung** und **Anmeldeinformationen** fügen Sie eigene Konfigurationswerte hinzu, die über die Erweiterung übergeben werden. Erwägen Sie bei Auswahl von **Anmeldeinformationen** die Verwendung integrierter Konfigurationseinstellungen, die von Apple für den Typ **Kerberos** bereitgestellt werden.

- **Erweiterungs-ID** (Umleiten, Anmeldeinformationen): Geben Sie den Bundlebezeichner ein, der Ihre SSO-App-Erweiterung identifiziert, z. B. `com.apple.ssoexample`.
- **Team-ID** (Umleiten, Anmeldeinformationen): Geben Sie den Teambezeichner Ihrer SSO-App-Erweiterung ein. Eine Team-ID ist eine aus 10 Zeichen bestehende alphanumerische (Ziffern und Buchstaben) Zeichenfolge, die von Apple generiert wird, z. B. `ABCDE12345`. 

  Auf der [Seite zur Team-ID-Ermittlung](https://help.apple.com/developer-account/#/dev55c3c710c) (öffnet die Website von Apple) finden Sie weitere Informationen.

- **Bereich** (Anmeldeinformationen, Kerberos): Geben Sie den Namen Ihres Authentifizierungsbereichs ein. Der Bereichsname sollte groß geschrieben werden, z. B. `CONTOSO.COM`. In der Regel ist Ihr Bereichsname mit dem DNS-Domänennamen identisch, besteht aber nur aus Großbuchstaben.

- **Domänen** (Anmeldeinformationen, Kerberos): Geben Sie die Domänen- oder Hostnamen der Websites ein, auf denen eine Authentifizierung über SSO möglich ist. Wenn Ihre Website beispielsweise `mysite.contoso.com` lautet, ist `mysite` der Hostname und `contoso.com` der Domänenname. Wenn Benutzer eine Verbindung mit einer dieser Websites herstellen, verarbeitet die App-Erweiterung die Authentifizierung. Diese Authentifizierung ermöglicht es Benutzern Face ID, Touch ID oder eine PIN/einen Passcode von Apple für die Anmeldung zu verwenden.

  - Alle Domänen in den Intune-Profilen für Ihre SSO-App-Erweiterung müssen eindeutig sein. Sie können eine Domäne nicht mehrfach in einem SSO-App-Erweiterungsprofil verwenden – selbst dann nicht, wenn Sie verschiedene Arten von SSO-App-Erweiterungen verwenden.
  - Für diese Domänen erfolgt keine Beachtung der Groß-/Kleinschreibung.

- **URLs** (nur „Umleiten“): Geben Sie die URL-Präfixe der Identitätsanbieter ein, in deren Auftrag die Umleitungs-App-Erweiterung die SSO-Authentifizierung nutzt. Wenn Benutzer auf diese URLs umgeleitet werden, greift die SSO-App-Erweiterung ein und fordert eine SSO-Authentifizierung an.

  - Alle URLs in Ihren Intune-SSO-Erweiterungsprofilen müssen eindeutig sein. Sie können eine Domäne nicht mehrfach in einem SSO-App-Erweiterungsprofil verwenden – selbst dann nicht, wenn Sie verschiedene Arten von SSO-App-Erweiterungen verwenden.
  - Die URLs müssen mit `http://` oder `https://` beginnen.

- **Zusätzliche Konfiguration** (Microsoft Azure AD, Umleiten, Anmeldeinformationen): Geben Sie zusätzliche erweiterungsspezifische Daten ein, die an die SSO-App-Erweiterung übergeben werden sollen:
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
- **Windows Server Active Directory password complexity** (Windows Server Active Directory-Kennwortkomplexität) (nur „Kerberos“): Klicken Sie auf **Anfordern**, um durchzusetzen, dass Benutzer die Anforderungen an die Kennwortkomplexität erfüllen müssen, die Active Directory stellt. Weitere Informationen finden Sie unter [Kennwort muss Komplexitätsvoraussetzungen entsprechen](/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements). Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig fordert das Betriebssystem möglicherweise nicht, dass Benutzer die Active Directory-Kennwortanforderungen erfüllen.
- **Mindestkennwortlänge** (nur „Kerberos“): Geben Sie die Mindestanzahl von Zeichen ein, aus denen das Kennwort eines Benutzers bestehen muss. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig erzwingt das Betriebssystem möglicherweise keine Mindestlänge für Benutzerkennwörter.
- **Limit für die Wiederverwendung von Kennwörtern** (nur „Kerberos“): Geben Sie die Anzahl neuer Kennwörter ein (1 bis 24), die verwendet werden, bis ein vorheriges Kennwort für die Domäne wiederverwendet werden kann. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig erzwingt das Betriebssystem möglicherweise kein Limit für die Wiederverwendung von Kennwörtern.
- **Minimum password age** (Mindestkennwortalter) (nur „Kerberos“): Geben Sie die Anzahl von Tagen ein, die ein Kennwort für die Domäne verwendet wird, bevor ein Benutzer es ändern kann. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig erzwingt das Betriebssystem möglicherweise kein Mindestkennwortalter, bevor ein Kennwort geändert werden kann.
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
- **Modus für gemeinsam genutzte Geräte aktivieren** (nur Microsoft Azure AD): Klicken Sie auf **Ja**, wenn Sie das Microsoft Enterprise SSO-Plug-In auf macOS-Geräten bereitstellen, die für den Azure AD-Modus für gemeinsam genutzte Geräte konfiguriert sind. Geräte im Freigabemodus ermöglichen es vielen Benutzern, sich global bei Anwendungen, die den Freigabemodus für Geräte unterstützen, an- und abzumelden. Wenn die Einstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert. 

  Bei Auswahl von **Ja** werden alle vorhandenen Benutzerkonten von den Geräten gelöscht. Sie müssen genau wissen, wie diese Einstellungen die Geräte ändern, damit es nicht zu Datenverlusten kommt oder die Geräte unabsichtlich auf die Werkseinstellungen zurückgesetzt werden.

  Weitere Informationen zum Modus für gemeinsam genutzte Geräte finden Sie unter [Übersicht über den Modus für gemeinsam genutzte Geräte](/azure/active-directory/develop/msal-shared-devices).

- **App-Bundle-IDs** (Microsoft Azure AD, Kerberos): Mit **Hinzufügen** werden die App-Bundle-IDs hinzugefügt, für die auf Ihren Geräten SSO verwendet werden soll. Diese Apps erhalten Zugriff auf das Kerberos-TGT (Ticket Granting Ticket) sowie das Authentifizierungsticket. Außerdem authentifizieren diese Apps Benutzer für Dienste, für die sie über Zugriffsberechtigungen verfügen.
- **Domänenbereichszuordnung** (nur „Kerberos“): Mit **Hinzufügen** werden die Domänen-DNS-Suffixe hinzugefügt, die Ihrem Bereich zugeordnet werden sollen. Verwenden Sie diese Einstellung, wenn die DNS-Namen der Hosts nicht mit dem Bereichsnamen identisch sind. Wahrscheinlich ist es nicht erforderlich, diese Zuordnung zwischen benutzerdefinierter Domäne und Bereich zu erstellen.
- **PKINIT-Zertifikat** (nur „Kerberos“): Mit **Auswählen** legen Sie das PKINIT-Zertifikat (Public Key Cryptography for Initial Authentication) fest, das für die Kerberos-Authentifizierung verwendet werden kann. Sie können aus [PKCS](../protect/certficates-pfx-configure.md)- oder [SCEP](../protect/certificates-scep-configure.md)-Zertifikaten auswählen, die Sie in Intune hinzugefügt haben. Weitere Informationen zu Zertifikaten finden Sie unter [Verwenden von Zertifikaten zur Authentifizierung in Microsoft Intune](../protect/certificates-configure.md).

## <a name="next-steps"></a>Nächste Schritte

[Zuweisen von Profilen](device-profile-assign.md) und [Überwachen von Profilen](device-profile-monitor.md)

Sie können außerdem Gerätefeatures für [iOS/iPadOS](ios-device-features-settings.md) konfigurieren.