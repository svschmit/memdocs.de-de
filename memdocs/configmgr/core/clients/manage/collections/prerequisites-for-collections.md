---
title: Voraussetzungen für Sammlungen
titleSuffix: Configuration Manager
description: Hier erhalten Sie Informationen zur Verwendung von Sammlungen in Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a53e4cf1-518a-4210-9c16-022c4261d2fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 313c3183cd6401390d743575ba513026a3e3f607
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695538"
---
# <a name="prerequisites-for-collections-in-configuration-manager"></a>Voraussetzungen für Sammlungen in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Sammlungen in Configuration Manager weisen nur Abhängigkeiten innerhalb des Produkts auf.  

## <a name="configuration-manager-dependencies"></a>Abhängigkeiten in Configuration Manager  

|Abhängigkeit|Weitere Informationen|  
|----------------|----------------------|  
|Reporting Services-Punkt|Die Standortsystemrolle des Reporting Services-Punkts muss installiert werden, bevor Berichte für Sammlungen ausgeführt werden können. Weitere Informationen finden Sie unter [Einführung in die Berichterstellung](../../../servers/manage/introduction-to-reporting.md).|  
|Für die Verwaltung von Sammlungen sind spezielle Sicherheitsberechtigungen erforderlich.|Zum Verwalten der Konformitätseinstellungen müssen Sie über folgende Sicherheitsberechtigungen verfügen:<br /><br /> – Berechtigungen für das Erstellen und Verwalten von Sammlungen: **Erstellen**, **Löschen**, **Ändern**, **Ordner ändern**, **Objekt verschieben**, **Lesen** und **Ressource lesen** für das Objekt **Sammlung**.<br /><br /> – Berechtigungen für das Verwalten von Sammlungseinstellungen: **Sammlungseinstellungen ändern** für das Objekt **Sammlung**.<br /><br /> Die Berechtigung **Ordner ändern** ist für alle Sammlungsordner, einschließlich der Stammordners, erforderlich.|  
