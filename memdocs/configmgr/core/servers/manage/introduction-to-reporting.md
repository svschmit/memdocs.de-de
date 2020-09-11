---
title: Einführung in die Berichterstellung
titleSuffix: Configuration Manager
description: Erfahren Sie mehr zu den Tools und Ressourcen, die Ihnen für die Verwaltung der Berichterstattung in Configuration Manager zur Verfügung stehen.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 230be984-d2cd-4d53-bd7a-bc24dd93fc22
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: bfed31b820ac1f09b240122207b5bf27e432b10a
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607538"
---
# <a name="introduction-to-reporting-in-configuration-manager"></a>Einführung in die Berichterstellung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Zur Berichterstellung in Configuration Manager gehören mehrere Tools und Ressourcen, mit deren Hilfe Sie die erweiterten Berichterstellungsfunktionen der SQL Server Reporting Services (SSRS) und des Power BI-Berichtsservers nutzen können. Beide Berichterstellungsplattformen bieten viele Möglichkeiten, um benutzerdefinierte Berichte zu erstellen. Die Berichterstellung unterstützt Sie beim Sammeln, Sortieren und Darstellen von Informationen zur Integrität von Configuration Manager-Daten in Ihrer Organisation. Configuration Manager stellt viele vordefinierte Berichte in den Reporting Services zur Verfügung, die Sie verwenden können, ohne Änderungen daran vornehmen zu müssen. Sie können die Standardberichte duplizieren und bearbeiten, um Sie an Ihre speziellen Anforderungen anzupassen, oder Sie erstellen selbst benutzerdefinierte Berichte.

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

Die SQL Server Reporting Services bieten eine umfangreiche Palette direkt einsatzbereiter Tools und Dienste, die Sie dabei unterstützen, Berichte für Ihre Organisation zu erstellen, bereitzustellen und zu verwalten. Die Reporting Services bieten außerdem Programmierfeatures, mit denen Sie die Features Ihrer Berichte erweitern und anpassen können. Bei den Reporting Services handelt es sich um eine serverbasierte Berichterstellungsplattform, von der umfassende Berichterstellungsfunktionen für verschiedene Arten von Datenquellen bereitgestellt werden.

Configuration Manager verwendet die SQL Server Reporting Services als Hauptberichterstellungslösung. Die Integration mit Reporting Services bietet die folgenden Vorteile:  

- Verwendet ein Industriestandard-Berichterstattungssystem zum Abfragen der Configuration Manager-Datenbank.  

- Zeigt Berichte mithilfe der Configuration Manager-Berichtsanzeige an oder mithilfe des Berichts-Managers, einer webbasierten Verbindung mit dem Bericht.  

- Bietet hohe Leistung, Verfügbarkeit und Skalierbarkeit.  

- Stellen Abonnements für Berichte zur Verfügung, die Benutzer abonnieren können. Ein Manager könnte beispielsweise einen Bericht abonnieren, den er täglich per E-Mail erhält und in dem der Status der Einführung eines Softwareupdates erläutert wird.

- Exportieren Berichte in verschiedenen häufig genutzten Formaten.  

Weitere Informationen finden Sie unter [Was sind die SQL Server Reporting Services (SSRS)?](/sql/reporting-services/create-deploy-and-manage-mobile-and-paginated-reports).

## <a name="power-bi-report-server"></a>Power BI-Berichtsserver

<!-- 3721603 -->

Sie können den Power BI-Berichtsserver ab der Version 2002 mit der Configuration Manager-Berichterstellung integrieren. So lässt sich die Visualisierung modernisieren und die Leistung verbessern. Durch die Integration werden Power BI-Berichte in der Konsole unterstützt. Dieses Feature ähnelt dem bereits für SQL Server Reporting Services verfügbaren Angebot. Weitere Informationen hierzu finden Sie unter [Integration mit dem Power BI-Berichtsserver](powerbi-report-server.md).

Beim Power BI-Berichtsserver handelt es sich um einen lokalen Berichtsserver mit einem Webportal,in dem Sie Berichte anzeigen und verwalten können. Er beinhaltet Tools für die Erstellung von Power BI-Berichten, paginierten Berichten, Mobilgeräteberichten und KPIs. Weitere Informationen finden Sie unter [Was ist der Power BI-Berichtsserver?](/power-bi/report-server/get-started).

