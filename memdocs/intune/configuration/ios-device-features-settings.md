---
title: iOS/iPadOS-Gerätefunktionseinstellungen in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Schauen Sie sich alle Einstellungen an, um iOS- und iPadOS-Geräte für AirPrint, das Layout des Startbildschirms, App-Benachrichtigungen, freigegebene Geräte, einmaliges Anmelden und Webinhaltsfiltereinstellungen in Microsoft Intune zu konfigurieren. Verwenden Sie diese Einstellungen in einem Gerätekonfigurationsprofil, um iOS/iPadOS-Geräte so zu konfigurieren, dass sie diese Apple-Funktionen in Ihrem Unternehmen nutzen.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/07/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: ''
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 235a79f644bf15b82eb9e8750f04519238760aca
ms.sourcegitcommit: 5d32dd481e2a944465755ce74e14c835cce2cd1c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/18/2020
ms.locfileid: "83551926"
---
# <a name="ios-and-ipados-device-settings-to-use-common-iosipados-features-in-intune"></a>iOS- und iPadOS-Geräteeinstellungen zur Verwendung gängiger iOS/iPadOS-Features in Intune

Intune umfasst einige integrierte Einstellungen, damit iOS/iPadOS-Benutzer verschiedene Apple-Features auf ihren Geräten nutzen können. Sie können beispielsweise AirPrint-Drucker steuern, Apps und Ordner dem Dock und den Seiten des Startbildschirms hinzufügen, App-Benachrichtigungen anzeigen, Details zu Bestandskennzeichen auf dem Sperrbildschirm anzeigen, Authentifizierung für einmaliges Anmelden und Zertifikatauthentifizierung verwenden.

Nutzen Sie diese Features, um iOS/iPadOS-Geräte im Rahmen Ihrer MDM-Lösung (Mobile Device Management, Verwaltung mobiler Geräte) zu verwalten.

In diesem Artikel werden diese Einstellungen mit ihren Funktionsbeschreibungen aufgeführt. Weitere Informationen zu diesen Gerätefeatures finden Sie unter [Hinzufügen von Einstellungen für iOS/iPadOS- oder macOS-Gerätefunktionen in Intune](device-features-configure.md).

## <a name="before-you-begin"></a>Vorbereitung

[Erstellen Sie ein iOS-/iPadOS-Gerätefeatureprofil.](device-features-configure.md)

> [!NOTE]
> Diese Einstellungen gelten für verschiedene Registrierungstypen, wobei einige Einstellungen für alle Registrierungsoptionen gelten. Weitere Informationen zu den verschiedenen Registrierungstypen finden Sie unter [iOS/iPadOS-Registrierung](../enrollment/ios-enroll.md).

## <a name="airprint"></a>AirPrint

### <a name="settings-apply-to-all-enrollment-types"></a>Die Einstellungen gelten für: Alle Registrierungstypen

> [!NOTE]
> Stellen Sie sicher, dass Sie alle Drucker demselben Profil hinzufügen. Apple verhindert, dass mehrere AirPrint-Profile auf dasselbe Gerät verweisen.

- **IP-Adresse**: Geben Sie die IPv4- oder IPv6-Adresse des Druckers ein. Wenn Sie den Hostnamen verwenden, um Drucker zu identifizieren, erhalten Sie die IP-Adresse, indem Sie den Drucker am Terminal pingen. Der Abschnitt über das Abrufen von IP-Adresse und Pfad (in diesem Artikel) enthält weitere Details.
- **Pfad:** Der Pfad ist für Drucker in Ihrem Netzwerk in der Regel `ipp/print`. Der Abschnitt über das Abrufen von IP-Adresse und Pfad (in diesem Artikel) enthält weitere Details.
- **Port:** Geben Sie den Lauschport des AirPrint-Ziels ein. Wenn Sie diese Eigenschaft leer lassen, verwendet AirPrint den Standardport. In iOS 11.0+ und iPadOS 13.0+ verfügbar.
- **TLS**: **Aktivieren** sichert AirPrint-Verbindungen mit Transport Layer Security (TLS). In iOS 11.0+ und iPadOS 13.0+ verfügbar.

Zum Hinzufügen von AirPrint-Servern können Sie folgende Schritte ausführen:

- Über **Hinzufügen** wird der AirPrint-Server der Liste hinzugefügt. Es können zahlreiche AirPrint-Server hinzugefügt werden.
- **Importieren** Sie eine durch Trennzeichen getrennte Datei (.csv) mit diesen Informationen. Oder erstellen Sie über **Exportieren** eine Liste der von Ihnen hinzugefügten AirPrint-Server.

### <a name="get-server-ip-address-resource-path-and-port"></a>Abrufen der IP-Adresse des Servers, des Ressourcenpfads und Ports

Um AirPrinter-Server hinzuzufügen, benötigen Sie die IP-Adresse des Druckers, den Ressourcenpfad und den Port. Die folgenden Schritte zeigen Ihnen, wie Sie diese Informationen abrufen.

1. Öffnen Sie das **Terminal** auf einem Mac, der mit demselben lokalen Netzwerk (Subnetz) verbunden ist wie die AirPrint-Drucker (über **/Programme/Dienstprogramme**).
2. Geben Sie im Terminal `ippfind` ein, und wählen Sie „Eingabe“ aus.

    Beachten Sie die Druckerinformationen. Es könnte z.B. `ipp://myprinter.local.:631/ipp/port1` zurückgegeben werden. Der erste Teil ist der Name des Druckers. Der letzte Teil (`ipp/port1`) ist der Pfad der Ressource.

3. Geben Sie im Terminal `ping myprinter.local` ein, und wählen Sie „Eingabe“ aus.

   Beachten Sie die IP-Adresse. Es könnte z.B. `PING myprinter.local (10.50.25.21)` zurückgegeben werden.

