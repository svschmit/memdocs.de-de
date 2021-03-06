---
title: Einstellungen für Intune-Sicherheitsbaselines in Windows 10 MDM
titleSuffix: Microsoft Intune
description: Überprüfen Sie die Standardeinstellungen und die verfügbaren Einstellungen für die verschiedenen Versionen der Windows-Sicherheitsbaseline für die Verwaltung mobiler Geräte (Mobile Device Management, MDM), die Sie in Microsoft Intune verwenden können.
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
zone_pivot_groups: windows-mdm-versions
ms.reviewer: laarrizz
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 01df8f50da5b0665c1c29949c1ee2c954e47cc9f
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914887"
---
# <a name="windows-mdm-security-baseline-settings-for-intune"></a>Einstellungen für Windows MDM-Sicherheitsbaselines in Intune

Überprüfen Sie die Einstellungen für die MDM-Sicherheitsbaseline, die Microsoft Intune für Geräte unterstützt, auf denen Windows 10 oder höher ausgeführt wird. Die Standardwerte für Einstellungen in dieser Baseline werden für die Konfiguration dieser Geräte empfohlen. Die Standardwerte einer bestimmten Baseline entsprechen möglicherweise nicht den Standardwerten anderer Sicherheitsbaselines oder einer anderen Version der betreffenden Baseline.

- Weitere Informationen zur Verwendung von Sicherheitsbaselines mit Intune und zum Aktualisieren der Baselineversion in Ihren Sicherheitsbaselineprofilen finden Sie unter [Verwenden von Sicherheitsbaselines](security-baselines.md).
- Die neueste Baselineversion ist die **MDM-Sicherheitsbaseline für Mai 2019**.

Verwenden Sie die im Bereich *Versionen* für diese Baseline verfügbare Aktion [Compare baselines](../protect/security-baselines.md#compare-baseline-versions) (Baselines vergleichen), um zu sehen, was sich in dieser Version der Baseline im Vergleich zu früheren Versionen geändert hat.

Wählen Sie die Version der Baseline aus, die Sie prüfen möchten.
<!-- Cookies might be required to enable some browsers to display the zone options -->

::: zone pivot="mdm-may-2019"

**MDM-Sicherheitsbaseline für Mai 2019**:  
> [!NOTE]
> Im Juni 2019 wurde eine allgemein verfügbare Version (keine Vorschauversion) der Vorlage *MDM-Sicherheitsbaseline für Mai 2019* veröffentlicht. Diese Version der Sicherheitsbaseline ersetzt die vorherige Baseline *MDM-Sicherheitsbaseline für Oktober 2018*.  Profile, die vor der Bereitstellung der Baseline für Mai 2019 erstellt wurden, werden nicht auf die Einstellungen und Werte dieser Version aktualisiert.  Obwohl Sie basierend auf der Vorschauversion der Vorlage keine neuen Profile erstellen können, können Sie Profile, die Sie mit dieser Version erstellt haben, bearbeiten und weiterhin verwenden.

Weitere Informationen zu den Änderungen in dieser Version im Vergleich zur vorherigen Version finden Sie im Abschnitt [Eigenschaften der neuen Vorlage](#whats-changed-in-the-new-template).

::: zone-end
::: zone pivot="mdm-preview"

**Vorschau: MDM-Sicherheitsbaseline für Oktober 2018**:  
> [!NOTE]
> Hierbei handelt es sich um die Vorschauversion der MDM-Sicherheitsbaseline, die im Oktober 2018 veröffentlicht wurde. Sie wurde im Juni 2019 durch die allgemein verfügbare (keine Vorschauversion) Vorlage *MDM-Sicherheitsbaseline für Mai 2019* ersetzt. Profile, die vor der Bereitstellung der *MDM-Sicherheitsbaseline für Mai 2019* erstellt wurden, werden nicht auf die Einstellungen und Werte dieser Version aktualisiert. Obwohl Sie basierend auf der Vorschauversion der Vorlage keine neuen Profile erstellen können, können Sie Profile, die Sie mit dieser Version erstellt haben, bearbeiten und weiterhin verwenden.

::: zone-end
::: zone pivot="mdm-may-2019,mdm-preview"

## <a name="above-lock"></a>Sperrbildschirm

Weitere Informationen finden Sie unter [Policy CSP - AboveLock (Richtlinien-Konfigurationsdienstanbieter: AboveLock)](/windows/client-management/mdm/policy-csp-abovelock) in Ihrer Windows-Dokumentation.  

- **Anzeige von Popupbenachrichtigungen blockieren**:  
  Diese Richtlinieneinstellung ermöglicht Ihnen, zu verhindern, dass App-Benachrichtigungen auf dem Sperrbildschirm angezeigt werden. Wenn Sie diese Richtlinieneinstellung aktivieren, werden keine App-Benachrichtigungen auf dem Sperrbildschirm angezeigt. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, können Benutzer wählen, welche Apps Benachrichtigungen auf dem Sperrbildschirm anzeigen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067101)

  **Standardeinstellung:** Ja

::: zone-end
::: zone pivot="mdm-may-2019"

- **Sprachaktivierung von Apps über Sperrbildschirm**:  
  **Standardeinstellung:** Deaktiviert

::: zone-end
::: zone pivot="mdm-may-2019,mdm-preview"

## <a name="app-runtime"></a>App-Laufzeit

Weitere Informationen finden Sie unter [Policy CSP - AppRuntime (Richtlinien-Konfigurationsdienstanbieter: AppRuntime)](/windows/client-management/mdm/policy-csp-appruntime) in Ihrer Windows-Dokumentation.

- **Microsoft-Konten optional für Windows Store-Apps**:  
  Mit dieser Richtlinieneinstellung können Sie steuern, ob für Windows Store-Apps, die eine Anmeldung mit einem Konto erfordern, Microsoft-Konten optional sind. Diese Richtlinie betrifft nur Windows Store-Apps, die dies unterstützen. Wenn Sie diese Richtlinieneinstellung aktivieren, ermöglichen Windows Store-Apps, die normalerweise die Anmeldung mit einem Microsoft-Konto erfordern, Benutzern stattdessen die Anmeldung mit einem Unternehmenskonto. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, müssen Benutzer sich mit einem Microsoft-Konto anmelden.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067104)
  
  **Standardeinstellung:** Aktiviert

## <a name="application-management"></a>Anwendungsverwaltung

Weitere Informationen finden Sie unter [Policy CSP - ApplicationManagement (Richtlinien-Konfigurationsdienstanbieter: ApplicationManagement)](/windows/client-management/mdm/policy-csp-applicationmanagement) in Ihrer Windows-Dokumentation.

::: zone-end
::: zone pivot="mdm-may-2019"

- **Benutzerkontrolle über Installationen blockieren:**  
  Diese Richtlinieneinstellung ermöglicht es Benutzern, Installationsoptionen zu ändern, die normalerweise nur für Systemadministratoren verfügbar sind. Wenn Sie diese Richtlinieneinstellung aktivieren, werden einige der Sicherheitsfeatures des Windows Installers umgangen. Dadurch können Installationen abgeschlossen werden, die andernfalls aufgrund eines Sicherheitsverstoßes unterbrochen werden würden. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, können die Sicherheitsfeatures des Windows Installers Benutzer daran hindern, Installationsoptionen zu ändern, auf die normalerweise nur Systemadministratoren Zugriff haben, z. B. das Verzeichnis, in dem Dateien installiert werden. Wenn der Windows Installer feststellt, dass der Benutzer aufgrund eines bestimmten Installationspakets eine geschützte Option ändern kann, wird die Installation angehalten, und es wird eine Meldung angezeigt. Diese Sicherheitsfeatures funktionieren nur, wenn das Installationsprogramm in einem erhöhten Sicherheitskontext ausgeführt wird, in dem es Zugriff auf Verzeichnisse hat, die für den Benutzer nicht zugänglich sind. Diese Richtlinieneinstellung ist für weniger restriktive Umgebungen bestimmt. Sie kann verwendet werden, um Fehler in einem Installationsprogramm zu umgehen, die verhindern, dass eine Software installiert wird.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067060)

  **Standardeinstellung:** Ja

- **MSI-App-Installationen mit erhöhten Rechten blockieren:**  
  Diese Richtlinieneinstellung weist den Windows Installer an, bei der Installation von Programmen auf dem System erhöhte Rechte anzuwenden.

  - *Wenn Sie diese Richtlinieneinstellung aktivieren*, werden die Berechtigungen auf alle Programme übertragen. In der Regel sind diese Berechtigungen für Programme reserviert, die dem Benutzer (auf dem Desktop angeboten) oder dem Computer (automatisch installiert) zugewiesen oder in der Systemsteuerung unter „Software“ verfügbar sind. Diese Profileinstellung ermöglicht es Benutzern, Programme zu installieren, die Zugriff auf Verzeichnisse benötigen, die der Benutzer aufgrund fehlender Berechtigungen möglicherweise nicht aufrufen oder ändern kann. Dazu gehören auch Verzeichnisse auf stark eingeschränkten Computern.

  - *Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren*, übernimmt das System die Berechtigungen des aktuellen Benutzers, wenn es Programme installiert, die der Systemadministrator weder verteilt noch anbietet. Anmerkung: Diese Richtlinieneinstellung wird sowohl im Ordner für die Computerkonfiguration als auch im Ordner für die Benutzerkonfiguration angezeigt. Damit diese Richtlinieneinstellung wirksam wird, müssen Sie sie in beiden Ordnern aktivieren. Achtung: Geschickte Benutzer können die durch diese Richtlinieneinstellung gewährten Berechtigungen zu ihrem Vorteil ausnutzen und ihre Rechte so ändern, dass sie dauerhaften Zugriff auf eingeschränkte Dateien und Ordner erhalten. Es kann nicht garantiert werden, dass die Benutzerkonfigurationsversion dieser Richtlinieneinstellung sicher ist.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067134)

  **Standardeinstellung:** Ja

::: zone-end
::: zone pivot="mdm-preview,mdm-may-2019"

- **Game DVR (nur Desktop) blockieren**:  
  konfiguriert, ob Aufzeichnen und Übertragen von Spielen zulässig ist.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067056)

  **Standardeinstellung:** Ja

## <a name="auto-play"></a>Automatische Wiedergabe

Weitere Informationen finden Sie unter [Policy CSP - Autoplay (Richtlinien-Konfigurationsdienstanbieter: Autoplay)](/windows/client-management/mdm/policy-csp-autoplay) in Ihrer Windows-Dokumentation.

- **Standardverhalten für automatische Ausführung der automatischen Wiedergabe**:  
  Diese Einstellung betrifft das Standardverhalten für AutoRun-Befehle. AutoRun-Befehle werden in autorun.inf-Dateien gespeichert und können Installationsprogramme oder andere Routinen auslösen. Wenn das Standardverhalten für AutoRun-Befehle *Aktiviert* ist, können es Administratoren auf einem Gerät ändern, das Windows Vista oder eine höhere Version ausführt. Für das Verhalten bestehen die folgenden Einstellungsmöglichkeiten: a) AutoRun-Befehle komplett deaktivieren, oder b) Wiederherstellen des Verhaltens vor der Ausführung von Windows Vista, damit AutoRun-Befehle wieder automatisch ausgeführt werden. Wenn *Deaktiviert* oder *Nicht konfiguriert* eingestellt ist, wird der Benutzer von Geräten, auf denen Windows Vista ausgeführt wird, dazu aufgefordert, zu entscheiden, ob ein AutoRun-Befehl ausgeführt werden soll.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067133)

  **Standardeinstellung:** Nicht ausführen

- **Modus für automatische Wiedergabe**:  
  Diese Richtlinieneinstellung ermöglicht Ihnen, die Funktion für die automatische Wiedergabe zu deaktivieren. Die automatische Wiedergabe startet den Lesevorgang von einem Laufwerk, sobald Sie Medien in das Laufwerk einlegen. Daher wird die Installationsdatei von Programmen sofort gestartet, und Musik auf Audiomedien wird sofort abgespielt. Mit Windows XP SP2 und früher ist die automatische Wiedergabe standardmäßig auf Wechseldatenträgern wie dem Diskettenlaufwerk (nicht aber auf dem CD-ROM-Laufwerk) und Netzlaufwerken deaktiviert. Ab Windows XP SP2 ist die automatische Wiedergabe auch für Wechseldatenträger, einschließlich Ziplaufwerken und einigen USB-Massenspeichergeräten, aktiviert. Wenn Sie diese Richtlinieneinstellung aktivieren, ist die automatische Wiedergabe auf CD-ROM-Laufwerken und Wechselmedien oder auf allen Laufwerken deaktiviert. Diese Richtlinieneinstellung deaktiviert die automatische Wiedergabe auf weiteren Laufwerktypen. Sie können diese Einstellung nicht dazu verwenden, die automatische Wiedergabe auf Laufwerken zu aktivieren, auf denen sie standardmäßig deaktiviert ist. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, ist die automatische Wiedergabe aktiviert. Anmerkung: Diese Richtlinieneinstellung wird sowohl in den Ordnern für die Computerkonfiguration als auch für die Benutzerkonfiguration angezeigt. Wenn die Richtlinieneinstellungen miteinander im Konflikt stehen, hat die Richtlinieneinstellung in der Computerkonfiguration Vorrang gegenüber der Richtlinieneinstellung in der Benutzerkonfiguration.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2066793)

  **Standardeinstellung:** Deaktiviert

- **Automatische Wiedergabe für Nicht-Volume-Geräte blockieren**:  
  Diese Richtlinieneinstellung deaktiviert die automatische Wiedergabe für MTP-Geräte wie Kameras oder Telefone. Wenn Sie diese Richtlinieneinstellung aktivieren, ist die automatische Wiedergabe auf MTP-Geräten wie Kameras oder Telefonen nicht möglich. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, ist die automatische Wiedergabe für Nicht-Volume-Geräte aktiviert.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067106)

  **Standardeinstellung:** Aktiviert

## <a name="bitlocker"></a>BitLocker

Weitere Informationen finden Sie unter [Richtlinie CSP – BitLocker](/windows/client-management/mdm/policy-csp-bitlocker) in Ihrer Windows-Dokumentation.

- **BitLocker-Richtlinie für Wechseldatenträger**:  
  Diese Richtlinieneinstellung wird verwendet, um die Verschlüsselungsmethode und Verschlüsselungsstärke zu steuern. Die Werte dieser Richtlinie bestimmen die Stärke der Verschlüsselung, die BitLocker für die Verschlüsselung verwendet. Unternehmen sollten die Verschlüsselungsstufe für erhöhte Sicherheit steuern (AES-256 ist sicherer als AES-128). Wenn Sie diese Einstellung aktivieren, können Sie einen Verschlüsselungsalgorithmus konfigurieren und für Festplattenlaufwerke, Betriebssystemlaufwerke und Wechseldatenträger die Verschlüsselungsstärke für Schlüssel individuell konfigurieren. Für Festplatten- und Betriebssystemlaufwerke wird die Verwendung des XTS-AES-Algorithmus empfohlen. Für Wechseldatenträger sollten Sie AES-CBC 128-Bit oder AES-CBC 256-Bit verwenden, wenn es in anderen Geräten verwendet wird, auf denen nicht Windows 10, Version 1511 oder höher ausgeführt wird. Das Ändern der Verschlüsselungsmethode hat keine Auswirkungen, wenn das Laufwerk bereits verschlüsselt ist oder die Verschlüsselung gerade ausgeführt wird. In diesen Fällen wird diese Richtlinieneinstellung ignoriert.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067140)

  Konfigurieren Sie bei der Richtlinie für BitLocker-Verschlüsselung von Wechseldatenträgern die folgende Einstellung:

::: zone-end
::: zone pivot="mdm-may-2019"

  - **Block write access to removable data-drives not protected by BitLocker** (Schreibzugriff auf Wechseldatenträger ohne BitLocker-Schutz blockieren):  
    **Standardeinstellung:** Ja

::: zone-end
::: zone pivot="mdm-preview"

  - **Verschlüsselung für Schreibzugriff anfordern**:  
    **Standardeinstellung:** Ja

- **BitLocker-Richtlinie für Wechseldatenträger**:  
  Diese Richtlinieneinstellung wird verwendet, um die Verschlüsselungsmethode und Verschlüsselungsstärke zu steuern. Die Werte dieser Richtlinie bestimmen die Stärke der Verschlüsselung, die BitLocker für die Verschlüsselung verwendet. Unternehmen sollten die Verschlüsselungsstufe für erhöhte Sicherheit steuern (AES-256 ist sicherer als AES-128). Wenn Sie diese Einstellung aktivieren, können Sie einen Verschlüsselungsalgorithmus konfigurieren und für Festplattenlaufwerke, Betriebssystemlaufwerke und Wechseldatenträger die Verschlüsselungsstärke für Schlüssel individuell konfigurieren. Für Festplatten- und Betriebssystemlaufwerke wird die Verwendung des XTS-AES-Algorithmus empfohlen. Für Wechseldatenträger sollten Sie AES-CBC 128-Bit oder AES-CBC 256-Bit verwenden, wenn es in anderen Geräten verwendet wird, auf denen nicht Windows 10, Version 1511 oder höher ausgeführt wird. Das Ändern der Verschlüsselungsmethode hat keine Auswirkungen, wenn das Laufwerk bereits verschlüsselt ist oder die Verschlüsselung gerade ausgeführt wird. In diesen Fällen wird diese Richtlinieneinstellung ignoriert.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067140)

  Konfigurieren Sie bei der Richtlinie für BitLocker-Verschlüsselung von Wechseldatenträgern die folgende Einstellung:

  - **Verschlüsselung für Schreibzugriff anfordern**:  
    **Standardeinstellung:** Ja  

  - **Verschlüsselungsmethode**:  
    **Standardeinstellung:** AES-256-Bit (CBC)  

- **BitLocker-Richtlinie für lokale Festplattenlaufwerke**:  
  Diese Richtlinieneinstellung wird verwendet, um die Verschlüsselungsmethode und Verschlüsselungsstärke zu steuern. Die Werte dieser Richtlinie bestimmen die Stärke der Verschlüsselung, die BitLocker für die Verschlüsselung verwendet. Unternehmen sollten die Verschlüsselungsstufe für erhöhte Sicherheit steuern (AES-256 ist sicherer als AES-128). Wenn Sie diese Einstellung aktivieren, können Sie einen Verschlüsselungsalgorithmus konfigurieren und für Festplattenlaufwerke, Betriebssystemlaufwerke und Wechseldatenträger die Verschlüsselungsstärke für Schlüssel individuell konfigurieren. Für Festplatten- und Betriebssystemlaufwerke wird die Verwendung des XTS-AES-Algorithmus empfohlen. Für Wechseldatenträger sollten Sie AES-CBC 128-Bit oder AES-CBC 256-Bit verwenden, wenn es in anderen Geräten verwendet wird, auf denen nicht Windows 10, Version 1511 oder höher ausgeführt wird. Das Ändern der Verschlüsselungsmethode hat keine Auswirkungen, wenn das Laufwerk bereits verschlüsselt ist oder die Verschlüsselung gerade ausgeführt wird. In diesen Fällen wird diese Richtlinieneinstellung ignoriert.

  Konfigurieren Sie bei der Richtlinie für BitLocker-Verschlüsselung von Festplattenlaufwerken die folgenden Einstellungen:

  - **Verschlüsselungsmethode**:  
    **Standardeinstellung:** AES-256-Bit (XTS)  

- **Richtlinie für BitLocker-Verschlüsselung von Systemlaufwerken**:  
  Diese Richtlinieneinstellung wird verwendet, um die Verschlüsselungsmethode und Verschlüsselungsstärke zu steuern. Die Werte dieser Richtlinie bestimmen die Stärke der Verschlüsselung, die BitLocker für die Verschlüsselung verwendet. Unternehmen sollten die Verschlüsselungsstufe für erhöhte Sicherheit steuern (AES-256 ist sicherer als AES-128). Wenn Sie diese Einstellung aktivieren, können Sie einen Verschlüsselungsalgorithmus konfigurieren und für Festplattenlaufwerke, Betriebssystemlaufwerke und Wechseldatenträger die Verschlüsselungsstärke für Schlüssel individuell konfigurieren. Für Festplatten- und Betriebssystemlaufwerke wird die Verwendung des XTS-AES-Algorithmus empfohlen. Für Wechseldatenträger sollten Sie AES-CBC 128-Bit oder AES-CBC 256-Bit verwenden, wenn es in anderen Geräten verwendet wird, auf denen nicht Windows 10, Version 1511 oder höher ausgeführt wird. Das Ändern der Verschlüsselungsmethode hat keine Auswirkungen, wenn das Laufwerk bereits verschlüsselt ist oder die Verschlüsselung gerade ausgeführt wird. In diesen Fällen wird diese Richtlinieneinstellung ignoriert.

  Konfigurieren Sie bei der Richtlinie für BitLocker-Verschlüsselung von Systemlaufwerken die folgenden Einstellungen:

  - **Verschlüsselungsmethode**:  
    **Standardeinstellung:** AES-256-Bit (XTS)

::: zone-end
::: zone pivot="mdm-preview,mdm-may-2019"

## <a name="browser"></a>Browser

Weitere Informationen finden Sie unter [Policy CSP - Browser (Richtlinien-Konfigurationsdienstanbieter - Browser)](/windows/client-management/mdm/policy-csp-browser) in Ihrer Windows-Dokumentation.

- **SmartScreen für Microsoft Edge anfordern**:  
  Microsoft Edge verwendet Microsoft Defender SmartScreen (aktiviert), um Benutzer standardmäßig vor potenziellen betrügerischen Phishingangriffen und Schadsoftware zu schützen. Standardmäßig ist auch eingestellt, dass Benutzer Microsoft Defender SmartScreen nicht deaktivieren können. Wenn Sie diese Richtlinie aktivieren, wird Microsoft Defender SmartScreen deaktiviert und kann von Benutzern nicht aktiviert werden. Konfigurieren Sie diese Richtlinie nicht so, dass Benutzer auswählen können, ob Microsoft Defender SmartScreen aktiviert oder deaktiviert wird.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067029)

  **Standardeinstellung:** Ja

- **Zugriff auf schädliche Websites blockieren**:  
  Standardmäßig ermöglicht Microsoft Edge es Benutzern, die Warnungen von Microsoft Defender SmartScreen zu potenziell schädlichen Websites zu umgehen (ignorieren) und trotzdem auf die betreffende Website zuzugreifen. Mit dieser Richtlinie können Sie Microsoft Edge jedoch so konfigurieren, dass Benutzer die Warnungen nicht umgehen und nicht auf die Website zugreifen können.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067040)
  
  **Standardeinstellung:** Ja
  
- **Nicht überprüfte Dateidownloads blockieren**:  
  Standardmäßig ermöglicht Microsoft Edge es Benutzern, die Warnungen von Microsoft Defender SmartScreen zu potenziell schädlichen Dateien zu umgehen (ignorieren) und nicht geprüfte Dateien trotzdem herunterzuladen. Durch die Aktivierung dieser Richtlinie wird verhindert, dass Benutzer die Warnungen umgehen und die nicht geprüfte(n) Datei(en) herunterladen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067023)
  
  **Standardeinstellung:** Ja
  
- **Kennwort-Manager blockieren**:  
  Standardmäßig verwendet Microsoft Edge den Kennwort-Manager automatisch, wodurch Benutzern die lokale Verwaltung von Kennwörtern ermöglicht wird. Wenn diese Richtlinie deaktiviert wird, kann Microsoft Edge den Kennwort-Manager nicht nutzen. Konfigurieren Sie diese Richtlinie nicht, wenn Sie Benutzern erlauben möchten, selbst zu entscheiden, ob sie den Kennwort-Manager zum lokalen Speichern und Verwalten von Kennwörtern verwenden möchten.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067128)
  
  **Standardeinstellung:** Ja
  
- **Außerkraftsetzen von Zertifikatfehlern durch Benutzer verhindern:**  
  Diese Richtlinieneinstellung verhindert, dass der Benutzer SSL/TLS-Zertifikatfehler (Secure Sockets Layer/Transport Layer Security), die die Navigation in Internet Explorer unterbrechen (z.B. „Abgelaufen“, „Gesperrt“ oder „Name stimmt nicht überein“ ) ignoriert. Wenn Sie diese Richtlinieneinstellung aktivieren, können Benutzer das Browsen nicht mehr fortsetzen. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, kann der Benutzer entscheiden, ob Zertifikatfehler ignoriert werden sollen und das Browsen fortsetzen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067126)
  
  **Standardeinstellung:** Ja

## <a name="connectivity"></a>Verbindung

Weitere Informationen finden Sie unter [Policy CSP – Connectivity (Richtlinien-Konfigurationsdienstanbieter: Konnektivität)](/windows/client-management/mdm/policy-csp-connectivity) in der Windows-Dokumentation.

- **Internetdownload für die Assistenten zur Webveröffentlichung und Onlinebestellung von Abzügen blockieren**:  
  Diese Richtlinieneinstellung legt fest, ob Windows eine Liste von Anbietern für den Webpublishing-Assistenten und den Assistenten für Onlinebestellung herunterladen soll. Diese Assistenten ermöglichen Benutzern, aus einer Liste Firmen auszuwählen, die Dienste wie Onlinespeicherung und Fotodruck anbieten. Standardmäßig werden zusätzlich zu den in der Registrierung angegebenen Anbietern auch solche angezeigt, die von einer Windows-Website heruntergeladen wurden. Wenn Sie diese Richtlinieneinstellung aktivieren, werden keine Anbieter heruntergeladen, sondern nur die Dienstanbieter angezeigt, die in der lokalen Registrierung zwischengespeichert sind. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, wird eine Liste von Anbietern heruntergeladen, wenn der Benutzer den Webpublishing-Assistenten und den Assistenten für Onlinebestellung verwendet. Weitere Informationen über den Webpublishing-Assistenten und den Assistenten für Onlinebestellung finden Sie in der Dokumentation, einschließlich Details über das Angeben von Dienstanbietern in der Registrierung.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067136)
  
  **Standardeinstellung:** Aktiviert

::: zone-end
::: zone pivot="mdm-may-2019"

- **Sicheren Zugriff auf UNC-Pfade konfigurieren:**  
  Diese Richtlinieneinstellung konfiguriert den sicheren Zugriff auf UNC-Pfade. Wenn Sie diese Einstellung aktivieren, lässt Windows nur nach Erfüllung zusätzlicher Sicherheitsanforderungen den Zugriff auf die angegebenen UNC-Pfade zu.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067243)

  **Standardeinstellung:** Hiermit wird Windows so konfiguriert, dass nach Erfüllung zusätzlicher Sicherheitsanforderungen nur der Zugriff auf die angegebenen UNC-Pfade zugelassen wird.

  Wenn Sie *Windows so konfigurieren, dass nur nach Erfüllung zusätzlicher Sicherheitsanforderungen der Zugriff auf die angegebenen UNC-Pfade zugelassen wird*, können Sie die *Liste der festgeschriebenen UNC-Pfade* konfigurieren.

  - **Liste der festgeschriebenen UNC-Pfade:**  
    Klicken Sie auf **Hinzufügen**, um zusätzliche Sicherheitsflags und Serverpfade anzugeben.

::: zone-end
::: zone pivot="mdm-preview,mdm-may-2019"

- **Download von Druckertreibern über HTTP blockieren**:  
  Diese Richtlinieneinstellung gibt an, ob dieser Client Druckertreiberpakete über HTTP herunterladen darf. Nicht im Lieferumfang enthaltene Treiber müssen über HTTP heruntergeladen werden, um das HTTP-Drucken einzurichten. Anmerkung: Diese Richtlinieneinstellung hindert den Client nicht daran, auf Druckern im Intranet oder im Internet über HTTP zu drucken. Sie verhindert nur das Herunterladen von Treibern, die noch nicht lokal installiert sind. Wenn Sie diese Richtlinieneinstellung aktivieren, können keine Druckertreiber über HTTP heruntergeladen werden. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, können die Benutzer Druckertreiber über HTTP herunterladen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067141)
  
  **Standardeinstellung:** Aktiviert

## <a name="credentials-delegation"></a>Delegierung von Anmeldeinformationen

Weitere Informationen finden Sie unter [Policy CSP – CredentialsDelegation (Richtlinien-Konfigurationsdienstanbieter: CredentialsDelegation)](/windows/client-management/mdm/policy-csp-credentialsdelegation) in der Windows-Dokumentation.

- **Remotehost ermöglicht die Delegierung nicht exportierbarer Anmeldeinformationen**:  
  Remotehost ermöglicht die Delegierung nicht exportierbarer Anmeldeinformationen. Bei Verwendung der Delegierung von Anmeldeinformationen stellen Geräte eine exportierbare Version der Anmeldeinformationen für den Remotehost bereit. Dadurch laufen Benutzer Gefahr, dass ihre Anmeldeinformationen von Angreifern auf dem Remotehost gestohlen werden. Wenn Sie die Richtlinieneinstellung aktivieren, unterstützt der Host den eingeschränkten Verwaltungsmodus oder Remote Credential Guard-Modus. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, werden der eingeschränkte Verwaltungsmodus und der Remote Credential Guard-Modus nicht unterstützt, und Benutzer müssen ihre Anmeldeinformationen immer an den Host übergeben.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067103)
  
  **Standardeinstellung:** Aktiviert

## <a name="credentials-ui"></a>Benutzeroberfläche für Anmeldeinformationen

Weitere Informationen finden Sie unter [Policy CSP – Connectivity (Richtlinien-Konfigurationsdienstanbieter: CredentialsUI)](/windows/client-management/mdm/policy-csp-credentialsui) in der Windows-Dokumentation.

- **Administratoren aufzählen**:  
  Diese Richtlinieneinstellung steuert, ob Administratorkonten angezeigt werden, wenn ein Benutzer versucht, eine Anwendung mit erhöhten Rechten auszuführen. Standardmäßig werden Administratorkonten beim Versuch eines Benutzers, eine Anwendung mit erhöhten Rechten auszuführen, nicht angezeigt. Wenn Sie diese Richtlinieneinstellung aktivieren, werden alle lokalen Administratorkonten auf dem Computers angezeigt, damit der Benutzer eines auswählen und das richtige Kennwort eingeben kann. Wenn Sie diese Richtlinieneinstellung deaktivieren, müssen Benutzer jedes Mal einen Benutzernamen und ein Kennwort eingeben, um eine Anwendung mit erhöhten Rechten auszuführen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067021)

  **Standardeinstellung:** Deaktiviert

## <a name="data-protection"></a>Schutz von Daten

Weitere Informationen finden Sie unter [Policy CSP – Defender (Richtlinien-Konfigurationsdienstanbieter: DataProtection)](/windows/client-management/mdm/policy-csp-dataprotection) in der Windows-Dokumentation.

- **Direkten Speicherzugriff blockieren**:  
  Mit dieser Richtlinieneinstellung können Sie den direkten Speicherzugriff (Direct Memory Access, DMA) für alle Hot-Plug-PCI-Downstream-Anschlüsse blockieren, bis sich ein Benutzer bei Windows anmeldet. Sobald sich ein Benutzer anmeldet, werden die mit den Hot-Plug-PCI-Anschlüssen verbundenen PCI-Geräte von Windows aufgezählt. Jedes Mal, wenn der Benutzer den Computer sperrt, wird DMA an Hot-Plug-PCI-Anschlüssen ohne untergeordnete Geräte blockiert, bis sich der Benutzer erneut anmeldet. Geräte, die vor dem Entsperren des Computers bereits aufgezählt wurden, sind weiterhin funktionsfähig, bis sie entfernt werden oder das System neu gestartet bzw. in den Ruhezustand versetzt wird. Die Richtlinieneinstellung wird nur erzwungen, wenn BitLocker oder die Geräteverschlüsselung aktiviert ist.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067031)

  **Standardeinstellung:** Ja

## <a name="device-guard"></a>Device Guard

Weitere Informationen finden Sie unter [Policy CSP – DeviceGuard (Richtlinien-Konfigurationsdienstanbieter: DeviceGuard)](/windows/client-management/mdm/policy-csp-deviceguard) in der Windows-Dokumentation.

- **Turn on credential guard** (Credential Guard aktivieren):  
  Mit dieser Einstellung können Benutzer Credential Guard mit virtualisierungsbasierter Sicherheit aktivieren, um den Schutz von Anmeldeinformationen beim nächsten Neustart zu unterstützen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067044)

  **Standardeinstellung:** Mit UEFI-Sperre aktivieren

::: zone-end
::: zone pivot="mdm-may-2019"

- **Virtualisierungsbasierte Sicherheit**:  
  **Standardeinstellung:** VBS mit sicherem Start aktivieren

::: zone-end
::: zone pivot="mdm-preview,mdm-may-2019"

- **Virtualisierungsbasierte Sicherheit aktivieren**:  
  Aktiviert die virtualisierungsbasierte Sicherheit (VBS) beim nächsten Neustart. Virtualisierungsbasierte Sicherheit verwendet Windows Hypervisor, um die Sicherheitsdienste zu unterstützen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067066)
  
  **Standardeinstellung:** Ja

- **Systemüberwachung starten**:  
  **Standardeinstellung:** Aktiviert

