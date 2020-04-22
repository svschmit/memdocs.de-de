---
title: Verwenden von Asset Intelligence
titleSuffix: Configuration Manager
description: Führen Sie allgemeine Asset Intelligence-Tasks in Configuration Manager aus.
ms.date: 08/30/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e8159bd9-5c2b-4d25-82f9-78fcfd732ba9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1e272e8e71ceaa15c712cb3a53d9db835747d327
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695068"
---
# <a name="how-to-use-asset-intelligence-in-configuration-manager"></a>Verwenden von Asset Intelligence in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Dieses Thema enthält Informationen zum Verwalten typischer Asset Intelligence-Tasks in Ihrer Configuration Manager-Hierarchie:  

##  <a name="view-asset-intelligence-information"></a><a name="BKMK_ViewInformation"></a> Anzeigen von Asset Intelligence-Informationen  
 Asset Intelligence-Informationen können auf der **Asset Intelligence** -Startseite und in Asset Intelligence-Berichten angezeigt werden.  

###  <a name="asset-intelligence-home-page"></a><a name="BKMK_AssetIntelligenceHomePage"></a> Asset Intelligence-Startseite  
 Auf der **Asset Intelligence** -Startseite wird eine Zusammenfassung von Asset Intelligence-Kataloginformationen angezeigt. Auf der Startseite können Sie Informationen zur Katalogsynchronisierung und zum Status für inventarisierte Software anzeigen. Die **Asset Intelligence** -Startseite ist in folgende Abschnitte untergliedert:  

- **Katalogsynchronisierung:** Enthält Informationen darüber, ob Asset Intelligence aktiviert ist, über den aktuellen Status des Asset Intelligence-Synchronisierungspunkts, den Synchronisierungszeitplan, ferner darüber, ob die Kundenlizenzübersicht importiert wird und wann der Status zuletzt aktualisiert wurde. Außerdem enthält der Bereich Informationen über den Zeitpunkt des nächsten geplanten Updates und über die Anzahl der vorgenommenen Änderungen seit der Installation des Asset Intelligence-Synchronisierungspunkt-Standortsystems.  

  > [!NOTE]  
  >  Der Synchronisierungsbereich des Asset Intelligence-Katalogs auf der **Asset Intelligence** -Startseite wird nur angezeigt, wenn eine Standortsystemrolle für den Asset Intelligence-Synchronisierungspunkt installiert wurde.  

- **Status für inventarisierte Software:** Enthält die Anzahl und den Prozentsatz inventarisierter Softwaretitel, Softwarekategorien und Softwarefamilien, die von Microsoft oder einem Administrator identifiziert wurden, deren Onlineidentifikation aussteht oder die nicht identifiziert sind und deren Onlineidentifikation nicht ausstehend ist. Die Informationen im Tabellenformat repräsentieren die jeweilige Anzahl, die Informationen im Diagramm den jeweiligen Prozentsatz.  

  Gehen Sie wie folgt vor, um Asset Intelligence-Informationen auf der **Asset Intelligence** -Startseite anzuzeigen.  

##### <a name="to-view-asset-intelligence-information-on-the-asset-intelligence-home-page"></a>So zeigen Sie Asset Intelligence-Informationen auf der Asset Intelligence-Startseite an  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Asset Intelligence**. Die Asset Intelligence-Berichte werden angezeigt.  

###  <a name="asset-intelligence-reports"></a><a name="BKMK_AssetIntelligenceReports"></a> Asset Intelligence-Berichte  
 Es sind über 60 Asset Intelligence-Berichte verfügbar, die die von Asset Intelligence gesammelten Informationen anzeigen. Viele dieser Berichte sind mit detaillierteren Berichten verknüpft, sodass Sie allgemeine Informationen abfragen und dann per Drilldown ausführlichere Informationen anzeigen können. Sie finden die Asset Intelligence-Berichte in der Configuration Manager-Konsole im Arbeitsbereich **Überwachung** unter dem Knoten **Berichterstellung**. Die Berichte enthalten Informationen zu Hardware, Lizenzverwaltung und Software. Weitere Informationen zu Berichten in Configuration Manager finden Sie unter [Einführung in die Berichterstellung](../../../servers/manage/introduction-to-reporting.md).  

