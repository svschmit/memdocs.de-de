---
title: Funktionen in Technical Preview 1605
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über Features, die in der Technical Preview-Version 1605 für Configuration Manager zur Verfügung stehen.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bafd028-1923-4463-9e3e-ee41bc0c437b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: 1836a4c7d08547405dad08d7e60eb108d0dfd00f
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695714"
---
# <a name="capabilities-in-technical-preview-1605-for-configuration-manager"></a>Funktionen in der Technical Preview 1605 für Configuration Manager

*Gilt für: Configuration Manager (Technical Preview-Branch)*

In diesem Artikel werden die Features vorgestellt, die in der Technical Preview-Version 1605 für Configuration Manager verfügbar sind. Sie können diese Version installieren, um neue Funktionen für Ihren Configuration Manager Technical Preview-Standort zu aktualisieren oder hinzuzufügen.      Bevor Sie diese Version der Technical Preview installieren, lesen Sie das einführende Thema [Technical Preview für Configuration Manager](../../core/get-started/technical-preview.md), um sich mit den allgemeinen Anforderungen und Einschränkungen bei der Verwendung einer Technical Preview vertraut zu machen und um zu erfahren, wie Sie Updates für Versionen durchführen und Feedback zu den Features in einer Technical Preview geben können.  

 **Bekannte Probleme in dieser Technical Preview:**  

- Mit Technical Preview 1605 erhalten Sie möglicherweise einen Konsolenfehler, der die Konsole schließt, wenn Sie die Eigenschaften eines Verwaltungspunkts aktualisieren, nachdem er installiert wurde.  Wenn dies geschieht, können Sie den Verwaltungspunkt deinstallieren, und ihn dann mit den gewünschten Einstellungen erneut installieren. Alternativ können Sie den Verwaltungspunkt vor der Installation von Technical Preview 1605 ändern.  

- Wenn Sie das Windows Store für Unternehmen-Feature mit der Technical Preview 1604 verwenden, und ein Upgrade auf Technical Preview 1605 durchführen, können Sie die Onboarding-Daten nicht mehr anzeigen. Alle anderen Funktionen können weiterhin durchgeführt werden. Wenn Sie das Onboarding mit der Technical Preview 1604 durchgeführt haben, bleibt dies nach der Installation von Technical Preview 1605 bestehen, und Sie müssen keine weiteren Maßnahmen ergreifen.  

  **Im Folgenden werden neue Features aufgelistet, die Sie mit dieser Version ausprobieren können.**  

##  <a name="per-app-vpn-for-windows-10-devices"></a><a name="BKMK_PerAppVPN"></a> VPN pro App für Windows 10-Geräte  
 Für Windows 10-Geräte, die mithilfe von Configuration Manager mit Intune verwaltet werden, können Sie eine Liste von Apps hinzufügen, die automatisch eine VPN-Verbindung öffnen, die Sie über die Configuration Manager-Verwaltungskonsole konfiguriert haben. Sie haben die Möglichkeit, den VPN-Datenverkehr auf diese Apps zu beschränken, oder Sie können weiterhin den gesamten Datenverkehr über die VPN-Verbindung ermöglichen.  

 **Anforderungen**:  

-   Configuration Manager mit Intune  

-   Ein Windows 10-VPN-Profil, das für mindestens ein Gerät bereitgestellt wurde  

##  <a name="improvements-to-the-install-software-updates-task-sequence"></a><a name="BKMK_InstallSU"></a> Verbesserungen an der Tasksequenz „Softwareupdates installieren“  
 Die folgenden Verbesserungen wurden an der Tasksequenz „Softwareupdates installieren“ durchgeführt:  

-   Eine neue Tasksequenzvariable, „SMSTSSoftwareUpdateScanTimeout“, steht Ihnen zur Verfügung. Mit ihr können Sie das Timeout für die Softwareupdateprüfung während des Tasksequenzschritts „Softwareupdates installieren“ kontrollieren. Der Standardwert beträgt 30 Minuten.  

-   Es wurden Verbesserungen für die Protokollierung durchgeführt. Die Protokolldatei „smsts.log“ wird neue Protokolleinträge enthalten, die auf andere Protokolldateien verweisen, die Sie bei der Problembehandlung während der Installation der Softwareupdates unterstützen.  

##  <a name="improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step"></a><a name="BKMK_PrepareConfigMgrClient"></a> Verbesserungen am Tasksequenzschritt „ConfigMgr-Client für Erfassung vorbereiten“  
 Im Schritt „Configuration Manager-Client vorbereiten“ wird der Configuration Manager-Client nun vollständig entfernt, und nicht nur die wichtigen Informationen. Wenn die Tasksequenz das erfasste Betriebssystemimage bereitstellt, wird jedes Mal ein neuer Configuration Manager-Client installiert.  

##  <a name="grace-period-for-required-application-deployments"></a><a name="BKMK_Grace"></a> Karenzzeit für die erforderlichen Anwendungsbereitstellungen  
 In einigen Fällen empfiehlt es sich, Benutzern mehr Zeit zum Installieren von erforderlichen Anwendungsbereitstellungen zu geben, über die von Ihnen konfigurierten Fristen hinaus. Wenn z.B. ein Endbenutzer gerade aus dem Urlaub zurückgekehrt ist, muss er möglicherweise sehr lange warten, bis überfällige Anwendungsbereitstellungen installiert werden. Sie können jedoch die Anwendung weiterhin zu einem beliebigen Zeitpunkt installieren.  

 Sie können jetzt eine **Karenzzeit** definieren, um dieses Problem zu lösen. Dafür müssen Sie die Configuration Manager-Clienteinstellungen für eine Sammlung bereitstellen.  

 Führen Sie folgende Aktionen aus, um die Karenzzeit zu konfigurieren:  

