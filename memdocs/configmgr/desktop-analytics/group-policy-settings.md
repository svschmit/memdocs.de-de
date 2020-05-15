---
title: Gruppenrichtlinieneinstellungen
titleSuffix: Configuration Manager
description: Verstehen der lokalen und Gruppenrichtlinieneinstellungen in Windows, die von Configuration Manager und Desktop Analytics verwendet werden
ms.date: 04/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 004ca404-e6fa-47f0-ae77-e44e18a08b33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 8251e21c7eccb87b764af75e883018bdc894ca37
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268673"
---
# <a name="group-policy-settings-for-desktop-analytics"></a>Gruppenrichtlinieneinstellungen für Desktop Analytics

*Gilt für: Configuration Manager (Current Branch)*

In diesem Artikel werden die lokalen und Gruppenrichtlinieneinstellungen in Windows beschrieben, die von Configuration Manager und Desktop Analytics verwendet werden.

Wenn Configuration Manager Geräte in Desktop Analytics registriert, legt es Windows-Richtlinien fest, um das Gerät zu konfigurieren. In den meisten Fällen konfigurieren Sie diese Einstellungen ausschließlich mit Configuration Manager.

## <a name="windows-settings"></a>Windows-Einstellungen

Configuration Manager legt Windows-Richtlinien in einem oder beiden der folgenden Registrierungsschlüssel fest:

