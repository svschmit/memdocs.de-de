---
title: Windows Autopilot Reset
description: Durch Windows Autopilot Reset wird das Gerät wieder in einen Zustand versetzt, in dem sich der nächste Benutzer schnell und einfach anmelden kann.
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
ms.openlocfilehash: 8388febead5953fd6c76e7e40571d3b2e1b91e4d
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/04/2020
ms.locfileid: "87756500"
---
# <a name="windows-autopilot-reset"></a>Windows Autopilot Reset

- Gilt für: Windows 10, Version 1709 und höher (lokale zurück Setzung)
- Gilt für: Windows 10, Version 1809 und höher (Remote Zurücksetzung)

Windows Autopilot Reset entfernt persönliche Dateien, Apps und Einstellungen und wendet die ursprünglichen Einstellungen eines Geräts erneut an, wobei seine Identitäts Verbindung mit Azure AD und dessen Verwaltungs Verbindung zu InTune aufrechterhalten wird, sodass das Gerät wieder verwendet werden kann. Durch Windows Autopilot Reset wird das Gerät wieder in einen Zustand versetzt, in dem sich der nächste Benutzer anmelden und die Produktivität schnell und einfach wiederherstellen lässt. 

Der Windows Autopilot Reset-Prozess speichert automatisch Informationen vom vorhandenen Gerät:
 
-   Legen Sie Region, Sprache und Tastatur auf die ursprünglich konfigurierten Werte fest.
-   Details zur Wi-Fi-Verbindung.
-   Bereitstellung von Paketen, die zuvor auf das Gerät angewendet wurden, sowie ein Bereitstellungs Paket, das auf einem USB-Laufwerk vorhanden ist, wenn der Zurücksetzungs Prozess initiiert wird. 
-   Azure Active Directory Geräte Mitgliedschaft und MDM-Registrierungsinformationen.

Der Windows Autopilot-Reset blockiert den Zugriff des Benutzers auf den Desktop, bis diese Informationen wieder hergestellt werden, einschließlich der erneuten Anwendung von Bereitstellungs Paketen.  Bei Geräten, die bei einem MDM-Dienst registriert sind, wird die Windows Autopilot-zurück Setzung auch blockiert, bis eine MDM-Synchronisierung abgeschlossen ist  
Bei der Verwendung der Autopilot-Zurücksetzung auf einem Gerät, wird dessen primäre Benutzer entfernt. Der nächste Benutzer, der sich nach dem Zurücksetzen anmeldet, wird als primärer Benutzer festgelegt.
 
 
>[!NOTE]
>Die Autopilot-zurück Setzung unterstützt keine Azure AD Hybrid verbundenen Geräte.

## <a name="scenarios"></a>Szenarien

Windows Autopilot Reset unterstützt zwei Szenarien:

-   [Lokale zurück](#reset-devices-with-local-windows-autopilot-reset) setzung, initiiert von IT-Mitarbeitern oder anderen Administratoren aus der Organisation.
-   [Remote](#reset-devices-with-remote-windows-autopilot-reset) Zurücksetzung von IT-Mitarbeitern über einen MDM-Dienst (z. b. Microsoft InTune).

Bei jedem Szenario gelten zusätzliche Anforderungen und Konfigurationsdetails. Weitere Informationen finden Sie unter den detaillierten Links oben.

## <a name="reset-devices-with-local-windows-autopilot-reset"></a>Zurücksetzen von Geräten mit der lokalen Windows Autopilot-zurück Setzung 

**Gilt für: Windows 10, Version 1709 und höher**

Zum Ausführen dieser Aufgabe ist die Rolle "InTune-Dienst Administrator" erforderlich.  Weitere Informationen finden Sie unter [Hinzufügen von Benutzern und Gewähren von Administratorrechten für Intune](https://docs.microsoft.com/intune/users-add).

IT-Administratoren können eine lokale Windows Autopilot-zurück Setzung durchführen, um persönliche Dateien, Apps und Einstellungen schnell zu entfernen und Windows 10-Geräte jederzeit über den Sperrbildschirm zurückzusetzen. Außerdem können Sie die ursprünglichen Einstellungen und die Verwaltungs Registrierung (Azure Active Directory und Geräteverwaltung) anwenden, sodass die Geräteeinsatz bereit sind. Bei einer lokalen Autopilot-zurück Setzung werden Geräte in einen vollständig konfigurierten oder bekannten Zustand zurückversetzt.

So aktivieren Sie die lokale Autopilot-zurück Setzung in Windows 10:

1. [Aktivieren der Richtlinie für das Feature](#enable-local-windows-autopilot-reset)
2. [Zurücksetzen für jedes Gerät zurücksetzen](#trigger-local-windows-autopilot-reset)

### <a name="enable-local-windows-autopilot-reset"></a>Aktivieren der lokalen Windows Autopilot-zurück Setzung

Um eine lokale Windows Autopilot-zurück Setzung zu aktivieren, muss die Richtlinie **disableautomatikredeploymentanmelde** Informationen konfiguriert werden. Diese Richtlinie ist in den [Richtlinien-CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-credentialproviders), " **erleistungsanbieter/disableautomatikredeploymentanmelde**Informationen" dokumentiert. Standardmäßig ist der lokale Windows Autopilot deaktiviert. Dadurch wird sichergestellt, dass eine lokale Autopilot-zurück Setzung nicht versehentlich ausgelöst wird.

Die Richtlinie kann mit einer der folgenden Methoden festgelegt werden:

- MDM-Anbieter

    - Wenn Sie InTune verwenden, können Sie ein neues Geräte Konfigurations Profil erstellen und für die Plattform "Windows 10 oder höher", "Geräte Einschränkungen" für den Profiltyp und "Allgemein" für die Kategorie "Einstellungen" angeben.  Die Einstellung für die **automatische erneute Bereitstellung** sollte auf **zulassen**festgelegt sein.  Stellen Sie diese Einstellung auf allen Geräten bereit, auf denen eine lokale zurück Setzung zulässig sein soll.
    - Wenn Sie einen anderen MDM-Anbieter als InTune verwenden, finden Sie in der Dokumentation zum MDM-Anbieter Informationen zum Festlegen dieser Richtlinie. 

- Windows-Konfigurations-Designer

    Sie können den [Windows-Konfigurations-Designer verwenden](https://docs.microsoft.com/windows/configuration/provisioning-packages/provisioning-create-package) , um die **Lauf Zeit Einstellungen > Richtlinien festzulegen > >** die Einstellung für "" auf "0", und erstellen Sie ein Bereitstellungs Paket.

- Einrichten der App "School PCs"

    Die neueste Version der App "Einrichtung von PCs" unterstützt das Aktivieren der lokalen Windows Autopilot-zurück Setzung.

### <a name="trigger-local-windows-autopilot-reset"></a>Lokale Windows Autopilot-zurück Setzung auslöst

Die Ausführung einer lokalen Windows Autopilot-zurück Setzung ist ein zweistufiger Prozess: Sie löst Sie aus, und Authentifizieren Sie sich dann. Nachdem Sie diese beiden Schritte ausgeführt haben, können Sie den Prozess ausführen lassen, und sobald der Vorgang abgeschlossen ist, ist das Gerät wieder einsatzbereit. 

**So initiieren Sie eine lokale Autopilot-zurück Setzung**

1. Geben Sie auf dem Windows-Geräte Sperrbildschirm die Tastenkombination: **STRG + ![ Windows-Taste ](images/windows_glyph.png) + R**ein. 

    ![Drücken Sie auf dem Windows-Sperrbildschirm STRG + Windows-Taste + R.](images/autopilot-reset-lockscreen.png)

    Dadurch wird ein benutzerdefinierter Anmeldebildschirm für die lokale Autopilot-zurück Setzung geöffnet. Der Bildschirm dient zwei Zwecken:
    1. Vergewissern Sie sich, dass der Endbenutzer über die Berechtigung verfügt, lokale Autopilot-zurück Setzung zu initiieren.
    2. Benachrichtigen Sie den Benutzer, wenn ein Bereitstellungs Paket, das mit Windows Configuration Designer erstellt wurde, als Teil des Prozesses verwendet wird.

    ![Benutzerdefinierter Anmeldebildschirm für lokale Autopilot-zurück Setzung](images/autopilot-reset-customlogin.png)

2. Melden Sie sich mit den Anmelde Informationen des Administrator Kontos an. Wenn Sie ein Bereitstellungs Paket erstellt haben, schließen Sie das USB-Laufwerk ein, und lösen Sie die lokale Autopilot-zurück Setzung aus.

    Sobald die lokale Autopilot-zurück Setzung ausgelöst wird, wird der Zurücksetzungs Vorgang gestartet. Nachdem die Bereitstellung abgeschlossen ist, kann das Gerät wieder verwendet werden.

## <a name="reset-devices-with-remote-windows-autopilot-reset"></a>Zurücksetzen von Geräten mit Remote-Windows Autopilot Reset

**Gilt für: Windows 10, Version 1809 oder höher**

Beim Durchführen einer Remote Zurücksetzung von Windows Autopilot kann ein MDM-Dienst wie Microsoft InTune verwendet werden, um den Zurücksetzungs Prozess zu initiieren. dadurch ist es nicht erforderlich, dass das IT-Personal oder andere Administratoren jeden Computer besuchen müssen, um den Prozess zu initiieren.

Zum Aktivieren eines Geräts für eine Remote Zurücksetzung von Windows Autopilot muss das Gerät über MDM verwaltet und mit Azure AD verknüpft werden. Diese Funktion wird auf Geräten, die mit dem Autopilot- [Self-Bereitstellungs Modus](self-deploying.md)registriert wurden, nicht unterstützt.

### <a name="triggering-a-remote-windows-autopilot-reset"></a>Auslösen einer Remote-Windows Autopilot-zurück Setzung

Führen Sie die folgenden Schritte aus, um eine Remote-Windows Autopilot-zurück setzung über InTune zu starten:
 
-   Navigieren Sie in der InTune-Konsole zur Registerkarte **Geräte** . 
-   Wählen Sie in der Ansicht **alle Geräte** die Zielgeräte zurücksetzen aus, und klicken Sie dann auf **Weitere** , um Geräte Aktionen anzuzeigen. 
-   Wählen Sie **Autopilot Reset** aus, um die Aufgabe zum Zurücksetzen zu starten. 

>[!NOTE]
>Die Option Autopilot Reset wird in Microsoft InTune für Geräte, auf denen Windows 10 Build 17672 oder höher nicht ausgeführt wird, nicht aktiviert.

>[!IMPORTANT]
>Das Feature für die Autopilot-zurück Setzung bleibt abgeblendet, **es sei denn** , Sie setzen das Gerät mithilfe von Autopilot zurück (entweder mithilfe der neuen zurück setzung oder der manuellen System Vorbereitung des Geräts).

Nachdem der Vorgang abgeschlossen ist, ist das Gerät wieder einsatzbereit.
 


## <a name="troubleshooting"></a>Problembehandlung

Windows Autopilot Reset erfordert, dass die [Windows-Wiederherstellungs Umgebung (WinRE)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference) ordnungsgemäß konfiguriert und auf dem Gerät aktiviert ist. Wenn Sie nicht konfiguriert und aktiviert ist, wird ein Fehler wie `Error code: ERROR_NOT_SUPPORTED (0x80070032)` gemeldet.

Um sicherzustellen, dass WinRE aktiviert ist, führen Sie mit dem [REAgentC.exe Tool](https://docs.microsoft.com/windows-hardware/manufacture/desktop/reagentc-command-line-options) den folgenden Befehl aus:

```
reagentc /enable
```

Wenn das Zurücksetzen von Windows Autopilot nach dem Aktivieren von WinRE fehlschlägt oder Sie WinRE nicht aktivieren können, wenden Sie sich an [Microsoft-Support](https://support.microsoft.com) , um Unterstützung zu erhalten.
