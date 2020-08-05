---
title: Problembehandlung bei Windows Autopilot
description: Erfahren Sie, wie Sie Probleme behandeln, die während des Windows Autopilot-Bereitstellungs Prozesses auftreten.
keywords: MDM, Setup, Windows, Windows 10, OOBE, Manage, Bereitstellung, Autopilot, ZTD, Zero-Touchscreen, Partner, msfb, InTune
ms.reviewer: mniehaus
manager: laurawi
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
ms.openlocfilehash: a15de87dc657fb9ee819fd303bc50a4e7a792623
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/04/2020
ms.locfileid: "87756548"
---
# <a name="troubleshooting-windows-autopilot"></a>Problembehandlung bei Windows Autopilot

**Gilt für: Windows 10**

Windows Autopilot ist so konzipiert, dass alle Teile des Windows-Geräte Lebenszyklus vereinfacht werden, aber es gibt immer Situationen, in denen Probleme auftreten können.  Überprüfen Sie die folgenden Informationen, um die Problembehandlung zu unterstützen.

## <a name="troubleshooting-process"></a>Prozess zur Problembehandlung

Unabhängig davon, ob Sie benutzergesteuerte oder selbst bereitgestellte Geräte Bereitstellungen durchführen, ist der Problem Behandlungsprozess ungefähr identisch.  Es ist immer sinnvoll, den Flow für ein bestimmtes Gerät zu verstehen:

- Eine Netzwerkverbindung wird hergestellt.  Bei der Verbindung kann es sich um eine drahtlos Verbindung (Wi-Fi) oder eine verkabelte Verbindung (Ethernet) handeln.
- Das Windows Autopilot-Profil wird heruntergeladen. Wenn Sie eine kabelgebundene Verbindung verwenden oder eine drahtlose Verbindung manuell herstellen, wird das Windows Autopilot-Profil aus dem Autopilot-Bereitstellungs Dienst heruntergeladen, sobald die Netzwerkverbindung hergestellt ist.
- Die Benutzerauthentifizierung erfolgt.  Wenn eine benutzergesteuerte Bereitstellung durchgeführt wird, gibt der Benutzer seine Azure Active Directory Anmelde Informationen ein, die überprüft werden.
- Azure Active Directory Join.  Bei benutzergesteuerten bereit Stellungen wird das Gerät mit Azure AD mithilfe der angegebenen Benutzer Anmelde Informationen verknüpft.  Bei selbst Bereitstellungs Szenarien wird das Gerät ohne Angabe von Benutzer Anmelde Informationen verknüpft.
- Die automatische MDM-Registrierung erfolgt.  Im Rahmen des Azure AD Join-Prozesses wird das Gerät in den in Azure AD konfigurierten MDM-Dienst registriert (z. b. Microsoft InTune).
- Einstellungen werden angewendet.  Wenn die [Seite](enrollment-status.md) Anmeldungs Status konfiguriert ist, werden die meisten Einstellungen angewendet, während die Seite Registrierungsstatus angezeigt wird.  Wenn diese nicht konfiguriert oder verfügbar sind, werden die Einstellungen nach der Anmeldung des Benutzers angewendet.

Für die Problembehandlung sind folgende wichtige Aktivitäten auszuführen:

- Konfiguration: verfügt über Azure Active Directory und Microsoft InTune (oder einen entsprechenden MDM-Dienst) gemäß den [Windows Autopilot-Konfigurations Anforderungen](windows-autopilot-requirements.md)konfiguriert?
- Netzwerk Konnektivität: kann das Gerät auf die in den [Windows Autopilot-Netzwerk Anforderungen](windows-autopilot-requirements.md)beschriebenen Dienste zugreifen?
- Standardverhalten von Autopilot (OOBE): Es wurden nur die erwarteten Standard-Erfahrungs Bildschirme angezeigt?  Wurde die Seite mit den Azure AD Anmelde Informationen erwartungsgemäß mit organisationsspezifischen Details angepasst?
- Azure AD joinprobleme: war das Gerät in der Lage, Azure Active Directory beizutreten?
- MDM-Registrierungsprobleme: war das Gerät in der Lage, sich bei Microsoft InTune (oder einem entsprechenden MDM-Dienst) anzumelden?

## <a name="troubleshooting-autopilot-device-import"></a>Problembehandlung bei Autopilot-Geräte Import

