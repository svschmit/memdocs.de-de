---
title: Aktivieren von oder Transport Layer Security 1.2 (TLS) auf Clients
titleSuffix: Configuration Manager
description: Informationen zum Aktivieren von TLS 1.2 für Configuration Manager-Clients
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5b094a02-a425-4b67-81d3-8455e4265512
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e5b525da4a58240b34c30403db618ea0d2ca85f1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704108"
---
# <a name="how-to-enable-tls-12-on-clients"></a>Aktivieren von TLS 1.2 auf Clients

*Gilt für: Configuration Manager (Current Branch)*

Wenn Sie TLS 1.2 für Ihre Configuration Manager-Umgebung aktivieren, stellen Sie zunächst sicher, dass die Clients TLS 1.2 verwenden können und dafür ordnungsgemäß konfiguriert sind, bevor Sie TLS 1.2 aktivieren und ältere Protokolle auf den Standortservern und Remotestandortsystemen deaktivieren. Für die Aktivierung von TLS 1.2 auf Clients sind drei Schritte durchzuführen:

- Aktualisieren von Windows und WinHTTP
- Sicherstellen, dass TLS 1.2 als Protokoll für SChannel auf Betriebssystemebene aktiviert ist
- Aktualisieren und Konfigurieren von .NET Framework zur Unterstützung von TLS 1.2.

Weitere Informationen zu den Abhängigkeiten für bestimmte Configuration Manager-Features und -Szenarios finden Sie unter [Informationen zum Aktivieren von TLS 1.2](enable-tls-1-2.md).

## <a name="update-windows-and-winhttp"></a><a name="bkmk_winhttp"></a> Aktualisieren von Windows und WinHTTP

Windows 8.1, Windows Server 2012 R2, Windows 10, Windows Server 2016 und neuere Versionen von Windows bieten systemeigene Unterstützung für TLS 1.2 für die Client-Server-Kommunikation über WinHTTP. 

Unter früheren Windows-Versionen wie Windows 7 oder Windows Server 2012 werden TLS 1.1 und TLS 1.2 nicht standardmäßig für die sichere Kommunikation über WinHTTP aktiviert. Installieren Sie für frühere Windows-Versionen [Update 3140245](https://support.microsoft.com/help/3140245), um den unten dargestellten Registrierungswert zu aktivieren, der so festgelegt werden kann, um TLS 1.1 und TLS 1.2 zur Standardliste der sicheren Protokolle für WinHTTP hinzuzufügen. Erstellen Sie mit installiertem Patch die folgenden Registrierungswerte:

> [!IMPORTANT]
> Aktivieren Sie diese Einstellungen auf allen Clients, die auf früheren Versionen von Windows ausgeführt werden, *bevor* Sie TLS 1.2 aktivieren und die älteren Protokolle auf den Configuration Manager-Servern deaktivieren. Andernfalls können Sie diese versehentlich verwaisen.

Überprüfen Sie den Wert der Registrierungseinstellung `DefaultSecureProtocols`. Nachfolgend sehen Sie ein Beispiel:

``` Registry
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
```

Wenn Sie diesen Wert ändern, starten Sie den Computer neu.

Das obige Beispiel zeigt den Wert `0xAA0` für die Einstellung `DefaultSecureProtocols` von WinHTTP. Unter [KB 3140245: Update zum Aktivieren von TLS 1.1 und TLS 1.2 als standardmäßige Sicherheitsprotokolle in WinHTTP unter Windows](https://support.microsoft.com/help/3140245) ist der hexadezimale Wert für jedes Protokoll aufgelistet. Dieser Wert ist unter Windows standardmäßig auf `0x0A0` gesetzt, um SSL 3.0 und TLS 1.0 für WinHTTP zu aktivieren. Im obigen Beispiel werden diese Standardeinstellungen beibehalten und außerdem TLS 1.1 und TLS 1.2 für WinHTTP aktiviert. Mit dieser Konfiguration wird sichergestellt, dass durch die Änderung keine andere Anwendung unterbrochen wird, die möglicherweise immer noch auf SSL 3.0 oder TLS 1.0 basiert. Sie können den Wert `0xA00` verwenden, um nur TLS 1.1 und TLS 1.2 zu aktivieren. Configuration Manager unterstützt das sicherste Protokoll, das Windows zwischen beiden Geräten aushandelt.

 Wenn Sie SSL 3.0 und TLS 1.0 vollständig deaktivieren möchten, verwenden Sie die SChannel-Einstellung für deaktivierte Protokolle unter Windows. Weitere Informationen finden Sie unter [Beschränken der Verwendung bestimmter kryptografischer Algorithmen und Protokolle in „Schannel.dll“](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc).

## <a name="ensure-that-tls-12-is-enabled-as-a-protocol-for-schannel-at-the-operating-system-level"></a><a name="bkmk_protocol"></a> Sicherstellen, dass TLS 1.2 als Protokoll für SChannel auf Betriebssystemebene aktiviert ist

[!INCLUDE [Enable TLS 1.2 protocol as a security provider](includes/enable-tls-1-2-protocol-security-provider.md)]

## <a name="update-and-configure-the-net-framework-to-support-tls-12"></a><a name="bkmk_net"></a> Aktualisieren und Konfigurieren von .NET Framework zur Unterstützung von TLS 1.2.

[!INCLUDE [Update and configure the .NET framework to support TLS 1.2](includes/update-net-framework-to-support-tls-1-2.md)]


## <a name="next-steps"></a>Nächste Schritte

- [Aktivieren von TLS 1.2 auf Standortservern und Remotestandortsystemen](enable-tls-1-2-server.md)
- [Häufige Probleme beim Aktivieren von TLS 1.2](enable-tls-1-2-troubleshoot.md)

