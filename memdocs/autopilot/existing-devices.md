---
title: Windows Autopilot-Bereitstellung für vorhandene Geräte
description: Mit der modernen Desktop Bereitstellung mit Windows Autopilot können Sie die neueste Version von Windows 10 auf Ihren vorhandenen Geräten problemlos bereitstellen.
keywords: MDM, Setup, Windows, Windows 10, OOBE, Manage, Bereitstellung, Autopilot, ZTD, Zero-Touchscreen, Partner, msfb, InTune
ms.reviewer: mniehaus
manager: laurawi
ms.prod: w10
ms.technology: windows
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: 685466a9760fa8aa688e76b10e1f44b7ac9eb37e
ms.sourcegitcommit: d4ed7b4369389fd8ab07d28a7fa507797b6c6e57
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89643559"
---
# <a name="windows-autopilot-deployment-for-existing-devices"></a>Windows Autopilot-Bereitstellung für vorhandene Geräte

**Gilt für: Windows 10**

Bei der modernen Desktop Bereitstellung mit Windows Autopilot können Sie die neueste Version von Windows 10 auf Ihren vorhandenen Geräten problemlos bereitstellen. Die apps, die Sie für die Arbeit benötigen, können automatisch installiert werden. Ihr Arbeitsprofil ist synchronisiert, sodass Sie sofort mit der Arbeit fortfahren können.

In diesem Thema wird beschrieben, wie Sie Windows 7 oder Windows 8.1 in die Domäne eingebundenen Computer in Windows 10-Geräte konvertieren können, die mit Windows Autopilot entweder mit Azure Active Directory oder Active Directory (Azure AD Hybrid Join) verknüpft sind.

>[!NOTE]
>Windows Autopilot für vorhandene Geräte unterstützt nur benutzergesteuerte Azure Active Directory und Azure AD Hybrid Profile. Selbst Bereitstellungs Profile werden nicht unterstützt.

## <a name="prerequisites"></a>Voraussetzungen

