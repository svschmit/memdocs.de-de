---
title: Schließen Ihres Kontos
titleSuffix: Configuration Manager
description: In diesem Artikel wird beschrieben, wie Sie Desktop Analytics aus Ihrem Azure-Konto entfernen.
ms.date: 10/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 6e7d2850-b0af-497e-bbc1-bfc2a7420a7a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e1d031588100f3930bf5bf25970f544b91017d77
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706608"
---
# <a name="how-to-close-your-account"></a>Schließen Ihres Kontos

Wenn Sie Desktop Analytics in Ihrer Umgebung einrichten und dann entscheiden, dass Sie den Dienst entfernen müssen, führen Sie diese Schritte aus, um Ihr Konto zu schließen.

## <a name="prerequisites"></a>Voraussetzungen

Das Konto kann nur von einem **globalen Administrator** im Azure-Portal geschlossen oder erneut aktiviert werden.

## <a name="process-to-offboard"></a>Offboarding-Prozess

1. Öffnen Sie das [Desktop Analytics-Portal](https://aka.ms/desktopanalytics) in der Microsoft 365-Geräteverwaltung als Benutzer mit der Rolle **Globaler Administrator**.

1. Wählen Sie im Menü **Globale Einstellungen** die Option **Verbundene Dienste** aus. Wählen Sie im Abschnitt „Geräte registrieren“ die Option **Offboard** aus.

1. Wenn Sie sich entscheiden fortzufahren, wird Ihr Konto geschlossen.

> [!Important]
> Befolgen Sie die Anweisungen im Rest dieses Artikels erst nach 90 Tagen, oder wenn Sie das Konto nicht reaktivieren möchten.
>
> Wenn Sie Ihr Konto komplett schließen möchten, ohne 90 Tage zu warten, müssen Sie Ihr [zurücksetzen](account-reset.md).

## <a name="reactivate"></a>Reaktivieren

In den nächsten 90 Tagen erhält jeder Administrator Ihrer Organisation, der auf das Desktop Analytics-Portal zugreift, einen Hinweis, dass Sie sich für das Offboarding entschieden haben.

Ein globaler Administrator kann das Konto innerhalb von 90 Tagen reaktivieren. Wählen Sie die Option **Zurück** aus, um Desktop Analytics für die Organisation wiederherzustellen.

## <a name="delete-the-solution"></a>Löschen der Lösung

> [!Warning]
> Befolgen Sie die Anweisungen im Rest dieses Artikels erst nach 90 Tagen, oder wenn Sie das Konto nicht reaktivieren möchten. Wenn Sie diese anderen Komponenten löschen und trennen, versuchen Sie sie nicht zu reaktivieren.

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com) als Benutzer mit der Rolle **Globaler Administrator** an.

1. Suchen Sie in **Alle Ressourcen** nach dem Namen Ihres Desktop Analytics-Arbeitsbereichs. Diesen Namen haben Sie beim Anmelden für den Dienst angelegt.

1. Löschen Sie `Microsoft365Analytics(YourWorkspaceName)` vom Typ **Lösung**.

Die Desktop Analytics-Daten laufen je nach festgelegter Datenaufbewahrungsrichtlinie für den Arbeitsbereich ab. Sie können weiterhin alle anderen Lösungen im gleichen Arbeitsbereich verwenden.

> [!Important]  
> Wenn Sie den Log Analytics-Arbeitsbereich mit anderen Lösungen verwenden, löschen Sie den Arbeitsbereich nicht.

## <a name="remove-user-and-app-access"></a>Entfernen des Benutzer-und App-Zugriffs

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com) als Benutzer mit der Rolle **Globaler Administrator** an. Wechseln Sie zu **Azure Active Directory**.

1. Suchen Sie in **Rollen und Administratoren** nach der Rolle **Desktop Analytics-Administrator**. Entfernen Sie ihre Mitglieder.

1. Entfernen Sie in **Gruppen**die Mitglieder der folgenden Gruppen:

    - **M365 Analytics Client Admins (Log Analytics Owners)** (M365 Analytics-Clientadministratoren (Log Analytics-Besitzer))
    - **M365 Analytics Client Admins (Log Analytics Contributors)** (M365 Analytics-Clientadministratoren (Log Analytics-Mitwirkende))

1. Löschen bzw. widerrufen Sie in **Unternehmensanwendungen** die Zugriffsberechtigungen für die folgenden Apps:

    - `MaLogAnalyticsReader`

    - ConfigMgr-App. Wechseln Sie zur Configuration Manager-Konsole, um nach dem Namen dieser App zu suchen. Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Clouddienste**, und wählen Sie den Knoten **Azure-Dienste** aus. Öffnen Sie die Eigenschaften des Diensts **Desktop Analytics**, und wechseln Sie zur Registerkarte **Anwendungen**. Die **Web-App** ist diese Azure-App.

        > [!Important]  
        > Bevor Sie Änderungen an dieser App in Azure AD vornehmen, stellen Sie sicher, dass Sie sie nicht mit einem anderen Dienst in Configuration Manager wiederverwenden.

## <a name="disconnect-configuration-manager"></a>Trennen von Configuration Manager

1. Öffnen Sie die Configuration Manager-Konsole als Benutzer mit der Rolle **Hauptadministrator**.

1. Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Clouddienste**, und wählen Sie den Knoten **Azure-Dienste** aus.

1. Löschen Sie den Desktop Analytics-Dienst.

### <a name="delete-collections-for-the-pilot-and-production-deployments"></a>Löschen von Sammlungen für die Pilot-und Produktionsbereitstellungen

1. Wählen Sie in der Configuration Manager-Konsole im Arbeitsbereich **Bestand und Kompatibilität** die Option **Gerätesammlungen** aus.

1. Löschen Sie alle Sammlungen, die Sie nicht mehr verwenden. Standardmäßig befinden sich die Sammlungen unter dem Ordner **Bereitstellungspläne**.  

## <a name="reconfigure-clients"></a>Neukonfigurieren von Clients

### <a name="unenroll-devices"></a>Aufheben der Registrierung von Geräten

Entfernen Sie auf registrierten Geräten den Wert für CommercialID aus den folgenden Windows-Registrierungsschlüsseln:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

### <a name="windows-diagnostic-data-configuration"></a>Konfiguration der Windows-Diagnosedaten

Wenn Ihre Geräte nicht weiterhin Diagnosedaten senden sollen:

- Windows 10: Legen Sie die Diagnosedatenebene auf **Sicherheit** fest.
- Windows 7 SP1 oder 8.1: Deaktivieren Sie den Schlüssel **Einwilligung für kommerzielle Windows-Daten**.

Legen Sie diese Werte mithilfe einer der folgenden Methoden fest:

- Gruppenrichtlinie, in **Computerkonfiguration** > **Administrative Vorlagen** > **Windows-Komponenten** > **Datensammlung und Vorabversionen**
- Verwaltung mobiler Geräte (MDM), z. B. mit [Microsoft Intune](https://docs.microsoft.com/intune/device-restrictions-windows-10#reporting-and-telemetry)

Weitere Informationen finden Sie unter [Konfigurieren von Windows-Diagnosedaten in Ihrer Organisation](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization).

> [!NOTE]  
> Wenn Sie diese Änderungen anwenden, senden Geräte ab sofort keine Diagnosedaten mehr. Es kann 24 bis 48 Stunden dauern, bis Microsoft die Verarbeitung von Erkenntnissen für Ihren Arbeitsbereich einstellt. Microsoft löscht diese Daten spätestens nach 30 Tagen aus seinen Clouddiensten.
