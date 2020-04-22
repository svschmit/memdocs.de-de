---
title: Windows Autopilot für vorhandene Geräte
titleSuffix: Configuration Manager
description: Verwenden Sie eine Configuration Manager-Tasksequenz zum Reimaging und die Bereitstellung für ein Windows 7-Gerät für den benutzergesteuerten Windows Autopilot-Modus.
ms.date: 03/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 2e96f847-5b5a-4da9-8e8f-6aa488838508
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e9f2ddf106c641c4433ddd1d09a2457900f670e8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709018"
---
# <a name="windows-autopilot-for-existing-devices"></a>Windows Autopilot für vorhandene Geräte
<!--3607717, fka 1358333-->

*Gilt für: Configuration Manager (Current Branch)*

[Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot) bietet Unternehmen die Möglichkeit, unveränderte, neue Windows 10-Geräte direkt an den Endbenutzer zu liefern und den Bereitstellungsablauf festzulegen, den der Benutzer durchläuft, um ein sicheres, produktives Windows 10-Gerät zu erhalten. Das Gerät ist beim Windows Autopilot-Dienst registriert, sodass Sie das erforderliche Windows Autopilot-Profil zuweisen können. Dieses Profil definiert die den Eindruck beim ersten Ausführen (Out-of-Box-Experience, OOBE)) für dieses Gerät. 

[Windows Autopilot ist für vorhandene Geräte](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) mit Windows 10-Version 1809 oder höher verfügbar. Mit dieser Funktion können Sie ein Reimaging für ein Windows 7-Gerät für den [benutzergesteuerten Windows Autopilot-Modus](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) mit einer einzigen, nativen Configuration Manager-Tasksequenz durchführen und das Gerät bereitstellen. 



## <a name="prerequisites"></a>Voraussetzungen

- Erwerben Sie das Installationsmedium für Windows 10, Version 1809 oder höher. Erstellen Sie dann ein Configuration Manager-Betriebssystemimage. Weitere Informationen finden Sie unter [Verwalten von Betriebssystemimages](../get-started/manage-operating-system-images.md).

- Erstellen Sie in Microsoft Intune Profile für Windows Autopilot. Weitere Informationen finden Sie unter [Registrieren von Windows-Geräten in Intune mit Windows Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot).

- Ein Gerät, das noch nicht für den Windows Autopilot-Dienst registriert ist. Wenn das Gerät bereits registriert ist, hat das zugewiesene Profil Vorrang. Das Profil „Autopilot für bestehende Geräte“ gilt nur, falls das Onlineprofil ausfällt.



## <a name="create-the-configuration-file"></a>Erstellen einer Konfigurationsdatei

1. Öffnen Sie auf einem Windows-Gerät mit Internetverbindung ein administratives PowerShell-Befehlsfenster, und führen Sie die folgenden Befehle aus:  

    1. Installieren Sie die erforderlichen Module, und akzeptieren Sie die Aufforderungen zum Fortfahren.  
        ``` PowerShell  
        Install-Module AzureAD
        Install-Module WindowsAutopilotIntune 
        Import-Module WindowsAutopilotIntune 
        ```

    2. Melden Sie sich mit Administrator-Anmeldeinformationen bei Intune an.  
        ``` PowerShell  
        connect-msgraph 
        ```

    3. Rufen Sie alle Windows Autopilot-Profile ab, die mit Ihren Intune-Mandanten verknüpft sind.  
        ``` PowerShell  
        $AutopilotProfile = Get-AutopilotProfile
        ```

    4. Erstellen Sie eine Konfigurationsdatei für jedes Profil. Die Dateien werden nach dem Anzeigenamen des Profils benannt und auf dem Desktop des aktuellen Benutzers gespeichert.<!--PowerShell example courtesy of GitHub user treestryder from SCCMDocs issue #1196-->  
        ``` PowerShell  
        $AutopilotProfile | ForEach-Object { $_ | ConvertTo-AutoPilotConfigurationJSON | Set-Content -Encoding Ascii "~\Desktop\$($_.displayName).json" }
        ```  

        > [!Note]  
        > Die Konfigurationsdatei kann nur ein Profil enthalten. Jedes Profil muss in geschweifte Klammern `{}` eingeschlossen sein.  

