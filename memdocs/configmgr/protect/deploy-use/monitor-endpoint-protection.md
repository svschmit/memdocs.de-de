---
title: Überwachen des Endpoint Protection-Status
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Endpoint Protection in der Configuration Manager-Hierarchie überwachen.
ms.date: 03/13/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f4a1335c-bb3d-493e-a124-83a32a107dc8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 18bbbfc6486a1e5a784603e6725629d966f6c11a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706278"
---
# <a name="how-to-monitor-endpoint-protection-status"></a>So überwachen Sie den Endpoint Protection-Status

*Gilt für: Configuration Manager (Current Branch)*

Sie können Endpoint Protection in der Microsoft Configuration Manager-Hierarchie mithilfe des Knotens **Endpoint Protection-Status** unter **Sicherheit** im Arbeitsbereich **Überwachung**, mithilfe des Knotens **Endpoint Protection** im Arbeitsbereich **Bestand und Kompatibilität** und mithilfe von Berichten überwachen.  

##  <a name="how-to-monitor-endpoint-protection-by-using-the-endpoint-protection-status-node"></a><a name="BKMK_1"></a> Überwachen von Endpoint Protection mithilfe des Knotens „Endpoint Protection-Status“  

1. Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2. Erweitern Sie im Arbeitsbereich **Überwachung** die Option **Sicherheit**, und klicken Sie auf **Endpoint Protection-Status**.  

3. Wählen Sie in der Liste **Sammlung** die Sammlung aus, für die Sie Statusinformationen anzeigen möchten.  

   > [!IMPORTANT]
   >  Sammlungen können in den folgenden Fällen ausgewählt werden:  
   > 
   > - Wenn Sie **Diese Sammlung im Endpoint Protection-Dashboard anzeigen** auf der Registerkarte **Warnungen** im Dialogfeld <em><Sammlungsname\></em>**Eigenschaften** auswählen.  
   >   -   Wenn Sie eine Endpoint Protection-Antischadsoftware-Richtlinie für die Sammlung bereitstellen.  
   >   -   Wenn Sie Endpoint Protection-Clienteinstellungen für die Sammlung aktivieren und bereitstellen.  

4. Überprüfen Sie die Informationen, die angezeigt wird, in der **Sicherheitsstatus** und **Betriebsstatus** Abschnitte. Sie können auf eine beliebige Statusverknüpfung klicken, um im Arbeitsbereich **Bestand und Kompatibilität** unter dem Knoten **Geräte** eine temporäre Sammlung zu erstellen. Die temporäre Sammlung enthält die Computer mit dem ausgewählten Status.  

   > [!IMPORTANT]  
   >  Informationen, die im Knoten **Endpoint Protection-Status** angezeigt werden, basieren auf den letzten Daten, die von der Configuration Manager-Datenbank zusammengefasst wurden, und sind möglicherweise nicht aktuell. Wenn Sie die aktuellen Daten abrufen möchten, klicken Sie auf der Registerkarte **Startseite** auf **Zusammenfassung ausführen**, oder klicken Sie auf **Zusammenfassung planen** , um das Zusammenfassungsintervall anzupassen.  

##  <a name="how-to-monitor-endpoint-protection-in-the-assets-and-compliance-workspace"></a><a name="BKMK_2"></a> Überwachen von Endpoint Protection im Arbeitsbereich „Bestand und Kompatibilität“  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Führen Sie im Arbeitsbereich **Bestand und Kompatibilität** eine der folgenden Aktionen aus:  

    -   Klicken Sie auf **Geräte**. Wählen Sie in der Liste **Geräte** einen Computer aus, und klicken Sie dann auf die Registerkarte **Schadsoftwaredetails** .  

    -   Klicken Sie auf **Gerätesammlungen**. Wählen Sie in der Liste **Gerätesammlungen** die Sammlung mit dem zu überwachenden Computer aus, und klicken Sie anschließend auf der Registerkarte **Startseite** in der Gruppe **Sammlung** auf **Mitglieder anzeigen**.  

3.  Wählen Sie in der Liste *<Sammlungsname\>* einen Computer aus, und klicken Sie dann auf die Registerkarte **Schadsoftwaredetails**.  

##  <a name="how-to-monitor-endpoint-protection-by-using-reports"></a><a name="BKMK_3"></a> Überwachen von Endpoint Protection in Configuration Manager  
 Verwenden Sie die folgenden Berichte, um Informationen zu Endpoint Protection in der Hierarchie übersichtlich angezeigt zu bekommen. Sie können diese Berichte auch verwenden, um Probleme mit Endpoint Protection zu beheben. Weitere Informationen zum Konfigurieren der Berichterstellung in Configuration Manager finden Sie unter [Einführung in die Berichterstellung](../../core/servers/manage/introduction-to-reporting.md) und [Protokolldateien](../../core/plan-design/hierarchy/log-files.md). Die Endpoint Protection-Berichte befinden sich im Ordner „Endpoint Protection“.  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|**Aktivitätsbericht für Antischadsoftware**|Zeigt eine Übersicht der Antischadsoftware-Aktivität für eine bestimmte Sammlung an.|  
|**Infizierte Computer**|Zeigt eine Liste der Computer, auf denen eine angegebene Bedrohung erkannt wird.|  
|**Benutzer nach häufigsten Bedrohungen**|Zeigt eine Liste der Benutzer mit der höchsten Anzahl an erkannten Bedrohungen an.|  
|**Benutzerspezifische Bedrohungsliste**|Zeigt eine Liste von Risiken, die für eine angegebene Benutzerkonto gefunden wurden.|  

## <a name="malware-alert-levels"></a>Malwarewarnstufen  
 Verwenden Sie die folgende Tabelle zum Identifizieren der verschiedenen Endpoint Protection-Benachrichtigungsebenen, die in Berichten oder in der Configuration Manager-Konsole angezeigt werden können.  

|Warnstufe|Beschreibung|  
|-----------------|-----------------|  
|**Fehlgeschlagen**|Fehler von Endpoint Protection beim Beheben der Schadsoftware. Überprüfen Sie die Protokolle für die Details des Fehlers.<br /><br /> **Hinweis:** Eine Liste der Configuration Manager- und Endpoint Protection-Protokolldateien finden Sie im Abschnitt „Endpoint Protection“ im Thema [Protokolldateien](../../core/plan-design/hierarchy/log-files.md).|  
|**Entfernt**|Endpoint Protection hat die Schadsoftware erfolgreich entfernt.|  
|**Isoliert**|Endpoint Protection hat die Schadsoftware an einen sicheren Speicherort verschoben und verhindert, dass sie ausgeführt wird, bis Sie sie entfernen oder erlauben, dass sie ausgeführt wird.|  
|**Bereinigt**|Die Malware wurde aus der infizierten Datei bereinigt.|  
|**Zulässig**|Ein Administrator ausgewählt, um die Software zu ermöglichen, die die Malware ausgeführt wird.|  
|**Keine Aktion**|Endpoint Protection hat keine Aktion auf der Schadsoftware ausgeführt. Dies kann vorkommen, wenn der Computer neu gestartet wird, nach Malware erkannt wird, und die Malware wird nicht mehr erkannt; z. B. wenn ein zugeordnetes Netzlaufwerk auf ist denen Malware entdeckt wurde keine Verbindung beim Neustart des Computers.|  
|**Gesperrt**|Endpoint Protection hat das Ausführen der Schadsoftware blockiert. Dies kann auftreten, wenn ein Prozess auf dem Computer gefunden wird, um Malware enthalten.|