4. Verwenden Sie die Werte von IP-Adresse und Ressourcenpfad. In diesem Beispiel ist die IP-Adresse `10.50.25.21` und der Ressourcenpfad `/ipp/port1`.

## <a name="home-screen-layout"></a>Layout des Startbildschirms

Diese Funktion gilt für:

- iOS 9.3 oder höher
- iOS 13.0 und höher

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Die Einstellungen gelten für: Automatisierte Geräteregistrierung (überwacht)

### <a name="dock"></a>Dock

Mit der Einstellung **Dock** können Sie dem Dock des Bildschirms bis zu sechs Elemente oder Ordner hinzufügen. Viele Geräte unterstützen weniger Elemente. Beispielsweise unterstützen iPhone-Geräte bis zu vier Elemente. In diesem Fall werden nur die ersten vier Elemente, die Sie hinzugefügt haben, auf dem Gerät angezeigt.

Sie können für den Gerätedock bis zu **sechs** Elemente hinzufügen (Apps und Ordner kombiniert).

- **Hinzufügen**: Fügt dem Dock auf dem Gerät Apps oder Ordner hinzu.
- **Typ:** Fügen Sie eine **App** oder einen **Ordner** hinzu:

  - **App**: Wählen Sie diese Option, um Apps zum Dock auf dem Bildschirm hinzuzufügen. Eingeben:

    - **App-Name:** Geben Sie einen Namen für die App ein. Dieser Name wird zu Ihrer Referenz im Microsoft Endpoint Manager Admin Center verwendet. Er wird *nicht* auf dem iOS/iPadOS-Gerät angezeigt.
    - **App-Bündel-ID:** Geben Sie die „Bündel-ID“ der App ein. Einige Beispiele finden Sie unter [Bundle-IDs für integrierte iOS/iPadOS-Apps](bundle-ids-built-in-ios-apps.md).

  - **Ordner**: Wählen Sie diese Option, um einen Ordner zum Dock auf dem Bildschirm hinzuzufügen.

    Apps, die Sie zu einer Seite in einem Ordner hinzufügen, werden von links nach rechts und in der gleichen Reihenfolge wie die Liste angeordnet. Wenn Sie mehr Apps hinzufügen, als auf eine Seite passen, werden die Apps auf eine andere Seite verschoben.

    - **Ordnername:** Geben Sie den Namen des Ordners ein. Dieser Name wird Benutzern auf ihren Geräten angezeigt.
    - **Liste der Seiten**: **Fügen Sie** eine Seite hinzu, und geben Sie die folgenden Eigenschaften ein:

      - **Name der Seite**: Geben Sie einen Namen für die Seite ein. Dieser Name wird zu Ihrer Referenz im Microsoft Endpoint Manager Admin Center verwendet. Er wird *nicht* auf dem iOS/iPadOS-Gerät angezeigt.
      - **App-Name:** Geben Sie einen Namen für die App ein. Dieser Name wird zu Ihrer Referenz im Microsoft Endpoint Manager Admin Center verwendet. Er wird *nicht* auf dem iOS/iPadOS-Gerät angezeigt.
      - **App-Bündel-ID:** Geben Sie die „Bündel-ID“ der App ein. Einige Beispiele finden Sie unter [Bundle-IDs für integrierte iOS/iPadOS-Apps](bundle-ids-built-in-ios-apps.md).

      Sie können für den Gerätedock bis zu **20** Seiten hinzufügen.

> [!NOTE]
> Wenn Sie die Layouteinstellungen für den Startbildschirm verwenden, um Seiten hinzuzufügen oder Seiten und Apps zum Dock hinzuzufügen, werden die Symbole auf dem Startbildschirm und den Seiten gesperrt. Sie können nicht verschoben oder gelöscht werden. Dies kann bei iOS-/iPadOS- und MDM-Richtlinien von Apple absichtlich der Fall sein.

#### <a name="example"></a>Beispiel

Im folgenden Beispiel werden im Bildschirm „Dock“ nur die Anwendungen Safari, Mail und Stocks angezeigt. Die Mail-App wird ausgewählt, um deren Eigenschaften anzuzeigen:

> [!div class="mx-imgBorder"]
> ![Beispieleinstellungen für das iOS/iPad-Startbildschirmlayout in Intune](./media/ios-device-features-settings/dock-screen-mail-app.png)

Wenn Sie einem iPhone die Richtlinie zuweisen, sieht der Dock etwa so aus:

> [!div class="mx-imgBorder"]
> ![Beispiellayout für das iOS-/iPadOS-Dock auf dem iPhone](./media/ios-device-features-settings/bAgCe8F.png)

### <a name="pages"></a>Seiten

Fügen Sie die Seiten hinzu, die auf dem Startbildschirm angezeigt werden sollen, und die Apps, die auf jeder Seite angezeigt werden. Apps, die Sie zu einer Seite hinzufügen, werden von links nach rechts und in der gleichen Reihenfolge wie die Liste angeordnet. Wenn Sie mehr Apps hinzufügen, als auf eine Seite passen, werden die Apps auf eine andere Seite verschoben.

> [!TIP]
> Elemente auf jedem Startbildschirm und auf allen Seiten können Sie mittels Ziehen und Ablegen sortieren.

Sie können bis zu **40** Seiten zu einem Gerät hinzufügen.

