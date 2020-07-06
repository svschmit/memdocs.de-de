---
title: Hinzufügen und Zuweisen von MTD-Apps mit Microsoft Intune
titleSuffix: Microsoft Intune
description: Hinzufügen von Mobile Threat Defense-Apps (MTD), der Microsoft Authenticator-App und der iOS-Konfigurationsrichtlinie im Azure-Portal mit Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/26/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 00356258-76a8-4a84-9cf5-64ceedb58e72
ms.reviewer: davera
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 03dbdccd1626db5ad97bc230a3d6b9a82060ee2e
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/01/2020
ms.locfileid: "85590489"
---
# <a name="add-and-assign-mobile-threat-defense-mtd-apps-with-intune"></a>Hinzufügen und Zuweisen von Mobile Threat Defense-Apps (MTD) mit Intune

Sie können Intune verwenden, um MTD-Apps hinzuzufügen und bereitzustellen, damit Endbenutzer Benachrichtigungen über auf ihren mobilen Geräten erkannte Bedrohungen sowie eine Anleitung zur Behebung der Bedrohungen erhalten können.

> [!NOTE]
> Dieser Artikel gilt für alle Mobile Threat Defense-Partner.

## <a name="before-you-begin"></a>Vorbereitung

Führen Sie die folgenden Schritte in Intune aus. Stellen Sie sicher, dass Sie mit den folgenden Prozessen vertraut sind:

- [Hinzufügen von Apps in Microsoft Intune](../apps/apps-add.md)
- [Hinzufügen von iOS-Apps mit Konfigurationsrichtlinien in Microsoft Intune](../apps/app-configuration-policies-use-ios.md)
- [Zuweisen einer App mit Intune](../apps/apps-deploy.md)

> [!TIP]
> Das Intune-Unternehmensportal arbeitet als Broker auf Android-Geräten, damit Benutzer ihre Identitäten von Azure AD überprüfen lassen können.

## <a name="configure-microsoft-authenticator-for-ios"></a>Konfigurieren von Microsoft Authenticator für iOS

