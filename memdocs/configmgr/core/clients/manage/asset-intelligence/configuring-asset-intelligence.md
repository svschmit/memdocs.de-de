---
title: Konfigurieren von Asset Intelligence
titleSuffix: Configuration Manager
description: Richten Sie Asset Intelligence in Configuration Manager ein.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 08e0382d-de05-4a76-ba5c-7223173f7066
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 56a65a0a4e1dd9a96e5725ea8c68cc435947bb08
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694758"
---
# <a name="configure-asset-intelligence-in-configuration-manager"></a>Konfigurieren von Asset Intelligence in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Asset Intelligence erstellt eine Inventarliste der Softwarelizenzen und überwacht ihre Verwendung.   

## <a name="steps-to-configure-asset-intelligence"></a>Schritte zum Konfigurieren von Asset Intelligence  
   

- **Schritt 1**: Zum Sammeln von Inventurdaten, die für Asset Intelligence-Berichte erforderlich sind, müssen Sie den Hardwareinventurclient-Agent aktivieren. Dies wird unter [Erweitern der Hardwareinventur](../../../../core/clients/manage/inventory/extend-hardware-inventory.md) beschrieben.
- **Schritt 2**: [Aktivieren von Asset Intelligence-Hardwareinventur-Berichtsklassen](#BKMK_EnableAssetIntelligence)  
- **Schritt 3**: [Installieren eines Asset Intelligence-Synchronisierungspunkts](#BKMK_InstallAssetIntelligenceSynchronizationPoint)
- **Schritt 4**: [Aktivieren der Überwachung erfolgreicher Anmeldeereignisse](#BKMK_EnableSuccessLogonEvents)  
- **Schritt 5**: [Importieren von Softwarelizenzinformationen](#BKMK_ImportSoftwareLicenseInformation)  
- **Schritt 6:** [Konfigurieren von Asset Intelligence-Wartungstasks](#BKMK_ConfigureMaintenanceTasks) 


###  <a name="enable-asset-intelligence-hardware-inventory-reporting-classes"></a><a name="BKMK_EnableAssetIntelligence"></a> Enable Asset Intelligence hardware inventory reporting classes  
 Zum Aktivieren von Asset Intelligence in Configuration Manager-Standorten müssen Sie mindestens eine Asset Intelligence-Hardwareinventur-Berichtsklasse aktivieren. Sie können die Klassen auf der **Asset Intelligence** -Startseite oder im Arbeitsbereich **Verwaltung** im Knoten **Clienteinstellungen** in den Eigenschaften der Clienteinstellungen aktivieren. Wenden Sie eines der folgenden Verfahren an:  

##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-the-asset-intelligence-home-page"></a>So aktivieren Sie Asset Intelligence-Hardwareinventur-Berichtsklassen von der Asset Intelligence-Startseite aus  

1.  Wählen Sie in der Configuration Manager-Konsole **Bestand und Konformität** > **Asset Intelligence** aus.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Asset Intelligence** **Inventurklassen bearbeiten** aus.   

4.  Zum Aktivieren der Asset Intelligence-Berichterstattung wählen Sie **Alle Asset Intelligence-Berichtsklassen aktivieren** oder **Nur die ausgewählten Asset Intelligence-Berichtsklassen aktivieren** und mindestens eine der angezeigten Berichtsklassen aus.  

    > [!NOTE]  
    >  In den von den Hardwareinventurklassen abhängigen Asset Intelligence-Berichten, die mit diesem Verfahren aktiviert werden, werden erst dann Daten angezeigt, wenn die Hardwareinventurdaten von den Clients überprüft und zurückgegeben wurden.  


##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-client-settings-properties"></a>So aktivieren Sie Asset Intelligence-Hardwareinventur-Berichtsklassen in den Eigenschaften der Clienteinstellungen  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Verwaltung** >  **Clienteinstellungen** > **Client-Agent-Standardeinstellungen** aus. Wenn Sie benutzerdefinierte Clienteinstellungen erstellt haben, können Sie alternativ diese auswählen.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus.   

4.  Wählen Sie **Hardwareinventur** > **Klassen festlegen** aus. .  

5.  Wählen Sie **Filter by category** (Nach Kategorie filtern) > **Asset Intelligence-Berichtsklassen** aus. In der aktualisierten Liste werden nur Asset Intelligence-Hardwareinventur-Berichtsklassen angezeigt.  

6.  Wählen Sie mindestens eine Berichtsklasse aus der Liste aus.  

    > [!NOTE]  
    >  In den von den Hardwareinventurklassen abhängigen Asset Intelligence-Berichten, die mit diesem Verfahren aktiviert werden, werden erst dann Daten angezeigt, wenn die Hardwareinventurdaten von den Clients überprüft und zurückgegeben wurden.  
  

###  <a name="install-an-asset-intelligence-synchronization-point"></a><a name="BKMK_InstallAssetIntelligenceSynchronizationPoint"></a> Install an Asset Intelligence Synchronization Point  

Die Standortsystemrolle des Asset Intelligence-Synchronisierungspunkts wird verwendet, um eine Verbindung von Configuration Manager-Standorten zu System Center Online herstellen und Asset Intelligence-Kataloginformationen synchronisieren zu können. Der Asset Intelligence-Synchronisierungspunkt kann nur auf einem Standortsystem installiert werden, das sich am Standort der obersten Ebene in der Configuration Manager-Hierarchie befindet, und erfordert für die Synchronisierung mit System Center Online über TCP-Port 443 eine Internetverbindung.

Zusätzlich zum Herunterladen neuer Asset Intelligence-Kataloginformationen können vom Asset Intelligence-Synchronisierungspunkt Informationen zu benutzerdefinierten Softwaretiteln zur Kategorisierung in System Center Online hochgeladen werden. Microsoft behandelt alle hochgeladenen Softwaretitel als öffentliche Informationen. Stellen Sie sicher, dass Ihre benutzerdefinierten Softwaretitel keine vertraulichen oder geschützten Informationen enthalten. Weitere Informationen zu Kategorisierungsanforderungen für Softwaretitel finden Sie unter [Request a catalog update for uncategorized software titles (Anfordern eines Katalogupdates für nicht kategorisierte Softwaretitel)](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_RequestCatalogUpdate).  

##### <a name="to-install-an-asset-intelligence-synchronization-point-site-system-role"></a>So installieren Sie eine Asset Intelligence-Synchronisierungspunkt-Standortsystemrolle  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Verwaltung**> **Standortkonfiguration** > **Server und Standortsystemrollen** aus.  

3.  Fügen Sie die Standortsystemrolle für den Asset Intelligence-Synchronisierungspunkt zu einem neuen oder bestehenden Standortsystemserver hinzu:  

    -  Für einen **neuen Standortsystemserver**: Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** die Option **Standortsystemserver erstellen** aus, um den Assistenten zu starten.   

        > [!NOTE]  
        >  Wenn eine Standortsystemrolle von Configuration Manager in der Standardeinstellung installiert wird, erfolgt die Installation auf dem ersten verfügbaren NTFS-formatierten Festplattenlaufwerk, das genügend Speicherplatz bietet. Soll die Installation durch Configuration Manager nicht auf einem bestimmten Laufwerk vorgenommen werden, erstellen Sie eine leere Datei mit dem Namen „No_sms_on_drive.sms“, und kopieren Sie sie in den Stammordner des Laufwerks, bevor Sie den Standortsystemserver installieren.  

    -  Für einen **bestehenden Standortsystemserver**: Wählen Sie den Server aus, auf dem die Standortsystemrolle "Asset Intelligence-Synchronisierungspunkt" installiert werden soll. Wenn Sie einen Server auswählen, wird im Detailbereich eine Liste der Standortsystemrollen angezeigt, die bereits auf dem Server installiert sind.  

         Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Server** **Add Site System Role** (Standortsystemrollen hinzufügen) aus, um den Assistenten zu starten.  

4.  Schließen Sie die Seite **Allgemein** ab. Soll der Asset Intelligence-Synchronisierungspunkt zu einem bestehenden Standortsystemserver hinzugefügt werden, überprüfen Sie die zuvor konfigurierten Werte.  

5.  Wählen Sie auf der Seite **Systemrollenauswahl** in der Liste der verfügbaren Rollen **Asset Intelligence-Synchronisierungspunkt** aus.  

6.  Wählen Sie auf der Seite **Asset Intelligence Synchronization Point Connection Settings** (Asset Intelligence-Synchronisierungspunkteinstellungen) **Weiter** aus.  

     Die Einstellung **Diesen Asset Intelligence-Synchronisierungspunkt verwenden** ist in der Standardeinstellung ausgewählt und kann auf dieser Seite nicht konfiguriert werden. Von System Center Online wird Netzwerkverkehr nur über TCP-Port 443 akzeptiert, daher können die Einstellungen für die **SSL-Portnummer** auf dieser Seite des Assistenten nicht konfiguriert werden.  

7.  Sie können optional einen Pfad zur System Center Online-Authentifizierungszertifikatdatei (.pfx) angeben. Normalerweise geben Sie keinen Pfad für das Zertifikat an, weil das Verbindungszertifikat bei der Standortrolleninstallation automatisch bereitgestellt wird.  

8.  Geben Sie auf der Seite **Proxyservereinstellungen** an, ob vom Asset Intelligence-Synchronisierungspunkt ein Proxyserver für die Verbindung mit System Center Online verwendet werden soll, um den Katalog zu synchronisieren. Geben Sie außerdem an, ob bei der Verbindung mit dem Proxyserver Anmeldeinformationen verwendet werden sollen.  

    > [!WARNING]  
    >  Wenn zur Verbindung mit System Center Online ein Proxyserver erforderlich ist, kann das Verbindungszertifikat auch dann gelöscht werden, wenn das Benutzerkontokennwort für das zur Proxyserverauthentifizierung konfigurierte Konto abläuft.  

9. Geben Sie auf der Seite **Synchronisierungszeitplan** an, ob der Asset Intelligence-Katalog nach einem Zeitplan synchronisiert werden soll. Wenn Sie den Synchronisierungszeitplan aktivieren, geben Sie einen einfachen oder einen benutzerdefinierten Synchronisierungszeitplan an. Bei der geplanten Synchronisierung wird vom Asset Intelligence-Synchronisierungspunkt eine Verbindung mit System Center Online hergestellt, um den aktuellsten Asset Intelligence-Katalog abzurufen. Sie können den Asset Intelligence-Katalog im Knoten „Asset Intelligence“ in der Configuration Manager-Konsole manuell synchronisieren. Die Schritte für die manuelle Synchronisierung des Asset Intelligence-Katalogs finden Sie im Abschnitt [So führen Sie eine manuelle Synchronisierung des Asset Intelligence-Katalogs durch](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ManuallySynchronizeCatalog) in [Vorgänge für Asset Intelligence](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md).  

10. Abschließen des Assistenten 

###  <a name="enable-auditing-of-success-logon-events"></a><a name="BKMK_EnableSuccessLogonEvents"></a> Enable auditing of success logon events  
 In vier Asset Intelligence-Berichten werden Informationen angezeigt, die aus den Windows-Sicherheitsereignisprotokollen auf den Clientcomputern zusammengestellt werden. So konfigurieren Sie Sicherheitsrichtlinien für die Anmeldeeinstellungen zur Überprüfung erfolgreicher Anmeldeereignisse.  

##### <a name="to-enable-success-logon-event-logging-by-using-a-local-security-policy"></a>So aktivieren Sie die Protokollierung von erfolgreichen Anmeldeereignissen mithilfe einer lokalen Sicherheitsrichtlinie  

1.  Wählen Sie auf einem Configuration Manager-Clientcomputer **Starten** > **Verwaltungstools** > **Lokale Sicherheitsrichtlinie** aus.  

2.  Erweitern Sie im Dialogfeld **Lokale Sicherheitsrichtlinie** unter **Sicherheitseinstellungen** **Lokale Richtlinien**, und wählen Sie **Audit Policy** (Überwachungsrichtlinie) aus.  

3.  Doppelklicken Sie im Ergebnisbereich auf **Anmeldeereignisse überwachen**, vergewissern Sie sich, dass das Kontrollkästchen **Erfolg** aktiviert ist, und wählen Sie **OK** aus.  

##### <a name="to-enable-success-logon-event-logging-by-using-an-active-directory-domain-security-policy"></a>So aktivieren Sie die Protokollierung von erfolgreichen Anmeldeereignissen mithilfe einer Active Directory-Domänensicherheitsrichtlinie  

1.  Wählen Sie auf einem Domänencontrollercomputer **Starten** aus, zeigen Sie mit der Maus auf **Verwaltungstools**, und wählen Sie **Domain Security Policy** (Sicherheitsrichtlinie für Domänen) aus.  

2.  Erweitern Sie im Dialogfeld **Lokale Sicherheitsrichtlinie** unter **Sicherheitseinstellungen** **Lokale Richtlinien**, und wählen Sie **Audit Policy** (Überwachungsrichtlinie) aus.  

3.  Doppelklicken Sie im Ergebnisbereich auf **Anmeldeereignisse überwachen**, vergewissern Sie sich, dass das Kontrollkästchen **Erfolg** aktiviert ist, und wählen Sie **OK** aus.  

###  <a name="import-software-license-information"></a><a name="BKMK_ImportSoftwareLicenseInformation"></a> Import software license information  
 In den folgenden Abschnitten werden die erforderlichen Vorgehensweisen zum Importieren von Microsoft- und allgemeinen Softwarelizenzierungsinformationen in die Configuration Manager-Standortdatenbank mithilfe des Assistenten zum Importieren von Softwarelizenzen beschrieben. Beim Importieren von Softwarelizenzinformationen aus Lizenzübersichtsdateien in die Standortdatenbank wird für das Computerkonto des Standortservers **Vollzugriff** im NTFS-Dateisystem auf die Dateifreigabe benötigt, die zum Importieren der Softwarelizenzinformationen verwendet wird.  

> [!IMPORTANT]  
>  Beim Import von Softwarelizenzinformationen in die Standortdatenbank werden vorhandene Softwarelizenzinformationen überschrieben. Vergewissern Sie sich, dass die mit dem Assistenten zum Importieren von Softwarelizenzen verwendete Datei mit Softwarelizenzinformationen eine vollständige Liste aller erforderlichen Softwarelizenzinformationen enthält.  

##### <a name="to-import-software-license-information-into-the-asset-intelligence-catalog"></a>So importieren Sie Softwarelizenzinformationen in den Asset Intelligence-Katalog  

1.  Wählen Sie im Arbeitsbereich **Bestand und Konformität** **Asset Intelligence** aus.  

2.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Asset Intelligence** **Softwarelizenzen importieren** aus.   

4.  Geben Sie auf der Seite **Importieren** an, ob eine Microsoft-Volumenlizenzierungsdatei (MVLS) (.xml oder .csv) oder eine allgemeine Lizenzzusammenfassung (.csv) importiert werden soll. Weitere Informationen zum Erstellen einer allgemeinen Lizenzübersichtsdatei finden Sie unter [Erstellen einer allgemeinen Lizenzzusammenfassungsdatei zum Import](#BKMK_CreateGeneralLicenseStatement) weiter unten in diesem Thema.  

    > [!WARNING]  
    >  Informationen zum Herunterladen einer MVLS-Datei im CSV-Format, die in den Asset Intelligence-Katalog importiert werden kann, finden Sie im [Microsoft Volume Licensing Service Center](https://go.microsoft.com/fwlink/p/?LinkId=226547). Für den Zugriff auf diese Informationen benötigen Sie ein registriertes Konto auf der Website. Wenden Sie sich an Ihren Microsoft-Kontobeauftragten, um sich zu informieren, wie Sie Ihre MVLS-Datei im XML-Format erhalten.  

5.  Geben Sie den UNC-Pfad zur Lizenzinformationsdatei ein, oder wählen Sie **Durchsuchen** aus, um einen freigegebenen Netzwerkordner und die entsprechende Datei auszuwählen.  

    > [!NOTE]  
    >  Der freigegebene Ordner muss ordnungsgemäß gesichert sein, um nicht autorisierte Zugriffe auf die Lizenzinformationsdatei zu verhindern. Außerdem muss das Computerkonto des Computers, auf dem der Assistent ausgeführt wird, Vollzugriff auf die Freigabe haben, in der sich die Lizenzimportdatei befindet.  

6. Schließen Sie den Assistenten ab.  

###  <a name="create-a-general-license-statement-information-file-for-import"></a><a name="BKMK_CreateGeneralLicenseStatement"></a> Erstellen einer allgemeinen Lizenzzusammenfassungsdatei zum Import  
 Eine allgemeine Lizenzübersicht kann auch mithilfe einer manuell im kommagetrennten CSV-Dateiformat erstellten Lizenzimportdatei in den Asset Intelligence-Katalog importiert werden.  

> [!NOTE]  
>  Obwohl nur in den Feldern **Name**, **Herausgeber**, **Version**und **Tatsächliche Menge** Daten enthalten sein müssen, ist die Eingabe in alle Felder der ersten Zeile der Lizenzimportdatei obligatorisch. Alle Datumsfelder müssen das folgende Format aufweisen: Monat/Tag/Jahr, z. B. 08/04/2008.  

Von Asset Intelligence werden die Produkte, die Sie in der allgemeinen Lizenzerklärung angeben, anhand von Produktnamen und Produktversion abgeglichen, jedoch nicht anhand des Namens des Herausgebers. Sie müssen in der allgemeinen Lizenzerklärung einen Produktnamen verwenden, der exakt mit dem in der Standortdatenbank gespeicherten Produktnamen übereinstimmt. Von Asset Intelligence wird der Wert **Tatsächliche Menge**, der in der allgemeinen Lizenzerklärung angegeben ist, mit der Anzahl installierter Produkte verglichen, die bei der Configuration Manager-Inventur gefunden werden.  

> [!TIP]  
>  Für eine vollständige Liste der in der Configuration Manager-Standortdatenbank gespeicherten Produktnamen können Sie auf der Standortdatenbank die folgende Abfrage ausführen: SELECT ProductName0 FROM v_GS_INSTALLED_SOFTWARE.  

 Sie können die exakte Version oder einen Teil der Version (z. B. die Hauptversion) für ein Produkt angeben. Die folgenden Beispiele sind die Übereinstimmungen der Version mit einem Versionseintrag einer allgemeinen Lizenzzusammenfassung für ein bestimmtes.  

|Eintrag der allgemeinen Lizenzzusammenfassung|Übereinstimmende Standortdatenbankeinträge|  
|-------------------------------------|------------------------------------|  
|Name: „MeineSoftware“, Produktversion0:„2“|ProductName0: „MeineSoftware“, Produktversion0: "2.01.1234"<br /><br /> ProductName0: „MeineSoftware“, Produktversion0: "2.02.5678"<br /><br /> ProductName0: „MeineSoftware“, Produktversion0: "2.05.1234"<br /><br /> ProductName0: „MeineSoftware“, Produktversion0: "2.05.5678"<br /><br /> ProductName0: „MeineSoftware“, Produktversion0: "2.05.3579.000"<br /><br /> ProductName0: „MeineSoftware“, Produktversion0: "2.10.1234"|  
|Name: „MeineSoftware“, Version „2.05“|ProductName0: „MeineSoftware“, Produktversion0: "2.05.1234"<br /><br /> ProductName0: „MeineSoftware“, Produktversion0: "2.05.5678"<br /><br /> ProductName0: „MeineSoftware“, Produktversion0: "2.05.3579.000"|  
|Name: „MeineSoftware“, Version „2“<br /><br /> Name: „MeineSoftware“, Version „2.05“|Fehler beim Importieren. Beim Import tritt ein Fehler auf, wenn mehr als ein Eintrag mit derselben Produktversion übereinstimmt.|  
  

##### <a name="to-create-a-general-license-statement-import-file-by-using-microsoft-excel"></a>So erstellen sie eine Importdatei für die allgemeine Lizenzzusammenfassung unter Verwendung von Microsoft Excel  

1.  Öffnen Sie Microsoft Excel, und erstellen Sie ein neues Arbeitsblatt.  

2.  Geben Sie in die erste Zeile der neuen Kalkulationstabelle die Namen aller Softwarelizenz-Datenfelder ein.  

3.  Geben Sie in die zweite sowie die folgenden Zeilen der neuen Kalkulationstabelle die notwendigen Softwarelizenzinformationen ein. Stellen Sie sicher, dass in den darauf folgenden Zeilen für alle zu importierenden Softwarelizenzen mindestens die obligatorischen Softwarelizenz-Datenfelder eingegeben werden. Der in der Kalkulationstabelle eingegebene Softwaretitel muss identisch mit dem Titel sein, der im Anschluss an die Ausführung der Hardwareinventur für einen Client im Ressourcen-Explorer angezeigt wird.  

4.  Speichern Sie die Datei im CSV-Format.  

5.  Kopieren Sie die CSV-Datei in die Dateifreigabe, die für den Import von Softwarelizenzinformationen in den Asset Intelligence-Katalog verwendet wird.  

6.  Verwenden Sie in der Configuration Manager-Konsole den Assistenten zum Importieren von Softwarelizenzen, um die neu erstellte CSV-Datei zu importieren.  

7.  Führen Sie den **Asset Intelligence-MVLS-Abstimmungsbericht für Lizenz 15A** aus, um sicherzustellen, dass die Lizenzinformationen erfolgreich in den Asset Intelligence-Katalog importiert wurden.  

> [!NOTE]  
>  Ein Beispiel für eine allgemeine Softwarelizenzdatei, die für Testzwecke verwendet werden kann, finden Sie unter [Beispiel für eine allgemeine Asset Intelligence-Lizenzimportdatei](../../../../core/clients/manage/asset-intelligence/example-asset-intelligence-general-license-import.md).  

#### <a name="sample-table-to-describe-software-licenses"></a>Tabelle mit Beispielen zur Beschreibung von Softwarelizenzen  
 Bei der Erstellung einer Importdatei für die allgemeine Lizenzzusammenfassung können die Informationen in der folgenden Tabelle zum Beschreiben der in den Asset Intelligence-Katalog zu importierenden Softwarelizenzen verwendet werden.  

|Spaltenname|Datentyp|Erforderlich|Beispiel|  
|-----------------|---------------|--------------|-------------|  
|Name|Bis zu 255 Zeichen|Ja|Softwaretitel|  
|Herausgeber|Bis zu 255 Zeichen|Ja|Softwareherausgeber|  
|Version|Bis zu 255 Zeichen|Ja|Version des Softwaretitels|  
|Sprache|Bis zu 255 Zeichen|Ja|Sprache des Softwaretitels|  
|Tatsächliche Menge|Ganzzahliger Wert|Ja|Anzahl erworbener Lizenzen|  
|PONumber|Bis zu 255 Zeichen|Nein|Bestellinformationen|  
|Name des Wiederverkäufers|Bis zu 255 Zeichen|Nein|Informationen zum Vertragshändler|  
|Kaufdatum|Datumswert in folgendem Format: TT.MM.JJJJ|Nein|Datum des Lizenzerwerbs|  
|Support erworben|Bitwert|Nein|0 oder 1: Geben Sie „0“ für „Ja“ oder „1“ für „Nein“ ein.|  
|Ablaufdatum Support|Datumswert in folgendem Format: TT.MM.JJJJ|Nein|Enddatum des erworbenen Supports|  
|Kommentare|Bis zu 255 Zeichen|Nein|Optionale Kommentare|  

###  <a name="configure-asset-intelligence-maintenance-tasks"></a><a name="BKMK_ConfigureMaintenanceTasks"></a> Configure Asset Intelligence maintenance tasks  
 Die folgenden Wartungstasks sind für Asset Intelligence verfügbar:  

-   **Anwendungstitel mit Inventurinformationen prüfen:** Mit diesem Wartungstask wird geprüft, ob der im Softwareinventar gemeldete Softwaretitel mit dem Softwaretitel im Asset Intelligence-Katalog abgestimmt ist. Dieser Task ist standardmäßig aktiviert und zur Ausführung an Samstagen nach 0:00 Uhr und vor 5:00 Uhr eingeplant. Dieser Wartungstask ist nur am Standort der obersten Ebene in der Configuration Manager-Hierarchie verfügbar.  

-   **Daten installierter Software zusammenfassen**: Durch diesen Wartungstask werden die Informationen zur Verfügung gestellt, die im Arbeitsbereich **Assets und Konformität** im Knoten **Inventarisierte Software** unter dem Knoten **Asset Intelligence** angezeigt werden. Wenn der Task ausgeführt wird, wird die Anzahl aller inventarisierten Softwaretitel am primären Standort von Configuration Manager gesammelt. Dieser Task ist standardmäßig aktiviert und zur täglichen Ausführung nach 0:00 Uhr und vor 5:00 Uhr eingeplant. Dieser Wartungstask ist nur an primären Standorten verfügbar.  

##### <a name="to-configure-asset-intelligence-maintenance-tasks"></a>So konfigurieren Sie Wartungstasks für Asset Intelligence  

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** > **Standortkonfiguration** > **Standorte** aus.  

3.  Wählen Sie den Standort aus, an dem der Wartungstask für Asset Intelligence konfiguriert werden soll.  

4.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Einstellungen** **Standortwartung** aus. Wählen Sie einen Task und anschließend **Bearbeiten** aus, um die Einstellungen zu ändern. 

    Es wird empfohlen, den Zeitpunkt außerhalb der Spitzenzeiten des Standorts zu legen. Der Zeitraum ist das Zeitintervall, in dem der Task ausgeführt werden kann. Er wird über die Optionen **Start nach** und **Spätester Startzeitpunkt** im Dialogfeld **Taskeigenschaften** definiert.  

    Sie können den Task direkt initiieren, indem Sie den aktuellen Tag auswählen und für die Option **Start nach** eine Zeit wenige Minuten nach der aktuellen Zeit festlegen.  

7.  Wählen Sie **OK** aus, um die Einstellungen zu speichern. Der Task wird nun gemäß dem Zeitplan ausgeführt.  

    > [!NOTE]  
    >  Wenn beim ersten Versuch, den Task auszuführen, ein Fehler auftritt, wird von Configuration Manager versucht, den Task solange erneut auszuführen, bis der Task entweder erfolgreich ausgeführt wird oder der Zeitraum, in dem der Task ausgeführt werden kann, verstrichen ist.  
