---
title: Selbstbereitstellungs Modus von Windows Autopilot
description: Der Modus für die selbst Bereitstellung ermöglicht die Bereitstellung eines Geräts ohne Benutzerinteraktion. Dieser Modus ist für die Bereitstellung von Windows 10 als Kiosk, digitales Signalgerät oder frei gegebenes Gerät konzipiert.
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
ms.openlocfilehash: 5fccc36ff1ecacaee3d2aa3ed7c317faaaefc113
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/04/2020
ms.locfileid: "87756539"
---
# <a name="windows-autopilot-self-deploying-mode"></a>Selbstbereitstellungs Modus von Windows Autopilot

**Gilt für: Windows 10, Version 1903 oder höher**

Der selbst Bereitstellungs Modus von Windows Autopilot ermöglicht die Bereitstellung eines Geräts ohne Benutzerinteraktion. Bei Geräten mit einer Ethernet-Verbindung ist keine Benutzerinteraktion erforderlich. bei Geräten, die über Wi-Fi verbunden sind, ist nach dem Herstellen der WLAN-Verbindung (Auswählen von Sprache, Gebiets Schema und Tastatur und anschließendes Herstellen einer Netzwerkverbindung) keine Interaktion erforderlich.  

Der Modus für die selbst Bereitstellung fügt das Gerät in Azure Active Directory ein, registriert das Gerät bei InTune (oder einem anderen MDM-Dienst) und nutzt Azure AD für die automatische MDM-Registrierung und stellt sicher, dass alle Richtlinien, Anwendungen, Zertifikate und Netzwerk Profile auf dem Gerät bereitgestellt werden. dabei wird die Seite Anmeldungs Status genutzt, um den Zugriff auf den Desktop zu verhindern 

>[!NOTE]
>Der Modus für die selbst Bereitstellung unterstützt Active Directory Join oder Azure AD Hybrid Join nicht.  Alle Geräte werden Azure Active Directory hinzugefügt.

