---
title: Bekannte Probleme von Windows Autopilot
ms.reviewer: ''
manager: laurawi
description: Informieren Sie sich über bekannte Probleme, die während der Bereitstellung von Windows Autopilot auftreten können.
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
ms.openlocfilehash: d7c92d2e999ffe9a4e503359a81e6422cd24ee30
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252023"
---
# <a name="windows-autopilot---known-issues"></a>Windows Autopilot-bekannte Probleme

**Zielgruppe**

- Windows 10

<table>
<th>Problem<th>Weitere Informationen

<tr><td>Das Blockieren von apps, die in einem benutzerorientierten Registrierungs Status Profil angegeben sind, wird während des Geräte-ESP ignoriert.</td>
<td>Die Dienste, die für die Ermittlung der Liste der apps verantwortlich sind, die während des Geräte-ESP blockiert werden sollten, können das richtige ESP-Profil mit der Liste der apps nicht ermitteln, da Sie die Benutzeridentität nicht kennen. Aktivieren Sie als Problem Umgehung das Standard-ESP-Profil (das alle Benutzer und Geräte als Ziel hat), und platzieren Sie die Liste der blockierenden apps dort. In Zukunft ist es möglich, stattdessen das ESP-Profil für Gerätegruppen als Ziel zu verwenden, um dieses Problem zu vermeiden.</tr>

<tr><td>Dieser Benutzername gehört zu einer anderen Organisation. Versuchen Sie, sich erneut anzumelden, oder beginnen Sie mit einem anderen Konto.</td>
 <td>Vergewissern Sie sich, dass alle Informationen unter HKEY_LOCAL_MACHINE \software\microsoft\provisioning\diagnostics\autopilotcs korrekt sind. Weitere Informationen finden Sie unter <a href="troubleshooting.md#windows-10-version-1709-and-above">Problembehandlung bei Windows Autopilot</a>.</td></tr>

<tr><td>Benutzergesteuerte Windows Autopilot-Azure AD Hybrid Bereitstellungen gewähren Benutzern keine Administrator Rechte, auch wenn Sie im Windows Autopilot-Profil angegeben sind.</td>
<td>Dieses Problem tritt auf, wenn ein anderer Benutzer auf dem Gerät vorhanden ist, der bereits über Administrator Rechte verfügt. Beispielsweise könnte ein PowerShell-Skript oder eine Richtlinie ein zusätzliches lokales Konto erstellen, das Mitglied der Gruppe "Administratoren" ist. Um sicherzustellen, dass dies ordnungsgemäß funktioniert, erstellen Sie erst dann ein zusätzliches Konto, wenn der Windows Autopilot-Prozess abgeschlossen ist.</tr>

<tr><td>Die Windows Autopilot-Geräte Bereitstellung kann mit TPM-Nachweis Fehlern oder ESP-Timeouts auf Geräten fehlschlagen, bei denen die Echtzeit-Uhr über einen beträchtlichen Zeitraum (z. b. mehrere Minuten oder mehr) ausfällt.</td>
<td>So beheben Sie dieses Problem: <ol><li>Starten Sie das Gerät bis zum Anfang der Out-of-Box-Funktion (OOBE).
<li>Richten Sie eine Netzwerkverbindung (Kabel-oder Drahtlos Netzwerk) ein.
<li>Führen Sie den Befehl <b>w32tm/resync/Force</b> aus, um die Uhrzeit mit dem Standardzeit Server (Time.Windows.com) zu synchronisieren.</ol>
</tr>

<tr><td>Windows Autopilot für vorhandene Geräte funktioniert nicht für Windows 10, Version 1903 oder 1909; Sie sehen Bildschirme, die Sie in Ihrem Windows Autopilot-Profil deaktiviert haben, z. b. den Bildschirm Windows 10-Lizenzvertrag.
<br>&nbsp;<br>
Dieses Problem tritt auf, weil Windows 10, Version 1903 und 1909, die AutopilotConfigurationFile.jsfür die Datei löscht.
<td>So beheben Sie dieses Problem: <ol><li>Bearbeiten Sie die Configuration Manager Tasksequenz, und deaktivieren Sie den Schritt <b>Windows für die Erfassung vorbereiten</b> .
<li>Fügen Sie einen neuen Schritt <b>Befehlszeile ausführen</b> hinzu, der <b>c:\windows\system32\sysprep\sysprep.exe/OOBE/Reboot</b>ausgeführt wird.</ol>
<a href="https://oofhours.com/2019/09/19/a-challenge-with-windows-autopilot-for-existing-devices-and-windows-10-1903/">Weitere Informationen</a></tr>
 
