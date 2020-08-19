---
title: Sperren von Geräten mit Microsoft Intune – Azure | Microsoft-Dokumentation
description: Verwenden Sie die Aktion „Remotesperre“ in Microsoft Intune, um ein Gerät zu sperren, das durch eine PIN oder ein Kennwort geschützt ist.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3b67f285-229d-4a0f-ae34-0402a20b4518
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4e558c885098b8b396ca0e6304bd18ef36e3c28b
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252236"
---
# <a name="remotely-lock-devices-with-intune"></a>Remotesperren von Geräten mit Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Mit der Geräteaktion **Remotesperre** wird ein Gerät gesperrt. Zum Entsperren des Geräts muss der Eigentümer des Geräts die entsprechende Kennung verwenden. Sie können Geräte remote sperren, für die eine PIN oder ein Kennwort festgelegt ist. Geräte, die nicht über eine PIN oder ein Kennwort verfügen, können nicht remote gesperrt werden.

## <a name="supported-platforms"></a>Unterstützte Plattformen

Die **Remotesperre** wird für folgende Plattformen unterstützt:

- Android
- Android Enterprise-Kioskgeräte
- Android Enterprise-Geräte mit Arbeitsprofil
- Vollständig verwaltete Android Enterprise-Geräte
- Unternehmenseigene Android Enterprise-Geräte mit Arbeitsprofil
- iOS
- macOS

Die **Remotesperre** wird für folgende Plattformen nicht unterstützt:
- Windows 10 Desktop

> [!NOTE]
> Bei macOS-Geräten legen Sie eine Wiederherstellungs-PIN aus 6 Ziffern fest. Wenn das Gerät gesperrt ist, wird in der **Geräteübersicht** die PIN angezeigt, bis eine andere Geräteaktion gesendet wird. Stellen Sie sicher, dass Sie sich die PIN notieren, da sie nur 30 Tage nach dem Senden des Remotesperrbefehls verfügbar ist. Nach diesen 30 Tagen verfügt Intune nicht mehr über die PIN. Außerdem wird der Status in der Berichterstattung als fehlerhaft angezeigt, wenn Sie diesen Befehl für dasselbe Gerät noch mal initiieren, das Gerät jedoch nicht mit der ursprünglichen PIN erfolgreich entsperrt wurde. Sie sollten diesen Befehl nur einmal senden, sich die PIN notieren und bis zum erfolgreichen Entsperren des macOS-Geräts nicht versuchen, diesen Befehl noch mal an dasselbe Gerät zu senden.


## <a name="remote-lock-a-device"></a>Remotesperre für Gerät aktivieren

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
3. Klicken Sie auf **Geräte** > **Alle Geräte**.
4. Wählen Sie aus der Geräteliste ein Gerät aus, und klicken Sie dann auf die Aktion **Remotesperre**.

## <a name="next-steps"></a>Nächste Schritte

- Klicken Sie auf **Microsoft Intune** > **Geräte** > **Geräteaktionen**, um den Status dieser Aktion anzuzeigen. 
- Weitere Aktionen zum Verwalten Ihrer Geräte finden Sie unter [Verfügbare Aktionen](device-management.md).
