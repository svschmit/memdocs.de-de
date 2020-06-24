---
title: Registrieren eines Android-Geräts mit der Microsoft Intune-App und Entrust Datacard
description: Registrieren Sie ein Android-Gerät, und richten Sie die Authentifizierung mit abgeleiteten Anmeldeinformationen mit Entrust Datacard ein.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/17/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: jeyang
ms.suite: ems
ms.custom: intune-enduser
ms.collection: M365-identity-device-management
ms.openlocfilehash: f59d3c0d06e9b12acab3292ba0c977b181e7c07e
ms.sourcegitcommit: 48ec5cdc5898625319aed2893a5aafa402d297fc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/08/2020
ms.locfileid: "84531790"
---
# <a name="set-up-android-device-with-company-portal-and-entrust-datacard"></a>Einrichten eines Android-Geräts über das Unternehmensportal und Entrust Datacard

Registrieren Sie Ihr Gerät bei der Microsoft Intune-App, um sicheren mobilen Zugriff auf E-Mails, Dateien und Apps Ihrer Organisation zu erhalten. Sobald Ihr Gerät registriert ist, gilt es als *verwaltet*. Ihre Organisation kann dem Gerät über einen MDM-Anbieter (Mobile Device Management, Verwaltung mobiler Geräte) wie Intune Richtlinien und Anwendungen zuweisen.

Während der Registrierung installieren Sie auch abgeleitete Anmeldeinformationen auf Ihrem Gerät. Ihre Organisation kann verlangen, dass Sie die abgeleiteten Anmeldeinformationen als Authentifizierungsmethode beim Zugriff auf Ressourcen oder zum Signieren und Verschlüsseln von E-Mails verwenden.

Sie müssen wahrscheinlich abgeleitete Anmeldeinformationen einrichten, wenn Sie eine Smartcard für Folgendes verwenden:

* Anmelden bei Geschäfts-, Schul- oder Uni-Apps, im WLAN und in virtuellen privaten Netzwerken (VPNs)
* Signieren und Verschlüsseln von Geschäfts-, Schul- oder Uni-E-Mails mithilfe von S/MIME-Zertifikaten

Folgendes wird in diesem Artikel beschrieben:

