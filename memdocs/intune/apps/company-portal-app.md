---
title: Anpassen von Intune-Unternehmensportal-Apps, der Unternehmensportal-Website und der Intune-App
titleSuffix: Microsoft Intune
description: Erfahren Sie, wie Sie unternehmensspezifisches Branding auf die Intune-Unternehmensportal-Apps, die Unternehmensportal-Website und die Intune-App anwenden können.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/12/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: dec6f258-ee1b-4824-bf66-29053051a1ae
ms.reviewer: esthermsft
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: a82fbfa9e494828450729e29467580c29a590282
ms.sourcegitcommit: d1bfd5b8481439babc7eae43493f28edaebe647a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/13/2020
ms.locfileid: "88179552"
---
# <a name="how-to-customize-the-intune-company-portal-apps-company-portal-website-and-intune-app"></a>Anpassen von Intune-Unternehmensportal-Apps, der Unternehmensportal-Website und der Intune-App

In den Unternehmensportal-Apps, auf der Unternehmensportal-Website und in der Intune-App unter Android greifen Benutzer auf Unternehmensdaten zu und können häufig anfallende Aufgaben ausführen. Zu den häufigen Aufgaben gehören das Registrieren von Geräten, das Installieren von Apps und die Suche nach Informationen (beispielsweise zur Unterstützung durch Ihre IT-Abteilung). Darüber hinaus können Benutzer an diesen Stellen sicher auf Unternehmensressourcen zugreifen. Die Oberfläche für Endbenutzer bietet verschiedene Seiten, z. B. „Startseite“, „Apps“, „App-Details“, „Geräte“ und „Gerätedetails“. Um Apps im Unternehmensportal schnell zu finden, können Sie die Apps auf der Seite „Apps“ filtern.

## <a name="customizing-the-user-experience"></a>Anpassen der Benutzeroberfläche

Durch Anpassen der Oberflächenoptionen können Sie Ihren Endbenutzern eine vertraute und hilfreiche Benutzeroberfläche bereitstellen. Navigieren Sie dazu zum [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431), und wählen Sie **Mandantenverwaltung** > **Anpassung** aus, wo Sie entweder die Standardrichtlinie bearbeiten oder bis zu zehn gruppenorientierte Richtlinien erstellen können. Diese Einstellungen gelten für die Unternehmensportal-Apps, die Unternehmensportal-Website und die Intune-App unter Android.

## <a name="branding"></a>Branding

In der folgenden Tabelle finden Sie Details zur Anpassung des Brandings für die Oberfläche für Endbenutzer:

| Feldname | Weitere Informationen |
|---|---|---|
| **Name der Organisation** | Dieser Name wird im gesamten Messaging auf der Oberfläche für Endbenutzer angezeigt. Über die Einstellung **In Kopfzeile anzeigen** kann der Name auch in Kopfzeilen angezeigt werden. Die maximale Länge beträgt 40 Zeichen. |
| **Farbe** | Über die Option **Standard** stehen fünf Standardfarben zur Auswahl. Über die Option **Benutzerdefiniert** können Sie eine bestimmte Farbe anhand eines Hexadezimalwerts auswählen. |
| **Farbdesign** | Legen Sie das Farbdesign fest, das auf der gesamten Oberfläche für Endbenutzer angezeigt werden soll. Die Textfarbe wird automatisch auf Schwarz oder Weiß festgelegt, dass sie auf der ausgewählten Designfarbe möglichst gut sichtbar ist. |
| **In Kopfzeile anzeigen** | Wählen Sie aus, ob in Kopfzeilen der Benutzeroberfläche das **Organisationslogo und der Organisationsname**, **nur das Organisationslogo**  oder **nur der Organisationsname** angezeigt werden soll. Die Vorschaufelder unten zeigen nur die Logos, nicht den Namen.  |
| **Logo für Hintergrund in Designfarbe hochladen** | Laden Sie das Logo hoch, das Sie auf der ausgewählten Designfarbe anzeigen möchten. Um eine optimale Darstellung zu erzielen, laden Sie ein Logo mit transparentem Hintergrund hoch. Im Vorschaufeld unterhalb der Einstellung können Sie die Darstellung sehen.<p>Maximale Bildgröße: 400 × 400 px<br>Maximale Dateigröße:   750 KB<br>Dateityp: PNG, JPG oder JPEG |
| **Logo für weißen oder hellen Hintergrund hochladen** | Laden Sie das Logo hoch, das Sie vor weißen oder hellen Hintergründen anzeigen möchten. Um eine optimale Darstellung zu erzielen, laden Sie ein Logo mit transparentem Hintergrund hoch. Im Vorschaufeld unterhalb der Einstellung können Sie die Darstellung vor einem weißen Hintergrund sehen.<p>Maximale Bildgröße: 400 × 400 px<br>Maximale Dateigröße: 750 KB<br>Dateityp: PNG, JPG oder JPEG |
| **Markenimage hochladen** | Laden Sie ein Bild hoch, das für die Marke Ihrer Organisation steht.<p><ul><li>Empfohlene Bildbreite: Größer als 1125 px (mindestens 650 px)</li><li>Maximale Bildgröße: 1,3 MB</li><li>Dateityp: PNG, JPG oder JPEG</li><li>Das Logo wird an folgenden Stellen angezeigt:</li><ul><li>iOS/iPadOS-Unternehmensportal: Hintergrundbild auf der Profilseite des Benutzers.</li><li>Unternehmensportal-Website:   Hintergrundbild auf der Profilseite des Benutzers</li><li>Android-Intune-App: Im Drawer und als Hintergrundbild auf der Profilseite des Benutzers</li></ul></ul> |

> [!NOTE]
> Wenn ein Benutzer eine iOS/iPadOS-Anwendung über das Unternehmensportal installiert, wird eine Eingabeaufforderung angezeigt. Dies passiert, wenn die iOS/iPadOS-App mit dem App-Store, einem Volumenlizenzprogramm (Volume-Purchase Program, VPP) oder einer branchenspezifischen App (Line-Of-Business, LOB) verknüpft ist. In der Eingabeaufforderung kann der Benutzer die Aktion akzeptieren oder die Verwaltung der App erlauben. Die Eingabeaufforderung zeigt den Namen Ihres Unternehmens oder – wenn dieser nicht verfügbar ist – den Text **Unternehmensportal** an.

### <a name="brand-image-best-practices"></a>Best Practices für Markenbilder

Ein geeignetes Markenbild trägt zum Vertrauen der Benutzer bei, da die Identität Ihrer Organisation aussagekräftig dargestellt wird. Im Folgenden finden Sie einige Tipps, die Sie beim Erwerben, Auswählen und Optimieren des Bilds für die verschiedenen Anzeigeorte beachten sollten.

- Wenden Sie sich an Ihre Marketing- oder Designabteilung. Möglicherweise verfügt sie bereits über zulässige Markenbilder. Eventuell können sie Sie bei Bedarf auch beim Optimieren der Bilder unterstützen.
- Beachten Sie die Komposition sowohl im Querformat als auch im Hochformat. Das Bild sollte ausreichend Hintergrundfläche um den Fokus herum aufweisen. Das Bild wird möglicherweise je nach Größe, Ausrichtung und Plattform des Geräts anders zugeschnitten.
- Vermeiden Sie typische Archivbilder. Das Bild sollte die Marke Ihrer Organisation widerspiegeln und für Benutzer vertraut wirken. Wenn Sie keines besitzen, ist es besser, keines zu verwenden, anstatt ein allgemeines Bild zu nutzen, das keine Bedeutung für Ihre Benutzer hat.
- Entfernen Sie unnötige Metadaten. Bilddateien können Metadaten enthalten, z.B. das Kameraprofil, der geografische Standort, Titel, Beschreibung usw. Verwenden Sie ein Bildbearbeitungstool, um diese Informationen zu entfernen, die Qualität beizubehalten und die maximale Dateigröße einzuhalten.