### <a name="clicking-import-after-selecting-csv-does-nothing-400-error-appears-in-network-trace-with-error-body-cannot-convert-the-literal-devicehash-to-the-expected-type-edmbinary"></a>Wenn Sie auf "Importieren" klicken, nachdem Sie CSV ausgewählt haben, wird der Fehler "400" in der Netzwerk Ablauf Verfolgung mit dem Fehlertext **"das Literale" [devicehash] "kann nicht in den erwarteten Typ" EDM. Binary "konvertiert werden.**

Dieser Fehler zeigt an, dass der Geräte Hash falsch formatiert ist. Dieser Fehler kann dadurch verursacht werden, dass der gesammelte Hash beschädigt wird. eine Möglichkeit besteht darin, dass der Hash selbst (auch wenn er vollständig gültig ist) nicht decodiert werden kann.

Der Geräte Hash ist Base64. Auf Geräteebene wird Sie als nicht aufgefüllte Base64-Datei codiert, Autopilot erwartet aber eine hoch gefüllte base64. In den meisten Fällen erfordert die Nutzlast keine Auffüll Vorgänge, und der Prozess funktioniert. Manchmal ist die Nutzlast jedoch nicht ordnungsgemäß, und Auffüllung ist erforderlich. Dies ist der Fall, wenn Sie den oben angezeigten Fehler erhalten. Der Base64-Decoder von PowerShell erwartet auch das Auffüllen von Base64, damit wir mithilfe dieses Decoders überprüfen können, ob der Hash ordnungsgemäß aufgefüllt ist.

Die "A"-Zeichen am Ende des Hashs sind tatsächlich leere Daten. jedes Zeichen in Base64 ist 6 Bit, ein in Base64 ist 6 Bits gleich 0 (null). Das Löschen oder **Hinzufügen von am**Ende ändert nicht die tatsächlichen Nutzlastdaten.

Um dieses Problem zu beheben, müssen wir den Hash ändern und dann den neuen Wert testen, bis PowerShell erfolgreich den Hash decodiert. Das Ergebnis ist größtenteils nicht lesbar, das ist in Ordnung. Wir suchen nur nach dem Fehler "ungültige Länge für ein Base-64 Char-Array oder eine Zeichenfolge". 

Zum Testen des Base64 können Sie Folgendes verwenden:
```powershell
[System.Text.Encoding]::ascii.getstring( [System.Convert]::FromBase64String("DEVICE HASH"))
```

Als Beispiel (Dies ist kein Geräte Hash, aber es ist falsch ausgerichtet, nicht ausgefülltes Base64, sodass es für Tests geeignet ist):
```powershell
[System.Text.Encoding]::ascii.getstring( [System.Convert]::FromBase64String("Q29udG9zbwAAA"))
```

Jetzt für die Auffüll Regeln. Das Auffüll Zeichen ist "=". Das Auffüll Zeichen darf nur am Ende des Hashs liegen, und es dürfen maximal zwei Auffüll Zeichen vorhanden sein. Hier ist die grundlegende Logik.

- Schlägt die Decodierung des Hashs fehl?
  - Ja: sind die letzten zwei Zeichen "="?
     - Ja: Ersetzen Sie "=" durch ein einzelnes "a"-Zeichen, und wiederholen Sie dann den Vorgang.
     - Nein: Fügen Sie am Ende ein weiteres Zeichen "=" ein, und wiederholen Sie dann den Vorgang.
  - Nein: dieser Hash ist gültig.

Wenn Sie die Logik oben im vorherigen Beispiel Hash Schleifen, werden die folgenden Permutationen angezeigt:
- Q29udG9zbwAAA
- Q29udG9zbwAAA =
- Q29udG9zbwAAA = =
- Q29udG9zbwAAAA
- Q29udG9zbwAAAA =
- **Q29udG9zbwAAAA = =** (dieses hat eine gültige Auffüll Zeichen)

Ersetzen Sie den gesammelten Hash durch diesen neuen ausgefülltem Hash, und wiederholen Sie dann den Import Vorgang.

## <a name="troubleshooting-autopilot-oobe-issues"></a>Problembehandlung bei Autopilot OOBE-Problemen

Wenn das erwartete Autopilot-Verhalten nicht während des OOBE-Verhaltens auftritt, ist es hilfreich zu sehen, ob das Gerät ein Autopilot-Profil empfangen hat und welche Einstellungen dieses Profil enthielt.  Abhängig von der Windows 10-Version sind verschiedene Mechanismen verfügbar.

