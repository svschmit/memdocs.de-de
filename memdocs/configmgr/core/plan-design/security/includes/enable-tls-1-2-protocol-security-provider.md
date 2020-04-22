---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.openlocfilehash: 08cebf6ef844e1854daa9444462f4c4470319186
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704078"
---
<!--## Enable Transport layer security (TLS) 1.2 protocol as a security provider Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

TLS 1.2 ist standardmäßig aktiviert. Deshalb müssen Sie an diesen Schlüsseln keine Änderungen vornehmen, um das Protokoll zu aktivieren. Sie können unter `Protocols` Änderungen vornehmen, um TLS 1.0 und TLS 1.1 zu deaktivieren, nachdem Sie alle Anweisungen in diesen Artikeln befolgt und überprüft haben, ob die Umgebung funktioniert, wenn nur TLS 1.2 aktiviert ist.

Überprüfen Sie die Einstellung des Registrierungsunterschlüssels `\SecurityProviders\SCHANNEL\Protocols`. Dieser Vorgang wird unter [Bewährte Methoden für Transport Layer Security (TLS) mit .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry) erläutert.

