---
title: Benutzergesteuerte Windows Autopilot-Modus
description: Der benutzergesteuerte Modus von Windows Autopilot ermöglicht die Bereitstellung von Geräten in einem gebrauchsfertigen Zustand, ohne dass Hilfe von IT-Mitarbeitern erforderlich ist.
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
ms.openlocfilehash: b5e7c88272f8da386d25e7e7bca1973026f4407a
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/04/2020
ms.locfileid: "87756536"
---
# <a name="windows-autopilot-user-driven-mode"></a>Benutzergesteuerter Modus von Windows Autopilot

**Gilt für: Windows 10, Version 1809 oder höher**

Der benutzergesteuerte Modus von Windows Autopilot ist so konzipiert, dass neue Windows 10-Geräte von Ihrem anfänglichen Factory-Zustand in einen gebrauchsfertigen Zustand transformiert werden können, ohne dass die IT-Mitarbeiter das Gerät jemals kontaktieren müssen.  Der Prozess ist so konzipiert, dass er einfach ist, damit jeder ihn Fertigstellen kann, sodass Geräte direkt mit einfachen Anweisungen an den Endbenutzer gesendet oder an den Endbenutzer verteilt werden können:

- Entfernen Sie das Gerät, und schalten Sie es ein.
- Wählen Sie eine Sprache (nur erforderlich, wenn mehrere Sprachen installiert sind), Gebiets Schema und Tastatur aus.
- Verbinden Sie die Verbindung mit einem Drahtlos Netzwerk oder einem Kabelnetzwerk mit Internetzugang.  Wenn Sie drahtlos verwenden, muss der Benutzer den Wi-Fi-Link einrichten.  
- Geben Sie Ihre e-Mail-Adresse und Ihr Kennwort für Ihr Organisations Konto

Nachdem Sie diese einfachen Schritte durchgeführt haben, wird der restliche Prozess automatisiert, wobei das Gerät der Organisation hinzugefügt, bei InTune (oder einem anderen MDM-Dienst) registriert und gemäß der Definition durch die Organisation vollständig konfiguriert ist.  Alle zusätzlichen Eingabe Aufforderungen während der Out-of-Box-Darstellung (OOBE) können unterdrückt werden. Optionen, die verfügbar sind, finden Sie unter [Konfigurieren von Autopilot-Profilen](profiles.md) .

