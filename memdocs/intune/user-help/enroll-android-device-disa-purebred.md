---
title: Registrieren eines Android-Geräts mit der Microsoft Intune-App und DISA Purebred
description: Erfahren Sie, wie Sie ein Android-Gerät registrieren und eine Authentifizierung mit abgeleiteten Anmeldeinformationen mit DISA Purebred einrichten.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/15/2020
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
ms.openlocfilehash: 584392891320f96eed16863225ffb323dc240594
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83880618"
---
# <a name="set-up-android-device-with-the-microsoft-intune-app-and-disa-purebred"></a>Einrichten eines Android-Geräts mit der Microsoft Intune-App und DISA Purebred

Registrieren Sie Ihr Gerät bei der Microsoft Intune-App, um sicheren mobilen Zugriff auf E-Mails, Dateien und Apps Ihrer Organisation zu erhalten. Sobald Ihr Gerät registriert ist, gilt es als *verwaltet*. Ihre Organisation kann dem Gerät über einen MDM-Anbieter (Mobile Device Management, Verwaltung mobiler Geräte) wie Intune Richtlinien und Anwendungen zuweisen.  

Während der Registrierung installieren Sie auch abgeleitete Anmeldeinformationen auf Ihrem Gerät. Ihre Organisation kann verlangen, dass Sie die abgeleiteten Anmeldeinformationen als Authentifizierungsmethode beim Zugriff auf Ressourcen oder zum Signieren und Verschlüsseln von E-Mails verwenden.

Sie müssen wahrscheinlich abgeleitete Anmeldeinformationen einrichten, wenn Sie eine Smartcard für Folgendes verwenden:

* Anmelden bei Geschäfts-, Schul- oder Uni-Apps, im WLAN und in virtuellen privaten Netzwerken (VPNs)
* Signieren und Verschlüsseln von Geschäfts-, Schul- oder Uni-E-Mails mithilfe von S/MIME-Zertifikaten

Folgendes wird in diesem Artikel beschrieben:

* Registrieren eines Android-Geräts über die Intune-App
* Richten Sie Ihre Smartcard ein, indem Sie eine abgeleitete Anmeldeinformation vom Anbieter ([DISA Purebred](https://public.cyber.mil/pki-pke/purebred/)) abgeleiteter Anmeldeinformationen installieren.

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
* Die auf Ihrem Gerät installierte Purebred-App. (Diese sollte nach dem Einrichten des Geräts automatisch installierte werden. Sollte dies nicht der Fall sein, wenden Sie sich an Ihren Ansprechpartner beim IT-Support.)

Zudem müssen Sie sich beim Setup an einen Purebred-Agent oder -Mitarbeiter wenden.

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

16. Fahren Sie mit dem Abschnitt [Einrichten Ihrer Smartcard](enroll-android-device-disa-purebred.md#set-up-smart-card) in diesem Artikel fort, um die Einrichtung Ihres Geräts abzuschließen.  

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

1. Geben Sie **afw#setup** auf dem Google-Anmeldebildschirm in das Feld **Email or phone** (E-Mail-Adresse oder Telefonnummer) ein. Tippen Sie auf **Weiter**. 

   ![Beispielbild des Google-Anmeldebildschirms mit „afw#setup“ im Feld](./media/token-intune-app-01.png)   

2. Tippen Sie bei der **Android-Geräterichtlinien**-App auf **Installieren**. Führen Sie die weiteren Schritte der Installation aus. Möglicherweise müssen Sie je nach Gerät weitere Nutzungsbedingungen prüfen und akzeptieren.    

3. Tippen Sie auf der Anzeige **Dieses Gerät registrieren** auf **Weiter**.  

4. Tippen Sie auf **Enter code** (Code eingeben).  

5. Geben Sie auf der Anzeige **Scan or enter code** (Code scannen oder eingeben) den Code ein, den Sie von Ihrem Unternehmen erhalten haben.  Klicken Sie anschließend auf **Weiter**.  

   ![Beispielbild der Anzeige „Scan or enter code“ (Code scannen oder eingeben) mit hervorgehobener Schaltfläche „Weiter“](./media/token-intune-app-04.png)  

6. Kehren Sie zu Schritt 4 des Abschnitts [Registrieren eines Geräts](#enroll-device) zurück, um mit dem Setup fortzufahren.


## <a name="set-up-smart-card"></a>Einrichten der Smartcard  

> [!NOTE]
> Die Purebred-App wird benötigt, um diese Schritte abzuschließen und wird automatisch nach der Registrierung auf Ihrem Gerät registriert. Wenn Sie nach einer kurzen Wartezeit immer noch keine App haben, wenden Sie sich an Ihren IT-Support.  

1. Nach Abschluss der Registrierung werden Sie von der Intune-App benachrichtigt, dass Sie Ihre Smartcard nun einrichten können. Tippen Sie auf die Benachrichtigung. Wenn Sie keine Benachrichtigung erhalten, überprüfen Sie Ihre E-Mails.

   > [!div class="mx-imgBorder"]
   > ![Screenshot der Pushbenachrichtigung der Intune-App auf dem Startbildschirm des Geräts](./media/action-required-in-app-android.png)

2. Legen Sie auf dem Bildschirm **Smartcard einrichten** Folgendes fest:

   1. Tippen Sie auf den Link zu den Setupanweisungen Ihrer Organisation, und überprüfen Sie sie. Wenn Ihre Organisation keine weiteren Anweisungen bereitstellt, werden Sie zu diesem Artikel weitergeleitet.

   2. Tippen Sie auf **Begin** (Starten).   

   > [!div class="mx-imgBorder"]
   > ![Screenshot der Intune-App mit Bildschirm „Smartcard einrichten“](./media/smart-card-open-disa-purebred-android.png)

3. Tippen Sie auf dem Bildschirm **Zertifikate abrufen** auf **Purebred starten**, um die Purebred-App zu öffnen. (Die App sollte standardmäßig automatisch auf Ihrem Gerät installiert worden sein. Wenn Sie sie nicht besitzen, wenden Sie sich an Ihre Supportabteilung.)  

   > [!div class="mx-imgBorder"]
   > ![Screenshot der Eingabeaufforderung der Intune-App zum Öffnen der DISA Purebred-App](./media/open-app-prompt-disa-purbred-android.png)  

4. Die Purebred-App benötigt ggf. zusätzliche Berechtigungen, damit sie ordnungsgemäß ausgeführt werden kann. Tippen Sie auf **Zulassen** oder **Allow all the time** (Immer zulassen), wenn Sie dazu aufgefordert werden. Weitere Informationen darüber, warum diese Berechtigungen erforderlich sind, erhalten Sie von Ihrer Supportabteilung oder dem Purebred-Agent.  

5. Sobald Sie die Purebred-App geöffnet haben, arbeiten Sie mit dem Purebred-Agent Ihrer Organisation, um die Zertifikate herunterzuladen und zu installieren, die Sie für den Zugriff auf Arbeits- oder Schulressourcen benötigen.

    > [!IMPORTANT]
    > Tippen Sie während dieses Vorgangs bei Aufforderung auf **OK** oder **Installieren**. Ändern Sie nicht die Namen von Zertifizierungsstellen (CAs) oder Zertifikaten, für die Sie zur Installation aufgefordert werden.    

6. Nach Abschluss der Installation erhalten Sie eine Benachrichtigung, dass Ihre Zertifikate nun bereit sind. Tippen Sie auf die Benachrichtigung, um zur Intune-App zurückzukehren.

    > [!div class="mx-imgBorder"]
    > ![Screenshot des Bildschirms zum Zulassen des Zugriffs auf Zertifikate](./media/certificates-ready-prompt-disa-purbred-android.png)

7. Über den Bildschirm **Allow access to certificates** (Zugriff auf Zertifikate zulassen) erteilen Sie der Intune-App die Berechtigung, auf die abgeleiteten Anmeldeinformationen zuzugreifen, die Sie von DISA Purebred erhalten haben. Mit diesem Schritt wird sichergestellt, dass Ihre Organisation Ihre Identität überprüfen kann, wenn Sie auf geschützte Geschäfts- oder Schulressourcen zugreifen.  

    1. Tippen Sie auf **Weiter**.

       > [!div class="mx-imgBorder"]
       > ![Screenshot mit der Benachrichtigung, dass Ihre Zertifikate bereit sind](./media/certificates-access-disa-purbred-android.png)

    2. Wenn Sie aufgefordert werden, ein Zertifikat auszuwählen (**Zertifikat auswählen**), ändern Sie die Auswahl nicht. Das richtige Zertifikat ist bereits ausgewählt, tippen Sie also einfach auf **Auswählen** oder **OK**.  

       > [!div class="mx-imgBorder"]
       > ![Screenshot der Aufforderung zur Zertifikatauswahl](./media/choose-certificates-prompt-disa-purbred-android.png)

    3. Ihre abgeleiteten Anmeldeinformationen bestehen aus mehreren Zertifikaten, es kann also sein, dass die Aufforderung **Zertifikat auswählen** mehrmals angezeigt wird. Wiederholen Sie den vorherigen Schritt, bis keine Aufforderungen mehr angezeigt werden.  

8. Nachdem alle Zertifikate verarbeitet wurden, warten Sie, bis die Intune-App die Einrichtung Ihres Geräts abgeschlossen hat. Wenn der Bildschirm **Alles erledigt!** angezeigt wird, wissen Sie, dass das Setup abgeschlossen ist.  

    > [!div class="mx-imgBorder"]
    > ![Screenshot des Bildschirms „Alles erledigt!“](./media/all-set-android.png)

## <a name="next-steps"></a>Nächste Schritte

Nach der Registrierung haben Sie Zugriff auf Arbeitsressourcen wie E-Mail, WLAN und alle Apps, die Ihre Organisation zur Verfügung stellt. Weitere Informationen darüber, wie Sie Apps in der Intune-App erhalten, suchen, installieren und deinstallieren können, finden Sie unter:

* [Verwenden verwalteter Apps auf Ihrem Gerät](use-managed-apps-on-your-device-android.md)  
* [Verwalten von Apps von der Unternehmensportalwebsite](manage-apps-cpweb.md)  


Benötigen Sie weitere Unterstützung? Kontaktieren Sie den Support Ihres Unternehmens. Die entsprechenden Kontaktinformationen finden Sie auf der [Unternehmensportal-Website](https://go.microsoft.com/fwlink/?linkid=2010980).
