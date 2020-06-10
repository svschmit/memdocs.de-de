---
title: Erstellen eines Intune-Berichts aus dem OData-Feed mit Power BI
titleSuffix: Microsoft Intune
description: Erstellen Sie eine Treemap-Visualisierung mithilfe von Power BI Desktop mit einem interaktiven Filter der Intune Data Warehouse-API.
keywords: Intune Data Warehouse
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/29/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: A2C8A336-29D3-47DF-BB4A-62748339391D
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 081d293432e15fccfd2b30d2eb7b7c300789e74f
ms.sourcegitcommit: 1e04fcd0d6c43897cf3993f705d8947cc9be2c25
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/02/2020
ms.locfileid: "84270972"
---
# <a name="create-an-intune-report-from-the-odata-feed-with-power-bi"></a>Erstellen eines Intune-Berichts aus dem OData-Feed mit Power BI

In diesem Artikel wird erläutert, wie Sie eine Treemap-Visualisierung Ihrer Intune-Daten mithilfe von Power BI Desktop mit einem interaktiven Filter erstellen können. Beispielsweise möchte Ihr Finanzdirektor möglicherweise wissen, in welchem Zusammenhang die Verteilung von im Besitz von Unternehmen befindlichen mit persönlichen Geräten steht. Die Treemap gibt einen Überblick über die Gesamtanzahl von Gerätetypen. Sie können die Anzahl von iOS/iPadOS-, Android- und Windows-Geräten prüfen, die weder einem Unternehmen noch einer Privatperson gehören.

## <a name="overview-of-creating-the-chart"></a>Übersicht zum Erstellen des Diagramms

Gehen Sie wie folgt vor, um dieses Diagramm zu erstellen:
1. Falls noch nicht geschehen, installieren Sie Power BI Desktop.
2. Stellen Sie eine Verbindung mit dem Intune Data Warehouse-Datenmodell her, und rufen Sie aktuelle Daten für das Modell ab.
3. Erstellen oder verwalten Sie die Beziehungen des Datenmodells.
4. Erstellen Sie das Diagramm mit Daten aus der **Gerätetabelle**.
5. Erstellen Sie einen interaktiven Filter.
6. Lassen Sie sich das fertige Diagramm anzeigen.

### <a name="a-note-about-tables-and-entities"></a>Hinweis zu Tabellen und Entitäten

In Power BI arbeiten Sie mit Tabellen. Eine Tabelle enthält Datenfelder. Jedes Datenfeld ist einem Datentypen zugeordnet. Das Feld kann nur Daten dieses Datentyps enthalten. Datentypen sind u.a. Nummern, Text oder Datumsangaben. Die Tabellen in Power BI füllen sich mit kürzlich erfassten Daten aus Ihrem Mandanten, wenn Sie das Modell laden. Obwohl sich die spezifischen Daten mit der Zeit ändern, bleibt die Tabellenstruktur solange unverändert, bis das zugrunde liegende Datenmodell aktualisiert worden ist.

Die Verwendung der Begriffe *Entität* und *Tabelle* erscheint Ihnen möglicherweise nicht ganz eindeutig. Sie können über einen OData-Feed (Open Data Protocol) auf das Datenmodell zugreifen. Im Zusammenhang mit OData gelten die Container, die in Power BI als Tabellen bezeichnet werden, als Entitäten. Beide Begriffe beziehen sich auf dasselbe Konzept zum Speichern Ihrer Daten. Weitere Informationen zu OData finden Sie in der [OData-Übersicht](/odata/overview).

## <a name="install-power-bi-desktop"></a>Installieren von Power BI Desktop

