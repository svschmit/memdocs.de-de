---
title: Verwalten von Microsoft Edge für iOS und Android mit Intune
titleSuffix: ''
description: Nutzen Sie die Intune-App-Schutz- und Konfigurationsrichtlinien mit Microsoft Edge für iOS und Android, um sicherzustellen, dass der Zugriff auf Unternehmenswebsites stets mit entsprechenden Sicherheitsvorkehrungen erfolgt.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/03/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3fb2f050-ec94-42ab-be05-c3d4101148bb
ms.reviewer: ilwu
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9391be828452cbda25dd6c4f4ed75cffa2ef687c
ms.sourcegitcommit: b95eac00a0cd979dc88be953623c51dbdc9327c5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/03/2020
ms.locfileid: "89423746"
---
# <a name="manage-web-access-by-using-edge-for-ios-and-android-with-microsoft-intune"></a>Verwalten des Webzugriffs mithilfe von Microsoft Edge für iOS und Android mit Microsoft Intune

Microsoft Edge für iOS und Android ist so konzipiert, dass Benutzer im Web browsen können, und unterstützt mehrere Identitäten. Benutzer können sowohl Geschäftskonten als auch persönliche Konten zum Browsen hinzufügen. Es besteht eine vollständige Trennung beider Identitäten, wie sie auch in anderen mobilen Apps von Microsoft geboten wird.

Microsoft Edge für iOS wird ab iOS 12.0 unterstützt. Microsoft Edge für Android wird ab Android 5 unterstützt.

> [!NOTE]
> Für Microsoft Edge für iOS und Android gelten keine Einstellungen, die Benutzer für den nativen Browser auf ihren Geräten festlegen, da Edge für iOS und Android auf diese Einstellungen nicht zugreifen kann.

Die vielfältigsten und umfangreichsten Schutzfunktionen für Microsoft 365-Daten sind verfügbar, wenn Sie die Enterprise Mobility + Security-Suite abonnieren, die Microsoft Intune und Azure Active Directory Premium-Features wie bedingten Zugriff bietet. Zumindest sollten Sie eine Richtlinie für bedingten Zugriff bereitstellen, die nur die Konnektivität mit Microsoft Edge für iOS und Android auf mobilen Geräten zulässt, sowie eine Intune-App-Schutzrichtlinie, die gewährleistet, dass die Browserumgebung geschützt ist.

> [!NOTE]
> Neue Webclips (angeheftete Web-Apps) auf iOS-Geräten werden in Microsoft Edge für iOS und Android statt in Intune Managed Browser geöffnet, wenn das Öffnen in einem geschützten Browser erforderlich ist. Ältere iOS-Webclips müssen neu zugewiesen werden, um sicherzustellen, dass sie in Microsoft Edge für iOS und Android statt in Managed Browser geöffnet werden.

## <a name="apply-conditional-access"></a>Aktivieren des bedingten Zugriff
Organisationen können Richtlinien für bedingten Zugriff von Azure AD nutzen, um sicherzustellen, dass Benutzer nur mit Microsoft Edge für iOS und Android auf Geschäfts-, Schul- oder Uni-Inhalte zugreifen können. Dazu benötigen Sie eine Richtlinie für bedingten Zugriff, die für alle potenziellen Benutzer gilt. Einzelheiten zur Erstellung dieser Richtlinie finden Sie unter [Erzwingen einer App-Schutzrichtlinie für den Cloud-App-Zugriff mit bedingtem Zugriff](/azure/active-directory/conditional-access/app-protection-based-conditional-access).

1. Befolgen Sie die Anweisungen unter [Szenario 2: Browser-Apps erfordern genehmigte Apps mit App-Schutzrichtlinien.](/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-2-browser-apps-require-approved-apps-with-app-protection-policies) So kann Microsoft Edge für iOS und Android zugelassen werden, aber andere Webbrowser werden auf dem Mobilgerät daran gehindert, eine Verbindung mit Office 365-Endpunkten herzustellen.

   >[!NOTE]
   > Diese Richtlinie stellt sicher, dass mobile Benutzer in Microsoft Edge für iOS und Android auf alle Microsoft 365-Endpunkte zugreifen können. Diese Richtlinie verhindert auch, dass Benutzer die Einstellung InPrivate für den Zugriff auf Microsoft 365-Endpunkte nutzen können.

Mit bedingtem Zugriff können Sie auch auf lokale Websites zugreifen, die Sie externen Benutzern über den [Microsoft Azure AD-Anwendungsproxy](/azure/active-directory/active-directory-application-proxy-get-started) zur Verfügung gestellt haben.

## <a name="create-intune-app-protection-policies"></a>Erstellen von Intune-App-Schutzrichtlinien

App-Schutzrichtlinien legen fest, welche Apps zulässig sind und welche Aktionen sie auf die Daten Ihres Unternehmens anwenden dürfen. Die in den App-Schutzrichtlinien verfügbaren Optionen ermöglichen Organisationen, den Schutz an ihre speziellen Anforderungen anzupassen. In einigen Situationen ist es jedoch möglicherweise nicht offensichtlich, welche Richtlinieneinstellungen genau erforderlich sind, um ein vollständiges Szenario zu implementieren. Um Unternehmen bei der Priorisierung der Absicherung mobiler Clientendpunkte zu unterstützen, hat Microsoft für die Verwaltung mobiler iOS- und Android-Apps eine Taxonomie für sein Datenschutzframework für App-Schutzrichtlinien eingeführt.

Dieses Datenschutzframework ist in drei Konfigurationsebenen unterteilt, wobei jede Ebene auf der vorherigen Ebene aufbaut:

- **Einfacher Datenschutz für Unternehmen** (Ebene 1): Diese Ebene stellt sicher, dass Apps mit einer PIN geschützt und verschlüsselt sind, und dient zum Durchführen selektiver Löschvorgänge. Bei Android-Geräten überprüft diese Ebene den Android-Gerätenachweis. Dabei handelt es sich um eine Konfiguration auf Einstiegsebene, die ähnliche Datenschutzkontrolle in Exchange Online-Postfachrichtlinien bereitstellt und der IT sowie dem Benutzerstamm eine Einführung in App-Schutzrichtlinien bietet.
- **Erweiterter Datenschutz für Unternehmen** (Ebene 2): Diese Ebene führt Mechanismen für App-Schutzrichtlinien zur Verhinderung von Datenlecks sowie die mindestens zu erfüllenden Betriebssystemanforderungen ein. Dies ist die Konfiguration, die für die meisten mobilen Benutzer gilt, die auf Geschäfts-, Schul- oder Unidaten zugreifen.
- **Hoher Datenschutz für Unternehmen** (Ebene 3): Auf dieser Ebene werden Mechanismen zum erweiterten Datenschutz, eine verbesserte PIN-Konfiguration sowie Mobile Threat Defense für App-Schutzrichtlinien eingeführt. Diese Konfiguration ist für Benutzer vorgesehen, die auf Hochrisikodaten zugreifen.