2. Speichern Sie eines der Profile in einer ANSI-codierten Datei namens **AutopilotConfigurationFile.json**. Wählen Sie einen als Configuration Manager-Paketquelle geeigneten Speicherort aus.  

    > [!Tip]  
    > Wenn Sie die JSON-Ausgabe mit dem PowerShell-Cmdlet **Out-File** an eine Datei weiterleiten, wird standardmäßig die Unicode-Codierung verwendet. Dieses Cmdlet kann auch lange Zeilen abschneiden. Verwenden Sie das Cmdlet **Set-Content** mit dem `-Encoding ASCII`-Parameter um die richtige Textcodierung festzulegen.   
    > 
    > Windows-Editor verwendet standardmäßig die ANSI-Codierung.  

3. Erstellen Sie ein Configuration Manager-Paket, das diese Datei enthält. Es ist kein Programm erforderlich. Weitere Informationen finden Sie unter [Erstellen eines Pakets](../../apps/deploy-use/packages-and-programs.md#create-a-package-and-program).  

    > [!NOTE]  
    > Windows setzt den Dateinamen **AutopilotConfigurationFile.json** voraus. Um mehrere Autopilot-Profile zu verwenden, erstellen Sie separate Configuration Manager-Pakete.  



## <a name="create-the-task-sequence"></a>Erstellen einer Tasksequenz

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und wählen Sie anschließend den Knoten **Tasksequenzen** aus. Wählen Sie im Menüband **Tasksequenz erstellen** aus.  

2. Wählen Sie auf der Seite **Neue Tasksequenz erstellen** die Option **Windows Autopilot für vorhandene Geräte bereitstellen** aus.  

3. Geben Sie auf der Seite **Informationen zur Tasksequenz** einen Namen an, fügen Sie optional eine Beschreibung hinzu, und wählen Sie ein Startimage aus. Weitere Informationen zu unterstützten Startimageimageversionen finden Sie unter [Unterstützung für Windows 10](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk).  

4. Wählen Sie auf der Seite **Windows installieren** das Windows 10-**Imagepaket**. Konfigurieren Sie dann die folgenden Einstellungen:  

    - **Imageindex:** Wählen Sie entweder „Enterprise“, „Education“ oder „Professional“ gemäß Anforderungen Ihrer Organisation.  

    - Aktivieren Sie die Option **Zielcomputer vor Installation des Betriebssystems partitionieren und formatieren**.  

    - **Konfigurieren Sie die Tasksequenz zur Verwendung mit BitLocker**: Wenn Sie diese Option aktivieren, beinhaltet die Tasksequenz die notwendigen Schritte, um BitLocker zu aktivieren.  

    - **Product Key:** Wenn Sie einen Product Key für die Windows-Aktivierung angeben müssen, geben Sie ihn hier ein.  

    - Wählen Sie eine der folgenden Optionen, um das lokale Administratorkonto unter Windows 10 zu konfigurieren:  
        - **Lokales Administratorkennwort zufällig erstellen und das Konto auf allen unterstützten Plattformen deaktivieren (empfohlen)**
        - **Konto aktivieren und lokales Administratorkennwort angeben**

5. Wählen Sie auf der Seite **Netzwerk konfigurieren** die Option **Einer Arbeitsgruppe beitreten**. Diese Tasksequenz verwendet das Windows-Systemvorbereitungstool (sysprep). Wenn das Gerät mit einer Domäne verbunden ist, schlägt sysprep fehl.  

6. Fügen Sie auf der Seite **Configuration Manager installieren** alle erforderlichen Installationseigenschaften für Ihre Umgebung hinzu.  

    > [!Tip]  
    > Die Tasksequenz benötigt diese Informationen nur, wenn die Clientkomponenten des Configuration Managers während der Tasksequenz vor der Ausführung von sysprep benötigt werden. Zum Beispiel zum Installieren von Softwareupdates oder Anwendungen. Wenn Sie diese Aktionen nicht durchführen, ist der Client nicht erforderlich. Er wird deinstalliert, bevor die Tasksequenz sysprep ausführt.  

7. Die Seite **Updates einschließen** wählt standardmäßig die Option **Keine Softwareupdates installieren** aus.  

    > [!Tip]  
    > Verwenden Sie die Imageofflinewartung, um das Image mit den neuesten Windows 10-Qualitätsupdates zu aktualisieren. Weitere Informationen finden Sie unter [Anwenden von Softwareupdates auf ein Betriebssystemimage](../get-started/manage-operating-system-images.md#BKMK_OSImagesApplyUpdates).  

8. Auf der Seite **Anwendungen installieren** können Sie Anwendungen auswählen, die während der Tasksequenz installiert werden sollen. Es wird jedoch empfohlen, bei diesem Szenario den Signaturimageansatz darzustellen. Wenden Sie nach der Gerätebereitstellung mit Autopilot alle Anwendungen und Konfigurationen aus der Co-Verwaltung von Microsoft Intune oder Configuration Manager an. Dadurch wird eine einheitliche Umgebung geschaffen – für Benutzer, die neue Geräte erhalten, und Benutzer, die Windows Autopilot für vorhandene Geräte verwenden.  

8. Wählen Sie auf der Seite **Systemvorbereitung** das Paket aus, das die Autopilot-Konfigurationsdatei enthält. Standardmäßig startet die Tasksequenz den Computer neu, nachdem Windows-Sysprep ausgeführt wurde. Sie können auch die Option **Computer nach Abschluss dieser Tasksequenz herunterfahren** auswählen. Damit können Sie ein Gerät vorbereiten und es dann einem Benutzer für eine einheitliche Autopilot-Umgebung zur Verfügung stellen.  

9. Schließen Sie den Assistenten ab.  

Das Bearbeiten der Tasksequenz ähnelt der Standardtasksequenz zum Anwenden eines vorhandenen Betriebssystemimages. Diese Tasksequenz umfasst die folgenden zusätzlichen Schritte:  

- **Windows Autopilot-Konfiguration anwenden**: In diesem Schritt wird die Autopilot-Konfigurationsdatei aus dem angegebenen Paket angewendet. Es ist kein neuer Typ von Schritt, es ist der Schritt **Befehlszeile ausführen**, um die Datei zu kopieren.  

- **Windows für die Erfassung vorbereiten**: Dieser Schritt führt Windows-Sysprep aus und hat die Einstellung **Computer nach dem Ausführen dieser Aktion herunterfahren**. Weitere Informationen finden Sie unter [Windows für die Erfassung vorbereiten](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture).  

Der Windows Autopilot für bestehende Geräte führt dazu, dass ein Gerät mit Azure Active Directory (Azure AD) verbunden wird. 

> [!NOTE]  
> Mit Windows 10, Version 1903 und Version 1909 tritt bei Autopilot ein bekanntes Problem auf, wobei Sysprep die **AutopilotConfigurationFile.json**-Datei löscht. Wenn Sie diese Methode zum Bereitstellen der Windows 10-Version 1903 oder der Version 1909 verwenden, bearbeiten Sie diese Tasksequenz, und nehmen Sie die folgenden Änderungen vor:
>
> 1. Deaktivieren Sie den Schritt **Windows für die Erfassung vorbereiten**.
> 2. Fügen Sie direkt nach dem deaktivierten Schritt **Windows für die Erfassung vorbereiten** einen neuen Schritt **Befehlszeile ausführen** hinzu. Konfigurieren Sie ihn zur Ausführung der folgenden Befehlszeile: `c:\windows\system32\sysprep\sysprep.exe /oobe /reboot`
>
> Weitere Informationen finden Sie unter [Windows Autopilot – bekannte Probleme](https://docs.microsoft.com/windows/deployment/windows-autopilot/known-issues).

Verwenden Sie [Known Folder Move](https://docs.microsoft.com/onedrive/redirect-known-folders) von OneDrive for Business, um sicherzustellen, dass die Daten des Benutzers vor dem Windows 10-Upgrade gesichert werden.



## <a name="next-steps"></a>Nächste Schritte

Nutzen Sie die Co-Verwaltung, um die Verwaltungsfunktionen Ihrer Windows 10-Geräte zu verbessern. Der zweite Pfad zur Co-Verwaltung erfolgt über die moderne Bereitstellung mit Windows Autopilot. Weitere Informationen finden Sie in den folgenden Artikeln:

- [Was ist Co-Verwaltung?](../../comanage/overview.md)
- [Pfade zur Co-Verwaltung](../../comanage/quickstart-paths.md)
- [Windows Autopilot mit Co-Verwaltung](../../comanage/quickstart-autopilot.md)

## <a name="see-also"></a>Weitere Informationen:

- [Registrieren von Windows-Geräten in Intune mithilfe von Windows Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot)
