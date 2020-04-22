---
title: Bereitstellen für die Pilotphase
titleSuffix: Configuration Manager
description: Dieser Artikel bietet eine Anleitung für das Bereitstellen in einer Desktop Analytics-Pilotgruppe.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b0e939b51c464215ac1d4feea539ceb5677a01a6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708268"
---
# <a name="how-to-deploy-to-pilot-with-desktop-analytics"></a>Bereitstellen für die Pilotphase mit Desktop Analytics

Einer der Vorteile von Desktop Analytics besteht darin, dass die kleinste Gruppe von Geräten bestimmt werden kann, die die breiteste Abdeckung von Faktoren bieten. Der Schwerpunkt liegt dabei auf den Faktoren, die für einen Pilotversuch von Windows-Upgrades und -Updates am wichtigsten sind. Indem Sie eine erfolgreichere Durchführung des Pilotversuchs sicherstellen, können Sie schneller und zuverlässiger zu umfassenden Bereitstellungen in der Produktion wechseln.  

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]

## <a name="identify-devices"></a>Identifizieren von Geräten

Im ersten Schritt werden die Geräte identifiziert, die in den Pilotversuch aufgenommen werden sollen. Desktop Analytics empfiehlt Geräte auf der Grundlage der gemeldeten Daten, und Sie können Geräte in der Liste hinzufügen oder ersetzen.

