---
title: Problembehandlung der SQL-Replikation
titleSuffix: Configuration Manager
description: Diese Diagramme bieten eine Übersicht und Hilfe zur Problembehandlung bei der SQL-Replikation zwischen Configuration Manager-Standorten.
ms.date: 02/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 71d7430e-c5aa-485b-8dc0-c80fd8f29f17
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 202a3360b5e04d66ada0d3b47ddd4638c2197167
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703988"
---
# <a name="troubleshoot-sql-replication"></a>Problembehandlung der SQL-Replikation

In einer Hierarchie mit mehreren Standorten verwendet Configuration Manager die SQL-Replikation zum Übertragen von Daten zwischen Standorten. Weitere Informationen finden Sie unter [Datenbankreplikation](../../../plan-design/hierarchy/database-replication.md).

Diese Diagramme bieten eine Übersicht und Hilfe zur Problembehandlung bei der SQL-Replikation.

- [SQL-Replikation](sql-replication.md)
- [SQL-Konfiguration](sql-configuration.md)
- [SQL-Leistung](sql-performance.md)
- [Neuinitialisierung der SQL-Replikation (wiederherstellen)](sql-replication-reinit.md)
- [Globale Datenwiederherstellung](global-data-reinit.md)
- [Wiederherstellung von Standortdaten](site-data-reinit.md)
- [Wiederherstellung der fehlenden Meldung](reinit-missing-message.md)

Diese Diagramme zur Problembehandlung sind miteinander verbunden. Verwenden Sie das folgende Diagramm, um die Beziehungen nachzuvollziehen:

![Übersichtsdiagramm für die Problembehandlung bei der SQL-Replikation](media/overview.png)

<!-- PNG used instead of SVG because of weird blankspace in the SVG. The SVG file exists in the same location. -->

Weitere Informationen finden Sie in der folgenden Reihe von Microsoft-Support-Blogs:

- [ConfigMgr DRS Synchronization Internals (Informationen zur Synchronisierung mit ConfigMgr DRS)](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-drs-synchronization-internals/ba-p/1154317)
- [ConfigMgr 2012 Data Replication Service (DRS) Unleashed (Einführung in den Datenreplikationsdienst (DRS) in ConfigMgr 2012)](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-data-replication-service-drs-unleashed/ba-p/339916)
- [ConfigMgr 2012 DRS – Troubleshooting FAQs (ConfigMgr 2012 DRS – FAQs zur Problembehandlung)](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-troubleshooting-faqs/ba-p/339934)
- [ConfigMgr 2012 DRS Initialization Internals (Informationen zur Initialisierung mit ConfigMgr 2012 DRS)](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-initialization-internals/ba-p/339948)
- [ConfigMgr 2012: DRS and SQL service broker certificate issues (ConfigMgr 2012: Probleme mit DRS und SQL Service Broker-Zertifikaten)](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-and-sql-service-broker-certificate-issues/ba-p/339910)
