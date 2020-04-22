---
title: Einführung in Asset Intelligence
titleSuffix: Configuration Manager
description: Mit Asset Intelligence in Configuration Manager können Sie die Softwarelizenzverwendung im gesamten Unternehmen inventarisieren und verwalten.
ms.date: 12/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0bdfdef5-390f-4099-8bde-de51d9a89175
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 25deb098f6e1f4ce275a0c0a0817249cd36558f7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695088"
---
# <a name="introduction-to-asset-intelligence-in-configuration-manager"></a>Einführung in Asset Intelligence in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Inventarisieren und verwalten Sie die Softwarelizenzverwendung im gesamten Unternehmen mithilfe des Asset Intelligence-Katalogs. Durch die in Asset Intelligence hinzugefügten Hardwareinventurklassen wird der Umfang der von Configuration Manager erfassten Informationen erweitert. Diese Informationen umfassen die Hardware- und Softwaretitel, die in Ihrer Umgebung verwendet werden. In über 60 Berichten werden diese Informationen in einem benutzerfreundlichen Format dargestellt. Viele dieser Berichte sind mit spezifischeren Berichten verknüpft. Sie können also allgemeine Informationen abfragen und einen Drilldown ausführen, um detailliertere Informationen anzuzeigen. 

Sie können dem Asset Intelligence-Katalog benutzerdefinierte Informationen hinzufügen. Dies gilt beispielsweise für benutzerdefinierte Softwarekategorien, Softwarefamilien, Softwarebezeichnungen und Hardwareanforderungen. Um den Asset Intelligence-Katalog mit den neuesten verfügbaren Informationen dynamisch zu aktualisieren, können Sie ihn mit der Microsoft Cloud verbinden. 

Mit Asset Intelligence können Sie die Verwendung von Unternehmenssoftwarelizenzen abstimmen. Importieren Sie die Softwarelizenzinformationen in die Configuration Manager-Standortdatenbank, und vergleichen Sie diese mit der verwendeten Software.  



## <a name="asset-intelligence-catalog"></a><a name="BKMK_AssetIntelligenceCatalog"></a> Asset Intelligence-Katalog  

Beim Asset Intelligence-Katalog handelt es sich um eine Reihe von in der Standortdatenbank gespeicherten Datenbanktabellen. Diese Tabellen enthalten Kategorisierungs- und Identifikationsinformationen von über 300.000 Softwaretiteln und -versionen. Außerdem unterstützen Sie diese Tabellen beim Verwalten der Hardwareanforderungen bestimmter Softwaretitel.  

Asset Intelligence stellt Softwarelizenzinformationen für die verwendeten Softwaretitel sowohl für Software von Microsoft als auch von anderen Anbietern bereit. Im Asset Intelligence-Katalog sind vordefinierte Hardwareanforderungen für Softwaretitel verfügbar, und Sie können neue benutzerdefinierte Hardwareanforderungsinformationen gemäß Ihren individuellen Anforderungen erstellen. Sie können auch Informationen im Asset Intelligence-Katalog anpassen und Softwaretitelinformationen zur Kategorisierung in die Microsoft Cloud hochladen.  

Asset Intelligence-Katalogupdates, die neu veröffentlichte Software umfassen, können in regelmäßigen Abständen heruntergeladen werden, um Massenkatalogupdates auszuführen. Der Katalog kann auch mithilfe des Asset Intelligence-Synchronisierungspunkts dynamisch aktualisiert werden.  


### <a name="software-categories"></a><a name="BKMK_SoftwareCategories"></a> Softwarekategorien  

Asset Intelligence-Softwarekategorien werden zur groben Kategorisierung inventarisierter Softwaretitel sowie zum allgemeinen Gruppieren von spezifischeren Softwarefamilien verwendet. Eine Softwarekategorie könnte beispielsweise ein Energieversorgungsunternehmen sein und eine Softwarefamilie innerhalb dieser Softwarekategorie beispielsweise Öl und Gas oder Wasserenergie. Viele Softwarekategorien sind im Asset Intelligence-Katalog vordefiniert. Sie können benutzerdefinierte Kategorien erstellen, um die inventarisierte Software zusätzlich zu definieren. Der Überprüfungszustand aller vordefinierten Softwarekategorien lautet immer **Überprüft**. Dem Asset Intelligence-Katalog hinzugefügte benutzerdefinierte Softwarekategorieinformationen werden als **Benutzerdefiniert** angegeben. 