## <a name="device-installation"></a>Geräteinstallation

Weitere Informationen finden Sie unter [Policy CSP – DeviceInstallation (Richtlinien-Konfigurationsdienstanbieter: DeviceInstallation)](/windows/client-management/mdm/policy-csp-deviceinstallation) in der Windows-Dokumentation.

- **Hardwaregeräteinstallation nach Gerätebezeichner**:  
  Mit dieser Richtlinieneinstellung können Sie eine Liste von Plug & Play-Hardware-IDs und kompatiblen IDs für Geräte angeben, deren Installation unter Windows verhindert wird. Diese Richtlinieneinstellung hat Vorrang gegenüber jeder anderen Richtlinieneinstellung, die die Installation eines Geräts ermöglicht. Wenn Sie diese Richtlinieneinstellung aktivieren, kann Windows ein Gerät nicht installieren, wenn die zugehörige Hardware-ID oder kompatible ID in der von Ihnen erstellten Liste enthalten ist. Wenn Sie diese Richtlinieneinstellung auf einem Remotedesktopserver aktivieren, wirkt sich dies auf die Umleitung der angegebenen Geräte von einem Remotedesktopclient an den Remotedesktopserver aus. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, können Geräte installiert und aktualisiert werden, sofern andere Richtlinieneinstellungen dies zulassen.  
  [Erfahren Sie mehr](/windows/client-management/mdm/policy-csp-deviceinstallation#deviceinstallation-preventinstallationofmatchingdeviceids)

  **Standardeinstellung:** Block hardware device installation (Hardwaregeräteinstallation blockieren)

  Wenn *Block hardware device installation* ausgewählt wurde, stehen die folgenden Einstellungen zur Verfügung.

  - **Übereinstimmende Hardwaregeräte entfernen**:  
    Diese Einstellung ist nur verfügbar, wenn die Option *Hardware device installation by device identifiers* (Installation von Hardwaregeräten anhand der Geräte-ID) auf *Block hardware device installation* (Hardwaregeräteinstallation blockieren) festgelegt ist.

    **Standardeinstellung:** Ja

  - **Hardwaregerätebezeichner, die blockiert werden**:  
    Diese Einstellung ist nur verfügbar, wenn die Option *Hardware device installation by device identifiers* (Installation von Hardwaregeräten anhand der Geräte-ID) auf *Block hardware device installation* (Hardwaregeräteinstallation blockieren) festgelegt ist.

    **Standardeinstellung:** Ja

- **Hardwaregeräteinstallation nach Setupklassen**:  
  Mit dieser Richtlinieneinstellung können Sie eine Liste von GUIDs für Gerätesetupklassen angeben, die Gerätetreiber beschreiben, die unter Windows nicht installierbar sind. Diese Richtlinieneinstellung hat Vorrang gegenüber jeder anderen Richtlinieneinstellung, die die Installation eines Geräts ermöglicht. Wenn Sie diese Richtlinieneinstellung aktivieren, kann Windows Gerätetreiber nicht installieren oder aktualisieren, deren GUIDs für Gerätesetupklassen in der von Ihnen erstellten Liste enthalten sind. Wenn Sie diese Richtlinieneinstellung auf einem Remotedesktopserver aktivieren, wirkt sich dies auf die Umleitung der angegebenen Geräte von einem Remotedesktopclient an den Remotedesktopserver aus. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, können Geräte unter Windows installiert und aktualisiert werden, sofern andere Richtlinieneinstellungen dies zulassen.  
  [Erfahren Sie mehr](/windows/client-management/mdm/policy-csp-deviceinstallation#deviceinstallation-preventinstallationofmatchingdevicesetupclasses)

  **Standardeinstellung:** Block hardware device installation (Hardwaregeräteinstallation blockieren)

  Wenn *Block hardware device installation* ausgewählt wurde, stehen die folgenden Einstellungen zur Verfügung.

  - **Übereinstimmende Hardwaregeräte entfernen**:  
    Diese Einstellung ist nur verfügbar, wenn *Hardware device installation by setup classes (Hardwaregeräteinstallation nach Setup-Klasse)* auf *Block hardware device installation (Hardwaregeräteinstallation blockieren)* eingestellt ist.

    **Standardeinstellung:** *Keine Standardkonfiguration*

  - **Hardwaregerätebezeichner, die blockiert werden**:  
    Diese Einstellung ist nur verfügbar, wenn *Hardware device installation by setup classes (Hardwaregeräteinstallation nach Setup-Klasse)* auf *Block hardware device installation (Hardwaregeräteinstallation blockieren)* eingestellt ist.

    **Standardeinstellung:** *Keine Standardkonfiguration*

## <a name="device-lock"></a>Gerätesperre

Weitere Informationen finden Sie unter [Policy CSP - DeviceLock (Richtlinien-CSP: DeviceLock)](/windows/client-management/mdm/policy-csp-devicelock) in Ihrer Windows-Dokumentation.

- **Verwendung der Kamera verhindern**:  
  Deaktiviert das Ein-/Ausschalten der Kamera auf dem Sperrbildschirm in den PC-Einstellungen und verhindert, dass eine Kamera auf dem Sperrbildschirm aufgerufen wird. Standardmäßig können Benutzer das Aufrufen einer verfügbaren Kamera auf dem Sperrbildschirm aktivieren. Wenn Sie diese Einstellung aktivieren, können Benutzer den Kamerazugriff auf den Sperrbildschirm in den PC-Einstellungen nicht aktivieren oder deaktivieren, und die Kamera kann nicht mehr auf dem Sperrbildschirm aufgerufen werden.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067052)

  **Standardeinstellung:** Aktiviert

- **Kennwort anfordern**:  
  Gibt an, ob eine Gerätesperre aktiviert ist.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067049)  

  **Standardeinstellung:** Ja
  
  Wenn *Kennwort anfordern* auf *Ja* festgelegt wurde, stehen die folgenden Einstellungen zur Verfügung.

  - **Mindestanzahl von Zeichensätzen für Kennwörter**:  
    Anzahl der komplexen Elementtypen (Groß- und Kleinbuchstaben, Zahlen und Interpunktionszeichen), die für eine sichere PIN oder ein sicheres Kennwort erforderlich sind. PIN erzwingt das folgende Verhalten für Desktop- und mobile Geräte: 1: nur Ziffern 2: Ziffern und Kleinbuchstaben sind erforderlich 3: Ziffern, Klein- und Großbuchstaben sind erforderlich. Nicht unterstützt in Microsoft- und Domänenkonten für Desktopgeräte. 4: Ziffern, Kleinbuchstaben, Großbuchstaben und Sonderzeichen sind erforderlich. Nicht unterstützt für Desktop-Geräte.  
    [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067055)

    **Standardeinstellung:** 3

  - **Anzahl von fehlgeschlagenen Anmeldungen, bevor das Gerät zurückgesetzt wird:**  
    Die Anzahl von zulässigen Authentifizierungsfehlern bevor das Gerät zurückgesetzt wird. Der Wert 0 deaktiviert die Rücksetzfunktion eines Geräts.  
    [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067030)

    **Standardeinstellung:** 10  

  - **Kennwortablauf (Tage):**  
    Die Richtlinieneinstellung für das maximale Kennwortalter bestimmt die Zeitspanne (in Tagen), in der ein Kennwort verwendet werden kann, bevor das System den Benutzer zum Ändern des Kennworts auffordert. Sie können einstellen, dass Kennwörter nach einer bestimmten Anzahl von Tagen (zwischen 1 und 999) ablaufen, oder dass Kennwörter nie ablaufen, indem Sie die Anzahl der Tage auf 0 einstellen. Wenn das maximale Kennwortalter zwischen 1 und 999 Tagen liegt, muss das minimale Kennwortalter darunter liegen. Wenn das maximale Kennwortalter auf 0 eingestellt ist, kann das minimale Kennwortalter ein Wert zwischen 0 und 998 Tagen sein.  
    [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067028)

    **Standardeinstellung:** 60

  - **Erforderliches Kennwort:**  
    Bestimmt den Typ der erforderlichen PIN oder des erforderlichen Kennworts.  
    [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067027)

    **Standardeinstellung:** Alphanumerisch

  - **Minimale Kennwortlänge:**  
    Die Richtlinieneinstellung für die minimale Kennwortlänge bestimmt die Mindestanzahl von Zeichen, die ein Kennwort für ein Benutzerkonto besitzen muss. Sie können einen Wert zwischen 1 und 14 Zeichen einstellen, oder Sie können einstellen, dass kein Kennwort erforderlich ist, indem Sie die Zeichenanzahl auf 0 einstellen.  
    [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067024)

    **Standardeinstellung:** 8

  - **Einfache Kennwörter blockieren**:  
    Gibt an, ob PINs oder Kennwörter wie „1111“ oder „1234“ zulässig sind. Für Desktop-Geräte wird auch die Verwendung von Bildcodes gesteuert.  
    [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067127)

    **Standardeinstellung:** Ja  
    *Eine Einstellung auf „Ja“ verhindert die Verwendung einfacher Kennwörter.*

  - **Wiederverwendung vorheriger Kennwörter verhindern:**  
    Hiermit wird angegeben, wie viele Kennwörter, die nicht mehr verwendet werden können, im Verlauf gespeichert werden. Der Wert schließt das aktuelle Kennwert des Benutzers mit ein. So kann der Benutzer beispielsweise bei der Einstellung *1* sein aktuelles Kennwort nicht ändern, wenn er ein neues Kennwort auswählt. Die Einstellung *5* bedeutet, dass ein Benutzer sein neues Kennwort nicht auf sein aktuelles Kennwort oder eines seiner vorherigen vier Kennwörter festlegen kann.  
    [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2066795)

    **Standardeinstellung:** 24

- **Diashow verhindern**:  
  Deaktiviert die Diashow-Einstellungen für den Sperrbildschirm in den PC-Einstellungen und verhindert das Abspielen einer Diashow auf dem Sperrbildschirm. Standardmäßig können Benutzer eine Diashow aktivieren, die nach dem Sperren des Computers abgespielt wird. Wenn Sie diese Einstellung aktivieren, können Benutzer Diashow-Einstellungen in den PC-Einstellungen nicht ändern, und es kann keine Diashow gestartet werden.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067105)

  **Standardeinstellung:** Aktiviert  

  *Die Einstellung „Deaktiviert“ verhindert das Abspielen von Diashows.*

- **Minimales Kennwortalter in Tagen**:  
  Die Richtlinieneinstellung für das minimale Kennwortalter bestimmt die Zeitspanne (in Tagen), in der ein Kennwort verwendet werden muss, bevor der Benutzer es ändern kann. Sie können einen Wert zwischen 1 und 998 Tagen festlegen, oder Sie können Kennwortänderungen sofort zulassen, indem Sie die Anzahl der Tage auf 0 setzen. Das minimale Kennwortalter muss unter dem maximalen Kennwortalter liegen, es sei denn, das maximale Kennwortalter ist auf 0 eingestellt, was bedeutet, dass ein Kennwörter nie ablaufen. Wenn das maximale Kennwortalter auf 0 eingestellt ist, kann für das minimale Kennwortalter ein Wert zwischen 0 und 998 eingestellt werden.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067022)

  **Standardeinstellung:** 1

::: zone-end
::: zone pivot="mdm-may-2019"

## <a name="dma-guard"></a>DMA Guard

Weitere Informationen finden Sie unter [Policy CSP – DmaGuard (Richtlinien-Konfigurationsdienstanbieter: DmaGuard)](/windows/client-management/mdm/policy-csp-dmaguard) in der Windows-Dokumentation.

- **Aufzählung externer Geräte, die mit Kernel-DMA-Schutz nicht kompatibel sind**:  
  Diese Richtlinie soll zusätzliche Sicherheit für externe DMA-fähige Geräte bieten. Sie ermöglicht eine bessere Kontrolle über die Aufzählung von externen DMA-fähigen Geräten, die mit DMA Remapping/Gerätespeicherisolation und Sandboxing nicht kompatibel sind. Diese Richtlinie gilt nur, wenn der Kernel-DMA-Schutz unterstützt wird und durch die Systemfirmware aktiviert wurde. Der Kernel-DMA-Schutz ist ein Plattformfeature, das nicht durch Richtlinien oder den Endbenutzer gesteuert werden kann. Er muss zum Zeitpunkt der Herstellung vom System unterstützt werden. Sie können auf der Zusammenfassungsseite der Datei „MSINFO32.exe“ über das Feld „Kernel DMA Protection“ (Kernel-DMA-Schutz) überprüfen, ob das System den Kernel-DMA-Schutz unterstützt.  
  [Erfahren Sie mehr](/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy)

  **Standardeinstellung:** Alle blockieren

::: zone-end
::: zone pivot="mdm-preview,mdm-may-2019"

## <a name="event-log-service"></a>Ereignisprotokolldienst

Weitere Informationen finden Sie unter [Policy CSP - EventLogService (Richtlinien-Konfigurationsdienstanbieter: EventLogService)](/windows/client-management/mdm/policy-csp-eventlogservice) in Ihrer Windows-Dokumentation.

- **Sicherheitsprotokoll: maximale Dateigröße in KB**:  
  Diese Richtlinieneinstellung gibt die maximale Größe der Protokolldatei in Kilobyte an. Wenn Sie diese Richtlinieneinstellung aktivieren, können Sie die maximale Protokolldateigröße so konfigurieren, dass sie zwischen 1 Megabyte (1.024 Kilobyte) und 2 Terabyte (2.147.483.647 Kilobyte) in Kilobyte-Schritten liegt. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, wird die maximale Größe der Protokolldatei auf den lokal konfigurierten Wert eingestellt. Dieser Wert kann durch den lokalen Administrator über das Dialogfeld „Protokolleigenschaften“ geändert werden und wird standardmäßig auf 20 Megabyte eingestellt.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067042)

   **Standardeinstellung:** 196608

- **Systemprotokoll: maximale Dateigröße in KB**:  
  Diese Richtlinieneinstellung gibt die maximale Größe der Protokolldatei in Kilobyte an. Wenn Sie diese Richtlinieneinstellung aktivieren, können Sie die maximale Protokolldateigröße so konfigurieren, dass sie zwischen 1 Megabyte (1.024 Kilobyte) und 2 Terabyte (2.147.483.647 Kilobyte) in Kilobyte-Schritten liegt. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, wird die maximale Größe der Protokolldatei auf den lokal konfigurierten Wert eingestellt. Dieser Wert kann durch den lokalen Administrator über das Dialogfeld „Protokolleigenschaften“ geändert werden und wird standardmäßig auf 20 Megabyte eingestellt.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2066798)

  **Standardeinstellung:** 32768

- **Anwendungsprotokoll: maximale Dateigröße in KB**:  
  Diese Richtlinieneinstellung gibt die maximale Größe der Protokolldatei in Kilobyte an. Wenn Sie diese Richtlinieneinstellung aktivieren, können Sie die maximale Protokolldateigröße so konfigurieren, dass sie zwischen 1 Megabyte (1.024 Kilobyte) und 2 Terabyte (2.147.483.647 Kilobyte) in Kilobyte-Schritten liegt. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, wird die maximale Größe der Protokolldatei auf den lokal konfigurierten Wert eingestellt. Dieser Wert kann durch den lokalen Administrator über das Dialogfeld „Protokolleigenschaften“ geändert werden und wird standardmäßig auf 20 Megabyte eingestellt.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067125)

  **Standardeinstellung:** 32768

## <a name="experience"></a>Erfahrung

Weitere Informationen finden Sie unter [Policy CSP - Experience (Richtlinien-Konfigurationsdienstanbieter: Experience)](/windows/client-management/mdm/policy-csp-experience) in Ihrer Windows-Dokumentation.

- **Windows-Blickpunkt blockieren**:  
  Hiermit wird IT-Administratoren gestattet, alle Windows-Blickpunkt-Features zu deaktivieren (blockieren). Dies schließt Windows-Blickpunkt auf dem Sperrbildschirm, Windows-Tipps, Microsoft-Features für Endbenutzer und weitere zugehörige Features ein.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067037)

  **Standardeinstellung:** Ja

  Ist *Windows-Blickpunkt blockieren* auf *Nicht konfiguriert* festgelegt, wird Windows-Blickpunkt nicht auf den Geräten blockiert, und Sie können die folgenden Einstellungen konfigurieren, um ausgewählte Elemente für Windows-Blickpunkt zu blockieren:

  - **Drittanbietervorschläge in Windows-Blickpunkt blockieren**:  
    Gibt an, ob App- und Inhaltsvorschläge durch Herausgeber von Drittanbieter-Software in Features von Windows-Blickpunkt (z.B. Windows-Blickpunkt auf dem Sperrbildschirm, vorgeschlagene Apps im Startmenü oder Windows-Tipps) zulässig sind. Benutzer sehen möglicherweise trotzdem Vorschläge für Microsoft-Features, -Apps und -Dienste.  
    [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067045)

    **Standardeinstellung:** Nicht konfiguriert

  - **Bestimmte Funktionen für Endbenutzer blockieren**:  
    Ermöglicht IT-Administratoren das Aktivieren von Funktionen, die normalerweise nur für Endbenutzer bestimmt sind, beispielsweise Startvorschläge, Mitgliedschaftsbenachrichtigungen, App-Installation nach Anzeige der Windows-Willkommensseite und Kachelumleitungen.  
    [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067054)

    **Standardeinstellung:** Nicht konfiguriert

## <a name="exploit-guard"></a>Exploit Guard

Weitere Informationen finden Sie unter [Policy CSP - ExploitGuard (Richtlinien-Konfigurationsdienstanbieter: ExploitGuard)](/windows/client-management/mdm/policy-csp-exploitguard) in Ihrer Windows-Dokumentation.

- **XML hochladen:**  
  Ermöglicht dem IT-Administrator, eine Konfiguration vorzunehmen, die für alle Geräte in der Organisation die gewünschten Optionen zur Risikominderung für System und Anwendungen abbildet. Die Konfiguration wird in einer XML-Datei vorgenommen. Durch den Exploit-Schutz können Geräte vor Schadsoftware geschützt werden, die Exploits für die Verbreitung und den Befall von Systemen verwendet. Sie können die App „Windows-Sicherheit“ oder PowerShell verwenden, um Lösungen zur Entschärfung (Konfigurationen) zu erstellen. Diese Konfiguration können Sie anschließend als XML-Datei exportieren und für die Computer in Ihrem Netzwerk freigeben, sodass diese über dieselben Einstellungen zur Entschärfung verfügen. Sie können außerdem eine vorhandene XML-Konfigurationsdatei aus EMET in eine XML-Konfigurationsdatei für den Exploit-Schutz konvertieren und importieren.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067035)

  **Standardeinstellung:** *Sample xml is provided* (XML-Beispieldatei wird bereitgestellt)

## <a name="file-explorer"></a>Datei-Explorer

Weitere Informationen finden Sie unter [Policy CSP - FileExplorer (Richtlinien-CSP: FileExplorer)](/windows/client-management/mdm/policy-csp-fileexplorer) in der Windows-Dokumentation.  

- **Verhindern der Datenausführung blockieren**:  
  Wenn Sie den Schutz vor der Ausführung von Daten deaktivieren, können bestimmte veraltete Plug-In-Anwendungen erfolgreich ausgeführt werden, ohne dass der Explorer geschlossen wird.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067043)  

  **Standardeinstellung:** Deaktiviert

- **Heapabbruch bei Beschädigung blockieren**:  
  Wenn Sie das Beenden von Heaps bei Beschädigung deaktivieren, können bestimmte veraltete Plug-In-Anwendungen erfolgreich ausgeführt werden, ohne dass der Explorer sofort geschlossen wird. Der Explorer wird jedoch möglicherweise zu einem späteren Zeitpunkt unerwartet beendet.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067107)

  **Standardeinstellung:** Deaktiviert

## <a name="firewall"></a>Firewall

Weitere Informationen finden Sie unter [2.2.2 FW_PROFILE_TYPE]( /openspecs/windows_protocols/ms-fasp/7704e238-174d-4a5e-b809-5f3787dd8acc) in der Dokumentation zu Windows-Protokollen.

- **Firewallprofil: Domäne:**  
  Gibt die Profile an, zu denen die Regel gehört: „Domäne“, „Privat“ oder „Öffentlich“. Dieser Wert stellt das Profil für Netzwerke dar, die mit Domänen verbunden sind.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2066796)

  - **Eingehende Verbindungen blockiert**:  
    **Standardeinstellung:** Ja

  - **Ausgehende Verbindungen erforderlich**:  
    **Standardeinstellung:** Ja

  - **Eingehende Benachrichtigungen blockiert**:  
    **Standardeinstellung:** Ja

  - **Firewall aktiviert**:  
    **Standardeinstellung:** Zulässig

- **Firewallprofil: öffentlich:**  
  Gibt die Profile an, zu denen die Regel gehört: „Domäne“, „Privat“ oder „Öffentlich“. Dieser Wert stellt das Profil für öffentliche Netzwerke dar. Diese Netzwerke werden von den Administratoren des Serverhosts als „öffentlich“ klassifiziert. Die Klassifizierung erfolgt, wenn sich der Host zum ersten Mal mit dem Netzwerk verbindet. In der Regel sind diese Netzwerke an Flughäfen, in Cafés und an anderen öffentlichen Orten zu finden, an denen die Peers im Netzwerk oder der Netzwerkadministrator nicht vertrauenswürdig sind.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067143)

  - **Eingehende Verbindungen blockiert**:  
    **Standardeinstellung:** Ja

  - **Ausgehende Verbindungen erforderlich**:  
    **Standardeinstellung:** Ja

  - **Eingehende Benachrichtigungen blockiert**:  
    **Standardeinstellung:** Ja

  - **Firewall aktiviert**:  
    **Standardeinstellung:** Zulässig

  - **Verbindungssicherheitsregeln aus Gruppenrichtlinie nicht zusammengeführt**:  
    **Standardeinstellung:** Ja

  - **Richtlinienregeln aus Gruppenrichtlinie nicht zusammengeführt**:  
    **Standardeinstellung:** Ja

- **Firewallprofil: privat:**  
  Gibt die Profile an, zu denen die Regel gehört: „Domäne“, „Privat“ oder „Öffentlich“. Dieser Wert stellt das Profil für private Netzwerke dar.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067041)

  - **Eingehende Verbindungen blockiert**:  
    **Standardeinstellung:** Ja

  - **Ausgehende Verbindungen erforderlich**:  
    **Standardeinstellung:** Ja

  - **Eingehende Benachrichtigungen blockiert**:  
    **Standardeinstellung:** Ja

  - **Firewall aktiviert**:  
    **Standardeinstellung:** Zulässig

## <a name="internet-explorer"></a>Internet Explorer

Weitere Informationen finden Sie unter [Policy CSP - Internet Explorer (Richtlinien-CSP: Internet Explorer)](/windows/client-management/mdm/policy-csp-internetexplorer) in der Windows-Dokumentation.

- **Internet Explorer: Eingeschränkte Zone: Aktualisierungen der Statusleiste per Skript**:  
  Über diese Richtlinieneinstellung können Sie festlegen, ob die Statusleiste in der Zone durch ein Skript aktualisiert werden darf.

  - *Wenn Sie diese Richtlinieneinstellung aktivieren*, kann die Statusleiste über Skripts aktualisiert werden.
  - *Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren*, kann die Statusleiste nicht über Skripts aktualisiert werden.

  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067074)

  **Standardeinstellung:** Deaktiviert

::: zone-end
::: zone pivot="mdm-may-2019"

- **Internet Explorer: Internetzone: Ziehen und Ablegen oder Kopieren und Einfügen von Dateien**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob Benutzer Dateien aus einer Quelle innerhalb der Zone per Drag & Drop verschieben oder kopieren und einfügen können. Wenn Sie diese Richtlinieneinstellung aktivieren, können Benutzer Dateien automatisch aus dieser Zone per Drag & Drop verschieben oder kopieren und einfügen. Wenn Sie die Option „Bestätigen“ im Dropdownfeld auswählen, werden Benutzer dazu aufgefordert, auszuwählen, ob sie Dateien aus dieser Zone ziehen oder kopieren möchten. Wenn Sie diese Richtlinieneinstellung deaktivieren, können Benutzer Dateien aus dieser Zone nicht per Drag & Drop verschieben oder kopieren und einfügen. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, können Benutzer Dateien automatisch aus dieser Zone per Drag & Drop verschieben oder kopieren und einfügen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067076)

  **Standardeinstellung:** Deaktivieren

- **Internet Explorer: Eingeschränkte Zone: Komponenten, die .NET Framework erfordern**:  
  Bestimmen Sie mit dieser Richtlinieneinstellung, ob .NET Framework-Komponenten, die nicht mit Authenticode signiert wurden, von Internet Explorer ausgeführt werden können. Dazu zählen verwaltete Steuerelemente, auf die über Objekttags verwiesen wird, sowie verwaltete ausführbare Dateien, auf die über einen Link verwiesen wird. Wenn Sie diese Richtlinieneinstellung aktivieren, führt Internet Explorer nicht signierte verwaltete Komponenten aus. Wenn Sie im Dropdownfeld „Bestätigen“ auswählen, fordert Internet Explorer den Benutzer dazu auf, zu entscheiden, ob nicht signierte verwaltete Komponenten ausgeführt werden sollen. Wenn Sie diese Richtlinieneinstellung deaktivieren, führt Internet Explorer nicht signierte verwaltete Komponenten nicht aus. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, führt Internet Explorer nicht signierte verwaltete Komponenten nicht aus.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067077)

  **Standardeinstellung:** Deaktivieren

- **Internet Explorer: Zone des lokalen Computers: Keine Antischadsoftware für ActiveX-Steuerelemente ausführen**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob von Internet Explorer Antischadsoftwareprogramme für ActiveX-Steuerelemente ausgeführt werden, um zu überprüfen, ob sie sicher auf Seiten geladen werden können. Wenn Sie diese Richtlinieneinstellung aktivieren, prüft Internet Explorer nicht anhand des Antischadsoftwareprogramms, ob das Erstellen einer Instanz des ActiveX-Steuerelements sicher ist. Wenn Sie diese Richtlinieneinstellung deaktivieren, prüft Internet Explorer immer anhand des Antischadsoftwareprogramms, ob das Erstellen einer Instanz des ActiveX-Steuerelements sicher ist. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, prüft Internet Explorer nicht anhand des Antischadsoftwareprogramms, ob das Erstellen einer Instanz des ActiveX-Steuerelements sicher ist. Benutzer können diese Option über die Sicherheitseinstellungen von Internet Explorer aktivieren und deaktivieren.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067152)

  **Standardeinstellung:** Deaktiviert

::: zone-end
::: zone pivot="mdm-preview,mdm-may-2019"

- **Internet Explorer: Internetzone: Zugriff auf Datenquellen**:  
  Durch diese Richtlinieneinstellung können Sie festlegen, ob Internet Explorer mithilfe von Microsoft XML Parser (MSXML) oder ActiveX Data Objects (ADO) auf Daten aus anderen Sicherheitszonen zugreifen kann. Wenn Sie diese Richtlinieneinstellung aktivieren, können Benutzer eine Seite in die Zone laden, die MSXML oder ADO verwendet, um auf Daten in einer anderen Site in der Zone zuzugreifen. Wenn Sie im Dropdownfeld „Prompt“ (Bestätigen) auswählen, werden Benutzer dazu aufgefordert, zu entscheiden, ob eine Seite in der Zone geladen werden soll, die MSXML oder ADO verwendet, um auf Daten in einer anderen Site in der Zone zuzugreifen. Wenn Sie diese Richtlinieneinstellung deaktivieren, können Benutzer keine Seite in die Zone laden, die MSXML oder ADO verwendet, um auf Daten in einer anderen Site in der Zone zuzugreifen. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, können Benutzer keine Seite in die Zone laden, die MSXML oder ADO verwendet, um auf Daten in einer anderen Site in der Zone zuzugreifen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067078)  

  **Standardeinstellung:** Deaktivieren

- **Internet Explorer: Eingeschränkte Zone: Ziehen von Inhalten aus unterschiedlichen Domänen innerhalb von Fenstern**:  
  Mit dieser Richtlinieneinstellung können Sie Optionen zum Ziehen von Inhalten von einer Domäne in eine andere festlegen, wenn sich Quelle und Ziel im selben Fenster befinden. Wenn Sie diese Richtlinieneinstellung aktiveren und auf „Aktivieren“ klicken, können Benutzer Inhalte von einer Domäne in eine andere ziehen, wenn sich Quelle und Ziel im selben Fenster befinden. Benutzer können diese Einstellung nicht ändern. Wenn Sie diese Richtlinieneinstellung aktiveren und auf „Deaktivieren“ klicken, können die Benutzer keine Inhalte von einer Domäne in eine andere ziehen, wenn sich Quelle und Ziel im selben Fenster befinden. Die Benutzer können diese Einstellung im Dialogfeld „Internetoptionen“ nicht ändern. Wenn Sie diese Richtlinieneinstellung in Internet Explorer 10 deaktivieren oder nicht konfigurieren, können die Benutzer keine Inhalte von einer Domäne in eine andere ziehen, wenn sich Quelle und Ziel im selben Fenster befinden. Die Benutzer können diese Einstellung im Dialogfeld „Internetoptionen“ ändern. Wenn Sie diese Richtlinieneinstellung in Internet Explorer 9 oder einer früheren Version deaktivieren oder nicht konfigurieren, können die Benutzer Inhalte von einer Domäne in eine andere ziehen, wenn sich Quelle und Ziel im selben Fenster befinden. Die Benutzer können diese Einstellung im Dialogfeld „Internetoptionen“ nicht ändern.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067079)  

  **Standardeinstellung:** Deaktiviert

- **Internet Explorer: Warnung bei Zertifikatadresskonflikten**:  
  Mit dieser Richtlinieneinstellung können Sie die Sicherheitswarnung für Zertifikatadressenkonflikte aktivieren. Wenn diese Richtlinieneinstellung aktiviert ist, wird der Benutzer gewarnt, wenn eine sichere HTTP-Website (HTTPS) Zertifikate enthält, die für eine andere Adresse ausgestellt wurden. Durch diese Warnung können Spoofingangriffe verhindert werden. Wenn Sie diese Richtlinieneinstellung aktivieren, wird die Warnung für Zertifikatadressenkonflikte immer angezeigt. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, kann der Benutzer über die Seite „Erweitert“ in der Internetsystemsteuerung festlegen, ob die Warnung für Zertifikatadressenkonflikte angezeigt wird.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067153)  

  **Standardeinstellung:** Aktiviert

- **Internet Explorer: Eingeschränkte Zone: Websites mit niedrigeren Berechtigungen**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob Websites aus Zonen mit geringeren Berechtigungen, z.B. aus der Internetzone, zu dieser Zone navigieren können. Wenn Sie diese Richtlinieneinstellung aktivieren, können Websites aus Zonen mit geringeren Berechtigungen neue Fenster in dieser Zone öffnen oder zu dieser Zone navigieren. Die Sicherheitszone wird ohne den zusätzlichen Schutz durch das Sicherheitsfeature „Schutz vor Zonenanhebung“ ausgeführt. Wenn Sie im Dropdownfeld „Bestätigen“ auswählen, wird der Benutzer gewarnt, dass er dabei ist, in einen möglicherweise gefährlichen Bereich zu navigieren. Wenn Sie diese Richtlinieneinstellung deaktivieren, werden potentiell gefährliche Navigationsvorgänge verhindert. Wie von „Schutz vor Zonenanhebung“ festgelegt, ist das Internet Explorer-Sicherheitsfeature ist in dieser Zone aktiviert. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, werden potentiell gefährliche Navigationsvorgänge verhindert. Wie von „Schutz vor Zonenanhebung“ festgelegt, ist das Internet Explorer-Sicherheitsfeature ist in dieser Zone aktiviert.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067148)

  **Standardeinstellung:** Deaktivieren

- **Internet Explorer: Eingeschränkte Zone: Automatische Aufforderung für Dateidownloads**:  
  Mit dieser Richtlinieneinstellung wird festgelegt, ob eine Eingabeaufforderung bei Dateidownloads angezeigt wird, die nicht vom Benutzer gestartet werden. Downloaddialogfelder werden unabhängig von dieser Einstellung für vom Benutzer gestartete Downloadvorgänge angezeigt. Wenn Sie diese Einstellung aktivieren, werden den Benutzern Downloaddialogfelder für automatische Downloadversuche angezeigt. Wenn Sie diese Einstellung deaktivieren oder nicht konfigurieren, werden Dateidownloads, die nicht von Benutzern gestartet werden, blockiert, und Benutzern wird die Benachrichtigungsleiste anstelle des Downloaddialogfelds angezeigt. Die Benutzer können dann auf die Benachrichtigungsleiste klicken, um den Dateidownload zu genehmigen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067150)

  **Standardeinstellung:** Deaktiviert

