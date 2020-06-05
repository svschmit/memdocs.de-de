---
title: Datei einfügen
description: Datei einfügen
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 06/02/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: bc8bb79d4f950edc303fb12504ef1a4a8dda9a64
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347249"
---
## <a name="apple-device-network-information"></a>Informationen zum Netzwerk von Apple-Geräten

|**Verwendung**|**Hostname (IP-Adresse/-Subnetz)**|**Protokoll**|**Port**|
|------------|-----------|------------|-----------|
|Abrufen und Anzeigen von Inhalten von Apple-Servern|itunes.apple.com<br>\*.itunes.apple.com<br>\*.mzstatic.com<br>\*.phobos.apple.com<br>\*.phobos.itunes-apple.com.akadns.net|HTTP|80|
|Kommunikation mit APNs-Servern|#-courier.push.apple.com<br># ist eine zufällige Zahl zwischen 0 und 50.|TCP|5223 und 443|
|Verschiedene Funktionen, z. B. Zugriff auf das Internet, den iTunes Store, den macOS App Store, iCloud, Messaging usw.|phobos.apple.com<br>ocsp.apple.com<br>ax.itunes.apple.com<br>ax.itunes.apple.com.edgesuite.net|HTTP/HTTPS|80 oder 443|

Weitere Informationen finden Sie in folgenden Quellen:

- [Von Apple-Softwareprodukten verwendete TCP- und UDP-Ports](https://support.apple.com/HT202944)
- [Informationen zu macOS-, iOS- und iTunes-Server-Hostverbindungen und iTunes-Hintergrundprozessen](https://support.apple.com/HT201999)
- [Wenn Ihre macOS- und iOS-Clients keine Apple Push-Benachrichtigungen empfangen](https://support.apple.com/HT203609)