Weitere Informationen zum Verwalten von Softwarekategorien finden Sie unter [Konfigurieren von Asset Intelligence](configuring-asset-intelligence.md).  

> [!NOTE]  
> Die im Asset Intelligence-Katalog gespeicherten vordefinierten Softwarekategorieinformationen sind schreibgeschützt. Sie können nicht geändert oder gelöscht werden. Administratoren können benutzerdefinierte Softwarekategorien hinzufügen, ändern und löschen.  


### <a name="software-families"></a><a name="BKMK_SoftwareFamilies"></a> Softwarefamilien  

Mithilfe von Asset Intelligence-Softwarefamilien werden inventarisierte Softwaretitel innerhalb von Softwarekategorien definiert. Viele Softwarefamilien sind im Asset Intelligence-Katalog vordefiniert. Sie können benutzerdefinierte Kategorien erstellen, um die inventarisierte Software zusätzlich zu definieren. Der Überprüfungszustand aller vordefinierten Softwarefamilien lautet immer **Überprüft**. Dem Asset Intelligence-Katalog hinzugefügte benutzerdefinierte Softwarefamilieninformationen werden als **Benutzerdefiniert** angegeben. 

Weitere Informationen zum Verwalten von Softwarefamilien finden Sie unter [Konfigurieren von Asset Intelligence](configuring-asset-intelligence.md).  

> [!NOTE]  
> Vordefinierte Softwarefamilieninformationen sind schreibgeschützt und können nicht geändert werden. Administratoren können benutzerdefinierte Softwarefamilien hinzufügen, ändern und löschen.  


### <a name="software-labels"></a><a name="BKMK_CustomLabels"></a> Softwarebezeichnungen  

Mit benutzerdefinierten Asset Intelligence-Softwarebezeichnungen können Sie Filter zum Gruppieren von Softwaretiteln und zum Anzeigen der Softwaretitel in Asset Intelligence-Berichten erstellen. Verwenden Sie Softwarebezeichnungen, um benutzerdefinierte Gruppen von Softwaretiteln zu erstellen, die ein gemeinsames Attribut aufweisen. Beispielsweise können Sie die Softwarebezeichnung „Shareware“ erstellen, sie den inventarisierten Sharewaretiteln zuordnen und dann einen Bericht ausführen, in dem alle Softwaretitel mit dieser Bezeichnung angezeigt werden. Es sind keine vordefinierten Bezeichnungen verfügbar. Der Überprüfungszustand für Softwarebezeichnungen ist immer **Benutzerdefiniert**. 

Weitere Informationen zum Verwalten von Softwarebezeichnungen finden Sie unter [Konfigurieren von Asset Intelligence](configuring-asset-intelligence.md).  


### <a name="hardware-requirements"></a><a name="BKMK_HardwareRequirements"></a> Hardwareanforderungen  

Mithilfe der Hardwareanforderungsinformationen können Sie überprüfen, ob Computer die Hardwareanforderungen für Softwaretitel erfüllen, bevor auf ihnen Softwarebereitstellungen erfolgen. Hardwareanforderungen für Softwaretitel werden im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **Hardwareanforderungen** unter dem Knoten **Asset Intelligence** verwaltet. 

Viele Hardwareanforderungen sind im Asset Intelligence-Katalog vordefiniert. Erstellen Sie neue benutzerdefinierte Hardwareanforderungsinformationen, um benutzerdefinierte Anforderungen zu erfüllen. Der Überprüfungszustand aller vordefinierten Hardwareanforderungen lautet immer **Überprüft**. Dem Asset Intelligence-Katalog hinzugefügte benutzerdefinierte Hardwareanforderungsinformationen werden als **Benutzerdefiniert** angegeben. 

Weitere Informationen zum Verwalten von Hardwareanforderungen finden Sie unter [Konfigurieren von Asset Intelligence](configuring-asset-intelligence.md).  

