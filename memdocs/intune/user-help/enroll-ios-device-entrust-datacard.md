---
title: Registrieren eines iOS- oder iPadOS-Geräts beim Intune-Unternehmensportal und bei Entrust Datacard
description: Hier erfahren Sie, wie Sie ein iOS- oder iPadOS-Gerät registrieren und eine Authentifizierung mit abgeleiteten Anmeldeinformationen mit Entrust Datacard einrichten.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/08/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: tisilver
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: e849936e7e0686af3377fd4d10182d3a4eb84458
ms.sourcegitcommit: 678104677ad36b789630befdc5e0f1efc572c14b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/08/2020
ms.locfileid: "86137445"
---
# <a name="set-up-ios-or-ipados-device-with-company-portal-and-entrust-datacard"></a>Einrichten eines iOS- oder iPadOS-Geräts beim Unternehmensportal und bei Entrust Datacard

Registrieren Sie Ihr Gerät bei der Intune-Unternehmensportal-App, um sicheren mobilen Zugriff auf E-Mails, Dateien und Apps Ihrer Organisation zu erhalten. Sobald Ihr Gerät registriert ist, gilt es als *verwaltet*. Ihre Organisation kann dem Gerät über einen MDM-Anbieter (Mobile Device Management, Verwaltung mobiler Geräte) wie Intune Richtlinien und Anwendungen zuweisen.  

Während der Registrierung installieren Sie auch abgeleitete Anmeldeinformationen auf Ihrem Gerät. Ihre Organisation kann verlangen, dass Sie die abgeleiteten Anmeldeinformationen als Authentifizierungsmethode beim Zugriff auf Ressourcen oder zum Signieren und Verschlüsseln von E-Mails verwenden. 

Sie müssen wahrscheinlich abgeleitete Anmeldeinformationen einrichten, wenn Sie eine Smartcard für Folgendes verwenden:  

* Anmelden bei Geschäfts-, Schul- oder Uni-Apps, im WLAN und in virtuellen privaten Netzwerken (VPNs)
* Signieren und Verschlüsseln von Geschäfts-, Schul- oder Uni-E-Mails mithilfe von S/MIME-Zertifikaten  