## <a name="reporting-services-point"></a>Reporting Services-Punkt

Der Reporting Services-Punkt ist eine Standortsystemrolle, die Sie auf einem Server hinzufügen, auf dem die Microsoft SQL Server Reporting Services ausgeführt werden. Der Reporting Services-Punkt übernimmt die folgenden Funktionen:

- Kopieren der Configuration Manager-Berichtsdefinitionen in die Reporting Services.
- Erstellen von Berichtsordnern auf Grundlage von Berichtskategorien.
- Festlegen von Sicherheitsrichtlinien für die Berichtsordner und Berichte. Diese Richtlinien basieren auf den rollenbasierten Berechtigungen für Configuration Manager-Administratoren. Der Reporting Services-Punkt stellt in einem 10-Minuten-Intervall eine Verbindung zu den Reporting Services her, um die Sicherheitsrichtlinie neu anzuwenden, wenn Sie sie geändert haben.

Weitere Informationen zum Planen und Installieren eines Reporting Services-Punkts finden Sie in den folgenden Artikeln:

- [Planen der Berichterstattung in Configuration Manager](planning-for-reporting.md)

- [Configure reporting (Konfigurieren der Berichterstellung)](configuring-reporting.md)

## <a name="configuration-manager-reports"></a>Configuration Manager-Berichte

Configuration Manager stellt Berichtsdefinitionen für mehr als 400 Berichte in mehr als 50 Ordnern zur Verfügung. Während der Installation des Reporting Services-Punkts werden diese Definitionen in den Stammberichtsordner in den SQL Server Reporting Services kopiert. Die Berichte werden in der Configuration Manager-Konsole angezeigt und dort anhand der Berichtskategorie in Unterordnern sortiert.

Berichte werden in der Configuration Manager-Hierarchie nicht nach oben oder unten weitergegeben. Sie werden nur für die Datenbank des Standorts ausgeführt, an dem Sie sie erstellt haben. Da in Configuration Manager globale Daten über die gesamte Hierarchie repliziert werden, können Sie in Berichten auf hierarchieweite Informationen zugreifen. Wenn für einen Bericht Daten aus einer Standortdatenbank abgerufen werden, liegen Zugriffsrechte für die Standortdaten von den aktuellen und untergeordneten Standorten sowie für globale Daten aller Standorte in der Hierarchie vor.

Wie bei anderen Configuration Manager-Objekten benötigen Administratoren auch zum Ausführen und Ändern von Berichten die entsprechenden Berechtigungen. Administratoren müssen über die Berechtigung **Bericht ausführen** für das Objekt verfügen, um einen Bericht ausführen zu können. Administratoren müssen über die Berechtigung **Bericht ändern** für das Objekt verfügen, um einen Bericht erstellen oder ändern zu können.

### <a name="create-and-modify-reports"></a>Erstellen und Ändern von Berichten

Für auf den Reporting Services basierende Berichte verwendet Configuration Manager den Berichts-Generator von Microsoft SQL Server Reporting Services sowohl für modellbasierte als auch für SQL-basierte Berichte als ausschließliches Erstellungs- und Bearbeitungstool. Beim Erstellen oder Bearbeiten eines Berichts in der Configuration Manager-Konsole wird der Berichts-Generator geöffnet. Weitere Informationen finden Sie unter [Vorgänge und Wartungstasks für die Berichterstellung](operations-and-maintenance-for-reporting.md).