> [!NOTE]  
> Die in der Configuration Manager-Konsole angezeigten Hardwareanforderungen werden vom Asset Intelligence-Katalog abgerufen. Sie basieren nicht auf inventarisierten Softwaretitelinformationen von Clients. 
> 
> Die Hardwareanforderungsinformationen werden nicht im Rahmen der Synchronisierung mit Microsoft aktualisiert. 
> 
> Sie können benutzerdefinierte Hardwareanforderungen für inventarisierte Software erstellen, der keine Hardwareanforderungen zugeordnet sind.  

In der Standardeinstellung werden für jede aufgeführte Hardwareanforderung die folgenden Informationen angezeigt:  

- **Softwaretitel**: Der einer Hardwareanforderung zugeordnete Softwaretitel  

- **Mindesttaktfrequenz der CPU (MHz)** : Die für den Softwaretitel erforderliche Mindestprozessorgeschwindigkeit in Megahertz (MHz)  

- **Mindestgröße des RAM (KB)** : Die für den Softwaretitel erforderliche Mindestgröße des Arbeitsspeichers in Kilobyte (KB)  

- **Mindestspeicherplatz auf dem Datenträger (KB)** : Der für den Softwaretitel erforderliche freie Mindestspeicherplatz auf dem Datenträger in KB  

- **Mindestgröße des Datenträgers (KB)** : Die für den Softwaretitel erforderliche Mindestgröße der Festplatte in KB  

- **Überprüfungszustand**: Der Überprüfungszustand für die Hardwareanforderung  

Im Asset Intelligence-Katalog gespeicherte vordefinierte Hardwareanforderungen sind schreibgeschützt und können nicht gelöscht werden. Administratoren können benutzerdefinierte Hardwareanforderungen für Softwaretitel hinzufügen, ändern und löschen, die nicht im Asset Intelligence-Katalog gespeichert sind.  



## <a name="inventoried-software-titles"></a><a name="BKMK_InventoriedSoftwareTitles"></a> Inventarisierte Softwaretitel  

Wenn Sie in der Configuration Manager-Konsole inventarisierte Softwaretitelinformationen anzeigen möchten, wechseln Sie zum Arbeitsbereich **Bestand und Kompatibilität**, erweitern Sie den Knoten **Asset Intelligence**, und wählen Sie dann den Knoten **Inventarisierte Software** aus. Der Hardwareinventur-Agent erfasst die inventarisierten Softwareinformationen von Configuration Manager-Clients basierend auf den im Asset Intelligence-Katalog gespeicherten Softwaretiteln.  

> [!Note]  
> Der Hardwareinventur-Agent erfasst die Inventardaten basierend auf den von Ihnen aktivierten Berichtsklassen der Asset Intelligence-Hardwareinventur. Weitere Informationen zum Aktivieren der Berichtsklassen finden Sie unter [Konfigurieren von Asset Intelligence](configuring-asset-intelligence.md).  

In der Standardeinstellung werden für jeden inventarisierten Softwaretitel die folgenden Informationen angezeigt:  

- **Name:** der Name des inventarisierten Softwaretitels.  

- **Hersteller:** Der Name des Herstellers, der den inventarisierten Softwaretitel entwickelt hat  

- **Version:** die Produktversion des inventarisierten Softwaretitels.  

- **Kategorie**: Die dem inventarisierten Softwaretitel aktuell zugewiesene Softwarekategorie  

- **Familie**: Die dem inventarisierten Softwaretitel aktuell zugewiesene Softwarefamilie  

- **Bezeichnung** [**1**, **2** und **3**]: Die dem Softwaretitel zugeordneten benutzerdefinierten Bezeichnungen. Inventarisierten Softwaretiteln können bis zu drei benutzerdefinierte Bezeichnungen zugeordnet sein.  

- **Anzahl**: Die Anzahl der Configuration Manager-Clients, bei denen der Softwaretitel inventarisiert ist  

- **Zustand**: Der Überprüfungszustand für den inventarisierten Softwaretitel  

