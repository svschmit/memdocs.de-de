---
title: Remoteunterstützung für von Intune verwaltete mobile Geräte
description: Sie können vier verschiedene Optionen verwenden, um Benutzer remote bei ihren mobilen Geräten zu unterstützen.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 34f88d4e7aefe9a32238bb6d14203de0defd65ef
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988259"
---
# <a name="remotely-assist-mobile-devices-managed-by-microsoft-endpoint-manager"></a>Remoteunterstützung für von Microsoft Endpoint Manager verwaltete mobile Geräte

Für die Remoteunterstützung für von Microsoft Endpoint Manager verwaltete Geräte stehen Ihnen vier Optionen zur Verfügung:

- [Microsoft Teams](https://products.office.com/microsoft-teams/) ist der Hub für die Teamarbeit, in dem Sie von jedem Ort der Welt aus mit Mitgliedern Ihres Teams chatten, diskutieren und zusammenarbeiten können.
- [Quick Assist](https://support.microsoft.com/help/4027243/windows-10-solve-pc-problems-with-quick-assist) ist eine Windows 10-Anwendung, mit der zwei Personen ein Gerät über eine Remoteverbindung gemeinsam nutzen können.
- [TeamViewer](https://www.teamviewer.com/) ist ein Drittanbieterprogramm, das Sie separat erwerben können. Es bietet umfassende Funktionen für Remotezugriff und -support. Die Integration von Intune und [TeamViewer](teamviewer-support.md) ermöglicht die Bereitstellung von Remotesupport über TeamViewer. Der Connector wird dabei direkt in Intune verwaltet.
- Microsoft Endpoint Configuration Manager umfasst eine [Remotesteuerung](https://docs.microsoft.com/configmgr/core/clients/manage/remote-control/introduction-to-remote-control). Mit dieser Funktion können Sie alle Arbeitsgruppencomputer und in die Domäne eingebundenen Computer remote verwalten, unterstützen oder anzeigen.

| Features, Plattformen, Lizenzierung | **Teams** | Quick Assist | TeamViewer (Intune) | Remotesteuerung (Configuration Manager) |
|:---:|:---:|:---:|:---:|:---:|
| Remoteansicht und -steuerung |![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)|![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)|![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)|![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Chat |![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)||![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)||
| Dateiübertragung |![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)|![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)|![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)|![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Administratorzugriff mit erhöhten Rechten |||![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)|![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Unbeaufsichtigter Zugriff |||![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)|![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Simultane Remotesteuerung |![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)|![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)|||
| Unterstützung mehrerer Benutzer |||![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)|![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Remoteaktionen ||![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)|![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)|![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Support über das Internet |![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)|![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)|![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)||
| Überwachungsberichte |![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)||![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)|![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Unterstützung für alle Plattformen (Windows, iOS, Android, macOS) |![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)||![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)||
| In Windows 10 integriert – keine zusätzliche App erforderlich ||![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)|||
| Erfordert Co-Verwaltung des Geräts durch Configuration Manager und Intune ||||![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Erfordert zusätzliche Lizenzierung\* |![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)||![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)|![Häkchen](../enrollment/media/enrollment-method-capab/checkmark.png)|

\* Teams erfordert O365- oder M365-Lizenzen. Für die Verwendung von TeamViewer und Intune müssen beide Programme lizenziert sein. Die Remotesteuerung ist ein Feature von Configuration Manager und erfordert die Lizenzierung von Configuration Manager.