- **Internet Explorer: Internetzone: Komponenten, die .NET Framework erfordern**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob .NET Framework-Komponenten, die nicht mit Authenticode signiert wurden, von Internet Explorer ausgeführt werden können. Dazu zählen verwaltete Steuerelemente, auf die über Objekttags verwiesen wird, sowie verwaltete ausführbare Dateien, auf die über einen Link verwiesen wird. Wenn Sie diese Richtlinieneinstellung aktivieren, führt Internet Explorer nicht signierte verwaltete Komponenten aus. Wenn Sie im Dropdownfeld „Bestätigen“ auswählen, fordert Internet Explorer den Benutzer dazu auf, zu entscheiden, ob nicht signierte verwaltete Komponenten ausgeführt werden sollen. Wenn Sie diese Richtlinieneinstellung deaktivieren, führt Internet Explorer nicht signierte verwaltete Komponenten nicht aus. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, führt Internet Explorer nicht signierte verwaltete Komponenten aus.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067073)

  **Standardeinstellung:** Deaktivieren

- **Internet Explorer: Internetzone: Nur genehmigte Domänen können TDC-ActiveX-Steuerelemente verwenden**:  
  Diese Richtlinieneinstellung steuert, ob der Benutzer das TDC-ActiveX-Steuerelement auf Websites ausführen kann. Wenn Sie diese Richtlinieneinstellung aktivieren, wird das TDC-ActiveX-Steuerelement nicht von Websites in dieser Zone ausgeführt. Wenn Sie diese Richtlinieneinstellung deaktivieren, wird das TDC-ActiveX-Steuerelement von allen Websites in dieser Zone ausgeführt.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067151)

  **Standardeinstellung:** Aktiviert

- **Internet Explorer: Eingeschränkte Zone: Per Skript ausgelöste Fenster**:  
  Mit dieser Richtlinieneinstellung können Sie die Einschränkungen zu durch Skripts geöffneten Popupfenstern und Fenstern mit Titel und Leisten verwalten. Wenn Sie diese Richtlinieneinstellung aktivieren, gilt das Sicherheitsfeature für Fenstereinschränkungen in dieser Zone nicht. Die Sicherheitszone wird also ohne die Sicherheitsebene ausgeführt, die von diesem Feature bereitgestellt wird. Wenn Sie diese Richtlinieneinstellung deaktivieren, können potenziell schädliche Aktionen aus durch Skripts initiierten Popupfenstern und Fenstern mit Titeln und Leisten nicht ausgeführt werden. Dieses Sicherheitsfeature von Internet Explorer wird in der Zone so verwendet, wie es im Sicherheitsfeature für durch Skripts geöffnete Fenster für den Prozess festgelegt ist. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, können potenziell schädliche Aktionen aus durch Skripts initiierten Popupfenstern und Fenstern mit Titeln und Leisten nicht ausgeführt werden. Dieses Sicherheitsfeature von Internet Explorer wird in der Zone so verwendet, wie es im Sicherheitsfeature für durch Skripts geöffnete Fenster für den Prozess festgelegt ist.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067075)

  **Standardeinstellung:** Deaktiviert

- **Internet Explorer: Internetzone: Lokalen Pfad beim Hochladen von Dateien auf den Server einbeziehen**:  
  Mit dieser Richtlinieneinstellung können Sie festlegen, ob Informationen zu lokalen Pfaden beim Hochladen einer Datei über ein HTML-Formular übermittelt werden. Wenn die Informationen zu lokalen Pfaden übermittelt werden, kann es vorkommen, dass einige davon versehentlich für den Server offengelegt werden. Dabei kann es sich beispielsweise um Dateien vom Desktop des Benutzers handeln, die den Benutzernamen im Pfad enthalten. Wenn Sie diese Richtlinieneinstellung aktivieren, werden die Pfadinformationen beim Hochladen einer Datei über ein HTML-Formular übermittelt. Wenn Sie diese Richtlinieneinstellung deaktivieren, werden die Pfadinformationen beim Hochladen einer Datei über ein HTML-Formular entfernt. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, kann der Benutzer entscheiden, ob Pfadinformationen beim Hochladen einer Datei über ein HTML-Formular übermittelt werden sollen. Die Pfadinformationen werden standardmäßig gesendet.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067072)

  **Standardeinstellung:** Deaktiviert

- **Internet Explorer: Prozesse im erweiterten geschützten Modus deaktivieren**:  
  Mit dieser Richtlinieneinstellung wird bestimmt, ob 64-Bit-Prozesse (höhere Sicherheit) oder 32-Bit-Prozesse (bessere Kompatibilität) von Internet Explorer 11 verwendet werden, wenn unter 64-Bit-Versionen von Windows der erweiterte geschützte Modus aktiv ist. Wichtig: Einige ActiveX-Steuerelemente und Symbolleisten sind möglicherweise nicht verfügbar, wenn 64-Bit-Prozesse verwendet werden. Wenn Sie diese Richtlinieneinstellung aktivieren, werden 64-Bit-Registerkartenprozesse von Internet Explorer 11 verwendet, sofern der erweiterte geschützte Modus unter 64-Bit-Versionen von Windows aktiv ist. Wenn Sie diese Richtlinieneinstellung deaktivieren, werden 32-Bit-Registerkartenprozesse von Internet Explorer 11 verwendet, sofern der erweiterte geschützte Modus unter 64-Bit-Versionen von Windows aktiv ist. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, können Benutzer dieses Feature über die Internet Explorer-Einstellungen ein- oder ausschalten. Dieses Feature ist standardmäßig deaktiviert.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067149)

  **Standardeinstellung:** Aktiviert

- **Internet Explorer: Zertifikatfehler ignorieren**:  
  Diese Richtlinieneinstellung verhindert, dass der Benutzer SSL/TLS-Zertifikatfehler (Secure Sockets Layer/Transport Layer Security), die die Navigation in Internet Explorer unterbrechen (z.B. „Abgelaufen“, „Gesperrt“ oder „Name stimmt nicht überein“ ) ignoriert. Wenn Sie diese Richtlinieneinstellung aktivieren, können Benutzer das Browsen nicht mehr fortsetzen. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, kann der Benutzer Zertifikatfehler ignorieren und das Browsen fortsetzen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067071)

  **Standardeinstellung:** Deaktiviert

- **Internet Explorer: Internetzone: Laden von XAML-Dateien**:  
  Mit dieser Richtlinieneinstellung können Sie das Laden von XAML-Dateien (Extensible Application Markup Language) verwalten. XAML ist eine deklarative Markupsprache auf XML-Grundlage, die normalerweise zum Erstellen intelligenter Benutzeroberflächen und Grafiken verwendet wird, die Windows Presentation Foundation nutzen. Wenn Sie diese Richtlinieneinstellung aktivieren und im Dropdownfeld „Aktivieren“ festgelegt ist, werden die XAML-Dateien automatisch in Internet Explorer geladen. Benutzer können dieses Verhalten nicht ändern. Wenn Sie im Dropdownfeld „Bestätigen“ auswählen, wird der Benutzer zum Laden von XAML-Dateien aufgefordert. Wenn Sie diese Richtlinieneinstellung deaktivieren, werden XAML-Dateien nicht in Internet Explorer geladen. Benutzer können dieses Verhalten nicht ändern. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, können Benutzer entscheiden, ob XAML-Dateien in Internet Explorer geladen werden sollen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067147)

  **Standardeinstellung:** Deaktivieren

::: zone-end
::: zone pivot="mdm-may-2019"

- **Internet Explorer: Internetzone: Automatische Aufforderung für Dateidownloads**:  
  Mit dieser Richtlinieneinstellung wird festgelegt, ob eine Eingabeaufforderung bei Dateidownloads angezeigt wird, die nicht vom Benutzer gestartet werden. Downloaddialogfelder werden unabhängig von dieser Einstellung für vom Benutzer gestartete Downloadvorgänge angezeigt. Wenn Sie diese Einstellung aktivieren, werden den Benutzern Downloaddialogfelder für automatische Downloadversuche angezeigt. Wenn Sie diese Einstellung deaktivieren oder nicht konfigurieren, werden Dateidownloads, die nicht von Benutzern gestartet werden, blockiert, und Benutzern wird die Benachrichtigungsleiste anstelle des Downloaddialogfelds angezeigt. Die Benutzer können dann auf die Benachrichtigungsleiste klicken, um den Dateidownload zu genehmigen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067117)

  **Standardeinstellung:** Deaktiviert

::: zone-end
::: zone pivot="mdm-preview"

- **Internet Explorer: Internetzone: Automatische Aufforderung für Dateidownloads**:  
  Mit dieser Richtlinieneinstellung wird festgelegt, ob eine Eingabeaufforderung bei Dateidownloads angezeigt wird, die nicht vom Benutzer gestartet werden. Downloaddialogfelder werden unabhängig von dieser Einstellung für vom Benutzer gestartete Downloadvorgänge angezeigt. Wenn Sie diese Einstellung aktivieren, werden den Benutzern Downloaddialogfelder für automatische Downloadversuche angezeigt. Wenn Sie diese Einstellung deaktivieren oder nicht konfigurieren, werden Dateidownloads, die nicht von Benutzern gestartet werden, blockiert, und Benutzern wird die Benachrichtigungsleiste anstelle des Downloaddialogfelds angezeigt. Die Benutzer können dann auf die Benachrichtigungsleiste klicken, um den Dateidownload zu genehmigen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067117)

  **Standardeinstellung:** Aktiviert

::: zone-end
::: zone pivot="mdm-preview,mdm-may-2019"

- **Internet Explorer: Eingeschränkte Zone: Sicherheitswarnung für potenziell unsichere Dateien**:  
  Mit dieser Richtlinieneinstellung wird bestimmt, ob die Nachricht „Datei öffnen – Sicherheitswarnung“ angezeigt wird, wenn der Benutzer versucht, ausführbare Dateien oder andere potenziell unsichere Dateien (z.B. aus einer Dateifreigabe im Intranet über den Datei-Explorer) zu öffnen. Wenn Sie diese Richtlinieneinstellung aktivieren und „Aktivieren“ im Dropdownfeld auswählen, werden diese Dateien ohne Sicherheitswarnung geöffnet. Wenn Sie das Dropdownfeld auf „Bestätigen“ einstellen, wird eine Sicherheitswarnung angezeigt, bevor die Dateien geöffnet werden. Wenn Sie diese Richtlinieneinstellung deaktivieren, werden diese Dateien nicht geöffnet. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, kann der Benutzer konfigurieren, wie der Computer diese Dateien behandeln soll. Standardmäßig werden diese Dateien in der eingeschränkten Zone blockiert, in der Intranetzone sowie in Zonen für lokale Computer aktiviert und in Internetzonen und vertrauenswürdigen Zonen auf „Bestätigen“ festgelegt.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2066797)

  **Standardeinstellung:** Deaktivieren

- **Internet Explorer: Internetzone: Cross-Site Scripting-Filter**:  
  Mit dieser Richtlinie können Sie steuern, ob websiteübergreifende Skripteinschleusungen in Websites in dieser Zone vom XSS-Filter (Cross-Site Scripting) erkannt und verhindert werden. Wenn Sie diese Richtlinieneinstellung aktivieren, ist der XSS-Filter für Websites in dieser Zone aktiviert, um Versuche einer websiteübergreifenden Skripteinschleusung zu blockieren. Wenn Sie diese Richtlinieneinstellung deaktivieren, wird der XSS-Filter für Websites in dieser Zone deaktiviert, und Internet Explorer lässt die websiteübergreifende Skripteinschleusung zu.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067053)

  **Standardeinstellung:** Aktiviert

- **Internet Explorer: Fallback auf SSL3**:  
  Mit dieser Richtlinieneinstellung können Sie unsichere Fallbacks auf SSL 3.0 blockieren. Wenn die Richtlinie aktiviert ist und TLS 1.0 oder höher einen Fehler verursacht, versucht Internet Explorer, über SSL 3.0 oder eine niedrigere Version eine Verbindung mit Websites herzustellen. Um einen Man-in-the-Middle-Angriff zu vermeiden, sollten Sie unsichere Fallbacks nicht zulassen. Die Richtlinie wirkt sich nicht darauf aus, welche Sicherheitsprotokolle aktiviert sind. Wenn Sie diese Richtlinie deaktivieren, werden die Standardeinstellungen des Systems verwendet.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067118)

  **Standardeinstellung:** Keine Websites

::: zone-end
::: zone pivot="mdm-may-2019"

- **Internet Explorer: Verschlüsselungsunterstützung:**  
  Mit dieser Richtlinieneinstellung können Sie die Unterstützung der Versionen 1.0, 1.1 und 1.2 von Transport Layer Security (TLS) und der Versionen 2.0 und 3.0 von Secure Sockets Layer (SSL) im Browser deaktivieren. TLS und SSL sind Protokolle, die die Kommunikation zwischen Browser und Zielserver schützen. Wenn der Browser versucht, die geschützte Kommunikation mit dem Zielserver einzurichten, vereinbaren der Browser und der Server, welches Protokoll und welche Version verwendet werden sollen. Der Browser und der Server versuchen, ihre jeweiligen Listen mit unterstützten Protokollen und Versionen abzugleichen und wählen die bevorzugte Übereinstimmung aus. Wenn Sie diese Richtlinieneinstellung aktivieren, handelt der Browser ggf. über die von Ihnen in der Dropdownliste ausgewählten Verschlüsselungsmethoden einen Verschlüsselungstunnel aus. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, kann der Benutzer auswählen, welche Verschlüsselungsmethode der Browser unterstützen soll.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067057)

  **Standardeinstellung:** 2 Elemente:  TLS v1.1 und TLS v1.2  
  *Wenn Sie auf den Pfeil nach unten klicken, werden die verschiedenen Optionen angezeigt, die Sie für diese Einstellung auswählen können.*

::: zone-end
::: zone pivot="mdm-preview,mdm-may-2019"

- **Internet Explorer: Sperrung der Internetzone: SmartScreen**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob der SmartScreen-Filter Seiten in dieser Zone auf schädlichen Inhalt überprüft. Wenn Sie diese Richtlinieneinstellung aktivieren, überprüft der SmartScreen-Filter Seiten in dieser Zone auf schädlichen Inhalt. Wenn Sie diese Richtlinieneinstellung deaktivieren, werden Seiten in dieser Zone vom SmartScreen-Filter nicht auf schädlichen Inhalt überprüft. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, kann der Benutzer entscheiden, ob der SmartScreen-Filter Seiten in dieser Zone auf schädlichen Inhalt überprüft. Anmerkung: In Internet Explorer 7 steuert diese Richtlinieneinstellung, ob der Phishingfilter Seiten in dieser Zone auf schädlichen Inhalt überprüft.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067059)

  **Standardeinstellung:** Aktiviert

- **Internet Explorer: Eingeschränkte Zone: Anwendungen und Dateien in einem IFRAME starten**:  
  Mit dieser Richtlinieneinstellung können Sie steuern, ob Anwendungen ausgeführt und Dateien aus einem iFrame-Verweis im HTML-Code der Seiten in dieser Zone heruntergeladen werden können. Wenn Sie diese Richtlinieneinstellung aktivieren, können Benutzer Anwendungen ausführen und Dateien aus iFrames auf den Seiten in dieser Zone ohne Benutzereingriff herunterladen. Wenn Sie „Bestätigen“ aus dem Dropdownfeld auswählen, werden Benutzer dazu aufgefordert, zu entscheiden, ob Anwendungen ausgeführt und Daten aus iFrames auf den Seiten in dieser Zone heruntergeladen werden. Wenn Sie diese Richtlinieneinstellung deaktivieren, können die Benutzer über iFrames auf den Seiten in dieser Zone weder Anwendungen ausführen noch Dateien herunterladen. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, können Benutzer aus iFrames auf den Seiten in dieser Zone keine Anwendungen ausführen und Dateien herunterladen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067061)

  **Standardeinstellung:** Deaktivieren

- **Internet Explorer: Umgehung von SmartScreen-Warnungen zu ungewöhnlichen Dateien**:  
  Mit dieser Richtlinieneinstellung wird bestimmt, ob Benutzer Warnungen des SmartScreen-Filters umgehen können. Der SmartScreen-Filter warnt Benutzer vor ausführbaren Dateien im Internet, die selten von Benutzern heruntergeladen werden. Wenn Sie diese Richtlinieneinstellung aktivieren, hindern die Warnungen des SmartScreen-Filters Benutzer am Herunterladen. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, können Benutzer die Warnungen des SmartScreen-Filters umgehen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067068)

  **Standardeinstellung:** Deaktiviert

- **Internet Explorer: Internetzone: Popupblocker**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob unerwünschte Popupfenster angezeigt werden. Popupfenster, die geöffnet werden, wenn der Endbenutzer auf einen Link klickt, werden nicht blockiert. Wenn Sie diese Richtlinieneinstellung aktivieren, werden die meisten unerwünschten Popupfenster nicht angezeigt. Wenn Sie diese Richtlinieneinstellung deaktivieren, werden Popupfenster angezeigt. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, werden die meisten unerwünschten Popupfenster nicht angezeigt.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067069)

  **Standardeinstellung:** Aktivieren Sie

- **Internet Explorer-Prozesse: Konsistente MIME-Verarbeitung**:  
  Internet Explorer enthält dynamische Binärverhalten: Komponenten, die spezifische Funktionalität für die HTML-Elemente einkapseln, an die sie angefügt sind. Mit dieser Richtlinieneinstellung wird gesteuert, ob Binärverhalten durch die Sicherheitseinschränkungen verhindert oder zugelassen wird. Wenn Sie diese Richtlinieneinstellung aktivieren, werden Binärverhalten für alle Datei-Explorer- und Internet Explorer-Prozesse verhindert. Wenn Sie diese Richtlinieneinstellung deaktivieren, werden Binärverhalten für alle Datei-Explorer- und Internet Explorer-Prozesse zugelassen. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, werden Binärverhalten für alle Datei-Explorer- und Internet Explorer-Prozesse verhindert.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067144)  

  **Standardeinstellung:** Aktiviert

- **Internet Explorer: Eingeschränkte Zone: Java-Berechtigungen**:  
  Mit dieser Richtlinieneinstellung können Sie Berechtigungen für Java-Applets verwalten. Durch das Aktivieren dieser Richtlinieneinstellung können Sie Optionen aus dem Dropdownfeld auswählen. Wählen Sie „Benutzerdefiniert“ aus, um Berechtigungseinstellungen einzeln zu bestimmen. Wählen Sie „Niedrige Sicherheit“ aus, um Applets die Ausführung aller Vorgänge zu ermöglichen. Wählen Sie „Mittlere Sicherheit“ aus, um Applets die Ausführung in der zugehörigen Sandbox (ein Bereich im Speicher, außerhalb dessen das Programm keine Aufrufe ausführen kann) sowie Funktionen wie den sicheren Speicherbereich (ein geschützter und sicherer Speicherbereich auf dem Clientcomputer) und die benutzergesteuerte Datei-E/A zu ermöglichen. Wählen Sie „Hohe Sicherheit“ aus, um Applets die Ausführung in der zugehörigen Sandbox zu ermöglichen. Deaktivieren Sie Java, um zu verhindern, dass Applets ausgeführt werden. Wenn Sie diese Richtlinieneinstellung deaktivieren, können Java-Applets nicht ausgeführt werden. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, sind Java-Applets deaktiviert.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067132)

  **Standardeinstellung:** Java deaktivieren

- **Internet Explorer: ActiveX-Steuerelemente im geschützten Modus**:  
  Diese Richtlinieneinstellung verhindert, dass ActiveX-Steuerelemente im geschützten Modus ausgeführt werden, wenn der erweiterte geschützte Modus aktiviert ist. Hat ein Benutzer eine ActiveX-Kontrolle installiert, die nicht mit dem erweiterten geschützten Modus kompatibel ist, und versucht eine Website, diese Kontrolle zu laden, zeigt Internet Explorer dem Benutzer eine entsprechende Benachrichtigung an und bietet die Option an, die Website im regulären geschützten Modus auszuführen. Diese Richtlinieneinstellung deaktiviert diese Benachrichtigung und erzwingt, dass alle Websites im erweiterten geschützten Modus ausgeführt werden. Der erweiterte geschützte Modus bietet durch die Verwendung von 64-Bit-Prozessen auf 64-Bit-Versionen von Windows zusätzlichen Schutz gegen schädliche Websites. Bei Computern mit Windows 8 oder höher beschränkt der erweiterte geschützte Modus außerdem die Speicherorte von Internet Explorer in der Registrierung und im Dateisystem. Wenn ein Benutzer bei aktiviertem erweiterten geschützten Modus eine Website aufruft, die versucht, eine ActiveX-Kontrolle zu laden, die nicht mit dem erweiterten geschützten Modus kompatibel ist, zeigt Internet Explorer dem Benutzer eine entsprechende Benachrichtigung an und bietet die Option an, die Website im regulären geschützten Modus auszuführen. Wenn Sie diese Richtlinieneinstellung deaktivieren, zeigt der Internet Explorer dem Benutzer die Option, den erweiterten geschützten Modus zu deaktivieren, nicht an. Alle Websites im geschützten Modus werden im erweiterten geschützten Modus ausgeführt. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, zeigt Internet Explorer dem Benutzer eine Benachrichtigung an, in der er ihm die Option bietet, Websites mit nicht kompatiblen ActiveX-Kontrollen im regulären geschützten Modus auszuführen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067145)

  **Standardeinstellung:** Deaktiviert

- **Internet Explorer: Eingeschränkte Zone: Laden von XAML-Dateien**:  
  Mit dieser Richtlinieneinstellung können Sie das Laden von XAML-Dateien (Extensible Application Markup Language) verwalten. XAML ist eine deklarative Markupsprache auf XML-Grundlage, die normalerweise zum Erstellen intelligenter Benutzeroberflächen und Grafiken verwendet wird, die Windows Presentation Foundation nutzen. Wenn Sie diese Richtlinieneinstellung aktivieren und im Dropdownfeld „Aktivieren“ festgelegt ist, werden die XAML-Dateien automatisch in Internet Explorer geladen. Benutzer können dieses Verhalten nicht ändern. Wenn Sie im Dropdownfeld „Bestätigen“ auswählen, wird der Benutzer zum Laden von XAML-Dateien aufgefordert. Wenn Sie diese Richtlinieneinstellung deaktivieren, werden XAML-Dateien nicht in Internet Explorer geladen. Benutzer können dieses Verhalten nicht ändern. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, können Benutzer entscheiden, ob XAML-Dateien in Internet Explorer geladen werden sollen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067070)

  **Standardeinstellung:** Deaktivieren

- **Internet Explorer-Prozesse: Sicherheitseinschränkungen für Skriptfenster**:  
  Internet Explorer lässt zu, das Skripts programmgesteuert Fenster verschiedener Typen öffnen und in Größe und Position anpassen können. Die Sicherheitsfunktion für Fenstereinschränkungen schränkt Popupfenster ein und verhindert, dass Skripts Fenster anzeigen, in denen Titel- und Statusleiste für den Benutzer nicht sichtbar sind oder die die Sichtbarkeit der Titel- und Statusleiste anderer Fenster behindern. Wenn Sie diese Richtlinieneinstellung aktivieren, werden Skriptfenster für alle Prozesse eingeschränkt. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, werden Skriptfenster nicht eingeschränkt.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067146)

  **Standardeinstellung:** Aktiviert

- **Internet Explorer: Eingeschränkte Zone: ActiveX-Steuerelemente und Plug-Ins ausführen**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob ActiveX-Steuerelemente und Plug-Ins über die festgelegte Zone auf Seiten in Internet Explorer ausgeführt werden kann. Wenn Sie diese Richtlinieneinstellung aktivieren, werden Steuerelemente und Plug-Ins ohne Benutzereingriff ausgeführt. Wenn Sie die Option „Bestätigen“ im Dropdownfeld ausgewählt haben, werden Benutzer dazu aufgefordert, auszuwählen, ob Steuerelemente oder Plug-Ins ausgeführt werden dürfen. Wenn Sie diese Richtlinieneinstellung deaktivieren, werden Steuerelemente und Plug-Ins nicht ausgeführt. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, werden Steuerelemente und Plug-Ins nicht ausgeführt.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067114)

  **Standardeinstellung:** Deaktivieren

- **Internet Explorer: Eingeschränkte Zone: ActiveX-Steuerelemente ausführen, die als „Sicher für Skripts“ markiert sind**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob ein ActiveX-Steuerelement, das für die Skripterstellung als sicher gekennzeichnet wurde, mit einem Skript interagieren darf. Wenn Sie diese Richtlinie aktivieren, kann mit Skripts automatisch ohne Benutzereingriff interagiert werden. Wenn Sie im Dropdownfeld „Bestätigen“ auswählen, werden die Benutzer zur Bestätigung aufgefordert, ob sie die Skriptinteraktion erlauben möchten. Wenn Sie diese Richtlinieneinstellung deaktivieren, ist keine Skriptinteraktion erlaubt. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, ist keine Skriptinteraktion erlaubt.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067062)

  **Standardeinstellung:** Deaktivieren

- **Internet Explorer: Eingeschränkte Zone: Anmeldeoptionen**:  
  Mit dieser Richtlinieneinstellung können Sie Einstellungen für Anmeldeoptionen verwalten. Durch das Aktivieren dieser Richtlinieneinstellung können Sie eine der folgenden Anmeldeoptionen auswählen.

  - *Anonym*: Verwenden Sie die anonyme Anmeldung, um die HTTP-Authentifizierung zu deaktivieren. Das Gastkonto kann nur für das CIFS-Protokoll (Common Internet File System) verwendet werden.

  - *Nach Benutzername und Kennwort fragen*: Verwenden Sie „Nach Benutzername und Kennwort fragen“, um die Benutzer-IDs und Kennwörter von Benutzern abzufragen. Nachdem ein Benutzer abgefragt wurde, können diese Werte für den Rest der Sitzung im Hintergrund verwendet werden.

  - *Automatisches Anmelden nur in der Intranetzone* – Verwenden Sie diese Option, um Benutzer-IDs und Kennwörter von Benutzern in anderen Zonen abzufragen. Nachdem ein Benutzer abgefragt wurde, können diese Werte für den Rest der Sitzung im Hintergrund verwendet werden.

  - *Automatische Anmeldung mit aktuellem Benutzernamen und Kennwort* – Verwenden Sie diese Option, um die Anmeldung mithilfe der NTLM-Authentifizierung (auch bekannt als „integrierte Windows-Authentifizierung“ oder „Windows NT Challenge Response“) durchzuführen. Wenn der Server die NTLM-Authentifizierung unterstützt, wird der Netzwerkbenutzername und das Kennwort des Benutzers für die Anmeldung verwendet. Wenn die NTLM-Authentifizierung vom Server nicht unterstützt wird, wird der Benutzer dazu aufgefordert, seinen Benutzernamen und sein Kennwort einzugeben.

  Wenn Sie diese Richtlinieneinstellung deaktivieren, wird die *automatische Anmeldung nur in der Intranetzone zugelassen*. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, wird *Nach Benutzername und Kennwort fragen* für die Anmeldung festgelegt.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067110)

  **Standardeinstellung:** Anonym

- **Internet Explorer: Vertrauenswürdige Zone: Nicht als sicher markierte ActiveX-Steuerelemente initialisieren und ausführen**:  
  Mit dieser Richtlinieneinstellung können Sie ActiveX-Steuerelemente verwalten, die als unsicher gekennzeichnet sind. Wenn Sie diese Richtlinieneinstellung aktivieren, werden ActiveX-Steuerelemente ausgeführt und mit Parametern geladen, und das Skript wird ohne Festlegen der Objektsicherheit für nicht vertrauenswürdige Daten oder Skripts erstellt. Von dieser Einstellung wird abgeraten, es sei denn, es handelt sich um sichere und verwaltete Zonen. Mit dieser Einstellung werden sowohl unsichere als auch sichere Steuerelemente initialisiert und Skripte für diese erstellt, ohne dabei die Option „ActiveX-Steuerelemente ausführen, die für Skripting sicher sind“ zu beachten. Wenn Sie diese Richtlinieneinstellung aktivieren und die Option „Prompt“ (Bestätigen) im Dropdownfeld auswählen, werden Benutzer dazu aufgefordert, auszuwählen, ob das Steuerelement mit Parametern geladen oder ein Skript erstellt werden soll. Wenn Sie diese Richtlinieneinstellung deaktivieren, werden ActiveX-Steuerelemente, die nicht als sicher gekennzeichnet werden können, nicht geladen, und es wird kein Skript erstellt. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, werden Benutzer dazu aufgefordert, auszuwählen, ob das Steuerelement mit Parametern geladen oder ein Skript erstellt werden soll.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067137)

  **Standardeinstellung:** Deaktivieren

- **Internet Explorer: Auf gesperrte Serverzertifikate überprüfen**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob Internet Explorer den Widerrufstatus der Serverzertifikat prüft. Zertifikate werden widerrufen, wenn sie kompromittiert wurden oder nicht mehr gültig sind. Durch diese Option wird verhindert, dass Benutzer vertrauliche Daten an eine Website übermitteln, die unter Betrugsverdacht steht oder nicht sicher ist. Wenn Sie diese Richtlinieneinstellung aktivieren, prüft Internet Explorer, ob Serverzertifikate widerrufen wurden. Wenn Sie diese Richtlinieneinstellung deaktivieren, prüft Internet Explorer nicht, ob Serverzertifikate widerrufen wurden. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, prüft Internet Explorer nicht, ob Serverzertifikate widerrufen wurden.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067046)

  **Standardeinstellung:** Aktiviert

- **Internet Explorer: Internetzone: Websites mit weniger Berechtigungen**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob Websites aus Zonen mit geringeren Berechtigungen, z.B. eingeschränkte Websites, zu dieser Zone navigieren können. Wenn Sie diese Richtlinieneinstellung aktivieren, können Websites aus Zonen mit geringeren Berechtigungen neue Fenster in dieser Zone öffnen oder zu dieser Zone navigieren. Die Sicherheitszone wird ohne den zusätzlichen Schutz durch das Sicherheitsfeature „Schutz vor Zonenanhebung“ ausgeführt. Wenn Sie im Dropdownfeld „Bestätigen“ auswählen, wird der Benutzer gewarnt, dass er dabei ist, in einen möglicherweise gefährlichen Bereich zu navigieren. Wenn Sie diese Richtlinieneinstellung deaktivieren, werden potentiell gefährliche Navigationsvorgänge verhindert. Wie von „Schutz vor Zonenanhebung“ festgelegt, ist das Internet Explorer-Sicherheitsfeature ist in dieser Zone aktiviert. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, können Websites aus Zonen mit geringeren Berechtigungen neue Fenster in dieser Zone öffnen oder zu dieser Zone navigieren.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067109)

  **Standardeinstellung:** Deaktivieren

- **Internet Explorer: Eingeschränkte Zone: Dateidownloads**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob Dateidownloads aus dieser Zone zulässig sind. Diese Option hängt von der Zone der Webseite ab, die den Downloadlink enthält, und nicht von der Zone, in die heruntergeladen wird. Wenn Sie diese Richtlinieneinstellung aktivieren, können Dateien aus der Zone heruntergeladen werden. Wenn Sie diese Richtlinieneinstellung deaktivieren, können keine Dateien aus der Zone heruntergeladen werden. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, können keine Dateien aus der Zone heruntergeladen werden.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067038)

  **Standardeinstellung:** Deaktivieren

- **Internet Explorer: Internetzone: Mit Authenticode signierte Komponenten ausführen, die .NET Framework erfordern**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob .NET Framework-Komponenten, die mit Authenticode signiert wurden, von Internet Explorer ausgeführt werden können. Dazu zählen verwaltete Steuerelemente, auf die über Objekttags verwiesen wird, sowie verwaltete ausführbare Dateien, auf die über einen Link verwiesen wird. Wenn Sie diese Richtlinieneinstellung aktivieren, führt Internet Explorer signierte verwaltete Komponenten aus. Wenn Sie im Dropdownfeld „Bestätigen“ auswählen, fordert Internet Explorer den Benutzer dazu auf, zu entscheiden, ob signierte verwaltete Komponenten ausgeführt werden sollen. Wenn Sie diese Richtlinieneinstellung deaktivieren, führt Internet Explorer signierte verwaltete Komponenten nicht aus. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, führt Internet Explorer signierte verwaltete Komponenten nicht aus.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067033)

  **Standardeinstellung:** Deaktivieren

- **Internet Explorer: Benutzerbezogene Installation von ActiveX-Steuerelementen verhindern**:  
  Mit dieser Richtlinieneinstellung können Sie die Installation von ActiveX-Steuerelement pro Benutzer verhindern. Wenn Sie diese Richtlinieneinstellung aktivieren, können keine ActiveX-Steuerelemente pro Benutzer installiert werden. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, können ActiveX-Steuerelemente pro Benutzer installiert werden.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067058)

  **Standardeinstellung:** Aktiviert