1. Wechseln Sie zum [Desktop Analytics-Portal](https://aka.ms/desktopanalytics), und wählen Sie in der Gruppe „Verwalten“ die Option **Bereitstellungspläne** aus.

1. Wählen Sie einen Bereitstellungsplan aus.

1. Wählen Sie im Menü des Bereitstellungsplans in der Gruppe „Vorbereiten“ die Option **Pilot identifizieren** aus.

Die Daten aus Desktop Analytics werden angezeigt; in diesen wird empfohlen, wie viele Geräte für eine optimale Abdeckung eingeschlossen werden sollten. Dieser Algorithmus basiert hauptsächlich auf der Nutzung wichtiger und kritischer Apps sowie auf dem Umfang der Hardwarekonfigurationen.

Führen Sie für die Liste der zusätzlich empfohlenen Geräte die folgenden Aktionen aus:

- **Alle zu Pilot hinzufügen**: Hiermit werden der Pilotgruppe alle empfohlenen Geräte hinzugefügt.
- **Zu Pilot hinzufügen**: Es werden nur einzelne Geräte hinzugefügt.
- **Ersetzen** Sie bestimmte Geräte im Pilotversuch.

Je mehr Geräte Sie aus der Pilotliste der **empfohlenen** in die der **enthaltenen** Geräte hinzufügen, desto mehr Faktoren decken Sie ab und desto höher ist die Redundanz. Eine höhere Redundanz bedeutet, dass die abgedeckten Ressourcen eine statistisch signifikante Anzahl von Geräten in Ihrer Pilotgruppe ausmachen.

## <a name="global-pilot"></a><a name="bkmk_GlobalPilot"></a>Globaler Pilot

Sie können auch systemweite Entscheidungen darüber treffen, welche Configuration Manager-Sammlungen in Pilotversuche eingeschlossen bzw. aus diesen ausgeschlossen werden sollen. Wählen Sie im Hauptmenü von Desktop Analytics in der Gruppe „Globale Einstellungen“ die Option **Weltweiter Pilot** aus.

Wenn Sie mehrere Configuration Manager-Hierarchien mit derselben Desktop Analytics-Instanz verbinden, wird dem Sammlungsnamen in der Konfiguration des globalen Piloten ein Anzeigename für die Hierarchie vorangestellt. Dieser Name ist die **Anzeigename**-Eigenschaft der Desktop Analytics-Verbindung in der Configuration Manager-Konsole.<!-- 4814075 -->

> [!NOTE]
> Die Unterstützung mehrerer Hierarchien erfordert Configuration Manager-Version 1910 oder höher.

- Schließen Sie keine Sammlungen ein, die mehr als 20% Ihrer gesamten für Desktop Analytics registrierten Geräte enthalten. Wenn Sie eine große Sammlung hinzufügen, wird im Portal eine Warnung angezeigt. Sie können mehrere kleine Sammlungen einschließen, ohne dass eine Warnung angezeigt wird, sollten die Anzahl von Geräten in Ihrem Pilotprojekt jedoch trotzdem mit Bedacht wählen. <!-- 6079184 -->

- Um präzise Pilotempfehlungen für Bereitstellungpläne in einer bestimmten Configuration Manager-Hierarchie zu erhalten, schließen Sie nur Sammlungen aus dieser Hierarchie ein.

### <a name="example"></a>Beispiel

- Sie konfigurieren die Desktop Analytics-Verbindung in Configuration Manager, um die Sammlung **Alle Systeme** als Ziel zu bestimmen. Durch diese Aktion werden alle Clients für den Dienst registriert.

- Außerdem konfigurieren Sie zusätzliche Sammlungen, die mit Desktop Analytics synchronisiert werden sollen:

  - Alle Windows 10-Clients (3.000 Geräte)

  - Alle IT-Geräte (200 Geräte insgesamt, davon 150 mit Windows 10)

  - CEO-Büro (20 Geräte)

- In den Einstellungen für **Weltweiter Pilot** schließen Sie die Sammlungen **Alle Windows 10-Geräte** ein. Sie schließen die Sammlung **CEO-Büro** aus.

- Sie erstellen einen Bereitstellungsplan und wählen die Sammlung **Alle IT-Geräte** als **Zielgruppe** aus. Dieser Bereitstellungsplan soll nur für Geräte in der IT-Abteilung verwendet werden.

- In der Liste **Enthaltene Pilotgeräte** wird die Teilmenge der Geräte angezeigt, die in beiden **Zielgruppen** enthalten sind: **Alle IT-Geräte** und die *Aufnahmeliste* für den weltweiten Piloten: **Alle Windows 10-Clients**. Da nur auf 150 Geräten in der Sammlung **Alle IT-Geräte** Windows 10 ausgeführt wird, enthält diese Liste 150 Geräte.

- Die Liste **Zusätzliche empfohlene Geräte** enthält eine Gruppe von Geräten aus der **Zielgruppe**, die maximale Abdeckung und Redundanz für Ihre wichtigen Objekte bieten. Desktop Analytics schließt aus dieser Liste alle in der *Ausschlussliste* für „Weltweiter Pilot“ enthaltenen Geräte aus: **CEO-Büro**.

## <a name="address-issues"></a>Beheben von Problemen

Überprüfen Sie im Desktop Analytics-Portal die gemeldeten Probleme mit Objekten, welche die Bereitstellung blockieren könnten. Genehmigen Sie dann die vorgeschlagene Korrektur, lehnen Sie sie ab, oder ändern Sie sie. Vor dem Starten der Pilotbereitstellung müssen alle Elemente als **Bereit** oder **Bereit (mit Korrektur)** markiert sein.

1. Wechseln Sie zum [Desktop Analytics-Portal](https://aka.ms/desktopanalytics), und wählen Sie in der Gruppe „Verwalten“ die Option **Bereitstellungspläne** aus.  

2. Wählen Sie einen Bereitstellungsplan aus.  

3. Wählen Sie im Menü des Bereitstellungsplans in der Gruppe „Vorbereiten“ die Option **Piloten vorbereiten** aus.  

4. Überprüfen Sie auf der Registerkarte **Apps** die Apps, für die Ihre Eingabe erforderlich ist.  

5. Wählen Sie für jede App den App-Namen aus. Überprüfen Sie im Informationsbereich die Empfehlung, und wählen Sie die Upgradeentscheidung aus. Wenn Sie **Nicht überprüft** oder **Nicht möglich** auswählen, schließt Desktop Analytics keine Geräte mit dieser App in die Pilotbereitstellung ein. Wenn Sie **Bereit (mit Korrektur)** auswählen, erfassen Sie in **Gegenmaßnahmehinweise** die Maßnahmen, mit denen das Problem adressiert wurde, z.B. *Neuinstallation* oder *vom Hersteller empfohlene Version suchen*.

6. Wiederholen Sie diese Überprüfung für andere Objekte.  

Weitere Informationen zu diesem Überprüfungsprozess finden Sie unter [Kompatibilitätsbewertung](compat-assessment.md).

## <a name="create-software"></a>Erstellen von Software

Erstellen Sie vor dem Bereitstellen von Windows zuerst die Softwareobjekte in Configuration Manager. Weitere Informationen finden Sie unter [Tasksequenz für direktes Windows 10-Upgrade](../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md).

## <a name="deploy-to-pilot-devices"></a>Bereitstellen auf Pilotgeräten

Configuration Manager erstellt anhand der Daten aus Desktop Analytics Sammlungen für die Pilotbereitstellung und die Produktionsbereitstellung. Führen Sie die folgenden Schritte aus, um eine stufenweise Bereitstellung mit Desktop Analytics-Integration zu erstellen und die Integrität der Geräte nach jeder Bereitstellungsphase sicherzustellen:

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, erweitern Sie den Knoten **Desktop Analytics-Wartung**, und wählen Sie den Knoten **Bereitstellungspläne** aus.  

2. Wählen Sie Ihren Bereitstellungsplan aus, und wählen Sie anschließend im Menüband **Bereitstellungsplandetails** aus.  

3. Wählen Sie im Menüband die Option **Stufenweise Bereitstellung erstellen** aus. Dadurch wird der Assistent zum Erstellen der stufenweisen Bereitstellung gestartet.

    > [!Tip]  
    > Wenn Sie eine klassische Bereitstellung mit Tasksequenz ausschließlich für die Pilotsammlung erstellen möchten, wählen Sie in der Kachel **Pilotstatus** die Option **Bereitstellen** aus. Dadurch wird der Assistent zum Bereitstellen von Software gestartet. Weitere Informationen finden Sie unter [Deploy a task sequence](../osd/deploy-use/deploy-a-task-sequence.md).  

4. Geben Sie einen Namen für die Bereitstellung ein, und wählen Sie die zu verwendende Tasksequenz aus. Wählen Sie die Option **Automatisch 2-Phasen-Standardbereitstellung erstellen** aus, und konfigurieren Sie anschließend die folgenden Sammlungen:  

    - **Erste Sammlung**: Suchen Sie die **Pilotsammlung** für diesen Bereitstellungsplan, und wählen Sie sie aus. Die Standardnamenskonvention für diese Sammlung ist `<deployment plan name> (Pilot)`.

    - **Zweite Sammlung**: Suchen Sie die **Produktionssammlung** für diesen Bereitstellungsplan, und wählen Sie sie aus. Die Standardnamenskonvention für diese Sammlung ist `<deployment plan name> (Production)`.

    > [!Note]  
    > Bei Integration mit Desktop Analytics erstellt Configuration Manager automatisch Pilot- und Produktionssammlungen für den Bereitstellungsplan. Bevor Sie diese verwenden können, kann es eine Weile dauern, bis die Sammlungen synchronisiert wurden. Weitere Informationen finden Sie unter [Problembehandlung – Datenlatenz](troubleshooting.md#data-latency).<!-- 4984639 -->
    >
    > Diese Sammlungen sind für Geräte im Desktop Analytics-Bereitstellungsplan reserviert. Diese Sammlungen können nicht manuell geändert werden.<!-- 3866460, SCCMDocs-pr 3544 -->  

5. Beenden Sie den Assistenten, um die stufenweise Bereitstellung zu konfigurieren. Weitere Informationen finden Sie unter [Erstellen von stufenweisen Bereitstellungen mit Configuration Manager](../osd/deploy-use/create-phased-deployment-for-task-sequence.md).

    > [!Note]  
    > Übernehmen Sie die Standardeinstellung für **Diese Phase nach Verzögerung (in Tagen) automatisch starten**. Die folgenden Kriterien müssen erfüllt sein, damit die zweite Phase gestartet werden kann:
    >
    > 1. In der ersten Phase wird das Erfolgskriterium **Bereitstellungserfolg in Prozent** erfüllt. Diese Einstellung wird in der stufenweisen Bereitstellung konfiguriert.
    > 1. Sie müssen in Desktop Analytics Upgradeentscheidungen überprüfen und treffen, um wichtige und kritische Objekte als *Bereit* zu markieren. Weitere Informationen finden Sie unter [Überprüfen von Objekten, für die eine Upgradeentscheidung erforderlich ist](deploy-prod.md#bkmk_review).
    > 1. Desktop Analytics synchronisiert alle Produktionsgeräte, die die Kriterien von *Bereit* erfüllen, mit den Configuration Manager-Sammlungen.

> [!Important]  
> Diese Sammlungen werden auch nach Ändern ihrer Mitgliedschaft weiterhin synchronisiert. Wenn Sie z. B. ein Problem mit einem Objekt feststellen und dieses als **Nicht möglich** markieren, erfüllen Geräte mit diesem Objekt nicht mehr die Kriterien von *Bereit*. Diese Geräte werden aus der Sammlung für die Produktionsbereitstellung entfernt.

## <a name="monitor"></a>Überwachen

### <a name="configuration-manager-console"></a>Configuration Manager-Konsole

Öffnen Sie den Bereitstellungsplan. In der Kachel **Upgradeentscheidungen werden vorbereitet – Gesamtstatus** finden Sie eine Statusübersicht für den Bereitstellungsplan. Dieser Status bezieht sich sowohl auf die Pilotsammlung als auch auf die Produktionssammlung. Geräte können in eine der folgenden Kategorien fallen:

- **Aktuell**: Für die Geräte wurde ein Upgrade auf die Windows-Zielversion für diesen Bereitstellungsplan ausgeführt.

- **Upgradeentscheidung abgeschlossen**: Einer der folgenden Status:

  - Geräte mit beachtenswerten Objekten, die als **Bereit** oder **Bereit (mit Korrektur)** markiert sind

  - Der Gerätestatus ist **Blockiert**, [**Gerät ersetzen**](about-deployment-plans.md#plan-assets) oder **Gerät erneut installieren**.

- **Nicht überprüft**: Geräte mit beachtenswerten Objekten, die als **Nicht überprüft** oder **Überprüfung wird durchgeführt** markiert sind

Der Gerätestatus wird in den Kacheln **Pilotstatus** und **Produktion: Status** durch folgende Aktionen aktualisiert:

- Sie nehmen Änderungen an der Kompatibilitätsbewertung vor.
- Ein Upgrade der Geräte auf die Windows-Zielversion wird ausgeführt.
- Fortschritt der Bereitstellung

Sie können die Configuration Manager-Bereitstellungsüberwachung auf dieselbe Weise wie jede andere Tasksequenzbereitstellung verwenden. Weitere Informationen finden Sie unter [Überwachen von Betriebssystembereitstellungen in System Center Configuration Manager](../osd/deploy-use/monitor-operating-system-deployments.md).

### <a name="desktop-analytics-portal"></a>Desktop Analytics-Portal

Im [Desktop Analytics-Portal](https://aka.ms/desktopanalytics) können Sie den Status von Bereitstellungsplänen überprüfen. Wählen Sie den Bereitstellungsplan aus, und wählen Sie dann **Planübersicht** aus.

![Screenshot der Übersicht über den Bereitstellungsplan in Desktop Analytics](media/deployment-plan-overview.png)

Wählen Sie die Kachel **Pilot** aus. Dort wird der aktuelle Status der Pilotbereitstellung zusammengefasst. In dieser Kachel werden auch Daten zur Anzahl von Geräten angezeigt, die nicht gestartet wurden, die verarbeitet werden oder abgeschlossen wurden oder für die Probleme zurückgegeben werden.

Im Detailbereich von „Pilot“ rechts sind alle Geräte aufgelistet, für die Fehler oder andere Probleme gemeldet werden. Wählen Sie **Überprüfen**, um Details zum gemeldeten Problem abzurufen. Dadurch wird zur Seite **Bereitstellungsstatus** gewechselt.

Auf der Seite **Bereitstellungsstatus** werden Geräte in den folgenden Kategorien aufgelistet:

- Nicht gestartet
- In Bearbeitung
- Abgeschlossen
- Eingreifen erforderlich – Geräte
- Eingreifen erforderlich – Probleme

In den Kategorien **Eingreifen erforderlich** werden dieselben Informationen angezeigt; diese sind jedoch anders sortiert.

Wählen Sie eine bestimmte Liste in einer Ansicht aus, um weitere Details zum festgestellten Problem abzurufen.

Während Sie diese Bereitstellungsprobleme adressieren, wird im Dashboard weiterhin der Fortschritt der Geräte angezeigt. Dieser wird aktualisiert, wenn Geräte von **Eingreifen erforderlich** zu **Abgeschlossen** wechseln.

## <a name="next-steps"></a>Nächste Schritte

Führen Sie den Pilotversuch eine Weile aus, um operative Daten zu sammeln. Fordern Sie Benutzer von Pilotgeräten auf, Apps zu testen.

Wenn die Pilotbereitstellung ihre Erfolgskriterien erfüllt, fahren Sie mit dem nächsten Artikel fort, um eine Bereitstellung für die Produktion auszuführen.
> [!div class="nextstepaction"]  
> [Bereitstellen für die Produktion](deploy-prod.md)  
