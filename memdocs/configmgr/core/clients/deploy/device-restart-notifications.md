---
title: Benachrichtigungen zum Geräteneustart
titleSuffix: Configuration Manager
description: Hier wird das Verhalten von Benachrichtigungen zum Neustart für diverse Clienteinstellungen in Configuration Manager beschrieben.
ms.date: 08/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5ef1bff8-9733-4b5a-b65f-26b94accd210
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5b6d383b2d5904f4d31fff5f549127dc21c39f29
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693958"
---
# <a name="device-restart-notifications-in-configuration-manager"></a>Benachrichtigungen zum Geräteneustart in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Die Benachrichtigungen, die ein Benutzer zu einem ausstehenden Geräteneustart erhält, können je nach [Clienteinstellungen für den Computerneustart](about-client-settings.md#computer-restart) und verwendeter Version von Configuration Manager variieren. Dieser Artikel unterstützt Administratoren bei der Bestimmung der Benutzeroberfläche bei Benachrichtigungen zu einem ausstehenden Geräteneustart.

>[!NOTE]
> - Der Schwerpunkt dieses Artikels liegt auf den Clienteinstellungen in Configuration Manager, Version 1902 und Version 1906.


## <a name="deployment-types-for-restart-notifications"></a>Bereitstellungstypen für Benachrichtigungen zum Neustart

