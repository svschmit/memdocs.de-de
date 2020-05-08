---
title: Einstellungen für Intune-Sicherheitsbaselines für Microsoft Edge
titleSuffix: Microsoft Intune
description: Von Intune unterstützte Einstellungen für Sicherheitsbaselines zur Verwaltung des Microsoft Edge-Browsers
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
ms.topic: reference
ms.service: microsoft-intune
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
zone_pivot_groups: edge-baseline-versions
ms.reviewer: laarrizz
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 861d7f526711f2169e8fd03b3df09659440523b9
ms.sourcegitcommit: a4ec80c5dd51e40f3b468e96a71bbe29222ebafd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82693456"
---
<!-- Pivots in use: 
::: zone pivot="edge-october-2019"
::: zone-end

::: zone pivot="edge-april-2020"
::: zone-end

::: zone pivot="edge-october-2019,edge-april-2020"
::: zone-end
-->

# <a name="microsoft-edge-baseline-settings-for-intune"></a>Microsoft Edge-Baselineeinstellungen für Intune

Machen Sie sich mit den Baselineeinstellungen für den Microsoft Edge-Webbrowser vertraut, die von Microsoft Intune unterstützt werden. Die Standardeinstellungen der Microsoft Edge-Baseline entsprechen der für Microsoft Edge empfohlenen Konfiguration und stimmen möglicherweise nicht mit den Standardeinstellungen anderer Sicherheitsbaselines überein.

::: zone pivot="edge-october-2019"

> [!NOTE]
> Die Microsoft Edge-Baseline für Oktober 2019 befindet sich in Public Preview.

::: zone-end
::: zone pivot="edge-april-2020"

