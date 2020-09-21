---
title: Aktivieren von Updates von Drittanbietern
titleSuffix: Configuration Manager
description: Aktivieren von Updates von Drittanbietern in Configuration Manager
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 946b0f74-0794-4e8f-a6af-9737d877179b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: bf50039a7c2fe8490c89f3e3b0adca275bb69e20
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607991"
---
# <a name="enable-third-party-updates"></a>Aktivieren von Updates von Drittanbietern 

*Gilt für: Configuration Manager (Current Branch)*

Ab Version 1806 können Sie über den neue Knoten **Katalog mit Updates für Drittanbietersoftware** in der Configuration Manager-Konsole Drittanbieterkataloge abonnieren, deren Updates für Ihren Softwareupdatepunkt (SUP) veröffentlichen und diese dann für Clients bereitstellen.  <!--1357605, 1352101, 1358714-->

> [!Note]  
> Configuration Manager aktiviert dieses Feature nicht automatisch. Aktivieren Sie das optionale Feature **Unterstützung für Drittanbieterupdates auf Clients aktivieren**, bevor Sie es verwenden. Weitere Informationen finden Sie unter [Enable optional features from updates (Aktivieren optionaler Features von Updates)](../../core/servers/manage/install-in-console-updates.md#bkmk_options).


## <a name="prerequisites"></a>Voraussetzungen 
- Auf dem SUP (im Ordner „WSUSContent“) auf oberster Ebene muss ausreichend Speicherplatz zur Verfügung stehen, um die Binärdateien des Quellinhalts für Updates der Drittanbietersoftware zu speichern.
    - Der erforderliche Speicher variiert je nach Anbieter, Updatetypen und spezifischen Updates, die Sie für die Bereitstellung veröffentlichen.
    - Wenn Sie den Ordner „WSUSContent“ auf ein anderes Laufwerk mit genügend freiem Speicherplatz verschieben müssen, finden Sie Informationen dazu in dem Blogbeitrag [How to change the location where WSUS stores updates locally (Ändern des Speicherorts für lokale WSUS-Updates)](/archive/blogs/sus/wsus-how-to-change-the-location-where-wsus-stores-updates-locally).
- Der Synchronisierungsdienst für Updates für Drittanbietersoftware muss Zugriff auf das Internet haben.
    - Für die Katalogliste mit Partnern wird download.microsoft.com über den HTTPS-Port 443 benötigt. 
    -  Internetzugriff auf Drittanbieterkataloge und Updateinhaltsdateien. Möglicherweise benötigen Sie neben Port 443 noch weitere Ports.
    - Updates von Drittanbietern verwenden dieselben Proxyeinstellungen wie der SUP.
- Bei Configuration Manager-Versionen vor Version 1910 kann die Sicherheitsrolle **Softwareupdate-Manager** keine Kataloge von Drittanbietern synchronisieren. Sie benötigen die Sicherheitsrolle **Hauptadministrator**, um die Kataloge zu synchronisieren.


## <a name="additional-requirements-when-the-sup-is-remote-from-the-top-level-site-server"></a>Zusätzliche Anforderungen, wenn der SUP sich nicht auf dem Standortserver auf oberster Ebene befindet 

1. Wenn sich der SUP nicht auf dem Standortserver befindet, muss Secure Sockets Layer (SSL) aktiviert sein. Dies erfordert ein Serverauthentifizierungszertifikat von einer internen Zertifizierungsstelle oder über einen öffentlichen Anbieter.
    - [Configure SSL on WSUS (Konfigurieren von WSUS für SSL)](/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol)
        - Wenn Sie SSL in WSUS konfigurieren, beachten Sie, dass einige der Webdienste und virtuellen Verzeichnisse HTTP anstelle von HTTPS verwenden. 
        - Configuration Manager lädt Inhalte von Drittanbietern für Softwareupdatepakete über HTTP aus Ihrem WSUS-Inhaltsverzeichnis herunter.   
    - [Configure SSL on SUP (Konfigurieren von SSL auf dem SUP)](../get-started/install-a-software-update-point.md#configure-ssl-communications-to-wsus)

2. Wenn Sie die WSUS-Signaturzertifikat-Konfiguration für Updates von Drittanbietern in den Eigenschaften der Softwareupdatepunkt-Komponente auf **Configuration Manager verwaltet das Zertifikat** festlegen, sind die folgenden Konfigurationen erforderlich, um das Erstellen des selbstsignierten WSUS-Signaturzertifikats zu ermöglichen: 
   - Die Remoteregistrierung sollte auf dem SUP-Server aktiviert sein.
   -  Das **Verbindungskonto für den WSUS-Server** sollte auf dem SUP- bzw. WSUS-Server über Berechtigungen für die Remoteregistrierung verfügen. 


3. Erstellen Sie den folgenden Registrierungsschlüssel auf dem Configuration Manager-Standortserver: 
    - `HKLM\Software\Microsoft\Update Services\Server\Setup`, erstellen Sie ein neues DWORD mit dem Namen **EnableSelfSignedCertificates** und dem Wert `1`. 

4. Gehen Sie wie folgt vor, um die Installation des selbstsignierten WSUS-Signaturzertifikats in den Speichern des vertrauenswürdigen Herausgebers und des vertrauenswürdigen Stamms auf dem SUP-Remoteserver zu aktivieren:
   - Das **Verbindungskonto für den WSUS-Server** sollte über Berechtigungen für die Remoteverwaltung auf dem SUP-Server verfügen.

     Wenn dies nicht möglich ist, exportieren Sie das Zertifikat aus dem WSUS-Speicher des lokalen Computers in die Speicher des vertrauenswürdigen Herausgebers und des vertrauenswürdigen Stamms. 

> [!NOTE] 
>Sie können das **Verbindungskonto für WSUS-Server** über die Registerkarte **Proxy- und Kontoeinstellungen** unter den Eigenschaften der Standortsystemrolle des SUP ermitteln. Wird kein Konto angegeben, wird das Computerkonto des Standortservers verwendet.

## <a name="enable-third-party-updates-on-the-sup"></a>Aktivieren von Updates von Drittanbietern auf dem SUP
Wenn Sie diese Option aktivieren, können Sie in der Configuration Manager-Konsole Updatekataloge von Drittanbietern abonnieren. Anschließend können Sie diese Updates für WSUS veröffentlichen und für Clients bereitstellen. Sie sollten die folgenden Schritte für jede Hierarchie einmal durchführen, um das Feature für die Verwendung zu aktivieren und einzurichten. Sie müssen diese Schritte möglicherweise wiederholen, wenn Sie den WSUS-Server der SUPs auf oberster Ebene ersetzen. 

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**. Erweitern Sie **Standortkonfiguration**, und klicken Sie auf den Knoten **Standorte**.
2. Wählen Sie den obersten Standort in der Hierarchie aus. Klicken Sie im Menüband auf **Standortkomponenten konfigurieren**, und wählen Sie dann **Softwareupdatepunkt** aus.
3. Wechseln Sie zur Registerkarte **Third-Party Updates** (Updates von Drittanbietern). Klicken Sie auf die Option **Updates für Drittanbietersoftware aktivieren**.

    ![Screenshot der SUP-Eigenschaften für Drittanbieterupdates](media/third-party-sup-properties.PNG)


## <a name="configure-the-wsus-signing-certificate"></a>Konfigurieren des WSUS-Signaturzertifikats
Sie müssen entscheiden, ob Configuration Manager automatisch das WSUS-Signaturzertifikat für Drittanbieter mit einem selbstsignierten Zertifikat verwalten soll, oder ob Sie das Zertifikat manuell konfigurieren möchten. 

### <a name="automatically-manage-the-wsus-signing-certificate"></a>Automatisches Verwalten des WSUS-Signaturzertifikats
Wenn Sie nicht dazu verpflichtet sind, PKI-Zertifikate zu verwenden, können Sie Sicherheitszertifikate für Updates von Drittanbietern automatisch verwalten lassen. Die WSUS-Zertifikate werden dann im Laufe der Synchronisierung ausgeführt. Protokolle dazu werden in der `wsyncmgr.log`-Datei geführt. 

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**. Erweitern Sie **Standortkonfiguration**, und klicken Sie auf den Knoten **Standorte**.
2. Wählen Sie den obersten Standort in der Hierarchie aus. Klicken Sie im Menüband auf **Standortkomponenten konfigurieren**, und wählen Sie dann **Softwareupdatepunkt** aus.
3. Wechseln Sie zur Registerkarte **Third-Party Updates** (Updates von Drittanbietern). Klicken Sie auf die Option **Zertifikatverwaltung durch Configuration Manager**. 
4. Dann wird ein neues Zertifikat vom Typ **Drittanbieter-WSUS-Signatur** im Knoten **Zertifikate** unter **Sicherheit** im Arbeitsbereich **Verwaltung** erstellt.  

### <a name="manually-manage-the-wsus-signing-certificate"></a>Manuelles Verwalten des WSUS-Signaturzertifikats
Wenn Sie das Zertifikat manuell konfigurieren müssen (genauso wie Sie z.B. auch ein PKI-Zertifikat verwenden müssen), müssen Sie dafür entweder [System Center Updates Publisher](../tools/updates-publisher-options.md#update-server) oder ein anderes Tool verwenden.  

1. Konfigurieren des Signaturzertifikats mit [System Center Updates Publisher](../tools/updates-publisher-options.md#update-server).
2. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**. Erweitern Sie **Standortkonfiguration**, und klicken Sie auf den Knoten **Standorte**.
3. Wählen Sie den obersten Standort in der Hierarchie aus. Klicken Sie im Menüband auf **Standortkomponenten konfigurieren**, und wählen Sie dann **Softwareupdatepunkt** aus.
4. Wechseln Sie zur Registerkarte **Third-Party Updates** (Updates von Drittanbietern). Klicken Sie auf die Option **Zertifikat manuell verwalten**.


## <a name="enable-third-party-updates-on-the-clients"></a>Aktivieren von Updates von Drittanbietern für die Clients
Aktivieren Sie Updates von Drittanbietern auf den Clients in den Clienteinstellungen. Die Einstellung legt die Richtlinie des Windows Update-Agents für das [Zulassen signierter Updates für einen Intranetspeicherort für den Microsoft-Updatedienst](/windows-server/administration/windows-server-update-services/deploy/4-configure-group-policy-settings-for-automatic-updates#allow-signed-updates-from-an-intranet-microsoft-update-service-location) fest. Außerdem installiert diese Clienteinstellung das WSUS-Signaturzertifikat im Speicher des vertrauenswürdigen Herausgebers auf dem Client. Protokolle zur Zertifikatverwaltung finden Sie in der `updatesdeployment.log`-Datei auf den Clients.  Führen Sie diese Schritte für jede benutzerdefinierte Clienteinstellung durch, die Sie für Updates von Drittanbietern verwenden möchten. Weitere Informationen finden Sie in dem Artikel [Informationen zu Clienteinstellungen in System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md#enable-third-party-software-updates).

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, und klicken Sie auf den Knoten **Clienteinstellungen**.
2. Wählen Sie eine bereits vorhandene benutzerdefinierte Clienteinstellung aus, oder erstellen Sie eine neue. 
3. Klicken Sie auf der linken Seite auf die Registerkarte **Softwareupdates**. Wenn Sie nicht über diese Registerkarte verfügen, stellen Sie sicher, dass das Feld **Softwareupdates** ausgewählt ist.
4. Wählen Sie für die Option **Updates für Drittanbietersoftware aktivieren** **Ja** aus. 


## <a name="add-a-custom-catalog"></a>Hinzufügen eines benutzerdefinierten Katalogs
Bei *Partnerkatalogen* handelt es sich um Kataloge von Softwareherstellern, deren Daten bereits bei Microsoft registriert wurden. Sie können diese Kataloge abonnieren, ohne dafür zusätzliche Informationen angeben zu müssen. Kataloge, die Sie selbst hinzufügen, werden als *benutzerdefinierte Kataloge* bezeichnet. Sie können einen benutzerdefinierten Katalog von einem Drittanbieter von Updates zu Configuration Manager hinzufügen. Benutzerdefinierte Kataloge müssen HTTPS verwenden, und die Updates müssen digital signiert sein. 

1. Wechseln Sie zum Arbeitsbereich **Software Updates Library** (Bibliothek für Softwareupdates), erweitern Sie die Option **Softwareupdates**, und klicken Sie auf den Knoten **Katalog mit Updates für Drittanbietersoftware**. 
   
     ![Screenshot des Knotens für Updates von Drittanbietern](media/third-party-updates-node.PNG)
2. Klicken Sie im Menüband auf **Benutzerdefinierten Katalog hinzufügen**. 

     ![Benutzerdefinierter Katalog, zu dem Updates von Drittanbietern hinzugefügt wurden](media/third-party-updates-custom-catalog.png)
1. Geben Sie auf der Seite **Allgemein** folgende Elemente an: 
    - **Download URL:** eine gültige HTTPS-Adresse des benutzerdefinierten Katalogs.
    - **Herausgeber:** der Name der Organisation, die den Katalog veröffentlicht. 
    - **Name:** der Name des Katalogs, der in der Configuration Manager-Konsole angezeigt werden soll. 
    - **Beschreibung:** eine Beschreibung der Warnung. 
    - **Support-URL** (optional): eine gültige HTTPS-Adresse einer Website, auf der Hilfe zum Katalog angeboten wird. 
    - **Supportkontakt** (optional): Kontaktinformationen, über die man Hilfe zum Katalog erhält. 
2. Wenn Sie auf **Weiter** klicken, erhalten Sie eine Katalogzusammenfassung und können weitere Schritte mit dem Assistenten für **benutzerdefinierte Kataloge mit Softwareupdates für Drittanbieter** ausführen.


## <a name="subscribe-to-a-third-party-catalog-and-sync-updates"></a>Abonnieren von Drittanbieterkatalogen und Synchronisierungsupdates
Wenn Sie in der Configuration Manager-Konsole Drittanbieterkataloge abonnieren, werden die Metadaten für alle Updates im Katalog auf den WSUS-Servern für Ihren SUP synchronisiert. Wenn die Metadaten synchronisiert werden, können die Clients bestimmen, ob die jeweiligen Updates ausgeführt werden sollen. Führen Sie die folgenden Schritte für jeden Drittanbieterkatalog aus, den Sie abonnieren möchten:  

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**. Erweitern Sie **Softwareupdates**, und klicken Sie auf den Knoten **Katalog mit Updates für Drittanbietersoftware**.  
2. Wählen Sie den zu abonnierenden Katalog aus, und klicken Sie im Menüband auf **Subscribe to Catalog** (Katalog abonnieren). 
    ![Drittanbieterupdates – Katalog abonnieren](media/third-party-updates-subscribe.png)
3. Überprüfen und genehmigen Sie das Katalogzertifikat.  
   > [!NOTE]
   > 
   > Wenn Sie einen Katalog mit Updates für Drittanbietersoftware abonnieren, wird das Zertifikat, das Sie im Assistenten überprüfen und genehmigen, dem Standort hinzugefügt. Dieses Zertifikat ist vom Typ **Katalog mit Updates für Drittanbietersoftware**. Sie können es über den Knoten **Zertifikate** unter **Sicherheit** im Arbeitsbereich **Verwaltung** verwalten.  
4. Schließen Sie den Assistenten ab. Wenn das erste Abonnement abgeschlossen wurde, sollte der Download des Katalogs innerhalb weniger Minuten beginnen. 
    - Der Katalog wird automatisch alle sieben Tage synchronisiert.
    - Klicken Sie im Menüband auf **Jetzt synchronisieren**, um die Synchronisierung zu erzwingen.
5. Nachdem der Katalog heruntergeladen wurde, müssen die Produktmetadaten der WSUS-Datenbank in der Configuration Manager-Datenbank synchronisiert werden. [Starten Sie die Synchronisierung von Softwareupdates manuell](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization), um die Produktinformationen zu synchronisieren.
6. Wenn die Produktinformationen synchronisiert sind, [konfigurieren Sie den SUP, um das gewünschte Produkt](../get-started/configure-classifications-and-products.md#to-configure-classifications-and-products-to-synchronize) in Configuration Manager zu synchronisieren.  
7. [Starten Sie die Synchronisierung von Softwareupdates manuell](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization), um die neuen Updates für das Produkt in Configuration Manager zu synchronisieren.  
8. Wenn die Synchronisierung abgeschlossen ist, werden alle Updates von Drittanbietern im Knoten **Alle Updates** angezeigt. Diese Updates werden als **reine Metadatenupdates** veröffentlicht, bis Sie diese für die Allgemeinheit veröffentlichen möchten. 
     - Das Symbol mit dem blauen Pfeil kennzeichnet ein nur Metadaten enthaltendes Softwareupdate. ![Symbol für ein reines Metadatensoftwareupdate](media/MetadataOnly.png)


## <a name="publish-and-deploy-third-party-software-updates"></a>Veröffentlichen und Bereitstellen von Updates für Drittanbietersoftware 
Sobald die Updates von Drittanbietern im Knoten **Alle Updates** angezeigt werden, können Sie auswählen, welche bereitgestellt werden sollten. Wenn Sie ein Update veröffentlichen, werden die Binärdateien von der Website des Herstellers heruntergeladen und im Verzeichnis „WSUSContent“ auf dem SUP der obersten Ebene gespeichert. 

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**. Erweitern Sie **Softwareupdates**, und klicken Sie auf den Knoten **Alle Softwareupdates**.
2. Klicken Sie auf **Kriterien hinzufügen**, um die Liste von Updates zu filtern. Fügen Sie z.B. **Hersteller** für **HP** hinzu, um alle Updates von HP abzurufen.  
3. Wählen Sie die Updates aus, die für Ihre Organisation erforderlich sind. Klicken Sie auf **Softwareupdateinhalte von Drittanbietern veröffentlichen**.
    - Diese Aktion lädt die Updatebinärdateien vom Hersteller herunter und speichert sie im Ordner „WSUSContent“ auf dem SUP der obersten Ebene. 
4. [Starten Sie die Synchronisierung von Softwareupdates manuell](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization), um den Status der veröffentlichten Updates von „Metadata-only Updates“ (Reine Metadatenupdates) in „Deployable Updates“ (Bereitstellbare Updates) mit Inhalt zu ändern. 
    >[!NOTE]
    >Wenn Sie Softwareupdateinhalte von Drittanbietern veröffentlichen, werden alle zum Signieren des Inhalts verwendete Zertifikate dem Standort hinzugefügt. Diese Zertifikate sind vom Typ **Inhalt von Updates für Drittanbietersoftware**. Sie können sie über den Knoten **Zertifikate** unter **Sicherheit** im Arbeitsbereich **Verwaltung** verwalten.  

5. Überprüfen Sie den Fortschritt im Protokoll „SMS_ISVUPDATES_SYNCAGENT.log“. Dieses Protokoll ist im Order „Site System Logs“ (Standortsystemprotokoll) auf dem SUP der obersten Ebene gespeichert.
6. Stellen Sie Softwareupdates über den Prozess zum [Bereitstellen von Softwareupdates](../deploy-use/deploy-software-updates.md) bereit. 
7. Wählen Sie auf der Seite **Download Locations** (Downloadpfade) des **Assistenten zum Bereitstellen von Softwareupdates** die Standardoption **Softwareupdates aus dem Internet herunterladen** aus. In diesem Szenario ist der Inhalt bereits für den Softwareupdatepunkt bereitgestellt, der dazu genutzt wird, den Inhalt für das Bereitstellungspaket herunterzuladen.
8. Clients müssen die Updates überprüfen und auswerten, bevor Ihnen Ergebnisse zur Kompatibilität angezeigt werden können.  Sie können diesen Zyklus über die Configuration Manager-Systemsteuerung auf einem Client manuell auslösen, indem Sie die Aktion **Überprüfungszyklus für Softwareupdates** ausführen.


## <a name="improvements-for-third-party-updates-starting-in-1910"></a><a name="bkmk_1910"></a> Verbesserungen für Updates von Drittanbietern ab Version 1910
<!--4469002-->
Sie verfügen nun über eine präzisere Steuerung über die Synchronisierung von Katalogen mit Updates von Drittanbietern. Ab Configuration Manager Version 1910 können Sie den Synchronisierungszeitplan für jeden Katalog unabhängig konfigurieren. Wenn Sie Kataloge verwenden, die kategorisierte Updates enthalten, können Sie die Synchronisierung so konfigurieren, dass nur bestimmte Updatekategorien eingeschlossen werden, um eine Synchronisierung des gesamten Katalogs zu vermeiden. Wenn Sie bei kategorisierten Katalogen sicher sind, dass Sie eine Kategorie bereitstellen werden, können Sie sie so konfigurieren, dass sie automatische heruntergeladen und in WSUS veröffentlicht wird.

### <a name="set-the-schedule-for-a-catalog-in-a-new-catalog-subscription"></a>Festlegen des Zeitplans für einen Katalog in einem neuen Katalogabonnement

1. Wechseln Sie zum Arbeitsbereich **Softwarebibliothek**, erweitern Sie die Option **Softwareupdates**, und klicken Sie auf den Knoten **Katalog mit Updates für Drittanbietersoftware**.
1. Wählen Sie den zu abonnierenden Katalog aus, und klicken Sie im Menüband auf **Subscribe to Catalog** (Katalog abonnieren).
1. Wählen Sie auf der Seite **Zeitplan** die gewünschten Optionen aus, wenn Sie den standardmäßigen Synchronisierungszeitplan außer Kraft setzen möchten:
   - **Einfacher Zeitplan**:  Wählen Sie das Intervall in Stunden, Tagen oder Monaten aus.
   - **Benutzerdefinierter Zeitplan**: Legen Sie einen komplexen Zeitplan fest.

### <a name="update-the-schedule-per-catalog"></a>Aktualisieren des Zeitplans je Katalog

1. Wechseln Sie zum Arbeitsbereich **Softwarebibliothek**, erweitern Sie die Option **Softwareupdates**, und klicken Sie auf den Knoten **Katalog mit Updates für Drittanbietersoftware**.
1. Klicken Sie mit der rechten Maustaste auf den Katalog, und wählen Sie **Eigenschaften** aus.
1. Wählen Sie auf der Registerkarte „Zeitplan“ die gewünschten Optionen aus: 
   - **Einfacher Zeitplan**:  Wählen Sie das Intervall in Stunden, Tagen oder Monaten aus.
   - **Benutzerdefinierter Zeitplan**: Legen Sie einen komplexen Zeitplan fest.

### <a name="new-subscription-to-a-third-party-v3-catalog"></a>Neues Abonnement für einen v3-Drittanbieterkatalog

> [!IMPORTANT]
> Diese Option ist nur für v3-Drittanbieterupdatekataloge verfügbar, die Kategorien für Updates unterstützen. Diese Optionen sind für Kataloge deaktiviert, die nicht im neuen v3-Format veröffentlicht werden.


1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**. Erweitern Sie **Softwareupdates**, und klicken Sie auf den Knoten **Katalog mit Updates für Drittanbietersoftware**.
1. Wählen Sie den zu abonnierenden Katalog aus, und klicken Sie im Menüband auf **Subscribe to Catalog** (Katalog abonnieren).
1. Wählen Sie Ihre Optionen auf der Seite **Kategorien auswählen** aus:

   - **Alle Updatekategorien synchronisieren** (Standard)
       - Synchronisiert alle Updates im Drittanbieterupdatekatalog im Configuration Manager.
   -  **Kategorien für Synchronisierung auswählen**
       - Wählen Sie die Kategorien und untergeordneten Kategorien aus, die in Configuration Manager synchronisiert werden sollen.

      ![Auswählen der Updatekategorien zum Synchronisieren in Configuration Manager](./media/4469002-select-categories-for-sync.png)
1. Wählen Sie aus, ob Sie für den Katalog **Updateinhalt bereitstellen** möchten. Wenn Sie den Inhalt bereitstellen, werden alle Updates in den ausgewählten Kategorien automatisch auf Ihren obersten Softwareupdatepunkt heruntergeladen, was bedeutet, dass Sie vor der Bereitstellung nicht sicherstellen müssen, dass sie bereits heruntergeladen wurden. Sie sollten Inhalt nur für Updates, die Sie wahrscheinlich bereitstellen, automatisch bereitstellen, um übermäßige Bandbreiten- und Speicheranforderungen zu vermeiden.

   - **Keine Inhalte bereitstellen, nur zur Überprüfung synchronisieren (empfohlen)**
     - Keine Inhalte für Updates im Drittanbieterkatalog herunterladen
   - **Inhalt für ausgewählte Kategorien automatisch bereitstellen**
     - Wählen Sie die Updatekategorien aus, die automatisch Inhalte herunterladen.
     - Der Inhalt für Updates in ausgewählten Kategorien wird in das WSUS-Inhaltsverzeichnis des obersten Softwareupdatepunkts heruntergeladen.
      ![Auswählen von Updatekategorien zum Bereitstellen von Inhalt](./media/4469002-stage-content.png)
1. Legen Sie den **Zeitplan** für die Katalogsynchronisierung fest, und schließen Sie den Assistenten ab.

 

### <a name="edit-an-existing-subscription"></a>Bearbeiten eines vorhandenen Abonnements

> [!IMPORTANT]
> Diese Option ist nur für v3-Drittanbieterupdatekataloge verfügbar, die Kategorien für Updates unterstützen. Diese Optionen sind für Kataloge deaktiviert, die nicht im neuen v3-Format veröffentlicht werden.

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**. Erweitern Sie **Softwareupdates**, und klicken Sie auf den Knoten **Katalog mit Updates für Drittanbietersoftware**.
1. Klicken Sie mit der rechten Maustaste auf den Katalog, und wählen Sie **Eigenschaften** aus.
1. Wählen Sie Ihre Optionen auf der Registerkarte **Kategorien auswählen** aus.
   - **Alle Updatekategorien synchronisieren** (Standard)
       - Synchronisiert alle Updates im Drittanbieterupdatekatalog im Configuration Manager.
   -  **Kategorien für Synchronisierung auswählen**
       - Wählen Sie die Kategorien und untergeordneten Kategorien aus, die in Configuration Manager synchronisiert werden sollen.
1. Wählen Sie Ihre Optionen auf der Registerkarte **Updateinhalt bereitstellen** aus.
   - **Keine Inhalte bereitstellen, nur zur Überprüfung synchronisieren (empfohlen)**
     - Keine Inhalte für Updates im Drittanbieterkatalog herunterladen
   - **Inhalt für ausgewählte Kategorien automatisch bereitstellen**
     - Wählen Sie die Updatekategorien aus, die automatisch Inhalte herunterladen.
     - Der Inhalt für Updates in ausgewählten Kategorien wird in das WSUS-Inhaltsverzeichnis des obersten Softwareupdatepunkts heruntergeladen. 

## <a name="monitoring-progress-of-third-party-software-updates"></a>Überwachen des Fortschritts von Updates für Drittanbietersoftware 

Die Synchronisierung von Updates für Drittanbietersoftware wird auf dem Standard-SUP der obersten Ebene von der Komponente SMS_ISVUPDATES_SYNCAGENT verarbeitet. Sie können die Statusmeldungen von dieser Komponente oder ausführlichere Statusinformationen in „SMS_ISVUPDATES_SYNCAGENT.log“ sehen. Dieses Protokoll ist im Ordner „Site System Logs“ (Standortsystemprotokoll) auf dem SUP der obersten Ebene gespeichert. Der Standardpfad lautet C:\Programme\Microsoft Configuration Manager\Logs. Weitere Informationen über das Überwachen des allgemeinen Verwaltungsprozesses für Softwareupdates finden Sie unter [Überwachen von Softwareupdates in System Center Configuration Manager](../deploy-use/monitor-software-updates.md). 

## <a name="known-issues"></a>Bekannte Probleme

- Der Computer, auf dem die Konsole ausgeführt wird, wird verwendet, um die Updates aus WSUS herunterzuladen und zu den Updatepaketen hinzuzufügen. Das WSUS-Signaturzertifikat muss vom Konsolencomputer als vertrauenswürdig eingestuft sein. Wenn dies nicht der Fall ist, entstehen möglicherweise während des Downloads der Updates von Drittanbietern Probleme bei der Signaturüberprüfung. 
- Der Synchronisierungsdienst für Drittanbietersoftware-Updates kann Inhalte nicht für Updates bereitstellen, die nur Metadaten enthalten und über eine andere Anwendung, ein anderes Tool oder Skript (z.B. SCUP) zu WSUS hinzugefügt wurden. Die Aktion **Softwareupdateinhalte von Drittanbietern veröffentlichen** schlägt für diese Updates fehl. Wenn Sie Updates von Drittanbietern bereitstellen müssen, die noch nicht von diesem Feature unterstützt werden, verwenden Sie den vorhandenen Prozess vollständig für die Bereitstellung dieser Updates.  
-  Configuration Manager verfügt über eine neue Version des CAB-Formats für Katalogdateien. Diese enthält die Zertifikate zu den Binärdateien des Herstellers. Diese Zertifikate werden im Arbeitsbereich **Verwaltung** unter **Sicherheit** zum Knoten **Zertifikate** hinzugefügt, wenn Sie den Katalog genehmigen und als vertrauenswürdig einstufen.  
     - Sie können auch weiter ältere Versionen von CAB-Dateien verwenden, wenn die Download-URL HTTPS enthält und die Updates signiert sind. Dann kann der Inhalt nicht veröffentlicht werden, weil die Zertifikate zu diesen Binärdateien nicht in der CAB-Datei gespeichert sind und noch nicht genehmigt wurden. Sie können dieses Problem umgehen, wenn Sie das Zertifikat im Knoten **Zertifikate** suchen, blockieren und anschließend das Update erneut veröffentlichen. Wenn Sie mehrere Updates veröffentlichen, die mit verschiedenen Zertifikaten signiert wurden, müssen Sie die Blockierung für jedes Zertifikat aufheben, das verwendet wird.
     - Weitere Informationen finden Sie in der nachfolgenden Tabelle in den Statusmeldungen 11523 und 11524.
-  Wenn der Dienst zur Synchronisierung von Updates für Drittanbietersoftware auf dem Softwareupdatepunkt der obersten Ebene einen Proxyserver für den Internetzugriff benötigt, treten bei der Überprüfung digitaler Signaturen möglicherweise Fehler auf. Um dieses Problem zu beheben, konfigurieren Sie die WinHTTP-Proxyeinstellungen im Standortsystem. Weitere Informationen finden Sie unter [Netsh-Befehle für Windows Hypertext Transfer Protocol (WinHTTP)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731131(v=ws.10)).
- Bei der Verwendung eines CMG zum Speichern von Inhalten werden die Inhalte für Updates für Drittanbietersoftware nicht auf Clients heruntergeladen, wenn die [Clienteinstellung](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) **Clients das Herunterladen von Deltainhalten ermöglichen (falls verfügbar)** aktiviert ist. <!--6598587-->

## <a name="status-messages"></a>Statusmeldungen

| Meldungs-ID       | Schweregrad           | Beschreibung | Mögliche Ursache| Mögliche Lösung
| ------------- |-------------| -----|----|----|
| 11516     | Fehler |Fehler beim Veröffentlichen von Inhalten für das Update „Update-ID“, weil der Inhalt nicht signiert ist.  Es kann nur Inhalt mit gültigen Signaturen veröffentlicht werden.  |Configuration Manager lässt nicht zu, dass nicht signierte Updates veröffentlicht werden.| Veröffentlichen Sie das Update auf einem anderen Weg. </br></br>Prüfen Sie, ob der Hersteller ein signiertes Update anbietet.|
| 11523  | Warnung |  Katalog „X“ enthält keine Zertifikate zum Signieren von Inhalt. Updateinhalt für Updates aus diesem Katalog kann möglicherweise erst verwendet werden, wenn Zertifikate hinzugefügt und genehmigt werden, die Inhalt signieren. | Diese Meldung wird ggf. angezeigt, wenn Sie einen Katalog importieren, der eine ältere Version des CAB-Formats für eine Datei verwendet.|Kontaktieren Sie den Kataloganbieter, um einen aktualisierten Katalog zu erhalten, der Zertifikate enthält, die Inhalt signieren. </br> </br> Die Zertifikate zu diesen Binärdateien sind nicht in der CAB-Datei gespeichert, weshalb sie nicht veröffentlicht werden können. Sie können dieses Problem umgehen, indem Sie das Zertifikat im Knoten **Zertifikate** suchen, blockieren und anschließend das Update erneut veröffentlichen. Wenn Sie mehrere Updates veröffentlichen, die mit verschiedenen Zertifikaten signiert wurden, müssen Sie die Blockierung für jedes Zertifikat aufheben, das verwendet wird.|
| 11524| Fehler  | Fehler beim Veröffentlichen das Updates „ID“ aufgrund von fehlenden Updatemetadaten. | Das Update wurde möglicherweise ohne Configuration Manager für WSUS synchronisiert.| Synchronisieren Sie das Update mit Configuration Manager, bevor Sie dessen Inhalt veröffentlichen.  </br> </br>Wenn ein externes Tool verwendet wurde, um das Update als **Metadata only** (Reines Metadatenupdate) zu veröffentlichen, verwenden Sie dasselbe Tool, um den Updateinhalt zu veröffentlichen.|



## <a name="working-with-third-party-updates-video"></a>Arbeiten mit Videos zu Updates von Drittanbietern
<iframe width="560" height="315" src="https://www.youtube.com/embed/ai8rLCLtuTI?rel=0" frameborder="0" allowfullscreen></iframe>



## <a name="next-step"></a>Nächster Schritt
> [!div class="nextstepaction"]
> [Bereitstellen von Softwareupdates](./deploy-software-updates.md)