Die [Clienteinstellungen für den Computerneustart](about-client-settings.md#computer-restart) ändern die Benutzeroberfläche für alle erforderlichen Bereitstellungen folgender Arten, die einen Neustart erfordern:

- [Anwendung](../../../apps/deploy-use/deploy-applications.md)
- [Tasksequenz](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
- [Softwareupdate](../../../sum/deploy-use/deploy-software-updates.md)

## <a name="restart-notification-types"></a>Typen von Benachrichtigung zum Neustart

Wenn ein Neustart erforderlich ist, erhält der Endbenutzer eine Benachrichtigung über den bevorstehenden Neustart. Es gibt vier allgemeine Benachrichtigungen, die Benutzer erhalten können:

**Popupbenachrichtigung** mit der Information über einen erforderlichen Neustart. Die Informationen in der Popupbenachrichtigung können unterschiedlich sein, je nachdem, welche Version von Configuration Manager Sie ausführen. Dieser Benachrichtigungstyp ist für das Windows-Betriebssystem nativ, und möglicherweise wird dieser Benachrichtigungstyp auch in Drittanbietersoftware verwendet.

![Popupbenachrichtigung über ausstehenden Neustart](media/3555947-restart-toast.png)

Softwarecenter-Benachrichtigung mit einer Option für eine erneute Erinnerung, in der die verbleibende Zeit bis zum Erzwingen eines Neustarts angegeben wird. Die Benachrichtigung kann je nach Configuration Manager-Version variieren.

![Softwarecenter-Benachrichtigung über ausstehenden Neustart mit Schaltfläche „Erneut erinnern“](media/3976435-snooze-restart-countdown.png)

Softwarecenter-Benachrichtigung mit finalem Countdown, die vom Benutzer nicht geschlossen werden kann. Die Schaltfläche „Erneut erinnern“ ist ausgegraut.

![Softwarecenter-Benachrichtigung mit finalem Countdown](media/3976435-final-restart-countdown.png)

Wenn der Benutzer proaktiv erforderliche Software installiert, die vor einem Stichtag neu gestartet werden muss, wird eine andere Benachrichtigung angezeigt. Die folgende Benachrichtigung wird ausgegeben, wenn die Einstellung für die Benutzeroberfläche Benachrichtigungen zulässt und Sie keine Popupbenachrichtigungen für die Bereitstellung verwenden. Weitere Informationen zum Konfigurieren dieser Einstellungen finden Sie unter [Deployment **User Experience** settings](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux) (Bereitstellungseinstellungen für [Benutzeroberfläche])und [Benutzerbenachrichtigungen für erforderliche Bereitstellungen](../../../apps/deploy-use/deploy-applications.md#bkmk_notify).

![Benachrichtigung für proaktiv installierte Software](media/3976435-proactive-user-restart-notification.png)

- Wenn Sie keine Popupbenachrichtigungen verwenden, ähnelt das Dialogfeld für als **Verfügbar** markierte Software proaktiv installierter Software.

  - Bei als **Verfügbar** markierter Software enthält die Benachrichtigung keine Frist für den Neustart, und der Benutzer kann das Intervall für eine erneute Erinnerung selbst wählen. Weitere Informationen finden Sie unter [Genehmigungseinstellungen](../../../apps/deploy-use/deploy-applications.md#bkmk_approval).

    ![Bei Software, die als „Verfügbar“ markiert ist, ist in der Benachrichtigung keine Frist für einen Neustart angegeben.](media/3555947-deployment-marked-available-restart.png)

## <a name="device-restart-notifications-in-version-1902"></a>Benachrichtigungen zum Geräteneustart in Version 1902

<!--3555947-->
In einigen Fällen werden Benutzern Windows-Popupbenachrichtigungen über einen Neustart oder eine erforderliche Bereitstellung nicht angezeigt. So haben sie nicht die Möglichkeit, eine erneute Erinnerung anzufordern. Dieses Verhalten kann zu Problemen für den Benutzer führen, wenn der Client einen Stichtag erreicht.

Wenn Softwareänderungen erforderlich sind oder Bereitstellungen einen Neustart erfordern, haben Sie ab Version 1902 die Möglichkeit, ein nachdrücklicheres Dialogfeld zu verwenden.

Aktivieren Sie in der Gruppe der Clienteinstellungen [Computerneustart](about-client-settings.md#computer-restart) die folgende Option: **Wenn für eine Bereitstellung ein Neustart erforderlich ist, dem Benutzer ein Dialogfeld anstelle einer Popupbenachrichtigung anzeigen**  

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

## <a name="device-restart-notifications-starting-in-version-1906"></a>Benachrichtigungen zum Geräteneustart ab Version 1906
<!--3976435-->
Einige Administratoren bevorzugen häufige Neustartbenachrichtigungen sowie ein kurzes Zeitfenster, für das ein Neustart aufgeschoben werden kann. Andere Administratoren gestatten Benutzern, den Neustart für eine längere Zeit aufzuschieben, und Benutzer sollen weniger oft über den ausstehenden Neustart benachrichtigt werden. Configuration Manager, Version 1906 bietet Administratoren zusätzliche Kontrolle über die Terminierung und Häufigkeit von Neustartbenachrichtigungen. Die folgenden Elemente wurden in Version 1906 eingeführt, um dem Administrator eine umfassendere Kontrolle zu ermöglichen:

- Die Option **Dauer für erneute Erinnerung für Countdownbenachrichtigungen zum Computerneustart (Minuten) angeben** wurde den [Clienteinstellungen für den Computerneustart](about-client-settings.md#computer-restart) hinzugefügt.
- Der maximale Wert für **Temporäre Benachrichtigung für Benutzer anzeigen, in der auf das Intervall (in Minuten) bis zum Abmelden des Benutzers oder Neustart des Computers hingewiesen wird** wird von 1.440 Minuten (24 Stunden) auf 20.160 Minuten (zwei Wochen) heraufgesetzt.
- Dem Benutzer wird keine Statusanzeige in der Neustartbenachrichtigung angezeigt, bis der ausstehende Neustart weniger als 24 Stunden bevorsteht.

### <a name="notifications-when-required-software-is-installed-at-or-after-the-deadline"></a>Benachrichtigungen, wenn erforderliche Software am oder nach dem Stichtag installiert wird

Wenn erforderliche Software am oder nach dem Stichtag installiert wird, werden Benutzern Benachrichtigungen entsprechend den ausgewählten Clienteinstellungen angezeigt.

Wenn die Einstellung **Wenn für eine Bereitstellung ein Neustart erforderlich ist, dem Benutzer ein Dialogfeld anstelle einer Popupbenachrichtigung anzeigen** auf folgenden Wert festgelegt ist:

- **Nein**: Popupbenachrichtigungen werden verwendet, bis die finale Benachrichtigung mit Countdown erreicht wird.
- **Ja**: Eine Softwarecenter-Benachrichtigung wird angezeigt.
  - Wenn der Neustart noch mehr als 24 Stunden aussteht, wird ein geschätzter Zeitpunkt für den Neustart angezeigt. Die Terminierung dieser Benachrichtigung basiert auf der Einstellung: **Temporäre Benachrichtigung für Benutzer anzeigen, in der auf das Intervall (in Minuten) bis zum Abmelden des Benutzers oder Neustart des Computers hingewiesen wird**.

     ![Der Neustartzeitpunkt liegt mehr als 24 Stunden entfernt](media/3976435-notification-greater-than-24-hours.png)

  - Wenn ein Neustart weniger als 24 Stunden aussteht, wird eine Statusanzeige angezeigt. Die Terminierung dieser Benachrichtigung basiert auf der Einstellung: **Temporäre Benachrichtigung für Benutzer anzeigen, in der auf das Intervall (in Minuten) bis zum Abmelden des Benutzers oder Neustart des Computers hingewiesen wird**

     ![Der Neustartzeitpunkt liegt weniger als 24 Stunden entfernt](media/3976435-notification-less-than-24-hours.png)

Wenn der Benutzer die Schaltfläche **Erneut erinnern** auswählt, wird nach Ablauf des Erinnerungszeitraums eine weitere temporäre Erinnerung ausgegeben, vorausgesetzt, der finale Countdown wurde noch nicht erreicht. Die Terminierung dieser nächsten Benachrichtigung basiert auf der Einstellung: **Dauer für erneute Erinnerung für Countdownbenachrichtigungen zum Computerneustart (Stunden) angeben**. Wenn der Benutzer **Erneut erinnern** auswählt und der Erinnerungszeitraum eine Stunde beträgt, wird er nach 60 Minuten erneut erinnert, es sei denn, der finale Countdown wurde noch nicht erreicht.

Bei Erreichen des finalen Countdowns wird für den Benutzer eine Benachrichtigung angezeigt, die nicht geschlossen werden kann. Die Statusanzeige ist rot, und der Benutzer kann nicht **Erneut erinnern** auswählen.

![Softwarecenter-Benachrichtigung mit finalem Countdown in Version 1906](media/3976435-1906-final-restart-countdown.png)

### <a name="the-user-proactively-installs-before-the-deadline"></a>Der Benutzer führt die Installation proaktiv vor dem Stichtag aus

Wenn der Benutzer proaktiv erforderliche Software installiert, die vor einem Stichtag neu gestartet werden muss, wird eine andere Benachrichtigung angezeigt. Weitere Informationen zum Konfigurieren dieser Einstellungen finden Sie unter [Deployment **User Experience** settings](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux) (Bereitstellungseinstellungen für [Benutzeroberfläche]) und [Benutzerbenachrichtigungen für erforderliche Bereitstellungen](../../../apps/deploy-use/deploy-applications.md#bkmk_notify). 

Die folgende Benachrichtigung wird ausgegeben, wenn die Einstellung für die Benutzeroberfläche Benachrichtigungen zulässt und Sie keine Popupbenachrichtigungen für die Bereitstellung verwenden:

![Benachrichtigung für proaktiv installierte Software](media/3976435-proactive-user-restart-notification.png)

Wenn die Frist für die Software abgelaufen ist, ist das unter [Benachrichtigungen, wenn erforderliche Software am oder nach dem Stichtag installiert wird](#notifications-when-required-software-is-installed-at-or-after-the-deadline) beschriebene Verhalten zu beobachten.

## <a name="log-files"></a>Protokolldateien

Probleme mit Geräteneustarts können Sie mithilfe von **RebootCoordinator.log** und **SCNotify.log** behandeln. Je nach verwendeter Bereitstellung müssen Sie auch weitere [Protokolldateien](../../plan-design/hierarchy/log-files.md) des Clients verwenden.

## <a name="next-steps"></a>Nächste Schritte

- [Einführung in die Anwendungsverwaltung](../../../apps/understand/introduction-to-application-management.md)
- [Einführung in die Betriebssystembereitstellung](../../../osd/understand/introduction-to-operating-system-deployment.md)
- [Einführung in die Verwaltung von Softwareupdates](../../../sum/understand/software-updates-introduction.md)