### <a name="brand-image-examples"></a>Beispiele für Markenbilder

Die folgende Abbildung zeigt ein Beispiel des Markenbilds auf einem iPhone:

<img alt="Screenshot of example iPhone branding image" src="./media/company-portal-app/company-portal-app-01.png" width="250">

Die folgende Abbildung zeigt ein Beispiel des Markenbilds in der Intune-App für Android:

<img alt="Screenshot of example #1 for Intune app for Android branding image" src="./media/company-portal-app/company-portal-app-02.png" width="250">

<img alt="Screenshot of example #2 for Intune app for Android branding image" src="./media/company-portal-app/company-portal-app-03.png" width="250">

## <a name="support-information"></a>Supportinformationen

Geben Sie die Supportinformationen Ihrer Organisation ein, sodass Mitarbeiter ganz einfach Fragen stellen können. Die Supportinformationen werden auf der gesamten Oberfläche für Endbenutzer auf den Seiten **Support**, **Hilfe und Support** und **Helpdesk** angezeigt.

| Feldname | Maximale Länge | Weitere Informationen |
|------------------------|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Kontaktname | 40 | Wenn Benutzer sich an den Support wenden, erreichen sie die Kontaktperson mit diesem Namen. |
| Telefonnummer | 20 | Unter dieser Nummer können Benutzer Support anfordern. |
| E-Mail-Adresse | 40 | An diese E-Mail-Adresse können Benutzer Supportanfragen senden. Sie müssen eine gültige E-Mail-Adresse im Format `alias@domainname.com` eingeben. |
| Name der Website | 40 | Dies ist der Anzeigename der URL für die Supportwebsite, der an einige Stellen angezeigt wird. Wenn Sie keinen Anzeigenamen, sondern nur eine URL für die Supportwebsite angeben, wird die URL selbst auf der Oberfläche für Endbenutzer angezeigt.  |
| Website-URL | 150 | Die Supportwebsite, die Benutzer verwenden sollen. Die URL muss im Format `https://www.contoso.com` vorliegen.  |
| Zusätzliche Informationen | 120 | Geben Sie hier weitere Informationen zum Support für Benutzer an. |

## <a name="configuration"></a>Konfiguration

Sie können die Benutzeroberfläche des Unternehmensportals speziell für die Registrierung, den Datenschutz, Benachrichtigungen, App-Quellen und Self-Service-Aktionen konfigurieren.

### <a name="enrollment"></a>Anmeldung

Die folgende Tabelle enthält registrierungsspezifische Konfigurationsinformationen:

