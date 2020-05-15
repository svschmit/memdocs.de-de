---
title: Bereitstellen für die Produktion
titleSuffix: Configuration Manager
description: Dieser Artikel bietet eine Anleitung für das Bereitstellen in einer Desktop Analytics-Produktionsgruppe.
ms.date: 06/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 0a7ffe8eea1048e696ce7dd254d58364226efc58
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268782"
---
# <a name="how-to-deploy-to-production-with-desktop-analytics"></a>Bereitstellen für die Produktion mit Desktop Analytics

Nachdem Sie die [Pilotbereitstellung](deploy-pilot.md) durchgeführt und den Status Ihrer Objekte überprüft haben, können Sie die weitere Produktionsumgebung aktualisieren.

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]

Die Bereitstellung von Updates auf Produktionsgeräten lässt sich in drei Hauptteile unterteilen:

1. [Überprüfen von Objekten, für die eine Upgradeentscheidung erforderlich ist](#bkmk_review): Um Geräte auf die Bereitstellung in der Produktionsumgebung vorzubereiten, muss die Upgradeentscheidung für deren Objekte auf **Bereit** oder **Bereit, Wartung erforderlich** festgelegt sein.  

2. [Bereitstellen auf vorbereiteten Geräten](#bkmk_deploy) Verwenden Sie Configuration Manager zum Aktualisieren von vorbereiteten Geräten. Desktop Analytics stellt eine Liste der Geräte zur Verfügung, die in der Produktionsumgebung bereitgestellt werden können, sowie Berichte zur Überwachung des Erfolgs der Bereitstellung.  

3. [Überwachen der Integrität aktualisierter Geräte](#bkmk_monitor): Im Verlauf der Updatebereitstellung können Sie die Integrität wichtiger Objekte überwachen. Wenn ein Eingriff erforderlich ist, analysieren und beheben Sie diese Probleme. Wenn Sie feststellen, dass die Probleme nicht behoben werden können, unterbinden Sie die Bereitstellung auf den betroffenen Geräten, indem Sie deren Upgradeentscheidung auf **Nicht möglich** festlegen.  

> [!NOTE]  
> Wenn Sie sicher sind, dass die Pilotbereitstellung erfolgreich ist, können Sie jederzeit mit der Produktionsbereitstellung beginnen. Es ist nicht erforderlich, dass alle Pilotgeräte erst den Status „Abgeschlossen“ erreichen.  



## <a name="review-assets-that-need-an-upgrade-decision"></a><a name="bkmk_review"></a> Überprüfen von Objekten, für die eine Upgradeentscheidung erforderlich ist

Desktop Analytics führt Sie durch den Prozess der Überprüfung Ihrer Objekte für die Produktionsbereitstellung. Wechseln Sie im Azure-Portal zu **Bereitstellungspläne**, wählen Sie einen Bereitstellungsplan und im linken Menü **Produktion vorbereiten** aus.

![Screenshot der Ansicht „Produktion vorbereiten“ in Desktop Analytics](media/prepare-production.png)

Überprüfen Sie den Status Ihrer Apps. Verwenden Sie diese Informationen, um die Upgradeentscheidung für jedes dieser Objekte festzulegen.

Verwenden Sie die einzelnen Registerkarten, um den Status der Apps zu überprüfen. Auf den einzelnen Registerkartenansichten können Sie die Ergebnisse filtern, um Geräte anzuzeigen, die für das Upgrade infrage kommen, einen Eingriff erfordern, gemischte Ergebnisse oder einen unbestimmten Zustand aufweisen.

Wählen Sie **Ziele werden erreicht** aus, um die Ansicht nach Objekten zu filtern, bei denen eine Produktionsbereitstellung basierend auf den folgenden Kriterien wahrscheinlich möglich ist:

- Risiko: eine Bewertung bekannter Risiken vor dem Upgrade für die Aktualisierung von Geräten, auf denen dieses Objekt installiert ist  

- Integritätsstatus: eine Bewertung nach dem Upgrade von Geräten in anderen Bereitstellungen und des Auftretens von Problemen nach der Installation des Updates. Weitere Informationen zur Integrität finden Sie unter [Überwachen der Integrität aktualisierter Geräte](#bkmk_monitor).  

Um ein Objekt für ein Upgrade zu genehmigen, wählen Sie den Namen in der Liste und dann eine der folgenden Optionen aus der Liste **Upgradeentscheidung** aus:

- Überprüfung wird durchgeführt
- Sind Sie bereit
- Bereit (mit Wartung)
- Nicht möglich
- Nicht überprüft

Um diesen Wert für mehrere Apps gleichzeitig festzulegen, verwenden Sie **Dieses Element auswählen** in der ersten Spalte, und wählen Sie dann **Upgradeentscheidung festlegen** aus.

![Option „Upgradeentscheidung festlegen“ für mehrere Apps](media/prep-prod-set-upgrade-decision.png)

Wählen Sie **Keine Daten** aus, um Objekte anzuzeigen, die nicht klassifiziert werden konnten. Bei diesen Objekten handelt es sich in der Regel um Objekte, bei denen die Abdeckung nicht ausreicht, um mit Desktop Analytics eine Analyse des Risikos oder des Integritätsstatus durchzuführen. Um die Abdeckung zu verbessern, fügen Sie dem Pilotprojekt zusätzliche Geräte mit diesen Objekten hinzu, oder bitten Sie Pilotbenutzer, diese Objekte zu testen.

Möglicherweise weisen Objekte auch den Status **Eingreifen erforderlich** oder **Gemischte Ergebnisse** auf. Bei diesen Objekten ist möglicherweise eine zusätzliche Überprüfung erforderlich, bevor Sie die Upgradeentscheidung treffen können.

Überprüfen Sie alle Apps. Sobald ein bestimmtes Gerät eine positive Upgradeentscheidung für alle Objekte aufweist, ändert sich dessen Status in „Bereit für die Produktion“. Die aktuelle Anzahl wird auf der Hauptseite für den Bereitstellungsplan angezeigt, wenn Sie den dritten Bereitstellungsschritt **Bereitstellen** auswählen.


## <a name="deploy-to-devices-that-are-ready"></a><a name="bkmk_deploy"></a> Bereitstellen auf vorbereiteten Geräten

Configuration Manager erstellt anhand der Daten aus Desktop Analytics eine Sammlung für die Produktionsbereitstellung. Stellen Sie die Tasksequenz nicht mithilfe einer herkömmlichen Bereitstellung bereit. Gehen Sie wie folgt vor, um eine integrierte Desktop Analytics-Bereitstellung zu erstellen:

Wenn Sie den empfohlenen Prozess zum [Bereitstellen auf Pilotgeräten](deploy-pilot.md#deploy-to-pilot-devices) befolgt haben, kann jetzt die stufenweise Bereitstellung mit Configuration Manager ausgeführt werden. Sobald Sie Objekte als *Bereit* markieren, werden diese Geräte von Desktop Analytics automatisch mit Configuration Manager synchronisiert. Diese Geräte werden dann der Produktionssammlung hinzugefügt. Wenn die stufenweise Bereitstellung zur zweiten Phase wechselt, erfolgt die Upgradebereitstellung dieser Produktionsgeräte.

Wenn Sie die stufenweise Bereitstellung mit **Zweite Phase der Bereitstellung manuell starten** konfiguriert haben, müssen Sie die nächste Stufe manuell starten. Weitere Informationen finden Sie unter [Verwalten und Überwachen stufenweiser Bereitstellungen](../osd/deploy-use/manage-monitor-phased-deployments.md#bkmk_move).

Wenn Sie eine in Desktop Analytics integrierte einzelne Bereitstellung für die Pilotsammlung erstellt haben, müssen Sie diesen Vorgang wiederholen, um die Bereitstellung für die Produktionssammlung durchzuführen.


### <a name="address-deployment-alerts"></a>Behandeln von Bereitstellungswarnungen

Wie bei der Pilotbereitstellung werden bei Desktop Analytics alle Probleme, die Ihre Aufmerksamkeit erfordern, während der Produktionsbereitstellung angezeigt. Wechseln Sie in Desktop Analytics zum Bereitstellungsplan, und wählen Sie im linken Menü **Bereitstellungsstatus** aus. In der Ansicht „Bereitstellungsstatus“ werden Geräte in den folgenden Kategorien aufgelistet:  

- Nicht gestartet
- In Bearbeitung
- Abgeschlossen
- Eingreifen erforderlich – Geräte (sortiert nach Gerätename)
- Eingreifen erforderlich – Probleme (sortiert nach Problemtyp)

![Screenshot des Status der Produktionsbereitstellung in Desktop Analytics](media/prod-deployment-status.png)


## <a name="monitor-the-health-of-updated-devices"></a><a name="bkmk_monitor"></a> Überwachen der Integrität aktualisierter Geräte

Auf der Seite **Produktion vorbereiten** finden Sie Informationen, die Ihnen beim Treffen der Upgradeentscheidungen für Ihre Objekte helfen sollen. Auf dieser Seite werden standardmäßig nur die Objekte angezeigt, die noch nicht den Zustand **Bereit** aufweisen. Auf der Seite **Integrität überwachen** werden Integritätsprobleme bei allen relevanten Objekten angezeigt, auch wenn diese Objekte als **Bereit** gekennzeichnet sind. Wenn Probleme auftreten, können Sie das Problem analysieren und beheben oder die Upgradeentscheidung in **Nicht möglich** ändern. Wenn Sie die Upgradeentscheidung ändern, verhindert diese Aktion zukünftige Upgrades auf Geräten mit diesem Objekt.

Filtern Sie diese Seite nach Objekten mit den folgenden Integritätszuständen:

| Integritätsstatusfilter | Beschreibung |
|----------------------|-------------|
| **Eingreifen erforderlich** | (Standardfilter) Desktop Analytics erkennt eine statistisch signifikante Regression der Integritätsmetrik für dieses Objekt.
| **Ziele werden erreicht** | Desktop Analytics erkennt keine Regression im Verhalten. |
| **Unzureichende Daten** | Desktop Analytics verfügt nicht über genügend Daten zu diesem Objekt, um Empfehlungen abzugeben. |
| **Keine Daten** | Für dieses Objekt sind noch keine Nutzungsdaten verfügbar. |

Wählen Sie den aktuellen Filter aus, um eine ungefilterte Ansicht aller Objekte anzuzeigen. Mit dieser Aktion wird der Filter entfernt.

> [!NOTE]  
> Um die Anzahl von Objekten mit unzureichenden Daten zu verringern, überwacht Desktop Analytics die Objekte auf allen Geräten, die auf die in Ihrem Bereitstellungsplan angegebene Windows-Zielversion aktualisiert wurden. Diese Geräte enthalten auch Geräte, die nicht im jeweiligen Bereitstellungsplan enthalten sind.  

Die Standardsortierreihenfolge ist die Anzahl der Geräte, bei denen ein Vorfall bei dem jeweiligen Objekt aufgetreten ist, sodass Sie schnell feststellen können, welche die meisten Probleme verursachen. Wenn Sie beispielsweise **Apps**anzeigen, wird nach **Geräte mit App-Abstürzen in den letzten zwei Wochen** sortiert.

Wenn Sie die Integrität aller Objekte einschließlich der Objekte mit unzureichenden Daten überprüfen möchten, die Desktop Analytics keine statistischen Rückschlüsse erlauben, gehen Sie wie folgt vor:

1. Wählen Sie das Dropdownmenü in der Spalte **Geräte mit Vorfällen in den letzten zwei Wochen** aus. Fügen Sie nur den Objekten einen Filter hinzu, bei denen bei einer Mindestanzahl von Geräten Vorfälle aufgetreten sind. Zeigen Sie z. B. Elemente mit Werten **größer als** 100 an.  

2. Wählen Sie das Dropdownmenü in der Spalte **Geräte mit Vorfällen in den letzten zwei Wochen** aus, und wählen Sie als Sortierung **Absteigend**.  

    Die resultierende Ansicht zeigt die Objekte mit der höchsten Rate von Vorfällen bei einer Mindestanzahl von Vorfällen.  

3. Wählen Sie ein Objekt aus, um weitere Details zu erhalten, oder ändern Sie dessen Upgradeentscheidung.  

Weitere Informationen finden Sie unter [Überwachen des Integritätsstatus](health-status-monitoring.md).
