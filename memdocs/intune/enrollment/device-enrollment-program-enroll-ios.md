---
title: 'Automatisierte Geräteregistrierung: Registrieren von iOS/iPadOS-Geräten'
titleSuffix: Microsoft Intune
description: Hier erfahren Sie, wie Sie unternehmenseigene iOS/iPadOS-Geräte mit der automatischen Geräteregistrierung registrieren.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/10/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7ddbf360-0c61-11e8-ba89-0ed5f89f718b
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: d5ec26d03336e73f7dadf0912992b018058dc493
ms.sourcegitcommit: cba06c182646cb6dceef304b35230bf728d5133e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/15/2020
ms.locfileid: "90574880"
---
# <a name="automatically-enroll-iosipados-devices-with-apples-automated-device-enrollment"></a>Automatisches Registrieren von iOS-/iPadOS-Geräten mit der automatischen Geräteregistrierung von Apple

> [!IMPORTANT]
> Apple hat vor Kurzem vom Programm zur Geräteregistrierung (DEP, Device Enrollment Program) auf die automatische Geräteregistrierung (ADE, Automated Device Enrollment) umgestellt. Die Benutzeroberfläche von Intune wird derzeit entsprechend aktualisiert. Bis diese Änderungen abgeschlossen sind, wird im Intune-Portal weiterhin der Begriff *Programm zur Geräteregistrierung* verwendet. Überall, wo dieser steht, wird nun die automatische Geräteregistrierung verwendet.

