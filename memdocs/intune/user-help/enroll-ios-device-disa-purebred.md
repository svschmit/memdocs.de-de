---
title: Registrieren eines iOS- oder iPadOS-Geräts beim Intune-Unternehmensportal und bei DISA Purebred
description: Erfahren Sie, wie Sie ein iOS- oder iPadOS-Gerät registrieren und eine Authentifizierung mit abgeleiteten Anmeldeinformationen mit DISA Purebred einrichten.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/31/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: tisilver
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 38d1b40ecdeee5bfd872297a5fd4f0229cb48dcf
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79337589"
---
# <a name="set-up-ios-or-ipados-device-with-company-portal-and-disa-purebred"></a>Einrichten eines iOS- oder iPadOS-Geräts beim Unternehmensportal und bei DISA Purebred  

Registrieren Sie Ihr Gerät bei der Intune-Unternehmensportal-App, um sicheren mobilen Zugriff auf E-Mails, Dateien und Apps Ihrer Organisation zu erhalten. Sobald Ihr Gerät registriert ist, gilt es als *verwaltet*. Ihre Organisation kann dem Gerät über einen MDM-Anbieter (Mobile Device Management, Verwaltung mobiler Geräte) wie Intune Richtlinien und Anwendungen zuweisen.  

Während der Registrierung installieren Sie auch abgeleitete Anmeldeinformationen auf Ihrem Gerät. Ihre Organisation kann verlangen, dass Sie die abgeleiteten Anmeldeinformationen als Authentifizierungsmethode beim Zugriff auf Ressourcen oder zum Signieren und Verschlüsseln von E-Mails verwenden. 

Sie müssen wahrscheinlich abgeleitete Anmeldeinformationen einrichten, wenn Sie eine Smartcard für Folgendes verwenden:

* Anmelden bei Geschäfts-, Schul- oder Uni-Apps, im WLAN und in virtuellen privaten Netzwerken (VPN)
* Signieren und Verschlüsseln von Geschäfts-, Schul- oder Uni-E-Mails mithilfe von S/MIME-Zertifikaten  