| Feldname | Maximale Länge | Weitere Informationen |
|------------------------------------------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Geräteregistrierung | N/V | Hier geben Sie an, ob und wie Benutzer aufgefordert werden sollen, sich für die mobile Geräteverwaltung zu registrieren. Weitere Informationen finden Sie unter [Optionen für die Einstellung „Geräteregistrierung“](../apps/company-portal-app.md#device-enrollment-setting-options). |

#### <a name="device-enrollment-setting-options"></a>Optionen für die Einstellung „Geräteregistrierung“

> [!NOTE]
> Damit die Einstellung „Geräteregistrierung“ unterstützt wird, müssen Endbenutzer über eine der folgenden Unternehmensportalversionen verfügen:
> - Unternehmensportal unter iOS/iPadOS: Version 4.4 oder höher
> - Unternehmensportal unter Android: Version 5.0.4715.0 oder höher 

> [!IMPORTANT]
> Die folgenden Einstellungen gelten nicht für iOS-/iPadOS-Geräte, die dafür konfiguriert sind, sich über die [automatische Geräteregistrierung](../enrollment/device-enrollment-program-enroll-ios.md) zu registrieren. Unabhängig von dieser Einstellung werden iOS-/iPadOS-Geräte, die sich ihrer Konfiguration gemäß über die automatische Geräteregistrierung registrieren, während des Willkommensflows registriert. Die Benutzer werden beim Start des Unternehmensportals aufgefordert, sich anzumelden.
> 
> Die folgenden Einstellungen gelten für Android-Geräte, die mit [Samsung Knox Mobile Enrollment](../enrollment/android-samsung-knox-mobile-enroll.md) (KME) konfiguriert sind. Wenn ein Gerät für KME konfiguriert wurde und die Geräteregistrierung auf „Nicht verfügbar“ festgelegt ist, kann das Gerät nicht während des Standardablaufs registriert werden.

|    Optionen für die Geräteregistrierung    |    Beschreibung    |    Eingabeaufforderungen als Prüfliste    |    Benachrichtigung    |    Gerätedetailstatus    |    App-Detailstatus (einer App, die eine Registrierung erfordert)    |
|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------|-------------------------|--------------------|-----------------------------|--------------------------------------------------------------------|
|    Verfügbar, mit Eingabeaufforderungen    |    Die Standardeinstellung mit Eingabeaufforderungen zur Registrierung bei allen möglichen Speicherorten.    |    Ja    |    Ja    |    Ja    |    Ja    |
|    Verfügbar, keine Eingabeaufforderungen    |    Benutzer können sich über den Status in den Gerätedetails für ihr aktuelles Gerät oder über Apps registrieren, die eine Registrierung erfordern.    |    Nein    |    Nein    |    Ja    |    Ja    |
|    Nicht verfügbar    |    Benutzer können sich nicht registrieren.    |    Nein    |    Nein    |    Nein    |    Nein    |

### <a name="privacy"></a>Datenschutz

Die folgende Tabelle enthält datenschutzspezifische Konfigurationsinformationen:

| Feldname | Maximale Länge | Weitere Informationen |
|------------------------------------------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| URL zur Datenschutzerklärung | 79 | Legen Sie fest, dass die Datenschutzerklärung Ihrer Organisation angezeigt wird, wenn Benutzer auf entsprechende Links klicken. Sie müssen eine gültige URL im Format `https://www.contoso.com` eingeben. |
| Datenschutzmeldung im Unternehmensportal für iOS/iPadOS | 520 | Behalten Sie die **Standardeinstellung** bei, oder legen Sie eine **benutzerdefinierte** Nachricht fest, um die Elemente aufzulisten, die in Ihrer Organisation nicht auf verwalteten iOS-/iPadOS-Geräten angezeigt werden dürfen. Mithilfe von Markdown können Sie Aufzählungspunkte, Fett- und Kursivformatierung sowie Links hinzufügen. Benutzern wird außerdem eine Liste der Elemente und Aktionen angezeigt, die in Ihrer Organisation aufgerufen und ausgeführt werden dürfen. Diese Liste wird jedoch automatisch von Intune generiert und ist nicht anpassbar. |

### <a name="device-ownership-notification"></a>Benachrichtigung über Gerätebesitz

Die folgende Tabelle enthält benachrichtigungsspezifische Konfigurationsinformationen:

| Feldname | Maximale Länge | Weitere Informationen |
|------------------------------------------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Pushbenachrichtigung an Benutzer senden, wenn sich der Besitztyp des Geräts von „Persönlich“ in „Unternehmen“ ändert (nur Android und iOS/iPadOS) | N/V | Senden Sie eine Pushbenachrichtigung an Ihre Android- und iOS-Unternehmensportalbenutzer, wenn ihr Gerätebesitzertyp von „Persönlich“ in „Unternehmen“ geändert wird. Diese Pushbenachrichtigung ist standardmäßig deaktiviert. Wenn der Gerätebesitz auf „Unternehmen“ festgelegt wird, hat Intune einen umfassenderen Zugriff auf das Gerät, einschließlich des vollständigen App-Inventars, der FileVault-Schlüsselrotation, des Abrufs von Rufnummern und einiger ausgewählter Remoteaktionen. Weitere Informationen finden Sie unter [Ändern des Gerätebesitzes](../enrollment/corporate-identifiers-add.md#change-device-ownership).  |

### <a name="app-sources"></a>App-Quellen

Sie können auswählen, welche zusätzlichen App-Quellen im Unternehmensportal angezeigt werden. Die folgende Tabelle enthält spezifische Konfigurationsinformationen zur App-Quelle:

| Feldname | Maximale Länge | Weitere Informationen |
|------------------------------------------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Azure AD-Unternehmensanwendungen | N/V | Klicken Sie auf **Ausblenden** oder **Zeigen**, damit **Azure AD-Unternehmensanwendungen** jedem Endbenutzer im Unternehmensportal angezeigt werden. Weitere Informationen finden Sie unter [Einstellungsoptionen für App-Quellen](../apps/company-portal-app.md#app-source-setting-options). |
| Office Online-Anwendungen | N/V | Klicken Sie auf **Ausblenden** oder **Anzeigen**, damit **Office Online-Anwendungen** jedem Endbenutzer im Unternehmensportal angezeigt werden. Weitere Informationen finden Sie unter [Einstellungsoptionen für App-Quellen](../apps/company-portal-app.md#app-source-setting-options). |

#### <a name="app-source-setting-options"></a>Einstellungsoptionen für App-Quellen

> [!NOTE]
> Auf der Website des Unternehmensportals werden initial Apps aus anderen Microsoft-Diensten angezeigt.

Sie können **Azure AD-Unternehmensanwendungen** und **Office Online-Anwendungen** für alle Endbenutzer im Unternehmensportal ausblenden oder anzeigen lassen. Wenn Sie auf **Anzeigen** klicken, wird der gesamte Anwendungskatalog aus den ausgewählten, dem Benutzer zugewiesenen Microsoft-Diensten im Unternehmensportal anzeigt. **Azure AD-Unternehmensanwendungen** werden über das [Azure-Portal](https://portal.azure.com) registriert und zugewiesen. **Office Online-Anwendungen** werden mithilfe der im [M365-Admin Center](https://admin.microsoft.com) verfügbaren Steuerfunktionen für die Lizenzierung zugewiesen. Diese Konfigurationseinstellung finden Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) unter **Mandantenverwaltung** > **Anpassung**. Standardmäßig wird jede zusätzliche App auf **Ausblenden** festgelegt. 

### <a name="customizing-user-self-service-actions-for-the-company-portal"></a>Anpassen von Self-Service-Geräteaktionen für Benutzer im Unternehmensportal

Sie können die verfügbaren Self-Service-Geräteaktionen anpassen, die Endbenutzern in der App und auf der Website des Unternehmensportals angezeigt werden. Damit nicht beabsichtigte Geräteaktionen vermieden werden, können Sie Einstellungen für die Unternehmensportal-App konfigurieren. Klicken Sie dazu auf **Mandantenverwaltung** > **Anpassung**. 

Die folgenden Aktionen sind verfügbar:
- Schaltfläche **Entfernen** auf unternehmenseigenen Windows-Geräten ausblenden
- Schaltfläche **Zurücksetzen** auf unternehmenseigenen Windows-Geräten ausblenden
- Schaltfläche **Entfernen** auf unternehmenseigenen iOS-/iPadOS-Geräten ausblenden
- Schaltfläche **Zurücksetzen** auf unternehmenseigenen iOS-/iPadOS-Geräten ausblenden

> [!NOTE]
> Mit diesen Aktionen lassen sich Geräteaktionen in der App und auf der Website des Unternehmensportals einschränken. Damit werden jedoch keine Richtlinien zur Einschränkung von Geräten implementiert. Damit Benutzer ihre Geräte nicht über die Einstellungen auf die Werkseinstellungen zurücksetzen oder die mobile Geräteverwaltung entfernen, müssen Sie Richtlinien für Geräteeinschränkungen konfigurieren. 

## <a name="opening-web-company-portal-applications"></a>Öffnen von Anwendungen des Webunternehmensportals
Bei Anwendungen des Webunternehmensportals wird Endbenutzern, wenn sie die Unternehmensportalanwendung installiert haben, ein Dialogfeld mit der Frage angezeigt, wie die Anwendung außerhalb des Browsers geöffnet werden soll. Wenn die App nicht im Pfad des Unternehmensportals enthalten ist, öffnet das Unternehmensportal die Homepage. Andernfalls öffnet das Unternehmensportal die entsprechende App. 

Nachdem der Benutzer das Unternehmensportal ausgewählt hat, wird er zur entsprechenden Seite in der Anwendung weitergeleitet, wenn der URI-Pfad einer der folgenden ist:

- `/apps`: Das Webunternehmensportal öffnet die Seite „Apps“, auf der alle Apps aufgelistet sind.
- `/apps/[appID]`: Das Webunternehmensportal öffnet die Seite „Details“ in der entsprechenden App.
- *Der URI-Pfad lautet anders oder ist unerwartet:* Die Startseite des Webunternehmensportals wird angezeigt.

Wenn der Benutzer die Unternehmensportal-App nicht installiert hat, wird der Benutzer zum Webunternehmensportal weitergeleitet.

## <a name="company-portal-derived-credentials-for-iosipados-devices"></a>Vom Unternehmensportal abgeleitete Anmeldeinformationen für iOS/iPadOS-Geräte

Intune unterstützt von Personal Identity Verification (PIV) und Common Access Card (CAC) abgeleitete Anmeldeinformationen in Partnerschaft mit den Anmeldeinformationsanbietern DISA Purebred, Entrust Datacard und Intercede. Endbenutzer durchlaufen nach der Registrierung ihres iOS/iPadOS-Geräts weitere Schritte, um ihre Identität in der Unternehmensportalanwendung zu bestätigen. Abgeleitete Anmeldeinformationen werden für Benutzer aktiviert, indem zuerst ein Anmeldeinformationsanbieter für Ihren Mandanten eingerichtet und dann ein Profil als Ziel verwendet wird, das abgeleitete Anmeldeinformationen für Benutzer oder Geräte verwendet.

> [!NOTE]
> Der Benutzer erhält Anweisungen zu abgeleiteten Anmeldeinformationen, die auf dem Link basieren, den Sie über Intune angegeben haben.

Weitere Informationen zu abgeleiteten Anmeldeinformationen für iOS/iPadOS-Geräte finden Sie unter [Verwenden abgeleiteter Anmeldeinformationen in Microsoft Intune](../protect/derived-credentials.md).

## <a name="dark-mode-for-the-company-portal"></a>Dunkler Modus für das Unternehmensportal

Der dunkle Modus ist für das Unternehmensportal für iOS/iPadOS, macOS und Windows verfügbar. Benutzer können im Farbschema ihrer Wahl – basierend auf den Geräteeinstellungen – Apps herunterladen, ihre Geräte verwalten und IT-Support erhalten. Das Unternehmensportal für iOS/iPadOS, macOS und Windows passt sich automatisch den Einstellungen des Endbenutzergeräts für den hellen oder dunklen Modus an.

## <a name="windows-company-portal-keyboard-shortcuts"></a>Tastenkombinationen für die Windows-Unternehmensportal-App

Endbenutzer können mithilfe von Tastenkombinationen (Tastenkombinations-Editor) Navigations-, App- und Geräteaktionen in der Windows-Unternehmensportal-App auslösen.

Die folgenden Tastenkombinationen stehen Ihnen in der Windows-Unternehmensportal-App zur Verfügung.

| Bereich | Beschreibung | Tastenkombination |
|--------------------|----------------|-------------------|
| Navigationsmenü | Navigation | ALT+M |
|  | -Startseite | ALT+H |
|  | Alle Apps | Alt+A |
|  | Installierte Apps | ALT+I |
|  | Senden von Feedback | ALT+F |
|  | Mein Profil | ALT+U |
|  | Einstellung | Alt+T |
| Start – Gerätekachel | Umbenennen | F2 |
|  | Entfernen | STRG+D oder ENTF-TASTE |
|  | Zugriff prüfen | STRG+M oder F9 |
| Gerätedetails | Umbenennen | F2 |
|  | Entfernen | STRG+D oder ENTF-TASTE |
|  | Zugriff prüfen | STRG+M oder F9 |
| App-Details | Installation | STRG+I |
| Geräte | Verfügbar | Strg+D |

Endbenutzer können zudem die verfügbaren Tastenkombinationen in der Windows-Unternehmensportal-App einsehen.

![Screenshot der verfügbaren Tastenkombinationen im Windows-Unternehmensportal](./media/company-portal-app/company-portal-app-04.png)

## <a name="user-self-service-device-actions-from-the-company-portal"></a>Self-Service-Geräteaktionen für Benutzer im Unternehmensportal

Benutzer können über die Unternehmensportal-App, die Website des Unternehmensportals oder die Intune-App unter Android Aktionen auf ihren lokalen Geräten oder Remotegeräten ausführen. Die von Benutzern ausführbaren Aktionen variieren je nach Geräteplattform und -konfiguration. In allen Fällen können Remotegeräteaktionen nur vom primären Benutzer eines Geräts ausgeführt werden.  

Die folgenden Aktionen sind Beispiele für verfügbare Self-Service-Geräteaktionen:

- **Außerbetriebnahme**: Entfernt das Gerät aus der Intune-Verwaltung. In der Unternehmensportal-App und der Unternehmensportal-Website wird dies als **Entfernen** angezeigt.
- **Zurücksetzen**: Diese Aktion initiiert eine Rücksetzung des Geräts. In der Unternehmensportal-Website wird dies als **Zurücksetzen** angezeigt, in der iOS/iPadOS-Unternehmensportal-App als **Auf Werkseinstellungen zurücksetzen**.
- **Umbenennen**: Diese Aktion ändert den Gerätenamen, der dem Benutzer im Unternehmensportal angezeigt wird. Diese Aktion ändert nur die Liste im Unternehmensportal, nicht den lokalen Gerätenamen.
- **Synchronisieren**: Diese Aktion initiiert das Check-In eines Geräts beim Intune-Dienst. Diese Aktion wird im Unternehmensportal als **Status überprüfen** angezeigt.
- **Remotesperre**: Diese Aktion sperrt das Gerät und erfordert eine PIN zum Entsperren.
- **Passcode zurücksetzen**: Diese Aktion wird zum Zurücksetzen des Passcodes eines Geräts verwendet. Auf iOS/iPadOS-Geräten wird der Passcode entfernt, und der Endbenutzer muss in den Einstellungen einen neuen Code eingeben. Auf unterstützten Android-Geräten wird ein neuer Passcode von Intune generiert und temporär im Unternehmensportal angezeigt.
- **Schlüsselwiederherstellung**: Diese Aktion wird verwendet, um einen persönlichen Wiederherstellungsschlüssel für verschlüsselte macOS-Geräte von der Unternehmensportalwebsite wiederherzustellen. 

Informationen zum Anpassen der verfügbaren Self-Service-Benutzeraktionen finden Sie unter [Anpassen von Self-Service-Geräteaktionen für Benutzer im Unternehmensportal](../apps/company-portal-app.md#customizing-user-self-service-actions-for-the-company-portal).

### <a name="self-service-actions"></a>Self-Service-Aktionen

Einige Plattformen und Konfigurationen lassen keine Self-Service-Geräteaktionen zu. In der folgenden Tabelle finden Sie weitere Informationen zu Self-Service-Aktionen:

| Aktion | Windows 10<sup>(3)</sup> | iOS/iPadOS<sup>(3)</sup> | macOS<sup>(3)</sup> | Android<sup>(3)</sup> |
|----------------------|--------------------------|-------------------|-----------------------------------|-------------------------|
| Außerkraftsetzen | Verfügbar<sup>(1)</sup> | Verfügbar<sup>(9)</sup> | Verfügbar | Verfügbar<sup>(7)</sup> |
| Zurücksetzen | Verfügbar | Verfügbar<sup>(5)</sup><sup>(9)</sup> | N/V | Verfügbar<sup>(7)</sup> |
| Umbenennen<sup>(4)</sup> | Verfügbar | Verfügbar | Verfügbar | Verfügbar |
| Sync | Verfügbar | Verfügbar | Verfügbar | Verfügbar |
| Schlüsselwiederherstellung | Nicht verfügbar | Nicht verfügbar | Verfügbar<sup>(2)</sup> | N/V |

<sup>(1)</sup> Die **Außerbetriebnahme** ist auf Windows-Geräten, die Azure AD beigetreten sind, immer blockiert.<br>
<sup>(2)</sup> Die **Schlüsselwiederherstellung** für macOS ist nur über das Webportal verfügbar.<br>
<sup>(3)</sup> Bei Verwendung einer Registrierung über den Geräteregistrierungs-Manager sind alle Remoteaktionen deaktiviert.<br>
<sup>(4)</sup> Durch **Umbenennen** wird nur der Gerätename in der Unternehmensportal-App oder im Webportal geändert, nicht auf dem Gerät selbst.<br>
<sup>(5)</sup>**Löschen** ist auf iOS/iPadOS-Geräten, die vom Benutzer registriert werden, nicht verfügbar.<br>
<sup>(6)</sup> Das **Zurücksetzen von Passcodes** wird in einigen Android- und Android Enterprise-Konfigurationen nicht unterstützt. Weitere Informationen finden Sie unter [Zurücksetzen oder Entfernen eines Gerätepasscodes in Intune](../remote-actions/device-passcode-reset.md).<br>
<sup>(7)</sup> Aktionen für **Außerbetriebnahme** und **Zurücksetzen** sind in Szenarios mit Android Enterprise-Gerätebesitzern (COPE, COBO, COSU) nicht verfügbar.<br>
<sup>(8)</sup> **Passcode zurücksetzen** wird auf von Benutzern registrierten iOS/iPadOS-Geräten nicht unterstützt.<br>
<sup>(9)</sup> Die Optionen **Zurückziehen** und **Zurücksetzen** sind auf allen iOS-/iPadOS-Geräten deaktiviert, die für die automatische Geräteregistrierung (früher „DEP“) konfiguriert sind.

### <a name="app-logs"></a>App-Protokolle

Wenn Sie Azure Government verwenden, werden dem Endbenutzer App-Protokolle angeboten. Er kann nun entscheiden, wie er diese teilen möchte, wenn der er den Prozess zum Abrufen von Hilfe zu einem Problem startet. Wird Azure Government jedoch nicht verwendet, sendet das Unternehmensportal App-Protokolle direkt an Microsoft, wenn der Benutzer den Prozess zum Anfordern von Hilfe zu einem Problem startet. Das Senden der App-Protokolle an Microsoft erleichtert die Problembehandlung und -behebung.

> [!NOTE]
> In Übereinstimmung mit den Richtlinien von Microsoft und Apple werden die von unserem Dienst gesammelten Daten keinesfalls an Dritte verkauft.

## <a name="next-steps"></a>Nächste Schritte

- [Konfigurieren des Logos und der Markenfarbe Ihrer Organisation für neue Registerkartenseiten in Microsoft Edge](manage-microsoft-edge.md#organization-logo-and-brand-color)
- [Hinzufügen von Apps](apps-add.md)
