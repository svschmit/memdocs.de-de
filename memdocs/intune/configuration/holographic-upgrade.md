---
title: Upgrade auf Windows Holographic for Business in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Führen Sie ein Upgrade auf Windows 10 Holographic for Business mithilfe eines Gerätekonfigurationsprofils in Microsoft Intune aus.
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
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 65a45b13a91671c1de9bcf04f23156d75313285f
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907768"
---
# <a name="upgrade-devices-running-windows-holographic-to-windows-holographic-for-business"></a>Aktualisieren von Geräten, die Windows Holographic ausführen, auf Windows Holographic for Business

In Microsoft Intune gibt es viele Einstellungen, die dazu dienen, Ihre Geräte zu verwalten und zu schützen. In diesem Artikel werden die Einstellungen zum Upgraden von Windows Holographic-Geräten auf Windows Holographic for Business aufgelistet und beschrieben.

Als Bestandteil Ihrer Lösung für die mobile Geräteverwaltung (Mobile Device Management, MDM) verwenden Sie diese Einstellungen, um Ihre Windows Holographic-Geräte zu aktualisieren. Für Microsoft HoloLens können Sie die Commercial Suite erwerben, um die erforderliche Lizenz für das Upgrade zu erhalten. Weitere Informationen finden Sie unter [Entsperren der Features von Windows Holographic für Unternehmen](/hololens/hololens1-upgrade-enterprise).

Als Intune-Administrator können Sie für Ihre Geräte diese Einstellungen erstellen und ihnen zuweisen.

Weitere Informationen zu diesem Feature finden Sie unter [Verwenden eines Konfigurationsprofils zum Upgraden von Windows 10 oder Verlassen des S Modus in Intune](edition-upgrade-configure-windows-10.md).

## <a name="before-you-begin"></a>Vorbereitung

[Erstellen Sie ein Gerätekonfigurationsprofil für Windows 10-Editionsupgrade und Moduswechsel](edition-upgrade-configure-windows-10.md#create-the-profile).

Beim Erstellen eines Windows 10-Konfigurationsprofils für Editionsupgrade und Moduswechsel für mehrere Benutzer gibt es mehr Einstellungen, als in diesem Artikel aufgeführt werden. Die Einstellungen in diesem Artikel werden auf Geräten mit Windows Holographic for Business unterstützt.

## <a name="edition-upgrade"></a>Upgrade der Edition

- **Edition, auf die das Upgrade erfolgen soll**: Wählen Sie **Windows 10 Holographic for Business** aus.
- **Lizenzdatei**: Navigieren Sie zu der XML-Lizenzdatei, die für Sie bereitgestellt wurde, und wählen Sie sie aus.

  :::image type="content" source="./media/holographic-upgrade/Holographic-edition-upgrade.png" alt-text="Geben Sie in Intune den Namen der XML-Datei ein, die die Holographic for Business-Lizenzinformationen enthält.":::

## <a name="next-steps"></a>Nächste Schritte

[Weisen Sie das Profil zu](device-profile-assign.md), und [überwachen Sie dessen Status](device-profile-monitor.md).

Sie können auch Editionsupgradeprofile für [Windows 10-Geräte und höher](edition-upgrade-windows-settings.md) erstellen.