> [!NOTE]  
>  Die Genauigkeit der in Asset Intelligence-Berichten angezeigten Anzahl installierter Softwaretitel und der Lizenzinformationen kann aufgrund komplizierter Abhängigkeiten und Einschränkungen bei der Inventur von Softwarelizenzinformationen für die in Unternehmen installierten Softwaretitel von der tatsächlichen Anzahl installierter Softwaretitel oder verwendeter Lizenzen in Unternehmensumgebungen abweichen. Asset Intelligence-Berichte sollten bei der Prüfung der erworbenen Softwarelizenzen nicht als alleinige Quelle herangezogen werden.  

 Gehen Sie wie folgt vor, um Asset Intelligence-Informationen mithilfe der Asset Intelligence-Berichte anzuzeigen.  

##### <a name="to-view-collected-asset-intelligence-information-by-using-asset-intelligence-reports"></a>So zeigen Sie die gesammelten Asset Intelligence-Informationen mithilfe der Asset Intelligence-Berichte an  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Erweitern Sie im Arbeitsbereich **Überwachung** den Knoten **Berichterstattung**, dann **Berichte**, und klicken Sie auf **Asset Intelligence**. Die Asset Intelligence-Berichte werden angezeigt.  

    > [!WARNING]  
    >  Wenn unter dem Knoten **Berichte** keine Berichtsordner vorhanden sind, überprüfen Sie, ob Sie die Berichterstattung konfiguriert haben. Weitere Informationen finden Sie unter [Konfigurieren von Berichten](../../../../core/servers/manage/configuring-reporting.md).  

3.  Wählen Sie den Asset Intelligence-Bericht aus, der ausgeführt werden soll, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Berichtsgruppe** auf **Ausführen**.  

##  <a name="synchronize-the-asset-intelligence-catalog"></a><a name="BKMK_SynchronizeTheCatalog"></a> Synchronisieren des Asset Intelligence-Katalogs  
 Sie können den lokalen Asset Intelligence-Katalog mit System Center Online synchronisieren, um die aktuellste Softwaretitelkategorisierung abzurufen. Wenn Sie die Katalogsynchronisierung mit System Center Online manuell anfordern, kann es mindestens 15 Minuten dauern, bis der Synchronisierungsprozess mit System Center Online abgeschlossen ist. Configuration Manager aktualisiert die Einstellung **Letztes erfolgreiches Update** auf der **Asset Intelligence**-Startseite mit der aktuellen Zeit, zu der die Synchronisierung erfolgreich abgeschlossen wurde.  