### <a name="windows-10-version-1803-and-above"></a>Windows 10, Version 1803 und höher

Um Details im Zusammenhang mit den Autopilot-Profileinstellungen und dem OOBE-Flow anzuzeigen, fügt Windows 10, Version 1803 und höher, Ereignisprotokoll Einträge hinzu.  Diese können mit Ereignisanzeige angezeigt werden. Lesen Sie die Informationen unter **Anwendungs-und Dienst Protokolle – > Microsoft – > Windows – > Provisioning-Diagnostics-Provider – > Autopilot** für Versionen vor 1903. Informationen zu den Versionen 1903 und höher finden Sie unter **Anwendungs-und Dienst Protokolle – > Microsoft – > Windows – > moderndeployment-Diagnostics-Provider – > Autopilot**.  Je nach Szenario und Profil Konfiguration können die folgenden Ereignisse aufgezeichnet werden:

| Ereignis-ID | type | BESCHREIBUNG |
|----------|------|-------------| 
| 100 | Warnung | "Die Autopilot-Richtlinie [Name] wurde nicht gefunden."  Dieser Fehler ist in der Regel ein vorübergehendes Problem, während das Gerät darauf wartet, dass ein Autopilot-Profil heruntergeladen wird. |
| 101 | Info | "Autopilotgetpolicydwordbyname war erfolgreich: Richtlinien Name = [Einstellungs Name]; Richtlinien Wert = [Wert]. "  Diese Meldung zeigt Autopilot zum Abrufen und verarbeiten numerischer OOBE-Einstellungen. |
| 103 | Info | "Autopilotgetpolicystringbyname erfolgreich: Richtlinien Name = [Name]; Wert = [Wert]. "  Diese Meldung zeigt Autopilot zum Abrufen und Verarbeiten von OOBE-Zeichen folgen, wie z. b. den Azure AD Mandanten Namen. |
| 109 | Info | "Autopilotgestarobesettingsoverride erfolgreich: OOBE-Einstellung [Einstellungs Name]; State = [State]. "  Diese Meldung zeigt Autopilot zum Abrufen und verarbeiten Zustands bezogener OOBE-Einstellungen. |
| 111 | Info | "Autopilotretrievesettings war erfolgreich."  Diese Meldung bedeutet, dass die im Autopilot-Profil gespeicherten Einstellungen, die das OOBE-Verhalten steuern, erfolgreich abgerufen wurden. |
| 153 | Info | "Autopilotmanager hat gemeldet, dass der Zustand von [ursprünglicher Zustand] in [neuer Zustand] geändert wurde."  In der Regel sollte diese Meldung "ProfileState_Unknown" für "ProfileState_Available" lauten, um anzuzeigen, dass ein Profil für das Gerät verfügbar und heruntergeladen wurde, damit das Gerät mithilfe von Autopilot bereitgestellt werden kann. |
| 160 | Info | "Autopilotretrievesettings beginnt mit dem Erwerb."  Diese Meldung zeigt, dass Autopilot bereit ist, die benötigten Autopilot-Profileinstellungen herunterzuladen. |
| 161 | Info | "Die Einstellungen für den automatischen automatischen Abruf von Einstellungen wurden erfolgreich abgeschlossen."  Das Autopilot-Profil wurde erfolgreich heruntergeladen. |
| 163 | Info | "Der von autopilotmanager festgelegte Download ist nicht erforderlich, und das Gerät wurde bereits bereitgestellt.  Bereinigen oder setzen Sie das Gerät zurück, um dies zu ändern. "  Diese Meldung gibt an, dass sich ein Autopilot-Profil auf dem Gerät befindet. Sie wird in der Regel nur vom **syspree/generalize** -Prozess entfernt. |
| 164 | Info | "Das von Auto-Manager festgelegte Internet ist zum Herunterladen der Richtlinie verfügbar." |
| 171 | Fehler | "Vom autopilotmanager konnte die TPM-Identität nicht bestätigt werden.  HRESULT = [Fehlercode]. "  Dies weist auf ein Problem hin, das einen TPM-Nachweis ausführt, der zum Abschluss des selbst Bereitstellungs Modus erforderlich ist. | 
| 172 | Fehler | "Autopilotmanager konnte das Autopilot-Profil nicht als verfügbar festlegen.  HRESULT = [Fehlercode]. "  Dieser Fehler bezieht sich in der Regel auf die Ereignis-ID 171. |

