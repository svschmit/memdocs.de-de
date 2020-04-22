---
title: Überwachen des Integritätsstatus
titleSuffix: Configuration Manager
description: In diesem Artikel wird die Funktionsweise der Überwachung des Integritätsstatus in Desktop Analytics erläutert.
ms.date: 01/16/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 343dbe2a-597c-4719-b7ac-45b1f39b49ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 359fdec13ee6bfd43e66d4bf9cec70c5a3188a32
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693048"
---
# <a name="health-status-monitoring-in-desktop-analytics"></a>Überwachen des Integritätsstatus in Desktop Analytics

Verwenden Sie beim [Bereitstellen eines Updates für die Produktion](deploy-prod.md) Desktop Analytics, um den Integritätsstatus Ihrer Geräte zu überwachen. In diesem Artikel wird ausführlich erläutert, wie die Integritätsüberwachung funktioniert.

Weitere Informationen zum Verwenden dieser Funktion finden Sie unter [Überwachen der Integrität aktualisierter Geräte](deploy-prod.md#bkmk_monitor).

![Screenshot der Seite „System überwachen“ in Desktop Analytics](media/monitor-health.png)

> [!NOTE]  
> Desktop Analytics sammelt nur Integritätsdaten von Geräten, die Nutzungsdaten liefern, welche als Bezugspunkt verwendet werden können. Das heißt, es sind keine Geräte unter Windows 7 und Windows 10 eingeschlossen, für die keine Übermittlung von Diagnosedaten auf der Ebene „Erweitert (begrenzt)“ festgelegt ist. Wenn für mehr als 10 % der Windows 10-Geräte die Übermittlung von Diagnosedaten auf anderen Ebenen als „Erweitert (begrenzt)“ konfiguriert ist, wird auf der Seite **System überwachen** im Bannerbereich eine Warnung angezeigt.  

Wenn Sie weitere Informationen zu einer bestimmten App anzeigen möchten, wählen Sie diese in der Liste aus.

## <a name="apps"></a>Apps

### <a name="health-status-factors"></a>Faktoren für den Integritätsstatus

![Faktoren des Integritätsstatus für eine App in Desktop Analytics](media/monitor-health-status-factors.png)

Desktop Analytics überwacht die folgenden Faktoren des Integritätsstatus für Apps:

- **% Geräte mit Abstürzen**: Die Anzahl der Geräte, auf denen diese konkrete App in den letzten zwei Wochen abgestürzt ist, dividiert durch die Anzahl der Geräte, auf denen die App verwendet wurde. In dieser Ansicht können Sie feststellen, ob die Stabilität der App unter der neuen Betriebssystemversion zugenommen hat oder gesunken ist. Desktop Analytics berechnet diesen Prozentsatz für die folgenden Gruppen:  

  - **Nach Aktualisierung**: Geräte, die auf die im Bereitstellungsplan angegebene Zielversion des Betriebssystems aktualisiert wurden. Um die Anzahl der Objekte mit unzureichenden Daten zu senken, sammelt Desktop Analytics diese Daten für alle aktualisierten Geräte. Zu dieser Gruppe zählen auch die Geräte, die nicht im Bereitstellungsplan enthalten sind.  

  - **Vor Aktualisierung**: Geräte, auf denen eine ältere als die im Bereitstellungsplan angegebene Betriebssystemversion installiert ist. Diese Liste enthält keine Geräte, auf denen Windows 7 ausgeführt wird.  

  - **Gewerbl. Durchschn.** : Die durchschnittliche Absturzrate für alle kommerziellen Geräte. Dieser Durchschnitt wird für *alle* Versionen der App berechnet. Wird für Ihre Version eine Absturzrate über dem gewerblichen Durchschnitt verzeichnet, ist möglicherweise eine stabilere Version verfügbar.  

- **% Sitzungen mit Abstürzen**: Ähnlich wie die vorherige Gruppe. Hier wird jedoch der Prozentsatz der Sitzungen mit Abstürzen in den letzten zwei Wochen angegeben.  

Um den Integritätsstatus einer App zu ermitteln, benötigt Desktop Analytics Daten von mindestens 20 Geräten. Andernfalls wird für die App **Unzureichende Daten** gemeldet. Der Dienst berechnet den Integritätsstatus anhand der *Sitzungsabsturzrate* für diese Geräte. Die Geräteabsturzrate wird nur zu Informationszwecken angegeben. Sie wird in der Berechnung des Integritätsstatus nicht berücksichtigt.

### <a name="usage"></a>Verwendung

<!-- 5533890 -->

- **Aktive Geräte:** Dieser Wert gibt die Anzahl der Geräte an, auf denen ein Benutzer die ausgewählte App innerhalb der letzten zwei Wochen gestartet hat. Er basiert auf den Geräten im ausgewählten Bereitstellungsplan, auf denen die Zielversion von Windows 10 ausgeführt wird.

- **Sitzungen:** Dieser Wert gibt an, wie oft ein Benutzer die ausgewählte App unter der Windows-Zielversion gestartet hat.

### <a name="additional-tabs"></a>Zusätzliche Registerkarten

Am unteren Rand der Seite mit den App-Details finden Sie die folgenden drei Registerkarten, die hilfreich bei Problembehandlung sein können:

- **Andere Versionen**: Eine Liste alternativer Versionen dieser App. Für jede Version werden die relativen Änderungen der Absturzraten in Ihrer Organisation und des gewerblichen Durchschnitts angezeigt. Wenn Sie eine neuere Version der App mit einer niedrigeren Absturzrate ermitteln, empfiehlt es sich möglicherweise, die App zu aktualisieren.  

    Außerdem wird angezeigt, ob weitere Informationen zur Version vorliegen. Weitere Informationen finden Sie unter [Bewertung der Kompatibilität](compat-assessment.md).  

- **Top-Probleme**: Eine Liste der am häufigsten auftretenden Fehler-IDs nach Anzahl der Instanzen. Eine Fehler-ID identifiziert die dem Absturz zugeordnete Stapelüberwachung. Sie können diese ID angeben, wenn Sie beim App-Anbieter Supportleistungen anfordern.  

- **Aktuelle Abstürze**:  Eine Liste der Geräte, auf denen die App vor Kurzem abgestürzt ist. Sie können nach Fehler-ID und anderen Kriterien filtern. Nutzen Sie diese Informationen für die Fehlerbehebung, indem Sie Protokolle erfassen oder Fehlerkorrekturen auf bestimmte Geräte anwenden, bevor Sie eine umfassendere Bereitstellung versuchen.  

Wenn Sie eine schwerwiegende Integritätsregression feststellen, die Sie nicht beheben können, ändern Sie die **Upgradeentscheidung** der App in **Nicht möglich**. Durch diese Aktion wird die künftige Bereitstellung des Updates auf Geräten mit diesem Objekt verhindert.

## <a name="see-also"></a>Weitere Informationen:

- [Kompatibilitätsbewertung in Desktop Analytics](compat-assessment.md)  

- [Bereitstellen für die Produktion mit Desktop Analytics](deploy-prod.md)  