> [!NOTE]  
>  Bevor das in diesem Thema beschriebenen Verfahren angewendet werden kann, muss eine Standortsystemrolle für den Asset Intelligence-Synchronisierungspunkt installiert werden. Weitere Informationen zum Installieren eines Asset Intelligence-Synchronisierungspunkts finden Sie im Abschnitt [Konfigurieren von Asset Intelligence](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

 Gehen Sie wie folgt vor, um einen Synchronisierungszeitplan für den Asset Intelligence-Katalog zu erstellen.  

#### <a name="to-create-a-synchronization-schedule-for-the-asset-intelligence-catalog"></a>So erstellen Sie einen Synchronisierungszeitplan für den Asset Intelligence-Katalog  

1. Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2. Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Asset Intelligence**.  

3. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Synchronisieren**und dann auf **Synchronisierung planen**.  

4. Wählen Sie im Dialogfeld **Zeitplan für Asset Intelligence-Synchronisierungspunkt** die Option **Synchronisierung nach Zeitplan aktivieren**aus, und konfigurieren Sie dann einen einfachen oder benutzerdefinierten Zeitplan.  

5. Klicken Sie zum Speichern der Änderungen auf **OK** .  

   > [!NOTE]  
   >  Weitere Informationen zum Synchronisierungszeitplan einschließlich der nächsten geplanten Synchronisierung finden Sie im Knoten **Asset Intelligence** im Arbeitsbereich **Bestand und Kompatibilität** im Standort der obersten Ebene der Hierarchie.  

   Gehen Sie wie folgt vor, um den Asset Intelligence-Katalog manuell zu synchronisieren.  

> [!WARNING]  
>  Von System Center Online wird innerhalb eines Zeitraums von 12 Stunden nur eine Synchronisierungsanforderung zugelassen.  

###  <a name="to-manually-synchronize-the-asset-intelligence-catalog"></a><a name="BKMK_ManuallySynchronizeCatalog"></a> So führen Sie eine manuelle Synchronisierung des Asset Intelligence-Katalogs durch  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Asset Intelligence**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Synchronisieren**, dann auf **Asset Intelligence-Katalog synchronisieren**und dann auf **OK**.  

##  <a name="customize-the-asset-intelligence-catalog"></a><a name="BKMK_CustomizeCatalog"></a> Anpassen des Asset Intelligence-Katalogs  
 Kategorisierungsinformationen zum Asset Intelligence-Katalog, die von System Center Online heruntergeladen wurden, werden schreibgeschützt in der Standortdatenbank gespeichert und können weder geändert noch gelöscht werden. Es können jedoch benutzerdefinierte Softwarekategorien, Softwarefamilien, Softwarebezeichnungen und Hardwareanforderungs-Kataloginformationen erstellt, geändert und gelöscht werden. Dann können benutzerdefinierte Kategorisierungsdaten anstatt der von System Center Online bereitgestellten Daten für vorhandene benutzerdefinierte Softwaretitelinformationen verwendet werden. Wenn Kategorisierungsinformationen geändert oder hinzugefügt werden, gelten die Kataloginformationen als benutzerdefiniert. Benutzerdefinierte Kategorisierungsinformationen werden in anderen Datenbanktabellen gespeichert als geprüfte Kataloginformationen.  

###  <a name="software-categories"></a><a name="BKMK_SoftwareCategories"></a> Softwarekategorien  
 Asset Intelligence-Softwarekategorien werden zur groben Kategorisierung inventarisierter Softwaretitel verwendet sowie zum allgemeinen Gruppieren spezifischerer Softwarefamilien. Eine Softwarekategorie könnte beispielsweise ein Energieversorgungsunternehmen sein und eine Softwarefamilie innerhalb dieser Softwarekategorie beispielsweise Öl und Gas oder Wasserenergie. Viele Softwarekategorien sind im Asset Intelligence-Katalog vordefiniert. Zusätzliche benutzerdefinierte Kategorien können hinzugefügt werden, um die inventarisierte Software näher zu definieren. Der Überprüfungszustand aller vordefinierten Softwarekategorien lautet immer **Überprüft**, während dem Asset Intelligence-Katalog hinzugefügte benutzerdefinierte Softwarekategorieinformationen als **Benutzerdefiniert**angegeben werden.  

 Gehen Sie wie folgt vor, um eine benutzerdefinierte Softwarekategorie zu erstellen.  

##### <a name="to-create-a-user-defined-software-category"></a>So erstellen Sie eine benutzerdefinierte Softwarekategorie  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Asset Intelligence**, und klicken Sie dann auf **Katalog**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Softwarekategorie erstellen**.  

4.  Geben Sie auf der Seite **Allgemein** einen Namen und optional eine Beschreibung für die neue Softwarekategorie ein.  

    > [!NOTE]  
    >  Der Überprüfungszustand für alle selbst erstellten neuen Softwarekategorien ist immer auf **Benutzerdefiniert**eingestellt.  

     Klicken Sie auf **Weiter**.  

5.  Überprüfen Sie auf der Seite **Zusammenfassung** die Einstellungen, und klicken Sie dann auf **Weiter**.  

6.  Klicken Sie auf der Seite **Abschluss des Vorgangs** zum Beenden des Assistenten auf **Schließen** .  

###  <a name="software-families"></a><a name="BKMK_SoftwareFamilies"></a> Softwarefamilien  
 Mithilfe von Asset Intelligence-Softwarefamilien können inventarisierte Softwaretitel innerhalb von Softwarekategorien genauer definiert werden. Eine Softwarekategorie könnte beispielsweise ein Energieversorgungsunternehmen sein und eine Softwarefamilie innerhalb dieser Softwarekategorie beispielsweise Öl und Gas oder Wasserenergie. Viele Softwarefamilien sind im Asset Intelligence-Katalog vordefiniert. Zur Definition der inventarisierten Software können zusätzliche benutzerdefinierte Familien erstellt werden. Der Überprüfungszustand aller vordefinierten Softwarefamilien lautet immer **Überprüft**, während dem Asset Intelligence-Katalog hinzugefügte benutzerdefinierte Softwarefamilien als **Benutzerdefiniert**angegeben werden.  

 Gehen Sie wie folgt vor, um eine benutzerdefinierte Softwarefamilie zu erstellen.  

##### <a name="to-create-a-user-defined-software-family"></a>So erstellen Sie eine benutzerdefinierte Softwarefamilie  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Asset Intelligence**, und klicken Sie dann auf **Katalog**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Softwarefamilie erstellen**.  

4.  Geben Sie auf der Seite **Allgemein** einen Namen und optional eine Beschreibung für die neue Softwarefamilie ein.  

    > [!NOTE]  
    >  Der Überprüfungszustand für alle selbst erstellten neuen Softwarefamilien ist immer auf **Benutzerdefiniert**eingestellt.  

5.  Überprüfen Sie auf der Seite **Zusammenfassung** die Einstellungen, und klicken Sie dann auf **Weiter**.  

6.  Klicken Sie auf der Seite **Abschluss des Vorgangs** zum Beenden des Assistenten auf **Schließen** .  

###  <a name="software-labels"></a><a name="BKMK_SoftwareLabels"></a> Softwarebezeichnungen  
 Mit benutzerdefinierten Softwarebezeichnungen können Sie in Asset Intelligence Filter zum Gruppieren von Softwaretiteln und zum Anzeigen der Softwaretitel in Asset Intelligence-Berichten erstellen. Sie können beispielsweise eine Softwarebezeichnung namens "Shareware" erstellen, diese einer Reihe von Anwendungen zuweisen und dann einen Bericht ausführen, in dem alle Titel mit der Bezeichnung "Shareware" aufgeführt werden. Der Überprüfungszustand ist für alle benutzerdefinierten Softwarebezeichnungen, die dem Asset Intelligence-Katalog hinzugefügt werden, auf **Benutzerdefiniert** eingestellt.  

 Gehen Sie wie folgt vor, um eine benutzerdefinierte Softwarebezeichnung zu erstellen.  

##### <a name="to-create-a-user-defined-software-label"></a>So erstellen Sie eine benutzerdefinierte Softwarebezeichnung  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Asset Intelligence**, und klicken Sie dann auf **Katalog**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Softwarebezeichnung erstellen**.  

4.  Geben Sie auf der Seite **Allgemein** einen Namen und optional eine Beschreibung für die neue Softwarefamilie ein.  

    > [!NOTE]  
    >  Der Überprüfungszustand für alle selbst erstellten neuen Softwarebezeichnungen ist immer auf **Benutzerdefiniert**eingestellt.  

5.  Überprüfen Sie auf der Seite **Zusammenfassung** die Einstellungen, und klicken Sie dann auf **Weiter**.  

6.  Klicken Sie auf der Seite **Abschluss des Vorgangs** zum Beenden des Assistenten auf **Schließen** .  

###  <a name="hardware-requirements"></a><a name="BKMK_HardwareRequirements"></a> Hardwareanforderungen  
 Mithilfe von Informationen zu Hardwareanforderungen kann überprüft werden, ob Computer die Hardwareanforderungen für Softwaretitel erfüllen, bevor auf ihnen Softwarebereitstellungen vorgenommen werden. Viele Hardwareanforderungen sind im Asset Intelligence-Katalog vordefiniert, und es können neue benutzerdefinierte Hardwareanforderungsinformationen erstellt werden, um benutzerdefinierten Anforderungen zu entsprechen. Der Überprüfungszustand aller vordefinierten Hardwareanforderungen lautet immer **Überprüft**, während dem Asset Intelligence-Katalog hinzugefügte benutzerdefinierte Hardwareanforderungen als **Benutzerdefiniert**angegeben werden.  

> [!IMPORTANT]  
>  Die in der Configuration Manager-Konsole angezeigten Hardwareanforderungen werden vom Asset Intelligence-Katalog auf dem lokalen Computer abgerufen und basieren nicht auf inventarisierten Informationen zu Softwaretiteln von System Center 2012 Configuration Manager-Clients. Die Hardwareanforderungsinformationen werden nicht als Teil der Synchronisierung mit System Center Online aktualisiert. Sie können benutzerdefinierte Hardwareanforderungen für inventarisierte Software erstellen, der keine Hardwareanforderungen zugeordnet sind.  

 Gehen Sie wie folgt vor, um benutzerdefinierte Hardwareanforderungen zu erstellen.  

##### <a name="to-create-a-user-defined-hardware-requirements"></a>So erstellen Sie benutzerdefinierte Hardwareanforderungen  

1. Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2. Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Asset Intelligence**, und klicken Sie dann auf **Hardwareanforderungen**.  

3. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Hardwareanforderungen erstellen**.  

4. Geben Sie auf der Seite **Allgemein** die folgenden Informationen ein:  

   1. **Softwaretitel:** Gibt den Softwaretitel an, dem die Hardwareanforderungen zugeordnet sind. Der Softwaretitel darf im Asset Intelligence-Katalog noch nicht vorhanden sein.  

   2. **Überprüfungszustand:** Gibt den Überprüfungszustand für die Hardwareanforderungen als **Benutzerdefiniert** an. Diese Einstellung kann nicht geändert werden.  

   3. **Mindesttaktfrequenz der CPU (MHz):** Gibt die Mindestprozessorgeschwindigkeit in Megahertz (MHz) an, die vom Softwaretitel benötigt wird.  

   4. **Mindestgröße des RAM (KB):** Gibt die Mindestgröße des Arbeitsspeichers in Kilobyte (KB) an, die vom Softwaretitel benötigt wird.  

   5. **Mindestspeicherplatz auf dem Datenträger (KB):** Gibt den freien Mindestspeicherplatz auf dem Datenträger in KB an, der vom Softwaretitel benötigt wird.  

   6. **Mindestgröße des Datenträgers (KB):** Gibt die Mindestgröße des Datenträgers in KB an, der vom Softwaretitel benötigt wird.  

      Klicken Sie auf **Weiter**.  

5. Überprüfen Sie auf der Seite **Zusammenfassung** die Einstellungen, und klicken Sie dann auf **Weiter**.  

6. Klicken Sie auf der Seite **Abschluss des Vorgangs** zum Beenden des Assistenten auf **Schließen** .  

###  <a name="modify-categorization-information-for-inventoried-software"></a><a name="BKMK_ModifyCategorization"></a> Ändern von Kategorisierungsinformationen für inventarisierte Software  
 Im Asset Intelligence-Katalog vordefinierte Software ist mit bestimmten Kategorisierungsinformationen beispielsweise zu Produktnamen, Hersteller, Softwarekategorie und Softwarefamilie konfiguriert. Wenn die vordefinierten Kategorisierungsinformationen Ihren Anforderungen nicht entsprechen, können Sie die Informationen in den Eigenschaften für den Softwaretitel ändern. Wenn Kategorisierungsinformationen für vordefinierte Software geändert werden, wird der Überprüfungszustand für die Software von **Überprüft** auf **Benutzerdefiniert**geändert.  

> [!IMPORTANT]  
>  Die Kategorisierungsinformationen können nur am Standort der obersten Ebene geändert werden.  

 Gehen Sie wie folgt vor, um Kategorisierungsinformationen für inventarisierte Software zu ändern.  

##### <a name="to-modify-the-categorizations-for-software-titles"></a>So ändern Sie die Kategorisierungen für Softwaretitel  

1. Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2. Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Asset Intelligence**, und klicken Sie dann auf **Inventarisierte Software**.  

3. Wählen Sie mindestens einen Softwaretitel aus, für den Kategorisierungen geändert werden sollen.  

4. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

5. Auf der Registerkarte **Allgemein** können Sie die folgenden Kategorisierungsinformationen ändern:  

   -   **Produktname:** Gibt den Namen des inventarisierten Softwaretitels an.  

   -   **Hersteller:** Gibt den Namen des Herstellers an, der den inventarisierten Softwaretitel entwickelt hat.  

   -   **Kategorie**: Gibt die Softwarekategorie an, die dem inventarisierten Softwaretitel derzeit zugewiesen ist.  

   -   **Familie:** Gibt die Softwarefamilie an, die dem inventarisierten Softwaretitel derzeit zugewiesen ist.  

6. Klicken Sie zum Speichern der Änderungen auf **OK** .  

   Gehen Sie wie folgt vor, um die ursprünglichen Kategorisierungsinformationen für Software wiederherzustellen.  

### <a name="revert-categorization-information-to-original-settings-for-software"></a>Wiederherstellen der ursprünglichen Kategorisierungsinformationen für Software  
 In Configuration Manager werden von System Center Online erhaltene Kategorisierungsinformationen in der Datenbank gespeichert. Die Informationen können nicht gelöscht werden. Nach Änderungen an den Informationen können die Kategorisierungsinformationen wieder auf die System Center Online-Kategorisierung zurückgesetzt werden. Auch inventarisierte Software, die sich nicht im Asset Intelligence-Katalog befindet, kann auf die ursprünglichen Einstellungen zurückgesetzt werden.  

 Gehen Sie wie folgt vor, um die ursprünglichen Kategorisierungsinformationen wiederherzustellen.  

##### <a name="to-revert-categorization-information-to-original-settings"></a>So stellen Sie die ursprünglichen Kategorisierungsinformationen wieder her  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Asset Intelligence**, und klicken Sie dann auf **Inventarisierte Software**.  

3.  Wählen Sie mindestens einen Softwaretitel aus, bei dem Sie die ursprünglichen Einstellungen wiederherstellen möchten. Es können nur bei Softwaretiteln mit dem Zustand **Benutzerdefiniert** die ursprünglichen Kategorisierungsinformationen wiederhergestellt werden.  

    > [!TIP]  
    >  Klicken Sie auf die Spalte **Zustand** , um nach dem Überprüfungszustand zu sortieren. Durch Sortieren erhalten Sie einen Softwareüberblick nach Überprüfungszustand und können im Handumdrehen mehrere Elemente auswählen, um für diese die ursprünglichen Einstellungen wiederherzustellen.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Produkt** auf **Wiederherstellen**.  

5.  Klicken Sie auf **Ja** , um die ursprünglichen Kategorisierungsinformationen der Software wiederherzustellen.  

6.  Wenn Sie Kategorisierungsinformationen für Software wiederherstellen, die sich im Asset Intelligence-Katalog befindet, ändert sich der Überprüfungszustand von **Benutzerdefiniert** in **Überprüft**. Wenn Sie Software wiederherstellen, die sich nicht im Katalog befindet, ändert sich der Überprüfungszustand von **Benutzerdefiniert** in **Nicht kategorisiert**.  

##  <a name="request-a-catalog-update-for-uncategorized-software-titles"></a><a name="BKMK_RequestCatalogUpdate"></a> Anfordern eines Katalogupdates für nicht kategorisierte Softwaretitel  
 Informationen zu nicht kategorisierten Softwaretiteln können zu Recherche- und Kategorisierungszwecken an System Center Online übermittelt werden. Nach der Übermittlung eines nicht kategorisierten Softwaretitels identifizieren und kategorisieren Entwicklungsmitarbeiter den Softwaretitel und stellen die Informationen zur Softwaretitelkategorisierung dann über System Center Online für alle Kunden zur Verfügung. Voraussetzung ist allerdings, dass mindestens vier Kategorisierungsanforderungen von Kunden für diesen Softwaretitel vorliegen. Microsoft verleiht den Softwaretiteln die höchste Priorität, deren Kategorisierung am häufigsten angefordert wurde. Benutzerdefinierte Software und Branchenanwendungen erhalten i. d. R. keine Kategorie. Es empfiehlt sich daher, diese Softwaretitel nicht zur Kategorisierung an Microsoft zu senden.  

 Wenn Informationen zu nicht kategorisierten Softwaretiteln an System Center Online übermittelt werden, gelten die folgenden Bedingungen.  

-   Nur grundlegende Informationen zum Softwaretitel werden an System Center Online übermittelt, und die zu kategorisierenden Softwaretitelinformationen können vor der Übermittlung überprüft werden.  

-   Softwarelizenzinformationen werden nicht übermittelt.  

-   Jeder aktualisierte Softwaretitel wird als Teil des System Center Online-Katalogs öffentlich zur Verfügung gestellt und kann von anderen Kunden heruntergeladen werden.  

-   Die Quelle des Softwaretitels wird nicht im System Center Online-Katalog gespeichert. Allerdings sollten Anwendungstitel, die vertrauliche oder proprietäre Informationen enthalten, nicht zur Kategorisierung durch System Center Online übermittelt werden.  

> [!NOTE]  
>  Weitere Informationen zum Datenschutz in Asset Intelligence finden Sie unter [Sicherheit und Datenschutz für Asset Intelligence](../../../../core/clients/manage/asset-intelligence/security-and-privacy-for-asset-intelligence.md).  

 Gehen Sie wie folgt vor, um eine Softwaretitelkategorisierung für den Asset Intelligence-Katalog von System Center Online anzufordern.  

#### <a name="to-request-a-catalog-update-for-uncategorized-software-titles"></a>So fordern Sie ein Katalogupdate für nicht kategorisierte Softwaretitel an  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Asset Intelligence**, und klicken Sie dann auf **Inventarisierte Software**.  

3.  Wählen Sie mindestens einen zur Kategorisierung an System Center Online zu übermittelnden Produktnamen aus. Nur nicht kategorisierte inventarisierte Softwaretitel können zur Kategorisierung an System Center Online übermittelt werden. Wenn ein inventarisierter Softwaretitel von einem Administrator kategorisiert wurde und das zu einem benutzerdefinierten Zustand geführt hat, müssen Sie mit der rechten Maustaste auf den inventarisierten Softwaretitel und dann auf **Wiederherstellen** klicken, um den Softwaretitel in den Zustand **Nicht kategorisiert** zurückzusetzen, bevor er zur Kategorisierung an System Center Online übermittelt werden kann.  

    > [!NOTE]  
    >  In Configuration Manager können bis zu 2.000 Softwaretitel gleichzeitig zur Kategorisierung verarbeitet werden. Wenn Sie eine höhere Anzahl auswählen, werden nur die ersten 2.000 Softwaretitel verarbeitet. Sie müssen die verbleibenden zu kategorisierenden Softwaretitel stapelweise auswählen, wobei sich weniger als 2.000 Softwaretitel im jeweiligen Stapel befinden dürfen.  

    > [!TIP]  
    >  Klicken Sie auf die Spalte **Zustand** , um nach dem Überprüfungszustand zu sortieren. Mit dieser Aktion können Sie alle nicht kategorisierten Produktnamen anzeigen und schnell mehrere Elemente auswählen, um eine Kategorisierungsanforderung für diese zu übermitteln.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Produkt** auf **Katalogupdate anfordern**.  

5.  Lesen Sie die Datenschutzmeldung zur Kategorisierungsübermittlung an System Center Online. Klicken Sie auf **Details** , um die Informationen anzuzeigen, die an System Center Online gesendet werden.  

6.  Wählen Sie **Ich habe diese Meldung gelesen und verstanden**aus, und klicken Sie dann auf **OK** , damit die ausgewählten Softwaretitel zur Kategorisierung übermittelt werden können.  

7.  Überprüfen Sie, ob sich der Zustand der Namen von inventarisierten Softwareprodukten, die an System Center Online zur Kategorisierung übermittelt wurden, von **Nicht kategorisiert** in **Ausstehend**ändert.  

    > [!NOTE]  
    >  Software, die an System Center Online zur Kategorisierung übermittelt wurde, hat zwar den Überprüfungszustand **Ausstehend** am zentralen Verwaltungsstandort, wird jedoch an untergeordneten primären Standorten mit dem Überprüfungszustand **Nicht kategorisiert** angezeigt.  

##  <a name="resolve-software-details-conflicts"></a><a name="BKMK_ResolveSoftwareDetails"></a> Auflösen von Konflikten zwischen Softwaredetails  
 Wenn neu aktualisierte Softwarekategorisierungsdetails von System Center Online empfangen wurden, die in Konflikt mit vorhandenen Softwaredetailinformationen stehen, haben Sie die Möglichkeit auszuwählen, wie Sie den Konflikt auflösen möchten. Software, bei der ein aktueller Konflikt vorliegt, hat den Überprüfungszustand **Aktualisierbar**. Nach der Lösung des Konflikts zwischen Softwaredetails verbleiben die Softwarekategorisierungsinformationen entsprechend der festgelegten Einstellungen im Asset Intelligence-Katalog. Für denselben Softwarekategorisierungswert tritt kein erneuter Konflikt zwischen Softwaredetails auf, es sei denn, der System Center Online-Wert wird nach Lösung des Konflikts geändert.  

 Gehen Sie wie folgt vor, um einen Konflikt zwischen Softwaredetails aufzulösen.  

#### <a name="to-resolve-a-software-details-conflict"></a>So lösen Sie einen Konflikt zwischen Softwaredetails auf  

1. Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2. Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Asset Intelligence**, und klicken Sie dann auf **Inventarisierte Software**.  

3. Überprüfen Sie die Spalte **Zustand** für Softwaretitel mit dem Zustand **Aktualisierbar** .  

4. Wählen Sie den Softwaretitel aus, für den es einen Konflikt zu beheben gilt, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Produkt** auf **Konflikt beheben**.  

5. Überprüfen Sie die folgenden Informationen:  

   -   **Lokaler Wert:** Gibt die vorhandenen Softwarekategorisierungsinformationen des Asset Intelligence-Katalogs an, die in Konflikt mit neueren Softwarekategorisierungsdetails von System Center Online stehen.  

   -   **Heruntergeladener Wert:** Gibt die neuen Softwarekategorisierungsinformationen von System Center Online an, die in Konflikt mit den Softwarekategorisierungsinformationen des Asset Intelligence-Katalogs stehen.  

6. Wählen Sie mindestens eine der folgenden Einstellungen aus, um den Konflikt zwischen Softwaredetails aufzulösen:  

   - **Do not change the locally edited catalog information value** (Die im lokal bearbeiteten Katalog enthaltenen Informationen beibehalten): Löst den Konflikt zwischen Softwaredetails durch Beibehalten der vorhandenen Softwarekategorisierungsinformationen im Asset Intelligence-Katalog. Wenn Sie diese Einstellung auswählen, ändert sich der Softwaretitelzustand von **Aktualisierbar** in **Benutzerdefiniert**.  

   - **Overwrite the locally edited catalog information value with the downloaded System Center Online value** (Die im lokal bearbeiteten Katalog enthaltenen Informationen mit den Informationen aus dem System Center Online-Katalog überschreiben): Löst den Konflikt zwischen Softwaredetails durch Überschreiben der vorhandenen Softwarekategorisierungsinformationen im Asset Intelligence-Katalog mit den neuen Informationen von System Center Online. Wenn Sie diese Einstellung auswählen, ändert sich der Softwaretitelzustand von **Aktualisierbar** in **Überprüft**.  

     Klicken Sie auf **OK** , um die Konfliktauflösung zu speichern.  
