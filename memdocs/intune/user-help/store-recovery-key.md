---
title: Speichern eines Wiederherstellungsschlüssels in Intune über die Unternehmensportalwebsite
description: In diesem Artikel erfahren Sie, wie Sie Ihren Gerätewiederherstellungsschlüssel über die Unternehmensportalwebsite hochladen und speichern.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/17/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: annochiva
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 826515026e578cb993bb706fc61dedb4a80fb3e6
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2020
ms.locfileid: "86465019"
---
# <a name="store-your-personal-filevault-key"></a>Speichern Ihres persönlichen FileVault-Schlüssels 

Speichern Sie einen FileVault-Schlüssel für Ihr persönlich verschlüsseltes macOS-Gerät. Indem Sie Ihren Schlüssel in Intune speichern erfüllen Sie Verschlüsselungsanforderungen und ermöglichen Folgendes: 

* Sie können den Schlüssel über ein beliebiges Gerät einfach und schnell abrufen oder rotieren. 
* Wenden Sie sich an Ihren Support, um Hilfe zu erhalten, wenn Sie den Schlüssel abrufen oder rotieren müssen und nicht auf die Apps oder die Website zugreifen können, um dies selbst zu tun.


## <a name="retrieve-or-rotate-the-key"></a>Abrufen oder Rotieren des Schlüssels

Wenn Ihr Gerät gesperrt wird, stehen Ihnen die folgenden Möglichkeiten zum Abrufen Ihres Schlüssels zur Auswahl:
   
- Unternehmensportal-Website
- Unternehmensportal-App für iOS oder iPadOS 
- Unternehmensportal-App für Android
- Intune-App
 
 Der IT-Support kann Ihren persönlichen Schlüssel mithilfe des Administratorzugriffs auf Intune für Sie rotieren, wenn Ihr Gerät gesperrt wird. Außerdem kann der Support die Schlüssel anzeigen, sofern diese zu unternehmenseigenen Geräten gehören. Die IT-Supportmitarbeiter können keine Wiederherstellungsschlüssel einsehen, die zu persönlichen Geräten gehören.   


## <a name="do-i-need-to-store-my-key"></a>Muss der Schlüssel gespeichert werden?  
Ein IT-Supportmitarbeiter wird Sie darüber informieren, ob Sie einen persönlichen Wiederherstellungsschlüssel hochladen müssen. Möglicherweise erhalten Sie eine Benachrichtigung von den Unternehmensportal-Apps für iOS/iPadOS oder Android, wenn die IT-Abteilung Ihrer Organisation auf diese Weise mit Ihnen kommuniziert. 

Es wird empfohlen, einen Wiederherstellungsschlüssel nur hochzuladen, wenn Sie in eine der folgenden Kategorien fallen:
* Sie haben Ihr Gerät verschlüsselt, bevor Sie es bei Ihrer Organisation registriert haben. 
* Sie haben Ihr Gerät manuell über die macOS-Systemeinstellungen verschlüsselt.   

Abhängig von den Richtlinien Ihrer Organisation wird der Zugriff auf Unternehmensressourcen über Ihr Gerät möglicherweise gesperrt, bis Sie Ihren Schlüssel hochgeladen haben.  

## <a name="upload-personal-recovery-key"></a>Hochladen eines persönlichen Wiederherstellungsschlüssels 
Führen Sie die folgenden Schritte aus, um den persönlichen FileVault-Schlüssel für Ihr verschlüsseltes Mac-Gerät zu speichern.  


