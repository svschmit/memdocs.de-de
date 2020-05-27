---
title: Zurücksetzen von Windows 10-Geräten mit Microsoft Intune – Azure | Microsoft-Dokumentation
description: Verwenden Sie den sauberen Start, um Apps mithilfe von Microsoft Intune von Windows 10 PCs zu entfernen oder zu deinstallieren.
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
ms.assetid: 5aa5cfa3-c483-4099-b40f-578ff8dca425
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d7003bf0aa943eab6d884b55c511fea5dddeae8e
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989927"
---
# <a name="use-fresh-start-to-reset-windows-10-devices-with-intune"></a>Verwenden der Aktion „Sauberer Start“ zum Zurücksetzen von Windows 10-Geräten mit Intune


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Die Geräteaktion **Sauberer Start** entfernt alle Apps, die auf einem PC unter Windows 10, Version 1709 oder höher, installiert wurden. „Sauberer Start“ hilft dabei, Apps (von OEMs) zu entfernen, die auf einem neuen PC häufig vorinstalliert sind. 

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an, und klicken Sie auf **Geräte** > **Alle Geräte**.
2. Wählen Sie aus der Liste der verwalteten Geräte ein Windows 10-Desktopgerät aus.
3. Klicken Sie auf **Sauberer Start**. 
4. Wählen Sie **Benutzerdaten auf diesem Gerät beibehalten** aus, um Folgendes zu ermöglichen:
   * Azure AD für das Gerät bleibt eingebunden.
   * Das Gerät wird erneut bei der Verwaltung mobiler Geräte registriert, wenn ein Azure Active Directory-Benutzer sich am Gerät anmeldet.
   * Die Inhalte des Basisordners des Gerätebenutzers werden beibehalten, und Apps und Einstellungen werden entfernt.

  > [!IMPORTANT]
 > Wenn Sie die Benutzerdaten nicht beibehalten, wird das Gerät auf den standardmäßigen abgeschlossenen OOBE-Zustand (Out-of-Box-Experience) zurückgesetzt, der das integrierte Administratorkonto beibehält.
 > Die Registrierung bei Azure AD und der mobilen Geräteverwaltung von BYOD-Geräten wird aufgehoben.
 > Mit Azure AD verknüpfte Geräte werden erneut bei der mobilen Geräteverwaltung registriert, wenn ein Azure Active Directory-Benutzer sich am Gerät anmeldet.
 
5. Klicken Sie auf **OK**.   
6. Wenn Sie den Status dieser Aktion anzeigen möchten, wechseln Sie zu **Geräte**, und klicken Sie auf **Geräteaktionen**.  
7. Das Gerät wird auf den anfänglichen Anmeldebildschirm zurückgesetzt.
