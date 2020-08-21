---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.openlocfilehash: 0f91860ad591e20c6f199e098a8c957f50294386
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88704255"
---
<!-- ## Update and configure the .NET Framework to support TLS 1.2 Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

### <a name="determine-net-version"></a>Ermitteln der .NET-Version

Bestimmen Sie zuerst die installierten .NET-Versionen. Weitere Informationen finden Sie unter [Ermitteln der installierten Versionen und Service Pack-Stufen von Microsoft .NET Framework](https://support.microsoft.com/help/318785/how-to-determine-which-versions-and-service-pack-levels-of-the-microso).

### <a name="install-net-updates"></a>Installieren von .NET-Updates

Installieren Sie die .NET-Updates, damit Sie die starke Kryptografie aktivieren können. Für einige Versionen von .NET Framework sind möglicherweise Updates notwendig, um die starke Kryptografie zu aktivieren. Orientieren Sie sich an diesen Richtlinien:

- .NET Framework 4.6.2 und höher unterstützen TLS 1.1 and TLS 1.2. Überprüfen Sie die Registrierungseinstellungen, es sind jedoch keine zusätzlichen Änderungen erforderlich.

- Aktualisieren Sie .NET Framework 4.6 und frühere Versionen, damit TLS 1.1 und TLS 1.2 unterstützt werden. Weitere Informationen finden Sie unter [.NET Framework-Versionen und -Abhängigkeiten](/dotnet/framework/migration-guide/versions-and-dependencies).

- Wenn Sie .NET Framework 4.5.1 oder 4.5.2 unter Windows 8.1 oder Windows Server 2012 nutzen, finden Sie die relevanten Updates und Informationen auch im [Download Center](https://www.microsoft.com/download/details.aspx?id=42883).


### <a name="configure-for-strong-cryptography"></a>Konfigurieren für starke Kryptografie

Konfigurieren Sie .NET Framework so, dass starke Kryptografie unterstützt wird. Legen Sie die Registrierungseinstellung `SchUseStrongCrypto` auf `DWORD:00000001` fest. Durch diesen Wert wird die RC4-Streamverschlüsselung deaktiviert, und ein Neustart ist erforderlich. Weitere Informationen zu dieser Einstellung finden Sie unter [Microsoft Security Advisory 296038 (Microsoft-Sicherheitsempfehlung 296038)](/security-updates/SecurityAdvisories/2015/2960358).

Stellen Sie sicher, dass Sie die folgenden Registrierungsschlüssel auf allen Computern festlegen, die über das Netzwerk mit einem TLS 1.2-fähigen System kommunizieren. Dies sind beispielsweise Configuration Manager-Clients, Systemrollen des Remotestandorts, die nicht auf dem Standortserver installiert sind, und der Standortserver selbst.

Aktualisieren Sie für 32-Bit-Anwendungen, die auf 32-Bit-Betriebssystemen ausgeführt werden, und für 64-Bit-Anwendungen, die auf 64-Bit-Betriebssystemen ausgeführt werden, folgende Unterschlüsselwerte:

``` Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

Aktualisieren Sie für 32-Bit-Anwendungen, die auf 64-Bit-Betriebssystemen ausgeführt werden, folgende Unterschlüsselwerte:

``` Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

> [!Note]  
> Die Einstellung `SchUseStrongCrypto` ermöglicht .NET die Verwendung von TLS 1.1 und TLS 1.2. Die Einstellung `SystemDefaultTlsVersions` ermöglicht .NET die Verwendung der Betriebssystemkonfiguration. Weitere Informationen finden Sie unter [Bewährte Methoden für TLS mit .NET Framework](/dotnet/framework/network-programming/tls).