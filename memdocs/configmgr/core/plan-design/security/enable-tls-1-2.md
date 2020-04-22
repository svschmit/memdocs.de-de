---
title: 'Aktivieren von Transport Layer Security 1.2 (TLS): Übersicht'
titleSuffix: Configuration Manager
description: Übersicht zur Aktivierung von TLS 1.2 für Configuration Manager
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 31de47c9-891b-4de7-8d5e-fbbc1bff7c60
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5d9d7cea7e5653b338a3eb4adb01d9fded99035e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704058"
---
# <a name="how-to-enable-tls-12"></a>Aktivieren von TLS 1.2

*Gilt für: Configuration Manager (Current Branch)*

Transport Layer Security (TLS) ist genauso wie Secure Sockets Layer (SSL) ein Verschlüsselungsprotokoll, das dazu bestimmt ist, Daten zu sichern, wenn diese über ein Netzwerk übertragen werden. In diesen Artikeln werden die erforderlichen Schritte beschrieben, um sicherzustellen, dass die sichere Configuration Manager-Kommunikation das TLS 1.2-Protokoll verwendet. In diesen Artikeln werden zudem die Updateanforderungen für häufig verwendete Komponenten sowie die Behandlung häufiger Probleme erläutert.

## <a name="enabling-tls-12"></a>Aktivierung von TLS 1.2

Die sichere Kommunikation von Configuration Manager basiert auf einer Reihe von Komponenten. Das Protokoll, das für eine bestimmte Verbindung verwendet wird, hängt von den Funktionen aller relevanten Komponenten auf der Seite des Clients als auch auf der Seite des Servers ab. Wenn eine Komponente veraltet oder nicht ordnungsgemäß ist, wird für die Kommunikation möglicherweise ein älteres, weniger sicheres Protokoll verwenden. Sie müssen TLS 1.2 für alle erforderlichen Komponenten aktivieren, damit Configuration Manager TLS 1.2 für alle sicheren Kommunikationen unterstützt. Die erforderlichen Komponenten hängen von Ihrer Umgebung und den verwendeten Configuration Manager-Features ab.

> [!IMPORTANT]
> Starten Sie diesen Prozess mit den Clients, insbesondere bei früheren Versionen von Windows. Bevor Sie TLS 1.2 auf den Configuration Manager-Servern aktivieren und ältere Protokolle deaktivieren, stellen Sie sicher, dass alle Clients TLS 1.2 unterstützen. Andernfalls können die Clients nicht mit den Servern kommunizieren und können verwaisen.


## <a name="tasks-for-configuration-manager-clients-site-servers-and-remote-site-systems"></a>Tasks für Configuration Manager-Clients, Standortserver und Remotestandortsysteme

Sie müssen jeweils auf den Clients und den Standortservern mehrere Tasks ausführen, um TLS 1.2 für Komponenten zu aktivieren, von denen Configuration Manager für die sichere Kommunikation abhängig ist.

### <a name="enable-tls-12-for-configuration-manager-clients"></a>Aktivieren von TLS 1.2 für Configuration Manager-Clients

