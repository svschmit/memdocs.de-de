---
title: Einrichten der Laborumgebung
titleSuffix: Configuration Manager
description: Richten Sie eine Laborumgebung ein, um Configuration Manager mit simulierten realen Aktivitäten zu evaluieren.
ms.date: 09/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b1970688-0cd2-404f-a17f-9e2aa4a78758
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: a23f6106a8c922b3ff4e8306fb76aec4fd26b148
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691408"
---
# <a name="set-up-a-configuration-manager-lab"></a>Einrichten eines Configuration Manager-Labs

*Gilt für: Configuration Manager (Current Branch)*

Gemäß der Anleitung in diesem Thema können Sie eine Laborumgebung einrichten, um Configuration Manager mit simulierten realen Aktivitäten zu evaluieren.  

> [!NOTE]
> Microsoft bietet eine vorkonfigurierte Version dieses Labs unter Verwendung einer Evaluierungsversion von Configuration Manager. Weitere Informationen finden Sie unter [Deployment Lab Kit für Windows und Office](https://docs.microsoft.com/microsoft-365/enterprise/modern-desktop-deployment-and-management-lab). 

##  <a name="core-components"></a><a name="BKMK_LabCore"></a> Kernkomponenten  
 Das Einrichten der Umgebung für Configuration Manager erfordert einige Kernkomponenten, um die Installation von Configuration Manager zu unterstützen.    

-   **Für die Laborumgebung wird das Betriebssystem Windows Server 2012 R2 verwendet**, unter dem Configuration Manager installiert wird.  

     Sie können eine Evaluierungsversion von Windows Server 2012 R2 aus dem [TechNet Evaluierungscenter](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012) herunterladen.  

     Ändern oder deaktivieren Sie ggf. „Verstärkte Sicherheitskonfiguration für Internet Explorer“, um einfacher auf einige der Downloads zuzugreifen, auf die in diesen Übungen Bezug genommen wird. Weitere Informationen finden Sie unter [Internet Explorer: Enhanced Security Configuration](https://technet.microsoft.com/library/dd883248\(v=ws.10\).aspx) (Konfiguration für erhöhte Sicherheit von Internet Explorer).  

-   **Die Laborumgebung verwendet SQL Server 2012 SP2** für die Standortdatenbank.  

     Sie können eine Evaluierungsversion von SQL Server 2012 aus dem [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=43340) herunterladen.  

     SQL Server verfügt über [unterstützte Versionen von SQL Server](../../core/plan-design/configs/support-for-sql-server-versions.md#bkmk_SQLVersions), denen für die Verwendung mit Configuration Manager Rechnung getragen werden muss.  

    -   Configuration Manager erfordert eine 64-Bit-Version von SQL Server, um die Standortdatenbank zu hosten.  

    -   **SQL_Latin1_General_CP1_CI_AS** als **SQL Collation** -Klasse.  

    -   **Windows-Authentifizierung**[statt SQL-Authentifizierung](https://technet.microsoft.com/library/ms144284.aspx) is required.  

    -   Eine dedizierte **SQL Server-Instanz** ist erforderlich.  

    -   Beschränken Sie nicht den **adressierbaren Systemspeicher** für SQL Server.  

    -   Konfigurieren Sie das **SQL Server-Dienstkonto** so, dass es mit einem Domänenbenutzerkonto mit geringen Rechten ausgeführt wird.  

    -   Sie müssen **SQL Server Reporting Services** installieren.  

    -   **Die Kommunikation zwischen Standorten** verwendet den SQL Server Service Broker auf TCP-Standardport 4022.  

    -   **Die Kommunikation zwischen Standorten** zwischen der SQL Server-Datenbank-Engine und ausgewählten Configuration Manager-Standortsystemrollen verwendet den TCP-Standardport 1433.  

-   **Der Domänencontroller verwendet Windows Server 2008 R2**, wobei Active Directory Domain Services installiert ist. Der Domänencontroller fungiert auch als Host für den DHCP- und den DNS-Server zur Verwendung mit einem vollqualifzierten Domänennamen.  

     Weitere Informationen finden Sie in dieser [Übersicht von Active Directory Domain Services](https://technet.microsoft.com/library/hh831484).  

-   **Hyper-V wird mit einigen virtuellen Computern verwendet**, um zu überprüfen, ob die in diesen Übungen ergriffenen Verwaltungsschritte wie erwartet funktionieren. Mindestens drei virtuelle Computer unter Windows 10 werden empfohlen.  

     Weitere Informationen finden Sie in dieser [Übersicht über Hyper-V](https://technet.microsoft.com/library/hh831531.aspx).  

-   **Administratorberechtigungen** sind für all diese Komponenten erforderlich.  

    -   Configuration Manager erfordert einen Administrator mit lokalen Berechtigungen innerhalb der Windows Server-Umgebung  

    -   Active Directory erfordert einen Administrator mit Berechtigungen zum Ändern des Schemas.  

    -   Virtuelle Computer erfordern lokale Berechtigungen auf den Computern selbst.  

Unter [Unterstützte Konfigurationen für Configuration Manager](../../core/plan-design/configs/supported-configurations.md) finden Sie weitere Informationen zu den Anforderungen für die Implementierung von Configuration Manager, die allerdings für diese Laborumgebung nicht erforderlich sind. Lesen Sie die Dokumentation für andere als die hier erwähnten Softwareversionen.  

Nachdem Sie alle Komponenten installiert haben, müssen Sie weitere Schritte durchführen, um Ihre Windows-Umgebung für Configuration Manager zu konfigurieren:  

##  <a name="prepare-active-directory-content-for-the-lab"></a><a name="BKMK_LabADPrep"></a> Vorbereiten von Active Directory-Inhalten für die Laborumgebung  
 Für diese Laborumgebung erstellen Sie eine Sicherheitsgruppe, der Sie anschließend einen Domänenbenutzer hinzufügen.  

-   Sicherheitsgruppe: **Evaluierung**  

    -   Gruppenbereich: **Universal**  

    -   Gruppentyp: **Sicherheit**  

-   Domänenbenutzer: **ConfigUser**  

     Unter normalen Umständen würden Sie nicht allen Benutzern in Ihrer Umgebung universellen Zugriff gewähren. Bei diesem Benutzer machen Sie eine Ausnahme, um Ihre Laborumgebung schneller online zu schalten.  

Die nächsten Schritte, die erforderlich sind, um Configuration Manager-Clients die Abfrage von Standortressourcen von Active Directory Domain Services zu ermöglichen, werden in den nachfolgenden Verfahren behandelt.  

##  <a name="create-the-system-management-container"></a><a name="BKMK_CreateSysMgmtLab"></a> Erstellen des System Management-Containers  
 Der in Active Directory Domain Services erforderliche System Management-Container wird von Configuration Manager nicht automatisch erstellt, wenn das Schema erweitert wird. Daher müssen Sie ihn für diese Laborumgebung erstellen. Dieser Schritt erfordert die [Installation von ADSI Edit](https://technet.microsoft.com/library/cc773354\(WS.10\).aspx#BKMK_InstallingADSIEdit).  

 Stellen Sie sicher, dass Sie mit einem Konto angemeldet sind, das im Container **System** in den Active Directory-Domänendiensten über die Rechte **Alle untergeordneten Objekte erstellen** verfügt.  

#### <a name="to-create-the-system-management-container"></a>So erstellen Sie den System Management-Container  

1.  Führen Sie **ADSI Edit**aus, und stellen Sie eine Verbindung mit der Domäne her, in der sich der Standortserver befindet.  

2.  Erweitern Sie **Domäne&lt;Vollqualifizierter Domänenname\>** und dann **<Definierter Name\>** , klicken Sie mit der rechten Maustaste auf **CN=System**, und klicken Sie auf **Neu** und dann auf **Objekt**.  

3.  Wählen Sie im Dialogfeld **Objekt erstellen** die Option **Container**aus, und klicken Sie auf **Weiter**.  

4.  Geben Sie in das Feld **Wert** die Zeichenfolge **System Management**ein, und klicken Sie dann auf **Weiter**.  

5.  Klicken Sie auf **Fertig stellen** , um den Vorgang abzuschließen.  

##  <a name="set-security-permissions-for-the-system-management-container"></a><a name="BKMK_SetSecPermLab"></a> Festlegen der Sicherheitsberechtigungen für den System Management-Container  
 Gewähren Sie dem Computerkonto des Standortservers die Berechtigungen, die zum Veröffentlichen von Standortinformationen im Container erforderlich sind. Für diese Aufgabe verwenden Sie ebenfalls ADSI Edit.  

> [!IMPORTANT]  
>  Vergewissern Sie sich, dass Sie mit der Domäne des Standortservers verbunden sind, bevor Sie mit dem folgenden Verfahren beginnen.  

#### <a name="to-set-security-permissions-for-the-system-management-container"></a>So legen Sie Sicherheitsberechtigungen für den System Management-Container fest  

1.  Erweitern Sie im Konsolenfenster die **Domäne des Standortservers**, erweitern Sie **DC=&lt;definierter Name des Servers\>** und anschließend **CN=System**. Klicken Sie mit der rechten Maustaste auf **CN=System Management**, und klicken Sie dann auf **Eigenschaften**.  

2.  Klicken Sie im Dialogfeld **Eigenschaften von CN=System Management** auf die Registerkarte **Sicherheit** und dann auf **Hinzufügen** , um das Computerkonto des Standortservers hinzuzufügen. Erteilen Sie dem Konto die Berechtigung **Vollzugriff** .  

3.  Klicken Sie auf **Erweitert**, wählen Sie das Computerkonto des Standortservers aus, und klicken Sie dann auf **Bearbeiten**.  

4.  Wählen Sie in der Liste **Übernehmen für** den Eintrag **Dieses und alle untergeordneten Objekte**aus.  

5.  Klicken Sie auf **OK** , um die **ADSI Edit** -Konsole zu schließen und den Vorgang abzuschließen.  

     Zusätzliche Einblicke in dieses Verfahren erhalten Sie unter [Erweitern des Active Directory-Schemas für Configuration Manager](../../core/plan-design/network/extend-the-active-directory-schema.md).  

##  <a name="extend-the-active-directory-schema-using-extadschexe"></a><a name="BKMK_ExtADSchLab"></a> Erweitern des Active Directory-Schemas mithilfe von "extadsch.exe"  
 Für diese Laborumgebung erweitern Sie das Active Directory-Schema, da Sie dadurch alle Configuration Manager-Features und -Funktionen mit geringstem Verwaltungsaufwand verwenden können. Die Erweiterung des Active Directory-Schemas ist eine gesamtstrukturübergreifende Konfiguration, die pro Gesamtstruktur nur einmal ausgeführt werden kann. Durch die Erweiterung des Schemas wird die Gruppe von Klassen und Attributen in der Active Directory-Basiskonfiguration dauerhaft geändert. Diese Aktion kann nicht rückgängig gemacht werden. Durch die Erweiterung des Schemas erhält Configuration Manager Zugriff auf Komponenten, die seine möglichst effiziente Ausführung in der Laborumgebung ermöglichen.  

> [!IMPORTANT]  
>  Stellen Sie sicher, dass Sie auf dem Schemamaster-Domänencontroller über ein Konto angemeldet sind, das Mitglied der Sicherheitsgruppe **Schema-Admins** ist. Die Verwendung alternativer Anmeldeinformationen ist nicht erfolgreich.  

#### <a name="to-extend-the-active-directory-schema-using-extadschexe"></a>So erweitern Sie das Active Directory-Schema mithilfe von "extadsch.exe"  

1.  Erstellen Sie eine Sicherung des Systemzustands für den Schemamaster-Domänencontroller. Weitere Informationen zum Sichern der Masterdomänencontroller finden Sie unter [Windows Server-Sicherung](https://technet.microsoft.com/library/cc770757.aspx).  

2.  Navigieren Sie zu **\SMSSETUP\BIN\X64** auf den Installationsmedien.  

3.  Führen Sie **extadsch.exe**aus.  

4.  Überprüfen Sie in **extadsch.log** im Stammordner des Systemlaufwerks, ob die Schemaerweiterung erfolgreich durchgeführt wurde.  

     Zusätzliche Einblicke in dieses Verfahren erhalten Sie unter [Erweitern des Active Directory-Schemas für Configuration Manager](../../core/plan-design/network/extend-the-active-directory-schema.md).  

##  <a name="other-required-tasks"></a><a name="BKMK_OtherTasksLab"></a> Weitere erforderliche Aufgaben  
 Vor der Installation müssen Sie folgende Aufgaben abschließen.  

 **Erstellen Sie einen Ordner zum Speichern aller Downloads.**  

 Während dieser Übung sind mehrere Downloads für die Komponenten auf den Installationsmedien erforderlich. Bevor Sie mit den Installationsschritten beginnen, legen Sie einen Speicherort fest, von dem die Dateien für die Dauer der Laborumgebung nicht verschoben werden müssen. Es wird empfohlen, diese Downloads in einem einzelnen Ordner mit separaten Unterordnern zu speichern.  

 **Installieren von .NET und Aktivieren von Windows Communication Foundation (WCF)**  

 Sie müssen zwei .NET Framework-Versionen installieren: zuerst .NET 3.5.1 und anschließend .NET 4.5.2+. Außerdem müssen Sie Windows Communication Foundation (WCF) aktivieren. WCF bietet einfachen Zugang zu verteilter Datenverarbeitung, umfassender Interoperabilität und direkte Unterstützung für die dienstorientierte Entwicklung. Zudem vereinfacht sie die Entwicklung vernetzter Anwendungen über ein dienstorientiertes Programmiermodell. Weitere Einblicke in WCF erhalten Sie unter [Was ist die Windows Communication Foundation?](https://technet.microsoft.com/subscriptions/ms731082\(v=vs.90\).aspx)  

#### <a name="to-install-net-and-activate-windows-communication-foundation"></a>So installieren Sie .NET und aktivieren Windows Communication Foundation (WCF)  

1.  Öffnen Sie **Server Manager**, und navigieren Sie zu **Verwalten**. Klicken Sie auf **Rollen und Features hinzufügen** , um den **Rollen und Features hinzufügen Wizard.** zu öffnen.  

2.  Lesen Sie die Informationen im Bereich **Bevor Sie beginnen** , und klicken Sie dann **Weiter**.  

3.  Wählen Sie **Rollenbasierte oder featurebasierte Installation**aus, und klicken Sie dann auf **Weiter**.  

4.  Wählen Sie Ihren Server aus dem **Serverpool**aus, und klicken Sie dann auf **Weiter**.  

5.  Überprüfen Sie den Bereich **Serverrollen** , und klicken Sie dann **Weiter**.  

6.  Fügen Sie die folgenden **Features** hinzu, indem Sie sie aus der Liste auswählen:  

    -   **.NET Framework 3.5-Features**  

        -   **.NET Framework 3.5 (umfasst .NET 2.0 und 3.0)**  

    -   **.NET Framework 4.5-Features**  

        -   **.NET Framework 4.5**  

        -   **ASP.NET 4.5**  

        -   **WCF-Dienste**  

            -   **HTTP-Aktivierung**  

            -   **TCP-Portfreigabe**  

7.  Überprüfen Sie den Bildschirm **Webserverrolle (IIS)** und **Rollendienste** , und klicken Sie dann **Weiter**.  

8.  Überprüfen Sie den Bildschirm **Bestätigung** , und klicken Sie dann **Weiter**.  

9. Klicken Sie auf **Installieren** , und stellen Sie anhand des Bereichs **Benachrichtigungen** im **Server-Manager**sicher, dass die Installation ordnungsgemäß abgeschlossen wurde.  

10. Nach Abschluss der .NET-Standardinstallation navigieren Sie zum [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=42643) , um den Webinstaller für .NET Framework 4.5.2 abzurufen. Klicken Sie auf die Schaltfläche **Herunterladen** , und starten Sie das Installationsprogramm mit **Ausführen** . Die erforderlichen Komponenten werden automatisch erkannt und in der ausgewählten Sprache installiert.  

Die folgenden Artikel enthalten weitere Informationen darüber, warum diese .NET Framework-Versionen erforderlich sind:  

-   [.NET Framework – Versionen und Abhängigkeiten](https://technet.microsoft.com/library/bb822049.aspx)  

-   [Exemplarische Vorgehensweise zur .NET Framework 4 RTM-Anwendungskompatibilität](https://technet.microsoft.com/library/dd889541.aspx)  

-   [How to: Upgrade an ASP.NET Web Application to ASP.NET 4 (Vorgehensweise: Aktualisieren einer ASP.NET-Webanwendung auf ASP.NET 4)](https://technet.microsoft.com/library/dd483478\(VS.100\).aspx)  

-   [Microsoft .NET Framework Support Lifecycle-Richtlinien – häufig gestellte Fragen](https://support.microsoft.com/en-us/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update)  

-   [CLR Inside Out – In-Process Side-by-Side](https://msdn.microsoft.com/magazine/ee819091.aspx)  

**Aktivieren von BITS, IIS und RDC**  

Der [Background Intelligent Transfer Service (BITS)](https://technet.microsoft.com/library/dn282296.aspx) wird für Anwendungen verwendet, die Dateien asynchron zwischen einem Client und einem Server übertragen müssen. Durch Messung des Übertragungsflusses im Vorder- und Hintergrund gewährleistet BITS die Reaktionsfähigkeit anderer Netzwerkanwendungen. Dateiübertragungen werden zudem automatisch fortgesetzt, wenn eine Übertragungssitzung unterbrochen wurde.  

Sie installieren BITS für diese Laborumgebung, weil dieser Standortserver zusätzlich als Verwaltungspunkt verwendet wird.  

Internetinformationsdienste (Internet Information Services, IIS) ist ein flexibler, skalierbarer Webserver, der zum Hosten verschiedener Komponenten im Web verwendet werden kann. Der Dienst wird von Configuration Manager für eine Reihe von Standortsystemrollen eingesetzt. Weitere Informationen zu IIS finden Sie unter [Websites für Standortsystemserver](../../core/plan-design/network/websites-for-site-system-servers.md).  

[Remotedifferenzialkomprimierung (Remote Differential Compression, (RDC)](https://technet.microsoft.com/library/cc754372.aspx) ist eine Sammlung von APIs, über die Clientanwendungen feststellen können, ob ein Satz von Dateien geändert wurde. RDC ermöglicht der Anwendung, nur die geänderten Dateibereiche zu replizieren, und beschränkt den Netzwerkdatenverkehr dadurch auf ein Minimum.  

#### <a name="to-enable-bits-iis-and-rdc-site-server-roles"></a>So aktivieren Sie BITS-, IIS- und RDC-Standortserverrollen  

1.  Öffnen Sie auf dem Standortserver **Server Manager**. Navigieren Sie zu **Verwalten**. Klicken Sie auf **Rollen und Features hinzufügen** , um den **Assistenten zum Hinzufügen von Rollen und Features**zu öffnen.  

2.  Lesen Sie die Informationen im Bereich **Bevor Sie beginnen** , und klicken Sie dann **Weiter**.  

3.  Wählen Sie **Rollenbasierte oder featurebasierte Installation**aus, und klicken Sie dann auf **Weiter**.  

4.  Wählen Sie Ihren Server aus dem **Serverpool**aus, und klicken Sie dann auf **Weiter**.  

5.  Fügen Sie die folgenden **Serverrollen** hinzu, indem Sie sie aus der Liste auswählen:  

    -   **Webserver (IIS)**  

        -   **Allgemeine HTTP-Features**  

            -   **Standarddokument**  

            -   **Verzeichnissuche**  

            -   **HTTP-Fehler**  

            -   **Statischer Inhalt**  

            -   **HTTP-Umleitung**  

        -   **Integrität und Diagnose**  

            -   **HTTP-Protokollierung**  

            -   **Protokollierungstools**  

            -   **Anforderungsüberwachung**  

            -   **Ablaufverfolgung**  

    -   **Leistung**  

        -   **Komprimierung statischer Inhalte**  

        -   **Komprimierung dynamischer Inhalte**  

    -   **Security**  

        -   **Anforderungsfilterung**  

        -   **Standardauthentifizierung**  

        -   **Authentifizierung durch Clientzertifikatszuordnung**  

        -   **IP- und Domäneneinschränkungen**  

        -   **URL-Autorisierung**  

        -   **Windows-Authentifizierung**  

    -   **Anwendungsentwicklung**  

        -   **.NET-Erweiterbarkeit 3.5**  

        -   **.NET-Erweiterbarkeit 4.5**  

        -   **ASP**  

        -   **ASP.NET 3.5**  

        -   **ASP.NET 4.5**  

        -   **ISAPI-Erweiterungen**  

        -   **ISAPI-Filter**  

        -   **Serverseitige Include-Dateien**  

    -   **FTP-Server**  

        -   **FTP-Dienst**  

    -   **Verwaltungstools**  

        -   **IIS-Verwaltungskonsole**  

        -   **IIS 6-Verwaltungskompatibilität**  

            -   **IIS 6-Metabasiskompatibilität**  

            -   **IIS 6-Verwaltungskonsole**  

            -   **IIS 6-Skripttools**  

            -   **IIS 6-WMI-Kompatibilität**  

        -   **IIS 6-Verwaltungsskripts und -Tools**  

        -   **Management Service**  

6.  Fügen Sie die folgenden **Features** hinzu, indem Sie sie aus der Liste auswählen:  

    -   **Background Intelligent Transfer Service (BITS)**  

          -   **IIS-Servererweiterung**  

    -   **Remoteserver-Verwaltungstools**  

          -   **Featureverwaltungstools**  

          -   **Tools für BITS-Servererweiterungen**  

7.  Klicken Sie auf **Installieren** , und stellen Sie anhand des Bereichs **Benachrichtigungen** im **Server-Manager**sicher, dass die Installation ordnungsgemäß abgeschlossen wurde.  

IIS sperrt standardmäßig mehrere Dateierweiterungen und Speicherorte für den Zugriff durch die HTTP- oder HTTPS-Kommunikation. Um die Verteilung dieser Dateien an Clientsysteme zu ermöglichen, müssen Sie die Anforderungsfilterung für IIS auf dem Verteilungspunkt konfigurieren. Weitere Informationen finden Sie unter [IIS-Anforderungsfilterung für Verteilungspunkte](../../core/plan-design/network/prepare-windows-servers.md#BKMK_IISFiltering).  

#### <a name="to-configure-iis-filtering-on-distribution-points"></a>So konfigurieren Sie die IIS-Filterung für Verteilungspunkte  

1.  Öffnen Sie **IIS Manager** , und wählen Sie den Namen des Servers in der Randleiste aus. Dadurch gelangen Sie zur **Startseite** .  

2.  Überprüfen Sie, ob die **Ansicht "Features"** am unteren Rand der **Startseite** ausgewählt ist. Navigieren Sie zu **IIS** , und öffnen Sie **Anforderungsfilterung**.  

3.  Klicken Sie im Bereich **Aktionen** auf **Dateinamenerweiterung zulassen**.  

4.  Geben Sie **.msi** in das Dialogfeld ein, und klicken Sie auf **OK**.  

##  <a name="installing-configuration-manager"></a><a name="BKMK_InstallCMLab"></a> Installieren von Configuration Manager  
Sie erstellen [Ermitteln des Zeitpunkts für die Verwendung eines primären Standorts](../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md#BKMK_ChoosePriimary), um Clients direkt zu verwalten. Dadurch unterstützt Ihre Laborumgebung die Verwaltung für die [Standortsystemskalierung](../plan-design/configs/size-and-scale-numbers.md) potenzieller Geräte.  
Während dieses Vorgangs installieren Sie außerdem die Configuration Manager-Konsole, die ab diesem Zeitpunkt zur Verwaltung von Evaluierungsgeräten verwendet wird.  

Bevor Sie mit der Installation beginnen, starten Sie die [Voraussetzungsprüfung](../servers/deploy/install/prerequisite-checker.md) auf dem unter Windows Server 2012 ausgeführten Server, um zu bestätigen, dass alle Einstellungen ordnungsgemäß aktiviert wurden.  

#### <a name="to-download-and-install-configuration-manager"></a>So laden Sie Configuration Manager herunter und installieren die Anwendung  

1.  Navigieren Sie zur Seite für [System Center-Evaluierungsversionen](https://www.microsoft.com/evalcenter/evaluate-system-center-2012-configuration-manager-and-endpoint-protection), um die neueste Evaluierungsversion von Configuration Manager herunterzuladen.  

2.  Dekomprimieren Sie die Downloadmedien an dem von Ihnen festgelegten Speicherort.  

3.  Führen Sie die unter [Installieren eines Standorts mithilfe des Setup-Assistenten von Configuration Manager](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md) beschriebenen Installationsschritte aus. Während dieser Prozedur sind folgende Eingaben erforderlich:  

    |Schritt in der Prozedur der Standortinstallation|Auswahl|  
    |-----------------------------------------|---------------|  
    |Schritt 4: die Seite **Product Key**|Wählen Sie **Evaluierung**aus.|  
    |Schritt 7:  **Download der Voraussetzungskomponenten**|Wählen Sie **Erforderliche Dateien herunterladen** aus, und geben Sie den zuvor festgelegten Speicherort an.|  
    |Schritt 10: **Standort- und Installationseinstellungen**|-   **Standortcode:LAB**<br />-   **Standortname:Evaluation**<br />-   **Installationsordner:** Geben Sie den zuvor festgelegten Speicherort an.|  
    |Schritt 11: **Installation am primären Standort**|Wählen Sie **Den primären Standort als eigenständigen Standort installieren**aus, klicken Sie dann auf **Weiter**.|  
    |Schritt 12: **Datenbankinstallation**|-   **SQL Server-Name (FQDN):** Geben Sie hier Ihren FQDN ein.<br />-   **Instanzname:** Dieses Feld bleibt leer, da Sie die zuvor installierte Standardinstanz von SQL verwenden.<br />-   **Port des Service Brokers:** Behalten Sie den Standardport 4022 bei.|  
    |Schritt 13: **Datenbankinstallation**|Behalten Sie die Standardeinstellungen bei.|  
    |Schritt 14: **SMS-Anbieter**|Behalten Sie die Standardeinstellungen bei.|  
    |Schritt 15: **Clientkommunikationseinstellungen**|Überprüfen Sie, ob **Alle Standortsystemrollen lassen ausschließlich die HTTPS-Kommunikation mit Clients zu** deaktiviert ist.|  
    |Schritt 16: **Standortsystemrollen**|Geben Sie Ihren FQDN ein, und stellen Sie sicher, dass **Alle Standortsystemrollen lassen ausschließlich die HTTPS-Kommunikation mit Clients zu** weiterhin deaktiviert ist.|  

##  <a name="enable-publishing-for-the-configuration-manager-site"></a><a name="BKMK_EnablePubLab"></a> Aktivieren der Veröffentlichung am Configuration Manager-Standort  
Jeder Configuration Manager-Standort veröffentlicht standortspezifische Informationen im Systemverwaltungscontainer innerhalb seiner Domänenpartition im Active Directory-Schema. Bidirektionale Kanäle für die Kommunikation zwischen Active Directory und Configuration Manager müssen geöffnet sein, um den Datenverkehr zu verarbeiten. Aktivieren Sie zudem die Gesamtstrukturermittlung, um bestimmte Komponenten Ihrer Active Directory- und Netzwerkinfrastruktur zu ermitteln.  

#### <a name="to-configure-active-directory-forests-for-publishing"></a>So konfigurieren Sie Active Directory-Gesamtstrukturen für die Veröffentlichung  

1.  Klicken Sie in der unteren linken Ecke der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Hierarchiekonfiguration**, und klicken Sie dann auf **Ermittlungsmethoden**.  

3.  Wählen Sie **Active Directory-Gesamtstrukturermittlung** aus, und klicken Sie auf **Eigenschaften**.  

4.  Wählen Sie im Dialogfeld **Eigenschaften** die Option **Gesamtstrukturermittlung von Active Directory aktivieren**aus. Nachdem die Ermittlung aktiviert wurde, wählen Sie **Active Directory-Standortgrenzen bei der Ermittlung automatisch erstellen**aus. Ein Dialogfeld mit der Frage **Möchten Sie die vollständige Ermittlung so bald wie möglich ausführen?** Klicken Sie auf **Ja**.  

5.  Klicken Sie in der Gruppe **Ermittlungsmethode** am oberen Bildschirmrand auf **Gesamtstrukturermittlung jetzt ausführen**, und navigieren Sie auf der Randleiste zu **Active Directory-Gesamtstrukturen** . Die Active Directory-Gesamtstruktur sollte in der Liste der ermittelten Gesamtstrukturen angezeigt werden.  

6.  Navigieren Sie zur Registerkarte **Allgemein** am oberen Bildschirmrand.  

7.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Hierarchiekonfiguration**, und klicken Sie dann auf **Active Directory-Gesamtstrukturen**.  

#### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-your-active-directory-forest"></a>So aktivieren Sie einen Configuration Manager-Standort für das Veröffentlichen von Standortinformationen in Active Directory-Gesamtstrukturen:  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Konfigurieren Sie eine neue Gesamtstruktur, die noch nicht ermittelt wurde.  

3.  Klicken Sie im Arbeitsbereich **Verwaltung** auf **Active Directory-Gesamtstrukturen**.  

4.  Wählen Sie auf der Registerkarte **Veröffentlichung** der Standorteigenschaften die verbundene Gesamtstruktur aus, und klicken Sie auf **OK** , um die Konfiguration zu speichern.