- Gruppenrichtlinienobjekt (**GPO**): `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

- Einstellung für **Lokale** Richtlinie: `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`

| Richtlinie | Pfad | Gilt für | Wert |
|--------|------|------------|-------|
| **CommercialId** | Lokal | Alle Windows-Versionen | Damit ein Gerät in Desktop Analytics aufgeführt wird, müssen Sie es mit der kommerziellen ID Ihrer Organisation konfigurieren. |
| **AllowTelemetry**  | GPO | Windows 10 | Legen Sie `1` für Diagnosedaten der Ebene **Einfach**, `2` für **Erweitert** oder `3` für **Vollständig** fest. Für Desktop Analytics sind mindestens grundlegende Diagnosedaten erforderlich. Microsoft empfiehlt, dass Sie für Desktop Analytics die Ebene „Erweitert (begrenzt)“ verwenden. Weitere Informationen finden Sie unter [Konfigurieren von Windows-Diagnosedaten in Ihrer Organisation](https://docs.microsoft.com/windows/configuration/configure-windows-diagnostic-data-in-your-organization). |
| **LimitEnhancedDiagnosticDataWindowsAnalytics** | GPO | Windows 10, Version 1803 und höher | Diese Einstellung gilt nur, wenn die Einstellung für AllowTelemetry gleich `2` ist. Sie begrenzt die an Microsoft gesendeten erweiterten Diagnosedatenereignisse auf die Ereignisse, die von Desktop Analytics benötigt werden. Weitere Informationen finden Sie unter [Erweiterte Windows 10-Diagnosedatenereignisse und Felder, die von Windows Analytics verwendet werden](https://docs.microsoft.com/windows/configuration/enhanced-diagnostic-data-windows-analytics-events-and-fields). |
| **AllowDeviceNameInTelemetry** | GPO | Windows 10, Version 1803 und höher | Aktivieren Sie für Geräte das Senden des Gerätenamens. Der Gerätename wird standardmäßig nicht an Microsoft gesendet. Wenn Sie den Gerätenamen nicht senden, wird dieser in Desktop Analytics als „Unbekannt“ angezeigt. Weitere Informationen finden Sie unter [Gerätename](enroll-devices.md#device-name). |
| **CommercialDataOptIn** | Lokal | Windows 8.1 und früher | Für Desktop Analytics ist ein Wert von `1` erforderlich. Weitere Informationen finden Sie unter [Commercial Data Opt-in in Windows 7](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/ee126127\(v=ws.10\)) (Aktivierung von kommerziellen Daten). |
| **RequestAllAppraiserVersions** | Beide | Windows 8.1 und früher | Desktop Analytics benötigt einen Wert von `1`, damit die Datensammlung ordnungsgemäß funktioniert. |
| **DisableEnterpriseAuthProxy** | GPO | Alle Windows-Versionen | Wenn Ihre Umgebung einen benutzerauthentifizierten Proxy mit integrierter Windows-Authentifizierung für den Internetzugriff erfordert, benötigt Desktop Analytics einen Wert von `0`, damit die Datensammlung ordnungsgemäß funktioniert. Weitere Informationen finden Sie unter [Proxyserverauthentifizierung](enable-data-sharing.md#proxy-server-authentication). |

> [!IMPORTANT]
> In den meisten Fällen konfigurieren Sie diese Einstellungen ausschließlich mit Configuration Manager. Wenden Sie diese Einstellungen nicht gleichzeitig in Domänen-Gruppenrichtlinienobjekten an. Weitere Informationen finden Sie unter [Konfliktauflösung](enroll-devices.md#conflict-resolution).

### <a name="settings-from-upgrade-readiness"></a>Einstellungen der Upgradebereitschaft

Windows Analytics legt außerdem die folgenden Richtlinien über das Skript für die Upgradebereitschaft fest:

- CommercialId
- AllowDeviceNameInTelemetry
- CommercialDataOptIn
- RequestAllAppraiserVersions

Wenn Sie das Onboardingskript für die Upgradebereitschaft auf einem Gerät ausgeführt haben, sind diese Richtlinieneinstellungen möglicherweise noch vorhanden. Verwenden Sie nicht das Legacyskript. Bevor Sie das Gerät bei Desktop Analytics registrieren, entfernen Sie diese früheren Richtlinieneinstellungen.

## <a name="group-policy-settings"></a>Gruppenrichtlinieneinstellungen

Im Allgemeinen verwenden Sie Configuration Manager-Sammlungen, um Desktop Analytics-Einstellungen und -Registrierung zu steuern. Verwenden Sie direkte Mitgliedschaften oder Abfragen, um Geräte in die Sammlung einzuschließen oder aus der Sammlung auszuschließen. Weitere Informationen finden Sie unter [Erstellen von Sammlungen](../core/clients/manage/collections/create-collections.md).

Configuration Manager konfiguriert die Einstellungen für kommerzielle ID und Diagnosedaten für Ihre Zielsammlung. Wenn Sie unterschiedliche Diagnosedateneinstellungen für verschiedene Gerätegruppen konfigurieren müssen, verwenden Sie die Gruppenrichtlinieneinstellungen, um die Configuration Manager-Einstellungen außer Kraft zu setzen. Sie müssen z. B. die Stufe **Erweitert (begrenzt)** für einige Geräte und **Einfach** für andere festlegen. Einige Geräte weisen möglicherweise unterschiedliche Einstellungen für die [Proxyserverauthentifizierung](enable-data-sharing.md#proxy-server-authentication) auf.

Die relevanten Gruppenrichtlinieneinstellungen befinden sich in folgendem Pfad: **Computerkonfiguration** > **Administrative Vorlagen** > **Windows-Komponenten** > **Datensammlung und Vorabversionen**.

Gruppenrichtlinieneinstellungen ändern nur Registrierungseinstellungen im folgenden Schlüssel: `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