Der benutzergesteuerte Modus von Windows Autopilot unterstützt Azure Active Directory und Hybrid Azure Active Directory verbundene Geräte.  Weitere Informationen zu diesen beiden joinoptionen finden Sie unter [Was ist eine Geräte Identität](https://docs.microsoft.com/azure/active-directory/devices/overview).

Aus der Perspektive des Prozess Flusses sind die Aufgaben, die während des benutzergesteuerten Prozesses ausgeführt werden, wie folgt:

- Nachdem eine Verbindung mit einem Netzwerk hergestellt wurde, lädt das Gerät ein Windows Autopilot-Profil herunter, das die zu verwendenden Einstellungen angibt (z. b. die Eingabe Aufforderungen während der OOBE, die unterdrückt werden sollen).
- Windows 10 prüft auf kritische OOBE-Updates. Wenn Updates verfügbar sind, werden Sie automatisch installiert (bei Bedarf neu gestartet).
- Der Benutzer wird zur Eingabe Azure Active Directory Anmelde Informationen aufgefordert, und es wird eine angepasste Benutzer Darstellung mit dem Namen des Azure AD Mandanten, dem Logo und dem Anmelde Text angezeigt.
- Das Gerät wird basierend auf den Windows Autopilot-Profileinstellungen Azure Active Directory oder Active Directory beitreten.
- Das Gerät wird bei InTune (oder anderen konfigurierten MDM-Diensten) registriert.  (Diese Registrierung erfolgt im Rahmen des Azure Active Directory Join-Prozesses über die automatische MDM-Registrierung oder vor dem Active Directory joinprozess.)
- Wenn Sie konfiguriert ist, wird die Seite Anmeldungs [Status](enrollment-status.md) (ESP) angezeigt.
- Nachdem die Geräte Konfigurationsaufgaben abgeschlossen sind, wird der Benutzer mit den zuvor bereitgestellten Anmelde Informationen bei Windows 10 angemeldet.  (Hinweis: Wenn das Gerät während des Geräte-ESP-Prozesses neu gestartet wird, muss der Benutzer seine Anmelde Informationen erneut eingeben, da diese Details nicht über Neustarts hinweg beibehalten werden.)
- Nachdem Sie sich angemeldet haben, wird die Seite Anmeldungs Status erneut für benutzerorientierte Konfigurations Tasks angezeigt.

Wenn während dieses Vorgangs Probleme auftreten, finden Sie weitere Informationen in der Dokumentation zur [Windows Autopilot-Problem](troubleshooting.md) Behandlung.

Weitere Informationen zu den verfügbaren joinoptionen finden Sie in den folgenden Abschnitten:

- [Azure Active Directory Join](#user-driven-mode-for-azure-active-directory-join) ist verfügbar, wenn Geräte nicht zu einer lokalen Active Directory Domäne hinzugefügt werden müssen.
- [Hybrid Azure Active Directory Join](#user-driven-mode-for-hybrid-azure-active-directory-join) ist für Geräte verfügbar, die mit Azure Active Directory und ihrer lokalen Active Directory Domäne verknüpft werden müssen.

## <a name="user-driven-mode-for-azure-active-directory-join"></a>Benutzergesteuerte Modus für Azure Active Directory Join

Um eine benutzergesteuerte Bereitstellung mit Windows Autopilot auszuführen, müssen die folgenden Vorbereitungsschritte ausgeführt werden:

- Stellen Sie sicher, dass die Benutzer, die die bereit Stellungen im benutzergesteuerten Modus durchführen werden, Geräte zu Azure Active Directory hinzufügen können.  Weitere Informationen finden Sie unter [Konfigurieren von Geräteeinstellungen](https://docs.microsoft.com/azure/active-directory/device-management-azure-portal#configure-device-settings) in der Azure Active Directory-Dokumentation.
- Erstellen Sie ein Autopilot-Profil für den benutzergesteuerten Modus mit den gewünschten Einstellungen.  In Microsoft InTune wird dieser Modus explizit ausgewählt, wenn das Profil erstellt wird. Bei der Microsoft Store für Unternehmen und Partner Center ist der benutzergesteuerte Modus die Standardeinstellung und muss nicht ausgewählt werden.
- Wenn Sie InTune verwenden, erstellen Sie eine Gerätegruppe in Azure Active Directory, und weisen Sie dieser Gruppe das Autopilot-Profil zu.

Für jedes Gerät, das über eine benutzergesteuerte Bereitstellung bereitgestellt wird, sind diese zusätzlichen Schritte erforderlich:

- Stellen Sie sicher, dass das Gerät zu Windows Autopilot hinzugefügt wurde.  Diese Addition kann automatisch von einem OEM oder Partner zu dem Zeitpunkt durchgeführt werden, an dem das Gerät gekauft wird, oder es kann später mithilfe eines manuellen Erstellungsprozesses durchgeführt werden.  Weitere Informationen finden Sie unter [Hinzufügen von Geräten zu Windows Autopilot](add-devices.md).
- Stellen Sie sicher, dass dem Gerät ein Autopilot-Profil zugewiesen wurde:
  - Wenn Sie InTune und Azure Active Directory dynamischen Gerätegruppen verwenden, kann diese Zuweisung automatisch durchgeführt werden.
  - Wenn Sie InTune verwenden und statische Gerätegruppen Azure Active Directory, fügen Sie das Gerät manuell der Gerätegruppe hinzu.
  - Wenn Sie andere Methoden verwenden (z. b. Microsoft Store für Business oder Partner Center), weisen Sie dem Gerät manuell ein Autopilot-Profil zu.


## <a name="user-driven-mode-for-hybrid-azure-active-directory-join"></a>Benutzergesteuerte Modus für Hybrid Azure Active Directory Join

Windows Autopilot erfordert, dass Geräte Azure Active Directory verknüpft sind. Wenn Sie über eine lokale Active Directory Umgebung verfügen und Geräte auch mit Ihrer lokalen Domäne verknüpfen möchten, können Sie Autopilot-Geräte so konfigurieren, dass Sie [mit Azure Active Directory (Azure AD) Hybrid](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)verknüpft sind.  

### <a name="requirements"></a>Requirements (Anforderungen)

So führen Sie eine benutzergesteuerte Bereitstellung mit Hybrid Azure AD mithilfe von Windows Autopilot durch:

- Ein Windows Autopilot-Profil für den benutzergesteuerten Modus muss erstellt werden. 
  - **Azure AD Hybrid** verknüpft muss als die ausgewählte Option unter **Join to Azure AD as** in the Autopilot Profile angegeben werden.
- Wenn Sie InTune verwenden, muss eine Gerätegruppe in Azure Active Directory mit dem Windows Autopilot-Profil vorhanden sein, das dieser Gruppe zugewiesen ist.
- Auf dem Gerät muss Windows 10, Version 1809 oder höher, ausgeführt werden.
- Das Gerät muss auf einen Active Directory Domänen Controller zugreifen können. er muss daher mit dem Netzwerk der Organisation verbunden sein (wo die DNS-Einträge für die AD-Domäne und der AD-Domänen Controller aufgelöst werden können und mit dem Domänen Controller kommunizieren kann, um den Benutzer zu authentifizieren).
- Das Gerät muss auf das Internet zugreifen können, und zwar gemäß den [dokumentierten Netzwerk Anforderungen für Windows Autopilot](windows-autopilot-requirements.md).
- Der InTune-Connector für Active Directory muss installiert sein.
  - Hinweis: der InTune-Connector führt einen lokalen AD Join aus, sodass Benutzer keine lokale Ad-Join-Berechtigung benötigen, vorausgesetzt, der Connector ist [für die Durchführung dieser Aktion](https://docs.microsoft.com/intune/windows-autopilot-hybrid#increase-the-computer-account-limit-in-the-organizational-unit) im Auftrag des Benutzers konfiguriert. 
- Bei Verwendung eines Proxys müssen WPAD-Proxyeinstellungen aktiviert und konfiguriert sein.

**Azure AD Geräte**Verknüpfung: der Hybrid Azure AD Join-Prozess verwendet den Systemkontext zum Durchführen eines Geräte Azure AD Joins. aus diesem Grund werden die benutzerbasierten Azure AD joinberechtigungs Einstellungen nicht beeinträchtigt. Außerdem sind alle Benutzer standardmäßig in der Lage, Geräte mit Azure AD zu verbinden.

## <a name="user-driven-mode-for-hybrid-azure-active-directory-join-with-vpn-support"></a>Der benutzergesteuerte Modus für Hybrid Azure Active Directory Join mit VPN-Unterstützung

Geräte, die mit Active Directory verknüpft sind, benötigen eine Verbindung mit einem Active Directory Domänen Controller für eine Vielzahl von Aktivitäten, wie z. b. Benutzeranmeldung (Überprüfung der Anmelde Informationen des Benutzers) und Gruppenrichtlinie Anwendung.  Daher würde der benutzergesteuerte Windows Autopilot-Azure AD Hybrid Join Prozess überprüfen, ob das Gerät einen Active Directory Domänen Controller kontaktieren kann, indem er diesen Domänen Controller anhefteter.

Dank der zusätzlichen VPN-Unterstützung für dieses Szenario können Sie jetzt angeben, dass die Konnektivitätsprüfung während des Azure AD Hybrid Join übersprungen werden soll.  Dies beseitigt nicht die Notwendigkeit der Kommunikation mit einem Active Directory Domänen Controller, sondern ermöglicht es, dass das Gerät zuerst mit einer erforderlichen VPN-Konfiguration vorbereitet wird, die über InTune bereitgestellt wurde, bevor der Benutzer versucht hat, sich bei Windows anzumelden, und ermöglicht so die Konnektivität mit dem Netzwerk der Organisation.

### <a name="requirements"></a>Requirements (Anforderungen)

Die folgenden zusätzlichen Anforderungen gelten für Azure AD Hybrid Join mit VPN-Unterstützung:

- Eine unterstützte Version von Windows 10:
  - Windows 10 1903 + 10. Dezember-Kumulatives Update (KB4530684, OS Build 18362,535) oder höher 
  - Windows 10 1909 + 10. Dezember-Kumulatives Update (KB4530684, OS Build 18363,535) oder höher  
  - Windows 10 2004 oder höher 
- Aktivieren Sie im Azure AD Hybrid Join Autopilot-Profil die neue Option "Überprüfung der Domänen Konnektivität überspringen".
- Eine VPN-Konfiguration, die über InTune bereitgestellt werden kann, die es dem Benutzer ermöglicht, eine VPN-Verbindung über den Windows-Anmeldebildschirm manuell herzustellen, oder eine VPN-Verbindung, die automatisch eine VPN-Verbindung herstellt.  

Welche VPN-Konfiguration erforderlich ist, hängt von der verwendeten VPN-Software und der verwendeten Authentifizierung ab.  Bei VPN-Lösungen von Drittanbietern (nicht von Microsoft) ist dies in der Regel die Bereitstellung einer Win32-app (die sowohl die VPN-Client Software selbst als auch alle spezifischen Verbindungsinformationen (z. b. VPN-Endpunkt-Hostnamen) über InTune-Verwaltungs Erweiterungen umfasst.  Informationen zu den für diesen anbieterspezifischen Konfigurationsdetails finden Sie in der Dokumentation des VPN-Anbieters.

> [!NOTE]
> Die VPN-Anforderungen sind nicht spezifisch für Windows Autopilot. Wenn Sie z. b. bereits eine VPN-Konfiguration implementiert haben, die das Zurücksetzen von Remote Kennwörtern ermöglicht, wenn sich ein Benutzer bei Windows mit einem neuen Kennwort anmelden muss, wenn er nicht im Netzwerk der Organisation vorhanden ist, kann dieselbe Konfiguration mit Windows Autopilot verwendet werden.  Nachdem sich der Benutzer angemeldet hat, um seine Anmelde Informationen zwischenzuspeichern, benötigen nachfolgende Anmeldeversuche keine Konnektivität, da die zwischengespeicherten Anmelde Informationen verwendet werden können. 

In Fällen, in denen die Zertifikat Authentifizierung für die VPN-Software erforderlich ist, sollte das erforderliche Computer Zertifikat auch über InTune bereitgestellt werden.  Diese Bereitstellung kann mithilfe der InTune-Zertifikat Registrierungsfunktionen erfolgen, die die Zertifikat Profile für das Gerät als Ziel verwenden.

Beachten Sie, dass Benutzerzertifikate nicht unterstützt werden, da diese Zertifikate erst bereitgestellt werden können, wenn sich der Benutzer anmeldet.  Außerdem werden nicht von Microsoft aus dem Windows Store übermittelte UWP-VPN-Plug-ins ebenfalls nicht unterstützt, da diese Plug-ins nicht installiert werden, nachdem sich der Benutzer angemeldet hat.

### <a name="validation"></a>Überprüfen

Vor dem Versuch, einen Hybrid Azure AD Join per VPN zu verwenden, ist es wichtig, zuerst zu bestätigen, dass ein Benutzer gesteuAzure AD Hybrid Join Prozess im Netzwerk der Organisation ausgeführt werden kann, bevor die unten beschriebenen zusätzlichen Anforderungen hinzugefügt werden.  Dies vereinfacht die Problembehandlung, indem sichergestellt wird, dass der Hauptprozess einwandfrei funktioniert, bevor die zusätzliche VPN-Konfiguration hinzugefügt wird

Überprüfen Sie als nächstes, ob die VPN-Konfiguration (Win32-APP, certs und andere Anforderungen) über InTune auf einem vorhandenen Gerät bereitgestellt werden können, das bereits Hybrid Azure AD verknüpft ist.  Einige VPN-Clients erstellen z. b. eine Computer spezifische VPN-Verbindung im Rahmen des Installationsvorgangs, sodass Sie die Konfiguration mithilfe von folgenden Schritten überprüfen können:

- Überprüfen Sie in PowerShell, ob mindestens eine Computer spezifische VPN-Verbindung mit dem Befehl "Get-VPNconnection-alluserconnection" erstellt wurde.
- Versuchen Sie, die VPN-Verbindung mit dem folgenden Befehl manuell zu starten: RASDIAL.EXE "ConnectionName"
- Melden Sie sich ab, und überprüfen Sie, ob auf der Windows-Anmeldeseite das Symbol "VPN-Verbindung" angezeigt wird.
- Verschieben Sie das Gerät aus dem Unternehmensnetzwerk, und versuchen Sie, die Verbindung mithilfe des Symbols auf der Windows-Anmeldeseite herzustellen, und melden Sie sich bei einem Konto an, das über keine zwischengespeicherten Anmelde Informationen verfügt.

Bei VPN-Konfigurationen, die automatisch eine Verbindung herstellen, können sich die Validierungs Schritte unterscheiden.

> [!NOTE]
> Always on-VPN kann für dieses Szenario verwendet werden.  Weitere Informationen finden Sie in der Dokumentation zum Bereitstellen von [Always on-VPN](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy-deployment) .  Beachten Sie, dass InTune das erforderliche Computer spezifische VPN-Profil noch nicht bereitstellen kann. 

Um den End-to-End-Prozess zu überprüfen, stellen Sie sicher, dass das erforderliche kumulative Update für Windows 10 unter Windows 10 1903 oder Windows 10 1909 installiert wurde. Dieses Update kann manuell während des OOBE-Vorgangs durchgeführt werden, indem zuerst das neueste kumulative von heruntergeladen https://catalog.update.microsoft.com und dann manuell installiert wird:

- Drücken Sie UMSCHALT + F10, um eine Eingabeaufforderung zu öffnen.
- Fügen Sie einen USB-Schlüssel mit dem heruntergeladenen Update ein.
- Installieren Sie das Update mit dem Befehl (durch den tatsächlichen Dateinamen): WUSA.EXE <filename> . msu/quiet
- Starten Sie den Computer mit dem folgenden Befehl neu: shutdown.exe/r/t 0

Alternativ können Sie Windows Update aufrufen, um die neuesten Updates über diesen Prozess zu installieren:

- Drücken Sie UMSCHALT + F10, um eine Eingabeaufforderung zu öffnen.
- Führen Sie den Befehl "Start MS-Settings:" aus.
- Navigieren Sie zum Knoten "& Sicherheit aktualisieren", und suchen Sie nach Updates.
- Neustart nach der Installation der Updates.

### <a name="step-by-step-instructions"></a>Schrittweise Anleitung

Weitere Informationen finden Sie unter Bereitstellen von [Hybrid Azure AD verbundenen Geräten mit InTune und Windows Autopilot](https://docs.microsoft.com/intune/windows-autopilot-hybrid).