- **Liste der Seiten**: **Fügen Sie** eine Seite hinzu, und geben Sie die folgenden Eigenschaften ein:

  - **Name der Seite**: Geben Sie einen Namen für die Seite ein. Dieser Name wird zu Ihrer Referenz im Microsoft Endpoint Manager Admin Center verwendet und *nicht* auf dem iOS/iPadOS-Gerät angezeigt.

  Sie können auf einem Gerät bis zu **60** Elemente hinzufügen (Apps und Ordner kombiniert).

  - **Hinzufügen**: Fügt einer Seite auf dem Gerät Apps oder Ordner hinzu

    - **Typ:** Fügen Sie eine **App** oder einen **Ordner** hinzu:

      - **App**: Verwenden Sie diese Option, um Apps zu einer Seite auf dem Bildschirm hinzuzufügen. Geben Sie außerdem Folgendes ein:

        - **App-Name:** Geben Sie einen Namen für die App ein. Dieser Name wird zu Ihrer Referenz im Microsoft Endpoint Manager Admin Center verwendet. Er wird *nicht* auf dem iOS/iPadOS-Gerät angezeigt.
        - **App-Bündel-ID:** Geben Sie die „Bündel-ID“ der App ein. Einige Beispiele finden Sie unter [Bundle-IDs für integrierte iOS/iPadOS-Apps](bundle-ids-built-in-ios-apps.md).

      - **Ordner**: Wählen Sie diese Option, um einen Ordner zum Dock auf dem Bildschirm hinzuzufügen.

        Apps, die Sie zu einer Seite in einem Ordner hinzufügen, werden von links nach rechts und in der gleichen Reihenfolge wie die Liste angeordnet. Wenn Sie mehr Apps hinzufügen, als auf eine Seite passen, werden die Apps auf eine andere Seite verschoben.

        - **Ordnername:** Geben Sie einen Namen für den Ordner ein. Dieser Name wird Benutzern auf ihren Geräten angezeigt.
        - **Hinzufügen**: Fügt dem Ordner Seiten hinzu. Geben Sie auch die folgenden Eigenschaften ein:

          - **Name der Seite**: Geben Sie einen Namen für die Seite ein. Dieser Name wird zu Ihrer Referenz im Microsoft Endpoint Manager Admin Center verwendet. Er wird *nicht* auf dem iOS/iPadOS-Gerät angezeigt.
          - **App-Name:** Geben Sie einen Namen für die App ein. Dieser Name wird zu Ihrer Referenz im Microsoft Endpoint Manager Admin Center verwendet. Er wird *nicht* auf dem iOS/iPadOS-Gerät angezeigt.
          - **App-Bündel-ID:** Geben Sie die „Bündel-ID“ der App ein. Einige Beispiele finden Sie unter [Bundle-IDs für integrierte iOS/iPadOS-Apps](bundle-ids-built-in-ios-apps.md).

#### <a name="example"></a>Beispiel

Im folgenden Beispiel wird eine neue Seite mit dem Namen **Contoso** hinzugefügt. Die Seite zeigt die Apps „Freunde finden“ und „Einstellungen“ an:

> [!div class="mx-imgBorder"]
> ![Einstellungen für neue Seiten und Beispiel für das iOS/iPad-Startbildschirmlayout in Intune](./media/ios-device-features-settings/page-find-friends-settings-apps.png)

Die Settings-App wird ausgewählt, um deren Eigenschaften anzuzeigen:

> [!div class="mx-imgBorder"]
> ![Beispieleigenschaften für die App „Einstellungen“ für das iOS/iPad-Startbildschirmlayout in Intune](./media/ios-device-features-settings/page-settings-app-properties.png)

Wenn Sie einem iPhone die Richtlinie zuweisen, sieht die Seite etwa so aus:

> [!div class="mx-imgBorder"]
> ![iOS-/iPadOS-Gerät mit geändertem Startbildschirm in Intune](./media/ios-device-features-settings/Bd37PHa.png)

## <a name="app-notifications"></a>App-Benachrichtigungen

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Die Einstellungen gelten für: Automatisierte Geräteregistrierung (überwacht)

- **Hinzufügen**: Hinzufügen von Benachrichtigungen für Apps:

  > [!div class="mx-imgBorder"]
  > ![Hinzufügen von App-Benachrichtigungen in einem iOS-/iPadOS-Profil in Intune](./media/ios-device-features-settings/ios-ipados-app-notifications.png)

  - **App-Bündel-ID**: Geben Sie die **App-Bündel-ID** der App ein, die Sie hinzufügen möchten. Einige Beispiele finden Sie unter [Bundle-IDs für integrierte iOS/iPadOS-Apps](bundle-ids-built-in-ios-apps.md).
  - **App-Name:** Geben Sie die den Namen der App ein, die Sie hinzufügen möchten. Dieser Name wird zu Ihrer Referenz im Microsoft Endpoint Manager Admin Center verwendet. Er wird *nicht* auf dem Gerät angezeigt.
  - **Herausgeber**: Geben Sie den Namen des Herausgebers der App ein, die Sie hinzufügen. Dieser Name wird zu Ihrer Referenz im Microsoft Endpoint Manager Admin Center verwendet. Er wird *nicht* auf dem Gerät angezeigt.
  - **Benachrichtigungen:** **Aktivieren** oder **deaktivieren** Sie das Senden von Benachrichtigungen von der App an Geräte.
    - **In Mitteilungszentrale anzeigen**: **Aktivieren** Sie diese Option, um zuzulassen, dass Benachrichtigungen der App in der Mitteilungszentrale angezeigt werden. **Deaktivieren** Sie diese Option, um zu verhindern, dass Benachrichtigungen in der Mitteilungszentrale angezeigt werden.
    - **In Sperrbildschirm anzeigen**: Mit der Einstellung **Aktivieren** werden App-Benachrichtigungen auf dem Sperrbildschirm des Geräts angezeigt. **Deaktivieren** Sie diese Option, um zu verhindern, dass Benachrichtigungen im Sperrbildschirm angezeigt werden.
    - **Warnungstyp**: Wählen Sie aus, wie die Benachrichtigung angezeigt wird, wenn das Gerät entsperrt wird. Folgende Optionen sind verfügbar:
      - **Keine**: Es werden keine Benachrichtigungen angezeigt.
      - **Banner**: Es wird kurz ein Banner mit der Benachrichtigung angezeigt.
      - **Modal**: Die Benachrichtigung wird angezeigt, und der Benutzer muss sie manuell schließen, um das Gerät weiter verwenden zu können.
    - **Badge auf App-Symbol**: Wählen Sie **Aktivieren**, um ein Badge zum App-Symbol hinzuzufügen. Das Badge bedeutet, dass die App eine Benachrichtigung gesendet hat.
    - **Sounds**: Wählen sie **Aktivieren**, um einen Sound wiederzugeben, wenn eine Benachrichtigung eintrifft.

