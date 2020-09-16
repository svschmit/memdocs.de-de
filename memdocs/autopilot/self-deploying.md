---
title: Selbstbereitstellungs Modus von Windows Autopilot
description: Der Modus für die selbst Bereitstellung ermöglicht die Bereitstellung eines Geräts ohne Benutzerinteraktion. Dieser Modus ist für die Bereitstellung von Windows 10 als Kiosk, digitales Signalgerät oder frei gegebenes Gerät konzipiert.
keywords: MDM, Setup, Windows, Windows 10, OOBE, Manage, Bereitstellung, Autopilot, ZTD, Zero-Touchscreen, Partner, msfb, InTune
ms.reviewer: mniehaus
manager: laurawi
ms.technology: windows
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
ms.openlocfilehash: 13b45b972ed17d24efedaa048c0e48ea2f2d90d2
ms.sourcegitcommit: e533cdf8722156a66b1cc46f710def96587345d0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/15/2020
ms.locfileid: "90568610"
---
# <a name="windows-autopilot-self-deploying-mode"></a>Selbstbereitstellungs Modus von Windows Autopilot

**Gilt für: Windows 10, Version 1903 oder höher**

Mit dem selbstbereitstellungs Modus von Windows Autopilot können Sie ein Gerät ohne Benutzerinteraktion bereitstellen. Bei Geräten mit einer Ethernet-Verbindung ist keine Benutzerinteraktion erforderlich. Für Geräte, die über Wi-Fi verbunden sind, darf der Benutzer nur folgende Aktionen ausführen:
- Wählen Sie die Sprache, das Gebiets Schema und die Tastatur aus.
- Erstellen Sie eine Netzwerkverbindung. 

Der selbst Bereitstellungs Modus bietet Folgendes:
- Verbindet das Gerät mit Azure Active Directory.
- Registriert das Gerät bei InTune (oder einem anderen MDM-Dienst) mit Azure AD für die automatische MDM-Registrierung.
- Stellt sicher, dass alle Richtlinien, Anwendungen, Zertifikate und Netzwerk Profile auf dem Gerät bereitgestellt werden.
- Verwendet die Seite Anmeldungs Status, um den Zugriff zu verhindern, bis das Gerät vollständig bereitgestellt wurde.

>[!NOTE]
>Der Modus für die selbst Bereitstellung unterstützt Active Directory Join oder Azure AD Hybrid Join nicht. Alle Geräte werden Azure Active Directory hinzugefügt.

Mit dem Modus für die selbst Bereitstellung können Sie ein Windows 10-Gerät als Kiosk, digitales Geräte Signal oder frei gegebenes Gerät bereitstellen.

