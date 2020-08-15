---
title: Benutzergesteuerte Windows Autopilot-Modus
description: Mit dem benutzergesteuerten Windows Autopilot-Modus können Sie Geräte so konfigurieren, dass Sie in einem gebrauchsfertigen Zustand bereitgestellt werden, ohne dass die IT-Mitarbeiter Hilfe benötigen.
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
ms.openlocfilehash: b2c9d3b8741fdae30b42aede8f5c7443e35d8bc7
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/15/2020
ms.locfileid: "88251959"
---
# <a name="windows-autopilot-user-driven-mode"></a>Benutzergesteuerter Modus von Windows Autopilot

**Gilt für: Windows 10, Version 1809 oder höher**

Mit dem benutzergesteuerten Modus von Windows Autopilot können Sie neue Windows 10-Geräte so konfigurieren, dass Sie automatisch von Ihrem Werkszustand in einen sofort einsatzbereiten Zustand transformiert werden. Dieser Prozess erfordert nicht, dass IT-Mitarbeiter das Gerät berühren.

Der Prozess ist einfach, damit jeder ihn Fertigstellen kann. Geräte können direkt mit einfachen Anweisungen an den Endbenutzer versendet oder an den Endbenutzer verteilt werden:

1. Entfernen Sie das Gerät, und schalten Sie es ein.
2. Wählen Sie eine Sprache (nur erforderlich, wenn mehrere Sprachen installiert sind), Gebiets Schema und Tastatur aus.
3. Verbinden Sie die Verbindung mit einem Drahtlos Netzwerk oder einem Kabelnetzwerk mit Internetzugang. Wenn Sie drahtlos verwenden, muss der Benutzer den Wi-Fi-Link einrichten. 
4. Geben Sie Ihre e-Mail-Adresse und Ihr Kennwort für Ihr Organisations Konto

Der restliche Prozess ist automatisiert, wie das Gerät:
1. Wird der Organisation beitreten.
2. Anmelden bei InTune (oder einem anderen MDM-Dienst)
3. Wird gemäß der Definition durch die Organisation konfiguriert.

Alle zusätzlichen Eingabe Aufforderungen während der Out-of-Box-Darstellung (OOBE) können unterdrückt werden. Optionen, die verfügbar sind, finden Sie unter [Konfigurieren von Autopilot-Profilen](profiles.md) .

