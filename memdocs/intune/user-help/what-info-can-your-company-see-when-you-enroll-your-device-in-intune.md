---
title: Auf welche Informationen kann Ihr Unternehmen zugreifen, wenn Sie Ihr Gerät registrieren?
description: Erläutert, auf was die IT-Abteilung zugreifen kann und auf was nicht.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/31/2019
ms.topic: article
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
ms.openlocfilehash: ed3f9f6f01c8dc2df3a89daee991d9f8c61056b9
ms.sourcegitcommit: f94cdca69981627d6a3471b04ac6f0f5ee8f554f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/28/2020
ms.locfileid: "82210314"
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
    
**Was Ihre Organisation möglicherweise außerdem sehen kann:**

- Telefonnummer: Bei unternehmenseigenen Geräten ist Ihre vollständige Telefonnummer zu sehen. Bei Geräten, die persönliches Eigentum sind, werden der Organisation nur die letzten vier Ziffern Ihrer Telefonnummer angezeigt. Sie können den Besitztyp für jedes einzelne Gerät auf der jeweiligen **Gerätedetails**-Seite einsehen.
- Speicherplatz auf dem Gerät: Wenn Sie eine erforderliche App nicht installieren können, prüft Ihre Organisation möglicherweise den freien Speicherplatz auf Ihrem Gerät, um festzustellen, ob der Speicherplatz nicht ausreicht.  
- Speicherort: Ihre Organisation kann den Standort Ihres Geräts niemals anzeigen, es sei denn, Sie müssen ein überwachtes iOS-Gerät auffinden, das verloren gegangen ist. In der [Dokumentation zu Apple iOS](https://go.microsoft.com/fwlink/?linkid=853816) erhalten Sie weitere Informationen zu überwachten Geräten.  
- App-Bestandsdetails: Wenn Ihr Unternehmen Mobile Threat Defense verwendet, können weitere Informationen zu den Apps auf Ihrem iOS-Gerät eingesehen werden. Erfahren Sie mehr über [Mobile Threat Defense](set-up-mobile-threat-defense.md). Auf Ihrem persönlichen Gerät kann Ihre Organisation nur sehen, welche verwalteten Apps installiert sind. Auf Ihrem unternehmenseigenen Gerät kann Ihre Organisation alle installierten Apps sehen.
- Netzwerkinformationen: Möglicherweise sind einige Informationen über Netzwerkverbindungen für Android-Geräte für den Support Ihrer Organisation verfügbar. Wenn Ihre Organisation beispielsweise verlangt, dass Geräte in einem bestimmten Gebäude bleiben, identifiziert Ihr Gerät das Netzwerk, mit dem es verbunden ist. 
