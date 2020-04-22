---
title: Bereitstellen von Mac-Clients
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Clients auf Mac-Computern in Configuration Manager bereitstellen.
ms.date: 12/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8993f4c05b7156f3aecf6fcc9c8ea3790e49e98d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694028"
---
# <a name="how-to-deploy-clients-to-macs"></a>Bereitstellen von Clients auf Macintosh-Computern

*Gilt für: Configuration Manager (Current Branch)*

In diesem Artikel wird beschrieben, wie Sie den Konfigurations-Manager-Client auf Mac-Computern bereitstellen und warten. Sie finden Informationen dazu, welche Einstellungen Sie vor der Bereitstellung von Clients auf Macintosh-Computern konfigurieren müssen, unter [Vorbereiten der Bereitstellung von Clientsoftware auf Macs](prepare-to-deploy-mac-clients.md).

Wenn Sie einen neuen Client für Macintosh-Computer installieren, müssen Sie möglicherweise auch Configuration Manager-Updates installieren, um die neuen Clientinformationen in der Configuration Manager-Konsole darzustellen.

In diesen Verfahren haben Sie zwei Optionen zum Installieren von Clientzertifikaten. Weitere Informationen zu Clientzertifikaten für Macs finden Sie unter [Vorbereiten der Bereitstellung von Clientsoftware auf Macs](prepare-to-deploy-mac-clients.md#certificate-requirements).  

- Verwenden der Configuration Manager-Registrierung mithilfe des Tools [CMEnroll](#bkmk_enroll). Der Registrierungsprozess unterstützt die automatische Zertifikaterneuerung nicht. Registrieren Sie den Mac-Computer erneut, bevor das installierte Zertifikat abläuft.    

- [Verwenden einer von Configuration Manager unabhängigen Zertifikatanforderungs- und -installationsmethode](#bkmk_external).  

> [!IMPORTANT]  
> Zum Bereitstellen des Clients auf Geräten mit macOS Sierra müssen Sie den **Antragstellernamen** des Verwaltungspunktzertifikats ordnungsgemäß konfigurieren. Verwenden Sie beispielsweise den FQDN des Verwaltungspunktservers.



## <a name="configure-client-settings"></a>Konfigurieren von Clienteinstellungen  

Verwenden Sie die [Clientstandardeinstellungen](about-client-settings.md), um die Registrierung für Mac-Computer zu konfigurieren. Benutzerdefinierte Clienteinstellungen können Sie nicht verwenden. Zum Anfordern und Installieren des Zertifikats erfordert der Konfigurations-Manager-Client für Mac die Clientstandardeinstellungen.  

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**. Wählen Sie den Knoten **Clienteinstellungen** und anschließend die Option **Clientstandardeinstellungen** aus.  

2. Wählen Sie auf dem Menüband auf der Registerkarte **Start** in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus.  

3. Wählen Sie den Abschnitt **Registrierung** aus, und konfigurieren Sie dann die folgenden Einstellungen:  

    1. **Benutzern die Registrierung von mobilen Geräten und Mac-Computern gestatten:** **Ja**  

    2. **Registrierungsprofil:** Wählen Sie **Profil festlegen** aus.  

4. Wählen Sie im Dialogfeld **Anmeldungsprofil für mobile Geräte** **Erstellen**.  

5. Geben Sie im Dialogfeld **Registrierungsprofil erstellen** einen Namen für dieses Registrierungsprofil ein. Konfigurieren Sie dann den **Verwaltungsstandortcode**. Wählen Sie den primären Configuration Manager-Standort aus, der die Verwaltungspunkte für diese Mac-Computer enthält.  

    > [!NOTE]  
    >  Wenn Sie den Standort nicht auswählen können, stellen Sie sicher, dass Sie mindestens einen Verwaltungspunkt an dem Standort für die Unterstützung mobiler Geräte konfigurieren.  

6. Wählen Sie **Hinzufügen** aus.  

7. Wählen Sie im Fenster **Zertifizierungsstelle für mobile Geräte hinzufügen** den Server der Zertifizierungsstelle aus, von der Zertifikate für Mac-Computer ausgestellt werden.  

8. Wählen Sie im Dialogfeld **Registrierungsprofil erstellen** die Zertifikatvorlage für Mac-Computer aus, die Sie zuvor erstellt haben.  

9. Wählen Sie **OK** aus, um das Dialogfeld **Registrierungsprofil**, und anschließend das Dialogfeld **Clientstandardeinstellungen** zu schließen.  

    > [!TIP]  
    > Wenn Sie das Clientrichtlinienintervall ändern möchten, verwenden Sie in der Clienteinstellungsgruppe **Clientrichtlinie** die Clienteinstellung **Clientrichtlinien-Abrufintervall**.  

Beim nächsten Herunterladen der Clientrichtlinie auf die Geräte wendet der Configuration Manager diese Einstellungen für alle Benutzer an. Informationen zum Initiieren des Richtlinienabrufs für einen einzelnen Client finden Sie unter [Initiieren des Richtlinienabrufs für einen Configuration Manager-Client](../manage/manage-clients.md#BKMK_PolicyRetrieval).  

Zusätzlich zu den Clienteinstellungen für die Registrierung müssen Sie unbedingt auch die folgenden Clientgeräteeinstellungen konfigurieren:  

- **Hardwareinventur:** Aktivieren und konfigurieren Sie dieses Feature, wenn Sie Hardwareinventurdaten von Mac- und Windows-Clientcomputern sammeln möchten. Weitere Informationen finden Sie unter [Vorgehensweise: Erweitern der Hardwareinventur](../manage/inventory/extend-hardware-inventory.md).  

- **Konformitätseinstellungen:** Aktivieren und konfigurieren Sie dieses Feature, wenn Sie Einstellungen von Mac- und Windows-Clientcomputern auswerten und wiederherstellen möchten. Weitere Informationen finden Sie unter [Planen und Konfigurieren von Konformitätseinstellungen](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md).  

Weitere Informationen finden Sie unter [Konfigurieren von Clienteinstellungen](configure-client-settings.md).  



## <a name="download-the-client-for-macos"></a><a name="bkmk_download"></a> Herunterladen des Clients für macOS

1. Laden Sie das macOS-Clientdateipaket herunter, [Microsoft Endpoint Configuration Manager – macOS-Client (64-Bit)](https://www.microsoft.com/download/details.aspx?id=100850). Speichern Sie **ConfigmgrMacClient.msi** auf einem Windows-Computer. Diese Datei befindet sich nicht auf den Configuration Manager-Installationsmedien.  

2. Führen Sie das Installationsprogramm auf dem Windows-Computer aus. Extrahieren Sie das Mac-Clientpaket **Macclient.dmg** in einen Ordner auf dem lokalen Datenträger. Der Standardpfad lautet `C:\Program Files\Microsoft\System Center Configuration Manager for Mac client`.  

3. Kopieren Sie die Datei **Macclient.dmg** in einen Ordner auf dem Mac-Computer.  

4. Führen Sie auf dem Mac-Computer **Macclient.dmg** aus, um die Dateien in einem Ordner auf der lokalen Festplatte zu extrahieren.  

5. Stellen Sie sicher, dass der Ordner die folgenden Dateien enthält: 

    - **Ccmsetup**: Installiert den Konfigurations-Manager-Client auf Ihren Mac-Computern mit **CMClient.pkg**.  

    - **CMDiagnostics**: Sammelt Diagnoseinformationen zu dem auf Mac-Computern installierten Konfigurations-Manager-Client.  

    - **CMUninstall**: Deinstalliert den Client von Ihren Mac-Computern.  

    - **CMAppUtil**: Konvertiert Apple-Anwendungspakete in ein Format, das Sie als Configuration Manager-Anwendung bereitstellen können.  

    - **CMEnroll**: Fordert das Clientzertifikat für einen Mac-Computer an und installiert es, damit Sie den Konfigurations-Manager-Client installieren können.  



## <a name="enroll-the-mac-client"></a><a name="bkmk_enroll"></a> Registrieren des Mac-Clients  

Registrieren Sie einzelne Clients mithilfe des [Assistenten für die Mac-Computerregistrierung](#enroll-the-client-with-the-mac-computer-enrollment-wizard).

Um die Registrierung für viele Clients zu automatisieren, verwenden Sie das [CMEnroll-Tool](#client-and-certificate-automation-with-cmenroll).   


### <a name="enroll-the-client-with-the-mac-computer-enrollment-wizard"></a>Registrieren des Clients mithilfe des Assistenten für die Mac-Computerregistrierung  

1. Nach der Installation des Clients wird der Assistent für die Computerregistrierung geöffnet. Zum manuellen Starten des Assistenten wählen Sie auf der Einstellungsseite von **Configuration Manager** die Option **Registrieren** aus.  

2. Geben Sie auf der zweiten Seite des Assistenten die folgenden Informationen ein:  

   - **Benutzername:** Der Benutzername kann die folgenden Formate aufweisen:  

     - `domain\name`. Beispiel: `contoso\mnorth`  

     - `user@domain`. Beispiel: `mnorth@contoso.com`  

         > [!IMPORTANT]  
         >  Wenn Sie in das Feld **Benutzername** eine E-Mail-Adresse eingeben, wird das Feld **Servername** von Configuration Manager automatisch ausgefüllt. Hierfür wird der Standardname des Anmeldungsproxypunkt-Servers und der Domänenname der E-Mail-Adresse verwendet. Wenn diese Namen nicht mit dem Namen des Anmeldungsproxypunkt-Servers übereinstimmen, berichtigen Sie den **Servernamen** während der Registrierung.  

       Der Benutzername und das zugehörige Kennwort müssen mit den entsprechenden Angaben eines Active Directory-Benutzerkontos übereinstimmen, für das in der Mac-Clientzertifikatvorlage die Berechtigungen **Lesen** und **Registrieren** zugewiesen wurden.  

   - **Servername:** Geben Sie den Namen des Anmeldungsproxypunkt-Servers ein.  


### <a name="client-and-certificate-automation-with-cmenroll"></a>Automatisierung von Client und Zertifikat mit CMEnroll  

Verwenden Sie dieses Verfahren für die Automatisierung der Installation des Clients und zum Anfordern und Registrieren der Clientzertifikate mit dem Tool „CMEnroll“. Sie müssen über ein Active Directory-Benutzerkonto verfügen, um das Tool ausführen zu können.

1. Navigieren Sie auf dem Mac-Computer zu dem Ordner, in dem Sie den Inhalt der Datei **Macclient.dmg** extrahiert haben.  

2. Geben Sie den folgenden Befehl ein: `sudo ./ccmsetup`  

3. Warten Sie, bis die Meldung **Installation abgeschlossen** angezeigt wird. Vom Installationsprogramm wird eine Meldung angezeigt, dass Sie den Computer jetzt neu starten müssen. Führen Sie den Neustart nicht aus, sondern fahren Sie mit dem nächsten Schritt fort.  

4. Geben Sie auf dem Mac-Computer im Ordner **Tools** den folgenden Befehl ein: `sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u '<user_name>'`  

    Nach der Clientinstallation wird der Assistent für die Macintosh-Computeranmeldung geöffnet, um Ihnen beim Anmelden des Macintosh-Computers zu helfen. Weitere Informationen finden Sie im Artikel zum [Registrieren des Clients mit dem Assistenten für die Mac-Computerregistrierung](#bkmk_enroll).  

     Beispiel: Wenn der Anmeldungsproxypunkt-Server als **server02.contoso.com** bezeichnet ist und Sie **contoso\mnorth** Berechtigungen für die Mac-Clientzertifikatvorlage erteilen, geben Sie den folgenden Befehl ein: `sudo ./CMEnroll -s server02.contoso.com -ignorecertchainvalidation -u 'contoso\mnorth'`  

    > [!NOTE]  
    > Wenn der Benutzername eines der folgenden Zeichen enthält, kann die Registrierung nicht abgeschlossen werden: `<>"+=,`. Verwenden Sie ein Out-of-Band-Zertifikat mit einem Benutzernamen, der diese Zeichen nicht enthält.  
    >  
    > Erstellen Sie zur Verbesserung der Benutzererfahrung ein Skript mit den Installationsschritten. Dann müssen Benutzer nur noch ihren Benutzernamen und das Kennwort eingeben.  

5. Geben Sie das Kennwort für das Active Directory-Benutzerkonto ein. Wenn Sie diesen Befehl eingeben, werden Sie zur Eingabe von zwei Kennwörtern aufgefordert. Das erste Kennwort ist für das Administratorkonto, um den Befehl auszuführen. Die zweite Eingabeaufforderung bezieht sich auf das Active Directory-Benutzerkonto. Da beide Eingabeaufforderungen identisch aussehen, achten Sie darauf, dass Sie die richtige Reihenfolge einhalten.  

6. Warten Sie, bis die Meldung angezeigt wird, dass die **Anmeldung erfolgreich** war.  

7. Öffnen Sie auf dem Macintosh-Computer ein Terminalfenster, und nehmen Sie folgende Änderungen vor, um das registrierte Zertifikat auf Configuration Manager zu beschränken:  

    1. Geben Sie den Befehl `sudo /Applications/Utilities/Keychain Access.app/Contents/MacOS/Keychain Access` ein.  

    2. Wählen Sie im Fenster **Schlüsselbundverwaltung** im Abschnitt **Schlüsselbunde** die Option **System** aus. Wählen Sie anschließend im Abschnitt **Kategorie** die Option **Zertifikate** aus.  

    3. Erweitern Sie die Schlüssel, um die Clientzertifikate anzuzeigen. Suchen Sie nach dem Zertifikat mit einem privaten Schlüssel, den Sie installiert haben, und öffnen Sie den Schlüssel.  

    4. Wählen Sie auf der Registerkarte **Zugriffssteuerung** die Option **Confirm before allowing access** (Bestätigen, bevor Zugriff zugelassen wird) aus.  

    5. Navigieren Sie zum Ordner **/Library/Application Support/Microsoft/CCM**, wählen Sie **CCMClient** aus, und wählen Sie dann **Hinzufügen** aus.  

    6. Wählen Sie **Änderungen sichern** aus, und schließen Sie das Dialogfeld **Schlüsselbundverwaltung**.  

8. Starten Sie den Macintosh-Computer neu.  

Überprüfen Sie, ob die Clientinstallation erfolgreich ausgeführt wurde. Öffnen Sie hierzu auf dem Mac-Computer in den **Systemeinstellungen** das Element **Configuration Manager**. Aktualisieren Sie in der Configuration Manager-Konsole zudem die Sammlung **Alle Systeme**, und zeigen Sie diese an. Bestätigen Sie, dass der Mac-Computer in dieser Sammlung als verwalteter Client aufgeführt ist.  

> [!TIP]  
> Mögliche Probleme mit dem Mac-Client können Sie mithilfe des **CMDiagnostics-Tools** beheben, das in dem Mac-Clientpaket enthalten ist. Verwenden Sie es, um folgende Diagnoseinformationen zu sammeln:  
>   
> - Eine Liste der ausgeführten Prozesse  
> - Die Version des Mac OS X-Betriebssystems  
> - Mac OS X-Absturzberichte, die sich auf den Configuration Manager-Client beziehen, einschließlich **CCM\*.crash** und **System Preference.crash**.  
> - Die BOM-Datei (Bill of Materials) und die Eigenschaftenlistendatei (PLIST-Datei), die im Rahmen der Configuration Manager-Clientinstallation erstellt wurden  
> - Der Inhalt des Ordners **/Library/Application Support/Microsoft/CCM/Logs**  
>   
> Die von „CmDiagnostics“ gesammelten Informationen werden einer ZIP-Datei (`cmdiag-<hostname>-<datetime>.zip`) hinzugefügt, die auf dem Desktop des Computers gespeichert wird.



## <a name="manage-certificates-external-to-configuration-manager"></a><a name="bkmk_external"></a> Verwalten von Zertifikaten außerhalb von Configuration Manager

Sie können eine von Configuration Manager unabhängige Zertifikatanforderungs- und -installationsmethode verwenden. Führen Sie zunächst die gleichen allgemeinen Schritte aus, und fügen Sie dann die folgenden Schritte hinzu: 

- Verwenden Sie bei der Installation des Konfigurations-Manager-Clients die Befehlszeilenoptionen **MP** und **SubjectName**. Geben Sie den folgenden Befehl ein: `sudo ./ccmsetup -MP <management point internet FQDN> -SubjectName <certificate subject name>`. Beim Namen für den Zertifikatantragsteller muss die Groß-/Kleinschreibung beachtet werden, daher muss dieser genauso eingegeben werden, wie er in den Zertifikatdetails angezeigt wird.  

     Beispiel: Der Internet-FQDN des Verwaltungspunkts lautet **server03.contoso.com**. Das Mac-Clientzertifikat verwendet den FQDN **mac12.contoso.com** als allgemeinen Namen im Zertifikatantragsteller. Verwenden Sie den folgenden Befehl: `sudo ./ccmsetup -MP server03.contoso.com -SubjectName mac12.contoso.com`.  

- Wenn Sie über mehrere Zertifikate mit dem gleichen Wert für den Antragsteller verfügen, geben Sie die Seriennummer des Zertifikats für den Konfigurations-Manager-Client an. Verwenden Sie den folgenden Befehl: `sudo defaults write com.microsoft.ccmclient SerialNumber -data "<serial number>"`.  

     Beispiel: `sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"`  



## <a name="renew-the-mac-client-certificate"></a>Erneuern des Mac-Clientzertifikats  

Bei dieser Prozedur wird die SMS-ID entfernt. Der Konfigurations-Manager-Client für Mac erfordert eine neue ID zur Verwendung eines neuen oder erneuerten Zertifikats.  

> [!IMPORTANT]  
> Nachdem Sie die Client-SMS-ID ersetzt haben, wird beim Löschen der alten Ressource in der Configuration Manager-Konsole auch der gespeicherte Clientverlauf gelöscht. Dies kann zum Beispiel der Hardwareinventurverlauf für diesen Client sein.  


1. Erstellen Sie für die Mac-Computer, deren Benutzerzertifikate verlängert werden müssen, eine Gerätesammlung.  

2. Starten Sie im Arbeitsbereich **Bestand und Kompatibilität** den **Assistenten zum Erstellen von Konfigurationselementen**.  

3. Geben Sie auf der Seite **Allgemein** des Assistenten die folgenden Informationen an:  

    - **Name:** **SMS-ID für Mac entfernen**  

    - **Typ:** **Mac OS X**  

4. Wählen Sie auf der Seite **Unterstützte Plattformen** alle Mac OS X-Versionen aus.  

5. Wählen Sie auf der Seite **Einstellungen** die Option **Neu** aus. Geben Sie im Fenster **Einstellung erstellen** die folgenden Informationen ein:  

    - **Name:** **SMS-ID für Mac entfernen**  

    - **Einstellungstyp:** **Skript**  

    - **Datentyp:** **Zeichenfolge**  

6. Wählen Sie im Fenster **Einstellung erstellen** für **Ermittlungsskript** die Option **Skript hinzufügen** aus. Mit dieser Aktion wird ein Skript festgelegt, um mit einer SMS-ID konfigurierte Mac-Computer zu ermitteln.  

7. Geben Sie im Fenster **Ermittlungsskript bearbeiten** das folgende Shellskript ein:  

    ``` Shell
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8. Wählen Sie **OK** aus, um das Fenster **Ermittlungsskript bearbeiten** zu schließen.  

9. Wählen Sie im Fenster **Einstellung erstellen** für **Wiederherstellungsskript (optional)** die Option **Skript hinzufügen** aus. Mit dieser Aktion wird ein Skript festgelegt, um die SMS-ID zu entfernen, wenn diese auf Mac-Computern gefunden wird.  

10. Geben Sie im Fenster **Wiederherstellungsskript erstellen** das folgende Shellskript ein:  

    ``` Shell
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Wählen Sie **OK** aus, um das Fenster **Wiederherstellungsskript erstellen** zu schließen.  

12. Wählen Sie auf der Seite **Konformitätsregeln** die Option **Neu** aus. Geben Sie im Fenster **Regel erstellen** die folgenden Informationen ein:  

    - **Name:** **SMS-ID für Mac entfernen**  

    - **Ausgewählte Einstellung:** Wählen Sie **Durchsuchen** aus, und wählen Sie dann das Ermittlungsskript aus, das Sie zuvor angegeben haben.  

    - Gehen Sie im Feld **die folgenden Werte** wie folgt vor: **Das Domänen-/Standardpaar (com.microsoft.ccmclient, SMS-ID) ist nicht vorhanden**.  

    - Aktivieren Sie die Option **Das angegebene Wiederherstellungsskript ausführen, wenn diese Einstellung nicht konform ist**.  

13. Schließen Sie den Assistenten ab.  

14. Erstellen Sie eine Konfigurationsbaseline, die dieses Konfigurationselement enthält. Stellen Sie die Baseline in der Zielsammlung bereit.  

     Weitere Informationen finden Sie unter [Vorgehensweise: Erstellen von Konfigurationsbaselines](../../../compliance/deploy-use/create-configuration-baselines.md).  

15. Führen Sie den folgenden Befehl aus, nachdem Sie ein neues Zertifikat auf Mac-Computern mit entfernter SMS-ID installiert haben, um den Client so zu konfigurieren, dass das neue Zertifikat verwendet wird:  

    ``` Shell
    sudo defaults write com.microsoft.ccmclient SubjectName -string <subject_name_of_new_certificate>  
    ```  



## <a name="see-also"></a>Weitere Informationen:

[Vorbereiten der Bereitstellung von Clients auf Macintosh-Computern](prepare-to-deploy-mac-clients.md)

[Warten von Macintosh-Clients](../manage/maintain-mac-clients.md)
