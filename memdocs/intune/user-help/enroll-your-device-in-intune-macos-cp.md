---
title: Registrieren eines Mac-Geräts im Intune-Unternehmensportal | Microsoft-Dokumentation
description: In diesem Artikel erfahren Sie, wie Sie Ihr Mac-Gerät über die Unternehmensportal-App in Intune registrieren.
keywords: Mac OS X, macOS, OS X
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/16/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 3bb659cc-9b57-4d19-8631-2c26749fa71c
searchScope:
- User help
ROBOTS: ''
ms.reviewer: kakyker
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 2ef7951217b0b6df21a86ca29a8637385aa65715
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "79337017"
---
# <a name="enroll-your-macos-device-using-the-company-portal-app"></a>Registrieren eines macOS-Geräts mithilfe der Unternehmensportal-App  

Registrieren Sie Ihr macOS-Gerät bei der Intune-Unternehmensportal-App, um sicheren Zugriff auf E-Mails, Dateien und Apps Ihres Geschäfts-, Schul- oder Unikontos zu erhalten.

Organisationen verlangen in der Regel, dass Sie Ihr Gerät registrieren, bevor Sie auf proprietäre Daten zugreifen können. Sobald Ihr Gerät registriert ist, gilt es als *verwaltet*. Ihre Organisation kann dem Gerät über einen MDM-Anbieter (Mobile Device Management, Verwaltung mobiler Geräte) wie Intune Richtlinien und Anwendungen zuweisen. Sie müssen Ihr Gerät entsprechend der Richtlinieneinstellungen Ihrer Organisation konfigurieren, um über Ihr Gerät kontinuierlich auf Ihre Geschäfts-, Schul- oder Uniressourcen zugreifen zu können.  

In diesem Artikel wird beschrieben, wie Sie Ihr Gerät mit der Unternehmensportal-App für macOS registrieren, konfigurieren und verwalten, um die Anforderungen Ihrer Organisation zu erfüllen.  


## <a name="what-to-expect-from-the-company-portal-app"></a>Vorteile der Unternehmensportal-App

Während der ersten Einrichtung werden Sie von der Unternehmensportal-App aufgefordert, sich anzumelden und bei der Organisation zu authentifizieren. Das Unternehmensportal informiert Sie dann über jegliche Geräteeinstellungen, die Sie konfigurieren müssen, um die Anforderungen Ihrer Organisation zu erfüllen. Beispielsweise legen Organisationen oft Anforderungen an die minimale oder maximale Zeichenanzahl des Kennworts fest, die Sie einhalten müssen.    

Nachdem Sie Ihr Gerät registriert haben, stellt das Unternehmensportal immer sicher, dass Ihr Gerät gemäß der Anforderungen Ihrer Organisation geschützt ist. Wenn Sie beispielsweise eine App aus einer nicht vertrauenswürdigen Quelle herunterladen, zeigt das Unternehmensportal eine Warnung an und schränkt womöglich Ihren Zugriff auf die Ressourcen der Organisation ein. App-Schutzrichtlinien wie diese sind üblich. Sie müssen wahrscheinlich die nicht vertrauenswürdige App deinstallieren, um den Zugriff wieder zu erhalten. 

Wenn Ihre Organisation nach der Registrierung eine neue Sicherheitsanforderung durchsetzt, z. B. die mehrstufige Authentifizierung, erhalten Sie eine Benachrichtigung vom Unternehmensportal. Sie haben dann die Möglichkeit, Ihre Einstellungen so zu ändern, dass Sie von Ihrem Gerät aus weiterarbeiten können.  

Weitere Informationen zur Registrierung finden Sie unter [Was geschieht, wenn ich die Unternehmensportal-App installiere und mein Gerät registriere?](what-happens-if-you-install-the-Company-Portal-app-and-enroll-your-device-in-intune-macos.md).  

## <a name="get-your-macos-device-managed"></a>Verwaltung Ihres macOS-Geräts  
Führen Sie die folgenden Schritte aus, um Ihr macOS-Gerät bei Ihrer Organisation zu registrieren. Auf dem macOS-Gerät muss macOS 10.12 oder höher ausgeführt werden.   

> [!NOTE]
> Im Laufe dieses Prozesses werden Sie möglicherweise dazu aufgefordert, dem Unternehmensportal die Verwendung vertraulicher Informationen zu verwenden, die in Ihrem Schlüsselbund gespeichert sind. Diese Eingabeaufforderungen sind Teil der Apple-Sicherheit. Wenn die Eingabeaufforderung angezeigt wird, geben Sie Ihre Anmeldeinformationen und Ihr Kennwort für den Schlüsselbund ein, und wählen Sie dann **Immer zulassen** aus. Wenn Sie die **EINGABETASTE** oder die **ENTERTASTE** auf Ihrer Tastatur drücken, wird in der Eingabeaufforderung die Option **Zulassen** bestätigt, was zu weiteren Eingabeaufforderungen führen kann.  

