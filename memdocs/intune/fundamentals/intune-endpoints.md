---
title: Netzwerkendpunkte für Microsoft Intune
titleSuffix: ''
description: Überprüfen Sie die Endpunkte für Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/08/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: b8d9aef2-8757-4e22-9b24-a0833d27304c
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: fbf157c50ce3ffd2e090c8e0c0310c40b9e26202
ms.sourcegitcommit: 6e488937039e8437866d55f2f23e5944a4b35a35
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/23/2020
ms.locfileid: "91022350"
---
# <a name="network-endpoints-for-microsoft-intune"></a>Netzwerkendpunkte für Microsoft Intune  

Auf dieser Seite werden IP-Adressen und Porteinstellungen aufgelistet, die für Proxyeinstellungen in Ihren Intune-Bereitstellungen benötigt werden.

Da Intune ein Clouddienst ist, ist keine lokale Infrastruktur wie etwa Server oder Gateways erforderlich.

## <a name="access-for-managed-devices"></a>Zugriff für verwaltete Geräte  

Sie müssen die Kommunikation für Intune aktivieren, um Geräte hinter Firewalls und Proxyservern zu verwalten.

> [!NOTE]
> Die Informationen in diesem Abschnitt gelten auch für den Microsoft Intune Certificate Connector. Der Connector hat die gleichen Netzwerkanforderungen wie verwaltete Geräte.

- Der Proxyserver muss sowohl **HTTP (80)** als auch **HTTPS (443)** unterstützen, weil Intune-Clients beide Protokolle verwenden. Windows Information Protection verwendet Port 444.
- Bei einigen Aufgaben (wie dem Herunterladen von Softwareupdates für den klassischen PC-Agent) erfordert Intune Zugriff auf nicht authentifizierte Proxyserver auf „manage.microsoft.com“.

Sie können die Proxyservereinstellungen auf einzelnen Clientcomputern festlegen. Sie können zudem Gruppenrichtlinieneinstellungen verwenden, um die Einstellungen für alle Clientcomputer hinter einem bestimmten Proxyserver anzupassen.


<!--
> [!NOTE] If Windows 8.1 devices haven't cached proxy server credentials, enrollment might fail because the request doesn't prompt for credentials. Enrollment fails without warning as the request wait for a connection. If users might experience this issue, instruct them to open their browser settings and save proxy server settings to enable a connection.   -->

Für verwaltete Geräte sind Konfigurationen erforderlich, über die **Alle Benutzer** über Firewalls auf Dienste zugreifen können.


In den folgenden Tabellen sind die Ports und Dienste aufgeführt, auf die der Intune-Client zugreift:

