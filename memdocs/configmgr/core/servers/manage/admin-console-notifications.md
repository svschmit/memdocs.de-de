---
title: Configuration Manager-Konsolenbenachrichtigungen
titleSuffix: Configuration Manager
description: Erfahren Sie mehr zu Benachrichtigungen in der Configuration Manager-Konsole.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a0d709fa-c4f8-46e1-b432-582cc293be35
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 12ec788fdf19ec72e954f5a9f229a5a3f95a4610
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129515"
---
# <a name="configuration-manager-console-notifications"></a>Configuration Manager-Konsolenbenachrichtigungen

*Gilt für: Configuration Manager (Current Branch)*

<!--3556016, fka 1318035-->
Ab der Configuration Manager-Version 1902 benachrichtigt die Configuration Manager-Konsole Sie bei bestimmten auftretenden Ereignissen. Sie können für Ihre Configuration Manager-Standorte einige der Ereignisbenachrichtigungen konfigurieren.

- Nicht konfigurierbare Ereignisbenachrichtigungen:
   - Ein Update ist für Configuration Manager selbst verfügbar.
   - Lebenszyklus- und Verwaltungsereignisse treten in der Umgebung auf.
- Konfigurierbare Ereignisbenachrichtigungen:
   - [Nicht kritische Änderungen der Standortintegrität](#bkmk_noncrit)
   - [Nachrichten von Microsoft](#bkmk_msft) (ab Version 2006)

Diese Benachrichtigung wird als Leiste am oberen Rand des Konsolenfensters unter dem Menüband dargestellt. Es ersetzt die vorherige Oberfläche, wenn Configuration Manager-Updates verfügbar sind. Diese Benachrichtigungen in der Konsole enthalten wichtige Informationen, beeinträchtigen aber nicht Ihre Arbeit in der Konsole. Sie können kritische Benachrichtigungen nicht verwerfen. Die Konsole zeigt alle Benachrichtigungen in einem neuen Benachrichtigungsbereich der Titelleiste an.

![Benachrichtigungsleiste und -Flag in der Konsole](./media/1318035-notify-eval-version-expired.png)

## <a name="configure-a-site-to-show-non-critical-notifications"></a><a name="bkmk_noncrit"></a> Konfigurieren eines Standorts zur Anzeige nicht kritischer Benachrichtigungen

Sie können die Eigenschaften jedes Standorts so konfigurieren, dass nicht kritische Benachrichtigungen angezeigt werden.

1. Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Standortkonfiguration**, und wählen Sie dann den Knoten **Standorte** aus.
1. Wählen Sie den Standort aus, den Sie für nicht kritische Benachrichtigungen konfigurieren möchten.
1. Wählen Sie im Menüband **Eigenschaften** aus.
1. Wählen Sie auf der Registerkarte **Warnungen** die Option **Konsolenbenachrichtigungen für nicht kritische Integritätsänderungen der Website aktivieren** aus.
   - Wenn Sie diese Einstellung aktivieren, sehen alle Konsolenbenutzer Benachrichtigungen der Typen „Kritisch“, „Warnung“ und „Information“. Diese Einstellung ist standardmäßig aktiviert.  
   - Wenn Sie diese Einstellung deaktivieren, sehen Konsolenbenutzer nur kritische Benachrichtigungen.  

Die meisten Konsolenbenachrichtigungen gelten pro Sitzung. Die Konsole wertet Abfragen aus, wenn sie von einem Benutzer gestartet wird. Wenn Sie Änderungen in den Benachrichtigungen anzeigen möchten, starten Sie die Konsole neu. Verwirft ein Benutzer eine nicht kritische Benachrichtigung, wird sie erneut angezeigt, wenn die Konsole neu gestartet wird und die Benachrichtigung noch immer gültig ist.

Die folgenden Benachrichtigungen werden alle fünf Minuten neu ausgewertet:

- Standort befindet sich im Wartungsmodus  
- Site is in recovery mode (Standort befindet sich im Wiederherstellungsmodus)  
- Site is in upgrade mode (Standort befindet sich im Upgrademodus)  

Benachrichtigungen unterliegen den Berechtigungen der rollenbasierten Verwaltung. Wenn ein Benutzer z. B. nicht über Berechtigungen zum Anzeigen von Configuration Manager-Updates verfügt, werden ihm diese Benachrichtigungen nicht angezeigt.

Einige Benachrichtigungen verfügen über eine zugehörige Aktion. Wenn die Konsolenversion beispielsweise nicht mit der Standortversion übereinstimmt, klicken Sie **Install the new console version** (Neue Konsolenversion installieren). Diese Aktion startet den Konsoleninstaller.

Wenn Sie ab Version 2006 Azure-Dienste so konfigurieren, dass Ihr Standort an die Cloud angebunden wird, erhalten Sie Benachrichtigungen mit einer Aktion zum [Verlängern des geheimen Schlüssels](../deploy/configure/azure-services-wizard.md#bkmk_renew).<!--6386392--> Der Standort bewertet den Zustand der folgenden Warnungen einmal pro Stunde:

- Mindestens ein geheimer Azure AD-Schlüssel für die App läuft bald ab
- Mindestens ein geheimer Azure AD-Schlüssel für die App ist abgelaufen

Die folgenden Benachrichtigungen treten häufig im Technical Preview-Branch auf:  

- Evaluation version is within 30 days of expiration (Evaluierungsversion läuft innerhalb von 30 Tagen ab) (Warnung): Die Evaluierungsversion läuft ab dem aktuellen Datum innerhalb von 30 Tagen ab.  
- Evaluation version is expired (Evaluierungsversion ist abgelaufen) (Kritisch): Zum aktuellen Datum liegt das Ablaufdatum bereits in der Vergangenheit.  
- Console version mismatch (Konflikt der Konsolenversionen) (Kritisch): Die Konsolenversion entspricht nicht der Standortversion.  
- Site upgrade is available (Standortupgrade ist verfügbar) (Warnung): Es ist ein neues Updatepaket verfügbar.  

Weitere Informationen und Unterstützung bei der Problembehandlung finden Sie in der Datei **SmsAdminUI.log** auf dem Konsolencomputer. Diese Protokolldatei befindet sich standardmäßig im folgenden Pfad: `C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\AdminUILog\SmsAdminUI.log`.

## <a name="configure-a-site-to-receive-messages-from-microsoft"></a><a name="bkmk_msft"></a> Konfigurieren eines Standorts zum Empfangen von Nachrichten von Microsoft
 <!--3953121-->

Ab Version 2006 haben Sie die Möglichkeit, Benachrichtigungen von Microsoft in der Configuration Manager-Konsole zu empfangen. Mithilfe dieser Benachrichtigungen bleiben Sie über neue oder aktualisierte Features, Änderungen an Configuration Manager und angefügte Dienste sowie Probleme, die Behebungsmaßnahmen erfordern, auf dem Laufenden.

### <a name="configure-notification-settings-for-microsoft-messages"></a>Konfigurieren von Benachrichtigungseinstellungen für Nachrichten von Microsoft

1. Navigieren Sie zu **Verwaltung** > **Standortkonfiguration** > **Standorte**.
1. Klicken Sie mit der rechten Maustaste auf einen Standort, und wählen Sie **Eigenschaften** aus.
1. Aktivieren Sie auf der Registerkarte **Warnungen** die Benachrichtigungen, indem Sie **Nachrichten von Microsoft empfangen** auswählen. Sie können die Auswahl der folgenden Benachrichtigungen aufheben, wenn Sie diese nicht erhalten möchten:  
   - **Verhindern/korrigieren**: Bekannte Probleme, die Ihre Organisation betreffen und möglicherweise eine Aktion erfordern.
   - **Änderungen einplanen**: Änderungen an Configuration Manager, die möglicherweise eine Aktion erfordern.
   - **Auf dem Laufenden bleiben**: Informationen zur Verfügbarkeit neuer oder aktualisierter Features.

     [ ![Optionen für Benachrichtigungen von Microsoft in den Standorteigenschaften](./media/3953121-microsoft-notifications.png)](./media/3953121-microsoft-notifications.png#lightbox)



## <a name="next-steps"></a>Nächste Schritte

- [Verwendung der Konsole](admin-console.md)
- [Tipps für die Konsole](admin-console-tips.md)
- [Barrierefreiheitsfunktionen](../../understand/accessibility-features.md)