Zusätzlich zu den Ereignisprotokoll Einträgen funktionieren die unten beschriebenen Registrierungs-und etw-Ablauf Verfolgungs Optionen auch mit Windows 10, Version 1803 und höher.

### <a name="windows-10-version-1709-and-above"></a>Windows 10, Version 1709 und höher

Unter Windows 10, Version 1709 und höher, werden Informationen zu den Autopilot-Profileinstellungen in der Registrierung auf dem Gerät gespeichert, nachdem Sie vom Autopilot-Bereitstellungs Dienst empfangen wurden.  Diese finden Sie unter " **hklm\software\microsoft\provisioning\diagnostics\autopilot**".  Folgende Registrierungseinträge sind verfügbar:

| Wert | BESCHREIBUNG |
|-------|-------------|
| AadTenantId | Der GUID des Azure AD Mandanten, bei dem sich der Benutzer angemeldet hat.  Dies sollte dem Mandanten entsprechen, bei dem das Gerät registriert wurde. Wenn dies nicht der Fall ist, erhält der Benutzer eine Fehlermeldung. |
| Cloudassignedtenantdomain | Der Azure AD Mandanten, bei dem das Gerät registriert wurde, z. b. "contosomn.onmicrosoft.com".  Wenn das Gerät nicht bei Autopilot registriert ist, ist dieser Wert leer. |
| Cloudassignedtenantid | Die GUID des Azure AD Mandanten, bei dem das Gerät registriert wurde (die GUID entspricht der Mandanten Domäne aus dem Registrierungs Wert "cloudassignedtenantdomain").  Wenn das Gerät nicht bei Autopilot registriert ist, ist dieser Wert leer.|
| Isautopilotdeaktiviert | Wenn der Wert auf 1 festgelegt ist, weist dies darauf hin, dass das Gerät nicht bei Autopilot registriert ist.  Dies kann auch darauf hindeuten, dass das Autopilot-Profil aufgrund von Netzwerk Konnektivität oder Firewallproblemen oder Netzwerk Timeouts nicht heruntergeladen werden konnte. |
| Tenantmatching | Dieser Wert wird auf 1 festgelegt, wenn die Mandanten-ID des Benutzers mit der Mandanten-ID übereinstimmt, bei der das Gerät registriert wurde.  Wenn der Wert 0 ist, wird dem Benutzer ein Fehler angezeigt, und es wird ein Neustart erzwungen. |
| Cloudassignetdoobeconfig | Dies ist eine Bitmap, die anzeigt, welche Autopilot-Einstellungen konfiguriert wurden.  Folgende Werte sind verfügbar: skipcortanaoptin = 1, oobeusernotlocaladmin = 2, skipexpress Settings = 4, skipoemregistration = 8, skipep = 16 |

### <a name="windows-10-semi-annual-channel-supported-versions"></a>Unterstützte Versionen von halbjährlichen Kanälen in Windows 10

