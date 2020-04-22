---
title: Voraussetzungen für die Remotesteuerung
titleSuffix: Configuration Manager
description: Hier finden Sie Informationen zu den Voraussetzungen für die Remotesteuerung in Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c1b2057e-b74f-43fa-a293-763a8f866d3d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f19f8799dd90fc61c0bfeeee1dc60125ba491fef
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696418"
---
# <a name="prerequisites-for-remote-control-in-configuration-manager"></a>Voraussetzungen für die Remotesteuerung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Die Remotesteuerung in Configuration Manager hat externe Abhängigkeiten sowie Abhängigkeiten innerhalb des Produkts.  

## <a name="dependencies-external-to-configuration-manager"></a>Externe Abhängigkeiten von Configuration Manager  

|Abhängigkeit|Weitere Informationen|  
|----------------|----------------------|  
|Computer-Grafikkartentreiber|Vergewissern Sie sich, dass auf den Clientcomputern der aktuelle Grafikkartentreiber installiert ist, um bei der Remotesteuerung optimale Ergebnisse zu erzielen.|  

 Computer, auf denen Windows Embedded, Windows Embedded for Point of Service (POS) oder Windows Fundamentals for Legacy PCs ausgeführt wird, unterstützen den Remotesteuerungsviewer nicht, doch sie unterstützen den Remotesteuerungsclient.  

 Die Configuration Manager-Remotesteuerung kann nicht zur Remotesteuerung von Clientcomputern verwendet werden, auf denen Systems Management Server 2003 oder Configuration Manager 2007 ausgeführt wird.  

> [!NOTE]  
>  Keine Windows-Dienste sind als externe Abhängigkeit für die Remotesteuerung erforderlich.  

### <a name="supported-operating-systems-for-the-remote-control-viewer"></a>Unterstützte Betriebssysteme für den Remotesteuerungsviewer  
Der Remotesteuerungsviewer wird auf allen Betriebssystemen unterstützt, die für die Configuration Manager-Konsole unterstützt werden. Weitere Informationen finden Sie unter [Unterstützte Betriebssystemversionen für Configuration Manager-Konsolen](../../../../core/plan-design/configs/supported-operating-systems-consoles.md).   

## <a name="configuration-manager-dependencies"></a>Abhängigkeiten in Configuration Manager  

|Abhängigkeit|Weitere Informationen|  
|----------------|----------------------|  
|Remotesteuerung muss für Clients aktiviert werden|Die Remotesteuerung ist in der Standardeinstellung nicht aktiviert, wenn Configuration Manager installiert wird. Informationen zum Aktivieren und Konfigurieren der Remotesteuerung finden Sie unter [Konfigurieren der Remotesteuerung](../../../../core/clients/manage/remote-control/configuring-remote-control.md).|  
|Reporting Services-Punkt|Die Standortsystemrolle des Reporting Services-Punkts muss installiert werden, bevor Berichte für die Remotesteuerung ausgeführt werden können. Weitere Informationen finden Sie unter [Einführung in die Berichterstellung](../../../servers/manage/introduction-to-reporting.md).|  
|Sicherheitsberechtigungen zum Verwalten der Remotesteuerung|Sie benötigen die folgenden Berechtigungen, um auf Sammlungsressourcen zugreifen und eine Remotesteuerungssitzung über die Configuration Manager-Konsole starten zu können: **Lesen**, **Ressource lesen** und **Remotesteuerung** für das Objekt **Sammlung**.<br /><br /> Die Sicherheitsrolle **Remotetoolsverantwortlicher** umfasst diese Berechtigungen, die zum Verwalten der Remotesteuerung in Configuration Manager erforderlich sind.<br /><br /> Weitere Informationen finden Sie unter [Konfigurieren der rollenbasierten Verwaltung für Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md).<br /><br /> Darüber hinaus müssen zugelassene Viewer die Berechtigung erhalten, die Remotesteuerung einzusetzen, indem Sie diese Benutzer der Liste **Zugelassene Viewer für Remotesteuerung und Remoteunterstützung** der **Remotetools**-Clienteinstellungen hinzufügen.
