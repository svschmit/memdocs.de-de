---
title: Datei einfügen
description: Datei einfügen
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 03/30/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: fbf352c3bccfb17efc35e34a2a822b6bbbcc215d
ms.sourcegitcommit: 53bab52e42de28b87e53596646a3532e25eb9c14
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/28/2020
ms.locfileid: "82183046"
---
Diese Hinweise enthalten wichtige Informationen, die Ihnen bei der Vorbereitung auf künftige Änderungen und Features im Zusammenhang mit Intune helfen können.

### <a name="microsoft-intune-support-for-windows-10-mobile-ending--3544938--"></a>Ende des Microsoft Intune-Supports für Windows 10 Mobile<!--3544938-->
Der grundlegende Microsoft-Support für Windows 10 Mobile endet im Dezember 2019. Wie in diesem Supporthinweis erwähnt, erlischt für Benutzer von Windows 10 Mobile der Anspruch auf neue Sicherheitsupdates, nicht sicherheitsrelevante Hotfixes, kostenlose Supportoptionen oder Onlineupdates für technische Inhalte von Microsoft. Auf Grundlage der umfassenden Mobile-Betriebssystemunterstützung stellt Microsoft Intune die Unterstützung sowohl für das Unternehmensportal für die Windows 10 Mobile-App als auch für das Windows 10 Mobile-Betriebssystem am 10. August 2020 ein.

#### <a name="how-does-this-affect-me"></a>Wie wirkt sich das auf mich aus?
Wenn Sie in Ihrer Organisation Windows 10 Mobile-Geräte im Einsatz haben, können Sie bis zum 10. August 2020 neue Geräte registrieren, Richtlinien und Apps hinzufügen oder entfernen oder beliebige Verwaltungseinstellungen aktualisieren. Nach dem 10. August sind keine neue Registrierungen mehr möglich, und die Windows 10 Mobile-Verwaltung wird schließlich aus der Intune-Benutzeroberfläche entfernt. Geräte werden nicht mehr in den Intune-Dienst eingecheckt, und Geräte- und Richtliniendaten werden gelöscht.  

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Was muss ich als Vorbereitung auf diese Veränderung tun?
Sie können Ihre Intune-Berichterstellung überprüfen, um zu sehen, welche Geräte oder Benutzer möglicherweise betroffen sind. Wechseln Sie zu **Geräte** > **Alle Geräte**, und filtern Sie nach „Betriebssystem“. Sie können weitere Spalten hinzufügen, um besser bestimmen zu können, welche Benutzer in Ihrer Organisation Geräte mit Windows 10 Mobile verwenden. Fordern Sie Ihre Endbenutzer auf, ihre Geräte zu aktualisieren oder die Geräte nicht mehr für den Unternehmenszugang zu verwenden.


### <a name="end-of-support-for-legacy-pc-management"></a>Ende der Unterstützung für die Legacy-PC-Verwaltung

Legacy-PC-Verwaltungsfunktionen werden ab 15. Oktober 2020 nicht mehr unterstützt. Führen Sie ein Upgrade der Geräte auf Windows 10 aus, und registrieren Sie die Geräte neu als Geräte der Verwaltung mobiler Geräte (MDM), um diese weiterhin in Intune zu verwalten.

[Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2107122)


### <a name="decreasing-support-for-android-device-administrator--5857738--"></a>Verringern der Unterstützung für den Android-Geräteadministrator<!--5857738-->
Der Android-Geräteadministrator (mit Android 2.2 veröffentlicht und manchmal auch als „Legacy“-Android-Verwaltung bezeichnet) ist eine Möglichkeit zum Verwalten von Android-Geräten. [Android Enterprise](../enrollment/connect-intune-android-enterprise.md) (veröffentlicht mit Android 5.0) bietet jetzt jedoch eine verbesserte Verwaltungsfunktionalität. In dem Bestreben, auf eine moderne, umfassendere und sicherere Geräteverwaltung umzusteigen, reduziert Google die Geräteadministratorunterstützung in neuen Android-Releases.

#### <a name="how-does-this-affect-me"></a>Wie wirkt sich das auf mich aus?
Die Änderungen von Google haben für Intune-Benutzer diese Folgen:  
- Intune bietet vollständige Unterstützung für Geräte, die vom Administrator verwaltet werden und auf denen Android 10 und höher bis zum zweiten Quartal CY2020 ausgeführt wird. Geräte, die vom Geräteadministrator verwaltet werden und nach Ablauf dieser Zeit Android 10 oder höher ausführen, können nicht vollständig verwaltet werden. Dies bedeutet, dass betroffene Geräte keine neuen Kennwortanforderungen erhalten.
    - Samsung Knox-Geräte werden in diesem Zeitraum nicht betroffen sein, da Intune durch die Integration mit der Knox-Plattform erweiterte Unterstützung bietet. Dies gibt Ihnen mehr Zeit für die Planung des Übergangs von der Geräteadministratorverwaltung.    
- Vom Geräteadministrator verwaltete Android-Geräte, auf denen Android-Versionen unter 10 ausgeführt werden, sind nicht betroffen und können weiterhin vollständig mit dem Geräteadministrator verwaltet werden.    
- Für alle Geräte unter Android 10 und höher hat Google für Geräteadministratorverwaltung-Agents – wie z. B. das Unternehmensportal – die Möglichkeit beschränkt, auf Gerätebezeichnerinformationen zuzugreifen. Diese Einschränkung wirkt sich nach Geräteupdates auf Android 10 oder höher auf die folgenden Intune-Features wie folgt aus:  
    - Die Netzwerkzugriffssteuerung für VPN funktioniert nicht mehr.   
    - Die Identifizierung von Geräten mit IMEI oder Seriennummer als unternehmenseigen kennzeichnet Geräte nicht automatisch als unternehmenseigen.  
    - IMEI und Seriennummer sind für IT-Administratoren in Intune nicht mehr sichtbar. 
        > [!NOTE]
        > Dies betrifft nur vom Geräteadministrator verwaltete Geräte unter Android 10 und höher, nicht jedoch Geräte, die im Rahmen von Android Enterprise verwaltet werden. 

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Was muss ich als Vorbereitung auf diese Veränderung tun?
Wir empfehlen Folgendes, um die im dritten Quartal CY2020 auftretende Einschränkung der Funktionalität zu vermeiden:
- Binden Sie neue Geräte nicht in die Geräteadministratorverwaltung ein.
- Wenn zu erwarten ist, dass ein Gerät ein Update auf Android 10 erhalten wird, migrieren Sie es von der Geräteadministratorverwaltung zur Android Enterprise-Verwaltung und/oder zu App-Schutzrichtlinien.

#### <a name="additional-information"></a>Zusätzliche Informationen
- [Google-Leitfaden für die Migration vom Geräteadministrator zu Android Enterprise](http://static.googleusercontent.com/media/android.com/en/enterprise/static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf)
- [Google-Dokumentation zum Plan, die Geräteadministrator-API als veraltet zu kennzeichnen](https://developers.google.com/android/work/device-admin-deprecation)