|Domänen    |IP-Adresse      |
|-----------|----------------|
| login.microsoftonline.com <br> *.officeconfig.msocdn.com <br> config.office.com <br> graph.windows.net <br> enterpriseregistration.windows.net | Weitere Informationen finden Sie unter [URLs und IP-Adressbereiche von Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2). |
|portal.manage.microsoft.com<br> m.manage.microsoft.com |52.175.12.209<br>20.188.107.228<br>52.138.193.149<br>51.144.161.187<br>52.160.70.20<br>52.168.54.64 <br>13.72.226.202<br>52.189.220.232|
| sts.manage.microsoft.com | 13.93.223.241 <br>52.170.32.182 <br>52.164.224.159 <br>52.174.178.4 <br>13.75.122.143 <br>52.163.120.84<br>13.73.112.122<br>52.237.192.112|
|Manage.microsoft.com <br>i.manage.microsoft.com <br>r.manage.microsoft.com <br>a.manage.microsoft.com <br>p.manage.microsoft.com <br>EnterpriseEnrollment.manage.microsoft.com <br>EnterpriseEnrollment-s.manage.microsoft.com |40.83.123.72<br>13.76.177.110<br>52.169.9.87<br>52.174.26.23<br>104.40.82.191<br>13.82.96.212<br>52.147.8.239<br>40.115.69.185|
|portal.fei.msua01.manage.microsoft.com<br>m.fei.msua01.manage.microsoft.com<br>portal.fei.msua02.manage.microsoft.com<br>m.fei.msua02.manage.microsoft.com<br>portal.fei.msua04.manage.microsoft.com<br>m.fei.msua04.manage.microsoft.com<br>portal.fei.msua05.manage.microsoft.com<br>m.fei.msua05.manage.microsoft.com<br>portal.fei.amsua0502.manage.microsoft.com<br>m.fei.amsua0502.manage.microsoft.com<br>portal.fei.msua06.manage.microsoft.com<br>m.fei.msua06.manage.microsoft.com<br>portal.fei.amsua0602.manage.microsoft.com<br>m.fei.amsua0602.manage.microsoft.com<br>fei.amsua0202.manage.microsoft.com<br>portal.fei.amsua0202.manage.microsoft.com<br>m.fei.amsua0202.manage.microsoft.com<br>portal.fei.amsua0402.manage.microsoft.com<br>m.fei.amsua0402.manage.microsoft.com<br>portal.fei.amsua0801.manage.microsoft.com<br>portal.fei.msua08.manage.microsoft.com<br>m.fei.msua08.manage.microsoft.com<br>m.fei.amsua0801.manage.microsoft.com|52.160.70.20<br>52.168.54.64 |
|portal.fei.msub01.manage.microsoft.com<br>m.fei.msub01.manage.microsoft.com<br>portal.fei.amsub0102.manage.microsoft.com<br>m.fei.amsub0102.manage.microsoft.com<br>fei.msub02.manage.microsoft.com<br>portal.fei.msub02.manage.microsoft.com<br>m.fei.msub02.manage.microsoft.com<br>portal.fei.msub03.manage.microsoft.com<br>m.fei.msub03.manage.microsoft.com<br>portal.fei.msub05.manage.microsoft.com<br>m.fei.msub05.manage.microsoft.com<br>portal.fei.amsub0202.manage.microsoft.com<br>m.fei.amsub0202.manage.microsoft.com<br>portal.fei.amsub0302.manage.microsoft.com<br>m.fei.amsub0302.manage.microsoft.com<br>portal.fei.amsub0502.manage.microsoft.com<br>m.fei.amsub0502.manage.microsoft.com<br>portal.fei.amsub0601.manage.microsoft.com<br>m.fei.amsub0601.manage.microsoft.com|52.138.193.149<br>51.144.161.187|
|portal.fei.msuc01.manage.microsoft.com <br>m.fei.msuc01.manage.microsoft.com<br>portal.fei.msuc02.manage.microsoft.com <br>m.fei.msuc02.manage.microsoft.com<br>portal.fei.msuc03.manage.microsoft.com <br>m.fei.msuc03.manage.microsoft.com<br>portal.fei.msuc05.manage.microsoft.com <br>m.fei.msuc05.manage.microsoft.com|52.175.12.209<br>20.188.107.228|
|portal.fei.amsud0101.manage.microsoft.com<br>m.fei.amsud0101.manage.microsoft.com|13.72.226.202|
|fef.msua02.manage.microsoft.com|52.177.194.236|
|fef.msua04.manage.microsoft.com|23.96.112.28|
|fef.msua06.manage.microsoft.com|13.78.185.97|
|fef.msuc03.manage.microsoft.com|23.101.0.100|
|fef.amsua0502.manage.microsoft.com|13.85.68.142|
|fef.amsua0602.manage.microsoft.com|52.161.28.64|
|Admin.manage.microsoft.com|52.224.221.227<br>52.161.162.117<br>52.178.44.195<br>52.138.206.56<br>52.230.21.208<br>13.75.125.10|
|wip.mam.manage.microsoft.com|52.187.76.84<br>13.76.5.121<br>52.165.160.237<br>40.86.82.163<br>52.233.168.142<br>168.63.101.57<br>52.187.196.98<br>52.237.196.51|
|mam.manage.microsoft.com|104.40.69.125<br>13.90.192.78<br>40.85.174.177<br>40.85.77.31<br>137.116.229.43<br>52.163.215.232<br>52.174.102.180<br>52.187.196.173<br>52.156.162.48|
|*.manage.microsoft.com|40.82.248.224/28<br>20.189.105.0/24<br>20.37.153.0/24<br>20.37.192.128/25<br>20.38.81.0/24<br>20.41.1.0/24<br>20.42.1.0/24<br>20.42.130.0/24<br>20.42.224.128/25<br>20.43.129.0/24<br>40.119.8.128/25<br>40.74.25.0/24<br>40.82.249.128/25<br>40.80.184.128/25<br>52.150.137.0/25|