Der Modus für die selbst Bereitstellung ist für die Bereitstellung von Windows 10 als Kiosk, digitales Signalgerät oder frei gegebenes Gerät konzipiert. Wenn Sie einen Kiosk einrichten, können Sie den neuen Kiosk Browser nutzen, eine auf Microsoft Edge basierende APP, die zum Erstellen einer angepassten, MDM-verwalteten Browserumgebung verwendet werden kann. In Kombination mit MDM-Richtlinien, um ein lokales Konto zu erstellen und für die automatische Anmeldung zu konfigurieren, kann die komplette Konfiguration des Geräts automatisiert werden. Weitere Informationen zu diesen Optionen finden Sie unter Vereinfachen der Kiosk Verwaltung mit Windows 10.  Weitere Informationen finden [Sie unter Einrichten eines Kiosk-oder digitalen Anmeldens in InTune oder einem anderen MDM-Dienst](https://docs.microsoft.com/windows/configuration/setup-kiosk-digital-signage#set-up-a-kiosk-or-digital-sign-in-intune-or-other-mdm-service) .

>[!NOTE]
>Der Modus für die selbst Bereitstellung ordnet dem Gerät derzeit keinen Benutzer zu (da im Rahmen des Prozesses keine Benutzer-ID oder kein Kennwort angegeben ist).  Folglich sind einige Azure AD-und InTune-Funktionen (z. b. die BitLocker-Wiederherstellung, die Installation von Apps aus dem Unternehmensportal oder der bedingte Zugriff) möglicherweise nicht für einen Benutzer verfügbar, der sich beim Gerät anmeldet. Weitere Informationen finden Sie unter [Windows Autopilot-Szenarios und-Funktionen](windows-autopilot-scenarios.md) und [Festlegen des BitLocker-Verschlüsselungsalgorithmus für Autopilot-Geräte](bitlocker.md).

![Die Benutzer Darstellung mit dem selbstbereitstellungs Modus von Windows Autopilot](images/self-deploy-welcome.png)

## <a name="requirements"></a>Requirements (Anforderungen)

Da der Modus für die selbst Bereitstellung die TPM 2,0-Hardware eines Geräts verwendet, um das Gerät bei einem Azure AD Mandanten einer Organisation zu authentifizieren, können Geräte ohne TPM 2,0 in diesem Modus nicht verwendet werden.  Die Geräte müssen auch einen TPM-Geräte Nachweis unterstützen.  (Alle neu hergestellten Windows-Geräte sollten diese Anforderungen erfüllen.)

>[!IMPORTANT]
>Wenn Sie versuchen, eine Bereitstellung im selbst Bereitstellungs Modus auf einem Gerät durchführen, das TPM 2,0 oder auf einem virtuellen Computer nicht unterstützt, schlägt der Prozess fehl, wenn das Gerät mit einem 0x800705b4-Timeout Fehler überprüft wird (virtuelle Hyper-V-TPMs werden nicht unterstützt). Beachten Sie außerdem, dass Windows 10, Version 1903 oder höher, aufgrund von Problemen mit dem TPM-Geräte Nachweis in Windows 10, Version 1809, den Modus für die selbst Bereitstellung verwenden muss. Da Windows 10 Enterprise 2019 LTSC auf Windows 10, Version 1809 basiert, wird der Modus für die selbst Bereitstellung in Windows 10 Enterprise 2019 LTSC ebenfalls nicht unterstützt. Informationen zu anderen bekannten Fehlern und Lösungen finden Sie unter [bekannte Probleme von Windows Autopilot](known-issues.md) .

Um während des Autopilot-Prozesses ein Organisations spezifisches Logo und einen Organisationsnamen anzuzeigen, muss Azure Active Directory Unternehmens Branding mit den Bildern und Text konfiguriert werden, die angezeigt werden sollen.  Weitere Informationen finden Sie [unter Schnellstart: Hinzufügen eines Unternehmensbrandings zur Anmeldeseite in Azure AD](https://docs.microsoft.com/azure/active-directory/fundamentals/customize-branding) . 

## <a name="step-by-step"></a>Schritt für Schritt

Die folgenden Vorbereitungsschritte müssen ausgeführt werden, um eine Bereitstellung im Self-Deployment-Modus mithilfe von Windows Autopilot durchführen zu können:

-   Erstellen Sie ein Autopilot-Profil für den selbst Bereitstellungs Modus mit den gewünschten Einstellungen.  In Microsoft InTune wird dieser Modus explizit ausgewählt, wenn das Profil erstellt wird. (Beachten Sie, dass es nicht möglich ist, ein Profil im Microsoft Store for Business oder Partner Center für den selbst Bereitstellungs Modus zu erstellen.)
-   Wenn Sie InTune verwenden, erstellen Sie eine Gerätegruppe in Azure Active Directory, und weisen Sie dieser Gruppe das Autopilot-Profil zu.  Stellen Sie sicher, dass das Profil dem Gerät zugewiesen wurde, bevor Sie versuchen, dieses Gerät bereitzustellen.
-   Starten Sie das Gerät, und stellen Sie ggf. eine Verbindung mit Wi-Fi her, und warten Sie, bis der Bereitstellungs Prozess beendet ist.

## <a name="validation"></a>Überprüfen

Beim Ausführen einer Bereitstellung im Self-Deployment-Modus mithilfe von Windows Autopilot sollten folgende Endbenutzer Erfahrungen beachtet werden:

-   Nachdem eine Verbindung mit einem Netzwerk hergestellt wurde, wird das Autopilot-Profil heruntergeladen.
-   Wenn das Autopilot-Profil so konfiguriert wurde, dass die Sprache, das Gebiets Schema und das Tastaturlayout automatisch konfiguriert werden, sollten diese OOBE-Bildschirme übersprungen werden, solange Ethernet-Konnektivität verfügbar ist.  Andernfalls sind manuelle Schritte erforderlich:
    -   Wenn mehrere Sprachen in Windows 10 vorinstalliert sind, muss der Benutzer eine Sprache auswählen.
    -   Der Benutzer muss ein Gebiets Schema und ein Tastaturlayout und optional ein zweites Tastaturlayout auswählen.
-   Wenn eine Verbindung über Ethernet besteht, wird keine Netzwerk Aufforderung erwartet.  Wenn keine Ethernet-Verbindung verfügbar ist und Wi-Fi integriert ist, muss der Benutzer eine Verbindung mit einem Drahtlos Netzwerk herstellen.
-   Windows 10 prüft, ob wichtige OOBE-Updates vorhanden sind. falls vorhanden, werden diese automatisch installiert (bei Bedarf neu gestartet).
-   Das Gerät wird Azure Active Directory beitreten.
-   Nach dem beitreten Azure Active Directory wird das Gerät bei InTune (oder anderen konfigurierten MDM-Diensten) registriert.
-   Die [Seite](enrollment-status.md) Anmeldungs Status wird angezeigt.
-   Abhängig von den bereitgestellten Geräteeinstellungen führt das Gerät Folgendes aus:
    -   Bleiben Sie auf dem Anmeldebildschirm, auf dem sich alle Mitglieder der Organisation anmelden können, indem Sie Ihre Azure AD Anmelde Informationen angeben.
    -   Melden Sie sich automatisch als lokales Konto für Geräte an, die als Kiosk oder digitale Beschilderung konfiguriert sind.

>[!NOTE]
>Das Bereitstellen von EAS-Richtlinien mithilfe des selbst Bereitstellungs Modus für Kiosk Bereitstellungen führt zu einem Fehler bei der automatischen Anmeldung. 

Wenn die beobachteten Ergebnisse nicht den Erwartungen entsprechen, lesen Sie die Dokumentation zur [Windows Autopilot-Problem](troubleshooting.md) Behandlung.
