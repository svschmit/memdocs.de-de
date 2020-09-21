---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: 27436e7cd782ca910049007d52f37e2d7945f01e
ms.sourcegitcommit: e533cdf8722156a66b1cc46f710def96587345d0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/15/2020
ms.locfileid: "90606838"
---
- `https://aka.ms/configmgrgateway`

- `https://*.manage.microsoft.com` <!--7424742-->

- `https://dc.services.visualstudio.com` <!--7541816-->

Der Dienstverbindungspunkt stellt eine langfristige ausgehende Verbindung mit dem Benachrichtigungsdienst her, der auf `https://*.manage.microsoft.com` gehostet wird. Vergewissern Sie sich, dass das Timeout des für den Dienstverbindungspunkt verwendeten Proxys nicht zu früh auftritt. Für ausgehende Verbindungen dieses Internetendpunkts werden drei Minuten empfohlen. <!--7820969-->