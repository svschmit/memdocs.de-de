---
title: Schützen von Computern vor Schadsoftware
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über das Implementieren von Endpoint Protection in Configuration Manager, um Computer vor Angriffen durch Schadsoftware zu schützen.
ms.date: 05/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 539c7a89-3c03-4571-9cb4-02d455064eeb
author: mestew
ms.author: mstewart
manager: doubeby
ms.openlocfilehash: 6e0e350fe490de50a053e93f2922feba5e0ea8c5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706418"
---
# <a name="example-scenario-use-endpoint-protection-to-protect-computers-from-malware"></a>Beispielszenario: Verwenden von Endpoint Protection zum Schützen von Computern vor Schadsoftware

*Gilt für: Configuration Manager (Current Branch)*

Dieser Artikel enthält ein Beispielszenario zur Implementierung von Endpoint Protection in Configuration Manager, um Computer in Ihrer Organisation vor Angriffen durch Schadsoftware zu schützen.  



## <a name="scenario-overview"></a>Szenarioübersicht

 Die Woodgrove Bank hat Configuration Manager installiert und verwendet die Software. Derzeit verwendet die Bank System Center Endpoint Protection für den Schutz der Computer vor Angriffen durch Schadsoftware. Darüber hinaus verwendet die Bank Windows-Gruppenrichtlinien, um sicherzustellen, dass die Windows-Firewall auf allen Computern im Unternehmen aktiviert ist und Benutzer benachrichtigt werden, wenn die Windows-Firewall ein neues Programm blockiert.  

Die Configuration Manager-Administratoren sollen ein Upgrade für die Antischadsoftware der Woodgrove Bank auf System Center Endpoint Protection durchführen, sodass die Bank die neuesten Antischadsoftware-Features nutzen und die Antischadsoftware-Lösung über die Configuration Manager-Konsole verwalten kann. 


## <a name="business-requirements"></a>Geschäftsanforderungen

Diese Implementierung setzt Folgendes voraus:  

- Verwendung von Configuration Manager zum Verwalten der Einstellungen der Windows-Firewall, die derzeit von der Gruppenrichtlinie verwaltet werden  

- Verwendung von Configuration Manager-Softwareupdates zum Herunterladen von Schadsoftwaredefinitionen auf Computer. Wenn Softwareupdates nicht verfügbar sind, z. B. für den Fall, dass der Computer nicht mit dem Unternehmensnetzwerk verbunden ist, müssen Computer die Definitionsupdates über Microsoft Update herunterladen.  

- Tägliche Ausführung einer schnellen Prüfung auf Schadsoftware auf den Computern der Benutzer. Server müssen hingegen jeden Samstag um 1 Uhr morgens (außerhalb der Geschäftszeiten) eine vollständige Prüfung durchführen.  

- Senden einer E-Mail-Warnung für folgende Ereignisse:  

  -   Schadsoftware wird auf einem der Computer erkannt.  

  -   Dieselbe Bedrohung durch Schadsoftware wird auf mehr als 5 Prozent der Computer gefunden.  

  -   Dieselbe Bedrohung durch Schadsoftware wurde innerhalb von 24 Stunden mehr als fünfmal gefunden.  

  -   Mehr als drei unterschiedliche Arten von Schadsoftware wurden innerhalb von 24 Stunden gefunden.  

  Die Administratoren führen anschließend die folgenden Schritte zur Implementierung von Endpoint Protection aus:  



##  <a name="steps-to-implement-endpoint-protection"></a>Schritte zum Implementieren von Endpoint Protection  

