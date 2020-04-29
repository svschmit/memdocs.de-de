---
title: Tutorial – Verwenden von Apple Business Manager oder des Programms zur Geräteregistrierung zum Registrieren von iOS-/iPadOS-Geräten in Intune
titleSuffix: Microsoft Intune
description: In diesem Tutorial richten Sie die Apple-Features für Unternehmensgeräteregistrierung über ABM ein, um iOS-/iPadOS-Geräte in Intune zu registrieren.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/30/2019
ms.topic: tutorial
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
Customer intent: As an Intune admin, I want to set up the Apple's corporate device enrollment features so that corporate devices can automatically enroll in Intune.
ms.collection: M365-identity-device-management
ms.openlocfilehash: a3a949738056c9acf33ef09e28f7664690dfd77f
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078905"
---
# <a name="tutorial-use-apples-corporate-device-enrollment-features-in-apple-business-manager-abm-to-enroll-iosipados-devices-in-intune"></a>Tutorial: Verwenden der Apple-Features für Unternehmensgeräteregistrierung in Apple Business Manager (ABM) zum Registrieren von iOS-/iPadOS-Geräten in Intune
Die Geräteregistrierungsfeatures in Apple Business Manager vereinfachen das Registrieren von Geräten. Intune unterstützt auch das ältere Portal für das Programm zur Geräteregistrierung (Device Enrollment Program, DEP), doch wir empfehlen Ihnen einen Neustart mit Apple Business Manager. Mit Microsoft Intune und der Apple-Unternehmensgeräteregistrierung werden Geräte automatisch sicher registriert, wenn der Benutzer das Gerät zum ersten Mal einschaltet. Sie können Geräte daher für mehrere Benutzer bereitstellen, ohne jedes Gerät einzeln einrichten zu müssen. 

In diesem Tutorial lernen Sie Folgendes:
> [!div class="checklist"]
> * Abrufen eines Tokens für Apple-Geräteregistrierung
> * Synchronisieren verwalteter Geräte mit Intune
> * Erstellen eines Registrierungsprofils
> * Zuweisen des Registrierungsprofils an Geräte

Wenn Sie über kein Intune-Abonnement verfügen, [registrieren Sie sich für eine kostenlose Testversion](../fundamentals/free-trial-sign-up.md).

