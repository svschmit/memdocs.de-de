---
title: Beispielszenario für die Bereitstellung und Überwachung von Updates
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Softwareupdates in Configuration Manager zur Bereitstellung und Überwachung monatlicher Softwareupdates verwenden.
ms.date: 10/21/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: c32f757a-02da-43f2-b055-5cfd097d8c43
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ea654c4ec13b95b78a65c85d9d36ce576619854e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696128"
---
# <a name="example-scenario-to-deploy-and-monitor-monthly-software-updates"></a>Beispielszenario für die Bereitstellung und Überwachung monatlicher Softwareupdates

*Gilt für: Configuration Manager (Current Branch)*

Dieses Thema beschreibt anhand eines Beispielszenarios, wie Sie Softwareupdates in Configuration Manager verwenden können, um die von Microsoft monatlich veröffentlichten Sicherheitssoftwareupdates bereitzustellen und zu überwachen.  

 In diesem Szenario folgen wird den Aktionen des Configuration Manager-Administrators bei der Woodgrove Bank. Der Administrator muss eine Bereitstellungsstrategie für Softwareupdates mit folgenden Bedingungen und Anforderungen erstellen:  

- Eine aktive Softwareupdatebereitstellung wird eine Woche nach Veröffentlichung der Sicherheitssoftwareupdates durch Microsoft, jeden zweiten Dienstag des Monats, durchgeführt. Dieses Ereignis wird in der Regel als Patch-Dienstag bezeichnet.  

- Softwareupdates werden heruntergeladen und auf Verteilungspunkten bereitgestellt. Dann wird die Bereitstellung auf einer Teilmenge von Clients getestet, bevor der Configuration Manager-Administrator die Softwareupdates vollständig in seiner Produktionsumgebung bereitstellt.  

- Der Administrator muss die Konformität der Softwareupdates pro Monat oder Jahr überwachen können.  

  In diesem Szenario wird davon ausgegangen, dass die Infrastruktur der Softwareupdatepunkte bereits implementiert wurde. Verwenden Sie die folgenden Informationen zum Planen und Konfigurieren von Softwareupdates in Configuration Manager.  

|Prozess|Reference|  
|-------------|---------------|  
|Überprüfen der wichtigsten Konzepte für die Softwareupdates.|[Einführung zu Softwareupdates](../understand/software-updates-introduction.md)|  
|Einplanen von Softwareupdates. Diese Informationen helfen Ihnen beim Planen im Hinblick auf Kapazitätsüberlegungen, bei der Ermittlung der Infrastruktur der Softwareupdatepunkte, der Installation von Softwareupdatepunkten, bei Synchronisierungseinstellungen sowie den Clienteinstellungen für Softwareupdates.|[Planen von Softwareupdates](../plan-design/plan-for-software-updates.md)|  
|Konfigurieren von Softwareupdates. Diese Informationen helfen Ihnen beim Installieren und Konfigurieren von Softwareupdatepunkten in der Hierarchie sowie beim Konfigurieren und Synchronisieren von Softwareupdates.<br /><br /> In diesem Szenario konfiguriert der Configuration Manager-Administrator den Zeitplan für die Softwareupdatesynchronisierung so, dass diese am zweiten Mittwoch jedes Monats ausgeführt wird, um sicherzustellen, dass immer die neuesten Sicherheitssoftwareupdates von Microsoft abgerufen werden.|[Synchronisieren von Softwareupdates](../get-started/synchronize-software-updates.md)|  

 In den folgenden Abschnitten in diesem Thema wird eine beispielhafte Schritt-für-Schritt-Anleitung zur Verfügung gestellt, um Ihnen beim Bereitstellen und Überwachen der Sicherheitssoftwareupdates für Configuration Manager in Ihrem Unternehmen zu helfen.

##  <a name="step-1-create-a-software-update-group-for-yearly-compliance"></a><a name="BKMK_Step1"></a> Schritt 1: Erstellen einer Softwareupdategruppe für jährliche Konformität  
 Der Configuration Manager-Administrator erstellt eine Softwareupdategruppe, die zur Überwachung der Konformität aller Sicherheitssoftwareupdates, die 2016 veröffentlicht wurden, verwendet werden kann. Der Administrator führt die Schritte in der folgenden Tabelle aus.  