- **Internet Explorer: Verwaltung von SmartScreen-Filter verhindern**:  
  Diese Richtlinieneinstellung verhindert, dass der Benutzer den SmartScreen Filter verwalten kann, der den Benutzer warnt, wenn er eine Website besucht, die in der Vergangenheit durch Phishing persönliche Informationen gesammelt hat, oder wenn bekannt ist, dass die Website Schadsoftware hostet. Wenn Sie diese Richtlinieneinstellung aktivieren, wird der Benutzer nicht aufgefordert, den SmartScreen-Filter zu aktivieren. Alle Websiteadressen, die sich nicht auf der Zulassungsliste des Filters befinden, werden automatisch an Microsoft gesendet, ohne dass der Benutzer dies bestätigen muss. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, wird der Benutzer bei der ersten Ausführung aufgefordert, den SmartScreen Filter zu aktivieren oder zu deaktivieren.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067135)

  **Standardeinstellung:** Aktivieren Sie

- **Internet Explorer-Prozesse: Sicherheitsfunktion für MIME-Ermittlung**:  
  Diese Richtlinieneinstellung bestimmt, ob die MIME-Ermittlung von Internet Explorer die Höherstufung einer Datei eines bestimmten Typs auf einen gefährlicheren Dateitypen verhindert. Wenn Sie diese Einstellung aktivieren, stuft die MIME-Ermittlung eine Datei eines bestimmten Typs nie auf einen gefährlicheren Dateityp hoch. Wenn Sie diese Richtlinieneinstellung deaktivieren, lassen Internet Explorer-Prozesse die Höherstufung eines Dateityps auf einen gefährlicheren Dateityp durch die MIME-Ermittlung zu. Wenn Sie diese Einstellung nicht konfigurieren, stuft die MIME-Ermittlung eine Datei eines bestimmten Typs nie auf einen gefährlicheren Dateityp hoch.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067124)

  **Standardeinstellung:** Aktiviert

- **Internet Explorer: Eingeschränkte Zone: Download signierter ActiveX-Steuerelemente**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob Benutzer signierte ActiveX-Steuerelemente auf einer Seite in der Zone herunterladen können. Wenn Sie diese Richtlinieneinstellung aktivieren, können Benutzer signierte Steuerelemente ohne Benutzereingriff herunterladen. Wenn Sie „Bestätigen“ in der Dropdownliste auswählen, werden Benutzer zur Bestätigung aufgefordert, ob Steuerelemente von nicht vertrauenswürdigen Herausgebern heruntergeladen werden sollen. Von vertrauenswürdigen Herausgebern signierter Code wird im Hintergrund heruntergeladen. Wenn Sie diese Richtlinieneinstellung deaktivieren, können signierte Steuerelemente nicht heruntergeladen werden. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, werden die Benutzer gefragt, ob Steuerelemente von nicht vertrauenswürdigen Herausgebern heruntergeladen werden sollen. Von vertrauenswürdigen Herausgebern signierter Code wird im Hintergrund heruntergeladen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067120)

  **Standardeinstellung:** Deaktivieren

- **Internet Explorer: AutoVervollständigen**:  
  Die Funktion AutoVervollständigen kann Benutzernamen und Kennwörter speichern und beim Ausfüllen von Formularen vorschlagen. Wenn Sie diese Einstellung aktivieren, können die Benutzer die Einstellungen „Benutzernamen und Kennwörter für Formulare“ und „Nachfragen, ob Kennwörter gespeichert werden sollen“ anpassen. Die Funktion AutoVervollständigen wird für Benutzernamen und Kennwörter in Formularen aktiviert. Entscheiden Sie, ob Sie „Nachfragen, ob Kennwörter gespeichert werden sollen“ aktivieren möchten. Wenn Sie diese Einstellung deaktivieren, können die Benutzer die Einstellungen „Benutzernamen und Kennwörter für Formulare“ und „Nachfragen, ob Kennwörter gespeichert werden sollen“ nicht anpassen. Die Funktion AutoVervollständigen wird für Benutzernamen und Kennwörter in Formularen deaktiviert. Der Benutzer kann auch nicht selbst festlegen, dass er zur Bestätigung aufgefordert wird, ob das Kennwort gespeichert werden soll. Wenn Sie diese Einstellung nicht konfigurieren, kann der Benutzer AutoVervollständigen für „Benutzernamen und Kennwörter für Formulare“ und „Nachfragen, ob Kennwörter gespeichert werden sollen“ selbst aktivieren. Benutzer müssen zu „Internetoptionen“ navigieren und dann auf die Registerkarte „Inhalte“ und auf „Einstellungen“ klicken, um diese Option anzuzeigen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067122)

  **Standardeinstellung:** Deaktiviert

- **Internet Explorer: Internetzone: VBScript-Ausführung zulassen**:  
  Diese Einstellung bestimmt, ob das VBScript auf Seiten in bestimmten Internet Explorer-Zonen ausgeführt werden kann. Zu den Optionen gehören:

  - *Aktivieren*: Das VBScript wird auf Seiten in bestimmten Zonen ohne Interaktionen ausgeführt.

  - *Bestätigung*: Mitarbeiter werden aufgefordert festzulegen, ob das VBScript in der Zone ausgeführt werden soll.

  - *Deaktivieren*: Das VBScript wird in der Zone nicht ausgeführt. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, wird das VBScript ohne Interaktionen in der angegebenen Zone ausgeführt.

  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067119)

  **Standardeinstellung:** Deaktivieren

- **Internet Explorer: Eingeschränkte Zone: Nur genehmigte Domänen können TDC-ActiveX-Steuerelemente verwenden**:  
  Diese Richtlinieneinstellung steuert, ob der Benutzer das TDC-ActiveX-Steuerelement auf Websites ausführen kann. Wenn Sie diese Richtlinieneinstellung aktivieren, wird das TDC-ActiveX-Steuerelement nicht von Websites in dieser Zone ausgeführt. Wenn Sie diese Richtlinieneinstellung deaktivieren, wird das TDC-ActiveX-Steuerelement von allen Websites in dieser Zone ausgeführt.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067032)

  **Standardeinstellung:** Aktiviert

- **Internet Explorer trusted zone do not run antimalware against Active X controls** (Vertrauenswürdige Zone in Internet Explorer: Keine Antischadsoftware für ActiveX-Steuerelemente ausführen):  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob von Internet Explorer Antischadsoftwareprogramme für ActiveX-Steuerelemente ausgeführt werden, um zu überprüfen, ob sie sicher auf Seiten geladen werden können. Wenn Sie diese Richtlinieneinstellung aktivieren, prüft Internet Explorer nicht anhand des Antischadsoftwareprogramms, ob das Erstellen einer Instanz des ActiveX-Steuerelements sicher ist. Wenn Sie diese Richtlinieneinstellung deaktivieren, prüft Internet Explorer immer anhand des Antischadsoftwareprogramms, ob das Erstellen einer Instanz des ActiveX-Steuerelements sicher ist. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, prüft Internet Explorer immer anhand des Antischadsoftwareprogramms, ob das Erstellen einer Instanz des ActiveX-Steuerelements sicher ist. Benutzer können diese Option über die Sicherheitseinstellungen von Internet Explorer aktivieren und deaktivieren.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067115)

  **Standardeinstellung:** Deaktiviert

- **Internet Explorer: Zone des lokalen Computers: Java-Berechtigungen**:  
  Mit dieser Richtlinieneinstellung können Sie Berechtigungen für Java-Applets verwalten. Durch das Aktivieren dieser Richtlinieneinstellung können Sie Optionen aus dem Dropdownfeld auswählen. Wählen Sie „Benutzerdefiniert“ aus, um Berechtigungseinstellungen einzeln zu bestimmen. Wählen Sie „Niedrige Sicherheit“ aus, um Applets die Ausführung aller Vorgänge zu ermöglichen. Wählen Sie „Mittlere Sicherheit“ aus, um Applets die Ausführung in der zugehörigen Sandbox (ein Bereich im Speicher, außerhalb dessen das Programm keine Aufrufe ausführen kann) sowie Funktionen wie den sicheren Speicherbereich (ein geschützter und sicherer Speicherbereich auf dem Clientcomputer) und die benutzergesteuerte Datei-E/A zu ermöglichen. Wählen Sie „Hohe Sicherheit“ aus, um Applets die Ausführung in der zugehörigen Sandbox zu ermöglichen. Deaktivieren Sie Java, um zu verhindern, dass Applets ausgeführt werden. Wenn Sie diese Richtlinieneinstellung deaktivieren, können Java-Applets nicht ausgeführt werden. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, wird die Berechtigung auf „Mittlere Sicherheit“ festgelegt.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067113)

  **Standardeinstellung:** Java deaktivieren

- **Internet Explorer: Intranetzone: Keine Antischadsoftware für ActiveX-Steuerelemente ausführen**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob von Internet Explorer Antischadsoftwareprogramme für ActiveX-Steuerelemente ausgeführt werden, um zu überprüfen, ob sie sicher auf Seiten geladen werden können. Wenn Sie diese Richtlinieneinstellung aktivieren, prüft Internet Explorer nicht anhand des Antischadsoftwareprogramms, ob das Erstellen einer Instanz des ActiveX-Steuerelements sicher ist. Wenn Sie diese Richtlinieneinstellung deaktivieren, prüft Internet Explorer immer anhand des Antischadsoftwareprogramms, ob das Erstellen einer Instanz des ActiveX-Steuerelements sicher ist. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, prüft Internet Explorer nicht anhand des Antischadsoftwareprogramms, ob das Erstellen einer Instanz des ActiveX-Steuerelements sicher ist. Benutzer können diese Option über die Sicherheitseinstellungen von Internet Explorer aktivieren und deaktivieren.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067138)

  **Standardeinstellung:** Deaktiviert

- **Internet Explorer: Eingeschränkte Zone: Scriptlets**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob Benutzer Skriptlets ausführen können. Wenn Sie diese Richtlinieneinstellung aktivieren, können Benutzer Skriptlets ausführen. Wenn Sie diese Richtlinieneinstellung deaktivieren, können Benutzer Skriptlets nicht ausführen. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, können Benutzer Skriptlets aktivieren oder deaktivieren.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067112)

  **Standardeinstellung:** Deaktiviert

- **Internet Explorer-Prozesse: Benachrichtigungsleiste**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob die Benachrichtigungsleiste für Internet Explorer-Prozesse angezeigt wird, wenn Datei- oder Codeinstallationen eingeschränkt sind. Die Benachrichtigungsleiste wird standardmäßig für Internet Explorer-Prozesse angezeigt. Wenn Sie diese Richtlinieneinstellung aktivieren, wird die Benachrichtigungsleiste für Internet Explorer-Prozesse angezeigt. Wenn Sie diese Richtlinieneinstellung deaktivieren, wird die Benachrichtigungsleiste nicht für Internet Explorer-Prozesse angezeigt. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, wird die Benachrichtigungsleiste für Internet Explorer-Prozesse angezeigt.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067139)

  **Standardeinstellung:** Aktiviert

- **Internet Explorer: Internetzone: Download signierter ActiveX-Steuerelemente**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob Benutzer signierte ActiveX-Steuerelemente auf einer Seite in der Zone herunterladen können. Wenn Sie diese Richtlinieneinstellung aktivieren, können Benutzer signierte Steuerelemente ohne Benutzereingriff herunterladen. Wenn Sie „Bestätigen“ in der Dropdownliste auswählen, werden Benutzer zur Bestätigung aufgefordert, ob Steuerelemente von nicht vertrauenswürdigen Herausgebern heruntergeladen werden sollen. Von vertrauenswürdigen Herausgebern signierter Code wird im Hintergrund heruntergeladen. Wenn Sie diese Richtlinieneinstellung deaktivieren, können signierte Steuerelemente nicht heruntergeladen werden. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, werden die Benutzer gefragt, ob Steuerelemente von nicht vertrauenswürdigen Herausgebern heruntergeladen werden sollen. Von vertrauenswürdigen Herausgebern signierter Code wird im Hintergrund heruntergeladen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067064)

  **Standardeinstellung:** Deaktivieren

- **Internet Explorer: Eingeschränkte Zone: SmartScreen**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob der SmartScreen-Filter Seiten in dieser Zone auf schädlichen Inhalt überprüft. Wenn Sie diese Richtlinieneinstellung aktivieren, überprüft der SmartScreen-Filter Seiten in dieser Zone auf schädlichen Inhalt. Wenn Sie diese Richtlinieneinstellung deaktivieren, werden Seiten in dieser Zone vom SmartScreen-Filter nicht auf schädlichen Inhalt überprüft. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, kann der Benutzer entscheiden, ob der SmartScreen-Filter Seiten in dieser Zone auf schädlichen Inhalt überprüft. Anmerkung: In Internet Explorer 7 steuert diese Richtlinieneinstellung, ob der Phishingfilter Seiten in dieser Zone auf schädlichen Inhalt überprüft.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067034)

  **Standardeinstellung:** Aktiviert

- **Internet Explorer: Schaltfläche „Einmal ausführen“ für veraltete ActiveX-Steuerelemente entfernen**:  
  Mit dieser Richtlinieneinstellung können Sie verhindern, dass Benutzer die Schaltfläche „Run this time“ (Dieses Mal ausführen) sehen und bestimmte veraltete ActiveX-Steuerelemente in Internet Explorer ausführen. Wenn Sie diese Richtlinieneinstellung aktivieren, können Benutzer die Schaltfläche „Run this time“ (Dieses Mal ausführen) in der Warnmeldung nicht sehen, die angezeigt wird, wenn Internet Explorer ein veraltetes ActiveX-Steuerelement blockiert. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, können Benutzer die Schaltfläche „Run this time“ in der Warnung sehen, die angezeigt wird, wenn Internet Explorer ein veraltetes ActiveX-Steuerelement in Internet Explorer blockiert. Durch Klicken auf diese Schaltfläche kann der Benutzer das veraltete ActiveX-Steuerelement einmal ausführen. Weitere Informationen finden Sie unter „Outdated ActiveX Controls“ (Veraltete ActiveX-Steuerelemente) in der TechNet-Bibliothek in Internet Explorer.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067123)

  **Standardeinstellung:** Aktiviert

- **Internet Explorer: Internetzone: Anwendungen und Dateien in einem IFRAME starten**:  
  Mit dieser Richtlinieneinstellung können Sie steuern, ob aus einem iFrame-Verweis im HTML-Code der Seiten in dieser Zone Anwendungen ausgeführt und Dateien heruntergeladen werden können. Wenn Sie diese Richtlinieneinstellung aktivieren, können Benutzer Anwendungen ausführen und Dateien aus iFrames auf den Seiten in dieser Zone ohne Benutzereingriff herunterladen. Wenn Sie „Bestätigen“ aus dem Dropdownfeld auswählen, werden Benutzer dazu aufgefordert, zu entscheiden, ob Anwendungen ausgeführt und Daten aus iFrames auf den Seiten in dieser Zone heruntergeladen werden. Wenn Sie diese Richtlinieneinstellung deaktivieren, können die Benutzer über iFrames auf den Seiten in dieser Zone weder Anwendungen ausführen noch Dateien herunterladen. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, werden Benutzer dazu aufgefordert, zu entscheiden, ob Anwendungen ausgeführt und Daten aus iFrames auf den Seiten in dieser Zone heruntergeladen werden.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067020)

  **Standardeinstellung:** Deaktivieren

- **Internet Explorer: Eingeschränkte Zone: Domänenübergreifende Navigation zwischen Fenstern und Frames**:  
  Mit dieser Richtlinieneinstellung können Sie Optionen zum Ziehen von Inhalten von einer Domäne in eine andere festlegen, wenn sich Quelle und Ziel in unterschiedlichen Fenstern befinden. Wenn Sie diese Richtlinieneinstellung aktivieren und auf „Aktivieren“ klicken, können die Benutzer Inhalte von einer Domäne in eine andere ziehen, wenn sich Quelle und Ziel in unterschiedlichen Fenstern befinden. Benutzer können diese Einstellung nicht ändern. Wenn Sie diese Richtlinieneinstellung aktiveren und auf „Deaktivieren“ klicken, können die Benutzer keine Inhalte von einer Domäne in eine andere ziehen, wenn sich Quelle und Ziel in unterschiedlichen Fenstern befinden. Benutzer können diese Einstellung nicht ändern. Wenn Sie diese Richtlinieneinstellung in Internet Explorer 10 deaktivieren oder nicht konfigurieren, können die Benutzer keine Inhalte von einer Domäne in eine andere ziehen, wenn sich Quelle und Ziel in unterschiedlichen Fenstern befinden. Die Benutzer können diese Einstellung im Dialogfeld „Internetoptionen“ ändern. Wenn Sie diese Richtlinieneinstellung in Internet Explorer 9 oder einer früheren Version deaktivieren oder nicht konfigurieren, können die Benutzer Inhalte von einer Domäne in eine andere ziehen, wenn sich Quelle und Ziel in unterschiedlichen Fenstern befinden. Benutzer können diese Einstellung nicht ändern.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067050)

  **Standardeinstellung:** Deaktivieren

- **SmartScreen für die Internetzone von Internet Explorer**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob der SmartScreen-Filter Seiten in dieser Zone auf schädlichen Inhalt überprüft. Wenn Sie diese Richtlinieneinstellung aktivieren, überprüft der SmartScreen-Filter Seiten in dieser Zone auf schädlichen Inhalt. Wenn Sie diese Richtlinieneinstellung deaktivieren, werden Seiten in dieser Zone vom SmartScreen-Filter nicht auf schädlichen Inhalt überprüft. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, kann der Benutzer entscheiden, ob der SmartScreen-Filter Seiten in dieser Zone auf schädlichen Inhalt überprüft. Anmerkung: In Internet Explorer 7 steuert diese Richtlinieneinstellung, ob der Phishingfilter Seiten in dieser Zone auf schädlichen Inhalt überprüft.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067047)

  **Standardeinstellung:** Aktiviert

- **Java-Berechtigungen für die gesperrte vertrauenswürdige Zone in Internet Explorer**:  
  Mit dieser Richtlinieneinstellung können Sie Berechtigungen für Java-Applets verwalten. Durch das Aktivieren dieser Richtlinieneinstellung können Sie Optionen aus dem Dropdownfeld auswählen. Wählen Sie „Benutzerdefiniert“ aus, um Berechtigungseinstellungen einzeln zu bestimmen. Wählen Sie „Niedrige Sicherheit“ aus, um Applets die Ausführung aller Vorgänge zu ermöglichen. Wählen Sie „Mittlere Sicherheit“ aus, um Applets die Ausführung in der zugehörigen Sandbox (ein Bereich im Speicher, außerhalb dessen das Programm keine Aufrufe ausführen kann) sowie Funktionen wie den sicheren Speicherbereich (ein geschützter und sicherer Speicherbereich auf dem Clientcomputer) und die benutzergesteuerte Datei-E/A zu ermöglichen. Wählen Sie „Hohe Sicherheit“ aus, um Applets die Ausführung in der zugehörigen Sandbox zu ermöglichen. Deaktivieren Sie Java, um zu verhindern, dass Applets ausgeführt werden. Wenn Sie diese Richtlinieneinstellung deaktivieren, können Java-Applets nicht ausgeführt werden. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, sind Java-Applets deaktiviert.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067142)

  **Standardeinstellung:** Java deaktivieren

- **Signaturen von heruntergeladenen Programmen in Internet Explorer überprüfen**:  
  Mit dieser Richtlinieneinstellung können Sie steuern, ob Internet Explorer auf Computern von Benutzern ausführbare Programme auf digitale Signaturen überprüft (was den Herausgeber von signierter Software identifiziert und verifiziert, dass diese nicht verändert oder manipuliert wurde), bevor diese heruntergeladen werden. Wenn Sie diese Richtlinieneinstellung aktivieren, überprüft Internet Explorer die digitalen Signaturen von ausführbaren Programmen und zeigt ihre Identitäten an, bevor sie auf Computer von Benutzern heruntergeladen werden. Wenn Sie diese Richtlinieneinstellung deaktivieren, überprüft Internet Explorer die digitalen Signaturen von ausführbaren Programmen nicht oder zeigt ihre Identitäten nicht an, bevor sie auf Computer von Benutzern heruntergeladen werden. Wenn Sie diese Richtlinie nicht konfigurieren, überprüft Internet Explorer die digitalen Signaturen von ausführbaren Programmen nicht oder zeigt ihre Identitäten nicht an, bevor sie auf Computer von Benutzern heruntergeladen werden.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067051)

  **Standardeinstellung:** Aktiviert

- **Scripting von WebBrowser-Steuerelementen in der eingeschränkten Zone von Internet Explorer**:  
  Diese Richtlinieneinstellung bestimmt, ob eine Seite eingebettete WebBrowser-Steuerelemente per Skript steuern kann. Wenn Sie diese Richtlinieneinstellung aktivieren, ist der Skriptzugriff auf das WebBrowser-Steuerelement möglich. Wenn Sie diese Richtlinieneinstellung deaktivieren, ist der Skriptzugriff auf das WebBrowser-Steuerelement nicht möglich. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, kann der Benutzer den Skriptzugriff auf das WebBrowser-Steuerelement aktivieren oder deaktivieren. Standardmäßig ist der Skriptzugriff auf das WebBrowser-Steuerelement nur auf dem lokalen Computer und in Intranetzonen möglich.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067098)

  **Standardeinstellung:** Deaktiviert

- **Cross-Site Scripting-Filter in der eingeschränkten Zone von Internet Explorer**:  
  Mit dieser Richtlinie können Sie steuern, ob websiteübergreifende Skripteinschleusungen in Websites in dieser Zone vom XSS-Filter (Cross-Site Scripting) erkannt und verhindert werden. Wenn Sie diese Richtlinieneinstellung aktivieren, ist der XSS-Filter für Websites in dieser Zone aktiviert, um Versuche einer websiteübergreifenden Skripteinschleusung zu blockieren. Wenn Sie diese Richtlinieneinstellung deaktivieren, wird der XSS-Filter für Websites in dieser Zone deaktiviert, und Internet Explorer lässt die websiteübergreifende Skripteinschleusung zu.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067178)

  **Standardeinstellung:** Aktiviert

- **Dynamische Binär- und Skriptverhalten in der eingeschränkten Zone von Internet Explorer**:  
  Diese Richtlinieneinstellung ermöglicht Ihnen, dynamische Binär- und Skriptverhalten zu verwalten: Komponenten, die spezifische Funktionalität für die HTML-Elemente einkapseln, an die sie angefügt wurden. Wenn Sie diese Richtlinieneinstellung aktivieren, stehen Binär- und Skriptverhalten zur Verfügung. Wenn Sie „Vom Administrator genehmigt“ in der Dropdownliste auswählen, sind nur Verhalten verfügbar, die in der Liste „Vom Administrator zugelassenes Verhalten“ der Richtlinie „ Sicherheitseinschränkung für Binärverhalten“ aufgeführt sind. Wenn Sie diese Richtlinieneinstellung deaktivieren, stehen Binär- und Skriptverhalten nicht zur Verfügung, es sei denn, Anwendungen haben einen benutzerdefinierten Sicherheits-Manager implementiert. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, stehen Binär- und Skriptverhalten nicht zur Verfügung, es sei denn, Anwendungen haben einen benutzerdefinierten Sicherheits-Manager implementiert.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067224)

  **Standardeinstellung:** Deaktivieren

- **Überprüfung der Sicherheitseinstellungen von Internet Explorer**:  
  Mit dieser Richtlinieneinstellung wird die Funktion zur Überprüfung der Sicherheitseinstellungen deaktiviert, die die Sicherheitseinstellungen von Internet Explorer überprüft, um zu bestimmen, wann die Einstellungen für Internet Explorer ein potenzielles Risiko darstellen. Wenn Sie diese Richtlinieneinstellung aktivieren, wird die Funktion deaktiviert. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, wird die Funktion aktiviert.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067182)

  **Standardeinstellung:** Aktiviert

- **Sicherheitswarnung für potenziell unsichere Dateien in der Internetzone von Internet Explorer**:  
  Mit dieser Richtlinieneinstellung wird bestimmt, ob die Nachricht „Datei öffnen – Sicherheitswarnung“ angezeigt wird, wenn der Benutzer versucht, ausführbare Dateien oder andere potenziell unsichere Dateien (z.B. aus einer Dateifreigabe im Intranet über den Datei-Explorer) zu öffnen. Wenn Sie diese Richtlinieneinstellung aktivieren und „Aktivieren“ im Dropdownfeld auswählen, werden diese Dateien ohne Sicherheitswarnung geöffnet. Wenn Sie das Dropdownfeld auf „Bestätigen“ einstellen, wird eine Sicherheitswarnung angezeigt, bevor die Dateien geöffnet werden. Wenn Sie diese Richtlinieneinstellung deaktivieren, werden diese Dateien nicht geöffnet. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, kann der Benutzer konfigurieren, wie der Computer diese Dateien behandeln soll. Standardmäßig werden diese Dateien in der eingeschränkten Zone blockiert, in der Intranetzone sowie in Zonen für lokale Computer aktiviert und in Internetzonen und vertrauenswürdigen Zonen auf „Bestätigen“ festgelegt.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067204)

  **Standardeinstellung:** Bestätigen

- **Java-Berechtigungen in der Intranetzone von Internet Explorer**:  
  Mit dieser Richtlinieneinstellung können Sie Berechtigungen für Java-Applets verwalten. Durch das Aktivieren dieser Richtlinieneinstellung können Sie Optionen aus dem Dropdownfeld auswählen. Wählen Sie „Benutzerdefiniert“ aus, um Berechtigungseinstellungen einzeln zu bestimmen. Wählen Sie „Niedrige Sicherheit“ aus, um Applets die Ausführung aller Vorgänge zu ermöglichen. Wählen Sie „Mittlere Sicherheit“ aus, um Applets die Ausführung in der zugehörigen Sandbox (ein Bereich im Speicher, außerhalb dessen das Programm keine Aufrufe ausführen kann) sowie Funktionen wie den sicheren Speicherbereich (ein geschützter und sicherer Speicherbereich auf dem Clientcomputer) und die benutzergesteuerte Datei-E/A zu ermöglichen. Wählen Sie „Hohe Sicherheit“ aus, um Applets die Ausführung in der zugehörigen Sandbox zu ermöglichen. Deaktivieren Sie Java, um zu verhindern, dass Applets ausgeführt werden. Wenn Sie diese Richtlinieneinstellung deaktivieren, können Java-Applets nicht ausgeführt werden. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, wird die Berechtigung auf „Mittlere Sicherheit“ festgelegt.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067206)

  **Standardeinstellung:** Hohe Sicherheit

- **Veraltete ActiveX-Steuerelemente in Internet Explorer blockieren**:  
  Mit dieser Richtlinieneinstellung wird bestimmt, ob Internet Explorer bestimmte veraltete ActiveX-Steuerelemente blockiert. Veraltete ActiveX-Steuerelemente werden in der Intranetzone nie blockiert. Wenn Sie diese Richtlinieneinstellung aktivieren, blockiert Internet Explorer veraltete ActiveX-Steuerelemente nicht mehr. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, blockiert Internet Explorer weiterhin bestimmte veraltete ActiveX-Steuerelemente. Weitere Informationen finden Sie unter „Outdated ActiveX Controls“ (Veraltete ActiveX-Steuerelemente) in der TechNet-Bibliothek in Internet Explorer.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067203)

  **Standardeinstellung:** Aktiviert

- **Popupblocker in der eingeschränkten Zone von Internet Explorer**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob unerwünschte Popupfenster angezeigt werden. Popupfenster, die geöffnet werden, wenn der Endbenutzer auf einen Link klickt, werden nicht blockiert. Wenn Sie diese Richtlinieneinstellung aktivieren, werden die meisten unerwünschten Popupfenster nicht angezeigt. Wenn Sie diese Richtlinieneinstellung deaktivieren, werden Popupfenster angezeigt. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, werden die meisten unerwünschten Popupfenster nicht angezeigt.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067180)

  **Standardeinstellung:** Aktivieren Sie

- **Internet Explorer-Prozesse: Sicherheitseinschränkung für MK-Protokoll**:  
  Die Richtlinieneinstellung „Sicherheitseinschränkung für MK-Protokoll“ verringert die Angriffsfläche durch Blockieren des MK-Protokolls. Bei Ressourcen, die im MK-Prokoll gehostet werden, treten Fehler auf. Wenn Sie diese Richtlinieneinstellung aktivieren, wird das MK-Protokoll für den Datei-Explorer und Internet Explorer blockiert. Bei Ressourcen, die im MK-Protokoll gehostet werden, treten Fehler auf. Wenn Sie diese Richtlinieneinstellung deaktivieren, können Anwendungen die MK-Protokoll-API verwenden. Ressourcen, die im MK-Protokoll gehostet werden, können für den Datei-Explorer und für Internet Explorer-Prozesse verwendet werden. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, wird das MK-Protokoll für den Datei-Explorer und Internet Explorer blockiert. Bei Ressourcen, die im MK-Protokoll gehostet werden, treten Fehler auf.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067179)

  **Standardeinstellung:** Aktiviert

- **Internet Explorer: Vertrauenswürdige Zone: Java-Berechtigungen**:  
  Mit dieser Richtlinieneinstellung können Sie Berechtigungen für Java-Applets verwalten. Durch das Aktivieren dieser Richtlinieneinstellung können Sie Optionen aus dem Dropdownfeld auswählen. Wählen Sie „Benutzerdefiniert“ aus, um Berechtigungseinstellungen einzeln zu bestimmen. Wählen Sie „Niedrige Sicherheit“ aus, um Applets die Ausführung aller Vorgänge zu ermöglichen. Wählen Sie „Mittlere Sicherheit“ aus, um Applets die Ausführung in der zugehörigen Sandbox (ein Bereich im Speicher, außerhalb dessen das Programm keine Aufrufe ausführen kann) sowie Funktionen wie den sicheren Speicherbereich (ein geschützter und sicherer Speicherbereich auf dem Clientcomputer) und die benutzergesteuerte Datei-E/A zu ermöglichen. Wählen Sie „Hohe Sicherheit“ aus, um Applets die Ausführung in der zugehörigen Sandbox zu ermöglichen. Deaktivieren Sie Java, um zu verhindern, dass Applets ausgeführt werden. Wenn Sie diese Richtlinieneinstellung deaktivieren, können Java-Applets nicht ausgeführt werden. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, wird die Berechtigung auf „Niedrige Sicherheit“ festgelegt.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067200)

  **Standardeinstellung:** Hohe Sicherheit

- **Internet Explorer: Eingeschränkte Zone: Skripting von Java-Applets**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob Applets in dieser Zone für Skripts verfügbar gemacht werden. Wenn Sie diese Richtlinie aktivieren, können Skripts automatisch und ohne Benutzereingriff auf Applets zugreifen. Wenn Sie im Dropdownfeld „Bestätigen“ auswählen, werden die Benutzer zur Bestätigung aufgefordert, ob ein Skript auf Applets zugreifen darf. Wenn Sie diese Richtlinieneinstellung deaktivieren, können Skripts nicht auf Applets zugreifen. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, können Skripts nicht auf Applets zugreifen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067202)

  **Standardeinstellung:** Deaktivieren

- **Internet Explorer: Sperrung der eingeschränkten Zone: Java-Berechtigungen**:  
  Mit dieser Richtlinieneinstellung können Sie Berechtigungen für Java-Applets verwalten. Durch das Aktivieren dieser Richtlinieneinstellung können Sie Optionen aus dem Dropdownfeld auswählen. Wählen Sie „Benutzerdefiniert“ aus, um Berechtigungseinstellungen einzeln zu bestimmen. Wählen Sie „Niedrige Sicherheit“ aus, um Applets die Ausführung aller Vorgänge zu ermöglichen. Wählen Sie „Mittlere Sicherheit“ aus, um Applets die Ausführung in der zugehörigen Sandbox (ein Bereich im Speicher, außerhalb dessen das Programm keine Aufrufe ausführen kann) sowie Funktionen wie den sicheren Speicherbereich (ein geschützter und sicherer Speicherbereich auf dem Clientcomputer) und die benutzergesteuerte Datei-E/A zu ermöglichen. Wählen Sie „Hohe Sicherheit“ aus, um Applets die Ausführung in der zugehörigen Sandbox zu ermöglichen. Deaktivieren Sie Java, um zu verhindern, dass Applets ausgeführt werden. Wenn Sie diese Richtlinieneinstellung deaktivieren, können Java-Applets nicht ausgeführt werden. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, sind Java-Applets deaktiviert.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067181)

  **Standardeinstellung:** Java deaktivieren

- **Internet Explorer: Internetzone: Nur genehmigte Domänen können ActiveX-Steuerelemente verwenden**:  
  Mit dieser Richtlinieneinstellung wird bestimmt, ob Benutzer dazu aufgefordert werden, zuzulassen, dass ActiveX-Steuerelemente auf Websites ausgeführt werden, die nicht die Website sind, auf der das ActiveX-Steuerelement installiert wurde. Wenn Sie diese Richtlinieneinstellung aktivieren, werden Benutzer zur Bestätigung aufgefordert, bevor die ActiveX-Steuerelemente von Websites in dieser Zone ausgeführt werden können. Der Benutzer kann die Ausführung des Steuerelements wahlweise für die aktuelle Website oder für alle Websites zulassen. Wenn Sie diese Richtlinieneinstellung deaktivieren, werden die Benutzer nicht pro Website zum Zulassen von ActiveX aufgefordert, und ActiveX-Steuerelemente dürfen für alle Websites in dieser Zone ausgeführt werden.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067091)

  **Standardeinstellung:** Aktiviert