### <a name="install-company-portal-app"></a>Installieren der Unternehmensportal-App  
1. Fahren Sie mit dem Abschnitt [Registrieren eines Mac-Geräts](https://go.microsoft.com/fwlink/?linkid=853070) fort.  
2. Die PGK-Installationsdatei für das Unternehmensportal wird heruntergeladen. Öffnen Sie das Installationsprogramm, und führen Sie die Schritte durch. 
3. Stimmen Sie den Softwarelizenzbedingungen zu. 
4. Geben Sie Ihr Gerätekennwort ein, oder nutzen Sie Ihren registrierten Fingerabdruck, um die Software zu installieren.  
5. Öffnen Sie das Unternehmensportal. 

> [!IMPORTANT]
> Möglicherweise wird Microsoft AutoUpdate geöffnet, um Ihre Microsoft-Software zu aktualisieren. Öffnen Sie die Unternehmensportal-App, nachdem Sie alle Updates installiert haben. Installieren Sie für die optimale Einrichtung die neuesten Versionen von Microsoft AutoUpdate und dem Unternehmensportal.  


### <a name="enroll-your-mac"></a>Registrieren eines Mac-Geräts  


1. Melden Sie sich mit Ihrem Geschäfts-, Schul- oder Unikonto beim Unternehmensportal an.  
2. Wenn die App geöffnet wird, klicken Sie auf **Beginnen**.  
3. Überprüfen Sie, was Ihre Organisation auf Ihrem registrieren Gerät sehen kann und was nicht. Wählen Sie dann **Weiter** aus.
4.  Geben Sie Ihr Gerätekennwort in der Anzeige **Verwaltungsprofil installieren** ein, wenn Sie dazu aufgefordert werden.

    ![Beispielscreenshot: Anzeige „Verwaltungsprofil installieren“ mit hervorgehobener Kennworteingabeaufforderung des Unternehmensportals](./media/install-management-profile-macos-1912.PNG)   
5. Klicken Sie in der Anzeige **Geräteverwaltung bestätigen** auf **Systemeinstellungen öffnen**.  

    ![Beispielscreenshot: Anzeige „Geräteverwaltung bestätigen“ mit hervorgehobener Schaltfläche „Systemeinstellungen öffnen“](./media/confirm-device-management-macos-1912.PNG)  
6. Daraufhin werden die Systemeinstellungen Ihres Geräts geöffnet. Wählen Sie **Verwaltungsprofil** aus der Geräteprofilliste aus, und klicken Sie dann auf **Zulassen** > **Zulassen**.  
    ![Beispielscreenshot: Systemeinstellungen und Verwaltungsprofilanzeige mit hervorgehobener Schaltfläche „Zulassen“](./media/management-profile-approve-macos-1912.PNG)   
1. Kehren Sie zum Unternehmensportal zurück, und klicken Sie auf **Fortfahren**.    
2. In Ihrer Organisation ist es möglicherweise erforderlich, dass Sie Ihre Geräteeinstellungen aktualisieren. Klicken Sie auf **Einstellungen überprüfen**, nachdem Sie die Einstellungen angepasst haben.  

    ![Beispielscreenshot: Anzeige „Geräteeinstellungen aktualisieren“ mit hervorgehobener Schaltfläche „Einstellungen überprüfen“ des Unternehmensportals](./media/update-settings-mac-1911.PNG)  
9. Klicken Sie nach Abschluss des Setups auf **Fertig**.  


 ## <a name="troubleshooting-and-feedback"></a>Problembehandlung und Feedback   

Wenn Probleme bei der Registrierung auftreten, navigieren Sie zu **Hilfe** > **Diagnosebericht senden**, um das Problem den App-Entwicklern von Microsoft zu melden. Diese Informationen werden zur Verbesserung der App verwendet. Außerdem werden sie dazu verwendet, das Problem zu lösen, wenn Ihr Ansprechpartner des IT-Supports sich an sie wendet.  

Nachdem Sie das Problem an Microsoft gemeldet haben, können Sie Ihre Informationen zum Fehler Ihrem IT-Support-Ansprechpartner mitteilen. Klicken Sie auf **E-Mail-Details**. Geben Sie Ihre Informationen zum Fehler in den Text der E-Mail ein. Die E-Mail-Adresse Ihres Supports finden Sie in der Unternehmensportal-App unter **Kontakt**. Oder sehen Sie auf der [Unternehmensportal-Website](https://go.microsoft.com/fwlink/?linkid=2010980) nach.  
 

Darüber hinaus, freut sich das Team des Microsoft Intune-Unternehmensportals über Ihr Feedback. Navigieren Sie zu **Hilfe** > **Feedback senden**, um Ihre Gedanken und Ideen mitzuteilen.  

## <a name="unverified-profiles"></a>Nicht überprüfte Profile  
Wenn Sie die installierten MDM-Profile (mobile Geräteverwaltung) unter **Systemeinstellungen** > **Profile** anzeigen, wird für einige Profile möglicherweise der Status „Nicht überprüft“ angezeigt. Solange das Verwaltungsprofil den Status „Geprüft“ aufweist, müssen Sie sich keine Sorgen machen.  

Das Verwaltungsprofil definiert die MDM-Kanalverbindung. Solange das Verwaltungsprofil geprüft ist, erben alle anderen Profile, die über diesen Kanal auf dem Computer bereitgestellt werden, die Sicherheitseigenschaften des Verwaltungsprofils.  

## <a name="updating-the-company-portal-app"></a>Aktualisieren der Unternehmensportal-App

Das Aktualisieren des Unternehmensportals erfolgt auf die gleiche Weise wie bei jeder anderen Office-App, nämlich über Microsoft AutoUpdate für macOS. Weitere Informationen finden Sie im Artikel zum [Aktualisieren von Microsoft-Apps für macOS](https://support.office.com/article/Check-for-Office-for-Mac-updates-automatically-bfd1e497-c24d-4754-92ab-910a4074d7c1).  

## <a name="next-steps"></a>Nächste Schritte  
Benötigen Sie weitere Unterstützung? Kontaktieren Sie den Support Ihres Unternehmens. Die entsprechenden Kontaktinformationen finden Sie auf der [Unternehmensportal-Website](https://go.microsoft.com/fwlink/?linkid=2010980).  


