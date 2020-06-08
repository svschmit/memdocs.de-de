---
title: Auf welche Informationen kann Ihr Unternehmen zugreifen, wenn Sie Ihr Gerät registrieren?
description: Erläutert, auf was die IT-Abteilung zugreifen kann und auf was nicht.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/31/2019
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 12655728-a1af-4d89-97bc-925fe36c0dc4
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.collection: ''
ms.openlocfilehash: 028a568b9a588697139f97f292c70c50347217f3
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83882079"
---
# <a name="what-information-can-my-organization-see-when-i-enroll-my-device"></a>Welche Informationen erhält meine Organisation, wenn ich mein Gerät registriere?

Ihre Organisation kann Ihre privaten Informationen nicht einsehen, wenn Sie ein Gerät für Microsoft Intune registrieren. Wenn Sie ein Gerät registrieren, erhält Ihre Organisation die Berechtigung zum Anzeigen bestimmter Arten von Informationen auf Ihrem Gerät, z.B. das Gerätemodell und die Seriennummer. Ihre Organisation verwendet diese Informationen, um die Unternehmensdaten auf dem Gerät zu schützen.

**Folgendes kann nicht von Ihrer Organisation eingesehen werden:**

- Ihren Anrufs- und Browserverlauf
- E-Mail-Nachrichten und SMS
- Kontakte
- Kalender
- Kennwörter
- Ihre Bilder, einschließlich dem, was sich in der Fotos- und Kamera-App befindet
- Dateien

**Folgendes kann von Ihrer Organisation eingesehen werden:**

- Gerätemodell, z.B. Google Pixel
- Gerätehersteller, z.B. Microsoft
- Betriebssystem und Version, z.B. iOS 12.0.1
- App-Bestand und App-Namen, z.B. „Microsoft Word“. Auf persönlichen Geräten kann Ihre Organisation nur sehen, welche verwalteten Apps installiert sind. Auf unternehmenseigenen Geräten kann Ihre Organisation alle installierten Apps sehen.
- Geräteeigentümer
- Gerätename
- Seriennummer des Geräts
- IMEI

 > [!NOTE]
 > Für vollständig verwaltete und dedizierte Android Enterprise-Geräte kann nicht der gesamte App-Bestand angezeigt werden.
 
 > [!NOTE]
 > Eine App wird als **verwaltete App** betrachtet, wenn sie auf eine der folgenden Arten installiert wird:
 > 1. Ein Benutzer installiert sie aus der Unternehmensportal-App, nachdem sie von einem Intune-Administrator als **verfügbar** veröffentlicht wurde.
 > 2. Die App wird als **erforderlich** von einem Intune-Administrator veröffentlicht und auf dem Gerät installiert. 
 >
 > Wenn Sie ein IT-Administrator oder Supportmitarbeiter in Ihrer Organisation sind, finden Sie weitere Informationen zur App-Verwaltung in Intune unter [Grundlegendes zu den Funktionen von nicht verwalteten Apps, verwalteten Apps und MAM-Apps](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/understanding-the-capabilities-of-unmanaged-apps-managed-apps/ba-p/249164).
    
**Was Ihre Organisation möglicherweise außerdem sehen kann:**

- Telefonnummer: Bei unternehmenseigenen Geräten ist Ihre vollständige Telefonnummer zu sehen. Bei Geräten, die persönliches Eigentum sind, werden der Organisation nur die letzten vier Ziffern Ihrer Telefonnummer angezeigt. Sie können den Besitztyp für jedes einzelne Gerät auf der jeweiligen **Gerätedetails**-Seite einsehen.
- Speicherplatz auf dem Gerät: Wenn Sie eine erforderliche App nicht installieren können, prüft Ihre Organisation möglicherweise den freien Speicherplatz auf Ihrem Gerät, um festzustellen, ob der Speicherplatz nicht ausreicht.  
- Speicherort: Ihre Organisation kann den Standort Ihres Geräts niemals anzeigen, es sei denn, Sie müssen ein überwachtes iOS-Gerät auffinden, das verloren gegangen ist. In der [Dokumentation zu Apple iOS](https://go.microsoft.com/fwlink/?linkid=853816) erhalten Sie weitere Informationen zu überwachten Geräten.  
- App-Bestandsdetails: Wenn Ihr Unternehmen Mobile Threat Defense verwendet, können weitere Informationen zu den Apps auf Ihrem iOS-Gerät eingesehen werden. Erfahren Sie mehr über [Mobile Threat Defense](set-up-mobile-threat-defense.md). Auf Ihrem persönlichen Gerät kann Ihre Organisation nur sehen, welche verwalteten Apps installiert sind. Auf Ihrem unternehmenseigenen Gerät kann Ihre Organisation alle installierten Apps sehen.
- Netzwerkinformationen: Möglicherweise sind einige Informationen über Netzwerkverbindungen für Android-Geräte für den Support Ihrer Organisation verfügbar. Wenn Ihre Organisation beispielsweise verlangt, dass Geräte in einem bestimmten Gebäude bleiben, identifiziert Ihr Gerät das Netzwerk, mit dem es verbunden ist. 