|Prozess|Reference|  
|-------------|---------------|  
|Der Configuration Manager-Administrator fügt in der Configuration Manager-Konsole im Knoten **Alle Softwareupdates** Kriterien hinzu, um nur Sicherheitssoftwareupdates anzuzeigen, die im Jahr 2015 veröffentlicht oder überarbeitet wurden und folgende Kriterien erfüllen:<br /><br /><ul><li>**Kriterien:** Veröffentlichungs- oder Überarbeitungsdatum</li><li>**Bedingung**: stimmt mit einem bestimmten Datum überein oder liegt danach<br />**Wert:** 1.1.2015</li><li>**Kriterien:** Updateklassifizierung<br />**Wert:** Sicherheitsupdates</li><li>**Kriterien:** Abgelaufen <br />**Wert:** Nein</li></ul>|Keine weiteren Informationen|
|Der Configuration Manager-Administrator fügt alle gefilterten Softwareupdates zur neuen Softwareupdategruppe mit folgenden Anforderungen hinzu:<br /><br /><ul><li>**Name:** Konformitätsgruppe – Microsoft-Sicherheitsupdates 2015</li><li>**Beschreibung:** Softwareupdates|[Hinzufügen von Softwareupdates zu einer Updategruppe](add-software-updates-to-an-update-group.md)|  

##  <a name="step-2-create-an-automatic-deployment-rule-for-the-current-month"></a><a name="BKMK_Step2"></a> Schritt 2: Erstellen einer automatischen Bereitstellungsregel für den aktuellen Monat  
 Der Configuration Manager-Administrator erstellt eine automatische Bereitstellungsregel für Sicherheitssoftwareupdates, die von Microsoft für den laufenden Monat veröffentlicht werden. Der Administrator führt die Schritte in der folgenden Tabelle aus.  

|Prozess|Reference|  
|-------------|---------------|  
|Der Configuration Manager-Administrator erstellt eine automatische Bereitstellungsregel mit folgenden Anforderungen:<br /><br /><ol><li>Auf der Registerkarte **Allgemein** nimmt der Configuration Manager-Administrator folgende Konfiguration vor:<br /> <ul><li>Er legt **Monatliche Sicherheitsupdates** für den Namen fest.</li><li>Er wählt eine Testsammlung mit einer begrenzten Anzahl von Clients aus.</li><li>Er wählt **Erstellen einer neuen Softwareupdategruppe** aus.</li><li>Er stellt sicher, dass **Bereitstellen nach Ausführung dieser Regel aktivieren** nicht aktiviert ist.</li></ul></li><li>Auf der Registerkarte **Bereitstellungseinstellungen** wählt der Configuration Manager-Administrator die Standardeinstellungen aus.</li><li>Auf der Seite **Softwareupdates** konfiguriert der Configuration Manager-Administrator folgende Eigenschaftsfilter und Suchkriterien:<br /><ul><li>Veröffentlichungs- oder Überarbeitungsdatum **Letzter Monat**.</li><li>Updateklassifizierung **Sicherheitsupdates**.</li></ul></li><li>Auf der Seite **Auswertung** aktiviert der Configuration Manager-Administrator die Regel zur Ausführung gemäß Zeitplan am **zweiten Donnerstag** jedes **Monats**.  Außerdem stellt der Configuration Manager-Administrator sicher, dass der Synchronisierungszeitplan für die Ausführung am **zweiten Mittwoch** jedes **Monats** eingerichtet ist.</li><li>Der Configuration Manager-Administrator verwendet die Standardeinstellungen auf den Seiten für Bereitstellungszeitplan, Benutzerfreundlichkeit, Warnungen und Downloadeinstellungen.</li><li>Auf der Seite **Bereitstellungspakete** legt der Configuration Manager-Administrator ein neues Bereitstellungspaket fest.</li><li>Der Configuration Manager-Administrator verwendet die Standardeinstellungen auf den Seiten für Downloadort und Sprachauswahl.</li></ol>|[Automatisches Bereitstellen von Softwareupdates](automatically-deploy-software-updates.md)|  

##  <a name="step-3-verify-that-software-updates-are-ready-to-deploy"></a><a name="BKMK_Step3"></a> Schritt 3: Überprüfen, ob Softwareupdates bereitgestellt werden können  
 Am zweiten Donnerstag jedes Monats überprüft der Configuration Manager-Administrator, ob die Softwareupdates bereitgestellt werden können. Der Administrator führt den folgenden Schritt aus.  

