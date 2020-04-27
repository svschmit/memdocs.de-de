---
title: Registrieren eines iOS- oder iPadOS-Geräts im Intune-Unternehmensportal und bei Intercede
description: Erfahren Sie, wie Sie ein iOS- oder iPadOS-Gerät registrieren und eine Authentifizierung mit abgeleiteten Anmeldeinformationen bei Intercede einrichten.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/31/2019
ms.topic: article
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
ms.openlocfilehash: b83092521f1ab0058d47d599e7fd9c10c2fd6d35
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82077766"
---
# <a name="set-up-ios-or-ipados-device-with-company-portal-and-intercede"></a>Einrichten eines iOS- oder iPadOS-Geräts im Unternehmensportal und bei Intercede

Registrieren Sie Ihr Gerät bei der Intune-Unternehmensportal-App, um sicheren mobilen Zugriff auf E-Mails, Dateien und Apps Ihrer Organisation zu erhalten.  Sobald Ihr Gerät registriert ist, gilt es als *verwaltet*. Ihre Organisation kann dem Gerät über einen MDM-Anbieter (Mobile Device Management, Verwaltung mobiler Geräte) wie Intune Richtlinien und Anwendungen zuweisen.  

Während der Registrierung installieren Sie auch abgeleitete Anmeldeinformationen auf Ihrem Gerät. Ihre Organisation kann verlangen, dass Sie die abgeleiteten Anmeldeinformationen als Authentifizierungsmethode beim Zugriff auf Ressourcen oder zum Signieren und Verschlüsseln von E-Mails verwenden. 

Sie müssen wahrscheinlich abgeleitete Anmeldeinformationen einrichten, wenn Sie eine Smartcard für Folgendes verwenden:

* Anmelden bei Geschäfts-, Schul- oder Uni-Apps, im WLAN und in virtuellen privaten Netzwerken (VPNs)
* Signieren und Verschlüsseln von Geschäfts-, Schul- oder Uni-E-Mails mithilfe von S/MIME-Zertifikaten  

Folgendes wird in diesem Artikel beschrieben:  