1. Rufen Sie die [Unternehmensportalwebsite](https://portal.manage.microsoft.com) auf, und melden Sie sich mit Ihrem Geschäfts-, Schul- oder Unikonto an. 
2. Wählen Sie Ihr verschlüsseltes Gerät aus.
3. Klicken Sie auf **Wiederherstellungsschlüssel speichern**.  
4. Geben Sie Ihren alphanumerischen FileVault-Schlüssel mit 24 Zeichen ein.  
5. Geben Sie den Schlüssel nochmal ein. Klicken Sie dann auf **Speichern**.
6. Das Unternehmensportal versucht dann, Ihren persönlichen Wiederherstellungsschlüssel zu verifizieren, zu rotieren und zu speichern. Sobald der Schlüssel gespeichert wurde, sind keine weiteren Aktionen erforderlich. Wenn Sie die Website verlassen, bevor der Upload abgeschlossen ist, können Sie seinen Status auf der Gerätedetailseite anzeigen, wenn Sie sich das nächste Mal anmelden.  

Weitere Informationen über die Meldungen, die Ihnen während dieses Prozesses angezeigt werden können, finden Sie unter [Unternehmensportalnachrichten](store-recovery-key.md#company-portal-messages).  

## <a name="company-portal-messages"></a>Unternehmensportalnachrichten

|Nachricht  |Bedeutung  |
|---------|---------|
|Die Schlüssel müssen übereinstimmen. Überprüfen Sie die Schlüssel, und versuchen Sie es noch mal.     | Diese Meldung wird unter dem Feld **Wiederherstellungsschlüssel bestätigen** angezeigt, um Sie darüber zu informieren, dass Ihre Schlüssel nicht übereinstimmen. Geben Sie die Schlüssel in beiden Feldern erneut ein, und wiederholen Sie dann den Speichervorgang.        |
|Der Wiederherstellungsschlüssel für das Gerät konnte nicht aktualisiert werden.| Diese Meldung wird am oberen Bildschirmrand als Popupbenachrichtigung angezeigt, wenn das Unternehmensportal einen Wiederherstellungsschlüssel nicht für Sie speichern konnte. Weitere Informationen erhalten Sie, indem Sie Ihr verschlüsseltes Gerät auswählen. Lesen Sie dann die Meldung ganz oben auf der Seite, um Anweisungen für die nächsten Schritte zu erhalten. |
|Der Wiederherstellungsschlüssel konnte nicht hochgeladen werden. Überprüfen Sie, ob Sie den richtigen Schlüssel eingegeben haben, und versuchen Sie es noch mal. Wenn das Problem weiterhin besteht, führen Sie eine manuelle Schlüsselrotation durch. Tippen Sie, um weitere Informationen zu erhalten.     | Diese Meldung wird auf der Gerätedetailseite angezeigt und könnte auf mehrere Dinge hindeuten: Das Unternehmensportal konnte Ihren Schlüssel nicht rotieren und speichern, weil der eingegebene Schlüssel falsch ist. Stellen Sie sicher, dass Sie über den richtigen Schlüssel verfügen, und versuchen Sie es nochmal. Der zweite mögliche Fall besteht darin, dass Ihr Gerät seit einiger Zeit nicht bei Ihrer Organisation eingecheckt wurde. Wählen Sie Ihr Gerät aus, und klicken Sie auf **Status** > **Zugriff überprüfen**, um die neuesten Updates von Ihrer Organisation zu synchronisieren. Versuchen Sie dann noch mal, den Wiederherstellungsschlüssel zu speichern. Wenn das Problem weiterhin besteht, könnte dies schließlich bedeuten, dass Ihre Organisation FileVault nicht auf ihrer Seite aktiviert haben. Wenden Sie sich an Ihren IT-Support, und informieren Sie ihn darüber, dass Sie Ihr Gerät synchronisiert haben, aber Ihren FileVault-Schlüssel weiterhin nicht speichern können.         |
|Der Wiederherstellungsschlüssel wurde aktualisiert. Wenn Sie jemals von Ihrem Gerät ausgesperrt werden und Ihren Schlüssel abrufen müssen, melden Sie sich beim Unternehmensportal an, und wählen Sie **Wiederherstellungsschlüssel abrufen** aus.    | Diese Meldung wird auf der Gerätedetailseite angezeigt. Der von Ihnen gespeicherte Schlüssel wurde erfolgreich rotiert, und Ihr neuer persönlicher Wiederherstellungsschlüssel wird gespeichert.    |



## <a name="it-pro-support"></a>IT Pro-Support

Wenn Sie ein IT-Supportmitarbeiter sind und die FileVault-Verschlüsselung für die Mac-Geräte Ihrer Organisation konfigurieren und verwalten möchten, finden Sie weitere Informationen unter [Verwenden der FileVault-Datenträgerverschlüsselung für macOS mit Intune](https://docs.microsoft.com/mem/intune/protect/encrypt-devices-filevault).  

## <a name="next-steps"></a>Nächste Schritte

Sie können Ihren Schlüssel jederzeit über die Unternehmensportalwebsite, die Intune-App und die Unternehmensportal-Apps für iOS und Android abrufen. Diesen können Sie dann für den Zugriff auf Ihr Mac-Gerät verwenden. Weitere Informationen zum Abrufen Ihres Wiederherstellungsschlüssels finden Sie unter [Abrufen des Wiederherstellungsschlüssels](get-recovery-key-cpweb.md).

Außerdem können Sie mehr darüber erfahren, welche Aktionen Sie auf der Unternehmensportalwebsite ausführen können. Eine Liste dieser Aktionen finden Sie unter [Verwenden der Intune-Unternehmensportalwebsite](using-the-intune-company-portal-website.md).  

Benötigen Sie weitere Unterstützung? Wenden Sie sich an Ihren Ansprechpartner beim IT-Support. Die entsprechenden Kontaktinformationen finden Sie auf der [Unternehmensportal-Website](https://go.microsoft.com/fwlink/?linkid=2010980).  
