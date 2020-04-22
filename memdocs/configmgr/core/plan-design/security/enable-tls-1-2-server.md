---
title: Aktivieren von Transport Layer Security 1.2 (TLS) auf Standortservern und Remotestandortsystemen
titleSuffix: Configuration Manager
description: Informationen zum Aktivieren von TLS 1.2 für Configuration Manager-Standortserver
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0ce9b428-cb0f-46f3-bf69-c465e6623d6f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 15377520b76b9b3a3813e6ad4253548f29e011db
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704098"
---
# <a name="how-to-enable-tls-12-on-the-site-servers-and-remote-site-systems"></a>Aktivieren von TLS 1.2 auf Standortservern und Remotestandortsystemen

*Gilt für: Configuration Manager (Current Branch)*

Wenn Sie TLS 1.2 für Ihre Configuration Manager-Umgebung aktivieren, beginnen Sie mit dem [Aktivieren von TLS 1.2 für die Clients](enable-tls-1-2-client.md). Aktivieren Sie anschließend TLS 1.2 auf Standortservern und Remotestandortsystemen. Testen Sie schließlich die Kommunikation zwischen Clients und dem Standortsystem, bevor Sie möglicherweise die älteren Protokolle auf der Serverseite deaktivieren. Die folgenden Aufgabe sind für die Aktivierung von TLS 1.2 auf Standortservern und Remotestandortsystemen erforderlich:

- Sicherstellen, dass TLS 1.2 als Protokoll für SChannel auf Betriebssystemebene aktiviert ist
- Aktualisieren und Konfigurieren von .NET Framework zur Unterstützung von TLS 1.2.
- Aktualisieren von SQL Server und Clientkomponenten
- Aktualisieren von Windows Server Update Services (WSUS)

Weitere Informationen zu den Abhängigkeiten für bestimmte Configuration Manager-Features und -Szenarios finden Sie unter [Informationen zum Aktivieren von TLS 1.2](enable-tls-1-2.md). 

## <a name="ensure-that-tls-12-is-enabled-as-a-protocol-for-schannel-at-the-operating-system-level"></a><a name="bkmk_protocol"></a> Sicherstellen, dass TLS 1.2 als Protokoll für SChannel auf Betriebssystemebene aktiviert ist

[!INCLUDE [Enable TLS 1.2 protocol as a security provider](includes/enable-tls-1-2-protocol-security-provider.md)]

## <a name="update-and-configure-the-net-framework-to-support-tls-12"></a><a name="bkmk_net"></a> Aktualisieren und Konfigurieren von .NET Framework zur Unterstützung von TLS 1.2.

[!INCLUDE [Update and configure the .NET framework to support TLS 1.2](includes/update-net-framework-to-support-tls-1-2.md)]


## <a name="update-sql-server-and-client-components"></a><a name="bkmk_sql"></a> Aktualisieren von SQL Server und Clientkomponenten

Microsoft SQL Server 2016 und höher unterstützen TLS 1.1 und TLS 1.2. Für frühere Versionen und abhängige Bibliotheken sind möglicherweise Updates erforderlich. Weitere Informationen finden Sie unter [KB 3135244: TLS 1.2 support for Microsoft SQL Server (KB 3135244: TLS 1.2-Unterstützung für Microsoft SQL Server)](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server).

Sekundäre Standortserver müssen mindestens SQL Server 2016 Express mit Service Pack 2 (13.2.50.26) oder höher verwenden.

### <a name="sql-server-native-client"></a><a name="bkmk_sql-client"></a> SQL Server Native Client

> [!NOTE]
> Unter [KB 3135244](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server) werden auch die Anforderungen für SQL Server-Clientkomponenten aufgeführt.

Stellen Sie sicher, dass auch der SQL Server Native Client mindestens auf Version SQL 2012 SP4 (11.*.7001.0) aktualisiert ist. Ab Version 1810 ist diese Anforderung eine [Voraussetzungsprüfung (Warnung)](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

Configuration Manager verwendet den SQL Server Native Client für die folgenden Standortsystemrollen:

- Standortdatenbankserver
- Standortserver: Standort der zentralen Verwaltung, primärer Standort, sekundärer Standort
- Verwaltungspunkt
- Geräteverwaltungspunkt
- Zustandsmigrationspunkt
- SMS-Anbieter
- Softwareupdatepunkt
- Multicast-fähiger Verteilungspunkt
- Asset Intelligence-Aktualisierungsdienstpunkt
- Reporting Services-Punkt
- Anwendungskatalog-Webdienst
- Anmeldungspunkt
- Endpoint Protection-Punkt
- Dienstverbindungspunkt
- Zertifikatregistrierungspunkt
- Data Warehouse-Dienstpunkt


## <a name="update-windows-server-update-services-wsus"></a><a name="bkmk_wsus"></a> Aktualisieren von Windows Server Update Services (WSUS)

Installieren Sie das folgende Update auf dem WSUS-Server, um TLS 1.2 in früheren Versionen von WSUS zu unterstützen:

- Installieren Sie auf einem WSUS-Server, auf dem Windows Server 2012 ausgeführt wird, [Update 4022721](https://support.microsoft.com/help/4022721) oder ein späteres Rollupupdate.
- Installieren Sie auf einem WSUS-Server, auf dem Windows Server 2012 R2 ausgeführt wird, [Update 4022720](https://support.microsoft.com/help/4022720) oder ein späteres Rollupupdate.

Ab Windows Server 2016 wird TLS 1.2 standardmäßig für WSUS unterstützt.  TLS 1.2-Updates werden nur auf Windows Server 2012 und Windows Server Update Services-Servern für Windows Server 2012 R2 benötigt.

## <a name="next-steps"></a>Nächste Schritte

- [Häufige Probleme beim Aktivieren von TLS 1.2](enable-tls-1-2-troubleshoot.md)
