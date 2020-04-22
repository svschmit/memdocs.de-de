---
title: Administratorcheckliste für die Energieverwaltung
titleSuffix: Configuration Manager
description: Verwenden der Administratorcheckliste für das Planen und Implementieren der Energieverwaltung in Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 94e42cbe-9df8-4228-a04e-0ad7626180ca
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 039ebf73fba9850b8479bfabab6ab928b7d6f2df
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696658"
---
# <a name="administrator-checklist-for-power-management-in-configuration-manager"></a>Administratorcheckliste für die Energieverwaltung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Diese Administratorcheckliste enthält die empfohlenen Schritte für die Verwendung der Configuration Manager-Energieverwaltung in Ihrer Organisation.  

## <a name="configuring-power-management"></a>Konfigurieren der Energieverwaltung  
 Gehen Sie folgendermaßen vor, um Hilfe beim Konfigurieren der Hierarchie zu erhalten, sodass Energieverwaltungsinformationen von Clientcomputern gesammelt werden können.  

> [!IMPORTANT]  
>  Wenden Sie keine Energiesparpläne auf Computer in Ihrer Hierarchie an, bevor Sie die Energiedaten der Clientcomputer gesammelt und ausgewertet haben. Wenn Sie neue Energieverwaltungseinstellungen auf Computer anwenden, ohne die bestehenden Einstellungen zu untersuchen, könnte dies zu einem Anstieg im Energieverbrauch führen.  

|Aufgabe|Details|  
|----------|-------------|  
|Lesen Sie die Konzepte zur Energieverwaltung in der Configuration Manager-Dokumentationsbibliothek.|Siehe [Introduction to power management (Einführung in die Energieverwaltung)](introduction-to-power-management.md).|  
|Lesen Sie die Voraussetzungen zur Energieverwaltung in der Configuration Manager-Dokumentationsbibliothek.|Siehe [Prerequisites for power management (Voraussetzungen für die Energieverwaltung)](prerequisites-for-power-management.md).|  
|Lesen Sie die Informationen zu bewährten Methoden für die Energieverwaltung.|Siehe [Best practices for power management (Bewährte Methoden für die Energieverwaltung)](best-practices-for-power-management.md).|  
|Konfigurieren Sie Ihre Sammlungen zum Verwalten des Stromverbrauchs von Computern in Ihrer Umgebung.|Verwenden Sie die **Sammlung für die Erstellung von Berichten über Basisdaten**, **Sammlung für die Erstellung von Berichten über Basisdaten**, **Sammlung von Computern, von denen die Energieverwaltung nicht unterstützt wird**, **Sammlungen von Computern, auf die Energiesparpläne angewendet werden**, **Sammlungen von Computern, auf die Energiesparpläne angewendet werden**, und **Sammlungen von Computern, auf denen Windows Server ausgeführt wird**, um die Energieeinstellungen für Computer in Ihrer Hierarchie zu verwalten. Sie können mehrere Sammlungen erstellen und unterschiedliche Energiesparpläne auf jede Sammlung anwenden.|  
|Aktivieren Sie die Energieverwaltung.|Bevor Sie die Energieverwaltung einsetzen können, müssen Sie sie aktivieren und die erforderlichen Clienteinstellungen konfigurieren. Weitere Informationen finden Sie unter [Configuring power management (Konfigurieren der Energieverwaltung)](configuring-power-management.md).|  
|Sammeln Sie die Energieverwaltungsinformationen von Clientcomputern.|Energieverwaltungsdaten werden von Clients über die Configuration Manager-Hardwareinventur gemeldet. Je nach konfiguriertem Zeitplan für die Hardwareinventur kann es einige Zeit dauern, bis das Inventar aller Clientcomputer abgerufen ist.|  

## <a name="monitoring-and-planning-phase"></a>Überwachungs- und Planungsphase  

