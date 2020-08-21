---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: ca735cde1da5d563b9a7772fdaa55834e307312e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125945"
---
### <a name="server-connectivity-endpoints"></a>Serverkonnektivitäts-Endpunkte

Der Dienstverbindungspunkt muss mit den folgenden Endpunkten kommunizieren:

| Endpunkt  | Funktion  |
|-----------|-----------|
| `https://aka.ms` | Zum Suchen des Diensts |
| `https://graph.windows.net` | Wird beim Anfügen Ihrer Hierarchie an Desktop Analytics (für Configuration Manager-Serverrolle) zum automatischen Abrufen von Einstellungen wie CommercialId verwendet. Weitere Informationen finden Sie unter [Konfigurieren des Proxys für einen Standortsystemserver](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Wird zum Synchronisieren der Mitgliedschaften von Gerätesammlungen, von Bereitschaftsplänen und des Bereitschaftsstatus von Geräten mit Desktop Analytics verwendet (nur für Configuration Manager-Serverrolle). Weitere Informationen finden Sie unter [Konfigurieren des Proxys für einen Standortsystemserver](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://dc.services.visualstudio.com` | Für Diagnosedaten vom lokalen Dienstconnector, um Erkenntnisse über die Integrität von mit der Cloud verbundenen Diensten zu gewinnen.<!--7541816--> |

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
