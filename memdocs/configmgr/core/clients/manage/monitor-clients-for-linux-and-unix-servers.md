---
title: Überwachen von Linux/UNIX-Clients
titleSuffix: Configuration Manager
description: Clients auf Linux- und UNIX-Servern können in Configuration Manager überwacht werden.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d827cf91-b18f-4ee7-b538-24ba6f003ab9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d2ea3a0b630e1710aeaf74a4349f202806d45039
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696768"
---
# <a name="how-to-monitor-clients-for-linux-and-unix-servers-in-configuration-manager"></a>Überwachen von Clients für Linux- und UNIX-Server in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

> [!Important]  
> Ab Version 1902 unterstützt Configuration Manager keine Linux- oder UNIX-Clients mehr. 
> 
> Ziehen Sie deshalb Microsoft Azure Management zum Verwalten von Linux-Servern in Betracht. Azure-Lösungen verfügen über umfangreiche Linux-Unterstützung, die i.d.R. über die Funktionen von Configuration Manager hinausgeht (einschließlich der End-to-End-Patchverwaltung für Linux).

Sie können in der Configuration Manager-Konsole Informationen von Linux- und UNIX-Servern mithilfe derselben Methoden anzeigen, die Sie auch zum Anzeigen von Informationen von Windows-basierten Clients verwenden.  

 Die Informationen, die Sie anzeigen können, umfassen Folgendes:  

- Statusdetails von Clients in den Dashboards der Configuration Manager-Konsole  

- Details zu Clients in den Configuration Manager-Standardberichten  

- Inventurdetails im Ressourcen-Explorer  

  In den folgenden Abschnitten wird beschrieben, wie Sie diese Details aus dem Ressourcen-Explorer und den Berichten erhalten.  

##  <a name="use-resource-explorer-to-view-inventory-for-linux-and-unix-servers"></a><a name="BKMK_UseResourceExpforLnU"></a> Verwenden des Ressourcen-Explorers zur Anzeige von Inventuren für Linux- und UNIX-Server  

 Nachdem ein Configuration Manager-Client die Hardwareinventur an den Configuration Manager-Standort gesendet hat, können Sie Ressourcen-Explorer zum Anzeigen dieser Informationen verwenden. Der Configuration Manager-Client für Linux und UNIX fügt keine neuen Klassen oder Ansichten für die Inventur zu Ressourcen-Explorer hinzu. Die Linux- und UNIX-Inventurdaten werden vorhandenen WMI-Klassen zugeordnet. Mit dem Ressourcen-Explorer können Sie die Inventurdetails für Ihre Linux- und UNIX-Server in den Windows-basierten Klassifikationen anzeigen.  

 Beispielsweise können Sie die Liste aller systemeigen installierten Programme zusammenstellen, die auf den Linux- und UNIX-Servern gefunden werden. Beispiele für systemeigen installierte Programme umfassen **RPMS** in Linux oder **PKGS** in Solaris. Nachdem die Inventur von einem Linux- oder UNIX-Client gesendet wurde, können Sie die Liste aller nativ installierten Linux- oder UNIX-Programme im Ressourcen-Explorer in der Configuration Manager-Konsole anzeigen.  

 Informationen zur Verwendung des Ressourcen-Explorers finden Sie unter [Verwenden des Ressourcen-Explorers zum Anzeigen der Hardwareinventur](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

##  <a name="how-to-use-reports-to-view-information-for-linux-and-unix-servers"></a><a name="BKMK_UseReportsforLnU"></a> Verwenden von Berichten zur Anzeige von Informationen für Linux- und UNIX-Server  
 Berichte für Configuration Manager enthalten Informationen von Linux- und UNIX-Servern zusammen mit Informationen von Windows-basierten Computern. Es sind keine zusätzlichen Konfigurationen erforderlich, um die Linux- und UNIX-Daten in die Berichte zu integrieren.  

 Wenn Sie beispielsweise den Bericht zur Anzahl der Betriebssystemversionen ausführen, wird die Liste der verschiedenen Betriebssysteme und die Anzahl der Clients, auf denen das jeweilige Betriebssystem ausgeführt wird, angezeigt. Der Bericht basiert auf den Hardwareinventurinformationen, die von den verschiedenen Configuration Manager-Clients, auf denen die unterschiedlichen Betriebssysteme ausgeführt werden, gesendet wurden.  

 Es können auch benutzerdefinierte Berichte erstellt werden, die für Linux- und UNIX-Serverdaten spezifisch sind. Die Eigenschaft **Caption** der Hardwareinventurklasse **Operating System** ist ein nützliches Attribut, mit dem Sie bestimmte Betriebssysteme in der Berichtsabfrage ermitteln können.  

 Informationen zu Berichten in Configuration Manager finden Sie unter [Einführung in die Berichterstellung](../../servers/manage/introduction-to-reporting.md).  
