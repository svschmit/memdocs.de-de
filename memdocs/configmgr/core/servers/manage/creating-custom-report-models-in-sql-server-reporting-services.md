---
title: Erstellen benutzerdefinierter Berichte
titleSuffix: Configuration Manager
description: Definieren Sie Berichtsmodelle, um Ihre Geschäftsanforderungen zu erfüllen, und stellen Sie die Berichtsmodelle anschließend in Configuration Manager bereit.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f2df88b4-c348-4dcf-854a-54fd6eedf485
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 590f3adec168fe6d7f4718505bd6f7d6b9f7c25f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692728"
---
# <a name="creating-custom-report-models-for-configuration-manager-in-sql-server-reporting-services"></a>Erstellen benutzerdefinierter Berichtsmodelle für Configuration Manager in SQL Server Reporting Services

*Gilt für: Configuration Manager (Current Branch)*

In Configuration Manager sind Beispielberichtsmodelle enthalten. Sie können aber auch Berichtsmodelle definieren, die Ihren eigenen Geschäftsanforderungen entsprechen, und diese anschließend zur Verwendung beim Erstellen neuer modellbasierter Berichte in Configuration Manager bereitstellen. In der folgenden Tabelle sind die Schritte zum Erstellen und Bereitstellen eines grundlegenden Berichtsmodells aufgelistet.  