Sie können den [Kiosk-Browser](https://www.microsoft.com/p/kiosk-browser/9ngb5s5xg2kp?rtc=1&activetab=pivot:overviewtab) verwenden, wenn Sie ein Kiosk Gerät einrichten. Diese APP basiert auf Microsoft Edge und kann verwendet werden, um eine angepasste, MDM-verwaltete Browser Darstellung zu erstellen.

Sie können die Gerätekonfiguration vollständig automatisieren, indem Sie den selbstbereitstellungs Modus mit MDM-Richtlinien kombinieren. Verwenden Sie die MDM-Richtlinien zum Erstellen eines lokalen Kontos, das für die automatische Anmeldung konfiguriert ist. Weitere Informationen finden Sie in folgenden Quellen:
- [Vereinfachung der Kiosk Verwaltung mit Windows 10](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/simplifying-kiosk-management-for-it-with-windows-10/ba-p/187691).
- [Einrichten eines Kiosk-oder digitalen Anmeldens in InTune oder einem anderen MDM-Dienst](/windows/configuration/setup-kiosk-digital-signage#set-up-a-kiosk-or-digital-sign-in-intune-or-other-mdm-service).

>[!NOTE]
>Der Modus für die selbst Bereitstellung ordnet dem Gerät derzeit keinen Benutzer zu (da im Rahmen des Prozesses keine Benutzer-ID oder kein Kennwort angegeben ist). Folglich sind einige Azure AD-und InTune-Funktionen (z. b. die BitLocker-Wiederherstellung, die Installation von Apps aus dem Unternehmensportal oder der bedingte Zugriff) möglicherweise nicht für einen Benutzer verfügbar, der sich beim Gerät anmeldet. Weitere Informationen finden Sie unter [Windows Autopilot-Szenarios und-Funktionen](windows-autopilot-scenarios.md) und [Festlegen des BitLocker-Verschlüsselungsalgorithmus für Autopilot-Geräte](bitlocker.md).

![Die Benutzer Darstellung mit dem selbstbereitstellungs Modus von Windows Autopilot](images/self-deploy-welcome.png)

## <a name="requirements"></a>Anforderungen

Der Modus für die selbst Bereitstellung verwendet die TPM 2,0-Hardware eines Geräts, um das Gerät beim Azure AD Mandanten einer Organisation zu authentifizieren. Daher können Geräte ohne TPM 2,0 in diesem Modus nicht verwendet werden. Geräte müssen auch den TPM-Geräte Nachweis unterstützen. Alle neuen Windows-Geräte sollten diese Anforderungen erfüllen.

>[!IMPORTANT]
>Wenn Sie versuchen, eine Bereitstellung im selbst Bereitstellungs Modus auf einem Gerät durchführen, das TPM 2,0 oder auf einem virtuellen Computer nicht unterstützt, schlägt der Prozess fehl, wenn das Gerät mit einem 0x800705b4-Timeout Fehler überprüft wird (virtuelle Hyper-V-TPMs werden nicht unterstützt). Beachten Sie außerdem, dass Windows 10, Version 1903 oder höher, aufgrund von Problemen mit dem TPM-Geräte Nachweis in Windows 10, Version 1809, den Modus für die selbst Bereitstellung verwenden muss. Da Windows 10 Enterprise 2019 LTSC auf Windows 10, Version 1809 basiert, wird der Modus für die selbst Bereitstellung in Windows 10 Enterprise 2019 LTSC ebenfalls nicht unterstützt. Informationen zu anderen bekannten Fehlern und Lösungen finden Sie unter [bekannte Probleme von Windows Autopilot](known-issues.md) .

Während des Autopilot-Prozesses können Sie ein Organisations spezifisches Logo und einen Organisationsnamen anzeigen. Zu diesem Zweck muss Azure AD Unternehmens Branding mit den Bildern und Text konfiguriert werden, die Sie anzeigen möchten. Weitere Informationen finden Sie [unter Schnellstart: Hinzufügen eines Unternehmensbrandings zur Anmeldeseite in Azure AD](/azure/active-directory/fundamentals/customize-branding) . 

## <a name="step-by-step"></a>Schritt für Schritt

Die folgenden Vorbereitungsschritte müssen ausgeführt werden, um Windows Autopilot im Self-Bereitstellungs Modus bereitstellen zu können:

1. Erstellen Sie ein Autopilot-Profil für den selbst Bereitstellungs Modus mit den gewünschten Einstellungen. In Microsoft InTune wird dieser Modus explizit ausgewählt, wenn das Profil erstellt wird. Es ist nicht möglich, ein Profil im Microsoft Store für das Unternehmen oder Partner Center für den selbst Bereitstellungs Modus zu erstellen.
2. Wenn Sie InTune verwenden, erstellen Sie eine Gerätegruppe in Azure Active Directory, und weisen Sie dieser Gruppe das Autopilot-Profil zu. Stellen Sie sicher, dass das Profil dem Gerät zugewiesen wurde, bevor Sie versuchen, dieses Gerät bereitzustellen.
3. Starten Sie das Gerät, und stellen Sie ggf. eine Verbindung mit WLAN her, und warten Sie, bis der Bereitstellungs Prozess beendet ist.

## <a name="validation"></a>Überprüfen

Wenn Sie Windows Autopilot für die Bereitstellung im selbst Bereitstellungs Modus verwenden, sollte die folgende Endbenutzer Leistung beachtet werden:

-  Nachdem eine Verbindung mit einem Netzwerk hergestellt wurde, wird das Autopilot-Profil heruntergeladen.
- Wenn eine Verbindung mit Ethernet besteht und das Autopilot-Profil so konfiguriert ist, dass Sie übersprungen werden, werden die folgenden Seiten nicht angezeigt: Sprache, Gebiets Schema und Tastaturlayout. Andernfalls sind manuelle Schritte erforderlich:
  -  Wenn mehrere Sprachen in Windows 10 vorinstalliert sind, muss der Benutzer eine Sprache auswählen.
  -  Der Benutzer muss ein Gebiets Schema und ein Tastaturlayout und optional ein zweites Tastaturlayout auswählen.
-  Wenn eine Verbindung über Ethernet besteht, wird keine Netzwerk Aufforderung erwartet. Wenn keine Ethernet-Verbindung verfügbar ist und Wi-Fi integriert ist, muss der Benutzer eine Verbindung mit einem Drahtlos Netzwerk herstellen.
-  Windows 10 prüft, ob wichtige OOBE-Updates vorhanden sind. falls vorhanden, werden diese automatisch installiert (bei Bedarf neu gestartet).
-  Das Gerät wird Azure Active Directory beitreten.
-  Nach dem beitreten Azure Active Directory wird das Gerät bei InTune (oder anderen konfigurierten MDM-Diensten) registriert.
-  Die [Seite](enrollment-status.md) Anmeldungs Status wird angezeigt.
-  Abhängig von den bereitgestellten Geräteeinstellungen führt das Gerät Folgendes aus:
  -  Bleiben Sie auf dem Anmeldebildschirm, auf dem sich alle Mitglieder der Organisation anmelden können, indem Sie Ihre Azure AD Anmelde Informationen angeben.
  -  Melden Sie sich automatisch als lokales Konto für Geräte an, die als Kiosk oder digitale Beschilderung konfiguriert sind.

>[!NOTE]
>Das Bereitstellen von EAS-Richtlinien mithilfe des selbst Bereitstellungs Modus für Kiosk Bereitstellungen führt zu einem Fehler bei der automatischen Anmeldung. 

Wenn die beobachteten Ergebnisse nicht den Erwartungen entsprechen, lesen Sie die Dokumentation zur [Windows Autopilot-Problem](troubleshooting.md) Behandlung.
