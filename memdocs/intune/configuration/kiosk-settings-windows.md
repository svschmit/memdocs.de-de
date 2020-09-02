---
title: Kioskeinstellungen für Windows 10 in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Konfigurieren Sie Ihre Geräte mit Windows 10 (und höher) als Kiosks mit einer App oder mehreren Apps, und passen Sie das Startmenü an, fügen Sie Apps hinzu, zeigen Sie die Taskleiste an und konfigurieren Sie einen Webbrowser in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/21/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6a37b94ee0e474e9e3da6aae359ba1b315212910
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88911929"
---
# <a name="windows-10-and-later-device-settings-to-run-as-a-kiosk-in-intune"></a>Geräteeinstellungen bei Windows 10 (und höher) zur Ausführung als Kiosk in Intune

Sie können Geräte mit Windows 10 und höher so konfigurieren, dass sie im Single-App- oder im Multi-App-Kioskmodus ausgeführt werden.

In diesem Artikel werden die verschiedenen Einstellungen aufgeführt und beschrieben, die Sie auf Geräten mit Windows 10 und höher festlegen können. Als Bestandteil Ihrer Lösung für die mobile Geräteverwaltung (Mobile Device Management, MDM) verwenden Sie diese Einstellungen, um Ihre Geräte mit Windows 10 und höher für die Ausführung im Kioskmodus zu konfigurieren.

Als Intune-Administrator können Sie Ihre Geräte diese Einstellungen erstellen und zuweisen.

Weitere Informationen zur Windows-Kioskfunktion in Intune finden Sie unter [Konfigurieren der Kiosk-Einstellungen](kiosk-settings.md).

## <a name="before-you-begin"></a>Vorbereitung