> [!NOTE]  
>  Die Schritte zum Erstellen erweiterter Berichtsmodelle finden Sie im Abschnitt [Schritte zum Erstellen eines erweiterten Berichtsmodells in SQL Server Reporting Services](#AdvancedReportModel) in diesem Thema.  

|Schritt|Beschreibung|Weitere Informationen|  
|----------|-----------------|----------------------|  
|Überprüfen, ob SQL Server Business Intelligence Development Studio installiert ist|Berichtsmodelle werden mithilfe von SQL Server Business Intelligence Development Studio entworfen und erstellt. Überprüfen Sie, ob auf dem Computer, auf dem Sie das benutzerdefinierte Berichtsmodell erstellen, SQL Server Business Intelligence Development Studio installiert ist.|Weitere Informationen zu SQL Server Business Intelligence Development Studio finden Sie in der Dokumentation zu SQL Server 2008.|  
|Erstellen eines Berichtsmodellprojekts|Ein Berichtsmodellprojekt enthält die Definition der Datenquelle (eine DS-Datei), die Definition der Datenquellensicht (eine DSV-Datei) und das Berichtsmodell (eine SMDL-Datei).|Weitere Informationen finden Sie im Abschnitt [So erstellen Sie das Berichtsmodellprojekt](#BKMK_CreateReportModelProject) in diesem Thema.|  
|Definieren einer Datenquelle für ein Berichtsmodell|Nach dem Erstellen eines Berichtsmodellprojekts müssen Sie eine Datenquelle festlegen, aus der Sie die Unternehmensdaten extrahieren. Das ist normalerweise die Configuration Manager-Standortdatenbank.|Weitere Informationen finden Sie im Abschnitt [So legen Sie die Datenquelle für das Berichtsmodell fest](#BKMK_DefineReportModelDataSource) in diesem Thema.|  
|Definieren einer Datenquellensicht für ein Berichtsmodell|Nach der Definition der Datenquellen, die Sie in Ihrem Berichtsmodellprojekt verwenden werden, definieren Sie im nächsten Schritt eine Datenquellensicht für das Projekt. Eine Datenquellensicht ist ein logisches Datenmodell, das auf mindestens einer Datenquelle basiert. Datenquellensichten schließen den Zugriff auf physische Objekte wie Tabellen und Ansichten ein, die in den zugrundeliegenden Datenquellen enthalten sind. SQL Server Reporting Services generiert das Berichtsmodell aus der Datenquellensicht.<br /><br /> Datenquellensichten vereinfachen den Modellentwurfsvorgang, weil sie Ihnen eine nützliche Darstellung der Daten bereitstellen, die Sie angegeben haben. Sie können in einer Datenquellensicht Tabellen und Felder umbenennen sowie aggregierte Felder und abgeleitete Tabellen hinzufügen, ohne die zugrundeliegende Datenquelle ändern zu müssen. Fügen Sie der Datenquellensicht für ein effizientes Modell nur die Tabellen hinzu, die Sie verwenden möchten.|Weitere Informationen finden Sie im Abschnitt [So legen Sie die Datenquellensicht für das Berichtsmodell fest](#BKMK_DefineReportModelDataSourceView) in diesem Thema.|  
|Erstellen eines Berichtsmodells|Ein Berichtsmodell ist eine Schicht über einer Datenbank, die Geschäftseinheiten, Felder und Rollen identifiziert. Nach dem Veröffentlichen können Benutzer von Report Builder mithilfe dieser Modelle Berichte entwickeln, ohne mit den Datenbankstrukturen vertraut zu sein oder Abfragen verstehen und schreiben zu müssen. Modelle bestehen aus Sätzen verwandter Berichtselemente, die einschließlich vordefinierter Beziehungen zwischen diesen Geschäftselementen und einschließlich vordefinierter Kalkulationen unter einem Anzeigenamen gruppiert werden. Modelle werden mithilfe der XML-Sprache SMDL (Semantic Model Definition Language) definiert. Die Dateinamenerweiterung für Berichtsmodelldateien ist „smdl“.|Weitere Informationen finden Sie im Abschnitt [So erstellen Sie das Berichtsmodell](#BKMK_CreateReportModel) in diesem Thema.|  
|Veröffentlichen eines Berichtsmodells|Zum Aufbauen eines Berichts mithilfe des soeben erstellten Modells müssen Sie das Modell auf einem Berichtsserver veröffentlichen. Die Datenquelle und die Datenquellensicht werden in das Modell eingeschlossen, wenn es veröffentlicht wird.|Weitere Informationen finden Sie im Abschnitt [So veröffentlichen Sie das Berichtsmodell (zur Verwendung in SQL Server Reporting Services)](#BKMK_PublishReportModel) in diesem Thema.|  
|Bereitstellen des Berichtsmodells in Configuration Manager|Bevor Sie mithilfe des **Assistenten zum Erstellen von Berichten** einen modellbasierten Bericht auf der Basis eines benutzerdefinierten Berichtsmodells erstellen können, müssen Sie das Berichtsmodell in Configuration Manager bereitstellen.|Weitere Informationen finden Sie im Abschnitt [So stellen Sie das benutzerdefinierte Berichtsmodell in Configuration Manager bereit](#BKMK_DeployReportModel) in diesem Thema.|  

## <a name="steps-for-creating-a-basic-report-model-in-sql-server-reporting-services"></a>Schritte zum Erstellen eines grundlegenden Berichtsmodells in SQL Server Reporting Services  
 Mithilfe der folgenden Verfahren können Sie ein grundlegendes Berichtsmodell erstellen, das Benutzern an Ihrem Standort die Ausführung bestimmter modellbasierter Berichte auf der Basis von Daten in einer einzigen Ansicht der Configuration Manager-Datenbank erlaubt. Das von Ihnen erstellte Berichtsmodell gibt dem Berichtsautor Aufschluss über die Clientcomputer an Ihrem Standort. Die entsprechenden Informationen werden der Ansicht **v_R_System** in der Configuration Manager-Datenbank entnommen.  

 Stellen Sie auf dem Computer, auf dem das Verfahren ausgeführt werden soll, sicher, dass SQL Server Business Intelligence Development Studio installiert ist und dass der Computer über eine Netzwerkverbindung zum Reporting Services-Punktserver verfügt. Ausführlichere Informationen zu SQL Server Business Intelligence Development Studio finden Sie in der Dokumentation zu SQL Server 2008.  

###  <a name="to-create-the-report-model-project"></a><a name="BKMK_CreateReportModelProject"></a> So erstellen Sie das Berichtsmodell  

1.  Klicken Sie auf dem Desktop im **Startmenü**auf **Microsoft SQL Server 2008**, und klicken Sie dann auf **SQL Server Business Intelligence Development Studio**.  

2.  Wenn **SQL Server Business Intelligence Development Studio** in Microsoft Visual Studio geöffnet wurde, klicken Sie auf **Datei**, dann auf **Neu**und anschließend auf **Projekt**.  

3.  Wählen Sie im Dialogfeld **Neues Projekt** die Option **Berichtsmodellprojekt** aus der Liste **Vorlagen** aus.  

4.  Geben Sie im Feld **Name** einen Namen für dieses Berichtsmodell an. Geben Sie für dieses Beispiel **Einfaches_Modell**ein.  

5.  Zum Erstellen des Berichtsmodellprojekts klicken Sie auf **OK**.  

6.  Die Lösung **Einfaches_Modell** wird im **Projektmappen-Explorer**angezeigt.  

    > [!NOTE]  
    >  Wenn der Bereich **Projektmappen-Explorer** nicht angezeigt wird, klicken Sie auf **Anzeigen**und anschließend auf **Projektmappen-Explorer**.  

###  <a name="to-define-the-data-source-for-the-report-model"></a><a name="BKMK_DefineReportModelDataSource"></a> So legen Sie die Datenquelle für das Berichtsmodell fest  

1.  Klicken Sie im Bereich **Projektmappen-Explorer** von **SQL Server Business Intelligence Development Studio**mit der rechten Maustaste auf **Datenquellen** , um **Neue Datenquelle hinzufügen**auszuwählen.  

2.  Klicken Sie auf der Seite **Willkommen** des Datenquellen-Assistenten auf **Weiter**.  

3.  Vergewissern Sie sich auf der Seite **Wählen Sie aus, wie die Verbindung definiert werden soll** , dass die Option **Eine Datenquelle basierend auf einer vorhandenen oder neuen Verbindung erstellen** aktiviert ist, und klicken Sie dann auf **Neu**.  

4.  Geben Sie im Dialogfeld **Verbindungs-Manager** die folgenden Verbindungseigenschaften für die Datenquelle an:  

    -   **Servername:** Geben Sie den Namen Ihres Configuration Manager-Standortdatenbankservers ein, oder wählen Sie ihn aus der Liste aus. Wenn Sie mit einer benannten Instanz statt mit der Standardinstanz arbeiten, geben Sie &lt;*Datenbankserver*>\\&lt;*Instanzname*> ein.  

    -   Aktivieren Sie **Windows-Authentifizierung verwenden**.  

    -   Wählen Sie aus der Liste **Datenbanknamen eingeben oder auswählen** den Namen Ihrer Configuration Manager-Standortdatenbank aus.  

5.  Klicken Sie auf **Verbindung testen**, um die Datenverbindung zu prüfen.  

6.  Bei erfolgreicher Verbindung klicken Sie auf **OK** , um das Dialogfeld **Verbindungs-Manager** zu schließen. Andernfalls vergewissern Sie sich, dass die von Ihnen eingegebenen Informationen korrekt sind, und klicken Sie dann erneut auf **Testverbindung** .  

7.  Vergewissern Sie sich, dass auf der Seite **Wählen Sie aus, wie die Verbindung definiert werden soll** die Option **Eine Datenquelle basierend auf einer vorhandenen oder neuen Verbindung erstellen** aktiviert ist. Stellen Sie sicher, dass die soeben von Ihnen angegebene Datenquelle unter **Datenverbindungen**ausgewählt ist, und klicken Sie dann auf **Weiter**.  

8.  Geben Sie unter **Datenquellenname**einen Namen für die Datenquelle an, und klicken Sie dann auf **Fertig stellen**. Geben Sie für dieses Beispiel **Einfaches_Modell**ein.  

9. Die Datenquelle **Einfaches_Modell.ds** wird jetzt im **Projektmappen-Explorer** unter **Datenquellen** angezeigt.  

    > [!NOTE]  
    >  Zum Bearbeiten der Eigenschaften einer vorhandenen Datenquelle doppelklicken Sie auf die Datenquelle im Ordner **Datenquellen** im Bereich **Projektmappen-Explorer** , um die Datenquelleneigenschaften im Datenquellen-Designer anzuzeigen.  

###  <a name="to-define-the-data-source-view-for-the-report-model"></a><a name="BKMK_DefineReportModelDataSourceView"></a> So legen Sie die Datenquellensicht für das Berichtsmodell fest  

1.  Klicken Sie im Bereich **Projektmappen-Explorer**mit der rechten Maustaste auf **Datenquellensichten** , um **Neue Datenquellensicht hinzufügen**auszuwählen.  

2.  Klicken Sie auf der Seite **Willkommen beim Datenquellensicht-Assistenten** auf **Weiter**. Die Seite **Datenquelle auswählen** wird angezeigt.  

3.  Vergewissern Sie sich, dass im Fenster **Relationale Datenquellen** die Datenquelle **Einfaches_Modell** ausgewählt ist, und klicken Sie dann auf **Weiter**.  

4.  Wählen Sie auf der Seite **Tabellen und Sichten auswählen** in der Liste **Verfügbare Objekte** die folgende Ansicht für das Berichtsmodell aus: **v_R_System (dbo)** .  

    > [!TIP]  
    >  Zum Suchen von Ansichten in der Liste **Verfügbare Objekte** klicken Sie auf die Überschrift **Name** im Listenkopf. Dadurch werden die Objekte in alphabetischer Reihenfolge sortiert.  

5.  Klicken Sie nach Auswahl der Ansicht auf den Pfeil nach rechts **>** , um das Objekt in die Liste **Eingeschlossene Objekte** aus.  

6.  Wenn die Seite **Namensübereinstimmung** angezeigt wird, übernehmen Sie die Standardoptionen, und klicken Sie dann auf **Weiter**.  

7.  Wenn Sie die gewünschten Objekte ausgewählt haben, klicken Sie auf **Weiter**, und geben Sie dann einen Namen für die Datenquellensicht an. Geben Sie für dieses Beispiel **Einfaches_Modell**ein.  

8.  Klicken Sie auf **Fertig stellen**. Die Datenquellensicht **Einfaches_Modell.dsv** wird im Ordner **Datenquellensichten** des **Projektmappen-Explorers**angezeigt.  

###  <a name="to-create-the-report-model"></a><a name="BKMK_CreateReportModel"></a> To create the report model  

1.  Klicken Sie im **Projektmappen-Explorer**mit der rechten Maustaste auf **Berichtsmodelle** , um **Neues Berichtsmodell hinzufügen**auszuwählen.  

2.  Klicken Sie auf der Seite **Willkommen** des Berichtsmodell-Assistenten auf **Weiter**.  

3.  Wählen Sie auf der Seite **Datenquellensichten auswählen** in der Liste **Verfügbare Datenquellensichten** die Datenquellensicht aus, und klicken Sie dann auf **Weiter**. Wählen Sie für dieses Beispiel **Einfaches_Modell.dsv**aus.  

4.  Übernehmen Sie auf der Seite **Regeln zur Berichtsmodellgenerierung auswählen** die Standardwerte, und klicken Sie dann auf **Weiter**.  

5.  Vergewissern Sie sich auf der Seite **Modellstatistiken sammeln** , dass die Option **Modellstatistiken vor Generierung aktualisieren** aktiviert ist, und klicken Sie dann auf **Weiter**.  

6.  Geben Sie auf der Seite **Assistenten abschließen** einen Namen für das Berichtsmodell an. Für dieses Beispiel muss **Einfaches_Modell** angezeigt sein.  

7.  Klicken Sie auf **Ausführen**, um den Assistenten abzuschließen und das Berichtsmodell zu erstellen.  

8.  Zum Beenden des Assistenten klicken Sie auf **Fertig stellen**. Das Berichtsmodell wird im Entwurfsfenster angezeigt.  

###  <a name="to-publish-the-report-model-for-use-in-sql-server-reporting-services"></a><a name="BKMK_PublishReportModel"></a> So veröffentlichen Sie das Berichtsmodell (zur Verwendung in SQL Server Reporting Services)  

1.  Klicken Sie im **Projektmappen-Explorer**mit der rechten Maustaste auf das Berichtsmodell, um **Bereitstellen**auszuwählen. In diesem Beispiel wird das Berichtsmodell **Einfaches_Modell.smdl**verwendet.  

2.  Unten links im Fenster **SQL Server Business Intelligence Development Studio** wird der Bereitstellungsstatus angezeigt. Wenn die Bereitstellung abgeschlossen ist, wird die Meldung **Bereitstellen erfolgreich** angezeigt. Falls bei der Bereitstellung ein Fehler aufgetreten ist, wird die Ursache im Fenster **Ausgabe** angezeigt. Das neue Berichtsmodell steht nun auf Ihrer SQL Server Reporting Services-Website zur Verfügung.  

3.  Klicken Sie auf **Datei**und dann auf **Alle speichern**, und beenden Sie danach **SQL Server Business Intelligence Development Studio**.  

###  <a name="to-deploy-the-custom-report-model-to-configuration-manager"></a><a name="BKMK_DeployReportModel"></a> To deploy the custom report model to Configuration Manager  

1. Suchen Sie den Ordner, in dem Sie das Berichtsmodellprojekt erstellt haben. Beispiel: %*USERPROFILE*%\Documents\Visual Studio 2008\Projects\\ *&lt;Projektname\>.*  

2. Kopieren Sie die folgenden Dateien aus dem Projektordner für das Berichtsmodell in einen temporären Ordner auf Ihrem Computer.  

   -   *&lt;Modellname\>* **.dsv**  

   -   *&lt;Modellname\>* **.smdl**  

3. Öffnen Sie die oben aufgeführten Dateien mit einem Text-Editor, z. B. Notepad.  

4. Suchen Sie in der Datei _&lt;Modellname\>_ **.dsv** die erste Zeile, die wie folgt lautet:  

    `<DataSourceView xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">`

    Bearbeiten Sie diese Zeile, sodass sie wie folgt lautet:  

    `<DataSourceView xmlns="<https://schemas.microsoft.com/analysisservices/2003/engine>" xmlns:xsi="RelationalDataSourceView">`  

5. Kopieren Sie den gesamten Inhalt der Datei in die Windows-Zwischenablage.  

6. Schließen Sie die Datei _&lt;Modellname\>_ **.dsv**.  

7. Suchen Sie in der Datei _&lt;Modellname\>_ **.smdl** die letzten drei Zeilen der Datei, die wie folgt lauten:  

    `</Entity>`  

    `</Entities>`  

    `</SemanticModel>`  

8. Fügen Sie den Inhalt der Datei _&lt;Modellname\>_ **.dsv** direkt vor der letzten Zeile der Datei ein ( **&lt;SemanticModel\>** ).  

9. Speichern und schließen Sie die Datei _&lt;Modellname\>_ **.smdl**.  

10. Kopieren Sie die Datei _&lt;Modellname\>_ **.smdl** in den Ordner „ *%programfiles%* \Microsoft Configuration Manager \AdminConsole\XmlStorage\Other“ auf dem Configuration Manager-Standortserver.  

    > [!IMPORTANT]  
    >  Nach dem Kopieren der Berichtsmodelldatei auf den Configuration Manager-Standortserver müssen Sie die Configuration Manager-Konsole beenden und neu starten, um das Berichtsmodell im **Assistenten zum Erstellen von Berichten** verwenden zu können.  

##  <a name="steps-for-creating-an-advanced-report-model-in-sql-server-reporting-services"></a><a name="AdvancedReportModel"></a> Schritte zum Erstellen eines erweiterten Berichtsmodells in SQL Server Reporting Services  
 Mithilfe der folgenden Verfahren können Sie ein erweitertes Berichtsmodell erstellen, das Benutzern an Ihrem Standort die Ausführung bestimmter modellbasierter Berichte auf der Basis von Daten in mehreren Ansichten der Configuration Manager-Datenbank erlaubt. Das von Ihnen erstellte Berichtsmodell gibt dem Berichtsautor Aufschluss über die Clientcomputer und die auf diesen installierten Betriebssysteme. Die entsprechenden Informationen werden den folgenden Ansichten der Configuration Manager-Datenbank entnommen:  

- **V_R_System:** Diese Ansicht enthält Informationen zu den ermittelten Computern und zum Configuration Manager-Client.  

- **V_GS_OPERATING_SYSTEM:** Diese Ansicht enthält Informationen zum auf dem Clientcomputer installierten Betriebssystem.  

  Die in den vorherigen Ansichten ausgewählten Elemente werden in einer Liste zusammengefasst, umbenannt und können anschließend vom Berichtsautor im Berichts-Generator aufgerufen sowie für bestimmte Berichte verwendet werden.  

  Stellen Sie auf dem Computer, auf dem das Verfahren ausgeführt werden soll, sicher, dass SQL Server Business Intelligence Development Studio installiert ist und dass der Computer über eine Netzwerkverbindung zum Reporting Services-Punktserver verfügt. Ausführlichere Informationen zu SQL Server Business Intelligence Development Studio finden Sie in der Dokumentation zu SQL Server.  

#### <a name="to-create-the-report-model-project"></a>To create the report model project  

1.  Klicken Sie auf dem Desktop im **Startmenü**auf **Microsoft SQL Server 2008**, und klicken Sie dann auf **SQL Server Business Intelligence Development Studio**.  

2.  Wenn **SQL Server Business Intelligence Development Studio** in Microsoft Visual Studio geöffnet wurde, klicken Sie auf **Datei**, dann auf **Neu**und anschließend auf **Projekt**.  

3.  Wählen Sie im Dialogfeld **Neues Projekt** die Option **Berichtsmodellprojekt** aus der Liste **Vorlagen** aus.  

4.  Geben Sie im Feld **Name** einen Namen für dieses Berichtsmodell an. Geben Sie für dieses Beispiel **Erweitertes_Modell**ein.  

5.  Zum Erstellen des Berichtsmodellprojekts klicken Sie auf **OK**.  

6.  Die Lösung **Erweitertes_Modell** wird im **Projektmappen-Explorer**angezeigt.  

    > [!NOTE]  
    >  Wenn der Bereich **Projektmappen-Explorer** nicht angezeigt wird, klicken Sie auf **Anzeigen**und anschließend auf **Projektmappen-Explorer**.  

#### <a name="to-define-the-data-source-for-the-report-model"></a>So legen Sie die Datenquelle für das Berichtsmodell fest  

1.  Klicken Sie im Bereich **Projektmappen-Explorer** von **SQL Server Business Intelligence Development Studio**mit der rechten Maustaste auf **Datenquellen** , um **Neue Datenquelle hinzufügen**auszuwählen.  

2.  Klicken Sie auf der Seite **Willkommen** des Datenquellen-Assistenten auf **Weiter**.  

3.  Vergewissern Sie sich auf der Seite **Wählen Sie aus, wie die Verbindung definiert werden soll** , dass die Option **Eine Datenquelle basierend auf einer vorhandenen oder neuen Verbindung erstellen** aktiviert ist, und klicken Sie dann auf **Neu**.  

4.  Geben Sie im Dialogfeld **Verbindungs-Manager** die folgenden Verbindungseigenschaften für die Datenquelle an:  

    -   **Servername:** Geben Sie den Namen Ihres Configuration Manager-Standortdatenbankservers ein, oder wählen Sie ihn aus der Liste aus. Wenn Sie mit einer benannten Instanz statt mit der Standardinstanz arbeiten, geben Sie &lt;*Datenbankserver*>\\&lt;*Instanzname*> ein.  

    -   Aktivieren Sie **Windows-Authentifizierung verwenden**.  

    -   Wählen Sie aus der Liste **Datenbanknamen eingeben oder auswählen** den Namen Ihrer Configuration Manager-Standortdatenbank aus.  

5.  Klicken Sie auf **Verbindung testen**, um die Datenverbindung zu prüfen.  

6.  Bei erfolgreicher Verbindung klicken Sie auf **OK** , um das Dialogfeld **Verbindungs-Manager** zu schließen. Andernfalls vergewissern Sie sich, dass die von Ihnen eingegebenen Informationen korrekt sind, und klicken Sie dann erneut auf **Testverbindung** .  

7.  Vergewissern Sie sich auf der Seite **Wählen Sie aus, wie die Verbindung definiert werden soll** , dass die Option **Eine Datenquelle basierend auf einer vorhandenen oder neuen Verbindung erstellen** aktiviert ist. Stellen Sie sicher, dass die soeben von Ihnen angegebene Datenquelle im Listenfeld **Datenverbindungen** ausgewählt ist, und klicken Sie dann auf **Weiter**.  

8.  Geben Sie unter **Datenquellenname**einen Namen für die Datenquelle an, und klicken Sie dann auf **Fertig stellen**. Geben Sie für dieses Beispiel **Erweitertes_Modell**ein.  

9. Die Datenquelle **Erweitertes_Modell.ds** wird jetzt im **Projektmappen-Explorer** unter dem Knoten **Datenquellen** angezeigt.  

    > [!NOTE]  
    >  Zum Bearbeiten der Eigenschaften einer vorhandenen Datenquelle doppelklicken Sie auf die Datenquelle im Ordner **Datenquellen** im Bereich **Projektmappen-Explorer** , um die Datenquelleneigenschaften im Datenquellen-Designer anzuzeigen.  

#### <a name="to-define-the-data-source-view-for-the-report-model"></a>So legen Sie die Datenquellensicht für das Berichtsmodell fest  

1. Klicken Sie im Bereich **Projektmappen-Explorer**mit der rechten Maustaste auf **Datenquellensichten** , um **Neue Datenquellensicht hinzufügen**auszuwählen.  

2. Klicken Sie auf der Seite **Willkommen beim Datenquellensicht-Assistenten** auf **Weiter**. Die Seite **Datenquelle auswählen** wird angezeigt.  

3. Vergewissern Sie sich, dass im Fenster **Relationale Datenquellen** die Datenquelle **Erweitertes_Modell** ausgewählt ist, und klicken Sie dann auf **Weiter**.  

4. Wählen Sie auf der Seite **Tabellen und Sichten auswählen** in der Liste **Verfügbare Objekte** die folgenden Ansichten für das Berichtsmodell aus:  

   - **v_R_System (dbo)**  

   - **v_GS_OPERATING_SYSTEM (dbo)**  

     Klicken Sie nach Auswahl einer Ansicht jeweils auf den Pfeil nach rechts **>** , um das Objekt in die Liste **Eingeschlossene Objekte** aus.  

   > [!TIP]  
   >  Zum Suchen von Ansichten in der Liste **Verfügbare Objekte** klicken Sie auf die Überschrift **Name** im Listenkopf. Dadurch werden die Objekte in alphabetischer Reihenfolge sortiert.  

5. Wenn das Dialogfeld **Namensübereinstimmung** angezeigt wird, übernehmen Sie die Standardoptionen, und klicken Sie dann auf **Weiter**.  

6. Wenn Sie die gewünschten Objekte ausgewählt haben, klicken Sie auf **Weiter**, und geben Sie dann einen Namen für die Datenquellensicht an. Geben Sie für dieses Beispiel **Erweitertes_Modell**ein.  

7. Klicken Sie auf **Fertig stellen**. Die Datenquellensicht **Erweitertes_Modell.dsv** wird im Ordner **Datenquellensichten** des **Projektmappen-Explorers**angezeigt.  

#### <a name="to-define-relationships-in-the-data-source-view"></a>So legen Sie die Beziehungen in der Datenquellensicht fest  

1.  Doppelklicken Sie im **Projektmappen-Explorer**auf **Erweitertes_Modell.dsv** , um das Entwurfsfenster zu öffnen.  

2.  Klicken Sie mit der rechten Maustaste auf die Titelleiste des Fensters **v_R_System** , um **Tabelle ersetzen**auszuwählen, und klicken Sie dann auf **Durch neue benannte Abfrage**.  

3.  Klicken Sie im Dialogfeld **Benannte Abfrage erstellen** auf das Symbol **Tabelle hinzufügen** (in der Regel das letzte Symbol im Menüband).  

4.  Klicken Sie im Dialogfeld **Tabelle hinzufügen** auf die Registerkarte **Sichten** , wählen Sie **V_GS_OPERATING_SYSTEM** in der Liste aus, und klicken Sie dann auf **Hinzufügen**.  

5.  Klicken Sie auf **Schließen** , um das Dialogfeld **Tabelle hinzufügen** zu schließen.  

6.  Geben Sie im Dialogfeld **Benannte Abfrage erstellen** die folgenden Informationen ein:  

    -   **Name:** Geben Sie hier den Namen für die Abfrage an. Geben Sie für dieses Beispiel **Erweitertes_Modell**ein.  

    -   **Beschreibung:** Geben Sie hier eine Beschreibung für die Abfrage an. Geben Sie für dieses Beispiel **Beispiel eines Reporting Services-Berichtsmodells**.  

7.  Wählen Sie im Fenster **v_R_System** in der Liste der Objekte die folgenden Elemente aus, die im Berichtsmodell enthalten sein sollen:  

    -   **ResourceID**  

    -   **ResourceType**  

    -   **Active0**  

    -   **AD_Domain_Name0**  

    -   **AD_SiteName0**  

    -   **Client0**  

    -   **Client_Type0**  

    -   **Client_Version0**  

    -   **CPUType0**  

    -   **Hardware_ID0**  

    -   **User_Domain0**  

    -   **User_Name0**  

    -   **Netbios_Name0**  

    -   **Operating_System_Name_and0**  

8.  Wählen Sie im Feld **v_GS_OPERATING_SYSTEM** in der Liste der Objekte die folgenden Elemente aus, die im Berichtsmodell enthalten sein sollen:  

    -   **ResourceID**  

    -   **Caption0**  

    -   **CountryCode0**  

    -   **CSDVersion0**  

    -   **Description0**  

    -   **InstallDate0**  

    -   **LastBootUpTime0**  

    -   **Locale0**  

    -   **Manufacturer0**  

    -   **Version0**  

    -   **WindowsDirectory0**  

9. Damit die Objekte in diesen Ansichten als Liste zusammengefasst werden, müssen Sie eine Beziehung zwischen den beiden Tabellen bzw. Ansichten mithilfe einer Verknüpfung angeben. Sie können die beiden Ansichten mithilfe des Objekts **ResourceID**verknüpfen, das in beiden Ansichten angezeigt wird.  

10. Klicken Sie im Fenster **v_R_System** auf das Objekt **ResourceID** , und ziehen Sie es auf das Objekt **ResourceID** im Fenster **v_GS_OPERATING_SYSTEM** .  

11. Klicken Sie auf **OK**.  

12. Das Fenster **Erweitertes_Modell** ersetzt das Fenster **v_R_System** und umfasst alle Objekte aus den Ansichten **v_R_System** sowie **v_GS_OPERATING_SYSTEM** , die für das Berichtsmodell erforderlich sind. Das Fenster **v_GS_OPERATING_SYSTEM** kann jetzt aus dem Datenquellensicht-Designer gelöscht werden. Klicken Sie mit der rechten Maustaste auf die Titelleiste des Fensters **v_GS_OPERATING_SYSTEM** , um **Tabelle aus Datenquellensicht löschen**auszuwählen. Klicken Sie zur Bestätigung des Löschens im Dialogfeld **Objekte löschen** auf **OK** .  

13. Klicken Sie auf **Datei**und dann auf **Alle speichern**.  

#### <a name="to-create-the-report-model"></a>To create the report model  

1.  Klicken Sie im **Projektmappen-Explorer**mit der rechten Maustaste auf **Berichtsmodelle** , um **Neues Berichtsmodell hinzufügen**auszuwählen.  

2.  Klicken Sie auf der Seite **Willkommen** des Berichtsmodell-Assistenten auf **Weiter**.  

3.  Wählen Sie auf der Seite **Datenquellensicht auswählen** in der Liste **Verfügbare Datenquellensichten** die Datenquellensicht aus, und klicken Sie dann auf **Weiter**. Wählen Sie für dieses Beispiel **Einfaches_Modell.dsv**aus.  

4.  Übernehmen Sie auf der Seite **Regeln zur Berichtsmodellgenerierung auswählen** die Standardwerte, und klicken Sie dann auf **Weiter**.  

5.  Vergewissern Sie sich auf der Seite **Modellstatistiken sammeln** , dass die Option **Modellstatistiken vor Generierung aktualisieren** aktiviert ist, und klicken Sie dann auf **Weiter**.  

6.  Geben Sie auf der Seite **Assistenten abschließen** einen Namen für das Berichtsmodell an. Für dieses Beispiel muss **Erweitertes_Modell** angezeigt sein.  

7.  Klicken Sie auf **Ausführen**, um den Assistenten abzuschließen und das Berichtsmodell zu erstellen.  

8.  Zum Beenden des Assistenten klicken Sie auf **Fertig stellen**.  

9. Das Berichtsmodell wird im Entwurfsfenster angezeigt.  

#### <a name="to-modify-object-names-in-the-report-model"></a>So ändern Sie Objektnamen im Berichtsmodell  

1.  Klicken Sie im **Projektmappen-Explorer**mit der rechten Maustaste auf ein Berichtsmodell, um **Sicht-Designer**auszuwählen. Wählen Sie für dieses Beispiel **Erweitertes_Modell.smdl**aus.  

2.  Klicken Sie in der Berichtsmodell-Entwurfsansicht mit der rechten Maustaste auf einen Objektnamen, um **Umbenennen**auszuwählen.  

3.  Geben Sie einen neuen Namen für das ausgewählte Objekt ein, und drücken Sie die Eingabetaste. Zum Beispiel könnten Sie den Namen des Objekts **CSD_Version_0** in **Windows Service Pack-Version**ändern.  

4.  Nachdem Sie alle gewünschten Objekte umbenannt haben, klicken Sie auf **Datei**und dann auf **Alle speichern**.  

#### <a name="to-publish-the-report-model-for-use-in-sql-server-reporting-services"></a>So veröffentlichen Sie das Berichtsmodell (zur Verwendung in SQL Server Reporting Services)  

1.  Klicken Sie im **Projektmappen-Explorer**mit der rechten Maustaste auf **Erweitertes_Modell.smdl** , um **Bereitstellen**auszuwählen.  

2.  Unten links im Fenster **SQL Server Business Intelligence Development Studio** wird der Bereitstellungsstatus angezeigt. Wenn die Bereitstellung abgeschlossen ist, wird die Meldung **Bereitstellen erfolgreich** angezeigt. Falls bei der Bereitstellung ein Fehler aufgetreten ist, wird die Ursache im Fenster **Ausgabe** angezeigt. Das neue Berichtsmodell steht nun auf Ihrer SQL Server Reporting Services-Website zur Verfügung.  

3.  Klicken Sie auf **Datei**und dann auf **Alle speichern**, und beenden Sie danach **SQL Server Business Intelligence Development Studio**.  

#### <a name="to-deploy-the-custom-report-model-to-configuration-manager"></a>To deploy the custom report model to Configuration Manager  

1. Suchen Sie den Ordner, in dem Sie das Berichtsmodellprojekt erstellt haben. Beispiel: %*USERPROFILE*%\Documents\Visual Studio 2008\Projects\\ *&lt;Projektname\>.*  

2. Kopieren Sie die folgenden Dateien aus dem Projektordner für das Berichtsmodell in einen temporären Ordner auf Ihrem Computer.  

   -   *&lt;Modellname\>* **.dsv**  

   -   *&lt;Modellname\>* **.smdl**  

3. Öffnen Sie die oben aufgeführten Dateien mit einem Text-Editor, z. B. Notepad.  

4. Suchen Sie in der Datei _&lt;Modellname\>_ **.dsv** die erste Zeile, die wie folgt lautet:  

    `<DataSourceView xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">`

    Bearbeiten Sie diese Zeile, sodass sie wie folgt lautet:  

    `<DataSourceView xmlns="<https://schemas.microsoft.com/analysisservices/2003/engine>" xmlns:xsi="RelationalDataSourceView">`

5. Kopieren Sie den gesamten Inhalt der Datei in die Windows-Zwischenablage.  

6. Schließen Sie die Datei _&lt;Modellname\>_ **.dsv**.  

7. Suchen Sie in der Datei _&lt;Modellname\>_ **.smdl** die letzten drei Zeilen der Datei, die wie folgt lauten:  

    `</Entity>`  

    `</Entities>`  

    `</SemanticModel>`  

8. Fügen Sie den Inhalt der Datei _&lt;Modellname\>_ **.dsv** direkt vor der letzten Zeile der Datei ein ( **&lt;SemanticModel\>** ).  

9. Speichern und schließen Sie die Datei _&lt;Modellname\>_ **.smdl**.  

10. Kopieren Sie die Datei _&lt;Modellname\>_ **.smdl** in den Ordner „ *%programfiles%* \Microsoft Configuration Manager \AdminConsole\XmlStorage\Other“ auf dem Configuration Manager-Standortserver.  

    > [!IMPORTANT]  
    >  Nach dem Kopieren der Berichtsmodelldatei auf den Configuration Manager-Standortserver müssen Sie die Configuration Manager-Konsole beenden und neu starten, um das Berichtsmodell im **Assistenten zum Erstellen von Berichten** verwenden zu können.  
