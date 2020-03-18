---
title: Löschen eines macOS-Geräts
titleSuffix: Microsoft Intune
description: Erfahren Sie, wie Sie alle Daten einschließlich des Betriebssystems von einem macOS-Gerät löschen.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ab396092-907a-44b7-a157-aabee62176a9
ms.reviewer: coferro
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 650ba81c9e92ce03b67e90cf188435b7dc0800fb
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79338213"
---
# <a name="erase-all-data-from-a-macos-device"></a>Löschen aller Daten von einem macOS-Gerät

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Sie können alle Daten einschließlich des Betriebssystems von einem macOS-Gerät löschen. Das Gerät wird auch aus der Intune-Verwaltung entfernt. Der Endbenutzer erhält keine Warnung.

1. Wählen Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) die Option **Geräte** > **Alle Geräte**, und wählen Sie das Gerät aus, das Sie löschen möchten.
2. Klicken Sie auf **Weitere** > **Löschen**, und geben Sie eine sechsstellige Nummer für die **PIN für Wiederherstellung** ein. Dies ist die Pin, die Sie dem Benutzer zur Verfügung stellen müssen, damit er das Betriebssystem auf seinem Gerät installieren kann. Achten Sie darauf, dass Sie sich diese Pin notieren, da sie nach der Löschaktion nicht sichtbar ist.
![Screenshot](./media/device-erase/providepin.png)
3. Klicken Sie auf **OK**, um das Gerät zu löschen.