Die spezifischen Empfehlungen für jede Konfigurationsebene sowie die zumindest zu schützenden Apps finden Sie unter [Datenschutzframework mithilfe von App-Schutzrichtlinien](app-protection-framework.md).

Unabhängig davon, ob das Gerät in einer UEM-Lösung (Unified Endpoint Management) registriert ist, muss eine Intune-App-Schutzrichtlinie sowohl für iOS- als auch für Android-Apps erstellt werden, indem die Schritte unter [Erstellen und Zuweisen von App-Schutzrichtlinien](app-protection-policies.md) ausgeführt werden. Diese Richtlinien müssen mindestens die folgenden Bedingungen erfüllen:

1. Sie umfassen alle mobilen Microsoft 365-Anwendungen wie Microsoft Edge, Outlook, OneDrive, Office oder Teams. Damit wird sichergestellt, dass Benutzer in jeder Microsoft-App sicher auf Geschäfts-, Schul- oder Unidaten zugreifen und diese bearbeiten können.

2. Sie werden allen Benutzern zugewiesen. Dadurch wird sichergestellt, dass alle Benutzer unabhängig davon, ob sie Microsoft Edge für iOS oder Android nutzen, geschützt sind.

3. Bestimmen Sie, welche Frameworkebene Ihre Anforderungen erfüllt. Die meisten Organisationen sollten die Einstellungen, die unter **Erweiterter Datenschutz für Unternehmen** (Ebene 2) festgelegt wurden, implementieren, da dadurch Datenschutz und Zugriffsanforderungskontrollen ermöglicht werden.

Weitere Informationen zu den verfügbaren Einstellungen finden Sie unter [Einstellungen für App-Schutzrichtlinien für Android](app-protection-policy-settings-android.md) und [Einstellungen für App-Schutzrichtlinien für iOS](app-protection-policy-settings-ios.md).

> [!IMPORTANT]
> Um Intune-App-Schutzrichtlinien auf Apps auf Android-Geräten anzuwenden, die nicht bei Intune registriert sind, muss der Benutzer auch das Intune-Unternehmensportal installieren. Weitere Informationen finden Sie unter [Was Sie erwartet, wenn Ihre Android-App von App-Schutzrichtlinien verwaltet wird](../fundamentals/end-user-mam-apps-android.md).

## <a name="single-sign-on-to-azure-ad-connected-web-apps-in-policy-protected-browsers"></a>Einmaliges Anmelden bei mit Azure AD verbundenen Web-Apps in richtliniengeschützten Browsern

Microsoft Edge für iOS und Android kann für alle Web-Apps (SaaS und lokal), die mit Azure AD verbunden sind, den Vorteil des einmaligen Anmeldens (Single Sign-On, SSO) nutzen. Dank SSO können Benutzer über Microsoft Edge für iOS und Android auf mit Azure AD verbundene Web-Apps zugreifen, ohne ihre Anmeldeinformationen erneut eingeben zu müssen.

Für SSO muss Ihr Gerät entweder durch die Microsoft Authenticator-App für iOS-Geräte oder durch das Intune-Unternehmensportal unter Android registriert werden. Wenn Benutzer über eine dieser beiden Optionen verfügen, werden sie aufgefordert, ihr Gerät zu registrieren, sobald sie eine mit Azure AD verbundene Web-App in einem richtliniengeschützten Browser öffnen (dies gilt nur, wenn ihr Gerät bereits registriert wurde). Nachdem das Gerät mit dem von Intune verwalteten Benutzerkonto registriert wurde, ist bei diesem Konto das einmalige Anmelden für mit Azure AD verbundene Web-Apps aktiviert.

> [!NOTE]
> Bei der Geräteregistrierung handelt es sich um einen einfachen Check-In beim Azure AD-Dienst. Hierbei ist keine vollständige Geräteregistrierung erforderlich, und die IT-Abteilung erhält keine zusätzlichen Berechtigungen auf dem Gerät.

## <a name="utilize-app-configuration-to-manage-the-browsing-experience"></a>Verwalten der Browserumgebung mithilfe der App-Konfiguration

Microsoft Edge für iOS und Android unterstützt App-Einstellungen, die eine einheitliche Endpunktverwaltung ermöglichen, wie z. B. Microsoft Endpoint Manager. Administratoren können das Verhalten der App anpassen.