|Prozess|Reference|  
|-------------|---------------|  
|Der Configuration Manager-Administrator überprüft, ob die Synchronisierung der Softwareupdates erfolgreich abgeschlossen wurde.|[Status der Softwareupdatesynchronisierung](monitor-software-updates.md#BKMK_SUSyncStatus)|  

##  <a name="step-4-deploy-the-software-update-group"></a><a name="BKMK_Step4"></a> Schritt 4: Bereitstellen der Softwareupdategruppe  
 Nachdem der Configuration Manager-Administrator überprüft hat, ob die Softwareupdates bereitgestellt werden können, werden sie bereitgestellt. Der Administrator führt die Schritte in der folgenden Tabelle aus.  

|Prozess|Reference|  
|-------------|---------------|  
|Der Configuration Manager-Administrator erstellt zwei Testbereitstellungen für die neue Softwareupdategruppe. Er berücksichtigt die folgenden Umgebungen für jede Bereitstellung:<br /><br /> **Arbeitsstation-Testbereitstellung**: Der Configuration Manager-Administrator berücksichtigt bei der Testbereitstellung für Arbeitsstationen Folgendes:<br /><br /><ul><li>Er gibt eine Bereitstellungssammlung an, die eine Teilmenge der Arbeitsstationsclients enthält, um die Bereitstellung zu überprüfen.</li><li>Er konfiguriert die Bereitstellungseinstellungen, die für die Arbeitsstationsclients in seiner Umgebung zutreffen.</li></ul><br />**Servertestbereitstellung**: Der Configuration Manager-Administrator berücksichtigt bei der Testbereitstellung für Server Folgendes:<br /><br /><ul><li>Er gibt eine Bereitstellungssammlung an, die eine Teilmenge der Serverclients enthält, um die Bereitstellung zu überprüfen.</li><li>Er konfiguriert die Bereitstellungseinstellungen, die für die Serverclients in seiner Umgebung zutreffen.</li></ul>|[Bereitstellen von Softwareupdates](deploy-software-updates.md)|  
|Der Configuration Manager-Administrator überprüft, ob die Testbereitstellungen erfolgreich waren.|[Status der Softwareupdatebereitstellung](monitor-software-updates.md#BKMK_SUDeployStatus)|  
|Der Configuration Manager-Administrator aktualisiert die beiden Bereitstellungen mit neuen Sammlungen, die seine Produktionsarbeitsstationen und -server umfassen.|Keine weiteren Informationen|  

##  <a name="step-5-monitor-compliance-for-deployed-software-updates"></a><a name="BKMK_Step5"></a> Schritt 5: Überwachen der Konformität bereitgestellter Softwareupdates  
 Der Configuration Manager-Administrator überwacht die Konformität seiner Softwareupdatebereitstellungen. Der Administrator führt den Schritt in der folgenden Tabelle aus.  

|Prozess|Reference|  
|-------------|---------------|  
|Der Configuration Manager-Administrator überwacht den Status der Softwareupdatebereitstellung in der Configuration Manager-Konsole und überprüft die in der Konsole verfügbaren Berichte zur Softwareupdatebereitstellung.|[Überwachen von Softwareupdates](../../sum/deploy-use/monitor-software-updates.md)|  

##  <a name="step-6-add-monthly-software-updates-to-the-yearly-update-group"></a><a name="BKMK_Step6"></a> Schritt 6: Hinzufügen monatlicher Softwareupdates zur jährlichen Updategruppe  
 Der Configuration Manager-Administrator fügt die Softwareupdates aus der monatlichen Softwareupdategruppe zur jährlichen Softwareupdategruppe hinzu. Der Administrator führt den Schritt in der folgenden Tabelle aus.  

|Prozess|Reference|  
|-------------|---------------|  
|Der Configuration Manager-Administrator wählt die Softwareupdates aus der monatlichen Softwareupdategruppe aus und fügt sie zu der Softwareupdategruppe hinzu, die er für die jährliche Konformität erstellt hat. Er verfolgt die Softwareupdatekonformität und erstellt verschiedene Berichte für die Geschäftsleitung.|[Hinzufügen von Softwareupdates zu einer bereitgestellten Updategruppe](add-software-updates-to-an-update-group.md)|  

Der Configuration Manager-Administrator hat die monatliche Bereitstellung für Sicherheitssoftwareupdates erfolgreich abgeschlossen. Er überwacht weiterhin die Konformität der Softwareupdates und erstellt Berichte dazu, um sicherzustellen, dass sich die Clients in der Umgebung innerhalb der zulässigen Konformitätsstufen bewegen.  

##  <a name="recurring-monthly-process-to-deploy-software-updates"></a><a name="BKMK_MonthlyProcess"></a> Regelmäßiger monatlicher Prozess zur Bereitstellung von Softwareupdates  
 Nach dem ersten Monat, in dem der Configuration Manager-Administrator Softwareupdates bereitgestellt hat, führt er die Schritte 3 bis 6 aus, um die von Microsoft veröffentlichten monatlichen Sicherheitssoftwareupdates bereitzustellen.  