- **Alle Netzwerkpfade in Internet Explorer einbeziehen**:  
  Alle Netzwerkpfade in Internet Explorer einbeziehen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067090)

  **Standardeinstellung:** Deaktiviert

- **Internet Explorer: Internetzone: Geschützter Modus**:  
  Mit dieser Richtlinieneinstellung können Sie den geschützten Modus aktivieren. Im geschützten Modus wird Internet Explorer vor der Ausnutzung von Schwachstellen geschützt. Hierbei wird die Anzahl der Speicherorte in der Registrierung und im Dateisystem verringert, in die Internet Explorer schreiben kann. Wenn Sie diese Richtlinieneinstellung aktivieren, wird der geschützte Modus aktiviert. Benutzer können den geschützten Modus nicht deaktivieren. Wenn Sie diese Richtlinieneinstellung deaktivieren, wird der geschützte Modus deaktiviert. Benutzer können den geschützten Modus nicht aktivieren. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, können Benutzer den geschützten Modus aktivieren oder deaktivieren.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067171)

  **Standardeinstellung:** Aktivieren Sie

- **Internet Explorer: Internetzone: Nicht als sicher markierte ActiveX-Steuerelemente initialisieren und ausführen**:  
  Mit dieser Richtlinieneinstellung können Sie ActiveX-Steuerelemente verwalten, die als unsicher gekennzeichnet sind. Wenn Sie diese Richtlinieneinstellung aktivieren, werden ActiveX-Steuerelemente ausgeführt und mit Parametern geladen, und das Skript wird ohne Festlegen der Objektsicherheit für nicht vertrauenswürdige Daten oder Skripts erstellt. Von dieser Einstellung wird abgeraten, es sei denn, es handelt sich um sichere und verwaltete Zonen. Mit dieser Einstellung werden sowohl unsichere als auch sichere Steuerelemente initialisiert und Skripte für diese erstellt, ohne dabei die Option „ActiveX-Steuerelemente ausführen, die für Skripting sicher sind“ zu beachten. Wenn Sie diese Richtlinieneinstellung aktivieren und die Option „Prompt“ (Bestätigen) im Dropdownfeld auswählen, werden Benutzer dazu aufgefordert, auszuwählen, ob das Steuerelement mit Parametern geladen oder ein Skript erstellt werden soll. Wenn Sie diese Richtlinieneinstellung deaktivieren, werden ActiveX-Steuerelemente, die nicht als sicher gekennzeichnet werden können, nicht geladen, und es wird kein Skript erstellt. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, werden ActiveX-Steuerelemente, die nicht als sicher gekennzeichnet werden können, nicht geladen, und es wird kein Skript erstellt.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067170)

  **Standardeinstellung:** Deaktivieren

- **Internet Explorer: Sperrung der eingeschränkten Zone: SmartScreen**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob der SmartScreen-Filter Seiten in dieser Zone auf schädlichen Inhalt überprüft. Wenn Sie diese Richtlinieneinstellung aktivieren, überprüft der SmartScreen-Filter Seiten in dieser Zone auf schädlichen Inhalt. Wenn Sie diese Richtlinieneinstellung deaktivieren, werden Seiten in dieser Zone vom SmartScreen-Filter nicht auf schädlichen Inhalt überprüft. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, kann der Benutzer entscheiden, ob der SmartScreen-Filter Seiten in dieser Zone auf schädlichen Inhalt überprüft. Anmerkung: In Internet Explorer 7 steuert diese Richtlinieneinstellung, ob der Phishingfilter Seiten in dieser Zone auf schädlichen Inhalt überprüft.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067092)

  **Standardeinstellung:** Aktiviert

- **Internet Explorer: Absturzerkennung**:  
  Mit dieser Richtlinieneinstellung können Sie die Absturzermittlungsfunktion der Add-On-Verwaltung verwalten. Wenn Sie diese Richtlinieneinstellung aktivieren, wird durch einen Absturz von Internet Explorer die Windows-Fehlerberichterstattung eingeleitet. Dieses Verhalten gibt es im Windows XP Professional Service Pack 1 und früher. Alle Richtlinieneinstellung für die Windows-Fehlerberichterstattung bleiben bestehen. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, bleibt die Absturzermittlungsfunktion für die Add-On-Verwaltung aktiviert.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067094)

  **Standardeinstellung:** Deaktiviert

- **Internet Explorer: Internetzone: Java-Berechtigungen**:  
  Mit dieser Richtlinieneinstellung können Sie Berechtigungen für Java-Applets verwalten. Durch das Aktivieren dieser Richtlinieneinstellung können Sie Optionen aus dem Dropdownfeld auswählen. Wählen Sie „Benutzerdefiniert“ aus, um Berechtigungseinstellungen einzeln zu bestimmen. Wählen Sie „Niedrige Sicherheit“ aus, um Applets die Ausführung aller Vorgänge zu ermöglichen. Wählen Sie „Mittlere Sicherheit“ aus, um Applets die Ausführung in der zugehörigen Sandbox (ein Bereich im Speicher, außerhalb dessen das Programm keine Aufrufe ausführen kann) sowie Funktionen wie den sicheren Speicherbereich (ein geschützter und sicherer Speicherbereich auf dem Clientcomputer) und die benutzergesteuerte Datei-E/A zu ermöglichen. Wählen Sie „Hohe Sicherheit“ aus, um Applets die Ausführung in der zugehörigen Sandbox zu ermöglichen. Deaktivieren Sie Java, um zu verhindern, dass Applets ausgeführt werden. Wenn Sie diese Richtlinieneinstellung deaktivieren, können Java-Applets nicht ausgeführt werden. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, wird die Berechtigung auf „Hohe Sicherheit“ festgelegt.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067174)

  **Standardeinstellung:** Java deaktivieren

- **Internet Explorer: Eingeschränkte Zone: Active Scripting**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob Skriptcode auf Seiten in der Zone ausgeführt werden darf. Wenn Sie diese Richtlinieneinstellung aktivieren, wird Skriptcode automatisch auf Seiten in der Zone ausgeführt. Wenn Sie im Dropdownfeld „Bestätigen“ auswählen, werden die Benutzer zur Bestätigung aufgefordert, ob Skriptcode auf Seiten in der Zone ausgeführt werden darf. Wenn Sie diese Richtlinieneinstellung deaktivieren, wird kein Skriptcode auf Seiten in der Zone ausgeführt. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, wird kein Skriptcode auf Seiten in der Zone ausgeführt.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067172)

  **Standardeinstellung:** Deaktivieren

- **Internet Explorer: Internetzone: Anmeldeoptionen**:  
  Mit dieser Richtlinieneinstellung können Sie Einstellungen für Anmeldeoptionen verwalten. Durch das Aktivieren dieser Richtlinieneinstellung können Sie eine der folgenden Anmeldeoptionen auswählen. Die Anmeldung kann anonym durchgeführt werden, um die HTTP-Authentifizierung zu deaktivieren, und das Gastkonto kann nur für das CIFS-Protokoll (Common Internet File System) verwendet werden. Sie können die Eingabe eines Benutzernamens und eines Kennworts anfordern, um die Benutzer-ID und Kennwörter von Benutzern abzufragen. Nachdem ein Benutzer abgefragt wurde, können diese Werte für den Rest der Sitzung im Hintergrund verwendet werden. Sie können die automatische Anmeldung nur in der Intranetzone zulassen, um Benutzer-IDs und Kennwörter von Benutzern in anderen Zonen abzufragen. Nachdem ein Benutzer abgefragt wurde, können diese Werte für den Rest der Sitzung im Hintergrund verwendet werden. Sie können die automatische Anmeldung mit dem aktuellen Benutzernamen und Kennwort durchführen, um die Anmeldung mithilfe der NTLM-Authentifizierung (auch bekannt als Windows NT Challenge Response) durchzuführen. Wenn der Server die NTLM-Authentifizierung unterstützt, werden der Netzwerkbenutzername und das Kennwort für die Anmeldung verwendet. Wenn die NTLM-Authentifizierung vom Server nicht unterstützt wird, wird der Benutzer dazu aufgefordert, seinen Benutzernamen und sein Kennwort einzugeben. Wenn Sie diese Richtlinieneinstellung deaktivieren, wird die automatische Anmeldung nur in der Intranetzone zugelassen. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, wird für die Anmeldung „Automatisches Anmelden nur in der Intranetzone“ festgelegt.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067194)

  **Standardeinstellung:** Bestätigen

- **Internet Explorer: Eingeschränkte Zone: VBScript-Ausführung zulassen**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob das VBScript über die in Internet Explorer festgelegte Zone auf Seiten ausgeführt werden kann. Wenn Sie die Option „Aktivieren“ im Dropdownfeld ausgewählt haben, kann das VBScript ohne Benutzereingriff verwendet werden. Wenn Sie die Option „Bestätigen“ im Dropdownfeld ausgewählt haben, werden Benutzer dazu aufgefordert, auszuwählen, ob das VBScript ausgeführt werden darf. Wenn Sie die Option „Deaktivieren“ im Dropdownfeld ausgewählt haben, wird die Ausführung des VBScript verhindert. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren oder deaktivieren, wird die Ausführung des VBScript verhindert.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067173)

  **Standardeinstellung:** Deaktivieren

- **Internet Explorer: Internetzone: Ziehen von Inhalten aus unterschiedlichen Domänen zwischen Fenstern**:  
  Mit dieser Richtlinieneinstellung können Sie Optionen zum Ziehen von Inhalten von einer Domäne in eine andere festlegen, wenn sich Quelle und Ziel in unterschiedlichen Fenstern befinden. Wenn Sie diese Richtlinieneinstellung aktivieren und auf „Aktivieren“ klicken, können die Benutzer Inhalte von einer Domäne in eine andere ziehen, wenn sich Quelle und Ziel in unterschiedlichen Fenstern befinden. Benutzer können diese Einstellung nicht ändern. Wenn Sie diese Richtlinieneinstellung aktiveren und auf „Deaktivieren“ klicken, können die Benutzer keine Inhalte von einer Domäne in eine andere ziehen, wenn sich Quelle und Ziel in unterschiedlichen Fenstern befinden. Benutzer können diese Einstellung nicht ändern. Wenn Sie diese Richtlinieneinstellung in Internet Explorer 10 deaktivieren oder nicht konfigurieren, können die Benutzer keine Inhalte von einer Domäne in eine andere ziehen, wenn sich Quelle und Ziel in unterschiedlichen Fenstern befinden. Die Benutzer können diese Einstellung im Dialogfeld „Internetoptionen“ ändern. Wenn Sie diese Richtlinieneinstellung in Internet Explorer 9 oder einer früheren Version deaktivieren oder nicht konfigurieren, können die Benutzer Inhalte von einer Domäne in eine andere ziehen, wenn sich Quelle und Ziel in unterschiedlichen Fenstern befinden. Benutzer können diese Einstellung nicht ändern.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067093)

  **Standardeinstellung:** Deaktiviert

- **Internet Explorer: Intranetzone: Nicht als sicher markierte ActiveX-Steuerelemente initialisieren und ausführen**:  
  Mit dieser Richtlinieneinstellung können Sie ActiveX-Steuerelemente verwalten, die als unsicher gekennzeichnet sind. Wenn Sie diese Richtlinieneinstellung aktivieren, werden ActiveX-Steuerelemente ausgeführt und mit Parametern geladen, und das Skript wird ohne Festlegen der Objektsicherheit für nicht vertrauenswürdige Daten oder Skripts erstellt. Von dieser Einstellung wird abgeraten, es sei denn, es handelt sich um sichere und verwaltete Zonen. Mit dieser Einstellung werden sowohl unsichere als auch sichere Steuerelemente initialisiert und Skripte für diese erstellt, ohne dabei die Option „ActiveX-Steuerelemente ausführen, die für Skripting sicher sind“ zu beachten. Wenn Sie diese Richtlinieneinstellung aktivieren und die Option „Prompt“ (Bestätigen) im Dropdownfeld auswählen, werden Benutzer dazu aufgefordert, auszuwählen, ob das Steuerelement mit Parametern geladen oder ein Skript erstellt werden soll. Wenn Sie diese Richtlinieneinstellung deaktivieren, werden ActiveX-Steuerelemente, die nicht als sicher gekennzeichnet werden können, nicht geladen, und es wird kein Skript erstellt. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, werden ActiveX-Steuerelemente, die nicht als sicher gekennzeichnet werden können, nicht geladen, und es wird kein Skript erstellt.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067175)

  **Standardeinstellung:** Deaktivieren

- **Internet Explorer: Anlagen herunterladen**:  
  Mit dieser Richtlinieneinstellung wird verhindert, dass Benutzer Dateianlagen aus einem Feed auf den Computer herunterladen können. Wenn Sie diese Richtlinieneinstellung aktivieren, können Benutzer die Feedsynchronisierungsengine nicht über die Eigenschaftenseite für Feeds zum Herunterladen von Anlagen konfigurieren. Entwickler können die Downloadeinstellung über die Feed-APIs nicht ändern. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, können Benutzer die Feedsynchronisierungsengine über die Eigenschaftenseite für Feeds zum Herunterladen von Anlagen konfigurieren. Außerdem können Entwickler die Downloadeinstellung dann über die Feed-APIs ändern.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067245)

  **Standardeinstellung:** Deaktiviert

- **Internet Explorer: Eingeschränkte Zone: Download nicht signierter ActiveX-Steuerelemente**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob Benutzer nicht signierte ActiveX-Steuerelemente aus der Zone herunterladen können. Insbesondere, wenn Code aus einer nicht vertrauenswürdigen Zone stammt, kann er potenziell schädlich sein. Wenn Sie diese Richtlinieneinstellung aktivieren, können Benutzer nicht signierte Steuerelemente ohne Benutzereingriff ausführen. Wenn Sie die Option „Bestätigen“ im Dropdownfeld auswählen, werden Benutzer dazu aufgefordert, auszuwählen, ob die Ausführung von nicht signierten Steuerelementen zugelassen werden soll. Wenn Sie diese Richtlinieneinstellung deaktivieren, können Benutzer nicht signierte Steuerelemente nicht ausführen. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, können Benutzer nicht signierte Steuerelemente nicht ausführen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067177)

  **Standardeinstellung:** Deaktivieren

- **Internet Explorer: Internetzone: Ziehen von Inhalten aus unterschiedlichen Domänen innerhalb von Fenstern**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob Benutzer nicht signierte ActiveX-Steuerelemente aus der Zone herunterladen können. Insbesondere, wenn Code aus einer nicht vertrauenswürdigen Zone stammt, kann er potenziell schädlich sein. Wenn Sie diese Richtlinieneinstellung aktivieren, können Benutzer nicht signierte Steuerelemente ohne Benutzereingriff ausführen. Wenn Sie die Option „Bestätigen“ im Dropdownfeld auswählen, werden Benutzer dazu aufgefordert, auszuwählen, ob die Ausführung von nicht signierten Steuerelementen zugelassen werden soll. Wenn Sie diese Richtlinieneinstellung deaktivieren, können Benutzer nicht signierte Steuerelemente nicht ausführen. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, können Benutzer nicht signierte Steuerelemente nicht ausführen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067095)

  **Standardeinstellung:** Deaktiviert

- **Internet Explorer-Prozesse: ActiveX-Installation einschränken**:  
  Diese Richtlinieneinstellung ermöglicht es Anwendungen, die das WebBrowser-Steuerelement hosten, die automatische Eingabeaufforderung für die Installation von ActiveX-Steuerelementen zu blockieren. Wenn Sie diese Richtlinieneinstellung aktivieren, blockiert das WebBrowser-Steuerelement die automatische Eingabeaufforderung für die Installation von ActiveX-Steuerelementen für alle Prozesse. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, wird die automatische Eingabeaufforderung für die Installation von ActiveX-Steuerelementen nicht vom Webbrowsersteuerelement für alle Prozesse blockiert.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067250)

  **Standardeinstellung:** Aktiviert

- **Internet Explorer: Internetzone: Scriptlets:**  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob Benutzer Skriptlets ausführen können. Wenn Sie diese Richtlinieneinstellung aktivieren, können Benutzer Skriptlets ausführen. Wenn Sie diese Richtlinieneinstellung deaktivieren, können Benutzer Skriptlets nicht ausführen. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, können Benutzer Skriptlets aktivieren oder deaktivieren.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067176)

  **Standardeinstellung:** Deaktivieren

- **Internet Explorer: Eingeschränkte Zone: Ziehen und Ablegen oder Kopieren und Einfügen von Dateien**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob Benutzer Dateien aus einer Quelle innerhalb der Zone per Drag & Drop verschieben oder kopieren und einfügen können. Wenn Sie diese Richtlinieneinstellung aktivieren, können Benutzer Dateien automatisch aus dieser Zone per Drag & Drop verschieben oder kopieren und einfügen. Wenn Sie die Option „Bestätigen“ im Dropdownfeld auswählen, werden Benutzer dazu aufgefordert, auszuwählen, ob sie Dateien aus dieser Zone ziehen oder kopieren möchten. Wenn Sie diese Richtlinieneinstellung deaktivieren, können Benutzer Dateien aus dieser Zone nicht per Drag & Drop verschieben oder kopieren und einfügen. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, werden Benutzer dazu aufgefordert, auszuwählen, ob sie Dateien aus dieser Zone ziehen oder kopieren möchten.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067096)

  **Standardeinstellung:** Deaktivieren

- **Internet Explorer: Software mit ungültiger Signatur**:  
  Mit dieser Richtlinie können Sie verwalten, ob Software, z.B. ActiveX-Steuerelemente und Dateidownloads, von Benutzern installiert oder ausgeführt werden können, wenn die Signatur ungültig ist. Eine ungültige Signatur kann darauf hindeuten, dass die Datei manipuliert wurde. Wenn Sie diese Richtlinieneinstellung aktivieren, werden Benutzer zum Installieren oder Ausführen von Dateien mit einer ungültigen Signatur aufgefordert. Wenn Sie diese Richtlinieneinstellung deaktivieren, können Benutzer Dateien mit ungültiger Signatur weder ausführen noch installieren. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, können Benutzer entscheiden, ob sie Dateien mit ungültiger Signatur ausführen oder installieren.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067201)

  **Standardeinstellung:** Deaktiviert

- **Internet Explorer: Eingeschränkte Zone: Kopieren und Einfügen über Skript**:  
  Mit dieser Richtlinieneinstellung können Sie festlegen, ob Skripts in einer angegebenen Region Zwischenablagevorgänge (z. B. Ausschneiden, Kopieren und Einfügen) durchführen dürfen. Wenn Sie diese Richtlinieneinstellung aktivieren, können Skripts Zwischenablagevorgänge durchführen. Wenn Sie „Bestätigen“ im Dropdownfeld auswählen, werden die Benutzer zur Bestätigung aufgefordert, ob Zwischenablagevorgänge ausgeführt werden dürfen. Wenn Sie diese Richtlinieneinstellung deaktivieren, können Skripts keine Zwischenablagevorgänge durchführen. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, können Skripts keine Zwischenablagevorgänge durchführen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067165)

  **Standardeinstellung:** Deaktivieren

- **Internet Explorer: Eingeschränkte Zone: Ziehen von Inhalten aus unterschiedlichen Domänen zwischen Fenstern**:  
  Mit dieser Richtlinieneinstellung können Sie Optionen zum Ziehen von Inhalten von einer Domäne in eine andere festlegen, wenn sich Quelle und Ziel in unterschiedlichen Fenstern befinden. Wenn Sie diese Richtlinieneinstellung aktivieren und auf „Aktivieren“ klicken, können die Benutzer Inhalte von einer Domäne in eine andere ziehen, wenn sich Quelle und Ziel in unterschiedlichen Fenstern befinden. Benutzer können diese Einstellung nicht ändern. Wenn Sie diese Richtlinieneinstellung aktiveren und auf „Deaktivieren“ klicken, können die Benutzer keine Inhalte von einer Domäne in eine andere ziehen, wenn sich Quelle und Ziel in unterschiedlichen Fenstern befinden. Benutzer können diese Einstellung nicht ändern. Wenn Sie diese Richtlinieneinstellung in Internet Explorer 10 deaktivieren oder nicht konfigurieren, können die Benutzer keine Inhalte von einer Domäne in eine andere ziehen, wenn sich Quelle und Ziel in unterschiedlichen Fenstern befinden. Die Benutzer können diese Einstellung im Dialogfeld „Internetoptionen“ ändern. Wenn Sie diese Richtlinieneinstellung in Internet Explorer 9 oder einer früheren Version deaktivieren oder nicht konfigurieren, können die Benutzer Inhalte von einer Domäne in eine andere ziehen, wenn sich Quelle und Ziel in unterschiedlichen Fenstern befinden. Benutzer können diese Einstellung nicht ändern.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067166)

  **Standardeinstellung:** Deaktiviert

- **Internet Explorer: Hinzufügen von Websites durch Benutzer**:  
  Durch diese Einstellung wird verhindert, dass Benutzer Sites zu Sicherheitszonen hinzufügen oder aus diesen entfernen. Bei einer Sicherheitszone handelt es sich um Websites, die die gleiche Sicherheitsstufe aufweisen. Wenn Sie diese Richtlinie aktivieren, werden die Verwaltungseinstellungen für Sites für Sicherheitszonen deaktiviert. (Sie können die Verwaltungseinstellungen für Sites für Sicherheitszonen aufrufen, indem Sie im Dialogfeld „Internetoptionen“ auf die Registerkarte „Sicherheit“ und dann auf die Schaltfläche „Sites“ klicken.) Wenn Sie diese Richtlinie deaktivieren oder nicht konfigurieren, können Benutzer Websites hinzufügen oder aus den Zonen für vertrauenswürdige oder eingeschränkte Sites entfernen oder die Einstellungen für das lokale Intranet bearbeiten. Durch diese Richtlinie wird verhindert, dass Benutzer die Verwaltungseinstellungen für Sites für Sicherheitszonen ändern, die vom Administrator eingerichtet wurden. Anmerkung: Die Richtlinie „Sicherheitsseite deaktivieren“ (unter \Benutzerkonfiguration\Administrative Vorlagen\Windows-Komponenten\Internet Explorer\Internetsystemsteuerung) entfernt die Registerkarte „Sicherheit“ aus der Benutzeroberfläche und hat somit Vorrang vor dieser Richtlinie. Ist sie aktiviert, wird diese Richtlinie ignoriert. Weitere Informationen finden Sie im Abschnitt zur Richtlinie „Sicherheitszonen: Nur Computereinstellungen verwenden“.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067167)

  **Standardeinstellung:** Deaktiviert

- **Internet Explorer: Internetzone: Per Skript ausgelöste Fenster**:  
  Mit dieser Richtlinieneinstellung können Sie die Einschränkungen zu durch Skripts geöffneten Popupfenstern und Fenstern mit Titel und Leisten verwalten. Wenn Sie diese Richtlinieneinstellung aktivieren, gilt das Sicherheitsfeature für Fenstereinschränkungen in dieser Zone nicht. Die Sicherheitszone wird also ohne die Sicherheitsebene ausgeführt, die von diesem Feature bereitgestellt wird. Wenn Sie diese Richtlinieneinstellung deaktivieren, können potenziell schädliche Aktionen aus durch Skripts initiierten Popupfenstern und Fenstern mit Titeln und Leisten nicht ausgeführt werden. Dieses Sicherheitsfeature von Internet Explorer wird in der Zone so verwendet, wie es im Sicherheitsfeature für durch Skripts geöffnete Fenster für den Prozess festgelegt ist. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, können potenziell schädliche Aktionen aus durch Skripts initiierten Popupfenstern und Fenstern mit Titeln und Leisten nicht ausgeführt werden. Dieses Sicherheitsfeature von Internet Explorer wird in der Zone so verwendet, wie es im Sicherheitsfeature für durch Skripts geöffnete Fenster für den Prozess festgelegt ist.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067088)

  **Standardeinstellung:** Deaktiviert

- **Internet Explorer – Sicherheitszonen: Nur Computereinstellungen verwenden**:  
  Mit dieser Einstellung werden Informationen zu Sicherheitszonen für alle Benutzer desselben Computers angewendet. Bei einer Sicherheitszone handelt es sich um Websites, die die gleiche Sicherheitsstufe aufweisen. Wenn Sie diese Richtlinie aktivieren, werden die Änderungen, die ein Benutzer an einer Sicherheitszone vornimmt, für alle Benutzer dieses Computers übernommen. Wenn Sie diese Richtlinie deaktivieren oder nicht konfigurieren, können die Benutzer des Computers eigene Einstellungen für Sicherheitszonen einrichten. Verwenden Sie diese Richtlinie, um sicherzustellen, dass die Einstellungen für Sicherheitszonen einheitlich auf einen Benutzer angewendet werden und sich nicht von Benutzer zu Benutzer unterscheiden. Weitere Informationen finden Sie im Abschnitt zur Richtlinie „Sicherheitszonen: Benutzer können keine Einstellungen ändern“.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067086)

  **Standardeinstellung:** Aktiviert

- **Internet Explorer: Sperrung der Zone des lokalen Computers: Java-Berechtigungen**:  
  Mit dieser Richtlinieneinstellung können Sie Berechtigungen für Java-Applets verwalten. Durch das Aktivieren dieser Richtlinieneinstellung können Sie Optionen aus dem Dropdownfeld auswählen. Wählen Sie „Benutzerdefiniert“ aus, um Berechtigungseinstellungen einzeln zu bestimmen. Wählen Sie „Niedrige Sicherheit“ aus, um Applets die Ausführung aller Vorgänge zu ermöglichen. Wählen Sie „Mittlere Sicherheit“ aus, um Applets die Ausführung in der zugehörigen Sandbox (ein Bereich im Speicher, außerhalb dessen das Programm keine Aufrufe ausführen kann) sowie Funktionen wie den sicheren Speicherbereich (ein geschützter und sicherer Speicherbereich auf dem Clientcomputer) und die benutzergesteuerte Datei-E/A zu ermöglichen. Wählen Sie „Hohe Sicherheit“ aus, um Applets die Ausführung in der zugehörigen Sandbox zu ermöglichen. Deaktivieren Sie Java, um zu verhindern, dass Applets ausgeführt werden. Wenn Sie diese Richtlinieneinstellung deaktivieren, können Java-Applets nicht ausgeführt werden. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, sind Java-Applets deaktiviert.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067253)

  **Standardeinstellung:** Java deaktivieren

- **Internet Explorer: Eingeschränkte Zone: Keine Antischadsoftware für ActiveX-Steuerelemente ausführen**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob von Internet Explorer Antischadsoftwareprogramme für ActiveX-Steuerelemente ausgeführt werden, um zu überprüfen, ob sie sicher auf Seiten geladen werden können. Wenn Sie diese Richtlinieneinstellung aktivieren, prüft Internet Explorer nicht anhand des Antischadsoftwareprogramms, ob das Erstellen einer Instanz des ActiveX-Steuerelements sicher ist. Wenn Sie diese Richtlinieneinstellung deaktivieren, prüft Internet Explorer immer anhand des Antischadsoftwareprogramms, ob das Erstellen einer Instanz des ActiveX-Steuerelements sicher ist. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, prüft Internet Explorer immer anhand des Antischadsoftwareprogramms, ob das Erstellen einer Instanz des ActiveX-Steuerelements sicher ist. Benutzer können diese Option über die Sicherheitseinstellungen von Internet Explorer aktivieren und deaktivieren.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067089)

  **Standardeinstellung:** Deaktiviert

- **Internet Explorer: Eingeschränkte Zone: Mit Authenticode signierte Komponenten ausführen, die .NET Framework erfordern**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob .NET Framework-Komponenten, die mit Authenticode signiert wurden, von Internet Explorer ausgeführt werden können. Dazu zählen verwaltete Steuerelemente, auf die über Objekttags verwiesen wird, sowie verwaltete ausführbare Dateien, auf die über einen Link verwiesen wird. Wenn Sie diese Richtlinieneinstellung aktivieren, führt Internet Explorer signierte verwaltete Komponenten aus. Wenn Sie im Dropdownfeld „Bestätigen“ auswählen, fordert Internet Explorer den Benutzer dazu auf, zu entscheiden, ob signierte verwaltete Komponenten ausgeführt werden sollen. Wenn Sie diese Richtlinieneinstellung deaktivieren, führt Internet Explorer signierte verwaltete Komponenten nicht aus. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, führt Internet Explorer signierte verwaltete Komponenten nicht aus.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067169)

  **Standardeinstellung:** Deaktivieren

- **Internet Explorer: Eingeschränkte Zone: Zugriff auf Datenquellen**:  
  Durch diese Richtlinieneinstellung können Sie festlegen, ob Internet Explorer mithilfe von Microsoft XML Parser (MSXML) oder ActiveX Data Objects (ADO) auf Daten aus anderen Sicherheitszonen zugreifen kann. Wenn Sie diese Richtlinieneinstellung aktivieren, können Benutzer eine Seite in die Zone laden, die MSXML oder ADO verwendet, um auf Daten in einer anderen Site in der Zone zuzugreifen. Wenn Sie im Dropdownfeld „Prompt“ (Bestätigen) auswählen, werden Benutzer dazu aufgefordert, zu entscheiden, ob eine Seite in der Zone geladen werden soll, die MSXML oder ADO verwendet, um auf Daten in einer anderen Site in der Zone zuzugreifen. Wenn Sie diese Richtlinieneinstellung deaktivieren, können Benutzer keine Seite in die Zone laden, die MSXML oder ADO verwendet, um auf Daten in einer anderen Site in der Zone zuzugreifen. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, können Benutzer keine Seite in die Zone laden, die MSXML oder ADO verwendet, um auf Daten in einer anderen Site in der Zone zuzugreifen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067161)

  **Standardeinstellung:** Deaktivieren

- **Internet Explorer: Internetzone: Keine Antischadsoftware für ActiveX-Steuerelemente ausführen**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob von Internet Explorer Antischadsoftwareprogramme für ActiveX-Steuerelemente ausgeführt werden, um zu überprüfen, ob sie sicher auf Seiten geladen werden können. Wenn Sie diese Richtlinieneinstellung aktivieren, prüft Internet Explorer nicht anhand des Antischadsoftwareprogramms, ob das Erstellen einer Instanz des ActiveX-Steuerelements sicher ist. Wenn Sie diese Richtlinieneinstellung deaktivieren, prüft Internet Explorer immer anhand des Antischadsoftwareprogramms, ob das Erstellen einer Instanz des ActiveX-Steuerelements sicher ist. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, prüft Internet Explorer immer anhand des Antischadsoftwareprogramms, ob das Erstellen einer Instanz des ActiveX-Steuerelements sicher ist. Benutzer können diese Option über die Sicherheitseinstellungen von Internet Explorer aktivieren und deaktivieren.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067162)

  **Standardeinstellung:** Deaktiviert

- **Internet Explorer: Internetzone: Kopieren und Einfügen über Skript**:  
  Mit dieser Richtlinieneinstellung können Sie festlegen, ob Skripts in einer angegebenen Region Zwischenablagevorgänge (z. B. Ausschneiden, Kopieren und Einfügen) durchführen dürfen. Wenn Sie diese Richtlinieneinstellung aktivieren, können Skripts Zwischenablagevorgänge durchführen. Wenn Sie „Bestätigen“ im Dropdownfeld auswählen, werden die Benutzer zur Bestätigung aufgefordert, ob Zwischenablagevorgänge ausgeführt werden dürfen. Wenn Sie diese Richtlinieneinstellung deaktivieren, können Skripts keine Zwischenablagevorgänge durchführen. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, können Skripts keine Zwischenablagevorgänge durchführen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067084)

  **Standardeinstellung:** Deaktivieren

- **Internet Explorer: ActiveX-Installationsdienst verwenden**:  
  Mit dieser Richtlinieneinstellung können Sie festlegen, wie ActiveX-Steuerelemente installiert werden. Wenn Sie diese Richtlinieneinstellung aktivieren, werden ActiveX-Steuerelemente nur installiert, wenn der ActiveX-Installationsdienst vorhanden ist und dafür konfiguriert wurde, die Installation von ActiveX-Steuerelementen zuzulassen. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, werden ActiveX-Steuerelemente (einschließlich Benutzersteuerelemente) über den Standardinstallationsvorgang installiert.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067163)

  **Standardeinstellung:** Aktiviert

- **Internet Explorer-Prozesse: Schutz vor Zonenanhebung**:  
  Internet Explorer wendet auf jede Website, die geöffnet wird, Einschränkungen an. Diese hängen vom Speicherort der Webseite ab (z.B. Internet, Intranet, lokaler Computer). Für Webseiten, die sich auf lokalen Computern befinden, gelten beispielsweise die niedrigsten Sicherheitseinschränkungen. Sie befinden sich in der Zone „Lokaler Computer“, sodass diese in der Regel das Primärziel von Angreifern darstellt. Wenn Sie diese Richtlinieneinstellung aktivieren, kann jede Zone gegen die Erhöhung der Rechte durch alle Prozesse geschützt werden. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, ist kein Schutz vor Prozessen vorhanden, die nicht Internet Explorer oder die in der Prozessliste aufgeführten Prozesse darstellen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067160)

  **Standardeinstellung:** Aktiviert

