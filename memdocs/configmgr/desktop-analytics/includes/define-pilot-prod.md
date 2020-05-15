---
author: aczechowski
ms.author: aaroncz
ms.reviewer: acabello
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/30/2018
ms.openlocfilehash: 431c88b07889f7c80d2723425aaef2245c7f06bc
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268781"
---
Verwenden Sie zur Unterscheidung zwischen Pilot- und Produktionsumgebungen die folgenden Definitionen:  

- **Pilot**: Hierbei handelt es sich um einen Teil Ihrer Geräte, die Sie überprüfen möchten, bevor Sie sie in größerem Umfang bereitstellen. Verwenden Sie Desktop Analytics, um Geräte für den Pilotversuch als eindeutig zu markieren. Geräte in der Pilotgruppe können aktualisiert werden, wenn keine Objekte blockiert werden. Ein blockierendes Objekt wird als *kritisch* markiert, und für dieses Objekt kann *kein* Upgrade durchgeführt werden.  

- **Produktion:** Hierbei handelt es sich um alle anderen bei Desktop Analytics registrierten Geräte, die sich nicht in der Pilotphase befinden. Produktionsgeräte können aktualisiert werden, wenn alle Objekte abgemeldet wurden. Desktop Analytics meldet automatisch alle nicht kritischen Objekte ab.  
