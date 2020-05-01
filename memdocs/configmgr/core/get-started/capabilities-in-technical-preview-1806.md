---
title: Technical Preview 1806
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über neue Features, die mit der Technical Preview-Version 1806 für System Center Configuration Manager zur Verfügung stehen.
ms.date: 06/06/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 52d64ef0-8c0d-42c3-857e-07d7ec776f29
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 522e01b0d811d768d4f239bc917c2e3db08e05ef
ms.sourcegitcommit: f94cdca69981627d6a3471b04ac6f0f5ee8f554f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/28/2020
ms.locfileid: "82210076"
---
# <a name="capabilities-in-technical-preview-1806-for-configuration-manager"></a>Funktionen in der Technical Preview 1806 für Configuration Manager

*Gilt für: Configuration Manager (Technical Preview-Branch)*

In diesem Artikel werden die Features vorgestellt, die in der Technical Preview-Version 1806 für System Center Configuration Manager verfügbar sind. Sie können diese Version installieren, um Funktionen für Ihren Technical Preview-Standort zu aktualisieren oder neue Funktionen hinzuzufügen. 

Lesen Sie den [Technical Preview](technical-preview.md)-Artikel vor der Installation dieses Updates. In diesem Artikel erhalten Sie Informationen zu den allgemeinen Anforderungen und Einschränkungen, die für die Verwendung der Technical Preview gelten. Außerdem erfahren Sie, wie Sie Updates zwischen den Versionen ausführen und Feedback übermitteln.     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->
## <a name="known-issues-in-this-technical-preview"></a>Bekannte Probleme in dieser Technical Preview

### <a name="site-fails-to-upgrade-with-remote-content-library"></a><a name="ki_contentlib"></a>Aktualisieren des Standorts mit Remoteinhaltsbibliothek schlägt fehl
<!--514642-->
Das Aktualisieren des Standorts schlägt fehl, und die folgenden Fehlermeldungen werden in **cmupdate.log** ausgegeben:  

``` Log
Failed to find any valid drives  
GetContentLibraryParameters failed; 0x80070057  
ERROR: Failed to process configuration manager update.  
```  

Dieses Problem tritt in diesem Release auf, wenn die Inhaltsbibliothek sich an einem Remotespeicherort befindet.

