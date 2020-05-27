---
title: Einrichten des iOS-Gerätezugriffs auf Unternehmensressourcen | Microsoft-Dokumentation
description: Beschreibt die Aktivierung der Verwaltung Ihrer iOS-Geräte über Intune
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/18/2019
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 6eeec7aa-1b07-4ce3-894c-13e09b89bdd4
searchScope:
- User help
ROBOTS: ''
ms.reviewer: tisilv
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: a8d48235141c0b5ad07fbdce4d24e894f8103e6f
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83882411"
---
# <a name="set-up-ios-device-access-to-your-company-resources"></a>Einrichten des iOS-Gerätezugriffs auf Unternehmensressourcen  

Registrieren Sie Ihr iOS-Gerät bei der Intune-Unternehmensportal-App, um sicheren Zugriff auf E-Mails, Dateien und Apps Ihrer Organisation zu erhalten.

Sobald Ihr Gerät registriert ist, gilt es als *verwaltet*. Ihre Organisation kann dem Gerät über einen MDM-Anbieter (Mobile Device Management, Verwaltung mobiler Geräte) wie Intune Richtlinien und Anwendungen zuweisen.  

> [!NOTE]
> Die von unserem Dienst gesammelten Daten werden keinesfalls an Dritte verkauft.  

Um auf Ihrem Gerät auf Ihre Geschäfts-, Schul- oder Uniressourcen zugreifen zu können, müssen Sie Ihr Gerät entsprechend der von Ihrer Organisation bevorzugten Einstellungen konfigurieren. In diesem Artikel wird beschrieben, wie Sie mithilfe des Unternehmensportals Ihr Gerät registrieren und die Einstellungsanforderungen Ihrer Organisation erfüllen können.  
</br>
> [!VIDEO https://www.youtube.com/embed/mJyv6YcHi7c?rel=0]

> [!NOTE]
> Wenn Sie versucht haben, in der E-Mail-App auf Unternehmens-E-Mails zuzugreifen und aufgefordert wurden, Ihr Gerät verwalten zu lassen, sind Sie hier richtig. Befolgen Sie die untenstehenden Anweisungen, um über Ihr iOS-Gerät den Zugriff auf Ihre E-Mails und andere Unternehmensressourcen zu ermöglichen.  


## <a name="what-to-expect-from-the-company-portal-app"></a>Vorteile der Unternehmensportal-App  

### <a name="security"></a>Sicherheit  
Während der ersten Einrichtung werden Sie von der App aufgefordert, sich bei Ihrer Organisation zu authentifizieren. Anschließend werden Sie über alle notwendigen Geräteeinstellungen informiert, die Sie aktualisieren müssen. Beispielsweise legen Organisationen oft Anforderungen an die minimale oder maximale Zeichenanzahl des Kennworts fest, die Sie einhalten müssen.

### <a name="protection"></a>Schutz  
Nachdem Ihr Gerät registriert ist, wird es mithilfe der Unternehmensportal-App weiter geschützt. Wenn Sie beispielsweise eine App aus einer nicht vertrauenswürdigen Quelle installieren, benachrichtigt Sie die Unternehmensportal-App und entzieht Ihnen in manchen Fällen den Zugriff auf Unternehmensdaten. Diese Art von Richtlinie ist in Organisationen üblich und erfordert oft die Deinstallation der nicht vertrauenswürdigen App, ehe Sie Ihre Zugriffsrechte zurück erhalten.  

### <a name="setting-notifications"></a>Benachrichtigungseinstellungen  
Wenn Ihre Organisation nach der Registrierung eine neue Sicherheitsanforderung, wie beispielsweise eine mehrstufige Authentifizierung, durchsetzt, erhalten Sie eine Benachrichtigung von der Unternehmensportal-App. Sie haben dann die Möglichkeit, Ihre Einstellungen so zu ändern, dass Sie von Ihrem Gerät aus weiterarbeiten können.  

Weitere Informationen zur Registrierung finden Sie unter [Was geschieht, wenn ich die Unternehmensportal-App installiere und mein Gerät registriere?](https://docs.microsoft.com//mem/intune/user-help/what-happens-if-you-install-the-company-portal-app-and-enroll-your-device-in-intune-ios).  

## <a name="enroll-your-ios-device"></a>Registrieren Ihres iOS-Geräts  

Navigieren Sie zum App Store, um die [Intune-Unternehmensportal-App](install-and-sign-in-to-the-intune-company-portal-app-ios.md) auf Ihr Gerät herunterzuladen und zu installieren. Außerdem müssen Sie während der Registrierung über eine WLAN-Verbindung verfügen und Zugriff auf Safari haben. 

Eine Unterbrechung von mehr als einigen Minuten während der Registrierung kann dazu führen, dass die App das Setup schließt oder beendet. Öffnen Sie in diesem Fall die Unternehmensportal-App, und wiederholen Sie den Vorgang.  

1. Öffnen Sie das Unternehmensportal, und melden Sie sich mit Ihrem Geschäfts-, Schul- oder Unikonto an.  

2. Wenn Sie gefragt werden, ob Sie Benachrichtigungen vom Unternehmensportal empfangen möchten, tippen Sie auf **Zulassen.** Das Unternehmensportal informiert Sie anhand von Benachrichtigungen, wenn z.B. Ihre Geräteeinstellungen aktualisiert werden müssen.  

3. Klicken Sie auf dem Bildschirm **Zugriff einrichten** auf **Anfang**.   

    ![Beispielscreenshot des Bildschirms „Zugriff einrichten“ im Unternehmensportal.](./media/ios-enrollment-checklist-1909.PNG)  

4. Die Anzeige **Gerät und Registrierungstyp auswählen** wird angezeigt und fordert Sie dazu auf, Ihren Gerätetyp anzugeben.  
    * Tippen Sie auf **<Ihre Organisation> besitzt dieses Gerät**, wenn Sie das Gerät von Ihrer Organisation erhalten haben. Fahren Sie dann ab [Schützen des gesamten Geräts](#secure-entire-device) in diesem Artikel fort, um das Setup abzuschließen.  
    * Tippen Sie auf **Ich besitze dieses Gerät**, wenn Sie ein privates Gerät verwenden. Fahren Sie anschließend mit dem nächsten Schritt fort.  

    Wenn diese Anzeige nicht angezeigt wird, fahren Sie ab [Schützen des gesamten Geräts](#secure-entire-device) fort, um das Setup abzuschließen.  
    
    ![Beispielscreenshot des Unternehmensportals mit der Anzeige „Gerät und Registrierungstyp auswählen“ und den Optionen für den Gerätetyp](./media/ios-device-type-1909.PNG)  


5. Wählen Sie aus, wie die Daten auf Ihrem Gerät geschützt werden sollen, sobald es registriert wurde.  
    * Tippen Sie auf **Gesamtes Gerät schützen**, um alle Apps und Daten auf dem Gerät zu schützen. Fahren Sie anschließend mit dem Abschnitt [Schützen des gesamten Geräts](enroll-your-device-in-intune-ios.md#secure-entire-device), um das Setup abzuschließen.
    * Tippen Sie auf **Nur arbeitsbezogene Apps und Daten schützen**, um nur die Apps und Daten zu schützen, auf die Sie mit Ihrem Geschäftskonto zugreifen. Fahren Sie dann mit dem Abschnitt [Schützen arbeitsbezogener Apps und Daten](enroll-your-device-in-intune-ios.md#secure-work-related-apps-and-data) fort.  

    ![Beispielscreenshot des Unternehmensportals mit der Anzeige „Gerät und Registrierungstyp auswählen“ und den Optionen für den Registrierungstyp](./media/ios-enrollment-type-1909.PNG)  


### <a name="secure-entire-device"></a>Schützen des gesamten Geräts  

1. Lesen Sie sich auf der Anzeige **Geräteverwaltung und Datenschutz** die Liste der Geräteinformationen durch, die Ihre Organisation einsehen oder nicht einsehen kann. Tippen Sie dann auf **Weiter**.  


 > [!IMPORTANT]
> Diese nächsten Schritte und Bildschirme sind je nach iOS-Version unterschiedlich. Führen Sie die Schritte für Ihre iOS-Version aus. 

2. Safari öffnet die Unternehmensportal-Website auf Ihrem Gerät. Wenn Sie aufgefordert werden, das Konfigurationsprofil herunterzuladen, tippen Sie auf **Zulassen**. Falls Sie ein Gerät haben mit:  
    * iOS 12.2 und höher: Wenn der Download abgeschlossen ist, tippen Sie auf **Schließen**. Fahren Sie dann mit Schritt 3 fort.  
    * iOS 12.1 und früher: Sobald der Download abgeschlossen ist, werden Sie automatisch zur App „Einstellungen“ weitergeleitet. Fahren Sie mit Schritt 4 fort.  
 
    Wenn Sie versehentlich auf **Ignorieren** tippen sollten, aktualisieren Sie die Seite. Sie werden aufgefordert, die Unternehmensportal-App zu öffnen. Tippen Sie auf **Erneut herunterladen**, sobald diese geöffnet wurde.

  > [!NOTE]
  > Sie müssen das Verwaltungsprofil, wie in den nächsten Schritten beschrieben, innerhalb von 8 Minuten nach dem Herunterladen installieren. Wenn dies nicht geschieht, wird das Profil entfernt, woraufhin Sie die Registrierung erneut starten müssen.  

3. Tippen Sie auf **Öffnen**, wenn Sie dazu aufgefordert werden, das Unternehmensportal zu öffnen. Lesen Sie die Informationen auf der Anzeige **Installieren des Verwaltungsprofils** durch.  

4. Öffnen Sie die App „Einstellungen“, und tippen Sie dann auf **Bei <Organisationsname> registrieren** oder auf **Profil heruntergeladen**.  

    ![Beispielscreenshot der App „Einstellungen“ mit der Option „Bei Organisation registrieren“](./media/enroll-in-organization-ios-1909.PNG)  

   Wenn keine dieser Optionen angezeigt werden, navigieren Sie zu **Allgemein** > **Profile & Geräteverwaltung**> **Verwaltungsprofil**. Wenn weiterhin kein Verwaltungsprofil angezeigt wird, müssen Sie es möglicherweise erneut herunterladen.  

5. Tippen Sie auf **Installieren**.  
    
6. Geben Sie das Gerätekennwort ein. Tippen Sie dann auf **Installieren**.    

7. Der nächste Bildschirm ist eine standardmäßige Systemwarnung zur Geräteverwaltung. Um mit der Installation fortzufahren, tippen Sie auf **Installieren**. Wenn Sie aufgefordert werden, der Remoteverwaltung zu vertrauen, tippen Sie auf **Vertrauen**.  

8. Klicken Sie nach Abschluss der Installation auf **Fertig**. Um zu bestätigen, dass das Profil installiert wurde, wechseln Sie zu den Einstellungen unter **Profile und Geräteverwaltung**. Daraufhin sollte das Profile unter **Verwaltung mobiler Geräte** aufgeführt sein.   

    ![Beispielscreenshot der App „Einstellungen“ mit den Einstellungen unter „Profile und Geräteverwaltung“ mit gezeigtem Verwaltungsprofil.](./media/ios-12-cp-enroll-1904.PNG)  

9. Kehren Sie zur Unternehmensportal-App zurück. Das Unternehmensportal beginnt mit der Synchronisierung und Einrichtung Ihres Geräts. Das Unternehmensportal fordert Sie möglicherweise auf, zusätzliche Geräteeinstellungen zu aktualisieren. Wenn das der Fall ist, tippen Sie auf **Weiter**.  

10. Sie erkennen, dass das Setup abgeschlossen ist, wenn alle Elemente in der Liste ein grünes Häkchen aufweisen. Tippen Sie auf **Fertig**.   

> [!Note]
> Wenn in Ihrer Organisation Obergrenzen für Gesprächsminuten oder Datenvolumen gelten oder sie Ihnen ein unternehmenseigenes Gerät zur Verfügung stellt, müssen Sie möglicherweise noch einige weitere Schritte durchführen. Wenn Sie aufgefordert werden, die App **Datalert** zu installieren, lesen Sie [Registrieren Ihres Geräts im Telecom Expense Management](enroll-your-device-with-telecom-expense-management-ios.md). Wenn Ihr Unternehmen am Apple-Programm zur Geräteregistrierung teilnimmt, finden Sie heraus, [wie Sie Ihr unternehmenseigenes Gerät registrieren können](enroll-your-device-dep-ios.md).  

### <a name="secure-work-related-apps-and-data"></a>Schützen arbeitsbezogener Apps und Daten  
1. Die Anzeige **Microsoft Authenticator herunterladen** wird angezeigt (wenn Sie bereits über die Authenticator-App verfügen, wird diese Anzeige nicht angezeigt, fahren Sie also mit Schritt 2 fort).  
    1. Tippen Sie auf **Aus App Store herunterladen**.
    2. Installieren Sie die App, wenn der App Store geöffnet wurde. 
    3. Kehren Sie zum Unternehmensportal zurück, und tippen Sie auf **Fortfahren**.    
    
   Nachdem Sie Microsoft Authenticator installiert haben, müssen Sie nichts Weiteres mit der App tun. Sie muss lediglich auf Ihrem Gerät installiert sein. 

   ![Beispielscreenshot des Unternehmensportals mit der Anzeige „Microsoft Authenticator herunterladen“](./media/download-ms-authenticator-1909.PNG)  

2. Lesen Sie sich auf der Anzeige **Geräteverwaltung und Datenschutz** die Liste der Geräteinformationen durch, die Ihre Organisation einsehen oder nicht einsehen kann. Tippen Sie dann auf **Weiter**.  


 > [!IMPORTANT]
> Diese nächsten Schritte und Bildschirme sind je nach iOS-Version unterschiedlich. Führen Sie die Schritte für Ihre iOS-Version aus. 

3. Safari öffnet die Unternehmensportal-Website auf Ihrem Gerät. Wenn Sie aufgefordert werden, das Konfigurationsprofil herunterzuladen, tippen Sie auf **Zulassen**. Falls Sie ein Gerät haben mit:  
    * iOS 12.2 und höher: Wenn der Download abgeschlossen ist, tippen Sie auf **Schließen**. Fahren Sie dann mit Schritt 4 fort.  
    * iOS 12.1 und früher: Sobald der Download abgeschlossen ist, werden Sie automatisch zur App „Einstellungen“ weitergeleitet. Fahren Sie mit Schritt 5 fort.  
 
    Wenn Sie versehentlich auf **Ignorieren** tippen sollten, aktualisieren Sie die Seite. Sie werden aufgefordert, die Unternehmensportal-App zu öffnen. In der App können Sie auf **Erneut herunterladen** tippen.

  > [!NOTE]
  > Sie müssen das Verwaltungsprofil, wie in den nächsten Schritten beschrieben, innerhalb von 8 Minuten nach dem Herunterladen installieren. Wenn dies nicht geschieht, wird das Profil entfernt, woraufhin Sie die Registrierung erneut starten müssen.  

4. Tippen Sie auf **Öffnen**, wenn Sie dazu aufgefordert werden, das Unternehmensportal zu öffnen. Lesen Sie die Informationen auf der Anzeige **Installieren des Verwaltungsprofils** durch. 

5. Öffnen Sie die App „Einstellungen“, und tippen Sie dann auf **Bei <Organisationsname> registrieren** oder auf **Profil heruntergeladen**.  

    ![Beispielscreenshot der App „Einstellungen“ mit der Option „Bei Organisation registrieren“](./media/enroll-in-organization-ios-1909.PNG)  

   Wenn keine dieser Optionen angezeigt werden, navigieren Sie zu **Allgemein** > **Profile & Geräteverwaltung**> **Verwaltungsprofil**. Wenn weiterhin kein Verwaltungsprofil angezeigt wird, müssen Sie es möglicherweise erneut herunterladen.   


6. Tippen Sie auf der Anzeige **Benutzerregistrierung** auf **Enroll My iPhone** (Mein iPhone registrieren).  

    ![Beispielscreenshot der App „Einstellungen“ mit der Anzeige „Benutzerregistrierung“ und hervorgehobener Schaltfläche „Registrieren“](./media/user-enrollment-information-1909.PNG)  

7. Geben Sie das Kennwort des Geräts ein. Tippen Sie dann auf **Installieren**.  

8. Geben Sie in der Anzeige **Anmelden** das Kennwort für Ihre verwaltete Apple-ID ein. In den meisten Fällen sind diese Anmeldeinformationen identisch mit denen, die Sie für die Anmeldung bei Ihrem Geschäfts-, Schul- oder Unikonto verwenden, es sei denn, Ihre Organisation hat Ihnen andere Anmeldeinformationen zugeteilt. 
9. Tippen Sie auf **Anmelden**.  
10. Kurz nach der Installation des Profils wird eine Erfolgsmeldung angezeigt. Um zu bestätigen, dass das Profil installiert wurde, wechseln Sie zu den Einstellungen unter **Profile und Geräteverwaltung**. Daraufhin sollte das Profile unter **Verwaltung mobiler Geräte** aufgeführt sein.  

    ![Beispielscreenshot der App „Einstellungen“ mit den Einstellungen unter „Profile und Geräteverwaltung“ mit gezeigtem Verwaltungsprofil.](./media/ios-12-cp-enroll-1904.PNG)  

11. Kehren Sie zur Unternehmensportal-App zurück. Das Unternehmensportal beginnt mit der Synchronisierung und Einrichtung Ihres Geräts. Das Unternehmensportal fordert Sie möglicherweise auf, zusätzliche Geräteeinstellungen zu aktualisieren. Wenn das der Fall ist, tippen Sie auf **Weiter**.    

12. Sie erkennen, dass das Setup abgeschlossen ist, wenn alle Elemente in der Liste ein grünes Häkchen aufweisen. Tippen Sie auf **Fertig**.  

## <a name="it-administrator-support"></a>Unterstützung für IT-Administratoren  
Wenn Sie IT-Administrator sind und Probleme bei der Registrierung von Geräten haben, lesen Sie [Behandeln von Problemen bei der Registrierung von iOS-Geräten in Microsoft Intune](https://support.microsoft.com/en-us/help/4039809). Dieser Artikel listet häufige Fehler, ihre Ursachen und Schritte zur Behebung auf.  

## <a name="next-steps"></a>Nächste Schritte  
Finden Sie Apps, die Ihnen bei der Arbeit oder in der Schule oder Hochschule helfen. Erfahren Sie, wie über das Unternehmensportal [Apps zur Verfügung gestellt werden](use-managed-apps-on-your-device-ios.md).  

Benötigen Sie weitere Unterstützung? Kontaktieren Sie die Supportabteilung Ihres Unternehmens. Sie finden entsprechende Kontaktinformationen auf der [Unternehmensportal-Website](https://go.microsoft.com/fwlink/?linkid=2010980).  
