---
title: Installieren von Mobile Threat Defense auf Ihrem mobilen Gerät
description: Hier erfahren Sie, was Mobile Threat Defense-Apps sind und wie sie eingerichtet werden.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/20/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.custom: intune-enduser, contperfq1
ms.collection: ''
ms.openlocfilehash: 37b7006ef912d87276c11e09cb6db0c0f14059c4
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193911"
---
# <a name="install-mobile-threat-defense-app"></a>Installieren einer Mobile Threat Defense-App  

> [!TIP]
> Es gibt eine Vielzahl von Mobile Threat Defense-Apps (MTD) auf dem Markt. Ihre Organisation muss Ihnen mitteilen, welche zu verwenden ist. Wenn Sie aufgefordert werden, eine MTD-App zu installieren, und nicht direkt an eine Stelle weitergeleitet werden, von der aus Sie die App einrichten oder installieren können, wenden Sie sich an Ihren IT-Support, um Hilfe zu erhalten.  

Im Rahmen der Sicherheitsanforderungen Ihrer Organisation müssen Sie möglicherweise eine App eines MTD-Anbieters installieren. Diese Arten von Apps erkennen Bedrohungen auf Ihrem Gerät und warnen Sie vor diesen, z. B. verdächtige Apps, Netzwerke oder Betriebssystem-Sicherheitsrisiken.  

