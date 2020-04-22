---
title: Sicherheit und Datenschutz bei Konformitätseinstellungen
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über bewährte Sicherheitsmethoden für Kompatibilitätseinstellungen in Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 1c409244-6778-4970-a99c-d2508c9cf62b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: eae705b97add7515403549eb668e68f1489d6756
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692178"
---
# <a name="security-and-privacy-for-compliance-settings-in-configuration-manager"></a>Sicherheit und Datenschutz bei Konformitätseinstellungen in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*


## <a name="security-best-practices-for-compliance-settings"></a>Bewährte Sicherheitsmethoden für Kompatibilitätseinstellungen  

|Bewährte Sicherheitsmethode|Weitere Informationen|  
|----------------------------|----------------------|  
|Überwachen Sie keine vertraulichen Daten.|Vermeiden Sie Offenlegungen von Daten, indem Sie keine Konfigurationselemente zum Überwachen von möglicherweise sensiblen Informationen konfigurieren.|  
|Konfigurieren Sie keine Kompatibilitätsregeln, von denen Daten verwendet werden, die von Endbenutzern geändert werden können.|Wenn Sie eine Kompatibilitätsregel auf Grundlage von Daten erstellen, die Benutzer ändern können, z. B. Registrierungseinstellungen für Konfigurationsoptionen, sind die Ergebnisse der Kompatibilitätsüberprüfung nicht zuverlässig.|  
|Sie sollten Microsoft System Center-Konfigurationspakete und andere Konfigurationsdaten aus externen Quellen nur dann importieren, wenn sie über eine gültige digitale Signatur von einem vertrauenswürdigen Herausgeber verfügen.|Veröffentlichte Konfigurationsdaten können digital signiert werden, sodass Sie die Veröffentlichungsquelle überprüfen und sicherstellen können, dass die Daten nicht manipuliert wurden. Wenn bei der Überprüfung der digitalen Signatur ein Fehler auftritt, erhalten Sie eine Warnung und werden aufgefordert, mit dem Import fortzufahren. Importieren Sie keine Daten, die nicht signiert sind und deren Quelle bzw. Integrität Sie nicht überprüfen können.|  
|Implementieren Sie Zugriffssteuerungen zum Schutz von Referenzcomputern.|Wenn ein Administrator eine Registrierungs- oder Dateisystemeinstellung konfiguriert, indem er zu einem Referenzcomputer navigiert, müssen Sie sicherstellen, dass der Referenzcomputer nicht gefährdet ist.|  
|Sichern Sie den Kommunikationskanal, wenn Sie einen Referenzcomputer durchsuchen.|Vermeiden Sie die Manipulation von Daten bei der Übertragung im Netzwerk, indem Sie zwischen dem Computer, auf dem die Configuration Manager-Konsole ausgeführt wird, und dem Referenzcomputer das IPsec- (Internetprotokollsicherheit) oder das SMB-Protokoll (Server Message Block) verwenden.|  
|Überwachen Sie die Administratoren, denen die Sicherheitsrolle im Kompatibilitätseinstellungs-Manager zugewiesen wurde, und beschränken Sie ihre Anzahl.|Administratoren mit der Rolle **Kompatibilitätseinstellungs-Manager** können Konfigurationselemente für alle Geräte und Benutzer in der Hierarchie bereitstellen. Mit Konfigurationselementen kann viel bewirkt werden, und sie können beispielsweise Skripts und Neukonfigurationen der Registrierung beinhalten.|  

## <a name="privacy-information-for-compliance-settings"></a>Datenschutzinformationen zu Kompatibilitätseinstellungen  
 Sie können Konformitätseinstellungen verwenden, um herauszufinden, ob Ihre Clientcomputer konform mit Konfigurationselementen sind, die Sie in Konfigurationsbasislinien bereitstellen. Einige Einstellungen können automatisch korrigiert werden, wenn sie nicht kompatibel sind. Die Kompatibilitätsinformationen werden vom Verwaltungspunkt an den Standortserver gesendet und in der Standortdatenbank gespeichert. Die Informationen werden verschlüsselt, wenn sie von Geräten an den Verwaltungspunkt gesendet werden, sie werden aber nicht in einem verschlüsselten Format in der Standortdatenbank gespeichert. Die Informationen verbleiben in der Datenbank, bis sie mit dem Standortwartungstask **Veraltete Konfigurationsverwaltungsdaten löschen** jeweils nach 90 Tagen gelöscht werden. Sie können das Löschintervall konfigurieren. Die Kompatibilitätsinformationen werden nicht an Microsoft gesendet.  

 Von Geräten werden standardmäßig keine Kompatibilitätseinstellungen ausgewertet. Außerdem müssen die Konfigurationselemente und Konfigurationsbasislinien konfiguriert und dann auf Geräten bereitgestellt werden.  