|Prozess|Reference|  
|-------------|---------------|  
|Die Administratoren prüfen die verfügbaren Informationen zu den grundlegenden Konzepten für Endpoint Protection in Configuration Manager.|Weitere Informationen zu Endpoint Protection finden Sie unter [Endpoint Protection](endpoint-protection.md).|  
|Die Administratoren überprüfen und implementieren die erforderlichen Voraussetzungen zur Verwendung von Endpoint Protection.|Informationen zu den erforderlichen Komponenten für Endpoint Protection finden Sie unter [Planung für Endpoint Protection](../plan-design/planning-for-endpoint-protection.md).|  
|Die Administratoren installieren die Endpoint Protection-Standortsystemrolle nur auf einem Standortsystemserver, der sich in der Hierarchie der Woodgrove Bank an höchster Stelle befindet.|Weitere Informationen zum Installieren der Endpoint Protection-Standortsystemrolle finden Sie unter „Voraussetzungen“ in [Konfigurieren von Endpoint Protection](endpoint-protection-configure.md).|  
|Die Administratoren konfigurieren Configuration Manager für die Verwendung eines SMTP-Servers zum Senden der E-Mail-Warnungen.<br /><br /> **Hinweis:** Ein SMTP-Server muss nur konfiguriert werden, wenn Sie per E-Mail benachrichtigt werden möchten, falls eine Endpoint Protection-Warnung generiert wird.|Weitere Informationen finden Sie unter [Configure alerts in Endpoint Protection (Konfigurieren von Warnungen in Endpoint Protection)](endpoint-configure-alerts.md).|  
|Die Administratoren erstellen eine Gerätesammlung, die alle Computer und Server für die Installation des Endpoint Protection-Clients enthält. Sie weisen dieser Sammlung den Namen **Alle durch Endpoint Protection geschützten Computer** zu.<br /><br /> **Tipp:** Für Benutzersammlungen können keine Warnungen konfiguriert werden.|Weitere Informationen zum Erstellen von Sammlungen finden Sie unter [Erstellen von Sammlungen](../../core/clients/manage/collections/create-collections.md).|  
|Die Administratoren konfigurieren die folgenden Warnungen für die Sammlung: <br /><br />1. **Schadsoftware wurde erkannt**: Die Administratoren konfigurieren den Warnungsschweregrad **Kritisch**. <br /><br />2. **Derselbe Schadsoftwaretyp wird auf mehreren Computern erkannt**: Die Administratoren konfigurieren den Warnungsschweregrad **Kritisch** und legen fest, dass die Warnung generiert wird, wenn auf mehr als fünf Prozent der Computer Schadsoftware entdeckt wurde. <br /><br />3. **Derselbe Schadsoftwaretyp wird im angegebenen Intervall wiederholt auf einem Computer erkannt**: Die Administratoren konfigurieren den Warnungsschweregrad „Kritisch“ und legen fest, dass die Warnung generiert wird, wenn in einem Zeitraum von 24 Stunden mehr als fünfmal Schadsoftware entdeckt wurde. <br /><br />4. **Verschiedene Schadsoftwaretypen werden im angegebenen Intervall auf einem Computer erkannt**: Die Administratoren konfigurieren den Warnungsschweregrad „Kritisch“ und legen fest, dass die Warnung generiert wird, wenn in einem Zeitraum von 24 Stunden mehr als drei Schadsoftwaretypen entdeckt wurden.<br /><br /> Der Wert für **Warnungsschweregrad** gibt die Warnungsebene an, die in der Configuration Manager-Konsole und in Warnungen angezeigt wird, die sie in einer E-Mail empfangen.<br /><br /> Außerdem aktivieren sie die Option **Diese Sammlung im Endpoint Protection-Dashboard anzeigen**, damit sie die Warnungen in der Configuration Manager-Konsole überwachen können.|Weitere Informationen finden Sie unter „Konfigurieren von Warnungen für Endpoint Protection“ in [Konfigurieren von Endpoint Protection](endpoint-configure-alerts.md).|  
|Die Administratoren konfigurieren Configuration Manager-Softwareupdates, um drei Mal täglich mithilfe einer automatischen Bereitstellungsregel Definitionsupdates herunterzuladen und bereitzustellen.|Weitere Informationen finden Sie unter „Verwenden von Configuration Manager-Softwareupdates zum Bereitstellen von Definitionsupdates“ in [Use Configuration Manager software updates to deliver definition updates (Verwenden von Configuration Manager-Softwareupdates zum Bereitstellen von Definitionsupdates)](endpoint-definitions-configmgr.md).|  
|Die Administratoren überprüfen die Einstellungen in der Standardrichtlinie für Antischadsoftware, die von Microsoft empfohlene Sicherheitseinstellungen enthält. Damit Computer täglich eine schnelle Überprüfung durchführen können, ändern sie die folgenden Einstellungen:<br /><br /> 1. **Täglich eine Schnellüberprüfung auf Clientcomputern ausführen**: **Ja**.<br /><br /> 2. **Geplante Zeit für tägliche Schnellüberprüfung**:  **9:00 Uhr**.<br /><br /> Die Administratoren bemerken, dass **Von Microsoft Update verteilte Updates** standardmäßig als Quelle von Definitionsupdates ausgewählt ist. Dies erfüllt die Unternehmensanforderung, dass Computer Definitionen von Microsoft Update herunterladen, wenn sie keine Configuration Manager-Softwareupdates empfangen können.|Weitere Informationen finden Sie unter [Erstellen und Bereitstellen von Richtlinien für Antischadsoftware für Endpoint Protection](endpoint-antimalware-policies.md).|  
|Die Administratoren erstellen eine Sammlung, die nur die Woodgrove Bank-Server namens **Woodgrove Bank-Server**enthält.|Weitere Informationen finden Sie unter [Erstellen von Sammlungen](../../core/clients/manage/collections/create-collections.md).|  
|Die Administratoren erstellen eine benutzerdefinierte Richtlinie für Antischadsoftware namens **Woodgrove Bank-Serverrichtlinie**. Sie fügen nur die Einstellungen für **Geplante Überprüfung** hinzu und nehmen folgende Änderungen vor:<br /><br /> **Überprüfungstyp**:  **Vollständig**<br /><br /> **Überprüfungstag**:  **Samstag**<br /><br /> **Überprüfungszeit**: **1:00 Uhr**<br /><br /> **Täglich eine Schnellüberprüfung auf Clientcomputern ausführen**:  **Nein**.|Weitere Informationen finden Sie unter [Erstellen und Bereitstellen von Richtlinien für Antischadsoftware für Endpoint Protection](endpoint-antimalware-policies.md).|  
|Die Administratoren stellen die benutzerdefinierte Richtlinie für Antischadsoftware **Woodgrove Bank-Richtlinie** für die Sammlung **Woodgrove Bank-Server** bereit.|Informationen hierzu finden Sie im Abschnitt„Bereitstellen einer Richtlinie für Antischadsoftware für Clientcomputer“ im Artikel [Erstellen und Bereitstellen von Richtlinien für Antischadsoftware für Endpoint Protection](endpoint-antimalware-policies.md).|  
|Die Administratoren erstellen neue benutzerdefinierte Einstellungen für Clientgeräte für Endpoint Protection und nennen diese **Woodgrove Bank Endpoint Protection-Einstellungen**.<br /><br /> **Hinweis:** Wenn Sie Endpoint Protection nicht auf allen Clients in Ihrer Hierarchie installieren und aktivieren möchten, stellen Sie sicher, dass die Optionen **Endpoint Protection-Client auf Clientcomputern verwalten** und **Endpoint Protection-Client auf Clientcomputern installieren** in den Standardeinstellungen für den Client mit **Nein** konfiguriert sind.|Weitere Informationen finden Sie unter [Konfigurieren Sie benutzerdefinierte Clienteinstellungen für Endpoint Protection](endpoint-protection-configure-client.md).|  
|Die Administratoren konfigurieren die folgenden Einstellungen für Endpoint Protection:<br /><br /> **Endpoint Protection-Client auf Clientcomputern verwalten**:  **Ja**<br /><br /> Diese Einstellung und der entsprechende Wert stellen sicher, dass jeder vorhandene Endpoint Protection-Client, der installiert ist, von Configuration Manager verwaltet wird.<br /><br /> **Endpoint Protection-Client auf Clientcomputern installieren**:  **Ja**.</br></br>**Hinweis:** Ab der Configuration Manager-Version 1802 muss für Windows 10-Geräte der Endpoint Protection-Agent nicht mehr installiert werden. Wenn dieser bereits auf Windows 10-Geräten installiert ist, wird er von Configuration Manager nicht entfernt. Administratoren können den Endpoint Protection-Agent auf Windows 10-Geräten entfernen, auf denen die Clientversion 1802 oder eine neuere Version ausgeführt wird.|Weitere Informationen finden Sie unter [Konfigurieren Sie benutzerdefinierte Clienteinstellungen für Endpoint Protection](endpoint-protection-configure-client.md).|  
|Die Administratoren stellen die Clienteinstellungen für **Woodgrove Bank Endpoint Protection-Einstellungen** für die Sammlung **Alle durch Endpoint Protection geschützten Computer** bereit.|Weitere Informationen finden Sie unter „Konfigurieren Sie benutzerdefinierte Clienteinstellungen für Endpoint Protection“ in [Konfigurieren von Endpoint Protection in Configuration Manager](endpoint-antimalware-policies.md).|  
|Die Administratoren verwenden den Assistenten zum Erstellen von Windows-Firewall-Richtlinien, um eine Richtlinie zu erstellen, indem sie die folgenden Einstellungen für das Domänenprofil konfigurieren:<br /><br /> 1. **Windows-Firewall aktivieren**: **Ja**<br /><br /> 2)<br />                    **Benutzer benachrichtigen, wenn ein neues Programm von der Windows-Firewall blockiert wird**: **Ja**|Weitere Informationen finden Sie unter [Erstellen und Bereitstellen von Windows-Firewall-Richtlinien für Endpoint Protection](../../protect/deploy-use/create-windows-firewall-policies.md).|  
|Die Administratoren stellen die neue Firewallrichtlinie für die Sammlung **Alle durch Endpoint Protection geschützten Computer** bereit, die sie zuvor erstellt haben.|Weitere Informationen finden Sie unter „So stellen Sie eine Windows-Firewall-Richtlinie bereit“ in [Erstellen und Bereitstellen von Windows-Firewall-Richtlinien für Endpoint Protection](create-windows-firewall-policies.md).|  
|Die Administratoren verwenden die verfügbaren Verwaltungsaufgaben für Endpoint Protection, um Antischadsoftware und Windows-Firewallrichtlinien zu verwalten, bedarfsgesteuerte Überprüfungen von Computern durchzuführen und auf Computern zu erzwingen, dass die neuesten Definitionen heruntergeladen werden. Außerdem werden sie dazu verwendet, um weitere Maßnahmen anzugeben, die bei der Erkennung von Schadsoftware eingeleitet werden.|Weitere Informationen finden Sie unter [Verwalten von Richtlinien für Antischadsoftware und Firewalleinstellungen für Endpoint Protection](endpoint-antimalware-firewall.md).|  
|Die Administratoren verwenden die folgenden Methoden zum Überwachen des Status von Endpoint Protection und der von Endpoint Protection durchzuführenden Aktionen:<br /><br /> 1) Mithilfe des Knotens **Endpoint Protection-Status** unter **Sicherheit** im Arbeitsbereich **Überwachung**<br /><br /> 2) Mithilfe des Knotens **Endpoint Protection** im Arbeitsbereich **Bestand und Kompatibilität**<br /><br /> 3) Mithilfe der integrierten Configuration Manager-Berichte|Weitere Informationen finden Sie unter [So überwachen Sie Endpoint Protection](monitor-endpoint-protection.md).|  

 Die Administratoren melden ihrem Vorgesetzten eine erfolgreiche Implementierung von Endpoint Protection und bestätigen, dass die Computer der Woodgrove Bank jetzt gemäß den angegebenen Unternehmensanforderungen vor Antischadsoftware geschützt sind. 

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen finden Sie unter [How to Configure Endpoint Protection (Konfigurieren von Endpoint Protection)](endpoint-protection-configure.md).