> [!NOTE]  
> Sie können die Kategorisierungsinformationen für inventarisierte Software nur am Standort der obersten Ebene Ihrer Hierarchie ändern. Diese Informationen umfassen Folgendes: Produktname, Hersteller, Softwarekategorie und Softwarefamilie. Wenn Kategorisierungsinformationen für vordefinierte Software geändert werden, wird der Überprüfungszustand für die Software von **Überprüft** auf **Benutzerdefiniert**geändert.  



## <a name="asset-intelligence-synchronization-point"></a><a name="AssetIntelligenceSycnronizationPoint"></a> Asset Intelligence-Synchronisierungspunkt  

Der Asset Intelligence-Synchronisierungspunkt ist eine Configuration Manager-Standortsystemrolle. Diese Rolle wird verwendet, um über TCP-Port 443 eine Verbindung mit der Microsoft Cloud herzustellen und dynamische Updates von Kataloginformationen zu verwalten. Installieren Sie diese Standortrolle nur am Standort der obersten Ebene der Hierarchie. Konfigurieren Sie alle Asset Intelligence-Kataloganpassungen unter Verwendung einer mit dem Standort der obersten Ebene verbundenen Configuration Manager-Konsole. 

Während Sie alle Updates am Standort obersten Ebene konfigurieren, werden die Kataloginformationen an andere Standorte in der Hierarchie repliziert. Mit dieser Standortrolle können Sie eine bedarfsgesteuerte Katalogsynchronisierung mit Microsoft anfordern oder eine automatische Katalogsynchronisierung planen. Zusätzlich zum Herunterladen neuer Kataloginformationen kann der Asset Intelligence-Synchronisierungspunkt Informationen zu benutzerdefinierten Softwaretiteln zur Kategorisierung an Microsoft senden (hochladen). Microsoft behandelt alle hochgeladenen Softwaretitel als öffentliche Informationen. Stellen Sie sicher, dass Ihre benutzerdefinierten Softwaretitel keine vertraulichen oder proprietären Informationen enthalten.  

Ein von Ihnen übermittelter nicht kategorisierter Softwaretitel wird von Microsoft erst überprüft, wenn mindestens vier Kategorisierungsanforderungen von Kunden für diesen Softwaretitel vorliegen. Dann identifizieren und kategorisieren Microsoft-Forscher den Softwaretitel und stellen die Softwaretitel-Kategorisierungsinformationen allen Kunden zur Verfügung, die den Onlinedienst nutzen. Die Softwaretitel, für die die meisten Kategorisierungsanforderungen vorliegen, werden bei der Kategorisierung am höchsten priorisiert. Benutzerdefinierte Software und Branchenanwendungen erhalten in der Regel keine Kategorie. Senden Sie diese Softwaretitel daher nicht zur Kategorisierung an Microsoft.  

Zum Herstellen einer Verbindung mit der Microsoft Cloud ist ein Asset Intelligence-Synchronisierungspunkt erforderlich. Informationen zum Installieren dieser Rolle finden Sie unter [Konfigurieren von Asset Intelligence](configuring-asset-intelligence.md).  



## <a name="asset-intelligence-home-page"></a><a name="BKMK_AssetIntelligenceHomePage"></a> Asset Intelligence-Startseite  

Der Knoten **Asset Intelligence** im Arbeitsbereich **Bestand und Kompatibilität** dient als Startseite für Asset Intelligence in Configuration Manager. Auf dieser Startseite wird eine Dashboardansicht mit einer Zusammenfassung von Asset Intelligence-Kataloginformationen angezeigt.  

> [!NOTE]  
> Die **Asset Intelligence**-Startseite wird während der Anzeige nicht automatisch aktualisiert.  

Die **Asset Intelligence**-Startseite umfasst die folgenden Abschnitte:  

- **Katalogsynchronisierung**: Dieser Abschnitt enthält Informationen darüber, ob Asset Intelligence aktiviert ist, und zeigt den aktuellen Status des Asset Intelligence-Synchronisierungspunkts an.  

    > [!NOTE]  
    > Auf der Startseite wird dieser Abschnitt nur angezeigt, wenn ein Asset Intelligence-Synchronisierungspunkt installiert wurde.  

    Darüber hinaus enthält dieser Abschnitt die folgenden Informationen:  

    - Synchronisierungszeitplan  

    - Ob Sie eine Kundenlizenzübersicht importiert haben   

    - Die letzte Statusaktualisierung  

    - Den Zeitpunkt des nächsten geplanten Updates  

    - Die Anzahl der nach der Installation des Asset Intelligence-Synchronisierungspunkts vorgenommenen Änderungen   