Folgendes wird in diesem Artikel beschrieben:  

   * Registrieren eines mobilen iOS- oder iPadOS-Geräts beim Intune-Unternehmensportal  
   * Abrufen von abgeleiteten Anmeldeinformationen vom Anbieter Ihrer Organisation, [DISA Purebred](https://cyber.mil/pki-pke/purebred/)  

## <a name="what-are-derived-credentials"></a>Was sind abgeleitete Anmeldeinformationen?  
Eine abgeleitete Anmeldeinformation ist ein Zertifikat, das von Ihren Smartcard-Anmeldeinformationen abgeleitet und auf Ihrem Gerät installiert wird. Es gewährt Ihnen Remotezugriff auf Arbeitsressourcen und verhindert gleichzeitig, dass nicht autorisierte Benutzer auf vertrauliche Informationen zugreifen.  

Abgeleitete Anmeldeinformationen werden für Folgendes verwendet: 
* Authentifizieren von Kursteilnehmern und Mitarbeitern, die sich bei Geschäfts-, Schul- oder Uni-Apps, im WLAN oder im VPN anmelden
* Signieren und Verschlüsseln von Geschäfts-, Schul- oder Uni-E-Mails mithilfe von S/MIME-Zertifikaten

Abgeleitete Anmeldeinformationen sind eine Implementierung der NIST-Richtlinien (National Institute of Standards and Technology) für PIV-Anmeldeinformationen (Personal Identity Verification) aus SP 800-157 (Special Publication).  

## <a name="prerequisites"></a>Voraussetzungen

 Um die Registrierung abzuschließen, benötigen Sie Folgendes:

* Ihre Smartcard von der Schule, der Uni oder der Arbeit
* Zugriff auf einen Computer oder ein Kiosk, an dem Sie sich mit Ihrer Smartcard anmelden können
* Ihr mobiles Gerät
* Die auf Ihrem iOS- oder iPadOS-Gerät installierte Intune-Unternehmensportal-App   

Zudem müssen Sie sich beim Setup an einen Purebred-Agent oder -Mitarbeiter wenden.      

## <a name="enroll-device"></a>Registrieren eines Geräts  
1. Öffnen Sie die Unternehmensportal-App für iOS/iPadOS auf Ihrem mobilen Gerät, und melden Sie sich mit Ihrem Geschäftskonto an.  

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
    b. Klicken Sie auf **Öffnen**, um die Purebred-App zu öffnen.  

    ![Beispielscreenshot des Bildschirms „Zugriff auf mobile Smartcard einrichten“ im Unternehmensportal](./media/smart-card-open-disa-purebred.png)  
9. Wenn Sie gefragt werden, ob das Unternehmensportal die Purebred-Registrierungs-App öffnen darf, wählen Sie **Öffnen** aus.   

    ![Beispielscreenshot der Eingabeaufforderung des Unternehmensportals zum Öffnen der DISA Purebred-App](./media/open-app-prompt-disa-purbred.png)  
10. Wenn die App funktioniert, arbeiten Sie mit dem Purebred-Agent Ihrer Organisation zusammen, um das Purebred-Konfigurationsprofil für die Vorabregistrierung zu konfigurieren und herunterzuladen.   
11. Wechseln Sie zu den Einstellungen der App > **Allgemein** > **Profile und Geräteverwaltung** > **Profil Installieren**, und tippen Sie auf **Installieren**.  
12. Geben Sie Ihren Gerätepasscode ein.  
13. Installieren des Profils Möglicherweise müssen Sie mehr als einmal auf **Installieren** tippen, um die Installation zu starten. 
14. Kehren Sie zur Purebred-Registrierungs-App zurück. Befolgen Sie die Anweisungen Ihres Purebred-Agents, um den Vorgang fortzusetzen.  
 
15. Nach dem Download des Konfigurationsprofils wechseln Sie zu den Einstellungen der App > **Allgemein** > **Profile und Geräteverwaltung** > **Profil Installieren**, und tippen Sie auf **Installieren**.   
16.  Geben Sie Ihren Gerätepasscode ein.
17. Installieren des Profils Möglicherweise müssen Sie mehr als einmal auf **Installieren** tippen, um die Installation zu starten. 
18. Kehren Sie nach Abschluss der Installation zur Unternehmensportal-App zurück.  
19.  Tippen Sie in der Anzeige **Zugriff auf mobile Smartcard einrichten** auf **Weiter**.  

20. Über die Anzeige **Importzertifikate** können Sie die von DISA Purebred erhaltenen abgeleiteten Anmeldeinformationen abrufen und importieren.  

    a. Tippen Sie auf **Weiter**.   

    ![Beispielscreenshot der Unternehmensportal-Anzeige zum Importieren der Zertifikate](./media/import-certificate-disa-purebred.png)  
    b. Wechseln Sie zu iCloud Drive **Durchsuchen** > **Speicherorte**, und tippen Sie auf **Weitere Speicherorte**.  

    ![Beispielscreenshot von iCloud Drive, Menü „Durchsuchen“ mit hervorgehobener Option „Weitere Speicherorte“](./media/icloud-drive-more-locations.png)  
    c. Tippen Sie auf den Schalter, um **Purebred Key Chain** (Purebred-Schlüsselkette) zu aktivieren.  

    ![Beispielscreenshot von iCloud Drive, Ansicht „Durchsuchen“ mit hervorgehobenem Schalter „Purebred Key Chain“, der aktiviert ist.](./media/icloud-drive-enable-purebred-keychain.png)   

    d. Tippen Sie auf **Purebred Credential Package** (Paket mit Purebred-Anmeldeinformationen).  

    ![Beispielscreenshot einer iOS-Anzeige mit auswählbarer Option für das Paket mit Purebred-Anmeldeinformationen](./media/purebred-credential-package.png)  
    f. Eine Liste der Zertifikate wird angezeigt. Wählen Sie eines aus, und tippen Sie dann auf **Schlüssel importieren**.  

    ![Beispielscreenshot einer Liste auswählbarer Zertifikate, von denen eines bereits ausgewählt ist.](./media/import-purebred-keychain.png) 
21. Kehren Sie zur Unternehmensportal-App zurück, und warten Sie, bis das Einrichten Ihres Geräts im Unternehmensportal abgeschlossen ist.   

## <a name="next-steps"></a>Nächste Schritte  
Nach der Registrierung haben Sie Zugriff auf Arbeitsressourcen wie E-Mail, WLAN und alle Apps, die Ihre Organisation zur Verfügung stellt. Weitere Informationen darüber, wie Sie Apps im Unternehmensportal erhalten, suchen, installieren und deinstallieren können, finden Sie unter:

* [Verwalten von Apps von der Unternehmensportalwebsite](manage-apps-cpweb.md)  
* [Verwenden verwalteter Apps auf Ihrem Gerät](use-managed-apps-on-your-device-ios.md)  

Benötigen Sie weitere Unterstützung? Kontaktieren Sie den Support Ihres Unternehmens. Die entsprechenden Kontaktinformationen finden Sie auf der [Unternehmensportal-Website](https://go.microsoft.com/fwlink/?linkid=2010980).
