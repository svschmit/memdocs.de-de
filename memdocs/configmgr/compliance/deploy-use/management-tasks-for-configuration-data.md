---
title: Verwalten von Konfigurationsdaten
titleSuffix: Configuration Manager
description: Nachdem Sie Konfigurationselemente und Baselines in Configuration Manager erstellt haben, können Sie andere Befehle verwenden, um verschiedene Aktionen ausführen.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: b48c693c-d2b0-4707-a5dd-fe92172c49fe
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: de8168d7d699998117eff8821929c654815f1a49
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692398"
---
# <a name="manage-configuration-data-in-configuration-manager"></a>Verwalten von Konfigurationsdaten in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Nachdem Sie Konfigurationselemente und Konfigurationsbaselines in Configuration Manager erstellt haben, sind weitere Befehle zur Ausführung verschiedener Aktionen verfügbar.  

## <a name="manage-configuration-items"></a>Verwalten von Konfigurationselementen  

-   Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** die Option **Kompatibilitätseinstellungen** > **Konfigurationselemente**, und wählen Sie das zu verwaltende Konfigurationselement und dann einen Verwaltungstask aus.  

|Verwaltungstask|Details|  
|---------------------|-------------|  
|**Untergeordnetes Konfigurationselement erstellen**|Öffnet den **Assistenten zum Erstellen untergeordneter Konfigurationselemente** , mit dem Sie aus einem ausgewählten Konfigurationselement ein untergeordnetes Konfigurationselement erstellen können.<br /><br /> Von einem Mobilgerät-Konfigurationselement können Sie kein untergeordnetes Konfigurationselement erstellen.<br /><br /> Details finden Sie unter [Erstellen untergeordneter Konfigurationselemente](../../compliance/deploy-use/create-child-configuration-items.md).|  
|**Revisionsverlauf**|Öffnet das Dialogfeld **Konfigurationselement-Revisionsverlauf** , in dem Sie vorherige Revisionen des ausgewählten Konfigurationselements anzeigen und verwalten können.|  
|**XML-Definition anzeigen**|Zeigt die XML-Definitionsdatei des ausgewählten Konfigurationselements in einem neuen Fenster an. Diese Informationen können hilfreich sein, wenn Sie Konfigurationsdaten manuell erstellen möchten.|  
|**Exportierenieren**|Exportiert ein Konfigurationselement in eine CAB-Datei, unter der Voraussetzung, dass sie an diesem Standort erstellt wurde. Anschließend können Sie das Element in denselben oder einen anderen Configuration Manager-Standort importieren. Konfigurationsdaten werden in DCM Digest konvertiert.|  
|**Kopieren**|Erstellt eine Kopie des ausgewählten Konfigurationselements mit einem von Ihnen angegebenen Namen. Vom neuen Konfigurationselement wird keine Beziehung zum ursprünglichen Konfigurationselement beibehalten. Dies bedeutet, dass vom Duplikat des Konfigurationselements keine Konfigurationsinformationen mehr vom ursprünglichen Konfigurationselement übernommen werden.|  
|**Löschen**|Öffnet das Dialogfeld **Konfigurationselement löschen** , in dem Sie Verweise auf dieses Konfigurationselement überprüfen können.<br /><br /> Sie müssen erst alle Verweise auf ein Konfigurationselement entfernen, bevor Sie das Konfigurationselement löschen können.|  

## <a name="manage-configuration-baselines"></a>Verwalten von Konfigurationsbaselines  

-   Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** die Option **Kompatibilitätseinstellungen** > **Konfigurationsbaselines**, und wählen Sie das zu verwaltende Konfigurationselement und dann einen Verwaltungstask aus.  


|Verwaltungstask|Details|  
|---------------------|-------------|  
|**Mitglieder anzeigen**|Zeigt alle Konfigurationselemente an, auf die in der Konfigurationsbasislinie verwiesen wird.|  
|**Zusammenfassung planen**|Konfiguriert den Zeitplan, nach dem die im Knoten **Konfigurationsbaselines** in der Configuration Manager-Konsole angezeigten Daten mit den neuesten Informationen aus der Standortdatenbank aktualisiert werden.|  
|**Zusammenfassung ausführen**|Durch die Zusammenfassung werden Daten im Knoten **Konfigurationsbasislinien** mit den neuesten Daten von der Standortdatenbank aktualisiert. Diese Aktion kann einige Minuten dauern. Möglicherweise müssen Sie auf **Aktualisieren** klicken, damit die neuesten Daten in der Konsole angezeigt werden.|  
|**XML-Definition anzeigen**|Zeigt die XML-Definitionsdatei für die ausgewählte Konfigurationsbasislinie in einem neuen Fenster an. Diese Informationen können hilfreich sein, wenn Sie Konfigurationsdaten manuell erstellen möchten.|  
|**Aktivieren**|Aktiviert eine Konfigurationsbasislinie für die Konformitätsüberwachung.|  
|**Deaktivieren**|Deaktiviert eine Konfigurationsbasislinie, sodass sie auf Clientcomputern nicht mehr auf Konformität bewertet wird. Konfigurationsbasislinien, die diese Konfigurationsbasislinie verweisen werden auch deaktiviert werden.|  
|**Exportierenieren**|Exportiert eine Konfigurationsbasislinie in eine CAB-Datei, unter der Voraussetzung, dass sie an diesem Standort erstellt wurde. Anschließend können Sie das Element in denselben oder einen anderen Configuration Manager-Standort importieren. Konfigurationsdaten werden in DCM Digest konvertiert.<br /><br /> Informationen zum Importieren von Konfigurationsdaten finden Sie unter [Importieren von Konfigurationsdaten](../../compliance/deploy-use/import-configuration-data.md).|  
|**Kopieren**|Erstellt eine Kopie der ausgewählten Konfigurationsbasislinie mit einem von Ihnen angegebenen Namen. Von der neuen Konfigurationsbasislinie wird keine Beziehung zur ursprünglichen Konfigurationsbasislinie beibehalten.|  
|**Löschen**|Öffnet das Dialogfeld **Konfigurationsbasislinie löschen** , in dem Sie Verweise auf diese Konfigurationsbasislinie überprüfen können.<br /><br /> Sie müssen erst alle Verweise auf eine Konfigurationsbasislinie entfernen, bevor Sie die Konfigurationsbasislinie löschen können.|  
|**Bereitstellen**|Öffnet das Dialogfeld **Konfigurationsbasislinien bereitstellen** , in dem Sie eine oder mehrere Konfigurationsbasislinien für Geräte in der Hierarchie bereitstellen können.<br /><br /> Details finden Sie unter [Bereitstellen von Konfigurationsbaselines](../../compliance/deploy-use/deploy-configuration-baselines.md).|  
