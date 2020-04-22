---
title: Problembehandlung für Connected Cache
titleSuffix: Configuration Manager
description: Technische Details für Microsoft Connected Cache, um Sie bei der Problembehandlung zu unterstützen.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 121e0341-4f51-4d54-a357-732c26caf7c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e5be6158a2ed7d79af2bee72c81a462e4d83b68e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700868"
---
# <a name="troubleshoot-microsoft-connected-cache-in-configuration-manager"></a>Problembehandlung für Microsoft Connected Cache in Configuration Manager

Dieser Artikel enthält technische Details zu Microsoft Connected Cache in Configuration Manager. Verwenden Sie diesen Dienst, um Probleme zu beheben, die möglicherweise in Ihrer Umgebung auftreten. Weitere Informationen zur Funktionsweise und Verwendung finden Sie unter [Microsoft Connected Cache in Configuration Manager](../../../plan-design/hierarchy/microsoft-connected-cache.md).

> [!NOTE]
> Ab Version 1910 wird dieses Feature als **Microsoft Connected Cache** bezeichnet. Zuvor wurde es als Übermittlungsoptimierung durch netzwerkinternen Cache (Delivery Optimization In-Network Cache, DOINC) bezeichnet.

## <a name="verify"></a>Überprüfen

Wenn Sie den Cacheserver für die Übermittlungsoptimierung ordnungsgemäß installieren und Clients ordnungsgemäß konfigurieren, werden diese von dem auf Ihrem Verteilungspunkt installierten Cacheserver und nicht vom Internet heruntergeladen.

