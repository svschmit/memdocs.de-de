---
title: Problembehandlung für den Windows 10-Gerätezugriff auf Geschäfts-, Schul- oder Unikonten | Microsoft Intune
description: Beheben Sie Probleme mit dem Zugriff oder der Kontoverbindung bei einem registrierten Windows 10-Gerät.
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
ms.assetid: 4ab630b6-47ff-443b-a2a5-be23388bcea7
searchScope:
- User help
ROBOTS: ''
ms.reviewer: amanh
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 7c96bef7c1be004714f0b06dd47c9c28850118da
ms.sourcegitcommit: d4ed7b4369389fd8ab07d28a7fa507797b6c6e57
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89643420"
---
# <a name="troubleshoot-windows-10-device-access"></a>Problembehandlung für den Windows 10-Gerätezugriff
Dieser Artikel beschreibt, wie Sie Zugriffsprobleme bei einem registrierten Windows 10-Gerät lösen. 

## <a name="check-wi-fi-connection"></a>Überprüfen der WLAN-Verbindung  

Für den Zugriff auf Geschäfts-, Schul- oder Uniressourcen ist eine WLAN-Verbindung erforderlich. Überprüfen Sie, ob eine Verbindung mit einem WLAN besteht, und versuchen Sie erneut, auf die Ressourcen zuzugreifen.  

## <a name="add-work-or-school-account-in-settings-app"></a>Hinzufügen eines Geschäfts-, Schul- oder Unikontos in der App „Einstellungen“  
Diese Schritte entsprechen denen, die Sie zum Registrieren Ihres Geräts ausgeführt haben. Wenn Ihr Konto jedoch in der App **Einstellungen** nicht angezeigt wird, müssen Sie diese Schritte möglicherweise erneut ausführen.  

1. Öffnen Sie die App **Einstellungen**. 
2. Wählen Sie **Konten** aus.
3. Der nächste Schritt variiert je nach verwendeter Windows 10-Version. 
    * Version 1607 und höher: Wählen Sie **Zugriff auf Geschäfts-, Schul- oder Unikonto** aus.
    * Version 1511 und früher: Wählen Sie **Arbeitsplatzzugriff** aus.  
4. Suchen Sie nach Ihrem Konto. Wenn es nicht aufgeführt wird, wählen Sie die Schaltfläche mit dem Pluszeichen (**Verbinden**), um es hinzuzufügen. 
5. Melden Sie sich mit den Anmeldeinformationen Ihres Geschäfts- oder Schulkontos an. 
6. Befolgen Sie die Anweisungen auf dem Bildschirm, um die Verbindungsherstellung abzuschließen.  
7. Wenn der Vorgang beendet ist, wird Ihr Konto als Verbindung hinzugefügt. Dann haben Sie Zugriff auf alle Ressourcen, die Ihre Organisation zur Verfügung stellt.   

## <a name="contact-it-support-for-access-requirements"></a>Kontaktieren des IT-Supports bezüglich der Zugriffsanforderungen  
Wenn Ihr Geschäfts-, Schul- oder Unikonto in der App „Einstellungen“ aufgeführt wird, sind Ihr Gerät und Ihr Konto bereits verbunden. Wenden Sie sich Ihren IT-Supportkontakt, wenn Sie weitere Hilfe bei Zugriffsproblemen benötigen. Möglicherweise liegen Einschränkungen oder Anforderungen vor, die verhindert, dass Sie auf bestimmte Ressourcen zugreifen können.  

## <a name="error-messages"></a>Fehlermeldungen  

### <a name="we-couldnt-auto-discover-a-management-endpoint-matching-the-username-entered-please-check-your-username-and-try-again-if-you-know-the-url-to-your-management-endpoint-please-enter-it"></a>Ein Verwaltungsendpunkt, der mit dem eingegebenen Benutzernamen übereinstimmt, konnte nicht gefunden werden. Please check your username and try again. Wenn Sie die URL Ihres Verwaltungsendpunkts kennen, geben Sie sie ein.

**Ursache:** Ihr Konto konnte mit der angegebenen URL (auch als Verwaltungsendpunkt bezeichnet) nicht verifiziert werden.  

#### <a name="resolution"></a>Lösung
1. Geben Sie Ihren Benutzernamen und Ihr Kennwort erneut ein. 
2. Wenn der Zugriff weiterhin nicht funktioniert, wenden Sie sich an Ihren IT-Supportkontakt, um die richtige URL zu erhalten (Beispiel: www.IhrUnternehmen.onmicrosoft.com). 
3. Geben Sie die angegebene URL bei entsprechender Aufforderung ein. 

### <a name="it-looks-like-youre-not-connected-make-sure-youre-connected-to-the-network"></a>Anscheinend sind Sie nicht verbunden. Stellen Sie sicher, dass eine Verbindung mit dem Netzwerk besteht.

**Ursache:** Ihr Gerät ist mit keinem WLAN verbunden, aber zum Hinzufügen eines Geschäfts-, Schul- oder Unikontos ist eine Verbindung erforderlich.     

#### <a name="resolution"></a>Lösung
1. Wählen Sie in der Symbolleiste oder den Einstellungen Ihres Geräts das Globussymbol **Netzwerkstatus** aus.
2. Wählen Sie ein WLAN aus, und klicken Sie auf **Verbinden**.  
3. Versuchen Sie erneut, Ihr Konto zu verbinden.  


## <a name="next-steps"></a>Nächste Schritte  

Benötigen Sie weitere Unterstützung? Wenden Sie sich an Ihren Ansprechpartner beim IT-Support. Die entsprechenden Kontaktinformationen finden Sie auf der [Unternehmensportal-Website](https://go.microsoft.com/fwlink/?linkid=2010980).