- **Status für inventarisierte Software**: Dieser Abschnitt enthält die Anzahl und den Prozentsatz inventarisierter Software, Softwarekategorien und Softwarefamilien, die von Microsoft oder einem Administrator identifiziert wurden, deren Onlineidentifikation aussteht oder die nicht identifiziert sind und deren Onlineidentifikation nicht ausstehend ist. Die Informationen im Tabellenformat repräsentieren die jeweilige Anzahl, die Informationen im Diagramm den jeweiligen Prozentsatz.  



## <a name="asset-intelligence-reports"></a><a name="BKMK_AssetIntelligenceReports"></a> Asset Intelligence-Berichte  

Die Asset Intelligence-Berichte befinden sich in der Configuration Manager-Konsole im Arbeitsbereich **Überwachung** im Ordner **Asset Intelligence** im Knoten **Berichterstattung**. Die Berichte enthalten Informationen zu Hardware, Lizenzverwaltung und Software. Weitere Informationen zu Berichten in Configuration Manager finden Sie unter [Einführung in die Berichterstellung](../../../servers/manage/introduction-to-reporting.md).  

> [!NOTE]  
> Die Genauigkeit der Anzahl der installierten Softwaretitel und der Lizenzinformationen in den Asset Intelligence-Berichten kann von der tatsächlichen Anzahl der installierten Softwaretitel oder den in der Umgebung verwendeten Lizenzen abweichen. Diese Variation ist auf die komplexen Abhängigkeiten und Einschränkungen bei der Inventarisierung von Softwarelizenzinformationen für Softwaretitel zurückzuführen, die in Unternehmensumgebungen installiert sind. Verlassen Sie sich bei der Bestimmung der Konformität der erworbenen Softwarelizenzen nicht ausschließlich auf die Asset Intelligence-Berichte.  


### <a name="hardware-reports"></a><a name="BKMK_HardwareReports"></a> Hardwareberichte  

Asset Intelligence-Hardwareberichte enthalten Informationen zum Hardwarebestand in der Organisation. Auf der Basis von Informationen zum Hardwareinventar (wie Geschwindigkeit, Arbeitsspeicher und Peripheriegeräte) können in Asset Intelligence-Hardwareberichten Informationen zu USB-Geräten, zu upgradebedürftiger Hardware und sogar zu Computern, die für ein bestimmtes Softwareupgrade nicht bereit sind, angezeigt werden.  

> [!NOTE]  
> Einige Benutzerdaten in den Asset Intelligence-Hardwareberichten stammen aus dem Windows-Sicherheitsereignisprotokoll. Löschen Sie dieses Protokoll, wenn Sie einen Computer einem neuen Benutzer zuweisen, um die Genauigkeit der Berichte zu erhöhen.  


### <a name="license-management-reports"></a><a name="BKMK_LicenseManagementReports"></a> Lizenzverwaltungsberichte  

Asset Intelligence-Lizenzverwaltungsberichte enthalten Daten über die verwendeten Lizenzen. Im **Lizenzregisterbericht** werden die installierten Microsoft-Anwendungen in einem Format aufgelistet, das dem einer Microsoft-Lizenzübersicht (Microsoft License Statement, MLS) entspricht. Dieses Format bietet eine praktische Methode zur Abstimmung neu erworbener und bereits verwendeter Lizenzen. Andere Lizenzverwaltungsberichte enthalten Informationen zu Computern, die als Server zum Ausführen des Schlüsselverwaltungsdiensts (Key Management Service, KMS) für Windows-Aktivierungsstatistiken fungieren.  

> [!IMPORTANT]  
> Einige der Asset Intelligence-Lizenzverwaltungsberichte enthalten Informationen zur Funktion des KMS, einer Methode zum Verwalten der Volumenlizenzierung. Wenn Sie keinen KMS-Server implementiert haben, werden von einigen Berichten möglicherweise keine Daten zurückgegeben.  