## <a name="lock-screen-message"></a>Nachricht auf Sperrbildschirm

Diese Funktion gilt für:

- iOS 9.3 und höher
- iOS 13.0 und höher

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Die Einstellungen gelten für: Automatisierte Geräteregistrierung (überwacht)

- **Bestandskennzeicheninformationen:** Geben Sie Informationen zum Bestandskennzeichen des Geräts ein. Geben Sie beispielsweise `Owned by Contoso Corp` oder `Serial Number: {{serialnumber}}` ein.

  Der von Ihnen eingegebene Text wird auf dem Gerät im Anmeldefenster und auf dem Sperrbildschirm angezeigt.

- **Fußnote im Sperrbildschirm:** Geben Sie einen Hinweis ein, der Ihnen helfen könnte, das Gerät zurückzubekommen, wenn es verloren geht oder gestohlen wird. Sie können einen beliebigen Text eingeben. Geben Sie zum Beispiel `If found, call Contoso at ...` ein.

  Gerätetoken können auch verwendet werden, um gerätespezifische Informationen zu diesen Feldern hinzuzufügen. Geben Sie zum Beispiel zur Anzeige der Seriennummer `Serial Number: {{serialnumber}}` ein. Auf dem Sperrbildschirm sieht der Text dann in etwa so aus: `Serial Number 123456789ABC`. Achten Sie darauf, bei der Eingabe von Variablen geschweifte Klammern `{{ }}` zu verwenden. [App-Konfigurationstoken](../apps/app-configuration-policies-use-ios.md#tokens-used-in-the-property-list) umfassen eine Reihe von Variablen, die Sie nutzen können. Zudem können Sie `deviceName` oder einen anderen gerätespezifischen Wert verwenden.

  > [!NOTE]
  > Variablen werden in der Benutzeroberfläche nicht überprüft, und die Groß-/Kleinschreibung muss beachtet werden. Daher gibt es möglicherweise Profile, die mit fehlerhaften Eingaben gespeichert wurden. Wenn Sie beispielsweise `{{DeviceID}}` anstelle von `{{deviceid}}` oder '{{DEVICEID}}' eingeben, wird die Literalzeichenfolge anstelle der eindeutigen Geräte-ID angezeigt. Stellen Sie sicher, dass die eingegebenen Informationen korrekt sind. Variablen, die vollständig klein oder groß geschrieben sind, werden unterstützt. Eine Kombination beider Schreibweisen ist jedoch nicht zulässig. 

## <a name="single-sign-on"></a>Einmaliges Anmelden

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Die Einstellungen gelten für: Geräteregistrierung, automatisierte Geräteregistrierung (überwacht)

- **Bereich**: Geben Sie den Domänenteil der URL ein. Geben Sie beispielsweise `contoso.com` ein.
- **Kerberos-Prinzipalname**: Intune sucht für jeden Azure AD-Benutzer nach diesem Attribut. Intune füllt anschließend das entsprechende Feld (z. B. „UPN“) aus, bevor der auf dem Gerät zu installierende XML-Code generiert wird. Folgende Optionen sind verfügbar:

  - **Nicht konfiguriert:** Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Standardmäßig fordert das Betriebssystem die Benutzer zur Eingabe eines Kerberos-Prinzipalnamens auf, wenn das Profil auf Geräten bereitgestellt wird. Ein Prinzipalname ist erforderlich, damit MDMs SSO-Profile installieren können.
  - **Benutzerprinzipalname**: Der Benutzerprinzipalname wird wie folgt analysiert:

    > [!div class="mx-imgBorder"]
    > ![SSO-Attribut für den iOS-/iPadOS-Benutzernamen in Intune](./media/ios-device-features-settings/User-name-attribute.png)

    Sie können den Bereich auch mit dem Text überschreiben, den Sie in das Textfeld **Bereich** eingeben.

    Beispielsweise verfügt Contoso über mehrere Regionen, wie z.B. Europa, Asien und Nordamerika. Contoso möchte, dass seine Benutzer in Asien das einmalige Anmelden verwenden und der UPN muss laut App im Format `username@asia.contoso.com` vorliegen. Wenn Sie den **Benutzerprinzipalname** auswählen, wird der Bereich für die einzelnen Benutzer aus Azure AD übernommen, z.B. `contoso.com`. Wählen Sie für Benutzer in Asien, also **Benutzerprinzipalname**, und geben Sie `asia.contoso.com` ein. Daraufhin wird für den UPN des Benutzers `username@asia.contoso.com` anstelle von `username@contoso.com` verwendet.

  - **Intune-Geräte-ID**: Intune wählt die Intune-Geräte-ID automatisch aus.

    Standardmäßig müssen Apps lediglich die Geräte-ID verwenden. Wenn Ihre App den Bereich und die Geräte-ID verwendet, können Sie den Bereich in das Textfeld **Bereich** eingeben.

    > [!NOTE]
    > Der Bereich sollte standardmäßig leer gelassen werden, wenn Sie die Geräte-ID verwenden.

  - **Azure AD-Geräte-ID**
  - **SAM-Kontoname**: Intune füllt den SAM-Kontonamen (Security Accounts Manager) lokal aus.


- **Apps**: **Fügen** Sie Apps auf Benutzergeräten hinzu, die das einmalige Anmelden verwenden können.

  Das `AppIdentifierMatches`-Array muss Zeichenfolgen enthalten, die mit App-Bündel-IDs übereinstimmen. Bei diesen Zeichenfolgen kann es sich um exakte Übereinstimmungen (z.B. `com.contoso.myapp`) handeln. Sie können aber auch Präfixübereinstimmungen der Bündel-ID unter Verwendung des Platzhalterzeichens \* angeben. Das Platzhalterzeichen muss nach einem Punkt (.) folgen und kann nur einmal am Ende der Zeichenfolge verwendet werden (z.B. `com.contoso.*`). Wenn ein Platzhalter enthalten ist, erhält jede App, deren Bündel-ID mit dem Präfix beginnt, Zugriff auf das Konto.

  Verwenden Sie den **App-Namen** als benutzerfreundlichen Namen, um die Bündel-ID einfacher identifizieren zu können.

- **URL-Präfixe**: **Fügen** Sie alle URLs in Ihrer Organisation hinzu, für die Benutzer eine Authentifizierung durch einmaliges Anmelden durchführen müssen.

  Wenn ein Benutzer beispielsweise eine Verbindung mit einer dieser Websites herstellt, verwendet das iOS/iPadOS-Gerät die SSO-Anmeldeinformationen. Der Benutzer muss keine zusätzlichen Anmeldeinformationen eingeben. Wenn Sie die mehrstufige Authentifizierung aktiviert haben, müssen Benutzer die zweite Authentifizierungsmethode anwenden.

  > [!NOTE]
  > Bei diesen URLs muss es sich um ordnungsgemäß formatierte FQDNs handeln. Bei Apple müssen diese im Format `http://<yourURL.domain>` sein.

  Die URL-Übereinstimmungsmuster müssen entweder mit `http://` oder `https://` beginnen. Es wird ein einfacher Zeichenfolgenabgleich ausgeführt, sodass das URL-Präfix `http://www.contoso.com/` nicht mit `http://www.contoso.com:80/` übereinstimmt. With iOS 10.0+ und iPadOS 13.0+ kann ein einzelnes Platzhalterzeichen (\*) verwendet werden, um alle übereinstimmenden Werte anzugeben. Beispielsweise entspricht `http://*.contoso.com/` sowohl `http://store.contoso.com/` als auch `http://www.contoso.com`.

  Die Muster `http://.com` und `https://.com` stimmen mit allen HTTP- bzw. HTTPS-URLs überein.

- **Erneuerungszertifikat**: Erfolgt die Authentifizierung anhand von Zertifikaten (nicht Kennwörtern), wählen Sie als Authentifizierungszertifikat das vorhandene SCEP- oder PFX-Zertifikat aus. In der Regel handelt es sich dabei um das Zertifikat, das dem Benutzer für andere Profile wie VPN, WLAN oder E-Mail bereitgestellt wird.

## <a name="web-content-filter"></a>Webinhaltsfilter

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Die Einstellungen gelten für: Automatisierte Geräteregistrierung (überwacht)

- **Filtertyp**: Wählen, ob bestimmte Websites zugelassen werden sollen. Folgende Optionen sind verfügbar:

  - **URLs konfigurieren**: Verwenden Sie den integrierten Webfilter von Apple, der nach jugendgefährdender Sprache wie Kraftausdrücken und sexuell freizügiger Sprache sucht. Diese Funktion wertet jede Webseite beim Laden aus und identifiziert und blockiert ungeeignete Inhalte. Sie können auch URLs hinzufügen, die nicht vom Filter überprüft werden sollen. Alternativ können bestimmte URLs blockiert werden, unabhängig von den Apple-Filtereinstellungen.

    - **Zulässige URLs**: **Fügen** Sie die URLs hinzu, die Sie zulassen möchten. Diese URLs umgehen den Apple-Webfilter.

        > [!NOTE]
        > Die eingegebene URLs sind die URLs, die Sie nicht vom Apple-Webfilter überprüfen lassen möchten. Diese URLs sind keine Liste der zulässigen Websites. Um eine Liste der zulässigen Websites zu erstellen, legen Sie **Filtertyp** auf **Nur bestimmte Websites** fest.

    - **Blockierte URLs**: **Fügen** Sie die URLs hinzu, die Sie nicht öffnen möchten, unabhängig von der den Einstellung für den Apple-Webfilter.

  - **Nur bestimmte Websites** (nur für Safari-Webbrowser): Diese URLs werden den Lesezeichen im Safari-Browser hinzugefügt. Benutzer dürfen **nur** diese Websites besuchen. Ein Zugriff auf andere Websites ist nicht möglich. Verwenden Sie diese Option nur, wenn Sie genau wissen, auf welche URLs Benutzer zugreifen können.

    - **URL**: Geben Sie die URL der Website ein, die Sie zulassen möchten. Geben Sie beispielsweise `https://www.contoso.com` ein.
    - **Lesezeichenpfad**: Apple hat diese Einstellung geändert. Alle Lesezeichen werden dem Ordner **Genehmigte Websites** hinzugefügt. Lesezeichen werden nicht in dem von Ihnen eingegebenen Lesezeichenpfad gespeichert.
    - **Titel**: Geben Sie einen beschreibenden Titel für das Lesezeichen ein.

    Wenn Sie keine URLs eingeben, können Benutzer nur auf die Websites `microsoft.com`, `microsoft.net` und `apple.com` zugreifen. Diese URLs werden von Intune automatisch zugelassen.

## <a name="single-sign-on-app-extension"></a>App-Erweiterung für einmaliges Anmelden

Diese Funktion gilt für:

- iOS 13.0 und höher
- iPadOS 13.0 und höher

### <a name="settings-apply-to-all-enrollment-types"></a>Die Einstellungen gelten für: Alle Registrierungstypen

- **Typ der SSO-App-Erweiterung:** Wählen Sie den Typ der SSO-App-Erweiterung aus. Folgende Optionen sind verfügbar:

  - **Nicht konfiguriert:** Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Standardmäßig verwendet das Betriebssystem keine App-Erweiterungen. Um eine App-Erweiterung zu deaktivieren, können Sie den Typ der SSO-App-Erweiterung in **Nicht konfiguriert** ändern.
  - **Microsoft Azure AD**: Verwendet das Microsoft Enterprise SSO-Plug-In, das eine SSO-App-Erweiterung vom Typ „Umleitung“ ist. Dieses Plug-In bietet einmaliges Anmelden für Active Directory-Konten in allen Anwendungen, die das Feature [Enterprise Single Sign-On von Apple](https://developer.apple.com/documentation/authenticationservices) unterstützen. Verwenden Sie diesen SSO-App-Erweiterungstyp, um einmaliges Anmelden in Microsoft-Apps, Unternehmens-Apps und auf Websites zu aktivieren, die die Authentifizierung mit Azure AD durchführen.

    Das SSO-Plug-In fungiert als erweiterter Authentifizierungsbroker, der eine Verbesserung der Sicherheit und der Benutzerfreundlichkeit bietet. Alle Apps, die bisher eine brokerbasierte Authentifizierung über die Microsoft Authenticator-App verwendet haben, können das einmalige Anmelden mit dem [Microsoft Enterprise SSO-Plug-In für Apple-Geräte](https://docs.microsoft.com/azure/active-directory/develop/apple-sso-plugin) weiterhin nutzen.

    > [!IMPORTANT]
    > Um einmaliges Anmelden mit dem SSO-App-Erweiterungstyp von Microsoft Azure AD zu erreichen, installieren Sie zuerst die iOS-/iPadOS-Microsoft Authenticator-App auf dem Gerät. Die Authenticator-App bietet das Microsoft Enterprise SSO-Plug-In für Geräte, und die Einstellungen der MDM SSO-App-Erweiterung aktivieren das Plug-In. Wenn Authenticator und das SSO-App-Erweiterungsprofil auf dem Gerät installiert sind, müssen die Benutzer ihre Anmeldeinformationen eingeben, um sich anzumelden und eine Sitzung auf ihren Geräten einzurichten. Diese Sitzung wird dann für verschiedene Anwendungen verwendet, ohne dass sich die Benutzer erneut authentifizieren müssen. Weitere Informationen zu Authenticator finden Sie unter [Wozu dient die Microsoft Authenticator-App?](https://docs.microsoft.com/azure/active-directory/user-help/user-help-auth-app-overview).

  - **Umleiten:** Verwenden Sie eine generische, anpassbare App-Erweiterung für die Umleitung, um das einmalige Anmelden (Single Sign-On, SSO) mit modernen Authentifizierungsflows zu nutzen. Stellen Sie sicher, dass Sie die Erweiterungs-ID für die App-Erweiterung Ihrer Organisation kennen.
  - **Anmeldeinformationen:** Verwenden Sie eine generische, anpassbare App-Erweiterung für Anmeldeinformationen, um das einmalige Anmelden mit Challenge-Response-Authentifizierungsflows zu nutzen. Stellen Sie sicher, dass Sie die Erweiterungs-ID für die App-Erweiterung Ihrer Organisation kennen.
  - **Kerberos**: Verwenden Sie die integrierte Kerberos-Erweiterung von Apple, die in iOS 13.0 und höher und iPadOS 13.0 und höher enthalten ist. Bei dieser Option handelt es sich um eine Kerberos-spezifische Version der App-Erweiterung vom Typ **Anmeldeinformationen**.

  > [!TIP]
  > Mit den Typen **Umleitung** und **Anmeldeinformationen** fügen Sie eigene Konfigurationswerte hinzu, die über die Erweiterung übergeben werden. Erwägen Sie bei Auswahl von **Anmeldeinformationen** die Verwendung integrierter Konfigurationseinstellungen, die von Apple für den Typ **Kerberos** bereitgestellt werden.

- **Freigabemodus für Geräte** (nur Microsoft Azure AD): Wählen Sie **Aktivieren** aus, wenn Sie das Microsoft Enterprise SSO-Plug-In auf iOS/iPadOS-Geräten bereitstellen, die für das Feature „Freigabemodus für Geräte“ von Azure AD konfiguriert sind. Geräte im Freigabemodus ermöglichen es vielen Benutzern, sich global bei Anwendungen, die den Freigabemodus für Geräte unterstützen, an- und abzumelden. Wenn die Einstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert. Standardmäßig sind iOS/iPadOS-Geräte nicht für die gemeinsame Nutzung durch mehrere Benutzer vorgesehen.

  Weitere Informationen über den Freigabemodus für Geräte und wie er aktiviert wird, finden Sie unter [Übersicht über den Freigabemodus für Geräte](https://docs.microsoft.com/azure/active-directory/develop/msal-shared-devices) und [Freigabemodus für iOS-Geräte](https://docs.microsoft.com/azure/active-directory/develop/msal-ios-shared-devices).  

- **Erweiterungs-ID** („Umleiten“ und „Anmeldeinformationen“): Geben Sie den Bundlebezeichner ein, der Ihre SSO-App-Erweiterung identifiziert, z. B. `com.apple.extensiblesso`.

- **Team-ID** („Umleiten“ und „Anmeldeinformationen“): Geben Sie den Teambezeichner Ihrer SSO-App-Erweiterung ein. Eine Team-ID ist eine aus 10 Zeichen bestehende alphanumerische (Ziffern und Buchstaben) Zeichenfolge, die von Apple generiert wird, z. B. `ABCDE12345`. Die Team-ID ist nicht erforderlich.

  Auf der [Seite zur Team-ID-Ermittlung](https://help.apple.com/developer-account/#/dev55c3c710c) (öffnet die Website von Apple) finden Sie weitere Informationen.

- **Bereich** („Anmeldeinformationen“ und „Kerberos“): Geben Sie den Namen Ihres Authentifizierungsbereichs ein. Der Bereichsname sollte groß geschrieben werden, z. B. `CONTOSO.COM`. In der Regel ist Ihr Bereichsname mit dem DNS-Domänennamen identisch, besteht aber nur aus Großbuchstaben.

- **Domänen** („Anmeldeinformationen“ und „Kerberos“): Geben Sie die Domänen- oder Hostnamen der Websites ein, auf denen eine Authentifizierung über SSO möglich ist. Wenn Ihre Website beispielsweise `mysite.contoso.com` lautet, ist `mysite` der Hostname und `contoso.com` der Domänenname. Wenn Benutzer eine Verbindung mit einer dieser Websites herstellen, verarbeitet die App-Erweiterung die Authentifizierung. Diese Authentifizierung ermöglicht es Benutzern Face ID, Touch ID oder eine PIN/einen Passcode von Apple für die Anmeldung zu verwenden.

  - Alle Domänen in den Intune-Profilen für Ihre SSO-App-Erweiterung müssen eindeutig sein. Sie können eine Domäne nicht mehrfach in einem SSO-App-Erweiterungsprofil verwenden – selbst dann nicht, wenn Sie verschiedene Arten von SSO-App-Erweiterungen verwenden.
  - Für diese Domänen erfolgt keine Beachtung der Groß-/Kleinschreibung.

- **URLs** (nur „Umleiten“): Geben Sie die URL-Präfixe der Identitätsanbieter ein, in deren Auftrag die Umleitungs-App-Erweiterung die SSO-Authentifizierung nutzt. Wenn Benutzer an diese URLs umgeleitet werden, greift die SSO-App-Erweiterung ein und fordert eine SSO-Authentifizierung an.

  - Alle URLs in Ihren Intune-SSO-Erweiterungsprofilen müssen eindeutig sein. Sie können eine Domäne nicht mehrfach in einem SSO-App-Erweiterungsprofil verwenden – selbst dann nicht, wenn Sie verschiedene Arten von SSO-App-Erweiterungen verwenden.
  - Die URLs müssen mit `http://` oder `https://` beginnen.

- **Zusätzliche Konfiguration** („Microsoft Azure AD“, „Umleiten“ und „Anmeldeinformationen“): Geben Sie zusätzliche erweiterungsspezifische Daten ein, die an die SSO-App-Erweiterung übergeben werden sollen:
  - **Schlüssel:** Geben Sie den Namen des Elements ein, das Sie hinzufügen möchten, z. B. `user name`.
  - **Typ:** Geben Sie den Datentyp ein. Folgende Optionen sind verfügbar:

    - Zeichenfolge
    - Boolean: Geben Sie unter **Konfigurationswert** entweder `True` oder `False` ein.
    - Integer: Geben Sie unter **Konfigurationswert** eine Zahl ein.

  - **Wert:** Geben Sie die Daten ein.

  - **Hinzufügen**: Tippen Sie auf diese Option, um Ihre Konfigurationsschlüssel hinzuzufügen.

- **Verwendung des Schlüsselbunds** (nur „Kerberos“): Die Einstellung **Blockieren** verhindert, dass Kennwörter im Schlüsselbund gespeichert werden. Wenn diese Option blockiert ist, werden Benutzer nicht aufgefordert, Ihr Kennwort zu speichern, sondern müssen es noch einmal eingeben, wenn das Kerberos-Ticket abläuft. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise das Speichern von Kennwörtern im Schlüsselbund zu. Benutzer werden nicht aufgefordert, Ihr Kennwort noch einmal einzugeben, wenn das Ticket abgelaufen ist.
- **Face ID, Touch ID, or passcode** (Face ID, Touch ID oder Passcode) (nur „Kerberos“): Bei der Option **Anfordern** werden Benutzer dazu gezwungen, ihre Face-ID, ihre Touch-ID oder ihren Gerätepasscode einzugeben, wenn die Anmeldeinformationen zum Aktualisieren des Kerberos-Tickets benötigt werden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig fordert das Betriebssystem möglicherweise nicht, dass Benutzer sich mit biometrischen Daten oder einem Gerätepasscode authentifizieren, um das Kerberos-Ticket zu aktualisieren. Wenn die Einstellung **Verwendung des Schlüsselbunds** blockiert ist, wird diese Einstellung nicht angewendet.
- **Default realm** (Standardbereich) (nur „Kerberos“): Mit **Aktivieren** wird der von Ihnen eingegebene **Bereich** als Standardbereich festgelegt. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig legt das Betriebssystem möglicherweise keinen Standardbereich fest.

  > [!TIP]
  > - **Aktivieren** Sie diese Einstellung, wenn Sie mehrere Kerberos-SSO-App-Erweiterungen in Ihrer Organisation konfigurieren.
  > - **Aktivieren** Sie diese Einstellung, wenn Sie mehrere Bereiche verwenden. Der von Ihnen eingegebene **Bereich** wird als Standardbereich festgelegt.
  > - Wenn Sie nur über einen Bereich verfügen, behalten Sie die Einstellung **Nicht konfiguriert** (Standardeinstellung) bei.

- **Prinzipalname** (nur „Kerberos“): Geben Sie den Benutzernamen des Kerberos-Prinzipals ein. Sie müssen den Bereichsnamen nicht einschließen. In `user@contoso.com` lautet der Prinzipalname beispielsweise `user`, und `contoso.com` ist der Bereichsname.

  > [!TIP]
  > - Sie können auch Variablen im Prinzipalnamen verwenden, indem Sie geschweifte Klammern `{{ }}` eingeben. Geben Sie z. B. `Username: {{username}}` ein, um den Benutzernamen anzuzeigen. 
  > - Verwenden Sie die Variablenersetzung jedoch mit Bedacht, da die Variablen in der Benutzeroberfläche nicht validiert werden und die Groß- und Kleinschreibung berücksichtigt wird. Stellen Sie sicher, dass die eingegebenen Informationen korrekt sind.

- **Active Directory site code** (Active Directory-Standortcode) (nur „Kerberos“): Geben Sie den Namen des Active Directory-Standorts ein, der von der Kerberos-Erweiterung verwendet werden soll. Möglicherweise müssen Sie diesen Wert nicht ändern, weil die Kerberos-Erweiterung den Active Directory-Standortcode ggf. automatisch ermittelt.
- **Cachename** (nur „Kerberos“): Geben Sie den Generic Security Services-Namen (GSS) für den Kerberos-Cache ein. Dieser Wert muss höchstwahrscheinlich nicht festgelegt werden.
- **App-Bundle-IDs** (nur „Kerberos“): Mit **Hinzufügen** werden die App-Bundle-IDs hinzugefügt, für die auf Ihren Geräten SSO verwendet werden soll. Diese Apps erhalten Zugriff auf das Kerberos-TGT (Ticket Granting Ticket) sowie das Authentifizierungsticket und authentifizieren Benutzer für Dienste, für die sie über Zugriffsberechtigungen verfügen.
- **Domänenbereichszuordnung** (nur „Kerberos“): Mit **Hinzufügen** werden die Domänen-DNS-Suffixe hinzugefügt, die Ihrem Bereich zugeordnet werden sollen. Verwenden Sie diese Einstellung, wenn die DNS-Namen der Hosts nicht mit dem Bereichsnamen identisch sind. Wahrscheinlich ist es nicht erforderlich, diese Zuordnung zwischen benutzerdefinierter Domäne und Bereich zu erstellen.
- **PKINIT-Zertifikat** (nur „Kerberos“): Mit **Auswählen** legen Sie das PKINIT-Zertifikat (Public Key Cryptography for Initial Authentication) fest, das für die Kerberos-Authentifizierung verwendet werden kann. Sie können aus [PKCS](../protect/certficates-pfx-configure.md)- oder [SCEP](../protect/certificates-scep-configure.md)-Zertifikaten auswählen, die Sie in Intune hinzugefügt haben. Weitere Informationen zu Zertifikaten finden Sie unter [Verwenden von Zertifikaten zur Authentifizierung in Microsoft Intune](../protect/certificates-configure.md).

## <a name="wallpaper"></a>Hintergrundbild

Möglicherweise kommt es zu unerwartetem Verhalten, wenn ein Profil ohne Bild einem Gerät mit einem Bild zugewiesen wird. Angenommen, Sie erstellen z.B. ein Profil ohne Bild. Dieses Profil wird dann Geräten zugewiesen, für die bereits Bilder vorhanden sind. In diesem Szenario ändert sich das Bild möglicherweise in den Gerätestandard, oder es wird weiter das ursprüngliche Bild auf dem Gerät verwendet. Dieses Verhalten wird von der MDM-Plattform von Apple kontrolliert und eingeschränkt.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Die Einstellungen gelten für: Automatisierte Geräteregistrierung (überwacht)

- **Position für die Anzeige des Hintergrundbilds**: Geben Sie einen Ort auf dem Gerät an, an dem das Bild angezeigt werden soll. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert:** Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Es wird kein benutzerdefiniertes Bild auf dem Gerät hinzugefügt. Standardmäßig legt das Betriebssystem möglicherweise selbst ein Bild fest.
  - **Sperrbildschirm**: Fügt das Bild zum Sperrbildschirm hinzu.
  - **Startbildschirm**: Fügt das Bild zum Startbildschirm hinzu.
  - **Sperrbildschirm und Startbildschirm**: Verwendet das gleiche Bild auf dem Sperr- und dem Startbildschirm.
- **Hintergrundbild**: Laden Sie ein vorhandenes PNG-, JPG- oder JPEG-Bild hoch, das Sie verwenden möchten. Achten Sie darauf, dass die Dateigröße kleiner als 750 KB ist. Sie können ein hinzugefügtes Bild auch **entfernen**.

> [!TIP]
> Um verschiedene Bilder auf dem Sperrbildschirm und dem Startbildschirm anzuzeigen, erstellen Sie ein Profil mit dem Sperrbildschirmbild. Erstellen Sie ein anderes Profil mit dem Startbildschirmbild. Fügen Sie beide Profile zu Ihren iOS/iPadOS-Benutzer- oder Gerätegruppen hinzu.

## <a name="next-steps"></a>Nächste Schritte

[Zuweisen von Profilen](device-profile-assign.md) und [Überwachen von Profilen](device-profile-monitor.md)

Sie können auch Gerätefunktionsprofile für [macOS](macos-device-features-settings.md)-Geräte erstellen.
