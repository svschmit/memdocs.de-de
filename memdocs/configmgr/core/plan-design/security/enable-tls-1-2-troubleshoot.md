---
title: Häufige Probleme beim Aktivieren von Transport Layer Security 1.2 (TLS)
titleSuffix: Configuration Manager
description: Informationen zu den häufigsten Probleme beim Aktivieren von Transport Layer Security 1.2 (TLS)
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 15083f28-8ff2-4e23-9f5e-b5dbd0859839
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7c07b0af1b3063619ac5f71965d96f611aefafd9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704068"
---
# <a name="common-issues-when-enabling-tls-12"></a>Häufige Probleme beim Aktivieren von TLS 1.2

In diesem Artikel wird beschrieben, wie Sie häufige Probleme beheben können, die beim Aktivieren der TLS 1.2-Unterstützung in Configuration Manager auftreten können.

## <a name="unsupported-platforms"></a>Nicht unterstützte Plattformen

Die folgenden Clientplattformen werden von Configuration Manager unterstützt, jedoch nicht in einer TLS 1.2-Umgebung:

- Windows CE
- Apple OS X
- Windows 10-Geräte, die mit lokalem MDM verwaltet werden

## <a name="reports-dont-show-in-the-console"></a>Berichte werden nicht in der Konsole angezeigt