- **Internet Explorer: Internetzone: Download nicht signierter ActiveX-Steuerelemente**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob Benutzer nicht signierte ActiveX-Steuerelemente aus der Zone herunterladen können. Insbesondere, wenn Code aus einer nicht vertrauenswürdigen Zone stammt, kann er potenziell schädlich sein. Wenn Sie diese Richtlinieneinstellung aktivieren, können Benutzer nicht signierte Steuerelemente ohne Benutzereingriff ausführen. Wenn Sie die Option „Bestätigen“ im Dropdownfeld auswählen, werden Benutzer dazu aufgefordert, auszuwählen, ob die Ausführung von nicht signierten Steuerelementen zugelassen werden soll. Wenn Sie diese Richtlinieneinstellung deaktivieren, können Benutzer nicht signierte Steuerelemente nicht ausführen. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, können Benutzer nicht signierte Steuerelemente nicht ausführen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067325)

  **Standardeinstellung:** Deaktivieren

- **Internet Explorer: Internetzone: Domänenübergreifende Navigation zwischen Fenstern und Frames**:  
  Mit dieser Richtlinieneinstellung können Sie festlegen, wie Fenster und Frames geöffnet werden, und den Zugriff auf Anwendungen über verschiedene Domänen regeln. Wenn Sie diese Richtlinieneinstellung aktivieren, können Benutzer Fenster und Frames von anderen Domänen öffnen und auf Anwendungen von anderen Domänen zugreifen. Wenn Sie im Dropdownfeld „Bestätigen“ auswählen, werden Benutzer dazu aufgefordert, zu entscheiden, ob Fenster und Frames auf Anwendungen von anderen Domänen zugreifen dürfen. Wenn Sie diese Richtlinieneinstellung deaktivieren, können Benutzer keine Fenster und Frames für den Zugriff auf Anwendungen von anderen Domänen öffnen. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, können Benutzer Fenster und Frames von anderen Domänen öffnen und auf Anwendungen von anderen Domänen zugreifen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067083)

  **Standardeinstellung:** Deaktivieren

- **Internet Explorer: Internetzone: Aktualisierungen der Statusleiste per Skript**:  
  Über diese Richtlinieneinstellung können Sie festlegen, ob die Statusleiste in der Zone durch Skripts aktualisiert werden darf. Wenn Sie diese Richtlinieneinstellung aktivieren, kann die Statusleiste durch Skripts aktualisiert werden. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, kann die Statusleiste nicht über Skripts aktualisiert werden.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067087)

  **Standardeinstellung:** Deaktiviert

- **Internet Explorer: Eingeschränkte Zone: Lokalen Pfad beim Hochladen von Dateien auf den Server einbeziehen**:  
  Mit dieser Richtlinieneinstellung können Sie festlegen, ob Informationen zu lokalen Pfaden beim Hochladen einer Datei über ein HTML-Formular übermittelt werden. Wenn die Informationen zu lokalen Pfaden übermittelt werden, kann es vorkommen, dass einige davon versehentlich für den Server offengelegt werden. Dabei kann es sich beispielsweise um Dateien vom Desktop des Benutzers handeln, die den Benutzernamen im Pfad enthalten. Wenn Sie diese Richtlinieneinstellung aktivieren, werden die Pfadinformationen beim Hochladen einer Datei über ein HTML-Formular übermittelt. Wenn Sie diese Richtlinieneinstellung deaktivieren, werden die Pfadinformationen beim Hochladen einer Datei über ein HTML-Formular entfernt. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, kann der Benutzer entscheiden, ob Pfadinformationen beim Hochladen einer Datei über ein HTML-Formular übermittelt werden sollen. Die Pfadinformationen werden standardmäßig gesendet.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067085)

  **Standardeinstellung:** Deaktiviert

- **Internet Explorer-Prozesse: Dateidownload einschränken**:  
  Diese Richtlinieneinstellung ermöglicht es Anwendungen, die das WebBrowser-Steuerelement hosten, die automatische Eingabeaufforderung für nicht vom Benutzer initiierte Dateidownloads zu blockieren. Wenn Sie diese Richtlinieneinstellung aktivieren, blockiert das WebBrowser-Steuerelement die automatische Eingabeaufforderung für nicht vom Benutzer initiierte Dateidownloads für alle Prozesse. Wenn Sie diese Richtlinieneinstellung deaktivieren, blockiert das WebBrowser-Steuerelement die automatische Eingabeaufforderung für nicht vom Benutzer initiierte Dateidownloads für alle Prozesse nicht.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067164)

  **Standardeinstellung:** Aktiviert

- **Internet Explorer: Eingeschränkte Zone: Nur genehmigte Domänen können ActiveX-Steuerelemente verwenden**:  
  Mit dieser Richtlinieneinstellung wird bestimmt, ob Benutzer dazu aufgefordert werden, zuzulassen, dass ActiveX-Steuerelemente auf Websites ausgeführt werden, die nicht die Website sind, auf der das ActiveX-Steuerelement installiert wurde. Wenn Sie diese Richtlinieneinstellung aktivieren, werden Benutzer zur Bestätigung aufgefordert, bevor die ActiveX-Steuerelemente von Websites in dieser Zone ausgeführt werden können. Der Benutzer kann die Ausführung des Steuerelements wahlweise für die aktuelle Website oder für alle Websites zulassen. Wenn Sie diese Richtlinieneinstellung deaktivieren, werden die Benutzer nicht pro Website zum Zulassen von ActiveX aufgefordert, und ActiveX-Steuerelemente dürfen für alle Websites in dieser Zone ausgeführt werden.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067233)

  **Standardeinstellung:** Aktiviert

- **Internet Explorer: Eingeschränkte Zone: Nicht als sicher markierte ActiveX-Steuerelemente initialisieren und ausführen**:  
  Mit dieser Richtlinieneinstellung können Sie ActiveX-Steuerelemente verwalten, die als unsicher gekennzeichnet sind. Wenn Sie diese Richtlinieneinstellung aktivieren, werden ActiveX-Steuerelemente ausgeführt und mit Parametern geladen, und das Skript wird ohne Festlegen der Objektsicherheit für nicht vertrauenswürdige Daten oder Skripts erstellt. Von dieser Einstellung wird abgeraten, es sei denn, es handelt sich um sichere und verwaltete Zonen. Mit dieser Einstellung werden sowohl unsichere als auch sichere Steuerelemente initialisiert und Skripte für diese erstellt, ohne dabei die Option „ActiveX-Steuerelemente ausführen, die für Skripting sicher sind“ zu beachten. Wenn Sie diese Richtlinieneinstellung aktivieren und die Option „Prompt“ (Bestätigen) im Dropdownfeld auswählen, werden Benutzer dazu aufgefordert, auszuwählen, ob das Steuerelement mit Parametern geladen oder ein Skript erstellt werden soll. Wenn Sie diese Richtlinieneinstellung deaktivieren, werden ActiveX-Steuerelemente, die nicht als sicher gekennzeichnet werden können, nicht geladen, und es wird kein Skript erstellt. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, werden ActiveX-Steuerelemente, die nicht als sicher gekennzeichnet werden können, nicht geladen, und es wird kein Skript erstellt.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067097)

  **Standardeinstellung:** Deaktivieren

- **Internet Explorer: Änderung von Richtlinien durch Benutzer**:  
  Durch diese Einstellung wird verhindert, dass Benutzer die Einstellungen für Sicherheitszonen ändern können. Bei einer Sicherheitszone handelt es sich um Websites, die die gleiche Sicherheitsstufe aufweisen. Wenn Sie diese Richtlinie aktivieren, werden die Schaltfläche „Custom Level“ (Stufe anpassen) und der Schieberegler „Sicherheitsstufe“ auf der Registerkarte „Sicherheit“ im Dialogfeld „Internetoptionen“ deaktiviert. Wenn Sie diese Richtlinie deaktivieren oder nicht konfigurieren, können Benutzer die Einstellungen für Sicherheitszonen bearbeiten. Durch diese Richtlinie wird verhindert, dass Benutzer die Einstellungen für Sicherheitszonen ändern, die vom Administrator eingerichtet wurden. Anmerkung: Die Richtlinie „Sicherheitsseite deaktivieren“ (unter \Benutzerkonfiguration\Administrative Vorlagen\Windows-Komponenten\Internet Explorer\Internetsystemsteuerung) entfernt die Registerkarte „Sicherheit“ aus Internet Explorer in der Systemsteuerung und hat somit Vorrang vor dieser Richtlinie. Ist sie aktiviert, wird diese Richtlinie ignoriert. Weitere Informationen finden Sie im Abschnitt zur Richtlinie „Sicherheitszonen: Nur Computereinstellungen verwenden“.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067155)

  **Standardeinstellung:** Deaktiviert

- **Internet Explorer: Eingeschränkte Zone: Geschützter Modus**:  
  Mit dieser Richtlinieneinstellung können Sie den geschützten Modus aktivieren. Im geschützten Modus wird Internet Explorer vor der Ausnutzung von Schwachstellen geschützt. Hierbei wird die Anzahl der Speicherorte in der Registrierung und im Dateisystem verringert, in die Internet Explorer schreiben kann. Wenn Sie diese Richtlinieneinstellung aktivieren, wird der geschützte Modus aktiviert. Benutzer können den geschützten Modus nicht deaktivieren. Wenn Sie diese Richtlinieneinstellung deaktivieren, wird der geschützte Modus deaktiviert. Benutzer können den geschützten Modus nicht aktivieren. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, können Benutzer den geschützten Modus aktivieren oder deaktivieren.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067080)

  **Standardeinstellung:** Aktivieren Sie

- **Internet Explorer: Internetzone: Dauerhaftigkeit der Benutzerdaten**:  
  Über diese Richtlinieneinstellung können Sie die Speicherung von Informationen im Verlauf, in den Favoriten und im XML-Speicher des Browsers bzw. in einer auf einem Datenträger gespeicherten Webseite regeln. Wenn ein Benutzer eine gespeicherte Seite erneut besucht, kann der Zustand der Seite wiederhergestellt werden, wenn Sie diese Richtlinieneinstellung entsprechend konfiguriert haben. Wenn Sie diese Richtlinieneinstellung aktivieren, können Benutzer die Speicherung von Informationen im Verlauf, in den Favoriten und im XML-Speicher des Browsers bzw. in einer auf einem Datenträger gespeicherten Webseite aktivieren. Wenn Sie diese Richtlinieneinstellung deaktivieren, können Benutzer die Speicherung von Informationen im Verlauf, in den Favoriten und im XML-Speicher des Browsers bzw. in einer auf einem Datenträger gespeicherten Webseite nicht aktivieren. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, können Benutzer die Speicherung von Informationen im Verlauf, in den Favoriten und im XML-Speicher des Browsers bzw. in einer auf einem Datenträger gespeicherten Webseite aktivieren.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067156)

  **Standardeinstellung:** Deaktiviert

- **Internet Explorer: Internetzone: Skripting von Webbrowser-Steuerelementen**:  
  Diese Richtlinieneinstellung bestimmt, ob eine Seite eingebettete WebBrowser-Steuerelemente per Skript steuern kann. Wenn Sie diese Richtlinieneinstellung aktivieren, ist der Skriptzugriff auf das WebBrowser-Steuerelement möglich. Wenn Sie diese Richtlinieneinstellung deaktivieren, ist der Skriptzugriff auf das WebBrowser-Steuerelement nicht möglich. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, kann der Benutzer den Skriptzugriff auf das WebBrowser-Steuerelement aktivieren oder deaktivieren. Standardmäßig ist der Skriptzugriff auf das WebBrowser-Steuerelement nur auf dem lokalen Computer und in Intranetzonen möglich.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067157)

  **Standardeinstellung:** Deaktiviert

- **Internet Explorer: Eingeschränkte Zone: Dauerhaftigkeit der Benutzerdaten**:  
  Über diese Richtlinieneinstellung können Sie die Speicherung von Informationen im Verlauf, in den Favoriten und im XML-Speicher des Browsers bzw. in einer auf einem Datenträger gespeicherten Webseite regeln. Wenn ein Benutzer eine gespeicherte Seite erneut besucht, kann der Zustand der Seite wiederhergestellt werden, wenn Sie diese Richtlinieneinstellung entsprechend konfiguriert haben. Wenn Sie diese Richtlinieneinstellung aktivieren, können Benutzer die Speicherung von Informationen im Verlauf, in den Favoriten und im XML-Speicher des Browsers bzw. in einer auf einem Datenträger gespeicherten Webseite aktivieren. Wenn Sie diese Richtlinieneinstellung deaktivieren, können Benutzer die Speicherung von Informationen im Verlauf, in den Favoriten und im XML-Speicher des Browsers bzw. in einer auf einem Datenträger gespeicherten Webseite nicht aktivieren. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, können Benutzer die Speicherung von Informationen im Verlauf, in den Favoriten und im XML-Speicher des Browsers bzw. in einer auf einem Datenträger gespeicherten Webseite nicht aktivieren.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067081)

  **Standardeinstellung:** Deaktiviert

- **Internet Explorer: Sperrung der Intranetzone: Java-Berechtigungen**:  
  Mit dieser Richtlinieneinstellung können Sie Berechtigungen für Java-Applets verwalten. Durch das Aktivieren dieser Richtlinieneinstellung können Sie Optionen aus dem Dropdownfeld auswählen. Wählen Sie „Benutzerdefiniert“ aus, um Berechtigungseinstellungen einzeln zu bestimmen. Wählen Sie „Niedrige Sicherheit“ aus, um Applets die Ausführung aller Vorgänge zu ermöglichen. Wählen Sie „Mittlere Sicherheit“ aus, um Applets die Ausführung in der zugehörigen Sandbox (ein Bereich im Speicher, außerhalb dessen das Programm keine Aufrufe ausführen kann) sowie Funktionen wie den sicheren Speicherbereich (ein geschützter und sicherer Speicherbereich auf dem Clientcomputer) und die benutzergesteuerte Datei-E/A zu ermöglichen. Wählen Sie „Hohe Sicherheit“ aus, um Applets die Ausführung in der zugehörigen Sandbox zu ermöglichen. Deaktivieren Sie Java, um zu verhindern, dass Applets ausgeführt werden. Wenn Sie diese Richtlinieneinstellung deaktivieren, können Java-Applets nicht ausgeführt werden. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, sind Java-Applets deaktiviert.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067082)

  **Standardeinstellung:** Java deaktivieren

- **Internet Explorer: Erweiterter geschützter Modus**:  
  Der erweiterte geschützte Modus bietet durch die Verwendung von 64-Bit-Prozessen auf 64-Bit-Versionen von Windows zusätzlichen Schutz gegen schädliche Websites. Bei Computern mit Windows 8 oder höher beschränkt der erweiterte geschützte Modus außerdem die Speicherorte von Internet Explorer in der Registrierung und im Dateisystem. Wenn Sie diese Richtlinieneinstellung aktivieren, wird der erweiterte geschützte Modus aktiviert. Jede Zone, für die der geschützte Modus aktiviert ist, verwendet den erweiterten geschützten Modus. Benutzer können den erweiterten geschützten Modus nicht deaktivieren. Wenn Sie diese Richtlinieneinstellung deaktivieren, wird der erweiterte geschützte Modus deaktiviert. Jede Zone, für die der geschützte Modus aktiviert ist, verwendet die Version des geschützten Modus, die im Internet Explorer 7 für Windows Vista eingeführt wurde. Wenn Sie diese Richtlinie nicht konfigurieren, können die Benutzer den erweiterten geschützten Modus über die Registerkarte „Erweitert“ im Dialogfeld „Internetoptionen“ ein oder ausschalten.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067158)

  **Standardeinstellung:** Aktiviert

- **Internet Explorer: SmartScreen-Warnungen umgehen**:  
  Mit dieser Richtlinieneinstellung wird bestimmt, ob Benutzer Warnungen des SmartScreen-Filters umgehen können. Der SmartScreen-Filter warnt Benutzer vor ausführbaren Dateien im Internet, die selten von Benutzern heruntergeladen werden. Wenn Sie diese Richtlinieneinstellung aktivieren, hindern die Warnungen des SmartScreen-Filters Benutzer am Herunterladen. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, können Benutzer die Warnungen des SmartScreen-Filters umgehen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067159)

  **Standardeinstellung:** Deaktiviert

- **Internet Explorer: Eingeschränkte Zone: Meta Refresh**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob Benutzerbrowser auf eine andere Webseite umgeleitet werden können, wenn der Autor der Webseite die Einstellung „Meta Refresh“ (Tag) verwendet, um Browser auf eine andere Webseite umzuleiten. Wenn Sie diese Richtlinieneinstellung aktivieren, können Browser, die eine Seite mit einer aktiven Meta Refresh-Einstellung laden, auf andere Webseiten umgeleitet werden. Wenn Sie diese Richtlinieneinstellung deaktivieren, können Browser, die eine Seite mit einer aktiven Meta Refresh-Einstellung laden, nicht auf andere Webseiten umgeleitet werden. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, können Browser, die eine Seite mit einer aktiven Meta Refresh-Einstellung laden, nicht auf andere Webseiten umgeleitet werden.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067154)

  **Standardeinstellung:** Deaktiviert

## <a name="local-policies-security-options"></a>Sicherheitsoptionen für lokale Richtlinien

Weitere Informationen finden Sie unter [Policy CSP – LocalPoliciesSecurityOptions (Richtlinien-Konfigurationsdienstanbieter: LocalPoliciesSecurityOptions)](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions) in der Windows-Dokumentation.

- **Anonymen Zugriff auf Named Pipes und Freigaben einschränken**:  
  Wenn diese Sicherheitseinstellung aktiviert ist, wird der anonyme Zugriff auf Freigaben und Pipes für folgende Einstellungen eingeschränkt: Named Pipes und Freigaben, auf die anonym zugegriffen werden kann.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067212)

  **Standardeinstellung:** Ja

- **Minimale Sitzungssicherheit für NTLM-SSP-basierte Server**:  
  Mit dieser Sicherheitseinstellung kann die Aushandlung der 128-Bit-Verschlüsselung und der NTLMv2-Sitzungssicherheit für einen Server als erforderlich festgelegt werden. Diese Werte hängen vom Wert des Sicherheitseinstellungswerts für die LAN Manager-Authentifizierungsebene ab. Folgende Optionen sind verfügbar: NTLMv2-Sitzungssicherheit erfordern: Die Verbindung schlägt fehl, wenn die Nachrichtenintegrität nicht ausgehandelt wird. 128-Bit-Verschlüsselung erfordern: Die Verbindung schlägt fehl, wenn die keine starke Verschlüsselung (128-Bit) ausgehandelt wird.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067246)

  **Standardeinstellung:** NTLMv2- und 128-Bit-Verschlüsselung erfordern:

- **Inaktivität in Minuten für Anmeldebildschirm bis zur Aktivierung des Bildschirmschoners:**  
  Windows stellt die Inaktivität einer Anmeldesitzung fest. Wenn die Inaktivitätsdauer ihr Limit überschreitet, wird der Bildschirmschoner aktiviert, und die Sitzung wird gesperrt.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067210)

  **Standardeinstellung:** 15

- **Client muss Kommunikation immer digital signieren:**  
  Diese Sicherheitseinstellung bestimmt, ob von Domänenmitgliedern gestarteter Datenverkehr über den sicheren Kanal signiert oder verschlüsselt sein muss. Wenn ein Computer einer Domäne beitritt, wird ein Computerkonto erstellt. Daraufhin wird das Kennwort des Computerkontos beim Starten des Systems zum Erstellen eines sicheren Kanals mit einem Domänencontroller als Domäne verwendet. Dieser sichere Kanal wird verwendet, um Vorgänge wie die NTLM-Pass-Through-Authentifizierung, LSA SID/Namenlookups usw. durchzuführen. Diese Einstellung bestimmt, ob jeglicher Datenverkehr über den sicheren Kanal, der von Domänenmitgliedern gestartet wird, den Mindestanforderungen für die Sicherheit entspricht. Insbesondere bestimmt sie, ob von Domänenmitgliedern gestarteter Datenverkehr über den sicheren Kanal signiert oder verschlüsselt sein muss. Wenn diese Richtlinie aktiviert ist, wird der sichere Kanal nicht erstellt, es sei denn, die Signierung oder Verschlüsselung des gesamten Datenverkehrs über den sicheren Kanal wird ausgehandelt. Wenn diese Richtlinie deaktiviert ist, wird die Verschlüsselung und Signierung des Datenverkehrs über den sicheren Kanal mit dem Domänencontroller ausgehandelt. In diesem Fall hängen die Signierung und die Verschlüsselung von der Version des Domänencontrollers und den Einstellungen der zwei folgenden Richtlinien ab: Domänenmitglied: Daten des sicheren Kanals digital verschlüsseln (wenn möglich). Domänenmitglied: Daten des sicheren Kanals digital signieren (wenn möglich).  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067187)

  **Standardeinstellung:** Ja

- **Authentifizierungsebene**:  
  Mit dieser Sicherheitseinstellung wird festgelegt, welches Abfrage/Antwort-Authentifizierungsprotokoll für Netzwerkanmeldungen verwendet wird. Diese Auswahl wirkt sich wie folgt auf das von Clients verwendete Authentifizierungsprotokoll, die ausgehandelte Sitzungssicherheit und die von Servern akzeptierte Authentifizierung aus:

  - *LM- und NTLM-Antworten senden*: Clients verwenden die NTLM-Authentifizierung und nie die NTLMv2-Sitzungssicherheit. Domänencontroller akzeptieren die LM-, NTLM- und NTLMv2-Authentifizierungen.

  - *LM und NTLM senden – NTLMv2 bei Aushandlung:* Clients verwenden die LM- und die NTLM-Authentifizierung sowie die NTLMv2-Sitzungssicherheit, wenn der Server diese unterstützt. Domänencontroller akzeptieren die LM-, die NTLM- und die NTLMv2-Authentifizierung.

  - *Nur NTLM-Antworten senden*: Clients verwenden ausschließlich die NTLM-Authentifizierung sowie die NTLMv2-Sitzungssicherheit, wenn der Server diese unterstützt. Domänencontroller akzeptieren die LM-, NTLM- und NTLMv2-Authentifizierungen.

  - *Nur NTLMv2-Antworten senden*: Clients verwenden ausschließlich die NTLMv2-Authentifizierung sowie die NTLMv2-Sitzungssicherheit, wenn der Server diese unterstützt. Domänencontroller akzeptieren die LM-, NTLM- und NTLMv2-Authentifizierungen.

  - *Nur NTLMv2-Antworten senden. LM verweigern:* Clients verwenden ausschließlich die NTLMv2-Authentifizierung sowie die NTLMv2-Sitzungssicherheit, wenn der Server diese unterstützt. Domänencontroller lehnen die LM-Authentifizierung ab und akzeptieren nur die NTLM- und die NTLMv2-Authentifizierung.

  - *Nur NTLMv2-Antworten senden. LM und NTLM verweigern:* Clients verwenden ausschließlich die NTLMv2-Authentifizierung sowie die NTLMv2-Sitzungssicherheit, wenn der Server diese unterstützt. Domänencontroller lehnen die LM- und die NTLM-Authentifizierung ab und akzeptieren nur die NTLMv2-Authentifizierung.

  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067189)

  **Standardeinstellung:** Nur NTLMv2-Antworten senden. LM und NTLM ablehnen.

- **Clients können keine unverschlüsselten Kennwörter an SMB-Server von Drittanbietern senden**:  
  Wenn diese Sicherheitseinstellung aktiviert ist, darf der SMB-Redirector (Server Message Block) Klartextkennwörter an Nicht-Microsoft-SMB-Server senden, die keine Kennwortverschlüsselung während der Authentifizierung unterstützen. Das Senden unverschlüsselter Kennwörter ist ein Sicherheitsrisiko.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067235)

  **Standardeinstellung:** Ja

- **Server muss Kommunikation immer digital signieren**:  
  Mit dieser Sicherheitseinstellung wird festgelegt, ob der SMB-Client versucht, die SMB-Paketsignierung auszuhandeln. Das SMB-Protokoll (Server Message Block) stellt die Grundlage für Microsoft-Dateien und die Druckfreigabe sowie viele andere Netzwerkvorgänge, z.B. die Windows-Remoteverwaltung. Das SMB-Protokoll unterstützt das digitale Signieren von SMB-Paketen, um Man-in-the-Middle-Angriffe zu vermeiden, die SMB-Pakete während der Übermittlung ändern. Mit dieser Richtlinieneinstellung wird festgelegt, ob die SMB-Clientkomponente versucht, die Signierung von SMB-Paketen auszuhandeln, wenn eine Verbindung mit einem SMB-Server hergestellt wird. Wenn diese Einstellung aktiviert wird, fordert der Microsoft-Netzwerkclient den Server dazu auf, die SMB-Paketsignatur bei der Einrichtung der Sitzung durchzuführen. Wenn die Paketsignatur auf dem Server aktiviert wurde, wird die Paketsignatur ausgehandelt. Wenn diese Richtlinie deaktiviert ist, handelt der SMB-Client nie die SMB-Paketsignatur aus.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067319)

  **Standardeinstellung:** Ja

- **Verhalten der Eingabeaufforderung für erhöhte Rechte für Administratoren**:  
  Mit dieser Richtlinieneinstellung können Sie das Verhalten der Eingabeaufforderung für erhöhte Rechte für Administratoren bestimmen. Folgende Optionen sind verfügbar:

  - *Rechte ohne Eingabeaufforderung erhöhen*: Ermöglicht mit Rechten versehenen Konten das Ausführen eines Vorgangs, für den erhöhte Rechte erforderlich sind, ohne dass dafür Zustimmung oder Anmeldeinformationen erforderlich sind. Anmerkung: Verwenden Sie diese Option nur in Umgebungen, die besonders starken Beschränkungen unterliegen.

  - *Eingabeaufforderung zu Anmeldeinformationen auf dem sicheren Desktop*: Wenn für einen Vorgang erhöhte Rechte erforderlich sind, wird der Benutzer auf dem sicheren Desktop zur Eingabe eines entsprechenden Benutzernamens und Kennworts aufgefordert. Wenn der Benutzer gültige Anmeldeinformationen eingibt, wird der Vorgang mit dem höchsten verfügbaren Recht des Benutzers fortgesetzt.

  - *Eingabeaufforderung zur Zustimmung auf dem sicheren Desktop*: Wenn für einen Vorgang erhöhte Rechte erforderlich sind, wird der Benutzer auf dem sicheren Desktop zur Auswahl von „Zulassen“ oder „Verweigern“ aufgefordert. Wenn der Benutzer „Zulassen“ auswählt, wird der Vorgang mit dem höchsten verfügbaren Recht des Benutzers fortgesetzt.

  - *Eingabeaufforderung zu Anmeldeinformationen*: Wenn für einen Vorgang erhöhte Rechte erforderlich sind, wird der Benutzer zur Eingabe eines Administratorbenutzernamens und -kennworts aufgefordert. Wenn der Benutzer gültige Anmeldeinformationen eingibt, wird der Vorgang mit der jeweiligen Berechtigung des Benutzers fortgesetzt.

  - *Eingabeaufforderung zur Zustimmung*: Wenn für einen Vorgang erhöhte Rechte erforderlich sind, wählen Sie entweder „Zulassen“ oder „Verweigern“ aus. Wenn der Benutzer „Zulassen“ auswählt, wird der Vorgang mit dem höchsten verfügbaren Recht des Benutzers fortgesetzt.

  - *Eingabeaufforderung zur Zustimmung für Nicht-Windows-Binärdateien*: Wenn für einen Vorgang für eine nicht von Microsoft stammende Anwendung erhöhte Rechte erforderlich sind, wird der Benutzer auf dem sicheren Desktop aufgefordert, entweder „Zulassen“ oder „Verweigern“ auszuwählen. Wenn der Benutzer „Zulassen“ auswählt, wird der Vorgang mit dem höchsten verfügbaren Recht des Benutzers fortgesetzt.

  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067215)

  **Standardeinstellung:** Zustimmungsaufforderung für sicheren Desktop

- **Minimale Sitzungssicherheit für NTLM-SSP-basierte Clients**:  
  Mit dieser Sicherheitseinstellung kann die Aushandlung der 128-Bit-Verschlüsselung und der NTLMv2-Sitzungssicherheit für einen Client als erforderlich festgelegt werden. Diese Werte hängen vom Wert des Sicherheitseinstellungswerts für die LAN Manager-Authentifizierungsebene ab. Folgende Optionen sind verfügbar:

  - *NTLMv2-Sitzungssicherheit erfordern*: Die Verbindung schlägt fehl, wenn das NTLMv2-Protokoll nicht ausgehandelt wird.

  - *128-Bit-Verschlüsselung erfordern*: Die Verbindung schlägt fehl, wenn keine starke Verschlüsselung (128-Bit) ausgehandelt wird.

  - *NTLMv2- und 128-Bit-Verschlüsselung erfordern*.

  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067324)

  **Standardeinstellung:** NTLMv2- und 128-Bit-Verschlüsselung erfordern

- **Verhalten beim Entfernen von Smartcards:**  
  Diese Sicherheitseinstellung legt fest, was geschieht, wenn die Smartcard für einen angemeldeten Benutzer aus dem Smartcardleser entfernt wird. Folgende Optionen sind verfügbar:

  - *Keine Aktion*.

  - *Arbeitsstation sperren* – Die Arbeitsstation wird beim Entfernen der Smartcard gesperrt, sodass Benutzer den Arbeitsbereich verlassen, die Smartcard mitnehmen und dennoch eine geschützte Sitzung aufrechterhalten können.

  - *Abmeldung erzwingen*: Der Benutzer wird automatisch abgemeldet, wenn die Smartcard entfernt wird.

  - *Disconnect Remote Desktop session* (Remotedesktopsitzung beenden): Das Entfernen der Smartcard beendet die Sitzung, ohne den Benutzer abzumelden. Dies ermöglicht es Benutzern, die Smartcard einzulegen und die Sitzung später oder auf einem anderen Computer mit Smartcard-Leser fortzusetzen, ohne sich erneut anmelden zu müssen. Wenn die Sitzung lokal stattfindet, funktioniert diese Richtlinie genau wie „Arbeitsstation sperren“.

  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067331)

  **Standardeinstellung:** Arbeitsstation sperren

- **Anonyme Aufzählung von SAM-Konten und Freigaben blockieren**:  
  Diese Sicherheitseinstellung legt fest, ob die anonyme Aufzählung von SAM-Konten und Freigaben zugelassen wird. Windows erlaubt anonymen Benutzern bestimmte Aktionen, z. B. das Aufzählen der Namen von Domänenkonten und Netzwerkfreigaben. Das kann z. B. besonders nützlich sein, wenn ein Administrator Benutzern in einer vertrauenswürdigen Domäne Zugriffsberechtigungen gewähren möchte, die diese Vertrauensstellung nicht erwidert. Wenn Sie die anonyme Aufzählung von SAM-Konten und Freigaben nicht zulassen möchten, legen Sie für diese Richtlinie *Ja* fest.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067191)

  **Standardeinstellung:** Ja

- **Remoteanmeldung mit leerem Kennwort blockieren**:  
  Diese Sicherheitseinstellung legt fest, ob lokale Konten, die nicht kennwortgeschützt sind, zum Anmelden an anderen Orten als der Konsole des physischen Computers verwendet werden können. Wenn diese Einstellung aktiviert ist, können lokale Konten ohne Kennwortschutz nur über die Computertastatur angemeldet werden.

  *Warnung:* Für Computer, die sich nicht an sicheren Orten befinden, sollten immer strikte Kennwortrichtlinien für alle Benutzerkonten verwendet werden. Ansonsten kann sich jeder mit physischem Zugang zu dem Computer mit einem Benutzerkonto ohne Kennwort anmelden. Dies gilt besonders für tragbare Computer.

  Wenn Sie diese Sicherheitsrichtlinie auf die Gruppe „Alle“ anwenden, kann sich niemand über Remotedesktopdienste anmelden. Diese Einstellung wirkt sich nicht auf Anmeldungen mit Domänenkonten aus. Anwendungen mit interaktiven Remoteanmeldungen können diese Einstellung umgehen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067219)

  **Standardeinstellung:** Ja

- **Verhalten der Eingabeaufforderung für erhöhte Rechte für Standardbenutzer**:  
  Mit dieser Richtlinieneinstellung können Sie das Verhalten der Eingabeaufforderung für erhöhte Rechte für Standardbenutzer bestimmen.

  - *Anforderungen für erhöhte Rechte automatisch ablehnen*: Wenn für einen Vorgang erhöhte Rechte erforderlich sind, wird eine konfigurierbare Fehlermeldung für verweigerten Zugriff angezeigt. Ein Unternehmen, in dem Desktops als Standardbenutzer ausgeführt werden, kann diese Einstellung verwenden, damit der Helpdesk seltener kontaktiert wird.

  - *Eingabeaufforderung zu Anmeldeinformationen auf dem sicheren Desktop*: Wenn für einen Vorgang erhöhte Rechte erforderlich sind, wird der Benutzer auf dem sicheren Desktop zur Eingabe eines anderen Benutzernamens und Kennworts aufgefordert. Wenn der Benutzer gültige Anmeldeinformationen eingibt, wird der Vorgang mit der jeweiligen Berechtigung des Benutzers fortgesetzt.

  - *Eingabeaufforderung zu Anmeldeinformationen*: Wenn für einen Vorgang erhöhte Rechte erforderlich sind, wird der Benutzer zur Eingabe eines Administratorbenutzernamens und -kennworts aufgefordert. Wenn der Benutzer gültige Anmeldeinformationen eingibt, wird der Vorgang mit der jeweiligen Berechtigung des Benutzers fortgesetzt.

  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067183)

  **Standardeinstellung:** Anforderungen für erhöhte Rechte automatisch ablehnen

