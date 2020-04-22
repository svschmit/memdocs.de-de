---
title: Voraussetzungen für die Energieverwaltung
titleSuffix: Configuration Manager
description: Hier erhalten Sie Informationen über die Voraussetzungen für die Energieverwaltung in Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9c062f13-3c1f-4621-9cae-de0e322aa03f
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: a816d333d96dba6cb1c38f6499ccac78e2db8a3c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696518"
---
# <a name="prerequisites-for-power-management-in-configuration-manager"></a>Voraussetzungen für die Energieverwaltung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Die Energieverwaltung in Configuration Manager weist externe Abhängigkeiten sowie Abhängigkeiten innerhalb des Produkts auf.  

## <a name="dependencies-external-to-configuration-manager"></a>Externe Abhängigkeiten von Configuration Manager  
 In der folgenden Tabelle sind die Abhängigkeiten aufgelistet, die außerhalb von Configuration Manager für die Energieverwaltung bestehen.  

|Abhängigkeit|Weitere Informationen|  
|----------------|----------------------|  
|Clientcomputer müssen die erforderlichen Energiezustände unterstützen.|Um alle Funktionen der Energieverwaltung nutzen zu können, müssen Clientcomputer die Zustände "Standbymodus" und "Ruhezustand" sowie die Aktionen "Aktivierung nach Standbymodus" und "Aktivierung nach Ruhezustand" unterstützen. Klären Sie anhand des Berichts **Energiefunktionen** , ob die Computer diese Modi und Aktionen unterstützen. Weitere Informationen finden Sie unter [Bericht „Energiefunktionen“](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Capabilites) im Thema [Überwachen und Planen der Energieverwaltung](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).|  

## <a name="configuration-manager-dependencies"></a>Abhängigkeiten in Configuration Manager  
 In der folgenden Tabelle sind die Abhängigkeiten aufgelistet, die innerhalb von Configuration Manager für die Energieverwaltung bestehen.  

|Abhängigkeit|Weitere Informationen|  
|----------------|----------------------|  
|Die Energieverwaltung muss aktiviert sein, damit Energiesparpläne erstellt und überwacht werden können.|Informationen zum Aktivieren und Konfigurieren der Energieverwaltung finden Sie unter [Konfigurieren der Energieverwaltung](../../../../core/clients/manage/power/configuring-power-management.md).|  
|Reporting Services-Punkt|Es muss ein Reporting Services-Punkt erstellt werden, bevor Energieverwaltungsberichte angezeigt werden können. Weitere Informationen finden Sie unter [Einführung in die Berichterstellung](../../../servers/manage/introduction-to-reporting.md).|  
