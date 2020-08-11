---
title: Hinzufügen von Geräten
ms.reviewer: ''
manager: laurawi
description: Vorgehensweise beim Hinzufügen von Geräten zu Windows Autopilot
keywords: MDM, Setup, Windows, Windows 10, OOBE, Manage, Bereitstellung, Autopilot, ZTD, Zero-Touchscreen, Partner, msfb, InTune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: fc892a4372aa7d72f294ddf93f811d641ca961b5
ms.sourcegitcommit: 47ed9af2652495adb539638afe4e0bb0be267b9e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/10/2020
ms.locfileid: "88051424"
---
# <a name="adding-devices-to-windows-autopilot"></a>Hinzufügen von Geräten zu Windows Autopilot

**Zielgruppe**

- Windows 10

Vor der Bereitstellung eines Geräts mithilfe von Windows Autopilot muss das Gerät beim Windows Autopilot-Bereitstellungs Dienst registriert werden. Im Idealfall erfolgt dies durch den OEM, den Reseller oder den Verteiler, von dem die Geräte gekauft wurden. Dies kann jedoch auch durch die Organisation erfolgen, indem die Hardware Identität gesammelt und manuell hochgeladen wird.

## <a name="oem-registration"></a>OEM-Registrierung

Wenn Sie Geräte direkt von einem OEM kaufen, kann der OEM die Geräte automatisch beim Windows Autopilot-Bereitstellungs Dienst registrieren.  Eine Liste der OEMs, die diese zurzeit unterstützen, finden Sie im Abschnitt "Teilnehmer Gerätehersteller und-Reseller" auf der [Windows Autopilot-Informationsseite](https://aka.ms/windowsautopilot).

Bevor ein OEM Geräte im Auftrag einer Organisation registrieren kann, muss die Organisation den OEM-Berechtigung erteilen.  Dieser Prozess wird vom OEM initiiert, wobei die Genehmigung durch einen Azure AD globalen Administrator der Organisation gewährt wird.  Weitere Informationen finden Sie im Abschnitt "Kunden Zustimmung" auf der [Seite "Kunden Zustimmung](registration-auth.md#oem-authorization)".

> [!Note]
> Während die hardwarehashes im Rahmen der OEM-Gerätefertigung generiert werden, sollten diese nicht direkt für Kunden oder CSP-Partner bereitgestellt werden.  Stattdessen sollte der OEM Geräte im Auftrag des Kunden registrieren.  In Fällen, in denen Geräte von CSP-Partnern registriert werden, können OEMs pkid-Informationen für diese Partner bereitstellen, um den Geräte Registrierungsprozess zu unterstützen.

## <a name="reseller-distributor-or-partner-registration"></a>Wiederverkäufer-, Verteiler-oder Partner Registrierung

Kunden können Geräte von Wiederverkäufern, Verteilern oder anderen Partnern erwerben.  Solange diese Händler, Verteiler und Partner Teil des [Cloud Solution Partners (CSP)-Programms](https://partner.microsoft.com/cloud-solution-provider)sind, können Sie auch Geräte im Auftrag des Kunden registrieren.  

Wie bei OEMs muss den CSP-Partnern die Berechtigung erteilt werden, Geräte im Auftrag einer Organisation zu registrieren.  Dies folgt dem auf der [Seite Kunden Zustimmung](registration-auth.md#csp-authorization)beschriebenen Prozess.  Der CSP-Partner initiiert eine Anforderung zum Einrichten einer Beziehung mit der Organisation, wobei die Genehmigung durch einen globalen Administrator der Organisation gewährt wird.  Nach der Genehmigung fügen CSP-Partner Geräte mithilfe von [Partner Center](https://partner.microsoft.com/pcv/dashboard/overview)hinzu, entweder direkt über die Website oder über verfügbare APIs, mit denen die gleichen Aufgaben automatisiert werden können.

Für Windows Autopilot sind beim Einrichten der Beziehung zwischen dem CSP-Partner und der Organisation keine delegierten Administrator Berechtigungen erforderlich.  Im Rahmen des Genehmigungsprozesses, der vom globalen Administrator ausgeführt wird, kann der globale Administrator auswählen, dass das Kontrollkästchen "delegierte Administrator Berechtigungen einschließen" deaktivieren soll.

> [!Note]
> Auch wenn Reseller, Verteiler oder Partner alle neuen Windows-Geräte starten können, um den Hardwarehash abzurufen (um Sie für Kunden bereitzustellen oder eine direkte Registrierung durch den Partner zu erhalten), wird dies nicht empfohlen.  Stattdessen sollten diese Partner Geräte mithilfe der pkid-Informationen registrieren, die aus der Geräte Verpackung (Barcode) abgerufen oder elektronisch vom OEM-oder upstreampartner (z. b. Verteiler) bezogen werden.

## <a name="automatic-registration-of-existing-devices"></a>Automatische Registrierung vorhandener Geräte

Wenn auf einem vorhandenen Gerät bereits eine unterstützte Version des halbjährlichen Kanals von Windows 10 ausgeführt und in einem MDM-Dienst wie InTune registriert ist, kann der MDM-Dienst das Gerät nach der Hardware-ID (auch als Hardwarehash bezeichnet) Abfragen.  Sobald dies der Fall ist, kann das Gerät automatisch bei Windows Autopilot registriert werden.

Anweisungen dazu, wie Sie dies mit Microsoft InTune tun, finden Sie unter [Erstellen einer Autopilot-Bereitstellungs Profil](https://docs.microsoft.com/intune/enrollment-autopilot#create-an-autopilot-deployment-profile) Dokumentation, in der die Einstellung "Konvertieren aller Zielgeräte in Autopilot" beschrieben wird. 

Beachten Sie auch, dass bei Verwendung des Szenarios [Windows Autopilot für vorhandene Geräte](existing-devices.md) das vorab registrieren der Geräte bei Windows Autopilot nicht erforderlich ist.  Stattdessen wird eine Konfigurationsdatei (AutopilotConfigurationFile.js) mit allen Windows Autopilot-Profileinstellungen verwendet. das Gerät kann bei Windows Autopilot registriert werden, wenn die Einstellung "alle Zielgeräte in Autopilot konvertieren" verwendet wird.

## <a name="manual-registration"></a>Manuelle Registrierung

Um die manuelle Registrierung eines Geräts auszuführen, müssen Sie zunächst die Hardware-ID (auch als Hardwarehash bezeichnet) erfassen.  Nachdem dieser Vorgang abgeschlossen wurde, kann die resultierende Hardware-ID in den Windows Autopilot-Dienst hochgeladen werden.  Da für diesen Vorgang das Gerät in Windows 10 gestartet werden muss, um die Hardware-ID zu erhalten, ist dies hauptsächlich für Test-und Auswertungs Szenarien vorgesehen.

> [!Note]
> Kunden können Geräte nur mit einem Hardware Hash registrieren.  Andere Methoden (pkid, Tupel) sind über OEMs oder CSP-Partner verfügbar, wie in den vorherigen Abschnitten beschrieben.

## <a name="device-identification"></a>Geräteidentifikation

Zum Definieren eines Geräts für den Windows Autopilot-Bereitstellungs Dienst muss eine eindeutige Hardware-ID für das Gerät erfasst und in den Dienst hochgeladen werden. Dieser Schritt wird zwar idealerweise vom Hardwarehersteller (OEM, Reseller oder Distributor) durchgeführt, und das Gerät wird automatisch einer Organisation zugeordnet, aber es ist auch möglich, dies durch einen erfassten Prozess zu erreichen, bei dem das Gerät von einer laufenden Windows 10-Installation erfasst wird.

Die Hardware-ID (auch als Hardwarehash bezeichnet) enthält verschiedene Details zum Gerät, einschließlich Hersteller, Modell, Geräteserien Nummer, Festplatten Seriennummer und zahlreichen anderen Attributen, mit denen das Gerät eindeutig identifiziert werden kann.

Beachten Sie, dass der Hardware Hash auch Details zu dem Zeitpunkt enthält, zu dem er generiert wurde, sodass er sich bei jeder Generierung ändert. Wenn der Windows Autopilot-Bereitstellungs Dienst versucht, ein Gerät abzugleichen, berücksichtigt es Änderungen wie diese und ausführlichere Änderungen, wie z. b. eine neue Festplatte, und kann dennoch erfolgreich abgeglichen werden. Wesentliche Änderungen an der Hardware, wie z. b. das Austauschen von Motherboards, stimmen jedoch nicht, sodass ein neuer Hash generiert und hochgeladen werden muss.

### <a name="collecting-the-hardware-id-from-existing-devices-using-microsoft-endpoint-configuration-manager"></a>Erfassen der Hardware-ID von vorhandenen Geräten mithilfe von Microsoft Endpoint Configuration Manager

Microsoft Endpoint Configuration Manager erfasst automatisch die hardwarehashes für vorhandene Windows 10-Geräte. Weitere Informationen finden Sie unter [Sammeln von Informationen aus Configuration Manager für Windows Autopilot](https://docs.microsoft.com/configmgr/comanage/how-to-prepare-win10#windows-autopilot). Sie können die Hash Informationen aus Configuration Manager in eine CSV-Datei extrahieren.

> [!Note]
> Stellen Sie vor dem Hochladen der CSV-Datei in InTune sicher, dass die erste Zeile die Seriennummer des Geräts, die Windows-Produkt-ID, den Hardware Hash, das Gruppentag und den zugewiesenen Benutzer enthält. Wenn oben in der CSV-Dateiheader Informationen vorhanden sind, löschen Sie diese Header Informationen. Weitere Informationen finden Sie unter [Registrieren von Windows-Geräten in InTune](https://docs.microsoft.com/intune/enrollment/enrollment-autopilot).

### <a name="collecting-the-hardware-id-from-existing-devices-using-powershell"></a>Erfassen der Hardware-ID von vorhandenen Geräten mithilfe von PowerShell

Die Hardware-ID oder der Hardwarehash für ein vorhandenes Gerät steht über Windows-Verwaltungsinstrumentation (WMI) zur Verfügung, solange auf diesem Gerät eine unterstützte Version des halbjährlichen Kanals von Windows 10 ausgeführt wird. Um diese Informationen und die Seriennummer des Geräts zu erfassen (auf einen Blick auf den Computer, zu dem Sie gehört), wird ein PowerShell-Skript mit dem Namen [Get-WindowsAutoPilotInfo.ps1 auf der PowerShell-Katalog-Website veröffentlicht](https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo).

Um dieses Skript zu verwenden, können Sie es vom PowerShell-Katalog herunterladen und auf jedem Computer ausführen, oder Sie können es direkt über die PowerShell-Katalog installieren. Verwenden Sie die folgenden Befehle an einer Windows PowerShell-Eingabeaufforderung mit erhöhten Rechten, um Sie direkt zu installieren und den Hardware Hash vom lokalen Computer zu erfassen:

```powershell
md c:\\HWID
Set-Location c:\\HWID
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Unrestricted
Install-Script -Name Get-WindowsAutoPilotInfo
Get-WindowsAutoPilotInfo.ps1 -OutputFile AutoPilotHWID.csv
```

Die Befehle können auch remote ausgeführt werden, solange WMI-Berechtigungen vorhanden sind und auf WMI über die Windows-Firewall auf dem Remote Computer zugegriffen werden kann. Weitere Informationen zum Ausführen des Skripts finden Sie in der Hilfe zum [Get-windowsautopilotinfo](https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo) -Skript (unter Verwendung von "Get-Help Get-WindowsAutoPilotInfo.ps1").

>[!IMPORTANT]
>Verbinden Sie Geräte nicht vor dem Erfassen der Hardware-ID und dem Erstellen eines Autopilot-Geräte Profils mit dem Internet. Dies umfasst das Erfassen der Hardware-ID und das Hochladen von. CSV in msfb oder InTune, Zuweisen des Profils und bestätigen der Profil Zuweisung. Das Herstellen einer Verbindung zwischen dem Gerät und dem Internet, bevor dieser Vorgang ausgeführt wird, führt dazu, dass das Gerät ein leeres Profil herunterlädt, das auf dem Gerät gespeichert wird, bis es explizit entfernt wird. In Windows 10, Version 1809, können Sie das zwischengespeicherte Profil durch Neustarten von OOBE löschen. In früheren Versionen ist die einzige Möglichkeit, das gespeicherte Profil zu löschen, das Neuinstallieren des Betriebssystems, das reimaging des PCs oder das Ausführen von **syredp/generalize/oobe**. <br>
>Wenn InTune das Profil für den einsatzbereit meldet, sollte das Gerät nur mit dem Internet verbunden sein.

>[!NOTE]
>Wenn OOBE zu oft neu gestartet wird, kann es in den Wiederherstellungs Modus wechseln und die Autopilot-Konfiguration nicht ausführen. Sie können dieses Szenario identifizieren, wenn in OOBE mehrere Konfigurationsoptionen auf derselben Seite angezeigt werden, einschließlich Sprache, Region und Tastaturlayout. In der normalen OOBE werden diese auf einer separaten Seite angezeigt. Der folgende Wert Schlüssel verfolgt die Anzahl von OOBE-Wiederholungen: <br>
>**Hkcu\software \\ Microsoft \\ Windows \\ CurrentVersion \\ useroobe** <br>
>Um sicherzustellen, dass OOBE zu oft nicht neu gestartet wurde, können Sie diesen Wert in 1 ändern.

## <a name="registering-devices"></a>Registrieren von Geräten

<img src="./images/image2.png" width="511" height="249" alt="process" />


Nachdem die Hardware-IDs von vorhandenen Geräten erfasst wurden, können Sie über eine Vielzahl von Methoden hochgeladen werden. Lesen Sie die ausführliche Dokumentation für jeden verfügbaren Mechanismus.

-   [Microsoft InTune](enrollment-autopilot.md).  Dies ist der bevorzugte Mechanismus für alle Kunden.
    - Das Microsoft Endpoint Manager Admin Center wird für die Intune-Geräteregistrierung verwendet.
-   [Partner Center](https://msdn.microsoft.com/partner-center/autopilot).  Diese wird von CSP-Partnern zum Registrieren von Geräten im Auftrag von Kunden verwendet.
-   [Microsoft 365 Business & Office 365 admin](https://support.office.com/article/Create-and-edit-AutoPilot-profiles-5cf7139e-cfa1-4765-8aad-001af1c74faa).  Dies wird in der Regel von kleinen und mittelständischen Unternehmen (smsb) verwendet, die Ihre Geräte mit Microsoft 365 Business verwalten.
-   [Microsoft Store für Unternehmen](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#manage-autopilot-deployment-profiles).  Möglicherweise verwenden Sie msfb bereits zum Verwalten Ihrer Apps und Einstellungen.

Unten finden Sie eine Übersicht über die Funktionen der einzelnen Plattformen.<br>
<br>
<table>
<tr>
<td BGCOLOR="#a0e4fa"><B><font color="#000000">Plattform/Portal</font></td>
<td BGCOLOR="#a0e4fa"><B><font color="#000000">Geräte registrieren?</font></td>
<td BGCOLOR="#a0e4fa"><B><font color="#000000">Profil erstellen/zuweisen</font></td>
<td BGCOLOR="#a0e4fa"><B><font color="#000000">Akzeptable Geräte-ID</font></td>
</tr>

<tr>
<td>OEM Direct-API</td>
<td>Ja-1000 gleichzeitig max.</td>
<td>Nein</td>
<td>Tupel oder pkid</td>
</tr>

<tr>
<td><a href="https://docs.microsoft.com/partner-center/autopilot">Partner Center</a></td>
<td>Ja-1000 gleichzeitig max.</td>
<td>Ja<b><sup>34</sup></b></td>
<td>Tupel oder pkid oder 4K HH</td>
</tr>

<tr>
<td><a href="enrollment-autopilot.md">Intune</a></td>
<td>Ja-500 zu einer Zeit (max.<b><sup>1</sup> )</b></td> 
<td>Ja<b><sup>12</sup></b></td> 
<td>4K HH</td>
</tr>

<tr>
<td><a href="https://docs.microsoft.com/microsoft-store/add-profile-to-devices#manage-autopilot-deployment-profiles">Microsoft Store für Unternehmen</a></td>
<td>Ja-1000 gleichzeitig max.</td>
<td>Ja<b><sup>4</sup></b></td>
<td>4K HH</td>
</tr>

<tr>
<td><a href="https://docs.microsoft.com/microsoft-365/business/create-and-edit-autopilot-profiles">Microsoft 365 Business</a></td>
<td>Ja-1000 gleichzeitig max.</td>
<td>Ja<b><sup>3</sup></b></td>
<td>4K HH</td>
</tr>

</table>

><b><sup>1</sup></b> Von Microsoft empfohlene Plattform für die Verwendung<br>
><b><sup>2</sup></b> InTune-Lizenz erforderlich<br>
><b><sup>3</sup></b> Funktions Funktionen sind eingeschränkt<br>
><b><sup>4</sup></b> Die Geräte Profil Zuweisung wird in den nächsten Monaten von msfb und Partner Center eingestellt.<br>


Weitere Informationen zu Geräte-IDs finden Sie auch in den folgenden Themen:
- [Geräte Identifizierung](#device-identification)
- [Windows Autopilot-Geräte Richtlinien](autopilot-device-guidelines.md)
- [Hinzufügen von Geräten zu einem Kundenkonto](https://docs.microsoft.com/partner-center/autopilot)


## <a name="summary"></a>Zusammenfassung

Wenn Sie neue Geräte mit Windows Autopilot bereitstellen, sind die folgenden Schritte erforderlich:

1.  [Registrieren von Geräten](#registering-devices). Im Idealfall erfolgt dieser Schritt durch den OEM, den Reseller oder den Verteiler, von dem die Geräte gekauft wurden. Dies kann jedoch auch von der Organisation durchgeführt werden, indem die Hardware Identität gesammelt und manuell hochgeladen wird.
2.  [Konfigurieren von Geräte Profilen](profiles.md), angeben der Art und Weise, wie das Gerät bereitgestellt werden soll und welche Benutzerinhalte angezeigt werden sollen.
3.  Starten Sie das Gerät. Wenn das Gerät mit einem Netzwerk verbunden ist, das über Internet Zugriff verfügt, wird der Windows Autopilot-Bereitstellungs Dienst kontaktiert, um festzustellen, ob das Gerät registriert ist. ist dies der Fall, werden Profileinstellungen wie z. b. die Seite zum Registrierungs [Status](enrollment-status.md)heruntergeladen, die zum Anpassen der Endbenutzer Umgebung verwendet werden.

## <a name="other-configuration-settings"></a>Weitere Konfigurationseinstellungen

- [BitLocker-Verschlüsselungseinstellungen](bitlocker.md): Sie können die BitLocker-Verschlüsselungseinstellungen so konfigurieren, dass Sie vor dem Start der automatischen Verschlüsselung angewendet werden.