---
title: Aktivieren der Datenfreigabe
titleSuffix: Configuration Manager
description: Dieser Artikel ist ein allgemeiner Leitfaden zum Teilen von Diagnosedaten mit Desktop Analytics.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: be680198-4cea-4378-a686-d52f382ba483
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 999d8441e8c97f0a4b7ad4a92c8175300dcc4ead
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696445"
---
# <a name="enable-data-sharing-for-desktop-analytics"></a>Aktivieren der Datenfreigabe für Desktop Analytics

Zum Registrieren von Geräten bei Desktop Analytics müssen sie Diagnosedaten an Microsoft senden. Wenn in Ihrer Umgebung ein Proxyserver verwendet wird, orientieren Sie sich beim Konfigurieren des Proxys an diesen Informationen.

## <a name="diagnostic-data-levels"></a>Diagnosedatenebenen

:::image type="content" source="media/diagnostic-data-levels.png" alt-text="Diagramm der Diagnosedatenebenen für Desktop Analytics":::

Wenn Sie Configuration Manager in Desktop Analytics integrieren, verwenden Sie den Dienst auch zum Verwalten der Diagnosedatenebene auf Geräten. Verwenden Sie Configuration Manager, um eine optimale Leistung zu erzielen.

> [!IMPORTANT]
> In den meisten Fällen konfigurieren Sie diese Einstellungen ausschließlich mit Configuration Manager. Wenden Sie diese Einstellungen nicht gleichzeitig in Domänen-Gruppenrichtlinienobjekten an. Weitere Informationen finden Sie unter [Konfliktauflösung](enroll-devices.md#conflict-resolution).

Die grundlegende Funktionalität von Desktop Analytics ist auf die [Diagnosedatenebene](/windows/privacy/configure-windows-diagnostic-data-in-your-organization#diagnostic-data-levels) **Erforderlich** festgelegt. Wenn Sie in Configuration Manager nicht die Ebene **Optional (begrenzt)** konfigurieren, stehen die folgenden Features in Desktop Analytics nicht zur Verfügung:

- App-Nutzung
- [Zusätzliche App-Erkenntnisse](compat-assessment.md#additional-insights)
- [Daten zum Bereitstellungsstatus](deploy-prod.md#address-deployment-alerts)
- [Systemüberwachungsdaten](health-status-monitoring.md)

Microsoft empfiehlt die Aktivierung der Diagnosedatenebene **Optional (begrenzt)** für Desktop Analytics, damit Sie optimal von diesem Dienst profitieren.

> [!TIP]
> Die Einstellung **Optional (begrenzt)** in Configuration Manager entspricht der Richtlinieneinstellung **Erweiterte Diagnosedaten auf das für Windows Analytics erforderliche Mindestmaß beschränken**, die auf Geräten unter Windows 10, Version 1709 und höher, verfügbar ist.
>
> Auf Geräten unter Windows 10, Version 1703 und früher, Windows 8.1 und Windows 7 ist diese Richtlinieneinstellung nicht vorhanden. Wenn Sie die Einstellung **Optional (begrenzt)** in Configuration Manager konfigurieren, erfolgt ein Fallback der betreffenden Geräte auf die Ebene **Erforderlich**.
>
> Diese Richtlinieneinstellung ist auf Geräten unter Windows 10, Version 1709 vorhanden. Wenn Sie jedoch die Einstellung **Optional (begrenzt)** in Configuration Manager konfigurieren, erfolgt auch für diese Geräte ein Fallback auf die Ebene **Erforderlich**.
>
> In Configuration Manager, Version 2002 und früher, hatten die Einstellungen andere Namen:<!-- 7363467 -->
>
> | Version 2006 und höher | Version 2002 und früher |
> |---------|---------|
> | Erforderlich | Basic |
> | Optional (begrenzt) | Erweitert (begrenzt) |
> | Nicht zutreffend | Verbessert |
> | Optional | Vollständig |
>
> Wenn Sie zuvor Geräte auf der Ebene **Erweitert** konfiguriert haben, werden diese bei einem Upgrade auf Version 2006 auf **Optional (begrenzt)** zurückgesetzt. Dadurch senden diese Geräte weniger Daten an Microsoft. Diese Änderung sollte keine Auswirkungen auf die in Desktop Analytics angezeigten Informationen haben.

Weitere Informationen zu Diagnosedaten, die mit der Einstellung **Optional (begrenzt)** an Microsoft übermittelt werden, finden Sie unter [Windows 10-Diagnosedatenereignisse und -felder, die über die Richtlinie zum Einschränken erweiterter Diagnosedaten erfasst werden](/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields).

> [!IMPORTANT]
> Microsoft ist bestrebt, Ihnen Tools und Ressourcen zur Verfügung zu stellen, mit denen Sie die Kontrolle über Ihre Privatsphäre erlangen. Daher werden von Desktop Analytics zwar Windows 8.1-Geräte unterstützt, Microsoft erfasst jedoch keine Windows-Diagnosedaten von Windows 8.1-Geräten, die sich in europäischen Ländern (EWR und Schweiz) befinden.

Weitere Informationen finden Sie unter [Desktop Analytics – Datenschutz](privacy.md).

Auch anhand der folgenden Artikel können Sie ein besseres Verständnis der Windows-Diagnosedatenebenen erlangen:

- [Windows und die DSGVO: Informationen für IT-Administratoren und Entscheidungsträger](/windows/privacy/gdpr-it-guidance)  

- [Konfigurieren von Windows-Diagnosedaten in Ihrer Organisation](/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

> [!NOTE]
> Clients, die für das Senden von Diagnosedaten auf der Ebene **Optional (begrenzt)** konfiguriert sind, senden bei der anfänglichen vollständigen Überprüfung ca. 2 MB Daten an die Microsoft-Cloud. Das tägliche Delta schwankt zwischen 250 und 400 KB.
>
> Die tägliche Delta-Überprüfung erfolgt um 03:00 Uhr (Ortszeit des Geräts). Einige Ereignisse werden bei erster Verfügbarkeit im Verlauf des Tages gesendet. Diese Zeiten können nicht konfiguriert werden.
>
> Weitere Informationen finden Sie unter [Konfigurieren von Windows-Diagnosedaten in Ihrer Organisation](https://aka.ms/enterprisetelemetry).  

## <a name="endpoints"></a>Endpunkte

Konfigurieren Sie zum Aktivieren der Datenfreigabe den Proxyserver so, dass die folgenden Internetendpunkte zulässig sind.

> [!IMPORTANT]
> Aus Gründen des Datenschutzes und der Datenintegrität führt Windows bei der Kommunikation mit den Diagnosedatenendpunkten eine Prüfung auf ein Microsoft SSL-Zertifikat (Anheften von Zertifikaten) aus. SSL-Abfangen und -Untersuchung sind somit nicht möglich. Um Desktop Analytics nutzen zu können, müssen Sie diese Endpunkte aus der SSL-Untersuchung ausschließen.<!-- BUG 4647542 -->

Seit Version 2002 gilt Folgendes: Wenn die Verbindung des Configuration Manager-Standorts mit den erforderlichen Endpunkten für einen Clouddienst nicht hergestellt werden kann, wird eine kritische Statusmeldung mit der ID 11488 ausgegeben. Wenn keine Verbindung mit dem Dienst hergestellt werden kann, wird der Status der Komponente „SMS_SERVICE_CONNECTOR“ in „kritisch“ geändert. Zeigen Sie detaillierte Statusinformationen im Knoten [Komponentenstatus](../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) in der Configuration Manager-Konsole an.<!-- 5566763 -->

> [!NOTE]
> Weitere Informationen zum IP-Adressbereich von Microsoft finden Sie unter [Microsoft Public IP Space](https://www.microsoft.com/download/details.aspx?id=53602) (Öffentlicher IP-Adressraum von Microsoft). Diese Adressen werden regelmäßig aktualisiert. Es gibt keine dienstspezifische Granularität, alle IP-Adressen in diesen Bereichen können verwendet werden.

[!INCLUDE [Internet endpoints for Desktop Analytics](../core/plan-design/network/includes/internet-endpoints-desktop-analytics.md)]

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
> Die Benutzerproxyauthentifizierung ist inkompatibel mit der Verwendung von Microsoft Defender Advanced Threat Protection. Dieses Verhalten ist darauf zurückzuführen, dass bei dieser Authentifizierung der Registrierungsschlüssel **DisableEnterpriseAuthProxy** auf `0` festgelegt ist, während er für Microsoft Defender ATP auf `1` festgelegt sein muss. Weitere Informationen finden Sie unter [Konfigurieren von Computerproxy- und Internetverbindungseinstellungen in Microsoft Defender ATP](/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection).

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