#### <a name="workaround"></a>Problemumgehung
Verschieben Sie die Inhaltsbibliothek auf ein lokales Laufwerk auf dem Standortserver. Weitere Informationen finden Sie unter [Konfigurieren einer Remoteinhaltsbibliothek für den Standortserver](capabilities-in-technical-preview-1804.md#configure-a-remote-content-library-for-the-site-server). 



</br>

**Im Folgenden werden neue Features aufgelistet, die Sie mit dieser Version ausprobieren können.**  



## <a name="third-party-software-updates"></a><a name="bkmk-3pupdate"></a>Updates für Drittanbietersoftware
<!--1352101-->
Aufgrund Ihres [UserVoice-Feedbacks](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co) unterstützt dieses Release weiterhin Updates für Drittanbietersoftware. Für einige allgemeine Szenarios benötigen Sie System Center Updates Publisher (SCUP) nicht mehr. Der neue Knoten **Third-Party Software Update Catalogs** (Katalog mit Updates für Drittanbietersoftware) in der Configuration Manager-Konsole ermöglicht Ihnen, Drittanbieterkataloge zu abonnieren, deren Updates für Ihren Softwareupdatepunkt zu veröffentlichen und diese dann für Clients bereitzustellen. 

Die folgenden Kataloge mit Updates für Drittanbietersoftware sind in diesem Release verfügbar:

 | Herausgeber | Katalogname |
 |--------|---------------------|
 | HP | HP Client Updates Catalog |

SCUP unterstützt weiterhin andere Kataloge und Szenarios. Die Liste von Katalogen im Knoten „Katalog mit Updates für Drittanbietersoftware“ der Configuration Manager-Konsole ist dynamisch und wird aktualisiert, wenn zusätzliche Kataloge verfügbar sind und unterstützt werden.


### <a name="prerequisites"></a>Voraussetzungen
- Die Softwareupdateverwaltung muss mit einem HTTPS-fähigen Softwareupdatepunkt eingerichtet sein. Weitere Informationen finden Sie unter [Prepare for software updates management (Vorbereiten der Softwareudateverwaltung)](../../sum/get-started/prepare-for-software-updates-management.md).  
  - Der Softwareupdatepunkt muss sich in diesem Release auf dem Standortserver für dieses Feature befinden. <!--515810--> 

    > [!Tip]  
    > Der Softwareupdatepunkt erfordert HTTPS, da dies eine Voraussetzung für die WSUS-APIs ist, die zum Verarbeiten der Signaturzertifikate verwendet werden. Clients müssen jedoch nicht HTTPS-fähig sein. Weitere Informationen zum Aktivieren von HTTPS für WSUS finden Sie in den folgenden Artikeln:  
    > - [2.5 Secure WSUS with the Secure Sockets Layer Protocol (2.5 Schützen von WSUS mit dem Secure Sockets Layer-Protokoll)](/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol) 
    > - [Blogbeitrag zur Unterstützung von WSUS](https://blogs.technet.microsoft.com/sus/2011/05/09/how-to-create-an-internet-facing-wsus-server-that-uses-different-internal-and-external-names/)

- Auf dem Softwareupdatepunkt (im Ordner „WSUSContent“) muss ausreichend Speicherplatz zur Verfügung stehen, um die Binärdateien des Quellinhalts für Updates der Drittanbietersoftware zu speichern. Der erforderliche Speicher variiert je nach Anbieter, Updatetypen und spezifischen Updates, die Sie für die Bereitstellung veröffentlichen. Wenn Sie den Ordner „WSUSContent“ auf ein anderes Laufwerk mit genügend freiem Speicherplatz verschieben müssen, finden Sie Informationen dazu unter [How to change the location where WSUS stores updates locally (Vorgehensweise: Ändern des Speicherorts für lokale WSUS-Updates)](https://blogs.technet.microsoft.com/sus/2008/05/19/wsus-how-to-change-the-location-where-wsus-stores-updates-locally/).  

- Aktivieren und Bereitstellen der Clienteinstellung [Softwareupdates von Drittanbietern aktivieren](../clients/deploy/about-client-settings.md#enable-third-party-software-updates) in der Gruppe **Softwareupdates**.  

- Der Standortserver erfordert eine Internetverbindung, um über HTTPS-Port 443 auf download.microsoft.com zugreifen zu können. Der Synchronisierungsdienst für Drittanbietersoftware-Updates wird derzeit auf dem Standortserver ausgeführt. Dieser Dienst aktualisiert die Liste der verfügbaren Drittanbieterkataloge, lädt die Kataloge herunter, die Sie abonnieren, und lädt die Updates herunter, wenn sie veröffentlicht werden. Konfigurieren Sie bei Bedarf die Internetproxyeinstellungen auf der Registerkarte **Proxy** der Einstellungen für die Standortsystemrolle des Standortservercomputers.  


### <a name="try-it-out"></a>Probieren Sie es aus!
 Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie uns anschließend Ihr [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback), und lassen Sie uns wissen, wie es gelaufen ist.


#### <a name="phase-1-enable-and-set-up-the-feature"></a>Phase 1: Aktivieren und Einrichten des Features
Führen Sie die folgenden Schritte *für jede Hierarchie einmal* aus, um das Feature für die Verwendung zu aktivieren und einzurichten:  

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**. Erweitern Sie **Standortkonfiguration**, und klicken Sie auf den Knoten **Standorte**.  

2. Wählen Sie den obersten Standort in der Hierarchie aus. Klicken Sie im Menüband auf **Standortkomponenten konfigurieren**, und wählen Sie dann **Softwareupdatepunkt** aus.  

3. Wechseln Sie zu der Registerkarte **Drittanbieterupdates**. Klicken Sie auf die Option **Updates für Drittanbietersoftware aktivieren**. Weitere Informationen über Zertifikatoptionen finden Sie unter [Verbesserungen zum aktivieren der Unterstützung von Drittanbietersoftware-Updates](capabilities-in-technical-preview-1805.md#improvements-for-enabling-third-party-software-update-support).  

   > [!Note]  
   > Wenn Sie die Standardoption von Configuration Manager zum Verwalten dieses Zertifikats verwenden, wird ein neues Zertifikat vom Typ **Third-party WSUS Signing** (Drittanbieter-WSUS-Signatur) im Knoten **Zertifikate** unter **Sicherheit** im Arbeitsbereich **Verwaltung** erstellt.  


#### <a name="phase-2-subscribe-to-a-third-party-catalog-and-sync-updates"></a>Phase 2: Abonnieren von Drittanbieterkatalogen und Synchronisierungsupdates
Führen Sie die folgenden Schritte für *jeden Drittanbieterkatalog* aus, den Sie abonnieren möchten:  

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**. Erweitern Sie **Softwareupdates**, und klicken Sie auf den Knoten **Katalog mit Updates für Drittanbietersoftware**.  

2. Wählen Sie den zu abonnierenden Katalog aus, und klicken Sie im Menüband auf **Katalog abonnieren**.   

3. Überprüfen und genehmigen Sie das Katalogzertifikat.  

   > [!Note]  
   > Wenn Sie einen Katalog mit Updates für Drittanbietersoftware abonnieren, wird das Zertifikat, das Sie im Assistenten überprüfen und genehmigen, dem Standort hinzugefügt. Dieses Zertifikat ist vom Typ **Katalog mit Updates für Drittanbietersoftware**. Sie können es über den Knoten **Zertifikate** unter **Sicherheit** im Arbeitsbereich **Verwaltung** verwalten.  

4. Schließen Sie den Assistenten ab.  

   > [!Tip]  
   > Nach dem ersten Abonnement sollte der Katalog sofort heruntergeladen werden. Es wird in diesem Release dann alle 24 Stunden erneut synchronisiert. Wenn Sie nicht darauf warten möchten, dass der Katalog automatisch heruntergeladen wird, klicken Sie im Menüband auf **Jetzt synchronisieren**.  
   > 
   > Nachdem der Katalog heruntergeladen wurde, müssen die Produktmetadaten mit dem Softwareupdatepunkt synchronisiert werden. Weitere Informationen zu diesem Prozess und dazu, wie Sie ihn manuell initiieren, finden Sie unter [Synchronisieren von Softwareupdates](../../sum/get-started/synchronize-software-updates.md). An diesem Punkt können Sie sehen, dass alle Updates von Drittanbietern im Knoten **Alle Updates** angezeigt werden. 

5. Konfigurieren Sie als nächstes den Softwareupdatepunkt **Produkte** für den Drittanbieterkatalog, den Sie abonniert haben. Weitere Informationen finden Sie unter [Konfigurieren der zu synchronisierenden Klassifizierungen und Produkte](../../sum/get-started/configure-classifications-and-products.md). Nach den Änderungen der Produktkriterien muss eine weitere Softwareupdatesynchronisierung stattfinden.

Bevor Sie die Kompatibilitätsergebnisse von Clients sehen können, müssen sie diese Updates überprüfen und auswerten. Sie können diesen Zyklus über die Configuration Manager-Systemsteuerung auf einem Client manuell auslösen, indem Sie die Aktion **Überprüfungszyklus für Softwareupdates** ausführen. Weitere Informationen zum Prozess finden Sie unter [Einführung zu Softwareupdates](../../sum/understand/software-updates-introduction.md).


#### <a name="phase-3-deploy-third-party-software-updates"></a>Phase 3: Bereitstellen von Updates für Drittanbietersoftware
Führen Sie die folgenden Schritte für *alle Drittanbietersoftware-Updates* aus, die für Clients bereitgestellt werden sollen:  

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**. Erweitern Sie **Softwareupdates**, und klicken Sie auf den Knoten **Alle Softwareupdates**.  

   > [!Tip]  
   > Klicken Sie auf **Kriterien hinzufügen**, um die Liste von Updates zu filtern. Fügen Sie zum Beispiel für **Adobe Systems, Inc.** **Hersteller** hinzu, um alle Updates von Adobe anzuzeigen.  

2. Wählen Sie die Updates aus, die für Clients erforderlich sind. Klicken Sie auf **Softwareupdateinhalte von Drittanbietern veröffentlichen**, und überprüfen Sie den Fortschritt in „SMS_ISVUPDATES_SYNCAGENT.log“. Diese Aktion lädt die Updatebinärdateien vom Hersteller herunter und speichert sie im Ordner „WSUSContent“ auf dem Softwareupdatepunkt. Außerdem wird der Status des Updates von „nur Metadaten“ in „mit Inhalt und bereitstellbar“ geändert.  

   > [!Note]  
   > Wenn Sie Softwareupdateinhalte von Drittanbietern veröffentlichen, werden alle zum Signieren des Inhalts verwendete Zertifikate dem Standort hinzugefügt. Diese Zertifikate sind vom Typ **Inhalt von Updates für Drittanbietersoftware**. Sie können sie über den Knoten **Zertifikate** unter **Sicherheit** im Arbeitsbereich **Verwaltung** verwalten.  

3. Stellen Sie die Updates mithilfe des vorhandenen Verwaltungsprozesses für Softwareupdates bereit. Weitere Informationen finden Sie unter [Bereitstellen von Softwareupdates](../../sum/deploy-use/deploy-software-updates.md). Wählen Sie auf der Seite **Download Locations** (Downloadpfade) des Assistenten zum Bereitstellen von Softwareupdates die Standardoption **Softwareupdates aus dem Internet herunterladen** aus. In diesem Szenario ist der Inhalt bereits für den Softwareupdatepunkt bereitgestellt, der dazu genutzt wird, den Inhalt für das Bereitstellungspaket herunterzuladen.


### <a name="monitoring-progress-of-third-party-software-updates"></a>Überwachen des Fortschritts von Updates für Drittanbietersoftware
Die Synchronisierung von Updates für Drittanbietersoftware wird auf dem Standortserver von der Komponente SMS_ISVUPDATES_SYNCAGENT verarbeitet. Sie können die Statusmeldungen von dieser Komponente oder ausführlichere Statusinformationen in „SMS_ISVUPDATES_SYNCAGENT.log“ sehen. Dieses Protokoll befindet sich auf dem Standortserver im Unterordner **Protokolle** des Standortinstallationsverzeichnisses. Der Pfad ist standardmäßig `C:\Program Files\Microsoft Configuration Manager\Logs`. Weitere Informationen über das Überwachen des allgemeinen Verwaltungsprozesses für Softwareupdates finden Sie unter [Überwachen von Softwareupdates](../../sum/deploy-use/monitor-software-updates.md).


### <a name="known-issues"></a>Bekannte Probleme
- Der Synchronisierungsdienst für Drittanbietersoftware-Updates unterstützt nicht den Softwareupdatepunkt, der für die Verwendung eines **Verbindungskontos für WSUS-Server** konfiguriert ist. Wenn dieses Konto auf der Registerkarte **Proxy- und Kontoeinstellungen** der Eigenschaftenseite des Softwareupdatepunkts konfiguriert wird, wird die folgende Fehlermeldung in „SMS_ISVUPDATES_SYNCAGENT.log“ angezeigt:  
`WSUS access account appears to be configured, it is not yet supported for third party updates sync.`  
Weitere Informationen über dieses Konto finden Sie unter [Verbindungskonto des Softwareupdatepunkts](../plan-design/hierarchy/accounts.md#software-update-point-connection-account).<!--515492-->  

- Verwenden Sie andere Tools (z.B. SCUP) nicht mit diesem neu integrierten Feature für Drittanbietersoftware-Updates. Der Synchronisierungsdienst für Drittanbietersoftware-Updates kann Inhalte nicht für Updates bereitstellen, die nur Metadaten enthalten und über eine andere Anwendung, ein anderes Tool oder Skript (z.B. SCUP) zu WSUS hinzugefügt wurden. Die Aktion **Softwareupdateinhalte von Drittanbietern veröffentlichen** schlägt für diese Updates fehl. Wenn Sie Updates von Drittanbietern bereitstellen müssen, die noch nicht von diesem Feature unterstützt werden, verwenden Sie den vorhandenen Prozess vollständig für die Bereitstellung dieser Updates.<!--515497-->  



## <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Konfigurieren von Windows Defender SmartScreen-Einstellungen für Microsoft Edge
<!--1353701-->
In diesem Release werden der [Konformitätsrichtlinie für Microsoft Edge-Browsereinstellungen](../../compliance/deploy-use/browser-profiles.md) drei Einstellungen für [Windows Defender SmartScreen](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview) hinzugefügt. Die Richtlinie enthält nun die folgenden zusätzlichen Einstellungen auf der Seite **SmartScreen-Einstellungen**:
- **SmartScreen zulassen:** Gibt an, ob Windows Defender SmartScreen zugelassen wird. Weitere Informationen finden Sie unter [AllowSmartScreen browser policy (Browserrichtlinie „AllowSmartScreen“)](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen).
- **Benutzer können SmartScreen-Aufforderung für Websites außer Kraft setzen:** Gibt an, ob Benutzer die Windows Defender SmartScreen-Filterwarnungen zu potenziell schädlichen Websites außer Kraft setzen können. Weitere Informationen finden Sie unter [PreventSmartScreenPromptOverride browser policy (Browserrichtlinie „PreventSmartScreenPromptOverride“)](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride).
- **Benutzer können SmartScreen-Aufforderung für Dateien außer Kraft setzen:** Gibt an, ob Benutzer die Windows Defender SmartScreen-Filterwarnungen zum Herunterladen nicht überprüfter Dateien außer Kraft setzen können. Weitere Informationen finden Sie unter [PreventSmartScreenPromptOverride browser policy (Browserrichtlinie „PreventSmartScreenPromptOverrideForFiles“)](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles).



## <a name="sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device"></a>Synchronisieren von MDM-Richtlinien von Microsoft Intune für ein gemeinsam verwaltetes Gerät
<!--1357377-->
Ab diesem Release synchronisieren die gemeinsam verwalteten Geräte automatisch die MDM-Richtlinie von Microsoft Intune, wenn Sie [eine gemeinsam verwaltete Workload anpassen](../../comanage/how-to-switch-workloads.md). Diese Synchronisierung findet auch statt, wenn Sie die Aktion **Computerrichtlinie herunterladen** aus den Clientbenachrichtigungen in der Configuration Manager-Konsole auslösen. Weitere Informationen finden Sie unter [So lösen Sie den Clientrichtlinienabruf mithilfe der Clientbenachrichtigung aus](../clients/manage/manage-clients.md#BKMK_PolicyRetrieval).



## <a name="transition-office-365-workload-to-intune-using-co-management"></a>Übertragen der Office 365-Workload auf Intune mithilfe der Co-Verwaltung
<!--1357841-->
Sie können jetzt die Office 365-Workload von Configuration Manager in Microsoft Intune übertragen, nachdem Sie die Co-Verwaltung aktiviert haben. Wechseln Sie für den Übergang dieser Workload zur Eigenschaftenseite für die Co-Verwaltung, und bewegen Sie den Schieberegler von Configuration Manager zu Pilot oder Alle. Weitere Informationen finden Sie unter [Co-Verwaltung für Windows 10-Geräte](../../comanage/overview.md).

Außerdem gibt es die neue globale Bedingung **Are Office 365 applications managed by Intune on the device** (Office 365-Anwendungen auf dem Gerät mit Intune verwalten). Diese Bedingung wird neuen Office 365-Anwendungen standardmäßig als Anforderung hinzugefügt. Wenn Sie diese Workload übertragen, entsprechen gemeinsam verwaltete Clients nicht den Anforderungen der Anwendung, weshalb Sie Office 365 nicht über Configuration Manager installieren sollten.

### <a name="known-issue"></a>Bekanntes Problem
- Dieser Workloadübergang gilt derzeit nur für Office 365-Bereitstellungen. Office 365-Updates werden weiterhin von Configuration Manager verwaltet.<!--510876--> Weitere Informationen, einschließlich einer möglichen Problemumgehung, finden Sie in den Anmerkungen zu Configuration Manager Version 1802 unter [Changing Office 365 client setting doesn’t apply (Das Ändern einer Office 365-Clienteinstellung wird nicht übernommen)](../servers/deploy/install/release-notes.md).



## <a name="package-conversion-manager"></a>Package Conversion Manager 
<!--1357861-->
Der Paketkonvertierungs-Manager ist nun ein integriertes Tool, mit dem Sie Legacypakete von Configuration Manager 2007 in Configuration Manager-Anwendungen (Current Branch) konvertieren können. Anschließend können Sie Features von Anwendungen verwenden, z.B. Abhängigkeiten, Anforderungsregeln und Affinität zwischen Benutzer und Gerät.

> [!Tip]  
> Ältere Dokumentationen zu vorhandenen Funktionen im Paketkonvertierungs-Manager stehen auf [TechNet](https://technet.microsoft.com/library/hh531519.aspx) zur Verfügung. Relevante Informationen werden derzeit zur docs.microsoft.com-Bibliothek migriert.

### <a name="try-it-out"></a>Probieren Sie es aus!
 Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie uns anschließend Ihr [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback), und lassen Sie uns wissen, wie es gelaufen ist.

> [!Important]  
> Wenn Sie bereits eine ältere Version des Paketkonvertierungs-Managers installiert haben, deinstallieren Sie diese, bevor Sie Ihren Standort aktualisieren. Die neue integrierte Version erfordert keine Installation, jedoch kann ein Konflikt mit vorhandenen Versionen auftreten.  

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**. Erweitern Sie **Anwendungsverwaltung**, und klicken Sie auf **Pakete**.  
2. Wählen Sie ein Paket aus. Die folgenden drei Optionen stehen Ihnen in der Menübandgruppe **Paketkonvertierung** zu Verfügung:  
     - **Paket analysieren:** Startet den Konvertierungsprozess durch Analysieren des Pakets.
     - **Paket konvertieren:** Einige Pakete können mit dieser Aktion problemlos in Anwendungen konvertiert werden.
     - **Korrigieren und konvertieren:** Bei einigen Paketen müssen Fehler behoben werden, bevor sie in Anwendungen konvertiert werden können.  

   Weitere Informationen zu diesen Aktionen finden Sie unter [Analysieren und Konvertieren von Paketen](https://docs.microsoft.com/previous-versions/system-center/system-center-2012-R2/hh846244%28v%3dtechnet.10%29).  

3. Navigieren Sie zum Arbeitsbereich **Überwachung**, und wählen Sie **Package Conversion Status** (Status der Paketkonvertierung) aus. Das neue Dashboard zeigt die Gesamtanalyse und den Konvertierungsstatus der Pakete im Standort an. Eine neue Hintergrundaufgabe fasst die Daten der Analyse automatisch zusammen.  

   > [!Tip]  
   > Sie müssen keinen Zeitplan für die Analyse von Paketen für den Paketkonvertierungs-Manager einrichten. Diese Aktion wird nun vom integrierten Zusammenfassungstask verarbeitet.  

![Screenshot des Dashboards für den Status der Paketkonvertierung](media/1357861-pcm-dashboard.png)



## <a name="deploy-software-updates-without-content"></a>Bereitstellen von Softwareupdates ohne Inhalt
<!--1357933-->
Sie können Softwareupdates nun auf Geräten bereitstellen, ohne zuvor Softwareupdateinhalte herunterladen und an Verteilungspunkte verteilen zu müssen. Dieses Feature ist nützlich, wenn Sie mit großen Updateinhalten arbeiten, oder wenn Clients den Inhalt immer vom Microsoft Update-Clouddienst erhalten sollen. Clients können den Inhalt in diesem Szenario auch von Peers herunterladen, die bereits über den erforderlichen Inhalt verfügen. Der Configuration Manager-Client verwaltet weiterhin den Inhaltsdownload und kann deshalb das Feature „Peercache“ von Configuration Manager oder andere Technologien verwenden, z.B. die Übermittlungsoptimierung. Dieses Feature unterstützt alle Updatetypen, die von der Configuration Manager-Softwareupdateverwaltung unterstützt werden, einschließlich Windows- und Office-Updates. 

### <a name="try-it-out"></a>Probieren Sie es aus!
 Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie uns anschließend Ihr [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback), und lassen Sie uns wissen, wie es gelaufen ist.

1. Starten Sie wie gewohnt die Softwareupdatebereitstellung. Weitere Informationen finden Sie unter [Bereitstellen von Softwareupdates](../../sum/deploy-use/deploy-software-updates.md).
2. Wählen Sie auf der Seite **Bereitstellungspaket** des Assistenten zum Bereitstellen von Softwareupdates die neue Option **No deployment package** (Kein Bereitstellungspaket) aus.

### <a name="known-issues"></a>Bekannte Probleme
- Das Symbol für ein Update, das mit dieser Einstellung bereitgestellt wurde, wird fälschlicherweise mit einem roten X angezeigt, als wäre das Update ungültig. Weitere Informationen finden Sie unter [Icons for software updates (Symbole für Softwareupdates)](../../sum/understand/software-updates-icons.md). <!--515556-->  
- Diese Einstellung ist nur in den Assistenten zum Bereitstellen von Softwareupdates integriert. Sie ist derzeit nicht mit automatischen Bereitstellungsregeln verfügbar. <!--515558-->  



## <a name="office-customization-tool-integration-with-the-office-365-installer"></a>Integration des Office-Anpassungstools in den Office 365-Installer
<!--1358149-->
Das Office-Anpassungstool ist jetzt in das Office 365-Installer in der Configuration Manager-Konsole integriert. Beim Erstellen einer Bereitstellung für Office 365 können Sie die neuesten Verwaltungseinstellungen von Office konfigurieren. Das Office-Anpassungstool wird mit der Veröffentlichung neuer Builds von Office 365 aktualisiert. Sie können jetzt neue Verwaltungseinstellungen in Office 365 verwenden, sobald sie verfügbar sind. 

### <a name="prerequisites"></a>Voraussetzungen
- Der Computer, auf dem die Configuration Manager-Konsole ausgeführt wird, erfordert Internetzugriff über den HTTPS-Port 443. Der Office 365-Installations-Assistent verwendet eine Standardwebbrowser-API von Windows zum Öffnen von https://config.office.com. Wenn ein Internetproxy verwendet wird, muss der Benutzer auf diese URL zugreifen können.

### <a name="try-it-out"></a>Probieren Sie es aus!
 Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie uns anschließend Ihr [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback), und lassen Sie uns wissen, wie es gelaufen ist.

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, und klicken Sie auf den Knoten **Office 365-Clientverwaltung**.
2. Klicken Sie im Dashboard auf die Kachel **Office 365-Installationsprogramm**, um den Office 365-Installations-Assistenten zu starten. Weitere Informationen finden Sie unter [Bereitstellen von Office 365-Apps](../../sum/deploy-use/manage-office-365-proplus-updates.md#deploy-office-365-apps).
3. Klicken Sie auf der Seite **Office-Einstellung** auf **Go To Office Web Page** (Zur Office-Webseite wechseln). Verwenden Sie das Office-Onlineanpassungstool, um Einstellungen für diese Bereitstellung anzugeben. 
4. Klicken Sie in der oberen rechten Ecke auf **Senden**, wenn Sie fertig sind. Beenden Sie den Office 365-Installations-Assistenten.



## <a name="improvements-to-cloud-management-gateway"></a>Verbesserungen am Cloudverwaltungsgateway
Dieses Release umfasst folgende Verbesserungen am Cloudverwaltungsgateway:

### <a name="simplified-client-bootstrap-command-line"></a>Vereinfachte Befehlszeile für das Clientbootstrapping
<!--1358215-->
Bei der Installation des Configuration Manager-Clients im Internet über das Cloudverwaltungsgateway sind jetzt weniger Befehlszeileneigenschaften erforderlich. Ein Beispiel dieses Szenarios finden Sie unter [Befehlszeile zum Installieren von Configuration Manager-Clients](../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client) bei der Vorbereitung auf die Co-Verwaltung. 

Die folgenden Befehlszeileneigenschaften sind in allen Szenarios erforderlich:
- CCMHOSTNAME  
- SMSSITECODE  

Die folgenden Eigenschaften sind erforderlich, wenn Sie anstelle von PKI-basierten Clientauthentifizierungszertifikaten Azure AD für die Clientauthentifizierung verwenden:
- AADCLIENTAPPID  
- AADRESOURCEURI  

Die folgende Eigenschaft ist erforderlich, wenn der Client ins Intranet wechselt:
- SMSMP  

Das folgende Beispiel enthält alle der obigen Eigenschaften:   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

Weitere Informationen finden Sie unter [Informationen zu Clientinstallationseigenschaften](../clients/deploy/about-client-installation-properties.md).

### <a name="download-content-from-a-cmg"></a>Herunterladen von Inhalten von einem Cloudverwaltungsgateway
<!--1358651-->
Zuvor mussten Sie einen Cloudverteilungspunkt und ein Cloudverwaltungsgateway als separate Rollen bereitstellen. In diesem Release kann ein Cloudverwaltungsgateway Inhalte für Clients bereitstellen. Diese Funktion reduziert die erforderlichen Zertifikate und Kosten für Azure-VMs. Aktivieren Sie die neue Option **Allow CMG to function as a cloud distribution point and serve content from Azure storage** (Cloudverwaltungsgateway erlauben, als Cloudverteilungspunkt zu fungieren und Inhalt aus Azure Storage bereitzustellen) auf der Registerkarte **Einstellungen** der Eigenschaften des Cloudverwaltungsgateways. 

### <a name="trusted-root-certificate-isnt-required-with-azure-ad"></a>Das vertrauenswürdige Stammzertifikat ist mit Azure AD nicht erforderlich
<!--503899-->
Wenn Sie ein Cloudverwaltungsgateway erstellen, müssen Sie kein [vertrauenswürdiges Stammzertifikat](../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_cmgroot) auf der Seite „Einstellungen“ angeben. Dieses Zertifikat ist nicht erforderlich, wenn Sie Azure Active Directory (Azure AD) für die Clientauthentifizierung verwenden. Früher war es im Assistenten erforderlich.

> [!Important]  
> Wenn Sie PKI-Clientauthentifizierungszertifikate verwenden, müssen Sie weiterhin ein vertrauenswürdiges Stammzertifikat für das Cloudverwaltungsgateway hinzufügen.



## <a name="improvements-to-secure-client-communications"></a>Verbesserungen an der sicheren Clientkommunikation
<!--1358278,1358279-->
Dieses Release führt [verbesserte und sichere Clientkommunikation](capabilities-in-technical-preview-1805.md#improved-secure-client-communications) fort, indem zusätzliche Abhängigkeiten vom Netzwerkzugriffskonto entfernt werden. Wenn Sie die neue Standortoption **Für HTTP-Websitesysteme von Configuration Manager generierte Zertifikate verwenden** aktivieren, erfordern die folgenden Szenarios keine Netzwerkzugriffskonten zum Herunterladen von Inhalten von einem Verteilungspunkt:  

- Tasksequenzen, die über ein Bootmedium oder über PXE ausgeführt werden
- Tasksequenzen, die über das Softwarecenter ausgeführt werden  

Diese Tasksequenzen können für die Betriebssystembereitstellung oder benutzerdefinierte Bereitstellung verwendet werden. Sie werden auch von Arbeitsgruppencomputern unterstützt.



## <a name="software-center-infrastructure-improvements"></a>Verbesserungen an der Infrastruktur des Softwarecenters
<!--1358309-->
Es werden keine Anwendungskatalogrollen mehr benötigt, um für Benutzer verfügbare Anwendungen im Softwarecenter anzuzeigen. Diese Änderung hilft dabei, die erforderliche Serverinfrastruktur zu reduzieren, um Anwendungen schneller für Benutzer bereitzustellen. Softwarecenter verlässt sich nun auf den Verwaltungspunkt, um diese Informationen abzurufen, weshalb größere Umgebungen besser skaliert werden, da sie [Begrenzungsgruppen](../servers/deploy/configure/boundary-groups.md#management-points) zugewiesen werden.

### <a name="try-it-out"></a>Probieren Sie es aus!
 Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie uns anschließend Ihr [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback), und lassen Sie uns wissen, wie es gelaufen ist.

1. Entfernen Sie alle Anwendungskatalogrollen vom Standort. Zu diesen Rollen gehört der Anwendungskatalog-Webdienstpunkt und der Anwendungskatalog-Websitepunkt.
2. Stellen Sie eine Anwendung als für eine Benutzersammlung verfügbar bereit.
3. Verwenden Sie Softwarecenter als Zielbenutzer, um nach der Anwendung zu suchen, diese anzufordern und zu installieren.

### <a name="known-issue"></a>Bekanntes Problem
- Wenn Sie einen in Azure Active Directory eingebundenen Client mit diesem Feature verwenden, legen Sie die Konfiguration des Standorts nicht auf **Für HTTP-Websitesysteme von Configuration Manager generierte Zertifikate verwenden** fest. Derzeit besteht ein Konflikt mit diesem Feature.<!--515846--> Weitere Informationen zu dieser Einstellung finden Sie unter [Verbesserte sichere Clientkommunikation](capabilities-in-technical-preview-1805.md#improved-secure-client-communications).



## <a name="provision-windows-app-packages-for-all-users-on-a-device"></a>Bereitstellen von Windows-App-Paketen für alle Benutzer auf einem Gerät
<!--1358310-->
Sie können jetzt eine Anwendung mit einem Windows-App-Paket für alle Benutzer auf dem Gerät bereitstellen. Ein allgemeines Beispiel für dieses Szenario ist das Bereitstellen einer App aus dem Microsoft Store für Unternehmen und Bildungseinrichtungen, z. B. Minecraft: Education Edition, für alle Geräte, die von Kursteilnehmer einer Bildungseinrichtung verwendet werden. Zuvor hat Configuration Manager die Installation solcher Anwendungen nur für einzelne Benutzer unterstützt. Wenn ein Schüler sich an einem neuen Gerät anmeldet, musste er warten, bevor er auf eine App zugreifen konnte. Wenn die App nun für das Gerät für alle Benutzer bereitgestellt wird, können sie schneller produktiv sein.

> [!Important]  
> Beachten Sie bei der Installation, Bereitstellung und Aktualisierung, dass verschiedene Versionen des gleichen Windows-App-Pakets auf einem Gerät zu unerwarteten Ergebnissen führen können. Dieses Verhalten kann auftreten, wenn Sie Configuration Manager zum Bereitstellen der App verwenden, aber dann zulassen, dass Benutzer die App über den Microsoft Store aktualisieren können. Weitere Informationen finden Sie im Abschnitt „Nächste Schritte“ unter [Verwalten von Apps aus dem Microsoft Store für Unternehmen](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md#next-steps).  

Wenn Sie eine offline lizenzierte App bereitstellen, lässt Configuration Manager nicht zu, dass Windows die App automatisch über den Microsoft Store aktualisiert.  

### <a name="try-it-out"></a>Probieren Sie es aus!
 Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie uns anschließend Ihr [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback), und lassen Sie uns wissen, wie es gelaufen ist.

1. Erstellen Sie eine neue Anwendung. Diese Anwendung muss aus einem Windows-App-Paket stammen oder eine offline lizenzierte App sein, die Sie über den Microsoft Store für Unternehmen und Bildungseinrichtungen synchronisiert haben.  

2. Aktivieren Sie auf der Seite **Allgemeine Informationen** des Assistenten zum Erstellen von Anwendungen die Option **Provision this application for all users on the device** (Diese Anwendung für alle Benutzer auf dem Gerät bereitstellen).  

   > [!Tip]  
   > Wenn Sie eine vorhandene Anwendung bearbeiten, befindet sich diese Einstellung auf der Registerkarte **Benutzerfreundlichkeit** der Anwendungseigenschaften.  

3. Stellen Sie die Anwendung für eine Gerätesammlung bereit.  

4. Melden Sie sich an einem Zielgerät mit verschiedenen Benutzerkonten an, und starten Sie die Anwendung.  

> [!Note]  
> Wenn Sie eine bereitgestellte Anwendung auf Geräten deinstallieren müssen, an denen sich bereits ein Benutzer angemeldet hat, müssen Sie zwei Deinstallationsbereitstellungen erstellen. Erstellen Sie die erste Deinstallationsbereitstellung für eine Gerätesammlung, die die Geräte enthält. Erstellen Sie die zweite Deinstallationsbereitstellung für eine Benutzersammlung, die die Benutzer enthält, die sich bereits an den Geräten bei der bereitgestellten Anwendung angemeldet haben. Wenn Sie eine bereitgestellte Anwendung auf einem Gerät deinstallieren, deinstalliert Windows sie nicht für die Benutzer. 



## <a name="improvements-to-the-surface-dashboard"></a>Verbesserungen am Surface-Dashboard
<!--1358654-->
Dieses Release umfasst die folgenden Verbesserungen am [Surface-Dashboard](../clients/manage/surface-device-dashboard.md):
- Das Surface-Dashboard zeigt ab sofort eine Liste der relevanten Geräte an, wenn Diagrammabschnitte ausgewählt werden.
   - Wenn Sie auf die Kachel **Prozent der Surface-Geräte** klicken, wird eine Liste der Surface-Geräte geöffnet.
   - Wenn Sie auf die Kachel **Top 5-Firmwareversionen** klicken, wird eine Liste der Surface-Geräte mit der entsprechenden Firmwareversion geöffnet.
- Wenn Sie diese Gerätelisten über das Surface-Dashboard anzeigen, können Sie mit der rechten Maustaste auf ein Gerät klicken und allgemeine Aktionen durchführen.



## <a name="hardware-inventory-default-unit-revision"></a>Überarbeitung der Standardeinheit der Hardwareinventur
<!--514442-->
In [Configuration Manager Version 1710](../plan-design/changes/whats-new-in-version-1710.md#site-infrastructure) wurde die Standardeinheit in vielen Berichtsansichten von Megabytes (MB) in Gigabytes (GB) geändert. Aufgrund von [Verbesserungen der Hardwareinventur für große ganzzahlige Werte](capabilities-in-technical-preview-1805.md#improvement-to-hardware-inventory-for-large-integer-values) und Kundenfeedback ist MB nun wieder die Standardeinheit.



## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen zur Installation oder dem Update der Technical Preview finden Sie unter [Technical Preview für Configuration Manager](technical-preview.md).    
