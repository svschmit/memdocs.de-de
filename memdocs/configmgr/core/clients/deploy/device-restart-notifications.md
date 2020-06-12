---
title: Benachrichtigungen zum Geräteneustart
titleSuffix: Configuration Manager
description: Hier wird das Verhalten von Benachrichtigungen zum Neustart für diverse Clienteinstellungen in Configuration Manager beschrieben.
ms.date: 06/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5ef1bff8-9733-4b5a-b65f-26b94accd210
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b326c4dd8112a72555239f2c3eda078ebf47bf82
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347218"
---
# <a name="device-restart-notifications-in-configuration-manager"></a>Benachrichtigungen zum Geräteneustart in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Die Benachrichtigungen, die ein Benutzer zu einem ausstehenden Geräteneustart erhält, können je nach [Clienteinstellungen für den Computerneustart](#client-settings) und verwendeter Version von Configuration Manager variieren. Dieser Artikel unterstützt Administratoren bei der Konfiguration von Benachrichtigungen zu einem ausstehenden Geräteneustart.

## <a name="deployment-types-for-restart-notifications"></a>Bereitstellungstypen für Benachrichtigungen zum Neustart

Die [Clienteinstellungen für den Computerneustart](#client-settings) ändern die Benutzeroberfläche für alle erforderlichen Bereitstellungen folgender Arten, die einen Neustart erfordern:

- [Anwendung](../../../apps/deploy-use/deploy-applications.md)
- [Tasksequenz](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
- [Softwareupdate](../../../sum/deploy-use/deploy-software-updates.md)

## <a name="restart-notification-types"></a>Typen von Benachrichtigung zum Neustart

Wenn ein Gerät neu gestartet werden muss, zeigt der Client dem Benutzer eine entsprechende Benachrichtigung an. Es gibt vier allgemeine Benachrichtigungen, die Benutzer erhalten können.

### <a name="toast-notification"></a>Popupbenachrichtigung

Eine Windows-Popupbenachrichtigung informiert den Benutzer darüber, dass das Gerät neu gestartet werden muss. Die Informationen in der Popupbenachrichtigung können unterschiedlich sein, je nachdem, welche Version von Configuration Manager Sie ausführen. Dies ist eine native Benachrichtigung des Windows-Betriebssystems. Diese Art von Benachrichtigung wird auch in Software von Drittanbietern verwendet.

![Popupbenachrichtigung über ausstehenden Neustart](media/3555947-restart-toast.png)

### <a name="software-center-notification-with-snooze"></a>Softwarecenter-Benachrichtigungen mit Erinnerungsoption

Im Softwarecenter wird eine Benachrichtigung mit einer Erinnerungsoption und der verbleibenden Zeit angezeigt, bevor der Neustart des Geräts erzwungen wird. Die Benachrichtigung kann je nach Configuration Manager-Version variieren.

![Softwarecenter-Benachrichtigung über ausstehenden Neustart mit Schaltfläche „Erneut erinnern“](media/3976435-snooze-restart-countdown.png)

### <a name="software-center-final-countdown-notification"></a>Softwarecenter-Benachrichtigung mit finalem Countdown

Diese finale Countdownbenachrichtigung wird vom Softwarecenter angezeigt. Der Benutzer kann die Benachrichtigung nicht schließen und keine Option zum erneuten Erinnern auswählen.

![Softwarecenter-Benachrichtigung mit finalem Countdown](media/3976435-final-restart-countdown.png)

Ab Version 1906 wird dem Benutzer erst dann eine Statusanzeige in der Neustartbenachrichtigung angezeigt, wenn der ausstehende Neustart in weniger als 24 Stunden durchgeführt wird.

### <a name="software-center-notification-before-deadline"></a>Softwarecenter-Benachrichtigung vor dem Stichtag

Wenn der Benutzer die erforderliche Software proaktiv vor dem Stichtag installiert und ein Neustart erforderlich ist, wird eine andere Benachrichtigung angezeigt. Die folgende Benachrichtigung wird ausgegeben, wenn die Einstellung für die Benutzeroberfläche Benachrichtigungen zulässt und Sie keine Popupbenachrichtigungen für die Bereitstellung verwenden. Weitere Informationen zum Konfigurieren dieser Einstellungen finden Sie unter [Deployment **User Experience** settings](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux) (Bereitstellungseinstellungen für [Benutzeroberfläche])und [Benutzerbenachrichtigungen für erforderliche Bereitstellungen](../../../apps/deploy-use/deploy-applications.md#bkmk_notify).

![Benachrichtigung für proaktiv installierte Software](media/3976435-proactive-user-restart-notification.png)

#### <a name="available-apps"></a>Verfügbare Apps

Wenn Sie keine Popupbenachrichtigungen verwenden, ähnelt das Dialogfeld für als **Verfügbar** markierte Software proaktiv installierter Software. Bei als **Verfügbar** markierter Software enthält die Benachrichtigung keine Frist für den Neustart, und der Benutzer kann das Intervall für eine erneute Erinnerung selbst wählen. Weitere Informationen finden Sie unter [Genehmigungseinstellungen](../../../apps/deploy-use/deploy-applications.md#bkmk_approval).

![Bei Software, die als „Verfügbar“ markiert ist, ist in der Benachrichtigung keine Frist für einen Neustart angegeben.](media/3555947-deployment-marked-available-restart.png)

## <a name="client-settings"></a>Clienteinstellungen

Konfigurieren Sie die folgenden Clienteinstellungen auf dem Gerät in der Gruppe **Computerneustart**, um das Neustartverhalten von Clients zu steuern. Weitere Informationen finden Sie unter [Konfigurieren von Clienteinstellungen](configure-client-settings.md).

### <a name="specify-the-amount-of-time-after-the-deadline-before-a-device-gets-restarted-minutes"></a>Geben Sie den Zeitraum (in Minuten) nach dem Stichtag an, bevor ein Gerät neu gestartet wird

Die folgende Einstellung muss eine kürzere Dauer als das kürzeste Wartungsfenster des Computers aufweisen. Weitere Informationen zu Wartungsfenstern finden Sie unter [Verwenden von Wartungsfenstern](../manage/collections/use-maintenance-windows.md).

Der Standardwert beträgt 90 Minuten. Ab Version 1906 wurde der Höchstwert von 1.440 Minuten (24 Stunden) auf 20.160 Minuten (zwei Wochen) erhöht.

> [!NOTE]
> Der Name dieser Einstellung lautete zuvor **Temporäre Benachrichtigung für Benutzer anzeigen, in der auf das Intervall (in Minuten) bis zum Abmelden des Benutzers oder Neustart des Computers hingewiesen wird**.

### <a name="specify-the-amount-of-time-that-a-user-is-presented-a-final-countdown-notification-before-a-device-gets-restarted-minutes"></a>Geben Sie den Zeitraum (in Minuten) an, für den ein Benutzer eine letzte Countdownbenachrichtigung erhält, bevor ein Gerät neu gestartet wird

Die folgende Einstellung muss eine kürzere Dauer als das kürzeste Wartungsfenster des Computers aufweisen. Weitere Informationen zu Wartungsfenstern finden Sie unter [Verwenden von Wartungsfenstern](../manage/collections/use-maintenance-windows.md).

Der Standardwert beträgt 15 Minuten.

> [!NOTE]
> Der Name dieser Einstellung lautete zuvor **Nicht vom Benutzer schließbares Dialogfeld anzeigen, in der das Countdownintervall (in Minuten) bis zum Abmelden des Benutzers oder Neustart des Computers angezeigt wird**.

### <a name="specify-the-frequency-of-reminder-notifications-presented-to-the-user-after-the-deadline-before-a-device-gets-restarted-minutes"></a>Legen Sie fest, wie häufig dem Benutzer nach dem Stichtag Erinnerungen angezeigt werden, bevor ein Gerät neu gestartet wird (in Minuten)
<!--3976435-->
_Ab Version 1906_

Dieser Häufigkeitswert sollte geringer sein als der Wert von **Geben Sie den Zeitraum (in Minuten) nach dem Stichtag an, bevor ein Gerät neu gestartet wird** abzüglich des Werts von **Geben Sie den Zeitraum (in Minuten) an, für den ein Benutzer eine letzte Countdownbenachrichtigung erhält, bevor ein Gerät neu gestartet wird**. Anderenfalls funktionieren die Erinnerungsbenachrichtigungen nicht.

Der Standardwert beträgt 240 Minuten.

> [!NOTE]
> Der Name dieser Einstellung lautete zuvor **Dauer für erneute Erinnerung für Countdownbenachrichtigungen zum Computerneustart (Minuten) angeben**.

### <a name="when-a-deployment-requires-a-restart-show-a-dialog-window-to-the-user-instead-of-a-toast-notification"></a>Wenn für eine Bereitstellung ein Neustart erforderlich ist, dem Benutzer ein Dialogfeld anstelle einer Popupbenachrichtigung anzeigen
<!--3555947-->
Ab Version 1902 wird die Benutzeroberfläche durch die Konfiguration dieser Einstellung auf **Ja** deutlicher gestaltet. Diese Einstellung gilt für alle Bereitstellungen von Anwendungen, Tasksequenzen und Softwareupdates. Weitere Informationen finden Sie unter [Planen für Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_impact).

> [!IMPORTANT]
> In Configuration Manager 1902 ersetzt das Dialogfeld unter bestimmten Umständen keine Popupbenachrichtigungen. Installieren Sie zur Behebung dieses Problems das [Updaterollup für Configuration Manager Version 1902](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902). <!--4404715-->

## <a name="device-restart-notifications-version-1906"></a>Benachrichtigungen zum Geräteneustart (Version 1906)
<!--3976435-->
Einige Kunden bevorzugen häufige Neustartbenachrichtigungen sowie ein kurzes Zeitfenster, für das ein Neustart aufgeschoben werden kann. Andere Organisationen gestatten Benutzern, den Neustart für eine längere Zeit aufzuschieben, und benachrichtigen Benutzer seltener über den ausstehenden Neustart. Ab der Configuration Manager-Version 1906 sind zusätzliche Optionen zum Steuern der Terminierung und Häufigkeit von Neustartbenachrichtigungen verfügbar.

### <a name="install-required-software-at-or-after-the-deadline"></a>Installation der erforderlichen Software am oder nach dem Stichtag

Wenn erforderliche Software am oder nach dem Stichtag installiert wird, werden Benutzern Benachrichtigungen entsprechend den ausgewählten Clienteinstellungen angezeigt.

Wenn die Einstellung **Wenn für eine Bereitstellung ein Neustart erforderlich ist, dem Benutzer ein Dialogfeld anstelle einer Popupbenachrichtigung anzeigen** auf folgenden Wert festgelegt ist:

- **Nein**: Windows zeigt Popupbenachrichtigungen an, bis die finale Countdownbenachrichtigung für die Bereitstellung erscheint.

- **Ja**: Das Softwarecenter zeigt eine Benachrichtigung an:

  - Wenn der Neustart in mehr als 24 Stunden durchgeführt wird, wird ein geschätzter Zeitpunkt für den Neustart angezeigt. Die Terminierung dieser Benachrichtigung basiert auf der Einstellung: **Geben Sie den Zeitraum (in Minuten) nach dem Stichtag an, bevor ein Gerät neu gestartet wird**.

    ![Der Neustartzeitpunkt liegt mehr als 24 Stunden entfernt](media/3976435-notification-greater-than-24-hours.png)

  - Wenn der Neustart in weniger als 24 Stunden durchgeführt wird, wird eine Statusanzeige angezeigt. Die Terminierung dieser Benachrichtigung basiert auf der Einstellung: **Geben Sie den Zeitraum (in Minuten) nach dem Stichtag an, bevor ein Gerät neu gestartet wird**.

    ![Der Neustartzeitpunkt liegt weniger als 24 Stunden entfernt](media/3976435-notification-less-than-24-hours.png)

Wenn der Benutzer die Option **Erneut erinnern** auswählt, wird nach Ablauf des Zeitraums für die erneute Erinnerung eine weitere temporäre Benachrichtigung angezeigt. Bei diesem Verhalten wird davon ausgegangen, dass der finale Countdown noch nicht erreicht wurde. Die Terminierung dieser nächsten Benachrichtigung basiert auf der Einstellung: **Legen Sie fest, wie häufig dem Benutzer nach dem Stichtag Erinnerungen angezeigt werden, bevor ein Gerät neu gestartet wird (in Minuten)** . Wenn der Benutzer die Option **Erneut erinnern** auswählt, und Ihr Intervall für die erneute Erinnerung eine Stunde beträgt, benachrichtigt das Softwarecenter den Benutzer nach 60 Minuten erneut. Bei diesem Verhalten wird davon ausgegangen, dass der finale Countdown noch nicht erreicht wurde.

Beim Erreichen des finalen Countdowns zeigt das Softwarecenter dem Benutzer eine Benachrichtigung an, die er nicht schließen kann. Die Statusanzeige ist rot, und der Benutzer kann nicht **Erneut erinnern** auswählen.

![Softwarecenter-Benachrichtigung mit finalem Countdown in Version 1906](media/3976435-1906-final-restart-countdown.png)

### <a name="proactively-install-required-software-before-the-deadline"></a>Proaktive Installation der erforderlichen Software vor dem Stichtag

Wenn der Benutzer proaktiv erforderliche Software installiert, die vor dem Stichtag einen Neustart erforderlich macht, wird eine andere Benachrichtigung angezeigt. Weitere Informationen zum Konfigurieren dieser Einstellungen finden Sie unter [Deployment **User Experience** settings](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux) (Bereitstellungseinstellungen für [Benutzeroberfläche]) und [Benutzerbenachrichtigungen für erforderliche Bereitstellungen](../../../apps/deploy-use/deploy-applications.md#bkmk_notify).

Die folgende Benachrichtigung wird ausgegeben, wenn die Einstellung für die Benutzeroberfläche Benachrichtigungen zulässt und Sie keine Popupbenachrichtigungen für die Bereitstellung verwenden:

![Benachrichtigung für proaktiv installierte Software](media/3976435-proactive-user-restart-notification.png)

Sobald der Stichtag erreicht ist, wird im Softwarecenter das Verhalten für die [Installation der erforderlichen Software am oder nach dem Stichtag](#install-required-software-at-or-after-the-deadline) angewendet.

## <a name="example-configurations"></a>Beispielkonfigurationen

Die folgenden Beispiele zeigen, wie Sie die Clienteinstellungen für ein bestimmtes Verhalten konfigurieren.

### <a name="reminders-are-off"></a>Erinnerungen sind deaktiviert

| Einstellung | Wert |
|---------|---------|
|Geben Sie den Zeitraum (in Minuten) nach dem Stichtag an, bevor ein Gerät neu gestartet wird|180|
|Geben Sie den Zeitraum (in Minuten) an, für den ein Benutzer eine letzte Countdownbenachrichtigung erhält, bevor ein Gerät neu gestartet wird|60|
|Legen Sie fest, wie häufig dem Benutzer nach dem Stichtag Erinnerungen angezeigt werden, bevor ein Gerät neu gestartet wird (in Minuten)|240|
|Wenn für eine Bereitstellung ein Neustart erforderlich ist, dem Benutzer ein Dialogfeld anstelle einer Popupbenachrichtigung anzeigen|Nein|

Das Gerät wird drei Stunden (**180** Minuten) nach dem Stichtag neu gestartet. Eine Stunde (**60** Minuten) vor dem Neustart wird dem Benutzer ein Countdown angezeigt, den er nicht schließen und für den er keine erneute Erinnerung auswählen kann. Die erste Erinnerungsbenachrichtigung wird vier Stunden (**240** Minuten) nach dem Stichtag, also nach dem Neustart angezeigt. Dem Benutzer werden also keine Erinnerungen angezeigt.

### <a name="low-reminder-frequency"></a>Niedrige Erinnerungshäufigkeit

| Einstellung | Wert |
|---------|---------|
|Geben Sie den Zeitraum (in Minuten) nach dem Stichtag an, bevor ein Gerät neu gestartet wird|7200|
|Geben Sie den Zeitraum (in Minuten) an, für den ein Benutzer eine letzte Countdownbenachrichtigung erhält, bevor ein Gerät neu gestartet wird|120|
|Legen Sie fest, wie häufig dem Benutzer nach dem Stichtag Erinnerungen angezeigt werden, bevor ein Gerät neu gestartet wird (in Minuten)|900|
|Wenn für eine Bereitstellung ein Neustart erforderlich ist, dem Benutzer ein Dialogfeld anstelle einer Popupbenachrichtigung anzeigen|Ja|

Das Gerät wird fünf Tage (**7.200** Minuten) nach dem Stichtag neu gestartet. Zwei Stunden (**120** Minuten) vor dem Neustart wird dem Benutzer ein Countdown angezeigt, den er nicht schließen und für den er keine erneute Erinnerung auswählen kann. Bei dieser Konfiguration können 118 Stunden lang Erinnerungen angezeigt werden (`(7200 - 120) / 60`). Das Softwarecenter zeigt 15 Stunden (**900** Minuten) nach dem Stichtag die erste Erinnerung an. Es werden maximal sechs zusätzliche Erinnerungen alle 15 Stunden (**900 Minuten**) angezeigt. Die Erinnerung erscheint nicht in einer Benachrichtigung, die nach wenigen Sekunden wieder ausgeblendet wird, sondern in einem Fenster auf dem Bildschirm.

### <a name="high-reminder-frequency"></a>Hohe Erinnerungshäufigkeit

| Einstellung | Wert |
|---------|---------|
|Geben Sie den Zeitraum (in Minuten) nach dem Stichtag an, bevor ein Gerät neu gestartet wird|2880|
|Geben Sie den Zeitraum (in Minuten) an, für den ein Benutzer eine letzte Countdownbenachrichtigung erhält, bevor ein Gerät neu gestartet wird|60|
|Legen Sie fest, wie häufig dem Benutzer nach dem Stichtag Erinnerungen angezeigt werden, bevor ein Gerät neu gestartet wird (in Minuten)|30|
|Wenn für eine Bereitstellung ein Neustart erforderlich ist, dem Benutzer ein Dialogfeld anstelle einer Popupbenachrichtigung anzeigen|Ja|

Das Gerät wird zwei Tage (**2.880** Minuten) nach dem Stichtag neu gestartet. Eine Stunde (**60** Minuten) vor dem Neustart wird dem Benutzer ein Countdown angezeigt, den er nicht schließen und für den er keine erneute Erinnerung auswählen kann. Bei dieser Konfiguration können 47 Stunden lang Erinnerungen angezeigt werden (`(2880 - 60) / 60`). Das Softwarecenter zeigt **30** Minuten nach dem Stichtag die erste Erinnerung an. Es werden maximal 92 zusätzliche Erinnerungen alle **30 Minuten** angezeigt. Die Erinnerung erscheint nicht in einer Benachrichtigung, die nach wenigen Sekunden wieder ausgeblendet wird, sondern in einem Fenster auf dem Bildschirm.

## <a name="device-restart-notifications-version-1902"></a>Benachrichtigungen zum Geräteneustart (Version 1902)

<!--3555947-->
In einigen Fällen werden Benutzern Windows-Popupbenachrichtigungen über einen Neustart oder eine erforderliche Bereitstellung nicht angezeigt. So haben sie nicht die Möglichkeit, eine erneute Erinnerung anzufordern. Dieses Verhalten kann zu Problemen für den Benutzer führen, wenn der Client einen Stichtag erreicht.

Wenn Softwareänderungen erforderlich sind oder Bereitstellungen einen Neustart erfordern, haben Sie ab Version 1902 die Möglichkeit, ein nachdrücklicheres Dialogfeld zu verwenden.

Aktivieren Sie in der Gruppe der Clienteinstellungen [Computerneustart](#client-settings) die folgende Option: **Wenn für eine Bereitstellung ein Neustart erforderlich ist, dem Benutzer ein Dialogfeld anstelle einer Popupbenachrichtigung anzeigen**  

Durch die Konfiguration dieser Clienteinstellung ändert sich die Benutzeroberfläche für alle erforderlichen Bereitstellungen, in denen ein Neustart per Popupbenachrichtigung gefordert wird:

![Popupbenachrichtigung, dass ein Neustart erforderlich ist](media/3555947-restart-toast-initial.png)  

Im eindringlicheren Softwarecenter-Dialogfeld:

![Dialogfeld zum Neustart des Computers](media/3976435-proactive-user-restart-notification.png)

Wenn der Benutzer das Gerät nach der Installation nicht neu gestartet hat, erhält er eine Benachrichtigung als Erinnerung. Diese temporäre Erinnerung wird für den Benutzer entsprechend der Clienteinstellung angezeigt: **Temporäre Benachrichtigung für Benutzer anzeigen, in der auf das Intervall (in Minuten) bis zum Abmelden des Benutzers oder Neustart des Computers hingewiesen wird**. Diese Einstellung gibt die Gesamtzeit an, innerhalb derer der Benutzer den Computer neu starten muss, bevor ein Neustart erzwungen wird.

- Temporäre Benachrichtigung bei Verwendung von Popupbenachrichtigungen:

  ![Popupbenachrichtigung über ausstehenden Neustart](media/3555947-restart-toast.png)

- Temporäre Benachrichtigung bei Verwendung des Softwarecenter-Dialogfelds, kein Popup:

  ![Softwarecenter-Benachrichtigung über ausstehenden Neustart mit Schaltfläche „Erneut erinnern“](media/3555947-1902-hide-notification.png)

Wenn der Benutzer nach der temporären Benachrichtigung keinen Neustart ausführt, wird die finale Benachrichtigung mit Countdown ausgegeben; diese kann nicht geschlossen werden. Der Zeitpunkt, zu dem die finale Benachrichtigung angezeigt wird, basiert auf der Clienteinstellung: **Nicht vom Benutzer schließbares Dialogfeld anzeigen, in der das Countdownintervall (in Minuten) bis zum Abmelden des Benutzers oder Neustart des Computers angezeigt wird**. Wenn die Einstellung z. B. auf 60 festgelegt ist, wird die finale Benachrichtigung für den Benutzer eine Stunde vor dem Erzwingen eines Neustarts angezeigt:

![Softwarecenter-Benachrichtigung mit finalem Countdown](media/3555947-1902-final-countdown.png)

Die folgende Einstellung muss eine kürzere Dauer als das kürzeste [Wartungsfenster](../manage/collections/use-maintenance-windows.md) aufweisen, das auf den Computer angewendet wird:

- **Temporäre Benachrichtigung für Benutzer anzeigen, in der auf das Intervall (in Minuten) bis zum Abmelden des Benutzers oder Neustart des Computers hingewiesen wird**
- **Nicht vom Benutzer schließbares Dialogfeld anzeigen, in der das Countdownintervall (in Minuten) bis zum Abmelden des Benutzers oder Neustart des Computers angezeigt wird**

> [!IMPORTANT]
> In Configuration Manager 1902 ersetzt das Dialogfeld unter bestimmten Umständen keine Popupbenachrichtigungen. Installieren Sie zur Behebung dieses Problems das [Updaterollup für Configuration Manager Version 1902](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902). <!--4404715-->

## <a name="log-files"></a>Protokolldateien

Probleme beim Geräteneustart können mithilfe von **RebootCoordinator.log** und **SCNotify.log** behandelt werden. Je nach verwendeter Bereitstellung müssen Sie möglicherweise weitere [Protokolldateien](../../plan-design/hierarchy/log-files.md) des Clients verwenden.

## <a name="next-steps"></a>Nächste Schritte

- [Konfigurieren von Clienteinstellungen](configure-client-settings.md)
- Einstellungen für die **Benutzerfreundlichkeit** bei der [Anwendungsbereitstellung](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux)
- [Benutzerbenachrichtigungen für erforderliche Bereitstellungen](../../../apps/deploy-use/deploy-applications.md#bkmk_notify)
