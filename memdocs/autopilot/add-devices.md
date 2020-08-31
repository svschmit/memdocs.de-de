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
ms.openlocfilehash: b3f25f424857d99919450ec1426ee1023bae3aca
ms.sourcegitcommit: 41e6e6b7f5c2a87aaf7f23d90d0f175dd63c0579
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2020
ms.locfileid: "89057372"
---
# <a name="adding-devices-to-windows-autopilot"></a>Hinzufügen von Geräten zu Windows Autopilot

**Zielgruppe**

- Windows 10

Vor der Bereitstellung eines Geräts mithilfe von Windows Autopilot muss das Gerät beim Windows Autopilot-Bereitstellungs Dienst registriert werden. Diese Registrierung erfolgt idealerweise durch den OEM, den Reseller oder den Verteiler, von dem die Geräte gekauft wurden. Die Registrierung kann jedoch auch in Ihrer Organisation durchgeführt werden, indem die Hardware Identität gesammelt und manuell hochgeladen wird.

## <a name="oem-registration"></a>OEM-Registrierung

Wenn Sie Geräte von einem OEM kaufen, kann der OEM die Geräte automatisch beim Windows Autopilot registrieren. Eine Liste der OEMs, die die Registrierung unterstützen, finden Sie im Abschnitt "Teilnehmer Gerätehersteller und-Reseller" auf der [Windows Autopilot-Seite](https://aka.ms/windowsautopilot).

Bevor ein OEM Geräte für eine Organisation registrieren kann, muss die Organisation den OEM-Berechtigung erteilen. Der OEM startet diesen Prozess, wobei die Genehmigung durch einen Azure AD globalen Administrator der Organisation gewährt wird. Weitere Informationen finden Sie im Abschnitt "Kunden Zustimmung" auf der [Seite "Kunden Zustimmung](registration-auth.md#oem-authorization)".

> [!Note]
> Die hardwarehashes (auch als Hardware-IDs bezeichnet) werden im Rahmen der OEM-Gerätefertigung generiert und sollten nicht direkt für Kunden oder CSP-Partner bereitgestellt werden. Stattdessen sollte der OEM Geräte im Auftrag des Kunden registrieren. In Fällen, in denen Geräte von CSP-Partnern registriert werden, können OEMs pkid-Informationen für diese Partner bereitstellen, um den Geräte Registrierungsprozess zu unterstützen.

## <a name="reseller-distributor-or-partner-registration"></a>Wiederverkäufer-, Verteiler-oder Partner Registrierung

Kunden können Geräte von Wiederverkäufern, Verteilern oder anderen Partnern erwerben. Solange diese Vertriebspartner, Verteiler und Partner Teil des [CSP-Programms (Cloud Solution Partners)](https://partner.microsoft.com/cloud-solution-provider)sind, können Sie auch Geräte für den Kunden registrieren. 

Wie bei OEMs müssen CSP-Partner die Berechtigung zum Registrieren von Geräten für eine Organisation erhalten. Sie können den auf der [Seite Kunden Zustimmung](registration-auth.md#csp-authorization)beschriebenen Prozess verwenden. Der CSP-Partner fordert eine Beziehung mit der Organisation an. Der globale Administrator dieser Organisation genehmigt die Anforderung. Nach der Genehmigung fügen CSP-Partner Geräte mithilfe von [Partner Center](https://partner.microsoft.com/pcv/dashboard/overview)hinzu, entweder direkt über die Website oder über verfügbare APIs, mit denen die gleichen Aufgaben automatisiert werden können.

Für Windows Autopilot sind beim Einrichten der Beziehung zwischen dem CSP-Partner und der Organisation keine delegierten Administrator Berechtigungen erforderlich. Im Rahmen des Genehmigungsprozesses des globalen Administrators können die Benutzer das Kontrollkästchen "delegierte Administrator Berechtigungen einschließen" deaktivieren.

> [!Note]
> Obwohl Reseller, Verteiler oder Partner jedes neue Windows-Gerät starten können, um den Hardwarehash abzurufen (um Sie für Kunden bereitzustellen oder eine direkte Registrierung durch den Partner zu erhalten), wird dies nicht empfohlen. Stattdessen sollten diese Partner Geräte mithilfe der pkid-Informationen registrieren, die aus der Geräte Verpackung (Barcode) abgerufen oder elektronisch vom OEM-oder upstreampartner (z. b. Verteiler) bezogen werden.

## <a name="automatic-registration-of-existing-devices"></a>Automatische Registrierung vorhandener Geräte

Wenn dies der Fall ist, können Sie automatisch ein vorhandenes Gerät registrieren:
- Ausführen einer unterstützten Version von Windows 10 (halbjährlicher Kanal)
- wird bei einem MDM-Dienst wie InTune registriert.

Bei Geräten, die diese Anforderungen erfüllen, kann der MDM-Dienst das Gerät zum Hardware Hash auffordern. Danach kann das Gerät automatisch bei Windows Autopilot registriert werden.
Anweisungen dazu, wie Sie dies mit Microsoft InTune tun, finden Sie unter [Erstellen einer Autopilot-Bereitstellungs Profil](/intune/enrollment-autopilot#create-an-autopilot-deployment-profile) Dokumentation, in der die Einstellung "Konvertieren aller Zielgeräte in Autopilot" beschrieben wird. 

Diese Geräte können mithilfe der InTune-Einstellung **alle Zielgeräte in Autopilot konvertieren** automatisch in Windows konvertiert werden. Weitere Informationen finden Sie unter [Erstellen eines Autopilot-Bereitstellungsprofils](https://docs.microsoft.com/intune/enrollment-autopilot#create-an-autopilot-deployment-profile). 

Wenn Sie das Szenario [Windows Autopilot for vorhandene Geräte](existing-devices.md) verwenden, müssen Sie die Geräte nicht bei Windows Autopilot vorab registrieren. Stattdessen wird eine Konfigurationsdatei (AutopilotConfigurationFile.js) mit allen Windows Autopilot-Profileinstellungen verwendet. Das Gerät kann dann bei Windows Autopilot mithilfe der gleichen Einstellung "alle Zielgeräte in Autopilot konvertieren" registriert werden.

## <a name="manual-registration"></a>Manuelle Registrierung

Um ein Gerät manuell zu registrieren, müssen Sie zuerst den Hardware Hash erfassen. Nachdem dieser Vorgang abgeschlossen ist, kann der resultierende Hardware Hash in den Windows Autopilot-Dienst hochgeladen werden. Da für diesen Vorgang das Starten des Geräts in Windows 10 erforderlich ist, um den Hardware Hash abzurufen, ist die manuelle Registrierung hauptsächlich für Test-und Auswertungs Szenarien vorgesehen.

> [!Note]
> Kunden können Geräte nur mit einem Hardware Hash registrieren. Andere Methoden (pkid, Tupel) sind über OEMs oder CSP-Partner verfügbar, wie in den vorherigen Abschnitten beschrieben.

## <a name="device-identification"></a>Geräteidentifikation

Zum Identifizieren eines Geräts mit Windows Autopilot muss der eindeutige Hardware Hash des Geräts aufgezeichnet und in den Dienst hochgeladen werden. Dieser Schritt wird idealerweise vom Hardwarehersteller (OEM, Reseller oder Distributor) ausgeführt, der das Gerät automatisch einer Organisation zuordnet. Es ist auch möglich, ein Gerät mit einem erfassten Prozess zu identifizieren, der das Gerät innerhalb einer laufenden Windows 10-Installation sammelt.

Der Hardware Hash enthält Details zum Gerät:
- Hersteller
- model
- Seriennummer des Geräts
- Seriennummer der Festplatte
- Details zu dem Zeitpunkt, zu dem die ID generiert wurde
- viele weitere Attribute, mit denen das Gerät eindeutig identifiziert werden kann

Der Hardware Hash ändert sich bei jeder Generierung, da er Details zu dem Zeitpunkt enthält, zu dem er generiert wurde. Wenn der Windows Autopilot-Bereitstellungs Dienst versucht, ein Gerät abzugleichen, berücksichtigt es Änderungen wie diese. Außerdem werden umfangreiche Änderungen, wie z. b. eine neue Festplatte, berücksichtigt und dennoch erfolgreich abgeglichen. Große Änderungen an der Hardware, wie z. b. die Ersetzung von Motherboards, stimmen jedoch nicht, sodass ein neuer Hash generiert und hochgeladen werden muss.

### <a name="collecting-the-hardware-hash-from-existing-devices-using-microsoft-endpoint-configuration-manager"></a>Erfassen des Hardware Hashs von vorhandenen Geräten mithilfe von Microsoft Endpoint Configuration Manager

Microsoft Endpoint Configuration Manager erfasst automatisch die hardwarehashes für vorhandene Windows 10-Geräte. Weitere Informationen finden Sie unter [Sammeln von Informationen aus Configuration Manager für Windows Autopilot](/configmgr/comanage/how-to-prepare-win10#windows-autopilot). Sie können die Hash Informationen aus Configuration Manager in eine CSV-Datei extrahieren.

> [!Note]
> Stellen Sie vor dem Hochladen der CSV-Datei in InTune sicher, dass die erste Zeile die Seriennummer des Geräts, die Windows-Produkt-ID, den Hardware Hash, das Gruppentag und den zugewiesenen Benutzer enthält. Wenn oben in der CSV-Dateiheader Informationen vorhanden sind, löschen Sie diese Header Informationen. Weitere Informationen finden Sie unter [Registrieren von Windows-Geräten in InTune](/intune/enrollment/enrollment-autopilot).

### <a name="collecting-the-hardware-hash-from-existing-devices-using-powershell"></a>Erfassen des Hardware Hashs von vorhandenen Geräten mithilfe von PowerShell

Der Hardwarehash für ein vorhandenes Gerät steht über Windows-Verwaltungsinstrumentation (WMI) zur Verfügung, solange auf diesem Gerät eine unterstützte Version des halbjährlichen Kanals von Windows 10 ausgeführt wird. Sie können ein PowerShell-Skript verwenden ([Get-WindowsAutoPilotInfo.ps1](https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo) , um den Hardware Hash und die Seriennummer eines Geräts zu erhalten. Die Seriennummer ist hilfreich, um schnell festzustellen, zu welchem Gerät der Hardware Hash gehört.

Um dieses Skript zu verwenden, können Sie eine der folgenden Methoden verwenden:
- Laden Sie Sie vom PowerShell-Katalog herunter, und führen Sie Sie auf jedem Computer aus.
- Installieren Sie Sie direkt aus dem PowerShell-Katalog.

Verwenden Sie die folgenden Befehle an einer Windows PowerShell-Eingabeaufforderung mit erhöhten Rechten, um Sie direkt zu installieren und den Hardware Hash vom lokalen Computer zu erfassen:

```powershell
md c:\\HWID
Set-Location c:\\HWID
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Unrestricted
Install-Script -Name Get-WindowsAutoPilotInfo
Get-WindowsAutoPilotInfo.ps1 -OutputFile AutoPilotHWID.csv
```

Sie können die Befehle remote ausführen, wenn die beiden folgenden Punkte zutreffen:
- WMI-Berechtigungen sind vorhanden.
- Der Zugriff auf WMI erfolgt über die Windows-Firewall auf dem Remote Computer.

Weitere Informationen zum Ausführen des Skripts finden Sie in der Hilfe zum [Get-windowsautopilotinfo](https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo) -Skript unter Verwendung von "Get-Help Get-WindowsAutoPilotInfo.ps1".

>[!IMPORTANT]
>Verbinden Sie Geräte nicht mit dem Internet, bevor Sie den Hardware Hash erfassen und ein Autopilot-Geräte Profil erstellen. Dies umfasst das Erfassen des Hardware Hashs und das Hochladen von. CSV in msfb oder InTune, Zuweisen des Profils und bestätigen der Profil Zuweisung. Das Herstellen einer Verbindung zwischen dem Gerät und dem Internet, bevor dieser Vorgang ausgeführt wird, führt dazu, dass das Gerät ein leeres Profil herunterlädt, das auf dem Gerät gespeichert wird, bis es explizit entfernt wird. In Windows 10, Version 1809, können Sie das zwischengespeicherte Profil durch Neustarten von OOBE löschen. In früheren Versionen ist die einzige Möglichkeit, das gespeicherte Profil zu löschen, das Neuinstallieren des Betriebssystems, das reimaging des PCs oder das Ausführen von **syredp/generalize/oobe**. <br>
>Wenn InTune das Profil für den einsatzbereit meldet, sollte das Gerät nur mit dem Internet verbunden sein.

>[!NOTE]
>Wenn OOBE zu oft neu gestartet wird, kann es in den Wiederherstellungs Modus wechseln und die Autopilot-Konfiguration nicht ausführen. Sie können dieses Szenario identifizieren, wenn in OOBE mehrere Konfigurationsoptionen auf derselben Seite angezeigt werden, einschließlich Sprache, Region und Tastaturlayout. In der normalen OOBE werden diese auf einer separaten Seite angezeigt. Der folgende Wert Schlüssel verfolgt die Anzahl von OOBE-Wiederholungen: <br>
>**Hkcu\software \\ Microsoft \\ Windows \\ CurrentVersion \\ useroobe** <br>
>Um sicherzustellen, dass OOBE zu oft nicht neu gestartet wurde, können Sie diesen Wert in 1 ändern.

## <a name="registering-devices"></a>Registrieren von Geräten

<img src="./images/image2.png" width="511" height="249" alt="process" />


Nachdem die hardwarehashes von vorhandenen Geräten erfasst wurden, können Sie mit einer der folgenden Methoden hochgeladen werden:

- [Microsoft InTune](enrollment-autopilot.md) ist der bevorzugte Mechanismus für alle Kunden.
 - Das Microsoft Endpoint Manager Admin Center wird für die Intune-Geräteregistrierung verwendet.
- [Partner Center](https://msdn.microsoft.com/partner-center/autopilot) wird von CSP-Partnern zum Registrieren von Geräten für Kunden verwendet.
- [Microsoft 365 Business & Office 365 admin](https://support.office.com/article/Create-and-edit-AutoPilot-profiles-5cf7139e-cfa1-4765-8aad-001af1c74faa) wird in der Regel von kleinen und mittelständischen Unternehmen (smsb) verwendet, die Ihre Geräte mit Microsoft 365 Business verwalten.
- [Microsoft Store für Unternehmen](/microsoft-store/add-profile-to-devices#manage-autopilot-deployment-profiles). Möglicherweise verwenden Sie msfb bereits zum Verwalten Ihrer Apps und Einstellungen.

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
<td><a href="https://docs.microsoft.com/microsoft-365/business/create-and-edit-autopilot-profiles">Microsoft 365 Business Premium</a></td>
<td>Ja-1000 gleichzeitig max.</td>
<td>Ja<b><sup>3</sup></b></td>
<td>4K HH</td>
</tr>

</table>

><b><sup>1</sup></b> Von Microsoft empfohlene Plattform für die Verwendung<br>
><b><sup>2</sup></b> InTune-Lizenz erforderlich<br>
><b><sup>3</sup></b> Funktions Funktionen sind eingeschränkt<br>
><b><sup>4</sup></b> Die Geräte Profil Zuweisung wird in den nächsten Monaten von msfb und Partner Center eingestellt.<br>

Weitere Informationen zu Geräte-IDs finden Sie in den folgenden Themen:
- [Geräte Identifizierung](#device-identification)
- [Windows Autopilot-Geräte Richtlinien](autopilot-device-guidelines.md)
- [Hinzufügen von Geräten zu einem Kundenkonto](/partner-center/autopilot)


## <a name="summary"></a>Zusammenfassung

Wenn Sie neue Geräte mit Windows Autopilot bereitstellen, sind die folgenden Schritte erforderlich:

1. [Registrieren von Geräten](#registering-devices). Im Idealfall erfolgt dieser Schritt durch den OEM, den Reseller oder den Verteiler, von dem die Geräte gekauft wurden. Die Registrierung kann jedoch auch von der Organisation durchgeführt werden, indem die Hardware Identität gesammelt und manuell hochgeladen wird.
2. [Konfigurieren von Geräte Profilen](profiles.md). Geben Sie an, wie das Gerät bereitgestellt werden soll und welche Benutzerinhalte angezeigt werden sollen.
3. Starten Sie das Gerät. Wenn das Gerät mit einem Netzwerk verbunden ist, das über Internet Zugriff verfügt, wird der Windows Autopilot-Bereitstellungs Dienst kontaktiert, um festzustellen, ob das Gerät registriert ist. Wenn Sie registriert ist, werden Profileinstellungen wie z. b. die Seite Anmeldungs [Status](enrollment-status.md)heruntergeladen, die zum Anpassen der Endbenutzer Umgebung verwendet wird.

## <a name="next-steps"></a>Nächste Schritte

[BitLocker-Verschlüsselungseinstellungen](bitlocker.md): Sie können die BitLocker-Verschlüsselungseinstellungen so konfigurieren, dass Sie vor dem Start der automatischen Verschlüsselung angewendet werden.