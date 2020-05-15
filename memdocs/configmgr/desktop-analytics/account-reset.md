---
title: Zurücksetzen Ihres Kontos
titleSuffix: Configuration Manager
description: In diesem Artikel erfahren Sie, wie Sie Ihr Desktop Analytics-Konto zurücksetzen.
ms.date: 08/16/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 884d4864-950b-4139-b778-d5368e1f6ef2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 29f108254e3201925917a0546dd96d36a19763b6
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268877"
---
# <a name="how-to-reset-your-account"></a>Zurücksetzen Ihres Kontos

<!-- 3733897 -->

Wenn Sie Desktop Analytics in Ihrer Umgebung einrichten, jedoch mit dem Onboarding und der Registrierung von vorn beginnen möchten, führen Sie diesen Vorgang aus, um Ihr Konto zurückzusetzen.

## <a name="prerequisites"></a>Voraussetzungen

Das Konto kann nur von einem **globalen Administrator** im Azure-Portal zurückgesetzt werden.

## <a name="behaviors"></a>Verhalten

- Bei diesem Prozess werden keine vorhandenen Azure AD-Benutzer, -Apps und -Berechtigungen geändert.

- Wenn Sie einen neuen Arbeitsbereich hinzufügen, werden die folgenden Benutzereingaben für Elemente nicht beibehalten:
    - Wichtigkeit
    - Besitzer
    - Upgradeentscheidung
    - Hinweise zu Gegenmaßnahmen

## <a name="process"></a>Prozess

1. Öffnen Sie das [Desktop Analytics-Portal](https://aka.ms/desktopanalytics) in der Microsoft 365-Geräteverwaltung als Benutzer mit der Rolle **Globaler Administrator**.

1. Wählen Sie im Menü **Globale Einstellungen** die Option **Verbundene Dienste** aus. Wählen Sie im Abschnitt „Geräte registrieren“ die Option **Zurücksetzen** aus.

1. Wenn Sie angeben, dass der Vorgang fortgesetzt werden soll, wird Ihr Konto zurückgesetzt. Sie müssen Desktop Analytics erneut einrichten.

## <a name="next-steps"></a>Nächste Schritte

Aktualisieren Sie nach dem Zurücksetzen die Seite, und führen Sie den Onboarding-Prozess erneut aus. Weitere Informationen finden Sie unter [Einrichten von Desktop Analytics](set-up.md).

Wenn während dieses Vorgangs Probleme auftreten, wenden Sie sich an Microsoft-Support, um weitere Unterstützung zu erhalten.