*Diese neue Baseline wird über die nächsten Wochen für Mandanten eingeführt. Wir gehen davon aus, dass allen Mandanten diese neue Baseline Anfang Mai zur Verfügung steht.*
Verwenden Sie die im Bereich *Versionen* für diese Baseline verfügbare Aktion [Compare baselines](../protect/security-baselines.md#compare-baseline-versions) (Baselines vergleichen), um zu sehen, was sich in dieser Version der Baseline im Vergleich zu früheren Versionen geändert hat.

::: zone-end
::: zone pivot="edge-october-2019,edge-april-2020"

## <a name="microsoft-edge"></a>Microsoft Edge

::: zone-end
::: zone pivot="edge-april-2020"

- **Unterstützte Authentifizierungsschemas**  
  Gibt an, welche HTTP-Authentifizierungsschemas unterstützt werden. Sie können die Richtlinie mit den folgenden Werten konfigurieren: *basic*, *digest*, *ntlm* und *negotiate*. Trennen Sie mehrere Werte durch Kommas voneinander ab. Wenn Sie diese Richtlinie nicht konfigurieren, werden alle vier Schemas verwendet.

  - **Aktiviert** (*Standardeinstellung*): Von Ihnen ausgewählte Schemas werden verwendet.
  - **Deaktiviert**
  - **Nicht konfiguriert**: Alle vier Schemas werden verwendet.
  
  Wenn die Einstellung auf *Aktiviert* festgelegt ist, können Sie die folgende Einstellung konfigurieren, bei der Sie auswählen, welche Authentifizierung verwendet werden soll:

  - **Unterstützte Authentifizierungsschemas**  
    Wählen Sie eine der folgenden Optionen aus:
    - **Basic**
    - **Digest**
    - **NTLM** *(Standardeinstellung)*
    - **Negotiate** *(Standardeinstellung)*

- **Standardeinstellung für Adobe Flash**  
  CSP: [Browser/AllowFlash](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowflash) und [Browser/AllowFlashClickToRun](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowflashclicktorun)

  Aktivieren Sie den Zugriff auf die folgende Einstellung, in der Sie das Verhalten für die Ausführung des Adobe Flash-Plug-Ins konfigurieren können.  

  - **Aktiviert** (*Standardeinstellung*)
  - **Deaktiviert**
  - **Nicht konfiguriert**

  Wenn *Aktiviert* festgelegt ist, können Sie die folgende Einstellung konfigurieren.

  - **Standardeinstellung für Adobe Flash**

    - **Adobe Flash-Plug-In blockieren** (*Standardeinstellung*): Blockieren Sie Adobe Flash auf allen Websites.
    - **Zur Wiedergabe klicken**: Adobe Flash wird ausgeführt, aber der Benutzer muss die Option auswählen, um sie zu starten.

- **Nicht installierbare Erweiterungen steuern**  
  Aktivieren Sie die Verwendung einer Liste, die Erweiterungen angibt, die Benutzer nicht in Microsoft Edge installieren können. Wenn die Liste verwendet wird, werden alle Einstellungen auf der Liste, die zuvor installiert wurden, deaktiviert, und der Benutzer kann sie nicht aktivieren. Wenn Sie ein Element aus der Liste der blockierten Erweiterungen entfernen, wird diese Erweiterung automatisch überall dort erneut aktiviert, wo sie zuvor installiert wurde.

  - **Aktiviert** (*Standardeinstellung*): Aktivieren Sie die Verwendung der Liste, um Erweiterungen zu blockieren.
  - **Deaktiviert**
  - **Nicht konfiguriert**: Benutzer können eine beliebige Erweiterung in Microsoft Edge installieren.
  
  Wenn die Einstellung auf *Aktiviert* festgelegt ist, können Sie die folgende Einstellung konfigurieren, die die Liste der zu blockierenden Erweiterungen definiert.

  - **Erweiterungs-IDs, an deren Installation der Benutzer gehindert werden soll (oder * für alle)**

    Klicken Sie auf **Hinzufügen**, und geben Sie zusätzliche Erweiterungen an. **\*** ist standardmäßig ausgewählt.

- **Native Messaginghosts auf Benutzerebene zulassen (Installation ohne Administratorberechtigungen)**  
  Aktiviert die Installation nativer Messaginghosts auf Benutzerebene.

  - **Enabled**
  - **Deaktiviert** (*Standardeinstellung*): Microsoft Edge verwendet nur native Messaginghosts, die auf Systemebene installiert sind.
  - **Nicht konfiguriert**: Standardmäßig gestattet Microsoft Edge die Verwendung von nativen Messaginghosts auf Benutzerebene.

- **Speichern von Kennwörtern im Kennwort-Manager aktivieren**  
  Microsoft Edge CSP: [Browser/AllowPasswordManager](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)  

  Hiermit ermöglichen Sie Microsoft Edge das Speichern von Benutzerkennwörtern.

  - **Aktiviert**: Benutzer können ihre Kennwörter in Microsoft Edge speichern. Beim nächsten Besuch der Website wird das Kennwort von Microsoft Edge automatisch eingegeben. Benutzer können diese Richtlinie in Microsoft Edge nicht ändern oder außer Kraft setzen.
  - **Deaktiviert** (*Standardeinstellung*): Benutzer können keine neuen Kennwörter speichern, können aber zuvor gespeicherte Kennwörter weiterhin verwenden. Benutzer können diese Richtlinie in Microsoft Edge nicht ändern oder außer Kraft setzen.
  - **Nicht konfiguriert**: Benutzer können Kennwörter speichern und dieses Feature deaktivieren.

- **Umgehung von Microsoft Defender SmartScreen-Eingabeaufforderungen für Websites verhindern**  
  CSP: [Browser/PreventSmartScreenPromptOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

  Sie können entscheiden, ob Benutzer die Microsoft Defender SmartScreen-Warnungen zu potenziell schädlichen Websites außer Kraft setzen können.

  - **Aktiviert** (*Standardeinstellung*): Wenn Sie diese Einstellung aktivieren, können Benutzer keine Microsoft Defender SmartScreen-Warnungen ignorieren und sind nicht mehr in der Lage, die Website weiter zu nutzen.
  - **Deaktiviert**: Benutzer können Microsoft Defender SmartScreen-Warnungen ignorieren und mit der Nutzung der Website fortfahren.
  - **Nicht konfiguriert**: Benutzer können die Microsoft Defender SmartScreen-Warnungen ignorieren und mit der Website fortfahren.

- **Umgehung von Microsoft Defender SmartScreen-Warnungen zu Downloads verhindern**  
  CSP: [Browser/PreventSmartScreenPromptOverrideForFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)  

  Bestimmen Sie, ob Benutzer Microsoft Defender SmartScreen-Warnungen zu nicht überprüften Downloads außer Kraft setzen können.

  - **Aktiviert** (*Standardeinstellung*): Benutzer können Microsoft Defender SmartScreen-Warnungen nicht ignorieren und werden am Abschließen der nicht überprüften Downloads gehindert.
  - **Deaktiviert**: Benutzer können Microsoft Defender SmartScreen-Warnungen ignorieren und nicht überprüfte Downloads abschließen.
  - **Nicht konfiguriert**: Benutzer können Microsoft Defender SmartScreen-Warnungen ignorieren und nicht überprüfte Downloads abschließen.

- **Website-Isolation für jede Website aktivieren**  
  Konfigurieren Sie die Website-Isolation, um zu verhindern, dass Benutzer das Standardverhalten der Isolation aller Websites ablehnen.
  
  - **Aktiviert** (*Standardeinstellung*): Benutzer können das Standardverhalten nicht deaktivieren, bei dem jede Website in einem eigenen Prozess ausgeführt wird.
  - **Deaktiviert**: Benutzer können die Website-Isolation deaktivieren. Die Website-Isolation ist nicht deaktiviert.
  - **Nicht konfiguriert**: Benutzer können die Website-Isolation deaktivieren. Die Website-Isolation ist nicht deaktiviert.

  Microsoft Edge unterstützt auch die Richtlinie [IsolateOrigins](https://docs.microsoft.com/deployedge/microsoft-edge-policies#isolateorigins), die zusätzliche, differenziertere Ursprünge isolieren kann.  Intune unterstützt nicht die Konfiguration der Richtlinie „IsolateOrigins“.
  
- **Microsoft Defender SmartScreen konfigurieren**  
  CSP: [Browser/AllowSmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)  
  
  Microsoft Defender SmartScreen stellt Warnmeldungen bereit, um Benutzer vor potenziellem Phishingbetrug und schädlicher Software zu schützen. Microsoft Defender SmartScreen ist standardmäßig aktiviert.
  
  - **Aktiviert** (*Standardeinstellung*): Microsoft Defender SmartScreen wird aktiviert, und Benutzer können die Einstellung nicht deaktivieren.
  - **Deaktiviert**: Microsoft Defender SmartScreen wird deaktiviert, und Benutzer können die Einstellung nicht aktivieren.
  - **Nicht konfiguriert**: Benutzer können auswählen, ob Microsoft Defender SmartScreen verwendet werden soll.

  Diese Richtlinie ist nur auf Windows-Instanzen verfügbar, die einer Microsoft Active Directory-Domäne angehören, oder auf Windows 10 Pro- oder Enterprise-Instanzen, die für die Geräteverwaltung registriert sind.

- **Microsoft Defender SmartScreen zum Blockieren potenziell unerwünschter Apps konfigurieren**  
    Konfigurieren Sie das Microsoft Defender SmartScreen-Verhalten zum Blockieren potenziell unerwünschter Anwendungen. Microsoft Defender SmartScreen kann Warnmeldungen bereitstellen, um Benutzer vor Adware, Coin Mining, Bundleware und anderen unseriösen Anwendungen zu schützen, die von Websites gehostet werden. Die Blockierung potenziell unerwünschter Apps ist in Microsoft Defender SmartScreen standardmäßig deaktiviert.

  - **Aktiviert** (*Standardeinstellung*): Potenziell unerwünschte Apps werden blockiert.
  - **Deaktiviert**: Potenziell unerwünschte Apps werden nicht blockiert.
  - **Nicht konfiguriert**: Benutzer können auswählen, ob sie potenziell unerwünschte App-Blockierungen in Microsoft Defender SmartScreen verwenden möchten.

  Diese Richtlinie ist nur auf Windows-Instanzen verfügbar, die einer Microsoft Active Directory-Domäne angehören, oder auf Windows 10 Pro- oder Enterprise-Instanzen, die für die Geräteverwaltung registriert sind.

- **Benutzern das Fortfahren von der SSL-Warnungsseite erlauben**  
   CSP: [Browser/PreventCertErrorOverrides](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventcerterroroverrides)  

  Microsoft Edge zeigt eine Warnseite an, wenn Benutzer Websites mit SSL-Fehlern besuchen.
  - **Aktiviert**: Benutzer können sich durch die Warnungsseiten klicken.
  - **Aktiviert** (*Standardeinstellung*): Benutzer werden daran gehindert, sich durch eine Warnungsseite zu klicken.
  - **Nicht konfiguriert**: Benutzer können sich durch diese Warnungsseiten klicken.

- **SSL-Mindestversion aktiviert**  
  Aktivieren Sie die Option, eine Mindestversion von SSL festzulegen.

  - **Aktiviert** (*Standardeinstellung*): Aktivieren Sie den Zugriff auf die nächste Einstellung, bei der Sie die zu verwendende Mindestversion von TLS angeben.
  - **Deaktiviert**
  - **Nicht konfiguriert**: Microsoft Edge verwendet eine standardmäßig Mindestversion von *TLS 1.0*.

  Wenn *Aktiviert* festgelegt ist, können Sie TLS mithilfe der folgenden Einstellung konfigurieren.

  - **SSL-Mindestversion aktiviert**: Legen Sie die zu verwendende Mindestversion von TLS fest. Microsoft Edge verwendet keine SSL/TLS-Version, die niedriger als die angegebene Version ist.
    - **TLS 1.0**
    - **TLS 1.1**
    - **TLS 1.2** (*Standardeinstellung*)

::: zone-end

::: zone pivot="edge-october-2019"

- **Umgehung von Microsoft Defender SmartScreen-Eingabeaufforderungen für Websites verhindern**  
  **Standardeinstellung:** Aktiviert  
  Microsoft Edge CSP: [Browser/PreventSmartScreenPromptOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

  Mit dieser Richtlinieneinstellung können Sie festlegen, ob Benutzer die Microsoft Defender SmartScreen-Warnungen zu potenziell schädlichen Websites außer Kraft setzen können. 
  - Wenn Sie diese Einstellung aktivieren, können Benutzer keine Microsoft Defender SmartScreen-Warnungen ignorieren und sind nicht mehr in der Lage, die Website weiter zu nutzen. 
  - Wenn Sie diese Einstellung deaktivieren oder nicht konfigurieren, können Benutzer Microsoft Defender SmartScreen-Warnungen ignorieren und mit der Nutzung der Website fortfahren.

- **SSL-Mindestversion aktiviert**  
  **Standardeinstellung:** Aktiviert  

  Legen Sie eine unterstützte Mindestversion von SSL fest. Wenn Sie diese Richtlinie auf *Nicht konfiguriert* festlegen, verwendet Microsoft Edge standardmäßig die Mindestversion *TLS 1.0*. Wenn Sie sie auf *Aktiviert* festgelegt haben, können Sie eine Mindestversion aus den folgenden Werten auswählen:

  - TLS 1.0
  - TLS 1.1
  - TLS 1.2

  - **SSL-Mindestversion aktiviert**  
    **Standardeinstellung:** TLS 1.2

- **Umgehung von Microsoft Defender SmartScreen-Warnungen zu Downloads verhindern**  
  **Standardeinstellung:** Aktiviert  
  Microsoft Edge CSP: [Browser/PreventSmartScreenPromptOverrideForFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)  

  Mit dieser Richtlinie können Sie festlegen, ob Benutzer Microsoft Defender SmartScreen-Warnungen zu nicht überprüften Downloads außer Kraft setzen können.
  - Wenn Sie diese Richtlinie aktivieren, können Benutzer in Ihrer Organisation Microsoft Defender SmartScreen-Warnungen nicht ignorieren und werden am Abschließen der nicht überprüften Downloads gehindert.
  - Wenn Sie diese Richtlinie deaktivieren oder nicht konfigurieren, können Benutzer Microsoft Defender SmartScreen-Warnungen ignorieren und nicht überprüfte Downloads abschließen.

- **Benutzern das Fortfahren von der SSL-Warnungsseite erlauben**  
  **Standardeinstellung:** Deaktiviert  
  Microsoft Edge CSP: [Browser/PreventCertErrorOverrides](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventcerterroroverrides)  

  Microsoft Edge zeigt eine Warnseite an, wenn Benutzer Websites mit SSL-Fehlern besuchen. Wenn Sie diese Richtlinie auf *Aktiviert* oder *Nicht konfiguriert* festlegen, können Benutzer diese Warnseiten ignorieren. Wenn diese Richtlinie auf *Deaktiviert* festgelegt ist, können Benutzer diese Warnseiten nicht ignorieren. 

- **Standardeinstellung für Adobe Flash**  
  **Standardeinstellung:** Aktiviert  
  Microsoft Edge CSP: [Browser/AllowFlash](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowflash) und [Browser/AllowFlashClickToRun](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowflashclicktorun)  

  Legt fest, ob Websites, die nicht von „PluginsAllowedForUrls“ oder „PluginsBlockedForUrls“ abgedeckt werden, das Adobe Flash-Plug-In automatisch ausführen können. 

  - Wählen Sie „BlockPlugins“ aus, um Adobe Flash auf allen Websites zu blockieren.
  - Wählen Sie „ClickToPlay“ aus, damit Adobe Flash zwar ausgeführt wird, aber der Benutzer auf den Platzhalter klicken muss, um das Plug-In zu starten.
  
  Die Richtlinien „PluginsAllowedForUrls“ und „PluginsBlockedForUrls“ haben immer Vorrang vor „DefaultPluginsSetting“. Die automatische Wiedergabe ist nur für Domänen zulässig, die in der Richtlinie „PluginsAllowedForUrls“ explizit aufgeführt werden. 
   Wenn Sie die automatische Wiedergabe für alle Websites aktivieren möchten, können Sie dieser Liste http://* und https://* hinzufügen.

  - Wenn Sie diese Richtlinie auf *Nicht konfiguriert* festlegen, kann der Benutzer diese Einstellung manuell ändern. * 2 = Adobe Flash-Plug-In blockieren, * 3 = Klicken, um Inhalte wiederzugeben – die frühere Option „1“ legt „Alle zulassen“ fest, diese Funktion wird jedoch jetzt von der Richtlinie „PluginsAllowedForUrls“ übernommen. Vorhandene Richtlinien, die „1“ verwenden, werden im Click-to-Play-Modus ausgeführt.  

  - **Standardeinstellung für Adobe Flash**  
    **Standardeinstellung:** Adobe Flash-Plug-In blockieren

- **Website-Isolation für jede Website aktivieren**  
  **Standardeinstellung:** Aktiviert  

  Die Richtlinie „SitePerProcess“ kann verwendet werden, um zu verhindern, dass Benutzer das Standardverhalten der Isolierung aller Websites ablehnen. Sie können auch die Richtlinie „IsolateOrigins“ verwenden, um zusätzliche, differenziertere Ursprünge zu isolieren.

  - Wenn diese Richtlinie auf *Aktiviert* festgelegt ist, können Benutzer das Standardverhalten nicht deaktivieren, wenn jede Website in einem eigenen Prozess ausgeführt wird. 
  - Wenn Sie *Deaktiviert* oder *Nicht konfiguriert* verwenden, kann der Benutzer die Isolation von Websites deaktivieren. Hierfür kann beispielsweise der Eintrag zum Deaktivieren der Isolation von Websites in edge://flags verwendet werden. Wenn Sie die Richtlinie deaktivieren oder nicht konfigurieren, wird die Isolation von Websites nicht deaktiviert.

- **Unterstützte Authentifizierungsschemas**  
  **Standardeinstellung:** Aktiviert  

  Gibt an, welche HTTP-Authentifizierungsschemas unterstützt werden. Sie können die Richtlinie mit den folgenden Werten konfigurieren: basic, digest, ntlm und negotiate. Trennen Sie mehrere Werte durch Kommas voneinander ab. Wenn Sie diese Richtlinie nicht konfigurieren, werden alle vier Schemas verwendet.

  - **Unterstützte Authentifizierungsschemas**  
    Wählen Sie eine der folgenden Optionen aus:
    - Einfach
    - Digest
    - Integrierte Windows-Authentifizierung (NTLM) *(Standardeinstellung)*
    - Negotiate *(Standardeinstellung)*

- **Speichern von Kennwörtern im Kennwort-Manager aktivieren**  
  **Standardeinstellung:** Deaktiviert  
  Microsoft Edge CSP: [Browser/AllowPasswordManager](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)  

  Hiermit ermöglichen Sie Microsoft Edge das Speichern von Benutzerkennwörtern.
  - Wenn Sie diese Richtlinie aktivieren, können Benutzer ihre Kennwörter in Microsoft Edge speichern. Beim nächsten Besuch der Website wird das Kennwort von Microsoft Edge automatisch eingegeben.
  - Wenn Sie diese Richtlinie deaktivieren, können Benutzer keine neuen Kennwörter speichern. Zuvor gespeicherte Kennwörter können jedoch weiterhin verwendet werden.
  
  Wenn Sie diese Richtlinie auf *Aktiviert* oder *Deaktiviert* festlegen, kann sie von Benutzern in Microsoft Edge nicht geändert oder außer Kraft gesetzt werden.
  
  Wenn Sie diese Option auf *Nicht konfiguriert* festlegen, können Benutzer Kennwörter speichern oder dieses Feature deaktivieren.

- **Nicht installierbare Erweiterungen steuern**  
  **Standardeinstellung:** Aktiviert  

  Listet die spezifischen Erweiterungen auf, die Benutzer in Microsoft Edge nicht installieren können. Wenn Sie diese Richtlinie bereitstellen, werden alle zuvor installierten Erweiterungen in dieser Liste deaktiviert, und Benutzer sind nicht in der Lage, sie zu aktivieren. Wenn Sie ein Element aus der Liste der blockierten Erweiterungen entfernen, wird diese Erweiterung automatisch überall dort erneut aktiviert, wo sie zuvor installiert wurde.
  
  Verwenden Sie **\*** , um alle Erweiterungen zu blockieren, die nicht explizit in der Zulassungsliste aufgeführt werden. Wenn diese Richtlinie auf *Nicht konfiguriert* festgelegt ist, können Benutzer jede Erweiterung in Microsoft Edge installieren.
  
  Beispielwert: extension_id1, extension_id2.  
  <br>
  - **Erweiterungs-IDs, an deren Installation der Benutzer gehindert werden soll (oder * für alle)**  
    Klicken Sie auf **Hinzufügen**, und geben Sie zusätzliche Erweiterungen an. **\*** ist standardmäßig ausgewählt.

- **Microsoft Defender SmartScreen konfigurieren**  
  **Standardeinstellung:** Aktiviert  
  Microsoft Edge CSP: [Browser/AllowSmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

  Mit dieser Richtlinieneinstellung können Sie konfigurieren, ob Microsoft Defender SmartScreen aktiviert werden soll. Microsoft Defender SmartScreen stellt Warnmeldungen bereit, um Ihre Benutzer vor potenziellem Phishingbetrug und schädlicher Software zu schützen.
  
  - Microsoft Defender SmartScreen ist standardmäßig aktiviert. Wenn Sie diese Einstellung aktivieren, wird Microsoft Defender SmartScreen aktiviert, und Benutzer können die Einstellung nicht deaktivieren.
  - Wenn Sie diese Einstellung deaktivieren, wird Microsoft Defender SmartScreen deaktiviert, und Benutzer können die Einstellung nicht aktivieren.
  - Wenn Sie diese Einstellung auf *Nicht konfiguriert* festlegen, können Benutzer auswählen, ob Microsoft Defender SmartScreen verwendet werden soll.
  
  Diese Richtlinie ist nur auf Windows-Instanzen verfügbar, die einer Microsoft Active Directory-Domäne angehören, oder auf Windows 10 Pro- oder Enterprise-Instanzen, die für die Geräteverwaltung registriert sind.

- **Native Messaginghosts auf Benutzerebene zulassen (Installation ohne Administratorberechtigungen)**  
  **Standardeinstellung:** Deaktiviert

  Aktiviert die Installation nativer Messaginghosts auf Benutzerebene. 
  - Wenn Sie diese Richtlinie deaktivieren, verwendet Microsoft Edge nur auf Systemebene installierte native Messaginghosts. Wenn Sie diese Richtlinie nicht konfigurieren, lässt Microsoft Edge standardmäßig die Verwendung nativer Messaginghosts auf Benutzerebene zu.

::: zone-end

## <a name="next-steps"></a>Nächste Schritte

- [Informationen zu Sicherheitsbaselines](security-baselines.md)
- [Vermeiden von Konflikten](security-baselines.md#avoid-conflicts)
- [Richtlinien und Profile zur Problembehandlung in Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)