Ab Version 2002 ist die Konsole mit Power BI Desktop integriert, um Power BI-Berichte zu erstellen oder zu bearbeiten. Weitere Informationen finden Sie unter [Erstellen von Power BI-Berichten](powerbi-report-server.md#create-power-bi-reports).

### <a name="run-reports"></a>Ausführen von Berichten

Wenn Sie einen auf den Reporting Services basierenden Bericht in der Configuration Manager-Konsole ausführen, wird die Berichtsanzeige geöffnet und eine Verbindung mit den Reporting Services hergestellt. Nachdem Sie alle erforderlichen Berichtsparameter angegeben haben, werden die Daten von Reporting Services abgerufen, und das Ergebnis wird im Viewer angezeigt. Sie können auch eine Verbindung mit SQL Services Reporting Services und mit der Datenquelle für den Standort herstellen und dann Berichte ausführen.

Ab Version 2002 wird ein auf Power BI basierter Bericht beim Ausführen in einem Webbrowser geöffnet.

### <a name="report-prompts"></a>Berichtaufforderungen

Sie können eine Eingabeaufforderung für Berichtsparameter oder einen Parameter konfigurieren, wenn Sie einen Bericht erstellen oder ändern. Eingabeaufforderungen für Berichte werden zum Begrenzen oder Auswählen der Zieldaten verwendet, die ein Bericht abruft. Ein Bericht kann auch mehr als eine Eingabeaufforderung enthalten. Achten Sie darauf, dass die Eingabeaufforderungsnamen eindeutig sind und nur alphanumerische Zeichen enthalten, die den SQL Server-Regeln für Bezeichner entsprechen.

Wenn Sie einen Bericht ausführen, fordert die Eingabeaufforderung einen Wert für einen erforderlichen Parameter an. Je nach Wert des Parameters werden die Berichtsdaten abgerufen. Bei der Berichtseingabeaufforderung **Computerinformationen für einen bestimmten Computer** muss beispielsweise der Name eines Computers eingegeben werden. Der angegebene Wert wird von den Reporting Services an eine angegebene Variable weitergegeben, die in der SQL-Anweisung des Berichts definiert ist.

### <a name="report-links"></a>Berichtslinks

Berichtslinks in Configuration Manager werden in einem Quellbericht verwendet, um einfachen Zugriff auf zusätzliche Daten zu bieten. Ein Link kann beispielsweise zu detaillierteren Informationen zu den einzelnen Elementen im Quellbericht führen. Wenn zum Ausführen des Zielberichts eine oder mehrere Aufforderungen erforderlich sind, muss der Quellbericht eine Spalte mit den entsprechenden Werten für jede Aufforderung enthalten.

Der Link muss die Spaltennummer zusammen mit dem Wert für die Eingabeaufforderung angeben. Beispiel:

- Es gibt einen Bericht, der die Computer aufführt, die vom Standort vor Kurzem ermittelt wurden.
- Sie fügen in diesem Link einen Link zu einem anderen Bericht hinzu, in dem die letzten Nachrichten aufgeführt sind, die der Standort für einen bestimmten Computer erhalten hat.
- Sie erstellen den Link und geben an, dass Spalte `2` im Quellbericht den Computername enthält. Dieser Wert ist eine erforderliche Eingabeaufforderung für den Zielbericht.
- Wenn Sie den Quellbericht ausführen, werden Verknüpfungssymbole links neben jeder Datenzeile angezeigt.
- Wenn Sie in einer Zeile auf ein Symbol klicken, wird der Wert in der angegebenen Spalte für diese Zeile der Berichtsanzeige als Eingabeaufforderungswert für den Zielbericht übermittelt.

Sie können nur einen Link für einen Bericht konfigurieren, und dieser Link kann nur zu einem einzelnen Zielbericht führen.

> [!WARNING]  
> Wenn Sie einen Zielbericht in einen anderen Berichtsordner verschieben, ändert sich der Speicherort für den Zielbericht. Configuration Manager aktualisiert den Berichtslink im Quellbericht nicht automatisch mit dem neuen Speicherort, und der Link funktioniert dann im Quellbericht nicht.

## <a name="report-folders"></a>Berichtsordner

Berichtsordner in Configuration Manager bieten eine Methode für das Sortieren und Filtern von Berichten, die in den Reporting Services gespeichert sind. Berichtordner sind nützlich, wenn Sie viele Berichte verwalten müssen. Wenn Sie einen Reporting Services-Punkt installieren, werden Berichte in Reporting Services kopiert und in über 50 Berichtsordnern sortiert. Die Berichtsordner sind schreibgeschützt. Sie können sie in der Configuration Manager-Konsole nicht ändern.

## <a name="report-subscriptions"></a>Berichtsabonnements

Bei einem Berichtsabonnement in den Reporting Services handelt es sich um eine wiederkehrende Anforderung, einen Bericht zu einem bestimmten Zeitpunkt oder als Reaktion auf ein Ereignis zu übermitteln. Sie geben im Abonnement ein Anwendungsdateiformat an. Abonnements sind eine Alternative zum Ausführen eines Berichts bei Bedarf. Bei der Berichterstattung bei Bedarf muss der Bericht immer wieder aktiv ausgewählt werden, um ihn anzeigen zu können. Mit Abonnements ist dagegen die geplante automatische Übermittlung eines Berichts möglich.

Sie können Berichtsabonnements in der Configuration Manager-Konsole verwalten. Der Berichtsserver verarbeitet die Abonnements. Die Abonnements werden mithilfe von Übermittlungserweiterungen verteilt, die auf dem Server bereitgestellt werden. Standardmäßig können Sie Abonnements erstellen, um Berichte in einen freigegebenen Ordner oder an eine E-Mail-Adresse senden zu lassen.

Weitere Informationen finden Sie unter [Verwalten von Berichtsabonnements](operations-and-maintenance-for-reporting.md#bkmk_subscription).

## <a name="report-builder"></a>Report Builder

Für auf den Reporting Services basierende Berichte verwendet Configuration Manager den Berichts-Generator von Microsoft SQL Server Reporting Services sowohl für modellbasierte als auch für SQL-basierte Berichte als ausschließliches Erstellungs- und Bearbeitungstool. Beim Erstellen oder Bearbeiten eines Berichts in der Configuration Manager-Konsole wird der Berichts-Generator geöffnet. Der Berichts-Generator wird automatisch installiert, wenn Sie zum ersten Mal einen Bericht erstellen oder ändern. Die Version von Report Builder, die der installierten Version von SQL Server zugeordnet ist, wird beim Ausführen oder Bearbeiten von Berichten geöffnet.  

 Bei der Installation von Report Builder wird Unterstützung für mehr als 20 Sprachen hinzugefügt. Wenn Sie den Berichts-Generator ausführen, zeigt er Daten in der Sprache an, die der des Betriebssystems des lokalen Computers entspricht. Wenn der Berichts-Generator die Sprache nicht unterstützt, zeigt er die Daten in Englisch an. Von Report Builder wird der gesamte Funktionsumfang der SQL Server Reporting Services unterstützt, darunter die folgenden Funktionen:

- Intuitive Umgebung zum Erstellen von Berichten, die Microsoft 365 Apps ähnelt.  

- Flexibles Berichtslayout der Berichtsdefinitionssprache (RDL) von SQL Server  

- Verschiedene Formen der Datenvisualisierung, darunter Diagramme und Anzeigen  

- Textfelder mit umfassenden Formatierungsmöglichkeiten  

- Exportieren nach Microsoft Word  

Sie können den Berichts-Generator auch direkt in den SQL Server Reporting Services öffnen.

## <a name="report-models-in-sql-server-reporting-services"></a>Berichtsmodelle in SQL Server Reporting Services

Sie werden von den SQL Reporting Services mithilfe von Berichtsmodellen bei der Auswahl von Elementen aus der Configuration Manager-Datenbank unterstützt, die in modellbasierte Berichte eingeschlossen werden sollen. Berichtsmodelle stellen dem Benutzer, der den Bericht erstellt, nur bestimmte Ansichten und Elemente zur Auswahl. Zur Erstellung von modellbasierten Berichten muss mindestens ein Berichtsmodell zur Verfügung stehen.

Berichtsmodelle bieten die folgenden Features:

- Sie weisen Datenbankfeldern und Ansichten logische Geschäftsnamen zu. Sie benötigen keine Kenntnisse der Datenbankstruktur von Configuration Manager, um Berichte erstellen zu können.

- Sie können Elemente logisch gruppieren.  

- Sie können Beziehungen zwischen Elementen definieren.  

- Sie können Modellelemente schützen, sodass Administratoren nur die Daten angezeigt werden, für die sie die Berechtigung zum Anzeigen haben.

Zwar sind in Configuration Manager Beispielmodellberichte enthalten, aber Sie können auch eigene Berichtsmodelle definieren, die Ihre speziellen Unternehmensanforderungen erfüllen. Weitere Informationen zum Erstellen von Berichtsmodellen finden Sie unter [Erstellen benutzerdefinierter Berichtsmodelle für Configuration Manager in SQL Server Reporting Services](creating-custom-report-models-in-sql-server-reporting-services.md).

## <a name="next-steps"></a>Nächste Schritte

[Planen der Berichterstattung in Configuration Manager](planning-for-reporting.md)