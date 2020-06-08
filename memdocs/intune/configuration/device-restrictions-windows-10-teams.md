---
title: Surface Hub Windows 10 Team-Geräteeinschränkungen in Microsoft Intune – Azure | Microsoft-Dokumentation
titleSuffix: ''
description: Verwenden Sie Intune, um Einstellungen für Surface Hub-Geräte mit Windows 10 Team hinzuzufügen oder zu konfigurieren.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/14/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b57bc0b7c76a6b67a26c7b1fdacb7880173a055c
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429689"
---
# <a name="windows-10-team-settings-to-allow-or-restrict-features-on-surface-hub-devices-using-intune"></a>Windows 10 Team-Einstellungen zum Zulassen oder Einschränken von Features auf Surface Hub-Geräten mit Intune

In diesem Artikel erhalten Sie Informationen zu den Einstellungen für Microsoft Intune-Geräteeinschränkungen, die Sie für Windows 10 Team-Geräte (einschließlich Surface Hub-Geräte) konfigurieren können.

## <a name="before-you-begin"></a>Vorbereitung

[Erstellen des Geräteprofils](device-restrictions-configure.md#create-the-profile).

## <a name="apps-and-experience"></a>Apps und Benutzerfreundlichkeit

Diese Einstellungen verwenden den [SurfaceHub-CSP](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp).

- **Bildschirm aktivieren, wenn eine Person im Raum ist**: **Blockieren** verhindert das automatische Aktivieren des Bildschirms, wenn der Sensor des Geräts eine Person im Raum erkennt. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Besprechungsinformationen auf Willkommensbildschirm anzeigen**: Wählen Sie die Informationen aus, die auf der Kachel „Besprechungen“ des Willkommensbildschirms angezeigt werden. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
  - **Nur Organisator und Uhrzeit**
  - **Organisator, Uhrzeit und Thema (Thema bei privaten Besprechungen ausgeblendet)**
- **URL für Hintergrundbild des Willkommensbildschirms**: Geben Sie die URL einer PNG-Bilddatei ein, die Sie als benutzerdefinierten Hintergrund auf dem **Willkommensbildschirm** auf Windows 10 Team-Geräten anzeigen möchten. Das Bild muss im PNG-Format vorliegen, und die URL muss mit `https://` beginnen.
- **App „Verbinden“ automatisch starten**: **Blockieren** verhindert, dass die App „Verbinden“ beim Starten einer Projektion automatisch geöffnet wird. Wenn sie blockiert ist, können Benutzer die App „Verbinden“ über die Einstellungen des Hubs manuell starten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Anmeldevorschläge**: **Blockieren** deaktiviert das automatische Ausfüllen des Anmeldedialogfelds mit eingeladenen Personen aus geplanten Besprechungen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Meine Besprechungen und Dateien**: **Blockieren** deaktiviert das Feature **Meine Besprechungen und Dateien** im Startmenü. Dieses Feature zeigt die Besprechungen und Dateien des angemeldeten Benutzers aus Office 365 an. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

## <a name="azure-operational-insights"></a>Azure Operational Insights

- **Azure Operational Insights**: **Aktivieren** erfasst, speichert und analysiert Protokolldaten von Windows 10 Team-Geräten mit Azure Operational Insights. Azure-Operational Insights ist Teil der Microsoft Operations Manager-Suite. Geben Sie zum Herstellen einer Verbindung mit Azure Operational Insights eine **Arbeitsbereichs-ID** und einen **Arbeitsbereichsschlüssel** ein.

  Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig erfasst das Betriebssystem diese Daten nicht.

## <a name="maintenance"></a>Wartung

Diese Einstellungen verwenden den [SurfaceHub-CSP](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp).

- **Wartungsfenster für Updates**: **Aktivieren** erstellt ein Wartungsfenster, in dem Updates installiert werden können. Geben Sie die **Startzeit** des Wartungsfensters und die **Dauer in Stunden** an. Diese kann zwischen 1 und 5 Stunden betragen.

  Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

## <a name="session"></a>Sitzung

Diese Einstellungen verwenden den [SurfaceHub-CSP](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp).

- **Lautstärke**: Geben Sie den Wert für die Standardlautstärke für eine neue Sitzung ein (0 bis 100). Wenn kein Wert angegeben wird, ändert oder aktualisiert Intune diese Einstellung nicht. Standardmäßig legt das Betriebssystem die Lautstärke auf 45 fest.
- **Bildschirmtimeout**: Geben Sie die Anzahl der Minuten ein, nach der der Bildschirm des Hubs ausgeschaltet wird.
- **Sitzungstimeout**: Geben Sie die Anzahl der Minuten ein, nach der die Sitzung durch ein Timeout beendet wird.
- **Zeitlimit für Energiesparmodus**: Geben Sie die Anzahl der Minuten ein, nach der der Hub in den Energiesparmodus wechselt.
- **Sitzung fortsetzen**: **Blockieren** verhindert, dass Benutzer eine Sitzung fortsetzen können, wenn ein Sitzungstimeout auftritt. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

## <a name="wireless-projection"></a>Drahtlose Projektion

Diese Einstellungen verwenden den [SurfaceHub-CSP](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp).

- **PIN für Funkprojektion**: **Anfordern** zwingt Benutzer zur Eingabe einer PIN, bevor sie die Funkprojektionsfeatures des Geräts verwenden können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Miracast-Funkprojektion**: **Blockieren** verhindert die Verwendung von Miracast-fähigen Geräten zum Projizieren. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Kanal für die Miracast-Funkprojektion**: Wählen Sie den Miracast-Kanal aus, um die Verbindung herzustellen.

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen finden Sie unter [So konfigurieren Sie Einstellungen für Geräteeinschränkungen in Microsoft Intune](device-restrictions-configure.md).

[Weisen Sie das Profil zu](device-profile-assign.md), und [überwachen Sie seinen Status](device-profile-monitor.md).