Für iOS-Geräte benötigen Sie [Microsoft Authenticator](https://docs.microsoft.com/azure/multi-factor-authentication/end-user/microsoft-authenticator-app-how-to), damit Benutzer ihre Identitäten von Azure AD überprüfen lassen können. Außerdem benötigen Sie eine iOS-App-Konfigurationsrichtlinie, die die MTD-iOS-App festlegt, die mit Intune verwendet werden soll.

Sehen Sie sich die Anleitungen für [das Hinzufügen von iOS Store-Apps zu Microsoft Intune](../apps/store-apps-ios.md) an. Verwenden Sie diese [App Store-URL von Microsoft Authenticator](https://itunes.apple.com/us/app/microsoft-authenticator/id983156458?mt=8), wenn Sie **App-Informationen** konfigurieren.

## <a name="configure-your-mtd-apps-with-an-app-configuration-policy"></a>Konfigurieren von MTD-Apps mit einer App-Konfigurationsrichtlinie

Um das Onboarding von Benutzern zu vereinfachen, verwenden die Mobile Threat Defense-Apps auf mit MDM verwalteten Geräten die App-Konfiguration. Für nicht registrierte Geräte ist die MDM-basierte App-Konfiguration nicht verfügbar. Weitere Informationen finden Sie unter [Hinzufügen von Mobile Threat Defense-Apps zu nicht registrierten Geräten](../protect/mtd-add-apps-unenrolled-devices.md).

### <a name="lookout-for-work-app-configuration-policy"></a>Konfigurationsrichtlinie für Lookout for Work-Apps

Erstellen Sie die iOS-App-Konfigurationsrichtlinie wie im Artikel [zur Verwendung der iOS-App-Konfigurationsrichtlinie](../apps/app-configuration-policies-use-ios.md) beschrieben.

### <a name="sep-mobile-app-configuration-policy"></a>Konfigurationsrichtlinie für SEP Mobile-Apps

Verwenden Sie dasselbe Azure AD-Konto, das zuvor in der [Symantec Endpoint Protection-Verwaltungskonsole](https://aad.skycure.com) konfiguriert wurde. Dabei sollte es sich um das Konto handeln, mit dem Sie sich bei Intune anmelden.

- **Herunterladen** der iOS-App-Konfigurationsrichtliniendatei:
  - Wechseln Sie zur [Symantec Endpoint Protection-Verwaltungskonsole](https://aad.skycure.com), und melden Sie sich mit Ihren Anmeldeinformationen an.

  - Wechseln Sie zu **Einstellungen**, und wählen Sie unter **Integrationen** die Option **Intune** aus. Wählen Sie **EMM Integration Selection** (EMM-Integrationsauswahl) aus. Wählen Sie **Microsoft** aus, und speichern Sie Ihre Auswahl.

  - Klicken Sie auf den Link **Integration setup files** (Integrationssetupdateien), und speichern Sie die generierte \*.zip-Datei. Die ZIP-Datei enthält die Datei „* **.plist**“, die zum Erstellen der iOS-App-Konfigurationsrichtlinie in Intune verwendet wird.

  - In den Anweisungen für [die Verwendung der iOS-App-Konfigurationsrichtlinien von Microsoft Intune](../apps/app-configuration-policies-use-ios.md) erfahren Sie, wie Sie die iOS-App-Konfigurationsrichtlinie für SEP Mobile hinzufügen.

    - Wählen Sie für **Format der Konfigurationseinstellungen** **XML-Daten eingeben** aus, kopieren Sie den Inhalt aus der * **.plist**-Datei, und fügen Sie diesen Inhalt in den Text der Konfigurationsrichtlinie ein.

> [!NOTE]
> Wenn Sie die Dateien nicht abrufen können, wenden Sie sich an den [Symantec Endpoint Protection Mobile Enterprise Support](https://support.symantec.com/en_US/contact-support.html).

### <a name="check-point-sandblast-mobile-app-configuration-policy"></a>Konfigurationsrichtlinie für Check Point SandBlast Mobile-Apps

In den Anweisungen für [die Verwendung der iOS-App-Konfigurationsrichtlinien von Microsoft Intune](../apps/app-configuration-policies-use-ios.md) erfahren Sie, wie Sie die iOS-App-Konfigurationsrichtlinie für Check Point SandBlast Mobile hinzufügen.

- Wählen Sie für **Format der Konfigurationseinstellungen** **XML-Daten eingeben** aus, kopieren Sie den folgenden Inhalt, und fügen Sie diesen Inhalt in den Text der Konfigurationsrichtlinie ein.

  `<dict><key>MDM</key><string>INTUNE</string></dict>`


### <a name="zimperium-app-configuration-policy"></a>Konfigurationsrichtlinie für Zimperium-Apps

In den Anweisungen für [die Verwendung der iOS-App-Konfigurationsrichtlinien von Microsoft Intune](../apps/app-configuration-policies-use-ios.md) erfahren Sie, wie Sie die iOS-App-Konfigurationsrichtlinie für Zimperium hinzufügen.

- Wählen Sie für **Format der Konfigurationseinstellungen** **XML-Daten eingeben** aus, kopieren Sie den folgenden Inhalt, und fügen Sie diesen Inhalt in den Text der Konfigurationsrichtlinie ein.

   ```
   <dict>
   <key>provider</key><string>Intune</string>
   <key>userprincipalname</key><string>{{userprincipalname}}</string>
   <key>deviceid</key>
   <string>{{deviceid}}</string>
   <key>serialnumber</key>
   <string>{{serialnumber}}</string>
   <key>udidlast4digits</key>
   <string>{{udidlast4digits}}</string>
   </dict>
   ```

### <a name="pradeo-app-configuration-policy"></a>Pradeo-App-Konfigurationsrichtlinie

Pradeo unterstützt keine Anwendungskonfigurationsrichtlinien für iOS/iPadOS.  Wenn Sie eine konfigurierte App erhalten möchten, arbeiten Sie stattdessen mit Pradeo zusammen, um benutzerdefinierte IPA- und APK-Dateien zu implementieren, die mit den gewünschten Einstellungen vorkonfiguriert sind.

### <a name="better-mobile-app-configuration-policy"></a>Konfigurationsrichtlinie für Better Mobile-Apps

In den Anweisungen für [die Verwendung der iOS-App-Konfigurationsrichtlinien von Microsoft Intune](../apps/app-configuration-policies-use-ios.md) erfahren Sie, wie Sie die iOS-App-Konfigurationsrichtlinie für Better Mobile hinzufügen.

- Wählen Sie für **Format der Konfigurationseinstellungen** **XML-Daten eingeben** aus, kopieren Sie den folgenden Inhalt, und fügen Sie diesen Inhalt in den Text der Konfigurationsrichtlinie ein. Ersetzen Sie die URL für `https://client.bmobi.net` durch die URL für die entsprechende Konsole.

   ```
    <dict>
   <key>better_server_url</key>
   <string>https://client.bmobi.net</string>
   <key>better_udid</key>
   <string>{{aaddeviceid}}</string>
   <key>better_user</key>
   <string>{{userprincipalname}}</string>
   </dict>
   ```

### <a name="sophos-mobile-app-configuration-policy"></a>Konfigurationsrichtlinie für Sophos Mobile-Apps

Erstellen Sie die iOS-App-Konfigurationsrichtlinie wie im Artikel [zur Verwendung der iOS-App-Konfigurationsrichtlinie](../apps/app-configuration-policies-use-ios.md) beschrieben. Weitere Informationen finden Sie in der Sophos-Wissensdatenbank unter [Sophos Intercept X for Mobile iOS - Available managed settings](https://community.sophos.com/kb/133963) (Sophos Intercept X for Mobile iOS – verfügbare verwaltete Einstellungen).

### <a name="wandera-app-configuration-policy"></a>Wandera-App-Konfigurationsrichtlinie

> [!NOTE]
> Verwenden Sie für die anfänglichen Tests eine Testgruppe, wenn Sie Benutzer und Geräte im Abschnitt „Zuweisungen“ in der Richtlinie zur Konfiguration zuweisen. 

- **Android**
  - In den Anweisungen zur[Verwendung der Android-App-Konfigurationsrichtlinien von Microsoft Intune](../apps/app-configuration-policies-use-android.md) erfahren Sie, wie Sie bei Aufforderung die Android-App-Konfigurationsrichtlinie für Wandera gemäß den nachstehenden Informationen hinzufügen.

1. Klicken Sie im **RADAR Wandera Portal** unter **Configuration settings** (Konfigurationseinstellungen) auf die Schaltfläche **Add+** (Hinzufügen+).
2. Wählen Sie in der Liste **Configuration Keys** (Konfigurationsschlüssel) **Activation Profile URL** (Aktivierungsprofil-URL) aus. Klicken Sie auf **OK**.
3. Wählen Sie für **Activation Profile URL** (Aktivierungsprofil-URL) im Menü **Value type** (Werttyp) die Option **string** (Zeichenfolge) aus. Kopieren Sie dann die **Shareable Link URL** (Freigabelink-URL) aus dem gewünschten Aktivierungsprofil in RADAR, und fügen Sie sie ein.
4. Definieren Sie in **Settings** (Einstellungen) **Configuration settings format > Use Configuration Designer** (Format der Konfigurationseinstellungen > Konfigurations-Designer verwenden), und führen Sie die folgenden Schritte aus.

> [!NOTE] 
> Im Gegensatz zu iOS müssen Sie bei Android Enterprise-Apps für jedes Wandera-Aktivierungsprofil eine eindeutige Konfigurationsrichtlinie definieren. Wenn Sie nicht mehrere Wandera-Aktivierungsprofile benötigen, können Sie für alle Zielgeräte eine zentrale Android-App-Konfiguration verwenden. Wenn Sie in Wandera Aktivierungsprofile erstellen, müssen Sie unter der Konfiguration „Associated User (Zugeordnete Benutzer)“ die Option „Azure Active Directory“ auswählen, um sicherzustellen, dass Wandera in der Lage ist, das Gerät über UEM Connect mit Microsoft Endpoint Manager zu synchronisieren.

- **iOS**
  - In den Anweisungen zur[Verwendung der iOS-App-Konfigurationsrichtlinien von Microsoft Intune](../apps/app-configuration-policies-use-ios.md) erfahren Sie, wie Sie bei Aufforderung die iOS-App-Konfigurationsrichtlinie für Wandera gemäß den nachstehenden Informationen hinzufügen.

1. Navigieren Sie im **RADAR Wandera Portal** zu **Devices > Activations** (Geräte > Aktivierungen), und wählen Sie ein beliebiges Aktivierungsprofil aus. Klicken Sie auf **Deployment Strategies > Managed Devices > Microsoft Intune** (Bereitstellungsstrategien > Verwaltete Geräte > Microsoft Intune), und suchen Sie die **iOS App Configuration settings** (iOS-App-Konfigurationseinstellungen).  
2. Klappen Sie das Feld auf, um den XML-Code der iOS-App-Konfiguration anzuzeigen, und kopieren Sie ihn in die Zwischenablage Ihres Systems.  
3. Definieren Sie in **Settings** (Einstellungen) **Configuration settings format > Enter XML data** (Format der Konfigurationseinstellungen > XML-Daten eingeben), und führen Sie die folgenden Schritte aus:
4. Fügen Sie in Microsoft Endpoint Manager den XML-Code in das Textfeld „App-Konfiguration“ ein.

> [!NOTE]
> Eine zentrale iOS-Konfigurationsrichtlinie kann für alle Geräte verwendet werden, auf denen Wandera bereitgestellt werden soll.  

## <a name="assigning-mobile-threat-defense-apps-to-end-users-via-intune"></a>Zuweisen von Mobile Threat Defense-Apps für Endbenutzer über Intune

Um die App Mobile Threat Defense auf dem Endgerät des Benutzers zu installieren, können Sie im Azure-Portal die folgenden Schritte ausführen. Stellen Sie sicher, dass Sie mit den folgenden Prozessen vertraut sind:

- [Zuweisen von Apps zu Gruppen mit Intune](../apps/apps-deploy.md)

Wählen Sie den Abschnitt aus, der Ihrem MTD-Anbieter entspricht:

- [Lookout for Work](#assigning-lookout-for-work)
- [Symantec Endpoint Protection Mobile (SEP Mobile)](#assigning-symantec-endpoint-protection-mobile)
- [Check Point SandBlast Mobile](#assigning-check-point-sandblast-mobile)
- [Zimperium](#assigning-zimperium)
- [Pradeo](#assigning-pradeo)
- [Better Mobile](#assigning-better-mobile)
- [Sophos Mobile](#assigning-sophos)
- [Wandera](#assigning-wandera)

### <a name="assigning-lookout-for-work"></a>Zuweisen von Lookout for Work

- **Android**
  - Sehen Sie sich die Anleitungen für [das Hinzufügen von Android Store-Apps zu Microsoft Intune](../apps/store-apps-android.md) an. Verwenden Sie diese [App-Store-URL zu Lookout for Work für Google](https://play.google.com/store/apps/details?id=com.lookout.enterprise) für die **App-Store-URL**.

- **iOS**
  - Sehen Sie sich die Anleitungen für [das Hinzufügen von iOS Store-Apps zu Microsoft Intune](../apps/store-apps-ios.md) an. Verwenden Sie diese [App Store-URL zu Lookout for Work für iOS](https://itunes.apple.com/us/app/lookout-for-work/id997193468?mt=8) für die **App Store-URL**.

- **Lookout for Work-App außerhalb des Apple Stores**
  - Sie müssen nun die Lookout for Work-App für iOS erneut signieren. Lookout verteilt seine Lookout for Work iOS-App außerhalb des iOS App Store. Bevor Sie die App verteilen, müssen Sie die App mit Ihrem iOS Enterprise Developer Certificate neu signieren.  
  - Ausführliche Anweisungen zum erneuten Signieren der Lookout for Work-Apps für iOS finden Sie unter [iOS App Re-Signing Process (Erneute Signatur bei iOS-Apps)](https://personal.support.lookout.com/hc/articles/114094038714) auf der Lookout-Website.

  - **Aktivieren der Azure AD-Authentifizierung für Benutzer der Lookout for Work-iOS-App**

    1. Wechseln Sie zum [Azure-Portal](https://portal.azure.com), melden Sie sich mit Ihren Anmeldeinformationen an, und navigieren Sie zur Seite „Anwendungen“.

    2. Fügen Sie die **Lookout for Work iOS-App** als eine **native Clientanwendung** hinzu.

    3. Ersetzen Sie **com.lookout.enterprise.yourcompanyname** mit der Kundenbundle-ID, die Sie beim Unterzeichnen der IPA ausgewählt haben.

    4. Hinzufügen von zusätzlichen Umleitungs-URI: **&lt;companyportal://code/>** gefolgt von einer URL-codierten Version Ihrer ursprünglichen URI-Umleitung.

    5. Fügen Sie **Delegierte Berechtigungen** zu Ihrer App hinzu.

    > [!NOTE]
    > Weitere Informationen finden Sie unter [Konfigurieren Sie eine native Clientanwendung](https://azure.microsoft.com/documentation/articles/app-service-mobile-how-to-configure-active-directory-authentication/#optional-configure-a-native-client-application).

  - **Hinzufügen der IPA-Datei für Lookout for Work**

    - Laden Sie die neu signierte IPA-Datei hoch, wie im Artikel [Hinzufügen von branchenspezifischen iOS-Apps in Microsoft Intune](../apps/lob-apps-ios.md) beschrieben. Sie müssen auch iOS 8.0 oder höher als die mindestens erforderliche Betriebssystemversion festlegen.

### <a name="assigning-symantec-endpoint-protection-mobile"></a>Zuweisen von Symantec Endpoint Protection Mobile

- **Android**
  - Sehen Sie sich die Anleitungen für [das Hinzufügen von Android Store-Apps zu Microsoft Intune](../apps/store-apps-android.md) an. Verwenden Sie diese [App-Store-URL zu SEP Mobile](https://play.google.com/store/apps/details?id=com.skycure.skycure) für die **App-Store-URL**.  Wählen Sie für **Mindestens erforderliches Betriebssystem** die Option **Android 4.0 (Ice Cream Sandwich)** aus.

- **iOS**
  - Sehen Sie sich die Anleitungen für [das Hinzufügen von iOS Store-Apps zu Microsoft Intune](../apps/store-apps-ios.md) an. Verwenden Sie diese [App Store-URL zu SEP Mobile](https://itunes.apple.com/us/app/skycure/id695620821?mt=8) für die **App Store-URL**.

### <a name="assigning-check-point-sandblast-mobile"></a>Zuweisen von Check Point SandBlast Mobile

- **Android**  
  - Sehen Sie sich die Anleitungen für [das Hinzufügen von Android Store-Apps zu Microsoft Intune](../apps/store-apps-android.md) an. Verwenden Sie diese [App-Store-URL zu Check Point SandBlast Mobile](https://play.google.com/store/apps/details?id=com.lacoon.security.fox) als **App-Store-URL**.

- **iOS**
  - Sehen Sie sich die Anleitungen für [das Hinzufügen von iOS Store-Apps zu Microsoft Intune](../apps/store-apps-ios.md) an. Verwenden Sie diese [App Store-URL zu Check Point SandBlast Mobile](https://apps.apple.com/us/app/sandblast-mobile-protect/id1006390797) als **App-Store-URL**.  

### <a name="assigning-zimperium"></a>Zuweisen von Zimperium

- **Android**
  - Sehen Sie sich die Anleitungen für [das Hinzufügen von Android Store-Apps zu Microsoft Intune](../apps/store-apps-android.md) an. Verwenden Sie diese [App-Store-URL zu Zimperium](https://play.google.com/store/apps/details?id=com.zimperium.zips&hl=en) für die **App-Store-URL**.

- **iOS**
  - Sehen Sie sich die Anleitungen für [das Hinzufügen von iOS Store-Apps zu Microsoft Intune](../apps/store-apps-ios.md) an. Verwenden Sie diese [App Store-URL zu Zimperium](https://itunes.apple.com/us/app/zimperium-zips/id1030924459?mt=8) für die **App Store-URL**.  
 
### <a name="assigning-pradeo"></a>Zuweisen von Pradeo

- **Android**
  - Sehen Sie sich die Anleitungen für [das Hinzufügen von Android Store-Apps zu Microsoft Intune](../apps/store-apps-android.md) an. Verwenden Sie diese [App-Store-URL zu Pradeo](https://play.google.com/store/apps/details?id=net.pradeo.service&hl=en_US) für die **App-Store-URL**.

- **iOS**
  - Sehen Sie sich die Anleitungen für [das Hinzufügen von iOS Store-Apps zu Microsoft Intune](../apps/store-apps-ios.md) an. Verwenden Sie diese [App Store-URL zu Pradeo](https://itunes.apple.com/us/app/pradeo-agent/id547979360?mt=8) für die **App Store-URL**.

### <a name="assigning-better-mobile"></a>Zuweisen von Better Mobile

- **Android**
  - Sehen Sie sich die Anleitungen für [das Hinzufügen von Android Store-Apps zu Microsoft Intune](../apps/store-apps-android.md) an. Verwenden Sie diese [App-Store-URL zu Active Shield](https://play.google.com/store/apps/details?id=com.better.active.shield.enterprise) für die **App-Store-URL**.

- **iOS**
  - Sehen Sie sich die Anleitungen für [das Hinzufügen von iOS Store-Apps zu Microsoft Intune](../apps/store-apps-ios.md) an. Verwenden Sie diese [App Store-URL zu Active Shield](https://itunes.apple.com/us/app/activeshield/id980234260?mt=8&uo=4) für die **App Store-URL**.

### <a name="assigning-sophos"></a>Zuweisen von Sophos

- **Android**
  - Sehen Sie sich die Anleitungen für [das Hinzufügen von Android Store-Apps zu Microsoft Intune](../apps/store-apps-android.md) an. Verwenden Sie diese [App-Store-URL zu Sophos](https://play.google.com/store/apps/details?id=com.sophos.smsec) für die **App-Store-URL**.

- **iOS**
  - Sehen Sie sich die Anleitungen für [das Hinzufügen von iOS Store-Apps zu Microsoft Intune](../apps/store-apps-ios.md) an. Verwenden Sie diese [App Store-URL zu Active Shield](https://itunes.apple.com/us/app/sophos-mobile-security/id1086924662?mt=8) für die **App Store-URL**.

### <a name="assigning-wandera"></a>Zuweisen von Wandera

- **Android**
  - Sehen Sie sich die Anleitungen für [das Hinzufügen von Android Store-Apps zu Microsoft Intune](../apps/store-apps-android.md) an. Verwenden Sie diese [App-Store-URL zu Wandera Mobile](https://play.google.com/store/apps/details?id=com.wandera.android) für die **App-Store-URL**. Wählen Sie für **Mindestens erforderliches Betriebssystem** die Option **Android 5.0** aus.

- **iOS**
  - Sehen Sie sich die Anleitungen für [das Hinzufügen von iOS Store-Apps zu Microsoft Intune](../apps/store-apps-ios.md) an. Verwenden Sie diese [App Store-URL zu Wandera Mobile](https://itunes.apple.com/app/wandera/id605469330) für die **App Store-URL**.

## <a name="next-steps"></a>Nächste Schritte

- [Konfigurieren einer Mobile Threat Defense-Gerätekompatibilitätsrichtlinie (MTD) mit Intune](mtd-device-compliance-policy-create.md)