|Aufgabe|Details|  
|----------|-------------|  
|Führen Sie den Bericht **Computeraktivität**aus.|Im Bericht **Computeraktivität** wird ein Diagramm angezeigt, in dem die Monitor-, Computer- und Benutzeraktivität für eine angegebene Sammlung über einen bestimmten Zeitraum zu sehen ist. Dieser Bericht enthält eine Verknüpfung zum Bericht **Computeraktivitätsdetails** , in dem die Standby- und Aktivierungsfunktionen von Computern einer bestimmten Sammlung angezeigt werden. Weitere Informationen finden Sie unter [How to monitor and plan for power management (Überwachen und Planen der Energieverwaltung in Configuration Manager)](monitor-and-plan-for-power-management.md).|  
|Führen Sie den Bericht **Stromverbrauch** oder **Stromverbrauch nach Tag**aus.|In den Berichten **Stromverbrauch** bzw. **Stromverbrauch nach Tag** wird der monatliche Gesamtstromverbrauch einer bestimmten Sammlung für einen angegebenen Zeitraum in Kilowatt pro Stunde (kWh) angezeigt. Weitere Informationen finden Sie unter [How to monitor and plan for power management (Überwachen und Planen der Energieverwaltung in Configuration Manager)](monitor-and-plan-for-power-management.md).|  
|Führen Sie den Bericht **Umweltbelastung** oder  **Umweltbelastung nach Tag**aus.|In den Berichten **Umweltbelastung** bzw. **Umweltbelastung nach Tag** wird ein Diagramm angezeigt, in dem die durch eine bestimmte Sammlung von Computern während eines bestimmten Zeitraums eingesparte Kohlendioxidemission (CO2) zu sehen ist. Weitere Informationen finden Sie unter [How to monitor and plan for power management (Überwachen und Planen der Energieverwaltung in Configuration Manager)](monitor-and-plan-for-power-management.md).|  
|Führen Sie den Bericht **Stromkosten** oder **Stromkosten nach Tag**aus.|In den Berichten **Stromkosten** bzw. **Stromkosten nach Tag** werden die Gesamtstromkosten während eines bestimmten Zeitraums angezeigt. Weitere Informationen finden Sie unter [How to monitor and plan for power management (Überwachen und Planen der Energieverwaltung in Configuration Manager)](monitor-and-plan-for-power-management.md).|  
|Führen Sie den Bericht **Energiefunktionen**aus.|Im Bericht **Energiefunktionen** werden die Energieverwaltungsfunktionen von Computern in der bestimmten Sammlung angezeigt. Weitere Informationen finden Sie unter [How to monitor and plan for power management (Überwachen und Planen der Energieverwaltung in Configuration Manager)](monitor-and-plan-for-power-management.md).|  
|Führen Sie den Bericht **Energieeinstellungen**aus.|Im Bericht **Energieeinstellungen** wird eine aggregierte Liste der aktuellen Energieeinstellungen angezeigt, die von Computern in einer bestimmten Sammlung verwendet werden. Weitere Informationen finden Sie unter [How to monitor and plan for power management (Überwachen und Planen der Energieverwaltung in Configuration Manager)](monitor-and-plan-for-power-management.md).|  
|Schließen Sie alle erforderlichen Sammlungen von Computern aus der Energieverwaltung aus.|Siehe [Configuring power management (Konfigurieren der Energieverwaltung)](configuring-power-management.md).|  

> [!IMPORTANT]  
>  Stellen Sie sicher, dass Sie die Informationen aus den während der Überwachungs- und Planungsphase generierten Berichten zur Energieverwaltung speichern. Sie können diese Daten mit den während der Erzwingungs- und Kompatibilitätsphasen generierten Energieverwaltungsinformationen vergleichen, um die Einsparungen beim Energieverbrauch, bei den Energiekosten und bei der Umweltbelastung auszuwerten, die durch das Anwenden eines Energiesparplans auf Computer in Ihrer Hierarchie erzielt wurden.  

## <a name="enforcement-phase"></a>Erzwingungsphase  

|Aufgabe|Details|  
|----------|-------------|  
|Wählen Sie für Sammlungen von Computern in der Organisation vorhandene Energiesparpläne aus, oder erstellen Sie neue Energiesparpläne.|Siehe [How to create and apply power plans (Erstellen und Anwenden von Energiesparplänen)](create-and-apply-power-plans.md).|  
|Wenden Sie diese Energiesparpläne auf Computer an.|Siehe [How to create and apply power plans (Erstellen und Anwenden von Energiesparplänen)](create-and-apply-power-plans.md).|  

