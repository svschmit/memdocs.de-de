---
title: Data Warehouse
titleSuffix: Configuration Manager
description: Der Data Warehouse-Dienstpunkt und die Data Warehouse-Datenbank für Configuration Manager
ms.date: 05/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aaf43e69-68b4-469a-ad58-9b66deb29057
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: abe6b05d24955959e1d08defc2c5054c4499d756
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075590"
---
#  <a name="the-data-warehouse-service-point-for-configuration-manager"></a>Der Data Warehouse-Dienstpunkt für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

<!--1277922-->
Verwenden Sie den Data Warehouse-Dienstpunkt, um langfristige Verlaufsdaten zur Bereitstellung für Configuration Manager zu speichern und hierfür Berichte zu erstellen.

> [!Note]  
> In Version 1910 wird dieses Feature standardmäßig von Configuration Manager aktiviert. In Version 1906 oder früher aktiviert Configuration Manager dieses optionale Feature nicht automatisch. Sie müssen dieses Feature aktivieren, bevor Sie es verwenden. Weitere Informationen finden Sie unter [Enable optional features from updates (Aktivieren optionaler Features von Updates)](install-in-console-updates.md#bkmk_options).<!--505213-->  


Das Data Warehouse unterstützt ein Datenvolumen von bis zu 2 TB, inklusive der Zeitstempel für Änderungsnachverfolgung. Das Data Warehouse speichert die Daten durch die automatisierte Synchronisierung der Configuration Manager-Standortdatenbank mit der Data Warehouse-Datenbank. Auf diese Informationen kann dann über den Reporting Services-Punkt aus zugegriffen werden. Daten, die mit der Data Warehouse-Datenbank synchronisiert werden, werden drei Jahre lang gespeichert. Daten, die älter als drei Jahre sind, werden in regelmäßigen Abständen über einen integrierten Task entfernt.

Zu synchronisierten Daten zählen folgende Gruppen von globalen und Standortdaten:
- Infrastrukturintegrität
- Sicherheit
- Konformität
- Malware   
- Softwarebereitstellungen
- Inventurdetails (der Inventurverlauf wird allerdings nicht synchronisiert)

Bei der Installation der Standortsystemrolle wird auch die Data Warehouse-Datenbank installiert und konfiguriert. Außerdem werden mehrere Berichte installiert, damit Sie leicht nach diesen Daten suchen und über diese berichten können.

Ab Version 1810 können Sie mehr Tabellen aus der Standortdatenbank mit dem Data Warehouse synchronisieren. Diese Änderung ermöglicht es Ihnen, mehr Berichte basierend auf Ihren geschäftlichen Anforderungen zu erstellen.<!--1358870--> 



## <a name="prerequisites"></a>Voraussetzungen

- Die Data Warehouse-Standortsystemrolle wird nur am Standort auf der obersten Ebene der Hierarchie unterstützt. Dabei handelt es sich z. B. um einen zentralen Verwaltungsstandort oder einen eigenständigen primären Standort.  

- Der Computer, auf dem die Standortsystemrolle installiert ist, erfordert .NET Framework 4.5.2 oder höher.  

- Geben Sie dem **Konto des Reporting Services-Punkts** die Berechtigung **db_datareader** für die Data Warehouse-Datenbank.  

- Configuration Manager verwendet das Computerkonto der Standortsystemrolle, um Daten mit der Data Warehouse-Datenbank zu synchronisieren. Für dieses Konto sind folgende Berechtigungen erforderlich:  

    - Ein **Administrator** auf dem Computer, auf dem die Data Warehouse-Datenbank gehostet wird.  

    - Die Berechtigung **DB_Creator** in der Data Warehouse-Datenbank.  

    - **DB_owner** oder **DB_reader** mit der Berechtigung **Ausführen** für die Standortdatenbank auf oberster Ebene.  

- Für die Data Warehouse-Datenbank wird SQL Server 2012 oder neuer benötigt. Sie können die Editionen Standard, Enterprise oder Datacenter verwenden. Die SQL Server-Version für das Data Warehouse muss nicht dem Standortdatenbankserver entsprechen.<!--SCCMDocs issue 662-->  

- Die Data Warehouse-Datenbank unterstützt die folgenden SQL Server-Konfigurationen:  

    - Eine Standardinstanz oder eine benannte Instanz  

    - SQL Server Always On-Verfügbarkeitsgruppe  

    - SQL Server-Failovercluster  

- Bei Verwendung von [verteilten Ansichten](../../plan-design/hierarchy/database-replication.md#bkmk_distviews) muss der Data Warehouse-Dienstpunkt auf dem Server installiert sein, auf dem die Datenbank des Standorts der zentralen Verwaltung gehostet wird.  

Weitere Informationen zur SQL Server-Lizenzierung finden Sie unter [Häufig gestellte Fragen zum Produkt und zur Lizenzierung](../../understand/product-and-licensing-faq.md). <!-- sms500967 -->

Achten Sie darauf, dass die Data Warehouse-Datenbank und die Standortdatenbank gleich groß sind. Das Data Warehouse ist zwar zu Beginn kleiner, wird aber mit der Zeit immer größer. <!--SCCMDocs issue 756-->



## <a name="install"></a>Installation

Jede Hierarchie unterstützt auf jedem Standortsystem des obersten Standorts eine einzelne Instanz dieser Rolle. Der SQL Server, der die Datenbank für Warehouse hostet, kann für die Standortsystemrolle sowohl lokal als auch remote sein. Das Data Warehouse arbeitet mit dem Reporting Services-Punkt, der am gleichen Standort installiert ist. Die Installation der zwei Standortsystemrollen auf demselben Server ist nicht erforderlich.   

Um die Rolle zu installieren, verwenden Sie den **Assistent zum Hinzufügen von Standortsystemrollen** oder den **Assistent zum Erstellen von Standortsystemservern**. Weitere Informationen finden Sie unter [Installieren von Standortsystemrollen](../deploy/configure/install-site-system-roles.md). Wählen Sie im Assistenten auf der Seite **Systemrollenauswahl** die Rolle **Data Warehouse-Dienstpunkt** aus. 

Bei der Installation einer Rolle erstellt Configuration Manager die Data Warehouse-Datenbank auf der von Ihnen bestimmten Instanz von SQL Server für Sie. Wenn Sie den Namen einer bereits vorhandenen Datenbank angeben, erstellt Configuration Manager keine neue Datenbank. Stattdessen wird die von Ihnen angegebene Datenbank verwendet. Es handelt sich dabei um den gleichen Prozess wie beim [Verschieben der Data Warehouse-Datenbank auf einen neuen Server mit SQL Server](#move-the-database).


### <a name="configure-properties"></a>Konfigurieren von Eigenschaften

#### <a name="general-page"></a>Seite „Allgemein“

- **Vollqualifizierter SQL Server-Domänenname**: Geben Sie den FQDN des Servers an, der den Data Warehouse-Dienstpunkt hostet.  

- **SQL Server-Instanzname (falls zutreffend)** : Wenn Sie keine Standardinstanz des SQL Servers verwenden, geben Sie die benannte Instanz an.  

- **Datenbankname**: Legen Sie einen Namen für die Data Warehouse-Datenbank fest. Configuration Manager erstellt die Data Warehouse-Datenbank mit diesem Namen. Wenn ein Datenbankname angegeben wird, der bereits in der Instanz von SQL Server existiert, verwendet Configuration Manager diese Datenbank.  

- **Verwendeter SQL Server-Port für die Verbindung**: Geben Sie die TCP/IP-Portnummer an, die vom SQL Server verwendet wird, der die Data Warehouse-Datenbank hostet. Der Data Warehouse-Synchronisierungsdienst verwendet diesen Port, um eine Verbindung mit der Data Warehouse-Datenbank herzustellen. Standardmäßig wird der SQL Server-Port **1433** für die Kommunikation verwendet.  

- **Konto für Data Warehouse-Dienstpunkt**: Ab Version 1802 legen Sie den **Benutzernamen** fest, der von SQL Server Reporting Services beim Herstellen einer Verbindung mit der Data Warehouse-Datenbank verwendet wird.  


#### <a name="synchronization-schedule-page"></a>Die Seite „Synchronisierungszeitplan“
*Gilt für Version 1806 und früher*

- **Startzeit**: Geben Sie die Zeit an, zu der mit der Synchronisierung von Data Warehouse begonnen werden soll.  

- **Serienmuster**

    - **Täglich**: Legen Sie fest, dass die Synchronisierung täglich durchgeführt wird.  

    - **Wöchentlich:** Legen Sie einen Tag in der Woche fest, an dem die Synchronisierung wöchentlich durchgeführt werden soll.


#### <a name="synchronization-settings-page"></a>Die Seite „Synchronisierungseinstellungen“
*Gilt für Version 1810 und höher*

- **Benutzerdefinierte Einstellung für die Datensynchronisierung:** Wählen Sie die Option **Tabellen auswählen** aus. Wählen Sie im Fenster „Datenbanktabellen“ die Tabellennamen aus, die mit der Data Warehouse-Datenbank synchronisiert werden sollen. Verwenden Sie den Filter, um nach Namen zu suchen, oder verwenden Sie die Dropdownliste, um bestimmte Gruppen auszuwählen. Klicken Sie zum Speichern auf **OK**, wenn Sie fertig sind.  

    > [!Note]  
    > Sie können keine Tabellen entfernen, die die Rolle standardmäßig auswählt.  

- **Startzeit**: Geben Sie die Zeit an, zu der mit der Synchronisierung von Data Warehouse begonnen werden soll.  

- **Serienmuster**

    - **Täglich**: Legen Sie fest, dass die Synchronisierung täglich durchgeführt wird.  

    - **Wöchentlich:** Legen Sie einen Tag in der Woche fest, an dem die Synchronisierung wöchentlich durchgeführt werden soll.



## <a name="reporting"></a>Berichterstellung

Sobald Sie einen Data Warehouse-Dienstpunkt installieren, stehen Ihnen mehrere Berichte über den Reporting Services-Punkt zur Verfügung, der für den gleichen Standort installiert ist. Wenn Sie den Data Warehouse-Dienstpunkt vor der Installation eines Reporting Services-Punkts installieren, werden die Berichte automatisch mit der späteren Installation des Reporting Services-Punkt hinzugefügt.

> [!WARNING]  
> Ab Version 1802 unterstützt der Data Warehouse-Dienstpunkt alternative Anmeldeinformationen.<!--507334--> Wenn Sie von einer früheren Version von Configuration Manager ein Upgrade ausgeführt haben, müssen Sie Anmeldeinformationen angeben, mit denen SQL Server Reporting Services eine Verbindung mit der Data Warehouse-Datenbank herstellen kann. Die Data Warehouse-Berichte werden erst geöffnet, wenn Sie Anmeldeinformationen hinzufügen. 
> 
> Geben Sie in den Rolleneigenschaften den **Benutzernamen** für das Konto für den Data Warehouse-Dienstpunkt an, um ein Konto festzulegen. Weitere Informationen finden Sie unter [Konfigurieren von Eigenschaften](#configure-properties). 

Die Data Warehouse-Standortsystemrolle beinhaltet folgende Berichte in der Kategorie **Data Warehouse**:  

- **Anwendungsbereitstellungsbericht – Verlauf**: Anzeigen von Details zur Anwendungsbereitstellung für eine bestimmte Anwendung und einen bestimmten Computer  

- **Konformität von Endpoint Protection und Softwareupdates – Verlauf**: Anzeigen von Computern, auf denen Softwareupdates fehlen.  

- **Bestandsbericht zur gesamten Hardware – Verlauf**: Anzeigen des gesamten Hardwarebestands für einen bestimmten Computer.  

- **Bestandsbericht zur gesamten Software – Verlauf**: Anzeigen des gesamten Softwarebestands für einen bestimmten Computer.  

- **Übersicht der Infrastrukturintegrität – Verlauf**: Zeigt eine Übersicht der Integrität der Configuration Manager-Infrastruktur an.  

- **Liste der erkannten Malware – Verlauf**: Zeigt Malware an, die in der Organisation gefunden wurde.  

- **Zusammenfassungsbericht der Softwareverteilung – Verlauf**: Eine Zusammenfassung der Softwareverteilung für eine bestimmte Ankündigung und einen bestimmten Computer.  



## <a name="site-expansion"></a>Standorterweiterung

Bevor Sie einen Standort der zentralen Verwaltung installieren können, um einen vorhandenen eigenständigen primären Standort zu erweitern, müssen Sie zunächst die Rolle „Data Warehouse-Dienstpunkt“ installieren. Nach der Installation des Standorts der zentralen Verwaltung können Sie die Standortsystemrolle am Standort der zentralen Verwaltung installieren.  

Im Gegensatz zum Bewegen der Data Warehouse-Datenbank führt diese Änderung zum Verlust aller Verlaufsdaten, die vorher am primären Standort synchronisiert wurden. Eine Sicherung der Datenbank am primären Standort und eine Wiederherstellung am Standort der zentralen Verwaltung werden nicht unterstützt.



## <a name="move-the-database"></a>Verschieben der Datenbank

Führen Sie zum Verschieben der Data Warehouse-Datenbank auf einen neuen Server von SQL Server die folgenden Schritte aus:  

1. Verwenden Sie SQL Server Management Studio, um die Datawarehouse-Datenbank zu sichern. Stellen Sie dann die Datenbank in einem SQL Server auf einem Computer wieder her, auf dem das Data Warehouse gehostet wird.  

    > [!NOTE]  
    > Nachdem Sie die Datenbank auf dem neuen Server wiederhergestellt haben, stellen Sie sicher, dass die Zugriffsberechtigungen der neuen Data Warehouse-Datenbank mit denen der ursprünglichen Data Warehouse-Datenbank identisch sind.  

2. Verwenden Sie die Configuration Manager-Konsole, um den Data Warehouse-Dienstpunkt vom aktuellen Server zu entfernen.  

3. Installieren Sie den Data Warehouse-Dienstpunkt neu. Geben Sie den Namen der neuen SQL Server-Instanz und der Instanz an, die die von Ihnen wiederhergestellte Data Warehouse-Datenbank hosten.  

4. Nach der Installation der Standortsystemrolle ist der Verschiebevorgang abgeschlossen.  



## <a name="troubleshooting"></a>Problembehandlung 

### <a name="log-files"></a>Protokolldateien 

Verwenden Sie die folgenden Protokolle zur Untersuchung von Problemen bei der Installation des Data Warehouse-Dienstpunkts oder der Synchronisierung von Daten:

- **DWSSMSI.log** und **DWSSSetup.log**: Verwenden Sie diese Protokolle, um Fehler bei der Installation des Data Warehouse-Dienstpunkts zu untersuchen.  

- **Microsoft.ConfigMgrDataWarehouse.log:** Verwenden Sie dieses Protokoll, um die Datensynchronisierung zwischen der Standortdatenbank und der Data Warehouse-Datenbank zu untersuchen.  


### <a name="set-up-failure"></a>Fehler beim Setup 

Wenn die Rolle „Data Warehouse-Dienstpunkt“ die erste Rolle ist, die Sie auf einem Remoteserver installieren, schlägt die Installation für das Data Warehouse fehl.  

#### <a name="workaround"></a>Problemumgehung 
Stellen Sie sicher, das der Computer, auf dem Sie den Data Warehouse-Dienstpunkt installieren möchten, bereits mindestens eine andere Rolle hostet.  


### <a name="synchronization-failed-to-populate-schema-objects"></a>Bei der Synchronisierung ist ein Fehler aufgetreten, durch den keine Schemaobjekte aufgefüllt wurden 

Die Synchronisierung schlägt mit folgender Meldung in der **Microsoft.ConfigMgrDataWarehouse.log**-Datei fehl: `failed to populate schema objects` (Auffüllen der Schemaobjekte fehlgeschlagen)

#### <a name="workaround"></a>Problemumgehung 
Stellen Sie sicher, dass das Computerkonto der Standortsystemrolle in der Data Warehouse-Datenbank die Rolle **db_owner** aufweist.


### <a name="reports-fail-to-open"></a>Berichte können nicht geöffnet werden

Data Warehouse-Berichte können nicht geöffnet werden, wenn die Data Warehouse-Datenbank und der Reporting Services-Punkt sich auf unterschiedlichen Standortsystemen befinden.  

#### <a name="workaround"></a>Problemumgehung
Geben Sie dem **Konto des Reporting Services-Punkts** die Berechtigung **db_datareader** für die Data Warehouse-Datenbank.


### <a name="error-opening-reports"></a>Fehler beim Erstellen von Berichten

Beim Öffnen eines Data Warehouse-Berichts wird folgender Fehler zurückgegeben:

``` Output
An error has occurred during report processing. (rsProcessingAborted)
Cannot create a connection to data source 'AutoGen__39B693BB_524B_47DF_9FDB_9000C3118E82_'. (rsErrorOpeningConnection)
A connection was successfully established with the server, but then an error occurred during the pre-login handshake. (provider: SSL Provider, error: 0 - The certificate chain was issued by an authority that is not trusted.)
```

#### <a name="workaround"></a>Problemumgehung 
Führen Sie die folgenden Schritte aus, um Zertifikate zu konfigurieren:

1. Auf dem Computer, auf dem der Serverteil des Data Warehouse gehostet wird:  

    1. Öffnen Sie den IIS, klicken Sie auf **Serverzertifikate**, und klicken Sie mit der rechten Maustaste auf **Selbstsigniertes Zertifikat erstellen**. Geben Sie dann den Anzeigename für den Zertifikatnamen als **Data Warehouse SQL Server Identification Certificate** (SQL Server-Identifizierungszertifikat für Data Warehouse) an. Wählen Sie für Zertifikatspeicher **Persönlich** aus.  

    2. Öffnen Sie **SQL Server Configuration Manager**. Klicken Sie unter **SQL Server-Netzwerkkonfiguration** unter **Protocols for MSSQLSERVER** (Protokolle für MMSSQLSERVER) mit der rechten Maustaste auf **Eigenschaften**. Wechseln Sie dann zur Registerkarte **Zertifikat**, wählen Sie **Data Warehouse SQL Server Identification Certificate** (SQL Server-Identifizierungszertifikat für Data Warehouse) als Zertifikat aus, und speichern Sie dann die Änderungen.  

    3. Starten Sie im **SQL Server-Konfigurations-Manager** unter **SQL Server-Dienste** den **SQL Server-Dienst** neu. Wenn SQL Server Reporting Services ebenfalls auf dem Server installiert ist, der die Data Warehouse-Datenbank hostet, sollten Sie **Reporting Services** ebenfalls neu starten.  

    4. Öffnen Sie die Microsoft Management Console (MMC), und fügen Sie das Snap-In **Zertifikate** hinzu. Wählen Sie das **Computerkonto** des lokalen Computers aus. Erweitern Sie den Ordner **Persönlich**, und klicken Sie auf **Zertifikate**. Exportieren Sie das **Data Warehouse SQL Server Identification Certificate** (SQL Server-Identifizierungszertifikat für Data Warehouse ) als **DER-codierte binäre X.509-Datei (.CER)** .  

2. Öffnen Sie auf dem Computer, der SQL Server Reporting Services hostet, die MMC, und fügen Sie das Snap-In **Zertifikate** hinzu. Klicken Sie auf **Computerkonto**. Importieren Sie im Ordner **Als vertrauenswürdig eingestufte Stammzertifizierungsstelle** das **Data Warehouse SQL Server Identification Certificate** (Data Warehouse SQL Server-Idenfikationszertifikat).  



## <a name="data-flow"></a>Datenfluss   

![Diagramm, auf dem der logische Datenfluss zwischen den Standortkomponenten für das Data Warehouse dargestellt wird](./media/datawarehouse.png)

#### <a name="data-storage-and-synchronization"></a>Datenspeicherung und Synchronisierung

| Schritt   | Details  |
|--------|----------|  
| **1**  | Der Standortserver überträgt und speichert Daten in der Standortdatenbank. |  
| **2**  | Basierend auf Zeitplan und Konfiguration, ruft der Data Warehouse-Dienstpunkt Daten aus der Standortdatenbank ab. |  
| **3**  | Der Data Warehouse-Dienstpunkt überträgt und speichert eine Kopie der synchronisierten Daten in der Data Warehouse-Datenbank. |  


#### <a name="reporting"></a>Berichterstellung

| Schritt   | Details  |
|--------|----------|  
| **A**  | Mithilfe integrierter Berichte fordert ein Benutzer Daten an. Diese Anforderung wird mittels SQL Server Reporting Services an den Reporting Services-Punkt übertragen. |  
| **B**  | Die meisten Berichte gelten für aktuelle Informationen. Diese Anfragen werden in der Standortdatenbank ausgeführt. |  
| **C**  | Wenn ein Bericht über einen der Berichte mit der *Kategorie* **Data Warehouse** alte Daten anfordert, ist die Data Warehouse-Datenbank das Ziel der Anforderung. |  
