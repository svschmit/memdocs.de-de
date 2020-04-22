---
title: Orchestrierungsgruppen
titleSuffix: Configuration Manager
description: Erstellen Sie Orchestrierungsgruppen, und stellen Sie Updates für diese bereit.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: cddbebea-b418-4839-b0a8-7809486c8a4c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d9998f298cee24e9f10b3fd8c5e58d7b76200485
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702978"
---
# <a name="orchestration-groups-in-configuration-manager"></a>Orchestrierungsgruppen in Configuration Manager
<!--3098816-->
*Gilt für: Configuration Manager (Current Branch)*

Ab Configuration Manager, Version 2002 können Sie Orchestrierungsgruppen erstellen. Erstellen Sie eine Orchestrierungsgruppe, um die Bereitstellung von Softwareupdates auf Geräten besser steuern zu können. Viele Serveradministratoren müssen Updates für bestimmte Workloads sehr sorgfältig verwalten und das Verhalten zwischen diesen Updates automatisieren.

Eine Orchestrierungsgruppe bietet Ihnen Flexibilität, sodass Sie Geräte basierend auf einem Prozentsatz, einer bestimmten Anzahl oder einer expliziten Reihenfolge aktualisieren können. Sie können auch ein PowerShell-Skript ausführen, bevor und nachdem die Geräte die Updatebereitstellung ausführen.

Nicht nur Server, sondern auch alle Configuration Manager-Clients können Mitglied einer Orchestrierungsgruppe sein. Die Regeln der Orchestrierungsgruppe gelten für Geräte für alle Bereitstellungen von Softwareupdates in allen Sammlungen, die ein Mitglied dieser Orchestrierungsgruppe enthalten. Andere Verhaltensweisen für Bereitstellungen gelten weiterhin. Beispiel: Wartungsfenster und Bereitstellungszeitpläne.

> [!NOTE]
> In dieser Version von Configuration Manager sind Orchestrierungsgruppen ein Vorabfeature. Wie Sie es aktivieren, erfahren Sie unter [Pre-release features (Features von Vorabreleases)](../../core/servers/manage/pre-release-features.md).  
>
> Das Feature **Orchestrierungsgruppen** ist eine Weiterentwicklung des Features [Servergruppen](service-a-server-group.md). Eine Orchestrierungsgruppe ist ein Objekt in Configuration Manager.

## <a name="orchestration-group-usage-example"></a>Verwendungsbeispiel für Orchestrierungsgruppen

- Als zuständiger Administrator für Softwareupdates verwalten Sie alle Updates für Ihre Organisation.
- Sie verfügen über eine große Sammlung für alle Server und eine große Sammlung für alle Clients. Sie stellen alle Updates für diese Sammlungen bereit.
- Die SQL-Administratoren möchten alle Softwarekomponenten steuern, die auf den SQL Server-Instanzen installiert sind. Diese Administratoren möchten fünf Server in einer bestimmten Reihenfolge patchen. Der aktuelle Prozess besteht darin, dass bestimmte Dienste vor dem Installieren von Updates angehalten und danach neu gestartet werden.
- Sie erstellen eine Orchestrierungsgruppe und fügen alle fünf SQL Server-Instanzen hinzu. Sie fügen auch Skripts für Tasks vor und nach der Installation hinzu. Dafür verwenden Sie die von den SQL-Administratoren bereitgestellten PowerShell-Skripts.
- Während des nächsten Aktualisierungszyklus verwenden Sie das normale Verfahren, um die Softwareupdates zu erstellen und für die große Sammlung von Servern bereitzustellen. Die SQL-Administratoren führen die Bereitstellung aus, und die Orchestrierungsgruppe automatisiert die Reihenfolge und die Dienste.

## <a name="prerequisites"></a>Voraussetzungen

### <a name="site-server-and-permission-prerequisites"></a>Standortserver und Berechtigungsvoraussetzungen
- Damit Sie alle Orchestrierungsgruppen und Updates für diese Gruppen anzeigen können, muss Ihr Konto ein **Hauptadministrator** sein.
   - Die rollenbasierte Verwaltung für Orchestrierungsgruppen ist derzeit nicht verfügbar.