- [Aktualisieren Sie Windows und WinHTTP unter Windows 8.0, Windows Server 2012 (nicht R2) und früher.](enable-tls-1-2-client.md#bkmk_winhttp)
- [Stellen Sie sicher, dass TLS 1.2 als Protokoll für SChannel auf Betriebssystemebene aktiviert ist.](enable-tls-1-2-client.md#bkmk_protocol)
- [Aktualisieren und konfigurieren Sie .NET Framework zur Unterstützung von TLS 1.2.](enable-tls-1-2-client.md#bkmk_net)


### <a name="enable-tls-12-for-configuration-manager-site-servers-and-remote-site-systems"></a>Aktivieren von TLS 1.2 für Configuration Manager-Standortserver und -Remotestandortsysteme

- [Stellen Sie sicher, dass TLS 1.2 als Protokoll für SChannel auf Betriebssystemebene aktiviert ist.](enable-tls-1-2-server.md#bkmk_protocol)
- [Aktualisieren und konfigurieren Sie .NET Framework zur Unterstützung von TLS 1.2.](enable-tls-1-2-server.md#bkmk_net)
- [Aktualisieren Sie SQL Server und den SQL Native Client.](enable-tls-1-2-server.md#bkmk_sql)
- [Aktualisieren Sie Windows Server Update Services (WSUS).](enable-tls-1-2-server.md#bkmk_wsus)


## <a name="features-and-scenario-dependencies"></a>Features und Szenarioabhängigkeiten

In diesem Abschnitt werden die Abhängigkeiten für bestimmte Configuration Manager-Features und -Szenarios erläutert. Suchen Sie nach den Elementen, die auf Ihre Umgebung zutreffen, um die nächsten Schritte zu ermitteln.

|Funktion oder Szenario|Updateaktion|
|--- |--- |
|Standortserver (zentral, primär oder sekundär)| - [Aktualisieren Sie .NET Framework.](enable-tls-1-2-server.md#bkmk_net)<br/> – Überprüfen Sie die Einstellungen für starke Kryptografie.|
|Standortdatenbankserver|[Aktualisieren Sie SQL Server und seine Clientkomponenten.](enable-tls-1-2-server.md#bkmk_sql)|
|Sekundäre Standortserver|[Aktualisieren Sie SQL Server und seine Clientkomponenten](enable-tls-1-2-server.md#bkmk_sql) auf eine kompatible Version von SQL Express.|
|Standortsystemrollen| - [Aktualisieren Sie .NET Framework](enable-tls-1-2-server.md#bkmk_net), und überprüfen Sie die Einstellungen für starke Kryptografie. <br/> - [Aktualisieren Sie SQL Server und seine Clientkomponenten](enable-tls-1-2-server.md#bkmk_sql) für Rollen, die dies erfordern, einschließlich [SQL Server Native Client](enable-tls-1-2-server.md#bkmk_sql-client).|
|Reporting Services-Punkt|- [Aktualisieren Sie .NET Framework](enable-tls-1-2-server.md#bkmk_net) auf dem Standortserver, den SQL Reporting Services-Servern und jedem Computer mit der Konsole.<br/> – Starten Sie den Dienst SMS_Executive bei Bedarf neu.|
|Softwareupdatepunkt|[Aktualisieren Sie WSUS.](enable-tls-1-2-server.md#bkmk_wsus)|
|Cloudverwaltungsgateway|[TLS 1.2 erzwingen](../../clients/manage/cmg/security-and-privacy-for-cloud-management-gateway.md#bkmk_tls)|
|Configuration Manager-Konsole| - [Aktualisieren Sie .NET Framework.](enable-tls-1-2-client.md#bkmk_net)<br/> – Überprüfen Sie die Einstellungen für starke Kryptografie.|
|Configuration Manager-Client mit HTTPS-Standortsystemrollen|[Aktualisieren Sie Windows, damit TLS 1.2 für die Client-Server-Kommunikation mit WinHTTP unterstützt wird.](enable-tls-1-2-client.md#bkmk_winhttp)|
|Software Center| - [Aktualisieren Sie .NET Framework.](enable-tls-1-2-client.md#bkmk_net)<br/> – Überprüfen Sie die Einstellungen für starke Kryptografie.|
|Windows 7-Clients| *Bevor* Sie TLS 1.2 auf Serverkomponenten aktivieren, [aktualisieren Sie Windows, damit TLS 1.2 für die Client-Server-Kommunikation mit WinHTTP unterstützt wird](enable-tls-1-2-client.md#bkmk_winhttp). Wenn Sie TLS 1.2 zuerst auf Serverkomponenten aktivieren, können frühere Versionen von Clients verwaisen.|

## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen

### <a name="why-use-tls-12-with-configuration-manager"></a>Gründe für die Verwendung von TLS 1.2 mit Configuration Manager

TLS 1.2 ist sicherer als die vorherigen Kryptografieprotokolle wie SSL 2.0, SSL 3.0, TLS 1.0 und TLS 1.1. Im Wesentlichen sorgt TLS 1.2 dafür, dass Daten sicherer über das Netzwerk übertragen werden.

### <a name="where-does-configuration-manager-use-encryption-protocols-like-tls-12"></a>Wo verwendet Configuration Manager Verschlüsselungsprotokolle wie TLS 1.2?

Es gibt im Grunde genommen fünf Bereiche, für die Configuration Manager Verschlüsselungsprotokolle wie TLS 1.2 verwendet:

- Bei Clientkommunikationen zu IIS-basierten Standortserverrollen, wenn die Rolle für die Verwendung von HTTPS konfiguriert ist. Diese Rollen sind u. a. Verteilungspunkte, Softwareupdatepunkte und Verteilungspunkte.
- Verwaltungspunkt-, SMS-Executive- und SMS-Anbieterkommunikationen mit SQL. Configuration Manager verschlüsselt SQL-Kommunikationen immer.
- Kommunikation zwischen Standortserver und WSUS, wenn WSUS für die Verwendung von HTTPS konfiguriert ist
- Configuration Manager-Konsole zu SQL Server Reporting Services (SSRS), wenn SSRS für die Verwendung von HTTPS konfiguriert ist
- Alle Verbindungen zu internetbasierten Diensten. Beispiele hierfür sind das Cloudverwaltungsgateway (Cloud Management Gateway, CMG), die Synchronisierung des Dienstverbindungspunkts und die Synchronisierung der Updatemetadaten von Microsoft Update.

### <a name="what-determines-which-encryption-protocol-is-used"></a>Wodurch wird bestimmt, welches Verschlüsselungsprotokoll verwendet wird?

HTTPS wird immer die höchste Protokollversion aushandeln, die vom Client und dem Server in einer verschlüsselten Konversation unterstützt wird. Beim Herstellen einer Verbindung sendet der Client eine Nachricht an den Server mit dem höchsten verfügbaren Protokoll. Wenn der Server die gleiche Version unterstützt, sendet dieser eine Nachricht mit dieser Version. Diese ausgehandelte Version ist die, die für die Verbindung verwendet wird. Wenn der Server die vom Client vorgelegte Version nicht unterstützt, gibt die Servermeldung die höchste Version an, die der Server verwenden kann. Weitere Informationen zum TLS-Handshake-Protokoll finden Sie unter [Einrichten einer sicheren Sitzung mithilfe von TLS](https://docs.microsoft.com/windows/win32/secauthn/tls-handshake-protocol#establishing-a-secure-session-by-using-tls).

### <a name="what-determines-which-protocol-version-the-client-and-server-can-use"></a>Was bestimmt die Protokollversion, die vom Client und vom Server verwendet werden kann?

Im Allgemeinen können die folgenden Elemente bestimmen, welche Protokollversion verwendet wird:

- Die Anwendung kann vorschreiben, welche bestimmte Protokollversion aushandelt werden soll.
  - Gemäß der Best Practices soll verhindert werden, dass bestimmte Protokolle auf Anwendungsebene hartcodiert werden und dass die auf der Protokollebene der Komponente und des Betriebssystems definierte Konfiguration befolgt wird.
  - Configuration Manager befolgt diese Best Practices.
- Für Anwendungen, die mit .NET Framework geschrieben werden, sind die Standardprotokollversionen von der Version des Frameworks abhängig, auf dem sie kompiliert wurden.  
  - in den .NET-Versionen vor 4.6.3 waren TLS 1.1 und 1.2 standardmäßig nicht in der Liste der Protokolle für die Aushandlung enthalten.
- Anwendungen, die WinHTTP für HTTPS-Kommunikationen (wie den Configuration Manager-Client) verwenden, sind von der Betriebssystemversion, der Patchebene und der Konfiguration für die Protokollversionsunterstützung abhängig.


## <a name="additional-resources"></a>Zusätzliche Ressourcen

- [Technische Referenz für kryptografische Steuerelemente](cryptographic-controls-technical-reference.md)
- [Bewährte Methoden für Transport Layer Security (TLS) mit .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)
- [KB 3135244: TLS 1.2 support for Microsoft SQL Server (KB 3135244: TLS 1.2-Unterstützung für Microsoft SQL Server)](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)

## <a name="next-steps"></a>Nächste Schritte

- [Aktivieren von TLS 1.2 auf Clients](enable-tls-1-2-client.md)
- [Aktivieren von TLS 1.2 auf Standortservern](enable-tls-1-2-server.md)