- **Administratorgenehmigungsmodus für Administratoren erforderlich**:  
  Mit dieser Richtlinieneinstellung wird das Verhalten aller UAC-Richtlinieneinstellungen (User Account Control, Benutzerkontensteuerung) für den Computer bestimmt. Wenn Sie diese Richtlinieneinstellung ändern, müssen Sie den Computer neu starten. Folgende Optionen sind verfügbar:

  - *Nicht konfiguriert*: Der Administratorgenehmigungsmodus und alle verwandten UAC-Richtlinieneinstellungen sind deaktiviert. Anmerkung: Wenn diese Richtlinieneinstellung deaktiviert ist, werden Sie vom Security Center benachrichtigt, dass die allgemeine Sicherheit des Betriebssystems eingeschränkt ist.

  - *Ja*: Der Administratorgenehmigungsmodus ist aktiviert. Diese Richtlinieneinstellung muss aktiviert und die verwandten UAC-Richtlinieneinstellungen müssen entsprechend festgelegt werden, damit das integrierte Administratorkonto und alle anderen Benutzerkonten, die Mitglieder der Administratorgruppe sind, im Administratorgenehmigungsmodus ausgeführt werden können.

  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067184)

  **Standardeinstellung:** Ja

- **Anonyme Aufzählung von SAM-Konten verhindern**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, welche zusätzlichen Berechtigungen für anonyme Verbindungen mit dem Computer gewährt werden. Windows erlaubt anonymen Benutzern bestimmte Aktionen, z. B. das Aufzählen der Namen von Domänenkonten und Netzwerkfreigaben. Das kann z. B. besonders nützlich sein, wenn ein Administrator Benutzern in einer vertrauenswürdigen Domäne Zugriffsberechtigungen gewähren möchte, die diese Vertrauensstellung nicht erwidert. Mit dieser Sicherheitseinstellung können die folgenden zusätzlichen Einschränkungen für anonyme Verbindungen vorgenommen werden:

  - *Ja*: Enumeration von SAM-Konten nicht zulassen. Diese Option ersetzt die Option „Everyone with Authenticated Users“ (Jeder mit authentifizierten Benutzern) in den Sicherheitsberechtigungen für Ressourcen.

  - *Nicht konfiguriert*: Keine zusätzlichen Einschränkungen. Es gelten die Standardberechtigungen.

  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067318)

  **Standardeinstellung:** Ja

- **SAM-Remoteaufrufe zulassen**:  
  Mit dieser Richtlinieneinstellung können Sie RPC-Verbindungen mit dem SAM einschränken. Wenn diese Einstellung nicht festgelegt wurde, wird die Standardsicherheitsbeschreibung verwendet.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067209)

  **Standardeinstellung:** *O:BAG:BAD:(A;;RC;;;BA)*

- **Verwendung des Administratorgenehmigungsmodus**:  
  Mit dieser Richtlinieneinstellung können Sie das Verhalten des Administratorgenehmigungsmodus für das integriertes Administratorkonto bestimmen. Folgende Optionen sind verfügbar:

  - *Ja*: Für das integrierte Administratorkonto wird der Administratorgenehmigungsmodus verwendet. Der Benutzer wird standardmäßig bei jedem Vorgang, der eine Rechteerweiterungen erfordert, zur Genehmigung aufgefordert.

  - *Nicht konfiguriert*: Mit dem integrierten Administratorkonto werden alle Anwendungen mit vollständigen Administratorrechten ausgeführt.

  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067186)

  **Standardeinstellung:** Ja
  
- **Nur UIAccess-Anwendungen für sichere Speicherorte zulassen:**  
  Mit dieser Sicherheitseinstellung können Sie bestimmen, ob Programme für Bedienungshilfen für die Benutzeroberfläche (UIAccess oder UIA) automatisch den sicheren Desktop für Eingabeaufforderungen mit erhöhten Rechten eines Standardbenutzers deaktivieren kann.

  - *Ja*: UIA-Programme, darunter Windows-Remoteunterstützung, deaktivieren automatisch den sicheren Desktop für Eingabeaufforderungen für erhöhte Rechte. Wenn Sie die Richtlinieneinstellung „Benutzerkontensteuerung: Bei Benutzeraufforderung nach erhöhten Rechten zum sicheren Desktop wechseln“ nicht deaktivieren, werden die Eingabeaufforderungen auf dem Desktop des interaktiven Benutzers und nicht auf dem sicheren Desktop angezeigt.

  - *Nicht konfiguriert:* Der sichere Desktop kann nur vom Benutzer des interaktiven Desktops oder durch Deaktivieren der Richtlinieneinstellung „Benutzerkontensteuerung: Bei Benutzeraufforderung nach erhöhten Rechten zum sicheren Desktop wechseln“ deaktiviert werden.

  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067185)

  **Standardeinstellung:** Ja

- **Anwendungsinstallationen erkennen und erhöhte Rechte anfordern**:  
  Mit dieser Richtlinieneinstellung können Sie das Verhalten bei der Erkennung einer Anwendungsinstallation auf dem Computer bestimmen. Folgende Optionen sind verfügbar:

  - *Aktiviert*: Wenn ein Anwendungsinstallationspaket erkannt wird, das erhöhte Rechte erfordert, wird der Benutzer zur Eingabe eines Administratorbenutzernamens und -kennworts aufgefordert. Wenn der Benutzer gültige Anmeldeinformationen eingibt, wird der Vorgang mit der jeweiligen Berechtigung des Benutzers fortgesetzt.

  - *Deaktiviert*: Anwendungsinstallationspakete werden nicht erkannt, und es wird keine Eingabeaufforderung für erhöhte Rechte angezeigt. Unternehmen, die Desktops von Standardbenutzern ausführen und delegierte Installationstechnologien wie Group Policy Software Installation oder Systems Management Server (SMS) verwenden, sollten diese Richtlinieneinstellung deaktivieren. In diesem Fall ist die Installererkennung unnötig.

  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067208)

  **Standardeinstellung:** Ja

- **Speichern von LAN-Manager-Hashwert bei nächster Kennwortänderung verhindern**:  
  Mit dieser Sicherheitseinstellung können Sie bestimmen, ob der Hashwert des LAN-Managers (LM) bei der nächsten Kennwortänderung für das neue Kennwort gespeichert werden soll. Der LM-Hashwert ist im Vergleich zum kryptografisch stärkeren Windows NT-Hashwert relativ schwach und angreifbar. Da der LM-Hashwert auf dem lokalen Computer in der Sicherheitsdatenbank gespeichert wird, können die Kennwörter gefährdet sein, wenn die Sicherheitsdatenbank angegriffen wird.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067213)

  **Standardeinstellung:** Ja

- **Fehler bei Schreibvorgängen für Dateien und Registrierung basierend auf Benutzerspeicherorten virtualisieren**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob Fehler bei Anwendungsschreibvorgängen an definierte Registrierungs- und Dateisystemspeicherorte weitergeleitet werden. Mit dieser Richtlinieneinstellung werden Anwendungen, die mit Administratorrechten ausgeführt werden und die Laufzeitanwendungsdaten schreiben, zum folgenden Verzeichnis migriert: *%Programme%* , *%Windir%* , *%Windir%\system32* oder *HKLM\Software*.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067321)

  **Standardeinstellung:** Ja

## <a name="microsoft-defender"></a>Microsoft Defender

Weitere Informationen finden Sie unter [Policy CSP - Defender (Richtlinien-Konfigurationsdienstanbieter: Defender)](/windows/client-management/mdm/policy-csp-defender) in Ihrer Windows-Dokumentation.

::: zone-end
::: zone pivot="mdm-may-2019"

- **Block Adobe Reader from creating child processes** (Adobe Reader am Erstellen von untergeordneten Prozessen hindern):  
Diese Regel verhindert Angriffe, indem Adobe Reader am Erstellen zusätzlicher Prozesse gehindert wird. Über Social Engineering oder Exploits kann Schadsoftware zusätzliche Payloads herunterladen und starten sowie Adobe Reader unterbrechen. Durch das Blockieren der Generierung untergeordneter Prozesse durch Adobe Reader wird Malware, die versucht, sie als Vektor zu verwenden, an der Verbreitung gehindert.
[Erfahren Sie mehr](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  **Standardeinstellung:** Aktivieren Sie

- **Office: Kommunikations-Apps starten in untergeordnetem Prozess**:  
  [Schützen von Geräten vor Exploits](https://go.microsoft.com/fwlink/?linkid=874499)

  **Standardeinstellung:** Aktivieren Sie

- **Eingeben, wie oft (0–24 Stunden) nach Security Intelligence-Updates gesucht wird**  
  CSP: [Defender/SignatureUpdateInterval](https://go.microsoft.com/fwlink/?linkid=2113936)
  
  Geben Sie an, wie oft nach neuen Signaturen gesucht werden soll. Der Wert 1 bedeutet eine Stunde, 2 bedeutet zwei Stunden und so weiter.

  **Standardeinstellung:** 4

::: zone-end
::: zone pivot="mdm-preview,mdm-may-2019"

- **Defender-Überprüfungstag planen**:  
  Defender-Überprüfungstag planen.

  **Standardeinstellung:** Täglich

- **Von der Cloud bereitgestellten Schutz aktivieren:**  
  CSP: [Defender/AllowCloudProtection](https://go.microsoft.com/fwlink/?linkid=2113937)
  
  Wenn „Ja“ festgelegt ist, sendet Microsoft Defender zu jedem entdeckten Problem Informationen an Microsoft. Wenn „Nicht konfiguriert“ festgelegt ist, verwendet der Client die Standardeinstellung, bei der das Feature zwar aktiviert ist, aber vom Benutzer deaktiviert werden kann.

  **Standardeinstellung:**  Ja  

- **Echtzeitschutz aktivieren**  
  CSP: [Defender/AllowRealtimeMonitoring](https://go.microsoft.com/fwlink/?linkid=2114050)

  Wenn für diese Einstellung „Ja“ festgelegt ist, wird die Echtzeitüberwachung erzwungen und kann vom Benutzer nicht deaktiviert werden. Wenn „Nicht konfiguriert“ festgelegt ist, wird die Einstellung auf den Standardwert des Clients zurückgesetzt, d. h. aktiviert. Der Benutzer kann dies jedoch ändern. Verwenden Sie einen benutzerdefinierten URI, um die Echtzeitüberwachung zu deaktivieren.

  **Standardeinstellung:**  Ja  

- **Archivdateien überprüfen:**  
  CSP: [Defender/AllowArchiveScanning](https://go.microsoft.com/fwlink/?linkid=2114047)
  
  Wenn für diese Einstellung „Ja“ festgelegt ist, wird das Überprüfen von Archivdateien wie ZIP- oder CAB-Dateien erzwungen. Wenn „Nicht konfiguriert“ festgelegt ist, wird die Einstellung auf den Standardwert des Clients zurückgesetzt, d. h., archivierte Dateien werden überprüft. Der Benutzer kann die Überprüfung jedoch deaktivieren.

  **Standardeinstellung:** Ja

- **Verhaltensüberwachung aktivieren:**  
  CSP: [Defender/AllowBehaviorMonitoring](https://go.microsoft.com/fwlink/?linkid=2114048)

  Wenn für diese Einstellung „Ja“ festgelegt ist, wird die Verhaltensüberwachung erzwungen und kann vom Benutzer nicht deaktiviert werden. Wenn „Nicht konfiguriert“ festgelegt ist, wird die Einstellung auf den Standardwert des Clients zurückgesetzt, d. h. aktiviert. Der Benutzer kann dies jedoch ändern. Verwenden Sie einen benutzerdefinierten URI, um die Echtzeitüberwachung zu deaktivieren.

  **Standardeinstellung:** Ja

- **Eingehende E-Mail überprüfen:**  
  CSP: [Defender/AllowEmailScanning](https://go.microsoft.com/fwlink/?linkid=2114052)

  Wenn „Ja“ festgelegt ist, werden das E-Mail-Postfach sowie E-Mail-Dateien wie PST-, DBX-, MNX-, MIME- und BINHEX-Dateien überprüft. Wenn „Nicht konfiguriert“ festgelegt ist, wird die Einstellung auf den Standardwert des Clients zurückgesetzt, d. h., E-Mail-Dateien werden nicht überprüft.

  **Standardeinstellung:** Ja

- **Scan removable drives during a full scan** (Bei einer vollständigen Überprüfung Wechseldatenträger überprüfen):  
  CSP: [Defender/AllowFullScanRemovableDriveScanning](https://go.microsoft.com/fwlink/?linkid=2113946)

  Wenn „Ja“ festgelegt ist, werden bei einer vollständigen Überprüfung Wechseldatenträger (z. B. USB-Speichersticks) überprüft. Wenn „Nicht konfiguriert“ festgelegt ist, wird die Einstellung auf den Standardwert des Clients zurückgesetzt, d. h., Wechseldatenträger werden überprüft. Der Benutzer kann diese Überprüfung jedoch deaktivieren.
  **Standardeinstellung:** Ja  

- **Block Office applications from injecting code into other processes** (Einschleusung von Code durch Office-Anwendungen in andere Prozesse blockieren):  
  [Schützen von Geräten vor Exploits](https://go.microsoft.com/fwlink/?linkid=872974)

  Wenn „Ja“ festgelegt ist, wird die Einschleusung von Code durch Office-Anwendungen in andere Prozesse blockiert. Wenn „Nur überwachen“ festgelegt ist, werden statt des Blockierens Windows-Ereignisse ausgelöst. Wenn „Nicht konfiguriert“ festgelegt ist, wird die Einstellung auf den Standardwert von Windows zurückgesetzt, d. h. deaktiviert. Diese ASR-Regel wird über die folgende GUID gesteuert: 75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84

  **Standardeinstellung:**  Blockieren

- **Erstellung ausführbarer Inhalte durch Office-Anwendungen blockieren**  
  [Schützen von Geräten vor Exploits](https://go.microsoft.com/fwlink/?linkid=872975)

  Wenn „Ja“ festgelegt ist, dürfen Office-Anwendungen keine ausführbaren Inhalte erstellen. Wenn „Nur überwachen“ festgelegt ist, werden statt des Blockierens Windows-Ereignisse ausgelöst. Wenn „Nicht konfiguriert“ festgelegt ist, wird die Einstellung auf den Standardwert von Windows zurückgesetzt, d. h. deaktiviert. Diese ASR-Regel wird über die folgende GUID gesteuert: 3B576869-A4EC-4529-8536-B80A7769E899

  **Standardeinstellung:**  Blockieren

- **Alle Office-Anwendungen am Erstellen von untergeordneten Prozessen hindern**  
  [Schützen von Geräten vor Exploits](https://go.microsoft.com/fwlink/?linkid=872976)

  Wenn der Überwachungsmodus aktiviert ist, werden statt des Blockierens Windows-Ereignisse ausgelöst. Wenn „Nicht konfiguriert“ festgelegt ist, wird die Einstellung auf den Standardwert von Windows zurückgesetzt, d. h. deaktiviert. Diese ASR-Regel wird über die folgende GUID gesteuert: D4F940AB-401B-4EFC-AADC-AD5F3C50688A

  **Standardeinstellung:**  Blockieren

- **Block Win32 API calls from Office macro** (Win32-API-Aufrufe von Office-Makros blockieren):  
  [Schützen von Geräten vor Exploits](https://go.microsoft.com/fwlink/?linkid=872977)

  Wenn „Ja“ festgelegt ist, wird die Verwendung von Win32-API-Aufrufen durch Office-Makros wird blockiert. Wenn „Nur überwachen“ festgelegt ist, werden statt des Blockierens Windows-Ereignisse ausgelöst. Wenn „Nicht konfiguriert“ festgelegt ist, wird die Einstellung auf den Standardwert von Windows zurückgesetzt, d. h. deaktiviert. Diese ASR-Regel wird über die folgende GUID gesteuert: 92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B
  
  **Standardeinstellung:** Blockieren

- **Block execution of potentially obfuscated scripts (js/vbs/ps)** (Ausführung möglicherweise verschleierter Skripts blockieren (JS/VBS/PS)):  
  [Schützen von Geräten vor Exploits](https://go.microsoft.com/fwlink/?linkid=872978)

  Wenn „Ja“ festgelegt ist, blockiert Microsoft Defender die Ausführung verschleierter Skripts. Wenn „Nur überwachen“ festgelegt ist, werden statt des Blockierens Windows-Ereignisse ausgelöst. Wenn „Nicht konfiguriert“ festgelegt ist, wird die Einstellung auf den Standardwert von Windows zurückgesetzt, d. h. deaktiviert. Diese ASR-Regel wird über die folgende GUID gesteuert: 5BEB7EFE-FD9A-4556-801D-275E5FFC04CC
  
  **Standardeinstellung:** Blockieren

- **Ausführungstyp für E-Mail-Inhalt**:    
  [Download ausführbarer Inhalte aus E-Mail- und Webmailclients blockieren](https://go.microsoft.com/fwlink/?linkid=872980)

  Wenn „Ja“ festgelegt ist, werden ausführbare Inhalte blockiert, die über E-Mail-Clients oder Webmailclients heruntergeladen wurden. Wenn „Nur überwachen“ festgelegt ist, werden statt des Blockierens Windows-Ereignisse ausgelöst. Wenn „Nicht konfiguriert“ festgelegt ist, wird die Einstellung auf den Standardwert von Windows zurückgesetzt, d. h. deaktiviert.

  **Standardeinstellung:** Blockieren

- **Diebstahl von Anmeldeinformationen verhindern**:  
  [Schützen von Geräten vor Exploits](https://go.microsoft.com/fwlink/?linkid=874499)
  
  Wenn „Ja“ festgelegt ist, werden Versuche, Anmeldeinformationen über „lsass.exe“ zu stehlen, blockiert. Wenn „Nur überwachen“ festgelegt ist, werden statt des Blockierens Windows-Ereignisse ausgelöst. Wenn „Nicht konfiguriert“ festgelegt ist, wird die Einstellung auf den Standardwert von Windows zurückgesetzt, d. h. deaktiviert. Diese ASR-Regel wird über die folgende GUID gesteuert: 9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2

  **Standardeinstellung:** Aktivieren Sie

- **Potenziell unerwünschte App-Aktion in Defender**:  
  CSP: [Defender/PUAProtection](/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)+

  Das Feature zum Schutz vor potenziell unerwünschten Anwendungen (Potentially Unwanted Applications, PUAs) in Microsoft Defender Antivirus kann solche Anwendungen identifizieren und verhindern, dass diese auf Endpunkte in ihrem Netzwerk heruntergeladen und dort installiert werden. Bei diesen Anwendungen handelt es sich nicht um Viren, Schadsoftware oder andere Arten von Bedrohungen. Diese Anwendungen können Aktionen auf Endpunkten ausführen, die deren Leistung oder Verwendung beeinträchtigen. Mit PUAs können auch Anwendungen gemeint sein, die einen schlechten Ruf haben. Typisches PUA-Verhalten umfasst: verschiedene Arten von Softwarebündelungen, die Einschleusung von Werbung in Webbrowser sowie Treiber- und Registrierungsoptimierungen, die Probleme erkennen, eine Zahlung zur Fehlerbehebung anfordern, aber auf dem Endpunkt verbleiben und weder Änderungen noch Optimierungen vornehmen (auch bekannt als „Rogue-Sicherheitssoftware“). Diese Anwendungen können das Risiko einer Infektion mit Schadsoftware für Ihr Netzwerk erhöhen, das Identifizieren von Infektionen erschweren und unnötig IT-Ressourcen zum Bereinigen der Anwendungen belegen.

  **Standardeinstellung:** Blockieren

- **Block untrusted and unsigned processes that run from USB** (Blockieren von nicht vertrauenswürdigen und nicht signierten Prozessen, die von USB ausgeführt werden):  
  [Schützen von Geräten vor Exploits](https://go.microsoft.com/fwlink/?linkid=874502)
  
  Wenn „Ja“ festgelegt ist, werden nicht vertrauenswürdige/nicht signierte Prozesse blockiert, die von einem USB-Laufwerk aus ausgeführt werden. Wenn „Nur überwachen“ festgelegt ist, werden statt des Blockierens Windows-Ereignisse ausgelöst. Wenn „Nicht konfiguriert“ festgelegt ist, wird die Einstellung auf den Standardwert von Windows zurückgesetzt, d. h. deaktiviert. Diese ASR-Regel wird über die folgende GUID gesteuert: b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4

  **Standardeinstellung:** Blockieren

- **Netzwerkschutz**:  
  [Defender/EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=872618)

  Wenn „Ja“ festgelegt ist, ist der Netzwerkschutz für alle Benutzer im System aktiviert. Der Netzwerkschutz schützt Mitarbeiter vor betrügerischen Phishingversuchen und dem Zugriff auf schädliche Inhalte im Internet. Dies umfasst auch Browser von Drittanbietern. Wenn „Nur überwachen“ festgelegt ist, wird der Zugriff auf gefährliche Domänen für Benutzer nicht blockiert, es werden jedoch stattdessen Windows-Ereignisse ausgelöst. Wenn „Nicht konfiguriert“ festgelegt ist, wird die Einstellung auf den Standardwert von Windows zurückgesetzt, d. h. deaktiviert.

  **Standardeinstellung:** Aktivieren Sie

- **Defender: Zustimmung für Stichprobenübermittlung**:  
  [Defender/SubmitSamplesConsent](https://go.microsoft.com/fwlink/?linkid=2067131)

  Diese Einstellung sucht nach der Benutzerzustimmungsebene in Microsoft Defender, um Daten zu senden. Wenn die erforderliche Zustimmung bereits erteilt wurde, sendet Microsoft Defender die Daten. Wenn nicht (und wenn der Benutzer angegeben hat, nie zu fragen), wird die Benutzeroberfläche gestartet, um nach der Benutzerzustimmung zu fragen (wenn Defender/AllowCloudProtection gestattet ist), bevor Daten gesendet werden.

  **Standardeinstellung:** Sichere Beispiele automatisch senden

::: zone-end
::: zone pivot="mdm-may-2019"

- **Netzwerkdateien überprüfen**  
  [Defender/AllowScanningNetworkFiles](https://go.microsoft.com/fwlink/?linkid=2114049)

  - **Standardeinstellung:** Ja

- **Starten heruntergeladener ausführbarer Inhalte durch JavaScript oder VBScript blockieren**  
  [Schützen von Geräten vor Exploits](https://go.microsoft.com/fwlink/?linkid=872979)

  Wenn „Ja“ festgelegt ist, blockiert Microsoft Defender das Ausführen von JavaScript- oder VBScript-Dateien, die aus dem Internet heruntergeladen wurden. Wenn „Nur überwachen“ festgelegt ist, werden statt des Blockierens Windows-Ereignisse ausgelöst. Wenn „Nicht konfiguriert“ festgelegt ist, wird die Einstellung auf den Standardwert von Windows zurückgesetzt, d. h. deaktiviert. Diese ASR-Regel wird über die folgende GUID gesteuert: D3E037E1-3EB8-44C8-A917-57927947596D

::: zone-end
::: zone pivot="mdm-may-2019,mdm-preview"

## <a name="ms-security-guide"></a>MSSecurityGuide

Weitere Informationen finden Sie unter [Policy CSP - MSSecurityGuide (Richtlinien-CSP: MSSecurityGuide)](/windows/client-management/mdm/policy-csp-mssecurityguide) in der Windows-Dokumentation.

- **Bei Netzwerkanmeldung Einschränkungen der Benutzerkontensteuerung auf lokale Konten anwenden**:  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067188)

  **Standardeinstellung:** Aktiviert

- **Startkonfiguration für SMB v1-Clienttreiber**:  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067214)

  **Standardeinstellung:** Treiber deaktiviert

- **SMB v1-Server**:  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067190)

  **Standardeinstellung:** Deaktiviert

- **Digestauthentifizierung**:  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067193)

  **Standardeinstellung:** Deaktiviert

- **Überschreibungsschutz für strukturierte Ausnahmebehandlung**:  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067217)

  **Standardeinstellung:** Aktiviert

## <a name="mss-legacy"></a>MSS Legacy

Weitere Informationen finden Sie unter [Policy CSP - MSSLegacy (Richtlinen-CSP: MSSLegacy)](/windows/client-management/mdm/policy-csp-msslegacy) in der Windows-Dokumentation.

- **Schutzebene für Netzwerk-IPv6-Quellrouting**:  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067220)

  **Standardeinstellung:** Höchster Schutz  

- **Netzwerk ignoriert Anforderungen zur NetBIOS-Namensfreigabe, WINS-Server ausgenommen**:  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067218)

  **Standardeinstellung:** Aktiviert

- **Schutzebene für Netzwerk-IPv6-Quellrouting**:  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067216)

  **Standardeinstellung:** Höchster Schutz

- **Network ICMP redirects override OSPF generated routes** (Netzwerk-ICMP-Umleitungen setzen OSPF-generierte Routen außer Kraft):  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067326)

  **Standardeinstellung:** Deaktiviert

## <a name="power"></a>Power

Weitere Informationen finden Sie unter [Policy CSP - Power (Richtlinien-CSP: Power)](/windows/client-management/mdm/policy-csp-power) in der Windows-Dokumentation.

- **Kennwort bei Aktivierung im Netzbetrieb erforderlich**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob der Benutzer zur Eingabe eines Kennworts aufgefordert wird, wenn das System aus dem Energiesparmodus reaktiviert wird. Wenn Sie diese Richtlinieneinstellung aktivieren oder nicht konfigurieren, wird der Benutzer beim Verlassen des Energiesparmodus zur Eingabe eines Kennworts aufgefordert. Wenn Sie diese Richtlinieneinstellung deaktivieren, wird der Benutzer beim Verlassen des Energiesparmodus nicht zur Eingabe eines Kennworts aufgefordert.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067221)

  **Standardeinstellung:** Aktiviert

- **Standbyzustände bei Ruhezustand im Akkubetrieb**:  
  Diese Richtlinieneinstellung legt fest, ob Windows Standbyzustände verwenden kann, wenn der Computer in den Energiesparmodus versetzt wird. Wenn Sie diese Richtlinieneinstellung aktivieren oder nicht konfigurieren, verwendet Windows Standbyzustände, um den Computer in den Energiesparmodus zu versetzen. Wenn Sie diese Richtlinieneinstellung deaktivieren, sind Standbyzustände (S1–S3) nicht zulässig.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067195)

  **Standardeinstellung:** Deaktiviert

- **Standbyzustände bei Ruhezustand im Netzbetrieb**:  
  Diese Richtlinieneinstellung legt fest, ob Windows Standbyzustände verwenden kann, wenn der Computer in den Energiesparmodus versetzt wird. Wenn Sie diese Richtlinieneinstellung aktivieren oder nicht konfigurieren, verwendet Windows Standbyzustände, um den Computer in den Energiesparmodus zu versetzen. Wenn Sie diese Richtlinieneinstellung deaktivieren, sind Standbyzustände (S1–S3) nicht zulässig.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067196)

  **Standardeinstellung:** Deaktiviert

- **Kennwort bei Aktivierung im Akkubetrieb erforderlich**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob der Benutzer zur Eingabe eines Kennworts aufgefordert wird, wenn das System aus dem Energiesparmodus reaktiviert wird. Wenn Sie diese Richtlinieneinstellung aktivieren oder nicht konfigurieren, wird der Benutzer beim Verlassen des Energiesparmodus zur Eingabe eines Kennworts aufgefordert. Wenn Sie diese Richtlinieneinstellung deaktivieren, wird der Benutzer beim Verlassen des Energiesparmodus nicht zur Eingabe eines Kennworts aufgefordert.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067322)

  **Standardeinstellung:** Aktiviert

::: zone-end
::: zone pivot="mdm-may-2019"

## <a name="remote-assistance"></a>Remoteunterstützung

Erfahren Sie mehr unter [Richtlinien-CSP: RemoteAssistance](/windows/client-management/mdm/policy-csp-remoteassistance#remoteassistance-solicitedremoteassistance) in der Windows Dokumentation.

- **Angeforderte Remoteunterstützung:**  
  Mit dieser Richtlinieneinstellung können Sie die Einstellung „Angeforderte Remoteunterstützung“ auf diesem Computer aktivieren bzw. deaktivieren.
  
  - *Wenn Sie diese Richtlinieneinstellung aktivieren*, können Benutzer auf diesem Computer per E-Mail oder Dateiübertragung Hilfe anfordern. Außerdem können Benutzer Instant-Messaging-Programme verwenden, um Verbindungen mit diesem Computer zuzulassen, und Sie können zusätzliche Einstellungen für die Remoteunterstützung konfigurieren.

  - *Wenn Sie diese Richtlinieneinstellung deaktivieren*, können Benutzer auf diesem Computer nicht per E-Mail oder Dateiübertragung Hilfe anfordern. Außerdem können Benutzer keine Instant-Messaging-Programme verwenden, um Verbindungen mit diesem Computer zuzulassen.

  - *Wenn Sie diese Richtlinieneinstellung nicht konfigurieren*, können Benutzer die Einstellung „Angeforderte Remoteunterstützung“ selbst unter „Systemeigenschaften“ in der Systemsteuerung aktivieren bzw. deaktivieren. Benutzer können zudem die Einstellungen für die Remoteunterstützung konfigurieren.

  Wenn Sie diese Richtlinieneinstellung aktivieren, stehen Ihnen zwei Möglichkeiten zur Verfügung, um zuzulassen, dass Helfer Remoteunterstützung leisten können: „Helfer dürfen den Computer nur ansehen“ oder „Helfer dürfen den Computer remote steuern“. Die Richtlinieneinstellung „Maximum ticket time“ (Maximale Ticketgültigkeit) legt fest, wie lange eine per E-Mail oder Dateiübertragung übermittelte Einladung zur Remoteunterstützung offen bleiben darf. Die Einstellung „Select the method for sending email invitations“ (Methode zum Senden von E-Mail-Einladungen auswählen) gibt an, welcher E-Mail-Standard zum Senden von Einladungen zur Remoteunterstützung verwendet werden soll. Je nach E-Mail-Programm können Sie entweder den *Mailto*-Standard (der Empfänger der Einladung stellt über einen Link eine Verbindung her) oder den SMAPI-Standard (Simple MAPI; die Einladung wird an Ihre E-Mail angehängt) verwenden. Diese Richtlinieneinstellung ist unter Windows Vista nicht verfügbar, da dieses Betriebssystem nur die SMAPI-Methode unterstützt. Wenn Sie diese Richtlinieneinstellung aktivieren, sollten Sie auch passende Firewallausnahmen aktivieren, um die Kommunikation zur Remoteunterstützung zuzulassen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067198)

  **Standardeinstellung:** Remoteunterstützung deaktivieren

<!-- These settings are not available: 
  When set to *Enable Remote Assistance*, configure the following additional settings:

  - **Remote Assistance solicited permission**:  
    **Default**: View

  - **Maximum ticket time value**:  
    **Default**: *Not configured*

  - **Maximum ticket time period**:  
    **Default**: Minutes

  - **E-Mail invitation method**:  
    **Default**: Simple MAPI
-->

::: zone-end
::: zone pivot="mdm-preview,mdm-may-2019"

## <a name="remote-desktop-services"></a>Remotedesktopdienste

Weitere Informationen finden Sie unter [Policy CSP – RemoteDesktopServices (Richtlinien-Konfigurationsdienstanbieter: RemoteDesktopServices)](/windows/client-management/mdm/policy-csp-remotedesktopservices) in der Windows-Dokumentation.

- **Kennwortspeicherung blockieren**:  
  Diese Richtlinieneinstellung steuert, ob Kennwörter auf diesem Computer über die Remotedesktopverbindung gespeichert werden können. Wenn Sie diese Einstellung aktivieren, wird das Kontrollkästchen für die Kennwortspeicherung in der Remotedesktopverbindung deaktiviert, und Benutzer können Kennwörter nicht speichern. Wenn ein Benutzer eine RDP-Datei über die Remotedesktopverbindung öffnet und seine Einstellungen speichert, werden alle zuvor in der RDP-Datei vorhandenen Kennwörter gelöscht. Wenn Sie diese Einstellung deaktivieren oder nicht konfigurieren, kann der Benutzer Kennwörter über die Remotedesktopverbindung speichern.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067301)

   **Standardeinstellung:** Aktiviert

- **Sichere RPC-Kommunikation**:  
  Diese Richtlinieneinstellung legt fest, ob für einen Remotedesktopsitzungs-Hostserver die sichere RPC-Kommunikation mit allen Clients erforderlich bzw. ob die unsichere Kommunikation zulässig ist. Mit dieser Einstellung können Sie die Sicherheit der RPC-Kommunikation mit Clients verbessern, indem Sie nur authentifizierte und verschlüsselte Anforderungen zulassen. Wenn die Einstellung aktiviert ist, akzeptieren Remotedesktopdienste Anforderungen von RPC-Clients, die sichere Anforderungen unterstützen, und unterstützen keine unsichere Kommunikation mit nicht vertrauenswürdigen Clients. Wenn die Einstellung deaktiviert ist, muss der gesamte RPC-Datenverkehr für Remotedesktopdienste immer sicher sein. Für RPC-Clients, die nicht auf die Anforderung reagieren, ist jedoch eine unsichere Kommunikation zulässig. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, ist die unsichere Kommunikation zulässig. Anmerkung: Die RPC-Schnittstelle wird zum Verwalten und Konfigurieren der Remotedesktopdienste verwendet.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067248)

  **Standardeinstellung:** Aktiviert

- **Laufwerkumleitung blockieren**:  
  Mit dieser Richtlinieneinstellung wird festgelegt, ob die Zuordnung von Clientlaufwerken während einer Remotedesktopdienst-Sitzung (Laufwerkumleitung) verhindert werden soll. Remotedesktopdienst-Hostserver ordnen Clientlaufwerke standardmäßig beim Herstellen der Verbindung automatisch zu. Zugeordnete Laufwerke werden in der Sitzungsordnerstruktur im Datei-Explorer oder auf dem Computer im Format *\<driveletter>* auf *\<computername>* angezeigt. Mit dieser Richtlinieneinstellung können Sie dieses Verhalten überschreiben. Wenn Sie diese Richtlinieneinstellung aktivieren, ist die Umleitung von Clientlaufwerken in Remotedesktopdienst-Sitzungen nicht zulässig, und die Zwischenablageumleitung beim Kopieren von Dateien ist auf Computern unter Windows Server 2003, Windows 8 und Windows XP nicht zulässig. Wenn Sie diese Richtlinieneinstellung deaktivieren, ist die Umleitung von Clientlaufwerken immer zulässig. Außerdem ist die Zwischenablageumleitung beim Kopieren von Dateien immer zulässig, wenn die Zwischenablageumleitung zulässig ist. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, werden die Umleitung von Clientlaufwerken und die Zwischenablageumleitung beim Kopieren von Dateien nicht auf Gruppenrichtlinienebene festgelegt.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067197)

  **Standardeinstellung:** Aktiviert

- **Bei Verbindungsherstellung zur Kennworteingabe auffordern**:  
  Diese Richtlinieneinstellung legt fest, ob Remotedesktopdienste beim Herstellen einer Verbindung immer ein Kennwort vom Client anfordern. Mit dieser Einstellung können Sie erzwingen, dass Benutzer, die sich bei Remotedesktopdiensten anmelden, selbst dann zur Eingabe eines Kennworts aufgefordert werden, wenn sie das Kennwort bereits im Remotedesktopverbindungs-Client angegeben haben. Remotedesktopdienste lassen standardmäßig zu, dass Benutzer sich automatisch anmelden, indem sie ein Kennwort im Remotedesktopverbindungs-Client eingeben. Wenn Sie diese Richtlinieneinstellung aktivieren, können sich Benutzer nicht automatisch bei Remotedesktopdiensten anmelden, indem sie ihr Kennwort im Remotedesktopverbindungs-Client eingeben. Sie müssen bei der Anmeldung ein Kennwort eingeben. Wenn Sie diese Richtlinieneinstellung deaktivieren, können Benutzer sich immer automatisch bei Remotedesktopdiensten anmelden, indem sie ihr Kennwort im Remotedesktopverbindungs-Client eingeben. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, wird die automatische Anmeldung nicht auf Gruppenrichtlinienebene festgelegt.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067328)

  **Standardeinstellung:** Aktiviert

- **Verschlüsselungsstufe für Remotedesktopdienste-Clientverbindung**:  
  Mit dieser Richtlinieneinstellung wird festgelegt, ob eine bestimmte Verschlüsselungsstufe zum Schutz der Kommunikation zwischen Clientcomputern und RD-Sitzungshostservern während RDP-Verbindungen (Remotedesktopprotokoll) erforderlich ist. Diese Richtlinie gilt nur, wenn Sie die native RDP-Verschlüsselung verwenden. Allerdings wird von der Verwendung der nativen RDP-Verschlüsselung (im Gegensatz zur SSL-Verschlüsselung) abgeraten. Diese Richtlinie gilt nicht für die SSL-Verschlüsselung. Wenn Sie diese Richtlinieneinstellung aktivieren, muss für die gesamte Kommunikation zwischen Clients und RD-Sitzungshostservern während Remoteverbindungen die in dieser Einstellung festgelegte Verschlüsselungsmethode verwendet werden. Die Verschlüsselungsstufe ist standardmäßig auf „Hoch“ festgelegt. Die folgenden Verschlüsselungsmethoden stehen zur Verfügung:

  - *Hoch*: Mit der Einstellung „Hoch“ werden zwischen dem Client und dem Server gesendete Daten mit einer starken 128-Bit-Verschlüsselung verschlüsselt. Verwenden Sie diese Verschlüsselungsstufe in Umgebungen, die nur 128-Bit-Clients enthalten (z.B. Clients mit Remotedesktopverbindung). Clients, die diese Verschlüsselungsstufe nicht unterstützen, können keine Verbindung mit RD-Sitzungshostservern herstellen.

  - *Clientkompatibel*: Mit der Einstellung „Clientkompatibel“ werden zwischen dem Client und dem Server gesendete Daten mit der vom Client unterstützten maximalen Schlüsselstärke verschlüsselt. Verwenden Sie diese Verschlüsselungsstufe für Umgebungen mit Clients, die keine 128-Bit-Verschlüsselung unterstützen.

  - *Niedrig*: Mit der Einstellung „Niedrig“ werden nur vom Client an den Server gesendete Daten mithilfe der 56-Bit-Verschlüsselung verschlüsselt.  
  
  Wenn Sie diese Einstellung deaktivieren oder nicht konfigurieren, wird die für Remoteverbindungen mit RD-Sitzungshostservern zu verwendende Verschlüsselungsstufe nicht über Gruppenrichtlinien erzwungen. Wichtig: die FIPS-Konformität (Federal Information Processing Standard) kann mithilfe der Systemkryptografie konfiguriert werden. Verwenden Sie FIPS-konforme Algorithmen für die Verschlüsselung, das Hashing und das Signieren von Einstellungen in der Gruppenrichtlinie (unter Computer Configuration\Windows Settings\Security Settings\Local Policies\Security Options). Mit der FIPS-konformen Einstellung werden Daten, die vom Client an den Server und vom Server an den Client gesendet werden, mit Verschlüsselungsalgorithmen gemäß FIPS 140 mithilfe von kryptografischen Modulen von Microsoft verschlüsselt und entschlüsselt. Verwenden Sie diese Verschlüsselungsstufe, wenn die Kommunikation zwischen Clients und RD-Sitzungshostservern die höchste Verschlüsselungsstufe erfordert.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067222)

  **Standardeinstellung:** Hoch

## <a name="remote-management"></a>Remoteverwaltung

Weitere Informationen finden Sie unter [Policy CSP – RemoteManagement (Richtlinien-Konfigurationsdienstanbieter: RemoteManagement)](/windows/client-management/mdm/policy-csp-remotemanagement) in der Windows-Dokumentation.

- **Speichern der RunAs-Anmeldeinformationen blockieren**:  
  Standardclientauthentifizierung.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067300)

  **Standardeinstellung:** Aktiviert

- **Standardauthentifizierung**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob der Windows-Remoteverwaltungsdienst (Windows Remote Management, WinRM) die Standardauthentifizierung von einem Remoteclient akzeptiert. Wenn Sie diese Richtlinieneinstellung aktivieren, akzeptiert der WinRM-Dienst die Standardauthentifizierung von einem Remoteclient. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, akzeptiert der WinRM-Dienst keine Standardauthentifizierung von einem Remoteclient.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067223)

  **Standardeinstellung:** Deaktiviert