Wenn Berichte nicht in der Configuration Manager-Konsole angezeigt werden, stellen Sie sicher, dass der Computer aktualisiert ist, auf dem Sie die Konsole ausführen. [Aktualisieren Sie .NET Framework](enable-tls-1-2-client.md#bkmk_net), und aktivieren Sie die starke Kryptografie.

## <a name="fips-security-policy-enabled"></a>Aktivierte FIPS-Sicherheitsrichtlinie

Wenn Sie die FIPS-Sicherheitsrichtlinie für den Client oder einen Server aktivieren, kann die Aushandlung eines Schannels (sicherer Kanal) dazu führen, dass TLS 1.0 verwendet wird. Dieses Verhalten tritt auch dann auf, wenn Sie das Protokoll in der Registrierung deaktivieren.

Sie können überprüfen, ob dieser Fall vorliegt, indem Sie die Ereignisprotokollierung für Schannels aktivieren und dann die Schannel-Ereignisse im Systemprotokoll ansehen. Weitere Informationen finden Sie unter [Beschränken der Verwendung bestimmter kryptografischer Algorithmen und Protokolle in „Schannel.dll“](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc).

## <a name="sql-server-communication-failure"></a>SQL Server-Kommunikationsfehler

Wenn bei der SQL Server-Kommunikation ein Fehler auftritt und der Fehler **SslSecurityError** zurückgegeben wird, überprüfen Sie die folgenden Einstellungen:

- [Aktualisierung von .NET Framework](enable-tls-1-2-server.md#bkmk_net) und Aktivierung der starken Kryptografie auf allen Computern
- [Aktualisierung von SQL Server](enable-tls-1-2-server.md#bkmk_sql) auf dem Hostserver
- [Aktualisierung der SQL-Clientkomponenten](enable-tls-1-2-server.md#bkmk_sql-client) auf allen Systemen, die mit SQL kommunizieren. Dies sind beispielsweise die Standortserver, der SMS-Anbieter und die Standortrollenserver.

## <a name="configuration-manager-client-communication-failures"></a>Kommunikationsfehler mit Configuration Manager-Clients

Wenn der Configuration Manager-Client nicht mit Standortrollen kommuniziert, überprüfen Sie, ob Sie [Windows so aktualisiert haben](enable-tls-1-2-client.md#bkmk_winhttp), dass TLS 1.2 für die Client-Server-Kommunikation mit WinHTTP unterstützt wird. Übliche Standortrollen umfassen Verteilungspunkte, Verwaltungspunkte und Zustandsmigrationspunkte.

## <a name="reporting-services-point-fails-and-returns-an-expected-error"></a>Fehler bei Reporting Services-Punkt und Ausgabe eines erwarteten Fehlers

Wenn der Reporting Services-Punkt keine Berichte konfiguriert, überprüfen Sie, ob folgender Fehlereintrag in **SRSRP.log** vorhanden ist:

`The underlying connection was closed:`
`An expected error occurred on a receive.`

Gehen Sie folgendermaßen vor, um das Problem zu lösen:

1. [Aktualisieren Sie .NET Framework](enable-tls-1-2-client.md#bkmk_net), und aktivieren Sie die starke Kryptografie auf allen relevanten Computern.

1. Nachdem Sie Updates installiert haben, starten Sie den SMS_Executive-Dienst neu.

## <a name="application-catalog-doesnt-initialize"></a>Keine Initialisierung des Anwendungskatalogs

> [!Important]  
> Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910. Weitere Informationen finden Sie unter [Entfernte und veraltete Features](../changes/deprecated/removed-and-deprecated-cmfeatures.md).

Wenn der Anwendungskatalog nicht initialisiert wird, überprüfen Sie, ob folgender Fehlereintrag in **ServicePortalWebSite.svclog** vorhanden ist:

`SOAP security negotiation failed. The client and server can't communicate because they don't share a common algorithm.`

Gehen Sie folgendermaßen vor, um das Problem zu lösen:

1. [Aktualisieren Sie .NET Framework](enable-tls-1-2-client.md#bkmk_net), und aktivieren Sie die starke Kryptografie auf allen relevanten Computern.

1. Erstellen Sie im Ordner `%WinDir%\System32\InetSrv` des Anwendungskatalogservers eine Datei **W2SP.exe.config** mit folgendem Inhalt:

    ``` XML
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <runtime>
      <AppContextSwitchOverrides value="Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols=false;Switch.System.Net.DontEnableSchUseStrongCrypto=false" />
      </runtime>
    </configuration>
    ```

    > [!NOTE]
    > Bei dieser Datei handelt es sich um die Standarddatei, die erstellt wird, sofern die Anwendung mit .NET Framework 4.6.3 erstellt wurde.

1. Verwenden Sie die HTTPS-Transportsicherheit für Anwendungskatalogrollen.

    > [!Important]
    > Wenn Sie die HTTP-Nachrichtensicherheit für Anwendungskatalogrollen verwenden, wird WCF (Windows Communication Foundation) dafür hartcodiert, nur SSL 3.0 und TLS 1.0 zu verwenden. Dadurch wird die Verwendung von TLS 1.2 verhindert.

1. Wenn Sie Änderungen vorgenommen haben, starten Sie den Computer neu.

## <a name="software-center-or-browser-doesnt-communicate-with-the-application-catalog"></a>Softwarecenter oder Browser kommunizieren nicht mit dem Anwendungskatalog

> [!Important]  
> Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910. Weitere Informationen finden Sie unter [Entfernte und veraltete Features](../changes/deprecated/removed-and-deprecated-cmfeatures.md).

Die beste Methode, damit das Softwarecenter mit für Benutzer verfügbaren Apps an einem TL 1.2-fähigen Standort arbeiten kann, ist das Entfernen der Anwendungskatalogrolle. Lassen Sie das Softwarecenter anschließend direkt mit einem Verwaltungspunkt kommunizieren. Weitere Informationen finden Sie unter [Entfernen des Anwendungskatalogs](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat).

Wenn Sie Kommunikationsfehler zwischen dem Anwendungskatalog und dem Softwarecenter beheben müssen, überprüfen Sie Folgendes:

- [Aktualisieren Sie .NET Framework](enable-tls-1-2-client.md#bkmk_net), und aktivieren Sie die starke Kryptografie auf allen Computern.

- Starten Sie alle betroffenen Computer neu, nachdem Sie die Änderungen vorgenommen haben.

<!-- - Configure the browser is configured to support TLS 1. Prior to Windows 10, this option was disabled by default. removing, Silverlight experience is out of support-->

## <a name="service-connection-point-upload-failures"></a>Uploadfehler bei Dienstverbindungspunkten

Wenn der Dienstverbindungspunkt keine Daten in SCCMConnectedService hochlädt, [aktualisieren Sie .NET Framework](enable-tls-1-2-server.md#bkmk_net), und aktivieren Sie die starke Kryptografie auf allen Computern. Denken Sie nach dem Ausführen der Änderungen daran, den Computer neu zu starten.

## <a name="configuration-manager-console-displays-intune-onboarding-dialog-box"></a>Intune-Anmeldedialogfeld in der Configuration Manager-Konsole

Wenn das Intune-Anmeldedialogfeld angezeigt wird, sobald die Konsole eine Verbindung mit dem Intune-Portal herstellt, [aktualisieren Sie .NET Framework](enable-tls-1-2-client.md#bkmk_net), und aktivieren Sie die starke Kryptografie auf allen Computern. Denken Sie nach dem Ausführen der Änderungen daran, den Computer neu zu starten.

## <a name="configuration-manager-console-displays-failure-to-sign-in-to-azure"></a>Fehler in der Configuration Manager-Konsole bei der Anmeldung bei Azure

Wenn bei dem Versuch, Anwendungen in Azure Active Directory (Azure AD) zu erstellen, sofort ein Fehler im Anmeldedialogfeld für Azure-Dienste auftritt, nachdem Sie auf **Anmelden** geklickt haben, [aktualisieren Sie .NET Framework](enable-tls-1-2-server.md#bkmk_net), und aktivieren Sie die starke Kryptografie. Denken Sie nach dem Ausführen der Änderungen daran, den Computer neu zu starten.

## <a name="configuration-manager-cloud-services-and-tls-12"></a>Configuration Manager-Clouddienste und TLS 1.2

Die virtuellen Azure-Computer, die von Cloud Management Gateway und Cloudverteilungspunkten verwendet werden, bieten Unterstützung für TLS 1.2. Unterstützte Clientversionen verwenden automatisch TLS 1.2.

**SMSAdminui.log** kann einen Fehler enthalten, der folgendem Beispiel ähnelt:

``` Log
Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationException
Service returned error. Check InnerException for more details
at Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationContext.GetAADAuthResultObject
...
Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException
Service returned error. Check InnerException for more details
at Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext.RunAsyncTask
...
System.Net.WebException
The underlying connection was closed: An unexpected error occurred on a receive.
at System.Net.HttpWebRequest.GetResponse
```

Im Systemereignisprotokoll ist möglicherweise SChannel-Ereignis-ID 36874 mit der folgenden Beschreibung protokolliert: `An TLS 1.2 connection request was received from a remote client application, but none of the cipher suites supported by the client application are supported by the server. The TLS connection request has failed.`
<!--SCCMDocs issue #1608-->

## <a name="additional-resources"></a>Zusätzliche Ressourcen

- [Bewährte Methoden für Transport Layer Security (TLS) mit .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)
- [KB 3135244: TLS 1.2 support for Microsoft SQL Server (KB 3135244: TLS 1.2-Unterstützung für Microsoft SQL Server)](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)
- [Technische Referenz für kryptografische Steuerelemente](cryptographic-controls-technical-reference.md)

## <a name="next-steps"></a>Nächste Schritte

- [Aktivieren von TLS 1.2 auf Clients](enable-tls-1-2-client.md)
- [Aktivieren von TLS 1.2 auf Standortservern und Remotestandortsystemen](enable-tls-1-2-server.md)