1. Auf der Seite **Computer-Agent** der Clienteinstellungen müssen Sie die neue Eigenschaft **Karenzzeit für Erzwingung nach Bereitstellungsfrist (Stunden)** mit einem Wert zwischen **1** und **120** Stunden konfigurieren.  

2. Aktivieren Sie in einer neuen Anwendungsbereitstellung oder in den Eigenschaften einer vorhandenen Bereitstellung auf der Seite **Planung** das Kontrollkästchen **Erzwingung für diese Bereitstellung basierend auf den Benutzereinstellungen innerhalb der Karenzzeit verzögern**, bis zu der Karenzzeit, die in den Clienteinstellungen definiert ist.  

    Alle Bereitstellungen, für die dieses Kontrollkästchen ausgewählt ist, und die für Geräte vorgesehen sind, für die Sie ebenfalls die Clienteinstellungen bereitgestellt haben, werden die Karenzzeit verwenden.  

   In diesem Release wird die Karenzzeit, die Sie konfigurieren, nicht von Clientgeräten verwendet. Wenn Sie eine Karenzzeit konfigurieren und das Kontrollkästchen aktivieren, wird die Anwendung im ersten, nicht geschäftlichen Fenster installiert werden, das der Benutzer nach Ablauf der Frist konfiguriert.  

   Ähnliche Optionen wurden zum Bereitstellungsassistenten für Softwareupdates, zum Assistenten für automatische Bereitstellungsregeln und den Eigenschaftenseiten hinzugefügt. Jedoch sind diese zur Zeit nicht in dieser Technical Preview implementiert.  

##  <a name="new-experience-for-remote-device-actions"></a><a name="BKMK_Remote"></a> Benutzerfreundlichere Remotegeräteaktionen  
 Die Ausführung von Remotegeräteaktionen über die Configuration Manager-Konsole wurde benutzerfreundlicher gestaltet und verbessert.  
Häufig verwendete Aktionen, wie z.B. **Abkoppeln/Zurücksetzen**, **Kennung zurücksetzen**, **Remotesperre** und **Aktivierungssperre umgehen**, befinden sich nun im Menü **Remotegeräteaktionen**, auf das Sie über den Arbeitsbereich **Bestand und Kompatibilität** zugreifen können.  

 ![Screenshot, der die neuen Remotegeräteaktionen anzeigt](media/New-Remote-Device-Actions.png)  

 Sie finden den Status für jeden dieser Vorgänge an den folgenden Stellen:  

- Im Detailbereich, bei der Auswahl eines Geräts aus dem Knoten **Geräte**.  

- Auf der Seite **Eigenschaften** für ein Gerät.  

- Auf der Hauptseite des Knotens **Geräte** (möglicherweise sind nicht alle Spalten standardmäßig sichtbar).  