### <a name="software-reports"></a><a name="BKMK_SoftwareReports"></a> Softwareberichte  

Asset Intelligence-Softwareberichte enthalten Informationen zu Softwarefamilien, Softwarekategorien und bestimmten Softwaretiteln, die auf Computern in der Organisation installiert sind. Die Softwareberichte enthalten Informationen wie Browserhilfsobjekte und Software, die automatisch gestartet wird. Diese Berichte können zum Identifizieren von Adware, Spyware und anderer Schadsoftware verwendet werden. Sie können diese Berichte auch zum Identifizieren von Softwareredundanz verwenden, um den Erwerb und die Unterstützung von Software zu optimieren.  


### <a name="software-identification-tag-reports"></a><a name="BKMK_SoftwareIdTagReports"></a> Berichte zu Softwarerkennungstags  

Berichte zu Asset Intelligence-Softwarerkennungstags bieten Informationen zu Software, die ein mit ISO/IEC 19770-2 konformes Softwarekennungstag enthält. Die Softwarekennungstags bieten Autorisierungsinformationen, mit denen die installierte Software identifiziert wird. Wenn Sie die Hardwareinventur-Berichterstellungsklasse **SMS_SoftwareTag** aktivieren, erfasst Configuration Manager Informationen zu Software mit Softwareerkennungstags. 

Die folgenden Berichte stellen Informationen zur Software bereit:  

- **Software 14A – Suche nach softwareerkennungstagfähiger Software**: Die Anzahl der installierten Software mit aktiviertem Softwareerkennungstag  

- **Software 14B – Computer, auf denen eine bestimmte softwareerkennungstagfähige Software installiert ist**: Alle Computer, auf denen Software mit einem bestimmten aktivierten Softwareerkennungstag installiert ist  

- **Software 14C – Installierte softwareerkennungstagfähige Software auf einem bestimmten Computer**: Sämtliche auf einem bestimmten Computer installierte Software mit einem bestimmten aktivierten Softwareerkennungstag  


### <a name="reporting-limitations"></a><a name="BKMK_ReportingLImitations"></a> Einschränkungen bei der Berichterstellung  

Asset Intelligence-Berichte können große Mengen an Informationen zu installierten Softwaretiteln sowie erworbenen und verwendeten Softwarelizenzen enthalten. Verwenden Sie diese Informationen bei der Bestimmung der Konformität der erworbenen Softwarelizenzen nicht als einzige Quelle.  

#### <a name="example-dependencies"></a><a name="BKMK_ExampleDependencies"></a> Beispielabhängigkeiten  
Die Genauigkeit der Anzahl der installierten Softwaretitel und der Lizenzinformationen in den Asset Intelligence-Berichten kann von der tatsächlichen, aktuell verwendeten Anzahl abweichen. Diese Variation ist auf die komplexen Abhängigkeiten bei der Inventarisierung von Softwarelizenzinformationen für Softwaretitel zurückzuführen, die in Unternehmensumgebungen verwendet werden. Im Folgenden finden Sie Beispiele für Abhängigkeiten, die bei der Inventur installierter Software im Unternehmen unter Verwendung von Asset Intelligence auftreten und die Genauigkeit von Asset Intelligence-Berichten beeinflussen können:  

- **Abhängigkeiten bezüglich der Clienthardwareinventur**: Asset Intelligence-Berichte zu installierter Software basieren auf Daten, die von Configuration Manager-Clients durch die Erweiterung der Hardwareinventur zum Aktivieren der Asset Intelligence-Berichterstellung erfasst wurden. Aufgrund dieser Abhängigkeit von der Hardwareinventurberichterstellung werden in Asset Intelligence-Berichten nur Daten von Clients angegeben, deren Hardwareinventurprozesse erfolgreich mit den erforderlichen aktivierten Asset Intelligence-WMI-Berichtsklassen abgeschlossen wurden. Da Configuration Manager-Clients Hardwareinventurprozesse nach einem vom Administrator definierten Zeitplan ausführen, kann es bei der Datenberichterstellung zu einer Verzögerung mit Einfluss auf die Genauigkeit von Asset Intelligence-Berichten kommen. 

    Beispielsweise kann ein inventarisierter lizenzierter Softwaretitel deinstalliert werden, nachdem der Client einen erfolgreichen Hardwareinventurzyklus abgeschlossen hat. In Asset Intelligence-Berichten wird der Softwaretitel bis zum nächsten geplanten Hardwareinventur-Berichtszyklus des Clients als installiert angezeigt.  

