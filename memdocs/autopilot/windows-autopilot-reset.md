---
title: Windows Autopilot Reset
description: Durch Windows Autopilot Reset wird das Gerät wieder in einen Zustand versetzt, in dem sich der nächste Benutzer schnell und einfach anmelden kann.
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
ms.openlocfilehash: 5ec7e9eeb9da46e1d9bc77dcd71e76be4948fc23
ms.sourcegitcommit: e533cdf8722156a66b1cc46f710def96587345d0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/15/2020
ms.locfileid: "90568566"
---
# <a name="windows-autopilot-reset"></a>Windows Autopilot Reset

- Gilt für: Windows 10, Version 1709 und höher (lokale zurück Setzung)
- Gilt für: Windows 10, Version 1809 und höher (Remote Zurücksetzung)

Durch Windows Autopilot Reset wird das Gerät wieder in einen Zustand versetzt, in dem sich der nächste Benutzer anmelden und die Produktivität schnell und einfach wiederherstellen lässt. Insbesondere Windows Autopilot Reset:
- Entfernt persönliche Dateien, Apps und Einstellungen.
- Wendet die ursprünglichen Einstellungen eines Geräts erneut an.
- Verwaltet die Identitäts Verbindung des Geräts mit Azure AD.
- Verwaltet die Verwaltungs Verbindung des Geräts mit InTune.

Der Windows Autopilot Reset-Prozess speichert automatisch Informationen vom vorhandenen Gerät:
 
- Legen Sie Region, Sprache und Tastatur auf die ursprünglichen Werte fest.
- Details zur Wi-Fi-Verbindung.
- Bereitstellen von Paketen, die zuvor auf das Gerät angewendet wurden
- Ein Bereitstellungs Paket, das auf einem USB-Laufwerk vorhanden ist, wenn der Zurücksetzungs Vorgang gestartet wird 
- Azure Active Directory Geräte Mitgliedschaft und MDM-Registrierungsinformationen.

Windows Autopilot Reset blockiert den Zugriff des Benutzers auf den Desktop, bis diese Informationen wieder hergestellt werden, einschließlich der erneuten Anwendung von Bereitstellungs Paketen. Bei Geräten, die bei einem MDM-Dienst registriert sind, wird die Windows Autopilot-zurück Setzung auch blockiert, bis eine MDM-Synchronisierung abgeschlossen ist Bei der Verwendung der Autopilot-Zurücksetzung auf einem Gerät, wird dessen primäre Benutzer entfernt. Der nächste Benutzer, der sich nach dem Zurücksetzen anmeldet, wird als primärer Benutzer festgelegt.
 
 
>[!NOTE]
>Die Autopilot-zurück Setzung unterstützt keine Azure AD Hybrid verbundenen Geräte.

## <a name="scenarios"></a>Szenarien

Windows Autopilot Reset unterstützt zwei Szenarien:

- [Lokale zurück](#reset-devices-with-local-windows-autopilot-reset) Setzung wurde von IT-Mitarbeitern oder anderen Administratoren aus der Organisation gestartet.
- [Remote](#reset-devices-with-remote-windows-autopilot-reset) Zurücksetzung von IT-Mitarbeitern über einen MDM-Dienst, z. b. Microsoft InTune, gestartet.

Für jedes Szenario gelten zusätzliche Anforderungen und Konfigurationsdetails.

## <a name="reset-devices-with-local-windows-autopilot-reset"></a>Zurücksetzen von Geräten mit der lokalen Windows Autopilot-zurück Setzung 

**Gilt für: Windows 10, Version 1709 und höher**

Für diese Aufgabe ist die Rolle "InTune-Dienst Administrator" erforderlich. Weitere Informationen finden Sie unter [Hinzufügen von Benutzern und Gewähren von Administratorrechten für Intune](/intune/users-add).

IT-Administratoren können eine lokale Windows Autopilot-zurück setzung für Folgendes verwenden:
- Schnelles Entfernen persönlicher Dateien, Apps und Einstellungen.
- Zurücksetzen von Windows 10-Geräten über den Sperrbildschirm
- Anwenden ursprünglicher Einstellungen und Verwaltungs Registrierung (Azure Active Directory-und Geräteverwaltung) das Gerät kann dann verwendet werden. Bei einer lokalen Autopilot-zurück Setzung werden Geräte in einen vollständig konfigurierten oder bekannten Zustand zurückversetzt.

So aktivieren Sie die lokale Autopilot-zurück Setzung in Windows 10:

1. [Aktivieren der Richtlinie für das Feature](#enable-local-windows-autopilot-reset)
2. [Zurücksetzen für jedes Gerät zurücksetzen](#trigger-local-windows-autopilot-reset)

### <a name="enable-local-windows-autopilot-reset"></a>Aktivieren der lokalen Windows Autopilot-zurück Setzung

Um eine lokale Windows Autopilot-zurück Setzung zu aktivieren, muss die Richtlinie **disableautomatikredeploymentanmelde** Informationen konfiguriert werden. Diese Richtlinie ist in den [Richtlinien-CSP](/windows/client-management/mdm/policy-csp-credentialproviders), " **erleistungsanbieter/disableautomatikredeploymentanmelde**Informationen" dokumentiert. Standardmäßig ist der lokale Windows Autopilot deaktiviert. Diese Standardeinstellung stellt sicher, dass eine lokale Autopilot-zurück Setzung nicht versehentlich ausgelöst wird.

Die Richtlinie kann mit einer der folgenden Methoden festgelegt werden:

- MDM-Anbieter

 - Wenn Sie InTune verwenden, können Sie ein neues Geräte Konfigurations Profil mit den folgenden Einstellungen erstellen:
   - **Plattform**  =  **Windows 10 oder** höher
   - **Profiltyp**  =  **Geräte Einschränkungen**
   - **Kategorie**  =  **Allgemein**
   - **Automatische erneute Bereitstellung**  =  **Zulassen**. Stellen Sie diese Einstellung auf allen Geräten bereit, auf denen eine lokale zurück Setzung zulässig sein soll.
 - Wenn Sie einen anderen MDM-Anbieter als InTune verwenden, finden Sie in der Dokumentation zum MDM-Anbieter Informationen zum Festlegen dieser Richtlinie. 

- Windows-Konfigurations-Designer

 Sie können den [Windows-Konfigurations-Designer verwenden](/windows/configuration/provisioning-packages/provisioning-create-package) , um die **Lauf Zeit Einstellungen > Richtlinien festzulegen > >** die Einstellung für "" auf "0", und erstellen Sie ein Bereitstellungs Paket.

- Einrichten der App "School PCs"

 Die neueste Version der App "Einrichtung von PCs" unterstützt das Aktivieren der lokalen Windows Autopilot-zurück Setzung.

### <a name="trigger-local-windows-autopilot-reset"></a>Lokale Windows Autopilot-zurück Setzung auslöst

Eine lokale Windows Autopilot-zurück Setzung ist ein zweistufiger Prozess: Sie löst Sie aus, und Authentifizieren Sie sich dann. Nachdem Sie diese beiden Schritte ausgeführt haben, können Sie den Prozess ausführen lassen, und sobald der Vorgang abgeschlossen ist, ist das Gerät wieder einsatzbereit. 

**So initiieren Sie eine lokale Autopilot-zurück Setzung**

1. Geben Sie auf dem Windows-Geräte Sperrbildschirm die Tastenkombination: **STRG + ![ Windows-Taste ](images/windows_glyph.png) + R**ein. 

    ![Drücken Sie auf dem Windows-Sperrbildschirm STRG + Windows-Taste + R.](images/autopilot-reset-lockscreen.png)

    Mit diesen Tastatureingaben wird ein benutzerdefinierter Anmeldebildschirm für die lokale Autopilot-zurück Setzung geöffnet. Der Bildschirm dient zwei Zwecken:
    1. Vergewissern Sie sich, dass der Endbenutzer über die Berechtigung verfügt, lokale Autopilot-zurück Setzung zu initiieren.
    2. Benachrichtigen Sie den Benutzer, wenn ein Bereitstellungs Paket, das mit Windows Configuration Designer erstellt wurde, als Teil des Prozesses verwendet wird.

        ![Benutzerdefinierter Anmeldebildschirm für lokale Autopilot-zurück Setzung](images/autopilot-reset-customlogin.png)

2. Melden Sie sich mit den Anmelde Informationen des Administrator Kontos an. Wenn Sie ein Bereitstellungs Paket erstellt haben, schließen Sie das USB-Laufwerk ein, und lösen Sie die lokale Autopilot-zurück Setzung aus.

 Sobald die lokale Autopilot-zurück Setzung ausgelöst wird, wird der Zurücksetzungs Vorgang gestartet. Nachdem die Bereitstellung abgeschlossen ist, kann das Gerät wieder verwendet werden.

## <a name="reset-devices-with-remote-windows-autopilot-reset"></a>Zurücksetzen von Geräten mit Remote-Windows Autopilot Reset

**Gilt für: Windows 10, Version 1809 oder höher**

Sie können einen MDM-Dienst wie einen Microsoft InTune verwenden, um den Remote-Windows Autopilot Reset-Prozess zu starten. Wenn Sie auf diese Weise zurücksetzen, ist es nicht mehr erforderlich, dass IT-Mitarbeiter jeden Computer besuchen, um den Prozess zu starten.

Zum Aktivieren eines Geräts für eine Remote Zurücksetzung von Windows Autopilot muss das Gerät über MDM verwaltet und mit Azure AD verknüpft werden. Diese Funktion wird nicht auf Geräten unterstützt, die mit dem [Autopilot-Self-Bereitstellungs Modus](self-deploying.md)registriert wurden.

### <a name="triggering-a-remote-windows-autopilot-reset"></a>Auslösen einer Remote-Windows Autopilot-zurück Setzung

Führen Sie die folgenden Schritte aus, um eine Remote-Windows Autopilot-zurück setzung über InTune zu starten:
 
1. Navigieren Sie in der InTune-Konsole zur Registerkarte **Geräte** . 
2. Wählen Sie in der Ansicht **alle Geräte** die Zielgeräte zurücksetzen aus, und klicken Sie dann auf **Weitere** , um Geräte Aktionen anzuzeigen. 
3. Wählen Sie **Autopilot Reset** aus, um die Aufgabe zurücksetzen zu starten. 

>[!NOTE]
>Die Option Autopilot Reset wird in Microsoft InTune für Geräte, auf denen Windows 10 Build 17672 oder höher nicht ausgeführt wird, nicht aktiviert.

>[!IMPORTANT]
>Das Feature für die Autopilot-zurück Setzung bleibt abgeblendet, **es sei denn** , Sie setzen das Gerät mithilfe von Autopilot zurück (entweder mithilfe der neuen zurück setzung oder der manuellen System Vorbereitung des Geräts).

Nachdem der Vorgang abgeschlossen ist, ist das Gerät wieder einsatzbereit.
 


## <a name="troubleshooting"></a>Problembehandlung

Windows Autopilot Reset erfordert, dass die [Windows-Wiederherstellungs Umgebung (WinRE)](/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference) ordnungsgemäß konfiguriert und auf dem Gerät aktiviert ist. Wenn Sie nicht konfiguriert und aktiviert ist, wird ein Fehler wie `Error code: ERROR_NOT_SUPPORTED (0x80070032)` gemeldet.

Um sicherzustellen, dass WinRE aktiviert ist, führen Sie mit dem [REAgentC.exe Tool](/windows-hardware/manufacture/desktop/reagentc-command-line-options) den folgenden Befehl aus:

```
reagentc /enable
```

Wenn das Zurücksetzen von Windows Autopilot nach dem Aktivieren von WinRE fehlschlägt oder Sie WinRE nicht aktivieren können, wenden Sie sich an [Microsoft-Support](https://support.microsoft.com) , um Hilfe zu erhalten.