##  <a name="windows-store-for-business-apps"></a><a name="BKMK_WSFB"></a> Windows Store für Unternehmen-Apps  
 Im [Windows Store für Unternehmen](https://www.microsoft.com/business-store) können Sie Apps für Ihre Organisation finden und entweder einzeln oder per Volumenlizenz erwerben. Indem Sie den Store mit Configuration Manager verbinden, können Sie per Volumenlizenz erworbene Apps in der Configuration Manager-Konsole verwalten, zum Beispiel:  

- Sie können die Liste der erworbenen Apps mit Configuration Manager synchronisieren  

- Synchronisierte Apps werden in der Configuration Manager-Konsole angezeigt, und Sie können sie wie alle anderen Apps bereitstellen  

- Configuration Manager lädt alle 24 Stunden App-Lizenzinformationen aus dem Store herunter, und Sie können diese in der Configuration Manager-Konsole überprüfen  

  In Technical Preview Release 1604 konnten Sie Apps aus dem Windows Store für Unternehmen in der Configuration Manager-Konsole synchronisieren und anzeigen. In diesem Release haben wir die Möglichkeit zum Erstellen und Bereitstellen von Configuration Manager-Anwendungen von synchronisierten Store-Apps hinzugefügt.  

### <a name="set-up-windows-store-for-business-synchronization"></a>Einrichten der Synchronisierung mit Windows Store für Unternehmen  

1.  Registrieren Sie Configuration Manager als „Webanwendung und/oder Web-API“-Verwaltungstool in Azure Active Directory. Sie erhalten eine Client-ID, die Sie später benötigen.  

    1.  Wählen Sie im Active Directory-Knoten von [https://manage.windowsazure.com](https://manage.windowsazure.com) Ihr Azure Active Directory aus, und klicken Sie dann auf **Anwendungen** > **Hinzufügen**.  

    2.  Klicken Sie auf **Eine von meinem Unternehmen entwickelte Anwendung hinzufügen**.  

    3.  Geben Sie einen Namen für die Anwendung ein, wählen Sie **Webanwendung** und/oder **Web-API** aus, und klicken Sie anschließend auf den Pfeil **Weiter**.  

    4.  Geben Sie die gleiche URL für die **Registrierungs-URL** und die **App-ID-URI** ein. Dabei kann es sich um eine beliebige URL handeln, die nicht in eine reale Adresse aufgelöst werden muss. Sie können z.B. **https://&lt;Ihre Domäne>/sccm** eingeben.  

    5.  Schließen Sie den Assistenten ab.  

2.  Erstellen Sie in Azure Active Directory einen Clientschlüssel für das registrierte Verwaltungstool.  

    1.  Markieren Sie die App, die Sie soeben erstellt haben, und klicken Sie auf **Konfigurieren**.  

    2.  Wählen Sie unter **Schlüssel** eine Dauer aus der Liste aus, und klicken Sie anschließend auf **Speichern**. Dadurch wird ein neuer Clientschlüssel erstellt. Verlassen Sie diese Seite nicht, bevor Sie Windows Store für Unternehmen erfolgreich in Configuration Manager eingebunden haben.  

3.  Konfigurieren von Configuration Manager als Speicherverwaltungstool im Windows Store für Unternehmen.  

    1.  Öffnen Sie [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/managementtools), und melden Sie sich an, wenn Sie dazu aufgefordert werden.  

    2.  Akzeptieren Sie gegebenenfalls die Nutzungsbedingungen.  

    3.  Klicken Sie unter **Verwaltungstools** auf **Verwaltungstool hinzufügen**.  

    4.  Geben Sie unter **Tool nach Namen suchen** den Namen der App ein, die Sie zuvor in AAD erstellt haben, und klicken Sie anschließend auf **Hinzufügen**.  

    5.  Klicken Sie neben der App, die Sie gerade importiert haben, auf **Aktivieren**.  

    6.  Klicken Sie im Assistenten **Offline lizenzierte Apps anzeigen** auf **Ja**, wenn Sie den Erwerb offline lizenzierter Apps zulassen möchten.  

4.  Kaufen Sie mindestens eine App aus dem Windows Store für Unternehmen.  

5.  Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** den Eintrag **Clouddienste**, und klicken Sie dann auf **Windows Store für Unternehmen.**  

6.  Klicken Sie auf der Registerkarte **Start** in der Gruppe **Erstellen** auf **Konto in Windows Store für Unternehmen hinzufügen**.  

7.  Fügen Sie Mandanten-ID, Client-ID und Clientschlüssel aus Azure Active Directory hinzu, und schließen Sie den Assistenten ab.  

8.  Sobald Sie fertig sind, wird das von Ihnen konfigurierte Konto in der Liste **Konto in Windows Store für Unternehmen** in der Configuration Manager-Konsole aufgeführt.  

### <a name="try-it-out"></a>Probieren Sie es aus!  
 Versuchen Sie, den folgenden Task auszuführen, und lassen Sie uns dann wissen, wie es funktioniert hat, indem Sie unserer Feedbackformular auf der Seite [Configuration Manager-Feedbackprogramm](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) auf der Microsoft Connect-Website ausfüllen:  

 Erstellen und Bereitstellen einer Configuration Manager-App aus einer offline lizenzierten App aus dem Windows Store für Unternehmen.  

1. Erweitern Sie im Arbeitsbereich **Softwarebibliothek** der Configuration Manager-Konsole **App-Verwaltung**, und klicken Sie anschließend auf **Lizenzinformationen für Store-Apps**.  

2. Wählen Sie zunächst die App aus, die Sie bereitstellen möchten. Klicken Sie anschließend auf der Registerkarte **Start** in der Gruppe **Erstellen** auf **Anwendung erstellen**.  

   Eine Configuration Manager-App wird erstellt, die eine App aus dem Windows Store für Unternehmen enthält. Sie können diese App dann wie jede andere Configuration Manager-App bereitstellen und überwachen.  

> [!IMPORTANT]  
>  Beim Erstellen einer Configuration Manager-App mit einem einzelnen Bereitstellungstyp aus einer offline lizenzierten App kann dies für Geräte bereitgestellt werden, die MDM-verwaltet und auch mit dem Configuration Manager-Client verwaltet werden. Wenn Sie versuchen, eine App mit mehreren Bereitstellungstypen bereitzustellen, schlägt die Installation fehl.  
>   
>  Sie können derzeit keine online lizenzierten Apps mit Configuration Manager bereitstellen.  

##  <a name="general-improvements-for-volume-purchased-apps"></a><a name="BKMK_VPP2"></a> Allgemeine Verbesserungen für per Volumenlizenz erworbene Apps  

-   In diesem Release wurden per Volumenlizenz erworbene Apps aus dem Windows Store für Unternehmen und dem iOS App-Store in der gleichen Ansicht, **Lizenzinformationen für Store-Apps**, konsolidiert.  

-   Für per Volumenlizenz erworbene iOS-Apps wurde die Registerkarte Apple Volume Purchase Program aus dem Dialogfeld **App-Paket für iOS-Browser** des Assistenten zum Erstellen von Apps entfernt. Gehen Sie folgendermaßen vor, um eine per Volumenlizenz erworbene App für iOS zu erstellen:  

    1.  1.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** der Configuration Manager-Konsole den Eintrag **Anwendungsverwaltung**, und klicken Sie anschließend auf **Lizenzinformationen für Store-Apps**.  

    2.  2.  Wählen Sie zunächst die App aus, die Sie bereitstellen möchten. Klicken Sie anschließend auf der Registerkarte **Start** in der Gruppe **Erstellen** auf **Anwendung erstellen**.  

-   Der Ort, die Sie zum Abrufen und Hochladen eines Apple VPP-Token für per Volumenlizenz erworbenen Apps in der Configuration Manager-Konsole verwenden, hat sich geändert. Sie können das jetzt im Arbeitsbereich **Admin** im Knoten **Clouddienste** > **Apple Volume Purchase Program Token** erledigen.  

##  <a name="enterprise-data-protection-edp"></a><a name="BKMK_VPP"></a> Unternehmensdatenschutz (Enterprise Data Protection; EDP)  
 Sie können Konfigurationselemente erstellen, mit denen Sie Ihre EDP-Richtlinien bereitstellen, Ihre geschützten Apps und Ihre EDP-Schutzebene auswählen, und Unternehmensdaten im Netzwerk suchen können. Weitere Informationen zu EDP finden Sie in den folgenden Themen:  

- [Schützen von Unternehmensdaten mit Windows Information Protection (WIP)](/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip)
- [Erstellen und Bereitstellen einer Windows Information Protection-Richtlinie (WIP) mithilfe von Configuration Manager](/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr)


##  <a name="end-users-can-install-apps-from-the-company-portal"></a><a name="BKMK_End"></a> Endbenutzer können Apps über das Unternehmensportal installieren.  
 Die lokale Verwaltung mobiler Geräte (MDM) wurde in Version 1511 von Configuration Manager eingeführt. In früheren Versionen konnten Sie Anwendungen für MDM-verwaltete Windows 10-Geräte mit dem Bereitstellungszweck **erforderliche Installation** für lokale, MDM-verwaltete Geräte, bereitstellen.  

 In diesem Release können Sie jetzt Apps mit dem Bereitstellungszweck **Verfügbar** für Benutzer der lokalen, MDM-verwalteten Windows-10-Computer bereitstellen, und Benutzer können diese Apps jetzt selbst aus dem Unternehmensportal installieren.
Wenn das Unternehmensportal in dieser Technical Preview länger als 15 Minuten geöffnet ist, wird dem Endbenutzer eine Fehlermeldung angezeigt. Starten Sie das Unternehmensportal neu, um das Problem zu umgehen.  

### <a name="before-you-start"></a>Vorbereitung  

#### <a name="server-prerequisites"></a>Voraussetzungen für den Server  

-   .NET 4.5 oder höher (Neustart erforderlich)  

-   PowerShell 3.0 für Konfigurationsskript (Neustart erforderlich)  

#### <a name="client-prerequisites"></a>Client-Voraussetzungen  

-   Windows 10 Desktop 1511 (OS Build 10586.218) oder höher  

#### <a name="general-prerequisites"></a>Allgemeine Voraussetzungen  

-   Stellen Sie sicher, dass Sie die [Vorbereitungsschritte für lokales MDM](../../mdm/plan-design/plan-on-premises-mdm.md) durchgeführt und [Ihre Geräte registriert](../../mdm/deploy-use/enroll-devices-on-premises-mdm.md) haben.  

-   Stellen Sie sicher, dass Configuration Manager über eine aktive Verbindung zu Microsoft Intune verfügt, um die beste Anwendungsinstallation mit dem Unternehmensportal zu garantieren.  

-   Bei Auswahl der Option „Massenregistrierung“ konfigurieren Sie die Benutzer-Gerät-Affinität für das registrierte Gerät, bevor Sie dieses Szenario ausprobieren.  

### <a name="configuration-steps"></a>Konfigurationsschritte  

#### <a name="install-the-application-catalog-roles-and-enable-mobile-device-management-support"></a>Installieren Sie die Anwendungskatalogrollen, und aktivieren Sie die Unterstützung der Verwaltung mobiler Geräte  

1.  Fügen Sie den Anwendungskatalog-Webdienst und Websiterollen hinzu  

    1.  Wählen Sie **HTTPS-Modus** und die Option **Mobilen Geräten die Verwendung dieses Anwendungskatalog-Webdienstpunkts erlauben**.  

    2.  Einschränkungen in dieser Technical Preview:  

        -   Sie müssen alle vorhandenen Anwendungskatalogrollen deinstallieren, bevor Sie die Option auswählen können, mit der mobile Geräte eine Verbindung herstellen können.  

        -   Stellen Sie sicher, dass es nur einen Satz von Anwendungskatalogrollen gibt, und dass die Rollen auf dem gleichen Standortsystem mit dem Registrierungspunkt und den Registrierungsproxypunkt-Rollen zusammengestellt werden.  

2.  Stellen Sie im Knoten Komponentenstatus in der Configuration Manager-Konsole sicher, dass die folgenden Komponenten funktionsfähig sind:  

    -   **SMS_AWEBSVC_CONTROL_MANAGER**  

    -   **SMS_DMAPPSVC_CONTROL_MANAGER**  

    -   **SMS_DMCONTENTSVC_CONTROL_MANAGER**  

    -   **SMS_PORTALWEB_CONTROL_MANAGER**  

### <a name="configure-boundaries"></a>Konfigurieren von Grenzen  
 Konfigurieren von erforderlichen Grenzen für Nur Intranet-Verteilungspunkte.  

> [!NOTE]  
>  Zu diesem Zeitpunkt werden nur IPv4-Bereichsgrenzen für die Verwaltung mobiler Geräte unterstützt.  

### <a name="deploy-the-company-portal-application-and-configuration"></a>Bereitstellen der Unternehmensportal-Anwendung und -Konfiguration  

1. Verwenden Sie das Konfigurationsskript in der Technical Preview, um die Unternehmensportal-Bereitstellung und -Konfiguration vorzubereiten:  

   1. Öffnen Sie ein erhöhtes PowerShell-Befehlsfenster.  

   2. Führen Sie **set-executionPolicy RemoteSigned** aus  

   3. Führen Sie **.\ConfigurationScript.ps1** aus dem Ordner **&lt;SCCM-Installationsverzeichnis\>\cd.latest\SMSSETUP\TOOLS\MDM** aus  

      Das Konfigurationsskript erledigt Folgendes:  

   4. Erstellt eine Configuration Manager-Anwendung mit einem Windows-App-Paketbereitstellungstyp und verwendet **CompanyPortalOnPremisesMDM.appx** im gleichen Ordner.  

   5. Erstellt ein Konfigurationselement und eine Konfigurationsbaseline, die das Unternehmensportal konfiguriert.  

   6. Stellt die Konfigurationsbaseline und die Anwendung bereit, und fügt die Anwendung auf allen Verteilungspunkten hinzu.  

   > [!NOTE]
   >  Wenn die Anwendungskatalogrollen nicht mit dem primären Standort zusammengestellt werden, müssen Sie folgende Aktionen ausführen:  
   > 
   > - Suchen Sie das Konfigurationselement **OnPremMDM Portal Configuration CI – Server-URLs** im Arbeitsbereich **Bestand und Kompatibilität**  
   >   -   Ändern Sie die den Wert **Kompatibilitätsregeln** auf den vollqualifizierten Domänennamen des Standortsystems, wo die Anwendungskatalogrollen gespeichert sind.  

2. Wenn die Unternehmensportal-Anwendung und ihre Konfiguration bereitgestellt sind, überprüfen Sie im Abschnitt **Bereitstellungen** der Configuration Manager-Konsole, ob die Anwendung und die Baselinekonfiguration für das angegebene Gerät kompatibel sind. Das Unternehmensportal erscheint als **Unternehmensportal (Technical Preview)** im Startmenü auf dem Gerät.  

### <a name="try-it-out"></a>Probieren Sie es aus!  
 Versuchen Sie, die folgenden Tasks auszuführen, und lassen Sie uns dann wissen, wie es funktioniert hat, indem Sie unserer Feedbackformular auf der Seite [Configuration Manager-Feedbackprogramm](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) auf der Microsoft Connect-Website ausfüllen:  

1.  Stellen Sie mehrere Anwendungen mit unterstützten Bereitstellungstypen mit dem Bereitstellungszweck **Verfügbar** für eine Benutzersammlung bereit. Für diese Technical Preview werden Anwendungen, für die eine Genehmigung des Administrators erforderlich ist, nicht unterstützt und nicht im Unternehmensportal angezeigt.  

2.  Benutzer können dann Anwendungen aus dem Unternehmensportal suchen und installieren.  

     Wenn Sie das Unternehmensportal geöffnet haben, sehen Sie ein Authentifizierungsdialogfeld mit dem Namen **Configuration Manager**. Geben Sie die Active Directory-Anmeldeinformationen des Benutzers an (entweder in Form von user@domain oder Domäne\Benutzer), um sich anzumelden.  

##  <a name="new-tabs-for-updates-and-operating-systems-in-software-center"></a><a name="BKMK_SW1"></a> Neue Registerkarten für Updates und Betriebssysteme im Software Center  
 In diesem Release wurden die folgenden Änderungen vorgenommen, um das Layout der Software Center-Anwendung zu verbessern:  

-   Die Registerkarte **Anwendungen** wurde in drei separate Registerkarten aufgeteilt: **Updates**, **Betriebssysteme** (die beide zuvor in der Liste **Filter** zu finden waren) und **Anwendungen**.  

##  <a name="service-a--server-group"></a><a name="BKMK_ServerGroups"></a> Bereitstellung einer Servergruppe  
 Die Technical Preview-Version 1511 für Configuration Manager enthält die Möglichkeit, eine Sammlung zu erstellen, in der alle Geräte in der Sammlung eine Servergruppe bilden. Anschließend könnten Sie die Einstellungen der Servergruppe konfigurieren, die Sie verwenden, wenn Sie Softwareupdates für die Servergruppe bereitstellen, den Prozentsatz der Computer überprüfen, die zu jedem Zeitpunkt aktualisiert werden und die PowerShell-Skripts vor und nach der Bereitstellung zur Ausführung benutzerdefinierter Aktionen konfigurieren.  

 Mit der Technical Preview-Version 1605 für Configuration Manager haben Sie ebenso die Möglichkeit, die Computer in der Servergruppe in einer bestimmten Reihenfolge, die Sie definieren, zu aktualisieren, eine erweiterte Überwachung zum Anzeigen des Status für die Computer in der Servergruppe hinzuzufügen und die Bereitstellungssperren zu deaktivieren. Dies ist hilfreich, wenn Clients die Softwareupdates nicht installieren konnten und verhindern, dass andere Clients die Softwareupdates installieren.  

### <a name="try-it-out"></a>Probieren Sie es aus!  
 Versuchen Sie, die folgenden Tasks auszuführen, und lassen Sie uns dann wissen, wie es funktioniert hat, indem Sie unserer Feedbackformular auf der Seite [Configuration Manager-Feedbackprogramm](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) auf der Microsoft Connect-Website ausfüllen:  

-   Ich kann eine Sammlung erstellen, die eine Servergruppe darstellt. Für diesen Test können Sie Ihre Sammlungsmitgliedschaftsregeln  für zwei Computer in dieser Sammlung konfigurieren.   

-   Ich kann angeben, dass Computer in der Servergruppe Softwareupdates in einer bestimmten Reihenfolge, basierend auf Servergruppeneinstellungen für die Sammlung, installieren. Verwenden Sie die Beispielskripts in der Prozedur, um die Skripts für die vor und nach der Bereitstellung auszuführenden Aktionen festzulegen.  

-   Ich kann ein Softwareupdate für diese Sammlung bereitstellen. Überprüfen Sie die in den Dateien „start.txt“ und „end.txt“ (aus dem Vorlagenskript erstellt) in „C:\temp“ und überprüfen Sie die Start- und Endzeiten für die Bereitstellung auf den Computern in der Servergruppe. In der Protokolldatei "UpdatesDeployment.log" finden Sie weitere Informationen.  

#### <a name="to-create-a-collection-for-a-server-group"></a>So erstellen Sie eine Sammlung für eine Servergruppe  

1.  [Erstellen Sie eine Gerätesammlung](../clients/manage/collections/create-collections.md), die die Computer in der Servergruppe enthält.  

2.  Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Gerätesammlungen**, klicken Sie mit der rechten Maustaste auf die Sammlung mit den Computern in der Servergruppe, und klicken Sie anschließend auf **Eigenschaften**.  

3.  Wählen Sie auf der Registerkarte **Allgemein** die Option **Alle Geräte gehören derselben Servergruppe an** aus, und klicken Sie auf **Einstellungen**.  

4.  Legen Sie auf der Seite **Servergruppeneinstellungen** eine der folgenden Einstellungen fest:  

    -   **Allow a percentage of machines to be updated at the same time** (Zulassen, dass ein bestimmter Prozentsatz der Computer gleichzeitig aktualisiert wird): Gibt an, dass nur ein bestimmter Prozentsatz von Clients gleichzeitig aktualisiert wird. Wenn eine Sammlung beispielsweise 10 Clients enthält und für die Sammlung festgelegt wurde, dass 30 % der Clients gleichzeitig aktualisiert werden, werden Softwareupdates immer nur auf 3 Clients gleichzeitig installiert.  

    -   **Allow a number of machines to be updated at the same time** (Zulassen, dass eine bestimmte Anzahl von Computern gleichzeitig aktualisiert wird): Gibt an, dass nur eine bestimmte Anzahl von Clients gleichzeitig aktualisiert wird.  

    -   **Geben Sie die Wartungssequenz an:** Gibt an, dass die Clients in der Sammlung in der von Ihnen festgelegten Reihenfolge nacheinander aktualisiert werden. Auf einem Client werden Softwareupdates erst installiert, nachdem die Installation von Softwareupdates auf dem Client abgeschlossen ist, der sich in der Liste vor diesem Client befindet.  

5.  Geben Sie an, ob ein Skript vor der Bereitstellung (Knoten sperren) oder ein Skript nach der Bereitstellung (Knoten fortsetzen) verwendet werden soll.  

    > [!TIP]  
    >  Die folgenden Beispiele können Sie beim Testen für Skripts vor und nach der Bereitstellung verwenden, die die aktuelle Uhrzeit in eine Textdatei schreiben:  
    >   
    >  **Vor der Bereitstellung**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\start.txt`  
    >   
    >  **Nach der Bereitstellung**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\end.txt`  

#### <a name="to-deploy-software-updates-to-the-server-group-and-monitor-status"></a>Bereitstellen von Softwareupdates für die Servergruppe und Überwachen des Status  

1.  [Bereitstellen von Softwareupdates](../../sum/deploy-use/deploy-software-updates.md) für die Servergruppensammlung.  

2.  [Überwachen der Softwareupdatebereitstellung](../../sum/deploy-use/monitor-software-updates.md). Zusätzlich zu den standardmäßigen Überwachungsansichten für die Bereitstellung von Softwareupdates wird eine neue Statusbeschreibung angezeigt, wenn ein Client darauf wartet, die Softwareupdates zu installieren. Für den neuen Status wird **Auf die Sperre warten** angezeigt.  

#### <a name="to-clear-the-deployment-locks-for-computers-in-a-server-group"></a>So löschen Sie die Bereitstellungssperren für Computer in einer Servergruppe  

1.  Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Gerätesammlungen** und anschließend auf die Sammlung, um Bereitstellungssperren zu löschen.  

2.  Klicken Sie auf der Registerkarte **Start** in der Gruppe **Bereitstellung** auf **Bereitstellungssperren für Servergruppe löschen**. Wenn die Softwareupdates auf einem Client nicht installiert werden konnten und dadurch die Installation der Softwareupdates auf anderen Clients verhindert wird, können die Bereitstellungssperren manuell gelöscht werden.  

##  <a name="support-for-microsoft-defender-advanced-threat-protection-service"></a><a name="BKMK_ATP"></a> Unterstützung für den Microsoft Defender Advanced Threat Protection-Dienst  
 Microsoft Defender Advanced Threat Protection (ATP) ist ein Dienst, der Unternehmen dabei unterstützt, erweiterte Angriffe auf ihre Netzwerke zu entdecken, zu untersuchen und darauf zu reagieren. Microsoft Defender ATP wurde früher als Windows Defender ATP bezeichnet. Hier finden Sie weitere Informationen zu [Microsoft Defender ATP](https://blogs.windows.com/windowsexperience/2016/03/01/announcing-windows-defender-advanced-threat-protection). Configuration Manager kann Sie beim Onboarding unterstützen, und verwaltete Windows 10 Anniversary Edition-Clientgeräte überwachen.  

### <a name="try-it-now"></a>Probieren Sie es jetzt aus!  
 Versuchen Sie, die folgenden Tasks auszuführen, und lassen Sie uns dann wissen, wie es funktioniert hat, indem Sie unserer Feedbackformular auf der Seite [Configuration Manager-Feedbackprogramm](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) auf der Microsoft Connect-Website ausfüllen:  

- Integrieren von Geräten in den Microsoft Defender ATP-Onlinedienst (Advanced Threat Protection)  

- Überwachen der Microsoft Defender ATP-Bereitstellung für verwaltete Geräte  

  **Voraussetzungen**  

- Abonnement für den Microsoft Defender Advanced Threat Protection-Onlinedienst  

- Clients unter Windows 10 Anniversary Edition (Build 14328 und höher)  

- Erstellen einer Client-Onbardingkonfigurationsdatei  

  ##### <a name="how-to-create-an-onboarding-configuration-file"></a>So erstellen Sie eine Onboardingkonfigurationsdatei  

  1.  Melden Sie sich beim Microsoft Defender ATP-Onlinedienst an.  

  2.  Klicken Sie auf das Menüelement **Client On-boarding** (Client-Onboarding)  

  3.  Wählen Sie **Configuration Manager** aus, und klicken Sie auf **Paket herunterladen**.  

  4.  Laden Sie die komprimierte Archiv-Datei (ZIP-Datei) herunter, und extrahieren Sie die Inhalte.  


##### <a name="onboard-devices-for-microsoft-defender-atp"></a>Integrieren von Geräten für Microsoft Defender ATP  

1. Wechseln Sie in der Configuration Manager-Konsole zu **Bestand und Kompatibilität** > **Übersicht** > **Endpoint Protection** > **Windows Defender ATP-Richtlinien**, und klicken Sie auf **Windows Defender ATP-Richtlinie erstellen**. Dann wird der Assistent für Microsoft Defender ATP-Richtlinien geöffnet.  

2. Geben Sie den **Namen** und die **Beschreibung** für die Microsoft Defender ATP-Richtlinie ein, und wählen Sie **Onboarding** aus. Klicken Sie auf Weiter .  

3. **Wechseln** Sie zu der Konfigurationsdatei, die vom Microsoft Defender ATP-Clouddienstmandanten Ihrer Organisation bereitgestellt wurde. Klicken Sie auf **Weiter**.  

4. Geben Sie die Dateibeispiele an, die gesammelt und gemeinsam von verwalteten Geräten für die Analyse freigegeben werden.  

   - **Keine** – Es werden keine Beispieldateien für die Analyse gesammelt  

   - **Portierbare ausführbare Dateien** – Dateien wie z.B. Programmdateien (.exe), dynamische Bibliotheklinkdateien (.dll), Schriftartdateien, und ähnliche Dateien, die in Cyberangriffen ausgenutzt werden können, werden gesammelt und zur Analyse freigegeben  

     Klicken Sie auf **Weiter**.  

5. Überprüfen Sie die Zusammenfassung, und schließen Sie den Assistenten ab.  

6. Sie können nun die Microsoft Defender ATP-Richtlinie für verwaltete Clientcomputer bereitstellen, indem Sie auf **Bereitstellen** klicken.  

##### <a name="monitor-microsoft-defender-atp"></a>Überwachen von Microsoft Defender ATP  

1.  Navigieren Sie in der Configuration Manager-Konsole zu **Überwachung** > **Übersicht** > **Sicherheit**, und klicken Sie dann auf **Windows Defender ATP**.  

2.  Überprüfen Sie das Microsoft Defender Advanced Threat Protection-Dashboard.  

    -   **Windows Defender Agent Deployment Status** (Windows Defender-Agent-Bereitstellungsstatus) – Anzahl und Prozentsatz der geeigneten verwalteten Clientcomputer mit integrierter aktiver Microsoft Defender ATP-Richtlinie  

    -   **Integrität von Windows Defender ATP-Agent** – Prozentsatz von Computerclients, die den Status für ihren Microsoft Defender-ATP-Agent melden  

        -   **Integriert** – Funktioniert ordnungsgemäß  

        -   **Inaktiv** – In dem Zeitraum wurden keine Daten an den Dienst gesendet  

        -   **Agent-Status** – Der Systemdienst für den Agent in Windows wird nicht ausgeführt  

        -   **Nicht integriert** – Die Richtlinie wurde angewendet, aber der Agent hat die Richtlinienintegration nicht gemeldet  

##  <a name="on-premises-device-health-attestation"></a><a name="BKMK_DHA"></a> Integritätsnachweis für lokale Geräte  
 Der Integritätsnachweis für Windows 10-Geräte kann jetzt so konfiguriert werden, dass die Kommunikation über die lokale Infrastruktur erfolgt. Administratoren können angeben, ob die Berichterstellung über die Cloud oder über lokale Ressourcen durchgeführt wird. Wenn für die Berichterstellung für den Integritätsnachweis „lokal“ ausgewählt wird, kann ein URL für den Dienst angegeben werden. Dadurch können Client-PCs ohne Internetzugriff Geräte, die den Integritätsnachweis verwenden, aktivieren und verwalten.  

### <a name="enable-health-attestation-for-on-premises-devices"></a>Aktivieren des Integritätsnachweises für lokale Geräte  
 In Technical Preview 1605 haben wir einige Fehler behoben, die in 1604 aufgetreten sind.  Konfigurieren Sie zu Testzwecken den lokalen Health Attestation-Dienst anhand der Client-Agent-Einstellungen.  

1.  Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Übersicht** > **Clienteinstellungen**, und legen Sie anschließend **Lokalen Integritätsnachweisdienst verwenden** auf **Ja**fest.  

2.  Geben Sie die **URL für lokalen Integritätsnachweisdienst**an, und klicken Sie anschließend auf **OK**.  

##  <a name="new-restart-options-for-windows-10-clients-after-software-update-installation"></a><a name="BKMK_RestartOptions"></a> Neue Neustartoptionen für Windows 10-Clients nach der Installation von Softwareupdates  
 Wenn ein Softwareupdate, das einen Neustart benötigt, mit Configuration Manager bereitgestellt und auf einem Computer installiert wird, wird ein ausstehender Neustart geplant, und das Dialogfeld „Neustart“ wird angezeigt. Wenn Sie in Versionen, die unter Windows 8 oder höher laufen, den Computer mithilfe der Windows Power-Optionen (anstatt über den Neustartdialog) herunterfahren oder neu starten, wird das Neustartdialogfeld auch nach dem Neustart weiterhin angezeigt. Der Computer muss trotzdem innerhalb der konfigurierten Zeitspanne neu gestartet werden. In dieser Technical Preview werden die Optionen **Update und Neustart** und **Update und Herunterfahren** auf Windows 10-Computern in den Windows Power-Optionen verfügbar sein, sobald es einen ausstehenden Neustart für ein Configuration Manager-Softwareupdate gibt. Nach der Verwendung einer dieser Optionen, wird das Dialogfeld „Neustart“ nach dem Neustart des Computers nicht angezeigt.  

##  <a name="pre-declare-corporate-owned-devices-with-imei-or-ios-serial-number"></a><a name="BKMK_IMEI"></a> Vorabdeklarieren von firmeneigenen Geräten mit IMEI- oder iOS-Seriennummer  
 Sie können nun firmeneigene Geräte identifizieren, indem Sie deren IMEI-Nummern (International Station Mobile Equipment Identity) importieren. Sie können eine CSV-Datei (comma-separated values, durch Trennzeichen getrennte Datei) hochladen, die die IMEI-Nummern der Geräte enthält, oder Geräteinformationen manuell eingeben.  Sie können auch die Seriennummern für iOS-Geräte importieren.  Importierte Informationen legen den Besitz der registrierten Geräte auf „Unternehmen“ fest.  Für jeden Benutzer, der auf den Dienst zugreift, wird dennoch eine Intune-Lizenz benötigt.  

### <a name="try-it-out"></a>Probieren Sie es aus!  
 Versuchen Sie, die folgenden Tasks auszuführen, und lassen Sie uns dann wissen, wie es funktioniert hat, indem Sie unserer Feedbackformular auf der Seite [Configuration Manager-Feedbackprogramm](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) auf der Microsoft Connect-Website ausfüllen:  

-   Importieren Sie IMEI-Nummern in eine CSV-Datei. Jede Zeile kann die IMEI-Nummer, gefolgt von einem Detailfeld, enthalten.  

-   Importieren Sie IMEI-Nummern manuell über die Configuration Manager-Konsole.  

-   Importieren Sie iOS-Seriennummern in eine CSV-Datei. Jede Zeile enthält wiederum eine Zahl, gefolgt von allen Details für das Gerät.  

##### <a name="pre-declare-corporate-owned-devices-with-imei-or-ios-serial-number"></a>Vorabdeklarieren von firmeneigenen Geräten mit IMEI- oder iOS-Seriennummer  

1. Navigieren Sie in der Configuration Manager-Konsole zu **Bestand und Kompatibilität** > **Übersicht** > **Alle unternehmenseigene Geräte** > **Vorabdeklarierte Geräte**, und klicken Sie dann auf **Create Pre-declared Devices** (Erstellen von vorabdeklarierten Geräten). Der Assistent für vorabdeklarierte Geräte wird geöffnet.  

2. Geben Sie an, wie Sie Geräteinformationen hinzufügen möchten:  

   -   **Hochladen einer CSV-Datei mit den IMEI-Nummern und Details** – Siehe Schritt 3 zum Hochladen einer Nummernliste.  

   -   **Manuelles Hinzufügen von IMEI-Nummern und Details** – Um Informationen manuell einzugeben, geben Sie die IMEI-Nummer oder iOS-Seriennummer und Details zu Geräten ein, und gehen Sie zu Schritt 4 über.  

3. Für hochgeladene Dateien navigieren Sie zu der CSV-Datei, die Informationen zu unternehmenseigenen, vorabdeklarierten Geräten enthält. Die Datei muss das folgende Format aufweisen, ausgenommen der obersten Zeile (die nur zur Erklärung zur Verfügung gestellt wird):  

   |**IMEI-Nummer**|**iOS-Seriennummer**|**Betriebssystem**|**Details**|
   |---|---|---|---|
   |123456789012345||WINDOWS|Unternehmenseigenes Windows-Gerät|
   |123456789012|A0BCD0EFGH0J|IOS|Unternehmenseigenes iOS-Gerät|
   |123456789012346||ANDROID|Unternehmenseigenes Android-Gerät|

    **Spalten:**  

   - Spalte 1: IMEI-Nummer: Eine IMEI-Nummer oder eine iOS-Seriennummer ist für jede Zeile erforderlich.  

   - Spalte 2: iOS-Seriennummer – Es können ausschließlich iOS-Seriennummern vorabdeklariert sein. Verwenden Sie die IMEI-Nummer für andere Geräteplattformen  

   - Spalte 3: Betriebssystem des Geräts (Großschreibung erforderlich):  

     -   IOS – Alle iOS-Geräte  

     -   WINDOWS – Umfasst Windows Phone, Windows 10 Mobile und Windows-PCs  

     -   ANDROID – Alle Android-Geräte  

   - Spalte 4: Details: Zusätzliche Geräteinformationen, die in der Configuration Manager-Konsole angezeigt werden  

     Klicken Sie auf **Weiter**.  

4. Überprüfen der Ergebnisse des Dateiimports. Die Details zuvor importierter IMEI- oder Seriennummern werden mit neuen Details aktualisiert.  Klicken Sie auf **Weiter**, um fortzufahren oder auf **Zurück**, um aktualisierte Details beizubehalten, und schließen Sie dann den Assistenten ab.