- **Abhängigkeiten bezüglich der Softwarepakete**: Asset Intelligence-Berichte basieren auf Daten zu installierten Softwaretiteln, die mithilfe von standardmäßigen Hardwareinventurprozessen der Configuration Manager-Clients erfasst werden. Einige Softwaretiteldaten werden möglicherweise nicht richtig erfasst. Ungenauigkeiten in Asset Intelligence-Berichten können beispielsweise durch Folgendes verursacht werden:  

    - Softwareinstallationen, die nicht den Standardinstallationsprozessen entsprechen  

    - Softwareinstallationen, die vor der Installation geändert wurden   

#### <a name="legal-limitations"></a><a name="BKMK_LegalLimitations"></a> Rechtliche Einschränkungen  
Die in Asset Intelligence-Berichten angezeigten Informationen unterliegen vielen Einschränkungen. Die darin angezeigten Informationen dürfen nicht als rechtlicher, buchhaltungstechnischer oder professioneller Rat angesehen werden. Die in Asset Intelligence-Berichten bereitgestellten Informationen dienen lediglich Informationszwecken. Verwenden Sie diese Informationen bei der Bestimmung der Konformität der Softwarelizenzverwendung nicht als einzige Quelle.  

Im Folgenden finden Sie Beispiele für Einschränkungen, die bei der Verwendung von Asset Intelligence auftreten und die Genauigkeit der Berichte beeinträchtigen können:  

- **Einschränkungen bezüglich der Anzahl der verwendeten Microsoft-Lizenzen**:  

    - Die Anzahl der erworbenen Microsoft-Softwarelizenzen basiert auf den von Administratoren zur Verfügung gestellten Informationen. Überprüfen Sie diese sorgfältig, um sicherzustellen, dass die richtige Anzahl von Softwarelizenzen angegeben wird.  

    - Die gemeldete Anzahl der Microsoft-Softwarelizenzen umfasst nur Informationen zu Microsoft-Softwarelizenzen, die über Volumenlizenzierungsprogramme erworben wurden. Informationen zu im Einzelhandel, über OEMs oder andere Vertriebskanäle für Softwarelizenzen erworbenen Lizenzen werden nicht widergespiegelt.  

    - In den letzten 45 Tagen erworbene Softwarelizenzen sind in der gemeldeten Anzahl der Microsoft-Softwarelizenzen möglicherweise aufgrund der Anforderungen und Zeitpläne für die Berichterstellung durch Softwarehändler nicht inbegriffen.  

    - Übertragungen von Softwarelizenzen nach Unternehmenszusammenschlüssen oder -akquisitionen sind in der Anzahl der Microsoft-Softwarelizenzen ggf. nicht enthalten.  

    - Sonderbedingungen in Microsoft-Volumenlizenzierungsvereinbarungen haben möglicherweise Einfluss auf die Anzahl der gemeldeten Softwarelizenzen. Sie erfordern möglicherweise eine zusätzliche Überprüfung durch einen zuständigen Microsoft-Mitarbeiter.  

- **Einschränkungen bezüglich der Anzahl der installierten Softwaretitel**: Configuration Manager-Clients müssen die Hardwareinventur-Berichtszyklen erfolgreich abschließen, damit die Anzahl der installierten Softwaretitel in den Asset Intelligence-Berichten korrekt wiedergegeben wird. Nach einem erfolgreichen Hardwareinventur-Berichtszyklus kann es zwischen der Installation oder Deinstallation eines lizenzierten Softwaretitels zu einer Verzögerung kommen. Diese Aktion wird in Asset Intelligence-Berichten, die ausgeführt wurden, bevor der Client die nächste geplante Hardwareinventur meldet, möglicherweise nicht berücksichtigt.  