Sie können Intune zum Registrieren von iOS/iPadOS-Geräten über die [automatischen Geräteregistrierung](https://deploy.apple.com) konfigurieren, die von Apple erworben wurden. Mit der automatischen Geräteregistrierung können Sie eine große Anzahl von Geräten registrieren, ohne diese jemals zu berühren. Geräte wie iPhones, iPads und MacBooks können direkt an Benutzer geliefert werden. Wenn der Benutzer das Gerät anschaltet, wird der Setup-Assistent, der in der Regel eine schnelle und unkomplizierte Installation für Apple-Produkte bietet, mit vordefinierten Einstellungen ausgeführt, und das Gerät wird für die Verwaltung registriert.

Um die automatische Geräteregistrierung zu aktivieren, müssen Sie die Portale von Intune und [Apple Business Manager (ABM)](https://business.apple.com/) oder [Apple School Manager (ASM)](https://school.apple.com/) verwenden. Sie benötigen auch eine Liste von Seriennummern oder eine Bestellnummer, um Geräte in einem der beiden Apple-Portale Intune zur Verwaltung zuweisen zu können. Sie erstellen in Intune ADE-Registrierungsprofile, die Einstellungen enthalten, die bei der Registrierung auf Geräte angewendet werden. Die automatische Geräteregistrierung kann nicht mit einem [Geräteregistrierungs-Manager](device-enrollment-manager-enroll.md)-Konto verwendet werden.

> [!NOTE]
> Bei der automatischen Geräteregistrierung werden Gerätekonfigurationen festgelegt, die nicht zwangsläufig vom Endbenutzer entfernt werden können. Daher muss das Gerät vor der [Migration zu ADE](../fundamentals/migration-guide-considerations.md) zurückgesetzt werden, um es in den werkseitigen (neuen) Zustand zurückzuversetzen.

## <a name="automated-device-enrollment-and-the-company-portal"></a>Automatische Geräteregistrierung und das Unternehmensportal

Die automatische Geräteregistrierung ist mit der App Store-Version der Unternehmensportal-App nicht kompatibel. Sie können Benutzern Zugriff auf die Unternehmensportal-App über ein ADE-Gerät gewähren. Sie sollten diesen Zugriff bereitstellen, damit Benutzer wählen können, welche Unternehmens-Apps sie auf ihrem Gerät verwenden möchten, oder damit sie eine moderne Authentifizierungsmethode verwenden können, um den Registrierungsprozess abzuschließen. 

Sie können die moderne Authentifizierung während der Registrierung aktivieren, indem Sie die App mithilfe von **Unternehmensportal mit VPP installieren** (Apple Volume Purchase Program) im ADE-Profil per Push auf das Gerät übertragen. Weitere Informationen finden Sie unter [Automatisches Registrieren von iOS-/iPadOS-Geräten mit der automatischen Geräteregistrierung von Apple](device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile).

Damit das Unternehmensportal automatisch Updates ausführt und um die Unternehmensportal-App auf Geräten bereitzustellen, die bereits mit der automatischen Geräteregistrierung registriert wurden, stellen Sie die Unternehmensportal-App über Intune als erforderliche VPP-App (Apple Volume Purchase Program) mit angewendeter [Anwendungskonfigurationsrichtlinie](../apps/app-configuration-policies-use-ios.md) bereit.

## <a name="what-is-supervised-mode"></a>Überwachter Modus

Apple hat für iOS/iPadOS 5 den überwachten Modus eingeführt. Ein iOS-/iPadOS-Gerät im überwachten Modus kann mit mehr Steuerelementen verwaltet werden, z. B. Blockieren der Bildschirmaufnahme und Blockieren der Installation von Apps aus dem App Store. Dies ist bei unternehmenseigenen Geräten besonders nützlich. Intune unterstützt die Konfiguration von Geräten für den überwachten Modus als Teil der automatischen Geräteregistrierung.

Die Unterstützung für nicht überwachte ADE-Geräte ist seit iOS/iPadOS 11 veraltet. In iOS/iPadOS 11 und höher sollten für ADE konfigurierte Geräte immer überwacht werden. Das ADE-Flag *is_supervised* wird in iOS/iPadOS 13.0 und höher ignoriert. Alle iOS/iPadOS-Geräte mit Version 13.0 und höher werden bei einer Registrierung über die automatische Geräteregistrierung automatisch überwacht. 

<!--
**Steps to enable enrollment programs from Apple**
1. [Get an Apple DEP token and assign devices](#get-the-apple-dep-token)
2. [Create an enrollment profile](#create-an-apple-enrollment-profile)
3. [Synchronize DEP-managed devices](#sync-managed-device)
4. [Assign DEP profile to devices](#assign-an-enrollment-profile-to-devices)
5. [Distribute devices to users](#end-user-experience-with-managed-devices)
-->
## <a name="prerequisites"></a>Voraussetzungen
- Über die [automatische Geräteregistrierung von Apple](https://deploy.apple.com) erworbene Geräte
- [Autorität für die Verwaltung mobiler Geräte (Mobile Device Management, MDM)](../fundamentals/mdm-authority-set.md)
- [Apple-MDM-Push-Zertifikat](apple-mdm-push-certificate-get.md)

## <a name="supported-volume"></a>Unterstütztes Volume

- Maximale Registrierungsprofile pro Token: 1,000  
- Maximale Anzahl von Geräten mit automatischer Geräteregistrierung pro Profil: keine Beschränkung (innerhalb der maximalen Anzahl von Geräten pro Token)
- Maximale Anzahl der Token für die automatische Geräteregistrierung pro Intune-Konto: 2,000
- Maximale Anzahl von Geräten mit automatischer Geräteregistrierung pro Token: Der Grenzwert bei der ersten Synchronisierung ist 75.000 bis 80.000 Geräte. Intune wird weiterhin alle 12 Stunden mit ABM oder ASM synchronisiert, um mit jedem Mal mehr Geräte hinzuzufügen. Eine manuelle Synchronisierung (die alle 15 Minuten ausgelöst werden kann) fügt auch ein Gerätebatch zu Intune hinzu. Synchronisierungen erfolgen weiterhin, und Geräte werden weiterhin in großen Mengen zwischen ABM/ASM und Intune synchronisiert. 

## <a name="get-an-apple-automated-device-enrollment-token"></a>Abrufen eines Tokens für die automatische Geräteregistrierung von Apple

Damit Sie iOS-/iPadOS-Geräte mit der automatischen Geräteregistrierung registrieren können, benötigen Sie eine ADE-Tokendatei (P7M) von Apple. Mit diesem Token kann Intune Informationen zu ADE-Geräten synchronisieren, die Ihrem Unternehmen gehören. Damit kann Intune außerdem Registrierungsprofile zu Apple hochladen und diesen Profilen Geräte zuweisen.

Sie verwenden das Portal [Apple Business Manager (ABM)](https://business.apple.com/) oder [Apple School Manager (ASM)](https://school.apple.com/) zum Erstellen eines Tokens. Sie verwenden das ABM/ASM-Portal auch, um in Intune Geräte für die Verwaltung zuzuweisen.

> [!NOTE]
> Wenn Sie das Token vor der Migration zu Azure aus dem klassischen Intune-Portal löschen, stellt Intune möglicherweise ein gelöschtes Apple-ADE-Token wieder her. Sie können das ADE-Token wieder aus dem Azure-Portal löschen.

### <a name="step-1-download-the-intune-public-key-certificate-required-to-create-the-token"></a>Schritt 1: Laden Sie das Intune-Zertifikat mit öffentlichem Schlüssel herunter, das zum Erstellen des Tokens erforderlich ist.

1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf die Option **Devices** > **iOS/iPadOS** > **iOS/iPadOS enrollment** (Geräte > iOS/iPadOS > iOS/iPadOS-Registrierung).

    ![Rufen Sie ein Registrierungsprogrammtoken ab.](./media/device-enrollment-program-enroll-ios/ios-enroll.png)

2. Klicken Sie auf **Token für Registrierungsprogramm** > **Hinzufügen**.

3. Erteilen Sie Microsoft die Berechtigung, Benutzer- und Geräteinformationen an Apple zu senden, indem Sie auf **Ich stimme zu** klicken.

   > [!NOTE]
   > Sobald Sie Schritt 2 ausgeführt haben, um das öffentliche Schlüsselzertifikat in Intune herunterzuladen, schließen Sie den Assistenten nicht, und bleiben Sie auf dieser Seite. Wenn Sie den Assistenten bzw. die Seite schließen, verliert das heruntergeladene Zertifikat seine Gültigkeit, und Sie müssen den Prozess noch mal durchführen. Wenn diese Situation bei Ihnen eintritt, stellen Sie üblicherweise fest, dass die Schaltfläche **Erstellen** auf der Registerkarte **Überprüfen + erstellen** abgeblendet dargestellt wird und Sie den Prozess nicht abschließen können.

   ![Screenshot des Bereichs „Registrierungsprogrammtoken“ im Arbeitsbereich „Apple-Zertifikate“ zum Herunterladen des öffentlichen Schlüssels](./media/device-enrollment-program-enroll-ios/add-enrollment-program-token-pane.png)

4. Wählen Sie **Laden Sie Ihr Zertifikat mit öffentlichem Schlüssel herunter** aus, um die Verschlüsselungsschlüsseldatei (PEM) herunterzuladen und lokal zu speichern. Die PEM-Datei wird verwendet, um ein Vertrauensstellungszertifikat vom Apple-Portal anzufordern.


### <a name="step-2-use-your-key-to-download-a-token-from-apple"></a>Schritt 2: Verwenden Sie Ihren Schlüssel, um ein Token von Apple herunterzuladen.

1. Klicken Sie auf **Create a token via Apple Business Manager** (Token über Apple Business Manager erstellen), um das Unternehmensportal von Apple zu öffnen, und melden Sie sich dann mit Ihrer Unternehmens-Apple-ID an. Sie können diese Apple-ID auch zum Erneuern Ihres ADE-Tokens verwenden.
2. Klicken Sie im [Business-Portal](https://business.apple.com) von Apple auf die Option **Erste Schritte** für das **Programm zur Geräteregistrierung**.

3. Wählen Sie auf der Seite **Server verwalten** die Option **MDM-Server hinzufügen** aus.
4. Geben Sie den **MDM-Servernamen** ein, und wählen Sie anschließend **Weiter** aus. Der Servername dient als Referenz zum Identifizieren des MDM-Servers (mobile device management, Verwaltung mobiler Geräte). Es handelt sich nicht um den Namen oder die URL des Microsoft Intune-Servers.

5. Das Dialogfeld **&lt;Servername&gt; hinzufügen** wird geöffnet, und die Meldung **Laden Sie Ihren öffentlichen Schlüssel hoch** wird angezeigt. Wählen Sie **Datei auswählen** aus, um die PEM-Datei hochzuladen, und wählen Sie anschließend **Weiter** aus.

6. Wechseln Sie zu **Bereitstellungsprogramm** &gt; **Programm zur Geräteregistrierung** &gt; **Geräte verwalten**.
7. Geben Sie unter **Geräte auswählen nach** an, wie die Geräte identifiziert werden sollen:
    - **Seriennummer**
    - **Reihenfolge**
    - **Upload der CSV-Datei**

   ![Screenshot bei Festlegen von „Geräte auswählen nach“ auf „Seriennummer“, der Einstellung „Aktion auswählen“ auf „Zu Server zuweisen“ und der Auswahl des Servernamens.](./media/device-enrollment-program-enroll-ios/enrollment-program-token-specify-serial.png)

8. Wählen Sie als Nächstes für **Aktion auswählen** die Option **Zu Server zuweisen** aus. Wählen Sie den für Microsoft Intune angegebenen &lt;Servernamen&gt; und anschließend **OK** aus. Das Apple-Portal weist die angegebenen Geräte dem Intune-Server für die Verwaltung zu und zeigt dann **Zuweisung abgeschlossen** an.

   Wechseln Sie im Apple-Portal zu **Bereitstellungsprogramme** &gt; **Programm zur Geräteregistrierung** &gt; **Zuweisungsverlauf anzeigen**, um eine Liste der Geräte und ihre MDM-Server-Zuordnung anzuzeigen.

### <a name="step-3-save-the-apple-id-used-to-create-this-token"></a>Schritt 3: Speichern Sie die zum Erstellen dieses Tokens verwendete Apple-ID.

Geben Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) die Apple-ID zur späteren Verwendung an.

![Screenshot der Angabe der Apple-ID zur Erstellung des Registrierungsprogrammtokens und Navigieren zu diesem Token](./media/device-enrollment-program-enroll-ios/image03.png)

### <a name="step-4-upload-your-token-and-choose-scope-tags"></a>Schritt 4: Laden Sie Ihr Token hoch, und wählen Sie Bereichsmarkierungen aus.

1. Navigieren Sie im Feld **Apple token** (Apple-Token) zur Zertifikatsdatei (P7M), und wählen Sie **Öffnen** aus.
2. Wenn Sie [Bereichsmarkierungen](../fundamentals/scope-tags.md) auf dieses DEP-Token anwenden möchten, klicken Sie auf **Scope (tags)** (Bereich (Markierungen)), und wählen Sie die gewünschten Bereichsmarkierungen aus. Bereichsmarkierungen, die auf ein Token angewendet wurden, werden von Profilen und Geräten geerbt, die diesem Token hinzugefügt werden.
3. Wählen Sie **Erstellen** aus.

Mit dem Pushzertifikat kann Intune iOS-/iPadOS-Geräte registrieren und verwalten, indem die Richtlinie auf registrierte mobile Geräte gepusht wird. Intune führt eine automatische Synchronisierung mit Apple durch, um Ihr Registrierungsprogrammkonto anzuzeigen.

## <a name="create-an-apple-enrollment-profile"></a>Erstellen eines Apple-Registrierungsprofils

Da Sie nun Ihr Token installiert haben, können Sie ein Registrierungsprofil für ADE-Geräte erstellen. Ein Geräteregistrierungsprofil definiert die Einstellungen, die während der Registrierung auf eine Gruppe von Geräten angewendet werden. Es gilt ein Limit von 100 Registrierungsprofilen pro ADE-Token.

> [!NOTE]
> Geräte werden blockiert, wenn nicht genügend Unternehmensportallizenzen für ein VPP-Token vorhanden sind oder das Token abgelaufen ist. Intune zeigt eine Warnung an, wenn ein Token in Kürze abläuft oder bald keine Lizenzen mehr zur Verfügung stehen.
 

1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Devices** > **iOS/iPadOS** > **iOS/iPadOS enrollment** > **Enrollment program tokens** (Geräte > iOS/iPadOS > iOS/iPadOS-Registrierung > Token für Registrierungsprogramm).
2. Wählen Sie ein Token aus, und wählen Sie dann **Profile** > **Profil erstellen** > **iOS/iPadOS** aus.

    ![Screenshot „Profil erstellen“](./media/device-enrollment-program-enroll-ios/image04.png)

3. Geben Sie zu administrativen Zwecken auf der Seite **Grundlegende Einstellungen** einen **Namen** und eine **Beschreibung** für das Profil ein. Benutzer können diese Informationen nicht sehen. 

    ![Profilname und Beschreibung](./media/device-enrollment-program-enroll-ios/image05.png)

4. Wählen Sie **Weiter: Geräteverwaltungseinstellungen** aus.

5. Wählen Sie unter **Benutzeraffinität** aus, ob sich Geräte mit diesem Profil mit oder ohne einen zugewiesenen Benutzer registrieren müssen.
    - **Mit Benutzeraffinität registrieren**: Wählen Sie diese Option für Geräte aus, die Benutzern gehören und für Dienste wie z.B. die Installation von Apps das Unternehmensportal verwenden sollen. Wenn Sie ADFS verwenden und zur Authentifizierung den Setup-Assistenten verwenden, ist der [Endpunkt WS-Trust 1.3 Username/Mixed](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff608241(v=ws.10)) [Weitere Informationen](/powershell/module/adfs/get-adfsendpoint?view=win10-ps) erforderlich.

    - **Ohne Benutzeraffinität registrieren**: Wählen Sie diese Option für Geräte aus, die keinem einzelnen Benutzer zugeordnet sind. Verwenden Sie diese Option für Geräte, die nicht auf lokale Benutzerdaten zugreifen. Um es einem Endbenutzer zu ermöglichen, sich beim iOS-Unternehmensportal anzumelden und sich selbst als primären Benutzer des Geräts festzulegen, senden Sie den `IntuneUDAUserlessDevice`-Schlüssel in einer App-Konfigurationsrichtlinie für verwaltete Geräte an das iOS-Unternehmensportal. Hinweis: Nur der erste Benutzer, der sich anmeldet, wird als primärer Benutzer festgelegt. Wenn sich der erste Benutzer abmeldet und ein anderer Benutzer anmeldet, bleibt der erste Benutzer der primäre Benutzer des Geräts. Weitere Informationen finden Sie unter [Konfigurieren der Unternehmensportal-App zur Unterstützung von iOS-und iPadOS-DEP-Geräten](../apps/app-configuration-policies-use-ios.md#configure-the-company-portal-app-to-support-ios-and-ipados-dep-devices). 

6. Wenn Sie **Mit Benutzeraffinität registrieren** ausgewählt haben, können Sie es Benutzern ermöglichen, sich über das Unternehmensportal statt über den Apple-Setup-Assistenten zu authentifizieren.

    ![Authentifizieren über das Unternehmensportal](./media/device-enrollment-program-enroll-ios/authenticatewithcompanyportal.png)

    > [!NOTE]
    > Wenn Sie eine der folgenden Aktionen ausführen möchten, legen Sie **Wählen Sie aus, wo Benutzer sich authentifizieren müssen** auf **Unternehmensportal** fest.
    >    - Sie möchten die mehrstufige Authentifizierung verwenden.
    >    - Sie möchten Benutzer zum Ändern ihres Kennworts auffordern, wenn sie sich zum ersten Mal anmelden.
    >    - Sie möchten Benutzer dazu auffordern, ihre abgelaufenen Kennwörter bei der Registrierung zurückzusetzen.
    >
    > Diese Optionen werden nicht unterstützt, wenn die Authentifizierung über den Setup-Assistenten von Apple erfolgt.

7. Wenn Sie **Unternehmensportal** für **Wählen Sie aus, wo Benutzer sich authentifizieren müssen** ausgewählt haben, können Sie ein VPP-Token verwenden, um das Unternehmensportal automatisch auf dem Gerät zu installieren. In diesem Fall muss der Benutzer keine Apple-ID angeben. Wählen Sie unter **Install Company Portal with VPP** (Unternehmensportal mit VPP installieren) ein Token aus, um das Unternehmensportal mit einem VPP-Token zu installieren. Setzt voraus, dass das Unternehmensportal dem VPP-Token bereits hinzugefügt wurde. Um sicherzustellen, dass die Unternehmensportal-App nach der Registrierung weiterhin aktualisiert wird, stellen Sie sicher, dass Sie in Intune eine App-Bereitstellung konfiguriert haben (Intune > Client-Apps). Damit keine Benutzerinteraktion erforderlich ist, sollten Sie das Unternehmensportal unbedingt als iOS-/iPadOS-VPP-App verwenden, als erforderliche App festlegen und für die Zuordnung die Gerätelizenzierung verwenden. Stellen Sie sicher, dass das Token nicht abläuft, und dass Sie über genügend Gerätelizenzen für die Unternehmensportal-App verfügen. Wenn das Token abgelaufen ist, oder wenn dessen Lizenzen abgelaufen sind, installiert Intune stattdessen das App Store-Unternehmensportal und fordert zur Eingabe einer Apple-ID auf. 

    > [!NOTE]
    > Wenn **Wählen Sie aus, wo Benutzer sich authentifizieren müssen** auf **Unternehmensportal** festgelegt ist, stellen Sie sicher, dass der Geräteregistrierungsprozess innerhalb der ersten 24 Stunden erfolgt, nachdem das Unternehmensportal auf das ADE-Gerät heruntergeladen wurde. Andernfalls schlägt die Registrierung möglicherweise fehl, und es wird eine Zurücksetzung auf Werkseinstellungen erforderlich, um das Gerät zu registrieren.
    
    ![Screenshot einer Installation des Unternehmensportals mit VPP](./media/device-enrollment-program-enroll-ios/install-cp-with-vpp.png)

8. Wenn Sie **Setup-Assistent** für **Wählen Sie aus, wo Benutzer sich authentifizieren müssen** ausgewählt haben, aber auch „Bedingter Zugriff“ verwenden oder Unternehmens-Apps auf den Geräten bereitstellen möchten, müssen Sie das Unternehmensportal auf den Geräten installieren. Wählen Sie hierzu **Ja** für **Unternehmensportal installieren** aus.  Wenn Sie möchten, dass Benutzer das Unternehmensportal erhalten, ohne sich beim App Store authentifizieren zu müssen, wählen Sie **Unternehmensportal mit VPP installieren** aus, und wählen Sie ein VPP-Token aus. Vergewissern Sie sich, dass das Token nicht abläuft, und dass Sie über genügend Gerätelizenzen für die Unternehmensportal-App verfügen, um eine ordnungsgemäße Bereitstellung zu ermöglichen.

9. Wenn Sie ein Token für **Unternehmensportal mit VPP installieren** ausgewählt haben, können Sie das Gerät unmittelbar nach Beendigung des Setup-Assistenten in den Einzelanwendungsmodus (insbesondere die Unternehmensportal-App) sperren. Wählen Sie für **Run Company Portal in Single App Mode until authentication** (Unternehmensportal bis zur Authentifizierung im Einzelanwendungsmodus ausführen) **Ja** aus, um diese Option festzulegen. Der Benutzer muss sich erst authentifizieren, indem er sich über das Unternehmensportal anmeldet, um das Gerät zu verwenden.

    Mehrstufige Authentifizierung wird auf einem einzelnen Gerät, das im Einzelanwendungsmodus gesperrt ist, nicht unterstützt. Diese Einschränkung gibt es, weil das Gerät nicht zu einer anderen App wechseln kann, um den zweiten Authentifizierungsfaktor abzuschließen. Daher muss sich der zweite Faktor, wenn Sie mehrstufige Authentifizierung auf einem Einzelanwendungsmodus-Gerät verwenden möchten, auf einem anderen Gerät befinden.

    Dieses Feature wird nur für iOS/iPadOS 11.3.1 und höher unterstützt.

   ![Screenshot: Einzelanwendungsmodus](./media/device-enrollment-program-enroll-ios/single-app-mode.png)

10. Wenn Sie möchten, dass Geräte, die dieses Profil verwenden, überwacht werden, wählen Sie **Ja** für **Überwacht** aus.

    ![Screenshot der Geräteverwaltungseinstellungen](./media/device-enrollment-program-enroll-ios/supervisedmode.png)

    Bei **überwachten** Geräten stehen mehr Verwaltungsfunktionen zur Verfügung, und die Aktivierungssperre ist standardmäßig deaktiviert. Microsoft empfiehlt, die automatische Geräteregistrierung als Mechanismus zur Aktivierung des überwachten Modus zu verwenden. Dies gilt insbesondere, wenn Sie eine große Anzahl von iOS-/iPadOS-Geräten bereitstellen. Apple Shared iPad for Business-Geräte müssen überwacht werden.

    Die Benutzer werden auf zweierlei Weise benachrichtigt, dass ihre Geräte überwacht werden:

   - Auf dem Sperrbildschirm wird Folgendes angezeigt: „This iPhone is managed by Contoso“ (Dieses iPhone wird von Contoso verwaltet).
   - Auf dem Bildschirm **Settings** > **General** > **About** (Einstellungen > Allgemein > Info) wird Folgendes angezeigt: „This iPhone is supervised. „This iPhone is supervised. Contoso can monitor your Internet traffic and locate this device“ (Dieses iPhone wird überwacht. Contoso kann Ihren Internetdatenverkehr überwachen und dieses Gerät suchen.)

     > [!NOTE]
     > Ein Gerät, das ohne Überwachung registriert wurde, kann nur mithilfe von Apple Configurator auf den Status „Überwacht“ zurückgesetzt werden. Wenn Sie das Gerät auf diese Weise zurücksetzen möchten, müssen Sie ein iOS-/iPadOS-Gerät über ein USB-Kabel mit einem Mac verbinden. Erfahren Sie mehr über dieses Thema in der [Dokumentation zu Apple Configurator](http://help.apple.com/configurator/mac/2.3).

11. Wählen Sie aus, ob für Geräte mit diesem Profil die gesperrte Registrierung verwendet werden soll. Wenn **Gesperrte Registrierung** aktiviert ist, sind die iOS-/iPadOS-Einstellungen deaktiviert, mit denen das Verwaltungsprofil aus dem Menü **Einstellungen** entfernt werden kann. Nach der Geräteregistrierung können Sie diese Einstellung nicht ändern, ohne das Gerät zurückzusetzen. Bei solchen Geräten muss der Verwaltungsmodus **Überwacht** auf *Ja* eingestellt sein. 

    > [!NOTE]
    > Nachdem das Gerät mit **Gesperrte Registrierung** registriert wurde, können Benutzer nicht mehr **Gerät entfernen** oder **Zurück auf Werkseinstellungen** in der Unternehmensportal-App verwenden. Die Optionen sind für den Benutzer nicht verfügbar. Der Benutzer wird auch nicht in der Lage sein, das Gerät auf der Website des Unternehmensportals zu entfernen (https://portal.manage.microsoft.com).
    > Wenn ein BYOD-Gerät in ein Apple-Gerät für die automatische Geräteregistrierung umgewandelt und mit einem Profil mit **Gesperrte Registrierung** registriert wird, kann der Benutzer 30 Tage lang **Gerät entfernen** und **Zurück auf Werkseinstellungen** verwenden. Anschließend sind die Optionen deaktiviert oder nicht verfügbar. Referenz: https://help.apple.com/configurator/mac/2.8/#/cad99bc2a859.

12. Wenn Sie sich oben für die Optionen **Ohne Benutzeraffinität registrieren** und **Überwacht** entschieden haben, müssen Sie sich entscheiden, ob die Geräte als [Apple Shared iPad for Business-Geräte](https://support.apple.com/guide/mdm/shared-ipad-overview-cad7e2e0cf56/web) konfiguriert werden sollen oder nicht. Wenn Sie **Ja** für **Shared iPad** festlegen, können sich mehrere Benutzer beim gleichen Gerät anmelden. Die Benutzer authentifizieren sich mit ihrer verwalteten Apple-ID und ihren föderierten Authentifizierungskonten oder über eine temporäre Sitzung (z. B. mit einem Gastkonto). Für diese Option ist iOS/iPadOS 13.4 oder höher erforderlich.

    Wenn Sie Ihre Geräte als Apple Shared iPad for Business-Geräte konfigurieren möchten, müssen Sie einen Wert für die Einstellung **Maximale Anzahl zwischengespeicherter Benutzer** festlegen. Legen Sie die Anzahl der Benutzer fest, die Sie für das Shared iPad-Gerät erwarten. Sie können bis zu 24 Benutzer auf einem Gerät mit 32 GB oder 64 GB zwischenspeichern. Wenn Sie sich für eine sehr geringe Anzahl entscheiden, kann es eine Weile dauern, bis die Daten Ihrer Benutzer nach der Anmeldung beim Gerät eingehen. Wenn Sie sich für eine sehr hohe Anzahl entscheiden, verfügen Ihre Benutzer möglicherweise nicht über ausreichend Speicherplatz.  

    > [!NOTE]
    > Wenn Sie Apple Shared iPad for Business einrichten möchten, legen Sie Folgendes fest: 
    > - **Benutzeraffinität** = **Ohne Benutzeraffinität registrieren** 
    > - **Überwacht** = **Ja** 
    > - **Shared iPad** = **Ja**
    > Temporäre Sitzungen sind standardmäßig aktiviert und ermöglichen Ihren Benutzern die Anmeldung bei einem Shared iPad-Gerät ohne ein verwaltetes Apple-ID-Konto. Sie können temporäre Sitzungen auf Shared iPad-Geräten deaktivieren, indem Sie die [Einstellungen für Geräteeinschränkungen](../configuration/device-restrictions-ios.md) für iOS/iPadOS und das Shared iPad-Gerät konfigurieren.  

13. Wählen Sie aus, ob für Geräte, für die dieses Profil verwendet wird, die Option **Mit Computern synchronisieren** verfügbar sein soll. Wenn Sie **Apple Configurator nach Zertifikat zulassen** auswählen, müssen Sie unter **Apple Configurator-Zertifikate** ein Zertifikat auswählen.

     > [!NOTE]
     > Wenn **Mit Computern synchronisieren** auf **Alle ablehnen** festgelegt ist, wird der Port auf iOS- und iPadOS-Geräten beschränkt. Der Port kann ausschließlich zum Laden verwendet werden. Die Verwendung von iTunes oder Apple Configurator 2 an diesem Port wird blockiert.
     Wenn **Sync with computers** (Mit Computern synchronisieren) auf **Apple Configurator nach Zertifikat zulassen** festgelegt ist, stellen Sie sicher, dass Sie eine lokale Kopie des Zertifikats speichern, auf die Sie später zugreifen können. Sie können keine Änderungen an der hochgeladenen Kopie vornehmen. Es ist wichtig, dieses Zertifikat beizubehalten, damit es weiterhin zugänglich ist. Zum Herstellen einer Verbindung mit dem iOS/iPadOS-Gerät über ein macOS-Gerät oder PC muss dasselbe Zertifikat auf dem Gerät installiert sein, von dem die Verbindung mit dem iOS/iPadOS-Gerät ausgeht, das mit dem automatischen Geräteregistrierungsprofil mit dieser Konfiguration und dem Zertifikat registriert wurde.

14. Wenn Sie im vorherigen Schritt **Apple Configurator nach Zertifikat zulassen** ausgewählt haben, müssen Sie ein Apple Configurator-Zertifikat zum Importieren auswählen.

15. Sie können ein Benennungsformat für Geräte angeben, das sowohl bei deren Registrierung als auch bei jeder ihrer späteren Anmeldungen automatisch angewendet wird. Um eine Benennungsvorlage zu erstellen, wählen Sie **Ja** unter **Vorlage für Gerätenamen anwenden** aus. Geben Sie dann in das Feld **Vorlage für Gerätenamen** den Namen der Vorlage ein, die für die Geräte verwendet werden soll, für die dieses Profil verwendet wird. Sie können ein Vorlagenformat angeben, das den Gerätetyp und die Seriennummer enthält. Die Vorlage für den Gerätenamen unterstützt iPhone, iPad und iPod Touch. 
16. Klicken Sie auf **Weiter: Anpassung des Setup-Assistenten**.

17. Wählen Sie **Anpassung des Setup-Assistenten** aus, um die folgenden Profileinstellungen zu konfigurieren: ![Anpassung des Setup-Assistenten](./media/device-enrollment-program-enroll-ios/setupassistantcustom.png)


    | Abteilungseinstellungen | Beschreibung |
    |---|---|
    | <strong>Abteilungsname</strong> | Wird angezeigt, wenn der Benutzer während der Aktivierung auf <strong>Info zur Konfiguration</strong> tippt. |
    |    <strong>Abteilungstelefonnummer</strong>     | Wird angezeigt, wenn der Benutzer während der Aktivierung auf die Schaltfläche <strong>Benötigen Sie Hilfe?</strong> klickt. |

    Sie können festlegen, dass die Bildschirme des Setup-Assistenten während des Setups eines Benutzers auf dem Gerät ausgeblendet werden.
    - Wenn Sie auf **Ausblenden** klicken, wird der Bildschirm nicht während des Setups angezeigt. Nach dem Setup des Geräts kann der Benutzer weiterhin zum Menü **Einstellungen** navigieren, um das Feature einzurichten.
    - Wenn Sie auf **Anzeigen** klicken, wird der Bildschirm während des Setups angezeigt. Gelegentlich kann der Benutzer den Bildschirm überspringen, ohne weitere Maßnahmen ergreifen zu müssen. Er kann aber später zum Gerätemenü **Einstellungen** navigieren, um das Feature einzurichten. 


    | Bildschirmeinstellungen des Setup-Assistenten | Wenn Sie während des Setups des Geräts auf **Anzeigen** klicken, führt das Gerät die folgenden Aktionen durch: |
    |------------------------------------------|------------------------------------------|
    | <strong>Kennung</strong> | Es fordert den Benutzer auf, eine Kennung einzugeben. Verlangen Sie immer eine Kennung (Passcode) für ungeschützte Geräte, es sei denn, der Zugriff ist auf andere Weise geschützt (etwa im Kioskmodus, in dem das Gerät auf eine App beschränkt wird). Für iOS/iPadOS 7.0 und höher |
    | <strong>Standortdienste</strong> | Es fordert den Benutzer auf, seinen Standort anzugeben. Für macOS 10.11 und höher sowie iOS/iPadOS 7.0 und höher |
    | <strong>Wiederherstellen</strong> | Es zeigt den Bildschirm „Apps & Daten“ an. Über diesen Bildschirm hat der Benutzer die Möglichkeit, Daten aus der iCloud-Sicherung wiederherzustellen oder aus dieser zu übertragen, wenn er das Gerät einrichtet. Für macOS 10.9 und höher sowie iOS/iPadOS 7.0 und höher |
    | <strong>iCloud und Apple-ID</strong> | Es lässt zu, dass der Benutzer sich mit seiner Apple-ID anmelden und iCloud verwenden kann. Für macOS 10.9 und höher sowie iOS/iPadOS 7.0 und höher   |
    | <strong>Geschäftsbedingungen</strong> | Es verlangt, dass der Benutzer die Nutzungsbedingungen von Apple akzeptiert. Für macOS 10.9 und höher sowie iOS/iPadOS 7.0 und höher |
    | <strong>Touch ID</strong> | Es lässt zu, dass der Benutzer die Identifikation per Fingerabdruck für das Gerät einrichtet. Für macOS 10.12.4 und höher sowie iOS/iPadOS 8.1 und höher |
    | <strong>Apple Pay</strong> | Es lässt zu, dass der Benutzer Apple Pay auf dem Gerät einrichtet. Für macOS 10.12.4 und höher sowie iOS/iPadOS 7.0 und höher |
    | <strong>Zoom</strong> | Es lässt zu, dass der Benutzer die Anzeige vergrößern bzw. verkleinern kann, während er das Gerät einrichtet. Für iOS/iPadOS 8.3 und höher |
    | <strong>Siri</strong> | Es lässt zu, dass der Benutzer Siri einrichtet. Für macOS 10.12 und höher sowie iOS/iPadOS 7.0 und höher |
    | <strong>Diagnosedaten</strong> | Zeigt dem Benutzer den Bildschirm „Diagnose“ an. Über diesen Bildschirm kann der Benutzer Diagnosedaten an Apple senden. Für macOS 10.9 und höher sowie iOS/iPadOS 7.0 und höher |
    | <strong>Displayfarbton</strong> | Geben Sie dem Benutzer die Möglichkeit, den Anzeigefarbton zu aktivieren. Für macOS 10.13.6 und höher sowie iOS/iPadOS 9.3.2 und höher |
    | <strong>Datenschutz</strong> | Lassen Sie den Benutzer auf den Bildschirm Privatsphäre zugreifen. Für macOS 10.13.4 und höher sowie iOS/iPadOS 11.3 und höher |
    | <strong>Android-Migration</strong> | Ermöglichen Sie dem Benutzer die Migration von Dateien von einem Android-Gerät. Für iOS/iPadOS 9.0 und höher|
    | <strong>iMessage und FaceTime</strong> | Ermöglichen Sie dem Benutzer, iMessage und FaceTime einzurichten. Für iOS/iPadOS 9.0 und höher |
    | <strong>Onboarding</strong> | Zeigen Sie den Benutzern Onboarding-Bildschirme zu Informationszwecken an, z. B. „Deckblatt“, „Multitasking“ oder „Steuerungscenter“. Für iOS/iPadOS 11.0 und höher |
    | <strong>Watch-Migration</strong> | Ermöglichen Sie dem Benutzer die Migration von Dateien von einem Überwachungsgerät. Für iOS/iPadOS 11.0 und höher|
    | <strong>Bildschirmzeit</strong> | Aktivieren Sie den Bildschirm „Bildschirmzeit“. Für macOS 10.15 und höher sowie iOS/iPadOS 12.0 und höher |
    | <strong>Softwareupdate</strong> | Lassen Sie erforderliche Softwareupdates anzeigen. Für iOS/iPadOS 12.0 und höher |
    | <strong>SIM-Setup</strong> | Ermöglichen Sie dem Benutzer, einen Mobilfunkplan hinzuzufügen. Für iOS/iPadOS 12.0 und höher |
    | <strong>Darstellung</strong> | Zeigen Sie den Bildschirm „Darstellung“ für den Benutzer an. Für macOS 10.14 und höher sowie iOS/iPadOS 13.0 und höher |
    | <strong>Express-Sprache</strong>| Zeigen Sie den Bildschirm „Express-Sprache“ für den Benutzer an. |
    | <strong>Bevorzugte Sprache</strong> | Ermöglichen Sie dem Benutzer, seine **Bevorzugte Sprache** auszuwählen. |
    | <strong>Migration von Gerät zu Gerät</strong> | Ermöglichen Sie dem Benutzer, Daten von seinem alten Gerät auf dieses Gerät zu migrieren. Für iOS/iPadOS 13.0 und höher |
    | <strong>Registrierung</strong> | Mit dieser Einstellung wird dem Benutzer die Registrierungsanzeige angezeigt. Für macOS 10.9 und höher |
    | <strong>FileVault</strong> | Mit dieser Einstellung wird dem Benutzer die Anzeige für die FileVault 2-Verschlüsselung angezeigt. Für macOS 10.10 und höher |
    | <strong>iCloud-Diagnose</strong> | Mit dieser Einstellung wird dem Benutzer die Anzeige für die iCloud-Analyse angezeigt. Für macOS 10.12.4 und höher |
    | <strong>iCloud-Speicher</strong> | Mit dieser Einstellung wird dem Benutzer die Anzeige für Dokumente und den Desktop angezeigt. Für macOS 10.13.4 und höher |
    

18. Wählen Sie **Weiter** aus, um zur Seite **Überprüfen + erstellen** zu wechseln.

19. Wählen Sie **Erstellen** aus, um das Profil zu speichern.

### <a name="dynamic-groups-in-azure-active-directory"></a>Dynamische Gruppen in Azure Active Directory

Sie können das Registrierungsfeld **Name** zum Erstellen einer dynamischen Gruppe in Azure Active Directory verwenden. Weitere Informationen finden Sie unter [Dynamische Gruppen in Azure Active Directory](/azure/active-directory/users-groups-roles/groups-dynamic-membership).

Sie können den Profilnamen zum Definieren des Parameters [enrollmentProfileName](/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices) verwenden, um Geräte mit diesem Registrierungsprofil zuzuweisen.

Stellen Sie für die schnellste Richtlinienbereitstellung auf ADE-Geräten mit Benutzeraffinität vor dem Einrichten des Geräts sicher, dass der Benutzer, der sich registriert ein Mitglied einer AAD-Benutzergruppe ist. 

Das Zuweisen dynamischer Gruppen zu Registrierungsprofilen kann zu einer gewissen Verzögerung bei der Bereitstellung von Anwendungen und Richtlinien auf Geräten nach der Registrierung führen.


## <a name="sync-managed-devices"></a>Synchronisieren verwalteter Geräte
Nachdem Intune nun die Berechtigung zum Verwalten Ihrer Geräte besitzt, können Sie Intune mit Apple synchronisieren, um Ihre verwalteten Geräte in Intune im Azure-Portal anzuzeigen.

1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Devices** > **iOS/iPadOS** > **iOS/iPadOS enrollment** > **Enrollment program tokens** (Geräte > iOS/iPadOS > iOS/iPadOS-Registrierung > Token für Registrierungsprogramm).

2. Wählen Sie ein Token in der Liste aus, und klicken Sie auf **Geräte** > **Synchronisieren**. ![Screenshot des Knotens „Geräte des Registrierungprogramms“ und des Links „Synchronisierung“](./media/device-enrollment-program-enroll-ios/image06.png)

   Zur Befolgung der Apple-Bedingungen für zulässigen Datenverkehr des Registrierungsprogramms erzwingt Intune die folgenden Einschränkungen:
   - Eine vollständige Synchronisation kann nicht öfter als einmal alle sieben Tage erfolgen. Während einer vollständigen Synchronisierung ruft Intune die vollständig aktualisierte Liste der Seriennummern auf, die dem mit Intune verbundenen Apple MDM-Server zugewiesen sind. Wenn ein ADE-Gerät aus dem Intune-Portal gelöscht wird, sollte seine Zuweisung zum Apple-MDM-Server im ADE-Portal aufgehoben werden. Wird seine Zuweisung nicht aufgehoben, wird es solange nicht erneut in Intune importiert, bis die vollständige Synchronisierung ausgeführt wird.   
   - Die Synchronisierung wird automatisch alle 12 Stunden ausgeführt. Sie können eine Synchronisierung ebenfalls durchführen, indem Sie auf die Schaltfläche **Synchronisierung** klicken (nicht öfter als einmal alle 15 Minuten). Alle Synchronisierungsanforderungen müssen innerhalb von 15 Minuten abgeschlossen werden. Die Schaltfläche **Synchronisierung** bleibt bis zum Abschluss der Synchronisierung deaktiviert. Durch diese Synchronisierung werden vorhandene Gerätestatus aktualisiert und neue Geräte importiert, die dem Apple MDM-Server zugewiesen sind.   


## <a name="assign-an-enrollment-profile-to-devices"></a>Zuweisen eines Registrierungsprofils an Geräte
Sie müssen Geräten ein Profil des Registrierungsprogramms zuweisen, bevor Sie mit der Registrierung beginnen können.

>[!NOTE]
>Sie können auch auf dem Blatt **Apple-Seriennummern** Profilen Seriennummern zuweisen.

1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Devices** > **iOS/iPadOS** > **iOS/iPadOS enrollment** > **Enrollment Program Tokens** (Geräte > iOS/iPadOS > iOS/iPadOS-Registrierung > Token für Registrierungsprogramm), und wählen Sie in der Liste ein Token aus.
2. Wählen Sie **Geräte** aus, wählen Sie in der Liste die Geräte aus, und wählen Sie dann **Profil zuweisen** aus.
3. Wählen Sie unter **Profil zuweisen** ein Profil für die Geräte aus, und klicken Sie dann auf **Zuweisen**.

### <a name="assign-a-default-profile"></a>Zuweisen eines Standardprofils

Sie können ein Standardprofil auswählen, das auf alle Geräte angewendet wird, die sich mit einem bestimmten Token registrieren.

1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Devices** > **iOS/iPadOS** > **iOS/iPadOS enrollment** > **Enrollment Program Tokens** (Geräte > iOS/iPadOS > iOS/iPadOS-Registrierung > Token für Registrierungsprogramm), und wählen Sie in der Liste ein Token aus.
2. Wählen Sie **Standardprofil festlegen** aus, wählen Sie ein Profil in der Dropdownliste aus, und wählen Sie dann **Speichern** aus. Dieses Profil wird auf alle Geräte angewendet, die sich mit dem Token registrieren.

## <a name="distribute-devices"></a>Verteilen von Geräten
Sie haben die Verwaltung und Synchronisierung zwischen Apple und Intune aktiviert und haben ein Profil zugewiesen, damit Ihre ADE-Geräte registriert werden können. Sie können jetzt Geräte an Benutzer verteilen. Für Geräte mit Benutzeraffinität muss jedem Benutzer eine Intune-Lizenz zugewiesen werden. Geräte ohne Benutzeraffinität benötigen eine Gerätelizenz. Ein aktiviertes Gerät kann kein Registrierungsprofil anwenden, bis das Gerät zurückgesetzt wurde.

Informationen finden Sie unter [Registrieren Ihres iOS-/iPadOS-Geräts in Intune mit dem Programm zur Geräteregistrierung](../user-help/enroll-your-device-dep-ios.md).

## <a name="renew-an-automated-device-enrollment-token"></a>Erneuern eines Tokens für die automatische Geräteregistrierung  

> [!NOTE]
> Zusätzlich zur jährlichen Erneuerung Ihres ADE-Tokens müssen Sie das Token Ihres Registrierungsprogramms in Intune und Apple Business Manager erneuern, wenn das Kennwort der verwalteten Apple-ID für den Benutzer geändert wird, der das Token in Apple Business Manager eingerichtet hat, oder wenn dieser Benutzer Ihre Apple Business Manager-Organisation verlässt.

1. Navigieren Sie zu business.apple.com.
2. Klicken Sie auf **Einstellungen** (unten links).
3. Wählen Sie unter  **MDM Servers** (MDM-Server) Ihren MDM-Server aus, der dem ADE/DEP-Token zugeordnet ist, das Sie erneuern möchten.
4. Klicken Sie auf **Download token** (Token herunterladen).

    ![Screenshot von „Neues Token generieren“](./media/device-enrollment-program-enroll-ios/generatenewtoken.png)

5. Klicken Sie in der Eingabeaufforderung auf „Download server token“ (Servertoken herunterladen).
> [!NOTE]
> Klicken Sie nicht auf **Download server token** (Servertoken herunterladen), wenn Sie das Token nicht (wie in der Eingabeaufforderung erwähnt) erneuern möchten, da sonst das aktuell von Intune verwendete Token (oder eine andere MDM-Lösung) ungültig wird. Wenn Sie das Token bereits heruntergeladen haben, stellen Sie sicher, dass Sie mit den nächsten Schritten fortfahren, bis das Token erneuert wird.

6. Klicken Sie nach dem Herunterladen des Tokens im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Devices** > **iOS/iPadOS** > **iOS/iPadOS enrollment** > **Enrollment Program Tokens** (Geräte > iOS/iPadOS > iOS/iPadOS-Registrierung > Token für Registrierungsprogramm), und wählen Sie ein Token aus.
    ![Screenshot der Registrierungsprogrammtoken.](./media/device-enrollment-program-enroll-ios/enrollmentprogramtokens.png)

7. Klicken Sie auf **Token erneuern**, und geben Sie die Apple-ID ein, die zum Erstellen des ursprünglichen Tokens verwendet wurde (falls nicht automatisch ausgefüllt).  
    ![Screenshot von „Token erneuern“](./media/device-enrollment-program-enroll-ios/renewtoken.png)

8. Laden Sie das neu heruntergeladene Token hoch.

9. Klicken Sie auf **Weiter**, um zur Seite **Bereichstags** zu gelangen, und weisen Sie bei Bedarf Bereichstags zu.

10. Klicken Sie auf **Token erneuern**. Es wird eine Bestätigung angezeigt, dass das Token erneuert wurde.   
    ![Screenshot der Bestätigung](./media/device-enrollment-program-enroll-ios/confirmation.png)

## <a name="delete-an-automated-device-enrollment-token-from-intune"></a>Löschen eines Tokens für die automatische Geräteregistrierung aus Intune

Sie können Token des Registrierungsprofils aus Intune löschen, solange Folgendes gilt:
- Dem Token sind keine Geräte zugewiesen
- Dem Standardprofil sind keine Geräte zugewiesen

1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Geräte** > **iOS/macOS** > **iOS/macOS enrollment (iOS/macOS-Registrierung)**  > **Enrollment Program Tokens** (Registrierungsprogrammtoken). Wählen Sie das Token und dann **Geräte** aus.
2. Löschen Sie alle Geräte, die dem Token zugewiesen sind.
3. Wechseln Sie zu **Geräte** > **iOS/macOS** > **iOS/macOS enrollment (iOS/macOS-Registrierung)**  > **Enrollment Program Tokens** (Registrierungsprogrammtoken). Wählen Sie das Token und dann **Profile** aus.
4. Wenn ein Standardprofil vorhanden ist, löschen Sie es.
5. Wechseln Sie zu **Geräte** > **iOS/macOS** > **iOS/macOS enrollment (iOS/macOS-Registrierung)**  > **Enrollment Program Tokens** (Registrierungsprogrammtoken). Wählen Sie das Token und dann **Löschen** aus.
