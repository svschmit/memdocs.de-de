---
title: Registrieren eines Windows 10-Geräts beim Intune-Unternehmensportal | Microsoft-Dokumentation
description: Schritte zum Registrieren von Windows 10-Geräten beim Intune-Unternehmensportal
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 09/09/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 812e82df-76df-402b-bfe9-29302838f40e
searchScope:
- User help
ROBOTS: ''
ms.reviewer: amanh
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 46f8d7d46e376d2fb8f1cab1b3d0b3bc583bdeed
ms.sourcegitcommit: d4ed7b4369389fd8ab07d28a7fa507797b6c6e57
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89643464"
---
# <a name="enroll-windows-10-devices-with-intune-company-portal"></a>Registrieren von Windows 10-Geräten mit dem Intune-Unternehmensportal

Verwenden Sie das Intune-Unternehmensportal zum Registrieren der Windows 10-Geräte Ihrer Organisation. In diesem Artikel wird beschrieben, wie Sie Windows 10-Geräte (Version 1607 und höher bzw. Version 1511 und früher) registrieren. Bevor Sie mit der Registrierung beginnen, sollten Sie sicherstellen, dass Sie die [Version auf Ihrem Gerät überprüfen](windows-enrollment-company-portal.md#find-windows-10-version-number), um die richtigen Schritte auszuführen.  

Windows 10 wird von verschiedenen Gerätetypen unterstützt (einschließlich Desktop, Smartphone und Tablet). Die Schritte für die Registrierung sind auf allen Geräten gleich. Jedoch ist es möglich, dass die auf Ihrem Bildschirm angezeigten Schritte von denen in diesem Artikel abweichen.  
</br>
> [!VIDEO https://www.youtube.com/embed/TKQxEckBHiE?rel=0]

## <a name="enroll-windows-10-version-1607-and-later-device"></a>Registrieren von Windows 10-Geräten (Version 1607 und höher) 
In diesen Schritten wird beschrieben, wie Sie ein Windows 10-Gerät (Version 1607 und höher) registrieren.  

1. Öffnen Sie das **Startmenü**. 

2. Öffnen Sie die App **Einstellungen**. Wenn die App in der Liste Ihrer Apps noch nicht verfügbar ist, navigieren Sie zur Suchleiste und geben „Einstellungen“ ein.

3. Wählen Sie **Konten** > **Zugriff auf Geschäfts-, Schul- oder Unikonto** > **Verbinden** aus.  


    ![Wählen Sie „Auf Geschäfts-,Schul- oder Unikonto zugreifen“ aus](./media/w10-enroll-rs1-connect-to-work-or-school.png)  

4. Um zur Intune-Anmeldeseite Ihrer Organisation zu gelangen, geben Sie Ihre Geschäfts-, Schul- oder Uni-E-Mail-Adresse ein. Klicken Sie dann auf **Weiter**.  


   ![Enter your work or school-account](./media/w10-enroll-rs1-set-up-work-or-school-account.png)  

5. Melden Sie sich mit Ihrem Geschäfts-, Schul- oder Unikonto bei Intune an.  


    ![Geschäfts- oder Schulkonto hinzufügen](./media/w10-enroll-rs1-enter-your-credentials.png)  

    In einer Meldung wird schließlich angezeigt, dass Ihr Unternehmen oder Ihre Bildungseinrichtung das Gerät registriert.

6. Wenn Ihre Organisation vorgibt, dass Sie eine PIN für Windows Hello einrichten müssen, werden Sie aufgefordert, einen Prüfcode einzugeben. Geben Sie den Code ein, und führen Sie die auf dem Bildschirm angezeigten Schritte aus, um eine PIN zu erstellen.  

7. Auf dem Bildschirm **Alles erledigt!** wählen Sie **Fertig** aus. Ihr Gerät ist jetzt bei registriert.  

8. Wechseln Sie zu **Einstellungen** > **Konten** > **Access work or school** (Zugriff auf Geschäft, Schule oder Uni), um Ihre Verbindung zu überprüfen.  Ihr Konto sollte jetzt in der Liste aufgeführt werden.  


## <a name="enroll-windows-10-version-1511-and-earlier-device"></a>Registrieren von Windows 10-Geräten (Version 1511 und früher)  
In diesen Schritten wird beschrieben, wie Sie ein Windows 10-Gerät (Version 1511 und früher) registrieren.  

1. Öffnen Sie das **Startmenü**. 

2. Öffnen Sie die App **Einstellungen**. Wenn die App in der Liste Ihrer Apps noch nicht verfügbar ist, navigieren Sie zur Suchleiste und geben „Einstellungen“ ein.

3. Klicken Sie auf **Konten** > **Your account** (Ihr Konto).  


    ![Wählen Sie „Ihr Konto“ aus.](./media/W10-enroll-2-accounts-your-account.png)  

5. Wählen Sie **Geschäfts- oder Schulkonto hinzufügen** aus.  


    ![Wählen Sie „Geschäfts- oder Schulkonto hinzufügen“ aus.](./media/w10-enroll-3-add-work-school-acct.png)  

6. Melden Sie sich mit den Anmeldeinformationen Ihres Geschäfts- oder Schulkontos an.  


    ![Anmelden](./media/W10-enroll-4-sign-in.png)  


## <a name="troubleshooting"></a>Problembehandlung 
Eine nicht abschließende Liste der Fehlermeldungen und weiterer Lösungsmöglichkeiten für Verbindungsfehler finden Sie unter [Problembehandlung für den Windows 10-Gerätezugriff](troubleshoot-your-windows-10-device-windows.md).  


## <a name="it-administrator-support"></a>Unterstützung für IT-Administratoren   

Wenn Sie IT-Administrator sind und Probleme bei der Registrierung von Geräten haben, lesen Sie [Troubleshooting Windows device enrollment problems in Microsoft Intune (Behandeln von Problemen bei der Registrierung von Windows-Geräten in Microsoft Intune)](https://support.microsoft.com/help/4469913). In diesem Artikel werden häufige Fehler, ihre Ursachen und Schritte zur Behebung aufgelistet. 

## <a name="next-steps"></a>Nächste Schritte  
Wenden Sie sich an das IT-Supportteam Ihrer Organisation, wenn Sie Hilfe bei der Verwendung des Unternehmensportals oder der Registrierung benötigen. Die erforderlichen Kontaktinformationen finden Sie auf der [Unternehmensportal-Website](https://go.microsoft.com/fwlink/?linkid=2010980). Melden Sie sich mit Ihrem Geschäfts-, Schul- oder Unikonto bei der Website an.  

 