## <a name="network-requirements-for-powershell-scripts-and-win32-apps"></a>Netzwerkanforderungen für PowerShell-Skripts und Win32-Apps  

Wenn Sie Intune zum Bereitstellen von PowerShell-Skripts oder Win32-Apps verwenden, müssen Sie auch Zugriff auf Endpunkte gewähren, in denen sich Ihr Mandant derzeit befindet.

|ASU | Speichername | CDN |
| --- | --- |--- |
|AMSUA0601<br>AMSUA0602<br>AMSUA0101<br>AMSUA0102<br>AMSUA0201<br>AMSUA0202<br>AMSUA0401<br>AMSUA0402<br>AMSUA0501<br>AMSUA0502<br>AMSUA0701<br>AMSUA0702 | naprodimedatapri<br>naprodimedatasec<br>naprodimedatahotfix | naprodimedatapri.azureedge.net<br>naprodimedatasec.azureedge.net<br>naprodimedatahotfix.azureedge.net |
| AMSUB0101<br>AMSUB0102<br>AMSUB0201<br>AMSUB0202<br>AMSUB0301<br>AMSUB0302<br>AMSUB0501<br>AMSUB0502 | euprodimedatapri<br>euprodimedatasec<br>euprodimedatahotfix | euprodimedatapri.azureedge.net<br>euprodimedatasec.azureedge.net<br>euprodimedatahotfix.azureedge.net |
| AMSUC0101<br>AMSUC0201<br>AMSUC0301<br>AMSUC0501<br>AMSUD0101| approdimedatapri<br>approdimedatasec<br>approdimedatahotifx | approdimedatapri.azureedge.net<br>approdimedatasec.azureedge.net<br>approdimedatahotfix.azureedge.net |

## <a name="windows-push-notification-services-wns"></a>Windows-Pushbenachrichtigungsdienste (WNS)  

Bei von Intune verwalteten Windows-Geräten, die mithilfe von mobiler Geräteverwaltung (Mobile Device Management, MDM) verwaltet werden, müssen für Geräteaktionen und andere sofortige Aktivitäten die Windows-Pushbenachrichtigungsdienste (Windows Push Notification Services, WNS) verwendet werden. Weitere Informationen finden Sie unter [Zulassen von Windows Notification-Datenverkehr durch Unternehmensfirewalls](/windows/uwp/design/shell/tiles-and-notifications/firewall-allowlist-config).  

## <a name="delivery-optimization-port-requirements"></a>Übermittlungsoptimierung bei Portanforderungen  

### <a name="port-requirements"></a>Portanforderungen  

Bei Peer-zu-Peer-Datenverkehr verwendet die Übermittlungsoptimierung 7680 für TCP/IP oder 3544 für NAT-Traversal (optional Teredo). Für die Client-Dienst-Kommunikation verwendet sie HTTP oder HTTPS über Port 80/443.

### <a name="proxy-requirements"></a>Proxyanforderungen  

Um die Übermittlungsoptimierung nutzen zu können, müssen Sie Bytebereichsanforderungen zulassen. Weitere Informationen finden Sie unter [Proxyanforderungen für Windows Update](/windows/deployment/update/windows-update-troubleshooting).

### <a name="firewall-requirements"></a>Firewallanforderungen  

Lassen Sie die folgenden Hostnamen durch Ihre Firewall zur Unterstützung der Übermittlungsoptimierung zu.
Für die Kommunikation zwischen Clients und dem Clouddienst zur Übermittlungsoptimierung:
- \*.do.dsp.mp.microsoft.com

Für Metadaten für die Übermittlungsoptimierung:
- \*.dl.delivery.mp.microsoft.com
- \*.emdl.ws.microsoft.com