<tr><td>Der TPM-Nachweis schlägt unter Windows 10 1903 fehl, weil die aki-Erweiterung im EK-Zertifikat fehlt. (Eine zusätzliche Validierung wurde in Windows 10 1903 hinzugefügt, um zu überprüfen, ob die TPM EK-Zertifikate über die richtigen Attribute verfügen, die den TCG-Spezifikationen zufolge nicht entsprechen, sodass die Validierung entfernt wird.)
<td>Laden Sie das <a href="https://support.microsoft.com/help/4517211/windows-10-update-kb4517211">KB4517211 Update</a>herunter, und installieren Sie es.
<tr><td>Die folgenden bekannten Probleme werden durch die Installation des Updates vom 30. August 2019 KB4512941 (OS Build 18362,329) behoben:

- Das Feature Windows Autopilot für vorhandene Geräte unterdrückt die Seite "Aktivitäten" während des OOBE-Features nicht ordnungsgemäß. (Aufgrund dieses Problems sehen Sie diese zusätzliche Seite während OOBE).
- Der TPM-Nachweis Status wird nicht durch die systatp-/generalize gelöscht, was zu einem TPM-Nachweis Fehler während eines späteren OOBE-Flusses führt. (Dies ist kein besonders häufiges Problem, aber Sie können es beim Testen ausführen, wenn Sie systrep ausführen/generalize und dann neu starten oder das Gerät neu starten, um durch einen Autopilot-weißen Handschuh oder ein selbst Bereitstellungs Szenario zurückzukehren.
- Der TPM-Nachweis schlägt möglicherweise fehl, wenn das Gerät über ein gültiges AIK-Zertifikat, aber kein EK-Zertifikat verfügt. (dieses Problem bezieht sich auf das vorherige Element.)
- Wenn der TPM-Nachweis während des Windows Autopilot-White-Glove-Prozesses fehlschlägt, scheint die Landing Page nicht mehr zu reagieren. (Im Grunde ist die Startseite des weißen handtrehs, bei der Sie auf "Bereitstellen" klicken, um den weißen Hand Schuh Prozess zu starten, Fehler nicht ordnungsgemäß.)
- Der TPM-Nachweis schlägt bei neueren Version von Infineon-TPMs (Firmwareversion > 7,69) fehl. (Vor dieser Behebung wurde nur eine bestimmte Liste der Firmwareversionen akzeptiert.)
- Geräte Benennungs Vorlagen können den Computernamen bei 14 Zeichen anstelle von 15 abschneiden.
- Zugewiesene Zugriffsrichtlinien verursachen einen Neustart, der die Konfiguration von Kiosk Geräten mit einer einzelnen App beeinträchtigen kann.
<td>Laden Sie das <a href="https://support.microsoft.com/help/4512941">KB4512941 Update</a>herunter, und installieren Sie es. <br><br>Informationen zu bestimmten releasekanälen, die Sie zum Abrufen des Updates verwenden können, finden Sie im Abschnitt: Abrufen <b>dieses Updates</b> .
<tr><td>Die folgenden bekannten Probleme werden durch die Installation des Updates vom 26. Juli 2019 KB4505903 (OS Build 18362,267) behoben:

- Der Windows Autopilot White Glove funktioniert nicht für ein nicht englischsprachiges Betriebssystem, und es wird ein Roter Bildschirm angezeigt, der besagt, dass "Erfolg" lautet.
- Windows Autopilot meldet einen autopilotupdate-Fehler während des OOBE-Fehlers nach syunp, Reset oder anderen Variationen. Dieses Problem tritt normalerweise auf, wenn Sie das Betriebssystem zurücksetzen oder ein benutzerdefiniertes System mit System Vorbereitung verwenden.
- Die BitLocker-Verschlüsselung ist nicht ordnungsgemäß konfiguriert. Beispiel: BitLocker hat keine erwartete Benachrichtigung erhalten, nachdem Richtlinien angewendet wurden, um die Verschlüsselung zu starten.
- Sie sind nicht in der Lage, UWP-Apps aus dem Microsoft Store zu installieren, was bei Windows Autopilot zu Fehlern führt. Wenn Sie Unternehmensportal als blockierende APP während der Windows Autopilot-ESP-Bereitstellung bereitstellen, ist dieser Fehler wahrscheinlich aufgetreten.
- Einem Benutzer werden keine Administratorrechte im Windows Autopilot-Szenario für das benutzergesteuerte Azure AD Hybrid beitreten erteilt. Dies ist ein weiteres nicht englischsprachiges Betriebssystem Problem.
<td>Laden Sie das <a href="https://support.microsoft.com/help/4505903">KB4505903 Update</a>herunter, und installieren Sie es. <br><br>Informationen zu bestimmten releasekanälen, die Sie zum Abrufen des Updates verwenden können, finden Sie im Abschnitt: Abrufen <b>dieses Updates</b> .
<tr><td>Der Modus für die <a href="self-deploying.md">selbst</a> Bereitstellung von Windows Autopilot schlägt mit einem Fehlercode fehl:
<td><table>
<tr><td>0x800705B4<td>Dies ist ein allgemeiner Fehler, der einen Timeout angibt. Eine häufige Ursache für diesen Fehler im selbst Bereitstellungs Modus besteht darin, dass das Gerät nicht TPM 2,0-fähig ist (z.: ein virtueller Computer). Geräte, die nicht über TPM 2,0-fähig sind, können nicht mit dem selbst Bereitstellungs Modus verwendet werden.
<tr><td>0x801c03ea<td>Dieser Fehler weist darauf hin, dass der TPM-Nachweis fehlgeschlagen ist, was dazu führt, dass Azure Active Directory mit einem Geräte Token nicht verknüpft wird.
<tr><td>0xc1036501<td>Das Gerät kann keine automatische MDM-Registrierung durchführen, da in Azure AD mehrere MDM-Konfigurationen vorhanden sind. Siehe <a href="https://oofhours.com/2019/10/01/inside-windows-autopilot-self-deploying-mode/">im selbstbereitstellungs Modus von Windows Autopilot</a>.
</table>
<tr><td>Weißer Handschuh gibt einen roten Bildschirm an, und das Ereignisprotokoll " <b>Microsoft-Windows-Benutzer Geräteregistrierung/admin</b> " zeigt den <b>HRESULT-Fehlercode 0x801c03f</b><td>Dieses Problem kann auftreten, wenn Azure AD für das Gerät, das Sie bereitstellen möchten, kein Azure AD Geräte Objekt finden kann. Dieses Problem tritt auf, wenn Sie das Objekt manuell löschen. Um dieses Problem zu beheben, entfernen Sie das Gerät aus Azure AD, InTune und Autopilot, und registrieren Sie es anschließend bei Autopilot, wodurch das Azure AD Device-Objekt neu erstellt wird.<br> 
<br>Verwenden Sie zum Abrufen von Problem Behandlungsprotokollen: <b>Mdmdiagnosticstool.exe-Area Autopilot; TPM-CAB-c:\autopilot.cab</b>
<tr><td>Weißer Handschuh gibt einen roten Bildschirm an<td>Ein weißer Handschuh wird auf einem virtuellen Computer nicht unterstützt.
<tr><td>Fehler beim Importieren von Windows Autopilot-Geräten aus einer CSV-Datei.<td>Stellen Sie sicher, dass Sie die CSV-Datei in Microsoft Excel oder einem anderen Editor als Notepad nicht bearbeitet haben. Einige dieser Editoren können zusätzliche Zeichen enthalten, wodurch das Dateiformat ungültig wird. 
<tr><td>Windows Autopilot für vorhandene Geräte folgt nicht der Autopilot OOBE-Darstellung.<td>Stellen Sie sicher, dass die JSON-Profil Datei im <b>ANSI/ASCII-</b> Format (nicht in Unicode oder UTF-8) gespeichert wird.
<tr><td>Während des OOBE-Elements wird eine <b>Fehler</b> hafte Seite angezeigt.<td>Der Client kann wahrscheinlich nicht auf alle erforderlichen Azure AD/MSA-bezogenen URLs zugreifen. Weitere Informationen finden Sie unter [Netzwerk Anforderungen](networking-requirements.md).
<tr><td>Die Verwendung eines Bereitstellungs Pakets in Verbindung mit Windows Autopilot kann zu Problemen führen, insbesondere dann, wenn das ppkg Informationen zu Join, Registrierung oder Gerätename enthält.<td>Das Verwenden von ppkgs in Kombination mit Windows Autopilot ist nicht empfehlenswert.
</table>

## <a name="related-topics"></a>Zugehörige Themen

[Diagnostizieren von MDM-Fehlern in Windows 10](https://docs.microsoft.com/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10)<br>
[Problembehandlung bei Windows Autopilot](troubleshooting.md)
