---
title: Einführung in Sammlungen
titleSuffix: Configuration Manager
description: Hier erhalten Sie eine Einführung in die Verwendung von Sammlungen in Configuration Manager.
ms.date: 05/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d17e1188-d277-438f-9236-db9cd213b421
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0665c6378ac81d6f6f254501760647048ce66b0b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695328"
---
# <a name="introduction-to-collections-in-configuration-manager"></a>Einführung in Sammlungen in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Mithilfe von Sammlungen können Sie Ressourcen in verwaltbaren Einheiten organisieren. Sie können Sammlungen erstellen, die mit Ihren Anforderungen zur Clientverwaltung übereinstimmen und um Vorgänge für mehrere Ressourcen gleichzeitig auszuführen. 

Die meisten Verwaltungsaufgaben basieren auf der Verwendung einer oder mehrerer Sammlungen oder erfordern diese. Obwohl Sie die integrierte Sammlung aller Systeme verwenden können, stellt die Verwendung dieser Sammlung für Verwaltungsaufgaben keine Best Practice dar. Erstellen Sie benutzerdefinierte Sammlungen, um die Geräte oder Benutzer für eine Aufgabe genauer anzugeben.  

 Integrierte und benutzerdefinierte Sammlungen werden in den Knoten **Benutzersammlungen** und **Gerätesammlungen** im Arbeitsbereich **Bestände und Kompatibilität** in der Configuration Manager-Konsole angezeigt.  

 Die zuletzt verwendeten Sammlungen werden im Knoten **Benutzer** sowie im Knoten **Geräte** des Arbeitsbereichs **Bestand und Kompatibilität** angezeigt.  

Hier einige Beispiele für die Verwendung von Sammlungen:  

|Vorgang|Beispiel|  
|---------|-------|  
|Gruppieren von Ressourcen|Sie können Sammlungen erstellen, die die auf der Hierarchie Ihrer Organisation basierenden Ressourcen gruppieren.<br /><br /> Sie können z.B. eine Sammlung aller Computer in der Active Directory-Organisationseinheit (OE) „Hauptsitz in London“ erstellen. Weitere Informationen zum Erstellen dieser Art von Sammlung finden Sie unter [Erstellen von Sammlungen](../../../../core/clients/manage/collections/create-collections.md).<br /><br /> Sie können diese Sammlung für bestimmte Vorgänge verwenden, z.B. zum Konfigurieren von Endpoint Protection-Einstellungen oder Geräteeinstellungen für die Energieverwaltung sowie zum Installieren des Configuration Manager-Clients.|  
|Anwendungsbereitstellung|Sie können eine Sammlung aller Computer erstellen, auf denen Microsoft Office 2013 nicht installiert ist, und dann die Software auf allen Computern in der Sammlung bereitstellen.<br /><br /> Sie können auch Anwendungsanforderungen verwenden, um diese Aufgabe durchzuführen. Weitere Informationen finden Sie unter [Erstellen von Anwendungen mit Configuration Manager](../../../../apps/deploy-use/create-applications.md).|  
|[Verwalten von Clienteinstellungen](../../../../core/clients/deploy/about-client-settings.md)|Obwohl die Standardclienteinstellungen in Configuration Manager für alle Geräte und alle Benutzer gelten, können Sie benutzerdefinierte Clienteinstellungen erstellen, die für eine Sammlung von Geräten oder eine Sammlung von Benutzern gelten.<br /><br /> Wenn z.B. die Remotesteuerung mit wenigen Ausnahmen auf allen Geräten zur Verfügung stehen soll, konfigurieren Sie die Standardclienteinstellungen so, dass die Remotesteuerung zulässig ist. Anschließend konfigurieren Sie benutzerdefinierte Clienteinstellungen, die die Remotesteuerung nicht zulassen, und stellen sie für die Sammlung der ausgenommenen Clients bereit. |  
|[Energieverwaltung](../power/introduction-to-power-management.md)|Für jede Sammlung können Sie bestimmte Energieeinstellungen konfigurieren.|  
|[Rollenbasierte Verwaltung](../../../../core/servers/deploy/configure/configure-role-based-administration.md)|Verwenden Sie Sammlungen, um zu steuern, welche Benutzergruppen Zugriff auf verschiedene Funktionen in der Configuration Manager-Konsole haben.|  
|[Wartungsfenster](../../../../core/clients/manage/collections/use-maintenance-windows.md)|Mithilfe von Wartungsfenstern können Sie einen Zeitraum definieren, innerhalb dessen verschiedene Configuration Manager-Vorgänge bei Mitgliedern von Gerätesammlungen durchgeführt werden können. |  


## <a name="collection-types-in-configuration-manager"></a>Sammlungstypen in Configuration Manager  
 Configuration Manager verfügt über integrierte Sammlungen für allgemeine Vorgänge. Darüber hinaus können Sie benutzerdefinierte Sammlungen erstellen.   

### <a name="built-in-collections"></a>Integrierte Sammlungen  
 In der Standardeinstellung sind in Configuration Manager die folgenden Sammlungen enthalten, die nicht geändert werden können.  

|**Sammlungsnamen**|Beschreibung|  
|-------------------------|-----------------|  
|**Alle Benutzergruppen**|Benutzergruppen sind enthalten, die mithilfe der Active Directory-Sicherheitsgruppenermittlung ermittelt wurden.|  
|**Allen Benutzern**|Benutzer sind enthalten, die mithilfe der Active Directory-Benutzerermittlung ermittelt wurden.|  
|**Alle Benutzer und Benutzergruppen**|Die Sammlungen "Alle Benutzer" und "Alle Benutzergruppen" sind enthalten. Diese Sammlung enthält den größten Bereich von Benutzer- und Benutzergruppenressourcen.|  
|**Alle Desktop- und Serverclients**|Enthält die Server- und Desktopgeräte, auf denen der Configuration Manager-Client installiert ist. Die Mitgliedschaft wird per Frequenzermittlung gepflegt.|  
|**Alle mobilen Geräte**|Enthält die mobilen Geräte, die von Configuration Manager verwaltet werden Die Mitgliedschaft ist auf mobile Geräte beschränkt, die erfolgreich einem Standort zugewiesen oder vom Exchange Server-Connector ermittelt wurden.|  
|**Alle Systeme**|Enthält die Sammlungen „Alle Desktop- und Serverclients“, „Alle mobilen Geräte“ und „Alle unbekannten Computer“ sowie alle von Microsoft Intune registrierten mobilen Geräte. Diese Sammlung enthält den größten Bereich von Geräteressourcen.|  
|**Alle unbekannten Computer**|Generische Computerdatensätze für verschiedene Computerplattformen sind enthalten. Sie können diese Sammlung verwenden, um ein Betriebssystem bereitzustellen, indem Sie eine Tasksequenz mit PXE-Start, startbare oder vorab bereitgestellte Medien einsetzen.|  

### <a name="custom-collections"></a>Benutzerdefinierte Sammlungen  
 Beim Erstellen einer benutzerdefinierten Sammlung in Configuration Manager wird die Mitgliedschaft dieser Sammlung durch mindestens eine Sammlungsregel bestimmt. Siehe dazu die Beschreibung unter [Erstellen von Sammlungen](../../../../core/clients/manage/collections/create-collections.md). 