## <a name="apple-device-network-information"></a>Informationen zum Netzwerk von Apple-Geräten  

|Verwendet für|Hostname (IP-Adresse/-Subnetz)|Protokoll|Port|
|-----|--------|------|-------|
|Abrufen und Anzeigen von Inhalten von Apple-Servern|itunes.apple.com<br>\*.itunes.apple.com<br>\*.mzstatic.com<br>\*.phobos.apple.com<br> \*.phobos.itunes-apple.com.akadns.net |    HTTP    |      80      |
|Kommunikation mit APNs-Servern|#-courier.push.apple.com<br># ist eine zufällige Zahl zwischen 0 und 50.|    TCP     |  5223 und 443  |
|Verschiedene Funktionen, z.B. Zugriff auf das Internet, den iTunes Store, den Mac App Store, iCloud, Messaging usw. |phobos.apple.com<br>ocsp.apple.com<br>ax.itunes.apple.com<br>ax.itunes.apple.com.edgesuite.net| HTTP/HTTPS |  80 oder 443   |

Weitere Informationen finden Sie in den Apple-Artikeln [Von Apple-Softwareprodukten verwendete TCP- und UDP-Ports](https://support.apple.com/HT202944), [Informationen zu macOS-, iOS- und iTunes-Server-Hostverbindungen und iTunes-Hintergrundprozessen](https://support.apple.com/HT201999) und [Wenn Ihre macOS- und iOS-Clients keine Apple Push-Benachrichtigungen empfangen](https://support.apple.com/HT203609).  

## <a name="android-port-information"></a>Android-Portinformationen

Je nachdem, wie Sie Android-Geräte verwalten möchten, müssen Sie möglicherweise Google Android Enterprise-Ports öffnen und/oder Android-Pushbenachrichtigungen aktivieren. Weitere Informationen zu den unterstützten Verwaltungsmethoden für Android finden Sie in der [Dokumentation zur Android-Registrierung](../enrollment/android-enroll.md). 

> [!NOTE]
> Da Google Mobile Services in China nicht verfügbar ist, können von Intune verwaltete Geräte in China keine Features nutzen, die Google Mobile Services erfordern. Zu diesen Funktionen gehören: Google Play Protect-Funktionen wie der SafetyNet-Gerätenachweis, die Verwaltung von Apps über den Google Play Store und Android Enterprise-Funktionen (siehe diese [Google-Dokumentation](https://support.google.com/work/android/answer/6270910)). Darüber hinaus erfolgt die Kommunikation mit dem Microsoft Intune-Dienst in der Intune Unternehmensportal-App für Android über Google Mobile Services. Da Google Play-Dienste in China nicht verfügbar sind, kann es bis zu 8 Stunden dauern, bis einige Aufgaben abgeschlossen sind. Weitere Informationen finden Sie in [diesem Artikel](../apps/manage-without-gms.md#limitations-of-intune-device-administrator-management-when-gms-is-unavailable).

### <a name="google-android-enterprise"></a>Google Android Enterprise 

Google stellt Dokumentationen zu erforderlichen Netzwerkports und Zielhostnamen unter [Android Enterprise Bluebook](https://static.googleusercontent.com/media/www.android.com/en//static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf) im Abschnitt **Firewall** bereit. 

### <a name="android-push-notification"></a>Android-Pushbenachrichtigungen

Intune nutzt Google Firebase Cloud Messaging (FCM) für Pushbenachrichtigungen, um Geräteaktionen und Check-Ins auszulösen. Dies ist für Android-Geräteadministrator und Android Enterprise erforderlich. Informationen zu den FCM-Netzwerkanforderungen finden Sie unter [FCM-Ports und Ihre Firewall](https://firebase.google.com/docs/cloud-messaging/concept-options#messaging-ports-and-your-firewall).

## <a name="endpoint-analytics"></a>Endpunktanalyse

Weitere Informationen zu den erforderlichen Endpunkten für die Endpunktanalyse finden Sie unter [Proxykonfiguration](../../analytics/troubleshoot.md#bkmk_endpoints).