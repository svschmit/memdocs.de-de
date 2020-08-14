---
title: Problembehandlung für BitLocker
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Probleme mit der BitLocker-Verwaltung in Configuration Manager beheben.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: troubleshooting
ms.assetid: 134c5b50-edeb-4d60-aaca-944d26deb9ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0158738f77a0070835bec2385dd85c42dfd763fd
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127813"
---
# <a name="troubleshoot-bitlocker"></a>Problembehandlung für BitLocker

*Gilt für: Configuration Manager (Current Branch)*

Verwenden Sie die Informationen in diesem Artikel, um Probleme mit der BitLocker-Verwaltung in Configuration Manager zu beheben.

## <a name="server-error-in-self-service"></a>Serverfehler beim Self-Service

Wenn Sie versuchen, das Self-Service-Portal (`https://webserver.contoso.com/SelfService`) zum ersten Mal zu öffnen, wird die folgende Fehlermeldung angezeigt:

``` error
Configuration Error - Server Error in '/SelfService' Application

Description: An error occurred during the processing of a configuration file required to service this request. Please review the specific error details below and modify your configuration file appropriately.

Parser Error Message: Could not load file or assembly 'System.Web.Mvc, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' or one of its dependencies. The system cannot find the file specified.
```

Um dieses Problem zu beheben, stellen Sie sicher, dass Sie die [Voraussetzung](../../plan-design/bitlocker-management.md#prerequisites) für **Microsoft ASP.NET MVC 4.0** auf dem Webserver installiert haben.

## <a name="see-also"></a>Weitere Informationen

Weitere Informationen zur Verwendung von BitLocker-Ereignisprotokollen finden Sie unter [BitLocker-Ereignisprotokolle](about-event-logs.md).

Eine Liste der bekannten Fehler und möglichen Ursachen für Ereignisprotokolleinträge finden Sie in den folgenden Artikeln:

- [Clientereignisprotokolle](client-event-logs.md)
- [Serverereignisprotokolle](server-event-logs.md)

Weitere Informationen dazu, warum Clients nicht mit der BitLocker-Verwaltungsrichtlinie konform sind, finden Sie unter [Codes für Nichtkonformität](non-compliance-codes.md).
