---
title: Aktivieren der Datenfreigabe
titleSuffix: Configuration Manager
description: Dieser Artikel ist ein allgemeiner Leitfaden zum Teilen von Diagnosedaten mit Desktop Analytics.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: be680198-4cea-4378-a686-d52f382ba483
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c7610b0e60f3ea02918c9dd98858a3b2bfd7c712
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708198"
---
# <a name="enable-data-sharing-for-desktop-analytics"></a>Aktivieren der Datenfreigabe für Desktop Analytics

Zum Registrieren von Geräten bei Desktop Analytics müssen sie Diagnosedaten an Microsoft senden. Wenn in Ihrer Umgebung ein Proxyserver verwendet wird, orientieren Sie sich beim Konfigurieren des Proxys an diesen Informationen.

## <a name="diagnostic-data-levels"></a>Diagnosedatenebenen

![Diagramm der Diagnosedatenebenen für Desktop Analytics](media/diagnostic-data-levels.png)

Wenn Sie Configuration Manager in Desktop Analytics integrieren, verwenden Sie den Dienst auch zum Verwalten der Diagnosedatenebene auf Geräten. Verwenden Sie Configuration Manager, um eine optimale Leistung zu erzielen.

> [!Important]  
> In den meisten Fällen konfigurieren Sie diese Einstellungen ausschließlich mit Configuration Manager. Wenden Sie diese Einstellungen nicht gleichzeitig in Domänen-Gruppenrichtlinienobjekten an. Weitere Informationen finden Sie unter [Konfliktauflösung](enroll-devices.md#conflict-resolution).

Die grundlegende Funktionalität von Desktop Analytics ist auf die [Diagnosedatenebene](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#diagnostic-data-levels) **Einfach** festgelegt. Wenn Sie in Configuration Manager nicht die Ebene **Erweitert (begrenzt)** konfigurieren, stehen die folgenden Features in Desktop Analytics nicht zur Verfügung:

- App-Nutzung
- [Zusätzliche App-Erkenntnisse](compat-assessment.md#additional-insights)
- Daten zum Bereitstellungsstatus
- Systemüberwachungsdaten

Microsoft empfiehlt, dass Sie die Diagnosedatenebene **Erweitert (begrenzt)** für Desktop Analytics aktivieren, um eine optimale Leistung des Diensts zu erzielen.

> [!Tip]
> Die Einstellung **Erweitert (begrenzt)** in Configuration Manager entspricht der Richtlinieneinstellung **Hiermit werden die erweiterten Diagnosedaten auf das für Windows Analytics erforderliche Mindestmaß eingeschränkt**, die auf Geräten unter Windows 10, Version 1709 und höher verfügbar ist.
>
> Auf Geräten unter Windows 10, Version 1703 und früher, Windows 8.1 und Windows 7 ist diese Richtlinieneinstellung nicht vorhanden. Wenn Sie die Einstellung **Erweitert (begrenzt)** in Configuration Manager konfigurieren, erfolgt ein Fallback der betreffenden Geräte auf die Ebene **Einfach**.
>
> Diese Richtlinieneinstellung ist auf Geräten unter Windows 10, Version 1709 vorhanden. Wenn Sie jedoch die Einstellung **Erweitert (begrenzt)** in Configuration Manager konfigurieren, erfolgt auch für diese Geräte ein Fallback auf die Ebene **Einfach**.

Weitere Informationen zu Diagnosedaten, die mit der Einstellung **Erweitert (begrenzt)** mit Windows geteilt werden, finden Sie unter [Erweiterte Windows 10-Diagnosedatenereignisse und Felder, die von Windows Analytics verwendet werden](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields).

> [!Important]
> Microsoft ist bestrebt, Ihnen Tools und Ressourcen zur Verfügung zu stellen, mit denen Sie die Kontrolle über Ihre Privatsphäre erlangen. Daher werden von Desktop Analytics zwar Windows 8.1-Geräte unterstützt, Microsoft erfasst jedoch keine Windows-Diagnosedaten von Windows 8.1-Geräten, die sich in europäischen Ländern (EWR und Schweiz) befinden.

Weitere Informationen finden Sie unter [Desktop Analytics – Datenschutz](privacy.md).

Auch anhand der folgenden Artikel können Sie ein besseres Verständnis der Windows-Diagnosedatenebenen erlangen:

- [Windows und die DSGVO: Informationen für IT-Administratoren und Entscheidungsträger](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [Konfigurieren von Windows-Diagnosedaten in Ihrer Organisation](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

> [!Note]  
> Clients, für deren Diagnosedaten die Einstellung „Erweitert (begrenzt)“ festgelegt ist, senden bei der anfänglichen vollständigen Überprüfung ca. 2 MB Daten an die Microsoft-Cloud. Das tägliche Delta schwankt zwischen 250 und 400 KB.
>
> Die tägliche Delta-Überprüfung erfolgt um 03:00 Uhr (Ortszeit des Geräts). Einige Ereignisse werden bei erster Verfügbarkeit im Verlauf des Tages gesendet. Diese Zeiten können nicht konfiguriert werden.
>
> Weitere Informationen finden Sie unter [Konfigurieren von Windows-Diagnosedaten in Ihrer Organisation](https://aka.ms/enterprisetelemetry).  

## <a name="endpoints"></a>Endpunkte

Konfigurieren Sie zum Aktivieren der Datenfreigabe den Proxyserver so, dass die folgenden Internetendpunkte zulässig sind.

> [!Important]  
> Aus Gründen des Datenschutzes und der Datenintegrität führt Windows bei der Kommunikation mit den Diagnosedatenendpunkten eine Prüfung auf ein Microsoft SSL-Zertifikat (Anheften von Zertifikaten) aus. SSL-Abfangen und -Untersuchung sind somit nicht möglich. Um Desktop Analytics nutzen zu können, müssen Sie diese Endpunkte aus der SSL-Untersuchung ausschließen.<!-- BUG 4647542 -->

Seit Version 2002 gilt Folgendes: Wenn die Verbindung des Configuration Manager-Standorts mit den erforderlichen Endpunkten für einen Clouddienst nicht hergestellt werden kann, wird eine kritische Statusmeldung mit der ID 11488 ausgegeben. Wenn keine Verbindung mit dem Dienst hergestellt werden kann, wird der Status der Komponente „SMS_SERVICE_CONNECTOR“ in „kritisch“ geändert. Zeigen Sie detaillierte Statusinformationen im Knoten [Komponentenstatus](../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) in der Configuration Manager-Konsole an.<!-- 5566763 -->

### <a name="server-connectivity-endpoints"></a>Serverkonnektivitäts-Endpunkte

Der Dienstverbindungspunkt muss mit den folgenden Endpunkten kommunizieren:

| Endpunkt  | Funktion  |
|-----------|-----------|
| `https://aka.ms` | Zum Suchen des Diensts |
| `https://graph.windows.net` | Wird beim Anfügen Ihrer Hierarchie an Desktop Analytics (für Configuration Manager-Serverrolle) zum automatischen Abrufen von Einstellungen wie CommercialId verwendet. Weitere Informationen finden Sie unter [Konfigurieren des Proxys für einen Standortsystemserver](../core/plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Wird zum Synchronisieren der Mitgliedschaften von Gerätesammlungen, von Bereitschaftsplänen und des Bereitschaftsstatus von Geräten mit Desktop Analytics verwendet (nur für Configuration Manager-Serverrolle). Weitere Informationen finden Sie unter [Konfigurieren des Proxys für einen Standortsystemserver](../core/plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |

### <a name="user-experience-and-diagnostic-component-endpoints"></a>Endpunkte für Benutzerfreundlichkeit und Diagnosekomponenten

Clientgeräte müssen mit den folgenden Endpunkten kommunizieren:

| Endpunkt  | Funktion  |
|-----------|-----------|
| `https://v10c.events.data.microsoft.com` | Endpunkt für Benutzererfahrung im verbundenen Modus und Diagnosekomponenten. Wird von Geräten unter Windows 10, Version 1809 oder höher oder Version 1803 mit einer Installation des kumulativen Updates 2018-09 oder höher verwendet. |
| `https://v10.events.data.microsoft.com` | Endpunkt für Benutzererfahrung im verbundenen Modus und Diagnosekomponenten. Wird von Geräten unter Windows 10, Version 1803 _ohne_ Installation des kumulativen Updates 2018-09 verwendet. |
| `https://v10.vortex-win.data.microsoft.com` | Endpunkt für Benutzererfahrung im verbundenen Modus und Diagnosekomponenten. Wird von Geräten unter Windows 10, Version 1709 oder früher verwendet. |
| `https://vortex-win.data.microsoft.com` | Endpunkt für Benutzererfahrung im verbundenen Modus und Diagnosekomponenten. Wird von Geräten unter Windows 7 und Windows 8.1 verwendet. |

### <a name="client-connectivity-endpoints"></a>Clientkonnektivitäts-Endpunkte

Clientgeräte müssen mit den folgenden Endpunkten kommunizieren:

| Index | Endpunkt  | Funktion  |
|-------|-----------|-----------|
| 1 | `https://settings-win.data.microsoft.com` | Ermöglicht dem Kompatibilitätsupdate das Senden von Daten an Microsoft. |
| 2 | `http://adl.windows.com` | Ermöglicht dem Kompatibilitätsupdate das Empfangen der neuesten Kompatibilitätsdaten von Microsoft. |
| 3 | `https://watson.telemetry.microsoft.com` | [Windows-Fehlerberichterstattung (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Erforderlich zum Überwachen der Bereitstellungsintegrität in Windows 10, Version 1803 oder früher. |
| 4 | `https://umwatsonc.events.data.microsoft.com` | [Windows-Fehlerberichterstattung (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Erforderlich für Berichte über die Geräteintegrität in Windows 10, Version 1809 oder höher. |
| 5 | `https://ceuswatcab01.blob.core.windows.net` | [Windows-Fehlerberichterstattung (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Erforderlich zum Überwachen der Bereitstellungsintegrität in Windows 10, Version 1809 oder später. |
| 6 | `https://ceuswatcab02.blob.core.windows.net` | [Windows-Fehlerberichterstattung (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Erforderlich zum Überwachen der Bereitstellungsintegrität in Windows 10, Version 1809 oder später. |
| 7 | `https://eaus2watcab01.blob.core.windows.net` | [Windows-Fehlerberichterstattung (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Erforderlich zum Überwachen der Bereitstellungsintegrität in Windows 10, Version 1809 oder später. |
| 8 | `https://eaus2watcab02.blob.core.windows.net` | [Windows-Fehlerberichterstattung (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Erforderlich zum Überwachen der Bereitstellungsintegrität in Windows 10, Version 1809 oder später. |
| 9 | `https://weus2watcab01.blob.core.windows.net` | [Windows-Fehlerberichterstattung (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Erforderlich zum Überwachen der Bereitstellungsintegrität in Windows 10, Version 1809 oder später. |
| 10 | `https://weus2watcab02.blob.core.windows.net` | [Windows-Fehlerberichterstattung (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Erforderlich zum Überwachen der Bereitstellungsintegrität in Windows 10, Version 1809 oder später. |
| 11 | `https://kmwatsonc.events.data.microsoft.com` | [OCA (Online Crash Analysis)](https://docs.microsoft.com/windows/win32/dxtecharts/crash-dump-analysis). Erforderlich für Berichte über die Geräteintegrität in Windows 10, Version 1809 oder höher. |
| 12 | `https://oca.telemetry.microsoft.com`  | [OCA (Online Crash Analysis)](https://docs.microsoft.com/windows/win32/dxtecharts/crash-dump-analysis). Erforderlich zum Überwachen der Bereitstellungsintegrität in Windows 10, Version 1803 oder früher. |
| 13 | `https://login.live.com` | Erforderlich zum Bereitstellen einer zuverlässigeren Geräteidentität für Desktop Analytics. <br> <br>Verwenden Sie Richtlinieneinstellungen, anstatt diesen Endpunkt zu blockieren, um den Zugriff auf Endbenutzer-Microsoft-Konten zu deaktivieren. Weitere Informationen finden Sie unter [Das Microsoft-Konto im Unternehmen](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication). |
| 14 | `https://v20.events.data.microsoft.com` | Endpunkt für Benutzererfahrung im verbundenen Modus und Diagnosekomponenten. |

## <a name="proxy-server-authentication"></a>Proxyserverauthentifizierung

Wenn Ihr Unternehmen die Proxyserverauthentifizierung für den Internetzugriff verwendet, stellen Sie sicher, dass die Diagnosedaten nicht aufgrund der Authentifizierung blockiert werden. Wenn Ihr Proxy es nicht zulässt, dass Geräte diese Daten senden, werden sie in Desktop Analytics nicht angezeigt.

### <a name="bypass-recommended"></a>Umgehung (empfohlen)

Konfigurieren Sie die Proxyserver so, dass keine Proxyauthentifizierung für den Datenverkehr zu den Diagnosedaten-Endpunkten erforderlich ist. Diese Option ist die umfassendste Lösung. Sie funktioniert für alle Windows 10-Versionen.  

### <a name="user-proxy-authentication"></a>Benutzerproxyauthentifizierung

Konfigurieren Sie die Geräte so, dass der Kontext des angemeldeten Benutzers für die Proxyauthentifizierung verwendet wird. Für diese Methode werden die folgenden Konfigurationen benötigt:

- Die Geräte verfügen über das aktuelle Qualitätsupdate für eine unterstützte Version von Windows

- Konfigurieren Sie in der Gruppe „Netzwerk und Internet“ der Windows-Einstellungen in **Proxyeinstellungen** den Proxy auf Benutzerebene (WinINET-Proxy). Sie können auch „Internetoptionen“ in der Legacy-Systemsteuerung verwenden.

- Stellen Sie sicher, dass die Benutzer über die Proxyberechtigung für den Zugriff auf die Diagnosedaten-Endpunkte verfügen. Für diese Option müssen die Geräte über Konsolenbenutzer mit Proxyberechtigungen verfügen; daher können Sie diese Methode nicht auf monitorlosen Geräten verwenden.

> [!IMPORTANT]
> Die Benutzerproxyauthentifizierung ist inkompatibel mit der Verwendung von Microsoft Defender Advanced Threat Protection. Dieses Verhalten ist darauf zurückzuführen, dass bei dieser Authentifizierung der Registrierungsschlüssel **DisableEnterpriseAuthProxy** auf `0` festgelegt ist, während er für Microsoft Defender ATP auf `1` festgelegt sein muss. Weitere Informationen finden Sie unter [Konfigurieren von Computerproxy- und Internetverbindungseinstellungen in Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection).

### <a name="device-proxy-authentication"></a>Geräteproxyauthentifizierung

Dieser Ansatz unterstützt folgende Szenarien:

- Monitorlose Geräte, bei denen sich kein Benutzer anmeldet oder die Benutzer des Geräts keinen Internetzugriff haben

- Authentifizierte Proxys, die keine integrierte Windows-Authentifizierung verwenden

- Wenn Sie auch Microsoft Defender Advanced Threat Protection verwenden

Dies ist der Ansatz mit der höchsten Komplexität, da er die folgenden Konfigurationen erfordert:

- Stellen Sie sicher, dass die Geräte über WinHTTP im lokalen Systemkontext auf den Proxyserver zugreifen können. Verwenden Sie zum Konfigurieren dieses Verhaltens eine der folgenden Optionen:

  - Die Befehlszeile `netsh winhttp set proxy`

  - WPAD-Protokoll (Web Proxy Auto-Discovery)

  - Transparenter Proxy

  - Konfigurieren Sie den geräteweiten WinINET-Proxy unter Verwendung der folgenden Gruppenrichtlinieneinstellung: **Erstellen Sie Proxyeinstellungen pro Computer (anstatt pro Benutzer)** (ProxySettingsPerUser = `1`)

  - Geroutete Verbindung, oder Verwendung von Netzwerkadressübersetzung (Network Address Translation, NAT)

- Konfigurieren Sie Proxyserver so, dass den Computerkonten in Active Directory der Zugriff auf die Diagnosedaten-Endpunkte ermöglicht wird. Für diese Konfiguration müssen Proxyserver die integrierte Windows-Authentifizierung unterstützen.  
