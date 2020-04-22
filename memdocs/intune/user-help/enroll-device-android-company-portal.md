---
title: Registrieren eines Android-Geräts im Intune-Unternehmensportal | Microsoft-Dokumentation
description: Beschreibt, wie Sie ein Android-Gerät im Intune-Unternehmensportal registrieren
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/01/2020
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 0ed3a002-7533-4001-ae24-e10b64b66620
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 0c9bf96188e27afeaf66e7b2897f8cda19f9df37
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "80551651"
---
# <a name="enroll-your-device-with-company-portal"></a>Registrieren Ihres Geräts im Unternehmensportal  
Registrieren Sie Ihr privates oder unternehmenseigenes Android-Gerät, um sicheren Zugriff auf Unternehmens-E-Mails, -Apps und -Daten zu erhalten. Das Unternehmensportal unterstützt Android-Geräte, einschließlich Samsung Knox, mit Android 4.4 und höher.  
</br>
> [!VIDEO https://www.youtube.com/embed/k0Q_sGLSx6o?rel=0]

> [!NOTE]
> Samsung Knox ist ein Sicherheitssystem, mit dem bestimmte Geräte von Samsung neben den nativen Android-Sicherheitsfeatures zusätzlichen Schutz bieten. Navigieren Sie zu **Einstellungen** > **System > Über das Telefon**, um zu überprüfen, ob es sich bei Ihrem Gerät um ein Samsung Knox-Gerät handelt. Wird dort keine **Knox-Version** angezeigt, verfügen Sie über ein natives Android-Gerät.

## <a name="enroll-device"></a>Registrieren eines Geräts  
Installieren Sie die Intune-Unternehmensportal-App [über Google Play](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal). Eine Liste der Geschäfte, die die App auf dem chinesischen Festland anbieten, finden Sie unter [Installieren der Unternehmensportal-App auf dem chinesischen Festland](install-company-portal-android-china.md).    

Während der Registrierung werden Sie möglicherweise aufgefordert, eine Kategorie auszuwählen, die am besten beschreibt, wie Sie Ihr Gerät nutzen. Der Support Ihres Unternehmens verwendet Ihre Antwort, um die Apps zu überprüfen, auf die Sie Zugriff haben.  

1. Öffnen Sie die Unternehmensportal-App, und melden Sie sich mit Ihrem Geschäfts-, Schul- oder Unikonto an.  

2. Wenn Sie dazu aufgefordert werden, die Geschäftsbedingungen Ihrer Organisation zu akzeptieren, tippen Sie auf **ALLE AKZEPTIEREN**.  

   ![Beispielbild der Nutzungsbedingungen des Unternehmensportals mit hervorgehobener Schaltfläche „Alle akzeptieren“.](./media/accept-terms-1911.png)  


3. Überprüfen Sie, was Ihre Organisation sehen kann und was nicht. Tippen Sie dann auf **WEITER**.


    ![Beispielbild des Unternehmensportals mit dem Bildschirm „We care about your privacy“ (Ihre Privatsphäre ist uns wichtig) mit hervorgehobener Schaltfläche „Continue“ (Weiter)](./media/android-privacy-screen-1911.png)  
4. Lesen Sie, was Sie in den nächsten Schritten erwartet. Tippen Sie dann auf **WEITER**.  

    ![Beispielbild der Anzeige „Wie geht es weiter?“ des Unternehmensportals mit hervorgehobener Schaltfläche „Weiter“.](./media/android-whats-next-1911.png)  


5. Abhängig von Ihrer Android-Version werden Sie möglicherweise aufgefordert, den Zugriff auf bestimmte Teile des Geräts zuzulassen. Diese Eingabeaufforderungen werden von Google benötigt und nicht von Microsoft kontrolliert.  

    Tippen Sie auf **Zulassen** für die folgenden Berechtigungen:  
    * **Zulassen, dass das Unternehmensportal Telefonanrufe tätigt und verwaltet**: Diese Berechtigung ermöglicht es Ihrem Gerät, seine internationale IMEI-Nummer (International Mobile Station Equipment Identity) mit Intune, dem Geräteverwaltungsanbieter Ihrer Organisation, zu teilen. Es ist sicher, diese Berechtigung zuzulassen. Microsoft wird niemals Telefonanrufe tätigen oder verwalten.  
    * **Zulassen, dass das Unternehmensportal auf Ihre Kontakte zugreift**: Diese Berechtigung erlaubt der Unternehmensportal-App das Erstellen, Verwenden und Verwalten Ihres Geschäftskontos.  Es ist sicher, diese Berechtigung zuzulassen. Microsoft greift nie auf Ihre Kontakte zu. 

    Wenn Sie die Berechtigung verweigern, werden Sie bei der nächsten Anmeldung im Unternehmensportal nochmals dazu aufgefordert. Wenn Sie dies nicht wünschen, wählen Sie **Never ask again** (Nicht noch mal fragen) aus. Um App-Berechtigungen zu verwalten, wechseln Sie zu den Einstellungen der App > **Apps** > **Unternehmensportal** > **Berechtigungen** > **Telefon**.  

6. Aktivieren Sie die Geräteadministrator-App. 

    Das Unternehmensportal benötigt Geräteadministratorberechtigungen, um Ihr Gerät sicher zu verwalten. Durch die Aktivierung der App kann Ihre Organisation mögliche Sicherheitsprobleme identifizieren, wie z.B. wiederholte fehlgeschlagene Versuche, Ihr Gerät zu entsperren, und entsprechend reagieren.  

    ![Beispielbild der Anzeige „Geräteadministrator aktivieren“ mit hervorgehobener Schaltfläche „Aktivieren“.](./media/activate-device-administrator-1911.png)  

> [!NOTE]
> Die Meldungen auf diesem Bildschirm werden nicht von Microsoft kontrolliert. Wir wissen, dass deren Formulierungen etwas drastisch erscheinen können. Das Unternehmensportal kann nicht angeben, welche Einschränkungen und welche Zugriffsberechtigungen für Ihre Organisation relevant sind. Wenn Sie Fragen zur Nutzung der Anwendung in Ihrer Organisation haben, wenden Sie sich an Ihren IT-Supportmitarbeiter. Besuchen Sie die [Unternehmensportal-Website](https://go.microsoft.com/fwlink/?linkid=2010980), um die Kontaktinformationen für Ihre Organisation zu erhalten.  


7. Das Gerät beginnt mit der Registrierung. Wenn Sie ein Samsung Knox-Gerät verwenden, werden Sie aufgefordert, zunächst die Datenschutzrichtlinie des ELM-Agents zu lesen und zu akzeptieren.   

    ![Beispielbild der Anzeige „Samsung Knox-Datenschutzrichtlinie“, die während der Registrierung angezeigt wird.](./media/and-enroll-7-knox-privacy-policy.png)  

8. Überprüfen Sie auf dem Bildschirm **Unternehmenszugriff einrichten**, ob Ihr Gerät registriert wurde. Tippen Sie dann auf **WEITER**.  

    ![Beispielabbildung der Anzeige „Unternehmenszugriff einrichten“ des Unternehmensportals, auf der zu sehen ist, dass „Gerät in die Verwaltung einbinden“ abgeschlossen ist.](./media/update-settings-1911.png)  

9. In Ihrer Organisation ist es möglicherweise erforderlich, dass Sie Ihre Geräteeinstellungen aktualisieren. Tippen Sie auf **AUFLÖSEN**, um eine Einstellung anzupassen. Wenn Sie mit dem Aktualisieren der Einstellungen fertig sind, tippen Sie auf **WEITER**.  

   ![Beispielabbildung der Anzeige „Geräteeinstellungen aktualisieren“ des Unternehmensportals mit hervorgehobenen Schaltflächen „Auflösen“ und „Weiter“.](./media/resolve-settings-1911.png)  

10. Wenn das Setup abgeschlossen ist, tippen Sie auf **FERTIG**.    

    ![Beispielabbildung des Unternehmensportals, Bildschirm „Geräteeinstellungen aktualisieren“, mit dem abgeschlossenen Setup und hervorgehobener Schaltfläche „Done“ (Fertig)](./media/android-enrollment-done-1911.png) 

## <a name="next-steps"></a>Nächste Schritte  

Bevor Sie versuchen, Bildungseinrichtungs- oder Unternehmens-Apps zu installieren, navigieren Sie zu **Einstellungen** > **Sicherheit**, und aktivieren Sie **Unknown sources** (Unbekannte Quellen). Wenn Sie diese Option nicht aktivieren, wird die folgende Meldung angezeigt, wenn Sie versuchen, eine App zu installieren: "Installation blockiert. Aus Sicherheitsgründen ist Ihr Gerät so eingestellt, dass die Installation von Apps aus unbekannten Quellen blockiert wird.“ Sie können auf der Meldung auf **Einstellungen** tippen, um direkt zu **Unknown sources** (Unbekannte Quellen) zu wechseln.  

> [!Note]
> Wenn Ihre Organisation Telecom Expense Management-Software verwendet, müssen Sie ein paar zusätzliche Schritte ausführen, bevor das Gerät vollständig registriert ist. [Hier](enroll-your-device-with-telecom-expense-management-android.md) erfahren Sie mehr.

Sollte beim Versuch der Registrierung Ihres Geräts bei Intune ein Fehler auftreten, können Sie [Registrierungsfehler an den Support Ihres Unternehmens senden](send-logs-to-your-it-admin-by-email-android.md).  

Benötigen Sie weitere Unterstützung? Kontaktieren Sie den Support Ihres Unternehmens. Die entsprechenden Kontaktinformationen finden Sie auf der [Unternehmensportal-Website](https://go.microsoft.com/fwlink/?linkid=2010980).  