Wenn die erforderliche MTD-App nicht installiert ist, können Sie sich bei geschützten, verwalteten Apps (z. B. Microsoft Excel oder OneDrive) nicht mit Ihrem Geschäfts-, Schul- oder Unikonto anmelden. In diesem Artikel erfahren Sie, [wie Sie eine MTD-App einrichten](set-up-mobile-threat-defense.md#set-up-mtd-app), damit Sie wieder Zugriff erhalten.    

## <a name="mtd-apps-for-ios"></a>MTD-Apps für iOS
Die folgenden MTD-Apps werden häufig auf iOS-Geräten verwendet. Wählen Sie eine App aus, um das entsprechende Listing im App Store zu öffnen.   

* [Lookout for Work](https://go.microsoft.com/fwlink/?linkid=2139367)
* [Symantec Endpoint Protection (SEP) Mobile](https://go.microsoft.com/fwlink/?linkid=2139141)
* [Sandblast Mobile Protect](https://go.microsoft.com/fwlink/?linkid=2139231)
* [Zimperium zIPS](https://go.microsoft.com/fwlink/?linkid=2139232)


## <a name="mtd-apps-for-android"></a>MTD-Apps für Android 
Die folgenden MTD-Apps werden häufig auf Android-Geräten verwendet. Wählen Sie eine App aus, um das entsprechende Listing in Google Play zu öffnen.  

* [Lookout for Work](https://go.microsoft.com/fwlink/?linkid=2139453)
* [Symantec Endpoint Protection (SEP) Mobile](https://go.microsoft.com/fwlink/?linkid=2139454)
* [SandBlast Mobile Protect](https://go.microsoft.com/fwlink/?linkid=2139455)
* [Zimperium Mobile IPS (zIPS)](https://go.microsoft.com/fwlink/?linkid=2139142)  


## <a name="information-your-organization-can-see"></a>Von Ihrer Organisation einsehbare Informationen   

Ihre Organisation kann keine Daten wie SMS, E-Mails und Bilder in Ihren persönlichen Apps einsehen. Die MTD-App meldet allerdings Informationen über Ihre Apps, z. B. Name und Version, an Ihre Organisation. Die tatsächlich gemeldeten Informationen hängen davon ab, welchen MTD-Anbieter Ihr Unternehmen verwendet. Ihre Organisation sieht möglicherweise:   

* App-Name  
* App-ID: der eindeutige Name, der die App in Google Play identifiziert.  
* App-Version und kurze Versionsnummer: Die spezifischen Releasenummern für eine App.  
* App Bundle und dynamische Größe: Die Menge Speicherplatz, die eine App auf Ihrem Gerät verwendet 


## <a name="set-up-mtd-app"></a>Einrichten der MTD-App 
Wenn Sie sich bei einer geschützten App anmelden, werden Sie aufgefordert, eine MTD-App zu installieren. Führen Sie die auf dem Bildschirm angezeigten Schritte aus, um die Installation abzuschließen und Zugriff auf die geschützte App zu erhalten. 

Weitere Informationen finden Sie in den Anweisungen zu [iOS](set-up-mobile-threat-defense.md#ios-setup) und [Android](set-up-mobile-threat-defense.md#android-setup) in diesem Abschnitt. Diese Schritte sind ergänzend und sollen die auf dem Bildschirm angezeigten Anweisungen nicht ersetzen. 

Wenn Sie aufgefordert werden, eine MTD-App zu installieren, aber nicht sicher sind, welche Sie verwenden sollen, wenden Sie sich an Ihren IT-Support.  

### <a name="device-registration"></a>Geräteregistrierung  
Die Geräteregistrierung ist erforderlich, um Ihre Identität zu bestätigen und Ihr Schul-, Uni- oder Geschäftskonto mit Ihrem Gerät zu verbinden. Wenn Ihr Gerät nicht registriert ist, werden Sie vor dem Installieren der MTD-App automatisch durch die erforderlichen Schritte geführt.   

Weitere Informationen zur Geräteregistrierung finden Sie unter [Registrieren Ihres persönlichen Geräts im Netzwerk Ihrer Organisation](/azure/active-directory/user-help/user-help-register-device-on-network).  

### <a name="ios-setup"></a>iOS-Setup  
Diese Schritte beginnen auf dem Bildschirm **Zugriff erhalten**, der angezeigt wird, nachdem Sie sich bei einer geschützten App angemeldet haben.  

1. Folgen Sie auf der Seite **Zugriff anfordern** den Anweisungen zum Installieren der von Ihrer Organisation geforderten MTD-App.   
2. Kehren Sie zurück zur Seite **Zugriff anfordern**, und tippen Sie auf **Öffnen**.  
3. Die MTD-App fragt nach der Berechtigung zum Öffnen von Microsoft Authenticator. Wählen Sie **Öffnen** aus. 
4. Tippen Sie auf Ihr Geschäftskonto, um sich anzumelden. 
5. Warten Sie, während die MTD-App Ihr Gerät auf Sicherheitsbedrohungen überprüft. 
6. Kehren Sie zu der Schul-, Uni- oder Geschäfts-App zurück, auf die Sie ursprünglich zugreifen wollten. An diesem Punkt fordert Ihre Organisation Sie möglicherweise dazu auf, andere App-Sicherheitsanforderungen zu konfigurieren, z. B. dazu, eine PIN zu erstellen.   
7. Sie sollten nun auf die App zugreifen können. Gehen Sie wie folgt vor, wenn Sie noch immer blockiert sind:  
    * Tippen Sie auf der Seite **Zugriff anfordern** auf **Erneut prüfen**.  
    * Wechseln Sie zur MTD-App, und suchen Sie nach vorhandenen Bedrohungen. Führen Sie die empfohlenen Schritte aus, um die Bedrohung zu beheben und den Zugriff wiederherzustellen.    

### <a name="android-setup"></a>Android-Setup 
Diese Schritte beginnen auf dem Bildschirm **Zugriff erhalten**, der angezeigt wird, nachdem Sie sich bei einer geschützten App angemeldet haben.  

1. Folgen Sie auf der Seite **Zugriff anfordern** den Anweisungen zum Installieren der von Ihrer Organisation geforderten MTD-App.  
2. Kehren Sie zurück zur Seite **Zugriff anfordern**, und tippen Sie auf **Öffnen**.  
3. Die MTD-App bittet Sie um die Berechtigung, auf bestimmte Bereiche Ihres Geräts zuzugreifen, sofern dies erforderlich ist. Damit diese App richtig funktioniert, müssen Sie den Zugriff auf Kontakte **Zulassen**. Die angeforderten Berechtigungen unterscheiden sich bei den verschiedenen MTD-Anbietern.  
4. Tippen Sie auf Ihr Geschäftskonto, um sich anzumelden.  
5. Warten Sie, während die MTD-App Ihr Gerät auf Sicherheitsbedrohungen überprüft.  
6. Kehren Sie zu der Schul-, Uni- oder Geschäfts-App zurück, auf die Sie ursprünglich zugreifen wollten. An diesem Punkt fordert Ihre Organisation Sie möglicherweise dazu auf, andere App-Sicherheitsanforderungen zu konfigurieren, z. B. dazu, eine PIN zu erstellen.  
7. Sie sollten nun auf die App zugreifen können. Gehen Sie wie folgt vor, wenn Sie noch immer blockiert sind:  
    * Tippen Sie auf der Seite **Zugriff anfordern** auf **Erneut prüfen**.  
    * Wechseln Sie zur MTD-App, und suchen Sie nach vorhandenen Bedrohungen. Führen Sie die empfohlenen Schritte aus, um die Bedrohung zu beheben und den Zugriff wiederherzustellen.  


## <a name="resolving-a-threat"></a>Auflösen einer Bedrohung
Wenn eine Bedrohung erkannt wird und die von Ihrer Organisation definierte Bedrohungsstufe übersteigt, wurde von Ihrer Organisation eine der folgenden Maßnahmen festgelegt:  
   
* Zugriff blockieren: Verhindert, dass Sie die geschützten Apps Ihrer Organisation verwenden, während Sie bei Ihrem Geschäfts-, Schul- oder Unikonto angemeldet sind  
* Daten löschen: Löscht Ihre Arbeits-, Schul- oder Unidaten aus einer oder mehreren der geschützten Apps Ihrer Organisation  

So lösen Sie eine Bedrohung auf und erhalten wieder Zugriff auf geschützte Apps:  

1. Öffnen Sie die MTD-App auf Ihrem Gerät.     
2. Lesen Sie die Details zur Bedrohung in der App. In diesen wird erläutert, wie sich die Bedrohung auf Ihr Gerät auswirkt, falls sie nicht aufgelöst wird. Außerdem wird beschrieben, wie die Auflösung erfolgen kann. 
3. Nachdem Sie die erforderlichen Änderungen auf Ihrem Gerät vorgenommen haben, kehren Sie zur MTD-App zurück und starten eine neue Überprüfung. Wiederholen Sie die Schritte, bis alle Bedrohungen aufgelöst sind. Es kann einige Minuten dauern, bis Ihre Änderungen mit Ihrer Organisation synchronisiert sind. Sobald die Synchronisierung abgeschlossen ist, können Sie wieder auf die geschützte App zugreifen. 

## <a name="get-support"></a>Support
Besuchen Sie die [Unternehmensportal-Website](https://go.microsoft.com/fwlink/?linkid=2010980), um die Kontaktinformationen für Ihre Organisation zu erhalten. Wenden Sie sich an den Support, um Hilfe bei Folgendem zu erhalten:

* Ermitteln der zu verwendenden MTD-App  
* Installation  
* Installationsfehler  
* Erkennen und Auflösen einer Bedrohung  
* Deinstallieren einer MTD-App   
 

### <a name="share-app-logs-with-it-support"></a>Freigeben von App-Protokollen für den IT-Support  
Sie können auch Ihre App-Protokolle an Ihren IT-Support senden, um mehr Kontextinformationen zu Installationsfehlern zu liefern.  
* Android-Benutzer: Verwenden Sie das Unternehmensportal, um [Ihre Protokolle hochzuladen und per E-Mail zu versenden](./send-logs-to-your-it-admin-by-email-android.md).   

* Benutzer von iOS-Geräten: Verwenden Sie Microsoft Edge für iOS, um [Ihre Protokolle abzurufen und zu versenden](/intune/apps/manage-microsoft-edge#use-microsoft-edge-to-access-managed-app-logs).  


## <a name="next-steps"></a>Nächste Schritte  

In den folgenden Artikeln erfahren Sie, wie verwaltete Apps funktionieren, wie Sie solche Apps erhalten und wie Sie erkennen, dass Sie eine solche App verwenden.  

* [Verwenden verwalteter Apps auf Ihrem Android-Gerät](use-managed-apps-on-your-device-android.md)
* [Verwenden verwalteter Apps auf Ihrem iOS-Gerät](use-managed-apps-on-your-device-ios.md)  

Benötigen Sie weitere Unterstützung? Kontaktieren Sie den Support Ihres Unternehmens. Die entsprechenden Kontaktinformationen finden Sie auf der [Unternehmensportal-Website](https://go.microsoft.com/fwlink/?linkid=2010980).