- Eine derzeit unterstützte Version von Microsoft Endpoint Configuration Manager Current Branch-oder Technical Preview-Branch. 
- [Windows ADK](https://developer.microsoft.com/en-us/windows/hardware/windows-assessment-deployment-kit) 1803 oder höher
    - Weitere Informationen zur Configuration Manager Unterstützung finden Sie [unter Unterstützung für Windows 10 ADK](/configmgr/core/plan-design/configs/support-for-windows-10#windows-10-adk).
- Zugewiesene Microsoft InTune Lizenzen
- Azure Active Directory Premium
- Windows 10, Version 1809 oder höher, in Configuration Manager als Betriebs System Abbild importiert
  - **Wichtig**: Weitere Informationen finden Sie unter [bekannte Probleme](known-issues.md) bei Verwendung von Windows 10 1903 Configuration Manager mit der integrierten Windows Autopilot-Tasksequenz Vorlage für **Windows Autopilot** . Derzeit muss einer der Schritte in dieser Tasksequenz so bearbeitet werden, dass er ordnungsgemäß mit Windows 10, Version 1903, funktioniert.

## <a name="procedures"></a>Prozeduren

### <a name="configure-the-enrollment-status-page-optional"></a>Konfigurieren der Seite "Anmeldungs Status" (optional)

Wenn Sie möchten, können Sie eine Seite zum Registrierungs [Status](enrollment-status.md) für Autopilot mithilfe von InTune einrichten.

So aktivieren und konfigurieren Sie die Seite "Registrierung und Status":

1. Öffnen Sie [InTune in der Azure-Portal](https://aka.ms/intuneportal).
2. Greifen Sie auf **InTune > Geräteregistrierung > Windows** -Registrierung zu [, und richten Sie eine Seite zum Registrierungsstatus ein](/intune/windows-enrollment-status). 
3. Greifen Sie auf **Azure Active Directory > Mobility (MDM und MAM) > Microsoft InTune** , und konfigurieren Sie die [Automatische MDM](/configmgr/mdm/deploy-use/enroll-hybrid-windows#enable-windows-10-automatic-enrollment) -Registrierung, und konfigurieren Sie den MDM-Benutzerbereich für einige oder alle Benutzer. 

Weitere Informationen finden Sie in den folgenden Beispielen.

![Seite "Registrierungsstatus"](images/esp-config.png)<br><br>
![mdm](images/mdm-config.png)

### <a name="create-the-json-file"></a>Erstellen der JSON-Datei 

>[!TIP]
>Um die folgenden Befehle auf einem Computer mit Windows Server 2012/2012 R2 oder Windows 7/8.1 auszuführen, müssen Sie zuerst das [Windows Management Framework](https://www.microsoft.com/download/details.aspx?id=54616)herunterladen und installieren.

1. Öffnen Sie auf einem Windows-PC oder-Server mit Internet Verbindung ein Windows PowerShell-Befehlsfenster mit erhöhten Rechten.
2. Geben Sie die folgenden Zeilen ein, um die erforderlichen Module zu installieren:

    #### <a name="install-required-modules"></a>Erforderliche Module installieren

    ```powershell
    Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force
    Install-Module AzureAD -Force
    Install-Module WindowsAutopilotIntune -Force
    Install-Module Microsoft.Graph.Intune -Force
    ```
   
3. Geben Sie die folgenden Zeilen ein, und geben Sie InTune-Anmelde Informationen an
   - Stellen Sie sicher, dass das von Ihnen angegebene Benutzerkonto über ausreichende Administratorrechte verfügt.

     ```powershell
     Connect-MSGraph
     ```
     Der Benutzer und das Kennwort für Ihr Konto werden mit einem Standard Azure AD Formular angefordert. Geben Sie Ihren Benutzernamen und Ihr Kennwort ein, und klicken Sie auf **Anmelden** 
     <br>Sehen Sie sich folgendes Beispiel an:

     ![Azure AD-Authentifizierung](images/pwd.png)

     Wenn Sie die Intune Graph-APIs zum ersten Mal verwenden, werden Sie aufgefordert, Microsoft InTune PowerShell-Lese-und Schreibberechtigungen zu aktivieren. So aktivieren Sie diese Berechtigungen
   - Wählen Sie **die Zustimmung im Namen oder Ihrer Organisation aus** .
   - Klicken Sie auf **Annehmen**.

4. Anschließend rufen Sie alle Autopilot-Profile ab, die im angegebenen InTune-Mandanten im JSON-Format verfügbar sind, und zeigen Sie an:

    #### <a name="retrieve-profiles-in-autopilot-for-existing-devices-json-format"></a>Abrufen von Profilen im Autopilot für vorhandene Geräte im JSON-Format

    ```powershell
    Get-AutopilotProfile | ConvertTo-AutopilotConfigurationJSON
    ```

    Sehen Sie sich die folgende Beispielausgabe an: (verwenden Sie die horizontale Schiebe Leiste unten zum Anzeigen von langen Zeilen)
    <pre style="overflow-y: visible">
    PS C:\> Get-AutopilotProfile | ConvertTo-AutopilotConfigurationJSON
    {
        "CloudAssignedTenantId": "1537de22-988c-4e93-b8a5-83890f34a69b",
        "CloudAssignedForcedEnrollment": 1,
        "Version": 2049,
        "Comment_File": "Profile Autopilot Profile",
        "CloudAssignedAadServerData": "{\"ZeroTouchConfig\":{\"CloudAssignedTenantUpn\":\"\",\"ForcedEnrollment\":1,\"CloudAssignedTenantDomain\":\"M365x373186.onmicrosoft.com\"}}",
        "CloudAssignedTenantDomain": "M365x373186.onmicrosoft.com",
        "CloudAssignedDomainJoinMethod": 0,
        "CloudAssignedOobeConfig": 28,
        "ZtdCorrelationId": "7F9E6025-1E13-45F3-BF82-A3E8C5B59EAC"
    }</pre>

    Jedes Profil ist in geschweiften Klammern **{}** gekapselt. Im vorherigen Beispiel wird ein einzelnes Profil angezeigt.

    In der folgenden Tabelle finden Sie eine Beschreibung der Eigenschaften, die in der JSON-Datei verwendet werden.


   |                          Eigenschaft                          |                                                                                                                                                                        BESCHREIBUNG                                                                                                                                                                         |
   |------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |                 Version (Zahl, optional)                 | Die Versionsnummer, die das Format der JSON-Datei identifiziert. Für Windows 10 1809 muss die angegebene Version 2049 lauten.                                                                                                                  |
   |           Cloudassignedtenantid (GUID, erforderlich)           | Die Azure Active Directory Mandanten-ID, die verwendet werden soll. Diese Eigenschaft ist die GUID für den Mandanten und befindet sich in den Eigenschaften des Mandanten. Der Wert darf keine geschweiften Klammern enthalten.                                                                                       |
   |        Cloudassignedtenantdomain (Zeichenfolge, erforderlich)        | Der Name des Azure Active Directory Mandanten, der verwendet werden soll, z. b.: Tenant.onmicrosoft.com.                                                                                                                                  |
   |         Cloudassignetdoobeconfig (Zahl, erforderlich)         | Diese Eigenschaft ist eine Bitmap, die anzeigt, welche Autopilot-Einstellungen konfiguriert wurden. Folgende Werte sind verfügbar: skipcortanaoptin = 1, oobeusernotlocaladmin = 2, skipexpress Settings = 4, skipoemregistration = 8, skipep = 16                                                                           |
   |      Cloudassigneddomainjoinmethod (Zahl, erforderlich)      |                                                                                                                                    Diese Eigenschaft gibt an, ob das Gerät Azure Active Directory oder Active Directory (Azure AD Hybrid Join) beitreten soll. Folgende Werte sind enthalten: Active AD Join = 0, Azure AD Hybrid Join = 1                                                        |
   |      Cloudassignedforcedenrollment (Zahl, erforderlich)      |                                                                                                                         Gibt an, dass das Gerät Azure AD beitreten und die MDM-Registrierung erfordern soll. <br>0 = nicht erforderlich, 1 = erforderlich.                                                                                                                         |
   |             Ztdcorrelationid (GUID, erforderlich)              | Eine eindeutige GUID (ohne geschweifte Klammern), die Intune als Teil des Registrierungsprozesses bereitgestellt wird. Ztdcorrelationid wird in der Registrierungs Nachricht als "offlineautopilotenrollmentcorrelator" eingeschlossen. Dieses Attribut ist nur vorhanden, wenn die Registrierung auf einem Gerät stattfindet, das bei der Zero-Touchscreen-Bereitstellung über die Offline Registrierung registriert ist. |
   | Cloudassignedaadserverdata (codierte JSON-Zeichenfolge, erforderlich) |                                                  Eine eingebettete JSON-Zeichenfolge für das Branding. Hierfür muss Azure AD Corp-Branding aktiviert werden. <br> Beispiel Wert: "cloudassignedaadserverdata": "{ \" zerotouchconfig \" : { \" cloudassignedtenantupn \" : \" \" , \" cloudassignedtenantdomain \" : \" Tenant.onmicrosoft.com \" }}"                                                   |
   |         Cloudassigneddevicename (Zeichenfolge, optional)         | Der Name, der dem Computer automatisch zugewiesen wird. Dies folgt der in InTune Autopilot profile konfigurierten Benennungs Muster Konvention. Oder Sie können einen expliziten Namen angeben, der verwendet werden soll. |


5. Das Autopilot-Profil muss als JSON-Datei im ASCII-oder ANSI-Format gespeichert werden. Windows PowerShell verwendet standardmäßig das Unicode-Format. Wenn Sie also die Ausgabe der Befehle in eine Datei umleiten, geben Sie auch das Dateiformat an. Wenn Sie die Datei beispielsweise mithilfe von Windows PowerShell im ASCII-Format speichern möchten, können Sie ein Verzeichnis erstellen (z. b. c:\autopilot) und das Profil speichern, wie unten gezeigt: (verwenden Sie die horizontale Schiebe Leiste unten, wenn dies erforderlich ist, um die gesamte Befehls Zeichenfolge anzuzeigen)

    ```powershell
    Get-AutopilotProfile | ConvertTo-AutopilotConfigurationJSON | Out-File c:\Autopilot\AutopilotConfigurationFile.json -Encoding ASCII
    ```
    **Wichtig**: der Dateiname muss **AutopilotConfigurationFile.json** lauten und als ASCII/ANSI codiert werden. 

    Wenn Sie dies bevorzugen, können Sie das Profil in einer Textdatei speichern und im Editor bearbeiten. Wenn Sie in Editor die Option **Speichern** unter auswählen, müssen Sie Dateityp: **alle Dateien** auswählen und ANSI in der Dropdown Liste neben **Codierung**auswählen. Siehe folgendes Beispiel.

    ![Notepad-JSON](images/notepad.png)

    Verschieben Sie die Datei nach dem Speichern an einen Speicherort, der als Microsoft-Endpunkt Configuration Manager Paketquelle geeignet ist.

    >[!IMPORTANT]
    >Es können mehrere JSON-Profil Dateien verwendet werden, aber jeder muss mit dem Namen **AutopilotConfigurationFile.js** werden, damit OOBE das Autopilot-Verhalten befolgt. Die Datei muss auch als ANSI codiert werden. <br><br>**Das Speichern der Datei mit Unicode-oder UTF-8-Codierung oder das Speichern mit einem anderen Dateinamen bewirkt, dass Windows 10 OOBE dem Autopilot-Vorgang nicht folgt**.<br>


### <a name="create-a-package-containing-the-json-file"></a>Erstellen eines Pakets, das die JSON-Datei enthält

1. Navigieren Sie in Configuration Manager zu **\Software library\overview\anwendungsmanagement\packages** .
2. Klicken Sie im Menüband auf **Paket erstellen** .
3. Geben Sie im **Assistenten zum Erstellen von Paketen und Programmen** die folgenden **Paket** -und **Programmtyp** Details ein:<br>
    - <u>Name</u>: **Autopilot für vorhandene Gerätekonfiguration**
    - Wählen Sie **Dieses Paket enthält Quelldateien** aus.
    - <u>Quellordner</u>: Klicken Sie auf **Durchsuchen** , und geben Sie einen UNC-Pfad an, der die Datei AutopilotConfigurationFile.jsenthält 
    - Klicken Sie auf **OK** und anschließend auf **Weiter**.
    - <u>Programmtyp</u>: kein **Programm erstellen**
4. Klicken Sie zweimal auf **weiter** und dann auf **Schließen**.

**Hinweis**: Wenn Sie die Einstellungen für das benutzergesteuerte Autopilot-Profil in InTune zu einem späteren Zeitpunkt ändern, müssen Sie auch die JSON-Datei aktualisieren und das zugehörige Configuration Manager Paket erneut verteilen.

### <a name="create-a-target-collection"></a>Erstellen einer Ziel Sammlung

>[!NOTE]
>Sie können auch eine vorhandene Sammlung wieder verwenden.

1. Navigieren Sie zu " **\assets" und "compliance\overview\device Collections** ".
2. Klicken Sie im Menüband auf **Erstellen** und dann auf **Geräte Sammlung erstellen** .
3. Geben Sie im **Assistenten zum Erstellen von Geräte Sammlungen** die folgenden **allgemeinen** Informationen ein:
   - <u>Name</u>: **Autopilot für vorhandene Geräte Sammlung**
   - Kommentar: (optional)
   - <u>Begrenzende Sammlung</u>: Klicken Sie auf **Durchsuchen** , **und wählen Sie**

     >[!NOTE]
     >Optional können Sie auch eine Alternative Sammlung für die begrenzende Sammlung verwenden. Auf dem zu aktualisierenden Gerät muss der ConfigMgr-Agent in der von Ihnen ausgewählten Sammlung ausgeführt werden.

4. Klicken Sie auf **weiter**, und geben Sie die folgenden **Mitgliedschafts Regel** Details ein:
   - Klicken Sie auf **Regel hinzufügen** , und geben Sie entweder eine direkte oder eine Abfrage basierte Sammlungs Regel an, um der neuen Sammlung die Windows 7-Zielgeräte hinzuzufügen.
   - Wenn beispielsweise der Hostname des Computers, der zurückgesetzt und neu geladen werden soll, PC-01 ist und Sie den Namen als Attribut verwenden möchten:
      1. Klicken Sie auf **Regel hinzufügen > direkt Regel > (Assistent wird geöffnet) > weiter**.
      2. Geben Sie **PC-01** neben **Wert**ein.
      3. Klicken Sie auf **Next**  >  **PC-01** (unter **Ressourcen**). Weitere Informationen finden Sie in den folgenden Beispielen.

         ![Ressourcen suchen (Dialogfeld) ](images/pc-01a.png)
          ![ Ressourcen auswählen (Dialogfeld)](images/pc-01b.png)

5. Erstellen Sie die Geräte Sammlung mit den Standardeinstellungen weiter:
    - Inkrementelle Updates für diese Sammlung verwenden: nicht ausgewählt
    - Vollständiges Update für diese Sammlung planen: Standard
    - Klicken Sie zweimal auf **weiter** und dann auf **Schließen** .

### <a name="create-an-autopilot-for-existing-devices-task-sequence"></a>Erstellen eines Autopilot für vorhandene Geräte (Task Sequenz)

>[!TIP]
>Für das nächste Verfahren ist ein Start Abbild für Windows 10 1803 oder höher erforderlich. Überprüfen Sie die verfügbaren Start Abbilder in der Configuration Manager-Datei unter " **Software library\overview\operating systems\boot Images** ", und vergewissern Sie sich, dass die **Betriebssystem Version** 10.0.17134.1 (Windows 10, Version 1803) oder höher lautet.

1. Navigieren Sie in der Configuration Manager Konsole zu " **\Software library\overview\operating systems\task Sequenzen** ".
2. Klicken Sie auf dem Menüband Start auf **Task Sequenz erstellen** .
3. Wählen Sie **bestehendes Abbild Paket installieren** aus, und klicken Sie auf **weiter** .
4. Geben Sie im Tasksequenzerstellungs-Assistenten die folgenden Details ein:
   - <u>Task Sequenz Name</u>: **Autopilot für vorhandene Geräte**
   - <u>Startimage</u>: Klicken Sie auf **Durchsuchen** , und wählen Sie ein Windows 10-Start Abbild (1803 oder höher)
   - Klicken Sie auf **weiter**  >  **Durchsuchen** > wählen Sie ein Windows 10- **Abbild Paket** und **Abbild Index**, Version 1803 oder höher aus.
   - Aktivieren Sie das Kontrollkästchen **Zielcomputer vor Installation des Betriebssystems partitionieren und formatieren** .
   - Aktivieren oder deaktivieren Sie das Kontrollkästchen **Tasksequenz für die Verwendung mit BitLocker konfigurieren** . Diese Eingabe ist optional.
   - <u>Product Key</u> -und <u>Server Lizenzierungs Modus</u>: Geben Sie optional einen Product Key-und Server Lizenzierungs Modus ein.
   - <u>Lokales Administrator Kennwort zufällig generieren und das Konto auf allen unterstützten Plattformen deaktivieren (empfohlen)</u>: optional.
   - <u>Aktivieren Sie das Konto, und geben Sie das lokale Administrator Kennwort</u>an: optional.
   - Klicken Sie auf **weiter**, und wählen Sie dann auf der Seite Netzwerk konfigurieren die Option **einer Arbeitsgruppe beitreten** aus, und geben Sie einen Namen (z. b. Arbeitsgruppe) neben **Arbeitsgruppe**ein.

     > [!IMPORTANT]
     > Die Tasksequenz "Autopilot for vorhandene Geräte" führt die Aktion " **Windows für die Erfassung vorbereiten" aus, bei** der das System Vorbereitungs Tool (syunp) verwendet wird. Diese Aktion schlägt fehl, wenn der Zielcomputer einer Domäne hinzugefügt wird.
     
     >[!IMPORTANT]
     > Das System Vorbereitungs Tool (sycrip) wird mit dem/generalize-Parameter ausgeführt, der in den Windows 10-Versionen 1903 und 1909 die Autopilot-Profil Datei löscht, und der Computer wird in der OOBE-Phase statt in der Autopilot-Phase gestartet. Um dieses Problem zu beheben, finden Sie weitere Informationen unter [Windows Autopilot-bekannte Probleme](known-issues.md).

5. Klicken Sie auf **weiter**, und klicken Sie dann erneut auf **weiter** , um die Standardeinstellungen auf der Seite Configuration Manager installieren zu übernehmen.
6. Geben Sie auf der Seite Zustands Migration die folgenden Details ein:
   - Deaktivieren Sie das Kontrollkästchen **Benutzereinstellungen und Dateien erfassen** .
   - Deaktivieren Sie das Kontrollkästchen **Netzwerkeinstellungen erfassen** .
   - Deaktivieren Sie das Kontrollkästchen **Microsoft Windows-Einstellungen erfassen** .
   - Klicken Sie auf **Weiter**.

     >[!NOTE]
     >Da die Tasksequenz Autopilot für vorhandene Geräte in Windows PE abgeschlossen wird, wird die Migration des User State Migration Toolkit (USMT) nicht unterstützt, da es keine Möglichkeit gibt, den Benutzer Zustand im neuen Betriebssystem wiederherzustellen. Außerdem unterstützt das User State Migration Toolkit (USMT) keine Geräte, die Azure AD verknüpft sind.

7. Wählen Sie auf der Seite Updates einschließen eine der drei verfügbaren Optionen aus. Diese Auswahl ist optional.
8. Auf der Seite Anwendungen installieren können Sie optional Anwendungen hinzufügen.
9. Klicken Sie auf **weiter**, bestätigen Sie die Einstellungen, klicken Sie auf **weiter**und dann auf **Schließen**.
10. Klicken Sie mit der rechten Maustaste auf die Aufgabe Autopilot für vorhandene Geräte, und klicken Sie auf **Bearbeiten**.
11. Klicken Sie im Task Sequenz-Editor unter der Gruppe **Betriebs System installieren** auf die Aktion **Windows-Einstellungen anwenden** .
12. Klicken Sie auf **Hinzufügen** und dann auf **neue Gruppe**.
13. Ändern Sie den Gruppen **Namen** von " **neue Gruppe** " in " **Autopilot" für vorhandene Gerätekonfiguration**.
14. Klicken Sie auf **Hinzufügen**, zeigen Sie auf **Allgemein**, und klicken Sie dann auf **Befehlszeile ausführen**.
15. Vergewissern Sie sich, dass der Schritt **Befehlszeile ausführen** unter der **Konfigurations Gruppe Autopilot for existierende Devices (Autopilot für vorhandene Geräte** ) angezeigt wird.
16. Ändern Sie den **Namen** zum **Anwenden von Autopilot für vorhandene Geräte Konfigurationsdatei**, und fügen Sie Folgendes in das Textfeld **Befehlszeile** ein > **anwenden**:
    ```
    cmd.exe /c xcopy AutopilotConfigurationFile.json %OSDTargetSystemDrive%\windows\provisioning\Autopilot\ /c
    ```
    - **AutopilotConfigurationFile.json** muss der Name der JSON-Datei sein, die im zuvor erstellten Paket Autopilot für vorhandene Geräte enthalten ist.

17. Wählen Sie im Schritt **Autopilot für vorhandene Geräte der Konfigurationsdatei anwenden** das **Paket**  >  **Durchsuchen**aus.
18. Wählen Sie das zuvor erstellte **Konfigurations Paket Autopilot für vorhandene Geräte aus** , und klicken Sie auf **OK**. Am Ende dieses Abschnitts wird ein Beispiel angezeigt.
19. Klicken Sie unter der Gruppe **Setup Betriebs System** auf den Task **Windows und Configuration Manager einrichten** .
20. Klicken Sie auf **Hinzufügen** und dann auf **neue Gruppe**.
21. Ändern Sie den **Namen** der **neuen Gruppe** , um das **Gerät für Autopilot vorzubereiten** .
22. Vergewissern Sie sich, dass die Gruppe **Vorbereiten des Geräts für Autopilot** der letzte Schritt in der Tasksequenz ist. Verwenden Sie ggf. die Schaltfläche **nach unten** .
23. Klicken Sie bei ausgewählter Option **Gerät für Autopilot vorbereiten** auf **Hinzufügen**, zeigen Sie auf **Bilder** , und klicken Sie dann auf **ConfigMgr-Client für Erfassung vorbereiten**.
24. Fügen Sie einen zweiten Schritt hinzu, indem Sie auf **Hinzufügen**klicken, auf **Bilder**zeigen und dann auf **Windows für die Erfassung vorbereiten**klicken. Verwenden Sie in diesem Schritt die folgenden Einstellungen:
    - <u>Liste der Massenspeicher Treiber automatisch erstellen</u>: **nicht ausgewählt**
    - <u>Aktivierungs Kennzeichen nicht zurücksetzen</u>: **nicht ausgewählt**
    - <u>Computer nach dem Ausführen dieser Aktion herunter</u>fahren: **optional**

    ![Autopilot-Tasksequenz](images/ap-ts-1.png)

25. Klicken Sie auf **OK**, um den Tasksequenz-Editor zu schließen.

> [!NOTE]
> Unter Windows 10 1903 und 1909 wird der **AutopilotConfigurationFile.jsauf** dem Schritt **Windows für die Erfassung vorbereiten** gelöscht. Weitere Informationen und eine Problem Umgehung finden Sie unter [Windows Autopilot-Known Issues](known-issues.md).

### <a name="deploy-content-to-distribution-points"></a>Bereitstellen von Inhalten für Verteilungs Punkte

Stellen Sie als nächstes sicher, dass alle für die Tasksequenz erforderlichen Inhalte auf Verteilungs Punkten bereitgestellt werden.

1. Klicken Sie mit der rechten Maustaste auf die Tasksequenz **Autopilot für vorhandene Geräte** , und klicken Sie auf **Inhalt verteilen**.
2. Klicken Sie auf **weiter**, **Überprüfen Sie den zu verteilenden Inhalt**, und klicken Sie auf **weiter**.
3. Klicken Sie auf der Seite Inhalts Verteilung angeben auf **Hinzufügen** , um einen **Verteilungs Punkt** oder eine **Verteilungs Punkt Gruppe**anzugeben.
4. Geben Sie im Assistenten zum Hinzufügen von Verteilungs Punkten oder Verteilungs Punkt Gruppen hinzufügen Inhalts Ziele an, mit denen die Tasksequenz die JSON-Datei abrufen kann.
5. Wenn Sie mit der Angabe der Inhalts Verteilung fertig sind, klicken Sie zweimal auf **weiter** und dann auf **Schließen**.

### <a name="deploy-the-os-with-autopilot-task-sequence"></a>Bereitstellen des Betriebssystems mit Autopilot-Task Sequenz

1. Klicken Sie mit der rechten Maustaste auf die Aufgabe **Autopilot für vorhandene Geräte** , und klicken Sie **dann auf bereitstellen.**
2. Geben Sie im Assistenten zum Bereitstellen von Software die folgenden Details für **Allgemeine** und **Bereitstellungs Einstellungen** ein:
    - <u>Task Sequenz</u>: **Autopilot für vorhandene Geräte**.
    - <u>Sammlung</u>: Klicken Sie auf **Durchsuchen** , und wählen Sie dann **Autopilot für vorhandene Geräte Sammlung** (oder eine andere von Ihnen bevorzugte Sammlung) aus.
    - Klicken Sie auf **weiter** , um die **Bereitstellungs Einstellungen**anzugeben.
    - <u>Aktion</u>: **Installieren**Sie.
    - <u>Zweck</u>: **verfügbar**. Optional können Sie die Option **erforderlich** anstelle von **verfügbar**auswählen. Diese Einstellung wird während des Tests nicht empfohlen, da unbeabsichtigte Konfigurationen negative Auswirkungen haben können.
    - <u>Stellen Sie Folgendes zur Verfügung</u>: **nur Configuration Manager Clients**. Hinweis: Wählen Sie hier die Option aus, die für den Kontext des Tests relevant ist. Wenn der Configuration Manager-Agent oder Windows auf dem Ziel Client nicht installiert ist, müssen Sie eine Option auswählen, die PXE oder Start Medien enthält.
    - Klicken Sie auf **weiter** , um Zeit **Plan Details anzugeben** .
    - <u>Zeitpunkt der Verfügbarkeit dieser Bereitstellung planen</u>: optional
    - Ablaufdatum <u>der Bereitstellung</u>festlegen: optional
    - Klicken Sie auf **weiter** , um Details zur **Benutzer** Darstellung anzugeben.
    - <u>Task Sequenz Status anzeigen</u>: ausgewählt.
    - <u>Software Installation</u>: nicht ausgewählt.
    - <u>System Neustart (falls dieser zum Abschluss der Installation erforderlich ist)</u>: nicht ausgewählt.
    - <u>Commit wurde zum Stichtag oder während eines Wartungsfenster geändert (Neustart erforderlich)</u>: optional.
    - <u>Ausführen der Tasksequenz für den Client im Internet zulassen</u>: optional
    - Klicken Sie auf **weiter** , um Warnungs **Details anzugeben** .
    - <u>Erstellen Sie eine Bereitstellungs Warnung, wenn der Schwellenwert höher ist als der folgende</u>: optional.
    - Klicken Sie auf **weiter** , um Details zu **Verteilungs Punkten** anzugeben.
    - <u>Bereitstellungs Optionen</u>: **Inhalt lokal herunterladen, wenn dies für die Ausführung der Tasksequenz erforderlich**ist.
    - <u>Wenn kein lokaler Verteilungs Punkt verfügbar ist, verwenden Sie einen Remote Verteilungs Punkt</u>: optional.
    - <u>Clients die Verwendung von Verteilungs Punkten aus der standardmäßigen Standort Begrenzungs Gruppe gestatten</u>: optional.
    - Klicken Sie auf **weiter**, bestätigen Sie die Einstellungen, klicken Sie auf **weiter**und dann auf **Schließen**.

### <a name="complete-the-client-installation-process"></a>Schließen Sie den Client Installationsprozess ab.

1. Wählen Sie auf dem Windows 7-oder Windows 8.1 Client Computer starten > geben Sie **Software Center** ein > drücken Sie die EINGABETASTE.

2. Wählen Sie in der Software Bibliothek **Autopilot für vorhandene Geräte aus** , und klicken Sie auf **Installieren**. Sehen Sie sich folgendes Beispiel an:

    ![](images/sc.png)Dialogfeld zur Bestätigung der Seite Autopilot für vorhandene Geräte ![](images/sc1.png)

Die Task Sequenz führt Folgendes aus:
1. Inhalt herunterladen
2. Neustarten des Geräts
3. Formatieren der Laufwerke
4. Installieren von Windows 10
5. Auf Autopilot vorbereiten

Nachdem die Tasksequenz abgeschlossen wurde, wird das Gerät in OOBE gestartet und bietet einen Autopilot-Vorgang.

![Refresh-1 ](images/up-1.png)
 ![ Refresh-2 ](images/up-2.png)
 ![ Refresh-3](images/up-3.png)

>[!NOTE]
>Wenn Sie Geräte zu Active Directory (Azure AD Hybrid Join) hinzufügen, ist es erforderlich, ein Domänen Beitritt-Geräte Konfigurations Profil zu erstellen, das auf "alle Geräte" ausgerichtet ist (da es kein Azure Active Directory Geräte Objekt für den Computer gibt, auf dem die Gruppenbasierte Ausrichtung erfolgt). Weitere Informationen finden Sie unter der [benutzergesteuerte Modus für Hybrid Azure Active Directory Join](user-driven.md#user-driven-mode-for-hybrid-azure-active-directory-join).

### <a name="register-the-device-for-windows-autopilot"></a>Registrieren des Geräts für Windows Autopilot

Geräte, die mit Autopilot bereitgestellt werden, erhalten beim ersten Start nur die gesteuerte OOBE Autopilot-Funktion. Stellen Sie nach dem Aktualisieren auf Windows 10 sicher, dass Sie das Gerät registrieren, damit das Autopilot-Verhalten beim Zurücksetzen des Computers wieder hergestellt wird. Sie können die automatische Registrierung für eine zugewiesene Gruppe mithilfe der Einstellung **alle Zielgeräte in Autopilot konvertieren** aktivieren. Weitere Informationen finden Sie unter [Erstellen eines Autopilot-Bereitstellungsprofils](enrollment-autopilot.md#create-an-autopilot-deployment-profile).

Siehe auch [Hinzufügen von Geräten zu Windows Autopilot](add-devices.md).

## <a name="speeding-up-the-deployment-process"></a>Beschleunigen des Bereitstellungs Prozesses

Wenn Sie ca. 20 Minuten aus dem Bereitstellungs Prozess entfernen möchten, finden Sie weitere Informationen im Blog von Michael Niehaus mit Anweisungen zum [beschleunigen von Windows Autopilot für vorhandene Geräte](/archive/blogs/mniehaus/speeding-up-windows-autopilot-for-existing-devices).