## <a name="compliance-phase"></a>Kompatibilitätsphase  

|Aufgabe|Details|  
|----------|-------------|  
|Führen Sie den Bericht **Computeraktivität**aus.|Im Bericht **Computeraktivität** wird ein Diagramm angezeigt, in dem die Monitor-, Computer- und Benutzeraktivität für eine angegebene Sammlung über einen bestimmten Zeitraum zu sehen ist. Dieser Bericht enthält eine Verknüpfung zum Bericht **Energieverwaltung - Computeraktivitätsdetails** , in dem die Standby- und Aktivierungsfunktionen von Computern einer bestimmten Sammlung angezeigt werden. Weitere Informationen finden Sie unter [How to monitor and plan for power management (Überwachen und Planen der Energieverwaltung in Configuration Manager)](monitor-and-plan-for-power-management.md).|  
|Führen Sie den Bericht **Stromverbrauch** oder **Stromverbrauch nach Tag**aus.|In den Berichten **Stromverbrauch** bzw. **Stromverbrauch nach Tag** wird der monatliche Gesamtstromverbrauch einer bestimmten Sammlung für einen angegebenen Zeitraum in Kilowatt pro Stunde (kWh) angezeigt. Weitere Informationen finden Sie unter [How to monitor and plan for power management (Überwachen und Planen der Energieverwaltung in Configuration Manager)](monitor-and-plan-for-power-management.md).|  
|Führen Sie den Bericht **Umweltbelastung** oder **Umweltbelastung nach Tag**aus.|In den Berichten **Umweltbelastung** bzw. **Umweltbelastung nach Tag** wird ein Diagramm angezeigt, in dem die durch eine bestimmte Sammlung von Computern während eines bestimmten Zeitraums eingesparte Kohlendioxidemission (CO2) zu sehen ist. Weitere Informationen finden Sie unter [How to monitor and plan for power management (Überwachen und Planen der Energieverwaltung in Configuration Manager)](monitor-and-plan-for-power-management.md).|  
|Führen Sie den Bericht **Stromkosten** oder **Stromkosten nach Tag**aus.|In den Berichten **Stromkosten** bzw. **Stromkosten nach Tag** werden die Gesamtstromkosten während eines bestimmten Zeitraums angezeigt. Weitere Informationen finden Sie unter [How to monitor and plan for power management (Überwachen und Planen der Energieverwaltung in Configuration Manager)](monitor-and-plan-for-power-management.md).|  

## <a name="troubleshooting"></a>Problembehandlung  

|Aufgabe|Details|  
|----------|-------------|  
|Wenn es Computer in der Hierarchie gibt, für die weder der Standby- noch der Ruhezustand aktiviert wurde, führen Sie den Bericht mit dem Namen **Störungsbericht** aus, um mögliche Ursachen anzuzeigen.|Im **Störungsbericht** wird eine Liste der häufigsten Ursachen angezeigt, deretwegen für Computer weder der Standbymodus noch der Ruhezustand aktiviert werden konnte, sowie die Anzahl von Computern, die für einen bestimmten Zeitraum von jeder Ursache betroffen waren. Weitere Informationen finden Sie unter [How to monitor and plan for power management (Überwachen und Planen der Energieverwaltung in Configuration Manager)](monitor-and-plan-for-power-management.md).|  
|Werden mehrere Energiesparpläne auf einen Computer angewendet, so hat der am wenigsten einschränkende Energiesparplan Priorität. Führen Sie den Bericht **Computer mit mehreren Energiesparplänen** aus, um Computer anzuzeigen, auf die mehrere Energiesparpläne angewendet werden.|Siehe **Computers with Multiple Power Plans (Computer mit mehreren Energiesparplänen)**  im Thema [How to Monitor and Plan for Power Management (Überwachen und Planen der Energieverwaltung)](monitor-and-plan-for-power-management.md).|  