* Registrieren eines mobilen iOS- oder iPadOS-Geräts im Intune-Unternehmensportal  
* Abrufen von abgeleiteten Anmeldeinformationen vom Anbieter Ihrer Organisation, [Intercede](https://www.intercede.com/)   


## <a name="what-are-derived-credentials"></a>Was sind abgeleitete Anmeldeinformationen?  
Eine abgeleitete Anmeldeinformation ist ein Zertifikat, das von Ihren Smartcard-Anmeldeinformationen abgeleitet und auf Ihrem Gerät installiert wird. Es gewährt Ihnen Remotezugriff auf Arbeitsressourcen und verhindert gleichzeitig, dass nicht autorisierte Benutzer auf vertrauliche Informationen zugreifen.  

Abgeleitete Anmeldeinformationen werden für Folgendes verwendet: 
* Authentifizieren von Kursteilnehmern und Mitarbeitern, die sich bei Geschäfts-, Schul- oder Uni-Apps, im WLAN oder im VPN anmelden
* Signieren und Verschlüsseln von Geschäfts-, Schul- oder Uni-E-Mails mithilfe von S/MIME-Zertifikaten  

Abgeleitete Anmeldeinformationen sind eine Implementierung der NIST-Richtlinien (National Institute of Standards and Technology) für PIV-Anmeldeinformationen (Personal Identity Verification) aus SP 800-157 (Special Publication).  

## <a name="prerequisites"></a>Voraussetzungen

 Sie benötigen Folgendes, um die Registrierung abzuschließen:

* Ihre Smartcard von der Schule, der Uni oder der Arbeit
* Zugriff auf einen Computer oder ein Self-Service-Kiosk, an dem Sie sich mit Ihrer Smartcard anmelden können
* Ihr mobiles Gerät
* Die auf Ihrem iOS- oder iPadOS-Gerät installierte Intune-Unternehmensportal-App


## <a name="enroll-device"></a>Registrieren eines Geräts  
1. Öffnen Sie die Unternehmensportal-App für iOS/iPadOS auf Ihrem mobilen Gerät, und melden Sie sich mit Ihrem Geschäftskonto an.  
2. Notieren Sie sich den Code, der auf dem Bildschirm angezeigt wird.  

    ![Beispielbild der Unternehmensportal-App mit Nachricht und Code auf dem Bildschirm](./media/copy-code-intercede.png)  
1. Wechseln Sie zu dem Gerät, für das Sie Ihre Smartcard aktiviert haben, und navigieren Sie zu https://microsoft.com/devicelogin. 

1. Geben Sie den Code ein, den Sie zuvor notiert haben.
 
2. Legen Sie Ihre Smartcard ein, um sich anzumelden.   

3. Kehren Sie zur Unternehmensportal-App auf Ihrem mobilen Gerät zurück, und befolgen Sie die Anweisungen auf dem Bildschirm, um Ihr Gerät zu registrieren.  
4. Nach Abschluss der Registrierung werden Sie vom Unternehmensportal benachrichtigt, dass Sie Ihre Smartcard nun einrichten können. Tippen Sie auf die Benachrichtigung. Wenn Sie keine Benachrichtigung erhalten, überprüfen Sie Ihre E-Mails.   

    ![Beispielscreenshot der Pushbenachrichtigung des Unternehmensportals auf dem Startbildschirm des Geräts](./media/action-required-in-app-intercede.png)  

5. Gehen Sie in der Anzeige **Zugriff auf mobile Smartcard einrichten** wie folgt vor:  
    a. Tippen Sie auf den Link zu den Setupanweisungen Ihrer Organisation. Wenn Ihre Organisation keine weiteren Anweisungen bereitstellt, werden Sie zu diesem Artikel weitergeleitet.  
    b. Tippen Sie auf **Beginn**.  

    ![Beispielscreenshot des Bildschirms „Zugriff auf mobile Smartcard einrichten“ im Unternehmensportal](./media/smart-card-info-intercede.png)  

6. Wechseln Sie zum Gerät, für das Sie die Smartcard aktiviert haben oder zum Self-Service-Kiosk, und öffnen Sie die MyID-App. Melden Sie sich mit Ihren Anmeldeinformationen an.  
7. Wählen Sie die Option aus, Ihre ID anzufordern. 
8. Wenn Sie gefragt werden, welches Profil Sie verwenden möchten, wählen Sie die Option aus, es mit Anmeldeinformationen eines mobilen Geräts zu aktivieren. Ein QR-Code wird angezeigt.  
9. Wechseln Sie zurück zu Ihrem mobilen Gerät. Tippen Sie im Unternehmensportal auf dem Bildschirm **QR-Code abrufen** auf **Weiter**.  

    ![Beispielscreenshot: Bildschirm „QR-Code abrufen“ im Unternehmensportals](./media/get-qr-code-intercede.png) 
 
10. Tippen Sie auf **Kamera verwenden** > **OK**.  

    ![Beispielscreenshot einer Aufforderung im Unternehmensportal zum Erlauben des Zugriffs auf die Kamera](./media/allow-cp-camera-access-intercede.png)  

11. Scannen Sie das Bild des QR-Codes auf Ihrem smartcardfähigen Gerät. 
12. Warten Sie, bis das Unternehmensportal das Einrichten Ihres Geräts abgeschlossen hat.  

## <a name="next-steps"></a>Nächste Schritte  
Nach der Registrierung haben Sie Zugriff auf Arbeitsressourcen wie E-Mail, WLAN und alle Apps, die Ihre Organisation zur Verfügung stellt. Weitere Informationen darüber, wie Sie Apps im Unternehmensportal erhalten, suchen, installieren und deinstallieren können, finden Sie unter:

* [Verwalten von Apps von der Unternehmensportalwebsite](manage-apps-cpweb.md)  
* [Verwenden verwalteter Apps auf Ihrem Gerät](use-managed-apps-on-your-device-ios.md)  

Benötigen Sie weitere Unterstützung? Kontaktieren Sie den Support Ihres Unternehmens. Die entsprechenden Kontaktinformationen finden Sie auf der [Unternehmensportal-Website](https://go.microsoft.com/fwlink/?linkid=2010980).
