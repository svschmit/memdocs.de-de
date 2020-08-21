---
title: Zusätzliche Datenschutzinformationen
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Microsoft Daten aus Configuration Manager sammelt und verwendet.
ms.date: 09/04/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1fcc921f-085f-4b0b-9c53-1e0707211076
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f6d3f6dbbbb407ee63eb8253cbf3ca740a10479c
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699788"
---
# <a name="additional-information-about-privacy-for-configuration-manager"></a>Weitere Informationen zum Datenschutz für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*


## <a name="updates-and-servicing"></a>Updates und Wartung

Configuration Manager verwendet ein Updatemodell, mit dem Sie Ihre Umgebung dank den neuesten Updates und Funktionen auf dem aktuellen Stand halten können. Diese Funktion verwendet eine Standortsystemrolle namens „Dienstverbindungspunkt“. Sie bestimmen den Server, auf dem diese Rolle installiert wird. 

Weitere Informationen zum Sammeln und Verwenden von Informationen finden Sie unter [Nutzungsdaten](#usage-data).



## <a name="usage-data"></a>Nutzungsdaten

Configuration Manager sammelt interne Diagnose- und Nutzungsdaten, mit deren Hilfe Microsoft Anwendungsinstallation, Qualität und Sicherheit künftiger Releases verbessert.
Diagnose- und Nutzungsdaten sind für jede Configuration Manager-Hierarchie aktiviert. Sie bestehen aus SQL Server-Abfragen, die wöchentlich an jedem primären Standort und am Standort der zentralen Verwaltung ausgeführt werden. Wenn die Hierarchie einen Standort der zentralen Verwaltung verwendet, werden die Daten von primären Standorten dann an diesen Standort repliziert. Am obersten Standort Ihrer Hierarchie sendet der Dienstverbindungspunkt diese Informationen, wenn er prüft, ob Updates vorhanden sind. Wenn sich der Dienstverbindungspunkt im Offlinemodus befindet, werden die Informationen mithilfe des Dienstverbindungstools übertragen.

Configuration Manager sammelt Daten nur von der SQL Server-Datenbank des Standorts – nicht direkt von Clients oder Standortservern.

Administratoren können die Ebene der Datensammlung in der Configuration Manager-Konsole im Abschnitt **Nutzungsdaten** ändern.

Weitere Informationen zu den Ebenen der Datensammlung finden Sie unter [Diagnose- und Nutzungsdaten](../diagnostics/diagnostics-and-usage-data.md).



## <a name="log-analytics-connector"></a>Log Analytics-Connector

Der Log Analytics-Connector synchronisiert Daten, z.B. Sammlungen, aus Configuration Manager mit dem Azure-Clouddienst. Die Azure-Abonnement-ID und der geheime Schlüssel werden in der Configuration Manager-Datenbank gespeichert, wenn ein Administrator die Funktion konfiguriert. Sowohl der geheime Azure Active Directory-Clientschlüssel als auch der gemeinsam verwendete Schlüssel des Azure-Arbeitsbereichs werden in der lokalen Configuration Manager-Datenbank gespeichert. Für alle Kommunikationsvorgänge zwischen Configuration Manager und Azure wird HTTPS verwendet. Außer zufälligen Diagnose- und Nutzungsdaten erhält Microsoft keine weiteren Informationen zu gesammelten Daten. 

Weitere Informationen zu den von Log Analytics erfassten Daten finden Sie unter [Log Analytics-Datensicherheit](/azure/log-analytics/log-analytics-data-security).



## <a name="asset-intelligence"></a>Asset Intelligence

Mit Asset Intelligence können Administratoren die Konformität mit Konfigurationsstandards definieren, nachverfolgen und proaktiv verwalten. Durch Messungen und Berichterstattung zu Bereitstellung und Verwendung sowohl physischer als auch virtueller Anwendungen werden den Organisationen gute Geschäftsentscheidungen zur Softwarelizenzierung und die Einhaltung von Lizenzverträgen erleichtert. Nachdem Nutzungsdaten von Konfigurations-Manager-Clients gesammelt wurden, können Sie verschiedene Funktionen verwenden, um Daten wie Sammlungen, Abfragen und Berichte anzuzeigen.

Bei jeder Synchronisierung wird ein Katalog bekannter Software von Microsoft heruntergeladen. Sie können Informationen über nicht kategorisierte Softwaretitel senden, die in ihrer Organisation gefunden wurden, um entsprechende Recherchen auszuführen und die Informationen dem Katalog hinzuzufügen. Vor dem Hochladen dieser Informationen werden in einem Dialogfeld die Daten angezeigt, die hochgeladen werden sollen. Hochgeladene Daten können nicht zurückgerufen werden. Asset Intelligence sendet keine Informationen zu Benutzer, Computer oder Lizenzverwendung an Microsoft.

Nachdem ein Softwaretitel hochgeladen wurde, können die Microsoft-Mitarbeiter diesen identifizieren und kategorisieren und danach dieses Wissen allen anderen Kunden, die dieses Feature verwenden, sowie anderen Kunden des Katalogs zur Verfügung stellen. Alle hochgeladenen Softwaretitel werden öffentlich. Die Anwendung und ihre Kategorisierung werden Teil des Katalogs und können für andere Kunden des Katalogs heruntergeladen werden. Berücksichtigen Sie beim Konfigurieren der Asset Intelligence-Datensammlung und bei der Entscheidung, ob Informationen an System Center Online übermittelt werden sollen, die Datenschutzanforderungen Ihrer Organisation.

Asset Intelligence ist nicht standardmäßig in Configuration Manager aktiviert. Nicht kategorisierte Titel werden nie automatisch hochgeladen. Das System ist nicht darauf ausgelegt, diese Aufgabe zu automatisieren. Sie müssen den Upload jedes Softwaretitels manuell auswählen und genehmigen.



## <a name="endpoint-protection"></a>Endpoint Protection

Microsoft Cloud Protection Service wurde früher als Microsoft Active Protection Service oder MAPS bezeichnet.

Die relevanten Produkte sind System Center Endpoint Protection und das Endpoint Protection-Feature von Configuration Manager (für die Verwaltung von System Center Endpoint Protection und Windows Defender für Windows 10). Diese Funktion ist für System Center Endpoint Protection für Linux oder Mac nicht implementiert.

Die Microsoft Cloud Protection Service-Antimalware-Community ist eine freiwillige weltweite Online-Community, die System Center Endpoint Protection-Benutzer umfasst. Wenn Sie Microsoft Cloud Protection Service beitreten, sendet System Center Endpoint Protection automatisch Informationen an Microsoft. Anhand dieser Informationen bestimmt Microsoft die Software, die auf mögliche Bedrohungen prüft und zur Verbesserung der Effektivität von System Center Endpoint Protection beiträgt. Diese Community hilft bei der Eindämmung neuer Infektionen mit Schadsoftware. Wenn ein Microsoft Cloud Protection Service-Bericht Details zu Schadsoftware oder potenziell unerwünschter Software enthält, die möglicherweise vom Endpoint Protection-Client entfernt werden kann, lädt Microsoft Cloud Protection Service die jüngste Signatur herunter, um für Abhilfe zu sorgen. Microsoft Cloud Protection Service kann auch „falsch positive Ergebnisse“ ermitteln und beheben. Falsch positive Ergebnisse liegen vor, wenn ein Element als Schadsoftware identifiziert wird, obwohl es keine ist. 

Microsoft Cloud Protection Service-Berichte enthalten Informationen zu potenziellen Schadsoftwaredateien, wie z.B. Dateinamen, kryptografische Hashwerte, Anbieter, Größe und Datumsstempel. Darüber hinaus sammelt Microsoft Cloud Protection Service möglicherweise vollständige URLs, um den Ursprung der Datei anzugeben. Die URLs können gelegentlich persönliche Informationen wie Suchbegriffe oder in Formularen eingegebene Daten enthalten. Berichte können auch die Aktionen enthalten, die Sie vorgenommen haben, wenn Endpoint Protection Sie über unerwünschte Software informiert hat. Microsoft Cloud Protection Service-Berichte enthalten diese Informationen, damit Microsoft beurteilen kann, wie effektiv Endpoint Protection Malware und potenziell unerwünschte Software erkennen und entfernen kann und versuchen kann, neue Malware zu identifizieren.

Sie können Microsoft Cloud Protection Service beitreten, wenn Sie eine einfache Mitgliedschaft oder eine Premiummitgliedschaft besitzen. In einfachen Mitgliederberichten sind die oben beschriebenen Informationen enthalten. Premiummitgliederberichte sind umfangreicher und können zusätzliche Details über die von Endpoint Protection erkannte Software enthalten, darunter den Speicherort der Software, Dateinamen, die Funktionsweise der Software sowie deren Auswirkungen auf den Computer. Anhand dieser Berichte und der Berichte anderer Endpoint Protection-Benutzer, die an Microsoft Cloud Protection Service teilnehmen, können Microsoft-Mitarbeiter neue Bedrohungen schneller erkennen. Anschließend werden Schadsoftwaredefinitionen für Programme erstellt, die den Analysekriterien entsprechen, und als aktualisierte Definitionen allen Benutzern über Microsoft Update zugänglich gemacht.

Zur besseren Erkennung und Behebung bestimmter Infektionen mit Schadsoftware sendet das Produkt regelmäßig Informationen zum Sicherheitszustand des PCs an Microsoft Cloud Protection Service. Diese Informationen umfassen Details zu den Sicherheitseinstellungen des PCs sowie Protokolldateien, in denen die Treiber und andere Software beschrieben sind, die beim Starten des PCs geladen werden.

Eine Nummer, die Ihren PC eindeutig identifiziert, wird ebenfalls gesendet. Möglicherweise werden von Microsoft Cloud Protection Service die IP-Adressen gesammelt, mit denen die potenziellen Schadsoftwaredateien eine Verbindung herstellen.

Microsoft Cloud Protection Service-Berichte werden zur Verbesserung der Softwareprodukte und Dienste von Microsoft verwendet. Die Berichte können außerdem zu Statistik-, Test- oder Analysezwecken sowie zur Erstellung von Definitionen verwendet werden. Nur Mitarbeiter, Auftragnehmer, Partner und Lieferanten von Microsoft, die diese Berichte für ihre Arbeit benötigen, erhalten Zugriff darauf.

Die Erfassung persönlicher Informationen durch Microsoft Cloud Protection Service erfolgt nicht absichtlich. Die von Microsoft Cloud Protection Service unbeabsichtigt erfassten persönlichen Informationen werden von Microsoft nicht verwendet, um Sie zu identifizieren oder zu kontaktieren.

Weitere Informationen finden Sie unter [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).



## <a name="site-hierarchy--geographical-view-with-bing-maps"></a>Standorthierarchie – geografische Ansicht mit Bing Maps

Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Überwachung**, wählen Sie den Knoten **Standorthierarchie** aus, und wechseln Sie zu **Geografische Ansicht**. In dieser Ansicht können Sie von Bing Karten bereitgestellte Karten verwenden, um die physische Configuration Manager-Servertopologie anzuzeigen. Zum Aktivieren dieses Features werden von Ihnen bereitgestellte Standortinformationen von Ihrem Server an den Webdienst Bing Maps übertragen.

Microsoft verwendet die Informationen, um Microsoft Bing Maps sowie andere Websites und Dienste zu betreiben und zu verbessern. Weitere Informationen finden Sie in der [Datenschutzerklärung von Microsoft](https://privacy.microsoft.com/privacystatement).

Sie haben die Wahl, die geografische Ansicht der Standorthierarchie nicht zu verwenden. Die Standardansicht „Hierarchiediagramm“ ermöglicht Ihnen, die Hierarchie anzusehen, ohne den Dienst Bing Karten zu verwenden.