Die App-Konfiguration kann entweder über den Kanal „MDM (Mobile Device Management, Verwaltung mobiler Geräte)“ des Betriebssystems auf registrierten Geräten (Kanal [Managed App Configuration](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) für iOS oder [Android in the Enterprise ](https://developer.android.com/work/managed-configurations) für Android) oder über den Kanal „Intune-App-Schutzrichtlinie“ bereitgestellt werden. Microsoft Edge für iOS und Android unterstützt die folgenden Konfigurationsszenarien:

- Nur Geschäfts-, Schul- oder Unikonten zulassen
- Allgemeine App-Konfigurationseinstellungen
- Datenschutzeinstellungen

> [!IMPORTANT]
> Für Konfigurationsszenarien, die eine Geräteregistrierung unter Android erfordern, müssen die Geräte in Android Enterprise registriert werden, und Microsoft Edge für Android muss über den Managed Google Play Store bereitgestellt werden. Weitere Informationen finden Sie unter [Einrichten der Registrierung von Android Enterprise-Arbeitsprofilgeräten](../enrollment/android-work-profile-enroll.md) und [Hinzufügen von App-Konfigurationsrichtlinien für verwaltete Android Enterprise-Geräte](app-configuration-policies-use-android.md).

Für jedes Konfigurationsszenario werden die spezifischen Anforderungen hervorgehoben. Zum Beispiel, ob das Konfigurationsszenario die Registrierung von Geräten verlangt und somit mit jedem UEM-Anbieter funktioniert oder ob Intune-App-Schutzrichtlinien erforderlich sind.

> [!NOTE]
> Bei Microsoft Endpoint Manager wird die App-Konfiguration, die über den MDM-OS-Kanal bereitgestellt wird, als App-Konfigurationsrichtlinie für **verwaltete Geräte** bezeichnet. Eine App-Konfiguration, die über den Kanal „App-Schutzrichtlinie“ bereitgestellt wird, wird als App-Konfigurationsrichtlinie für **verwaltete Apps** bezeichnet.

## <a name="only-allow-work-or-school-accounts"></a>Nur Geschäfts-, Schul- oder Unikonten zulassen

Die Einhaltung der Datensicherheits- und Compliancerichtlinien unserer größten und hoch regulierten Kunden ist eine tragende Säule des Werts von Microsoft 365. In einigen Unternehmen müssen alle Kommunikationsinformationen in der Unternehmensumgebung aufgezeichnet werden, und ebenso muss sichergestellt werden, dass die Geräte nur für die Unternehmenskommunikation verwendet werden. Um diese Anforderungen zu unterstützen, kann Microsoft Edge für iOS und Android auf registrierten Geräten so konfiguriert werden, dass nur ein einziges Firmenkonto innerhalb der App bereitgestellt werden darf.

Hier erfahren Sie mehr über das Konfigurieren der Einstellung des Modus für zulässige Organisationskonten:

- [Einstellungen für Android](app-configuration-policies-use-android.md#allow-only-configured-organization-accounts-in-multi-identity-apps)
- [Einstellungen für iOS](app-configuration-policies-use-ios.md#allow-only-configured-organization-accounts-in-multi-identity-apps)

Dieses Konfigurationsszenario funktioniert nur mit registrierten Geräten. Allerdings werden beliebige UEM-Anbieter unterstützt. Wenn Sie Microsoft Endpoint Manager nicht nutzen, müssen Sie in Ihrer UEM-Dokumentation nachschlagen, wie Sie diese Konfigurationsschlüssel bereitstellen können.

## <a name="general-app-configuration-scenarios"></a>Allgemeine App-Konfigurationsszenarien

Microsoft Edge für iOS und Android bietet Administratoren die Möglichkeit, die Standardkonfiguration für verschiedene In-App-Einstellungen festzulegen. Diese Funktion wird derzeit nur angeboten, wenn Microsoft Edge für iOS und Android eine Richtlinie für den Intune-App-Schutz auf das Geschäfts-, Schul- oder Unikonto angewendet hat, das bei der App angemeldet ist, und die App-Einstellungen über eine App Configuration-Richtlinie für verwaltete Apps ausgeliefert werden.

> [!IMPORTANT]
> Microsoft Edge für Android unterstützt keine Chromium-Einstellungen, die in Managed Google Play verfügbar sind.

Microsoft Edge unterstützt die folgenden Konfigurationseinstellungen:

- Neue Registerkartenseite
- Lesezeichen
- App-Verhalten
- Kioskmodus

Diese Einstellungen können in der App unabhängig vom Registrierungsstatus des Geräts bereitgestellt werden.

### <a name="new-tab-page-experiences"></a>Neue Registerkartenseite

Microsoft Edge für iOS und Android bietet Organisationen mehrere Optionen zur Anpassung der neuen Registerkartenseite.

#### <a name="organization-logo-and-brand-color"></a>Organisationslogo und Markenfarbe

Diese Einstellungen ermöglichen Ihnen, die neue Registerkartenseite für Microsoft Edge für iOS und Android so anzupassen, dass Logo und Markenfarbe Ihrer Organisation als Seitenhintergrund angezeigt werden.

Um das Logo und die Farbe Ihrer Organisation hochzuladen, führen Sie zuerst die folgenden Schritte aus:
1. Navigieren Sie in [Microsoft Endpoint Manager](https://endpoint.microsoft.com) zu **Mandantenverwaltung** -> **Anpassung** -> **Unternehmensbranding**.
2. Um das Logo Ihrer Marke festzulegen, wählen Sie als Nächstes neben **In der Kopfzeile anzeigen** „Nur Organisationslogo“ aus. Es empfiehlt sich, transparente Hintergrundlogos zu verwenden.
3. Um die Hintergrundfarbe Ihrer Marke festzulegen, wählen Sie eine **Designfarbe** aus. Microsoft Edge für iOS und Android wendet einen helleren Farbton auf die neue Registerkartenseite an, was eine bessere Lesbarkeit der Seite gewährleistet.

Verwenden Sie nun die folgenden Schlüssel-Wert-Paare, um das Branding Ihrer Organisation in Microsoft Edge für iOS und Android zu übernehmen:

|    Key    |    Wert    |
|--------------------------------------------------------------------|------------|
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.BrandLogo    |    **TRUE**: Das Markenlogo der Organisation wird angezeigt.<br>**FALSE** (Standard): Das Logo wird nicht angezeigt.    |
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.BrandColor    |    **TRUE**: Die Markenfarbe der Organisation wird angezeigt.<br>**FALSE** (Standard): Die Markenfarbe der Organisation wird nicht angezeigt.    |

#### <a name="homepage-shortcut"></a>Verknüpfung zur Startseite

Diese Einstellung ermöglicht Ihnen das Konfigurieren einer Verknüpfung zur Startseite für Microsoft Edge für iOS und Android. Die von Ihnen konfigurierte Verknüpfung mit der Startseite wird als erstes Symbol unterhalb der Suchleiste angezeigt, sobald ein Benutzer eine neue Registerkarte in Microsoft Edge für iOS und Android öffnet. Der Benutzer kann diese Verknüpfung in seinem verwalteten Kontext nicht bearbeiten oder löschen. Die Verknüpfung mit der Homepage zeigt zur besseren Erkennbarkeit den Namen Ihrer Organisation an. 

|    Key    |    Wert    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.homepage   |    Geben Sie eine gültige URL ein. Ungültige URLs werden zur Sicherheit gesperrt.<br>Beispiel: `https://www.bing.com`     |

#### <a name="multiple-top-site-shortcuts"></a>Mehrere Verknüpfungen mit wichtigen Websites

Ähnlich wie beim Konfigurieren einer Verknüpfung mit der Startseite können Sie in Microsoft Edge für iOS und Android auf neuen Registerkartenseiten mehrere Verknüpfungen mit wichtigen Websites konfigurieren. Der Benutzer kann diese Verknüpfungen nicht in einem verwalteten Kontext bearbeiten oder löschen. Hinweis: Sie können insgesamt acht Verknüpfungen konfigurieren, einschließlich einer Verknüpfung mit der Startseite. Wenn Sie eine Tastenkombination für die Startseite konfiguriert haben, wird die erste konfigurierte Seite überschrieben. 

|    Key    |    Wert    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.managedTopSites   |    Legen Sie mehrere URL-Werte fest. Jede allgemeine Website-Verknüpfung besteht aus einem Titel und einer URL. Trennen Sie Titel und URL durch das `|`-Zeichen.<br>Beispiel: `GitHub|https://github.com/||LinkedIn|https://www.linkedin.com`    |

#### <a name="industry-news"></a>Branchennachrichten

Sie können das Element „Neue Registerkartenseite“ in Microsoft Edge für iOS und Android konfigurieren, um Branchennachrichten anzuzeigen, die für Ihre Organisation von Interesse sind. Wenn Sie dieses Feature aktivieren, verwendet Microsoft Edge für iOS und Android den Domänennamen Ihres Unternehmens, um Nachrichten aus dem Internet über Ihr Unternehmen, die Branche Ihres Unternehmens und Ihre Mitbewerber zu aggregieren, sodass Ihre Benutzer relevante externe Nachrichten auf den zentralisierten neuen Registerkarten innerhalb von Microsoft Edge für iOS und Android finden können. Branchennachrichten sind standardmäßig deaktiviert. 

|    Key    |    Wert    |
|------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.IndustryNews    |    **TRUE**: Branchennachrichten werden auf der neuen Registerkartenseite angezeigt.<br>**FALSE** (Standard): Branchennachrichten werden auf der neuen Registerkartenseite nicht angezeigt.    |

### <a name="bookmark-experiences"></a>Lesezeichen

Microsoft Edge für iOS und Android bietet Organisationen mehrere Optionen zum Verwalten von Lesezeichen.

#### <a name="managed-bookmarks"></a>Verwaltete Lesezeichen

Für eine erleichterte Bedienung können Sie Lesezeichen festlegen, die Ihren Benutzern in Microsoft Edge für iOS und Android zur Verfügung stehen sollen.

- Lesezeichen werden nur im Geschäfts-, Schul- oder Unikonto angezeigt und sind nicht für persönliche Konten verfügbar.
- Lesezeichen können von Benutzern nicht gelöscht oder geändert werden.
- Lesezeichen werden oben in der Liste angezeigt. Alle von Benutzern erstellten Lesezeichen werden unterhalb dieser Lesezeichen angezeigt.
- Wenn Sie die Anwendungsproxyumleitung aktiviert haben, können Sie Anwendungsproxy-Web-Apps mit deren interner oder externer URL hinzufügen.
- Stellen Sie beim Eingeben der URLs in die Liste sicher, dass Sie allen URLs **http://** oder **https://** voranstellen.
- Lesezeichen werden in einem Ordner erstellt, der nach dem in Azure Active Directory festgelegten Namen der Organisation benannt ist.

|    Key    |    Wert    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.bookmarks    |    Der Wert für diese Konfiguration ist eine Liste von Lesezeichen. Jedes Lesezeichen besteht aus dem Lesezeichentitel und der Lesezeichen-URL. Trennen Sie Titel und URL durch das `|`-Zeichen.<br> Beispiel: `Microsoft Bing|https://www.bing.com`<p>Zum Konfigurieren von mehreren Lesezeichen trennen Sie jedes Paar durch ein doppeltes `||`-Zeichen.<br>Beispiel:<br>`Microsoft Bing|https://www.bing.com||Contoso|https://www.contoso.com`    |

#### <a name="my-apps-bookmark"></a>Lesezeichen „Meine Apps“

Standardmäßig ist für Benutzer in Microsoft Edge für iOS und Android das Lesezeichen „Meine Apps“ im Organisationsordner konfiguriert.

|    Key    |    Wert    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.MyApps    |    **TRUE** (Standard): „Meine Apps“ wird in Microsoft Edge für iOS und Android in den Lesezeichen angezeigt.<br>**FALSE**: „Meine Apps“ wird in Microsoft Edge für iOS und Android nicht in den Lesezeichen angezeigt.    |

### <a name="app-behavior-experiences"></a>App-Verhalten

Microsoft Edge für iOS und Android bietet Organisationen mehrere Optionen zum Verwalten des Verhaltens der App.

#### <a name="default-protocol-handler"></a>Standardprotokollhandler

Standardmäßig nutzt Microsoft Edge für iOS und Android den HTTPS-Protokollhandler, wenn der Benutzer das Protokoll nicht in der URL angibt. Im Allgemeinen gilt dies als bewährte Methode, kann jedoch deaktiviert werden.

|    Key    |    Wert    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.defaultHTTPS     |     **TRUE** (Standard): Der Standardprotokollhandler ist HTTPS.<br>**FALSE** Der Standardprotokollhandler ist HTTP.     |

#### <a name="disable-data-sharing-for-personalization"></a>Deaktivieren der Datenfreigabe für die Personalisierung

Standardmäßig fordert Microsoft Edge für iOS und Android Benutzer zur Sammlung von Nutzungsdaten und zur Freigabe des Browserverlaufs auf, um ihre Browserumgebung zu personalisieren. Organisationen können diese Freigabe von Daten deaktivieren, indem sie verhindern, dass diese Aufforderung den Endbenutzern angezeigt wird.

|    Key    |    Wert    |
|----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.disableShareUsageData    |     **TRUE**: Diese Aufforderung wird Endbenutzern nicht angezeigt.<br>**FALSE** (Standard): Benutzer werden zur Freigabe von Nutzungsdaten aufgefordert.    |
|     com.microsoft.intune.mam.managedbrowser.disableShareBrowsingHistory    |     **TRUE**: Diese Aufforderung wird Endbenutzern nicht angezeigt.<br>**FALSE** (Standard) Benutzer werden aufgefordert, den Browserverlauf freizugeben.     |

#### <a name="disable-specific-features"></a>Deaktivieren bestimmter Features

Microsoft Edge für iOS und Android ermöglicht Organisationen, bestimmte Features zu deaktivieren, die standardmäßig aktiviert sind. Um diese Features zu deaktivieren, konfigurieren Sie die folgende Einstellung:

|    Key    |    Wert    |
|-----------------------|-----------------------|
|    com.microsoft.intune.mam.managedbrowser.disabledFeatures    |    **password**: deaktiviert Eingabeaufforderungen, die das Speichern von Kennwörtern für den Endbenutzer anbieten<br>**inprivate**: deaktiviert InPrivate-Browsen<p>Wenn Sie mehrere Features deaktivieren möchten, trennen Sie die Werte mit `|`. Beispielsweise deaktiviert `inprivate|password` sowohl InPrivate als auch die Kennwortspeicherung.     |

> [!NOTE]
> Microsoft Edge für Android unterstützt nicht die Deaktivierung des Kennwort-Managers.

#### <a name="disable-extensions"></a>Deaktivieren von Erweiterungen

Sie können das Erweiterungsframework in Microsoft Edge für Android deaktivieren, um zu verhindern, dass Benutzer App-Erweiterungen installieren. Konfigurieren Sie hierzu die folgende Einstellung:

|    Key    |    Wert    |
|-----------|-------------|
|    com.microsoft.intune.mam.managedbrowser.disableExtensionFramework    |    **TRUE**: deaktiviert das Erweiterungsframework<br>**FALSE** (Standard): aktiviert das Erweiterungsframework    |

### <a name="kiosk-mode-experiences-on-android-devices"></a>Kioskmodus auf Android-Geräten

Microsoft Edge für Android kann mit den folgenden Einstellungen als Kiosk-App aktiviert werden:

|    Key    |    Wert    |
|-----------|-------------|
|    com.microsoft.intune.mam.managedbrowser.enableKioskMode    |    **TRUE**: aktiviert den Kioskmodus für Microsoft Edge für Android<br>**FALSE** (Standard): deaktiviert den Kioskmodus    |
|    com.microsoft.intune.mam.managedbrowser.showAddressBarInKioskMode    |    **TRUE**: zeigt die Adressleiste im Kioskmodus an<br> **false** (Standard): blendet die Adressleiste aus, wenn der Kioskmodus aktiviert ist    |
|    com.microsoft.intune.mam.managedbrowser.showBottomBarInKioskMode    |    **TRUE**: zeigt die untere Aktionsleiste im Kioskmodus an<br> **false** (Standard): blendet die untere Leiste aus, wenn der Kioskmodus aktiviert ist    |

## <a name="data-protection-app-configuration-scenarios"></a>App-Konfigurationsszenarien für Datenschutz

Wenn die App vom Microsoft Endpoint Manager mit einer Richtlinie für den Intune-App-Schutz verwaltet wird, die für das bei der App angemeldete Geschäfts-, Schul- oder Unikonto gilt, und die Richtlinieneinstellungen über eine App Configuration-Richtlinie für verwaltete Apps ausgeliefert werden, unterstützt Microsoft Edge für iOS und Android App-Konfigurationsrichtlinien für die folgenden Datenschutzeinstellungen:

- Verwalten der Kontosynchronisierung
- Verwalten eingeschränkter Websites
- Verwalten der Proxykonfiguration
- Verwalten von NTLM-Websites mit einmaligem Anmelden

Diese Einstellungen können in der App unabhängig vom Registrierungsstatus des Geräts bereitgestellt werden.

### <a name="manage-account-synchronization"></a>Verwalten der Kontosynchronisierung

Standardmäßig ermöglicht die Microsoft Edge-Synchronisierung Benutzern auf allen ihren angemeldeten Geräten Zugriff auf ihre Browserdaten. Folgende Daten werden für die Synchronisierung unterstützt:

- Favoriten
- Kennwörter
- Adressen und mehr (automatisches Ausfüllen von Formulareinträgen)

Die Synchronisierungsfunktion wird mittels Zustimmung des Benutzers aktiviert. Benutzer können die Synchronisierung für jeden der oben aufgeführten Datentypen ein- oder ausschalten. Weitere Informationen finden Sie unter [Microsoft Edge-Synchronisierung](/DeployEdge/microsoft-edge-enterprise-sync).

Organisationen haben die Möglichkeit, die Microsoft Edge-Synchronisierung unter iOS und Android zu deaktivieren. 

|Key  |Wert  |
|---------|---------|
|com.microsoft.intune.mam.managedbrowser.account.syncDisabled     |**TRUE** (Standard): lässt die Edge-Synchronisierung zu<br>**FALSE**: deaktiviert die Edge-Synchronisierung          |

### <a name="manage-restricted-web-sites"></a>Verwalten eingeschränkter Websites

Organisationen können festlegen, auf welche Websites Benutzer im Kontext des Geschäfts-, Schul- oder Unikontos in Microsoft Edge für iOS und Android zugreifen können. Wenn Sie eine Zulassungsliste verwenden, können Ihre Benutzer nur auf die Websites zugreifen, die explizit aufgelistet sind. Wenn Sie eine Sperrliste verwenden, können Benutzer auf alle Websites mit Ausnahme derjenigen zugreifen, die explizit blockiert sind. Sie sollten entweder nur eine Zulassungsliste oder nur eine Blockierungsliste vorgeben, nicht beide Listen. Wenn Sie beide Listen vorgeben, wird nur die Zulassungsliste berücksichtigt.

Organisation legen auch fest, was passiert, wenn ein Benutzer versucht, zu einer eingeschränkten Website zu navigieren. Übergänge sind standardmäßig zulässig. Wenn die Organisation es erlaubt, können eingeschränkte Websites im Kontext des persönlichen Kontos, im InPrivate-Kontext des Azure AD-Kontos oder unabhängig davon, ob die Website vollständig gesperrt ist, geöffnet werden. Weitere Informationen zu den verschiedenen unterstützten Szenarien finden Sie unter [Restricted website transitions in Microsoft Edge mobile](https://techcommunity.microsoft.com/t5/intune-customer-success/restricted-website-transitions-in-microsoft-edge-mobile/ba-p/1381333) (Übergänge zu eingeschränkten Websites in der mobilen Version von Microsoft Edge). Durch das Erlauben von Übergängen bleiben die Benutzer der Organisation geschützt, während gleichzeitig die Unternehmensressourcen abgesichert bleiben.

> [!NOTE]
> Microsoft Edge für iOS und Android kann den Zugriff auf Websites nur blockieren, wenn direkt darauf zugegriffen wird. Der Zugriff auf die Website wird nicht blockiert, wenn Benutzer dafür Zwischendienste (z.B. einen Übersetzungsdienst) verwenden.

Verwenden Sie die folgenden Schlüssel-Wert-Paare, um entweder eine Zulassungs- oder eine Sperrliste für Websites in Microsoft Edge für iOS und Android zu konfigurieren. 

|Key  |Wert  |
|---------|---------|
|com.microsoft.intune.mam.managedbrowser.AllowListURLs     |Der entsprechende Wert für den Schlüssel ist eine Liste mit URLs. Sie geben alle URLs, die Sie zulassen möchten, als einen einzigen Wert getrennt durch einen senkrechten Strich `|` ein.<p>**Beispiele:**<br>`URL1|URL2|URL3`<br>`http://.contoso.com/|https://.bing.com/|https://expenses.contoso.com`         |
|com.microsoft.intune.mam.managedbrowser.BlockListURLs     |Der entsprechende Wert für den Schlüssel ist eine Liste mit URLs. Sie geben alle URLs, die Sie sperren möchten, als einen einzigen Wert getrennt durch einen senkrechten Strich `|` ein.<br>**Beispiele:**<br>`URL1|URL2|URL3`<br>`http://.contoso.com/|https://.bing.com/|https://expenses.contoso.com`         |
|com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock     |**TRUE** (Standard): In Microsoft Edge für iOS und Android sind Übergänge zu eingeschränkten Websites erlaubt. Wenn persönliche Konten nicht deaktiviert sind, werden Benutzer aufgefordert, entweder in den persönlichen Kontext zu wechseln, um die eingeschränkte Website zu öffnen, oder ein persönliches Konto hinzuzufügen. Wenn com.microsoft.intune.mam.managedbrowser.openInPrivateIfBlocked auf TRUE festgelegt ist, haben Benutzer die Möglichkeit, die eingeschränkte Website im InPrivate-Kontext zu öffnen.<p>**FALSE**: In Microsoft Edge für iOS und Android sind Übergänge für Benutzer nicht erlaubt. Benutzern wird einfach eine Meldung angezeigt, die besagt, dass die Website, auf die sie versuchen zuzugreifen, gesperrt ist.         |
|com.microsoft.intune.mam.managedbrowser.openInPrivateIfBlocked     |**TRUE**: ermöglicht das Öffnen eingeschränkter Websites im InPrivate-Kontext des Azure AD-Kontos. Wenn das Azure AD-Konto das einzige in Microsoft Edge für iOS und Android konfigurierte Konto ist, wird die eingeschränkte Website automatisch im InPrivate-Kontext geöffnet. Wenn der Benutzer ein persönliches Konto konfiguriert hat, wird er aufgefordert, zwischen dem Öffnen von InPrivate oder Wechseln zum persönlichen Konto zu wählen.<p> **FALSE** (Standard): erfordert, dass die eingeschränkte Website im persönlichen Konto des Benutzers geöffnet wird. Wenn persönliche Konten deaktiviert sind, wird die Website blockiert.<p>Damit diese Einstellung wirksam wird, muss com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock auf TRUE festgelegt werden.          |
|com.microsoft.intune.mam.managedbrowser.durationOfOpenInPrivateSnackBar     | Geben Sie die Anzahl der Sekunden ein, die Benutzer die folgende Snackbarbenachrichtigung sehen: „Link im InPrivate-Modus geöffnet. Ihre Organisation verlangt die Nutzung des InPrivate-Modus für diese Inhalte.“ Standardmäßig wird die Snackbarbenachrichtigung 7 Sekunden angezeigt.

Die folgenden Websites sind unabhängig von den definierten Zulassungs- oder Sperrlisteneinstellungen immer zulässig:
- `https://*.microsoft.com/*`
- `http://*.microsoft.com/*`
- `https://microsoft.com/*`
- `http://microsoft.com/*`
- `https://*.windowsazure.com/*`
- `https://*.microsoftonline.com/*`
- `https://*.microsoftonline-p.com/*`

#### <a name="url-formats-for-allowed-and-blocked-site-list"></a>URL-Formate für die Liste zulässiger und blockierter Websites 

Sie können verschiedene URL-Formate verwenden, um Ihre Listen für zulässige/blockierte Websites zu erstellen. Diese zulässigen Muster werden in der folgenden Tabelle beschrieben.

- Stellen Sie beim Eingeben der URLs in die Liste sicher, dass Sie allen URLs **http://** oder **https://** voranstellen.
- Sie können das Platzhaltersymbol (\*) entsprechend den Regeln in der folgenden Liste mit zulässigen Mustern verwenden.
- Ein Platzhalter kann nur mit einem Abschnitt (z. B. `news-contoso.com`), einer vollständigen Komponente des Hostnamens (z. B. `host.contoso.com`) oder vollständigen Bestandteilen des Pfads übereinstimmen, wenn dieser durch Schrägstriche getrennt ist (`www.contoso.com/images`).
- Sie können Portnummern in der Adresse angeben. Wenn Sie keine Portnummer angeben, werden folgende Werte verwendet:
  - Port 80 für http
  - Port 443 für https
- Die Verwendung von Platzhaltern für die Portnummer wird **nicht** unterstützt. Beispielsweise werden `http://www.contoso.com:*` und `http://www.contoso.com:*/` nicht unterstützt. 

    |    URL    |    Details    |    Treffer    |    Stimmt nicht überein mit    |
    |-------------------------------------------|--------------------------------------------------------|-------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
    |    `http://www.contoso.com`    |    Entspricht einer einzelnen Seite    |    `www.contoso.com`    |    `host.contoso.com`<br>`www.contoso.com/images`<br>`contoso.com/`    |
    |    `http://contoso.com`    |    Entspricht einer einzelnen Seite    |    `contoso.com/`    |    `host.contoso.com`<br>`www.contoso.com/images`<br>`www.contoso.com`    |
    |    `http://www.contoso.com/*`   |    Entspricht allen URLs, die mit `www.contoso.com` beginnen    |    `www.contoso.com`<br>`www.contoso.com/images`<br>`www.contoso.com/videos/tvshows`    |    `host.contoso.com`<br>`host.contoso.com/images`    |
    |    `http://*.contoso.com/*`    |    Entspricht allen Unterdomänen unter `contoso.com`    |    `developer.contoso.com/resources`<br>`news.contoso.com/images`<br>`news.contoso.com/videos`    |    `contoso.host.com`<br>`news-contoso.com`
    |    `http://*contoso.com/*`    |    Entspricht allen Unterdomänen, die mit `contoso.com/` enden    |    `news-contoso.com`<br>`news-contoso.com.com/daily`    |    `news-contoso.host.com`<br>`news.contoso.com`    |
    `http://www.contoso.com/images`    |    Entspricht einem einzelnen Ordner    |    `www.contoso.com/images`    |    `www.contoso.com/images/dogs`    |
    |    `http://www.contoso.com:80`    |    Entspricht einer einzelnen Seite, unter Verwendung einer Portnummer    |    `www.contoso.com:80`    |         |
    |    `https://www.contoso.com`    |    Entspricht einer einzelnen, sicheren Seite    |    `www.contoso.com`    |    `www.contoso.com`    |
    |    `http://www.contoso.com/images/*`    |    Entspricht einem einzelnen Ordner und allen Unterordnern    |    `www.contoso.com/images/dogs`<br>`www.contoso.com/images/cats`    |    `www.contoso.com/videos`    |
  
- Im Folgenden finden Sie Beispiele für Eingaben, die nicht unterstützt werden:
  - `*.com`
  - `*.contoso/*`
  - `www.contoso.com/*images`
  - `www.contoso.com/*images*pigs`
  - `www.contoso.com/page*`
  - IP-Adressen
  - `https://*`
  - `http://*`
  - `http://www.contoso.com:*`
  - `http://www.contoso.com: /*`

### <a name="manage-proxy-configuration"></a>Verwalten der Proxykonfiguration

Sie können Microsoft Edge für iOS und Android und den [Azure AD-Anwendungsproxy](/azure/active-directory/active-directory-application-proxy-get-started) gemeinsam verwenden, um Benutzern auf ihren mobilen Geräten Zugriff auf Intranetsites zu ermöglichen. Beispiel: 

- Ein Benutzer verwendet die mobile Outlook-App, die durch Intune geschützt ist. Dann klickt er in einer E-Mail auf einen Link zu einer Intranetsite, und Edge für iOS und Android erkennt, dass diese Website dem Benutzer über den Anwendungsproxy verfügbar gemacht wurde. Der Benutzer wird automatisch über den Anwendungsproxy weitergeleitet, um sich mit einer anwendbaren Option für die mehrstufige Authentifizierung und bedingtem Zugriff zu authentifizieren, bevor er zur Intranetsite gelangt. Der Benutzer kann jetzt auch auf seinem mobilen Gerät auf Intranetsites zugreifen, und der Link in Outlook funktioniert wie erwartet.
- Ein Benutzer öffnet Edge für iOS und Android auf seinem iOS- oder Android-Gerät. Wenn Edge für iOS und Android durch Intune geschützt ist und der Anwendungsproxy aktiviert wurde, kann der Benutzer über die gewohnte interne URL zu einer Intranetsite navigieren. Edge für iOS und Android erkennt, dass diese Intranetsite dem Benutzer über den Anwendungsproxy verfügbar gemacht wurde. Der Benutzer wird zur Authentifizierung automatisch über den Anwendungsproxy weitergeleitet, bevor er zur Intranetsite gelangt. 

Vorbereitung:

- Richten Sie Ihre internen Anwendungen über den Azure AD-Anwendungsproxy ein.
  - Informationen zum Konfigurieren des Anwendungsproxys und zum Veröffentlichen von Anwendungen finden Sie in der [Setup-Dokumentation](/azure/active-directory/manage-apps/application-proxy).
- Der App „Edge für iOS und Android“ muss eine [Intune-App-Schutzrichtlinie](app-protection-policy.md) zugewiesen sein.
- Microsoft-Apps müssen über eine App-Schutzrichtlinie verfügen, bei der die Datenübertragungseinstellung **Übertragung von Webinhalten mit anderen Apps einschränken** auf **Microsoft Edge** festgelegt ist.

> [!NOTE]
> Es kann bis zu 24 Stunden dauern, bis aktualisierte Umleitungsdaten des Anwendungsproxys in Edge für iOS und Android in Kraft treten.

Geben Sie Edge für iOS als Ziel für das folgende Schlüssel-Wert-Paar an, um den Anwendungsproxy zu aktivieren:

|    Key    |    Wert    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.AppProxyRedirection    |    **TRUE**: ermöglicht Umleitungsszenarien für den Azure AD-Anwendungsproxy<br>**FALSE** (Standard): verhindert Szenarien für den Azure AD-Anwendungsproxy    |

> [!NOTE]
> Edge für Android verwendet diesen Schlüssel nicht. Stattdessen nutzt Edge für Android die Konfiguration des Azure AD-Anwendungsproxys automatisch, solange für das angemeldete Azure AD-Konto eine App-Schutzrichtlinie gilt.

Weitere Informationen zur gemeinsamen Verwendung von Edge für iOS und Android und Azure AD-Anwendungsproxy für nahtlosen (und geschützten) Zugriff auf lokale Web-Apps finden Sie im Blogbeitrag [Better together: Intune and Azure Active Directory team up to improve user access](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/better-together-intune-and-azure-active-directory-team-up-to/ba-p/250254) (Intune und Azure Active Directory gemeinsam verwenden, um den Benutzerzugriff zu verbessern). Dieser Blogbeitrag verweist auf den Intune Managed Browser, doch der Inhalt gilt auch für Edge für iOS und Android.

### <a name="manage-ntlm-single-sign-on-sites"></a>Verwalten von NTLM-Websites mit einmaligem Anmelden

Organisationen können von Benutzern verlangen, dass sie sich mit NTLM authentifizieren, um auf Intranetsites zugreifen zu können. Standardmäßig werden Benutzer bei jedem Zugriff auf eine Website, die eine NTLM-Authentifizierung erfordert, zur Eingabe von Anmeldeinformationen aufgefordert, da das Zwischenspeichern von NTLM-Anmeldeinformationen deaktiviert ist. 

Organisationen können das Zwischenspeichern von NTLM-Anmeldeinformationen für bestimmte Websites aktivieren. Bei diesen Websites werden die Anmeldeinformationen, nachdem der Benutzer sie eingegeben und sich erfolgreich authentifiziert hat, standardmäßig 30 Tage zwischengespeichert.


|Key  |Wert  |
|---------|---------|
|com.microsoft.intune.mam.managedbrowser.NTLMSSOURLs     |Der entsprechende Wert für den Schlüssel ist eine Liste mit URLs. Sie geben alle URLs, die Sie zulassen möchten, als einen einzigen Wert getrennt durch einen senkrechten Strich `|` ein.<p>**Beispiele:**<br>`URL1|URL2`<br>`http://app.contoso.com/|https://expenses.contoso.com`<p>Weitere Informationen zu den unterstützten URL-Formaten finden Sie unter [URL-Formate für die Liste zulässiger und blockierter Websites](#url-formats-for-allowed-and-blocked-site-list).         |
|com.microsoft.intune.mam.managedbrowser.durationOfNTLMSSO     |Anzahl der Stunden, die Anmeldeinformationen zwischengespeichert werden, Standardwert 720         |

## <a name="deploy-app-configuration-scenarios-with-microsoft-endpoint-manager"></a>Bereitstellen von Szenarien zur App-Konfiguration mit Microsoft Endpoint Manager

Wenn Sie Microsoft Endpoint Manager als Anbieter für die Verwaltung mobiler Anwendungen nutzen, können Sie mit den folgenden Schritten eine Richtlinie zur Konfiguration verwalteter Apps erstellen. Nachdem die Konfiguration erstellt wurde, können Sie ihre Einstellungen Benutzergruppen zuweisen.

1. Melden Sie sich bei [Microsoft Endpoint Manager](https://endpoint.microsoft.com) an.

2. Wählen Sie **Apps** und dann **App-Konfigurationsrichtlinien** aus.

3. Wählen Sie auf dem Blatt **App-Konfigurationsrichtlinien** erst **Hinzufügen** und dann **Verwaltete Apps** aus.

4. Geben Sie im Abschnitt **Grundlagen** einen **Namen** und optional eine **Beschreibung** für die App-Konfigurationseinstellungen ein.

5. Wählen Sie für **Öffentliche Apps** zunächst **Öffentliche Apps auswählen** und dann auf dem Blatt **Ziel-Apps** die Option **Edge für iOS und Android**, indem Sie sowohl die Apps für die iOS- als auch für die Android-Plattform auswählen. Klicken Sie auf **Auswählen**, um die ausgewählten öffentlichen Apps zu speichern.

6. Klicken Sie auf **Weiter**, um die grundlegenden Einstellungen der App-Konfigurationsrichtlinie festzulegen.

7. Erweitern Sie im Abschnitt **Einstellungen** die Option **Edge-Konfigurationseinstellungen**.

8. Wenn Sie die Datenschutzeinstellungen verwalten möchten, konfigurieren Sie die gewünschten Einstellungen entsprechend:

    - Treffen Sie für **Anwendungsproxyumleitung** eine Wahl aus den verfügbaren Optionen: **Aktivieren**, **Deaktivieren** (Standard).

    - Geben Sie für **URL-Verknüpfung zur Startseite** eine gültige URL an, die entweder das Präfix *http://* oder *https://* enthält. Ungültige URLs werden zur Sicherheit gesperrt.

    - Geben Sie für **Verwaltete Lesezeichen** den Titel und eine gültige URL an, die entweder das Präfix *http://* oder *https://* enthält.

    - Geben Sie für **Zulässige URLs** eine gültige URL an (nur diese URLs sind zulässig. Zugriff auf andere Websites ist nicht möglich). Weitere Informationen zu den unterstützten URL-Formaten finden Sie unter [URL-Formate für die Liste zulässiger und blockierter Websites](#url-formats-for-allowed-and-blocked-site-list).

    - Geben Sie für **Blockierte URLs** eine gültige URL an (nur diese URLs werden blockiert). Weitere Informationen zu den unterstützten URL-Formaten finden Sie unter [URL-Formate für die Liste zulässiger und blockierter Websites](#url-formats-for-allowed-and-blocked-site-list).

    - Treffen Sie für **Eingeschränkte Sites an persönlichen Kontext umleiten** eine Wahl aus den verfügbaren Optionen: **Aktivieren** (Standard), **Deaktivieren**.

    > [!NOTE]
    > Wenn in der Richtlinie sowohl zulässige als auch blockierte URLs definiert sind, wird nur die Liste mit den zulässigen URLs berücksichtigt.

9. Wenn Sie zusätzliche App-Konfigurationseinstellungen festlegen möchten, die in der obigen Richtlinie nicht festgelegt sind, erweitern Sie den Knoten **Allgemeine Konfigurationseinstellungen**, und geben Sie in die Schlüssel-Wert-Paare entsprechend ein.

10. Wenn Sie die Konfiguration der Einstellungen abgeschlossen haben, klicken Sie auf **Weiter**.

11. Wählen Sie im Abschnitt **Zuweisungen** die Option **Wählen Sie die Gruppen aus, die eingeschlossen werden sollen** aus. Wählen Sie die Azure AD-Gruppe, der Sie die App-Konfigurationsrichtlinie zuweisen möchten, und anschließend **Auswählen** aus.

12. Wenn Sie mit den Zuweisungen fertig sind, wählen Sie **Weiter** aus.

13. Überprüfen Sie auf dem Blatt  **App-Konfigurationsrichtlinie erstellen** unter „Überprüfen + erstellen“ die konfigurierten Einstellungen, und wählen Sie **Erstellen** aus.

Die neu erstellte Konfigurationsrichtlinie wird auf dem Blatt **App-Konfiguration** angezeigt.

## <a name="use-edge-for-ios-and-android-to-access-managed-app-logs"></a>Verwenden von Microsoft Edge für iOS und Android für den Zugriff auf Protokolle von verwalteten Apps

Benutzer, auf deren Gerät Edge für iOS oder Android installiert ist, können den Verwaltungsstatus aller von Microsoft veröffentlichten Apps anzeigen. Mithilfe der folgenden Schritte können sie Protokolle zur Behandlung von Problemen mit ihren verwalteten iOS- oder Android-Apps senden:

1. Öffnen Sie auf Ihrem Gerät Edge für iOS oder Android.
2. Geben Sie im Adressfeld `about:intunehelp` ein.
3. Edge für iOS oder Android wird im Problembehandlungsmodus gestartet.

Eine Liste der in den App-Protokollen gespeicherten Einstellungen finden Sie unter [Überprüfen der Schutzprotokolle für Client-Apps](app-protection-policy-settings-log.md).

Informationen zum Anzeigen von Protokollen auf Android-Geräten finden Sie unter [Senden von Protokollen an Ihren IT-Administrator per E-Mail](../user-help/send-logs-to-your-it-admin-by-email-android.md).

## <a name="next-steps"></a>Nächste Schritte

- [Was sind App-Schutzrichtlinien?](app-protection-policy.md) 
- [App-Konfigurationsrichtlinien für Microsoft Intune](app-configuration-policies-overview.md)