## <a name="prerequisites"></a>Voraussetzungen
- Geräte, die über [Apple Business Manager](https://business.apple.com) oder das [Apple-Programm zur Geräteregistrierung ](http://deploy.apple.com) erworben wurden
- Die [Autorität für die Verwaltung mobiler Geräte](../fundamentals/mdm-authority-set.md) muss festgelegt sein
- Abrufen eines [Apple-MDM-Push-Zertifikats](apple-mdm-push-certificate-get.md)

## <a name="get-an-apple-device-enrollment-token"></a>Abrufen eines Tokens für Apple-Geräteregistrierung
Vor der Registrierung von iOS-/iPadOS-Geräten mit den Apple-Features für Unternehmensregistrierung benötigen Sie ein Token für die Apple-Geräteregistrierung, d.h. eine PEM-Datei. Mit diesem Token kann Intune Informationen zu Apple-Geräten synchronisieren, die Ihrem Unternehmen gehören. Damit kann Intune außerdem Registrierungsprofile zu Apple hochladen und diesen Profilen Geräte zuweisen.

Sie verwenden das Apple-Portal zum Erstellen eines Tokens für die Geräteregistrierung. Sie verwenden die Portale auch, um Intune Geräte zur Verwaltung zuzuweisen.

1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Geräte** > **iOS** > **iOS enrollment** (iOS-Registrierung) > **Enrollment Program Tokens** (Registrierungsprogrammtoken) > **Hinzufügen**.

2. Erteilen Sie Microsoft die Berechtigung, Benutzer- und Geräteinformationen an Apple zu senden, indem Sie auf **Ich stimme zu** klicken.

   ![Screenshot des Bereichs „Registrierungsprogrammtoken“ im Arbeitsbereich „Apple-Zertifikate“ zum Herunterladen des öffentlichen Schlüssels](./media/tutorial-use-device-enrollment-program-enroll-ios/add-enrollment-program-token-pane.png)

3. Wählen Sie **Laden Sie Ihr Zertifikat mit öffentlichem Schlüssel herunter** aus, um die Verschlüsselungsschlüsseldatei (PEM) herunterzuladen und lokal zu speichern. Die PEM-Datei wird verwendet, um ein Vertrauensstellungszertifikat vom Apple-Portal anzufordern.

4. Wählen Sie **Create a token for Apple's Device Enrollment Program** (Token für das Programm zur Geräteregistrierung von Apple erstellen) aus, um das Portal des Bereitstellungsprogramms von Apple zu öffnen. Melden Sie sich mit der Apple-ID Ihres Unternehmens an. Diese Apple-ID kann später zum Erneuern Ihres Tokens verwendet werden.

5. Wählen Sie im [Portal des Bereitstellungsprogramms](https://deploy.apple.com) von Apple die Option **Erste Schritte** für das **Programm zur Geräteregistrierung** aus. Möglicherweise ist Ihr Prozess etwas anders als die folgenden Schritte in [Apple Business Manager](https://business.apple.com).

4. Wählen Sie auf der Seite **Server verwalten** die Option **MDM-Server hinzufügen** aus.

5. Geben Sie *TestMDMServer* als **MDM-Servernamen** ein, und klicken Sie dann auf **Weiter**. Der Servername dient als Referenz zum Identifizieren des MDM-Servers (mobile device management, Verwaltung mobiler Geräte). Es handelt sich nicht um den Namen oder die URL des Microsoft Intune-Servers.

6. Das Dialogfeld **&lt;Servername&gt; hinzufügen** wird geöffnet, und die Meldung **Laden Sie Ihren öffentlichen Schlüssel hoch** wird angezeigt. Wählen Sie **Datei auswählen** aus, um die PEM-Datei hochzuladen, und wählen Sie anschließend **Weiter** aus.

6. Wechseln Sie zu **Bereitstellungsprogramme** > **Programm zur Geräteregistrierung** > **Geräte verwalten**.
7. Wählen Sie **Seriennummer** unter **Choose Devices By** (Geräte auswählen nach) aus. <!--ask Tiffany about this-->

8. Wählen Sie als Nächstes für **Aktion auswählen** die Option **Zu Server zuweisen** aus. Wählen Sie den für Microsoft Intune angegebenen &lt;Servernamen&gt; und anschließend **OK** aus. Das Apple-Portal weist die angegebenen Geräte dem Intune-Server für die Verwaltung zu und zeigt dann **Zuweisung abgeschlossen** an.

   Wechseln Sie im Apple-Portal zu **Bereitstellungsprogramme** &gt; **Programm zur Geräteregistrierung** &gt; **Zuweisungsverlauf anzeigen**, um eine Liste der Geräte und ihre MDM-Server-Zuordnung anzuzeigen.

9. Geben Sie die Apple-ID, die zum Erstellen dieses Tokens verwendet wurde, für die zukünftige Verwendung im Azure-Portal in Intune an.

    ![Screenshot der Angabe der Apple-ID zur Erstellung des Registrierungsprogrammtokens und Navigieren zu diesem Token](./media/tutorial-use-device-enrollment-program-enroll-ios/image03.png)

10. Navigieren Sie im Feld **Apple-Token** zur Zertifikatsdatei (PEM), und wählen Sie **Öffnen** und dann **Erstellen** aus. 

11. Wenn Sie Bereichsmarkierungen anwenden möchten, um genau festzulegen, welche Administratoren auf dieses Token zugreifen können, wählen Sie „Bereiche“ aus.

## <a name="create-an-apple-enrollment-profile"></a>Erstellen eines Apple-Registrierungsprofils
Nachdem Sie Ihr Token installiert haben, können Sie nun ein Registrierungsprofil für unternehmenseigene iOS-/iPadOS-Geräte erstellen. Ein Geräteregistrierungsprofil definiert die Einstellungen, die während der Registrierung auf eine Gruppe von Geräten angewendet werden.

1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Geräte** > **iOS** > **iOS enrollment** (iOS-Registrierung) > **Enrollment Program Tokens** (Registrierungsprogrammtoken).

2. Wählen Sie das soeben installierte Token aus, und klicken Sie auf **Profile** > **Profil erstellen** > **iOS**.

3. Geben Sie auf der Seite **Grundlagen** den **Namen** *TestProfile* und die **Beschreibung** *Test von ADE für iOS-/iPadOS-Geräte* ein. Benutzer können diese Informationen nicht sehen.

4. Wählen Sie **Weiter** aus.

5. Entscheiden Sie auf der Seite **Verwaltungseinstellungen**, ob Ihre Geräte mit oder ohne **Benutzeraffinität** registriert werden sollen. „Benutzeraffinität“ ist für Geräte vorgesehen, die von bestimmten Benutzern verwendet werden. Wenn Ihre Benutzer das Unternehmensportal für Dienste wie das Installieren von Apps verwenden möchten, wählen Sie **Mit Benutzeraffinität registrieren** aus. Wenn Ihre Benutzer das Unternehmensportal nicht benötigen oder wenn Sie das Gerät für viele Benutzer bereitstellen möchten, wählen Sie **Ohne Benutzeraffinität registrieren** aus.

6. Wenn Sie sich für die Registrierung mit Benutzeraffinität entschieden haben, wird die Option **Wählen Sie aus, wo Benutzer sich authentifizieren müssen** angezeigt. Entscheiden Sie, ob Sie sich über das Unternehmensportal oder den Apple Setup-Assistenten authentifizieren möchten.
   - **Unternehmensportal**: Wählen Sie diese Option aus, um die Multi-Factor Authentication zu verwenden, Benutzern die Möglichkeit zu geben, Kennwörter bei der ersten Anmeldung zu ändern, oder Benutzer aufzufordern, ihre abgelaufenen Kennwörter während der Registrierung zurückzusetzen. Wenn Sie die Unternehmensportal-App automatisch auf den Geräten der Endbenutzer aktualisieren möchten, stellen Sie das Unternehmensportal über das Apple Volume Purchase Program (VPP) separat als erforderliche App für diese Benutzer bereit.
   - **Setup-Assistent**: Wählen Sie diese Option aus, um die von Apple bereitgestellte einfache HTTP-Authentifizierung über den Apple Setup-Assistenten zu verwenden.
  
7. Wenn Sie sich mit Benutzeraffinität anmelden und sich beim Unternehmensportal authentifizieren möchten, wird die Option **Unternehmensportal mit VPP installieren** angezeigt. Wenn Sie das Unternehmensportal mit einem VPP-Token installieren, muss Ihr Benutzer keine Apple-ID und kein Kennwort eingeben, um das Unternehmensportal während der Registrierung aus dem App Store herunterzuladen. Wählen Sie unter **Unternehmensportal mit VPP installieren** die Option **Token verwenden:** , um ein VPP-Token auszuwählen, dem kostenlose Lizenzen des Unternehmensportals zur Verfügung stehen. Wenn Sie VPP zum Bereitstellen des Unternehmensportals nicht verwenden möchten, wählen Sie die Option **VPP nicht verwenden** aus. 

8. Wenn Sie ausgewählt haben, dass Sie mit „Benutzeraffinität“, „Über das Unternehmensportal authentifizieren“ und „Unternehmensportal mit VPP installieren“ registrieren möchten, entscheiden Sie, ob Sie das Unternehmensportal bis zur Authentifizierung im Einzelanwendungsmodus ausführen möchten. Mithilfe dieser Einstellung können Sie sicherstellen, dass der Benutzer so lange auf keine anderen Apps zugreifen kann, bis er die Unternehmensregistrierung abgeschlossen hat. Wenn Sie den Benutzer bis zum Abschluss der Registrierung auf diesen Ablauf einschränken möchten, wählen Sie unter **Unternehmensportal bis zur Authentifizierung im Einzelanwendungsmodus ausführen** die Option **Ja** aus. 

9. Wählen Sie unter **Geräteverwaltungseinstellungen** die Option **Ja** unter **Überwacht** aus (wenn Sie **Mit Benutzeraffinität registrieren** ausgewählt haben, wird diese automatisch auf **Ja** festgelegt). Überwachte Geräte bieten Ihnen die meisten Verwaltungsoptionen für Ihre unternehmenseigenen iOS-/iPadOS-Geräte.

10. Wählen Sie unter **Gesperrte Registrierung** die Option **Ja** aus, um sicherzustellen, dass Ihre Benutzer die Verwaltung des unternehmenseigenen Geräts nicht entfernen können. 

11. Wählen Sie unter **Mit Computern synchronisieren** eine Option aus, um zu bestimmen, ob die iOS-/iPadOS-Geräte mit Computern synchronisiert werden können.

12. Apple benennt das Gerät standardmäßig mit dem Gerätetyp (z.B. „iPad“). Wenn Sie eine andere Namensvorlage bereitstellen möchten, wählen Sie unter **Vorlage für Gerätenamen anwenden** die Option **Ja** aus. Geben Sie den Namen ein, den Sie auf die Geräte anwenden möchten. Dabei stehen die Zeichenfolgen *{{SERIAL}}* und *{{DEVICETYPE}}* für die Seriennummer und den Gerätetyp jedes Geräts. Wählen Sie andernfalls unter **Vorlage für Gerätenamen anwenden** die Option **Nein** aus.

13. Wählen Sie **Weiter** aus.

14. Auf der Seite **Setup-Assistent**, wählen Sie *Tutorial department* (Tutorialabteilung) für **Abteilungsname** aus. Diese Zeichenfolge wird Benutzern angezeigt, wenn sie während der Geräteaktivierung auf **About configuration** (Informationen zur Konfiguration) tippen.

15. Geben Sie unter **Abteilungstelefonnummer** eine Telefonnummer ein. Diese Nummer wird angezeigt, wenn Benutzer während der Aktivierung auf **Need help** (Hilfe) tippen.

16. Während der Geräteaktivierung können Sie eine Vielzahl von Anzeigen **anzeigen** oder **ausblenden**. Um die nahtloseste Registrierung zu ermöglichen, legen Sie für alle Bildschirme **Ausblenden** fest.

17. Wählen Sie **Weiter** aus, um zur Seite **Überprüfen + erstellen** zu wechseln. Wählen Sie **Erstellen** aus.

## <a name="sync-managed-devices-to-intune"></a>Synchronisieren verwalteter Geräte mit Intune

Nachdem Sie im ABM-, ASM- oder ADE-Portal ein Registrierungsprogrammtoken erstellt und dort dem MDM-Server Geräte zugewiesen haben, können Sie warten, bis diese Geräte mit dem Intune-Dienst synchronisiert werden oder eine Synchronisierung manuell per Push starten. Ohne eine manuelle Synchronisierung kann es bis zu 24 Stunden dauern, bis Geräte im Azure-Portal angezeigt werden.

1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Geräte**  >  **iOS**  >  **iOS enrollment** (iOS-Registrierung)  >  **Enrollment Program Tokens** (Registrierungsprogrammtoken), wählen Sie in der Liste ein Token aus, und klicken Sie auf **Geräte** > **Synchronisieren**.

## <a name="assign-an-enrollment-profile-to-iosipados-devices"></a>Zuweisen eines Registrierungsprofils an iOS-/iPadOS-Geräte

Sie müssen Geräten ein Profil des Registrierungsprogramms zuweisen, bevor Sie mit der Registrierung beginnen können. Diese Geräte werden mit Intune aus Apple synchronisiert und müssen im ABM-, ASM- oder ADE-Portal dem richtigen MDM-Servertoken zugewiesen werden.

1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Geräte**  >  **iOS**  >  **iOS enrollment** (iOS-Registrierung)  >  **Enrollment Program Tokens** (Registrierungsprogrammtoken), und wählen Sie in der Liste Ihr Token aus.
2. Wählen Sie **Geräte** aus, wählen Sie in der Liste die Geräte aus, und wählen Sie dann **Profil zuweisen** aus.
3. Wählen Sie unter **Profil zuweisen** ein Profil für die Geräte aus, und klicken Sie dann auf **Zuweisen**.

## <a name="distribute-devices-to-users"></a>Verteilen von Geräten an Benutzer

Sie haben die Verwaltung und Synchronisierung zwischen Apple und Intune eingerichtet und haben ein Profil zugewiesen, damit Ihre ADE-Geräte registriert werden können. Sie können jetzt Geräte an Benutzer verteilen. Für Geräte mit Benutzeraffinität muss jedem Benutzer eine Intune-Lizenz zugewiesen werden.

## <a name="next-steps"></a>Nächste Schritte

Informieren Sie sich auch über die anderen Optionen, die für das Registrieren von iOS-/iPadOS-Geräten verfügbar sind.

> [!div class="nextstepaction"]
> [Ausführlicher Artikel zur automatischen Registrierung unter iOS/iPadOS](device-enrollment-program-enroll-ios.md)

<!--commenting out because inaccurate>
## Clean up resources
<!--If you don't want to use iOS/iPadOS corporate enrolled devices anymore, you can delete them.>
<!--- If the devices are enrolled in Intune, you must first [delete them from the Azure Active Directory portal](../remote-actions/devices-wipe.md#delete-devices-from-the-azure-active-directory-portal).>