- Aktivieren Sie das Feature **Orchestrierungsgruppen**. Weitere Informationen finden Sie unter [Aktivieren optionaler Features von Updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).
   - Wenn Sie **Orchestrierungsgruppen** aktivieren, deaktiviert der Standort das Feature **Servergruppen**. Dieses Verhalten verhindert Konflikte zwischen den beiden Features.

### <a name="client-prerequisites"></a>Client-Voraussetzungen

- Führen Sie ein Upgrade für die Zielgeräte auf die neueste Version des Konfigurations-Manager-Clients durch.
- Mitglieder einer Orchestrierungsgruppe sollten dem gleichen Standort zugewiesen werden.
- Geräte dürfen sich nicht in mehr als einer Orchestrierungsgruppe befinden.
   - Geräte, die sich bereits in einer Orchestrierungsgruppe befinden, können beim Hinzufügen neuer Mitglieder nicht ausgewählt werden.


## <a name="limitations"></a>Einschränkungen

- Eine Orchestrierungsgruppe kann bis zu 1.000 Mitglieder umfassen.
- Orchestrierungsgruppen funktionieren im Interoperabilitätsmodus nicht. Weitere Informationen finden Sie unter [Interoperabilität zwischen verschiedenen Versionen von Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#bkmk_mixed). <!--6389000-->
- Wenn Updates von Benutzern aus dem Softwarecenter initiiert werden, wird die Orchestrierung umgangen. <!--6362887-->

## <a name="server-groups-are-automatically-updated-to-orchestration-groups"></a>Automatisches Aktualisieren von Servergruppen in Orchestrierungsgruppen

Das Feature **Orchestrierungsgruppen** ist eine Weiterentwicklung des Features [Servergruppen](service-a-server-group.md). Wenn Sie Configuration Manager, Version 2002 oder höher installieren und Servergruppen aktiviert sind, werden die Servergruppen automatisch in Orchestrierungsgruppen verschoben.

## <a name="create-an-orchestration-group"></a>Erstellen einer Orchestrierungsgruppe

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Assets und Konformität**, und wählen Sie den Knoten **Orchestrierungsgruppe** aus.

1. Wählen Sie im Menüband die Option **Orchestrierungsgruppe erstellen** aus, um den **Assistenten zur Erstellung von Orchestrierungsgruppen** zu öffnen.

1. Legen Sie auf der Seite **Allgemein** einen **Namen** und optional eine **Beschreibung** für Ihre Orchestrierungsgruppe fest. Geben Sie Werte für die folgenden Elemente an:
   - **Zeitlimit für Orchestrierungsgruppe (in Minuten):** Das Zeitlimit, innerhalb dessen alle Gruppenmitglieder die Installation von Updates abschließen müssen.
   - **Zeitlimit für Orchestrierungsgruppenmitglied (in Minuten)** : Das Zeitlimit, innerhalb dessen ein einzelnes Gerät in der Gruppe die Installation von Updates abschließen muss.

1. Geben Sie auf der Seite **Mitgliederauswahl** zuerst den **Standortcode** an. Klicken Sie dann auf **Hinzufügen**, um Geräteressourcen als Mitglieder dieser Orchestrierungsgruppe hinzuzufügen. **Suchen** Sie nach den Namen von Geräten, und klicken Sie auf **Hinzufügen**, um die Geräte hinzuzufügen. Sie können Ihre Suche mithilfe von **In dieser Sammlung suchen** auch auf eine einzelne Sammlung filtern.  Klicken Sie auf **OK**, wenn Sie mit dem Hinzufügen von Geräten zur ausgewählten Ressourcenliste fertig sind.
   - Wenn Sie Ressourcen für die Gruppe auswählen, werden nur gültige Clients angezeigt. Es wird überprüft, ob der Standortcode stimmt, der Client installiert ist und keine Ressourcen dupliziert wurden.

1. Wählen Sie auf der Seite **Regelauswahl** eine der folgenden Optionen aus:

   - **Gleichzeitiges Aktualisieren eines Prozentsatzes der Computer zulassen** – geben Sie eine Zahl für diesen Prozentsatz an. Verwenden Sie diese Einstellung, um die Größe der Orchestrierungsgruppe später flexibel anpassen zu können. Beispiel: Ihre Orchestrierungsgruppe umfasst 50 Geräte, und Sie legen diesen Wert auf 10 fest. Während der Bereitstellung eines Softwareupdates lässt Configuration Manager die gleichzeitige Ausführung der Bereitstellung auf fünf Geräten zu. Wenn Sie die Größe der Orchestrierungsgruppe später auf 100 erhöhen, werden 10 Geräte gleichzeitig aktualisiert.

   - **Gleichzeitiges Aktualisieren einer Anzahl von Computern zulassen** – geben Sie eine Zahl an. Verwenden Sie diese Einstellung, um die Ausführung von Updates unabhängig von der Gesamtgröße der Orchestrierungsgruppe immer auf eine bestimmte Anzahl von Geräten zu beschränken.

   - **Geben Sie die Wartungssequenz an**, und sortieren Sie die ausgewählten Ressourcen dann in der gewünschten Reihenfolge. Verwenden Sie diese Einstellung, um die Reihenfolge, in der Geräte die Bereitstellung eines Softwareupdates ausführen, explizit zu definieren.

1. Geben Sie auf der Seite **Skript vor Vorgang** ein PowerShell-Skript ein, das *vor* Ausführung der Bereitstellung auf jedem Gerät ausgeführt werden soll. Das Skript gibt den Wert `0` bei erfolgreicher Ausführung oder `3010` bei erfolgreicher Ausführung mit Neustart zurück.

1. Geben Sie auf der Seite **Skript nach Vorgang** ein PowerShell-Skript ein, das *nach* Ausführung der Bereitstellung auf jedem Gerät ausgeführt werden soll. Das Verhalten dieses Skripts entspricht dem von PreScript.

1. Schließen Sie den Assistenten ab.

> [!WARNING]
> Stellen Sie sicher, dass Skripts, die vor bzw. nach dem Vorgang ausgeführt werden sollen, getestet werden, bevor Sie sie für Orchestrierungsgruppen verwenden. Für Skripts, die vor bzw. nach dem Vorgang ausgeführt werden sollen, tritt kein Timeout auf, und sie werden so lange ausgeführt, bis das Timeout für das Orchestrierungsgruppenmitglied erreicht wurde.

## <a name="view-orchestration-groups-and-members"></a>Anzeigen von Orchestrierungsgruppen und Mitgliedern

Wählen Sie im Arbeitsbereich **Bestand und Konformität** den Knoten **Orchestrierungsgruppe** aus. Um Mitglieder anzuzeigen, wählen Sie eine Orchestrierungsgruppe aus, und klicken Sie im Menüband auf **Mitglieder anzeigen**. Weitere Informationen über die verfügbaren Spalten für die Knoten finden Sie unter [Überwachen von Orchestrierungsgruppen und Mitgliedern](#bkmk_orch_monitor).

## <a name="edit-or-delete-an-orchestration-group"></a>Bearbeiten oder Löschen einer Orchestrierungsgruppe

Klicken Sie auf eine Orchestrierungsgruppe und dann im Menüband oder per Rechtsklick im Menü auf **Löschen**, um sie zu löschen. Klicken Sie auf eine Orchestrierungsgruppe und dann im Menüband oder per Rechtsklick im Menü auf **Eigenschaften**, um sie zu bearbeiten. Ändern Sie die Einstellungen der folgenden Registerkarten:

   - **Allgemein:** 
      - **Name:** Dies ist der Name Ihrer Orchestrierungsgruppe.
      - **Beschreibung:** Dies ist die Beschreibung der Orchestrierungsgruppe (optional).
      - **Zeitlimit für Orchestrierungsgruppe (in Minuten):** Das Zeitlimit, innerhalb dessen alle Gruppenmitglieder die Installation von Updates abschließen müssen.
      - **Zeitlimit für Orchestrierungsgruppenmitglied (in Minuten)** : Das Zeitlimit, innerhalb dessen ein einzelnes Gerät in der Gruppe die Installation von Updates abschließen muss.

  - **Mitgliederauswahl:**
     - **Standortcode:** Dies ist der Standortcode für die Orchestrierungsgruppe.
     - **Mitglieder**: Klicken Sie auf **Hinzufügen**, um zusätzliche Geräte für die Orchestrierungsgruppe auszuwählen. Klicken Sie auf **Entfernen**, um das ausgewählte Gerät zu entfernen.

   - **Regelauswahl:**
      - **Gleichzeitiges Aktualisieren eines Prozentsatzes der Computer zulassen** – geben Sie eine Zahl für diesen Prozentsatz an. Verwenden Sie diese Einstellung, um die Größe der Orchestrierungsgruppe später flexibel anpassen zu können. Beispiel: Ihre Orchestrierungsgruppe umfasst 50 Geräte, und Sie legen diesen Wert auf 10 fest. Während der Bereitstellung eines Softwareupdates lässt Configuration Manager die gleichzeitige Ausführung der Bereitstellung auf fünf Geräten zu. Wenn Sie die Größe der Orchestrierungsgruppe später auf 100 erhöhen, werden 10 Geräte gleichzeitig aktualisiert.
      - **Gleichzeitiges Aktualisieren einer Anzahl von Computern zulassen** – geben Sie eine Zahl an. Verwenden Sie diese Einstellung, um die Ausführung von Updates unabhängig von der Gesamtgröße der Orchestrierungsgruppe immer auf eine bestimmte Anzahl von Geräten zu beschränken.
      - **Geben Sie die Wartungssequenz an:** Sortieren Sie die ausgewählten Ressourcen in der richtigen Reihenfolge. Verwenden Sie diese Einstellung, um die Reihenfolge, in der Geräte die Bereitstellung eines Softwareupdates ausführen, explizit zu definieren.

   - **Skript vor Vorgang:** 
       - Geben Sie ein PowerShell-Skript ein, das *vor* der Ausführung der Bereitstellung auf jedem Gerät ausgeführt wird. Das Skript gibt den Wert `0` bei erfolgreicher Ausführung oder `3010` bei erfolgreicher Ausführung mit Neustart zurück.
       
   - **Skript nach Vorgang:**
      - Geben Sie ein PowerShell-Skript ein, das *nach* der Ausführung der Bereitstellung auf jedem Gerät ausgeführt wird. Das Skript gibt den Wert `0` bei erfolgreicher Ausführung oder `3010` bei erfolgreicher Ausführung mit Neustart zurück.
   > [!WARNING]
   > Stellen Sie sicher, dass Skripts, die vor bzw. nach dem Vorgang ausgeführt werden sollen, getestet werden, bevor Sie sie für Orchestrierungsgruppen verwenden. Für Skripts, die vor bzw. nach dem Vorgang ausgeführt werden sollen, tritt kein Timeout auf, und sie werden so lange ausgeführt, bis das Timeout für das Orchestrierungsgruppenmitglied erreicht wurde.


## <a name="start-orchestration"></a>Starten der Orchestrierung

1. [Stellen Sie Softwareupdates in einer Sammlung bereit](deploy-software-updates.md), die die Mitglieder der Orchestrierungsgruppe enthält.

1. Die Orchestrierung beginnt, wenn ein beliebiger Client in der Gruppe versucht, ein Softwareupdate zu einem bestimmten Termin oder während eines Wartungsfensters zu installieren. Die Orchestrierung beginnt für die gesamte Gruppe und stellt sicher, dass die Geräte gemäß den Regeln der Orchestrierungsgruppe aktualisiert werden.
1. Sie können die Orchestrierung manuell starten, indem Sie sie im Knoten **Orchestrierungsgruppe** auswählen und dann im Menüband oder Kontextmenü auf **Orchestrierung starten** klicken.
1. Führen Sie folgende Schritte aus, wenn eine Orchestrierungsgruppe den Status *Fehlgeschlagen* aufweist:
   1. Bestimmen Sie, warum die Orchestrierung fehlgeschlagen ist, und beheben Sie die Probleme.
   1. [Setzen Sie den Orchestrierungsstatus für Gruppenmitglieder zurück.](#bkmk_reset)
   1. Klicken Sie im Knoten **Orchestrierungsgruppe** auf die Schaltfläche **Orchestrierung starten**, um die Orchestrierung zu starten.
    Setzen Sie diesen Status mithilfe der Schaltfläche **Orchestrierung starten** zurück.  
   [![Starten der Orchestrierung](./media/3098816-start-orchestration.png)](./media/3098816-start-orchestration.png#lightbox)


> [!TIP]
> - Orchestrierungsgruppen gelten nur für Softwareupdatebereitstellungen. Sie gelten nicht für andere Bereitstellungen.
> - Sie können mit der rechten Maustaste auf ein Orchestrierungsgruppenmitglied klicken und **Orchestrierungsgruppenmitglied zurücksetzen** auswählen. Auf diese Weise können Sie die Orchestrierung erneut ausführen.


## <a name="monitor-orchestration-groups"></a><a name="bkmk_orch_monitor"></a> Überwachen von Orchestrierungsgruppen

Wählen Sie im Arbeitsbereich **Bestand und Konformität** den Knoten **Orchestrierungsgruppe** aus. Fügen Sie eine oder mehrere der folgenden Spalten hinzu, um Informationen zu den Gruppen zu erhalten:

- **Orchestrierungsname**: Der Name Ihrer Orchestrierungsgruppe.
- **Standortcode:** Der Standortcode für die Gruppe.
- Der **Orchestrierungstyp** ist einer der folgenden Typen:
   - Zahl
   - Prozentsatz
   - Sequenz

- **Orchestrierungswert**: Anzahl oder Prozentsatz von Mitgliedern, die gleichzeitig gesperrt werden können. Der **Orchestrierungswert** wird nur aufgefüllt, wenn der **Orchestrierungstyp** entweder *Zahl* oder *Prozentsatz* lautet.  
- **Orchestrierungsstatus**: „In Bearbeitung“ während der Orchestrierung. „Leerlauf“, wenn keine Orchestrierung ausgeführt wird.
- **Startzeit der Orchestrierung**: Datum und Uhrzeit des Orchestrierungsbeginns.
- **Aktuelle Sequenznummer**: Gibt an, für welches Mitglied der Gruppe die Orchestrierung aktiv ist. Diese Nummer entspricht der **Sequenznummer** für das Mitglied.  
- **Zeitlimit für Orchestrierung (in Minuten)** : Der Wert von **Zeitlimit für Orchestrierungsgruppe (in Minuten)** , der beim Erstellen der Gruppe auf der Seite **Allgemein** oder beim Bearbeiten der Gruppe auf der Registerkarte **Allgemein** festgelegt wird.
- **Zeitlimit für Orchestrierungsgruppenmitglied (in Minuten)** : Der Wert von **Zeitlimit für Orchestrierungsgruppenmitglied (in Minuten)** , der beim Erstellen der Gruppe auf der Seite **Allgemein** oder beim Bearbeiten der Gruppe auf der Registerkarte **Allgemein** festgelegt wird.
- **Orchestrierungsgruppen-ID**: Die ID der Gruppe. Diese wird in Protokollen und der Datenbank verwendet.
- **Eindeutige ID für Orchestrierungsgruppe**: Die eindeutige ID der Gruppe. Diese wird in Protokollen und der Datenbank verwendet.

## <a name="monitor-orchestration-group-members"></a>Überwachen von Orchestrierungsgruppenmitgliedern

Wählen Sie im Knoten **Orchestrierungsgruppe** eine Orchestrierungsgruppe aus. Wählen Sie im Menüband die Option **Mitglieder anzeigen** aus. Sie können die Mitglieder der Gruppe und ihren Orchestrierungsstatus sehen. Fügen Sie eine oder mehrere der folgenden Spalten hinzu, um Informationen zu den Mitgliedern zu erhalten:

- **Name:** Der Gerätename des Orchestrierungsgruppenmitglieds.
- **Aktueller Status**: Gibt den Status des Mitgliedsgeräts an.
   - **In Bearbeitung** während der Orchestrierung.
   - **Warten:** Gibt an, dass der Client im gesperrten Zustand wartet, bis er für die Installation von Updates an der Reihe ist.
   - **Leerlauf**, wenn die Orchestrierung abgeschlossen ist oder nicht ausgeführt wird.
- **Statuscode**: Sie können mit der rechten Maustaste auf ein Orchestrierungsgruppenmitglied klicken und **Orchestrierungsgruppenmitglied zurücksetzen** auswählen. Durch diese Rücksetzung können Sie die Orchestrierung erneut ausführen. Folgende Status sind möglich: 
   - Leerlauf
   - Wartet – das Gerät wartet, bis es an der Reihe ist
   - In Bearbeitung – ein Update wird installiert
   - Failed
   - Neustart ausstehend
- **Sperre abgerufen um**: Sperren werden vom Client basierend auf der zugehörigen Richtlinie angefordert. Sobald der Client eine Sperre abgerufen hat, wird die Orchestrierung auf diesem Client ausgelöst.  
-**Status zuletzt gemeldet um**: Die Uhrzeit, zu der das Mitglied zum letzten Mal einen Status gemeldet hat.
- **Sequenznummer**: Die Position des Clients in der Warteschlange zum Installieren von Updates.
- **Standortcode:** Der Standortcode für das Mitglied.
- **Clientaktivität**: Gibt ab, ob der Client aktiv oder inaktiv ist.
- **Primäre(r) Benutzer**: Gibt an, welche Benutzer für das Gerät als „primär“ angegeben sind.
- **Clienttyp**: Gibt den Gerätetyp des Clients an.
- **Aktuell angemeldeter Benutzer**: Gibt an, welcher Benutzer derzeit auf dem Gerät angemeldet ist.
- **OG-ID**: Die ID der Orchestrierungsgruppe, zu der das Mitglied gehört.
- **Eindeutige OG-ID**: Die eindeutige ID der Orchestrierungsgruppe, zu der das Mitglied gehört.
- **Ressourcen-ID**: Die Ressourcen-ID des Geräts.

## <a name="reset-the-orchestration-state-for-a-group-member"></a><a name="bkmk_reset"></a> Zurücksetzen des Orchestrierungsstatus für ein Gruppenmitglied

Wenn Sie die Orchestrierung für ein Gruppenmitglied noch mal ausführen möchten, können Sie beispielsweise den Status *Abgeschlossen* oder *Fehlgeschlagen* löschen. Klicken Sie mit der rechten Maustaste zunächst auf ein Orchestrierungsgruppenmitglied und dann auf **Reset Orchestration Group Member** (Orchestrierungsgruppenmitglied zurücksetzen), um den Status zu löschen. Sie können auch im Menüband auf **Reset Orchestration Group Member** (Orchestrierungsgruppenmitglied zurücksetzen) klicken. Bevor Sie den Status zurücksetzen, sollten Sie den Client überprüfen, um festzustellen, warum er fehlgeschlagen ist, und ggf. alle gefundenen Probleme zu beheben.
   [![Orchestrierungsgruppenmitglied zurücksetzen](./media/3098816-reset-group-member.png)](./media/3098816-reset-group-member.png#lightbox)

## <a name="log-files"></a>Protokolldateien

Verwenden Sie die folgenden Protokolldateien auf dem Standortserver zur Überwachung und Problembehandlung:

### <a name="site-server"></a>Standortserver

- **Policypv.log**: Zeigt an, dass der Standort die Orchestrierungsgruppe auf die Clients ausrichtet.
- **SMS_OrchestrationGroup.log**: Zeigt das Verhalten der Orchestrierungsgruppe an.

### <a name="client"></a>Client

- **MaintenanceCoordinator.log**: Hiermit werden Informationen zum Sperrenabruf, der Installation von Updates, den Skripts vor bzw. nach der Ausführung und der Sperrenaufhebung angezeigt.
- **UpdateDeployment.log**: Zeigt den Installationsprozess für Updates an.
- **PolicyAgent.log**: Überprüft, ob sich der Client in einer Orchestrierungsgruppe befindet.

## <a name="next-steps"></a>Nächste Schritte

[Bereitstellen von Softwareupdates](deploy-software-updates.md)