---
title: 'Einstellungen für gemeinsam genutzte Windows Holographic for Business-Geräte – Microsoft Intune: Azure | Microsoft-Dokumentation'
description: Fügen Sie Windows Holographic for Business hinzu, um Geräte zu konfigurieren, die gemeinsam genutzt oder von mehreren Benutzern in Microsoft Intune verwendet werden. Hier finden Sie die Einstellungen für die Kontoverwaltung und ihren Auswirkungen auf die Geräte (einschließlich Microsoft HoloLens).
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 49d1b8f407814fd368a7ff45bb94bc4c5ef7fd9d
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556284"
---
# <a name="windows-holographic-for-business-settings-to-manage-shared-devices-using-intune"></a>Windows Holographic for Business-Einstellungen zum Verwalten gemeinsam genutzter Geräte in Intune

Windows Holographic for Business-Geräte, z.B. Microsoft HoloLens, können von mehreren Benutzern verwendet werden. Geräte mit mehreren Benutzern werden als „gemeinsam genutzte Geräte“ bezeichnet und sind in den Lösungen für die mobile Geräteverwaltung (Mobile Device Management, MDM) enthalten.

Mithilfe von Microsoft Intune können Benutzer sich bei gemeinsam genutzten Geräten mit einem Gastkonto anmelden. Bei der Verwendung des Geräts erhalten diese Benutzer dann nur Zugriff auf von Ihnen ausgewählte Features.

In diesem Artikel werden die Einstellungen aufgeführt und beschrieben, die in einem Gerätekonfigurationsprofil für Windows Holographic for Business verwendet werden können. Nach dem Erstellen des Profils in Intune stellen Sie das Profil für die Gerätegruppen in Ihrer Organisation bereit oder weisen es diesen zu. Sie können dieses Profil ebenfalls zu Gerätegruppen mit gemischten Gerätetypen und Betriebssystemversionen zuweisen.

Weitere Informationen zu diesem Intune-Feature finden Sie unter [Control access, accounts, and power features on shared PC or multi-user devices (Features für das Steuern von Zugriff, Konten und Energieeinstellungen auf gemeinsam genutzten Computern oder Geräten mit mehreren Benutzern)](shared-user-device-settings.md). Weitere Informationen zum Windows-Konfigurationsdienstanbieter (Configuration Service Provider, CSP) finden Sie unter [AccountManagement CSP (Konfigurationsdienstanbieter „AccountManagement“)](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp).

## <a name="before-your-begin"></a>Vorbereitungen

[Erstellen Sie ein gemeinsames Windows 10-Gerätekonfigurationsprofil für mehrere Benutzer](shared-user-device-settings.md).

Beim Erstellen eines Windows 10-Gerätekonfigurationsprofils für mehrere Benutzer gibt es mehr Einstellungen, als in diesem Artikel aufgeführt werden. Die Einstellungen in diesem Artikel werden auf Geräten mit Windows Holographic for Business unterstützt.

## <a name="shared-multi-user-device-settings"></a>Einstellungen für von mehreren Benutzern gemeinsam genutzte Geräte

> [!NOTE]
> Unter Windows Holographic for Business ausgeführte Geräte, z.B. Microsoft HoloLens, unterstützen ausschließlich die Einstellungen der **Kontoverwaltung**. Wenn Sie eine der anderen in Intune angezeigten Einstellungen konfigurieren (wie z.B. **Modus für die gemeinsame PC-Nutzung**), hat dies keine Auswirkungen auf diese Geräte.

- **Kontoverwaltung:** Entscheiden Sie, ob die Konten automatisch gelöscht werden sollen. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Mit dieser Einstellung werden lokale Konten automatisch gelöscht, die von Gästen und Konten in Azure Active Directory erstellt werden. Wenn ein Benutzer sich von einem Gerät abmeldet oder die Systemwartung ausgeführt wird, werden diese Konten gelöscht.

    Geben Sie außerdem Folgendes ein:

    - **Kontolöschung:** Legen Sie fest, wann Konten gelöscht werden sollen:
      - **Bei Erreichen des Schwellenwerts für Speicherplatz**
      - **Bei Erreichen des Schwellenwerts für Speicherplatz und inaktive Konten**
      - **Sofort nach der Abmeldung**

    Geben Sie außerdem Folgendes ein:

    - **Schwellenwert (%) für das Starten von Löschungen:** Geben Sie einen Prozentsatz (0 – 100) für den Speicherplatz ein. Wenn der gesamte Speicherplatz unter den eingegebenen Wert fällt, werden die zwischengespeicherten Konten gelöscht. Es werden fortlaufend Konten gelöscht, um Speicherplatz freizugeben. Die Konten, die am längsten inaktiv sind, werden zuerst gelöscht.
    - **Schwellenwert (%) für das Beenden von Löschungen:** Geben Sie einen Prozentsatz (0 – 100) für den Speicherplatz ein. Wenn der gesamte Speicherplatz dem eingegebenen Wert entspricht, werden keine Konten mehr gelöscht.

  - **Deaktivieren:** Die lokalen und die Azure AD-Konten, die von Gästen erstellt werden, bleiben auf dem Gerät erhalten und werden nicht gelöscht.

## <a name="next-steps"></a>Nächste Schritte

- [Zuweisen von Profilen](device-profile-assign.md) und [Überwachen von Profilen](device-profile-monitor.md)
- Sehen Sie sich die Einstellungen für gemeinsame Benutzergeräte unter [Windows 10 und höher](shared-user-device-settings-windows.md) an.
