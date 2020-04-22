---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/30/2018
ms.openlocfilehash: 1b4fb4fb087639d1b3c3075339ce890a9c1dbbca
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708218"
---
Verwenden Sie zur Unterscheidung zwischen Pilot- und Produktionsumgebungen die folgenden Definitionen:  

- **Pilot**: Hierbei handelt es sich um einen Teil Ihrer Geräte, die Sie überprüfen möchten, bevor Sie sie in größerem Umfang bereitstellen. Verwenden Sie Desktop Analytics, um Geräte für den Pilotversuch als eindeutig zu markieren. Geräte in der Pilotgruppe können aktualisiert werden, wenn keine Objekte blockiert werden. Ein blockierendes Objekt wird als *kritisch* markiert, und für dieses Objekt kann *kein* Upgrade durchgeführt werden.  

- **Produktion:** Hierbei handelt es sich um alle anderen bei Desktop Analytics registrierten Geräte, die sich nicht in der Pilotphase befinden. Produktionsgeräte können aktualisiert werden, wenn alle Objekte abgemeldet wurden. Desktop Analytics meldet automatisch alle nicht kritischen Objekte ab.  

