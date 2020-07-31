---
title: Überwachen der Integration von Microsoft Defender Advanced Threat Protection (ATP) in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Überwachen Sie die Integration von Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) in Intune, einschließlich Gerätekonformität und Onboardingstatus.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: cedb255a575d4b6ea04dd684b5592748e63397c8
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/28/2020
ms.locfileid: "87264538"
---
# <a name="monitor-device-status-when-you-integrate-microsoft-defender-atp-with-intune"></a>Überwachen des Gerätestatus beim Integrieren von Microsoft Defender ATP in Intune

Wenn Sie Microsoft Defender Advanced Threat Protection (ATP) in Microsoft Intune integrieren, können Sie Informationen zu Gerätekonformität und Onboardingstatus im Microsoft Endpoint Manager Admin Center anzeigen.

## <a name="monitor-device-compliance"></a>Überwachen der Gerätekonformität

Überwachen Sie den Status von Geräten, auf die die Microsoft Defender ATP-Konformitätsrichtlinie angewandt wird.

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Geräte** > **Überwachen** > **Richtlinienkonformität** aus.

3. Suchen Sie Ihre Microsoft Defender ATP-Richtlinie in der Liste, und sehen Sie, welche Geräte konform bzw. nicht konform sind.

Sie können für nicht konforme Geräte am gleichen Speicherort auch die Option für einen *operational report* (Betriebsbericht) verwenden:

- Klicken Sie auf **Geräte** > **Überwachen** > **Noncompliant devices** (Nicht konforme Geräte).

Weitere Informationen zu Berichten finden Sie unter [Intune-Berichte](../fundamentals/reports.md).

## <a name="view-onboarding-status"></a>Anzeigen des Onboardingstatus

Um den Onboardingstatus Ihrer über Intune verwalteten Geräte anzuzeigen, navigieren Sie zu **Endpunktsicherheit** > **Microsoft Defender ATP**. Auf dieser Seite können Sie auch ein Gerätekonfigurationsprofil für das Onboarding mehrerer Geräte in Microsoft Defender ATP erstellen.

## <a name="next-steps"></a>Nächste Schritte

[Erzwingen der Konformität für Microsoft Defender ATP mit bedingtem Zugriff in Intune](../protect/advanced-threat-protection.md)
