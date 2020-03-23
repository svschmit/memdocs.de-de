---
title: Verwenden Sie Massengeräteaktionen auf dem Microsoft Intune-Gerät.
titleSuffix: ''
description: Verwenden Sie Remote-Massengeräteaktionen.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 3/12/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8c50f5495aa593dc8904fe6a9120ecd29de693ee
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79349146"
---
# <a name="use-bulk-device-actions"></a>Verwenden von Massengeräteaktionen

Massengeräteaktionen können für die folgenden Remoteaktionen verwendet werden:
- [Autopilot-Zurücksetzung](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset)
- [Benutzerdefinierte Benachrichtigungen](custom-notifications.md#send-a-custom-notification-to-a-single-device)
- [Löschen](devices-wipe.md#delete-devices-from-the-intune-portal)
- [Umbenennen](device-rename.md)
- [Neu starten](device-restart.md)
- [Synchronisieren](device-sync.md)
- [Zurücksetzen](devices-wipe.md#wipe)

## <a name="use-a-bulk-device-action"></a>Verwenden einer Massengeräteaktion

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Geräte** > **alle Geräte** > **Massengeräteaktionen** aus.
![Massengeräteaktionen](./media/bulk-device-actions/bulk-device-actions.png)
3. Wählen Sie auf der Seite **Massengeräteaktion** ein **Betriebssystem** und eine **Geräteaktion** aus. Für einige Geräteaktionen sind zusätzliche Optionen oder Felder zum Auffüllen vorhanden. Wählen Sie **Weiter** aus.
4. Wählen Sie auf der Seite **Geräte** zwischen 1 und 100 Geräte > **Weiter** aus.
5. Klicken Sie auf der Seite **Bewerten + erstellen** auf **Erstellen**.

## <a name="next-steps"></a>Nächste Schritte
[Übersicht über die Geräteverwaltung](device-management.md)