- [Erstellen Sie das Profil.](kiosk-settings.md#create-the-profile)

- Dieses Kioskprofil steht in direktem Zusammenhang mit dem Geräteeinschränkungsprofil, das Sie mithilfe der [Microsoft Edge-Kioskeinstellungen](device-restrictions-windows-10.md#microsoft-edge-browser) erstellen. Zusammenfassung:

  1. Erstellen Sie das Kioskprofil, um das Gerät im Kioskmodus auszuführen.
  2. Erstellen Sie das [Geräteeinschränkungsprofil](device-restrictions-windows-10.md#microsoft-edge-browser), und konfigurieren Sie spezifische Features und Einstellungen, die in Microsoft Edge zulässig sind.

- Stellen Sie sicher, dass sich alle Dateien, Skripts und Verknüpfungen auf dem lokalen System befinden. Weitere Informationen einschließlich anderer Windows-Anforderungen finden Sie unter [Anpassen und Exportieren des Startlayouts](/windows/configuration/customize-and-export-start-layout).

> [!IMPORTANT]
> Achten Sie darauf, dass Sie dieses Kioskprofil den gleichen Geräten wie Ihr [Microsoft Edge-Profil](device-restrictions-windows-10.md#microsoft-edge-browser) zuweisen.

## <a name="single-app-full-screen-kiosk"></a>Einzelne App, Vollbildkiosk

Hiermit wird nur eine App auf dem Gerät ausgeführt.

- **Kioskmodus auswählen**: Wählen Sie **Single app, full-screen kiosk** (Einzelne App, Vollbildkiosk) aus.

- **Typ der Benutzeranmeldung:** Wählen Sie den Kontotyp aus, der die App ausführt. Folgende Optionen sind verfügbar:

  - **Automatische Anmeldung (Windows 10, Version 1803 und neuer):** Verwenden Sie diese Option für Kiosks in öffentlichen Umgebungen, die ähnlich einem Gastkonto keine Benutzeranmeldung erfordern. Diese Einstellung verwendet [AssignedAccess CSP](/windows/client-management/mdm/assignedaccess-csp).
  - **Lokales Benutzerkonto:** Geben Sie das lokale Benutzerkonto (auf dem Gerät) an. Das von Ihnen eingegebene Konto wird zum Anmelden im Kiosk verwendet.

- **Anwendungstyp:** Wählen Sie den Anwendungstyp aus. Folgende Optionen sind verfügbar:

  - **Microsoft Edge-Browser hinzufügen**: Klicken Sie auf **Microsoft Edge-Browser**, und wählen Sie den **Microsoft Edge-Kioskmodustyp** aus:

    - **Digitale/interaktive Beschilderung**: Durch diese Option wird eine URL im Vollbildmodus geöffnet, und es wird nur der Inhalt dieser Website angezeigt. Weitere Informationen zu diesem Feature finden Sie unter [Einrichten digitaler Beschilderungen](/windows/configuration/setup-digital-signage).
    - **Öffentliches Browsen (InPrivate)** : Durch diese Option wird eine Version von Microsoft Edge mit mehreren Registerkarten ausgeführt. Benutzer können öffentlich browsen oder ihre Sitzung beenden.

    Weitere Informationen zu diesen Optionen finden Sie unter [Bereitstellen des Microsoft Edge-Kioskmodus](/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types).

    > [!NOTE]
    > Mit dieser Einstellung wird der Microsoft Edge-Browser auf dem Gerät aktiviert. Erstellen Sie zum Konfigurieren spezifischer Microsoft Edge-Einstellungen ein Geräteeinschränkungsprofil (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > **Windows 10** (Plattform) > **Geräteeinschränkungen** > **Microsoft Edge-Browser**). Der [Microsoft Edge-Browser](device-restrictions-windows-10.md#microsoft-edge-browser) führt alle Einstellungen und Beschreibungen dieser auf.

  - **Kioskbrowser hinzufügen**: Klicken Sie auf **Einstellungen für Kioskbrowser**. Mit diesen Einstellungen können Sie die Webbrowser-App im Kiosk steuern. Laden Sie die [Kioskbrowser-App](https://businessstore.microsoft.com/store/details/kiosk-browser/9NGB5S5XG2KP) aus dem Store herunter, und fügen Sie sie Intune als [Client-App](../apps/apps-add.md) hinzu. Ordnen Sie sie anschließend den Kioskgeräten zu.

    Legen Sie folgende Einstellungen fest:

    - **URL der Standardhomepage:** Geben Sie die Standard-URL ein, die angezeigt wird, wenn der Kioskbrowser geöffnet oder neu gestartet wird. Geben Sie beispielsweise `http://bing.com` oder `http://www.contoso.com` ein.

    - **Startschaltfläche:** Sie können die Startschaltfläche des Kioskbrowsers **einblenden** oder **ausblenden**. Standardmäßig wird die Schaltfläche ausgeblendet.

    - **Navigationsschaltflächen:** Sie können die Schaltflächen „Weiter“ und „Zurück“ **einblenden** oder **ausblenden**. Standardmäßig werden sie ausgeblendet.

    - **Schaltfläche „Sitzung beenden“:** Sie können die Schaltfläche „Sitzung beenden“ **einblenden** oder **ausblenden**. Wenn die Schaltfläche angezeigt wird, tippt der Benutzer darauf, und die App fragt, ob die Sitzung beendet werden soll. Wenn dies bestätigt wird, löscht der Browser alle Browserdaten (z.B. Cookies und Cache) und öffnet dann die Standard-URL. Standardmäßig wird die Schaltfläche ausgeblendet.

    - **Browser nach Leerlaufzeit aktualisieren:** Geben Sie die Leerlaufzeit ein (1 bis 1.440 Minuten), nach der der Kioskbrowser im aktualisierten Zustand neu gestartet wird. Die Leerlaufzeit ist die Anzahl von Minuten seit der letzten Benutzerinteraktion. Standardmäßig ist der Wert leer, d.h., es gibt kein Leerlauftimeout.

    - **Zulässige Websites:** Verwenden Sie diese Einstellung, um das Öffnen bestimmter Websites zu ermöglichen. Mithilfe dieser Funktion können Sie also auf dem Gerät den Zugriff auf bestimmte Websites einschränken oder verhindern. Sie können z.B. gewähren, dass alle Websites unter `http://contoso.com` geöffnet werden. Standardmäßig sind alle Websites zulässig.

      Um den Zugriff auf bestimmte Websites zu erlauben, laden Sie eine Datei mit einer in Zeilen unterteilten Liste der zulässigen Websites hoch. Wenn Sie keine Datei hinzufügen, können alle Websites aufgerufen werden. Standardmäßig erlaubt Intune alle Unterdomänen der Website. Beispielsweise können Sie die Domäne `sharepoint.com` eingeben. Intune lässt automatisch alle Unterdomänen zu, z. B. `contoso.sharepoint.com`, `my.sharepoint.com` usw. Geben Sie keine Platzhalterzeichen wie das Sternchen (`*`) ein.

      Die Beispieldatei sollte der folgenden Beispielliste ähnlich sein:

      `http://bing.com`  
      `https://bing.com`  
      `http://contoso.com`  
      `https://contoso.com`  
      `office.com`

    > [!NOTE]
    > Bei Windows 10-Kiosken mit automatischer Anmeldung, die mit dem Microsoft-Kioskbrowser aktiviert wird, muss eine Offlinelizenz aus dem Microsoft Store für Unternehmen verwendet werden. Diese Anforderung besteht, da bei der automatischen Anmeldung ein lokales Benutzerkonto ohne AD-Anmeldeinformationen (Azure Active Directory) verwendet wird. Onlinelizenzen können daher nicht ausgewertet werden. Weitere Informationen finden Sie unter [Verteilen von Offline-Apps](/microsoft-store/distribute-offline-apps).

  - **Store-App hinzufügen**: Klicken Sie auf **Store-App hinzufügen**, und wählen Sie eine App aus der Liste aus.

    Es sind keine Apps aufgelistet? Fügen Sie einige mithilfe der Schritte unter [Client-Apps](../apps/apps-add.md) hinzu.

- **Wartungsfenster für App-Neustarts angeben**: Einige Apps müssen neu gestartet werden, um die App-Installation oder die Installation von Updates abzuschließen. **Anfordern** erstellt ein Wartungsfenster. Wenn die App einen Neustart erfordert, wird sie während dieses Fensters neu gestartet.

  Geben Sie außerdem Folgendes ein:

  - **Startzeit des Wartungsfensters**: Wählen Sie das Datum und die Uhrzeit aus, zu der die Überprüfung von Clients auf App-Updates gestartet werden soll, die einen Neustart erfordern. Die Standardzeit für den Start ist auf Mitternacht bzw. null Minuten festgelegt. Wenn der Wert leer ist, werden Apps 3 Tage nach der Installation eines App-Updates zu einem ungeplanten Zeitpunkt neu gestartet.

  - **Wiederholung des Wartungsfensters**: Die Standardeinstellung sieht eine tägliche Wiederholung vor. Wählen Sie aus, wie oft Wartungsfenster für App-Updates bereitgestellt werden. Um nicht geplante App-Neustarts zu vermeiden, lautet die Empfehlung **Täglich**.

  Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

  [ApplicationManagement/ScheduleForceRestartForUpdateFailures CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-scheduleforcerestartforupdatefailures)

## <a name="multi-app-kiosk"></a>Kiosk mit mehreren Apps

Apps, die sich in diesem Modus befinden, sind über das Startmenü verfügbar. Diese Apps sind die einzigen Apps, die der Benutzer öffnen kann. Wenn bei einer App eine Abhängigkeit von einer anderen App vorliegt, müssen beide in der Liste zulässiger Apps enthalten sein. Internet Explorer (64-Bit) weist beispielsweise eine Abhängigkeit von Internet Explorer (32-Bit) auf, d. h., Sie müssen sowohl „C:\Programme\internet explorer\iexplore.exe“ als auch „C:\Programme (x86)\Internet Explorer\iexplore.exe“ zulassen. 

- **Kioskmodus auswählen**: Wählen Sie **Kiosk mit mehreren Apps** aus.

- **Geräte unter Windows 10 im S Modus als Ziel verwenden:**
  - **Ja**: Store-Apps und AUMID-Apps werden im Kioskprofil erlaubt. Win32-Apps werden ausgeschlossen.
  - **Nein**: Store-Apps, Win32-Apps und AUMID-Apps werden im Kioskprofil erlaubt. Dieses Kioskprofil wird auf Geräten im S-Modus nicht bereitgestellt.

- **Typ der Benutzeranmeldung:** Wählen Sie den Kontotyp aus, der Ihre Apps ausführt. Folgende Optionen sind verfügbar:

  - **Automatische Anmeldung (Windows 10, Version 1803 und höher):** Verwenden Sie diese Option für Kiosks in öffentlichen Umgebungen, die ähnlich einem Gastkonto keine Benutzeranmeldung erfordern. Diese Einstellung verwendet [AssignedAccess CSP](/windows/client-management/mdm/assignedaccess-csp).
  - **Lokales Benutzerkonto:** **Fügen Sie das lokale Benutzerkonto (auf dem Gerät) hinzu**. Das von Ihnen eingegebene Konto wird zum Anmelden im Kiosk verwendet.
  - **Azure AD-Benutzer oder Gruppe (Windows 10, Version 1803 und höher):** Klicken Sie auf **Hinzufüge**, und wählen Sie Azure AD-Benutzer oder Gruppen aus der Liste aus. Sie können mehrere Benutzer und Gruppen auswählen. Wählen Sie **OK** aus, um die Änderungen zu speichern.
  - **HoloLens-Besucher:** Beim Besucherkonto handelt es sich um ein Gastkonto, für das keine Anmeldeinformationen oder Authentifizierung erforderlich ist. Weitere Informationen dazu finden Sie unter [shared PC mode concepts (Konzepte für den Modus „Freigegebener Computer“)](/windows/configuration/set-up-shared-or-guest-pc#shared-pc-mode-concepts).

- **Browser und Anwendungen**: Wählen Sie die Apps aus, die auf dem Kioskgerät ausgeführt werden sollen. Denken Sie daran, dass Sie mehrere Apps hinzufügen können.

  :::image type="content" source="./media/kiosk-settings-windows/multi-app-kiosk-add-applications-browser.png" alt-text="Fügen Sie einem Kioskprofil mit mehreren Apps in Microsoft Intune Browser oder Apps hinzu.":::  

  - **Browser**

    - **Microsoft Edge hinzufügen**: Microsoft Edge wird dem App-Raster hinzugefügt, und alle Anwendungen können in diesem Kiosk ausgeführt werden. Wählen Sie den **Microsoft Edge-Kioskmodustyp** aus:

      - **Normalmodus (Vollversion von Microsoft Edge)** : Führt eine Vollversion von Microsoft Edge mit sämtlichen Funktionen für das Browsen aus. Benutzerdaten und -zustand werden zwischen Sitzungen beibehalten.
      - **Öffentliches Browsen (InPrivate)** : Hiermit wird eine Version von Microsoft Edge InPrivate mit mehreren Registerkarten mit einer für Kioske ausgelegten Benutzeroberfläche im Vollbildmodus ausgeführt.

      Weitere Informationen zu diesen Optionen finden Sie unter [Bereitstellen des Microsoft Edge-Kioskmodus](/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types).

      > [!NOTE]
      > Mit dieser Einstellung wird der Microsoft Edge-Browser auf dem Gerät aktiviert. Erstellen Sie zum Konfigurieren spezifischer Microsoft Edge-Einstellungen ein Geräteeinschränkungsprofil (**Geräte** > **Konfigurationsprofile** > **Profil erstellen** > >**Windows 10** (Plattform) > **Geräteeinschränkungen** >  **Microsoft Edge-Browser**). Der [Microsoft Edge-Browser](device-restrictions-windows-10.md#microsoft-edge-browser) führt alle Einstellungen und Beschreibungen dieser auf.

    - **Kioskbrowser hinzufügen**: Mit diesen Einstellungen können Sie die Webbrowser-App im Kiosk steuern. Achten Sie darauf, dass Sie eine Webbrowser-App auf dem Kioskgerät über [Client-Apps](../apps/apps-add.md) bereitstellen.

      Legen Sie folgende Einstellungen fest:

      - **URL der Standardhomepage:** Geben Sie die Standard-URL ein, die angezeigt wird, wenn der Kioskbrowser geöffnet oder neu gestartet wird. Geben Sie beispielsweise `http://bing.com` oder `http://www.contoso.com` ein.

      - **Startschaltfläche:** Sie können die Startschaltfläche des Kioskbrowsers **einblenden** oder **ausblenden**. Standardmäßig wird die Schaltfläche ausgeblendet.

      - **Navigationsschaltflächen:** Sie können die Schaltflächen „Weiter“ und „Zurück“ **einblenden** oder **ausblenden**. Standardmäßig werden sie ausgeblendet.

      - **Schaltfläche „Sitzung beenden“:** Sie können die Schaltfläche „Sitzung beenden“ **einblenden** oder **ausblenden**. Wenn die Schaltfläche angezeigt wird, tippt der Benutzer darauf, und die App fragt, ob die Sitzung beendet werden soll. Wenn dies bestätigt wird, löscht der Browser alle Browserdaten (z.B. Cookies und Cache) und öffnet dann die Standard-URL. Standardmäßig wird die Schaltfläche ausgeblendet.

      - **Browser nach Leerlaufzeit aktualisieren:** Geben Sie die Leerlaufzeit ein (1–1.440 Minuten), nach der der Kioskbrowser im aktualisierten Zustand neu gestartet wird. Die Leerlaufzeit ist die Anzahl von Minuten seit der letzten Benutzerinteraktion. Standardmäßig ist der Wert leer, d.h., es gibt kein Leerlauftimeout.

      - **Zulässige Websites:** Verwenden Sie diese Einstellung, um das Öffnen bestimmter Websites zu ermöglichen. Mithilfe dieser Funktion können Sie also auf dem Gerät den Zugriff auf bestimmte Websites einschränken oder verhindern. Sie können z.B. gewähren, dass alle Websites unter `contoso.com*` geöffnet werden. Standardmäßig sind alle Websites zulässig.

        Um den Zugriff auf bestimmte Websites zu erlauben, laden Sie eine CSV-Datei mit einer Liste der zulässigen Websites hoch. Wenn Sie keine CSV-Datei hinzufügen, können alle Websites aufgerufen werden.

      > [!NOTE]
      > Bei Windows 10-Kiosken mit automatischer Anmeldung, die mit dem Microsoft-Kioskbrowser aktiviert wird, muss eine Offlinelizenz aus dem Microsoft Store für Unternehmen verwendet werden. Diese Anforderung besteht, da bei der automatischen Anmeldung ein lokales Benutzerkonto ohne AD-Anmeldeinformationen (Azure Active Directory) verwendet wird. Onlinelizenzen können daher nicht ausgewertet werden. Weitere Informationen finden Sie unter [Verteilen von Offline-Apps](/microsoft-store/distribute-offline-apps).

  - **Anwendungen**

    - **Store-App hinzufügen:** Fügen Sie eine App aus dem Microsoft Store for Business hinzu. Wenn keine Apps aufgelistet sind, können Sie Apps abrufen und [Intune hinzufügen](../apps/store-apps-windows.md). Beispielsweise lassen sich der Kioskbrowser, Excel und OneNote hinzufügen.

    - **Win32-App hinzufügen:** Eine Win32-App ist eine klassische Desktop-App wie Visual Studio Code oder Google Chrome. Geben Sie die folgenden Eigenschaften ein:

      - **Anwendungsname:** Erforderlich. Geben Sie einen Namen für die Anwendung ein.
      - **Lokaler Pfad zur ausführbaren App-Datei**: Erforderlich. Geben Sie den Pfad zur ausführbaren Datei ein, z.B. `C:\Program Files (x86)\Microsoft VS Code\Code.exe` oder `C:\Program Files (x86)\Google\Chrome\Application\chrome.exe`.
      - **Geben Sie die AUMID (Application User Model ID) der Win32-App ein**: Geben Sie die AUMID der Win32-App ein. Diese Einstellung bestimmt das Startlayout der Kachel auf dem Desktop. Informationen zum Abrufen dieser ID finden Sie unter [Get-StartApps](/powershell/module/startlayout/get-startapps?view=win10-ps).

    - **Nach AUMID hinzufügen:** Mit dieser Option können Sie Windows-Posteingangs-Apps wie Editor oder Rechner hinzufügen. Geben Sie die folgenden Eigenschaften ein:

      - **Anwendungsname:** Erforderlich. Geben Sie einen Namen für die Anwendung ein.
      - **Anwendungsbenutzermodell-ID (AUMID):** Erforderlich. Geben Sie die AUMID der Windows-App ein. Weitere Informationen zum Abrufen dieser ID finden Sie unter [Ermitteln der Anwendungsbenutzermodell-ID einer installierten App](/windows-hardware/customize/enterprise/find-the-application-user-model-id-of-an-installed-app).

    - **AutoLaunch**: (Optional) Nachdem Sie Ihre Apps und Ihren Browser hinzugefügt haben, wählen Sie eine App oder einen Browser aus, die bzw. der jeweils automatisch geöffnet werden soll, wenn sich der Benutzer anmeldet. Nur eine App oder ein Browser kann automatisch gestartet werden.
    - **Kachelgröße:** Erforderlich. Nachdem Sie Ihre Apps hinzugefügt haben, wählen Sie eine kleine, mittlere, breite oder große App-Kachelgröße aus.

      :::image type="content" source="./media/kiosk-settings-windows/multi-app-kiosk-autolaunch-tiles.png" alt-text="Starten Sie die App oder den Browser automatisch, und wählen Sie in Microsoft Intune die Kachelgröße in einem Kioskprofil mit mehreren Apps aus.":::

  > [!TIP]
  > Nachdem Sie alle Apps hinzugefügt haben, können Sie die Anzeigereihenfolge ändern, indem Sie auf die Apps in der Liste klicken und sie dann verschieben.  

- **Alternatives Startlayout verwenden:** Wählen Sie **Ja** aus, um eine XML-Datei einzufügen, die beschreibt, wie die Apps im Startmenü dargestellt werden (z. B. die Reihenfolge der Apps). Verwenden Sie diese Option, wenn Sie in Ihrem Startmenü weitere Anpassungen vornehmen möchten. [Anpassen und Exportieren des Startlayouts](/windows/configuration/customize-and-export-start-layout): Bietet Anweisungen und XML-Beispiele.

- **Windows-Taskleiste:** Sie können die Taskleiste **einblenden** oder **ausblenden**. Standardmäßig wird sie ausgeblendet. Symbole, z.B. das WLAN-Symbol werden dargestellt, die Einstellungen können jedoch nicht vom Endbenutzer geändert werden.

- **Zugriff auf Downloadordner zulassen**: Klicken Sie auf **Ja**, um Benutzern den Zugriff auf den Downloadordner in Windows Explorer zu gewähren. Der Zugriff auf den Downloadordner ist standardmäßig deaktiviert. Dieses Feature wird häufig verwenden, um Endbenutzern den Zugriff auf Elemente zu gewähren, die über einen Browser heruntergeladen wurden.

- **Wartungsfenster für App-Neustarts angeben**: Einige Apps müssen neu gestartet werden, um die App-Installation oder die Installation von Updates abzuschließen. **Anfordern** erstellt ein Wartungsfenster. Wenn Apps einen Neustart erfordern, werden sie während dieses Fensters neu gestartet.

  Geben Sie außerdem Folgendes ein:

  - **Startzeit des Wartungsfensters**: Wählen Sie das Datum und die Uhrzeit aus, zu der die Überprüfung von Clients auf App-Updates gestartet werden soll, die einen Neustart erfordern. Die Standardzeit für den Start ist auf Mitternacht bzw. null Minuten festgelegt. Wenn der Wert leer ist, werden Apps 3 Tage nach der Installation eines App-Updates zu einem ungeplanten Zeitpunkt neu gestartet.

  - **Wiederholung des Wartungsfensters**: Die Standardeinstellung sieht eine tägliche Wiederholung vor. Wählen Sie aus, wie oft Wartungsfenster für App-Updates bereitgestellt werden. Um nicht geplante App-Neustarts zu vermeiden, lautet die Empfehlung **Täglich**.

  Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

  [ApplicationManagement/ScheduleForceRestartForUpdateFailures CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-scheduleforcerestartforupdatefailures)

## <a name="next-steps"></a>Nächste Schritte

[Weisen Sie das Profil zu](device-profile-assign.md), und [überwachen Sie seinen Status](device-profile-monitor.md).

Außerdem können Sie Kioskprofile für Geräte mit [Android](device-restrictions-android.md#kiosk), [Android Enterprise](device-restrictions-android-for-work.md#device-experience), and [Windows Holographic for Business](kiosk-settings-holographic.md) erstellen.

Weitere Informationen finden Sie unter [Einrichten eines Kiosks mit einer einzelnen App](/windows/configuration/kiosk-single-app) oder [Einrichten eines Kiosks mit mehreren Apps](/windows/configuration/lock-down-windows-10-to-specific-apps) im Windows-Leitfaden.