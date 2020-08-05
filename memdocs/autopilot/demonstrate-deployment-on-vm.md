---
title: Demonstration von Autopilot
ms.reviewer: ''
manager: laurawi
description: Schritt-für-Schritt-Anleitung zum Einrichten eines virtuellen Computers mit einer Windows Autopilot-Bereitstellung
keywords: MDM, Setup, Windows, Windows 10, OOBE, Manage, Bereitstellung, Autopilot, ZTD, Zero-Touchscreen, Partner, msfb, InTune, Upgrade
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.custom: autopilot
ms.openlocfilehash: 7ff25816c0398389fc23bbde4983f4bc9556d192
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/04/2020
ms.locfileid: "87756946"
---
# <a name="demonstrate-autopilot-deployment"></a>Demonstration von Autopilot

**Zielgruppe**

- Windows 10

Für den Einstieg in Windows Autopilot sollten Sie es mit einem virtuellen Computer (VM) ausprobieren, oder Sie können ein physisches Gerät verwenden, das zurückgesetzt wird, und dann eine Neuinstallation von Windows 10 durchführen.

In diesem Thema erfahren Sie, wie Sie eine Windows Autopilot-Bereitstellung für einen virtuellen Computer mithilfe von Hyper-V einrichten.

> [!NOTE]
> Obwohl [mehrere Plattformen](add-devices.md#registering-devices) zur Aktivierung von Autopilot verfügbar sind, verwendet dieses Lab in erster Linie InTune.

> Hyper-V und eine VM sind für dieses Lab nicht erforderlich. Sie können auch ein physisches Gerät verwenden. Bei den Anweisungen wird jedoch davon ausgegangen, dass Sie einen virtuellen Computer verwenden. Wenn Sie ein physisches Gerät verwenden möchten, überspringen Sie die Anweisungen zum Installieren von Hyper-V und Erstellen eines virtuellen Computers. Alle Verweise auf "Device" im Handbuch beziehen sich auf das Client Gerät, entweder physisch oder virtuell.

Das folgende Video enthält eine Übersicht über den Prozess:

</br>
<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/KYVptkpsOqs" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

> Eine Liste der in diesem Handbuch verwendeten Begriffe finden Sie im Abschnitt [Glossar](#glossary) .

## <a name="prerequisites"></a>Voraussetzungen

Dies sind die Dinge, die Sie benötigen, um dieses Lab abzuschließen:
<table><tr><td>Windows 10-Installationsmedien</td><td>Windows 10 Professional oder Enterprise (ISO-Datei) für eine unterstützte Version von Windows 10, halbjährlicher Kanal. Wenn Sie noch nicht über ein ISO-Image verfügen, wird ein Link zum Herunterladen einer <a href="https://www.microsoft.com/evalcenter/evaluate-windows-10-enterprise" data-raw-source="[evaluation version of Windows 10 Enterprise](https://www.microsoft.com/evalcenter/evaluate-windows-10-enterprise)">Evaluierungsversion von Windows 10 Enterprise</a>bereitgestellt.</td></tr>
<tr><td>Zugriff auf das Internet</td><td>Wenn Sie sich hinter einer Firewall befinden, finden Sie weitere Informationen unter den detaillierten <a href="windows-autopilot-requirements.md#networking-requirements" data-raw-source="[networking requirements](windows-autopilot-requirements.md#networking-requirements)">Netzwerk Anforderungen</a>. Stellen Sie andernfalls sicher, dass Sie über eine Verbindung mit dem Internet verfügen.</td></tr>
<tr><td>Hyper-V oder ein physisches Gerät unter Windows 10</td><td>In der Anleitung wird davon ausgegangen, dass Sie einen virtuellen Hyper-v-Computer verwenden und bei Bedarf Anweisungen zum Installieren und Konfigurieren von Hyper-v bereitstellen. Wenn Sie ein physisches Gerät verwenden möchten, überspringen Sie die Schritte zum Installieren und Konfigurieren von Hyper-V.</td></tr>
<tr><td>Ein Premium InTune-Konto</td><td>In diesem Leitfaden wird beschrieben, wie Sie ein Kostenloses 30-Tage-Testversion Premium-Konto erhalten, das zum Abschluss des Labs verwendet werden kann.</td></tr></table>

## <a name="procedures"></a>Prozeduren

Im folgenden finden Sie eine Zusammenfassung der Abschnitte und Prozeduren im Lab. Befolgen Sie jeden Abschnitt in der Reihenfolge, in der er angezeigt wird, und überspringen Sie die Abschnitte, die nicht für Sie gelten. Optionale Prozeduren werden im Anhang bereitgestellt.

[Überprüfen der Unterstützung für Hyper-V](#verify-support-for-hyper-v)
<br>[Aktivieren von Hyper-V](#enable-hyper-v)
<br>[Erstellen einer Demo-VM](#create-a-demo-vm)
<br>&nbsp;&nbsp;&nbsp;[ISO-Datei Speicherort festlegen](#set-iso-file-location)
<br>&nbsp;&nbsp;&nbsp;[Festlegen des Netzwerkadapter namens](#determine-network-adapter-name)
<br>&nbsp;&nbsp;&nbsp;  [Verwenden von Windows PowerShell zum Erstellen der Demo-VM](#use-windows-powershell-to-create-the-demo-vm)
<br>&nbsp;&nbsp;&nbsp;[Installieren von Windows 10](#install-windows-10)
<br>[Erfassen der Hardware-ID](#capture-the-hardware-id)
<br>[Zurücksetzen des virtuellen Computers auf "Out-of-Box-do" (OOBE)](#reset-the-vm-back-to-out-of-box-experience-oobe)
<br>[Abonnement Ebene überprüfen](#verify-subscription-level)
<br>[Konfigurieren des Unternehmensbrandings](#configure-company-branding)
<br>[Konfigurieren Microsoft InTune automatischen Registrierung](#configure-microsoft-intune-auto-enrollment)
<br>[Registrieren Ihrer VM](#register-your-vm)
<br>&nbsp;&nbsp;&nbsp;[Autopilot-Registrierung mit InTune](#autopilot-registration-using-intune)
<br>&nbsp;&nbsp;&nbsp;[Autopilot-Registrierung mit msfb](#autopilot-registration-using-msfb)
<br>[Erstellen und Zuweisen eines Windows Autopilot-Bereitstellungs Profils](#create-and-assign-a-windows-autopilot-deployment-profile)
<br>&nbsp;&nbsp;&nbsp;[Erstellen eines Windows Autopilot-Bereitstellungs Profils mit InTune](#create-a-windows-autopilot-deployment-profile-using-intune)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Profil zuweisen](#assign-the-profile)
<br>&nbsp;&nbsp;&nbsp;[Erstellen eines Windows Autopilot-Bereitstellungs Profils mit msfb](#create-a-windows-autopilot-deployment-profile-using-msfb)
<br>[Siehe Windows Autopilot in Aktion](#see-windows-autopilot-in-action)
<br>[Entfernen von Geräten aus Autopilot](#remove-devices-from-autopilot)
<br>&nbsp;&nbsp;&nbsp;[Löschen eines Autopilot-Geräts (](#delete-deregister-autopilot-device) Aufheben der Registrierung)
<br>[Anhang A: Überprüfen der Unterstützung für Hyper-V](#appendix-a-verify-support-for-hyper-v)
<br>[Anhang B: Hinzufügen von apps zu Ihrem Profil](#appendix-b-adding-apps-to-your-profile)
<br>&nbsp;&nbsp;&nbsp;[Hinzufügen einer Win32-App](#add-a-win32-app)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Vorbereiten der APP für InTune](#prepare-the-app-for-intune)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Erstellen einer APP in InTune](#create-app-in-intune)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Zuweisen der APP zu Ihrem InTune-Profil](#assign-the-app-to-your-intune-profile)
<br>&nbsp;&nbsp;&nbsp;[Hinzufügen von Office 365](#add-office-365)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Erstellen einer APP in InTune](#create-app-in-intune)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Zuweisen der APP zu Ihrem InTune-Profil](#assign-the-app-to-your-intune-profile)
<br>[Glossar](#glossary)

## <a name="verify-support-for-hyper-v"></a>Überprüfen der Unterstützung für Hyper-V

Wenn Sie noch nicht über Hyper-V verfügen, müssen wir dies zunächst auf einem Computer aktivieren, auf dem Windows 10 oder Windows Server (2012 R2 oder höher) ausgeführt wird.

> Wenn Sie Hyper-V bereits aktiviert haben, fahren Sie mit dem Schritt [Erstellen einer Demo-VM](#create-a-demo-vm) fort. Wenn Sie anstelle eines virtuellen Computers ein physisches Gerät verwenden, fahren Sie mit [Installieren von Windows 10](#install-windows-10)fort.

Wenn Sie nicht sicher sind, dass Ihr Gerät Hyper-v unterstützt, oder wenn Sie Probleme bei der Installation von Hyper-v haben, finden Sie in [Anhang A](#appendix-a-verify-support-for-hyper-v) unten Weitere Informationen zum Überprüfen, ob Hyper-v erfolgreich installiert werden kann.

## <a name="enable-hyper-v"></a>Aktivieren von Hyper-V

Öffnen Sie zum Aktivieren von Hyper-V eine Windows PowerShell-Eingabeaufforderung mit erhöhten Rechten, und führen Sie den folgenden Befehl aus:

```powershell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
```

Dieser Befehl funktioniert auf allen Betriebssystemen, die Hyper-v unterstützen, aber unter Windows Server-Betriebssystemen müssen Sie einen zusätzlichen Befehl (unten) eingeben, um das Hyper-v-Windows PowerShell-Modul und die Hyper-v-Manager-Konsole hinzuzufügen. Mit dem folgenden Befehl wird auch Hyper-V installiert, wenn es nicht bereits installiert ist. Wenn Sie also Windows Server verwenden, können Sie einfach den folgenden Befehl eingeben, anstatt den Befehl enable-windowsoptionalfeature zu verwenden:

```powershell
Install-WindowsFeature -Name Hyper-V -IncludeManagementTools
```

Wenn Sie aufgefordert werden, den Computer neu zu starten, wählen Sie **Ja**aus. Der Computer kann mehrmals neu gestartet werden.

> Alternativ dazu können Sie Hyper-V mithilfe der Systemsteuerung in Windows unter Windows-Funktionen ein- **oder ausschalten** für ein Client Betriebssystem oder Server-Manager **Assistenten zum Hinzufügen von Rollen und Features** auf einem Server Betriebssystem installieren, wie unten dargestellt:

   ![Hyper-V-Feature](images/hyper-v-feature.png)

   ![Hyper-V](images/svr_mgr2.png)

<P>Wenn Sie Hyper-V mithilfe von Server-Manager installieren, übernehmen Sie die Standardauswahl. Achten Sie auch darauf, beide Elemente unter <strong>Rollen Verwaltung tools\hyper-v-Verwaltungs Tools</strong>zu installieren.

Öffnen Sie nach Abschluss der Installation den Hyper-v-Manager, indem Sie an einer Eingabeaufforderung mit erhöhten Rechten den Befehl **virtmgmt. msc** eingeben, oder geben Sie im Suchfeld Startmenü den Eintrag **Hyper-v** ein.

Weitere Informationen zu Hyper-v finden Sie unter [Einführung in Hyper-v unter Windows 10](https://docs.microsoft.com/virtualization/hyper-v-on-windows/about/) und [Hyper-v unter Windows Server](https://docs.microsoft.com/windows-server/virtualization/hyper-v/hyper-v-on-windows-server).

## <a name="create-a-demo-vm"></a>Erstellen einer Demo-VM

Da Hyper-V nun aktiviert ist, müssen wir einen virtuellen Computer erstellen, auf dem Windows 10 ausgeführt wird. Wir können [einen](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/create-virtual-machine) virtuellen Computer und ein [virtuelles Netzwerk](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/connect-to-network) mit dem Hyper-V-Manager erstellen, aber es ist einfacher, Windows PowerShell zu verwenden.

Um Windows PowerShell verwenden zu können, müssen wir nur zwei Dinge kennen:

1. Der Speicherort der Windows 10-ISO-Datei.
   - Im Beispiel wird davon ausgegangen, dass der Speicherort " **c:\iso\win10-eval.ISO**" lautet.
2. Der Name der Netzwerkschnittstelle, die eine Verbindung mit dem Internet herstellt.
   - Im Beispiel verwenden wir einen Windows PowerShell-Befehl, um dies automatisch zu bestimmen.

Nachdem wir den Speicherort der ISO-Datei festgelegt und den Namen der entsprechenden Netzwerkschnittstelle festgelegt haben, können wir Windows 10 installieren.

### <a name="set-iso-file-location"></a>ISO-Datei Speicherort festlegen

Sie können eine ISO-Datei für eine Evaluierungsversion der neuesten Version von Windows 10 Enterprise [hier](https://www.microsoft.com/evalcenter/evaluate-windows-10-enterprise)herunterladen.
- Wenn Sie aufgefordert werden, eine Plattform auszuwählen, wählen Sie **64 Bit**aus.

Nachdem Sie diese Datei heruntergeladen haben, ist der Name extrem lang (z.b. 17763.107.101029-1455. rs5_release_svc_refresh_CLIENTENTERPRISEEVAL_OEMRET_x64FRE_en-US. ISO).

1. Benennen Sie die Datei in **win10-eval. ISO**um, damit Sie einfacher einzugeben und zu merken ist.
2. Erstellen Sie auf Ihrem Computer ein Verzeichnis mit dem Namen **c:\ISO** , und verschieben Sie die Datei **win10-eval. ISO** dorthin. der Pfad zur Datei lautet also **c:\iso\win10-eval.ISO**.
3. Wenn Sie für die Datei einen anderen Namen und Speicherort verwenden möchten, müssen Sie die unten aufgeführten Windows PowerShell-Befehle ändern, um Ihren benutzerdefinierten Namen und Ihr Verzeichnis zu verwenden.

### <a name="determine-network-adapter-name"></a>Festlegen des Netzwerkadapter namens

Das Cmdlet "Get-netadaper" wird unten zum automatischen Auffinden des Netzwerkadapters verwendet, bei dem es sich höchstwahrscheinlich um den Netzwerkadapter handelt, mit dem Sie eine Verbindung mit dem Internet herstellen. Sie sollten diesen Befehl zuerst testen, indem Sie an einer Windows PowerShell-Eingabeaufforderung mit erhöhten Rechten Folgendes ausführen:

```powershell
(Get-NetAdapter |?{$_.Status -eq "Up" -and !$_.Virtual}).Name
```

Die Ausgabe dieses Befehls sollte der Name der Netzwerkschnittstelle sein, die Sie zum Herstellen einer Verbindung mit dem Internet verwenden. Vergewissern Sie sich, dass dies der richtige Schnittstellen Name ist. Wenn dies nicht der richtige Schnittstellen Name ist, müssen Sie den ersten Befehl unten bearbeiten, um Ihren Netzwerkschnittstellen Namen zu verwenden.

Wenn der obige Befehl z. b. Ethernet anzeigt, Sie aber Ethernet2 verwenden möchten, lautet der erste folgende Befehl New-VMSwitch-Name autopilotexternal-allowmanagementos $true-netadaptername **Ethernet2**.

### <a name="use-windows-powershell-to-create-the-demo-vm"></a>Verwenden von Windows PowerShell zum Erstellen der Demo-VM

Alle VM-Daten werden unter dem aktuellen Pfad in der PowerShell-Eingabeaufforderung erstellt. Sie sollten vor dem Ausführen der folgenden Befehle in einen neuen Ordner navigieren.

> [!IMPORTANT]
> **VM-Switch**: ein VM-Switch gibt an, wie Hyper-V VMS mit einem Netzwerk verbindet. <br><br>Wenn Sie Hyper-V bereits aktiviert haben und Ihre Netzwerkschnittstelle mit Internet Verbindung bereits an einen VM-Switch gebunden ist, können die folgenden PowerShell-Befehle nicht ausgeführt werden. In diesem Fall können Sie entweder den vorhandenen VM-Switch löschen (damit die folgenden Befehle erstellen können). Alternativ können Sie diesen VM-Switch auch wieder verwenden, indem Sie den ersten Befehl unten überspringen und den zweiten Befehl ändern, um den Switchnamen " **autopilotexternal** " durch den Namen Ihres Schalters zu ersetzen<br><br>Wenn Sie noch nie einen externen VM-Switch erstellt haben, führen Sie einfach die folgenden Befehle aus.

```powershell
New-VMSwitch -Name AutopilotExternal -AllowManagementOS $true -NetAdapterName (Get-NetAdapter |?{$_.Status -eq "Up" -and !$_.Virtual}).Name
New-VM -Name WindowsAutopilot -MemoryStartupBytes 2GB -BootDevice VHD -NewVHDPath .\VMs\WindowsAutopilot.vhdx -Path .\VMData -NewVHDSizeBytes 80GB -Generation 2 -Switch AutopilotExternal
Add-VMDvdDrive -Path c:\iso\win10-eval.iso -VMName WindowsAutopilot
Start-VM -VMName WindowsAutopilot
```

Nachdem Sie diese Befehle eingegeben haben, stellen Sie eine Verbindung mit dem virtuellen Computer her, den Sie soeben erstellt haben, und warten Sie, bis eine Eingabeaufforderung zum Drücken einer Taste und zum Starten  Sie können eine Verbindung mit dem virtuellen Computer herstellen, indem Sie im Hyper-V-Manager auf die VM doppelklicken.

Sehen Sie sich die Beispielausgabe unten an. In diesem Beispiel wird der virtuelle Computer unter dem Verzeichnis " **c:\autopilot** " erstellt, und der vmconnect.exe-Befehl wird verwendet (dieser ist nur unter Windows Server verfügbar). Wenn Sie Hyper-v unter Windows 10 installiert haben, stellen Sie mit dem Hyper-v-Manager eine Verbindung mit dem virtuellen Computer her.

<pre style="overflow-y: visible">
PS C:\autopilot&gt; dir c:\iso


    Directory: C:\iso


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/12/2019   2:46 PM     4627343360 win10-eval.iso

PS C:\autopilot&gt; (Get-NetAdapter |?{$<em>.Status -eq &quot;Up&quot; -and !$</em>.Virtual}).Name
Ethernet
PS C:\autopilot&gt; New-VMSwitch -Name AutopilotExternal -AllowManagementOS $true -NetAdapterName (Get-NetAdapter |?{$<em>.Status -eq &quot;Up&quot; -and !$</em>.Virtual}).Name

Name              SwitchType NetAdapterInterfaceDescription
----              ---------- ------------------------------
AutopilotExternal External   Intel(R) Ethernet Connection (2) I218-LM

PS C:\autopilot&gt; New-VM -Name WindowsAutopilot -MemoryStartupBytes 2GB -BootDevice VHD -NewVHDPath .\VMs\WindowsAutopilot.vhdx -Path .\VMData -NewVHDSizeBytes 80GB -Generation 2 -Switch AutopilotExternal

Name             State CPUUsage(%) MemoryAssigned(M) Uptime   Status             Version
----             ----- ----------- ----------------- ------   ------             -------
WindowsAutopilot Off   0           0                 00:00:00 Operating normally 8.0

PS C:\autopilot&gt; Add-VMDvdDrive -Path c:\iso\win10-eval.iso -VMName WindowsAutopilot
PS C:\autopilot&gt; Start-VM -VMName WindowsAutopilot
PS C:\autopilot&gt; vmconnect.exe localhost WindowsAutopilot
PS C:\autopilot&gt; dir

    Directory: C:\autopilot

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----        3/12/2019   3:15 PM                VMData
d-----        3/12/2019   3:42 PM                VMs

PS C:\autopilot&gt;
</pre>

### <a name="install-windows-10"></a>Installieren von Windows 10

Stellen Sie sicher, dass der virtuelle Computer aus der Installations-ISO gestartet wurde, klicken Sie auf **weiter** , und klicken Sie dann auf **jetzt installieren** . Hierzu folgende Beispiele:

   ![Windows Setup ](images/winsetup1.png) Windows Setup Windows Setup Windows Setup Windows ![ ](images/winsetup2.png) ![ ](images/winsetup3.png) ![ Setup ](images/winsetup4.png) ![ ](images/winsetup5.png) ![ Windows Setup](images/winsetup6.png)

Nachdem der virtuelle Computer neu gestartet wurde, können Sie bei der Erstellung des virtuellen Computers die Option **für den persönlichen Gebrauch** oder den **Domänen Beitritt** einrichten und dann auf dem **Anmelde** Bildschirm ein Offline Konto auswählen.  Dies bietet die schnellste Möglichkeit zum Desktop. Beispiel:

   ![Windows-Setup](images/winsetup7.png)

Melden Sie sich nach Abschluss der Installation an, und vergewissern Sie sich, dass Sie sich auf dem Windows 10-Desktop befinden, und erstellen Sie dann Ihren ersten Hyper-V-Prüfpunkt. Prüfpunkte werden verwendet, um den virtuellen Computer in einem früheren Zustand wiederherzustellen. In diesem Lab erstellen Sie mehrere Prüfpunkte, die später verwendet werden können, um den Prozess zu durchlaufen.

   ![Windows-Setup](images/winsetup8.png)

Um ihren ersten Prüfpunkt zu erstellen, öffnen Sie eine Windows PowerShell-Eingabeaufforderung mit erhöhten Rechten auf dem Computer, auf dem Hyper-V ausgeführt wird (nicht auf dem virtuellen Computer)

```powershell
Checkpoint-VM -Name WindowsAutopilot -SnapshotName "Finished Windows install"
```

Klicken Sie im Hyper-V-Manager auf den virtuellen Computer **windowsautopilot** , und vergewissern Sie sich, dass die **fertige Windows-Installation** im Bereich Prüfpunkte aufgeführt ist.

## <a name="capture-the-hardware-id"></a>Erfassen der Hardware-ID

> [!NOTE]
> Normalerweise wird die Geräte-ID vom OEM aufgezeichnet, während Sie das OA3-Tool auf jedem Gerät in der Factory ausführen.  Der OEM sendet dann die vom OA3-Tool erstellte 4K HH an Microsoft, indem er ihn mit einem computerbuildbericht (CBR) übermittelt.  Für die Zwecke dieses Labs fungieren Sie als OEM (Erfassen der 4K HH), aber Sie werden nicht das OA3-Tool verwenden, um die vollständige 4K HH aus verschiedenen Gründen zu erfassen. (Sie müssen das OA3-Tool installieren, Ihr Gerät kann nicht über eine Volumenlizenz Version von Windows verfügen. es ist komplizierter als die Verwendung eines PS-Skripts usw.).  Stattdessen simulieren Sie das Ausführen des OA3-Tools, indem Sie ein PowerShell-Skript ausführen, das das Gerät 4K HH genau wie das OA3-Tool erfasst.

Führen Sie die folgenden Schritte aus, um das PS-Skript auszuführen:

1. Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, und führen Sie die folgenden Befehle aus. Diese Befehle sind identisch, unabhängig davon, ob Sie eine VM oder ein physisches Gerät verwenden:

    ```powershell
    md c:\HWID
    Set-Location c:\HWID
    Set-ExecutionPolicy -Scope Process -ExecutionPolicy Unrestricted -Force
    Install-Script -Name Get-WindowsAutopilotInfo -Force
    $env:Path += ";C:\Program Files\WindowsPowerShell\Scripts"
    Get-WindowsAutopilotInfo.ps1 -OutputFile AutopilotHWID.csv
    ```

Wenn Sie aufgefordert werden, das nuget-Paket zu installieren, wählen Sie **Ja**aus.

Sehen Sie sich die Beispielausgabe unten an.

<pre>
PS C:\> md c:\HWID

    Directory: C:\

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----        3/14/2019  11:33 AM                HWID

PS C:\> Set-Location c:\HWID
PS C:\HWID> Set-ExecutionPolicy -Scope Process -ExecutionPolicy Unrestricted -Force
PS C:\HWID> Install-Script -Name Get-WindowsAutopilotInfo -Force

NuGet provider is required to continue
PowerShellGet requires NuGet provider version '2.8.5.201' or newer to interact with NuGet-based repositories. The NuGet
 provider must be available in 'C:\Program Files\PackageManagement\ProviderAssemblies' or
'C:\Users\user1\AppData\Local\PackageManagement\ProviderAssemblies'. You can also install the NuGet provider by running
 'Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force'. Do you want PowerShellGet to install and
import the NuGet provider now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y
PS C:\HWID> $env:Path += ";C:\Program Files\WindowsPowerShell\Scripts"
PS C:\HWID> Get-WindowsAutopilotInfo.ps1 -OutputFile AutopilotHWID.csv
PS C:\HWID> dir

    Directory: C:\HWID

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/14/2019  11:33 AM           8184 AutopilotHWID.csv

PS C:\HWID>
</pre>

Vergewissern Sie sich, dass im Verzeichnis " **c:\hwid** " eine **AutopilotHWID.csv** -Datei mit einer Größe von ungefähr 8 KB vorhanden ist.  Diese Datei enthält die gesamte 4K hh.

> [!NOTE]
> Obwohl die CSV-Erweiterung möglicherweise Microsoft Excel zugeordnet ist, können Sie die Datei nicht ordnungsgemäß anzeigen, indem Sie darauf doppelklicken. Zum ordnungsgemäßen analysieren der Komma Trennzeichen und zum Anzeigen der Datei in Excel müssen Sie die **Daten**  >  **aus der Text/CSV-** Funktion in Excel verwenden, um die entsprechenden Datenspalten zu importieren. Sie müssen die Datei nicht in Excel anzeigen, es sei denn, Sie sind neugierig. Das Dateiformat wird überprüft, wenn es in Autopilot importiert wird. Ein Beispiel für die Daten in dieser Datei finden Sie unten.

![Seriennummer und Hardware Hash](images/hwid.png)

Sie müssen diese Daten in InTune hochladen, um Ihr Gerät für Autopilot zu registrieren, sodass es auf den Computer übertragen werden muss, den Sie für den Zugriff auf die Azure-Portal verwenden.  Wenn Sie anstelle eines virtuellen Computers ein physisches Gerät verwenden, können Sie die Datei auf einen USB-Stick kopieren.  Wenn Sie einen virtuellen Computer verwenden, können Sie mit der rechten Maustaste auf die AutopilotHWID.csv Datei klicken und Sie kopieren. Klicken Sie dann mit der rechten Maustaste darauf, und fügen Sie die Datei auf Ihrem Desktop (außerhalb der VM) ein.

Wenn Sie Probleme beim Kopieren und Einfügen der Datei haben, zeigen Sie einfach den Inhalt in Editor auf dem virtuellen Computer an, und kopieren Sie den Text außerhalb des virtuellen Computers in den Editor. Verwenden Sie hierfür keinen anderen Text-Editor.

> [!NOTE]
> Vermeiden Sie beim Kopieren und Einfügen in oder von virtuellen Computern das Klicken auf andere Dinge mit dem Mauszeiger zwischen dem Kopier-und dem Einfügevorgang, da die Zwischenablage leer ist oder überschrieben werden kann, sodass Sie beginnen müssen. Wechseln Sie direkt von kopieren zum Einfügen.

## <a name="reset-the-vm-back-to-out-of-box-experience-oobe"></a>Zurücksetzen des virtuellen Computers auf "Out-of-Box-do" (OOBE)

Bereiten Sie die Hardware-ID, die in einer Datei aufgezeichnet wurde, auf den virtuellen Computer für die Windows Autopilot-Bereitstellung vor, indem Sie Sie auf OOBE zurücksetzen

Wechseln Sie auf dem virtuellen Computer zu **Einstellungen > aktualisieren Sie & Sicherheit > Wiederherstellung** , und klicken Sie unter **Zurücksetzen des Computers**auf " **starten** ".
Wählen Sie **alles entfernen** aus, und **Entfernen Sie einfach meine Dateien**. Klicken Sie abschließend auf **Zurücksetzen**.

![Letzte Aufforderung zum Zurücksetzen des PCs](images/autopilot-reset-prompt.jpg)

Das Zurücksetzen der VM oder des Geräts kann einige Zeit in Anspruch nehmen. Fahren Sie mit dem nächsten Schritt fort (überprüfen Sie die Abonnement Ebene) während des Zurücksetzungs Vorgangs.

![Diese PC-Bildschirmaufnahme zurücksetzen](images/autopilot-reset-progress.jpg)

## <a name="verify-subscription-level"></a>Abonnement Ebene überprüfen

Für dieses Lab benötigen Sie ein Aad Premium-Abonnement.  Sie können festzustellen, ob Sie über ein Premium-Abonnement verfügen, indem Sie zum Blatt für die [Konfiguration der MDM](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Mobility) -Registrierung navigieren. Sehen Sie sich folgendes Beispiel an:

**Azure Active Directory**  >  **Mobilität (MDM und MAM)**  >  **Microsoft InTune**

![MDM und InTune](images/mdm-intune2.png)

Wenn das oben gezeigte Konfigurations Blatt nicht angezeigt wird, ist es wahrscheinlich, dass Sie kein **Premium** -Abonnement besitzen.  Die automatische Registrierung ist ein Feature, das nur in Aad Premium verfügbar ist.

Wenn Sie Ihr InTune-Test Konto in ein kostenloses Premium-Testkonto konvertieren möchten, navigieren Sie zu **Azure Active Directory**  >  **Lizenzen**  >  **Alle Produkte**  >  **try/Buy** , und wählen Sie die **Kostenlose Testversion** für Azure AD Premium oder EMS E5.

![Letzte Aufforderung zum Zurücksetzen des PCs](images/aad-lic1.png)

## <a name="configure-company-branding"></a>Konfigurieren des Unternehmensbrandings

Wenn Sie das Unternehmens Branding bereits in Azure Active Directory konfiguriert haben, können Sie diesen Schritt überspringen.

> [!IMPORTANT]
> Stellen Sie sicher, dass Sie sich mit einem globalen Administrator Konto anmelden.

Navigieren Sie [in Azure Active Directory zu Unternehmens Branding](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/LoginTenantBranding), und klicken Sie auf **Konfigurieren** und konfigurieren Sie einen beliebigen unternehmensbrandingtyp, der während des OOBE angezeigt werden soll.

![Konfigurieren des Unternehmensbrandings](images/branding.png)

Wenn Sie fertig sind, klicken Sie auf **Speichern**.

> [!NOTE]
> Die Anwendung von Änderungen am Unternehmens Branding kann bis zu 30 Minuten dauern.

## <a name="configure-microsoft-intune-auto-enrollment"></a>Konfigurieren Microsoft InTune automatischen Registrierung

Wenn die automatische MDM-Registrierung bereits in Azure Active Directory konfiguriert ist, können Sie diesen Schritt überspringen.

Öffnen Sie [Mobility (MDM und MAM) in Azure Active Directory](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Mobility) , und wählen Sie **Microsoft InTune**aus. Wenn Microsoft InTune nicht angezeigt wird, klicken Sie auf **Anwendung hinzufügen** , und wählen Sie **InTune**aus.

Wählen Sie im Rahmen dieser Demo unter dem **MDM-Benutzerbereich** **alle** aus, und klicken Sie auf **Speichern**.

![MDM-Benutzerbereich auf dem Blatt "Mobilität"](images/autopilot-aad-mdm.png)

## <a name="register-your-vm"></a>Registrieren Ihrer VM

Ihre VM (oder Ihr Gerät) kann entweder über InTune oder Microsoft Store for Business (msfb) registriert werden.  Beide Prozesse werden hier angezeigt, <u>wählen aber nur eine</u> für die Zwecke dieses Labs aus. Es wird dringend empfohlen, InTune anstelle von msfb zu verwenden.

### <a name="autopilot-registration-using-intune"></a>Autopilot-Registrierung mit InTune

1. Wählen Sie in InTune im Azure-Portal die **Option Geräteregistrierung**  >  **Windows**-Registrierung  >  **Geräte**  >  **importieren**aus.

    ![InTune-Geräte Import](images/device-import.png)

    > [!NOTE]
    > Wenn Menü Elemente wie die **Windows** -Registrierung für Sie nicht aktiviert sind, sehen Sie sich das Blatt "ganz rechts" in der Benutzeroberfläche an.  Möglicherweise müssen Sie InTune-Konfigurations Berechtigungen in einem ausgestellte Anforderungs Fenster bereitstellen.

2. Navigieren Sie unter **Windows Autopilot-Geräte hinzufügen** ganz rechts zu der **AutopilotHWID.csv** Datei, die Sie zuvor auf den lokalen Computer kopiert haben.  Die Datei sollte die Seriennummer und 4K HH Ihres virtuellen Computers (oder Geräts) enthalten.  Es ist in Ordnung, wenn andere Felder (Windows-Produkt-ID) leer gelassen werden.

    ![HWID-CSV](images/hwid-csv.png)

    Sie sollten bestätigen, dass die Datei vor dem Hochladen korrekt formatiert ist, wie oben gezeigt.

3. Klicken Sie auf **importieren** und warten Sie, bis der Import Vorgang abgeschlossen ist. Der Vorgang kann bis zu 15 Minuten dauern.

4. Klicken Sie auf **Synchronisieren** , um das soeben registrierte Gerät zu synchronisieren. Warten Sie einige Minuten, bevor Sie aktualisieren, um sicherzustellen, dass Ihre VM oder Ihr Gerät hinzugefügt wurde. Siehe folgendes Beispiel.

   ![Importieren von HWID](images/import-vm.png)

### <a name="autopilot-registration-using-msfb"></a>Autopilot-Registrierung mit msfb

> [!IMPORTANT]
> Wenn Sie Ihren virtuellen Computer (oder Ihr Gerät) bereits mit InTune registriert haben, überspringen Sie diesen Schritt.

Optional: eine Übersicht über den Prozess finden Sie im folgenden Video.

&nbsp;

> [!video https://www.youtube.com/embed/IpLIZU_j7Z0]

Zunächst benötigen Sie ein msfb-Konto.  Sie können das gleiche verwenden, das Sie oben für InTune erstellt haben, oder [diese Anweisungen](https://docs.microsoft.com/microsoft-store/windows-store-for-business-overview) befolgen, um ein neues zu erstellen.

Melden Sie sich als nächstes mit Ihrem Testkonto bei [Microsoft Store für Unternehmen](https://businessstore.microsoft.com/en-us/store) an, indem Sie oben rechts auf der Hauptseite auf " **Anmelden** " klicken.

Wählen Sie im oberen Menü die Option **Verwalten** aus, und klicken Sie dann auf der Karte **Geräte** auf den Link **Windows Autopilot Deployment Program** . Sehen Sie sich folgendes Beispiel an:

![Microsoft Store für Unternehmen](images/msfb.png)

Klicken Sie zum Hochladen der CSV-Datei auf den Link **Geräte hinzufügen** . Eine Meldung wird angezeigt, die anzeigt, dass Ihre Anforderung verarbeitet wird. Warten Sie einige Minuten, bevor Sie aktualisieren, um anzuzeigen, dass Ihr neues Gerät hinzugefügt wurde.

![Geräte](images/msfb-device.png)

## <a name="create-and-assign-a-windows-autopilot-deployment-profile"></a>Erstellen und Zuweisen eines Windows Autopilot-Bereitstellungs Profils

> [!IMPORTANT]
> Autopilot-Profile können erstellt und ihrem registrierten virtuellen Computer bzw. Gerät entweder über InTune oder msfb zugewiesen werden.  Beide Prozesse werden hier angezeigt, wählen aber nur <U>eine für die Zwecke dieses Labs aus</U>:

Wählen Sie eine aus:
- [Erstellen von Profilen mithilfe von InTune](#create-a-windows-autopilot-deployment-profile-using-intune)
- [Erstellen von Profilen mit msfb](#create-a-windows-autopilot-deployment-profile-using-msfb)

### <a name="create-a-windows-autopilot-deployment-profile-using-intune"></a>Erstellen eines Windows Autopilot-Bereitstellungs Profils mit InTune

> [!NOTE]
> Auch wenn Sie Ihr Gerät in msfb registriert haben, wird es weiterhin in InTune angezeigt, aber Sie müssen möglicherweise zuerst die Geräteliste **Synchronisieren** und **Aktualisieren** :

![Geräte](images/intune-devices.png)

> Im obigen Beispiel werden sowohl ein physisches Gerät als auch ein virtueller Computer aufgeführt. Ihre Liste sollte nur eine der folgenden einschließen.

Um ein Windows Autopilot-Profil zu erstellen, wählen Sie **Geräte**Registrierung Windows-Registrierung  >  **Windows enrollment**  >  **Bereitstellungs profile** aus.

![Bereitstellungsprofile](images/deployment-profiles.png)

Klicken Sie auf **Profil erstellen**.

![Bereitstellungs Profil erstellen](images/create-profile.png)

Verwenden Sie auf dem Blatt **Profil erstellen** die folgenden Werte:

| Einstellung | Wert |
|---|---|
| Name | Autopilot-Lab-Profil |
| BESCHREIBUNG | leer |
| Alle Zielgeräte in Autopilot konvertieren | Nein |
| Bereitstellungsmodus | Benutzer gesteuert |
| Mit Azure AD verknüpfen als | In Azure AD eingebunden |

Klicken Sie auf " **out-of-Box-Umgebung" (OOBE),** und konfigurieren Sie die folgenden Einstellungen:

| Einstellung | Wert |
|---|---|
| ENDBENUTZER-LIZENZVERTRAG | Hide (Ausblenden) |
| Datenschutzeinstellungen | Hide (Ausblenden) |
| Optionen zum Ändern des Kontos ausblenden | Hide (Ausblenden) |
| Benutzer Kontotyp | Standard |
| Gerätenamen Vorlage anwenden | Nein |

Sehen Sie sich folgendes Beispiel an:

![Bereitstellungsprofil](images/profile.png)

Klicken Sie auf **OK** , und klicken Sie dann auf **Erstellen**.

> Wenn Sie Ihrem Profil über InTune eine APP hinzufügen möchten, finden Sie die entsprechenden optionalen Schritte in [Anhang B: Hinzufügen von apps zu Ihrem Profil](#appendix-b-adding-apps-to-your-profile).

#### <a name="assign-the-profile"></a>Zuweisen des Profils

Profile können nur Gruppen zugewiesen werden. Daher müssen Sie zuerst eine Gruppe erstellen, die die Geräte enthält, auf die das Profil angewendet werden soll. Dieses Handbuch bietet einfache Anweisungen zum Zuweisen eines Profils. ausführlichere Anweisungen finden Sie unter [Erstellen einer Autopilot-Gerätegruppe](https://docs.microsoft.com/intune/enrollment-autopilot#create-an-autopilot-device-group) und [Zuweisen eines Autopilot-Bereitstellungs Profils zu einer Gerätegruppe](https://docs.microsoft.com/intune/enrollment-autopilot#assign-an-autopilot-deployment-profile-to-a-device-group)als optionales lesen.

Um eine Gruppe zu erstellen, öffnen Sie die Azure-Portal, und wählen Sie **Azure Active Directory**  >  **Gruppen**  >  **alle Gruppen**aus:

![Alle Gruppen](images/all-groups.png)

Wählen Sie auf dem Blatt Gruppen die Option neue Gruppe, um die Benutzeroberfläche neue Gruppen zu öffnen.  Wählen Sie den Gruppentyp "Sicherheit" aus, benennen Sie die Gruppe, und wählen Sie den mitgliedschaftentyp "zugewiesen" aus:

Erweitern Sie vor dem Klicken auf **Erstellen**den Bereich **Mitglieder** , klicken Sie auf die Seriennummer Ihres Geräts (wird dann unter **ausgewählte Mitglieder**angezeigt), und klicken Sie dann auf **auswählen** , um dieses Gerät dieser Gruppe hinzuzufügen.

![Neue Gruppe](images/new-group.png)

Klicken Sie jetzt auf **Erstellen** , um die Erstellung der neuen Gruppe abzuschließen.

Klicken Sie auf **alle Gruppen** , und klicken Sie auf **Aktualisieren** , um zu überprüfen, ob die neue Gruppe erfolgreich erstellt wurde.

Wenn eine Gruppe mit Ihrem Gerät erstellt wurde, können Sie nun zurückgehen und Ihr Profil dieser Gruppe zuweisen. Navigieren Sie zurück zur Seite InTune in der Azure-Portal (eine Möglichkeit besteht darin, **InTune** in der oberen Banner Suchleiste einzugeben und **InTune** aus den Ergebnissen auszuwählen).

Wählen Sie in InTune die Option **Geräte**Registrierung Windows-Registrierung  >  **Windows enrollment**  >  **Bereitstellungs profile** aus, um das Profil Blatt zu öffnen.  Klicken Sie auf den Namen des Profils, das Sie zuvor erstellt haben (Autopilot Lab profile), um das Blatt "Details" für dieses Profil zu öffnen:

![Lab-Profil](images/deployment-profiles2.png)

Klicken Sie unter **Verwalten**auf **Zuweisungen**, und erweitern Sie dann auf der Registerkarte **einschließen** das Blatt **Gruppen auswählen** , und klicken Sie auf **AP Lab Group 1** (die Gruppe wird unter **ausgewählte Mitglieder**angezeigt).

![Gruppe einschließen](images/include-group.png)

Klicken Sie auf **Auswählen**, und klicken Sie dann auf **Speichern**.

![Gruppe einschließen](images/include-group2.png)

Es ist auch möglich, bestimmte Benutzer einem Profil zuzuweisen, aber dieses Szenario wird im Lab nicht behandelt. Ausführlichere Informationen finden Sie unter [Registrieren von Windows-Geräten in InTune mithilfe von Windows Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot).

### <a name="create-a-windows-autopilot-deployment-profile-using-msfb"></a>Erstellen eines Windows Autopilot-Bereitstellungs Profils mit msfb

Wenn Sie bereits ein Profil mithilfe der oben beschriebenen Schritte über InTune erstellt und zugewiesen haben, überspringen Sie diesen Abschnitt.

Es ist ein [Video](https://www.youtube.com/watch?v=IpLIZU_j7Z0) verfügbar, das die erforderlichen Schritte zum Erstellen und Zuweisen von Profilen in msfb umfasst. Diese Schritte sind ebenfalls unten zusammengefasst.

Melden Sie sich zunächst mit dem InTune-Konto, das Sie ursprünglich für dieses Lab erstellt haben, bei der [Microsoft Store für Unternehmen](https://businessstore.microsoft.com/manage/dashboard) an.

Klicken Sie im oberen Menü auf **Verwalten** , und klicken Sie dann in der linken Navigationsstruktur auf **Geräte** .

![Msfb-Verwaltung](images/msfb-manage.png)

Klicken Sie in der Kachel **Geräte** auf den Link **Windows Autopilot Deployment Program** .

So erstellen Sie das Profil:

Wählen Sie Ihr Gerät in der **Geräte** Liste aus:

![Msfb-Erstellung](images/msfb-create1.png)

Wählen Sie im Dropdown Menü Autopilot-Bereitstellung die Option **Neues Profil erstellen**aus:

![Msfb-Erstellung](images/msfb-create2.png)

Benennen Sie das Profil, wählen Sie die gewünschten Einstellungen aus, und klicken Sie dann auf **Erstellen**:

![Msfb-Erstellung](images/msfb-create3.png)

Das neue Profil wird der Autopilot-Bereitstellungs Liste hinzugefügt.

So weisen Sie das Profil zu:

Aktivieren Sie das Kontrollkästchen neben dem Gerät, das Sie für dieses Lab registriert haben, und wählen Sie dann im Dropdown Menü **Autopilot Deployment** das Profil aus, das Sie zuweisen möchten, wie im folgenden gezeigt:

![Msfb-Zuweisung](images/msfb-assign1.png)

Vergewissern Sie sich, dass das Profil erfolgreich dem vorgesehenen Gerät zugewiesen wurde, indem Sie den Inhalt der **Profil** Spalte überprüfen:

![Msfb-Zuweisung](images/msfb-assign2.png)

> [!IMPORTANT]
> Das neue Profil wird nur angewendet, wenn das Gerät nicht gestartet wurde und durch OOBE gegangen ist. Einstellungen aus einem anderen Profil können nicht angewendet werden, wenn ein anderes Profil angewendet wurde. Windows muss auf dem Gerät erneut installiert werden, damit das zweite Profil auf das Gerät angewendet werden muss.

## <a name="see-windows-autopilot-in-action"></a>Siehe Windows Autopilot in Aktion

Wenn Sie den virtuellen Computer nach der letzten zurück Setzung Herunterfahren, ist es an der Zeit, ihn erneut zu starten, sodass er die **Autopilot-** OOBE-Darstellung durchlaufen kann. versuchen Sie jedoch nicht, das Gerät erneut zu starten, bis der **Profil Status** für **Not assigned** Ihr Gerät in InTune geändert wurde und schließlich **zugewiesen**wurde:

![Gerätestatus](images/device-status.png)

Stellen Sie außerdem sicher, dass Sie mindestens 30 Minuten ab dem Zeitpunkt der [Konfiguration des Unternehmens Brandings](#configure-company-branding)warten. andernfalls werden diese Änderungen möglicherweise nicht angezeigt.

> [!TIP]
> Wenn Sie Ihr Gerät zuvor nach der Erfassung der Informationen zu 4K HH zurückgesetzt haben und es dann wieder auf den ersten OOBE-Bildschirm zurücksetzen möchten, müssen Sie das Gerät möglicherweise erneut starten, um sicherzustellen, dass das Gerät als Autopilot-Gerät erkannt wird, und zeigt die von Ihnen erwartete Autopilot OOBE-Darstellung an.  Wenn die Autopilot OOBE-Umgebung nicht angezeigt wird, setzen Sie das Gerät erneut zurück (Einstellungen > aktualisieren Sie & Sicherheit > Wiederherstellung, und klicken Sie auf "starten".  Wählen Sie unter diesen PC zurücksetzen die Option Alles entfernen aus, und entfernen Sie einfach meine Dateien. Klicken Sie auf Zurücksetzen).

- Stellen Sie sicher, dass Ihr Gerät eine Internetverbindung aufweist.
- Einschalten des Geräts
- Überprüfen Sie, ob die entsprechenden OOBE-Bildschirme (mit dem entsprechenden Unternehmens Branding) angezeigt werden.  Der Bildschirm Regions Auswahl, der Bildschirm Tastaturauswahl und der zweite Tastaturauswahl-Bildschirm, den Sie überspringen können, werden angezeigt.

![OOBE-Anmeldeseite](images/autopilot-oobe.jpg)

Kurz nach dem Erreichen des Desktops sollte das Gerät in InTune als **aktiviertes** Autopilot-Gerät angezeigt werden.  Wechseln Sie in den InTune-Azure-Portal, wählen Sie **Geräte > alle Geräte**aus, und **Aktualisieren** Sie die Daten, um zu überprüfen, ob sich das Gerät von deaktiviert in aktiviert geändert hat und der Name des Geräts aktualisiert wurde.

![Gerät aktiviert](images/enabled-device.png)

Nachdem Sie eine Sprache und ein Tastaturlayout ausgewählt haben, sollte Ihr Unternehmens Branding-Anmeldebildschirm angezeigt werden. Geben Sie Ihre Azure Active Directory Anmelde Informationen an, und Sie sind fertig.

Windows Autopilot übernimmt jetzt das automatische Hinzufügen Ihres Geräts in Azure Active Directory und die Registrierung für Microsoft InTune. Verwenden Sie die Prüfpunkte, die Sie erstellt haben, um diesen Vorgang mit unterschiedlichen Einstellungen erneut durchzugehen.

## <a name="remove-devices-from-autopilot"></a>Entfernen von Geräten aus Autopilot

Wenn Sie das Gerät (oder den virtuellen Computer) nach Abschluss dieses Labs für andere Zwecke verwenden möchten, müssen Sie es entweder über InTune oder msfb aus Autopilot entfernen und dann zurücksetzen.  Anweisungen zum Aufheben der Registrierung von Geräten finden Sie [hier](https://docs.microsoft.com/intune/enrollment-autopilot#create-an-autopilot-device-group) und [hier](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal) .

### <a name="delete-deregister-autopilot-device"></a>Löschen eines Autopilot-Geräts (Aufheben der Registrierung)

Sie müssen das Gerät von InTune löschen (oder außer Kraft setzen oder zurücksetzen), bevor Sie das Gerät von Autopilot aufheben. Wenn Sie das Gerät aus InTune löschen möchten (nicht Azure Active Directory), melden Sie sich bei Ihrem InTune-Azure-Portal an, und navigieren Sie dann zu **InTune > Geräte > alle Geräte**.  Aktivieren Sie das Kontrollkästchen neben dem Gerät, das Sie löschen möchten, und klicken Sie dann im oberen Menü auf die Schaltfläche Löschen.

![Löschen des Geräts](images/delete-device1.png)

Klicken Sie auf **X** , wenn die Ausführung des Vorgangs angefordert wird:

![Löschen des Geräts](images/delete-device2.png)

Dadurch wird das Gerät aus der InTune-Verwaltung entfernt, und es wird nicht mehr von **InTune > Geräten > allen Geräten**entfernt. Das Gerät wird jedoch noch nicht von Autopilot registriert, sodass das Gerät weiterhin unter **InTune > Geräteregistrierung > Windows-Registrierung > Windows Autopilot-Bereitstellungs Programm > Geräte**angezeigt wird.

![Löschen des Geräts](images/delete-device3.png)

Die **InTune-> Geräte > Liste alle Geräte** und die **InTune-> Geräteregistrierung > Windows-Registrierung > Windows Autopilot-Bereitstellungs Programm > Geräte** Liste bedeuten verschiedene Dinge, die zwei vollständig getrennte Datenspeicher sind.  Der erste (alle Geräte) ist die Liste der Geräte, die derzeit bei InTune registriert sind.

> [!NOTE]
> Ein Gerät wird nur dann in der Liste alle Geräte angezeigt, nachdem es gestartet wurde.  Letzteres (Windows Autopilot Deployment Program > Devices) ist die Liste der Geräte, die derzeit von diesem InTune-Konto in das Autopilot-Programm registriert sind, das möglicherweise nicht bei InTune registriert ist.

Um das Gerät aus dem Autopilot-Programm zu entfernen, wählen Sie das Gerät aus, und klicken Sie auf Löschen.

![Löschen des Geräts](images/delete-device4.png)

Eine Warnmeldung wird angezeigt, in der Sie zunächst das Gerät aus InTune entfernen.

![Löschen des Geräts](images/delete-device5.png)

An diesem Punkt wurde die Registrierung Ihres Geräts bei InTune aufgehoben und die Registrierung von Autopilot aufgehoben.  Klicken Sie nach einigen Minuten auf die Schaltfläche **Synchronisieren** und dann auf die Schaltfläche **Aktualisieren** , um zu bestätigen, dass das Gerät nicht mehr im Autopilot-Programm aufgeführt ist:

![Löschen des Geräts](images/delete-device6.png)

Wenn das Gerät nicht mehr angezeigt wird, können Sie es für andere Zwecke wieder verwenden.

Wenn Sie das Gerät (optional) aus Aad entfernen möchten, navigieren Sie zu **Azure Active Directory > Geräte > alle Geräte**, wählen Sie Ihr Gerät aus, und klicken Sie auf die Schaltfläche "Löschen":

![Löschen des Geräts](images/delete-device7.png)

## <a name="appendix-a-verify-support-for-hyper-v"></a>Anhang A: Überprüfen der Unterstützung für Hyper-V

Ab Windows 8 muss der Mikroprozessor des Host Computers die slat (Second Level Address Translation) für die Installation von Hyper-V unterstützen. Weitere Informationen finden Sie [unter Hyper-V: Liste der slat-fähigen CPUs für Hosts](https://social.technet.microsoft.com/wiki/contents/articles/1401.hyper-v-list-of-slat-capable-cpus-for-hosts.aspx) .

Um zu überprüfen, ob Ihr Computer slat unterstützt, öffnen Sie eine Administrator Eingabeaufforderung, geben Sie **System Info**ein, drücken Sie die EINGABETASTE, Scrollen Sie nach unten, und überprüfen Sie den unten in der Ausgabe angezeigten Abschnitt neben den Hyper-V-Anforderungen. Sehen Sie sich folgendes Beispiel an:

<pre style="overflow-y: visible">
C:>systeminfo

...
Hyper-V Requirements:      VM Monitor Mode Extensions: Yes
                           Virtualization Enabled In Firmware: Yes
                           Second Level Address Translation: Yes
                           Data Execution Prevention Available: Yes
</pre>

In diesem Beispiel unterstützt der Computer slat und Hyper-V.

> Wenn eine oder mehrere Anforderungen als **Nein** ausgewertet werden, unterstützt der Computer die Installation von Hyper-V nicht.  Wenn jedoch nur die Einstellung für die Virtualisierung nicht kompatibel ist, können Sie die Virtualisierung im BIOS aktivieren und die in der **Firmware-Einstellung aktivierte Virtualisierung** von **Nein** in **Ja**ändern. Der Speicherort dieser Einstellung hängt vom Hersteller und der BIOS-Version ab, wird jedoch in der Regel mit den BIOS-Sicherheitseinstellungen verknüpft.

Sie können auch Hyper-V-Unterstützung mithilfe der [Tools](https://blogs.msdn.microsoft.com/taylorb/2008/06/19/hyper-v-will-my-computer-run-hyper-v-detecting-intel-vt-and-amd-v/) des Prozessor Herstellers, des [msinfo32](https://technet.microsoft.com/library/cc731397.aspx) -Tools oder des Hilfsprogramms [Coreinfo](https://technet.microsoft.com/sysinternals/cc835722) herunterladen und ausführen, wie im folgenden Beispiel gezeigt:

<pre style="overflow-y: visible">
C:>coreinfo -v

Coreinfo v3.31 - Dump information on system CPU and memory topology
Copyright (C) 2008-2014 Mark Russinovich
Sysinternals - www.sysinternals.com

Intel(R) Core(TM) i7-2600 CPU @ 3.40GHz
Intel64 Family 6 Model 42 Stepping 7, GenuineIntel
Microcode signature: 0000001B
HYPERVISOR      -       Hypervisor is present
VMX             *       Supports Intel hardware-assisted virtualization
EPT             *       Supports Intel extended page tables (SLAT)
</pre>

> [!NOTE]
> Zum Ausführen von Hyper-V ist ein 64-Bit-Betriebssystem erforderlich.

## <a name="appendix-b-adding-apps-to-your-profile"></a>Anhang B: Hinzufügen von apps zu Ihrem Profil

### <a name="add-a-win32-app"></a>Hinzufügen einer Win32-App

#### <a name="prepare-the-app-for-intune"></a>Vorbereiten der APP für InTune

Bevor wir eine Anwendung in InTune einbinden können, um Sie in unserem AP-Profil zu erstellen, müssen wir die Anwendung mit dem [Befehlszeilen Tool "IntuneWinAppUtil.exe](https://github.com/Microsoft/Microsoft-Win32-Content-Prep-Tool)" Verpacken.  Nachdem Sie das Tool heruntergeladen haben, sammeln Sie die folgenden drei Bits von Informationen, um das Tool zu verwenden:

1. Der Quellordner für Ihre Anwendung.
2. Der Name der ausführbaren Setup Datei.
3. Der Ausgabeordner für die neue Datei.

Im Rahmen dieses Labs verwenden wir das Tool Notepad + + als Win32-app.

Laden Sie das Notepad-MSI-Paket [hier](https://www.hass.de/content/notepad-msi-package-enterprise-deployment-available) herunter, und kopieren Sie die Datei an einen bekannten Speicherort, z. b. "c:\notepad + msi".

Führen Sie das intunewinapputil-Tool aus, und stellen Sie Antworten auf die drei Fragen bereit, z. b.:

![Hinzufügen der App](images/app01.png)

Nachdem die Ausführung des Tools abgeschlossen ist, sollten Sie über eine intunewin-Datei im Ausgabeordner verfügen, die Sie nun mithilfe der folgenden Schritte in InTune hochladen können.

#### <a name="create-app-in-intune"></a>Erstellen einer APP in InTune

Melden Sie sich beim Azure-Portal an, und wählen Sie **InTune**aus.

Navigieren Sie zu **InTune > Clients apps > apps**, und klicken Sie dann auf die Schaltfläche **Hinzufügen** , um ein neues app-Paket zu erstellen.

![Hinzufügen der App](images/app02.png)

Wählen Sie unter **App-Typ**die Option **Windows-app (Win32)** aus:

![Hinzufügen der App](images/app03.png)

Navigieren Sie auf dem Blatt **App-Paketdatei** zu der Datei **NPP. 7.6.3. Installer. x64. intunewin** in Ihrem Ausgabeordner, öffnen Sie Sie, und klicken Sie dann auf **OK**:

![Hinzufügen der App](images/app04.png)

Geben Sie auf dem Blatt **app-Informationen konfigurieren** einen anzeigen Amen, eine Beschreibung und einen Herausgeber an, z. b.:

![Hinzufügen der App](images/app05.png)

Geben Sie auf dem Blatt " **Programmkonfiguration** " die Befehle zum Installieren und deinstallieren an:

Installation: msiexec/i "npp.7.6.3.installer.x64.msi"/q uninstall: msiexec/x "{F188A506-C3C6-4411-BE3A-DA5BF1EA6737}"/q

> [!NOTE]
> Wahrscheinlich müssen Sie die Installations-und Deinstallations Befehle nicht selbst schreiben, da Sie vom [Befehlszeilen ToolIntuneWinAppUtil.exe](https://github.com/Microsoft/Microsoft-Win32-Content-Prep-Tool) automatisch generiert wurden, als die MSI-Datei in eine intunewin-Datei konvertiert wurde.

![Hinzufügen der App](images/app06.png)

Wenn Sie einfach einen Installations Befehl wie "Notepad + +. exe/S" verwenden, wird Notepad nicht installiert. Es wird nur die APP gestartet.  Um das Programm tatsächlich zu installieren, müssen Sie stattdessen die MSI-Datei verwenden.  Notepad + + hat tatsächlich keine MSI-Version des Programms, aber wir haben eine MSI-Version von einem [Drittanbieter](https://www.hass.de/content/notepad-msi-package-enterprise-deployment-available).

Klicken Sie auf **OK** , um die Eingabe zu speichern und das Blatt **Anforderungen** zu aktivieren.

Geben Sie auf dem Blatt **Anforderungs Konfiguration** die **Betriebssystemarchitektur** und die **Mindestversion des Betriebssystems**an:

![Hinzufügen der App](images/app07.png)

Konfigurieren Sie als nächstes die **Erkennungsregeln**.  Zu diesem Zweck wählen wir Manuelles Format aus:

![Hinzufügen der App](images/app08.png)

Klicken Sie zum Definieren der Regel Eigenschaften auf **Hinzufügen** .  Wählen Sie für **Regeltyp**die Option **MSI**aus. Dadurch wird automatisch der richtige MSI-Produktcode in die Regel importiert:

![Hinzufügen der App](images/app09.png)

Klicken Sie zweimal auf **OK** , um den Vorgang zu speichern, und wiederholen Sie den Vorgang für die endgültige Konfiguration zum hauptblatt **app hinzufügen** .

**Rückgabecodes**: belassen Sie für unsere Zwecke die Rückgabecodes mit ihren Standardwerten:

![Hinzufügen der App](images/app10.png)

Klicken Sie zum Beenden auf **OK**.

Sie können die Konfiguration des Blatts " **Endbereich (Tags)** " überspringen.

Klicken Sie auf die Schaltfläche **Hinzufügen** , um das App-Paket abzuschließen und zu speichern.

Sobald die Indikator Meldung besagt, dass die Addition abgeschlossen wurde.

![Hinzufügen der App](images/app11.png)

Sie können Ihre APP in Ihrer APP-Liste finden:

![Hinzufügen der App](images/app12.png)

#### <a name="assign-the-app-to-your-intune-profile"></a>Zuweisen der APP zu Ihrem InTune-Profil

> [!NOTE]
> Die folgenden Schritte funktionieren nur, wenn Sie zuvor [eine Gruppe in InTune erstellt und ihr ein Profil zugewiesen](#assign-the-profile)haben.  Wenn Sie dies noch nicht getan haben, kehren Sie zum Hauptteil des Labs zurück, und führen Sie diese Schritte aus, bevor Sie die Rückgabe hier durchführen.

Wählen Sie im Bereich **InTune-> Client-apps > apps** das App-Paket aus, das Sie bereits erstellt haben, um das zugehörige Blatt Eigenschaften anzuzeigen.  Klicken Sie dann im Menü auf **Zuweisungen** :

![Hinzufügen der App](images/app13.png)

Wählen Sie **Gruppe hinzufügen** aus, um den Bereich **Gruppe hinzufügen** zu öffnen, der mit der App verknüpft ist.

Wählen Sie für unsere Zwecke im Dropdown Menü **Zuweisungstyp** die Option **erforderlich** aus:

> **Verfügbar für registrierte Geräte** bedeutet, dass Benutzer die APP über die Unternehmensportal APP oder Unternehmensportal Website installieren.

Wählen Sie **enthaltene Gruppen** aus, und weisen Sie die zuvor erstellten Gruppen zu, von denen diese APP verwendet wird:

![Hinzufügen der App](images/app14.png)

![Hinzufügen der App](images/app15.png)

Klicken Sie im Bereich **Gruppen auswählen** auf die Schaltfläche **auswählen** .

Wählen Sie im Bereich **Gruppe zuweisen** die Option **OK**aus.

Wählen Sie im Bereich **Gruppe hinzufügen** die Option **OK** aus.

Wählen Sie im Bereich **Zuweisungen** die Option **Speichern** aus.

![Hinzufügen der App](images/app16.png)

An dieser Stelle haben Sie alle Schritte zum Hinzufügen einer Win32-App zu Intune abgeschlossen.

Weitere Informationen zum Hinzufügen von apps zu InTune finden Sie unter [InTune Standalone-Win32-App-Verwaltung](https://docs.microsoft.com/intune/apps-win32-app-management).

### <a name="add-office-365"></a>Hinzufügen von Office 365

#### <a name="create-app-in-intune"></a>Erstellen einer APP in InTune

Melden Sie sich beim Azure-Portal an, und wählen Sie **InTune**aus.

Navigieren Sie zu **InTune > Clients apps > apps**, und klicken Sie dann auf die Schaltfläche **Hinzufügen** , um ein neues app-Paket zu erstellen.

![Hinzufügen der App](images/app17.png)

Wählen Sie unter **App-Typ**die Option **Office 365 Suite > Windows 10**:

![Hinzufügen der App](images/app18.png)

Wählen Sie im Bereich **App-Suite konfigurieren** die Office-Apps aus, die Sie installieren möchten.  Im Rahmen dieser Labe haben wir nur Excel ausgewählt:

![Hinzufügen der App](images/app19.png)

Klicken Sie auf **OK**.

Geben Sie im Bereich "Informationen" der **App-Suite** einen <i>eindeutigen</i> Sammlungsnamen und eine passende Beschreibung ein.

> Geben Sie den Namen der App-Suite so ein, wie er im Unternehmensportal angezeigt wird. Stellen Sie sicher, dass alle Suitenamen eindeutig sind. Wenn ein Sammlungsname zweimal vergeben wird, wird den Benutzern im Unternehmensportal nur eine der Apps angezeigt.

![Hinzufügen der App](images/app20.png)

Klicken Sie auf **OK**.

Wählen Sie im Bereich " **App-Suite-Einstellungen** " die Option **monatlich** für den **Aktualisierungs Kanal** aus. (jede Auswahl wäre für die Zwecke dieses Labs in Ordnung.)  Wählen Sie außerdem **Ja** für **Endbenutzer-Lizenzbedingungen der APP automatisch akzeptieren**aus:

![Hinzufügen der App](images/app21.png)

Klicken Sie auf **OK** und dann auf **Hinzufügen**.

#### <a name="assign-the-app-to-your-intune-profile"></a>Zuweisen der APP zu Ihrem InTune-Profil

> [!NOTE]
> Die folgenden Schritte funktionieren nur, wenn Sie zuvor [eine Gruppe in InTune erstellt und ihr ein Profil zugewiesen](#assign-the-profile)haben.  Wenn Sie dies noch nicht getan haben, kehren Sie zum Hauptteil des Labs zurück, und führen Sie diese Schritte aus, bevor Sie die Rückgabe hier durchführen.

Wählen Sie im Bereich **InTune-> Client-apps > apps** das Office-Paket aus, das Sie bereits erstellt haben, um das Blatt mit den Eigenschaften anzuzeigen.  Klicken Sie dann im Menü auf **Zuweisungen** :

![Hinzufügen der App](images/app22.png)

Wählen Sie **Gruppe hinzufügen** aus, um den Bereich **Gruppe hinzufügen** zu öffnen, der mit der App verknüpft ist.

Wählen Sie für unsere Zwecke im Dropdown Menü **Zuweisungstyp** die Option **erforderlich** aus:

> **Verfügbar für registrierte Geräte** bedeutet, dass Benutzer die APP über die Unternehmensportal APP oder Unternehmensportal Website installieren.

Wählen Sie **enthaltene Gruppen** aus, und weisen Sie die zuvor erstellten Gruppen zu, von denen diese APP verwendet wird:

![Hinzufügen der App](images/app23.png)

![Hinzufügen der App](images/app24.png)

Klicken Sie im Bereich **Gruppen auswählen** auf die Schaltfläche **auswählen** .

Wählen Sie im Bereich **Gruppe zuweisen** die Option **OK**aus.

Wählen Sie im Bereich **Gruppe hinzufügen** die Option **OK** aus.

Wählen Sie im Bereich **Zuweisungen** die Option **Speichern** aus.

![Hinzufügen der App](images/app25.png)

An diesem Punkt sind die Schritte zum Hinzufügen von Office zu InTune abgeschlossen.

Weitere Informationen zum Hinzufügen von Office-Apps zu InTune finden Sie unter [Zuweisen von Office 365-apps zu Windows 10-Geräten mit Microsoft InTune](https://docs.microsoft.com/intune/apps-add-office365).

Wenn Sie sowohl die Win32-app (Notepad + +) als auch Office (nur Excel) gemäß den Anweisungen in dieser Übungseinheit installiert haben, werden Sie auf Ihrem virtuellen Computer in der Liste der apps angezeigt. es kann jedoch einige Minuten dauern, bis Sie aufgefüllt werden:

![Hinzufügen der App](images/app26.png)

## <a name="glossary"></a>Glossar

<table border="1">
<tr><td>OEM</td><td>Original Equipment Manufacturer</td></tr>
<tr><td>CSV</td><td>Durch Kommas getrennte Werte</td></tr>
<tr><td>MPC</td><td>Microsoft Partner Center</td></tr>
<tr><td>CSP</td><td>Cloud Solution Provider</td></tr>
<tr><td>Msfb</td><td>Microsoft Store für Unternehmen</td></tr>
<tr><td>AAD</td><td>Azure Active Directory</td></tr>
<tr><td>4K HH</td><td>4K Hardware Hash</td></tr>
<tr><td>CBR</td><td>Bericht "Computer Erstellung"</td></tr>
<tr><td>EC</td><td>Enterprise Commerce (Server)</td></tr>
<tr><td>DDS</td><td>Geräte Verzeichnisdienst</td></tr>
<tr><td>OOBE</td><td>Standardmäßig</td></tr>
<tr><td>VM</td><td>Virtual Machine</td></tr>
</table>