- **Clientdigestauthentifizierung blockieren**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob der Windows-Remoteverwaltungsclient die Digestauthentifizierung verwendet. Wenn Sie diese Richtlinieneinstellung aktivieren, verwendet der WinRM-Client keine Digestauthentifizierung. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, verwendet der WinRM-Client die Digestauthentifizierung.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067302)

  **Standardeinstellung:** Aktiviert

- **Unverschlüsselter Datenverkehr**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob der WinRM-Dienst unverschlüsselte Nachrichten über das Netzwerk sendet und empfängt. Wenn Sie diese Richtlinieneinstellung aktivieren, sendet und empfängt der WinRM-Client unverschlüsselte Nachrichten über das Netzwerk. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, sendet und empfängt der WinRM-Client nur verschlüsselte Nachrichten über das Netzwerk.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067226)

  **Standardeinstellung:** Deaktiviert

- **Unverschlüsselter Clientdatenverkehr**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob der WinRM-Client unverschlüsselte Nachrichten über das Netzwerk sendet und empfängt. Wenn Sie diese Richtlinieneinstellung aktivieren, sendet und empfängt der WinRM-Client unverschlüsselte Nachrichten über das Netzwerk. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, sendet und empfängt der WinRM-Client nur verschlüsselte Nachrichten über das Netzwerk.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067304)

  **Standardeinstellung:** Deaktiviert

- **Standardclientauthentifizierung**:  
  Mit dieser Richtlinieneinstellung können Sie bestimmen, ob der WinRM-Client die Standardauthentifizierung verwendet. Wenn Sie diese Richtlinieneinstellung aktivieren, verwendet der WinRM-Client die Standardauthentifizierung. Wenn WinRM für die Verwendung des HTTP-Transports konfiguriert ist, werden der Benutzername und das Kennwort unverschlüsselt über das Netzwerk übertragen. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, verwendet der WinRM-Client die Standardauthentifizierung nicht.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067252)

  **Standardeinstellung:** Deaktiviert

## <a name="remote-procedure-call"></a>Remoteprozeduraufruf

Weitere Informationen finden Sie unter [Policy CSP – RemoteProcedureCall (Richtlinien-Konfigurationsdienstanbieter: RemoteProcedureCall)](/windows/client-management/mdm/policy-csp-remoteprocedurecall) in der Windows-Dokumentation.

- **Optionen für nicht authentifizierte RPC-Clients**:  
  Diese Richtlinieneinstellung steuert, wie die RPC-Server-Runtime nicht authentifizierte RPC-Clients behandelt, die sich mit RPC-Servern verbinden. Diese Richtlinieneinstellung betrifft alle RPC-Anwendungen. Verwenden Sie diese Richtlinieneinstellung in einer Domänenumgebung mit Vorsicht, da sie eine Vielzahl von Funktionen, darunter auch die Gruppenrichtlinienverarbeitung selbst, beeinträchtigen kann. Um nach einer Änderung die Richtlinieneinstellung wiederherzustellen, kann ein manueller Eingriff auf jedem betroffenen Computer erforderlich sein. Verwenden Sie diese Richtlinieneinstellung nicht für Domänencontroller. Wenn Sie diese Richtlinieneinstellung deaktivieren, verwendet die RPC-Server-Runtime den Wert für „Authenticated“ (Authentifiziert) auf dem Windows-Client und den Wert für „None“ (Keine Authentifizierung) auf Windows-Server-Versionen, die diese Richtlinieneinstellung unterstützen. Wenn Sie diese Richtlinieneinstellung nicht konfigurieren, bleibt sie deaktiviert. Die RPC-Server-Runtime verhält sich so, als wäre sie aktiviert mit dem für Windows-Clients verwendeten Wert für „Authenticated“ (Authentifiziert) und dem für Server-SKUs verwendeten Wert für „None“ (Keine Authentifizierung), die diese Richtlinieneinstellung unterstützen. Wenn Sie diese Richtlinieneinstellung aktivieren, wird die RPC-Server-Runtime angewiesen, nicht authentifizierte RPC-Clients, die sich mit RPC-Servern verbinden, welche auf einem Computer ausgeführt werden, einzuschränken. Ein Client gilt als authentifizierter Client, wenn er für die Kommunikation mit dem Server eine benannte Pipe verwendet, oder wenn er RPC-Sicherheit verwendet. RPC-Schnittstellen, die speziell den Zugriff durch nicht authentifizierte Clients angefordert haben, können von dieser Einschränkung ausgenommen werden, abhängig von dem für diese Richtlinieneinstellung gewählten Wert.

  - Durch *None* (Keine Authentifzierung) wird allen RPC-Clients gestattet, sich mit RPC-Servern zu verbinden, die auf dem Computer ausgeführt werden, auf den die Richtlinieneinstellung angewandt wird.

  - Durch *Authenticated* (Authentifiziert) wird nur authentifizierten RPC-Clients (per oben stehender Definition) gestattet, sich mit RPC-Servern zu verbinden, die auf dem Computer ausgeführt werden, auf den die Richtlinieneinstellung angewandt wird. Ausnahmen werden für Schnittstellen gewährt, die solche angefordert haben.

  - Durch *Authenticated without exceptions* (Authentifiziert ohne Ausnahmen) wird nur authentifizierten RPC-Clients (per oben stehender Definition) gestattet, sich mit RPC-Servern zu verbinden, die auf dem Computer ausgeführt werden, auf den die Richtlinieneinstellung angewandt wird. Ausnahmen sind nicht zulässig. Anmerkung: Diese Richtlinieneinstellung wird erst angewendet, wenn das System neu gestartet wird.

  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067225)

  **Standardeinstellung:** Authentifiziert

## <a name="search"></a>Suchen

Weitere Informationen finden Sie unter [Policy CSP - Search (Richtlinien-Konfigurationsdienstanbieter: Search)](/windows/client-management/mdm/policy-csp-search) in Ihrer Windows-Dokumentation.

- **Indizierung verschlüsselter Elemente deaktivieren**:  
  Hiermit wird die Indizierung von Elementen zugelassen oder verweigert. Diese Option ist für die Windows Search-Indexerstellung bestimmt und steuert, ob verschlüsselte Elemente wie beispielsweise WIP-geschützte Dateien (Windows Information Protection) indiziert werden. Wenn die Richtlinie aktiviert ist, werden WIP-geschützte Elemente indiziert und die zugehörigen Metadaten werden an einem nicht verschlüsselten Speicherort gespeichert. Die Metadaten umfassen beispielsweise den Dateipfad und das Änderungsdatum. Wenn die Richtlinie deaktiviert ist, werden WIP-geschützte Elemente nicht indiziert und sie werden nicht in den Ergebnissen in Cortana oder im Datei-Explorer angezeigt. Ferner sind bei Fotos und Groove-Apps Leistungseinbußen möglich, wenn sich auf dem Gerät große Mengen an WIP-geschützten Mediendateien befinden.  
  [Erfahren Sie mehr]( https://go.microsoft.com/fwlink/?linkid=2067303)

  **Standardeinstellung:** Ja

## <a name="smart-screen"></a>SmartScreen

Weitere Informationen finden Sie unter [Policy CSP - SmartScreen (Richtlinien-Konfigurationsdienstanbieter: SmartScreen)](/windows/client-management/mdm/policy-csp-smartscreen) in Ihrer Windows-Dokumentation.

::: zone-end
::: zone pivot="mdm-preview"

- **Ausführen nicht überprüfter Dateien blockieren**:  
  Hindern Sie Benutzer am Ausführen von nicht überprüften Dateien.

  - *Nicht konfiguriert*: Mitarbeiter können SmartScreen-Warnungen ignorieren und schädliche Dateien ausführen.

  - *Ja*: Mitarbeiter können SmartScreen-Warnungen nicht ignorieren und keine schädlichen Dateien ausführen.

  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067228)

  **Standardeinstellung:** Ja

- **SmartScreen für Apps und Dateien anfordern**:  
  Ermöglicht IT-Administratoren das Konfigurieren von SmartScreen für Windows.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067168)

  **Standardeinstellung:** Ja

::: zone-end
::: zone pivot="mdm-may-2019"

- **Windows SmartScreen aktivieren**  
  CSP: [SmartScreen/EnableSmartScreenInShell](https://go.microsoft.com/fwlink/?linkid=872784)

  Wenn „Ja“ festgelegt ist, wird die Verwendung von SmartScreen wird für alle Benutzer erzwungen. Wenn „Nicht konfiguriert“ festgelegt ist, wird die Einstellung auf den Standardwert von Windows zurückgesetzt, d. h., SmartScreen ist aktiviert. Der Benutzer kann diese Einstellung jedoch ändern. Verwenden Sie einen benutzerdefinierten URI, um SmartScreen zu deaktivieren.

  **Standardeinstellung:** Ja

- **Ignorieren von SmartScreen-Warnungen durch die Benutzer blockieren**  
  CSP: [SmartScreen/PreventOverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

  Wenn „Ja“ festgelegt wird, wird SmartScreen aktiviert und Benutzer können Warnungen für Dateien oder bösartige Apps nicht umgehen. Wenn „Nicht konfiguriert“ festgelegt wird, können Benutzer SmartScreen-Warnungen für Dateien ignorieren und schädliche Apps ausführen.  

  Diese Einstellung erfordert, dass die Einstellung „Windows SmartScreen aktivieren“ auf „Ja“ festgelegt ist.

  **Standardeinstellung:** Ja

::: zone-end
::: zone pivot="mdm-preview,mdm-may-2019"

## <a name="system"></a>System

Weitere Informationen finden Sie unter [Policy CSP - System (Richtlinien-Konfigurationsdienstanbieter: System)](/windows/client-management/mdm/policy-csp-system) in Ihrer Windows-Dokumentation.

- **Starttreiberinitialisierung für Systemstart**:  
  Mit dieser Richtlinieneinstellung können Sie angeben, welche Bootstarttreiber initialisiert werden. Dies geschieht basierend auf einer durch den Bootstarttreiber für den Antischadsoftware-Frühstart festgelegten Klassifizierung. Der Bootstarttreiber für den Antischadsoftware-Frühstart kann die folgenden Klassifizierungen für die einzelnen Bootstarttreiber zurückgeben:

  - *Gut*: Der Treiber wurde signiert und nicht manipuliert.

  - *Schlecht:* Der Treiber wurde als Schadsoftware identifiziert. Wir empfehlen, die Initialisierung von bekannten schlechten Treibern nicht zuzulassen.

  - *Schlecht, doch für den Bootvorgang erforderlich*: Der Treiber wurde als Schadsoftware identifiziert, doch der Computer kann nicht erfolgreich gestartet werden, ohne diesen Treiber zu laden.

  - *Unbekannt*: Dieser Treiber wurde von Ihrer Anwendung zur Erkennung von Schadsoftware nicht bestätigt und vom Bootstarttreiber für den Antischadsoftware-Frühstart nicht klassifiziert.

  Wenn Sie diese Richtlinieneinstellung aktivieren, können Sie auswählen, welche Bootstarttreiber beim nächsten Start des Computers initialisiert werden sollen. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, werden die guten, unbekannten oder schlechten, aber für den Bootvorgang erforderlichen Bootstarttreiber initialisiert. Die Initialisierung von schlechten Treibern wird übersprungen. Falls Ihre Anwendung für die Erkennung von Schadsoftware keinen Bootstarttreiber für den Antischadsoftware-Frühstart enthält oder dieser Treiber deaktiviert wurde, ist diese Richtlinieneinstellung wirkungslos, und alle Bootstarttreiber werden initialisiert.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067307)

  **Standardeinstellung:** Gut, unbekannt und schlecht, aber erforderlich

## <a name="wi-fi"></a>WLAN

Weitere Informationen finden Sie unter [Policy CSP - Wifi (Richtlinien-Konfigurationsdienstanbieter: Wifi)](/windows/client-management/mdm/policy-csp-wifi) in Ihrer Windows-Dokumentation.

- **Internetfreigabe blockieren**:  
  Gibt an, ob die Internetfreigabe auf dem Gerät möglich ist.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067327)

  **Standardeinstellung:** Ja

- **Automatisches Verbinden mit WLAN-Hotspots blockieren**:  
  Gestattet oder verweigert das automatische Verbinden des Geräts mit WLAN-Hotspots.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067320)

  **Standardeinstellung:** Ja

## <a name="windows-connection-manager"></a>Windows-Verbindungs-Manager

Weitere Informationen finden Sie unter [Policy CSP - WindowsConnectionManager (Richtlinien-Konfigurationsdienstanbieter: WindowsConnectionManager)](/windows/client-management/mdm/policy-csp-windowsconnectionmanager) in Ihrer Windows-Dokumentation.

- **Verbindung zu Nicht-Domänennetzwerken blockieren**:  
  Diese Richtlinieneinstellung verhindert, dass Computer gleichzeitig eine Verbindung zu einem domänenbasierten Netzwerk und zu einem nicht-domänenbasierten Netzwerk herstellen. Wenn diese Richtlinieneinstellung aktiviert ist, reagiert der Computer, abhängig von den folgenden Situationen, wie folgt auf automatische und manuelle Versuche, eine Netzwerkverbindung herzustellen:

  - *Automatische Verbindungsversuche*: Wenn der Computer bereits mit einem domänenbasierten Netzwerk verbunden ist, werden alle automatischen Verbindungsversuche zu nicht-domänenbasierten Netzwerken blockiert. Wenn der Computer bereits mit einem nicht-domänenbasierten Netzwerk verbunden ist, werden automatische Verbindungsversuche zu domänenbasierten Netzwerken blockiert.

  - *Manuelle Verbindungsversuche*: Wenn der Computer bereits mit einem nicht-domänenbasierten Netzwerk oder einem domänenbasierten Netzwerk über andere Medien als Ethernet verbunden ist, und ein Benutzer versucht, entgegen dieser Richtlinieneinstellung eine manuelle Verbindung zu einem zusätzlichen Netzwerk herzustellen, wird die bestehende Netzwerkverbindung abgebrochen und die manuelle Verbindung gestattet. Wenn der Computer bereits mit einem nicht-domänenbasierten Netzwerk oder einem domänenbasierten Netzwerk über Ethernet verbunden ist, und ein Benutzer versucht, entgegen dieser Richtlinieneinstellung eine manuelle Verbindung zu einem zusätzlichen Netzwerk herzustellen, wird die bestehende Ethernet-Verbindung gehalten und der manuelle Verbindungsversuch wird blockiert.

  Wenn diese Richtlinieneinstellung nicht konfiguriert oder deaktiviert wird, ist es zulässig, dass Computer gleichzeitig eine Verbindung mit einem Domänen- und einem Nicht-Domänennetzwerk herstellen.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067323)

  **Standardeinstellung:** Aktiviert

::: zone-end
::: zone pivot="mdm-may-2019"

## <a name="windows-hello-for-business"></a>Windows Hello for Business

- **Windows Hello for Business blockieren**  
  Windows Hello for Business ist eine alternative Methode zum Anmelden bei Windows durch Ersetzen von Kennwörtern, Smartcards und virtuellen Smartcards. Wenn Sie diese Richtlinieneinstellung deaktivieren oder nicht konfigurieren, stellt das Gerät Windows Hello for Business bereit. Wenn Sie diese Richtlinieneinstellung aktivieren, stellt das Gerät Windows Hello for Business für keinen Benutzer bereit.

  **Standardeinstellung:** Aktiviert
  
  Wenn *Deaktiviert* festgelegt ist, können Sie die folgenden Einstellungen konfigurieren:

  - **PIN-Mindestlänge**  
    Die PIN-Mindestlänge muss zwischen 4 und 127 Zeichen liegen.

    **Standardeinstellung:** *Nicht konfiguriert*

  - **Aktivieren Sie diese Option, um erweitertes Antispoofing zu verwenden, falls verfügbar:**  
    [Anti-spoofing protection](https://go.microsoft.com/fwlink/?linkid=2067192) (Schutz vor Spoofing)

    Wenn diese Option aktiviert ist, verwenden Geräte erweitertes Antispoofing, falls verfügbar. Wenn sie nicht konfiguriert ist, wird die Clientkonfiguration für Antispoofing verwendet.

    **Standardeinstellung:** Nicht konfiguriert

  - **Kleinbuchstaben in PIN**:  
    Wenn diese Option als erforderlich festgelegt ist, muss die Benutzer-PIN mindestens einen Kleinbuchstaben enthalten.

    **Standardeinstellung:** Nicht zulässig

  - **Sonderzeichen in PIN**:  
    Wenn diese Option als erforderlich festgelegt ist, muss die Benutzer-PIN mindestens ein Sonderzeichen enthalten.

    **Standardeinstellung:** Nicht zulässig
 

  - **Großbuchstaben in PIN**:  
    Wenn diese Option als erforderlich festgelegt ist, muss die Benutzer-PIN mindestens einen Großbuchstaben enthalten.

    **Standardeinstellung:** Nicht zulässig

::: zone-end
::: zone pivot="mdm-preview,mdm-may-2019"

## <a name="windows-ink-workspace"></a>Windows Ink-Arbeitsbereich

Weitere Informationen finden Sie unter [Policy CSP - WindowsInkWorkspace (Richtlinien-Konfigurationsdienstanbieter - WindowsInkWorkspace)](/windows/client-management/mdm/policy-csp-windowsinkworkspace) in Ihrer Windows-Dokumentation.

- **Ink-Arbeitsbereich:**  
  Gibt an, ob der Benutzer auf den Ink-Arbeitsbereich zugreifen darf.

  - *Deaktiviert*: Der Zugriff auf den Ink-Arbeitsbereich ist deaktiviert. Die Funktion ist deaktiviert.

  - *Aktiviert*: Der Ink-Arbeitsbereich ist aktiviert, aber der Benutzer kann nicht über den Sperrbildschirm darauf zugreifen.

  - *Nicht konfiguriert* – Der Ink-Arbeitsbereich ist aktiviert, und der Benutzer kann über den Sperrbildschirm darauf zugreifen.

  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067241)

  **Standardeinstellung:** Aktiviert

## <a name="windows-powershell"></a>Windows PowerShell

Weitere Informationen finden Sie unter [Policy CSP - WindowsPowerShell (Richtlinien-Konfigurationsdienstanbieter - WindowsPowerShell)](/windows/client-management/mdm/policy-csp-windowspowershell) in Ihrer Windows-Dokumentation.

- **Protokollierung von PowerShell-Skriptblöcken:**  
  Mit dieser Richtlinieneinstellung können alle PowerShell-Skript-Eingaben im Microsoft-Windows-PowerShell/Operational-Ereignisprotokoll protokolliert werden. Wenn Sie diese Richtlinieneinstellung aktivieren, protokolliert Windows PowerShell die Verarbeitung von Befehlen, Skriptblöcken, Funktionen und Skripts, unabhängig davon, ob diese interaktiv oder automatisch aufgerufen wurden. Wenn Sie diese Richtlinieneinstellung deaktivieren, ist das Protokollieren von PowerShell-Skript-Eingaben deaktiviert. Wenn Sie die Protokollierung von Skriptblockaufrufen aktivieren, protokolliert PowerShell zusätzlich Protokollereignisse, wenn ein Befehl, ein Skriptblock, eine Funktion oder Skriptstarts oder -stops aufgerufen werden. Das Aktivieren der Protokollierung von Aufrufen führt zu einer großen Anzahl von Ereignisprotokollen. Anmerkung: Diese Richtlinieneinstellung ist sowohl unter„Computerkonfiguration“ als auch unter „Benutzerkonfiguration“ im Editor für Gruppenrichtlinien vorhanden. Die Richtlinieneinstellung in der Computerkonfiguration hat Vorrang vor der Richtlinieneinstellung in der Benutzerkonfiguration.  
  [Erfahren Sie mehr](https://go.microsoft.com/fwlink/?linkid=2067330)

  **Standardeinstellung:** Aktiviert

::: zone-end
::: zone pivot="mdm-may-2019"

## <a name="whats-changed-in-the-new-template"></a>Eigenschaften der neuen Vorlage

Die Vorlage *MDM-Sicherheitsbaseline für Mai 2019* enthält die folgenden Änderungen im Vergleich zur *Vorschauversion* der Vorlage.

### <a name="changes-to-the-baseline-settings"></a>Änderungen der Baselineeinstellungen

Die folgenden Einstellungen sind entweder:

- *Neu* in der aktuellen Version der Baseline
- Aus der neuesten Baselineversion *entfernt*, aber in der Vorgängerversion enthalten
- Auf irgendeine Weise im Vergleich zu den Einstellungen in der Vorgängerversion *überarbeitet*

*[Neu]* [**Oberhalb von Sperrbildschirm:** ](#above-lock)

- **Sprachaktivierung von Apps über Sperrbildschirm**

*[Neu]* [**Anwendungsverwaltung:** ](#application-management)

- **Benutzerkontrolle über Installationen blockieren**
- **MSI-App-Installationen mit erhöhten Rechten blockieren**

*[Entfernt]* [**BitLocker**](#bitlocker):

- BitLocker: Richtlinie für Wechseldatenträger > **Verschlüsselungsmethode**
- **BitLocker: Richtlinie für Festplattenlaufwerk** *(alle Einstellungen)*
- **BitLocker: Richtlinie für Systemlaufwerk** *(alle Einstellungen)*

*[Neu]* [**Konnektivität:** ](#connectivity)

- **Sicheren Zugriff auf UNC-Pfade konfigurieren**

*[Neu]* [**Device Guard:** ](#device-guard)

- **Virtualisierungsbasierte Sicherheit**

*[Neu]* [**DMA Guard:** ](#dma-guard)

- **Aufzählung externer Geräte, die mit Kernel-DMA-Schutz nicht kompatibel sind**

*[Neu]* [**Internet Explorer:** ](#internet-explorer)

- **Internet Explorer internet zone updates to status bar via script** (Skriptgesteuerte Updates für die Statusleiste in der Internetzone von Internet Explorer)
- **Internet Explorer internet zone drag and drop or copy and paste files** (Drag & Drop oder Kopieren und Einfügen von Dateien in einer Internetzone in Internet Explorer)
- **Internet Explorer restricted zone .NET Framework reliant components** (.NET Framework-Komponenten in eingeschränkten Zonen von Internet Explorer)
- **Internet Explorer local machine zone do not run antimalware against Active X controls** (Keine Antischadsoftwareprogramme für ActiveX-Steuerelemente in lokaler Computerzone in Internet Explorer ausführen)
- **Internet Explorer: Verschlüsselungsunterstützung**

*[Überarbeitet]* [**Internet Explorer**](#internet-explorer):

- **Internet Explorer: Internetzone: Automatische Aufforderung für Dateidownloads** > Der Standardwert ist nun **Deaktiviert**. In der Vorschauversion war diese Einstellung auf „Aktiviert“ festgelegt.

*[New]* [**Remoteunterstützung:** ](#remote-assistance)

- **Angeforderte Remoteunterstützung**
  - **Angeforderte Remoteunterstützung: Berechtigung**
  - **Maximaler Zeitwert des Tickets**
  - **Maximaler Ticketzeitraum**
  - **E-Mail-Einladungsmethode**

*[Neu]* [**Microsoft Defender:** ](#microsoft-defender)

- **Adobe Reader launch in a child process** (Adobe Reader in einem untergeordneten Prozess starten)
- **Office communication apps launch in a child process** (Office-Kommunikations-Apps in einem untergeordneten Prozess starten)

*[Neu]* [ **Firewall**](#firewall)

- **Firewallprofil: Domäne**
  - **Eingehende Verbindungen blockiert**
  - **Ausgehende Verbindungen erforderlich**
  - **Eingehende Benachrichtigungen blockiert**
  - **Firewall aktiviert**
- **Firewallprofil: öffentlich**
  - **Eingehende Verbindungen blockiert**
  - **Ausgehende Verbindungen erforderlich**
  - **Eingehende Benachrichtigungen blockiert**
  - **Firewall aktiviert**
  - **Verbindungssicherheitsregeln aus Gruppenrichtlinie nicht zusammengeführt**
  - **Richtlinienregeln aus Gruppenrichtlinie nicht zusammengeführt**
- **Firewallprofil: privat**
  - **Eingehende Verbindungen blockiert**
  - **Ausgehende Verbindungen erforderlich**
  - **Eingehende Benachrichtigungen blockiert**
  - **Firewall aktiviert**

*[Neu]* [**Windows Hello for Business**](#windows-hello-for-business):

- **Erweitertes Antispoofing erfordern, falls verfügbar**:
- **Konfigurieren von Windows Hello for Business**
- **Kleinbuchstaben in PIN vorschreiben**
- **Sonderzeichen in PIN vorschreiben**
- **PIN-Mindestlänge**
- **Großbuchstaben in PIN vorschreiben**

::: zone-end

## <a name="next-steps"></a>Nächste Schritte

- [Informationen zu Sicherheitsbaselines](security-baselines.md)
- [Vermeiden von Konflikten](security-baselines.md#avoid-conflicts)
- [Richtlinien und Profile zur Problembehandlung in Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)