Der benutzergesteuerte Modus von Windows Autopilot unterstützt Azure Active Directory und Hybrid Azure Active Directory verbundene Geräte. Weitere Informationen zu diesen beiden joinoptionen finden Sie unter [Was ist eine Geräte Identität](https://docs.microsoft.com/azure/active-directory/devices/overview).

Der Prozessfluss, der während des benutzergesteuerten Prozesses abgeschlossen wurde, lautet wie folgt:

1. Nach dem Herstellen einer Verbindung mit einem Netzwerk wird von dem Gerät ein Windows Autopilot-Profil heruntergeladen. Das Profil definiert die Einstellungen, die für das Gerät verwendet werden. Definieren Sie z. b. die während OOBE unterdrückten Eingabe Aufforderungen.
2. Windows 10 prüft auf kritische OOBE-Updates. Wenn Updates verfügbar sind, werden Sie automatisch installiert (bei Bedarf neu gestartet).
3. Der Benutzer wird aufgefordert, Azure Active Directory Anmelde Informationen einzugeben. Diese angepasste Benutzer Darstellung zeigt den Namen, das Logo und den Anmelde Text des Azure AD Mandanten.
4.  Das Gerät wird abhängig von den Windows Autopilot-Profileinstellungen Azure Active Directory oder Active Directory.
5. Das Gerät wird bei InTune (oder anderen konfigurierten MDM-Diensten) registriert. Abhängig von den Anforderungen Ihrer Organisation erfolgt diese Registrierung:
    - während des Azure Active Directory Join-Prozesses mithilfe der automatischen MDM-Registrierung
    - oder vor dem Active Directory Join-Prozess.
6. Wenn Sie konfiguriert ist, wird die Seite Anmeldungs [Status](enrollment-status.md) (ESP) angezeigt.
7. Nachdem die Geräte Konfigurationsaufgaben abgeschlossen sind, wird der Benutzer mit den zuvor bereitgestellten Anmelde Informationen bei Windows 10 angemeldet. (Wenn das Gerät im ESP-Prozess des Geräts neu gestartet wird, muss der Benutzer seine Anmelde Informationen erneut eingeben, da diese Details nicht über Neustarts hinweg beibehalten werden.)
8. Nach der Anmeldung wird die Seite Registrierungsstatus für benutzerorientierte Konfigurations Tasks angezeigt.

Wenn während dieses Vorgangs Probleme auftreten, finden Sie weitere Informationen in der Dokumentation zur [Windows Autopilot-Problem](troubleshooting.md) Behandlung.

Weitere Informationen zu den verfügbaren joinoptionen finden Sie in den folgenden Abschnitten:

- [Azure Active Directory Join](#user-driven-mode-for-azure-active-directory-join) ist verfügbar, wenn Geräte nicht zu einer lokalen Active Directory Domäne hinzugefügt werden müssen.
- [Hybrid Azure Active Directory Join](#user-driven-mode-for-hybrid-azure-active-directory-join) ist für Geräte verfügbar, die mit Azure Active Directory und ihrer lokalen Active Directory Domäne verknüpft werden müssen.

## <a name="user-driven-mode-for-azure-active-directory-join"></a>Benutzergesteuerte Modus für Azure Active Directory Join

Um eine benutzergesteuerte Bereitstellung mit Windows Autopilot abzuschließen, führen Sie die folgenden Vorbereitungsschritte aus:

1. Stellen Sie sicher, dass die Benutzer, die bereit Stellungen im benutzergesteuerten Modus durchführen werden, Geräte zu Azure Active Directory hinzufügen können. Weitere Informationen finden Sie unter [Konfigurieren von Geräteeinstellungen](https://docs.microsoft.com/azure/active-directory/device-management-azure-portal#configure-device-settings) in der Azure Active Directory-Dokumentation.
2. Erstellen Sie ein Autopilot-Profil für den benutzergesteuerten Modus mit den gewünschten Einstellungen. In Microsoft InTune wird dieser Modus explizit ausgewählt, wenn das Profil erstellt wird. Bei der Microsoft Store für Unternehmen und Partner Center ist der benutzergesteuerte Modus die Standardeinstellung und muss nicht ausgewählt werden.
3. Wenn Sie InTune verwenden, erstellen Sie eine Gerätegruppe in Azure Active Directory, und weisen Sie dieser Gruppe das Autopilot-Profil zu.

Für jedes Gerät, das über eine benutzergesteuerte Bereitstellung bereitgestellt wird, sind diese zusätzlichen Schritte erforderlich:

- Stellen Sie sicher, dass das Gerät zu Windows Autopilot hinzugefügt wurde. Das Hinzufügen eines Geräts zu Windows Autopilot kann auf zwei Arten erfolgen:
  - Automatisch von einem OEM oder Partner zum Zeitpunkt des Kaufs des Geräts
  - Manuelle Ernte, wie unter [Hinzufügen von Geräten zu Windows Autopilot](add-devices.md)beschrieben.
- Stellen Sie sicher, dass dem Gerät ein Autopilot-Profil zugewiesen wurde:
 - Wenn Sie InTune und Azure Active Directory dynamischen Gerätegruppen verwenden, kann diese Zuweisung automatisch durchgeführt werden.
 - Wenn Sie InTune verwenden und statische Gerätegruppen Azure Active Directory, fügen Sie das Gerät manuell der Gerätegruppe hinzu.
 - Wenn Sie andere Methoden verwenden (z. b. Microsoft Store für Business oder Partner Center), weisen Sie dem Gerät manuell ein Autopilot-Profil zu.


## <a name="user-driven-mode-for-hybrid-azure-active-directory-join"></a>Benutzergesteuerte Modus für Hybrid Azure Active Directory Join

Windows Autopilot erfordert, dass Geräte Azure Active Directory verknüpft sind. Wenn Sie über eine lokale Active Directory Umgebung verfügen, können Sie Geräte zu Ihrer lokalen Domäne hinzufügen. Um den Geräten beizutreten, müssen Sie Autopilot-Geräte so konfigurieren, dass Sie [mit Azure Active Directory (Azure AD) Hybrid](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)verknüpft werden. 

### <a name="requirements"></a>Anforderungen

So führen Sie eine benutzergesteuerte Bereitstellung mit Hybrid Azure AD mithilfe von Windows Autopilot durch:

- Ein Windows Autopilot-Profil für den benutzergesteuerten Modus muss erstellt werden. 
 - **Azure AD Hybrid** verknüpft muss als die ausgewählte Option unter **Join to Azure AD as** in the Autopilot Profile angegeben werden.
- Wenn Sie InTune verwenden, muss eine Gerätegruppe in Azure Active Directory mit dem Windows Autopilot-Profil vorhanden sein, das dieser Gruppe zugewiesen ist.
- Auf dem Gerät muss Windows 10, Version 1809 oder höher, ausgeführt werden.
- Das Gerät muss Zugriff auf einen Active Directory Domänen Controller haben. Es muss mit dem Netzwerk der Organisation verbunden sein. Sie muss in der Lage sein, die DNS-Einträge für die AD-Domäne und den AD-Domänen Controller aufzulösen. Sie muss in der Lage sein, mit dem Domänen Controller zu kommunizieren, um den Benutzer zu authentifizieren.
- Das Gerät muss auf das Internet zugreifen können, und zwar gemäß den [dokumentierten Netzwerk Anforderungen für Windows Autopilot](networking-requirements.md).
- Der InTune-Connector für Active Directory muss installiert sein.
 - Hinweis: der InTune-Connector führt einen lokalen AD Join aus. Daher benötigen Benutzer keine lokale Ad-Join-Berechtigung. Dabei wird davon ausgegangen, dass der Connector so konfiguriert ist, dass er [Diese Aktion](https://docs.microsoft.com/intune/windows-autopilot-hybrid#increase-the-computer-account-limit-in-the-organizational-unit) im Auftrag des Benutzers ausführt. 
- Bei Verwendung eines Proxys müssen WPAD-Proxyeinstellungen aktiviert und konfiguriert sein.

**Azure AD Geräte**Verknüpfung: der Hybrid Azure AD Join-Prozess verwendet den Systemkontext, um die Geräte Azure AD beitreten auszuführen. Dies ist nicht von den Einstellungen der benutzerbasierten Azure AD Join-Berechtigung betroffen. Alle Benutzer können Geräte standardmäßig Azure AD hinzufügen.

## <a name="user-driven-mode-for-hybrid-azure-active-directory-join-with-vpn-support"></a>Der benutzergesteuerte Modus für Hybrid Azure Active Directory Join mit VPN-Unterstützung

Geräte, die mit Active Directory verknüpft sind, benötigen für viele Aktivitäten eine Verbindung mit einem Active Directory Domänen Controller. Zu diesen Aktivitäten gehören die Benutzeranmeldung (Überprüfung der Anmelde Informationen des Benutzers) und die Gruppenrichtlinie Anwendung. Daher würde der benutzergesteuerte Windows Autopilot-Azure AD Hybrid Join Prozess überprüfen, ob das Gerät einen Active Directory Domänen Controller kontaktieren kann, indem er diesen Domänen Controller anhefteter.

Durch das Hinzufügen von VPN-Unterstützung für dieses Szenario können Sie den Azure AD Hybrid Join Prozess so konfigurieren, dass die Konnektivitätsüberprüfung übersprungen wird. Dadurch entfällt die Notwendigkeit, mit einem Active Directory Domänen Controller zu kommunizieren. Um die Verbindung zum Unternehmensnetzwerk zuzulassen, stellt InTune stattdessen die erforderliche VPN-Konfiguration bereit, bevor der Benutzer versucht, sich bei Windows anzumelden. 


### <a name="requirements"></a>Anforderungen

Die folgenden zusätzlichen Anforderungen gelten für Azure AD Hybrid Join mit VPN-Unterstützung:

- Eine unterstützte Version von Windows 10:
 - Kumulatives Update für Windows 10 1903 + Dezember 10 (KB4530684, OS Build 18362,535) oder höher 
 - Kumulatives Update für Windows 10 1909 + Dezember 10 (KB4530684, OS Build 18363,535) oder höher 
 - Windows 10 2004 oder höher 
- Aktivieren Sie im Azure AD Hybrid Join Autopilot-Profil die neue Option "Überprüfung der Domänen Konnektivität überspringen".
- Eine VPN-Konfiguration:
  - kann mit InTune bereitgestellt werden und ermöglicht dem Benutzer, eine VPN-Verbindung über den Windows-Anmeldebildschirm manuell herzustellen, oder
  - eine, die bei Bedarf automatisch eine VPN-Verbindung herstellt. 

Welche VPN-Konfiguration erforderlich ist, hängt von der verwendeten VPN-Software und der verwendeten Authentifizierung ab. Bei VPN-Lösungen von Drittanbietern (nicht von Microsoft) ist dies in der Regel die Bereitstellung einer Win32-app (mit der VPN-Client Software selbst und aller speziellen Verbindungsinformationen, z. b. VPN-Endpunkt Hostnamen) über InTune-Verwaltungs Erweiterungen. Informationen zu den für diesen anbieterspezifischen Konfigurationsdetails finden Sie in der Dokumentation des VPN-Anbieters.

> [!NOTE]
> Die VPN-Anforderungen sind nicht spezifisch für Windows Autopilot. Wenn Sie z. b. bereits eine VPN-Konfiguration implementiert haben, die das Zurücksetzen von Remote Kennwörtern ermöglicht, wenn sich ein Benutzer bei Windows mit einem neuen Kennwort anmelden muss, wenn er nicht im Netzwerk der Organisation vorhanden ist, kann dieselbe Konfiguration mit Windows Autopilot verwendet werden. Nachdem sich der Benutzer angemeldet hat, um seine Anmelde Informationen zwischenzuspeichern, benötigen nachfolgende Anmeldeversuche keine Konnektivität, da die zwischengespeicherten Anmelde Informationen verwendet werden können. 

In Fällen, in denen die Zertifikat Authentifizierung für die VPN-Software erforderlich ist, sollte das erforderliche Computer Zertifikat auch über InTune bereitgestellt werden. Diese Bereitstellung kann mithilfe der InTune-Zertifikat Registrierungsfunktionen erfolgen, die die Zertifikat Profile für das Gerät als Ziel verwenden.

Benutzerzertifikate werden nicht unterstützt, da Sie erst bereitgestellt werden können, wenn sich der Benutzer anmeldet. Da Sie erst nach der Benutzeranmeldung installiert werden, werden nicht von Microsoft unterstützte UWP-VPN-Plug-ins, die aus dem Windows Store übermittelt werden, nicht unterstützt.

### <a name="validation"></a>Überprüfen

Bevor Sie versuchen, einen Hybrid Azure AD Join per VPN zu verwenden, ist es wichtig zu bestätigen, dass ein Benutzer gesteuAzure AD Hybrid Join Prozess im Netzwerk der Organisation ausgeführt werden kann. Diese Bestätigung vereinfacht die Problembehandlung, indem sichergestellt wird, dass der Hauptprozess funktioniert, bevor die zusätzliche VPN-Konfiguration erforderlich wird.

Überprüfen Sie als nächstes, ob die VPN-Konfiguration (Win32-APP, certs und andere Anforderungen) mithilfe von InTune für ein vorhandenes Gerät bereitgestellt werden können, das bereits Hybrid Azure AD verknüpft ist. Einige VPN-Clients erstellen z. b. eine Computer spezifische VPN-Verbindung im Rahmen des Installationsvorgangs. Daher können Sie die Konfiguration überprüfen, indem Sie folgende Schritte ausführen:

- Überprüfen Sie in PowerShell, ob mindestens eine Computer spezifische VPN-Verbindung mit dem Befehl "Get-VPNconnection-alluserconnection" erstellt wurde.
- Versuchen Sie, die VPN-Verbindung mit dem folgenden Befehl manuell zu starten: RASDIAL.EXE "ConnectionName"
- Melden Sie sich ab, und überprüfen Sie, ob auf der Windows-Anmeldeseite das Symbol "VPN-Verbindung" angezeigt wird.
- Verschieben Sie das Gerät aus dem Unternehmensnetzwerk, und versuchen Sie, die Verbindung mithilfe des Symbols auf der Windows-Anmeldeseite herzustellen. Melden Sie sich bei einem Konto an, das keine zwischengespeicherten Anmelde Informationen enthält

Bei VPN-Konfigurationen, die automatisch eine Verbindung herstellen, können sich die Validierungs Schritte unterscheiden.

> [!NOTE]
> Always on-VPN kann für dieses Szenario verwendet werden. Weitere Informationen finden Sie in der Dokumentation zum Bereitstellen von [Always on-VPN](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy-deployment) . Beachten Sie, dass InTune das erforderliche Computer spezifische VPN-Profil noch nicht bereitstellen kann. 

Stellen Sie sicher, dass das erforderliche kumulative Windows 10-Update unter Windows 10 1903 oder Windows 10 1909 installiert wurde, um den Prozess zu überprüfen. Sie können das Update während des OOBE-Vorgangs manuell installieren, indem Sie zuerst den aktuellen kumulativen aus herunterladen https://catalog.update.microsoft.com . Folgen Sie diesen Schritten:

1. Drücken Sie UMSCHALT + F10, um eine Eingabeaufforderung zu öffnen.
2. Fügen Sie einen USB-Schlüssel mit dem heruntergeladenen Update ein.
3. Installieren Sie das Update mit dem Befehl (durch den tatsächlichen Dateinamen): WUSA.EXE <filename> . msu/quiet
4. Starten Sie den Computer mit dem folgenden Befehl neu: shutdown.exe/r/t 0

Oder Sie können Windows Update starten, um die neuesten Updates zu installieren:

1. Drücken Sie UMSCHALT + F10, um eine Eingabeaufforderung zu öffnen.
2. Führen Sie den Befehl "Start MS-Settings:" aus.
3. Navigieren Sie zum Knoten "& Sicherheit aktualisieren", und suchen Sie nach Updates.
4. Neustart nach der Installation der Updates.

### <a name="step-by-step-instructions"></a>Schrittweise Anweisungen

Weitere Informationen finden Sie unter Bereitstellen von [Hybrid Azure AD verbundenen Geräten mit InTune und Windows Autopilot](https://docs.microsoft.com/intune/windows-autopilot-hybrid).



