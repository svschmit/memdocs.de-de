---
title: Problembehandlung bei der automatischen Registrierung von Windows 10-Geräten bei Intune
titleSuffix: Microsoft Intune
description: Hier erfahren Sie, wie Sie Probleme bei der automatischen Registrierung beheben.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 8/3/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: jchombe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6aff5dfe62c1c44ec22f56c287220b59b98a7536
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915482"
---
# <a name="troubleshoot-windows-10-group-policy-based-auto-enrollment-in-intune"></a>Problembehandlung bei der gruppenrichtlinienbasierten automatischen Registrierung von Windows 10-Geräten bei Intune

Mithilfe von Gruppenrichtlinien können Sie die automatische Registrierung bei MDM für der Active Directory Domain Services-Domäne beigetretene Geräte auslösen. Weitere Informationen zu diesem Feature finden Sie unter [Automatische Registrierung von Windows 10-Geräten mithilfe von Gruppenrichtlinien](/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy).

## <a name="verify-the-configuration"></a>Überprüfen der Konfiguration

Bevor Sie mit der Problembehandlung beginnen, sollten Sie überprüfen, ob alle Konfigurationen ordnungsgemäß vorgenommen wurden. Wenn das Problem dadurch nicht behoben werden kann, können Sie damit fortfahren, wichtige Protokolldateien auf Probleme zu prüfen.

- Vergewissern Sie sich, dass dem Benutzer, der das Gerät registrieren möchte, eine gültige Intune-Lizenz zugewiesen ist.

   ![Überprüfen der Intune-Lizenz](./media/troubleshoot-windows-auto-enrollment/intune-license.png)

- Vergewissern Sie sich, dass die automatische Registrierung für alle Benutzer aktiviert ist, die Geräte bei Intune registrieren. Weitere Informationen finden Sie unter [Azure AD und Microsoft Intune: Automatische MDM-Registrierung beim neuen Portal](/windows/client-management/mdm/azure-ad-and-microsoft-intune-automatic-mdm-enrollment-in-the-new-portal).

   ![Überprüfen der automatischen Registrierung](./media/troubleshoot-windows-auto-enrollment/verify-auto-enrollment.png)

   - Vergewissern Sie sich, dass **MDM-Benutzerbereich** auf **Alle** festgelegt ist, damit alle Benutzer Geräte bei Intune registrieren können.
   - Vergewissern Sie sich, dass **MAM-Benutzerbereich** auf **Keine** festgelegt ist. Andernfalls hat diese Einstellung Vorrang vor dem MDM-Bereich und verursacht Probleme.
   - Vergewissern Sie sich, dass **URL für MDM-Ermittlung** auf **https://enrollment.manage.microsoft.com/enrollmentserver/discovery** festgelegt ist.

- Vergewissern Sie sich, dass auf dem Gerät Windows 10 1709 oder höher ausgeführt wird.

- Vergewissern Sie sich, dass die Geräte auf  **In Azure AD Hybrid eingebunden** festgelegt sind. Diese Einstellung bedeutet, dass die Geräte der Domäne und Azure AD beigetreten sind.

   Führen Sie **dsregcmd /status** über die Befehlszeile aus, um die Einstellungen zu überprüfen. Bestätigen Sie dann die folgenden Statuswerte in der Ausgabe:

   - Device State
 
     ```asciidoc
     AzureAdJoined: YES
     DomainJoined: YES
     ```

   - SSO State

     ```asciidoc
     AzureAdPrt: YES
     ```

   Diese Informationen finden Sie in der Liste der Azure AD beigetretenen Geräte:

   ![Liste der Azure AD beigetretenen Geräte](./media/troubleshoot-windows-auto-enrollment/ad-joined-devices.png)

- Auf dem Azure AD-Blatt werden ggf. **Microsoft Intune** und **Microsoft Intune-Registrierung** unter  **Mobilität (MDM und MAM)**  aufgeführt. Wenn beide Einträge vorhanden sind, müssen Sie die Einstellungen für die automatische Registrierung unter **Microsoft Intune** konfigurieren.

- Vergewissern Sie sich, dass die folgende Gruppenrichtlinieneinstellung erfolgreich für alle Geräte bereitgestellt wird, die bei Intune registriert werden sollen:

   **Computerkonfiguration** > **Richtlinien** > **Administrative Vorlagen** > **Windows-Komponenten** > **MDM** > **Enable automatic MDM enrollment using default Azure AD credentials** (Automatische MDM-Registrierung mit Azure AD-Standardanmeldeinformationen zulassen)

   Wenden Sie sich an Ihren Domänenadministrator, um zu bestätigen, ob die Gruppenrichtlinieneinstellung erfolgreich bereitgestellt wurde.