> [!IMPORTANT]
> Wenn Sie Gruppenrichtlinieneinstellungen verwenden, um komplexe Szenarien zu aktivieren, achten Sie besonders auf Richtlinieneinstellungen, die Konfigurationskonflikte verursachen können. Configuration Manager konfiguriert nur die [Windows-Einstellungen](#windows-settings), *wenn der Wert noch nicht vorhanden ist*. Gruppenrichtlinieneinstellungen haben Vorrang vor Configuration Manager-Einstellungen, sodass bestimmte Gruppenrichtlinienkonfigurationen Probleme mit Desktop Analytics verursachen können.

### <a name="group-policy-settings-that-could-conflict-with-configuration-manager-settings-for-desktop-analytics"></a>Gruppenrichtlinieneinstellungen, die mit Configuration Manager-Einstellungen für Desktop Analytics in Konflikt geraten könnten

Die Gruppenrichtlinieneinstellungen in der folgenden Tabelle haben das größte Konfliktpotenzial hinsichtlich der Windows-Einstellungen, die Configuration Manager auf Geräten festlegt, die für Desktop Analytics registriert werden:

| Anzeigename | Registrierungswert | Auswirkung auf Geräte, die für Desktop Analytics registriert sind |
|--------------|----------------|-------------------------------------------------|
| **Kommerzielle ID konfigurieren** | CommercialId | Wenn Sie diese Richtlinie auf einen anderen Wert festlegen, wird die von Configuration Manager festgelegte kommerzielle ID überschrieben. Wenn es sich nicht um dieselbe ID handelt, werden konfigurierte Geräte möglicherweise nicht in Desktop Analytics angezeigt. |
| **Telemetrie zulassen** | AllowTelemetry | Wenn Sie diese Richtlinie auf einen anderen Wert festlegen, setzt sie die globale Diagnosedatenebene außer Kraft, die Sie in Configuration Manager für die Zielsammlung festgelegt haben. |
| **Erweiterte Diagnosedaten auf das für Windows Analytics erforderliche Minimum beschränken** | LimitEnhancedDiagnosticDataWindowsAnalytics | Diese Richtlinie ist abhängig von der vorherigen AllowTelemetry-Einstellung. Abhängig von der Ebene, die Sie im Configuration Manager oder mit der Gruppenrichtlinie festlegen, kann diese Richtlinie die Diagnosedatenebene auf dem Gerät in **Erweitert** oder **Erweitert (begrenzt)** ändern. Diese Richtlinie gilt nur, wenn AllowTelemetry auf `2` (**Erweitert**) festgelegt ist. |
| **Senden von Gerätenamen in Windows-Diagnosedaten zulassen** | AllowDeviceNameInTelemetry | Wenn Sie sich dafür entscheiden, Gerätenamen im Configuration Manager zu senden, können Sie diese Richtlinie durch Konfigurieren dieser Richtlinie auf „Deaktiviert“ außer Kraft setzen. Wenn Sie diese Einstellung deaktivieren, werden Gerätenamen in Desktop Analytics als „Unbekannt“ angezeigt. Weitere Informationen finden Sie unter [Gerätename](enroll-devices.md#device-name). |
| **Verwendung des authentifizierten Proxys für den Dienst „Benutzererfahrung und Telemetrie im verbundenen Modus“ konfigurieren** | DisableEnterpriseAuthProxy | Wenn Sie Configuration Manager-Geräte für die Verwendung eines benutzerauthentifizierten Proxys (`0`) konfigurieren, dann sendet das Gerät die Diagnosedaten im Systemkontext und nicht im Kontext des Benutzers, wenn Sie diese Richtlinie so konfiguriert haben, dass **die Verwendung eines authentifizierten Proxys deaktiviert wird** (`1`). Wenn Sie das Gerät nicht im Systemkontext mit einem Proxy konfigurieren oder sich das Gerät nicht beim Proxy authentifizieren kann, dann kann Windows keine Diagnosedaten an Desktop Analytics senden. |

> [!NOTE]
> Die Legacy-Richtlinie **Benutzererfahrung und Telemetrie im verbundenen Modus konfigurieren** (TelemetryProxy) ermöglicht es Windows, Diagnosedaten an einen dedizierten Proxy weiterzuleiten, anstatt den Benutzer- (WinINET) oder Geräteproxy (WinHTTP) zu verwenden. Einige Windows-Komponenten unterstützen diese Richtlinie nicht. Wenn Sie diese Richtlinie verwenden, kann dies zu Datenqualitätsproblemen in Desktop Analytics führen.

#### <a name="behavior-of-disabled-settings"></a>Verhalten von deaktivierten Einstellungen

Wenn Sie diese Gruppenrichtlinieneinstellungen auf **Deaktiviert** festlegen, hat dies unterschiedliche Auswirkungen auf das Systemverhalten.

- Wenn Sie die Richtlinie **CommercialId** deaktivieren, entfernt Windows den Registrierungswert. Die Configuration Manager-Einstellung für die kommerzielle ID, die im lokalen Richtlinienregistrierungspfad festgelegt ist, gilt dann für das Gerät.

- Bei Richtlinien, die Configuration Manager am gleichen Registrierungsort wie die Gruppenrichtlinie festlegt, entfernt Windows den Registrierungswert, wenn Sie die Einstellung in der Gruppenrichtlinie deaktivieren. Configuration Manager legt ihn beim nächsten Richtlinienverarbeitungszyklus erneut fest, und Windows entfernt ihn dann bei der nächsten Aktualisierung der Gruppenrichtlinie. Diese ständige Änderung der Konfiguration kann zu unerwünschtem Verhalten bei Desktop Analytics führen.

  - Wenn Sie diese Gruppenrichtlinieneinstellungen auf **Nicht konfiguriert** festlegen, entfernt Windows den Wert einmal, aber setzt das Entfernen nicht fort. Mit dieser Konfiguration kann Configuration Manager seine Werte wie erwartet anwenden.

### <a name="group-policy-settings-to-customize-the-user-experience"></a>Gruppenrichtlinieneinstellungen zur Anpassung der Benutzererfahrung

Diese Gruppenrichtlinieneinstellungen sind für Configuration Manager oder Desktop Analytics nicht erforderlich. Sie können sie in Gruppenrichtlinien konfigurieren, um die Erfahrung Ihrer Benutzer mit Windows-Diagnosedaten zu konfigurieren.

| Anzeigename | Registrierungswert | Auswirkung auf Geräte, die für Desktop Analytics registriert sind |
|--------------|----------------|-------------------------------------------------|
| **Änderungsbenachrichtigungen für die Telemetrieaktivierung konfigurieren** | DisableTelemetryOptInChangeNotification | Ab Windows 10, Version 1803, benachrichtigt Windows die Benutzer, wenn sich die Diagnosedatenebene ändert. Verwenden Sie diese Richtlinie, um Benachrichtigungen zu deaktivieren. |
| **Benutzeroberfläche für die Festlegung der Telemetrieaktivierung konfigurieren** | DisableTelemetryOptInSettingsUx | Beim Konfigurieren der Diagnosedatenebene legen Sie die Obergrenze für das Gerät fest. Ab Windows 10, Version 1803, können Benutzer eine niedrigere Ebene festlegen. Verwenden Sie diese Richtlinie, um zu verhindern, dass Benutzer die Diagnoseebene ändern. Weitere Informationen finden Sie unter [Konfigurieren von Windows-Diagnosedaten in Ihrer Organisation](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management). |
| **Löschen von Diagnosedaten deaktivieren** | DisableDeviceDelete | Ab Windows 10, Version 1809, können Benutzer Diagnosedaten von der Einstellungsseite für **Diagnose und Feedback** löschen. Verwenden Sie diese Richtlinie, um das Löschen von Diagnosedaten zu verhindern, die Microsoft von dem Gerät erfasst. |
| **Diagnosedaten-Viewer deaktivieren** | DisableDiagnosticDataViewer | Ab Windows 10, Version 1809, können Benutzer den Diagnosedaten-Viewer über die Einstellungsseite für **Diagnose und Feedback** aktivieren und öffnen. Verwenden Sie diese Richtlinie, um den Diagnosedaten-Viewer in den Windows-Einstellungen zu deaktivieren und zu verhindern, dass er Diagnosedaten anzeigt, die Microsoft von dem Gerät erfasst.|