Überprüfen Sie dieses Verhalten [auf einem Client](#bkmk_verify-client) oder [auf dem Server](#bkmk_verify-server).

### <a name="verify-on-a-client"></a><a name="bkmk_verify-client"></a> Überprüfung auf einem Client

1. Laden Sie auf dem Client mit Windows 10, Version 1809 oder höher, in der Cloud verwaltete Inhalte herunter. Weitere Informationen zu den Inhaltstypen, die von Connected Cache unterstützt werden, finden Sie unter [Überprüfen von Connected Cache](../../../plan-design/hierarchy/microsoft-connected-cache.md#verify).

2. Öffnen Sie PowerShell, und führen Sie den folgenden Befehl aus: `Get-DeliveryOptimizationStatus`

Beispiel:

```PowerShell
PS C:\> Get-DeliveryOptimizationStatus

FileId                      : ec523d49c4f7c3c4444f0d9b952286ce40fdcee4
FileSize                    : 549064
TotalBytesDownloaded        : 549064
PercentPeerCaching          : 0
BytesFromPeers              : 0
BytesFromHttp               : 0
Status                      : Caching
Priority                    : Background
BytesFromCacheServer        : 549064
BytesFromLanPeers           : 0
BytesFromGroupPeers         : 0
BytesFromInternetPeers      : 0
BytesToLanPeers             : 0
BytesToGroupPeers           : 0
BytesToInternetPeers        : 0
DownloadDuration            : 00:00:00.0780000
HttpConnectionCount         : 2
LanConnectionCount          : 0
GroupConnectionCount        : 0
InternetConnectionCount     : 0
DownloadMode                : 99
SourceURL                   : http://au.download.windowsupdate.com/c/msdownload/update/software/defu/2019/09/am_delta_p
                              atch_1.301.664.0_ec523d49c4f7c3c4444f0d9b952286ce40fdcee4.exe
NumPeers                    : 0
PredefinedCallerApplication : WU Client Download
ExpireOn                    : 9/6/2019 8:36:19 AM
IsPinned                    : False
```

Beachten Sie, dass das `BytesFromCacheServer`-Attribut nicht 0 (null) ist.

Wenn der Client nicht ordnungsgemäß konfiguriert oder der Cacheserver nicht ordnungsgemäß installiert ist, greift der Übermittlungsoptimierungsclient auf die ursprüngliche Cloudquelle zurück. Dann hat das BytesFromCacheServer-Attribut den Wert 0 (null).

### <a name="verify-on-the-server"></a><a name="bkmk_verify-server"></a> Überprüfung auf einem Server

Vergewissern Sie sich zunächst, dass die Registrierungseigenschaften ordnungsgemäß konfiguriert sind: `HKLM\SOFTWARE\Microsoft\Delivery Optimization In-Network Cache`. Der Cachespeicherort des Laufwerks lautet z. B. `PrimaryDrivesInput\DOINC-E77D08D0-5FEA-4315-8C95-10D359D59294`, wobei `PrimaryDrivesInput` mehrere Laufwerke sein können, wie z. B. `C,D,E`.

Verwenden Sie als Nächstes die folgende Methode, um eine Clientdownloadanforderung an den Server mit den obligatorischen Headern zu simulieren.

1. Öffnen Sie ein 64-Bit-PowerShell-Fenster als Administrator.
2. Führen Sie den folgenden Befehl aus, und ersetzen Sie den Namen oder die IP-Adresse des Servers für `<DoincServer>`:

```PowerShell
Invoke-WebRequest -URI "http://<DoincServer>/mscomtest/wuidt.gif" -Headers @{"Host"="b1.download.windowsupdate.com"}
```

Die Ausgabe sieht etwa folgendermaßen aus:

```PowerShell
PS C:\WINDOWS\system32> Invoke-WebRequest -URI "http://SERVER01.CONTOSO.COM/mscomtest/wuidt.gif" -Headers @{"Host"="b1.download.windowsupdate.com"}


StatusCode        : 200
StatusDescription : OK
Content           : {71, 73, 70, 56...}
RawContent        : HTTP/1.1 200 OK
                    X-HW: 1567797125.dop019.se2.t,1567797125.cds058.se2.s,1567797125.dop114.at2.r,1567797125.cds079.at2
                    .p,1567797125.cds058.se2.p
                    X-CCC: cdP+dRBgUCoZO1mezA9zhg2VwQ7P1JWTh9k+GhfQmu8=_SLwv...
Headers           : {[X-HW, 1567797125.dop019.se2.t,1567797125.cds058.se2.s,1567797125.dop114.at2.r,1567797125.cds079.a
                    t2.p,1567797125.cds058.se2.p], [X-CCC,
                    cdP+dRBgUCoZO1mezA9zhg2VwQ7P1JWTh9k+GhfQmu8=_SLwvtSBQdT3uPQ5ikBe1ABMbdYIIncem+h5dtcLI6GY=],
                    [X-CID, 100], [Accept-Ranges, bytes]...}
RawContentLength  : 969710
```

Die folgenden Attribute geben Erfolg an:

- `StatusCode : 200`
- `StatusDescription : OK`

## <a name="log-files"></a>Protokolldateien

- ARR-Setupprotokoll: `%temp%\arr_setup.log`

- Setupprotokoll des Cacheservers der Übermittlungsoptimierung: `SMS_DP$\Ms.Dsp.Do.Inc.Setup\DoincSetup.log` auf dem Verteilungspunkt und `DistMgr.log` auf dem Standortserver

- IIS-Betriebsprotokolle: Standardmäßig lauten sie `%SystemDrive%\inetpub\logs\LogFiles`.

- Betriebsprotokoll des Cacheservers der Übermittlungsoptimierung: `C:\Doinc\Product\Install\Logs`

    > [!TIP]
    > Neben anderen Verwendungsmöglichkeiten kann dieses Protokoll Ihnen helfen, Konnektivitätsprobleme mit der Microsoft-Cloud zu identifizieren.

## <a name="setup-error-codes"></a>Setup-Fehlercodes

In der folgenden Tabelle werden die möglichen Fehlercodes aufgeführt, die auftreten können, wenn Configuration Manager die Connected Cache-Komponente auf dem Verteilungspunkt installiert:

| Fehlercode | Fehlerbeschreibung |
|------------|-------------------|
| 0x00000000 | Erfolgreich |
| 0x00000BC2 | Erfolgreich, Neustart erforderlich |
| 0x00000643 | Generischer Installationsfehler |
| 0x00D00001 | Das Connected Cache-Setup kann nur ausgeführt werden, wenn Internetinformationsdienste (IIS) installiert sind. |
| 0x00D00002 | Das Connected Cache-Setup kann nur ausgeführt werden, wenn auf dem Server eine Standardwebsite vorhanden ist. |
| 0x00D00003 | Sie können Connected Cache nicht installieren, wenn das Routing von Anwendungsanforderungen (ARR) bereits installiert ist. |
| 0x00D00004 | Das Connected Cache-Setup kann nur ausgeführt werden, wenn das Routing von Anwendungsanforderungen (ARR) durch das Skript „Install.ps1“ installiert wurde. |
| 0x00D00005 | Das Connected Cache-Setup erfordert eine PowerShell-Sitzung, die als Administrator ausgeführt wird. |
| 0x00D00006 | Das Connected Cache-Setup kann nur über eine 64-Bit-PowerShell-Umgebung ausgeführt werden. |
| 0x00D00007 | Das Connected Cache-Setup kann nur auf Windows-Server ausgeführt werden. |
| 0x00D00008 | Fehler: Die Zahl der angegebenen Cachelaufwerke muss mit der Zahl der angegebenen Cachelaufwerk-Prozentsätze identisch sein. |
| 0x00D00009 | Fehler: Es muss eine gültige Cacheknoten-ID angegeben werden. |
| 0x00D0000A | Fehler: Es muss ein gültiger Cachelaufwerksatz angegeben werden. |
| 0x00D0000B | Fehler: Es muss ein gültiger Prozentsatz der Cachelaufwerkgröße angegeben werden. |
| 0x00D0000C | Fehler: Es muss ein gültiger Prozentsatz der Cachelaufwerkgröße oder die Cachelaufwerkgröße in GB angegeben werden. |
| 0x00D0000D | Fehler: Ein gültiger Prozentsatz der Cachelaufwerkgröße und die Cachelaufwerkgröße in GB können nicht gleichzeitig angegeben werden. |
| 0x00D0000E | Fehler: Die Zahl der angegebenen Cachelaufwerke muss der Zahl der angegebenen Cachelaufwerkgröße in GB entsprechen. |
| 0x00D0000F | Fehler: Die Datei „applicationhost.config“ konnte nicht von $AppHostConfig nach $AppHostConfigDestinationName gesichert werden. |
| 0x00D00010 | Fehler: Die Datei „web.config“ der Standardwebsite konnte nicht von $WebsiteConfigFilePath nach $WebConfigDestinationName gesichert werden. |
| 0x00D00011 | Fehler: In „SetupARRWebFarm.ps1“ ist eine Ausnahme aufgetreten. |
| 0x00D00012 | Fehler: In „SetupARRWebFarmRewriteRules.ps1“ ist eine Ausnahme aufgetreten. |
| 0x00D00013 | Fehler: In „SetupARRWebFarmProperties.ps1“ ist eine Ausnahme aufgetreten. |
| 0x00D00014 | Fehler: In „SetupAllowableServerVariables.ps1“ ist eine Ausnahme aufgetreten. |
| 0x00D00015 | Fehler: In „SetupFirewallRules.ps1“ ist eine Ausnahme aufgetreten. |
| 0x00D00016 | Fehler: In „SetupAppPoolProperties.ps1“ ist eine Ausnahme aufgetreten. |
| 0x00D00017 | Fehler: In „SetupARROutboundRules.ps1“ ist eine Ausnahme aufgetreten. |
| 0x00D00018 | Fehler: In „SetupARRDiskCache.ps1“ ist eine Ausnahme aufgetreten. |
| 0x00D00019 | Fehler: In „SetupARRProperties.ps1“ ist eine Ausnahme aufgetreten. |
| 0x00D0001A | Fehler: In „SetupARRHealthProbes.ps1“ ist eine Ausnahme aufgetreten. |
| 0x00D0001B | Fehler: In „VerifyIISSItesStarted.ps1“ ist eine Ausnahme aufgetreten. |
| 0x00D0001C | Fehler: In „SetDrivesToHealthy.ps1“ ist eine Ausnahme aufgetreten. |
| 0x00D0001D | Fehler: In "VerifyCacheNodeSetup.ps1" ist eine Ausnahme aufgetreten. |
| 0x00D0001E | Sie können Connected Cache nicht installieren, wenn die Standardwebsite nicht auf Port 80 festgelegt ist. |
| 0x00D0001F | Fehler: Die Cachelaufwerkzuordnung in Prozent darf 100 nicht überschreiten. |
| 0x00D00020 | Fehler: Die Cachelaufwerkzuordnung in GB darf den freien Speicherplatz des Laufwerks nicht überschreiten. |
| 0x00D00021 | Fehler: Die Cachelaufwerkzuordnung in Prozent muss größer als 0 sein. |
| 0x00D00022 | Fehler: Die Cachelaufwerkzuordnung in GB muss größer als 0 sein. |
| 0x00D00023 | Fehler: In RegisterScheduledTask_CacheNodeKeepAlive ist eine Ausnahme aufgetreten. |
| 0x00D00024 | Fehler: In RegisterScheduledTask_Maintenance ist eine Ausnahme aufgetreten. |
| 0x00D00025 | Fehler: Beim Einrichten der Nachschreibungsregeln für HTTPS-Farm: $FarmName ist eine Ausnahme aufgetreten. |
| 0x00D00026 | Fehler: Beim Einrichten der Nachschreibungsregeln für HTTP-Farm: $FarmName ist eine Ausnahme aufgetreten. |
| 0x00D00027 | Connected Cache kann nicht installiert werden, da die abhängige Software „Routing von Anwendungsanforderungen (ARR)“ nicht installiert werden konnte. Weitere Informationen finden Sie in der Protokolldatei unter %temp%\arr_setup.log. |

## <a name="iis-configurations"></a>IIS-Konfigurationen

Die Installation des Cacheservers der Übermittlungsoptimierung durchführt mehrere Änderungen an der IIS-Konfiguration auf dem Verteilungspunkt.

### <a name="application-request-routing"></a>Routing der Anwendungsanforderung

Der Cacheserver der Übermittlungsoptimierung installiert und konfiguriert IIS [Routing von Anwendungsanforderungen (ARR)](https://www.iis.net/downloads/microsoft/application-request-routing). Diese Komponente darf auf dem Verteilungspunkt nicht vorinstalliert sein, um potenzielle Konflikte zu vermeiden.

### <a name="allowed-server-variables"></a>Zulässige Servervariablen

Nachdem Sie den Cacheserver der Übermittlungsoptimierung installiert haben, verfügt die Standardwebsite über die folgenden *lokalen* Servervariablen:

- HTTP_HOST
- QUERY_STRING
- X-CCC
- X-CID
- X-DOINC-OUTBOUND

### <a name="rewrite-rules"></a>Neuschreibungsregeln

Der Cacheserver der Übermittlungsoptimierung fügt die folgenden Neuschreibungsregeln hinzu:

#### <a name="inbound-rewrite-rules"></a>Eingehende Neuschreibungsregeln

- `Doinc_ForwardToFarm_shswda01.download.manage-selfhost.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_swdc01.manage.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_swdc02.manage.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_dl.delivery.mp.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_officecdn.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_b1.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_officecdn.microsoft.com.edgesuite.net_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_au.b1.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_assets1.xboxlive.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_au.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_emdl.ws.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_tlu.dl.delivery.mp.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_assets2.xboxlive.com_E77D08D0-5FEA-4315-8C95-10D359D59294`

#### <a name="outbound-rewrite-rules"></a>Ausgehende Neuschreibungsregeln

- `Doinc_Outbound_SetHeader_X_CID_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_Outbound_SetHeader_X_CCC_E77D08D0-5FEA-4315-8C95-10D359D59294`

## <a name="manage-server-resources"></a>Verwalten von Serverressourcen

Der für jeden Cacheserver der Übermittlungsoptimierung erforderliche Speicherplatz kann je nach den Updateanforderungen Ihres Unternehmens variieren. 100 GB sollten ausreichend Speicherplatz bieten, um den folgenden Inhalt zwischenzuspeichern:

- Ein Featureupdate
- Qualitätsupdates und Office-Updates für zwei bis drei Monate
- Microsoft Intune-Apps und Windows-Inbox-Apps

Der Cacheserver der Übermittlungsoptimierung sollte nicht viel Systemarbeitsspeicher oder Prozessorzeit beanspruchen. Wenn Sie nach der Installation des Cacheservers der Übermittlungsoptimierung einen erheblichen Prozess- oder Arbeitsspeicherressourcenverbrauch feststellen, analysieren Sie die IIS- und ARR-Protokolldateien.

Wenn die IIS- und ARR-Protokolldateien zu viel Speicherplatz auf dem Server beanspruchen, gibt es mehrere Methoden, die Sie zum Verwalten der Protokolldateien anwenden können. Weitere Informationen finden Sie unter [IIS-Protokolldateienspeicher verwalten](https://docs.microsoft.com/iis/manage/provisioning-and-managing-iis/managing-iis-log-file-storage#overview).

## <a name="see-also"></a>Weitere Informationen:

[Microsoft Connected Cache in Configuration Manager](../../../plan-design/hierarchy/microsoft-connected-cache.md)