- Stellen Sie sicher, dass das Gerät nicht bei Intune registriert ist, indem Sie den klassischen PC-Agent verwenden.
- Bestätigen Sie die folgenden Einstellungen in Azure AD und Intune:

   **In den Azure AD-Geräteeinstellungen:**

   ![Azure AD-Geräteeinstellungen](./media/troubleshoot-windows-auto-enrollment/device-setting.png)

   - Die Einstellung **Benutzer dürfen Geräte in Azure AD einbinden** ist auf **Alle** festgelegt.
   - Die Anzahl der Azure AD beigetretenen Geräte eines Benutzers überschreitet das Kontingent von **Maximale Anzahl von Geräten pro Benutzer** nicht.
   
   **In den Intune-Registrierungseinschränkungen:**

   - Die Registrierung von Windows-Geräten ist zulässig.

     ![Registrierung von Windows-Geräten ist zulässig](./media/troubleshoot-windows-auto-enrollment/restrictions.png)

## <a name="troubleshooting"></a>Problembehandlung

Wenn das Problem weiterhin besteht, überprüfen Sie die MDM-Protokolle auf dem Gerät in der Ereignisanzeige:

**Anwendungs- und Dienstprotokolle** > **Microsoft** > **Windows** > **DeviceManagement-Enterprise-Diagnostics-Provider** > **Admin**

Suchen Sie nach der Ereignis-ID 75 (Ereignismeldung: „Automatische MDM-Registrierung: Erfolgreich“). Dieses Ereignis bedeutet, dass die automatische Registrierung erfolgreich war.

In folgenden Situationen wird die Ereignis-ID 75 nicht protokolliert:

- wenn bei der Registrierung ein Fehler auftritt

  Suchen Sie nach der Ereignis-ID 76, um diesen Fehler zu bestätigen (Ereignismeldung: Automatische MDM-Registrierung: Fehler (Unbekannter Win32-Fehlercode: 0x8018002b)). Dieses Ereignis bedeutet, dass bei der automatischen Registrierung ein Fehler aufgetreten ist.

  Eine Lösung für dieses Problem finden Sie unter [Behandlung von Problemen bei der Windows-Geräteregistrierung in Microsoft Intune](/intune/troubleshoot-windows-enrollment-errors).

- Die Registrierung wurde nicht ausgelöst. In diesem Fall werden die Ereignis-IDs 75 und 76 nicht protokolliert.
  
  Der automatische Registrierungsprozess wird durch den Task **Schedule created by enrollment client for automatically enrolling in MDM from AAD** (Vom Registrierungsclient erstellter Zeitplan für die automatische Registrierung bei MDM über AAD) ausgelöst, der sich im Taskplaner unter **Microsoft** > **Windows** > **EnterpriseMgmt** befindet.

  ![Nicht ausgelöste Registrierung](./media/troubleshoot-windows-auto-enrollment/trigger.png)

  Der Task wird erstellt, wenn die Gruppenrichtlinieneinstellung **Enable automatic MDM enrollment using default Azure AD credentials** (Automatische MDM-Registrierung mit Azure AD-Standardanmeldeinformationen zulassen) erfolgreich auf dem Zielgerät bereitgestellt wurde. Der Task wird laut Zeitplan einen Tag lang alle fünf Minuten ausgeführt.

  Bestätigen Sie, dass der Task gestartet wurde, indem Sie die Ereignisprotokolle im Taskplaner über die Ereignisanzeige überprüfen:

  **Anwendungs- und Dienstprotokolle > Microsoft > Windows > Taskplaner > Betrieb**

  Wenn der Task im Taskplaner ausgelöst wird, wird die Ereignis-ID 107 protokolliert.

  Wenn der Task abgeschlossen ist, wird die Ereignis-ID 102 protokolliert. Dieses Ereignis wird unabhängig davon protokolliert, ob die automatische Registrierung erfolgreich war.

  > [!NOTE]
  > Über das Protokoll des Taskplaners können Sie überprüfen, ob die automatische Registrierung ausgelöst wurde. Aus dem Protokoll geht jedoch nicht hervor, ob die automatische Registrierung erfolgreich war.

  In folgenden Situation wird der Task „Schedule created by enrollment client for automatically enrolling in MDM from AAD“ (Vom Registrierungsclient erstellter Zeitplan für die automatische Registrierung bei MDM über AAD) ggf. nicht gestartet:

  - Das Gerät ist bereits bei einer anderen MDM-Lösung registriert. In diesem Fall werden die Ereignis-ID 7016 und der Fehlercode 2149056522 im Ereignisprotokoll unter **Anwendungs- und Dienstprotokolle** > **Microsoft** > **Windows** > **Taskplaner** > **Betrieb** erfasst.

    Heben Sie die Registrierung des Geräts bei MDM auf, um dieses Problem zu beheben.

  - Es liegt ein Problem mit der Gruppenrichtlinie vor. Erzwingen Sie in diesem Fall ein Update der Gruppenrichtlinieneinstellungen, indem Sie folgenden Befehl ausführen:

    **gpupdate /force**

    Wenn das Problem weiterhin besteht, sollten Sie in Active Directory Domain Services weitere Problembehandlungsschritte einleiten.

## <a name="next-steps"></a>Nächste Schritte
[Behandlung von Problemen bei der Registrierung von Windows-Geräten](troubleshoot-windows-enrollment-errors.md)