Auf Geräten, auf denen eine [unterstützte Version](https://docs.microsoft.com/windows/release-information/) des halbjährlichen Kanals von Windows 10 ausgeführt wird, kann die ETW-Ablauf Verfolgung verwendet werden, um ausführliche Informationen von Autopilot und zugehörigen Komponenten zu erfassen.  Die sich ergebenden etw-Ablauf Verfolgungs Dateien können dann mithilfe von Windows Performance Analyzer oder ähnlichen Tools angezeigt werden.  Weitere Informationen finden Sie [im Blog zur erweiterten Problem](https://blogs.technet.microsoft.com/mniehaus/2017/12/13/troubleshooting-windows-autopilot-level-300400/) Behandlung.

## <a name="troubleshooting-azure-ad-join-issues"></a>Problembehandlung bei Azure AD Verknüpfungs Problemen

Das häufigste Problem bei der Verbindung zwischen einem Gerät und Azure AD bezieht sich auf Azure AD Berechtigungen.  Stellen Sie sicher, dass [die richtige Konfiguration vorhanden ist](windows-autopilot-requirements.md) , damit Benutzer Geräte zu Azure AD hinzufügen können.  Fehler können auch auftreten, wenn der Benutzer die Anzahl der Geräte überschritten hat, denen Sie beitreten dürfen, wie in Azure AD konfiguriert.

Beim Importieren wird ein Azure AD Gerät erstellt. es ist wichtig, dass dieses Objekt nicht gelöscht wird. Er dient als Autopilot-Anker in Aad für die Gruppenmitgliedschaft und das Ziel (einschließlich des Profils) und kann zu joinfehlern führen, wenn er gelöscht wird. Nachdem dieses Objekt gelöscht wurde, ist das Löschen und erneute Importieren dieses Autopilot-Hashs erforderlich, damit das zugeordnete Objekt neu erstellt werden kann, um das Problem zu beheben.

Fehlercode 801c0003 wird in der Regel auf einer Fehlerseite mit dem Titel "ein Fehler ist aufgetreten" angezeigt.  Dieser Fehler weist darauf hin, dass der Azure AD Join fehlgeschlagen ist.

## <a name="troubleshooting-intune-enrollment-issues"></a>Problembehandlung bei InTune-Registrierungs Problemen

Informationen zu Problemen bei der InTune-Registrierung finden Sie in [diesem Knowledge Base-Artikel](https://support.microsoft.com/help/4089533/troubleshooting-windows-device-enrollment-problems-in-microsoft-intune) .  Häufige Probleme sind falsche oder fehlende Lizenzen, die dem Benutzer zugewiesen sind, oder zu viele Geräte, die für den Benutzer registriert sind.

Der Fehlercode 80180018 wird in der Regel auf einer Fehlerseite mit dem Titel "ein Fehler ist aufgetreten" angezeigt.  Dieser Fehler bedeutet, dass die MDM-Registrierung fehlgeschlagen ist.

Wenn die Autopilot-zurück Setzung sofort fehlschlägt, tritt ein Fehler **auf. Melden Sie sich mit einem Administrator Konto an, um zu erfahren, warum und manuell zurückgesetzt**werden. Weitere Informationen finden Sie unter Problembehandlung bei [Autopilot Reset](https://docs.microsoft.com/education/windows/autopilot-reset#troubleshoot-autopilot-reset) .

## <a name="profile-download"></a>Profil Download

Wenn ein Windows 10-Gerät mit Internet Verbindung gestartet wird, wird versucht, eine Verbindung mit dem Autopilot-Dienst herzustellen und ein Autopilot-Profil herunterzuladen. Hinweis: Es ist wichtig, dass ein Profil in dieser Phase vorhanden ist, damit ein leeres Profil nicht lokal auf dem PC zwischengespeichert wird. Um das zurzeit zwischengespeicherte lokale Profil in Windows 10, Version 1803 und früher, zu entfernen, müssen Sie das Betriebssystem mithilfe von **syationp/generalize/oobe**neu generalisieren, das Betriebssystem neu installieren oder den PC neu Abbild erstellen. In Windows 10, Version 1809 und höher, können Sie ein neues Profil abrufen, indem Sie den PC neu starten.

Wenn ein Profil heruntergeladen wird, hängt von der Windows 10-Version ab, die auf dem PC ausgeführt wird. Siehe folgende Tabelle.

| Windows 10-Version | Profil Download Verhalten |
| --- | --- |
| 1709 | Das Profil wird nach der Seite "Oobe-Netzwerkverbindung" heruntergeladen. Diese Seite wird nicht angezeigt, wenn eine kabelgebundene Verbindung verwendet wird. In diesem Fall wird das Profil direkt vor dem Bildschirm EULA heruntergeladen. |
| 1803 | Das Profil wird so bald wie möglich heruntergeladen.  Wenn Sie verdrahtet ist, wird Sie zu Beginn von OOBE heruntergeladen. Wenn drahtlos, wird diese nach der Seite Netzwerkverbindung heruntergeladen. |
| 1809 | Das Profil wird so bald wie möglich heruntergeladen (identisch mit 1803) und nach jedem Neustart erneut heruntergeladen. |

Wenn Sie einen Computer während OOBE neu starten müssen:
- Drücken Sie UMSCHALT + F10, um eine Eingabeaufforderung zu öffnen.
- Geben Sie **Shutdown/r/t 0** ein, um sofort neu zu starten oder **herunterzufahren/s/t 0** , um sofort herunterzufahren.

Weitere Informationen finden Sie unter [Windows Setup-Befehlszeilenoptionen](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options).

## <a name="related-topics"></a>Zugehörige Themen

[Windows Autopilot-bekannte Probleme](known-issues.md)<br>
[Diagnostizieren von MDM-Fehlern in Windows 10](https://docs.microsoft.com/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10)<br>
