---
title: Installieren von Mobile Threat Defense auf Ihrem mobilen Gerät
description: Erfahren Sie, wie Sie Mobile Threat Defense auf Ihrem mobilen Gerät installieren.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/25/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: b5df63a14f27b657c585eb43e09b02368d969939
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/21/2020
ms.locfileid: "80084402"
---
# <a name="install-mobile-threat-defense"></a>Installieren von Mobile Threat Defense   

Möglicherweise müssen Sie aufgrund der Sicherheitsanforderungen Ihrer Organisation eine App eines MTD-Anbieters (Mobile Threat Defense) installieren. Diese Arten von Apps erkennen Bedrohungen auf Ihrem Gerät und warnen Sie vor diesen, z. B. verdächtige Apps, Netzwerke oder Betriebssystem-Sicherheitsrisiken.  

Wenn die erforderliche MTD-App nicht installiert ist, können Sie sich bei geschützten Apps mit Ihrem Geschäfts-, Schul- oder Unikonto nicht anmelden. In diesem Artikel lernen Sie, [wie Sie eine MTD-App installieren](set-up-mobile-threat-defense.md#install-app), damit die Blockierung aufgehoben wird.  

Es gibt zahlreiche Apps von MTD-Anbietern, die installiert werden können. Ihre Organisation wird Ihnen mitteilen, welche Sie verwenden sollen. 


## <a name="information-your-organization-can-see"></a>Von Ihrer Organisation einsehbare Informationen   

Ihre Organisation kann keine Daten wie SMS, E-Mails und Bilder in Ihren persönlichen Apps einsehen. Die MTD-App meldet allerdings Informationen über Ihre Apps, z. B. Name und Version, an Ihre Organisation. Die tatsächlich gemeldeten Informationen hängen davon ab, welchen MTD-Anbieter Ihr Unternehmen verwendet. Ihre Organisation sieht möglicherweise:   

* App-Name  
* App-ID: der eindeutige Name, der die App in Google Play identifiziert.  
* App-Version und kurze Versionsnummer: Die spezifischen Releasenummern für eine App.  
* App Bundle und dynamische Größe: Die Menge Speicherplatz, die eine App auf Ihrem Gerät verwendet 


## <a name="install-app"></a>Installieren der App    
Wenn Sie sich bei einer geschützten App anmelden, werden Sie automatisch dazu aufgefordert, eine MTD-App zu installieren. Führen Sie die auf dem Display angezeigten Schritte aus, um die Installation durchzuführen. Verwenden Sie die Schritte in diesem Abschnitt als zusätzliche Hilfestellung.  
 
Sie werden möglicherweise auch dazu aufgefordert, Ihr Gerät zu registrieren. Eine Registrierung ist erforderlich, um Ihre Identität zu bestätigen und Ihr Schul-, Uni- oder Geschäftskonto mit Ihrem Gerät zu verbinden. Wenn Sie nicht registriert sind, werden Sie vor dem Installieren der MTD-App automatisch durch das entsprechende Setup geführt. Wenn Sie auf der Seite **Zugriff anfordern** angekommen sind, können Sie mit den Installationsschritten beginnen.  

Weitere Informationen zur Geräteregistrierung finden Sie unter [Registrieren Ihres persönlichen Geräts im Netzwerk Ihrer Organisation](https://docs.microsoft.com/azure/active-directory/user-help/user-help-register-device-on-network).  

### <a name="ios-setup"></a>iOS-Setup  

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

1. Folgen Sie auf der Seite **Zugriff anfordern** den Anweisungen zum Installieren der von Ihrer Organisation geforderten MTD-App.  
2. Kehren Sie zurück zur Seite **Zugriff anfordern**, und tippen Sie auf **Öffnen**.  
3. Die MTD-App bittet Sie um die Berechtigung, auf bestimmte Bereiche Ihres Geräts zuzugreifen, sofern dies erforderlich ist. Damit diese App richtig funktioniert, müssen Sie den Zugriff auf Kontakte **Zulassen**. Die angeforderten Berechtigungen unterscheiden sich bei den verschiedenen MTD-Anbietern.  
4. Tippen Sie auf Ihr Geschäftskonto, um sich anzumelden.  
5. Warten Sie, während die MTD-App Ihr Gerät auf Sicherheitsbedrohungen überprüft.  
6. Kehren Sie zu der Schul-, Uni- oder Geschäfts-App zurück, auf die Sie ursprünglich zugreifen wollten. An diesem Punkt fordert Ihre Organisation Sie möglicherweise dazu auf, andere App-Sicherheitsanforderungen zu konfigurieren, z. B. dazu, eine PIN zu erstellen.  
7. Sie sollten nun auf die App zugreifen können. Gehen Sie wie folgt vor, wenn Sie noch immer blockiert sind:  
    * Tippen Sie auf der Seite **Zugriff anfordern** auf **Erneut prüfen**.  
    * Wechseln Sie zur MTD-App, und suchen Sie nach vorhandenen Bedrohungen. Führen Sie die empfohlenen Schritte aus, um die Bedrohung zu beheben und den Zugriff wiederherzustellen.  

### <a name="installation-failed"></a>Fehler bei der Installation.  

Wenden Sie sich an Ihren IT-Support, wenn bei der Installation ein Fehler auftritt. Besuchen Sie die [Unternehmensportal-Website](https://go.microsoft.com/fwlink/?linkid=2010980), um die Kontaktinformationen für Ihre Organisation zu erhalten.  

Sie können auch Ihre App-Protokolle an Ihren IT-Support senden, um mehr Kontextinformationen zur Installation bereitzustellen.  
* Android-Benutzer: Verwenden Sie das Unternehmensportal, um [Ihre Protokolle hochzuladen und per E-Mail zu versenden](https://docs.microsoft.com/mem/intune/user-help/send-logs-to-your-it-admin-by-email-android).   

* Benutzer von iOS-Geräten: Verwenden Sie Microsoft Edge für iOS, um [Ihre Protokolle abzurufen und zu versenden](https://docs.microsoft.com/intune/apps/manage-microsoft-edge#use-microsoft-edge-to-access-managed-app-logs).  

## <a name="resolve-a-threat"></a>Beheben einer Bedrohung  
Wenn eine Bedrohung die von Ihrer Organisation definierte Bedrohungsstufe übersteigt, ergreift Ihre Organisation eine der folgenden Maßnahmen:  
   
* Zugriff blockieren: Verhindert, dass Sie die geschützten Apps Ihrer Organisation verwenden, während Sie bei Ihrem Geschäfts-, Schul- oder Unikonto angemeldet sind  
* Daten löschen: Löscht Ihre Arbeits-, Schul- oder Unidaten aus einer oder mehreren der geschützten Apps Ihrer Organisation  

Öffnen Sie die MTD-App auf Ihrem Gerät, um eine Bedrohung zu beheben und den Zugriff wiederherzustellen. Lesen Sie sich die bereitgestellten Informationen durch, um zu erfahren, welche Auswirkungen die Bedrohung auf Ihr Gerät haben kann und wie Sie sie beheben. Wenn Sie die Schritte zum Beheben der Bedrohung ausgeführt haben, wechseln Sie zurück zur MTD-App, und starten Sie eine neue Überprüfung. Es kann ein paar Minuten dauern, bis der Zugriff auf Ihre Organisation wiederhergestellt ist.  

## <a name="next-steps"></a>Nächste Schritte  

Benötigen Sie weitere Unterstützung? Kontaktieren Sie den Support Ihres Unternehmens. Die entsprechenden Kontaktinformationen finden Sie auf der [Unternehmensportal-Website](https://go.microsoft.com/fwlink/?linkid=2010980).

