---
title: Überwachungsänderungen und -ereignisse in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie Überwachungsprotokolle, die Microsoft Intune-Aktivitäten erfassen, überprüfen können.
keywords: ''
ms.author: dougeby
author: dougeby
manager: dougeby
ms.date: 03/18/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 6ee841cc-5694-4ba1-8f66-1d58edec30a4
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 923a7c192121530d84ca2034b2ca8a4be3cc32d6
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990758"
---
# <a name="use-audit-logs-to-track-and-monitor-events-in-microsoft-intune"></a>Verwenden von Überwachungsprotokollen, um Ereignisse in Microsoft Intune zu verfolgen und zu überwachen

Überwachungsprotokolle umfassen einen Datensatz von Aktivitäten, die eine Änderung in Microsoft Intune bewirken. Durch Vorgänge zum Erstellen, Aktualisieren (Bearbeiten), Löschen, Zuweisen sowie Remoteaktionen werden alle Überwachungsereignisse erstellt, die Administratoren für die meisten Intune-Workloads überprüfen können. Die Überwachung ist standardmäßig für alle Kunden aktiviert. Sie kann nicht deaktiviert werden.

> [!NOTE]
> Die Aufzeichnung der Überwachungsereignisse wurde im Rahmen des Featurerelease im Dezember 2017 eingeführt und ab da begonnen. Frühere Ereignisse sind nicht verfügbar.

## <a name="who-can-access-the-data"></a>Wer kann auf die Daten zugreifen?

Benutzer mit den folgenden Berechtigungen können Überwachungsprotokolle überprüfen:

- Globaler Administrator
- Intune-Dienstadministrator
- Administratoren, denen eine Intune-Rolle mit den Berechtigungen **Überwachungsdaten** - **Lesen** zugewiesen wurde

## <a name="audit-logs-for-intune-workloads"></a>Überwachungsprotokolle für Intune-Workloads

Sie können für jede Intune-Workload Überwachungsprotokolle in der Überwachungsgruppe einsehen.

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Klicken Sie auf **Mandantenverwaltung** > **Überwachungsprotokolle**.
3. Wählen Sie **Filter** aus, und grenzen Sie die Ergebnisse mithilfe der folgenden Optionen ein, um die Ergebnisse zu filtern.
    - **Kategorie:** z. B. **Konformität**, **Gerät** und **Rolle**.
    - **Aktivität:** Die hier aufgeführten Optionen werden durch die Option eingeschränkt, die unter **Kategorie** ausgewählt ist.
    - **Datumsbereich:** Sie können Protokolle des vorherigen Monats, der vorherigen Woche oder des vorherigen Tags auswählen.
4. Wählen Sie **Anwenden** aus.
4. Klicken Sie auf ein Element in der Liste, um sich die Aktivitätsdetails anzeigen zu lassen.

## <a name="route-logs-to-azure-monitor"></a>Routen von Protokollen an Azure Monitor

Überwachungsprotokolle und Betriebsprotokolle können auch zu Azure Monitor weitergeleitet werden. Wählen Sie im Bereich **Überwachungsprotokolle** die **Einstellungen für das Exportieren von Daten** aus:

![Exportieren von Protokolldaten in Azure Monitor, indem die Einstellungen für das Exportieren von Daten in Intune ausgewählt werden](./media/monitor-audit-logs/audit-logs-export-data-settings.png)

> [!NOTE]
> Weitere Informationen zu diesem Feature und den Voraussetzungen für dessen Verwendung finden Sie unter [Senden von Protokolldaten an Azure Storage, Azure Event Hub oder Azure Log Analytics in Intune (Vorschau)](review-logs-using-azure-monitor.md).

> [!NOTE]
> **Initiiert von (Akteur)** enthält Informationen dazu, wer die Aufgabe ausgeführt hat, und wo sie ausgeführt wurde. Wenn Sie beispielsweise im Azure-Portal in Intune die Aktivität ausführen, wird unter **Anwendung** immer **Microsoft Intune-Portalerweiterung** und unter **Anwendungs-ID** immer dieselbe GUID aufgeführt.
>
> Im Abschnitt **Ziel(e)** werden mehrere Ziele und die geänderten Eigenschaften aufgeführt.  

## <a name="use-graph-api-to-retrieve-audit-events"></a>Abrufen von Überwachungsereignissen mithilfe der Graph-API

Details zur Verwendung der Graph-API, um bis zu einem Jahr an Überwachungsereignissen zu erhalten, finden Sie unter [List auditEvents (Auflisten von Überwachungsereignissen)](https://docs.microsoft.com/graph/api/intune-auditing-auditevent-list?view=graph-rest-1.0).

## <a name="next-steps"></a>Nächste Schritte

[Senden von Daten an den Speicher, an Event Hubs oder Azure Monitor-Protokolle in Intune (Vorschauversion)](review-logs-using-azure-monitor.md)

[Überprüfen der Schutzprotokolle für Client-Apps](../apps/app-protection-policy-settings-log.md).