- **Einschränkungen bezüglich des Lizenzabgleichs**: Der Abgleich der Anzahl der installierten Softwaretitel mit der Anzahl der erworbenen Softwarelizenzen wird durch einen Vergleich der vom Administrator angegebenen Anzahl von Lizenzen und der Anzahl der installierten Softwaretitel berechnet, die durch Hardwareinventuren der Configuration Manager-Clients auf Grundlage des vom Administrator festgelegten Zeitplans erfasst wurden. Dieser Vergleich stellt keine endgültige Entscheidung zu Lizenzpositionen von Microsoft dar. Die tatsächliche Lizenzposition ist von der bestimmten Softwaretitellizenz sowie den durch die Lizenzbedingungen gewährten Verwendungsrechten abhängig.  



## <a name="asset-intelligence-validation-states"></a><a name="BKMK_ValidationStates"></a> Asset Intelligence-Überprüfungszustände  

Die Asset Intelligence-Überprüfungszustände geben den Quell- und den aktuellen Überprüfungsstatus von Asset Intelligence-Kataloginformationen an. In der folgenden Tabelle werden mögliche Asset Intelligence-Überprüfungszustände und Administratoraktionen, durch die sie verursacht werden können, angezeigt.  

| Zustand | Definition | Administratoraktion | Kommentar |  
|---------------|--------------------|------------------------------|-----------------|  
|**Überprüft**|Das Katalogelement wurde von Microsoft-Forschern definiert.|Keine|Der optimale Zustand|  
|**Benutzerdefiniert**|Das Katalogelement wurde nicht von Microsoft-Forschern definiert.|Anpassen der lokalen Kataloginformationen|Dieser Zustand wird in Asset Intelligence-Berichten angezeigt.|  
|**Ausstehend**|Das Katalogelement wurde nicht von Microsoft-Forschern definiert, aber Sie haben das Element zur Kategorisierung an Microsoft übermittelt.|Keine weitere Aktion nach dem Anfordern der Kategorisierung|Das Katalogelement bleibt in diesem Zustand, bis Microsoft-Forscher das Element kategorisieren und Sie Ihren Asset Intelligence-Katalog synchronisieren.|  
|**Aktualisierbar**|Ein benutzerdefiniertes Katalogelement wurde während der Katalogsynchronisierung von Microsoft anders kategorisiert.|Mit der Aktion **Konflikt beheben** können Sie entscheiden, ob die neuen Kategorisierungsinformationen oder der vorherige benutzerdefinierte Wert verwendet werden soll(en). Weitere Informationen zum Lösen von Konflikten finden Sie unter [Vorgänge für Asset Intelligence](operations-for-asset-intelligence.md).|Nachdem Sie einen Kategorisierungskonflikt gelöst haben, wird das Element nicht mehr als in Konflikt stehend überprüft, es sei denn, es werden durch nachfolgende Kategorisierungsaktualisierungen neue Informationen über das Element hinzugefügt.|  
|**Nicht kategorisiert**|Das Katalogelement wurde weder von Microsoft-Forschern definiert noch zur Kategorisierung an Microsoft übermittelt, und der Administrator hat dem Element keinen benutzerdefinierten Kategorisierungswert zugewiesen.|Fordern Sie die Kategorisierung an, oder passen Sie Ihre lokalen Kataloginformationen an. Weitere Informationen finden Sie unter [Vorgänge für Asset Intelligence](operations-for-asset-intelligence.md).|Keine|  

> [!NOTE]  
> Katalogelemente, die Sie zur Kategorisierung an Microsoft übermitteln, weisen zwar am Standort der zentralen Verwaltung den Überprüfungszustand **Ausstehend** auf, werden jedoch an untergeordneten primären Standorten weiterhin mit dem Überprüfungszustand **Nicht kategorisiert** angezeigt.  

Beispiele für das Szenario eines möglichen Übergangs von einem Überprüfungszustand in einen anderen finden Sie unter [Beispiel-Überprüfungszustandsübergänge für Asset Intelligence](example-validation-state-transitions-for-asset-intelligence.md).  
