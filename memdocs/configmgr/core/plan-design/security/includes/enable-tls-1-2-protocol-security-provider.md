---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.openlocfilehash: f14713431c71c1f3625d13ea4be1d919b072e273
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88704433"
---
<!--## Enable Transport layer security (TLS) 1.2 protocol as a security provider Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

TLS 1.2 ist standardmäßig aktiviert. Deshalb müssen Sie an diesen Schlüsseln keine Änderungen vornehmen, um das Protokoll zu aktivieren. Sie können unter `Protocols` Änderungen vornehmen, um TLS 1.0 und TLS 1.1 zu deaktivieren, nachdem Sie alle Anweisungen in diesen Artikeln befolgt und überprüft haben, ob die Umgebung funktioniert, wenn nur TLS 1.2 aktiviert ist.

Überprüfen Sie die Einstellung des Registrierungsunterschlüssels `\SecurityProviders\SCHANNEL\Protocols`. Dieser Vorgang wird unter [Bewährte Methoden für Transport Layer Security (TLS) mit .NET Framework](/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry) erläutert.