Installieren Sie die neueste Version von Power BI Desktop. Sie können Power BI Desktop hier herunterladen: [PowerBI.microsoft.com](https://powerbi.microsoft.com/desktop)

## <a name="connect-to-the-odata-feed-for-the-intune-data-warehouse-for-your-tenant"></a>Stellen Sie eine Verbindung zum OData-Feed für das Intune Data Warehouse für Ihren Mandanten her.

> [!Note]  
> Sie benötigen in Intune eine Berechtigung, um auf **Berichte** zugreifen zu können. Weitere Informationen finden Sie unter [Autorisierung](reports-api-url.md#authorization).

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Berichte** > **Intune Data Warehouse** > **Data Warehouse** aus.
3. Kopieren Sie die benutzerdefinierte Feed-URL. Beispiel: `https://fef.tenant.manage.microsoft.com/ReportingService/DataWarehouseFEService?api-version=v1.0`
4. Öffnen Sie Power BI Desktop.
5. Klicken Sie auf der Menüleiste auf **Datei** > **Daten abrufen** > **OData-Feed**.
6. Fügen Sie die im vorherigen Schritt kopierte benutzerdefinierte Feed-URL in das URL-Feld im Fenster **OData-Feed** ein.
7. Wählen Sie **Basic** aus.

    ![OData-Feed für Intune Data Warehouse für Ihren Mandanten](./media/reports-proc-create-with-odata/reports-create-01-odatafeed.png)

8. Klicken Sie auf **OK**.
9. Wählen Sie **Organisationskonto** aus, und melden Sie sich anschließend mit Ihren Anmeldeinformationen für Intune an.

    ![Anmeldeinformationen für das Organisationskonto](./media/reports-proc-create-with-odata/reports-create-02-org-account.png)

10. Wählen Sie **Verbinden** aus. Der Navigator öffnet sich und zeigt Ihnen eine Liste mit Tabelle im Intune Data Warehouse an.

    ![Screenshot des Navigators mit der Liste der Data Warehouse-Tabellen](./media/reports-proc-create-with-odata/reports-create-02-loadentities.png)

11. Wählen Sie die **Geräte** und die **OwnerTypes**-Tabellen aus.  Wählen Sie **Laden** aus. Power BI lädt die Daten in das Modell.

## <a name="create-a-relationship"></a>Erstellen einer Beziehung

Sie können mehrerer Tabellen importieren, um nicht nur die Daten in einer einzigen Tabelle zu analysieren, sondern auch tabellenübergreifende Daten. In Power BI gibt es eine Funktion namens **Automatische Erkennung**, mit der Sie Beziehungen finden und erstellen können. Die Tabellen im Data Warehouse wurden so konzipiert, dass sie mit der automatischen Erkennungsfunktion in Power BI kompatibel sind. Auch wenn Power BI die Beziehungen nicht automatisch finden sollte, können Sie sie dennoch verwalten.

![Tabellenübergreifendes Verwalten von Beziehungen verwandter Daten](./media/reports-proc-create-with-odata/reports-create-03-managerelationships.png)

1. Wählen Sie **Beziehungen verwalten** aus.
2. Wählen Sie **Automatische Erkennung** aus, wenn Power BI die Beziehungen noch nicht erkannt hat.

Die Beziehung wird von einer „From“-Spalte zu einer „To“-Spalte angezeigt. In diesem Beispiel ist das Datenfeld **ownerTypeKey** in der **Gerätetabelle** mit dem Datenfeld **ownerTypeKey** in der Tabelle **ownerTypes** verknüpft. Sie können die Beziehung verwenden, um den einfachen Namen eines Gerätetypcodes in der Tabelle **Geräte** nachzuschlagen.

## <a name="create-a-treemap-visualization"></a>Erstellen einer Treemap-Visualisierung

In einem Strukturdiagramm werden hierarchische Daten als Felder innerhalb von Feldern angezeigt. Jede Verzweigung der Hierarchie ist ein Feld, das kleinere Felder enthält, die untergeordnete Verzweigungen darstellen. Sie können Power BI Desktop verwenden, um eine Treemap Ihrer Intune-Mandantendaten zu erstellen, die relative Anteile von Geräteherstellertypen anzeigt.

![Power BI-Treemap-Visualisierungen](./media/reports-proc-create-with-odata/reports-create-03-treemap.png)

1. Suchen Sie im Bereich **Visualisierungen** die Option **TreeMap**, und wählen Sie Sie aus. Das **Treemap**-Diagramm wird zu den Berichtszeichenbereichen hinzugefügt.
2. Suchen Sie im Bereich **Felder** nach der `devices`-Tabelle.
3. Erweitern Sie die `devices`-Tabelle, und klicken Sie auf das Datenfeld `manufacturer`.
4. Ziehen Sie das Datenfeld `manufacturer` in den Berichtszeichenbereich, und legen Sie es im **Treemap**-Diagramm ab.
5. Ziehen Sie das Datenfeld `deviceKey` aus der `devices`-Tabelle in den Bereich **Visualisierungen**, und legen Sie es im Abschnitt **Werte** auf dem Feld mit der Bezeichnung **Hier Datenfelder hinzufügen** ab.  

Jetzt verfügen Sie über eine Visualisierung der Verteilung von Herstellern und Geräten innerhalb Ihrer Organisation.

![Treemap mit Daten: Verteilung der Gerätehersteller](./media/reports-proc-create-with-odata/reports-create-06-treemapwdata.png)

## <a name="add-a-filter"></a>Hinzufügen eines Filters

Sie können Ihrer Treemap einen Filter hinzufügen, damit Sie mithilfe Ihrer App zusätzliche Fragen beantworten können.

1. Um einen Filter hinzuzufügen, wählen Sie zunächst die Berichtscanvas aus, und klicken Sie anschließend unter **Visualisierungen** auf das **Slicer-Symbol** (![Treemap mit Datenmodell und unterstützten Beziehungen](./media/reports-proc-create-with-odata/reports-create-slicer.png)). Die leere **Slicervisualisierung** wird in der Canvas angezeigt.
2. Suchen Sie im Bereich **Felder** nach der `ownerTypes`-Tabelle.
3. Erweitern Sie die `ownerTypes`-Tabelle, und klicken Sie auf das Datenfeld `ownerTypeName`.
4. Ziehen Sie das Datenfeld `onwerTypeName` aus der `ownerTypes`-Tabelle in den Bereich **Filter**, und legen Sie es im Abschnitt **Filter für diese Seite** auf dem Feld mit der Bezeichnung **Hier Datenfelder hinzufügen** ab.  

   In der `OwnerTypes`-Tabelle gibt es ein Datenfeld namens `OwnerTypeKey`, das Daten enthält, die darauf hinweisen, ob ein Gerät Eigentum eines Unternehmens oder einer Privatperson ist. Da Sie Anzeigenamen in diesem Filter anzeigen möchten, suchen Sie nach der Tabelle `ownerTypes`, und ziehen Sie den **ownerTypeName** auf den Slicer. Das folgende Beispiel zeigt, wie das Datenmodell Beziehungen zwischen den Tabellen unterstützt.

![Treemap mit Filter: Unterstützung von Beziehungen zwischen Tabellen](./media/reports-proc-create-with-odata/reports-create-08_ownertype.png)

Nun verfügen Sie über einen interaktiven Filter, der zum Wechseln zwischen unternehmenseigenen und privaten Geräten verwendet werden kann. Mit diesem Filter können Sie Veränderungen in der Verteilung nachvollziehen.

1. Klicken Sie innerhalb des Slicers auf **Unternehmen**, um die Verteilung der unternehmenseigenen Geräte anzuzeigen.
2. Klicken Sie innerhalb des Slicers auf **Persönlich**, um die privaten Geräte anzuzeigen.

## <a name="next-steps"></a>Nächste Schritte

- Erfahren Sie mehr über das [Erstellen und Verwalten von Beziehungen](https://powerbi.microsoft.com/documentation/powerbi-desktop-create-and-manage-relationships/) in Power BI Desktop in der Power BI-Dokumentation.
- Lesen Sie den Artikel [Datenmodell von Intune Data Warehouse](reports-ref-data-model.md).
