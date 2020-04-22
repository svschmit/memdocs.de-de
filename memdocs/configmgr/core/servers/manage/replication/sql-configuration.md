---
title: SQL-Konfiguration
titleSuffix: Configuration Manager
description: Anhand dieses Diagramms können Sie die Problembehandlung der SQL-Konfiguration für Configuration Manager starten.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 95ab8cbd-0807-4422-823a-f5f9314ba623
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b909d992dc16b6e786c62143347ed420d913dbc5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707618"
---
# <a name="sql-configuration"></a>SQL-Konfiguration

In einer Hierarchie mit mehreren Standorten verwendet Configuration Manager die SQL-Replikation zum Übertragen von Daten zwischen Standorten. Weitere Informationen finden Sie unter [Datenbankreplikation](../../../plan-design/hierarchy/database-replication.md).

Anhand des folgenden Diagramms können Sie die Problembehandlung der SQL-Konfiguration für SQL Service Broker starten:

![Diagramm zur Problembehandlung der SQL-Konfiguration](media/sql-configuration.svg)

## <a name="queries"></a>Abfragen

Dieses Diagramm enthält die folgenden Abfragen und Aktionen:

### <a name="check-if-sql-can-deliver-ssb-messages"></a>Überprüfen, ob SQL SSB-Nachrichten übermitteln kann

```sql
SELECT transmission_status, *
FROM sys.transmission_queue
ORDER BY enqueue_time DESC
```

## <a name="remediation-actions"></a>Wiederherstellungsmaßnahmen

### <a name="remediate-the-issues-reported-from-transmission_status"></a>Beheben der von transmission_status gemeldeten Probleme

Häufige Probleme:

- Firewallkonfiguration
- Netzwerkkonfiguration
- Falsch konfiguriertes SSB-Zertifikat

### <a name="run-sql-profiler-to-trace-ssb-events"></a>Ausführen von SQL Profiler zum Verfolgen von SSB-Ereignissen

Führen Sie SQL Profiler für die Datenbank des CAS- und primären Standorts aus, um Ereignisse im Zusammenhang mit SQL Service Broker zu verfolgen:

- **Audit Broker-Anmeldung**
- **Audit Broker-Konversation**
- Ereignisse in der Kategorie **Broker**