* Registrieren eines Android-Geräts über die Intune-App
* Einrichten Ihrer Smartcard, indem Sie eine abgeleitete Anmeldeinformation vom Anbieter ([Entrust Datacard](https://www.entrustdatacard.com/)) abgeleiteter Anmeldeinformationen installieren

## <a name="what-are-derived-credentials"></a>Was sind abgeleitete Anmeldeinformationen?

Eine abgeleitete Anmeldeinformation ist ein Zertifikat, das von Ihren Smartcard-Anmeldeinformationen abgeleitet und auf Ihrem Gerät installiert wird. Es gewährt Ihnen Remotezugriff auf Arbeitsressourcen und verhindert gleichzeitig, dass nicht autorisierte Benutzer auf vertrauliche Informationen zugreifen.

Abgeleitete Anmeldeinformationen werden für Folgendes verwendet:

* Authentifizieren von Kursteilnehmern und Mitarbeitern, die sich bei Geschäfts-, Schul- oder Uni-Apps, im WLAN oder im VPN anmelden
* Signieren und Verschlüsseln von Geschäfts-, Schul- oder Uni-E-Mails mithilfe von S/MIME-Zertifikaten

Abgeleitete Anmeldeinformationen sind eine Implementierung der NIST-Richtlinien (National Institute of Standards and Technology) für PIV-Anmeldeinformationen (Personal Identity Verification) aus SP 800-157 (Special Publication).

## <a name="prerequisites"></a>Voraussetzungen

 Sie benötigen Folgendes, um die Registrierung abzuschließen:

* Ihre Smartcard von der Schule, der Uni oder der Arbeit
* Zugriff auf einen Computer oder ein Kiosk, an dem Sie sich mit Ihrer Smartcard anmelden können
* Ein neues oder werkseitig zurückgesetztes Gerät mit Android 7.0 oder höher
* Die Microsoft Intune-App muss auf Ihrem Gerät installiert sein

## <a name="enroll-device"></a>Registrieren eines Geräts  

1. Schalten Sie Ihr neues oder auf Werkseinstellungen zurückgesetztes Gerät ein.  
2. Wählen Sie auf dem **Willkommenssbildschirm** Ihre Sprache aus. Wenn Sie angewiesen wurden, sich mit einem QR-Code oder per NFC zu registrieren, führen Sie die für diese Methoden unten beschriebenen Schritte aus.  
     * NFC: Halten Sie Ihr Gerät mit NFC-Unterstützung an das hierzu vorgesehene Gerät, um eine Verbindung mit dem Netzwerk Ihres Unternehmens herzustellen. Führen Sie die angezeigten Schritte aus. Fahren Sie mit Schritt 5 dieser Anleitung fort, wenn Sie die Nutzungsbedingungen von Google Chrome erreichen.  

     * QR-Code: Führen Sie die unter [Registrierung per QR-Code](#qr-code-enrollment) beschriebenen Schritte aus.  

     Wenn Sie angewiesen wurden, eine andere Methode zu verwenden, fahren Sie mit Schritt 3 fort.    

3. Stellen Sie eine Verbindung mit dem WLAN-Netzwerk her, und tippen Sie dann auf **NEXT** (WEITER). Führen Sie den Schritt aus, der Ihrer Registrierungsmethode entspricht. 

    * Token: Wenn Sie zum Google-Anmeldebildschirm erreichen, führen Sie die Schritte unter [Registrierung per Token](#token-enrollment) aus.  
    * Google Zero Touch: Sobald Sie mit dem WLAN-Netzwerk verbunden sind, wird Ihr Gerät vom Unternehmen erkannt. Fahren Sie mit Schritt 4 fort, und führen Sie die auf dem Bildschirm angezeigten Anweisungen aus, bis das Setup abgeschlossen ist.    
 
       ![Beispielbild der Anzeige der Google-Nutzungsbedingungen, die bei der Verwendung von Google Zero Touch angezeigt werden, mit hervorgehobener Schaltfläche „Accept & Continue“ (Zustimmen & Weiter).](./media/google-zero-touch-intune-app-01.png)   
   
4. Prüfen Sie die Nutzungsbedingungen von Google. Tippen Sie anschließend auf **ACCEPT & CONTINUE** (ZUSTIMMEN & WEITER).  

      ![Beispielbild der Google-Nutzungsbedingungen mit hervorgehobener Schaltfläche „Accept & Continue“ (Akzeptieren & Weiter)](./media/fully-managed-intune-app-04.png)   

5. Prüfen Sie die Nutzungsbedingungen von Google Chrome. Tippen Sie anschließend auf **ACCEPT & CONTINUE** (ZUSTIMMEN & WEITER).  

   ![Beispielbild der Google Chrome-Nutzungsbedingungen mit hervorgehobener Schaltfläche „Accept & Continue“ (Akzeptieren & Weiter)](./media/fully-managed-intune-app-06.png)   

6. Tippen Sie auf dem Anmeldebildschirm auf **Anmeldeoptionen** und dann auf **Anmeldung über ein anderes Gerät**. 

7. Notieren Sie sich den Code auf dem Bildschirm.  

8. Wechseln Sie zu Ihrem Gerät, für das Sie die Smartcard aktiviert haben, und navigieren Sie zu der Webadresse, die auf dem Bildschirm angezeigt wird. 

9. Geben Sie den Code ein, den Sie zuvor notiert haben.

   > [!div class="mx-imgBorder"]
   > ![Screenshot der Eingabeaufforderung „Code eingeben“ auf der Unternehmensportal-Website.](./media/enter-code-intercede.png)

10. Legen Sie Ihre Smartcard ein, um sich anzumelden.  

11. Wählen Sie auf dem Anmeldebildschirm Ihr Geschäfts-, Schul- oder Unikonto aus. Wechseln Sie dann zurück zu Ihrem mobilen Gerät. 

12. Je nach Anforderungen Ihres Unternehmens werden Sie möglicherweise dazu aufgefordert, Ihre Einstellungen zu aktualisieren (z. B. die Bildschirmsperre oder Verschlüsselung). Wenn Ihnen diese Aufforderungen angezeigt werden, tippen Sie auf **SET** (ANPASSEN), und befolgen Sie die angezeigten Anweisungen.  

       ![Beispielbild der Einrichtung Ihres Arbeitssmartphones mit hervorgehobener Schaltfläche „Set“ (Anpassen)](./media/fully-managed-intune-app-10.png)   

13. Tippen Sie auf **INSTALL** (Installieren), um die Geschäfts-Apps zu installieren. Klicken Sie nach Abschluss der Installation auf **NEXT** (WEITER).  

       ![Beispielbild der Einrichtung Ihres Arbeitssmartphones mit hervorgehobener Schaltfläche „Install“ (Installieren)](./media/fully-managed-intune-app-11.png)    

14. Tippen Sie auf **START** (Starten), um die Microsoft Intune-App zu öffnen. 

    ![Beispielbild der Einrichtung Ihres Arbeitssmartphones mit hervorgehobener Schaltfläche „Start“](./media/fully-managed-intune-app-17.png)   
 
15. Kehren Sie zur Intune-App auf Ihrem mobilen Gerät zurück, und befolgen Sie die Anweisungen auf dem Bildschirm, bis die Registrierung abgeschlossen ist. 

    ![Beispielbild zur erfolgreichen Einrichtung, Bildschirm zur Geräteregistrierung mit hervorgehobener Schaltfläche „Done“ (Fertig)](./media/fully-managed-intune-app-19.png)   

16. Fahren Sie mit dem Abschnitt [Einrichten Ihrer Smartcard](enroll-android-device-entrust-datacard.md#set-up-smart-card) in diesem Artikel fort, um die Einrichtung Ihres Geräts abzuschließen.  

### <a name="qr-code-enrollment"></a>Registrierung per QR-Code  
In diesem Abschnitt scannen Sie den von Ihrem Unternehmen bereitgestellten QR-Code.  Wenn Sie fertig sind, werden Sie an die Schritte für die Geräteregistrierung weitergeleitet.     
  
1. Tippen Sie auf dem **Willkommensbildschirm** fünfmal auf den Bildschirm, um das Setup per QR-Code zu starten.  

   ![Beispielbild des Willkommensbildschirms der Geräteeinrichtung mit hervorgehobener Anweisung, auf den Bildschirm zu tippen](./media/qr-code-intune-app-01.png)  

2. Führen Sie die angezeigten Anweisungen aus, um eine Verbindung mit dem WLAN-Netzwerk herzustellen.  
3. Wenn Ihr Gerät über keinen QR-Scanner verfügt, wird der Fortschritt der Installation eines QR-Scanners angezeigt. Warten Sie auf den Abschluss der Installation.  
4. Scannen Sie den QR-Code des Bereitstellungsprofils Ihres Unternehmens, wenn Sie dazu aufgefordert werden.  
5. Kehren Sie zu Schritt 4 des Abschnitts [Registrieren eines Geräts](#enroll-device) zurück, um mit dem Setup fortzufahren.  

### <a name="token-enrollment"></a>Registrierung per Token  
In diesem Abschnitt geben Sie das von Ihrem Unternehmen bereitgestellte Token ein. Wenn Sie fertig sind, werden Sie an die Schritte für die Geräteregistrierung weitergeleitet.  

1. Geben Sie **afw#setup** auf dem Google-Anmeldebildschirm in das Feld **Email or phone** (E-Mail-Adresse oder Telefonnummer) ein. Tippen Sie dann auf **Weiter**. 

   ![Beispielbild des Google-Anmeldebildschirms mit „afw#setup“ im Feld](./media/token-intune-app-01.png)   

2. Tippen Sie bei der **Android-Geräterichtlinien**-App auf **Installieren**. Führen Sie die weiteren Schritte der Installation aus. Möglicherweise müssen Sie je nach Gerät weitere Nutzungsbedingungen prüfen und akzeptieren.    

3. Tippen Sie auf der Anzeige **Dieses Gerät registrieren** auf **Weiter**.  

4. Tippen Sie auf **Enter code** (Code eingeben).  

5. Geben Sie auf der Anzeige **Scan or enter code** (Code scannen oder eingeben) den Code ein, den Sie von Ihrem Unternehmen erhalten haben.  Klicken Sie anschließend auf **Weiter**.  

   ![Beispielbild der Anzeige „Scan or enter code“ (Code scannen oder eingeben) mit hervorgehobener Schaltfläche „Weiter“](./media/token-intune-app-04.png)  

6. Kehren Sie zu Schritt 4 des Abschnitts [Registrieren eines Geräts](#enroll-device) zurück, um mit dem Setup fortzufahren.

## <a name="set-up-smart-card"></a>Einrichten der Smartcard  

1. Nach Abschluss der Registrierung werden Sie von der Intune-App benachrichtigt, dass Sie Ihre Smartcard nun einrichten können. Tippen Sie auf die Benachrichtigung. Wenn Sie keine Benachrichtigung erhalten, überprüfen Sie Ihre E-Mails.

   > [!div class="mx-imgBorder"]
   > ![Beispielscreenshot der Pushbenachrichtigung des Unternehmensportals auf dem Startbildschirm des Geräts.](./media/action-required-in-app-android.png)

2. Legen Sie auf dem Bildschirm **Smartcard einrichten** Folgendes fest:

   1. Tippen Sie auf den Link zu den Setupanweisungen Ihrer Organisation. Wenn Ihre Organisation keine weiteren Anweisungen bereitstellt, werden Sie zu diesem Artikel weitergeleitet.

   2. Tippen Sie auf **BEGIN** (Starten). 

   > [!div class="mx-imgBorder"]
   > ![Beispielscreenshot des Bildschirms „Zugriff auf mobile Smartcard einrichten“ im Unternehmensportal.](./media/smart-card-open-entrust-android.png)

3. Wechseln Sie zu dem Gerät, für das Sie Ihre Smartcard aktiviert haben, und navigieren Sie zu „IdentityGuard“.

4. Suchen Sie nach dem Anmeldebereich für intelligente Anmeldeinformationen, und klicken Sie auf die Schaltfläche zum Anmelden.

5. Wenn Sie aufgefordert werden, ein Zertifikat auszuwählen, wählen Sie Ihre Smartcard-Anmeldeinformationen aus. Klicken Sie dann auf **OK**.

6. Geben Sie Ihre Smartcard-PIN ein.

7. Sie werden aufgefordert, aus einer Liste von Aktionen auszuwählen. Wählen Sie jene aus, mit der Sie sich mit abgeleiteten mobilen Smartcard-Anmeldeinformationen registrieren können. Der Link oder die Schaltfläche zeigt möglicherweise die folgende Meldung **I'd like to enroll for a derived mobile smart card credential** (Ich möchte mich mit abgeleiteten mobilen Smartcard-Anmeldeinformationen registrieren) an.

8. Wählen Sie aus, ob Sie die Anwendung mit intelligenten Anmeldeinformationen erfolgreich heruntergeladen und installiert haben. Fahren Sie fort, und wechseln Sie zum nächsten Bildschirm.

9. Geben Sie Informationen zu Ihren abgeleiteten Smartcard-Anmeldeinformationen ein:

    1. Geben Sie für den Identitätsnamen einen beliebigen Namen ein (z. B. *Entrust Derived Cred*).  
    2. Klicken Sie im Dropdownmenü auf **Entrust IdentityGuard Mobile Smart Credential** (Entrust IdentityGuard die mobilen Smartcard-Anmeldeinformationen überlassen).

    3. Fahren Sie zum nächsten Bildschirm fort. Es wird ein QR-Code mit einem numerischen Kennwort angezeigt.

10. Kehren Sie zu Ihrem Android-Gerät zurück. Tippen Sie in der Intune-App auf dem Bildschirm **QR-Code abrufen** auf **WEITER**.

    > [!div class="mx-imgBorder"]
    > ![Beispielscreenshot: Bildschirm „QR-Code abrufen“ im Unternehmensportals.](./media/get-qr-code-entrust-android.png)

11. Wenn Sie aufgefordert werden, die Verwendung Ihrer Kamera für die Intune-App zuzulassen, tippen Sie auf **Zulassen**.

12. Scannen Sie das Bild des QR-Codes auf Ihrem smartcardfähigen Gerät.

13. Geben Sie auf dem Bildschirm **Kennwort erforderlich** das Kennwort ein, das unter dem QR-Code angezeigt wird.

    > [!div class="mx-imgBorder"]
    > ![Beispielscreenshot des Bildschirms „Kennwort erforderlich“ im Unternehmensportal.](./media/password-required-entrust-android.png)  

14. Die Intune-App startet das Herunterladen und Installieren der Zertifikate, die für den Zugriff auf Geschäfts-, Schul- oder Uniressourcen erforderlich sind. Abhängig von Ihrer Internetverbindung kann dieser Vorgang einige Zeit in Anspruch nehmen. Schließen Sie die App während dieser Zeit nicht.

    > [!div class="mx-imgBorder"]
    > ![Beispielscreenshot der Unternehmensportal-Anzeige zum Herunterladen und Installieren der Zertifikate.](./media/install-certificates-entrust-android.png)

15. Nachdem alle Zertifikate verarbeitet wurden, warten Sie, bis die Intune-App die Einrichtung Ihres Geräts abgeschlossen hat. Wenn der Bildschirm **Alles erledigt!** angezeigt wird, wissen Sie, dass das Setup abgeschlossen ist.

    > [!div class="mx-imgBorder"]
    > ![Beispielscreenshot des Bildschirms „Alles erledigt!“.](./media/all-set-android.png)

## <a name="next-steps"></a>Nächste Schritte

Nach der Registrierung haben Sie Zugriff auf Arbeitsressourcen wie E-Mail, WLAN und alle Apps, die Ihre Organisation zur Verfügung stellt. Weitere Informationen darüber, wie Sie Apps in der Intune-App erhalten, suchen, installieren und deinstallieren können, finden Sie unter:

* [Verwenden verwalteter Apps auf Ihrem Gerät](use-managed-apps-on-your-device-android.md)  
* [Verwalten von Apps von der Unternehmensportalwebsite](manage-apps-cpweb.md)  

Benötigen Sie weitere Unterstützung? Kontaktieren Sie den Support Ihres Unternehmens. Die entsprechenden Kontaktinformationen finden Sie auf der [Unternehmensportal-Website](https://go.microsoft.com/fwlink/?linkid=2010980).