---
title: Voraussetzungen für die Berichterstattung
titleSuffix: Configuration Manager
description: Hier finden Sie Informationen zu verschiedenen Abhängigkeiten, die sich auf die Nutzung der Berichterstellung in Configuration Manager auswirken.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9cc508a5-5023-4833-b776-ae9a6971138f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e08833a5ef560a0f958fe68b4ade0d4717dffc73
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703518"
---
# <a name="prerequisites-for-reporting-in-configuration-manager"></a>Voraussetzungen für die Berichterstattung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Für die Berichterstattung in Configuration Manager Reporting gelten die folgenden Abhängigkeiten:

- SQL Server Reporting Services
- Reporting Services-Punkt
- Power BI-Berichtsserver (optional, ab Version 2002)

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

Installieren und konfigurieren Sie zuerst SQL Server Reporting Services, damit die Berichterstellung in Configuration Manager verwendet werden kann.

Weitere Informationen zum Planen und Bereitstellen von Reporting Services finden Sie unter [SQL Server Reporting Services installieren](https://docs.microsoft.com/sql/reporting-services/install-windows/install-reporting-services).

Installieren Sie die Reporting Services-Datenbank entweder auf der Standardinstanz oder auf einer benannten Instanz einer 64-Bit-SQL Server-Installation. Installieren Sie die SQL Server-Instanz auf dem gleichen Computer wie der Standortsystemserver, oder konfigurieren Sie sie auf einem Remotecomputer.

Configuration Manager unterstützt die gleichen Versionen von SQL Server für die Berichterstattung wie für die Standortdatenbank. Weitere Informationen finden Sie unter [Unterstützte SQL Server-Versionen](../../plan-design/configs/support-for-sql-server-versions.md#bkmk_SQLVersions).

## <a name="reporting-services-point"></a>Reporting Services-Punkt

Konfigurieren Sie die Standortsystemrolle des Reporting Services-Punkts, um die Berichterstellung in Configuration Manager zu verwenden.

Weitere Informationen finden Sie unter [Site and site system prerequisites for System Center Configuration Manager](../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012RSpoint) (Standort- und Standortsystemanforderungen für System Center Configuration Manager).

## <a name="power-bi-report-server"></a>Power BI-Berichtsserver

Ab Version 2002 können Sie die Berichterstellung mit dem Power BI-Berichtsserver integrieren. Weitere Informationen hierzu (einschließlich der Voraussetzungen) finden Sie unter [Integration mit dem Power BI-Berichtsserver](powerbi-report-server.md).

## <a name="next-steps"></a>Nächste Schritte

[Configure reporting (Konfigurieren der Berichterstellung)](configuring-reporting.md)