Folgendes wird in diesem Artikel beschrieben:  

   * Registrieren eines mobilen iOS- oder iPadOS-Geräts beim Intune-Unternehmensportal  
   * Abrufen von abgeleiteten Anmeldeinformationen vom Anbieter Ihrer Organisation [Entrust Datacard](https://www.entrustdatacard.com/)  

### <a name="what-are-derived-credentials"></a>Was sind abgeleitete Anmeldeinformationen?  
Eine abgeleitete Anmeldeinformation ist ein Zertifikat, das von Ihren Smartcard-Anmeldeinformationen abgeleitet und auf Ihrem Gerät installiert wird. Es gewährt Ihnen Remotezugriff auf Arbeitsressourcen und verhindert gleichzeitig, dass nicht autorisierte Benutzer auf vertrauliche Informationen zugreifen.  

Abgeleitete Anmeldeinformationen werden für Folgendes verwendet: 
* Authentifizieren von Kursteilnehmern und Mitarbeitern, die sich bei Geschäfts-, Schul- oder Uni-Apps, im WLAN oder im VPN anmelden
* Signieren und Verschlüsseln von Geschäfts-, Schul- oder Uni-E-Mails mithilfe von S/MIME-Zertifikaten

Abgeleitete Anmeldeinformationen sind eine Implementierung der NIST-Richtlinien (National Institute of Standards and Technology) für PIV-Anmeldeinformationen (Personal Identity Verification) aus SP 800-157 (Special Publication).  

## <a name="prerequisites"></a>Voraussetzungen

 Sie benötigen Folgendes, um die Registrierung abzuschließen:

* Ihre Smartcard von der Schule, der Uni oder der Arbeit
* Zugriff auf einen Computer oder ein Kiosk, an dem Sie sich mit Ihrer Smartcard anmelden können
* Ihr mobiles Gerät
* Die auf Ihrem iOS- oder iPadOS-Gerät installierte Intune-Unternehmensportal-App  


## <a name="enroll-device"></a>Registrieren eines Geräts  
1. Öffnen Sie die Unternehmensportal-App für iOS/iPadOS auf Ihrem mobilen Gerät, und wählen Sie die Option zum Anmelden von einem anderen Gerät aus.  

2. Notieren Sie sich den Code auf dem Bildschirm.  

    ![Beispielbild der Unternehmensportal-App mit Meldung und Code auf dem Bildschirm](./media/copy-code-intercede.png)   

3. Wechseln Sie zu dem Gerät, für das Sie Ihre Smartcard aktiviert haben, und navigieren Sie zu https://microsoft.com/devicelogin. 
4. Geben Sie den Code ein, den Sie zuvor notiert haben.  

    ![Beispielscreenshot der Eingabeaufforderung „Code eingeben“ auf der Unternehmensportal-Website](./media/enter-code-intercede.png)   

5. Legen Sie Ihre Smartcard ein, um sich anzumelden.   
6. Kehren Sie zur Unternehmensportal-App auf Ihrem mobilen Gerät zurück, und befolgen Sie die Anweisungen auf dem Bildschirm, um Ihr Gerät zu registrieren.  
7. Nach Abschluss der Registrierung werden Sie vom Unternehmensportal benachrichtigt, dass Sie Ihre Smartcard nun einrichten können. Tippen Sie auf die Benachrichtigung. Wenn Sie keine Benachrichtigung erhalten, überprüfen Sie Ihre E-Mails.   

    ![Beispielscreenshot der Pushbenachrichtigung des Unternehmensportals auf dem Startbildschirm des Geräts](./media/action-required-in-app-intercede.png)  

8. Gehen Sie in der Anzeige **Zugriff auf mobile Smartcard einrichten** wie folgt vor:   
    a. Tippen Sie auf den Link zu den Setupanweisungen Ihrer Organisation. Wenn Ihre Organisation keine weiteren Anweisungen bereitstellt, werden Sie zu diesem Artikel weitergeleitet.  
    b. Tippen Sie auf **Beginn**.  

    ![Beispielscreenshot des Bildschirms „Zugriff auf mobile Smartcard einrichten“ im Unternehmensportal](./media/smart-card-info-intercede.png)

9. Wechseln Sie zu dem Gerät, für das Sie Ihre Smartcard aktiviert haben, und navigieren Sie zu „IdentityGuard“. 
10. Suchen Sie nach dem Anmeldebereich für intelligente Anmeldeinformationen, und klicken Sie auf die Schaltfläche zum Anmelden.  
11. Wenn Sie aufgefordert werden, ein Zertifikat auszuwählen, wählen Sie Ihre Smartcard-Anmeldeinformationen aus. Klicken Sie dann auf **OK**. 
12. Geben Sie Ihre Smartcard-PIN ein.  
13. Sie werden aufgefordert, aus einer Liste von Aktionen auszuwählen. Wählen Sie jene aus, mit der Sie sich mit abgeleiteten mobilen Smartcard-Anmeldeinformationen registrieren können. Der Link oder die Schaltfläche zeigt möglicherweise die folgende Meldung **I'd like to enroll for a derived mobile smart card credential** (Ich möchte mich mit abgeleiteten mobilen Smartcard-Anmeldeinformationen registrieren) an.  
14. Wählen Sie aus, ob Sie die Anwendung mit intelligenten Anmeldeinformationen erfolgreich heruntergeladen und installiert haben. Fahren Sie fort, und wechseln Sie zum nächsten Bildschirm.   
15. Geben Sie Informationen zu Ihren abgeleiteten Smartcard-Anmeldeinformationen ein.  
    a. Geben Sie für den Identitätsnamen einen beliebigen Namen ein (z. B. *Entrust Derived Cred*).  
    b. Klicken Sie im Dropdownmenü auf **Entrust IdentityGudard Mobile Smart Credential** (Entrust IdentityGudard die mobilen Smartcard-Anmeldeinformationen überlassen).  
    c. Fahren Sie zum nächsten Bildschirm fort. Es wird ein QR-Code mit einem numerischen Kennwort angezeigt.  

16. Wechseln Sie zurück zu Ihrem mobilen Gerät. Tippen Sie im Unternehmensportal auf dem Bildschirm **QR-Code abrufen** auf **Weiter**. 

    ![Beispielscreenshot: Bildschirm „QR-Code abrufen“ im Unternehmensportals](./media/get-qr-code-intercede.png)  
17. Tippen Sie auf **Kamera verwenden** > **OK**.  

    ![Beispielscreenshot einer Aufforderung im Unternehmensportal zum Erlauben des Zugriffs auf die Kamera](./media/allow-cp-camera-access-intercede.png)  
18. Scannen Sie das Bild des QR-Codes auf Ihrem smartcardfähigen Gerät.  
19. Geben Sie das numerische Kennwort ein, das im QR-Code angezeigt wird.  

    ![Beispielscreenshot des Bildschirms „Kennwort erforderlich“ im Unternehmensportal mit dem Feld für die Kennworteingabe](./media/enter-password-derived-credentials.png)   

20. Warten Sie, bis das Unternehmensportal das Einrichten Ihres Geräts abgeschlossen hat.  


## <a name="next-steps"></a>Nächste Schritte  
Nach der Registrierung haben Sie Zugriff auf Arbeitsressourcen wie E-Mail, WLAN und alle Apps, die Ihre Organisation zur Verfügung stellt. Weitere Informationen darüber, wie Sie Apps im Unternehmensportal erhalten, suchen, installieren und deinstallieren können, finden Sie unter:

* [Verwalten von Apps von der Unternehmensportalwebsite](manage-apps-cpweb.md)  
* [Verwenden verwalteter Apps auf Ihrem Gerät](use-managed-apps-on-your-device-ios.md)  

Benötigen Sie weitere Unterstützung? Kontaktieren Sie den Support Ihres Unternehmens. Die entsprechenden Kontaktinformationen finden Sie auf der [Unternehmensportal-Website](https://go.microsoft.com/fwlink/?linkid=2010980).  
